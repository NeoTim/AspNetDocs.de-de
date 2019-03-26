---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Ausführen von Animationen mit clientseitigen Code (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Die Ausführung der Animation...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: a8812b3b9f9a34b34a579d6f5595b9ffc175caa4
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/25/2019
ms.locfileid: "58420985"
---
<a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="caa06-104">Ausführen von Animationen mit clientseitigem Code (C#)</span><span class="sxs-lookup"><span data-stu-id="caa06-104">Executing Animations Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="caa06-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="caa06-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="caa06-106">[Code herunterladen](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="caa06-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="caa06-107">Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="caa06-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="caa06-108">Die Ausführung der Animation kann auch mit benutzerdefinierte clientseitige JavaScript-Code ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="caa06-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="caa06-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="caa06-109">Overview</span></span>

<span data-ttu-id="caa06-110">Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="caa06-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="caa06-111">Die Ausführung der Animation kann auch mit benutzerdefinierte clientseitige JavaScript-Code ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="caa06-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="caa06-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="caa06-112">Steps</span></span>

<span data-ttu-id="caa06-113">Zunächst einmal sind die `ScriptManager` in die Seite klicken Sie dann die ASP.NET AJAX-Bibliothek wird geladen, lässt sich das Steuerelement-Toolkit verwenden:</span><span class="sxs-lookup"><span data-stu-id="caa06-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="caa06-114">Die Animation wird auf einen Bereich des Texts angewendet werden, der so aussieht:</span><span class="sxs-lookup"><span data-stu-id="caa06-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="caa06-115">Definieren Sie in der zugehörigen CSS-Klasse für den Bereich eine gute Hintergrundfarbe aus, und auch festlegen Sie eine feste Breite für den Bereich:</span><span class="sxs-lookup"><span data-stu-id="caa06-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="caa06-116">Fügen Sie dann die `AnimationExtender` auf der Seite Bereitstellen einer `ID`, `TargetControlID` -Attribut und das obligatorische `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="caa06-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="caa06-117">In der `<Animations>` Knoten verwenden `<OnClick>` klickt Sie auf den Animationen nach dem Benutzer ausgeführt werden im Bereich.</span><span class="sxs-lookup"><span data-stu-id="caa06-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="caa06-118">Fügen Sie zwei Animationen, die parallel ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="caa06-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="caa06-119">Die Zwecke dieser Demo werden dieser Animation (und alle anderen Animationen erstellt, mit dem Steuerelement-Toolkit) ausgeführt mithilfe von JavaScript-Code, sobald die Seite ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="caa06-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="caa06-120">Zunächst einmal benötigen wir Zugriff auf die `AnimationExtender` Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="caa06-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="caa06-121">Die ASP.NET AJAX-Bibliothek stellt die `$find()` -Funktion für diese Aufgabe:</span><span class="sxs-lookup"><span data-stu-id="caa06-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="caa06-122">Die `AnimationExtender` Steuerelement stellt eine umfangreiche API, einschließlich der Methoden mit Namen, die identisch mit die Ereignishandler, die in das XML-Markup verwendet: `OnClick()`, `OnLoad()`und so weiter.</span><span class="sxs-lookup"><span data-stu-id="caa06-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="caa06-123">Z. B. einen Aufruf von der `OnClick()` Methode führt die Animation innerhalb der `<OnClick>` Element der `AnimationExtender` Steuerelement:</span><span class="sxs-lookup"><span data-stu-id="caa06-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="caa06-124">Hier ist der vollständige clientseitige JavaScript-Code, der dem Klicken auf den Bereich emuliert, sobald die Seite vollständig geladen wurde Beachten Sie, dass die `pageLoad()` Funktionsnamen wird verwendet, die von ASP.NET AJAX nach der Seite aufgerufen wird und alle enthaltenen JavaScript-Bibliotheken wurden geladen.</span><span class="sxs-lookup"><span data-stu-id="caa06-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


<span data-ttu-id="caa06-125">[![Die Animation wird sofort ohne ein Mausklick ausgeführt.](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="caa06-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="caa06-126">Die Animation wird sofort ausgeführt, ohne ein Mausklick ([klicken Sie, um das Bild in voller Größe anzeigen](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="caa06-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="caa06-127">[Zurück](modifying-animations-from-the-server-side-cs.md)
> [Weiter](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="caa06-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>
