---
uid: mvc/overview/deployment/docker-aspnetmvc
title: Migrieren von ASP.NET MVC-Anwendungen zu Windows-Containern
description: Erfahren Sie, wie Sie eine vorhandene ASP.NET MVC-Anwendung in einem Windows Docker-Container ausführen können.
keywords: Windows-Container, Docker, ASP. NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 1c5e6af79c87123891ddd4d30c60e3a427910e9d
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763492"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Migrieren von ASP.NET MVC-Anwendungen zu Windows-Containern

Wird eine vorhandene .NET Framework-basierte Anwendung in einem Windows-Container ausgeführt, sind keine Änderungen an der Anwendung erforderlich. Um die Anwendung in einem Windows-Container auszuführen, erstellen Sie ein Docker-Image, das die Anwendung enthält, und starten Sie den Container. In diesem Thema wird erläutert, wie eine vorhandene [ASP.NET MVC-Anwendung](http://www.asp.net/mvc) übernommen und in einem Windows-Container bereitgestellt wird.

Sie beginnen mit einer vorhandenen ASP.NET MVC-Anwendung und erstellen dann mit Visual Studio die veröffentlichten Objekte. Mithilfe von Docker erstellen Sie das Image, in dem die Anwendung enthalten ist und aus dem sie ausgeführt wird. Sie navigieren zu der Website, die in einem Windows-Container ausgeführt wird, und vergewissern sich, dass die Anwendung funktioniert.

In diesem Artikel werden grundlegende Kenntnisse von Docker vorausgesetzt. Weitere Informationen zu Docker finden Sie in der [Docker-Übersicht](https://docs.docker.com/engine/understanding-docker/).

Die Anwendung, die Sie in einem Container ausführen, ist eine einfache Website, die Fragen nach dem Zufallsprinzip beantwortet. Diese Anwendung ist eine grundlegende MVC-Anwendung ohne Authentifizierung oder Datenbankspeicher. Somit wird es Ihnen ermöglicht, sich auf das Verschieben der Webebene in einen Container zu konzentrieren. In zukünftigen Themen wird das Verschieben und Verwalten von beständigem Speicher in Containeranwendungen gezeigt.

Das Verschieben Ihrer Anwendung umfasst folgenden Schritte:

1. [Erstellen einer Veröffentlichungsaufgabe, um die Objekte für ein Image zu erstellen](#publish-script)
1. [Erstellen eines Docker-Images, das die Anwendung ausführt](#build-the-image)
1. [Starten eines Docker-Containers, der das Image ausführt](#start-a-container)
1. [Überprüfen der Anwendung mit Ihrem Browser](#verify-in-the-browser)

Die [fertige Anwendung](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/deployment/docker-aspnetmvc/samples/MVCRandomAnswerGenerator) finden Sie auf GitHub.

## <a name="prerequisites"></a>Voraussetzungen

Auf dem Entwicklungs Computer muss die folgende Software vorhanden sein:

- [Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (oder höher) oder [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (oder höher)
- [Docker für Windows](https://docs.docker.com/docker-for-windows/) -Version Stable 1.13.0 oder 1.12 Beta 26 (oder neuere Versionen)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Wenn Sie Windows Server 2016 verwenden, gehen Sie entsprechend den Anweisungen für [Containerhostbereitstellung: Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment) vor.

Klicken Sie nach dem Installieren und Starten von Docker mit der rechten Maustaste auf das Taskleistensymbol, und wählen Sie **Switch to Windows containers** (Zu Windows-Containern wechseln). Dies ist erforderlich, um Docker-Images auszuführen, die auf Windows basieren. Die Ausführung dieses Befehls dauert ein paar Sekunden:

![Windows-Container][windows-container]

## <a name="publish-script"></a>Veröffentlichen des Skripts

Sammeln Sie alle Ressourcen, die Sie in ein Docker-Image laden müssen, an einem Ort. Sie können den Visual Studio-Befehl **Veröffentlichen** verwenden, um ein Veröffentlichungsprofil für Ihre Anwendung zu erstellen. In diesem Profil sind alle Objekte in einer einzigen Verzeichnisstruktur untergebracht, die Sie später in diesem Tutorial in Ihr Zielimage kopieren.

**Veröffentlichungsschritte**

1. Klicken Sie mit der rechten Maustaste in Visual Studio auf das Webprojekt, und wählen Sie **Veröffentlichen**.
1. Klicken Sie auf die Schaltfläche **Benutzerdefiniertes Profil**, und wählen Sie **Dateisystem** als Methode aus.
1. Wählen Sie das Verzeichnis aus. Konventionsgemäß verwendet das heruntergeladene Beispiel `bin\Release\PublishOutput`.

![Veröffentlichungsverbindung][publish-connection]

Öffnen Sie den Abschnitt **Datei Veröffentlichungs Optionen** der Registerkarte **Einstellungen** . Wählen Sie **während der Veröffentlichung Vorkompilieren**. Diese Optimierung bedeutet, dass Sie beim Kompilieren von Ansichten im Docker-Container die vorkompilierten Ansichten kopieren.

![Veröffentlichungs Einstellungen][publish-settings]

Klicken Sie auf **Veröffentlichen**, und Visual Studio kopiert alle erforderlichen Objekte in den Zielordner.

## <a name="build-the-image"></a>Erstellen des Image

Erstellen Sie eine neue Datei namens *dockerfile* , um Ihr docker-Image zu definieren. Die *dockerfile-Datei* enthält Anweisungen zum Erstellen des endgültigen Bilds und enthält alle Basis Image Namen, erforderlichen Komponenten, die APP, die Sie ausführen möchten, und andere Konfigurations Images. *Dockerfile* ist die Eingabe für den `docker build` Befehl, der das Image erstellt.

In dieser Übung erstellen Sie ein Image, das auf dem Image basiert, das `microsoft/aspnet` sich auf dem [docker-Hub](https://hub.docker.com/r/microsoft/aspnet/)befindet.
Das Basisimage `microsoft/aspnet` ist ein Windows Server-Image. Sie enthält Windows Server Core, IIS und ASP.NET 4.7.2. Wenn Sie dieses Image im Container ausführen, werden IIS und die installierten Websites automatisch gestartet.

Die Dockerfile-Datei, die das Image erstellt, sieht folgendermaßen aus:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

In dieser Dockerfile-Datei ist kein `ENTRYPOINT`-Befehl enthalten. Ein solcher Befehl ist nicht erforderlich. Bei der Ausführung von Windows Server mit IIS ist der IIS-Prozess der Einstiegspunkt, der für den Start im ASPNET-Basis Image konfiguriert ist.

Führen Sie den Docker-Erstellungsbefehl aus, um das Image zu erstellen, über das die ASP.NET-Anwendung ausgeführt wird. Öffnen Sie zu diesem Zweck ein PowerShell-Fenster im Verzeichnis des Projekts, und geben Sie den folgenden Befehl in das Projektmappenverzeichnis ein:

```console
docker build -t mvcrandomanswers .
```

Mit diesem Befehl wird das neue Image mithilfe der Anweisungen in ihrer dockerfile-Datei erstellt, wobei das Image als "mvcrandomanswers" benannt wird. Dies kann beinhalten, dass Sie das Basisimage aus [Docker Hub](http://hub.docker.com) abrufen und dann Ihre Anwendung zu diesem Image hinzufügen müssen.

Nach Abschluss dieses Befehls können Sie den `docker images`-Befehl ausführen, um Informationen über das neue Image anzuzeigen:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

Die IMAGE-ID wird auf Ihrem Computer anders lauten. Führen Sie die Anwendung jetzt aus.

## <a name="start-a-container"></a>Starten eines Containers

Starten Sie mit folgendem `docker run`-Befehl einen Container:

```console
docker run -d --name randomanswers mvcrandomanswers
```

Das `-d`-Argument weist Docker an, das Image im getrennten Modus zu starten. Das bedeutet, dass das Docker-Image getrennt von der aktuellen Shell ausgeführt wird.

In vielen docker-Beispielen kann-p angezeigt werden, um den Container und die Hostports zuzuordnen. Das standardmäßige ASPNET-Image hat den Container bereits so konfiguriert, dass er an Port 80 lauscht und ihn verfügbar macht.

`--name randomanswers` gibt dem ausgeführten Container einen Namen. Sie können diesen Namen in den meisten Befehlen anstelle der Container-ID verwenden.

`mvcrandomanswers` ist der Name des zu startenden Images.

## <a name="verify-in-the-browser"></a>Überprüfen im Browser

Nachdem der Container gestartet wurde, stellen Sie eine Verbindung mit dem laufenden Container her, indem Sie `http://localhost` im gezeigten Beispiel verwenden. Wenn Sie diese URL in Ihren Browser eingeben, sollte die ausgeführte Website angezeigt werden.

> [!NOTE]
> Manche VPN- oder Proxysoftware könnte Ihren Wechsel zu Ihrer Website verhindern.
> Sie können diese Software vorübergehend deaktivieren, um sicherzustellen, dass der Container ausgeführt wird.

Das Beispielverzeichnis auf GitHub enthält ein [PowerShell-Skript](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1), das diese Befehle für Sie ausführt. Öffnen Sie ein PowerShell-Fenster, wechseln Sie in das Projektmappenverzeichnis, und geben Sie ein:

```console
./run.ps1
```

Der obige Befehl erstellt das Image, zeigt die Liste der Images auf dem Computer an und startet einen Container.

Um den Container zu stoppen, geben Sie einen `docker stop`-Befehl ein:

```console
docker stop randomanswers
```

Um den Container zu entfernen, geben Sie einen `docker rm`-Befehl ein:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Wechseln zu Windows-Container"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Im Dateisystem veröffentlichen"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Veröffentlichungs Einstellungen"
