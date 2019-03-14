---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Hinzufügen von Modellen und Controllern | Microsoft-Dokumentation
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 162ef2cd4ba11040e1bc938617a36495489ba5bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037287"
---
<a name="add-models-and-controllers"></a><span data-ttu-id="c2834-102">Hinzufügen von Modellen und Controllern</span><span class="sxs-lookup"><span data-stu-id="c2834-102">Add Models and Controllers</span></span>
====================
<span data-ttu-id="c2834-103">durch [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c2834-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c2834-104">Abgeschlossenes Projekt herunterladen</span><span class="sxs-lookup"><span data-stu-id="c2834-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c2834-105">In diesem Abschnitt fügen Sie ViewModel-Klassen, die die Datenbankentitäten zu definieren.</span><span class="sxs-lookup"><span data-stu-id="c2834-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="c2834-106">Dann können Sie Web-API-Controller hinzufügen, die CRUD-Vorgänge für diese Entitäten ausführen.</span><span class="sxs-lookup"><span data-stu-id="c2834-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="c2834-107">Hinzufügen von Modellklassen</span><span class="sxs-lookup"><span data-stu-id="c2834-107">Add Model Classes</span></span>

<span data-ttu-id="c2834-108">In diesem Tutorial erstellen wir die Datenbank mithilfe des "Code First"-Ansatzes zu Entity Framework (EF).</span><span class="sxs-lookup"><span data-stu-id="c2834-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="c2834-109">Klicken Sie mit Code First Sie schreiben C#-Klassen, die entsprechen, Datenbanktabellen, und EF erstellt die Datenbank.</span><span class="sxs-lookup"><span data-stu-id="c2834-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="c2834-110">(Weitere Informationen finden Sie unter [Entity Framework-Webentwicklungsansätzen](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span><span class="sxs-lookup"><span data-stu-id="c2834-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="c2834-111">Definieren zunächst wir unser Domänenobjekte als POCOs (Plain-Old CLR Objects).</span><span class="sxs-lookup"><span data-stu-id="c2834-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="c2834-112">Wir erstellen die folgenden POCOs:</span><span class="sxs-lookup"><span data-stu-id="c2834-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="c2834-113">Autor</span><span class="sxs-lookup"><span data-stu-id="c2834-113">Author</span></span>
- <span data-ttu-id="c2834-114">Buch</span><span class="sxs-lookup"><span data-stu-id="c2834-114">Book</span></span>

<span data-ttu-id="c2834-115">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner "Models".</span><span class="sxs-lookup"><span data-stu-id="c2834-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="c2834-116">Wählen Sie **hinzufügen**, und wählen Sie dann **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="c2834-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="c2834-117">Nennen Sie die Klasse `Author`.</span><span class="sxs-lookup"><span data-stu-id="c2834-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="c2834-118">Ersetzen Sie alle die Codebausteine in Author.cs durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="c2834-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="c2834-119">Fügen Sie eine andere Klasse, die mit dem Namen `Book`, durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="c2834-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="c2834-120">Entitätsframework verwendet diese Modelle zum Erstellen von Tabellen.</span><span class="sxs-lookup"><span data-stu-id="c2834-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="c2834-121">Für jedes Modell das `Id` Eigenschaft werden die Primärschlüsselspalte der Datenbanktabelle.</span><span class="sxs-lookup"><span data-stu-id="c2834-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="c2834-122">In der Book-Klasse die `AuthorId` definiert einen Fremdschlüssel in der `Author` Tabelle.</span><span class="sxs-lookup"><span data-stu-id="c2834-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="c2834-123">(Der Einfachheit halber habe ich vorausgesetzt, dass jedes Buch einen einzelnen Autor hat.) Die Buch-Klasse enthält auch eine Navigationseigenschaft für den zugehörigen `Author`.</span><span class="sxs-lookup"><span data-stu-id="c2834-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="c2834-124">Können Sie den entsprechenden Zugriff auf die Navigationseigenschaft `Author` im Code.</span><span class="sxs-lookup"><span data-stu-id="c2834-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="c2834-125">Weitere Informationen zu Navigationseigenschaften in Teil 4, sagen [Verarbeiten von Entitätsbeziehungen](part-4.md).</span><span class="sxs-lookup"><span data-stu-id="c2834-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="c2834-126">Hinzufügen von Web-API-Controllern</span><span class="sxs-lookup"><span data-stu-id="c2834-126">Add Web API Controllers</span></span>

<span data-ttu-id="c2834-127">In diesem Abschnitt fügen wir Web-API-Controller, die CRUD-Vorgänge zu unterstützen (erstellen, lesen, aktualisieren und löschen).</span><span class="sxs-lookup"><span data-stu-id="c2834-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="c2834-128">Controller werden Entity Framework verwenden, um mit der Datenbankebene kommunizieren zu können.</span><span class="sxs-lookup"><span data-stu-id="c2834-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="c2834-129">Erstens können Sie die Datei Controllers/ValuesController.cs löschen.</span><span class="sxs-lookup"><span data-stu-id="c2834-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="c2834-130">Diese Datei enthält einen Beispiel-Web-API-Controller, aber nicht für dieses Tutorial erforderlich.</span><span class="sxs-lookup"><span data-stu-id="c2834-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="c2834-131">Als Nächstes erstellen Sie das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="c2834-131">Next, build the project.</span></span> <span data-ttu-id="c2834-132">Das Web-API-Gerüst verwendet Reflektion, um die Modellklassen gefunden, daher muss die kompilierte Assembly festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c2834-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="c2834-133">Klicken Sie im Projektmappen-Explorer den Ordner "Controllers".</span><span class="sxs-lookup"><span data-stu-id="c2834-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="c2834-134">Wählen Sie **hinzufügen**, und wählen Sie dann **Controller**.</span><span class="sxs-lookup"><span data-stu-id="c2834-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="c2834-135">In der **Gerüst hinzufügen** wählen Sie im Dialogfeld "Web-API 2-Controller mit Aktionen unter Verwendung von Entitätsframework".</span><span class="sxs-lookup"><span data-stu-id="c2834-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="c2834-136">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c2834-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="c2834-137">In der **Controller hinzufügen** Dialogfeld, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="c2834-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="c2834-138">In der **Modellklasse** Dropdownliste, wählen die `Author` Klasse.</span><span class="sxs-lookup"><span data-stu-id="c2834-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="c2834-139">(Wenn Sie nicht, dass es in der Dropdownliste aufgeführt sehen, stellen Sie sicher, dass Sie das Projekt erstellt.)</span><span class="sxs-lookup"><span data-stu-id="c2834-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="c2834-140">Überprüfen Sie "Async-Controlleraktionen verwenden".</span><span class="sxs-lookup"><span data-stu-id="c2834-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="c2834-141">Lassen Sie den Namen der Controller als &quot;"authorscontroller"&quot;.</span><span class="sxs-lookup"><span data-stu-id="c2834-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="c2834-142">Klicken Sie auf Pluszeichen (+) neben Schaltfläche **Datenkontextklasse**.</span><span class="sxs-lookup"><span data-stu-id="c2834-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="c2834-143">In der **neuer Datenkontext** Dialogfeld, übernehmen Sie den Standardnamen, und klicken Sie auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c2834-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="c2834-144">Klicken Sie auf **hinzufügen** zum Abschließen der **Controller hinzufügen** Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="c2834-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="c2834-145">Das Dialogfeld fügt zwei Klassen zu Ihrem Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="c2834-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="c2834-146">`AuthorsController` definiert einen Web-API-Controller.</span><span class="sxs-lookup"><span data-stu-id="c2834-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="c2834-147">Der Controller implementiert die REST-API, die Clients zum Ausführen von CRUD-Vorgänge in der Liste der Autoren verwenden.</span><span class="sxs-lookup"><span data-stu-id="c2834-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="c2834-148">`BookServiceContext` Entitätsobjekte verwaltet während der Laufzeit, einschließlich ausfüllenden Objekten mit Daten aus einer Datenbank, Nachverfolgen von Änderungen und Beibehalten von Daten in der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="c2834-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="c2834-149">Sie erbt von `DbContext`.</span><span class="sxs-lookup"><span data-stu-id="c2834-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="c2834-150">An diesem Punkt erstellen Sie das Projekt erneut.</span><span class="sxs-lookup"><span data-stu-id="c2834-150">At this point, build the project again.</span></span> <span data-ttu-id="c2834-151">Kehren Sie nun über die gleichen Schritte zum Hinzufügen von eines API-Controllers für `Book` Entitäten.</span><span class="sxs-lookup"><span data-stu-id="c2834-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="c2834-152">Wählen Sie dieses Mal `Book` für die Model-Klasse, und wählen Sie die vorhandene `BookServiceContext` -Klasse für das die Datenkontextklasse.</span><span class="sxs-lookup"><span data-stu-id="c2834-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="c2834-153">(Erstellen Sie keinen neuen Datenkontext.) Klicken Sie auf **hinzufügen** Controller hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c2834-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="c2834-154">[Zurück](part-1.md)
> [Weiter](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="c2834-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
