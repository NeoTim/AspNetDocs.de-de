---
title: Ansichten in ASP.NET Core MVC
author: ardalis
description: Informationen zur Verarbeitung der Darstellung von App-Daten und zur Benutzerinteraktion in den Ansichten von ASP.NET Core MVC
ms.author: riande
ms.date: 12/12/2017
uid: mvc/views/overview
ms.openlocfilehash: 6c5b4d7b89ac07a85b5aad626e37855de98064eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036097"
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="445dc-103">Ansichten in ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="445dc-103">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="445dc-104">Von [Steve Smith](https://ardalis.com/) und [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="445dc-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="445dc-105">In diesem Artikel werden die Ansichten erläutert, die in ASP.NET Core MVC-Anwendungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-105">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="445dc-106">Informationen zu Razor Pages finden Sie unter [Introduction to Razor Pages (Einführung in Razor Pages)](xref:razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="445dc-106">For information on Razor Pages, see [Introduction to Razor Pages](xref:razor-pages/index).</span></span>

<span data-ttu-id="445dc-107">Im Muster Model-View-Controller (MVC) verarbeitet die *Ansicht* die Darstellung der App-Daten und der Benutzerinteraktion.</span><span class="sxs-lookup"><span data-stu-id="445dc-107">In the Model-View-Controller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="445dc-108">Bei einer Ansicht handelt es sich um eine HTML-Vorlage mit eingebettetem [Razor-Markup](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="445dc-108">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="445dc-109">Bei einem Razor-Markup handelt es sich um Code, der mit einem HTML-Markup interagiert, um eine Webseite herzustellen, die an den Client gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-109">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="445dc-110">In ASP.NET Core MVC sind Ansichten *.cshtml*-Dateien, die die [Programmiersprache C#](/dotnet/csharp/) im Razor-Markup verwenden.</span><span class="sxs-lookup"><span data-stu-id="445dc-110">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="445dc-111">In der Regel werden Ansichtsdateien in Ordnern gruppiert, die für jeden [Controller](xref:mvc/controllers/actions) der App benannt werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-111">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="445dc-112">Die Ordner werden in *Ansichten*-Ordnern im Stammverzeichnis der App gespeichert:</span><span class="sxs-lookup"><span data-stu-id="445dc-112">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Ansichtenordner werden im Projektmappen-Explorer von Visual Studio zusammen mit dem Basisordner geöffnet, um die Dateien „About.cshtml“, „Contact.cshtml“ und „Index.cshtml“ angezeigt werden.](overview/_static/views_solution_explorer.png)

<span data-ttu-id="445dc-114">Der *Basis*-Controller wird im *Ansichten*-Ordner von einem *Basis*-Ordner dargestellt.</span><span class="sxs-lookup"><span data-stu-id="445dc-114">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="445dc-115">Der *Basis*-Ordner enthält Ansichten für die (Homepage-)Webseiten *Hilfe*, *Kontakt* und *Index*.</span><span class="sxs-lookup"><span data-stu-id="445dc-115">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="445dc-116">Wenn ein Benutzer eine dieser drei Webseiten aufruft, legen Controlleraktionen im *Basis*-Controller fest, welche der drei Ansichten verwendet werden, um Webseiten zu erstellen und diese an den Benutzer zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="445dc-116">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="445dc-117">Verwenden Sie [Layouts](xref:mvc/views/layout), damit die Abschnitte der Webseiten konsistent angezeigt werden und die Wiederholung von Code vermieden wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-117">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="445dc-118">Layouts bestehen in der Regel aus der Kopfzeile, der Navigation, Menüelementen und der Fußzeile.</span><span class="sxs-lookup"><span data-stu-id="445dc-118">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="445dc-119">Die Kopf- und die Fußzeile enthalten in der Regel Markupbausteine für viele Metadatenelemente sowie Links zu Skripts und Stilelemente.</span><span class="sxs-lookup"><span data-stu-id="445dc-119">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="445dc-120">Mithilfe von Layouts können Sie die Markupbausteine in Ihren Ansichten vermeiden.</span><span class="sxs-lookup"><span data-stu-id="445dc-120">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="445dc-121">Über [Teilansichten](xref:mvc/views/partial) wird weniger Code dupliziert, indem wiederverwendbare Bestandteile der Ansichten verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-121">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="445dc-122">Sie sind z.B. nützlich für Autorenbiografien auf einem Blog, die in verschiedenen Ansichten angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-122">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="445dc-123">Bei einer Autorenbiografie handelt es sich um gewöhnlichen Inhalt von Ansichten. Sie erfordern keinen Code, der ausgeführt werden muss, um den Inhalt für die Webseite herzustellen.</span><span class="sxs-lookup"><span data-stu-id="445dc-123">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="445dc-124">Die Ansicht kann auf die Inhalte der Autorenbiografie über eine Modellbindung zugreifen. Daher sollten idealerweise Teilansichten für diese Art von Inhalt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-124">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="445dc-125">Über [Ansichtskomponenten](xref:mvc/views/view-components) können Sie genauso wie über Teilansichten Wiederholungen von Code reduzieren. Sie sind besonders geeignet für Inhalt von Ansichten, für den Code auf dem Server ausgeführt werden muss, um die Webseite zu rendern.</span><span class="sxs-lookup"><span data-stu-id="445dc-125">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="445dc-126">Ansichtskomponenten sind nützlich, wenn der gerenderte Inhalt Datenbankinformationen erfordert, z.B. bei einem Warenkorb auf einer Website.</span><span class="sxs-lookup"><span data-stu-id="445dc-126">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="445dc-127">Ansichtskomponenten sind nicht auf Modellbindungen beschränkt, um Webseitenausgaben herzustellen.</span><span class="sxs-lookup"><span data-stu-id="445dc-127">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="445dc-128">Vorteile der Verwendung von Ansichten</span><span class="sxs-lookup"><span data-stu-id="445dc-128">Benefits of using views</span></span>

<span data-ttu-id="445dc-129">Über Ansichten kann in einer MVC-App eine [Trennung von Belangen](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) erfolgen, indem das Markup der Benutzeroberfläche von anderen Bestandteilen der App getrennt wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-129">Views help to establish [separation of concerns](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="445dc-130">Das SoC-Design macht Ihre App modularer. Dies hat folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="445dc-130">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="445dc-131">Die App kann einfacher verwaltet werden, da sie besser organisiert ist.</span><span class="sxs-lookup"><span data-stu-id="445dc-131">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="445dc-132">Ansichten werden in der Regel nach App-Features gruppiert.</span><span class="sxs-lookup"><span data-stu-id="445dc-132">Views are generally grouped by app feature.</span></span> <span data-ttu-id="445dc-133">Dadurch können Sie zugehörige Ansichten leichter finden, wenn Sie an einem Feature arbeiten.</span><span class="sxs-lookup"><span data-stu-id="445dc-133">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="445dc-134">Die Bestandteile der App sind lose miteinander verknüpft.</span><span class="sxs-lookup"><span data-stu-id="445dc-134">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="445dc-135">Sie können die Ansichten der App getrennt von der Geschäftslogik und den Datenzugriffskomponenten erstellen und aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="445dc-135">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="445dc-136">Sie können die Ansichten der App verändern, müssen dafür aber nicht unbedingt andere Bestandteile der App aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="445dc-136">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="445dc-137">Sie können die Bestandteile der Benutzeroberfläche der App leichter testen, da es sich bei den Ansichten um voneinander getrennte Einheiten handelt.</span><span class="sxs-lookup"><span data-stu-id="445dc-137">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="445dc-138">Durch die verbesserte Organisation sinkt die Wahrscheinlichkeit, dass Sie versehentlich Code für die Benutzeroberfläche wiederholt schreiben.</span><span class="sxs-lookup"><span data-stu-id="445dc-138">Due to better organization, it's less likely that you'll accidentally repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="445dc-139">Erstellen einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="445dc-139">Creating a view</span></span>

<span data-ttu-id="445dc-140">Ansichten, die nur für bestimmte Controller erstellt werden, werden im Ordner *Views/[NamedesControllers]* erstellt.</span><span class="sxs-lookup"><span data-stu-id="445dc-140">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="445dc-141">Ansichten, die von mehreren Controllern verwendet werden können, werden im Ordner *Views/Shared* gespeichert.</span><span class="sxs-lookup"><span data-stu-id="445dc-141">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="445dc-142">Wenn Sie eine Ansicht erstellen möchten, fügen Sie eine neue Datei hinzu, und geben Sie ihr denselben Namen wie der zugehörigen Controlleraktion mit der Erweiterung *.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="445dc-142">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="445dc-143">Wenn Sie eine Ansicht erstellen möchten, die mit der Aktion *Hilfe* im *Basis*-Controller übereinstimmt, erstellen Sie eine *About.cshtml*-Datei im Ordner *Views/Home*:</span><span class="sxs-lookup"><span data-stu-id="445dc-143">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="445dc-144">Das *Razor*-Markup beginnt mit dem Symbol `@`.</span><span class="sxs-lookup"><span data-stu-id="445dc-144">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="445dc-145">Führen Sie C#-Anweisungen aus, indem Sie C#-Code in den [Razor-Codeblocks](xref:mvc/views/razor#razor-code-blocks) speichern, die von geschweiften Klammern (`{ ... }`) umgeben sind.</span><span class="sxs-lookup"><span data-stu-id="445dc-145">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="445dc-146">Weitere Informationen finden Sie im obenstehenden Beispiel für die Zuweisung von „Hilfe“ zu `ViewData["Title"]`.</span><span class="sxs-lookup"><span data-stu-id="445dc-146">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="445dc-147">Sie können Werte innerhalb von HTML-Code angeben, indem Sie auf den Wert mit dem Symbol `@` verweisen.</span><span class="sxs-lookup"><span data-stu-id="445dc-147">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="445dc-148">Weitere Informationen finden Sie in den Inhalten der obenstehenden Elemente `<h2>` und `<h3>`.</span><span class="sxs-lookup"><span data-stu-id="445dc-148">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="445dc-149">Der obenstehende Inhalt der Ansicht ist nur ein Teil der gesamten Webseite, die für den Benutzer gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-149">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="445dc-150">Der Rest des Seitenlayouts und andere häufig auftretende Aspekte werden in anderen Ansichtsdateien angegeben.</span><span class="sxs-lookup"><span data-stu-id="445dc-150">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="445dc-151">Weitere Informationen dazu finden Sie im Artikel [Layout](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="445dc-151">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="445dc-152">Angeben von Ansichten durch Controller</span><span class="sxs-lookup"><span data-stu-id="445dc-152">How controllers specify views</span></span>

<span data-ttu-id="445dc-153">Ansichten werden in der Regel von Aktionen als [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult) zurückgegeben. Dabei handelt es sich um eine Art [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="445dc-153">Views are typically returned from actions as a [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="445dc-154">Über Ihre Aktionsmethode kann eine `ViewResult`-Klasse direkt erstellt und zurückgegeben werden. Diese Methode wird allerdings selten genutzt.</span><span class="sxs-lookup"><span data-stu-id="445dc-154">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="445dc-155">Da die meisten Controller von [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller) erben, können Sie einfach die `View`-Hilfsprogrammmethode verwenden, um `ViewResult` zurückzugeben:</span><span class="sxs-lookup"><span data-stu-id="445dc-155">Since most controllers inherit from [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="445dc-156">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="445dc-156">*HomeController.cs*</span></span>

[!code-csharp[](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="445dc-157">Wenn diese Aktion zurückgegeben wird, wird die im letzten Abschnitt angezeigte *About.cshtml*-Ansicht als die folgende Webseite gerendert:</span><span class="sxs-lookup"><span data-stu-id="445dc-157">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Hilfe-Seite in Microsoft Edge gerendert](overview/_static/about-page.png)

<span data-ttu-id="445dc-159">Für die `View`-Hilfsprogrammmethode gibt es einige Überladungen.</span><span class="sxs-lookup"><span data-stu-id="445dc-159">The `View` helper method has several overloads.</span></span> <span data-ttu-id="445dc-160">Sie können bei Bedarf folgende Elemente angeben:</span><span class="sxs-lookup"><span data-stu-id="445dc-160">You can optionally specify:</span></span>

* <span data-ttu-id="445dc-161">Eine explizite Ansicht, die zurückgegeben werden soll:</span><span class="sxs-lookup"><span data-stu-id="445dc-161">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="445dc-162">Ein [Modell](xref:mvc/models/model-binding), das an die Ansicht übergeben werden soll:</span><span class="sxs-lookup"><span data-stu-id="445dc-162">A [model](xref:mvc/models/model-binding) to pass to the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="445dc-163">Sowohl eine Ansicht als auch ein Modell:</span><span class="sxs-lookup"><span data-stu-id="445dc-163">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="445dc-164">Ansichtsermittlung</span><span class="sxs-lookup"><span data-stu-id="445dc-164">View discovery</span></span>

<span data-ttu-id="445dc-165">Wenn eine Aktion eine Ansicht zurückgibt, wird ein Prozess namens *Ansichtsermittlung* ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="445dc-165">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="445dc-166">Über diesen Prozess wird auf Grundlage des Ansichtsnamens festgelegt, welche Ansichtsdatei verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-166">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="445dc-167">Standardmäßig gibt die `View`-Methode (`return View();`) eine Ansicht zurück, die denselben Namen wie die Aktionsmethode besitzt, über die diese aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-167">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="445dc-168">Der `ActionResult`-Methodenname *Hilfe* des Controllers wird verwendet, um nach einer Ansichtsdatei mit dem Namen *About.cshtml* zu suchen.</span><span class="sxs-lookup"><span data-stu-id="445dc-168">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="445dc-169">Zuerst sucht die Runtime im Ordner *Views/[NamedesControllers]* nach der Ansicht.</span><span class="sxs-lookup"><span data-stu-id="445dc-169">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="445dc-170">Wenn keine passende Ansicht gefunden wird, wird im Ordner *Freigegeben* nach der Ansicht gesucht.</span><span class="sxs-lookup"><span data-stu-id="445dc-170">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="445dc-171">Es macht keinen Unterschied, ob Sie implizit `ViewResult` mit `return View();` zurückgeben, oder den Ansichtsnamen mit `return View("<ViewName>");` explizit an die `View`-Methode übergeben.</span><span class="sxs-lookup"><span data-stu-id="445dc-171">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="445dc-172">In beiden Fällen sucht die Ansichtsermittlung nach einer passenden Ansichtsdatei in diesem Ordner:</span><span class="sxs-lookup"><span data-stu-id="445dc-172">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="445dc-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="445dc-173">*Views/\[ControllerName]/\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="445dc-174">*Views/Shared/\[Ansichtsname].cshtml*</span><span class="sxs-lookup"><span data-stu-id="445dc-174">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="445dc-175">Anstelle eines Ansichtsnamens kann auch ein Pfad zu einer Ansichtsdatei verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-175">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="445dc-176">Wenn Sie einen absoluten Pfad im Stammverzeichnis der App verwenden (der mit „/“ oder „~/“ beginnt), muss die Erweiterung *.cshtml* angegeben sein:</span><span class="sxs-lookup"><span data-stu-id="445dc-176">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="445dc-177">Sie können auch einen relativen Pfad verwenden, um Ansichten in verschiedenen Verzeichnissen ohne die Erweiterung *.cshtml* anzugeben.</span><span class="sxs-lookup"><span data-stu-id="445dc-177">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="445dc-178">In der `HomeController`-Klasse können Sie die Ansicht *Index* in Ihrer *Verwaltungs*-Ansicht mit einem relativen Pfad angeben:</span><span class="sxs-lookup"><span data-stu-id="445dc-178">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="445dc-179">Genauso können Sie auch das aktuelle controllerspezifische Verzeichnis mit dem Präfix „./“ angeben:</span><span class="sxs-lookup"><span data-stu-id="445dc-179">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="445dc-180">[Teilansichten](xref:mvc/views/partial) und [Ansichtskomponenten](xref:mvc/views/view-components) verwenden ähnliche (aber nicht identische) Ermittlungsmechanismen.</span><span class="sxs-lookup"><span data-stu-id="445dc-180">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="445dc-181">Sie können die Standardkonvention zum Suchen von Ansichten in der App anpassen, indem Sie eine benutzerdefinierte [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander)-Schnittstelle verwenden.</span><span class="sxs-lookup"><span data-stu-id="445dc-181">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/dotnet/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="445dc-182">Die Ansichtsermittlung ist davon abhängig, ob Ansichtsdateien über Dateinamen gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-182">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="445dc-183">Wenn das zugrunde liegende Dateisystem die Groß-/Kleinschreibung beachtet, wird wahrscheinlich auch bei den Ansichtsnamen zwischen Groß- und Kleinschreibung unterschieden.</span><span class="sxs-lookup"><span data-stu-id="445dc-183">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="445dc-184">Damit die Kompatibilität für alle Betriebssysteme eingehalten werden kann, müssen Sie Groß-/Kleinbuchstaben zwischen dem Controller und den Aktionsnamen sowie den zugeordneten Ansichtsordnern und Dateinamen aufeinander abstimmten.</span><span class="sxs-lookup"><span data-stu-id="445dc-184">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="445dc-185">Wenn ein Fehler ausgelöst wird und eine Ansichtsdatei nicht gefunden werden kann, während Sie mit einem Dateisystem arbeiten, das zwischen Groß- und Kleinbuchstaben unterscheidet, bestätigen Sie, dass die Groß-/Kleinschreibung der gesuchten Ansichtsdatei mit dem tatsächlichen Dateinamen der Ansicht übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="445dc-185">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="445dc-186">Halten Sie sich an die bewährten Methoden zum Organisieren der Dateistruktur Ihrer Ansichten, um die Beziehungen zwischen Controllern, Aktionen und Ansichten auf die Verwaltbarkeit und Klarheit auszurichten.</span><span class="sxs-lookup"><span data-stu-id="445dc-186">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="445dc-187">Übergeben von Daten an Ansichten</span><span class="sxs-lookup"><span data-stu-id="445dc-187">Passing data to views</span></span>

<span data-ttu-id="445dc-188">Übergeben Sie Daten über verschiedene Ansätze an Ansichten:</span><span class="sxs-lookup"><span data-stu-id="445dc-188">Pass data to views using several approaches:</span></span>

* <span data-ttu-id="445dc-189">Stark typisierte Daten: viewmodel</span><span class="sxs-lookup"><span data-stu-id="445dc-189">Strongly typed data: viewmodel</span></span>
* <span data-ttu-id="445dc-190">Schwach typisierte Daten</span><span class="sxs-lookup"><span data-stu-id="445dc-190">Weakly typed data</span></span>
  * <span data-ttu-id="445dc-191">`ViewData` (`ViewDataAttribute`)</span><span class="sxs-lookup"><span data-stu-id="445dc-191">`ViewData` (`ViewDataAttribute`)</span></span>
  * `ViewBag`

### <a name="strongly-typed-data-viewmodel"></a><span data-ttu-id="445dc-192">Stark typisierte Daten (viewmodel)</span><span class="sxs-lookup"><span data-stu-id="445dc-192">Strongly typed data (viewmodel)</span></span>

<span data-ttu-id="445dc-193">Wenn Sie Stabilität wünschen, sollten Sie einen [Modell](xref:mvc/models/model-binding)-Typen in der Ansicht angeben.</span><span class="sxs-lookup"><span data-stu-id="445dc-193">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="445dc-194">Das Modell wird häufig als *Ansichtsmodell* bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="445dc-194">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="445dc-195">Übergeben Sie eine Instanz des Ansichtsmodelltyps an die Ansicht aus der Aktion.</span><span class="sxs-lookup"><span data-stu-id="445dc-195">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="445dc-196">Wenn Sie ein Ansichtsmodell verwenden, um eine Ansicht zu übergeben, kann die Ansicht die Vorteile der *starken* Typüberprüfung nutzen.</span><span class="sxs-lookup"><span data-stu-id="445dc-196">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="445dc-197">Man spricht von *starker Typisierung* (oder *stark typisiert* als Adjektiv), wenn es für jede Variable und jede Konstante einen explizit definierten Typ gibt, z.B. `string`, `int` oder `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="445dc-197">*Strong typing* (or *strongly typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="445dc-198">Die Gültigkeit der in der Ansicht verwendeten Typen wird zur Kompilierzeit überprüft.</span><span class="sxs-lookup"><span data-stu-id="445dc-198">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="445dc-199">[Visual Studio](https://www.visualstudio.com/vs/) und [Visual Studio Code](https://code.visualstudio.com/) erstellen Listen von stark typisierten Klassenmembern mithilfe des Features [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="445dc-199">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="445dc-200">Wenn Sie die Eigenschaften eines Ansichtsmodell anzeigen wollen, geben Sie den Namen der Variablen für dieses an, und setzen Sie einen Punkt (`.`).</span><span class="sxs-lookup"><span data-stu-id="445dc-200">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="445dc-201">Dadurch können Sie Code schneller schreiben, und Sie machen weniger Fehler.</span><span class="sxs-lookup"><span data-stu-id="445dc-201">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="445dc-202">Geben Sie mithilfe der `@model`-Anweisung ein Modell an.</span><span class="sxs-lookup"><span data-stu-id="445dc-202">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="445dc-203">Verwenden Sie das Modell mit `@Model`:</span><span class="sxs-lookup"><span data-stu-id="445dc-203">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="445dc-204">Der Controller übergibt das Modell als Parameter, um es für die Ansicht bereitzustellen:</span><span class="sxs-lookup"><span data-stu-id="445dc-204">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="445dc-205">Es gibt keine Einschränkungen der Modelltypen, die in einer Ansicht enthalten sein sollten.</span><span class="sxs-lookup"><span data-stu-id="445dc-205">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="445dc-206">Es wird empfohlen, Plain Old CLR Object-Ansichtsmodelle (POCO) mit wenigen oder gar keinen definierten Methoden zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="445dc-206">We recommend using Plain Old CLR Object (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="445dc-207">In der Regel werden Ansichtsmodellklassen weder im Ordner *Modelle* noch in einem separaten *Ansichtsmodelle*-Ordner im Stammverzeichnis der App gespeichert.</span><span class="sxs-lookup"><span data-stu-id="445dc-207">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="445dc-208">Bei dem im zuvor genannten Beispiel verwendeten *Adresse*-Ansichtsmodell handelt es sich um ein POCO-Ansichtsmodell, das in einer Datei mit dem Namen *Address.cs* gespeichert ist:</span><span class="sxs-lookup"><span data-stu-id="445dc-208">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

<span data-ttu-id="445dc-209">Es ist möglich, für die Ansichtsmodelltypen und Unternehmensmodelltypen dieselben Klassen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="445dc-209">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="445dc-210">Wenn Sie allerdings unterschiedliche Modelle verwenden, können Ihre Ansichten unabhängig von der Geschäftslogik und den Bestandteilen zum Datenzugriff Ihrer App variieren.</span><span class="sxs-lookup"><span data-stu-id="445dc-210">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="445dc-211">Wenn Sie Modelle und Ansichtsmodelle trennen, wird mehr Sicherheit geboten, wenn Modelle die [Modellbindung](xref:mvc/models/model-binding) und die [Validierung](xref:mvc/models/validation) von Daten verwenden, die vom Benutzer an die App gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-211">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>

<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-viewdata-attribute-and-viewbag"></a><span data-ttu-id="445dc-212">Schwach typisierte Daten (ViewData, ViewData-Attribut und ViewBag)</span><span class="sxs-lookup"><span data-stu-id="445dc-212">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>

<span data-ttu-id="445dc-213">`ViewBag` *ist für die Razor-Seiten nicht verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="445dc-213">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="445dc-214">Ansichten haben nicht nur Zugriff auf stark typisierte Datensammlungen, sondern auch auf *schwach typisierte* (auch als *lose typisiert* bezeichnet).</span><span class="sxs-lookup"><span data-stu-id="445dc-214">In addition to strongly typed views, views have access to a *weakly typed* (also called *loosely typed*) collection of data.</span></span> <span data-ttu-id="445dc-215">Im Gegensatz zu starken Typen werden bei *schwachen Typen* (oder *losen Typen*) nicht explizit die Datentypen deklariert, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="445dc-215">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="445dc-216">Sie können die Sammlung schwach typisierter Daten verwenden, um kleinere Datenmengen an Controller und Ansichten zu übergeben oder sie ihnen zu entnehmen.</span><span class="sxs-lookup"><span data-stu-id="445dc-216">You can use the collection of weakly typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="445dc-217">Übergeben von Daten zwischen...</span><span class="sxs-lookup"><span data-stu-id="445dc-217">Passing data between a ...</span></span>                        | <span data-ttu-id="445dc-218">Beispiel</span><span class="sxs-lookup"><span data-stu-id="445dc-218">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="445dc-219">einem Controller und einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="445dc-219">Controller and a view</span></span>                             | <span data-ttu-id="445dc-220">Auffüllen einer Dropdownliste mit Daten</span><span class="sxs-lookup"><span data-stu-id="445dc-220">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="445dc-221">einer Ansicht und einer [Layoutansicht](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="445dc-221">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="445dc-222">Festlegen des **\<title>**-Elementinhalts in der Layoutansicht über eine Ansichtsdatei.</span><span class="sxs-lookup"><span data-stu-id="445dc-222">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="445dc-223">einer [Teilansicht](xref:mvc/views/partial) und einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="445dc-223">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="445dc-224">Ein Widget, das Daten anzeigt, die der Webseite zugrunde liegen, die der Benutzer angefordert hat.</span><span class="sxs-lookup"><span data-stu-id="445dc-224">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="445dc-225">Auf diese Sammlung kann entweder über die Eigenschaft `ViewData` oder über die Eigenschaft `ViewBag` auf Controller und Ansichten verwiesen werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-225">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="445dc-226">Die `ViewData`-Eigenschaft ist ein Wörterbuch, das aus schwach typisierten Objekten besteht.</span><span class="sxs-lookup"><span data-stu-id="445dc-226">The `ViewData` property is a dictionary of weakly typed objects.</span></span> <span data-ttu-id="445dc-227">Bei der `ViewBag`-Eigenschaft handelt es sich um einen Wrapper um `ViewData`, der dynamische Eigenschaften für die zugrunde liegende `ViewData`-Sammlung bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="445dc-227">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="445dc-228">`ViewData` und `ViewBag` werden zur Laufzeit dynamisch aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="445dc-228">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="445dc-229">Da in diesen Elementen keine Typüberprüfung zur Kompilierzeit enthalten sind, sind beide in der Regel fehleranfälliger als Ansichtsmodelle.</span><span class="sxs-lookup"><span data-stu-id="445dc-229">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="445dc-230">Aus diesem Grund verwenden Entwickler `ViewData` und `ViewBag` selten oder nie.</span><span class="sxs-lookup"><span data-stu-id="445dc-230">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>

<a name="VD"></a>

<span data-ttu-id="445dc-231">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="445dc-231">**ViewData**</span></span>

<span data-ttu-id="445dc-232">Bei `ViewData` handelt es sich um ein [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)-Objekt, auf das über `string`-Schlüssel zugegriffen wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-232">`ViewData` is a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="445dc-233">Zeichenfolgendaten können gespeichert und ohne Umwandlung direkt verwendet werden. Trotzdem müssen Sie für die Extraktion andere `ViewData`-Objektwerte in bestimmte Typen umwandeln.</span><span class="sxs-lookup"><span data-stu-id="445dc-233">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="445dc-234">Sie können `ViewData` verwenden, um Daten von Controllern an Ansichten und innerhalb von Ansichten zu übergeben, einschließlich [Teilansichten](xref:mvc/views/partial) und [Layouts](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="445dc-234">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="445dc-235">Im Folgenden finden Sie ein Beispiel, über das Werte für eine Begrüßung und eine Anrede mithilfe von `ViewData` in einer Aktion festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="445dc-235">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="445dc-236">Arbeiten Sie mit den Daten in einer Ansicht:</span><span class="sxs-lookup"><span data-stu-id="445dc-236">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="445dc-237">**ViewData-Attribut**</span><span class="sxs-lookup"><span data-stu-id="445dc-237">**ViewData attribute**</span></span>

<span data-ttu-id="445dc-238">Ein anderer Ansatz zur Verwendung von [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) ist das [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute)-Attribut.</span><span class="sxs-lookup"><span data-stu-id="445dc-238">Another approach that uses the [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) is [ViewDataAttribute](/dotnet/api/microsoft.aspnetcore.mvc.viewdataattribute).</span></span> <span data-ttu-id="445dc-239">Die Werte der Eigenschaften auf Controllern oder Razor-Seiten-Modellen, die mit `[ViewData]` versehen sind, werden in dem Verzeichnis gespeichert und daraus geladen.</span><span class="sxs-lookup"><span data-stu-id="445dc-239">Properties on controllers or Razor Page models decorated with `[ViewData]` have their values stored and loaded from the dictionary.</span></span>

<span data-ttu-id="445dc-240">Im folgenden Beispiel enthält der Home-Controller die Eigenschaft `Title`, die mit `[ViewData]` versehen ist.</span><span class="sxs-lookup"><span data-stu-id="445dc-240">In the following example, the Home controller contains a `Title` property decorated with `[ViewData]`.</span></span> <span data-ttu-id="445dc-241">Die `About`-Methode legt den Titel der Infoansicht fest:</span><span class="sxs-lookup"><span data-stu-id="445dc-241">The `About` method sets the title for the About view:</span></span>

```csharp
public class HomeController : Controller
{
    [ViewData]
    public string Title { get; set; }

    public IActionResult About()
    {
        Title = "About Us";
        ViewData["Message"] = "Your application description page.";

        return View();
    }
}
```

<span data-ttu-id="445dc-242">Greifen Sie auf der Infoansicht auf die Eigenschaft `Title` als Modelleigenschaft zu:</span><span class="sxs-lookup"><span data-stu-id="445dc-242">In the About view, access the `Title` property as a model property:</span></span>

```cshtml
<h1>@Model.Title</h1>
```

<span data-ttu-id="445dc-243">Im Layout wird der Titel aus dem ViewData-Wörterbuch gelesen:</span><span class="sxs-lookup"><span data-stu-id="445dc-243">In the layout, the title is read from the ViewData dictionary:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"] - WebApplication</title>
    ...
```

::: moniker-end

<span data-ttu-id="445dc-244">**ViewBag**</span><span class="sxs-lookup"><span data-stu-id="445dc-244">**ViewBag**</span></span>

<span data-ttu-id="445dc-245">`ViewBag` *ist für die Razor-Seiten nicht verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="445dc-245">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="445dc-246">Bei `ViewBag` handelt es sich um ein [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata)-Objekt, das den dynamischen Zugriff auf die in `ViewData` gespeicherten Objekte ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="445dc-246">`ViewBag` is a [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="445dc-247">Es ist angenehmer, mit `ViewBag` zu arbeiten, da keine Umwandlung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="445dc-247">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="445dc-248">Im Folgenden finden Sie ein Beispiel, in dem dargestellt wird, wie Sie mit `ViewBag` das gleiche Ergebnis wie mit `ViewData` erzielen:</span><span class="sxs-lookup"><span data-stu-id="445dc-248">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="445dc-249">**Gleichzeitiges Verwenden von „ViewData“ and „ViewBag“**</span><span class="sxs-lookup"><span data-stu-id="445dc-249">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="445dc-250">`ViewBag` *ist für die Razor-Seiten nicht verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="445dc-250">`ViewBag` *isn't available in Razor Pages.*</span></span>

<span data-ttu-id="445dc-251">Da `ViewData` und `ViewBag` beide auf dieselbe zugrunde liegende `ViewData`-Sammlung verweisen, können Sie sowohl `ViewData` als auch `ViewBag` verwenden, und zwischen beiden Elementen wechseln, wenn Sie Werte schreiben und lesen.</span><span class="sxs-lookup"><span data-stu-id="445dc-251">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="445dc-252">Legen Sie oben in einer *About.cshtml*-Ansicht mit `ViewBag` den Titel und mit `ViewData` die Beschreibung fest:</span><span class="sxs-lookup"><span data-stu-id="445dc-252">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="445dc-253">Lesen Sie die Eigenschaften, aber verwenden Sie `ViewData` und `ViewBag` in umgekehrter Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="445dc-253">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="445dc-254">Rufen Sie in der *_Layout.cshtml*-Datei mithilfe von `ViewData` den Titel und mithilfe von `ViewBag` die Beschreibung ab:</span><span class="sxs-lookup"><span data-stu-id="445dc-254">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="445dc-255">Bedenken Sie, dass für Zeichenfolgen mit `ViewData` keine Umwandlung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="445dc-255">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="445dc-256">`@ViewData["Title"]` kann ohne Umwandlung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-256">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="445dc-257">Sie können `ViewData` und `ViewBag` gleichzeitig verwenden und zwischen dem Lesen und Schreiben der Eigenschaften abwechseln.</span><span class="sxs-lookup"><span data-stu-id="445dc-257">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="445dc-258">Das folgende Markup wird gerendert:</span><span class="sxs-lookup"><span data-stu-id="445dc-258">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="445dc-259">**Zusammenfassung der Unterschiede zwischen „ViewData“ und „ViewBag“**</span><span class="sxs-lookup"><span data-stu-id="445dc-259">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="445dc-260">`ViewBag` ist für die Razor Pages nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="445dc-260">`ViewBag` isn't available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="445dc-261">Wird von [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) abgeleitet und verfügt daher über Wörterbucheigenschaften wie `ContainsKey`, `Add`, `Remove` und `Clear`, die nützlich sein können.</span><span class="sxs-lookup"><span data-stu-id="445dc-261">Derives from [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="445dc-262">Schlüssel sind Zeichenfolgen im Wörterbuch. Daher sind Leerzeichen erlaubt.</span><span class="sxs-lookup"><span data-stu-id="445dc-262">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="445dc-263">Ein Beispiel: `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="445dc-263">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="445dc-264">Jeder Typ, der von `string` abweicht, muss in der Ansicht umgewandelt werden, sodass `ViewData` verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="445dc-264">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="445dc-265">Wird von [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) abgeleitet. Daher können dynamische Eigenschaften über die Punktnotation (`@ViewBag.SomeKey = <value or object>`) erstellt werden, und es ist keine Umwandlung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="445dc-265">Derives from [DynamicViewData](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="445dc-266">Über die Syntax von `ViewBag` können Controller und Ansichten schneller hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-266">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="445dc-267">Es ist einfacher, nach NULL-Werten zu suchen.</span><span class="sxs-lookup"><span data-stu-id="445dc-267">Simpler to check for null values.</span></span> <span data-ttu-id="445dc-268">Ein Beispiel: `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="445dc-268">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="445dc-269">**Empfohlene Verwendung von „ViewData“ und „ViewBag“**</span><span class="sxs-lookup"><span data-stu-id="445dc-269">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="445dc-270">`ViewData` und `ViewBag` sind beides gültige Ansätze, wenn Sie kleinere Datenmengen zwischen Controllern und Ansichten übergeben möchten.</span><span class="sxs-lookup"><span data-stu-id="445dc-270">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="445dc-271">Sie können beliebig entscheiden, welche Methode Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="445dc-271">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="445dc-272">Sie können zwar `ViewData`- und `ViewBag`-Objekte miteinander vermischen, jedoch ist es einfacher, den Code zu lesen und zu verwalten, wenn nur ein Ansatz verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="445dc-272">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="445dc-273">Beide Ansätze werden zur Laufzeit dynamisch aufgelöst, wodurch häufig Laufzeitfehler entstehen.</span><span class="sxs-lookup"><span data-stu-id="445dc-273">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="445dc-274">Einige Entwicklerteams vermeiden diese Ansätze daher.</span><span class="sxs-lookup"><span data-stu-id="445dc-274">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="445dc-275">Dynamische Ansichten</span><span class="sxs-lookup"><span data-stu-id="445dc-275">Dynamic views</span></span>

<span data-ttu-id="445dc-276">Ansichten, die einen Modelltyp nicht mit `@model` deklarieren, an die aber eine Modellinstanz übergeben wird (z.B. `return View(Address);`), können dynamisch auf die Eigenschaften der Instanz verweisen:</span><span class="sxs-lookup"><span data-stu-id="445dc-276">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="445dc-277">Dieses Feature bietet zwar Flexibilität, jedoch weder Kompilierungsschutz noch IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="445dc-277">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="445dc-278">Wenn die Eigenschaft nicht vorhanden ist, löst die Webseitengenerierung zur Laufzeit einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="445dc-278">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="445dc-279">Weitere Ansichtsfeatures</span><span class="sxs-lookup"><span data-stu-id="445dc-279">More view features</span></span>

<span data-ttu-id="445dc-280">Mithilfe von [Taghilfsprogrammen](xref:mvc/views/tag-helpers/intro) können Sie einfach serverseitiges Verhalten zu vorhandenen HTML-Tags hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="445dc-280">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="445dc-281">Wenn Sie Taghilfsprogramme verwenden, müssen Sie keinen benutzerdefinierten Code oder Hilfsprogramme in Ihren Ansichten schreiben.</span><span class="sxs-lookup"><span data-stu-id="445dc-281">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="445dc-282">Taghilfsprogramme werden als Attribute für HTML-Elemente angewendet und werden von Editors ignoriert, da sie diese nicht verarbeiten können.</span><span class="sxs-lookup"><span data-stu-id="445dc-282">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="445dc-283">Dadurch können Sie Ansichtsmarkups in verschiedenen Tools bearbeiten und rendern.</span><span class="sxs-lookup"><span data-stu-id="445dc-283">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="445dc-284">Sie können benutzerdefinierte HTML-Markups über verschiedene integrierte HTML-Hilfsprogramme generieren.</span><span class="sxs-lookup"><span data-stu-id="445dc-284">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="445dc-285">Eine komplexere Logik von Benutzeroberflächen kann über [Ansichtskomponenten](xref:mvc/views/view-components) verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-285">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="445dc-286">Ansichtskomponenten stellen dieselben SoC-Designs bereit, die Controller und Ansichten bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="445dc-286">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="445dc-287">Wenn diese verwendet werden, werden keine Aktionen und Ansichten benötigt, die Daten verarbeiten, die von häufig verwendeten Benutzeroberflächenelementen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="445dc-287">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="445dc-288">Wie viele andere Aspekte von ASP.NET Core unterstützen Ansichten [Dependency Injection](xref:fundamentals/dependency-injection) und lassen zu, dass Dienste [in Ansichten eingefügt werden](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="445dc-288">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>
