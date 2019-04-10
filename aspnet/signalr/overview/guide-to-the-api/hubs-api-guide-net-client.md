---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR-für-API-Hubs - Client für .NET (c#) | Microsoft-Dokumentation
author: bradygaster
description: Dieses Dokument enthält eine Einführung zur Verwendung von den Hubs-API für den SignalR .NET-Client zu erhalten, wie z. B. Windows Store (WinRT), WPF, Silverlight und Nachteile Version 2...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 473c8dd14d639fb9f4ff9e11a4c3ffa2b1a3a81e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59396030"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="c58ba-103">ASP.NET SignalR-für-API-Hubs - Client für .NET (c#)</span><span class="sxs-lookup"><span data-stu-id="c58ba-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>


[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c58ba-104">Dieses Dokument enthält eine Einführung zur Verwendung von den Hubs-API für den SignalR .NET-Client zu erhalten, wie z. B. Windows Store (WinRT), WPF, Silverlight und konsolenanwendungen Version 2.</span><span class="sxs-lookup"><span data-stu-id="c58ba-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="c58ba-105">Der SignalR-Hubs-API können Sie die Remoteprozeduraufrufe (RPCs) von einem Server verbundene Clients und von den Clients an den Server vornehmen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="c58ba-106">Im Server-Code Sie Methoden definieren, die von Clients aufgerufen werden können, und rufen Sie Methoden, die auf dem Client ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="c58ba-107">Im Clientcode Sie Methoden definieren, die vom Server aufgerufen werden können, und rufen Sie Methoden, die auf dem Server ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="c58ba-108">SignalR ist für alle Client-zu-Server sich für Sie übernimmt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="c58ba-109">SignalR bietet außerdem eine Low-Level-API wird aufgerufen, dauerhafte Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="c58ba-110">Eine Einführung in die SignalR-Hubs und dauerhafte Verbindungen oder für ein Lernprogramm, das zeigt, wie Sie eine vollständige SignalR-Anwendung erstellen, finden Sie unter [SignalR - erste Schritte](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="c58ba-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c58ba-111">In diesem Thema verwendeten Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="c58ba-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c58ba-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c58ba-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="c58ba-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c58ba-113">.NET 4.5</span></span>
> - <span data-ttu-id="c58ba-114">SignalR-Version 2</span><span class="sxs-lookup"><span data-stu-id="c58ba-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c58ba-115">Vorherige Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="c58ba-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c58ba-116">Weitere Informationen zu früheren Versionen von SignalR, finden Sie unter [ältere Versionen von SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="c58ba-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c58ba-117">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="c58ba-117">Questions and comments</span></span>
>
> <span data-ttu-id="c58ba-118">Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können.</span><span class="sxs-lookup"><span data-stu-id="c58ba-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c58ba-119">Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="c58ba-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c58ba-120">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c58ba-120">Overview</span></span>

<span data-ttu-id="c58ba-121">Dieses Dokument enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="c58ba-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="c58ba-122">Client-Setup</span><span class="sxs-lookup"><span data-stu-id="c58ba-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="c58ba-123">Gewusst wie: Herstellen einer Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="c58ba-124">Domänenübergreifende Verbindungen von Silverlight-clients</span><span class="sxs-lookup"><span data-stu-id="c58ba-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="c58ba-125">Gewusst wie: Konfigurieren der Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="c58ba-126">Die maximale Anzahl gleichzeitiger Verbindungen in WPF-Clients festlegen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="c58ba-127">Gewusst wie: Angeben von Abfragezeichenfolgen-Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="c58ba-128">Das Angeben der Transportmethode</span><span class="sxs-lookup"><span data-stu-id="c58ba-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="c58ba-129">Gewusst wie: Angeben von HTTP-Header</span><span class="sxs-lookup"><span data-stu-id="c58ba-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="c58ba-130">Gewusst wie: Geben Sie Clientzertifikate</span><span class="sxs-lookup"><span data-stu-id="c58ba-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="c58ba-131">Vorgehensweise: Erstellen Sie die Hubproxy-Klasse</span><span class="sxs-lookup"><span data-stu-id="c58ba-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="c58ba-132">Wie Sie Methoden auf dem Client zu definieren, die der Server aufgerufen werden können</span><span class="sxs-lookup"><span data-stu-id="c58ba-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="c58ba-133">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="c58ba-134">Methoden mit Parametern, Parametertypen angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="c58ba-135">Methoden mit Parametern, dynamische Objekte für die Parameter angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="c58ba-136">Vorgehensweise beim Entfernen eines Handlers</span><span class="sxs-lookup"><span data-stu-id="c58ba-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="c58ba-137">Gewusst wie: Servermethoden vom Client aufrufen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="c58ba-138">Gewusst wie: Behandeln der Objektlebensdauer-Ereignisse der Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="c58ba-139">Gewusst wie: Behandeln von Fehlern</span><span class="sxs-lookup"><span data-stu-id="c58ba-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="c58ba-140">Gewusst wie: Aktivieren der clientseitigen Protokollierung</span><span class="sxs-lookup"><span data-stu-id="c58ba-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="c58ba-141">WPF, Silverlight und Konsolenanwendung Codebeispiele für Clientmethoden, die der Server aufgerufen werden können</span><span class="sxs-lookup"><span data-stu-id="c58ba-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="c58ba-142">Ein .NET Client Beispielprojekte finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="c58ba-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="c58ba-143">[Gustavo-Armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) auf "github.com" (app-Beispiele in WinRT, Silverlight-Konsole).</span><span class="sxs-lookup"><span data-stu-id="c58ba-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="c58ba-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) auf GitHub.com (WPF-Beispiel).</span><span class="sxs-lookup"><span data-stu-id="c58ba-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="c58ba-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) auf "github.com" (Console app-Beispiel).</span><span class="sxs-lookup"><span data-stu-id="c58ba-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="c58ba-146">Dokumentation zum Programmieren des Servers oder Clients mit JavaScript finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="c58ba-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="c58ba-147">SignalR-Hubs-API-Guide - Server</span><span class="sxs-lookup"><span data-stu-id="c58ba-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="c58ba-148">SignalR-Hubs-API-Leitfaden – JavaScript-Client</span><span class="sxs-lookup"><span data-stu-id="c58ba-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="c58ba-149">Links zu Themen,-API-Referenz sind, .NET 4.5-Version der API.</span><span class="sxs-lookup"><span data-stu-id="c58ba-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="c58ba-150">Wenn Sie .NET 4 verwenden, finden Sie unter [.NET 4-Version der API-Themen](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="c58ba-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="c58ba-151">Client-setup</span><span class="sxs-lookup"><span data-stu-id="c58ba-151">Client setup</span></span>

<span data-ttu-id="c58ba-152">Installieren Sie die [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet-Paket (nicht die [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) Paket).</span><span class="sxs-lookup"><span data-stu-id="c58ba-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="c58ba-153">Dieses Paket unterstützt WinRT, Silverlight, WPF, Konsolenanwendung und Windows Phone-Clients, die für .NET 4 und .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="c58ba-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="c58ba-154">Ist die Version von SignalR, die Sie auf dem Client haben sich von der Version, die Sie auf dem Server haben, ist SignalR häufig auf den Unterschied anpassen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="c58ba-155">Ein Server mit SignalR 2-Version unterstützt z. B. Clients, die 1.1.x installiert haben, sowie Clients, die Version 2 installiert haben.</span><span class="sxs-lookup"><span data-stu-id="c58ba-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="c58ba-156">Wenn der Unterschied zwischen der Version auf dem Server und die Version auf dem Client zu groß ist oder SignalR löst aus, wenn der Client neuer als der Server ist, eine `InvalidOperationException` Ausnahme aus, wenn der Client versucht, eine Verbindung herzustellen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="c58ba-157">Die Fehlermeldung lautet "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span><span class="sxs-lookup"><span data-stu-id="c58ba-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="c58ba-158">Gewusst wie: Herstellen einer Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-158">How to establish a connection</span></span>

<span data-ttu-id="c58ba-159">Bevor Sie eine Verbindung herstellen können, müssen Sie erstellen eine `HubConnection` Objekt, und erstellen Sie einen Proxy.</span><span class="sxs-lookup"><span data-stu-id="c58ba-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="c58ba-160">Rufen Sie zum Herstellen einer Verbindung, die `Start` Methode für die `HubConnection` Objekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="c58ba-161">JavaScript-Clients müssen Sie mindestens einen Ereignishandler vor dem Aufruf registriert die `Start` Methode zum Herstellen der Verbindung.</span><span class="sxs-lookup"><span data-stu-id="c58ba-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="c58ba-162">Dies ist nicht für .NET-Clients erforderlich.</span><span class="sxs-lookup"><span data-stu-id="c58ba-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="c58ba-163">Für JavaScript-Clients, erstellt des generierte Proxycodes-Proxys für alle Hubs, die vorhanden sind automatisch auf dem Server, und Registrieren eines Handlers ist, geben Sie die Hubs an der Client verwenden will.</span><span class="sxs-lookup"><span data-stu-id="c58ba-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="c58ba-164">Aber für einen .NET Client Hub Proxys manuell erstellt, damit SignalR wird davon ausgegangen, dass Sie eine Hub-Instanz verwendet werden, die Sie über einen Proxy für erstellen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="c58ba-165">Der Beispielcode verwendet die Standardeinstellung "/ Signalr" die URL für die Verbindung mit Ihrem SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="c58ba-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="c58ba-166">WPF-Clientcode für die Methode wird vom Server ohne Parameter aufgerufen. [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="c58ba-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="c58ba-167">Wenn die `Start` Methode asynchron ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c58ba-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="c58ba-168">Um sicherzustellen, dass es sich bei nachfolgenden Codezeilen nicht erst ausführen, nachdem die Verbindung hergestellt ist, verwenden Sie `await` in einer asynchronen Methode von ASP.NET 4.5 oder `.Wait()` in eine synchrone Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="c58ba-169">Verwenden Sie keine `.Wait()` in einem WinRT-Client.</span><span class="sxs-lookup"><span data-stu-id="c58ba-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="c58ba-170">Domänenübergreifende Verbindungen von Silverlight-clients</span><span class="sxs-lookup"><span data-stu-id="c58ba-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="c58ba-171">Informationen dazu, wie Sie die domänenübergreifende Verbindungen von Silverlight-Clients zu aktivieren, finden Sie unter [vornehmen einer Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="c58ba-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="c58ba-172">Gewusst wie: Konfigurieren der Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-172">How to configure the connection</span></span>

<span data-ttu-id="c58ba-173">Bevor Sie eine Verbindung herstellen, können Sie eine der folgenden Optionen angeben:</span><span class="sxs-lookup"><span data-stu-id="c58ba-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="c58ba-174">Gleichzeitige Verbindungen beschränken.</span><span class="sxs-lookup"><span data-stu-id="c58ba-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="c58ba-175">Abfragezeichenfolgenparameter.</span><span class="sxs-lookup"><span data-stu-id="c58ba-175">Query string parameters.</span></span>
- <span data-ttu-id="c58ba-176">Die Transportmethode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-176">The transport method.</span></span>
- <span data-ttu-id="c58ba-177">HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="c58ba-177">HTTP headers.</span></span>
- <span data-ttu-id="c58ba-178">Clientzertifikate.</span><span class="sxs-lookup"><span data-stu-id="c58ba-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="c58ba-179">Die maximale Anzahl gleichzeitiger Verbindungen in WPF-Clients festlegen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="c58ba-180">In WPF-Clients müssen Sie möglicherweise die maximale Anzahl gleichzeitiger Verbindungen vom Standardwert 2 erhöhen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="c58ba-181">Der empfohlene Wert ist 10.</span><span class="sxs-lookup"><span data-stu-id="c58ba-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="c58ba-182">Weitere Informationen finden Sie unter [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="c58ba-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="c58ba-183">Gewusst wie: Angeben von Abfragezeichenfolgen-Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-183">How to specify query string parameters</span></span>

<span data-ttu-id="c58ba-184">Wenn Sie möchten die Daten an den Server gesendet, wenn der Client eine Verbindung herstellt, können Sie Abfragezeichenfolgen-Parameter an das Verbindungsobjekt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="c58ba-185">Das folgende Beispiel zeigt, wie Sie einen Abfragezeichenfolgen-Parameter in Client-Code festlegen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="c58ba-186">Das folgende Beispiel zeigt, wie Sie einen Abfragezeichenfolgen-Parameter im Servercode zu lesen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="c58ba-187">Das Angeben der Transportmethode</span><span class="sxs-lookup"><span data-stu-id="c58ba-187">How to specify the transport method</span></span>

<span data-ttu-id="c58ba-188">Als Teil der Prozess der verbindungsherstellung verhandelt ein SignalR-Client normalerweise mit dem Server um den besten Transport zu bestimmen, der unterstützt wird, indem sowohl Server-als auch.</span><span class="sxs-lookup"><span data-stu-id="c58ba-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="c58ba-189">Wenn Sie bereits wissen, dass Transport Sie verwenden möchten, können Sie dieser Aushandlungsprozess umgehen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="c58ba-190">Um die Transportmethode anzugeben, übergeben Sie einen Transport-Objekt an die Start-Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="c58ba-191">Das folgende Beispiel zeigt, wie die Transportmethode im Clientcode angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="c58ba-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="c58ba-192">Die [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) Namespace enthält die folgenden Klassen, die Sie verwenden können, an den Transport.</span><span class="sxs-lookup"><span data-stu-id="c58ba-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- [<span data-ttu-id="c58ba-193">LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="c58ba-193">LongPollingTransport</span></span>](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [<span data-ttu-id="c58ba-194">ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="c58ba-194">ServerSentEventsTransport</span></span>](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- <span data-ttu-id="c58ba-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (nur verfügbar, wenn sowohl Server-als auch .NET 4.5 verwenden.)</span><span class="sxs-lookup"><span data-stu-id="c58ba-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="c58ba-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (wählt automatisch den besten Transport, die von dem Client und dem Server unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="c58ba-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="c58ba-197">Dies ist der Standardtransport.</span><span class="sxs-lookup"><span data-stu-id="c58ba-197">This is the default transport.</span></span> <span data-ttu-id="c58ba-198">Übergeben dies in der `Start` Methode hat dieselbe Wirkung wie das alles nicht übergeben.)</span><span class="sxs-lookup"><span data-stu-id="c58ba-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="c58ba-199">Der Transport ForeverFrame ist nicht in dieser Liste enthalten, da er nur von Browsern verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c58ba-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="c58ba-200">Informationen zum Überprüfen der Transportmethode in Server-Code finden Sie unter [für die ASP.NET SignalR-Hubs-API - Server – zum Abrufen von Informationen über den Client aus der Kontexteigenschaft](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="c58ba-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="c58ba-201">Weitere Informationen zu Transporten und Fallbacks, finden Sie unter [Einführung zu SignalR - Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="c58ba-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="c58ba-202">Gewusst wie: Angeben von HTTP-Header</span><span class="sxs-lookup"><span data-stu-id="c58ba-202">How to specify HTTP headers</span></span>

<span data-ttu-id="c58ba-203">Um HTTP-Header festzulegen, verwenden die `Headers` Eigenschaft für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="c58ba-204">Das folgende Beispiel zeigt, wie Sie einen HTTP-Header hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="c58ba-205">Gewusst wie: Geben Sie Clientzertifikate</span><span class="sxs-lookup"><span data-stu-id="c58ba-205">How to specify client certificates</span></span>

<span data-ttu-id="c58ba-206">Verwenden Sie zum Hinzufügen von Clientzertifikaten die `AddClientCertificate` Methode für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="c58ba-207">Vorgehensweise: Erstellen Sie die Hubproxy-Klasse</span><span class="sxs-lookup"><span data-stu-id="c58ba-207">How to create the Hub proxy</span></span>

<span data-ttu-id="c58ba-208">Um Methoden auf dem Client definieren, die ein Hub vom Server aufrufen können, und zum Aufrufen von Methoden für einen Hub auf dem Server, erstellen Sie einen Proxy für den Hub durch Aufrufen von `CreateHubProxy` für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="c58ba-209">Die Zeichenfolge übergebenen `CreateHubProxy` ist der Name der Hub-Klasse, oder den Namen trägt die `HubName` Attribut, wenn auf dem Server verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="c58ba-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="c58ba-210">Die namenszuordnung wird Groß-/Kleinschreibung.</span><span class="sxs-lookup"><span data-stu-id="c58ba-210">Name matching is case-insensitive.</span></span>

**<span data-ttu-id="c58ba-211">Hub-Klasse auf server</span><span class="sxs-lookup"><span data-stu-id="c58ba-211">Hub class on server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**<span data-ttu-id="c58ba-212">Erstellen des Clientproxys für Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="c58ba-212">Create client proxy for the Hub class</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="c58ba-213">Wenn Sie ergänzen, um Ihre hubklasse mit einem `HubName` -Attributs festzulegen, verwenden Sie diesen Namen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

**<span data-ttu-id="c58ba-214">Hub-Klasse auf server</span><span class="sxs-lookup"><span data-stu-id="c58ba-214">Hub class on server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**<span data-ttu-id="c58ba-215">Erstellen des Clientproxys für Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="c58ba-215">Create client proxy for the Hub class</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="c58ba-216">Wenn Sie aufrufen `HubConnection.CreateHubProxy` mehrmals mit dem gleichen `hubName`, erhalten Sie dieselbe zwischengespeichert `IHubProxy` Objekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c58ba-217">Wie Sie Methoden auf dem Client zu definieren, die der Server aufgerufen werden können</span><span class="sxs-lookup"><span data-stu-id="c58ba-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="c58ba-218">Um eine Methode definieren, die der Server aufrufen können, verwenden Sie den Proxy des `On` Methode, um einen Ereignishandler zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="c58ba-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="c58ba-219">Methode-namenszuordnung wird Groß-/Kleinschreibung.</span><span class="sxs-lookup"><span data-stu-id="c58ba-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="c58ba-220">Z. B. `Clients.All.UpdateStockPrice` auf dem Server führt `updateStockPrice`, `updatestockprice`, oder `UpdateStockPrice` auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="c58ba-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="c58ba-221">Verschiedene Clientplattformen haben unterschiedliche Anforderungen an wie Sie den Code schreiben, die Benutzeroberfläche aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="c58ba-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="c58ba-222">Die dargestellten Beispiele gelten für WinRT (Windows Store-.NET)-Clients.</span><span class="sxs-lookup"><span data-stu-id="c58ba-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="c58ba-223">WPF, Silverlight und Beispiele für Konsole finden Sie unter [einem separaten Abschnitt weiter unten in diesem Thema](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="c58ba-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="c58ba-224">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-224">Methods without parameters</span></span>

<span data-ttu-id="c58ba-225">Wenn die Methode Sie verarbeiten nicht über Parameter verfügt, verwenden Sie die nicht generische Überladung von der `On` Methode:</span><span class="sxs-lookup"><span data-stu-id="c58ba-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

**<span data-ttu-id="c58ba-226">Clientmethode ohne Parameter aufrufen Servercode</span><span class="sxs-lookup"><span data-stu-id="c58ba-226">Server code calling client method without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**<span data-ttu-id="c58ba-227">WinRT-Clientcode für die Methode, die vom Server ohne Parameter aufgerufen ([finden Sie in WPF und Silverlight-Beispielen weiter unten in diesem Thema](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="c58ba-227">WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c58ba-228">Methoden mit Parametern, die Parametertypen angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="c58ba-229">Wenn die Methode, die Sie verarbeiten Parameter verfügt, geben Sie die Typen der Parameter als die generischen Typen von der `On` Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="c58ba-230">Es gibt generische Überladung von der `On` Methode, um Ihnen die Angabe von bis zu 8 Parameter (4 unter Windows Phone 7) zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="c58ba-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="c58ba-231">Im folgenden Beispiel wird ein Parameter gesendet, auf die `UpdateStockPrice` Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

**<span data-ttu-id="c58ba-232">Aufrufen der Methode mit einem Parameter Servercode</span><span class="sxs-lookup"><span data-stu-id="c58ba-232">Server code calling client method with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**<span data-ttu-id="c58ba-233">Die Stock-Klasse für den Parameter verwendet</span><span class="sxs-lookup"><span data-stu-id="c58ba-233">The Stock class used for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**<span data-ttu-id="c58ba-234">WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen ([finden Sie in WPF und Silverlight-Beispielen weiter unten in diesem Thema](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="c58ba-234">WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c58ba-235">Methoden mit Parametern, dynamische Objekte für die Parameter angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="c58ba-236">Als Alternative zum Angeben von Parametern als generische Typen, die von der `On` -Methode, Sie können Parameter angeben, als dynamische Objekte:</span><span class="sxs-lookup"><span data-stu-id="c58ba-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

**<span data-ttu-id="c58ba-237">Aufrufen der Methode mit einem Parameter Servercode</span><span class="sxs-lookup"><span data-stu-id="c58ba-237">Server code calling client method with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**<span data-ttu-id="c58ba-238">Die Stock-Klasse für den Parameter verwendet</span><span class="sxs-lookup"><span data-stu-id="c58ba-238">The Stock class used for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**<span data-ttu-id="c58ba-239">WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter, die ein dynamisches Objekt verwenden, für den Parameter aufgerufen ([finden Sie in WPF und Silverlight-Beispielen weiter unten in diesem Thema](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="c58ba-239">WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="c58ba-240">Vorgehensweise beim Entfernen eines Handlers</span><span class="sxs-lookup"><span data-stu-id="c58ba-240">How to remove a handler</span></span>

<span data-ttu-id="c58ba-241">Um einen Handler zu entfernen, rufen Sie die `Dispose` Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-241">To remove a handler, call its `Dispose` method.</span></span>

**<span data-ttu-id="c58ba-242">Clientcode für eine vom Server aufgerufene Methode</span><span class="sxs-lookup"><span data-stu-id="c58ba-242">Client code for a method called from server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**<span data-ttu-id="c58ba-243">Client-Code, um den Ereignishandler zu entfernen</span><span class="sxs-lookup"><span data-stu-id="c58ba-243">Client code to remove the handler</span></span>**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="c58ba-244">Gewusst wie: Servermethoden vom Client aufrufen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-244">How to call server methods from the client</span></span>

<span data-ttu-id="c58ba-245">Verwenden Sie zum Aufrufen einer Methode auf dem Server die `Invoke` Methode für die Hubproxy-Klasse.</span><span class="sxs-lookup"><span data-stu-id="c58ba-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="c58ba-246">Verfügt die Server-Methode keinen Wert zurückgibt, verwenden Sie die nicht generische Überladung von der `Invoke` Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

**<span data-ttu-id="c58ba-247">Servercode für eine Methode, die keinen zurückgibt Wert</span><span class="sxs-lookup"><span data-stu-id="c58ba-247">Server code for a method that has no return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**<span data-ttu-id="c58ba-248">Client-Code Aufrufen einer Methode, die keinen zurückgibt Wert</span><span class="sxs-lookup"><span data-stu-id="c58ba-248">Client code calling a method that has no return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="c58ba-249">Wenn die Server-Methode einen Rückgabewert verfügt, geben Sie den Rückgabetyp als den generischen Typ, der die `Invoke` Methode.</span><span class="sxs-lookup"><span data-stu-id="c58ba-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

**<span data-ttu-id="c58ba-250">Servercode für eine Methode, die hat einen Rückgabewert und nimmt einen Parameter des komplexen Typs</span><span class="sxs-lookup"><span data-stu-id="c58ba-250">Server code for a method that has a return value and takes a complex type parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**<span data-ttu-id="c58ba-251">Die Stock-Klasse, die für die Parameter und Rückgabewert verwendet</span><span class="sxs-lookup"><span data-stu-id="c58ba-251">The Stock class used for the parameter and return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**<span data-ttu-id="c58ba-252">Client-Code Aufrufen einer Methode, die einen Rückgabewert und nimmt einen Parameter des komplexen Typs, in einer ASP.NET 4.5-Async-Methode</span><span class="sxs-lookup"><span data-stu-id="c58ba-252">Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**<span data-ttu-id="c58ba-253">Aufrufen einer Methode, die einen Rückgabewert und eine synchrone Methode nimmt einen Parameter des komplexen Typs, der Client-code</span><span class="sxs-lookup"><span data-stu-id="c58ba-253">Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="c58ba-254">Die `Invoke` Methode asynchron ausgeführt wird, und gibt eine `Task` Objekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="c58ba-255">Wenn Sie keinen `await` oder `.Wait()`, die nächste Codezeile ausgeführt, bevor die Methode, die Sie aufrufen beendet wurde.</span><span class="sxs-lookup"><span data-stu-id="c58ba-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="c58ba-256">Gewusst wie: Behandeln der Objektlebensdauer-Ereignisse der Verbindung</span><span class="sxs-lookup"><span data-stu-id="c58ba-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="c58ba-257">SignalR bietet die folgenden Verbindung, die Objektlebensdauer-Ereignisse, die Sie behandeln können:</span><span class="sxs-lookup"><span data-stu-id="c58ba-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- `Received`<span data-ttu-id="c58ba-258">: Wird ausgelöst, wenn alle Daten für die Verbindung empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="c58ba-258">: Raised when any data is received on the connection.</span></span> <span data-ttu-id="c58ba-259">Stellt die empfangenen Daten bereit.</span><span class="sxs-lookup"><span data-stu-id="c58ba-259">Provides the received data.</span></span>
- `ConnectionSlow`<span data-ttu-id="c58ba-260">: Wird ausgelöst, wenn der Client eine Verbindung langsame ist oder häufig löschen erkennt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-260">: Raised when the client detects a slow or frequently dropping connection.</span></span>
- `Reconnecting`<span data-ttu-id="c58ba-261">: Wird ausgelöst, wenn des zugrunde liegenden Transports, erneut eine Verbindung herzustellen beginnt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-261">: Raised when the underlying transport begins reconnecting.</span></span>
- `Reconnected`<span data-ttu-id="c58ba-262">: Wird ausgelöst, wenn der zugrunde liegenden Transport die Verbindung wiederhergestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="c58ba-262">: Raised when the underlying transport has reconnected.</span></span>
- `StateChanged`<span data-ttu-id="c58ba-263">: Wird ausgelöst, wenn der Verbindungsstatus ändert.</span><span class="sxs-lookup"><span data-stu-id="c58ba-263">: Raised when the connection state changes.</span></span> <span data-ttu-id="c58ba-264">Enthält der alte Status und den neuen Zustand.</span><span class="sxs-lookup"><span data-stu-id="c58ba-264">Provides the old state and the new state.</span></span> <span data-ttu-id="c58ba-265">Informationen zur Verbindung finden Sie unter Statuswerte [ConnectionState-Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="c58ba-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- `Closed`<span data-ttu-id="c58ba-266">: Wird ausgelöst, wenn die Verbindung getrennt wurde.</span><span class="sxs-lookup"><span data-stu-id="c58ba-266">: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="c58ba-267">Beispielsweise sollten Sie Warnmeldungen für Fehler angezeigt, die nicht schwerwiegend sind, aber dazu führen, dass zeitweilige Verbindungsprobleme, wie die Langsamkeit oder häufige Löschen der Verbindung, behandeln die `ConnectionSlow` Ereignis.</span><span class="sxs-lookup"><span data-stu-id="c58ba-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="c58ba-268">Weitere Informationen finden Sie unter [verstehen und Behandeln von Ereignissen für Lebensdauer in SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="c58ba-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="c58ba-269">Gewusst wie: Behandeln von Fehlern</span><span class="sxs-lookup"><span data-stu-id="c58ba-269">How to handle errors</span></span>

<span data-ttu-id="c58ba-270">Wenn Sie detaillierte Fehlermeldungen auf dem Server nicht explizit aktivieren, enthält das Ausnahmeobjekt an, dem SignalR nach einem Fehler zurückgibt minimale Informationen über den Fehler an.</span><span class="sxs-lookup"><span data-stu-id="c58ba-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="c58ba-271">Beispielsweise wenn ein Aufruf von `newContosoChatMessage` ein Fehler auftritt, der die Fehlermeldung in das Fehlerobjekt enthält "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Senden detaillierte Fehlermeldungen für Clients in einer produktionsumgebung wird nicht empfohlen aus Sicherheitsgründen aber wenn Sie möchten detaillierte Fehlermeldungen für aktivieren Problembehandlung, verwenden Sie den folgenden Code auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="c58ba-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="c58ba-272">Zur Behandlung von Fehlern, die SignalR auslöst, können Sie hinzufügen, einen Handler für die `Error` Ereignis für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="c58ba-273">Zur Behandlung von Fehlern von Methodenaufrufen, umschließen Sie den Code in einem Try / Catch-Block.</span><span class="sxs-lookup"><span data-stu-id="c58ba-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="c58ba-274">Gewusst wie: Aktivieren der clientseitigen Protokollierung</span><span class="sxs-lookup"><span data-stu-id="c58ba-274">How to enable client-side logging</span></span>

<span data-ttu-id="c58ba-275">Um die clientseitige Protokollierung zu aktivieren, legen die `TraceLevel` und `TraceWriter` Eigenschaften für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="c58ba-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="c58ba-276">WPF, Silverlight und Konsolenanwendung Codebeispiele für Clientmethoden, die der Server aufgerufen werden können</span><span class="sxs-lookup"><span data-stu-id="c58ba-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="c58ba-277">Die Codebeispiele, die zuvor gezeigte zum Definieren von Clientmethoden, die der Server aufrufen kann, gelten für WinRT-Clients.</span><span class="sxs-lookup"><span data-stu-id="c58ba-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="c58ba-278">Den folgenden Beispielen wird den entsprechenden Code für WPF, Silverlight und Console Application-Clients.</span><span class="sxs-lookup"><span data-stu-id="c58ba-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="c58ba-279">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-279">Methods without parameters</span></span>

**<span data-ttu-id="c58ba-280">WPF-Clientcode für die Methode wird vom Server ohne Parameter aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-280">WPF client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**<span data-ttu-id="c58ba-281">Silverlight-Client-Code für die Methode wird vom Server ohne Parameter aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="c58ba-281">Silverlight client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**<span data-ttu-id="c58ba-282">Console Application-Clientcode für die Methode aufgerufen wird, vom Server ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-282">Console application client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="c58ba-283">Methoden mit Parametern, die Parametertypen angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-283">Methods with parameters, specifying the parameter types</span></span>

**<span data-ttu-id="c58ba-284">WPF-Client-Code für eine Methode aufgerufen wird, vom Server mit einem parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-284">WPF client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**<span data-ttu-id="c58ba-285">Silverlight-Client-Code für eine Methode aufgerufen wird, vom Server mit einem parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-285">Silverlight client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**<span data-ttu-id="c58ba-286">Console Application-Clientcode für eine Methode aufgerufen wird, vom Server mit einem parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-286">Console application client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="c58ba-287">Methoden mit Parametern, dynamische Objekte für die Parameter angeben</span><span class="sxs-lookup"><span data-stu-id="c58ba-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

**<span data-ttu-id="c58ba-288">WPF-Client-Code für eine Methode aufgerufen wird, vom Server mit einem Parameter, die ein dynamisches Objekt verwenden, für den parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-288">WPF client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**<span data-ttu-id="c58ba-289">Silverlight-Client-Code für eine Methode aufgerufen wird, vom Server mit einem Parameter, die ein dynamisches Objekt verwenden, für den parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-289">Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**<span data-ttu-id="c58ba-290">Console Application-Clientcode für eine Methode aufgerufen wird, vom Server mit einem Parameter, die ein dynamisches Objekt verwenden, für den parameter</span><span class="sxs-lookup"><span data-stu-id="c58ba-290">Console application client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
