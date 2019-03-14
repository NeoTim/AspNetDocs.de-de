---
title: Hinzufügen eines neuen Felds zu einer Razor-Seite in ASP.NET Core
author: rick-anderson
description: Veranschaulicht das Hinzufügen ein neues Felds zu einer Razor Page mit Entity Framework Core
ms.author: riande
ms.custom: mvc
ms.date: 12/5/2018
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: 98de39c63c992dce7d60563df316d848339b811a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050417"
---
# <a name="add-a-new-field-to-a-razor-page-in-aspnet-core"></a><span data-ttu-id="d3089-103">Hinzufügen eines neuen Felds zu einer Razor-Seite in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d3089-103">Add a new field to a Razor Page in ASP.NET Core</span></span>

<span data-ttu-id="d3089-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d3089-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="d3089-105">In diesem Abschnitt werden [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First-Migrationen für folgende Zwecke verwendet:</span><span class="sxs-lookup"><span data-stu-id="d3089-105">In this section [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First Migrations is used to:</span></span>

* <span data-ttu-id="d3089-106">Dem Modell wird ein neues Feld hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d3089-106">Add a new field to the model.</span></span>
* <span data-ttu-id="d3089-107">Die neue Änderung am Feldschema wird in die Datenbank migriert.</span><span class="sxs-lookup"><span data-stu-id="d3089-107">Migrate the new field schema change to the database.</span></span>

<span data-ttu-id="d3089-108">Bei der Verwendung von EF Code First für die automatische Erstellung einer Datenbank geht Code First wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="d3089-108">When using EF Code First to automatically create a database, Code First:</span></span>

* <span data-ttu-id="d3089-109">Es fügt eine Tabelle zur Datenbank hinzu, um nachzuverfolgen, ob das Schema der Datenbank mit den Modellklassen synchron ist, aus denen sie generiert wurde.</span><span class="sxs-lookup"><span data-stu-id="d3089-109">Adds a table to the database to track whether the schema of the database is in sync with the model classes it was generated from.</span></span>
* <span data-ttu-id="d3089-110">Wenn die Datenbank mit den Modellklassen nicht synchron ist, löst EF eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="d3089-110">If the model classes aren't in sync with the DB, EF throws an exception.</span></span>

<span data-ttu-id="d3089-111">Durch die automatische Überprüfung, ob das Schema und das Modell synchron sind, können Probleme inkonsistenter Datenbanken/Codes leichter ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="d3089-111">Automatic verification of schema/model in sync makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="d3089-112">Hinzufügen einer Rating-Eigenschaft zum Movie-Modell</span><span class="sxs-lookup"><span data-stu-id="d3089-112">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="d3089-113">Öffnen Sie die Datei *Models/Movie.cs*, und fügen Sie eine `Rating`-Eigenschaft hinzu:</span><span class="sxs-lookup"><span data-stu-id="d3089-113">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

<span data-ttu-id="d3089-114">Erstellen Sie die App.</span><span class="sxs-lookup"><span data-stu-id="d3089-114">Build the app.</span></span>

<span data-ttu-id="d3089-115">Bearbeiten Sie *Pages/Movies/Index.cshtml*, und fügen ein `Rating`-Feld hinzu:</span><span class="sxs-lookup"><span data-stu-id="d3089-115">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexRating.cshtml.?highlight=40-42,61-63)]

<span data-ttu-id="d3089-116">Aktualisieren Sie die folgenden Seiten:</span><span class="sxs-lookup"><span data-stu-id="d3089-116">Update the following pages:</span></span>

* <span data-ttu-id="d3089-117">Fügen Sie das `Rating`-Feld zu den Seiten „Delete“ und „Details“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="d3089-117">Add the `Rating` field to the Delete and Details pages.</span></span>
* <span data-ttu-id="d3089-118">Aktualisieren Sie die Datei [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml) mit einem `Rating`-Feld.</span><span class="sxs-lookup"><span data-stu-id="d3089-118">Update [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml) with a `Rating` field.</span></span>
* <span data-ttu-id="d3089-119">Fügen Sie das Feld `Rating` der Bearbeitungsseite hinzu.</span><span class="sxs-lookup"><span data-stu-id="d3089-119">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="d3089-120">Die App funktioniert erst, nachdem die Datenbank mit dem neuen Feld aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="d3089-120">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="d3089-121">Wenn sie jetzt ausgeführt wird, löst die App eine `SqlException` aus:</span><span class="sxs-lookup"><span data-stu-id="d3089-121">If run now, the app throws a `SqlException`:</span></span>

`SqlException: Invalid column name 'Rating'.`

<span data-ttu-id="d3089-122">Dieser Fehler wird dadurch verursacht, dass sich die aktualisierte Modellklasse „Movie“ vom Schema der Tabelle „Movie“ der Datenbank unterscheidet.</span><span class="sxs-lookup"><span data-stu-id="d3089-122">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="d3089-123">(Die Datenbanktabelle enthält nicht die Spalte `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="d3089-123">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="d3089-124">Es gibt mehrere Vorgehensweisen zum Beheben des Fehlers:</span><span class="sxs-lookup"><span data-stu-id="d3089-124">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="d3089-125">Lassen Sie die Datenbank von Entity Framework automatisch löschen und mit dem neuen Modellklassenschema neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d3089-125">Have the Entity Framework automatically drop and re-create the database using the new model class schema.</span></span> <span data-ttu-id="d3089-126">Dieser Ansatz ist früh im Entwicklungszyklus sehr praktisch. Er ermöglicht Ihnen, das Modell und das Datenbankschema schnell gemeinsam weiterzuentwickeln.</span><span class="sxs-lookup"><span data-stu-id="d3089-126">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="d3089-127">Der Nachteil ist, dass in der Datenbank vorhandene Daten verloren gehen.</span><span class="sxs-lookup"><span data-stu-id="d3089-127">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="d3089-128">Verwenden Sie diesen Ansatz nicht in einer Produktionsdatenbank!</span><span class="sxs-lookup"><span data-stu-id="d3089-128">Don't use this approach on a production database!</span></span> <span data-ttu-id="d3089-129">Das Löschen der Datenbank bei Schemaänderungen und das Verwenden eines Initialisierers zum automatischen Ausführen eines Seedings für eine Datenbank mit Testdaten ist häufig eine produktive Möglichkeit zum Entwickeln einer App.</span><span class="sxs-lookup"><span data-stu-id="d3089-129">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="d3089-130">Ändern Sie das Schema der vorhandenen Datenbank explizit so, dass es mit den Modellklassen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="d3089-130">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="d3089-131">Der Vorteil dieses Ansatzes ist, dass Sie Ihre Daten behalten.</span><span class="sxs-lookup"><span data-stu-id="d3089-131">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="d3089-132">Sie können diese Änderung entweder manuell oder durch Erstellen eines Änderungsskripts für die Datenbank vornehmen.</span><span class="sxs-lookup"><span data-stu-id="d3089-132">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="d3089-133">Verwenden Sie Code First-Migrationen, um das Datenbankschema zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="d3089-133">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="d3089-134">Verwenden Sie für dieses Tutorial Code First-Migrationen.</span><span class="sxs-lookup"><span data-stu-id="d3089-134">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="d3089-135">Aktualisieren Sie die `SeedData`-Klasse so, dass sie einen Wert für die neue Spalte bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="d3089-135">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="d3089-136">Eine Beispieländerung ist nachstehend gezeigt, aber Sie sollten diese Änderung für jeden `new Movie`-Block vornehmen.</span><span class="sxs-lookup"><span data-stu-id="d3089-136">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

<span data-ttu-id="d3089-137">Sehen Sie sich die [fertige SeedData.cs-Datei an](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs).</span><span class="sxs-lookup"><span data-stu-id="d3089-137">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="d3089-138">Erstellen Sie die Projektmappe.</span><span class="sxs-lookup"><span data-stu-id="d3089-138">Build the solution.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d3089-139">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3089-139">Visual Studio</span></span>](#tab/visual-studio)

<a name="pmc"></a>

### <a name="add-a-migration-for-the-rating-field"></a><span data-ttu-id="d3089-140">Hinzufügen einer Migration für das Bewertungsfeld</span><span class="sxs-lookup"><span data-stu-id="d3089-140">Add a migration for the rating field</span></span>

<span data-ttu-id="d3089-141">Öffnen Sie das Menü **Extras**. Wählen Sie dort **NuGet-Paket-Manager > Paket-Manager-Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="d3089-141">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="d3089-142">Geben Sie in der PMC die folgenden Befehle ein:</span><span class="sxs-lookup"><span data-stu-id="d3089-142">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="d3089-143">Der `Add-Migration`-Befehl weist das Framework an, Folgendes auszuführen:</span><span class="sxs-lookup"><span data-stu-id="d3089-143">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="d3089-144">Das `Movie`-Modell mit dem Schema der `Movie`-Datenbank vergleichen.</span><span class="sxs-lookup"><span data-stu-id="d3089-144">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="d3089-145">Code erstellen, um das Schema der Datenbank in das neue Modell zu migrieren.</span><span class="sxs-lookup"><span data-stu-id="d3089-145">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="d3089-146">Der Name „Rating“ ist beliebig und wird verwendet, um die Migrationsdatei zu benennen.</span><span class="sxs-lookup"><span data-stu-id="d3089-146">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="d3089-147">Es ist hilfreich, einen aussagekräftigen Namen für die Migrationsdatei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="d3089-147">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="d3089-148">Der `Update-Database`-Befehl weist das Framework an, die Schemaänderungen auf die Datenbank anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="d3089-148">The `Update-Database` command tells the framework to apply the schema changes to the database.</span></span>

<a name="ssox"></a>

<span data-ttu-id="d3089-149">Wenn Sie alle Datensätze aus der Datenbank löschen, führt der Initialisierer ein Seeding für die Datenbank aus und fügt das Feld `Rating` hinzu.</span><span class="sxs-lookup"><span data-stu-id="d3089-149">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="d3089-150">Dies ist über die Links „Löschen“ im Browser oder [SQL Server-Objekt-Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX) möglich.</span><span class="sxs-lookup"><span data-stu-id="d3089-150">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span>

<span data-ttu-id="d3089-151">Eine weitere Möglichkeit ist, die Datenbank zu löschen und Migrationen zu verwenden, um die Datenbank neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d3089-151">Another option is to delete the database and use migrations to re-create the database.</span></span> <span data-ttu-id="d3089-152">So löschen Sie die Datenbank in SSOX</span><span class="sxs-lookup"><span data-stu-id="d3089-152">To delete the database in SSOX:</span></span>

* <span data-ttu-id="d3089-153">Wählen Sie die Datenbank in SSOX aus.</span><span class="sxs-lookup"><span data-stu-id="d3089-153">Select the database in SSOX.</span></span>
* <span data-ttu-id="d3089-154">Klicken Sie mit der rechten Maustaste auf die Datenbank, und wählen Sie *Löschen* aus.</span><span class="sxs-lookup"><span data-stu-id="d3089-154">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="d3089-155">Aktivieren Sie **Vorhandene Verbindungen schließen**.</span><span class="sxs-lookup"><span data-stu-id="d3089-155">Check **Close existing connections**.</span></span>
* <span data-ttu-id="d3089-156">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3089-156">Select **OK**.</span></span>
* <span data-ttu-id="d3089-157">Aktualisieren Sie die Datenbank in [PMC](xref:tutorials/razor-pages/new-field#pmc):</span><span class="sxs-lookup"><span data-stu-id="d3089-157">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database:</span></span>

  ```powershell
  Update-Database
  ```

<!-- Code -------------------------->
# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="d3089-158">Visual Studio Code / Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="d3089-158">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<!-- copy/paste this tab to the next. Not worth an include  -->

<span data-ttu-id="d3089-159">Führen Sie die folgenden .NET Core-CLI-Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="d3089-159">Run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add Rating
dotnet ef database update
```

<span data-ttu-id="d3089-160">Der `ef migrations add`-Befehl weist das Framework an, Folgendes auszuführen:</span><span class="sxs-lookup"><span data-stu-id="d3089-160">The `ef migrations add` command tells the framework to:</span></span>

* <span data-ttu-id="d3089-161">Das `Movie`-Modell mit dem Schema der `Movie`-Datenbank vergleichen.</span><span class="sxs-lookup"><span data-stu-id="d3089-161">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="d3089-162">Code erstellen, um das Schema der Datenbank in das neue Modell zu migrieren.</span><span class="sxs-lookup"><span data-stu-id="d3089-162">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="d3089-163">Der Name „Rating“ ist beliebig und wird verwendet, um die Migrationsdatei zu benennen.</span><span class="sxs-lookup"><span data-stu-id="d3089-163">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="d3089-164">Es ist hilfreich, einen aussagekräftigen Namen für die Migrationsdatei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="d3089-164">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="d3089-165">Der `ef database update`-Befehl weist das Framework an, die Schemaänderungen auf die Datenbank anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="d3089-165">The `ef database update` command tells the framework to apply the schema changes to the database.</span></span>

<span data-ttu-id="d3089-166">Wenn Sie alle Datensätze aus der Datenbank löschen, führt der Initialisierer ein Seeding für die Datenbank aus und fügt das Feld `Rating` hinzu.</span><span class="sxs-lookup"><span data-stu-id="d3089-166">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="d3089-167">Dies ist über die „Löschen“-Links im Browser oder über ein SQLite-Tool möglich.</span><span class="sxs-lookup"><span data-stu-id="d3089-167">You can do this with the delete links in the browser or by using a SQLite tool.</span></span>

<span data-ttu-id="d3089-168">Eine weitere Möglichkeit ist, die Datenbank zu löschen und Migrationen zu verwenden, um die Datenbank neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d3089-168">Another option is to delete the database and use migrations to re-create the database.</span></span> <span data-ttu-id="d3089-169">Um die Datenbank zu löschen, löschen Sie die Datenbankdatei (*MvcMovie.db*).</span><span class="sxs-lookup"><span data-stu-id="d3089-169">To delete the database, delete the database file (*MvcMovie.db*).</span></span> <span data-ttu-id="d3089-170">Führen Sie dann den `ef database update`-Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="d3089-170">Then run the `ef database update` command:</span></span> 

```console
dotnet ef database update
```

> [!NOTE]
> <span data-ttu-id="d3089-171">Viele Schemaänderungsvorgänge werden vom EF Core SQLite-Anbieter nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d3089-171">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="d3089-172">Zum Beispiel wird Hinzufügen einer Spalten unterstützt, wogegen Entfernen einer Spalte nicht unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="d3089-172">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="d3089-173">Wenn Sie eine Migration hinzufügen, um eine Spalte zu entfernen, wird der `ef migrations add`-Befehl erfolgreich ausgeführt, aber der `ef database update`-Befehl schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="d3089-173">If you add a migration to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="d3089-174">Sie können einige der Einschränkungen umgehen, indem Sie manuell Migrationscode schreiben, um eine Tabellenneuerstellung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="d3089-174">You can work around some of the limitations by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="d3089-175">Eine Tabellenneuerstellung umfasst Umbenennen der vorhandenen Tabelle, Erstellen einer neuen Tabelle, Kopieren von Daten in die neue Tabelle und Löschen der alten Tabelle.</span><span class="sxs-lookup"><span data-stu-id="d3089-175">A table rebuild involves renaming the existing table, creating a new table, copying data to the new table, and dropping the old table.</span></span> <span data-ttu-id="d3089-176">Weitere Informationen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="d3089-176">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="d3089-177">SQLite EF Core-Datenbank-Anbieter-Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="d3089-177">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="d3089-178">Anpassen des Migrationscodes</span><span class="sxs-lookup"><span data-stu-id="d3089-178">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="d3089-179">Datenseeding</span><span class="sxs-lookup"><span data-stu-id="d3089-179">Data seeding</span></span>](/ef/core/modeling/data-seeding)

---  
<!-- End of VS tabs -->

<span data-ttu-id="d3089-180">Führen Sie die App aus, und überprüfen Sie, ob Sie Filme mit dem Feld `Rating` erstellen/bearbeiten/anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="d3089-180">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="d3089-181">Wenn für die Datenbank kein Seed ausgeführt wird, legen Sie einen Haltepunkt in der `SeedData.Initialize`-Methode fest.</span><span class="sxs-lookup"><span data-stu-id="d3089-181">If the database isn't seeded, set a break point in the `SeedData.Initialize` method.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d3089-182">[Zurück: Hinzufügen der Suche](xref:tutorials/razor-pages/search)
> [Weiter: Hinzufügen der Validierung](xref:tutorials/razor-pages/validation)</span><span class="sxs-lookup"><span data-stu-id="d3089-182">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding Validation](xref:tutorials/razor-pages/validation)</span></span>
