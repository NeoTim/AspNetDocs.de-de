---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: Verwenden von Postbacks mit dem ReorderList-Steuerelement (VB) | Microsoft-Dokumentation
author: wenz
description: Die ReorderList-Steuerelement im AJAX Control Toolkit enthält eine Liste, die durch den Benutzer über Drag & Drop neu angeordnet werden kann. Wenn die Liste neu angeordnet wird, eine Bestellung...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 1e2124327a36c94db8bafbdf91f767068ac7e834
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025427"
---
<a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="23c84-104">Verwenden von Postbacks mit dem ReorderList-Steuerelement (VB)</span><span class="sxs-lookup"><span data-stu-id="23c84-104">Using Postbacks with ReorderList (VB)</span></span>
====================
<span data-ttu-id="23c84-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="23c84-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="23c84-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="23c84-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="23c84-107">Die ReorderList-Steuerelement im AJAX Control Toolkit enthält eine Liste, die durch den Benutzer über Drag & Drop neu angeordnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="23c84-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="23c84-108">Wenn die Liste neu angeordnet wird, unterrichtet ein Postback den Server über die Änderung.</span><span class="sxs-lookup"><span data-stu-id="23c84-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="23c84-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="23c84-109">Overview</span></span>

<span data-ttu-id="23c84-110">Die `ReorderList` Steuerelement im AJAX Control Toolkit enthält eine Liste, die durch den Benutzer über Drag & Drop neu angeordnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="23c84-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="23c84-111">Wenn die Liste neu angeordnet wird, unterrichtet ein Postback den Server über die Änderung.</span><span class="sxs-lookup"><span data-stu-id="23c84-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="23c84-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="23c84-112">Steps</span></span>

<span data-ttu-id="23c84-113">Es gibt mehrere mögliche Datenquellen für die `ReorderList` Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="23c84-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="23c84-114">Eine ist die Verwendung einer `XmlDataSource` Steuerelement:</span><span class="sxs-lookup"><span data-stu-id="23c84-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="23c84-115">Zum Binden dieser XML-Code, um eine `ReorderList` Postbacks an Kontrolle und aktivieren, die folgenden Attribute müssen festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="23c84-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="23c84-116">`DataSourceID`: Die ID der Datenquelle</span><span class="sxs-lookup"><span data-stu-id="23c84-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="23c84-117">`SortOrderField`: Die Eigenschaft, um nach zu sortieren</span><span class="sxs-lookup"><span data-stu-id="23c84-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="23c84-118">`AllowReorder`: Angibt, ob der Benutzer auf die Listenelemente neu anordnen.</span><span class="sxs-lookup"><span data-stu-id="23c84-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="23c84-119">`PostBackOnReorder`: Angibt, ob einen Postback erstellt, wenn die Liste neu angeordnet werden</span><span class="sxs-lookup"><span data-stu-id="23c84-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="23c84-120">Hier ist das entsprechende Markup für das Steuerelement ein:</span><span class="sxs-lookup"><span data-stu-id="23c84-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="23c84-121">In der `ReorderList` -Steuerelement, bestimmte Daten aus der Datenquelle kann gebunden werden, mithilfe der `Eval()` Methode:</span><span class="sxs-lookup"><span data-stu-id="23c84-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="23c84-122">An einer beliebigen Stelle auf der Seite wird eine Bezeichnung auf die Informationen aufnimmt, wenn die letzte Neuordnung aufgetreten ist:</span><span class="sxs-lookup"><span data-stu-id="23c84-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="23c84-123">Diese Bezeichnung wird mit Text in den serverseitigen Code, der Verarbeitung des Postbacks gefüllt:</span><span class="sxs-lookup"><span data-stu-id="23c84-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="23c84-124">Zum Schluss, um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement auf der Seite platziert werden muss:</span><span class="sxs-lookup"><span data-stu-id="23c84-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


<span data-ttu-id="23c84-125">[![Jede Neuordnung auslöst einen postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23c84-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="23c84-126">Jede Neuordnung einen Postback auslöst ([klicken Sie, um das Bild in voller Größe anzeigen](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="23c84-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="23c84-127">[Zurück](drag-and-drop-via-reorderlist-cs.md)
> [Weiter](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="23c84-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
