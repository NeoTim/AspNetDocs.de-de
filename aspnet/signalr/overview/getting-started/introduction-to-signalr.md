---
uid: signalr/overview/getting-started/introduction-to-signalr
title: Einführung in SignalR | Microsoft Docs
author: bradygaster
description: In diesem Artikel wird beschrieben, was SignalR ist und welche Lösungen es erstellen soll.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675940"
---
# <a name="introduction-to-signalr"></a>Einführung in SignalR

von [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> In diesem Artikel wird beschrieben, was SignalR ist und welche Lösungen es erstellen soll. 
> 
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
> 
> Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten. Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).

## <a name="what-is-signalr"></a>Was ist SignalR?

ASP.NET SignalR ist eine Bibliothek für ASP.NET Entwickler, die das Hinzufügen von Echtzeit-Webfunktionen zu Anwendungen vereinfacht. Echtzeit-Webfunktionalität ist die Möglichkeit, Servercode-Push-Inhalte sofort an verbundene Clients zu übertragen, sobald sie verfügbar sind, anstatt dass der Server darauf wartet, dass ein Client neue Daten anfordert.

SignalR kann verwendet werden, um jede Art von "Echtzeit"-Webfunktionalität zu Ihrer ASP.NET-Anwendung hinzuzufügen. Während Chat oft als Beispiel verwendet wird, können Sie eine ganze Menge mehr tun. Jedes Mal, wenn ein Benutzer eine Webseite aktualisiert, um neue Daten anzuzeigen, oder wenn die Seite [lange Abfragen](http://en.wikipedia.org/wiki/Push_technology#Long_polling) implementiert, um neue Daten abzurufen, ist sie ein Kandidat für die Verwendung von SignalR. Beispiele hierfür sind Dashboards und Überwachungsanwendungen, kollaborative Anwendungen (z. B. die gleichzeitige Bearbeitung von Dokumenten), Aktualisierungen des Auftragsfortschritts und Echtzeitformulare.

SignalR ermöglicht auch völlig neue Arten von Web-Anwendungen, die hochfrequente Updates vom Server erfordern, z. B. Echtzeit-Gaming.

SignalR bietet eine einfache API zum Erstellen von RPC (Server-zu-Client-Remoteprozeduraufrufen), die JavaScript-Funktionen in Clientbrowsern (und anderen Clientplattformen) aus serverseitigem .NET-Code aufrufen. SignalR enthält auch API für die Verbindungsverwaltung (z. B. Verbindungs- und Trennen von Ereignissen) und das Gruppieren von Verbindungen.

![Aufrufen von Methoden mit SignalR](introduction-to-signalr/_static/image1.png)

SignalR übernimmt die Verbindungsverwaltung automatisch und ermöglicht Ihnen, Nachrichten an alle verbundenen Clients gleichzeitig zu übertragen, wie in einem Chatroom. Nachrichten können auch nur an bestimmte Clients gesendet werden. Die Verbindung zwischen Client und Server besteht permanent und unterscheidet sich damit von einer klassischen HTTP-Verbindung, die für jede Kommunikation neu hergestellt wird.

SignalR unterstützt die "Server-Push"-Funktionalität, bei der Servercode clientcode im Browser mithilfe von Remoteprozeduraufrufen (Remote Procedure Calls, RPC) aufrufen kann, anstatt des Anforderungs-Antwort-Modells, das heute im Web üblich ist.

SignalR-Anwendungen können mithilfe integrierter und Drittanbieter-Scale-Out-Anbieter auf Tausende von Clients skaliert werden.

Zu den integrierten Anbietern gehören:
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Zu den Drittanbietern gehören:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR ist Open-Source, zugänglich über [GitHub](https://github.com/signalr).

## <a name="signalr-and-websocket"></a>SignalR und WebSocket

SignalR verwendet den neuen WebSocket-Transport, sofern verfügbar, und greift bei Bedarf auf ältere Transporte zurück. Während Sie Ihre App sicherlich direkt mit WebSocket schreiben könnten, bedeutet die Verwendung von SignalR, dass ein Großteil der zusätzlichen Funktionen, die Sie implementieren müssten, bereits für Sie erledigt ist. Am wichtigsten ist, dass Sie Ihre App codieren können, um WebSocket zu nutzen, ohne sich um das Erstellen eines separaten Codepfads für ältere Clients kümmern zu müssen. SignalR schützt Sie auch davor, sich um Aktualisierungen von WebSocket kümmern zu müssen, da SignalR aktualisiert wird, um Änderungen im zugrunde liegenden Transport zu unterstützen, wodurch Ihre Anwendung eine konsistente Schnittstelle für alle Versionen von WebSocket bereitstellt.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Transporte und Fallbacks

SignalR ist eine Abstraktion über einige der Transporte, die erforderlich sind, um Echtzeitarbeit zwischen Client und Server zu erledigen. Eine SignalR-Verbindung wird als HTTP gestartet und dann zu einer WebSocket-Verbindung heraufgestuft, sofern diese verfügbar ist. WebSocket ist der ideale Transport für SignalR, da es den Serverspeicher am effizientesten nutzt, die geringste Latenz aufweist und die meisten zugrunde liegenden Features aufweist (z. B. Vollduplexkommunikation zwischen Client und Server), aber auch die strengsten Anforderungen hat: WebSocket erfordert, dass der Server Windows Server 2012 oder Windows 8 und .NET Framework 4.5 verwendet. Wenn diese Anforderungen nicht erfüllt werden, versucht SignalR, andere Transporte zu verwenden, um verbindungen zu stellen.

### <a name="html-5-transports"></a>HTML 5-Transporte

Diese Transporte sind auf die Unterstützung für [HTML 5](http://en.wikipedia.org/wiki/HTML5)angewiesen. Wenn der Clientbrowser den HTML 5-Standard nicht unterstützt, werden ältere Transporte verwendet.

- **WebSocket** (wenn sowohl der Server als auch der Browser angeben, dass sie Websocket unterstützen können). WebSocket ist der einzige Transport, der eine echte persistente, zweiseitige Verbindung zwischen Client und Server herstellt. WebSocket hat jedoch auch die strengsten Anforderungen. Es wird nur in den neuesten Versionen von Microsoft Internet Explorer, Google Chrome und Mozilla Firefox vollständig unterstützt und hat nur eine teilweise Implementierung in anderen Browsern wie Opera und Safari.
- **Server Sent Events**, auch als EventSource bezeichnet (wenn der Browser Server Sent Events unterstützt, was im Grunde alle Browser außer Internet Explorer ist).)

### <a name="comet-transports"></a>Kometentransporte

Die folgenden Transporte basieren [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) auf dem Comet-Webanwendungsmodell, bei dem ein Browser oder ein anderer Client eine lang gehegte HTTP-Anforderung verwaltet, die der Server verwenden kann, um Daten an den Client zu übertragen, ohne dass der Client sie ausdrücklich anfordert.

- **Forever Frame** (nur für Internet Explorer). Forever Frame erstellt einen ausgeblendeten IFrame, der eine Anforderung an einen Endpunkt auf dem Server stellt, der nicht abgeschlossen wird. Der Server sendet dann kontinuierlich Skript an den Client, das sofort ausgeführt wird, und stellt eine unwegsame Echtzeitverbindung vom Server zum Client bereit. Die Verbindung vom Client zum Server verwendet eine separate Verbindung vom Server zur Clientverbindung, und wie bei einer Standard-HTTP-Anforderung wird für jedes Datenelement, das gesendet werden muss, eine neue Verbindung erstellt.
- **Ajax lange Umfragen**. Lange Abfragen stellen keine dauerhafte Verbindung her, sondern fragt den Server mit einer Anforderung ab, die geöffnet bleibt, bis der Server antwortet, an dem die Verbindung geschlossen wird und sofort eine neue Verbindung angefordert wird. Dies kann zu einer gewissen Latenz führen, während die Verbindung zurückgesetzt wird.

Weitere Informationen dazu, welche Transporte unter welchen Konfigurationen unterstützt werden, finden Sie unter [Unterstützte Plattformen](supported-platforms.md).

### <a name="transport-selection-process"></a>Transportauswahlverfahren

Die folgende Liste zeigt die Schritte, die SignalR verwendet, um zu entscheiden, welchen Transport verwendet werden soll.

1. Wenn der Browser Internet Explorer 8 oder früher ist, wird Long Polling verwendet.
2. Wenn JSONP konfiguriert ist (d. h., der `jsonp` Parameter wird beim `true` Starten der Verbindung auf "Long Polling" festgelegt.
3. Wenn eine domänenübergreifende Verbindung hergestellt wird (d. h., wenn sich der SignalR-Endpunkt nicht in derselben Domäne wie die Hostingseite befindet), wird WebSocket verwendet, wenn die folgenden Kriterien erfüllt sind:

   - Der Client unterstützt CORS (Cross-Origin Resource Sharing). Weitere Informationen dazu, welche Clients CORS unterstützen, finden [Sie unter CORS unter caniuse.com](http://www.caniuse.com/CORS).
   - Der Client unterstützt WebSocket
   - Der Server unterstützt WebSocket

     Wenn eines dieser Kriterien nicht erfüllt ist, wird Long Polling verwendet. Weitere Informationen zu domänenübergreifenden Verbindungen finden Sie unter [Einrichten einer domänenübergreifenden Verbindung](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).
4. Wenn JSONP nicht konfiguriert ist und die Verbindung nicht domänenübergreifend ist, wird WebSocket verwendet, wenn sowohl der Client als auch der Server dies unterstützen.
5. Wenn der Client oder der Server WebSocket nicht unterstützt, werden Server-Gesendete Ereignisse verwendet, wenn sie verfügbar sind.
6. Wenn Server Sent Events nicht verfügbar ist, wird versucht, den Rahmen für immer zu verwenden.
7. Wenn Forever Frame fehlschlägt, wird Long Polling verwendet.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Überwachung von Transporten

Sie können bestimmen, welchen Transport Ihre Anwendung verwendet, indem Sie die Protokollierung auf Ihrem Hub aktivieren und das Konsolenfenster in Ihrem Browser öffnen.

Um die Protokollierung für die Ereignisse Ihres Hubs in einem Browser zu aktivieren, fügen Sie der Clientanwendung den folgenden Befehl hinzu:

`$.connection.hub.logging = true;`

- Öffnen Sie in Internet Explorer die Entwicklertools, indem Sie F12 drücken, und klicken Sie auf die Registerkarte Konsole.

    ![Konsole in Microsoft Internet Explorer](introduction-to-signalr/_static/image2.png)
- Öffnen Sie in Chrome die Konsole, indem Sie Strg+Umschalt+J drücken.

    ![Konsole in Google Chrome](introduction-to-signalr/_static/image3.png)

Wenn die Konsole geöffnet und die Protokollierung aktiviert ist, können Sie sehen, welcher Transport von SignalR verwendet wird.

![Konsole in Internet Explorer mit WebSocket-Transport](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Angeben eines Transports

Das Aushandeln eines Transports nimmt eine gewisse Zeit und Client-/Serverressourcen in Anspruch. Wenn die Clientfunktionen bekannt sind, kann beim Starten der Clientverbindung ein Transport angegeben werden. Der folgende Codeausschnitt veranschaulicht das Starten einer Verbindung mithilfe des Ajax Long Polling-Transports, wie er verwendet würde, wenn bekannt wäre, dass der Client kein anderes Protokoll unterstützt:

`connection.start({ transport: 'longPolling' });`

Sie können einen Fallbackauftrag angeben, wenn ein Client bestimmte Transporte in der Reihenfolge ausprobieren soll. Der folgende Codeausschnitt veranschaulicht, wie WebSocket versucht wird und dies nicht der Fall ist, und er geht direkt zu Long Polling.

`connection.start({ transport: ['webSockets','longPolling'] });`

Die Zeichenfolgenkonstanten zum Angeben von Transporten werden wie folgt definiert:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Verbindungen und Hubs

Die SignalR-API enthält zwei Modelle für die Kommunikation zwischen Clients und Servern: Persistente Verbindungen und Hubs.

Eine Verbindung stellt einen einfachen Endpunkt zum Senden von Einzelempfänger-, gruppierten oder Broadcastnachrichten dar. Die Persistent Connection-API (dargestellt in .NET-Code durch die PersistentConnection-Klasse) bietet dem Entwickler direkten Zugriff auf das Low-Level-Kommunikationsprotokoll, das SignalR verfügbar macht. Die Verwendung des Kommunikationsmodells "Verbindungen" ist Entwicklern vertraut, die verbindungsbasierte APIs wie Windows Communication Foundation verwendet haben.

Ein Hub ist eine umfassendere Pipeline, die auf der Verbindungs-API aufbaut und es Ihrem Client und Server ermöglicht, Methoden direkt aufeinander aufzurufen. SignalR verarbeitet den Versand über Maschinengrenzen hinweg wie von Zauberhand, sodass Clients Methoden auf dem Server genauso einfach aufrufen können wie lokale Methoden und umgekehrt. Die Verwendung des Hubs-Kommunikationsmodells ist Entwicklern vertraut, die Remoteaufruf-APIs wie .NET Remoting verwendet haben. Mit einem Hub können Sie auch stark typisierte Parameter an Methoden übergeben, wodurch die Modellbindung aktiviert wird.

### <a name="architecture-diagram"></a>Architekturdiagramm

Das folgende Diagramm zeigt die Beziehung zwischen Hubs, Persistent Connections und den zugrunde liegenden Technologien, die für Transporte verwendet werden.

![SignalR-Architekturdiagramm mit APIs, Transporten und Clients](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Funktionsweise von Hubs

Wenn serverseitiger Code eine Methode auf dem Client aufruft, wird ein Paket über den aktiven Transport gesendet, der den Namen und die Parameter der aufzurufenden Methode enthält (wenn ein Objekt als Methodenparameter gesendet wird, wird es mit JSON serialisiert). Der Client gleicht dann den Methodennamen mit Methoden ab, die im clientseitigen Code definiert sind. Wenn eine Übereinstimmung vorliegt, wird die Clientmethode mithilfe der deserialisierten Parameterdaten ausgeführt.

Der Methodenaufruf kann mit Tools wie Fiddler überwacht [werden.](http://fiddler2.com/) Die folgende Abbildung zeigt einen Methodenaufruf, der von einem SignalR-Server an einen Webbrowserclient im Protokollbereich von Fiddler gesendet wird. Der Methodenaufruf wird von einem `MoveShapeHub`Hub mit dem Namen `updateShape`gesendet, und die aufgerufene Methode wird aufgerufen.

![Ansicht des Fiddler-Protokolls mit SignalR-Datenverkehr](introduction-to-signalr/_static/image6.png)

In diesem Beispiel wird der Hubname mit dem `H` Parameter identifiziert. Der Methodenname wird `M` mit dem Parameter identifiziert, und die an `A` die Methode gesendeten Daten werden mit dem Parameter identifiziert. Die Anwendung, die diese Nachricht generiert hat, wird im [Hochfrequenz-Echtzeit-Tutorial](tutorial-high-frequency-realtime-with-signalr.md) erstellt.

### <a name="choosing-a-communication-model"></a>Auswählen eines Kommunikationsmodells

Die meisten Anwendungen sollten die Hubs-API verwenden. Die Connections-API kann unter den folgenden Umständen verwendet werden:

- Das Format der tatsächlich gesendeten Nachricht muss angegeben werden.
- Der Entwickler arbeitet lieber mit einem Messaging- und Dispatchingmodell als mit einem Remoteaufrufmodell.
- Eine vorhandene Anwendung, die ein Messagingmodell verwendet, wird portiert, um SignalR zu verwenden.
