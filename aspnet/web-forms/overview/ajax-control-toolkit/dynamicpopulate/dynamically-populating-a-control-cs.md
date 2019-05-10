---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: Dynamisches Auffüllen eines Steuerelements (c#) | Microsoft-Dokumentation
author: wenz
description: Das DynamicPopulate-Steuerelement in ASP.NET AJAX Control Toolkit Aufrufe eines Webdiensts (oder eine Seitenmethode) und füllt den resultierenden Wert in ein Zielsteuerelement, auf t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 1b3e944e45e8d2b746b2e42360693c245d93901f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132856"
---
# <a name="dynamically-populating-a-control-c"></a>Dynamisches Auffüllen eines Steuerelements (C#)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)

> Das DynamicPopulate-Steuerelement in ASP.NET AJAX Control Toolkit Aufrufe eines Webdiensts (oder eine Seitenmethode) und füllt den resultierenden Wert in einem Zielsteuerelement auf der Seite, ohne eine seitenaktualisierung.

## <a name="overview"></a>Übersicht

Die `DynamicPopulate` -Steuerelement in ASP.NET AJAX Control Toolkit Aufrufe eines Webdiensts (oder eine Seitenmethode), und füllt den resultierenden Wert in einem Zielsteuerelement auf der Seite, ohne eine seitenaktualisierung. In diesem Tutorial veranschaulicht, wie dies eingerichtet wird.

## <a name="steps"></a>Schritte

Zunächst einmal benötigen Sie eines ASP.NET-Webdiensts die implementiert wird, die Methode aufgerufen werden, indem Sie `DynamicPopulate`. Die Webdienstklasse erfordert die `ScriptService` in definierte Attribut `Microsoft.Web.Script.Services`; andernfalls ASP.NET AJAX kann nicht erstellt werden die clientseitige JavaScript-Proxy für den Webdienst, die wiederum erforderlich ist `DynamicPopulate`.

Die Webmethode muss erwarten, dass ein Argument vom Typzeichenfolge, mit dem Namen `contextKey`, da die `DynamicPopulate` Steuerelement sendet ein Teil der Informationen zum Sitzungskontext mit jeder Aufruf des Webdiensts. Der folgende Webdienst liefert das aktuelle Datum in einem Format dargestellt, durch die `contextKey` Argument:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

Der Webdienst wird als gespeichert `DynamicPopulate.cs.asmx`. Alternativ könnten Sie implementieren die `getDate()` Methode als Seitenmethode in der tatsächlichen ASP.NET-Seite mit dem `DynamicPopulate` Steuerelement.

Erstellen Sie im nächsten Schritt eine neue ASP.NET-Datei. Wie immer ist der erste Schritt zum Einschließen der `ScriptManager` in der aktuellen Seite, um die ASP.NET AJAX-Bibliothek zu laden und die Steuerelement-Toolkit-Arbeit zu machen:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

Fügen Sie dann ein Label-Steuerelement (z. B. über das HTML-Steuerelement mit dem gleichen Namen, oder die &lt; `asp:Label`  / &gt; Webserver-Steuerelement) zeigt die das Ergebnis des Webdienstaufrufs später noch mal.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

Eine HTML-Schaltfläche (wie ein HTML-Steuerelement, da es ein Postback an den Server nicht erforderlich ist) wird dann verwendet werden, um die dynamische Auffüllung auszulösen:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

Schließlich müssen wir die `DynamicPopulateExtender` Steuerelement zum Verbinden aller Elemente. Die folgenden Attribute festgelegt (abgesehen von der offensichtlichen Beziehungen, `ID` und `runat` = `"server"`):

- `TargetControlID` an welcher Stelle das Ergebnis über den Aufruf des Webdiensts
- `ServicePath` Pfad, an den Webdienst (weglassen, wenn Sie eine Seitenmethode verwenden möchten)
- `ServiceMethod` Name der Webmethode oder Seitenmethode
- `ContextKey` Kontextinformationen, die an den Webdienst gesendet werden
- `PopulateTriggerControlID` Element, das den Aufruf des Webdiensts wird ausgelöst.
- `ClearContentsDuringUpdate` angibt, ob das Zielelement beim den Aufruf des Webdiensts leere

Wie Sie sehen können, wird das Steuerelement erfordert einige Informationen, aber alles, was näher ist relativ einfach. Dies ist das Markup für die `DynamicPopulateExtender` -Steuerelement in das aktuelle Szenario:

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

Führen Sie die ASP.NET-Seite in den Browser, und klicken Sie auf die Schaltfläche; Sie erhalten das aktuelle Datum im Format Monat-Tag-Jahr.

[![Ein Klick auf die Schaltfläche mit den Ruft das Datum vom Server ab.](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)

Ein Klick auf die Schaltfläche mit den Ruft das Datum ab, auf dem Server ([klicken Sie, um das Bild in voller Größe anzeigen](dynamically-populating-a-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Nächste](dynamically-populating-a-control-using-javascript-code-cs.md)
