---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Erstellen einer Routeneinschränkung (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 42c0ce5e158e2fe9387ac218ac0762b6362094f9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389570"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="6f11f-103">Erstellen einer Routeneinschränkung (C#)</span><span class="sxs-lookup"><span data-stu-id="6f11f-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="6f11f-104">durch [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6f11f-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6f11f-105">Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.</span><span class="sxs-lookup"><span data-stu-id="6f11f-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>


<span data-ttu-id="6f11f-106">Sie verwenden die routeneinschränkungen, um die Browseranforderungen zu beschränken, die eine bestimmte Route übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="6f11f-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="6f11f-107">Sie können einen regulären Ausdruck verwenden, einer routeneinschränkung an.</span><span class="sxs-lookup"><span data-stu-id="6f11f-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="6f11f-108">Angenommen Sie, dass Sie die Route in Codebeispiel 1 in der Datei "Global.asax" definiert haben.</span><span class="sxs-lookup"><span data-stu-id="6f11f-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="6f11f-109">**Codebeispiel 1 – "Global.asax.cs"**</span><span class="sxs-lookup"><span data-stu-id="6f11f-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="6f11f-110">Codebeispiel 1 enthält eine Route mit dem Namen Product.</span><span class="sxs-lookup"><span data-stu-id="6f11f-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="6f11f-111">Sie können die Produkt-Route verwenden, Browseranforderungen ProductController in Listing 2 enthaltenen zuordnen.</span><span class="sxs-lookup"><span data-stu-id="6f11f-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="6f11f-112">**Codebeispiel 2 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="6f11f-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="6f11f-113">Beachten Sie, dass die Details()-Aktion, die von der Produkt-Controller verfügbar gemacht werden, einen einzelnen Parameter mit dem Namen "ProductID" akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="6f11f-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="6f11f-114">Dieser Parameter ist ein Integer-Parameter.</span><span class="sxs-lookup"><span data-stu-id="6f11f-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="6f11f-115">Die Route definiert, die in Codebeispiel 1 wird eine der folgenden URLs übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="6f11f-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="6f11f-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="6f11f-116">/Product/23</span></span>
- <span data-ttu-id="6f11f-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="6f11f-117">/Product/7</span></span>

<span data-ttu-id="6f11f-118">Leider wird die Route auch die folgenden URLs übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="6f11f-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="6f11f-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="6f11f-119">/Product/blah</span></span>
- <span data-ttu-id="6f11f-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="6f11f-120">/Product/apple</span></span>

<span data-ttu-id="6f11f-121">Da die Details() Aktion einen ganzzahligen Parameter erwartet, verursacht der eine Anforderung, die etwas anderes als ein ganzzahliger Wert enthält einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="6f11f-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="6f11f-122">Z. B. Wenn Sie die URL-/Product/apple in Ihren Browser eingeben erhalten die Fehlerseite in Abbildung 1 Sie.</span><span class="sxs-lookup"><span data-stu-id="6f11f-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>


<span data-ttu-id="6f11f-123">[![Das Dialogfeld "Neues Projekt"](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f11f-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f11f-124">**Abbildung 01**: Eine Seite explode angezeigt ([klicken Sie, um das Bild in voller Größe anzeigen](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6f11f-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>


<span data-ttu-id="6f11f-125">Was Sie wirklich tun werden nur auf URLs überein, die eine richtige ganze Zahl "ProductID" enthalten.</span><span class="sxs-lookup"><span data-stu-id="6f11f-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="6f11f-126">Eine Einschränkung können beim Definieren einer Route zum Einschränken der URLs, die mit die Route übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="6f11f-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="6f11f-127">Die geänderte Produkt Route in Programmausdruck 3 enthält eine reguläre-Einschränkung, die nur Ganzzahlen entspricht.</span><span class="sxs-lookup"><span data-stu-id="6f11f-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="6f11f-128">**Codebeispiel 3: "Global.asax.cs"**</span><span class="sxs-lookup"><span data-stu-id="6f11f-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="6f11f-129">Der reguläre Ausdruck \d+ entspricht eine oder mehrere Ganzzahlen.</span><span class="sxs-lookup"><span data-stu-id="6f11f-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="6f11f-130">Diese Einschränkung bewirkt, dass die Product-Route mit den folgenden URLs übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="6f11f-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="6f11f-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="6f11f-131">/Product/3</span></span>
- <span data-ttu-id="6f11f-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="6f11f-132">/Product/8999</span></span>

<span data-ttu-id="6f11f-133">Aber nicht die folgenden URLs:</span><span class="sxs-lookup"><span data-stu-id="6f11f-133">But not the following URLs:</span></span>

- <span data-ttu-id="6f11f-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="6f11f-134">/Product/apple</span></span>
- <span data-ttu-id="6f11f-135">/Product</span><span class="sxs-lookup"><span data-stu-id="6f11f-135">/Product</span></span>

- <span data-ttu-id="6f11f-136">Diese Browseranforderungen von einer anderen Route verarbeitet werden oder, wenn es keine übereinstimmenden Routen sind, eine *die Ressource konnte nicht gefunden werden* Fehler zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="6f11f-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f11f-137">[Zurück](creating-custom-routes-cs.md)
> [Weiter](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6f11f-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
