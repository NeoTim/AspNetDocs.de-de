---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: Abrufen und Anzeigen von Daten mit Modell Bindung und Web Forms | Microsoft-Dokumentation
author: Rick-Anderson
description: In dieser tutorialreihe werden grundlegende Aspekte der Verwendung der Modell Bindung mit einem ASP.net Web Forms-Projekt veranschaulicht. Die Modell Bindung führt zu einer geraden Daten Interaktion-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240746"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="bc986-104">Abrufen und Anzeigen von Daten mit Modell Bindung und Web Forms</span><span class="sxs-lookup"><span data-stu-id="bc986-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="bc986-105">In dieser tutorialreihe werden grundlegende Aspekte der Verwendung der Modell Bindung mit einem ASP.net Web Forms-Projekt veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="bc986-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="bc986-106">Die Modell Bindung sorgt für eine genauere Daten Interaktion als bei der Verarbeitung von Datenquellen Objekten (z. b. ObjectDataSource oder SqlDataSource).</span><span class="sxs-lookup"><span data-stu-id="bc986-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="bc986-107">Diese Serie beginnt mit Einführungs Material und wechselt in spätere Tutorials zu erweiterten Konzepten.</span><span class="sxs-lookup"><span data-stu-id="bc986-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="bc986-108">Das Modell bindungsmuster funktioniert mit jeder Datenzugriffs Technologie.</span><span class="sxs-lookup"><span data-stu-id="bc986-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="bc986-109">In diesem Tutorial verwenden Sie Entity Framework, aber Sie können die Datenzugriffs Technologie verwenden, die Ihnen am meisten vertraut ist.</span><span class="sxs-lookup"><span data-stu-id="bc986-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="bc986-110">Über ein Daten gebundenes Server Steuerelement, z. b. ein GridView-, ListView-, DetailsView-oder FormView-Steuerelement, geben Sie die Namen der Methoden an, die zum auswählen, aktualisieren, löschen und Erstellen von Daten verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="bc986-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="bc986-111">In diesem Tutorial geben Sie einen Wert für die SelectMethod-Methode an.</span><span class="sxs-lookup"><span data-stu-id="bc986-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="bc986-112">Innerhalb dieser Methode stellen Sie die Logik zum Abrufen der Daten bereit.</span><span class="sxs-lookup"><span data-stu-id="bc986-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="bc986-113">Im nächsten Tutorial legen Sie Werte für UpdateMethod, DeleteMethod und InsertMethod fest.</span><span class="sxs-lookup"><span data-stu-id="bc986-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="bc986-114">Sie können das gesamte Projekt in c# oder Visual Basic [herunterladen](https://go.microsoft.com/fwlink/?LinkId=286116) .</span><span class="sxs-lookup"><span data-stu-id="bc986-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="bc986-115">Der herunterladbare Code funktioniert mit Visual Studio 2012 und höher.</span><span class="sxs-lookup"><span data-stu-id="bc986-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="bc986-116">Dabei wird die Vorlage Visual Studio 2012 verwendet, die sich geringfügig von der in diesem Tutorial gezeigten Vorlage in Visual Studio 2017 unterscheidet.</span><span class="sxs-lookup"><span data-stu-id="bc986-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="bc986-117">In diesem Tutorial führen Sie die Anwendung in Visual Studio aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="bc986-118">Sie können die Anwendung auch für einen Hostinganbieter bereitstellen und über das Internet verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="bc986-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="bc986-119">Microsoft bietet kostenloses Webhosting für bis zu 10 Websites in einer</span><span class="sxs-lookup"><span data-stu-id="bc986-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="bc986-120">[Kostenloses Azure-Testkonto](https://azure.microsoft.com/free/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="bc986-120">[free Azure trial account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="bc986-121">Informationen zum Bereitstellen eines Visual Studio-Webprojekts für die Azure App Service von Web-Apps finden Sie unter [ASP.net Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) Series.</span><span class="sxs-lookup"><span data-stu-id="bc986-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="bc986-122">In diesem Tutorial erfahren Sie außerdem, wie Sie Entity Framework Code First-Migrationen zum Bereitstellen Ihrer SQL Server-Datenbank in Azure SQL-Datenbank verwenden.</span><span class="sxs-lookup"><span data-stu-id="bc986-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bc986-123">Im Tutorial verwendete Software Versionen</span><span class="sxs-lookup"><span data-stu-id="bc986-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="bc986-124">Microsoft Visual Studio 2017 oder Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="bc986-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="bc986-125">Dieses Tutorial funktioniert auch mit Visual Studio 2012 und Visual Studio 2013. es gibt jedoch einige Unterschiede in der Benutzeroberfläche und der Projektvorlage.</span><span class="sxs-lookup"><span data-stu-id="bc986-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="bc986-126">Was Sie erstellen</span><span class="sxs-lookup"><span data-stu-id="bc986-126">What you'll build</span></span>

<span data-ttu-id="bc986-127">In diesem Tutorial gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="bc986-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="bc986-128">Erstellen von Datenobjekten, die eine Universität mit Studenten widerspiegeln, die in Kursen angemeldet sind</span><span class="sxs-lookup"><span data-stu-id="bc986-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="bc986-129">Erstellen von Datenbanktabellen aus den Objekten</span><span class="sxs-lookup"><span data-stu-id="bc986-129">Build database tables from the objects</span></span>
* <span data-ttu-id="bc986-130">Auffüllen der Datenbank mit Testdaten</span><span class="sxs-lookup"><span data-stu-id="bc986-130">Populate the database with test data</span></span>
* <span data-ttu-id="bc986-131">Anzeigen von Daten in einem Webformular</span><span class="sxs-lookup"><span data-stu-id="bc986-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="bc986-132">Erstellen des Projekts</span><span class="sxs-lookup"><span data-stu-id="bc986-132">Create the project</span></span>

1. <span data-ttu-id="bc986-133">Erstellen Sie in Visual Studio 2017 ein Projekt mit dem Namen " **contosouniversitymodelbinding**" der **ASP.NET-Webanwendung (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="bc986-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![Erstellen des Projekts](retrieving-data/_static/image19.png)

2. <span data-ttu-id="bc986-135">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc986-135">Select **OK**.</span></span> <span data-ttu-id="bc986-136">Das Dialogfeld zum Auswählen einer Vorlage wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bc986-136">The dialog box to select a template appears.</span></span>

   ![Auswählen von Web Forms](retrieving-data/_static/image3.png)

3. <span data-ttu-id="bc986-138">Wählen Sie die **Web Forms** Vorlage aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="bc986-139">Ändern Sie ggf. die Authentifizierung in **einzelne Benutzerkonten**.</span><span class="sxs-lookup"><span data-stu-id="bc986-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="bc986-140">Klicken Sie auf **OK**, um das Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="bc986-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="bc986-141">Website Darstellung ändern</span><span class="sxs-lookup"><span data-stu-id="bc986-141">Modify site appearance</span></span>

   <span data-ttu-id="bc986-142">Nehmen Sie einige Änderungen vor, um das Erscheinungsbild der Website anzupassen.</span><span class="sxs-lookup"><span data-stu-id="bc986-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="bc986-143">Öffnen Sie die Datei Site. Master.</span><span class="sxs-lookup"><span data-stu-id="bc986-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="bc986-144">Ändern Sie den Titel, um die "The **University** " und nicht die **ASP.NET-Anwendung**anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="bc986-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="bc986-145">Ändern Sie den Header Text vom **Anwendungsnamen** in die **Datei**"Configuration Manager".</span><span class="sxs-lookup"><span data-stu-id="bc986-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="bc986-146">Ändern Sie die Navigations Header Links zu den entsprechenden Websites.</span><span class="sxs-lookup"><span data-stu-id="bc986-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="bc986-147">Entfernen Sie die Links für " **about** " und " **Contact** ", und verknüpfen Sie die Seite mit der Seite " **Studenten** ", die Sie erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="bc986-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="bc986-148">Speichern Sie Site. Master.</span><span class="sxs-lookup"><span data-stu-id="bc986-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="bc986-149">Hinzufügen eines Webformulars zum Anzeigen von Studenten Daten</span><span class="sxs-lookup"><span data-stu-id="bc986-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="bc986-150">Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** und dann **Neues Element**aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="bc986-151">Wählen Sie im Dialogfeld **Neues Element hinzufügen** das **Webformular mit der Vorlage Master Seite** aus, und nennen Sie es **students. aspx**.</span><span class="sxs-lookup"><span data-stu-id="bc986-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![Seite erstellen](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="bc986-153">Wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="bc986-154">Wählen Sie für die Master Seite des Webformulars die Option **Site. Master**aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="bc986-155">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc986-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="bc986-156">Datenmodell hinzufügen</span><span class="sxs-lookup"><span data-stu-id="bc986-156">Add the data model</span></span>

<span data-ttu-id="bc986-157">Fügen Sie im Ordner **Models** eine Klasse mit dem Namen **UniversityModels.cs**hinzu.</span><span class="sxs-lookup"><span data-stu-id="bc986-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="bc986-158">Klicken Sie mit der rechten Maustaste auf **Modelle**, und wählen Sie **Hinzufügen**und **Neues Element**aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="bc986-159">Das Dialogfeld **Neues Element hinzufügen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bc986-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="bc986-160">Klicken Sie im linken Navigationsmenü auf **Code**und dann auf **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="bc986-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![Modell Klasse erstellen](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="bc986-162">Benennen Sie die Klasse **UniversityModels.cs** , und wählen Sie **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="bc986-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="bc986-163">Definieren Sie in dieser Datei die `SchoolContext` `Student` Klassen,, `Enrollment` und `Course` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="bc986-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="bc986-164">Die `SchoolContext` -Klasse wird von abgeleitet `DbContext` , die die Datenbankverbindung und Änderungen an den Daten verwaltet.</span><span class="sxs-lookup"><span data-stu-id="bc986-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="bc986-165">`Student`Beachten Sie in der-Klasse die Attribute, die auf die `FirstName` Eigenschaften, und angewendet werden `LastName` `Year` .</span><span class="sxs-lookup"><span data-stu-id="bc986-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="bc986-166">In diesem Tutorial werden diese Attribute für die Datenüberprüfung verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc986-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="bc986-167">Um den Code zu vereinfachen, werden nur diese Eigenschaften mit Daten Validierungs Attributen gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="bc986-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="bc986-168">In einem echten Projekt würden Sie Validierungs Attribute auf alle Eigenschaften anwenden, die überprüft werden müssen.</span><span class="sxs-lookup"><span data-stu-id="bc986-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="bc986-169">Speichern Sie UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="bc986-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="bc986-170">Einrichten der Datenbank auf der Grundlage von Klassen</span><span class="sxs-lookup"><span data-stu-id="bc986-170">Set up the database based on classes</span></span>

<span data-ttu-id="bc986-171">In diesem Tutorial werden [Code First-Migrationen](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) zum Erstellen von Objekten und Datenbanktabellen verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc986-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="bc986-172">In diesen Tabellen werden Informationen zu den Studenten und deren Kursen gespeichert.</span><span class="sxs-lookup"><span data-stu-id="bc986-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="bc986-173">Klicken Sie auf **Extras** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole**.</span><span class="sxs-lookup"><span data-stu-id="bc986-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="bc986-174">Führen Sie in der **Paket-Manager-Konsole**den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="bc986-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="bc986-175">Wenn der Befehl erfolgreich abgeschlossen wurde, wird eine Meldung angezeigt, die besagt, dass Migrationen aktiviert wurden.</span><span class="sxs-lookup"><span data-stu-id="bc986-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![Migrationen aktivieren](retrieving-data/_static/image8.png)

      <span data-ttu-id="bc986-177">Beachten Sie, dass eine Datei mit dem Namen *Configuration.cs* erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="bc986-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="bc986-178">Die- `Configuration` Klasse verfügt über eine- `Seed` Methode, mit der die Datenbanktabellen mit Testdaten vorab aufgefüllt werden können.</span><span class="sxs-lookup"><span data-stu-id="bc986-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="bc986-179">Vorab Auffüllen der Datenbank</span><span class="sxs-lookup"><span data-stu-id="bc986-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="bc986-180">Öffnen Sie Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="bc986-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="bc986-181">Fügen Sie der `Seed` -Methode folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="bc986-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="bc986-182">Fügen Sie außerdem eine- `using` Anweisung für den- `ContosoUniversityModelBinding. Models` Namespace hinzu.</span><span class="sxs-lookup"><span data-stu-id="bc986-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="bc986-183">Speichern Sie Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="bc986-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="bc986-184">Führen Sie in der Paket-Manager-Konsole den Befehl **Add-Migration Initial**aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="bc986-185">Führen Sie den Befehl **Update-Database**aus.</span><span class="sxs-lookup"><span data-stu-id="bc986-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="bc986-186">Wenn Sie beim Ausführen dieses Befehls eine Ausnahme erhalten, können sich die `StudentID` `CourseID` Werte und von den `Seed` Methoden Werten unterscheiden.</span><span class="sxs-lookup"><span data-stu-id="bc986-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="bc986-187">Öffnen Sie diese Datenbanktabellen, und suchen Sie nach vorhandenen Werten für `StudentID` und `CourseID` .</span><span class="sxs-lookup"><span data-stu-id="bc986-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="bc986-188">Fügen Sie diese Werte dem Code für das Seeding der `Enrollments` Tabelle hinzu.</span><span class="sxs-lookup"><span data-stu-id="bc986-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="bc986-189">Hinzufügen eines GridView-Steuer Elements</span><span class="sxs-lookup"><span data-stu-id="bc986-189">Add a GridView control</span></span>

<span data-ttu-id="bc986-190">Mit aufgefüllten Datenbankdaten sind Sie nun bereit, diese Daten abzurufen und anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="bc986-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="bc986-191">Öffnen Sie students. aspx.</span><span class="sxs-lookup"><span data-stu-id="bc986-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="bc986-192">Suchen Sie den `MainContent` Platzhalter.</span><span class="sxs-lookup"><span data-stu-id="bc986-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="bc986-193">Fügen Sie innerhalb dieses Platzhalters ein **GridView** -Steuerelement hinzu, das diesen Code enthält.</span><span class="sxs-lookup"><span data-stu-id="bc986-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="bc986-194">Hinweise:</span><span class="sxs-lookup"><span data-stu-id="bc986-194">Things to note:</span></span>
   * <span data-ttu-id="bc986-195">Beachten Sie den Wert, der für die- `SelectMethod` Eigenschaft im GridView-Element festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="bc986-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="bc986-196">Dieser Wert gibt die Methode an, die zum Abrufen von GridView-Daten verwendet wird, die Sie im nächsten Schritt erstellen.</span><span class="sxs-lookup"><span data-stu-id="bc986-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="bc986-197">Die- `ItemType` Eigenschaft wird auf die `Student` zuvor erstellte-Klasse festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bc986-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="bc986-198">Diese Einstellung ermöglicht es Ihnen, auf Klasseneigenschaften im Markup zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="bc986-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="bc986-199">Beispielsweise verfügt die- `Student` Klasse über eine Auflistung mit dem Namen `Enrollments` .</span><span class="sxs-lookup"><span data-stu-id="bc986-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="bc986-200">Sie können verwenden `Item.Enrollments` , um diese Auflistung abzurufen, und dann die [LINQ-Syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) verwenden, um die registrierte Gutschriften Summe jedes Studenten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="bc986-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="bc986-201">Speichern Sie students. aspx.</span><span class="sxs-lookup"><span data-stu-id="bc986-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="bc986-202">Hinzufügen von Code zum Abrufen von Daten</span><span class="sxs-lookup"><span data-stu-id="bc986-202">Add code to retrieve data</span></span>

   <span data-ttu-id="bc986-203">Fügen Sie in der Code Behind-Datei students. aspx die für den Wert angegebene Methode hinzu `SelectMethod` .</span><span class="sxs-lookup"><span data-stu-id="bc986-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="bc986-204">Öffnen Sie students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="bc986-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="bc986-205">Fügen Sie `using` -Anweisungen für die `ContosoUniversityModelBinding. Models` `System.Data.Entity` Namespaces und hinzu.</span><span class="sxs-lookup"><span data-stu-id="bc986-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="bc986-206">Fügen Sie die Methode hinzu, die Sie für angegeben haben `SelectMethod` :</span><span class="sxs-lookup"><span data-stu-id="bc986-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="bc986-207">Die- `Include` Klausel verbessert die Abfrageleistung, ist aber nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="bc986-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="bc986-208">Ohne die- `Include` Klausel werden die Daten mit [*Lazy Loading*](https://en.wikipedia.org/wiki/Lazy_loading)abgerufen. Dies umfasst das Senden einer separaten Abfrage an die Datenbank, wenn verknüpfte Daten abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="bc986-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="bc986-209">Mit der- `Include` Klausel werden Daten mithilfe von *Eager Loading*abgerufen. Dies bedeutet, dass eine einzelne Datenbankabfrage alle zugehörigen Daten abruft.</span><span class="sxs-lookup"><span data-stu-id="bc986-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="bc986-210">Wenn verwandte Daten nicht verwendet werden, ist Eager Loading weniger effizient, da mehr Daten abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="bc986-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="bc986-211">In diesem Fall bietet Eager Loading jedoch die beste Leistung, da die zugehörigen Daten für jeden Datensatz angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bc986-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="bc986-212">Weitere Informationen zu Leistungs Überlegungen beim Laden von verknüpften Daten finden Sie im Artikel **Lazy, eifrig und Explizites Laden verwandter Daten** im Artikel [Lesen verwandter Daten mit dem Entity Framework in einer ASP.NET MVC-Anwendung](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) .</span><span class="sxs-lookup"><span data-stu-id="bc986-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="bc986-213">Standardmäßig werden die Daten nach den Werten der als Schlüssel markierten Eigenschaft sortiert.</span><span class="sxs-lookup"><span data-stu-id="bc986-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="bc986-214">Sie können eine- `OrderBy` Klausel hinzufügen, um einen anderen Sortier Wert anzugeben.</span><span class="sxs-lookup"><span data-stu-id="bc986-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="bc986-215">In diesem Beispiel wird die Standard `StudentID` Eigenschaft zum Sortieren verwendet.</span><span class="sxs-lookup"><span data-stu-id="bc986-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="bc986-216">Im Artikel [Sortieren, Paging und Filtern von Daten](sorting-paging-and-filtering-data.md) ist der Benutzer in der Lage, eine Spalte für die Sortierung auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="bc986-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="bc986-217">Speichern Sie students.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="bc986-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="bc986-218">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="bc986-218">Run your application</span></span> 

<span data-ttu-id="bc986-219">Führen Sie Ihre Webanwendung (**F5**) aus, und navigieren Sie zur Seite " **Studenten** ", auf der Folgendes angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="bc986-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![Daten anzeigen](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="bc986-221">Automatische Generierung von Modell Bindungsmethoden</span><span class="sxs-lookup"><span data-stu-id="bc986-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="bc986-222">Wenn Sie diese tutorialreihe durcharbeiten, können Sie einfach den Code aus dem Tutorial in Ihr Projekt kopieren.</span><span class="sxs-lookup"><span data-stu-id="bc986-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="bc986-223">Ein Nachteil dieses Ansatzes ist jedoch, dass Sie die von Visual Studio bereitgestellte Funktion möglicherweise nicht kennen, um automatisch Code für Modell Bindungsmethoden zu generieren.</span><span class="sxs-lookup"><span data-stu-id="bc986-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="bc986-224">Wenn Sie an Ihren eigenen Projekten arbeiten, können Sie mithilfe der automatischen Codegenerierung Zeit sparen und einen Eindruck davon gewinnen, wie ein Vorgang implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="bc986-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="bc986-225">In diesem Abschnitt wird das Feature zur automatischen Codegenerierung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="bc986-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="bc986-226">Dieser Abschnitt dient nur zu Informationszwecken und enthält keinen Code, den Sie in Ihrem Projekt implementieren müssen.</span><span class="sxs-lookup"><span data-stu-id="bc986-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="bc986-227">Wenn Sie einen Wert für die `SelectMethod` `UpdateMethod` Eigenschaften,, `InsertMethod` oder `DeleteMethod` im Markup Code festlegen, können Sie die Option **neue Methode erstellen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="bc986-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![Erstellen einer Methode](retrieving-data/_static/image18.png)

<span data-ttu-id="bc986-229">Visual Studio erstellt nicht nur eine Methode im Code-Behind mit der richtigen Signatur, sondern generiert auch Implementierungs Code, um den Vorgang auszuführen.</span><span class="sxs-lookup"><span data-stu-id="bc986-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="bc986-230">Wenn Sie zuerst die- `ItemType` Eigenschaft festlegen, bevor Sie die Funktion zur automatischen Codegenerierung verwenden, verwendet der generierte Code diesen Typ für die Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="bc986-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="bc986-231">Wenn Sie z. b. die- `UpdateMethod` Eigenschaft festlegen, wird der folgende Code automatisch generiert:</span><span class="sxs-lookup"><span data-stu-id="bc986-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="bc986-232">Dieser Code muss dem Projekt nicht hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="bc986-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="bc986-233">Im nächsten Tutorial implementieren Sie Methoden zum Aktualisieren, löschen und Hinzufügen neuer Daten.</span><span class="sxs-lookup"><span data-stu-id="bc986-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="bc986-234">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="bc986-234">Summary</span></span>

<span data-ttu-id="bc986-235">In diesem Tutorial haben Sie Datenmodell Klassen erstellt und eine Datenbank aus diesen Klassen generiert.</span><span class="sxs-lookup"><span data-stu-id="bc986-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="bc986-236">Sie haben die Datenbanktabellen mit Testdaten ausgefüllt.</span><span class="sxs-lookup"><span data-stu-id="bc986-236">You filled the database tables with test data.</span></span> <span data-ttu-id="bc986-237">Sie haben die Modell Bindung verwendet, um Daten aus der Datenbank abzurufen, und dann die Daten in einer GridView angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bc986-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="bc986-238">Im nächsten [Tutorial](updating-deleting-and-creating-data.md) dieser Reihe aktivieren Sie das Aktualisieren, löschen und Erstellen von Daten.</span><span class="sxs-lookup"><span data-stu-id="bc986-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bc986-239">Nächste</span><span class="sxs-lookup"><span data-stu-id="bc986-239">Next</span></span>](updating-deleting-and-creating-data.md)
