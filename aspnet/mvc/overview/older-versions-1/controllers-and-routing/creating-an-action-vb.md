---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Erstellen einer Aktion (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie einem ASP.NET MVC-Controller eine neue Aktion hinzufügen. Erfahren Sie mehr über die Anforderungen an eine Methode, die eine Aktion sein soll.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542247"
---
# <a name="creating-an-action-vb"></a>Erstellen einer Aktion (VB)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie einem ASP.NET MVC-Controller eine neue Aktion hinzufügen. Erfahren Sie mehr über die Anforderungen an eine Methode, die eine Aktion sein soll.

Das Ziel dieses Tutorials ist es, zu erklären, wie Sie eine neue Controlleraktion erstellen können. Sie lernen die Anforderungen einer Aktionsmethode. Außerdem erfahren Sie, wie Sie verhindern, dass eine Methode als Aktion verfügbar gemacht wird.

## <a name="adding-an-action-to-a-controller"></a>Hinzufügen einer Aktion zu einem Controller

Sie fügen einem Controller eine neue Aktion hinzu, indem Sie dem Controller eine neue Methode hinzufügen. Der Controller in Liste 1 enthält beispielsweise eine Aktion mit dem Namen Index() und eine Aktion mit dem Namen SayHello(). Beide Methoden werden als Aktionen verfügbar gemacht.

**Auflisten 1 - Controller-HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

Um dem Universum als Aktion ausgesetzt zu sein, muss eine Methode bestimmte Anforderungen erfüllen:

- Die Methode muss öffentlich sein.
- Die Methode kann keine statische Methode sein.
- Die Methode kann keine Erweiterungsmethode sein.
- Die Methode kann kein Konstruktor, Getter oder Setter sein.
- Die Methode kann keine offenen generischen Typen haben.
- Die Methode ist keine Methode der Controllerbasisklasse.
- Die Methode darf keine **ref-** oder **out-Parameter** enthalten.

Beachten Sie, dass der Rückgabetyp einer Controlleraktion nicht eingeschränkt ist. Eine Controlleraktion kann eine Zeichenfolge, eine DateTime, eine Instanz der Random-Klasse oder void zurückgeben. Das ASP.NET MVC-Framework konvertiert jeden Rückgabetyp, der kein Aktionsergebnis ist, in eine Zeichenfolge und rendert die Zeichenfolge in den Browser.

Wenn Sie eine Methode hinzufügen, die diese Anforderungen nicht zu einem Controller verletzt, wird die Methode als Controlleraktion verfügbar gemacht. Seien Sie hier vorsichtig. Eine Controlleraktion kann von jedem Benutzer aufgerufen werden, der mit dem Internet verbunden ist. Erstellen Sie z. B. keine DeleteMyWebsite()-Controlleraktion.

## <a name="preventing-a-public-method-from-being-invoked"></a>Verhindern, dass eine öffentliche Methode aufgerufen wird

Wenn Sie eine öffentliche Methode in einer Controllerklasse erstellen müssen und die Methode nicht als Controlleraktion verfügbar machen möchten, können Sie mithilfe des &lt;NonAction-Attributs&gt; verhindern, dass die Methode aufgerufen wird. Der Controller in Listing 2 enthält beispielsweise eine öffentliche Methode namens &lt;CompanySecrets(), die mit dem NonAction-Attribut&gt; versehen ist.

**Auflisten 2 - Controller-WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Wenn Sie versuchen, die Controlleraktion CompanySecrets() aufzurufen, indem Sie /Work/CompanySecrets in die Adressleiste Ihres Browsers eingeben, wird die Fehlermeldung in Abbildung 1 angezeigt.

[![Aufrufen einer NonAction-Methode](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Abbildung 01**: Aufrufen einer[NonAction-Methode (Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Zurück](creating-a-controller-vb.md)
> [Weiter](aspnet-mvc-controllers-overview-cs.md)
