---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: Routing- und Aktionsauswahl in ASP.NET Web-API | Microsoft-Dokumentation
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 238efd312a73e2452ca5f679f2b8f5ed1336c4dc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385877"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="4114b-102">Routing- und Aktionsauswahl in ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="4114b-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="4114b-103">durch [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4114b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4114b-104">In diesem Artikel wird beschrieben, wie ASP.NET Web-API eine HTTP-Anforderung an eine bestimmte Aktion für einen Controller weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="4114b-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="4114b-105">Eine allgemeine Übersicht über routing, finden Sie unter [Routing in ASP.NET Web-API](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="4114b-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>


<span data-ttu-id="4114b-106">Dieser Artikel behandelt die Details der routing-Prozess.</span><span class="sxs-lookup"><span data-stu-id="4114b-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="4114b-107">Wenn Sie ein Web-API-Projekt erstellen, und suchen, die einige Anforderungen werden nicht weitergeleitet, die Möglichkeit, die Sie erwarten, hilft dieser Artikel hoffentlich.</span><span class="sxs-lookup"><span data-stu-id="4114b-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="4114b-108">Routing verfügt über drei Hauptphasen aus:</span><span class="sxs-lookup"><span data-stu-id="4114b-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="4114b-109">Mit den URI, der eine routenvorlage übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="4114b-110">Wählen einen Controller.</span><span class="sxs-lookup"><span data-stu-id="4114b-110">Selecting a controller.</span></span>
3. <span data-ttu-id="4114b-111">Auswählen einer Aktion.</span><span class="sxs-lookup"><span data-stu-id="4114b-111">Selecting an action.</span></span>

<span data-ttu-id="4114b-112">Sie können einige Teile des Prozesses durch Ihre eigenen benutzerdefinierten Verhalten ersetzen.</span><span class="sxs-lookup"><span data-stu-id="4114b-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="4114b-113">In diesem Artikel beschreibe ich das Standardverhalten.</span><span class="sxs-lookup"><span data-stu-id="4114b-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="4114b-114">Beachten Sie am Ende ich die Stellen, in dem Sie das Verhalten anpassen können.</span><span class="sxs-lookup"><span data-stu-id="4114b-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="4114b-115">Routenvorlagen</span><span class="sxs-lookup"><span data-stu-id="4114b-115">Route Templates</span></span>

<span data-ttu-id="4114b-116">Eine routenvorlage ähnelt einem URI-Pfad, aber es kann Platzhalterwerte, mit geschweiften Klammern angegeben haben:</span><span class="sxs-lookup"><span data-stu-id="4114b-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="4114b-117">Wenn Sie eine Route erstellen, können Sie die Standardwerte für einige oder alle Platzhalter angeben:</span><span class="sxs-lookup"><span data-stu-id="4114b-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="4114b-118">Sie können auch Einschränkungen angeben, die eingeschränkt wie einen Platzhalter mit einer URI-Segment verglichen werden kann:</span><span class="sxs-lookup"><span data-stu-id="4114b-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="4114b-119">Das Framework versucht, die die Segmente im URI-Pfad der Vorlage übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="4114b-120">Literale in der Vorlage müssen genau übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="4114b-121">Ein Platzhalter entspricht ein beliebiger Wert, es sei denn, Sie Einschränkungen angeben.</span><span class="sxs-lookup"><span data-stu-id="4114b-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="4114b-122">Das Framework stimmt nicht mit anderen Teilen des URIS, wie z. B. den Hostnamen oder die Abfrageparameter überein.</span><span class="sxs-lookup"><span data-stu-id="4114b-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="4114b-123">Das Framework wählt die erste Route in der Routingtabelle, die den URI entspricht.</span><span class="sxs-lookup"><span data-stu-id="4114b-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="4114b-124">Es gibt zwei spezielle Platzhalter: "{Controller}" und "{Action}".</span><span class="sxs-lookup"><span data-stu-id="4114b-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="4114b-125">"{Controller}" enthält den Namen des Controllers.</span><span class="sxs-lookup"><span data-stu-id="4114b-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="4114b-126">"{Action}" enthält den Namen der Aktion.</span><span class="sxs-lookup"><span data-stu-id="4114b-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="4114b-127">Die übliche Konvention werden in der Web-API weglassen von "{Action}".</span><span class="sxs-lookup"><span data-stu-id="4114b-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="4114b-128">der Arbeitszeittabelle</span><span class="sxs-lookup"><span data-stu-id="4114b-128">Defaults</span></span>

<span data-ttu-id="4114b-129">Wenn Sie Standardwerte angeben, entspricht die Route einen URI, der diese Segmente nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="4114b-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="4114b-130">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4114b-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="4114b-131">Die URIs `http://localhost/api/products/all` und `http://localhost/api/products` die vorherige Route übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="4114b-132">Im letzteren URI, die fehlende `{category}` Segment ist der Standardwert zugewiesen `all`.</span><span class="sxs-lookup"><span data-stu-id="4114b-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="4114b-133">Routenwörterbuchs</span><span class="sxs-lookup"><span data-stu-id="4114b-133">Route Dictionary</span></span>

<span data-ttu-id="4114b-134">Wenn das Framework eine Übereinstimmung für einen URI findet, wird ein Wörterbuch, das den Wert für jeden Platzhalter enthält.</span><span class="sxs-lookup"><span data-stu-id="4114b-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="4114b-135">Die Schlüssel sind die Platzhalternamen, nicht einschließlich der geschweiften Klammern.</span><span class="sxs-lookup"><span data-stu-id="4114b-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="4114b-136">Die Werte stammen aus der URI-Pfad oder die Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="4114b-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="4114b-137">Das Wörterbuch befindet sich in der **IHttpRouteData** Objekt.</span><span class="sxs-lookup"><span data-stu-id="4114b-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="4114b-138">Während dieser Phase übereinstimmende Route sind die speziellen "{Controller}" und "{Action}" Platzhalter wie die anderen Platzhalter behandelt.</span><span class="sxs-lookup"><span data-stu-id="4114b-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="4114b-139">Sie werden einfach in das Wörterbuch mit den anderen Werten gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4114b-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="4114b-140">Ein Standardwert kann den speziellen Wert ist **RouteParameter.Optional**.</span><span class="sxs-lookup"><span data-stu-id="4114b-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="4114b-141">Wenn ein Platzhalter, diesen Wert zugewiesen wird, wird der Wert des Routenwörterbuchs nicht hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4114b-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="4114b-142">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4114b-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="4114b-143">Für den URI-Pfad "api/Produkte" enthält des Routenwörterbuchs Folgendes:</span><span class="sxs-lookup"><span data-stu-id="4114b-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="4114b-144">Controller: "Produkte"</span><span class="sxs-lookup"><span data-stu-id="4114b-144">controller: "products"</span></span>
- <span data-ttu-id="4114b-145">Kategorie: "all"</span><span class="sxs-lookup"><span data-stu-id="4114b-145">category: "all"</span></span>

<span data-ttu-id="4114b-146">Für "api/Produkte/Toys/123" enthält jedoch des Routenwörterbuchs:</span><span class="sxs-lookup"><span data-stu-id="4114b-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="4114b-147">Controller: "Produkte"</span><span class="sxs-lookup"><span data-stu-id="4114b-147">controller: "products"</span></span>
- <span data-ttu-id="4114b-148">Kategorie: "Toys"</span><span class="sxs-lookup"><span data-stu-id="4114b-148">category: "toys"</span></span>
- <span data-ttu-id="4114b-149">id: "123"</span><span class="sxs-lookup"><span data-stu-id="4114b-149">id: "123"</span></span>

<span data-ttu-id="4114b-150">Die Standardwerte können auch einen Wert, der nicht, eine beliebige Stelle angezeigt wird in der routenvorlage enthalten.</span><span class="sxs-lookup"><span data-stu-id="4114b-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="4114b-151">Wenn die Route übereinstimmt, wird dieser Wert im Wörterbuch gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4114b-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="4114b-152">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4114b-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="4114b-153">Wenn der URI-Pfad "api/Root/8" ist, wird das Wörterbuch zwei Werte enthalten:</span><span class="sxs-lookup"><span data-stu-id="4114b-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="4114b-154">Controller: "Customers"</span><span class="sxs-lookup"><span data-stu-id="4114b-154">controller: "customers"</span></span>
- <span data-ttu-id="4114b-155">id: "8"</span><span class="sxs-lookup"><span data-stu-id="4114b-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="4114b-156">Auswählen eines Controllers</span><span class="sxs-lookup"><span data-stu-id="4114b-156">Selecting a Controller</span></span>

<span data-ttu-id="4114b-157">Auswahl der Domänencontroller erfolgt durch die **IHttpControllerSelector.SelectController** Methode.</span><span class="sxs-lookup"><span data-stu-id="4114b-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="4114b-158">Diese Methode akzeptiert eine **HttpRequestMessage** -Instanz und gibt eine **HttpControllerDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="4114b-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="4114b-159">Die standardmäßige Implementierung erfolgt über die **DefaultHttpControllerSelector** Klasse.</span><span class="sxs-lookup"><span data-stu-id="4114b-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="4114b-160">Diese Klasse wird einen einfachen Algorithmus verwendet:</span><span class="sxs-lookup"><span data-stu-id="4114b-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="4114b-161">Suchen Sie in das Wörterbuch der Route für den Schlüssel "Controller".</span><span class="sxs-lookup"><span data-stu-id="4114b-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="4114b-162">Der Wert für diesen Schlüssel, und fügen Sie die Zeichenfolge "Controller", um den Namen des Controllers erhalten.</span><span class="sxs-lookup"><span data-stu-id="4114b-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="4114b-163">Suchen Sie nach einem Web-API-Controller mit diesem Namen geben.</span><span class="sxs-lookup"><span data-stu-id="4114b-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="4114b-164">Wenn das Route-Wörterbuch der Schlüssel-Wert-Paar "Controller" enthält = "Produkte", z. B. wird der Typ des Controllers "ProductsController".</span><span class="sxs-lookup"><span data-stu-id="4114b-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="4114b-165">Wenn keine übereinstimmenden Typ oder mehrere Übereinstimmungen vorhanden ist, gibt das Framework einen Fehler an den Client zurück.</span><span class="sxs-lookup"><span data-stu-id="4114b-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="4114b-166">Schritt 3 **DefaultHttpControllerSelector** verwendet die **IHttpControllerTypeResolver** -Schnittstelle zum Abrufen der Liste der Web-API-Controller-Typen.</span><span class="sxs-lookup"><span data-stu-id="4114b-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="4114b-167">Die standardmäßige Implementierung des **IHttpControllerTypeResolver** gibt alle öffentlichen Klassen, die (a) implementieren **IHttpController**, (b) werden nicht abstrahieren und (c) verfügen über einen Namen, die "Controller" enden.</span><span class="sxs-lookup"><span data-stu-id="4114b-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="4114b-168">Aktionsauswahl</span><span class="sxs-lookup"><span data-stu-id="4114b-168">Action Selection</span></span>

<span data-ttu-id="4114b-169">Nach der Auswahl des Controllers an, das Framework wählt die Aktion durch Aufrufen der **IHttpActionSelector.SelectAction** Methode.</span><span class="sxs-lookup"><span data-stu-id="4114b-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="4114b-170">Diese Methode akzeptiert eine **HttpControllerContext** und gibt eine **HttpActionDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="4114b-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="4114b-171">Die standardmäßige Implementierung erfolgt über die **ApiControllerActionSelector** Klasse.</span><span class="sxs-lookup"><span data-stu-id="4114b-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="4114b-172">Um eine Aktion auswählen, sieht es unter dem folgenden:</span><span class="sxs-lookup"><span data-stu-id="4114b-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="4114b-173">Die HTTP-Methode der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="4114b-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="4114b-174">Der Platzhalter "{Action}" in der routenvorlage, falls vorhanden.</span><span class="sxs-lookup"><span data-stu-id="4114b-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="4114b-175">Die Parameter der Aktionen auf dem Controller.</span><span class="sxs-lookup"><span data-stu-id="4114b-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="4114b-176">Vor dem Betrachten des Auswahlalgorithmus, müssen wir einige Dinge zu Controlleraktionen zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="4114b-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

**<span data-ttu-id="4114b-177">Welche Methoden auf dem Controller "Aktionen" gelten?</span><span class="sxs-lookup"><span data-stu-id="4114b-177">Which methods on the controller are considered "actions"?</span></span>** <span data-ttu-id="4114b-178">Wenn Sie eine Aktion auswählen, sucht das Framework nur auf Öffentliche Instanzenmethoden auf dem Controller.</span><span class="sxs-lookup"><span data-stu-id="4114b-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="4114b-179">Darüber hinaus schließt er ["spezielle Name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) Methoden (Konstruktoren, Ereignisse, operatorüberladungen und So weiter) und von geerbten Methoden der **ApiController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="4114b-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

**<span data-ttu-id="4114b-180">HTTP-Methoden.</span><span class="sxs-lookup"><span data-stu-id="4114b-180">HTTP Methods.</span></span>** <span data-ttu-id="4114b-181">Das Framework wählt nur die Aktionen, die die HTTP-Methode der Anforderung wie folgt bestimmt entsprechen:</span><span class="sxs-lookup"><span data-stu-id="4114b-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="4114b-182">Sie können die HTTP-Methode mit einem Attribut angeben: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **"HttpOptions"**, **HttpPatch**, **HttpPost**, oder **HttpPut**.</span><span class="sxs-lookup"><span data-stu-id="4114b-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="4114b-183">Andernfalls, wenn der Name der Controller-Methode mit "Get", "Post", "Put", "Delete", "Head", "Optionen" oder "Patch" gestartet wird, klicken Sie dann gemäß der Konvention die Aktion unterstützt diese HTTP-Methode.</span><span class="sxs-lookup"><span data-stu-id="4114b-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="4114b-184">Wenn keine der oben genannten, unterstützt die Methode POST aus.</span><span class="sxs-lookup"><span data-stu-id="4114b-184">If none of the above, the method supports POST.</span></span>

**<span data-ttu-id="4114b-185">Der Parameterbindungen.</span><span class="sxs-lookup"><span data-stu-id="4114b-185">Parameter Bindings.</span></span>** <span data-ttu-id="4114b-186">Eine parameterbindung ist wie Web-API auf einen Wert für einen Parameter erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="4114b-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="4114b-187">Hier ist die Standardregel für die parameterbindung:</span><span class="sxs-lookup"><span data-stu-id="4114b-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="4114b-188">Einfache Typen stammen aus dem URI.</span><span class="sxs-lookup"><span data-stu-id="4114b-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="4114b-189">Komplexe Typen stammen aus dem Anforderungstext.</span><span class="sxs-lookup"><span data-stu-id="4114b-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="4114b-190">Einfache Typen umfassen alle der [.NET Framework-primitive Typen](https://msdn.microsoft.com/library/system.type.isprimitive), plus **"DateTime"**, **Decimal**, **Guid**, **Zeichenfolge** , und **TimeSpan**.</span><span class="sxs-lookup"><span data-stu-id="4114b-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="4114b-191">Für jede Aktion kann höchstens einen Parameter den Anforderungstext lesen.</span><span class="sxs-lookup"><span data-stu-id="4114b-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="4114b-192">Es ist möglich, die Regeln für die Bindung zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="4114b-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="4114b-193">Finden Sie unter [WebAPI parameterbindung im Hintergrund](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span><span class="sxs-lookup"><span data-stu-id="4114b-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>


<span data-ttu-id="4114b-194">Mit diesem Hintergrund sieht der Auswahlalgorithmus für die Aktion aus.</span><span class="sxs-lookup"><span data-stu-id="4114b-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="4114b-195">Erstellen Sie eine Liste mit allen Aktionen auf dem Controller an, die die HTTP-Anforderungsmethode entsprechen.</span><span class="sxs-lookup"><span data-stu-id="4114b-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="4114b-196">Wenn des Routenwörterbuchs einen Eintrag "Action" aufweist, entfernen Sie Aktionen, deren Name nicht mit diesem Wert übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="4114b-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="4114b-197">Versuchen Sie es, Action-Parameter an den URI, folgendermaßen an:</span><span class="sxs-lookup"><span data-stu-id="4114b-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="4114b-198">Erhalten Sie für jede Aktion eine Liste mit den Parametern, die einen einfachen Typ, sind, in dem die Bindung ruft den Parameter aus dem URI.</span><span class="sxs-lookup"><span data-stu-id="4114b-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="4114b-199">Schließen Sie optionale Parameter.</span><span class="sxs-lookup"><span data-stu-id="4114b-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="4114b-200">Versuchen Sie, eine Übereinstimmung mit jeder Parametername in des Routenwörterbuchs oder in der URI-Abfragezeichenfolge zu suchen, aus dieser Liste.</span><span class="sxs-lookup"><span data-stu-id="4114b-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="4114b-201">Übereinstimmungen werden Groß-/Kleinschreibung und hängen nicht von der Reihenfolge der Parameter.</span><span class="sxs-lookup"><span data-stu-id="4114b-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="4114b-202">Wählen Sie eine Aktion aus, in dem alle Parameter in der Liste eine Übereinstimmung im URI verfügt.</span><span class="sxs-lookup"><span data-stu-id="4114b-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="4114b-203">Wenn mehr, eine Aktion diese Kriterien erfüllt, wählen Sie die Woche mit der meisten Parameter übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="4114b-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="4114b-204">Ignorieren Sie Aktionen mit der **[NonAction]** Attribut.</span><span class="sxs-lookup"><span data-stu-id="4114b-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="4114b-205">Schritt #3 ist die am häufigsten verwirrend.</span><span class="sxs-lookup"><span data-stu-id="4114b-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="4114b-206">Die grundlegende Idee ist, dass ein Parameter den Wert entweder aus dem URI, aus dem Anforderungstext oder aus einer benutzerdefinierten Bindung abrufen kann.</span><span class="sxs-lookup"><span data-stu-id="4114b-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="4114b-207">Für Parameter, die aus dem URI enthalten sind, möchten wir sicherstellen, dass der URI einen Wert für diesen Parameter, entweder im Pfad (über die Route-Wörterbuch) oder in der Abfragezeichenfolge enthält.</span><span class="sxs-lookup"><span data-stu-id="4114b-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="4114b-208">Betrachten Sie beispielsweise die folgende Aktion aus:</span><span class="sxs-lookup"><span data-stu-id="4114b-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="4114b-209">Die *Id* Parameter bindet an den URI.</span><span class="sxs-lookup"><span data-stu-id="4114b-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="4114b-210">Diese Aktion kann daher nur einen URI übereinstimmen, die einen Wert für "Id", im Wörterbuch Route oder in der Abfragezeichenfolge enthält.</span><span class="sxs-lookup"><span data-stu-id="4114b-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="4114b-211">Optionale Parameter sind eine Ausnahme aus, da sie optional sind.</span><span class="sxs-lookup"><span data-stu-id="4114b-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="4114b-212">Für einen optionalen Parameter ist es in Ordnung Wenn die Bindung den Wert aus dem URI nicht.</span><span class="sxs-lookup"><span data-stu-id="4114b-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="4114b-213">Komplexe Typen stellen eine Ausnahme für einen anderen Grund.</span><span class="sxs-lookup"><span data-stu-id="4114b-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="4114b-214">Ein komplexer Typ kann nur über eine benutzerdefinierte Bindung an den URI binden.</span><span class="sxs-lookup"><span data-stu-id="4114b-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="4114b-215">Aber in diesem Fall das Framework darf nicht bereits im Voraus wissen, ob der Parameter an einen bestimmten URI gebunden würde.</span><span class="sxs-lookup"><span data-stu-id="4114b-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="4114b-216">Sie müssen herausfinden, rufen Sie die Bindung.</span><span class="sxs-lookup"><span data-stu-id="4114b-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="4114b-217">Das Ziel der Auswahlalgorithmus ist der statische Beschreibung vor dem Aufrufen von Bindungen eine Aktion aus.</span><span class="sxs-lookup"><span data-stu-id="4114b-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="4114b-218">Aus diesem Grund werden komplexe Typen aus den entsprechenden Algorithmus ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="4114b-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="4114b-219">Nachdem die Aktion ausgewählt wurde, werden alle parameterbindungen aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="4114b-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="4114b-220">Zusammenfassung:</span><span class="sxs-lookup"><span data-stu-id="4114b-220">Summary:</span></span>

- <span data-ttu-id="4114b-221">Die Aktion muss die HTTP-Methode der Anforderung übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="4114b-222">Der Name der Aktion muss den "Action"-Eintrag im Wörterbuch Route vorhanden ist, falls vorhanden übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="4114b-223">Für jeden Parameter der Aktion Wenn der Parameter, aus dem URI erstellt wird, muss dann der Name des Parameters im Wörterbuch Route oder in der URI-Abfragezeichenfolge gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="4114b-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="4114b-224">(Parameter mit komplexen Typen und optionale Parameter werden ausgeschlossen.)</span><span class="sxs-lookup"><span data-stu-id="4114b-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="4114b-225">Versuchen Sie es mit der höchsten Anzahl von Parametern übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="4114b-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="4114b-226">Die beste Übereinstimmung möglicherweise eine Methode ohne Parameter.</span><span class="sxs-lookup"><span data-stu-id="4114b-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="4114b-227">Erweitertes Beispiel</span><span class="sxs-lookup"><span data-stu-id="4114b-227">Extended Example</span></span>

<span data-ttu-id="4114b-228">Routen:</span><span class="sxs-lookup"><span data-stu-id="4114b-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="4114b-229">Controller:</span><span class="sxs-lookup"><span data-stu-id="4114b-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="4114b-230">HTTP-Anforderung:</span><span class="sxs-lookup"><span data-stu-id="4114b-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="4114b-231">Weiterleiten von übereinstimmenden</span><span class="sxs-lookup"><span data-stu-id="4114b-231">Route Matching</span></span>

<span data-ttu-id="4114b-232">Der URI entspricht der Route, die mit dem Namen "DefaultApi".</span><span class="sxs-lookup"><span data-stu-id="4114b-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="4114b-233">Das Wörterbuch für die Route enthält die folgenden Einträge:</span><span class="sxs-lookup"><span data-stu-id="4114b-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="4114b-234">Controller: "Produkte"</span><span class="sxs-lookup"><span data-stu-id="4114b-234">controller: "products"</span></span>
- <span data-ttu-id="4114b-235">id: "1"</span><span class="sxs-lookup"><span data-stu-id="4114b-235">id: "1"</span></span>

<span data-ttu-id="4114b-236">Des Routenwörterbuchs enthält nicht den Abfragezeichenfolgen-Parameter, "Version" und "Details", aber diese werden betrachtet werden bei der Auswahl der Aktion.</span><span class="sxs-lookup"><span data-stu-id="4114b-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="4114b-237">Auswahl der Domänencontroller</span><span class="sxs-lookup"><span data-stu-id="4114b-237">Controller Selection</span></span>

<span data-ttu-id="4114b-238">Über den "Controller"-Eintrag im Wörterbuch weiterleiten, ist der Typ des Controllers `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="4114b-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="4114b-239">Aktionsauswahl</span><span class="sxs-lookup"><span data-stu-id="4114b-239">Action Selection</span></span>

<span data-ttu-id="4114b-240">Die HTTP-Anforderung ist eine GET-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="4114b-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="4114b-241">Die Controlleraktionen, die GET zu unterstützen sind `GetAll`, `GetById`, und `FindProductsByName`.</span><span class="sxs-lookup"><span data-stu-id="4114b-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="4114b-242">Des Routenwörterbuchs enthält keinen Eintrag für "Action", daher wir nicht mit dem Aktionsnamen übereinstimmen müssen.</span><span class="sxs-lookup"><span data-stu-id="4114b-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="4114b-243">Als Nächstes versuchen wir, Parameternamen für die Aktionen entsprechen nur auf den GET-Aktionen suchen.</span><span class="sxs-lookup"><span data-stu-id="4114b-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="4114b-244">Aktion</span><span class="sxs-lookup"><span data-stu-id="4114b-244">Action</span></span> | <span data-ttu-id="4114b-245">Parameter zur Übereinstimmung</span><span class="sxs-lookup"><span data-stu-id="4114b-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="4114b-246">none</span><span class="sxs-lookup"><span data-stu-id="4114b-246">none</span></span> |
| `GetById` | <span data-ttu-id="4114b-247">"id"</span><span class="sxs-lookup"><span data-stu-id="4114b-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="4114b-248">"Name"</span><span class="sxs-lookup"><span data-stu-id="4114b-248">"name"</span></span> |

<span data-ttu-id="4114b-249">Beachten Sie, dass die *Version* Parameter `GetById` gilt nicht, da es sich um einen optionalen Parameter ist.</span><span class="sxs-lookup"><span data-stu-id="4114b-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="4114b-250">Die `GetAll` Methode entspricht im Grunde kann.</span><span class="sxs-lookup"><span data-stu-id="4114b-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="4114b-251">Die `GetById` Methode auch entspricht, da des Routenwörterbuchs "Id" enthält.</span><span class="sxs-lookup"><span data-stu-id="4114b-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="4114b-252">Die `FindProductsByName` Methode stimmt nicht überein.</span><span class="sxs-lookup"><span data-stu-id="4114b-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="4114b-253">Die `GetById` wins-Methode, da es einen Parameter, und keine Parameter für entspricht `GetAll`.</span><span class="sxs-lookup"><span data-stu-id="4114b-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="4114b-254">Die Methode wird mit den folgenden Parameterwerten aufgerufen:</span><span class="sxs-lookup"><span data-stu-id="4114b-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="4114b-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="4114b-255">*id* = 1</span></span>
- <span data-ttu-id="4114b-256">*Version* = 1.5</span><span class="sxs-lookup"><span data-stu-id="4114b-256">*version* = 1.5</span></span>

<span data-ttu-id="4114b-257">Beachten Sie, dass, obwohl *Version* nicht verwendet wurde, in der Auswahlalgorithmus stammt der Wert des Parameters die URI-Abfragezeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="4114b-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="4114b-258">Erweiterungspunkte</span><span class="sxs-lookup"><span data-stu-id="4114b-258">Extension Points</span></span>

<span data-ttu-id="4114b-259">Web-API stellt Erweiterungspunkte für einige Teile der routing-Prozess bereit.</span><span class="sxs-lookup"><span data-stu-id="4114b-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="4114b-260">Interface</span><span class="sxs-lookup"><span data-stu-id="4114b-260">Interface</span></span> | <span data-ttu-id="4114b-261">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4114b-261">Description</span></span> |
| --- | --- |
| **<span data-ttu-id="4114b-262">IHttpControllerSelector</span><span class="sxs-lookup"><span data-stu-id="4114b-262">IHttpControllerSelector</span></span>** | <span data-ttu-id="4114b-263">Wählt den Controller.</span><span class="sxs-lookup"><span data-stu-id="4114b-263">Selects the controller.</span></span> |
| **<span data-ttu-id="4114b-264">IHttpControllerTypeResolver</span><span class="sxs-lookup"><span data-stu-id="4114b-264">IHttpControllerTypeResolver</span></span>** | <span data-ttu-id="4114b-265">Ruft die Liste der Controllertypen ab.</span><span class="sxs-lookup"><span data-stu-id="4114b-265">Gets the list of controller types.</span></span> <span data-ttu-id="4114b-266">Die **DefaultHttpControllerSelector** wählt den Controllertyp aus dieser Liste.</span><span class="sxs-lookup"><span data-stu-id="4114b-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| **<span data-ttu-id="4114b-267">IAssembliesResolver</span><span class="sxs-lookup"><span data-stu-id="4114b-267">IAssembliesResolver</span></span>** | <span data-ttu-id="4114b-268">Ruft die Liste der Projektassemblys ab.</span><span class="sxs-lookup"><span data-stu-id="4114b-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="4114b-269">Die **IHttpControllerTypeResolver** Schnittstelle verwendet diese Liste, um die Controllertypen gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="4114b-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| **<span data-ttu-id="4114b-270">IHttpControllerActivator</span><span class="sxs-lookup"><span data-stu-id="4114b-270">IHttpControllerActivator</span></span>** | <span data-ttu-id="4114b-271">Erstellen von neuen Controllerinstanzen.</span><span class="sxs-lookup"><span data-stu-id="4114b-271">Creates new controller instances.</span></span> |
| **<span data-ttu-id="4114b-272">IHttpActionSelector</span><span class="sxs-lookup"><span data-stu-id="4114b-272">IHttpActionSelector</span></span>** | <span data-ttu-id="4114b-273">Wählt die Aktion.</span><span class="sxs-lookup"><span data-stu-id="4114b-273">Selects the action.</span></span> |
| **<span data-ttu-id="4114b-274">IHttpActionInvoker</span><span class="sxs-lookup"><span data-stu-id="4114b-274">IHttpActionInvoker</span></span>** | <span data-ttu-id="4114b-275">Ruft die Aktion.</span><span class="sxs-lookup"><span data-stu-id="4114b-275">Invokes the action.</span></span> |

<span data-ttu-id="4114b-276">Um Ihre eigene Implementierung für den folgenden Schnittstellen bereitzustellen, verwenden die **Services** Auflistung auf der **HttpConfiguration** Objekt:</span><span class="sxs-lookup"><span data-stu-id="4114b-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
