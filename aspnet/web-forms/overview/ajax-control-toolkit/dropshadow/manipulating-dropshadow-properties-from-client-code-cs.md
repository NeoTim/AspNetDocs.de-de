---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: Bearbeiten von DropShadow-Eigenschaften über den Clientcode (c#) | Microsoft-Dokumentation
author: wenz
description: Die Bearbeitung von DataList anpassen
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bf4b8fe85780135c821fbb7fcceefd326dce656
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381340"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="8c6c9-103">Bearbeiten von DropShadow-Eigenschaften über den Clientcode (C#)</span><span class="sxs-lookup"><span data-stu-id="8c6c9-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>

<span data-ttu-id="8c6c9-104">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8c6c9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8c6c9-105">[Code herunterladen](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8c6c9-105">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="8c6c9-106">DropShadow-Steuerelements im AJAX Control Toolkit erweitert, einen Bereich mit einem Schlagschatteneffekt.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8c6c9-107">Eigenschaften dieses Extenders können auch mithilfe von JavaScript-Clientcode geändert werden.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-107">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="8c6c9-108">Übersicht</span><span class="sxs-lookup"><span data-stu-id="8c6c9-108">Overview</span></span>

<span data-ttu-id="8c6c9-109">DropShadow-Steuerelements im AJAX Control Toolkit erweitert, einen Bereich mit einem Schlagschatteneffekt.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8c6c9-110">Eigenschaften dieses Extenders können auch mithilfe von JavaScript-Clientcode geändert werden.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8c6c9-111">Schritte</span><span class="sxs-lookup"><span data-stu-id="8c6c9-111">Steps</span></span>

<span data-ttu-id="8c6c9-112">Der Code beginnt mit einem Bereich, der einige Textzeilen enthält:</span><span class="sxs-lookup"><span data-stu-id="8c6c9-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="8c6c9-113">Die zugeordnete CSS-Klasse bietet dem Bereich eine schöne Hintergrundfarbe:</span><span class="sxs-lookup"><span data-stu-id="8c6c9-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="8c6c9-114">Die `DropShadowExtender` hinzugefügt wird, erweitern Sie den Bereich mit einem Schlagschatteneffekt, Deckkraft, die auf 50 % festgelegt:</span><span class="sxs-lookup"><span data-stu-id="8c6c9-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="8c6c9-115">Klicken Sie dann das ASP.NET AJAX `ScriptManager` -Steuerelement können Sie das Steuerelement-Toolkit funktioniert:</span><span class="sxs-lookup"><span data-stu-id="8c6c9-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="8c6c9-116">Einen anderen Bereich enthält zwei JavaScript-Links zum Festlegen der Durchlässigkeit des Schlagschattens: das Minuszeichen links verringert den Schatten Deckkraft, die plus-Verknüpfung wird vergrößert.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="8c6c9-117">Die JavaScript-Funktion `changeOpacity()` suchen müssen Sie dann zuerst die `DropShadowExtender` Steuerelement auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="8c6c9-118">ASP.NET AJAX-definiert den `$find()` -Methode für genau diese Aufgabe.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="8c6c9-119">Anschließend wird die `get_Opacity()` -Methode ruft die aktuelle Durchlässigkeit, ab der `set_Opacity()` Methode festgelegt.</span><span class="sxs-lookup"><span data-stu-id="8c6c9-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="8c6c9-120">Der JavaScript-Code fügt den aktuellen durchsichtigkeitswert klicken Sie dann in der `<label>` Element:</span><span class="sxs-lookup"><span data-stu-id="8c6c9-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


[![T<span data-ttu-id="8c6c9-121">HE Deckkraft wird auf der Clientseite geändert.]</span><span class="sxs-lookup"><span data-stu-id="8c6c9-121">he opacity is changed on the client side]</span></span>(manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

<span data-ttu-id="8c6c9-122">Die Deckkraft wird auf der Clientseite geändert ([klicken Sie, um das Bild in voller Größe anzeigen](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8c6c9-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c6c9-123">[Zurück](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [Weiter](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8c6c9-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
