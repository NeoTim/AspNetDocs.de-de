---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Datenbindung an Accordion (c#) | Microsoft-Dokumentation
author: wenz
description: Das ' Accordion '-Steuerelement im AJAX Control Toolkit bietet mehrere Bereiche und ermöglicht dem Benutzer eine von ihnen zu einem Zeitpunkt angezeigt. Bereiche werden in der Regel deklariert, w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: d908f89ea1a2b91b9dd7a26d72160e9f38e69c29
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133698"
---
# <a name="databinding-to-an-accordion-c"></a><span data-ttu-id="a39c0-104">Datenbindung an Accordion (C#)</span><span class="sxs-lookup"><span data-stu-id="a39c0-104">Databinding to an Accordion (C#)</span></span>

<span data-ttu-id="a39c0-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a39c0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a39c0-106">[Code herunterladen](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a39c0-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span></span>

> <span data-ttu-id="a39c0-107">Das ' Accordion '-Steuerelement im AJAX Control Toolkit bietet mehrere Bereiche und ermöglicht dem Benutzer eine von ihnen zu einem Zeitpunkt angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a39c0-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="a39c0-108">Bereiche werden in der Regel auf der Seite selbst deklariert, aber die Bindung an eine Datenquelle bietet mehr Flexibilität.</span><span class="sxs-lookup"><span data-stu-id="a39c0-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="a39c0-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a39c0-109">Overview</span></span>

<span data-ttu-id="a39c0-110">Das ' Accordion '-Steuerelement im AJAX Control Toolkit bietet mehrere Bereiche und ermöglicht dem Benutzer eine von ihnen zu einem Zeitpunkt angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a39c0-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="a39c0-111">Bereiche werden in der Regel auf der Seite selbst deklariert, aber die Bindung an eine Datenquelle bietet mehr Flexibilität.</span><span class="sxs-lookup"><span data-stu-id="a39c0-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="a39c0-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="a39c0-112">Steps</span></span>

<span data-ttu-id="a39c0-113">Zunächst einmal ist eine Datenquelle erforderlich.</span><span class="sxs-lookup"><span data-stu-id="a39c0-113">First of all, a data source is required.</span></span> <span data-ttu-id="a39c0-114">Dieses Beispiel verwendet die AdventureWorks-Datenbank und die Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="a39c0-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="a39c0-115">Die Datenbank ist eine optionale Komponente von einer Visual Studio-Installation (einschließlich express Edition) und steht auch als separater Download unter [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="a39c0-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="a39c0-116">Die AdventureWorks-Datenbank ist Teil der SQL Server 2005 Samples and Sample Databases (download unter [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="a39c0-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="a39c0-117">Die einfachste Möglichkeit zum Einrichten der Datenbank ist die Verwendung der Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) und fügen Sie der `AdventureWorks.mdf` Datenbankdatei.</span><span class="sxs-lookup"><span data-stu-id="a39c0-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="a39c0-118">In diesem Beispiel wird angenommen, dass, dass Sie die Instanz von SQL Server 2005 Express Edition aufgerufen wird `SQLEXPRESS` und befindet sich auf dem gleichen Computer wie der Webserver; Dies ist auch der standardeinrichtung.</span><span class="sxs-lookup"><span data-stu-id="a39c0-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="a39c0-119">Wenn Ihr Setup unterscheidet, müssen Sie die Verbindungsinformationen für die Datenbank anpassen.</span><span class="sxs-lookup"><span data-stu-id="a39c0-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="a39c0-120">Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):</span><span class="sxs-lookup"><span data-stu-id="a39c0-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

<span data-ttu-id="a39c0-121">Fügen Sie eine Datenquelle klicken Sie dann auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="a39c0-121">Then, add a data source to the page.</span></span> <span data-ttu-id="a39c0-122">Um eine begrenzte Menge an Daten zu verwenden, wählen wir nur die ersten fünf Einträge in der Vendor-Tabelle der AdventureWorks-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="a39c0-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="a39c0-123">Wenn Sie den Visual Studio-Assistenten zum Erstellen der Datenquelle verwenden, beachten Sie, ein Fehler in der aktuellen Version nicht den Tabellennamen als Präfix ist (`Vendor`) mit `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="a39c0-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="a39c0-124">Das folgende Markup zeigt die korrekte Syntax:</span><span class="sxs-lookup"><span data-stu-id="a39c0-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

<span data-ttu-id="a39c0-125">Beachten Sie den Namen (ID) der Datenquelle aus.</span><span class="sxs-lookup"><span data-stu-id="a39c0-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="a39c0-126">Diese sehr Identifikation muss dann verwendet werden, der `DataSourceID` -Eigenschaft des Steuerelements ' Accordion ':</span><span class="sxs-lookup"><span data-stu-id="a39c0-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

<span data-ttu-id="a39c0-127">Sie können Vorlagen für verschiedene Teile des Steuerelements, einschließlich des Headers bereitstellen, innerhalb des Steuerelements ' Accordion ' (`<HeaderTemplate>`) und den Inhalt (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="a39c0-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="a39c0-128">In der folgenden Elemente, die die Daten aus den Daten ausgeben Datenquelle, mit der `DataBinder.Eval()` Methode:</span><span class="sxs-lookup"><span data-stu-id="a39c0-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

<span data-ttu-id="a39c0-129">Wenn die Seite geladen wird, muss die Datenquelle an das ' Accordion ' durch den folgenden serverseitigen Code gebunden werden:</span><span class="sxs-lookup"><span data-stu-id="a39c0-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

<span data-ttu-id="a39c0-130">Um dieses Beispiel zu beenden, müssen Sie die beiden CSS-Klassen, auf die verwiesen wird, werden im Steuerelement ' Accordion ' definieren (in seinen Eigenschaften `HeaderCssClass` und `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="a39c0-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="a39c0-131">Fügen Sie das folgende Markup in der `<head>` Abschnitt der Seite:</span><span class="sxs-lookup"><span data-stu-id="a39c0-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

<span data-ttu-id="a39c0-132">[![Die Daten in der ' Accordion ' stammt direkt aus der Datenquelle](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a39c0-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span></span>

<span data-ttu-id="a39c0-133">Die Daten in der ' Accordion ' stammt direkt aus der Datenquelle ([klicken Sie, um das Bild in voller Größe anzeigen](databinding-to-an-accordion-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a39c0-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a39c0-134">Nächste</span><span class="sxs-lookup"><span data-stu-id="a39c0-134">Next</span></span>](dynamically-adding-an-accordion-pane-cs.md)
