---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET und Web Tools 2012.2 Versionshinweise | Microsoft Docs
author: rick-anderson
description: Versionshinweise für ASP.NET und Web Tools 2012.2.
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675904"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET and Web Tools 2012.2 – Anmerkungen zu dieser Version

> Dieses Dokument beschreibt die Veröffentlichung von ASP.NET und Web Tools 2012.2. Es handelt sich um ein Update für Visual Studio Web Tooling und ASP.NET.

- [Installationshinweise](#_Installation)
- [Dokumentation](#_Documentation)
- [Unterstützung](#_Support)
- [Software-Anforderungen](#_Software_Requirements)
- [Neue Funktionen in ASP.NET und Web Tools 2012.2](#_New_Features_in)

    - [Tools](#_Tooling)
    - [Webveröffentlichung](#_Web_Publishing)
    - [mVC-Vorlagen ASP.NET](#_Templates)
    - [ASP.NET-Web-API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET Friendly URLs](#_ASP.NET_Friendly_URLs)
- [Bekannte Probleme und brechende Änderungen](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>Installationshinweise

ASP.NET und WebTools 2012.2 für Visual Studio 2012 können mit [dem Web Platform Installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)installiert werden. Dies ist ein Update für Visual Studio 2012 oder Visual Studio Express 2012 für Web, das erforderlich ist. Wenn Visual Studio nicht installiert ist, wird Visual Studio Express 2012 für Web installiert.

Sie können ASP.NET und Web Tools 2012.2 auch manuell installieren. Für Web muss Visual Studio 2012 oder Visual Studio Express 2012 installiert sein. Verwenden Sie dann die folgenden Anweisungen: 

1. Laden Sie [ASP.NET und Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) Installer vom Download Center herunter.
2. Wenn Sie dazu aufgefordert werden, klicken Sie auf Ausführen. Sie können die Datei auch speichern, um sie später auszuführen.
3. Überprüfen Sie die Version von Visual Studio, die Sie aktualisieren möchten. Sie können dies tun, indem Sie Visual Studio starten, das Sie aktualisieren möchten. Klicken Sie dann auf das Menüelement Hilfe.   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. Wenn der Menüpunkt &quot;Über Microsoft Visual Studio 2012 für Web&quot; angezeigt wird, laden Sie Web Developer Tools [2012.2 - Visual Studio Express 2012 für Web](https://go.microsoft.com/fwlink/?LinkID=282228)herunter. Andernfalls laden Sie [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)herunter.
5. Wenn Sie dazu aufgefordert werden, klicken Sie auf Ausführen. Sie können die Datei auch speichern, um sie später auszuführen.

> [!NOTE]
> ASP.NET und Web Tools 2012.2-Version enthält sql Server Data Tools nicht. SQL Server und Windows Azure SQL-Datenbanken bieten eine umfangreichere Gruppe von Datenbanktools, einschließlich offlineer projektgestützter Entwicklung, Schemavergleich und erweiterten Datenbankbereitstellungsfunktionen. Weitere Informationen oder die Installation von [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)SQL Server Data Tools finden Sie unter .

<a id="_Documentation"></a>
## <a name="documentation"></a>Dokumentation

Tutorials und weitere Informationen zu ASP.NET und Web Tools 2012.2 finden Sie auf ASP.NET Website ( . https://www.asp.net)

<a id="_Support"></a>
## <a name="support"></a>Support

ASP.NET und Web Tools 2012.2 wird offiziell veröffentlicht und unterstützt. Sie können Ihren normalen Support-Kanal verwenden. Sie können auch Fragen an[https://forums.asp.net/](https://forums.asp.net/)die ASP.NET Foren ( ) senden, in denen Mitglieder der ASP.NET Community häufig informelle Unterstützung anbieten können.

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>Softwareanforderungen

Für die ASP.NET und Webtools 2012.2 ist Visual Studio 2012 oder Visual Studio Express 2012 für Web erforderlich.

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>Neue Funktionen in ASP.NET und Web Tools 2012.2

In diesem Abschnitt werden Features beschrieben, die in der Version ASP.NET und Web Tools 2012.2 eingeführt wurden.

<a id="_Tooling"></a>
### <a name="tooling"></a>Tools

- Seitenprüfung 

    - Unterstützung Der JavaScript-Auswahlzuordnung, mit der Page Inspector Elemente, die der Seite dynamisch hinzugefügt wurden, dem entsprechenden JavaScript-Code zuordnen kann.
    - Die Möglichkeit, CSS-Updates in Echtzeit anzuzeigen.
    - Weitere Informationen finden Sie [unter CSS Auto-Sync und JavaScript Selection Mapping im Seiteninspektor](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).
- Editor 

    - Unterstützung Syntaxhervorhebung für CoffeeScript, Schnurrbart, Lenker und JsRender.
    - Der HTML-Editor stellt Intellisense für Knockout-Bindungen bereit.
    - LESS-Bearbeitung und Compilerunterstützung, um das Erstellen dynamischer CSS mit LESS zu ermöglichen.
    - Fügen Sie JSON als .NET-Klasse ein. Verwenden Sie diesen Befehl Spezielle sinieren, um JSON in eine Codedatei von C oder VB.NET einzufügen, und Visual Studio generiert automatisch .NET-Klassen, die aus dem JSON abgeleitet werden.
- Die Unterstützung für mobile Emulatoren fügt Erweiterbarkeits-Hooks hinzu, sodass Emulatoren von Drittanbietern als VSIX installiert werden können. Die installierten Emulatoren werden in der Dropdown-Liste F5 angezeigt, sodass Entwickler eine Vorschau ihrer Websites auf einer Vielzahl von mobilen Geräten anzeigen können. Lesen Sie mehr über diese Funktion in Scott Hanselmans Blogeintrag [zur neuen BrowserStack-Integration mit Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Webveröffentlichung

- Websiteprojekte verfügen jetzt über die gleiche Veröffentlichungserfahrung wie Webanwendungsprojekte, einschließlich der Veröffentlichung auf Windows Azure-Websites.
- Selektives Veröffentlichen &#8211; für eine oder mehrere Dateien können Sie die folgenden Aktionen ausführen (nach der Veröffentlichung auf einem Web Deploy-Endpunkt): 

    - Veröffentlichen Sie ausgewählte Dateien.
    - Sehen Sie sich den Unterschied zwischen einer lokalen und einer Remotedatei an.
    - Aktualisieren Sie die lokale Datei mit der Remotedatei, oder aktualisieren Sie die Remotedatei mit der lokalen Datei.

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>mVC-Vorlagen ASP.NET

- Die neue Facebook-Anwendungsvorlage erleichtert das Schreiben von Facebook Canvas-Anwendungen. In wenigen einfachen Schritten können Sie eine Facebook-Anwendung erstellen, die Daten von einem angemeldeten Benutzer abruft und Integration mit dessen Freunden bietet. Die Vorlage enthält eine neue Bibliothek, die Ihnen zusätzliche Arbeiten abnimmt, die mit dem Erstellen einer Facebook-App verbunden sind, z. B. die Authentifizierung, Berechtigungen, den Zugriff auf Facebook-Daten und Vieles mehr. Weitere Informationen zur Verwendung der [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)Facebook-Anwendungsvorlage finden Sie unter .
- Eine neue MVC-Vorlage für eine Anwendung mit einer Seite ermöglicht Entwicklern das Erstellen von interaktiven clientseitigen Web-Apps mithilfe von HTML 5, CSS 3 und den beliebten Knockout- und jQuery JavaScript-Bibliotheken auf der Grundlage der ASP.NET Web-API. Die Vorlage enthält eine "Todo"-Listenanwendung, die gängige Vorgehensweisen zum Erstellen einer JavaScript HTML5-Anwendung veranschaulicht, die eine RESTful-Server-API verwendet. Weitere Informationen finden [https://www.asp.net/single-page-application](../../../single-page-application/index.md)Sie unter .
- Sie können jetzt eine VSIX erstellen, die dem Dialogfeld ASP.NET MVC New Project neue Vorlagen hinzufügt. Erfahren Sie hier:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes-Paket &#8211; MVC-Projektvorlagen wurden um das neue NuGet-Paket "FixedDisplayModes" erweitert, das eine Problemumgehung für einen Fehler in MVC 4 enthält. Weitere Informationen zur im Paket enthaltenen Korrektur finden Sie[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)in diesem Blogbeitrag ( ) des MVC-Teams.

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET-Web-API

ASP.NET Web-API wurde um mehrere neue Funktionen erweitert:

- ASP.NET Web-API-OData
- ASP.NET Web-API-Ablaufverfolgung
- ASP.NET Web-API-Hilfeseite

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web-API-OData

ASP.NET Web API OData bietet Ihnen die Flexibilität, die Sie benötigen, um OData-Endpunkte mit umfangreicher Geschäftslogik über jede Datenquelle zu erstellen. Mit ASP.NET Web API OData steuern Sie die Menge der OData-Semantik, die Sie verfügbar machen möchten. ASP.NET Web API OData ist in den ASP.NET MVC 4-Projektvorlagen[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)enthalten und ist auch in NuGet ( ) verfügbar.

ASP.NET Web API OData unterstützt derzeit die folgenden Funktionen:

- Aktivieren Sie die OData-Abfragesemantik, indem Sie das Attribut [Queryable] anwenden.
- Überprüfen Sie einfach OData-Abfragen und schränken Sie den Satz unterstützter Abfrageoptionen, Operatoren und Funktionen ein.
- Parameterbindung direkt an ODataQueryOptions, um eine abstrakte Syntaxstrukturdarstellung der Abfrage abzufragen, die dann überprüft und auf eine IQueryable oder IEnumerable angewendet werden kann.
- Aktivieren Sie das dienstgesteuerte Paging und die Generierung von nächsten Seitenverknüpfungen, indem Sie Ergebnislimits für das Attribut [Queryable] angeben.
- Fordern Sie eine inline Anzahl der Gesamtzahl der übereinstimmenden Ressourcen an, die $inlinecount verwenden.
- Steuern Sie die Nichtverbreitung.
- Alle/Alle Operatoren in $filter.
- Leiten Sie ein Entitätsdatenmodell nach Konventionen ab, oder passen Sie ein Modell explizit an, ähnlich wie Entity Framework Code-First.
- Stellen Sie Entitätssätze durch Ableiten von EntitySetController auf.
- Einfache, anpassbare Konventionen zum Verfügbarmachen von Navigationseigenschaften, Bearbeiten von Links und Implementieren von OData-Aktionen.
- Vereinfachtes Routing mit der MapODataRoute-Erweiterungsmethode.
- Unterstützung für die Versionsversion durch das Aufsetzen mehrerer EDM-Modelle.
- Stellen Sie Dienstdokument und $metadata verfügbar, damit Sie Clients (.NET, Windows Phone, Windows Store usw.) für Ihre Web-API generieren können.
- Unterstützung für die ausführlichen Formate OData Atom, JSON und JSON.
- Erstellen, Aktualisieren, teilweise aktualisieren (PATCH) und Löschen von Entitäten.
- Abfragen und Bearbeiten von Beziehungen zwischen Entitäten.
- Erstellen Sie Beziehungsverknüpfungen, die mit Ihren Routen verdrahtet werden.
- Komplexe Typen
- Entitätstypvererbung.
- Auflistungseigenschaften.
- Enumerationen.
- OData-Aktionen.
- Aufbauend auf der gleichen Grundlage wie WCF[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)Data Services, nämlich ODataLib ( ).

Weitere Informationen zu ASP.NET Web-API OData finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web-API-Ablaufverfolgung

ASP.NET Web API Tracing integriert Ablaufverfolgungsdaten aus Ihren Web-APIs in .NET Tracing. Sie ist jetzt standardmäßig in der Web-API-Projektvorlage aktiviert. Ablaufverfolgungsdaten für Ihre Web-APIs werden an das Ausgabefenster gesendet und über IntelliTrace zur Verfügung gestellt. ASP.NET Web-API-Ablaufverfolgung ermöglicht es Ihnen, Informationen über Ihre Web-API nachzuverfolgen, wenn sie in Windows Azure gehostet wird, durch die Integration mit [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx). Sie können ASP.NET Web-API-Ablaufverfolgung auch in jeder Anwendung installieren und[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)aktivieren, indem Sie das ASP.NET Web-API-Ablaufverfolgungspaket NuGet ( ) verwenden.

Weitere Informationen zum Konfigurieren und Verwenden ASP.NET [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)Web-API-Ablaufverfolgung finden Sie unter .

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web-API-Hilfeseite

Die ASP.NET Web-API-Hilfeseite ist jetzt standardmäßig in der Web-API-Projektvorlage enthalten. Die ASP.NET Web-API-Hilfeseite generiert automatisch Dokumentation für Web-APIs, einschließlich der HTTP-Endpunkte, der unterstützten HTTP-Methoden, Parameter und Beispielanforderungs- und Antwortnachrichtennutzlasten. Die Dokumentation wird automatisch aus Kommentaren in Ihrem Code abgezogen. Sie können die ASP.NET Web-API-Hilfeseite auch jeder Anwendung hinzufügen,[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)indem Sie das ASP.NET Web API Help Page NuGet-Paket ( ) verwenden.

Weitere Informationen zum Einrichten und Anpassen der ASP.NET [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)Web-API-Hilfeseite finden Sie unter .

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR macht es einfach, Ihrer ASP.NET-Anwendung Echtzeit-Webfunktionen hinzuzufügen, indem WebSockets verwendet werden, sofern verfügbar, und automatisch auf andere Techniken zurückfällt, wenn dies nicht der Fall ist.

Weitere Informationen zur Verwendung von [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)ASP.NET SignalR finden Sie unter .

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET Friendly URLs

ASP.NET FriendlyURLs macht es Webforms-Entwicklern sehr einfach, sauberer aussehende URLs zu generieren (ohne die ASPX-Erweiterung). Es erfordert wenig bis gar keine Konfiguration und kann mit vorhandenen ASP.NET v4.0-Anwendungen verwendet werden. Die FriendlyURLs-Funktion erleichtert Entwicklern auch das Hinzufügen mobiler Unterstützung für ihre Anwendungen, indem sie den Wechsel zwischen Desktop- und mobilen Ansichten unterstützt.

Weitere Informationen zur Installation und Verwendung ASP.NET [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)Freundliche URLs finden Sie unter .

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>Bekannte Probleme und brechende Änderungen

In diesem Abschnitt werden bekannte Probleme und Änderungen beschrieben, die sich in der Version ASP.NET und Web Tools 2012.2 befinden.

### <a name="installation-issues"></a>Probleme bei der Installation

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>Nicht in Ordnung installiert e.B. Visual Studio 2012

Die Installation einer zusätzlichen SKU von Visual Studio 2012 nach der Installation der ASP.NET und Web Tools 2012.2 erfordert einen Reparaturvorgang. Gehen Sie dabei von der folgenden Abfolge aus:

1. Installieren von Visual Studio 2012 Express for Web
2. Installieren ASP.NET und Webtools 2012.2
3. Installieren von Visual Studio 2012 Professional, Premium oder Ultimate

Schritt 2 würde nur zur Installation von Updates für Express for Web führen. Um sicherzustellen, dass die zusätzliche SKU, die in Schritt 3 installiert wurde, das Update enthält, müssen Sie die ASP.NET und Web Tools 2012.2 reparieren, um die Updates für die zuletzt installierte SKU zu installieren. Dies gilt auch, wenn die SKUs in Schritt 1 und 3 umgekehrt werden.

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>Installieren von Microsoft ASP.NET und Web Tools 2012.2, wenn Visual Studio geöffnet ist

Wenn VS während der Installation von Microsoft ASP.NET und Web Tools 2012.2 geöffnet ist, befindet sich Visual Studio möglicherweise in einem schlechten Zustand. Es wird empfohlen, dass Benutzer alle Instanzen von Visual Studio schließen, bevor Sie mit der Installation fortfahren.

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>Abbrechen ASP.NET und Web Tools 2012.2 Setup mitten in der Installation

Wenn Sie ASP.NET und Web Tools 2012.2-Setup mitten in der Installation abbrechen, befindet sich Visual Studio in einem schlechten Zustand. Gehen Sie folgend zu den folgenden Schritten vor, um dieses Problem zu beheben: 

- Wechseln Sie zu Programme.
- Deinstallieren Sie Microsoft ASP.NET und Web Tools 2012.2, falls vorhanden.
- Neuinstallation von Microsoft ASP.NET und Web Tools 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>Nach der Deinstallation ASP.NET und Web Tools 2012.2 fehlen die ASP.NET MVC 4-Vorlagen und Razor v2-Websitevorlagen

Durch das Deinstallieren von ASP.NET und Webtools 2012.2 werden außerdem alle ASP.NET MVC 4- und Razor v2-Websitevorlagen aus Visual Studio 2012 deinstalliert.

Die Problemumgehung besteht darin, Ihre Visual Studio 2012-Installation zu reparieren, um ASP.NET MVC 4- und Razor v2-Websitevorlagen neu zu installieren.

### <a name="tooling-issues"></a>Tooling-Probleme

#### <a name="nuget-error-reported-during-project-creation"></a>NuGet-Fehler, der während der Projekterstellung gemeldet wurde

Nach der Installation von ASP.NET und Web Tools 2012.2 wird beim Erstellen eines MVC 4-Projekts möglicherweise der folgende Fehler angezeigt.

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

Die ASP.NET und Web Tools 2012.2 liefert NuGet 2.1 aus und aktualisiert die Erweiterung in Visual Studio 2012. In einigen Fällen kann das VSIX-Installationsprogramm die VSIX nicht ordnungsgemäß aktualisieren. Mit den folgenden Schritten können Sie dieses Problem beheben:

1. Starten von Visual Studio 2012 als Administrator
2. Gehen Sie&gt;zu Tools- Erweiterungen und Updates und deinstallieren Sie NuGet.
3. Schließen Sie Visual Studio.
4. Navigieren Sie zum Installationsordner ASP.NET und Web Tools 2012.2:

    1. Für Visual Studio 2012: **Programmdateien, Microsoft ASP.NET, ASP.NET-Webstapel, Visual Studio 2012**
    2. Für Visual Studio 2012 Express for Web: **Programmdateien, Microsoft ASP.NET, ASP.NET Web Stack, Visual Studio Express 2012 für Web**
5. Doppelklicken Sie auf NuGet.Tools.vsix, um NuGet neu zu installieren

### <a name="web-api-issues"></a>Web-API-Probleme

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>Analyseprobleme in $filter- und DateTime-Literalen

Der OData-URI-Parser kann partielle Datetime-Literale nicht ordnungsgemäß analysieren. Beispielsweise kann $filter=start eq datetime'2012-12-31T12:00' nicht ordnungsgemäß analysiert werden. Eine Problemumgehung besteht darin, das vollständige Literal zu verwenden, $filter=start eq datetime'2012-12-31T12:00:00'.

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData unterstützt keine Nicht-Wert-Eigenschaftsnamen, bei der die Groß-/Kleinschreibung nicht berücksichtigt wird.

OData unterstützt keine Eigenschaftsnamen, bei der die Groß-/Kleinschreibung nicht berücksichtigt wird, in OData-Abfragen und im odata-Pfad. Siehe Arbeitspunkte:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

Wenn Benutzer unterschiedliche Gehäuse auf Javascript-Client- und Serverseite haben, wird dieses Problem wahrscheinlich auftreten. Dieses Problem ist nach DemDesign im odata-Protokoll enthalten. Viele Benutzer berichten jedoch über dieses Problem. Um es zu umgehen, müssen Benutzer ihre Fälle in DER URL korrigieren.

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>Standard-OData-Routingkonventionen unterstützen POST/PUT für die Navigationseigenschaft nicht.

Standard-OData-Routingkonventionen unterstützen POST/PUT für die Navigationseigenschaft nicht. Siehe Arbeitspunkt [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366). Es fehlt diese häufig verwendete Konvention in Standardkonventionen.

Um dies zu umgehen, müssen Benutzer neue Routingkonventionen erweitern, um sie zu unterstützen.

### <a name="facebook-template-issues"></a>Probleme mit Facebook-Vorlagen

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook-Anwendungsvorlage funktioniert nur mit .NET 4.5

Sie müssen .NET 4.5 in der Dropdown-Liste des Frameworks im Dialogfeld Neues Projekt auswählen, um die Facebook-Anwendungsvorlage in ASP.NET MVC 4 anzuzeigen.

#### <a name="real-time-update-controller"></a>Echtzeit-Update-Controller

Die Facebook-Anwendungsvorlage ermöglicht es Dem Benutzer, ganz einfach einen Web-API-Controller zu erstellen, um Echtzeit-Updates von Facebook zu verarbeiten. Wenn sich Ihr Entwicklungscomputer hinter NAT befindet, funktioniert Ihr Controller möglicherweise nicht ohne weitere Netzwerkkonfiguration. Weitere Informationen finden Sie hier:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>Abfragezeichenfolgenwerte stehen in Konflikt mit Facebook OAuth-Parametern

Die folgenden Felder stehen im Widerspruch zur Rückruf-URL des Facebook OAuth-Dialogs. Fügen Sie keine eigenen Abfragezeichenfolgenwerte mit den folgenden\_Namen\_hinzu: Code, Fehler, Fehlerbeschreibung, Fehlergrund.

#### <a name="using-page-inspector-with-facebook-template"></a>Verwenden des Seiteninspektors mit Facebook-Vorlage

Sie können die Seiteninspektorfunktion in Visual Studio 2012 nicht verwenden, während Sie Ihre Facebook-Anwendung debuggen. Der Seiteninspektor unterstützt derzeit keine iframes.

### <a name="single-page-application-template-issues"></a>Probleme mit der Anwendung senfürztigen Seite

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>Mit JQuery 1.9/Knockout 2.2.1 Update, wenn Standard MVC SPA-Projekt ausführen, neue Todo-Element-Eingabe-Eingabe-Fokus-Ereignis wird nicht ordnungsgemäß behandelt.

Mit JQuery 1.9/Knockout 2.2.1 Update, wenn Standard MVC SPA-Projekt ausgeführt wird, neue Todo-Element-Bearbeitung nicht mehr Fokus zurück auf das neue Todo-Element-Bearbeitungsfeld nach eingabe der neuen Todo-Element in die Todo-Liste.

Um den [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)Problemumgehungsverweis zu umgehen, und machen Sie eine ähnliche Korrektur wie den folgenden Beispielcode:

Datei todo.model.js  
 Funktion todolist(daten), fügen Sie Folgendes hinzu:  
 **self.isSelected = ko.observable(false);**

Funktion todoList.prototype.addTodo, fügen Sie den folgenden geschärften Text hinzu:  
 **self.isSelected(true);**  
 self.newTodoTitle(&quot;&quot;);

Datei index.cshtml, fügen Sie den folgenden geschärften Text hinzu:  
 &lt;Formular data-bind=&quot;senden: addTodo&quot;&gt;  
 &lt;eingabe&quot;class= addTodo&quot; type=&quot;&quot; text&quot;data-bind= value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: ' blur: addTodo '&quot; /&gt;  
 &lt;/form&gt;
