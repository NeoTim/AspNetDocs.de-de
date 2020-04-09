---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hubs API Guide - .NET Client (C) | Microsoft Docs
author: bradygaster
description: Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in .NET-Clients wie Windows Store (WinRT), WPF, Silverlight und Cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675928"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="3a0f5-103">ASP.NET SignalR Hubs API Guide - .NET Client (C')</span><span class="sxs-lookup"><span data-stu-id="3a0f5-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3a0f5-104">Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in .NET-Clients wie Windows Store (WinRT), WPF, Silverlight und Konsolenanwendungen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="3a0f5-105">Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="3a0f5-106">Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="3a0f5-107">Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="3a0f5-108">SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="3a0f5-109">SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="3a0f5-110">Eine Einführung in SignalR, Hubs und Persistent Connections oder ein Tutorial zum Erstellen einer vollständigen SignalR-Anwendung finden Sie unter [SignalR - Erste Schritte](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="3a0f5-111">In diesem Thema verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="3a0f5-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3a0f5-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="3a0f5-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3a0f5-113">.NET 4.5</span></span>
> - <span data-ttu-id="3a0f5-114">SignalR Version 2</span><span class="sxs-lookup"><span data-stu-id="3a0f5-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="3a0f5-115">Frühere Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="3a0f5-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="3a0f5-116">Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3a0f5-117">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="3a0f5-117">Questions and comments</span></span>
>
> <span data-ttu-id="3a0f5-118">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3a0f5-119">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="3a0f5-120">Übersicht</span><span class="sxs-lookup"><span data-stu-id="3a0f5-120">Overview</span></span>

<span data-ttu-id="3a0f5-121">Dieses Dokument enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="3a0f5-122">Client-Setup</span><span class="sxs-lookup"><span data-stu-id="3a0f5-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="3a0f5-123">So stellen Sie eine Verbindung her</span><span class="sxs-lookup"><span data-stu-id="3a0f5-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="3a0f5-124">Domänenübergreifende Verbindungen von Silverlight-Clients</span><span class="sxs-lookup"><span data-stu-id="3a0f5-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="3a0f5-125">So konfigurieren Sie die Verbindung</span><span class="sxs-lookup"><span data-stu-id="3a0f5-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="3a0f5-126">Festlegen der maximalen Anzahl gleichzeitiger Verbindungen in WPF-Clients</span><span class="sxs-lookup"><span data-stu-id="3a0f5-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="3a0f5-127">Angeben von Abfragezeichenfolgenparametern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="3a0f5-128">So geben Sie die Transportmethode an</span><span class="sxs-lookup"><span data-stu-id="3a0f5-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="3a0f5-129">Angeben von HTTP-Headern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="3a0f5-130">Angeben von Clientzertifikaten</span><span class="sxs-lookup"><span data-stu-id="3a0f5-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="3a0f5-131">Erstellen des Hub-Proxys</span><span class="sxs-lookup"><span data-stu-id="3a0f5-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="3a0f5-132">Definieren von Methoden auf dem Client, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="3a0f5-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="3a0f5-133">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="3a0f5-134">Methoden mit Parametern, Angabe von Parametertypen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="3a0f5-135">Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="3a0f5-136">So entfernen Sie einen Handler</span><span class="sxs-lookup"><span data-stu-id="3a0f5-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="3a0f5-137">Aufrufen von Servermethoden vom Client</span><span class="sxs-lookup"><span data-stu-id="3a0f5-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="3a0f5-138">Behandeln von Verbindungslebensdauerereignissen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="3a0f5-139">Umgang mit Fehlern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="3a0f5-140">So aktivieren Sie die clientseitige Protokollierung</span><span class="sxs-lookup"><span data-stu-id="3a0f5-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="3a0f5-141">WPF-, Silverlight- und Konsolenanwendungscodebeispiele für Clientmethoden, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="3a0f5-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="3a0f5-142">Ein Beispiel für .NET-Clientprojekte finden Sie unter den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="3a0f5-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) auf GitHub.com (WinRT, Silverlight, Konsolen-App-Beispiele).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="3a0f5-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) auf GitHub.com (WPF-Beispiel).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="3a0f5-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) auf GitHub.com (Beispiel Konsolen-App).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="3a0f5-146">Eine Dokumentation zum Programmieren des Servers oder der JavaScript-Clients finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="3a0f5-147">SignalR Hubs API Guide - Server</span><span class="sxs-lookup"><span data-stu-id="3a0f5-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="3a0f5-148">SignalR Hubs API-Handbuch - JavaScript-Client</span><span class="sxs-lookup"><span data-stu-id="3a0f5-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="3a0f5-149">Links zu API-Referenzthemen beziehen sich auf die .NET 4.5-Version der API.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="3a0f5-150">Wenn Sie .NET 4 verwenden, lesen Sie [die .NET 4-Version der API-Themen](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="3a0f5-151">Clientsetup</span><span class="sxs-lookup"><span data-stu-id="3a0f5-151">Client setup</span></span>

<span data-ttu-id="3a0f5-152">Installieren Sie das [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet-Paket (nicht das [Microsoft.AspNet.SignalR-Paket).](http://nuget.org/packages/microsoft.aspnet.signalr)</span><span class="sxs-lookup"><span data-stu-id="3a0f5-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="3a0f5-153">Dieses Paket unterstützt WinRT-, Silverlight-, WPF-, Konsolenanwendung und Windows Phone-Clients für .NET 4 und .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="3a0f5-154">Wenn sich die Version von SignalR auf dem Client von der Version auf dem Server unterscheidet, kann sich SignalR häufig an den Unterschied anpassen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="3a0f5-155">Ein Server, auf dem SignalR Version 2 ausgeführt wird, unterstützt beispielsweise Clients, auf denen 1.1.x installiert ist, sowie Clients, auf denen Version 2 installiert ist.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="3a0f5-156">Wenn der Unterschied zwischen der Version auf dem Server und der Version auf dem Client zu groß `InvalidOperationException` ist oder wenn der Client neuer als der Server ist, löst SignalR eine Ausnahme aus, wenn der Client versucht, eine Verbindung herzustellen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="3a0f5-157">Die Fehlermeldung lautet`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" ".</span><span class="sxs-lookup"><span data-stu-id="3a0f5-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="3a0f5-158">So stellen Sie eine Verbindung her</span><span class="sxs-lookup"><span data-stu-id="3a0f5-158">How to establish a connection</span></span>

<span data-ttu-id="3a0f5-159">Bevor Sie eine Verbindung herstellen können, `HubConnection` müssen Sie ein Objekt erstellen und einen Proxy erstellen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="3a0f5-160">Um die Verbindung herzustellen, rufen Sie die `Start` Methode für das `HubConnection` Objekt auf.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="3a0f5-161">Für JavaScript-Clients müssen Sie mindestens einen Ereignishandler registrieren, bevor Sie die `Start` Methode aufrufen, um die Verbindung herzustellen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="3a0f5-162">Dies ist für .NET-Clients nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="3a0f5-163">Für JavaScript-Clients erstellt der generierte Proxycode automatisch Proxys für alle Hubs, die auf dem Server vorhanden sind, und beim Registrieren eines Handlers geben Sie an, welche Hubs Ihr Client verwenden möchte.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="3a0f5-164">Für einen .NET-Client erstellen Sie Hub-Proxys jedoch manuell, daher geht SignalR davon aus, dass Sie einen hub verwenden, für den Sie einen Proxy erstellen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="3a0f5-165">Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="3a0f5-166">Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="3a0f5-167">Die `Start` Methode wird asynchron ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="3a0f5-168">Um sicherzustellen, dass nachfolgende Codezeilen erst ausgeführt werden, `await` nachdem die Verbindung hergestellt wurde, `.Wait()` verwenden Sie eine ASP.NET asynchrone Methode 4.5 oder eine synchrone Methode.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="3a0f5-169">Nicht in `.Wait()` einem WinRT-Client verwenden.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="3a0f5-170">Domänenübergreifende Verbindungen von Silverlight-Clients</span><span class="sxs-lookup"><span data-stu-id="3a0f5-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="3a0f5-171">Informationen zum Aktivieren domänenübergreifender Verbindungen von Silverlight-Clients finden Sie unter [Verfügbarmachen eines Dienstes über Domänengrenzen](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)hinweg .</span><span class="sxs-lookup"><span data-stu-id="3a0f5-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="3a0f5-172">So konfigurieren Sie die Verbindung</span><span class="sxs-lookup"><span data-stu-id="3a0f5-172">How to configure the connection</span></span>

<span data-ttu-id="3a0f5-173">Bevor Sie eine Verbindung herstellen, können Sie eine der folgenden Optionen angeben:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="3a0f5-174">Grenzwerte für gleichzeitige Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="3a0f5-175">Abfragezeichenfolgenparameter.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-175">Query string parameters.</span></span>
- <span data-ttu-id="3a0f5-176">Die Transportmethode.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-176">The transport method.</span></span>
- <span data-ttu-id="3a0f5-177">HTTP-Header.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-177">HTTP headers.</span></span>
- <span data-ttu-id="3a0f5-178">Clientzertifikate.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="3a0f5-179">Festlegen der maximalen Anzahl gleichzeitiger Verbindungen in WPF-Clients</span><span class="sxs-lookup"><span data-stu-id="3a0f5-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="3a0f5-180">In WPF-Clients müssen Sie möglicherweise die maximale Anzahl gleichzeitiger Verbindungen von ihrem Standardwert 2 erhöhen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="3a0f5-181">Der empfohlene Wert ist 10.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="3a0f5-182">Weitere Informationen finden Sie unter [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="3a0f5-183">Angeben von Abfragezeichenfolgenparametern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-183">How to specify query string parameters</span></span>

<span data-ttu-id="3a0f5-184">Wenn Sie Daten an den Server senden möchten, wenn der Client eine Verbindung herstellt, können Sie dem Verbindungsobjekt Abfragezeichenfolgenparameter hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="3a0f5-185">Das folgende Beispiel zeigt, wie ein Abfragezeichenfolgenparameter im Clientcode festgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="3a0f5-186">Das folgende Beispiel zeigt, wie sie einen Abfragezeichenfolgenparameter im Servercode lesen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="3a0f5-187">So geben Sie die Transportmethode an</span><span class="sxs-lookup"><span data-stu-id="3a0f5-187">How to specify the transport method</span></span>

<span data-ttu-id="3a0f5-188">Im Rahmen der Verbindung verhandelt ein SignalR-Client normalerweise mit dem Server, um den besten Transport zu ermitteln, der sowohl vom Server als auch vom Client unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="3a0f5-189">Wenn Sie bereits wissen, welchen Transport Sie verwenden möchten, können Sie diesen Aushandlungsprozess umgehen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="3a0f5-190">Um die Transportmethode anzugeben, übergeben Sie ein Transportobjekt an die Start-Methode.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="3a0f5-191">Das folgende Beispiel zeigt, wie die Transportmethode im Clientcode angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="3a0f5-192">Der [Namespace Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) enthält die folgenden Klassen, die Sie zum Angeben des Transports verwenden können.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="3a0f5-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="3a0f5-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="3a0f5-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="3a0f5-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="3a0f5-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Verfügbar nur, wenn Server und Client .NET 4.5 verwenden.)</span><span class="sxs-lookup"><span data-stu-id="3a0f5-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="3a0f5-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Wählt automatisch den besten Transport aus, der sowohl vom Client als auch vom Server unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="3a0f5-197">Dies ist der Standardtransport.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-197">This is the default transport.</span></span> <span data-ttu-id="3a0f5-198">Das Übergeben an `Start` die Methode hat den gleichen Effekt wie das Übergeben von nichts.)</span><span class="sxs-lookup"><span data-stu-id="3a0f5-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="3a0f5-199">Der ForeverFrame-Transport ist nicht in dieser Liste enthalten, da er nur von Browsern verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="3a0f5-200">Informationen zum Überprüfen der Transportmethode im Servercode finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context-Eigenschaft](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="3a0f5-201">Weitere Informationen zu Transporten und Fallbacks finden Sie unter [Einführung in SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="3a0f5-202">Angeben von HTTP-Headern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-202">How to specify HTTP headers</span></span>

<span data-ttu-id="3a0f5-203">Um HTTP-Header festzulegen, `Headers` verwenden Sie die Eigenschaft für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="3a0f5-204">Das folgende Beispiel zeigt, wie Sie einen HTTP-Header hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="3a0f5-205">Angeben von Clientzertifikaten</span><span class="sxs-lookup"><span data-stu-id="3a0f5-205">How to specify client certificates</span></span>

<span data-ttu-id="3a0f5-206">Um Clientzertifikate hinzuzufügen, `AddClientCertificate` verwenden Sie die Methode für das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="3a0f5-207">Erstellen des Hub-Proxys</span><span class="sxs-lookup"><span data-stu-id="3a0f5-207">How to create the Hub proxy</span></span>

<span data-ttu-id="3a0f5-208">Um Methoden auf dem Client zu definieren, die ein Hub vom Server aufrufen kann, und um Methoden `CreateHubProxy` auf einem Hub auf dem Server aufzurufen, erstellen Sie einen Proxy für den Hub, indem Sie das Verbindungsobjekt aufrufen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="3a0f5-209">Die Zeichenfolge, an `CreateHubProxy` die Sie übergeben werden, ist der `HubName` Name Ihrer Hub-Klasse oder der Name, der durch das Attribut angegeben wird, wenn eine Zeichenfolge auf dem Server verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="3a0f5-210">Für die Namenszuordnung wird keine Groß-/Kleinschreibung berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="3a0f5-211">**Hub-Klasse auf dem Server**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="3a0f5-212">**Erstellen eines Clientproxys für die Hub-Klasse**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="3a0f5-213">Wenn Sie Ihre Hub-Klasse `HubName` mit einem Attribut dekorieren, verwenden Sie diesen Namen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="3a0f5-214">**Hub-Klasse auf dem Server**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="3a0f5-215">**Erstellen eines Clientproxys für die Hub-Klasse**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="3a0f5-216">Wenn Sie `HubConnection.CreateHubProxy` mehrmals mit `hubName`demselben aufrufen, erhalten `IHubProxy` Sie dasselbe zwischengespeicherte Objekt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="3a0f5-217">Definieren von Methoden auf dem Client, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="3a0f5-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="3a0f5-218">Um eine Methode zu definieren, die der `On` Server aufrufen kann, verwenden Sie die Methode des Proxys, um einen Ereignishandler zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="3a0f5-219">Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="3a0f5-220">Auf dem `Clients.All.UpdateStockPrice` Server wird `updateStockPrice`z. B. ausgeführt , `updatestockprice`, oder `UpdateStockPrice` auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="3a0f5-221">Verschiedene Clientplattformen haben unterschiedliche Anforderungen für das Schreiben von Methodencode zum Aktualisieren der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="3a0f5-222">Die gezeigten Beispiele beziehen sich auf WinRT-Clients (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="3a0f5-223">Beispiele für WPF-, Silverlight- und Konsolenanwendungen werden [in einem separaten Abschnitt weiter unten in diesem Thema](#wpfsl)bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="3a0f5-224">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-224">Methods without parameters</span></span>

<span data-ttu-id="3a0f5-225">Wenn die Methode, die Sie behandeln, keine Parameter enthält, `On` verwenden Sie die nicht generische Überladung der Methode:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="3a0f5-226">**Servercode, der clientmethod ohne Parameter aufruft**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="3a0f5-227">**WinRT-Clientcode für eine Methode, die vom Server ohne Parameter aufgerufen wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="3a0f5-228">Methoden mit Parametern, Angabe der Parametertypen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="3a0f5-229">Wenn die Methode, die Sie behandeln, über Parameter verfügt, geben `On` Sie die Typen der Parameter als generische Typen der Methode an.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="3a0f5-230">Es gibt generische Überladungen der Methode, mit denen `On` Sie bis zu 8 Parameter angeben können (4 unter Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="3a0f5-231">Im folgenden Beispiel wird ein Parameter `UpdateStockPrice` an die Methode gesendet.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="3a0f5-232">**Servercode, der die Clientmethode mit einem Parameter aufruft**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="3a0f5-233">**Die für den Parameter verwendete Stock-Klasse**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="3a0f5-234">**WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="3a0f5-235">Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="3a0f5-236">Alternativ zum Angeben von Parametern als `On` generische Typen der Methode können Sie Parameter als dynamische Objekte angeben:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="3a0f5-237">**Servercode, der die Clientmethode mit einem Parameter aufruft**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="3a0f5-238">**Die für den Parameter verwendete Stock-Klasse**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="3a0f5-239">**WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="3a0f5-240">So entfernen Sie einen Handler</span><span class="sxs-lookup"><span data-stu-id="3a0f5-240">How to remove a handler</span></span>

<span data-ttu-id="3a0f5-241">Um einen Handler zu `Dispose` entfernen, rufen Sie seine Methode auf.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="3a0f5-242">**Clientcode für eine vom Server aufgerufene Methode**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="3a0f5-243">**Clientcode zum Entfernen des Handlers**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="3a0f5-244">Aufrufen von Servermethoden vom Client</span><span class="sxs-lookup"><span data-stu-id="3a0f5-244">How to call server methods from the client</span></span>

<span data-ttu-id="3a0f5-245">Um eine Methode auf dem `Invoke` Server aufzurufen, verwenden Sie die Methode auf dem Hub-Proxy.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="3a0f5-246">Wenn die Servermethode keinen Rückgabewert hat, verwenden Sie `Invoke` die nicht generische Überladung der Methode.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="3a0f5-247">**Servercode für eine Methode ohne Rückgabewert**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="3a0f5-248">**Clientcode, der eine Methode aufruft, die keinen Rückgabewert hat**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="3a0f5-249">Wenn die Servermethode über einen Rückgabewert verfügt, geben `Invoke` Sie den Rückgabetyp als generischen Typ der Methode an.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="3a0f5-250">**Servercode für eine Methode, die einen Rückgabewert hat und einen komplexen Typparameter annimmt**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="3a0f5-251">**Die Für den Parameter und den Rückgabewert verwendete Stock-Klasse**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="3a0f5-252">**Clientcode, der eine Methode aufruft, die einen Rückgabewert hat und einen komplexen Typparameter annimmt, in einer ASP.NET 4.5-Async-Methode**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="3a0f5-253">**Clientcode, der eine Methode aufruft, die einen Rückgabewert hat und einen komplexen Typparameter annimmt, in einer synchronen Methode**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="3a0f5-254">Die `Invoke` Methode wird asynchron ausgeführt `Task` und gibt ein Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="3a0f5-255">Wenn Sie nicht `await` angeben `.Wait()`oder nicht , wird die nächste Codezeile ausgeführt, bevor die Methode, die Sie aufrufen, die Ausführung abgeschlossen hat.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="3a0f5-256">Behandeln von Verbindungslebensdauerereignissen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="3a0f5-257">SignalR stellt die folgenden Verbindungslebensdauerereignisse bereit, die Sie verarbeiten können:</span><span class="sxs-lookup"><span data-stu-id="3a0f5-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="3a0f5-258">`Received`: Wird ausgelöst, wenn Daten über die Verbindung empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="3a0f5-259">Stellt die empfangenen Daten bereit.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-259">Provides the received data.</span></span>
- <span data-ttu-id="3a0f5-260">`ConnectionSlow`: Wird ausgelöst, wenn der Client eine langsame oder häufig abbrechende Verbindung erkennt.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="3a0f5-261">`Reconnecting`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden wird.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="3a0f5-262">`Reconnected`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="3a0f5-263">`StateChanged`: Wird ausgelöst, wenn sich der Verbindungsstatus ändert.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="3a0f5-264">Stellt den alten und den neuen Status bereit.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-264">Provides the old state and the new state.</span></span> <span data-ttu-id="3a0f5-265">Informationen zu Verbindungsstatuswerten finden Sie unter [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="3a0f5-266">`Closed`: Wird ausgelöst, wenn die Verbindung getrennt wurde.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="3a0f5-267">Wenn Sie z. B. Warnmeldungen für Fehler anzeigen möchten, die nicht schwerwiegend sind, aber intermittierende Verbindungsprobleme verursachen, z. B. Langsamkeit oder häufiges Abbrechen der Verbindung, behandeln Sie das `ConnectionSlow` Ereignis.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="3a0f5-268">Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="3a0f5-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="3a0f5-269">Umgang mit Fehlern</span><span class="sxs-lookup"><span data-stu-id="3a0f5-269">How to handle errors</span></span>

<span data-ttu-id="3a0f5-270">Wenn Sie detaillierte Fehlermeldungen auf dem Server nicht explizit aktivieren, enthält das Ausnahmeobjekt, das SignalR nach einem Fehler zurückgibt, minimale Informationen über den Fehler.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="3a0f5-271">Wenn z. B. `newContosoChatMessage` ein Aufruf von fehlschlägt,`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`enthält die Fehlermeldung im Fehlerobjekt " " Das Senden detaillierter Fehlermeldungen an Clients in der Produktion wird aus Sicherheitsgründen nicht empfohlen, aber wenn Sie detaillierte Fehlermeldungen zur Fehlerbehebung aktivieren möchten, verwenden Sie den folgenden Code auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="3a0f5-272">Um Fehler zu behandeln, die SignalR auslöst, können Sie einen Handler für das `Error` Ereignis für das Verbindungsobjekt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="3a0f5-273">Um Fehler aus Methodenaufrufen zu behandeln, umschließen Sie den Code in einem try-catch-Block.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="3a0f5-274">So aktivieren Sie die clientseitige Protokollierung</span><span class="sxs-lookup"><span data-stu-id="3a0f5-274">How to enable client-side logging</span></span>

<span data-ttu-id="3a0f5-275">Um die clientseitige Protokollierung `TraceLevel` `TraceWriter` zu aktivieren, legen Sie die und eigenschaften für das Verbindungsobjekt fest.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="3a0f5-276">WPF-, Silverlight- und Konsolenanwendungscodebeispiele für Clientmethoden, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="3a0f5-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="3a0f5-277">Die zuvor gezeigten Codebeispiele zum Definieren von Clientmethoden, die der Server aufrufen kann, gelten für WinRT-Clients.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="3a0f5-278">Die folgenden Beispiele zeigen den entsprechenden Code für WPF-, Silverlight- und Konsolenanwendungsclients.</span><span class="sxs-lookup"><span data-stu-id="3a0f5-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="3a0f5-279">Methoden ohne Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-279">Methods without parameters</span></span>

<span data-ttu-id="3a0f5-280">**WPF-Clientcode für methode, die vom Server ohne Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="3a0f5-281">**Silverlight-Clientcode für methode, die vom Server ohne Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="3a0f5-282">**Konsolenanwendungsclientcode für Methode, die vom Server ohne Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="3a0f5-283">Methoden mit Parametern, Angabe der Parametertypen</span><span class="sxs-lookup"><span data-stu-id="3a0f5-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="3a0f5-284">**WPF-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="3a0f5-285">**Silverlight-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="3a0f5-286">**Konsolenanwendungsclientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="3a0f5-287">Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter</span><span class="sxs-lookup"><span data-stu-id="3a0f5-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="3a0f5-288">**WPF-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="3a0f5-289">**Silverlight-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="3a0f5-290">**Konsolenanwendungsclientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**</span><span class="sxs-lookup"><span data-stu-id="3a0f5-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
