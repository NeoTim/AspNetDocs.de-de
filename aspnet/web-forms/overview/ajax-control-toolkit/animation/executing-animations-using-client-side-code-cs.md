---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: Ausführen von Animationen mit clientseitigen Code (c#) | Microsoft-Dokumentation
author: wenz
description: Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Die Ausführung der Animation...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 23727e8f34afdd073b21aa1e7381237c48e699c4
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132720"
---
# <a name="executing-animations-using-client-side-code-c"></a>Ausführen von Animationen mit clientseitigem Code (C#)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)

> Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Die Ausführung der Animation kann auch mit benutzerdefinierte clientseitige JavaScript-Code ausgelöst werden.

## <a name="overview"></a>Übersicht

Die Animation-Steuerelement in ASP.NET AJAX Control Toolkit ist nicht nur ein Steuerelement, aber ein ganzes Framework Animationen an ein Steuerelement hinzufügen. Die Ausführung der Animation kann auch mit benutzerdefinierte clientseitige JavaScript-Code ausgelöst werden.

## <a name="steps"></a>Schritte

Zunächst einmal sind die `ScriptManager` in die Seite klicken Sie dann die ASP.NET AJAX-Bibliothek wird geladen, lässt sich das Steuerelement-Toolkit verwenden:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

Die Animation wird auf einen Bereich des Texts angewendet werden, der so aussieht:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

Definieren Sie in der zugehörigen CSS-Klasse für den Bereich eine gute Hintergrundfarbe aus, und auch festlegen Sie eine feste Breite für den Bereich:

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

Fügen Sie dann die `AnimationExtender` auf der Seite Bereitstellen einer `ID`, `TargetControlID` -Attribut und das obligatorische `runat="server"`:

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

In der `<Animations>` Knoten verwenden `<OnClick>` klickt Sie auf den Animationen nach dem Benutzer ausgeführt werden im Bereich. Fügen Sie zwei Animationen, die parallel ausgeführt werden:

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

Die Zwecke dieser Demo werden dieser Animation (und alle anderen Animationen erstellt, mit dem Steuerelement-Toolkit) ausgeführt mithilfe von JavaScript-Code, sobald die Seite ausgeführt wird. Zunächst einmal benötigen wir Zugriff auf die `AnimationExtender` Steuerelement. Die ASP.NET AJAX-Bibliothek stellt die `$find()` -Funktion für diese Aufgabe:

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

Die `AnimationExtender` Steuerelement stellt eine umfangreiche API, einschließlich der Methoden mit Namen, die identisch mit die Ereignishandler, die in das XML-Markup verwendet: `OnClick()`, `OnLoad()`und so weiter. Z. B. einen Aufruf von der `OnClick()` Methode führt die Animation innerhalb der `<OnClick>` Element der `AnimationExtender` Steuerelement:

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

Hier ist der vollständige clientseitige JavaScript-Code, der dem Klicken auf den Bereich emuliert, sobald die Seite vollständig geladen wurde Beachten Sie, dass die `pageLoad()` Funktionsnamen wird verwendet, die von ASP.NET AJAX nach der Seite aufgerufen wird und alle enthaltenen JavaScript-Bibliotheken wurden geladen.

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

[![Die Animation wird sofort ohne ein Mausklick ausgeführt.](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)

Die Animation wird sofort ausgeführt, ohne ein Mausklick ([klicken Sie, um das Bild in voller Größe anzeigen](executing-animations-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Zurück](modifying-animations-from-the-server-side-cs.md)
> [Weiter](changing-an-animation-using-client-side-code-cs.md)
