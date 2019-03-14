---
title: Verwenden von Teilansichten in ASP.NET Core
author: ardalis
description: Erfahren Sie, wie Sie Teilansichten verwenden können, um große Markupdateien aufzuteilen und die Duplizierung von allgemeinem Markup auf Webseiten in ASP.NET Core-Anwendungen zu verringern.
ms.author: riande
ms.custom: mvc
ms.date: 09/11/2018
uid: mvc/views/partial
ms.openlocfilehash: ff4b99580990edbd768128d77214e664a1e29e56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033297"
---
# <a name="partial-views-in-aspnet-core"></a>Verwenden von Teilansichten in ASP.NET Core

Von [Steve Smith](https://ardalis.com/), [Luke Latham](https://github.com/guardrex), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT) und [Scott Sauber](https://twitter.com/scottsauber)

Eine Teilansicht ist eine [Razor](xref:mvc/views/razor)-Markupdatei (*CSHTML-Datei*), die HTML-Ausgabe *innerhalb* der gerenderten Ausgabe einer anderen Markupdatei rendert.

::: moniker range=">= aspnetcore-2.1"

Der Begriff *Teilansicht* wird verwendet, wenn entweder eine MVC-App entwickelt wird, in der Markupdateien *Ansichten* genannt werden, oder eine Razor Pages-App, in der Markupdateien *Seiten* genannt werden. In diesem Thema werden MVC-Ansichten und Razor Pages-Seiten allgemein als *Markupdateien* bezeichnet.

::: moniker-end

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

## <a name="when-to-use-partial-views"></a>Wann werden Teilansichten verwendet?

Teilansichten bieten eine effektive Möglichkeit, um Folgendes zu erreichen:

* Aufteilen großer Markupdateien in kleinere Komponenten.

  In einer großen, komplexen Markupdatei, die aus mehreren logischen Teilen besteht, bringt es Vorteile mit sich, mit jeder einzelnen Komponente isoliert in einer Teilansicht zu arbeiten. Der Code in der Markupdatei ist verwaltbar, weil das Markup nur die allgemeine Seitenstruktur und Verweise auf Teilansichten enthält.
* Verringern der Duplizierung von allgemeinem Markupinhalt in Markupdateien.

  Wenn die gleichen Markupelemente in verschiedenen Markupdateien verwendet werden, entfernt eine Teilansicht die Duplizierung von Markupinhalten in einer Teilansichtsdatei. Wenn das Markup in der Teilansicht geändert wird, wird die gerenderte Ausgabe der Markupdateien aktualisiert, die die Teilansicht verwenden.

Teilansichten sollte nicht verwendet werden, um allgemeine Layoutelemente zu verwalten. Häufig verwendete Layoutelemente müssen in [_Layout.cshtml](xref:mvc/views/layout)-Dateien angegeben werden.

Verwenden Sie keine Teilansicht, wenn für das Rendern des Markups eine komplexe Renderinglogik oder Codeausführung erforderlich ist. Verwenden Sie anstelle einer Teilansicht eine [Ansichtskomponente](xref:mvc/views/view-components).

## <a name="declare-partial-views"></a>Deklarieren von Teilansichten

::: moniker range=">= aspnetcore-2.0"

Eine Teilansicht ist eine *CSHTML*-Markupdatei, die innerhalb des Ordners *Views* (MVC) oder des Ordners *Pages* (Razor Pages) verwaltet wird.

In ASP.NET Core MVC kann <xref:Microsoft.AspNetCore.Mvc.ViewResult> eines Controllers eine Ansicht oder eine Teilansicht zurückgeben. Eine analoge Funktion ist für Razor Pages in ASP.NET Core 2.2 geplant. In Razor Pages kann <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> ein <xref:Microsoft.AspNetCore.Mvc.PartialViewResult> zurückgeben. Das Verweisen auf und Rendern von Teilansichten wird im Abschnitt [Verweisen auf eine Teilansicht](#reference-a-partial-view) beschrieben.

Im Gegensatz zu MVC-Ansichten oder Seitenrendering führt eine Teilansicht *_ViewStart.cshtml* nicht aus. Weitere Informationen zu *_ViewStart.cshtml* finden Sie unter <xref:mvc/views/layout>.

Dateinamen von Teilansichten beginnen häufig mit einem Unterstrich (`_`). Diese Namenskonvention ist keine Voraussetzung, sie hilft aber dabei, Teilansichten von Ansichten und Seiten visuell zu unterscheiden.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Eine Teilansicht ist eine *CSHTML*-Markupdatei, die innerhalb des Ordners *Views* verwaltet wird.

<xref:Microsoft.AspNetCore.Mvc.ViewResult> eines Controllers kann eine Ansicht oder eine Teilansicht zurückgeben.

Im Gegensatz zu MVC-Ansichten oder Rendering führt eine Teilansicht *_ViewStart.cshtml* nicht aus. Weitere Informationen zu *_ViewStart.cshtml* finden Sie unter <xref:mvc/views/layout>.

Dateinamen von Teilansichten beginnen häufig mit einem Unterstrich (`_`). Diese Namenskonvention ist keine Voraussetzung, sie hilft aber dabei, Teilansichten von Ansichten visuell zu unterscheiden.

::: moniker-end

## <a name="reference-a-partial-view"></a>Verweisen auf eine Teilansicht

::: moniker range=">= aspnetcore-2.1"

Innerhalb einer Markupdatei gibt es mehrere Möglichkeiten, auf eine Teilansicht zu verweisen. Es wird empfohlen, dass Apps einen der folgenden Ansätze für asynchrones Rendering verwenden:

* [Hilfsprogramm für Teiltags](#partial-tag-helper)
* [Asynchrones HTML-Hilfsprogramm](#asynchronous-html-helper)

::: moniker-end

::: moniker range="< aspnetcore-2.1"

Innerhalb einer Markupdatei gibt es zwei Möglichkeiten, auf eine Teilansicht zu verweisen:

* [Asynchrones HTML-Hilfsprogramm](#asynchronous-html-helper)
* [Synchrones HTML-Hilfsprogramm](#synchronous-html-helper)

Es wird empfohlen, dass Apps das [asynchrone HTML-Hilfsprogramm](#asynchronous-html-helper) verwenden.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a>Hilfsprogramm für Teiltags

Das [Hilfsprogramm für Teiltags](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper) erfordert ASP.NET Core 2.1 oder höher.

Das Hilfsprogramm für Teiltags rendert Inhalte asynchron und verwendet eine HTML-ähnliche Syntax:

```cshtml
<partial name="_PartialName" />
```

Wenn eine Dateierweiterung vorhanden ist, verweist das Hilfsprogramm für Teiltags auf eine Teilansicht, die sich im gleichen Ordner wie die Markupdatei befinden muss, die die Teilansicht aufruft:

```cshtml
<partial name="_PartialName.cshtml" />
```

Im folgende Beispiel wird aus dem Stammverzeichnis der App auf eine Teilansicht verwiesen. Pfade, die mit einer Tilde und einem Schrägstrich (`~/`) oder einem Schrägstrich (`/`) beginnen, verweisen auf den Stamm der App:

**Razor Pages**

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

**MVC**

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

Das folgende Beispiel verweist auf eine Teilansicht mit einem relativen Pfad:

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

Weitere Informationen finden Sie unter <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>.

::: moniker-end

### <a name="asynchronous-html-helper"></a>Hilfsprogramm für asynchrone HTML

Wenn Sie ein HTML-Hilfsprogramm verwenden, stellt das Verwenden von <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*> eine bewährte Methode dar. `PartialAsync` gibt einen <xref:Microsoft.AspNetCore.Html.IHtmlContent>-Typ in einem <xref:System.Threading.Tasks.Task`1> als Wrapper zurück. Sie können auf die Methode verweisen, indem Sie dem erwarteten Aufruf das Zeichen `@` als Präfix voranstellen:

```cshtml
@await Html.PartialAsync("_PartialName")
```

Wenn die Dateierweiterung vorhanden ist, verweist das HTML-Hilfsprogramm auf eine Teilansicht, die sich im gleichen Ordner wie die Markupdatei befinden muss, die die Teilansicht aufruft:

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

Im folgende Beispiel wird aus dem Stammverzeichnis der App auf eine Teilansicht verwiesen. Pfade, die mit einer Tilde und einem Schrägstrich (`~/`) oder einem Schrägstrich (`/`) beginnen, verweisen auf den Stamm der App:

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

**MVC**

::: moniker-end

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

Das folgende Beispiel verweist auf eine Teilansicht mit einem relativen Pfad:

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

Alternativ können Sie eine Teilansicht auch mit <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*> rendern. Diese Methode gibt keinen <xref:Microsoft.AspNetCore.Html.IHtmlContent> zurück. Sie streamt die gerenderte Ausgabe direkt an die Antwort. Da die Methode kein Ergebnis zurückgibt, muss sie in einem Razor-Codeblock aufgerufen werden:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

Da `RenderPartialAsync` gerenderte Inhalte streamt, bietet diese Vorgehensweise in einigen Szenarien eine bessere Leistung. In leistungskritischen Situationen sollten Sie die Seite mit beiden Ansätzen einem Benchmarktest unterziehen und den Ansatz verwenden, der eine schnellere Antwort generiert.

### <a name="synchronous-html-helper"></a>Hilfsprogramm für synchrone HTML

<xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> und <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*> sind die synchronen Entsprechungen von `PartialAsync` bzw. `RenderPartialAsync`. Diese synchronen Entsprechungen werden nicht empfohlen, da sie in manchen Szenarien zu einem Deadlock führen können. Die synchronen Methoden sollen in einem zukünftigen Release entfernt werden.

> [!IMPORTANT]
> Wenn Sie Code ausführen müssen, verwenden Sie anstelle von Teilansichten [Ansichtskomponenten](xref:mvc/views/view-components).

::: moniker range=">= aspnetcore-2.1"

Das Aufrufen von `Partial` oder `RenderPartial` führt zu einer Visual Studio Analyzer-Warnung. Beispielsweise führt das Vorhandensein von `Partial` zu folgender Warnmeldung:

> Die Verwendung von IHtmlHelper.Partial kann zu Anwendungsdeadlocks führen. Erwägen Sie die Verwendung des Hilfsprogramms für &lt;Teiltags&gt; oder von IHtmlHelper.PartialAsync.

Ersetzen Sie Aufrufe von `@Html.Partial` durch `@await Html.PartialAsync` oder durch das [Hilfsprogramm für Teiltags](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper). Weiter Informationen zur Migration des Teiltaghilfsprogramms finden Sie unter [Migrate from an HTML Helper (Migration von einem HTML-Hilfsprogramm)](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper)

::: moniker-end

## <a name="partial-view-discovery"></a>Ermittlung von Teilansichten

Wenn auf eine Teilansicht anhand des Namens ohne eine Dateierweiterung verwiesen wird, werden die folgenden Speicherorte in der angegebenen Reihenfolge durchsucht:

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

1. Der Ordner der aktuell ausgeführten Seite
1. Der Verzeichnisgraph über dem Ordner der Seite
1. `/Shared`
1. `/Pages/Shared`
1. `/Views/Shared`

**MVC**

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`
1. `/Pages/Shared`

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`

::: moniker-end

Für die Ermittlung von Teilansichten gelten die folgenden Konventionen:

* Unterschiedliche Teilansichten mit dem gleichen Dateinamen sind zulässig, wenn sich die Teilansichten in verschiedenen Ordnern befinden.
* Wenn auf eine Teilansicht über den Namen ohne Dateierweiterung verwiesen wird und die Teilansicht sowohl im Ordner des Aufrufers als auch im Ordner *Shared* vorhanden ist, stellt die Teilansicht im Ordner des Aufrufers die Teilansicht bereit. Wenn die Teilansicht nicht im Ordner des Aufrufers vorhanden ist, wird die Teilansicht aus dem Ordner *Shared* bereitgestellt. Teilansichten im Ordner *Shared* werden als *Freigegebene Teilansichten* oder *Standardteilansichten* bezeichnet.
* Teilansichten können *verkettet* sein: Eine Teilansicht kann eine andere Teilansicht aufrufen, wenn durch den Aufruf kein Zirkelbezug entsteht. Relative Pfade sind immer relativ zur aktuellen Datei, nicht zum Stamm- oder übergeordneten Verzeichnis der Datei.

> [!NOTE]
> Ein [Razor](xref:mvc/views/razor) `section`, der in einer Teilansicht definiert ist, ist für übergeordnete Markupdateien nicht sichtbar. Die `section`-Anweisung ist nur für die Teilansicht, in der sie definiert ist, sichtbar.

## <a name="access-data-from-partial-views"></a>Zugriff auf Daten aus Teilansichten

Wenn eine Teilansicht instanziiert wird, erhält sie eine *Kopie* des `ViewData`-Wörterbuchs der übergeordneten Ansicht. An den Daten vorgenommene Änderungen in der Teilansicht werden in der übergeordneten Ansicht nicht beibehalten. Ein `ViewData`-Wörterbuch, das in einer Teilansicht verändert wird, geht verloren, wenn die Teilansicht eine Rückgabe ausgibt.

Das folgende Beispiel zeigt, wie eine Instanz von [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) an eine Teilansicht übergeben wird:

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

Außerdem können Sie ein Modell an eine Teilansicht übergeben. Das Modell kann ein benutzerdefiniertes Objekt sein. Sie können ein Modell mit `PartialAsync` (rendert einen Inhaltsblock für den Aufrufer) oder `RenderPartialAsync` (streamt den Inhalt in die Ausgabe) übergeben:

```cshtml
@await Html.PartialAsync("_PartialName", model)
```

::: moniker range=">= aspnetcore-2.1"

**Razor Pages**

Das folgende Markup in der Beispiel-App stammt von der Seite *Pages/ArticlesRP/ReadRP.cshtml*. Diese Seite enthält zwei Teilansichten. Die zweite Teilansicht übergibt ein Modell und `ViewData` an die Teilansicht. Die `ViewDataDictionary`-Konstruktorüberladung wird verwendet, um ein neues `ViewData`-Wörterbuch zu übergeben, während das vorhandene `ViewData`-Wörterbuch beibehalten wird.

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/ReadRP.cshtml?name=snippet_ReadPartialViewRP&highlight=5,15-19)]

*Pages/Shared/_AuthorPartialRP.cshtml* ist die erste Teilansicht, auf die durch die Markupdatei *ReadRP.cshtml* verwiesen wird:

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/Shared/_AuthorPartialRP.cshtml)]

*Pages/ArticlesRP/_ArticleSectionRP.cshtml* ist die zweite Teilansicht, auf die durch die Markupdatei *ReadRP.cshtml* verwiesen wird:

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/_ArticleSectionRP.cshtml)]

**MVC**

::: moniker-end

Das folgende Markup in der Beispiel-App zeigt die Ansicht *Views/Articles/Read.cshtml*. Die Ansicht enthält die zwei Teilansichten. Die zweite Teilansicht übergibt ein Modell und `ViewData` an die Teilansicht. Die `ViewDataDictionary`-Konstruktorüberladung wird verwendet, um ein neues `ViewData`-Wörterbuch zu übergeben, während das vorhandene `ViewData`-Wörterbuch beibehalten wird.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=5,15-19)]

*Views/Shared/_AuthorPartial.cshtml* ist die erste Teilansicht, auf die durch die Markupdatei *ReadRP.cshtml* verwiesen wird:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

*Views/Articles/_ArticleSection.cshtml* ist die zweite Teilansicht, auf die durch die Markupdatei *ReadRP.cshtml* verwiesen wird:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

Die Teilansichten werden zur Laufzeit in der gerenderten Ausgabe der übergeordneten Markupdatei gerendert, die wiederum in der freigegebenen Datei *_Layout.cshtml* gerendert wird. Die erste Teilansicht rendert den Namen des Artikelautors und das Erscheinungsdatum:

> Abraham Lincoln
>
> Diese Teilansicht aus dem &lt;Dateipfad der freigegebenen Teilansicht&gt;.
> 11/19/1863 12:00:00 AM

Die zweite Teilansicht rendert die Abschnitte des Artikels:

> Abschnitt einen Index an: 0
>
> Four score and seven years ago ...
>
> Abschnitt 2-Index: 1
>
> Now we are engaged in a great civil war, testing ...
>
> Abschnitt 3-Index: 2
>
> But, in a larger sense, we can not dedicate ...

## <a name="additional-resources"></a>Zusätzliche Ressourcen

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end
