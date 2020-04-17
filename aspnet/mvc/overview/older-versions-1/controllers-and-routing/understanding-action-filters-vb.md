---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: Grundlegendes zu Aktionsfiltern (VB) | Microsoft Docs
author: rick-anderson
description: Das Ziel dieses Tutorials ist es, Aktionsfilter zu erklären. Ein Aktionsfilter ist ein Attribut, das Sie auf eine Controlleraktion anwenden können -- oder einen gesamten Controller...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 70ab564bc1217f67874090d2ae6899d9bcd743a1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542104"
---
# <a name="understanding-action-filters-vb"></a>Grundlegendes zu Aktionsfiltern (VB)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> Das Ziel dieses Tutorials ist es, Aktionsfilter zu erklären. Ein Aktionsfilter ist ein Attribut, das Sie auf eine Controlleraktion -- oder einen gesamten Controller - anwenden können, die die Art und Weise ändert, in der die Aktion ausgeführt wird.

## <a name="understanding-action-filters"></a>Grundlegendes zu Aktionsfiltern

Das Ziel dieses Tutorials ist es, Aktionsfilter zu erklären. Ein Aktionsfilter ist ein Attribut, das Sie auf eine Controlleraktion -- oder einen gesamten Controller - anwenden können, die die Art und Weise ändert, in der die Aktion ausgeführt wird. Das ASP.NET MVC-Framework enthält mehrere Aktionsfilter:

- OutputCache – Dieser Aktionsfilter speichert die Ausgabe einer Controlleraktion für einen bestimmten Zeitraum zwischen.
- HandleError – Dieser Aktionsfilter behandelt Fehler, die beim Ausführen einer Controlleraktion ausgelöst werden.
- Autorisieren – Mit diesem Aktionsfilter können Sie den Zugriff auf einen bestimmten Benutzer oder eine bestimmte Rolle beschränken.

Sie können auch eigene benutzerdefinierte Aktionsfilter erstellen. Sie können z. B. einen benutzerdefinierten Aktionsfilter erstellen, um ein benutzerdefiniertes Authentifizierungssystem zu implementieren. Sie können auch einen Aktionsfilter erstellen, der die von einer Controlleraktion zurückgegebenen Ansichtsdaten ändert.

In diesem Tutorial erfahren Sie, wie Sie einen Aktionsfilter von Grund auf erstellen. Wir erstellen einen Protokollaktionsfilter, der verschiedene Phasen der Verarbeitung einer Aktion im Visual Studio-Ausgabefenster protokolliert.

### <a name="using-an-action-filter"></a>Verwenden eines Aktionsfilters

Ein Aktionsfilter ist ein Attribut. Sie können die meisten Aktionsfilter entweder auf eine einzelne Controlleraktion oder auf einen gesamten Controller anwenden.

Beispielsweise macht der Datencontroller in Liste 1 `Index()` eine Aktion mit dem Namen verfügbar, die die aktuelle Uhrzeit zurückgibt. Diese Aktion ist `OutputCache` mit dem Aktionsfilter dekoriert. Dieser Filter bewirkt, dass der von der Aktion zurückgegebene Wert für 10 Sekunden zwischengespeichert wird.

**Auflistung 1 –`Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

Wenn Sie die `Index()` Aktion wiederholt aufrufen, indem Sie die URL /Daten/Index in die Adressleiste Ihres Browsers eingeben und mehrmals auf die Schaltfläche Aktualisieren klicken, wird die gleiche Zeit für 10 Sekunden angezeigt. Die Ausgabe `Index()` der Aktion wird für 10 Sekunden zwischengespeichert (siehe Abbildung 1).

[![Zwischengespeicherte Zeit](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**Abbildung 01**: Zwischenspeichern der Zeit ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](understanding-action-filters-vb/_static/image3.png))

In Listing 1 wird ein `OutputCache` einzelner Aktionsfilter – `Index()` der Aktionsfilter – auf die Methode angewendet. Bei Bedarf können Sie mehrere Aktionsfilter auf dieselbe Aktion anwenden. Sie können z. B. `OutputCache` sowohl `HandleError` den Aktionsfilter als auch den Aktionsfilter auf dieselbe Aktion anwenden.

In Liste 1 `OutputCache` wird der Aktionsfilter auf die `Index()` Aktion angewendet. Sie können dieses Attribut `DataController` auch auf die Klasse selbst anwenden. In diesem Fall wird das Ergebnis, das von einer vom Controller ausgesetzten Aktion zurückgegeben wird, für 10 Sekunden zwischengespeichert.

### <a name="the-different-types-of-filters"></a>Die verschiedenen Filtertypen

Das ASP.NET MVC-Framework unterstützt vier verschiedene Filtertypen:

1. Autorisierungsfilter – `IAuthorizationFilter` Implementiert das Attribut.
2. Aktionsfilter – Implementiert `IActionFilter` das Attribut.
3. Ergebnisfilter – Implementiert `IResultFilter` das Attribut.
4. Ausnahmefilter – Implementiert `IExceptionFilter` das Attribut.

Filter werden in der oben aufgeführten Reihenfolge ausgeführt. Autorisierungsfilter werden beispielsweise immer ausgeführt, bevor Aktionsfilter und Ausnahmefilter immer nach jedem anderen Filtertyp ausgeführt werden.

Autorisierungsfilter werden verwendet, um Authentifizierung und Autorisierung für Controlleraktionen zu implementieren. Der Filter Autorisieren ist beispielsweise ein Beispiel für einen Autorisierungsfilter.

Aktionsfilter enthalten Logik, die vor und nach der Ausführung einer Controlleraktion ausgeführt wird. Sie können z. B. einen Aktionsfilter verwenden, um die Ansichtsdaten zu ändern, die von einer Controlleraktion zurückgegeben werden.

Ergebnisfilter enthalten Logik, die vor und nach der Ausführung eines Ansichtsergebnisses ausgeführt wird. Sie können z. B. ein Ansichtsergebnis direkt ändern, bevor die Ansicht im Browser gerendert wird.

Ausnahmefilter sind der letzte auszuführende Filtertyp. Sie können einen Ausnahmefilter verwenden, um Fehler zu behandeln, die entweder durch Die Controlleraktionen oder controller-Aktionsergebnisse ausgelöst werden. Sie können auch Ausnahmefilter verwenden, um Fehler zu protokollieren.

Jeder unterschiedliche Filtertyp wird in einer bestimmten Reihenfolge ausgeführt. Wenn Sie die Reihenfolge steuern möchten, in der Filter desselben Typs ausgeführt werden, können Sie die Order-Eigenschaft eines Filters festlegen.

Die Basisklasse für alle `System.Web.Mvc.FilterAttribute` Aktionsfilter ist die Klasse. Wenn Sie einen bestimmten Filtertyp implementieren möchten, müssen Sie eine Klasse erstellen, die von der Basisfilterklasse erbt und eine oder mehrere der Schnittstellen IAuthorizationFilter, IActionFilter, IResultFilter oder ExceptionFilter implementiert.

### <a name="the-base-actionfilterattribute-class"></a>Die Basis-ActionFilterAttribute-Klasse

Um Ihnen das Implementieren eines benutzerdefinierten Aktionsfilters zu erleichtern, enthält `ActionFilterAttribute` das ASP.NET MVC-Framework eine Basisklasse. Diese Klasse implementiert `IActionFilter` sowohl `IResultFilter` die als auch Schnittstellen `Filter` und erbt von der Klasse.

Die Terminologie hier ist nicht ganz konsistent. Technisch gesehen ist eine Klasse, die von der ActionFilterAttribute-Klasse erbt, sowohl ein Aktionsfilter als auch ein Ergebnisfilter. Im lockeren Sinne wird jedoch das Wort Aktionsfilter verwendet, um auf jede Art von Filter im ASP.NET MVC-Framework setzt sich.

Die Basis-ActionFilterAttribute-Klasse verfügt über die folgenden Methoden, die Sie überschreiben können:

- OnActionExecuting – Diese Methode wird aufgerufen, bevor eine Controlleraktion ausgeführt wird.
- OnActionExecuted – Diese Methode wird aufgerufen, nachdem eine Controlleraktion ausgeführt wurde.
- OnResultExecuting – Diese Methode wird aufgerufen, bevor ein Controlleraktionsergebnis ausgeführt wird.
- OnResultExecuted – Diese Methode wird aufgerufen, nachdem ein Controlleraktionsergebnis ausgeführt wurde.

Im nächsten Abschnitt erfahren Sie, wie Sie jede dieser verschiedenen Methoden implementieren können.

### <a name="creating-a-log-action-filter"></a>Erstellen eines Protokollaktionsfilters

Um zu veranschaulichen, wie Sie einen benutzerdefinierten Aktionsfilter erstellen können, erstellen wir einen benutzerdefinierten Aktionsfilter, der die Phasen der Verarbeitung einer Controlleraktion im Visual Studio-Ausgabefenster protokolliert. Unsere `LogActionFilter` ist in Listing 2 enthalten.

**Auflistung 2 –`ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

In Listing 2 `OnActionExecuting()` `OnActionExecuted()`rufen `OnResultExecuting()`die `OnResultExecuted()` , , `Log()` und die Methoden die Methode auf. Der Name der Methode und die aktuellen `Log()` Routendaten werden an die Methode übergeben. Die `Log()` Methode schreibt eine Nachricht in das Visual Studio-Ausgabefenster (siehe Abbildung 2).

[![Schreiben in das Visual Studio-Ausgabefenster](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**Abbildung 02**: Schreiben in das Visual Studio-Ausgabefenster ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](understanding-action-filters-vb/_static/image6.png))

Der Home-Controller in Liste 3 veranschaulicht, wie Sie den Aktionsfilter Protokoll auf eine gesamte Controllerklasse anwenden können. Immer wenn eine der vom Home-Controller verfügbar `Index()` gemachten `About()` Aktionen – entweder die Methode oder die Methode – aufgerufen wird, werden die Phasen der Verarbeitung der Aktion im Visual Studio-Ausgabefenster protokolliert.

**Auflistung 3 –`Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>Zusammenfassung

In diesem Tutorial wurden Sie mit ASP.NET MVC-Aktionsfiltern vorgestellt. Sie haben die vier verschiedenen Filtertypen gelernt: Autorisierungsfilter, Aktionsfilter, Ergebnisfilter und Ausnahmefilter. Sie haben auch `ActionFilterAttribute` etwas über die Basisklasse gelernt.

Schließlich haben Sie gelernt, wie Sie einen einfachen Aktionsfilter implementieren. Wir haben einen Protokollaktionsfilter erstellt, der die Phasen der Verarbeitung einer Controlleraktion im Visual Studio-Ausgabefenster protokolliert.

> [!div class="step-by-step"]
> [Zurück](asp-net-mvc-routing-overview-vb.md)
> [Weiter](improving-performance-with-output-caching-vb.md)
