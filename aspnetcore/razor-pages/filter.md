---
title: Filtermethoden für Razor-Seiten in ASP-NET Core
author: Rick-Anderson
description: Erfahren Sie, wie Sie Filtermethoden für Razor-Seiten in ASP.NET Core erstellen.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 04/05/2018
uid: razor-pages/filter
ms.openlocfilehash: 5b233d95c9fbab09c64072377b85b40b127df7b7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063427"
---
# <a name="filter-methods-for-razor-pages-in-aspnet-core"></a>Filtermethoden für Razor-Seiten in ASP-NET Core

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

Eine Razor-Seite filtert [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter?view=aspnetcore-2.0). [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter?view=aspnetcore-2.0) erlaubt Razor-Seiten Code auszuführen, bevor und nachdem ein Handler für Razor-Seiten ausgeführt wurde. Filter für Razor-Seiten ähneln [ASP.NET Core MVC-Aktionsfiltern](xref:mvc/controllers/filters#action-filters), sie können allerdings nicht auf einzelne Seitenhandlermethoden angewendet werden. 

Filter für Razor-Seiten:

* Führen Code aus, nachdem eine Handlermethode ausgewählt wurde, aber bevor die Modellbindung erfolgt
* Führen Code aus, bevor die Handlermethode ausgeführt wird, nachdem die Modellbindung abgeschlossen ist
* Führen Code aus, nachdem die Handlermethode ausgeführt wird
* Können auf einer Seite oder global implementiert werden
* Können nicht auf seitenspezifische Handlermethoden angewendet werden

Code kann ausgeführt werden, bevor eine Handlermethode ausgeführt wird, indem man den Seitenkonstruktor oder Middleware benutzt, aber nur Filter für Razor-Seiten haben Zugriff auf [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_HttpContext). Filter verfügen über einen Parameter, der von [FilterContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.filtercontext?view=aspnetcore-2.0) abgeleitet ist, um Zugriff auf `HttpContext` zu ermöglichen. Das Beispiel [Implementieren eines Filterattributs](#ifa) fügt der Antwort z.B. einen Header hinzu. Dies kann nicht über Konstruktoren oder Middleware erfolgen.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/filter/sample/PageFilter) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

Filter für Razor-Seiten bieten die folgenden Methoden, die global oder auf Seitenebene angewendet werden können:

* Synchrone Methoden:

    * [OnPageHandlerSelected](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerselected?view=aspnetcore-2.0) : Wird aufgerufen, nachdem eine Handlermethode ausgewählt wurde, aber vor dem Modell Bindung erfolgt.
    * [OnPageHandlerExecuting](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuting?view=aspnetcore-2.0) : Vor die Handlermethode ausgeführt wird, nach der modellbindung abgeschlossen ist, aufgerufen.
    * [OnPageHandlerExecuted](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuted?view=aspnetcore-2.0) : Wird aufgerufen, nachdem die Handlermethode ausgeführt, bevor das Aktionsergebnis wird.

* Asynchrone Methoden:

    * [OnPageHandlerSelectionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerselectionasync?view=aspnetcore-2.0) : Asynchron aufgerufen, nachdem die Handlermethode ausgewählt wurde, aber bevor die modellbindung erfolgt.
    * [OnPageHandlerExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerexecutionasync?view=aspnetcore-2.0) : Asynchron aufgerufen, bevor die Ereignishandlermethode aufgerufen wird, nach Abschluss der modellbindung.

> [!NOTE]
> Implementieren Sie **entweder** die synchrone oder asynchrone Version einer Filterschnittstelle, aber nicht beide. Das Framework prüft zuerst, ob der Filter die asynchrone Schnittstelle implementiert, und wenn dies der Fall ist, ruft es sie auf. Wenn dies nicht der Fall ist, ruft es die Methode(n) der synchronen Schnittstelle auf. Wenn beide Schnittstellen implementiert werden, werden nur die asynchronen Methoden aufgerufen. Die gleiche Regel gilt für Überschreibungen in Seiten. Implementieren Sie die synchrone oder asynchrone Version der Überschreibung, nicht beide.

## <a name="implement-razor-page-filters-globally"></a>Globales implementieren von Filtern für Razor-Seiten

Mit dem folgenden Code wird das `IAsyncPageFilter`-Element implementiert:

[!code-csharp[Main](filter/sample/PageFilter/Filters/SampleAsyncPageFilter.cs?name=snippet1)]

Im vorhergehenden Code wird [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger?view=aspnetcore-2.0) nicht benötigt. Es wird im Beispiel verwendet, um Überwachungsinformationen für die Anwendung bereitzustellen.

Der folgende Code aktiviert `SampleAsyncPageFilter` in der `Startup`-Klasse:

[!code-csharp[Main](filter/sample/PageFilter/Startup.cs?name=snippet2&highlight=11)]

Der folgende Code veranschaulicht die vollständige `Startup`-Klasse:

[!code-csharp[Main](filter/sample/PageFilter/Startup.cs?name=snippet1)]

Der folgende Code ruft `AddFolderApplicationModelConvention` auf, damit `SampleAsyncPageFilter` nur auf Seiten in */subFolder* angewendet wird:

[!code-csharp[Main](filter/sample/PageFilter/Startup2.cs?name=snippet2)]

Im folgenden Code wird `IPageFilter` synchron implementiert:

[!code-csharp[Main](filter/sample/PageFilter/Filters/SamplePageFilter.cs?name=snippet1)]

Der folgende Code aktiviert `SamplePageFilter`:

[!code-csharp[Main](filter/sample/PageFilter/StartupSync.cs?name=snippet2&highlight=11)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implement-razor-page-filters-by-overriding-filter-methods"></a>Implementieren von Filtern für Razor-Seiten durch Überschreiben von Filtermethoden

Der folgende Code überschreibt die synchronen Filter für Razor-Seiten:

[!code-csharp[Main](filter/sample/PageFilter/Pages/Index.cshtml.cs)]

::: moniker-end

<a name="ifa"></a>
## <a name="implement-a-filter-attribute"></a>Implementieren eines Filterattributs

Der integrierte attributbasierte Filter [OnResultExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncresultfilter.onresultexecutionasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Filters_IAsyncResultFilter_OnResultExecutionAsync_Microsoft_AspNetCore_Mvc_Filters_ResultExecutingContext_Microsoft_AspNetCore_Mvc_Filters_ResultExecutionDelegate_) kann als Unterklasse definiert werden. Der folgende Filter fügt der Antwort einen Header hinzu:

[!code-csharp[Main](filter/sample/PageFilter/Filters/AddHeaderAttribute.cs)]

Der folgende Code wendet das Attribut `AddHeader` an:

[!code-csharp[Main](filter/sample/PageFilter/Pages/Contact.cshtml.cs?name=snippet1)]

Informationen zum Überschreiben der Reihenfolge finden Sie unter [Überschreiben der Standardreihenfolge](xref:mvc/controllers/filters#overriding-the-default-order).

Informationen zum Kurzschließen der Filterpipeline eines Filters finden Sie unter [Abbrechen und Kurzschließen](xref:mvc/controllers/filters#cancellation-and-short-circuiting). 

<a name="auth"></a>
## <a name="authorize-filter-attribute"></a>Autorisieren eines Filterattributs

Das Attribut [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute?view=aspnetcore-2.0) kann auf ein `PageModel` angewendet werden:

[!code-csharp[Main](filter/sample/PageFilter/Pages/ModelWithAuthFilter.cshtml.cs?highlight=7)]
