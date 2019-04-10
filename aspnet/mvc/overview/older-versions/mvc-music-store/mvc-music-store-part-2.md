---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 'Teil 2: Controller | Microsoft-Dokumentation'
author: jongalloway
description: Dieser tutorialreihe werden alle Schritte ausgeführt, um die ASP.NET MVC Music Store-beispielanwendung zu erstellen. Teil 2 werden die Controller behandelt.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: b452c59f16107be6d356f86e6c313ba3229dbce6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392754"
---
# <a name="part-2-controllers"></a><span data-ttu-id="4a4ea-104">Teil 2: Controller</span><span class="sxs-lookup"><span data-stu-id="4a4ea-104">Part 2: Controllers</span></span>

<span data-ttu-id="4a4ea-105">durch [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="4a4ea-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="4a4ea-106">Die MVC Music Store ist ein lernprogrammanwendung, die eingeführt und erläutert Schritt für Schritt, wie ASP.NET MVC und Visual Studio für die Webentwicklung verwenden.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="4a4ea-107">Die MVC Music Store ist eine Implementierung eines einfachen Beispiels die Alben online verkauft und implementiert grundlegende Verwaltung, Benutzeranmeldung und shopping Cart-Funktionalität.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="4a4ea-108">Dieser tutorialreihe werden alle Schritte ausgeführt, um die ASP.NET MVC Music Store-beispielanwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="4a4ea-109">Teil 2 werden die Controller behandelt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-109">Part 2 covers Controllers.</span></span>


<span data-ttu-id="4a4ea-110">Mit herkömmlichen Web-Frameworks werden eingehende URLs in der Regel Dateien auf dem Datenträger zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="4a4ea-111">Zum Beispiel: eine Anforderung für eine URL wie "/ Products.aspx" oder "/" Products.PHP "" kann von einer "Products.aspx" oder ""Products.PHP ""-Datei verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="4a4ea-112">Web-basierten MVC-Frameworks Servercode URLs in eine etwas andere Weise zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="4a4ea-113">Anstatt das Zuordnen von eingehenden URLs zu Dateien, sie stattdessen URLs auf Methoden in Klassen zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="4a4ea-114">Diese Klassen werden als "Controller" bezeichnet und sie sind zuständig für die Verarbeitung der eingehender HTTP-Anforderungen, Behandeln von Benutzereingaben, abrufen und Speichern von Daten und bestimmen die zu sendende Antwort zurück an den Client (HTML-Seite anzeigen, Herunterladen einer Datei, auf einen anderen umleiten URL usw.).</span><span class="sxs-lookup"><span data-stu-id="4a4ea-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="4a4ea-115">Hinzufügen einen HomeController</span><span class="sxs-lookup"><span data-stu-id="4a4ea-115">Adding a HomeController</span></span>

<span data-ttu-id="4a4ea-116">Zunächst müssen wir unsere MVC Music Store-Anwendung Hinzufügen einer Controllerklasse, die URLs, die auf der Startseite unserer Website behandelt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="4a4ea-117">Wir führen Sie die Standard-Benennungskonventionen von ASP.NET MVC und HomeController aufrufen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="4a4ea-118">Mit der rechten Maustaste in des Ordners "Controllers" im Projektmappen-Explorer, und wählen Sie "Hinzufügen", und klicken Sie dann den Befehl "Controller...":</span><span class="sxs-lookup"><span data-stu-id="4a4ea-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="4a4ea-119">Hierdurch wird das Dialogfeld "Controller hinzufügen" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="4a4ea-120">Nennen Sie den Controller "HomeController" aus, und drücken Sie die Schaltfläche "hinzufügen".</span><span class="sxs-lookup"><span data-stu-id="4a4ea-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="4a4ea-121">Dies erstellt eine neue Datei "HomeController.cs", mit dem folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="4a4ea-122">Um so weit wie möglich zu starten, ersetzen Sie die Index-Methode lassen Sie uns eine einfache Möglichkeit, die nur eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="4a4ea-123">Wir erstellen zwei Änderungen:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-123">We'll make two changes:</span></span>

- <span data-ttu-id="4a4ea-124">Ändern Sie die Methode, um eine Zeichenfolge anstatt in ein Aktionsergebnis zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="4a4ea-125">Ändern Sie die return-Anweisung um "Hello aus Home" zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="4a4ea-126">Die Methode sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="4a4ea-127">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="4a4ea-127">Running the Application</span></span>

<span data-ttu-id="4a4ea-128">Jetzt führen wir die Website.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-128">Now let's run the site.</span></span> <span data-ttu-id="4a4ea-129">Können wir unsere Web-Server starten und Testen Sie die Website mithilfe eines der folgenden:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="4a4ea-130">Wählen Sie das Debuggen ⇨ Debuggen starten im Menü-Element</span><span class="sxs-lookup"><span data-stu-id="4a4ea-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="4a4ea-131">Klicken Sie auf der grünen Pfeilschaltfläche auf der Symbolleiste</span><span class="sxs-lookup"><span data-stu-id="4a4ea-131">Click the Green arrow button in the toolbar</span></span> ![](mvc-music-store-part-2/_static/image2.jpg)
- <span data-ttu-id="4a4ea-132">Verwenden Sie die Tastenkombination F5.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="4a4ea-133">Mit einer der oben genannten Schritte wird unser Projekt kompilieren, und dann dazu führen, dass der ASP.NET Development Server, die integriert in Visual Web Developer gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="4a4ea-134">Eine Benachrichtigung wird angezeigt, in der unteren Ecke des Bildschirms, um anzugeben, dass der ASP.NET Development Server gestartet wurde, und zeigt der Portnummer an, dass er unter ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="4a4ea-135">Visual Web Developer wird dann automatisch ein Browserfenster geöffnet, dessen URL auf unsere Web-Server verweist.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="4a4ea-136">Dies ermöglicht uns, wie Sie unserer Webanwendung testen:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="4a4ea-137">Okay, das war ziemlich schnell – wir eine neue Website erstellt haben, eine Zeile mit drei-Funktion hinzugefügt, und haben wir Text in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="4a4ea-138">Nicht rocket Science, aber es ist der Anfang.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-138">Not rocket science, but it's a start.</span></span>

*<span data-ttu-id="4a4ea-139">Hinweis: Visual Web Developer bietet ASP.NET Development Server, die Ihre Website auf einer Reihe zufälliger kostenlose "Port" ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-139">Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number.</span></span> <span data-ttu-id="4a4ea-140">Im obigen Screenshot, der Standort ausgeführt wird, am `http://localhost:26641/`, sodass sie Port 26641 verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-140">In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641.</span></span> <span data-ttu-id="4a4ea-141">Die Portnummer wird unterschiedlich sein.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-141">Your port number will be different.</span></span> <span data-ttu-id="4a4ea-142">Wenn wir in diesem Tutorial zu der URL wie /Store/Browse sprechen, geht, die nach der Portnummer.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-142">When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number.</span></span> <span data-ttu-id="4a4ea-143">Wenn 26641 die Portnummer an, navigieren zu/Store/durchsuchen bedeutet Navigieren zu `http://localhost:26641/Store/Browse`.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-143">Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.</span></span>*

## <a name="adding-a-storecontroller"></a><span data-ttu-id="4a4ea-144">Hinzufügen einer StoreController</span><span class="sxs-lookup"><span data-stu-id="4a4ea-144">Adding a StoreController</span></span>

<span data-ttu-id="4a4ea-145">Wir haben einen einfachen HomeController, die auf der Startseite unserer Website implementiert hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-145">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="4a4ea-146">Nun fügen Sie einen anderen Controller, mit denen auf die Durchsuchen-Funktionalität unseres neuen Speichers Musik zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-146">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="4a4ea-147">Unser Controller Store unterstützt drei Szenarien:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-147">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="4a4ea-148">Eine Angebotsseite von Musik Genres in unserer Music store</span><span class="sxs-lookup"><span data-stu-id="4a4ea-148">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="4a4ea-149">Seite "Durchsuchen", der alle von der Alben in einem bestimmten Genre auflistet</span><span class="sxs-lookup"><span data-stu-id="4a4ea-149">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="4a4ea-150">Eine Seite, die Informationen zu einem bestimmten Musikalbum anzeigt</span><span class="sxs-lookup"><span data-stu-id="4a4ea-150">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="4a4ea-151">Wir beginnen, indem Sie eine neue StoreController-Klasse hinzufügen...</span><span class="sxs-lookup"><span data-stu-id="4a4ea-151">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="4a4ea-152">Wenn Sie noch nicht geschehen, beenden Sie die Anwendung entweder über den Browser schließen, oder wählen das Debuggen ⇨ Debuggen beenden-Menüelement ausführen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-152">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="4a4ea-153">Fügen Sie nun eine neue StoreController hinzu.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-153">Now add a new StoreController.</span></span> <span data-ttu-id="4a4ea-154">Wie wir mit HomeController, wir erreichen dies, indem mit der rechten Maustaste auf den Ordner "Controllers" im Projektmappen-Explorer und Auswählen der hinzufügen -&gt;Controller-Menüelement</span><span class="sxs-lookup"><span data-stu-id="4a4ea-154">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="4a4ea-155">Unsere neue StoreController verfügt bereits über eine Methode "Index".</span><span class="sxs-lookup"><span data-stu-id="4a4ea-155">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="4a4ea-156">Wir verwenden diese Methode "Index" auf um unserer Seite mit den Preisen zu implementieren, die alle Genres in unserer Music Store auflistet.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-156">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="4a4ea-157">Wir fügen auch zwei weitere Methoden, um die beiden anderen Szenarien implementieren, die wir unsere StoreController behandeln soll: Durchsuchen und Details.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-157">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="4a4ea-158">Diese Methoden ("Index", "Durchsuchen" und "Details") in den Controller "Controlleraktionen" aufgerufen werden, und wie Sie mit der HomeController.Index ()-Aktionsmethode bereits gesehen haben, ist ihre Arbeit auf URL-Anforderungen zu reagieren, und (im Allgemeinen) zu ermitteln welcher Inhalt sollten gesendet werden, zurück an den Browser oder die Benutzer, die die URL aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-158">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="4a4ea-159">Wird zunächst unsere Implementierung StoreController ändern theIndex()-Methode, um die Zeichenfolge "Hello aus Store.Index()" zurückzugeben, und fügen es ähnliche Methoden für Browse() und Details():</span><span class="sxs-lookup"><span data-stu-id="4a4ea-159">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="4a4ea-160">Führen Sie das Projekt erneut aus, und Durchsuchen Sie die folgenden URLs:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-160">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="4a4ea-161">/Store</span><span class="sxs-lookup"><span data-stu-id="4a4ea-161">/Store</span></span>
- <span data-ttu-id="4a4ea-162">/ Store/durchsuchen</span><span class="sxs-lookup"><span data-stu-id="4a4ea-162">/Store/Browse</span></span>
- <span data-ttu-id="4a4ea-163">/ Store/Details</span><span class="sxs-lookup"><span data-stu-id="4a4ea-163">/Store/Details</span></span>

<span data-ttu-id="4a4ea-164">Zugriff auf diese URLs werden Aufrufen die Aktionsmethoden in unserem Controller und String-Antworten zurückgeben:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-164">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="4a4ea-165">Das ist großartig, aber dies sind nur Konstanten Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-165">That's great, but these are just constant strings.</span></span> <span data-ttu-id="4a4ea-166">Lassen Sie uns diese dynamisch, damit sie nutzen Informationen aus der URL, und sie auf der Seite ausgegeben zeigt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-166">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="4a4ea-167">Zuerst ändern wir die Aktionsmethode durchsuchen, um eine Querystring-Wert aus der URL abzurufen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-167">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="4a4ea-168">Dazu können wir unsere Aktionsmethode einen Parameter für "Genre" hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-168">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="4a4ea-169">Wenn wir dies tun übergibt ASP.NET MVC automatisch alle Querystring oder Formular Post-Parameter, die mit dem Namen "Genre" in unserem Aktionsmethode, wenn sie aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-169">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*<span data-ttu-id="4a4ea-170">Hinweis: HttpUtility.HtmlEncode Durchführen der Hilfsmethode verwendet, um die Benutzereingabe zu bereinigen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-170">Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input.</span></span> <span data-ttu-id="4a4ea-171">Dadurch wird verhindert, dass Benutzer Einfügen von Javascript in unserer Ansicht mit einem Link wie /Store/Browse? Genre =&lt;Skript&gt;Window.Location = "http://hackersite.com"&lt;/script&gt;.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-171">This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.</span></span>*

<span data-ttu-id="4a4ea-172">Nun navigieren wir zu/Store/durchsuchen? Genre = Disco</span><span class="sxs-lookup"><span data-stu-id="4a4ea-172">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="4a4ea-173">Als Nächstes ändern wir die Aktion "Details" zum Lesen und Anzeigen der Eingabeparameter mit dem Namen ID.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-173">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="4a4ea-174">Im Gegensatz zu unseren vorherigen Methode wird nicht wir den ID-Wert als Querystring-Parameter einbetten.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-174">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="4a4ea-175">Stattdessen werden wir es direkt in der URL selbst einbetten.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-175">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="4a4ea-176">Zum Beispiel: /Store/Details/5.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-176">For example: /Store/Details/5.</span></span>

<span data-ttu-id="4a4ea-177">ASP.NET MVC ermöglicht es uns, problemlos erreichen, ohne etwas konfigurieren zu müssen.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-177">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="4a4ea-178">Routing ASP.NETs Standardkonvention ist, das eine URL-Segment nach dem Namen der Aktionsmethode als einen Parameter namens "ID" zu behandeln.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-178">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="4a4ea-179">Wenn Ihrer Aktionsmethode einen Parameter namens-ID hat wird ASP.NET MVC automatisch das URL-Segment für Sie als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-179">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="4a4ea-180">Führen Sie die Anwendung, und navigieren Sie zu /Store/Details/5:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-180">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="4a4ea-181">Betrachten wir nun, was wir bisher gemacht haben:</span><span class="sxs-lookup"><span data-stu-id="4a4ea-181">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="4a4ea-182">Wir haben ein neues ASP.NET MVC-Projekt in Visual Web Developer erstellt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-182">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="4a4ea-183">Wir haben die grundlegenden Ordnerstruktur einer ASP.NET MVC-Anwendung erläutert.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-183">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="4a4ea-184">Wir haben wie unsere Website, die mithilfe von ASP.NET Development Server ausgeführt werden gelernt.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-184">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="4a4ea-185">Wir haben zwei Controller-Klassen erstellt: einen HomeController, und eine StoreController</span><span class="sxs-lookup"><span data-stu-id="4a4ea-185">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="4a4ea-186">Wir haben Aktionsmethoden unsere-Controller hinzugefügt, das auf URL-Anforderungen reagieren und Text an den Browser zurück.</span><span class="sxs-lookup"><span data-stu-id="4a4ea-186">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="4a4ea-187">[Zurück](mvc-music-store-part-1.md)
> [Weiter](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="4a4ea-187">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
