---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'Teil 3: Layout- und Kategoriemenü | Microsoft-Dokumentation'
author: JoeStagner
description: Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen. Teil 3 beschreibt das Hinzufügen von Layout und ein kategoriemenü.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: f55b29a271dbdb72d3e2249ed74517b77d78cf5e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034847"
---
<a name="part-3-layout-and-category-menu"></a><span data-ttu-id="95b41-104">Teil 3: Layout- und Kategoriemenü</span><span class="sxs-lookup"><span data-stu-id="95b41-104">Part 3: Layout and Category Menu</span></span>
====================
<span data-ttu-id="95b41-105">durch [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="95b41-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="95b41-106">Tailspin Spyworks wird veranschaulicht, wie außerordentlich einfach es ist, erstellen Sie leistungsstarke, skalierbare Anwendungen für die .NET-Plattform.</span><span class="sxs-lookup"><span data-stu-id="95b41-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="95b41-107">Es wird gezeigt, aus wie die hervorragenden neuen Funktionen in ASP.NET 4 zu verwenden, um eine online-Store, einschließlich der Warenkorb, Auschecken und Verwaltung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="95b41-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="95b41-108">Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen.</span><span class="sxs-lookup"><span data-stu-id="95b41-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="95b41-109">Teil 3 beschreibt das Hinzufügen von Layout und ein kategoriemenü.</span><span class="sxs-lookup"><span data-stu-id="95b41-109">Part 3 covers adding layout and a category menu.</span></span>


## <a id="_Toc260221669"></a>  <span data-ttu-id="95b41-110">Hinzufügen von einigen Layout- und eine Kategoriemenü</span><span class="sxs-lookup"><span data-stu-id="95b41-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="95b41-111">In unserem Masterseite der Website fügen wir ein DIV-Element für die Spalte der linken Seite, die unser Produkt kategoriemenü enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="95b41-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="95b41-112">Beachten Sie, dass die gewünschte Ausrichtung und sonstigen Formatierungen von CSS-Klasse bereitgestellt werden, die wir die Datei "Style.CSS" hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="95b41-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="95b41-113">Das Product Category-Menü wird dynamisch erstellt zur Laufzeit durch Abfragen der Commerce-Datenbank, für vorhandene Produktkategorien und erstellen die Menüelemente und entsprechenden links.</span><span class="sxs-lookup"><span data-stu-id="95b41-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="95b41-114">Zu diesem Zweck verwenden wir zwei von ASP zu gewährleisten. NET leistungsstarke Data-Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="95b41-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="95b41-115">Das Steuerelement "Entity Data Source" und das Steuerelement "ListView".</span><span class="sxs-lookup"><span data-stu-id="95b41-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="95b41-116">Wir wechseln Sie zu "Design View", und die Hilfsprogramme zur Konfiguration der unsere Steuerelemente verwenden.</span><span class="sxs-lookup"><span data-stu-id="95b41-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="95b41-117">Legen wir die EntityDataSource-ID-Eigenschaft für EDS\_Kategorie\_Menü, und klicken Sie auf "Datenquelle konfigurieren".</span><span class="sxs-lookup"><span data-stu-id="95b41-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="95b41-118">Wählen Sie die CommerceEntities-Verbindung, die für uns erstellt wurde, wenn wir das Entitätsdatenmodell für die Quelle für unsere Commerce-Datenbank erstellt haben, und klicken Sie auf "Weiter".</span><span class="sxs-lookup"><span data-stu-id="95b41-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="95b41-119">Wählen Sie den Namen der Entitätenmenge für "Categories", und lassen Sie die übrigen Standardeinstellungen der Optionen.</span><span class="sxs-lookup"><span data-stu-id="95b41-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="95b41-120">Klicken Sie auf "Fertig stellen".</span><span class="sxs-lookup"><span data-stu-id="95b41-120">Click "Finish".</span></span>

<span data-ttu-id="95b41-121">Jetzt legen wir die ID-Eigenschaft von der Instanz des ListView-Steuerelements, die wir auf unserer Seite aus, um die ListView platziert\_ProductsMenu und seinem Hilfsobjekt aktivieren.</span><span class="sxs-lookup"><span data-stu-id="95b41-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="95b41-122">Jedoch können wir Optionen zur aufgabensteuerung zum Formatieren der Anzeige der Daten und Formatierung, unsere im Menü erstellen, benötigen nur einfache Markup damit wir den Code in der Datenquellensicht eingeben, wird.</span><span class="sxs-lookup"><span data-stu-id="95b41-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="95b41-123">Bitte beachten Sie die Anweisung "Eval": &lt;% # Eval("CategoryName") %&gt;</span><span class="sxs-lookup"><span data-stu-id="95b41-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="95b41-124">Der ASP.NET-Syntax &lt;% # %&gt; ist eine Kurzform-Konvention, die weist die Laufzeit ausgeführt wird, was in enthalten ist, und die Ergebnisse "in Zeile".</span><span class="sxs-lookup"><span data-stu-id="95b41-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="95b41-125">Rufen Sie Eval("CategoryName") angewiesen, die für den aktuellen Eintrag in der gebundenen Auflistung von Datenelementen, den Wert der Elementnamen Entity Model "CatagoryName".</span><span class="sxs-lookup"><span data-stu-id="95b41-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CatagoryName".</span></span> <span data-ttu-id="95b41-126">Dies ist die kürzere Syntax für ein sehr leistungsfähiges Feature.</span><span class="sxs-lookup"><span data-stu-id="95b41-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="95b41-127">Können die Anwendung nun ausführen.</span><span class="sxs-lookup"><span data-stu-id="95b41-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="95b41-128">Beachten Sie, dass unser Produkt kategoriemenü wird nun angezeigt, wenn wir über eine Kategorie Menüelemente zeigen sehen wir, die im Menü Element Link verweist auf eine Seite, die wir noch implementieren müssen, mit dem Namen ProductsList.aspx und, wir ein Argument für eine dynamische Abfrage erstellt haben, enthält die  Kategorie-Id.</span><span class="sxs-lookup"><span data-stu-id="95b41-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95b41-129">[Zurück](tailspin-spyworks-part-2.md)
> [Weiter](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="95b41-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
