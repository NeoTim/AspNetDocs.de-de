---
uid: mvc/overview/getting-started/introduction/adding-search
title: Suchen | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211473"
---
# <a name="search"></a>Suchen,

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a>Hinzufügen einer Suchmethode und einer Such Ansicht

In diesem Abschnitt fügen Sie der Aktionsmethode Suchfunktionen hinzu `Index` , mit denen Sie Filme nach Genre oder Name durchsuchen können.

## <a name="prerequisites"></a>Voraussetzungen

Um den Screenshots dieses Abschnitts zu entsprechen, müssen Sie die Anwendung (F5) ausführen und der-Datenbank die folgenden Filme hinzufügen.

| Titel | Veröffentlichungsdatum | Genre | Preis |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | Di | 6,99 |
| Ghostbusters II | 6/16/1989 | Di | 6,99 |
| Planet der Affen | 3/27/1986 | Aktion | 5,99 |

## <a name="updating-the-index-form"></a>Aktualisieren des Index Formulars

Aktualisieren Sie zunächst die- `Index` Aktionsmethode auf die vorhandene- `MoviesController` Klasse. Der Code lautet wie folgt:

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

In der ersten Zeile der- `Index` Methode wird die folgende [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfrage erstellt, um die Filme auszuwählen:

[!code-csharp[Main](adding-search/samples/sample2.cs)]

Die Abfrage wird an dieser Stelle definiert, aber noch nicht für die Datenbank ausgeführt.

Wenn der- `searchString` Parameter eine Zeichenfolge enthält, wird die Film Abfrage so geändert, dass nach dem Wert der Such Zeichenfolge gefiltert wird, indem der folgende Code verwendet wird:

[!code-csharp[Main](adding-search/samples/sample3.cs)]

Der Code `s => s.Title` oben ist ein [Lambdaausdruck](https://msdn.microsoft.com/library/bb397687.aspx). Lambdas werden in Methoden basierten [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfragen als Argumente für Standard Abfrage Operator-Methoden wie z. b. die [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) -Methode verwendet, die im obigen Code verwendet wird. LINQ-Abfragen werden nicht ausgeführt, wenn Sie definiert oder durch Aufrufen einer Methode wie oder geändert werden `Where` `OrderBy` . Stattdessen wird die Abfrage Ausführung verzögert. Dies bedeutet, dass die Auswertung eines Ausdrucks verzögert wird, bis der erkannte Wert tatsächlich durchlaufen oder die- [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) Methode aufgerufen wird. Im `Search` Beispiel wird die Abfrage in der *Index. cshtml* -Ansicht ausgeführt. Weitere Informationen zur verzögerten Abfrageausführung finden Sie unter [Abfrageausführung](https://msdn.microsoft.com/library/bb738633.aspx).

> [!NOTE]
> Die [enthält](https://msdn.microsoft.com/library/bb155125.aspx) -Methode wird für die Datenbank ausgeführt, nicht für den obigen c#-Code. In der-Datenbank [sind](https://msdn.microsoft.com/library/bb155125.aspx) SQL-Tabellen [ähnlich](https://msdn.microsoft.com/library/ms179859.aspx), bei denen die Groß-/Kleinschreibung nicht beachtet wird.

Nun können Sie die `Index` Ansicht aktualisieren, in der das Formular für den Benutzer angezeigt wird.

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/Index*. Fügen Sie eine Abfragezeichenfolge wie `?searchString=ghost` an die URL an. Die gefilterten Filme werden angezeigt.

![Searchqrystr](adding-search/_static/image1.png)

Wenn Sie die Signatur der `Index` Methode so ändern, dass Sie einen Parameter mit dem Namen hat `id` , `id` entspricht der Parameter dem `{id}` Platzhalter für die Standardrouten, die in der Datei *App \_ start\routeconfig.cs* festgelegt sind.

[!code-json[Main](adding-search/samples/sample4.json)]

Die ursprüngliche `Index` Methode sieht wie folgt aus:

[!code-csharp[Main](adding-search/samples/sample5.cs)]

Die geänderte `Index` Methode sieht wie folgt aus:

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

Sie können nun den Suchtitel als Routendaten (ein URL-Segment) anstatt als Wert einer Abfragezeichenfolge übergeben.

![](adding-search/_static/image2.png)

Sie können jedoch von den Benutzern nicht erwarten, dass sie jedes Mal die URL ändern, wenn sie nach einem Film suchen möchten. Deshalb fügen Sie nun eine Benutzeroberflächenoption zum besseren Filtern von Filmen hinzu. Wenn Sie die Signatur der- `Index` Methode geändert haben, um zu testen, wie der Routen gebundene ID-Parameter übergeben wird, ändern Sie ihn so, dass die- `Index` Methode einen Zeichen folgen Parameter namens annimmt `searchString` :

[!code-csharp[Main](adding-search/samples/sample7.cs)]

Öffnen Sie die Datei " *views\movies\index.cshtml* ", und `@Html.ActionLink("Create New", "Create")` fügen Sie direkt nach das unten markierte Formular Markup hinzu:

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

Das-Hilfsprogramm `Html.BeginForm` erstellt ein öffnendes- `<form>` Tag. Das Hilfsprogramm bewirkt, dass `Html.BeginForm` das Formular in sich selbst gepostet wird, wenn der Benutzer das Formular durch Klicken auf die Schaltfläche **Filter** übermittelt.

Beim Anzeigen und Bearbeiten von Ansichts Dateien hat Visual Studio 2013 eine gute Verbesserung. Wenn Sie die Anwendung mit einer geöffneten Ansichts Datei ausführen, ruft Visual Studio 2013 die richtige Controller Aktionsmethode auf, um die Ansicht anzuzeigen.

![](adding-search/_static/image3.png)

Wenn die Index Ansicht in Visual Studio geöffnet ist (wie in der Abbildung oben gezeigt), tippen Sie auf CTR F5 oder F5, um die Anwendung auszuführen, und versuchen Sie dann, nach einem Film zu suchen.

![](adding-search/_static/image4.png)

Es gibt keine Überladung der- `HttpPost` `Index` Methode. Sie benötigen Sie nicht, da die Methode den Zustand der Anwendung nicht ändert, sondern nur das Filtern von Daten.

Sie können die folgende `HttpPost Index`-Methode hinzufügen. In diesem Fall würde der Aktions Aufruf mit der `HttpPost Index` -Methode verglichen, und die- `HttpPost Index` Methode würde wie in der folgenden Abbildung dargestellt ausgeführt werden.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![Searchpostghost](adding-search/_static/image5.png)

Doch selbst wenn Sie diese `HttpPost`-Version der `Index`-Methode hinzufügen, gibt es eine Einschränkung für die gesamte Implementierung. Stellen Sie sich vor, Sie möchten eine bestimmte Suche als Favorit speichern oder einen Link an Freunde senden, auf den diese klicken können, um dieselbe gefilterte Liste von Filmen anzuzeigen. Beachten Sie, dass die URL für die HTTP POST-Anforderung mit der URL für die Get-Anforderung übereinstimmt ("localhost: xxxxx/Movies/Index"). es sind keine Suchinformationen in der URL selbst vorhanden. Derzeit werden die Such Zeichenfolgen-Informationen als Formular Feldwert an den Server gesendet. Dies bedeutet, dass Sie diese Suchinformationen nicht in einem Lesezeichen erfassen oder an Freunde in einer URL senden können.

Die Lösung besteht darin, eine Überladung von zu verwenden `BeginForm` , die angibt, dass die Post-Anforderung die Suchinformationen der URL hinzufügen soll und dass Sie an die `HttpGet` Version der Methode weitergeleitet werden soll `Index` . Ersetzen Sie die vorhandene Parameter lose- `BeginForm` Methode durch das folgende Markup:

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

Wenn Sie nun eine Suche übermitteln, enthält die URL eine Suchabfrage Zeichenfolge. Das Suchen wird auch an Aktionsmethode `HttpGet Index` übertragen, auch wenn Sie eine `HttpPost Index`-Methode haben.

![Indexwithgeturl](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>Hinzufügen der Suche nach Genre

Wenn Sie die `HttpPost` Version der-Methode hinzugefügt `Index` haben, löschen Sie Sie jetzt.

Als Nächstes fügen Sie eine Funktion hinzu, um Benutzern das Suchen nach Filmen nach Genre zu ermöglichen. Ersetzen Sie die `Index`-Methode durch den folgenden Code:

[!code-csharp[Main](adding-search/samples/sample11.cs)]

Diese Version der- `Index` Methode nimmt einen zusätzlichen Parameter, nämlich, auf `movieGenre` . In den ersten Codezeilen wird ein- `List` Objekt erstellt, um Movie-Genres aus der Datenbank zu speichern.

Der folgende Code ist eine LINQ-Abfrage, die alle Genres aus der Datenbank abruft.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

Der Code verwendet die- `AddRange` Methode der generischen- `List` Auflistung, um alle eindeutigen Genres der Liste hinzuzufügen. (Ohne den- `Distinct` Modifizierer würden doppelte Genres hinzugefügt werden – beispielsweise würde die-Komödie in unserem Beispiel zweimal hinzugefügt werden.) Der Code speichert dann die Liste der Genres im- `ViewBag.MovieGenre` Objekt. Das Speichern von Kategorieinformationen (z. b. Filmgenres) als [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) -Objekt in einem `ViewBag` und der anschließende Zugriff auf die Kategoriedaten in einem Dropdown-Listenfeld ist ein typischer Ansatz für MVC-Anwendungen.

Der folgende Code zeigt, wie Sie den-Parameter überprüfen `movieGenre` . Wenn Sie nicht leer ist, schränkt der Code die Film Abfrage weiter ein, um die ausgewählten Filme auf das angegebene Genre zu beschränken.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

Wie bereits erwähnt, wird die Abfrage nicht in der Datenbank ausgeführt, bis die Filmliste durchlaufen wird (was in der Ansicht geschieht, nachdem die `Index` Aktionsmethode zurückgegeben wurde).

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>Hinzufügen von Markup zur Index Ansicht zur Unterstützung der Suche nach Genre

Fügen Sie `Html.DropDownList` der Datei " *views\movies\index.cshtml* " direkt vor dem Hilfsprogramm ein Hilfsobjekt hinzu `TextBox` . Das vollständige Markup ist unten dargestellt:

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

Im folgenden Code wird Folgendes ausgeführt:

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

Der Parameter "muviegenre" stellt den Schlüssel für das Hilfsprogramm bereit `DropDownList` , in dem ein gesucht werden soll `IEnumerable<SelectListItem>` `ViewBag` . Der `ViewBag` wurde in der Aktionsmethode aufgefüllt:

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

Der Parameter "All" stellt eine Options Bezeichnung bereit. Wenn Sie diese Auswahl in Ihrem Browser überprüfen, sehen Sie, dass das Attribut "Value" leer ist. Da der Controller nur filtert `if` , dass die Zeichenfolge nicht `null` oder leer ist, wird bei der Übermittlung eines leeren Werts für `movieGenre` Alle Genres angezeigt.

Sie können auch festlegen, dass eine Option standardmäßig ausgewählt ist. Wenn Sie "Comedy" als Standardoption wünschen, ändern Sie den Code im Controller wie folgt:

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/Index*. Probieren Sie eine Suche nach Genre, nach Film Name und nach beiden Kriterien aus.

![](adding-search/_static/image8.png)

In diesem Abschnitt haben Sie eine Such Aktionsmethode und-Ansicht erstellt, mit der Benutzer nach Film Titel und Genre suchen können. Im nächsten Abschnitt erfahren Sie, wie Sie dem Modell eine Eigenschaft hinzufügen `Movie` und wie Sie einen Initialisierer hinzufügen, mit dem automatisch eine Testdatenbank erstellt wird.

> [!div class="step-by-step"]
> [Zurück](examining-the-edit-methods-and-edit-view.md)
> [Weiter](adding-a-new-field.md)
