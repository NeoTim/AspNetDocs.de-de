---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: Verwenden von AJAX Control Toolkit Controls and Control Extenders (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie Ihren ASP.NET-Seiten AJAX Control Toolkit-Steuerelemente und Extender hinzufügen.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 129d6841bc4db62ecbe5f26c4830d1ce2f199bff
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540011"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>Verwenden von AJAX Control Toolkit-Steuerelementen und -Steuerelement-Extendern (VB)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie Ihren ASP.NET-Seiten AJAX Control Toolkit-Steuerelemente und Extender hinzufügen.

Das AJAX Control Toolkit enthält eine Reihe von Steuerelementen und Steuerelementerweiterungen. In diesem kurzen Tutorial erfahren Sie, wie Sie einer ASP.NET Seite sowohl Steuerelemente als auch Steuerelementerweiterungen hinzufügen.

> [!NOTE] 
> 
> Anweisungen zum Installieren des AJAX Control Toolkits und zum Hinzufügen des AJAX Control Toolkits zur Visual Studio/Visual Web Developer-Toolbox finden Sie im Tutorial [Erste Schritte mit dem AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).

## <a name="using-ajax-control-toolkit-controls"></a>Verwenden von AJAX Control Toolkit-Steuerelementen

Ein AJAX Control Toolkit-Steuerelement funktioniert wie ein normales ASP.NET-Steuerelement. Sie können das Steuerelement aus der Toolbox auf eine ASP.NET Seite ziehen. Sie können das Steuerelement der Seite entweder in der Entwurfsansicht oder in der Quellansicht hinzufügen.

Bei der Verwendung der Steuerelemente aus dem AJAX Control Toolkit gibt es eine besondere Anforderung. Die Seite muss ein ScriptManager-Steuerelement enthalten. Das ScriptManager-Steuerelement ist für die Einbeziehung aller erforderlichen JavaScript-Elemente verantwortlich, die für die AJAX Control Toolkit-Steuerelemente erforderlich sind.

Die Registerkarte AJAX Control Toolkit enthält z. B. ein Steuerelement mit dem Namen Editor-Steuerelement. Dieses Steuerelement zeigt einen rich HTML-Editor an. Führen Sie die folgenden Schritte aus, um das Editor-Steuerelement zu einer Seite hinzuzufügen:

1. Erstellen einer neuen ASP.NET Seite mit dem Namen ShowEditor.aspx
2. Wählen Sie das ScriptManager-Steuerelement unter der Registerkarte AJAX-Erweiterungen in der Toolbox aus, und ziehen Sie das Steuerelement auf die Seite.
3. Wählen Sie das Editor-Steuerelement unter der Registerkarte AJAX Control Toolkit in der Toolbox aus, und ziehen Sie das Steuerelement auf die Seite (siehe Abbildung 1). Der Designer sollte wie Abbildung 2 aussehen.
4. Führen Sie die Website aus, indem Sie die Menüoption **Debuggen, Debuggen starten** oder die F5-Taste drücken.
5. Sie sollten die Seite in Abbildung 3 sehen.

[![Auswählen des HTML-Editor-Steuerelements](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Abbildung 01**: Auswählen des HTML-Editor-Steuerelements ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))

[![Visual Studio Designer mit ScriptManager- und Edit-Steuerelement](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Abbildung 02**: Visual Studio Designer mit ScriptManager und Edit-Steuerelement ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))

[![Die Seite DisplayEditor.aspx](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Abbildung 03**: Die Seite DisplayEditor.aspx([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>Verwenden von AJAX Control Toolkit Control Extendern

Das AJAX Control Toolkit enthält auch Steuerelement-Extender. Wie der Name schon sagt, erweitert ein Steuerelement-Extender die Funktionalität eines vorhandenen Steuerelements. Der ConfirmButton-Steuerelement-Extender erweitert beispielsweise die Standard-ASP.NET-Schaltflächensteuerung. Der Extender ändert das Verhalten des Schaltflächensteuerelements, sodass die Schaltfläche beim Klicken darauf ein Bestätigungsdialogfeld anzeigt.

Ein Control Extender erfordert genau wie ein AJAX Control Toolkit-Steuerelement ein ScriptManager-Steuerelement. Sie müssen einer Seite ein ScriptManager-Steuerelement hinzufügen, bevor Sie mit der Verwendung von Steuerelementerweiterungen auf der Seite beginnen.

Führen Sie die folgenden Schritte aus, um den ConfirmButton-Steuerelement-Extender zu verwenden:

1. Erstellen einer neuen ASP.NET Seite mit dem Namen ShowConfirmButton.aspx
2. Fügen Sie der Seite ein ScriptManager-Steuerelement hinzu, indem Sie das Steuerelement auf die Seite unter der Registerkarte AJAX-Erweiterungen ziehen.
3. Fügen Sie der Seite ein Standard-Schaltflächensteuerelement hinzu, indem Sie die Schaltfläche unter der Registerkarte Standard in der Toolbox auf die Designer-Oberfläche ziehen.
4. Klicken Sie auf die Option **Extender hinzufügen** (siehe Abbildung 4).
5. Wählen Sie im Dialogfeld Extender auswählen die Option ConfirmButtonExtender (siehe Abbildung 5) aus, und klicken Sie auf die Schaltfläche OK.
6. Wählen Sie das Schaltflächensteuerelement im Designer aus,\_und erweitern Sie den Knoten Extender, Button1 ConfirmButtonExtender im Eigenschaftenfenster (siehe Abbildung 6). Weisen Sie den Wert *Really?* der ConfirmText-Eigenschaft zu.
7. Führen Sie die Seite aus, indem Sie die Menüoption **Debuggen, Debuggen starten** oder die F5-Taste drücken.

[![Die Option Extender hinzufügen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Abbildung 04**: Die Option Extender hinzufügen ([Klicken Sie darauf, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))

[![Auswählen des ConfirmButton-Steuerelement-Extenders](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**Abbildung 05**: Auswählen des ConfirmButton-Steuerelement-Extenders ([Klicken Sie hier, um ein Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))

[![Festlegen einer ConfirmButton-Eigenschaft](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Abbildung 06**: Festlegen einer[ConfirmButton-Eigenschaft (Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))

Wenn die Seite geöffnet wird, sollte eine Schaltfläche angezeigt werden. Wenn Sie auf die Schaltfläche klicken, erhalten Sie das Bestätigungsdialogfeld in Abbildung 7.

[![Anzeigen des Bestätigungsdialogs](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**Abbildung 07**: Anzeigen des Bestätigungsdialogs([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))

Beachten Sie, dass Sie normalerweise keinen Steuerelement-Extender auf eine Seite ziehen. Stattdessen verwenden Sie die Option **Erweiterung hinzufügen,** um einem Steuerelement, das Sie einer Seite bereits hinzugefügt haben, einen Extender hinzuzufügen. Beachten Sie außerdem, dass Sie Steuerelement-Extender-Eigenschaften festlegen, indem Sie das Eigenschaftenblatt für das zu erweiternde Steuerelement öffnen.

Ein einzelnes ASP.NET-Steuerelement kann um mehrere Steuerungs-Extender erweitert werden. Das Eigenschaftenblatt für das zu erweiternde Steuerelement listet alle dem Steuerelement zugeordneten Steuerelementerweiterungen auf.

> [!div class="step-by-step"]
> [Zurück](get-started-with-the-ajax-control-toolkit-vb.md)
> [Weiter](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
