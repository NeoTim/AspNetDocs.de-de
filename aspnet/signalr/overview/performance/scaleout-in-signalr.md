---
uid: signalr/overview/performance/scaleout-in-signalr
title: Einführung zur horizontalen Skalierung in SignalR | Microsoft-Dokumentation
author: bradygaster
description: Version der Software verwendete in diesem Thema Visual Studio 2013 .NET 4.5 SignalR Version 2-Vorgängerversionen des in diesem Thema Informationen zu früheren Versionen von...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0d17308d1e97279c0870ea02933a42400ef338c9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59411552"
---
# <a name="introduction-to-scaleout-in-signalr"></a>Einführung zur horizontalen Skalierung in SignalR

durch [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendeten Softwareversionen
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR-Version 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Vorherige Versionen dieses Themas
>
> Weitere Informationen zu früheren Versionen von SignalR, finden Sie unter [ältere Versionen von SignalR](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
>
> Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können. Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).


Im Allgemeinen stehen zwei Möglichkeiten, eine Webanwendung zu skalieren: *zentral hochskalieren* und *horizontal hochskalieren*.

- Zentral hochskalieren bedeutet einen größeren Server (oder eine größere VM) mit mehr Arbeitsspeicher, CPUs usw. verwenden.
- Horizontales hochskalieren bedeutet, dass weitere Server hinzufügen, die Last zu bewältigen.

Das Problem mit Zentrales Skalieren ist, dass Sie schnell eine Begrenzung der Größe des Computers erreicht. Darüber hinaus müssen Sie horizontal hochskalieren. Aber wenn Sie horizontal hochskalieren, können Clients auf verschiedenen Servern weitergeleitet werden. Ein Client, der mit einem Server verbunden ist, erhalten keine Nachrichten von einem anderen Server gesendet.

![](scaleout-in-signalr/_static/image1.png)

Eine Lösung besteht darin, Weiterleiten von Nachrichten zwischen Servern mit einer Komponente mit dem Namen einer *Rückwandplatine*. Mit einer Rückwandplatine aktiviert ist jede Anwendungsinstanz sendet Nachrichten an die Backplane und der Rückwand an die anderen Anwendungsinstanzen weitergeleitet werden. (Im Bereich der Elektronik ist eine Rückwandplatine eine Gruppe von parallelen Connectors. Entsprechend stellt eine Verbindung her SignalR-Backplane mehrerer Server.)

![](scaleout-in-signalr/_static/image2.png)

SignalR stellt derzeit drei Backplanes bereit:

- **Azure Servicebus**. Service Bus ist eine messaging-Infrastruktur, die Komponenten zum Senden von Nachrichten in einem lose gekoppelten System ermöglicht.
- **Redis**. Redis ist ein Schlüssel-Wert-Speicher im Arbeitsspeicher. Redis unterstützt ein Muster zum Veröffentlichen/Abonnieren ("Pub/Sub") zum Senden von Nachrichten an.
- **SQL Server**. Die SQL Server-Rückwandplatine Nachrichten, die in SQL-Tabellen geschrieben wird. Der Rückwand verwendet Service Broker für effiziente messaging. Es funktioniert jedoch auch, wenn Service Broker nicht aktiviert ist.

Wenn Sie Ihre Anwendung in Azure bereitstellen, sollten Sie die Redis-Rückwandplatine mit [Azure Redis Cache](https://azure.microsoft.com/services/cache/). Wenn Sie mit Ihren eigenen Serverfarm bereitstellen, sollten Sie Sie der SQL Server- oder Redis Backplanes.

Die folgenden Themen enthalten schrittweise aufgebaute Lernprogramme für jede-Rückwandplatine:

- [Horizontale Skalierung in SignalR mit Azure Service Bus](scaleout-with-windows-azure-service-bus.md)
- [Horizontale Skalierung in SignalR mit Redis](scaleout-with-redis.md)
- [Horizontale Skalierung in SignalR mit SQL Server](scaleout-with-sql-server.md)

## <a name="implementation"></a>Implementierung

In SignalR wird jede Nachricht über einen Nachrichtenbus gesendet. Implementiert ein Nachrichtenbus der ["imessagebus"](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) -Schnittstelle, die eine Abstraktion zum Veröffentlichen/Abonnieren bereitstellt. Die Backplanes zu arbeiten, indem Sie den standardmäßigen ersetzen **"imessagebus"** mit einem Bus, die für diese Rückwandplatine konzipiert. Der Nachrichtenbus für Redis ist z. B. [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), und nutzt die Redis [Pub/Sub-](http://redis.io/topics/pubsub) Mechanismus zum Senden und Empfangen von Nachrichten.

Jede Serverinstanz eine Verbindung mit der Rückwand über den Bus. Wenn eine Nachricht gesendet wird, an die Backplane darin, und der Rückwand sendet sie an jedem Server. Wenn ein Server eine Nachricht von der Backplane empfängt, werden diese die Nachricht in ihrem lokalen Cache abgelegt. Der Server sendet dann Nachrichten für Clients aus dem lokalen Cache.

Für jede Clientverbindung wird dem Client-Status im Lesen der Nachrichtenfolge nachverfolgt mithilfe eines Cursors. (Für ein Cursor stellt eine Position in den Nachrichtenstream dar.) Wenn ein Client die Verbindung trennt, und klicken Sie dann erneut eine Verbindung herstellt, fordert den Bus Nachrichten, die nach dem Clientstandort Cursorwert eingetroffen sind. Das gleiche passiert, wenn eine Verbindung verwendet [lange](../getting-started/introduction-to-signalr.md#transports). Nachdem die Anforderung eine lange Abfrage abgeschlossen ist, wird der Client öffnet eine neue Verbindung und fragt nach Nachrichten, die nach dem Cursor eingetroffen sind.

Der Cursor Mechanismus funktioniert auch, wenn ein Client auf einen anderen Server weitergeleitet wird erneut eine Verbindung herzustellen. Der Rückwand erkennt aller Server, und es spielt keine Rolle, welchen Server ein Client eine Verbindung herstellt.

## <a name="limitations"></a>Einschränkungen

Verwenden eine Rückwandplatine, ist der maximale Nachrichtendurchsatz niedriger als bei der Kommunikation von Clients direkt mit einem einzelnen Server-Knoten. Dies liegt daran der Rückwand leitet jede Nachricht auf jedem Knoten aus, damit der Rückwand Engpässe auftreten kann. Ob diese Einschränkung ein Problem aufgetreten ist, hängt von der Anwendung ab. Hier sind z. B. einige typischen Szenarien für SignalR:

- [Serverübertragung](../getting-started/tutorial-server-broadcast-with-signalr.md) (beispielsweise Börsenticker): Backplanes eignen sich gut für dieses Szenario, da der Server die Rate kontrolliert, an der Nachrichten gesendet werden.
- [Client-zu-Client](../getting-started/tutorial-getting-started-with-signalr.md) (z. B. chat): In diesem Szenario wird möglicherweise der Rückwand einen Engpass, wenn die Anzahl der Nachrichten mit der Anzahl der Clients skaliert werden kann; d. h., wenn die Anzahl der Nachrichten wird verknüpfen proportional mehr Clients.
- [Echtzeitnachrichten](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (z. B. in Echtzeit Spiele): Eine Rückwandplatine wird für dieses Szenario nicht empfohlen.

## <a name="enabling-tracing-for-signalr-scaleout"></a>Aktivieren der Ablaufverfolgung für horizontale Skalierung in SignalR

Fügen Sie zum Aktivieren der Ablaufverfolgung für die Backplanes in den folgenden Abschnitten in der Datei web.config unter dem Stamm **Konfiguration** Element:

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
