---
title: 'Razor-Seiten mit EF Core in ASP.NET Core: Lesen verwandter Daten (6 von 8)'
author: rick-anderson
description: In diesem Tutorial werden verwandte Daten gelesen und angezeigt. Das gilt für Daten, die Entity Framework in Navigationseigenschaften lädt.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: data/ef-rp/read-related-data
ms.openlocfilehash: cf8733e1e806c4be0c4b217fc45c7a338a03a3ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061857"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---read-related-data---6-of-8"></a><span data-ttu-id="689ec-103">Razor-Seiten mit EF Core in ASP.NET Core: Lesen verwandter Daten (6 von 8)</span><span class="sxs-lookup"><span data-stu-id="689ec-103">Razor Pages with EF Core in ASP.NET Core - Read Related Data - 6 of 8</span></span>

<span data-ttu-id="689ec-104">Von [Tom Dykstra](https://github.com/tdykstra), [Jon P. Smith](https://twitter.com/thereformedprog) und [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="689ec-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="689ec-105">In diesem Tutorial werden verwandte Daten gelesen und angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-105">In this tutorial, related data is read and displayed.</span></span> <span data-ttu-id="689ec-106">Verwandte Daten sind Daten, die von EF Core in die Navigationseigenschaften geladen werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-106">Related data is data that EF Core loads into navigation properties.</span></span>

<span data-ttu-id="689ec-107">Wenn nicht zu lösende Probleme auftreten, laden Sie die [fertige App](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) herunter, oder zeigen Sie diese an.</span><span class="sxs-lookup"><span data-stu-id="689ec-107">If you run into problems you can't solve, [download or view the completed app.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)</span></span> <span data-ttu-id="689ec-108">[Anweisungen zum Download.](xref:index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="689ec-108">[Download instructions](xref:index#how-to-download-a-sample).</span></span>

<span data-ttu-id="689ec-109">Die folgenden Abbildungen zeigen die abgeschlossenen Seiten für dieses Tutorial:</span><span class="sxs-lookup"><span data-stu-id="689ec-109">The following illustrations show the completed pages for this tutorial:</span></span>

![Indexseite „Kurse“](read-related-data/_static/courses-index.png)

![Indexseite „Dozenten“](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a><span data-ttu-id="689ec-112">Explizites, Eager und Lazy Loading verwandter Daten</span><span class="sxs-lookup"><span data-stu-id="689ec-112">Eager, explicit, and lazy Loading of related data</span></span>

<span data-ttu-id="689ec-113">Es gibt mehrere Möglichkeiten, mit denen EF Core verwandte Daten in die Navigationseigenschaften einer Entität laden kann:</span><span class="sxs-lookup"><span data-stu-id="689ec-113">There are several ways that EF Core can load related data into the navigation properties of an entity:</span></span>

* <span data-ttu-id="689ec-114">[Eager Loading (vorzeitiges Laden)](/ef/core/querying/related-data#eager-loading).</span><span class="sxs-lookup"><span data-stu-id="689ec-114">[Eager loading](/ef/core/querying/related-data#eager-loading).</span></span> <span data-ttu-id="689ec-115">Beim Eager Loading lädt eine Abfrage für einen Entitätstyp auch verwandte Entitäten.</span><span class="sxs-lookup"><span data-stu-id="689ec-115">Eager loading is when a query for one type of entity also loads related entities.</span></span> <span data-ttu-id="689ec-116">Wenn die Entität gelesen wird, werden ihre verwandten Daten abgerufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-116">When the entity is read, its related data is retrieved.</span></span> <span data-ttu-id="689ec-117">Dies führt normalerweise zu einer einzelnen Joinabfrage, die alle Daten abruft, die erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="689ec-117">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="689ec-118">EF Core wird mehrere Abfragen für einige Typen von Eager Loading ausgeben.</span><span class="sxs-lookup"><span data-stu-id="689ec-118">EF Core will issue multiple queries for some types of eager loading.</span></span> <span data-ttu-id="689ec-119">Die Ausgabe mehrerer Abfragen kann effizienter sein, als dies bei einigen Abfragen in EF6 der Fall war. Dort war nur eine einzelne Abfrage vorhanden.</span><span class="sxs-lookup"><span data-stu-id="689ec-119">Issuing multiple queries can be more efficient than was the case for some queries in EF6 where there was a single query.</span></span> <span data-ttu-id="689ec-120">Eager Loading wird mit den `Include`- und `ThenInclude`-Methoden angegeben.</span><span class="sxs-lookup"><span data-stu-id="689ec-120">Eager loading is specified with the `Include` and `ThenInclude` methods.</span></span>

  ![Beispiel für Eager Loading](read-related-data/_static/eager-loading.png)
 
  <span data-ttu-id="689ec-122">Eager Loading sendet mehrere Abfragen, wenn eine Sammlungsnavigation enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="689ec-122">Eager loading sends multiple queries when a collection navigation is included:</span></span>

  * <span data-ttu-id="689ec-123">Eine Abfrage für die Hauptabfrage</span><span class="sxs-lookup"><span data-stu-id="689ec-123">One query for the main query</span></span> 
  * <span data-ttu-id="689ec-124">Eine Abfrage für jeden „Sammlungsrand“ in der Ladestruktur.</span><span class="sxs-lookup"><span data-stu-id="689ec-124">One query for each collection "edge" in the load tree.</span></span>

* <span data-ttu-id="689ec-125">Beispiel für separate Abfragen mit `Load`: Die Daten können in separaten Abfragen abgerufen werden. EF Core korrigiert die Navigationseigenschaften.</span><span class="sxs-lookup"><span data-stu-id="689ec-125">Separate queries with `Load`: The data can be retrieved in separate queries, and EF Core "fixes up" the navigation properties.</span></span> <span data-ttu-id="689ec-126">„Korrigieren“ bedeutet, dass EF Core die Navigationseigenschaften automatisch füllt.</span><span class="sxs-lookup"><span data-stu-id="689ec-126">"fixes up" means that EF Core automatically populates the navigation properties.</span></span> <span data-ttu-id="689ec-127">Separate Abfragen mit `Load` ähneln mehr dem expliziten Laden als dem Eager Loading.</span><span class="sxs-lookup"><span data-stu-id="689ec-127">Separate queries with `Load` is more like explict loading than eager loading.</span></span>

  ![Beispiel für separate Abfragen](read-related-data/_static/separate-queries.png)

  <span data-ttu-id="689ec-129">Hinweis: EF Core korrigiert automatisch Navigationseigenschaften für alle anderen Entitäten, die zuvor in die Kontextinstanz geladen wurden.</span><span class="sxs-lookup"><span data-stu-id="689ec-129">Note: EF Core automatically fixes up navigation properties to any other entities that were previously loaded into the context instance.</span></span> <span data-ttu-id="689ec-130">Auch wenn die Daten für eine Navigationseigenschaft *nicht* explizit eingeschlossen sind, kann die Eigenschaft immer noch aufgefüllt werden, wenn einige oder alle verwandten Entitäten zuvor geladen wurden.</span><span class="sxs-lookup"><span data-stu-id="689ec-130">Even if the data for a navigation property is *not* explicitly included, the property may still be populated if some or all of the related entities were previously loaded.</span></span>

* <span data-ttu-id="689ec-131">[Explizites Laden](/ef/core/querying/related-data#explicit-loading).</span><span class="sxs-lookup"><span data-stu-id="689ec-131">[Explicit loading](/ef/core/querying/related-data#explicit-loading).</span></span> <span data-ttu-id="689ec-132">Wenn die Entität zuerst gelesen wird, werden verwandte Daten nicht abgerufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-132">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="689ec-133">Es muss Code geschrieben werden, um die verwandten Daten bei Bedarf abzurufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-133">Code must be written to retrieve the related data when it's needed.</span></span> <span data-ttu-id="689ec-134">Explizites Laden mit separaten Abfragen führt zu mehreren Abfragen, die an die Datenbank gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-134">Explicit loading with separate queries results in multiple queries sent to the DB.</span></span> <span data-ttu-id="689ec-135">Mit explizitem Laden gibt der Code die zu ladenden Navigationseigenschaften an.</span><span class="sxs-lookup"><span data-stu-id="689ec-135">With explicit loading, the code specifies the navigation properties to be loaded.</span></span> <span data-ttu-id="689ec-136">Verwenden Sie für explizites Laden die `Load`-Methode.</span><span class="sxs-lookup"><span data-stu-id="689ec-136">Use the `Load` method to do explicit loading.</span></span> <span data-ttu-id="689ec-137">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="689ec-137">For example:</span></span>

  ![Beispiel für explizites Laden](read-related-data/_static/explicit-loading.png)

* <span data-ttu-id="689ec-139">[Lazy Loading (verzögertes Laden)](/ef/core/querying/related-data#lazy-loading).</span><span class="sxs-lookup"><span data-stu-id="689ec-139">[Lazy loading](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="689ec-140">[Lazy Loading wurde in Version 2.1 zu EF Core hinzugefügt](/ef/core/querying/related-data#lazy-loading).</span><span class="sxs-lookup"><span data-stu-id="689ec-140">[Lazy loading was added to EF Core in version 2.1](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="689ec-141">Wenn die Entität zuerst gelesen wird, werden verwandte Daten nicht abgerufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-141">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="689ec-142">Wenn zum ersten Mal auf eine Navigationseigenschaft zugegriffen wird, werden die für diese Navigationseigenschaft erforderlichen Daten automatisch abgerufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-142">The first time a navigation property is accessed, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="689ec-143">Wenn zum ersten Mal auf eine Navigationseigenschaft zugegriffen wird, wird jedes Mal eine Abfrage an die Datenbank geschickt.</span><span class="sxs-lookup"><span data-stu-id="689ec-143">A query is sent to the DB each time a navigation property is accessed for the first time.</span></span>

* <span data-ttu-id="689ec-144">Der `Select`-Operator lädt nur die erforderlichen verwandten Daten.</span><span class="sxs-lookup"><span data-stu-id="689ec-144">The `Select` operator loads only the related data needed.</span></span>

## <a name="create-a-course-page-that-displays-department-name"></a><span data-ttu-id="689ec-145">Erstellen einer Kursseite, die den Abteilungsnamen anzeigt</span><span class="sxs-lookup"><span data-stu-id="689ec-145">Create a Course page that displays department name</span></span>

<span data-ttu-id="689ec-146">Die Course-Entität enthält eine Navigationseigenschaft, welche die `Department`-Entität enthält.</span><span class="sxs-lookup"><span data-stu-id="689ec-146">The Course entity includes a navigation property that contains the `Department` entity.</span></span> <span data-ttu-id="689ec-147">Die `Department`-Entität enthält die Abteilung, der der Kurs zugewiesen ist.</span><span class="sxs-lookup"><span data-stu-id="689ec-147">The `Department` entity contains the department that the course is assigned to.</span></span>

<span data-ttu-id="689ec-148">So zeigen Sie den Namen der zugewiesenen Abteilung in einer Kursliste an:</span><span class="sxs-lookup"><span data-stu-id="689ec-148">To display the name of the assigned department in a list of courses:</span></span>

* <span data-ttu-id="689ec-149">Rufen Sie `Name`-Eigenschaft aus der `Department`-Entität ab.</span><span class="sxs-lookup"><span data-stu-id="689ec-149">Get the `Name` property from the `Department` entity.</span></span>
* <span data-ttu-id="689ec-150">Die `Department`-Entität stammt aus der `Course.Department`-Navigationseigenschaft.</span><span class="sxs-lookup"><span data-stu-id="689ec-150">The `Department` entity comes from the `Course.Department` navigation property.</span></span>

![ourse.Department](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a><span data-ttu-id="689ec-152">Erstellen des Gerüsts für das Kursmodell</span><span class="sxs-lookup"><span data-stu-id="689ec-152">Scaffold the Course model</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="689ec-153">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="689ec-153">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="689ec-154">Führen Sie die Schritte unter [Erstellen des Gerüsts für das Studentenmodell](xref:data/ef-rp/intro#scaffold-the-student-model) aus, und verwenden Sie `Course` für die Modellklasse.</span><span class="sxs-lookup"><span data-stu-id="689ec-154">Follow the instructions in [Scaffold the student model](xref:data/ef-rp/intro#scaffold-the-student-model) and use `Course` for the model class.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="689ec-155">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="689ec-155">.NET Core CLI</span></span>](#tab/netcore-cli)

 <span data-ttu-id="689ec-156">Führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="689ec-156">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
  ```

------

<span data-ttu-id="689ec-157">Der vorherige Befehl erstellt ein Gerüst für das `Course`-Modell.</span><span class="sxs-lookup"><span data-stu-id="689ec-157">The preceding command scaffolds the `Course` model.</span></span> <span data-ttu-id="689ec-158">Öffnen Sie das Projekt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="689ec-158">Open the project in Visual Studio.</span></span>

<span data-ttu-id="689ec-159">Öffnen Sie *Pages/Courses/Index.cshtml.cs*. Untersuchen Sie die `OnGetAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="689ec-159">Open *Pages/Courses/Index.cshtml.cs* and examine the `OnGetAsync` method.</span></span> <span data-ttu-id="689ec-160">Die Gerüstbauengine gibt Eager Loading für die `Department`-Navigationseigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="689ec-160">The scaffolding engine specified eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="689ec-161">Die `Include`-Methode gibt Eager Loading an.</span><span class="sxs-lookup"><span data-stu-id="689ec-161">The `Include` method specifies eager loading.</span></span>

<span data-ttu-id="689ec-162">Führen Sie die Anwendung aus, und klicken Sie auf den Link **Kurse**.</span><span class="sxs-lookup"><span data-stu-id="689ec-162">Run the app and select the **Courses** link.</span></span> <span data-ttu-id="689ec-163">Die Abteilungsspalte zeigt die `DepartmentID` an, die nicht hilfreich ist.</span><span class="sxs-lookup"><span data-stu-id="689ec-163">The department column displays the `DepartmentID`, which isn't useful.</span></span>

<span data-ttu-id="689ec-164">Aktualisieren Sie die `OnGetAsync`-Methode mit folgendem Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-164">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

<span data-ttu-id="689ec-165">Der vorangehende Code fügt `AsNoTracking` hinzu.</span><span class="sxs-lookup"><span data-stu-id="689ec-165">The preceding code adds `AsNoTracking`.</span></span> <span data-ttu-id="689ec-166">`AsNoTracking` verbessert die Leistung, da die zurückgegebenen Entitäten nicht nachverfolgt werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-166">`AsNoTracking` improves performance because the entities returned are not tracked.</span></span> <span data-ttu-id="689ec-167">Die Entitäten werden nicht nachverfolgt, da sie nicht im aktuellen Kontext aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-167">The entities are not tracked because they're not updated in the current context.</span></span>

<span data-ttu-id="689ec-168">Aktualisieren Sie *Pages/Courses/Index.cshtml* mit dem folgenden hervorgehobenen Markup:</span><span class="sxs-lookup"><span data-stu-id="689ec-168">Update *Pages/Courses/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

<span data-ttu-id="689ec-169">Die folgenden Änderungen wurden am Codegerüst vorgenommen:</span><span class="sxs-lookup"><span data-stu-id="689ec-169">The following changes have been made to the scaffolded code:</span></span>

* <span data-ttu-id="689ec-170">Die Überschrift wurde von „Index“ in „Kurse“ geändert.</span><span class="sxs-lookup"><span data-stu-id="689ec-170">Changed the heading from Index to Courses.</span></span>
* <span data-ttu-id="689ec-171">Die Spalte **Anzahl** wurde hinzugefügt. Sie zeigt den `CourseID`-Eigenschaftswert an.</span><span class="sxs-lookup"><span data-stu-id="689ec-171">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="689ec-172">Primärschlüssel werden nicht standardmäßig eingerüstet, da sie normalerweise ohne Bedeutung für Endbenutzer sind.</span><span class="sxs-lookup"><span data-stu-id="689ec-172">By default, primary keys aren't scaffolded because normally they're meaningless to end users.</span></span> <span data-ttu-id="689ec-173">Allerdings hat der Primärschlüssel in diesem Fall jedoch Bedeutung.</span><span class="sxs-lookup"><span data-stu-id="689ec-173">However, in this case the primary key is meaningful.</span></span>
* <span data-ttu-id="689ec-174">Die Spalte **Abteilung** wurde geändert, sodass sie jetzt den Namen der Abteilung anzeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-174">Changed the **Department** column to display the department name.</span></span> <span data-ttu-id="689ec-175">Der Code zeigt die `Name`-Eigenschaft der `Department`-Entität an, die in die `Department`-Navigationseigenschaft geladen wird:</span><span class="sxs-lookup"><span data-stu-id="689ec-175">The code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

<span data-ttu-id="689ec-176">Führen Sie die Anwendung aus. Wählen Sie die Registerkarte **Kurse** aus, um die Liste mit den Abteilungsnamen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="689ec-176">Run the app and select the **Courses** tab to see the list with department names.</span></span>

![Indexseite „Kurse“](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a><span data-ttu-id="689ec-178">Laden verwandter Daten mit „Select“</span><span class="sxs-lookup"><span data-stu-id="689ec-178">Loading related data with Select</span></span>

<span data-ttu-id="689ec-179">Die `OnGetAsync`-Methode lädt verwandte Daten mit der `Include`-Methode:</span><span class="sxs-lookup"><span data-stu-id="689ec-179">The `OnGetAsync` method loads related data with the `Include` method:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="689ec-180">Der `Select`-Operator lädt nur die erforderlichen verwandten Daten.</span><span class="sxs-lookup"><span data-stu-id="689ec-180">The `Select` operator loads only the related data needed.</span></span> <span data-ttu-id="689ec-181">Für die einzelnen Elemente wie `Department.Name` wird ein INNER JOIN von SQL verwendet.</span><span class="sxs-lookup"><span data-stu-id="689ec-181">For single items, like the `Department.Name` it uses a SQL INNER JOIN.</span></span> <span data-ttu-id="689ec-182">Für Sammlungen wird ein anderer Zugriff auf die Datenbank verwendet, aber Gleiches gilt für den `Include`-Operator für Sammlungen.</span><span class="sxs-lookup"><span data-stu-id="689ec-182">For collections, it uses another database access, but so does the `Include` operator on collections.</span></span>

<span data-ttu-id="689ec-183">Der folgende Code lädt verwandte Daten mit der `Select`-Methode:</span><span class="sxs-lookup"><span data-stu-id="689ec-183">The following code loads related data with the `Select` method:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="689ec-184">Die `CourseViewModel`:</span><span class="sxs-lookup"><span data-stu-id="689ec-184">The `CourseViewModel`:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

<span data-ttu-id="689ec-185">Ein vollständiges Beispiel finden Sie unter [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) und [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs).</span><span class="sxs-lookup"><span data-stu-id="689ec-185">See [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) and [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) for a complete example.</span></span>

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="689ec-186">Erstellen einer Dozentenseite, die Kurse und Registrierungen anzeigt</span><span class="sxs-lookup"><span data-stu-id="689ec-186">Create an Instructors page that shows Courses and Enrollments</span></span>

<span data-ttu-id="689ec-187">In diesem Abschnitt wird die Dozentenseite erstellt.</span><span class="sxs-lookup"><span data-stu-id="689ec-187">In this section, the Instructors page is created.</span></span>

<a name="IP"></a>
<span data-ttu-id="689ec-188">![Indexseite „Dozenten“](read-related-data/_static/instructors-index.png)</span><span class="sxs-lookup"><span data-stu-id="689ec-188">![Instructors Index page](read-related-data/_static/instructors-index.png)</span></span>

<span data-ttu-id="689ec-189">Auf dieser Seite werden verwandte Daten auf folgende Weise gelesen und angezeigt:</span><span class="sxs-lookup"><span data-stu-id="689ec-189">This page reads and displays related data in the following ways:</span></span>

* <span data-ttu-id="689ec-190">Die Liste der Dozenten zeigt verwandte Daten aus der `OfficeAssignment`-Entität (Office in der vorherigen Abbildung).</span><span class="sxs-lookup"><span data-stu-id="689ec-190">The list of instructors displays related data from the `OfficeAssignment` entity (Office in the preceding image).</span></span> <span data-ttu-id="689ec-191">Die `Instructor`- und `OfficeAssignment`-Entitäten stehen in einer 1:0..1-Beziehung zueinander.</span><span class="sxs-lookup"><span data-stu-id="689ec-191">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="689ec-192">Eager Loading wird für die `OfficeAssignment`-Entitäten verwendet.</span><span class="sxs-lookup"><span data-stu-id="689ec-192">Eager loading is used for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="689ec-193">Eager Loading ist in der Regel effizienter, wenn die verwandten Daten angezeigt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="689ec-193">Eager loading is typically more efficient when the related data needs to be displayed.</span></span> <span data-ttu-id="689ec-194">In diesem Fall werden die Office-Zuweisungen für die Dozenten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-194">In this case, office assignments for the instructors are displayed.</span></span>
* <span data-ttu-id="689ec-195">Wenn der Benutzer einen Dozenten auswählt (Harui in der vorherigen Abbildung), werden verwandte `Course`-Entitäten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-195">When the user selects an instructor (Harui in the preceding image), related `Course` entities are displayed.</span></span> <span data-ttu-id="689ec-196">Die `Instructor`- und `Course`-Entitäten stehen in einer m:n-Beziehung zueinander.</span><span class="sxs-lookup"><span data-stu-id="689ec-196">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="689ec-197">Für die `Course`-Entitäten und ihre verwandten `Department`-Entitäten wird das Eager Loading verwendet.</span><span class="sxs-lookup"><span data-stu-id="689ec-197">Eager loading is used for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="689ec-198">In diesem Fall können separate Abfragen effizienter sein, da nur Kurse für den ausgewählten Dozenten benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-198">In this case, separate queries might be more efficient because only courses for the selected instructor are needed.</span></span> <span data-ttu-id="689ec-199">Dieses Beispiel zeigt, wie Eager Loading für Navigationseigenschaften in Entitäten in den Navigationseigenschaften verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="689ec-199">This example shows how to use eager loading for navigation properties in entities that are in navigation properties.</span></span>
* <span data-ttu-id="689ec-200">Wenn der Benutzer einen Kurs auswählt (Chemie in der vorherigen Abbildung), werden verwandte Daten aus der `Enrollments`-Entität angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-200">When the user selects a course (Chemistry in the preceding image), related data from the `Enrollments` entity is displayed.</span></span> <span data-ttu-id="689ec-201">In der vorherigen Abbildung sind der Name des Studenten und die Note angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-201">In the preceding image, student name and grade are displayed.</span></span> <span data-ttu-id="689ec-202">Die `Course`- und `Enrollment`-Entitäten stehen in einer 1:n-Beziehung zueinander.</span><span class="sxs-lookup"><span data-stu-id="689ec-202">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="689ec-203">Erstellen eines Ansichtsmodells für die Indexansicht „Dozenten“</span><span class="sxs-lookup"><span data-stu-id="689ec-203">Create a view model for the Instructor Index view</span></span>

<span data-ttu-id="689ec-204">Die Dozentenseite zeigt Daten aus drei verschiedenen Tabellen.</span><span class="sxs-lookup"><span data-stu-id="689ec-204">The instructors page shows data from three different tables.</span></span> <span data-ttu-id="689ec-205">Es wird ein Ansichtsmodell erstellt, das die drei Entitäten enthält, die die drei Tabellen darstellen.</span><span class="sxs-lookup"><span data-stu-id="689ec-205">A view model is created that includes the three entities representing the three tables.</span></span>

<span data-ttu-id="689ec-206">Erstellen Sie im Ordner *SchoolViewModels* die Datei *InstructorIndexData.cs* mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-206">In the *SchoolViewModels* folder, create *InstructorIndexData.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a><span data-ttu-id="689ec-207">Gerüstbau für das Dozentenmodell</span><span class="sxs-lookup"><span data-stu-id="689ec-207">Scaffold the Instructor model</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="689ec-208">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="689ec-208">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="689ec-209">Führen Sie die Schritte unter [Erstellen des Gerüsts für das Studentenmodell](xref:data/ef-rp/intro#scaffold-the-student-model) aus, und verwenden Sie `Instructor` für die Modellklasse.</span><span class="sxs-lookup"><span data-stu-id="689ec-209">Follow the instructions in [Scaffold the student model](xref:data/ef-rp/intro#scaffold-the-student-model) and use `Instructor` for the model class.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="689ec-210">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="689ec-210">.NET Core CLI</span></span>](#tab/netcore-cli)

 <span data-ttu-id="689ec-211">Führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="689ec-211">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
  ```

------

<span data-ttu-id="689ec-212">Der vorherige Befehl erstellt ein Gerüst für das `Instructor`-Modell.</span><span class="sxs-lookup"><span data-stu-id="689ec-212">The preceding command scaffolds the `Instructor` model.</span></span> <span data-ttu-id="689ec-213">Führen Sie die Anwendung aus, und navigieren Sie zur Dozentenseite.</span><span class="sxs-lookup"><span data-stu-id="689ec-213">Run the app and navigate to the instructors page.</span></span>

<span data-ttu-id="689ec-214">Ersetzen Sie *Pages/Instructors/Index.cshtml.cs* durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-214">Replace *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,18-99)]

<span data-ttu-id="689ec-215">Die `OnGetAsync`-Methode akzeptiert optional Routendaten für die ID des ausgewählten Dozenten.</span><span class="sxs-lookup"><span data-stu-id="689ec-215">The `OnGetAsync` method accepts optional route data for the ID of the selected instructor.</span></span>

<span data-ttu-id="689ec-216">Untersuchen Sie die Abfrage in der Datei *Pages/Instructors/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="689ec-216">Examine the query in the *Pages/Instructors/Index.cshtml.cs* file:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="689ec-217">Die Abfrage enthält zwei Dinge:</span><span class="sxs-lookup"><span data-stu-id="689ec-217">The query has two includes:</span></span>

* <span data-ttu-id="689ec-218">`OfficeAssignment`: In der [Dozentenansicht](#IP) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-218">`OfficeAssignment`: Displayed in the [instructors view](#IP).</span></span>
* <span data-ttu-id="689ec-219">`CourseAssignments`: Welche Kurse gegeben werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-219">`CourseAssignments`: Which brings in the courses taught.</span></span>


### <a name="update-the-instructors-index-page"></a><span data-ttu-id="689ec-220">Aktualisieren der Indexseite „Dozenten“</span><span class="sxs-lookup"><span data-stu-id="689ec-220">Update the instructors Index page</span></span>

<span data-ttu-id="689ec-221">Aktualisieren Sie *Pages/Instructors/Index.cshtml* mit folgendem Markup:</span><span class="sxs-lookup"><span data-stu-id="689ec-221">Update *Pages/Instructors/Index.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

<span data-ttu-id="689ec-222">Das oben stehende Markup führt die folgenden Änderungen durch:</span><span class="sxs-lookup"><span data-stu-id="689ec-222">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="689ec-223">Aktualisiert die `page`-Anweisung von `@page` auf `@page "{id:int?}"`.</span><span class="sxs-lookup"><span data-stu-id="689ec-223">Updates the `page` directive from `@page` to `@page "{id:int?}"`.</span></span> <span data-ttu-id="689ec-224">`"{id:int?}"` ist eine Routenvorlage.</span><span class="sxs-lookup"><span data-stu-id="689ec-224">`"{id:int?}"` is a route template.</span></span> <span data-ttu-id="689ec-225">Die Routenvorlage ändert ganzzahlige Abfragezeichenfolgen in der URL in Routendaten.</span><span class="sxs-lookup"><span data-stu-id="689ec-225">The route template changes integer query strings in the URL to route data.</span></span> <span data-ttu-id="689ec-226">Klicken Sie beispielsweise auf den Link **Auswählen** für einen Dozenten, wenn nur die `@page`-Anweisung eine URL wie die folgende erzeugt:</span><span class="sxs-lookup"><span data-stu-id="689ec-226">For example, clicking on the **Select** link for an instructor with only the `@page` directive produces a URL like the following:</span></span>

    `http://localhost:1234/Instructors?id=2`

    <span data-ttu-id="689ec-227">Wenn die Seitenanweisung `@page "{id:int?}"` ist, sieht die vorherige URL wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="689ec-227">When the page directive is `@page "{id:int?}"`, the previous URL is:</span></span>

    `http://localhost:1234/Instructors/2`

* <span data-ttu-id="689ec-228">Der Seitentitel lautet **Dozenten**.</span><span class="sxs-lookup"><span data-stu-id="689ec-228">Page title is **Instructors**.</span></span>
* <span data-ttu-id="689ec-229">Es wurde eine **Office**-Spalte hinzugefügt, die `item.OfficeAssignment.Location` nur anzeigt, wenn `item.OfficeAssignment` nicht gleich 0 (null) ist.</span><span class="sxs-lookup"><span data-stu-id="689ec-229">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` isn't null.</span></span> <span data-ttu-id="689ec-230">Da dies eine 1:0..1-Beziehung ist, gibt es möglicherweise keine verwandte OfficeAssignment-Entität.</span><span class="sxs-lookup"><span data-stu-id="689ec-230">Because this is a one-to-zero-or-one relationship, there might not be a related OfficeAssignment entity.</span></span>

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* <span data-ttu-id="689ec-231">Es wurde eine **Kurse**-Spalte hinzugefügt, die die Kurse eines jeden Dozenten anzeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-231">Added a **Courses** column that displays courses taught by each instructor.</span></span> <span data-ttu-id="689ec-232">Weitere Informationen über diese Razor-Syntax finden Sie unter [Explizite Zeilenübergänge mit `@:`](xref:mvc/views/razor#explicit-line-transition-with-).</span><span class="sxs-lookup"><span data-stu-id="689ec-232">See [Explicit Line Transition with `@:`](xref:mvc/views/razor#explicit-line-transition-with-) for more about this razor syntax.</span></span>

* <span data-ttu-id="689ec-233">Es wurde Code hinzugefügt, der `class="success"` dynamisch zum `tr`-Element des ausgewählten Dozenten hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="689ec-233">Added code that dynamically adds `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="689ec-234">Hiermit wird eine Hintergrundfarbe mit einer Bootstrapklasse für die ausgewählte Zeile hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="689ec-234">This sets a background color for the selected row using a Bootstrap class.</span></span>

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* <span data-ttu-id="689ec-235">Es wurde ein neuer Link mit der Bezeichnung **Auswählen** hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="689ec-235">Added a new hyperlink labeled **Select**.</span></span> <span data-ttu-id="689ec-236">Dieser Link sendet die ID des ausgewählten Dozenten an die `Index`-Methode und legt die Hintergrundfarbe fest.</span><span class="sxs-lookup"><span data-stu-id="689ec-236">This link sends the selected instructor's ID to the `Index` method and sets a background color.</span></span>

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

<span data-ttu-id="689ec-237">Führen Sie die Anwendung aus. Klicken Sie auf die Registerkarte **Dozenten**. Die Seite zeigt den `Location` (Office) aus der verwandten `OfficeAssignment`-Entität an.</span><span class="sxs-lookup"><span data-stu-id="689ec-237">Run the app and select the **Instructors** tab. The page displays the `Location` (office) from the related `OfficeAssignment` entity.</span></span> <span data-ttu-id="689ec-238">Wenn OfficeAssignment gleich ist 0 (null), wird eine leere Tabellenzelle angezeigt.</span><span class="sxs-lookup"><span data-stu-id="689ec-238">If OfficeAssignment\` is null, an empty table cell is displayed.</span></span>

![Indexseite „Dozenten“, nichts ausgewählt](read-related-data/_static/instructors-index-no-selection.png)

<span data-ttu-id="689ec-240">Klicken Sie auf den Link **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="689ec-240">Click on the **Select** link.</span></span> <span data-ttu-id="689ec-241">Der Zeilenstil verändert sich.</span><span class="sxs-lookup"><span data-stu-id="689ec-241">The row style changes.</span></span>

### <a name="add-courses-taught-by-selected-instructor"></a><span data-ttu-id="689ec-242">Hinzufügen von Kursen eines ausgewählten Dozenten</span><span class="sxs-lookup"><span data-stu-id="689ec-242">Add courses taught by selected instructor</span></span>

<span data-ttu-id="689ec-243">Aktualisieren Sie die `OnGetAsync`-Methode in *Pages/Instructors/Index.cshtml.cs* mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-243">Update the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-999)]

<span data-ttu-id="689ec-244">Fügen Sie `public int CourseID { get; set; }` hinzu.</span><span class="sxs-lookup"><span data-stu-id="689ec-244">Add `public int CourseID { get; set; }`</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_1&highlight=12)]

<span data-ttu-id="689ec-245">Überprüfen Sie die aktualisierte Abfrage:</span><span class="sxs-lookup"><span data-stu-id="689ec-245">Examine the updated query:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="689ec-246">Die vorhergehende Abfrage fügt die `Department`-Entitäten hinzu.</span><span class="sxs-lookup"><span data-stu-id="689ec-246">The preceding query adds the `Department` entities.</span></span>

<span data-ttu-id="689ec-247">Der folgende Code wird ausgeführt, wenn ein Dozent ausgewählt wird (`id != null`).</span><span class="sxs-lookup"><span data-stu-id="689ec-247">The following code executes when an instructor is selected (`id != null`).</span></span> <span data-ttu-id="689ec-248">Der ausgewählte Dozent wird aus der Liste der Dozenten im Ansichtsmodell abgerufen.</span><span class="sxs-lookup"><span data-stu-id="689ec-248">The selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="689ec-249">Die `Courses`-Eigenschaft des Ansichtsmodells wird mit den `Course`-Entitäten aus der `CourseAssignments`-Navigationseigenschaft dieses Dozenten geladen.</span><span class="sxs-lookup"><span data-stu-id="689ec-249">The view model's `Courses` property is loaded with the `Course` entities from that instructor's `CourseAssignments` navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

<span data-ttu-id="689ec-250">Die `Where`-Methode gibt eine Sammlung zurück.</span><span class="sxs-lookup"><span data-stu-id="689ec-250">The `Where` method returns a collection.</span></span> <span data-ttu-id="689ec-251">In der vorherigen `Where`-Methode wird nur eine einzige `Instructor`-Entität zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="689ec-251">In the preceding `Where` method, only a single `Instructor` entity is returned.</span></span> <span data-ttu-id="689ec-252">Die `Single`-Methode konvertiert die Sammlung in eine einzelne `Instructor`-Entität.</span><span class="sxs-lookup"><span data-stu-id="689ec-252">The `Single` method converts the collection into a single `Instructor` entity.</span></span> <span data-ttu-id="689ec-253">Die `Instructor`-Entität ermöglicht Zugriff auf die `CourseAssignments`-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="689ec-253">The `Instructor` entity provides access to the `CourseAssignments` property.</span></span> <span data-ttu-id="689ec-254">`CourseAssignments` ermöglicht Zugriff auf die verwandten `Course`-Entitäten.</span><span class="sxs-lookup"><span data-stu-id="689ec-254">`CourseAssignments` provides access to the related `Course` entities.</span></span>

![Dozent:Kurse m:N](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="689ec-256">Die `Single`-Methode wird für eine Sammlung verwendet, wenn die Sammlung nur ein Element aufweist.</span><span class="sxs-lookup"><span data-stu-id="689ec-256">The `Single` method is used on a collection when the collection has only one item.</span></span> <span data-ttu-id="689ec-257">Die `Single`-Methode löst eine Ausnahme aus, wenn die Sammlung leer ist oder mehr als ein Element vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="689ec-257">The `Single` method throws an exception if the collection is empty or if there's more than one item.</span></span> <span data-ttu-id="689ec-258">Eine Alternative ist `SingleOrDefault`, womit ein Standardwert (in diesem Fall 0 (null)) zurückgegeben wird, wenn die Sammlung leer ist.</span><span class="sxs-lookup"><span data-stu-id="689ec-258">An alternative is `SingleOrDefault`, which returns a default value (null in this case) if the collection is empty.</span></span> <span data-ttu-id="689ec-259">Für eine leere Sammlung wird `SingleOrDefault` verwendet:</span><span class="sxs-lookup"><span data-stu-id="689ec-259">Using `SingleOrDefault` on an empty collection:</span></span>

* <span data-ttu-id="689ec-260">Löst eine Ausnahme aus (auf der Suche nach einer `Courses`-Eigenschaft eines Nullverweises).</span><span class="sxs-lookup"><span data-stu-id="689ec-260">Results in an exception (from trying to find a `Courses` property on a null reference).</span></span>
* <span data-ttu-id="689ec-261">Die Ausnahmemeldung würde die Ursache des Problems weniger deutlich angeben.</span><span class="sxs-lookup"><span data-stu-id="689ec-261">The exception message would less clearly indicate the cause of the problem.</span></span>

<span data-ttu-id="689ec-262">Wenn ein Kurs ausgewählt ist, füllt der folgende Code die `Enrollments`-Eigenschaft des Ansichtsmodells:</span><span class="sxs-lookup"><span data-stu-id="689ec-262">The following code populates the view model's `Enrollments` property when a course is selected:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

<span data-ttu-id="689ec-263">Fügen Sie das folgende Markup zum Ende der Razor-Seite *Pages/Instructors/Index.cshtml* hinzu:</span><span class="sxs-lookup"><span data-stu-id="689ec-263">Add the following markup to the end of the *Pages/Instructors/Index.cshtml* Razor Page:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-999)]

<span data-ttu-id="689ec-264">Das vorhergehende Markup zeigt eine Liste der Kurse eines bestimmten Dozenten an, wenn einer ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="689ec-264">The preceding markup displays a list of courses related to an instructor when an instructor is selected.</span></span>

<span data-ttu-id="689ec-265">Testen Sie die App.</span><span class="sxs-lookup"><span data-stu-id="689ec-265">Test the app.</span></span> <span data-ttu-id="689ec-266">Klicken Sie auf den Link **Auswählen** auf der Dozentenseite.</span><span class="sxs-lookup"><span data-stu-id="689ec-266">Click on a **Select** link on the instructors page.</span></span>

![Indexseite „Dozenten“, Dozent ausgewählt](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a><span data-ttu-id="689ec-268">Anzeigen der Studentendaten</span><span class="sxs-lookup"><span data-stu-id="689ec-268">Show student data</span></span>

<span data-ttu-id="689ec-269">In diesem Abschnitt wird die Anwendung aktualisiert, um die Studentendaten für einen ausgewählten Kurs anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="689ec-269">In this section, the app is updated to show the student data for a selected course.</span></span>

<span data-ttu-id="689ec-270">Aktualisieren Sie die Abfrage in der `OnGetAsync`-Methode in *Pages/Instructors/Index.cshtml.cs* mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-270">Update the query in the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="689ec-271">Aktualisieren Sie *Pages/Instructors/Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="689ec-271">Update *Pages/Instructors/Index.cshtml*.</span></span> <span data-ttu-id="689ec-272">Fügen Sie dem Dateiende das folgende Markup hinzu:</span><span class="sxs-lookup"><span data-stu-id="689ec-272">Add the following markup to the end of the file:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

<span data-ttu-id="689ec-273">Das vorhergehende Markup zeigt eine Liste der Studenten, die im ausgewählten Kurs registriert sind.</span><span class="sxs-lookup"><span data-stu-id="689ec-273">The preceding markup displays a list of the students who are enrolled in the selected course.</span></span>

<span data-ttu-id="689ec-274">Aktualisieren Sie die Seite. Wählen Sie einen Dozenten aus.</span><span class="sxs-lookup"><span data-stu-id="689ec-274">Refresh the page and select an instructor.</span></span> <span data-ttu-id="689ec-275">Wählen Sie einen Kurs aus, um die Liste der registrierten Studenten und deren Noten einzusehen.</span><span class="sxs-lookup"><span data-stu-id="689ec-275">Select a course to see the list of enrolled students and their grades.</span></span>

![Indexseite „Dozenten“, Dozent und Kurs ausgewählt](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a><span data-ttu-id="689ec-277">Verwenden von „Single“</span><span class="sxs-lookup"><span data-stu-id="689ec-277">Using Single</span></span>

<span data-ttu-id="689ec-278">Die `Single`-Methode kann die `Where`-Bedingung übergehen, anstatt die `Where`-Methode separat aufzurufen:</span><span class="sxs-lookup"><span data-stu-id="689ec-278">The `Single` method can pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21-22,30-31)]

<span data-ttu-id="689ec-279">Der vorangehende `Single`-Ansatz bietet keine Vorteile gegenüber `Where`.</span><span class="sxs-lookup"><span data-stu-id="689ec-279">The preceding `Single` approach provides no benefits over using `Where`.</span></span> <span data-ttu-id="689ec-280">Einige Entwickler bevorzugen einfach den `Single`-Ansatz.</span><span class="sxs-lookup"><span data-stu-id="689ec-280">Some developers prefer the `Single` approach style.</span></span>

## <a name="explicit-loading"></a><span data-ttu-id="689ec-281">Explizites Laden</span><span class="sxs-lookup"><span data-stu-id="689ec-281">Explicit loading</span></span>

<span data-ttu-id="689ec-282">Der aktuelle Code gibt Eager Loading für `Enrollments` und `Students` an:</span><span class="sxs-lookup"><span data-stu-id="689ec-282">The current code specifies eager loading for `Enrollments` and `Students`:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="689ec-283">Angenommen, Benutzer möchten Registrierungen für einen Kurs nur selten anzeigen lassen.</span><span class="sxs-lookup"><span data-stu-id="689ec-283">Suppose users rarely want to see enrollments in a course.</span></span> <span data-ttu-id="689ec-284">In diesem Fall wäre es eine Optimierung, die Registrierungsdaten nur dann zu laden, wenn diese angefordert werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-284">In that case, an optimization would be to only load the enrollment data if it's requested.</span></span> <span data-ttu-id="689ec-285">In diesem Abschnitt wird die `OnGetAsync` aktualisiert, um das explizite Laden von `Enrollments` und `Students` zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="689ec-285">In this section, the `OnGetAsync` is updated to use explicit loading of `Enrollments` and `Students`.</span></span>

<span data-ttu-id="689ec-286">Aktualisieren Sie `OnGetAsync` mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="689ec-286">Update the `OnGetAsync` with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

<span data-ttu-id="689ec-287">Der vorangehende Code löscht die *ThenInclude*-Methodenaufrufe für Registrierung und Studentendaten.</span><span class="sxs-lookup"><span data-stu-id="689ec-287">The preceding code drops the *ThenInclude* method calls for enrollment and student data.</span></span> <span data-ttu-id="689ec-288">Wenn ein Kurs ausgewählt ist, ruft der hervorgehobene Code Folgendes ab:</span><span class="sxs-lookup"><span data-stu-id="689ec-288">If a course is selected, the highlighted code retrieves:</span></span>

* <span data-ttu-id="689ec-289">Die `Enrollment`-Entitäten für den ausgewählten Kurs.</span><span class="sxs-lookup"><span data-stu-id="689ec-289">The `Enrollment` entities for the selected course.</span></span>
* <span data-ttu-id="689ec-290">Die `Student`-Entitäten für jede `Enrollment`.</span><span class="sxs-lookup"><span data-stu-id="689ec-290">The `Student` entities for each `Enrollment`.</span></span>

<span data-ttu-id="689ec-291">Beachten Sie, dass der vorherige Code `.AsNoTracking()` auskommentiert.</span><span class="sxs-lookup"><span data-stu-id="689ec-291">Notice the preceding code comments out `.AsNoTracking()`.</span></span> <span data-ttu-id="689ec-292">Navigationseigenschaften können nur für nachverfolgte Entitäten explizit geladen werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-292">Navigation properties can only be explicitly loaded for tracked entities.</span></span>

<span data-ttu-id="689ec-293">Testen Sie die App.</span><span class="sxs-lookup"><span data-stu-id="689ec-293">Test the app.</span></span> <span data-ttu-id="689ec-294">Aus Benutzersicht verhält sich die Anwendung identisch mit der vorherigen Version.</span><span class="sxs-lookup"><span data-stu-id="689ec-294">From a users perspective, the app behaves identically to the previous version.</span></span>

<span data-ttu-id="689ec-295">Das nächste Tutorial zeigt, wie verwandte Daten aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="689ec-295">The next tutorial shows how to update related data.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="689ec-296">[Zurück](xref:data/ef-rp/complex-data-model)
>[Weiter](xref:data/ef-rp/update-related-data)</span><span class="sxs-lookup"><span data-stu-id="689ec-296">[Previous](xref:data/ef-rp/complex-data-model)
[Next](xref:data/ef-rp/update-related-data)</span></span>
