---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: Erstellen von benutzerdefinierten Routen (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen. In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542741"
---
# <a name="creating-custom-routes-vb"></a>Erstellen von benutzerdefinierten Routen (VB)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung benutzerdefinierte Routen hinzufügen. In diesem Tutorial erfahren Sie, wie Sie die Standardroutentabelle in der Datei Global.asax ändern.

In diesem Tutorial erfahren Sie, wie Sie einer ASP.NET MVC-Anwendung eine benutzerdefinierte Route hinzufügen. Sie erfahren, wie Sie die Standardroutentabelle in der Datei Global.asax mit einer benutzerdefinierten Route ändern.

In ASP.NET MVC-Anwendungen funktioniert die Standardroutentabelle einwandfrei. Möglicherweise stellen Sie jedoch fest, dass Sie spezielle Routinganforderungen haben. In diesem Fall können Sie eine benutzerdefinierte Route erstellen.

Stellen Sie sich beispielsweise vor, dass Sie eine Bloganwendung erstellen. Sie können eingehende Anforderungen verarbeiten, die wie folgt aussehen:

/Archiv/12-25-2009

Wenn ein Benutzer diese Anforderung eingibt, möchten Sie den Blogeintrag zurückgeben, der dem Datum 25.12.2009 entspricht. Um diesen Anforderungstyp zu verarbeiten, müssen Sie eine benutzerdefinierte Route erstellen.

Die Datei Global.asax in Listing 1 enthält eine neue benutzerdefinierte Route mit dem Namen Blog, die Anforderungen verarbeitet, die wie /Archive/*Eintragsdatum*aussehen.

**Auflistung 1 - Global.asax (mit benutzerdefinierter Route)**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

Die Reihenfolge der Routen, die Sie der Routentabelle hinzufügen, ist wichtig. Unsere neue benutzerdefinierte Blogroute wird vor der vorhandenen Standardroute hinzugefügt. Wenn Sie die Bestellung umgekehrt haben, wird die Standardroute immer anstelle der benutzerdefinierten Route aufgerufen.

Die benutzerdefinierte Blogroute entspricht jeder Anforderung, die mit /Archive/ beginnt. Es entspricht also allen folgenden URLs:

- /Archiv/12-25-2009

- /Archiv/10-6-2004

- /Archiv/Apfel

Die benutzerdefinierte Route ordnet die eingehende Anforderung einem Controller mit dem Namen Archiv zu und ruft die Aktion Entry() auf. Wenn die Entry()-Methode aufgerufen wird, wird das Eintragsdatum als Parameter namens entryDate übergeben.

Sie können die benutzerdefinierte Blog-Route mit dem Controller in Liste 2 verwenden.

**Eintrag 2 - ArchiveController.vb**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

Beachten Sie, dass die Entry()-Methode in Listing 2 einen Parameter vom Typ DateTime akzeptiert. Das MVC-Framework ist intelligent genug, um das Eintragsdatum von der URL automatisch in einen DateTime-Wert zu konvertieren. Wenn der Parameter für das Eintragsdatum aus der URL nicht in eine DateTime konvertiert werden kann, wird ein Fehler ausgelöst (siehe Abbildung 1).

**Abbildung 1: Fehler beim Konvertieren des Parameters**

[![Dialogfeld „New Project“ (Neues Projekt)](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**Abbildung 01**: Fehler beim Konvertieren des Parameters ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-routes-vb/_static/image2.png))

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu demonstrieren, wie Sie eine benutzerdefinierte Route erstellen können. Sie haben gelernt, wie Sie der Routingtabelle in der Datei Global.asax, die Blogeinträge darstellt, eine benutzerdefinierte Route hinzufügen. Wir haben erläutert, wie Anforderungen für Blogeinträge einem Controller mit dem Namen ArchiveController und einer Controlleraktion namens Entry() zugeordnet werden.

> [!div class="step-by-step"]
> [Zurück](asp-net-mvc-controller-overview-vb.md)
> [Weiter](creating-a-route-constraint-vb.md)
