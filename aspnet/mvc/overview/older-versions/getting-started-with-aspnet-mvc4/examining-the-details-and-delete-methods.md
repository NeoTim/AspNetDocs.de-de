---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
title: Untersuchen die Details und Delete-Methoden | Microsoft-Dokumentation
author: Rick-Anderson
description: 'Hinweis: Eine aktualisierte Version dieses Tutorials steht hier, dass das ASP.NET MVC 5 und Visual Studio 2013 verwendet. Es ist eine sicherere, viel einfacher zu folgen und demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 11425ff3-09fc-4efa-be9a-b53bce503460
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 1e23189fe927a5145647baa1f8886c4aed057b78
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063237"
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="a37a2-104">Untersuchen der Methoden „Details“ und „Delete“</span><span class="sxs-lookup"><span data-stu-id="a37a2-104">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="a37a2-105">durch [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="a37a2-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="a37a2-106">Eine aktualisierte Version dieses Tutorials finden Sie [hier](../../getting-started/introduction/getting-started.md) , ASP.NET MVC 5 und Visual Studio 2013 verwendet.</span><span class="sxs-lookup"><span data-stu-id="a37a2-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="a37a2-107">Dabei handelt es sich eine sicherere, einfacher, führen weitere Funktionen veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="a37a2-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="a37a2-108">In diesem Teil des Tutorials müssen Sie überprüfen die automatisch generierte `Details` und `Delete` Methoden.</span><span class="sxs-lookup"><span data-stu-id="a37a2-108">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="a37a2-109">Untersuchen der Methoden „Details“ und „Delete“</span><span class="sxs-lookup"><span data-stu-id="a37a2-109">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="a37a2-110">Öffnen der `Movie` Controller, und untersuchen Sie die `Details` Methode.</span><span class="sxs-lookup"><span data-stu-id="a37a2-110">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="a37a2-111">Die MVC-Gerüstbau-Engine, die diese Aktionsmethode erstellt hat, fügt einen Kommentar mit einer HTTP-Anforderung, die die Methode aufruft.</span><span class="sxs-lookup"><span data-stu-id="a37a2-111">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="a37a2-112">In diesem Fall ist es eine `GET` -Anforderung mit drei URL-Segmente, die `Movies` Controller die `Details` Methode und eine `ID` Wert.</span><span class="sxs-lookup"><span data-stu-id="a37a2-112">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="a37a2-113">Code zunächst ganz einfach suchen nach Daten mithilfe der `Find` Methode.</span><span class="sxs-lookup"><span data-stu-id="a37a2-113">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="a37a2-114">Eine wichtige Sicherheitsfunktion, die an die Methode erstellt wird, dass der Code, der überprüft, ob die `Find` Methode verfügt über einen Film gefunden, bevor der Code versucht, etwas damit zu tun.</span><span class="sxs-lookup"><span data-stu-id="a37a2-114">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="a37a2-115">Z. B. ein Hacker kann Fehler verursachen auf der Website durch Ändern der URL erstellt, indem Sie die Links aus `http://localhost:xxxx/Movies/Details/1` z. B. `http://localhost:xxxx/Movies/Details/12345` (oder einen anderen Wert, der keinen tatsächlichen Film darstellt).</span><span class="sxs-lookup"><span data-stu-id="a37a2-115">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="a37a2-116">Wenn Sie für einen null-Film nicht aktiviert haben, ergibt eine null-Movie eines Datenbankfehlers.</span><span class="sxs-lookup"><span data-stu-id="a37a2-116">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="a37a2-117">Untersuchen Sie die Methoden `Delete` und `DeleteConfirmed`.</span><span class="sxs-lookup"><span data-stu-id="a37a2-117">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="a37a2-118">Beachten Sie, dass die `HTTP Get``Delete` Methode nicht den angegebenen Film nicht gelöscht, es gibt eine Ansicht des Films, können Sie übermitteln (`HttpPost`) das Löschen...</span><span class="sxs-lookup"><span data-stu-id="a37a2-118">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="a37a2-119">Das Ausführen eines Löschvorgangs als Reaktion auf eine GET-Anforderung (oder eigentlich eines Bearbeitungs-, Erstellungs- oder sonstigen Vorgangs, der Daten ändern) stellt eine Sicherheitslücke dar.</span><span class="sxs-lookup"><span data-stu-id="a37a2-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="a37a2-120">Weitere Informationen hierzu finden Sie unter Stephen Walthers Blogeintrag [Tipp #46 von ASP.NET MVC – verwenden Sie keine Links löschen, da Sicherheitslücken entstehen](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="a37a2-120">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="a37a2-121">Die `HttpPost`-Methode, die die Daten löscht, heißt `DeleteConfirmed`, um der HTTP-POST-Methode eine eindeutige Signatur bzw. einen eindeutigen Namen zu geben.</span><span class="sxs-lookup"><span data-stu-id="a37a2-121">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="a37a2-122">Die beiden Methodensignaturen werden nachstehend gezeigt:</span><span class="sxs-lookup"><span data-stu-id="a37a2-122">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="a37a2-123">Die Common Language Runtime (CLR) erfordert überladene Methoden, um eine eindeutige Parametersignatur zu erhalten (selber Methodenname, aber unterschiedliche Liste von Parametern).</span><span class="sxs-lookup"><span data-stu-id="a37a2-123">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="a37a2-124">Hier benötigen Sie jedoch zwei Delete-Methoden – eine für GET und eine für POST beide die gleiche Parametersignatur haben.</span><span class="sxs-lookup"><span data-stu-id="a37a2-124">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="a37a2-125">(Beide müssen eine einzelne ganze Zahl als Parameter akzeptieren.)</span><span class="sxs-lookup"><span data-stu-id="a37a2-125">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="a37a2-126">Um dies zu sortieren, können Sie ein paar Dinge tun.</span><span class="sxs-lookup"><span data-stu-id="a37a2-126">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="a37a2-127">Eine besteht darin, die Methoden unterschiedlich zu benennen.</span><span class="sxs-lookup"><span data-stu-id="a37a2-127">One is to give the methods different names.</span></span> <span data-ttu-id="a37a2-128">Dafür das der Gerüstbaumechanismus im vorherigen Beispiel gesorgt.</span><span class="sxs-lookup"><span data-stu-id="a37a2-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="a37a2-129">Dies bringt jedoch ein kleines Problem mit sich: ASP.NET ordnet Segmente einer URL anhand des Namens zu Aktionsmethoden zu. Wenn Sie die Methode umbenennen sollten, ist das Routing normalerweise nicht in der Lage, diese Methode zu finden.</span><span class="sxs-lookup"><span data-stu-id="a37a2-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="a37a2-130">Die Lösung besteht (wie im Beispiel) im Hinzufügen des `ActionName("Delete")`-Attributs zur `DeleteConfirmed`-Methode.</span><span class="sxs-lookup"><span data-stu-id="a37a2-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="a37a2-131">Dies effektiv führt die Zuordnung für das Routingsystem so, dass eine URL, die beinhaltet <em>/Delete/</em>für eine POST-Anforderung findet die `DeleteConfirmed` Methode.</span><span class="sxs-lookup"><span data-stu-id="a37a2-131">This effectively performs mapping for the routing system so that a URL that includes <em>/Delete/</em>for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="a37a2-132">Um ein Problem mit den Methoden zu vermeiden, die identische Namen und Signaturen haben eine andere Möglichkeit besteht darin die Signatur der POST-Methode, um ein nicht verwendeter Parameter einzuschließen künstlich zu ändern.</span><span class="sxs-lookup"><span data-stu-id="a37a2-132">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="a37a2-133">Beispielsweise einige Entwickler einen Parametertyp hinzufügen `FormCollection` , das an die POST-Methode übergeben wird, und klicken Sie dann einfach nicht den Parameter verwenden:</span><span class="sxs-lookup"><span data-stu-id="a37a2-133">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="a37a2-134">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="a37a2-134">Summary</span></span>

<span data-ttu-id="a37a2-135">Sie haben jetzt eine vollständige ASP.NET MVC-Anwendung, die Daten in eine lokale DB-Datenbank speichert.</span><span class="sxs-lookup"><span data-stu-id="a37a2-135">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="a37a2-136">Sie können zu erstellen, lesen, aktualisieren, löschen und suchen Sie nach Filme.</span><span class="sxs-lookup"><span data-stu-id="a37a2-136">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="a37a2-137">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="a37a2-137">Next Steps</span></span>

<span data-ttu-id="a37a2-138">Nachdem Sie erstellt und eine Webanwendung getestet haben, besteht der nächste Schritt, um sie an andere Personen zu verwenden, über das Internet verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="a37a2-138">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="a37a2-139">Zu diesem Zweck müssen Sie es auf einen Webhostinganbieter bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a37a2-139">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="a37a2-140">Microsoft bietet kostenloses Webhosting für bis zu 10 Websites in einem [kostenlose Windows Azure-Testkonto](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="a37a2-140">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="a37a2-141">Ich schlage vor, Sie als Nächstes führen Sie meine Tutorial [bereitstellen eine sicheren ASP.NET MVC-app mit Mitgliedschaft, OAuth und SQL-Datenbank auf einem Windows Azure-Website](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="a37a2-141">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="a37a2-142">Ein ausgezeichnetes Tutorial ist Tom Dykstras fortgeschrittene [erstellen ein Entity Framework-Datenmodells für eine ASP.NET MVC-Anwendung](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="a37a2-142">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="a37a2-143">[Stackoverflow](http://stackoverflow.com/help) und [ASP.NET MVC-Foren](https://forums.asp.net/1146.aspx) sind eine gute platziert werden, um Fragen zu stellen.</span><span class="sxs-lookup"><span data-stu-id="a37a2-143">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="a37a2-144">Führen Sie [mich](https://twitter.com/RickAndMSFT) auf Twitter, sodass Sie Updates auf meinem neuesten Lernprogramme zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="a37a2-144">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="a37a2-145">Feedback ist Willkommen.</span><span class="sxs-lookup"><span data-stu-id="a37a2-145">Feedback is welcome.</span></span>

<span data-ttu-id="a37a2-146">– [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a37a2-146">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="a37a2-147">– [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="a37a2-147">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a37a2-148">Vorherige</span><span class="sxs-lookup"><span data-stu-id="a37a2-148">Previous</span></span>](adding-validation-to-the-model.md)