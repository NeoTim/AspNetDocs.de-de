---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Versionshinweise für ASP.NET und Webtools 2013.1 für Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools 2013.1 für Visual Studio 2012 beschrieben.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543573"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Anmerkungen zu dieser Version – ASP.NET and Web Tools 2013.1 für Visual Studio 2012

von [Microsoft](https://github.com/microsoft)

> In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools 2013.1 für Visual Studio 2012 beschrieben.

## <a name="contents"></a>Contents

- [Installationshinweise](#install)
- [Software-Anforderungen](#requirements)
- Neue Funktionen in ASP.NET und Webtools 2013.1 für Visual Studio 2012

    - [Bootstrap](#bootstrap)
    - [Vorlagen](#templates)

        - [ASP.NET MVC 5-Vorlage](#mvc5template)
        - [ASP.NET Web-API 2-Vorlage](#apitemplate)
        - [Elementvorlagen](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET Gerüst](#scaffold)
    - [Razor Editor](#razor)
    - [NuGet 2.7](#nuget)
- Bekannte Probleme und brechende Änderungen

    - [ASP.NET Gerüst](#issuescaffolding)

        - [MVC- und Web-API-Gerüstbau - HTTP 404, Fehler nicht gefunden](#404issue)
        - [Visual Studio Express 2012 für Web funktioniert nach dem Hinzufügen eines Gerüstelements nicht mehr](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Das Anzeigen der cshtml-Datei mit Browse With oder F5 verursacht einen Serverfehler](#browseissue)
        - [Url Rewrite und Tilde()](#rewriteissue)
    - [Vorlagen](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Installationshinweise

[Installieren](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET und Webtools 2013.1 für Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Softwareanforderungen

Sie müssen entweder Über Visual Studio 2012 oder Visual Studio Express 2012 für Web verfügen.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Neue Funktionen in ASP.NET und Webtools 2013.1 für Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

Wenn Sie MVC 5-Controller und -Ansichten auf gerüsten, verwendet das Markup für die Ansichten [Bootstrap](http://getbootstrap.com/).

<a id="templates"></a>
### <a name="templates"></a>Vorlagen

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5-Vorlage

Wir haben eine neue MVC 5-Vorlage hinzugefügt. Es verweist auf die neuesten MVC 5 NuGet-Pakete, und Sie können Gerüste verwenden, um Controller und Ansichten hinzuzufügen.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web-API 2-Vorlage

Wir haben eine neue Web API 2-Vorlage hinzugefügt. Es verweist auf die neuesten NuGet-Pakete der Web-API 2, und Sie können Gerüste verwenden, um Controller und Ansichten hinzuzufügen.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Elementvorlagen

Wir haben neue Elementvorlagen für MVC 5-Ansichten, Webseiten (Razor 3) und Web-API 2-Controller hinzugefügt. Sie installieren die zugehörigen NuGet-Pakete zum Projekt, während sie neue Elemente hinzufügen.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Wenn Sie einen MVC- oder Web-API-Controller mit Entity Framework erstellen, verwenden wir Framework 6. Weitere Informationen zu Entity Framework finden Sie im [Entity Framework-Versionsverlauf](https://msdn.com/data/jj574253).

Sie können auch entity Framework 6 Tools für Visual Studio 2012 herunterladen und installieren. Siehe [Get Entity Framework](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Gerüst

ASP.NET Scaffolding ist ein Codegenerierungsframework für ASP.NET Webanwendungen. Es erleichtert das Hinzufügen von Boilerplate-Code zu Ihrem Projekt, das mit einem Datenmodell interagiert.

In früheren Versionen von Visual Studio war das Gerüst auf ASP.NET MVC-Projekte beschränkt. Mit diesem Update können Sie jetzt Gerüste für jedes ASP.NET Projekt verwenden, einschließlich Web Forms. Dieses Update unterstützt das Generieren von Seiten für ein Web Forms-Projekt nicht, aber Sie können dennoch Gerüste mit Web forms verwenden, indem Sie dem Projekt MVC-Abhängigkeiten hinzufügen. Unterstützung für das Generieren von Seiten für Web forms wird in einem zukünftigen Update hinzugefügt.

Bei der Verwendung von Gerüsten stellen wir sicher, dass alle erforderlichen Abhängigkeiten im Projekt installiert sind. Wenn Sie beispielsweise mit einem ASP.NET Web Forms-Projekt beginnen und dann gerüstbauweise einen Web-API-Controller hinzufügen, werden die erforderlichen NuGet-Pakete und -Referenzen automatisch zu Ihrem Projekt hinzugefügt.

Um einem Web Forms-Projekt Ein MVC-Gerüst hinzuzufügen, fügen Sie ein **neues Gerüstelement** hinzu, und wählen Sie **mVC 5 Abhängigkeiten** im Dialogfeld aus. Es gibt zwei Möglichkeiten für Gerüste MVC; Minimal und voll. Wenn Sie Minimal auswählen, werden Ihrem Projekt nur die NuGet-Pakete und -Referenzen für ASP.NET MVC hinzugefügt. Wenn Sie die Option Voll auswählen, werden die minimalen Abhängigkeiten sowie die erforderlichen Inhaltsdateien für ein MVC-Projekt hinzugefügt.

Unterstützung für Gerüst-Asynchron-Controller verwendet die neuen asynchronen Features von Entity Framework 6.

Weitere Informationen und Tutorials finden Sie unter [ASP.NET Gerüstübersicht](../2013/aspnet-scaffolding-overview.md). Diese Tutorials zeigen Gerüste mit Visual Studio 2013, sind jedoch auch für ASP.NET und Webtools 2013.1 für Visual Studio 2012 anwendbar.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor Editor

Mit diesem Update unterstützt Visual Studio 2012 jetzt Razor 3-Tools/-bearbeitungen.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 enthält eine Vielzahl neuer Funktionen, die in [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7)ausführlich beschrieben werden.

Diese Version von NuGet entfällt die Notwendigkeit für Benutzer, NuGet explizit die Wiederherstellung fehlender Pakete zu erlauben. Bei der Installation von NuGet 2.7 stimmen Benutzer implizit der automatischen Wiederherstellung fehlender Pakete zu. Benutzer können die Paketwiederherstellung über die NuGet-Einstellungen in Visual Studio explizit deaktivieren. Diese Änderung vereinfacht die Funktionsweise der Paketwiederherstellung.

## <a name="known-issues-and-breaking-changes"></a>Bekannte Probleme und brechende Änderungen

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET Gerüst

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC- und Web-API-Gerüstbau - HTTP 404, Fehler nicht gefunden

Wenn beim Hinzufügen eines Gerüstelements zu einem Projekt ein Fehler auftritt, ist es möglich, dass das Projekt in einem inkonsistenten Zustand bleibt. Einige der vorgenommenen Änderungen als Gerüste werden zurückgesetzt, andere Änderungen, wie z. B. die installierten NuGet-Pakete, werden nicht zurückgesetzt. Wenn die Änderungen der Routingkonfiguration zurückgesetzt werden, erhalten Benutzer beim Navigieren zu Gerüstelementen einen HTTP 404-Fehler.

Um diesen Fehler für MVC zu beheben, fügen Sie ein neues Gerüstelement hinzu, und wählen Sie MVC 5-Abhängigkeiten (minimal oder vollständig). Dieser Prozess fügt dem Projekt alle erforderlichen Änderungen hinzu.

So beheben Sie diesen Fehler für die Web-API:

1. Fügen Sie Ihrem Projekt die folgende WebApiConfig-Klasse hinzu.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Konfigurieren Sie WebApiConfig.Register\_in der Application Start-Methode in Global.asax wie folgt:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 für Web funktioniert nach dem Hinzufügen eines Gerüstelements nicht mehr

Wenn Visual Studio Express 2012 für Web nach dem Hinzufügen eines Gerüstelements mit Entity Framework (z. B. Web API 2 Controller mit Aktionen unter Verwendung von Entity Framework) nicht mehr funktioniert, ist es möglich, dass Visual Studio Express das systemeigene Abbild einer Assembly, die von System.Web.Extensions abhängig ist, nicht geladen hat.

Um dieses Problem zu beheben, konfigurieren Sie Visual Studio Express so, dass es mit dem MSIL-Abbild von System.Web.Extensions funktioniert:

1. Öffnen Sie die Eingabeaufforderung im Administratormodus.
2. Wechseln Sie zu %ProgramFiles%'Microsoft Visual Studio 11.0'Common7'IDE oder %ProgramFiles(x86)%'Microsoft Visual Studio 11.0'Common7'IDE (für 64-Bit-Windows).
3. Öffnen Sie VWDExpress.exe.config in einem Texteditor.
4. Fügen Sie die &lt;folgende&gt;/&lt;Zeile&gt; unter dem Konfigurationslaufzeitelement hinzu:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Starten Sie Visual Studio Express 2012 für Web neu.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Das Anzeigen der cshtml-Datei mit Browse With oder F5 verursacht einen Serverfehler

Wenn Sie ein MVC 5-Projekt in Visual Studio 2012 erstellen (oder in Visual Studio 2012 ein MVC 5-Projekt öffnen, das in Visual Studio 2013 erstellt wurde) und versuchen, eine cshtml-Datei mithilfe von Durchsuchen With oder F5 anzuzeigen, wird eine Fehlermeldung angezeigt, die angibt: **Serverfehler in '/' Anwendung**. Der Server versucht, zu`http://localhost:XXXX/Views/../XXXX.cshtml`

Um dieses Problem zu beheben, ändern Sie die Einstellung **Startaktion** in Ihrem Projekt in **Spezifische Seite**. Sie müssen keinen Wert für die Seite angeben.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Nachdem Sie diese Änderung vornehmen, navigiert die`http://localhost:XXXX`Auswahl von F5 zum Stamm der Anwendung ( ). Dieses Verhalten entspricht nicht dem Verhalten für MVC 5-Projekte in Visual Studio 2013, bei dem die Einstellung **Aktuelle Seite** die geöffnete Seite startet.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url Rewrite und Tilde()

Nach dem Upgrade auf ASP.NET Razor 3 oder ASP.NET MVC 5 funktioniert die Tilde-Notation möglicherweise nicht mehr richtig, wenn Sie URL-Umschreibungen verwenden. Die URL-Umschreibung wirkt sich auf die tilde()-Notation&gt;in &lt;HTML-Elementen wie &lt;A/&gt;, &lt;SCRIPT/ , LINK/&gt;aus, und als Ergebnis wird die Tilde nicht mehr dem Stammverzeichnis zugeordnet.

Wenn Sie beispielsweise Anforderungen für **asp.net/content** in **asp.net**umschreiben, wird das href-Attribut in &lt;A href="/content/"/&gt; in **/content/content/** anstelle von **/** aufgelöst. Um diese Änderung zu unterdrücken, können Sie den **IIS\_WasUrlRewritten-Kontext** auf jeder Webseite oder in **\_Application BeginRequest** in Global.asax auf false festlegen.

<a id="templateissue"></a>
### <a name="templates"></a>Vorlagen

Wenn Sie ASP.NET MVC-Projekte mit Visual Studio 2012 unter Windows 8.1 oder Windows Server 2012 R2 erstellen, zeigt Visual Studio eine Fehlermeldung an, die besagt, dass "Konfigurieren von Web [URL] für ASP.NET 4.5 fehlgeschlagen ist".

![Konfigurationsfehler](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Dieser Fehler wird angezeigt, da Visual Studio 2012 die ASP.NET 4.5-Funktion nicht aktiviert, wenn sie auf diesen Windows-Versionen installiert ist. Führen Sie die unter [Windows-Features aktivierenden](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)Schritte aus, um ASP.NET 4.5 zu aktivieren.

![Ein- oder Ausschalten von Windows-Funktionen](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Alternativ können Sie ASP.NET 4.5 über die Befehlszeile aktivieren.

1. Öffnen Sie die Eingabeaufforderung im Administratormodus.
2. Führen Sie den folgenden Befehl aus, um ASP.NET 4.5 zu aktivieren.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
