---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: Verarbeiten von Postbacks über ein Popupsteuerelement ohne ein UpdatePanel-Steuerelement (VB) | Microsoft-Dokumentation
author: wenz
description: Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist. Wenn ein Postback in "su" erfolgt...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 6dcb2b09279ec6400465f79fadc2a1b6c72f8f07
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064557"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="0017f-104">Verarbeiten von Postbacks über ein Popupsteuerelement ohne ein UpdatePanel-Steuerelement (VB)</span><span class="sxs-lookup"><span data-stu-id="0017f-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="0017f-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0017f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0017f-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0017f-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="0017f-107">Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="0017f-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="0017f-108">Wenn ein Postback, in einem Bereich angezeigt auftritt, und es mehrere Bereiche auf der Seite gibt ist es schwierig, um zu bestimmen, welchen Bereich geklickt wurde.</span><span class="sxs-lookup"><span data-stu-id="0017f-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="0017f-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="0017f-109">Overview</span></span>

<span data-ttu-id="0017f-110">Der PopupControl Extender im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein Popup auslösen, wenn ein anderes Steuerelement aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="0017f-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="0017f-111">Wenn ein Postback, in einem Bereich angezeigt auftritt, und es mehrere Bereiche auf der Seite gibt ist es schwierig, um zu bestimmen, welchen Bereich geklickt wurde.</span><span class="sxs-lookup"><span data-stu-id="0017f-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="0017f-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="0017f-112">Steps</span></span>

<span data-ttu-id="0017f-113">Bei Verwendung einer `PopupControl` mit einem Postback, aber ohne eine `UpdatePanel` auf der Seite das Steuerelement-Toolkit nicht bietet eine Möglichkeit zu bestimmen, welche Client-Element des Popups ausgelöst hat, der wiederum das Postback verursacht hat.</span><span class="sxs-lookup"><span data-stu-id="0017f-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="0017f-114">Jedoch ein kleinen Trick zur Umgehung dieses Problems für dieses Szenario bietet.</span><span class="sxs-lookup"><span data-stu-id="0017f-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="0017f-115">Zunächst sieht die grundlegende Einrichtung: zwei Textfelder, die beide die gleiche Popup, einen Kalender auslösen.</span><span class="sxs-lookup"><span data-stu-id="0017f-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="0017f-116">Zwei `PopupControlExtenders` Vereinen von Textfeldern und den popupausrichtungspunkt.</span><span class="sxs-lookup"><span data-stu-id="0017f-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="0017f-117">Die grundlegende Idee ist, Hinzufügen einer ausgeblendeten Formularfelds in der &lt; `form` &gt; -Element, das das Textfeld enthält, die das Popup gestartet:</span><span class="sxs-lookup"><span data-stu-id="0017f-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="0017f-118">Wenn die Seite geladen wird, fügt einen Ereignishandler von JavaScript-Code auf die beiden Textfelder hinzu: Wenn der Benutzer auf das Textfeld klickt, wird der Name in ausgeblendeten Formularfelds geschrieben:</span><span class="sxs-lookup"><span data-stu-id="0017f-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="0017f-119">In den serverseitigen Code verwenden muss der Wert des ausgeblendeten Felds gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="0017f-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="0017f-120">Da ausgeblendeten Formularfeldern sehr einfach zu bearbeiten sind, ist ein Whitelist-Ansatz zur Überprüfung des Werts der ausgeblendeten erforderlich.</span><span class="sxs-lookup"><span data-stu-id="0017f-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="0017f-121">Nachdem das Textfeld für die richtige identifiziert wurde, wird das Datum aus dem Kalender in diese geschrieben.</span><span class="sxs-lookup"><span data-stu-id="0017f-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


<span data-ttu-id="0017f-122">[![Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0017f-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="0017f-123">Der Kalender wird angezeigt, wenn der Benutzer in das Textfeld klickt ([klicken Sie, um das Bild in voller Größe anzeigen](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0017f-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="0017f-124">[![Durch Klicken auf ein Datum in das Textfeld eingefügt](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0017f-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="0017f-125">Durch Klicken auf ein Datum in das Textfeld eingefügt ([klicken Sie, um das Bild in voller Größe anzeigen](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="0017f-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0017f-126">Vorherige</span><span class="sxs-lookup"><span data-stu-id="0017f-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
