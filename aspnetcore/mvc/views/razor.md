---
title: Razor-Syntaxreferenz für ASP.NET Core
author: rick-anderson
description: Informationen zur Razor-Markupsyntax zum Einbetten von serverbasiertem Code in Webseiten
ms.author: riande
ms.date: 10/26/2018
uid: mvc/views/razor
ms.openlocfilehash: 8e9ec3c5040e5a24cd5f773b1232897338741c0c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052497"
---
# <a name="razor-syntax-reference-for-aspnet-core"></a><span data-ttu-id="05188-103">Razor-Syntaxreferenz für ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="05188-103">Razor syntax reference for ASP.NET Core</span></span>

<span data-ttu-id="05188-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen) und [Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="05188-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="05188-105">Razor stellt eine Markupsyntax zum Einbetten von serverbasiertem Code in Webseiten dar.</span><span class="sxs-lookup"><span data-stu-id="05188-105">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="05188-106">Die Razor-Syntax besteht aus dem Razor-Markup, C# und HTML.</span><span class="sxs-lookup"><span data-stu-id="05188-106">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="05188-107">Dateien, die Razor enthalten, besitzen in der Regel die Dateierweiterung *.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05188-107">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="05188-108">Rendern von HTML</span><span class="sxs-lookup"><span data-stu-id="05188-108">Rendering HTML</span></span>

<span data-ttu-id="05188-109">Die Standardsprache für Razor ist HTML.</span><span class="sxs-lookup"><span data-stu-id="05188-109">The default Razor language is HTML.</span></span> <span data-ttu-id="05188-110">Das Rendern von HTML-Code aus einem Razor-Markup funktioniert genauso wie das Rendern von HTML aus einer HTML-Datei.</span><span class="sxs-lookup"><span data-stu-id="05188-110">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span> <span data-ttu-id="05188-111">Ein HTML-Markup wird in Razor-Dateien mit der Erweiterung *.cshtml* vom Server unverändert gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-111">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="05188-112">Razor-Syntax</span><span class="sxs-lookup"><span data-stu-id="05188-112">Razor syntax</span></span>

<span data-ttu-id="05188-113">Razor unterstützt C# und verwendet für den Übergang von HTML zu C# das `@`-Symbol.</span><span class="sxs-lookup"><span data-stu-id="05188-113">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="05188-114">Razor wertet C#-Ausdrücke aus und rendert sie in der HTML-Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="05188-114">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="05188-115">Folgt auf ein `@`-Symbol [ein für Razor reserviertes Schlüsselwort](#razor-reserved-keywords), wechselt es in ein Razor-spezifisches Markup.</span><span class="sxs-lookup"><span data-stu-id="05188-115">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="05188-116">Andernfalls erfolgt der Übergang in normales C#.</span><span class="sxs-lookup"><span data-stu-id="05188-116">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="05188-117">Verwenden Sie ein zweites `@`-Symbol, um im Razor-Markup ein `@`-Symbol mit Escapezeichen zu versehen:</span><span class="sxs-lookup"><span data-stu-id="05188-117">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="05188-118">Der Code wird in HTML mit einem einzelnen `@`-Symbol gerendert:</span><span class="sxs-lookup"><span data-stu-id="05188-118">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="05188-119">Bei HTML-Attributen und Inhalt mit E-Mail-Adressen wird das `@`-Symbol nicht als ein Übergangszeichen behandelt.</span><span class="sxs-lookup"><span data-stu-id="05188-119">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="05188-120">Die E-Mail-Adressen im folgenden Beispiel bleiben von der Razor-Analyse unverändert:</span><span class="sxs-lookup"><span data-stu-id="05188-120">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="05188-121">Implizite Razor-Ausdrücke</span><span class="sxs-lookup"><span data-stu-id="05188-121">Implicit Razor expressions</span></span>

<span data-ttu-id="05188-122">Implizite Razor-Ausdrücke beginnen mit `@` gefolgt von C#-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-122">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="05188-123">Mit Ausnahme des C#-Schlüsselworts `await` dürfen implizite Ausdrücke keine Leerzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="05188-123">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="05188-124">Wird die C#-Anweisung eindeutig beendet, können auch Leerzeichen verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="05188-124">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="05188-125">Implizite Ausdrücke dürfen **keine** C#-Generika enthalten, da die Zeichen innerhalb der Klammern (`<>`) als HTML-Tag interpretiert werden.</span><span class="sxs-lookup"><span data-stu-id="05188-125">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="05188-126">Der folgende Code ist **ungültig**:</span><span class="sxs-lookup"><span data-stu-id="05188-126">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="05188-127">Der vorhergehende Code erzeugt einen Compilerfehler, der folgendermaßen aussehen kann:</span><span class="sxs-lookup"><span data-stu-id="05188-127">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="05188-128">Das Element „int“ wurde nicht geschlossen.</span><span class="sxs-lookup"><span data-stu-id="05188-128">The "int" element wasn't closed.</span></span> <span data-ttu-id="05188-129">Alle Elemente müssen entweder selbstschließend sein oder ein zugehöriges Endtag besitzen.</span><span class="sxs-lookup"><span data-stu-id="05188-129">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="05188-130">Die Methodengruppe „GenericMethod“ kann nicht in den Nichtdelegattyp „Objekt“ konvertiert werden.</span><span class="sxs-lookup"><span data-stu-id="05188-130">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="05188-131">Wollten Sie die Methode aufrufen?</span><span class="sxs-lookup"><span data-stu-id="05188-131">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="05188-132">Generische Methodenaufrufe müssen von einem [expliziten Razor-Ausdruck](#explicit-razor-expressions) oder einem [Razor-Codeblock](#razor-code-blocks) umschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="05188-132">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="05188-133">Explizite Razor-Ausdrücke</span><span class="sxs-lookup"><span data-stu-id="05188-133">Explicit Razor expressions</span></span>

<span data-ttu-id="05188-134">Explizite Razor-Ausdrücke bestehen aus einem `@`-Symbol mit ausgeglichener Klammer.</span><span class="sxs-lookup"><span data-stu-id="05188-134">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="05188-135">Zum Rendern der Uhrzeit von letzter Woche wird folgendes Razor-Markup verwendet:</span><span class="sxs-lookup"><span data-stu-id="05188-135">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="05188-136">Jeglicher Inhalt innerhalb der `@()`-Klammer wird ausgewertet und in der Ausgabe gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-136">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="05188-137">Die im vorherigen Abschnitt beschriebenen impliziten Ausdrücke dürfen grundsätzlich keine Leerzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="05188-137">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="05188-138">Im folgenden Code wird eine Woche nicht von der aktuellen Uhrzeit abgezogen:</span><span class="sxs-lookup"><span data-stu-id="05188-138">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="05188-139">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-139">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="05188-140">Explizite Ausdrücke können zum Verketten von Text mit einem Ergebnis des Ausdrucks verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="05188-140">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="05188-141">Ohne den expliziten Ausdruck wird `<p>Age@joe.Age</p>` als E-Mail-Adresse behandelt und `<p>Age@joe.Age</p>` gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-141">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="05188-142">`<p>Age33</p>` wird gerendert, wenn es als expliziter Ausdruck geschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="05188-142">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>

<span data-ttu-id="05188-143">Explizite Ausdrücke können zum Rendern der Ausgabe von generischen Methoden in *.cshtml*-Dateien verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="05188-143">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="05188-144">Das folgende Markup zeigt, wie der weiter oben gezeigte Fehler behoben wird, der durch die Klammern einer generischen C#-Funktion verursacht wurde.</span><span class="sxs-lookup"><span data-stu-id="05188-144">The following markup shows how to correct the error shown earlier caused by the brackets of a C# generic.</span></span> <span data-ttu-id="05188-145">Der Code wird als expliziter Ausdruck geschrieben:</span><span class="sxs-lookup"><span data-stu-id="05188-145">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="05188-146">Codieren von Ausdrücken</span><span class="sxs-lookup"><span data-stu-id="05188-146">Expression encoding</span></span>

<span data-ttu-id="05188-147">C#-Ausdrücke, die als Zeichenfolge ausgewertet werden, werden HTML-codiert.</span><span class="sxs-lookup"><span data-stu-id="05188-147">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="05188-148">C#-Ausdrücke, die als `IHtmlContent` ausgewertet werden, werden direkt durch `IHtmlContent.WriteTo` gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-148">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="05188-149">C#-Ausdrücke, die nicht als `IHtmlContent` ausgewertet werden, werden durch `ToString` in eine Zeichenfolge konvertiert und vor dem Rendern codiert.</span><span class="sxs-lookup"><span data-stu-id="05188-149">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="05188-150">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-150">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="05188-151">Der HTML-Code wird im Browser folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="05188-151">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="05188-152">Die Ausgabe `HtmlHelper.Raw` wird nicht codiert, sondern als HTML-Markup gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-152">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="05188-153">Die Verwendung von `HtmlHelper.Raw` bei einer nicht bereinigten Benutzereingabe stellt ein Sicherheitsrisiko dar.</span><span class="sxs-lookup"><span data-stu-id="05188-153">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="05188-154">Benutzereingaben können schädlichen JavaScript-Code oder andere Sicherheitsrisiken enthalten.</span><span class="sxs-lookup"><span data-stu-id="05188-154">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="05188-155">Das Bereinigen von Benutzereingaben ist schwierig.</span><span class="sxs-lookup"><span data-stu-id="05188-155">Sanitizing user input is difficult.</span></span> <span data-ttu-id="05188-156">Vermeiden Sie daher die Verwendung von `HtmlHelper.Raw` bei Benutzereingaben.</span><span class="sxs-lookup"><span data-stu-id="05188-156">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="05188-157">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-157">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="05188-158">Razor-Codeblöcke</span><span class="sxs-lookup"><span data-stu-id="05188-158">Razor code blocks</span></span>

<span data-ttu-id="05188-159">Razor-Codeblöcke beginnen mit `@` und sind von `{}` eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="05188-159">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="05188-160">Im Gegensatz zu Ausdrücken wird C#-Code in Codeblöcken nicht gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-160">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="05188-161">Codeblöcke und Ausdrücke in einer Ansicht nutzen den gleichen Bereich und werden der Reihe nach definiert:</span><span class="sxs-lookup"><span data-stu-id="05188-161">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="05188-162">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-162">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="05188-163">Implizite Übergänge</span><span class="sxs-lookup"><span data-stu-id="05188-163">Implicit transitions</span></span>

<span data-ttu-id="05188-164">Die Standardsprache in einem Codeblock ist C#. Die Razor Page kann jedoch zurück zu HTML wechseln:</span><span class="sxs-lookup"><span data-stu-id="05188-164">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="05188-165">Durch Trennzeichen getrennte explizite Übergänge</span><span class="sxs-lookup"><span data-stu-id="05188-165">Explicit delimited transition</span></span>

<span data-ttu-id="05188-166">Soll ein Unterabschnitt eines Codeblocks in HTML gerendert werden, umschließen Sie die Zeichen, die gerendert werden sollen, mit dem Razor-Tag **\<text>**:</span><span class="sxs-lookup"><span data-stu-id="05188-166">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="05188-167">Verwenden Sie diese Methode zum Rendern von HTML-Code, der nicht von einem HTML-Tag umschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="05188-167">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="05188-168">Ohne HTML- oder Razor-Tag tritt ein Razor-Laufzeitfehler auf.</span><span class="sxs-lookup"><span data-stu-id="05188-168">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="05188-169">Das **\<text>**-Tag ist nützlich, wenn Sie beim Rendern von Inhalt Leerzeichen steuern möchten:</span><span class="sxs-lookup"><span data-stu-id="05188-169">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="05188-170">Nur der Inhalt zwischen den **\<text>**-Tags wird gerendert.</span><span class="sxs-lookup"><span data-stu-id="05188-170">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="05188-171">In der HTML-Ausgabe werden keine Leerzeichen vor oder nach dem **\<text>**-Tag angezeigt.</span><span class="sxs-lookup"><span data-stu-id="05188-171">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="05188-172">Explizite Zeilenübergänge mit @:</span><span class="sxs-lookup"><span data-stu-id="05188-172">Explicit Line Transition with @:</span></span>

<span data-ttu-id="05188-173">Verwenden Sie die `@:`-Syntax, um den Rest einer kompletten Zeile als HTML-Code in einem Codeblock zu rendern:</span><span class="sxs-lookup"><span data-stu-id="05188-173">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="05188-174">Ohne das `@:`-Symbol im Code wird ein Razor-Laufzeitfehler erzeugt.</span><span class="sxs-lookup"><span data-stu-id="05188-174">Without the `@:` in the code, a Razor runtime error is generated.</span></span>

<span data-ttu-id="05188-175">Warnung: Zusätzliche `@`-Zeichen in einer Razor-Datei können zu Compilerfehlern bei späteren Anweisungen im Block führen.</span><span class="sxs-lookup"><span data-stu-id="05188-175">Warning: Extra `@` characters in a Razor file can cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="05188-176">Diese Compilerfehler können dann schwer nachvollziehbar sein, da der tatsächliche vor dem gemeldeten Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="05188-176">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span> <span data-ttu-id="05188-177">Dieser Fehler tritt häufig auf, wenn mehrere implizite/explizite Ausdrücke in einem einzigen Codeblock kombiniert werden.</span><span class="sxs-lookup"><span data-stu-id="05188-177">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="05188-178">Steuerungsstrukturen</span><span class="sxs-lookup"><span data-stu-id="05188-178">Control structures</span></span>

<span data-ttu-id="05188-179">Steuerungsstrukturen sind eine Erweiterung von Codeblöcken.</span><span class="sxs-lookup"><span data-stu-id="05188-179">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="05188-180">Alle Aspekte von Codeblöcken (Übergang zu Markup, Inline-C#) gelten auch für die folgenden Strukturen:</span><span class="sxs-lookup"><span data-stu-id="05188-180">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="05188-181">Die Bedingungen @if, else if, else und @switch</span><span class="sxs-lookup"><span data-stu-id="05188-181">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="05188-182">`@if` steuert, wann der Code ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="05188-182">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="05188-183">`else` und `else if` erfordern kein `@`-Symbol:</span><span class="sxs-lookup"><span data-stu-id="05188-183">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="05188-184">Im folgenden Markup wird die Verwendung einer switch-Anweisung veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="05188-184">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="05188-185">Die Schleifen @for, @foreach, @while und @do while</span><span class="sxs-lookup"><span data-stu-id="05188-185">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="05188-186">Auf Vorlagen basierender HTML-Code kann mit Anweisungen zur Steuerung von Schleifen gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="05188-186">Templated HTML can be rendered with looping control statements.</span></span> <span data-ttu-id="05188-187">So rendern Sie eine Liste mit Personen.</span><span class="sxs-lookup"><span data-stu-id="05188-187">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="05188-188">Die folgenden Schleifenanweisungen werden unterstützt:</span><span class="sxs-lookup"><span data-stu-id="05188-188">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="05188-189">Zusammengesetztes @using</span><span class="sxs-lookup"><span data-stu-id="05188-189">Compound @using</span></span>

<span data-ttu-id="05188-190">In C# kann mit einer `using`-Anweisung sichergestellt werden, dass ein Objekt freigegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="05188-190">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="05188-191">In Razor wird derselbe Mechanismus verwendet, um HTML-Hilfsprogramme zu erstellen, die zusätzliche Inhalte enthalten.</span><span class="sxs-lookup"><span data-stu-id="05188-191">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="05188-192">Im folgenden Code wird ein Formulartag mit der `@using`-Anweisung durch HTML-Hilfsprogramme gerendert:</span><span class="sxs-lookup"><span data-stu-id="05188-192">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="05188-193">Aktionen auf Bereichsebene können mit [Taghilfsprogrammen](xref:mvc/views/tag-helpers/intro) ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="05188-193">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="05188-194">@try, catch, finally</span><span class="sxs-lookup"><span data-stu-id="05188-194">@try, catch, finally</span></span>

<span data-ttu-id="05188-195">Die Behandlung von Ausnahmen ist vergleichbar mit C#:</span><span class="sxs-lookup"><span data-stu-id="05188-195">Exception handling is similar to C#:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="05188-196">Razor kann kritische Abschnitte mit lock-Anweisungen schützen:</span><span class="sxs-lookup"><span data-stu-id="05188-196">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="05188-197">Kommentare</span><span class="sxs-lookup"><span data-stu-id="05188-197">Comments</span></span>

<span data-ttu-id="05188-198">Razor unterstützt C#- und HTML-Kommentare:</span><span class="sxs-lookup"><span data-stu-id="05188-198">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="05188-199">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-199">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="05188-200">Razor-Kommentare werden vom Server entfernt, bevor die Webseite gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="05188-200">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="05188-201">Zur Abgrenzung der Kommentare verwendet Razor `@*  *@`.</span><span class="sxs-lookup"><span data-stu-id="05188-201">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="05188-202">Der folgende Code ist auskommentiert, damit vom Server kein Markup gerendert wird:</span><span class="sxs-lookup"><span data-stu-id="05188-202">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="05188-203">Anweisungen</span><span class="sxs-lookup"><span data-stu-id="05188-203">Directives</span></span>

<span data-ttu-id="05188-204">Razor-Anweisungen werden durch implizite Ausdrücke mit reservierten Schlüsselwörtern nach dem `@`-Symbol dargestellt.</span><span class="sxs-lookup"><span data-stu-id="05188-204">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="05188-205">Eine Anweisung ändert in der Regel die Analyse einer Ansicht oder aktiviert unterschiedliche Funktionen.</span><span class="sxs-lookup"><span data-stu-id="05188-205">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="05188-206">Wenn Sie wissen, wie von Razor Code für eine Ansicht generiert wird, erleichtert dies das Verständnis dafür, wie Anweisungen funktionieren.</span><span class="sxs-lookup"><span data-stu-id="05188-206">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="05188-207">Durch den Code wird eine Klasse ähnlich der folgenden generiert:</span><span class="sxs-lookup"><span data-stu-id="05188-207">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="05188-208">Im Abschnitt [Überprüfen der Razor-C#-Klasse, die für eine Ansicht generiert wurde](#inspect-the-razor-c-class-generated-for-a-view) weiter unten wird erklärt, wie die generierte Klasse angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="05188-208">Later in this article, the section [Inspect the Razor C# class generated for a view](#inspect-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

<a name="using"></a>
### <a name="using"></a>@using

<span data-ttu-id="05188-209">Die `@using`-Anweisung fügt die C#-Anweisung `using`der generierten Ansicht hinzu:</span><span class="sxs-lookup"><span data-stu-id="05188-209">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="05188-210">Die `@model`-Anweisung gibt den Typ des Modells an, das an eine Ansicht übergeben wird:</span><span class="sxs-lookup"><span data-stu-id="05188-210">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="05188-211">In einer mit einzelnen Benutzerkonten erstellten ASP.NET Core MVC-App enthält die Ansicht *Views/Account/Login.cshtml* die folgende Modelldeklaration:</span><span class="sxs-lookup"><span data-stu-id="05188-211">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="05188-212">Die generierte Klasse erbt von `RazorPage<dynamic>`:</span><span class="sxs-lookup"><span data-stu-id="05188-212">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="05188-213">Razor macht eine `Model`-Eigenschaft für den Zugriff auf das an die Ansicht übergebene Modell verfügbar:</span><span class="sxs-lookup"><span data-stu-id="05188-213">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="05188-214">Die `@model`-Anweisung gibt den Typ dieser Eigenschaft an.</span><span class="sxs-lookup"><span data-stu-id="05188-214">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="05188-215">Die Anweisung legt das `T` in `RazorPage<T>` der generierten Klasse fest, von der die Ansicht abgeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="05188-215">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="05188-216">Wird die `@model`-Anweisung nicht angegeben, hat die `Model`-Eigenschaft den Typ `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="05188-216">If the `@model` directive isn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="05188-217">Der Wert des Modells wird vom Controller an die Ansicht übergeben.</span><span class="sxs-lookup"><span data-stu-id="05188-217">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="05188-218">Weitere Informationen finden Sie unter [Stark typisierte Modelle und das Schlüsselwort &commat;model](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword).</span><span class="sxs-lookup"><span data-stu-id="05188-218">For more information, see [Strongly typed models and the &commat;model keyword](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword).</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="05188-219">Die `@inherits`-Anweisung bietet uneingeschränkten Zugriff auf die Klasse, die die Ansicht erbt:</span><span class="sxs-lookup"><span data-stu-id="05188-219">The `@inherits` directive provides full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="05188-220">Der folgende Code ist ein benutzerdefinierter Typ der Razor Page:</span><span class="sxs-lookup"><span data-stu-id="05188-220">The following code is a custom Razor page type:</span></span>

[!code-csharp[](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="05188-221">`CustomText` wird in einer Ansicht angezeigt:</span><span class="sxs-lookup"><span data-stu-id="05188-221">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="05188-222">Der Code rendert den folgenden HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="05188-222">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="05188-223">`@model` und `@inherits` können in derselben Ansicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="05188-223">`@model` and `@inherits` can be used in the same view.</span></span> <span data-ttu-id="05188-224">`@inherits` kann in einer *_ViewImports.cshtml*-Datei verwendet werden, die von der Ansicht importiert wird:</span><span class="sxs-lookup"><span data-stu-id="05188-224">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="05188-225">Der folgende Code ist ein Beispiel für eine stark typisierte Ansicht:</span><span class="sxs-lookup"><span data-stu-id="05188-225">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="05188-226">Wird „rick@contoso.com“ im Modell übergeben, generiert die Ansicht das folgende HTML-Markup:</span><span class="sxs-lookup"><span data-stu-id="05188-226">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject

<span data-ttu-id="05188-227">Mit der `@inject`-Anweisung kann die Razor Page einen Dienst aus dem [Dienstcontainer](xref:fundamentals/dependency-injection) in eine Ansicht einfügen.</span><span class="sxs-lookup"><span data-stu-id="05188-227">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="05188-228">Weitere Informationen finden Sie unter [Dependency Injection in Ansichten](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="05188-228">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="05188-229">Mit der `@functions`-Anweisung kann eine Razor-Seite einer Ansicht einen C#-Codeblock hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="05188-229">The `@functions` directive enables a Razor Page to add a C# code block to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="05188-230">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="05188-230">For example:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="05188-231">Der Code generiert das folgende HTML-Markup:</span><span class="sxs-lookup"><span data-stu-id="05188-231">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="05188-232">Der folgende Code wird in der Razor-C#-Klasse generiert:</span><span class="sxs-lookup"><span data-stu-id="05188-232">The following code is the generated Razor C# class:</span></span>

[!code-csharp[](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="05188-233">Die `@section`-Anweisung wird in Verbindung mit dem [Layout](xref:mvc/views/layout) verwendet, damit Ansichten Inhalte in verschiedenen Teilen der HTML-Seite rendern können.</span><span class="sxs-lookup"><span data-stu-id="05188-233">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="05188-234">Weitere Informationen finden Sie unter [Abschnitte](xref:mvc/views/layout#layout-sections-label).</span><span class="sxs-lookup"><span data-stu-id="05188-234">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="templated-razor-delegates"></a><span data-ttu-id="05188-235">Auf Vorlagen basierende Razor-Delegate</span><span class="sxs-lookup"><span data-stu-id="05188-235">Templated Razor delegates</span></span>

<span data-ttu-id="05188-236">Mit Razor-Vorlagen können Sie einen Ausschnitt der Benutzeroberfläche mit dem folgenden Format festlegen:</span><span class="sxs-lookup"><span data-stu-id="05188-236">Razor templates allow you to define a UI snippet with the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="05188-237">Im folgenden Beispiel wird veranschaulicht, wie ein auf Vorlagen basierender Razor-Delegat als <xref:System.Func`2> angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="05188-237">The following example illustrates how to specify a templated Razor delegate as a <xref:System.Func`2>.</span></span> <span data-ttu-id="05188-238">Der Typ [dynamic](/dotnet/csharp/programming-guide/types/using-type-dynamic) wird für den Parameter der Methode angegeben, die der Delegat einkapselt.</span><span class="sxs-lookup"><span data-stu-id="05188-238">The [dynamic type](/dotnet/csharp/programming-guide/types/using-type-dynamic) is specified for the parameter of the method that the delegate encapsulates.</span></span> <span data-ttu-id="05188-239">Ein [object](/dotnet/csharp/language-reference/keywords/object)-Typ wird als Rückgabewert des Delegats angegeben.</span><span class="sxs-lookup"><span data-stu-id="05188-239">An [object type](/dotnet/csharp/language-reference/keywords/object) is specified as the return value of the delegate.</span></span> <span data-ttu-id="05188-240">Die Vorlage wird mit <xref:System.Collections.Generic.List`1> von `Pet` mit einer `Name`-Eigenschaft verwendet.</span><span class="sxs-lookup"><span data-stu-id="05188-240">The template is used with a <xref:System.Collections.Generic.List`1> of `Pet` that has a `Name` property.</span></span>

```csharp
public class Pet
{
    public string Name { get; set; }
}
```

```cshtml
@{
    Func<dynamic, object> petTemplate = @<p>You have a pet named <strong>@item.Name</strong>.</p>;

    var pets = new List<Pet>
    {
        new Pet { Name = "Rin Tin Tin" },
        new Pet { Name = "Mr. Bigglesworth" },
        new Pet { Name = "K-9" }
    };
}
```

<span data-ttu-id="05188-241">Die Vorlage wird mit `pets` in einer `foreach`-Anweisung gerendert:</span><span class="sxs-lookup"><span data-stu-id="05188-241">The template is rendered with `pets` supplied by a `foreach` statement:</span></span>

```cshtml
@foreach (var pet in pets)
{
    @petTemplate(pet)
}
```

<span data-ttu-id="05188-242">Gerenderte Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="05188-242">Rendered output:</span></span>

```html
<p>You have a pet named <strong>Rin Tin Tin</strong>.</p>
<p>You have a pet named <strong>Mr. Bigglesworth</strong>.</p>
<p>You have a pet named <strong>K-9</strong>.</p>
```

<span data-ttu-id="05188-243">Sie können auch eine Razor-Inlinevorlage als Argument für eine Methode angeben.</span><span class="sxs-lookup"><span data-stu-id="05188-243">You can also supply an inline Razor template as an argument to a method.</span></span> <span data-ttu-id="05188-244">Im folgenden Beispiel nimmt die `Repeat`-Methode eine Razor-Vorlage entgegen.</span><span class="sxs-lookup"><span data-stu-id="05188-244">In the following example, the `Repeat` method receives a Razor template.</span></span> <span data-ttu-id="05188-245">Die Methode verwendet die Vorlage dann zum Erstellen von HTML-Inhalten mit Wiederholungen von Elementen aus einer Liste:</span><span class="sxs-lookup"><span data-stu-id="05188-245">The method uses the template to produce HTML content with repeats of items supplied from a list:</span></span>

```cshtml
@using Microsoft.AspNetCore.Html

@functions {
    public static IHtmlContent Repeat(IEnumerable<dynamic> items, int times, 
        Func<dynamic, IHtmlContent> template)
    {
        var html = new HtmlContentBuilder();

        foreach (var item in items)
        {
            for (var i = 0; i < times; i++)
            {
                html.AppendHtml(template(item));
            }
        }

        return html;
    }
}
```

<span data-ttu-id="05188-246">Wird die Liste mit Haustieren aus dem vorherigen Beispiel verwendet, wird die `Repeat`-Methode wie folgt aufgerufen:</span><span class="sxs-lookup"><span data-stu-id="05188-246">Using the list of pets from the prior example, the `Repeat` method is called with:</span></span>

* <span data-ttu-id="05188-247"><xref:System.Collections.Generic.List`1> von `Pet`</span><span class="sxs-lookup"><span data-stu-id="05188-247"><xref:System.Collections.Generic.List`1> of `Pet`.</span></span>
* <span data-ttu-id="05188-248">Anzahl der Wiederholungen für jedes Haustier</span><span class="sxs-lookup"><span data-stu-id="05188-248">Number of times to repeat each pet.</span></span>
* <span data-ttu-id="05188-249">Inlinevorlage zur Verwendung für die Elemente einer unsortierten Liste</span><span class="sxs-lookup"><span data-stu-id="05188-249">Inline template to use for the list items of an unordered list.</span></span>

```cshtml
<ul>
    @Repeat(pets, 3, @<li>@item.Name</li>)
</ul>
```

<span data-ttu-id="05188-250">Gerenderte Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="05188-250">Rendered output:</span></span>

```html
<ul>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>K-9</li>
    <li>K-9</li>
    <li>K-9</li>
</ul>
```

## <a name="tag-helpers"></a><span data-ttu-id="05188-251">Taghilfsprogramme</span><span class="sxs-lookup"><span data-stu-id="05188-251">Tag Helpers</span></span>

<span data-ttu-id="05188-252">Die folgenden drei Anweisungen gehören zu den [Taghilfsprogrammen](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="05188-252">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="05188-253">Anweisung</span><span class="sxs-lookup"><span data-stu-id="05188-253">Directive</span></span> | <span data-ttu-id="05188-254">Funktion</span><span class="sxs-lookup"><span data-stu-id="05188-254">Function</span></span> |
| --------- | -------- |
| [<span data-ttu-id="05188-255">&commat;addTagHelper</span><span class="sxs-lookup"><span data-stu-id="05188-255">&commat;addTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="05188-256">Macht Taghilfsprogramme für eine Ansicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="05188-256">Makes Tag Helpers available to a view.</span></span> |
| [<span data-ttu-id="05188-257">&commat;removeTagHelper</span><span class="sxs-lookup"><span data-stu-id="05188-257">&commat;removeTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="05188-258">Entfernt zuvor hinzugefügte Taghilfsprogramme aus einer Ansicht.</span><span class="sxs-lookup"><span data-stu-id="05188-258">Removes Tag Helpers previously added from a view.</span></span> |
| [<span data-ttu-id="05188-259">&commat;tagHelperPrefix</span><span class="sxs-lookup"><span data-stu-id="05188-259">&commat;tagHelperPrefix</span></span>](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="05188-260">Gibt ein Tagpräfix an, um Unterstützung für Taghilfsprogramme zu aktivieren und ihre Verwendung explizit zu machen.</span><span class="sxs-lookup"><span data-stu-id="05188-260">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="05188-261">Für Razor reservierte Schlüsselwörter</span><span class="sxs-lookup"><span data-stu-id="05188-261">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="05188-262">Razor-Schlüsselwörter</span><span class="sxs-lookup"><span data-stu-id="05188-262">Razor keywords</span></span>

* <span data-ttu-id="05188-263">page (ASP.NET Core 2.0 und höher)</span><span class="sxs-lookup"><span data-stu-id="05188-263">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="05188-264">namespace</span><span class="sxs-lookup"><span data-stu-id="05188-264">namespace</span></span>
* <span data-ttu-id="05188-265">functions</span><span class="sxs-lookup"><span data-stu-id="05188-265">functions</span></span>
* <span data-ttu-id="05188-266">inherits</span><span class="sxs-lookup"><span data-stu-id="05188-266">inherits</span></span>
* <span data-ttu-id="05188-267">model</span><span class="sxs-lookup"><span data-stu-id="05188-267">model</span></span>
* <span data-ttu-id="05188-268">section</span><span class="sxs-lookup"><span data-stu-id="05188-268">section</span></span>
* <span data-ttu-id="05188-269">helper (wird derzeit nicht von ASP.NET Core unterstützt)</span><span class="sxs-lookup"><span data-stu-id="05188-269">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="05188-270">Razor-Schlüsselwörter werden mit dem Escapezeichen `@(Razor Keyword)` versehen (z.B. `@(functions)`).</span><span class="sxs-lookup"><span data-stu-id="05188-270">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="05188-271">Razor-C#-Schlüsselwörter</span><span class="sxs-lookup"><span data-stu-id="05188-271">C# Razor keywords</span></span>

* <span data-ttu-id="05188-272">case</span><span class="sxs-lookup"><span data-stu-id="05188-272">case</span></span>
* <span data-ttu-id="05188-273">do</span><span class="sxs-lookup"><span data-stu-id="05188-273">do</span></span>
* <span data-ttu-id="05188-274">default</span><span class="sxs-lookup"><span data-stu-id="05188-274">default</span></span>
* <span data-ttu-id="05188-275">for</span><span class="sxs-lookup"><span data-stu-id="05188-275">for</span></span>
* <span data-ttu-id="05188-276">foreach</span><span class="sxs-lookup"><span data-stu-id="05188-276">foreach</span></span>
* <span data-ttu-id="05188-277">if</span><span class="sxs-lookup"><span data-stu-id="05188-277">if</span></span>
* <span data-ttu-id="05188-278">else</span><span class="sxs-lookup"><span data-stu-id="05188-278">else</span></span>
* <span data-ttu-id="05188-279">lock</span><span class="sxs-lookup"><span data-stu-id="05188-279">lock</span></span>
* <span data-ttu-id="05188-280">switch</span><span class="sxs-lookup"><span data-stu-id="05188-280">switch</span></span>
* <span data-ttu-id="05188-281">try</span><span class="sxs-lookup"><span data-stu-id="05188-281">try</span></span>
* <span data-ttu-id="05188-282">catch</span><span class="sxs-lookup"><span data-stu-id="05188-282">catch</span></span>
* <span data-ttu-id="05188-283">finally</span><span class="sxs-lookup"><span data-stu-id="05188-283">finally</span></span>
* <span data-ttu-id="05188-284">using</span><span class="sxs-lookup"><span data-stu-id="05188-284">using</span></span>
* <span data-ttu-id="05188-285">while</span><span class="sxs-lookup"><span data-stu-id="05188-285">while</span></span>

<span data-ttu-id="05188-286">Razor-C#-Schlüsselwörter werden mit dem doppeltem Escapezeichen `@(@C# Razor Keyword)` versehen (z.B. `@(@case)`).</span><span class="sxs-lookup"><span data-stu-id="05188-286">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="05188-287">Das erste `@` dient als Escapezeichen für den Razor-Parser.</span><span class="sxs-lookup"><span data-stu-id="05188-287">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="05188-288">Das zweite `@` dient als Escapezeichen für den C#-Parser.</span><span class="sxs-lookup"><span data-stu-id="05188-288">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="05188-289">Reservierte Schlüsselwörter, die nicht von Razor verwendet werden</span><span class="sxs-lookup"><span data-stu-id="05188-289">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="05188-290">class</span><span class="sxs-lookup"><span data-stu-id="05188-290">class</span></span>

## <a name="inspect-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="05188-291">Überprüfen der Razor-C#-Klasse, die für eine Ansicht generiert wurde</span><span class="sxs-lookup"><span data-stu-id="05188-291">Inspect the Razor C# class generated for a view</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="05188-292">Bei .NET Core SDK 2.1 oder höher führt das [Razor SDK](xref:razor-pages/sdk) die Kompilierung von Razor-Dateien durch.</span><span class="sxs-lookup"><span data-stu-id="05188-292">With .NET Core SDK 2.1 or later, the [Razor SDK](xref:razor-pages/sdk) handles compilation of Razor files.</span></span> <span data-ttu-id="05188-293">Beim Erstellen eines Projekts generiert das Razor SDK das Verzeichnis *obj/<build_konfiguration>/<ziel_framework_bezeichnung>/Razor* im Projektstamm.</span><span class="sxs-lookup"><span data-stu-id="05188-293">When building a project, the Razor SDK generates an *obj/<build_configuration>/<target_framework_moniker>/Razor* directory in the project root.</span></span> <span data-ttu-id="05188-294">Die Verzeichnisstruktur im *Razor*-Verzeichnis spiegelt die Verzeichnisstruktur des Projekts.</span><span class="sxs-lookup"><span data-stu-id="05188-294">The directory structure within the *Razor* directory mirrors the project's directory structure.</span></span>

<span data-ttu-id="05188-295">Beachten Sie die folgende Verzeichnisstruktur in einem Razor Pages-Projekt in ASP.NET Core 2.1 für .NET Core 2.1:</span><span class="sxs-lookup"><span data-stu-id="05188-295">Consider the following directory structure in an ASP.NET Core 2.1 Razor Pages project targeting .NET Core 2.1:</span></span>

* <span data-ttu-id="05188-296">**Areas/**</span><span class="sxs-lookup"><span data-stu-id="05188-296">**Areas/**</span></span>
  * <span data-ttu-id="05188-297">**Admin/**</span><span class="sxs-lookup"><span data-stu-id="05188-297">**Admin/**</span></span>
    * <span data-ttu-id="05188-298">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="05188-298">**Pages/**</span></span>
      * <span data-ttu-id="05188-299">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="05188-299">*Index.cshtml*</span></span>
      * <span data-ttu-id="05188-300">*Index.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-300">*Index.cshtml.cs*</span></span>
* <span data-ttu-id="05188-301">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="05188-301">**Pages/**</span></span>
  * <span data-ttu-id="05188-302">**Shared/**</span><span class="sxs-lookup"><span data-stu-id="05188-302">**Shared/**</span></span>
    * <span data-ttu-id="05188-303">*_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="05188-303">*_Layout.cshtml*</span></span>
  * <span data-ttu-id="05188-304">*_ViewImports.cshtml*</span><span class="sxs-lookup"><span data-stu-id="05188-304">*_ViewImports.cshtml*</span></span>
  * <span data-ttu-id="05188-305">*_ViewStart.cshtml*</span><span class="sxs-lookup"><span data-stu-id="05188-305">*_ViewStart.cshtml*</span></span>
  * <span data-ttu-id="05188-306">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="05188-306">*Index.cshtml*</span></span>
  * <span data-ttu-id="05188-307">*Index.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-307">*Index.cshtml.cs*</span></span>

<span data-ttu-id="05188-308">Wenn Sie das Projekt mit der Konfiguration zum *Debuggen* erstellen, wird folgendes *obj*-Verzeichnis erstellt:</span><span class="sxs-lookup"><span data-stu-id="05188-308">Building the project in *Debug* configuration yields the following *obj* directory:</span></span>

* <span data-ttu-id="05188-309">**obj/**</span><span class="sxs-lookup"><span data-stu-id="05188-309">**obj/**</span></span>
  * <span data-ttu-id="05188-310">**Debug/**</span><span class="sxs-lookup"><span data-stu-id="05188-310">**Debug/**</span></span>
    * <span data-ttu-id="05188-311">**netcoreapp2.1/**</span><span class="sxs-lookup"><span data-stu-id="05188-311">**netcoreapp2.1/**</span></span>
      * <span data-ttu-id="05188-312">**Razor/**</span><span class="sxs-lookup"><span data-stu-id="05188-312">**Razor/**</span></span>
        * <span data-ttu-id="05188-313">**Areas/**</span><span class="sxs-lookup"><span data-stu-id="05188-313">**Areas/**</span></span>
          * <span data-ttu-id="05188-314">**Admin/**</span><span class="sxs-lookup"><span data-stu-id="05188-314">**Admin/**</span></span>
            * <span data-ttu-id="05188-315">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="05188-315">**Pages/**</span></span>
              * <span data-ttu-id="05188-316">*Index.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-316">*Index.g.cshtml.cs*</span></span>
        * <span data-ttu-id="05188-317">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="05188-317">**Pages/**</span></span>
          * <span data-ttu-id="05188-318">**Shared/**</span><span class="sxs-lookup"><span data-stu-id="05188-318">**Shared/**</span></span>
            * <span data-ttu-id="05188-319">*_Layout.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-319">*_Layout.g.cshtml.cs*</span></span>
          * <span data-ttu-id="05188-320">*_ViewImports.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-320">*_ViewImports.g.cshtml.cs*</span></span>
          * <span data-ttu-id="05188-321">*_ViewStart.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-321">*_ViewStart.g.cshtml.cs*</span></span>
          * <span data-ttu-id="05188-322">*Index.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="05188-322">*Index.g.cshtml.cs*</span></span>

<span data-ttu-id="05188-323">Öffnen Sie *obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs*, um die für *Pages/Index.cshtml* generierte Klasse anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="05188-323">To view the generated class for *Pages/Index.cshtml*, open *obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs*.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="05188-324">Fügen Sie dem ASP.NET Core MVC-Projekt die folgende Klasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="05188-324">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="05188-325">Überschreiben Sie in `Startup.ConfigureServices` die von MVC hinzugefügte `RazorTemplateEngine`-Klasse mit der `CustomTemplateEngine`-Klasse:</span><span class="sxs-lookup"><span data-stu-id="05188-325">In `Startup.ConfigureServices`, override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="05188-326">Legen Sie auf der `return csharpDocument;`-Anweisung von `CustomTemplateEngine` einen Haltepunkt fest.</span><span class="sxs-lookup"><span data-stu-id="05188-326">Set a breakpoint on the `return csharpDocument;` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="05188-327">Wenn die Ausführung des Programms am Haltepunkt angehalten wird, können Sie den Wert von `generatedCode` anzeigen.</span><span class="sxs-lookup"><span data-stu-id="05188-327">When program execution stops at the breakpoint, view the value of `generatedCode`.</span></span>

![Ansicht „Text-Schnellansicht“ von „generatedCode“](razor/_static/tvr.png)

::: moniker-end

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="05188-329">Ansicht der Suchvorgänge und Groß-/Kleinschreibung</span><span class="sxs-lookup"><span data-stu-id="05188-329">View lookups and case sensitivity</span></span>

<span data-ttu-id="05188-330">Die Razor-Ansichtsengine führt für Ansichten Suchvorgänge aus, die die Groß-/Kleinschreibung berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="05188-330">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="05188-331">Der tatsächliche Suchvorgang wird jedoch vom zugrunde liegenden Dateisystem bestimmt:</span><span class="sxs-lookup"><span data-stu-id="05188-331">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="05188-332">Dateibasierte Quelle:</span><span class="sxs-lookup"><span data-stu-id="05188-332">File based source:</span></span>
  * <span data-ttu-id="05188-333">Bei Betriebssystemen, die Dateisysteme ohne Berücksichtigung von Groß-/Kleinschreibung verwenden (z.B. Windows), wird bei Suchvorgängen nach physischen Dateianbietern die Groß- und Kleinschreibung nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="05188-333">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="05188-334">`return View("Test")` liefert beispielsweise Treffer für */Views/Home/Test.cshtml*, */Views/home/test.cshtml* sowie für jede andere Schreibweise.</span><span class="sxs-lookup"><span data-stu-id="05188-334">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="05188-335">Bei Dateisystemen, die die Groß-/Kleinschreibung berücksichtigen (z.B. Linux, OSX sowie mit `EmbeddedFileProvider`), wird die Groß-/Kleinschreibung auch bei Suchvorgängen berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="05188-335">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="05188-336">`return View("Test")` liefert beispielsweise ganz konkret Treffer für */Views/Home/Test.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05188-336">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="05188-337">Vorkompilierte Ansichten: Ab ASP.NET Core 2.0 wird bei der Suche nach vorkompilierten Ansichten unter allen Betriebssystemen die Groß-/Kleinschreibung nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="05188-337">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="05188-338">Das Verhalten ist mit dem des physischen Dateianbieters unter Windows identisch.</span><span class="sxs-lookup"><span data-stu-id="05188-338">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="05188-339">Unterscheiden sich zwei vorkompilierte Ansichten nur in der Groß-/Kleinschreibung, ist das Ergebnis der Suche nicht deterministisch.</span><span class="sxs-lookup"><span data-stu-id="05188-339">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="05188-340">Entwicklern wird empfohlen, sich bei der Groß-/Kleinschreibung von Datei- und Verzeichnisnamen an der Schreibweise folgender Begriffe zu orientieren:</span><span class="sxs-lookup"><span data-stu-id="05188-340">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

* <span data-ttu-id="05188-341">Bereichs-, Controller- und Aktionsnamen</span><span class="sxs-lookup"><span data-stu-id="05188-341">Area, controller, and action names.</span></span>
* <span data-ttu-id="05188-342">Razor Pages</span><span class="sxs-lookup"><span data-stu-id="05188-342">Razor Pages.</span></span>

<span data-ttu-id="05188-343">Durch Überprüfung der Groß-/Kleinschreibung wird sichergestellt, dass die entsprechenden Ansichten für die Bereitstellungen unabhängig von dem zugrunde liegenden Dateisystem gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="05188-343">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>
