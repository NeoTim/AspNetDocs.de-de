---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 'Teil 4: Hinzufügen einer-Administratoransicht | Microsoft-Dokumentation'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 54b3afac9b19962b02336a35909b208c4e3f7504
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400554"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="87f62-102">Teil 4: Hinzufügen einer-Administratoransicht</span><span class="sxs-lookup"><span data-stu-id="87f62-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="87f62-103">durch [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="87f62-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="87f62-104">Abgeschlossenes Projekt herunterladen</span><span class="sxs-lookup"><span data-stu-id="87f62-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="87f62-105">Hinzufügen einer-Administratoransicht</span><span class="sxs-lookup"><span data-stu-id="87f62-105">Add an Admin View</span></span>

<span data-ttu-id="87f62-106">Nun wir auf der Clientseite zu aktivieren, und fügen Sie eine Seite, die Daten über den Admin-Controller verwenden.</span><span class="sxs-lookup"><span data-stu-id="87f62-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="87f62-107">Die Seite können Benutzer zu erstellen, bearbeiten oder Löschen von Produkten, per AJAX-Anforderungen an den Controller.</span><span class="sxs-lookup"><span data-stu-id="87f62-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="87f62-108">Klicken Sie im Projektmappen-Explorer erweitern Sie den Ordner "Controllers", und öffnen Sie die Datei mit dem Namen "HomeController.cs".</span><span class="sxs-lookup"><span data-stu-id="87f62-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="87f62-109">Diese Datei enthält einen MVC-Controller.</span><span class="sxs-lookup"><span data-stu-id="87f62-109">This file contains an MVC controller.</span></span> <span data-ttu-id="87f62-110">Fügen Sie eine Methode mit dem Namen `Admin`:</span><span class="sxs-lookup"><span data-stu-id="87f62-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="87f62-111">Die **HttpRouteUrl** Methode erstellt den URI der Web-API, und wir dies in den ansichtsbehälter zur späteren Verwendung speichern.</span><span class="sxs-lookup"><span data-stu-id="87f62-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="87f62-112">Als Nächstes, positionieren Sie den Textcursor in den `Admin` Aktionsmethode, und klicken Sie dann mit der rechten Maustaste und wählen **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="87f62-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="87f62-113">Hierdurch wird die **Ansicht hinzufügen** Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="87f62-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="87f62-114">In der **Ansicht hinzufügen** Dialogfeld Namen der Ansicht "Admin".</span><span class="sxs-lookup"><span data-stu-id="87f62-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="87f62-115">Aktivieren Sie das Kontrollkästchen mit der Bezeichnung **eine stark typisierte Ansicht erstellen**.</span><span class="sxs-lookup"><span data-stu-id="87f62-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="87f62-116">Klicken Sie unter **Modellklasse**, wählen Sie "Product (ProductStore.Models)".</span><span class="sxs-lookup"><span data-stu-id="87f62-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="87f62-117">Behalten Sie alle anderen Optionen die Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="87f62-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="87f62-118">Auf **hinzufügen** Fügt eine Datei mit dem Namen Admin.cshtml unter Views/Home.</span><span class="sxs-lookup"><span data-stu-id="87f62-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="87f62-119">Öffnen Sie diese Datei, und fügen Sie folgenden HTML-Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="87f62-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="87f62-120">Dieser HTML-Code definiert die Struktur der Seite, aber keine Funktionen läuft noch.</span><span class="sxs-lookup"><span data-stu-id="87f62-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="87f62-121">Erstellen Sie einen Link auf der Seite "Administrator"</span><span class="sxs-lookup"><span data-stu-id="87f62-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="87f62-122">Klicken Sie im Projektmappen-Explorer erweitern Sie den Ordner "Views", und erweitern Sie dann den Ordner Shared.</span><span class="sxs-lookup"><span data-stu-id="87f62-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="87f62-123">Öffnen Sie die Datei mit dem Namen \_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="87f62-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="87f62-124">Suchen Sie die **Ul** Element mit der Id = "Menu" und einen Aktionslink für die Admin-Ansicht:</span><span class="sxs-lookup"><span data-stu-id="87f62-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="87f62-125">Im Beispielprojekt habe ich ein paar andere kosmetischen Änderungen ermöglicht, z. B. ersetzt die Zeichenfolge "Ihr Logo hier einfügen" vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="87f62-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="87f62-126">Dies betrifft nicht die Funktionalität der Anwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="87f62-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="87f62-127">Sie können das Projekt herunterladen und vergleichen Sie die Dateien.</span><span class="sxs-lookup"><span data-stu-id="87f62-127">You can download the project and compare the files.</span></span>


<span data-ttu-id="87f62-128">Führen Sie die Anwendung, und klicken Sie auf den Link "Admin", der am oberen Rand der Startseite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="87f62-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="87f62-129">Die Seite "Administrator" sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="87f62-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="87f62-130">Rechts jetzt die Seite nicht.</span><span class="sxs-lookup"><span data-stu-id="87f62-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="87f62-131">Im nächsten Abschnitt verwenden wir "Knockout.js" zum Erstellen einer dynamischen Benutzeroberflächenautomatisierungs.</span><span class="sxs-lookup"><span data-stu-id="87f62-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="87f62-132">Autorisierung hinzufügen</span><span class="sxs-lookup"><span data-stu-id="87f62-132">Add Authorization</span></span>

<span data-ttu-id="87f62-133">Die Seite "Administrator" ist derzeit für alle Benutzer Zugriff auf die Website zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="87f62-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="87f62-134">Wir ändern Sie diese Option, um die Berechtigungen für Administratoren einschränken.</span><span class="sxs-lookup"><span data-stu-id="87f62-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="87f62-135">Durch Hinzufügen einer Rolle "Administrator" und einen Benutzer mit Administratorrechten starten.</span><span class="sxs-lookup"><span data-stu-id="87f62-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="87f62-136">Klicken Sie im Projektmappen-Explorer erweitern Sie den Filter-Ordner, und öffnen Sie die Datei mit dem Namen InitializeSimpleMembershipAttribute.cs.</span><span class="sxs-lookup"><span data-stu-id="87f62-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="87f62-137">Suchen Sie die `SimpleMembershipInitializer` Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="87f62-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="87f62-138">Nach dem Aufruf von **WebSecurity.InitializeDatabaseConnection**, fügen Sie den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="87f62-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="87f62-139">Dies ist eine schnelle Möglichkeit zum Hinzufügen der Rolle "Administrator", und erstellen Sie einen Benutzer für die Rolle.</span><span class="sxs-lookup"><span data-stu-id="87f62-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="87f62-140">Klicken Sie im Projektmappen-Explorer erweitern Sie den Ordner "Controllers", und öffnen Sie die Datei "HomeController.cs".</span><span class="sxs-lookup"><span data-stu-id="87f62-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="87f62-141">Hinzufügen der **autorisieren** -Attribut auf die `Admin` Methode.</span><span class="sxs-lookup"><span data-stu-id="87f62-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="87f62-142">Öffnen Sie die Datei AdminController.cs und Hinzufügen der **autorisieren** -Attribut auf die gesamte `AdminController` Klasse.</span><span class="sxs-lookup"><span data-stu-id="87f62-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="87f62-143">MVC und Web-API, die beide definieren **autorisieren** Attribute, die in verschiedenen Namespaces.</span><span class="sxs-lookup"><span data-stu-id="87f62-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="87f62-144">MVC verwendet **System.Web.Mvc.AuthorizeAttribute**, während die Web-API verwendet **"System.Web.http.AuthorizeAttribute"**.</span><span class="sxs-lookup"><span data-stu-id="87f62-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>


<span data-ttu-id="87f62-145">Nur Administratoren können jetzt die Seite "Administrator" anzeigen.</span><span class="sxs-lookup"><span data-stu-id="87f62-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="87f62-146">Wenn Sie mit dem Admin-Controller eine HTTP-Anforderung senden, muss die Anforderung außerdem ein Authentifizierungscookie enthalten.</span><span class="sxs-lookup"><span data-stu-id="87f62-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="87f62-147">Wenn dies nicht der Fall ist, wird der Server sendet eine HTTP 401 (nicht autorisiert)-Antwort.</span><span class="sxs-lookup"><span data-stu-id="87f62-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="87f62-148">Dies sehen Sie in Fiddler durch Senden einer GET-Anforderung zu `http://localhost:*port*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="87f62-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="87f62-149">[Zurück](using-web-api-with-entity-framework-part-3.md)
> [Weiter](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="87f62-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
