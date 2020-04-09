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
# <a name="signalr-performance"></a><span data-ttu-id="58d7f-103">SignalR-Leistung</span><span class="sxs-lookup"><span data-stu-id="58d7f-103">SignalR Performance</span></span>

<span data-ttu-id="58d7f-104">von [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="58d7f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="58d7f-105">In diesem Thema wird beschrieben, wie Sie die Leistung in einer SignalR-Anwendung entwerfen, messen und verbessern.</span><span class="sxs-lookup"><span data-stu-id="58d7f-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="58d7f-106">In diesem Thema verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="58d7f-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="58d7f-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="58d7f-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="58d7f-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="58d7f-108">.NET 4.5</span></span>
> - <span data-ttu-id="58d7f-109">SignalR Version 2</span><span class="sxs-lookup"><span data-stu-id="58d7f-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="58d7f-110">Frühere Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="58d7f-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="58d7f-111">Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="58d7f-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="58d7f-112">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="58d7f-112">Questions and comments</span></span>
>
> <span data-ttu-id="58d7f-113">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="58d7f-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="58d7f-114">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="58d7f-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="58d7f-115">Eine aktuelle Präsentation zur SignalR-Leistung und -Skalierung finden Sie unter [Skalieren des Echtzeit-Webs mit ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span><span class="sxs-lookup"><span data-stu-id="58d7f-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="58d7f-116">Dieses Thema enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="58d7f-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="58d7f-117">Überlegungen zum Entwurf</span><span class="sxs-lookup"><span data-stu-id="58d7f-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="58d7f-118">Optimieren Ihres SignalR-Servers für die Leistung</span><span class="sxs-lookup"><span data-stu-id="58d7f-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="58d7f-119">Problembehandlung bei Leistungsproblemen</span><span class="sxs-lookup"><span data-stu-id="58d7f-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="58d7f-120">Verwenden von SignalR-Leistungsindikatoren</span><span class="sxs-lookup"><span data-stu-id="58d7f-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="58d7f-121">Verwenden anderer Leistungsindikatoren</span><span class="sxs-lookup"><span data-stu-id="58d7f-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="58d7f-122">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="58d7f-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="58d7f-123">Überlegungen zum Entwurf</span><span class="sxs-lookup"><span data-stu-id="58d7f-123">Design considerations</span></span>

<span data-ttu-id="58d7f-124">In diesem Abschnitt werden Muster beschrieben, die während des Entwurfs einer SignalR-Anwendung implementiert werden können, um sicherzustellen, dass die Leistung nicht durch die Generierung unnötigen Netzwerkdatenverkehrs beeinträchtigt wird.</span><span class="sxs-lookup"><span data-stu-id="58d7f-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="58d7f-125">Drosselung der Nachrichtenhäufigkeit</span><span class="sxs-lookup"><span data-stu-id="58d7f-125">Throttling message frequency</span></span>

<span data-ttu-id="58d7f-126">Selbst in einer Anwendung, die Nachrichten mit hoher Frequenz sendet (z. B. eine Echtzeit-Gaming-Anwendung), müssen die meisten Anwendungen nicht mehr als ein paar Nachrichten pro Sekunde senden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="58d7f-127">Um den Datenverkehrzulierungsaufwand zu reduzieren, den jeder Client generiert, kann eine Nachrichtenschleife implementiert werden, die Nachrichten nicht häufiger als eine feste Rate in die Warteschlange stellt und sendet (d. h. bis zu einer bestimmten Anzahl von Nachrichten wird jede Sekunde gesendet, wenn Nachrichten in diesem Zeitintervall gesendet werden sollen).</span><span class="sxs-lookup"><span data-stu-id="58d7f-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="58d7f-128">Eine Beispielanwendung, die Nachrichten auf eine bestimmte Rate (sowohl vom Client als auch vom Server) drosselt, finden Sie unter [Hochfrequenz-Echtzeit mit SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="58d7f-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="58d7f-129">Verringern der Nachrichtengröße</span><span class="sxs-lookup"><span data-stu-id="58d7f-129">Reducing message size</span></span>

<span data-ttu-id="58d7f-130">Sie können die Größe einer SignalR-Nachricht reduzieren, indem Sie die Größe Ihrer serialisierten Objekte reduzieren.</span><span class="sxs-lookup"><span data-stu-id="58d7f-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="58d7f-131">Wenn Sie im Servercode ein Objekt senden, das Eigenschaften enthält, die nicht übertragen werden müssen, `JsonIgnore` verhindern Sie, dass diese Eigenschaften mithilfe des Attributs serialisiert werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="58d7f-132">Die Namen der Eigenschaften werden ebenfalls in der Nachricht gespeichert. Die Namen von Eigenschaften können `JsonProperty` mit dem Attribut gekürzt werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="58d7f-133">Im folgenden Codebeispiel wird veranschaulicht, wie eine Eigenschaft vom Senden an den Client ausgeschlossen und Eigenschaftsnamen gekürzt werden:</span><span class="sxs-lookup"><span data-stu-id="58d7f-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="58d7f-134">**.NET-Servercode, der das JsonIgnore-Attribut demonstriert, um Daten vom Senden an den Client auszuschließen, und das JsonProperty-Attribut, um die Nachrichtengröße zu reduzieren**</span><span class="sxs-lookup"><span data-stu-id="58d7f-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="58d7f-135">Um die Lesbarkeit/Wartbarkeit im Clientcode beizubehalten, können die abgekürzten Eigenschaftsnamen nach dem Empfangen der Nachricht den namenweisend neu zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="58d7f-136">Das folgende Codebeispiel veranschaulicht eine möglichkeit, verkürzte Namen auf längere zuzuordnen, indem `reMap` ein Nachrichtenkontrakt (Mapping) definiert und die Funktion verwendet wird, um den Vertrag auf die optimierte Nachrichtenklasse anzuwenden:</span><span class="sxs-lookup"><span data-stu-id="58d7f-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="58d7f-137">**Clientseitigem JavaScript-Code, der verkürzte Eigenschaftsnamen zu lesbaren Namen neu zuordnet**</span><span class="sxs-lookup"><span data-stu-id="58d7f-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="58d7f-138">Namen können auch in Nachrichten vom Client an den Server gekürzt werden, mit der gleichen Methode.</span><span class="sxs-lookup"><span data-stu-id="58d7f-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="58d7f-139">Das Reduzieren des Speicherbedarfs (d. h. der für die Nachricht verwendete Speicher) des Nachrichtenobjekts kann auch die Leistung verbessern.</span><span class="sxs-lookup"><span data-stu-id="58d7f-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="58d7f-140">Wenn z. B. der `int` gesamte Bereich `short` von `byte` an nicht benötigt wird, kann stattdessen ein oder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="58d7f-141">Da Nachrichten im Nachrichtenbus im Serverspeicher gespeichert werden, kann durch die Verkleinerung der Nachrichten auch Probleme mit dem Serverspeicher beschwichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="58d7f-142">Optimieren Ihres SignalR-Servers für die Leistung</span><span class="sxs-lookup"><span data-stu-id="58d7f-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="58d7f-143">Die folgenden Konfigurationseinstellungen können verwendet werden, um Den Server für eine bessere Leistung in einer SignalR-Anwendung zu optimieren.</span><span class="sxs-lookup"><span data-stu-id="58d7f-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="58d7f-144">Allgemeine Informationen zur Verbesserung der Leistung in einer ASP.NET Anwendung finden Sie unter [Verbessern ASP.NET Leistung](https://msdn.microsoft.com/library/ff647787.aspx).</span><span class="sxs-lookup"><span data-stu-id="58d7f-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="58d7f-145">**SignalR-Konfigurationseinstellungen**</span><span class="sxs-lookup"><span data-stu-id="58d7f-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="58d7f-146">**DefaultMessageBufferSize**: Standardmäßig behält SignalR 1000 Nachrichten pro Hub pro Verbindung im Arbeitsspeicher bei.</span><span class="sxs-lookup"><span data-stu-id="58d7f-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="58d7f-147">Wenn große Nachrichten verwendet werden, kann dies zu Speicherproblemen führen, die durch Verringern dieses Werts verringert werden können.</span><span class="sxs-lookup"><span data-stu-id="58d7f-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="58d7f-148">Diese Einstellung kann im `Application_Start` Ereignishandler in einer ASP.NET `Configuration` Anwendung oder in der Methode einer OWIN-Startklasse in einer selbst gehosteten Anwendung festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="58d7f-149">Im folgenden Beispiel wird veranschaulicht, wie Sie diesen Wert reduzieren können, um den Speicherbedarf Ihrer Anwendung zu reduzieren, um die Menge des verwendeten Serverspeichers zu reduzieren:</span><span class="sxs-lookup"><span data-stu-id="58d7f-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="58d7f-150">**.NET-Servercode in Startup.cs für die Verringerung der Standardnachrichtenpuffergröße**</span><span class="sxs-lookup"><span data-stu-id="58d7f-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="58d7f-151">**IIS-Konfigurationseinstellungen**</span><span class="sxs-lookup"><span data-stu-id="58d7f-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="58d7f-152">**Max. gleichzeitige Anforderungen pro Anwendung:** Wenn Sie die Anzahl der gleichzeitigen IIS-Anforderungen erhöhen, werden die Fürstand der Serverressourcen für die Zustellung von Anforderungen erhöht.</span><span class="sxs-lookup"><span data-stu-id="58d7f-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="58d7f-153">Der Standardwert ist 5000; Um diese Einstellung zu erhöhen, führen Sie die folgenden Befehle in einer erhöhten Eingabeaufforderung aus:</span><span class="sxs-lookup"><span data-stu-id="58d7f-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="58d7f-154">**ApplicationPool QueueLength**: Dies ist die maximale Anzahl von Anforderungen, die Http.sys für den Anwendungspool in die Warteschlange stellt.</span><span class="sxs-lookup"><span data-stu-id="58d7f-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="58d7f-155">Wenn die Warteschlange voll ist, erhalten neue Anforderungen eine Antwort 503 "Service Nicht verfügbar".</span><span class="sxs-lookup"><span data-stu-id="58d7f-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="58d7f-156">Der Standardwert lautet „1000“.</span><span class="sxs-lookup"><span data-stu-id="58d7f-156">The default value is 1000.</span></span>

    <span data-ttu-id="58d7f-157">Durch das Verkürzen der Warteschlangenlänge für den Arbeitsprozess im Anwendungspool, in dem Ihre Anwendung gehostet wird, werden Speicherressourcen geschont.</span><span class="sxs-lookup"><span data-stu-id="58d7f-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="58d7f-158">Weitere Informationen finden Sie unter [Verwalten, Optimieren und Konfigurieren von Anwendungspools](https://technet.microsoft.com/library/cc745955.aspx).</span><span class="sxs-lookup"><span data-stu-id="58d7f-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="58d7f-159">**ASP.NET Konfigurationseinstellungen**</span><span class="sxs-lookup"><span data-stu-id="58d7f-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="58d7f-160">Dieser Abschnitt enthält Konfigurationseinstellungen, die `aspnet.config` in der Datei festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="58d7f-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="58d7f-161">Diese Datei befindet sich je nach Plattform an einem von zwei Speicherorten:</span><span class="sxs-lookup"><span data-stu-id="58d7f-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="58d7f-162">ASP.NET Einstellungen, die die SignalR-Leistung verbessern können, umfassen die folgenden:</span><span class="sxs-lookup"><span data-stu-id="58d7f-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="58d7f-163">**Maximale anzahlstelle gleichzeitige Anforderungen pro CPU:** Wenn Sie diese Einstellung erhöhen, können Leistungsengpässe verringert werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="58d7f-164">Um diese Einstellung zu erhöhen, fügen `aspnet.config` Sie der Datei die folgende Konfigurationseinstellung hinzu:</span><span class="sxs-lookup"><span data-stu-id="58d7f-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="58d7f-165">**Anforderungswarteschlangenlimit**: Wenn die Gesamtzahl `maxConcurrentRequestsPerCPU` der Verbindungen die Einstellung überschreitet, beginnt ASP.NET mit der Drosselung von Anforderungen mithilfe einer Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="58d7f-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="58d7f-166">Um die Größe der Warteschlange zu `requestQueueLimit` erhöhen, können Sie die Einstellung erhöhen.</span><span class="sxs-lookup"><span data-stu-id="58d7f-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="58d7f-167">Fügen Sie dazu die folgende Konfigurationseinstellung `processModel` `config/machine.config` zum Knoten `aspnet.config`in hinzu (anstelle von):</span><span class="sxs-lookup"><span data-stu-id="58d7f-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="58d7f-168">Problembehandlung bei Leistungsproblemen</span><span class="sxs-lookup"><span data-stu-id="58d7f-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="58d7f-169">In diesem Abschnitt werden Möglichkeiten beschrieben, wie Sie Leistungsengpässe in Ihrer Anwendung ermitteln können.</span><span class="sxs-lookup"><span data-stu-id="58d7f-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="58d7f-170">Überprüfen, ob WebSocket verwendet wird</span><span class="sxs-lookup"><span data-stu-id="58d7f-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="58d7f-171">Während SignalR eine Vielzahl von Transporten für die Kommunikation zwischen Client und Server verwenden kann, bietet WebSocket einen erheblichen Leistungsvorteil und sollte verwendet werden, wenn der Client und der Server dies unterstützen.</span><span class="sxs-lookup"><span data-stu-id="58d7f-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="58d7f-172">Informationen dazu, ob Client und Server die Anforderungen für WebSocket erfüllen, finden Sie unter [Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="58d7f-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="58d7f-173">Um zu ermitteln, welcher Transport in Ihrer Anwendung verwendet wird, können Sie die Browserentwicklertools verwenden und die Protokolle untersuchen, um zu sehen, welcher Transport für die Verbindung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="58d7f-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="58d7f-174">Informationen zur Verwendung der Browserentwicklungstools in Internet Explorer und Chrome finden Sie unter [Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="58d7f-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="58d7f-175">Verwenden von SignalR-Leistungsindikatoren</span><span class="sxs-lookup"><span data-stu-id="58d7f-175">Using SignalR performance counters</span></span>

<span data-ttu-id="58d7f-176">In diesem Abschnitt wird beschrieben, wie Sie SignalR-Leistungsindikatoren aktivieren und verwenden, die `Microsoft.AspNet.SignalR.Utils` im Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="58d7f-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="58d7f-177">Installieren von signalr.exe</span><span class="sxs-lookup"><span data-stu-id="58d7f-177">Installing signalr.exe</span></span>

<span data-ttu-id="58d7f-178">Leistungsindikatoren können dem Server mithilfe eines Dienstprogramms namens SignalR.exe hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="58d7f-179">Gehen Sie folgendzu, um dieses Dienstprogramm zu installieren:</span><span class="sxs-lookup"><span data-stu-id="58d7f-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="58d7f-180">Wählen Sie in Visual Studio **Tools** > **NuGet Package Manager** > **Verwalten von NuGet-Paketen für die Lösung** aus.</span><span class="sxs-lookup"><span data-stu-id="58d7f-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="58d7f-181">Suchen Sie nach **signalr.utils**, und wählen Sie Installieren aus.</span><span class="sxs-lookup"><span data-stu-id="58d7f-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="58d7f-182">Akzeptieren Sie den Lizenzvertrag, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="58d7f-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="58d7f-183">SignalR.exe wird auf `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`installiert.</span><span class="sxs-lookup"><span data-stu-id="58d7f-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="58d7f-184">Installieren von Leistungsindikatoren mit SignalR.exe</span><span class="sxs-lookup"><span data-stu-id="58d7f-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="58d7f-185">Um SignalR-Leistungsindikatoren zu installieren, führen Sie SignalR.exe in einer erhöhten Eingabeaufforderung mit dem folgenden Parameter aus:</span><span class="sxs-lookup"><span data-stu-id="58d7f-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="58d7f-186">Um SignalR-Leistungsindikatoren zu entfernen, führen Sie SignalR.exe in einer erhöhten Eingabeaufforderung mit dem folgenden Parameter aus:</span><span class="sxs-lookup"><span data-stu-id="58d7f-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="58d7f-187">SignalR-Leistungsindikatoren</span><span class="sxs-lookup"><span data-stu-id="58d7f-187">SignalR Performance counters</span></span>

<span data-ttu-id="58d7f-188">Das Dienstprogrammpaket installiert die folgenden Leistungsindikatoren.</span><span class="sxs-lookup"><span data-stu-id="58d7f-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="58d7f-189">Die Leistungsindikatoren "Gesamt" messen die Anzahl der Ereignisse seit dem letzten Anwendungspool oder Serverneustart.</span><span class="sxs-lookup"><span data-stu-id="58d7f-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="58d7f-190">**Verbindungsmetriken**</span><span class="sxs-lookup"><span data-stu-id="58d7f-190">**Connection metrics**</span></span>

<span data-ttu-id="58d7f-191">Die folgenden Metriken messen die auftretenden Ereignisse der Verbindungslebensdauer.</span><span class="sxs-lookup"><span data-stu-id="58d7f-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="58d7f-192">Weitere Informationen finden Sie [unter Grundlegendes zum Verstehen und Behandeln von Verbindungsereignissen](../guide-to-the-api/handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="58d7f-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="58d7f-193">**Verbindungen verbunden**</span><span class="sxs-lookup"><span data-stu-id="58d7f-193">**Connections Connected**</span></span>
- <span data-ttu-id="58d7f-194">**Verbindungen wieder verbunden**</span><span class="sxs-lookup"><span data-stu-id="58d7f-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="58d7f-195">**Verbindungen getrennt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="58d7f-196">**Verbindungen Strom**</span><span class="sxs-lookup"><span data-stu-id="58d7f-196">**Connections Current**</span></span>

<span data-ttu-id="58d7f-197">**Nachrichtenmetriken**</span><span class="sxs-lookup"><span data-stu-id="58d7f-197">**Message metrics**</span></span>

<span data-ttu-id="58d7f-198">Die folgenden Metriken messen den von SignalR generierten Nachrichtenverkehr.</span><span class="sxs-lookup"><span data-stu-id="58d7f-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="58d7f-199">**Empfangene Verbindungsmeldungen Insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="58d7f-200">**Verbindungsmeldungen insgesamt gesendet**</span><span class="sxs-lookup"><span data-stu-id="58d7f-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="58d7f-201">**Empfangene Verbindungsnachrichten/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="58d7f-202">**Gesendete Verbindungsnachrichten/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="58d7f-203">**Nachrichtenbusmetriken**</span><span class="sxs-lookup"><span data-stu-id="58d7f-203">**Message bus metrics**</span></span>

<span data-ttu-id="58d7f-204">Die folgenden Metriken messen den Datenverkehr über den internen SignalR-Nachrichtenbus, die Warteschlange, in der alle eingehenden und ausgehenden SignalR-Nachrichten platziert werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="58d7f-205">Eine Nachricht wird **veröffentlicht,** wenn sie gesendet oder gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="58d7f-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="58d7f-206">Ein **Abonnent** in diesem Kontext ist ein Abonnement für den Nachrichtenbus. Dies sollte der Anzahl der Clients plus dem Server selbst entsprechen.</span><span class="sxs-lookup"><span data-stu-id="58d7f-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="58d7f-207">Eine **zugewiesene Arbeitskraft** ist eine Komponente, die Daten an aktive Verbindungen sendet. Ein **beschäftigter Worker** sendet aktiv eine Nachricht.</span><span class="sxs-lookup"><span data-stu-id="58d7f-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="58d7f-208">**Nachricht Bus Nachrichten empfangen Insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="58d7f-209">**Empfangene Nachrichten nachrichten/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="58d7f-210">**Nachricht Bus-Nachrichten veröffentlicht Insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="58d7f-211">**Nachricht Bus Nachrichten veröffentlicht/Sek**</span><span class="sxs-lookup"><span data-stu-id="58d7f-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="58d7f-212">**Nachricht Busabonnenten Aktuell**</span><span class="sxs-lookup"><span data-stu-id="58d7f-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="58d7f-213">**Nachricht Busabonnenten Insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="58d7f-214">**Nachricht Busabonnenten/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="58d7f-215">**Message Bus Allocated Workers**</span><span class="sxs-lookup"><span data-stu-id="58d7f-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="58d7f-216">**Nachricht Bus Beschäftigte Arbeiter**</span><span class="sxs-lookup"><span data-stu-id="58d7f-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="58d7f-217">**Message Bus Themen Aktuell**</span><span class="sxs-lookup"><span data-stu-id="58d7f-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="58d7f-218">**Fehlermetriken**</span><span class="sxs-lookup"><span data-stu-id="58d7f-218">**Error metrics**</span></span>

<span data-ttu-id="58d7f-219">Die folgenden Metriken messen Fehler, die durch den SignalR-Nachrichtenverkehr generiert wurden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="58d7f-220">**Hubauflösungsfehler** treten auf, wenn eine Hub- oder Hubmethode nicht aufgelöst werden kann.</span><span class="sxs-lookup"><span data-stu-id="58d7f-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="58d7f-221">**Hubaufruffehler** sind Ausnahmen, die beim Aufrufen einer Hubmethode ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="58d7f-222">**Transportfehler** sind Verbindungsfehler, die während einer HTTP-Anforderung oder -Antwort ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="58d7f-223">**Fehler: Alle insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-223">**Errors: All Total**</span></span>
- <span data-ttu-id="58d7f-224">**Fehler: Alle/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="58d7f-225">**Fehler: Hub-Auflösung insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="58d7f-226">**Fehler: Hub-Auflösung/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="58d7f-227">**Fehler: Hub-Aufruf insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="58d7f-228">**Fehler: Hub-Aufruf/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="58d7f-229">**Fehler: Transport Summe**</span><span class="sxs-lookup"><span data-stu-id="58d7f-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="58d7f-230">**Fehler: Transport/Sec**</span><span class="sxs-lookup"><span data-stu-id="58d7f-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="58d7f-231">**Scaleout-Metriken**</span><span class="sxs-lookup"><span data-stu-id="58d7f-231">**Scaleout metrics**</span></span>

<span data-ttu-id="58d7f-232">Die folgenden Metriken messen Datenverkehr und Fehler, die vom Scaleoutanbieter generiert werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="58d7f-233">Ein **Stream** ist in diesem Kontext eine Skalierungseinheit, die vom Scaleout-Anbieter verwendet wird. Dies ist eine Tabelle, wenn SQL Server verwendet wird, ein Thema, wenn Service Bus verwendet wird, und ein Abonnement, wenn Redis verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="58d7f-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="58d7f-234">Jeder Stream stellt geordnete Lese- und Schreibvorgänge sicher. Ein einzelner Stream ist ein potenzieller Skalierungsengpass, sodass die Anzahl der Streams erhöht werden kann, um diesen Engpass zu verringern.</span><span class="sxs-lookup"><span data-stu-id="58d7f-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="58d7f-235">Wenn mehrere Streams verwendet werden, verteilt SignalR automatisch (Shard-)Nachrichten über diese Streams in einer Weise, die sicherstellt, dass Nachrichten, die von einer bestimmten Verbindung gesendet werden, in Ordnung sind.</span><span class="sxs-lookup"><span data-stu-id="58d7f-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="58d7f-236">Die [Einstellung MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) steuert die Länge der von SignalR verwalteten Skalierungssssendewarteschlange.</span><span class="sxs-lookup"><span data-stu-id="58d7f-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="58d7f-237">Wenn Sie ihn auf einen Wert größer als 0 setzen, werden alle Nachrichten in einer Sendewarteschlange platziert, die nacheinander an die konfigurierte Messaging-Backplane gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="58d7f-238">Wenn die Größe der Warteschlange über die konfigurierte Länge geht, schlagen nachfolgende Aufrufe zum Senden sofort mit einer [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) fehl, bis die Anzahl der Nachrichten in der Warteschlange erneut kleiner als die Einstellung ist.</span><span class="sxs-lookup"><span data-stu-id="58d7f-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="58d7f-239">Die Warteschlange ist standardmäßig deaktiviert, da die implementierten Backplanes im Allgemeinen über eine eigene Warteschlange oder Flusssteuerung verfügen.</span><span class="sxs-lookup"><span data-stu-id="58d7f-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="58d7f-240">Im Fall von SQL Server begrenzt das Verbindungspooling effektiv die Anzahl der Sendezeiten, die zu einem beliebigen Zeitpunkt ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="58d7f-241">Standardmäßig wird nur ein Stream für SQL Server und Redis verwendet, fünf Streams werden für Service Bus verwendet, und die Warteschlange ist deaktiviert, aber diese Einstellungen können durch Die Konfiguration auf SQL Server und Service Bus geändert werden:</span><span class="sxs-lookup"><span data-stu-id="58d7f-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="58d7f-242">**.NET ServerCode zum Konfigurieren der Tabellenanzahl und Warteschlangenlänge für SQL Server-Backplane**</span><span class="sxs-lookup"><span data-stu-id="58d7f-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="58d7f-243">**.NET ServerCode zum Konfigurieren der Themenanzahl und Warteschlangenlänge für Die Service Bus-Backplane**</span><span class="sxs-lookup"><span data-stu-id="58d7f-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="58d7f-244">Ein Pufferstream ist ein **Stream,** der in einen fehlerhaften Zustand eingetreten ist. Wenn sich der Stream im fehlerhaften Zustand befindet, schlagen alle nachrichten, die an die Backplane gesendet werden, sofort fehl, bis der Stream keinen Fehler mehr macht.</span><span class="sxs-lookup"><span data-stu-id="58d7f-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="58d7f-245">Die Länge der **Sendewarteschlange** ist die Anzahl der Nachrichten, die gesendet, aber noch nicht gesendet wurden.</span><span class="sxs-lookup"><span data-stu-id="58d7f-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="58d7f-246">**Scaleout Message Bus Empfangene/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="58d7f-247">**Scaleout-Streams insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="58d7f-248">**Scaleout Streams geöffnet**</span><span class="sxs-lookup"><span data-stu-id="58d7f-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="58d7f-249">**Scaleout Streams Buffering**</span><span class="sxs-lookup"><span data-stu-id="58d7f-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="58d7f-250">**Scaleout-Fehler insgesamt**</span><span class="sxs-lookup"><span data-stu-id="58d7f-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="58d7f-251">**Scaleout-Fehler/Sek.**</span><span class="sxs-lookup"><span data-stu-id="58d7f-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="58d7f-252">**Scaleout-Sendewarteschlangenlänge**</span><span class="sxs-lookup"><span data-stu-id="58d7f-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="58d7f-253">Weitere Informationen zu den Messpunkten dieser Leistungsindikatoren finden Sie unter [SignalR Scaleout mit Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="58d7f-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="58d7f-254">Verwenden anderer Leistungsindikatoren</span><span class="sxs-lookup"><span data-stu-id="58d7f-254">Using other performance counters</span></span>

<span data-ttu-id="58d7f-255">Die folgenden Leistungsindikatoren können auch bei der Überwachung der Leistung Ihrer Anwendung nützlich sein.</span><span class="sxs-lookup"><span data-stu-id="58d7f-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="58d7f-256">**Memory**</span><span class="sxs-lookup"><span data-stu-id="58d7f-256">**Memory**</span></span>

- <span data-ttu-id="58d7f-257">.NET CLR-Speicher\\in allen Heaps (für w3wp)</span><span class="sxs-lookup"><span data-stu-id="58d7f-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="58d7f-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="58d7f-258">**ASP.NET**</span></span>

- <span data-ttu-id="58d7f-259">ASP.NET-Anforderungen aktuell</span><span class="sxs-lookup"><span data-stu-id="58d7f-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="58d7f-260">ASP.NET-Warteschlange</span><span class="sxs-lookup"><span data-stu-id="58d7f-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="58d7f-261">ASP.NET-Abgelehnt</span><span class="sxs-lookup"><span data-stu-id="58d7f-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="58d7f-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="58d7f-262">**CPU**</span></span>

- <span data-ttu-id="58d7f-263">Prozessorinformationen,Prozessorzeit</span><span class="sxs-lookup"><span data-stu-id="58d7f-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="58d7f-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="58d7f-264">**TCP/IP**</span></span>

- <span data-ttu-id="58d7f-265">TCPv6/Verbindungen eingerichtet</span><span class="sxs-lookup"><span data-stu-id="58d7f-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="58d7f-266">TCPv4/Verbindungen eingerichtet</span><span class="sxs-lookup"><span data-stu-id="58d7f-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="58d7f-267">**Webdienst**</span><span class="sxs-lookup"><span data-stu-id="58d7f-267">**Web Service**</span></span>

- <span data-ttu-id="58d7f-268">Webdienst- und aktuelle Verbindungen</span><span class="sxs-lookup"><span data-stu-id="58d7f-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="58d7f-269">Webdienst-Maximale Verbindungen</span><span class="sxs-lookup"><span data-stu-id="58d7f-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="58d7f-270">**Threading**</span><span class="sxs-lookup"><span data-stu-id="58d7f-270">**Threading**</span></span>

- <span data-ttu-id="58d7f-271">.NET CLR-Sperren\\und -Threads der aktuellen logischen Threads</span><span class="sxs-lookup"><span data-stu-id="58d7f-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="58d7f-272">.NET CLR-Sperren\\und -Threads von aktuellen physikalischen Threads</span><span class="sxs-lookup"><span data-stu-id="58d7f-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="58d7f-273">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="58d7f-273">Other Resources</span></span>

<span data-ttu-id="58d7f-274">Weitere Informationen zur ASP.NET Leistungsüberwachung und -optimierung finden Sie in den folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="58d7f-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="58d7f-275">[ASP.NET Performance Overview (Die Leistung von ASP.NET im Überblick)](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="58d7f-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="58d7f-276">ASP.NET Threadverwendung auf IIS 7.5, IIS 7.0 und IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="58d7f-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="58d7f-277">&lt;applicationPool&gt; Element (Webeinstellungen)</span><span class="sxs-lookup"><span data-stu-id="58d7f-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
