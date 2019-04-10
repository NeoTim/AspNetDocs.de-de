---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Datenbindung des Schieberegler-Steuerelements (VB) | Microsoft-Dokumentation
author: wenz
description: Das Schieberegler-Steuerelement im AJAX Control Toolkit stellt einen grafischen Schieberegler, der mit der Maus kontrolliert werden können. Es ist möglich, binden Sie die aktuelle Position...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a60e09b7cdda7f924a4287aab8cda32fef5a53ac
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419768"
---
# <a name="databinding-the-slider-control-vb"></a><span data-ttu-id="fde2c-104">Datenbindung des Schieberegler-Steuerelements (VB)</span><span class="sxs-lookup"><span data-stu-id="fde2c-104">Databinding the Slider Control (VB)</span></span>

<span data-ttu-id="fde2c-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fde2c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fde2c-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fde2c-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="fde2c-107">Das Schieberegler-Steuerelement im AJAX Control Toolkit stellt einen grafischen Schieberegler, der mit der Maus kontrolliert werden können.</span><span class="sxs-lookup"><span data-stu-id="fde2c-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="fde2c-108">Es ist möglich, die die aktuelle Position des Schiebereglers an ein anderes ASP.NET-Steuerelement zu binden.</span><span class="sxs-lookup"><span data-stu-id="fde2c-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="fde2c-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="fde2c-109">Overview</span></span>

<span data-ttu-id="fde2c-110">Das Schieberegler-Steuerelement im AJAX Control Toolkit stellt einen grafischen Schieberegler, der mit der Maus kontrolliert werden können.</span><span class="sxs-lookup"><span data-stu-id="fde2c-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="fde2c-111">Es ist möglich, die die aktuelle Position des Schiebereglers an ein anderes ASP.NET-Steuerelement zu binden.</span><span class="sxs-lookup"><span data-stu-id="fde2c-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="fde2c-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="fde2c-112">Steps</span></span>

<span data-ttu-id="fde2c-113">Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):</span><span class="sxs-lookup"><span data-stu-id="fde2c-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="fde2c-114">Als Nächstes fügen Sie zwei `TextBox` Steuerelemente auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="fde2c-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="fde2c-115">Transformiert eine in einen grafischen Schieberegler, und der andere Controller wird die Position des Schiebereglers aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="fde2c-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="fde2c-116">Der nächste Schritt ist bereits im letzten Schritt.</span><span class="sxs-lookup"><span data-stu-id="fde2c-116">The next step is already the final step.</span></span> <span data-ttu-id="fde2c-117">Die `SliderExtender` Steuerelement von ASP.NET AJAX Control Toolkit stellt einen Schieberegler aus dem ersten Textfeld, und das zweite Textfeld automatisch aktualisiert, wenn der Schieberegler positionieren Änderungen.</span><span class="sxs-lookup"><span data-stu-id="fde2c-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="fde2c-118">Damit dies funktioniert die `SliderExtender`des `TargetControlID` Attribut muss festgelegt werden, auf die ID des ersten Textfelds; die `BoundControlID` Attribut muss auf die ID des im zweiten Textfeld festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="fde2c-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="fde2c-119">Wie Sie im Browser sehen können, funktioniert die Datenbindung in beide Richtungen: einen neuen Wert in das Textfeld eingeben, aktualisiert die Position der des Schiebereglers.</span><span class="sxs-lookup"><span data-stu-id="fde2c-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="fde2c-120">Wenn Sie das zweite Textfeld schreibgeschützt machen, können Sie einen unzureichenden Schutz auf das Textfeld hinzufügen, sodass es schwieriger für den Benutzer manuell auf den Wert hier aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="fde2c-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


[![S<span data-ttu-id="fde2c-121">Lider und Textfeldern sind synchron.]</span><span class="sxs-lookup"><span data-stu-id="fde2c-121">lider and text box are in sync]</span></span>(databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

<span data-ttu-id="fde2c-122">Schieberegler und Textfeld synchronisiert werden ([klicken Sie, um das Bild in voller Größe anzeigen](databinding-the-slider-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fde2c-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fde2c-123">Vorheriges</span><span class="sxs-lookup"><span data-stu-id="fde2c-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
