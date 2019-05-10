---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Erstellen einer Routeneinschränkung (VB) | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123423"
---
# <a name="creating-a-route-constraint-vb"></a>Erstellen einer Routeneinschränkung (VB)

durch [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.

Sie verwenden die routeneinschränkungen, um die Browseranforderungen zu beschränken, die eine bestimmte Route übereinstimmen. Sie können einen regulären Ausdruck verwenden, einer routeneinschränkung an.

Angenommen Sie, dass Sie die Route in Codebeispiel 1 in der Datei "Global.asax" definiert haben.

**Listing 1 - Global.asax.vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

Codebeispiel 1 enthält eine Route mit dem Namen Product. Sie können die Produkt-Route verwenden, Browseranforderungen ProductController in Listing 2 enthaltenen zuordnen.

**Codebeispiel 2 - Controllers\ProductController.vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

Beachten Sie, dass die Details()-Aktion, die von der Produkt-Controller verfügbar gemacht werden, einen einzelnen Parameter mit dem Namen "ProductID" akzeptiert. Dieser Parameter ist ein Integer-Parameter.

Die Route definiert, die in Codebeispiel 1 wird eine der folgenden URLs übereinstimmen:

- /Product/23
- /Product/7

Leider wird die Route auch die folgenden URLs übereinstimmen:

- /Product/blah
- /Product/apple

Da die Details() Aktion einen ganzzahligen Parameter erwartet, verursacht der eine Anforderung, die etwas anderes als ein ganzzahliger Wert enthält einen Fehler aus. Z. B. Wenn Sie die URL-/Product/apple in Ihren Browser eingeben erhalten die Fehlerseite in Abbildung 1 Sie.

[![Das Dialogfeld "Neues Projekt"](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)

**Abbildung 01**: Eine Seite explode angezeigt ([klicken Sie, um das Bild in voller Größe anzeigen](creating-a-route-constraint-vb/_static/image2.png))

Was Sie wirklich tun werden nur auf URLs überein, die eine richtige ganze Zahl "ProductID" enthalten. Eine Einschränkung können beim Definieren einer Route zum Einschränken der URLs, die mit die Route übereinstimmen. Die geänderte Produkt Route in Programmausdruck 3 enthält eine reguläre-Einschränkung, die nur Ganzzahlen entspricht.

**Codebeispiel 3 - Global.asax.vb**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

Der reguläre Ausdruck \d+ entspricht eine oder mehrere Ganzzahlen. Diese Einschränkung bewirkt, dass die Product-Route mit den folgenden URLs übereinstimmen:

- /Product/3
- /Product/8999

Aber nicht die folgenden URLs:

- /Product/apple
- /Product

Diese Browseranforderungen von einer anderen Route verarbeitet werden oder, wenn es keine übereinstimmenden Routen sind, eine *die Ressource konnte nicht gefunden werden* Fehler zurückgegeben.

> [!div class="step-by-step"]
> [Zurück](creating-custom-routes-vb.md)
> [Weiter](creating-a-custom-route-constraint-vb.md)
