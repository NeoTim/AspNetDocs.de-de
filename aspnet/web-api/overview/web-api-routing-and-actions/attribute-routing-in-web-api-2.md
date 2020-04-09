---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Attributrouting in ASP.NET Web-API 2 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675387"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="cc798-102">Attributrouting in ASP.NET Web-API 2</span><span class="sxs-lookup"><span data-stu-id="cc798-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="cc798-103">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cc798-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cc798-104">*Routing* ist die Art und Weise, wie die Web-API einen URI mit einer Aktion abgleicht.</span><span class="sxs-lookup"><span data-stu-id="cc798-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="cc798-105">Web API 2 unterstützt einen neuen Routingtyp, das *attributrouting*.</span><span class="sxs-lookup"><span data-stu-id="cc798-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="cc798-106">Wie der Name schon sagt, verwendet attributrouting Attribute, um Routen zu definieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="cc798-107">Das Attributrouting gibt Ihnen mehr Kontrolle über die URIs in Ihrer Web-API.</span><span class="sxs-lookup"><span data-stu-id="cc798-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="cc798-108">Sie können z. B. problemlos URIs erstellen, die Ressourcenhierarchien beschreiben.</span><span class="sxs-lookup"><span data-stu-id="cc798-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="cc798-109">Der frühere Routingstil, das als konventionsbasiertes Routing bezeichnet wird, wird weiterhin vollständig unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cc798-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="cc798-110">Tatsächlich können Sie beide Techniken im selben Projekt kombinieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="cc798-111">In diesem Thema wird gezeigt, wie Attributrouting aktiviert wird, und es werden die verschiedenen Optionen für das Attributrouting beschrieben.</span><span class="sxs-lookup"><span data-stu-id="cc798-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="cc798-112">Ein End-to-End-Tutorial, das Attributrouting verwendet, finden Sie unter [Erstellen einer REST-API mit Attributrouting in Web-API 2](create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="cc798-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc798-113">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="cc798-113">Prerequisites</span></span>

<span data-ttu-id="cc798-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community-, Professional- oder Enterprise-Edition</span><span class="sxs-lookup"><span data-stu-id="cc798-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="cc798-115">Alternativ können Sie NuGet Package Manager verwenden, um die erforderlichen Pakete zu installieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="cc798-116">Wählen Sie im Menü **Extras** in Visual Studio **NuGet Package Manager**aus , und wählen Sie dann **Package Manager Console**aus.</span><span class="sxs-lookup"><span data-stu-id="cc798-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="cc798-117">Geben Sie im Fenster Package Manager Console den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="cc798-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="cc798-118">Warum Attributrouting?</span><span class="sxs-lookup"><span data-stu-id="cc798-118">Why Attribute Routing?</span></span>

<span data-ttu-id="cc798-119">Die erste Version der Web-API verwendet *konventionsbasiertes* Routing.</span><span class="sxs-lookup"><span data-stu-id="cc798-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="cc798-120">In diesem Routingtyp definieren Sie eine oder mehrere Routenvorlagen, bei denen es sich im Grunde um parametrisierte Zeichenfolgen handelt.</span><span class="sxs-lookup"><span data-stu-id="cc798-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="cc798-121">Wenn das Framework eine Anforderung empfängt, stimmt es mit dem URI mit der Routenvorlage überein.</span><span class="sxs-lookup"><span data-stu-id="cc798-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="cc798-122">Weitere Informationen zum konventionsbasierten Routing finden Sie unter [Routing in ASP.NET Web-API](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="cc798-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="cc798-123">Ein Vorteil des konventionsbasierten Routings besteht darin, dass Vorlagen an einem einzigen Ort definiert werden und die Routingregeln konsistent auf alle Controller angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="cc798-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="cc798-124">Leider macht es das konventionsbasierte Routing schwierig, bestimmte URI-Muster zu unterstützen, die in RESTful-APIs üblich sind.</span><span class="sxs-lookup"><span data-stu-id="cc798-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="cc798-125">Ressourcen enthalten z. B. häufig untergeordnete Ressourcen: Kunden haben Aufträge, Filme haben Schauspieler, Bücher haben Autoren usw.</span><span class="sxs-lookup"><span data-stu-id="cc798-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="cc798-126">Es ist natürlich, URIs zu erstellen, die diese Beziehungen widerspiegeln:</span><span class="sxs-lookup"><span data-stu-id="cc798-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="cc798-127">Dieser URI-Typ ist mit konventionsbasiertem Routing schwer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cc798-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="cc798-128">Obwohl dies möglich ist, werden die Ergebnisse nicht gut skaliert, wenn Sie über viele Controller oder Ressourcentypen verfügen.</span><span class="sxs-lookup"><span data-stu-id="cc798-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="cc798-129">Beim Attributrouting ist es trivial, eine Route für diesen URI zu definieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="cc798-130">Sie fügen der Controlleraktion einfach ein Attribut hinzu:</span><span class="sxs-lookup"><span data-stu-id="cc798-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="cc798-131">Hier sind einige andere Muster, die Attributrouting macht einfach.</span><span class="sxs-lookup"><span data-stu-id="cc798-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="cc798-132">**API-Versionsverwaltung**</span><span class="sxs-lookup"><span data-stu-id="cc798-132">**API versioning**</span></span>

<span data-ttu-id="cc798-133">In diesem Beispiel würde "/api/v1/products" an einen anderen Controller als "/api/v2/products" weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="cc798-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="cc798-134">**Überladene URI-Segmente**</span><span class="sxs-lookup"><span data-stu-id="cc798-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="cc798-135">In diesem Beispiel ist "1" eine Bestellnummer, aber "ausstehend" wird einer Auflistung zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="cc798-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="cc798-136">**Mehrere Parametertypen**</span><span class="sxs-lookup"><span data-stu-id="cc798-136">**Multiple parameter types**</span></span>

<span data-ttu-id="cc798-137">In diesem Beispiel ist "1" eine Bestellnummer, aber "2013/06/16" gibt ein Datum an.</span><span class="sxs-lookup"><span data-stu-id="cc798-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="cc798-138">Aktivieren des Attributroutings</span><span class="sxs-lookup"><span data-stu-id="cc798-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="cc798-139">Um Attributrouting zu aktivieren, rufen Sie **MapHttpAttributeRoutes** während der Konfiguration auf.</span><span class="sxs-lookup"><span data-stu-id="cc798-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="cc798-140">Diese Erweiterungsmethode ist in der **System.Web.Http.HttpConfigurationExtensions-Klasse** definiert.</span><span class="sxs-lookup"><span data-stu-id="cc798-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="cc798-141">Attributrouting kann mit [konventionsbasiertem](routing-in-aspnet-web-api.md) Routing kombiniert werden.</span><span class="sxs-lookup"><span data-stu-id="cc798-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="cc798-142">Um konventionsbasierte Routen zu definieren, rufen Sie die **MapHttpRoute-Methode** auf.</span><span class="sxs-lookup"><span data-stu-id="cc798-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="cc798-143">Weitere Informationen zum Konfigurieren der Web-API finden Sie unter [Konfigurieren ASP.NET Web-API 2](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="cc798-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="cc798-144">Hinweis: Migrieren von Web-API 1</span><span class="sxs-lookup"><span data-stu-id="cc798-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="cc798-145">Vor Web-API 2 generierten die Web-API-Projektvorlagen Code wie folgt:</span><span class="sxs-lookup"><span data-stu-id="cc798-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="cc798-146">Wenn das Attributrouting aktiviert ist, löst dieser Code eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="cc798-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="cc798-147">Wenn Sie ein vorhandenes Web-API-Projekt aktualisieren, um Attributrouting zu verwenden, stellen Sie sicher, dass Dieser Konfigurationscode wie folgt aktualisiert wird:</span><span class="sxs-lookup"><span data-stu-id="cc798-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="cc798-148">Weitere Informationen finden Sie unter [Konfigurieren der Web-API mit ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="cc798-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="cc798-149">Hinzufügen von Routenattributen</span><span class="sxs-lookup"><span data-stu-id="cc798-149">Adding Route Attributes</span></span>

<span data-ttu-id="cc798-150">Hier ist ein Beispiel für eine Route, die mit einem Attribut definiert wurde:</span><span class="sxs-lookup"><span data-stu-id="cc798-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="cc798-151">Die &quot;Zeichenfolge customers/'customerId'/orders&quot; ist die URI-Vorlage für die Route.</span><span class="sxs-lookup"><span data-stu-id="cc798-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="cc798-152">Die Web-API versucht, den Anforderungs-URI mit der Vorlage abzugleichen.</span><span class="sxs-lookup"><span data-stu-id="cc798-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="cc798-153">In diesem Beispiel sind "customers" und "orders" Literalsegmente, und "-customerId" ist ein variabler Parameter.</span><span class="sxs-lookup"><span data-stu-id="cc798-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="cc798-154">Die folgenden URIs würden mit dieser Vorlage übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="cc798-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="cc798-155">Sie können die Übereinstimmung einschränken, indem Sie [Einschränkungen](#constraints)verwenden, die weiter unten in diesem Thema beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="cc798-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="cc798-156">Beachten Sie, dass &quot;&quot; der Parameter "customerId" in der Routenvorlage mit dem Namen des *customerId-Parameters* in der Methode übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="cc798-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="cc798-157">Wenn die Web-API die Controlleraktion aufruft, versucht sie, die Routenparameter zu binden.</span><span class="sxs-lookup"><span data-stu-id="cc798-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="cc798-158">Wenn der URI beispielsweise `http://example.com/customers/1/orders`lautet, versucht die Web-API, den Wert "1" an den *customerId-Parameter* in der Aktion zu binden.</span><span class="sxs-lookup"><span data-stu-id="cc798-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="cc798-159">Eine URI-Vorlage kann mehrere Parameter enthalten:</span><span class="sxs-lookup"><span data-stu-id="cc798-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="cc798-160">Alle Controllermethoden, die nicht über ein Routenattribut verfügen, verwenden konventionsbasiertes Routing.</span><span class="sxs-lookup"><span data-stu-id="cc798-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="cc798-161">Auf diese Weise können Sie beide Routingtypen im gleichen Projekt kombinieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cc798-162">HTTP-Methoden</span><span class="sxs-lookup"><span data-stu-id="cc798-162">HTTP Methods</span></span>

<span data-ttu-id="cc798-163">Web-API wählt auch Aktionen basierend auf der HTTP-Methode der Anforderung (GET, POST, etc.).</span><span class="sxs-lookup"><span data-stu-id="cc798-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="cc798-164">Standardmäßig sucht die Web-API nach einer Übereinstimmung ohne Groß-/Kleinschreibung mit dem Start des Controllermethodennamens.</span><span class="sxs-lookup"><span data-stu-id="cc798-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="cc798-165">Beispielsweise entspricht eine Controllermethode mit dem Namen `PutCustomers` einer HTTP PUT-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="cc798-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="cc798-166">Sie können diese Konvention überschreiben, indem Sie die Methode mit den folgenden Attributen dekorieren:</span><span class="sxs-lookup"><span data-stu-id="cc798-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="cc798-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="cc798-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="cc798-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="cc798-168">**[HttpGet]**</span></span>
- <span data-ttu-id="cc798-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="cc798-169">**[HttpHead]**</span></span>
- <span data-ttu-id="cc798-170">**[HttpOptionen]**</span><span class="sxs-lookup"><span data-stu-id="cc798-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="cc798-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="cc798-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="cc798-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="cc798-172">**[HttpPost]**</span></span>
- <span data-ttu-id="cc798-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="cc798-173">**[HttpPut]**</span></span>

<span data-ttu-id="cc798-174">Im folgenden Beispiel wird die CreateBook-Methode HTTP-POST-Anforderungen zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="cc798-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="cc798-175">Verwenden Sie für alle anderen HTTP-Methoden, einschließlich nicht standardmäßiger Methoden, das **AcceptVerbs-Attribut,** das eine Liste von HTTP-Methoden enthält.</span><span class="sxs-lookup"><span data-stu-id="cc798-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="cc798-176">Routenpräfixe</span><span class="sxs-lookup"><span data-stu-id="cc798-176">Route Prefixes</span></span>

<span data-ttu-id="cc798-177">Häufig beginnen die Routen in einem Controller mit demselben Präfix.</span><span class="sxs-lookup"><span data-stu-id="cc798-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="cc798-178">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cc798-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="cc798-179">Sie können ein gemeinsames Präfix für einen gesamten Controller festlegen, indem Sie das Attribut **[RoutePrefix]** verwenden:</span><span class="sxs-lookup"><span data-stu-id="cc798-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="cc798-180">Verwenden Sie eine Tilde für das Methodenattribut, um das Routenpräfix zu überschreiben:</span><span class="sxs-lookup"><span data-stu-id="cc798-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="cc798-181">Das Routenpräfix kann Parameter enthalten:</span><span class="sxs-lookup"><span data-stu-id="cc798-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="cc798-182">Routeneinschränkungen</span><span class="sxs-lookup"><span data-stu-id="cc798-182">Route Constraints</span></span>

<span data-ttu-id="cc798-183">Mit Routeneinschränkungen können Sie einschränken, wie die Parameter in der Routenvorlage abgeglichen werden.</span><span class="sxs-lookup"><span data-stu-id="cc798-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="cc798-184">Die allgemeine &quot;Syntax lautet "Parameter:Constraint"&quot;.</span><span class="sxs-lookup"><span data-stu-id="cc798-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="cc798-185">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cc798-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="cc798-186">Hier wird die erste Route nur &quot;&quot; ausgewählt, wenn das ID-Segment des URI eine ganze Zahl ist.</span><span class="sxs-lookup"><span data-stu-id="cc798-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="cc798-187">Andernfalls wird die zweite Route gewählt.</span><span class="sxs-lookup"><span data-stu-id="cc798-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="cc798-188">In der folgenden Tabelle sind die unterstützten Einschränkungen aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="cc798-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="cc798-189">Einschränkung</span><span class="sxs-lookup"><span data-stu-id="cc798-189">Constraint</span></span> | <span data-ttu-id="cc798-190">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="cc798-190">Description</span></span> | <span data-ttu-id="cc798-191">Beispiel</span><span class="sxs-lookup"><span data-stu-id="cc798-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc798-192">alpha</span><span class="sxs-lookup"><span data-stu-id="cc798-192">alpha</span></span> | <span data-ttu-id="cc798-193">Entspricht groß- oder kleinbuchstaben lateinischen Alphabetzeichen (a-z, A-Z)</span><span class="sxs-lookup"><span data-stu-id="cc798-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="cc798-194">X:alpha</span><span class="sxs-lookup"><span data-stu-id="cc798-194">{x:alpha}</span></span> |
| <span data-ttu-id="cc798-195">bool</span><span class="sxs-lookup"><span data-stu-id="cc798-195">bool</span></span> | <span data-ttu-id="cc798-196">Entspricht einem booleschen Wert.</span><span class="sxs-lookup"><span data-stu-id="cc798-196">Matches a Boolean value.</span></span> | <span data-ttu-id="cc798-197">X:bool</span><span class="sxs-lookup"><span data-stu-id="cc798-197">{x:bool}</span></span> |
| <span data-ttu-id="cc798-198">datetime</span><span class="sxs-lookup"><span data-stu-id="cc798-198">datetime</span></span> | <span data-ttu-id="cc798-199">Entspricht einem **DateTime-Wert.**</span><span class="sxs-lookup"><span data-stu-id="cc798-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="cc798-200">X:datetime</span><span class="sxs-lookup"><span data-stu-id="cc798-200">{x:datetime}</span></span> |
| <span data-ttu-id="cc798-201">Decimal</span><span class="sxs-lookup"><span data-stu-id="cc798-201">decimal</span></span> | <span data-ttu-id="cc798-202">Entspricht einem Dezimalwert.</span><span class="sxs-lookup"><span data-stu-id="cc798-202">Matches a decimal value.</span></span> | <span data-ttu-id="cc798-203">X:dezimal</span><span class="sxs-lookup"><span data-stu-id="cc798-203">{x:decimal}</span></span> |
| <span data-ttu-id="cc798-204">double</span><span class="sxs-lookup"><span data-stu-id="cc798-204">double</span></span> | <span data-ttu-id="cc798-205">Entspricht einem 64-Bit-Gleitkommawert.</span><span class="sxs-lookup"><span data-stu-id="cc798-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="cc798-206">X:double</span><span class="sxs-lookup"><span data-stu-id="cc798-206">{x:double}</span></span> |
| <span data-ttu-id="cc798-207">float</span><span class="sxs-lookup"><span data-stu-id="cc798-207">float</span></span> | <span data-ttu-id="cc798-208">Entspricht einem 32-Bit-Gleitkommawert.</span><span class="sxs-lookup"><span data-stu-id="cc798-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="cc798-209">X:float</span><span class="sxs-lookup"><span data-stu-id="cc798-209">{x:float}</span></span> |
| <span data-ttu-id="cc798-210">guid</span><span class="sxs-lookup"><span data-stu-id="cc798-210">guid</span></span> | <span data-ttu-id="cc798-211">Entspricht einem GUID-Wert.</span><span class="sxs-lookup"><span data-stu-id="cc798-211">Matches a GUID value.</span></span> | <span data-ttu-id="cc798-212">X:guid</span><span class="sxs-lookup"><span data-stu-id="cc798-212">{x:guid}</span></span> |
| <span data-ttu-id="cc798-213">INT</span><span class="sxs-lookup"><span data-stu-id="cc798-213">int</span></span> | <span data-ttu-id="cc798-214">Entspricht einem 32-Bit-Ganzzahlwert.</span><span class="sxs-lookup"><span data-stu-id="cc798-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="cc798-215">X:int</span><span class="sxs-lookup"><span data-stu-id="cc798-215">{x:int}</span></span> |
| <span data-ttu-id="cc798-216">length</span><span class="sxs-lookup"><span data-stu-id="cc798-216">length</span></span> | <span data-ttu-id="cc798-217">Entspricht einer Zeichenfolge mit der angegebenen Länge oder innerhalb eines angegebenen Längenbereichs.</span><span class="sxs-lookup"><span data-stu-id="cc798-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="cc798-218">X:Länge(6) X:Länge(1,20)"</span><span class="sxs-lookup"><span data-stu-id="cc798-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="cc798-219">long</span><span class="sxs-lookup"><span data-stu-id="cc798-219">long</span></span> | <span data-ttu-id="cc798-220">Entspricht einem 64-Bit-Ganzzahlwert.</span><span class="sxs-lookup"><span data-stu-id="cc798-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="cc798-221">X:lang</span><span class="sxs-lookup"><span data-stu-id="cc798-221">{x:long}</span></span> |
| <span data-ttu-id="cc798-222">max</span><span class="sxs-lookup"><span data-stu-id="cc798-222">max</span></span> | <span data-ttu-id="cc798-223">Entspricht einer ganzzahligen Datei mit einem maximalwert.</span><span class="sxs-lookup"><span data-stu-id="cc798-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="cc798-224">X:max(10)"</span><span class="sxs-lookup"><span data-stu-id="cc798-224">{x:max(10)}</span></span> |
| <span data-ttu-id="cc798-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="cc798-225">maxlength</span></span> | <span data-ttu-id="cc798-226">Entspricht einer Zeichenfolge mit einer maximalen Länge.</span><span class="sxs-lookup"><span data-stu-id="cc798-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="cc798-227">X:maxlength(10)</span><span class="sxs-lookup"><span data-stu-id="cc798-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="cc798-228">Min</span><span class="sxs-lookup"><span data-stu-id="cc798-228">min</span></span> | <span data-ttu-id="cc798-229">Entspricht einer ganzzahligen Datei mit einem Mindestwert.</span><span class="sxs-lookup"><span data-stu-id="cc798-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="cc798-230">X:min(10)</span><span class="sxs-lookup"><span data-stu-id="cc798-230">{x:min(10)}</span></span> |
| <span data-ttu-id="cc798-231">Minlength</span><span class="sxs-lookup"><span data-stu-id="cc798-231">minlength</span></span> | <span data-ttu-id="cc798-232">Entspricht einer Zeichenfolge mit einer Mindestlänge.</span><span class="sxs-lookup"><span data-stu-id="cc798-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="cc798-233">x:minlength(10)</span><span class="sxs-lookup"><span data-stu-id="cc798-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="cc798-234">range</span><span class="sxs-lookup"><span data-stu-id="cc798-234">range</span></span> | <span data-ttu-id="cc798-235">Entspricht einer ganzzahligen Datei innerhalb eines Wertebereichs.</span><span class="sxs-lookup"><span data-stu-id="cc798-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="cc798-236">X:range(10,50)"</span><span class="sxs-lookup"><span data-stu-id="cc798-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="cc798-237">regex</span><span class="sxs-lookup"><span data-stu-id="cc798-237">regex</span></span> | <span data-ttu-id="cc798-238">Entspricht einem regulären Ausdruck.</span><span class="sxs-lookup"><span data-stu-id="cc798-238">Matches a regular expression.</span></span> | <span data-ttu-id="cc798-239">X:regex(-d{3}--d{3}--d-D-)){4}</span><span class="sxs-lookup"><span data-stu-id="cc798-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="cc798-240">Beachten Sie, dass einige der &quot;Einschränkungen, z. B. min&quot;, Argumente in Klammern verwenden.</span><span class="sxs-lookup"><span data-stu-id="cc798-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="cc798-241">Sie können mehrere Abhängigkeiten auf einen Parameter anwenden, der durch einen Doppelpunkt getrennt ist.</span><span class="sxs-lookup"><span data-stu-id="cc798-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="cc798-242">Benutzerdefinierte Routeneinschränkungen</span><span class="sxs-lookup"><span data-stu-id="cc798-242">Custom Route Constraints</span></span>

<span data-ttu-id="cc798-243">Sie können benutzerdefinierte Routeneinschränkungen erstellen, indem Sie die **IHttpRouteConstraint-Schnittstelle** implementieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="cc798-244">Die folgende Einschränkung beschränkt z. B. einen Parameter auf einen Ganzzahlwert ungleich Null.</span><span class="sxs-lookup"><span data-stu-id="cc798-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="cc798-245">Der folgende Code zeigt, wie die Einschränkung registriert wird:</span><span class="sxs-lookup"><span data-stu-id="cc798-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="cc798-246">Jetzt können Sie die Einschränkung in Ihren Routen anwenden:</span><span class="sxs-lookup"><span data-stu-id="cc798-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="cc798-247">Sie können auch die gesamte **DefaultInlineConstraintResolver-Klasse** ersetzen, indem Sie die **IInlineConstraintResolver-Schnittstelle** implementieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="cc798-248">Dadurch werden alle integrierten Einschränkungen ersetzt, es sei denn, Ihre Implementierung von **IInlineConstraintResolver** fügt sie ausdrücklich hinzu.</span><span class="sxs-lookup"><span data-stu-id="cc798-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="cc798-249">Optionale URI-Parameter und Standardwerte</span><span class="sxs-lookup"><span data-stu-id="cc798-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="cc798-250">Sie können einen URI-Parameter optional machen, indem Sie dem Routenparameter ein Fragezeichen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cc798-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="cc798-251">Wenn ein Routenparameter optional ist, müssen Sie einen Standardwert für den Methodenparameter definieren.</span><span class="sxs-lookup"><span data-stu-id="cc798-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="cc798-252">Geben `/api/books/locale/1033` Sie `/api/books/locale` in diesem Beispiel dieselbe Ressource zurück.</span><span class="sxs-lookup"><span data-stu-id="cc798-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="cc798-253">Alternativ können Sie einen Standardwert in der Routenvorlage wie folgt angeben:</span><span class="sxs-lookup"><span data-stu-id="cc798-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="cc798-254">Dies ist fast das gleiche wie im vorherigen Beispiel, aber es gibt einen leichten Unterschied im Verhalten, wenn der Standardwert angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="cc798-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="cc798-255">Im ersten Beispiel wird der Standardwert 1033 direkt dem Methodenparameter zugewiesen, sodass der Parameter genau diesen Wert hat.</span><span class="sxs-lookup"><span data-stu-id="cc798-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="cc798-256">Im zweiten Beispiel ("-lcid:int=1033") wird der Standardwert "1033" durch den Modellbindungsprozess durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="cc798-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="cc798-257">Der Standardmodellbinder konvertiert "1033" in den numerischen Wert 1033.</span><span class="sxs-lookup"><span data-stu-id="cc798-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="cc798-258">Sie können jedoch einen benutzerdefinierten Modellbinder anschließen, was etwas anderes tun kann.</span><span class="sxs-lookup"><span data-stu-id="cc798-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="cc798-259">(In den meisten Fällen sind die beiden Formulare gleichwertig, es sei denn, Sie haben benutzerdefinierte Modellbindemittel in der Pipeline.)</span><span class="sxs-lookup"><span data-stu-id="cc798-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="cc798-260">Routennamen</span><span class="sxs-lookup"><span data-stu-id="cc798-260">Route Names</span></span>

<span data-ttu-id="cc798-261">In der Web-API hat jede Route einen Namen.</span><span class="sxs-lookup"><span data-stu-id="cc798-261">In Web API, every route has a name.</span></span> <span data-ttu-id="cc798-262">Routennamen sind nützlich zum Generieren von Verknüpfungen, sodass Sie einen Link in eine HTTP-Antwort einschließen können.</span><span class="sxs-lookup"><span data-stu-id="cc798-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="cc798-263">Um den Routennamen anzugeben, legen Sie die **Name-Eigenschaft** für das Attribut fest.</span><span class="sxs-lookup"><span data-stu-id="cc798-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="cc798-264">Das folgende Beispiel zeigt, wie der Routenname festgelegt wird und wie der Routenname beim Generieren einer Verknüpfung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cc798-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="cc798-265">Routenreihenfolge</span><span class="sxs-lookup"><span data-stu-id="cc798-265">Route Order</span></span>

<span data-ttu-id="cc798-266">Wenn das Framework versucht, einen URI mit einer Route abzugleichen, werden die Routen in einer bestimmten Reihenfolge ausgewertet.</span><span class="sxs-lookup"><span data-stu-id="cc798-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="cc798-267">Um den Auftrag anzugeben, legen Sie die **Order-Eigenschaft** für das route-Attribut fest.</span><span class="sxs-lookup"><span data-stu-id="cc798-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="cc798-268">Niedrigere Werte werden zuerst ausgewertet.</span><span class="sxs-lookup"><span data-stu-id="cc798-268">Lower values are evaluated first.</span></span> <span data-ttu-id="cc798-269">Der Standardauftragswert ist Null.</span><span class="sxs-lookup"><span data-stu-id="cc798-269">The default order value is zero.</span></span>

<span data-ttu-id="cc798-270">Hier ist, wie die Gesamtbestellung bestimmt wird:</span><span class="sxs-lookup"><span data-stu-id="cc798-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="cc798-271">Vergleichen Sie die **Order-Eigenschaft** des route-Attributs.</span><span class="sxs-lookup"><span data-stu-id="cc798-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="cc798-272">Sehen Sie sich jedes URI-Segment in der Routenvorlage an.</span><span class="sxs-lookup"><span data-stu-id="cc798-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="cc798-273">Ordnen Sie für jedes Segment wie folgt an:</span><span class="sxs-lookup"><span data-stu-id="cc798-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="cc798-274">Literale Segmente.</span><span class="sxs-lookup"><span data-stu-id="cc798-274">Literal segments.</span></span>
    2. <span data-ttu-id="cc798-275">Routenparameter mit Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="cc798-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="cc798-276">Routenparameter ohne Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="cc798-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="cc798-277">Platzhalterparametersegmente mit Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="cc798-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="cc798-278">Platzhalterparametersegmente ohne Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="cc798-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="cc798-279">Im Falle eines Unentschiedens werden Routen durch einen Ordinalzeichenfolgenvergleich ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) der Routenvorlage angeordnet.</span><span class="sxs-lookup"><span data-stu-id="cc798-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="cc798-280">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cc798-280">Here is an example.</span></span> <span data-ttu-id="cc798-281">Angenommen, Sie definieren den folgenden Controller:</span><span class="sxs-lookup"><span data-stu-id="cc798-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="cc798-282">Diese Routen werden wie folgt sortiert.</span><span class="sxs-lookup"><span data-stu-id="cc798-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="cc798-283">Bestellungen/Details</span><span class="sxs-lookup"><span data-stu-id="cc798-283">orders/details</span></span>
2. <span data-ttu-id="cc798-284">Bestellungen/ . . . . . . . . . . . . . . .</span><span class="sxs-lookup"><span data-stu-id="cc798-284">orders/{id}</span></span>
3. <span data-ttu-id="cc798-285">Bestellungen/-kundenname</span><span class="sxs-lookup"><span data-stu-id="cc798-285">orders/{customerName}</span></span>
4. <span data-ttu-id="cc798-286">Bestellungen/Datum\*</span><span class="sxs-lookup"><span data-stu-id="cc798-286">orders/{\*date}</span></span>
5. <span data-ttu-id="cc798-287">Aufträge/Ausstehende</span><span class="sxs-lookup"><span data-stu-id="cc798-287">orders/pending</span></span>

<span data-ttu-id="cc798-288">Beachten Sie, dass "Details" ein Literalsegment ist und vor dem "id" angezeigt wird, aber "ausstehend" als letzter angezeigt wird, da die **Order-Eigenschaft** 1 ist.</span><span class="sxs-lookup"><span data-stu-id="cc798-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="cc798-289">(In diesem Beispiel wird davon ausgegangen, dass keine Kunden mit den Namen "Details" oder "ausstehend" vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="cc798-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="cc798-290">Versuchen Sie im Allgemeinen, mehrdeutige Routen zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="cc798-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="cc798-291">In diesem Beispiel ist eine `GetByCustomer` bessere Routenvorlage für "customers/-customerName") .</span><span class="sxs-lookup"><span data-stu-id="cc798-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
