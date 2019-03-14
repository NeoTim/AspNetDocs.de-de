---
title: Erstellen von Back-End-Diensten für native mobile Apps mit ASP.NET Core
author: ardalis
description: Erfahren Sie, wie Back-End-Dienste mit ASP.NET Core MVC zur Unterstützung nativer mobiler Apps erstellt werden.
ms.author: riande
ms.date: 10/14/2016
uid: mobile/native-mobile-backend
ms.openlocfilehash: 3ebd30ad1ffbd66b256e7f3954a07d682f76a754
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036037"
---
# <a name="create-backend-services-for-native-mobile-apps-with-aspnet-core"></a><span data-ttu-id="a1d9f-103">Erstellen von Back-End-Diensten für native mobile Apps mit ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a1d9f-103">Create backend services for native mobile apps with ASP.NET Core</span></span>

<span data-ttu-id="a1d9f-104">Von [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="a1d9f-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="a1d9f-105">Mobile Apps können problemlos mit Back-End-Diensten von ASP.NET Core kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-105">Mobile apps can easily communicate with ASP.NET Core backend services.</span></span>

[<span data-ttu-id="a1d9f-106">Anzeigen oder Herunterladen von Beispielcode für Back-End-Dienste</span><span class="sxs-lookup"><span data-stu-id="a1d9f-106">View or download sample backend services code</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/mobile/native-mobile-backend/sample)

## <a name="the-sample-native-mobile-app"></a><span data-ttu-id="a1d9f-107">Die native mobile Beispiel-App</span><span class="sxs-lookup"><span data-stu-id="a1d9f-107">The Sample Native Mobile App</span></span>

<span data-ttu-id="a1d9f-108">In diesem Tutorial wird veranschaulicht, wie Back-End-Dienste mit ASP.NET Core MVC zur Unterstützung nativer mobiler Apps erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-108">This tutorial demonstrates how to create backend services using ASP.NET Core MVC to support native mobile apps.</span></span> <span data-ttu-id="a1d9f-109">Darin wird die [Xamarin.Forms-App ToDoRest](/xamarin/xamarin-forms/data-cloud/consuming/rest) als nativer Client verwendet, die separate native Clients für Android-, iOS-, Windows Universal- und Windows Phone-Geräte umfasst.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-109">It uses the [Xamarin Forms ToDoRest app](/xamarin/xamarin-forms/data-cloud/consuming/rest) as its native client, which includes separate native clients for Android, iOS, Windows Universal, and Window Phone devices.</span></span> <span data-ttu-id="a1d9f-110">Sie können das verlinkten Tutorial befolgen, um die native App zu erstellen (und die erforderlichen kostenfreien Xamarin-Tools zu installieren) und um die Xamarin-Beispielprojektmappe herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-110">You can follow the linked tutorial to create the native app (and install the necessary free Xamarin tools), as well as download the Xamarin sample solution.</span></span> <span data-ttu-id="a1d9f-111">Das Xamarin-Beispiel umfasst ein Dienstprojekt der ASP.NET-Web-API 2, das die ASP.NET Core-App aus diesem Artikel ersetzt (dabei sind keine Änderungen durch den Client erforderlich).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-111">The Xamarin sample includes an ASP.NET Web API 2 services project, which this article's ASP.NET Core app replaces (with no changes required by the client).</span></span>

![Ausführen der ToDoRest-App auf einem Android-Smartphone](native-mobile-backend/_static/todo-android.png)

### <a name="features"></a><span data-ttu-id="a1d9f-113">Features</span><span class="sxs-lookup"><span data-stu-id="a1d9f-113">Features</span></span>

<span data-ttu-id="a1d9f-114">Die ToDoRest-App unterstützt das Auflisten, Hinzufügen, Löschen und Aktualisieren von To-Do-Elementen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-114">The ToDoRest app supports listing, adding, deleting, and updating To-Do items.</span></span> <span data-ttu-id="a1d9f-115">Jedes Element verfügt über eine ID, einen Namen, Hinweise und über eine Eigenschaft, die angibt, ob ein Element abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-115">Each item has an ID, a Name, Notes, and a property indicating whether it's been Done yet.</span></span>

<span data-ttu-id="a1d9f-116">In der Hauptansicht der Elemente werden, wie oben dargestellt, die Namen der einzelnen Elemente aufgeführt. Sie sind mit einem Häkchen versehen, wenn sie abgeschlossen sind.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-116">The main view of the items, as shown above, lists each item's name and indicates if it's done with a checkmark.</span></span>

<span data-ttu-id="a1d9f-117">Durch Tippen auf das Symbol `+` wird ein Dialogfeld zum Hinzufügen eines Elements geöffnet:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-117">Tapping the `+` icon opens an add item dialog:</span></span>

![Dialogfeld „Element hinzufügen“](native-mobile-backend/_static/todo-android-new-item.png)

<span data-ttu-id="a1d9f-119">Durch Tippen auf ein Element auf dem Bildschirm mit der Hauptliste wird ein Dialogfeld zur Bearbeitung geöffnet, in dem die Einstellungen „Name“, „Hinweise“, und „Fertig“ für das Element geändert oder das Element gelöscht werden kann:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-119">Tapping an item on the main list screen opens up an edit dialog where the item's Name, Notes, and Done settings can be modified, or the item can be deleted:</span></span>

![Dialogfeld „Element bearbeiten“](native-mobile-backend/_static/todo-android-edit-item.png)

<span data-ttu-id="a1d9f-121">Dieses Beispiel ist standardmäßig für die Verwendung von Back-End-Diensten konfiguriert, die unter developer.xamarin.com gehostet werden, und in denen schreibgeschützte Vorgänge zugelassen sind.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-121">This sample is configured by default to use backend services hosted at developer.xamarin.com, which allow read-only operations.</span></span> <span data-ttu-id="a1d9f-122">Wenn Sie dies selbst bei der im nächsten Abschnitt erstellten ASP.NET Core-App testen möchten, die auf Ihrem Computer ausgeführt wird, müssen Sie die `RestUrl`-Konstante der App aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-122">To test it out yourself against the ASP.NET Core app created in the next section running on your computer, you'll need to update the app's `RestUrl` constant.</span></span> <span data-ttu-id="a1d9f-123">Navigieren Sie zu dem Projekt `ToDoREST`, und öffnen Sie die Datei *Constants.cs*.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-123">Navigate to the `ToDoREST` project and open the *Constants.cs* file.</span></span> <span data-ttu-id="a1d9f-124">Ersetzen Sie die `RestUrl` durch eine URL, die die IP-Adresse Ihres Computers enthält (nicht „localhost“ oder „127.0.0.1“, da diese Adresse vom Geräteemulator und nicht von Ihrem Computer verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-124">Replace the `RestUrl` with a URL that includes your machine's IP address (not localhost or 127.0.0.1, since this address is used from the device emulator, not from your machine).</span></span> <span data-ttu-id="a1d9f-125">Schließen Sie auch die Portnummer (5000) ein.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-125">Include the port number as well (5000).</span></span> <span data-ttu-id="a1d9f-126">Stellen Sie sicher, dass keine aktive Firewall den Zugriff auf diesen Port blockiert, wenn Sie testen möchten, ob Ihre Dienste auf einem Gerät funktionieren.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-126">In order to test that your services work with a device, ensure you don't have an active firewall blocking access to this port.</span></span>

```csharp
// URL of REST service (Xamarin ReadOnly Service)
//public static string RestUrl = "http://developer.xamarin.com:8081/api/todoitems{0}";

// use your machine's IP address
public static string RestUrl = "http://192.168.1.207:5000/api/todoitems/{0}";
```

## <a name="creating-the-aspnet-core-project"></a><span data-ttu-id="a1d9f-127">Erstellen des ASP.NET Core-Projekts</span><span class="sxs-lookup"><span data-stu-id="a1d9f-127">Creating the ASP.NET Core Project</span></span>

<span data-ttu-id="a1d9f-128">Erstellen Sie in Visual Studio eine neue ASP.NET Core-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-128">Create a new ASP.NET Core Web Application in Visual Studio.</span></span> <span data-ttu-id="a1d9f-129">Wählen Sie die Web-API-Vorlage und „Keine Authentifizierung“ aus.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-129">Choose the Web API template and No Authentication.</span></span> <span data-ttu-id="a1d9f-130">Geben Sie dem Projekt den Namen *ToDoApi*.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-130">Name the project *ToDoApi*.</span></span>

![Dialogfeld „Neue ASP.NET-Webanwendung“ mit ausgewählter Web-API-Projektvorlage](native-mobile-backend/_static/web-api-template.png)

<span data-ttu-id="a1d9f-132">Die Anwendung sollte auf alle an Port 5000 gestellten Anforderungen reagieren.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-132">The application should respond to all requests made to port 5000.</span></span> <span data-ttu-id="a1d9f-133">Aktualisieren Sie *Program.cs*, und schließen Sie `.UseUrls("http://*:5000")` ein, um Folgendes zu erreichen:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-133">Update *Program.cs* to include `.UseUrls("http://*:5000")` to achieve this:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Program.cs?range=10-16&highlight=3)]

> [!NOTE]
> <span data-ttu-id="a1d9f-134">Stellen Sie sicher, dass Sie die Anwendung direkt ausführen und nicht nach IIS Express, da dieser Dienst die nicht lokalen Anforderungen standardmäßig ignoriert.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-134">Make sure you run the application directly, rather than behind IIS Express, which ignores non-local requests by default.</span></span> <span data-ttu-id="a1d9f-135">Führen Sie [dotnet run](/dotnet/core/tools/dotnet-run) über eine Eingabeaufforderung aus, oder wählen Sie aus der Dropdownliste „Debugziel“ in der Symbolleiste von Visual Studio das Profil des Anwendungsnamens aus.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-135">Run [dotnet run](/dotnet/core/tools/dotnet-run) from a command prompt, or choose the application name profile from the Debug Target dropdown in the Visual Studio toolbar.</span></span>

<span data-ttu-id="a1d9f-136">Fügen Sie eine Modellklasse hinzu, in der die To-Do-Elemente dargestellt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-136">Add a model class to represent To-Do items.</span></span> <span data-ttu-id="a1d9f-137">Markieren Sie erforderliche Felder mit dem Attribut `[Required]`:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-137">Mark required fields using the `[Required]` attribute:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Models/ToDoItem.cs)]

<span data-ttu-id="a1d9f-138">Die API-Methoden müssen mit Daten arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-138">The API methods require some way to work with data.</span></span> <span data-ttu-id="a1d9f-139">Verwenden Sie die gleiche `IToDoRepository`-Schnittstelle, die im ursprünglichen Xamarin-Beispiel verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-139">Use the same `IToDoRepository` interface the original Xamarin sample uses:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Interfaces/IToDoRepository.cs)]

<span data-ttu-id="a1d9f-140">In diesem Beispiel verwendet die Implementierung nur eine private Sammlung von Elementen:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-140">For this sample, the implementation just uses a private collection of items:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Services/ToDoRepository.cs)]

<span data-ttu-id="a1d9f-141">Konfigurieren Sie die Implementierung in *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-141">Configure the implementation in *Startup.cs*:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Startup.cs?highlight=6&range=29-35)]

<span data-ttu-id="a1d9f-142">An diesem Punkt sind Sie bereit für die Erstellung von *ToDoItemsController*.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-142">At this point, you're ready to create the *ToDoItemsController*.</span></span>

> [!TIP]
> <span data-ttu-id="a1d9f-143">Weitere Informationen zur Erstellung von Web-APIs finden Sie unter [Build your first Web API with ASP.NET Core MVC and Visual Studio (Erstellen Ihrer ersten Web-API mit ASP.NET Core MVC und Visual Studio)](../tutorials/first-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-143">Learn more about creating web APIs in [Build your first Web API with ASP.NET Core MVC and Visual Studio](../tutorials/first-web-api.md).</span></span>

## <a name="creating-the-controller"></a><span data-ttu-id="a1d9f-144">Erstellen des Controllers</span><span class="sxs-lookup"><span data-stu-id="a1d9f-144">Creating the Controller</span></span>

<span data-ttu-id="a1d9f-145">Fügen Sie einen neuen Controller, *ToDoItemsController*, zu dem Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-145">Add a new controller to the project, *ToDoItemsController*.</span></span> <span data-ttu-id="a1d9f-146">Dieser sollte von „Microsoft.AspNetCore.Mvc.Controller“ erben.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-146">It should inherit from Microsoft.AspNetCore.Mvc.Controller.</span></span> <span data-ttu-id="a1d9f-147">Fügen Sie das Attribut `Route` hinzu, um anzugeben, dass der Controller Anforderungen für Pfade bearbeitet, die mit `api/todoitems` beginnen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-147">Add a `Route` attribute to indicate that the controller will handle requests made to paths starting with `api/todoitems`.</span></span> <span data-ttu-id="a1d9f-148">Das Token `[controller]` in der Route wird durch den Namen des Controllers ersetzt (dabei wird das Suffix `Controller` ausgelassen) und ist für globale Routen besonders nützlich.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-148">The `[controller]` token in the route is replaced by the name of the controller (omitting the `Controller` suffix), and is especially helpful for global routes.</span></span> <span data-ttu-id="a1d9f-149">Weitere Informationen zu [Routing](../fundamentals/routing.md).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-149">Learn more about [routing](../fundamentals/routing.md).</span></span>

<span data-ttu-id="a1d9f-150">Damit der Controller funktioniert, ist eine `IToDoRepository`-Schnittstelle erforderlich. Fordern Sie über den Konstruktor des Controllers eine Instanz dieses Typs an.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-150">The controller requires an `IToDoRepository` to function; request an instance of this type through the controller's constructor.</span></span> <span data-ttu-id="a1d9f-151">Zur Laufzeit wird diese Instanz über die Frameworkunterstützung für [Dependency Injection](../fundamentals/dependency-injection.md) bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-151">At runtime, this instance will be provided using the framework's support for [dependency injection](../fundamentals/dependency-injection.md).</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=1-17&highlight=9,14)]

<span data-ttu-id="a1d9f-152">Diese API unterstützt vier verschiedene HTTP-Verben zur Durchführung von CRUD-Vorgängen für die Datenquelle (CRUD = Create, Read, Update, Delete; Erstellen, Lesen, Aktualisieren, Löschen).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-152">This API supports four different HTTP verbs to perform CRUD (Create, Read, Update, Delete) operations on the data source.</span></span> <span data-ttu-id="a1d9f-153">Am einfachsten ist der Lesevorgang, der einer HTTP GET-Anforderung entspricht.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-153">The simplest of these is the Read operation, which corresponds to an HTTP GET request.</span></span>

### <a name="reading-items"></a><span data-ttu-id="a1d9f-154">Lesen von Elementen</span><span class="sxs-lookup"><span data-stu-id="a1d9f-154">Reading Items</span></span>

<span data-ttu-id="a1d9f-155">Die Anforderung einer Liste mit Elementen erfolgt über eine GET-Anforderung an die Methode `List`.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-155">Requesting a list of items is done with a GET request to the `List` method.</span></span> <span data-ttu-id="a1d9f-156">Das Attribut `[HttpGet]` in der Methode `List` gibt an, dass diese Aktion nur GET-Anforderungen verarbeiten soll.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-156">The `[HttpGet]` attribute on the `List` method indicates that this action should only handle GET requests.</span></span> <span data-ttu-id="a1d9f-157">Die Route für diese Aktion ist die auf dem Controller angegebene Route.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-157">The route for this action is the route specified on the controller.</span></span> <span data-ttu-id="a1d9f-158">Sie müssen den Aktionsnamen nicht unbedingt als Teil der Route verwenden.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-158">You don't necessarily need to use the action name as part of the route.</span></span> <span data-ttu-id="a1d9f-159">Sie müssen nur sicherstellen, dass die einzelnen Aktionen über eine eindeutige Route verfügen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-159">You just need to ensure each action has a unique and unambiguous route.</span></span> <span data-ttu-id="a1d9f-160">Routingattribute können auf Controller- und auf Methodenebene für die Erstellung bestimmter Routen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-160">Routing attributes can be applied at both the controller and method levels to build up specific routes.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=19-23)]

<span data-ttu-id="a1d9f-161">Die Methode `List` gibt den Antwortcode „200 OK“ und alle als JSON serialisierten To-Do-Elemente zurück.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-161">The `List` method returns a 200 OK response code and all of the ToDo items, serialized as JSON.</span></span>

<span data-ttu-id="a1d9f-162">Sie können Ihre neue API-Methode mit einer Vielzahl von Tools testen, z.B. wie im Folgenden dargestellt mit [Postman](https://www.getpostman.com/docs/):</span><span class="sxs-lookup"><span data-stu-id="a1d9f-162">You can test your new API method using a variety of tools, such as [Postman](https://www.getpostman.com/docs/), shown here:</span></span>

![Postman-Konsole mit einer GET-Anforderung für To-Do-Elemente und dem Antworttext, in dem die JSON für drei zurückgegebene Elemente angezeigt wird](native-mobile-backend/_static/postman-get.png)

### <a name="creating-items"></a><span data-ttu-id="a1d9f-164">Erstellen von Elementen</span><span class="sxs-lookup"><span data-stu-id="a1d9f-164">Creating Items</span></span>

<span data-ttu-id="a1d9f-165">Gemäß der Konvention wird die Erstellung neuer Datenelemente dem HTTP POST-Verb zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-165">By convention, creating new data items is mapped to the HTTP POST verb.</span></span> <span data-ttu-id="a1d9f-166">Auf die Methode `Create` wird das Attribut `[HttpPost]` angewendet, und sie akzeptiert eine `ToDoItem`-Instanz.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-166">The `Create` method has an `[HttpPost]` attribute applied to it, and accepts a `ToDoItem` instance.</span></span> <span data-ttu-id="a1d9f-167">Da das Argument `item` im POST-Text übergeben wird, wird dieser Parameter mit dem Attribut `[FromBody]` versehen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-167">Since the `item` argument will be passed in the body of the POST, this parameter is decorated with the `[FromBody]` attribute.</span></span>

<span data-ttu-id="a1d9f-168">Innerhalb der Methode wird überprüft, ob das Element gültig ist und ob es bereits im Datenspeicher vorhanden ist. Wenn keine Probleme auftreten, wird es über das Repository hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-168">Inside the method, the item is checked for validity and prior existence in the data store, and if no issues occur, it's added using the repository.</span></span> <span data-ttu-id="a1d9f-169">Bei der Überprüfung von `ModelState.IsValid` wird eine [Modellvalidierung](../mvc/models/validation.md) durchgeführt. Dies sollte bei jeder API-Methode geschehen, die Benutzereingaben akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-169">Checking `ModelState.IsValid` performs [model validation](../mvc/models/validation.md), and should be done in every API method that accepts user input.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=25-46)]

<span data-ttu-id="a1d9f-170">Im Beispiel wird eine Enumeration mit Fehlercodes verwendet, die an den mobilen Client übergeben werden:</span><span class="sxs-lookup"><span data-stu-id="a1d9f-170">The sample uses an enum containing error codes that are passed to the mobile client:</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=91-99)]

<span data-ttu-id="a1d9f-171">Testen Sie das Hinzufügen neuer Elemente mithilfe von Postman, indem Sie das POST-Verb auswählen und im Anforderungstext das neue Objekt im JSON-Format angeben.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-171">Test adding new items using Postman by choosing the POST verb providing the new object in JSON format in the Body of the request.</span></span> <span data-ttu-id="a1d9f-172">Sie sollten auch einen Anforderungsheader hinzufügen, in dem ein `Content-Type` von `application/json` angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-172">You should also add a request header specifying a `Content-Type` of `application/json`.</span></span>

![Postman-Konsole mit einem POST-Verb und einer Antwort](native-mobile-backend/_static/postman-post.png)

<span data-ttu-id="a1d9f-174">Die Methode gibt das neu erstellte Element in der Antwort zurück.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-174">The method returns the newly created item in the response.</span></span>

### <a name="updating-items"></a><span data-ttu-id="a1d9f-175">Aktualisieren von Elementen</span><span class="sxs-lookup"><span data-stu-id="a1d9f-175">Updating Items</span></span>

<span data-ttu-id="a1d9f-176">Datensätze werden mithilfe von HTTP PUT-Anforderungen geändert.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-176">Modifying records is done using HTTP PUT requests.</span></span> <span data-ttu-id="a1d9f-177">Abgesehen von dieser Änderung ist die Methode `Edit` mit der Methode `Create` weitgehend identisch.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-177">Other than this change, the `Edit` method is almost identical to `Create`.</span></span> <span data-ttu-id="a1d9f-178">Beachten Sie, dass die Aktion `Edit` die Antwort „`NotFound` (404)“ zurückgibt, wenn der Datensatz nicht gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-178">Note that if the record isn't found, the `Edit` action will return a `NotFound` (404) response.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=48-69)]

<span data-ttu-id="a1d9f-179">Ändern Sie zum Testen mit Postman das Verb in PUT.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-179">To test with Postman, change the verb to PUT.</span></span> <span data-ttu-id="a1d9f-180">Geben Sie die aktualisierten Objektdaten in den Anforderungstext ein.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-180">Specify the updated object data in the Body of the request.</span></span>

![Postman-Konsole mit einem PUT-Verb und einer Antwort](native-mobile-backend/_static/postman-put.png)

<span data-ttu-id="a1d9f-182">Diese Methode gibt bei erfolgreicher Ausführung die Antwort „`NoContent` (204)“ für die Konsistenz mit der bereits vorhandenen API zurück.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-182">This method returns a `NoContent` (204) response when successful, for consistency with the pre-existing API.</span></span>

### <a name="deleting-items"></a><span data-ttu-id="a1d9f-183">Löschen von Elementen</span><span class="sxs-lookup"><span data-stu-id="a1d9f-183">Deleting Items</span></span>

<span data-ttu-id="a1d9f-184">Datensätze werden gelöscht, indem DELETE-Anforderungen an den Dienst gestellt werden und die ID des zu löschenden Elements übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-184">Deleting records is accomplished by making DELETE requests to the service, and passing the ID of the item to be deleted.</span></span> <span data-ttu-id="a1d9f-185">Wie bei Updates erhalten Anforderungen bei nicht vorhandenen Elementen die Antwort `NotFound`.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-185">As with updates, requests for items that don't exist will receive `NotFound` responses.</span></span> <span data-ttu-id="a1d9f-186">Bei erfolgreicher Ausführung einer Anforderung hingegen wird die Antwort „`NoContent` (204)“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-186">Otherwise, a successful request will get a `NoContent` (204) response.</span></span>

[!code-csharp[](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=71-88)]

<span data-ttu-id="a1d9f-187">Beachten Sie, dass beim Testen der DELETE-Funktion im Anforderungstext nichts erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-187">Note that when testing the delete functionality, nothing is required in the Body of the request.</span></span>

![Postman-Konsole mit einer DELETE-Funktion und einer Antwort](native-mobile-backend/_static/postman-delete.png)

## <a name="common-web-api-conventions"></a><span data-ttu-id="a1d9f-189">Allgemeine Konventionen für die Web-API</span><span class="sxs-lookup"><span data-stu-id="a1d9f-189">Common Web API Conventions</span></span>

<span data-ttu-id="a1d9f-190">Da Sie die Back-End-Dienste für Ihre App entwickeln, sollten Sie sich auch eine Reihe von konsistenten Konventionen oder Richtlinien für den Umgang mit bereichsübergreifenden Anliegen überlegen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-190">As you develop the backend services for your app, you will want to come up with a consistent set of conventions or policies for handling cross-cutting concerns.</span></span> <span data-ttu-id="a1d9f-191">Im oben dargestellten Dienst haben Anforderungen für bestimmte Datensätze, die nicht gefunden werden konnten, beispielsweise die Antwort `NotFound` statt der Antwort `BadRequest` erhalten.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-191">For example, in the service shown above, requests for specific records that weren't found received a `NotFound` response, rather than a `BadRequest` response.</span></span> <span data-ttu-id="a1d9f-192">Gleichermaßen haben für diesen Dienst durchgeführte Befehle, die gebundene Modelltypen übergeben haben, immer `ModelState.IsValid` überprüft und bei ungültigen Modelltypen eine `BadRequest` zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-192">Similarly, commands made to this service that passed in model bound types always checked `ModelState.IsValid` and returned a `BadRequest` for invalid model types.</span></span>

<span data-ttu-id="a1d9f-193">Sobald Sie eine gängige Richtlinie für Ihre APIs ermittelt haben, können Sie diese in der Regel in einen [Filter](../mvc/controllers/filters.md) einschließen.</span><span class="sxs-lookup"><span data-stu-id="a1d9f-193">Once you've identified a common policy for your APIs, you can usually encapsulate it in a [filter](../mvc/controllers/filters.md).</span></span> <span data-ttu-id="a1d9f-194">Weitere Informationen zum [Einschließen gängiger API-Richtlinien in ASP.NET Core MVC-Anwendungen](https://msdn.microsoft.com/magazine/mt767699.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1d9f-194">Learn more about [how to encapsulate common API policies in ASP.NET Core MVC applications](https://msdn.microsoft.com/magazine/mt767699.aspx).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1d9f-195">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a1d9f-195">Additional resources</span></span>

* [<span data-ttu-id="a1d9f-196">Authentifizierung und Autorisierung</span><span class="sxs-lookup"><span data-stu-id="a1d9f-196">Authentication and Authorization</span></span>](/xamarin/xamarin-forms/enterprise-application-patterns/authentication-and-authorization)
