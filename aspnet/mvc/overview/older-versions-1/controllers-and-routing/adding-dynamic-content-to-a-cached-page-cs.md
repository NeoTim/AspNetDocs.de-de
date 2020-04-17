---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: Hinzufügen dynamischer Inhalte zu einer zwischengespeicherten Seite | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie dynamische und zwischengespeicherte Inhalte auf derselben Seite mischen. Post-Cache-Ersetzung ermöglicht es Ihnen, dynamische Inhalte anzuzeigen, wie Banner-Werbung o...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c8cd70a15c1ae93f7cf9b0a026b37b07e489040
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542286"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>Hinzufügen von dynamischen Inhalten zu einer zwischengespeicherten Seite (C#)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie dynamische und zwischengespeicherte Inhalte auf derselben Seite mischen. Mit der Post-Cache-Ersetzung können Sie dynamische Inhalte, z. B. Bannerwerbung oder Nachrichten, innerhalb einer Seite anzeigen, die zwischengespeichert wurde.

Durch die Nutzung der Ausgabezwischenspeicherung können Sie die Leistung einer ASP.NET MVC-Anwendung erheblich verbessern. Anstatt jedes Mal, wenn die Seite angefordert wird, eine Seite zu regenerieren, kann die Seite einmal generiert und für mehrere Benutzer im Arbeitsspeicher zwischengespeichert werden.

Aber es gibt ein Problem. Was ist, wenn Sie dynamischen Inhalt auf der Seite anzeigen müssen? Stellen Sie sich beispielsweise vor, dass Sie eine Bannerwerbung auf der Seite anzeigen möchten. Sie möchten nicht, dass die Bannerwerbung zwischengespeichert wird, so dass jeder Benutzer die gleiche Werbung sieht. Auf diese Weise würdest du kein Geld verdienen!

Glücklicherweise gibt es eine einfache Lösung. Sie können ein Feature des ASP.NET Frameworks nutzen, das *als Post-Cache-Ersetzung*bezeichnet wird. Mit der Post-Cache-Ersetzung können Sie dynamischen Inhalt auf einer Seite ersetzen, die im Arbeitsspeicher zwischengespeichert wurde.

Wenn Sie eine Seite mithilfe des Attributs [OutputCache] zwischenspeichern, wird die Seite normalerweise sowohl auf dem Server als auch auf dem Client (dem Webbrowser) zwischengespeichert. Wenn Sie die Post-Cache-Ersetzung verwenden, wird eine Seite nur auf dem Server zwischengespeichert.

#### <a name="using-post-cache-substitution"></a>Verwenden der Post-Cache-Ersetzung

Die Verwendung der Post-Cache-Ersetzung erfordert zwei Schritte. Zuerst müssen Sie eine Methode definieren, die eine Zeichenfolge zurückgibt, die den dynamischen Inhalt darstellt, den Sie auf der zwischengespeicherten Seite anzeigen möchten. Als Nächstes rufen Sie die HttpResponse.WriteSubstitution()-Methode auf, um den dynamischen Inhalt in die Seite einzuschleusen.

Stellen Sie sich beispielsweise vor, dass Sie zufällig verschiedene Nachrichtenelemente auf einer zwischengespeicherten Seite anzeigen möchten. Die Klasse in Listing 1 macht eine einzelne Methode namens RenderNews() verfügbar, die nach dem Zufallsprinzip ein Nachrichtenelement aus einer Liste von drei Nachrichtenelementen zurückgibt.

**Auflisten 1 – Models-News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

Um die Post-Cache-Ersetzung zu nutzen, rufen Sie die HttpResponse.WriteSubstitution()-Methode auf. Die WriteSubstitution()-Methode richtet den Code ein, um einen Bereich der zwischengespeicherten Seite durch dynamischen Inhalt zu ersetzen. Die WriteSubstitution()-Methode wird verwendet, um die zufällige Nachricht in der Ansicht in Liste 2 anzuzeigen.

**Auflisten 2 – Ansichten, Home, Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

Die RenderNews-Methode wird an die WriteSubstitution()-Methode übergeben. Beachten Sie, dass die RenderNews-Methode nicht aufgerufen wird (es gibt keine Klammern). Stattdessen wird ein Verweis auf die Methode an WriteSubstitution() übergeben.

Die Indexansicht wird zwischengespeichert. Die Ansicht wird vom Controller in Liste 3 zurückgegeben. Beachten Sie, dass die Index()-Aktion mit einem [OutputCache]-Attribut versehen ist, das bewirkt, dass die Indexansicht 60 Sekunden lang zwischengespeichert wird.

**Auflisten 3 – Controllers-HomeController.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

Obwohl die Indexansicht zwischengespeichert wird, werden beim Anfordern der Indexseite verschiedene zufällige Nachrichten elemente angezeigt. Wenn Sie die Indexseite anfordern, ändert sich die von der Seite angezeigte Zeit 60 Sekunden lang nicht (siehe Abbildung 1). Die Tatsache, dass sich die Zeit nicht ändert, beweist, dass die Seite zwischengespeichert ist. Der von der WriteSubstitution()-Methode – dem zufälligen Nachrichtenelement – eingefügte Inhalt ändert sich jedoch mit jeder Anforderung .

**Abbildung 1: Einfügen dynamischer Nachrichtenelemente in eine zwischengespeicherte Seite**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Verwenden der Post-Cache-Ersetzung in Hilfsmethoden

Eine einfachere Möglichkeit, die Post-Cache-Ersetzung zu nutzen, besteht darin, den Aufruf der WriteSubstitution()-Methode innerhalb einer benutzerdefinierten Hilfsmethode zu kapseln. Dieser Ansatz wird durch die Hilfsmethode in Liste 4 veranschaulicht.

**Auflistung 4 – AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

Listing 4 enthält eine statische Klasse, die zwei Methoden verfügbar macht: RenderBanner() und RenderBannerInternal(). Die RenderBanner()-Methode stellt die eigentliche Hilfsmethode dar. Diese Methode erweitert die Standard-ASP.NET MVC-HtmlHelper-Klasse, sodass Sie Html.RenderBanner() in einer Ansicht wie jede andere Hilfsmethode aufrufen können.

Die RenderBanner()-Methode ruft die HttpResponse.WriteSubstitution()-Methode auf, die die RenderBannerInternal()-Methode an die WriteSubstitution()-Methode übergibt.

Die RenderBannerInternal()-Methode ist eine private Methode. Diese Methode wird nicht als Hilfsmethode verfügbar gemacht. Die RenderBannerInternal()-Methode gibt nach dem Zufallsprinzip ein Banner-Werbebild aus einer Liste von drei Banner-Werbebildern zurück.

Die geänderte Indexansicht in Liste 5 veranschaulicht, wie Sie die RenderBanner()-Hilfsmethode verwenden können. Beachten Sie, &lt;dass oben&gt; in der Ansicht eine zusätzliche %-Import %-Direktive zum Importieren des Namespace MvcApplication1.Helpers enthalten ist. Wenn Sie es versäumen, diesen Namespace zu importieren, wird die RenderBanner()-Methode nicht als Methode für die Html-Eigenschaft angezeigt.

**Auflisten 5 – Views-Home-Index.aspx (mit RenderBanner()-Methode)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

Wenn Sie die von der Ansicht in Liste 5 gerenderte Seite anfordern, wird bei jeder Anforderung eine andere Bannerankündigung angezeigt (siehe Abbildung 2). Die Seite wird zwischengespeichert, aber die Bannerankündigung wird dynamisch von der RenderBanner()-Hilfsmethode eingefügt.

**Abbildung 2 – Die Indexansicht, in der eine zufällige Bannerwerbung angezeigt wird**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>Zusammenfassung

In diesem Tutorial wurde erläutert, wie Sie Inhalte auf einer zwischengespeicherten Seite dynamisch aktualisieren können. Sie haben gelernt, wie Sie die HttpResponse.WriteSubstitution()-Methode verwenden, um das Einfügen dynamischer Inhalte in eine zwischengespeicherte Seite zu ermöglichen. Sie haben auch gelernt, wie Sie den Aufruf der WriteSubstitution()-Methode innerhalb einer HTML-Hilfsmethode kapseln.

Nutzen Sie das Caching, wann immer es möglich ist – es kann sich dramatisch auf die Leistung Ihrer Webanwendungen auswirken. Wie in diesem Tutorial erläutert, können Sie das Zwischenspeichern auch dann nutzen, wenn Sie dynamischen Inhalt auf Ihren Seiten anzeigen müssen.

> [!div class="step-by-step"]
> [Zurück](improving-performance-with-output-caching-cs.md)
> [Weiter](creating-a-controller-cs.md)
