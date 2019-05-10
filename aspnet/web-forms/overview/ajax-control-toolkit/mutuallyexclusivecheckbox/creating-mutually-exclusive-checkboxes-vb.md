---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: Erstellen von sich gegenseitig ausschließenden Kontrollkästchen (VB) | Microsoft-Dokumentation
author: wenz
description: 'Wenn nur eine der Optionen ausgewählt werden kann, werden die Optionsfelder in der Regel verwendet. Es gibt jedoch ein Nachteil: Sobald ein Optionsfeld in einer Gruppe ausgewählt ist...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 5bf96cf287f2fe5f394449587c70d9fc6fb33af9
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132552"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>Erstellen von sich gegenseitig ausschließenden Kontrollkästchen (VB)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> Wenn nur eine der Optionen ausgewählt werden kann, werden die Optionsfelder in der Regel verwendet. Es gibt jedoch ein Nachteil: Sobald in einer Gruppe ein Optionsfeld ausgewählt ist, ist es nicht möglich, alle Optionsfelder deaktiviert. Kontrollkästchen kann jederzeit deaktiviert werden, jedoch sind nicht gegenseitig. In diesem Tutorial werden die Vorteile beider Ansätze: Kontrollkästchen, die sich gegenseitig.

## <a name="overview"></a>Übersicht

Wenn nur eine der Optionen ausgewählt werden kann, werden die Optionsfelder in der Regel verwendet. Es gibt jedoch ein Nachteil: Sobald in einer Gruppe ein Optionsfeld ausgewählt ist, ist es nicht möglich, alle Optionsfelder deaktiviert. Kontrollkästchen kann jederzeit deaktiviert werden, jedoch sind nicht gegenseitig. In diesem Tutorial werden die Vorteile beider Ansätze: Kontrollkästchen, die sich gegenseitig.

## <a name="steps"></a>Schritte

Das ASP.NET AJAX Control Toolkit enthält die MutuallyExclusiveCheckBox-Extender. Programmierer, der Name einer Gruppe alle Kontrollkästchen zuweisen können (`Key` Attribut). Aus alle Kontrollkästchen in der gleichen Gruppe kann nur eine gleichzeitig ausgewählt werden.

Wir beginnen mit zwei Kontrollkästchen in eine neue ASP.NET-Seite zu platzieren. Es können mehrere, aber zwei reicht aus, um das Prinzip zu demonstrieren:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

Für beide Kontrollkästchen muss ein MutuallyExclusiveCheckBoxExtender-Steuerelement auf der Seite eingefügt werden. Beide Schlüsselattribute müssen den gleichen Wert wie der Wert sich Attribute eines HTML-Radio Button-Elemente befinden, müssen identisch mit die Gruppe zu bezeichnen, in der sie angehören. Die TargetControlID-Eigenschaft des Extenders verweist auf die ID des Kontrollkästchens.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

Darüber hinaus enthalten die ASP.NET AJAX `ScriptManager` die alle Elemente des ASP.NET AJAX Control Toolkit erforderlich ist:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

Speichern Sie, und führen Sie die Seite: Sie aktivieren und deaktivieren Sie beide Kontrollkästchen, können jedoch zu keinem Zeitpunkt beide Kontrollkästchen geprüft werden kann.

[![Nur ein Kontrollkästchen kann zu einem Zeitpunkt überprüft werden](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

Nur ein Kontrollkästchen kann zu einem Zeitpunkt überprüft werden ([klicken Sie, um das Bild in voller Größe anzeigen](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Vorherige](creating-mutually-exclusive-checkboxes-cs.md)
