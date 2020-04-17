---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: Übergeben von Daten an Masterseiten (VB) | Microsoft Docs
author: rick-anderson
description: Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie Daten von einem Controller an eine Ansichtsmasterseite übergeben können. Wir untersuchen zwei Strategien für die Weitergabe von Daten an eine Ansicht m...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: ef65541a5f2297414f923e2f8108a14de67531e5
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542468"
---
# <a name="passing-data-to-view-master-pages-vb"></a>Übergeben von Daten an Ansichtsmasterseiten (VB)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie Daten von einem Controller an eine Ansichtsmasterseite übergeben können. Wir untersuchen zwei Strategien zum Übergeben von Daten an eine Ansichtsmasterseite. Zunächst wird eine einfache Lösung erläutert, die zu einer Anwendung führt, die schwer zu warten ist. Als Nächstes untersuchen wir eine viel bessere Lösung, die etwas mehr Anfängliche Arbeit erfordert, aber zu einer viel besser verwaltbaren Anwendung führt.

## <a name="passing-data-to-view-master-pages"></a>Übergeben von Daten zum Anzeigen von Masterseiten

Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie Daten von einem Controller an eine Ansichtsmasterseite übergeben können. Wir untersuchen zwei Strategien zum Übergeben von Daten an eine Ansichtsmasterseite. Zunächst wird eine einfache Lösung erläutert, die zu einer Anwendung führt, die schwer zu warten ist. Als Nächstes untersuchen wir eine viel bessere Lösung, die etwas mehr Anfängliche Arbeit erfordert, aber zu einer viel besser verwaltbaren Anwendung führt.

### <a name="the-problem"></a>Problemstellung

Stellen Sie sich vor, Sie erstellen eine Filmdatenbankanwendung und möchten die Liste der Filmkategorien auf jeder Seite Ihrer Anwendung anzeigen (siehe Abbildung 1). Stellen Sie sich außerdem vor, dass die Liste der Filmkategorien in einer Datenbanktabelle gespeichert ist. In diesem Fall wäre es sinnvoll, die Kategorien aus der Datenbank abzurufen und die Liste der Filmkategorien innerhalb einer Ansichtsmasterseite zu rendern.

[![Anzeigen von Filmkategorien in einer Ansichtsmasterseite](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**Abbildung 01**: Anzeigen von Filmkategorien auf einer Ansichtsmasterseite ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](passing-data-to-view-master-pages-vb/_static/image3.png))

Hier ist das Problem. Wie ruft man die Liste der Filmkategorien auf der Masterseite ab? Es ist verlockend, Methoden Ihrer Modellklassen direkt auf der Masterseite aufzurufen. Mit anderen Worten, es ist verlockend, den Code zum Abrufen der Daten aus der Datenbank direkt in Ihre Masterseite aufzunehmen. Wenn Sie jedoch Ihre MVC-Controller für den Zugriff auf die Datenbank umgehen, würde dies gegen die saubere Trennung von Bedenken verstoßen, die einer der Hauptvorteile beim Erstellen einer MVC-Anwendung ist.

In einer MVC-Anwendung soll die gesamte Interaktion zwischen Ihren MVC-Ansichten und Ihrem MVC-Modell von Ihren MVC-Controllern verarbeitet werden. Diese Trennung von Anliegen führt zu einer behaltebareren, anpassungsfähigeren und testbareren Anwendung.

In einer MVC-Anwendung sollten alle Daten, die an eine Ansicht übergeben werden – einschließlich einer Ansichtmasterseite – durch eine Controlleraktion an eine Ansicht übergeben werden. Darüber hinaus sollten die Daten unter Nutzung von Ansichtsdaten übergeben werden. Im weiteren Verlauf dieses Tutorials betrachte ich zwei Methoden zum Übergeben von Ansichtsdaten an eine Ansichtsmasterseite.

### <a name="the-simple-solution"></a>Die einfache Lösung

Beginnen wir mit der einfachsten Lösung zum Übergeben von Ansichtsdaten von einem Controller an eine Ansichtsmasterseite. Die einfachste Lösung besteht darin, die Ansichtsdaten für die Masterseite in jeder einzelnen Controlleraktion zu übergeben.

Betrachten Sie den Controller in Listing 1. Es macht zwei `Index()` Aktionen `Details()`mit dem Namen und verfügbar. Die `Index()` Aktionsmethode gibt jeden Film in der Tabelle Filme-Datenbank zurück. Die `Details()` Aktionsmethode gibt jeden Film in einer bestimmten Filmkategorie zurück.

**Auflistung 1 –`Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

Beachten Sie, `Index()` dass `Details()` sowohl die als auch die Aktionen zwei Elemente zum Anzeigen von Daten hinzufügen. Die `Index()` Aktion fügt zwei Schlüssel hinzu: Kategorien und Filme. Der Kategorieschlüssel stellt die Liste der Filmkategorien dar, die auf der Ansichtsmasterseite angezeigt werden. Der Filmschlüssel stellt die Liste der Filme dar, die auf der Seite Indexansicht angezeigt werden.

Die `Details()` Aktion fügt auch zwei Schlüssel namens Kategorien und Filme hinzu. Der Kategorienschlüssel stellt erneut die Liste der Filmkategorien dar, die von der Ansichtsmasterseite angezeigt werden. Der Filmschlüssel stellt die Liste der Filme in einer bestimmten Kategorie dar, die auf der Seite Details angezeigt werden (siehe Abbildung 2).

[![Die Detailansicht](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**Abbildung 02**: Die Detailansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](passing-data-to-view-master-pages-vb/_static/image6.png))

Die Indexansicht ist in Listing 2 enthalten. Es iteriert einfach durch die Liste der Filme durch das Filmelement in Ansicht Daten dargestellt.

**Auflistung 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

Die Ansichtsmasterseite ist in Liste 3 enthalten. Die Ansichtsmasterseite iteriert und rendert alle Filmkategorien, die durch das Kategorienelement aus Ansichtsdaten dargestellt werden.

**Auflistung 3 –`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

Alle Daten werden über Ansichtsdaten an die Ansicht und die Ansichtsmasterseite übergeben. Das ist der richtige Weg, um Daten an die Masterseite zu übergeben.

Also, was ist falsch an dieser Lösung? Das Problem ist, dass diese Lösung gegen das DRY-Prinzip (Don't Repeat Yourself) verstößt. Jede Controlleraktion muss dieselbe Liste von Filmkategorien hinzufügen, um Daten anzuzeigen. Durch das Verfügen mit doppeltem Code in der Anwendung wird die Wartung, Anpassung und Änderung der Anwendung erheblich erschwert.

### <a name="the-good-solution"></a>Die gute Lösung

In diesem Abschnitt untersuchen wir eine alternative und bessere Lösung zum Übergeben von Daten von einer Controlleraktion an eine Ansichtsmasterseite. Anstatt die Filmkategorien für die Masterseite in jeder einzelnen Controlleraktion hinzuzufügen, fügen wir die Filmkategorien nur einmal zu den Ansichtsdaten hinzu. Alle Ansichtsdaten, die von der Ansichtsmasterseite verwendet werden, werden in einem Anwendungscontroller hinzugefügt.

Die ApplicationController-Klasse ist in Liste 4 enthalten.

Die ApplicationController-Klasse ist in Liste 4 enthalten.

**Auflistung 4 –`Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

Es gibt drei Dinge, die Sie über den Anwendungscontroller in Listing 4 beachten sollten. Beachten Sie zunächst, dass die Klasse von der Basisklasse System.Web.Mvc.Controller erbt. Der Anwendungscontroller ist eine Controllerklasse.

Beachten Sie zweitens, dass die Application-Controllerklasse eine MustInherit-Klasse ist. Eine MustInherit-Klasse ist eine Klasse, die von einer konkreten Klasse implementiert werden muss. Da der Application-Controller eine MustInherit-Klasse ist, können Sie keine in der Klasse definierten Methoden direkt aufrufen. Wenn Sie versuchen, die Application-Klasse direkt aufzurufen, wird die Fehlermeldung Resource Cannot Be Found angezeigt.

Beachten Sie drittens, dass der Anwendungscontroller einen Konstruktor enthält, der die Liste der Filmkategorien zum Anzeigen von Daten hinzufügt. Jede Controllerklasse, die vom Anwendungscontroller erbt, ruft den Konstruktor des Anwendungscontrollers automatisch auf. Wenn Sie eine Aktion auf einem Controller aufrufen, der vom Anwendungscontroller erbt, werden die Filmkategorien automatisch in die Ansichtsdaten einbezogen.

Der Movies-Controller in Liste 5 erbt vom Anwendungscontroller.

**Auflistung 5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

Der Movies-Controller macht, genau wie der im vorherigen Abschnitt `Index()` besprochene Home-Controller, zwei Aktionsmethoden mit dem Namen und `Details()`verfügbar. Beachten Sie, dass die Liste der Filmkategorien, die von der `Index()` `Details()` Ansichtmasterseite angezeigt werden, nicht hinzugefügt wird, um Daten in der oder-Methode anzuzeigen. Da der Movies-Controller vom Anwendungscontroller erbt, wird die Liste der Filmkategorien hinzugefügt, um Daten automatisch anzuzeigen.

Beachten Sie, dass diese Lösung zum Hinzufügen von Ansichtsdaten für eine Ansichtsmasterseite nicht gegen das DRY-Prinzip (Wiederholen Sie sich selbst) verstößt. Der Code zum Hinzufügen der Liste der Filmkategorien zum Anzeigen von Daten ist nur an einem Speicherort enthalten: dem Konstruktor für den Anwendungscontroller.

### <a name="summary"></a>Zusammenfassung

In diesem Tutorial wurden zwei Ansätze zum Übergeben von Ansichtsdaten von einem Controller an eine Ansichtsmasterseite erläutert. Zunächst haben wir einen einfachen, aber schwer aufrechtzuerhaltenden Ansatz untersucht. Im ersten Abschnitt wurde erläutert, wie Sie Ansichtsdaten für eine Ansichtsmasterseite in jeder Controlleraktion in Ihrer Anwendung hinzufügen können. Wir kamen zu dem Schluss, dass dies ein schlechter Ansatz war, weil er gegen das DRY-Prinzip (Don't Repeat Yourself) verstößt.

Als Nächstes haben wir eine viel bessere Strategie zum Hinzufügen von Daten untersucht, die von einer Ansichtsmasterseite zum Anzeigen von Daten benötigt werden. Anstatt die Ansichtsdaten in jeder einzelnen Controlleraktion hinzuzufügen, haben wir die Ansichtsdaten nur einmal innerhalb eines Anwendungscontrollers hinzugefügt. Auf diese Weise können Sie doppelten Code vermeiden, wenn Sie Daten an eine Ansichtsmasterseite in einer ASP.NET MVC-Anwendung übergeben.

> [!div class="step-by-step"]
> [Vorherige](creating-page-layouts-with-view-master-pages-vb.md)
