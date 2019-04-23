---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Einrichten der Contact Manager-Lösung | Microsoft-Dokumentation
author: jrjlee
description: In diesem Thema wird beschrieben, wie zum Herunterladen und konfigurieren Sie die Projektmappe Contact Manager lokal auf einer Entwicklerarbeitsstation ausgeführt wird.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d0a7c29a590fcde504e5f5227806df62454f6add
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59410486"
---
# <a name="setting-up-the-contact-manager-solution"></a>Einrichten der Contact Manager-Lösung

durch [Jason Lee](https://github.com/jrjlee)

[PDF herunterladen](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> In diesem Thema wird beschrieben, wie zum Herunterladen und konfigurieren Sie die Projektmappe Contact Manager lokal auf einer Entwicklerarbeitsstation ausgeführt wird.


## <a name="system-requirements"></a>Systemanforderungen

Contact Manager-Lösung lokal ausführen und die anderen in diesem Lernprogramm beschriebene Aufgaben ausführen, müssen Sie zum Installieren der Software auf der Entwicklerarbeitsstation:

- Visual Studio 2010 Service Pack 1, Premium oder Ultimate Edition
- Internetinformationsdienste (IIS) 7.5 Express
- SQL Server Express 2008 R2
- IIS-Webbereitstellungstool (Web Deploy) 2.1 oder höher
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

Mit Ausnahme von Visual Studio 2010 können Sie herunterladen und installieren Sie die neuesten Versionen der Produkte und Komponenten über die [Webplattform-Installer](https://go.microsoft.com/?linkid=9805118).

## <a name="download-and-extract-the-solution"></a>Herunterladen Sie und extrahieren Sie die Lösung

Sie können die beispielanwendung Contact Manager aus der MSDN Code Gallery herunterladen [hier](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).

## <a name="configure-and-run-the-solution"></a>Konfigurieren und Ausführen der Lösung

Zum Konfigurieren und Contact Manager-Lösung auf Ihrem lokalen Computer ausführen, müssen Sie diese allgemeinen Schritte ausführen:

1. Wenn Sie eine noch nicht, erstellen Sie eine lokale Datenbank für ASP.NET-Anwendungsdienste die Mitgliedschafts- und Rollendatenbanken Management-Features aktiviert.
2. Bearbeiten von Verbindungszeichenfolgen in der *"Web.config"* Dateien, um auf Ihre lokale SQL Server Express-Instanz zu verweisen.
3. Führen Sie die Projektmappe von Visual Studio 2010.

Der übrige Teil dieses Abschnitts enthält weitere Anleitungen dazu, wie diese Aufgaben ausführen.

**Zum Erstellen der Anwendung-Services-Datenbank**

1. Öffnen Sie eine Visual Studio 2010-Eingabeaufforderung. Zu diesem Zweck die **starten** , zeigen Sie auf **Programme**, klicken Sie auf **Microsoft Visual Studio 2010**, klicken Sie auf **Visual Studio-Tools**, und klicken Sie dann Klicken Sie auf **Visual Studio-Eingabeaufforderung (2010)**.
2. Geben Sie folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. Verwenden der **-c** verwenden, um die Verbindungszeichenfolge für Ihren Datenbankserver anzugeben.
    2. Verwenden der **– ein** verwenden, um anzugeben, die Anwendung services-Funktionen, die Sie in der Datenbank hinzufügen möchten. In diesem Fall **m** gibt an, dass Sie zum Hinzufügen der Unterstützung für den Mitgliedschaftsanbieter und **r** gibt an, dass die Unterstützung für die Rollen-Manager hinzugefügt werden soll.
    3. Verwenden der **– d** verwenden, um einen Namen für die Anwendung-Services-Datenbank anzugeben. Wenn Sie diese Option weglassen, erstellt das Dienstprogramm eine Datenbank mit dem Standardnamen der **Aspnetdb**.
3. Wenn die Datenbank wurde erfolgreich erstellt wurde, wird der Eingabeaufforderung eine Bestätigung angezeigt.

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> Weitere Informationen zu den Aspnet\_Regsql Hilfsprogramm finden Sie unter [ASP.NET SQL Server-Registrierungstool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).


Der nächste Schritt ist, um sicherzustellen, dass die Verbindungszeichenfolgen in der Contact Manager-Lösung für Ihre lokale Instanz von SQL Server Express zeigen.

**Um die Verbindungszeichenfolgen zu aktualisieren.**

1. Öffnen Sie die Projektmappe Contact Manager, klicken Sie in Visual Studio 2010.
2. In der **Projektmappen-Explorer** Fenster, erweitern Sie die **ContactManager.Mvc** Projekt, und doppelklicken Sie dann auf die **"Web.config"** Knoten.

    > [!NOTE]
    > Das ContactManager.Mvc-Projekt enthält zwei *"Web.config"* Dateien. Sie müssen die Datei auf Projektebene bearbeiten.

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. In der **ConnectionStrings** -Element, stellen Sie sicher, dass die Verbindungszeichenfolge mit dem Namen **ApplicationServices** verweist auf Ihre lokale Datenbank für ASP.NET-Anwendungsdienste.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. In der **Projektmappen-Explorer** Fenster, erweitern Sie die **ContactManager.Service** Projekt, und doppelklicken Sie dann auf die **"Web.config"** Knoten.

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. In der **ConnectionStrings** Elements in der Verbindungszeichenfolge, die mit dem Namen **ContactManagerContext**, überprüfen Sie, ob die **Datenquelle** -Eigenschaftensatz auf Ihre lokale Instanz von SQL Server Express. Sie müssen nicht alles in der Verbindungszeichenfolge ändern.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. Speichern Sie alle geöffneten Dateien.

Sie sollten jetzt Contact Manager-Lösung auf Ihrem lokalen Computer ausführen können.

> [!NOTE]
> Wenn Sie folgende Schritte ausführen, ohne zuvor eine Datenbank, erstellt ASP.NET die Datenbank erstmals Sie versuchen, einen Benutzer zu erstellen. Allerdings haben Sie die Datenbank manuell erstellen Sie noch viel mehr Kontrolle über die Anwendung Dienste Funktionsgruppe, die Sie unterstützen möchten.


**Die Projektmappe Contact Manager ausführen**

1. Drücken Sie F5, klicken Sie in Visual Studio 2010.
2. Internet Explorer startet und die URL der Anwendung wenden Sie sich an Manager ASP.NET MVC 3-Anforderungen. Standardmäßig zeigt die Anwendung die **alle Kontakte** Seite.

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. Fügen Sie einige Kontakte, und stellen Sie sicher, dass die Anwendung wie erwartet funktioniert.

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. Navigieren Sie zu `http://localhost:50114/Account/Register` (passen Sie die URL aus, wenn Sie die Anwendung auf einen anderen Port hosten). Fügen Sie einen Benutzernamen, e-Mail-Adresse und Kennwort hinzu, und stellen Sie sicher, dass Sie ein Konto erfolgreich registrieren können.

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. Navigieren Sie zu `http://localhost:50114/Account/LogOn` (passen Sie die URL aus, wenn Sie die Anwendung auf einen anderen Port hosten). Stellen Sie sicher, dass Sie mit dem soeben erstellten Konto anmelden können.

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. Schließen Sie Internet Explorer zum Beenden des Debuggens.

## <a name="conclusion"></a>Schlussbemerkung

An diesem Punkt sollte Contact Manager-Lösung vollständig konfiguriert werden, führen Sie auf dem lokalen Computer. Sie können die Lösung als Verweis verwenden, wenn Sie über die anderen Themen in diesem Tutorial arbeiten.

Im nächsten Thema, [Grundlegendes zur Projektdatei](understanding-the-project-file.md), wird erläutert, wie Sie die benutzerdefinierte Microsoft Build Engine (MSBuild)-Projektdateien in der Contact Manager-Lösung verwenden können, um den Bereitstellungsprozess zu steuern.

> [!div class="step-by-step"]
> [Zurück](the-contact-manager-solution.md)
> [Weiter](understanding-the-project-file.md)
