---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Aufruft eine Web-API von einem .NET-Client (c#)-ASP.NET 4. x
author: MikeWasson
description: In diesem Tutorial wird gezeigt, wie Sie eine Web-API aus einer .NET 4. x-Anwendung abrufen.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172938"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="41059-103">Aufruft eine Web-API über einen .NET-Client (c#).</span><span class="sxs-lookup"><span data-stu-id="41059-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="41059-104">von [Mike Wasson](https://github.com/MikeWasson) und [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="41059-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="41059-105">Das [abgeschlossene Projekt herunterladen](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="41059-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="41059-106">[Anweisungen zum Download.](/aspnet/core/tutorials/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="41059-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="41059-107">In diesem Tutorial wird gezeigt, wie Sie eine Web-API mithilfe von [System .net. http. HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx) aus einer .NET-Anwendung abrufen.</span><span class="sxs-lookup"><span data-stu-id="41059-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="41059-108">In diesem Tutorial wird eine Client-App geschrieben, die die folgende Web-API nutzt:</span><span class="sxs-lookup"><span data-stu-id="41059-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="41059-109">Aktion</span><span class="sxs-lookup"><span data-stu-id="41059-109">Action</span></span> | <span data-ttu-id="41059-110">HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="41059-110">HTTP method</span></span> | <span data-ttu-id="41059-111">Relativer URI</span><span class="sxs-lookup"><span data-stu-id="41059-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41059-112">Abrufen eines Produkts nach ID</span><span class="sxs-lookup"><span data-stu-id="41059-112">Get a product by ID</span></span> | <span data-ttu-id="41059-113">GET</span><span class="sxs-lookup"><span data-stu-id="41059-113">GET</span></span> | <span data-ttu-id="41059-114">/API/Products/-*ID*</span><span class="sxs-lookup"><span data-stu-id="41059-114">/api/products/*id*</span></span> |
| <span data-ttu-id="41059-115">Erstellen eines neuen Produkts</span><span class="sxs-lookup"><span data-stu-id="41059-115">Create a new product</span></span> | <span data-ttu-id="41059-116">POST</span><span class="sxs-lookup"><span data-stu-id="41059-116">POST</span></span> | <span data-ttu-id="41059-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="41059-117">/api/products</span></span> |
| <span data-ttu-id="41059-118">Aktualisieren eines Produkts</span><span class="sxs-lookup"><span data-stu-id="41059-118">Update a product</span></span> | <span data-ttu-id="41059-119">PUT</span><span class="sxs-lookup"><span data-stu-id="41059-119">PUT</span></span> | <span data-ttu-id="41059-120">/API/Products/-*ID*</span><span class="sxs-lookup"><span data-stu-id="41059-120">/api/products/*id*</span></span> |
| <span data-ttu-id="41059-121">Löschen eines Produkts</span><span class="sxs-lookup"><span data-stu-id="41059-121">Delete a product</span></span> | <span data-ttu-id="41059-122">Delete</span><span class="sxs-lookup"><span data-stu-id="41059-122">DELETE</span></span> | <span data-ttu-id="41059-123">/API/Products/-*ID*</span><span class="sxs-lookup"><span data-stu-id="41059-123">/api/products/*id*</span></span> |

<span data-ttu-id="41059-124">Informationen dazu, wie Sie diese API mit ASP.net-Web-API implementieren, finden Sie unter [Erstellen einer Web-API, die CRUD-Vorgänge unterstützt](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="41059-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="41059-125">Der Einfachheit halber handelt es sich bei der Client Anwendung in diesem Tutorial um eine Windows-Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="41059-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="41059-126">**HttpClient** wird auch für Windows Phone-und Windows Store-Apps unterstützt.</span><span class="sxs-lookup"><span data-stu-id="41059-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="41059-127">Weitere Informationen finden Sie unter [Schreiben von Web-API-Client Code für mehrere Plattformen mit portablen Bibliotheken](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="41059-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<span data-ttu-id="41059-128">**Hinweis:** Wenn Sie Basis-URLs und relative URIs als hart codierte Werte übergeben, beachten Sie die Regeln für die Verwendung der `HttpClient` API.</span><span class="sxs-lookup"><span data-stu-id="41059-128">**NOTE:** If you pass base URLs and relative URIs as hard-coded values, be mindful of the rules for utilizing the `HttpClient` API.</span></span> <span data-ttu-id="41059-129">Die- `HttpClient.BaseAddress` Eigenschaft sollte auf eine Adresse mit einem nachstehenden Schrägstrich () festgelegt werden `/` .</span><span class="sxs-lookup"><span data-stu-id="41059-129">The `HttpClient.BaseAddress` property should be set to an address with a trailing forward slash (`/`).</span></span> <span data-ttu-id="41059-130">Wenn Sie z. b. hart codierte Ressourcen-URIs an die- `HttpClient.GetAsync` Methode übergeben, schließen Sie keinen führenden Schrägstrich ein.</span><span class="sxs-lookup"><span data-stu-id="41059-130">For example, when passing hard-coded resource URIs to the `HttpClient.GetAsync` method, don't include a leading forward slash.</span></span> <span data-ttu-id="41059-131">So erhalten Sie eine `Product` nach ID:</span><span class="sxs-lookup"><span data-stu-id="41059-131">To get a `Product` by ID:</span></span>

1. <span data-ttu-id="41059-132">Set`client.BaseAddress = new Uri("https://localhost:5001/");`</span><span class="sxs-lookup"><span data-stu-id="41059-132">Set `client.BaseAddress = new Uri("https://localhost:5001/");`</span></span>
1. <span data-ttu-id="41059-133">Anfordern einer `Product` .</span><span class="sxs-lookup"><span data-stu-id="41059-133">Request a `Product`.</span></span> <span data-ttu-id="41059-134">Beispiel: `client.GetAsync<Product>("api/products/4");`.</span><span class="sxs-lookup"><span data-stu-id="41059-134">For example, `client.GetAsync<Product>("api/products/4");`.</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="41059-135">Erstellen der Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="41059-135">Create the Console Application</span></span>

<span data-ttu-id="41059-136">Erstellen Sie in Visual Studio eine neue Windows-Konsolen-App mit dem Namen " **httpclientsample** ", und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="41059-136">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="41059-137">Der vorangehende Code ist die komplette Client-App.</span><span class="sxs-lookup"><span data-stu-id="41059-137">The preceding code is the complete client app.</span></span>

<span data-ttu-id="41059-138">`RunAsync`wird ausgeführt, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="41059-138">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="41059-139">Die meisten **HttpClient** -Methoden sind asynchron, da Sie Netzwerk-e/a-Vorgänge durchführen.</span><span class="sxs-lookup"><span data-stu-id="41059-139">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="41059-140">Alle asynchronen Aufgaben werden innerhalb von durchgeführt `RunAsync` .</span><span class="sxs-lookup"><span data-stu-id="41059-140">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="41059-141">Normalerweise blockiert eine APP den Haupt Thread nicht, aber diese APP lässt keine Interaktion zu.</span><span class="sxs-lookup"><span data-stu-id="41059-141">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="41059-142">Installieren der Web-API-Client Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="41059-142">Install the Web API Client Libraries</span></span>

<span data-ttu-id="41059-143">Verwenden Sie den nuget-Paket-Manager zum Installieren des Web-API-Client Bibliotheks Pakets.</span><span class="sxs-lookup"><span data-stu-id="41059-143">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="41059-144">Wählen Sie im Menü **Extras** die Optionen **NuGet-Paket-Manager** > **Paket-Manager-Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="41059-144">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="41059-145">Geben Sie in der Paket-Manager-Konsole (PMC) den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="41059-145">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="41059-146">Mit dem vorangehenden Befehl werden dem Projekt die folgenden nuget-Pakete hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="41059-146">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="41059-147">Microsoft. Aspnet. WebAPI. Client</span><span class="sxs-lookup"><span data-stu-id="41059-147">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="41059-148">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="41059-148">Newtonsoft.Json</span></span>

<span data-ttu-id="41059-149">Netwonsoft. JSON (auch als JSON.net bezeichnet) ist ein gängiges hochleistungsfähiges JSON-Framework für .net.</span><span class="sxs-lookup"><span data-stu-id="41059-149">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="41059-150">Hinzufügen einer Modell Klasse</span><span class="sxs-lookup"><span data-stu-id="41059-150">Add a Model Class</span></span>

<span data-ttu-id="41059-151">Überprüfen Sie die `Product`-Klasse:</span><span class="sxs-lookup"><span data-stu-id="41059-151">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="41059-152">Diese Klasse entspricht dem Datenmodell, das von der Web-API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41059-152">This class matches the data model used by the web API.</span></span> <span data-ttu-id="41059-153">Eine APP kann **HttpClient** verwenden, um eine- `Product` Instanz aus einer HTTP-Antwort zu lesen.</span><span class="sxs-lookup"><span data-stu-id="41059-153">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="41059-154">Die APP muss keinen Deserialisierungscode schreiben.</span><span class="sxs-lookup"><span data-stu-id="41059-154">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="41059-155">Erstellen und Initialisieren von httpclient</span><span class="sxs-lookup"><span data-stu-id="41059-155">Create and Initialize HttpClient</span></span>

<span data-ttu-id="41059-156">Überprüfen Sie die statische **HttpClient** -Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="41059-156">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="41059-157">**HttpClient** soll einmal instanziiert und während der gesamten Lebensdauer einer Anwendung wieder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="41059-157">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="41059-158">Die folgenden Bedingungen können zu **SocketException** -Fehlern führen:</span><span class="sxs-lookup"><span data-stu-id="41059-158">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="41059-159">Erstellen einer neuen **HttpClient** -Instanz pro Anforderung.</span><span class="sxs-lookup"><span data-stu-id="41059-159">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="41059-160">Server mit starker Auslastung.</span><span class="sxs-lookup"><span data-stu-id="41059-160">Server under heavy load.</span></span>

<span data-ttu-id="41059-161">Durch das Erstellen einer neuen **HttpClient** -Instanz pro Anforderung können die verfügbaren Sockets erschöpft werden.</span><span class="sxs-lookup"><span data-stu-id="41059-161">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="41059-162">Der folgende Code initialisiert die **HttpClient** -Instanz:</span><span class="sxs-lookup"><span data-stu-id="41059-162">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="41059-163">Der vorangehende Code:</span><span class="sxs-lookup"><span data-stu-id="41059-163">The preceding code:</span></span>

* <span data-ttu-id="41059-164">Legt den Basis-URI für HTTP-Anforderungen fest.</span><span class="sxs-lookup"><span data-stu-id="41059-164">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="41059-165">Ändern Sie die Portnummer in den Port, der in der Server-App verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41059-165">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="41059-166">Die APP funktioniert nur, wenn für die Server-App ein Port verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41059-166">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="41059-167">Legt den Accept-Header auf "application/json" fest.</span><span class="sxs-lookup"><span data-stu-id="41059-167">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="41059-168">Das Festlegen dieses Headers weist den Server an, Daten im JSON-Format zu senden.</span><span class="sxs-lookup"><span data-stu-id="41059-168">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="41059-169">Senden einer GET-Anforderung zum Abrufen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="41059-169">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="41059-170">Der folgende Code sendet eine GET-Anforderung für ein Produkt:</span><span class="sxs-lookup"><span data-stu-id="41059-170">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="41059-171">Die **getasync** -Methode sendet die HTTP GET-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="41059-171">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="41059-172">Wenn die Methode abgeschlossen ist, gibt Sie eine **httpresponanmessage** zurück, die die HTTP-Antwort enthält.</span><span class="sxs-lookup"><span data-stu-id="41059-172">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="41059-173">Wenn der Statuscode in der Antwort ein Erfolgs Code ist, enthält der Antworttext die JSON-Darstellung eines Produkts.</span><span class="sxs-lookup"><span data-stu-id="41059-173">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="41059-174">Aufrufen von "read **asasync** " zum Deserialisieren der JSON-Nutzlast in eine- `Product` Instanz.</span><span class="sxs-lookup"><span data-stu-id="41059-174">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="41059-175">Die "read **asasync** "-Methode ist asynchron, da der Antworttext beliebig groß sein kann.</span><span class="sxs-lookup"><span data-stu-id="41059-175">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="41059-176">**HttpClient** löst keine Ausnahme aus, wenn die HTTP-Antwort einen Fehlercode enthält.</span><span class="sxs-lookup"><span data-stu-id="41059-176">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="41059-177">Stattdessen ist die **issuccess Statuscode** -Eigenschaft **false** , wenn der Status ein Fehlercode ist.</span><span class="sxs-lookup"><span data-stu-id="41059-177">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="41059-178">Wenn Sie HTTP-Fehlercodes als Ausnahmen behandeln möchten, rufen Sie [HttpResponseMessage. ensuresuccmestatuscode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) für das Response-Objekt auf.</span><span class="sxs-lookup"><span data-stu-id="41059-178">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="41059-179">`EnsureSuccessStatusCode`löst eine Ausnahme aus, wenn der Statuscode außerhalb des Bereichs 200 &ndash; 299 liegt.</span><span class="sxs-lookup"><span data-stu-id="41059-179">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="41059-180">Beachten Sie, dass **HttpClient** Ausnahmen aus anderen Gründen auslösen kann &mdash; , z. b. bei einem Timeout der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="41059-180">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="41059-181">Zu deserialisierende Medientyp-Formatierer</span><span class="sxs-lookup"><span data-stu-id="41059-181">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="41059-182">Wenn " **leseasasync** " ohne Parameter aufgerufen wird, wird ein Standardsatz von *Medien Formatierern* verwendet, um den Antworttext zu lesen.</span><span class="sxs-lookup"><span data-stu-id="41059-182">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="41059-183">Die Standardformatierer unterstützen JSON-, XML-und Formular-URL-codierte Daten.</span><span class="sxs-lookup"><span data-stu-id="41059-183">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="41059-184">Anstatt die Standard Formatierer zu verwenden, können Sie eine Liste von Formatierern für die Methode "read **asasync** " bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="41059-184">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="41059-185">Die Verwendung einer Liste von Formatierern ist nützlich, wenn Sie über einen benutzerdefinierten Medientyp Formatierer verfügen:</span><span class="sxs-lookup"><span data-stu-id="41059-185">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="41059-186">Weitere Informationen finden Sie unter [Media Formatters in ASP.net-Web-API 2](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="41059-186">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="41059-187">Senden einer POST-Anforderung zum Erstellen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="41059-187">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="41059-188">Der folgende Code sendet eine Post-Anforderung, die eine- `Product` Instanz im JSON-Format enthält:</span><span class="sxs-lookup"><span data-stu-id="41059-188">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="41059-189">Die **postasjsonasync** -Methode:</span><span class="sxs-lookup"><span data-stu-id="41059-189">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="41059-190">Serialisiert ein Objekt in JSON.</span><span class="sxs-lookup"><span data-stu-id="41059-190">Serializes an object to JSON.</span></span>
* <span data-ttu-id="41059-191">Sendet die JSON-Nutzlast in einer POST-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="41059-191">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="41059-192">Wenn die Anforderung erfolgreich ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="41059-192">If the request succeeds:</span></span>

* <span data-ttu-id="41059-193">Es sollte eine 201-Antwort (created) zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="41059-193">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="41059-194">Die Antwort sollte die URL der erstellten Ressourcen im Location-Header enthalten.</span><span class="sxs-lookup"><span data-stu-id="41059-194">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="41059-195">Senden einer Put-Anforderung zum Aktualisieren einer Ressource</span><span class="sxs-lookup"><span data-stu-id="41059-195">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="41059-196">Der folgende Code sendet eine PUT-Anforderung zum Aktualisieren eines Produkts:</span><span class="sxs-lookup"><span data-stu-id="41059-196">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="41059-197">Die **putasjsonasync** -Methode funktioniert wie **postasjsonasync**, mit dem Unterschied, dass Sie eine PUT-Anforderung anstelle von Post sendet.</span><span class="sxs-lookup"><span data-stu-id="41059-197">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="41059-198">Hiermit wird eine DELETE-Anforderung zum Löschen einer Ressource gesendet.</span><span class="sxs-lookup"><span data-stu-id="41059-198">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="41059-199">Der folgende Code sendet eine DELETE-Anforderung zum Löschen eines Produkts:</span><span class="sxs-lookup"><span data-stu-id="41059-199">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="41059-200">Wie bei Get hat eine Löschanforderung keinen Anforderungs Text.</span><span class="sxs-lookup"><span data-stu-id="41059-200">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="41059-201">Sie müssen das JSON-oder XML-Format nicht mit DELETE angeben.</span><span class="sxs-lookup"><span data-stu-id="41059-201">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="41059-202">Testen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="41059-202">Test the sample</span></span>

<span data-ttu-id="41059-203">So testen Sie die Client-App:</span><span class="sxs-lookup"><span data-stu-id="41059-203">To test the client app:</span></span>

1. <span data-ttu-id="41059-204">[Herunterladen](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) und Ausführen der Server-app.</span><span class="sxs-lookup"><span data-stu-id="41059-204">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="41059-205">[Anweisungen zum Download.](/aspnet/core/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="41059-205">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="41059-206">Überprüfen Sie, ob die Server-APP funktioniert.</span><span class="sxs-lookup"><span data-stu-id="41059-206">Verify the server app is working.</span></span> <span data-ttu-id="41059-207">Beispielsweise `http://localhost:64195/api/products` sollte eine Liste der Produkte zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="41059-207">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="41059-208">Legen Sie den Basis-URI für HTTP-Anforderungen fest.</span><span class="sxs-lookup"><span data-stu-id="41059-208">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="41059-209">Ändern Sie die Portnummer in den Port, der in der Server-App verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="41059-209">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="41059-210">Führen Sie die Client-App aus.</span><span class="sxs-lookup"><span data-stu-id="41059-210">Run the client app.</span></span> <span data-ttu-id="41059-211">Es wird die folgende Ausgabe generiert:</span><span class="sxs-lookup"><span data-stu-id="41059-211">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
