---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: Deaktivieren von Aktionen während der Animation (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Darüber hinaus wird die Aktion unterstützt...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: 4315f06ea1599bacb93a23a3759610e19754cfba
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044347"
---
<a name="disabling-actions-during-animation-c"></a>Deaktivieren von Aktionen während einer Animation (C#)
====================
durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)

> Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Darüber hinaus werden die Aktionen, wie z.B. Mausklicks unterstützt. Beim Klicken mit der Maus eine Animation starten, ist es jedoch wünschenswert, Mausklicks während der Animation zu deaktivieren.


## <a name="overview"></a>Übersicht

Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Darüber hinaus werden die Aktionen, wie z.B. Mausklicks unterstützt. Beim Klicken mit der Maus eine Animation starten, ist es jedoch wünschenswert, Mausklicks während der Animation zu deaktivieren.

## <a name="steps"></a>Schritte

Zunächst einmal sind die `ScriptManager` in die Seite klicken Sie dann die ASP.NET AJAX-Bibliothek wird geladen, lässt sich das Steuerelement-Toolkit verwenden:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

Die Animation wird eine HTML-Schaltfläche wie folgt angewendet:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

Beachten Sie, dass ein HTML-Steuerelement statt eines Websteuerelements verwendet wird, da wir nicht, dass die Schaltfläche zum Erstellen eines Postbacks möchten. Sie müssen nur die clientseitige Animation für uns starten.

Fügen Sie dann die `AnimationExtender` auf der Seite Bereitstellen einer `ID`, `TargetControlID` -Attribut und das obligatorische `runat="server"`:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

In der `<Animations>` Knoten `<OnClick>` ist das richtige Element Mausklicks zu behandeln. Allerdings konnte die während der Animation auch gedrückt werden. Die `<EnableAction>` Element dieser kümmern. Festlegen von `Enabled="false"` deaktiviert die Schaltfläche mit den im Rahmen der Animation. Da wir mehrere einzelne Animationen (deaktivieren die Schaltfläche und die tatsächliche Animationen), verwenden die `<Parallel>` Element ist erforderlich, um die einzelnen Animationen zusammen in einer kleben. Hier ist das vollständige Markup für `AnimationExtender`:

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

Es wäre auch möglich, auf die Schaltfläche nach der Animation, verwenden das folgende XML-Element am Ende der Liste erneut zu aktivieren:

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

Aber im vorliegenden Szenario dies nutzlos seit der Schaltfläche wäre ausgeblendet wird, und ist nicht sichtbar ist, am Ende der Animation.


[![Die Schaltfläche ist deaktiviert, sobald die Animation ausgeführt wird](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)

Die Schaltfläche ist deaktiviert, sobald die Animation ausgeführt wird ([klicken Sie, um das Bild in voller Größe anzeigen](disabling-actions-during-animation-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Zurück](animating-in-response-to-user-interaction-cs.md)
> [Weiter](triggering-an-animation-in-another-control-cs.md)
