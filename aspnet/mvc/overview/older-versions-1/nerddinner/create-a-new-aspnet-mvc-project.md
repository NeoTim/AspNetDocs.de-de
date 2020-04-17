---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Erstellen eines neuen ASP.NET MVC-Projekts | Microsoft Docs
author: rick-anderson
description: Schritt 1 zeigt Ihnen, wie Sie die grundlegende NerdDinner-Anwendungsstruktur an Ort und Stelle setzen.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541480"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="6c12b-103">Erstellen eines neuen ASP.NET MVC-Projekts</span><span class="sxs-lookup"><span data-stu-id="6c12b-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="6c12b-104">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6c12b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="6c12b-105">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="6c12b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="6c12b-106">Dies ist Schritt 1 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.</span><span class="sxs-lookup"><span data-stu-id="6c12b-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="6c12b-107">Schritt 1 zeigt Ihnen, wie Sie die grundlegende NerdDinner-Anwendungsstruktur an Ort und Stelle setzen.</span><span class="sxs-lookup"><span data-stu-id="6c12b-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="6c12b-108">Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.</span><span class="sxs-lookup"><span data-stu-id="6c12b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="6c12b-109">NerdDinner Schritt 1:&gt;Datei- Neues Projekt</span><span class="sxs-lookup"><span data-stu-id="6c12b-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="6c12b-110">Wir beginnen unsere NerdDinner-Anwendung, indem wir den Menüpunkt **Datei-&gt;Neues Projekt** entweder in Visual Studio 2008 oder im kostenlosen Visual Web Developer 2008 Express auswählen.</span><span class="sxs-lookup"><span data-stu-id="6c12b-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="6c12b-111">Dadurch wird der Dialog "Neues Projekt" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6c12b-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="6c12b-112">Um eine neue ASP.NET MVC-Anwendung zu erstellen, wählen wir den Knoten "Web" auf der linken Seite des Dialogfelds und dann die Projektvorlage "ASP.NET MVC Web Application" auf der rechten Seite aus:</span><span class="sxs-lookup"><span data-stu-id="6c12b-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="6c12b-113">*Wichtig: Stellen Sie sicher, dass Sie ASP.NET MVC heruntergeladen und installiert haben – andernfalls wird es nicht im Dialogfeld Neues Projekt angezeigt. Sie können V2 des [Microsoft Web Platform Installerverwendens](https://www.microsoft.com/web/downloads/platform.aspx) verwenden, wenn Sie es noch nicht&gt;installiert haben (ASP.NET MVC ist im Abschnitt "Webplattform-Frameworks und Laufzeiten" verfügbar).*</span><span class="sxs-lookup"><span data-stu-id="6c12b-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="6c12b-114">Wir nennen das neue Projekt, das wir erstellen werden, "NerdDinner" und klicken dann auf die Schaltfläche "OK", um es zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6c12b-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="6c12b-115">Wenn wir auf "OK" klicken, ruft Visual Studio ein zusätzliches Dialogfeld auf, in dem wir aufgefordert werden, optional auch ein Komponententestprojekt für die neue Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6c12b-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="6c12b-116">Dieses Komponententestprojekt ermöglicht es uns, automatisierte Tests zu erstellen, die die Funktionalität und das Verhalten unserer Anwendung überprüfen (etwas, das wir später in diesem Tutorial behandeln werden).</span><span class="sxs-lookup"><span data-stu-id="6c12b-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="6c12b-117">Die Dropdownliste "Testframework" im obigen Dialogfeld wird mit allen verfügbaren ASP.NET MVC-Komponententestprojektvorlagen aufgefüllt, die auf dem Computer installiert sind.</span><span class="sxs-lookup"><span data-stu-id="6c12b-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="6c12b-118">Versionen können für NUnit, MBUnit und XUnit heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="6c12b-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="6c12b-119">Das integrierte Visual Studio Unit Test-Framework wird ebenfalls unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6c12b-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="6c12b-120">*Hinweis: Das Visual Studio Unit Test Framework ist nur mit Visual Studio 2008 Professional und höheren Versionen verfügbar. Wenn Sie VS 2008 Standard Edition oder Visual Web Developer 2008 Express verwenden, müssen Sie die NUnit-, MBUnit- oder XUnit-Erweiterungen für ASP.NET MVC herunterladen und installieren, damit dieses Dialogfeld angezeigt wird. Das Dialogfeld wird nicht angezeigt, wenn keine Testframeworks installiert sind.*</span><span class="sxs-lookup"><span data-stu-id="6c12b-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="6c12b-121">Wir verwenden den Standardnamen "NerdDinner.Tests" für das von uns erstellte Testprojekt und die Frameworkoption "Visual Studio Unit Test".</span><span class="sxs-lookup"><span data-stu-id="6c12b-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="6c12b-122">Wenn wir auf die Schaltfläche "ok" klicken, erstellt Visual Studio eine Lösung für uns mit zwei Projekten - eines für unsere Webanwendung und eines für unsere Komponententests:</span><span class="sxs-lookup"><span data-stu-id="6c12b-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="6c12b-123">Untersuchen der NerdDinner-Verzeichnisstruktur</span><span class="sxs-lookup"><span data-stu-id="6c12b-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="6c12b-124">Wenn Sie eine neue ASP.NET MVC-Anwendung mit Visual Studio erstellen, wird dem Projekt automatisch eine Reihe von Dateien und Verzeichnissen hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="6c12b-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="6c12b-125">ASP.NET MVC-Projekte verfügen standardmäßig über sechs Verzeichnisse der obersten Ebene:</span><span class="sxs-lookup"><span data-stu-id="6c12b-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="6c12b-126">**Verzeichnis**</span><span class="sxs-lookup"><span data-stu-id="6c12b-126">**Directory**</span></span> | <span data-ttu-id="6c12b-127">**Zweck**</span><span class="sxs-lookup"><span data-stu-id="6c12b-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="6c12b-128">**/Controller**</span><span class="sxs-lookup"><span data-stu-id="6c12b-128">**/Controllers**</span></span> | <span data-ttu-id="6c12b-129">Wo Sie Controller-Klassen einfügen, die URL-Anforderungen verarbeiten</span><span class="sxs-lookup"><span data-stu-id="6c12b-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="6c12b-130">**/Modelle**</span><span class="sxs-lookup"><span data-stu-id="6c12b-130">**/Models**</span></span> | <span data-ttu-id="6c12b-131">Wo Sie Klassen setzen, die Daten darstellen und bearbeiten</span><span class="sxs-lookup"><span data-stu-id="6c12b-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="6c12b-132">**/Ansichten**</span><span class="sxs-lookup"><span data-stu-id="6c12b-132">**/Views**</span></span> | <span data-ttu-id="6c12b-133">Wo Sie UI-Vorlagendateien einfügen, die für das Rendern der Ausgabe verantwortlich sind</span><span class="sxs-lookup"><span data-stu-id="6c12b-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="6c12b-134">**/Skripte**</span><span class="sxs-lookup"><span data-stu-id="6c12b-134">**/Scripts**</span></span> | <span data-ttu-id="6c12b-135">Wo Sie JavaScript-Bibliotheksdateien und -skripts (.js)</span><span class="sxs-lookup"><span data-stu-id="6c12b-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="6c12b-136">**/Inhalt**</span><span class="sxs-lookup"><span data-stu-id="6c12b-136">**/Content**</span></span> | <span data-ttu-id="6c12b-137">Wo Sie CSS- und Bilddateien und andere nicht-dynamische/nicht-JavaScript-Inhalte</span><span class="sxs-lookup"><span data-stu-id="6c12b-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="6c12b-138">**/App-Daten\_**</span><span class="sxs-lookup"><span data-stu-id="6c12b-138">**/App\_Data**</span></span> | <span data-ttu-id="6c12b-139">Wo Sie Datendateien speichern, die Sie lesen/schreiben möchten.</span><span class="sxs-lookup"><span data-stu-id="6c12b-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="6c12b-140">ASP.NET MVC erfordert diese Struktur nicht.</span><span class="sxs-lookup"><span data-stu-id="6c12b-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="6c12b-141">Tatsächlich partitionieren Entwickler, die an großen Anwendungen arbeiten, die Anwendung in der Regel über mehrere Projekte hinweg, um sie leichter zu verwalten (z. B. Datenmodellklassen werden häufig in einem separaten Klassenbibliotheksprojekt von der Webanwendung verwendet).</span><span class="sxs-lookup"><span data-stu-id="6c12b-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="6c12b-142">Die Standardprojektstruktur stellt jedoch eine nette Standardverzeichniskonvention bereit, die wir verwenden können, um unsere Anwendungsprobleme sauber zu halten.</span><span class="sxs-lookup"><span data-stu-id="6c12b-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="6c12b-143">Wenn wir das Verzeichnis /Controllers erweitern, werden wir feststellen, dass Visual Studio dem Projekt standardmäßig zwei Controllerklassen – HomeController und AccountController – hinzugefügt hat:</span><span class="sxs-lookup"><span data-stu-id="6c12b-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="6c12b-144">Wenn wir das Verzeichnis /Views erweitern, werden drei Unterverzeichnisse – /Home, /Account und /Shared – sowie mehrere Vorlagendateien darin standardmäßig ebenfalls zum Projekt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="6c12b-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="6c12b-145">Wenn wir die Verzeichnisse /Content und /Scripts erweitern, finden wir eine Site.css-Datei, die zum Formatieren aller HTML-Dateien auf der Website verwendet wird, sowie JavaScript-Bibliotheken, die ASP.NET AJAX- und jQuery-Unterstützung innerhalb der Anwendung aktivieren können:</span><span class="sxs-lookup"><span data-stu-id="6c12b-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="6c12b-146">Wenn wir das NerdDinner.Tests-Projekt erweitern, finden wir zwei Klassen, die Komponententests für unsere Controllerklassen enthalten:</span><span class="sxs-lookup"><span data-stu-id="6c12b-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="6c12b-147">Diese von Visual Studio hinzugefügten Standarddateien bieten uns eine grundlegende Struktur für eine funktionierende Anwendung - komplett mit Homepage, über Seite, Kontoanmeldung/Logout/Registrierungsseiten und einer nicht behandelten Fehlerseite (alle verkabelt und aus dem Feld heraus).</span><span class="sxs-lookup"><span data-stu-id="6c12b-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="6c12b-148">Ausführen der NerdDinner-Anwendung</span><span class="sxs-lookup"><span data-stu-id="6c12b-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="6c12b-149">Wir können das Projekt ausführen, indem wir entweder die Menüelemente **Debug-&gt;Debugging starten** oder **Debug-&gt;Start ohne Debugging** auswählen:</span><span class="sxs-lookup"><span data-stu-id="6c12b-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="6c12b-150">Dadurch wird der integrierte ASP.NET Webserver mit Visual Studio gestartet und unsere Anwendung ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="6c12b-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="6c12b-151">Unten ist die Startseite für unser neues Projekt (URL: "/"),wenn es läuft:</span><span class="sxs-lookup"><span data-stu-id="6c12b-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="6c12b-152">Wenn Sie auf die Registerkarte "Über" klicken, wird eine Übersichtsseite angezeigt (URL: "/Home/About"):</span><span class="sxs-lookup"><span data-stu-id="6c12b-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="6c12b-153">Ein Klick auf den Link "Anmelden" oben rechts führt uns zu einer Login-Seite (URL: "/Konto/LogOn")</span><span class="sxs-lookup"><span data-stu-id="6c12b-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="6c12b-154">Wenn wir kein Login-Konto haben, können wir auf den Registerlink (URL: "/Konto/Register") klicken, um eines zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="6c12b-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="6c12b-155">Der Code zum Implementieren der oben genannten Home-, about- und logout/register-Funktionalität wurde standardmäßig hinzugefügt, als wir unser neues Projekt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6c12b-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="6c12b-156">Wir verwenden es als Ausgangspunkt unserer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="6c12b-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="6c12b-157">Testen der NerdDinner-Anwendung</span><span class="sxs-lookup"><span data-stu-id="6c12b-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="6c12b-158">Wenn wir die Professional Edition oder eine höhere Version von Visual Studio 2008 verwenden, können wir die integrierte Komponententest-IDE-Unterstützung in Visual Studio verwenden, um das Projekt zu testen:</span><span class="sxs-lookup"><span data-stu-id="6c12b-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="6c12b-159">Wenn Sie eine der oben genannten Optionen auswählen, wird der Bereich "Testergebnisse" innerhalb der IDE geöffnet und uns der Status "Pass/Fail" für die 27 Komponententests in unserem neuen Projekt angezeigt, die die integrierte Funktionalität abdecken:</span><span class="sxs-lookup"><span data-stu-id="6c12b-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="6c12b-160">Später in diesem Tutorial werden wir mehr über automatisierte Tests sprechen und zusätzliche Komponententests hinzufügen, die die von uns implementierten Anwendungsfunktionen abdecken.</span><span class="sxs-lookup"><span data-stu-id="6c12b-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="6c12b-161">Nächster Schritt</span><span class="sxs-lookup"><span data-stu-id="6c12b-161">Next Step</span></span>

<span data-ttu-id="6c12b-162">Wir haben jetzt eine grundlegende Anwendungsstruktur eingerichtet.</span><span class="sxs-lookup"><span data-stu-id="6c12b-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="6c12b-163">Erstellen wir nun [eine Datenbank zum Speichern unserer Anwendungsdaten](create-a-database.md).</span><span class="sxs-lookup"><span data-stu-id="6c12b-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6c12b-164">[Zurück](introducing-the-nerddinner-tutorial.md)
> [Weiter](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="6c12b-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
