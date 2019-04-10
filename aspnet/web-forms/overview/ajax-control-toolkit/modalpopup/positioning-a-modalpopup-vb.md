---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: Positionieren eines ModalPopup-Steuerelements (VB) | Microsoft-Dokumentation
author: wenz
description: Der ModalPopup-Steuerelement im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein modales Fenster mithilfe der clientseitigen Methoden zu erstellen. Das Steuerelement jedoch keine bietet ein...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: e37d2f4450c697f963d954c2fbb58e3ed20a1566
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421146"
---
# <a name="positioning-a-modalpopup-vb"></a>Positionieren eines ModalPopup-Steuerelements (VB)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> Der ModalPopup-Steuerelement im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein modales Fenster mithilfe der clientseitigen Methoden zu erstellen. Das Steuerelement bietet jedoch keine integrierte Funktionen, die das Popup zu positionieren.


## <a name="overview"></a>Übersicht

Der ModalPopup-Steuerelement im AJAX Control Toolkit bietet eine einfache Möglichkeit, ein modales Fenster mithilfe der clientseitigen Methoden zu erstellen. Das Steuerelement bietet jedoch keine integrierte Funktionen, die das Popup zu positionieren.

## <a name="steps"></a>Schritte

Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager`. Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

Fügen Sie einen Bereich, der als modales Fenster dient. Eine Schaltfläche wird verwendet, um das Popup zu schließen:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

Wenn das Popup angezeigt wird, müssen sie an einer bestimmten Stelle auf der Seite angeordnet sein. Für diese Aufgabe wird eine clientseitige JavaScript-Funktion erstellt. Zuerst wird versucht, die dem Zugriffsbereich. Wenn dies gelingt, ist des Bereichs Position festgelegt mithilfe von CSS und JavaScript (Änderung, die die Position des Popupfensters am wird). Jedoch `ModalPopupExtender` Steuerelement außerdem versucht wird, um das Popup zu positionieren. Aus diesem Grund wird der JavaScript-Code Popupfenster jeder Zehntel Sekunde wiederholt positioniert.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

Wie Sie sehen können, den Rückgabewert der `setTimeout()` JavaScript-Methode wird in einer globalen Variablen gespeichert. Auf diese Weise beenden, die wiederholte Positionierung des Popups bei Bedarf kann mithilfe der `clearTimeout()` Methode:

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

Nun müssen lediglich um den Browser, rufen diese Funktionen an, wo immer möglich zu machen. Die `movePanel()` JavaScript-Funktion muss aufgerufen werden, wenn die Schaltfläche geklickt wird, die den Bereich auslöst:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

Und die `stopMoving()` Funktion ins Spiel, wenn das Popup kann geschlossen wird ausgelöst, der `ModalPopupExtender` Steuerelement:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]


[![THE modales Fenster angezeigt wird, an der angegebenen Position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

Die modales Fenster angezeigt wird, an der angegebenen Position ([klicken Sie, um das Bild in voller Größe anzeigen](positioning-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Vorheriges](handling-postbacks-from-a-modalpopup-vb.md)
