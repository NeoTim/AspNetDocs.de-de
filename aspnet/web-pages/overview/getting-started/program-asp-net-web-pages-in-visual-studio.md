---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programmierung ASP.NET-Webseiten (Razor) mithilfe von Visual Studio | Microsoft-Dokumentation
author: Rick-Anderson
description: In diesem Anhang wird erläutert, wie Sie Visual Studio 2010 noch Visual Web Developer 2010 Express Programm ASP.NET Web Pages mit Razor-Syntax verwenden können.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 6d25eb99f87c4c3d2c96e021e79a13c90da4a035
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414490"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="8fd39-103">Programmieren von ASP.NET-Webseiten (Razor) mithilfe von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fd39-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="8fd39-104">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8fd39-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8fd39-105">In diesem Artikel wird erläutert, wie Sie Visual Studio oder Visual Web Developer Express für Websites mit ASP.NET Web Pages (Razor)-Programm verwenden können.</span><span class="sxs-lookup"><span data-stu-id="8fd39-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="8fd39-106">Sie lernen Folgendes</span><span class="sxs-lookup"><span data-stu-id="8fd39-106">What you'll learn</span></span>
>
> - <span data-ttu-id="8fd39-107">Was müssen Sie (falls zutreffend) installieren, um mit ASP.NET Web Pages in Ihrer Version von Visual Studio arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8fd39-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="8fd39-108">Wie Sie Support für ASP.NET Web Pages Visual Web Developer 2010 Express hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="8fd39-109">Informationen zu den Funktionen zum Arbeiten mit ASP.NET Razor-Seiten, einschließlich IntelliSense und der Debugger in Visual Studio zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8fd39-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8fd39-110">Softwareversionen, die in diesem Tutorial verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8fd39-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="8fd39-111">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="8fd39-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="8fd39-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8fd39-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="8fd39-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="8fd39-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="8fd39-114">In diesem Tutorial funktioniert auch mit ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010 und WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="8fd39-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>


<span data-ttu-id="8fd39-115">Sie können ASP.NET Web Pages mit Razor-Syntax, die mithilfe von WebMatrix oder viele andere Code-Editoren programmieren.</span><span class="sxs-lookup"><span data-stu-id="8fd39-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="8fd39-116">Sie können auch Microsoft Visual Studio verwenden, eine voll funktionsfähige integrierte Entwicklungsumgebung (IDE), die einen Reihe leistungsstarken Tools bietet für viele Arten von Anwendungen (nicht nur Websites) erstellen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="8fd39-117">Um mit ASP.NET Razor-Seiten arbeiten, können Sie [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="8fd39-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="8fd39-118">Zwei besonders nützlich, Features, die Visual Studio für die Programmierung mit ASP.NET Razor-Webseiten bereitstellt, sind:</span><span class="sxs-lookup"><span data-stu-id="8fd39-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="8fd39-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="8fd39-119">*IntelliSense*.</span></span> <span data-ttu-id="8fd39-120">Die IntelliSense-Funktion, die in Visual Studio integriert ist umfassender als IntelliSense-Funktionen in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8fd39-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="8fd39-121">*Debugger*.</span><span class="sxs-lookup"><span data-stu-id="8fd39-121">*Debugger*.</span></span> <span data-ttu-id="8fd39-122">Mit dem Debugger können Sie Ihren Code zu beheben, indem Sie ein Programm wird beendet, während Sie ausgeführt wird, untersuchen Variablen, und den Code Zeile für Zeile durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="8fd39-123">Mithilfe von Visual Studio mit verschiedenen Versionen von ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="8fd39-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="8fd39-124">Zum Entwickeln von ASP.NET Web-apps in Visual Studio 2017 installieren die **ASP.NET und Webentwicklung** arbeitsauslastung.</span><span class="sxs-lookup"><span data-stu-id="8fd39-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="8fd39-125">Visual Studio 2012 und Visual Studio 2013 enthalten Unterstützung für ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="8fd39-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="8fd39-126">(Die Pakete, die erforderlich sind, um die Unterstützung von ASP.NET Web Pages sind installiert, bei der Installation von Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="8fd39-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="8fd39-127">Visual Studio 2010 wird nicht standardmäßig für ASP.NET Web Pages unterstützen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="8fd39-128">Um ASP.NET Web Pages mit Visual Studio 2010 verwenden zu können, müssen Sie das ASP.NET MVC-Paket installieren.</span><span class="sxs-lookup"><span data-stu-id="8fd39-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="8fd39-129">Um ASP.NET Web Pages 2 zu erhalten, installieren Sie ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="8fd39-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="8fd39-130">Die folgende Tabelle enthält die Unterstützung für ASP.NET Web Pages in verschiedenen Versionen von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fd39-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="8fd39-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="8fd39-131">Visual Studio 2010</span></span> | <span data-ttu-id="8fd39-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="8fd39-132">Visual Studio 2012</span></span> | <span data-ttu-id="8fd39-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8fd39-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| **<span data-ttu-id="8fd39-134">ASP.NET-Webseiten 2</span><span class="sxs-lookup"><span data-stu-id="8fd39-134">ASP.NET Web Pages 2</span></span>** | <span data-ttu-id="8fd39-135">Installieren Sie ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="8fd39-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="8fd39-136">(Enthalten)</span><span class="sxs-lookup"><span data-stu-id="8fd39-136">(Included)</span></span> | <span data-ttu-id="8fd39-137">(Enthalten)</span><span class="sxs-lookup"><span data-stu-id="8fd39-137">(Included)</span></span> |
| **<span data-ttu-id="8fd39-138">ASP.NET-Webseiten 3</span><span class="sxs-lookup"><span data-stu-id="8fd39-138">ASP.NET Web Pages 3</span></span>** |  | <span data-ttu-id="8fd39-139">Update für ASP.NET Web Pages 3 über NuGet</span><span class="sxs-lookup"><span data-stu-id="8fd39-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="8fd39-140">(Enthalten)</span><span class="sxs-lookup"><span data-stu-id="8fd39-140">(Included)</span></span> |

<span data-ttu-id="8fd39-141">Um mit Visual Studio 2010 arbeiten, finden Sie unter [Installieren der Datenbankunterstützung für ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="8fd39-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="8fd39-142">Starten von Visual Studio von WebMatrix</span><span class="sxs-lookup"><span data-stu-id="8fd39-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="8fd39-143">Wenn Sie ein Projekt, klicken Sie in WebMatrix gestartet haben und Visual Studio wechseln möchten, bietet WebMatrix eine Schaltfläche, um das Projekt ganz einfach in Visual Studio zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="8fd39-144">Sie benötigen Visual Studio installiert wird, auf dem Computer für diese Schaltfläche aktiviert werden.</span><span class="sxs-lookup"><span data-stu-id="8fd39-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="8fd39-145">Die folgende Abbildung zeigt die Schaltfläche mit den in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8fd39-145">The following image shows the button in WebMatrix.</span></span>

![Starten Sie Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="8fd39-147">Wenn Sie die Schaltfläche klicken, wird das Projekt in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="8fd39-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="8fd39-148">Sie können WebMatrix und Visual Studio hin-und problemlos wechseln.</span><span class="sxs-lookup"><span data-stu-id="8fd39-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="8fd39-149">Sie werden benachrichtigt, wenn alle Dateien, die in der anderen Umgebung geändert haben und neu geladen werden, um die neuesten Änderungen abzurufen müssen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="8fd39-150">Erstellen von ASP.NET Razor-Website in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fd39-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="8fd39-151">So erstellen eine ASP.NET Razor-Website in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8fd39-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="8fd39-152">Öffnen Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fd39-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="8fd39-153">In der **Datei** Menü klicken Sie auf **neue Website**.</span><span class="sxs-lookup"><span data-stu-id="8fd39-153">In the **File** menu, click **New Web Site**.</span></span>

    ![neue Website erstellen](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="8fd39-155">In der **neue Website** Dialogfeld wählen die Sprache (Visual c# oder Visual Basic) verwenden.</span><span class="sxs-lookup"><span data-stu-id="8fd39-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="8fd39-156">Wählen Sie die **ASP.NET-Website (Razor)** Vorlage.</span><span class="sxs-lookup"><span data-stu-id="8fd39-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![Razor-Website](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="8fd39-158">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fd39-158">Click **OK**.</span></span>

<span data-ttu-id="8fd39-159">Das neue Projekt vorhanden ist und mit einige Standard-Webseiten, die Ihnen beim Einstieg helfen aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="8fd39-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="8fd39-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="8fd39-160">Using IntelliSense</span></span>

<span data-ttu-id="8fd39-161">Nun, dass Sie eine Website erstellt haben, können Sie die Funktionsweise von IntelliSense in Visual Studio sehen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="8fd39-162">Öffnen Sie auf der Website, die Sie gerade erstellt haben, die *Default.cshtml* Seite.</span><span class="sxs-lookup"><span data-stu-id="8fd39-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="8fd39-163">Nach der `<h3>` Geben Sie Tags auf der Seite `@ServerInfo.` (samt Punkt).</span><span class="sxs-lookup"><span data-stu-id="8fd39-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="8fd39-164">Beachten Sie, wie zeigt IntelliSense die verfügbaren Methoden für die `ServerInfo` -Hilfsmethode in einem Dropdown-Liste.</span><span class="sxs-lookup"><span data-stu-id="8fd39-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="8fd39-166">Wählen Sie die `GetHtml` Methode aus der Liste und drücken Sie dann die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="8fd39-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="8fd39-167">IntelliSense füllt automatisch die Methode ab.</span><span class="sxs-lookup"><span data-stu-id="8fd39-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="8fd39-168">(Wie mit einer beliebigen Methode in c# werden soll, das Sie hinzufügen müssen `()` Zeichen nach der Methode.) Den vollständigen Code für die `GetHtml` Methode sieht wie im folgenden Beispiel aus:</span><span class="sxs-lookup"><span data-stu-id="8fd39-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="8fd39-169">Drücken Sie STRG + F5, um die Seite auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="8fd39-170">Dies ist, sieht die Seite, wie wenn in einem Browser angezeigt:</span><span class="sxs-lookup"><span data-stu-id="8fd39-170">This is what the page looks like when displayed in a browser:</span></span>

    ![Standardseite im browser](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="8fd39-172">Schließen Sie den Browser.</span><span class="sxs-lookup"><span data-stu-id="8fd39-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="8fd39-173">Verwenden des Debuggers</span><span class="sxs-lookup"><span data-stu-id="8fd39-173">Using the Debugger</span></span>

1. <span data-ttu-id="8fd39-174">Am oberen Rand der *Default.cshtml* Seite nach der Zeile, die mit beginnt `Page.Title`, fügen Sie die folgende Codezeile hinzu:</span><span class="sxs-lookup"><span data-stu-id="8fd39-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="8fd39-175">In den grauen Rand des Editors auf der linken Seite des Codes, klicken Sie neben auf diese neue Zeile zum Hinzufügen einer *Haltepunkt*.</span><span class="sxs-lookup"><span data-stu-id="8fd39-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="8fd39-176">Ein Haltepunkt ist ein Marker, der weist den Debugger Beenden der Ausführung des Programms an diesem Punkt an, damit Sie sehen, was passiert.</span><span class="sxs-lookup"><span data-stu-id="8fd39-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![Haltepunkt festlegen](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="8fd39-178">Entfernen Sie den Aufruf an die `ServerInfo.GetHtml` -Methode, und fügen Sie einen Aufruf von der `@myTime` Variable an.</span><span class="sxs-lookup"><span data-stu-id="8fd39-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="8fd39-179">Dieser Aufruf zeigt die aktuelle Zeitwert, der von der nächsten Codezeile zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="8fd39-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="8fd39-180">Drücken Sie F5, um die Seite im Debugger auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="8fd39-181">Die Seite hält am Breakpoint, den Sie festlegen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="8fd39-182">Die folgende Abbildung zeigt die Seite im Editor mit dem Haltepunkt (in gelb dargestellt).</span><span class="sxs-lookup"><span data-stu-id="8fd39-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![Haltepunkt](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="8fd39-184">Klicken Sie in der Debug-Symbolleiste auf die **Einzelschritt** Schaltfläche (oder drücken Sie F11), um die nächste Codezeile auszuführen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="8fd39-185">Bei jedem Klicken auf diese Schaltfläche, fahren Sie die Ausführung in die nächste Zeile des Codes fort.</span><span class="sxs-lookup"><span data-stu-id="8fd39-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Einzelschritt in Schaltfläche](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="8fd39-187">Überprüfen Sie den Wert, der die `myTime` Variable, indem Sie den Mauszeiger darüber halten oder überprüfen im angezeigten Werte die **"lokal"** und **Aufrufliste** Windows.</span><span class="sxs-lookup"><span data-stu-id="8fd39-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="8fd39-188">Der Wert der Variablen wird von Visual Studio angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8fd39-188">Visual Studio display the value of the variable.</span></span>

    ![Show-Time-Werten](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="8fd39-190">Wenn Sie fertig sind, untersuchen Variablen und Code schrittweise durchlaufen, drücken Sie F5, um fortzufahren, Ausführen der Seite, ohne bei jeder Zeile.</span><span class="sxs-lookup"><span data-stu-id="8fd39-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="8fd39-191">Wenn Sie alle den Code schrittweise durchlaufen abgeschlossen haben, zeigt der Browser die Seite.</span><span class="sxs-lookup"><span data-stu-id="8fd39-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="8fd39-192">Weitere Informationen zum Debugger und zum Debuggen von Code in Visual Studio finden Sie unter [Exemplarische Vorgehensweise: Debuggen von Webseiten in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fd39-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="8fd39-193">Verwenden von Razor in ASP.NET MVC-Projekte mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fd39-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="8fd39-194">Die Razor-Syntax wird auch umfassend in ASP.NET MVC-Projekten verwendet.</span><span class="sxs-lookup"><span data-stu-id="8fd39-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="8fd39-195">MVC ist eine leistungsfähige, auf Mustern basierende Funktionen zum Entwickeln dynamischer Websites.</span><span class="sxs-lookup"><span data-stu-id="8fd39-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="8fd39-196">Wenn Ihre ASP.NET Web Pages-Website schwierig zu verwalten ist, empfiehlt es sich, sollten ihn in einer ASP.NET MVC-Anwendung zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="8fd39-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="8fd39-197">Ein Beispiel zum Erstellen einer MVC-Anwendung finden Sie unter [erste Schritte mit ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fd39-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="8fd39-198">Installieren von Visual Studio 2010-Unterstützung für ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="8fd39-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="8fd39-199">In diesem Abschnitt veranschaulicht, wie Visual Web Developer Express 2010 und die ASP.NET Web Pages-Tools für Visual Studio zu installieren.</span><span class="sxs-lookup"><span data-stu-id="8fd39-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="8fd39-200">Wenn Sie bereits über den Webplattform-Installer haben, laden Sie sie von folgender URL ein:</span><span class="sxs-lookup"><span data-stu-id="8fd39-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="8fd39-201">Führen Sie den Webplattform-Installer.</span><span class="sxs-lookup"><span data-stu-id="8fd39-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="8fd39-202">Klicken Sie auf die **Produkte** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="8fd39-202">Click the **Products** tab.</span></span>

    ![Registerkarte "WebPI-Produkte"](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="8fd39-204">Suchen Sie nach **ASP.NET MVC 4** (für ASP.NET Web Pages 2), und klicken Sie dann auf **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8fd39-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="8fd39-205">Diese Produkte sind Visual Studio-Tools zum Erstellen von ASP.NET Razor-Websites.</span><span class="sxs-lookup"><span data-stu-id="8fd39-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Optionen der WebPi-Installation](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="8fd39-207">Klicken Sie auf **installieren** um die Installation abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="8fd39-207">Click **Install** to complete the installation.</span></span>
