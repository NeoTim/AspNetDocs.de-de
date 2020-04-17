---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Erstellen von benutzerdefinierten Routen (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen. In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542741"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="9f8d3-104">Erstellen von benutzerdefinierten Routen (VB)</span><span class="sxs-lookup"><span data-stu-id="9f8d3-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="9f8d3-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9f8d3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9f8d3-106">Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="9f8d3-107">In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="9f8d3-108">In diesem Tutorial erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung eine benutzerdefinierte Route hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="9f8d3-109">Sie erfahren, wie Sie die Standardroutentabelle in der Datei Global.asax mit einer benutzerdefinierten Route ändern.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="9f8d3-110">In ASP.NET MVC-Anwendungen funktioniert die Standardroutentabelle einwandfrei.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="9f8d3-111">Möglicherweise stellen Sie jedoch fest, dass Sie spezielle Routinganforderungen haben.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="9f8d3-112">In diesem Fall können Sie eine benutzerdefinierte Route erstellen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="9f8d3-113">Stellen Sie sich beispielsweise vor, dass Sie eine Bloganwendung erstellen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="9f8d3-114">Sie können eingehende Anforderungen verarbeiten, die wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="9f8d3-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="9f8d3-115">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="9f8d3-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="9f8d3-116">Wenn ein Benutzer diese Anforderung eingibt, möchten Sie den Blogeintrag zurückgeben, der dem Datum 25.12.2009 entspricht.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="9f8d3-117">Um diesen Anforderungstyp zu verarbeiten, müssen Sie eine benutzerdefinierte Route erstellen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="9f8d3-118">Die Datei Global.asax in Listing 1 enthält eine neue benutzerdefinierte Route mit dem Namen Blog, die Anforderungen verarbeitet, die wie /Archive/*Eintragsdatum*aussehen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="9f8d3-119">**Auflistung 1 - Global.asax (mit benutzerdefinierter Route)**</span><span class="sxs-lookup"><span data-stu-id="9f8d3-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="9f8d3-120">Die Reihenfolge der Routen, die Sie der Routentabelle hinzufügen, ist wichtig.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="9f8d3-121">Unsere neue benutzerdefinierte Blogroute wird vor der vorhandenen Standardroute hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="9f8d3-122">Wenn Sie die Bestellung umgekehrt haben, wird die Standardroute immer anstelle der benutzerdefinierten Route aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="9f8d3-123">Die benutzerdefinierte Blogroute entspricht jeder Anforderung, die mit /Archive/ beginnt.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="9f8d3-124">Es entspricht also allen folgenden URLs:</span><span class="sxs-lookup"><span data-stu-id="9f8d3-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="9f8d3-125">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="9f8d3-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="9f8d3-126">/Archiv/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="9f8d3-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="9f8d3-127">/Archiv/Apfel</span><span class="sxs-lookup"><span data-stu-id="9f8d3-127">/Archive/apple</span></span>

<span data-ttu-id="9f8d3-128">Die benutzerdefinierte Route ordnet die eingehende Anforderung einem Controller mit dem Namen Archiv zu und ruft die Aktion Entry() auf.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="9f8d3-129">Wenn die Entry()-Methode aufgerufen wird, wird das Eintragsdatum als Parameter namens entryDate übergeben.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="9f8d3-130">Sie können die benutzerdefinierte Blog-Route mit dem Controller in Liste 2 verwenden.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="9f8d3-131">**Eintrag 2 - ArchiveController.vb**</span><span class="sxs-lookup"><span data-stu-id="9f8d3-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="9f8d3-132">Beachten Sie, dass die Entry()-Methode in Listing 2 einen Parameter vom Typ DateTime akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="9f8d3-133">Das MVC-Framework ist intelligent genug, um das Eintragsdatum von der URL automatisch in einen DateTime-Wert zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="9f8d3-134">Wenn der Parameter für das Eintragsdatum aus der URL nicht in eine DateTime konvertiert werden kann, wird ein Fehler ausgelöst (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="9f8d3-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="9f8d3-135">**Abbildung 1: Fehler beim Konvertieren des Parameters**</span><span class="sxs-lookup"><span data-stu-id="9f8d3-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="9f8d3-136">[![Dialogfeld „New Project“ (Neues Projekt)](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9f8d3-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="9f8d3-137">**Abbildung 01**: Fehler beim Konvertieren des Parameters ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9f8d3-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="9f8d3-138">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9f8d3-138">Summary</span></span>

<span data-ttu-id="9f8d3-139">Das Ziel dieses Tutorials war es, zu demonstrieren, wie Sie eine benutzerdefinierte Route erstellen können.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="9f8d3-140">Sie haben gelernt, wie Sie der Routingtabelle in der Datei Global.asax, die Blogeinträge darstellt, eine benutzerdefinierte Route hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="9f8d3-141">Wir haben erläutert, wie Anforderungen für Blogeinträge einem Controller mit dem Namen ArchiveController und einer Controlleraktion namens Entry() zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="9f8d3-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9f8d3-142">[Zurück](asp-net-mvc-controller-overview-vb.md)
> [Weiter](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9f8d3-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
