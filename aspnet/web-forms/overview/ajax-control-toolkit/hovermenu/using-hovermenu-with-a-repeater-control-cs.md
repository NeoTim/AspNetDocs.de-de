---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Verwenden von HoverMenu mit einem Wiederholungssteuerelement (c#) | Microsoft-Dokumentation
author: wenz
description: 'Der HoverMenu-Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an eine speziell...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f64e90eb2f8f87e2f382cb7897793e7071d305d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384499"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>Verwenden von HoverMenu mit einem Wiederholungssteuerelement (C#)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> Der HoverMenu-Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an der angegebenen Position. Es ist auch möglich, dieses Steuerelement in einem wiederholungssteuerelement zu verwenden.


## <a name="overview"></a>Übersicht

Die `HoverMenu` Steuerelement im AJAX Control Toolkit bietet eine einfache Popup Auswirkung: Wenn der Mauszeiger über einem Element bewegt wird ein Popupfenster angezeigt wird, an der angegebenen Position. Es ist auch möglich, dieses Steuerelement in einem wiederholungssteuerelement zu verwenden.

## <a name="steps"></a>Schritte

Zunächst einmal ist eine Datenquelle erforderlich. Dieses Beispiel verwendet die AdventureWorks-Datenbank und die Microsoft SQL Server 2005 Express Edition. Die Datenbank ist eine optionale Komponente von einer Visual Studio-Installation (einschließlich express Edition) und steht auch als separater Download unter [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Die AdventureWorks-Datenbank ist Teil der SQL Server 2005 Samples and Sample Databases (download unter [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Die einfachste Möglichkeit zum Einrichten der Datenbank ist die Verwendung der Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = En](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) und fügen Sie der `AdventureWorks.mdf` Datenbankdatei.

In diesem Beispiel wird angenommen, dass, dass Sie die Instanz von SQL Server 2005 Express Edition aufgerufen wird `SQLEXPRESS` und befindet sich auf dem gleichen Computer wie der Webserver; Dies ist auch der standardeinrichtung. Wenn Ihr Setup unterscheidet, müssen Sie die Verbindungsinformationen für die Datenbank anpassen.

Um die Funktionalität von ASP.NET AJAX und das Steuerelement-Toolkit, aktivieren die `ScriptManager` Steuerelement an einer beliebigen Stelle auf der Seite platziert werden muss (jedoch innerhalb der `<form>` Element):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

Fügen Sie eine Datenquelle klicken Sie dann auf der Seite. Um eine begrenzte Menge an Daten zu verwenden, wählen wir nur die ersten fünf Einträge in der Vendor-Tabelle der AdventureWorks-Datenbank. Wenn Sie den Visual Studio-Assistenten zum Erstellen der Datenquelle verwenden, beachten Sie, ein Fehler in der aktuellen Version nicht den Tabellennamen als Präfix ist (`Vendor`) mit `Purchasing`. Das folgende Markup zeigt die korrekte Syntax:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

Als Nächstes fügen Sie einen Bereich, der als modales Fenster dient:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

Jetzt die `HoverMenuExtender` ins Spiel. Damit, dass jedes Element in der Datenquelle einen eigenen Popup erhält, muss der Extender platziert werden, innerhalb des Repeaters `<ItemTemplate>` Abschnitt. Dies ist das Markup:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

Jetzt jedes Element in der Datenquelle ein Popups auf der rechten Seite zeigt (`PopupPosition` Attribut) nach einer Verzögerung von 50 Millisekunden (`PopDelay` Attribut).


[![THE Hovermenü angezeigt wird, neben jedem Element im wiederholungsmodul](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

Das Hovermenü angezeigt wird, neben jedem Element im wiederholungsmodul ([klicken Sie, um das Bild in voller Größe anzeigen](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Weiter](using-hovermenu-with-a-repeater-control-vb.md)
