---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: Das ASP.NET 2.0-Seiten-Modell | Microsoft Docs
author: rick-anderson
description: In ASP.NET 1.x hatten Entwickler die Wahl zwischen einem Inlinecodemodell und einem CodeBehind-Codemodell. Code-Behind könnte entweder mit dem Src attr implementiert werden...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542858"
---
# <a name="the-aspnet-20-page-model"></a>Das ASP.NET 2.0-Seiten-Modell

von [Microsoft](https://github.com/microsoft)

> In ASP.NET 1.x hatten Entwickler die Wahl zwischen einem Inlinecodemodell und einem CodeBehind-Codemodell. Code-Behind kann entweder mit dem Attribut Src oder @Page dem CodeBehind-Attribut der Direktive implementiert werden. In ASP.NET 2.0 haben Entwickler immer noch die Wahl zwischen Inlinecode und CodeBehind, aber es gab erhebliche Verbesserungen am CodeBehind-Modell.

In ASP.NET 1.x hatten Entwickler die Wahl zwischen einem Inlinecodemodell und einem CodeBehind-Codemodell. Code-Behind kann entweder mit dem Attribut Src oder @Page dem CodeBehind-Attribut der Direktive implementiert werden. In ASP.NET 2.0 haben Entwickler immer noch die Wahl zwischen Inlinecode und CodeBehind, aber es gab erhebliche Verbesserungen am CodeBehind-Modell.

## <a name="improvements-in-the-code-behind-model"></a>Verbesserungen im Code-Behind-Modell

Um die Änderungen im CodeBehind-Modell in ASP.NET 2.0 vollständig zu verstehen, ist es am besten, das Modell so schnell zu überprüfen, wie es in ASP.NET 1.x existierte.

## <a name="the-code-behind-model-in-aspnet-1x"></a>Das Code-Behind-Modell in ASP.NET 1.x

In ASP.NET 1.x bestand das CodeBehind-Modell aus einer ASPX-Datei (das Webformular) und einer CodeBehind-Datei mit Programmiercode. Die beiden Dateien wurden @Page über die Direktive in der ASPX-Datei verbunden. Jedes Steuerelement auf der ASPX-Seite hatte eine entsprechende Deklaration in der CodeBehind-Datei als Instanzvariable. Die CodeBehind-Datei enthielt auch Code für die Ereignisbindung und generierten Code, der für den Visual Studio-Designer erforderlich ist. Dieses Modell funktionierte ziemlich gut, aber da jedes ASP.NET-Element auf der ASPX-Seite entsprechenden Code in der CodeBehind-Datei benötigte, gab es keine echte Trennung von Code und Inhalt. Wenn ein Designer z. B. einer ASPX-Datei außerhalb der Visual Studio-IDE ein neues Serversteuerelement hinzugefügt hat, wird die Anwendung aufgrund des Fehlens einer Deklaration für dieses Steuerelement in der CodeBehind-Datei brechen.

## <a name="the-code-behind-model-in-aspnet-20"></a>Das Code-Behind-Modell in ASP.NET 2.0

ASP.NET 2.0 verbessert dieses Modell erheblich. In ASP.NET 2.0 wird Code-Behind mithilfe der neuen *Teilklassen* implementiert, die in ASP.NET 2.0 bereitgestellt werden. Die CodeBehind-Klasse in ASP.NET 2.0 wird als partielle Klasse definiert, d. h. sie enthält nur einen Teil der Klassendefinition. Der verbleibende Teil der Klassendefinition wird dynamisch von ASP.NET 2.0 mithilfe der ASPX-Seite zur Laufzeit oder beim Vorkompilieren der Website generiert. Die Verknüpfung zwischen der CodeBehind-Datei und der ASPX-Seite wird weiterhin mithilfe der Direktive "Seite" hergestellt. Anstelle eines CodeBehind- oder Src-Attributs verwendet ASP.NET 2.0 nun jedoch das CodeFile-Attribut. Das Attribut Vererbt wird auch verwendet, um den Klassennamen für die Seite anzugeben.

Eine typische .-Page-Direktive könnte wie folgt aussehen:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

Eine typische Klassendefinition in einer ASP.NET 2.0-CodeBehind-Datei könnte wie folgt aussehen:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> Die beiden Hauptsprachen "C" und "Visual Basic" unterstützen derzeit nur Teilklassen. Daher können Entwickler, die J-Code-Zeichen verwenden, das CodeBehind-Modell in ASP.NET 2.0 nicht verwenden.

Das neue Modell verbessert das CodeBehind-Modell, da Entwickler jetzt über Codedateien verfügen, die nur den code enthalten, den sie erstellt haben. Es sieht auch eine echte Trennung von Code und Inhalt vor, da es keine Instanzvariablendeklarationen in der CodeBehind-Datei gibt.

> [!NOTE]
> Da die partielle Klasse für die ASPX-Seite den Ort ist, an dem die Ereignisbindung stattfindet, können Visual Basic-Entwickler eine leichte Leistungssteigerung erzielen, indem sie das Handles-Schlüsselwort im CodeBehind verwenden, um Ereignisse zu binden. Das Schlüsselwort "C" hat kein entsprechendes Schlüsselwort.

## <a name="new--page-directive-attributes"></a>Neue Attributs für die Seitenrichtlinie

ASP.NET 2.0 fügt der Direktive "Seite" viele neue Attribute hinzu. Die folgenden Attribute sind in ASP.NET 2.0 neu.

## <a name="async"></a>Async

Mit dem Async-Attribut können Sie die Seite so konfigurieren, dass sie asynchron ausgeführt wird. Behandeln Sie nun asynchrone Seiten weiter unten in diesem Modul.

## <a name="asynctimeout"></a>AsyncTimeout

Das Timeout für asynchrone Seiten wurde angegeben. Der Standardwert ist 45 Sekunden.

## <a name="codefile"></a>Codefile

Das CodeFile-Attribut ist der Ersatz für das CodeBehind-Attribut in Visual Studio 2002/2003.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

Das CodeFileBaseClass-Attribut wird in Fällen verwendet, in denen mehrere Seiten von einer einzelnen Basisklasse abstammen sollen. Aufgrund der Implementierung von Partipartklassen in ASP.NET ohne dieses Attribut würde eine Basisklasse, die gemeinsame gemeinsame Felder verwendet, um auf Steuerelemente zu verweisen, die auf einer ASPX-Seite deklariert wurden, nicht ordnungsgemäß funktionieren, da das KOMPilierungsmodul ASP.NETs automatisch neue Member basierend auf Steuerelementen auf der Seite erstellt. Wenn Sie daher eine gemeinsame Basisklasse für zwei oder mehr Seiten in ASP.NET möchten, müssen Sie die Basisklasse im CodeFileBaseClass-Attribut definieren und dann jede Seitenklasse von dieser Basisklasse ableiten. Das CodeFile-Attribut ist auch erforderlich, wenn dieses Attribut verwendet wird.

## <a name="compilationmode"></a>Compilationmode

Mit diesem Attribut können Sie die CompilationMode-Eigenschaft der ASPX-Seite festlegen. Die CompilationMode-Eigenschaft ist eine Enumeration, die die Werte **Always**, **Auto**und **Never**enthält. Der Standardwert ist **Always**. Die **Auto-Einstellung** verhindert, dass ASP.NET die Seite nach Möglichkeit dynamisch kompiliert. Das Ausschließen von Seiten aus der dynamischen Kompilierung erhöht die Leistung. Wenn jedoch eine ausgeschlossene Seite den Code enthält, der kompiliert werden muss, wird beim Durchsuchen der Seite ein Fehler ausgelöst.

## <a name="enableeventvalidation"></a>EnableEventValidation

Dieses Attribut gibt an, ob Postback- und Rückrufereignisse überprüft werden. Wenn dies aktiviert ist, werden Argumente für Postback- oder Rückrufereignisse überprüft, um sicherzustellen, dass sie von dem Serversteuerelement stammen, das sie ursprünglich gerendert hat.

## <a name="enabletheming"></a>EnableTheming

Dieses Attribut gibt an, ob ASP.NET Designs auf einer Seite verwendet werden. Der Standardwert ist **false**. ASP.NET Themen werden in [Modul 10](profiles-themes-and-web-parts.md)behandelt.

## <a name="linepragmas"></a>LinePragmas

Dieses Attribut gibt an, ob Zeilenpragmas während der Kompilierung hinzugefügt werden sollen. Linienpragmas sind Optionen, die von Debuggern verwendet werden, um bestimmte Codeabschnitte zu markieren.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Dieses Attribut gibt an, ob JavaScript in die Seite eingefügt wird, um die Bildlaufposition zwischen Postbacks beizubehalten. Dieses Attribut ist standardmäßig **false.**

Wenn dieses Attribut **true**ist, &lt;&gt; fügt ASP.NET einen Skriptblock für das Postback hinzu, der wie folgt aussieht:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Beachten Sie, dass die src für diesen Skriptblock WebResource.axd ist. Diese Ressource ist kein physischer Pfad. Wenn dieses Skript angefordert wird, erstellt ASP.NET das Skript dynamisch.

### <a name="masterpagefile"></a>Masterpagefile

Dieses Attribut gibt die Masterseitendatei für die aktuelle Seite an. Der Pfad kann relativ oder absolut sein. Masterseiten werden in [Modul 4](master-pages.md)behandelt.

## <a name="stylesheettheme"></a>Stylesheettheme

Mit diesem Attribut können Sie die Erscheinungsbildeigenschaften der Benutzeroberfläche überschreiben, die durch ein ASP.NET 2.0-Design definiert sind. Die Themen werden in [Modul 10](profiles-themes-and-web-parts.md)behandelt.

## <a name="theme"></a>Design

Gibt das Design für die Seite an. Wenn für das StyleSheetTheme-Attribut kein Wert angegeben ist, überschreibt das Designattribut alle Stile, die auf Steuerelemente auf der Seite angewendet werden.

## <a name="title"></a>Titel

Legt den Titel für die Seite fest. Der hier angegebene Wert &lt;wird&gt; im Titelelement der gerenderten Seite angezeigt.

### <a name="viewstateencryptionmode"></a>Viewstateencryptionmode

Legt den Wert für die ViewStateEncryptionMode-Enumeration fest. Die verfügbaren Werte sind **Always**, **Auto**und **Never**. Der Standardwert ist **Auto**. Wenn dieses Attribut auf den Wert **Auto**festgelegt ist, ist viewstate verschlüsselt, ein Steuerelement fordert es durch Aufrufen der **RegisterRequiresViewStateEncryption-Methode** an.

## <a name="setting-public-property-values-via-the--page-directive"></a>Festlegen von Public Property Values über die Richtlinie "Seite"

Eine weitere neue Funktion der ,,Seite"-Direktive in ASP.NET 2.0 ist die Möglichkeit, den Anfangswert öffentlicher Eigenschaften einer Basisklasse festzulegen. Angenommen, Sie haben eine öffentliche Eigenschaft namens **SomeText** in Ihrer Basisklasse und möchten, dass sie beim Laden einer Seite in **Hello** initialisiert wird. Sie können dies erreichen, indem Sie einfach den Wert in der Direktive "Seite" wie folgt festlegen:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

Mit dem **SomeText-Attribut** der Direktive ,,Seite" wird der Anfangswert der SomeText-Eigenschaft in der Basisklasse auf *Hello!* festgelegt. Das folgende Video ist eine exemplarische Vorgehensweise zum Festlegen des Anfangswerts einer öffentlichen Eigenschaft in einer Basisklasse mithilfe der Direktive "Seite".

![](the-asp-net-2-0-page-model/_static/image1.png)

[Öffnen sie Ein-Bild-Video](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Neue öffentliche Eigenschaften der Seitenklasse

Die folgenden öffentlichen Eigenschaften sind in ASP.NET 2.0 neu.

## <a name="apprelativetemplatesourcedirectory"></a>Apprelativetemplatesourcedirectory

Gibt den anwendungsrelativen Pfad an die Seite oder das Steuerelement zurück. Für eine Seite, die http://app/folder/page.aspxsich z. B. unter befindet, gibt die Eigenschaft die Datei ./folder/ zurück.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

Gibt den relativen virtuellen Verzeichnispfad an die Seite oder das Steuerelement zurück. Für eine Seite, http://app/folder/page.aspxdie sich z. B. unter befindet, gibt die Eigenschaft die Datei "/folder/page.aspx" zurück.

## <a name="asynctimeout"></a>AsyncTimeout

Ruft das Timeout ab, das für die asynchrone Seitenbehandlung verwendet wird, oder legt es fest. (Asynchrone Seiten werden weiter unten in diesem Modul behandelt.)

## <a name="clientquerystring"></a>ClientQueryString

Eine schreibgeschützte Eigenschaft, die den Abfragezeichenfolgenteil der angeforderten URL zurückgibt. Dieser Wert ist URL-codiert. Sie können die UrlDecode-Methode der HttpServerUtility-Klasse verwenden, um sie zu dekodieren.

## <a name="clientscript"></a>Clientscript

Diese Eigenschaft gibt ein ClientScriptManager-Objekt zurück, das zum Verwalten der ASP.NETs-Emission von clientseitigem Skript verwendet werden kann. (Die ClientScriptManager-Klasse wird weiter unten in diesem Modul behandelt.)

## <a name="enableeventvalidation"></a>EnableEventValidation

Diese Eigenschaft steuert, ob die Ereignisüberprüfung für Postback- und Rückrufereignisse aktiviert ist. Wenn diese Option aktiviert ist, werden Argumente für Postback- oder Rückrufereignisse überprüft, um sicherzustellen, dass sie von dem Serversteuerelement stammen, das sie ursprünglich gerendert hat.

## <a name="enabletheming"></a>EnableTheming

Diese Eigenschaft ruft einen booleschen Wert ab oder legt ihn fest, der angibt, ob ein ASP.NET 2.0-Design auf die Seite angewendet wird.

## <a name="form"></a>Form

Diese Eigenschaft gibt das HTML-Formular auf der ASPX-Seite als HtmlForm-Objekt zurück.

## <a name="header"></a>Header

Diese Eigenschaft gibt einen Verweis auf ein HtmlHead-Objekt zurück, das den Seitenkopf enthält. Sie können das zurückgegebene HtmlHead-Objekt verwenden, um Stylesheets, Meta-Tags usw. abzubekommen/festzulegen.

## <a name="idseparator"></a>IdSeparator

Diese schreibgeschützte Eigenschaft ruft das Zeichen ab, das zum Trennen von Steuerelementbezeichnern verwendet wird, wenn ASP.NET eine eindeutige ID für Steuerelemente auf einer Seite erstellen. Sie sollte nicht direkt im Code verwendet werden.

## <a name="isasync"></a>IsAsync

Diese Eigenschaft ermöglicht asynchrone Seiten. Asynchrone Seiten werden weiter unten in dieser Unterrichtseinheit erläutert.

## <a name="iscallback"></a>IsCallback

Diese schreibgeschützte Eigenschaft gibt **true** zurück, wenn die Seite das Ergebnis eines Rückrufs ist. Rückrufe werden weiter unten in dieser Unterrichtseinheit erläutert.

## <a name="iscrosspagepostback"></a>Iscrosspagepostback

Diese schreibgeschützte Eigenschaft gibt **true** zurück, wenn die Seite Teil eines seitenübergreifenden Postbacks ist. Seitenseitige Postbacks werden weiter unten in diesem Modul behandelt.

## <a name="items"></a>Items

Gibt einen Verweis auf eine IDictionary-Instanz zurück, die alle im Seitenkontext gespeicherten Objekte enthält. Sie können diesem IDictionary-Objekt Elemente hinzufügen, die Ihnen während der gesamten Lebensdauer des Kontexts zur Verfügung stehen.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Diese Eigenschaft steuert, ob ASP.NET JavaScript ausgibt, das die Bildlaufposition der Seiten im Browser nach einem Postback verwaltet. (Details zu dieser Eigenschaft wurden weiter oben in dieser Unterrichtseinheit erläutert.)

## <a name="master"></a>Master

Diese schreibgeschützte Eigenschaft gibt einen Verweis auf die MasterPage-Instanz für eine Seite zurück, auf die eine Masterseite angewendet wurde.

## <a name="masterpagefile"></a>Masterpagefile

Ruft den Masterseitendateinamen für die Seite ab oder legt sie fest. Diese Eigenschaft kann nur in der PreInit-Methode festgelegt werden.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

Diese Eigenschaft ruft oder legt die maximale Länge für den Seitenstatus in Bytes fest. Wenn die Eigenschaft auf eine positive Zahl festgelegt ist, wird der Seitenansichtsstatus in mehrere ausgeblendete Felder aufgeteilt, sodass die angegebene Anzahl von Bytes nicht überschritten wird. Wenn es sich bei der Eigenschaft um eine negative Zahl handelt, wird der Ansichtszustand nicht in Blöcke unterteilt.

## <a name="pageadapter"></a>Pageadapter

Gibt einen Verweis auf das PageAdapter-Objekt zurück, das die Seite für den anfordernden Browser ändert.

## <a name="previouspage"></a>Previouspage

Gibt einen Verweis auf die vorherige Seite zurück, wenn ein Server.Transfer oder ein seitenübergreifendes Postback auftritt.

## <a name="skinid"></a>Skinid

Gibt die ASP.NET 2.0-Skin an, die auf die Seite angewendet werden soll.

## <a name="stylesheettheme"></a>Stylesheettheme

Diese Eigenschaft ruft das Stylesheet ab oder legt es fest, das auf eine Seite angewendet wird.

## <a name="templatecontrol"></a>TemplateControl

Gibt einen Verweis auf das enthaltende Steuerelement für die Seite zurück.

## <a name="theme"></a>Design

Ruft den Namen des ASP.NET 2.0-Design ab, das auf die Seite angewendet wird, oder legt ihn fest. Dieser Wert muss vor der PreInit-Methode festgelegt werden.

## <a name="title"></a>Titel

Diese Eigenschaft ruft den Titel für die Seite ab oder legt diesen fest, wie aus dem Seitenkopf abgerufen.

## <a name="viewstateencryptionmode"></a>Viewstateencryptionmode

Ruft den ViewStateEncryptionMode der Seite ab oder legt er fest. Eine ausführliche Beschreibung dieser Eigenschaft finden Sie weiter oben in dieser Unterrichtseinheit.

## <a name="new-protected-properties-of-the-page-class"></a>Neue geschützte Eigenschaften der Seitenklasse

Im Folgenden sind die neuen geschützten Eigenschaften der Page-Klasse in ASP.NET 2.0.

## <a name="adapter"></a>Adapter

Gibt einen Verweis auf den ControlAdapter zurück, der die Seite auf dem Gerät rendert, das ihn angefordert hat.

## <a name="asyncmode"></a>AsyncMode

Diese Eigenschaft gibt an, ob die Seite asynchron verarbeitet wird. Es ist für die Verwendung durch die Laufzeit und nicht direkt im Code vorgesehen.

## <a name="clientidseparator"></a>ClientIDSeparator

Diese Eigenschaft gibt das Zeichen zurück, das beim Erstellen eindeutiger Client-IDs für Steuerelemente als Trennzeichen verwendet wird. Es ist für die Verwendung durch die Laufzeit und nicht direkt im Code vorgesehen.

## <a name="pagestatepersister"></a>Pagestatepersister

Diese Eigenschaft gibt das PageStatePersister-Objekt für die Seite zurück. Diese Eigenschaft wird hauptsächlich von ASP.NET Steuerelemententwicklern verwendet.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

Diese Eigenschaft gibt ein eindeutiges Suffix zurück, das an den Dateipfad für das Zwischenspeichern von Browsern angehängt wird. Der Standardwert \_ \_ist ufps= und eine 6-stellige Zahl.

## <a name="new-public-methods-for-the-page-class"></a>Neue öffentliche Methoden für die Seitenklasse

Die folgenden öffentlichen Methoden sind neu für die Page-Klasse in ASP.NET 2.0.

## <a name="addonprerendercompleteasync"></a>Addonprerendercompleteasync

Diese Methode registriert Ereignishandlerdelegaten für die asynchrone Seitenausführung. Asynchrone Seiten werden weiter unten in dieser Unterrichtseinheit erläutert.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

Wendet die Eigenschaften in einem Seitenstylesheet auf die Seite an.

## <a name="executeregisteredasynctasks"></a>Executeregisteredasynctasks

Diese Methode ist eine asynchrone Aufgabe.

### <a name="getvalidators"></a>GetValidators

Gibt eine Auflistung von Validatoren für die angegebene Validierungsgruppe oder die Standardvalidierungsgruppe zurück, wenn keine angegeben ist.

## <a name="registerasynctask"></a>Registerasynctask

Diese Methode registriert eine neue async-Aufgabe. Asynchrone Seiten werden weiter unten in diesem Modul behandelt.

## <a name="registerrequirescontrolstate"></a>Registerrequirescontrolstate

Diese Methode teilt ASP.NET mit, dass der Seitensteuerungsstatus beibehalten werden muss.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

Diese Methode teilt ASP.NET mit, dass der Seitenansichtsstatus verschlüsselt werden muss.

## <a name="resolveclienturl"></a>ResolveClientUrl

Gibt eine relative URL zurück, die für Clientanforderungen für Bilder usw. verwendet werden kann.

## <a name="setfocus"></a>SetFocus

Diese Methode setzt den Fokus auf das Steuerelement, das beim ersten Laden der Seite angegeben wird.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

Diese Methode wird die Registrierung des Anscheins, dass es keine Kontrollstatuspersistenz mehr erfordert, aufheben.

## <a name="changes-to-the-page-lifecycle"></a>Änderungen am Seitenlebenszyklus

Der Seitenlebenszyklus in ASP.NET 2.0 hat sich nicht dramatisch geändert, aber es gibt einige neue Methoden, die Sie beachten sollten. Der ASP.NET 2.0-Seiten-Lebenszyklus wird unten beschrieben.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (Neu in ASP.NET 2.0)

Das PreInit-Ereignis ist die früheste Phase des Lebenszyklus, auf die ein Entwickler zugreifen kann. Durch das Hinzufügen dieses Ereignisses ist es möglich, ASP.NET 2.0-Themen, Masterseiten, Zugriffseigenschaften für ein ASP.NET 2.0-Profil usw. programmgesteuert zu ändern. Wenn Sie sich in einem Postback-Status befinden, ist es wichtig zu erkennen, dass Viewstate zu diesem Zeitpunkt des Lebenszyklus noch nicht auf Steuerelemente angewendet wurde. Wenn ein Entwickler daher in dieser Phase eine Eigenschaft eines Steuerelements ändert, wird es wahrscheinlich später im Seitenlebenszyklus überschrieben.

## <a name="init"></a>Init

Das Init-Ereignis hat sich von ASP.NET 1.x nicht geändert. Hier möchten Sie die Eigenschaften von Steuerelementen auf der Seite lesen oder initialisieren. In dieser Phase werden Masterseiten, Themen usw. bereits auf die Seite angewendet.

## <a name="initcomplete-new-in-20"></a>InitComplete (Neu in 2.0)

Das InitComplete-Ereignis wird am Ende der Seiteninitialisierungsphase aufgerufen. An diesem Punkt des Lebenszyklus können Sie auf Steuerelemente auf der Seite zugreifen, deren Status jedoch noch nicht aufgefüllt wurde.

## <a name="preload-new-in-20"></a>PreLoad (Neu in 2.0)

Dieses Ereignis wird aufgerufen, nachdem alle Postback-Daten\_angewendet wurden und kurz vor Page Load.

## <a name="load"></a>Laden

Das Load-Ereignis wurde von ASP.NET 1.x nicht geändert.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (Neu in 2.0)

Das LoadComplete-Ereignis ist das letzte Ereignis in der Ladephase der Seiten. In dieser Phase wurden alle Postback- und Ansichtszustandsdaten auf die Seite angewendet.

## <a name="prerender"></a>Prerender

Wenn Viewstate für Steuerelemente, die der Seite dynamisch hinzugefügt werden, ordnungsgemäß verwaltet werden soll, ist das PreRender-Ereignis die letzte Möglichkeit, sie hinzuzufügen.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (neu in 2.0)

In der PreRenderComplete-Phase wurden der Seite alle Steuerelemente hinzugefügt, und die Seite kann gerendert werden. Das PreRenderComplete-Ereignis ist das letzte Ereignis, das ausgelöst wurde, bevor der Seitenansichtszustand gespeichert wird.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (neu in 2.0)

Das SaveStateComplete-Ereignis wird sofort aufgerufen, nachdem der gesamte Seitenansichtsstatus und der Steuerelementstatus gespeichert wurde. Dies ist das letzte Ereignis, bevor die Seite tatsächlich im Browser gerendert wird.

## <a name="render"></a>Rendern

Die Render-Methode hat sich seit ASP.NET 1.x nicht geändert. Hier wird der HtmlTextWriter initialisiert und die Seite im Browser gerendert.

## <a name="cross-page-postback-in-aspnet-20"></a>Cross-Page Postback in ASP.NET 2.0

In ASP.NET 1.x mussten Postbacks auf derselben Seite posten. Seitenübergreifende Postbacks waren nicht zulässig. ASP.NET 2.0 bietet die Möglichkeit, über die IButtonControl-Schnittstelle auf einer anderen Seite zu posten. Jedes Steuerelement, das die neue IButtonControl-Schnittstelle implementiert (Button, LinkButton und ImageButton zusätzlich zu benutzerdefinierten Steuerelementen von Drittanbietern), kann diese neue Funktionalität über die Verwendung des PostBackUrl-Attributs nutzen. Der folgende Code zeigt ein Schaltflächensteuerelement, das auf eine zweite Seite zurücksendet.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Wenn die Seite zurückgesendet wird, ist auf die Seite, die das Postback initiiert, über die PreviousPage-Eigenschaft auf der zweiten Seite zugegriffen. Diese Funktionalität wird über die\_neue WebForm DoPostBackWithOptions-Client-Seite implementiert, die ASP.NET 2.0 auf die Seite rendert, wenn ein Steuerelement auf eine andere Seite zurückgesendet wird. Diese JavaScript-Funktion wird vom neuen WebResource.axd-Handler bereitgestellt, der Skripts an den Client ausgibt.

Das folgende Video ist eine exemplarische Vorgehensweise eines seitenübergreifenden Postbacks.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Öffnen sie Ein-Bild-Video](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Weitere Details zu Cross-Page Postbacks

### <a name="viewstate"></a>Viewstate

Möglicherweise haben Sie sich bereits von der ersten Seite in einem seitenübergreifenden Postbackszenario gefragt, was mit dem Ansichtszustand geschieht. Schließlich behält jedes Steuerelement, das IPostBackDataHandler nicht implementiert, seinen Status über den Ansichtszustand, sodass Sie Zugriff auf die Eigenschaften dieses Steuerelements auf der zweiten Seite eines seitenübergreifenden Postbacks haben müssen, um Zugriff auf den Ansichtszustand für die Seite zu haben. ASP.NET 2.0 kümmert sich um dieses Szenario mit einem \_ \_neuen ausgeblendeten Feld auf der zweiten Seite namens PREVIOUSPAGE. Das \_ \_Formularfeld PREVIOUSPAGE enthält den Ansichtszustand für die erste Seite, sodass Sie auf die Eigenschaften aller Steuerelemente auf der zweiten Seite zugreifen können.

### <a name="circumventing-findcontrol"></a>Umgehung von FindControl

In der Video-Exemplar-Through-Anleitung eines cross-page-Postbacks habe ich die FindControl-Methode verwendet, um einen Verweis auf das TextBox-Steuerelement auf der ersten Seite abzuverweisen. Diese Methode funktioniert gut für diesen Zweck, aber FindControl ist teuer und erfordert das Schreiben von zusätzlichem Code. Glücklicherweise bietet ASP.NET 2.0 eine Alternative zu FindControl für diesen Zweck, die in vielen Szenarien funktioniert. Mit der PreviousPageType-Direktive können Sie einen stark typisierten Verweis auf die vorherige Seite verwenden, indem Sie entweder den TypeName oder das VirtualPath-Attribut verwenden. Mit dem TypeName-Attribut können Sie den Typ der vorherigen Seite angeben, während Sie mit dem VirtualPath-Attribut mithilfe eines virtuellen Pfads auf die vorherige Seite verweisen können. Nachdem Sie die PreviousPageType-Direktive festgelegt haben, müssen Sie die Steuerelemente usw. verfügbar machen, für die Sie den Zugriff mithilfe öffentlicher Eigenschaften zulassen möchten.

## <a name="lab-1-cross-page-postback"></a>Lab 1 Cross-Page Postback

In dieser Übungseinheit erstellen Sie eine Anwendung, die die neue seitenübergreifende Postbackfunktionalität von ASP.NET 2.0 verwendet.

1. Öffnen Sie Visual Studio 2005, und erstellen Sie eine neue ASP.NET Website.
2. Fügen Sie ein neues Webformular mit dem Namen page2.aspx hinzu.
3. Öffnen Sie die Default.aspx in der Entwurfsansicht, und fügen Sie ein Schaltflächensteuerelement und ein TextBox-Steuerelement hinzu. 

    1. Geben Sie dem Schaltflächensteuerelement eine ID von **SubmitButton** und dem TextBox-Steuerelement eine ID von **UserName**.
    2. Legen Sie die PostBackUrl-Eigenschaft der Schaltfläche auf page2.aspx fest.
4. Öffnen Sie page2.aspx in der Quellansicht.
5. Fügen Sie eine Direktive mit dem Wert "PreviousPageType" hinzu, wie unten gezeigt:
6. Fügen Sie dem Page\_Load des CodeBehind von page2.aspx den folgenden Code hinzu: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Erstellen Sie das Projekt, indem Sie im Menü Erstellen auf Erstellen klicken.
8. Fügen Sie dem CodeBehind für Default.aspx den folgenden Code hinzu: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Ändern Sie\_das Seitenladen in page2.aspx in Folgendes: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Erstellen Sie das Projekt.
11. Führen Sie das Projekt aus.
12. Geben Sie Ihren Namen in die TextBox ein und klicken Sie auf die Schaltfläche.
13. Was ist das Ergebnis?

## <a name="asynchronous-pages-in-aspnet-20"></a>Asynchrone Seiten in ASP.NET 2.0

Viele Konfliktprobleme in ASP.NET werden durch die Latenz externer Aufrufe (z. B. Webdienst- oder Datenbankaufrufe), der Datei-E/A-Latenz usw. verursacht. Wenn eine Anforderung für eine ASP.NET Anwendung gestellt wird, verwendet ASP.NET einen ihrer Arbeitsthreads, um diese Anforderung zu bearbeiten. Diese Anforderung ist Eigentümer dieses Threads, bis die Anforderung abgeschlossen ist und die Antwort gesendet wurde. ASP.NET 2.0 versucht, Latenzprobleme mit diesen Arten von Problemen zu beheben, indem die Möglichkeit hinzugefügt wird, Seiten asynchron auszuführen. Das bedeutet, dass ein Arbeitsthread die Anforderung starten und dann eine zusätzliche Ausführung an einen anderen Thread übergeben kann, wodurch schnell zum verfügbaren Threadpool zurückkehrt. Wenn die Datei-E/A, der Datenbankaufruf usw. abgeschlossen sind, wird ein neuer Thread aus dem Threadpool abgerufen, um die Anforderung abzuschließen.

Der erste Schritt, um eine Seite asynchron auszuführen, besteht darin, das **Async-Attribut** der Seitendirektive wie folgt festzulegen:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Dieses Attribut weist ASP.NET an, den IHttpAsyncHandler für die Seite zu implementieren.

Der nächste Schritt besteht darin, die AddOnPreRenderCompleteAsync-Methode an einem Punkt im Lebenszyklus der Seite vor PreRender aufzurufen. (Diese Methode wird in\_der Regel in Page Load aufgerufen.) Die AddOnPreRenderCompleteAsync-Methode verwendet zwei Parameter. einen BeginEventHandler und einen EndEventHandler. Der BeginEventHandler gibt ein IAsyncResult zurück, das dann als Parameter an den EndEventHandler übergeben wird.

Das folgende Video ist eine exemplarische Vorgehensweise einer asynchronen Seitenanforderung.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Öffnen sie Ein-Bild-Video](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Eine async-Seite wird erst im Browser gerendert, wenn der EndEventHandler abgeschlossen ist. Kein Zweifel, aber dass einige Entwickler asynchrone Anforderungen als ähnlich wie async-Rückrufe betrachten werden. Es ist wichtig zu erkennen, dass sie es nicht sind. Der Vorteil asynchroner Anforderungen besteht darin, dass der erste Arbeitsthread an den Threadpool zurückgegeben werden kann, um neue Anforderungen zu verarbeiten, wodurch Konflikte aufgrund von E/A-Gebunden usw. verringert werden.

## <a name="script-callbacks-in-aspnet-20"></a>Skriptrückrufe in ASP.NET 2.0

Webentwickler haben immer nach Möglichkeiten gesucht, das Flimmern zu verhindern, das mit einem Rückruf verbunden ist. In ASP.NET 1.x war SmartNavigation die häufigste Methode, um Flimmern zu vermeiden, aber SmartNavigation verursachte Probleme für einige Entwickler aufgrund der Komplexität seiner Implementierung auf dem Client. ASP.NET 2.0 behebt dieses Problem mit Skriptrückrufen. Skriptrückrufe verwenden XMLHttp, um Anforderungen über JavaScript an den Webserver zu stellen. Die XMLHttp-Anforderung gibt XML-Daten zurück, die dann über das DOM des Browsers bearbeitet werden können. XMLHttp-Code wird vom benutzerneuen WebResource.axd-Handler ausgeblendet.

Es gibt mehrere Schritte, die erforderlich sind, um einen Skriptrückruf in ASP.NET 2.0 zu konfigurieren.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>Schritt 1 : Implementieren der ICallbackEventHandler-Schnittstelle

Damit ASP.NET Ihre Seite als Teilnahme an einem Skriptrückruf erkennen können, müssen Sie die ICallbackEventHandler-Schnittstelle implementieren. Sie können dies in Ihrer Code-Behind-Datei wie folgt tun:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Sie können dies auch mit der Direktive "Implements" wie folgt tun:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

In der Regel verwenden Sie die Direktive " Implements", wenn Sie Inline-ASP.NET-Code verwenden.

## <a name="step-2--call-getcallbackeventreference"></a>Schritt 2 : Rufen Sie GetCallbackEventReference auf

Wie bereits erwähnt, wird der XMLHttp-Aufruf im WebResource.axd-Handler gekapselt. Wenn Ihre Seite gerendert wird, wird\_ASP.NET einen Aufruf von WebForm DoCallback hinzufügen, einem Clientskript, das von WebResource.axd bereitgestellt wird. Die WebForm\_DoCallback-Funktion \_ \_ersetzt die doPostBack-Funktion für einen Rückruf. Denken \_ \_Sie daran, dass doPostBack das Formular auf der Seite programmgesteuert absendet. In einem Rückrufszenario möchten Sie ein Postback \_ \_verhindern, sodass doPostBack nicht ausreicht.

> [!NOTE]
> \_\_doPostBack wird weiterhin in einem Clientskriptrückrufszenario auf der Seite gerendert. Es wird jedoch nicht für den Rückruf verwendet.

Die Argumente für\_die clientseitige WebForm DoCallback-Funktion werden über die serverseitige Funktion GetCallbackEventReference bereitgestellt, die normalerweise in Page\_Load aufgerufen wird. Ein typischer Aufruf von GetCallbackEventReference könnte wie folgt aussehen:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> In diesem Fall ist cm eine Instanz von ClientScriptManager. Die ClientScriptManager-Klasse wird später in diesem Modul behandelt.

Es gibt mehrere überladene Versionen von GetCallbackEventReference. In diesem Fall sind die Argumente wie folgt:

`this`

Ein Verweis auf das Steuerelement, in dem GetCallbackEventReference aufgerufen wird. In diesem Fall ist es die Seite selbst.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

Ein Zeichenfolgenargument, das vom clientseitigen Code an das serverseitige Ereignis übergeben wird. In diesem Fall übergibt Im den Wert einer Dropdown-Liste namens ddlCompany.

`ShowCompanyName`

Der Name der clientseitigen Funktion, die den Rückgabewert (als Zeichenfolge) vom serverseitigen Rückrufereignis akzeptiert. Diese Funktion wird nur aufgerufen, wenn der serverseitige Rückruf erfolgreich ist. Aus Gründen der Robustheit wird daher im Allgemeinen empfohlen, die überladene Version von GetCallbackEventReference zu verwenden, die ein zusätzliches Zeichenfolgenargument verwendet, das den Namen einer clientseitigen Funktion angibt, die im Fehlerfall ausgeführt werden soll.

`null`

Eine Zeichenfolge, die eine clientseitige Funktion darstellt, die sie vor dem Rückruf an den Server initiiert hat. In diesem Fall gibt es kein solches Skript, daher ist das Argument null.

`true`

Ein boolescher Wert, der angibt, ob der Rückruf asynchron durchgeführt werden soll.

Der Aufruf von\_WebForm DoCallback auf dem Client übergibt diese Argumente. Wenn diese Seite auf dem Client gerendert wird, sieht dieser Code daher wie folgt aus:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

Beachten Sie, dass die Signatur der Funktion auf dem Client etwas anders ist. Die clientseitige Funktion übergibt 5 Zeichenfolgen und eine boolesche. Die zusätzliche Zeichenfolge (die im obigen Beispiel null ist) enthält die clientseitige Funktion, die alle Fehler aus dem serverseitigen Rückruf verarbeitet.

## <a name="step-3--hook-the-client-side-control-event"></a>Schritt 3 : Haken des clientseitigen Steuerungsereignisses

Beachten Sie, dass der Rückgabewert von GetCallbackEventReference oben einer Zeichenfolgenvariablen zugewiesen wurde. Diese Zeichenfolge wird verwendet, um ein clientseitiges Ereignis für das Steuerelement zu hooken, das den Rückruf initiiert. In diesem Beispiel wird der Rückruf durch eine Dropdown-Liste auf der Seite initiiert, daher möchte ich das *OnChange-Ereignis* einbinden.

Um das clientseitige Ereignis zu hooken, fügen Sie dem clientseitigen Markup einfach wie folgt einen Handler hinzu:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

Beachten Sie, dass *cbRef* der Rückgabewert aus dem Aufruf von GetCallbackEventReference ist. Sie enthält den oben\_gezeigten Aufruf von WebForm DoCallback.

## <a name="step-4--register-the-client-side-script"></a>Schritt 4 : Registrieren des Client-Side-Skripts

Erinnern Sie sich daran, dass der Aufruf von GetCallbackEventReference angegeben hat, dass ein clientseitiges Skript namens **ShowCompanyName** ausgeführt wird, wenn der serverseitige Rückruf erfolgreich ist. Dieses Skript muss der Seite mithilfe einer ClientScriptManager-Instanz hinzugefügt werden. (Die ClientScriptManager-Klasse wird weiter unten in diesem Modul erläutert.) Sie tun das so:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>Schritt 5 : Aufrufen der Methoden der ICallbackEventHandler-Schnittstelle

Der ICallbackEventHandler enthält zwei Methoden, die Sie in Ihrem Code implementieren müssen. Sie sind **RaiseCallbackEvent** und **GetCallbackEvent**.

**RaiseCallbackEvent** nimmt eine Zeichenfolge als Argument und gibt nichts zurück. Das Zeichenfolgenargument wird vom clientseitigen Aufruf\_an WebForm DoCallback übergeben. In diesem Fall ist dieser Wert das *Wertattribut* der Dropdownliste namens ddlCompany. Ihr serverseitiger Code sollte in der RaiseCallbackEvent-Methode platziert werden. Wenn Ihr Rückruf z. B. eine WebRequest für eine externe Ressource ausführt, sollte dieser Code in RaiseCallbackEvent platziert werden.

**GetCallbackEvent** ist für die Verarbeitung der Rückgabe des Rückrufs an den Client verantwortlich. Es braucht keine Argumente und gibt eine Zeichenfolge zurück. Die zurückgegebene Zeichenfolge wird als Argument an die clientseitige Funktion übergeben, in diesem Fall *ShowCompanyName*.

Nachdem Sie die oben genannten Schritte abgeschlossen haben, können Sie einen Skriptrückruf in ASP.NET 2.0 durchführen.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Öffnen sie Ein-Bild-Video](the-asp-net-2-0-page-model/_static/callback1.wmv)

Skriptrückrufe in ASP.NET werden in jedem Browser unterstützt, der XMLHttp-Aufrufe unterstützt. Dazu gehören alle modernen Browser, die heute im Einsatz sind. Internet Explorer verwendet das XMLHttp ActiveX-Objekt, während andere moderne Browser (einschließlich des kommenden IE 7) ein systeminternes XMLHttp-Objekt verwenden. Um programmgesteuert zu bestimmen, ob ein Browser Rückrufe unterstützt, können Sie die **Request.Browser.SupportCallback-Eigenschaft** verwenden. Diese Eigenschaft gibt **true** zurück, wenn der anfordernde Client Skriptrückrufe unterstützt.

## <a name="working-with-client-script-in-aspnet-20"></a>Arbeiten mit ClientScript in ASP.NET 2.0

Clientskripts in ASP.NET 2.0 werden über die ClientScriptManager-Klasse verwaltet. Die ClientScriptManager-Klasse verfolgt Clientskripts mithilfe eines Typs und eines Namens. Dadurch wird verhindert, dass dasselbe Skript mehr als einmal programmgesteuert auf einer Seite eingefügt wird.

> [!NOTE]
> Nachdem ein Skript erfolgreich auf einer Seite registriert wurde, führt jeder nachfolgende Versuch, dasselbe Skript zu registrieren, einfach dazu, dass das Skript nicht ein zweites Mal registriert wird. Es werden keine doppelten Skripts hinzugefügt, und es tritt keine Ausnahme ein. Um unnötige Berechnungen zu vermeiden, können Sie mithilfe von Methoden ermitteln, ob ein Skript bereits registriert ist, damit Sie nicht mehr als einmal versuchen, es zu registrieren.

Die Methoden des ClientScriptManagers sollten allen aktuellen ASP.NET Entwicklern vertraut sein:

## <a name="registerclientscriptblock"></a>Registerclientscriptblock

Diese Methode fügt oben auf der gerenderten Seite ein Skript hinzu. Dies ist nützlich, um Funktionen hinzuzufügen, die explizit auf dem Client aufgerufen werden.

Es gibt zwei überladene Versionen dieser Methode. Drei von vier Argumenten sind unter ihnen üblich. Sie lauten wie folgt:

`type (string)`

Das ***Typargument*** identifiziert einen Typ für das Skript. Im Allgemeinen ist es eine gute Idee, den Seitentyp zu verwenden (dies. GetType()) für den Typ.

`key (string)`

Das ***Schlüsselargument*** ist ein benutzerdefinierter Schlüssel für das Skript. Dies sollte für jedes Skript eindeutig sein. Wenn Sie versuchen, ein Skript mit demselben Schlüssel und Typ eines bereits hinzugefügten Skripts hinzuzufügen, wird es nicht hinzugefügt.

`script (string)`

Das ***Skriptargument*** ist eine Zeichenfolge, die das eigentliche skript zu fügende Skript enthält. Es wird empfohlen, einen StringBuilder zum Erstellen des Skripts und dann die ToString()-Methode im StringBuilder zum Zuweisen des ***Skriptarguments*** zu verwenden.

Wenn Sie den überladenen RegisterClientScriptBlock verwenden, der nur&lt;drei&gt; &lt;Argumente&gt;verwendet, müssen Sie Skriptelemente ( Skript und /script ) in Ihr Skript aufnehmen.

Sie können die Überladung von RegisterClientScriptBlock verwenden, die ein viertes Argument verwendet. Das vierte Argument ist ein boolesche Argument, das angibt, ob ASP.NET Skriptelemente für Sie hinzufügen soll. Wenn dieses Argument **wahr**ist, sollte das Skript die Skriptelemente nicht explizit enthalten.

Verwenden Sie die IsClientScriptBlockRegistered-Methode, um zu ermitteln, ob ein Skript bereits registriert wurde. Auf diese Weise können Sie den Versuch vermeiden, ein bereits registriertes Skript erneut zu registrieren.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (neu in 2.0)

Das RegisterClientScriptInclude-Tag erstellt einen Skriptblock, der mit einer externen Skriptdatei verknüpft ist. Es hat zwei Überlastungen. Man nimmt einen Schlüssel und eine URL. Das zweite Fügt ein drittes Argument hinzu, das den Typ angibt.

Der folgende Code generiert beispielsweise einen Skriptblock, der im Stammverzeichnis des Skriptordners der Anwendung mit jsfunctions.js verknüpft ist:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Dieser Code erzeugt den folgenden Code auf der gerenderten Seite:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> Der Skriptblock wird am unteren Rand der Seite gerendert.

Verwenden Sie die IsClientScriptIncludeRegistered-Methode, um zu ermitteln, ob ein Skript bereits registriert wurde. Auf diese Weise können Sie einen Versuch vermeiden, ein Skript erneut zu registrieren.

## <a name="registerstartupscript"></a>Registerstartupscript

Die RegisterStartupScript-Methode verwendet dieselben Argumente wie die RegisterClientScriptBlock-Methode. Ein bei RegisterStartupScript registriertes Skript wird nach dem Laden der Seite, aber vor dem Client-side-Ereignis OnLoad ausgeführt. In 1.X wurden Skripte, die bei RegisterStartupScript registriert sind, kurz vor dem schließenden &lt;/form-Tag&gt; platziert, während Skripte, die bei RegisterClientScriptBlock registriert sind, unmittelbar nach dem öffnenden &lt;Formulartag&gt; platziert wurden. In ASP.NET 2.0 werden beide unmittelbar &lt;vor&gt; dem schließenden /form-Tag platziert.

> [!NOTE]
> Wenn Sie eine Funktion bei RegisterStartupScript registrieren, wird diese Funktion erst ausgeführt, wenn Sie sie explizit im clientseitigen Code aufrufen.

Verwenden Sie die IsStartupScriptRegistered-Methode, um zu ermitteln, ob ein Skript bereits registriert wurde, und um einen Versuch zu vermeiden, ein Skript erneut zu registrieren.

## <a name="other-clientscriptmanager-methods"></a>Andere ClientScriptManager-Methoden

Hier sind einige der anderen nützlichen Methoden der ClientScriptManager-Klasse.

|  <strong>Getcallbackeventreference</strong>   |                                                 Siehe Skriptrückrufe weiter oben in diesem Modul.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                Ruft einen JavaScript-Verweis&lt;(javascript: call&gt;) ab, der zum Zurückgeben von einem clientseitigen Ereignis verwendet werden kann.                 |
|  <strong>Getpostbackeventreference</strong>   |                                   Ruft eine Zeichenfolge ab, die verwendet werden kann, um einen Beitrag zurück vom Client zu initiieren.                                    |
|      <strong>GetWebResourceUrl</strong>       | Gibt eine URL an eine Ressource zurück, die in eine Assembly eingebettet ist. Muss in Verbindung mit <strong>RegisterClientScriptResource</strong>verwendet werden. |
| <strong>Registerclientscriptresource</strong> |     Registriert eine Webressource auf der Seite. Dies sind Ressourcen, die in eine Assembly eingebettet und vom neuen WebResource.axd-Handler verarbeitet werden.      |
|     <strong>Registerhiddenfield</strong>      |                                                 Registriert ein ausgeblendetes Formularfeld bei der Seite.                                                 |
|  <strong>Registeronsubmitstatement</strong>   |                                  Registriert clientseitigen Code, der ausgeführt wird, wenn das HTML-Formular gesendet wird.                                   |
