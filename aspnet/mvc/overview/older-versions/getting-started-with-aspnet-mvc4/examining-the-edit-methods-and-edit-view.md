---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: Untersuchen der Bearbeitungsmethoden und Bearbeiten der Ansicht | Microsoft-Dokumentation
author: Rick-Anderson
description: 'Hinweis: eine aktualisierte Version dieses Tutorials ist hier verfügbar, die ASP.NET MVC 5 und Visual Studio 2013 verwendet. Es ist sicherer, aber viel einfacher zu befolgen und zu demonstrieren...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163000"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Überprüfen der Edit-Methoden und -Ansicht

von [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Eine aktualisierte Version dieses Tutorials ist [hier](../../getting-started/introduction/getting-started.md) verfügbar, die ASP.NET MVC 5 und Visual Studio 2013 verwendet. Es ist sicherer, ist viel einfacher zu befolgen und zeigt mehr Features.

In diesem Abschnitt untersuchen Sie die generierten Aktionsmethoden und-Sichten für den Film Controller. Anschließend fügen Sie eine benutzerdefinierte Suchseite hinzu.

Führen Sie die Anwendung aus, und navigieren Sie zum `Movies` Controller, indem Sie */Movies* an die URL in der Adressleiste Ihres Browsers anhängen. Halten Sie den Mauszeiger auf einen **Bearbeitungs** Link, um die URL anzuzeigen, mit der er verknüpft ist.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Der **Bearbeitungs** Link wurde von der- `Html.ActionLink` Methode in der Ansicht *views\movies\index.cshtml* generiert:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![HTML. Action Link](examining-the-edit-methods-and-edit-view/_static/image2.png)

Das `Html` -Objekt ist ein Hilfsprogramm, das über eine Eigenschaft der [System. Web. MVC. webviewpage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) -Basisklasse verfügbar gemacht wird. Die-Methode des-Hilfsprogramms `ActionLink` erleichtert das dynamische Generieren von HTML-Hyperlinks, die mit Aktionsmethoden auf Controllern verknüpft sind. Das erste Argument für die- `ActionLink` Methode ist der zu Rendering-Linktext (z `<a>Edit Me</a>` . b.). Das zweite Argument ist der Name der aufzurufenden Aktionsmethode. Das abschließende Argument ist ein [Anonymes Objekt](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , das die Routendaten generiert (in diesem Fall die ID 4).

Der generierte Link, der in der vorherigen Abbildung angezeigt wird, ist `http://localhost:xxxxx/Movies/Edit/4` . Die Standardroute (festgelegt in *App \_ start\routeconfig.cs*) übernimmt das URL-Muster `{controller}/{action}/{id}` . Daher übersetzt ASP.net `http://localhost:xxxxx/Movies/Edit/4` in eine Anforderung an die `Edit` Aktionsmethode des Controllers, `Movies` wobei der-Parameter `ID` gleich 4 ist. Überprüfen Sie den folgenden Code in der Datei " * \_ start\routeconfig.cs* " der app.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Sie können auch Aktionsmethoden Parameter mithilfe einer Abfrage Zeichenfolge übergeben. Beispielsweise übergibt die URL `http://localhost:xxxxx/Movies/Edit?ID=4` auch den-Parameter `ID` von 4 an die `Edit` Aktionsmethode des `Movies` Controllers.

![Editquerystring](examining-the-edit-methods-and-edit-view/_static/image3.png)

Öffnen Sie den `Movies` Controller. Die zwei `Edit` Aktionsmethoden sind unten dargestellt.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

Beachten Sie, dass der zweiten `Edit`-Aktionsmethode das `HttpPost`-Attribut vorangestellt ist. Dieses Attribut gibt an, dass die Überladung der- `Edit` Methode nur für Post-Anforderungen aufgerufen werden kann. Sie können das `HttpGet` -Attribut auf die erste Bearbeitungsmethode anwenden, dies ist jedoch nicht notwendig, da es sich hierbei um den Standardwert handelt. (Wir verweisen auf Aktionsmethoden, denen das `HttpGet` Attribut implizit als Methoden zugewiesen wird `HttpGet` .)

Die- `HttpGet` `Edit` Methode nimmt den Movie ID-Parameter an, sucht den Film mit der Entity Framework `Find` -Methode und gibt den ausgewählten Film an die Bearbeitungs Ansicht zurück. Der ID-Parameter gibt den [Standardwert](https://msdn.microsoft.com/library/dd264739.aspx) 0 (null) an, wenn die `Edit` Methode ohne Parameter aufgerufen wird. Wenn ein Film nicht gefunden werden kann, wird [httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) zurückgegeben. Als das Gerüstsystem die Bearbeitungsansicht erstellt hat, wurde die `Movie`-Klasse überprüft und Code zum Rendern der `<label>`- und `<input>`-Elemente für jede Eigenschaft der Klasse erstellt. Im folgenden Beispiel wird die Ansicht "Bearbeiten" gezeigt, die generiert wurde:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

Beachten `@model MvcMovie.Models.Movie` Sie, dass die Ansichts Vorlage eine-Anweisung am Anfang der Datei enthält – dies gibt an, dass die Sicht erwartet, dass das Modell für die Ansichts Vorlage vom Typ ist `Movie` .

Der Gerüst Code verwendet mehrere *Hilfsmethoden* , um das HTML-Markup zu optimieren. Das Hilfsprogramm [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) zeigt den Namen des Felds an ( &quot; Titel &quot; , &quot; ReleaseDate &quot; , &quot; Genre &quot; oder &quot; Preis &quot; ). Das-Hilfsprogramm [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) rendert ein HTML-- `<input>` Element. Das Hilfsprogramm [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) zeigt alle Validierungs Meldungen an, die dieser Eigenschaft zugeordnet sind.

Führen Sie die Anwendung aus, und navigieren Sie zur URL */Movies* . Klicken Sie auf einen Link **Bearbeiten**. Zeigen Sie im Browser den Quelltext für die Seite an. Der HTML-Code für das Formular Element ist unten dargestellt.

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

Die- `<input>` Elemente befinden sich in einem HTML-- `<form>` Element, dessen-Attribut für `action` die Post-Bereitstellung an die URL */Movies/Edit* Die Formulardaten werden an den Server gesendet, wenn auf die Schaltfläche **Bearbeiten** geklickt wird.

## <a name="processing-the-post-request"></a>Verarbeiten der POST-Anforderung

Die folgende Liste zeigt die `HttpPost`-Version der `Edit`-Aktionsmethode.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

Der [ASP.NET MVC-Modell Binder](https://msdn.microsoft.com/magazine/hh781022.aspx) nimmt die übermittelten Formular Werte an und erstellt ein `Movie` -Objekt, das als-Parameter übergeben wird `movie` . Die `ModelState.IsValid`-Methode stellt sicher, dass die im Formular übermittelten Daten verwendet werden können, um ein `Movie`-Objekt zu ändern (bearbeiten oder aktualisieren). Wenn die Daten gültig sind, werden die Filmdaten in der-Auflistung `Movies` der- `db(MovieDBContext` Instanz gespeichert.) Die neuen Filmdaten werden in der Datenbank gespeichert, indem die- `SaveChanges` Methode von aufgerufen wird `MovieDBContext` . Nach dem Speichern der Daten leitet der Code den Benutzer an die `Index` Aktionsmethode der- `MoviesController` Klasse um, die die von Movie Collection anzeigt, einschließlich der soeben vorgenommenen Änderungen.

Wenn die bereitgestellte Werte nicht gültig sind, werden Sie erneut im Formular angezeigt. Die Hilfsprogramme `Html.ValidationMessageFor` in der Ansicht " *Edit. cshtml* " zeigen die entsprechenden Fehlermeldungen an.

![abcnotvalid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> um die jQuery-Validierung für nicht englische Gebiets Schemas zu unterstützen, die ein Komma (,) als Dezimaltrennzeichen verwenden &quot; &quot; , müssen Sie *globalize.js* und ihre spezifischen *Kulturen/globalize.cultures.js* Datei (von [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) und JavaScript einschließen, um zu verwenden `Globalize.parseFloat` . Der folgende Code zeigt die Änderungen an der Datei "views\movies\edit.cshtml", um mit der &quot; Kultur "fr-FR" zu arbeiten &quot; :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Für das Decimal-Feld ist möglicherweise ein Komma und kein Dezimaltrennzeichen erforderlich. Als temporäre Korrektur können Sie das globalization-Element dem Projektstamm web.config Datei hinzufügen. Der folgende Code zeigt das Globalisierungs Element, bei dem die Kultur auf USA Englisch festgelegt ist.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

Alle- `HttpGet` Methoden folgen einem ähnlichen Muster. Sie erhalten ein Movie-Objekt (oder eine Liste von Objekten im Fall von `Index` ) und übergeben das Modell an die Ansicht. Die- `Create` Methode übergibt ein leeres Movie-Objekt an die CREATE-Sicht. Alle Methoden, die Daten erstellen, bearbeiten, löschen oder in beliebiger Weise ändern, nutzen dazu die `HttpPost`-Überladung der Methode. Das Ändern von Daten in einer HTTP Get-Methode stellt ein Sicherheitsrisiko dar, wie im Blogbeitrag Entry [ASP.NET MVC Tip #46 – use Delete Links (Erstellen von Sicherheitslücken](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)). Das Ändern von Daten in einer Get-Methode verstößt auch gegen bewährte HTTP-Methoden und das architektonische [Rest](http://en.wikipedia.org/wiki/Representational_State_Transfer) -Muster, das angibt, dass Get-Anforderungen den Zustand der Anwendung nicht ändern sollten. Die Durchführung eines GET-Vorgangs sollte also eine sichere Operation sein, die keine Nebenwirkungen hat und die permanenten Daten nicht ändert.

## <a name="adding-a-search-method-and-search-view"></a>Hinzufügen einer Suchmethode und einer Such Ansicht

In diesem Abschnitt fügen Sie eine `SearchIndex` Aktionsmethode hinzu, mit der Sie Filme nach Genre oder Name durchsuchen können. Dies wird mithilfe der */Movies/SearchIndex* -URL zur Verfügung gestellt. In der Anforderung wird ein HTML-Formular angezeigt, das Eingabeelemente enthält, die ein Benutzer eingeben kann, um nach einem Film zu suchen. Wenn ein Benutzer das Formular sendet, erhält die Aktionsmethode die vom Benutzer gesendeten Suchwerte und verwendet die Werte, um die Datenbank zu durchsuchen.

## <a name="displaying-the-searchindex-form"></a>Anzeigen des SearchIndex-Formulars

Beginnen `SearchIndex` Sie, indem Sie der vorhandenen Klasse eine Aktionsmethode hinzufügen `MoviesController` . Die-Methode gibt eine Ansicht zurück, die ein HTML-Formular enthält. Der Code lautet wie folgt:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

In der ersten Zeile der- `SearchIndex` Methode wird die folgende [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfrage erstellt, um die Filme auszuwählen:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

Die Abfrage wird an dieser Stelle definiert, aber noch nicht für den Datenspeicher ausgeführt.

Wenn der- `searchString` Parameter eine Zeichenfolge enthält, wird die Film Abfrage so geändert, dass nach dem Wert der Such Zeichenfolge gefiltert wird, indem der folgende Code verwendet wird:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

Der Code `s => s.Title` oben ist ein [Lambdaausdruck](https://msdn.microsoft.com/library/bb397687.aspx). Lambdas werden in Methoden basierten [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfragen als Argumente für Standard Abfrage Operator-Methoden wie z. b. die [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) -Methode verwendet, die im obigen Code verwendet wird. LINQ-Abfragen werden nicht ausgeführt, wenn Sie definiert oder durch Aufrufen einer Methode wie oder geändert werden `Where` `OrderBy` . Stattdessen wird die Abfrage Ausführung verzögert. Dies bedeutet, dass die Auswertung eines Ausdrucks verzögert wird, bis der erkannte Wert tatsächlich durchlaufen oder die- [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) Methode aufgerufen wird. Im `SearchIndex` Beispiel wird die Abfrage in der SearchIndex-Sicht ausgeführt. Weitere Informationen zur verzögerten Abfrageausführung finden Sie unter [Abfrageausführung](https://msdn.microsoft.com/library/bb738633.aspx).

Nun können Sie die `SearchIndex` Ansicht implementieren, in der das Formular für den Benutzer angezeigt wird. Klicken Sie mit der rechten Maustaste in die `SearchIndex` Methode, und klicken Sie dann auf **Ansicht hinzufügen** Geben Sie im Dialogfeld **Ansicht hinzufügen** an, dass Sie ein- `Movie` Objekt an die Ansichts Vorlage als Modell Klasse übergeben. Wählen Sie in der Liste **Gerüst Vorlage** die Option **Liste**aus, und klicken Sie dann auf **Hinzufügen**.

![Addsearchview](examining-the-edit-methods-and-edit-view/_static/image5.png)

Wenn Sie auf die Schaltfläche **Hinzufügen** klicken, wird die Ansichts Vorlage *views\movies\searchindex.cshtml* erstellt. Da Sie **Liste** in der Liste **Gerüstbau Vorlage** ausgewählt haben, generiert Visual Studio automatisch ein Standard Markup in der Ansicht. Der Gerüstbau hat ein HTML-Formular erstellt. Die `Movie` Klasse wurde untersucht und Code erstellt, um `<label>` Elemente für jede Eigenschaft der Klasse zu erzeugen. In der folgenden Liste wird die erstellte Create View angezeigt:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/SearchIndex*. Fügen Sie eine Abfragezeichenfolge wie `?searchString=ghost` an die URL an. Die gefilterten Filme werden angezeigt.

![Searchqrystr](examining-the-edit-methods-and-edit-view/_static/image6.png)

Wenn Sie die Signatur der `SearchIndex` Methode so ändern, dass Sie einen Parameter mit dem Namen hat `id` , `id` entspricht der Parameter dem `{id}` Platzhalter für die Standardrouten, die in der Datei *Global. asax* festgelegt sind.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

Die ursprüngliche `SearchIndex` Methode sieht wie folgt aus:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

Die geänderte `SearchIndex` Methode sieht wie folgt aus:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

Sie können nun den Suchtitel als Routendaten (ein URL-Segment) anstatt als Wert einer Abfragezeichenfolge übergeben.

![Searchroutedata](examining-the-edit-methods-and-edit-view/_static/image7.png)

Sie können jedoch von den Benutzern nicht erwarten, dass sie jedes Mal die URL ändern, wenn sie nach einem Film suchen möchten. Nun fügen Sie die Benutzeroberfläche hinzu, um Sie beim Filtern von Filmen zu unterstützen. Wenn Sie die Signatur der- `SearchIndex` Methode geändert haben, um zu testen, wie der Routen gebundene ID-Parameter übergeben wird, ändern Sie ihn so, dass die- `SearchIndex` Methode einen Zeichen folgen Parameter namens annimmt `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

Öffnen Sie die Datei *views\movies\searchindex.cshtml* , und `@Html.ActionLink("Create New", "Create")` fügen Sie direkt nach Folgendes hinzu:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

Das folgende Beispiel zeigt einen Teil der *views\movies\searchindex.cshtml* -Datei mit dem hinzugefügten Filter Markup.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

Das-Hilfsprogramm `Html.BeginForm` erstellt ein öffnendes- `<form>` Tag. Das Hilfsprogramm bewirkt, dass `Html.BeginForm` das Formular in sich selbst gepostet wird, wenn der Benutzer das Formular durch Klicken auf die Schaltfläche **Filter** übermittelt.

Führen Sie die Anwendung aus, und suchen Sie nach einem Film.

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

Es gibt keine Überladung der- `HttpPost` `SearchIndex` Methode. Sie benötigen Sie nicht, da die Methode den Zustand der Anwendung nicht ändert, sondern nur das Filtern von Daten.

Sie können die folgende `HttpPost SearchIndex`-Methode hinzufügen. In diesem Fall würde der Aktions Aufruf mit der `HttpPost SearchIndex` -Methode verglichen, und die- `HttpPost SearchIndex` Methode würde wie in der folgenden Abbildung dargestellt ausgeführt werden.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![Searchpostghost](examining-the-edit-methods-and-edit-view/_static/image9.png)

Doch selbst wenn Sie diese `HttpPost`-Version der `SearchIndex`-Methode hinzufügen, gibt es eine Einschränkung für die gesamte Implementierung. Stellen Sie sich vor, Sie möchten eine bestimmte Suche als Favorit speichern oder einen Link an Freunde senden, auf den diese klicken können, um dieselbe gefilterte Liste von Filmen anzuzeigen. Beachten Sie, dass die URL für die HTTP POST-Anforderung mit der URL für die Get-Anforderung übereinstimmt (localhost: xxxxx/Movies/SearchIndex). in der URL selbst sind keine Suchinformationen vorhanden. Derzeit werden die Such Zeichenfolgen-Informationen als Formular Feldwert an den Server gesendet. Dies bedeutet, dass Sie diese Suchinformationen nicht in einem Lesezeichen erfassen oder an Freunde in einer URL senden können.

Die Lösung besteht darin, eine Überladung von zu verwenden `BeginForm` , die angibt, dass die Post-Anforderung die Suchinformationen der URL hinzufügen soll und dass Sie an die HttpGet-Version der Methode weitergeleitet werden soll `SearchIndex` . Ersetzen Sie die vorhandene Parameter lose- `BeginForm` Methode durch Folgendes:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

Wenn Sie nun eine Suche übermitteln, enthält die URL eine Suchabfrage Zeichenfolge. Das Suchen wird auch an Aktionsmethode `HttpGet SearchIndex` übertragen, auch wenn Sie eine `HttpPost SearchIndex`-Methode haben.

![Searchindexwithgeturl](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>Hinzufügen der Suche nach Genre

Wenn Sie die `HttpPost` Version der-Methode hinzugefügt `SearchIndex` haben, löschen Sie Sie jetzt.

Als Nächstes fügen Sie eine Funktion hinzu, um Benutzern das Suchen nach Filmen nach Genre zu ermöglichen. Ersetzen Sie die `SearchIndex`-Methode durch den folgenden Code:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

Diese Version der- `SearchIndex` Methode nimmt einen zusätzlichen Parameter, nämlich, auf `movieGenre` . In den ersten Codezeilen wird ein- `List` Objekt erstellt, um Movie-Genres aus der Datenbank zu speichern.

Der folgende Code ist eine LINQ-Abfrage, die alle Genres aus der Datenbank abruft.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

Der Code verwendet die- `AddRange` Methode der generischen- `List` Auflistung, um alle eindeutigen Genres der Liste hinzuzufügen. (Ohne den- `Distinct` Modifizierer würden doppelte Genres hinzugefügt werden – beispielsweise würde die-Komödie in unserem Beispiel zweimal hinzugefügt werden.) Der Code speichert dann die Liste der Genres im- `ViewBag` Objekt.

Der folgende Code zeigt, wie Sie den-Parameter überprüfen `movieGenre` . Wenn Sie nicht leer ist, schränkt der Code die Film Abfrage weiter ein, um die ausgewählten Filme auf das angegebene Genre zu beschränken.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Hinzufügen von Markup zur Ansicht "SearchIndex" zur Unterstützung der Suche nach Genre

Fügen Sie `Html.DropDownList` der Datei " *views\movies\searchindex.cshtml* " direkt vor dem Hilfsprogramm ein Hilfsobjekt hinzu `TextBox` . Das vollständige Markup ist unten dargestellt:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/SearchIndex*. Probieren Sie eine Suche nach Genre, nach Film Name und nach beiden Kriterien aus.

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

In diesem Abschnitt haben Sie die vom Framework generierten CRUD-Aktionsmethoden und-Sichten untersucht. Sie haben eine Such Aktionsmethode und-Ansicht erstellt, mit der Benutzer nach Film Titel und Genre suchen können. Im nächsten Abschnitt erfahren Sie, wie Sie dem Modell eine Eigenschaft hinzufügen `Movie` und wie Sie einen Initialisierer hinzufügen, mit dem automatisch eine Testdatenbank erstellt wird.

> [!div class="step-by-step"]
> [Zurück](accessing-your-models-data-from-a-controller.md)
> [Weiter](adding-a-new-field-to-the-movie-model-and-table.md)
