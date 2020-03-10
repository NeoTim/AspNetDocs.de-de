---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: Aktivieren der signalr-Ablauf Verfolgung | Microsoft-Dokumentation
author: bradygaster
description: In diesem Dokument wird beschrieben, wie die Ablauf Verfolgung für signalr-Server und-Clients aktiviert und konfiguriert wird. Mithilfe der Ablauf Verfolgung können Sie Diagnoseinformationen zu Ereignissen anzeigen...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467439"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="4bf49-104">Aktivieren der Ablaufverfolgung für SignalR</span><span class="sxs-lookup"><span data-stu-id="4bf49-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="4bf49-105">von [Tom fitzmacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4bf49-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4bf49-106">In diesem Dokument wird beschrieben, wie die Ablauf Verfolgung für signalr-Server und-Clients aktiviert und konfiguriert wird.</span><span class="sxs-lookup"><span data-stu-id="4bf49-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="4bf49-107">Mithilfe der Ablauf Verfolgung können Sie Diagnoseinformationen zu Ereignissen in der signalr-Anwendung anzeigen.</span><span class="sxs-lookup"><span data-stu-id="4bf49-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="4bf49-108">Dieses Thema wurde ursprünglich von Patrick Fletcher geschrieben.</span><span class="sxs-lookup"><span data-stu-id="4bf49-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4bf49-109">Im Tutorial verwendete Software Versionen</span><span class="sxs-lookup"><span data-stu-id="4bf49-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="4bf49-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4bf49-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="4bf49-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="4bf49-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="4bf49-112">Signalr Version 2</span><span class="sxs-lookup"><span data-stu-id="4bf49-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="4bf49-113">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="4bf49-113">Questions and comments</span></span>
>
> <span data-ttu-id="4bf49-114">Bitte informieren Sie sich darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren unten auf der Seite verbessern konnten.</span><span class="sxs-lookup"><span data-stu-id="4bf49-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4bf49-115">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie Sie im [ASP.net signalr-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder in [StackOverflow.com](http://stackoverflow.com/)veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="4bf49-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="4bf49-116">Wenn die Ablauf Verfolgung aktiviert ist, erstellt eine signalr-Anwendung Protokolleinträge für Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="4bf49-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="4bf49-117">Sie können Ereignisse sowohl vom Client als auch vom Server protokollieren.</span><span class="sxs-lookup"><span data-stu-id="4bf49-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="4bf49-118">Ablauf Verfolgung auf dem Server protokolliert die Verbindung, den Anbieter für horizontales hochskalieren und Nachrichtenbus Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="4bf49-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="4bf49-119">Bei der Ablauf Verfolgung auf dem Client werden Verbindungs Ereignisse protokolliert.</span><span class="sxs-lookup"><span data-stu-id="4bf49-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="4bf49-120">In signalr 2,1 und höher protokolliert die Ablauf Verfolgung auf dem Client den vollständigen Inhalt von hubaufruf Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="4bf49-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="4bf49-121">Inhalt</span><span class="sxs-lookup"><span data-stu-id="4bf49-121">Contents</span></span>

- [<span data-ttu-id="4bf49-122">Aktivieren der Ablauf Verfolgung auf dem Server</span><span class="sxs-lookup"><span data-stu-id="4bf49-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="4bf49-123">Protokollieren von Server Ereignissen in Textdateien</span><span class="sxs-lookup"><span data-stu-id="4bf49-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="4bf49-124">Protokollieren von Server Ereignissen im Ereignisprotokoll</span><span class="sxs-lookup"><span data-stu-id="4bf49-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="4bf49-125">Aktivieren der Ablauf Verfolgung im .NET-Client (Windows-Desktop-Apps)</span><span class="sxs-lookup"><span data-stu-id="4bf49-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="4bf49-126">Protokollieren von Desktop Client Ereignissen an der Konsole</span><span class="sxs-lookup"><span data-stu-id="4bf49-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="4bf49-127">Protokollieren von Desktop Client Ereignissen in einer Textdatei</span><span class="sxs-lookup"><span data-stu-id="4bf49-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="4bf49-128">Aktivieren der Ablauf Verfolgung in Windows Phone 8-Clients</span><span class="sxs-lookup"><span data-stu-id="4bf49-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="4bf49-129">Protokollieren von Windows Phone Client Ereignissen auf der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="4bf49-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="4bf49-130">Protokollieren von Windows Phone Client Ereignissen in der Debug-Konsole</span><span class="sxs-lookup"><span data-stu-id="4bf49-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="4bf49-131">Aktivieren der Ablauf Verfolgung im JavaScript-Client</span><span class="sxs-lookup"><span data-stu-id="4bf49-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="4bf49-132">Aktivieren der Ablauf Verfolgung auf dem Server</span><span class="sxs-lookup"><span data-stu-id="4bf49-132">Enabling tracing on the server</span></span>

<span data-ttu-id="4bf49-133">Sie aktivieren die Ablauf Verfolgung auf dem Server in der Konfigurationsdatei der Anwendung ("App. config" oder "Web. config", je nach Projekttyp). Sie geben an, welche Kategorien von Ereignissen Sie protokollieren möchten.</span><span class="sxs-lookup"><span data-stu-id="4bf49-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="4bf49-134">In der Konfigurationsdatei geben Sie auch an, ob die Ereignisse in einer Textdatei, im Windows-Ereignisprotokoll oder in einem benutzerdefinierten Protokoll mithilfe einer Implementierung von [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)protokolliert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4bf49-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="4bf49-135">Die Server Ereignis Kategorien umfassen die folgenden Arten von Nachrichten:</span><span class="sxs-lookup"><span data-stu-id="4bf49-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="4bf49-136">`Source`</span><span class="sxs-lookup"><span data-stu-id="4bf49-136">Source</span></span> | <span data-ttu-id="4bf49-137">Meldungen</span><span class="sxs-lookup"><span data-stu-id="4bf49-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="4bf49-138">SignalR.SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="4bf49-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="4bf49-139">Setup für den SQL-Nachrichtenbus-Anbieter für horizontales Skalieren, Daten Bank Vorgänge, Fehler und Timeout</span><span class="sxs-lookup"><span data-stu-id="4bf49-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="4bf49-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="4bf49-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="4bf49-141">Service Bus-Anbieter für horizontales Skalieren: Erstellen von und Abonnement-, Fehler-und Messaging Ereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="4bf49-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="4bf49-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="4bf49-143">Redis-Anbieter Verbindung für horizontales hochskalieren, Verbindungsfehler und Fehlerereignisse</span><span class="sxs-lookup"><span data-stu-id="4bf49-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="4bf49-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="4bf49-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="4bf49-145">Horizontales Skalieren von Messaging Ereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="4bf49-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="4bf49-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="4bf49-147">WebSocket-Transport Verbindung, trennen von Verbindungs-, Messaging-und Fehlerereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="4bf49-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="4bf49-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="4bf49-149">Serversentevents-Transport Verbindung, trennen von Verbindungs-, Messaging-und Fehlerereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="4bf49-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="4bf49-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="4bf49-151">Foreverframe-Transport Verbindung, trennen von Verbindungs-, Messaging-und Fehlerereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="4bf49-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="4bf49-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="4bf49-153">Longabruf-Transport Verbindung, trennen von Verbindungs-, Messaging-und Fehlerereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="4bf49-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="4bf49-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="4bf49-155">Transport Verbindung, trennen von Verbindungen und KeepAlive-Ereignissen</span><span class="sxs-lookup"><span data-stu-id="4bf49-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="4bf49-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="4bf49-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="4bf49-157">Hub-Ermittlungs Ereignisse</span><span class="sxs-lookup"><span data-stu-id="4bf49-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="4bf49-158">Protokollieren von Server Ereignissen in Textdateien</span><span class="sxs-lookup"><span data-stu-id="4bf49-158">Logging server events to text files</span></span>

<span data-ttu-id="4bf49-159">Der folgende Code zeigt, wie die Ablauf Verfolgung für jede Ereignis Kategorie aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="4bf49-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="4bf49-160">In diesem Beispiel wird die Anwendung so konfiguriert, dass Ereignisse in Textdateien protokolliert werden.</span><span class="sxs-lookup"><span data-stu-id="4bf49-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="4bf49-161">**XML-Servercode zum Aktivieren der Ablauf Verfolgung**</span><span class="sxs-lookup"><span data-stu-id="4bf49-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="4bf49-162">Im obigen Code gibt der `SignalRSwitch` Eintrag den [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) an, der für Ereignisse verwendet wird, die an das angegebene Protokoll gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="4bf49-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="4bf49-163">In diesem Fall wird Sie auf `Verbose` festgelegt, was bedeutet, dass alle Debugging-und Ablauf Verfolgungs Meldungen protokolliert werden.</span><span class="sxs-lookup"><span data-stu-id="4bf49-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="4bf49-164">Die folgende Ausgabe zeigt Einträge aus der `transports.log.txt`-Datei für eine Anwendung, die die oben beschriebene Konfigurationsdatei verwendet.</span><span class="sxs-lookup"><span data-stu-id="4bf49-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="4bf49-165">Es werden eine neue Verbindung, eine entfernte Verbindung und Transport Takt Ereignisse angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4bf49-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="4bf49-166">Protokollieren von Server Ereignissen im Ereignisprotokoll</span><span class="sxs-lookup"><span data-stu-id="4bf49-166">Logging server events to the event log</span></span>

<span data-ttu-id="4bf49-167">Um Ereignisse anstelle einer Textdatei im Ereignisprotokoll zu protokollieren, ändern Sie die Werte für die Einträge im Knoten `sharedListeners`.</span><span class="sxs-lookup"><span data-stu-id="4bf49-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="4bf49-168">Der folgende Code zeigt, wie Server Ereignisse im Ereignisprotokoll protokolliert werden:</span><span class="sxs-lookup"><span data-stu-id="4bf49-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="4bf49-169">**XML-Servercode zum Protokollieren von Ereignissen im Ereignisprotokoll**</span><span class="sxs-lookup"><span data-stu-id="4bf49-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="4bf49-170">Die Ereignisse werden im Anwendungsprotokoll protokolliert und sind über die Ereignisanzeige verfügbar, wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="4bf49-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![Ereignisanzeige mit signalr-Protokollen](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="4bf49-172">Wenn Sie das Ereignisprotokoll verwenden, legen Sie für die **TraceLevel** den Wert " **Error** " fest, um die Anzahl der Nachrichten beizubehalten.</span><span class="sxs-lookup"><span data-stu-id="4bf49-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="4bf49-173">Aktivieren der Ablauf Verfolgung im .NET-Client (Windows-Desktop-Apps)</span><span class="sxs-lookup"><span data-stu-id="4bf49-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="4bf49-174">Der .NET-Client kann mit einer Implementierung von [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)Ereignisse in der Konsole, in einer Textdatei oder in einem benutzerdefinierten Protokoll protokollieren.</span><span class="sxs-lookup"><span data-stu-id="4bf49-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="4bf49-175">Wenn Sie die Protokollierung im .NET-Client aktivieren möchten, legen Sie die `TraceLevel`-Eigenschaft der Verbindung auf einen [Tracelevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) -Wert und die Eigenschaft `TraceWriter` auf eine gültige [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) -Instanz fest.</span><span class="sxs-lookup"><span data-stu-id="4bf49-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="4bf49-176">Protokollieren von Desktop Client Ereignissen an der Konsole</span><span class="sxs-lookup"><span data-stu-id="4bf49-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="4bf49-177">Der folgende C# Code zeigt, wie Ereignisse im .NET-Client in der Konsole protokolliert werden:</span><span class="sxs-lookup"><span data-stu-id="4bf49-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="4bf49-178">Protokollieren von Desktop Client Ereignissen in einer Textdatei</span><span class="sxs-lookup"><span data-stu-id="4bf49-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="4bf49-179">Der folgende C# Code zeigt, wie Ereignisse im .NET-Client in einer Textdatei protokolliert werden:</span><span class="sxs-lookup"><span data-stu-id="4bf49-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="4bf49-180">Die folgende Ausgabe zeigt Einträge aus der `ClientLog.txt`-Datei für eine Anwendung, die die oben beschriebene Konfigurationsdatei verwendet.</span><span class="sxs-lookup"><span data-stu-id="4bf49-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="4bf49-181">Es zeigt den Client, der eine Verbindung mit dem Server herstellt, und der Hub, der eine Client Methode mit dem Namen `addMessage`aufruft:</span><span class="sxs-lookup"><span data-stu-id="4bf49-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="4bf49-182">Aktivieren der Ablauf Verfolgung in Windows Phone 8-Clients</span><span class="sxs-lookup"><span data-stu-id="4bf49-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="4bf49-183">Signalr-Anwendungen für Windows Phone-Apps verwenden denselben .NET-Client wie Desktop-Apps, aber [Console. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) und das Schreiben in eine Datei mit [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) sind nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="4bf49-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="4bf49-184">Stattdessen müssen Sie eine benutzerdefinierte Implementierung von [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) für die Ablauf Verfolgung erstellen.</span><span class="sxs-lookup"><span data-stu-id="4bf49-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="4bf49-185">Protokollieren von Windows Phone Client Ereignissen auf der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="4bf49-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="4bf49-186">Die [signalr-Codebasis](https://github.com/SignalR/SignalR/archive/master.zip) enthält ein Windows Phone Beispiel, das die Ablauf Verfolgungs Ausgabe mithilfe einer benutzerdefinierten [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) -Implementierung namens `TextBlockWriter`in einen [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) schreibt.</span><span class="sxs-lookup"><span data-stu-id="4bf49-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="4bf49-187">Diese Klasse befindet sich im Projekt **Samples/Microsoft. Aspnet. signalr. Client. WP8. Samples** .</span><span class="sxs-lookup"><span data-stu-id="4bf49-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="4bf49-188">Wenn Sie eine Instanz von `TextBlockWriter`erstellen, übergeben Sie den aktuellen [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)und einen [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , in dem ein [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) erstellt wird, der für die Ausgabe der Ablauf Verfolgung verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="4bf49-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="4bf49-189">Die Ausgabe der Ablauf Verfolgung wird dann in einen neuen [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) geschrieben, der im [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) erstellt wurde, das Sie eingegeben haben:</span><span class="sxs-lookup"><span data-stu-id="4bf49-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="4bf49-190">Protokollieren von Windows Phone Client Ereignissen in der Debug-Konsole</span><span class="sxs-lookup"><span data-stu-id="4bf49-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="4bf49-191">Um die Ausgabe an die Debugkonsole anstatt an die Benutzeroberfläche zu senden, erstellen Sie eine [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) -Implementierung, die in das Debugfenster schreibt, und weisen Sie Sie der Eigenschaft [traceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) ihrer Verbindung zu:</span><span class="sxs-lookup"><span data-stu-id="4bf49-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="4bf49-192">Ablauf Verfolgungs Informationen werden dann in das Debugfenster in Visual Studio geschrieben:</span><span class="sxs-lookup"><span data-stu-id="4bf49-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="4bf49-193">Aktivieren der Ablauf Verfolgung im JavaScript-Client</span><span class="sxs-lookup"><span data-stu-id="4bf49-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="4bf49-194">Um die Client seitige Protokollierung für eine Verbindung zu aktivieren, legen Sie die `logging`-Eigenschaft für das Verbindungs Objekt fest, bevor Sie die `start`-Methode zum Herstellen der Verbindung aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="4bf49-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="4bf49-195">**JavaScript-Client Code zum Aktivieren der Ablauf Verfolgung für die Browser Konsole (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="4bf49-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="4bf49-196">**JavaScript-Client Code zum Aktivieren der Ablauf Verfolgung in der Browser Konsole (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="4bf49-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="4bf49-197">Wenn die Ablauf Verfolgung aktiviert ist, protokolliert der JavaScript-Client Ereignisse in der Browser Konsole.</span><span class="sxs-lookup"><span data-stu-id="4bf49-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="4bf49-198">Informationen zum Zugriff auf die Browser Konsole finden Sie unter über [Wachen von Transporten](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span><span class="sxs-lookup"><span data-stu-id="4bf49-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="4bf49-199">Der folgende Screenshot zeigt einen signalr-JavaScript-Client mit aktivierter Ablauf Verfolgung.</span><span class="sxs-lookup"><span data-stu-id="4bf49-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="4bf49-200">Es werden Verbindungs-und hubaufruf Ereignisse in der Browser Konsole angezeigt:</span><span class="sxs-lookup"><span data-stu-id="4bf49-200">It shows connection and hub invocation events in the browser console:</span></span>

![Signalr-Ablauf Verfolgungs Ereignisse in der Browser Konsole](enabling-signalr-tracing/_static/image4.png)
