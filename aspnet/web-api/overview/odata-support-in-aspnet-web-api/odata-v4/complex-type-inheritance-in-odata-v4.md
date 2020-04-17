---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Komplexe Typvererbung in OData v4 mit ASP.NET Web-API | Microsoft Docs
author: rick-anderson
description: Gemäß der OData v4-Spezifikation kann ein komplexer Typ von einem anderen komplexen Typ erben. (Ein komplexer Typ ist ein strukturierter Typ ohne Schlüssel.) Web-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543599"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="fb802-104">Komplexe Typvererbung in OData v4 mit ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="fb802-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="fb802-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fb802-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fb802-106">Gemäß der OData [v4-Spezifikation](http://www.odata.org/documentation/odata-version-4-0/)kann ein komplexer Typ von einem anderen komplexen Typ erben.</span><span class="sxs-lookup"><span data-stu-id="fb802-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="fb802-107">(Ein *komplexer* Typ ist ein strukturierter Typ ohne Schlüssel.) Web-API OData 5.3 unterstützt komplexe Typvererbung.</span><span class="sxs-lookup"><span data-stu-id="fb802-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="fb802-108">In diesem Thema wird gezeigt, wie ein Entitätsdatenmodell (Entity Data Model, EDM) mit komplexen Vererbungstypen erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="fb802-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="fb802-109">Den vollständigen Quellcode finden Sie unter [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="fb802-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fb802-110">Im Tutorial verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="fb802-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fb802-111">Web-API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="fb802-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="fb802-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="fb802-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="fb802-113">Modellhierarchie</span><span class="sxs-lookup"><span data-stu-id="fb802-113">Model Hierarchy</span></span>

<span data-ttu-id="fb802-114">Zur Veranschaulichung der komplexen Typvererbung verwenden wir die folgende Klassenhierarchie.</span><span class="sxs-lookup"><span data-stu-id="fb802-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="fb802-115">`Shape`ist ein abstrakter komplexer Typ.</span><span class="sxs-lookup"><span data-stu-id="fb802-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="fb802-116">`Rectangle`, `Triangle`und `Circle` sind komplexe `Shape`Typen, `RoundRectangle` die von `Rectangle`abgeleitet sind und von abgeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="fb802-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="fb802-117">`Window`ist ein Entitätstyp `Shape` und enthält eine Instanz.</span><span class="sxs-lookup"><span data-stu-id="fb802-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="fb802-118">Hier sind die CLR-Klassen, die diese Typen definieren.</span><span class="sxs-lookup"><span data-stu-id="fb802-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="fb802-119">Erstellen des EDM-Modells</span><span class="sxs-lookup"><span data-stu-id="fb802-119">Build the EDM Model</span></span>

<span data-ttu-id="fb802-120">Zum Erstellen des EDM können Sie **ODataConventionModelBuilder**verwenden, das die Vererbungsbeziehungen aus den CLR-Typen ableitet.</span><span class="sxs-lookup"><span data-stu-id="fb802-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="fb802-121">Sie können das EDM auch explizit mit **ODataModelBuilder**erstellen.</span><span class="sxs-lookup"><span data-stu-id="fb802-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="fb802-122">Dies erfordert mehr Code, gibt Ihnen aber mehr Kontrolle über das EDM.</span><span class="sxs-lookup"><span data-stu-id="fb802-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="fb802-123">In diesen beiden Beispielen wird dasselbe EDM-Schema erstellt.</span><span class="sxs-lookup"><span data-stu-id="fb802-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="fb802-124">Metadatendokument</span><span class="sxs-lookup"><span data-stu-id="fb802-124">Metadata Document</span></span>

<span data-ttu-id="fb802-125">Hier ist das OData-Metadatendokument, das die Vererbung komplexer Typen anzeigt.</span><span class="sxs-lookup"><span data-stu-id="fb802-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="fb802-126">Aus dem Metadatendokument können Sie sehen, dass:</span><span class="sxs-lookup"><span data-stu-id="fb802-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="fb802-127">Der `Shape` komplexe Typ ist abstrakt.</span><span class="sxs-lookup"><span data-stu-id="fb802-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="fb802-128">Der `Rectangle` `Triangle`,- `Circle` und der komplexe `Shape`Typ haben den Basistyp .</span><span class="sxs-lookup"><span data-stu-id="fb802-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="fb802-129">Der `RoundRectangle` Typ hat `Rectangle`den Basistyp .</span><span class="sxs-lookup"><span data-stu-id="fb802-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="fb802-130">Casting Complex-Typen</span><span class="sxs-lookup"><span data-stu-id="fb802-130">Casting Complex Types</span></span>

<span data-ttu-id="fb802-131">Das Casting für komplexe Typen wird jetzt unterstützt.</span><span class="sxs-lookup"><span data-stu-id="fb802-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="fb802-132">Die folgende Abfrage gibt z. B. eine `Shape` in eine `Rectangle`aus.</span><span class="sxs-lookup"><span data-stu-id="fb802-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="fb802-133">Hier ist die Antwort Nutzlast:</span><span class="sxs-lookup"><span data-stu-id="fb802-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
