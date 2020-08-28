---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Erstellen einer Verbindungs Zeichenfolge und arbeiten mit SQL Server localdb | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 4400cb8c6a5d57da60d164220f929d69d7f4d2f7
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044258"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="8c1b3-102">Erstellen einer Verbindungszeichenfolge und Arbeiten mit SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="8c1b3-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8c1b3-103">von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8c1b3-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="8c1b3-104">Erstellen einer Verbindungszeichenfolge und Arbeiten mit SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="8c1b3-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8c1b3-105">Die `MovieDBContext` von Ihnen erstellte Klasse übernimmt die Aufgabe der Verbindung mit der Datenbank und die Zuordnung von `Movie` Objekten zu Datenbankdaten Sätzen.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="8c1b3-106">Eine Frage ist jedoch, wie Sie angeben können, mit welcher Datenbank eine Verbindung hergestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="8c1b3-107">Sie müssen eigentlich nicht angeben, welche Datenbank verwendet werden soll, Entity Framework standardmäßig [localdb](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="8c1b3-108">In diesem Abschnitt wird explizit eine Verbindungs Zeichenfolge in der *Web.config* -Datei der Anwendung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="8c1b3-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="8c1b3-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="8c1b3-110">[Localdb](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) ist eine vereinfachte Version der SQL Server Express Datenbank-Engine, die bei Bedarf gestartet wird und im Benutzermodus ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="8c1b3-111">Localdb wird in einem speziellen Ausführungs Modus von SQL Server Express ausgeführt, der es Ihnen ermöglicht, mit Datenbanken als *MDF* -Dateien zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="8c1b3-112">Normalerweise werden localdb-Datenbankdateien im *App- \_ Daten* Ordner eines Webprojekts gespeichert.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="8c1b3-113">SQL Server Express wird nicht für die Verwendung in produktionsweb Anwendungen empfohlen.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="8c1b3-114">Localdb sollte insbesondere nicht für die Produktion mit einer Webanwendung verwendet werden, da es nicht für die Verwendung mit IIS konzipiert ist.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="8c1b3-115">Eine localdb-Datenbank kann jedoch problemlos zu SQL Server oder SQL Azure migriert werden.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="8c1b3-116">In Visual Studio 2017 wird localdb standardmäßig mit Visual Studio installiert.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="8c1b3-117">Standardmäßig sucht die Entity Framework nach einer Verbindungs Zeichenfolge mit dem Namen, die mit der Objekt Kontext Klasse ( `MovieDBContext` für dieses Projekt) identisch ist.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="8c1b3-118">Weitere Informationen finden Sie unter SQL Server Verbindungs Zeichenfolgen [für ASP.NET-Webanwendungen](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c1b3-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="8c1b3-119">Öffnen Sie die Datei root *Web.config* der Anwendung, die unten dargestellt ist.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="8c1b3-120">(Nicht die *Web.config* Datei im Ordner " *views* ".)</span><span class="sxs-lookup"><span data-stu-id="8c1b3-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="8c1b3-121">Suchen Sie das- `<connectionStrings>` Element:</span><span class="sxs-lookup"><span data-stu-id="8c1b3-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="8c1b3-122">Fügen Sie dem- `<connectionStrings>` Element in der *Web.config* -Datei die folgende Verbindungs Zeichenfolge hinzu.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="8c1b3-123">Das folgende Beispiel zeigt einen Teil der *Web.config* -Datei, der die neue Verbindungs Zeichenfolge hinzugefügt wurde:</span><span class="sxs-lookup"><span data-stu-id="8c1b3-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="8c1b3-124">Die beiden Verbindungs Zeichenfolgen sind sehr ähnlich.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-124">The two connection strings are very similar.</span></span> <span data-ttu-id="8c1b3-125">Die erste Verbindungs Zeichenfolge hat den Namen `DefaultConnection` und wird für die Mitgliedschafts Datenbank verwendet, um zu steuern, wer auf die Anwendung zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="8c1b3-126">Die Verbindungs Zeichenfolge, die Sie hinzugefügt haben, gibt eine localdb-Datenbank mit dem Namen *Movie. mdf* im Ordner *App \_ Data* an.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="8c1b3-127">Die Mitgliedschafts Datenbank wird in diesem Tutorial nicht verwendet. Weitere Informationen zu Mitgliedschaft, Authentifizierung und Sicherheit finden Sie in meinem Tutorial [Erstellen einer ASP.NET MVC-App mit Authentifizierung und SQL-Datenbank und Bereitstellen in Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="8c1b3-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="8c1b3-128">Der Name der Verbindungs Zeichenfolge muss mit dem Namen der [dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) -Klasse identisch sein.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="8c1b3-129">Sie müssen die `MovieDBContext` Verbindungs Zeichenfolge nicht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="8c1b3-130">Wenn Sie keine Verbindungs Zeichenfolge angeben, erstellt Entity Framework eine localdb-Datenbank im Verzeichnis "Users" mit dem voll qualifizierten Namen der [dbcontext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) -Klasse (in diesem Fall `MvcMovie.Models.MovieDBContext` ).</span><span class="sxs-lookup"><span data-stu-id="8c1b3-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="8c1b3-131">Sie können der Datenbank einen beliebigen Namen benennen, solange Sie über verfügt *. MDF* -Suffix.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="8c1b3-132">Wir könnten der Datenbank beispielsweise den Namen " *myfilms. mdf*" geben.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="8c1b3-133">Als Nächstes erstellen Sie eine neue `MoviesController` Klasse, die Sie verwenden können, um die Filmdaten anzuzeigen und Benutzern das Erstellen neuer Film Auflistungen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="8c1b3-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c1b3-134">[Zurück](adding-a-model.md)
> [Weiter](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="8c1b3-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
