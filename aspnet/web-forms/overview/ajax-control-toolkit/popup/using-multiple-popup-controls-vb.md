---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: Verwenden von mehreren Popupsteuerelementen (VB) | Microsoft-Dokumentation
author: wenz
description: Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist. Es ist auch möglich, m verwenden...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: ee66e166d24bb80008671c84f6512d5c54707fcf
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389816"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="13c43-104">Verwenden von mehreren Popupsteuerelementen (VB)</span><span class="sxs-lookup"><span data-stu-id="13c43-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="13c43-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="13c43-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="13c43-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="13c43-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="13c43-107">Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="13c43-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="13c43-108">Es ist auch möglich, mehr als eine Popup-Steuerelement auf einer Seite zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="13c43-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="13c43-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="13c43-109">Overview</span></span>

<span data-ttu-id="13c43-110">Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="13c43-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="13c43-111">Es ist auch möglich, mehr als eine Popup-Steuerelement auf einer Seite zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="13c43-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="13c43-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="13c43-112">Steps</span></span>

<span data-ttu-id="13c43-113">Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):</span><span class="sxs-lookup"><span data-stu-id="13c43-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="13c43-114">Fügen Sie einen Bereich, der als das Popup dient.</span><span class="sxs-lookup"><span data-stu-id="13c43-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="13c43-115">In aktuellen Szenario können der Bereich enthält eine `Calendar` Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="13c43-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="13c43-116">Um die Seite wird aktualisiert, die aufgrund des Kalenders Postbacks zu vermeiden, platziert der Bereich innerhalb einer `UpdatePanel` Steuerelement:</span><span class="sxs-lookup"><span data-stu-id="13c43-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="13c43-117">Die Seite enthält außerdem zwei Textfelder.</span><span class="sxs-lookup"><span data-stu-id="13c43-117">The page also contains two text boxes.</span></span> <span data-ttu-id="13c43-118">Für jedes Textfeld muss Calendar Popupfenster angezeigt, sobald das Textfeld aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="13c43-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="13c43-119">Jetzt erweitern Sie die beiden Textfelder mit einem `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="13c43-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="13c43-120">Die `TargetControlID` Attribut stellt die ID des Steuerelements mit der Extender verknüpft.</span><span class="sxs-lookup"><span data-stu-id="13c43-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="13c43-121">Die `PopupControlID` Attribut enthält die ID der dem Popupfenster.</span><span class="sxs-lookup"><span data-stu-id="13c43-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="13c43-122">In diesem Fall sowohl Extender anzeigen im gleichen Bereich, jedoch unterschiedliche Bereiche sind auch möglich.</span><span class="sxs-lookup"><span data-stu-id="13c43-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="13c43-123">Nun, wenn Sie in einem Textfeld klicken, wird ein Kalender angezeigt unterhalb des Felds, in dem ein Datum ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="13c43-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="13c43-124">(Beim Abrufen des ausgewählten Datums zurück in die Textfelder wird in einem anderen Tutorial erläutert.)</span><span class="sxs-lookup"><span data-stu-id="13c43-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="13c43-125">[![Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="13c43-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="13c43-126">Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt ([klicken Sie, um das Bild in voller Größe anzeigen](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="13c43-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="13c43-127">[Zurück](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [Weiter](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="13c43-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
