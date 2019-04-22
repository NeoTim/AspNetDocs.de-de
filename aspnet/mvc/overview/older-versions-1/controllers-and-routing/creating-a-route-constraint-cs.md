---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Erstellen einer Routeneinschränkung (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 42c0ce5e158e2fe9387ac218ac0762b6362094f9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389570"
---
# <a name="creating-a-route-constraint-c"></a>Erstellen einer Routeneinschränkung (C#)

durch [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther wird in diesem Tutorial veranschaulicht, wie Sie steuern können, wie Browser Übereinstimmung Routen anfordert, durch das Erstellen von Einschränkungen mit regulären Ausdrücken.


Sie verwenden die routeneinschränkungen, um die Browseranforderungen zu beschränken, die eine bestimmte Route übereinstimmen. Sie können einen regulären Ausdruck verwenden, einer routeneinschränkung an.

Angenommen Sie, dass Sie die Route in Codebeispiel 1 in der Datei "Global.asax" definiert haben.

**Codebeispiel 1 – "Global.asax.cs"**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

Codebeispiel 1 enthält eine Route mit dem Namen Product. Sie können die Produkt-Route verwenden, Browseranforderungen ProductController in Listing 2 enthaltenen zuordnen.

**Codebeispiel 2 - Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

Beachten Sie, dass die Details()-Aktion, die von der Produkt-Controller verfügbar gemacht werden, einen einzelnen Parameter mit dem Namen "ProductID" akzeptiert. Dieser Parameter ist ein Integer-Parameter.

Die Route definiert, die in Codebeispiel 1 wird eine der folgenden URLs übereinstimmen:

- /Product/23
- /Product/7

Leider wird die Route auch die folgenden URLs übereinstimmen:

- /Product/blah
- /Product/apple

Da die Details() Aktion einen ganzzahligen Parameter erwartet, verursacht der eine Anforderung, die etwas anderes als ein ganzzahliger Wert enthält einen Fehler aus. Z. B. Wenn Sie die URL-/Product/apple in Ihren Browser eingeben erhalten die Fehlerseite in Abbildung 1 Sie.


[![Das Dialogfeld "Neues Projekt"](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**Abbildung 01**: Eine Seite explode angezeigt ([klicken Sie, um das Bild in voller Größe anzeigen](creating-a-route-constraint-cs/_static/image2.png))


Was Sie wirklich tun werden nur auf URLs überein, die eine richtige ganze Zahl "ProductID" enthalten. Eine Einschränkung können beim Definieren einer Route zum Einschränken der URLs, die mit die Route übereinstimmen. Die geänderte Produkt Route in Programmausdruck 3 enthält eine reguläre-Einschränkung, die nur Ganzzahlen entspricht.

**Codebeispiel 3: "Global.asax.cs"**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

Der reguläre Ausdruck \d+ entspricht eine oder mehrere Ganzzahlen. Diese Einschränkung bewirkt, dass die Product-Route mit den folgenden URLs übereinstimmen:

- /Product/3
- /Product/8999

Aber nicht die folgenden URLs:

- /Product/apple
- /Product

- Diese Browseranforderungen von einer anderen Route verarbeitet werden oder, wenn es keine übereinstimmenden Routen sind, eine *die Ressource konnte nicht gefunden werden* Fehler zurückgegeben.

> [!div class="step-by-step"]
> [Zurück](creating-custom-routes-cs.md)
> [Weiter](creating-a-custom-route-constraint-cs.md)
