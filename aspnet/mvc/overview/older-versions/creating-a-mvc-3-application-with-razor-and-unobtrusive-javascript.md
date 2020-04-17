---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Erstellen einer MVC 3-Anwendung mit Razor und unauffälligem JavaScript | Microsoft Docs
author: rick-anderson
description: Die Beispielwebanwendung "Benutzerliste" veranschaulicht, wie einfach es ist, ASP.NET MVC 3-Anwendungen mit dem Razor-Ansichtsmodul zu erstellen. Die Beispielanwendung...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542455"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="0e055-104">Erstellen einer MVC 3-Anwendung mit Razor und unaufdringlichem JavaScript</span><span class="sxs-lookup"><span data-stu-id="0e055-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="0e055-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0e055-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0e055-106">Die Beispielwebanwendung "Benutzerliste" veranschaulicht, wie einfach es ist, ASP.NET MVC 3-Anwendungen mit dem Razor-Ansichtsmodul zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0e055-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="0e055-107">Die Beispielanwendung zeigt, wie Sie das neue Razor-Ansichtsmodul mit ASP.NET MVC-Version 3 und Visual Studio 2010 verwenden, um eine fiktive Benutzerlistenwebsite zu erstellen, die Funktionen wie das Erstellen, Anzeigen, Bearbeiten und Löschen von Benutzern enthält.</span><span class="sxs-lookup"><span data-stu-id="0e055-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="0e055-108">In diesem Tutorial werden die Schritte beschrieben, die zum Erstellen des Beispiels für die Benutzerliste ASP.NET MVC 3-Anwendung ausgeführt wurden.</span><span class="sxs-lookup"><span data-stu-id="0e055-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="0e055-109">Zu diesem Thema steht ein Visual Studio-Projekt mit Demento-Quellcode von C- und VB-Quellcode zur Verfügung: [Herunterladen](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="0e055-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="0e055-110">Wenn Sie Fragen zu diesem Tutorial haben, posten Sie diese bitte im [MVC-Forum](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e055-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="0e055-111">Übersicht</span><span class="sxs-lookup"><span data-stu-id="0e055-111">Overview</span></span>

<span data-ttu-id="0e055-112">Die Anwendung, die Sie erstellen werden, ist eine einfache Benutzerlisten-Website.</span><span class="sxs-lookup"><span data-stu-id="0e055-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="0e055-113">Benutzer können Benutzerinformationen eingeben, anzeigen und aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0e055-113">Users can enter, view, and update user information.</span></span>

![Beispielsite](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="0e055-115">Sie können das Projekt VB und C- abgeschlossen [hier](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)herunterladen.</span><span class="sxs-lookup"><span data-stu-id="0e055-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="0e055-116">Erstellen der Webanwendung</span><span class="sxs-lookup"><span data-stu-id="0e055-116">Creating the Web Application</span></span>

<span data-ttu-id="0e055-117">Um das Tutorial zu starten, öffnen Sie Visual Studio 2010, und erstellen Sie ein neues Projekt mit der *ASP.NET MVC 3 Web Anwendungsvorlage.*</span><span class="sxs-lookup"><span data-stu-id="0e055-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="0e055-118">Benennen Sie &quot;die Anwendung&quot;Mvc3Razor .</span><span class="sxs-lookup"><span data-stu-id="0e055-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="0e055-119">[![Neues MVC 3-Projekt](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="0e055-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="0e055-120">Wählen Sie im Dialogfeld **Neue ASP.NET MVC 3-Projekt** die Option **Internetanwendung aus**, wählen Sie das Razor-Ansichtsmodul aus, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e055-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Neue ASP.NET MVC 3 Projektdialog](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="0e055-122">In diesem Tutorial verwenden Sie nicht die ASP.NET Mitgliedschaftsanbieter, sodass Sie alle Dateien löschen können, die mit der Anmeldung und Mitgliedschaft verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="0e055-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="0e055-123">Entfernen Sie im **Projektmappen-Explorer**die folgenden Dateien und Verzeichnisse:</span><span class="sxs-lookup"><span data-stu-id="0e055-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="0e055-124">*Controller-KontoController*</span><span class="sxs-lookup"><span data-stu-id="0e055-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="0e055-125">*Modelle- und Kontomodelle*</span><span class="sxs-lookup"><span data-stu-id="0e055-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="0e055-126">*Ansichten,\\freigegebene _LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="0e055-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="0e055-127">*Views-Konto* (und alle Dateien in diesem Verzeichnis)</span><span class="sxs-lookup"><span data-stu-id="0e055-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="0e055-129">Bearbeiten Sie `<div>` die `logindisplay` <em>&quot;</em>&quot; <em> \_Datei Layout.cshtml,</em> und ersetzen Sie das Markup innerhalb des namens elements durch die Meldung Login Disabled .</span><span class="sxs-lookup"><span data-stu-id="0e055-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="0e055-130">Das folgende Beispiel zeigt das neue Markup:</span><span class="sxs-lookup"><span data-stu-id="0e055-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="0e055-131">Hinzufügen des Modells</span><span class="sxs-lookup"><span data-stu-id="0e055-131">Adding the Model</span></span>

<span data-ttu-id="0e055-132">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf den Ordner *"Modelle",* wählen **Sie Hinzufügen**aus, und klicken Sie dann auf **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="0e055-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Neue Benutzer-Mdl-Klasse](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="0e055-134">Geben Sie der Klassen den Namen `UserModel`.</span><span class="sxs-lookup"><span data-stu-id="0e055-134">Name the class `UserModel`.</span></span> <span data-ttu-id="0e055-135">Ersetzen Sie den Inhalt der *UserModel-Datei* durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="0e055-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="0e055-136">Die `UserModel` Klasse stellt Benutzer dar.</span><span class="sxs-lookup"><span data-stu-id="0e055-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="0e055-137">Jeder Member der Klasse wird mit dem [Attribut Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) aus dem [DataAnnotations-Namespace](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) mit Anmerkungen versehen.</span><span class="sxs-lookup"><span data-stu-id="0e055-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="0e055-138">Die Attribute im [DataAnnotations-Namespace](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) bieten eine automatische client- und serverseitige Validierung für Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="0e055-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="0e055-139">Öffnen `HomeController` Sie die `using` Klasse, und fügen `UserModel` Sie `Users` eine Direktive hinzu, damit Sie auf die und-Klassen zugreifen können:</span><span class="sxs-lookup"><span data-stu-id="0e055-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="0e055-140">Fügen Sie `HomeController` kurz nach der Deklaration `Users` den folgenden Kommentar und den Verweis auf eine Klasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="0e055-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="0e055-141">Die `Users` Klasse ist ein vereinfachter In-Memory-Datenspeicher, den Sie in diesem Tutorial verwenden.</span><span class="sxs-lookup"><span data-stu-id="0e055-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="0e055-142">In einer echten Anwendung würden Sie eine Datenbank verwenden, um Benutzerinformationen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="0e055-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="0e055-143">Die ersten Zeilen `HomeController` der Datei werden im folgenden Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="0e055-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="0e055-144">Erstellen Sie die Anwendung so, dass das Benutzermodell im nächsten Schritt für den Gerüstbau-Assistenten verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="0e055-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="0e055-145">Erstellen der Standardansicht</span><span class="sxs-lookup"><span data-stu-id="0e055-145">Creating the Default View</span></span>

<span data-ttu-id="0e055-146">Der nächste Schritt besteht darin, eine Aktionsmethode und eine Ansicht hinzuzufügen, um die Benutzer anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0e055-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="0e055-147">Löschen Sie die vorhandene Datei *"Ansichten", "Home" und "Index".*</span><span class="sxs-lookup"><span data-stu-id="0e055-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="0e055-148">Sie erstellen eine neue *Indexdatei,* um die Benutzer anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0e055-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="0e055-149">Ersetzen `HomeController` Sie in der Klasse `Index` den Inhalt der Methode durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="0e055-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="0e055-150">Klicken Sie mit `Index` der rechten Maustaste in die Methode, und klicken Sie dann auf **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="0e055-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Ansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="0e055-152">Wählen Sie die Option **Eine stark typisierte Ansicht erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="0e055-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="0e055-153">Wählen Sie für **Datenklasse Anzeigen**die Option **Mvc3Razor.Models.UserModel**aus.</span><span class="sxs-lookup"><span data-stu-id="0e055-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="0e055-154">(Wenn **Mvc3Razor.Models.UserModel** im Feld **Datenklassenansicht** nicht angezeigt wird, müssen Sie das Projekt erstellen.) Stellen Sie sicher, dass das Ansichtsmodul auf **Razor**eingestellt ist.</span><span class="sxs-lookup"><span data-stu-id="0e055-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="0e055-155">Legen Sie **Inhalt anzeigen** auf **Liste** fest, und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="0e055-155">Set **View content** to **List** and then click **Add**.</span></span>

![Indexansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="0e055-157">Die neue Ansicht erstellt automatisch ein Gerüst für die `Index` Benutzerdaten, die an die Ansicht übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="0e055-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="0e055-158">Untersuchen Sie die neu generierte Datei *"Ansichten" und "Home" und "Index".*</span><span class="sxs-lookup"><span data-stu-id="0e055-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="0e055-159">Die Links **"Neu erstellen**", **"Bearbeiten**", **"Details"** und **"Löschen"** funktionieren nicht, aber der Rest der Seite ist funktionsfähig.</span><span class="sxs-lookup"><span data-stu-id="0e055-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="0e055-160">Führen Sie die Seite aus.</span><span class="sxs-lookup"><span data-stu-id="0e055-160">Run the page.</span></span> <span data-ttu-id="0e055-161">Es wird eine Liste der Benutzer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0e055-161">You see a list of users.</span></span>

![Indexseite](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="0e055-163">Öffnen Sie die Datei *Index.cshtml,* und ersetzen `ActionLink` Sie das Markup für **Bearbeiten**, **Details**und **Löschen durch** den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="0e055-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="0e055-164">Der Benutzername wird als ID verwendet, um den ausgewählten Datensatz in den **Verknüpfungen Bearbeiten**, **Details**und **Löschen** zu suchen.</span><span class="sxs-lookup"><span data-stu-id="0e055-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="0e055-165">Erstellen der Detailansicht</span><span class="sxs-lookup"><span data-stu-id="0e055-165">Creating the Details View</span></span>

<span data-ttu-id="0e055-166">Der nächste Schritt besteht `Details` darin, eine Aktionsmethode und -ansicht hinzuzufügen, um Benutzerdetails anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0e055-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Details](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="0e055-168">Fügen Sie `Details` dem Startcontroller die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="0e055-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="0e055-169">Klicken Sie mit `Details` der rechten Maustaste in die Methode, und wählen Sie dann <strong>Ansicht hinzufügen</strong>aus.</span><span class="sxs-lookup"><span data-stu-id="0e055-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="0e055-170">Stellen Sie sicher, dass das Feld <strong>Datenklassenansicht</strong> <strong>Mvc3Razor.Models.UserModel</strong><em>enthält.</em></span><span class="sxs-lookup"><span data-stu-id="0e055-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="0e055-171">Legen Sie <strong>Inhalt anzeigen</strong> auf <strong>Details</strong> fest, und klicken Sie dann auf <strong>Hinzufügen</strong>.</span><span class="sxs-lookup"><span data-stu-id="0e055-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Detailansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="0e055-173">Führen Sie die Anwendung aus, und wählen Sie einen Detaillink aus.</span><span class="sxs-lookup"><span data-stu-id="0e055-173">Run the application and select a details link.</span></span> <span data-ttu-id="0e055-174">Das automatische Gerüst zeigt jede Eigenschaft im Modell an.</span><span class="sxs-lookup"><span data-stu-id="0e055-174">The automatic scaffolding shows each property in the model.</span></span>

![Details](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="0e055-176">Erstellen der Bearbeitungsansicht</span><span class="sxs-lookup"><span data-stu-id="0e055-176">Creating the Edit View</span></span>

<span data-ttu-id="0e055-177">Fügen Sie `Edit` dem Startcontroller die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="0e055-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="0e055-178">Fügen Sie eine Ansicht wie in den vorherigen Schritten hinzu, legen Sie jedoch **Inhalt** **bearbeiten**an.</span><span class="sxs-lookup"><span data-stu-id="0e055-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Hinzufügen der Bearbeitungsansicht](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="0e055-180">Führen Sie die Anwendung aus, und bearbeiten Sie den Vor- und Nachnamen eines der Benutzer.</span><span class="sxs-lookup"><span data-stu-id="0e055-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="0e055-181">Wenn Sie `DataAnnotation` gegen Einschränkungen verstoßen, die `UserModel` auf die Klasse angewendet wurden, werden beim Absenden des Formulars Validierungsfehler angezeigt, die durch Servercode erzeugt werden.</span><span class="sxs-lookup"><span data-stu-id="0e055-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="0e055-182">Wenn Sie z. B. &quot;beim&quot; &quot;Absenden des Formulars den Vornamen Ann in A&quot;ändern, wird im Formular der folgende Fehler angezeigt:</span><span class="sxs-lookup"><span data-stu-id="0e055-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="0e055-183">In diesem Tutorial behandeln Sie den Benutzernamen als Primärschlüssel.</span><span class="sxs-lookup"><span data-stu-id="0e055-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="0e055-184">Daher kann die Benutzernameneigenschaft nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="0e055-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="0e055-185">Legen Sie in der Datei *Edit.cshtml* kurz nach der Anweisung den `Html.BeginForm` Benutzernamen als ausgeblendetes Feld fest.</span><span class="sxs-lookup"><span data-stu-id="0e055-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="0e055-186">Dadurch wird die Eigenschaft im Modell übergeben.</span><span class="sxs-lookup"><span data-stu-id="0e055-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="0e055-187">Das folgende Codefragment zeigt `Hidden` die Platzierung der Anweisung:</span><span class="sxs-lookup"><span data-stu-id="0e055-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="0e055-188">Ersetzen `TextBoxFor` Sie `ValidationMessageFor` das und das Markup für den Benutzernamen durch einen `DisplayFor` Aufruf.</span><span class="sxs-lookup"><span data-stu-id="0e055-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="0e055-189">Die `DisplayFor` Methode zeigt die Eigenschaft als schreibgeschütztes Element an.</span><span class="sxs-lookup"><span data-stu-id="0e055-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="0e055-190">Das folgende Beispiel enthält das vollständige Markup.</span><span class="sxs-lookup"><span data-stu-id="0e055-190">The following example shows the completed markup.</span></span> <span data-ttu-id="0e055-191">Das `TextBoxFor` Original `ValidationMessageFor` und die Anrufe werden mit den Zeichen Razor`@* *@`begin-comment und end-comment ( ) auskommentiert.</span><span class="sxs-lookup"><span data-stu-id="0e055-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="0e055-192">Aktivieren der clientseitigen Validierung</span><span class="sxs-lookup"><span data-stu-id="0e055-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="0e055-193">Um die clientseitige Validierung in ASP.NET MVC 3 zu aktivieren, müssen Sie zwei Flags festlegen und drei JavaScript-Dateien einschließen.</span><span class="sxs-lookup"><span data-stu-id="0e055-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="0e055-194">Öffnen Sie die *Datei Web.config* der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0e055-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="0e055-195">Überprüfen `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` sie und sind in den Anwendungseinstellungen auf true festgelegt.</span><span class="sxs-lookup"><span data-stu-id="0e055-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="0e055-196">Das folgende Fragment aus der Stammdatei *Web.config* zeigt die richtigen Einstellungen an:</span><span class="sxs-lookup"><span data-stu-id="0e055-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="0e055-197">Das `UnobtrusiveJavaScriptEnabled` Festlegen auf true ermöglicht eine unauffällige Ajax- und unauffällige Clientvalidierung.</span><span class="sxs-lookup"><span data-stu-id="0e055-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="0e055-198">Wenn Sie eine unauffällige Validierung verwenden, werden die Validierungsregeln in HTML5-Attribute umgewandelt.</span><span class="sxs-lookup"><span data-stu-id="0e055-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="0e055-199">HTML5-Attributnamen können nur aus Kleinbuchstaben, Zahlen und Bindestrichen bestehen.</span><span class="sxs-lookup"><span data-stu-id="0e055-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="0e055-200">Das `ClientValidationEnabled` Festlegen auf true ermöglicht die clientseitige Validierung.</span><span class="sxs-lookup"><span data-stu-id="0e055-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="0e055-201">Durch Festlegen dieser Schlüssel in der Datei *"Web.config"* der Anwendung aktivieren Sie die Clientvalidierung und unauffälliges JavaScript für die gesamte Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0e055-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="0e055-202">Sie können diese Einstellungen auch in einzelnen Ansichten oder in Controllermethoden aktivieren oder deaktivieren, indem Sie den folgenden Code verwenden:</span><span class="sxs-lookup"><span data-stu-id="0e055-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="0e055-203">Außerdem müssen Sie mehrere JavaScript-Dateien in die gerenderte Ansicht einschließen.</span><span class="sxs-lookup"><span data-stu-id="0e055-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="0e055-204">Eine einfache Möglichkeit, JavaScript in alle Ansichten einzuschließen, besteht darin, sie der Datei *Views-Shared\\_Layout.cshtml* hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="0e055-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="0e055-205">Ersetzen `<head>` Sie das Element der \* \_Datei Layout.cshtml\* durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="0e055-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="0e055-206">Die ersten beiden jQuery-Skripte werden vom Microsoft Ajax Content Delivery Network (CDN) gehostet.</span><span class="sxs-lookup"><span data-stu-id="0e055-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="0e055-207">Durch die Nutzung des Microsoft Ajax CDN können Sie die Leistung Ihrer Anwendungen im ersten Treffer deutlich verbessern.</span><span class="sxs-lookup"><span data-stu-id="0e055-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="0e055-208">Führen Sie die Anwendung aus, und klicken Sie auf einen Bearbeitungslink.</span><span class="sxs-lookup"><span data-stu-id="0e055-208">Run the application and click an edit link.</span></span> <span data-ttu-id="0e055-209">Zeigen Sie die Quelle der Seite im Browser an.</span><span class="sxs-lookup"><span data-stu-id="0e055-209">View the page's source in the browser.</span></span> <span data-ttu-id="0e055-210">Die Browserquelle zeigt viele Attribute `data-val` des Formulars (für die Datenvalidierung).</span><span class="sxs-lookup"><span data-stu-id="0e055-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="0e055-211">Wenn die Clientvalidierung und unauffällige JavaScript aktiviert ist, enthalten Eingabefelder mit einer Clientvalidierungsregel das `data-val="true"` Attribut, um eine unauffällige Clientüberprüfung auszulösen.</span><span class="sxs-lookup"><span data-stu-id="0e055-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="0e055-212">Beispielsweise wurde `City` das Feld im Modell mit dem [Attribut Erforderlich](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) eingerichtet, was zu dem HTML-Code führt, der im folgenden Beispiel gezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="0e055-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="0e055-213">Für jede Clientvalidierungsregel wird ein Attribut `data-val-rulename="message"`hinzugefügt, das das Formular hat.</span><span class="sxs-lookup"><span data-stu-id="0e055-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="0e055-214">Im `City` zuvor gezeigten Feldbeispiel generiert die erforderliche `data-val-required` Clientvalidierungsregel das Attribut und die Meldung &quot;Das Feld "Stadt" ist erforderlich.&quot;</span><span class="sxs-lookup"><span data-stu-id="0e055-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="0e055-215">Führen Sie die Anwendung aus, bearbeiten `City` Sie einen der Benutzer, und löschen Sie das Feld.</span><span class="sxs-lookup"><span data-stu-id="0e055-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="0e055-216">Wenn Sie das Feld aus der Registerkarte herauslassen, wird eine clientseitige Validierungsfehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0e055-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Stadt erforderlich](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="0e055-218">Ebenso wird für jeden Parameter in der Clientvalidierungsregel ein `data-val-rulename-paramname=paramvalue`Attribut hinzugefügt, das das Formular hat.</span><span class="sxs-lookup"><span data-stu-id="0e055-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="0e055-219">Die `FirstName` Eigenschaft wird z. B. mit dem [StringLength-Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) mit Anmerkungen versehen und gibt eine Mindestlänge von 3 und eine maximale Länge von 8 an.</span><span class="sxs-lookup"><span data-stu-id="0e055-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="0e055-220">Die benannte `length` Datenvalidierungsregel `max` hat den Parameternamen und den Parameterwert 8.</span><span class="sxs-lookup"><span data-stu-id="0e055-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="0e055-221">Im Folgenden wird der HTML-Code angezeigt, der für das `FirstName` Feld generiert wird, wenn Sie einen der Benutzer bearbeiten:</span><span class="sxs-lookup"><span data-stu-id="0e055-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="0e055-222">Weitere Informationen zur unauffälligen Clientvalidierung finden Sie im Eintrag [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) im Blog von Brad Wilson.</span><span class="sxs-lookup"><span data-stu-id="0e055-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="0e055-223">In ASP.NET MVC 3 Beta müssen Sie das Formular manchmal einreichen, um die clientseitige Validierung zu starten.</span><span class="sxs-lookup"><span data-stu-id="0e055-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="0e055-224">Dies kann für die endgültige Version geändert werden.</span><span class="sxs-lookup"><span data-stu-id="0e055-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="0e055-225">Erstellen der Erstellungsansicht</span><span class="sxs-lookup"><span data-stu-id="0e055-225">Creating the Create View</span></span>

<span data-ttu-id="0e055-226">Der nächste Schritt besteht `Create` darin, eine Aktionsmethode und -ansicht hinzuzufügen, damit der Benutzer einen neuen Benutzer erstellen kann.</span><span class="sxs-lookup"><span data-stu-id="0e055-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="0e055-227">Fügen Sie `Create` dem Startcontroller die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="0e055-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="0e055-228">Fügen Sie eine Ansicht wie in den vorherigen Schritten hinzu, legen Sie jedoch **Inhalt** anzeigen auf **Erstellen**fest.</span><span class="sxs-lookup"><span data-stu-id="0e055-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Erstellen einer Sicht](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="0e055-230">Führen Sie die Anwendung aus, wählen Sie den Link **Erstellen** aus, und fügen Sie einen neuen Benutzer hinzu.</span><span class="sxs-lookup"><span data-stu-id="0e055-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="0e055-231">Die `Create` Methode nutzt automatisch die client- und serverseitige Validierung.</span><span class="sxs-lookup"><span data-stu-id="0e055-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="0e055-232">Versuchen Sie, einen Benutzernamen einzugeben, &quot;der&quot;Leerraum enthält, z. B. Ben X .</span><span class="sxs-lookup"><span data-stu-id="0e055-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="0e055-233">Wenn Sie das Feld Benutzername ausklappen, wird`White space is not allowed`ein clientseitig ersichtlicher Validierungsfehler ( ) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0e055-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="0e055-234">Hinzufügen der Delete-Methode</span><span class="sxs-lookup"><span data-stu-id="0e055-234">Add the Delete method</span></span>

<span data-ttu-id="0e055-235">Um das Tutorial abzuschließen, `Delete` fügen Sie dem Startcontroller die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="0e055-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="0e055-236">Fügen `Delete` Sie eine Ansicht wie in den vorherigen Schritten hinzu und legen Sie Inhalt **löschen** **ansichtsbereit** fest.</span><span class="sxs-lookup"><span data-stu-id="0e055-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Ansicht löschen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="0e055-238">Sie haben jetzt eine einfache, aber voll funktionsfähige ASP.NET MVC 3-Anwendung mit Validierung.</span><span class="sxs-lookup"><span data-stu-id="0e055-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
