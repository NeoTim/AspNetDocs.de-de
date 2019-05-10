---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: Auswählen einer Animation aus einer Liste (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Das Framework auch zulassen...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: dd22d80775ebe3571fcf9d3225135766669ef85b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128717"
---
# <a name="picking-one-animation-out-of-a-list-c"></a>Auswählen einer Animation aus einer Liste (C#)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Das Framework ermöglicht es auch den Programmierer, wählen Sie eine Animation aus einer Liste von Animationen, je nach der Auswertung von JavaScript-Code.

## <a name="overview"></a>Übersicht

Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Das Framework ermöglicht es auch den Programmierer, wählen Sie eine Animation aus einer Liste von Animationen, je nach der Auswertung von JavaScript-Code.

## <a name="steps"></a>Schritte

Zunächst einmal sind die `ScriptManager` in die Seite klicken Sie dann die ASP.NET AJAX-Bibliothek wird geladen, lässt sich das Steuerelement-Toolkit verwenden:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

Die Animation wird auf einen Bereich des Texts angewendet werden, der so aussieht:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

Definieren Sie in der zugehörigen CSS-Klasse für den Bereich eine gute Hintergrundfarbe aus, und auch festlegen Sie eine feste Breite für den Bereich:

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

Fügen Sie dann die `AnimationExtender` auf der Seite Bereitstellen einer `ID`, `TargetControlID` -Attribut und das obligatorische `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

In der `<Animations>` Knoten verwenden `<OnLoad>` die Animationen ausgeführt werden, nachdem die Seite vollständig geladen wurde. Statt in einem regulären-Animationen die `<Case>` Element ins Spiel. Der Wert seines Attributs SelectScript wird ausgewertet; der Rückgabewert muss numerische sein. Je nach dieser Anzahl, eines der Subanimation in &lt;Fall&gt; ausgeführt wird. Wenn SelectScript 2 ergibt, führt das Steuerelement-Toolkit z. B. dritte Animation in &lt;Fall&gt; (Zählung von 0 beginnt).

Das folgende Markup definiert drei Subanimation: Ändern der Größe der Breite und ausgeblendet wird, ändern Sie die Höhe der Größe. Der JavaScript-Code (`Math.floor(3 * Math.random())`) wählt anschließend eine Zahl zwischen 0 und 2, sodass einer der drei Animationen ausgeführt wird:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

[![Eine der drei möglichen Animationen: Ruft der Bereich ab, größere](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

Eine der drei möglichen Animationen: Ruft der Bereich ab, größere ([klicken Sie, um das Bild in voller Größe anzeigen](picking-one-animation-out-of-a-list-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Zurück](animation-depending-on-a-condition-cs.md)
> [Weiter](animating-in-response-to-user-interaction-cs.md)
