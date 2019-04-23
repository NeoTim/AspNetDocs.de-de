---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 – Hilfsprogramme, Formulare und Überprüfung | Microsoft-Dokumentation
author: rick-anderson
description: In ASP.NET MVC 4-Modelle und Daten zugreifen, praktische Übungseinheit wurde beim Laden und Anzeigen von Daten aus der Datenbank. Fügen Sie in dieser praktischen Übungseinheit die...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 639a8e0e5fd9557221c95aee1bef0294df047ae8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59406313"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="c0f40-104">ASP.NET MVC 4 – Hilfsprogramme, Formulare und Überprüfung</span><span class="sxs-lookup"><span data-stu-id="c0f40-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="c0f40-105">durch [Web Camps Team](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c0f40-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="c0f40-106">Herunterladen Sie Web Camps Training Kit</span><span class="sxs-lookup"><span data-stu-id="c0f40-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="c0f40-107">In **ASP.NET MVC 4-Modelle und Datenzugriff** praktische Übungseinheit, Sie wurden laden und Anzeigen von Daten aus der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="c0f40-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="c0f40-108">Fügen Sie in dieser praktischen Übungseinheit die **Music Store** Anwendung die Möglichkeit, diese Daten zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="c0f40-109">Mit diesem Ziel vor Augen erstellen Sie zunächst den Controller, der die Aktionen erstellen, lesen, aktualisieren und löschen (CRUD) von Alben unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="c0f40-110">Generieren Sie eine Ansicht "Index"-Vorlage nutzen ASP.NETs gerüstfeature Alben Eigenschaften in einer HTML-Tabelle angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="c0f40-111">Um diese Ansicht zu verbessern, fügen Sie einer benutzerdefinierten HTML-Hilfsobjekt, der eine lange Beschreibung abgeschnitten wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="c0f40-112">Fügen Sie anschließend, dass das Bearbeiten und erstellen Sie Ansichten, mit denen Sie in der Datenbank mithilfe des Form-Elemente wie Dropdownlisten Alben ändern.</span><span class="sxs-lookup"><span data-stu-id="c0f40-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="c0f40-113">Schließlich können Sie Benutzer, die ein Album gelöscht, und auch Sie werden verhindert, dass sie falsche Daten eingeben, indem Sie ihre Eingabe zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="c0f40-114">Diese praktische Übungseinheit wird vorausgesetzt, dass grundlegende Kenntnisse der **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="c0f40-115">Wenn Sie nicht verwendet haben **ASP.NET MVC** vor, wir empfehlen Ihnen, sich mit Windows Live ID **Grundlagen von ASP.NET MVC** Hands-On Lab.</span><span class="sxs-lookup"><span data-stu-id="c0f40-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="c0f40-116">Dieses Lab führt Sie durch die Verbesserungen und neue Funktionen, die zuvor beschriebenen durch Anwenden von geringen Änderungen mit einer Beispiel-Webanwendung, die im Quellordner bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f40-117">Alle Beispielcode und Ausschnitte sind im Web Camps Training Kit unter enthalten [Versionen der Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="c0f40-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="c0f40-118">Das Projekt, das speziell für dieses Lab finden Sie unter [ASP.NET MVC 4-Hilfsprogramme, Formulare und Überprüfung](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span><span class="sxs-lookup"><span data-stu-id="c0f40-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c0f40-119">Ziele</span><span class="sxs-lookup"><span data-stu-id="c0f40-119">Objectives</span></span>

<span data-ttu-id="c0f40-120">In dieser praktischen Übungseinheit erfahren Sie, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="c0f40-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="c0f40-121">Erstellen Sie einen Controller zur Unterstützung von CRUD-Vorgänge</span><span class="sxs-lookup"><span data-stu-id="c0f40-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="c0f40-122">Generieren Sie eine Ansicht "Index" zum Anzeigen von Eigenschaften der Entität in eine HTML-Tabelle</span><span class="sxs-lookup"><span data-stu-id="c0f40-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="c0f40-123">Hinzufügen einer benutzerdefinierten HTML-Hilfsmethoden</span><span class="sxs-lookup"><span data-stu-id="c0f40-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="c0f40-124">Erstellen und Anpassen einer Ansicht bearbeiten</span><span class="sxs-lookup"><span data-stu-id="c0f40-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="c0f40-125">Unterscheiden Sie zwischen Aktionsmethoden, die auf HTTP-GET oder HTTP-POST-Aufrufe zu reagieren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="c0f40-126">Hinzufügen und Anpassen einer Ansicht erstellen</span><span class="sxs-lookup"><span data-stu-id="c0f40-126">Add and customize a Create View</span></span>
- <span data-ttu-id="c0f40-127">Behandelt das Löschen einer Entität</span><span class="sxs-lookup"><span data-stu-id="c0f40-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="c0f40-128">Validieren von Benutzereingaben</span><span class="sxs-lookup"><span data-stu-id="c0f40-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c0f40-129">Vorraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c0f40-129">Prerequisites</span></span>

<span data-ttu-id="c0f40-130">Sie benötigen Folgendes, um diese testumgebung abzuschließen:</span><span class="sxs-lookup"><span data-stu-id="c0f40-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c0f40-131">[Microsoft Visual Studio Express 2012 für Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) oder sogar eine höhere (Lesen [Anhang A](#AppendixA) Anleitungen zur Installation).</span><span class="sxs-lookup"><span data-stu-id="c0f40-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c0f40-132">Setup</span><span class="sxs-lookup"><span data-stu-id="c0f40-132">Setup</span></span>

<span data-ttu-id="c0f40-133">**Installieren von Codeausschnitten**</span><span class="sxs-lookup"><span data-stu-id="c0f40-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="c0f40-134">Der Einfachheit halber ist Großteil des Codes, die entlang dieser Übungseinheit verwaltet werden soll als Codeausschnitte für Visual Studio verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c0f40-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c0f40-135">So installieren Sie die Codeausschnitte ausführen **.\Source\Setup\CodeSnippets.vsi** Datei.</span><span class="sxs-lookup"><span data-stu-id="c0f40-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c0f40-136">Wenn Sie nicht mit dem Visual Studio Code Snippets und zu erfahren, wie Sie deren Verwendung vertraut sind, sehen Sie sich im Anhang in diesem Dokument &quot; [Anhang B: Verwenden von Codeausschnitten](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0f40-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c0f40-137">Übungen</span><span class="sxs-lookup"><span data-stu-id="c0f40-137">Exercises</span></span>

<span data-ttu-id="c0f40-138">Die folgenden Übungen besteht aus diesem Hands-On Lab:</span><span class="sxs-lookup"><span data-stu-id="c0f40-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="c0f40-139">Erstellen der Store Manager-Controller und die Ansicht "Index"</span><span class="sxs-lookup"><span data-stu-id="c0f40-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="c0f40-140">Ein HTML-Hilfsobjekt hinzufügen</span><span class="sxs-lookup"><span data-stu-id="c0f40-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="c0f40-141">Erstellen die Bearbeitungsansicht</span><span class="sxs-lookup"><span data-stu-id="c0f40-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="c0f40-142">Hinzufügen einer Ansicht erstellen</span><span class="sxs-lookup"><span data-stu-id="c0f40-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="c0f40-143">Löschung verarbeiten</span><span class="sxs-lookup"><span data-stu-id="c0f40-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="c0f40-144">Hinzufügen der Validierung</span><span class="sxs-lookup"><span data-stu-id="c0f40-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="c0f40-145">Unter Verwendung von unaufdringliche jQuery auf Clientseite</span><span class="sxs-lookup"><span data-stu-id="c0f40-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="c0f40-146">Jede Übung umfasst eine **End** Ordner mit der resultierenden Lösung, die Sie nach Abschluss der Übungen abrufen soll.</span><span class="sxs-lookup"><span data-stu-id="c0f40-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c0f40-147">Sie können diese Lösung als Leitfaden verwenden, bei Bedarf zusätzliche Hilfe bei der die Übungen durcharbeiten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="c0f40-148">Geschätzte Zeit für diese testumgebung abzuschließen: **60 Minuten**</span><span class="sxs-lookup"><span data-stu-id="c0f40-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="c0f40-149">Übung 1: Erstellen der Store Manager-Controller und die Ansicht "Index"</span><span class="sxs-lookup"><span data-stu-id="c0f40-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="c0f40-150">In dieser Übung erfahren Sie, wie zum Erstellen eines neuen Controllers CRUD-Vorgänge zu unterstützen, passen die Index-Aktionsmethode, um eine Liste der Alben aus der Datenbank und generiert schließlich eine Ansicht "Index"-Vorlage nutzen ASP.NETs Gerüstbau zurückzugeben die Funktion Alben Eigenschaften in einer HTML-Tabelle angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="c0f40-151">Aufgabe 1: Erstellen der StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="c0f40-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="c0f40-152">In dieser Aufgabe erstellen Sie einen neuen Controller namens **StoreManagerController** CRUD-Vorgänge zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="c0f40-153">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex1-CreatingTheStoreManagerController/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="c0f40-154">Sie müssen einige fehlende NuGet-Pakete herunterladen. bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-155">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-156">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-157">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-158">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-159">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-160">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-161">Fügen Sie einen neuen Controller hinzu.</span><span class="sxs-lookup"><span data-stu-id="c0f40-161">Add a new controller.</span></span> <span data-ttu-id="c0f40-162">Dazu, mit der Maustaste der **Controller** Ordner im Projektmappen-Explorer, wählen Sie **hinzufügen** und klicken Sie dann die **Controller** Befehl.</span><span class="sxs-lookup"><span data-stu-id="c0f40-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="c0f40-163">Ändern der **Controller** **Namen** zu **StoreManagerController** und stellen Sie sicher, dass die Option **MVC-Controller mit leeren Lese-/schreibaktionen**ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="c0f40-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="c0f40-164">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-164">Click **Add**.</span></span>

    <span data-ttu-id="c0f40-165">![Dialogfeld zum Hinzufügen Controller](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Controller-Dialogfeld \"hinzufügen\"")</span><span class="sxs-lookup"><span data-stu-id="c0f40-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="c0f40-166">*Controller-Dialogfeld "hinzufügen"*</span><span class="sxs-lookup"><span data-stu-id="c0f40-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="c0f40-167">Es wird eine neue Controllerklasse generiert.</span><span class="sxs-lookup"><span data-stu-id="c0f40-167">A new Controller class is generated.</span></span> <span data-ttu-id="c0f40-168">Da Sie zum Hinzufügen von Aktionen für Lese-/Schreibzugriff Stubmethoden, angegeben werden häufig verwendete CRUD-Aktionen mit TODO-Kommentare ausgefüllt, aufgefordert wird, sollen die anwendungsspezifische Logik erstellt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="c0f40-169">Aufgabe 2: Anpassen der StoreManager-Index</span><span class="sxs-lookup"><span data-stu-id="c0f40-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="c0f40-170">In dieser Aufgabe passen Sie die StoreManager Index-Aktionsmethode, um eine Ansicht mit der Liste der Alben aus der Datenbank zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="c0f40-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="c0f40-171">Fügen Sie Folgendes hinzu, in der Klasse StoreManagerController *mit* Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="c0f40-172">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Ex1 mit MvcMusicStore*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="c0f40-173">Hinzufügen eines Felds auf die **StoreManagerController** um eine Instanz von aufzunehmen **MusicStoreEntities.**</span><span class="sxs-lookup"><span data-stu-id="c0f40-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="c0f40-174">(Codeausschnitt - *ASP.NET MVC 4 – Hilfsprogramme und Formulare und Überprüfung - Ex1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="c0f40-175">Implementieren Sie die StoreManagerController Index-Aktion, um eine Ansicht mit der Liste der Alben zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="c0f40-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="c0f40-176">Die Logik des Controllers-Aktion werden ähnelt stark der StoreControllers Index-Aktion, die zuvor geschrieben.</span><span class="sxs-lookup"><span data-stu-id="c0f40-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="c0f40-177">Verwenden Sie LINQ, um alle Alben, einschließlich Informationen zu "Genre" und Interpreten für die Anzeige abzurufen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="c0f40-178">(Codeausschnitt - *ASP.NET MVC 4 – Hilfsprogramme und Formulare und Überprüfung - Ex1 StoreManagerController Index*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="c0f40-179">Aufgabe 3: Erstellen der Ansicht "Index"</span><span class="sxs-lookup"><span data-stu-id="c0f40-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="c0f40-180">In dieser Aufgabe erstellen Sie die Ansicht "Index"-Vorlage zum Anzeigen der Liste der Alben zurückgegebenes der **StoreManager** Controller.</span><span class="sxs-lookup"><span data-stu-id="c0f40-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="c0f40-181">Vor dem Erstellen der neuen Vorlage anzeigen, sollten Sie das Projekt erstellen, damit die **anzeigen-Dialogfeld hinzufügen** kennt die **Album** zu verwendende Klasse an.</span><span class="sxs-lookup"><span data-stu-id="c0f40-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="c0f40-182">Wählen Sie **erstellen | Erstellen von MvcMusicStore** zum Erstellen des Projekts.</span><span class="sxs-lookup"><span data-stu-id="c0f40-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="c0f40-183">Klicken Sie auf auf die **Index** Aktionsmethode, und wählen **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="c0f40-184">Hierdurch wird die **Ansicht hinzufügen** Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="c0f40-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="c0f40-185">![Ansicht hinzufügen](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Ansicht hinzufügen")</span><span class="sxs-lookup"><span data-stu-id="c0f40-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="c0f40-186">*Hinzufügen einer Ansicht aus, in der Index-Methode*</span><span class="sxs-lookup"><span data-stu-id="c0f40-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="c0f40-187">Stellen Sie sicher, dass der Ansichtsname ist, klicken Sie im Dialogfeld "Ansicht hinzufügen" **Index**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="c0f40-188">Wählen Sie die **eine stark typisierte Ansicht erstellen** aus, und wählen Sie **Album (MvcMusicStore.Models)** aus der **Modellklasse** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="c0f40-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="c0f40-189">Wählen Sie **Liste** aus der **Gerüst Vorlage** Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="c0f40-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="c0f40-190">Lassen Sie die **Ansichts-Engine** zu **Razor** und die anderen Felder mit ihren Standardwerten Wert, und klicken Sie dann auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="c0f40-191">![Hinzufügen einer Ansicht "Index"](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Hinzufügen einer Ansicht \"Index\"")</span><span class="sxs-lookup"><span data-stu-id="c0f40-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="c0f40-192">*Hinzufügen einer Ansicht "Index"*</span><span class="sxs-lookup"><span data-stu-id="c0f40-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="c0f40-193">Aufgabe 4: Anpassen das Gerüst der Ansicht "Index"</span><span class="sxs-lookup"><span data-stu-id="c0f40-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="c0f40-194">In dieser Aufgabe wird angepasst, die einfache ansichtsvorlage erstellt, die mit ASP.NET MVC-gerüstfeature so, dass sie die gewünschten Felder anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f40-195">Die **Gerüstbau** Unterstützung in ASP.NET MVC generiert eine einfache Vorlage Anzeigen der alle Felder im Modell Album aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="c0f40-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="c0f40-196">**Gerüstbau** bietet eine schnelle Möglichkeit zum Einstieg in eine stark typisierte Ansicht: anstatt die ansichtsvorlage manuell schreiben, schnell Gerüstbau eine Standardvorlage generiert und dann können Sie den generierten Code ändern.</span><span class="sxs-lookup"><span data-stu-id="c0f40-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>


1. <span data-ttu-id="c0f40-197">Überprüfen Sie den Code erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-197">Review the code created.</span></span> <span data-ttu-id="c0f40-198">Die generierte Liste der Felder werden Teil des folgenden HTML Tabelle, die **Gerüstbau** zum Anzeigen von Tabellendaten verwendet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="c0f40-199">Ersetzen Sie die **&lt;Tabelle&gt;** Code durch den folgenden Code zur Anzeige der **"Genre"**, **Interpreten**, **Albumtitel**, und **Preis** Felder.</span><span class="sxs-lookup"><span data-stu-id="c0f40-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="c0f40-200">Dies löscht die **AlbumId** und **Album Art URL** Spalten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="c0f40-201">Es ändert sich auch, GenreId und ArtistId Spalten zum Anzeigen ihrer Klasseneigenschaften verknüpfte **Artist.Name** und **Genre.Name**, und entfernt die **Details** Link.</span><span class="sxs-lookup"><span data-stu-id="c0f40-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="c0f40-202">Ändern Sie die folgenden Beschreibungen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c0f40-203">Aufgabe 5: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="c0f40-204">In dieser Aufgabe testen Sie, die die **StoreManager** **Index** ansichtsvorlage zeigt eine Liste der Alben der Entwurf der vorherigen Schritte entsprechend.</span><span class="sxs-lookup"><span data-stu-id="c0f40-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="c0f40-205">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-206">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-206">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-207">Ändern Sie die URL zum **/StoreManager** um sicherzustellen, dass eine Liste der Alben mit angezeigt wird, deren **Titel**, **Interpreten** und **"Genre"**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="c0f40-208">![Durchsuchen die Liste der Alben](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "durchsuchen die Liste der Alben")</span><span class="sxs-lookup"><span data-stu-id="c0f40-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="c0f40-209">*Durchsuchen die Liste der Alben*</span><span class="sxs-lookup"><span data-stu-id="c0f40-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="c0f40-210">Übung 2: Ein HTML-Hilfsobjekt hinzufügen</span><span class="sxs-lookup"><span data-stu-id="c0f40-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="c0f40-211">Die Indexseite mit StoreManager verfügt über ein potenzielles Problem: Titel und die Namen der Interpreten Eigenschaften können sowohl lang genug ist, deaktivieren Sie die Formatierung der Tabelle ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="c0f40-212">In dieser Übung lernen Sie, wie Sie eine benutzerdefinierte HTML-Hilfsfunktion, um das Abschneiden von Text hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="c0f40-213">In der folgenden Abbildung sehen Sie, wie das Format aufgrund der Länge des Texts geändert wird, wenn Sie eine kleines Browser-Größe verwenden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="c0f40-214">![Durchsuchen die Liste der Alben mit Text nicht abgeschnitten](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "durchsuchen die Liste der Alben mit Text nicht abgeschnitten")</span><span class="sxs-lookup"><span data-stu-id="c0f40-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="c0f40-215">*Durchsuchen die Liste der Alben mit nicht Text abgeschnitten*</span><span class="sxs-lookup"><span data-stu-id="c0f40-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="c0f40-216">Aufgabe 1: erweitern das HTML-Hilfsobjekt</span><span class="sxs-lookup"><span data-stu-id="c0f40-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="c0f40-217">In dieser Aufgabe fügen Sie eine neue Methode **Truncate** auf die **HTML** in ASP.NET MVC-Ansichten verfügbar gemachtes Objekt zu.</span><span class="sxs-lookup"><span data-stu-id="c0f40-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="c0f40-218">Implementieren Sie zu diesem Zweck eine **Erweiterungsmethode** für die integrierte **System.Web.Mvc.HtmlHelper** von ASP.NET MVC bereitgestellte Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f40-219">Weitere Informationen zu **Erweiterungsmethoden**, finden Sie unter diesem Msdn-Artikel.</span><span class="sxs-lookup"><span data-stu-id="c0f40-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="c0f40-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0f40-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>


1. <span data-ttu-id="c0f40-221">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex2-AddingAnHTMLHelper/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="c0f40-222">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-223">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-224">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-225">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-226">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-227">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-228">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-229">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-230">Öffnen Sie die StoreManager Ansicht "Index".</span><span class="sxs-lookup"><span data-stu-id="c0f40-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="c0f40-231">Zu diesem Zweck im Projektmappen-Explorer erweitern Sie die **Ansichten** Ordner, und klicken Sie dann die **StoreManager** , und öffnen Sie die **"Index.cshtml"** Datei.</span><span class="sxs-lookup"><span data-stu-id="c0f40-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="c0f40-232">Fügen Sie den folgenden Code unter der <strong>@model</strong> Richtlinie zum Definieren der <strong>Truncate</strong> Hilfsmethode.</span><span class="sxs-lookup"><span data-stu-id="c0f40-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="c0f40-233">Aufgabe 2 - Abschneiden von Text auf der Seite</span><span class="sxs-lookup"><span data-stu-id="c0f40-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="c0f40-234">In dieser Aufgabe verwenden Sie die **Truncate** Methode, um den Text in die ansichtsvorlage abgeschnitten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="c0f40-235">Öffnen Sie die StoreManager Ansicht "Index".</span><span class="sxs-lookup"><span data-stu-id="c0f40-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="c0f40-236">Zu diesem Zweck im Projektmappen-Explorer erweitern Sie die **Ansichten** Ordner, und klicken Sie dann die **StoreManager** , und öffnen Sie die **"Index.cshtml"** Datei.</span><span class="sxs-lookup"><span data-stu-id="c0f40-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="c0f40-237">Ersetzen Sie die Zeilen, die zeigen, die **Interpreten** und des "Album" **Titel**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="c0f40-238">Ersetzen Sie hierzu die folgenden Zeilen ein.</span><span class="sxs-lookup"><span data-stu-id="c0f40-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c0f40-239">Aufgabe 3: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="c0f40-240">In dieser Aufgabe testen Sie, die die **StoreManager** **Index** ansichtsvorlage schneidet, Titel und die Namen der Interpreten des Albums.</span><span class="sxs-lookup"><span data-stu-id="c0f40-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="c0f40-241">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-242">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-242">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-243">Ändern Sie die URL zu **/StoreManager** um zu überprüfen, ob lange Texte in der **Titel** und **Interpreten** Spalte werden abgeschnitten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="c0f40-244">![Titel und Interpreten Namen abgeschnitten](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "abgeschnitten, Titel und Interpreten Namen")</span><span class="sxs-lookup"><span data-stu-id="c0f40-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="c0f40-245">*Abgeschnittene Titel und die Namen der Künstler diese geändert hat*</span><span class="sxs-lookup"><span data-stu-id="c0f40-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="c0f40-246">Übung 3: Erstellen die Bearbeitungsansicht</span><span class="sxs-lookup"><span data-stu-id="c0f40-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="c0f40-247">In dieser Übung lernen Sie, wie erstellen Sie ein Formular zum Zulassen von Speicher-Manager, um ein Album zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="c0f40-248">Durchsuchen sie die **/StoreManager/Edit/id** URL (**Id** wird die eindeutige Id des Albums bearbeiten), wodurch eine HTTP-GET-Aufrufs an den Server.</span><span class="sxs-lookup"><span data-stu-id="c0f40-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="c0f40-249">Die Aktionsmethode Controller bearbeiten wird das entsprechende Album aus der Datenbank abrufen, erstellen eine **StoreManagerViewModel** Objekt, das (zusammen mit der eine Liste mit Interpreten und Genres) zu kapseln, und übergibt diese dann an eine ansichtsvorlage deaktivieren Rendern von HTML-Seite zurück an dem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="c0f40-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="c0f40-250">Diese Seite enthält eine **&lt;Formular&gt;** -Element mit Textfelder und Dropdownfelder zum Bearbeiten der Eigenschaften von Album.</span><span class="sxs-lookup"><span data-stu-id="c0f40-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="c0f40-251">Sobald der Benutzer klickt und die Formularwerte Album aktualisiert der **speichern** Schaltfläche, die Änderungen werden gesendet, über einen Rückruf aus eine HTTP-POST, **/StoreManager/Edit/id**. Obwohl die URL der gleiche wie in den letzten Aufruf verbleibt, ASP.NET MVC identifiziert, die dieses Mal, es ist ein HTTP-POST und aus diesem Grund führt eine andere Methode des bearbeiten-Aktion (eine ergänzt **[HttpPost]**).</span><span class="sxs-lookup"><span data-stu-id="c0f40-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="c0f40-252">Aufgabe 1: Implementieren von HTTP-GET-Edit-Aktion-Methode</span><span class="sxs-lookup"><span data-stu-id="c0f40-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="c0f40-253">In dieser Aufgabe implementieren Sie die HTTP-GET-Version, der die Aktionsmethode "Bearbeiten" zum Abrufen der entsprechenden Album aus der Datenbank sowie eine Liste aller Genres und Künstler.</span><span class="sxs-lookup"><span data-stu-id="c0f40-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="c0f40-254">Sie werden diese Daten Verpacken, in der **StoreManagerViewModel** Objekt definiert, die im letzten Schritt, die Sie dann auf eine ansichtsvorlage zum Rendern der Antwort mit übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="c0f40-255">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex3-CreatingTheEditView/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="c0f40-256">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-257">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-258">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-259">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-260">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-261">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-262">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-263">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-264">Öffnen der **StoreManagerController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="c0f40-265">Erweitern Sie dazu die **Controller** Ordner und doppelklicken Sie auf **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="c0f40-266">Ersetzen Sie die **HTTP-GET bearbeiten** Aktionsmethode mit den folgenden Code zum Abrufen von den entsprechenden **Album** als auch die **Genres** und **Künstler**aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="c0f40-267">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Aktion bearbeiten zu Ex3 StoreManagerController HTTP-GET*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-268">Verwenden Sie **System.Web.Mvc** **SelectList** Interpreten und Genres statt der **System.Collections.Generic** Liste.</span><span class="sxs-lookup"><span data-stu-id="c0f40-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="c0f40-269">**SelectList** ist eine sauberere Methode zum Auffüllen von HTML-Dropdownlisten und Dinge wie die aktuelle Auswahl zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="c0f40-270">Das Bearbeiten-Formular-Szenario werden lesbarer gestalten, instanziieren und diese ViewModel-Objekte in die Controlleraktion später einrichten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="c0f40-271">Aufgabe 2: Erstellen der Bearbeitungsansicht</span><span class="sxs-lookup"><span data-stu-id="c0f40-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="c0f40-272">In dieser Aufgabe erstellen Sie eine Vorlage bearbeiten anzeigen, die später die Album-Eigenschaften angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="c0f40-273">Erstellen Sie die Bearbeitungsansicht.</span><span class="sxs-lookup"><span data-stu-id="c0f40-273">Create the Edit View.</span></span> <span data-ttu-id="c0f40-274">Klicken Sie dazu auf, auf die **bearbeiten** Aktionsmethode, und wählen **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="c0f40-275">Stellen Sie sicher, dass der Ansichtsname ist, klicken Sie im Dialogfeld "Ansicht hinzufügen" **bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="c0f40-276">Überprüfen Sie die **eine stark typisierte Ansicht erstellen,** Kontrollkästchen, und wählen Sie **Album (MvcMusicStore.Models)** aus der **Datenklasse anzeigen** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="c0f40-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="c0f40-277">Wählen Sie **bearbeiten** aus der **Gerüst Vorlage** Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="c0f40-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="c0f40-278">Behalten Sie die anderen Felder auch die Standardwerte, und klicken Sie dann auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="c0f40-279">![Hinzufügen einer Bearbeitungsansicht](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "eine Bearbeitungsansicht hinzufügen")</span><span class="sxs-lookup"><span data-stu-id="c0f40-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="c0f40-280">*Hinzufügen einer Bearbeitungsansicht*</span><span class="sxs-lookup"><span data-stu-id="c0f40-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c0f40-281">Aufgabe 3: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="c0f40-282">In dieser Aufgabe testen Sie, die die **StoreManager** **bearbeiten** Ansichtsseite zeigt die Eigenschaften-Werte für das Album, die als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="c0f40-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="c0f40-283">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-284">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-284">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-285">Ändern Sie die URL zum **/StoreManager/Edit/1** um sicherzustellen, dass die Eigenschaften-Werte für das Album übergeben angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="c0f40-286">![Durchsuchen des Albums Bearbeitungsansicht](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Durchsuchen des Albums Bearbeitungsansicht")</span><span class="sxs-lookup"><span data-stu-id="c0f40-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="c0f40-287">*Durchsuchen des Albums Bearbeitungsansicht*</span><span class="sxs-lookup"><span data-stu-id="c0f40-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="c0f40-288">Aufgabe 4: Implementieren von Dropdown-Elemente in der Vorlage Album-Editor</span><span class="sxs-lookup"><span data-stu-id="c0f40-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="c0f40-289">In dieser Aufgabe fügen Sie Dropdownlisten die ansichtsvorlage erstellt, in der letzten Aufgabe hinzu, damit der Benutzer aus einer Liste von Künstlern und Genres auswählen kann.</span><span class="sxs-lookup"><span data-stu-id="c0f40-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="c0f40-290">Ersetzen Sie alle der **Album** Fieldset-Code durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0f40-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-291">Ein **Html.DropDownList** Hilfsprogramm zum Rendern von Dropdownlisten zum Auswählen von Künstlern und Genres hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="c0f40-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="c0f40-292">Die Parameter zu übergeben, um **Html.DropDownList** sind:</span><span class="sxs-lookup"><span data-stu-id="c0f40-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="c0f40-293">Der Name des Formularfelds (**&quot;ArtistId&quot;**).</span><span class="sxs-lookup"><span data-stu-id="c0f40-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="c0f40-294">Die **SelectList** der Werte für den Dropdown-Pfeil.</span><span class="sxs-lookup"><span data-stu-id="c0f40-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c0f40-295">Aufgabe 5: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="c0f40-296">In dieser Aufgabe testen Sie, die die **StoreManager** **bearbeiten** Ansichtsseite zeigt Dropdownlisten statt Interpreten und das Genre-ID-Text-Felder.</span><span class="sxs-lookup"><span data-stu-id="c0f40-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="c0f40-297">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-298">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-298">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-299">Ändern Sie die URL zum **/StoreManager/Edit/1** um sicherzustellen, dass der Dropdown-Elemente Interpreten und das Genre-ID-Text-Felder angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="c0f40-300">![Durchsuchen des Albums Bearbeiten-Ansicht mit Dropdownlisten](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "durchsuchen Album Bearbeiten-Ansicht mit Dropdownlisten")</span><span class="sxs-lookup"><span data-stu-id="c0f40-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="c0f40-301">*Durchsuchen des Albums-Edit-Ansicht mit Dropdownlisten*</span><span class="sxs-lookup"><span data-stu-id="c0f40-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="c0f40-302">Aufgabe 6: Implementieren der Bearbeiten Sie die HTTP-POST-Aktion-Methode</span><span class="sxs-lookup"><span data-stu-id="c0f40-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="c0f40-303">Nun, dass die Ansicht bearbeiten wie erwartet angezeigt wird, müssen Sie zur Implementierung der HTTP-POST-Aktion bearbeiten-Methode, um die Änderungen in das Album zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c0f40-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="c0f40-304">Schließen Sie den Browser, die ggf. zu Visual Studio-Fenster zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c0f40-305">Open **StoreManagerController** aus der **Controller** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="c0f40-306">Ersetzen Sie dies **HTTP-POST bearbeiten** Aktion-Methodencode durch Folgendes (Beachten Sie, dass die Methode, die ersetzt werden müssen überladene Version, die zwei Parameter empfängt):</span><span class="sxs-lookup"><span data-stu-id="c0f40-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="c0f40-307">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Aktion bearbeiten zu Ex3 StoreManagerController HTTP-POST*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-308">Diese Methode wird ausgeführt, wenn der Benutzer klickt auf die **speichern** Schaltfläche der Ansicht und führt einen HTTP-POST von die Formularwerte an den Server um dauerhaft in der Datenbank gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="c0f40-309">Das Decorator-Element **[HttpPost]** gibt an, dass die Methode für diese HTTP-POST-Szenarien verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="c0f40-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="c0f40-310">Die Methode akzeptiert eine **Album** Objekt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-310">The method takes an **Album** object.</span></span> <span data-ttu-id="c0f40-311">ASP.NET MVC erstellt automatisch das Album-Objekt aus der bereitgestellten &lt;Formular&gt; Werte.</span><span class="sxs-lookup"><span data-stu-id="c0f40-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="c0f40-312">Die Methode führt die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="c0f40-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="c0f40-313">Wenn das Modell gültig ist:</span><span class="sxs-lookup"><span data-stu-id="c0f40-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="c0f40-314">Aktualisieren Sie den Eintrag "Album" im Kontext als ein geändertes Objekt kennzeichnen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="c0f40-315">Speichern Sie die Änderungen, und leiten Sie zur Indexansicht.</span><span class="sxs-lookup"><span data-stu-id="c0f40-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="c0f40-316">Wenn das Modell nicht gültig ist, füllt es die ViewBag-Klasse mit dem **GenreId** und **ArtistId**, wird die Ansicht mit dem empfangenen Album-Objekt, damit der Benutzer kann zurückgegeben führen Sie ein Update erforderliches.</span><span class="sxs-lookup"><span data-stu-id="c0f40-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="c0f40-317">Aufgabe 7: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="c0f40-318">In dieser Aufgabe testen Sie, die die **StoreManager bearbeiten** Ansichtsseite speichert die aktualisierten Album Daten tatsächlich in der Datenbank.</span><span class="sxs-lookup"><span data-stu-id="c0f40-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="c0f40-319">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-320">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-320">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-321">Ändern Sie die URL zum **/StoreManager/Edit/1**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="c0f40-322">Ändern Sie den Titel Album zu **Load** und klicken Sie auf **speichern**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="c0f40-323">Stellen Sie sicher, dass die Albumtitel tatsächlich in der Liste der Alben geändert.</span><span class="sxs-lookup"><span data-stu-id="c0f40-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="c0f40-324">![Aktualisieren eines Albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "ein Album aktualisieren")</span><span class="sxs-lookup"><span data-stu-id="c0f40-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="c0f40-325">*Aktualisieren eines Albums*</span><span class="sxs-lookup"><span data-stu-id="c0f40-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="c0f40-326">Übung 4: Hinzufügen einer Ansicht erstellen</span><span class="sxs-lookup"><span data-stu-id="c0f40-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="c0f40-327">Nun, dass die **StoreManagerController** unterstützt die **bearbeiten** Möglichkeit, die in dieser Übung Sie erfahren, wie zum Hinzufügen einer Create View-Vorlage, damit Sie das Speichern von Manager neue Alben zur Anwendung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="c0f40-328">Wie Sie mit der Funktion bearbeiten, implementieren Sie die erstellen-Szenario mit zwei separate Methoden innerhalb der **StoreManagerController** Klasse:</span><span class="sxs-lookup"><span data-stu-id="c0f40-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="c0f40-329">Eine Aktionsmethode wird ein leeres Formular angezeigt, wenn Speicher-Manager zum ersten Mal besuchen der **/StoreManager/erstellen** URL.</span><span class="sxs-lookup"><span data-stu-id="c0f40-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="c0f40-330">Eine zweite Aktionsmethode behandelt das Szenario, in denen klickt auf der Store Manager die **speichern** Schaltfläche im Formular aus, und sendet die Werte zurück, an die **/StoreManager/erstellen** URL als eine HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="c0f40-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="c0f40-331">Aufgabe 1: Implementieren der Aktionsmethode erstellen HTTP-GET</span><span class="sxs-lookup"><span data-stu-id="c0f40-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="c0f40-332">In dieser Aufgabe implementieren Sie die HTTP-GET-Version, der die Create-Aktion-Methode zum Abrufen einer Liste mit allen Genres und Interpreten, Verpacken diese Daten in einem **StoreManagerViewModel** -Objekt, das dann an eine ansichtsvorlage übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="c0f40-333">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex4-AddingACreateView/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="c0f40-334">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-335">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-336">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-337">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-338">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-339">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-340">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-341">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-342">Open **StoreManagerController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="c0f40-343">Erweitern Sie dazu die **Controller** Ordner und doppelklicken Sie auf **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="c0f40-344">Ersetzen Sie die **erstellen** Aktion-Methodencode durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0f40-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="c0f40-345">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Aktion Ex4 StoreManagerController HTTP-GET-erstellen*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="c0f40-346">Aufgabe 2: Hinzufügen der Ansicht "erstellen"</span><span class="sxs-lookup"><span data-stu-id="c0f40-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="c0f40-347">In dieser Aufgabe fügen Sie die Create View-Vorlage, die ein neues-(leeres)-Albumformular angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="c0f40-348">Klicken Sie auf auf die **erstellen** Aktionsmethode, und wählen **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="c0f40-349">Hierdurch wird das Dialogfeld "Ansicht hinzufügen" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="c0f40-350">Stellen Sie sicher, dass der Ansichtsname ist, klicken Sie im Dialogfeld "Ansicht hinzufügen" **erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="c0f40-351">Wählen Sie die **eine stark typisierte Ansicht erstellen** aus, und wählen Sie **Album (MvcMusicStore.Models)** aus der **Modellklasse** Dropdown-Menü und **erstellen** aus der **Gerüst Vorlage** Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="c0f40-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="c0f40-352">Behalten Sie die anderen Felder auch die Standardwerte, und klicken Sie dann auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="c0f40-353">![Hinzufügen einer Erstellungsansicht](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "hinzufügen-a-erstellen-view.png")</span><span class="sxs-lookup"><span data-stu-id="c0f40-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="c0f40-354">*Hinzufügen der Ansicht "erstellen"*</span><span class="sxs-lookup"><span data-stu-id="c0f40-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="c0f40-355">Update der **GenreId** und **ArtistId** Felder, die eine Dropdown-Liste verwendet wird, wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="c0f40-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="c0f40-356">Aufgabe 3: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="c0f40-357">In dieser Aufgabe testen Sie, die die **StoreManager** **erstellen** Ansichtsseite wird ein leeres Albumformular ein angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="c0f40-358">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-359">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-359">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-360">Ändern Sie die URL zum **/StoreManager/erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="c0f40-361">Stellen Sie sicher, dass ein leeres Formular angezeigt wird, für das Auffüllen von Eigenschaften für die neuen Album.</span><span class="sxs-lookup"><span data-stu-id="c0f40-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="c0f40-362">![Erstellen Sie die Ansicht mit einem leeren Formular](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View mit einem leeren Formular")</span><span class="sxs-lookup"><span data-stu-id="c0f40-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="c0f40-363">*Ansicht mit einem leeren Formular erstellen*</span><span class="sxs-lookup"><span data-stu-id="c0f40-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="c0f40-364">Aufgabe 4: Implementierung der HTTP-POST erstellen Action-Methode</span><span class="sxs-lookup"><span data-stu-id="c0f40-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="c0f40-365">In dieser Aufgabe implementieren Sie die HTTP-POST-Version der erstellen-Aktionsmethode, die aufgerufen wird, wenn ein Benutzer klickt auf die **speichern** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c0f40-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="c0f40-366">Die Methode sollte das neue Album in der Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="c0f40-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="c0f40-367">Schließen Sie den Browser, die ggf. zu Visual Studio-Fenster zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c0f40-368">Open **StoreManagerController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="c0f40-369">Erweitern Sie dazu die **Controller** Ordner und doppelklicken Sie auf **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="c0f40-370">Ersetzen Sie dies **erstellen HTTP-POST** Aktion-Methodencode durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0f40-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="c0f40-371">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Ex4 StoreManagerController HTTP - POST Aktion erstellen*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-372">Die Create-Aktion ähnelt sehr der vorherigen Edit-Aktionsmethode, aber statt das Objekt als geändert, wird es in den Kontext hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c0f40-373">Aufgabe 5: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="c0f40-374">In dieser Aufgabe testen Sie, die die **StoreManager erstellen** Ansichtsseite können Sie ein neues Album zu erstellen, und klicken Sie dann zur Indexansicht StoreManager leitet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="c0f40-375">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-376">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-376">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-377">Ändern Sie die URL zum **/StoreManager/erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="c0f40-378">Füllen Sie alle Formularfelder mit Daten für ein neues Album, wie in der folgenden Abbildung:</span><span class="sxs-lookup"><span data-stu-id="c0f40-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="c0f40-379">![Erstellen eines Albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "ein Album erstellen")</span><span class="sxs-lookup"><span data-stu-id="c0f40-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="c0f40-380">*Erstellen eines Albums*</span><span class="sxs-lookup"><span data-stu-id="c0f40-380">*Creating an Album*</span></span>
3. <span data-ttu-id="c0f40-381">Stellen Sie sicher, dass Sie zur Indexansicht StoreManager umgeleitet, die den soeben erstellten neue Album enthält.</span><span class="sxs-lookup"><span data-stu-id="c0f40-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="c0f40-382">![Neues Album erstellt](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "neues Album erstellt")</span><span class="sxs-lookup"><span data-stu-id="c0f40-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="c0f40-383">*Neues Album erstellt*</span><span class="sxs-lookup"><span data-stu-id="c0f40-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="c0f40-384">Schritt 5: Löschung verarbeiten</span><span class="sxs-lookup"><span data-stu-id="c0f40-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="c0f40-385">Die Möglichkeit, Alben löschen wurde noch nicht implementiert.</span><span class="sxs-lookup"><span data-stu-id="c0f40-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="c0f40-386">Dies wird in dieser Übung zu.</span><span class="sxs-lookup"><span data-stu-id="c0f40-386">This is what this exercise will be about.</span></span> <span data-ttu-id="c0f40-387">Wie zuvor implementieren Sie die löschen-Szenario mit zwei separate Methoden innerhalb der **StoreManagerController** Klasse:</span><span class="sxs-lookup"><span data-stu-id="c0f40-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="c0f40-388">Eine Aktionsmethode wird eine Form der Bestätigung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="c0f40-389">Eine zweite Aktionsmethode übernimmt die Übermittlung des Formulars</span><span class="sxs-lookup"><span data-stu-id="c0f40-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="c0f40-390">Aufgabe 1: Implementieren der HTTP-GET-löschen-Aktion-Methode</span><span class="sxs-lookup"><span data-stu-id="c0f40-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="c0f40-391">Implementieren Sie die HTTP-GET-Version, der die Delete-Aktion-Methode zum Abrufen von Informationen für das Album des in dieser Aufgabe.</span><span class="sxs-lookup"><span data-stu-id="c0f40-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="c0f40-392">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex5-HandlingDeletion/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="c0f40-393">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-394">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-395">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-396">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-397">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-398">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-399">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-400">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-401">Open **StoreManagerController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="c0f40-402">Erweitern Sie dazu die **Controller** Ordner und doppelklicken Sie auf **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="c0f40-403">Die Löschaktion der Controller ist identisch mit der vorherigen Aktion des Store-Details-Controller: Abfragen der **Album** Objekt aus der Datenbank mithilfe der **Id** bereitgestellt, in der URL und gibt die entsprechende **Ansicht**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="c0f40-404">Ersetzen Sie dazu die HTTP-GET **löschen** Aktion-Methodencode durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0f40-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="c0f40-405">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Ex5 löschen verarbeiten HTTP-GET-löschen-Aktion*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="c0f40-406">Klicken Sie auf auf die **löschen** Aktionsmethode, und wählen **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="c0f40-407">Hierdurch wird das Dialogfeld "Ansicht hinzufügen" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="c0f40-408">Stellen Sie sicher, dass der Ansichtsname ist, klicken Sie im Dialogfeld "Ansicht hinzufügen" **löschen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="c0f40-409">Wählen Sie die **eine stark typisierte Ansicht erstellen** aus, und wählen Sie **Album (MvcMusicStore.Models)** aus der **Modellklasse** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="c0f40-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="c0f40-410">Wählen Sie **löschen** aus der **Gerüst Vorlage** Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="c0f40-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="c0f40-411">Behalten Sie die anderen Felder auch die Standardwerte, und klicken Sie dann auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="c0f40-412">![Hinzufügen einer Delete-Ansicht](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Hinzufügen einer Löschansicht")</span><span class="sxs-lookup"><span data-stu-id="c0f40-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="c0f40-413">*Hinzufügen einer Löschansicht*</span><span class="sxs-lookup"><span data-stu-id="c0f40-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="c0f40-414">Die Vorlage löschen, zeigt alle Felder aus dem Modell.</span><span class="sxs-lookup"><span data-stu-id="c0f40-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="c0f40-415">Sie werden nur das Album, den Titel angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-415">You will show only the album's title.</span></span> <span data-ttu-id="c0f40-416">Zu diesem Zweck ersetzen Sie den Inhalt der Ansicht durch den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="c0f40-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="c0f40-417">Aufgabe 2: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="c0f40-418">In dieser Aufgabe testen Sie, die die **StoreManager** **löschen** Ansichtsseite zeigt eine Form der Bestätigung löschen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="c0f40-419">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-420">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-420">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-421">Ändern Sie die URL zum **/StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="c0f40-422">Wählen Sie ein Album zu löschen, indem Sie auf **löschen** und stellen Sie sicher, dass die neue Ansicht hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="c0f40-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="c0f40-423">![Löschen eines Albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "ein Album gelöscht")</span><span class="sxs-lookup"><span data-stu-id="c0f40-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="c0f40-424">*Löschen eines Albums*</span><span class="sxs-lookup"><span data-stu-id="c0f40-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="c0f40-425">Aufgabe 3: Implementieren der HTTP-POST Delete-Aktion-Methode</span><span class="sxs-lookup"><span data-stu-id="c0f40-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="c0f40-426">In dieser Aufgabe implementieren Sie die HTTP-POST-Version der Delete-Aktionsmethode, die aufgerufen wird, wenn ein Benutzer klickt auf die **löschen** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c0f40-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="c0f40-427">Die Methode sollte das Album in der Datenbank löschen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="c0f40-428">Schließen Sie den Browser, die ggf. zu Visual Studio-Fenster zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="c0f40-429">Open **StoreManagerController** Klasse.</span><span class="sxs-lookup"><span data-stu-id="c0f40-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="c0f40-430">Erweitern Sie dazu die **Controller** Ordner und doppelklicken Sie auf **StoreManagerController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="c0f40-431">Ersetzen Sie dies **HTTP-POST löschen** Aktion-Methodencode durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0f40-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="c0f40-432">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung - Ex5 löschen verarbeiten HTTP-POST-löschen-Aktion*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c0f40-433">Aufgabe 4: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="c0f40-434">In dieser Aufgabe testen Sie, die die **StoreManager löschen** Ansichtsseite ermöglicht das Löschen eines Albums und leitet dann an die Indexansicht StoreManager weiter.</span><span class="sxs-lookup"><span data-stu-id="c0f40-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="c0f40-435">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-436">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-436">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-437">Ändern Sie die URL zum **/StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="c0f40-438">Wählen Sie ein Album zu löschen, indem Sie auf **löschen.**</span><span class="sxs-lookup"><span data-stu-id="c0f40-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="c0f40-439">Bestätigen Sie den Löschvorgang, indem Sie auf **löschen** Schaltfläche:</span><span class="sxs-lookup"><span data-stu-id="c0f40-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="c0f40-440">![Löschen eines Albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "ein Album gelöscht")</span><span class="sxs-lookup"><span data-stu-id="c0f40-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="c0f40-441">*Löschen eines Albums*</span><span class="sxs-lookup"><span data-stu-id="c0f40-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="c0f40-442">Stellen Sie sicher, dass das Album gelöscht wurde, da es sich nicht in erscheint die **Index** Seite.</span><span class="sxs-lookup"><span data-stu-id="c0f40-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="c0f40-443">Übung 6: Hinzufügen der Validierung</span><span class="sxs-lookup"><span data-stu-id="c0f40-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="c0f40-444">Derzeit führen die erstellen und Bearbeiten von Formen, die Sie verfügen keine Art von Validierung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="c0f40-445">Wenn der Benutzer ein erforderliches Feld ist leer oder Typ Buchstaben in das Preisfeld verlässt, wird der erste Fehler erhalten Sie aus der Datenbank sein.</span><span class="sxs-lookup"><span data-stu-id="c0f40-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="c0f40-446">Sie können die Anwendung durch Hinzufügen von Datenanmerkungen zu Ihrer Modellklasse Validierung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="c0f40-447">Datenanmerkungen ermöglichen, beschreiben die gewünschten Regeln angewendet werden, um Ihre Eigenschaften des Modells und ASP.NET MVC übernimmt erzwingen und die entsprechende Meldung für Benutzer anzeigen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="c0f40-448">Aufgabe 1: Hinzufügen von Datenanmerkungen</span><span class="sxs-lookup"><span data-stu-id="c0f40-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="c0f40-449">In dieser Aufgabe fügen Sie, dass von Datenanmerkungen auf dem Album-Modell, das der Seite "erstellen" und "Bearbeiten" zu machen, werden validierungsmeldungen bei Bedarf anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="c0f40-450">Für eine einfache Modellklasse, Hinzufügen einer Anmerkung Daten nur erfolgt durch Hinzufügen einer **mit** -Anweisung für **System.ComponentModel.DataAnnotation**, platzieren Sie dann eine **[erforderlich]** Attribut für die entsprechenden Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="c0f40-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="c0f40-451">Im folgende Beispiel würde machen die **Namen** -Eigenschaft ein Pflichtfeld in der Ansicht.</span><span class="sxs-lookup"><span data-stu-id="c0f40-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="c0f40-452">Dies ist in Fällen, wie diese Anwendung ein wenig komplexer, an dem das Entity Data Model generiert wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="c0f40-453">Wenn Sie direkt an die Modellklassen Datenanmerkungen hinzugefügt haben, würden sie überschrieben werden, wenn Sie das Modell aus der Datenbank aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="c0f40-454">Sie können stattdessen machen Metadaten partiellen Klassen, die zum Speichern von Anmerkungen vorhanden ist und mit dem Modell zugeordnet sind Klassen, mit der **["metadatatype"]** Attribut.</span><span class="sxs-lookup"><span data-stu-id="c0f40-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="c0f40-455">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex6-AddingValidation/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="c0f40-456">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-457">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-458">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-459">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-460">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-461">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-462">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-463">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-464">Öffnen der **Album.cs** aus der **Modelle** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="c0f40-465">Ersetzen Sie dies **Album.cs** Inhalt mit den hervorgehobenen Code, damit sie wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="c0f40-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0f40-466">Die Zeile **[DisplayFormat(ConvertEmptyStringToNull=false)]** gibt an, dass leere Zeichenfolgen aus dem Modell nicht auf null konvertiert werden, wenn das Datenfeld in der Datenquelle aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="c0f40-467">Diese Einstellung wird eine Ausnahme vermeiden, wenn Entity Framework null-Werte für das Modell zugewiesen werden, bevor Datenanmerkung Felder überprüft.</span><span class="sxs-lookup"><span data-stu-id="c0f40-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="c0f40-468">(Codeausschnitt - *ASP.NET MVC 4-Hilfsprogrammen und Formulare und Überprüfung: partielle Ex6 Album Metadatenklasse*)</span><span class="sxs-lookup"><span data-stu-id="c0f40-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-469">Dies **Album** partielle Klasse verfügt über eine **"metadatatype"** Attribut verweist auf die **AlbumMetaData** -Klasse für die Datenanmerkungen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="c0f40-470">Dies sind einige der Datenanmerkung Attribute, die Sie verwenden, um das Modell Album mit Anmerkungen versehen:</span><span class="sxs-lookup"><span data-stu-id="c0f40-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="c0f40-471">Erforderlich – gibt an, dass die Eigenschaft ein erforderliches Feld.</span><span class="sxs-lookup"><span data-stu-id="c0f40-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="c0f40-472">DisplayName - definiert den Text auf Formularfelder und von überprüfungsnachrichten verwendet werden</span><span class="sxs-lookup"><span data-stu-id="c0f40-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="c0f40-473">DisplayFormat – gibt an, wie Datenfelder angezeigt und formatiert sind.</span><span class="sxs-lookup"><span data-stu-id="c0f40-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="c0f40-474">StringLength - definiert die maximale Länge für ein Zeichenfolgenfeld eingegeben</span><span class="sxs-lookup"><span data-stu-id="c0f40-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="c0f40-475">Bereich – weist den maximalen und minimalen Wert für ein numerisches Feld</span><span class="sxs-lookup"><span data-stu-id="c0f40-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="c0f40-476">ScaffoldColumn – ermöglicht das Ausblenden von Feldern von Editor-Formularen</span><span class="sxs-lookup"><span data-stu-id="c0f40-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="c0f40-477">Aufgabe 2: Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c0f40-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="c0f40-478">In dieser Aufgabe testen Sie, dass die Seiten erstellen und Bearbeiten von Feldern, überprüft unter Verwendung der Anzeige in der vorhergehenden Aufgabe ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="c0f40-479">Drücken Sie **F5** zum Ausführen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c0f40-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0f40-480">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-480">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-481">Ändern Sie die URL zum **/StoreManager/erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="c0f40-482">Stellen Sie sicher, dass die Anzeigenamen in der partiellen Klasse übereinstimmen (z. B. **Album Art URL** anstelle von **AlbumArtUrl**)</span><span class="sxs-lookup"><span data-stu-id="c0f40-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="c0f40-483">Klicken Sie auf **erstellen**, ohne das Formular ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="c0f40-484">Stellen Sie sicher, dass Sie die entsprechende Überprüfung Nachrichten erhalten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="c0f40-485">![Überprüft die Felder in der Seite "erstellen"](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "überprüft die Felder in der Seite \"erstellen\"")</span><span class="sxs-lookup"><span data-stu-id="c0f40-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="c0f40-486">*Überprüfte Felder in der Seite "erstellen"*</span><span class="sxs-lookup"><span data-stu-id="c0f40-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="c0f40-487">Überprüfen, ob Sie dasselbe gilt, mit der **bearbeiten** Seite.</span><span class="sxs-lookup"><span data-stu-id="c0f40-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="c0f40-488">Ändern Sie die URL zum **/StoreManager/Edit/1** und stellen Sie sicher, dass die Anzeigenamen in der partiellen Klasse übereinstimmen (z. B. **Album Art URL** anstelle von **AlbumArtUrl**).</span><span class="sxs-lookup"><span data-stu-id="c0f40-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="c0f40-489">Leere der **Titel** und **Preis** Felder, und klicken Sie auf **speichern**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="c0f40-490">Stellen Sie sicher, dass Sie die entsprechende Überprüfung Nachrichten erhalten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-490">Verify that you get the corresponding validation messages.</span></span>

    ![Überprüfte Felder in der Seite "Bearbeiten"](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="c0f40-492">*Überprüfte Felder in der Seite "Bearbeiten"*</span><span class="sxs-lookup"><span data-stu-id="c0f40-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="c0f40-493">Übung 7: Unter Verwendung von unaufdringliche jQuery auf Clientseite</span><span class="sxs-lookup"><span data-stu-id="c0f40-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="c0f40-494">In dieser Übung lernen Sie, wie Sie MVC 4 unaufdringliche jQuery-Validierung auf Clientseite zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f40-495">Die unaufdringliche jQuery verwendet Data-Ajax-Präfix JavaScript zum Aufrufen der Aktionsmethoden, auf dem Server statt auf intrusively Ausgeben von Inline-Clientskripts.</span><span class="sxs-lookup"><span data-stu-id="c0f40-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="c0f40-496">Aufgabe 1: Ausführen der Anwendung vor dem Aktivieren unaufdringliche jQuery</span><span class="sxs-lookup"><span data-stu-id="c0f40-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="c0f40-497">In dieser Aufgabe führen Sie die Anwendung vor, einschließlich jQuery, um den beide Überprüfung Modelle verglichen werden soll.</span><span class="sxs-lookup"><span data-stu-id="c0f40-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="c0f40-498">Öffnen der **beginnen** Lösung controllerarbeitsverzeichnis **Quelle/Ex7-UnobtrusivejQueryValidation/Anfang/** Ordner.</span><span class="sxs-lookup"><span data-stu-id="c0f40-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="c0f40-499">Andernfalls können Sie weiterhin, verwenden die **End** Lösung abgerufen wird, indem Sie der vorherige Übung abschließen können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="c0f40-500">Wenn Sie die bereitgestellten geöffnet **beginnen** Lösung, Sie müssen einige fehlende NuGet-Pakete herunterladen bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0f40-501">Zu diesem Zweck klicken Sie auf die **Projekt** Menü **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0f40-502">In der **NuGet-Pakete verwalten** Dialogfeld klicken Sie auf **wiederherstellen** um das Herunterladen fehlender Pakete.</span><span class="sxs-lookup"><span data-stu-id="c0f40-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0f40-503">Abschließend erstellen Sie die Projektmappe, indem Sie auf **erstellen** | **Projektmappe**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0f40-504">Einer der Vorteile der Verwendung von NuGet ist, dass Sie nicht alle Bibliotheken in Ihrem Projekt, Versand Verringern der Projektgröße.</span><span class="sxs-lookup"><span data-stu-id="c0f40-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0f40-505">Mit NuGet Power Tools können werden durch Angabe von Versionen des Pakets in der Datei "Packages.config" Sie alle erforderlichen Bibliotheken das erstmalige herunterladen, die, das Sie das Projekt ausführen, können.</span><span class="sxs-lookup"><span data-stu-id="c0f40-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0f40-506">Deshalb müssen Sie diese Schritte ausgeführt werden, nach dem Öffnen einer vorhandenen Lösung aus dieser Übungseinheit wird.</span><span class="sxs-lookup"><span data-stu-id="c0f40-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0f40-507">Drücken Sie **F5**, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="c0f40-508">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-508">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-509">Navigieren Sie **/StoreManager/erstellen** , und klicken Sie auf **erstellen** ohne Ausfüllen des Formulars, sodass stellen Sie sicher, dass Sie validierungsmeldungen erhalten:</span><span class="sxs-lookup"><span data-stu-id="c0f40-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="c0f40-510">![Die Clientvalidierung deaktiviert](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "die Clientvalidierung deaktiviert")</span><span class="sxs-lookup"><span data-stu-id="c0f40-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="c0f40-511">*Die Clientvalidierung deaktiviert*</span><span class="sxs-lookup"><span data-stu-id="c0f40-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="c0f40-512">Öffnen Sie im Browser den HTML-Quellcode aus:</span><span class="sxs-lookup"><span data-stu-id="c0f40-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="c0f40-513">Aufgabe 2: Aktivieren der unaufdringlichen Clientvalidierung</span><span class="sxs-lookup"><span data-stu-id="c0f40-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="c0f40-514">In dieser Aufgabe aktivieren Sie jQuery **unaufdringliche Clientvalidierung** aus **"Web.config"** -Datei, die standardmäßig auf "false" in allen neuen ASP.NET MVC 4-Projekten festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="c0f40-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="c0f40-515">Fügen Sie außerdem, dass die erforderlichen Verweise auf jQuery Unobtrusive Client Validation Arbeit stellen Skripts.</span><span class="sxs-lookup"><span data-stu-id="c0f40-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="c0f40-516">Öffnen **"Web.config"** Datei am Stammverzeichnis des Projekts, und stellen Sie sicher, dass die **ClientValidationEnabled** und **UnobtrusiveJavaScriptEnabled** Schlüssel-Werte werden festgelegt, um **"true"**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-517">Sie können auch die Clientvalidierung durch Code in "Global.asax.cs" für die gleichen Ergebnisse erhalten aktivieren:</span><span class="sxs-lookup"><span data-stu-id="c0f40-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="c0f40-518">**HtmlHelper.ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="c0f40-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="c0f40-519">Darüber hinaus können Sie ClientValidationEnabled-Attributs in jedem Controller haben Sie ein benutzerdefiniertes Verhalten zuweisen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="c0f40-520">Open **Create.cshtml** am **Views\StoreManager**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="c0f40-521">Stellen Sie sicher, dass die folgenden Skriptdateien **jquery.validate** und **jquery.validate.unobtrusive**, auf die in der Ansicht über die &quot; **~/bundles/jqueryval** &quot; Paket.</span><span class="sxs-lookup"><span data-stu-id="c0f40-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="c0f40-522">Alle diese jQuery-Bibliotheken sind in neuen MVC 4-Projekte enthalten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="c0f40-523">Finden Sie weitere Bibliotheken in der **/Skripts** Ordner von Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="c0f40-524">Bibliotheken funktionieren, müssen Sie einen Verweis auf die jQuery-Framework-Bibliothek hinzufügen, um diese Validierung zu machen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="c0f40-525">Da dieser Verweis bereits, in hinzugefügt wurde der  **\_Layout.cshtml** -Datei, Sie müssen nicht in dieser Ansicht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="c0f40-526">Aufgabe 3: Ausführen der Anwendung mithilfe von unaufdringliche jQuery-Validierung</span><span class="sxs-lookup"><span data-stu-id="c0f40-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="c0f40-527">In dieser Aufgabe testen Sie, die die **StoreManager** Vorlage führt die Validierung auf Clientseite jQuery-Bibliotheken verwenden, wenn der Benutzer ein neues Album erstellt Ansicht erstellen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="c0f40-528">Drücken Sie **F5**, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="c0f40-529">Das Projekt, die auf der Startseite wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0f40-529">The project starts in the Home page.</span></span> <span data-ttu-id="c0f40-530">Navigieren Sie **/StoreManager/erstellen** , und klicken Sie auf **erstellen** ohne Ausfüllen des Formulars, sodass stellen Sie sicher, dass Sie validierungsmeldungen erhalten:</span><span class="sxs-lookup"><span data-stu-id="c0f40-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="c0f40-531">![Validierung mit jQuery aktiviert](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Validierung mit jQuery aktiviert")</span><span class="sxs-lookup"><span data-stu-id="c0f40-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="c0f40-532">*Validierung mit jQuery aktiviert*</span><span class="sxs-lookup"><span data-stu-id="c0f40-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="c0f40-533">Öffnen Sie im Browser den Quellcode für die Ansicht erstellen:</span><span class="sxs-lookup"><span data-stu-id="c0f40-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="c0f40-534">Für jede Clientvalidierungsregel, fügt die unaufdringliche jQuery ein Attribut mit Daten: Val -*Rulename*=&quot;*Nachricht*&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0f40-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="c0f40-535">Im folgenden finden Sie eine Liste von Tags, unauffälliger jQuery Fügt HTML-Feld für die Validierung ausführen:</span><span class="sxs-lookup"><span data-stu-id="c0f40-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="c0f40-536">Val-Daten</span><span class="sxs-lookup"><span data-stu-id="c0f40-536">Data-val</span></span>
   > - <span data-ttu-id="c0f40-537">Daten-Val-Anzahl</span><span class="sxs-lookup"><span data-stu-id="c0f40-537">Data-val-number</span></span>
   > - <span data-ttu-id="c0f40-538">Val-Datenbereich</span><span class="sxs-lookup"><span data-stu-id="c0f40-538">Data-val-range</span></span>
   > - <span data-ttu-id="c0f40-539">Daten-Val-Bereich: min / Daten-Val-Range-max '</span><span class="sxs-lookup"><span data-stu-id="c0f40-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="c0f40-540">Val erforderlichen Daten</span><span class="sxs-lookup"><span data-stu-id="c0f40-540">Data-val-required</span></span>
   > - <span data-ttu-id="c0f40-541">Val-Datenlänge</span><span class="sxs-lookup"><span data-stu-id="c0f40-541">Data-val-length</span></span>
   > - <span data-ttu-id="c0f40-542">Daten-Val-Länge-max ' / Daten-Val-Länge-min</span><span class="sxs-lookup"><span data-stu-id="c0f40-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="c0f40-543">Alle Datenwerte werden mit Modell gefüllt **Datenanmerkung**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="c0f40-544">Anschließend kann die gesamte Logik, die auf Serverseite funktioniert auf Clientseite ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="c0f40-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="c0f40-545">Price-Attribut hat beispielsweise die folgende datenanmerkung im Modell:</span><span class="sxs-lookup"><span data-stu-id="c0f40-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="c0f40-546">Ist nach der Verwendung von unaufdringliche jQuery, der generierte Code ein:</span><span class="sxs-lookup"><span data-stu-id="c0f40-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c0f40-547">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c0f40-547">Summary</span></span>

<span data-ttu-id="c0f40-548">Von dieser praktischen Übungseinheit haben Sie gelernt, Benutzern so ändern Sie die in der Datenbank mit der Verwendung der folgenden gespeicherten Daten ermöglichen:</span><span class="sxs-lookup"><span data-stu-id="c0f40-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="c0f40-549">Controlleraktionen wie z. B. Index erstellen, bearbeiten, löschen</span><span class="sxs-lookup"><span data-stu-id="c0f40-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="c0f40-550">ASP.NETs gerüstfeature zum Anzeigen von Eigenschaften in einer HTML-Tabelle</span><span class="sxs-lookup"><span data-stu-id="c0f40-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="c0f40-551">Auftreten von benutzerdefinierten HTML-Hilfsprogramme, um Benutzer zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="c0f40-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="c0f40-552">Aktionsmethoden, die auf HTTP-GET oder HTTP-POST-Aufrufe zu reagieren.</span><span class="sxs-lookup"><span data-stu-id="c0f40-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="c0f40-553">Eine freigegebene Editor-Vorlage für ähnliche Ansichtsvorlagen erstellen und bearbeiten</span><span class="sxs-lookup"><span data-stu-id="c0f40-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="c0f40-554">Form-Elemente wie Dropdownlisten</span><span class="sxs-lookup"><span data-stu-id="c0f40-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="c0f40-555">Datenanmerkungen bei der modellüberprüfung</span><span class="sxs-lookup"><span data-stu-id="c0f40-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="c0f40-556">Clientseitige Validierung mit unaufdringliche jQuery-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="c0f40-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c0f40-557">Anhang A: Installieren von Visual Studio Express 2012 für Web</span><span class="sxs-lookup"><span data-stu-id="c0f40-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c0f40-558">Sie installieren können **Microsoft Visual Studio Express 2012 für Web** oder einem anderen &quot;Express&quot; Version verwenden, die **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c0f40-559">Die folgenden Anweisungen führen Sie über die erforderlichen Schritte zum Installieren *Visual Studio Express 2012 für Web* mit *Microsoft Web Platform Installer*.</span><span class="sxs-lookup"><span data-stu-id="c0f40-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c0f40-560">Wechseln Sie zu [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="c0f40-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c0f40-561">Auch wenn Sie bereits Webplattform-Installer installiert haben, können Sie öffnen ihn, und suchen Sie nach dem Produkt &quot; <em>Visual Studio Express 2012 für das Web mit Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0f40-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="c0f40-562">Klicken Sie auf **jetzt installieren**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-562">Click on **Install Now**.</span></span> <span data-ttu-id="c0f40-563">Wenn Sie keine **Webplattform-Installer** gelangen Sie zum Herunterladen und installieren Sie diese zuerst.</span><span class="sxs-lookup"><span data-stu-id="c0f40-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c0f40-564">Einmal **Webplattform-Installer** geöffnet ist, klicken Sie auf **installieren** um das Setup zu starten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c0f40-565">![Installieren von Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Installieren von Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="c0f40-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c0f40-566">*Installieren von Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="c0f40-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c0f40-567">Lesen Sie die Produkte Lizenzen und Begriffe, und klicken Sie auf **akzeptieren** um den Vorgang fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Akzeptieren der Lizenzbedingungen](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="c0f40-569">*Akzeptieren der Lizenzbedingungen*</span><span class="sxs-lookup"><span data-stu-id="c0f40-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c0f40-570">Warten Sie, bis der Prozess zum Herunterladen und die Installation abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="c0f40-570">Wait until the downloading and installation process completes.</span></span>

    ![Installationsstatus](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="c0f40-572">*Installationsstatus*</span><span class="sxs-lookup"><span data-stu-id="c0f40-572">*Installation progress*</span></span>
6. <span data-ttu-id="c0f40-573">Wenn die Installation abgeschlossen ist, klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-573">When the installation completes, click **Finish**.</span></span>

    ![Die Installation wurde abgeschlossen](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="c0f40-575">*Die Installation wurde abgeschlossen*</span><span class="sxs-lookup"><span data-stu-id="c0f40-575">*Installation completed*</span></span>
7. <span data-ttu-id="c0f40-576">Klicken Sie auf **beenden** Webplattform-Installer zu schließen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c0f40-577">Um Visual Studio Express für Web zu öffnen, wechseln Sie zu der **starten** schreiben zu starten und Bildschirm &quot; **VS Express**&quot;, klicken Sie dann auf die **Visual Studio Express für Web** die Kachel.</span><span class="sxs-lookup"><span data-stu-id="c0f40-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Visual Studio Express für Web-Kachel](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="c0f40-579">*Visual Studio Express für Web-Kachel*</span><span class="sxs-lookup"><span data-stu-id="c0f40-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="c0f40-580">Anhang B: Verwenden von Codeausschnitten</span><span class="sxs-lookup"><span data-stu-id="c0f40-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="c0f40-581">Mit Codeausschnitten müssen Sie den Code zur Hand benötigten.</span><span class="sxs-lookup"><span data-stu-id="c0f40-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c0f40-582">Das Lab-Dokument informiert Sie genau wann sie verwendet werden kann wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c0f40-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c0f40-583">![Verwenden von Visual Studio-Codeausschnitten zum Einfügen von Code in Ihrem Projekt](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "mithilfe von Visual Studio-Codeausschnitten, die Code in das Projekt einfügen.")</span><span class="sxs-lookup"><span data-stu-id="c0f40-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c0f40-584">*Verwenden von Visual Studio-Codeausschnitten zum Einfügen von Code in Ihrem Projekt*</span><span class="sxs-lookup"><span data-stu-id="c0f40-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c0f40-585">***Hinzufügen ein Codeausschnitts, die über die Tastatur (nur c#)***</span><span class="sxs-lookup"><span data-stu-id="c0f40-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c0f40-586">Platzieren Sie den Cursor, wo Sie möchten den Code einfügen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c0f40-587">Starten Sie den codeausschnittsnamen (ohne Leerzeichen oder Bindestriche) eingeben.</span><span class="sxs-lookup"><span data-stu-id="c0f40-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c0f40-588">Beobachten Sie, wie IntelliSense zeigt übereinstimmende Codeausschnitte Namen.</span><span class="sxs-lookup"><span data-stu-id="c0f40-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c0f40-589">Wählen Sie den richtigen Codeausschnitt (oder halten Sie eingeben, bis die gesamte codeausschnittsnamen ausgewählt ist).</span><span class="sxs-lookup"><span data-stu-id="c0f40-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c0f40-590">Drücken Sie die Tab-Taste zweimal auf Einfügen des Codeausschnitts an der Cursorposition ein.</span><span class="sxs-lookup"><span data-stu-id="c0f40-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c0f40-591">![Geben Sie den Namen des Ausschnitts](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Geben Sie den Namen des Ausschnitts")</span><span class="sxs-lookup"><span data-stu-id="c0f40-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c0f40-592">*Geben Sie den Namen des Ausschnitts*</span><span class="sxs-lookup"><span data-stu-id="c0f40-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="c0f40-593">![Tabstopp drücken, um den hervorgehobenen Codeausschnitt auswählen](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab drücken, um den hervorgehobenen Codeausschnitt auswählen")</span><span class="sxs-lookup"><span data-stu-id="c0f40-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c0f40-594">*Drücken Sie Tabstopp, um den hervorgehobenen Codeausschnitt auswählen*</span><span class="sxs-lookup"><span data-stu-id="c0f40-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c0f40-595">![Drücken Sie die Tabulatortaste erneut, und der Ausschnitt erweitert](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "drücken Sie die Tabulatortaste erneut, und der Ausschnitt werden erweitert.")</span><span class="sxs-lookup"><span data-stu-id="c0f40-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c0f40-596">*Drücken Sie die Tabulatortaste erneut, und der Ausschnitt werden erweitert.*</span><span class="sxs-lookup"><span data-stu-id="c0f40-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c0f40-597">***Hinzufügen ein Codeausschnitts, die mit der Maus (c#, Visual Basic und XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="c0f40-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c0f40-598">Mit der rechten Maustaste, in dem den Codeausschnitt eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="c0f40-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c0f40-599">Wählen Sie **Ausschnitt einfügen** gefolgt von **Meine Codeausschnitte**.</span><span class="sxs-lookup"><span data-stu-id="c0f40-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c0f40-600">Wählen Sie die relevante Codeausschnitte in der Liste, indem Sie darauf klicken.</span><span class="sxs-lookup"><span data-stu-id="c0f40-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c0f40-601">![Mit der rechten Maustaste, in dem Sie den Codeausschnitt einfügen, und wählen Ausschnitt einfügen möchten](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "mit der rechten Maustaste, in dem Sie den Codeausschnitt einfügen, und wählen Ausschnitt einfügen möchten,")</span><span class="sxs-lookup"><span data-stu-id="c0f40-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c0f40-602">*Mit der rechten Maustaste, in dem Sie den Codeausschnitt einfügen, und wählen Ausschnitt einfügen möchten*</span><span class="sxs-lookup"><span data-stu-id="c0f40-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c0f40-603">![Wählen Sie die relevante Codeausschnitte in der Liste, indem Sie darauf klicken](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "die relevante Codeausschnitte in der Liste auswählen, indem Sie darauf klicken")</span><span class="sxs-lookup"><span data-stu-id="c0f40-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c0f40-604">*Wählen Sie die relevante Codeausschnitte in der Liste, indem Sie darauf klicken*</span><span class="sxs-lookup"><span data-stu-id="c0f40-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
