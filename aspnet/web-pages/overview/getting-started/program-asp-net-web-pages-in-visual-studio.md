---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programmieren ASP.NET Webseiten (Razor) mit Visual Studio | Microsoft Docs
author: Rick-Anderson
description: In diesem Anhang wird erläutert, wie Sie Visual Studio 2010 oder Visual Web Developer 2010 Express verwenden können, um ASP.NET Webseiten mit der Razor-Syntax zu programmieren.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542897"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="46c67-103">Programmieren ASP.NET Webseiten (Razor) mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46c67-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="46c67-104"> von [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="46c67-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="46c67-105">In diesem Artikel wird erläutert, wie Sie Visual Studio oder Visual Web Developer Express verwenden können, um ASP.NET Webseiten (Razor) zu programmieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="46c67-106">Sie lernen Folgendes</span><span class="sxs-lookup"><span data-stu-id="46c67-106">What you'll learn</span></span>
>
> - <span data-ttu-id="46c67-107">Was Sie installieren müssen (falls überhaupt), um mit ASP.NET Webseiten in Ihrer Version von Visual Studio zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="46c67-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="46c67-108">Hinzufügen von Unterstützung für ASP.NET Webseiten zu Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="46c67-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="46c67-109">Verwenden von Features in Visual Studio zum Arbeiten mit ASP.NET Razor-Seiten, einschließlich IntelliSense und dem Debugger.</span><span class="sxs-lookup"><span data-stu-id="46c67-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="46c67-110">Im Tutorial verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="46c67-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="46c67-111">ASP.NET Webseiten (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="46c67-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="46c67-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="46c67-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="46c67-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="46c67-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="46c67-114">Dieses Tutorial funktioniert auch mit ASP.NET Webseiten 2, Visual Studio 2012, Visual Studio 2010 und WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="46c67-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="46c67-115">Sie können ASP.NET Webseiten mit Razor-Syntax mit WebMatrix oder vielen anderen Code-Editoren programmieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="46c67-116">Sie können auch Microsoft Visual Studio verwenden, eine integrierte Entwicklungsumgebung (IDE) mit vollem Umfang, die eine leistungsstarke Reihe von Tools zum Erstellen vieler Anwendungstypen (nicht nur Websites) bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="46c67-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="46c67-117">Um mit ASP.NET Razor-Seiten zu arbeiten, können Sie [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)verwenden.</span><span class="sxs-lookup"><span data-stu-id="46c67-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="46c67-118">Zwei besonders nützliche Funktionen, die Visual Studio für die Programmierung mit ASP.NET Razor-Webseiten bereitstellt, sind:</span><span class="sxs-lookup"><span data-stu-id="46c67-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="46c67-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="46c67-119">*IntelliSense*.</span></span> <span data-ttu-id="46c67-120">Die in Visual Studio integrierte IntelliSense-Funktion ist umfassender als IntelliSense in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="46c67-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="46c67-121">*Debugger*.</span><span class="sxs-lookup"><span data-stu-id="46c67-121">*Debugger*.</span></span> <span data-ttu-id="46c67-122">Mit dem Debugger können Sie Ihren Code beheben, indem Sie ein Programm während der Ausführung anhalten, Variablen untersuchen und die Codezeile zeilefürsch ieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="46c67-123">Verwenden von Visual Studio mit verschiedenen Versionen von ASP.NET Webseiten</span><span class="sxs-lookup"><span data-stu-id="46c67-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="46c67-124">Um ASP.NET Web-Apps in Visual Studio 2017 zu entwickeln, installieren Sie die **ASP.NET- und Webentwicklungsarbeitsauslastung.**</span><span class="sxs-lookup"><span data-stu-id="46c67-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="46c67-125">Visual Studio 2012 und Visual Studio 2013 unterstützen ASP.NET Webseiten.</span><span class="sxs-lookup"><span data-stu-id="46c67-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="46c67-126">(Die Pakete, die zur Unterstützung ASP.NET Webseiten erforderlich sind, werden bei der Installation von Visual Studio installiert.)</span><span class="sxs-lookup"><span data-stu-id="46c67-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="46c67-127">Visual Studio 2010 bietet standardmäßig keine Unterstützung für ASP.NET Webseiten.</span><span class="sxs-lookup"><span data-stu-id="46c67-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="46c67-128">Um ASP.NET Webseiten mit Visual Studio 2010 zu verwenden, müssen Sie das ASP.NET MVC-Paket installieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="46c67-129">Um ASP.NET Webseiten 2 zu erhalten, installieren Sie ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="46c67-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="46c67-130">In der folgenden Tabelle wird die Unterstützung für ASP.NET Webseiten in verschiedenen Versionen von Visual Studio zusammengefasst.</span><span class="sxs-lookup"><span data-stu-id="46c67-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="46c67-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="46c67-131">Visual Studio 2010</span></span> | <span data-ttu-id="46c67-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="46c67-132">Visual Studio 2012</span></span> | <span data-ttu-id="46c67-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="46c67-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46c67-134">**ASP.NET-Webseiten 2**</span><span class="sxs-lookup"><span data-stu-id="46c67-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="46c67-135">Installieren ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="46c67-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="46c67-136">(Inbegriffen)</span><span class="sxs-lookup"><span data-stu-id="46c67-136">(Included)</span></span> | <span data-ttu-id="46c67-137">(Inbegriffen)</span><span class="sxs-lookup"><span data-stu-id="46c67-137">(Included)</span></span> |
| <span data-ttu-id="46c67-138">**ASP.NET-Webseiten 3**</span><span class="sxs-lookup"><span data-stu-id="46c67-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="46c67-139">Aktualisieren auf ASP.NET Webseiten 3 über NuGet</span><span class="sxs-lookup"><span data-stu-id="46c67-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="46c67-140">(Inbegriffen)</span><span class="sxs-lookup"><span data-stu-id="46c67-140">(Included)</span></span> |

<span data-ttu-id="46c67-141">Informationen zum Arbeiten mit Visual Studio 2010 finden Sie unter Installieren von [Support für ASP.NET Webseiten in Visual Studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="46c67-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="46c67-142">Starten von Visual Studio über WebMatrix</span><span class="sxs-lookup"><span data-stu-id="46c67-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="46c67-143">Wenn Sie ein Projekt in WebMatrix gestartet haben und zu Visual Studio wechseln möchten, stellt WebMatrix eine Schaltfläche zum einfachen Öffnen des Projekts in Visual Studio bereit.</span><span class="sxs-lookup"><span data-stu-id="46c67-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="46c67-144">Sie müssen Visual Studio auf Ihrem Computer installiert haben, damit diese Schaltfläche aktiviert werden kann.</span><span class="sxs-lookup"><span data-stu-id="46c67-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="46c67-145">Die folgende Abbildung zeigt die Schaltfläche in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="46c67-145">The following image shows the button in WebMatrix.</span></span>

![Starten von Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="46c67-147">Wenn Sie auf die Schaltfläche klicken, wird das Projekt in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="46c67-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="46c67-148">Sie können problemlos zwischen WebMatrix und Visual Studio hin- und herwechseln.</span><span class="sxs-lookup"><span data-stu-id="46c67-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="46c67-149">Sie werden benachrichtigt, wenn dateien in der anderen Umgebung geändert wurden und neu geladen werden müssen, um die neuesten Änderungen zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="46c67-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="46c67-150">Erstellen ASP.NET Razor-Site in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46c67-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="46c67-151">So erstellen Sie eine ASP.NET Razor-Website in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="46c67-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="46c67-152">Öffnen Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46c67-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="46c67-153">Klicken Sie im Menü **Datei** auf **Neue Website**.</span><span class="sxs-lookup"><span data-stu-id="46c67-153">In the **File** menu, click **New Web Site**.</span></span>

    ![Erstellen einer neuen Website](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="46c67-155">Wählen Sie im Dialogfeld **Neue Website** die zu verwendende Sprache aus (Visual C oder Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="46c67-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="46c67-156">Wählen Sie die **Vorlage ASP.NET Website (Razor)** aus.</span><span class="sxs-lookup"><span data-stu-id="46c67-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![Rasierer-Website](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="46c67-158">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="46c67-158">Click **OK**.</span></span>

<span data-ttu-id="46c67-159">Ihr neues Projekt ist vorhanden und wird mit einigen Standardwebseiten gefüllt, die Ihnen bei den ersten Informationen helfen.</span><span class="sxs-lookup"><span data-stu-id="46c67-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="46c67-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="46c67-160">Using IntelliSense</span></span>

<span data-ttu-id="46c67-161">Nachdem Sie nun eine Website erstellt haben, können Sie sehen, wie IntelliSense in Visual Studio funktioniert.</span><span class="sxs-lookup"><span data-stu-id="46c67-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="46c67-162">Öffnen Sie auf der Website, die Sie gerade erstellt haben, die Seite *Default.cshtml.*</span><span class="sxs-lookup"><span data-stu-id="46c67-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="46c67-163">Geben `<h3>` Sie `@ServerInfo.` nach den Tags auf der Seite (einschließlich des Punktes) ein.</span><span class="sxs-lookup"><span data-stu-id="46c67-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="46c67-164">Beachten Sie, wie IntelliSense `ServerInfo` die verfügbaren Methoden für den Helfer in einer Dropdownliste anzeigt.</span><span class="sxs-lookup"><span data-stu-id="46c67-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="46c67-166">Wählen `GetHtml` Sie die Methode aus der Liste aus, und drücken Sie dann die Eingabetaste.</span><span class="sxs-lookup"><span data-stu-id="46c67-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="46c67-167">IntelliSense füllt die Methode automatisch aus.</span><span class="sxs-lookup"><span data-stu-id="46c67-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="46c67-168">(Wie bei jeder Methode in C- müssen Sie Zeichen nach der Methode hinzufügen.) `()` Der abgeschlossene `GetHtml` Code für die Methode sieht wie im folgenden Beispiel aus:</span><span class="sxs-lookup"><span data-stu-id="46c67-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="46c67-169">Drücken Sie Strg+F5, um die Seite auszuführen.</span><span class="sxs-lookup"><span data-stu-id="46c67-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="46c67-170">So sieht die Seite aus, wenn sie in einem Browser angezeigt wird:</span><span class="sxs-lookup"><span data-stu-id="46c67-170">This is what the page looks like when displayed in a browser:</span></span>

    ![Standardseite im Browser](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="46c67-172">Schließen Sie den Browser.</span><span class="sxs-lookup"><span data-stu-id="46c67-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="46c67-173">Verwenden des Debuggers</span><span class="sxs-lookup"><span data-stu-id="46c67-173">Using the Debugger</span></span>

1. <span data-ttu-id="46c67-174">Fügen Sie oben auf der Seite *Default.cshtml* `Page.Title`nach der Zeile, die mit beginnt, die folgende Codezeile hinzu:</span><span class="sxs-lookup"><span data-stu-id="46c67-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="46c67-175">Klicken Sie am grauen Rand des Editors links neben dem Code, um einen *Haltepunkt*hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="46c67-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="46c67-176">Ein Haltepunkt ist ein Marker, der den Debugger anweist, das Programm zu diesem Zeitpunkt nicht mehr auszuführen, damit Sie sehen können, was passiert.</span><span class="sxs-lookup"><span data-stu-id="46c67-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![Sollpunkt festlegen](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="46c67-178">Entfernen Sie den `ServerInfo.GetHtml` Aufruf der Methode, `@myTime` und fügen Sie der Variablen an ihrer Stelle einen Aufruf hinzu.</span><span class="sxs-lookup"><span data-stu-id="46c67-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="46c67-179">Dieser Aufruf zeigt den aktuellen Zeitwert an, der von der neuen Codezeile zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="46c67-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="46c67-180">Drücken Sie F5, um die Seite im Debugger auszuführen.</span><span class="sxs-lookup"><span data-stu-id="46c67-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="46c67-181">Die Seite wird auf dem von Ihnen festgelegten Haltepunkt angehalten.</span><span class="sxs-lookup"><span data-stu-id="46c67-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="46c67-182">Die folgende Abbildung zeigt, wie die Seite im Editor mit dem Haltepunkt (gelb) aussieht.</span><span class="sxs-lookup"><span data-stu-id="46c67-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![Debug-Haltepunkt](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="46c67-184">Klicken Sie in der Symbolleiste Debuggen auf die Schaltfläche **Schritt in** (oder drücken Sie F11), um die nächste Codezeile auszuführen.</span><span class="sxs-lookup"><span data-stu-id="46c67-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="46c67-185">Jedes Mal, wenn Sie auf diese Schaltfläche klicken, leiten Sie die Ausführung zur nächsten Codezeile weiter.</span><span class="sxs-lookup"><span data-stu-id="46c67-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Schritt in die Taste](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="46c67-187">Untersuchen Sie den `myTime` Wert der Variablen, indem Sie den Mauszeiger darüber halten oder die Werte überprüfen, die in den Fenstern **Locals** und **Call Stack** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="46c67-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="46c67-188">Visual Studio zeigt den Wert der Variablen an.</span><span class="sxs-lookup"><span data-stu-id="46c67-188">Visual Studio display the value of the variable.</span></span>

    ![Zeitwert anzeigen](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="46c67-190">Wenn Sie die Variable untersuchen und den Code durchlaufen, drücken Sie F5, um die Ausführung der Seite fortzusetzen, ohne an jeder Zeile anzuhalten.</span><span class="sxs-lookup"><span data-stu-id="46c67-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="46c67-191">Wenn Sie den gesamten Code durchlaufen haben, zeigt der Browser die Seite an.</span><span class="sxs-lookup"><span data-stu-id="46c67-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="46c67-192">Weitere Informationen zum Debugger und zum Debuggen von Code in Visual Studio finden Sie unter [Exemplarische Vorgehensweise: Debuggen von Webseiten in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="46c67-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="46c67-193">Verwenden von Razor in ASP.NET MVC-Projekten mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46c67-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="46c67-194">Die Razor-Syntax wird auch in ASP.NET MVC-Projekten ausgiebig verwendet.</span><span class="sxs-lookup"><span data-stu-id="46c67-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="46c67-195">MVC ist eine leistungsstarke, musterbasierte Möglichkeit, dynamische Websites zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="46c67-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="46c67-196">Wenn ihre ASP.NET Webseiten-Website schwierig zu verwalten ist, sollten Sie sie in eine ASP.NET MVC-Anwendung konvertieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="46c67-197">Ein Beispiel für das Erstellen einer MVC-Anwendung finden Sie unter [Erste Schritte mit ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="46c67-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="46c67-198">Installieren der Unterstützung für ASP.NET Webseiten in Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="46c67-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="46c67-199">In diesem Abschnitt wird gezeigt, wie Sie Visual Web Developer Express 2010 und die ASP.NET Web Pages Tools for Visual Studio installieren.</span><span class="sxs-lookup"><span data-stu-id="46c67-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="46c67-200">Wenn Sie noch nicht über den Web Platform Installer verfügen, laden Sie ihn von der folgenden URL herunter:</span><span class="sxs-lookup"><span data-stu-id="46c67-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="46c67-201">Führen Sie das Web platform Installer aus.</span><span class="sxs-lookup"><span data-stu-id="46c67-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="46c67-202">Klicken Sie auf die Registerkarte **Produkte.**</span><span class="sxs-lookup"><span data-stu-id="46c67-202">Click the **Products** tab.</span></span>

    ![Registerkarte WebPI-Produkte](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="46c67-204">Suchen Sie nach **ASP.NET MVC 4** (für ASP.NET Webseiten 2) und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="46c67-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="46c67-205">Zu diesen Produkten gehören Visual Studio-Tools zum Erstellen ASP.NET Razor-Websites.</span><span class="sxs-lookup"><span data-stu-id="46c67-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi-Installationsoptionen](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="46c67-207">Klicken Sie auf **Installieren,** um die Installation abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="46c67-207">Click **Install** to complete the installation.</span></span>
