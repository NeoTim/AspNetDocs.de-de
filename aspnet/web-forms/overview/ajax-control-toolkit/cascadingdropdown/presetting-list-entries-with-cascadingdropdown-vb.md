---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: Vorab festlegen von Listeneinträgen mit CascadingDropDown (VB) | Microsoft-Dokumentation
author: wenz
description: Das CascadingDropDown-Steuerelement im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList zugeordnete Werte in Anoth laden...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599541"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="e604d-103">Vorheriges Festlegen von Listeneinträgen mit CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="e604d-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="e604d-104">von [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e604d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e604d-105">[Code herunterladen](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) oder [PDF herunterladen](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e604d-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="e604d-106">Das CascadingDropDown-Steuerelement im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer Dropdown List zugeordnete Werte in eine andere Dropdown List laden.</span><span class="sxs-lookup"><span data-stu-id="e604d-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="e604d-107">Mit etwas Code ist es möglich, dass ein Listenelement vorab ausgewählt wird, sobald die Daten dynamisch geladen wurden.</span><span class="sxs-lookup"><span data-stu-id="e604d-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="overview"></a><span data-ttu-id="e604d-108">Übersicht über</span><span class="sxs-lookup"><span data-stu-id="e604d-108">Overview</span></span>

<span data-ttu-id="e604d-109">Das CascadingDropDown-Steuerelement im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer Dropdown List zugeordnete Werte in eine andere Dropdown List laden.</span><span class="sxs-lookup"><span data-stu-id="e604d-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="e604d-110">(Eine Liste enthält beispielsweise eine Liste der US-Bundesstaaten, und die nächste Liste wird dann mit den wichtigsten Städten in diesem Zustand aufgefüllt.) Mit etwas Code ist es möglich, dass ein Listenelement vorab ausgewählt wird, sobald die Daten dynamisch geladen wurden.</span><span class="sxs-lookup"><span data-stu-id="e604d-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="e604d-111">Schritte</span><span class="sxs-lookup"><span data-stu-id="e604d-111">Steps</span></span>

<span data-ttu-id="e604d-112">Um die Funktionalität von ASP.NET AJAX und dem Steuerelement-Toolkit zu aktivieren, muss das `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden (innerhalb des `<form>` Elements):</span><span class="sxs-lookup"><span data-stu-id="e604d-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="e604d-113">Anschließend ist ein Dropdown List-Steuerelement erforderlich:</span><span class="sxs-lookup"><span data-stu-id="e604d-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="e604d-114">Für diese Liste wird ein CascadingDropDown-Extender hinzugefügt, der Webdienst-URL und Methoden Informationen bereitstellt:</span><span class="sxs-lookup"><span data-stu-id="e604d-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="e604d-115">Der "CascadingDropDown"-Extender ruft anschließend asynchron einen Webdienst mit der folgenden Methoden Signatur auf:</span><span class="sxs-lookup"><span data-stu-id="e604d-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="e604d-116">Die-Methode gibt ein Array vom Typ CascadingDropDown-Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="e604d-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="e604d-117">Der Konstruktor des Typs erwartet zuerst die Beschriftung des Listen Eintrags und dann den Wert (HTML `value`-Attribut).</span><span class="sxs-lookup"><span data-stu-id="e604d-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="e604d-118">Wenn das dritte Argument auf true festgelegt ist, wird das List-Element automatisch im Browser ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="e604d-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="e604d-119">Wenn Sie die Seite im Browser laden, wird die Dropdown Liste mit drei Anbietern aufgefüllt, die zweite ist vorab ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="e604d-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>

<span data-ttu-id="e604d-120">[![die Liste ausgefüllt und automatisch vorab ausgewählt wird.](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e604d-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="e604d-121">Die Liste wird automatisch ausgefüllt und vorab ausgewählt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)).</span><span class="sxs-lookup"><span data-stu-id="e604d-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e604d-122">[Zurück](using-cascadingdropdown-with-a-database-vb.md)
> [Weiter](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e604d-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
