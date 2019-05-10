---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Einführung in ASP.NET MVC | Microsoft-Dokumentation
author: shanselman
description: Dies ist ein Tutorial für Anfänger, die die Grundlagen von ASP.NET MVC eingeführt werden. Erstellen Sie eine einfache Webanwendung, die aus einer Datenbank liest und schreibt.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123125"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="d0b82-104">Einführung in ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="d0b82-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="d0b82-105">durch [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="d0b82-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="d0b82-106">Eine aktualisierte Version ist in diesem Tutorial verfügbaren [hier](../../getting-started/introduction/getting-started.md) mit [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span><span class="sxs-lookup"><span data-stu-id="d0b82-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="d0b82-107">Das neue Tutorial verwendet ASP.NET MVC 5, die viele Verbesserungen für dieses Tutorial bietet.</span><span class="sxs-lookup"><span data-stu-id="d0b82-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="d0b82-108">Dies ist ein Tutorial für Anfänger, die die Grundlagen von ASP.NET MVC eingeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d0b82-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="d0b82-109">Sie erstellen eine einfache Webanwendung, die aus einer Datenbank liest und schreibt.</span><span class="sxs-lookup"><span data-stu-id="d0b82-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="d0b82-110">Besuchen Sie die [ASP.NET MVC-Informationscenter](../../../index.md) anderen ASP.NET MVC anhand von Tutorials und Beispiele finden.</span><span class="sxs-lookup"><span data-stu-id="d0b82-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="d0b82-111">Lassen Sie uns unsere erste ASP.NET MVC-Webanwendung mit [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span><span class="sxs-lookup"><span data-stu-id="d0b82-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="d0b82-112">Wir erstellen eine kleine Anwendung "Movie List", die wir erstellen und Liste von Filmen.</span><span class="sxs-lookup"><span data-stu-id="d0b82-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d0b82-113">Sie lernen Folgendes</span><span class="sxs-lookup"><span data-stu-id="d0b82-113">What You'll Build</span></span>

<span data-ttu-id="d0b82-114">Hier sind die beiden Screenshots der Anwendung, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0b82-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="d0b82-115">Sie haben eine einfache Tabelle mit den Filmen mit verschiedenen Spalten.</span><span class="sxs-lookup"><span data-stu-id="d0b82-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="d0b82-116">[![Filmliste – Windows InternetExplorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="d0b82-117">Und Sie müssen ein Formular erstellen, damit Filme der Liste hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="d0b82-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="d0b82-118">[![Erstellen Sie einen Film - Windows InternetExplorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="d0b82-119">Fähigkeiten, mit denen, die Sie lernen Folgendes</span><span class="sxs-lookup"><span data-stu-id="d0b82-119">Skills You'll Learn</span></span>

<span data-ttu-id="d0b82-120">In diesem Tutorial lernen Sie die Grundlagen zum Erstellen einer ASP.NET MVC-Webanwendung mithilfe von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0b82-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="d0b82-121">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d0b82-121">You'll learn:</span></span>

- <span data-ttu-id="d0b82-122">Vorgehensweise: Erstellen Sie ein neues ASP.NET MVC-Projekt</span><span class="sxs-lookup"><span data-stu-id="d0b82-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="d0b82-123">Gewusst wie: Erstellen einer neuen Datenbank mit SQL Server</span><span class="sxs-lookup"><span data-stu-id="d0b82-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="d0b82-124">Gewusst wie: Erstellen von ASP.NET MVC-Controller und Ansichten</span><span class="sxs-lookup"><span data-stu-id="d0b82-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="d0b82-125">Das Abrufen und Anzeigen von Daten</span><span class="sxs-lookup"><span data-stu-id="d0b82-125">How to retrieve and display data</span></span>
- <span data-ttu-id="d0b82-126">Bearbeiten von Daten, und aktivieren die datenüberprüfung</span><span class="sxs-lookup"><span data-stu-id="d0b82-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="d0b82-127">Wie Sie das Datenbankschema aktualisieren</span><span class="sxs-lookup"><span data-stu-id="d0b82-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="d0b82-128">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="d0b82-128">Get Started</span></span>

<span data-ttu-id="d0b82-129">Starten Sie durch Ausführen von Visual Web Developer 2010 Express (Ich werde sie von nun an "VWD" bezeichnet), und wählen Sie Neues Projekt aus der Startbildschirm ausgeblendet wird.</span><span class="sxs-lookup"><span data-stu-id="d0b82-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="d0b82-130">Visual Web Developer ist eine IDE oder Integrated Developer Environment.</span><span class="sxs-lookup"><span data-stu-id="d0b82-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="d0b82-131">Wie Sie Microsoft Word zum Schreiben von Dokumenten verwenden, verwenden Sie eine IDE, um Anwendungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0b82-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="d0b82-132">Es wird eine Symbolleiste am oberen mit verschiedenen Optionen zur Verfügung, die Sie als auch im Menü kann außerdem verwendet haben, um die Datei auswählen | Neues Projekt.</span><span class="sxs-lookup"><span data-stu-id="d0b82-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="d0b82-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="d0b82-134">Erstellen Ihrer ersten Anwendung</span><span class="sxs-lookup"><span data-stu-id="d0b82-134">Creating Your First Application</span></span>

<span data-ttu-id="d0b82-135">Sie können mit Visual Basic oder Visual C#-Anwendungen erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0b82-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="d0b82-136">Jetzt wählen Sie Visual C# -Code auf der linken Seite Wählen Sie dann "ASP.NET MVC 2-Webanwendung".</span><span class="sxs-lookup"><span data-stu-id="d0b82-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="d0b82-137">Benennen Sie das Projekt "Movies", und klicken Sie auf OK.</span><span class="sxs-lookup"><span data-stu-id="d0b82-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="d0b82-138">[![Neues Projekt](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="d0b82-139">Auf die rechte Seite ist im Projektmappen-Explorer mit der alle Dateien und Ordner in Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="d0b82-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="d0b82-140">Fenster in der Mitte große ist, in dem Sie Ihren Code bearbeiten und verbringen die meiste Zeit.</span><span class="sxs-lookup"><span data-stu-id="d0b82-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="d0b82-141">Visual Studio verwendet eine Standardvorlage für das ASP.NET MVC-Projekt, das Sie gerade erstellt haben, müssen Sie eine funktionierende Anwendung jetzt ohne Benutzereingriff.</span><span class="sxs-lookup"><span data-stu-id="d0b82-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="d0b82-142">Dies ist eine einfache "Hello World!</span><span class="sxs-lookup"><span data-stu-id="d0b82-142">This is a simple "Hello World!</span></span> <span data-ttu-id="d0b82-143">Projekt, und es ist ein guter Ausgangspunkt für die Anwendung zu starten.</span><span class="sxs-lookup"><span data-stu-id="d0b82-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="d0b82-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="d0b82-145">Wählen Sie die Schaltfläche "Wiedergabe" auf der Symbolleiste aus.</span><span class="sxs-lookup"><span data-stu-id="d0b82-145">Select the "play" button to the toolbar.</span></span>

![Debugging starten](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="d0b82-147">Es ist ein grüner Pfeil auf der rechten Seite, die das Programm zu kompilieren und starten Sie die Anwendung in einem Webbrowser.</span><span class="sxs-lookup"><span data-stu-id="d0b82-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="d0b82-148">*HINWEIS: Sie können stattdessen drücken Sie F5 auf Ihrer Tastatur, oder wählen Sie Debug -&gt;Starten des Debuggens aus dem Menü "Debuggen".*</span><span class="sxs-lookup"><span data-stu-id="d0b82-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="d0b82-149">Dadurch wird Visual Web Developer zum Starten von eines Development Web-Servers und Ausführen von unserer Webanwendung (es gibt keine Konfiguration oder manuelle Schritte erforderlich, um dies zu ermöglichen).</span><span class="sxs-lookup"><span data-stu-id="d0b82-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="d0b82-150">Sie klicken Sie dann einen Browser starten und konfigurieren, dass die Startseite der Anwendung navigieren.</span><span class="sxs-lookup"><span data-stu-id="d0b82-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="d0b82-151">Unten können sehen Sie, dass die Adressleiste des Browsers "Localhost", und nicht etwa "example.com" lautet.</span><span class="sxs-lookup"><span data-stu-id="d0b82-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="d0b82-152">Das ist, da "localhost" auf Ihrem lokalen Computer - immer verweist, in dem in diesem Fall die Anwendung ausgeführt wird, die wir soeben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="d0b82-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="d0b82-153">[![Auf der Startseite](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="d0b82-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="d0b82-154">Standardmäßig gibt dieser Standardvorlage Sie zwei Seiten besuchen und eine einfache Anmeldeseite.</span><span class="sxs-lookup"><span data-stu-id="d0b82-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="d0b82-155">Wir ändern, wie diese Anwendung funktioniert, und erfahren Sie etwas, Informationen zu ASP.NET MVC im Prozess.</span><span class="sxs-lookup"><span data-stu-id="d0b82-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="d0b82-156">Schließen Sie Ihren Browser, und ermöglicht, Code zu ändern.</span><span class="sxs-lookup"><span data-stu-id="d0b82-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d0b82-157">Nächste</span><span class="sxs-lookup"><span data-stu-id="d0b82-157">Next</span></span>](getting-started-with-mvc-part2.md)
