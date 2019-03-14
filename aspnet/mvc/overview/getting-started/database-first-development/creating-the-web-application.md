---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Tutorial: Erstellen Sie die der Webanwendung und Datenmodelle für EF Database First mit ASP.NET MVC'
description: Dieses Tutorial konzentriert sich auf die Webanwendung erstellen und das Generieren von Datenmodelle auf Grundlage von Datenbanktabellen.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: dced55386c3f810e406c5c2b3f0071b45e3b2dbd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041577"
---
# <a name="tutorial-create-the-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="2fa04-103">Tutorial: Erstellen Sie die der Webanwendung und Datenmodelle für EF Database First mit ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="2fa04-103">Tutorial: Create the the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="2fa04-104">Verwenden MVC, Entity Framework und ASP.NET-Gerüstbau, können Sie eine Webanwendung erstellen, die eine Schnittstelle für eine vorhandene Datenbank bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="2fa04-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="2fa04-105">Dieser tutorialreihe erfahren Sie, wie Sie automatisch generierter Code, der ermöglicht Benutzern das anzeigen, bearbeiten, erstellen und Löschen von Daten, die in einer Datenbanktabelle gespeichert.</span><span class="sxs-lookup"><span data-stu-id="2fa04-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="2fa04-106">Der generierte Code entspricht die Spalten in der Datenbanktabelle.</span><span class="sxs-lookup"><span data-stu-id="2fa04-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="2fa04-107">Dieses Tutorial konzentriert sich auf die Webanwendung erstellen und das Generieren von Datenmodelle auf Grundlage von Datenbanktabellen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="2fa04-108">In diesem Tutorial:</span><span class="sxs-lookup"><span data-stu-id="2fa04-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2fa04-109">Erstellen einer ASP.NET-Web-App</span><span class="sxs-lookup"><span data-stu-id="2fa04-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="2fa04-110">Die Modelle generieren</span><span class="sxs-lookup"><span data-stu-id="2fa04-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fa04-111">Vorraussetzungen</span><span class="sxs-lookup"><span data-stu-id="2fa04-111">Prerequisites</span></span>

* [<span data-ttu-id="2fa04-112">Erste Schritte mit Entity Framework 6 Database First anhand von MVC 5</span><span class="sxs-lookup"><span data-stu-id="2fa04-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="2fa04-113">Erstellen einer ASP.NET-Web-App</span><span class="sxs-lookup"><span data-stu-id="2fa04-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="2fa04-114">Erstellen Sie ein neues Projekt in Visual Studio in einer neuen Projektmappe oder der gleichen Projektmappe wie das Projekt, und wählen Sie die **ASP.NET-Webanwendung** Vorlage.</span><span class="sxs-lookup"><span data-stu-id="2fa04-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="2fa04-115">Nennen Sie das Projekt **ContosoSite**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-115">Name the project **ContosoSite**.</span></span>

![Projekt erstellen](creating-the-web-application/_static/image1.png)

<span data-ttu-id="2fa04-117">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-117">Click **OK**.</span></span>

<span data-ttu-id="2fa04-118">Wählen Sie im Fenster Neues ASP.NET-Projekt die **MVC** Vorlage.</span><span class="sxs-lookup"><span data-stu-id="2fa04-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="2fa04-119">Sie können löschen, die **in der Cloud hosten** option jetzt, da Sie später die Anwendung in der Cloud bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="2fa04-120">Klicken Sie auf **OK** zum Erstellen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="2fa04-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="2fa04-121">Das Projekt wird mit der Standarddateien und Ordner erstellt.</span><span class="sxs-lookup"><span data-stu-id="2fa04-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="2fa04-122">In diesem Tutorial verwenden Sie Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="2fa04-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="2fa04-123">Sie können die Version von Entity Framework Vergewissern Sie sich in Ihrem Projekt über das Fenster "NuGet-Pakete verwalten".</span><span class="sxs-lookup"><span data-stu-id="2fa04-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="2fa04-124">Aktualisieren Sie Ihre Version von Entity Framework, bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="2fa04-124">If necessary, update your version of Entity Framework.</span></span>

![Version anzeigen](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="2fa04-126">Die Modelle generieren</span><span class="sxs-lookup"><span data-stu-id="2fa04-126">Generate the models</span></span>

<span data-ttu-id="2fa04-127">Erstellen Sie jetzt Entity Framework-Modellen aus den Datenbanktabellen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="2fa04-128">Diese Modelle sind Klassen, die Sie verwenden werden, um mit den Daten arbeiten.</span><span class="sxs-lookup"><span data-stu-id="2fa04-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="2fa04-129">Jedes Modell entspricht eine Tabelle in der Datenbank und enthält Eigenschaften, die die Spalten in der Tabelle entsprechen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="2fa04-130">Mit der rechten Maustaste die **Modelle** Ordner, und wählen **hinzufügen** und **neues Element**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="2fa04-131">Wählen Sie im Fenster "Neues Element hinzufügen", **Daten** im linken Bereich und **ADO.NET Entity Data Model** aus den Optionen im mittleren Bereich.</span><span class="sxs-lookup"><span data-stu-id="2fa04-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="2fa04-132">Nennen Sie die neue Modelldatei **ContosoModel**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="2fa04-133">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-133">Click **Add**.</span></span>

<span data-ttu-id="2fa04-134">Wählen Sie in der Assistent für Entity Data Model **EF Designer aus Datenbank**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="2fa04-135">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-135">Click **Next**.</span></span>

<span data-ttu-id="2fa04-136">Wenn Sie Verbindungen mit der Datenbank in Ihrer Entwicklungsumgebung definiert haben, sehen Sie diese Verbindungen vorab ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="2fa04-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="2fa04-137">Sie möchten jedoch eine neue Verbindung mit der Datenbank zu erstellen, die Sie im ersten Teil dieses Tutorials erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="2fa04-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="2fa04-138">Klicken Sie auf die **neue Verbindung** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="2fa04-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="2fa04-139">Geben Sie im Fenster Eigenschaften der Verbindung den Namen des lokalen Servers, in die Datenbank erstellt wurde (in diesem Fall **(Localdb) \Projects13**).</span><span class="sxs-lookup"><span data-stu-id="2fa04-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\Projects13**).</span></span> <span data-ttu-id="2fa04-140">Wählen Sie nachdem Sie den Namen des Servers haben die ContosoUniversityData aus den verfügbaren Datenbanken aus.</span><span class="sxs-lookup"><span data-stu-id="2fa04-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![Set-Verbindungseigenschaften](creating-the-web-application/_static/image8.png)

<span data-ttu-id="2fa04-142">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-142">Click **OK**.</span></span>

<span data-ttu-id="2fa04-143">Die richtige Verbindungseigenschaften werden nun angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2fa04-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="2fa04-144">Sie können den Standardnamen für die Verbindung in der Datei "Web.config" verwenden.</span><span class="sxs-lookup"><span data-stu-id="2fa04-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="2fa04-145">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-145">Click **Next**.</span></span>

<span data-ttu-id="2fa04-146">Wählen Sie die neueste Version von Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2fa04-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="2fa04-147">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-147">Click **Next**.</span></span>

<span data-ttu-id="2fa04-148">Wählen Sie **Tabellen** zum Generieren von Modellen für alle drei Tabellen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="2fa04-149">Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="2fa04-149">Click **Finish**.</span></span>

<span data-ttu-id="2fa04-150">Wenn eine sicherheitswarnung angezeigt wird, wählen Sie **OK** zum Fortsetzen der Ausführung der Vorlage.</span><span class="sxs-lookup"><span data-stu-id="2fa04-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="2fa04-151">Die Modelle aus Tabellen der Datenbank generiert wird, und ein Diagramm wird mit den Eigenschaften und Beziehungen zwischen den Tabellen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2fa04-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![Diagramm des Modells](creating-the-web-application/_static/image11.png)

<span data-ttu-id="2fa04-153">Der Ordner "Models" enthält jetzt viele neue Dateien, die im Zusammenhang mit der die Modelle, die aus der Datenbank generiert wurden.</span><span class="sxs-lookup"><span data-stu-id="2fa04-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="2fa04-154">Die **ContosoModel.Context.cs** -Datei enthält eine abgeleitete Klasse die **"DbContext"** Klasse, und stellt eine Eigenschaft für jede Modellklasse, die einer Datenbanktabelle entspricht.</span><span class="sxs-lookup"><span data-stu-id="2fa04-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="2fa04-155">Die **Course.cs**, **Enrollment.cs**, und **Student.cs** Dateien enthalten die Modellklassen, die in den Datenbanken Tabellen darstellen.</span><span class="sxs-lookup"><span data-stu-id="2fa04-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="2fa04-156">Sie werden sowohl der Context-Klasse und die Modellklassen verwenden, bei der Arbeit mit Gerüstbau.</span><span class="sxs-lookup"><span data-stu-id="2fa04-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="2fa04-157">Erstellen Sie bevor Sie mit diesem Tutorial Fortfahren das Projekt ein.</span><span class="sxs-lookup"><span data-stu-id="2fa04-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="2fa04-158">Im nächsten Abschnitt generieren Sie Code auf Grundlage der Datenmodelle, aber dieser Abschnitt funktioniert nicht, wenn das Projekt noch nicht erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="2fa04-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fa04-159">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="2fa04-159">Next steps</span></span>

<span data-ttu-id="2fa04-160">In diesem Tutorial:</span><span class="sxs-lookup"><span data-stu-id="2fa04-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2fa04-161">Erstellt eine ASP.NET Web-app</span><span class="sxs-lookup"><span data-stu-id="2fa04-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="2fa04-162">Generiert die Modelle</span><span class="sxs-lookup"><span data-stu-id="2fa04-162">Generated the models</span></span>

<span data-ttu-id="2fa04-163">Die nächsten Tutorial erfahren, wie zum Erstellen generieren Code basierend auf der Datenmodelle.</span><span class="sxs-lookup"><span data-stu-id="2fa04-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2fa04-164">Generieren von Sichten</span><span class="sxs-lookup"><span data-stu-id="2fa04-164">Generating views</span></span>](generating-views.md)