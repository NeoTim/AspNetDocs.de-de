---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Erstellen benutzerdefinierter HTML-Hilfsprogramme | Microsoft Docs
author: microsoft
description: Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML Helper...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675332"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="aeb57-104">Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (C#)</span><span class="sxs-lookup"><span data-stu-id="aeb57-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="aeb57-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="aeb57-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="aeb57-106">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="aeb57-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="aeb57-107">Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="aeb57-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="aeb57-108">Durch die Nutzung von HTML-Hilfsprogrammen können Sie die Menge der mühsamen Eingabe von HTML-Tags reduzieren, die Sie ausführen müssen, um eine Standard-HTML-Seite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="aeb57-109">Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="aeb57-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="aeb57-110">Durch die Nutzung von HTML-Hilfsprogrammen können Sie die Menge der mühsamen Eingabe von HTML-Tags reduzieren, die Sie ausführen müssen, um eine Standard-HTML-Seite zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="aeb57-111">Im ersten Teil dieses Tutorials beschreibe ich einige der vorhandenen HTML-Hilfsprogramme, die im ASP.NET MVC-Framework enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="aeb57-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="aeb57-112">Als Nächstes beschreibe ich zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogrammen: Ich erkläre, wie benutzerdefinierte HTML-Hilfsprogramme erstellt werden, indem eine statische Methode erstellt und eine Erweiterungsmethode erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="aeb57-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="aeb57-113">Html-Hilfen verstehen</span><span class="sxs-lookup"><span data-stu-id="aeb57-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="aeb57-114">Ein HTML-Hilfsmann ist nur eine Methode, die eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="aeb57-115">Die Zeichenfolge kann jede beliebige Art von Inhalt darstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="aeb57-116">Sie können beispielsweise HTML-Hilfsprogramme verwenden, um `<input>` `<img>` Standard-HTML-Tags wie HTML und Tags zu rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="aeb57-117">Sie können auch HTML-Hilfsprogramme verwenden, um komplexere Inhalte wie einen Tab-Strip oder eine HTML-Tabelle mit Datenbankdaten zu rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="aeb57-118">Das ASP.NET MVC-Framework enthält den folgenden Satz von Standard-HTML-Helfern (dies ist keine vollständige Liste):</span><span class="sxs-lookup"><span data-stu-id="aeb57-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="aeb57-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="aeb57-119">Html.ActionLink()</span></span>
- <span data-ttu-id="aeb57-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="aeb57-120">Html.BeginForm()</span></span>
- <span data-ttu-id="aeb57-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="aeb57-121">Html.CheckBox()</span></span>
- <span data-ttu-id="aeb57-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="aeb57-122">Html.DropDownList()</span></span>
- <span data-ttu-id="aeb57-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="aeb57-123">Html.EndForm()</span></span>
- <span data-ttu-id="aeb57-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="aeb57-124">Html.Hidden()</span></span>
- <span data-ttu-id="aeb57-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="aeb57-125">Html.ListBox()</span></span>
- <span data-ttu-id="aeb57-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="aeb57-126">Html.Password()</span></span>
- <span data-ttu-id="aeb57-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="aeb57-127">Html.RadioButton()</span></span>
- <span data-ttu-id="aeb57-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="aeb57-128">Html.TextArea()</span></span>
- <span data-ttu-id="aeb57-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="aeb57-129">Html.TextBox()</span></span>

<span data-ttu-id="aeb57-130">Betrachten Sie beispielsweise das Formular in Liste 1.</span><span class="sxs-lookup"><span data-stu-id="aeb57-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="aeb57-131">Dieses Formular wird mit Hilfe von zwei der Standard-HTML-Helfer gerendert (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="aeb57-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="aeb57-132">Dieses Formular `Html.BeginForm()` verwendet `Html.TextBox()` die und Helper-Methoden, um ein einfaches HTML-Formular zu rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="aeb57-133">[![Mit HTML-Helfern gerenderte Seite](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="aeb57-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="aeb57-134">**Abbildung 01**: Seite gerendert mit HTML-Hilfsprogrammen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="aeb57-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="aeb57-135">**Auflistung 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="aeb57-136">Die Html.BeginForm() Helper-Methode wird verwendet, `<form>` um das Öffnen und Schließen von HTML-Tags zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="aeb57-137">Beachten Sie, dass die `Html.BeginForm()` Methode innerhalb einer using-Anweisung aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="aeb57-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="aeb57-138">Die using-Anweisung `<form>` stellt sicher, dass das Tag am Ende des using-Blocks geschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="aeb57-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="aeb57-139">Wenn Sie möchten, können Sie anstelle des Erstellens eines Using-Blocks die Html.EndForm()-Hilfsmethode aufrufen, um das `<form>` Tag zu schließen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="aeb57-140">Verwenden Sie den Ansatz, um `<form>` ein öffnendes und schließendes Tag zu erstellen, das Ihnen am intuitivsten erscheint.</span><span class="sxs-lookup"><span data-stu-id="aeb57-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="aeb57-141">Die `Html.TextBox()` Hilfsmethoden werden in Liste 1 `<input>` zum Rendern von HTML-Tags verwendet.</span><span class="sxs-lookup"><span data-stu-id="aeb57-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="aeb57-142">Wenn Sie die Quellquelle in Ihrem Browser auswählen, wird die HTML-Quelle in Liste 2 angezeigt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="aeb57-143">Beachten Sie, dass die Quelle Standard-HTML-Tags enthält.</span><span class="sxs-lookup"><span data-stu-id="aeb57-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aeb57-144">Beachten Sie, dass der `Html.TextBox()`-HTML-Helfer mit `<%= %>` Tags anstelle von `<% %>` Tags gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="aeb57-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="aeb57-145">Wenn Sie das Gleichheitszeichen nicht einschließen, wird nichts im Browser gerendert.</span><span class="sxs-lookup"><span data-stu-id="aeb57-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="aeb57-146">Das ASP.NET MVC-Framework enthält eine kleine Gruppe von Helfern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="aeb57-147">Wahrscheinlich müssen Sie das MVC-Framework um benutzerdefinierte HTML-Hilfsprogramme erweitern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="aeb57-148">Im WeiterenVerlauf dieses Tutorials lernen Sie zwei Methoden zum Erstellen benutzerdefinierter HTML-Hilfsprogramme.</span><span class="sxs-lookup"><span data-stu-id="aeb57-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="aeb57-149">**Auflistung 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="aeb57-150">Erstellen von HTML-Hilfsprogrammen mit statischen Methoden</span><span class="sxs-lookup"><span data-stu-id="aeb57-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="aeb57-151">Die einfachste Möglichkeit zum Erstellen eines neuen HTML-Hilfselements besteht darin, eine statische Methode zu erstellen, die eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="aeb57-152">Stellen Sie sich beispielsweise vor, dass Sie einen neuen HTML-Helfer erstellen, der ein HTML-Tag `<label>` rendert.</span><span class="sxs-lookup"><span data-stu-id="aeb57-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="aeb57-153">Sie können die Klasse in Liste `<label>` 2 verwenden, um eine zu rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="aeb57-154">**Auflistung 2 –`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="aeb57-155">Es gibt nichts Besonderes an der Klasse in Listing 2.</span><span class="sxs-lookup"><span data-stu-id="aeb57-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="aeb57-156">Die `Label()` Methode gibt einfach eine Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="aeb57-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="aeb57-157">Die geänderte Indexansicht in `LabelHelper` Liste `<label>` 3 verwendet die zum Rendern von HTML-Tags.</span><span class="sxs-lookup"><span data-stu-id="aeb57-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="aeb57-158">Beachten Sie, dass `<%@ imports %>` die Ansicht `Application1.Helpers` eine Direktive enthält, die den Namespace importiert.</span><span class="sxs-lookup"><span data-stu-id="aeb57-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="aeb57-159">**Auflistung 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="aeb57-160">Erstellen von HTML-Hilfsprogrammen mit Erweiterungsmethoden</span><span class="sxs-lookup"><span data-stu-id="aeb57-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="aeb57-161">Wenn Sie HTML-Hilfsprogramme erstellen möchten, die genau wie die Standard-HTML-Hilfsprogramme funktionieren, die im ASP.NET MVC-Framework enthalten sind, müssen Sie Erweiterungsmethoden erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="aeb57-162">Mithilfe von Erweiterungsmethoden können Sie einer vorhandenen Klasse neue Methoden hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="aeb57-163">Beim Erstellen einer HTML-Hilfsmethode fügen Sie der HtmlHelper-Klasse, die durch die Html-Eigenschaft einer Ansicht dargestellt wird, neue Methoden hinzu.</span><span class="sxs-lookup"><span data-stu-id="aeb57-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="aeb57-164">Die Klasse in Listing 3 fügt `HtmlHelper` der `Label()`Klasse mit dem Namen eine Erweiterungsmethode hinzu.</span><span class="sxs-lookup"><span data-stu-id="aeb57-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="aeb57-165">Es gibt ein paar Dinge, die Sie über diese Klasse bemerken sollten.</span><span class="sxs-lookup"><span data-stu-id="aeb57-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="aeb57-166">Beachten Sie zunächst, dass es sich bei der Klasse um eine statische Klasse handelt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="aeb57-167">Sie müssen eine Erweiterungsmethode mit einer statischen Klasse definieren.</span><span class="sxs-lookup"><span data-stu-id="aeb57-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="aeb57-168">Beachten Sie zweitens, dass `Label()` dem ersten Parameter `this`der Methode das Schlüsselwort vorangestellt wird.</span><span class="sxs-lookup"><span data-stu-id="aeb57-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="aeb57-169">Der erste Parameter einer Erweiterungsmethode gibt die Klasse an, die die Erweiterungsmethode erweitert.</span><span class="sxs-lookup"><span data-stu-id="aeb57-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="aeb57-170">**Auflistung 3 –`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="aeb57-171">Nachdem Sie eine Erweiterungsmethode erstellt und die Anwendung erfolgreich erstellt haben, wird die Erweiterungsmethode in Visual Studio Intellisense wie alle anderen Methoden einer Klasse angezeigt (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="aeb57-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="aeb57-172">Der einzige Unterschied besteht darin, dass Erweiterungsmethoden mit einem speziellen Symbol neben ihnen angezeigt werden (ein Symbol eines Abwärtspfeils).</span><span class="sxs-lookup"><span data-stu-id="aeb57-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="aeb57-173">[![Verwenden der Html.Label()-Erweiterungsmethode](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="aeb57-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="aeb57-174">**Abbildung 02**: Verwenden der Html.Label()-Erweiterungsmethode ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="aeb57-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="aeb57-175">Die geänderte Indexansicht in Listing 4 verwendet die Html.Label()-Erweiterungsmethode, um alle tags `<label>` zu rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="aeb57-176">**Auflistung 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="aeb57-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="aeb57-177">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="aeb57-177">Summary</span></span>

<span data-ttu-id="aeb57-178">In diesem Tutorial haben Sie zwei Methoden zum Erstellen benutzerdefinierter HTML-Hilfsprogramme gelernt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="aeb57-179">Zuerst haben Sie gelernt, `Label()` wie Sie einen benutzerdefinierten HTML-Hilfsmittel erstellen, indem Sie eine statische Methode erstellen, die eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="aeb57-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="aeb57-180">Als Nächstes haben Sie gelernt, wie Sie eine benutzerdefinierte `Label()` `HtmlHelper` HTML-Hilfsmethode erstellen, indem Sie eine Erweiterungsmethode für die Klasse erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeb57-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="aeb57-181">In diesem Tutorial habe ich mich auf den Aufbau einer extrem einfachen HTML-Hilfsmethode konzentriert.</span><span class="sxs-lookup"><span data-stu-id="aeb57-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="aeb57-182">Beachten Sie, dass ein HTML-Helfer so kompliziert sein kann, wie Sie möchten.</span><span class="sxs-lookup"><span data-stu-id="aeb57-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="aeb57-183">Sie können HTML-Hilfsprogramme erstellen, die umfangreiche Inhalte wie Baumansichten, Menüs oder Tabellen mit Datenbankdaten rendern.</span><span class="sxs-lookup"><span data-stu-id="aeb57-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aeb57-184">[Zurück](asp-net-mvc-views-overview-cs.md)
> [Weiter](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="aeb57-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
