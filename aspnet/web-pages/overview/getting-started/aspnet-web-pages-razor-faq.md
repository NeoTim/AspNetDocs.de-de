---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: häufig gestellte Fragen zu ASP.NET Webseiten (Razor) | Microsoft Docs
author: Rick-Anderson
description: In diesem Artikel werden einige häufig gestellte Fragen zu ASP.NET Webseiten (Razor) und WebMatrix aufgelistet. Softwareversionen, die im Tutorial ASP.NET Webseiten (R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543703"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET-Webseiten (Razor) – FAQs

 von [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix wird nicht mehr als integrierte Entwicklungsumgebung für ASP.NET Webseiten empfohlen. Verwenden Sie [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) oder Visual [Studio Code](https://code.visualstudio.com/).
>
> In diesem Artikel werden einige häufig gestellte Fragen zu ASP.NET Webseiten (Razor) und WebMatrix aufgelistet.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Im Tutorial verwendete Softwareversionen
> 
> 
> - ASP.NET Webseiten (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> Dieses Tutorial funktioniert auch mit ASP.NET Webseiten 2, WebMatrix 2 und Visual Studio 2012.

- [Was ist der Unterschied zwischen ASP.NET Webseiten, ASP.NET Web forms und ASP.NET MVC?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [Benötige ich WebMatrix, um mit Webseiten arbeiten zu können?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [Kann ich ASP.NET Web Forms-Steuerelemente auf einer Webseitenseite verwenden?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [Kann ich eine ASP.NET Webseiten-Website bereitstellen, ohne WebMatrix zu verwenden?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [Muss ich den WebSecurity-Hilfsprogramm verwenden, um Anmeldungen zu unterstützen?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [Unterstützt ASP.NET Webseiten HTML5?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [Kann ich JavaScript und jQuery mit Webseiten verwenden?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [Zusätzliche Ressourcen](#AdditionalResources)

Fragen zu Fehlern und anderen Problemen finden Sie im [ASP.NET-Leitfaden zur Fehlerbehebung auf Webseiten (Razor).](https://go.microsoft.com/fwlink/?LinkId=253001)

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>Was ist der Unterschied zwischen ASP.NET Webseiten, ASP.NET Web forms und ASP.NET MVC?

Alle drei sind ASP.NET Technologien zum Erstellen dynamischer Webanwendungen:

- ASP.NET WebPages konzentriert sich auf das Hinzufügen von dynamischem (serverseitigem) Code und Datenbankzugriff auf HTML-Seiten und bietet einfache und einfache Syntax.
- ASP.NET Web Forms basiert auf einem Seitenobjektmodell und herkömmlichen Steuerelementen vom Fenstertyp (Schaltflächen, Listen usw.). Web Forms verwendet ein ereignisbasiertes Modell, das denjenigen vertraut ist, die mit der clientbasierten Entwicklung (Windows Forms) gearbeitet haben.
- ASP.NET MVC implementiert das Modellansichts-Controller-Muster für ASP.NET. Der Schwerpunkt liegt auf der "Trennung von Anliegen" (Verarbeitung, Daten und UI-Layer).

Alle drei Frameworks werden vom ASP.NET-Team umfassend unterstützt und weiter entwickelt. Im Allgemeinen hängt die Wahl des zu verwendenden Frameworks von Ihrem Hintergrund und Ihren Erfahrungen mit ASP.NET ab.

ASP.NET Webseiten wurde entwickelt, um es Personen, die HTML bereits kennen, leicht zu machen, ihren Seiten Serververarbeitung hinzuzufügen. Es ist eine gute Wahl für Studenten, Bastler, Menschen im Allgemeinen, die neu in der Programmierung sind. Es kann auch eine gute Wahl für Entwickler sein, die Erfahrung mit non-ASP.NET Web-Technologien haben.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>Benötige ich WebMatrix, um mit Webseiten arbeiten zu können?

Nein. WebMatrix wird nicht mehr als integrierte Entwicklungsumgebung für ASP.NET Webseiten empfohlen. Verwenden Sie [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) oder Visual [Studio Code](https://code.visualstudio.com/).

Wenn Sie weder Visual Studio noch Visual Studio Code verwenden möchten, können Sie die Komponentenprodukte einzeln mit [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)installieren. Sie benötigen folgende Produkte:

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (das auch das ASP.NET-Webpages-Framework installiert)
- IIS Express (der Webserver)
- Microsoft SQL Server Compact 4.0 (Datenbank)

Sie können einen Texteditor verwenden, um *.cshtml* (oder *.vbhtml*) Seiten zu bearbeiten.

Die Verwaltung von SQL Server Compact-Datenbanken *(Sdf-Dateien)* ohne Tool ist etwas schwieriger. Visual Studio enthält Tools zum Verwalten *von .sdf-Datenbanken.* Sie können SQL-Befehle auch im Code ausführen, um viele SQL Server-Verwaltungsaufgaben auszuführen.

Um *.cshtml-Seiten* zu testen, ohne eine integrierte Entwicklungsumgebung (IDE) zu verwenden, können Sie sie auf einem Live-Server bereitstellen. (Siehe [Kann ich eine ASP.NET Webseiten-Website bereitstellen, ohne WebMatrix](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)zu verwenden? )

### <a name="running-iis-express-without-using-an-ide"></a>Ausführen von IIS Express ohne Verwendung einer IDE

Wenn Sie IIS Express auf Ihrem Computer als Webserver installieren, können Sie die Seiten damit testen. Sie können IIS Express über die Befehlszeile ausführen und es einer bestimmten Portnummer zuordnen. Sie geben diesen Port dann an, wenn Sie *.cshtml-Dateien* in Ihrem Browser anfordern.

Öffnen Sie in Windows eine Eingabeaufforderung mit Administratorrechten, und wechseln Sie zu *C:-Programmdateien und IIS Express.* (Verwenden Sie für 64-Bit-Systeme den Ordner *C:-Programmdateien (x86) und IIS Express.)* Geben Sie dann den folgenden Befehl ein, indem Sie den eigentlichen Pfad zu Ihrer Site verwenden:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

Sie können eine beliebige Portnummer verwenden, die noch nicht von einem anderen Prozess reserviert ist. (Portnummern über 1024 sind in der Regel frei.) Verwenden `path` Sie für den Wert den Pfad des Websiteordners, in dem sich die *.cshtml-Dateien* befinden.

Nachdem Sie diesen Befehl ausgeführt haben, um IIS Express für ihre Seiten einzurichten, können Sie einen Browser öffnen und zu einer *.cshtml-Datei* navigieren. Verwenden Sie eine URL wie die folgende:

`http://localhost:35896/default.cshtml`

Geben Sie die Befehlszeile der `iisexpress.exe /?` Befehlszeilen in der Befehlszeile ein, um Hilfe zu den IIS Express-Befehlszeilenoptionen zu erhalten.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>Kann ich ASP.NET Web Forms-Steuerelemente auf einer Webseitenseite verwenden?

Nein. Web Forms-Steuerelemente wie das [CheckBox-Steuerelement,](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) die [Validierungssteuerelemente](https://msdn.microsoft.com/library/bwd43d0x)und das [GridView-Steuerelement](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) funktionieren nur in Web Forms-Seiten (*ASPX-Dateien).* Für diese Steuerelemente ist das Web Forms-Seitenframework erforderlich.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>Kann ich eine ASP.NET Webseiten-Website bereitstellen, ohne WebMatrix zu verwenden?

Ja. Sie können Websitedateien manuell auf einen Server kopieren (in der Regel mithilfe von FTP). Wenn Sie eine manuelle Kopie durchführen, müssen Sie auch die Dateien kopieren, die SQL Server Compact (die Datenbank) unterstützen. Weitere Informationen finden Sie im Blogeintrag [Bereitstellen von Webseitenanwendungen ohne Tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>Muss ich den WebSecurity-Hilfsprogramm verwenden, um Anmeldungen zu unterstützen?

Nein. Der `SimpleMembership` Anbieter, der Teil ASP.NET Webseiten ist, ist eine Option. Die Sicherheitsanbieter, die Teil von ASP.NET sind (die Sie möglicherweise in Web forms arbeiten können), sind ebenfalls verfügbar. Sie können beispielsweise die Formularauthentifizierung in ASP.NET Webseiten genauso verwenden wie in Webforms. Ein Beispiel für die Verwendung der Formularauthentifizierung finden Sie im Microsoft Support-Artikel [So implementieren Sie formularbasierte Authentifizierung in Ihrer ASP.NET Anwendung mithilfe von C.NET](https://support.microsoft.com/kb/301240). Informationen zum Herunterladen eines einfachen Beispiels finden Sie [in ASP.NET Version von "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Informationen zur Verwendung der Windows-Authentifizierung finden Sie im Blogbeitrag [Verwenden der Windows-Authentifizierung in ASP.NET Webseiten](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>Unterstützt ASP.NET Webseiten HTML5?

Ja. Die Seiten, die Sie mit ASP.NET Webseiten erstellen (*.cshtml* oder *.vbhtml-Seiten)* sind im Wesentlichen HTML-Seiten, die auch Code enthalten, der auf dem Server ausgeführt wird, bevor die Seite gerendert wird. Solange der Browser des Benutzers HTML5 unterstützt, können Sie HTML5-Elemente in einer *.cshtml-* oder *VBhtml-Seite* verwenden.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>Kann ich JavaScript und jQuery mit Webseiten verwenden?

Absolut. Die Seiten, die Sie mit ASP.NET Webseiten erstellen (*.cshtml* oder *.vbhtml-Seiten)* sind nur HTML-Seiten mit Servercode darin. Daher können Sie alles, was Sie in einer normalen HTML-Seite tun können, indem Sie JavaScript oder jQuery verwenden, auch auf einer *.cshtml-* oder *VBhtml-Seite* tun.

Die **Starter Site-Vorlage** in WebMatrix enthält eine Reihe von jQuery-Bibliotheken. Wenn Sie eine Website mithilfe dieser Vorlage erstellen, enthält der *Ordner Scripts* eine jQuery-Kernbibliothek (*jquery-1.6.2.js)* und Bibliotheken für die jQuery-Validierung (*jquery.validate.js*usw.).

Im Folgenden finden Sie einige Blogbeiträge, die die Verwendung von jQuery mit ASP.NET Webseiten veranschaulichen:

- [Hinzufügen von jQuery Goodness zu ASP.NET Webseiten mit WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) von Rachel Appel
- [5 Min: WebMatrix + jQuery UI + json + jQuery Vorlagen](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) von Jonas Eriksson
- [WebMatrix und jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) von Mike Brind

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Weitere Ressourcen

[Leitfaden zur Behandlung von Problemen mit ASP.NET Web Pages (Razor)](https://go.microsoft.com/fwlink/?LinkId=253001)

[WebMatrix und ASP.NET Webseiten-Forum](https://forums.asp.net/1224.aspx/1?WebMatrix) auf der ASP.NET-Website
