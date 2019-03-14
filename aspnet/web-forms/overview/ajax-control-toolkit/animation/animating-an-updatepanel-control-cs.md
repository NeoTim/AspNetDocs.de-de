---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Animieren eines UpdatePanel-Steuerelements (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Für den Inhalt einer...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3021da80635b8648d3119b939f2bdee77d858754
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026547"
---
<a name="animating-an-updatepanel-control-c"></a>Animieren eines UpdatePanel-Steuerelements (C#)
====================
durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Für den Inhalt von einem UpdatePanel-Steuerelement vorhanden ist, ein spezieller Extender, der stark auf die Animationsframework basiert: UpdatePanelAnimation. In diesem Tutorial veranschaulicht, wie Sie solche eine Animation für ein UpdatePanel einrichten.


## <a name="overview"></a>Übersicht

Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Für den Inhalt einer `UpdatePanel`, ein spezieller Extender vorhanden ist, die sehr auf die Animationsframework basiert: `UpdatePanelAnimation`. In diesem Tutorial wird gezeigt, wie solche eine Animation für Einrichten einer `UpdatePanel`.

## <a name="steps"></a>Schritte

Der erste Schritt ist wie üblich, enthalten die `ScriptManager` auf der Seite, damit die ASP.NET AJAX-Bibliothek geladen wird und das Steuerelement-Toolkit verwendet werden kann:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

Die Animation in diesem Szenario gelten für eine ASP.NET `Wizard` Websteuerelement Wohnsitz in einem `UpdatePanel`. Drei (beliebiger) Schritte stellen genügend Optionen zum Auslösen von Postbacks bereit:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

Das Markup für die `UpdatePanelAnimationExtender` Steuerelement ist sehr ähnlich, mit das Markup für die `AnimationExtender`. In der `TargetControlID` Attribut wir bieten die `ID` von der `UpdatePanel` animieren; innerhalb der `UpdatePanelAnimationExtender` -Steuerelement, die `<Animations>` -Element enthält XML-Markup für die Animation(s). Es gibt jedoch einen Unterschied: Die Größe der Ereignisse und Ereignishandler ist im Vergleich zur beschränkt `AnimationExtender`. Für `UpdatePanels`, nur zwei davon vorhanden:

- `<OnUpdated>` Wenn UpdatePanel aktualisiert wurde
- `<OnUpdating>` Beim Starten der UpdatePanel aktualisiert

In diesem Szenario wird der neue Inhalt, der die `UpdatePanel` (nach dem Postback) eingeblendet wird. Dies ist die notwendigen Markups dafür:

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

Nun, wenn ein Postback in UpdatePanel, was erfolgt, den neuen Inhalt des Bereichs reibungslos eingeblendet.


[![Der nächste Assistentenschritt wird eingeblendet,](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

Der nächste Assistentenschritt wird eingeblendet, ([klicken Sie, um das Bild in voller Größe anzeigen](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Zurück](changing-an-animation-using-client-side-code-cs.md)
> [Weiter](dynamically-controlling-updatepanel-animations-cs.md)
