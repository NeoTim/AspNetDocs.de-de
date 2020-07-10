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
# <a name="search"></a><span data-ttu-id="15fc3-102">Suchen,</span><span class="sxs-lookup"><span data-stu-id="15fc3-102">Search</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="15fc3-103">Hinzufügen einer Suchmethode und einer Such Ansicht</span><span class="sxs-lookup"><span data-stu-id="15fc3-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="15fc3-104">In diesem Abschnitt fügen Sie der Aktionsmethode Suchfunktionen hinzu `Index` , mit denen Sie Filme nach Genre oder Name durchsuchen können.</span><span class="sxs-lookup"><span data-stu-id="15fc3-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15fc3-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="15fc3-105">Prerequisites</span></span>

<span data-ttu-id="15fc3-106">Um den Screenshots dieses Abschnitts zu entsprechen, müssen Sie die Anwendung (F5) ausführen und der-Datenbank die folgenden Filme hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="15fc3-107">Titel</span><span class="sxs-lookup"><span data-stu-id="15fc3-107">Title</span></span> | <span data-ttu-id="15fc3-108">Veröffentlichungsdatum</span><span class="sxs-lookup"><span data-stu-id="15fc3-108">Release Date</span></span> | <span data-ttu-id="15fc3-109">Genre</span><span class="sxs-lookup"><span data-stu-id="15fc3-109">Genre</span></span> | <span data-ttu-id="15fc3-110">Preis</span><span class="sxs-lookup"><span data-stu-id="15fc3-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="15fc3-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="15fc3-111">Ghostbusters</span></span> | <span data-ttu-id="15fc3-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="15fc3-112">6/8/1984</span></span> | <span data-ttu-id="15fc3-113">Di</span><span class="sxs-lookup"><span data-stu-id="15fc3-113">Comedy</span></span> | <span data-ttu-id="15fc3-114">6,99</span><span class="sxs-lookup"><span data-stu-id="15fc3-114">6.99</span></span> |
| <span data-ttu-id="15fc3-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="15fc3-115">Ghostbusters II</span></span> | <span data-ttu-id="15fc3-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="15fc3-116">6/16/1989</span></span> | <span data-ttu-id="15fc3-117">Di</span><span class="sxs-lookup"><span data-stu-id="15fc3-117">Comedy</span></span> | <span data-ttu-id="15fc3-118">6,99</span><span class="sxs-lookup"><span data-stu-id="15fc3-118">6.99</span></span> |
| <span data-ttu-id="15fc3-119">Planet der Affen</span><span class="sxs-lookup"><span data-stu-id="15fc3-119">Planet of the Apes</span></span> | <span data-ttu-id="15fc3-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="15fc3-120">3/27/1986</span></span> | <span data-ttu-id="15fc3-121">Aktion</span><span class="sxs-lookup"><span data-stu-id="15fc3-121">Action</span></span> | <span data-ttu-id="15fc3-122">5,99</span><span class="sxs-lookup"><span data-stu-id="15fc3-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="15fc3-123">Aktualisieren des Index Formulars</span><span class="sxs-lookup"><span data-stu-id="15fc3-123">Updating the Index Form</span></span>

<span data-ttu-id="15fc3-124">Aktualisieren Sie zunächst die- `Index` Aktionsmethode auf die vorhandene- `MoviesController` Klasse.</span><span class="sxs-lookup"><span data-stu-id="15fc3-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="15fc3-125">Der Code lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="15fc3-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="15fc3-126">In der ersten Zeile der- `Index` Methode wird die folgende [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfrage erstellt, um die Filme auszuwählen:</span><span class="sxs-lookup"><span data-stu-id="15fc3-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="15fc3-127">Die Abfrage wird an dieser Stelle definiert, aber noch nicht für die Datenbank ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="15fc3-128">Wenn der- `searchString` Parameter eine Zeichenfolge enthält, wird die Film Abfrage so geändert, dass nach dem Wert der Such Zeichenfolge gefiltert wird, indem der folgende Code verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="15fc3-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="15fc3-129">Der Code `s => s.Title` oben ist ein [Lambdaausdruck](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="15fc3-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="15fc3-130">Lambdas werden in Methoden basierten [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfragen als Argumente für Standard Abfrage Operator-Methoden wie z. b. die [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) -Methode verwendet, die im obigen Code verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="15fc3-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="15fc3-131">LINQ-Abfragen werden nicht ausgeführt, wenn Sie definiert oder durch Aufrufen einer Methode wie oder geändert werden `Where` `OrderBy` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="15fc3-132">Stattdessen wird die Abfrage Ausführung verzögert. Dies bedeutet, dass die Auswertung eines Ausdrucks verzögert wird, bis der erkannte Wert tatsächlich durchlaufen oder die- [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) Methode aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="15fc3-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="15fc3-133">Im `Search` Beispiel wird die Abfrage in der *Index. cshtml* -Ansicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="15fc3-134">Weitere Informationen zur verzögerten Abfrageausführung finden Sie unter [Abfrageausführung](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="15fc3-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="15fc3-135">Die [enthält](https://msdn.microsoft.com/library/bb155125.aspx) -Methode wird für die Datenbank ausgeführt, nicht für den obigen c#-Code.</span><span class="sxs-lookup"><span data-stu-id="15fc3-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="15fc3-136">In der-Datenbank [sind](https://msdn.microsoft.com/library/bb155125.aspx) SQL-Tabellen [ähnlich](https://msdn.microsoft.com/library/ms179859.aspx), bei denen die Groß-/Kleinschreibung nicht beachtet wird.</span><span class="sxs-lookup"><span data-stu-id="15fc3-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="15fc3-137">Nun können Sie die `Index` Ansicht aktualisieren, in der das Formular für den Benutzer angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="15fc3-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="15fc3-138">Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/Index*.</span><span class="sxs-lookup"><span data-stu-id="15fc3-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="15fc3-139">Fügen Sie eine Abfragezeichenfolge wie `?searchString=ghost` an die URL an.</span><span class="sxs-lookup"><span data-stu-id="15fc3-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="15fc3-140">Die gefilterten Filme werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-140">The filtered movies are displayed.</span></span>

![Searchqrystr](adding-search/_static/image1.png)

<span data-ttu-id="15fc3-142">Wenn Sie die Signatur der `Index` Methode so ändern, dass Sie einen Parameter mit dem Namen hat `id` , `id` entspricht der Parameter dem `{id}` Platzhalter für die Standardrouten, die in der Datei *App \_ start\routeconfig.cs* festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="15fc3-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="15fc3-143">Die ursprüngliche `Index` Methode sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="15fc3-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="15fc3-144">Die geänderte `Index` Methode sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="15fc3-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="15fc3-145">Sie können nun den Suchtitel als Routendaten (ein URL-Segment) anstatt als Wert einer Abfragezeichenfolge übergeben.</span><span class="sxs-lookup"><span data-stu-id="15fc3-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="15fc3-146">Sie können jedoch von den Benutzern nicht erwarten, dass sie jedes Mal die URL ändern, wenn sie nach einem Film suchen möchten.</span><span class="sxs-lookup"><span data-stu-id="15fc3-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="15fc3-147">Deshalb fügen Sie nun eine Benutzeroberflächenoption zum besseren Filtern von Filmen hinzu.</span><span class="sxs-lookup"><span data-stu-id="15fc3-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="15fc3-148">Wenn Sie die Signatur der- `Index` Methode geändert haben, um zu testen, wie der Routen gebundene ID-Parameter übergeben wird, ändern Sie ihn so, dass die- `Index` Methode einen Zeichen folgen Parameter namens annimmt `searchString` :</span><span class="sxs-lookup"><span data-stu-id="15fc3-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="15fc3-149">Öffnen Sie die Datei " *views\movies\index.cshtml* ", und `@Html.ActionLink("Create New", "Create")` fügen Sie direkt nach das unten markierte Formular Markup hinzu:</span><span class="sxs-lookup"><span data-stu-id="15fc3-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="15fc3-150">Das-Hilfsprogramm `Html.BeginForm` erstellt ein öffnendes- `<form>` Tag.</span><span class="sxs-lookup"><span data-stu-id="15fc3-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="15fc3-151">Das Hilfsprogramm bewirkt, dass `Html.BeginForm` das Formular in sich selbst gepostet wird, wenn der Benutzer das Formular durch Klicken auf die Schaltfläche **Filter** übermittelt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="15fc3-152">Beim Anzeigen und Bearbeiten von Ansichts Dateien hat Visual Studio 2013 eine gute Verbesserung.</span><span class="sxs-lookup"><span data-stu-id="15fc3-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="15fc3-153">Wenn Sie die Anwendung mit einer geöffneten Ansichts Datei ausführen, ruft Visual Studio 2013 die richtige Controller Aktionsmethode auf, um die Ansicht anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="15fc3-154">Wenn die Index Ansicht in Visual Studio geöffnet ist (wie in der Abbildung oben gezeigt), tippen Sie auf CTR F5 oder F5, um die Anwendung auszuführen, und versuchen Sie dann, nach einem Film zu suchen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="15fc3-155">Es gibt keine Überladung der- `HttpPost` `Index` Methode.</span><span class="sxs-lookup"><span data-stu-id="15fc3-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="15fc3-156">Sie benötigen Sie nicht, da die Methode den Zustand der Anwendung nicht ändert, sondern nur das Filtern von Daten.</span><span class="sxs-lookup"><span data-stu-id="15fc3-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="15fc3-157">Sie können die folgende `HttpPost Index`-Methode hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="15fc3-158">In diesem Fall würde der Aktions Aufruf mit der `HttpPost Index` -Methode verglichen, und die- `HttpPost Index` Methode würde wie in der folgenden Abbildung dargestellt ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="15fc3-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![Searchpostghost](adding-search/_static/image5.png)

<span data-ttu-id="15fc3-160">Doch selbst wenn Sie diese `HttpPost`-Version der `Index`-Methode hinzufügen, gibt es eine Einschränkung für die gesamte Implementierung.</span><span class="sxs-lookup"><span data-stu-id="15fc3-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="15fc3-161">Stellen Sie sich vor, Sie möchten eine bestimmte Suche als Favorit speichern oder einen Link an Freunde senden, auf den diese klicken können, um dieselbe gefilterte Liste von Filmen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="15fc3-162">Beachten Sie, dass die URL für die HTTP POST-Anforderung mit der URL für die Get-Anforderung übereinstimmt ("localhost: xxxxx/Movies/Index"). es sind keine Suchinformationen in der URL selbst vorhanden.</span><span class="sxs-lookup"><span data-stu-id="15fc3-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="15fc3-163">Derzeit werden die Such Zeichenfolgen-Informationen als Formular Feldwert an den Server gesendet.</span><span class="sxs-lookup"><span data-stu-id="15fc3-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="15fc3-164">Dies bedeutet, dass Sie diese Suchinformationen nicht in einem Lesezeichen erfassen oder an Freunde in einer URL senden können.</span><span class="sxs-lookup"><span data-stu-id="15fc3-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="15fc3-165">Die Lösung besteht darin, eine Überladung von zu verwenden `BeginForm` , die angibt, dass die Post-Anforderung die Suchinformationen der URL hinzufügen soll und dass Sie an die `HttpGet` Version der Methode weitergeleitet werden soll `Index` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="15fc3-166">Ersetzen Sie die vorhandene Parameter lose- `BeginForm` Methode durch das folgende Markup:</span><span class="sxs-lookup"><span data-stu-id="15fc3-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="15fc3-168">Wenn Sie nun eine Suche übermitteln, enthält die URL eine Suchabfrage Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="15fc3-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="15fc3-169">Das Suchen wird auch an Aktionsmethode `HttpGet Index` übertragen, auch wenn Sie eine `HttpPost Index`-Methode haben.</span><span class="sxs-lookup"><span data-stu-id="15fc3-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![Indexwithgeturl](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="15fc3-171">Hinzufügen der Suche nach Genre</span><span class="sxs-lookup"><span data-stu-id="15fc3-171">Adding Search by Genre</span></span>

<span data-ttu-id="15fc3-172">Wenn Sie die `HttpPost` Version der-Methode hinzugefügt `Index` haben, löschen Sie Sie jetzt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="15fc3-173">Als Nächstes fügen Sie eine Funktion hinzu, um Benutzern das Suchen nach Filmen nach Genre zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="15fc3-174">Ersetzen Sie die `Index`-Methode durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="15fc3-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="15fc3-175">Diese Version der- `Index` Methode nimmt einen zusätzlichen Parameter, nämlich, auf `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="15fc3-176">In den ersten Codezeilen wird ein- `List` Objekt erstellt, um Movie-Genres aus der Datenbank zu speichern.</span><span class="sxs-lookup"><span data-stu-id="15fc3-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="15fc3-177">Der folgende Code ist eine LINQ-Abfrage, die alle Genres aus der Datenbank abruft.</span><span class="sxs-lookup"><span data-stu-id="15fc3-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="15fc3-178">Der Code verwendet die- `AddRange` Methode der generischen- `List` Auflistung, um alle eindeutigen Genres der Liste hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="15fc3-179">(Ohne den- `Distinct` Modifizierer würden doppelte Genres hinzugefügt werden – beispielsweise würde die-Komödie in unserem Beispiel zweimal hinzugefügt werden.)</span><span class="sxs-lookup"><span data-stu-id="15fc3-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="15fc3-180">Der Code speichert dann die Liste der Genres im- `ViewBag.MovieGenre` Objekt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="15fc3-181">Das Speichern von Kategorieinformationen (z. b. Filmgenres) als [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) -Objekt in einem `ViewBag` und der anschließende Zugriff auf die Kategoriedaten in einem Dropdown-Listenfeld ist ein typischer Ansatz für MVC-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="15fc3-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="15fc3-182">Der folgende Code zeigt, wie Sie den-Parameter überprüfen `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="15fc3-183">Wenn Sie nicht leer ist, schränkt der Code die Film Abfrage weiter ein, um die ausgewählten Filme auf das angegebene Genre zu beschränken.</span><span class="sxs-lookup"><span data-stu-id="15fc3-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="15fc3-184">Wie bereits erwähnt, wird die Abfrage nicht in der Datenbank ausgeführt, bis die Filmliste durchlaufen wird (was in der Ansicht geschieht, nachdem die `Index` Aktionsmethode zurückgegeben wurde).</span><span class="sxs-lookup"><span data-stu-id="15fc3-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="15fc3-185">Hinzufügen von Markup zur Index Ansicht zur Unterstützung der Suche nach Genre</span><span class="sxs-lookup"><span data-stu-id="15fc3-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="15fc3-186">Fügen Sie `Html.DropDownList` der Datei " *views\movies\index.cshtml* " direkt vor dem Hilfsprogramm ein Hilfsobjekt hinzu `TextBox` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="15fc3-187">Das vollständige Markup ist unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="15fc3-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="15fc3-188">Im folgenden Code wird Folgendes ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="15fc3-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="15fc3-189">Der Parameter "muviegenre" stellt den Schlüssel für das Hilfsprogramm bereit `DropDownList` , in dem ein gesucht werden soll `IEnumerable<SelectListItem>` `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="15fc3-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="15fc3-190">Der `ViewBag` wurde in der Aktionsmethode aufgefüllt:</span><span class="sxs-lookup"><span data-stu-id="15fc3-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="15fc3-191">Der Parameter "All" stellt eine Options Bezeichnung bereit.</span><span class="sxs-lookup"><span data-stu-id="15fc3-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="15fc3-192">Wenn Sie diese Auswahl in Ihrem Browser überprüfen, sehen Sie, dass das Attribut "Value" leer ist.</span><span class="sxs-lookup"><span data-stu-id="15fc3-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="15fc3-193">Da der Controller nur filtert `if` , dass die Zeichenfolge nicht `null` oder leer ist, wird bei der Übermittlung eines leeren Werts für `movieGenre` Alle Genres angezeigt.</span><span class="sxs-lookup"><span data-stu-id="15fc3-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="15fc3-194">Sie können auch festlegen, dass eine Option standardmäßig ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="15fc3-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="15fc3-195">Wenn Sie "Comedy" als Standardoption wünschen, ändern Sie den Code im Controller wie folgt:</span><span class="sxs-lookup"><span data-stu-id="15fc3-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="15fc3-196">Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/Index*.</span><span class="sxs-lookup"><span data-stu-id="15fc3-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="15fc3-197">Probieren Sie eine Suche nach Genre, nach Film Name und nach beiden Kriterien aus.</span><span class="sxs-lookup"><span data-stu-id="15fc3-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="15fc3-198">In diesem Abschnitt haben Sie eine Such Aktionsmethode und-Ansicht erstellt, mit der Benutzer nach Film Titel und Genre suchen können.</span><span class="sxs-lookup"><span data-stu-id="15fc3-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="15fc3-199">Im nächsten Abschnitt erfahren Sie, wie Sie dem Modell eine Eigenschaft hinzufügen `Movie` und wie Sie einen Initialisierer hinzufügen, mit dem automatisch eine Testdatenbank erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="15fc3-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="15fc3-200">[Zurück](examining-the-edit-methods-and-edit-view.md)
> [Weiter](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="15fc3-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
