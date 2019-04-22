---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Erstellen eines Bewertungssteuerelements (c#) | Microsoft-Dokumentation
author: wenz
description: Viele Websites bieten e-Commerce, Community-Sites, die Benutzer auf Rate Artikel oder Elemente. Dies in der Regel erfordert einigen Aufwand beim Codeschreiben, aber wir haben die...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: fa118b4d733d7848b838f80e9918d62ae60033af
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59378974"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="887a8-104">Erstellen eines Bewertungssteuerelements (C#)</span><span class="sxs-lookup"><span data-stu-id="887a8-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="887a8-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="887a8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="887a8-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="887a8-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="887a8-107">Viele Websites bieten e-Commerce, Community-Sites, die Benutzer auf Rate Artikel oder Elemente.</span><span class="sxs-lookup"><span data-stu-id="887a8-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="887a8-108">Dies in der Regel erfordert einigen Aufwand beim Codeschreiben, aber wir müssen das Steuerelement-Toolkit unsere Freigabe.</span><span class="sxs-lookup"><span data-stu-id="887a8-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="887a8-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="887a8-109">Overview</span></span>

<span data-ttu-id="887a8-110">Viele Websites bieten e-Commerce, Community-Sites, die Benutzer auf Rate Artikel oder Elemente.</span><span class="sxs-lookup"><span data-stu-id="887a8-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="887a8-111">Dies in der Regel erfordert einigen Aufwand beim Codeschreiben, aber wir müssen das Steuerelement-Toolkit unsere Freigabe.</span><span class="sxs-lookup"><span data-stu-id="887a8-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="887a8-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="887a8-112">Steps</span></span>

<span data-ttu-id="887a8-113">Als Erstes benötigen Sie (mindestens) zwei Arten von Images: eine für einen ausgefüllten Bewertung Element und eine für ein Element leer Bewertung.</span><span class="sxs-lookup"><span data-stu-id="887a8-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="887a8-114">Ein Element für die Bewertung ist normalerweise ein Stern- oder einem Smiley.</span><span class="sxs-lookup"><span data-stu-id="887a8-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="887a8-115">In diesem Szenario finden Sie drei Dateien, smiley.png und empty.png und Smiley-done.png als Teil der Source-Code-Downloads für dieses Tutorial.</span><span class="sxs-lookup"><span data-stu-id="887a8-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="887a8-116">Anschließend erstellen Sie eine neue ASP.NET-Datei, und beginnen mit dem Hinzufügen einer `ScriptManager` -Steuerelement hinzu:</span><span class="sxs-lookup"><span data-stu-id="887a8-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="887a8-117">Fügen Sie dann die `Rating` Steuerelement von ASP.NET AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="887a8-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="887a8-118">Die folgenden Attribute für dieses Beispiel festgelegt werden müssen:</span><span class="sxs-lookup"><span data-stu-id="887a8-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="887a8-119">`CurrentRating` die erste Bewertung verwendet werden</span><span class="sxs-lookup"><span data-stu-id="887a8-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="887a8-120">`MaxRating` die maximale Bewertung</span><span class="sxs-lookup"><span data-stu-id="887a8-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="887a8-121">`EmptyStarCssClass` die CSS-Klasse verwenden, wenn ein Element der Bewertung (Star) leer ist.</span><span class="sxs-lookup"><span data-stu-id="887a8-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="887a8-122">`FilledStarCssClass` zu verwenden, wenn ein Element der Bewertung (Star) ausgefüllt wird, die CSS-Klasse</span><span class="sxs-lookup"><span data-stu-id="887a8-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="887a8-123">`StarCssClass` die CSS-Klasse, die für einen sichtbaren Stat verwendet</span><span class="sxs-lookup"><span data-stu-id="887a8-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="887a8-124">`WaitingStarCssClass` die CSS-Klasse verwenden, während eine Bewertung von Daten an den Server gesendet wird</span><span class="sxs-lookup"><span data-stu-id="887a8-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="887a8-125">Und hier ist das Markup der einem Steuerelement für Bewertungen mit fünf erstellt Elemente (Smileys), von denen keine anfänglich ausgefüllt wird:</span><span class="sxs-lookup"><span data-stu-id="887a8-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="887a8-126">Die drei referenzierten CSS-Klassen müssen jetzt zeigen die entsprechenden Bilddateien, dies ist ganz einfach mithilfe von CSS:</span><span class="sxs-lookup"><span data-stu-id="887a8-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="887a8-127">Stellen Sie sicher, dass Sie in die Breite und Höhe der drei Images bereitstellen, andernfalls kann die Anzeige ein wenig dachte aussehen.</span><span class="sxs-lookup"><span data-stu-id="887a8-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="887a8-128">Schließlich sollte das Ergebnis der Bewertung werden dem Benutzer angezeigt (oder zumindest in einer Datenbank gespeichert).</span><span class="sxs-lookup"><span data-stu-id="887a8-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="887a8-129">So fügen Sie eine Bezeichnung für die Ausgabe eine SMS-Nachricht und eine Schaltfläche "Senden" Zurücksenden der Bewertung Formular an den Server hinzu:</span><span class="sxs-lookup"><span data-stu-id="887a8-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="887a8-130">Zugriff auf das Steuerelement für Bewertungen über, in den serverseitigen Code, dessen `ID` und rufen Sie die `CurrentRating` Eigenschaft, die die Anzahl der ausgewählten Bewertung Elemente, in unserem Beispiel ein Wert zwischen 0 und 5 ist.</span><span class="sxs-lookup"><span data-stu-id="887a8-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="887a8-131">Speichern Sie die Seite, und Laden Sie sie in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="887a8-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="887a8-132">Wenn Sie auf die Elemente (anfänglich leer) Bewertung zeigen, tritt ein JavaScript-Effekt: Die Bewertung ändert.</span><span class="sxs-lookup"><span data-stu-id="887a8-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="887a8-133">Wenn Sie auf den Satz von Sternen klicken, wird die aktuelle Bewertung beibehalten.</span><span class="sxs-lookup"><span data-stu-id="887a8-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="887a8-134">Wenn Sie das Formular übermitteln, gibt der serverseitige Code schließlich ausgewählte Bewertung aus.</span><span class="sxs-lookup"><span data-stu-id="887a8-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="887a8-135">[![Erstellen ein Bewertungssystem mit minimalem code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="887a8-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="887a8-136">Erstellen ein Bewertungssystem mit minimalem Code ([klicken Sie, um das Bild in voller Größe anzeigen](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="887a8-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="887a8-137">Nächste</span><span class="sxs-lookup"><span data-stu-id="887a8-137">Next</span></span>](creating-a-rating-control-vb.md)
