---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Erstellen benutzerdefinierter Routen | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen. In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542754"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="fd31c-104">Erstellen von benutzerdefinierten Routen (C#)</span><span class="sxs-lookup"><span data-stu-id="fd31c-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="fd31c-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fd31c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fd31c-106">Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="fd31c-107">In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.</span><span class="sxs-lookup"><span data-stu-id="fd31c-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="fd31c-108">In diesem Tutorial erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung eine benutzerdefinierte Route hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="fd31c-109">Sie erfahren, wie Sie die Standardroutentabelle in der Datei Global.asax mit einer benutzerdefinierten Route ändern.</span><span class="sxs-lookup"><span data-stu-id="fd31c-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="fd31c-110">Bei vielen einfachen ASP.NET MVC-Anwendungen funktioniert die Standardroutentabelle einwandfrei.</span><span class="sxs-lookup"><span data-stu-id="fd31c-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="fd31c-111">Möglicherweise stellen Sie jedoch fest, dass Sie spezielle Routinganforderungen haben.</span><span class="sxs-lookup"><span data-stu-id="fd31c-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="fd31c-112">In diesem Fall können Sie eine benutzerdefinierte Route erstellen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="fd31c-113">Stellen Sie sich beispielsweise vor, dass Sie eine Bloganwendung erstellen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="fd31c-114">Sie können eingehende Anforderungen verarbeiten, die wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fd31c-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="fd31c-115">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="fd31c-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="fd31c-116">Wenn ein Benutzer diese Anforderung eingibt, möchten Sie den Blogeintrag zurückgeben, der dem Datum 25.12.2009 entspricht.</span><span class="sxs-lookup"><span data-stu-id="fd31c-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="fd31c-117">Um diesen Anforderungstyp zu verarbeiten, müssen Sie eine benutzerdefinierte Route erstellen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="fd31c-118">Die Datei Global.asax in Listing 1 enthält eine neue benutzerdefinierte Route mit dem Namen Blog, die Anforderungen verarbeitet, die wie /Archive/*Eintragsdatum*aussehen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="fd31c-119">**Auflistung 1 - Global.asax (mit benutzerdefinierter Route)**</span><span class="sxs-lookup"><span data-stu-id="fd31c-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="fd31c-120">Die Reihenfolge der Routen, die Sie der Routentabelle hinzufügen, ist wichtig.</span><span class="sxs-lookup"><span data-stu-id="fd31c-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="fd31c-121">Unsere neue benutzerdefinierte Blogroute wird vor der vorhandenen Standardroute hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="fd31c-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="fd31c-122">Wenn Sie die Bestellung umgekehrt haben, wird die Standardroute immer anstelle der benutzerdefinierten Route aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="fd31c-123">Die benutzerdefinierte Blogroute entspricht jeder Anforderung, die mit /Archive/ beginnt.</span><span class="sxs-lookup"><span data-stu-id="fd31c-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="fd31c-124">Es entspricht also allen folgenden URLs:</span><span class="sxs-lookup"><span data-stu-id="fd31c-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="fd31c-125">/Archiv/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="fd31c-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="fd31c-126">/Archiv/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="fd31c-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="fd31c-127">/Archiv/Apfel</span><span class="sxs-lookup"><span data-stu-id="fd31c-127">/Archive/apple</span></span>

<span data-ttu-id="fd31c-128">Die benutzerdefinierte Route ordnet die eingehende Anforderung einem Controller mit dem Namen Archiv zu und ruft die Aktion Entry() auf.</span><span class="sxs-lookup"><span data-stu-id="fd31c-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="fd31c-129">Wenn die Entry()-Methode aufgerufen wird, wird das Eintragsdatum als Parameter namens entryDate übergeben.</span><span class="sxs-lookup"><span data-stu-id="fd31c-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="fd31c-130">Sie können die benutzerdefinierte Blog-Route mit dem Controller in Liste 2 verwenden.</span><span class="sxs-lookup"><span data-stu-id="fd31c-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="fd31c-131">**Inserat 2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="fd31c-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="fd31c-132">Beachten Sie, dass die Entry()-Methode in Listing 2 einen Parameter vom Typ DateTime akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="fd31c-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="fd31c-133">Das MVC-Framework ist intelligent genug, um das Eintragsdatum von der URL automatisch in einen DateTime-Wert zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="fd31c-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="fd31c-134">Wenn der Parameter für das Eintragsdatum aus der URL nicht in eine DateTime konvertiert werden kann, wird ein Fehler ausgelöst (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="fd31c-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="fd31c-135">**Abbildung 1: Fehler beim Konvertieren des Parameters**</span><span class="sxs-lookup"><span data-stu-id="fd31c-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="fd31c-136">[![Dialogfeld „New Project“ (Neues Projekt)](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fd31c-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="fd31c-137">**Abbildung 01**: Fehler beim Konvertieren des Parameters ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fd31c-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="fd31c-138">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="fd31c-138">Summary</span></span>

<span data-ttu-id="fd31c-139">Das Ziel dieses Tutorials war es, zu demonstrieren, wie Sie eine benutzerdefinierte Route erstellen können.</span><span class="sxs-lookup"><span data-stu-id="fd31c-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="fd31c-140">Sie haben gelernt, wie Sie der Routingtabelle in der Datei Global.asax, die Blogeinträge darstellt, eine benutzerdefinierte Route hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd31c-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="fd31c-141">Wir haben erläutert, wie Anforderungen für Blogeinträge einem Controller mit dem Namen ArchiveController und einer Controlleraktion namens Entry() zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="fd31c-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fd31c-142">[Zurück](aspnet-mvc-controllers-overview-cs.md)
> [Weiter](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fd31c-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
