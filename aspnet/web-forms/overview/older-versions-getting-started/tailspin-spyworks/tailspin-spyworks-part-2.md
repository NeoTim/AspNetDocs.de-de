---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Teil 2: Data Access Layer | Microsoft-Dokumentation'
author: JoeStagner
description: Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen. Teil 2 umfasst das Hinzufügen der Datenzugriffsschicht.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378387"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="5bf34-104">Teil 2: Datenzugriffsebene</span><span class="sxs-lookup"><span data-stu-id="5bf34-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="5bf34-105">durch [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="5bf34-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="5bf34-106">Tailspin Spyworks wird veranschaulicht, wie außerordentlich einfach es ist, erstellen Sie leistungsstarke, skalierbare Anwendungen für die .NET-Plattform.</span><span class="sxs-lookup"><span data-stu-id="5bf34-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="5bf34-107">Es wird gezeigt, aus wie die hervorragenden neuen Funktionen in ASP.NET 4 zu verwenden, um eine online-Store, einschließlich der Warenkorb, Auschecken und Verwaltung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5bf34-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="5bf34-108">Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen.</span><span class="sxs-lookup"><span data-stu-id="5bf34-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="5bf34-109">Teil 2 umfasst das Hinzufügen der Datenzugriffsschicht.</span><span class="sxs-lookup"><span data-stu-id="5bf34-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="5bf34-110">Hinzufügen der Datenzugriffsschicht</span><span class="sxs-lookup"><span data-stu-id="5bf34-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="5bf34-111">Die e-Commerce-Anwendung hängt von zwei Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="5bf34-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="5bf34-112">Für Informationen zu den Kunden verwenden wir die ASP.NET-Mitgliedschaft-Standarddatenbank.</span><span class="sxs-lookup"><span data-stu-id="5bf34-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="5bf34-113">Für unseren shopping Cart "und" Produkt-Katalog werden wir eine SQL Express-Datenbank wie folgt implementieren.</span><span class="sxs-lookup"><span data-stu-id="5bf34-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="5bf34-114">Erstellen der Datenbank (Commerce.mdf) in der Anwendung App\_Datenordner wir fortfahren können, um unsere Data Access Layer, die mithilfe von .NET Entity Framework zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5bf34-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="5bf34-115">Wir erstellen einen Ordner namens "Data\_Zugriff", und klicken Sie mit der rechten Maustaste auf diesen Ordner und wählen Sie "Neues Element hinzufügen".</span><span class="sxs-lookup"><span data-stu-id="5bf34-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="5bf34-116">Geben Sie unter "Installierte Vorlagen" Item "und" und wählen Sie dann "ADO.NET Entity Data Model" EDM\_Commerce.edmx als den Namen, und klicken Sie auf die Schaltfläche "Hinzufügen".</span><span class="sxs-lookup"><span data-stu-id="5bf34-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="5bf34-117">Wählen Sie "Aus Datenbank generieren".</span><span class="sxs-lookup"><span data-stu-id="5bf34-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="5bf34-118">Speichern und erstellen.</span><span class="sxs-lookup"><span data-stu-id="5bf34-118">Save and build.</span></span>

<span data-ttu-id="5bf34-119">Jetzt können wir unsere erste Feature – eines Product Category-Menüs hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5bf34-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5bf34-120">[Zurück](tailspin-spyworks-part-1.md)
> [Weiter](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="5bf34-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
