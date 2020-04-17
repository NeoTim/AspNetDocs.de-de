---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Wiederverwenden der Benutzeroberfläche mithilfe von Masterseiten und Partialen | Microsoft Docs
author: rick-anderson
description: Schritt 7 untersucht, wie wir das "DRY-Prinzip" in unseren Ansichtsvorlagen anwenden können, um Codeduplizierungen mithilfe von Partizipationsvorlagen und Masterseiten zu vermeiden.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542598"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Wiederverwenden der Benutzeroberfläche mit Masterseiten und Teilausführungen

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 7 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 7 untersucht, wie wir das "DRY-Prinzip" in unseren Ansichtsvorlagen anwenden können, um Codeduplizierungen mithilfe von Partizipationsvorlagen und Masterseiten zu vermeiden.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner Schritt 7: Partials und MasterPages

Eine der Designphilosophien, die ASP.NET MVC umfasst, ist das "Do Not Repeat Yourself"-Prinzip (gemeinhin als "DRY" bezeichnet). Ein DRY-Design hilft, die Duplizierung von Code und Logik zu beseitigen, wodurch Anwendungen letztendlich schneller zu erstellen und einfacher zu warten sind.

Wir haben bereits gesehen, dass das DRY-Prinzip in mehreren unserer NerdDinner-Szenarien angewendet wurde. Einige Beispiele: Unsere Validierungslogik ist in unserer Modellschicht implementiert, wodurch sie sowohl in der Bearbeitung als auch in der Erstellung von Szenarien in unserem Controller erzwungen werden kann. Wir verwenden die Ansichtsvorlage "NotFound" über die Aktionsmethoden Bearbeiten, Details und Löschen wieder; Wir verwenden ein Konventionsbenennungsmuster mit unseren Ansichtsvorlagen, das es überflüssig macht, den Namen explizit anzugeben, wenn wir die View()-Hilfsmethode aufrufen. und wir verwenden die DinnerFormViewModel-Klasse sowohl für Edit- als auch Create-Aktionsszenarien wieder.

Sehen wir uns nun an, wie wir das "DRY-Prinzip" in unseren Ansichtsvorlagen anwenden können, um auch dort Codeduplizierungen zu vermeiden.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Erneutes Besuchen unserer Vorlagen zum Bearbeiten und Erstellen von Ansichtsvorlagen

Derzeit verwenden wir zwei verschiedene Ansichtsvorlagen – "Edit.aspx" und "Create.aspx" – um unsere Menü-Formular-Benutzeroberfläche anzuzeigen. Ein kurzer visueller Vergleich zeigt, wie ähnlich sie sind. Im Folgenden sieht das Formular zum Erstellen aus:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

Und so sieht unser "Bearbeiten"-Formular aus:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Es gibt nicht viel unterschiedslos? Abgesehen von Titel- und Kopfzeilentext sind das Formularlayout und die Eingabesteuerelemente identisch.

Wenn wir die Ansichtsvorlagen "Edit.aspx" und "Create.aspx" öffnen, werden wir feststellen, dass sie identisches Formularlayout und Eingabesteuerungscode enthalten. Diese Duplizierung bedeutet, dass wir am Ende zweimal Änderungen vornehmen müssen, wenn wir eine neue Dinner-Eigenschaft einführen oder ändern - was nicht gut ist.

### <a name="using-partial-view-templates"></a>Verwenden von Partiellen Ansichtsvorlagen

ASP.NET MVC unterstützt die Möglichkeit, "Teilansichtsvorlagen" zu definieren, die zum Einkapseln der Ansichtsrenderinglogik für einen Teilbereich einer Seite verwendet werden können. "Partials" bieten eine nützliche Möglichkeit, die Ansichtsrenderinglogik einmal zu definieren und sie dann an mehreren Stellen in einer Anwendung wiederzuverwenden.

Um "DRY-up" unserer Bearbeitungsvorlage Edit.aspx und Create.aspx zu unterstützen, können wir eine partielle Ansichtsvorlage mit dem Namen "DinnerForm.ascx" erstellen, die das Formularlayout und die Eingabeelemente, die beiden gemeinsam sind, kapselt. Wir tun dies, indem wir mit der rechten Maustaste auf unser&gt;Verzeichnis /Views/Dinners klicken und den Menübefehl "Ansicht hinzufügen" auswählen:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

Dadurch wird das Dialogfeld "Ansicht hinzufügen" angezeigt. Wir nennen die neue Ansicht, die wir erstellen möchten, aktivieren das Kontrollkästchen "Eine Teilansicht erstellen" im Dialogfeld und geben an, dass wir ihr eine DinnerFormViewModel-Klasse übergeben:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, erstellt Visual Studio eine neue Ansichtsvorlage "DinnerForm.ascx" für uns im Verzeichnis "-Ansichten".

Wir können dann das doppelte Formularlayout / den Eingabesteuerungscode aus unseren Ansichtsvorlagen Edit.aspx/ Create.aspx in unsere neue "DinnerForm.ascx"-Teilansichtsvorlage kopieren/einfügen:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Anschließend können wir unsere Vorlagen für Die Bearbeitung und Erstellung von Ansichtsvorlagen aktualisieren, um die DinnerForm-Teilvorlage aufzurufen und die Formularduplizierung zu beseitigen. Wir können dies tun, indem wir Html.RenderPartial("DinnerForm") in unseren Ansichtsvorlagen aufrufen:

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Sie können den Pfad der gewünschten Teilvorlage beim Aufrufen von Html.RenderPartial explizit qualifizieren (z. B. "Views/Dinners/DinnerForm.ascx"). In unserem obigen Code nutzen wir jedoch das konventionsbasierte Namensmuster innerhalb ASP.NET MVC und geben einfach "DinnerForm" als Namen des zu rendernden Teils an. Wenn wir dies tun, wird ASP.NET MVC zuerst im konventionsbasierten Views-Verzeichnis suchen (für DinnersController wäre dies /Views/Dinners). Wenn die Teilvorlage dort nicht gefunden wird, wird sie im Verzeichnis /Views/Shared nach ihr suchen.

Wenn Html.RenderPartial() nur mit dem Namen der Teilansicht aufgerufen wird, wird ASP.NET MVC an die Teilansicht die gleichen Model- und ViewData-Wörterbuchobjekte übergeben, die von der aufrufenden Ansichtsvorlage verwendet werden. Alternativ gibt es überladene Versionen von Html.RenderPartial(), mit denen Sie ein alternatives Model-Objekt und/oder ViewData-Wörterbuch für die zu verwendende Teilansicht übergeben können. Dies ist nützlich für Szenarien, in denen Sie nur eine Teilmenge des vollständigen Modell/ViewModel übergeben möchten.

| **Nebenthema: &lt;Warum&gt; % &lt;statt %= %&gt;?** |
| --- |
| Eines der subtilen Dinge, die Sie mit dem obigen Code bemerkt &lt;haben,&gt; ist, dass wir beim Aufrufen von Html.RenderPartial(einen &lt;%%%-Block&gt; anstelle eines %= %%-Blocks verwenden. &lt;%=&gt; %-Blöcke in ASP.NET geben an, dass ein &lt;Entwickler einen angegebenen&gt; Wert rendern möchte (z. B. %= "Hello" % würde "Hello" rendern). &lt;%&gt; %-Blöcke geben stattdessen an, dass der Entwickler Code ausführen möchte und dass &lt;jede gerenderte Ausgabe in&gt;ihnen explizit ausgeführt werden muss (z. B. % Response.Write("Hello") % . Der Grund, warum &lt;wir&gt; einen %%-Block mit unserem html.RenderPartial-Code oben verwenden, ist, dass die Html.RenderPartial()-Methode keine Zeichenfolge zurückgibt und stattdessen den Inhalt direkt an den Ausgabestream der aufrufenden Ansichtsvorlage ausgibt. Dies geschieht aus Gründen der Leistungseffizienz und vermeidet dadurch die Notwendigkeit, ein (potenziell sehr großes) temporäres Zeichenfolgenobjekt zu erstellen. Dies reduziert die Speicherauslastung und verbessert den gesamten Anwendungsdurchsatz. Ein häufiger Fehler bei der Verwendung von Html.RenderPartial() besteht darin, zu vergessen, &lt;ein&gt; Semikolon am Ende des Aufrufs hinzuzufügen, wenn es sich innerhalb eines % %-Blocks befindet. Dieser Code verursacht z. B. &lt;einen Compilerfehler: % Html.RenderPartial("DinnerForm") %&gt; Sie müssen stattdessen schreiben: &lt;% Html.RenderPartial("DinnerForm"); %&gt; Dies &lt;liegt&gt; daran, dass %%-Blöcke eigenständige Codeanweisungen sind und bei Verwendung von Codeanweisungen mit einem Semikolon beendet werden müssen. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Verwenden von Partiellen Ansichtsvorlagen zum Verdeutlichen von Code

Wir haben die Partielle Ansichtsvorlage "DinnerForm" erstellt, um zu vermeiden, dass die Logik des Renderns von Ansicht an mehreren Stellen dupliziert wird. Dies ist der häufigste Grund zum Erstellen von Partiellenansichtsvorlagen.

Manchmal ist es immer noch sinnvoll, Partielle Ansichten zu erstellen, auch wenn sie nur an einem einzigen Ort aufgerufen werden. Sehr komplizierte Ansichtsvorlagen können oft viel einfacher zu lesen sein, wenn ihre Ansichtsrenderinglogik extrahiert und in eine oder mehrere gut benannte Teilvorlagen partitioniert wird.

Betrachten Sie z. B. den folgenden Codeausschnitt aus der Site.master-Datei in unserem Projekt (den wir uns in Kürze ansehen werden). Der Code ist relativ geradlinig zu lesen – auch weil die Logik zum Anzeigen eines Login-/Logout-Links oben rechts auf dem Bildschirm im "LogOnUserControl"-Teil gekapselt ist:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Wenn Sie verwirrt sind, wenn Sie versuchen, das HTML/Code-Markup in einer Ansichtsvorlage zu verstehen, sollten Sie überlegen, ob es nicht klarer wäre, wenn ein Teil davon extrahiert und in gut benannte Teilansichten umgestaltet würde.

### <a name="master-pages"></a>Masterseiten

Neben der Unterstützung von Teilansichten unterstützt ASP.NET MVC auch die Möglichkeit, "Masterpage"-Vorlagen zu erstellen, die verwendet werden können, um das gemeinsame Layout und html der obersten Ebene einer Website zu definieren. Inhaltsplatzhaltersteuerelemente können dann zur Masterseite hinzugefügt werden, um ersetzbare Bereiche zu identifizieren, die durch Ansichten überschrieben oder "ausgefüllt" werden können. Dies bietet eine sehr effektive (und DRY) Möglichkeit, ein gemeinsames Layout in einer Anwendung anzuwenden.

Standardmäßig wird in neuen ASP.NET MVC-Projekten automatisch eine Masterseitenvorlage hinzugefügt. Diese Masterseite trägt den Namen "Site.master" und befindet sich im Ordner "Ansichten" und "Gemeinsam":

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

Die Standarddatei Site.master sieht wie folgt aus. Es definiert die äußere HTML der Website, zusammen mit einem Menü für die Navigation an der Spitze. Es enthält zwei austauschbare Inhaltsplatzhaltersteuerelemente – eines für den Titel und das andere, bei dem der primäre Inhalt einer Seite ersetzt werden soll:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

Alle Ansichtsvorlagen, die wir für unsere NerdDinner-Anwendung erstellt haben ("Liste", "Details", "Bearbeiten", "Erstellen", "NotFound", usw.), basieren auf dieser Site.master-Vorlage. Dies wird über das Attribut "MasterPageFile" angezeigt, &lt;das standardmäßig&gt; der obersten % -Seite %-Direktive hinzugefügt wurde, als wir unsere Ansichten mit dem Dialogfeld "Ansicht hinzufügen" erstellt haben:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

Dies bedeutet, dass wir den Site.master-Inhalt ändern und die Änderungen automatisch anwenden und verwenden können, wenn wir eine unserer Ansichtsvorlagen rendern.

Lassen Sie uns unseren Site.master-Header-Bereich aktualisieren, so dass der Header unserer Anwendung "NerdDinner" anstelle von "Meine MVC-Anwendung" ist. Lassen Sie uns auch unser Navigationsmenü aktualisieren, so dass die erste Registerkarte "Find a Dinner" ist (von der HomeController Index() Aktionsmethode behandelt), und fügen wir eine neue Registerkarte namens "Host a Dinner" hinzu (behandelt von der Create()-Aktionsmethode des DinnersControllers):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Wenn wir die Site.master-Datei speichern und unseren Browser aktualisieren, werden unsere Header-Änderungen in allen Ansichten in unserer Anwendung angezeigt. Beispiel:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

Und mit der *URL /Dinners/Edit/[id]:*

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Nächster Schritt

Teile- und Masterseiten bieten sehr flexible Optionen, mit denen Sie Ansichten sauber organisieren können. Sie werden feststellen, dass sie Ihnen helfen, das Duplizieren von Ansichtsinhalt/-Code zu vermeiden und Ihre Ansichtsvorlagen einfacher zu lesen und zu verwalten.

Sehen wir uns nun das zuvor erstellte Listingszenario noch einmal an und ermöglichen skalierbare Paging-Unterstützung.

> [!div class="step-by-step"]
> [Zurück](use-viewdata-and-implement-viewmodel-classes.md)
> [Weiter](implement-efficient-data-paging.md)
