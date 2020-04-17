---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Verwenden von Controllern und Ansichten zum Implementieren einer Listen-/Details-Benutzeroberfläche | Microsoft Docs
author: rick-anderson
description: Schritt 4 zeigt, wie Sie der Anwendung einen Controller hinzufügen, der unser Modell nutzt, um Benutzern eine Datenauflistung/Details-Navigationserfahrung zu bieten...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541311"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Implementieren einer Auflistungs-/Detailbenutzeroberfläche mit Controllern und Ansichten

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 4 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 4 zeigt, wie Sie der Anwendung einen Controller hinzufügen, der unser Modell nutzt, um Benutzern eine Datenauflistung/Details-Navigationserfahrung für Abendessen auf unserer NerdDinner-Website zu bieten.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner Schritt 4: Controller und Ansichten

Bei herkömmlichen Webframeworks (klassische ASP, PHP, ASP.NET Web Forms usw.) werden eingehende URLs in der Regel Dateien auf der Festplatte zugeordnet. Beispiel: Eine Url-Anfrage wie "/Products.aspx" oder "/Products.php" kann beispielsweise mit einer Datei "Products.aspx" oder "Products.php" verarbeitet werden.

Webbasierte MVC-Frameworks ordnen URLs dem Servercode auf eine etwas andere Weise zu. Anstatt eingehende URLs Dateien zuzuordnen, ordnen sie URLs Methoden für Klassen zu. Diese Klassen werden als "Controller" bezeichnet und sind für die Verarbeitung eingehender HTTP-Anforderungen, die Verarbeitung von Benutzereingaben, das Abrufen und Speichern von Daten sowie das Bestimmen der Antwort zum Zurücksenden an den Client (Html anzeigen, Datei herunterladen, Umleiten zu einer anderen URL usw.) verantwortlich.

Nun, da wir ein grundlegendes Modell für unsere NerdDinner-Anwendung aufgebaut haben, wird unser nächster Schritt sein, einen Controller zu der Anwendung hinzuzufügen, die es nutzt, um Benutzern eine Datenauflistung/Details Navigationserfahrung für Abendessen auf unserer Website zu bieten.

### <a name="adding-a-dinnerscontroller-controller"></a>Hinzufügen eines DinnersController Controllers

Wir beginnen mit einem Rechtsklick auf den Ordner "Controller" in unserem Webprojekt und wählen dann den Menübefehl **Add-&gt;Controller** aus (Sie können diesen Befehl auch ausführen, indem Sie Strg-M, Strg-C eingeben):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Dadurch wird das Dialogfeld "Controller hinzufügen" angezeigt:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

Wir nennen den neuen Controller "DinnersController" und klicken auf die Schaltfläche "Hinzufügen". Visual Studio fügt dann eine DinnersController.cs-Datei unter unserem Verzeichnis "Controllers" hinzu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Außerdem wird die neue DinnersController-Klasse im Code-Editor geöffnet.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Hinzufügen von Index() und Details() Aktionsmethoden zur DinnersController-Klasse

Wir möchten es Besuchern, die unsere Anwendung nutzen, ermöglichen, eine Liste der bevorstehenden Abendessen zu durchsuchen, und ihnen erlauben, auf ein beliebiges Abendessen in der Liste zu klicken, um spezifische Details dazu zu sehen. Wir tun dies, indem wir die folgenden URLs aus unserer Anwendung veröffentlichen:

| **URL** | **Zweck** |
| --- | --- |
| */Abendessen/* | Anzeigen einer HTML-Liste der bevorstehenden Abendessen |
| */Dinners/Details/[id]* | Zeigen Sie Details zu einem bestimmten Abendessen an, die durch einen in die URL eingebetteten "id"-Parameter angezeigt werden – der mit der DinnerID des Abendessens in der Datenbank übereinstimmt. Beispiel: /Dinners/Details/2 zeigt eine HTML-Seite mit Details zum Dinner an, dessen DinnerID-Wert 2 ist. |

Wir werden erste Implementierungen dieser URLs veröffentlichen, indem wir unserer DinnersController-Klasse zwei öffentliche "Aktionsmethoden" hinzufügen, wie folgt:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Wir führen dann die NerdDinner-Anwendung aus und verwenden unseren Browser, um sie aufzurufen. Wenn Sie die *URL "/Dinners/" eingeben,* wird unsere *Index()-Methode* ausgeführt, und sie sendet die folgende Antwort zurück:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

Wenn Sie die *URL "/Dinners/Details/2" eingeben,* wird unsere *Details()-Methode* ausgeführt und die folgende Antwort zurückgesendet:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

Sie fragen sich vielleicht - wie wusste ASP.NET MVC, unsere DinnersController-Klasse zu erstellen und diese Methoden aufzurufen? Um dies zu verstehen, werfen wir einen kurzen Blick auf die Funktionsweise des Routings.

### <a name="understanding-aspnet-mvc-routing"></a>Grundlegendes zum ASP.NET MVC-Routing

ASP.NET MVC enthält ein leistungsstarkes URL-Routingmodul, das eine große Flexibilität bei der Steuerung der Zuordnung von URLs zu Controllerklassen bietet. Es ermöglicht uns, vollständig anzupassen, wie ASP.NET MVC wählt, welche Controller-Klasse zu erstellen, welche Methode auf sie aufgerufen werden, sowie verschiedene Möglichkeiten zu konfigurieren, dass Variablen automatisch aus der URL/Querystring analysiert und an die Methode als Parameterargumente übergeben werden können. Es bietet die Flexibilität, eine Website für SEO (Suchmaschinenoptimierung) vollständig zu optimieren und jede URL-Struktur zu veröffentlichen, die wir von einer Anwendung wollen.

Standardmäßig verfügen neue ASP.NET MVC-Projekten über einen vorkonfigurierten Satz von URL-Routingregeln, die bereits registriert sind. Dies ermöglicht es uns, einfach mit einer Anwendung zu beginnen, ohne explizit etwas konfigurieren zu müssen. Die Standard-Routingregelregistrierungen finden Sie in der Klasse "Anwendung" unserer Projekte – die wir öffnen können, indem wir auf die Datei "Global.asax" im Stammverzeichnis unseres Projekts doppelklicken:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

Die standardmäßigen ASP.NET MVC-Routingregeln werden innerhalb der "RegisterRoutes"-Methode dieser Klasse registriert:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

Die "Routen. MapRoute()" Methodenaufruf oben registriert eine Standardroutingregel, die eingehende URLs Controllerklassen unter Verwendung des URL-Formats "/-controller"/-action" zuordnet – wobei "controller" der Name der Controllerklasse ist, um instanziieren zu können, "action" der Name einer öffentlichen Methode ist, die darauf aufgerufen werden soll, und "id" ist ein optionaler Parameter, der in die URL eingebettet ist und als Argument an die Methode übergeben werden kann. Der dritte Parameter, der an den Methodenaufruf "MapRoute()" übergeben wird, ist ein Satz von Standardwerten, die für die Controller-/Aktions-/ID-Werte verwendet werden sollen, falls sie nicht in der URL vorhanden sind (Controller = "Home", Action="Index", Id=").

Im Folgenden finden Sie eine Tabelle, die veranschaulicht, wie eine Vielzahl von URLs mithilfe der Standardroute<em>"/-controller"</em>zugeordnet werden:

| **URL** | **Controller-Klasse** | **Aktionsmethode** | **Übergebene Parameter** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | AbendessenController | Details(id) | id=2 |
| */Dinners/Bearbeiten/5* | AbendessenController | Bearbeiten(id) | id=5 |
| */Dinners/Erstellen* | AbendessenController | Create() | – |
| */Abendessen* | AbendessenController | Index() | – |
| */Startseite* | Homecontroller | Index() | – |
| */* | Homecontroller | Index() | – |

Die letzten drei Zeilen zeigen die verwendeten Standardwerte (Controller = Home, Action = Index, Id = "") an. Da die "Index"-Methode als Standardaktionsname registriert ist, wenn kein "/Dinners" und "/Home"-URLs angegeben sind, wird die Index()-Aktionsmethode für ihre Controllerklassen aufgerufen. Da der "Home"-Controller als Standardcontroller registriert ist, wenn kein Controller angegeben ist, bewirkt die "/"-URL, dass der HomeController erstellt und die Index()-Aktionsmethode darauf aufgerufen wird.

Wenn Ihnen diese Standard-URL-Routingregeln nicht gefallen, ist die gute Nachricht, dass sie leicht zu ändern sind – bearbeiten Sie sie einfach innerhalb der RegisterRoutes-Methode oben. Für unsere NerdDinner-Anwendung werden wir jedoch keine der Standard-URL-Routingregeln ändern – stattdessen verwenden wir sie einfach so, wie sie sind.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Verwenden des DinnerRepository von unserem DinnersController

Ersetzen wir nun unsere aktuelle Implementierung der Aktionsmethoden Index() und Details() des DinnersControllers durch Implementierungen, die unser Modell verwenden.

Wir verwenden die DinnerRepository-Klasse, die wir zuvor erstellt haben, um das Verhalten zu implementieren. Wir beginnen mit dem Hinzufügen einer "using"-Anweisung, die auf den Namespace "NerdDinner.Models" verweist, und deklarieren dann eine Instanz unseres DinnerRepository als Feld in unserer DinnerController-Klasse.

Später in diesem Kapitel stellen wir das Konzept der "Dependency Injection" vor und zeigen einen anderen Weg für unsere Controller auf, einen Verweis auf ein DinnerRepository zu erhalten, das bessere Komponententests ermöglicht – aber im Moment erstellen wir nur eine Instanz unserer DinnerRepository-Inline wie unten.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Jetzt können wir eine HTML-Antwort mithilfe unserer abgerufenen Datenmodellobjekte wieder generieren.

### <a name="using-views-with-our-controller"></a>Verwenden von Ansichten mit unserem Controller

Während es möglich ist, Code innerhalb unserer Aktionsmethoden zu schreiben, um HTML zusammenzustellen und dann die *Response.Write()-Hilfsmethode* zu verwenden, um ihn an den Client zurückzusenden, wird dieser Ansatz schnell ziemlich schwerfällig. Ein viel besserer Ansatz ist, dass wir nur Anwendungs- und Datenlogik innerhalb unserer DinnersController-Aktionsmethoden ausführen und dann die Daten übergeben, die zum Rendern einer HTML-Antwort an eine separate "View"-Vorlage erforderlich sind, die für die Hereingabe der HTML-Darstellung verantwortlich ist. Wie wir in einem Moment sehen werden, ist eine "Ansicht"-Vorlage eine Textdatei, die in der Regel eine Kombination aus HTML-Markup und eingebettetem Rendering-Code enthält.

Die Trennung unserer Controller-Logik von unserer Sicht Rendering bringt mehrere große Vorteile. Insbesondere hilft es, eine klare "Trennung von Bedenken" zwischen dem Anwendungscode und UI-Formatierung /Rendering-Code zu erzwingen. Dies erleichtert das Einheitentesten der Anwendungslogik in Isolation von ui-Renderinglogik. Es erleichtert das spätere Ändern der UI-Renderingvorlagen, ohne Anwendungscodeänderungen vornehmen zu müssen. Und es kann Entwicklern und Designern die Zusammenarbeit bei Projekten erleichtern.

Wir können unsere DinnersController-Klasse aktualisieren, um anzugeben, dass wir eine Ansichtsvorlage verwenden möchten, um eine HTML-UI-Antwort zurückzusenden, indem wir die Methodensignaturen unserer beiden Aktionsmethoden von einem Rückgabetyp "void" ändern, um stattdessen den Rückgabetyp "ActionResult" zu verwenden. Wir können dann die *View()-Hilfsmethode* in der Controller-Basisklasse aufrufen, um ein "ViewResult"-Objekt wie folgt zurückzugeben:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

Die Signatur der *View()-Hilfsmethode,* die wir oben verwenden, sieht wie folgt aus:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

Der erste Parameter für die *View()-Hilfsmethode* ist der Name der Ansichtsvorlagendatei, die wir zum Rendern der HTML-Antwort verwenden möchten. Der zweite Parameter ist ein Modellobjekt, das die Daten enthält, die die Ansichtsvorlage zum Rendern der HTML-Antwort benötigt.

Innerhalb unserer Index()-Aktionsmethode rufen wir die *View()-Hilfsmethode* auf und geben an, dass wir eine HTML-Liste von Abendessen mithilfe einer Ansichtsvorlage "Index" rendern möchten. Wir übergeben die Ansichtsvorlage an eine Sequenz von Dinner-Objekten, um die Liste zu generieren:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Innerhalb unserer Detail()-Aktionsmethode versuchen wir, ein Dinner-Objekt mit der in der URL angegebenen ID abzurufen. Wenn ein gültiges Dinner gefunden wird, rufen wir die *View()-Hilfsmethode* auf, die angibt, dass wir eine Ansichtsvorlage "Details" verwenden möchten, um das abgerufene Dinner-Objekt zu rendern. Wenn ein ungültiges Abendessen angefordert wird, geben wir eine hilfreiche Fehlermeldung wieder, die darauf hinweist, dass das Dinner nicht mit einer "NotFound"-Ansichtsvorlage vorhanden ist (und einer überladenen Version der *View()-Hilfsmethode,* die nur den Vorlagennamen annimmt):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Implementieren wir nun die Ansichtsvorlagen "NotFound", "Details" und "Index".

### <a name="implementing-the-notfound-view-template"></a>Implementieren der Ansichtsvorlage "NotFound"

Wir beginnen mit der Implementierung der Ansichtsvorlage "NotFound", die eine freundliche Fehlermeldung anzeigt, die angibt, dass das gewünschte Abendessen nicht gefunden werden kann.

Wir erstellen eine neue Ansichtsvorlage, indem wir unseren Textcursor innerhalb einer Controller-Aktionsmethode positionieren und dann mit der rechten Maustaste klicken und den Menübefehl "Ansicht hinzufügen" auswählen (wir können diesen Befehl auch ausführen, indem wir Strg-M, Strg-V eingeben):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Dadurch wird ein Dialogfeld "Ansicht hinzufügen" wie folgt angezeigt. Standardmäßig füllt das Dialogfeld den Namen der Ansicht vor, die erstellt werden soll, um dem Namen der Aktionsmethode zu entsprechen, in der sich der Cursor beim Starten des Dialogfelds befand (in diesem Fall "Details"). Da wir zuerst die Vorlage "NotFound" implementieren möchten, überschreiben wir diesen Ansichtsnamen und legen ihn stattdessen auf "NotFound" fest:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, erstellt Visual Studio eine neue Ansichtsvorlage "NotFound.aspx" für uns im Verzeichnis "-Ansichten"-Dinners (die es auch erstellt, wenn das Verzeichnis noch nicht vorhanden ist):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Außerdem wird unsere neue Ansichtsvorlage "NotFound.aspx" im Code-Editor geöffnet:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

View-Vorlagen haben standardmäßig zwei "Inhaltsbereiche", in denen wir Inhalt und Code hinzufügen können. Die erste ermöglicht es uns, den "Titel" der zurückgesendeten HTML-Seite anzupassen. Die zweite ermöglicht es uns, den "Hauptinhalt" der zurückgesendeten HTML-Seite anzupassen.

Um unsere Ansichtsvorlage "NotFound" zu implementieren, fügen wir einige grundlegende Inhalte hinzu:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Wir können es dann im Browser ausprobieren. Um dies zu tun, lassen Sie uns die *"/Dinners/Details/9999"* URL anfordern. Dies bezieht sich auf ein Abendessen, das derzeit nicht in der Datenbank vorhanden ist, und veranlassen unsere DinnersController.Details() Aktionsmethode, um unsere Ansichtsvorlage "NotFound" zu rendern:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Eine Sache, die Sie im Screenshot oben bemerken werden, ist, dass unsere grundlegende Ansichtsvorlage eine Reihe von HTML geerbt hat, die den Hauptinhalt auf dem Bildschirm umgibt. Dies liegt daran, dass unsere Ansichtsvorlage eine "Master-Seite"-Vorlage verwendet, die es uns ermöglicht, ein konsistentes Layout auf alle Ansichten auf der Website anzuwenden. In einem späteren Teil dieses Tutorials wird erläutert, wie Masterseiten mehr funktionieren.

### <a name="implementing-the-details-view-template"></a>Implementieren der Ansichtsvorlage "Details"

Implementieren wir nun die Ansichtsvorlage "Details", die HTML für ein einzelnes Dinner-Modell generiert.

Dazu positionieren wir unseren Textcursor innerhalb der Aktionsmethode Details, und klicken Dann mit der rechten Maustaste auf den Menübefehl "Ansicht hinzufügen" (oder drücken Sie Strg-M, Strg-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Dadurch wird das Dialogfeld "Ansicht hinzufügen" angezeigt. Der Standardansichtsname ("Details") wird beibehalten. Außerdem aktivieren wir das Kontrollkästchen "Erstellen einer stark typisierten Ansicht" im Dialogfeld und wählen (mit der Dropdownliste Combobox) den Namen des Modelltyps aus, den wir vom Controller an die Ansicht übergeben. Für diese Ansicht übergeben wir ein Dinner-Objekt (der vollqualifizierte Name für diesen Typ ist: "NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

Im Gegensatz zur vorherigen Vorlage, bei der wir eine "Leere Ansicht" erstellt haben, wählen wir dieses Mal, die Ansicht automatisch mit einer "Details"-Vorlage zu "gerüsten". Wir können dies anzeigen, indem wir die Dropdown-Liste "Inhalt anzeigen" im Dialog oben ändern.

"Scaffolding" generiert eine erste Implementierung unserer Detailansichtsvorlage basierend auf dem Dinner-Objekt, das wir an sie übergeben. Dies bietet uns eine einfache Möglichkeit, schnell mit der Implementierung unserer Ansichtsvorlagen zu beginnen.

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, erstellt Visual Studio eine neue Ansichtsvorlagedatei "Details.aspx" für uns in unserem Verzeichnis "Ansichten":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Außerdem wird unsere neue Ansichtsvorlage "Details.aspx" im Code-Editor geöffnet. Es wird eine erste Gerüstimplementierung einer Detailansicht auf der Grundlage eines Dinner-Modells enthalten. Das Gerüstmodul verwendet .NET-Reflektion, um die öffentlichen Eigenschaften zu betrachten, die für die übergebene Klasse verfügbar gemacht wurden, und fügt basierend auf jedem gefundenen Typ den entsprechenden Inhalt hinzu:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

Wir können die *URL "/Dinners/Details/1"* anfordern, um zu sehen, wie diese "Details"-Gerüstimplementierung im Browser aussieht. Mit dieser URL wird eines der Abendessen angezeigt, die wir manuell zu unserer Datenbank hinzugefügt haben, als wir sie zum ersten Mal erstellt haben:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

Dies bringt uns schnell in Gang und bietet uns eine erste Implementierung unserer Details.aspx-Ansicht. Wir können dann gehen und optimieren, um die Benutzeroberfläche zu unserer Zufriedenheit anzupassen.

Wenn wir uns die Vorlage Details.aspx genauer ansehen, werden wir feststellen, dass sie sowohl statischen HTML- als auch eingebetteten Renderingcode enthält. &lt;%&gt; % Code-Nuggets führen Code aus, &lt;wenn&gt; die Ansichtsvorlage gerendert wird, und %= % Code-Nuggets führen den darin enthaltenen Code aus und rendern das Ergebnis dann in den Ausgabestream der Vorlage.

Wir können Code in unserer Ansicht schreiben, der auf das Modellobjekt "Dinner" zugreift, das von unserem Controller mit einer stark typisierten "Model"-Eigenschaft übergeben wurde. Visual Studio bietet uns vollen Code-Intellisense, wenn wir im Editor auf diese "Model"-Eigenschaft zugreifen:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Lassen Sie uns einige Anpassungen vornehmen, so dass die Quelle für unsere endgültige Detailansichtsvorlage wie folgt aussieht:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

Wenn wir wieder auf die *URL "/Dinners/Details/1"* zugreifen, wird sie nun wie folgt gerendert:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>Implementieren der Ansichtsvorlage "Index"

Implementieren wir nun die Ansichtsvorlage "Index", die eine Liste der kommenden Dinners generiert. Dazu positionieren wir unseren Textcursor innerhalb der Index-Aktionsmethode, und klicken dann mit der rechten Maustaste und wählen sie den Menübefehl "Ansicht hinzufügen" (oder drücken Sie Strg-M, Strg-V).

Im Dialogfeld "Ansicht hinzufügen" behalten wir die Ansichtsvorlage mit dem Namen "Index" und aktivieren das Kontrollkästchen "Eine stark typisierte Ansicht erstellen". Dieses Mal werden wir automatisch eine "Liste"-Ansichtsvorlage generieren und "NerdDinner.Models.Dinner" als Modelltyp auswählen, der an die Ansicht übergeben wird (was, weil wir angegeben haben, dass wir ein "Liste"-Gerüst erstellen, dazu führt, dass das Dialogfeld Ansicht hinzufügen davon ausgeht, dass wir eine Sequenz von Dinner-Objekten von unserem Controller an die Ansicht übergeben):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, erstellt Visual Studio eine neue Ansichtsvorlagedatei "Index.aspx" für uns in unserem Verzeichnis "-Ansichten". Es wird eine erste Implementierung darin "gerüsten", die eine HTML-Tabelle der Dinners enthält, die wir an die Ansicht übergeben.

Wenn wir die Anwendung ausführen und auf die *"/Dinners/"* URL zugreifen, wird unsere Liste der Abendessen wie folgt gerendert:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

Die Obige Tischlösung gibt uns ein gitterartiges Layout unserer Dinner-Daten – was nicht ganz das ist, was wir für unseren Verbraucher mit Blick auf dinner listing wollen. Wir können die Ansichtsvorlage Index.aspx aktualisieren und ändern, um &lt;&gt; weniger Datenspalten aufzulisten, und ein ul-Element verwenden, um sie anstelle einer Tabelle mit dem folgenden Code zu rendern:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Wir verwenden das Schlüsselwort "var" innerhalb der obigen Foreach-Anweisung, während wir jedes Abendessen in unserem Modell durchlaufen. Diejenigen, die nicht mit C-Nr. 3.0 vertraut sind, denken vielleicht, dass die Verwendung von "var" bedeutet, dass das Dinner-Objekt spät gebunden ist. Es bedeutet stattdessen, dass der Compiler typ-inference gegen die stark typisierte "Model"-Eigenschaft&lt;&gt;(die vom Typ "IEnumerable Dinner" ist) und die lokale "Dinner"-Variable als Dinner-Typ kompiliert – was bedeutet, dass wir volle Intellekt- und Kompilierungszeitüberprüfung enumgieren in Codeblöcken erhalten:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Wenn wir auf refresh on the */Dinners* URL in unserem Browser klicken, sieht unsere aktualisierte Ansicht jetzt wie folgt aus:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

Das sieht besser aus – ist aber noch nicht ganz da. Unser letzter Schritt besteht darin, Endbenutzern zu ermöglichen, auf einzelne Dinner in der Liste zu klicken und Details zu ihnen zu sehen. Wir implementieren dies, indem wir HTML-Hyperlinkelemente rendern, die mit der Detail-Aktionsmethode auf unserem DinnersController verknüpft sind.

Wir können diese Hyperlinks in unserer Indexansicht auf zwei Arten generieren. Die erste besteht darin, &lt;&gt; HTML manuell als Element &lt;wie&gt; unten zu &lt;&gt; erstellen, wobei wir % %-Blöcke in das HTML-Element einbetten:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Ein alternativer Ansatz, den wir verwenden können, besteht darin, die integrierte "Html.ActionLink()"-Hilfsmethode &lt;innerhalb&gt; ASP.NET MVC zu nutzen, die das programmgesteuerte Erstellen eines HTML-Elements unterstützt, das mit einer anderen Aktionsmethode auf einem Controller verknüpft ist:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Der erste Parameter für die Html.ActionLink()-Hilfsmethode ist der anzuzeigende Linktext (in diesem Fall der Titel des Abendessens), der zweite Parameter ist der Controller-Aktionsname, zu dem wir den Link generieren möchten (in diesem Fall die Details-Methode), und der dritte Parameter ist ein Satz von Parametern, die an die Aktion gesendet werden sollen (als anonymer Typ mit Eigenschaftsnamen/Werten implementiert). In diesem Fall geben wir den Parameter "id" des Abendessens an, mit dem wir eine Verknüpfung herstellen möchten, und da die Standardmäßige URL-Routingregel in ASP.NET MVC ""Controller"/"Aktion" ist, generiert die Html.ActionLink()-Hilfsmethode die folgende Ausgabe:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Für unsere Index.aspx-Ansicht verwenden wir den Html.ActionLink()-Hilfsmethodenansatz und haben jedes Abendessen im Listenlink zur entsprechenden Detail-URL:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

Und jetzt, wenn wir die */Dinners* URL treffen, sieht unsere Dinner-Liste wie folgt aus:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Wenn wir auf eines der Dinners in der Liste klicken, navigieren wir, um Details dazu zu sehen:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Konventionsbasierte Benennung und die Verzeichnisstruktur von Sviews

ASP.NET MVC-Anwendungen verwenden standardmäßig eine konventionsbasierte Verzeichnisbenennungsstruktur, wenn Ansichtsvorlagen aufgelöst werden. Auf diese Weise können Entwickler vermeiden, dass sie einen Standortpfad vollständig qualifizieren müssen, wenn sie auf Ansichten innerhalb einer Controller-Klasse verweisen. Standardmäßig sucht ASP.NET MVC nach der Ansichtsvorlagendatei\[im\* Verzeichnis *-Views ControllerName] unter der Anwendung.

Zum Beispiel haben wir an der DinnersController-Klasse gearbeitet, die explizit auf drei Ansichtsvorlagen verweist: "Index", "Details" und "NotFound". ASP.NET MVC sucht standardmäßig nach diesen Ansichten im Verzeichnis *"Views"* unter unserem Anwendungsstammverzeichnis:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Beachten Sie oben, wie es derzeit drei Controller-Klassen innerhalb des Projekts gibt (DinnersController, HomeController und AccountController – die letzten beiden wurden standardmäßig hinzugefügt, als wir das Projekt erstellt haben), und es gibt drei Unterverzeichnisse (eine für jeden Controller) innerhalb des Verzeichnisses .Views.

Ansichten, auf die von den Controllern "Startseite" und "Konten" verwiesen wird, lösen ihre Ansichtsvorlagen automatisch aus den jeweiligen Verzeichnissen *"Ansichten"* und *"Ansichten" auf.* Das Unterverzeichnis *"Ansichten"* bietet eine Möglichkeit, Ansichtsvorlagen zu speichern, die auf mehreren Controllern innerhalb der Anwendung wiederverwendet werden. Wenn ASP.NET MVC versucht, eine Ansichtsvorlage aufzulösen, überprüft es zunächst das spezifische Verzeichnis *von 'Views\[Controller],* und wenn es die Ansichtsvorlage dort nicht finden kann, wird es innerhalb des Verzeichnisses *"Ansichten"* angezeigt.

Wenn es darum geht, einzelne Ansichtsvorlagen zu benennen, wird empfohlen, dass die Ansichtsvorlage denselben Namen wie die Aktionsmethode verwendet, die sie zum Rendern veranlasst hat. Darüber wird z. B. die Ansicht "Index" verwendet, um das Ansichtsergebnis zu rendern, und die Aktionsmethode "Details" verwendet die Ansicht "Details", um die Ergebnisse zu rendern. Auf diese Weise können Sie schnell erkennen, welche Vorlage mit jeder Aktion verknüpft ist.

Entwickler müssen den Namen der Ansichtsvorlage nicht explizit angeben, wenn die Ansichtsvorlage denselben Namen wie die auf dem Controller aufgerufene Aktionsmethode hat. Stattdessen können wir das Modellobjekt einfach an die "View()"-Hilfsmethode übergeben (ohne den Ansichtsnamen anzugeben), und ASP.NET MVC leitet automatisch ab, dass wir die Ansichtsvorlage *"Views\[ControllerName]\[ActionName]* auf dem Datenträger verwenden möchten, um sie zu rendern.

Dies ermöglicht es uns, unseren Controller-Code ein wenig zu bereinigen und zu vermeiden, dass der Name zweimal in unserem Code dupliziert wird:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

Der obige Code ist alles, was benötigt wird, um eine schöne Dinner-Auflistung / Details Erfahrung für die Website zu implementieren.

#### <a name="next-step"></a>Nächster Schritt

Wir haben jetzt eine schöne Dinner-Browsing-Erfahrung gebaut.

Lassen Sie uns nun DIE Unterstützung für die Bearbeitungsunterstützung von CRUD-Datenformularen aktivieren (Erstellen, Lesen, Aktualisieren, Löschen).

> [!div class="step-by-step"]
> [Zurück](build-a-model-with-business-rule-validations.md)
> [Weiter](provide-crud-create-read-update-delete-data-form-entry-support.md)
