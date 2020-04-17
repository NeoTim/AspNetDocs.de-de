---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: Erste Schritte mit dem AJAX Control Toolkit (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie alles, was Sie wissen müssen, um mit dem AJAX Control Toolkit zu beginnen.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543560"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>Erste Schritte mit dem AJAX Control Toolkit (VB)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie alles, was Sie wissen müssen, um mit dem AJAX Control Toolkit zu beginnen.

Das AJAX Control Toolkit enthält mehr als 30 kostenlose Steuerelemente, die Sie in Ihren ASP.NET Anwendungen verwenden können. In diesem Tutorial erfahren Sie, wie Sie das AJAX Control Toolkit herunterladen und die Toolkitsteuerelemente zu Ihrer Visual Studio/Visual Web Developer Express-Toolbox hinzufügen.

## <a name="downloading-the-ajax-control-toolkit"></a>Herunterladen des AJAX Control Toolkit

Das [AJAX Control Toolkit](http://devexpress.com/act) ist ein Open-Source-Projekt, das von den Mitgliedern der ASP.NET Community und dem ASP.NET-Team entwickelt wurde.

[![Herunterladen des AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**Abbildung 01**: Herunterladen des AJAX Control Toolkit([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

Nachdem Sie die Datei heruntergeladen haben, müssen Sie die Blockierung der Datei aufheben. Klicken Sie mit der rechten Maustaste auf die Datei, wählen Sie Eigenschaften aus, und klicken Sie auf die Schaltfläche **Entsperren** (siehe Abbildung 2).

[![Entsperren der ZIP-Datei des AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**Abbildung 02**: Entsperren der ZIP-Datei des AJAX Control Toolkit ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)

Nachdem Sie die Datei aufheben, können Sie die Datei entpacken: Klicken Sie mit der rechten Maustaste auf die Datei und wählen Sie die Menüoption **Alle extrahieren** aus. Jetzt können wir das Toolkit der Visual Studio/Visual Web Developer-Toolbox hinzufügen.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Hinzufügen des AJAX Control Toolkits zur Toolbox

Die einfachste Möglichkeit, das AJAX Control Toolkit zu verwenden, besteht darin, das Toolkit zu Ihrer Visual Studio/Visual Web Developer-Toolbox hinzuzufügen (siehe Abbildung 3). Auf diese Weise können Sie einfach ein Toolkit-Steuerelement auf eine Seite ziehen, wenn Sie es verwenden möchten.

[![AJAX Control Toolkit wird in der Toolbox angezeigt](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**Abbildung 03**: AJAX Control Toolkit erscheint in toolbox([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)

Zuerst müssen Sie der Toolbox eine Registerkarte AJAX Control Toolkit hinzufügen. Führen Sie folgende Schritte durch:

1. Erstellen Sie eine neue ASP.NET Website, indem Sie die Menüoption Datei, Neue Website auswählen. Doppelklicken Sie im Projektmappen-Explorer auf Default.aspx, um die Datei im Editor zu öffnen.
2. Klicken Sie mit der rechten Maustaste auf die Toolbox unter der Registerkarte Allgemein und wählen Sie die Menüoption **Registerkarte Hinzufügen** aus (siehe Abbildung 4).
3. Geben Sie eine neue Registerkarte mit dem Namen AJAX Control Toolkit ein.

[![Hinzufügen einer neuen Registerkarte](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**Abbildung 04**: Hinzufügen einer neuen Registerkarte ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

Als Nächstes müssen Sie die AJAX Control Toolkit-Steuerelemente zur neuen Registerkarte hinzufügen. Führen Sie die folgenden Schritte aus:

- Klicken Sie mit der rechten Maustaste unter die Registerkarte AJAX Control Toolkit und wählen Sie die Menüoption **Elemente auswählen (siehe Abbildung 5)**.
- Navigieren Sie zu dem Speicherort, an dem Sie das AJAX Control Toolkit entpackt haben, und wählen Sie die AjaxControlToolkit.dll-Assembly aus.

[![Auswählen von Elementen, die der Toolbox hinzugefügt werden sollen](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**Abbildung 05**: Wählen Sie Elemente aus, die der Toolbox hinzugefügt werden sollen[(Klicken Sie hier, um das Bild in voller Größe anzuzeigen](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

Nachdem Sie diese Schritte ausgeführt haben, werden alle Toolkit-Steuerelemente in Der Toolbox angezeigt.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Upgrade auf eine neue Version des Toolkits

Wenn Sie eine ältere Version des Toolkits verwendet haben und nun zu einer späteren Version wechseln müssen, sind die folgenden Schritte die folgenden Schritte:

- Binärdateien - Löschen Sie die alte Version der AjaxControlToolkit.dll-Assembly aus Ihrem Ordner Bin-Ordner Ihrer Website.
- Toolbox-Elemente - Löschen Sie die Registerkarte AJAX Control Toolkit, und führen Sie die obigen Schritte aus, um die Registerkarte mit der neuen Version der AjaxControlToolkit.dll-Assembly neu zu erstellen.

> [!div class="step-by-step"]
> [Zurück](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [Weiter](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
