---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Öffnen von Typen in OData v4 mit ASP.NET Web-API | Microsoft Docs
author: rick-anderson
description: In OData v4 ist ein offener Typ ein strukturierter Typ, der dynamische Eigenschaften enthält, zusätzlich zu allen Eigenschaften, die in der Typdefinition deklariert werden. Öffnen...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543729"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="fe741-104">Öffnen von Typen in OData v4 mit ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="fe741-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="fe741-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fe741-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fe741-106">In OData v4 ist ein *offener Typ* ein strukturierter Typ, der dynamische Eigenschaften enthält, zusätzlich zu allen Eigenschaften, die in der Typdefinition deklariert werden.</span><span class="sxs-lookup"><span data-stu-id="fe741-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="fe741-107">Mit offenen Typen können Sie Ihren Datenmodellen Flexibilität verleihen.</span><span class="sxs-lookup"><span data-stu-id="fe741-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="fe741-108">In diesem Tutorial wird gezeigt, wie Sie offene Typen in ASP.NET Web-API OData verwenden.</span><span class="sxs-lookup"><span data-stu-id="fe741-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="fe741-109">In diesem Tutorial wird davon ausgegangen, dass Sie bereits wissen, wie Sie einen OData-Endpunkt in ASP.NET Web-API erstellen.</span><span class="sxs-lookup"><span data-stu-id="fe741-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="fe741-110">Wenn dies nicht der Fall ist, lesen Sie zuerst [Einen OData v4-Endpunkt](create-an-odata-v4-endpoint.md) erstellen.</span><span class="sxs-lookup"><span data-stu-id="fe741-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fe741-111">Im Tutorial verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="fe741-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fe741-112">Web-API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="fe741-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="fe741-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="fe741-113">OData v4</span></span>

<span data-ttu-id="fe741-114">Zunächst einige OData-Terminologie:</span><span class="sxs-lookup"><span data-stu-id="fe741-114">First, some OData terminology:</span></span>

- <span data-ttu-id="fe741-115">Entitätstyp: Ein strukturierter Typ mit einem Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="fe741-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="fe741-116">Komplexer Typ: Ein strukturierter Typ ohne Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="fe741-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="fe741-117">Offener Typ: Ein Typ mit dynamischen Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="fe741-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="fe741-118">Sowohl Entitätstypen als auch komplexe Typen können geöffnet sein.</span><span class="sxs-lookup"><span data-stu-id="fe741-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="fe741-119">Der Wert einer dynamischen Eigenschaft kann ein primitiver Typ, ein komplexer Typ oder ein Enumerationstyp sein. oder eine Sammlung dieser Typen.</span><span class="sxs-lookup"><span data-stu-id="fe741-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="fe741-120">Weitere Informationen zu geöffneten Typen finden Sie in der [OData v4-Spezifikation](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="fe741-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="fe741-121">Installieren der Web-OData-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="fe741-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="fe741-122">Verwenden Sie NuGet Package Manager, um die neuesten Web-API-OData-Bibliotheken zu installieren.</span><span class="sxs-lookup"><span data-stu-id="fe741-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="fe741-123">Aus dem Fenster Paket-Manager-Konsole:</span><span class="sxs-lookup"><span data-stu-id="fe741-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="fe741-124">Definieren der CLR-Typen</span><span class="sxs-lookup"><span data-stu-id="fe741-124">Define the CLR Types</span></span>

<span data-ttu-id="fe741-125">Definieren Sie zunächst die EDM-Modelle als CLR-Typen.</span><span class="sxs-lookup"><span data-stu-id="fe741-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="fe741-126">Wenn das Entity Data Model (EDM) erstellt wird,</span><span class="sxs-lookup"><span data-stu-id="fe741-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="fe741-127">`Category`ist ein Enumerationstyp.</span><span class="sxs-lookup"><span data-stu-id="fe741-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="fe741-128">`Address`ist ein komplexer Typ.</span><span class="sxs-lookup"><span data-stu-id="fe741-128">`Address` is a complex type.</span></span> <span data-ttu-id="fe741-129">(Es hat keinen Schlüssel, daher ist es kein Entitätstyp.)</span><span class="sxs-lookup"><span data-stu-id="fe741-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="fe741-130">`Customer`ist ein Entitätstyp.</span><span class="sxs-lookup"><span data-stu-id="fe741-130">`Customer` is an entity type.</span></span> <span data-ttu-id="fe741-131">(Es hat einen Schlüssel.)</span><span class="sxs-lookup"><span data-stu-id="fe741-131">(It has a key.)</span></span>
- <span data-ttu-id="fe741-132">`Press`ist ein offener komplexer Typ.</span><span class="sxs-lookup"><span data-stu-id="fe741-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="fe741-133">`Book`ist ein offener Entitätstyp.</span><span class="sxs-lookup"><span data-stu-id="fe741-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="fe741-134">Um einen offenen Typ zu erstellen, muss der `IDictionary<string, object>`CLR-Typ über eine Eigenschaft vom Typ verfügen, die die dynamischen Eigenschaften enthält.</span><span class="sxs-lookup"><span data-stu-id="fe741-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="fe741-135">Erstellen des EDM-Modells</span><span class="sxs-lookup"><span data-stu-id="fe741-135">Build the EDM Model</span></span>

<span data-ttu-id="fe741-136">Wenn Sie **ODataConventionModelBuilder** zum Erstellen `Press` des `Book` EDM verwenden und automatisch als offene `IDictionary<string, object>` Typen hinzugefügt werden, basierend auf dem Vorhandensein einer Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fe741-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="fe741-137">Sie können das EDM auch explizit mit **ODataModelBuilder**erstellen.</span><span class="sxs-lookup"><span data-stu-id="fe741-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="fe741-138">Hinzufügen eines OData Controllers</span><span class="sxs-lookup"><span data-stu-id="fe741-138">Add an OData Controller</span></span>

<span data-ttu-id="fe741-139">Fügen Sie als Nächstes einen OData-Controller hinzu.</span><span class="sxs-lookup"><span data-stu-id="fe741-139">Next, add an OData controller.</span></span> <span data-ttu-id="fe741-140">In diesem Tutorial verwenden wir einen vereinfachten Controller, der nur GET- und POST-Anforderungen unterstützt und eine In-Memory-Liste zum Speichern von Entitäten verwendet.</span><span class="sxs-lookup"><span data-stu-id="fe741-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="fe741-141">Beachten Sie, `Book` dass die erste Instanz keine dynamischen Eigenschaften aufweist.</span><span class="sxs-lookup"><span data-stu-id="fe741-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="fe741-142">Die `Book` zweite Instanz verfügt über die folgenden dynamischen Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="fe741-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="fe741-143">"Veröffentlicht": Primitiver Typ</span><span class="sxs-lookup"><span data-stu-id="fe741-143">"Published": Primitive type</span></span>
- <span data-ttu-id="fe741-144">"Autoren": Sammlung primitiver Typen</span><span class="sxs-lookup"><span data-stu-id="fe741-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="fe741-145">"Andere Kategorien": Auflistung von Enumerationstypen.</span><span class="sxs-lookup"><span data-stu-id="fe741-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="fe741-146">Außerdem verfügt `Press` die `Book` Eigenschaft dieser Instanz über die folgenden dynamischen Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="fe741-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="fe741-147">"Blog": Primitiver Typ</span><span class="sxs-lookup"><span data-stu-id="fe741-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="fe741-148">"Adresse": Komplexer Typ</span><span class="sxs-lookup"><span data-stu-id="fe741-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="fe741-149">Abfragen der Metadaten</span><span class="sxs-lookup"><span data-stu-id="fe741-149">Query the Metadata</span></span>

<span data-ttu-id="fe741-150">Um das OData-Metadatendokument abzurufen, `~/$metadata`senden Sie eine GET-Anforderung an .</span><span class="sxs-lookup"><span data-stu-id="fe741-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="fe741-151">Das Antwortgremium sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fe741-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="fe741-152">Aus dem Metadatendokument können Sie sehen, dass:</span><span class="sxs-lookup"><span data-stu-id="fe741-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="fe741-153">Für `Book` die `Press` und-Typen ist `OpenType` der Wert des Attributs true.</span><span class="sxs-lookup"><span data-stu-id="fe741-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="fe741-154">Die `Customer` `Address` und-Typen haben dieses Attribut nicht.</span><span class="sxs-lookup"><span data-stu-id="fe741-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="fe741-155">Der `Book` Entitätstyp hat drei deklarierte Eigenschaften: ISBN, Title und Press.</span><span class="sxs-lookup"><span data-stu-id="fe741-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="fe741-156">Die OData-Metadaten enthalten `Book.Properties` nicht die Eigenschaft aus der CLR-Klasse.</span><span class="sxs-lookup"><span data-stu-id="fe741-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="fe741-157">Ebenso hat `Press` der komplexe Typ nur zwei deklarierte Eigenschaften: Name und Kategorie.</span><span class="sxs-lookup"><span data-stu-id="fe741-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="fe741-158">Die Metadaten enthalten `Press.DynamicProperties` nicht die Eigenschaft aus der CLR-Klasse.</span><span class="sxs-lookup"><span data-stu-id="fe741-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="fe741-159">Abfragen einer Entität</span><span class="sxs-lookup"><span data-stu-id="fe741-159">Query an Entity</span></span>

<span data-ttu-id="fe741-160">Um das Buch mit ISBN gleich "978-0-7356-7942-9" `~/Books('978-0-7356-7942-9')`zu erhalten, senden Sie eine GET-Anfrage an .</span><span class="sxs-lookup"><span data-stu-id="fe741-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="fe741-161">Das Antwortgremium sollte wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="fe741-161">The response body should look similar to the following.</span></span> <span data-ttu-id="fe741-162">(Eingerückt, um es lesbarer zu machen.)</span><span class="sxs-lookup"><span data-stu-id="fe741-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="fe741-163">Beachten Sie, dass die dynamischen Eigenschaften inline mit den deklarierten Eigenschaften enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="fe741-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="fe741-164">POST einer Entität</span><span class="sxs-lookup"><span data-stu-id="fe741-164">POST an Entity</span></span>

<span data-ttu-id="fe741-165">Um eine Book-Entität hinzuzufügen, `~/Books`senden Sie eine POST-Anforderung an .</span><span class="sxs-lookup"><span data-stu-id="fe741-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="fe741-166">Der Client kann dynamische Eigenschaften in der Anforderungsnutzlast festlegen.</span><span class="sxs-lookup"><span data-stu-id="fe741-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="fe741-167">Hier ist eine Beispielanforderung.</span><span class="sxs-lookup"><span data-stu-id="fe741-167">Here is an example request.</span></span> <span data-ttu-id="fe741-168">Beachten Sie die Eigenschaften "Preis" und "Veröffentlicht".</span><span class="sxs-lookup"><span data-stu-id="fe741-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="fe741-169">Wenn Sie einen Haltepunkt in der Controllermethode festlegen, können Sie `Properties` sehen, dass die Web-API diese Eigenschaften dem Wörterbuch hinzugefügt hat.</span><span class="sxs-lookup"><span data-stu-id="fe741-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="fe741-170">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fe741-170">Additional Resources</span></span>

[<span data-ttu-id="fe741-171">OData Open Type-Beispiel</span><span class="sxs-lookup"><span data-stu-id="fe741-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
