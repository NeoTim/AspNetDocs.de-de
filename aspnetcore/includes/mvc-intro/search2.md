---
ms.openlocfilehash: d5d902a2a6fcae3155c23d0040a8026ed5808dff
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047957"
---
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull)]

![Index view](~/tutorials/first-mvc-app/search/_static/ghost.png)


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

--> 

<span data-ttu-id="877bc-101">Die vorherige `Index`-Methode:</span><span class="sxs-lookup"><span data-stu-id="877bc-101">The previous `Index` method:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_1stSearch)]

<span data-ttu-id="877bc-102">Die aktualisierte `Index`-Methode mit `id`-Parameter:</span><span class="sxs-lookup"><span data-stu-id="877bc-102">The updated `Index` method with `id` parameter:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_SearchID)]

<span data-ttu-id="877bc-103">Sie können nun den Suchtitel als Routendaten (ein URL-Segment) anstatt als Wert einer Abfragezeichenfolge übergeben.</span><span class="sxs-lookup"><span data-stu-id="877bc-103">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![Indexansicht mit dem der URL hinzugefügten Wort „ghost“ und einer zurückgegebenen Filmliste mit zwei Filmen: Ghostbusters und Ghostbusters 2](~/tutorials/first-mvc-app/search/_static/g2.png)

<span data-ttu-id="877bc-105">Sie können jedoch von den Benutzern nicht erwarten, dass sie jedes Mal die URL ändern, wenn sie nach einem Film suchen möchten.</span><span class="sxs-lookup"><span data-stu-id="877bc-105">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="877bc-106">Deshalb fügen Sie nun Benutzeroberflächenelemente zum besseren Filtern von Filmen hinzu.</span><span class="sxs-lookup"><span data-stu-id="877bc-106">So now you'll add UI elements to help them filter movies.</span></span> <span data-ttu-id="877bc-107">Wenn Sie die Signatur der `Index`-Methode geändert haben, um das Übergeben des routengebundenen Parameters `ID` zu testen, ändern Sie sie erneut so, dass sie einen Parameter namens `searchString` verwendet:</span><span class="sxs-lookup"><span data-stu-id="877bc-107">If you changed the signature of the `Index` method to test how to pass the route-bound `ID` parameter, change it back so that it takes a parameter named `searchString`:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_1stSearch)]

<span data-ttu-id="877bc-108">Öffnen Sie die Datei *Views/Movies/Index.cshtml*, und fügen Sie das hervorgehobene `<form>`-Markup hinzu:</span><span class="sxs-lookup"><span data-stu-id="877bc-108">Open the *Views/Movies/Index.cshtml* file, and add the `<form>` markup highlighted below:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]

<span data-ttu-id="877bc-109">Das HTML-Tag `<form>` nutzt das [Hilfsprogramm für Formulartags](xref:mvc/views/working-with-forms). Wenn Sie nun das Formular senden, wird die Filterzeichenfolge an die Aktion `Index` des „movies“-Controllers übermittelt.</span><span class="sxs-lookup"><span data-stu-id="877bc-109">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms), so when you submit the form, the filter string is posted to the `Index` action of the movies controller.</span></span> <span data-ttu-id="877bc-110">Speichern Sie Ihre Änderungen, und testen Sie dann den Filter.</span><span class="sxs-lookup"><span data-stu-id="877bc-110">Save your changes and then test the filter.</span></span>

![Indexansicht mit dem in das Filtertextfeld eingegebenen Wort „ghost“](~/tutorials/first-mvc-app/search/_static/filter.png)

<span data-ttu-id="877bc-112">Entgegen Ihrer Erwartung gibt es keine `[HttpPost]`-Überladung der `Index`-Methode.</span><span class="sxs-lookup"><span data-stu-id="877bc-112">There's no `[HttpPost]` overload of the `Index` method as you might expect.</span></span> <span data-ttu-id="877bc-113">Diese ist nicht erforderlich, da die Methode nicht den Status der App ändert, sondern bloß Daten filtert.</span><span class="sxs-lookup"><span data-stu-id="877bc-113">You don't need it, because the method isn't changing the state of the app, just filtering data.</span></span>

<span data-ttu-id="877bc-114">Sie können die folgende `[HttpPost] Index`-Methode hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="877bc-114">You could add the following `[HttpPost] Index` method.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]

<span data-ttu-id="877bc-115">Der Parameter `notUsed` dient zum Erstellen einer Überladung für die `Index`-Methode.</span><span class="sxs-lookup"><span data-stu-id="877bc-115">The `notUsed` parameter is used to create an overload for the `Index` method.</span></span> <span data-ttu-id="877bc-116">Damit beschäftigen wir uns später im Tutorial.</span><span class="sxs-lookup"><span data-stu-id="877bc-116">We'll talk about that later in the tutorial.</span></span>

<span data-ttu-id="877bc-117">Wenn Sie diese Methode hinzufügen, entspricht die aufrufende Aktionsinstanz der `[HttpPost] Index`-Methode, und die `[HttpPost] Index`-Methode wird wie in der folgenden Abbildung gezeigt ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="877bc-117">If you add this method, the action invoker would match the `[HttpPost] Index` method, and the `[HttpPost] Index` method would run as shown in the image below.</span></span>

![Browserfenster mit der Antwort der Anwendung von „Von HttpPost-Index“: Filter für „ghost“](~/tutorials/first-mvc-app/search/_static/fo.png)

<span data-ttu-id="877bc-119">Doch selbst wenn Sie diese `[HttpPost]`-Version der `Index`-Methode hinzufügen, gibt es eine Einschränkung für die gesamte Implementierung.</span><span class="sxs-lookup"><span data-stu-id="877bc-119">However, even if you add this `[HttpPost]` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="877bc-120">Stellen Sie sich vor, Sie möchten eine bestimmte Suche als Favorit speichern oder einen Link an Freunde senden, auf den diese klicken können, um dieselbe gefilterte Liste von Filmen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="877bc-120">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="877bc-121">Beachten Sie, dass die URL der HTTP POST-Anforderung identisch mit der URL der GET-Anforderung (localhost:xxxxx/Filme/Index) ist. Es sind keine Suchinformationen in der URL vorhanden.</span><span class="sxs-lookup"><span data-stu-id="877bc-121">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL.</span></span> <span data-ttu-id="877bc-122">Die Informationen in der Suchzeichenfolge werden an den Server als [Formularfeldwert](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data) gesendet.</span><span class="sxs-lookup"><span data-stu-id="877bc-122">The search string information is sent to the server as a [form field value](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data).</span></span> <span data-ttu-id="877bc-123">Sie können dies mit den Entwicklertools für den Browser oder dem exzellenten Tool [Fiddler](http://www.telerik.com/fiddler) überprüfen.</span><span class="sxs-lookup"><span data-stu-id="877bc-123">You can verify that with the browser Developer tools or the excellent [Fiddler tool](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="877bc-124">Die folgende Abbildung zeigt die Entwicklertools für den Browser Chrome:</span><span class="sxs-lookup"><span data-stu-id="877bc-124">The image below shows the Chrome browser Developer tools:</span></span>

![Registerkarte „Netzwerk“ der Entwicklertools in Microsoft Edge mit einem Anforderungstext mit dem „searchString“-Wert „ghost“](~/tutorials/first-mvc-app/search/_static/f12_rb.png)

<span data-ttu-id="877bc-126">Sie können den Suchparameter und das [XSRF](xref:security/anti-request-forgery)-Token im Anforderungstext erkennen.</span><span class="sxs-lookup"><span data-stu-id="877bc-126">You can see the search parameter and [XSRF](xref:security/anti-request-forgery) token in the request body.</span></span> <span data-ttu-id="877bc-127">Wie im vorherigen Tutorial erwähnt, generiert das [Hilfsprogramm für Formulartags](xref:mvc/views/working-with-forms) ein [XSRF](xref:security/anti-request-forgery)-Fälschungssicherheitstoken.</span><span class="sxs-lookup"><span data-stu-id="877bc-127">Note, as mentioned in the previous tutorial, the [Form Tag Helper](xref:mvc/views/working-with-forms) generates an [XSRF](xref:security/anti-request-forgery) anti-forgery token.</span></span> <span data-ttu-id="877bc-128">Da wir keine Daten ändern, müssen wir nicht das Token in der Controllermethode validieren.</span><span class="sxs-lookup"><span data-stu-id="877bc-128">We're not modifying data, so we don't need to validate the token in the controller method.</span></span>

<span data-ttu-id="877bc-129">Da sich der Suchparameter im Anforderungstext und nicht in der URL befindet, können Sie diese Suchinformationen nicht als Favorit speichern oder mit anderen teilen.</span><span class="sxs-lookup"><span data-stu-id="877bc-129">Because the search parameter is in the request body and not the URL, you can't capture that search information to bookmark or share with others.</span></span> <span data-ttu-id="877bc-130">Wir beheben dies durch Angeben der Anforderung als `HTTP GET`.</span><span class="sxs-lookup"><span data-stu-id="877bc-130">We'll fix this by specifying the request should be `HTTP GET`.</span></span>
