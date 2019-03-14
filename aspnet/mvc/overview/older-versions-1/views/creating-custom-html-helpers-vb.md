---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (VB) | Microsoft-Dokumentation
author: microsoft
description: Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML-Hilfsobjekt...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: e62e47bceddc516af7aa18fc66ed4ca4d704d277
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034947"
---
<a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="ade93-104">Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (VB)</span><span class="sxs-lookup"><span data-stu-id="ade93-104">Creating Custom HTML Helpers (VB)</span></span>
====================
<span data-ttu-id="ade93-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ade93-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ade93-106">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="ade93-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="ade93-107">Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ade93-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ade93-108">Durch Nutzen der HTML-Hilfsprogramme, können Sie die Menge der lästige Eingabe von HTML-Tags, die Sie ausführen müssen, um eine standard-HTML-Seite zu erstellen, reduzieren.</span><span class="sxs-lookup"><span data-stu-id="ade93-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="ade93-109">Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ade93-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ade93-110">Durch Nutzen der HTML-Hilfsprogramme, können Sie die Menge der lästige Eingabe von HTML-Tags, die Sie ausführen müssen, um eine standard-HTML-Seite zu erstellen, reduzieren.</span><span class="sxs-lookup"><span data-stu-id="ade93-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="ade93-111">Im ersten Teil dieses Lernprogramms beschreibe ich einige der vorhandenen HTML-Hilfsprogramme in ASP.NET MVC-Framework enthalten.</span><span class="sxs-lookup"><span data-stu-id="ade93-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="ade93-112">Als Nächstes beschreibe ich zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme: Ich erläutern, wie zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme durch Erstellen einer freigegebenen Methode und eine Erweiterungsmethode erstellen.</span><span class="sxs-lookup"><span data-stu-id="ade93-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="ade93-113">Grundlegendes zu HTML-Hilfsprogramme</span><span class="sxs-lookup"><span data-stu-id="ade93-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="ade93-114">Ein HTML-Hilfsprogramm ist nur eine Methode, die eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="ade93-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="ade93-115">Die Zeichenfolge kann jede Art von Inhalt darstellen, die Sie möchten.</span><span class="sxs-lookup"><span data-stu-id="ade93-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="ade93-116">Beispielsweise können Sie HTML-Hilfsmethoden zum Rendern von HTML-standard HTML-Tags `<input>` und `<img>` Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="ade93-117">Sie können auch HTML-Hilfsmethoden zum Rendern komplexeren Inhalts wie z. B. eine Registerkartenleiste oder eine HTML-Tabelle von Datenbankdaten verwenden.</span><span class="sxs-lookup"><span data-stu-id="ade93-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="ade93-118">ASP.NET MVC-Framework enthält den folgenden Satz von standardmäßigen HTML-Hilfsprogramme (Dies ist keine vollständige Liste):</span><span class="sxs-lookup"><span data-stu-id="ade93-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="ade93-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="ade93-119">Html.ActionLink()</span></span>
- <span data-ttu-id="ade93-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="ade93-120">Html.BeginForm()</span></span>
- <span data-ttu-id="ade93-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="ade93-121">Html.CheckBox()</span></span>
- <span data-ttu-id="ade93-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="ade93-122">Html.DropDownList()</span></span>
- <span data-ttu-id="ade93-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="ade93-123">Html.EndForm()</span></span>
- <span data-ttu-id="ade93-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="ade93-124">Html.Hidden()</span></span>
- <span data-ttu-id="ade93-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="ade93-125">Html.ListBox()</span></span>
- <span data-ttu-id="ade93-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="ade93-126">Html.Password()</span></span>
- <span data-ttu-id="ade93-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="ade93-127">Html.RadioButton()</span></span>
- <span data-ttu-id="ade93-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="ade93-128">Html.TextArea()</span></span>
- <span data-ttu-id="ade93-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="ade93-129">Html.TextBox()</span></span>

<span data-ttu-id="ade93-130">Betrachten Sie beispielsweise das Formular in Codebeispiel 1.</span><span class="sxs-lookup"><span data-stu-id="ade93-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="ade93-131">Dieses Formular wird mit der Hilfe von zwei der standardmäßigen HTML-Hilfsprogramme gerendert (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="ade93-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="ade93-132">Dieses Formular verwendet die `Html.BeginForm()` und `Html.TextBox()` Helper-Methoden.</span><span class="sxs-lookup"><span data-stu-id="ade93-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>


<span data-ttu-id="ade93-133">[![Rendern der Seite mit HTML-Hilfsprogramme](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ade93-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="ade93-134">**Abbildung 01**: Rendern der Seite mit HTML-Hilfsprogramme ([klicken Sie, um das Bild in voller Größe anzeigen](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ade93-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>


<span data-ttu-id="ade93-135">**Codebeispiel 1: `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ade93-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="ade93-136">Die `Html.BeginForm()` Hilfsmethode wird verwendet, um das öffnende und schließende HTML erstellen `<form>` Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="ade93-137">Beachten Sie, dass die `Html.BeginForm()` Methode wird aufgerufen, in einem using Anweisung.</span><span class="sxs-lookup"><span data-stu-id="ade93-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="ade93-138">Die using-Anweisung wird sichergestellt, dass die `<form>` Tags geschlossen wird, am Ende der Verwendung von Block.</span><span class="sxs-lookup"><span data-stu-id="ade93-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="ade93-139">Falls gewünscht, statt zum Erstellen eines neuen, blockieren, können Sie die Html.EndForm() Helper-Methode zum Schließen Aufrufen der `<form>` Tag.</span><span class="sxs-lookup"><span data-stu-id="ade93-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="ade93-140">Verwenden der Ansatz, erstellen eine öffnende und schließende `<form>` Tag, der Ihnen intuitivste erscheint.</span><span class="sxs-lookup"><span data-stu-id="ade93-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="ade93-141">Die `Html.TextBox()` Helper-Methoden werden zum Rendern von HTML in Codebeispiel 1 verwendet `<input>` Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="ade93-142">Bei Auswahl von Quelltext anzeigen in Ihrem Browser sehen Sie die HTML-Quelle im Codebeispiel 2.</span><span class="sxs-lookup"><span data-stu-id="ade93-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="ade93-143">Beachten Sie, dass die Quelle die standard-HTML-Tags enthält.</span><span class="sxs-lookup"><span data-stu-id="ade93-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ade93-144">Beachten Sie, dass die `Html.TextBox()`- HTML-Hilfsprogramm wird mit gerendert `<%= %>` anstelle von tags `<% %>` Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="ade93-145">Wenn Sie nicht das Gleichheitszeichen enthalten, wird Klicken Sie dann "nothing" an den Browser gerendert.</span><span class="sxs-lookup"><span data-stu-id="ade93-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="ade93-146">ASP.NET MVC-Framework enthält eine kleine Gruppe von Hilfsprogrammen.</span><span class="sxs-lookup"><span data-stu-id="ade93-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="ade93-147">In den meisten Fällen müssen Sie das MVC-Framework für benutzerdefinierte HTML-Hilfsprogramme zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="ade93-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="ade93-148">In den Rest dieses Tutorials erfahren Sie, zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme.</span><span class="sxs-lookup"><span data-stu-id="ade93-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="ade93-149">**Codebeispiel 2: `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="ade93-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="ade93-150">Erstellen von HTML-Hilfsprogramme mit freigegebenen Methoden</span><span class="sxs-lookup"><span data-stu-id="ade93-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="ade93-151">Die einfachste Möglichkeit zum Erstellen einer neuen HTML-Hilfe ist auf eine freigegebene Methode zu erstellen, die eine Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="ade93-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="ade93-152">Angenommen, Sie können eine neue HTML-Hilfsobjekt zu erstellen, die eine HTML rendert `<label>` Tag.</span><span class="sxs-lookup"><span data-stu-id="ade93-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="ade93-153">Sie können mithilfe die Klasse in Liste 2 Rendern einer `<label>`.</span><span class="sxs-lookup"><span data-stu-id="ade93-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="ade93-154">**Codebeispiel 2: `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="ade93-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="ade93-155">Es gibt keine besonderen, über die Klasse im Codebeispiel 2.</span><span class="sxs-lookup"><span data-stu-id="ade93-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="ade93-156">Die `Label()` Methode gibt einfach eine Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="ade93-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="ade93-157">Geänderte Ansicht "Index" in Programmausdruck 3 verwendet die `LabelHelper` zum Rendern von HTML `<label>` Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="ade93-158">Beachten Sie, die die Ansicht enthält eine `<%@ imports %>` -Direktive, die den Application1.Helpers-Namespace importiert.</span><span class="sxs-lookup"><span data-stu-id="ade93-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="ade93-159">**Codebeispiel 2: `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ade93-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="ade93-160">Erstellen von HTML-Hilfsprogrammen mit Erweiterungsmethoden</span><span class="sxs-lookup"><span data-stu-id="ade93-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="ade93-161">Wenn Sie erstellen möchten wie HTML-Hilfsprogramme, der einfach funktioniert der standardmäßigen HTML-Hilfsprogramme, die in ASP.NET MVC-Framework enthalten, müssen Sie Erweiterungsmethoden erstellen.</span><span class="sxs-lookup"><span data-stu-id="ade93-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="ade93-162">Erweiterungsmethoden ermöglichen Ihnen, neue Methoden zu einer vorhandenen Klasse hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ade93-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="ade93-163">Wenn Sie eine HTML-Hilfsmethode erstellen, Sie neue Methoden zum Hinzufügen der `HtmlHelper` Klasse, die eine Ansicht des HTML-Eigenschaft dargestellt.</span><span class="sxs-lookup"><span data-stu-id="ade93-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="ade93-164">Visual Basic-Moduls in Programmausdruck 3 fügt eine Erweiterungsmethode namens `Label()` auf die `HtmlHelper` Klasse.</span><span class="sxs-lookup"><span data-stu-id="ade93-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="ade93-165">Es gibt einige Dinge, die Sie zu diesem Modul sehen.</span><span class="sxs-lookup"><span data-stu-id="ade93-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="ade93-166">Erstens ist zu beachten, dass das Modul mit versehen ist die `<Extension()>` Attribut.</span><span class="sxs-lookup"><span data-stu-id="ade93-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="ade93-167">Um dieses Attribut verwenden, müssen Sie importieren die `System.Runtime.CompilerServices` Namespace</span><span class="sxs-lookup"><span data-stu-id="ade93-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="ade93-168">Zweitens: Beachten Sie, dass der erste Parameter der `Label()` Methode stellt der `HtmlHelper` Klasse.</span><span class="sxs-lookup"><span data-stu-id="ade93-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="ade93-169">Der erste Parameter einer extensionmethode gibt an, die Klasse, die die Erweiterungsmethode erweitert wird.</span><span class="sxs-lookup"><span data-stu-id="ade93-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="ade93-170">**Codebeispiel 3: `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="ade93-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="ade93-171">Nachdem Sie eine Erweiterungsmethode erstellen, und erstellen Sie Ihre Anwendung erfolgreich, wird die Erweiterungsmethode in Visual Studio Intellisense wie alle anderen Methoden einer Klasse (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="ade93-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="ade93-172">Der einzige Unterschied ist diese Erweiterung, die Methoden mit einem speziellen Symbol neben dem Namen (ein Symbol nach unten weisenden Pfeil) angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="ade93-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="ade93-173">[![Mithilfe der Erweiterungsmethode Html.Label()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ade93-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="ade93-174">**Abbildung 02**: Mithilfe der Erweiterungsmethode Html.Label() ([klicken Sie, um das Bild in voller Größe anzeigen](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ade93-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>


<span data-ttu-id="ade93-175">Geänderte Ansicht "Index" in Listing 4 verwendet die Html.Label()-Erweiterungsmethode, um alle Rendern die &lt;Bezeichnung&gt; Tags.</span><span class="sxs-lookup"><span data-stu-id="ade93-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="ade93-176">**Codebeispiel 4: `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ade93-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="ade93-177">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ade93-177">Summary</span></span>

<span data-ttu-id="ade93-178">In diesem Tutorial haben Sie zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme.</span><span class="sxs-lookup"><span data-stu-id="ade93-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="ade93-179">Zunächst haben Sie gelernt, erstellen Sie eine benutzerdefinierte `Label()` HTML-Hilfsobjekt, indem Sie eine freigegebene Methode erstellen, gibt eine Zeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="ade93-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="ade93-180">Anschließend haben Sie gelernt, erstellen Sie eine benutzerdefinierte `Label()` HTML-Hilfsobjekt-Methode, indem Sie eine Erweiterungsmethode erstellen, auf die `HtmlHelper` Klasse.</span><span class="sxs-lookup"><span data-stu-id="ade93-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="ade93-181">Ich Schwerpunkt in diesem Tutorial erstellen eine sehr einfache HTML-Hilfsmethode.</span><span class="sxs-lookup"><span data-stu-id="ade93-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="ade93-182">Beachten Sie, dass ein HTML-Hilfsprogramm kann so kompliziert, wie Sie möchten.</span><span class="sxs-lookup"><span data-stu-id="ade93-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="ade93-183">Sie können HTML-Hilfsprogramme erstellen, die umfangreiche Inhalte, z. B. Strukturansichten, Menüs oder Tabellen der Datenbankdaten rendern.</span><span class="sxs-lookup"><span data-stu-id="ade93-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ade93-184">[Zurück](asp-net-mvc-views-overview-vb.md)
> [Weiter](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ade93-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
