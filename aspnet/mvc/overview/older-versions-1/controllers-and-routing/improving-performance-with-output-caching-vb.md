---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: Verbesserung der Leistung mit Output Caching (VB) | Microsoft Docs
author: rick-anderson
description: In diesem Tutorial erfahren Sie, wie Sie die Leistung Ihrer ASP.NET MVC-Webanwendungen erheblich verbessern können, indem Sie die Ausgabezwischenspeicherung nutzen. Sie...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: e18d4c5132d4dccc97f1465e7885c9c47a0edab1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542689"
---
# <a name="improving-performance-with-output-caching-vb"></a>Verbessern der Leistung mit Ausgabezwischenspeicherung (VB)

von [Microsoft](https://github.com/microsoft)

> In diesem Tutorial erfahren Sie, wie Sie die Leistung Ihrer ASP.NET MVC-Webanwendungen erheblich verbessern können, indem Sie die Ausgabezwischenspeicherung nutzen. Sie erfahren, wie Sie das von einer Controlleraktion zurückgegebene Ergebnis zwischenspeichern, sodass nicht jedes Mal, wenn ein neuer Benutzer die Aktion aufruft, derselbe Inhalt erstellt werden muss.

Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie die Leistung einer ASP.NET MVC-Anwendung durch Die Nutzung des Ausgabecache erheblich verbessern können. Mit dem Ausgabecache können Sie den von einer Controlleraktion zurückgegebenen Inhalt zwischenspeichern. Auf diese Weise muss derselbe Inhalt nicht jedes Mal generiert werden, wenn dieselbe Controlleraktion aufgerufen wird.

Stellen Sie sich z. B. vor, dass Ihre ASP.NET MVC-Anwendung eine Liste von Datenbankdatensätzen in einer Ansicht mit dem Namen Index anzeigt. Normalerweise muss jedes Mal, wenn ein Benutzer die Controlleraktion aufruft, die die Indexansicht zurückgibt, der Satz von Datenbankdatensätzen aus der Datenbank abgerufen werden, indem eine Datenbankabfrage ausgeführt wird.

Wenn Sie hingegen den Ausgabecache nutzen, können Sie die Ausführung einer Datenbankabfrage vermeiden, wenn ein Benutzer dieselbe Controlleraktion aufruft. Die Ansicht kann aus dem Cache abgerufen werden, anstatt von der Controlleraktion regeneriert zu werden. Durch das Zwischenspeichern können Sie redundante Arbeiten auf dem Server vermeiden.

#### <a name="enabling-output-caching"></a>Aktivieren der Ausgangszwischenspeicherung

Sie aktivieren die Ausgabezwischenspeicherung, indem Sie entweder einer einzelnen Controlleraktion oder einer gesamten Controllerklasse ein &lt;OutputCache-Attribut&gt; hinzufügen. Beispielsweise macht der Controller in Listing 1 eine Aktion mit dem Namen Index() verfügbar. Die Ausgabe der Index()-Aktion wird für 10 Sekunden zwischengespeichert.

**Auflisten 1 – Controller-HomeController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

In den Betaversionen von ASP.NET MVC funktioniert die Ausgabezwischenspeicherung für eine URL wie [http://www.MySite.com/](http://www.mysite.com/)nicht . Stattdessen müssen Sie eine [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)URL wie eingeben.

In Listing 1 wird die Ausgabe der Index()-Aktion für 10 Sekunden zwischengespeichert. Wenn Sie möchten, können Sie eine viel längere Cachedauer angeben. Wenn Sie beispielsweise die Ausgabe einer Controlleraktion für einen Tag zwischenspeichern möchten, können Sie eine Cachedauer \* von \* 86400 Sekunden (60 Sekunden 60 Minuten und 24 Stunden) angeben.

Es gibt keine Garantie dafür, dass Inhalte für den von Ihnen angegebenen Zeitraum zwischengespeichert werden. Wenn die Speicherressourcen niedrig werden, beginnt der Cache automatisch mit dem Entfernen von Inhalten.

Der Home-Controller in Listing 1 gibt die Indexansicht in Listing 2 zurück. Es gibt nichts Besonderes an dieser Ansicht. In der Indexansicht wird einfach die aktuelle Uhrzeit angezeigt (siehe Abbildung 1).

**Auflisten 2 – Ansichten, Home, Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**Abbildung 1 – Ansicht zwischengespeicherter Index**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

Wenn Sie die Index()-Aktion mehrmals aufrufen, indem Sie die URL /Home/Index in die Adressleiste Ihres Browsers eingeben und wiederholt auf die Schaltfläche Aktualisieren/Erneut laden in Ihrem Browser klicken, ändert sich die von der Indexansicht angezeigte Zeit 10 Sekunden lang nicht. Die gleiche Zeit wird angezeigt, da die Ansicht zwischengespeichert wird.

Es ist wichtig zu verstehen, dass die gleiche Ansicht für alle Benutzer, die Ihre Anwendung besuchen, zwischengespeichert wird. Jeder, der die Index()-Aktion aufruft, erhält dieselbe zwischengespeicherte Version der Indexansicht. Dies bedeutet, dass der Arbeitsaufwand, den der Webserver ausführen muss, um die Indexansicht zu bedienen, drastisch reduziert wird.

Die Ansicht in Listing 2 geschieht, etwas wirklich einfaches zu tun. In der Ansicht wird nur die aktuelle Uhrzeit angezeigt. Sie können jedoch genauso einfach eine Ansicht zwischenspeichern, die eine Reihe von Datenbankdatensätzen anzeigt. In diesem Fall muss der Satz von Datenbankdatensätzen nicht jedes Mal aus der Datenbank abgerufen werden, wenn die Controlleraktion aufgerufen wird, die die Ansicht zurückgibt. Zwischenspeichern kann den Arbeitsaufwand reduzieren, den sowohl der Webserver als auch der Datenbankserver ausführen müssen.

Verwenden Sie in &lt;einer MVC-Ansicht nicht die Direktive "Seite %" "OutputCache %".&gt; Diese Direktive blutet aus der Web Forms-Welt aus und sollte nicht in einer ASP.NET MVC-Anwendung verwendet werden. 

#### <a name="where-content-is-cached"></a>Wo Inhalte zwischengespeichert werden

Wenn Sie das &lt;OutputCache-Attribut&gt; verwenden, werden Inhalte standardmäßig an drei Speicherorten zwischengespeichert: dem Webserver, allen Proxyservern und dem Webbrowser. Sie können genau steuern, wo Inhalte zwischengespeichert werden, indem Sie die Location-Eigenschaft des &lt;OutputCache-Attributs&gt; ändern.

Sie können die Location-Eigenschaft auf einen der folgenden Werte festlegen:

> · jegliche
> 
> · Kunde
> 
> · Nachgeschaltete
> 
> · Server
> 
> · nichts
> 
> · ServerAndClient

Standardmäßig hat die Location-Eigenschaft den Wert Any. Es gibt jedoch Situationen, in denen Sie möglicherweise nur im Browser oder nur auf dem Server zwischenspeichern möchten. Wenn Sie z. B. Informationen zwischenspeichern, die für jeden Benutzer personalisiert sind, sollten Sie die Informationen nicht auf dem Server zwischenspeichern. Wenn Sie verschiedenen Benutzern unterschiedliche Informationen anzeigen, sollten Sie die Informationen nur auf dem Client zwischenspeichern.

Beispielsweise macht der Controller in Listing 3 eine Aktion mit dem Namen GetName(verfügbar, die den aktuellen Benutzernamen zurückgibt. Wenn Jack sich bei der Website anmeldet und die GetName()-Aktion aufruft, gibt die Aktion die Zeichenfolge "Hi Jack" zurück. Wenn sich Jill anschließend bei der Website anmeldet und die GetName()-Aktion aufruft, erhält sie auch die Zeichenfolge "Hi Jack". Die Zeichenfolge wird auf dem Webserver für alle Benutzer zwischengespeichert, nachdem Jack die Controlleraktion zunächst aufgerufen hat.

**Auflisten 3 – Controller-BadUserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

Höchstwahrscheinlich funktioniert der Controller in Listing 3 nicht so, wie Sie möchten. Sie möchten Jill nicht die Meldung "Hi Jack" anzeigen.

Sie sollten niemals personalisierte Inhalte im Servercache zwischenspeichern. Sie können jedoch den personalisierten Inhalt im Browsercache zwischenspeichern, um die Leistung zu verbessern. Wenn Sie Inhalte im Browser zwischenspeichern und ein Benutzer dieselbe Controlleraktion mehrmals aufruft, kann der Inhalt aus dem Browsercache anstelle des Servers abgerufen werden.

Der geänderte Controller in Listing 4 speichert die Ausgabe der GetName()-Aktion zwischen. Der Inhalt wird jedoch nur im Browser und nicht auf dem Server zwischengespeichert. Auf diese Weise erhält jede Person, wenn mehrere Benutzer die GetName()-Methode aufrufen, ihren eigenen Benutzernamen und nicht den Benutzernamen einer anderen Person.

**Auflisten 4 – Controller-BenutzerController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

Beachten Sie, dass das &lt;OutputCache-Attribut&gt; in Listing 4 eine Location-Eigenschaft enthält, die auf den Wert OutputCacheLocation.Client festgelegt ist. Das &lt;OutputCache-Attribut&gt; enthält auch eine NoStore-Eigenschaft. Die NoStore-Eigenschaft wird verwendet, um Proxyserver und Browser darüber zu informieren, dass keine permanente Kopie des zwischengespeicherten Inhalts gespeichert werden soll.

#### <a name="varying-the-output-cache"></a>Ändern des Ausgabecache

In einigen Situationen möchten Sie möglicherweise unterschiedliche zwischengespeicherte Versionen desselben Inhalts. Stellen Sie sich beispielsweise vor, dass Sie eine Master-/Detailseite erstellen. Auf der Masterseite wird eine Liste der Filmtitel angezeigt. Wenn Sie auf einen Titel klicken, erhalten Sie Details für den ausgewählten Film.

Wenn Sie die Detailseite zwischenspeichern, werden die Details für denselben Film unabhängig davon angezeigt, auf welchen Film Sie klicken. Der erste Film, der vom ersten Benutzer ausgewählt wurde, wird allen zukünftigen Benutzern angezeigt.

Sie können dieses Problem beheben, indem Sie die &lt;VaryByParam-Eigenschaft des OutputCache-Attributs&gt; nutzen. Mit dieser Eigenschaft können Sie verschiedene zwischengespeicherte Versionen desselben Inhalts erstellen, wenn ein Formularparameter oder Abfragezeichenfolgenparameter variiert.

Beispielsweise macht der Controller in Listing 5 zwei Aktionen mit dem Namen Master() und Details() verfügbar. Die Master()-Aktion gibt eine Liste von Filmtiteln zurück, und die Aktion Details() gibt die Details für den ausgewählten Film zurück.

**Auflisten 5 – Controller-MoviesController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Die Master()-Aktion enthält eine VaryByParam-Eigenschaft mit dem Wert "none". Wenn die Master()-Aktion aufgerufen wird, wird dieselbe zwischengespeicherte Version der Masteransicht zurückgegeben. Alle Formularparameter oder Abfragezeichenfolgenparameter werden ignoriert (siehe Abbildung 2).

**Abbildung 2 – Die Ansicht /Movies/Master**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**Abbildung 3 : Die Ansicht /Movies/Details**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Die Aktion Details() enthält eine VaryByParam-Eigenschaft mit dem Wert "Id". Wenn unterschiedliche Werte des Id-Parameters an die Controlleraktion übergeben werden, werden verschiedene zwischengespeicherte Versionen der Detailansicht generiert.

Es ist wichtig zu verstehen, dass die Verwendung der VaryByParam-Eigenschaft zu mehr Zwischenspeicherung und nicht weniger führt. Für jede unterschiedliche Version des Id-Parameters wird eine andere zwischengespeicherte Version der Detailansicht erstellt.

Sie können die VaryByParam-Eigenschaft auf die folgenden Werte festlegen:

> \*= Erstellen Sie eine andere zwischengespeicherte Version, wenn ein Formular- oder Abfragezeichenfolgenparameter variiert.
> 
> none = Niemals verschiedene zwischengespeicherte Versionen erstellen
> 
> Semikolon-Liste der Parameter = Erstellen Sie verschiedene zwischengespeicherte Versionen, wenn sich die Parameter des Formulars oder der Abfragezeichenfolgen in der Liste ändern.

#### <a name="creating-a-cache-profile"></a>Erstellen eines Cacheprofils

Alternativ zum Konfigurieren von Ausgabecacheeigenschaften durch &lt;Ändern&gt; der Eigenschaften des OutputCache-Attributs können Sie ein Cacheprofil in der Webkonfigurationsdatei (web.config) erstellen. Das Erstellen eines Cacheprofils in der Webkonfigurationsdatei bietet einige wichtige Vorteile.

Erstens können Sie durch Konfigurieren der Ausgabezwischenspeicherung in der Webkonfigurationsdatei steuern, wie Controlleraktionen Inhalte an einem zentralen Speicherort zwischenspeichern. Sie können ein Cacheprofil erstellen und das Profil auf mehrere Controller oder Controlleraktionen anwenden.

Zweitens können Sie die Webkonfigurationsdatei ändern, ohne die Anwendung neu zu kompilieren. Wenn Sie die Zwischenspeicherung für eine Anwendung deaktivieren müssen, die bereits in der Produktion bereitgestellt wurde, können Sie einfach die in der Webkonfigurationsdatei definierten Cacheprofile ändern. Alle Änderungen an der Webkonfigurationsdatei werden automatisch erkannt und angewendet.

Der Abschnitt &lt;zwischen&gt; der Webkonfiguration in Liste 6 definiert beispielsweise ein Cacheprofil mit dem Namen Cache1Hour. Der &lt;Caching-Abschnitt&gt; muss &lt;im&gt; Abschnitt system.web einer Webkonfigurationsdatei angezeigt werden.

**Auflistung 6 – Caching-Bereich für web.config**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

Der Controller in Liste 7 veranschaulicht, wie Sie das Cache1Hour-Profil auf eine Controlleraktion mit dem &lt;OutputCache-Attribut&gt; anwenden können.

**Auflisten 7 – Controller-ProfileController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

Wenn Sie die Index()-Aktion aufrufen, die vom Controller in Liste 7 verfügbar gemacht wird, wird die gleiche Zeit für 1 Stunde zurückgegeben.

#### <a name="summary"></a>Zusammenfassung

Die Ausgangszwischenspeicherung bietet Ihnen eine sehr einfache Methode, um die Leistung Ihrer ASP.NET MVC-Anwendungen drastisch zu verbessern. In diesem Tutorial haben Sie &lt;gelernt,&gt; wie Sie das OutputCache-Attribut verwenden, um die Ausgabe von Controlleraktionen zwischenzuspeichern. Außerdem haben Sie gelernt, &lt;wie&gt; Sie Eigenschaften des OutputCache-Attributs ändern, z. B. die Eigenschaften Duration und VaryByParam, um zu ändern, wie Inhalte zwischengespeichert werden. Schließlich haben Sie gelernt, wie Sie Cacheprofile in der Webkonfigurationsdatei definieren.

> [!div class="step-by-step"]
> [Zurück](understanding-action-filters-vb.md)
> [Weiter](adding-dynamic-content-to-a-cached-page-vb.md)
