---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036757"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="30b67-101">Hinzufügen eines neuen Felds zu einer ASP.NET Core MVC-App</span><span class="sxs-lookup"><span data-stu-id="30b67-101">Add a new field to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="30b67-102">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="30b67-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="30b67-103">In diesem Tutorial fügen Sie der Tabelle `Movies` ein neues Feld hinzu.</span><span class="sxs-lookup"><span data-stu-id="30b67-103">This tutorial will add a new field to the `Movies` table.</span></span> <span data-ttu-id="30b67-104">Wenn wir das Schema ändern (durch Hinzufügen eines neuen Felds), löschen wir die Datenbank und erstellen eine neue.</span><span class="sxs-lookup"><span data-stu-id="30b67-104">We'll drop the database and create a new one when we change the schema (add a new field).</span></span> <span data-ttu-id="30b67-105">Dieser Workflow funktioniert in der Frühphase der Entwicklung gut, wenn es noch keine aufzubewahrenden Produktionsdaten gibt.</span><span class="sxs-lookup"><span data-stu-id="30b67-105">This workflow works well early in development when we don't have any production data to perserve.</span></span>

<span data-ttu-id="30b67-106">Nachdem Ihre App bereitgestellt wurde und Sie über aufzubewahrende Daten verfügen, können Sie die Datenbank nicht löschen, wenn Sie das Schema ändern müssen.</span><span class="sxs-lookup"><span data-stu-id="30b67-106">Once your app is deployed and you have data that you need to perserve, you can't drop your DB when you need to change the schema.</span></span> <span data-ttu-id="30b67-107">Mithilfe von Entity Framework [Code First-Migrationen](/ef/core/get-started/aspnetcore/new-db) können Sie Ihr Schema aktualisieren und die Datenbank ohne Datenverlust migrieren.</span><span class="sxs-lookup"><span data-stu-id="30b67-107">Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) allows you to update your schema and migrate the database without losing data.</span></span> <span data-ttu-id="30b67-108">Migrationen sind bei Verwendung von SQL Server ein beliebtes Feature, doch von SQLlite werden nicht viele Vorgänge für die Schemamigration unterstützt. Daher sind nur sehr einfache Migrationsvorgänge möglich.</span><span class="sxs-lookup"><span data-stu-id="30b67-108">Migrations is a popular feature when using SQL Server, but SQLlite doesn't support many migration schema operations, so only very simply migrations are possible.</span></span> <span data-ttu-id="30b67-109">Weitere Informationen finden Sie unter [SQLite-Einschränkungen](/ef/core/providers/sqlite/limitations).</span><span class="sxs-lookup"><span data-stu-id="30b67-109">See [SQLite Limitations](/ef/core/providers/sqlite/limitations) for more information.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="30b67-110">Hinzufügen einer Rating-Eigenschaft zum Movie-Modell</span><span class="sxs-lookup"><span data-stu-id="30b67-110">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="30b67-111">Öffnen Sie die Datei *Models/Movie.cs*, und fügen Sie eine `Rating`-Eigenschaft hinzu:</span><span class="sxs-lookup"><span data-stu-id="30b67-111">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

<span data-ttu-id="30b67-112">Da Sie der `Movie`-Klasse ein neues Feld hinzugefügt haben, müssen Sie auch die Positivliste für die Bindung aktualisieren, damit diese neue Eigenschaft eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="30b67-112">Because you've added a new field to the `Movie` class, you also need to update the binding whitelist so this new property will be included.</span></span> <span data-ttu-id="30b67-113">Aktualisieren Sie in *MoviesController.cs* das `[Bind]`-Attribut für die Aktionsmethoden `Create` und `Edit` so, dass die `Rating`-Eigenschaft eingeschlossen wird:</span><span class="sxs-lookup"><span data-stu-id="30b67-113">In *MoviesController.cs*, update the `[Bind]` attribute for both the `Create` and `Edit` action methods to include the `Rating` property:</span></span>

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

<span data-ttu-id="30b67-114">Sie müssen auch die Ansichtsvorlagen aktualisieren, um die neue `Rating`-Eigenschaft in der Browseransicht anzuzeigen, zu erstellen und zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="30b67-114">You also need to update the view templates in order to display, create, and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="30b67-115">Bearbeiten Sie die Datei */Views/Movies/Index.cshtml*, und fügen Sie das Feld `Rating` hinzu:</span><span class="sxs-lookup"><span data-stu-id="30b67-115">Edit the */Views/Movies/Index.cshtml* file and add a `Rating` field:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

<span data-ttu-id="30b67-116">Aktualisieren Sie die Datei */Views/Movies/Create.cshtml* mit dem Feld `Rating`.</span><span class="sxs-lookup"><span data-stu-id="30b67-116">Update the */Views/Movies/Create.cshtml* with a `Rating` field.</span></span>

<span data-ttu-id="30b67-117">Die App funktioniert erst, nachdem wir die Datenbank mit dem neuen Feld aktualisiert haben.</span><span class="sxs-lookup"><span data-stu-id="30b67-117">The app won't work until we update the DB to include the new field.</span></span> <span data-ttu-id="30b67-118">Wenn Sie sie jetzt ausführen, erhalten Sie die folgende `SqliteException`:</span><span class="sxs-lookup"><span data-stu-id="30b67-118">If you run it now, you'll get the following `SqliteException`:</span></span>

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

<span data-ttu-id="30b67-119">Dieser Fehler wird gemeldet, da die aktualisierte Modellklasse „Movie“ sich vom Schema der Tabelle „Movie“ der vorhandenen Datenbank unterscheidet.</span><span class="sxs-lookup"><span data-stu-id="30b67-119">You're seeing this error because the updated Movie model class is different than the schema of the Movie table of the existing database.</span></span> <span data-ttu-id="30b67-120">(Die Datenbanktabelle enthält nicht die Spalte `Rating`.)</span><span class="sxs-lookup"><span data-stu-id="30b67-120">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="30b67-121">Es gibt mehrere Vorgehensweisen zum Beheben des Fehlers:</span><span class="sxs-lookup"><span data-stu-id="30b67-121">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="30b67-122">Lassen Sie die Datenbank von Entity Framework automatisch löschen und basierend auf dem neuen Modellklassenschema neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="30b67-122">Drop the database and have the Entity Framework automatically re-create the database based on the new model class schema.</span></span> <span data-ttu-id="30b67-123">Bei dieser Vorgehensweise gehen in der Datenbank vorhandene Daten verloren, die deshalb bei einer Produktionsdatenbank nicht möglich ist!</span><span class="sxs-lookup"><span data-stu-id="30b67-123">With this approach, you lose existing data in the database — so you can't do this with a production database!</span></span> <span data-ttu-id="30b67-124">Das Verwenden eines Initialisierers zum automatischen Ausführen eines Seedings für eine Datenbank mit Testdaten ist häufig eine produktive Möglichkeit zum Entwickeln einer App.</span><span class="sxs-lookup"><span data-stu-id="30b67-124">Using an initializer to automatically seed a database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="30b67-125">Ändern Sie das Schema der vorhandenen Datenbank manuell so, dass es mit den Modellklassen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="30b67-125">Manually modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="30b67-126">Der Vorteil dieses Ansatzes ist, dass Sie Ihre Daten behalten.</span><span class="sxs-lookup"><span data-stu-id="30b67-126">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="30b67-127">Sie können diese Änderung entweder manuell oder durch Erstellen eines Änderungsskripts für die Datenbank vornehmen.</span><span class="sxs-lookup"><span data-stu-id="30b67-127">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="30b67-128">Verwenden Sie Code First-Migrationen, um das Datenbankschema zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="30b67-128">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="30b67-129">In diesem Tutorial löschen wir die Datenbank und erstellen Sie neu, sobald sich das Schema ändert.</span><span class="sxs-lookup"><span data-stu-id="30b67-129">For this tutorial, we'll drop and re-create the database when the schema changes.</span></span> <span data-ttu-id="30b67-130">Führen Sie über ein Terminal den folgenden Befehl aus, um die Datenbank zu löschen:</span><span class="sxs-lookup"><span data-stu-id="30b67-130">Run the following command from a terminal to drop the db:</span></span>

`dotnet ef database drop`

<span data-ttu-id="30b67-131">Aktualisieren Sie die `SeedData`-Klasse so, dass sie einen Wert für die neue Spalte bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="30b67-131">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="30b67-132">Eine Beispieländerung wird nachstehend gezeigt, aber Sie sollten diese Änderung für jedes `new Movie`-Element vornehmen.</span><span class="sxs-lookup"><span data-stu-id="30b67-132">A sample change is shown below, but you'll want to make this change for each `new Movie`.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

<span data-ttu-id="30b67-133">Fügen Sie das Feld `Rating` den Ansichten `Edit`, `Details` und `Delete` hinzu.</span><span class="sxs-lookup"><span data-stu-id="30b67-133">Add the `Rating` field to the `Edit`, `Details`, and `Delete` view.</span></span>

<span data-ttu-id="30b67-134">Führen Sie die App aus, und überprüfen Sie, ob Sie Filme mit dem Feld `Rating` erstellen/bearbeiten/anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="30b67-134">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="30b67-135">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="30b67-135">templates.</span></span>
