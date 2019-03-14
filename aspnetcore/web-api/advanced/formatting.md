---
title: Formatieren von Antwortdaten in Web-APIs in ASP.NET Core
author: ardalis
description: Informationen zum Formatieren von Antwortdaten in Web-APIS in ASP.NET Core
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
uid: web-api/advanced/formatting
ms.openlocfilehash: 819bf1b49b56e953a9a4398e82866ba0b01ab4db
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049787"
---
# <a name="format-response-data-in-aspnet-core-web-api"></a><span data-ttu-id="be8a2-103">Formatieren von Antwortdaten in Web-APIs in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="be8a2-103">Format response data in ASP.NET Core Web API</span></span>

<span data-ttu-id="be8a2-104">Von [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="be8a2-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="be8a2-105">ASP.NET Core MVC verfügt über integrierte Unterstützung zum Formatieren von Antwortdaten mithilfe von festen Formaten oder als Antwort auf Clientspezifikationen.</span><span class="sxs-lookup"><span data-stu-id="be8a2-105">ASP.NET Core MVC has built-in support for formatting response data, using fixed formats or in response to client specifications.</span></span>

<span data-ttu-id="be8a2-106">[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/formatting/sample) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="be8a2-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/formatting/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="format-specific-action-results"></a><span data-ttu-id="be8a2-107">Formatspezifische Aktionsergebnisse</span><span class="sxs-lookup"><span data-stu-id="be8a2-107">Format-Specific Action Results</span></span>

<span data-ttu-id="be8a2-108">Einige Aktionsergebnistypen sind für ein bestimmtes Format spezifisch, wie z.B. `JsonResult` und `ContentResult`.</span><span class="sxs-lookup"><span data-stu-id="be8a2-108">Some action result types are specific to a particular format, such as `JsonResult` and `ContentResult`.</span></span> <span data-ttu-id="be8a2-109">Aktionen können bestimmte Ergebnisse zurückgeben, die immer auf bestimmte Weise formatiert werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-109">Actions can return specific results that are always formatted in a particular manner.</span></span> <span data-ttu-id="be8a2-110">Beim Zurückgeben eines `JsonResult` werden beispielsweise unabhängig von den Clienteinstellungen JSON-formatierte Daten zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-110">For example, returning a `JsonResult` will return JSON-formatted data, regardless of client preferences.</span></span> <span data-ttu-id="be8a2-111">Dementsprechend werden beim Zurückgeben von `ContentResult` Zeichenfolgendaten im Textformat zurückgegeben (wie auch beim Zurückgeben einer Zeichenfolge).</span><span class="sxs-lookup"><span data-stu-id="be8a2-111">Likewise, returning a `ContentResult` will return plain-text-formatted string data (as will simply returning a string).</span></span>

> [!NOTE]
> <span data-ttu-id="be8a2-112">Eine Aktion muss keinen bestimmten Typ zurückgeben, da MVC jeden beliebigen Objektrückgabewert unterstützt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-112">An action isn't required to return any particular type; MVC supports any object return value.</span></span> <span data-ttu-id="be8a2-113">Gibt eine Aktion eine `IActionResult`-Implementierung zurück und erbt der Controller von `Controller`, verfügen Entwickler über zahlreiche Hilfsmethoden, die vielen der Auswahlmöglichkeiten entsprechen.</span><span class="sxs-lookup"><span data-stu-id="be8a2-113">If an action returns an `IActionResult` implementation and the controller inherits from `Controller`, developers have many helper methods corresponding to many of the choices.</span></span> <span data-ttu-id="be8a2-114">Ergebnisse von Aktionen, die Objekte zurückgeben, die nicht dem `IActionResult`-Typ angehören, werden mit der entsprechenden `IOutputFormatter`-Implementierung serialisiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-114">Results from actions that return objects that are not `IActionResult` types will be serialized using the appropriate `IOutputFormatter` implementation.</span></span>

<span data-ttu-id="be8a2-115">Sollen Daten in einem bestimmten Format von einem Controller zurückgegeben werden, der von der `Controller`-Basisklasse erbt, verwenden Sie die integrierte Hilfsmethode `Json`, um JSON-Daten zurückzugeben, sowie `Content` für Textdaten.</span><span class="sxs-lookup"><span data-stu-id="be8a2-115">To return data in a specific format from a controller that inherits from the `Controller` base class, use the built-in helper method `Json` to return JSON and `Content` for plain text.</span></span> <span data-ttu-id="be8a2-116">Die Aktionsmethode sollte entweder den spezifischen Ergebnistyp (z.B. `JsonResult`) oder `IActionResult` zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-116">Your action method should return either the specific result type (for instance, `JsonResult`) or `IActionResult`.</span></span>

<span data-ttu-id="be8a2-117">Zurückgeben von JSON-formatierten Daten:</span><span class="sxs-lookup"><span data-stu-id="be8a2-117">Returning JSON-formatted data:</span></span>

[!code-csharp[](./formatting/sample/Controllers/Api/AuthorsController.cs?highlight=3,5&range=21-26)]

<span data-ttu-id="be8a2-118">Beispielantwort dieser Aktion:</span><span class="sxs-lookup"><span data-stu-id="be8a2-118">Sample response from this action:</span></span>

![Registerkarte „Netzwerk“ von Developer Tools in Microsoft Edge mit „application/json“ als Inhaltstyp der Antwort](formatting/_static/json-response.png)

<span data-ttu-id="be8a2-120">Beachten Sie, dass der Inhaltstyp der Antwort `application/json` ist. Dies wird sowohl in der Liste der Netzwerkanforderungen als auch im Abschnitt „Antwortheader“ gezeigt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-120">Note that the content type of the response is `application/json`, shown both in the list of network requests and in the Response Headers section.</span></span> <span data-ttu-id="be8a2-121">Beachten Sie auch die Liste der Optionen, die vom Browser (hier Microsoft Edge) im Accept-Header im Abschnitt „Anforderungsheader“ angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="be8a2-121">Also note the list of options presented by the browser (in this case, Microsoft Edge) in the Accept header in the Request Headers section.</span></span> <span data-ttu-id="be8a2-122">Das aktuelle Verfahren sieht vor, dass dieser Header ignoriert wird. Informationen zur Berücksichtigung des Headers finden Sie weiter unten.</span><span class="sxs-lookup"><span data-stu-id="be8a2-122">The current technique is ignoring this header; obeying it is discussed below.</span></span>

<span data-ttu-id="be8a2-123">Wenn Sie Daten im Textformat zurückgeben möchten, verwenden Sie `ContentResult` und das `Content`-Hilfsprogramm:</span><span class="sxs-lookup"><span data-stu-id="be8a2-123">To return plain text formatted data, use `ContentResult` and the `Content` helper:</span></span>

[!code-csharp[](./formatting/sample/Controllers/Api/AuthorsController.cs?highlight=3,5&range=47-52)]

<span data-ttu-id="be8a2-124">Eine Antwort dieser Aktion:</span><span class="sxs-lookup"><span data-stu-id="be8a2-124">A response from this action:</span></span>

![Registerkarte „Netzwerk“ von Developer Tools in Microsoft Edge mit „text/plain“ als Inhaltstyp der Antwort](formatting/_static/text-response.png)

<span data-ttu-id="be8a2-126">Beachten Sie, dass der zurückgegebene `Content-Type` in diesem Fall `text/plain` ist.</span><span class="sxs-lookup"><span data-stu-id="be8a2-126">Note in this case the `Content-Type` returned is `text/plain`.</span></span> <span data-ttu-id="be8a2-127">Dasselbe Verhalten erreichen Sie auch mit einer Zeichenfolge als Antworttyp:</span><span class="sxs-lookup"><span data-stu-id="be8a2-127">You can also achieve this same behavior using just a string response type:</span></span>

[!code-csharp[](./formatting/sample/Controllers/Api/AuthorsController.cs?highlight=3,5&range=54-59)]

>[!TIP]
> <span data-ttu-id="be8a2-128">Für nicht triviale Aktionen mit mehreren Rückgabetypen oder Optionen (wie z.B. verschiedene HTTP-Statuscodes abhängig vom Ergebnis der ausgeführten Vorgänge) sollten Sie `IActionResult` als Rückgabetyp wählen.</span><span class="sxs-lookup"><span data-stu-id="be8a2-128">For non-trivial actions with multiple return types or options (for example, different HTTP status codes based on the result of operations performed), prefer `IActionResult` as the return type.</span></span>

## <a name="content-negotiation"></a><span data-ttu-id="be8a2-129">Inhaltsaushandlung</span><span class="sxs-lookup"><span data-stu-id="be8a2-129">Content Negotiation</span></span>

<span data-ttu-id="be8a2-130">Die Inhaltsaushandlung (auch *Conneg* genannt, kurz für „Content negotiation“) tritt auf, wenn der Client einen [Accept-Header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) angibt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-130">Content negotiation (*conneg* for short) occurs when the client specifies an [Accept header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span> <span data-ttu-id="be8a2-131">Das von ASP.NET Core MVC verwendete Standardformat ist JSON.</span><span class="sxs-lookup"><span data-stu-id="be8a2-131">The default format used by ASP.NET Core MVC is JSON.</span></span> <span data-ttu-id="be8a2-132">Die Inhaltsaushandlung wird durch `ObjectResult` implementiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-132">Content negotiation is implemented by `ObjectResult`.</span></span> <span data-ttu-id="be8a2-133">Sie ist auch in die Statuscode-spezifischen Aktionsergebnisse integriert, die von den Hilfsmethoden zurückgegeben werden (die alle auf `ObjectResult` basieren).</span><span class="sxs-lookup"><span data-stu-id="be8a2-133">It's also built into the status code specific action results returned from the helper methods (which are all based on `ObjectResult`).</span></span> <span data-ttu-id="be8a2-134">Sie können auch einen Modelltyp zurückgeben (eine Klasse, die Sie zuvor als Datenübertragungstyp definiert haben). Dadurch werden die Daten automatisch vom Framework in einem `ObjectResult` umschlossen.</span><span class="sxs-lookup"><span data-stu-id="be8a2-134">You can also return a model type (a class you've defined as your data transfer type) and the framework will automatically wrap it in an `ObjectResult` for you.</span></span>

<span data-ttu-id="be8a2-135">Die folgende Aktionsmethode verwendet die Hilfsmethoden `Ok` und `NotFound`:</span><span class="sxs-lookup"><span data-stu-id="be8a2-135">The following action method uses the `Ok` and `NotFound` helper methods:</span></span>

[!code-csharp[](./formatting/sample/Controllers/Api/AuthorsController.cs?highlight=8,10&range=28-38)]

<span data-ttu-id="be8a2-136">Sofern kein anderes Format angefordert wurde und der Server das angeforderte Format zurückgeben kann, wird eine Antwort im JSON-Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-136">A JSON-formatted response will be returned unless another format was requested and the server can return the requested format.</span></span> <span data-ttu-id="be8a2-137">Sie können ein Tool wie [Fiddler](http://www.telerik.com/fiddler) verwenden, um eine Anforderung mit einem Accept-Header zu erstellen und ein anderes Format anzugeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-137">You can use a tool like [Fiddler](http://www.telerik.com/fiddler) to create a request that includes an Accept header and specify another format.</span></span> <span data-ttu-id="be8a2-138">Verfügt der Server in diesem Fall über ein *Formatierungsprogramm*, das eine Antwort im angeforderten Format erstellen kann, wird das Ergebnis im vom Client gewünschten Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-138">In that case, if the server has a *formatter* that can produce a response in the requested format, the result will be returned in the client-preferred format.</span></span>

![Fiddler-Konsole mit einer manuell erstellten GET-Anforderung mit dem Accept-Headerwert „application/xml“](formatting/_static/fiddler-composer.png)

<span data-ttu-id="be8a2-140">Im obigen Screenshot wurde Fiddler Composer verwendet, um eine Anforderung mit der Angabe `Accept: application/xml` zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="be8a2-140">In the above screenshot, the Fiddler Composer has been used to generate a request, specifying `Accept: application/xml`.</span></span> <span data-ttu-id="be8a2-141">Standardmäßig unterstützt ASP.NET Core MVC ausschließlich JSON. Selbst wenn ein anderes Format angegeben wird, wird das Ergebnis dennoch im JSON-Format zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-141">By default, ASP.NET Core MVC only supports JSON, so even when another format is specified, the result returned is still JSON-formatted.</span></span> <span data-ttu-id="be8a2-142">Informationen zum Hinzufügen von zusätzlichen Formatierungsprogrammen finden Sie im nächsten Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-142">You'll see how to add additional formatters in the next section.</span></span>

<span data-ttu-id="be8a2-143">Controlleraktionen können POCOs (Plain Old CLR Objects) zurückgeben. In diesem Fall erstellt ASP.NET Core MVC automatisch ein `ObjectResult`, das das Objekt umschließt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-143">Controller actions can return POCOs (Plain Old CLR Objects), in which case ASP.NET Core MVC automatically creates an `ObjectResult` for you that wraps the object.</span></span> <span data-ttu-id="be8a2-144">Der Client erhält das formatierte serialisierte Objekt (das Standardformat ist JSON, Sie können auch XML oder andere Formaten konfigurieren).</span><span class="sxs-lookup"><span data-stu-id="be8a2-144">The client will get the formatted serialized object (JSON format is the default; you can configure XML or other formats).</span></span> <span data-ttu-id="be8a2-145">Ist das zurückgegebene Objekt `null`, gibt das Framework die Antwort `204 No Content` zurück.</span><span class="sxs-lookup"><span data-stu-id="be8a2-145">If the object being returned is `null`, then the framework will return a `204 No Content` response.</span></span>

<span data-ttu-id="be8a2-146">Zurückgeben eines Objekttyps:</span><span class="sxs-lookup"><span data-stu-id="be8a2-146">Returning an object type:</span></span>

[!code-csharp[](./formatting/sample/Controllers/Api/AuthorsController.cs?highlight=3&range=40-45)]

<span data-ttu-id="be8a2-147">In diesem Beispiel erhält eine Anforderung für einen gültigen Autoralias die Antwort „200 OK“ mit den Daten des Autors.</span><span class="sxs-lookup"><span data-stu-id="be8a2-147">In the sample, a request for a valid author alias will receive a 200 OK response with the author's data.</span></span> <span data-ttu-id="be8a2-148">Eine Anforderung für einen ungültigen Alias erhält die Antwort „204 Kein Inhalt“.</span><span class="sxs-lookup"><span data-stu-id="be8a2-148">A request for an invalid alias will receive a 204 No Content response.</span></span> <span data-ttu-id="be8a2-149">Weiter unten finden Sie Screenshots mit der Antwort im XML- und JSON-Format.</span><span class="sxs-lookup"><span data-stu-id="be8a2-149">Screenshots showing the response in XML and JSON formats are shown below.</span></span>

### <a name="content-negotiation-process"></a><span data-ttu-id="be8a2-150">Prozess der Inhaltsaushandlung</span><span class="sxs-lookup"><span data-stu-id="be8a2-150">Content Negotiation Process</span></span>

<span data-ttu-id="be8a2-151">Eine *Aushandlung* des Inhalts erfolgt nur, wenn in der Anforderung ein `Accept`-Header angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="be8a2-151">Content *negotiation* only takes place if an `Accept` header appears in the request.</span></span> <span data-ttu-id="be8a2-152">Enthält eine Anforderung einen Accept-Header, listet das Framework die Medientypen im Accept-Header nach Priorität auf und sucht ein Formatierungsprogramm, das eine Antwort in einem der im Accept-Header angegebenen Formate erstellen kann.</span><span class="sxs-lookup"><span data-stu-id="be8a2-152">When a request contains an accept header, the framework will enumerate the media types in the accept header in preference order and will try to find a formatter that can produce a response in one of the formats specified by the accept header.</span></span> <span data-ttu-id="be8a2-153">Wird kein Formatierungsprogramm gefunden, das der Clientanforderung entspricht, sucht das Framework das erste Formatierungsprogramm, das eine Antwort erstellen kann (sofern der Entwickler unter `MvcOptions` nicht stattdessen die Option für die Rückgabe von „406 Nicht akzeptabel“ konfiguriert hat).</span><span class="sxs-lookup"><span data-stu-id="be8a2-153">In case no formatter is found that can satisfy the client's request, the framework will try to find the first formatter that can produce a response (unless the developer has configured the option on `MvcOptions` to return 406 Not Acceptable instead).</span></span> <span data-ttu-id="be8a2-154">Wird in der Anforderung das XML-Format angegeben, wurde das XML-Formatierungsprogramm jedoch nicht konfiguriert, wird stattdessen das JSON-Formatierungsprogramm verwendet.</span><span class="sxs-lookup"><span data-stu-id="be8a2-154">If the request specifies XML, but the XML formatter has not been configured, then the JSON formatter will be used.</span></span> <span data-ttu-id="be8a2-155">Allgemein ausgedrückt: Wurde kein Formatierungsprogramm konfiguriert, das das angeforderte Format bereitstellen kann, wird das erste Formatierungsprogramm verwendet, mit dem das Objekt formatiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="be8a2-155">More generally, if no formatter is configured that can provide the requested format, then the first formatter that can format the object is used.</span></span> <span data-ttu-id="be8a2-156">Ist kein Header angegeben, wird das erste Formatierungsprogramm zum Serialisieren der Antwort verwendet, das das zurückzugebende Objekt bearbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="be8a2-156">If no header is given, the first formatter that can handle the object to be returned will be used to serialize the response.</span></span> <span data-ttu-id="be8a2-157">In diesem Fall findet keine Aushandlung statt, sondern der Server legt das Format fest, das verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="be8a2-157">In this case, there isn't any negotiation taking place - the server is determining what format it will use.</span></span>

> [!NOTE]
> <span data-ttu-id="be8a2-158">Enthält der Accept-Header `*/*`, wird der Header ignoriert, sofern `RespectBrowserAcceptHeader` unter `MvcOptions` nicht auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="be8a2-158">If the Accept header contains `*/*`, the Header will be ignored unless `RespectBrowserAcceptHeader` is set to true on `MvcOptions`.</span></span>

### <a name="browsers-and-content-negotiation"></a><span data-ttu-id="be8a2-159">Browser und Inhaltsaushandlung</span><span class="sxs-lookup"><span data-stu-id="be8a2-159">Browsers and Content Negotiation</span></span>

<span data-ttu-id="be8a2-160">Im Gegensatz zu typischen API-Clients unterstützen Webbrowser oft `Accept`-Header, die eine Vielzahl von Formaten, einschließlich Platzhaltern, enthalten.</span><span class="sxs-lookup"><span data-stu-id="be8a2-160">Unlike typical API clients, web browsers tend to supply `Accept` headers that include a wide array of formats, including wildcards.</span></span> <span data-ttu-id="be8a2-161">Erkennt das Framework, dass die Anforderung von einem Browser stammt, wird standardmäßig der `Accept`-Header ignoriert und der Inhalt stattdessen im konfigurierten Standardformat der Anwendung zurückgegeben (sofern nicht anders konfiguriert im JSON-Format).</span><span class="sxs-lookup"><span data-stu-id="be8a2-161">By default, when the framework detects that the request is coming from a browser, it will ignore the `Accept` header and instead return the content in the application's configured default format (JSON unless otherwise configured).</span></span> <span data-ttu-id="be8a2-162">Dadurch gestaltet sich die Verwendung von unterschiedlichen Browsern bei der Nutzung von APIs einheitlicher.</span><span class="sxs-lookup"><span data-stu-id="be8a2-162">This provides a more consistent experience when using different browsers to consume APIs.</span></span>

<span data-ttu-id="be8a2-163">Wenn Sie möchten, dass Ihre Anwendung Accept-Header berücksichtigt, können Sie dies als Teil der MVC-Konfiguration unter *Startup.cs* durch Festlegen von `RespectBrowserAcceptHeader` auf `true` in der `ConfigureServices`-Methode konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="be8a2-163">If you would prefer your application honor browser accept headers, you can configure this as part of MVC's configuration by setting `RespectBrowserAcceptHeader` to `true` in the `ConfigureServices` method in *Startup.cs*.</span></span>

```csharp
services.AddMvc(options =>
{
    options.RespectBrowserAcceptHeader = true; // false by default
});
```

## <a name="configuring-formatters"></a><span data-ttu-id="be8a2-164">Konfigurieren von Formatierungsprogrammen</span><span class="sxs-lookup"><span data-stu-id="be8a2-164">Configuring Formatters</span></span>

<span data-ttu-id="be8a2-165">Wenn Ihre Anwendung neben dem Standardformat JSON zusätzliche Formate unterstützen soll, können Sie NuGet-Pakete hinzufügen und MVC so konfigurieren, dass diese unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-165">If your application needs to support additional formats beyond the default of JSON, you can add NuGet packages and configure MVC to support them.</span></span> <span data-ttu-id="be8a2-166">Es gibt unterschiedliche Formatierungsprogramme für Ein- und für Ausgaben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-166">There are separate formatters for input and output.</span></span> <span data-ttu-id="be8a2-167">Eingabeformatierer werden bei der [Modellbindung](xref:mvc/models/model-binding) verwendet, Ausgabeformatierer zur Formatierung von Antworten.</span><span class="sxs-lookup"><span data-stu-id="be8a2-167">Input formatters are used by [Model Binding](xref:mvc/models/model-binding); output formatters are used to format responses.</span></span> <span data-ttu-id="be8a2-168">Sie können auch [benutzerdefinierte Formatierer](xref:web-api/advanced/custom-formatters) konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="be8a2-168">You can also configure [Custom Formatters](xref:web-api/advanced/custom-formatters).</span></span>

### <a name="adding-xml-format-support"></a><span data-ttu-id="be8a2-169">Hinzufügen von Unterstützung für das XML-Format</span><span class="sxs-lookup"><span data-stu-id="be8a2-169">Adding XML Format Support</span></span>

<span data-ttu-id="be8a2-170">Installieren Sie zum Hinzufügen von Unterstützung für XML-Formatierungen das NuGet-Paket `Microsoft.AspNetCore.Mvc.Formatters.Xml`.</span><span class="sxs-lookup"><span data-stu-id="be8a2-170">To add support for XML formatting, install the `Microsoft.AspNetCore.Mvc.Formatters.Xml` NuGet package.</span></span>

<span data-ttu-id="be8a2-171">Fügen Sie unter *Startup.cs* „XmlSerializerFormatters“ zur MVC-Konfiguration hinzu:</span><span class="sxs-lookup"><span data-stu-id="be8a2-171">Add the XmlSerializerFormatters to MVC's configuration in *Startup.cs*:</span></span>

[!code-csharp[](./formatting/sample/Startup.cs?name=snippet1&highlight=2)]

<span data-ttu-id="be8a2-172">Sie können auch nur das Ausgabeformatierungsprogramm hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="be8a2-172">Alternately, you can add just the output formatter:</span></span>

```csharp
services.AddMvc(options =>
{
    options.OutputFormatters.Add(new XmlSerializerOutputFormatter());
});
```

<span data-ttu-id="be8a2-173">Mit diesen beiden Ansätzen werden die Ergebnisse mithilfe von `System.Xml.Serialization.XmlSerializer` serialisiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-173">These two approaches will serialize results using `System.Xml.Serialization.XmlSerializer`.</span></span> <span data-ttu-id="be8a2-174">Sie können wahlweise auch den `System.Runtime.Serialization.DataContractSerializer` verwenden, indem Sie das entsprechende Formatierungsprogramm hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="be8a2-174">If you prefer, you can use the `System.Runtime.Serialization.DataContractSerializer` by adding its associated formatter:</span></span>

```csharp
services.AddMvc(options =>
{
    options.OutputFormatters.Add(new XmlDataContractSerializerOutputFormatter());
});
```

<span data-ttu-id="be8a2-175">Sobald Sie Unterstützung für das XML-Format hinzugefügt haben, geben die Controllermethoden das entsprechende Format wie in diesem Fiddler-Beispiel veranschaulicht basierend auf dem `Accept`-Header der Anforderung zurück:</span><span class="sxs-lookup"><span data-stu-id="be8a2-175">Once you've added support for XML formatting, your controller methods should return the appropriate format based on the request's `Accept` header, as this Fiddler example demonstrates:</span></span>

![Fiddler-Konsole: Die Registerkarte "Raw" für die Anforderung zeigt der Wert des Accept-Header Application/Xml.](formatting/_static/xml-response.png)

<span data-ttu-id="be8a2-178">Auf der Registerkarte „Inspektoren“ wird deutlich, dass die GET-Anforderung unter „Raw“ mit einem festgelegten `Accept: application/xml`-Header erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="be8a2-178">You can see in the Inspectors tab that the Raw GET request was made with an `Accept: application/xml` header set.</span></span> <span data-ttu-id="be8a2-179">Im Antwortbereich wird der `Content-Type: application/xml`-Header angezeigt, und das `Author`-Objekt in XML wurde serialisiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-179">The response pane shows the `Content-Type: application/xml` header, and the `Author` object has been serialized to XML.</span></span>

<span data-ttu-id="be8a2-180">Verwenden Sie die Registerkarte „Composer“, um für die Anforderung `application/json` im `Accept`-Header anzugeben.</span><span class="sxs-lookup"><span data-stu-id="be8a2-180">Use the Composer tab to modify the request to specify `application/json` in the `Accept` header.</span></span> <span data-ttu-id="be8a2-181">Führen Sie die Anforderung aus. Die Antwort wird nun als JSON formatiert:</span><span class="sxs-lookup"><span data-stu-id="be8a2-181">Execute the request, and the response will be formatted as JSON:</span></span>

![Fiddler-Konsole: Die Registerkarte "Raw" für die Anforderung zeigt der Wert des Accept-Header Application/Json.](formatting/_static/json-response-fiddler.png)

<span data-ttu-id="be8a2-184">In diesem Screenshot wird deutlich, dass die Anforderung einen Header für `Accept: application/json` festlegt und die Antwort denselben Header als `Content-Type` angibt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-184">In this screenshot, you can see the request sets a header of `Accept: application/json` and the response specifies the same as its `Content-Type`.</span></span> <span data-ttu-id="be8a2-185">Das `Author`-Objekt wird im Text der Antwort im JSON-Format dargestellt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-185">The `Author` object is shown in the body of the response, in JSON format.</span></span>

### <a name="forcing-a-particular-format"></a><span data-ttu-id="be8a2-186">Erzwingen eines bestimmten Formats</span><span class="sxs-lookup"><span data-stu-id="be8a2-186">Forcing a Particular Format</span></span>

<span data-ttu-id="be8a2-187">Wenn Sie die Antwortformate für eine bestimmte Aktion einschränken möchten, können Sie den `[Produces]`-Filter anwenden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-187">If you would like to restrict the response formats for a specific action you can, you can apply the `[Produces]` filter.</span></span> <span data-ttu-id="be8a2-188">Der `[Produces]`-Filter gibt die Antwortformate für eine bestimmte Aktion (oder einen Controller) an.</span><span class="sxs-lookup"><span data-stu-id="be8a2-188">The `[Produces]` filter specifies the response formats for a specific action (or controller).</span></span> <span data-ttu-id="be8a2-189">Wie die meisten [Filter](xref:mvc/controllers/filters) kann auch dieser Filter auf die Aktion, den Controller oder im globalen Gültigkeitsbereich angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-189">Like most [Filters](xref:mvc/controllers/filters), this can be applied at the action, controller, or global scope.</span></span>

```csharp
[Produces("application/json")]
public class AuthorsController
```

<span data-ttu-id="be8a2-190">Der `[Produces]`-Filter erzwingt bei allen Aktionen im `AuthorsController`, dass Antworten im JSON-Format zurückgegeben werden. Dies geschieht selbst, wenn für die Anwendung andere Formatierungsprogramme konfiguriert wurden und der Client einen `Accept`-Header bereitgestellt hat, der ein anderes verfügbares Format anfordert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-190">The `[Produces]` filter will force all actions within the `AuthorsController` to return JSON-formatted responses, even if other formatters were configured for the application and the client provided an `Accept` header requesting a different, available format.</span></span> <span data-ttu-id="be8a2-191">Weitere Informationen, einschließlich der globalen Anwendung von Filtern, finden Sie unter [Filter](xref:mvc/controllers/filters).</span><span class="sxs-lookup"><span data-stu-id="be8a2-191">See [Filters](xref:mvc/controllers/filters) to learn more, including how to apply filters globally.</span></span>

### <a name="special-case-formatters"></a><span data-ttu-id="be8a2-192">Spezielle Formatierungsprogramme</span><span class="sxs-lookup"><span data-stu-id="be8a2-192">Special Case Formatters</span></span>

<span data-ttu-id="be8a2-193">Einige besondere Fälle werden mithilfe von integrierten Formatierungsprogrammen implementiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-193">Some special cases are implemented using built-in formatters.</span></span> <span data-ttu-id="be8a2-194">Standardmäßig werden `string`-Rückgabetypen als *text/plain* formatiert (als *text/html*, wenn sie über den `Accept`-Header angefordert werden).</span><span class="sxs-lookup"><span data-stu-id="be8a2-194">By default, `string` return types will be formatted as *text/plain* (*text/html* if requested via `Accept` header).</span></span> <span data-ttu-id="be8a2-195">Dieses Verhalten kann durch Entfernen des `TextOutputFormatter` entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-195">This behavior can be removed by removing the `TextOutputFormatter`.</span></span> <span data-ttu-id="be8a2-196">Formatierungsprogramme werden in der `Configure`-Methode in *Startup.cs* entfernt (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="be8a2-196">You remove formatters in the `Configure` method in *Startup.cs* (shown below).</span></span> <span data-ttu-id="be8a2-197">Aktionen mit einem Modellobjekt-Rückgabetyp geben die Antwort „204 Kein Inhalt“ beim Zurückgeben von `null` zurück.</span><span class="sxs-lookup"><span data-stu-id="be8a2-197">Actions that have a model object return type will return a 204 No Content response when returning `null`.</span></span> <span data-ttu-id="be8a2-198">Dieses Verhalten kann durch Entfernen des `HttpNoContentOutputFormatter` entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-198">This behavior can be removed by removing the `HttpNoContentOutputFormatter`.</span></span> <span data-ttu-id="be8a2-199">Der folgende Code entfernt `TextOutputFormatter` und `HttpNoContentOutputFormatter`.</span><span class="sxs-lookup"><span data-stu-id="be8a2-199">The following code removes the `TextOutputFormatter` and `HttpNoContentOutputFormatter`.</span></span>

```csharp
services.AddMvc(options =>
{
    options.OutputFormatters.RemoveType<TextOutputFormatter>();
    options.OutputFormatters.RemoveType<HttpNoContentOutputFormatter>();
});
```

<span data-ttu-id="be8a2-200">Ohne `TextOutputFormatter` geben `string`-Rückgabetypen beispielsweise „406 Nicht akzeptabel“ zurück.</span><span class="sxs-lookup"><span data-stu-id="be8a2-200">Without the `TextOutputFormatter`, `string` return types return 406 Not Acceptable, for example.</span></span> <span data-ttu-id="be8a2-201">Beachten Sie, dass ein XML-Formatierer `string`-Rückgabetypen formatiert, wenn der `TextOutputFormatter` entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="be8a2-201">Note that if an XML formatter exists, it will format `string` return types if the `TextOutputFormatter` is removed.</span></span>

<span data-ttu-id="be8a2-202">Ohne `HttpNoContentOutputFormatter` werden NULL-Objekte mithilfe des konfigurierten Formatierungsprogramms formatiert.</span><span class="sxs-lookup"><span data-stu-id="be8a2-202">Without the `HttpNoContentOutputFormatter`, null objects are formatted using the configured formatter.</span></span> <span data-ttu-id="be8a2-203">Beispielsweise gibt das JSON-Formatierungsprogramm einfach eine Antwort mit dem Text `null` zurück, während das XML-Formatierungsprogramm ein leeres XML-Element mit dem festgelegten Attribut `xsi:nil="true"` zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="be8a2-203">For example, the JSON formatter will simply return a response with a body of `null`, while the XML formatter will return an empty XML element with the attribute `xsi:nil="true"` set.</span></span>

## <a name="response-format-url-mappings"></a><span data-ttu-id="be8a2-204">Antwortformat bei URL-Zuordnungen</span><span class="sxs-lookup"><span data-stu-id="be8a2-204">Response Format URL Mappings</span></span>

<span data-ttu-id="be8a2-205">Clients können ein bestimmtes Format als Teil der URL anfordern, wie z.B. in der Abfragezeichenfolge, als Teil des Pfads oder mithilfe einer formatspezifischen Dateierweiterung, wie etwa XML oder JSON.</span><span class="sxs-lookup"><span data-stu-id="be8a2-205">Clients can request a particular format as part of the URL, such as in the query string or part of the path, or by using a format-specific file extension such as .xml or .json.</span></span> <span data-ttu-id="be8a2-206">Die Zuordnung des Anforderungspfads sollte in der Route angegeben werden, die die API verwendet.</span><span class="sxs-lookup"><span data-stu-id="be8a2-206">The mapping from request path should be specified in the route the API is using.</span></span> <span data-ttu-id="be8a2-207">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="be8a2-207">For example:</span></span>

```csharp
[FormatFilter]
public class ProductsController
{
    [Route("[controller]/[action]/{id}.{format?}")]
    public Product GetById(int id)
```

<span data-ttu-id="be8a2-208">Mit dieser Route kann das angeforderte Format als optionale Dateierweiterung angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="be8a2-208">This route would allow the requested format to be specified as an optional file extension.</span></span> <span data-ttu-id="be8a2-209">Das `[FormatFilter]`-Attribut überprüft, ob in den `RouteData` ein Formatwert vorhanden ist und ordnet das Antwortformat beim Erstellen der Antwort dem entsprechenden Formatierungsprogramm zu.</span><span class="sxs-lookup"><span data-stu-id="be8a2-209">The `[FormatFilter]` attribute checks for the existence of the format value in the `RouteData` and will map the response format to the appropriate formatter when the response is created.</span></span>


|           <span data-ttu-id="be8a2-210">Route</span><span class="sxs-lookup"><span data-stu-id="be8a2-210">Route</span></span>            |             <span data-ttu-id="be8a2-211">Formatierungsprogramm</span><span class="sxs-lookup"><span data-stu-id="be8a2-211">Formatter</span></span>              |
|----------------------------|------------------------------------|
|   `/products/GetById/5`    |    <span data-ttu-id="be8a2-212">Standard-Ausgabeformatierungsprogramm</span><span class="sxs-lookup"><span data-stu-id="be8a2-212">The default output formatter</span></span>    |
| `/products/GetById/5.json` | <span data-ttu-id="be8a2-213">JSON-Formatierungsprogramm (falls konfiguriert)</span><span class="sxs-lookup"><span data-stu-id="be8a2-213">The JSON formatter (if configured)</span></span> |
| `/products/GetById/5.xml`  | <span data-ttu-id="be8a2-214">XML-Formatierungsprogramm (falls konfiguriert)</span><span class="sxs-lookup"><span data-stu-id="be8a2-214">The XML formatter (if configured)</span></span>  |

