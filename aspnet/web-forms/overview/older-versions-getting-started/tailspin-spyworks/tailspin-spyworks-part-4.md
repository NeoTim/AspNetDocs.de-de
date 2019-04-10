---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 'Teil 4: Auflisten von Produkten | Microsoft-Dokumentation'
author: JoeStagner
description: Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen. Teil 4 enthält die Auflistung von Produkten mit der GridView-Vertr....
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 63afd25e2ccf22d3c7ae5c5048c80a8cf060d4cf
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382822"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="658d2-104">Teil 4: Auflisten von Produkten</span><span class="sxs-lookup"><span data-stu-id="658d2-104">Part 4: Listing Products</span></span>

<span data-ttu-id="658d2-105">durch [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="658d2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="658d2-106">Tailspin Spyworks wird veranschaulicht, wie außerordentlich einfach es ist, erstellen Sie leistungsstarke, skalierbare Anwendungen für die .NET-Plattform.</span><span class="sxs-lookup"><span data-stu-id="658d2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="658d2-107">Es wird gezeigt, aus wie die hervorragenden neuen Funktionen in ASP.NET 4 zu verwenden, um eine online-Store, einschließlich der Warenkorb, Auschecken und Verwaltung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="658d2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="658d2-108">Dieser tutorialreihe werden alle Schritte ausgeführt, um die beispielanwendung Tailspin Spyworks erstellen.</span><span class="sxs-lookup"><span data-stu-id="658d2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="658d2-109">Teil 4 enthält die Auflistung von Produkten mit GridView-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="658d2-109">Part 4 covers listing products with the GridView control.</span></span>


## <a id="_Toc260221670"></a>  <span data-ttu-id="658d2-110">Auflistung von Produkten mit GridView-Steuerelement</span><span class="sxs-lookup"><span data-stu-id="658d2-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="658d2-111">Auf unserer Lösung und dann "Hinzufügen" und "Neues Element" Implementieren von unserer Seite ProductsList.aspx "Rechten Maustaste auf den" beginnen.</span><span class="sxs-lookup"><span data-stu-id="658d2-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="658d2-112">Wählen Sie "Web Form mithilfe von Masterseite", und geben Sie einen Seitennamen ProductsList.aspx".</span><span class="sxs-lookup"><span data-stu-id="658d2-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="658d2-113">Klicken Sie auf "Hinzufügen".</span><span class="sxs-lookup"><span data-stu-id="658d2-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="658d2-114">Als nächstes wählen Sie den "Stile"-Ordner, in dem wir die Site.Master-Seite platziert, und wählen Sie ihn in das Fenster "Inhalt des Ordners".</span><span class="sxs-lookup"><span data-stu-id="658d2-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="658d2-115">Klicken Sie auf "Ok", um die Seite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="658d2-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="658d2-116">Unsere Datenbank wird mit Produktdaten aufgefüllt, wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="658d2-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="658d2-117">Nach der Erstellung unserer Seite verwenden wir erneut eine Datenquelle für die Entität auf die Produktdaten zugreifen, aber in diesem Fall müssen wir die Product-Entitäten auswählen, und wir müssen die Elemente einzuschränken, um nur die für die ausgewählte Kategorie zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="658d2-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="658d2-118">Um dies zu erreichen wir verraten EntityDataSource zum automatischen Generieren der WHERE-Klausel aus, und wir legen die WhereParameter.</span><span class="sxs-lookup"><span data-stu-id="658d2-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="658d2-119">Sie erinnern sich, dass beim Erstellen der Menüelemente in unsere "Product Category-Menü" Wir dynamisch die Verknüpfung erstellt die Abfragezeichenfolge für jeden Link die CategoryID hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="658d2-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="658d2-120">Es informiert, dass der Entity-Datenquelle, QueryString-Parameter den WHERE-Parameter abgeleitet.</span><span class="sxs-lookup"><span data-stu-id="658d2-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="658d2-121">Als Nächstes konfigurieren wir das ListView-Steuerelement, um eine Liste von Produkten anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="658d2-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="658d2-122">Um eine optimale Einkaufserlebnis erstellen wir mehrere präzise Funktionen in jedes einzelne Produkt angezeigt, in unserem ListVew komprimiert werden.</span><span class="sxs-lookup"><span data-stu-id="658d2-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="658d2-123">Der Name des Produkts werden ein Link zur Detailansicht des Produkts.</span><span class="sxs-lookup"><span data-stu-id="658d2-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="658d2-124">Den Preis des Produkts wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="658d2-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="658d2-125">Ein Bild des Produkts wird angezeigt, und dynamisch wähle das Image aus einer Katalog-Bildverzeichnis in unserer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="658d2-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="658d2-126">Es enthält einen Link, um sofort das jeweiligen Produkt zum Einkaufswagen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="658d2-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="658d2-127">Hier ist das Markup für die gegebene Instanz des ListView-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="658d2-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="658d2-128">Dynamisch erstellen wir einige Links für die einzelnen Produkte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="658d2-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="658d2-129">Bevor wir eigene neue Seite testen müssen wir darüber hinaus die Verzeichnisstruktur für das Produkt Katalog-Images erstellen, die wie folgt.</span><span class="sxs-lookup"><span data-stu-id="658d2-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="658d2-130">Sobald unser Produktbilder zugegriffen werden kann, können wir unsere Produktseite für die Liste testen.</span><span class="sxs-lookup"><span data-stu-id="658d2-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="658d2-131">Klicken Sie auf einen der Links die Kategorie-Liste, auf der Startseite der Website.</span><span class="sxs-lookup"><span data-stu-id="658d2-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="658d2-132">Jetzt müssen wir die ProductDetails.aspx-Seite und die AddToCart-Funktionalität zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="658d2-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="658d2-133">Verwenden Sie Datei -&gt;neu, um einen Seitennamen ProductDetails.aspx mithilfe der Website-Masterseite, wie schon zuvor zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="658d2-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="658d2-134">Verwenden wir erneut einen EntityDataSource-Steuerelement auf den bestimmten Produktdatensatz in der Datenbank zugreifen, und wir verwenden ein ASP.NET FormView-Steuerelement, um die Produktdaten wie folgt anzeigen.</span><span class="sxs-lookup"><span data-stu-id="658d2-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="658d2-135">Machen Sie sich keine Gedanken Sie, wenn die Formatierung für Sie ein wenig seltsam aussieht.</span><span class="sxs-lookup"><span data-stu-id="658d2-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="658d2-136">Das Markup oben bleibt Platz im Anzeigelayout für eine Reihe von Features, die wir später implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="658d2-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="658d2-137">Der Warenkorb stellt die komplexere Logik in unserer Anwendung dar.</span><span class="sxs-lookup"><span data-stu-id="658d2-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="658d2-138">Verwenden Sie zum Einstieg Dateien&gt;neu, um eine Seite mit dem MyShoppingCart.aspx zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="658d2-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="658d2-139">Beachten Sie, dass wir nicht den Namen ShoppingCart.aspx auswählen.</span><span class="sxs-lookup"><span data-stu-id="658d2-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="658d2-140">Unsere Datenbank enthält eine Tabelle namens "ShoppingCart".</span><span class="sxs-lookup"><span data-stu-id="658d2-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="658d2-141">Wenn wir ein Entity Data Model generiert wurde eine Klasse für jede Tabelle in der Datenbank erstellt.</span><span class="sxs-lookup"><span data-stu-id="658d2-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="658d2-142">Aus diesem Grund generiert der Entity Data Model eine Entitätsklasse, die mit dem Namen "ShoppingCart".</span><span class="sxs-lookup"><span data-stu-id="658d2-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="658d2-143">Es konnte das Modell bearbeitet werden, damit wir verwenden Sie diesen Namen für die shopping Cart-Implementierung oder für unsere Anforderungen erweitern können, aber wir werden stattdessen angeben, dass Sie einfach einen Namen auswählen, der den Konflikt zu vermeiden, wird.</span><span class="sxs-lookup"><span data-stu-id="658d2-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="658d2-144">Es ist auch zu beachten Sie, dass wir einen einfachen Warenkorb erstellen und betten die shopping Cart-Logik, mit der shopping Cart-Anzeige.</span><span class="sxs-lookup"><span data-stu-id="658d2-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="658d2-145">Wir können auch auswählen, unsere warenkorbsoftware in einer vollständig separaten Business-Ebene zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="658d2-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="658d2-146">[Zurück](tailspin-spyworks-part-3.md)
> [Weiter](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="658d2-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
