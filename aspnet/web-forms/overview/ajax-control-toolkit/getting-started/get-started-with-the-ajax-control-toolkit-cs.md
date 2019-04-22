---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Erste Schritte mit dem AJAX Control Toolkit (c#) | Microsoft-Dokumentation
author: microsoft
description: Erfahren Sie, Sie müssen wissen, erste Schritte mit dem AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bbbe0c8240a2a77edee8d39a76bf865c95f345e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59381093"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="2705d-103">Erste Schritte mit dem AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="2705d-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="2705d-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2705d-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2705d-105">Erfahren Sie, Sie müssen wissen, erste Schritte mit dem AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="2705d-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="2705d-106">Das AJAX Control Toolkit enthält mehr als 30 kostenlosen Steuerelemente, die Sie in Ihren ASP.NET-Anwendungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="2705d-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="2705d-107">In diesem Tutorial erfahren Sie, wie das AJAX Control Toolkit herunterladen und Ihre Toolbox Visual Studio/Visual Web Developer Express Toolkit-Steuerelementen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2705d-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="2705d-108">Das AJAX Control Toolkit herunterladen</span><span class="sxs-lookup"><span data-stu-id="2705d-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="2705d-109">Die [AJAX Control Toolkit](http://devexpress.com/act) ist ein open-Source-Projekt entwickelt wurde, durch die Mitglieder der ASP.NET-Community und das ASP.NET-Team.</span><span class="sxs-lookup"><span data-stu-id="2705d-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


<span data-ttu-id="2705d-110">[![Das AJAX Control Toolkit herunterladen](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2705d-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="2705d-111">**Abbildung 01**: Das AJAX Control Toolkit herunterladen ([klicken Sie, um das Bild in voller Größe anzeigen](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="2705d-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="2705d-112">Nachdem Sie die Datei heruntergeladen haben, müssen Sie die Datei zu entsperren.</span><span class="sxs-lookup"><span data-stu-id="2705d-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="2705d-113">Mit der rechten Maustaste in der das, wählen Sie Eigenschaften und klicken Sie auf die **Unblock** Schaltfläche (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="2705d-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


<span data-ttu-id="2705d-114">[![Aufhebung der Blockierung der ZIP-AJAX Control Toolkit-Datei](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2705d-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="2705d-115">**Abbildung 02**: Aufhebung der Blockierung der ZIP-AJAX Control Toolkit-Datei ([klicken Sie, um das Bild in voller Größe anzeigen](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="2705d-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="2705d-116">Nachdem Sie die Blockierung der Datei aufzuheben, können Sie die Datei zu entpacken: Mit der rechten Maustaste in der das, und wählen Sie die **alle extrahieren** Option des Menüs.</span><span class="sxs-lookup"><span data-stu-id="2705d-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="2705d-117">Jetzt können wir das Toolkit zur Visual Studio/Visual Web Developer Toolbox hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2705d-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="2705d-118">Hinzufügen von AJAX Control Toolkit zur Toolbox</span><span class="sxs-lookup"><span data-stu-id="2705d-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="2705d-119">Die einfachste Möglichkeit zum Verwenden von AJAX Control Toolkit wird der Toolbox von Visual Studio/Visual Web Developer das Toolkit hinzugefügt (siehe Abbildung 3).</span><span class="sxs-lookup"><span data-stu-id="2705d-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="2705d-120">Auf diese Weise können Sie einfach ziehen ein Toolkit-Steuerelement auf eine Seite, wenn Sie sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="2705d-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


<span data-ttu-id="2705d-121">[![AJAX Control Toolkit wird in Toolbox angezeigt.](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2705d-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="2705d-122">**Abbildung 03**: AJAX Control Toolkit wird in Toolbox angezeigt ([klicken Sie, um das Bild in voller Größe anzeigen](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2705d-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="2705d-123">Zunächst müssen Sie eine AJAX Control Toolkit-Registerkarte der Toolbox hinzu.</span><span class="sxs-lookup"><span data-stu-id="2705d-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="2705d-124">Gehen Sie wie folgt vor.</span><span class="sxs-lookup"><span data-stu-id="2705d-124">Follow these steps.</span></span>

1. <span data-ttu-id="2705d-125">Erstellen Sie eine neue ASP.NET-Website durch Auswählen der Menüoption Datei neue Website.</span><span class="sxs-lookup"><span data-stu-id="2705d-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="2705d-126">Doppelklicken Sie auf der "default.aspx" im Projektmappen-Explorer-Fenster, um die Datei im Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="2705d-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="2705d-127">Mit der rechten Maustaste in der Toolbox unter der Registerkarte "Allgemein", und wählen Sie die Menüoption **Registerkarte hinzufügen** (siehe Abbildung 4).</span><span class="sxs-lookup"><span data-stu-id="2705d-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="2705d-128">Geben Sie eine neue Registerkarte mit dem Namen AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="2705d-128">Enter a new tab named AJAX Control Toolkit.</span></span>


<span data-ttu-id="2705d-129">[![Hinzufügen einer neuen Registerkarte](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2705d-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="2705d-130">**Abbildung 04**: Hinzufügen einer neuen Registerkarte ([klicken Sie, um das Bild in voller Größe anzeigen](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="2705d-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="2705d-131">Als Nächstes müssen Sie die neue Registerkarte dem AJAX Control Toolkit-Steuerelemente hinzufügen. Führen Sie folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="2705d-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="2705d-132">Mit der rechten Maustaste unterhalb der Registerkarte "AJAX Control Toolkit", und wählen Sie die Menüoption **"Elemente auswählen" (siehe Abbildung 5)**.</span><span class="sxs-lookup"><span data-stu-id="2705d-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="2705d-133">Navigieren Sie zum Speicherort, in dem Sie das AJAX Control Toolkit entpackt und wählen Sie die Assembly AjaxControlToolkit.dll.</span><span class="sxs-lookup"><span data-stu-id="2705d-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


<span data-ttu-id="2705d-134">[![Wählen Sie Elemente aus der Toolbox hinzu](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2705d-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="2705d-135">**Abbildung 05**: Wählen Sie Elemente aus der Toolbox hinzuzufügende ([klicken Sie, um das Bild in voller Größe anzeigen](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="2705d-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="2705d-136">Nachdem Sie diese Schritte abgeschlossen haben, werden sämtliche Toolkit-Steuerelementen in der Toolbox angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2705d-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="2705d-137">Ein Upgrade auf eine neue Version des Toolkits</span><span class="sxs-lookup"><span data-stu-id="2705d-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="2705d-138">Wenn Sie eine ältere Version des Toolkits verwenden würde, und nun verschieben, müssen hier eine höhere Version sind die empfohlenen Schritte:</span><span class="sxs-lookup"><span data-stu-id="2705d-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="2705d-139">Binärdateien - löschen die alte Version der Assembly AjaxControlToolkit.dll aus Ihrem Ordner "Website" Bin ".</span><span class="sxs-lookup"><span data-stu-id="2705d-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="2705d-140">Toolboxelemente - löschen die Registerkarte "AJAX Control Toolkit" und führen Sie die Schritte aus, um die Registerkarte mit der neuen Version der Assembly AjaxControlToolkit.dll neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2705d-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2705d-141">Nächste</span><span class="sxs-lookup"><span data-stu-id="2705d-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
