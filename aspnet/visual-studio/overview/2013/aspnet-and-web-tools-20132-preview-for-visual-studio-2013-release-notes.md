---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET und Webtools 2013.2 für Visual Studio 2013 Versionshinweise | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543625"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET and Web Tools 2013.2 für Visual Studio 2013 – Anmerkungen zu dieser Version

von [Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>Installationshinweise

ASP.NET und Webtools für Visual Studio 2013.2 sind im Hauptinstallationsprogramm enthalten und können als Teil von [Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)heruntergeladen werden.

## <a name="documentation"></a>Dokumentation

Tutorials und weitere Informationen zu ASP.NET und Webtools für Visual Studio 2013.2 finden Sie auf der [website ASP.NET](https://www.asp.net/).

## <a name="software-requirements"></a>Softwareanforderungen

ASP.NET und Webtools für Visual Studio 2013.2 ist Visual Studio 2013 erforderlich.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Neue Funktionen in ASP.NET und Webtools für Visual Studio 2013.2

In den folgenden Abschnitten werden die Features beschrieben, die in der Version eingeführt wurden.

- [Eine ASP.NET Projektvorlagen](#oneaspnet)
- [Unterstützung von SSL beim Starten von Webanwendungen auf IIS Express](#ssl)
- [Verbesserungen des Visual Studio-Web-Editors](#vswebeditor)
- [Browserverknüpfung](#browserlink)
- [Unterstützung für Azure App Service-Web-Apps in Visual Studio](#waws)
- [Erstellen von Remote-Azure-Ressourcen beim Erstellen eines neuen Webprojekts](#AzureResources)
- [Webveröffentlichungsverbesserungen](#webpublish)
- [ASP.NET Gerüst](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Webformulare](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web-API 2.1.2](#webapi)
- [ASP.NET Webseiten 3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET Identität 2.0.0](#identity)
- [Microsoft OWIN-Komponenten](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Eine ASP.NET Projektvorlagen

- Aktualisierungen ASP.NET Projektvorlagen, um die Kontobestätigung und das Zurücksetzen von Kennwörtern zu unterstützen.
- Aktualisieren Sie ASP.NET Web-API-Vorlage, um die Authentifizierung mithilfe von On Premises-Organisationskonten zu unterstützen.
- Die ASP.NET SPA-Vorlage enthält jetzt eine Authentifizierung, die auf MVC- und Server-Seitenansichten basiert. Die Vorlage verfügt über einen WebAPI-Controller, auf den nur authentifizierte Benutzer zugreifen können.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>Unterstützung von SSL beim Starten von Webanwendungen auf IIS Express

Um die Sicherheitswarnung beim Durchsuchen und Debuggen von HTTPS auf localhost zu beseitigen, haben wir ein Dialogfeld hinzugefügt, damit Internet Explorer und Chrome dem selbstsignierten IIS Express SSL-Zertifikat vertrauen können.

Beispielsweise kann eine Webprojekteigenschaft so eingestellt werden, dass SSL verwendet wird. Klicken Sie auf F4, um das Eigenschaftendialogfeld anzuzeigen. Ändern Sie **SSL Enabled** in true. Kopieren Sie die SSL-URL.

![SSL-aktivierte Eigenschaft](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Legen Sie die Webprojekt-Eigenschaftenseite-Webregisterkarte so fest, `https://localhost:44300/` dass die HTTPS-basierte URL verwendet wird (Die SSL-URL wird verwendet, es sei denn, Sie haben zuvor SSL-Websites erstellt.)

![Festlegen der Projekt-URL (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Drücken Sie STRG+F5, um die Anwendung auszuführen. Befolgen Sie die Anweisungen, um dem selbstsignierten Zertifikat zu vertrauen, das IIS Express generiert hat.

![SSL-Warnung](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Lesen Sie das Dialogfeld **Sicherheitswarnung,** und klicken Sie dann auf **Ja,** wenn Sie das Zertifikat installieren möchten, das localhost darstellt.

![Sicherheitshinweis](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Die Website wird in IE oder Chrome ohne die Zertifikatswarnung im Browser angezeigt.

![HTTPS-Seite ohne Warnungen](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox verwendet einen eigenen Zertifikatspeicher, sodass eine Warnung angezeigt wird.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Verbesserungen des Visual Studio-Web-Editors

- **Neues JSON-Projektelement und -Editor**: Wir haben Visual Studio ein JSON-Projektelement und einen Editor hinzugefügt. Zu den aktuellen JSON-Editorfunktionen gehören Farbgebung, Syntaxvalidierung, Korrektur der Geschweifklammern, Gliederung, Werkzeugoptionseinstellungen und vieles mehr.

    ![JSON-Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense unterstützt jetzt [JSON Schema](http://json-schema.org/) v3 und v4. Es gibt ein Schema-Kombinationsfeld, um vorhandene Schemas auszuwählen, den lokalen Schemapfad zu bearbeiten oder einfach eine Projekt-JSON-Datei zu ziehen, um den relativen Pfad abzubekommen.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON Schema-Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Neuer Sass (SCSS) Editor**: Wir haben LESS in VS2013 RTM hinzugefügt, und wir haben jetzt ein Sass-Projektelement und einen Editor. Sass-Editor-Funktionen sind vergleichbar mit dem LESS-Editor und umfassen Farbgebung, Variable und Mixins IntelliSense, Kommentar/Uncomment, Schnellinformationen, Formatierung, Syntaxvalidierung, Gliederung, Goto-Definition, Farbauswahl, Werkzeugoptionseinstellung usw.

    ![Neues Element hinzufügen: SCSS-Stylesheet](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Stylesheet-Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **Neue URL-Auswahl in HTML-, Razor-, CSS-, LESS- und Sass-Dokumenten:** VS 2013 wurde ohne URL-Auswahl außerhalb von Web Forms-Seiten ausgeliefert. Die neue URL-Auswahl für HTML-, Razor-, CSS-, LESS- und Sass-Editoren ist eine dialogfreie, fließende Tippauswahl, die '.'.' versteht. und filtert Dateilisten entsprechend für img-Tags und Links.

    ![URL-Auswahl für Bild-Tag](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![URL-Auswahl für Ansichten](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![URL-Auswahl für CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Aktualisierungen des LESS-Editors durch Hinzufügen weiterer Funktionen**
- **Knockout Intellisense Upgrade**: Wir haben eine nicht standardmäßige KnockOut-Syntax für VS intelliSense, "ko-vs-editor viewModel:" Syntax hinzugefügt. Es kann verwendet werden, um an mehrere Ansichtsmodelle auf einer Seite zu binden, indem Kommentare im Formular verwendet werden:

    ![Knockout Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Wir haben auch Unterstützung für verschachtelte ViewModel IntelliSense hinzugefügt, sodass Sie einen Drilldown in tief verschachtelte Objekte im ViewModel durchführen können.

    `<div data-bind="text: foo.bar.baz.etc" />`

    Der angezeigte IntelliSense ist der vollständige IntelliSense des JavaScript-Objekts.

    ![Intellisense zeigt vollständiges JavaScript-Objekt an](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **Neue URL-Auswahl in HTML-, Razor-, CSS-, LESS- und Sass-Dokumenten**: VS 2013 wird ohne URL-Auswahl außerhalb von Web Forms-Seiten ausgeliefert. Die neue URL-Auswahl für HTML-, Razor-, CSS-, LESS- und Sass-Editoren ist eine dialogfreie, fließende Tippauswahl, die '.'.' versteht. und filtert Dateilisten entsprechend für img-Tags und Links.

    ![URL-Auswahl für Bild-Tag](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![URL-Auswahl für Ansichten](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![URL-Auswahl für CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Browserverknüpfung

- Browser Link unterstützt jetzt HTTPS-Verbindungen und listet diese im Dashboard mit anderen Verbindungen auf, solange das Zertifikat vom Browser als vertrauenswürdig eingestuft wird.
- Statische HTML-Quellzuordnung
- SPA-Unterstützung für Mapping-Daten
- Automatische Aktualisierung von Zuordnungsdaten

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Unterstützung für Azure App Service-Web-Apps in Visual Studio

- **Unterstützen Sie die Azure-Anmeldung.**
- **Remote-Debugging und Remoteansicht für Web-Apps:** Wir unterstützen jetzt [Remote-Debugging für Web-Apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) und Remoteansicht von Web-App-Inhaltsdateien im Server-Explorer.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Erstellen von Remote-Azure-Ressourcen beim Erstellen eines neuen Webprojekts

Wir haben im Dialogfeld für neue Webanwendungen ein Kontrollkästchen ["Remoteressourcen erstellen"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) hinzugefügt. Wenn Sie es auswählen, können Sie die Erfahrung des Erstellens einer neuen Webanwendung, des Einrichtens der Azure-Publishingwebsite zum Testen und des Erstellens eines Veröffentlichungsprofils in wenigen einfachen Schritten integrieren.

![Neues Projekt mit Azure-Ressourcen](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Veröffentlichen in Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Webveröffentlichungsverbesserungen

- Verbessern Sie die Benutzerfreundlichkeit für die Veröffentlichung.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Gerüst

- **Enum-Unterstützung:** Wenn Ihr Modell Enums verwendet, generiert das MVC-Gerüst für Enum dropdown. Hierbei werden die Enum-Hilfsprogramme in MVC verwendet.
- **Bootstrap-Unterstützung**: Die EditorFor-Vorlagen in MVC-Gerüsten wurden aktualisiert, damit sie die Bootstrap-Klassen verwenden.
- **Paketunterstützung**: MVC- und Web-API-Gerüste fügen 5.1-Pakete für MVC und Web-API hinzu

Die folgenden Screenshots zeigen Gerüstmodelle.

- Modellcode:

     ![Modellcode](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Kompilieren Sie den Modellcode, klicken Sie mit der rechten Maustaste, und wählen Sie **Hinzufügen**, **Neues Gerüstelement**.

     ![Neues Gerüst hinzufügen](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- Wählen Sie **MVC5 Controller mit Ansichten mit Entity Framework**:

     ![Hinzufügen eines neuen MVC5-Controllers mit Ansichten](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- Controller mit dem Modell **hinzufügen:**

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Überprüfen Sie den generierten Code, z. B. `@Html.EnumDropDownListFor`Views/WeekdayModels/Edit.cshtml enthält : ![Ansicht mit EnumDropDownListFor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- Führen Sie die Seite aus, um die enum combobox generiert anzuzeigen, beachten Sie, dass, wenn ein Wert null sein kann, eine leere Zeichenfolge für das Kombinationsfeld ausgewählt werden kann. Auf der Seite **Erstellen** wird z. B. Folgendes angezeigt:

    ![Combo-Feld, das leere Zeichenfolgen zulässt](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM wird im April 2014 veröffentlicht. Hier sind die wichtigsten Punkte aus den Versionshinweisen, aber bitte überprüfen Sie die [vollständigen Versionshinweise](http://docs.nuget.org/docs/release-notes/nuget-2.8) für weitere Informationen zu diesen Änderungen.

- **Ziel-Windows Phone 8.1-Anwendungen**: NuGet 2.8.1 unterstützt jetzt die Ausrichtung auf Windows Phone 8.1-Anwendungen mithilfe der Zielframeworkmoniker "WindowsPhoneApp", "WPA", "WindowsPhoneApp81" und "WPA81".

- **Patch-Auflösung für Abhängigkeiten**: Beim Auflösen von Paketabhängigkeiten hat NuGet in der Vergangenheit eine Strategie zur Auswahl der niedrigsten Haupt- und Nebenpaketversion implementiert, die die Abhängigkeiten vom Paket erfüllt. Im Gegensatz zur Haupt- und Nebenversion wurde die Patch-Version jedoch immer auf die höchste Version aufgelöst. Obwohl das Verhalten gut gemeint war, verursachte es einen Mangel an Determinismus für die Installation von Paketen mit Abhängigkeiten.
- **DependencyVersion Switch**: Obwohl NuGet 2.8 das *Standardverhalten* zum Auflösen von Abhängigkeiten ändert, fügt es auch eine genauere Kontrolle über den Abhängigkeitsauflösungsprozess über den Schalter -DependencyVersion in der Paket-Manager-Konsole hinzu. Der Switch ermöglicht das Auflösen von Abhängigkeiten mit der niedrigsten möglichen Version (Standardverhalten), der höchstmöglichen Version oder der höchsten Neben- oder Patchversion. Dieser Switch funktioniert nur für installations-Paket im Powershell-Befehl.
- **DependencyVersion-Attribut**: Zusätzlich zum oben beschriebenen -DependencyVersion-Schalter hat NuGet auch die Möglichkeit ermöglicht, ein neues Attribut in der Datei nuget.config festzulegen, das definiert, was der Standardwert ist, wenn der Schalter -DependencyVersion nicht in einem Aufruf von install-package angegeben ist. Dieser Wert wird auch vom NuGet Package Manager-Dialog für alle Installationspaketvorgänge beachtet. Um diesen Wert festzulegen, fügen Sie das Attribut unten zu Ihrer datei nuget.config hinzu:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Vorschau NuGet Operations Mit -WhatIf**: Einige NuGet-Pakete können tiefe Abhängigkeitsdiagramme haben, und als solche kann es während eines Installations-, Deinstallations- oder Aktualisierungsvorgangs hilfreich sein, um zuerst zu sehen, was passieren wird. NuGet 2.8 fügt die standardmäßige PowerShell -was wenn wechseln zu den Befehlen install-package, deinstall-package und update-package, um die Visualisierung des gesamten Schließens von Paketen zu ermöglichen, auf die der Befehl angewendet wird.
- **Downgrade-Paket**: Es ist nicht ungewöhnlich, eine Vorabversion eines Pakets zu installieren, um neue Funktionen zu untersuchen und dann zu entscheiden, auf die letzte stabile Version zurückzusetzen. Vor NuGet 2.8 war dies ein mehrstufiger Prozess, bei dem das Vorabversionspaket und seine Abhängigkeiten deinstalliert und dann die frühere Version installiert wurden. Mit NuGet 2.8 wird das Update-Paket nun jedoch den gesamten Paketabschluss (z. B. den Abhängigkeitsbaum des Pakets) auf die vorherige Version zurücksetzen.
- **Entwicklungsabhängigkeiten**: Viele verschiedene Arten von Funktionen können als NuGet-Pakete bereitgestellt werden - einschließlich Tools, die zur Optimierung des Entwicklungsprozesses verwendet werden. Diese Komponenten können zwar bei der Entwicklung eines neuen Pakets eine wichtige Rolle sein, sollten jedoch bei der späteren Veröffentlichung nicht als Abhängigkeit des neuen Pakets betrachtet werden. NuGet 2.8 ermöglicht es einem Paket, sich in der .nuspec-Datei als Entwicklungsabhängigkeit zu identifizieren. Bei der Installation werden diese Metadaten auch der Datei packages.config des Projekts hinzugefügt, in dem das Paket installiert wurde. Wenn diese packages.config-Datei später während des nuget.exe-Pakets auf NuGet-Abhängigkeiten analysiert wird, werden diese Abhängigkeiten ausgeschlossen, die als Entwicklungsabhängigkeiten markiert sind.
- **Individuelle packages.config-Dateien für verschiedene Plattformen**: Bei der Entwicklung von Anwendungen für mehrere Zielplattformen ist es üblich, unterschiedliche Projektdateien für jede der jeweiligen Build-Umgebungen zu haben. Es ist auch üblich, verschiedene NuGet-Pakete in verschiedenen Projektdateien zu verwenden, da Pakete unterschiedliche Unterstützungsniveaus für verschiedene Plattformen haben. NuGet 2.8 bietet verbesserte Unterstützung für dieses Szenario, indem verschiedene packages.config-Dateien für verschiedene plattformspezifische Projektdateien erstellt werden.
- **Fallback zum lokalen Cache:** Obwohl NuGet-Pakete in der Regel von einem Remote-Galerie wie dem [NuGet-Katalog](http://www.nuget.org) über eine Netzwerkverbindung verbraucht werden, gibt es viele Szenarien, in denen der Client nicht verbunden ist. Ohne Netzwerkverbindung konnte der NuGet-Client keine Pakete erfolgreich installieren – selbst wenn sich diese Pakete bereits auf dem Clientcomputer im lokalen NuGet-Cache befanden. NuGet 2.8 fügt der Paket-Manager-Konsole einen automatischen Cache-Fallback hinzu.

    Die Cache-Fallback-Funktion erfordert keine spezifischen Befehlsargumente. Darüber hinaus funktioniert der Cache-Fallback derzeit nur in der Paket-Manager-Konsole – das Verhalten funktioniert derzeit nicht im Paket-Manager-Dialog.
- **Fehlerbehebungen**: Eine der wichtigsten Fehlerbehebungen war die Leistungsverbesserung im Befehl update-package -reinstall.

    Zusätzlich zu diesen Funktionen und der oben genannten Performance-Fix, enthält diese Version von NuGet auch viele andere Fehlerbehebungen. In der Veröffentlichung wurden insgesamt 181 Probleme behandelt. Eine vollständige Liste der in NuGet 2.8 behobenen Arbeitsaufgaben finden Sie im [NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) für diese Version.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Die Web Forms-Vorlagen zeigen nun, wie Kontobestätigung und Kennwortzurücksetzung für ASP.NET Identity erfolgen.
- Das Entitätsdatenquellensteuerelement und der dynamische Datenanbieter für Entity Framework 6. Weitere Informationen finden Sie im folgenden MSDN-Blog: [Dynamic Data Provider und EntityDataSource-Steuerelement für Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Verbesserungen beim Attributrouting](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Bootstrap-Unterstützung für Editorvorlagen](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Enumeratunterstützung in Ansichten](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Unauffällige Unterstützung für MinLength/ MaxLength-Attribute](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Unterstützung des "this"-Kontexts in unauffälligen Ajax](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Verschiedene [Fehlerbehebungen](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web-API 2.1.2

- [Globale Fehlerbehandlung](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Verbesserungen des Attributroutings](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Verbesserungen der Hilfeseite](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute-Unterstützung](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON-Medien-Formatter](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Bessere Unterstützung für Asynchronfilter](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [Abfrageanalyse für die Clientformatierungsbibliothek](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Verschiedene [Fehlerbehebungen](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Webseiten 3.1.2

- Verschiedene [Fehlerbehebungen](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

Entity Framework wurde sowohl für Laufzeit als auch für Tools auf Version 6.1 aktualisiert. Entity Framework (EF) 6.1 ist ein kleines Update für Entity Framework 6 und enthält eine Reihe von Fehlerbehebungen und neuen Funktionen. Ausführliche Informationen zu EF6.1, einschließlich Links zur Dokumentation zu den neuen Features, finden Sie unter [Entity Framework Version History](https://msdn.microsoft.com/data/jj574253). Zu den neuen Funktionen in dieser Version gehören:

- **Die Werkzeugkonsolidierung** bietet eine konsistente Möglichkeit, ein neues EF-Modell zu erstellen. Mit dieser Funktion wird der Assistent für ADO.NET Entitätsdatenmodell erweitert, um das Erstellen von Code First-Modellen zu unterstützen, einschließlich Reverse Engineering aus einer vorhandenen Datenbank. Diese Funktionen waren zuvor in Beta-Qualität in den EF Power Tools verfügbar.
- **Die Behandlung von Transaktionscommitfehlern** stellt den neuen [System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) bereit, der die neu eingeführte Möglichkeit zum Abfangen von Transaktionsvorgängen nutzt. **Der CommitFailureHandler** ermöglicht die automatische Wiederherstellung von Verbindungsfehlern beim Übertragen einer Transaktion.
- **IndexAttribute** ermöglicht die Angabe von Indizes, indem ein Attribut für eine Eigenschaft (oder Eigenschaften) in Ihrem Code First-Modell platziert wird. Code First erstellt dann einen entsprechenden Index in der Datenbank.
- **Die öffentliche Zuordnungs-API** bietet Zugriff auf die Informationen, die EF darüber enthält, wie Eigenschaften und Typen Spalten und Tabellen in der Datenbank zugeordnet werden. In früheren Versionen war diese API intern.
- **Möglichkeit, Interceptoren über die Datei App/Web.config zu konfigurieren**(sodass Interceptoren hinzugefügt werden können, ohne die Anwendung neu zu kompilieren).
- **DatabaseLogger** ist ein neuer Interceptor, der es einfach macht, alle Datenbankoperationen in einer Datei zu protokollieren. In Kombination mit der vorherigen Funktion können Sie die Protokollierung von Datenbankvorgängen für eine bereitgestellte Anwendung einfach einschalten, ohne dass eine Neukompilierung erforderlich ist.
- Die Erkennung von **Migrationsmodelländerungen** wurde verbessert, sodass Gerüstmigrationen genauer sind. Die Leistung des Änderungserkennungsprozesses wurde ebenfalls erheblich verbessert.
- **Leistungsverbesserungen,** einschließlich reduzierter Datenbankoperationen während der Initialisierung, Optimierungen für den Nullgleichheitsvergleich in LINQ-Abfragen, schnellere Ansichtsgenerierung (Modellerstellung) in mehr Szenarien und effizientere Materialisierung nachverfolgter Entitäten mit mehreren Zuordnungen.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identität 2.0.0

- **Zwei-Faktor-Authentifizierung:** ASP.NET Identity unterstützt jetzt die Zwei-Faktor-Authentifizierung. Die Zwei-Faktor-Authentifizierung bietet eine zusätzliche Sicherheitsebene für Ihre Benutzerkonten, wenn Ihr Kennwort kompromittiert wird. Es gibt auch Schutz für Brute-Force-Angriffe gegen die beiden Faktor-Codes.
- **Kontosperrung:** Bietet eine Möglichkeit, den Benutzer auszusperren, wenn der Benutzer sein Kennwort oder zwei-Faktor-Codes falsch eingibt. Die Anzahl der ungültigen Versuche und die Zeitspanne für die gesperrten Benutzer können konfiguriert werden. Ein Entwickler kann die Kontosperrung für bestimmte Benutzerkonten optional deaktivieren, falls dies erforderlich ist.
- **Kontobestätigung:** Das ASP.NET Identity-System unterstützt jetzt die Kontobestätigung. Dies ist ein ziemlich häufiges Szenario in den meisten Websites heute, wo, wenn Sie sich für ein neues Konto auf der Website registrieren, müssen Sie Ihre E-Mail bestätigen, bevor Sie etwas auf der Website tun können. E-Mail-Bestätigung ist nützlich, da sie verhindert, dass gefälschte Konten erstellt werden. Dies ist äußerst nützlich, wenn Sie E-Mail als Methode zur Kommunikation mit den Benutzern Ihrer Website wie Forum-Websites, Banking, E-Commerce oder social Websites verwenden.
- **Passwort-Reset:** Password Reset ist eine Funktion, bei der der Benutzer seine Passwörter zurücksetzen kann, wenn er sein Passwort vergessen hat.
- **Sicherheitsstempel (Überall abmelden):** Unterstützt eine Möglichkeit, das Sicherheitstoken für den Benutzer zu regenerieren, wenn der Benutzer sein Kennwort oder andere sicherheitsrelevante Informationen wie das Entfernen einer zugeordneten Anmeldung (z. B. Facebook, Google, Microsoft-Konto usw.) ändert. Dies ist erforderlich, um sicherzustellen, dass alle Token, die mit dem alten Kennwort generiert werden, ungültig werden. Wenn Sie im Beispielprojekt das Kennwort des Benutzers ändern, wird ein neues Token für den Benutzer generiert, und alle vorherigen Token werden ungültig. Diese Funktion bietet eine zusätzliche Sicherheitsebene für Ihre Anwendung, da Sie beim Ändern Ihres Kennworts von überall (allen anderen Browsern) abgemeldet werden, wo Sie sich bei dieser Anwendung angemeldet haben.
- **Den Typ des Primärschlüssels für Benutzer und Rollen erweiterbar machen:** In ASP.NET Identity 1.0 war der Typ des Primärschlüssels für Tabellenbenutzer und -rollen Zeichenfolgen. Dies bedeutet, wenn das ASP.NET Identity-System in SQL Server mithilfe von Entity Framework beibehalten wurde, haben wir nvarchar verwendet. Es gab viele Diskussionen um diese Standardimplementierung auf Stack Overflow und basierend auf dem eingehenden Feedback. Wir haben einen Erweiterbarkeits-Hook bereitgestellt, in dem Sie angeben können, was der Primärschlüssel Ihrer Tabelle "Benutzer und Rollen" sein soll. Dieser Erweiterbarkeits-Hook ist besonders nützlich, wenn Sie Ihre Anwendung migrieren und die Anwendung UserIds als GUIDs oder ints speichert.
- **Unterstützung Von IQueryable für Benutzer und Rollen:** Unterstützung für IQueryable in UsersStore und RolesStore wurde hinzugefügt, Sie können ganz einfach die Liste der Benutzer und Rollen abrufen.
- **Unterstützung Delete-Vorgang über den UserManager**
- **Indizierung auf UserName**: In ASP.NET Identity Entity Framework-Implementierung haben wir einen eindeutigen Index für den Benutzernamen hinzugefügt, indem wir das neue IndexAttribute in EF 6.1.0 verwendet haben. Dadurch wird sichergestellt, dass Benutzernamen immer eindeutig sind und es keine Race-Bedingung gab, in der Sie mit doppelten Benutzernamen enden konnten.
- **Enhanced Password Validator:** Der Kennwortvalidator, der in ASP.NET Identity 1.0 ausgeliefert wurde, war ein ziemlich einfacher Kennwortvalidator, der nur die Mindestlänge validierte. Es gibt einen neuen Kennwortvalidator, der Ihnen mehr Kontrolle über die Komplexität des Kennworts gibt. Bitte beachten Sie, dass sie, selbst wenn Sie alle Einstellungen in diesem Kennwort aktivieren, Sie dazu ermutigen, die Zwei-Faktor-Authentifizierung für die Benutzerkonten zu aktivieren.
- **IdentityFactory Middleware/ CreatePerOwinContext**:

    - **Benutzer-Manager**: Sie können die Factory-Implementierung verwenden, um eine Instanz von UserManager aus dem OWIN-Kontext abzuholen. Dieses Muster ähnelt dem, was wir zum Abrufen von AuthenticationManager aus dem OWIN-Kontext für SignIn und SignOut verwenden. Dies ist eine empfohlene Methode zum Abrufen einer Instanz von UserManager pro Anforderung für die Anwendung.
    - **DbContextFactory**: ASP.NET Identity verwendet Entity Framework zum Beibehalten des Identitätssystems in SQL Server. Dazu verfügt das Identitätssystem über einen Verweis auf den ApplicationDbContext. Die DbContextFactory Middleware gibt eine Instanz des ApplicationDbContext pro Anforderung zurück, die Sie in Ihrer Anwendung verwenden können.
- **ASP.NET Identity Samples NuGet-Paket**: Das Samples NuGet-Paket kann die Installation und Ausführung von Beispielen für ASP.NET Identity vereinfachen und die best Practices befolgen. Dies ist ein Beispiel ASP.NET MVC-Anwendung. Ändern Sie den Code entsprechend Ihrer Anwendung, bevor Sie ihn in der Produktion bereitstellen. Das Beispiel sollte in einer leeren ASP.NET-Anwendung installiert werden. Weitere Informationen zum Paket finden Sie im folgenden Blogbeitrag: [Ankündigung von RTM von ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN-Komponenten

Es gab viele Fehler, die in dieser Version behoben wurden. Ausführlichere Informationen finden Sie in den [Versionshinweisen für die Version 2.1.0.](https://katanaproject.codeplex.com/releases/view/113281)

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

Es gab viele Fehler, die in dieser Version behoben wurden. Ausführlichere Informationen finden Sie in den [Versionshinweisen für die Version 2.0.2.](https://github.com/SignalR/SignalR/releases/tag/2.0.2)
