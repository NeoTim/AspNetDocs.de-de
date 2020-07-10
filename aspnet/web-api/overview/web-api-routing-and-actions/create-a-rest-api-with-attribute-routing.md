---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Erstellen einer Rest-API mit Attribut Routing in ASP.net-Web-API 2 | Microsoft-Dokumentation
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188851"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="0b6c3-102">Erstellen einer Rest-API mit Attribut Routing in ASP.net-Web-API 2</span><span class="sxs-lookup"><span data-stu-id="0b6c3-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="0b6c3-103">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0b6c3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0b6c3-104">Web-API 2 unterstützt eine neue Art von Routing namens *Attribut Routing*.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="0b6c3-105">Eine allgemeine Übersicht über das Attribut Routing finden Sie unter [Attribut Routing in der Web-API 2](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="0b6c3-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="0b6c3-106">In diesem Tutorial verwenden Sie das Attribut Routing zum Erstellen einer Rest-API für eine Sammlung von Büchern.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="0b6c3-107">Die API unterstützt die folgenden Aktionen:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-107">The API will support the following actions:</span></span>

| <span data-ttu-id="0b6c3-108">Aktion</span><span class="sxs-lookup"><span data-stu-id="0b6c3-108">Action</span></span> | <span data-ttu-id="0b6c3-109">Beispiel-URI</span><span class="sxs-lookup"><span data-stu-id="0b6c3-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="0b6c3-110">Hier finden Sie eine Liste aller Bücher.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-110">Get a list of all books.</span></span> | <span data-ttu-id="0b6c3-111">/api/books</span><span class="sxs-lookup"><span data-stu-id="0b6c3-111">/api/books</span></span> |
| <span data-ttu-id="0b6c3-112">Sie erhalten ein Buch anhand der ID.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-112">Get a book by ID.</span></span> | <span data-ttu-id="0b6c3-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="0b6c3-113">/api/books/1</span></span> |
| <span data-ttu-id="0b6c3-114">Hier finden Sie die Details eines Buchs.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-114">Get the details of a book.</span></span> | <span data-ttu-id="0b6c3-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="0b6c3-115">/api/books/1/details</span></span> |
| <span data-ttu-id="0b6c3-116">Eine Liste der Bücher nach Genre erhalten.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-116">Get a list of books by genre.</span></span> | <span data-ttu-id="0b6c3-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="0b6c3-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="0b6c3-118">Eine Liste der Bücher nach Veröffentlichungsdatum erhalten.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="0b6c3-119">/API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (alternative Form)</span><span class="sxs-lookup"><span data-stu-id="0b6c3-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="0b6c3-120">Eine Liste der Bücher von einem bestimmten Autor erhalten.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="0b6c3-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="0b6c3-121">/api/authors/1/books</span></span> |

<span data-ttu-id="0b6c3-122">Alle Methoden sind schreibgeschützt (HTTP GET-Anforderungen).</span><span class="sxs-lookup"><span data-stu-id="0b6c3-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="0b6c3-123">Für die Datenebene verwenden wir Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="0b6c3-124">Buch Datensätze verfügen über die folgenden Felder:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="0b6c3-125">ID</span><span class="sxs-lookup"><span data-stu-id="0b6c3-125">ID</span></span>
- <span data-ttu-id="0b6c3-126">Titel</span><span class="sxs-lookup"><span data-stu-id="0b6c3-126">Title</span></span>
- <span data-ttu-id="0b6c3-127">Genre</span><span class="sxs-lookup"><span data-stu-id="0b6c3-127">Genre</span></span>
- <span data-ttu-id="0b6c3-128">Veröffentlichungsdatum</span><span class="sxs-lookup"><span data-stu-id="0b6c3-128">Publication date</span></span>
- <span data-ttu-id="0b6c3-129">Preis</span><span class="sxs-lookup"><span data-stu-id="0b6c3-129">Price</span></span>
- <span data-ttu-id="0b6c3-130">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0b6c3-130">Description</span></span>
- <span data-ttu-id="0b6c3-131">AutorID (Fremdschlüssel für eine Autoren Tabelle)</span><span class="sxs-lookup"><span data-stu-id="0b6c3-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="0b6c3-132">Bei den meisten Anforderungen gibt die API jedoch eine Teilmenge dieser Daten zurück (Titel, Autor und Genre).</span><span class="sxs-lookup"><span data-stu-id="0b6c3-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="0b6c3-133">Um den gesamten Datensatz zu erhalten, fordert der Client an `/api/books/{id}/details` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b6c3-134">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="0b6c3-134">Prerequisites</span></span>

<span data-ttu-id="0b6c3-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional oder Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="0b6c3-136">Erstellen des Visual Studio-Projekts</span><span class="sxs-lookup"><span data-stu-id="0b6c3-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="0b6c3-137">Führen Sie zuerst Visual Studio 2013 aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-137">Start by running Visual Studio.</span></span> <span data-ttu-id="0b6c3-138">Wählen Sie im Menü **Datei** die Option **neu** aus, und wählen Sie dann **Projekt**aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="0b6c3-139">Erweitern Sie die **installierte**  >  **Visual c#** -Kategorie.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="0b6c3-140">Wählen Sie unter **Visual c#** die Option **Web**aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="0b6c3-141">Wählen Sie in der Liste der Projektvorlagen die Option **ASP.NET Webanwendung (.NET Framework)** aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="0b6c3-142">Nennen Sie das Projekt &quot; booksapi &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="0b6c3-143">Wählen Sie im Dialogfeld **New ASP.NET Webanwendung** die Vorlage **leere** Vorlage aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="0b6c3-144">Aktivieren Sie unter "Ordner und Kern Verweise hinzufügen" das Kontrollkästchen **Web-API** .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="0b6c3-145">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="0b6c3-146">Dadurch wird ein Skeleton-Projekt erstellt, das für die Web-API-Funktionalität konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="0b6c3-147">Domänen Modelle</span><span class="sxs-lookup"><span data-stu-id="0b6c3-147">Domain Models</span></span>

<span data-ttu-id="0b6c3-148">Fügen Sie als nächstes Klassen für Domänen Modelle hinzu.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-148">Next, add classes for domain models.</span></span> <span data-ttu-id="0b6c3-149">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner „Modelle“.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="0b6c3-150">Wählen Sie **Hinzufügen**und dann **Klasse**aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="0b6c3-151">Geben Sie der Klassen den Namen `Author`.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="0b6c3-152">Ersetzen Sie den Code in Author.cs durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="0b6c3-153">Fügen Sie jetzt eine weitere Klasse namens hinzu `Book` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="0b6c3-154">Hinzufügen eines Web-API-Controllers</span><span class="sxs-lookup"><span data-stu-id="0b6c3-154">Add a Web API Controller</span></span>

<span data-ttu-id="0b6c3-155">In diesem Schritt fügen wir einen Web-API-Controller hinzu, der Entity Framework als Datenschicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="0b6c3-156">Drücken Sie STRG+UMSCHALT+B, um das Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="0b6c3-157">Entity Framework verwendet Reflektion, um die Eigenschaften der Modelle zu ermitteln. Daher ist eine kompilierte Assembly erforderlich, um das Datenbankschema zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="0b6c3-158">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner „Controller“.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="0b6c3-159">Wählen Sie **Hinzufügen**und dann **Controller**aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="0b6c3-160">Wählen Sie im Dialogfeld **Gerüst hinzufügen** die Option **Web-API 2-Controller mit Aktionen aus, indem Sie Entity Framework verwenden**.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="0b6c3-161">Geben Sie im Dialogfeld **Controller hinzufügen** für **Controller Name den Namen** &quot; bookscontroller ein &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="0b6c3-162">Aktivieren Sie das &quot; Kontrollkästchen Async Controller-Aktionen verwenden &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="0b6c3-163">Wählen Sie für **Modell Klasse**die Option &quot; Buch aus &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="0b6c3-164">(Wenn die `Book` in der Dropdown Liste aufgeführte Klasse nicht angezeigt wird, stellen Sie sicher, dass Sie das Projekt erstellt haben.) Klicken Sie dann auf die Schaltfläche "+".</span><span class="sxs-lookup"><span data-stu-id="0b6c3-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="0b6c3-165">Klicken Sie im Dialogfeld **neuer Datenkontext** auf **Hinzufügen** .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="0b6c3-166">Klicken Sie im Dialogfeld **Controller hinzufügen** auf **Hinzufügen** .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="0b6c3-167">Das Gerüst fügt eine Klasse mit dem Namen hinzu `BooksController` , die den API-Controller definiert.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="0b6c3-168">Außerdem wird im Ordner Models eine Klasse namens hinzugefügt `BooksAPIContext` , die den Datenkontext für Entity Framework definiert.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="0b6c3-169">Durchführen eines Datenbankseedings</span><span class="sxs-lookup"><span data-stu-id="0b6c3-169">Seed the Database</span></span>

<span data-ttu-id="0b6c3-170">Klicken Sie im Menü Extras auf **nuget-Paket-Manager**, und wählen Sie dann **Paket-Manager-Konsole**aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="0b6c3-171">Geben Sie im Fenster Paket-Manager-Konsole den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="0b6c3-172">Mit diesem Befehl wird ein Migrations Ordner erstellt und eine neue Codedatei mit dem Namen Configuration.cs hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="0b6c3-173">Öffnen Sie diese Datei, und fügen Sie der-Methode den folgenden Code hinzu `Configuration.Seed` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="0b6c3-174">Geben Sie im Fenster der Paket-Manager-Konsole die folgenden Befehle ein.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="0b6c3-175">Diese Befehle erstellen eine lokale Datenbank und rufen die Seed-Methode auf, um die Datenbank aufzufüllen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="0b6c3-176">Dto-Klassen hinzufügen</span><span class="sxs-lookup"><span data-stu-id="0b6c3-176">Add DTO Classes</span></span>

<span data-ttu-id="0b6c3-177">Wenn Sie die Anwendung jetzt ausführen und eine GET-Anforderung an/API/Books/1 senden, sieht die Antwort in etwa wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="0b6c3-178">(Ich habe zur besseren Lesbarkeit einen Einzug hinzugefügt.)</span><span class="sxs-lookup"><span data-stu-id="0b6c3-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="0b6c3-179">Stattdessen möchte ich, dass diese Anforderung eine Teilmenge der Felder zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="0b6c3-180">Außerdem möchte ich, dass Sie den Namen des Autors anstelle der Autoren-ID zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="0b6c3-181">Um dies zu erreichen, ändern wir die Controller Methoden so, dass ein *Datenübertragungs Objekt (Data Transfer Object* , dto) anstelle des EF-Modells zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="0b6c3-182">Ein DTO ist ein Objekt, das nur zum Übertragen von Daten vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="0b6c3-183">Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das **Add**Projekt, und wählen Sie  |  **neuen Ordner**hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="0b6c3-184">Benennen Sie den Ordner &quot; DTOs &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="0b6c3-185">Fügen Sie `BookDto` dem Ordner DTOs eine Klasse mit dem Namen mit der folgenden Definition hinzu:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="0b6c3-186">Fügen Sie eine weitere Klasse namens `BookDetailDto`hinzu.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="0b6c3-187">Aktualisieren Sie anschließend die- `BooksController` Klasse, um-Instanzen zurückzugeben `BookDto` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="0b6c3-188">Wir verwenden die abfragbare [. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) -Methode, um `Book` Instanzen in Instanzen zu projizieren `BookDto` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="0b6c3-189">Im folgenden finden Sie den aktualisierten Code für die Controller-Klasse.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="0b6c3-190">Ich habe die `PutBook` `PostBook` Methoden, und gelöscht `DeleteBook` , da Sie für dieses Tutorial nicht benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="0b6c3-191">Wenn Sie nun die Anwendung ausführen und/API/Books/1 anfordern, sollte der Antworttext wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="0b6c3-192">Routen Attribute hinzufügen</span><span class="sxs-lookup"><span data-stu-id="0b6c3-192">Add Route Attributes</span></span>

<span data-ttu-id="0b6c3-193">Als nächstes konvertieren wir den Controller, um Attribut Routing zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="0b6c3-194">Fügen Sie zunächst dem Controller ein **routeprefix** -Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="0b6c3-195">Dieses Attribut definiert die anfänglichen URI-Segmente für alle Methoden auf diesem Controller.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="0b6c3-196">Fügen Sie dann wie folgt **[Route]** -Attribute zu den Controller Aktionen hinzu:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="0b6c3-197">Die Routen Vorlage für jede Controller Methode ist das Präfix und die im **Routen** Attribut angegebene Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="0b6c3-198">Bei der- `GetBook` Methode enthält die Routen Vorlage die parametrisierte Zeichenfolge &quot; {ID: int} &quot; , die entspricht, wenn das URI-Segment einen ganzzahligen Wert enthält.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="0b6c3-199">Methode</span><span class="sxs-lookup"><span data-stu-id="0b6c3-199">Method</span></span> | <span data-ttu-id="0b6c3-200">Routenvorlage</span><span class="sxs-lookup"><span data-stu-id="0b6c3-200">Route Template</span></span> | <span data-ttu-id="0b6c3-201">Beispiel-URI</span><span class="sxs-lookup"><span data-stu-id="0b6c3-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="0b6c3-202">"API/Bücher"</span><span class="sxs-lookup"><span data-stu-id="0b6c3-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="0b6c3-203">"API/Books/{ID: int}"</span><span class="sxs-lookup"><span data-stu-id="0b6c3-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="0b6c3-204">Buch Details anzeigen</span><span class="sxs-lookup"><span data-stu-id="0b6c3-204">Get Book Details</span></span>

<span data-ttu-id="0b6c3-205">Um Buch Details zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/{id}/details` , wobei *{ID}* die ID des Buchs ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="0b6c3-206">Fügen Sie der `BooksController`-Klasse die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="0b6c3-207">Wenn Sie anfordern `/api/books/1/details` , sieht die Antwort wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="0b6c3-208">Bücher nach Genre erhalten</span><span class="sxs-lookup"><span data-stu-id="0b6c3-208">Get Books By Genre</span></span>

<span data-ttu-id="0b6c3-209">Um eine Liste der Bücher in einem bestimmten Genre zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/genre` , wobei *Genre* der Name des Genres ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="0b6c3-210">(Beispiel: `/api/books/fantasy`.)</span><span class="sxs-lookup"><span data-stu-id="0b6c3-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="0b6c3-211">Fügen Sie die folgende Methode hinzu `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="0b6c3-212">Hier definieren wir eine Route, die einen {Genre}-Parameter in der URI-Vorlage enthält.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="0b6c3-213">Beachten Sie, dass die Web-API diese beiden URIs unterscheiden und an verschiedene Methoden weiterleiten kann:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="0b6c3-214">Dies liegt daran, dass die- `GetBook` Methode eine Einschränkung enthält, dass das "ID"-Segment ein ganzzahliger Wert sein muss:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="0b6c3-215">Wenn Sie/API/Books/Fantasy anfordern, sieht die Antwort wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="0b6c3-216">Bücher von Autor erhalten</span><span class="sxs-lookup"><span data-stu-id="0b6c3-216">Get Books By Author</span></span>

<span data-ttu-id="0b6c3-217">Um eine Liste der Bücher für einen bestimmten Autor zu erhalten, sendet der Client eine GET-Anforderung an `/api/authors/id/books` , wobei *ID* die ID des Autors ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="0b6c3-218">Fügen Sie die folgende Methode hinzu `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="0b6c3-219">Dieses Beispiel ist interessant, da &quot; Bücher &quot; als untergeordnete Ressource von &quot; Autoren behandelt werden &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="0b6c3-220">Dieses Muster ist in den Rest-APIs sehr üblich.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="0b6c3-221">Die Tilde (~) in der Routen Vorlage überschreibt das Routen Präfix im **routeprefix** -Attribut.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="0b6c3-222">Bücher nach Veröffentlichungsdatum erhalten</span><span class="sxs-lookup"><span data-stu-id="0b6c3-222">Get Books By Publication Date</span></span>

<span data-ttu-id="0b6c3-223">Um eine Liste der Bücher nach Veröffentlichungsdatum zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/date/yyyy-mm-dd` , wobei *yyyy-mm-dd* das Datum ist.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="0b6c3-224">Dies ist eine Möglichkeit, dies zu erreichen:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="0b6c3-225">Der- `{pubdate:datetime}` Parameter ist auf einen **DateTime** -Wert beschränkt.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="0b6c3-226">Dies funktioniert, aber es ist besser, als wir wollen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="0b6c3-227">Beispielsweise entsprechen diese URIs auch der Route:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="0b6c3-228">Es gibt nichts falsches, wenn diese URIs zugelassen werden.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="0b6c3-229">Allerdings können Sie die Route auf ein bestimmtes Format beschränken, indem Sie der Routen Vorlage eine Einschränkung für reguläre Ausdrücke hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="0b6c3-230">Nun stimmen nur die Datumsangaben im Format &quot; yyyy-mm-dd ab &quot; .</span><span class="sxs-lookup"><span data-stu-id="0b6c3-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="0b6c3-231">Beachten Sie, dass wir den Regex nicht verwenden, um zu überprüfen, ob wir ein echtes Datum erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="0b6c3-232">Dies wird behandelt, wenn die Web-API versucht, das URI-Segment in eine **DateTime** -Instanz zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="0b6c3-233">Ein ungültiges Datum, wie z. b. "2012-47-99", kann nicht konvertiert werden, und der Client erhält einen 404-Fehler.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="0b6c3-234">Sie können auch ein Schrägstrich ( `/api/books/date/yyyy/mm/dd` ) durch Hinzufügen eines weiteren **[Route]** -Attributs mit einem anderen Regex unterstützen.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="0b6c3-235">Hier finden Sie ein sehr feines, aber wichtiges Detail.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="0b6c3-236">Die zweite Routen Vorlage enthält ein Platzhalter Zeichen ( \* ) am Anfang des {pubDate}-Parameters:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="0b6c3-237">Dadurch wird der Routing-Engine mitgeteilt, dass {pubDate} dem Rest des URIs entsprechen soll.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="0b6c3-238">Standardmäßig entspricht ein Vorlagen Parameter einem einzelnen URI-Segment.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="0b6c3-239">In diesem Fall möchten wir, dass {pubDate} mehrere URI-Segmente umfasst:</span><span class="sxs-lookup"><span data-stu-id="0b6c3-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="0b6c3-240">Controller Code</span><span class="sxs-lookup"><span data-stu-id="0b6c3-240">Controller Code</span></span>

<span data-ttu-id="0b6c3-241">Im folgenden finden Sie den gesamten Code für die bookscontroller-Klasse.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="0b6c3-242">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="0b6c3-242">Summary</span></span>

<span data-ttu-id="0b6c3-243">Das Attribut Routing bietet Ihnen mehr Kontrolle und größere Flexibilität beim Entwerfen der URIs für Ihre API.</span><span class="sxs-lookup"><span data-stu-id="0b6c3-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
