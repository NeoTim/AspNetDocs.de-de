---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: Verwenden von HoverMenu mit einem Wiederholungssteuerelement (VB) | Microsoft-Dokumentation
author: wenz
description: 'Der HoverMenu-Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an eine speziell...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ef2481b93a8bbe16b79edb8c93c02e24fc9890f3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046457"
---
<a name="using-hovermenu-with-a-repeater-control-vb"></a><span data-ttu-id="da5f0-103">Verwenden von HoverMenu mit einem Wiederholungssteuerelement (VB)</span><span class="sxs-lookup"><span data-stu-id="da5f0-103">Using HoverMenu with a Repeater Control (VB)</span></span>
====================
<span data-ttu-id="da5f0-104">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="da5f0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="da5f0-105">[Code herunterladen](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="da5f0-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span></span>

> <span data-ttu-id="da5f0-106">Der HoverMenu-Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an der angegebenen Position.</span><span class="sxs-lookup"><span data-stu-id="da5f0-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="da5f0-107">Es ist auch möglich, dieses Steuerelement in einem wiederholungssteuerelement zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="da5f0-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="da5f0-108">Übersicht</span><span class="sxs-lookup"><span data-stu-id="da5f0-108">Overview</span></span>

<span data-ttu-id="da5f0-109">Die `HoverMenu` Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an der angegebenen Position.</span><span class="sxs-lookup"><span data-stu-id="da5f0-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="da5f0-110">Es ist auch möglich, dieses Steuerelement in einem wiederholungssteuerelement zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="da5f0-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="da5f0-111">Schritte</span><span class="sxs-lookup"><span data-stu-id="da5f0-111">Steps</span></span>

<span data-ttu-id="da5f0-112">Zunächst einmal ist eine Datenquelle erforderlich.</span><span class="sxs-lookup"><span data-stu-id="da5f0-112">First of all, a data source is required.</span></span> <span data-ttu-id="da5f0-113">Dieses Beispiel verwendet die AdventureWorks-Datenbank und die Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="da5f0-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="da5f0-114">Die Datenbank ist eine optionale Komponente von einer Visual Studio-Installation (einschließlich express Edition) und steht auch als separater Download unter [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="da5f0-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="da5f0-115">Die AdventureWorks-Datenbank ist Teil der SQL Server 2005 Samples and Sample Databases (download unter [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="da5f0-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="da5f0-116">Die einfachste Möglichkeit zum Einrichten der Datenbank ist die Verwendung der Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) und fügen Sie der `AdventureWorks.mdf` Datenbankdatei.</span><span class="sxs-lookup"><span data-stu-id="da5f0-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="da5f0-117">In diesem Beispiel wird angenommen, dass, dass Sie die Instanz von SQL Server 2005 Express Edition aufgerufen wird `SQLEXPRESS` und befindet sich auf dem gleichen Computer wie der Webserver; Dies ist auch der standardeinrichtung.</span><span class="sxs-lookup"><span data-stu-id="da5f0-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="da5f0-118">Wenn Ihr Setup unterscheidet, müssen Sie die Verbindungsinformationen für die Datenbank anpassen.</span><span class="sxs-lookup"><span data-stu-id="da5f0-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="da5f0-119">Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):</span><span class="sxs-lookup"><span data-stu-id="da5f0-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="da5f0-120">Fügen Sie eine Datenquelle klicken Sie dann auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="da5f0-120">Then, add a data source to the page.</span></span> <span data-ttu-id="da5f0-121">Um eine begrenzte Menge an Daten zu verwenden, wählen wir nur die ersten fünf Einträge in der Vendor-Tabelle der AdventureWorks-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="da5f0-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="da5f0-122">Wenn Sie den Visual Studio-Assistenten zum Erstellen der Datenquelle verwenden, beachten Sie, ein Fehler in der aktuellen Version nicht den Tabellennamen als Präfix ist (`Vendor`) mit `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="da5f0-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="da5f0-123">Das folgende Markup zeigt die korrekte Syntax:</span><span class="sxs-lookup"><span data-stu-id="da5f0-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="da5f0-124">Als Nächstes fügen Sie einen Bereich, der als modales Fenster dient:</span><span class="sxs-lookup"><span data-stu-id="da5f0-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="da5f0-125">Jetzt die `HoverMenuExtender` ins Spiel.</span><span class="sxs-lookup"><span data-stu-id="da5f0-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="da5f0-126">Damit, dass jedes Element in der Datenquelle einen eigenen Popup erhält, muss der Extender platziert werden, innerhalb des Repeaters `<ItemTemplate>` Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="da5f0-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="da5f0-127">Dies ist das Markup:</span><span class="sxs-lookup"><span data-stu-id="da5f0-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="da5f0-128">Jetzt jedes Element in der Datenquelle ein Popups auf der rechten Seite zeigt (`PopupPosition` Attribut) nach einer Verzögerung von 50 Millisekunden (`PopDelay` Attribut).</span><span class="sxs-lookup"><span data-stu-id="da5f0-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="da5f0-129">[![Neben jedem Element im wiederholungsmodul wird im Menü angezeigt.](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="da5f0-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="da5f0-130">Das Hovermenü angezeigt wird, neben jedem Element im wiederholungsmodul ([klicken Sie, um das Bild in voller Größe anzeigen](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="da5f0-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="da5f0-131">Vorherige</span><span class="sxs-lookup"><span data-stu-id="da5f0-131">Previous</span></span>](using-hovermenu-with-a-repeater-control-cs.md)
