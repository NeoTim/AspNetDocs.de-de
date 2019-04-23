---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: Ausfüllen einer Liste mit CascadingDropDown (VB) | Microsoft-Dokumentation
author: wenz
description: Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in Anoth verknüpft...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 663dfc76dc3d07dbe9ddca002dc07cb3f9acdb1c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419339"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="487f8-103">Ausfüllen einer Liste mit CascadingDropDown (VB)</span><span class="sxs-lookup"><span data-stu-id="487f8-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="487f8-104">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="487f8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="487f8-105">[Code herunterladen](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="487f8-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="487f8-106">Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in einer anderen DropDownList verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="487f8-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="487f8-107">(Z. B. eine Liste enthält eine Liste der US-Staaten und die folgenden Liste wird dann mit der größten Städte in diesem Zustand gefüllt.) Die erste Herausforderung lösen werden tatsächlich eine Dropdownliste mit diesem Steuerelement geben.</span><span class="sxs-lookup"><span data-stu-id="487f8-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="487f8-108">Übersicht</span><span class="sxs-lookup"><span data-stu-id="487f8-108">Overview</span></span>

<span data-ttu-id="487f8-109">Das Steuerelement "CascadingDropDown" im AJAX Control Toolkit erweitert ein DropDownList-Steuerelement, sodass Änderungen in einer DropDownList lädt Werte in einer anderen DropDownList verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="487f8-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="487f8-110">(Z. B. eine Liste enthält eine Liste der US-Staaten und die folgenden Liste wird dann mit der größten Städte in diesem Zustand gefüllt.) Die erste Herausforderung lösen werden tatsächlich eine Dropdownliste mit diesem Steuerelement geben.</span><span class="sxs-lookup"><span data-stu-id="487f8-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="487f8-111">Schritte</span><span class="sxs-lookup"><span data-stu-id="487f8-111">Steps</span></span>

<span data-ttu-id="487f8-112">Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):</span><span class="sxs-lookup"><span data-stu-id="487f8-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="487f8-113">Anschließend ist ein DropDownList-Steuerelement erforderlich:</span><span class="sxs-lookup"><span data-stu-id="487f8-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="487f8-114">Für diese Liste wird ein CascadingDropDown-Extender hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="487f8-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="487f8-115">Eine asynchrone Anforderung sendet an einen Webdienst die klicken Sie dann eine Liste mit Einträgen in der Liste anzuzeigende zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="487f8-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="487f8-116">Damit dies funktioniert müssen die folgenden CascadingDropDown Attribute festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="487f8-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="487f8-117">`ServicePath`: Die URL eines Webdiensts, der Einträge in der Liste bereitstellen</span><span class="sxs-lookup"><span data-stu-id="487f8-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="487f8-118">`ServiceMethod`: Web-Methode, die Bereitstellung von Einträge in der Liste</span><span class="sxs-lookup"><span data-stu-id="487f8-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="487f8-119">`TargetControlID`: ID der Dropdown-Liste</span><span class="sxs-lookup"><span data-stu-id="487f8-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="487f8-120">`Category`: Kategorieinformationen, die beim Aufruf der Web-Methode übermittelt wird</span><span class="sxs-lookup"><span data-stu-id="487f8-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="487f8-121">`PromptText`: Text, der angezeigt wird, wenn Sie Daten aus der Liste asynchron vom Server geladen</span><span class="sxs-lookup"><span data-stu-id="487f8-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="487f8-122">Dies ist das Markup für die `CascadingDropDown` Element.</span><span class="sxs-lookup"><span data-stu-id="487f8-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="487f8-123">Der einzige Unterschied zwischen c# und VB ist der Name des zugeordneten Webdiensts:</span><span class="sxs-lookup"><span data-stu-id="487f8-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="487f8-124">Der JavaScript-Code, der von der `CascadingDropDown` Extender Aufrufen eine Webdienstmethode mit folgender Signatur:</span><span class="sxs-lookup"><span data-stu-id="487f8-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="487f8-125">Damit der wichtigste Aspekt ist, dass die Methode ein Array vom Typ zurückgeben muss `CascadingDropDownNameValue` (definiert durch die ASP.NET AJAX Control Toolkit).</span><span class="sxs-lookup"><span data-stu-id="487f8-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="487f8-126">In der `CascadingDropDownNameValue` Konstruktor, der erste Eintrag in der der Text, und klicken Sie dann seinen Wert angegeben werden müssen, ebenso wie `<option value="VALUE">NAME</option>` in HTML tun würden.</span><span class="sxs-lookup"><span data-stu-id="487f8-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="487f8-127">Hier sind einige Beispieldaten:</span><span class="sxs-lookup"><span data-stu-id="487f8-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="487f8-128">Die Seite im Browser laden, löst die Liste mit drei Anbietern gefüllt werden soll.</span><span class="sxs-lookup"><span data-stu-id="487f8-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="487f8-129">[![Die Liste wird automatisch ausgefüllt.](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="487f8-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="487f8-130">Die Liste wird automatisch übernommen ([klicken Sie, um das Bild in voller Größe anzeigen](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="487f8-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="487f8-131">[Zurück](using-auto-postback-with-cascadingdropdown-cs.md)
> [Weiter](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="487f8-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
