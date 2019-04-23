---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Animation Abhängigkeit einer Bedingung (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Gibt an, ob eine Animation zu ist...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: c05f0976a135615f7a272b8057eb4c56677e5117
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59412423"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="5c86c-104">Von einer Bedingung abhängige Animation (C#)</span><span class="sxs-lookup"><span data-stu-id="5c86c-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="5c86c-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5c86c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5c86c-106">[Code herunterladen](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5c86c-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="5c86c-107">Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5c86c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5c86c-108">Gibt an, ob eine Animation ausgeführt wird oder nicht, kann auch auf einer Bedingung in Form von JavaScript-Code abhängen.</span><span class="sxs-lookup"><span data-stu-id="5c86c-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="5c86c-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="5c86c-109">Overview</span></span>

<span data-ttu-id="5c86c-110">Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5c86c-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5c86c-111">Gibt an, ob eine Animation ausgeführt wird oder nicht, kann auch auf einer Bedingung in Form von JavaScript-Code abhängen.</span><span class="sxs-lookup"><span data-stu-id="5c86c-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="5c86c-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="5c86c-112">Steps</span></span>

<span data-ttu-id="5c86c-113">Zunächst einmal sind die `ScriptManager` in die Seite klicken Sie dann die ASP.NET AJAX-Bibliothek wird geladen, lässt sich das Steuerelement-Toolkit verwenden:</span><span class="sxs-lookup"><span data-stu-id="5c86c-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="5c86c-114">Die Animation wird auf einen Bereich des Texts angewendet werden, der so aussieht:</span><span class="sxs-lookup"><span data-stu-id="5c86c-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="5c86c-115">Definieren Sie in der zugehörigen CSS-Klasse für den Bereich eine gute Hintergrundfarbe aus, und auch festlegen Sie eine feste Breite für den Bereich:</span><span class="sxs-lookup"><span data-stu-id="5c86c-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="5c86c-116">Fügen Sie dann die `AnimationExtender` auf der Seite Bereitstellen einer `ID`, `TargetControlID` -Attribut und das obligatorische `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="5c86c-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="5c86c-117">In der `<Animations>` Knoten verwenden `<OnLoad>` die Animationen ausgeführt werden, nachdem die Seite vollständig geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="5c86c-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="5c86c-118">Statt in einem regulären-Animationen die `<Condition>` Element ins Spiel.</span><span class="sxs-lookup"><span data-stu-id="5c86c-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="5c86c-119">Der JavaScript-Code bereitgestellt, die als Wert für die `ConditionScript` Attribut zur Laufzeit ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5c86c-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="5c86c-120">Wenn sie auf "true" ausgewertet wird, wird die Animation, andernfalls nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="5c86c-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="5c86c-121">Das folgende Markup stellt zwei Animationen, die jeweils 50 % der Fälle, bei der zufälligen ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5c86c-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="5c86c-122">Da es möglicherweise nur eine Animation in `<OnLoad>`, die beiden `<Condition>` Animationen angehören, mithilfe der `<Sequence>` Element:</span><span class="sxs-lookup"><span data-stu-id="5c86c-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="5c86c-123">Beachten Sie, dass das kleiner-als-Zeichen (`<`) in der `ConditionScript` -Attribut muss mit Escapezeichen (-) sein.</span><span class="sxs-lookup"><span data-stu-id="5c86c-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="5c86c-124">Wenn Sie führen dieses Skript entweder keine Animation ausgeführt wird, ist einer der beiden oder beides.</span><span class="sxs-lookup"><span data-stu-id="5c86c-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="5c86c-125">[![Der Bereich wird ohne Änderung der Größe, ausgeblendet wird, damit nicht die zweite Animation-ausgeführt wird, die erste Bedingung](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5c86c-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="5c86c-126">Der Bereich wird ausgeblendet wird, ohne Änderung der Größe, damit die zweite Animation-ausgeführt wird, die erste Bedingung nicht ([klicken Sie, um das Bild in voller Größe anzeigen](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5c86c-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c86c-127">[Zurück](executing-several-animations-after-each-other-cs.md)
> [Weiter](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5c86c-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
