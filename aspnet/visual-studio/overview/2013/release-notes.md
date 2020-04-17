---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET und Webtools für Visual Studio 2013 Versionshinweise | Microsoft Docs
author: rick-anderson
description: In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools für Visual Studio 2013 beschrieben.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543495"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>ASP.NET and Web Tools für Visual Studio 2013 – Anmerkungen zu dieser Version

von [Microsoft](https://github.com/microsoft)

> In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools für Visual Studio 2013 beschrieben.

## <a name="contents"></a>Contents

- [Installationshinweise](#TOC1)
- [Dokumentation](#TOC2)
- [Software-Anforderungen](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Neue Funktionen in ASP.NET und Webtools für Visual Studio 2013

- [Ein ASP.NET](#TOC6)
- [Neue Webprojekterfahrung](#newproj)
- [ASP.NET Gerüst](#scaffold)
- [Browserverknüpfung](#browser-link)
- [Verbesserungen des Visual Studio-Web-Editors](#web-editor)
- [Unterstützung für Azure App Service-Webapps in Visual Studio](#waws)
- [Webveröffentlichungsverbesserungen](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Webformulare](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET-Web-API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Identity](#TOC8)
- [Microsoft OWIN-Komponenten](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET App Suspend](#TOC15)
- [Bekannte Probleme und brechende Änderungen](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>Installationshinweise

ASP.NET und Webtools für Visual Studio 2013 sind im Hauptinstallationsprogramm enthalten und können [hier](https://www.asp.net/downloads)heruntergeladen werden.

<a id="TOC2"></a>
## <a name="documentation"></a>Dokumentation

Tutorials und weitere Informationen zu ASP.NET und Webtools für Visual Studio 2013 sind auf der [ASP.NET-Website](https://www.asp.net/)verfügbar.

<a id="TOC4"></a>
## <a name="software-requirements"></a>Softwareanforderungen

ASP.NET und Webtools erfordert Visual Studio 2013.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>Neue Funktionen in ASP.NET und Webtools für Visual Studio 2013

In den folgenden Abschnitten werden die Features beschrieben, die in der Version eingeführt wurden.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>Ein ASP.NET

Mit der Veröffentlichung von Visual Studio 2013 haben wir einen Schritt zur Vereinheitlichung der Erfahrung mit ASP.NET Technologien gemacht, sodass Sie die gewünschten Technologien einfach mischen und anpassen können. Sie können z. B. ein Projekt mit MVC starten und dem Projekt später einfach Web Forms-Seiten oder Gerüst-Web-APIs in einem Web Forms-Projekt hinzufügen. Eine ASP.NET ist alles, um es einfacher für Sie als Entwickler zu machen, die Dinge zu tun, die Sie in ASP.NET lieben. Unabhängig davon, für welche Technologie Sie sich entscheiden, können Sie darauf vertrauen, dass Sie auf dem vertrauenswürdigen rahmen von One ASP.NET aufbauen.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>Neue Webprojekterfahrung

Wir haben die Erfahrung beim Erstellen neuer Webprojekte in Visual Studio 2013 verbessert. Im Dialogfeld **Neues ASP.NET Webprojekt** können Sie den gewünschten Projekttyp auswählen, eine beliebige Kombination von Technologien (Web Forms, MVC, Web API) konfigurieren, Authentifizierungsoptionen konfigurieren und ein Komponententestprojekt hinzufügen.

![Neues ASP.NET-Projekt](release-notes/_static/image1.png)

Im neuen Dialogfeld können Sie die Standardauthentifizierungsoptionen für viele Vorlagen ändern. Wenn Sie beispielsweise ein ASP.NET Web Forms-Projekt erstellen, können Sie eine der folgenden Optionen auswählen:

- Keine Authentifizierung
- Individuelle Benutzerkonten (ASP.NET Mitgliedschaft oder Social Provider anmelden)
- Organisationskonten (Active Directory in einer Internetanwendung)
- Windows-Authentifizierung (Active Directory in einer Intranetanwendung)

![Authentifizierungsoptionen](release-notes/_static/image2.png)

Weitere Informationen zum neuen Prozess zum Erstellen von Webprojekten finden Sie unter [Erstellen ASP.NET Webprojekten in Visual Studio 2013](creating-web-projects-in-visual-studio.md). Weitere Informationen zu den neuen Authentifizierungsoptionen finden Sie weiter unten in diesem Dokument [unter ASP.NET Identität.](#TOC8)

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET Gerüst

ASP.NET Scaffolding ist ein Codegenerierungsframework für ASP.NET Webanwendungen. Es erleichtert das Hinzufügen von Boilerplate-Code zu Ihrem Projekt, das mit einem Datenmodell interagiert.

In früheren Versionen von Visual Studio war das Gerüst auf ASP.NET MVC-Projekte beschränkt. Mit Visual Studio 2013 können Sie jetzt Gerüste für jedes ASP.NET-Projekt verwenden, einschließlich Web Forms. Visual Studio 2013 unterstützt derzeit nicht das Generieren von Seiten für ein Web Forms-Projekt, Aber Sie können dennoch Gerüste mit Webformularen verwenden, indem Sie dem Projekt MVC-Abhängigkeiten hinzufügen. Unterstützung für das Generieren von Seiten für Web forms wird in einem zukünftigen Update hinzugefügt.

Bei der Verwendung von Gerüsten stellen wir sicher, dass alle erforderlichen Abhängigkeiten im Projekt installiert sind. Wenn Sie beispielsweise mit einem ASP.NET Web Forms-Projekt beginnen und dann gerüstbauweise einen Web-API-Controller hinzufügen, werden die erforderlichen NuGet-Pakete und -Referenzen automatisch zu Ihrem Projekt hinzugefügt.

Um einem Web Forms-Projekt Ein MVC-Gerüst hinzuzufügen, fügen Sie ein **neues Gerüstelement** hinzu, und wählen Sie **mVC 5 Abhängigkeiten** im Dialogfeld aus. Es gibt zwei Möglichkeiten für Gerüste MVC; Minimal und voll. Wenn Sie Minimal auswählen, werden Ihrem Projekt nur die NuGet-Pakete und -Referenzen für ASP.NET MVC hinzugefügt. Wenn Sie die Option Voll auswählen, werden die minimalen Abhängigkeiten sowie die erforderlichen Inhaltsdateien für ein MVC-Projekt hinzugefügt.

Unterstützung für Gerüst-Asynchron-Controller verwendet die neuen asynchronen Features von Entity Framework 6.

Weitere Informationen und Tutorials finden Sie unter [ASP.NET Gerüstübersicht](aspnet-scaffolding-overview.md).

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>Browser-Link – SignalR-Kanal zwischen Browser und Visual Studio

Mit der neuen [Browserverknüpfungsfunktion](using-browser-link.md) können Sie mehrere Browser mit Visual Studio verbinden und alle aktualisieren, indem Sie auf eine Schaltfläche in der Symbolleiste klicken. Sie können mehrere Browser mit Ihrer Entwicklungswebsite verbinden, einschließlich mobiler Emulatoren, und auf Aktualisieren klicken, um alle Browser gleichzeitig zu aktualisieren. Browser Link macht auch eine API verfügbar, damit Entwickler Browser Link-Erweiterungen schreiben können.

![](release-notes/_static/image3.png)

Durch die Möglichkeit für Entwickler, die Browser Link-API zu nutzen, können sehr erweiterte Szenarien erstellt werden, die Grenzen zwischen Visual Studio und jedem verbundenen Browser überschreiten. Web Essentials nutzt die API, um ein integriertes Erlebnis zwischen Visual Studio und den Entwicklertools des Browsers, remote steuernde mobile Emulatoren und vieles mehr zu erstellen.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Verbesserungen des Visual Studio-Web-Editors

Visual Studio 2013 enthält einen neuen HTML-Editor für Razor-Dateien und HTML-Dateien in Webanwendungen. Der neue HTML-Editor bietet ein einheitliches Schema, das auf HTML5 basiert. Es verfügt über automatische Brace-Vervollständigung, jQuery UI und AngularJS-Attribut IntelliSense, Attribut IntelliSense Gruppierung, ID und Klassenname Intellisense, und andere Verbesserungen, einschließlich bessere Leistung, Formatierung und SmartTags.

Der folgende Screenshot veranschaulicht die Verwendung des Bootstrap-Attributs IntelliSense im HTML-Editor.

![Intellisense im HTML-Editor](release-notes/_static/image4.png)

Visual Studio 2013 kommt auch mit CoffeeScript und LESS-Editoren eingebaut. Der LESS-Editor kommt mit allen coolen Funktionen des CSS-Editors und verfügt über spezielle Intellisense für Variablen und Mixins in allen LESS-Dokumenten in der @import Kette.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Unterstützung für Azure App Service-Webapps in Visual Studio

In Visual Studio 2013 mit dem Azure SDK für .NET 2.2 können Sie **Server Explorer** verwenden, um direkt mit Ihren Remoteweb-Apps zu interagieren. Sie können sich bei Ihrem Azure-Konto anmelden, neue Web-Apps erstellen, Apps konfigurieren, Echtzeitprotokolle anzeigen und vieles mehr. Kurz nach der Veröffentlichung von SDK 2.2 können Sie im Debugmodus remote in Azure ausgeführt werden. Die meisten neuen Features für Azure App Service-Web-Apps funktionieren auch in Visual Studio 2012, wenn Sie die aktuelle Version des Azure SDK für .NET installieren.

Weitere Informationen finden Sie in den folgenden Ressourcen:

- [Erstellen einer ASP.NET Web-App in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Problembehandlung von Web-Apps in Azure App Service in Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Webveröffentlichungsverbesserungen

Visual Studio 2013 enthält neue und erweiterte Webveröffentlichungsfeatures. Einige davon sind:

- Automatisieren Sie ganz einfach [die Web.config-Dateiverschlüsselung](https://go.microsoft.com/fwlink/?LinkId=325529). (Dieser Link und die folgenden beiden Verweisen auf die Dokumentation zu MSDN, die möglicherweise erst spät am Tag am 10.17. verfügbar ist.)
- Automatische [Sendezeit für das Offlineschalten einer Anwendung während der Bereitstellung](https://go.microsoft.com/fwlink/?LinkId=325530).
- Konfigurieren Sie Web Deploy [so, dass Dateiprüfsummen anstelle des Datums](https://go.microsoft.com/fwlink/?LinkId=325531) der letzten Änderung verwendet werden, um zu bestimmen, welche Dateien auf den Server kopiert werden sollen.
- Schnelles Veröffentlichen einzelner ausgewählter Dateien (einschließlich Web.config), wenn Sie die FTP- oder Dateisystemveröffentlichungsmethoden sowie mit Web Deploy verwenden.

Weitere Informationen zu ASP.NET Webbereitstellung finden Sie auf [der ASP.NET Website](https://go.microsoft.com/fwlink/?LinkId=322027).

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 enthält eine Vielzahl neuer Funktionen, die in [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7)ausführlich beschrieben werden.

Diese Version von NuGet entfällt auch die Notwendigkeit, eine ausdrückliche Zustimmung für NuGetPaketwiederherstellungsfunktion zum Herunterladen von Paketen zu erteilen. Die Zustimmung (und das zugehörige Kontrollkästchen im NuGet-Dialogfeld für die Einstellungen) wird jetzt durch die Installation von NuGet erteilt. Jetzt funktioniert die Paketwiederherstellung standardmäßig.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>Ein ASP.NET

Die Web Forms-Projektvorlagen lassen sich nahtlos in das neue One ASP.NET integrieren. Sie können Ihrem Web Forms-Projekt MVC- und Web-API-Unterstützung hinzufügen und die Authentifizierung mithilfe des Assistenten für die Erstellung von Einem ASP.NET konfigurieren. Weitere Informationen finden Sie unter [Erstellen ASP.NET Webprojekten in Visual Studio 2013](creating-web-projects-in-visual-studio.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Die Web Forms-Projektvorlagen unterstützen das neue ASP.NET Identity Framework. Darüber hinaus unterstützen die Vorlagen jetzt die Erstellung eines Web Forms-Intranetprojekts. Weitere Informationen finden Sie unter [Authentifizierungsmethoden](creating-web-projects-in-visual-studio.md#auth) unter **Erstellen ASP.NET Webprojekten in Visual Studio 2013**.

### <a name="bootstrap"></a>Bootstrap

Die Web Forms-Vorlagen verwenden [Bootstrap,](http://twitter.github.io/bootstrap/) um ein schlankes und reaktionsschnelles Erscheinungsbild zu bieten, das Sie leicht anpassen können. Weitere Informationen finden Sie [unter Bootstrap in den Visual Studio 2013-Webprojektvorlagen](creating-web-projects-in-visual-studio.md#bootstrap).

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>Ein ASP.NET

Die Web MVC-Projektvorlagen lassen sich nahtlos in das neue One ASP.NET-Erlebnis integrieren. Sie können Ihr MVC-Projekt anpassen und die Authentifizierung mithilfe des Assistenten für die Erstellung von ASP.NET konfigurieren. Ein Einführungs-Tutorial zu ASP.NET MVC 5 finden Sie unter [Erste Schritte mit ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

Informationen zum Aktualisieren von MVC 4-Projekten auf MVC 5 finden Sie unter So aktualisieren Sie [ein ASP.NET MVC 4- und Web-API-Projekt auf ASP.NET MVC 5 und Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Die MVC-Projektvorlagen wurden aktualisiert, um ASP.NET Identity für die Authentifizierung und Identitätsverwaltung zu verwenden. Ein Tutorial mit Der Facebook- und Google-Authentifizierung und der neuen Mitgliedschafts-API finden Sie unter [Erstellen einer ASP.NET MVC 5-App mit Facebook und Google OAuth2 und OpenID-Anmeldung und](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Erstellen einer ASP.NET [MVC-App mit Auth und SQL DB und Bereitstellen in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).

### <a name="bootstrap"></a>Bootstrap

Die MVC-Projektvorlage wurde aktualisiert, um [Bootstrap](http://getbootstrap.com/) zu verwenden, um ein schlankes und reaktionsschnelles Erscheinungsbild zu bieten, das Sie leicht anpassen können. Weitere Informationen finden Sie [unter Bootstrap in den Visual Studio 2013-Webprojektvorlagen](creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Authentifizierungsfilter

Authentifizierungsfilter sind eine neue Art von Filter in ASP.NET MVC, die vor Autorisierungsfiltern in der ASP.NET MVC-Pipeline ausgeführt werden und es Ihnen ermöglichen, die Authentifizierungslogik pro Aktion, pro Controller oder global für alle Controller anzugeben. Authentifizierungsfilter verarbeiten Anmeldeinformationen in der Anforderung und geben einen entsprechenden Prinzipal an. Authentifizierungsfilter können auch Authentifizierungsherausforderungen als Reaktion auf nicht autorisierte Anforderungen hinzufügen.

### <a name="filter-overrides"></a>Filterüberschreibungen

Sie können nun überschreiben, welche Filter auf eine bestimmte Aktionsmethode oder einen bestimmten Controller angewendet werden, indem Sie einen Außerkraftsetzungsfilter angeben. Überschreiben von Filtern gibt einen Satz von Filtertypen an, die nicht für einen bestimmten Bereich (Aktion oder Controller) ausgeführt werden sollen. Auf diese Weise können Sie Filter konfigurieren, die global angewendet werden, dann aber bestimmte globale Filter von der Anwendung auf bestimmte Aktionen oder Controller ausschließen.

### <a name="attribute-routing"></a>Attributrouting

ASP.NET MVC unterstützt jetzt Attributrouting, dank eines Beitrags [http://attributerouting.net](http://attributerouting.net)von Tim McCall, dem Autor von . Mit Attributrouting können Sie Ihre Routen angeben, indem Sie Ihre Aktionen und Controller kommentieren.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET-Web-API 2

### <a name="attribute-routing"></a>Attributrouting

ASP.NET Web-API unterstützt jetzt Attributrouting, dank eines Beitrags [http://attributerouting.net](http://attributerouting.net)von Tim McCall, dem Autor von . Mit Attributrouting können Sie Ihre Web-API-Routen angeben, indem Sie Ihre Aktionen und Controller wie folgt kommentieren:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

Das Attributrouting gibt Ihnen mehr Kontrolle über die URIs in Ihrer Web-API. Sie können z. B. eine Ressourcenhierarchie einfach mit einem einzelnen API-Controller definieren:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

Das Attributrouting bietet auch eine praktische Syntax zum Angeben optionaler Parameter, Standardwerte und Routeneinschränkungen:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

Weitere Informationen zum Attributrouting finden Sie [unter Attributrouting in Web-API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).

### <a name="oauth-20"></a>OAuth 2.0

Die Projektvorlagen für Web-API und Einzelseitenanwendung unterstützen jetzt die Autorisierung mithilfe von OAuth 2.0. OAuth 2.0 ist ein Framework zum Autorisieren des Clientzugriffs auf geschützte Ressourcen. Es funktioniert für eine Vielzahl von Clients, einschließlich Browser und mobile Geräte.

Die Unterstützung für OAuth 2.0 basiert auf der neuen Sicherheits-Middleware, die von den Microsoft OWIN-Komponenten für die Bearer-Authentifizierung und die Implementierung der Autorisierungsserverrolle bereitgestellt wird. Alternativ können Clients über einen Organisationsautorisierungsserver wie Azure Active Directory oder ADFS in Windows Server 2012 R2 autorisiert werden.

### <a name="odata-improvements"></a>OData-Verbesserungen

**Unterstützung für $select, $expand, $batch und $value**

ASP.NET Web-API OData bietet jetzt vollständige Unterstützung für $select, $expand und $value. Sie können $batch auch für die Anforderungsbatching und Verarbeitung von Änderungssätzen verwenden.

Mit den Optionen $select und $expand können Sie die Form der Daten ändern, die von einem OData-Endpunkt zurückgegeben werden. Weitere Informationen finden Sie unter [Einführung $select und $expand Unterstützung in Web-API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).

**Verbesserte Erweiterbarkeit**

Die OData-Verfälssen sind jetzt erweiterbar. Sie können Atom-Eintragsmetadaten hinzufügen, benannte Stream- und Medienverknüpfungseinträge unterstützen, Instanzanmerkungen hinzufügen und anpassen, wie Links generiert werden.

**Typlose Unterstützung**

Sie können jetzt OData-Dienste erstellen, ohne CLR-Typen für Ihre Entitätstypen definieren zu müssen. Stattdessen können Ihre OData-Controller Instanzen von **IEdmObject**, bei denen es sich um die Serialisierung/Deserialisierung von OData-Formatters handelt, übernehmen oder zurückgeben.

**Wiederverwenden eines vorhandenen Modells**

Wenn Sie bereits über ein vorhandenes Entitätsdatenmodell (ENTITY data model, EDM) verfügen, können Sie es jetzt direkt wiederverwenden, anstatt ein neues erstellen zu müssen. Wenn Sie beispielsweise Entity Framework verwenden, können Sie das EDM verwenden, das EF für Sie erstellt.

### <a name="request-batching"></a>AnforderungBatching

Die Anforderungsbatching kombiniert mehrere Vorgänge in einer einzigen HTTP-POST-Anforderung, um den Netzwerkverkehr zu reduzieren und eine reibungslosere, weniger chattige Benutzeroberfläche bereitzustellen. ASP.NET Web-API unterstützt jetzt mehrere Strategien für die Anforderungsbatching:

- Verwenden Sie den $batch Endpunkt eines OData-Dienstes.
- Verpacken Sie mehrere Anforderungen in eine einzelne MIME-Mehrparteienanforderung.
- Verwenden Sie ein benutzerdefiniertes Batchformat.

Um die Anforderungsbatchverarbeitung zu aktivieren, fügen Sie einfach ihrer Web-API-Konfiguration eine Route mit einem Batchverarbeitungshandler hinzu:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

Sie können auch steuern, ob Anforderungen nacheinander oder in beliebiger Reihenfolge ausgeführt werden.

### <a name="portable-aspnet-web-api-client"></a>Portable ASP.NET Web-API-Client

Sie können jetzt den ASP.NET Web-API-Client verwenden, um portable Klassenbibliotheken zu erstellen, die in Ihren Windows Store- und Windows Phone 8-Anwendungen funktionieren. Sie können auch portable Formatters erstellen, die über Client und Server gemeinsam genutzt werden können.

### <a name="improved-testability"></a>Verbesserte Testbarkeit

Web API 2 erleichtert das Komponententesten Ihrer API-Controller erheblich. Instanziieren Sie einfach Ihren API-Controller mit Ihrer Anforderungsnachricht und Konfiguration, und rufen Sie dann die Aktionsmethode auf, die Sie testen möchten. Es ist auch einfach, die **UrlHelper-Klasse** für Aktionsmethoden zu verspotten, die die Linkgenerierung ausführen.

### <a name="ihttpactionresult"></a>IHttpActionResult

Sie können jetzt IHttpActionResult implementieren, um das Ergebnis Ihrer Web-API-Aktionsmethoden zu kapseln. Ein IHttpActionResult, das von einer Web-API-Aktionsmethode zurückgegeben wird, wird von der ASP.NET Web-API-Laufzeit ausgeführt, um die resultierende Antwortnachricht zu erzeugen. Ein IHttpActionResult kann von jeder Web-API-Aktion zurückgegeben werden, um das Komponententesten Ihrer Web-API-Implementierung zu vereinfachen. Der Einfachheit halber werden eine Reihe von IHttpActionResult-Implementierungen sofort bereitgestellt, einschließlich der Ergebnisse für die Rückgabe bestimmter Statuscodes, formatierter Inhalte oder inhaltsausgehandelter Antworten.

### <a name="httprequestcontext"></a>HttpRequestContext

Der neue **HttpRequestContext** verfolgt jeden Status, der an die Anforderung gebunden ist, aber nicht sofort von der Anforderung verfügbar ist. Sie können z. B. den **HttpRequestContext** verwenden, um Routendaten abzurufen, den der Anforderung zugeordneten Prinzipal, das Clientzertifikat, den **UrlHelper** und den virtuellen Pfadstamm. Sie können ganz einfach einen **HttpRequestContext** für Komponententests erstellen.

Da der Prinzipal für die Anforderung mit der Anforderung fließt, anstatt sich auf **Thread.CurrentPrincipal**zu verlassen, ist der Prinzipal jetzt während der gesamten Lebensdauer der Anforderung verfügbar, während er sich in der Web-API-Pipeline befindet.

### <a name="cors"></a>CORS

Dank eines weiteren großartigen Beitrags von Brock Allen unterstützt ASP.NET nun voll und ganz Cross Origin Request Sharing (CORS).

Die Browsersicherheit verhindert, dass eine Webseite AJAX-Anforderungen an eine andere Domäne richtet. [CORS](http://www.w3.org/TR/cors/) ist ein W3C-Standard, der es einem Server ermöglicht, die Richtlinie mit demselben Ursprung zu entspannen. Mit CORS kann ein Server explizit einige ursprungsübergreifende Anforderungen zulassen und andere ablehnen.

Web API 2 unterstützt jetzt CORS, einschließlich der automatischen Bearbeitung von Preflight-Anforderungen. Weitere Informationen finden Sie unter [Aktivieren von ursprungsübergreifenden Anforderungen in ASP.NET Web-API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).

### <a name="authentication-filters"></a>Authentifizierungsfilter

Authentifizierungsfilter sind eine neue Art von Filter in ASP.NET Web-API, die vor Autorisierungsfiltern in der ASP.NET Web-API-Pipeline ausgeführt werden und es Ihnen ermöglichen, authentifizierungslogik pro Aktion, pro Controller oder global für alle Controller anzugeben. Authentifizierungsfilter verarbeiten Anmeldeinformationen in der Anforderung und geben einen entsprechenden Prinzipal an. Authentifizierungsfilter können auch Authentifizierungsherausforderungen als Reaktion auf nicht autorisierte Anforderungen hinzufügen.

### <a name="filter-overrides"></a>Filterüberschreibungen

Sie können nun überschreiben, welche Filter auf eine bestimmte Aktionsmethode oder einen bestimmten Controller angewendet werden, indem Sie einen Außerkraftsetzungsfilter angeben. Überschreiben von Filtern gibt einen Satz von Filtertypen an, die nicht für einen bestimmten Bereich (Aktion oder Controller) ausgeführt werden sollen. Auf diese Weise können Sie globale Filter hinzufügen, dann aber einige von bestimmten Aktionen oder Controllern ausschließen.

### <a name="owin-integration"></a>OWIN-Integration

ASP.NET Web-API unterstützt jetzt vollständig OWIN und kann auf jedem OWIN-fähigen Host ausgeführt werden. Ebenfalls enthalten ist ein **HostAuthenticationFilter,** der die Integration mit dem OWIN-Authentifizierungssystem ermöglicht.

Mit der OWIN-Integration können Sie die Web-API in Ihrem eigenen Prozess zusammen mit anderen OWIN-Middleware, z. B. SignalR, selbst hosten. Weitere Informationen finden Sie unter [Verwenden von OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

In den folgenden Abschnitten werden die Funktionen von SignalR 2.0 beschrieben.

- [Auf OWIN aufgebaut](#builtonowin)
- [MapHubs und MapConnection sind jetzt MapSignalR](#MapSignalR)
- [Domänenübergreifende Unterstützung](#crossdomain)
- [iOS- und Android-Unterstützung über MonoTouch und MonoDroid](#mobile)
- [Portabler .NET-Client](#portable)
- [Neues Self-Host-Paket](#selfhost)
- [Abwärtskompatible Serverunterstützung](#backwardcompat)
- [Serverunterstützung für .NET 4.0 entfernt](#remove40)
- [Senden einer Nachricht an eine Liste von Clients und Gruppen](#messagelist)
- [Senden einer Nachricht an einen bestimmten Benutzer](#sendtouser)
- [Bessere Unterstützung bei der Fehlerbehandlung](#errorhandling)
- [Einfachere Komponentenprüfung von Hubs](#unittesting)
- [JavaScript-Fehlerbehandlung](#javascripterror)

Ein Beispiel für das Aktualisieren eines vorhandenen 1.x-Projekts auf SignalR 2.0 finden Sie unter [Aktualisieren eines SignalR 1.x-Projekts](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>Auf OWIN aufgebaut

SignalR 2.0 basiert vollständig auf [OWIN (Open Web Interface für .NET)](http://owin.org/). Diese Änderung macht den Setup-Prozess für SignalR viel konsistenter zwischen webgehosteten und selbst gehosteten SignalR-Anwendungen, erforderte aber auch eine Reihe von API-Änderungen.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs und MapConnection sind jetzt MapSignalR

Aus Gründen der Kompatibilität mit OWIN-Standards `MapSignalR`wurden diese Methoden in umbenannt. `MapSignalR`aufgerufen ohne Parameter werden alle `MapHubs` Hubs zugeordnet (wie in Version 1.x); Um einzelne **PersistentConnection-Objekte** zuzuordnen, geben Sie den Verbindungstyp als Typparameter und die URL-Erweiterung für die Verbindung als erstes Argument an.

Die `MapSignalR` Methode wird in einer Owin-Startklasse aufgerufen. Visual Studio 2013 enthält eine neue Vorlage für eine Owin-Startklasse. Gehen Sie wie folgt vor, um diese Vorlage zu verwenden:

1. Rechtsklick auf das Projekt
2. Auswählen **Add**, **New Item...**
3. Wählen Sie **Owin Startup-Klasse**. Benennen Sie die neue Klasse **Startup.cs**.

In einer **Webanwendung** wird die Owin-Startklasse, die die `MapSignalR` Methode enthält, dem Startprozess von Owin mithilfe eines Eintrags im Anwendungseinstellungsknoten der Datei Web.Config hinzugefügt, wie unten gezeigt.

In einer selbst gehosteten Anwendung wird die **Startup-Klasse**als Typparameter der `WebApp.Start` Methode übergeben.

**Zuordnen von Hubs und Verbindungen in SignalR 1.x (aus der globalen Anwendungsdatei in einer Webanwendung):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**Zuordnen von Hubs und Verbindungen in SignalR 2.0 (aus einer Owin Startup-Klassendatei):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

In einer selbst gehosteten Anwendung wird die **Startup-Klasse**als Typparameter für die `WebApp.Start` Methode übergeben, wie unten gezeigt.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>Domänenübergreifende Unterstützung

In SignalR 1.x wurden domänenübergreifende Anforderungen durch ein einzelnes EnableCrossDomain-Flag gesteuert. Dieses Flag steuerte sowohl JSONP- als auch CORS-Anforderungen. Für eine größere Flexibilität wurde die gesamte CORS-Unterstützung aus der Serverkomponente von SignalR entfernt (JavaScript-Clients verwenden CORS weiterhin normal, wenn festgestellt wird, dass der Browser dies unterstützt), und neue OWIN-Middleware wurde zur Unterstützung dieser Szenarien bereitgestellt.

Wenn in SignalR 2.0 JSONP auf dem Client erforderlich ist (zur Unterstützung domänenübergreifender Anforderungen in `EnableJSONP` älteren `HubConfiguration` Browsern), muss es explizit aktiviert werden, indem für das Objekt `true`auf , wie unten gezeigt, festgelegt wird. JSONP ist standardmäßig deaktiviert, da es weniger sicher als CORS ist.

Um die neue CORS-Middleware in SignalR `Microsoft.Owin.Cors` 2.0 hinzuzufügen, `UseCors` fügen Sie die Bibliothek zu Ihrem Projekt hinzu und rufen Sie vor Ihrer SignalR-Middleware auf, wie im folgenden Abschnitt gezeigt.

**Hinzufügen von Microsoft.Owin.Cors zu Ihrem Projekt:** Führen Sie den folgenden Befehl in der Package Manager-Konsole aus, um diese Bibliothek zu installieren:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

Mit diesem Befehl wird die Version 2.0.0 des Pakets zu Ihrem Projekt hinzugefügt.

**Aufrufen von UseCors**

Die folgenden Codeausschnitte veranschaulichen, wie domänenübergreifende Verbindungen in SignalR 1.x und 2.0 implementiert werden.

**Implementieren domänenübergreifender Anforderungen in SignalR 1.x (aus der globalen Anwendungsdatei)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**Implementieren domänenübergreifender Anforderungen in SignalR 2.0 (aus einer Codedatei von C')**

Der folgende Code veranschaulicht, wie CORS oder JSONP in einem SignalR 2.0-Projekt aktiviert wird. In diesem `Map` Codebeispiel wird anstelle `RunSignalR` von verwendet, `MapSignalR`sodass die CORS-Middleware nur für die SignalR-Anforderungen `MapSignalR`ausgeführt wird, die CORS-Unterstützung erfordern (und nicht für den gesamten Datenverkehr an dem unter .) angegebenen Pfad. `Map` kann auch für jede andere Middleware verwendet werden, die für ein bestimmtes URL-Präfix ausgeführt werden muss, und nicht für die gesamte Anwendung.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>iOS- und Android-Unterstützung über MonoTouch und MonoDroid

Unterstützung für iOS- und Android-Clients mit MonoTouch- und MonoDroid-Komponenten aus der [Xamarin-Bibliothek](https://xamarin.com/)wurde hinzugefügt. Weitere Informationen zur Verwendung dieser Komponenten finden Sie unter [Verwenden von Xamarin-Komponenten](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln). Diese Komponenten sind im [Xamarin Store](https://store.xamarin.com/) verfügbar, wenn die SignalR RTW-Version verfügbar ist.

<a id="portable"></a>• Tragbarer .NET-Client

Um die plattformübergreifende Entwicklung besser zu erleichtern, wurden die Silverlight-, WinRT- und Windows Phone-Clients durch einen einzigen tragbaren .NET-Client ersetzt, der die folgenden Plattformen unterstützt:

- NETTO 4,5
- Silverlight 5
- WinRT (.NET für Windows Store-Apps)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>Neues Self-Host-Paket

Es gibt jetzt ein NuGet-Paket, um den Einstieg in SignalR Self-Host (SignalR-Anwendungen, die in einem Prozess oder einer anderen Anwendung gehostet werden, anstatt auf einem Webserver) zu erleichtern. Um ein mit SignalR 1.x erstelltes Selbsthostprojekt zu aktualisieren, entfernen Sie das Microsoft.AspNet.SignalR.Owin-Paket, und fügen Sie das Microsoft.AspNet.SignalR.SelfHost-Paket hinzu. Weitere Informationen zu den ersten Informationen mit dem Self-Host-Paket finden Sie unter [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>Abwärtskompatible Serverunterstützung

In früheren Versionen von SignalR mussten die Versionen des SignalR-Pakets, die im Client und auf dem Server verwendet wurden, identisch sein. Um Anwendungen mit dickem Client zu unterstützen, die schwer zu aktualisieren wären, unterstützt SignalR 2.0 jetzt die Verwendung einer neueren Serverversion mit einem älteren Client. **Hinweis: SignalR 2.0 unterstützt keine Server, die mit älteren Versionen mit neueren Clients erstellt wurden.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>Serverunterstützung für .NET 4.0 entfernt

SignalR 2.0 hat die Unterstützung für die Serverinteroperabilität mit .NET 4.0 eingestellt. .NET 4.5 muss mit SignalR 2.0-Servern verwendet werden. Es ist immer noch ein .NET 4.0-Client für SignalR 2.0 vorhanden.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>Senden einer Nachricht an eine Liste von Clients und Gruppen

In SignalR 2.0 ist es möglich, eine Nachricht mithilfe einer Liste von Client- und Gruppen-IDs zu senden. Die folgenden Codeausschnitte veranschaulichen, wie Dies zu tun ist.

**Senden einer Nachricht an eine Liste von Clients und Gruppen mithilfe von PersistentConnection**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**Senden einer Nachricht an eine Liste von Clients und Gruppen mithilfe von Hubs**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>Senden einer Nachricht an einen bestimmten Benutzer

Mit dieser Funktion können Benutzer über eine neue Schnittstelle IUserIdProvider angeben, was die userId auf einer IRequest basiert:

**Die IUserIdProvider-Schnittstelle**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

Standardmäßig gibt es eine Implementierung, die die IPrincipal.Identity.Name des Benutzers als Benutzernamen verwendet.

In Hubs können Sie Nachrichten über eine neue API an diese Benutzer senden:

**Verwenden der Clients.User-API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>Bessere Unterstützung für die Fehlerbehandlung

Benutzer können jetzt **HubException** von jedem Hubaufruf auslösen. Der Konstruktor der **HubException** kann eine Zeichenfolgennachricht und ein Objekt zusätzliche Fehlerdaten annehmen. SignalR serialisiert die Ausnahme automatisch und sendet sie an den Client, wo sie zum Ablehnen/Failen des Hub-Methodenaufrufs verwendet wird.

Die Einstellung **detaillierte Hubausnahmen anzeigen** hat keinen Einfluss darauf, dass **HubException** an den Client zurückgesendet wird oder nicht. es wird immer gesendet.

**Serverseitiger Code, der das Senden einer HubException an den Client demonstriert**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**JavaScript-Clientcode, der die Reaktion auf eine vom Server gesendete HubException demonstriert**

[!code-html[Main](release-notes/samples/sample16.html)]

**.NET-Clientcode, der die Reaktion auf eine vom Server gesendete HubException demonstriert**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>Einfachere Komponentenprüfung von Hubs

SignalR 2.0 enthält `IHubCallerConnectionContext` eine Schnittstelle, die auf Hubs aufgerufen wird, die es einfacher macht, Mock-Client-Seitenaufrufe zu erstellen. Die folgenden Codeausschnitte veranschaulichen die Verwendung dieser Schnittstelle mit beliebten Testkabelbäumen [xUnit.net](https://github.com/xunit/xunit) und [moq](https://code.google.com/p/moq/).

**Komponententest SignalR mit xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Komponentenprüfung SignalR mit moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript-Fehlerbehandlung

In SignalR 2.0 geben alle JavaScript-Fehlerbehandlungsrückrufe JavaScript-Fehlerobjekte anstelle von unformatierten Zeichenfolgen zurück. Dadurch kann SignalR umfangreichere Informationen an Ihre Fehlerhandler weiterfließen lassen. Sie können die innere `source` Ausnahme von der Eigenschaft des Fehlers abrufen.

**JavaScript-Clientcode, der die Start.Fail-Ausnahme behandelt**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>Neues ASP.NET-Mitgliedschaftssystem

ASP.NET Identity ist das neue Mitgliedschaftssystem für ASP.NET Anwendungen. ASP.NET Identity erleichtert die Integration benutzerspezifischer Profildaten in Anwendungsdaten. ASP.NET Identität können Sie auch das Persistenzmodell für Benutzerprofile in Ihrer Anwendung auswählen. Sie können die Daten in einer SQL Server-Datenbank oder einem anderen Datenspeicher speichern, darunter auch NoSQL -Datenspeicher wie Azure Storage-Tabellen. Weitere Informationen finden Sie unter [Einzelne Benutzerkonten](creating-web-projects-in-visual-studio.md#indauth) unter **Erstellen ASP.NET Webprojekten in Visual Studio 2013**.

### <a name="claims-based-authentication"></a>Anspruchbasierte Authentifizierung

ASP.NET unterstützt jetzt die anspruchsbasierte Authentifizierung, bei der die Identität des Benutzers als eine Reihe von Ansprüchen eines vertrauenswürdigen Ausstellers dargestellt wird. Benutzer können mit einem Benutzernamen und Kennwort, das in einer Anwendungsdatenbank verwaltet wird, oder mithilfe von Anbietern sozialer Identitäten (z. B. Microsoft-Konten, Facebook, Google, Twitter) oder mithilfe von Organisationskonten über Azure Active Directory oder Active Directory-Verbunddienste (ADFS) authentifiziert werden.

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Integration mit Azure Active Directory und Windows Server Active Directory

Sie können jetzt ASP.NET Projekte erstellen, die Azure Active Directory oder Windows Server Active Directory (AD) für die Authentifizierung verwenden. Weitere Informationen finden Sie unter [Organisationskonten](creating-web-projects-in-visual-studio.md#orgauth) unter **Erstellen ASP.NET Webprojekten in Visual Studio 2013**.

### <a name="owin-integration"></a>OWIN-Integration

ASP.NET-Authentifizierung basiert jetzt auf OWIN-Middleware, die auf jedem OWIN-basierten Host verwendet werden kann. Weitere Informationen zu OWIN finden Sie im folgenden Abschnitt [Microsoft OWIN Components.](#TOC7)

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN-Komponenten

[Open Web Interface for .NET](http://owin.org/) (OWIN) definiert eine Abstraktion zwischen .NET-Webservern und Webanwendungen. OWIN entkoppelt die Webanwendung vom Server, wodurch Webanwendungen host-unabhängig werden. Sie können z. B. eine OWIN-basierte Webanwendung in IIS hosten oder in einem benutzerdefinierten Prozess selbst hosten.

Zu den Änderungen, die in den Microsoft OWIN-Komponenten (auch als Katana-Projekt bezeichnet) eingeführt wurden, gehören neue Server- und Hostkomponenten, neue Hilfsbibliotheken und Middleware sowie neue Authentifizierungsmiddleware.

Weitere Informationen zu OWIN und Katana finden Sie [unter Neuerungen in OWIN und Katana](../../../aspnet/overview/owin-and-katana/index.md).

**Hinweis: [OWIN-Anwendungen](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) können nicht im klassischen IIS-Modus ausgeführt werden. sie müssen im integrierten Modus ausgeführt werden.**

**Hinweis: [OWIN-Anwendungen](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) müssen in voller Vertrauenswürdigkeit ausgeführt werden.**

### <a name="new-servers-and-hosts"></a>Neue Server und Hosts

Mit dieser Version wurden neue Komponenten hinzugefügt, um Selbsthostszenarien zu aktivieren. Zu diesen Komponenten gehören die folgenden NuGet-Pakete:

- **Microsoft.Owin.Host.HttpListener**. Stellt einen OWIN-Server bereit, der **HttpListener** verwendet, um HTTP-Anforderungen zu verarbeiten und sie an die OWIN-Pipeline weiterzuleiten.
- **Microsoft.Owin.Hosting** Stellt eine Bibliothek für Entwickler bereit, die eine OWIN-Pipeline in einem benutzerdefinierten Prozess, z. B. einer Konsolenanwendung oder einem Windows-Dienst, selbst hosten möchten.
- **OwinHost**. Stellt eine eigenständige ausführbare `Microsoft.Owin.Hosting` Datei bereit, mit der Sie eine OWIN-Pipeline selbst hosten können, ohne eine benutzerdefinierte Hostanwendung schreiben zu müssen.

Darüber hinaus `Microsoft.Owin.Host.SystemWeb` ermöglicht das Paket nun Middleware, Hinweise an den **SystemWeb-Server** bereitzustellen, was darauf hinweist, dass die Middleware während einer bestimmten ASP.NET Pipelinephase aufgerufen werden soll. Diese Funktion ist besonders nützlich für Authentifizierungsmiddleware, die zu beginn der ASP.NET-Pipeline ausgeführt werden sollte.

### <a name="helper-libraries-and-middleware"></a>Hilfsbibliotheken und Middleware

Obwohl Sie OWIN-Komponenten nur mit den Funktions- und Typdefinitionen `Microsoft.Owin` aus der OWIN-Spezifikation schreiben können, bietet das neue Paket einen benutzerfreundlicheren Satz von Abstraktionen. Dieses Paket kombiniert mehrere frühere Pakete `Owin.Extensions`(z. B. , `Owin.Types`) zu einem einzigen, gut strukturierten Objektmodell, das dann problemlos von anderen OWIN-Komponenten verwendet werden kann. Tatsächlich verwenden die meisten Microsoft OWIN-Komponenten dieses Paket.

> [!NOTE]
> [OWIN-Anwendungen](http://www.owin.org) können nicht im klassischen IIS-Modus ausgeführt werden. sie müssen im integrierten Modus ausgeführt werden.

> [!NOTE]
> [OWIN-Anwendungen](http://www.owin.org) müssen in voller Vertrauenswürdigkeit ausgeführt werden.

Diese Version enthält auch das Microsoft.Owin.Diagnostics-Paket, das Middleware zum Überprüfen einer ausgeführten OWIN-Anwendung sowie Fehlerseiten-Middleware zur Untersuchung von Fehlern enthält.

### <a name="authentication-components"></a>Authentifizierungskomponenten

Die folgenden Authentifizierungskomponenten sind verfügbar.

- **Microsoft.Owin.Security.ActiveDirectory**. Ermöglicht die Authentifizierung mithilfe von lokalen oder cloudbasierten Verzeichnisdiensten.
- **Microsoft.Owin.Security.Cookies** Aktiviert die Authentifizierung mithilfe von Cookies. Dieses Paket hatte `Microsoft.Owin.Security.Forms`zuvor den Namen .
- **Microsoft.Owin.Security.Facebook** Aktiviert die Authentifizierung mithilfe des OAuth-basierten Dienstes von Facebook.
- **Microsoft.Owin.Security.Google** Aktiviert die Authentifizierung mit dem OpenID-basierten Dienst von Google.
- **Microsoft.Owin.Security.Jwt** Aktiviert die Authentifizierung mit JWT-Token.
- **Microsoft.Owin.Security.MicrosoftAccount** Aktiviert die Authentifizierung mit Microsoft-Konten.
- **Microsoft.Owin.Security.OAuth**. Stellt einen OAuth-Autorisierungsserver sowie Middleware für die Authentifizierung von Inhabertoken bereit.
- **Microsoft.Owin.Security.Twitter** Aktiviert die Authentifizierung mithilfe des OAuth-basierten Dienstes von Twitter.

Diese Version enthält `Microsoft.Owin.Cors` auch das Paket, das Middleware für die Verarbeitung von ursprungsübergreifenden HTTP-Anforderungen enthält.

> [!NOTE]
> Die Unterstützung für JWT-Signaturen wurde in der endgültigen Version von Visual Studio 2013 entfernt.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

Eine Liste der neuen Features und anderer Änderungen in Entity Framework 6 finden Sie unter [Entity Framework Version History](https://msdn.com/data/jj574253).

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3 enthält die folgenden neuen Funktionen:

- Unterstützung für Tab-Bearbeitung. Zuvor funktionierten der Befehl **Dokument formatieren,** automatischeeindrungen und automatische Formatierung in Visual Studio nicht ordnungsgemäß, wenn die Option **Registerkarten beibehalten** verwendet wurde. Diese Änderung korrigiert die Visual Studio-Formatierung für Razor-Code für die Registerkartenformatierung.
- Unterstützung für URL-Rewrite-Regeln beim Generieren von Links.
- Entfernen des sicherheitstransparenten Attributs.
  > [!NOTE]
  > Dies ist eine bahnbrechende Änderung und macht Razor 3 inkompatibel mit MVC4 und früher, während Razor 2 mit MVC5 oder Assemblys, die für MVC5 kompiliert wurden, nicht kompatibel ist.

Razor 3-Probleme, die in Visual Studio 2013 aus Vorabversionen behoben wurden, finden Sie [hier](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET App Suspend

ASP.NET App Suspend ist eine bahnbrechende Funktion in .NET Framework 4.5.1, die die Benutzerfreundlichkeit und das Wirtschaftsmodell für das Hosten einer großen Anzahl von ASP.NET Websites auf einem einzigen Computer radikal ändert. Weitere Informationen finden Sie unter [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>Bekannte Probleme und brechende Änderungen

In diesem Abschnitt werden bekannte Probleme und Änderungen in den ASP.NET und Webtools für Visual Studio 2013 beschrieben.

### <a name="nuget"></a>NuGet

- [Neue Paketwiederherstellung funktioniert auf Mono nicht, wenn SLN-Datei](https://nuget.codeplex.com/workitem/3596) verwendet wird – wird in einem kommenden nuget.exe-Download und [NuGet.CommandLine-Paketupdate](http://www.nuget.org/packages/NuGet.CommandLine/) behoben.
- [Neue Paketwiederherstellung funktioniert nicht mit Wix-Projekten](https://nuget.codeplex.com/workitem/3598) – wird in einem kommenden nuget.exe-Download und [NuGet.CommandLine-Paketupdate](http://www.nuget.org/packages/NuGet.CommandLine/) behoben.
- [Die automatische Paketwiederherstellung funktioniert nicht für Projekte unter einem Projektmappenordner](https://nuget.codeplex.com/workitem/3625) – wird in NuGet 2.8 behoben.

### <a name="aspnet-web-api"></a>ASP.NET-Web-API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`kehrt nicht `IQueryable<T>` immer zurück, da `$select` wir `$expand`Unterstützung für und hinzugefügt haben.

    Unsere früheren `ODataQueryOptions<T>` Beispiele für immer den `ApplyTo` `IQueryable<T>`Rückgabewert von nach gegossen. Dies funktionierte früher, da die`$filter`zuvor `$orderby` `$skip`unterstützten Abfrageoptionen ( , , `$top`, ) die Form der Abfrage nicht ändern. Jetzt, da `$select` `$expand` wir unterstützen `ApplyTo` und der `IQueryable<T>` Rückgabewert von wird nicht immer sein.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    Wenn Sie den Beispielcode von früher verwenden, funktioniert er `$select` weiter, wenn der Client nicht sendet und `$expand`. Wenn Sie jedoch unterstützen `$select` `$expand` möchten und diesen Code ändern müssen.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **Request.Url oder RequestContext.Url ist während einer Batchanforderung null**

    In einem Batchszenario ist **UrlHelper** null, wenn von **Request.Url** oder **RequestContext.Url**zugegriffen wird.

    Dieses Problem wird derzeit hier nachverfolgt: [BatchRequestContext.Url ist null für Batching-Anforderung](http://aspnetwebstack.codeplex.com/workitem/1301).

    Die Problemumgehung für dieses Problem besteht darin, eine neue Instanz von **UrlHelper**zu erstellen, wie im folgenden Beispiel:

    **Erstellen einer neuen UrlHelper-Instanz**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. Wenn Sie MVC5 und OrgAuth verwenden, können Sie beim Buchen von Daten in der Ansicht auf den folgenden Fehler stoßen, wenn Sie Ansichten haben, die die AntiForgerToken-Validierung durchführen:

    **Fehler**:

    *Serverfehler in der '/' Anwendung.*

    <em>Ein Anspruch des<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>Typs<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' oder ' ' war auf der bereitgestellten ClaimsIdentity nicht vorhanden. Um die Unterstützung von Anti-Fälschungstoken mit anspruchsbasierter Authentifizierung zu aktivieren, stellen Sie sicher, dass der konfigurierte Anspruchsanbieter beide Ansprüche für die von ihm generierten ClaimsIdentity-Instanzen bereitstellt. Wenn der konfigurierte Anspruchsanbieter stattdessen einen anderen Anspruchstyp als eindeutigen Bezeichner verwendet, kann er durch Festlegen der statischen Eigenschaft AntiForgeryConfig.UniqueClaimTypeIdentifier konfiguriert werden.</em>

    **Problemumgehung**:

    Fügen Sie die folgende Zeile in Global.asax hinzu, um sie zu beheben:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    Dies wird für die nächste Version behoben.
2. Erstellen Sie nach dem Upgrade einer MVC4-App auf MVC5 die Lösung, und starten Sie sie. Der folgende Fehler sollte angezeigt werden:

    [A] System.Web.WebPages.Razor.Configuration.HostSection kann nicht in [B]System.WebPages.Razor.Configuration.HostSection umgecastet werden. Typ A stammt aus 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' im Kontext 'Default' an der\_Position 'C:'windows'Microsoft.Net'assembly'GAC MSIL'System.WebPages.Razor'v4.0\_2.0.0.0.0\_\_31bf3856ad364e35'System.WebPages.WebPages.Razor.dll'. Typ B stammt aus 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' im Kontext 'Standard' am Speicherort 'C:'Windows'Microsoft.NET'Framework'v4.0.30319'Temporary ASP.NET Files'root'6d 05bbd0-e8b5908e-Assembly-dl3-c9cbca63-f8910382\_6273ce01-System.Web.WebPages.Razor.dll'.

    Um den obigen Fehler zu beheben, öffnen Sie *alle* Web.config-Dateien (einschließlich der Dateien im Ordner Ansichten) in Ihrem Projekt, und gehen Sie wie folgt vor:

   1. Aktualisieren Sie alle Vorkommen der Version "4.0.0.0" von "System.Web.Mvc" auf "5.0.0.0".
   2. Aktualisieren Sie alle Vorkommen der Version "2.0.0.0" von &quot;"System.Web.Helpers", System.Web.WebPages&quot; und &quot;System.WebPages.Razor&quot; auf "3.0.0.0"

      Nachdem Sie z. B. die obigen Änderungen vorgenommen haben, sollten die Assemblybindungen wie folgt aussehen:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      Informationen zum Aktualisieren von MVC 4-Projekten auf MVC 5 finden Sie unter So aktualisieren Sie [ein ASP.NET MVC 4- und Web-API-Projekt auf ASP.NET MVC 5 und Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).
3. Bei verwendung der clientseitigen Validierung mit jQuery Unobtrusive Validation ist die Validierungsmeldung für ein HTML-Eingabeelement mit type='number' manchmal falsch. Der Validierungsfehler für einen erforderlichen Wert ("Das Feld Alter ist erforderlich") wird angezeigt, wenn eine ungültige Zahl anstelle der richtigen Meldung eingegeben wird, dass eine gültige Zahl erforderlich ist.

    Dieses Problem wird häufig bei Gerüstcode für ein Modell mit einer ganzzahligen Eigenschaft in den Ansichten Erstellen und Bearbeiten gefunden.

    Um dieses Problem zu umgehen, ändern Sie den Editor-Helfer von:

    `@Html.EditorFor(person => person.Age)`

    in:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 unterstützt keine teilweise Vertrauensstellung mehr. Projekte, die mit den MVC- oder WebAPI-Binärdateien verknüpft sind, sollten das [SecurityTransparent-Attribut](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) und das [AllowPartiallyTrustedCallers-Attribut](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) entfernen. Durch das Entfernen dieser Attribute werden Compilerfehler wie die folgenden beseitigt.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > Beachten Sie, dass Sie als Nebeneffekt 4.0- und 5.0-Assemblys nicht in derselben Anwendung verwenden können. Sie müssen alle auf 5.0 aktualisieren.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>SPA-Vorlage mit Facebook-Autorisierung kann inIE instabil werden, während die Website in der Intranetzone gehostet wird

Die SPA-Vorlage bietet eine externe Anmeldung bei Facebook. Wenn das mit der Vorlage erstellte Projekt lokal ausgeführt wird, kann die Anmeldung zu einem Absturz von IE führen.

Lösung:

1. Hosten der Website in der Internetzone; Oder

2. Testen Sie das Szenario in einem anderen Browser als IE.

### <a name="web-forms-scaffolding"></a>Web Forms-Gerüst

Web Forms Scaffolding wurde aus VS2013 entfernt und wird in einem zukünftigen Update für Visual Studio verfügbar sein. Sie können jedoch weiterhin Gerüste in einem Web Forms-Projekt verwenden, indem Sie MVC-Abhängigkeiten hinzufügen und Gerüste für MVC generieren. Ihr Projekt enthält eine Kombination aus Web Forms und MVC.

Um MVC zu Ihrem Web Forms-Projekt hinzuzufügen, fügen Sie ein neues Gerüstelement hinzu, und wählen Sie **MVC 5 Abhängigkeiten**aus. Wählen Sie entweder Minimal oder Full aus, je nachdem, ob Sie alle Inhaltsdateien benötigen, z. B. Skripts. Fügen Sie dann ein Gerüstelement für MVC hinzu, das Ansichten und einen Controller in Ihrem Projekt erstellt.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC- und Web-API-Gerüstbau - HTTP 404, Fehler nicht gefunden

Wenn beim Hinzufügen eines Gerüstelements zu einem Projekt ein Fehler auftritt, ist es möglich, dass das Projekt in einem inkonsistenten Zustand bleibt. Einige der vorgenommenen Änderungen als Gerüste werden zurückgesetzt, andere Änderungen, wie z. B. die installierten NuGet-Pakete, werden nicht zurückgesetzt. Wenn die Änderungen der Routingkonfiguration zurückgesetzt werden, erhalten Benutzer beim Navigieren zu Gerüstelementen einen HTTP 404-Fehler.

Problemumgehung:

- Um diesen Fehler für MVC zu beheben, fügen Sie ein neues Gerüstelement hinzu, und wählen Sie MVC 5-Abhängigkeiten (minimal oder vollständig). Dieser Prozess fügt dem Projekt alle erforderlichen Änderungen hinzu.
- So beheben Sie diesen Fehler für die Web-API:

  1. Fügen Sie ihrem Projekt die WebApiConfig-Klasse hinzu.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. Konfigurieren Sie WebApiConfig.Register\_in der Application Start-Methode in Global.asax wie folgt:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
