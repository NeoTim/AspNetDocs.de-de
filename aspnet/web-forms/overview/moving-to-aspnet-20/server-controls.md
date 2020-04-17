---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Serversteuerelemente | Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0 verbessert die Serversteuerung in vielerlei Hinsicht. In dieser Unterrichtseinheit behandeln wir einige der architektonischen Änderungen an der Art und Weise, wie ASP.NET 2.0 und Visual Studio 200...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543742"
---
# <a name="server-controls"></a>Serversteuerelemente

von [Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 verbessert die Serversteuerung in vielerlei Hinsicht. In dieser Unterrichtseinheit werden einige der Architekturänderungen in Bezug auf die Art und Weise behandelt, wie ASP.NET 2.0 und Visual Studio 2005 mit Serversteuerelementen behandelt wird.

ASP.NET 2.0 verbessert die Serversteuerung in vielerlei Hinsicht. In dieser Unterrichtseinheit werden einige der Architekturänderungen in Bezug auf die Art und Weise behandelt, wie ASP.NET 2.0 und Visual Studio 2005 mit Serversteuerelementen behandelt wird.

## <a name="view-state"></a>Status anzeigen

Die primäre Änderung des Ansichtszustands in ASP.NET 2.0 ist eine dramatische Verkleinerung der Größe. Betrachten Sie eine Seite mit nur einem Kalendersteuerelement. Hier ist der Ansichtszustand in ASP.NET 1.1.

[!code-css[Main](server-controls/samples/sample1.css)]

Hier ist der Ansichtszustand auf einer identischen Seite in ASP.NET 2.0.

[!code-css[Main](server-controls/samples/sample2.css)]

Das ist eine ziemlich signifikante Änderung, und wenn man bedenkt, dass der Ansichtszustand über den Draht hin und her getragen wird, kann diese Änderung Entwicklern eine signifikante Leistungssteigerung bewirken. Die Verkleinerung des Ansichtszustands ist weitgehend auf die Art und Weise zurückzuführen, wie wir intern damit umgehen. Denken Sie daran, dass der Ansichtszustand eine Base64-codierte Zeichenfolge ist. Um die Änderung des Ansichtszustands in ASP.NET 2.0 besser zu verstehen, werfen wir einen Blick auf die decodierten Werte aus den obigen Beispielen.

Hier ist der 1.1 Ansichtszustand dekodiert:

[!code-css[Main](server-controls/samples/sample3.css)]

Dies mag ein bisschen wie Kauderwelsch aussehen, aber es gibt hier ein Muster. In ASP.NET 1.x haben wir einzelne Zeichen verwendet, um &lt; &gt; Datentypen und durchTrennwerte mit den Zeichen zu identifizieren. Das "t" im Ansichtszustandsbeispiel oben stellt ein Triplet dar. Das Triplet enthält ein Paar ArrayLists (das "l" stellt eine ArrayList dar).) Eine dieser ArrayLists enthält ein Int32 ("i") mit dem Wert 1 und das andere enthält ein weiteres Triplet. Das Triplet enthält ein Paar ArrayLists usw. Wichtig ist, dass wir Triplets verwenden, die Paare enthalten, wir identifizieren die Datentypen über einen Buchstaben, und wir verwenden die &lt; und &gt; Zeichen als Trennzeichen.

In ASP.NET 2.0 sieht der decodierte Ansichtszustand etwas anders aus.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Sie sollten eine große Änderung in der Darstellung des decodierten Ansichtszustands bemerken. Diese Änderung hat mehrere architektonische Grundlagen. Der Anzeigezustand in ASP.NET 1.x verwendet die LosFormatter verwendet, um Daten zu serialisieren. In 2.0 verwenden wir die neue ObjectStateFormatter-Klasse. Diese Klasse wurde speziell entwickelt, um die Serialisierung und Deserialisierung des Ansichts- und Kontrollstatus zu unterstützen. (Der Kontrollstatus wird im nächsten Abschnitt behandelt.) Es gibt viele Vorteile durch die Änderung der Methode, mit der Serialisierung und Deserialisierung stattfinden. Eine der dramatischsten ist die Tatsache, dass im Gegensatz zu der LosFormatter, die einen TextWriter verwendet, die ObjectStateFormatter verwendet einen BinaryWriter. Dadurch kann ASP.NET 2.0 eine Reihe von Bytes anstelle von Zeichenfolgen speichern. Nehmen wir zum Beispiel eine ganze Zahl. In ASP.NET 1.1 erforderte eine ganze Zahl 4 Byte Ansichtszustand. In ASP.NET 2.0 erfordert dieselbe ganze Zahl nur 1 Byte. Andere Verbesserungen wurden vorgenommen, um die Menge des angezeigten Ansichtszustands zu verringern. DateTime-Werte werden z. B. jetzt mit einem TickCount anstelle einer Zeichenfolge gespeichert.

Als ob all das nicht genug wäre, wurde besonderes Augenmerk auf die Tatsache, dass einer der größten Verbraucher von View-Status in 1.x war die DataGrid und ähnliche Kontrollen. Ein großer Nachteil von Steuerelementen wie dem DataGrid, wenn es um den Ansichtszustand geht, besteht darin, dass es häufig große Mengen wiederholter Informationen enthält. In ASP.NET 1.x wurden diese wiederholten Informationen einfach immer wieder gespeichert, was zu einem aufgeblähten Ansichtszustand führte. In ASP.NET 2.0 verwenden wir die neue IndexedString-Klasse, um solche Daten zu speichern. Wenn eine Zeichenfolge wiederholt wird, speichern wir nur das Token für den IndexedString und den Index in einer laufenden Tabelle von IndexedString-Objekten.

## <a name="control-state"></a>Kontrollzustand

Einer der Hauptgriffe, die Entwickler mit Demsichtszustand hatten, war die Größe, die sie der HTTP-Nutzlast hinzugefügt hat. Wie bereits erwähnt, ist einer der größten Consumer des Ansichtsstatus das DataGrid-Steuerelement. Um die riesigen Mengen an Ansichtsstatus zu vermeiden, die von einem DataGrid generiert werden, haben viele Entwickler den Ansichtszustand für dieses Steuerelement einfach deaktiviert. Leider war diese Lösung nicht immer eine gute. Der Anzeigezustand in ASP.NET 1.x enthält nicht nur Daten, die für die korrekte Funktionalität des Steuerelements erforderlich sind. Sie enthält auch Informationen zum Status der Benutzeroberfläche des Steuerelements. Wenn Sie die Paginierung in einem DataGrid zulassen möchten, müssen Sie den Ansichtszustand aktivieren, auch wenn Sie nicht alle UI-Informationen benötigen, die den Ansichtszustand enthalten. Es ist ein Alles-oder-Nichts-Szenario.

In ASP.NET 2.0 löst der Kontrollzustand dieses Problem durch die Einführung des Kontrollzustands gut. Der Steuerzustand enthält die Daten, die für die ordnungsgemäße Funktion eines Steuerelements unbedingt erforderlich sind. Im Gegensatz zum Ansichtszustand kann der Kontrollstatus nicht deaktiviert werden. Daher ist es wichtig, dass die im Kontrollzustand gespeicherten Daten sorgfältig kontrolliert werden.

> [!NOTE]
> Der Kontrollzustand wird zusammen mit dem \_ \_Ansichtszustand im Feld VIEWSTATE ausgeblendeter Form beibehalten.

Dieses Video ist eine exemplarische Vorgehensweise des Ansichts- und Kontrollstatus.

![](server-controls/_static/image1.png)

[Öffnen sie Ein-Bild-Video](server-controls/_static/state1.wmv)

Damit ein Serversteuerelement in den Steuerzustand gelesen und geschrieben werden kann, müssen Sie drei Schritte ausführen.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>Schritt 1: Aufrufen der RegisterRequiresControlState-Methode

Die RegisterRequiresControlState-Methode informiert ASP.NET, dass ein Steuerelement den Kontrollstatus beibehalten muss. Es wird ein Argument vom Typ Control verwendet, das das Steuerelement ist, das registriert wird.

Es ist wichtig zu beachten, dass die Registrierung nicht von Anforderung zu Anforderung beibehalten wird. Daher muss diese Methode bei jeder Anforderung aufgerufen werden, wenn ein Steuerelement den Kontrollstatus beibehalten soll. Es wird empfohlen, die Methode in OnInit aufzuberief.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>Schritt 2: Überschreiben von SaveControlState

Die SaveControlState-Methode speichert Steuerelementstatusänderungen für ein Steuerelement seit dem letzten Beitrag zurück. Es gibt ein Objekt zurück, das den Status des Steuerelements darstellt.

## <a name="step-3-override-loadcontrolstate"></a>Schritt 3: Überschreiben von LoadControlState

Die LoadControlState-Methode lädt den gespeicherten Status in ein Steuerelement. Die Methode verwendet ein Argument vom Typ Object, das den gespeicherten Status für das Steuerelement enthält.

## <a name="full-xhtml-compliance"></a>Vollständige XHTML-Konformität

Jeder Webentwickler weiß um die Bedeutung von Standards in Webanwendungen. Um eine standardbasierte Entwicklungsumgebung zu erhalten, ist ASP.NET 2.0 vollständig XHTML-kompatibel. Daher werden alle Tags gemäß XHTML-Standards in Browsern gerendert, die HTML 4.0 oder höher unterstützen.

Die DOCTYPE-Definition in ASP.NET 1.1 lautete wie folgt:

[!code-html[Main](server-controls/samples/sample6.html)]

In ASP.NET 2.0 lautet die standardmäßige DOCTYPE-Definition wie folgt:

[!code-html[Main](server-controls/samples/sample7.html)]

Wenn Sie dies wünschen, können Sie die standardmäßige XHTML-Kompatibilität über den XhtmlConformance-Knoten in der Konfigurationsdatei ändern. Der folgende Knoten in der Datei web.config ändert beispielsweise die XHTML-Konformität in XHTML 1.0 Strict:

[!code-xml[Main](server-controls/samples/sample8.xml)]

Wenn Sie dies wünschen, können Sie auch ASP.NET so konfigurieren, dass die in ASP.NET 1.x verwendete Legacykonfiguration wie folgt verwendet wird:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Adaptives Rendern mit Adaptern

In ASP.NET 1.x enthielt die &lt;Konfigurationsdatei einen browserCaps-Abschnitt,&gt; der ein HttpBrowserCapabilities-Objekt auffüllte. Dieses Objekt ermöglichte es einem Entwickler, zu bestimmen, welches Gerät eine bestimmte Anforderung stellt, und Code ordnungsgemäß zu rendern. In ASP.NET 2.0 wurde das Modell verbessert und verwendet nun die neue ControlAdapter-Klasse. Die ControlAdapter-Klasse überschreibt Ereignisse im Lebenszyklus des Steuerelements und steuert das Rendern von Steuerelementen basierend auf den Funktionen des Benutzer-Agents. Die Funktionen eines bestimmten Benutzer-Agenten werden durch eine Browserdefinitionsdatei (eine Datei mit einer .browser-Dateierweiterung) definiert, die in der Datei c:-windows-microsoft.net-framework-v2.0 gespeichert ist. \* \*Ordner \*"CONFIG" und \*"Browsers".

> [!NOTE]
> Die ControlAdapter-Klasse ist eine abstrakte Klasse.

Ähnlich wie &lt;der&gt; BrowserCaps-Abschnitt in 1.x verwendet die Browserdefinitionsdatei einen regulären Ausdruck, um die Benutzer-Agent-Zeichenfolge zu analysieren, um den anfordernden Browser zu identifizieren. Sie definieren bestimmte Funktionen für diesen Benutzer-Agent. Der ControlAdapter rendert das Steuerelement über die Render-Methode. Wenn Sie also die Render-Methode überschreiben, sollten Sie Render nicht für die Basisklasse aufrufen. Dies kann dazu führen, dass das Rendering zweimal auftritt, einmal für den Adapter und einmal für das Steuerelement selbst.

## <a name="developing-a-custom-adapter"></a>Entwickeln eines benutzerdefinierten Adapters

Sie können Ihren eigenen benutzerdefinierten Adapter entwickeln, indem Sie von ControlAdapter erben. Darüber hinaus können Sie von der abstrakten Klasse PageAdapter erben, wenn ein Adapter für eine Seite benötigt wird. Die Zuordnung von Steuerelementen zu &lt;Ihrem benutzerdefinierten Adapter erfolgt über das controlAdapters-Element in der Browserdefinitionsdatei.&gt; Der folgende XML-Code aus einer Browserdefinitionsdatei ordnet das Menüsteuerelement beispielsweise der MenuAdapter-Klasse zu:

[!code-html[Main](server-controls/samples/sample10.html)]

Mit diesem Modell wird es für einen Steuerelemententwickler ganz einfach, ein bestimmtes Gerät oder einen bestimmten Browser anzusprechen. Es ist auch ganz einfach für einen Entwickler, die vollständige Kontrolle darüber zu haben, wie Seiten auf jedem Gerät gerendert werden.

## <a name="per-device-rendering"></a>Pro-Gerät-Rendering

Serversteuerungseigenschaften in ASP.NET 2.0 können pro Gerät mit einem browserspezifischen Präfix angegeben werden. Der folgende Code ändert z. B. den Text einer Beschriftung, je nachdem, welches Gerät zum Durchsuchen der Seite verwendet wird.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Wenn die Seite, die diese Bezeichnung enthält, von Internet Explorer aus durchsucht wird, wird auf der Bezeichnung Text mit der Aufschrift "Sie surfen von Internet Explorer" angezeigt. Wenn die Seite von Firefox aus durchsucht wird, wird auf der Bezeichnung der Text "Sie surfen von Firefox aus" angezeigt. Wenn die Seite von einem anderen Gerät aus durchsucht wird, wird "Sie surfen von einem unbekannten Gerät aus" angezeigt. Jede Eigenschaft kann mit dieser speziellen Syntax angegeben werden.

## <a name="setting-focus"></a>Fokussetzen

ASP.NET 1.x-Entwickler wurden häufig gefragt, wie der anfängliche Fokus auf ein bestimmtes Steuerelement gelegt werden kann. Auf einer Anmeldeseite ist es beispielsweise nützlich, dass das Textfeld Benutzer-ID beim ersten Laden der Seite den Fokus erhält. In ASP.NET 1.x erforderte dies das Schreiben eines clientseitigen Skripts. Auch wenn ein solches Skript eine triviale Aufgabe ist, ist es in ASP.NET 2.0 dank der SetFocus-Methode nicht mehr notwendig. Die SetFocus-Methode verwendet ein Argument, das das Steuerelement angibt, das den Fokus erhalten soll. Dieses Argument kann entweder die Client-ID des Steuerelements als Zeichenfolge oder der Name des Serversteuerelements als Control-Objekt sein. Um beispielsweise den Anfangsfokus auf ein TextBox-Steuerelement namens txtUserID festzulegen, wenn\_die Seite zum ersten Mal geladen wird, fügen Sie dem Seitenladen den folgenden Code hinzu:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

-- oder

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 verwendet den (zuvor besprochenen) Webresource.axd-Handler, um eine clientseitige Funktion zu rendern, die den Fokus festlegt. Der Name der clientseitigen Funktion\_ist WebForm AutoFocus, wie hier gezeigt:

[!code-html[Main](server-controls/samples/sample14.html)]

Alternativ können Sie die Focus-Methode für ein Steuerelement verwenden, um den Anfangsfokus auf dieses Steuerelement festzulegen. Die Focus-Methode leitet sich von der Control-Klasse ab und ist für alle steuerelemente ASP.NET 2.0 verfügbar. Es ist auch möglich, den Fokus auf ein bestimmtes Steuerelement festzulegen, wenn ein Validierungsfehler auftritt. Das wird in einem späteren Modul behandelt.

## <a name="new-server-controls-in-aspnet-20"></a>Neue Serversteuerelemente in ASP.NET 2.0

Im Folgenden finden Sie neue Serversteuerelemente in ASP.NET 2.0. Einige davon werden wir in späteren Modulen näher erläutern.

## <a name="imagemap-control"></a>ImageMap-Steuerung

Mit dem ImageMap-Steuerelement können Sie einem Bild Hotspots hinzufügen, die einen Beitrag zurück initiieren oder zu einer URL navigieren können. Es stehen drei Arten von Hotspots zur Verfügung; CircleHotSpot, RectangleHotSpot und PolygonHotSpot. Hotspots werden über einen Sammlungseditor in Visual Studio oder programmgesteuert im Code hinzugefügt. Es ist keine Benutzeroberfläche zum Zeichnen von Hotspots auf einem Bild verfügbar. Die Koordinaten und die Größe oder der Radius des Hotspots müssen deklarativ angegeben werden. Es gibt auch keine visuelle Darstellung eines Hotspots im Designer. Wenn ein Hotspot für die Navigation zu einer URL konfiguriert ist, wird die URL über die NavigateUrl-Eigenschaft des Hotspots angegeben. Im Fall eines PostBack-Hotspots können Sie mit der PostBackValue-Eigenschaft eine Zeichenfolge im Postback übergeben, die im serverseitigen Code abgerufen werden kann.

![HotSpot-Sammlungs-Editor in Visual Studio](server-controls/_static/image1.jpg)

**Abbildung 1:** HotSpot-Sammlungs-Editor in Visual Studio

## <a name="bulletedlist-control"></a>BulletedList-Steuerelement

Das BulletedList-Steuerelement ist eine Aufzählung, die leicht an Daten gebunden werden kann. Die Liste kann über die BulletStyle-Eigenschaft bestellt (nummeriert) oder ungeordnet sein. Jedes Element in der Liste wird durch ein ListItem-Objekt dargestellt.

![BulletedList-Steuerelement in Visual Studio](server-controls/_static/image1.gif)

**Abbildung 2:** BulletedList-Steuerelement in Visual Studio

## <a name="hiddenfield-control"></a>HiddenField-Steuerung

Das HiddenField-Steuerelement fügt Ihrer Seite ein ausgeblendetes Formularfeld hinzu, dessen Wert im serverseitigen Code verfügbar ist. Der Wert eines ausgeblendeten Formularfelds wird im Allgemeinen zwischen den Post-Backs unverändert bleiben. Es ist jedoch möglich, dass ein böswilliger Benutzer den Wert vor dem Postback ändert. In diesem Fall wird das HiddenField-Steuerelement das ValueChanged-Ereignis auswerten. Wenn Sie vertrauliche Informationen im HiddenField-Steuerelement haben und sicherstellen möchten, dass sie unverändert bleiben, sollten Sie das ValueChanged-Ereignis im Code behandeln.

## <a name="fileupload-control"></a>FileUpload-Steuerelement

Das FileUpload-Steuerelement in ASP.NET 2.0 ermöglicht das Hochladen von Dateien auf einen Webserver über eine ASP.NET Seite. Dieses Steuerelement ähnelt der ASP.NET 1.x HtmlInputFile-Klasse mit wenigen Ausnahmen. In ASP.NET 1.x wurde empfohlen, die PostedFile-Eigenschaft auf NULL zu überprüfen, um festzustellen, ob Sie eine gute Datei haben. Das FileUpload-Steuerelement in ASP.NET 2.0 fügt eine neue HasFile-Eigenschaft hinzu, die Sie für denselben Zweck verwenden können, und es ist etwas effizienter.

Die PostedFile-Eigenschaft ist weiterhin für den Zugriff auf ein HttpPostedFile-Objekt verfügbar, aber einige der Funktionen der HttpPostedFile sind jetzt mit dem FileUpload-Steuerelement eigensystemintern verfügbar. Um beispielsweise eine hochgeladene Datei in ASP.NET 1.x zu speichern, rufen Sie die SaveAs-Methode für das HttpPostedFile-Objekt auf. Wenn Sie das FileUpload-Steuerelement in ASP.NET 2.0 verwenden, rufen Sie die SaveAs-Methode für das FileUpload-Steuerelement selbst auf.

Eine weitere signifikante Änderung des 2.0-Verhaltens (und wahrscheinlich die bedeutendste Änderung) ist, dass es nicht mehr notwendig ist, eine gesamte hochgeladene Datei in den Speicher zu laden, bevor sie gespeichert wird. In 1.x wird jede hochgeladene Datei vollständig im Speicher gespeichert, bevor sie auf die Festplatte geschrieben wird. Diese Architektur verhindert das Hochladen großer Dateien.

In ASP.NET 2.0 können Sie mit dem requestLengthDiskThreshold-Attribut des httpRuntime-Elements konfigurieren, wie viele Kilobytes in einem Puffer im Arbeitsspeicher gespeichert werden, bevor sie auf den Datenträger geschrieben werden.

**WICHTIG**: MSDN-Dokumentation (und Dokumentation an anderer Stelle) gibt an, dass dieser Wert in Bytes (nicht Kilobyte) liegt und dass der Standardwert 256 ist. Der Wert wird tatsächlich in Kilobytes angegeben, und der Standardwert ist 80. Wenn wir einen Standardwert von 80K haben, stellen wir sicher, dass der Puffer nicht auf dem Heap für große Objekte landet.

## <a name="wizard-control"></a>Assistentensteuerung

Es ist ziemlich häufig, ASP.NET Entwickler nzuringen mit dem Versuch, Informationen in einer Reihe von "Seiten" mit Panels oder durch Die Übertragung von Seite zu Seite zu sammeln. Meistens ist das Unterfangen frustrierend und zeitaufwändig. Das neue Wizard-Steuerelement löst die Probleme, indem lineare und nichtlineare Schritte in einer Assistentenschnittstelle zugelassen werden, mit denen Benutzer vertraut sind. Das Wizard-Steuerelement stellt Eingabeformulare in einer Reihe von Schritten dar. Jeder Schritt ist von einem bestimmten Typ, der von der StepType-Eigenschaft des Steuerelements angegeben wird. Die verfügbaren Schritttypen sind wie folgt:

| **Schritttyp** | **Erklärung** |
| --- | --- |
| Auto | Der Assistent bestimmt automatisch den Typ des Schritts basierend auf seiner Position innerhalb der Schritthierarchie. |
| Start | Der erste Schritt, oft verwendet, um eine einleitende Aussage zu präsentieren. |
| Schritt | Ein normaler Schritt. |
| Finish | Der letzte Schritt, der normalerweise verwendet wird, um eine Schaltfläche zum Beenden des Assistenten anzuzeigen. |
| Abgeschlossen | Stellt eine Nachricht dar, die Erfolg oder Misserfolg kommuniziert. |

> [!NOTE]
> Das Wizard-Steuerelement verfolgt seinen Status mithilfe ASP.NET-Steuerelementstatus. Daher kann die EnableViewState-Eigenschaft ohne Beeinträchtigung auf false festgelegt werden.

Dieses Video ist eine exemplarische Vorgehensweise des Assistenten-Steuerelements.

![](server-controls/_static/image2.png)

[Öffnen sie Ein-Bild-Video](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Lokalisieren der Steuerung

Das Lokalisierungssteuerelement ähnelt einem Literal-Steuerelement. Das Localize-Steuerelement verfügt **Mode** jedoch über eine Mode-Eigenschaft, die steuert, wie Markup, das dem Hinzugefügt wird, gerendert wird. Die Mode-Eigenschaft unterstützt die folgenden Werte:

| **Mode** | **Erklärung** |
| --- | --- |
| Transformieren | Markup wird entsprechend dem Protokoll des Browsers transformiert, der die Anforderung stellt. |
| Passthrough | Markup wird wie bisher gerendert. |
| Codieren | Markup, das dem Steuerelement hinzugefügt wird, wird mit HtmlEncode codiert. |

## <a name="multiview-and-view-controls"></a>MultiView- und View-Steuerelemente

Das MultiView-Steuerelement fungiert als Container für View-Steuerelemente, und das View-Steuerelement fungiert als Container (ähnlich wie ein Bedienfeld-Steuerelement) für andere Steuerelemente. Jede Ansicht in einem MultiView-Steuerelement wird durch ein einzelnes View-Steuerelement dargestellt. Das erste Ansichtssteuerelement in Der MultiView ist Ansicht 0, das zweite ist Ansicht 1 usw. Sie können Ansichten wechseln, indem Sie den ActiveViewIndex des MultiView-Steuerelements angeben.

## <a name="substitution-control"></a>Substitutionskontrolle

Das Substitutionssteuerelement wird in Verbindung mit ASP.NET Zwischenspeicherung verwendet. In Fällen, in denen Sie die Vorteile des Zwischenspeicherns nutzen möchten, Aber Teile einer Seite haben, die bei jeder Anforderung aktualisiert werden müssen (d. h. Teile einer Seite, die vom Zwischenspeichern ausgenommen sind), bietet die Substitution-Komponente eine großartige Lösung. Das Steuerelement rendert eigentlich keine Ausgabe allein. Stattdessen ist sie an eine Methode im serverseitigen Code gebunden. Wenn die Seite angefordert wird, wird die Methode aufgerufen, und das zurückgegebene Markup wird anstelle des Ersetzungssteuerelements gerendert.

Die Methode, an die das Substitution-Steuerelement gebunden ist, wird über die **MethodName-Eigenschaft** angegeben. Diese Methode muss die folgenden Kriterien erfüllen:

- Es muss sich um eine statische (in VB gemeinsam genutzte) Methode handelt.
- Es akzeptiert einen Parameter vom Typ HttpContext.
- Es gibt eine Zeichenfolge zurück, die das Markup darstellt, das das Steuerelement auf der Seite ersetzen soll.

Das Substitution-Steuerelement kann kein anderes Steuerelement auf der Seite ändern, aber es hat Zugriff auf den aktuellen HttpContext über seinen Parameter.

## <a name="gridview-control"></a>GridView-Steuerung

Das GridView-Steuerelement ist der Ersatz für das DataGrid-Steuerelement. Dieses Steuerelement wird in einem späteren Modul ausführlicher behandelt.

## <a name="detailsview-control"></a>DetailsView Control

Mit dem Steuerelement DetailsView können Sie einen einzelnen Datensatz aus einer Datenquelle anzeigen und bearbeiten oder löschen. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="formview-control"></a>FormView-Steuerelement

Das FormView-Steuerelement wird verwendet, um einen einzelnen Datensatz aus einer Datenquelle in einer konfigurierbaren Schnittstelle anzuzeigen. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="accessdatasource-control"></a>AccessDataSource-Steuerung

Das AccessDataSource-Steuerelement wird verwendet, um eine Access-Datenbank von Daten zu binden. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="objectdatasource-control"></a>ObjectDataSource-Steuerelement

Das ObjectDataSource-Steuerelement wird verwendet, um eine dreistufige Architektur zu unterstützen, sodass Steuerelemente an ein Geschäftsobjekt der mittleren Ebene gebunden werden können, im Gegensatz zu einem zweistufigen Modell, bei dem Steuerelemente direkt an die Datenquelle gebunden sind. Sie wird in einem späteren Modul ausführlicher behandelt.

## <a name="xmldatasource-control"></a>XmlDataSource-Steuerelement

Das XmlDataSource-Steuerelement wird verwendet, um Daten an eine XML-Datenquelle zu binden. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource-Steuerelement

Das SiteMapDataSource-Steuerelement stellt die Datenbindung für Websitenavigationssteuerelemente basierend auf einer Siteübersicht bereit. Sie wird in einem späteren Modul ausführlicher behandelt.

## <a name="sitemappath-control"></a>SiteMapPath-Steuerelement

Das SiteMapPath-Steuerelement zeigt eine Reihe von Navigationslinks an, die häufig als Breadcrumbs bezeichnet werden. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="menu-control"></a>Menu-Steuerelement

Das Menüsteuerelement zeigt dynamische Menüs mit DHTML an. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="treeview-control"></a>TreeView-Steuerelement

Das TreeView-Steuerelement wird verwendet, um eine hierarchische Strukturansicht von Daten anzuzeigen. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="login-control"></a>Login-Steuerung

Das Login-Steuerelement bietet einen Mechanismus zum Anmelden bei einer Website. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="loginview-control"></a>LoginView-Steuerelement

Das LoginView-Steuerelement ermöglicht die Anzeige verschiedener Vorlagen basierend auf dem Anmeldestatus eines Benutzers. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="passwordrecovery-control"></a>PasswordRecovery-Steuerung

Das PasswordRecovery-Steuerelement wird verwendet, um vergessene Kennwörter von Benutzern einer ASP.NET-Anwendung abzurufen. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="loginstatus"></a>LoginStatus

Das LoginStatus-Steuerelement zeigt den Anmeldestatus eines Benutzers an. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="loginname"></a>LoginName

Das LoginName-Steuerelement zeigt den Benutzernamen eines Benutzers an, nachdem er bei einer ASP.NET-Anwendung angemeldet wurde. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="createuserwizard"></a>Createuserwizard

Der CreateUserWizard ist ein konfigurierbarer Assistent, der Benutzern die Möglichkeit gibt, ein ASP.NET Mitgliedschaftskonto für die Verwendung in einer ASP.NET Anwendung zu erstellen. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="changepassword"></a>ChangePassword

Mit dem ChangePassword-Steuerelement können Benutzer ihr Kennwort für eine ASP.NET-Anwendung ändern. Es wird in einem späteren Modul ausführlicher behandelt.

## <a name="various-webparts"></a>Verschiedene WebParts

ASP.NET 2.0 wird mit verschiedenen Webparts ausgeliefert. Diese werden in einem späteren Modul ausführlich behandelt.
