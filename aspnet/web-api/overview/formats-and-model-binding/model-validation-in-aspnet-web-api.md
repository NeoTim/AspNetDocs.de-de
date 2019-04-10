---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Modellvalidierung in ASP.NET Web-API – ASP.NET 4.x
author: MikeWasson
description: Übersicht über die modellvalidierung in ASP.NET Web-API für ASP.NET 4.x.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: d4e792f8cc2f79c2ab82c5a74fd50f49475fac4f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404571"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="72c68-103">Modellvalidierung in ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="72c68-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="72c68-104">durch [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="72c68-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="72c68-105">In diesem Artikel zeigt, wie Ihre Modelle kommentieren, verwenden Sie die Anmerkungen für die datenvalidierung und Behandeln von Validierungsfehlern in Ihrer Web-API wird.</span><span class="sxs-lookup"><span data-stu-id="72c68-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="72c68-106">Wenn ein Client Daten an Ihre Web-API sendet, möchten Sie häufig die Daten vor der Verarbeitung zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="72c68-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="72c68-107">Datenanmerkungen</span><span class="sxs-lookup"><span data-stu-id="72c68-107">Data Annotations</span></span>

<span data-ttu-id="72c68-108">In ASP.NET Web-API können Sie Attribute aus der [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) Namespace, um Überprüfungsregeln für Eigenschaften für Ihr Modell festgelegt.</span><span class="sxs-lookup"><span data-stu-id="72c68-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="72c68-109">Sehen Sie sich das folgende Modell an:</span><span class="sxs-lookup"><span data-stu-id="72c68-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="72c68-110">Wenn Sie die modellvalidierung in ASP.NET MVC verwendet haben, sollte das bekannt vorkommen.</span><span class="sxs-lookup"><span data-stu-id="72c68-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="72c68-111">Die **erforderlich** Attribut wird angegeben, dass die `Name` Eigenschaft darf nicht null sein.</span><span class="sxs-lookup"><span data-stu-id="72c68-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="72c68-112">Die **Bereich** Attribut wird angegeben, dass `Weight` muss zwischen 0 und 999 liegen.</span><span class="sxs-lookup"><span data-stu-id="72c68-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="72c68-113">Nehmen wir an, dass ein Client eine POST-Anforderung mit der folgenden JSON-Darstellung sendet:</span><span class="sxs-lookup"><span data-stu-id="72c68-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="72c68-114">Sie sehen, dass der Client nicht enthält die `Name` -Eigenschaft, die als markiert ist erforderlich.</span><span class="sxs-lookup"><span data-stu-id="72c68-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="72c68-115">Bei Web-API konvertiert den JSON-Code in eine `Product` Instanz überprüft die `Product` für die Validierungsattribute.</span><span class="sxs-lookup"><span data-stu-id="72c68-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="72c68-116">In Ihrem-Controlleraktion können Sie überprüfen, ob das Modell gültig ist:</span><span class="sxs-lookup"><span data-stu-id="72c68-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="72c68-117">Modellvalidierung garantiert nicht, dass der Clientdaten sicher sind.</span><span class="sxs-lookup"><span data-stu-id="72c68-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="72c68-118">Zusätzliche Überprüfung kann in anderen Ebenen der Anwendung erforderlich sein.</span><span class="sxs-lookup"><span data-stu-id="72c68-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="72c68-119">(Z. B. möglicherweise die Datenschicht foreign Key-Einschränkungen erzwingen.) Das Tutorial [mithilfe des Web-API mit Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) untersucht einige dieser Probleme.</span><span class="sxs-lookup"><span data-stu-id="72c68-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="72c68-120">**"Unterdimensionierte Posting"**: Unterdimensionierte Bereitstellung geschieht, wenn es sich bei der Client und einige Eigenschaften zu verwerfen.</span><span class="sxs-lookup"><span data-stu-id="72c68-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="72c68-121">Nehmen wir beispielsweise an, dass der Client die folgenden sendet:</span><span class="sxs-lookup"><span data-stu-id="72c68-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="72c68-122">Hier ist der Client geben keine Werte für `Price` oder `Weight`.</span><span class="sxs-lookup"><span data-stu-id="72c68-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="72c68-123">Das JSON-Formatierungsprogramm weist den Standardwert 0 (null), um die fehlenden Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="72c68-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="72c68-124">Der Modellzustand ist ungültig, da 0 (null) einen gültigen Wert für diese Eigenschaften ist.</span><span class="sxs-lookup"><span data-stu-id="72c68-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="72c68-125">Ob dieses Problem auftritt, hängt von Ihrem Szenario ab.</span><span class="sxs-lookup"><span data-stu-id="72c68-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="72c68-126">Z. B. in einem Updatevorgang sollten Sie zur Unterscheidung zwischen "Zero" und "nicht festgelegt."</span><span class="sxs-lookup"><span data-stu-id="72c68-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="72c68-127">Um Clients zum Festlegen eines Werts zu erzwingen, stellen Sie die Eigenschaft NULL-Werte zulässt, und legen die **erforderlich** Attribut:</span><span class="sxs-lookup"><span data-stu-id="72c68-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="72c68-128">**"Overposting"**: Ein Client kann auch senden *weitere* Daten als erwartet.</span><span class="sxs-lookup"><span data-stu-id="72c68-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="72c68-129">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72c68-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="72c68-130">Hier der JSON-Code enthält eine Eigenschaft ("Color"), die in nicht vorhanden ist die `Product` Modell.</span><span class="sxs-lookup"><span data-stu-id="72c68-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="72c68-131">In diesem Fall ignoriert der JSON-Formatierungsprogramm einfach diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="72c68-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="72c68-132">(Das XML-Formatierungsprogramm führt.) Overposting verursacht Probleme auf, wenn Ihr Modell über Eigenschaften, die eigentlich verfügt schreibgeschützt sein.</span><span class="sxs-lookup"><span data-stu-id="72c68-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="72c68-133">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72c68-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="72c68-134">Sollen nicht zum Aktualisieren der `IsAdmin` Eigenschaft und selbst Administratoren Berechtigungen zu erhöhen!</span><span class="sxs-lookup"><span data-stu-id="72c68-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="72c68-135">Die sicherste Strategie ist die Verwendung eine Modellklasse, die genau übereinstimmt, was der Client senden darf:</span><span class="sxs-lookup"><span data-stu-id="72c68-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="72c68-136">Brad Wilsons Blog-Beitrag "[Eingabeüberprüfung Visual Studio. Modellvalidierung in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"eine gute Beschreibung von unterdimensionierte Bereitstellung und zu viele Angaben gemacht hat.</span><span class="sxs-lookup"><span data-stu-id="72c68-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="72c68-137">Obwohl im Beitrag zu ASP.NET MVC 2 ist, sind die Probleme weiterhin relevant, die Web-API.</span><span class="sxs-lookup"><span data-stu-id="72c68-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="72c68-138">Behandeln von Validierungsfehlern</span><span class="sxs-lookup"><span data-stu-id="72c68-138">Handling Validation Errors</span></span>

<span data-ttu-id="72c68-139">Einen Fehler an den Client werden von Web-API nicht automatisch zurück, wenn die Validierung fehlschlägt.</span><span class="sxs-lookup"><span data-stu-id="72c68-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="72c68-140">Es ist Aufgabe der Controlleraktion auf den Modellzustand überprüfen und entsprechend reagieren.</span><span class="sxs-lookup"><span data-stu-id="72c68-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="72c68-141">Sie können auch erstellen, dass einen Aktionsfilter, um den Modellstatus zu überprüfen, bevor die Controlleraktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="72c68-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="72c68-142">Der folgende Code zeigt ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="72c68-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="72c68-143">Wenn die modellvalidierung fehlschlägt, gibt dieser Filter eine HTTP-Antwort, die die Validierungsfehler enthält.</span><span class="sxs-lookup"><span data-stu-id="72c68-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="72c68-144">In diesem Fall wird die Controlleraktion nicht aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="72c68-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="72c68-145">Fügen Sie zum Anwenden dieses Filters auf alle Web-API-Controller eine Instanz des Filters, der die **HttpConfiguration.Filters** Auflistung während der Konfiguration:</span><span class="sxs-lookup"><span data-stu-id="72c68-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="72c68-146">Eine weitere Option ist der Filter als Attribut individuellen Controllern oder Controlleraktionen festgelegt:</span><span class="sxs-lookup"><span data-stu-id="72c68-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
