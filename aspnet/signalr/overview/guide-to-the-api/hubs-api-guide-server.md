---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hubs API Guide - Server (C) | Microsoft Docs
author: bradygaster
description: Dieses Dokument bietet eine Einführung in die Programmierung der Serverseite der ASP.NET SignalR Hubs API für SignalR Version 2, wobei Codebeispiele...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675802"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="4c38c-103">ASP.NET SignalR Hubs API Guide - Server (C')</span><span class="sxs-lookup"><span data-stu-id="4c38c-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="4c38c-104">von [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4c38c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4c38c-105">Dieses Dokument bietet eine Einführung in die Programmierung der Serverseite der ASP.NET SignalR Hubs API für SignalR Version 2, wobei Codebeispiele allgemeine Optionen demonstrieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="4c38c-106">Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="4c38c-107">Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="4c38c-108">Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="4c38c-109">SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.</span><span class="sxs-lookup"><span data-stu-id="4c38c-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="4c38c-110">SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="4c38c-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="4c38c-111">Eine Einführung in SignalR, Hubs und persistente Verbindungen finden Sie unter [Einführung in SignalR 2](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="4c38c-112">In diesem Thema verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="4c38c-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="4c38c-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4c38c-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="4c38c-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4c38c-114">.NET 4.5</span></span>
> - <span data-ttu-id="4c38c-115">SignalR Version 2</span><span class="sxs-lookup"><span data-stu-id="4c38c-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="4c38c-116">Themenversionen</span><span class="sxs-lookup"><span data-stu-id="4c38c-116">Topic versions</span></span>
> 
> <span data-ttu-id="4c38c-117">Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="4c38c-118">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="4c38c-118">Questions and comments</span></span>
> 
> <span data-ttu-id="4c38c-119">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="4c38c-120">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="4c38c-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="4c38c-121">Übersicht</span><span class="sxs-lookup"><span data-stu-id="4c38c-121">Overview</span></span>

<span data-ttu-id="4c38c-122">Dieses Dokument enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="4c38c-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="4c38c-123">So registrieren Sie SignalR Middleware</span><span class="sxs-lookup"><span data-stu-id="4c38c-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="4c38c-124">Die /signalr URL</span><span class="sxs-lookup"><span data-stu-id="4c38c-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="4c38c-125">Konfigurieren von SignalR-Optionen</span><span class="sxs-lookup"><span data-stu-id="4c38c-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="4c38c-126">Erstellen und Verwenden von Hub-Klassen</span><span class="sxs-lookup"><span data-stu-id="4c38c-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="4c38c-127">Hub-Objektlebensdauer</span><span class="sxs-lookup"><span data-stu-id="4c38c-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="4c38c-128">Camel-Gehäuse von Hub-Namen in JavaScript-Clients</span><span class="sxs-lookup"><span data-stu-id="4c38c-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="4c38c-129">Mehrere Hubs</span><span class="sxs-lookup"><span data-stu-id="4c38c-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="4c38c-130">Stark typisierte Hubs</span><span class="sxs-lookup"><span data-stu-id="4c38c-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="4c38c-131">Definieren von Methoden in der Hub-Klasse, die Clients aufrufen können</span><span class="sxs-lookup"><span data-stu-id="4c38c-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="4c38c-132">Kamelgehäuse von Methodennamen in JavaScript-Clients</span><span class="sxs-lookup"><span data-stu-id="4c38c-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="4c38c-133">Wann asynchron ausgeführt werden soll</span><span class="sxs-lookup"><span data-stu-id="4c38c-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="4c38c-134">Definieren von Überladungen</span><span class="sxs-lookup"><span data-stu-id="4c38c-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="4c38c-135">Melden des Fortschritts aus Hubmethodenaufrufen</span><span class="sxs-lookup"><span data-stu-id="4c38c-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="4c38c-136">Aufrufen von Clientmethoden aus der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="4c38c-137">Auswählen, welche Clients den RPC erhalten</span><span class="sxs-lookup"><span data-stu-id="4c38c-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="4c38c-138">Keine Kompilierungszeitüberprüfung für Methodennamen</span><span class="sxs-lookup"><span data-stu-id="4c38c-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="4c38c-139">Bei Fall-in-Sensitive-Methodennameabgleich</span><span class="sxs-lookup"><span data-stu-id="4c38c-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="4c38c-140">Asynchrone Ausführung</span><span class="sxs-lookup"><span data-stu-id="4c38c-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="4c38c-141">Verwalten der Gruppenmitgliedschaft aus der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="4c38c-142">Asynchrone Ausführung von Add- und Remove-Methoden</span><span class="sxs-lookup"><span data-stu-id="4c38c-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="4c38c-143">Gruppenmitgliedschaft Persistenz</span><span class="sxs-lookup"><span data-stu-id="4c38c-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="4c38c-144">Einzelbenutzergruppen</span><span class="sxs-lookup"><span data-stu-id="4c38c-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="4c38c-145">Behandeln von Verbindungslebensdauerereignissen in der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="4c38c-146">Wenn OnConnected, OnDisconnected und OnReconnected aufgerufen werden</span><span class="sxs-lookup"><span data-stu-id="4c38c-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="4c38c-147">Anruferstatus nicht bevölkert</span><span class="sxs-lookup"><span data-stu-id="4c38c-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="4c38c-148">So erhalten Sie Informationen über den Client aus der Context-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="4c38c-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="4c38c-149">Übergeben des Status zwischen Clients und der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="4c38c-150">Behandeln von Fehlern in der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="4c38c-151">Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="4c38c-152">Aufrufen von Clientmethoden</span><span class="sxs-lookup"><span data-stu-id="4c38c-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="4c38c-153">Verwalten der Gruppenmitgliedschaft</span><span class="sxs-lookup"><span data-stu-id="4c38c-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="4c38c-154">So aktivieren Sie die Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="4c38c-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="4c38c-155">Anpassen der Hubs-Pipeline</span><span class="sxs-lookup"><span data-stu-id="4c38c-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="4c38c-156">Eine Dokumentation zum Programmieren von Clients finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="4c38c-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="4c38c-157">SignalR Hubs API-Handbuch - JavaScript-Client</span><span class="sxs-lookup"><span data-stu-id="4c38c-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="4c38c-158">SignalR Hubs API-Leitfaden - .NET Client</span><span class="sxs-lookup"><span data-stu-id="4c38c-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="4c38c-159">Die Serverkomponenten für SignalR 2 sind nur in .NET 4.5 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="4c38c-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="4c38c-160">Server mit .NET 4.0 müssen SignalR v1.x verwenden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="4c38c-161">So registrieren Sie SignalR Middleware</span><span class="sxs-lookup"><span data-stu-id="4c38c-161">How to register SignalR middleware</span></span>

<span data-ttu-id="4c38c-162">Um die Route zu definieren, die Clients zum `MapSignalR` Herstellen einer Verbindung mit Ihrem Hub verwenden, rufen Sie die Methode auf, wenn die Anwendung gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="4c38c-163">`MapSignalR`ist eine [Erweiterungsmethode](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) für die `OwinExtensions` Klasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="4c38c-164">Das folgende Beispiel zeigt, wie Sie die SignalR Hubs-Route mithilfe einer OWIN-Startklasse definieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="4c38c-165">Wenn Sie einer ASP.NET MVC-Anwendung SignalR-Funktionalität hinzufügen, stellen Sie sicher, dass die SignalR-Route vor den anderen Routen hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="4c38c-166">Weitere Informationen finden Sie unter [Tutorial: Erste Schritte mit SignalR 2 und MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="4c38c-167">Die /signalr URL</span><span class="sxs-lookup"><span data-stu-id="4c38c-167">The /signalr URL</span></span>

<span data-ttu-id="4c38c-168">Standardmäßig lautet die Routen-URL, die Clients zum Herstellen einer Verbindung mit Ihrem Hub verwenden, "/signalr".</span><span class="sxs-lookup"><span data-stu-id="4c38c-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="4c38c-169">(Verwechseln Sie diese URL nicht mit der URL "/signalr/hubs", die für die automatisch generierte JavaScript-Datei gilt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="4c38c-170">Weitere Informationen zum generierten Proxy finden Sie unter [SignalR Hubs API Guide - JavaScript Client - Der generierte Proxy und was er für Sie tut](hubs-api-guide-javascript-client.md#genproxy).)</span><span class="sxs-lookup"><span data-stu-id="4c38c-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="4c38c-171">Es kann außergewöhnliche Umstände geben, die diese Basis-URL nicht für SignalR nutzbar machen. Sie haben z. B. einen Ordner mit dem Namen *Signalr* in Ihrem Projekt und möchten den Namen nicht ändern.</span><span class="sxs-lookup"><span data-stu-id="4c38c-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="4c38c-172">In diesem Fall können Sie die Basis-URL ändern, wie in den folgenden Beispielen gezeigt (ersetzen Sie "/signalr" im Beispielcode durch Ihre gewünschte URL).</span><span class="sxs-lookup"><span data-stu-id="4c38c-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="4c38c-173">**Servercode, der die URL angibt**</span><span class="sxs-lookup"><span data-stu-id="4c38c-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="4c38c-174">**JavaScript-Clientcode, der die URL angibt (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="4c38c-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="4c38c-175">**JavaScript-Clientcode, der die URL angibt (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="4c38c-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="4c38c-176">**.NET-Clientcode, der die URL angibt**</span><span class="sxs-lookup"><span data-stu-id="4c38c-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="4c38c-177">Konfigurieren von SignalR-Optionen</span><span class="sxs-lookup"><span data-stu-id="4c38c-177">Configuring SignalR Options</span></span>

<span data-ttu-id="4c38c-178">Überladen der `MapSignalR` Methode ermöglichen es Ihnen, eine benutzerdefinierte URL, einen benutzerdefinierten Abhängigkeitslöser und die folgenden Optionen anzugeben:</span><span class="sxs-lookup"><span data-stu-id="4c38c-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="4c38c-179">Aktivieren Sie domänenübergreifende Anrufe mit CORS oder JSONP von Browserclients aus.</span><span class="sxs-lookup"><span data-stu-id="4c38c-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="4c38c-180">Wenn der Browser eine `http://contoso.com`Seite aus lädt, befindet sich die `http://contoso.com/signalr`SignalR-Verbindung in derselben Domäne unter .</span><span class="sxs-lookup"><span data-stu-id="4c38c-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="4c38c-181">Wenn die `http://contoso.com` Seite von `http://fabrikam.com/signalr`eine Verbindung zu herstellt, handelt es sich um eine domänenübergreifende Verbindung.</span><span class="sxs-lookup"><span data-stu-id="4c38c-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="4c38c-182">Aus Sicherheitsgründen sind domänenübergreifende Verbindungen standardmäßig deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="4c38c-183">Weitere Informationen finden Sie unter [ASP.NET SignalR Hubs API Guide - JavaScript Client - So stellen Sie eine domänenübergreifende Verbindung her.](hubs-api-guide-javascript-client.md#crossdomain)</span><span class="sxs-lookup"><span data-stu-id="4c38c-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="4c38c-184">Aktivieren Sie detaillierte Fehlermeldungen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="4c38c-185">Wenn Fehler auftreten, besteht das Standardverhalten von SignalR darin, eine Benachrichtigung ohne Details zu den Geschehnissen an Clients zu senden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="4c38c-186">Das Senden detaillierter Fehlerinformationen an Clients wird in der Produktion nicht empfohlen, da böswillige Benutzer die Informationen möglicherweise bei Angriffen auf Ihre Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4c38c-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="4c38c-187">Zur Fehlerbehebung können Sie diese Option verwenden, um vorübergehend eine informativere Fehlerberichterstattung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="4c38c-188">Deaktivieren Sie automatisch generierte JavaScript-Proxydateien.</span><span class="sxs-lookup"><span data-stu-id="4c38c-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="4c38c-189">Standardmäßig wird als Antwort auf die URL "/signalr/hubs" eine JavaScript-Datei mit Proxys für Ihre Hub-Klassen generiert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="4c38c-190">Wenn Sie die JavaScript-Proxys nicht verwenden möchten oder wenn Sie diese Datei manuell generieren und auf eine physische Datei in Ihren Clients verweisen möchten, können Sie diese Option verwenden, um die Proxygenerierung zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="4c38c-191">Weitere Informationen finden Sie unter [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span><span class="sxs-lookup"><span data-stu-id="4c38c-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="4c38c-192">Das folgende Beispiel zeigt, wie Sie die SignalR-Verbindungs-URL und diese Optionen in einem Aufruf der `MapSignalR` Methode angeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="4c38c-193">Um eine benutzerdefinierte URL anzugeben, ersetzen Sie "/signalr" im Beispiel durch die URL, die Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="4c38c-194">Erstellen und Verwenden von Hub-Klassen</span><span class="sxs-lookup"><span data-stu-id="4c38c-194">How to create and use Hub classes</span></span>

<span data-ttu-id="4c38c-195">Um einen Hub zu erstellen, erstellen Sie eine Klasse, die von [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)abstammt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="4c38c-196">Das folgende Beispiel zeigt eine einfache Hub-Klasse für eine Chatanwendung.</span><span class="sxs-lookup"><span data-stu-id="4c38c-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="4c38c-197">In diesem Beispiel kann ein `NewContosoChatMessage` verbundener Client die Methode aufrufen, und wenn dies der Fall ist, werden die empfangenen Daten an alle verbundenen Clients übertragen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="4c38c-198">Hub-Objektlebensdauer</span><span class="sxs-lookup"><span data-stu-id="4c38c-198">Hub object lifetime</span></span>

<span data-ttu-id="4c38c-199">Sie instanziieren die Hub-Klasse nicht oder rufen ihre Methoden nicht über Ihren eigenen Code auf dem Server auf. alles, was von der SignalR Hubs-Pipeline für Sie erledigt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="4c38c-200">SignalR erstellt jedes Mal eine neue Instanz Ihrer Hub-Klasse, wenn es einen Hub-Vorgang verarbeiten muss, z. B. wenn ein Client eine Verbindung herstellt, die Verbindung trennt oder einen Methodenaufruf an den Server ausführt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="4c38c-201">Da Instanzen der Hub-Klasse vorübergehend sind, können Sie sie nicht verwenden, um den Status von einem Methodenaufruf zum nächsten beizubehalten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="4c38c-202">Jedes Mal, wenn der Server einen Methodenaufruf von einem Client empfängt, verarbeitet eine neue Instanz Ihrer Hub-Klasse die Nachricht.</span><span class="sxs-lookup"><span data-stu-id="4c38c-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="4c38c-203">Um den Status über mehrere Verbindungen und Methodenaufrufe beizubehalten, verwenden Sie eine andere Methode, z. B. eine `Hub`Datenbank oder eine statische Variable für die Hub-Klasse oder eine andere Klasse, die nicht von ableitet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="4c38c-204">Wenn Sie Daten im Arbeitsspeicher beibehalten, wird die Daten mithilfe einer Methode wie einer statischen Variable in der Hub-Klasse verloren gehen, wenn die App-Domäne wiederverwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="4c38c-205">Wenn Sie Nachrichten von Ihrem eigenen Code an Clients senden möchten, der außerhalb der Hub-Klasse ausgeführt wird, können Sie dies nicht tun, indem Sie eine Hub-Klasseninstanz instanziieren, aber Sie können dies tun, indem Sie einen Verweis auf das SignalR-Kontextobjekt für Ihre Hub-Klasse abrufen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="4c38c-206">Weitere Informationen finden Sie weiter unten in diesem Thema unter [Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse.](#callfromoutsidehub)</span><span class="sxs-lookup"><span data-stu-id="4c38c-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="4c38c-207">Camel-Gehäuse von Hub-Namen in JavaScript-Clients</span><span class="sxs-lookup"><span data-stu-id="4c38c-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="4c38c-208">Standardmäßig verweisen JavaScript-Clients auf Hubs, indem sie eine Kamel-Case-Version des Klassennamens verwenden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="4c38c-209">SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.</span><span class="sxs-lookup"><span data-stu-id="4c38c-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="4c38c-210">Das vorherige Beispiel wird `contosoChatHub` wie in JavaScript-Code bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="4c38c-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="4c38c-212">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="4c38c-213">Wenn Sie einen anderen Namen für Clients angeben `HubName` möchten, fügen Sie das Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="4c38c-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="4c38c-214">Wenn Sie `HubName` ein Attribut verwenden, gibt es auf JavaScript-Clients keine Namensänderung in Kamelfall.</span><span class="sxs-lookup"><span data-stu-id="4c38c-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="4c38c-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="4c38c-216">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="4c38c-217">Mehrere Hubs</span><span class="sxs-lookup"><span data-stu-id="4c38c-217">Multiple Hubs</span></span>

<span data-ttu-id="4c38c-218">Sie können mehrere Hubklassen in einer Anwendung definieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="4c38c-219">Wenn Sie dies tun, wird die Verbindung freigegeben, aber Gruppen sind getrennt:</span><span class="sxs-lookup"><span data-stu-id="4c38c-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="4c38c-220">Alle Clients verwenden dieselbe URL, um eine SignalR-Verbindung mit Ihrem Dienst herzustellen ("/signalr" oder Ihre benutzerdefinierte URL, falls Sie eine angegeben haben), und diese Verbindung wird für alle Hubs verwendet, die vom Dienst definiert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="4c38c-221">Es gibt keinen Leistungsunterschied für mehrere Hubs im Vergleich zum Definieren aller Hub-Funktionen in einer einzelnen Klasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="4c38c-222">Alle Hubs erhalten dieselben HTTP-Anforderungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="4c38c-223">Da alle Hubs dieselbe Verbindung haben, erhalten die Server nur die Informationen über HTTP-Anforderung, die er erhält, die ursprüngliche HTTP-Anforderung, die die SignalR-Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="4c38c-224">Wenn Sie die Verbindungsanforderung verwenden, um Informationen vom Client an den Server zu übergeben, indem Sie eine Abfragezeichenfolge angeben, können Sie keine unterschiedlichen Abfragezeichenfolgen an verschiedene Hubs bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="4c38c-225">Alle Hubs erhalten die gleichen Informationen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="4c38c-226">Die generierte JavaScript-Proxydatei enthält Proxys für alle Hubs in einer Datei.</span><span class="sxs-lookup"><span data-stu-id="4c38c-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="4c38c-227">Weitere Informationen zu JavaScript-Proxys finden Sie unter [SignalR Hubs API Guide - JavaScript Client - Der generierte Proxy und was er für Sie tut.](hubs-api-guide-javascript-client.md#genproxy)</span><span class="sxs-lookup"><span data-stu-id="4c38c-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="4c38c-228">Gruppen werden in Hubs definiert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="4c38c-229">In SignalR können Sie benannte Gruppen definieren, die an Teilmengen verbundener Clients übertragen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="4c38c-230">Gruppen werden für jeden Hub separat verwaltet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="4c38c-231">Eine Gruppe mit dem Namen "Administratoren" würde z. B. einen Satz von Clients für Ihre `ContosoChatHub` `StockTickerHub` Klasse enthalten, und derselbe Gruppenname würde sich auf einen anderen Satz von Clients für Ihre Klasse beziehen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="4c38c-232">Stark typisierte Hubs</span><span class="sxs-lookup"><span data-stu-id="4c38c-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="4c38c-233">Um eine Schnittstelle für Ihre Hub-Methoden zu definieren, auf die Ihr Client verweisen kann `Hub<T>` (und Intellisense für `Hub`Ihre Hub-Methoden aktivieren), leiten Sie Ihren Hub von (in SignalR 2.1 eingeführt) ab und nicht:</span><span class="sxs-lookup"><span data-stu-id="4c38c-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="4c38c-234">Definieren von Methoden in der Hub-Klasse, die Clients aufrufen können</span><span class="sxs-lookup"><span data-stu-id="4c38c-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="4c38c-235">Um eine Methode auf dem Hub verfügbar zu machen, die vom Client aus aufrufbar sein soll, deklarieren Sie eine öffentliche Methode, wie in den folgenden Beispielen gezeigt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="4c38c-236">Sie können einen Rückgabetyp und Parameter, einschließlich komplexer Typen und Arrays, wie in jeder C-Methode angeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="4c38c-237">Alle Daten, die Sie in Parametern erhalten oder an den Aufrufer zurückgeben, werden mithilfe von JSON zwischen dem Client und dem Server übermittelt, und SignalR verarbeitet die Bindung komplexer Objekte und Arrays von Objekten automatisch.</span><span class="sxs-lookup"><span data-stu-id="4c38c-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="4c38c-238">Kamelgehäuse von Methodennamen in JavaScript-Clients</span><span class="sxs-lookup"><span data-stu-id="4c38c-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="4c38c-239">Standardmäßig verweisen JavaScript-Clients auf Hub-Methoden, indem sie eine Kamel-Case-Version des Methodennamens verwenden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="4c38c-240">SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.</span><span class="sxs-lookup"><span data-stu-id="4c38c-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="4c38c-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="4c38c-242">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="4c38c-243">Wenn Sie einen anderen Namen für Clients angeben `HubMethodName` möchten, fügen Sie das Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="4c38c-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="4c38c-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="4c38c-245">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="4c38c-246">Wann asynchron ausgeführt werden soll</span><span class="sxs-lookup"><span data-stu-id="4c38c-246">When to execute asynchronously</span></span>

<span data-ttu-id="4c38c-247">Wenn die Methode lang andauernd ausgeführt wird oder arbeiten muss, die warten würde, z. B. eine Datenbanksuche oder einen Webdienstaufruf, machen Sie die `T` Hub-Methode asynchron, indem Sie ein [Task-Objekt](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (anstelle der `void` Rückgabe) oder das [Task&lt;&gt; T-Objekt](https://msdn.microsoft.com/library/dd321424.aspx) (anstelle des Rückgabetyps) zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="4c38c-248">Wenn Sie `Task` ein Objekt von der Methode zurückgeben, wartet SignalR, bis der `Task` abgeschlossen ist, und sendet dann das entpackte Ergebnis an den Client zurück, sodass es keinen Unterschied in der Art und Weise gibt, wie Sie den Methodenaufruf im Client codieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="4c38c-249">Wenn Sie eine Hub-Methode asynchron machen, wird vermieden, dass die Verbindung blockiert wird, wenn sie den WebSocket-Transport verwendet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="4c38c-250">Wenn eine Hub-Methode synchron ausgeführt wird und der Transport WebSocket ist, werden nachfolgende Aufrufe von Methoden auf dem Hub vom gleichen Client blockiert, bis die Hub-Methode abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="4c38c-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="4c38c-251">Das folgende Beispiel zeigt dieselbe Methode, die für die Synchron- oder Asynchronausführung codiert ist, gefolgt von JavaScript-Clientcode, der zum Aufrufen einer der beiden Versionen funktioniert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="4c38c-252">**Synchrone**</span><span class="sxs-lookup"><span data-stu-id="4c38c-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="4c38c-253">**Asynchronen**</span><span class="sxs-lookup"><span data-stu-id="4c38c-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="4c38c-254">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="4c38c-255">Weitere Informationen zur Verwendung asynchroner Methoden in ASP.NET 4.5 finden Sie unter [Verwenden asynchroner Methoden in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="4c38c-256">Definieren von Überladungen</span><span class="sxs-lookup"><span data-stu-id="4c38c-256">Defining Overloads</span></span>

<span data-ttu-id="4c38c-257">Wenn Sie Überladungen für eine Methode definieren möchten, muss die Anzahl der Parameter in jeder Überladung unterschiedlich sein.</span><span class="sxs-lookup"><span data-stu-id="4c38c-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="4c38c-258">Wenn Sie eine Überlast nur durch die Angabe verschiedener Parametertypen unterscheiden, wird Ihre Hub-Klasse kompiliert, aber der SignalR-Dienst löst zur Laufzeit eine Ausnahme aus, wenn Clients versuchen, eine der Überladungen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="4c38c-259">Melden des Fortschritts aus Hubmethodenaufrufen</span><span class="sxs-lookup"><span data-stu-id="4c38c-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="4c38c-260">SignalR 2.1 unterstützt das in .NET 4.5 eingeführte [Fortschrittsberichtsmuster.](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)</span><span class="sxs-lookup"><span data-stu-id="4c38c-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="4c38c-261">Um die Fortschrittsberichterstattung zu implementieren, definieren Sie einen `IProgress<T>` Parameter für Ihre Hubmethode, auf den Ihr Client zugreifen kann:</span><span class="sxs-lookup"><span data-stu-id="4c38c-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="4c38c-262">Beim Schreiben einer lang andauernden Servermethode ist es wichtig, ein asynchrones Programmiermuster wie Async/ Await zu verwenden, anstatt den Hubthread zu blockieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="4c38c-263">Aufrufen von Clientmethoden aus der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="4c38c-264">Um Clientmethoden vom Server aufzurufen, verwenden Sie die `Clients` Eigenschaft in einer Methode in Ihrer Hubklasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="4c38c-265">Das folgende Beispiel zeigt `addNewMessageToPage` Servercode, der alle verbundenen Clients aufruft, und Clientcode, der die Methode in einem JavaScript-Client definiert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="4c38c-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="4c38c-267">Das Aufrufen einer Clientmethode ist ein asynchroner Vorgang und gibt eine `Task`zurück.</span><span class="sxs-lookup"><span data-stu-id="4c38c-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="4c38c-268">Verwenden Sie `await`:</span><span class="sxs-lookup"><span data-stu-id="4c38c-268">Use `await`:</span></span>

* <span data-ttu-id="4c38c-269">So stellen Sie sicher, dass die Nachricht fehlerfrei gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="4c38c-270">So aktivieren Sie Abfangen und Behandeln von Fehlern in einem Try-Catch-Block.</span><span class="sxs-lookup"><span data-stu-id="4c38c-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="4c38c-271">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="4c38c-272">Sie können keinen Rückgabewert von einer Clientmethode abrufen. Syntax, `int x = Clients.All.add(1,1)` wie sie nicht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="4c38c-273">Sie können komplexe Typen und Arrays für die Parameter angeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="4c38c-274">Im folgenden Beispiel wird ein komplexer Typ an den Client in einem Methodenparameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="4c38c-275">**Servercode, der eine Clientmethode mithilfe eines komplexen Objekts aufruft**</span><span class="sxs-lookup"><span data-stu-id="4c38c-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="4c38c-276">**Servercode, der das komplexe Objekt definiert**</span><span class="sxs-lookup"><span data-stu-id="4c38c-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="4c38c-277">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="4c38c-278">Auswählen, welche Clients den RPC erhalten</span><span class="sxs-lookup"><span data-stu-id="4c38c-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="4c38c-279">Die Clients-Eigenschaft gibt ein [HubConnectionContext-Objekt](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) zurück, das mehrere Optionen zum Angeben bereitstellt, welche Clients die RPC empfangen:</span><span class="sxs-lookup"><span data-stu-id="4c38c-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="4c38c-280">Alle verbundenen Clients.</span><span class="sxs-lookup"><span data-stu-id="4c38c-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="4c38c-281">Nur der aufrufende Client.</span><span class="sxs-lookup"><span data-stu-id="4c38c-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="4c38c-282">Alle Clients mit Ausnahme des aufrufenden Clients.</span><span class="sxs-lookup"><span data-stu-id="4c38c-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="4c38c-283">Ein bestimmter Client, der durch die Verbindungs-ID identifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="4c38c-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="4c38c-284">Dieses Beispiel `addContosoChatMessageToPage` ruft den aufrufenden Client auf `Clients.Caller`und hat den gleichen Effekt wie die Verwendung von .</span><span class="sxs-lookup"><span data-stu-id="4c38c-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="4c38c-285">Alle verbundenen Clients mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="4c38c-286">Alle verbundenen Clients in einer angegebenen Gruppe.</span><span class="sxs-lookup"><span data-stu-id="4c38c-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="4c38c-287">Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="4c38c-288">Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme des aufrufenden Clients.</span><span class="sxs-lookup"><span data-stu-id="4c38c-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="4c38c-289">Ein bestimmter Benutzer, der durch userId identifiziert wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="4c38c-290">Standardmäßig ist `IPrincipal.Identity.Name`dies , aber dies kann durch [Registrieren einer Implementierung von IUserIdProvider beim globalen Host](mapping-users-to-connections.md#IUserIdProvider)geändert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="4c38c-291">Alle Clients und Gruppen in einer Liste von Verbindungs-IDs.</span><span class="sxs-lookup"><span data-stu-id="4c38c-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="4c38c-292">Eine Liste von Gruppen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="4c38c-293">Ein Benutzer nach Namen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="4c38c-294">Eine Liste der Benutzernamen (eingeführt in SignalR 2.1).</span><span class="sxs-lookup"><span data-stu-id="4c38c-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="4c38c-295">Keine Kompilierungszeitüberprüfung für Methodennamen</span><span class="sxs-lookup"><span data-stu-id="4c38c-295">No compile-time validation for method names</span></span>

<span data-ttu-id="4c38c-296">Der von Ihnen angegebene Methodenname wird als dynamisches Objekt interpretiert, was bedeutet, dass es keine IntelliSense- oder Kompilierungszeitüberprüfung dafür gibt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="4c38c-297">Der Ausdruck wird zur Laufzeit ausgewertet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="4c38c-298">Wenn der Methodenaufruf ausgeführt wird, sendet SignalR den Methodennamen und die Parameterwerte an den Client, und wenn der Client über eine Methode verfügt, die dem Namen entspricht, wird diese Methode aufgerufen, und die Parameterwerte werden an ihn übergeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="4c38c-299">Wenn auf dem Client keine Übereinstimmende Methode gefunden wird, wird kein Fehler ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="4c38c-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="4c38c-300">Informationen zum Format der Daten, die SignalR beim Aufrufen einer Clientmethode an den Client überträgt, finden Sie unter [Einführung in SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="4c38c-301">Bei Fall-in-Sensitive-Methodennameabgleich</span><span class="sxs-lookup"><span data-stu-id="4c38c-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="4c38c-302">Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="4c38c-303">Auf dem `Clients.All.addContosoChatMessageToPage` Server wird `AddContosoChatMessageToPage`z. B. ausgeführt , `addcontosochatmessagetopage`, oder `addContosoChatMessageToPage` auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="4c38c-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="4c38c-304">Asynchrone Ausführung</span><span class="sxs-lookup"><span data-stu-id="4c38c-304">Asynchronous execution</span></span>

<span data-ttu-id="4c38c-305">Die Methode, die Sie aufrufen, wird asynchron ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="4c38c-306">Jeder Code, der nach einem Methodenaufruf an einen Client kommt, wird sofort ausgeführt, ohne darauf zu warten, dass SignalR die Übertragung von Daten an Clients beendet, es sei denn, Sie geben an, dass die nachfolgenden Codezeilen auf den Abschluss der Methode warten sollen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="4c38c-307">Das folgende Codebeispiel zeigt, wie zwei Clientmethoden sequenziell ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="4c38c-308">**Verwenden von Await (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="4c38c-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="4c38c-309">Wenn Sie `await` warten, bis eine Clientmethode abgeschlossen ist, bevor die nächste Codezeile ausgeführt wird, bedeutet dies nicht, dass Clients die Nachricht tatsächlich empfangen, bevor die nächste Codezeile ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="4c38c-310">"Abschluss" eines Clientmethodenaufrufs bedeutet nur, dass SignalR alles Notwendige getan hat, um die Nachricht zu senden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="4c38c-311">Wenn Sie überprüfen müssen, ob Clients die Nachricht erhalten haben, müssen Sie diesen Mechanismus selbst programmieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="4c38c-312">Sie können z. `MessageReceived` B. eine Methode auf `addContosoChatMessageToPage` dem Hub codieren, und in der Methode auf dem Client können Sie aufrufen, `MessageReceived` nachdem Sie die Arbeit, die Sie auf dem Client erledigen müssen, durchgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="4c38c-313">Im `MessageReceived` Hub können Sie unabhängig davon tun, was vom tatsächlichen Clientempfang und der Verarbeitung des ursprünglichen Methodenaufrufs abhängt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="4c38c-314">Verwenden einer Zeichenfolgenvariablen als Methodenname</span><span class="sxs-lookup"><span data-stu-id="4c38c-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="4c38c-315">Wenn Sie eine Client-Methode aufrufen möchten, indem Sie `Clients.All` eine `Clients.Others`Zeichenfolgenvariable als Methodennamen verwenden, umwerfen (oder , `Clients.Caller`, usw.) an `IClientProxy` und rufen Sie dann [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)auf.</span><span class="sxs-lookup"><span data-stu-id="4c38c-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="4c38c-316">Verwalten der Gruppenmitgliedschaft aus der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="4c38c-317">Gruppen in SignalR stellen eine Methode zum Senden von Nachrichten an bestimmte Teilmengen verbundener Clients bereit.</span><span class="sxs-lookup"><span data-stu-id="4c38c-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="4c38c-318">Eine Gruppe kann eine beliebige Anzahl von Clients haben, und ein Client kann Mitglied einer beliebigen Anzahl von Gruppen sein.</span><span class="sxs-lookup"><span data-stu-id="4c38c-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="4c38c-319">Um die Gruppenmitgliedschaft zu verwalten, verwenden `Groups` Sie die Methoden [Hinzufügen](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) und [Entfernen,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) die von der Eigenschaft der Hub-Klasse bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="4c38c-320">Das folgende Beispiel `Groups.Add` `Groups.Remove` zeigt die und Methoden, die in Hub-Methoden verwendet werden, die vom Clientcode aufgerufen werden, gefolgt von JavaScript-Clientcode, der sie aufruft.</span><span class="sxs-lookup"><span data-stu-id="4c38c-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="4c38c-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="4c38c-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="4c38c-322">**JavaScript-Client mit generiertem Proxy**</span><span class="sxs-lookup"><span data-stu-id="4c38c-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="4c38c-323">Sie müssen keine Gruppen explizit erstellen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="4c38c-324">Tatsächlich wird eine Gruppe automatisch erstellt, wenn Sie ihren `Groups.Add`Namen zum ersten Mal in einem Aufruf von angeben, und sie wird gelöscht, wenn Sie die letzte Verbindung aus der Mitgliedschaft in ihr entfernen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="4c38c-325">Es gibt keine API zum Abrufen einer Gruppenmitgliedschaftsliste oder einer Liste von Gruppen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="4c38c-326">SignalR sendet Nachrichten an Clients und Gruppen basierend auf einem [Pub/Untermodell](http://en.wikipedia.org/wiki/Publish/subscribe), und der Server führt keine Listen von Gruppen oder Gruppenmitgliedschaften.</span><span class="sxs-lookup"><span data-stu-id="4c38c-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="4c38c-327">Dies trägt zur Maximierung der Skalierbarkeit bei, da jedes Mal, wenn Sie einen Knoten zu einer Webfarm hinzufügen, jeder Status, den SignalR verwaltet, an den neuen Knoten weitergegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="4c38c-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="4c38c-328">Asynchrone Ausführung von Add- und Remove-Methoden</span><span class="sxs-lookup"><span data-stu-id="4c38c-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="4c38c-329">Die `Groups.Add` `Groups.Remove` und-Methoden werden asynchron ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="4c38c-330">Wenn Sie einer Gruppe einen Client hinzufügen und sofort mithilfe der Gruppe eine Nachricht an `Groups.Add` den Client senden möchten, müssen Sie sicherstellen, dass die Methode zuerst abgeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="4c38c-331">Das folgende Codebeispiel zeigt, wie Sie dies tun.</span><span class="sxs-lookup"><span data-stu-id="4c38c-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="4c38c-332">**Hinzufügen eines Clients zu einer Gruppe und anschließende Übermittlung dieses Clients**</span><span class="sxs-lookup"><span data-stu-id="4c38c-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="4c38c-333">Gruppenmitgliedschaft Persistenz</span><span class="sxs-lookup"><span data-stu-id="4c38c-333">Group membership persistence</span></span>

<span data-ttu-id="4c38c-334">SignalR verfolgt Verbindungen, nicht Benutzer, also wenn Sie möchten, dass sich ein Benutzer jedes Mal `Groups.Add` in derselben Gruppe aufhält, wenn der Benutzer eine Verbindung herstellt, müssen Sie jedes Mal anrufen, wenn der Benutzer eine neue Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="4c38c-335">Nach einem vorübergehenden Verbindungsverlust kann SignalR die Verbindung manchmal automatisch wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="4c38c-336">In diesem Fall stellt SignalR dieselbe Verbindung wieder her, stellt keine neue Verbindung her, sodass die Gruppenmitgliedschaft des Clients automatisch wiederhergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="4c38c-337">Dies ist auch dann möglich, wenn die temporäre Unterbrechung das Ergebnis eines Serverneustarts oder -fehlers ist, da der Verbindungsstatus für jeden Client, einschließlich der Gruppenmitgliedschaften, auf den Client gerundet wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="4c38c-338">Wenn ein Server ausfällt und durch einen neuen Server ersetzt wird, bevor die Verbindung auftritt, kann ein Client automatisch eine Verbindung mit dem neuen Server herstellen und sich erneut in Gruppen registrieren, denen er angehört.</span><span class="sxs-lookup"><span data-stu-id="4c38c-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="4c38c-339">Wenn eine Verbindung nach einem Verbindungsverlust nicht automatisch wiederhergestellt werden kann, wenn die Verbindung unterbrochen wird oder wenn der Client die Verbindung trennt (z. B. wenn ein Browser zu einer neuen Seite navigiert), gehen Gruppenmitgliedschaften verloren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="4c38c-340">Das nächste Mal, wenn der Benutzer eine Verbindung herstellt, wird eine neue Verbindung hergestellt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="4c38c-341">Um Gruppenmitgliedschaften beizubehalten, wenn derselbe Benutzer eine neue Verbindung herstellt, muss Ihre Anwendung die Zuordnungen zwischen Benutzern und Gruppen nachverfolgen und Gruppenmitgliedschaften jedes Mal wiederherstellen, wenn ein Benutzer eine neue Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="4c38c-342">Weitere Informationen zu Verbindungen und Wiederverbindungen finden Sie weiter unten in diesem Thema unter Behandeln von [Verbindungslebensdauerereignissen in der Hub-Klasse.](#connectionlifetime)</span><span class="sxs-lookup"><span data-stu-id="4c38c-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="4c38c-343">Einzelbenutzergruppen</span><span class="sxs-lookup"><span data-stu-id="4c38c-343">Single-user groups</span></span>

<span data-ttu-id="4c38c-344">Anwendungen, die SignalR verwenden, müssen in der Regel die Zuordnungen zwischen Benutzern und Verbindungen nachverfolgen, um zu wissen, welcher Benutzer eine Nachricht gesendet hat und welche Benutzer eine Nachricht empfangen sollen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="4c38c-345">Gruppen werden in einem der beiden häufig verwendeten Muster verwendet, um dies zu tun.</span><span class="sxs-lookup"><span data-stu-id="4c38c-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="4c38c-346">Einzelbenutzergruppen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-346">Single-user groups.</span></span>

    <span data-ttu-id="4c38c-347">Sie können den Benutzernamen als Gruppennamen angeben und der Gruppe jedes Mal die aktuelle Verbindungs-ID hinzufügen, wenn der Benutzer eine Verbindung herstellt oder erneut eine Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="4c38c-348">So senden Sie Nachrichten an den Benutzer, den Sie an die Gruppe senden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="4c38c-349">Ein Nachteil dieser Methode besteht darin, dass die Gruppe Ihnen keine Möglichkeit bietet, herauszufinden, ob der Benutzer online oder offline ist.</span><span class="sxs-lookup"><span data-stu-id="4c38c-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="4c38c-350">Nachverfolgen von Zuordnungen zwischen Benutzernamen und Verbindungs-IDs.</span><span class="sxs-lookup"><span data-stu-id="4c38c-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="4c38c-351">Sie können eine Zuordnung zwischen jedem Benutzernamen und einer oder mehreren Verbindungs-IDs in einem Wörterbuch oder einer Datenbank speichern und die gespeicherten Daten jedes Mal aktualisieren, wenn der Benutzer eine Verbindung herstellt oder die Verbindung trennt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="4c38c-352">Um Nachrichten an den Benutzer zu senden, geben Sie die Verbindungs-IDs an.</span><span class="sxs-lookup"><span data-stu-id="4c38c-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="4c38c-353">Ein Nachteil dieser Methode ist, dass sie mehr Speicher benötigt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="4c38c-354">Behandeln von Verbindungslebensdauerereignissen in der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="4c38c-355">Typische Gründe für die Behandlung von Ereignissen mit der Verbindungslebensdauer sind, nachzuverfolgen, ob ein Benutzer verbunden ist oder nicht, und die Zuordnung zwischen Benutzernamen und Verbindungs-IDs nachzuverfolgen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="4c38c-356">Um Ihren eigenen Code auszuführen, wenn Clients `OnConnected` `OnDisconnected`eine `OnReconnected` Verbindung herstellen oder trennen, überschreiben Sie die , und die virtuellen Methoden der Hub-Klasse, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="4c38c-357">Wenn OnConnected, OnDisconnected und OnReconnected aufgerufen werden</span><span class="sxs-lookup"><span data-stu-id="4c38c-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="4c38c-358">Jedes Mal, wenn ein Browser zu einer neuen Seite navigiert, muss `OnDisconnected` eine neue `OnConnected` Verbindung hergestellt werden, was bedeutet, dass SignalR die Methode nach der Methode ausführt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="4c38c-359">SignalR erstellt immer eine neue Verbindungs-ID, wenn eine neue Verbindung hergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="4c38c-360">Die `OnReconnected` Methode wird aufgerufen, wenn die Verbindung vorübergehend unterbrochen wurde, von der SignalR automatisch wiederhergestellt werden kann, z. B. wenn ein Kabel vorübergehend getrennt und wieder verbunden wird, bevor die Verbindung unterbrochen wird. Die `OnDisconnected` Methode wird aufgerufen, wenn der Client getrennt wird und SignalR die Verbindung nicht automatisch wieder herstellen kann, z. B. wenn ein Browser zu einer neuen Seite navigiert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="4c38c-361">Daher ist `OnConnected`eine mögliche Abfolge von `OnReconnected`Ereignissen `OnDisconnected`für einen bestimmten Client , ; oder `OnConnected` `OnDisconnected`, .</span><span class="sxs-lookup"><span data-stu-id="4c38c-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="4c38c-362">Die Sequenz `OnConnected`, `OnDisconnected` `OnReconnected` wird für eine bestimmte Verbindung nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="4c38c-363">Die `OnDisconnected` Methode wird in einigen Szenarien nicht aufgerufen, z. B. wenn ein Server ausfällt oder die App-Domäne recycelt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="4c38c-364">Wenn ein anderer Server online geht oder die App-Domäne ihre Wiederverwertung abgeschlossen `OnReconnected` hat, können einige Clients möglicherweise die Verbindung wieder herstellen und das Ereignis ausschalten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="4c38c-365">Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="4c38c-366">Anruferstatus nicht bevölkert</span><span class="sxs-lookup"><span data-stu-id="4c38c-366">Caller state not populated</span></span>

<span data-ttu-id="4c38c-367">Die Ereignishandlermethoden für die Verbindungslebensdauer werden vom Server aufgerufen, `state` was bedeutet, dass jeder Status, den Sie in das Objekt auf dem Client setzen, nicht in der `Caller` Eigenschaft auf dem Server aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="4c38c-368">Weitere Informationen `state` zum Objekt `Caller` und zur Eigenschaft finden Sie weiter unten in diesem Thema [unter Übergeben des Status zwischen Clients und der Hub-Klasse.](#passstate)</span><span class="sxs-lookup"><span data-stu-id="4c38c-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="4c38c-369">So erhalten Sie Informationen über den Client aus der Context-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="4c38c-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="4c38c-370">Um Informationen über den Client `Context` abzubekommen, verwenden Sie die Eigenschaft der Hub-Klasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="4c38c-371">Die `Context` Eigenschaft gibt ein [HubCallerContext-Objekt](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) zurück, das Zugriff auf die folgenden Informationen bietet:</span><span class="sxs-lookup"><span data-stu-id="4c38c-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="4c38c-372">Die Verbindungs-ID des aufrufenden Clients.</span><span class="sxs-lookup"><span data-stu-id="4c38c-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="4c38c-373">Die Verbindungs-ID ist eine GUID, die von SignalR zugewiesen wird (Sie können den Wert nicht in Ihrem eigenen Code angeben).</span><span class="sxs-lookup"><span data-stu-id="4c38c-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="4c38c-374">Für jede Verbindung gibt es eine Verbindungs-ID, und die gleiche Verbindungs-ID wird von allen Hubs verwendet, wenn Sie mehrere Hubs in Ihrer Anwendung haben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="4c38c-375">HTTP-Headerdaten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="4c38c-376">Sie können auch HTTP-Header von `Context.Headers`abrufen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="4c38c-377">Der Grund für mehrere Verweise auf `Context.Headers` dasselbe ist, dass zuerst erstellt wurde, die `Context.Request` Eigenschaft wurde später hinzugefügt und `Context.Headers` wurde aus Gründen der Abwärtskompatibilität beibehalten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="4c38c-378">Abfragezeichenfolgendaten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="4c38c-379">Sie können auch Abfragezeichenfolgendaten aus `Context.QueryString`abrufen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="4c38c-380">Die Abfragezeichenfolge, die Sie in dieser Eigenschaft abrufen, ist diejenige, die mit der HTTP-Anforderung verwendet wurde, die die SignalR-Verbindung hergestellt hat.</span><span class="sxs-lookup"><span data-stu-id="4c38c-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="4c38c-381">Sie können Abfragezeichenfolgenparameter im Client hinzufügen, indem Sie die Verbindung konfigurieren, was eine bequeme Möglichkeit ist, Daten über den Client vom Client an den Server zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="4c38c-382">Das folgende Beispiel zeigt eine Möglichkeit zum Hinzufügen einer Abfragezeichenfolge in einem JavaScript-Client, wenn Sie den generierten Proxy verwenden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="4c38c-383">Weitere Informationen zum Festlegen von Abfragezeichenfolgenparametern finden Sie in den API-Leitfäden für die [JavaScript-](hubs-api-guide-javascript-client.md) und [.NET-Clients.](hubs-api-guide-net-client.md)</span><span class="sxs-lookup"><span data-stu-id="4c38c-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="4c38c-384">Sie können die Transportmethode, die für die Verbindung verwendet wird, in den Abfragezeichenfolgendaten sowie einige andere Werte finden, die intern von SignalR verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="4c38c-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="4c38c-385">Der Wert `transportMethod` von ist "webSockets", "serverSentEvents", "foreverFrame" oder "longPolling".</span><span class="sxs-lookup"><span data-stu-id="4c38c-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="4c38c-386">Beachten Sie, dass Sie `OnConnected` bei überprüfung dieses Werts in der Ereignishandlermethode in einigen Szenarien zunächst einen Transportwert erhalten, der nicht die endgültige ausgehandelte Transportmethode für die Verbindung ist.</span><span class="sxs-lookup"><span data-stu-id="4c38c-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="4c38c-387">In diesem Fall löst die Methode eine Ausnahme aus und wird später erneut aufgerufen, wenn die endgültige Transportmethode festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="4c38c-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="4c38c-388">Cookies.</span><span class="sxs-lookup"><span data-stu-id="4c38c-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="4c38c-389">Sie können auch `Context.RequestCookies`Cookies von erhalten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="4c38c-390">Benutzerinformationen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="4c38c-391">Das HttpContext-Objekt für die Anforderung :</span><span class="sxs-lookup"><span data-stu-id="4c38c-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="4c38c-392">Verwenden Sie diese `HttpContext.Current` Methode, `HttpContext` anstatt das Objekt für die SignalR-Verbindung abzusuchen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="4c38c-393">Übergeben des Status zwischen Clients und der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="4c38c-394">Der Clientproxy `state` stellt ein Objekt bereit, in dem Sie Daten speichern können, die mit jedem Methodenaufruf an den Server übertragen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="4c38c-395">Auf dem Server können Sie `Clients.Caller` auf diese Daten in der Eigenschaft in Hub-Methoden zugreifen, die von Clients aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="4c38c-396">Die `Clients.Caller` Eigenschaft wird für die Verbindungslebensdauerereignishandlermethoden `OnConnected`, `OnDisconnected`und `OnReconnected`nicht aufgefüllt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="4c38c-397">Das Erstellen oder `state` Aktualisieren von `Clients.Caller` Daten im Objekt und in der Eigenschaft funktioniert in beide Richtungen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="4c38c-398">Sie können Werte auf dem Server aktualisieren und diese an den Client zurückübergaben.</span><span class="sxs-lookup"><span data-stu-id="4c38c-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="4c38c-399">Das folgende Beispiel zeigt JavaScript-Clientcode, der den Status für die Übertragung an den Server mit jedem Methodenaufruf speichert.</span><span class="sxs-lookup"><span data-stu-id="4c38c-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="4c38c-400">Das folgende Beispiel zeigt den entsprechenden Code in einem .NET-Client.</span><span class="sxs-lookup"><span data-stu-id="4c38c-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="4c38c-401">In Ihrer Hub-Klasse können Sie `Clients.Caller` auf diese Daten in der Eigenschaft zugreifen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="4c38c-402">Das folgende Beispiel zeigt Code, der den im vorherigen Beispiel genannten Status abruft.</span><span class="sxs-lookup"><span data-stu-id="4c38c-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="4c38c-403">Dieser Mechanismus für den persistenten Zustand ist nicht für große `state` Datenmengen vorgesehen, da alles, was Sie in die oder `Clients.Caller` Eigenschaft legen, mit jedem Methodenaufruf rund ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="4c38c-404">Es ist nützlich für kleinere Elemente wie Benutzernamen oder Leistungsindikatoren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="4c38c-405">In VB.NET oder in einem stark typisierten Hub kann auf das `Clients.Caller`Aufruferstatusobjekt nicht über zugegriffen werden. verwenden `Clients.CallerState` (in SignalR 2.1 eingeführt):</span><span class="sxs-lookup"><span data-stu-id="4c38c-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="4c38c-406">**Verwenden von CallerState in C #**</span><span class="sxs-lookup"><span data-stu-id="4c38c-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="4c38c-407">**Verwenden von CallerState in Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="4c38c-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="4c38c-408">Behandeln von Fehlern in der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="4c38c-409">Um Fehler zu behandeln, die in Ihren Hub-Klassenmethoden auftreten, stellen Sie zunächst sicher, dass Sie `await`Ausnahmen von asynchronen Vorgängen (z. B. Aufrufen von Clientmethoden) mithilfe von "beachten".</span><span class="sxs-lookup"><span data-stu-id="4c38c-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="4c38c-410">Verwenden Sie dann eine oder mehrere der folgenden Methoden:</span><span class="sxs-lookup"><span data-stu-id="4c38c-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="4c38c-411">Umschließen Sie den Methodencode in try-catch-Blöcke, und protokollieren Sie das Ausnahmeobjekt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="4c38c-412">Für Debugging-Zwecke können Sie die Ausnahme an den Client senden, aber aus Sicherheitsgründen wird das Senden detaillierter Informationen an Clients in der Produktion nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="4c38c-413">Erstellen Sie ein Hubs-Pipelinemodul, das die [OnIncomingError-Methode](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="4c38c-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="4c38c-414">Das folgende Beispiel zeigt ein Pipelinemodul, das Fehler protokolliert, gefolgt von Code in Startup.cs, der das Modul in die Hubs-Pipeline einfügt.</span><span class="sxs-lookup"><span data-stu-id="4c38c-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="4c38c-415">Verwenden `HubException` Sie die Klasse (eingeführt in SignalR 2).</span><span class="sxs-lookup"><span data-stu-id="4c38c-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="4c38c-416">Dieser Fehler kann von jedem Hubaufruf ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="4c38c-417">Der `HubError` Konstruktor nimmt eine Zeichenfolgennachricht und ein Objekt zum Speichern zusätzlicher Fehlerdaten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="4c38c-418">SignalR serialisiert die Ausnahme automatisch und sendet sie an den Client, wo sie zum Ablehnen oder Faildes des Hub-Methodenaufrufs verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="4c38c-419">Die folgenden Codebeispiele veranschaulichen, wie sie während `HubException` eines Hub-Aufrufs ausgelöst werden und wie die Ausnahme auf JavaScript- und .NET-Clients behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="4c38c-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="4c38c-420">**Servercode zum Demonstrieren der HubException-Klasse**</span><span class="sxs-lookup"><span data-stu-id="4c38c-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="4c38c-421">**JavaScript-Clientcode demonstriert Reaktion auf das Auslösen einer HubException in einem Hub**</span><span class="sxs-lookup"><span data-stu-id="4c38c-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="4c38c-422">**.NET-Clientcode demonstriert Antwort auf das Auslösen einer HubException in einem Hub**</span><span class="sxs-lookup"><span data-stu-id="4c38c-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="4c38c-423">Weitere Informationen zu Hub-Pipelinemodulen finden Sie weiter unten in diesem Thema unter [Anpassen der Hubs-Pipeline.](#hubpipeline)</span><span class="sxs-lookup"><span data-stu-id="4c38c-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="4c38c-424">So aktivieren Sie die Ablaufverfolgung</span><span class="sxs-lookup"><span data-stu-id="4c38c-424">How to enable tracing</span></span>

<span data-ttu-id="4c38c-425">Um die serverseitige Ablaufverfolgung zu aktivieren, fügen Sie der Datei Web.config ein system.diagnostics-Element hinzu, wie in diesem Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="4c38c-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="4c38c-426">Wenn Sie die Anwendung in Visual Studio ausführen, können Sie die Protokolle im **Ausgabefenster** anzeigen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="4c38c-427">Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="4c38c-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="4c38c-428">Um Clientmethoden aus einer anderen Klasse als Ihrer Hub-Klasse aufzurufen, rufen Sie einen Verweis auf das SignalR-Kontextobjekt für den Hub ab, und verwenden Sie diese, um Methoden für den Client oder Verwaltungsgruppen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="4c38c-429">Die folgende `StockTicker` Beispielklasse ruft das Kontextobjekt ab, speichert es in einer Instanz der Klasse, speichert die Klasseninstanz in `updateStockPrice` einer statischen Eigenschaft und verwendet `StockTickerHub`den Kontext aus der singleton-Klasseninstanz, um die Methode auf Clients aufzurufen, die mit einem Hub mit dem Namen verbunden sind.</span><span class="sxs-lookup"><span data-stu-id="4c38c-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="4c38c-430">Wenn Sie den Kontext mehrmals in einem langlebigen Objekt verwenden müssen, erhalten Sie den Verweis einmal und speichern Sie ihn, anstatt ihn jedes Mal wieder zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="4c38c-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="4c38c-431">Durch das einmalige Abrufen des Kontexts wird sichergestellt, dass SignalR Nachrichten in derselben Reihenfolge an Clients sendet, in der Ihre Hubmethoden Clientmethodenaufrufen machen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="4c38c-432">Ein Tutorial zur Verwendung des SignalR-Kontexts für einen Hub finden Sie unter [ServerBroadcast mit ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="4c38c-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="4c38c-433">Aufrufen von Clientmethoden</span><span class="sxs-lookup"><span data-stu-id="4c38c-433">Calling client methods</span></span>

<span data-ttu-id="4c38c-434">Sie können angeben, welche Clients die RPC empfangen sollen, sie haben jedoch weniger Optionen als beim Aufruf von einer Hubklasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="4c38c-435">Der Grund dafür ist, dass der Kontext keinem bestimmten Aufruf von einem Client zugeordnet ist, sodass methoden, die Kenntnisse der aktuellen Verbindungs-ID erfordern, wie z. `Clients.Others`B. oder `Clients.Caller`, oder `Clients.OthersInGroup`, nicht verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="4c38c-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="4c38c-436">Die folgenden Optionen sind verfügbar:</span><span class="sxs-lookup"><span data-stu-id="4c38c-436">The following options are available:</span></span>

- <span data-ttu-id="4c38c-437">Alle verbundenen Clients.</span><span class="sxs-lookup"><span data-stu-id="4c38c-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="4c38c-438">Ein bestimmter Client, der durch die Verbindungs-ID identifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="4c38c-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="4c38c-439">Alle verbundenen Clients mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="4c38c-440">Alle verbundenen Clients in einer angegebenen Gruppe.</span><span class="sxs-lookup"><span data-stu-id="4c38c-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="4c38c-441">Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="4c38c-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="4c38c-442">Wenn Sie ihre Nicht-Hub-Klasse von Methoden in Ihrer Hub-Klasse aufrufen, können `Clients.Client`Sie `Clients.AllExcept`die `Clients.Group` aktuelle `Clients.Caller` `Clients.Others`Verbindungs-ID übergeben und diese mit verwenden, oder , oder , um , oder `Clients.OthersInGroup`zu simulieren.</span><span class="sxs-lookup"><span data-stu-id="4c38c-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="4c38c-443">Im folgenden Beispiel `MoveShapeHub` übergibt die Klasse `Broadcaster` die Verbindungs-ID an die Klasse, damit die `Broadcaster` Klasse simulieren `Clients.Others`kann.</span><span class="sxs-lookup"><span data-stu-id="4c38c-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="4c38c-444">Verwalten der Gruppenmitgliedschaft</span><span class="sxs-lookup"><span data-stu-id="4c38c-444">Managing group membership</span></span>

<span data-ttu-id="4c38c-445">Zum Verwalten von Gruppen haben Sie die gleichen Optionen wie in einer Hub-Klasse.</span><span class="sxs-lookup"><span data-stu-id="4c38c-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="4c38c-446">Hinzufügen eines Clients zu einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="4c38c-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="4c38c-447">Entfernen eines Clients aus einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="4c38c-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="4c38c-448">Anpassen der Hubs-Pipeline</span><span class="sxs-lookup"><span data-stu-id="4c38c-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="4c38c-449">Mit SignalR können Sie Ihren eigenen Code in die Hub-Pipeline einfügen.</span><span class="sxs-lookup"><span data-stu-id="4c38c-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="4c38c-450">Das folgende Beispiel zeigt ein benutzerdefiniertes Hubpipelinemodul, das jeden eingehenden Methodenaufruf protokolliert, der vom Client empfangen wurde, und den ausgehenden Methodenaufruf, der auf dem Client aufgerufen wird:</span><span class="sxs-lookup"><span data-stu-id="4c38c-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="4c38c-451">Der folgende Code in der *Startup.cs-Datei* registriert das Modul, das in der Hub-Pipeline ausgeführt werden soll:</span><span class="sxs-lookup"><span data-stu-id="4c38c-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="4c38c-452">Es gibt viele verschiedene Methoden, die Sie überschreiben können.</span><span class="sxs-lookup"><span data-stu-id="4c38c-452">There are many different methods that you can override.</span></span> <span data-ttu-id="4c38c-453">Eine vollständige Liste finden Sie unter [HubPipelineModule-Methoden](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="4c38c-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
