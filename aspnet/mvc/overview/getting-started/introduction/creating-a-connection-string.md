---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Erstellen einer Verbindungszeichenfolge und Arbeiten mit SQL Server LocalDB | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 746101344832793b199d2b3f3dfcfcd4e3b9a8da
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031947"
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="360a3-102">Erstellen einer Verbindungszeichenfolge und Arbeiten mit SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="360a3-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>
====================
<span data-ttu-id="360a3-103">durch [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="360a3-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="360a3-104">Erstellen einer Verbindungszeichenfolge und Arbeiten mit SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="360a3-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="360a3-105">Die `MovieDBContext` erstellten Klasse übernimmt die Aufgabe der Verbindung zur Datenbank und Zuordnung `Movie` Objekte mit Datenbank-Datensätzen.</span><span class="sxs-lookup"><span data-stu-id="360a3-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="360a3-106">Eine Frage, die Sie wahrscheinlich gebeten, die ist jedoch, nach welcher Datenbank geben sie eine Verbindung herstellen.</span><span class="sxs-lookup"><span data-stu-id="360a3-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="360a3-107">Sie müssen nicht unbedingt die zu verwendende Datenbank angeben, die Entity Framework standardmäßig [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="360a3-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="360a3-108">In diesem Abschnitt werden wir explizit hinzufügen eine Verbindungszeichenfolge in der *"Web.config"* -Datei der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="360a3-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="360a3-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="360a3-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="360a3-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) ist eine einfache Version von SQL Server Express-Datenbankmoduls, die wird bedarfsgesteuert gestartet und im Benutzermodus ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="360a3-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="360a3-111">LocalDB ausgeführt wird, in einem speziellen Ausführungsmodus von SQL Server Express, die Ihnen ermöglicht, die Arbeit mit Datenbanken als *mdf* Dateien.</span><span class="sxs-lookup"><span data-stu-id="360a3-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="360a3-112">LocalDB-Datenbankdateien bleiben in der Regel der *App\_Daten* Ordner eines Webprojekts.</span><span class="sxs-lookup"><span data-stu-id="360a3-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="360a3-113">SQL Server Express wird für die Verwendung in Produktionsanwendungen für Web nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="360a3-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="360a3-114">LocalDB sollte insbesondere nicht für die Produktion mit einer Webanwendung verwendet werden, da es nicht ausgelegt ist, arbeiten Sie mit IIS.</span><span class="sxs-lookup"><span data-stu-id="360a3-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="360a3-115">Eine LocalDB-Datenbank kann jedoch problemlos in SQL Server oder SQL Azure migriert werden.</span><span class="sxs-lookup"><span data-stu-id="360a3-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="360a3-116">In Visual Studio 2017 wird die LocalDB wird standardmäßig mit Visual Studio installiert.</span><span class="sxs-lookup"><span data-stu-id="360a3-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="360a3-117">Standardmäßig sucht die Entity Framework eine Verbindungszeichenfolge, die den gleichen Namen wie die Objektkontextklasse (`MovieDBContext` für dieses Projekt).</span><span class="sxs-lookup"><span data-stu-id="360a3-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="360a3-118">Weitere Informationen finden Sie unter [SQL Server-Verbindungszeichenfolgen für ASP.NET-Webanwendungen](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="360a3-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="360a3-119">Öffnen Sie den Stammordner der Anwendung *"Web.config"* unten angezeigten Datei.</span><span class="sxs-lookup"><span data-stu-id="360a3-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="360a3-120">(Nicht die *"Web.config"* Datei die *Ansichten* Ordner.)</span><span class="sxs-lookup"><span data-stu-id="360a3-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="360a3-121">Suchen der `<connectionStrings>` Element:</span><span class="sxs-lookup"><span data-stu-id="360a3-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="360a3-122">Fügen Sie die folgende Verbindungszeichenfolge für die `<connectionStrings>` Element in der *"Web.config"* Datei.</span><span class="sxs-lookup"><span data-stu-id="360a3-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="360a3-123">Das folgende Beispiel zeigt einen Teil der *"Web.config"* -Datei mit der neuen Verbindungszeichenfolge hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="360a3-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="360a3-124">Die beiden Verbindungszeichenfolgen sind sehr ähnlich.</span><span class="sxs-lookup"><span data-stu-id="360a3-124">The two connection strings are very similar.</span></span> <span data-ttu-id="360a3-125">Die erste Verbindungszeichenfolge wird mit dem Namen `DefaultConnection` und wird verwendet, für die Mitgliedschaftsdatenbank steuern, wer die Anwendung zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="360a3-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="360a3-126">Gibt die Verbindungszeichenfolge, die Sie hinzugefügt haben, an einer LocalDB-Datenbank, die mit dem Namen *Movie.mdf* befindet sich in der *App\_Daten* Ordner.</span><span class="sxs-lookup"><span data-stu-id="360a3-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="360a3-127">Es wird nicht die Mitgliedschaftsdatenbank in diesem Tutorial Weitere Informationen zur Mitgliedschaft, Authentifizierung und Sicherheit, finden Sie unter meinem Tutorial [eine ASP.NET MVC-app mit Authentifizierung und SQL-Datenbank erstellen und Bereitstellen in Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="360a3-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="360a3-128">Der Name der Verbindungszeichenfolge muss den Namen entsprechen den ["DbContext"](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) Klasse.</span><span class="sxs-lookup"><span data-stu-id="360a3-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="360a3-129">Sie müssen nicht tatsächlich fügen die `MovieDBContext` Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="360a3-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="360a3-130">Wenn Sie eine Verbindungszeichenfolge angeben, erstellt Entity Framework eine LocalDB-Datenbank im Benutzerverzeichnis mit dem vollqualifizierten Namen der die ["DbContext"](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) Klasse (in diesem Fall `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="360a3-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="360a3-131">Sie können name ist die Datenbank beliebig, solange sie verfügt über die *. MDF-Datei* Suffix.</span><span class="sxs-lookup"><span data-stu-id="360a3-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="360a3-132">Beispielsweise könnten wir nennen Sie die Datenbank *MyFilms.mdf*.</span><span class="sxs-lookup"><span data-stu-id="360a3-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="360a3-133">Als Nächstes erstellen Sie ein neues `MoviesController` -Klasse, die Sie verwenden können, die Filmdaten angezeigt und können Benutzer neue Film Auflistungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="360a3-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="360a3-134">[Zurück](adding-a-model.md)
> [Weiter](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="360a3-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
