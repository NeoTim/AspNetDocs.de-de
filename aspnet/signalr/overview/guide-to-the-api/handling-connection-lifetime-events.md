---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: Grundlegendes und Behandeln von Verbindungslebensdauerereignissen in SignalR | Microsoft Docs
author: bradygaster
description: In diesem Artikel wird beschrieben, wie die von der Hubs-API verfügbar gemachten Ereignisse verwendet werden.
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675826"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>Überblick und Behandeln von Ereignissen im Zusammenhang mit der Verbindungslebensdauer in SignalR

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Dieser Artikel bietet einen Überblick über die SignalR-Verbindungs-, Wiederverbindungs- und Trennungsereignisse, die Sie verarbeiten können, sowie Timeout- und Keepalive-Einstellungen, die Sie konfigurieren können.
>
> Der Artikel geht davon aus, dass Sie bereits über einige Kenntnisse von SignalR- und Verbindungslebensdauerereignissen verfügen. Eine Einführung in SignalR finden Sie unter [Einführung in SignalR](../getting-started/introduction-to-signalr.md). Listen der Ereignisse der Verbindungslebensdauer finden Sie in den folgenden Ressourcen:
>
> - [Behandeln von Verbindungslebensdauerereignissen in der Hub-Klasse](hubs-api-guide-server.md#connectionlifetime)
> - [Behandeln von Verbindungslebensdauerereignissen in JavaScript-Clients](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [Behandeln von Verbindungslebensdauerereignissen in .NET-Clients](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR Version 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Frühere Versionen dieses Themas
>
> Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
>
> Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten. Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Übersicht

Dieser Artikel enthält folgende Abschnitte:

- [Terminologie und Szenarien der Verbindungslebensdauer](#terminology)

    - [SignalR-Verbindungen, Transportverbindungen und physikalische Verbindungen](#signalrvstransport)
    - [Transporttrennungsszenarien](#transportdisconnect)
    - [Client-Trennungsszenarien](#clientdisconnect)
    - [Servertrennungsszenarien](#serverdisconnect)
- [Timeout- und Keepalive-Einstellungen](#timeoutkeepalive)

    - [Connectiontimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [So ändern Sie Timeout- und Keepalive-Einstellungen](#changetimeout)
- [So benachrichtigen Sie den Benutzer über Trennungen](#notifydisconnect)
- [Wie man sich kontinuierlich wieder verbindet](#continuousreconnect)
- [Trennen eines Clients im Servercode](#disconnectclientfromserver)
- [Erkennen des Grunds für eine Trennung](#detectingreasonfordisconnection)

Links zu API-Referenzthemen beziehen sich auf die .NET 4.5-Version der API. Wenn Sie .NET 4 verwenden, lesen Sie [die .NET 4-Version der API-Themen](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>Terminologie und Szenarien der Verbindungslebensdauer

Der `OnReconnected` Ereignishandler in einem SignalR `OnConnected` Hub kann `OnDisconnected` direkt nach, aber nicht nach einem bestimmten Client ausgeführt werden. Der Grund, warum Sie eine wiederhergestellte Verbindung ohne Trennung haben können, ist, dass es mehrere Möglichkeiten gibt, wie das Wort "Verbindung" in SignalR verwendet wird.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR-Verbindungen, Transportverbindungen und physikalische Verbindungen

In diesem Artikel wird zwischen *SignalR-Verbindungen*, *Verkehrsverbindungen*und *physischen Verbindungen*unterschieden:

- **Die SignalR-Verbindung** bezieht sich auf eine logische Beziehung zwischen einem Client und einer Server-URL, die von der SignalR-API verwaltet und durch eine Verbindungs-ID eindeutig identifiziert wird. Die Daten über diese Beziehung werden von SignalR verwaltet und zum Herstellen einer Transportverbindung verwendet. Die Beziehung endet, und SignalR verfügt über `Stop` die Daten, wenn der Client die Methode aufruft oder ein Timeoutlimit erreicht wird, während SignalR versucht, eine verlorene Transportverbindung wiederherzustellen.
- **Transportverbindung** bezieht sich auf eine logische Beziehung zwischen einem Client und einem Server, die von einer der vier Transport-APIs verwaltet wird: WebSockets, servergesendete Ereignisse, für immer Frame oder lange Abfragen. SignalR verwendet die Transport-API, um eine Transportverbindung zu erstellen, und die Transport-API hängt vom Vorhandensein einer physischen Netzwerkverbindung ab, um die Transportverbindung zu erstellen. Die Transportverbindung endet, wenn SignalR sie beendet oder wenn die Transport-API erkennt, dass die physische Verbindung unterbrochen ist.
- **Physische Verbindung** bezieht sich auf die physischen Netzwerkverbindungen -- Drähte, drahtlose Signale, Router usw. -- die die Kommunikation zwischen einem Clientcomputer und einem Servercomputer erleichtern. Die physische Verbindung muss vorhanden sein, um eine Transportverbindung herzustellen, und es muss eine Transportverbindung hergestellt werden, um eine SignalR-Verbindung herzustellen. Wenn Sie jedoch die physische Verbindung aufbrechen, wird die Transportverbindung oder die SignalR-Verbindung nicht sofort beendet, wie weiter unten in diesem Thema erläutert wird.

Im folgenden Diagramm wird die SignalR-Verbindung durch die Hubs-API und die PersistentConnection-API-SignalR-Schicht dargestellt, die Transportverbindung wird durch die Layer Transports dargestellt, und die physische Verbindung wird durch die Leitungen zwischen dem Server und den Clients dargestellt.

![SignalR-Architekturdiagramm](handling-connection-lifetime-events/_static/image1.png)

Wenn Sie `Start` die Methode in einem SignalR-Client aufrufen, stellen Sie SignalR-Clientcode alle Informationen zur Verfügung, die zum Herstellen einer physischen Verbindung zu einem Server erforderlich sind. SignalR-Clientcode verwendet diese Informationen, um eine HTTP-Anforderung zu stellen und eine physische Verbindung herzustellen, die eine der vier Transportmethoden verwendet. Wenn die Transportverbindung ausfällt oder der Server ausfällt, wird die SignalR-Verbindung nicht sofort getrennt, da der Client immer noch über die Informationen verfügt, die er benötigt, um automatisch eine neue Transportverbindung zur gleichen SignalR-URL wiederherzustellen. In diesem Szenario ist kein Eingriff der Benutzeranwendung beteiligt, und wenn der SignalR-Clientcode eine neue Transportverbindung herstellt, startet er keine neue SignalR-Verbindung. Die Kontinuität der SignalR-Verbindung spiegelt sich in der Tatsache wider, dass `Start` sich die Verbindungs-ID, die beim Aufrufen der Methode erstellt wird, nicht ändert.

Der `OnReconnected` Ereignishandler auf dem Hub wird ausgeführt, wenn eine Transportverbindung nach einem Verlust automatisch wiederhergestellt wird. Der `OnDisconnected` Ereignishandler wird am Ende einer SignalR-Verbindung ausgeführt. Eine SignalR-Verbindung kann auf eine der folgenden Arten enden:

- Wenn der Client `Stop` die Methode aufruft, wird eine Stoppnachricht an den Server gesendet, und sowohl Client als auch Server beenden die SignalR-Verbindung sofort.
- Nachdem die Verbindung zwischen Client und Server unterbrochen wurde, versucht der Client erneut eine Verbindung herzustellen, und der Server wartet, bis der Client die Verbindung wieder herstellt. Wenn die Versuche, die Verbindung wiederherzustellen, fehlschlagen und der Zeittimeoutzeitraum für die Trennung endet, beenden sowohl Client als auch Server die SignalR-Verbindung. Der Client versucht nicht mehr, die Verbindung wiederherzustellen, und der Server verfügt über seine Darstellung der SignalR-Verbindung.
- Wenn der Client nicht mehr ausgeführt `Stop` wird, ohne die Methode aufrufen zu können, wartet der Server, bis der Client die Verbindung wieder herstellt, und beendet dann die SignalR-Verbindung nach dem Zeittimeout.-
- Wenn der Server nicht mehr ausgeführt wird, versucht der Client erneut eine Verbindung herzustellen (die Transportverbindung neu zu erstellen) und beendet dann die SignalR-Verbindung nach dem Zeittimeout.-

Wenn keine Verbindungsprobleme auftreten und die Benutzeranwendung die SignalR-Verbindung durch Aufrufen der `Stop` Methode beendet, beginnen und enden die SignalR-Verbindung und die Transportverbindung ungefähr zur gleichen Zeit. In den folgenden Abschnitten werden die anderen Szenarien ausführlicher beschrieben.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>Transporttrennungsszenarien

Physische Verbindungen sind möglicherweise langsam oder es kommt zu Verbindungsunterbrechungen. Abhängig von Faktoren wie der Länge der Unterbrechung kann die Transportverbindung unterbrochen werden. SignalR versucht dann, die Transportverbindung wiederherzustellen. Manchmal erkennt die Transportverbindungs-API die Unterbrechung und löscht die Transportverbindung, und SignalR stellt sofort fest, dass die Verbindung verloren geht. In anderen Szenarien werden weder die Transportverbindungs-API noch SignalR sofort darauf aufmerksam, dass die Konnektivität verloren gegangen ist. Für alle Transporte außer Long Polling verwendet der SignalR-Client eine Funktion namens *keepalive,* um den Verbindungsverlust zu überprüfen, den die Transport-API nicht erkennen kann. Informationen zu langen Abrufverbindungen finden Sie weiter unten in diesem Thema unter [Timeout- und Keepalive-Einstellungen.](#timeoutkeepalive)

Wenn eine Verbindung inaktiv ist, sendet der Server in regelmäßigen Abständen ein Keepalive-Paket an den Client. Ab dem Datum, an dem dieser Artikel geschrieben wird, ist die Standardhäufigkeit alle 10 Sekunden. Wenn Sie auf diese Pakete warten, können Clients feststellen, ob ein Verbindungsproblem vorliegt. Wenn ein Keepalive-Paket nicht empfangen wird, wenn es erwartet wird, geht der Client nach kurzer Zeit von Verbindungsproblemen wie Langsamkeit oder Unterbrechungen aus. Wenn das Keepalive nach längerer Zeit immer noch nicht empfangen wird, geht der Client davon aus, dass die Verbindung getrennt wurde, und versucht, die Verbindung wiederherzustellen.

Das folgende Diagramm veranschaulicht die Client- und Serverereignisse, die in einem typischen Szenario ausgelöst werden, wenn Probleme mit der physischen Verbindung auftreten, die von der Transport-API nicht sofort erkannt werden. Das Diagramm gilt für folgende Umstände:

- Der Transport ist WebSockets, forever frame oder server-sent-Ereignisse.
- Die physische Netzwerkverbindung ist in unterschiedlichen Unterbrechungsphasen unterbrochen.
- Die Transport-API wird nicht auf die Unterbrechungen aufmerksam, daher verlässt sich SignalR auf die Keepalive-Funktionalität, um sie zu erkennen.

![Verkehrstrennungen](handling-connection-lifetime-events/_static/image2.png)

Wenn der Client in den Wiederverbindungsmodus wechselt, aber keine Transportverbindung innerhalb des Trennzeitlimits herstellen kann, beendet der Server die SignalR-Verbindung. In diesem Fall führt der Server `OnDisconnected` die Methode des Hubs aus und stellt eine Trennnachricht in die Warteschlange, die an den Client gesendet werden soll, falls der Client später eine Verbindung herstellen kann. Wenn der Client dann die Verbindung wieder herstellt, `Stop` empfängt er den Befehl "Disconnect" und ruft die Methode auf. In diesem `OnReconnected` Szenario wird nicht ausgeführt, wenn `OnDisconnected` der Client erneut eine `Stop`Verbindung herstellt, und wird nicht ausgeführt, wenn der Client aufruft. Das folgende Diagramm veranschaulicht dieses Szenario.

![Transportunterbrechungen - Servertimeout](handling-connection-lifetime-events/_static/image3.png)

Die SignalR-Verbindungslebensdauerereignisse, die auf dem Client ausgelöst werden können, sind die folgenden:

- `ConnectionSlow`Client-Ereignis.

    Wird ausgelöst, wenn ein voreingestellter Anteil des Keepalive-Timeoutzeitraums seit dem Eingang der letzten Nachricht oder des Keepalive-Pings verstrichen ist. Der standardmäßige Keepalive-Timeout-Warnzeitraum beträgt 2/3 des Keepalive-Timeouts. Das Keepalive-Timeout beträgt 20 Sekunden, die Warnung erfolgt also bei etwa 13 Sekunden.

    Standardmäßig sendet der Server alle 10 Sekunden Keepalive-Pings, und der Client überprüft etwa alle 2 Sekunden auf Keepalive-Pings (ein Drittel der Differenz zwischen dem Keepalive-Timeoutwert und dem Keepalive-Timeout-Warnungswert).

    Wenn der Transport-API eine Trennung bekannt wird, wird SignalR möglicherweise über die Trennung informiert, bevor die Keepalive-Timeout-Warnzeit verstrichen ist. In diesem Fall `ConnectionSlow` würde das Ereignis nicht ausgelöst, und `Reconnecting` SignalR würde direkt an das Ereignis gehen.
- `Reconnecting`Client-Ereignis.

    Wird ausgelöst, wenn (a) die Transport-API erkennt, dass die Verbindung verloren geht, oder (b) der Keepalive-Timeout-Zeitraum seit dem Erhalt der letzten Nachricht oder des Keepalive-Pings verstrichen ist. Der SignalR-Clientcode versucht, die Verbindung wiederherzustellen. Sie können dieses Ereignis behandeln, wenn Ihre Anwendung etwas unternehmen soll, wenn eine Transportverbindung unterbrochen wird. Der standardmäßige Keepalive-Timeout-Zeitraum beträgt derzeit 20 Sekunden.

    Wenn Ihr Clientcode versucht, eine Hub-Methode aufzurufen, während sich SignalR im Wiederherstellungsmodus befindet, versucht SignalR, den Befehl zu senden. Meistens werden solche Versuche scheitern, aber unter bestimmten Umständen könnten sie erfolgreich sein. Für die vom Server gesendeten Ereignisse, den Rahmen für immer und lange Abfragetransporte verwendet SignalR zwei Kommunikationskanäle, einen, den der Client zum Senden von Nachrichten verwendet, und einen, den er zum Empfangen von Nachrichten verwendet. Der Kanal, der für den Empfang verwendet wird, ist der permanent geöffnete Kanal, und das ist der Kanal, der geschlossen wird, wenn die physische Verbindung unterbrochen wird. Der für das Senden verwendete Kanal bleibt verfügbar, sodass bei Wiederherstellung der physischen Konnektivität ein Methodenaufruf vom Client zum Server erfolgreich sein kann, bevor der Empfangskanal wiederhergestellt wird. Der Rückgabewert wird erst empfangen, wenn SignalR den für den Empfang verwendeten Kanal wieder öffnet.
- `Reconnected`Client-Ereignis.

    Wird ausgelöst, wenn die Transportverbindung wiederhergestellt wird. Der `OnReconnected` Ereignishandler im Hub wird ausgeführt.
- `Closed`Clientereignis`disconnected` (Ereignis in JavaScript).

    Wird ausgelöst, wenn der Zeitverlustzeitraum für die Trennung abläuft, während der SignalR-Clientcode versucht, nach dem Verlust der Transportverbindung die Verbindung wiederherzustellen. Das standardmäßige Zeittimeout für die Trennung beträgt 30 Sekunden. (Dieses Ereignis wird auch ausgelöst, `Stop` wenn die Verbindung beendet wird, da die Methode aufgerufen wird.)

Transportverbindungsunterbrechungen, die von der Transport-API nicht erkannt werden und den Empfang von Keepalive-Pings vom Server nicht länger verzögern als der Keepalive-Timeout-Warnzeitraum, führen möglicherweise nicht dazu, dass Ereignisse der Verbindungslebensdauer ausgelöst werden.

Einige Netzwerkumgebungen schließen absichtlich Leerlaufverbindungen, und eine weitere Funktion der Keepalive-Pakete besteht darin, dies zu verhindern, indem diese Netzwerke darüber informiert werden, dass eine SignalR-Verbindung verwendet wird. In extremen Fällen reicht die Standardhäufigkeit von Keepalive-Pings möglicherweise nicht aus, um geschlossene Verbindungen zu verhindern. In diesem Fall können Sie Keepalive-Pings so konfigurieren, dass sie häufiger gesendet werden. Weitere Informationen finden Sie unter [Timeout- und Keepalive-Einstellungen](#timeoutkeepalive) weiter unten in diesem Thema.

> [!NOTE]
>
> **Wichtig**: Die hier beschriebene Abfolge der Ereignisse ist nicht garantiert. SignalR unternimmt jeden Versuch, Verbindungslebensdauerereignisse in vorhersehbarer Weise gemäß diesem Schema zu erhöhen, aber es gibt viele Variationen von Netzwerkereignissen und viele Möglichkeiten, wie zugrunde liegende Kommunikationsframeworks wie Transport-APIs sie behandeln. Beispielsweise wird `Reconnected` das Ereignis möglicherweise nicht ausgelöst, wenn `OnConnected` der Client erneut eine Verbindung herstellt, oder der Handler auf dem Server wird ausgeführt, wenn der Versuch, eine Verbindung herzustellen, fehlschlägt. In diesem Thema werden nur die Effekte beschrieben, die normalerweise durch bestimmte typische Umstände erzeugt werden.

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>Client-Trennungsszenarien

In einem Browserclient wird der SignalR-Clientcode, der eine SignalR-Verbindung verwaltet, im JavaScript-Kontext einer Webseite ausgeführt. Aus diesem Grund muss die SignalR-Verbindung beendet werden, wenn Sie von einer Seite zur anderen navigieren, und deshalb haben Sie mehrere Verbindungen mit mehreren Verbindungs-IDs, wenn Sie eine Verbindung über mehrere Browserfenster oder -registerkarten herstellen. Wenn der Benutzer ein Browserfenster oder eine Registerkarte schließt oder zu einer neuen Seite navigiert oder die Seite aktualisiert, wird die `Stop` SignalR-Verbindung sofort beendet, da SignalR-Clientcode dieses Browserereignis für Sie verarbeitet und die Methode aufruft. In diesen Szenarien oder auf einer beliebigen `Stop` Clientplattform, `OnDisconnected` wenn Ihre Anwendung die Methode aufruft, wird der Ereignishandler sofort auf dem Server ausgeführt, und der Client löst das `Closed` Ereignis aus (das Ereignis wird in JavaScript benannt). `disconnected`

Wenn eine Clientanwendung oder der Computer, auf dem sie ausgeführt wird, abstürzt oder in den Ruhezustand wechselt (z. B. wenn der Benutzer den Laptop schließt), wird der Server nicht über den Vorfall informiert. Soweit der Server weiß, kann der Verlust des Clients auf verbindungsunterbrechungen zurückzuführen sein, und der Client versucht möglicherweise, die Verbindung wiederherzustellen. Daher wartet der Server in diesen Szenarien darauf, dem Client `OnDisconnected` eine erneute Verbindung zu geben, und wird erst nach Ablauf des Zeittimeouts für die Trennung ausgeführt (standardmäßig ca. 30 Sekunden). Das folgende Diagramm veranschaulicht dieses Szenario.

![Clientcomputerfehler](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>Servertrennungsszenarien

Wenn ein Server offline geht -- er startet neu, schlägt fehl, die App-Domäne recycelt sich usw. -- kann das Ergebnis einer verlorenen Verbindung ähneln, oder die `ConnectionSlow` Transport-API und SignalR wissen möglicherweise sofort, dass der Server verschwunden ist, und SignalR versucht möglicherweise, die Verbindung wieder herzustellen, ohne das Ereignis zu erhöhen. Wenn der Client in den Wiederherstellungsmodus wechselt und der Server wiederhergestellt oder neu gestartet wird oder ein neuer Server vor Ablauf des Trennungstimeouts online geschaltet wird, stellt der Client erneut eine Verbindung mit dem wiederhergestellten oder neuen Server her. In diesem Fall wird die SignalR-Verbindung `Reconnected` auf dem Client fortgesetzt, und das Ereignis wird ausgelöst. Auf dem ersten `OnDisconnected` Server wird nie ausgeführt, und `OnReconnected` auf dem `OnConnected` neuen Server wird ausgeführt, obwohl noch nie für diesen Client auf diesem Server ausgeführt wurde. (Der Effekt ist derselbe, wenn der Client nach einem Neustart oder der Wiederverwendung der App-Domäne erneut eine Verbindung mit demselben Server herstellt, da er beim Neustart des Servers über keinen Speicher für frühere Verbindungsaktivitäten verfügt.) Das folgende Diagramm geht davon aus, dass die Transport-API sofort auf die verlorene Verbindung aufmerksam wird, sodass das `ConnectionSlow` Ereignis nicht ausgelöst wird.

![Serverausfall und wiederherstellende Verbindung](handling-connection-lifetime-events/_static/image5.png)

Wenn ein Server innerhalb des Trennungstimeoutzeitraums nicht verfügbar wird, wird die SignalR-Verbindung beendet. In diesem Szenario `Closed` wird`disconnected` das Ereignis (in JavaScript-Clients) auf dem Client ausgelöst, aber `OnDisconnected` nie auf dem Server aufgerufen. Das folgende Diagramm geht davon aus, dass die Transport-API nicht auf die verlorene `ConnectionSlow` Verbindung aufmerksam wird, daher wird sie von der SignalR-Keepalive-Funktionalität erkannt, und das Ereignis wird ausgelöst.

![Serverausfall und Timeout](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Timeout- und Keepalive-Einstellungen

Die `ConnectionTimeout`Standardwerte `DisconnectTimeout` `KeepAlive` , und Werte sind für die meisten Szenarien geeignet, können jedoch geändert werden, wenn Ihre Umgebung besondere Anforderungen hat. Wenn Ihre Netzwerkumgebung z. B. Verbindungen schließt, die sich 5 Sekunden lang im Leerlauf befinden, müssen Sie möglicherweise den Keepalive-Wert verringern.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

Diese Einstellung stellt die Zeit dar, die eine Transportverbindung geöffnet lässt und auf eine Antwort wartet, bevor sie geschlossen und eine neue Verbindung geöffnet wird. Der Standardwert ist 110 Sekunden.

Diese Einstellung gilt nur, wenn die Keepalive-Funktionalität deaktiviert ist, was normalerweise nur für den langen Abfragetransport gilt. Das folgende Diagramm veranschaulicht die Auswirkungen dieser Einstellung auf eine lange Abruftransportverbindung.

![Lange Polling-Transportverbindung](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

Diese Einstellung stellt die Zeit dar, die gewartet wird, nachdem eine Transportverbindung vor dem Aufhesetzen des `Disconnected` Ereignisses unterbrochen wurde. Der Standardwert beträgt 30 Sekunden. Wenn Sie `DisconnectTimeout` `KeepAlive` setzen, wird automatisch auf `DisconnectTimeout` 1/3 des Wertes gesetzt.

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

Diese Einstellung stellt die Wartezeit dar, bevor ein Keepalive-Paket über eine Verbindung im Leerlauf gesendet wird. Der Standardwert beträgt 10 Sekunden. Dieser Wert darf nicht mehr als `DisconnectTimeout` 1/3 des Wertes betragen.

Wenn `DisconnectTimeout` Sie sowohl und `KeepAlive`, `KeepAlive` `DisconnectTimeout`sondern nach festlegen möchten. Andernfalls `KeepAlive` wird Ihre Einstellung `DisconnectTimeout` überschrieben, wenn sie automatisch auf 1/3 des Timeoutwerts festgelegt `KeepAlive` wird.

Wenn Sie die Keepalive-Funktionalität `KeepAlive` deaktivieren möchten, setzen Sie auf null. Die Keepalive-Funktionalität wird für den langen Abfragetransport automatisch deaktiviert.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>So ändern Sie Timeout- und Keepalive-Einstellungen

Um die Standardwerte für diese Einstellungen `Application_Start` zu ändern, legen Sie sie in Ihrer *Datei Global.asax* fest, wie im folgenden Beispiel gezeigt. Die im Beispielcode angezeigten Werte entsprechen den Standardwerten.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>So benachrichtigen Sie den Benutzer über Trennungen

In einigen Anwendungen möchten Sie dem Benutzer möglicherweise eine Meldung anzeigen, wenn Verbindungsprobleme auftreten. Sie haben mehrere Möglichkeiten, wie und wann Sie dies tun können. Die folgenden Codebeispiele beziehen sich auf einen JavaScript-Client, der den generierten Proxy verwendet.

- Behandeln `connectionSlow` Sie das Ereignis, um eine Meldung anzuzeigen, sobald SignalR Verbindungsprobleme kennt, bevor es in den Wiederherstellungsmodus wechselt.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- Behandeln `reconnecting` Sie das Ereignis, um eine Meldung anzuzeigen, wenn SignalR von einer Trennung kenntnis und in den Wiederverbindungsmodus wechselt.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- Behandeln `disconnected` Sie das Ereignis, um eine Meldung anzuzeigen, wenn ein Erneutverbindungsversuch ein Timeout aufgetreten ist. In diesem Szenario besteht die einzige Möglichkeit, eine Verbindung mit dem Server wiederherzustellen, darin, die SignalR-Verbindung neu zu starten, indem Sie die `Start` Methode aufrufen, wodurch eine neue Verbindungs-ID erstellt wird. Im folgenden Codebeispiel wird ein Flag verwendet, um sicherzustellen, dass Sie die Benachrichtigung erst nach einem Timeout `Stop` für eine erneute Verbindung ausstellen, nicht nach einem normalen Ende der SignalR-Verbindung, das durch den Aufruf der Methode verursacht wurde.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>Wie man sich kontinuierlich wieder verbindet

In einigen Anwendungen möchten Sie möglicherweise automatisch eine Verbindung wiederherstellen, nachdem sie verloren gegangen ist und der Versuch, die Verbindung wiederherzustellen, ein Timeout aufgetreten ist. Dazu können Sie die `Start` Methode von `Closed` Ihrem`disconnected` Ereignishandler aufrufen (Ereignishandler auf JavaScript-Clients). Möglicherweise möchten Sie vor dem Anruf `Start` eine gewisse Zeit warten, um zu vermeiden, dass dies zu häufig geschieht, wenn der Server oder die physische Verbindung nicht verfügbar sind. Das folgende Codebeispiel ist für einen JavaScript-Client mit dem generierten Proxy.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

Ein potenzielles Problem bei mobilen Clients besteht darin, dass kontinuierliche Wiederverbindungsversuche, wenn der Server oder die physische Verbindung nicht verfügbar ist, zu einem unnötigen Batterieverbrauch führen können.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>Trennen eines Clients im Servercode

SignalR Version 2 verfügt nicht über eine integrierte Server-API zum Trennen von Clients. Es gibt [Pläne, diese Funktionalität in Zukunft hinzuzufügen.](https://github.com/SignalR/SignalR/issues/2101) In der aktuellen SignalR-Version besteht die einfachste Möglichkeit, einen Client vom Server zu trennen, darin, eine Trennmethode auf dem Client zu implementieren und diese Methode vom Server aufzurufen. Das folgende Codebeispiel zeigt eine Trennmethode für einen JavaScript-Client, der den generierten Proxy verwendet.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> Sicherheit - Weder diese Methode zum Trennen von Clients noch die vorgeschlagene integrierte API werden das Szenario von gehackten Clients `stopClient` behandeln, die bösartigen Code ausführen, da die Clients eine erneute Verbindung herstellen könnten oder der gehackte Code die Methode entfernen oder ändern könnte, was sie tut. Der geeignete Ort zum Implementieren des doS-Schutzes (Stateful Denial-of-Service) liegt nicht im Framework oder auf der Serverebene, sondern in der Front-End-Infrastruktur.

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>Erkennen des Grunds für eine Trennung

SignalR 2.1 fügt dem Serverereignis `OnDisconnect` eine Überladung hinzu, die angibt, ob der Client absichtlich die Verbindung getrennt hat, anstatt ein Timeout zu setzen. Der `StopCalled` Parameter ist true, wenn der Client die Verbindung explizit geschlossen hat. Wenn in JavaScript ein Serverfehler dazu geführt hat, dass der Client `$.connection.hub.lastError`die Verbindung trennt, werden die Fehlerinformationen als an den Client übergeben.

**Servercode: `stopCalled` Parameter**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript-Clientcode: `lastError` Zugriff `disconnect` im Ereignis.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
