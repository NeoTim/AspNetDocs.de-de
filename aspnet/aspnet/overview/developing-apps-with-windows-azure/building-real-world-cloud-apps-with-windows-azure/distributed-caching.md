---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: Verteiltes Caching (Erstellen von Echtzeit-Cloud-Apps mit Azure) | Microsoft Docs
author: MikeWasson
description: Das Building Real World Cloud Apps mit Azure E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es erklärt 13 Muster und Praktiken, die er...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675658"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>Verteiltes Caching (Erstellen von Echtzeit-Cloud-Apps mit Azure)

von [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project herunterladen](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) oder [E-Book herunterladen](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Das **Building Real World Cloud Apps mit Azure** E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es werden 13 Muster und Vorgehensweisen erläutert, die Ihnen bei der erfolgreichen Entwicklung von Web-Apps für die Cloud helfen können. Informationen zum E-Book finden Sie [im ersten Kapitel](introduction.md).

Im vorherigen Kapitel ging es um die vorübergehende Fehlerbehandlung und erwähnte die Zwischenspeicherung als Schutzschalterstrategie. Dieses Kapitel enthält mehr Hintergrundinformationen zum Zwischenspeichern, einschließlich der Verwendung, der allgemeinen Muster für die Verwendung und der Implementierung in Azure.

## <a name="what-is-distributed-caching"></a>Was ist verteiltes Caching

Ein Cache bietet zugriff auf häufig verwendete Anwendungsdaten mit hohem Durchsatz und geringer Latenz, indem die Daten im Arbeitsspeicher gespeichert werden. Für eine Cloud-App ist der nützlichste Cache-Typ verteilter Cache, d. h. die Daten werden nicht im Arbeitsspeicher des einzelnen Webservers, sondern auf anderen Cloudressourcen gespeichert, und die zwischengespeicherten Daten werden allen Webservern einer Anwendung (oder anderen Cloud-VMs, die von der Anwendung verwendet werden) zur Verfügung gestellt.

![Diagramm mit mehreren Webservern, die auf dieselben Cacheserver zugreifen](distributed-caching/_static/image1.png)

Wenn die Anwendung durch Hinzufügen oder Entfernen von Servern skaliert wird oder wenn Server aufgrund von Upgrades oder Fehlern ersetzt werden, bleiben die zwischengespeicherten Daten für jeden Server zugänglich, auf dem die Anwendung ausgeführt wird.

Durch die Vermeidung des hohen Latenzdatenzugriffs eines persistenten Datenspeichers kann das Zwischenspeichern die Reaktionsfähigkeit der Anwendung erheblich verbessern. Beispielsweise ist das Abrufen von Daten aus dem Cache viel schneller als das Abrufen aus einer relationalen Datenbank.

Ein Nebenvorteil der Zwischenspeicherung ist der reduzierte Datenverkehr zum persistenten Datenspeicher, was zu niedrigeren Kosten führen kann, wenn Datenausgangsgebühren für den persistenten Datenspeicher anfallen.

## <a name="when-to-use-distributed-caching"></a>Verwendung von verteilter Zwischenspeicherung

Zwischenspeichern eignet sich am besten für Anwendungsworkloads, die mehr lesen als das Schreiben von Daten ermöglichen, und wenn das Datenmodell die Schlüssel-/Wertorganisation unterstützt, die Sie zum Speichern und Abrufen von Daten im Cache verwenden. Es ist auch nützlicher, wenn Anwendungsbenutzer viele gemeinsame Daten gemeinsam nutzen. Beispielsweise würde der Cache nicht so viele Vorteile bieten, wenn jeder Benutzer in der Regel eindeutige Daten abruft. Ein Beispiel, bei dem das Zwischenspeichern sehr vorteilhaft sein könnte, ist ein Produktkatalog, da sich die Daten nicht häufig ändern und alle Kunden dieselben Daten betrachten.

Der Nutzen des Zwischenspeicherns wird umso messbarer, je mehr eine Anwendungsskalierung auftritt, da die Durchsatzgrenzen und Latenzverzögerungen des persistenten Datenspeichers zu einer stärkeren Einschränkung der Gesamtanwendungsleistung werden. Sie können jedoch auch aus anderen Gründen als der Leistung zwischen vordere Stellen implementieren. Für Daten, die nicht auf dem neuesten Stand sein müssen, wenn sie dem Benutzer angezeigt werden, kann der Cachezugriff als Leistungsschalter dienen, wenn der persistente Datenspeicher nicht reagiert oder nicht verfügbar ist.

## <a name="popular-cache-population-strategies"></a>Beliebte Cache-Bevölkerungsstrategien

Um Daten aus dem Cache abrufen zu können, müssen Sie sie zuerst dort speichern. Es gibt mehrere Strategien, um Daten, die Sie benötigen, in einen Cache zu bekommen:

- On Demand / Cache Aside

    Die Anwendung versucht, Daten aus dem Cache abzurufen, und wenn der Cache nicht über die Daten verfügt (ein "Fehler"), speichert die Anwendung die Daten im Cache, sodass sie beim nächsten Mal verfügbar sind. Wenn die Anwendung das nächste Mal versucht, dieselben Daten zu erhalten, findet sie, was sie sucht, im Cache (ein "Treffer"). Um das Abrufen zwischengespeicherter Daten zu verhindern, die sich in der Datenbank geändert haben, löschen Sie den Cache, wenn Sie Änderungen am Datenspeicher vornehmen.
- Hintergrunddaten-Push

    Hintergrunddienste übertragen Daten regelmäßig in den Cache, und die App wird immer aus dem Cache abziehbar. Dieser Ansatz funktioniert hervorragend mit Datenquellen mit hoher Latenz, für die Sie nicht immer die neuesten Daten zurückgeben müssen.
- Trennschalter

    Die Anwendung kommuniziert normalerweise direkt mit dem persistenten Datenspeicher, aber wenn der persistente Datenspeicher Verfügbarkeitsprobleme aufweist, ruft die Anwendung Daten aus dem Cache ab. Möglicherweise wurden Daten mithilfe der Cache-Seite oder der Hintergrunddaten-Push-Strategie in den Cache eingelegt. Dies ist eine Fehlerbehandlungsstrategie und keine leistungssteigernde Strategie.

Um Daten im Cache aktuell zu halten, können Sie zugehörige Cacheeinträge löschen, wenn Ihre Anwendung Daten erstellt, aktualisiert oder löscht. Wenn es für Ihre Anwendung in Ordnung ist, manchmal Daten zu erhalten, die etwas veraltet sind, können Sie sich auf eine konfigurierbare Ablaufzeit verlassen, um eine Begrenzung für die Art und Weise festzulegen, wie alte Cachedaten sein können.

Sie können den absoluten Ablauf (Zeitraum seit der Erstellung des Cacheelements) oder den gleitenden Ablauf (Zeitraum seit dem letzten Zugriff auf ein Cacheelement) konfigurieren. AbsoluteAblaufwird verwendet, wenn Sie vom Cacheablaufmechanismus abhängig sind, um zu verhindern, dass die Daten zu veraltet werden. In der Fix It-App entfernen wir veraltete Cacheelemente manuell und verwenden gleitenden Ablauf, um die aktuellsten Daten im Cache zu speichern. Unabhängig von der gewählten Ablaufrichtlinie entfernt der Cache automatisch die ältesten Elemente (Least Recently Used oder LRU), wenn das Speicherlimit des Caches erreicht ist.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Beispiel für Cache-Aside-Code für Fix It App

Im folgenden Beispielcode überprüfen wir zuerst den Cache, wenn wir eine Fix It-Aufgabe abrufen. Wenn die Aufgabe im Cache gefunden wird, geben wir sie zurück. Wenn nicht gefunden, erhalten wir es aus der Datenbank und speichern es im Cache. Die Änderungen, die Sie vornehmen würden, um der `FindTaskByIdAsync` Methode Zwischenspeicherung hinzuzufügen, werden hervorgehoben.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Wenn Sie einen Fix It-Task aktualisieren oder löschen, müssen Sie die zwischengespeicherte Aufgabe für ungültig erklären (entfernen). Andernfalls werden zukünftige Versuche, diese Aufgabe zu lesen, weiterhin die alten Daten aus dem Cache abrufen.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

Dies sind Beispiele zur Veranschaulichung von einfachem Zwischenspeicherungscode. Caching wurde im herunterladbaren Fix It-Projekt nicht implementiert.

## <a name="azure-caching-services"></a>Azure-Caching-Dienste

Azure bietet die folgenden Zwischenspeicherungsdienste: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) und [Azure Managed Cache](https://msdn.microsoft.com/library/dn386094.aspx). Der Azure Redis-Cache basiert auf dem beliebten [Open-Source-Redis-Cache](http://redis.io/) und ist die erste Wahl für die meisten Caching-Szenarien.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>ASP.NET Sitzungsstatus mithilfe eines Cacheanbieters

Wie im [Kapitel Best Practices](web-development-best-practices.md)für die Webentwicklung erwähnt, ist es eine bewährte Methode, die Verwendung des Sitzungsstatus zu vermeiden. Wenn Für Ihre Anwendung sitzungsstatus erforderlich ist, ist es die nächste bewährte Methode, den standardmäßigen In-Memory-Anbieter zu vermeiden, da dies keine horizontalen Skalierungsinstanzen (mehrere Instanzen des Webservers) aktiviert. Der ASP.NET SQL Server-Sitzungsstatusanbieter ermöglicht einer Site, die auf mehreren Webservern ausgeführt wird, die Verwendung des Sitzungsstatus, verursacht jedoch hohe Latenzkosten im Vergleich zu einem In-Memory-Anbieter. Die beste Lösung, wenn Sie den Sitzungsstatus verwenden müssen, ist die Verwendung eines Cacheanbieters, z. B. des [Sitzungsstatusanbieters für Azure Cache](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx).

## <a name="summary"></a>Zusammenfassung

Sie haben gesehen, wie die Fix It-App caching implementieren kann, um die Reaktionszeit und Skalierbarkeit zu verbessern und die App weiterhin für Lesevorgänge reagieren zu können, wenn die Datenbank nicht verfügbar ist. Im [nächsten Kapitel](queue-centric-work-pattern.md) wird gezeigt, wie Sie die Skalierbarkeit weiter verbessern und die App weiterhin für Schreibvorgänge ansprechen.

## <a name="resources"></a>Ressourcen

Weitere Informationen zum Zwischenspeichern finden Sie in den folgenden Ressourcen.

Dokumentation

- [Azure Cache](https://msdn.microsoft.com/library/gg278356.aspx). Offizielle MSDN-Dokumentation zum Zwischenspeichern in Azure.
- [Microsoft-Muster und -Praktiken - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx). Siehe Caching-Anleitung und Cache-Aside-Muster.
- [Failsafe: Anleitung für resiliente Cloud-Architekturen](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx). Whitepaper von Marc Mercuri, Ulrich Homann und Andrew Townhill. Siehe Abschnitt zum Caching.
- [Bewährte Methoden für den Entwurf großer Dienste in Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). W. Whitepaper von Mark Simms und Michael Thomassy. Siehe Abschnitt zum verteilten Zwischenspeichern.
- [Verteiltes Caching auf dem Pfad zur Skalierbarkeit](https://msdn.microsoft.com/magazine/dd942840.aspx). Ein älterer Artikel (2009) des MSDN Magazine, aber eine klar geschriebene Einführung in das verteilte Caching im Allgemeinen; geht in die Tiefe als die Caching-Abschnitte der Whitepapers FailSafe und Best Practices.

Videos

- [FailSafe: Erstellen skalierbarer, widerstandsfähiger Cloud-Services](https://channel9.msdn.com/Series/FailSafe). Neunteilige Serie von Ulrich Homann, Marc Mercuri und Mark Simms. Bietet eine 400-Level-Ansicht zum Entwerfen von Cloud-Apps. Diese Serie konzentriert sich auf Theorie und Gründe, warum; Weitere Informationen finden Sie in der Building Big Serie von Mark Simms. Sehen Sie die Caching-Diskussion in Folge 3 ab 1:24:14.
- [Groß erstellen: Lehren aus Azure-Kunden - Teil I](https://channel9.msdn.com/Events/Build/2012/3-029). Simon Davies spricht über verteiltes Caching ab 46:00 Uhr. Ähnlich wie bei der Failsafe-Serie, geht aber mehr How-to-Details. Die Präsentation wurde am 31. Oktober 2012 gehalten, sodass sie nicht den Caching-Dienst von Web-Apps in Azure App Service abdeckt, der 2013 eingeführt wurde.

Codebeispiel

- [Cloud Dienstgrundlagen in Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Beispielanwendung, die verteiltes Zwischenspeichern implementiert. Siehe den begleitenden Blogbeitrag [Cloud Service Fundamentals – Caching Basics](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx).

> [!div class="step-by-step"]
> [Zurück](transient-fault-handling.md)
> [Weiter](queue-centric-work-pattern.md)
