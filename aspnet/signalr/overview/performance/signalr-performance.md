---
uid: signalr/overview/performance/signalr-performance
title: SignalR-Leistung | Microsoft Docs
author: bradygaster
description: SignalR-Leistung
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675718"
---
# <a name="signalr-performance"></a>SignalR-Leistung

von [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> In diesem Thema wird beschrieben, wie Sie die Leistung in einer SignalR-Anwendung entwerfen, messen und verbessern.
>
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

Eine aktuelle Präsentation zur SignalR-Leistung und -Skalierung finden Sie unter [Skalieren des Echtzeit-Webs mit ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).

Dieses Thema enthält folgende Abschnitte:

- [Überlegungen zum Entwurf](#design)
- [Optimieren Ihres SignalR-Servers für die Leistung](#tuning)
- [Problembehandlung bei Leistungsproblemen](#troubleshooting)
- [Verwenden von SignalR-Leistungsindikatoren](#perfcounters)
- [Verwenden anderer Leistungsindikatoren](#othercounters)
- [Sonstige Ressourcen](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Überlegungen zum Entwurf

In diesem Abschnitt werden Muster beschrieben, die während des Entwurfs einer SignalR-Anwendung implementiert werden können, um sicherzustellen, dass die Leistung nicht durch die Generierung unnötigen Netzwerkdatenverkehrs beeinträchtigt wird.

### <a name="throttling-message-frequency"></a>Drosselung der Nachrichtenhäufigkeit

Selbst in einer Anwendung, die Nachrichten mit hoher Frequenz sendet (z. B. eine Echtzeit-Gaming-Anwendung), müssen die meisten Anwendungen nicht mehr als ein paar Nachrichten pro Sekunde senden. Um den Datenverkehrzulierungsaufwand zu reduzieren, den jeder Client generiert, kann eine Nachrichtenschleife implementiert werden, die Nachrichten nicht häufiger als eine feste Rate in die Warteschlange stellt und sendet (d. h. bis zu einer bestimmten Anzahl von Nachrichten wird jede Sekunde gesendet, wenn Nachrichten in diesem Zeitintervall gesendet werden sollen). Eine Beispielanwendung, die Nachrichten auf eine bestimmte Rate (sowohl vom Client als auch vom Server) drosselt, finden Sie unter [Hochfrequenz-Echtzeit mit SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>Verringern der Nachrichtengröße

Sie können die Größe einer SignalR-Nachricht reduzieren, indem Sie die Größe Ihrer serialisierten Objekte reduzieren. Wenn Sie im Servercode ein Objekt senden, das Eigenschaften enthält, die nicht übertragen werden müssen, `JsonIgnore` verhindern Sie, dass diese Eigenschaften mithilfe des Attributs serialisiert werden. Die Namen der Eigenschaften werden ebenfalls in der Nachricht gespeichert. Die Namen von Eigenschaften können `JsonProperty` mit dem Attribut gekürzt werden. Im folgenden Codebeispiel wird veranschaulicht, wie eine Eigenschaft vom Senden an den Client ausgeschlossen und Eigenschaftsnamen gekürzt werden:

**.NET-Servercode, der das JsonIgnore-Attribut demonstriert, um Daten vom Senden an den Client auszuschließen, und das JsonProperty-Attribut, um die Nachrichtengröße zu reduzieren**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

Um die Lesbarkeit/Wartbarkeit im Clientcode beizubehalten, können die abgekürzten Eigenschaftsnamen nach dem Empfangen der Nachricht den namenweisend neu zugeordnet werden. Das folgende Codebeispiel veranschaulicht eine möglichkeit, verkürzte Namen auf längere zuzuordnen, indem `reMap` ein Nachrichtenkontrakt (Mapping) definiert und die Funktion verwendet wird, um den Vertrag auf die optimierte Nachrichtenklasse anzuwenden:

**Clientseitigem JavaScript-Code, der verkürzte Eigenschaftsnamen zu lesbaren Namen neu zuordnet**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Namen können auch in Nachrichten vom Client an den Server gekürzt werden, mit der gleichen Methode.

Das Reduzieren des Speicherbedarfs (d. h. der für die Nachricht verwendete Speicher) des Nachrichtenobjekts kann auch die Leistung verbessern. Wenn z. B. der `int` gesamte Bereich `short` von `byte` an nicht benötigt wird, kann stattdessen ein oder verwendet werden.

Da Nachrichten im Nachrichtenbus im Serverspeicher gespeichert werden, kann durch die Verkleinerung der Nachrichten auch Probleme mit dem Serverspeicher beschwichtigt werden.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Optimieren Ihres SignalR-Servers für die Leistung

Die folgenden Konfigurationseinstellungen können verwendet werden, um Den Server für eine bessere Leistung in einer SignalR-Anwendung zu optimieren. Allgemeine Informationen zur Verbesserung der Leistung in einer ASP.NET Anwendung finden Sie unter [Verbessern ASP.NET Leistung](https://msdn.microsoft.com/library/ff647787.aspx).

**SignalR-Konfigurationseinstellungen**

- **DefaultMessageBufferSize**: Standardmäßig behält SignalR 1000 Nachrichten pro Hub pro Verbindung im Arbeitsspeicher bei. Wenn große Nachrichten verwendet werden, kann dies zu Speicherproblemen führen, die durch Verringern dieses Werts verringert werden können. Diese Einstellung kann im `Application_Start` Ereignishandler in einer ASP.NET `Configuration` Anwendung oder in der Methode einer OWIN-Startklasse in einer selbst gehosteten Anwendung festgelegt werden. Im folgenden Beispiel wird veranschaulicht, wie Sie diesen Wert reduzieren können, um den Speicherbedarf Ihrer Anwendung zu reduzieren, um die Menge des verwendeten Serverspeichers zu reduzieren:

    **.NET-Servercode in Startup.cs für die Verringerung der Standardnachrichtenpuffergröße**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS-Konfigurationseinstellungen**

- **Max. gleichzeitige Anforderungen pro Anwendung:** Wenn Sie die Anzahl der gleichzeitigen IIS-Anforderungen erhöhen, werden die Fürstand der Serverressourcen für die Zustellung von Anforderungen erhöht. Der Standardwert ist 5000; Um diese Einstellung zu erhöhen, führen Sie die folgenden Befehle in einer erhöhten Eingabeaufforderung aus:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: Dies ist die maximale Anzahl von Anforderungen, die Http.sys für den Anwendungspool in die Warteschlange stellt. Wenn die Warteschlange voll ist, erhalten neue Anforderungen eine Antwort 503 "Service Nicht verfügbar". Der Standardwert lautet „1000“.

    Durch das Verkürzen der Warteschlangenlänge für den Arbeitsprozess im Anwendungspool, in dem Ihre Anwendung gehostet wird, werden Speicherressourcen geschont. Weitere Informationen finden Sie unter [Verwalten, Optimieren und Konfigurieren von Anwendungspools](https://technet.microsoft.com/library/cc745955.aspx).

**ASP.NET Konfigurationseinstellungen**

Dieser Abschnitt enthält Konfigurationseinstellungen, die `aspnet.config` in der Datei festgelegt werden können. Diese Datei befindet sich je nach Plattform an einem von zwei Speicherorten:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

ASP.NET Einstellungen, die die SignalR-Leistung verbessern können, umfassen die folgenden:

- **Maximale anzahlstelle gleichzeitige Anforderungen pro CPU:** Wenn Sie diese Einstellung erhöhen, können Leistungsengpässe verringert werden. Um diese Einstellung zu erhöhen, fügen `aspnet.config` Sie der Datei die folgende Konfigurationseinstellung hinzu:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Anforderungswarteschlangenlimit**: Wenn die Gesamtzahl `maxConcurrentRequestsPerCPU` der Verbindungen die Einstellung überschreitet, beginnt ASP.NET mit der Drosselung von Anforderungen mithilfe einer Warteschlange. Um die Größe der Warteschlange zu `requestQueueLimit` erhöhen, können Sie die Einstellung erhöhen. Fügen Sie dazu die folgende Konfigurationseinstellung `processModel` `config/machine.config` zum Knoten `aspnet.config`in hinzu (anstelle von):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Problembehandlung bei Leistungsproblemen

In diesem Abschnitt werden Möglichkeiten beschrieben, wie Sie Leistungsengpässe in Ihrer Anwendung ermitteln können.

### <a name="verifying-that-websocket-is-being-used"></a>Überprüfen, ob WebSocket verwendet wird

Während SignalR eine Vielzahl von Transporten für die Kommunikation zwischen Client und Server verwenden kann, bietet WebSocket einen erheblichen Leistungsvorteil und sollte verwendet werden, wenn der Client und der Server dies unterstützen. Informationen dazu, ob Client und Server die Anforderungen für WebSocket erfüllen, finden Sie unter [Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports). Um zu ermitteln, welcher Transport in Ihrer Anwendung verwendet wird, können Sie die Browserentwicklertools verwenden und die Protokolle untersuchen, um zu sehen, welcher Transport für die Verbindung verwendet wird. Informationen zur Verwendung der Browserentwicklungstools in Internet Explorer und Chrome finden Sie unter [Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>Verwenden von SignalR-Leistungsindikatoren

In diesem Abschnitt wird beschrieben, wie Sie SignalR-Leistungsindikatoren aktivieren und verwenden, die `Microsoft.AspNet.SignalR.Utils` im Paket enthalten sind.

### <a name="installing-signalrexe"></a>Installieren von signalr.exe

Leistungsindikatoren können dem Server mithilfe eines Dienstprogramms namens SignalR.exe hinzugefügt werden. Gehen Sie folgendzu, um dieses Dienstprogramm zu installieren:

1. Wählen Sie in Visual Studio **Tools** > **NuGet Package Manager** > **Verwalten von NuGet-Paketen für die Lösung** aus.
2. Suchen Sie nach **signalr.utils**, und wählen Sie Installieren aus.

    ![](signalr-performance/_static/image1.png)
3. Akzeptieren Sie den Lizenzvertrag, um das Paket zu installieren.
4. SignalR.exe wird auf `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`installiert.

### <a name="installing-performance-counters-with-signalrexe"></a>Installieren von Leistungsindikatoren mit SignalR.exe

Um SignalR-Leistungsindikatoren zu installieren, führen Sie SignalR.exe in einer erhöhten Eingabeaufforderung mit dem folgenden Parameter aus:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

Um SignalR-Leistungsindikatoren zu entfernen, führen Sie SignalR.exe in einer erhöhten Eingabeaufforderung mit dem folgenden Parameter aus:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR-Leistungsindikatoren

Das Dienstprogrammpaket installiert die folgenden Leistungsindikatoren. Die Leistungsindikatoren "Gesamt" messen die Anzahl der Ereignisse seit dem letzten Anwendungspool oder Serverneustart.

**Verbindungsmetriken**

Die folgenden Metriken messen die auftretenden Ereignisse der Verbindungslebensdauer. Weitere Informationen finden Sie [unter Grundlegendes zum Verstehen und Behandeln von Verbindungsereignissen](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Verbindungen verbunden**
- **Verbindungen wieder verbunden**
- **Verbindungen getrennt**
- **Verbindungen Strom**

**Nachrichtenmetriken**

Die folgenden Metriken messen den von SignalR generierten Nachrichtenverkehr.

- **Empfangene Verbindungsmeldungen Insgesamt**
- **Verbindungsmeldungen insgesamt gesendet**
- **Empfangene Verbindungsnachrichten/Sek.**
- **Gesendete Verbindungsnachrichten/Sek.**

**Nachrichtenbusmetriken**

Die folgenden Metriken messen den Datenverkehr über den internen SignalR-Nachrichtenbus, die Warteschlange, in der alle eingehenden und ausgehenden SignalR-Nachrichten platziert werden. Eine Nachricht wird **veröffentlicht,** wenn sie gesendet oder gesendet wird. Ein **Abonnent** in diesem Kontext ist ein Abonnement für den Nachrichtenbus. Dies sollte der Anzahl der Clients plus dem Server selbst entsprechen. Eine **zugewiesene Arbeitskraft** ist eine Komponente, die Daten an aktive Verbindungen sendet. Ein **beschäftigter Worker** sendet aktiv eine Nachricht.

- **Nachricht Bus Nachrichten empfangen Insgesamt**
- **Empfangene Nachrichten nachrichten/Sek.**
- **Nachricht Bus-Nachrichten veröffentlicht Insgesamt**
- **Nachricht Bus Nachrichten veröffentlicht/Sek**
- **Nachricht Busabonnenten Aktuell**
- **Nachricht Busabonnenten Insgesamt**
- **Nachricht Busabonnenten/Sek.**
- **Message Bus Allocated Workers**
- **Nachricht Bus Beschäftigte Arbeiter**
- **Message Bus Themen Aktuell**

**Fehlermetriken**

Die folgenden Metriken messen Fehler, die durch den SignalR-Nachrichtenverkehr generiert wurden. **Hubauflösungsfehler** treten auf, wenn eine Hub- oder Hubmethode nicht aufgelöst werden kann. **Hubaufruffehler** sind Ausnahmen, die beim Aufrufen einer Hubmethode ausgelöst werden. **Transportfehler** sind Verbindungsfehler, die während einer HTTP-Anforderung oder -Antwort ausgelöst werden.

- **Fehler: Alle insgesamt**
- **Fehler: Alle/Sek.**
- **Fehler: Hub-Auflösung insgesamt**
- **Fehler: Hub-Auflösung/Sek.**
- **Fehler: Hub-Aufruf insgesamt**
- **Fehler: Hub-Aufruf/Sek.**
- **Fehler: Transport Summe**
- **Fehler: Transport/Sec**

<a id="scaleout_metrics"></a>

**Scaleout-Metriken**

Die folgenden Metriken messen Datenverkehr und Fehler, die vom Scaleoutanbieter generiert werden. Ein **Stream** ist in diesem Kontext eine Skalierungseinheit, die vom Scaleout-Anbieter verwendet wird. Dies ist eine Tabelle, wenn SQL Server verwendet wird, ein Thema, wenn Service Bus verwendet wird, und ein Abonnement, wenn Redis verwendet wird. Jeder Stream stellt geordnete Lese- und Schreibvorgänge sicher. Ein einzelner Stream ist ein potenzieller Skalierungsengpass, sodass die Anzahl der Streams erhöht werden kann, um diesen Engpass zu verringern. Wenn mehrere Streams verwendet werden, verteilt SignalR automatisch (Shard-)Nachrichten über diese Streams in einer Weise, die sicherstellt, dass Nachrichten, die von einer bestimmten Verbindung gesendet werden, in Ordnung sind.

Die [Einstellung MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) steuert die Länge der von SignalR verwalteten Skalierungssssendewarteschlange. Wenn Sie ihn auf einen Wert größer als 0 setzen, werden alle Nachrichten in einer Sendewarteschlange platziert, die nacheinander an die konfigurierte Messaging-Backplane gesendet werden. Wenn die Größe der Warteschlange über die konfigurierte Länge geht, schlagen nachfolgende Aufrufe zum Senden sofort mit einer [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) fehl, bis die Anzahl der Nachrichten in der Warteschlange erneut kleiner als die Einstellung ist. Die Warteschlange ist standardmäßig deaktiviert, da die implementierten Backplanes im Allgemeinen über eine eigene Warteschlange oder Flusssteuerung verfügen. Im Fall von SQL Server begrenzt das Verbindungspooling effektiv die Anzahl der Sendezeiten, die zu einem beliebigen Zeitpunkt ausgeführt werden.

Standardmäßig wird nur ein Stream für SQL Server und Redis verwendet, fünf Streams werden für Service Bus verwendet, und die Warteschlange ist deaktiviert, aber diese Einstellungen können durch Die Konfiguration auf SQL Server und Service Bus geändert werden:

**.NET ServerCode zum Konfigurieren der Tabellenanzahl und Warteschlangenlänge für SQL Server-Backplane**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**.NET ServerCode zum Konfigurieren der Themenanzahl und Warteschlangenlänge für Die Service Bus-Backplane**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

Ein Pufferstream ist ein **Stream,** der in einen fehlerhaften Zustand eingetreten ist. Wenn sich der Stream im fehlerhaften Zustand befindet, schlagen alle nachrichten, die an die Backplane gesendet werden, sofort fehl, bis der Stream keinen Fehler mehr macht. Die Länge der **Sendewarteschlange** ist die Anzahl der Nachrichten, die gesendet, aber noch nicht gesendet wurden.

- **Scaleout Message Bus Empfangene/Sek.**
- **Scaleout-Streams insgesamt**
- **Scaleout Streams geöffnet**
- **Scaleout Streams Buffering**
- **Scaleout-Fehler insgesamt**
- **Scaleout-Fehler/Sek.**
- **Scaleout-Sendewarteschlangenlänge**

Weitere Informationen zu den Messpunkten dieser Leistungsindikatoren finden Sie unter [SignalR Scaleout mit Azure Service Bus](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Verwenden anderer Leistungsindikatoren

Die folgenden Leistungsindikatoren können auch bei der Überwachung der Leistung Ihrer Anwendung nützlich sein.

**Memory**

- .NET CLR-Speicher\\in allen Heaps (für w3wp)

**ASP.NET**

- ASP.NET-Anforderungen aktuell
- ASP.NET-Warteschlange
- ASP.NET-Abgelehnt

**CPU**

- Prozessorinformationen,Prozessorzeit

**TCP/IP**

- TCPv6/Verbindungen eingerichtet
- TCPv4/Verbindungen eingerichtet

**Webdienst**

- Webdienst- und aktuelle Verbindungen
- Webdienst-Maximale Verbindungen

**Threading**

- .NET CLR-Sperren\\und -Threads der aktuellen logischen Threads
- .NET CLR-Sperren\\und -Threads von aktuellen physikalischen Threads

<a id="otherresources"></a>

## <a name="other-resources"></a>Weitere Ressourcen

Weitere Informationen zur ASP.NET Leistungsüberwachung und -optimierung finden Sie in den folgenden Themen:

- [ASP.NET Performance Overview (Die Leistung von ASP.NET im Überblick)](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [ASP.NET Threadverwendung auf IIS 7.5, IIS 7.0 und IIS 6.0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; Element (Webeinstellungen)](https://msdn.microsoft.com/library/dd560842.aspx)
