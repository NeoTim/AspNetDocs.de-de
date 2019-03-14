---
ms.openlocfilehash: 24726fba7f431f701b264a988a8de1b67d41d8a2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048717"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="69293-101">Hinzufügen der Suche zu einer ASP.NET Core MVC-App</span><span class="sxs-lookup"><span data-stu-id="69293-101">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="69293-102">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="69293-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="69293-103">In diesem Abschnitt fügen Sie die Suchfunktion der Aktionsmethode `Index` hinzu, mit der Sie Filme nach *Genre* oder *Namen* suchen können.</span><span class="sxs-lookup"><span data-stu-id="69293-103">In this section you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="69293-104">Aktualisieren Sie die `Index`-Methode mit folgendem Code:</span><span class="sxs-lookup"><span data-stu-id="69293-104">Update the `Index` method with the following code:</span></span>
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]
-->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="69293-105">Die erste Zeile der Aktionsmethode `Index` erstellt eine [LINQ](/dotnet/standard/using-linq)-Abfrage zum Auswählen der Filme:</span><span class="sxs-lookup"><span data-stu-id="69293-105">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="69293-106">Die Abfrage wird an dieser Stelle *nur* definiert und **nicht** auf die Datenbank angewendet.</span><span class="sxs-lookup"><span data-stu-id="69293-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="69293-107">Wenn der `searchString`-Parameter eine Zeichenfolge enthält, wird die Filmabfrage so geändert, dass nach dem Wert der Suchzeichenfolge gefiltert wird:</span><span class="sxs-lookup"><span data-stu-id="69293-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="69293-108">Der Code `s => s.Title.Contains()` oben ist ein [Lambdaausdruck](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="69293-108">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="69293-109">Lambdas werden in methodenbasierten [LINQ](/dotnet/standard/using-linq)-Abfragen als Argumente für standardmäßige Abfrageoperatormethoden wie die [Where](/dotnet/api/system.linq.enumerable.where)-Methode oder `Contains` verwendet (siehe den vorangehenden Code).</span><span class="sxs-lookup"><span data-stu-id="69293-109">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="69293-110">LINQ-Abfragen werden nicht ausgeführt, wenn sie definiert oder durch Aufrufen einer Methode geändert werden (z.B. `Where`, `Contains` oder `OrderBy`).</span><span class="sxs-lookup"><span data-stu-id="69293-110">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`  or `OrderBy`.</span></span> <span data-ttu-id="69293-111">Stattdessen wird die Ausführung der Abfrage verzögert.</span><span class="sxs-lookup"><span data-stu-id="69293-111">Rather, query execution is deferred.</span></span>  <span data-ttu-id="69293-112">Dies bedeutet, dass die Auswertung eines Ausdrucks so lange hinausgezögert wird, bis dessen realisierter Wert tatsächlich durchlaufen oder die `ToListAsync`-Methode aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="69293-112">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="69293-113">Weitere Informationen zur verzögerten Abfrageausführung finden Sie unter [Abfrageausführung](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span><span class="sxs-lookup"><span data-stu-id="69293-113">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="69293-114">Hinweis: Die [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains)-Methode wird in der Datenbank und nicht im oben gezeigten C#-Code ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="69293-114">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="69293-115">Die Groß-/Kleinschreibung in der Abfrage hängt von der Datenbank und Sortierung ab.</span><span class="sxs-lookup"><span data-stu-id="69293-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="69293-116">In SQL Server wird [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) zu [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql) zugeordnet, das Groß-/Kleinschreibung nicht beachtet.</span><span class="sxs-lookup"><span data-stu-id="69293-116">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="69293-117">In SQLite wird bei der Standardsortierung Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="69293-117">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="69293-118">Navigieren Sie zu `/Movies/Index`.</span><span class="sxs-lookup"><span data-stu-id="69293-118">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="69293-119">Fügen Sie eine Abfragezeichenfolge wie `?searchString=Ghost` an die URL an.</span><span class="sxs-lookup"><span data-stu-id="69293-119">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="69293-120">Die gefilterten Filme werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="69293-120">The filtered movies are displayed.</span></span>

![Indexansicht](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="69293-122">Wenn Sie die Signatur der `Index`-Methode so ändern, dass sie einen Parameter mit dem Namen `id` hat, entspricht der Parameter `id` dem optionalen Platzhalter `{id}` für die Standardrouten, die in *Startup.cs* festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="69293-122">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]
