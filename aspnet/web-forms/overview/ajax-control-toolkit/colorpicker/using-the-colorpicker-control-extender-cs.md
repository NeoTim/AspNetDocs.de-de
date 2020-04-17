---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: Verwenden des ColorPicker Control Extenders (C) | Microsoft Docs
author: rick-anderson
description: ColorPicker ist ein ASP.NET AJAX-Extender, der clientseitige Farbauswahlfunktionen mit Benutzeroberfläche in einem Popup-Steuerelement bereitstellt. Es kann an jedem ASP.NET angebracht werden...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 63b6bc58d36fdfcb5ee0a1c97988091e8d35505b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543131"
---
# <a name="using-the-colorpicker-control-extender-c"></a>Verwenden des ColorPicker Control Extenders (C-Wert)

von [Microsoft](https://github.com/microsoft)

> ColorPicker ist ein ASP.NET AJAX-Extender, der clientseitige Farbauswahlfunktionen mit Benutzeroberfläche in einem Popup-Steuerelement bereitstellt. Es kann an jede ASP.NET TextBox-Steuerelement sangehängt werden. Es.

Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie den AJAX Control Toolkit ColorPicker-Steuerelement-Extender verwenden können. Der ColorPicker-Steuerelement-Extender zeigt ein Popup-Dialogfeld an, in dem Sie eine Farbe auswählen können. Der ColorPicker ist immer dann nützlich, wenn Sie eine intuitive Benutzeroberfläche für die Auswahl einer Farbe bereitstellen möchten.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>Erweitern eines TextBox-Steuerelements mit dem ColorPicker Control Extender

Stellen Sie sich beispielsweise vor, dass Sie eine Website erstellen möchten, die es Besuchern ermöglicht, benutzerdefinierte Visitenkarten zu erstellen. Besucher können den Text für eine Visitenkarte eingeben und die Farbe auswählen. Die ASP.NET Seite in Liste 1 enthält zwei TextBox-Steuerelemente mit dem Namen txtCardText und txtCardColor. Wenn Sie das Formular absenden, werden die ausgewählten Werte angezeigt (siehe Abbildung 1).

[![Einfaches Formular zum Erstellen einer Visitenkarte](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**Abbildung 01**: Einfaches Formular zum Erstellen einer Visitenkarte ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-the-colorpicker-control-extender-cs/_static/image2.png)

**Auflistung 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

Das Formular in Listing 1 funktioniert, bietet aber keine großartige Benutzererfahrung. Der Benutzer muss eine Farbe in das Textfeld eingeben. Wenn der Benutzer eine spezielle Farbe - zum Beispiel genau die richtige Schattierung von Erbsengrün - will, dann muss der Benutzer den HTML-Farbcode ohne Hilfe herausfinden.

Sie können den ColorPicker-Steuerelement-Extender verwenden, um eine bessere Benutzererfahrung zu erstellen. Der ColorPicker zeigt ein Farbdialogfeld an, wenn Sie den Fokus auf ein TextBox-Steuerelement verschieben (siehe Abbildung 2).

[![Der ColorPicker Control Extender](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**Abbildung 02**: Der ColorPicker Control Extender ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-the-colorpicker-control-extender-cs/_static/image4.png))

Sie müssen zwei Schritte ausführen, um den ColorPicker-Steuerelement-Extender mit dem Formular in Liste 1 zu verwenden:

1. Hinzufügen eines ScriptManager-Steuerelements zur Seite
2. Hinzufügen des ColorPicker-Steuerelement-Extenders zur Seite

Bevor Sie den ColorPicker verwenden können, müssen Sie Ihrer Seite einen ScriptManager hinzufügen. Ein guter Ort, um den ScriptManager hinzuzufügen, &lt;&gt; befindet sich direkt unter dem öffnenden serverseitigen Formulartag. Sie können den ScriptManager aus der Toolbox auf die Seite ziehen (der ScriptManager befindet sich unter der Registerkarte AJAX-Erweiterungen). Alternativ können Sie das folgende Tag in die Quellansicht unter dem öffnenden serverseitigen Formulartag eingeben:

&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;

Die einfachste Möglichkeit, den ColorPicker-Steuerelement-Extender zur Seite hinzuzufügen, ist in der Entwurfsansicht. Wenn Sie den Mauszeiger über die txtCardColor TextBox bewegen, wird eine smarte Task-Option angezeigt, mit der Sie einen Extender hinzufügen können (siehe Abbildung 3). Wenn Sie diese Option auswählen, wird der Extender-Assistent angezeigt (siehe Abbildung 4).

[![Hinzufügen eines Extenders](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**Abbildung 03**: Hinzufügen eines Extenders[(Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-the-colorpicker-control-extender-cs/_static/image6.png))

[![Auswählen eines Steuerelement-Extenders mit dem Extender-Assistenten](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**Abbildung 04**: Auswählen eines Steuerelement-Extenders mit dem Extender-Assistenten ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-the-colorpicker-control-extender-cs/_static/image8.png))

Sie können den ColorPicker-Extender auswählen, um die txtCardColor TextBox mit dem ColorPicker-Extender zu erweitern. Klicken Sie auf OK, um das Dialogfeld zu schließen.

Nachdem Sie diese Änderungen vorgenommen haben, sieht die Quelle für die Seite wie Liste 2 aus.

Eintrag 2 - CreateCard.aspx (mit ColorPicker)

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

Beachten Sie, dass die Seite jetzt ein ColorPickerExtender-Steuerelement enthält, das direkt unter dem txtCardColor TextBox-Steuerelement angezeigt wird. Das ColorPickerExtender-Steuerelement erweitert das txtCardColor-Steuerelement, sodass ein Farbauswahldialog angezeigt wird.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Verwenden einer Schaltfläche zum Starten des Farbauswahldialogs

Der ColorPicker-Extender unterstützt die folgenden Eigenschaften:

- PopupButtonId - Die ID einer Schaltfläche auf der Seite, die bewirkt, dass das Farbauswahldialogfeld angezeigt wird.
- PopupPosition - Die Position des Farbauswahldialogs relativ zum Zielsteuerelement. Mögliche Werte sind Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right und Left (Standardistwert ist BottomLeft).
- SampleControlId - Die ID eines Steuerelements, das die ausgewählte Farbe anzeigt.
- SelectedColor - Die vom ColorPicker ausgewählte Anfangsfarbe.

Mit diesen Eigenschaften können Sie anpassen, wie das Farbauswahldialogfeld angezeigt und die ausgewählte Farbe angezeigt wird. Die Seite in Liste 3 veranschaulicht, wie Sie mehrere dieser Eigenschaften verwenden können.

**Eintrag 3 - CreateCardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

Die Seite in Liste 3 enthält eine Schaltfläche Farbe auswählen (siehe Abbildung 5). Wenn Sie auf diese Schaltfläche klicken, wird das Farbauswahldialogfeld über der TextBox angezeigt. Wenn Sie eine Farbe aus dem Dialogfeld auswählen, wird die ausgewählte Farbe als Hintergrundfarbe des lblSample-Beschriftungssteuerelements angezeigt.

Die ColorPicker PopupButtonID-Eigenschaft wird verwendet, um die Schaltfläche Farbe auswählen dem ColorPicker-Extender zuzuordnen. Wenn Sie einen Wert für die PopupButtonID-Eigenschaft angeben, wird das Farbauswahldialogfeld nicht mehr angezeigt, wenn das Zielsteuerelement den Fokus hat. Sie müssen auf die Schaltfläche klicken, um das Dialogfeld anzuzeigen.

Die SampleControlID-Eigenschaft wird verwendet, um dem ColorPicker ein Steuerelement zuzuordnen, das die ausgewählte Farbe anzeigt. Der ColorPicker ändert die Hintergrundfarbe dieses Steuerelements in die aktuell ausgewählte Farbe.

[![Anzeigen des Farbauswahldialogs mit einer Schaltfläche](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**Abbildung 05**: Anzeigen des Farbauswahldialogs mit einer Schaltfläche ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-the-colorpicker-control-extender-cs/_static/image10.png)

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie gelernt, wie Sie den ColorPicker-Steuerelement-Extender verwenden, um ein Popup-Farbauswahldialogfeld anzuzeigen. Zuerst haben wir untersucht, wie Sie das Dialogfeld anzeigen können, wenn der Fokus in ein TextBox-Steuerelement verschoben wird. Als Nächstes haben Sie gelernt, wie Sie eine Schaltfläche erstellen, die das Farbauswahldialogfeld anzeigt, wenn auf die Schaltfläche geklickt wird.

> [!div class="step-by-step"]
> [Nächste](using-the-colorpicker-control-extender-vb.md)
