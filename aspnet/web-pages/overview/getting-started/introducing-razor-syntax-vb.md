---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Einführung in ASP.NET-Webprogrammierung mithilfe der Razor-Syntax (Visual Basic) | Microsoft-Dokumentation
author: Rick-Anderson
description: Dieser Anhang enthält eine Übersicht der mit ASP.NET Web Pages-Programmierung in Visual Basic mit Razor-Syntax.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: e6b63afb9492e810e19999c7c7ffe074ad510bda
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59406768"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="fc36a-103">Einführung in ASP.NET-Webprogrammierung mithilfe der Razor-Syntax (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="fc36a-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="fc36a-104">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fc36a-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fc36a-105">Dieser Artikel bietet Ihnen einen Überblick über die Programmierung mit ASP.NET Web Pages mit der Razor-Syntax und Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="fc36a-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="fc36a-106">ASP.NET ist die Technologie von Microsoft für die Ausführung von dynamischen Webseiten auf Webservern.</span><span class="sxs-lookup"><span data-stu-id="fc36a-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="fc36a-107">**Sie lernen Folgendes**:</span><span class="sxs-lookup"><span data-stu-id="fc36a-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="fc36a-108">Das obere 8 Programmiertipps für die ersten Schritte mit ASP.NET Web Pages mit Razor-Syntax.</span><span class="sxs-lookup"><span data-stu-id="fc36a-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="fc36a-109">Grundlegende Programmierkonzepte kennen, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="fc36a-110">Welche ASP.NET-Servercode: und die Razor-Syntax geht.</span><span class="sxs-lookup"><span data-stu-id="fc36a-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="fc36a-111">Software-Versionen</span><span class="sxs-lookup"><span data-stu-id="fc36a-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="fc36a-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="fc36a-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="fc36a-113">In diesem Tutorial funktioniert auch mit ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="fc36a-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="fc36a-114">Die meisten Beispiele für die Verwendung von ASP.NET Web Pages mit Razor-Syntax Verwenden von c#.</span><span class="sxs-lookup"><span data-stu-id="fc36a-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="fc36a-115">Die Razor-Syntax unterstützt aber auch Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="fc36a-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="fc36a-116">Um eine ASP.NET-Webseite in Visual Basic zu programmieren, erstellen Sie eine Webseite mit einem *vbhtml* Dateierweiterung, und fügen Sie Visual Basic-Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc36a-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="fc36a-117">Dieser Artikel bietet Ihnen einen Überblick über die Arbeit mit Visual Basic-Sprache und Syntax zum Erstellen von ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="fc36a-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="fc36a-118">Die Standardvorlagen für die Website für Microsoft WebMatrix (**Bäckerei**, **Fotogalerie**, und **Starter Site**usw.) in c# und Visual Basic-Versionen verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="fc36a-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="fc36a-119">Sie können die Visual Basic-Vorlagen von als NuGet-Pakete installieren.</span><span class="sxs-lookup"><span data-stu-id="fc36a-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="fc36a-120">Websitevorlagen sind im Stammordner Ihrer Website in einen Ordner namens installiert *Microsoft Templates*.</span><span class="sxs-lookup"><span data-stu-id="fc36a-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="fc36a-121">Die besten Tipps für 8 Programmierung</span><span class="sxs-lookup"><span data-stu-id="fc36a-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="fc36a-122">Dieser Abschnitt enthält einige Tipps, die Sie unbedingt benötigen wissen, wie Sie mithilfe der Razor-Syntax ASP.NET-Servercode: schreibe.</span><span class="sxs-lookup"><span data-stu-id="fc36a-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="fc36a-123">1. Sie fügen Code hinzu, um eine Seite mit dem @-Zeichen</span><span class="sxs-lookup"><span data-stu-id="fc36a-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="fc36a-124">Die `@` Inlineausdrücke, einzelnen Anweisung ausgeführt und mit mehreren Anweisungen Blöcke beginnt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="fc36a-125">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="fc36a-127">**HTML-Codierung**</span><span class="sxs-lookup"><span data-stu-id="fc36a-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="fc36a-128">Wenn Sie Inhalt anzeigen, auf eine Seite mit den `@` Zeichen, wie in den obigen Beispielen ASP.NET HTML-Codierung der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="fc36a-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="fc36a-129">Dies ersetzt die reservierte HTML-Zeichen (z. B. `<` und `>` und `&`) mit Codes, mit denen die Zeichen als Zeichen statt als HTML-Tags oder Entitäten interpretiert wird auf einer Webseite angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="fc36a-130">Ohne HTML-Codierung, die aus Ihrem Code möglicherweise nicht richtig angezeigt, und möglicherweise eine Seite, um Sicherheitsrisiken ausgesetzt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="fc36a-131">Wenn Ihr Ziel ist, um HTML-Markup auszugeben, die Tags als Markup rendert (z. B. `<p></p>` für einen Absatz oder `<em></em>` Text hervorgehoben), finden Sie im Abschnitt [Kombinieren von Text, Markup und Code in Codeblöcken](#BM_CombiningTextMarkupAndCode) weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="fc36a-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="fc36a-132">Erfahren Sie mehr über die HTML-Codierung [arbeiten mit HTML-Formularen in ASP.NET Web Pages-Websites](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="fc36a-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="fc36a-133">2. Schließen Sie Codeblöcke mit Code... End-Code</span><span class="sxs-lookup"><span data-stu-id="fc36a-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="fc36a-134">Ein Codeblock enthält eine oder mehrere codeanweisungen und wird mit den Schlüsselwörtern eingeschlossen `Code` und `End Code`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="fc36a-135">Platzieren Sie das öffnende `Code` Schlüsselwort unmittelbar nach der `@` Zeichen &#8212; dazwischen können keine Leerzeichen vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="fc36a-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="fc36a-136">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="fc36a-138">3. In einem Block am Ende jeder Anweisung mit einem Zeilenumbruch</span><span class="sxs-lookup"><span data-stu-id="fc36a-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="fc36a-139">In einem Visual Basic-Codeblock endet jeder Anweisung ein Zeilenumbruch eingefügt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="fc36a-140">(Später in diesem Artikel wird eine Möglichkeit, eine lange codeanweisung in mehrere Zeilen umbrochen werden soll, falls erforderlich angezeigt.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="fc36a-141">4. Sie verwenden Variablen zum Speichern von Werten</span><span class="sxs-lookup"><span data-stu-id="fc36a-141">4. You use variables to store values</span></span>

<span data-ttu-id="fc36a-142">Sie können Werte in speichern eine *Variable*, einschließlich Zeichenfolgen, Zahlen und Datumsangaben. Sie erstellen eine neue Variable mit dem `Dim` Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="fc36a-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="fc36a-143">Sie können Werte direkt in eine Seite mit einfügen `@`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="fc36a-144">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="fc36a-146">5. Sie einschließen literale Zeichenfolgenwerte in Anführungszeichen</span><span class="sxs-lookup"><span data-stu-id="fc36a-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="fc36a-147">Ein *Zeichenfolge* ist eine Folge von Zeichen, die als Text behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="fc36a-148">Um eine Zeichenfolge angeben, schließen Sie ihn in doppelte Anführungszeichen ein:</span><span class="sxs-lookup"><span data-stu-id="fc36a-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="fc36a-149">Fügen Sie zum Einbetten von doppelten Anführungszeichen in einen Zeichenfolgenwert, zwei doppelte Anführungszeichen ein.</span><span class="sxs-lookup"><span data-stu-id="fc36a-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="fc36a-150">Das doppelte Anführungszeichen in die Seitenausgabe einmal enthalten sein sollen, geben Sie ihn als `""` innerhalb der Anführungszeichen-Zeichenfolge ein, und wenn es zweimal angezeigt werden soll, geben Sie ihn als `""""` innerhalb der Zeichenfolge in Anführungszeichen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="fc36a-151">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="fc36a-153">6. Visual Basic-Code ist nicht in der Groß-/Kleinschreibung beachten</span><span class="sxs-lookup"><span data-stu-id="fc36a-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="fc36a-154">Visual Basic-Sprache ist nicht in der Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="fc36a-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="fc36a-155">Programmierung Schlüsselwörter (z. B. `Dim`, `If`, und `True`) und Variablennamen (wie `myString`, oder `subTotal`) in jedem Fall geschrieben werden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="fc36a-156">Die folgenden Codezeilen die Variable einen Wert zuweisen `lastname` mit Kleinbuchstaben benennen, und dann den Wert den Variablen auf der Seite mit einem Großbuchstaben Namen ausgeben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="fc36a-157">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="fc36a-159">7. Großteil Ihrer Programmierung umfasst das Arbeiten mit Objekten</span><span class="sxs-lookup"><span data-stu-id="fc36a-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="fc36a-160">Ein Objekt darstellt, eine Sache, die Sie programmieren können, mit &#8212; eine Seite, ein Textfeld, eine Datei, ein Bild, eine webanforderung, eine e-Mail-Nachricht, einen Kundendatensatz (Datenbankzeile) usw. Objekte verfügen über Eigenschaften, die ihren Merkmalen beschreiben &#8212; ein Textfeld-Objekt verfügt über eine `Text` -Eigenschaft, ein Anforderungsobjekt verfügt über eine `Url` -Eigenschaft, die eine e-Mail-Nachricht verfügt über eine `From` -Eigenschaft, und ein Kundenobjekt verfügt über eine `FirstName` Diese Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fc36a-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="fc36a-161">Objekte verfügen außerdem über Methoden, die die &quot;Verben&quot; ausführen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="fc36a-162">Beispiele hierfür sind ein Dateiobjekt `Save` -Methode, ein Bildobjekt `Rotate` -Methode und eine e-Mail-Adresse des Objekts `Send` Methode.</span><span class="sxs-lookup"><span data-stu-id="fc36a-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="fc36a-163">Sie arbeiten häufig mit der `Request` -Objekt, das Sie Informationen wie die Werte des Formulars erhalten Felder auf der Seite (Textfelder usw.), welche Art von Browser die Anforderung, die URL der Seite, die Identität des Benutzers usw. vorgenommen. Dieses Beispiel veranschaulicht den Zugriff auf Eigenschaften von den `Request` -Objekt und das Aufrufen von der `MapPath` -Methode der der `Request` -Objekt, das Sie den absoluten Pfad der Seite auf dem Server erhalten:</span><span class="sxs-lookup"><span data-stu-id="fc36a-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="fc36a-164">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="fc36a-166">8. Sie können Code schreiben, die Entscheidungen trifft</span><span class="sxs-lookup"><span data-stu-id="fc36a-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="fc36a-167">Ein wichtiges Feature von dynamischen Webseiten ist, dass auf Sie bestimmen können, was zu tun ist basierend auf Bedingungen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="fc36a-168">Die gängigste Methode dazu ist die `If` Anweisung (und optional `Else` Anweisung).</span><span class="sxs-lookup"><span data-stu-id="fc36a-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="fc36a-169">Die Anweisung `If IsPost` ist eine schnelle Möglichkeit der Verfassung `If IsPost = True`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="fc36a-170">Zusammen mit `If` Anweisungen, es gibt eine Vielzahl von Möglichkeiten zum Testen von Bedingungen, wiederholen Sie Codeblöcke und usw., die sind weiter unten in diesem Artikel beschrieben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="fc36a-171">Das Ergebnis in einem Browser angezeigt (nach dem Klicken auf **senden**):</span><span class="sxs-lookup"><span data-stu-id="fc36a-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="fc36a-173">**HTTP GET und POST-Methoden und die IsPost-Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="fc36a-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="fc36a-174">Das Protokoll für Webseiten (HTTP) unterstützt eine sehr begrenzte Anzahl von Methoden (&quot;Verben&quot;), mit denen die Anforderungen an den Server zu senden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="fc36a-175">Die zwei häufigsten Gründe sind GET, die zum Lesen einer Seite verwendet wird, und POST, das verwendet wird, um eine Seite zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="fc36a-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="fc36a-176">Zum ersten Mal, das ein Benutzer eine Seite anfordert, wird im Allgemeinen unter Verwendung von GET eine Seite angefordert.</span><span class="sxs-lookup"><span data-stu-id="fc36a-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="fc36a-177">Wenn der Benutzer in einem Formular ausgefüllt, und klickt dann auf **senden**, sendet der Browser eine POST-Anforderung an dem Server.</span><span class="sxs-lookup"><span data-stu-id="fc36a-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="fc36a-178">In Web-Programmierung ist es oft hilfreich zu wissen, ob eine Seite als GET oder POST angefordert wird, damit Sie wissen, wie auf die Seite zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="fc36a-179">In ASP.NET Web Pages, können Sie die `IsPost` Eigenschaft, um festzustellen, ob eine Anforderung eine Get- oder POST ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="fc36a-180">Wenn die Anforderung eine POST-ist der `IsPost` Eigenschaft "true" zurück, und Sie können Aktionen wie lesen die Werte von Textfeldern in einem Formular.</span><span class="sxs-lookup"><span data-stu-id="fc36a-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="fc36a-181">Viele Beispiele, die Sie sehen, in dem Sie zeigen, wie zum Verarbeiten der Seite hängt der Wert des `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="fc36a-182">Ein einfaches Codebeispiel</span><span class="sxs-lookup"><span data-stu-id="fc36a-182">A Simple Code Example</span></span>

<span data-ttu-id="fc36a-183">Dieses Verfahren zeigt, wie Sie eine Seite erstellen, die die grundlegenden Programmiertechniken veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="fc36a-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="fc36a-184">Im Beispiel erstellen Sie eine Seite, mit dem Benutzer, die zwei Zahlen eingeben, dann fügt sie hinzu, und das Ergebnis wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="fc36a-185">Klicken Sie in Ihrem Editor, erstellen Sie eine neue Datei, und nennen sie *AddNumbers.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="fc36a-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="fc36a-186">Kopieren Sie den folgenden Code und Markup auf der Seite, und Ersetzen Sie dabei alle Elemente bereits in der Seite an.</span><span class="sxs-lookup"><span data-stu-id="fc36a-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="fc36a-187">Es gibt einige Dinge beachten Sie:</span><span class="sxs-lookup"><span data-stu-id="fc36a-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="fc36a-188">Die `@` Zeichen beginnt des erste Codeblocks auf der Seite, und ihm vorausgeht der `totalMessage` Variable im unteren Bereich eingebettet.</span><span class="sxs-lookup"><span data-stu-id="fc36a-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="fc36a-189">Der Block am oberen Rand der Seite "steht in `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="fc36a-190">Die Variablen `total`, `num1`, `num2`, und `totalMessage` mehrere Zahlen und einer Zeichenfolge zu speichern.</span><span class="sxs-lookup"><span data-stu-id="fc36a-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="fc36a-191">Der Zeichenfolgenliteral-Wert, der zugewiesen der `totalMessage` Variable ist in doppelte Anführungszeichen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="fc36a-192">Da Visual Basic-Code nicht wenn Groß-/Kleinschreibung beachtet, ist die `totalMessage` Variable, die am unteren Rand der Seite verwendet wird, muss der Name nur die Schreibweise der Variablendeklaration am oberen Rand der Seite übereinstimmen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="fc36a-193">Die Groß-/Kleinschreibung spielt keine Rolle.</span><span class="sxs-lookup"><span data-stu-id="fc36a-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="fc36a-194">Der Ausdruck `num1.AsInt()`  +  `num2.AsInt()` für die Arbeit mit Objekten und Methoden veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="fc36a-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="fc36a-195">Die `AsInt` Methode für jede Variable konvertiert die Zeichenfolge, die von einem Benutzer eingegeben wird, auf eine ganze Zahl (Integer), die hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="fc36a-196">Die `<form>` Tag enthält eine `method="post"` Attribut.</span><span class="sxs-lookup"><span data-stu-id="fc36a-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="fc36a-197">Dies gibt an, dass wenn der Benutzer klickt **hinzufügen**, die Seite an den Server mithilfe der HTTP-POST-Methode gesendet.</span><span class="sxs-lookup"><span data-stu-id="fc36a-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="fc36a-198">Wenn die Seite gesendet wird, den Code `If IsPost` ergibt "true" und der bedingte code ausgeführt wird, und das Ergebnis der Addition der Zahlen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="fc36a-199">Speichern Sie die Seite, und führen Sie sie in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="fc36a-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="fc36a-200">(Stellen Sie sicher, dass die Seite ist ausgewählt, der **Dateien** Arbeitsbereich vor der Ausführung.) Geben Sie zwei ganzen Zahlen, und klicken Sie dann auf die **hinzufügen** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="fc36a-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="fc36a-202">Visual Basic-Sprache und Syntax</span><span class="sxs-lookup"><span data-stu-id="fc36a-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="fc36a-203">Zuvor haben Sie ein einfaches Beispiel einer ASP.NET-Webseite zu erstellen, und wie Sie HTML-Markup Servercode hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="fc36a-204">Hier erfahren Sie die Grundlagen der Verwendung von Visual Basic zum Schreiben von ASP.NET-Code-Server mithilfe der Razor-Syntax &#8212; , also die programming Language-Regeln.</span><span class="sxs-lookup"><span data-stu-id="fc36a-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="fc36a-205">Wenn Sie bereits über Erfahrung mit Programmierung (insbesondere, wenn Sie C#, C++, c#, Visual Basic oder JavaScript verwendet haben), werden viele der hier Sie lesen vertraut sein.</span><span class="sxs-lookup"><span data-stu-id="fc36a-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="fc36a-206">Sie müssen wahrscheinlich machen Sie sich nur mit Markup wie WebMatrix-Code hinzugefügt wird *vbhtml* Dateien.</span><span class="sxs-lookup"><span data-stu-id="fc36a-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="fc36a-207">Kombinieren von Text, Markup und Code in Codeblöcken</span><span class="sxs-lookup"><span data-stu-id="fc36a-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="fc36a-208">In Server-Codeblöcken sollten Sie häufig zur Ausgabe von Text und Markup auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="fc36a-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="fc36a-209">Wenn ein Server-Codeblock Text enthält, die nicht Code und, stattdessen gerendert werden soll, wie, muss ASP.NET Text von Code zu unterscheiden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="fc36a-210">Dafür stehen verschiedene Möglichkeiten zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="fc36a-210">There are several ways to do this.</span></span>

- <span data-ttu-id="fc36a-211">Schließen Sie den Text in einem HTML-Block-Element wie `<p></p>` oder `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="fc36a-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="fc36a-212">Das HTML-Element kann Text, zusätzliche HTML-Elemente und Servercode Ausdrücke enthalten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="fc36a-213">Wenn erkennt ASP.NET das öffnende HTML-Tag (z. B. `<p>`), rendert alles, was das Element und dessen Inhalt als für den Browser (und löst die Servercode Ausdrücke) ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="fc36a-214">Verwenden der `@:` Operator oder die `<text>` Element.</span><span class="sxs-lookup"><span data-stu-id="fc36a-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="fc36a-215">Die `@:` Ausgaben eine einzelne Zeile des Inhalts, der nur-Text oder HTML-Tags für nicht übereinstimmenden; enthält die `<text>` Element einschließt, mehrere Zeilen ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="fc36a-216">Diese Optionen sind nützlich, wenn Sie nicht, ein HTML-Element als Teil der Ausgabe gerendert möchten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="fc36a-217">Im folgenden Beispiel wird das vorherige Beispiel wiederholt, aber verwendet ein einzelnes Paar von `<text>` Tags aus, um den Text Rendern einschließen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="fc36a-218">Im folgenden Beispiel die `<text>` und `</text>` Tags einschließen drei Zeilen, die jeweils einige nicht enthaltene Text und HTML-Tags, die nicht übereinstimmenden sind (`<br />`), sowie der Servercode und HTML-Tags, die übereinstimmende.</span><span class="sxs-lookup"><span data-stu-id="fc36a-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="fc36a-219">In diesem Fall können Sie auch jede Zeile einzeln mit voranstellen der `@:` Operator; beide Weise funktionieren.</span><span class="sxs-lookup"><span data-stu-id="fc36a-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="fc36a-220">Wenn Sie Text ausgeben, wie in diesem Abschnitt gezeigt &#8212; mithilfe eines HTML-Elements, die `@:` -Operator, oder die `<text>` Element &#8212; ASP.NET die Ausgabe nicht HTML-Codierung.</span><span class="sxs-lookup"><span data-stu-id="fc36a-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="fc36a-221">(Wie bereits erwähnt, ASP.NET codiert die Ausgabe von Codeausdrücken Server und Server-Codeblöcke, die vor `@`, außer in die Sonderfälle, in diesem Abschnitt erwähnt wurden.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="fc36a-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="fc36a-222">Whitespace</span></span>

<span data-ttu-id="fc36a-223">Zusätzliche Leerzeichen in einer Anweisung (und außerhalb eines Zeichenfolgenliterals) wirken sich nicht auf die Anweisung aus:</span><span class="sxs-lookup"><span data-stu-id="fc36a-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="fc36a-224">Lange Anweisungen Aufteilen in mehrere Zeilen</span><span class="sxs-lookup"><span data-stu-id="fc36a-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="fc36a-225">Sie können eine lange codeanweisung in mehrere Zeilen aufteilen, indem Sie mit dem Unterstrich `_` (die in Visual Basic den Namen der *Fortsetzungszeichen*) nach jeder Zeile des Codes.</span><span class="sxs-lookup"><span data-stu-id="fc36a-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="fc36a-226">Um eine Anweisung auf die nächste Zeile unterbrechen, am Ende der Zeile fügen Sie ein Leerzeichen, und klicken Sie dann das Fortsetzungszeichen hinzu.</span><span class="sxs-lookup"><span data-stu-id="fc36a-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="fc36a-227">Die Anweisung in der nächsten Zeile fortgesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-227">Continue the statement on the next line.</span></span> <span data-ttu-id="fc36a-228">Sie können die Anweisungen auf so viele Zeilen, wie Sie benötigen, um die Lesbarkeit zu verbessern umschließen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="fc36a-229">Die folgenden Anweisungen sind identisch:</span><span class="sxs-lookup"><span data-stu-id="fc36a-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="fc36a-230">Sie können keine jedoch eine Zeile in der Mitte eines Zeichenfolgenliterals umschließen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="fc36a-231">Das folgende Beispiel funktioniert nicht:</span><span class="sxs-lookup"><span data-stu-id="fc36a-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="fc36a-232">Um eine lange Zeichenfolge zu kombinieren, die in mehrere Zeilen wie im obigen Code umschließt, müssten Sie verwenden die *Verkettungsoperator* (`&`), die Sie später in diesem Artikel sehen werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="fc36a-233">Codekommentare</span><span class="sxs-lookup"><span data-stu-id="fc36a-233">Code comments</span></span>

<span data-ttu-id="fc36a-234">Kommentare können Sie Notizen für sich selbst oder andere zu verlassen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="fc36a-235">Razor-Syntax Kommentare vorangestellt `@*` und enden mit `*@`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="fc36a-236">Innerhalb der Codeblöcke können Sie die Kommentare der Razor-Syntax verwenden, oder Sie können normale Visual Basic-Kommentarzeichen, wird ein einfaches Anführungszeichen (`'`) mit dem Präfix für jede Zeile.</span><span class="sxs-lookup"><span data-stu-id="fc36a-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="fc36a-237">Variablen</span><span class="sxs-lookup"><span data-stu-id="fc36a-237">Variables</span></span>

<span data-ttu-id="fc36a-238">Eine Variable ist ein benanntes Objekt, das Sie verwenden, um Daten zu speichern.</span><span class="sxs-lookup"><span data-stu-id="fc36a-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="fc36a-239">Sie können Variablen Namen, aber der Name muss mit einem alphabetischen Zeichen beginnen, und es darf keine Leerzeichen oder reservierte Zeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="fc36a-240">Wie Sie zuvor gesehen haben, ist die Groß-/Kleinschreibung der Buchstaben im Namen einer Variablen in Visual Basic unerheblich.</span><span class="sxs-lookup"><span data-stu-id="fc36a-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="fc36a-241">Variablen und Datentypen</span><span class="sxs-lookup"><span data-stu-id="fc36a-241">Variables and data types</span></span>

<span data-ttu-id="fc36a-242">Eine Variable haben einen bestimmten Datentyp, der angibt, welche Art von Daten in der Variablen gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="fc36a-243">Können Sie Zeichenfolgenvariablen, in denen Zeichenfolgenwerte gespeichert haben (z. B. &quot;Hallo Welt&quot;), Ganzzahl-Variablen, die ganzzahlige Werte (z. B. 3 oder 79) speichern, und die Datenvariablen, die Datumswerte in einer Vielzahl von Formaten (z. B. 4/12/2012 oder März 2009 speichern ).</span><span class="sxs-lookup"><span data-stu-id="fc36a-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="fc36a-244">Und es gibt viele andere Datentypen, die Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="fc36a-245">Allerdings müssen Sie einen Typ für eine Variable angeben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="fc36a-246">In den meisten Fällen kann ASP.NET ermitteln den Typ basierend auf wie die Daten in der Variablen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="fc36a-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="fc36a-247">(Gelegentlich müssen Sie einen Typ angeben, sehen Sie Beispiele, in denen dies "true".)</span><span class="sxs-lookup"><span data-stu-id="fc36a-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="fc36a-248">Um eine Variable zu deklarieren, ohne Angabe eines Typs verwenden `Dim` sowie den Namen der Variablen (z. B. `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="fc36a-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="fc36a-249">Um eine Variable mit einem Typ zu deklarieren, verwenden `Dim` sowie den Variablennamen ein, gefolgt von `As` , und klicken Sie dann den Namen (z. B. `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="fc36a-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="fc36a-250">Das folgende Beispiel zeigt einige Inlineausdrücke, die die Variablen in einer Webseite verwenden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="fc36a-251">Das Ergebnis in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="fc36a-253">Konvertieren und Testen von Datentypen</span><span class="sxs-lookup"><span data-stu-id="fc36a-253">Converting and testing data types</span></span>

<span data-ttu-id="fc36a-254">Obwohl ASP.NET einen Datentyp in der Regel automatisch ermitteln kann, manchmal kann es nicht.</span><span class="sxs-lookup"><span data-stu-id="fc36a-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="fc36a-255">Aus diesem Grund müssen Sie ASP.NET weiterhelfen, indem Sie eine explizite Konvertierung ausführen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="fc36a-256">Auch wenn Sie keine Typen zu konvertieren, ist es manchmal hilfreich, testen, welche Art von Daten Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="fc36a-257">Der häufigste Fall ist, dass Sie zum Konvertieren von einer Zeichenfolge in einen anderen Typ, z. B. auf eine ganze Zahl oder Datum.</span><span class="sxs-lookup"><span data-stu-id="fc36a-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="fc36a-258">Das folgende Beispiel zeigt einem typischen Fall, in dem Sie eine Zeichenfolge in eine Zahl konvertieren müssen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="fc36a-259">Als Faustregel gilt wird der Benutzereingabe für Sie als Zeichenfolgen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="fc36a-260">Auch wenn Sie, den Benutzer aufgefordert haben, eine Zahl einzugeben, und auch wenn sie bei der Eingabe des Benutzers gesendet wird, und Sie finden es im Code eine Ziffer eingegeben haben, die Daten im Zeichenfolgenformat werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="fc36a-261">Aus diesem Grund müssen Sie die Zeichenfolge in eine Zahl konvertieren.</span><span class="sxs-lookup"><span data-stu-id="fc36a-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="fc36a-262">Im Beispiel wenn Sie versuchen, die Durchführung von Berechnungen auf den Werten, ohne zu konvertieren, führt der folgende Fehler, da zwei Zeichenfolgen von ASP.NET hinzugefügt werden können:</span><span class="sxs-lookup"><span data-stu-id="fc36a-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="fc36a-263">Um die Werte in ganzen Zahlen zu konvertieren, rufen Sie die `AsInt` Methode.</span><span class="sxs-lookup"><span data-stu-id="fc36a-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="fc36a-264">Wenn die Konvertierung erfolgreich ist, können Sie dann die Zahlen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="fc36a-265">Die folgende Tabelle enthält einige allgemeine Konvertierung und Test-Methoden für die Variablen an.</span><span class="sxs-lookup"><span data-stu-id="fc36a-265">The following table lists some common conversion and test methods for variables.</span></span>


:::row:::
    :::column:::
        <strong>Method</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Example</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        Converts a string that represents a whole number (like &quot;593&quot;) to an integer.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number. (In ASP.NET, a decimal number is more precise than a floating-point number.)
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        Converts a string that represents a date and time value to the ASP.NET `DateTime` type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        Converts any other data type to a string.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::


## <a name="operators"></a><span data-ttu-id="fc36a-266">Operatoren</span><span class="sxs-lookup"><span data-stu-id="fc36a-266">Operators</span></span>

<span data-ttu-id="fc36a-267">Ein Operator ist ein Schlüsselwort oder das Zeichen, das ASP.NET darüber informiert, welche Art von Befehl aus, um in einem Ausdruck durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-267">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="fc36a-268">Visual Basic unterstützt viele Operatoren, aber Sie müssen nur wenige zum Entwickeln von ASP.NET Web Pages erkennen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-268">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="fc36a-269">In der folgende Tabelle werden die am häufigsten verwendeten Operatoren zusammengefasst.</span><span class="sxs-lookup"><span data-stu-id="fc36a-269">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Examples</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        Math operators used in numerical expressions.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Assignment and equality. Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Inequality. Returns `True` if the values are not equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Less than, greater than, less than or equal, and greater than or equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Concatenation, which is used to join strings.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        The increment and decrement operators, which add and subtract 1 (respectively) from a variable.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        Dot. Used to distinguish objects and their properties and methods.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Parentheses. Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Not. Reverses a true value to false and vice versa. Typically used as a shorthand way to test for `False` (that is, for not `True`).
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Logical AND and OR, which are used to link conditions together.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="fc36a-270">Arbeiten mit Datei- und Ordnerpfade in Code</span><span class="sxs-lookup"><span data-stu-id="fc36a-270">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="fc36a-271">Sie werden häufig mit Datei- und Ordnerpfade in Ihrem Code arbeiten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-271">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="fc36a-272">Hier ist ein Beispiel der physischen Ordnerstruktur für eine Website auf, wie es auf Ihrem Entwicklungscomputer angezeigt werden kann:</span><span class="sxs-lookup"><span data-stu-id="fc36a-272">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="fc36a-273">Hier sind einige wichtigen Informationen über URLs und Pfade:</span><span class="sxs-lookup"><span data-stu-id="fc36a-273">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="fc36a-274">Eine URL beginnt entweder mit einen Domänennamen (`http://www.example.com`) oder einen Servernamen (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="fc36a-274">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="fc36a-275">Eine URL entspricht einem physischen Pfad auf einem Hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="fc36a-275">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="fc36a-276">Z. B. `http://myserver` möglicherweise zu dem Ordner entsprechen *C:\websites\mywebsite* auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="fc36a-276">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="fc36a-277">Ein virtueller Pfad ist die Abkürzung, um Pfade im Code darzustellen, ohne den vollständigen Pfad angeben zu müssen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-277">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="fc36a-278">Es umfasst den Teil einer URL, die der Domäne oder Server Name folgt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-278">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="fc36a-279">Wenn Sie die virtuellen Pfade verwenden, können Sie Ihren Code zu einer anderen Domäne oder Server verschieben, ohne die Pfade aktualisieren zu müssen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-279">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="fc36a-280">Hier ist ein Beispiel hilft Ihnen die Unterschiede zu verstehen:</span><span class="sxs-lookup"><span data-stu-id="fc36a-280">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="fc36a-281">Vollständige URL</span><span class="sxs-lookup"><span data-stu-id="fc36a-281">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="fc36a-282">Servername</span><span class="sxs-lookup"><span data-stu-id="fc36a-282">Server name</span></span> | <span data-ttu-id="fc36a-283">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="fc36a-283">*mycompanyserver*</span></span> |
| <span data-ttu-id="fc36a-284">Virtueller Pfad</span><span class="sxs-lookup"><span data-stu-id="fc36a-284">Virtual path</span></span> | <span data-ttu-id="fc36a-285">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="fc36a-285">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="fc36a-286">Physischer Pfad</span><span class="sxs-lookup"><span data-stu-id="fc36a-286">Physical path</span></span> | <span data-ttu-id="fc36a-287">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="fc36a-287">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="fc36a-288">Das virtuelle Stammverzeichnis ist /, genau wie der Stamm von Laufwerk C: Laufwerk \.</span><span class="sxs-lookup"><span data-stu-id="fc36a-288">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="fc36a-289">(Virtuelle Ordnerpfade verwenden immer Schrägstriche.) Der virtuelle Pfad eines Ordners muss nicht den gleichen Namen wie der physische Ordner haben; Es kann ein Alias sein.</span><span class="sxs-lookup"><span data-stu-id="fc36a-289">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="fc36a-290">(Auf Produktionsservern entspricht der virtuelle Pfad nur selten einen genaue physischen Pfad.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-290">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="fc36a-291">Bei der Arbeit mit Dateien und Ordner im Code, müssen Sie gelegentlich verweisen auf den physischen Pfad und manchmal auf einen virtuellen Pfad, je nachdem welche Objekte, die mit dem Sie arbeiten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-291">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="fc36a-292">ASP.NET bietet Ihnen diese Tools zum Arbeiten mit Datei- und Ordnerpfade im Code: die `Server.MapPath` -Methode, und die `~` Operator und `Href` Methode.</span><span class="sxs-lookup"><span data-stu-id="fc36a-292">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="fc36a-293">Konvertieren von virtuellen und physischen Pfade: die Server.MapPath-Methode</span><span class="sxs-lookup"><span data-stu-id="fc36a-293">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="fc36a-294">Die `Server.MapPath` Methode konvertiert einen virtuellen Pfad (z. B. */default.cshtml*), ein absoluter physischer Pfad (z. B. *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="fc36a-294">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="fc36a-295">Sie verwenden diese Methode können Sie jederzeit einen vollständigen physischen Pfad.</span><span class="sxs-lookup"><span data-stu-id="fc36a-295">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="fc36a-296">Ein typisches Beispiel ist beim Lesen oder Schreiben einer Text- oder Image-Datei auf dem Webserver.</span><span class="sxs-lookup"><span data-stu-id="fc36a-296">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="fc36a-297">Sie können die absoluten physischen Pfad der Website auf einer hosting-Site-Server in der Regel nicht kennen, damit diese Methode konvertieren des Pfads können Sie wissen – der virtuelle Pfad, in den entsprechenden Pfad auf dem Server für Sie.</span><span class="sxs-lookup"><span data-stu-id="fc36a-297">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="fc36a-298">Sie den virtuellen Pfad zu einer Datei oder Ordner für die Methode übergeben, und es gibt den physischen Pfad:</span><span class="sxs-lookup"><span data-stu-id="fc36a-298">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="fc36a-299">Verweisen auf das virtuelle Stammverzeichnis: der ~-Operator und Href-Methode</span><span class="sxs-lookup"><span data-stu-id="fc36a-299">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="fc36a-300">In einer *.cshtml* oder *vbhtml* -Datei können Sie verweisen, den virtuellen Stamm-Pfad mit der `~` Operator.</span><span class="sxs-lookup"><span data-stu-id="fc36a-300">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="fc36a-301">Dies ist sehr praktisch, da Sie Seiten, an einem Standort navigieren können, und alle Links zu anderen Seiten enthaltenen nicht unterbrochen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-301">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="fc36a-302">Es ist auch praktisch, für den Fall, dass Sie Ihre Website immer an einem anderen Speicherort verschieben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-302">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="fc36a-303">Hier einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="fc36a-303">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="fc36a-304">Wenn die Website ist `http://myserver/myapp`, sieht wie ASP.NET diese Pfade behandelt wird, wenn die Seite ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="fc36a-304">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="fc36a-305">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="fc36a-305">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="fc36a-306">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="fc36a-306">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="fc36a-307">(Diese Pfade nicht tatsächlich als die Werte der Variablen angezeigt, aber ASP.NET die Pfade behandelt, als ob einstellungsänderungen ist.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-307">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="fc36a-308">Sie können die `~` Operator sowohl im Server-Code (wie oben erläutert) und im Markup wie folgt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-308">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="fc36a-309">Im Markup, das Sie verwenden die `~` Operator, um Pfade zu den Ressourcen, wie Bilddateien, andere Webseiten und CSS-Dateien zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-309">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="fc36a-310">Wenn die Seite ausgeführt wird, durchsucht Sie die Seite (Code und Markup) und behebt alle ASP.NET die `~` Verweise auf den entsprechenden Pfad.</span><span class="sxs-lookup"><span data-stu-id="fc36a-310">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="fc36a-311">Bedingungen und Schleifen</span><span class="sxs-lookup"><span data-stu-id="fc36a-311">Conditional Logic and Loops</span></span>

<span data-ttu-id="fc36a-312">ASP.NET Server-Code können Sie die Aufgaben, die basierend auf Bedingungen und Schreiben Sie Code, die Anweisungen wiederholen, die also eine bestimmte Anzahl von Malen zu code, der eine Schleife ausgeführt wird).</span><span class="sxs-lookup"><span data-stu-id="fc36a-312">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="fc36a-313">Testen von Bedingungen</span><span class="sxs-lookup"><span data-stu-id="fc36a-313">Testing conditions</span></span>

<span data-ttu-id="fc36a-314">Um eine einfache Bedingung zu testen, Sie verwenden, die `If...Then` -Anweisung, die gibt `True` oder `False` basierend auf einen Test, die Sie angeben:</span><span class="sxs-lookup"><span data-stu-id="fc36a-314">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="fc36a-315">Die `If` Schlüsselwort beginnt einen Block.</span><span class="sxs-lookup"><span data-stu-id="fc36a-315">The `If` keyword starts a block.</span></span> <span data-ttu-id="fc36a-316">Der eigentliche Test (Bedingung) folgt die `If` -Schlüsselwort und gibt "true" oder "false".</span><span class="sxs-lookup"><span data-stu-id="fc36a-316">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="fc36a-317">Die `If` Anweisung endet mit `Then`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-317">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="fc36a-318">Die Anweisungen, die ausgeführt werden, wenn der Test "true" ist eingeschlossen sind `If` und `End If`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-318">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="fc36a-319">Ein `If` -Anweisung kann enthalten eine `Else` Block, der angibt, Anweisungen, die ausgeführt werden, wenn die Bedingung "false" ist:</span><span class="sxs-lookup"><span data-stu-id="fc36a-319">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="fc36a-320">Wenn ein `If` Anweisung beginnt einen Codeblock, müssen Sie nicht mit der normalen `Code...End Code` Anweisungen, um die Blöcke einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-320">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="fc36a-321">Sie können einfach hinzufügen `@` an den Block, und es funktioniert.</span><span class="sxs-lookup"><span data-stu-id="fc36a-321">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="fc36a-322">Dieser Ansatz funktioniert für `If` sowie andere Visual Basic-Schlüsselwörter, die von Codeblöcken, einschließlich eingehalten werden Programmierung `For`, `For Each`, `Do While`usw.</span><span class="sxs-lookup"><span data-stu-id="fc36a-322">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="fc36a-323">Sie können mehrere Bedingungen, die mit einem oder mehreren hinzufügen `ElseIf` Blöcken:</span><span class="sxs-lookup"><span data-stu-id="fc36a-323">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="fc36a-324">In diesem Beispiel, wenn in der ersten Bedingung die `If` Block ist nicht "true", die `ElseIf` Bedingung aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-324">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="fc36a-325">Wenn diese Bedingung erfüllt ist, die Anweisungen in der `ElseIf` Block ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-325">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="fc36a-326">Wenn keine der Bedingungen erfüllt sind, die Anweisungen in der `Else` Block ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-326">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="fc36a-327">Sie können eine beliebige Anzahl von hinzufügen `ElseIf` blockiert, und schließen Sie dann mit einer `Else` als blockiert die &quot;alles&quot; Bedingung.</span><span class="sxs-lookup"><span data-stu-id="fc36a-327">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="fc36a-328">Um eine große Anzahl von Bedingungen zu testen, verwenden Sie eine `Select Case` blockieren:</span><span class="sxs-lookup"><span data-stu-id="fc36a-328">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="fc36a-329">Der zu testende Wert wird in Klammern angegeben (in dem Beispiel wird die Variable Wochentag).</span><span class="sxs-lookup"><span data-stu-id="fc36a-329">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="fc36a-330">Jeder einzelne Test verwendet einen `Case` -Anweisung, die einen Wert enthält.</span><span class="sxs-lookup"><span data-stu-id="fc36a-330">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="fc36a-331">Wenn der Wert des einem `Case` Anweisung entspricht dem Testwert, der Code in diesem `Case` Block wird ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-331">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="fc36a-332">Das Ergebnis der letzten beiden bedingte Blöcke in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-332">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="fc36a-334">Schleifen-code</span><span class="sxs-lookup"><span data-stu-id="fc36a-334">Looping code</span></span>

<span data-ttu-id="fc36a-335">Sie müssen häufig die gleichen Anweisungen mehrmals ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-335">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="fc36a-336">Dazu müssen Sie Schleifen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-336">You do this by looping.</span></span> <span data-ttu-id="fc36a-337">Beispielsweise führen Sie häufig die gleichen Anweisungen für jedes Element in einer Auflistung von Daten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-337">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="fc36a-338">Wenn Sie wissen, wie oft Sie möchten eine Schleife, können Sie eine `For` Schleife.</span><span class="sxs-lookup"><span data-stu-id="fc36a-338">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="fc36a-339">Diese Art von Schleife eignet sich besonders für zugewiesen, oder nach unten zählen:</span><span class="sxs-lookup"><span data-stu-id="fc36a-339">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="fc36a-340">Die Schleife beginnt mit der `For` Schlüsselwort, gefolgt von drei Elementen:</span><span class="sxs-lookup"><span data-stu-id="fc36a-340">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="fc36a-341">Unmittelbar nach der `For` -Anweisung, Sie deklarieren eine Zählervariable (müssen Sie nicht mit `Dim`), und klicken Sie dann den Bereich angeben, wie in `i = 10 to 20`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-341">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="fc36a-342">Dies bedeutet, dass die Variable `i` beginnen bei 10 zu zählen und weiterhin bis 20 (einschließlich) erreicht wird.</span><span class="sxs-lookup"><span data-stu-id="fc36a-342">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="fc36a-343">Zwischen der `For` und `Next` Anweisungen ist der Inhalt des Blocks.</span><span class="sxs-lookup"><span data-stu-id="fc36a-343">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="fc36a-344">Dies kann eine oder mehrere Code-Anweisungen, die ausgeführt werden mit der foreach-Schleife enthalten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-344">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="fc36a-345">Die `Next i` Anweisung wird die Schleife beendet.</span><span class="sxs-lookup"><span data-stu-id="fc36a-345">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="fc36a-346">Es erhöht den Zähler und die nächste Iteration der Schleife beginnt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-346">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="fc36a-347">Die Zeile des Codes zwischen der `For` und `Next` Zeilen enthält den Code, der für jede Iteration der Schleife ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fc36a-347">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="fc36a-348">Das Markup erstellt einen neuen Absatz (`<p>` Element) jedes Mal, und fügt eine Zeile in die Ausgabe, sodass der Wert i (den Zähler).</span><span class="sxs-lookup"><span data-stu-id="fc36a-348">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="fc36a-349">Wenn Sie diese Seite ausführen, wird im Beispiel 11 Zeilen anzeigen der Ausgabe, mit dem Text in jeder Zeile an, der angibt, der Elementnummer erstellt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-349">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="fc36a-351">Wenn Sie mit einer Auflistung oder ein Array arbeiten, verwenden Sie häufig eine `For Each` Schleife.</span><span class="sxs-lookup"><span data-stu-id="fc36a-351">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="fc36a-352">Eine Auflistung ist eine Gruppe ähnlicher Objekte und die `For Each` Schleife können Sie eine Aufgabe für jedes Element in der Auflistung durchführen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-352">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="fc36a-353">Dieser Art von Schleife eignet sich für Auflistungen, da im Gegensatz zu einem `For` Schleife, Sie müssen keine Erhöhen des Zählerwerts oder ein Limit festlegen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-353">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="fc36a-354">Stattdessen die `For Each` Schleifen-Code wird einfach in der Auflistung fortgesetzt, bis er abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-354">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="fc36a-355">In diesem Beispiel gibt die Elemente in der `Request.ServerVariables` Sammlung (mit Informationen über den Webserver).</span><span class="sxs-lookup"><span data-stu-id="fc36a-355">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="fc36a-356">Er verwendet eine `For Each` Schleife, um den Namen der einzelnen Elemente anzeigen, indem Sie beim Erstellen eines neuen `<li>` Element in einer HTML-Aufzählung.</span><span class="sxs-lookup"><span data-stu-id="fc36a-356">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="fc36a-357">Die `For Each` Schlüsselwort folgt durch eine Variable, die ein einzelnes Element in der Auflistung darstellt (beispielsweise `myItem`), gefolgt von der `In` Schlüsselwort, gefolgt von der Auflistung durchlaufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-357">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="fc36a-358">Im Hauptteil der `For Each` Schleife können Sie das aktuelle Element, das mit der Variablen, die Sie zuvor deklarierten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-358">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="fc36a-360">Verwenden Sie zum Erstellen einer allgemeinen Schleife die `Do While` Anweisung:</span><span class="sxs-lookup"><span data-stu-id="fc36a-360">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="fc36a-361">Diese Schleife beginnt mit der `Do While` Schlüsselwort, gefolgt von einer Bedingung, gefolgt vom Block wiederholt werden soll.</span><span class="sxs-lookup"><span data-stu-id="fc36a-361">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="fc36a-362">Schleifen in der Regel erhöhen (hinzugefügt) oder zu verringern (subtrahiert) eine Variable oder ein Objekt, das für die Inventur verwendet.</span><span class="sxs-lookup"><span data-stu-id="fc36a-362">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="fc36a-363">Im Beispiel die `+=` Operator fügt 1 auf den Wert einer Variable jedes Mal die Schleife ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fc36a-363">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="fc36a-364">(Um eine Variable in einer Schleife zu verringern, die wird nach unten gezählt, verwenden Sie des Dekrementoperators `-=`.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-364">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="fc36a-365">Objekte und Auflistungen</span><span class="sxs-lookup"><span data-stu-id="fc36a-365">Objects and Collections</span></span>

<span data-ttu-id="fc36a-366">Fast alles in einer ASP.NET-Website ist ein Objekt, einschließlich der Webseite selbst.</span><span class="sxs-lookup"><span data-stu-id="fc36a-366">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="fc36a-367">Dieser Abschnitt beschreibt einige wichtige Objekte, die Sie häufig in Ihrem Code verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="fc36a-367">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="fc36a-368">Page-Objekte</span><span class="sxs-lookup"><span data-stu-id="fc36a-368">Page objects</span></span>

<span data-ttu-id="fc36a-369">Die meisten grundlegenden Objekts in ASP.NET ist die Seite.</span><span class="sxs-lookup"><span data-stu-id="fc36a-369">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="fc36a-370">Sie können die Eigenschaften der Page-Objekt, ohne alle berechtigten Objekte direkt zugreifen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-370">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="fc36a-371">Der folgende Code Ruft den Dateipfad der Seite mit den `Request` Objekt der Seite:</span><span class="sxs-lookup"><span data-stu-id="fc36a-371">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="fc36a-372">Können Sie Eigenschaften der `Page` Objekt um eine Vielzahl von Informationen, wie z. B. zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="fc36a-372">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="fc36a-373">`Request`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-373">`Request`.</span></span> <span data-ttu-id="fc36a-374">Wie Sie bereits gesehen haben, ist dies eine Auflistung von Informationen über die aktuelle Anforderung, einschließlich welche Art von Browser die Anforderung, die URL der Seite, die Identität des Benutzers usw. vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-374">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="fc36a-375">`Response`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-375">`Response`.</span></span> <span data-ttu-id="fc36a-376">Dies ist eine Auflistung von Informationen über die Antwort (Seite), die an den Browser gesendet wird, wenn der Code ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="fc36a-376">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="fc36a-377">Beispielsweise können Sie diese Eigenschaft, um Informationen in die Antwort zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-377">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="fc36a-378">Von Auflistungsobjekten (Arrays und Dictionarys)</span><span class="sxs-lookup"><span data-stu-id="fc36a-378">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="fc36a-379">Eine Auflistung ist eine Gruppe von Objekten desselben Typs, z. B. eine Auflistung von `Customer` Objekte aus einer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="fc36a-379">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="fc36a-380">ASP.NET enthält viele integrierte Auflistungen, z.B. die `Request.Files` Auflistung.</span><span class="sxs-lookup"><span data-stu-id="fc36a-380">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="fc36a-381">Sie werden häufig in Sammlungen mit Daten arbeiten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-381">You'll often work with data in collections.</span></span> <span data-ttu-id="fc36a-382">Zwei allgemeine Auflistungstypen sind die *Array* und *Wörterbuch*.</span><span class="sxs-lookup"><span data-stu-id="fc36a-382">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="fc36a-383">Ein Array ist nützlich, wenn Sie eine Sammlung mit ähnlichen Elementen gespeichert werden soll, aber nicht, erstellen Sie eine separate Variable für jedes Element möchten:</span><span class="sxs-lookup"><span data-stu-id="fc36a-383">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="fc36a-384">Mit Arrays, Sie deklarieren einen bestimmten Datentyp, z. B. `String`, `Integer`, oder `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-384">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="fc36a-385">Um anzugeben, dass die Variable darf ein Array, das Sie Klammern hinzufügen, um den Variablennamen in der Deklaration (z. B. `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="fc36a-385">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="fc36a-386">Es stehen die Elemente in einem Array mit ihrer Position (Index) oder mithilfe der `For Each` Anweisung.</span><span class="sxs-lookup"><span data-stu-id="fc36a-386">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="fc36a-387">Arrayindizes sind nullbasiert &#8212; , also das erste Element ist an position 0, das zweite Element ist an Position 1 und So weiter.</span><span class="sxs-lookup"><span data-stu-id="fc36a-387">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="fc36a-388">Sie können die Anzahl der Elemente in einem Array zu bestimmen, durch Abrufen der `Length` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fc36a-388">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="fc36a-389">Die Position eines bestimmten Elements im Array abzurufen (d. h. das Array zu suchen), verwenden die `Array.IndexOf` Methode.</span><span class="sxs-lookup"><span data-stu-id="fc36a-389">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="fc36a-390">Sie können auch Aktionen wie Reverse den Inhalt eines Arrays (die `Array.Reverse` Methode) oder den Inhalt zu sortieren (die `Array.Sort` Methode).</span><span class="sxs-lookup"><span data-stu-id="fc36a-390">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="fc36a-391">Die Ausgabe von der Zeichenfolgen-Array-Code in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fc36a-391">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="fc36a-393">Ein Wörterbuch ist eine Auflistung von Schlüssel/Wert-Paare, in dem Sie den Schlüssel (oder Name) festlegen oder Abrufen des entsprechenden Werts angeben:</span><span class="sxs-lookup"><span data-stu-id="fc36a-393">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="fc36a-394">Um ein Wörterbuch zu erstellen, verwenden Sie die `New` Schlüsselwort, um anzugeben, dass Sie ein neues erstellen `Dictionary` Objekt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-394">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="fc36a-395">Sie können ein Wörterbuch zuweisen, um eine Variable mit dem `Dim` Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="fc36a-395">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="fc36a-396">Sie zeigen die Daten der Elemente in das Wörterbuch, das die Verwendung von Klammern ( `( )` ).</span><span class="sxs-lookup"><span data-stu-id="fc36a-396">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="fc36a-397">Am Ende der Deklaration müssen Sie ein weiteres Paar Klammern hinzufügen, da es sich eigentlich eine Methode handelt, die ein neues Wörterbuch erstellt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-397">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="fc36a-398">Um Elemente zum Wörterbuch hinzuzufügen, rufen Sie die `Add` Methode der "Dictionary"-Variable (`myScores` in diesem Fall), und geben Sie einen Schlüssel und Wert.</span><span class="sxs-lookup"><span data-stu-id="fc36a-398">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="fc36a-399">Alternativ können Sie Klammern verwenden, um den Schlüssel angeben, und führen eine einfache Zuweisung, wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fc36a-399">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="fc36a-400">Um einen Wert aus dem Wörterbuch abzurufen, geben Sie den Schlüssel in Klammern ein:</span><span class="sxs-lookup"><span data-stu-id="fc36a-400">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="fc36a-401">Aufrufen von Methoden mit Parametern</span><span class="sxs-lookup"><span data-stu-id="fc36a-401">Calling Methods with Parameters</span></span>

<span data-ttu-id="fc36a-402">In diesem Artikel haben Sie gesehen, verfügen über die Objekte, denen Sie Programmieren mit Methoden aus.</span><span class="sxs-lookup"><span data-stu-id="fc36a-402">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="fc36a-403">Z. B. eine `Database` Objekt möglicherweise eine `Database.Connect` Methode.</span><span class="sxs-lookup"><span data-stu-id="fc36a-403">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="fc36a-404">Viele Methoden verfügen auch über einen oder mehrere Parameter.</span><span class="sxs-lookup"><span data-stu-id="fc36a-404">Many methods also have one or more parameters.</span></span> <span data-ttu-id="fc36a-405">Ein *Parameter* ist ein Wert, der Sie an eine Methode übergeben, um die Methode zum Abschließen des Tasks zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="fc36a-405">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="fc36a-406">Betrachten Sie z. B. eine Deklaration für die `Request.MapPath` -Methode, die drei Parameter akzeptiert:</span><span class="sxs-lookup"><span data-stu-id="fc36a-406">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="fc36a-407">Diese Methode gibt den physischen Pfad auf dem Server, der entspricht einem angegebenen virtuellen Pfad zurück.</span><span class="sxs-lookup"><span data-stu-id="fc36a-407">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="fc36a-408">Die drei Parameter für die Methode sind `virtualPath`, `baseVirtualDir`, und `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="fc36a-408">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="fc36a-409">(Beachten Sie, dass in der Deklaration, die Parameter mit den Datentypen der Daten aufgeführt sind, die eingegeben werden.) Wenn Sie diese Methode aufrufen, müssen Sie Werte für alle drei Parameter angeben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-409">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="fc36a-410">Wenn Sie Visual Basic mit Razor-Syntax verwenden, haben Sie zwei Möglichkeiten zum Übergeben von Parametern an eine Methode: *Positionsparameter* oder *benannte Parameter*.</span><span class="sxs-lookup"><span data-stu-id="fc36a-410">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="fc36a-411">Um eine Methode mithilfe von positionelle Parameter aufzurufen, übergeben Sie die Parameter in einem strikter Reihenfolge, der in der Deklaration der Methode angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="fc36a-411">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="fc36a-412">(Sie würden diese Reihenfolge in der Regel kennen, lesen Sie die Dokumentation für die Methode.) Führen Sie die Reihenfolge, und Sie können einen der Parameter nicht überspringen &#8212; erforderlich, eine leere Zeichenfolge übergeben (`""`) oder null, ein Positionsparameter, die einen Wert für nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="fc36a-412">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="fc36a-413">Im folgende Beispiel wird angenommen, Sie haben einen Ordner namens *Skripts* auf Ihrer Website.</span><span class="sxs-lookup"><span data-stu-id="fc36a-413">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="fc36a-414">Der Code Ruft die `Request.MapPath` -Methode auf und übergibt Werte für die drei Parameter in der richtigen Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="fc36a-414">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="fc36a-415">Dann wird den resultierenden zugeordneten Pfad angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-415">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="fc36a-416">Wenn viele Parameter für eine Methode vorhanden sind, können Sie Ihren Code übersichtlicher und lesbarer beibehalten, durch die Verwendung benannter Parameter.</span><span class="sxs-lookup"><span data-stu-id="fc36a-416">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="fc36a-417">Um eine Methode, die mit benannten Parametern aufzurufen, geben Sie den Parameternamen, gefolgt von `:=` und geben Sie dann den Wert.</span><span class="sxs-lookup"><span data-stu-id="fc36a-417">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="fc36a-418">Ein Vorteil von benannten Parametern ist, dass Sie sie in beliebiger Reihenfolge hinzufügen können Sie die gewünschten.</span><span class="sxs-lookup"><span data-stu-id="fc36a-418">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="fc36a-419">(Ein Nachteil ist, dass der Methodenaufruf nicht so kompakt ist).</span><span class="sxs-lookup"><span data-stu-id="fc36a-419">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="fc36a-420">Im folgenden Beispiel wird die gleiche Methode wie oben beschrieben, aber verwendet benannte Parameter, die Werte anzugeben:</span><span class="sxs-lookup"><span data-stu-id="fc36a-420">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="fc36a-421">Wie Sie sehen können, werden die Parameter in einer anderen Reihenfolge übergeben.</span><span class="sxs-lookup"><span data-stu-id="fc36a-421">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="fc36a-422">Wenn Sie im vorherigen Beispiel und in diesem Beispiel ausführen, werden sie jedoch den gleichen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="fc36a-422">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="fc36a-423">Behandeln von Fehlern</span><span class="sxs-lookup"><span data-stu-id="fc36a-423">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="fc36a-424">Try-Catch-Anweisungen</span><span class="sxs-lookup"><span data-stu-id="fc36a-424">Try-Catch statements</span></span>

<span data-ttu-id="fc36a-425">Sie müssen oft Anweisungen in Ihrem Code, die außerhalb Ihrer Kontrolle Gründen fehlschlagen kann.</span><span class="sxs-lookup"><span data-stu-id="fc36a-425">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="fc36a-426">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="fc36a-426">For example:</span></span>

- <span data-ttu-id="fc36a-427">Wenn Ihr Code versucht, öffnen, erstellen, lesen oder Schreiben einer Datei, alle möglichen Fehler auftreten können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-427">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="fc36a-428">Die gewünschte Datei nicht vorhanden sind, wird sie möglicherweise gesperrt, der Code möglicherweise nicht über Berechtigungen verfügen, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="fc36a-428">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="fc36a-429">Auf ähnliche Weise Wenn Ihr Code versucht, die Datensätze in einer Datenbank zu aktualisieren, können Berechtigungsprobleme vorhanden sein, kann die Verbindung mit der Datenbank gelöscht werden, die zu speichernden Daten möglicherweise ungültig und so weiter.</span><span class="sxs-lookup"><span data-stu-id="fc36a-429">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="fc36a-430">Programmiertechnisch ausgedrückt, werden diese Situationen aufgerufen *Ausnahmen*.</span><span class="sxs-lookup"><span data-stu-id="fc36a-430">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="fc36a-431">Wenn Ihr Code eine Ausnahme auftritt, generiert er (auslöst) eine Fehlermeldung angezeigt, d. h., im besten Fall es ziemlich ärgerlich, für Benutzer.</span><span class="sxs-lookup"><span data-stu-id="fc36a-431">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="fc36a-433">In Situationen, in denen Ihr Code kann Ausnahmen auftreten, und um Fehler Nachrichten dieses Typs zu vermeiden, können Sie `Try/Catch` Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-433">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="fc36a-434">In der `Try` -Anweisung, führen Sie den Code, die Sie überprüfen können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-434">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="fc36a-435">In einer oder mehreren `Catch` -Anweisungen, sehen Sie nach bestimmten Fehlern (bestimmte Arten von Ausnahmen), die aufgetreten sind.</span><span class="sxs-lookup"><span data-stu-id="fc36a-435">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="fc36a-436">Sie können beliebig viele einschließen `Catch` möchte, dass die Anweisungen, wie Sie nach Fehlern zu suchen, die Sie erwarten können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-436">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="fc36a-437">Es wird empfohlen, dass Sie, verwenden vermeiden die `Response.Redirect` -Methode in der `Try/Catch` -Anweisungen, da dies eine Ausnahme auf Ihrer Seite führen kann.</span><span class="sxs-lookup"><span data-stu-id="fc36a-437">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="fc36a-438">Das folgende Beispiel zeigt eine Seite, die auf der ersten Anforderung eine Textdatei erstellt und zeigt dann eine Schaltfläche der Benutzer die Datei zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="fc36a-438">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="fc36a-439">Im Beispiel verwendet absichtlich einen ungültigen Dateinamen ein, damit es eine Ausnahme ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="fc36a-439">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="fc36a-440">Der Code enthält `Catch` -Anweisungen für die zwei möglichen Ausnahmen: `FileNotFoundException`, Dies tritt ein, wenn der Dateiname ungültig, ist und `DirectoryNotFoundException`, Dies tritt ein, wenn ASP.NET nicht den Ordner selbst finden können.</span><span class="sxs-lookup"><span data-stu-id="fc36a-440">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="fc36a-441">(Sie können die auskommentierung Aufheben einer Anweisung im Beispiel um zu sehen, wie sie ausgeführt wird, wenn alles ordnungsgemäß funktioniert.)</span><span class="sxs-lookup"><span data-stu-id="fc36a-441">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="fc36a-442">Wenn Ihr Code die Ausnahme behandelt hat nicht, sehen Sie eine Fehlerseite angezeigt, wie im vorherigen Screenshot.</span><span class="sxs-lookup"><span data-stu-id="fc36a-442">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="fc36a-443">Allerdings die `Try/Catch` Abschnitt hilft zu verhindern, dass den Benutzer diese Arten von Fehlern angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc36a-443">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="fc36a-444">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fc36a-444">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="fc36a-445">Referenzdokumentation</span><span class="sxs-lookup"><span data-stu-id="fc36a-445">Reference Documentation</span></span>

- [<span data-ttu-id="fc36a-446">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fc36a-446">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="fc36a-447">Visual Basic-Sprache</span><span class="sxs-lookup"><span data-stu-id="fc36a-447">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
