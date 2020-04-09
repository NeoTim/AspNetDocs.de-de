---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Routing in ASP.NET Web-API | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675754"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="fb723-102">Routing in der ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="fb723-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="fb723-103">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fb723-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fb723-104">In diesem Artikel wird beschrieben, wie ASP.NET Web-API HTTP-Anforderungen an Controller weiterleitet.</span><span class="sxs-lookup"><span data-stu-id="fb723-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="fb723-105">Wenn Sie mit ASP.NET MVC vertraut sind, ähnelt das Web-API-Routing dem MVC-Routing sehr.</span><span class="sxs-lookup"><span data-stu-id="fb723-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="fb723-106">Der Hauptunterschied besteht darin, dass die Web-API das HTTP-Verb und nicht den URI-Pfad verwendet, um die Aktion auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="fb723-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="fb723-107">Sie können auch Dasrouting im MVC-Stil in der Web-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="fb723-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="fb723-108">Dieser Artikel geht nicht von Kenntnissen ASP.NET MVC aus.</span><span class="sxs-lookup"><span data-stu-id="fb723-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="fb723-109">Routingtabellen</span><span class="sxs-lookup"><span data-stu-id="fb723-109">Routing Tables</span></span>

<span data-ttu-id="fb723-110">In ASP.NET Web-API ist ein *Controller* eine Klasse, die HTTP-Anforderungen verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="fb723-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="fb723-111">Die öffentlichen Methoden des Controllers werden *als Aktionsmethoden* oder einfach *als Aktionen*bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="fb723-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="fb723-112">Wenn das Web-API-Framework eine Anforderung empfängt, leitet es die Anforderung an eine Aktion weiter.</span><span class="sxs-lookup"><span data-stu-id="fb723-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="fb723-113">Um zu bestimmen, welche Aktion aufgerufen werden soll, verwendet das Framework eine *Routingtabelle*.</span><span class="sxs-lookup"><span data-stu-id="fb723-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="fb723-114">Die Visual Studio-Projektvorlage für Web-API erstellt eine Standardroute:</span><span class="sxs-lookup"><span data-stu-id="fb723-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="fb723-115">Diese Route wird in der *WebApiConfig.cs-Datei* definiert, die im *\_App-Start-Verzeichnis* abgelegt wird:</span><span class="sxs-lookup"><span data-stu-id="fb723-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="fb723-116">Weitere Informationen zur `WebApiConfig` Klasse finden Sie unter [Konfigurieren ASP.NET Web-API](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="fb723-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="fb723-117">Wenn Sie die Web-API selbst hosten, müssen `HttpSelfHostConfiguration` Sie die Routingtabelle direkt für das Objekt festlegen.</span><span class="sxs-lookup"><span data-stu-id="fb723-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="fb723-118">Weitere Informationen finden Sie unter [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="fb723-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="fb723-119">Jeder Eintrag in der Routingtabelle enthält eine *Routenvorlage*.</span><span class="sxs-lookup"><span data-stu-id="fb723-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="fb723-120">Die Standardroutenvorlage für &quot;die Web-API ist api/-controller.&quot;</span><span class="sxs-lookup"><span data-stu-id="fb723-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="fb723-121">In dieser &quot;Vorlage&quot; ist api ein literales Pfadsegment, und die Platzhaltervariablen "controller" und "id" sind Platzhaltervariablen.</span><span class="sxs-lookup"><span data-stu-id="fb723-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="fb723-122">Wenn das Web-API-Framework eine HTTP-Anforderung empfängt, versucht es, den URI mit einer der Routenvorlagen in der Routingtabelle abzugleichen.</span><span class="sxs-lookup"><span data-stu-id="fb723-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="fb723-123">Wenn keine Route übereinstimmt, erhält der Client einen 404-Fehler.</span><span class="sxs-lookup"><span data-stu-id="fb723-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="fb723-124">Die folgenden URIs entsprechen beispielsweise der Standardroute:</span><span class="sxs-lookup"><span data-stu-id="fb723-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="fb723-125">/api/kontakte</span><span class="sxs-lookup"><span data-stu-id="fb723-125">/api/contacts</span></span>
- <span data-ttu-id="fb723-126">/api/kontakte/1</span><span class="sxs-lookup"><span data-stu-id="fb723-126">/api/contacts/1</span></span>
- <span data-ttu-id="fb723-127">/api/produkte/gizmo1</span><span class="sxs-lookup"><span data-stu-id="fb723-127">/api/products/gizmo1</span></span>

<span data-ttu-id="fb723-128">Der folgende URI stimmt jedoch nicht überein, da ihm das &quot;API-Segment&quot; fehlt:</span><span class="sxs-lookup"><span data-stu-id="fb723-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="fb723-129">/Kontakte/1</span><span class="sxs-lookup"><span data-stu-id="fb723-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="fb723-130">Der Grund für die Verwendung von "api" in der Route ist, Kollisionen mit ASP.NET MVC-Routing zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="fb723-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="fb723-131">Auf diese Weise &quot;können&quot; Sie /contacts zu einem &quot;MVC-Controller und /api/contacts&quot; zu einem Web-API-Controller aufrufen.</span><span class="sxs-lookup"><span data-stu-id="fb723-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="fb723-132">Wenn Ihnen diese Konvention nicht gefällt, können Sie natürlich die Standardroutentabelle ändern.</span><span class="sxs-lookup"><span data-stu-id="fb723-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="fb723-133">Sobald eine übereinstimmende Route gefunden wurde, wählt die Web-API den Controller und die Aktion aus:</span><span class="sxs-lookup"><span data-stu-id="fb723-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="fb723-134">Um den Controller zu &quot;finden, fügt die Web-API Controller&quot; zum Wert der Variable *"Controller"* hinzu.</span><span class="sxs-lookup"><span data-stu-id="fb723-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="fb723-135">Um die Aktion zu finden, sucht web API das HTTP-Verb und sucht dann nach einer Aktion, deren Name mit diesem HTTP-Verbnamen beginnt.</span><span class="sxs-lookup"><span data-stu-id="fb723-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="fb723-136">Bei einer GET-Anforderung sucht die Web-API beispielsweise &quot;&quot;nach einer &quot;Aktion&quot; &quot;mit dem&quot;Präfix Get , z. B. GetContact oder GetAllContacts .</span><span class="sxs-lookup"><span data-stu-id="fb723-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="fb723-137">Diese Konvention gilt nur für GET-, POST-, PUT-, DELETE-, HEAD-, OPTIONS- und PATCH-Verben.</span><span class="sxs-lookup"><span data-stu-id="fb723-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="fb723-138">Sie können andere HTTP-Verben aktivieren, indem Sie Attribute auf dem Controller verwenden.</span><span class="sxs-lookup"><span data-stu-id="fb723-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="fb723-139">Ein Beispiel dafür werden wir später sehen.</span><span class="sxs-lookup"><span data-stu-id="fb723-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="fb723-140">Andere Platzhaltervariablen in der Routenvorlage, wie z. B. *die Option "id",* werden Aktionsparametern zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="fb723-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="fb723-141">Schauen wir uns ein Beispiel an.</span><span class="sxs-lookup"><span data-stu-id="fb723-141">Let's look at an example.</span></span> <span data-ttu-id="fb723-142">Angenommen, Sie definieren den folgenden Controller:</span><span class="sxs-lookup"><span data-stu-id="fb723-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="fb723-143">Hier sind einige mögliche HTTP-Anforderungen, zusammen mit der Aktion, die für jede aufgerufen wird:</span><span class="sxs-lookup"><span data-stu-id="fb723-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="fb723-144">HTTP-Verb</span><span class="sxs-lookup"><span data-stu-id="fb723-144">HTTP Verb</span></span> | <span data-ttu-id="fb723-145">URI-Pfad</span><span class="sxs-lookup"><span data-stu-id="fb723-145">URI Path</span></span> | <span data-ttu-id="fb723-146">Aktion</span><span class="sxs-lookup"><span data-stu-id="fb723-146">Action</span></span> | <span data-ttu-id="fb723-147">Parameter</span><span class="sxs-lookup"><span data-stu-id="fb723-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb723-148">GET</span><span class="sxs-lookup"><span data-stu-id="fb723-148">GET</span></span> | <span data-ttu-id="fb723-149">api/Produkte</span><span class="sxs-lookup"><span data-stu-id="fb723-149">api/products</span></span> | <span data-ttu-id="fb723-150">GetAllProdukte</span><span class="sxs-lookup"><span data-stu-id="fb723-150">GetAllProducts</span></span> | <span data-ttu-id="fb723-151">*(keine)*</span><span class="sxs-lookup"><span data-stu-id="fb723-151">*(none)*</span></span> |
| <span data-ttu-id="fb723-152">GET</span><span class="sxs-lookup"><span data-stu-id="fb723-152">GET</span></span> | <span data-ttu-id="fb723-153">api/produkte/4</span><span class="sxs-lookup"><span data-stu-id="fb723-153">api/products/4</span></span> | <span data-ttu-id="fb723-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="fb723-154">GetProductById</span></span> | <span data-ttu-id="fb723-155">4</span><span class="sxs-lookup"><span data-stu-id="fb723-155">4</span></span> |
| <span data-ttu-id="fb723-156">Delete</span><span class="sxs-lookup"><span data-stu-id="fb723-156">DELETE</span></span> | <span data-ttu-id="fb723-157">api/produkte/4</span><span class="sxs-lookup"><span data-stu-id="fb723-157">api/products/4</span></span> | <span data-ttu-id="fb723-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="fb723-158">DeleteProduct</span></span> | <span data-ttu-id="fb723-159">4</span><span class="sxs-lookup"><span data-stu-id="fb723-159">4</span></span> |
| <span data-ttu-id="fb723-160">POST</span><span class="sxs-lookup"><span data-stu-id="fb723-160">POST</span></span> | <span data-ttu-id="fb723-161">api/Produkte</span><span class="sxs-lookup"><span data-stu-id="fb723-161">api/products</span></span> | <span data-ttu-id="fb723-162">*(keine Übereinstimmung)*</span><span class="sxs-lookup"><span data-stu-id="fb723-162">*(no match)*</span></span> |  |

<span data-ttu-id="fb723-163">Beachten Sie, dass das Segment *"id"* des URI, falls vorhanden, dem *ID-Parameter* der Aktion zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="fb723-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="fb723-164">In diesem Beispiel definiert der Controller zwei GET-Methoden, eine mit einem *id-Parameter* und eine ohne Parameter.</span><span class="sxs-lookup"><span data-stu-id="fb723-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="fb723-165">Beachten Sie außerdem, dass die POST-Anforderung fehlschlägt, da der Controller keine &quot;Post... &quot; Methode.</span><span class="sxs-lookup"><span data-stu-id="fb723-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="fb723-166">Routing-Variationen</span><span class="sxs-lookup"><span data-stu-id="fb723-166">Routing Variations</span></span>

<span data-ttu-id="fb723-167">Im vorherigen Abschnitt wurde der grundlegende Routingmechanismus für ASP.NET Web-API beschrieben.</span><span class="sxs-lookup"><span data-stu-id="fb723-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="fb723-168">In diesem Abschnitt werden einige Variationen beschrieben.</span><span class="sxs-lookup"><span data-stu-id="fb723-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="fb723-169">HTTP-Verben</span><span class="sxs-lookup"><span data-stu-id="fb723-169">HTTP verbs</span></span>

<span data-ttu-id="fb723-170">Anstatt die Namenskonvention für HTTP-Verben zu verwenden, können Sie explizit das HTTP-Verb für eine Aktion angeben, indem Sie die Aktionsmethode mit einem der folgenden Attribute dekorieren:</span><span class="sxs-lookup"><span data-stu-id="fb723-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="fb723-171">Im folgenden Beispiel `FindProduct` wird die Methode GET-Anforderungen zugeordnet:</span><span class="sxs-lookup"><span data-stu-id="fb723-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="fb723-172">Um mehrere HTTP-Verben für eine Aktion zuzulassen oder HTTP-Verben außer GET, PUT, POST, `[AcceptVerbs]` DELETE, HEAD, OPTIONS und PATCH zuzulassen, verwenden Sie das Attribut, das eine Liste von HTTP-Verben enthält.</span><span class="sxs-lookup"><span data-stu-id="fb723-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="fb723-173">Routing nach Aktionsname</span><span class="sxs-lookup"><span data-stu-id="fb723-173">Routing by Action Name</span></span>

<span data-ttu-id="fb723-174">Bei der Standardroutingvorlage verwendet Web API das HTTP-Verb, um die Aktion auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="fb723-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="fb723-175">Sie können jedoch auch eine Route erstellen, in der der Aktionsname im URI enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="fb723-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="fb723-176">In dieser Routenvorlage benennt der Parameter *"Aktion"* die Aktionsmethode auf dem Controller.</span><span class="sxs-lookup"><span data-stu-id="fb723-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="fb723-177">Verwenden Sie bei diesem Routingstil Attribute, um die zulässigen HTTP-Verben anzugeben.</span><span class="sxs-lookup"><span data-stu-id="fb723-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="fb723-178">Angenommen, Ihr Controller verfügt über die folgende Methode:</span><span class="sxs-lookup"><span data-stu-id="fb723-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="fb723-179">In diesem Fall würde eine GET-Anforderung für "api/products/details/1" der `Details` Methode zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="fb723-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="fb723-180">Dieser Routingstil ähnelt ASP.NET MVC und eignet sich möglicherweise für eine RPC-API.</span><span class="sxs-lookup"><span data-stu-id="fb723-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="fb723-181">Sie können den Aktionsnamen überschreiben, indem Sie das `[ActionName]` Attribut verwenden.</span><span class="sxs-lookup"><span data-stu-id="fb723-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="fb723-182">Im folgenden Beispiel gibt es zwei &quot;Aktionen, die api/products/thumbnail/*id*zugeordnet werden. Die eine unterstützt GET und die andere post:</span><span class="sxs-lookup"><span data-stu-id="fb723-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="fb723-183">Nicht-Aktionen</span><span class="sxs-lookup"><span data-stu-id="fb723-183">Non-Actions</span></span>

<span data-ttu-id="fb723-184">Um zu verhindern, dass eine Methode als `[NonAction]` Aktion aufgerufen wird, verwenden Sie das Attribut.</span><span class="sxs-lookup"><span data-stu-id="fb723-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="fb723-185">Dies signalisiert dem Framework, dass die Methode keine Aktion ist, auch wenn sie andernfalls den Routingregeln entsprechen würde.</span><span class="sxs-lookup"><span data-stu-id="fb723-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="fb723-186">Weitere nützliche Informationen</span><span class="sxs-lookup"><span data-stu-id="fb723-186">Further Reading</span></span>

<span data-ttu-id="fb723-187">Dieses Thema bot eine ansichtsebene Ansicht des Routings.</span><span class="sxs-lookup"><span data-stu-id="fb723-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="fb723-188">Weitere Informationen finden Sie unter [Routing und Aktionsauswahl](routing-and-action-selection.md), in dem genau beschrieben wird, wie das Framework einen URI mit einer Route abgleicht, einen Controller auswählt und dann die zu aufrufende Aktion auswählt.</span><span class="sxs-lookup"><span data-stu-id="fb723-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
