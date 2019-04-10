---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Mithilfe von AJAX Control Toolkit-Steuerelementen und Steuerelement-Extendern (c#) | Microsoft-Dokumentation
author: microsoft
description: Erfahren Sie, wie ASP.NET-Seiten AJAX Control Toolkit-Steuerelemente und Extender hinzugefügt.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 82fae91e40ec2f1508fe5c82992eeef4abc4e19a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419222"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Verwenden von AJAX Control Toolkit-Steuerelementen und -Steuerelement-Extendern (C#)

by [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie ASP.NET-Seiten AJAX Control Toolkit-Steuerelemente und Extender hinzugefügt.


Das AJAX Control Toolkit enthält eine Reihe von Steuerelementen und Steuerelement-Extendern. In diesem kurzen Tutorial erfahren Sie, wie Steuerelemente und Extender hinzuzufügen, zu einer ASP.NET-Seite.

> [!NOTE] 
> 
> Anweisungen zum Installieren von AJAX Control Toolkit, und Hinzufügen von AJAX Control Toolkit zur Toolbox Visual Studio/Visual Web Developer, finden Sie im Tutorial [erste Schritte mit dem AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).


## <a name="using-ajax-control-toolkit-controls"></a>Mithilfe von AJAX Control Toolkit-Steuerelementen

Ein AJAX Control Toolkit-Steuerelement funktioniert genauso wie ein normaler ASP.NET-Steuerelement. Sie können das Steuerelement aus der Toolbox auf einer ASP.NET-Seite ziehen. Sie können das Steuerelement auf der Seite in der Entwurfsansicht oder die Datenquellensicht hinzufügen.

Es ist eine spezielle Anforderung, bei der Verwendung der Steuerelemente aus dem AJAX Control Toolkit. Die Seite muss ein ScriptManager-Steuerelement enthalten. Das ScriptManager-Steuerelement ist dafür verantwortlich, alle notwendigen JavaScript das AJAX Control Toolkit-Steuerelemente erforderlich ist.

Die Registerkarte "AJAX Control Toolkit" enthält beispielsweise ein Steuerelement mit dem Namen der Editor-Steuerelement. Dieses Steuerelement zeigt einen umfassenden HTML-Editor. Um das Editor-Steuerelement zu einer Seite hinzufügen, gehen Sie wie folgt vor:

1. Erstellen Sie eine neue ASP.NET-Seite mit dem Namen ShowEditor.aspx
2. Wählen Sie das ScriptManager-Steuerelement vom der Registerkarte "AJAX-Erweiterungen" in der Toolbox, und ziehen Sie das Steuerelement auf der Seite.
3. Wählen Sie die Editor-Steuerelement vom dem AJAX Control Toolkit-Registerkarte in der Toolbox, und ziehen Sie das Steuerelement auf der Seite (siehe Abbildung 1). Der Designer sollte wie in Abbildung 2 aussehen.
4. Führen Sie die Website, indem Sie durch Auswählen der Menüoption **Debuggen, Debugging starten** oder F5 drücken.
5. Die Seite in Abbildung 3 sollte angezeigt werden.


[![SWahl das Steuerelement der HTML-Editor](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Abbildung 01**: Auswählen des HTML-Editor-Steuerelements ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))


[![VIsual Studio-Designer mit ScriptManager "und" Bearbeiten-Steuerelement](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Abbildung 02**: Visual Studio-Designer mit ScriptManager "und" Bearbeiten-Steuerelement ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))


[![THE DisplayEditor.aspx Page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Abbildung 03**: Die Seite "DisplayEditor.aspx" ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>Mithilfe von AJAX Control Toolkit-Steuerelement-Extendern

Das AJAX Control Toolkit enthält auch die Steuerelement-Extendern. Wie der Name schon sagt, wird ein Extender-Steuerelements die Funktionalität eines vorhandenen Steuerelements erweitert. Beispielsweise erweitert einen ConfirmButton-Extender-Steuerelement das standardmäßige ASP.NET Schaltflächen-Steuerelement. Der Extender ändert das Verhalten des Schaltfläche Steuerelements s, damit die Schaltfläche ein Bestätigungsdialogfeld angezeigt, wenn Sie darauf klicken.

Ein Extender-Steuerelements, wie ein AJAX Control Toolkit-Steuerelement erfordert ein ScriptManager-Steuerelement. Sie müssen ein ScriptManager-Steuerelement zu einer Seite hinzufügen, bevor Sie Steuerelement-Extendern auf der Seite verwenden.

Um einen ConfirmButton-Extender-Steuerelement verwenden, gehen Sie wie folgt vor:

1. Erstellen Sie eine neue ASP.NET-Seite mit dem Namen ShowConfirmButton.aspx
2. Fügen Sie ein ScriptManager-Steuerelement auf der Seite durch Ziehen des Steuerelements auf der Seite vom der Registerkarte "AJAX-Erweiterungen".
3. Fügen Sie eine standardmäßige Schaltflächen-Steuerelement auf der Seite vom die Registerkarte "Standard" die Schaltfläche mit den in der Toolbox auf die Entwurfsoberfläche ziehen.
4. Klicken Sie auf die **Extender hinzufügen** aufgabenoption (siehe Abbildung 4).
5. Wählen Sie im Dialogfeld für die auswählen-Extender ConfirmButtonExtender (siehe Abbildung 5), und klicken Sie auf die Schaltfläche "OK".
6. Wählen Sie das Schaltflächen-Steuerelement im Designer, und erweitern Sie den Extender, "Button1"\_ConfirmButtonExtender-Knotens im Eigenschaftenfenster (siehe Abbildung 6). Weisen Sie den Wert *wirklich?* der ConfirmText-Eigenschaft.
7. Führen Sie die Seite im Menü die Option **Debuggen, Debugging starten** oder die F5-Taste drücken.


[![Ter registerkartenoption Extender hinzufügen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Abbildung 04**: Die registerkartenoption Extender hinzufügen ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))


[![SWahl des ConfirmButton-Extenders-Steuerelements](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Abbildung 05**: Auswählen des ConfirmButton-Extenders-Steuerelements ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))


[![SSkala-Einstellung einer Eigenschaft ConfirmButton-Steuerelements](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Abbildung 06**: Festlegen einer Eigenschaft ConfirmButton-Steuerelements ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))


Wenn die Seite geöffnet wird, sollte eine Schaltfläche angezeigt werden. Wenn Sie die Schaltfläche klicken, erhalten Sie im Bestätigungsdialogfeld in Abbildung 7.


[![DDas Dialogfeld "Bestätigung" IsPlaying den Wert](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Abbildung 07**: Das Dialogfeld "Bestätigung" angezeigt ([klicken Sie, um das Bild in voller Größe anzeigen](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))


Beachten Sie, dass Sie normalerweise nicht den einen Extender-Steuerelements auf einer Seite ziehen. Verwenden Sie stattdessen die **Extender hinzufügen** aufgabenoption Extender an ein Steuerelement hinzufügen, die Sie bereits zu einer Seite hinzugefügt haben. Beachten Sie außerdem, dass Sie Control Extender-Eigenschaften festzulegen, öffnen das Eigenschaftenblatt für das Steuerelement erweitert wird.

Ein einzelnes ASP.NET-Steuerelement kann durch mehrere Steuerelement-Extendern erweitert werden. Das Eigenschaftenblatt für das Steuerelement erweitert wird, werden alle der Steuerelement-Extendern, die dem Steuerelement zugeordnete aufgelistet.

> [!div class="step-by-step"]
> [Zurück](get-started-with-the-ajax-control-toolkit-cs.md)
> [Weiter](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
