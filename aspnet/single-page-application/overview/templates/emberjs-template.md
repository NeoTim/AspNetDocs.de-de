---
uid: single-page-application/overview/templates/emberjs-template
title: Ember.js-Vorlage | Microsoft-Dokumentation
author: xqiu
description: EmberJS-Vorlage
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: e2bb8a13a0036f1fcfdcfd03a6a6e74e886a7f2c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59406859"
---
# <a name="emberjs-template"></a><span data-ttu-id="f3739-103">EmberJS-Vorlage</span><span class="sxs-lookup"><span data-stu-id="f3739-103">EmberJS template</span></span>

<span data-ttu-id="f3739-104">by [Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="f3739-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="f3739-105">Die ember.js-MVC-Vorlage wird von Nathan Totten, Thiago Santos und Xinyang Qiu geschrieben.</span><span class="sxs-lookup"><span data-stu-id="f3739-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="f3739-106">Die ember.js-MVC-Vorlage herunterladen</span><span class="sxs-lookup"><span data-stu-id="f3739-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="f3739-107">Die ember.js-SPA-Vorlage dient Sie beim schnellen Erstellen von interaktiven clientseitigen Web-apps, die mithilfe der ember.js Einstieg.</span><span class="sxs-lookup"><span data-stu-id="f3739-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="f3739-108">"Single-Page Application" (SPA) ist der allgemeine Begriff für eine Webanwendung, die eine einzelne HTML-Seite lädt, und klicken Sie dann die Seite wird dynamisch aktualisiert, anstatt neue Seiten laden.</span><span class="sxs-lookup"><span data-stu-id="f3739-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="f3739-109">Nach dem ersten Laden der Seite werden die SPA mit dem Server über AJAX-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="f3739-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="f3739-110">AJAX ist nichts neues, aber heute bestehen die JavaScript-Frameworks, die zum Erstellen und Verwalten einer großen anspruchsvollen SPA-Anwendung zu erleichtern.</span><span class="sxs-lookup"><span data-stu-id="f3739-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="f3739-111">Darüber hinaus sind HTML5 und CSS3 jetzt zum Erstellen umfassender Benutzeroberflächen einfacher.</span><span class="sxs-lookup"><span data-stu-id="f3739-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="f3739-112">Die ember.js-SPA-Vorlage verwendet die [Ember](http://emberjs.com/) JavaScript-Bibliothek Seitenupdates von AJAX-Anforderungen zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="f3739-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="f3739-113">Ember.js verwendet Datenbindung, um die Seite mit den neuesten Daten zu synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="f3739-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="f3739-114">Auf diese Weise müssen Sie keinen Code schreiben, die erläutert, der JSON-Daten, und aktualisiert das DOM.</span><span class="sxs-lookup"><span data-stu-id="f3739-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="f3739-115">Setzen Sie stattdessen deklarativen Attribute im HTML-Code, die Ember.js mitteilen, wie Sie die Daten zu präsentieren.</span><span class="sxs-lookup"><span data-stu-id="f3739-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="f3739-116">Klicken Sie auf der Serverseite der ember.js-Vorlage ist fast identisch mit der [KnockoutJS SPA-Vorlage](../introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="f3739-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="f3739-117">ASP.NET MVC verwendet, um HTML-Dokumente und ASP.NET Web-API zur Verarbeitung von AJAX-Anforderungen vom Client fungieren.</span><span class="sxs-lookup"><span data-stu-id="f3739-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="f3739-118">Weitere Informationen zu diesen Aspekten der Vorlage finden Sie in der [Knockout.js-Vorlage](../introduction/knockoutjs-template.md) Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="f3739-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="f3739-119">Dieses Thema konzentriert sich auf die Unterschiede zwischen die Knockout-Vorlage und die ember.js-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="f3739-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="f3739-120">Erstellen Sie ein Vorlagenprojekt für ember.js-SPA</span><span class="sxs-lookup"><span data-stu-id="f3739-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="f3739-121">Herunterladen Sie und installieren Sie die Vorlage, indem Sie auf die Schaltfläche "herunterladen" oben.</span><span class="sxs-lookup"><span data-stu-id="f3739-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="f3739-122">Sie müssen möglicherweise Visual Studio neu starten.</span><span class="sxs-lookup"><span data-stu-id="f3739-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="f3739-123">In der **Vorlagen** wählen Sie im Bereich **installierte Vorlagen** und erweitern Sie die **Visual C#-** Knoten.</span><span class="sxs-lookup"><span data-stu-id="f3739-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="f3739-124">Klicken Sie unter **Visual C#-** Option **Web**.</span><span class="sxs-lookup"><span data-stu-id="f3739-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="f3739-125">Wählen Sie in der Liste der Projektvorlagen das Projekt **ASP.NET MVC 4-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="f3739-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="f3739-126">Nennen Sie das Projekt, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3739-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="f3739-127">In der **neues Projekt** Assistenten **Ember.js-SPA-Projekt**.</span><span class="sxs-lookup"><span data-stu-id="f3739-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="f3739-128">Übersicht über die ember.js SPA-Vorlage</span><span class="sxs-lookup"><span data-stu-id="f3739-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="f3739-129">Die ember.js-Vorlage verwendet eine Kombination von jQuery, Ember.js, Handlebars.js, um eine glatte, interaktive Benutzeroberfläche zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f3739-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="f3739-130">Ember.js ist eine JavaScript-Bibliothek, die ein Client-Side-MVC-Muster verwendet.</span><span class="sxs-lookup"><span data-stu-id="f3739-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="f3739-131">Ein *Vorlage*, geschrieben in die Handlebars-Vorlagensprache beschreibt die Benutzeroberfläche der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="f3739-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="f3739-132">Im Releasemodus der [Handlebars-Compiler](https://github.com/Myslik/csharp-ember-handlebars) bündeln und Kompilieren die Handlebars-Vorlage verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f3739-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="f3739-133">Ein *Modell* speichert die Anwendungsdaten, die sie auf dem Server (ToDo-Listen und ToDo-Elemente) abruft.</span><span class="sxs-lookup"><span data-stu-id="f3739-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="f3739-134">Ein *Controller* speichert den Anwendungszustand.</span><span class="sxs-lookup"><span data-stu-id="f3739-134">A *controller* stores application state.</span></span> <span data-ttu-id="f3739-135">Domänencontroller stellen häufig Modellieren von Daten an den entsprechenden Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="f3739-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="f3739-136">Ein *Ansicht* primitiven Ereignisse aus der Anwendung übersetzt und übergibt diese an den Controller.</span><span class="sxs-lookup"><span data-stu-id="f3739-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="f3739-137">Ein *Router* verwaltet Anwendungsstatus, Synchronisieren von URLs und Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="f3739-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="f3739-138">Darüber hinaus kann die Ember-Data-Bibliothek verwendet werden, zum Synchronisieren von JSON-Objekte (abgerufen vom Server über eine RESTful-API) und die Client-Modelle.</span><span class="sxs-lookup"><span data-stu-id="f3739-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="f3739-139">Die ember.js-SPA-Vorlage werden die Skripts in acht Ebenen organisiert:</span><span class="sxs-lookup"><span data-stu-id="f3739-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="f3739-140">webapi\_adapter.js, webapi\_serializer.js: Erweitert die Ember datenbibliothek mit ASP.NET Web-API arbeiten.</span><span class="sxs-lookup"><span data-stu-id="f3739-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="f3739-141">Scripts/helpers.js: Definiert die neue Ember Handlebars-Hilfsprogramme.</span><span class="sxs-lookup"><span data-stu-id="f3739-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="f3739-142">Scripts/app.js: Erstellt die app aus, und Konfigurieren der Adapter und das Serialisierungsprogramm.</span><span class="sxs-lookup"><span data-stu-id="f3739-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="f3739-143">Skripts/Anwendungsmodelle/\*js: Definiert die Modelle an.</span><span class="sxs-lookup"><span data-stu-id="f3739-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="f3739-144">Skripts/app/Views/\*js: Werden die Ansichten definiert.</span><span class="sxs-lookup"><span data-stu-id="f3739-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="f3739-145">Skripts/app/Controllern/\*js: Definiert die Controller.</span><span class="sxs-lookup"><span data-stu-id="f3739-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="f3739-146">Skripts/app/Routes Scripts/app/router.js: Definiert die Routen an.</span><span class="sxs-lookup"><span data-stu-id="f3739-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="f3739-147">Vorlagen /\*.hbs: Definiert die Handlebars-Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="f3739-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="f3739-148">Sehen wir uns einige dieser Skripts genauer an.</span><span class="sxs-lookup"><span data-stu-id="f3739-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="f3739-149">Modelle</span><span class="sxs-lookup"><span data-stu-id="f3739-149">Models</span></span>

<span data-ttu-id="f3739-150">Die Modelle werden im Ordner "Skripts/app/Models" definiert.</span><span class="sxs-lookup"><span data-stu-id="f3739-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="f3739-151">Es gibt zwei Dateien: "todoitem.js" und todoList.js.</span><span class="sxs-lookup"><span data-stu-id="f3739-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="f3739-152">**TODO.Model.js** definiert, die die clientseitige (Browser) Modelle für die to-do-Listen.</span><span class="sxs-lookup"><span data-stu-id="f3739-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="f3739-153">Es gibt zwei Modellklassen: TodoItem und der "Todolist".</span><span class="sxs-lookup"><span data-stu-id="f3739-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="f3739-154">In Ember ist Modelle eine Unterklasse der DS. Modell.</span><span class="sxs-lookup"><span data-stu-id="f3739-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="f3739-155">Ein Modell kann es sich um Eigenschaften mit Attributen haben:</span><span class="sxs-lookup"><span data-stu-id="f3739-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="f3739-156">Modelle können Beziehungen zu anderen Modellen definieren:</span><span class="sxs-lookup"><span data-stu-id="f3739-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="f3739-157">Modelle können Eigenschaften berechnet, die an anderen Eigenschaften binden:</span><span class="sxs-lookup"><span data-stu-id="f3739-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="f3739-158">Modelle können Observer-Funktionen verfügen, die aufgerufen werden, wenn eine beobachtete Eigenschaft ändert:</span><span class="sxs-lookup"><span data-stu-id="f3739-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="f3739-159">Ansichten</span><span class="sxs-lookup"><span data-stu-id="f3739-159">Views</span></span>

<span data-ttu-id="f3739-160">Die Ansichten werden im Ordner "Skripts/app/Views" definiert.</span><span class="sxs-lookup"><span data-stu-id="f3739-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="f3739-161">Eine Sicht verschiebt Ereignisse aus der Benutzeroberfläche der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="f3739-161">A view translates events from the application UI.</span></span> <span data-ttu-id="f3739-162">Ein Ereignishandler kann einen Rückruf an, die Controllerfunktionen, oder rufen Sie einfach den Datenkontext direkt.</span><span class="sxs-lookup"><span data-stu-id="f3739-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="f3739-163">Views/TodoItemEditView.js z. B. stammt der folgende Code.</span><span class="sxs-lookup"><span data-stu-id="f3739-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="f3739-164">Ereignisbehandlung für ein Eingabetextfeld definiert.</span><span class="sxs-lookup"><span data-stu-id="f3739-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="f3739-165">Controller</span><span class="sxs-lookup"><span data-stu-id="f3739-165">Controller</span></span>

<span data-ttu-id="f3739-166">Die Controller werden im Ordner "Scripts/app/Controller" definiert.</span><span class="sxs-lookup"><span data-stu-id="f3739-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="f3739-167">Um ein einzelnes Modell darstellen möchten, erweitern `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="f3739-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="f3739-168">Ein Controller kann auch eine Auflistung von Modellen durch die Erweiterung repräsentieren `Ember.ArrayController`.</span><span class="sxs-lookup"><span data-stu-id="f3739-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="f3739-169">Die TodoListController stellt z. B. ein Array von `todoList` Objekte.</span><span class="sxs-lookup"><span data-stu-id="f3739-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="f3739-170">Der Controller wird nach "Todolist"-ID, in absteigender Reihenfolge sortiert:</span><span class="sxs-lookup"><span data-stu-id="f3739-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="f3739-171">Der Controller definiert eine Funktion namens `addTodoList`, die eine neue "Todolist" erstellt und dem Array hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f3739-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="f3739-172">Um anzuzeigen, wie diese Funktion aufgerufen wird, öffnen Sie die Vorlagendatei, die mit dem Namen todoListTemplate.html, im Ordner "Templates".</span><span class="sxs-lookup"><span data-stu-id="f3739-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="f3739-173">Die folgenden Vorlagencode bindet eine Schaltfläche, um die `addTodoList` Funktion:</span><span class="sxs-lookup"><span data-stu-id="f3739-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="f3739-174">Der Controller enthält auch eine `error` -Eigenschaft, die Fehlermeldung enthält.</span><span class="sxs-lookup"><span data-stu-id="f3739-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="f3739-175">Hier ist der Vorlagencode auf die Fehlermeldung (ebenfalls in todoListTemplate.html) anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="f3739-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="f3739-176">Routen</span><span class="sxs-lookup"><span data-stu-id="f3739-176">Routes</span></span>

<span data-ttu-id="f3739-177">Router.js definiert, die Routen und die Standardvorlage aus, um anzuzeigen, wird der Zustand der Anwendung, und entspricht URLs auf Routen:</span><span class="sxs-lookup"><span data-stu-id="f3739-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="f3739-178">TodoListRoute.js lädt Daten für die TodoListRoute durch Überschreiben der SetupController-Funktion:</span><span class="sxs-lookup"><span data-stu-id="f3739-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="f3739-179">Ember verwendet Benennungskonventionen, um URLs, Routennamen, Controller und Vorlagen zu entsprechen.</span><span class="sxs-lookup"><span data-stu-id="f3739-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="f3739-180">Weitere Informationen finden Sie unter [ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) der ember.js-Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="f3739-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="f3739-181">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="f3739-181">Templates</span></span>

<span data-ttu-id="f3739-182">Ordner "Templates" enthält vier Vorlagen:</span><span class="sxs-lookup"><span data-stu-id="f3739-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="f3739-183">Application.hbs: Die Standardvorlage, die gerendert wird, wenn die Anwendung gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="f3739-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="f3739-184">about.hbs: Die Vorlage für die Route "/ Info".</span><span class="sxs-lookup"><span data-stu-id="f3739-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="f3739-185">index.hbs: Die Vorlage für den Stamm "/" weiterleiten.</span><span class="sxs-lookup"><span data-stu-id="f3739-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="f3739-186">todoList.hbs: Die Vorlage für die "/ Todo" weiterleiten.</span><span class="sxs-lookup"><span data-stu-id="f3739-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="f3739-187">\_navbar.hbs: Die Vorlage definiert, im Navigationsmenü.</span><span class="sxs-lookup"><span data-stu-id="f3739-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="f3739-188">Die Anwendungsvorlage verhält sich wie eine Masterseite.</span><span class="sxs-lookup"><span data-stu-id="f3739-188">The application template acts like a master page.</span></span> <span data-ttu-id="f3739-189">Sie enthält eine Kopfzeile, Fußzeile und ein "{{Outlet}}" zum Einfügen von anderen Vorlagen im abhängig von der Route.</span><span class="sxs-lookup"><span data-stu-id="f3739-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="f3739-190">Weitere Informationen zu den Anwendungsvorlagen in Ember, finden Sie unter [ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="f3739-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="f3739-191">Die "/ TodoList"-Vorlage enthält zwei schleifenausdrücke.</span><span class="sxs-lookup"><span data-stu-id="f3739-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="f3739-192">Wird von die äußere Schleife `{{#each controller}}`, und der inneren Schleife `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="f3739-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="f3739-193">Der folgende Code zeigt eine integrierte `Ember.Checkbox` anzuzeigen, eine benutzerdefinierte `App.TodoItemEditView`, und eine Verbindung mit einem `deleteTodo` Aktion.</span><span class="sxs-lookup"><span data-stu-id="f3739-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="f3739-194">Die `HtmlHelperExtensions` in Controllers/HtmlHelperExtensions.cs, definierte Klasse definiert ein Hilfsprogramm-Funktion zum Zwischenspeichern und die Vorlage einfügen Dateien, wenn **Debuggen** nastaven NA hodnotu **"true"** in der Datei "Web.config".</span><span class="sxs-lookup"><span data-stu-id="f3739-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="f3739-195">Diese Funktion wird von der ASP.NET MVC-Ansichtsdatei in Views/Home/App.cshtml definierten aufgerufen:</span><span class="sxs-lookup"><span data-stu-id="f3739-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="f3739-196">Die Funktion, die ohne Argumente aufgerufen, rendert alle die Vorlagendateien im Ordner "Templates".</span><span class="sxs-lookup"><span data-stu-id="f3739-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="f3739-197">Sie können auch einen Unterordner oder eine spezifische Vorlagendatei angeben.</span><span class="sxs-lookup"><span data-stu-id="f3739-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="f3739-198">Wenn **Debuggen** ist **"false"** in "Web.config", die Anwendung das Bundle-Element "~/bundles/templates" enthält.</span><span class="sxs-lookup"><span data-stu-id="f3739-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="f3739-199">Dieses Bundle-Element wird in BundleConfig.cs, verwenden die Handlebars-Compiler-Bibliothek hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="f3739-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
