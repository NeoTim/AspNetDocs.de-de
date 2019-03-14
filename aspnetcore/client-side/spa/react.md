---
title: Verwenden der React-Projektvorlage mit ASP.NET Core
author: SteveSandersonMS
description: Erfahren Sie, wie Sie sich mit der Projektvorlage für die Einzelseitenanwendung (Single-Page Application, SPA) von ASP.NET Core für React und create-react-app vertraut machen.
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/13/2019
uid: spa/react
ms.openlocfilehash: 3b2b2e67b5d577872bafefef5624a13ca1a22449
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026847"
---
# <a name="use-the-react-project-template-with-aspnet-core"></a>Verwenden der React-Projektvorlage mit ASP.NET Core

Die aktualisierte React-Projektvorlage stellt einen geeigneten Anfangspunkt für ASP.NET Core-Apps dar, die React und CRA-Konventionen ([create-react-app](https://github.com/facebookincubator/create-react-app)) für die Implementierung einer umfangreichen, clientseitigen Benutzerschnittstelle (User Interface, UI) verwenden.

Mit der Vorlage können ein ASP.NET Core-Projekt, das als API-Back-End fungieren soll, und ein CRA React-Projekt, das als Benutzeroberfläche fungieren soll, erstellt werden. Sie bietet jedoch den Komfort, dass beide Projekte in einem einzigen App-Projekt gehostet werden, das als eine Einheit erstellt und veröffentlicht werden kann.

## <a name="create-a-new-app"></a>Erstellen einer neuen App

Wenn ASP.NET Core 2.1 auf Ihrem Computer installiert ist, müssen Sie die Vorlage für React-Projekte nicht installieren.

Erstellen Sie über eine Eingabeaufforderung mit dem Befehl `dotnet new react` in einem leeren Verzeichnis ein neues Projekt. Mit den folgenden Befehlen wird die App beispielsweise im Verzeichnis *my-new-app* erstellt und zu diesem Verzeichnis gewechselt:

```console
dotnet new react -o my-new-app
cd my-new-app
```

Führen Sie die App über Visual Studio oder die .NET Core CLI aus:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Öffnen Sie die generierte *CSPROJ*-Datei, und führen Sie die App von dort wie gewohnt aus.

Während der Erstellung werden bei der ersten Ausführung npm-Abhängigkeiten wiederhergestellt. Dies kann einige Minuten dauern. Nachfolgende Builds sind wesentlich schneller.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Stellen Sie sicher, dass Sie über eine Umgebungsvariable mit dem Namen `ASPNETCORE_Environment` und dem Wert `Development` verfügen. Führen Sie unter Windows (bei Eingabeaufforderungen außerhalb von PowerShell) `SET ASPNETCORE_Environment=Development` aus. Führen Sie unter Linux oder macOS `export ASPNETCORE_Environment=Development` aus.

Führen Sie [dotnet build](/dotnet/core/tools/dotnet-build) aus, um zu überprüfen, ob Ihre App ordnungsgemäß erstellt wurde. Während der Erstellung werden bei der ersten Ausführung npm-Abhängigkeiten wiederhergestellt. Dies kann einige Minuten dauern. Nachfolgende Builds sind wesentlich schneller.

Führen Sie [dotnet run](/dotnet/core/tools/dotnet-run) aus, um die App zu starten.

---

Mit der Projektvorlage werden eine ASP.NET Core-App und eine React-App erstellt. Die ASP.NET Core-App ist für die Verwendung für den Datenzugriff, die Autorisierung und weitere serverseitige Belange vorgesehen. Die React-App, die sich im Unterverzeichnis *ClientApp* befindet, ist für sämtliche Belange der Benutzeroberfläche vorgesehen.

## <a name="add-pages-images-styles-modules-etc"></a>Hinzufügen von Seiten, Images, Formatvorlagen, Modulen usw.

Das Verzeichnis *ClientApp* ist eine CRA-React-Standard-App. Weitere Informationen finden Sie in der offiziellen [CRA-Dokumentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md).

Zwischen der React-App, die mit dieser Vorlage erstellt wurde, und der App, die von CRA selbst erstellt wurde, gibt es jedoch leichte Unterschiede; die Funktionen der App sind jedoch unverändert. Die mit der Vorlage erstellte App enthält ein auf [Bootstrap](https://getbootstrap.com/) basiertes Layout und ein Beispiel für grundlegendes Routing.

## <a name="install-npm-packages"></a>NPM-Pakete installieren

Verwenden Sie für die Installation von npm-Paketen von Drittanbietern eine Eingabeaufforderung im Unterverzeichnis *ClientApp*. Zum Beispiel:

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a>Veröffentlichen und Bereitstellen

Bei der Entwicklung wird die App in einem für Entwickler optimierten Modus ausgeführt. JavaScript-Pakete enthalten beispielsweise Quellzuordnungen (damit Sie beim Debuggen Ihren ursprünglichen Quellcode anzeigen können). Die App überwacht JavaScript-, HTML- und CSS-Dateiänderungen auf dem Datenträger und führt bei Feststellung dieser Dateiänderungen automatisch eine Neukompilierung und ein erneutes Laden durch.

Stellen Sie bei der Produktion eine für Leistung optimierte Version Ihrer App bereit. Dies erfolgt gemäß der Konfiguration automatisch. Beim Veröffentlichen gibt die Buildkonfiguration einen verkleinerten, transpilierten Build Ihres clientseitigen Codes aus. Im Gegensatz zum Entwicklungsbuild muss Node.js beim Produktionsbuild nicht auf dem Server installiert sein.

Sie können [ASP.NET Core-Standardhosting- und -bereitstellungsmethoden](xref:host-and-deploy/index) verwenden.

## <a name="run-the-cra-server-independently"></a>Unabhängiges Ausführen des CRA-Servers

Das Projekt ist so konfiguriert, dass die eigene Instanz des CRA-Entwicklungsservers im Hintergrund gestartet wird, wenn die ASP.NET Core-App im Entwicklungsmodus gestartet wird. Dies ist nützlich, da es bedeutet, dass Sie keinen separaten Server manuell ausführen müssen.

Bei diesem Standardsetup gibt es einen Nachteil. Jedes Mal, wenn Sie Ihren C#-Code ändern und Ihre ASP.NET Core-App neu gestartet werden muss, wird auch der CRA-Server neu gestartet. Es dauert einige Sekunden, bis der Sicherungsvorgang gestartet wird. Wenn Sie Ihren C#-Code häufig bearbeiten und nicht warten möchten, bis der CRA-Server neu gestartet wurde, können Sie den CRA-Server extern ausführen, unabhängig vom ASP.NET Core-Prozess. Gehen Sie hierzu wie folgt vor:

1. Hinzufügen einer *env* -Datei in die *ClientApp* Unterverzeichnis mit folgender Einstellung:

    ```
    BROWSER=none
    ```
    
    Dadurch wird Ihrem Webbrowser öffnen zu verhindern, dass beim Starten des Servers von CRA extern.

2. Wechseln Sie in einer Eingabeaufforderung zu dem Unterverzeichnis *ClientApp*, und starten Sie den CRA-Bereitstellungsserver:

    ```console
    cd ClientApp
    npm start
    ```

3. Ändern Sie Ihre ASP.NET Core-App so, dass die externe CRA-Serverinstanz verwendet wird, statt eine eigene Instanz zu starten. Ersetzen Sie den `spa.UseReactDevelopmentServer`-Aufruf in Ihrer *Startklasse* durch Folgendes:

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

Wenn Sie Ihre ASP.NET Core-App starten, wird kein CRA-Server gestartet. Stattdessen wird die Instanz verwendet, die Sie manuell gestartet haben. Dadurch kann sie schneller gestartet und neu gestartet werden. So müssen Sie nicht mehr jedes Mal warten, bis Ihre React-App neu erstellt wurde.

> [!IMPORTANT]
> "Serverseitiges Rendering" ist keine unterstützte Funktion dieser Vorlage. Unser Ziel mit dieser Vorlage ist Parität mit "create-React-app" zu erfüllen. Daher ist es möglich, Szenarien und Features, die nicht in einem Projekt "erstellen-React-app" (z. B. SSR) enthalten werden nicht unterstützt, und Sie bleiben als Übung für den Benutzer.
