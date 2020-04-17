---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData verwenden und ViewModel-Klassen implementieren | Microsoft Docs
author: rick-anderson
description: Schritt 6 zeigt, wie die Unterstützung für umfangreichere Formularbearbeitungsszenarien aktiviert wird, und es werden auch zwei Ansätze erläutert, die zum Übergeben von Daten von Controllern an Ansichten verwendet werden können:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541103"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>Verwenden von ViewData und Implementieren von ViewModel-Klassen

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 6 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 6 zeigt, wie die Unterstützung für umfangreichere Formularbearbeitungsszenarien aktiviert wird, und es werden auch zwei Ansätze erläutert, die zum Übergeben von Daten von Controllern an Ansichten verwendet werden können: ViewData und ViewModel.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner Schritt 6: ViewData und ViewModel

Wir haben eine Reihe von Formular-Post-Szenarien behandelt und erläutert, wie die CRUD-Unterstützung (Create, Update and Delete) implementiert wird. Wir gehen nun mit unserer DinnersController-Implementierung weiter und ermöglichen die Unterstützung für umfangreichere Formularbearbeitungsszenarien. Dabei werden zwei Ansätze erläutert, mit denen Daten von Controllern an Ansichten übergeben werden können: ViewData und ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Übergeben von Daten von Controllern an View-Templates

Eines der bestimmenden Merkmale des MVC-Musters ist die strikte "Trennung von Bedenken", die es zwischen den verschiedenen Komponenten einer Anwendung erzwingen hilft. Modelle, Controller und Ansichten haben jeweils klar definierte Rollen und Verantwortlichkeiten und kommunizieren auf genau definierte Weise miteinander. Dies trägt zur Förderung der Testbarkeit und der Wiederverwendung von Code bei.

Wenn eine Controller-Klasse beschließt, eine HTML-Antwort an einen Client zurückzugeben, ist sie dafür verantwortlich, alle Daten, die zum Rendern der Antwort erforderlich sind, explizit an die Ansichtsvorlage zu übergeben. Ansichtsvorlagen sollten niemals Datenabruf oder Anwendungslogik ausführen – und sich stattdessen darauf beschränken, nur Rendercode zu haben, der aus dem Modell/den Daten gesteuert wird, die vom Controller an ihn übergeben werden.

Im Moment sind die Modelldaten, die von unserer DinnersController-Klasse an unsere Ansichtsvorlagen übergeben werden, einfach und geradlinig – eine Liste der Dinner-Objekte im Fall von Index() und ein einzelnes Dinner-Objekt im Fall von Details(), Edit(), Create() und Delete(). Da wir unserer Anwendung mehr UI-Funktionen hinzufügen, müssen wir häufig mehr als nur diese Daten übergeben, um HTML-Antworten in unseren Ansichtsvorlagen zu rendern. Beispielsweise können wir das Feld "Land" in unseren Ansichten bearbeiten und erstellen von einem HTML-Textfeld in eine Dropdownliste ändern. Anstatt die Dropdown-Liste der Ländernamen in der Ansichtsvorlage hart zu codieren, möchten wir sie möglicherweise aus einer Liste unterstützter Länder generieren, die wir dynamisch auffüllen. Wir benötigen eine Möglichkeit, sowohl *and* das Dinner-Objekt als auch die Liste der unterstützten Länder von unserem Controller zu unseren Ansichtsvorlagen zu übergeben.

Schauen wir uns zwei Möglichkeiten an, wie wir dies erreichen können.

### <a name="using-the-viewdata-dictionary"></a>Verwenden des ViewData-Wörterbuchs

Die Controller-Basisklasse macht eine "ViewData"-Wörterbucheigenschaft verfügbar, die zum Übergeben zusätzlicher Datenelemente von Controllern an Ansichten verwendet werden kann.

Um beispielsweise das Szenario zu unterstützen, in dem wir das Textfeld "Land" in unserer Bearbeitungsansicht von einem HTML-Textfeld in eine Dropdownliste ändern möchten, können wir unsere Edit()-Aktionsmethode aktualisieren, um (zusätzlich zu einem Dinner-Objekt) ein SelectList-Objekt zu übergeben, das als Modell einer Länder-Dropdownliste verwendet werden kann.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

Der Konstruktor der SelectList oben akzeptiert eine Liste der Landkreise, mit der die Dropdownliste sowie der aktuell ausgewählte Wert aufgepopt werden sollen.

Wir können dann unsere Edit.aspx-Ansichtsvorlage aktualisieren, um die Html.DropDownList()-Hilfsmethode anstelle der zuvor verwendeten Html.TextBox()-Hilfsmethode zu verwenden:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

Die obige Html.DropDownList()-Hilfsmethode nimmt zwei Parameter an. Der erste ist der Name des html-Formularelements, das ausgegeben werden soll. Das zweite ist das "SelectList"-Modell, das wir über das ViewData-Wörterbuch übergeben haben. Wir verwenden das Schlüsselwort "als" von C, um den Typ innerhalb des Wörterbuchs als SelectList zu umschreiben.

Und jetzt, wenn wir unsere Anwendung ausführen und auf die */Dinners/Edit/1* URL in unserem Browser zugreifen, werden wir sehen, dass unsere Bearbeitungsbenutzeroberfläche aktualisiert wurde, um eine Dropdownliste von Ländern anstelle eines Textfeldes anzuzeigen:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

Da wir auch die Vorlage für die Ansicht bearbeiten aus der HTTP-POST-Edit-Methode rendern (in Szenarien, in denen Fehler auftreten), sollten wir sicherstellen, dass wir diese Methode auch aktualisieren, um ViewData die SelectList hinzuzufügen, wenn die Ansichtsvorlage in Fehlerszenarien gerendert wird:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

Und jetzt unterstützt unser DinnersController-Bearbeitungsszenario eine DropDownList.

### <a name="using-a-viewmodel-pattern"></a>Verwenden eines ViewModel-Musters

Der ViewData-Wörterbuchansatz hat den Vorteil, dass er ziemlich schnell und einfach zu implementieren ist. Einige Entwickler verwenden jedoch keine zeichenfolgenbasierten Wörterbücher, da Tippfehler zu Fehlern führen können, die zur Kompilierungszeit nicht abgefangen werden. Das nicht typisierte ViewData-Wörterbuch erfordert auch die Verwendung des Operators "as" oder die Umwandlung, wenn in einer Ansichtsvorlage eine stark typisierte Sprache wie C- verwendet wird.

Ein alternativer Ansatz, den wir verwenden könnten, ist ein Muster, das oft als "ViewModel"-Muster bezeichnet wird. Bei Verwendung dieses Musters erstellen wir stark typisierte Klassen, die für unsere spezifischen Ansichtsszenarien optimiert sind und Eigenschaften für die dynamischen Werte/Inhalte verfügbar machen, die von unseren Ansichtsvorlagen benötigt werden. Unsere Controllerklassen können diese ansichtsoptimierten Klassen dann auffüllen und an unsere Ansichtsvorlage übergeben. Dies ermöglicht Typsicherheit, Kompilierungszeitprüfung und Editor-Intellisense in Ansichtsvorlagen.

Um z. B. Szenarios für die Bearbeitung von Abendessenzusen zu aktivieren, können wir eine "DinnerFormViewModel"-Klasse wie unten erstellen, die zwei stark typisierte Eigenschaften verfügbar macht: ein Dinner-Objekt und das SelectList-Modell, das zum Auffüllen der Länder-Dropdownliste erforderlich ist:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Wir können dann unsere Edit()-Aktionsmethode aktualisieren, um das DinnerFormViewModel mit dem Dinner-Objekt zu erstellen, das wir aus unserem Repository abrufen, und es dann an unsere Ansichtsvorlage übergeben:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Anschließend aktualisieren wir unsere Ansichtsvorlage, sodass ein "DinnerFormViewModel" anstelle eines "Dinner"-Objekts erwartet wird, indem das Attribut "erbt" oben auf der edit.aspx-Seite wie folgt geändert wird:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Sobald wir dies tun, wird der Intellekt der "Model"-Eigenschaft in unserer Ansichtsvorlage aktualisiert, um das Objektmodell des DinnerFormViewModel-Typs widerzuspiegeln, den wir übergeben:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Wir können dann unseren Ansichtscode aktualisieren, um ihn abzuarbeiten. Beachten Sie unten, wie wir die Namen der Eingabeelemente, die wir erstellen, nicht ändern (die Formularelemente werden immer noch "Titel", "Land") genannt, aber wir aktualisieren die HTML-Hilfsmethoden, um die Werte mithilfe der DinnerFormViewModel-Klasse abzurufen:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Wir aktualisieren auch unsere Edit-Post-Methode, um die DinnerFormViewModel-Klasse beim Rendern von Fehlern zu verwenden:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Wir können auch unsere Create()-Aktionsmethoden aktualisieren, um genau die gleiche *DinnerFormViewModel-Klasse* wiederzuverwenden, um die Länder DropDownList auch innerhalb dieser zu aktivieren. Im Folgenden finden Sie die HTTP-GET-Implementierung:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

Im Folgenden finden Sie die Implementierung der HTTP-POST Create-Methode:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

Und jetzt unterstützen unsere Bildschirme "Bearbeiten" und "Erstellen" Dropdownlisten für die Auswahl des Landes.

### <a name="custom-shaped-viewmodel-classes"></a>Benutzerdefinierte ViewModel-Klassen

Im obigen Szenario macht unsere DinnerFormViewModel-Klasse das Dinner-Modellobjekt direkt als Eigenschaft verfügbar, zusammen mit einer unterstützenden SelectList-Modelleigenschaft. Dieser Ansatz funktioniert gut für Szenarien, in denen die HTML-Benutzeroberfläche, die wir in unserer Ansichtsvorlage erstellen möchten, relativ nahe an unseren Domänenmodellobjekten entspricht.

In Szenarien, in denen dies nicht der Fall ist, können Sie eine Option verwenden, die Sie verwenden können, um eine benutzerdefinierte ViewModel-Klasse zu erstellen, deren Objektmodell für den Verbrauch durch die Ansicht optimiert ist – und die sich möglicherweise völlig vom zugrunde liegenden Domänenmodellobjekt unterscheidet. Beispielsweise können möglicherweise verschiedene Eigenschaftsnamen und/oder aggregierte Eigenschaften verfügbar gemacht werden, die von mehreren Modellobjekten erfasst wurden.

Benutzerdefinierte ViewModel-Klassen können sowohl zum Übergeben von Daten von Controllern an zu rendernde Ansichten als auch zum Verarbeiten von Formulardaten verwendet werden, die an die Aktionsmethode eines Controllers zurückgesendet werden. Für dieses spätere Szenario kann die Aktionsmethode ein ViewModel-Objekt mit den formulargeposteten Daten aktualisieren und dann die ViewModel-Instanz verwenden, um ein tatsächliches Domänenmodellobjekt zuzuordnen oder abzurufen.

Benutzerdefinierte ViewModel-Klassen können eine große Flexibilität bieten und sind bei jeder Suche nach dem Renderingcode in Ihren Ansichtsvorlagen oder dem Formularbuchungscode in Ihren Aktionsmethoden zu kompliziert. Dies ist häufig ein Zeichen dafür, dass Ihre Domänenmodelle nicht sauber mit der benutzeroberfläche übereinstimmen, die Sie generieren, und dass eine benutzerdefinierte Zwischenklasse viewModel helfen kann.

### <a name="next-step"></a>Nächster Schritt

Sehen wir uns nun an, wie wir Teile und Masterseiten verwenden können, um die Benutzeroberfläche in unserer Anwendung wiederzuverwenden und gemeinsam zu nutzen.

> [!div class="step-by-step"]
> [Zurück](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [Weiter](re-use-ui-using-master-pages-and-partials.md)
