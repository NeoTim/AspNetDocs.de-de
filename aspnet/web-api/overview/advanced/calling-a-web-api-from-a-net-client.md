---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: Aufrufen eine Web-API aus einem .NET-Client (C#) – ASP.NET 4.x
author: MikeWasson
description: In diesem Tutorial veranschaulicht, wie eine Web-API über eine .NET 4.x-Anwendung aufgerufen wird.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 113600ca1e77ae9667465464da505478fc948c9b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421107"
---
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="b2c84-103">Aufrufen einer Webs-API aus einem .NET-Client (c#)</span><span class="sxs-lookup"><span data-stu-id="b2c84-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="b2c84-104">durch [Mike Wasson](https://github.com/MikeWasson) und [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b2c84-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b2c84-105">[Herunterladen des abgeschlossenen Projekts](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span><span class="sxs-lookup"><span data-stu-id="b2c84-105">[Download Completed Project](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="b2c84-106">[Anweisungen zum Download.](/aspnet/core/tutorials/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="b2c84-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="b2c84-107">In diesem Tutorial wird gezeigt, wie eine Web-API aufrufen, aus einer .NET-Anwendung mit [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2c84-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="b2c84-108">In diesem Tutorial wird eine Client-app geschrieben, die die folgende Web-API nutzt:</span><span class="sxs-lookup"><span data-stu-id="b2c84-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="b2c84-109">Aktion</span><span class="sxs-lookup"><span data-stu-id="b2c84-109">Action</span></span> | <span data-ttu-id="b2c84-110">HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="b2c84-110">HTTP method</span></span> | <span data-ttu-id="b2c84-111">Relativer URI</span><span class="sxs-lookup"><span data-stu-id="b2c84-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2c84-112">Abrufen eines Produkts nach ID</span><span class="sxs-lookup"><span data-stu-id="b2c84-112">Get a product by ID</span></span> | <span data-ttu-id="b2c84-113">GET</span><span class="sxs-lookup"><span data-stu-id="b2c84-113">GET</span></span> | <span data-ttu-id="b2c84-114">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b2c84-114">/api/products/*id*</span></span> |
| <span data-ttu-id="b2c84-115">Erstellen eines neuen Produkts</span><span class="sxs-lookup"><span data-stu-id="b2c84-115">Create a new product</span></span> | <span data-ttu-id="b2c84-116">POST</span><span class="sxs-lookup"><span data-stu-id="b2c84-116">POST</span></span> | <span data-ttu-id="b2c84-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="b2c84-117">/api/products</span></span> |
| <span data-ttu-id="b2c84-118">Aktualisieren eines Produkts</span><span class="sxs-lookup"><span data-stu-id="b2c84-118">Update a product</span></span> | <span data-ttu-id="b2c84-119">PUT</span><span class="sxs-lookup"><span data-stu-id="b2c84-119">PUT</span></span> | <span data-ttu-id="b2c84-120">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b2c84-120">/api/products/*id*</span></span> |
| <span data-ttu-id="b2c84-121">Löschen eines Produkts</span><span class="sxs-lookup"><span data-stu-id="b2c84-121">Delete a product</span></span> | <span data-ttu-id="b2c84-122">DELETE</span><span class="sxs-lookup"><span data-stu-id="b2c84-122">DELETE</span></span> | <span data-ttu-id="b2c84-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b2c84-123">/api/products/*id*</span></span> |

<span data-ttu-id="b2c84-124">Gewusst wie: Implementieren Sie diese API mit ASP.NET Web-API finden Sie unter [erstellen eine Web-API, CRUD-Vorgänge unterstützt](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span><span class="sxs-lookup"><span data-stu-id="b2c84-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="b2c84-125">Der Einfachheit halber ist die Client-Anwendung in diesem Tutorial eine Windows-Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="b2c84-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="b2c84-126">**"HttpClient"** wird auch für Windows Phone und Windows Store-apps unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b2c84-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="b2c84-127">Weitere Informationen finden Sie unter [Schreiben von Web-API-Client-Code für mehrere Plattformen mithilfe von portablen Bibliotheken](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2c84-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="b2c84-128">Erstellen der Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="b2c84-128">Create the Console Application</span></span>

<span data-ttu-id="b2c84-129">Erstellen Sie in Visual Studio eine neue Windows-Konsolen-app mit dem Namen **HttpClientSample** und fügen Sie in den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="b2c84-129">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="b2c84-130">Der vorangehende Code ist die vollständige Client-app.</span><span class="sxs-lookup"><span data-stu-id="b2c84-130">The preceding code is the complete client app.</span></span>

`RunAsync` <span data-ttu-id="b2c84-131">Ausführungen und blockiert, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="b2c84-131">runs and blocks until it completes.</span></span> <span data-ttu-id="b2c84-132">Die meisten **"HttpClient"** Methoden sind asynchrone, da sie die Netzwerk-e/a ausführen.</span><span class="sxs-lookup"><span data-stu-id="b2c84-132">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="b2c84-133">Alle asynchronen Vorgänge erfolgen in `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="b2c84-133">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="b2c84-134">Normalerweise eine app den Hauptthread blockiert nicht, aber diese app nicht eingreifen kann.</span><span class="sxs-lookup"><span data-stu-id="b2c84-134">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="b2c84-135">Installieren Sie die Web-API-Client-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="b2c84-135">Install the Web API Client Libraries</span></span>

<span data-ttu-id="b2c84-136">Verwenden Sie NuGet Package Manager zum Installieren des Pakets für die Web-API-Client-Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="b2c84-136">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="b2c84-137">Öffnen Sie das Menü **Extras**, und wählen Sie **NuGet-Paket-Manager** > **Paket-Manager-Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="b2c84-137">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="b2c84-138">Geben Sie in der Paket-Manager-Konsole (PMC), den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="b2c84-138">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="b2c84-139">Der vorherige Befehl fügt die folgenden NuGet-Pakete dem Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="b2c84-139">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="b2c84-140">Microsoft.AspNet.WebApi.Client</span><span class="sxs-lookup"><span data-stu-id="b2c84-140">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="b2c84-141">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="b2c84-141">Newtonsoft.Json</span></span>

<span data-ttu-id="b2c84-142">Json.NET ist ein gängiges Hochleistungs-JSON-Framework für .NET.</span><span class="sxs-lookup"><span data-stu-id="b2c84-142">Json.NET is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="b2c84-143">Hinzufügen einer Modellklasse</span><span class="sxs-lookup"><span data-stu-id="b2c84-143">Add a Model Class</span></span>

<span data-ttu-id="b2c84-144">Überprüfen Sie die `Product`-Klasse:</span><span class="sxs-lookup"><span data-stu-id="b2c84-144">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="b2c84-145">Diese Klasse entspricht, das Datenmodell, die von der Web-API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b2c84-145">This class matches the data model used by the web API.</span></span> <span data-ttu-id="b2c84-146">Eine app kann verwenden **"HttpClient"** zum Lesen einer `Product` -Instanz anhand einer HTTP-Antwort.</span><span class="sxs-lookup"><span data-stu-id="b2c84-146">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="b2c84-147">Die app keine Deserialisierungscode zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="b2c84-147">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="b2c84-148">Erstellen und Initialisieren von "HttpClient"</span><span class="sxs-lookup"><span data-stu-id="b2c84-148">Create and Initialize HttpClient</span></span>

<span data-ttu-id="b2c84-149">Überprüfen Sie die statische **"HttpClient"** Eigenschaft:</span><span class="sxs-lookup"><span data-stu-id="b2c84-149">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="b2c84-150">**"HttpClient"** einmal instanziiert werden soll und während der Lebensdauer einer Anwendung wiederverwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b2c84-150">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="b2c84-151">Die folgenden Bedingungen können dazu führen, **SocketException** Fehler:</span><span class="sxs-lookup"><span data-stu-id="b2c84-151">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="b2c84-152">Erstellen eines neuen **"HttpClient"** Instanz pro Anforderung.</span><span class="sxs-lookup"><span data-stu-id="b2c84-152">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="b2c84-153">Der Server stark ausgelastet ist.</span><span class="sxs-lookup"><span data-stu-id="b2c84-153">Server under heavy load.</span></span>

<span data-ttu-id="b2c84-154">Erstellen eines neuen **"HttpClient"** Instanz pro Anforderung kann die verfügbaren Sockets ausgeschöpft.</span><span class="sxs-lookup"><span data-stu-id="b2c84-154">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="b2c84-155">Der folgende code initialisiert die **"HttpClient"** Instanz:</span><span class="sxs-lookup"><span data-stu-id="b2c84-155">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="b2c84-156">Der vorangehende Code:</span><span class="sxs-lookup"><span data-stu-id="b2c84-156">The preceding code:</span></span>

* <span data-ttu-id="b2c84-157">Definiert die Basis-URI für HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="b2c84-157">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="b2c84-158">Ändern Sie die Nummer des Ports, auf den Port, der in der Server-app verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2c84-158">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="b2c84-159">Die app funktioniert nicht, es sei denn, der Port für den Server-app verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b2c84-159">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="b2c84-160">Legt den Accept-Header auf "Application/Json" fest.</span><span class="sxs-lookup"><span data-stu-id="b2c84-160">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="b2c84-161">Dieser Header festlegen, weist den Server zum Senden von Daten im JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="b2c84-161">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="b2c84-162">Senden Sie eine GET-Anforderung zum Abrufen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="b2c84-162">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="b2c84-163">Der folgende Code sendet eine GET-Anforderung für ein Produkt:</span><span class="sxs-lookup"><span data-stu-id="b2c84-163">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="b2c84-164">Die **"getasync"** Methode sendet die HTTP-GET-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="b2c84-164">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="b2c84-165">Wenn die Methode abgeschlossen ist, wird ein **HttpResponseMessage** , die die HTTP-Antwort enthält.</span><span class="sxs-lookup"><span data-stu-id="b2c84-165">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="b2c84-166">Wenn der Statuscode der Antwort einen Erfolgscode ist, enthält der Antworttext die JSON-Darstellung eines Produkts.</span><span class="sxs-lookup"><span data-stu-id="b2c84-166">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="b2c84-167">Rufen Sie **ReadAsAsync** zum Deserialisieren der JSON-Nutzlast, die eine `Product` Instanz.</span><span class="sxs-lookup"><span data-stu-id="b2c84-167">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="b2c84-168">Die **ReadAsAsync** -Methode asynchron ist, da der Antworttext beliebig groß sein kann.</span><span class="sxs-lookup"><span data-stu-id="b2c84-168">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="b2c84-169">**"HttpClient"** löst keine Ausnahme aus, wenn die HTTP-Antwort einen Fehlercode enthält.</span><span class="sxs-lookup"><span data-stu-id="b2c84-169">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="b2c84-170">Stattdessen die **IsSuccessStatusCode** Eigenschaft **"false"** lautet der Status ein Fehlercode.</span><span class="sxs-lookup"><span data-stu-id="b2c84-170">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="b2c84-171">Falls gewünscht, HTTP-Fehlercodes als Ausnahmen zu behandeln, rufen [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) auf das Response-Objekt.</span><span class="sxs-lookup"><span data-stu-id="b2c84-171">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> `EnsureSuccessStatusCode` <span data-ttu-id="b2c84-172">löst eine Ausnahme aus, wenn der Statuscode außerhalb des Bereichs 200 liegt&ndash;299.</span><span class="sxs-lookup"><span data-stu-id="b2c84-172">throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="b2c84-173">Beachten Sie, dass **"HttpClient"** kann Ausnahmen auslösen, aus anderen Gründen &mdash; z. B., wenn die Anforderung ein Timeout auftritt.</span><span class="sxs-lookup"><span data-stu-id="b2c84-173">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="b2c84-174">Der Medientypformatierer, zu deserialisieren</span><span class="sxs-lookup"><span data-stu-id="b2c84-174">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="b2c84-175">Wenn **ReadAsAsync** wird aufgerufen, ohne Parameter verwendet eine Reihe von *medienformatierer* zum Lesen des Antworttexts.</span><span class="sxs-lookup"><span data-stu-id="b2c84-175">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="b2c84-176">Die Standard-Formatierer unterstützt JSON, XML und Formular-Url-codierte Daten.</span><span class="sxs-lookup"><span data-stu-id="b2c84-176">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="b2c84-177">Anstatt die Standard-Formatierer verwenden, Sie können eine Liste der Formatierer zum Bereitstellen der **ReadAsAsync** Methode.</span><span class="sxs-lookup"><span data-stu-id="b2c84-177">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="b2c84-178">Verwenden eine Liste der Formatierer ist nützlich, wenn Sie eine benutzerdefinierte medientypformatierer haben:</span><span class="sxs-lookup"><span data-stu-id="b2c84-178">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="b2c84-179">Weitere Informationen finden Sie unter [Medienformatierer in der ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span><span class="sxs-lookup"><span data-stu-id="b2c84-179">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="b2c84-180">Senden eine POST-Anforderung zum Erstellen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="b2c84-180">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="b2c84-181">Der folgende Code sendet eine POST-Anforderung, die enthält eine `Product` Instanz im JSON-Format:</span><span class="sxs-lookup"><span data-stu-id="b2c84-181">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="b2c84-182">Die **PostAsJsonAsync** Methode:</span><span class="sxs-lookup"><span data-stu-id="b2c84-182">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="b2c84-183">Serialisiert ein Objekt in JSON.</span><span class="sxs-lookup"><span data-stu-id="b2c84-183">Serializes an object to JSON.</span></span>
* <span data-ttu-id="b2c84-184">Die JSON-Nutzlast sendet eine POST-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="b2c84-184">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="b2c84-185">Wenn die Anforderung erfolgreich ist:</span><span class="sxs-lookup"><span data-stu-id="b2c84-185">If the request succeeds:</span></span>

* <span data-ttu-id="b2c84-186">Es sollte eine 201 (Created)-Antwort zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="b2c84-186">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="b2c84-187">Die Antwort sollte die URL der erstellten Ressourcen im Location-Header enthalten.</span><span class="sxs-lookup"><span data-stu-id="b2c84-187">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="b2c84-188">Senden von PUT-Anforderung zum Aktualisieren einer Ressource</span><span class="sxs-lookup"><span data-stu-id="b2c84-188">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="b2c84-189">Der folgende Code sendet eine PUT-Anforderung zum Aktualisieren eines Produkts:</span><span class="sxs-lookup"><span data-stu-id="b2c84-189">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="b2c84-190">Die **PutAsJsonAsync** -Methode funktioniert wie **PostAsJsonAsync**, außer dass eine PUT-Anforderung anstelle von POST gesendet.</span><span class="sxs-lookup"><span data-stu-id="b2c84-190">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="b2c84-191">Senden einer DELETE-Anforderung zum Löschen einer Ressource</span><span class="sxs-lookup"><span data-stu-id="b2c84-191">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="b2c84-192">Der folgende Code sendet eine DELETE-Anforderung, um ein Produkt zu löschen:</span><span class="sxs-lookup"><span data-stu-id="b2c84-192">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="b2c84-193">Wie GET muss eine DELETE-Anforderung nicht über einen Anforderungstext.</span><span class="sxs-lookup"><span data-stu-id="b2c84-193">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="b2c84-194">Sie müssen nicht JSON oder XML-Format mit DELETE angeben.</span><span class="sxs-lookup"><span data-stu-id="b2c84-194">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="b2c84-195">Testen Sie das Beispiel</span><span class="sxs-lookup"><span data-stu-id="b2c84-195">Test the sample</span></span>

<span data-ttu-id="b2c84-196">So testen Sie die Client-app:</span><span class="sxs-lookup"><span data-stu-id="b2c84-196">To test the client app:</span></span>

1. <span data-ttu-id="b2c84-197">[Herunterladen](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) , und führen Sie die Server-app.</span><span class="sxs-lookup"><span data-stu-id="b2c84-197">[Download](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="b2c84-198">[Anweisungen zum Download.](/aspnet/core/tutorials/#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="b2c84-198">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> <span data-ttu-id="b2c84-199">Stellen Sie sicher, dass die Server-app ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2c84-199">Verify the server app is working.</span></span> <span data-ttu-id="b2c84-200">Z. B. `http://localhost:64195/api/products` sollte eine Liste von Produkten zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="b2c84-200">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="b2c84-201">Legen Sie die Basis-URI für HTTP-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="b2c84-201">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="b2c84-202">Ändern Sie die Nummer des Ports, auf den Port, der in der Server-app verwendet.</span><span class="sxs-lookup"><span data-stu-id="b2c84-202">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="b2c84-203">Führen Sie die Client-app.</span><span class="sxs-lookup"><span data-stu-id="b2c84-203">Run the client app.</span></span> <span data-ttu-id="b2c84-204">Es wird die folgende Ausgabe generiert:</span><span class="sxs-lookup"><span data-stu-id="b2c84-204">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
