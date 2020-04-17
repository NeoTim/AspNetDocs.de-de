---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Effizientes Daten-Paging implementieren | Microsoft Docs
author: rick-anderson
description: Schritt 8 zeigt, wie Sie Paging-Unterstützung zu unserer /Dinners URL hinzufügen, so dass wir statt 1000 Abendessen auf einmal nur 10 bevorstehende Abendessen bei...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541324"
---
# <a name="implement-efficient-data-paging"></a>Implementieren einer effizienten Datenauslagerung

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 8 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 8 zeigt, wie Sie Paging-Unterstützung zu unserer /Dinners-URL hinzufügen, so dass wir, anstatt 1000 Abendessen gleichzeitig anzuzeigen, nur 10 bevorstehende Abendessen gleichzeitig anzeigen - und endbenutzern erlauben, die gesamte Liste auf SEO-freundliche Weise zurück und vorwärts zu blättern.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner Schritt 8: Paging-Unterstützung

Wenn unsere Website erfolgreich ist, wird es Tausende von bevorstehenden Abendessen haben. Wir müssen sicherstellen, dass unsere Benutzeroberfläche skaliert wird, um alle diese Abendessen zu verarbeiten, und es Benutzern ermöglicht, sie zu durchsuchen. Um dies zu ermöglichen, fügen wir paging-Unterstützung zu unserer */Dinners* URL hinzu, so dass wir, anstatt 1000 Abendessen gleichzeitig anzuzeigen, nur 10 bevorstehende Abendessen gleichzeitig anzeigen - und Es Endbenutzern ermöglichen, die gesamte Liste auf SEO-freundliche Weise zurück und vorwärts zu blättern.

### <a name="index-action-method-recap"></a>Index() Action-Methoden-Zusammenfassung

Die Index()-Aktionsmethode in unserer DinnersController-Klasse sieht derzeit wie folgt aus:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

Wenn eine Anfrage an die */Dinners-URL* gestellt wird, ruft sie eine Liste aller bevorstehenden Abendessen ab und rendert dann eine Liste aller abendessen:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>IQueryable&lt;T verstehen&gt;

*IQueryable&lt;&gt; T* ist eine Schnittstelle, die mit LINQ als Teil von .NET 3.5 eingeführt wurde. Es ermöglicht leistungsstarke "verzögerte Ausführungsszenarien", die wir nutzen können, um Paging-Unterstützung zu implementieren.

In unserem DinnerRepository geben wir&lt;eine&gt; IQueryable Dinner-Sequenz von unserer FindUpcomingDinners()-Methode zurück:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

Das IQueryable&gt; Dinner-Objekt,&lt;das von unserer FindUpcomingDinners()-Methode zurückgegeben wird, kapselt eine Abfrage, um Dinner-Objekte aus unserer Datenbank mit LINQ zu SQL abzurufen. Wichtig ist, dass die Abfrage für die Datenbank erst ausgeführt wird, wenn wir versuchen, auf die Daten in der Abfrage zuzugreifen/iterieren oder bis wir die ToList()-Methode darauf aufrufen. Der Code, der unsere FindUpcomingDinners()-Methode aufruft, kann optional festlegen, dass&lt;&gt; dem IQueryable Dinner-Objekt zusätzliche "verkettete" Operationen/Filter hinzugefügt werden, bevor die Abfrage ausgeführt wird. LINQ to SQL ist dann intelligent genug, um die kombinierte Abfrage für die Datenbank auszuführen, wenn die Daten angefordert werden.

Um Die Paging-Logik zu implementieren, können wir die Index()-Aktionsmethode unseres DinnersControllers aktualisieren, sodass&lt;&gt; sie zusätzliche "Skip"- und "Take"-Operatoren auf die zurückgegebene IQueryable Dinner-Sequenz anwendet, bevor ToList() darauf aufgerufen wird:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

Der obige Code überspringt die ersten 10 bevorstehenden Abendessen in der Datenbank und gibt dann 20 Abendessen zurück. LINQ to SQL ist intelligent genug, um eine optimierte SQL-Abfrage zu erstellen, die diese Übersprunglogik in der SQL-Datenbank und nicht im Webserver ausführt. Das bedeutet, dass selbst wenn wir Millionen von kommenden Dinners in der Datenbank haben, nur die 10, die wir wollen, als Teil dieser Anfrage abgerufen werden (was sie effizient und skalierbar macht).

### <a name="adding-a-page-value-to-the-url"></a>Hinzufügen eines "Seiten"-Werts zur URL

Anstatt einen bestimmten Seitenbereich hart zu codieren, möchten wir, dass unsere URLs einen "Seite"-Parameter enthalten, der angibt, welchen Dinnerbereich ein Benutzer anfordert.

#### <a name="using-a-querystring-value"></a>Verwenden eines Querystring-Werts

Der folgende Code zeigt, wie wir unsere Index()-Aktionsmethode aktualisieren können, um einen Querystring-Parameter zu unterstützen und URLs wie */Dinners?page=2*zu aktivieren:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

Die oben genannte Index()-Aktionsmethode hat einen Parameter mit dem Namen "page". Der Parameter wird als nullbare ganze Zahl deklariert (das ist, was int? angibt). Dies bedeutet, dass die *URL /Dinners?page=2* dazu führt, dass der Wert "2" als Parameterwert übergeben wird. Die */Dinners-URL* (ohne Abfragezeichenfolgenwert) bewirkt, dass ein NULL-Wert übergeben wird.

Wir multiplizieren den Seitenwert mit der Seitengröße (in diesem Fall 10 Zeilen), um zu bestimmen, wie viele Abendessen übersprungen werden sollen. Wir verwenden den [Operator "koaleszieren" (??),](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) der beim Umgang mit null-fähigen Typen nützlich ist. Der obige Code weist der Seite den Wert 0 zu, wenn der Seitenparameter null ist.

#### <a name="using-embedded-url-values"></a>Verwenden eingebetteter URL-Werte

Eine Alternative zur Verwendung eines Abfragezeichenfolgenwerts wäre das Einbetten des Seitenparameters in die tatsächliche URL selbst. Beispiel: */Dinners/Page/2* oder */Dinners/2*. ASP.NET MVC enthält ein leistungsstarkes URL-Routing-Modul, das es einfach macht, Szenarien wie diese zu unterstützen.

Wir können benutzerdefinierte Routingregeln registrieren, die jede eingehende URL oder jedes URL-Format jeder gewünschten Controllerklasse oder -aktionsmethode zuordnen. Alles, was wir tun müssen, ist die Datei Global.asax in unserem Projekt zu öffnen:

![](implement-efficient-data-paging/_static/image2.png)

Und registrieren Sie dann eine neue Zuordnungsregel mit der MapRoute()-Hilfsmethode wie dem ersten Aufruf von Routen. MapRoute() unten:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Oben registrieren wir eine neue Routing-Regel namens "UpcomingDinners". Wir geben an, dass es das URL-Format "Dinners/Page/"-Seite" hat – wobei "Page" ein In-URL eingebetteter Parameterwert ist. Der dritte Parameter der MapRoute()-Methode gibt an, dass wir URLs, die diesem Format entsprechen, der Index()-Aktionsmethode in der DinnersController-Klasse zuordnen sollten.

Wir können genau den gleichen Index()-Code verwenden, den wir zuvor mit unserem Querystring-Szenario hatten – außer jetzt kommt unser "Seite"-Parameter von der URL und nicht von der Abfragezeichenfolge:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

Und jetzt, wenn wir die Anwendung ausführen und */Dinners* eingeben, werden wir die ersten 10 bevorstehenden Abendessen sehen:

![](implement-efficient-data-paging/_static/image3.png)

Und wenn wir */Dinners/Page/1* eingeben, sehen wir die nächste Seite der Abendessen:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Hinzufügen der Seitennavigations-Benutzeroberfläche

Der letzte Schritt zum Abschließen unseres Paging-Szenarios besteht darin, die "nächste" und "vorherige" Navigationsbenutzeroberfläche in unserer Ansichtsvorlage zu implementieren, damit Benutzer die Dinner-Daten einfach überspringen können.

Um dies korrekt zu implementieren, müssen wir die Gesamtzahl der Abendessen in der Datenbank kennen, sowie wissen, wie viele Seiten Daten dies übersetzt. Wir müssen dann berechnen, ob sich der aktuell angeforderte "Seite"-Wert am Anfang oder Ende der Daten befindet, und die Benutzeroberfläche "vorherige" und "nächste" entsprechend ein- oder ausblenden. Wir könnten diese Logik innerhalb unserer Index()-Aktionsmethode implementieren. Alternativ können wir unserem Projekt eine Hilfsklasse hinzufügen, die diese Logik auf eine wiederverwendbarere Weise kapselt.

Im Folgenden finden Sie eine einfache "PaginatedList"-Hilfsklasse, die von der List&lt;T-Auflistungsklasse&gt; herleitet, die in .NET Framework integriert ist. Es implementiert eine wiederverwendbare Auflistungsklasse, die verwendet werden kann, um jede Sequenz von IQueryable-Daten zu paginieren. In unserer NerdDinner-Anwendung werden wir es&lt;über&gt; IQueryable Dinner Ergebnisse arbeiten lassen,&lt;aber&gt; es könnte&lt;&gt; genauso einfach gegen IQueryable Produkt oder IQueryable Kundenergebnisse in anderen Anwendungsszenarien verwendet werden:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

Beachten Sie oben, wie Eigenschaften wie "PageIndex", "PageSize", "TotalCount" und "TotalPages" berechnet und dann verfügbar gemacht werden. Anschließend werden außerdem zwei Hilfseigenschaften wie "HasPreviousPage" und "HasNextPage" verfügbar gemacht, die angeben, ob sich die Datenseite in der Auflistung am Anfang oder Ende der ursprünglichen Sequenz befindet. Der obige Code führt dazu, dass zwei SQL-Abfragen ausgeführt werden - die erste, die die Anzahl der Gesamten der Dinner-Objekte abruft (dies gibt die Objekte nicht zurück – stattdessen führt er eine "SELECT COUNT"-Anweisung aus, die eine ganze Zahl zurückgibt), und die zweite, um nur die Datenzeilen abzurufen, die wir für die aktuelle Datenseite aus unserer Datenbank benötigen.

Wir können dann unsere DinnersController.Index() Hilfsmethode aktualisieren, um&lt;&gt; ein PaginatedList Dinner aus unserem DinnerRepository.FindUpcomingDinners() Ergebnis zu erstellen, und es an unsere Ansichtsvorlage übergeben:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Wir können dann die Ansichtsvorlage "Views" aktualisieren, um sie&lt;von&lt;ViewPage NerdDinner.Helpers.PaginatedList Dinner&gt; &gt; anstelle von ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;zu erben, und dann den folgenden Code am unteren Rand unserer Ansichtsvorlage hinzufügen, um die nächste und vorherige Navigationsbenutzeroberfläche ein- oder auszublenden:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Beachten Sie oben, wie wir die Html.RouteLink()-Hilfsmethode verwenden, um unsere Hyperlinks zu generieren. Diese Methode ähnelt der Html.ActionLink()-Hilfsmethode, die wir zuvor verwendet haben. Der Unterschied besteht darin, dass wir die URL mit der Routingregel "UpcomingDinners" generieren, die wir in unserer Datei Global.asax einrichten. Dadurch wird sichergestellt, dass wir URLs für unsere Index()-Aktionsmethode generieren, die das Format *haben: /Dinners/Page/-Seite* – wobei der Wert "seite" eine Variable ist, die wir oben basierend auf dem aktuellen PageIndex bereitstellen.

Und jetzt, wenn wir unsere Anwendung wieder ausführen, sehen wir 10 Abendessen gleichzeitig in unserem Browser:

![](implement-efficient-data-paging/_static/image5.png)

Wir haben &lt; &lt; &lt; &gt; &gt; &gt; auch und Navigation UI am unteren Rand der Seite, die uns erlaubt, vorwärts und rückwärts über unsere Daten mit Suchmaschine zugängliche URLs zu überspringen:

![](implement-efficient-data-paging/_static/image6.png)

| **Side Topic: Verstehen der Auswirkungen&lt;von IQueryable T&gt;** |
| --- |
| IQueryable&lt;&gt; T ist eine sehr leistungsfähige Funktion, die eine Vielzahl interessanter Szenarien für die verzögerte Ausführung (z. B. Paging- und kompositionsbasierte Abfragen) ermöglicht. Wie bei allen leistungsstarken Funktionen, sie möchten Sie vorsichtig sein, wie Sie es verwenden und sicherstellen, dass es nicht missbraucht wird. Es ist wichtig zu erkennen,&lt;dass&gt; das Zurückgeben eines IQueryable T-Ergebnisses aus Ihrem Repository das Aufrufen von Code ermöglicht, um verkettete Operatormethoden an ihn anzuhängen, und daher an der ultimativen Abfrageausführung teilnehmen kann. Wenn Sie diesen Aufrufcode nicht bereitstellen möchten, sollten Sie&lt;&gt; IList T-&lt;oder&gt; IEnumerable T-Ergebnisse zurückgeben, die die Ergebnisse einer bereits ausgeführten Abfrage enthalten. Für Paginierungsszenarien müssten Sie die eigentliche Datenpaginationslogik in die repository-Methode übertragen, die aufgerufen wird. In diesem Szenario können wir unsere FindUpcomingDinners()-Findermethode aktualisieren, um eine Signatur zu&lt; haben,&gt; die entweder eine PaginatedList: PaginatedList Dinner FindUpcomingDinners(int pageIndex, int pageSize) zurückgegeben hat, oder ein IList&lt;Dinner&gt;zurückgibt, und verwenden Sie ein "totalCount" out param, um die Gesamtzahl der Dinners zurückzugeben: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out |

### <a name="next-step"></a>Nächster Schritt

Sehen wir uns nun an, wie wir unserer Anwendung Authentifizierungs- und Autorisierungsunterstützung hinzufügen können.

> [!div class="step-by-step"]
> [Zurück](re-use-ui-using-master-pages-and-partials.md)
> [Weiter](secure-applications-using-authentication-and-authorization.md)
