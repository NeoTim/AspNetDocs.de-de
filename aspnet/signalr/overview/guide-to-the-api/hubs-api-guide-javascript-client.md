---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API Guide - JavaScript Client | Microsoft Docs
author: bradygaster
description: Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in JavaScript-Clients, z. B. Browsern und Windows Store (WinJS)-Applicat...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675712"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="f915d-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span><span class="sxs-lookup"><span data-stu-id="f915d-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f915d-104">Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in JavaScript-Clients, z. B. Browsern und Windows Store-Anwendungen (WinJS).</span><span class="sxs-lookup"><span data-stu-id="f915d-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="f915d-105">Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen.</span><span class="sxs-lookup"><span data-stu-id="f915d-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="f915d-106">Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f915d-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="f915d-107">Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f915d-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="f915d-108">SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.</span><span class="sxs-lookup"><span data-stu-id="f915d-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="f915d-109">SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections.</span><span class="sxs-lookup"><span data-stu-id="f915d-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="f915d-110">Eine Einführung in SignalR, Hubs und persistente Verbindungen finden Sie unter [Einführung in SignalR](../getting-started/introduction-to-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="f915d-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="f915d-111">In diesem Thema verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="f915d-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="f915d-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f915d-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="f915d-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f915d-113">.NET 4.5</span></span>
> - <span data-ttu-id="f915d-114">SignalR Version 2</span><span class="sxs-lookup"><span data-stu-id="f915d-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="f915d-115">Frühere Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="f915d-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="f915d-116">Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="f915d-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="f915d-117">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="f915d-117">Questions and comments</span></span>
>
> <span data-ttu-id="f915d-118">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="f915d-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="f915d-119">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="f915d-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="f915d-120">Übersicht</span><span class="sxs-lookup"><span data-stu-id="f915d-120">Overview</span></span>

<span data-ttu-id="f915d-121">Dieses Dokument enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="f915d-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="f915d-122">Der generierte Proxy und was er für Sie tut</span><span class="sxs-lookup"><span data-stu-id="f915d-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="f915d-123">Wann der generierte Proxy verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="f915d-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="f915d-124">Client-Setup</span><span class="sxs-lookup"><span data-stu-id="f915d-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="f915d-125">Verweisen auf den dynamisch generierten Proxy</span><span class="sxs-lookup"><span data-stu-id="f915d-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="f915d-126">Erstellen einer physischen Datei für den von SignalR generierten Proxy</span><span class="sxs-lookup"><span data-stu-id="f915d-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="f915d-127">So stellen Sie eine Verbindung her</span><span class="sxs-lookup"><span data-stu-id="f915d-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="f915d-128">".connection.hub" ist das gleiche Objekt, das .hubConnection() erstellt.</span><span class="sxs-lookup"><span data-stu-id="f915d-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="f915d-129">Asynchrone Ausführung der Startmethode</span><span class="sxs-lookup"><span data-stu-id="f915d-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="f915d-130">So stellen Sie eine domänenübergreifende Verbindung her</span><span class="sxs-lookup"><span data-stu-id="f915d-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="f915d-131">So konfigurieren Sie die Verbindung</span><span class="sxs-lookup"><span data-stu-id="f915d-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="f915d-132">Angeben von Abfragezeichenfolgenparametern</span><span class="sxs-lookup"><span data-stu-id="f915d-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="f915d-133">So geben Sie die Transportmethode an</span><span class="sxs-lookup"><span data-stu-id="f915d-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="f915d-134">So erhalten Sie einen Proxy für eine Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="f915d-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="f915d-135">Definieren von Methoden auf dem Client, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="f915d-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="f915d-136">Aufrufen von Servermethoden vom Client</span><span class="sxs-lookup"><span data-stu-id="f915d-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="f915d-137">Behandeln von Verbindungslebensdauerereignissen</span><span class="sxs-lookup"><span data-stu-id="f915d-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="f915d-138">Umgang mit Fehlern</span><span class="sxs-lookup"><span data-stu-id="f915d-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="f915d-139">So aktivieren Sie die clientseitige Protokollierung</span><span class="sxs-lookup"><span data-stu-id="f915d-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="f915d-140">Eine Dokumentation zum Programmieren des Servers oder der .NET-Clients finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="f915d-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="f915d-141">SignalR Hubs API Guide - Server</span><span class="sxs-lookup"><span data-stu-id="f915d-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="f915d-142">SignalR Hubs API-Leitfaden - .NET Client</span><span class="sxs-lookup"><span data-stu-id="f915d-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="f915d-143">Die SignalR 2-Serverkomponente ist nur auf .NET 4.5 verfügbar (obwohl es einen .NET-Client für SignalR 2 auf .NET 4.0 gibt).</span><span class="sxs-lookup"><span data-stu-id="f915d-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="f915d-144">Der generierte Proxy und was er für Sie tut</span><span class="sxs-lookup"><span data-stu-id="f915d-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="f915d-145">Sie können einen JavaScript-Client programmieren, um mit einem SignalR-Dienst mit oder ohne Proxy zu kommunizieren, den SignalR für Sie generiert.</span><span class="sxs-lookup"><span data-stu-id="f915d-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="f915d-146">Der Proxy vereinfacht die Syntax des Codes, den Sie zum Herstellen einer Verbindung verwenden, schreibende Methoden, die der Server aufruft, und Aufrufmethoden auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="f915d-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="f915d-147">Wenn Sie Code zum Aufrufen von Servermethoden schreiben, können Sie mit dem generierten Proxy eine `serverMethod(arg1, arg2)` Syntax `invoke('serverMethod', arg1, arg2)`verwenden, die so aussieht, als würden Sie eine lokale Funktion ausführen: Sie können schreiben statt .</span><span class="sxs-lookup"><span data-stu-id="f915d-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="f915d-148">Die generierte Proxysyntax ermöglicht auch einen sofortigen und verständlichen clientseitigen Fehler, wenn Sie einen Servermethodennamen falsch eingeben.</span><span class="sxs-lookup"><span data-stu-id="f915d-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="f915d-149">Und wenn Sie die Datei, die die Proxys definiert, manuell erstellen, können Sie auch IntelliSense-Unterstützung für das Schreiben von Code erhalten, der Servermethoden aufruft.</span><span class="sxs-lookup"><span data-stu-id="f915d-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="f915d-150">Angenommen, Sie haben die folgende Hub-Klasse auf dem Server:</span><span class="sxs-lookup"><span data-stu-id="f915d-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="f915d-151">Die folgenden Codebeispiele zeigen, wie JavaScript-Code `NewContosoChatMessage` aussieht, um die Methode auf `addContosoChatMessageToPage` dem Server aufzurufen und Aufrufe der Methode vom Server zu empfangen.</span><span class="sxs-lookup"><span data-stu-id="f915d-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="f915d-152">**Mit dem generierten Proxy**</span><span class="sxs-lookup"><span data-stu-id="f915d-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="f915d-153">**Ohne den generierten Proxy**</span><span class="sxs-lookup"><span data-stu-id="f915d-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="f915d-154">Wann der generierte Proxy verwendet werden soll</span><span class="sxs-lookup"><span data-stu-id="f915d-154">When to use the generated proxy</span></span>

<span data-ttu-id="f915d-155">Wenn Sie mehrere Ereignishandler für eine Clientmethode registrieren möchten, die der Server aufruft, können Sie den generierten Proxy nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="f915d-156">Andernfalls können Sie den generierten Proxy verwenden oder nicht basierend auf Ihrer Codierungseinstellung.</span><span class="sxs-lookup"><span data-stu-id="f915d-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="f915d-157">Wenn Sie es nicht verwenden möchten, müssen Sie nicht auf die URL "Signalr/Hubs" in einem `script` Element in Ihrem Clientcode verweisen.</span><span class="sxs-lookup"><span data-stu-id="f915d-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="f915d-158">Clientsetup</span><span class="sxs-lookup"><span data-stu-id="f915d-158">Client setup</span></span>

<span data-ttu-id="f915d-159">Ein JavaScript-Client erfordert Verweise auf jQuery und die SignalR-Kern-JavaScript-Datei.</span><span class="sxs-lookup"><span data-stu-id="f915d-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="f915d-160">Die jQuery-Version muss 1.6.4 oder größere versionen, wie 1.7.2, 1.8.2 oder 1.9.1 sein.</span><span class="sxs-lookup"><span data-stu-id="f915d-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="f915d-161">Wenn Sie sich für die Verwendung des generierten Proxys entscheiden, benötigen Sie auch einen Verweis auf die von SignalR generierte JavaScript-Proxydatei.</span><span class="sxs-lookup"><span data-stu-id="f915d-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="f915d-162">Das folgende Beispiel zeigt, wie die Verweise auf einer HTML-Seite aussehen können, die den generierten Proxy verwendet.</span><span class="sxs-lookup"><span data-stu-id="f915d-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="f915d-163">Diese Verweise müssen in dieser Reihenfolge enthalten sein: jQuery first, SignalR core after, and SignalR proxies last.</span><span class="sxs-lookup"><span data-stu-id="f915d-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="f915d-164">Verweisen auf den dynamisch generierten Proxy</span><span class="sxs-lookup"><span data-stu-id="f915d-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="f915d-165">Im vorherigen Beispiel bezieht sich der Verweis auf den von SignalR generierten Proxy auf dynamisch generierten JavaScript-Code und nicht auf eine physische Datei.</span><span class="sxs-lookup"><span data-stu-id="f915d-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="f915d-166">SignalR erstellt den JavaScript-Code für den Proxy on the fly und stellt ihn dem Client als Antwort auf die URL "/signalr/hubs" zur Last.</span><span class="sxs-lookup"><span data-stu-id="f915d-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="f915d-167">Wenn Sie in Ihrer `MapSignalR` Methode eine andere Basis-URL für SignalR-Verbindungen auf dem Server angegeben haben, ist die URL für die dynamisch generierte Proxydatei Ihre benutzerdefinierte URL mit "/hubs", an die sie angehängt ist.</span><span class="sxs-lookup"><span data-stu-id="f915d-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="f915d-168">Verwenden Sie für Windows 8 (Windows Store)-JavaScript-Clients die physische Proxydatei anstelle der dynamisch generierten.</span><span class="sxs-lookup"><span data-stu-id="f915d-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="f915d-169">Weitere Informationen finden Sie weiter unten in diesem Thema unter [Erstellen einer physischen Datei für den von SignalR generierten Proxy.](#manualproxy)</span><span class="sxs-lookup"><span data-stu-id="f915d-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="f915d-170">Verwenden Sie in einer ASP.NET MVC 4- oder 5-Razor-Ansicht die Tilde, um auf den Anwendungsstamm in Ihrem Proxydateiverweis zu verweisen:</span><span class="sxs-lookup"><span data-stu-id="f915d-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="f915d-171">Weitere Informationen zur Verwendung von SignalR in MVC 5 finden Sie [unter Erste Schritte mit SignalR und MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span><span class="sxs-lookup"><span data-stu-id="f915d-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="f915d-172">Verwenden Sie `Url.Content` in einer ASP.NET MVC 3 Razor-Ansicht für Ihren Proxydateiverweis:</span><span class="sxs-lookup"><span data-stu-id="f915d-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="f915d-173">Verwenden Sie `ResolveClientUrl` in einer ASP.NET Web Forms-Anwendung für den Proxydateiverweis oder registrieren Sie sie über den ScriptManager mithilfe eines relativen App-Stammpfads (beginnend mit einer Tilde):</span><span class="sxs-lookup"><span data-stu-id="f915d-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="f915d-174">Verwenden Sie in der Regel dieselbe Methode zum Angeben der URL "/signalr/hubs", die Sie für CSS- oder JavaScript-Dateien verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="f915d-175">Wenn Sie eine URL ohne Tilde angeben, funktioniert die Anwendung in einigen Szenarien ordnungsgemäß, wenn Sie in Visual Studio mit IIS Express testen, schlägt jedoch mit einem 404-Fehler fehl, wenn Sie bei der Bereitstellung auf vollständigem IIS bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="f915d-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="f915d-176">Weitere Informationen finden Sie unter **Auflösen von Verweisen auf Ressourcen auf Stammebene** [in Webservern in Visual Studio für ASP.NET Webprojekte](https://msdn.microsoft.com/library/58wxa9w5.aspx) auf der MSDN-Website.</span><span class="sxs-lookup"><span data-stu-id="f915d-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="f915d-177">Wenn Sie ein Webprojekt in Visual Studio 2017 im Debugmodus ausführen und Internet Explorer als Browser verwenden, wird die Proxydatei im **Projektmappen-Explorer** unter **Skripts**angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f915d-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="f915d-178">Doppelklicken Sie auf **Hubs**, um den Inhalt der Datei anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f915d-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="f915d-179">Wenn Sie Visual Studio 2012 oder 2013 und Internet Explorer nicht verwenden oder sich nicht im Debugmodus befinden, können Sie den Inhalt der Datei auch abrufen, indem Sie zur URL "/signalR/hubs" navigieren.</span><span class="sxs-lookup"><span data-stu-id="f915d-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="f915d-180">Wenn Ihre Website z. `http://localhost:56699`B. `http://localhost:56699/SignalR/hubs` unter ausgeführt wird, wechseln Sie in Ihrem Browser zu.</span><span class="sxs-lookup"><span data-stu-id="f915d-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="f915d-181">Erstellen einer physischen Datei für den von SignalR generierten Proxy</span><span class="sxs-lookup"><span data-stu-id="f915d-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="f915d-182">Alternativ zum dynamisch generierten Proxy können Sie eine physische Datei mit dem Proxycode erstellen und auf diese Datei verweisen.</span><span class="sxs-lookup"><span data-stu-id="f915d-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="f915d-183">Sie können dies tun, um das Caching- oder Bündelungsverhalten zu steuern oder IntelliSense zu erhalten, wenn Sie Aufrufe von Servermethoden codieren.</span><span class="sxs-lookup"><span data-stu-id="f915d-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="f915d-184">Führen Sie die folgenden Schritte aus, um eine Proxydatei zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="f915d-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="f915d-185">Installieren Sie das [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="f915d-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="f915d-186">Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum *Ordner tools,* der die Datei SignalR.exe enthält.</span><span class="sxs-lookup"><span data-stu-id="f915d-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="f915d-187">Der Werkzeugordner befindet sich an folgendem Speicherort:</span><span class="sxs-lookup"><span data-stu-id="f915d-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="f915d-188">Geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f915d-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="f915d-189">Der Pfad zu Ihrer *DLL* ist in der Regel der *Ordner bin* in Ihrem Projektordner.</span><span class="sxs-lookup"><span data-stu-id="f915d-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="f915d-190">Dieser Befehl erstellt eine Datei mit dem Namen *server.js* im selben Ordner wie *signalr.exe*.</span><span class="sxs-lookup"><span data-stu-id="f915d-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="f915d-191">Legen Sie die Datei *server.js* in einen entsprechenden Ordner in Ihrem Projekt, benennen Sie sie entsprechend Ihrer Anwendung um, und fügen Sie anstelle der Referenz "signalr/hubs" einen Verweis darauf hinzu.</span><span class="sxs-lookup"><span data-stu-id="f915d-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="f915d-192">So stellen Sie eine Verbindung her</span><span class="sxs-lookup"><span data-stu-id="f915d-192">How to establish a connection</span></span>

<span data-ttu-id="f915d-193">Bevor Sie eine Verbindung herstellen können, müssen Sie ein Verbindungsobjekt erstellen, einen Proxy erstellen und Ereignishandler für Methoden registrieren, die vom Server aufgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="f915d-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="f915d-194">Wenn die Proxy- und Ereignishandler eingerichtet sind, `start` stellen Sie die Verbindung her, indem Sie die Methode aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="f915d-195">Wenn Sie den generierten Proxy verwenden, müssen Sie das Verbindungsobjekt nicht in Ihrem eigenen Code erstellen, da der generierte Proxycode dies für Sie tut.</span><span class="sxs-lookup"><span data-stu-id="f915d-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="f915d-196">**Herstellen einer Verbindung (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="f915d-197">**Herstellen einer Verbindung (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="f915d-198">Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen.</span><span class="sxs-lookup"><span data-stu-id="f915d-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="f915d-199">Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="f915d-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="f915d-200">Standardmäßig ist der Hubspeicherort der aktuelle Server. Wenn Sie eine Verbindung zu einem anderen Server `start` herstellen, geben Sie die URL an, bevor Sie die Methode aufrufen, wie im folgenden Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="f915d-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="f915d-201">Normalerweise registrieren Sie Ereignishandler, `start` bevor Sie die Methode aufrufen, um die Verbindung herzustellen.</span><span class="sxs-lookup"><span data-stu-id="f915d-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="f915d-202">Wenn Sie einige Ereignishandler registrieren möchten, nachdem Sie die Verbindung hergestellt haben, können Sie dies tun, `start` aber Sie müssen mindestens einen Ihrer Ereignishandler registrieren, bevor Sie die Methode aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="f915d-203">Ein Grund dafür ist, dass es viele Hubs in einer Anwendung geben `OnConnected` kann, aber Sie möchten das Ereignis nicht auf jedem Hub auslösen, wenn Sie nur für einen von ihnen verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="f915d-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="f915d-204">Wenn die Verbindung hergestellt wird, ist das Vorhandensein einer Clientmethode auf dem `OnConnected` Proxy eines Hubs, was SignalR anweist, das Ereignis auszulösen.</span><span class="sxs-lookup"><span data-stu-id="f915d-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="f915d-205">Wenn Sie vor dem Aufruf der `start` Methode keine Ereignishandler registrieren, können Sie Methoden auf dem `OnConnected` Hub aufrufen, aber die Hub-Methode wird nicht aufgerufen, und es werden keine Clientmethoden vom Server aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="f915d-206">".connection.hub" ist das gleiche Objekt, das .hubConnection() erstellt.</span><span class="sxs-lookup"><span data-stu-id="f915d-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="f915d-207">Wie Sie an den Beispielen sehen können, `$.connection.hub` bezieht sich die Verwendung des generierten Proxys auf das Verbindungsobjekt.</span><span class="sxs-lookup"><span data-stu-id="f915d-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="f915d-208">Dies ist das gleiche Objekt, das Sie beim Aufrufen `$.hubConnection()` erhalten, wenn Sie den generierten Proxy nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="f915d-209">Der generierte Proxycode erstellt die Verbindung für Sie, indem die folgende Anweisung ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="f915d-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![Erstellen einer Verbindung in der generierten Proxydatei](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="f915d-211">Wenn Sie den generierten Proxy verwenden, `$.connection.hub` können Sie alles tun, was Sie mit einem Verbindungsobjekt tun können, wenn Sie den generierten Proxy nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="f915d-212">Asynchrone Ausführung der Startmethode</span><span class="sxs-lookup"><span data-stu-id="f915d-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="f915d-213">Die `start` Methode wird asynchron ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="f915d-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="f915d-214">Es gibt ein [jQuery Deferred-Objekt](http://api.jquery.com/category/deferred-object/)zurück, was bedeutet, dass `pipe` `done`Sie `fail`Rückruffunktionen hinzufügen können, indem Sie Methoden wie , und aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="f915d-215">Wenn Sie Code haben, den Sie ausführen möchten, nachdem die Verbindung hergestellt wurde, z. B. einen Aufruf einer Servermethode, setzen Sie diesen Code in eine Rückruffunktion oder rufen Sie ihn von einer Rückruffunktion auf.</span><span class="sxs-lookup"><span data-stu-id="f915d-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="f915d-216">Die `.done` Rückrufmethode wird ausgeführt, nachdem die Verbindung hergestellt wurde und nachdem `OnConnected` der Code, den Sie in der Ereignishandlermethode auf dem Server haben, die Ausführung abgeschlossen hat.</span><span class="sxs-lookup"><span data-stu-id="f915d-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="f915d-217">Wenn Sie die Anweisung "Jetzt verbunden" aus dem vorherigen Beispiel `start` als nächste Codezeile nach dem Methodenaufruf (nicht in einem `.done` Rückruf) setzen, wird die `console.log` Zeile ausgeführt, bevor die Verbindung hergestellt wird, wie im folgenden Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="f915d-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![Falsche Art und Weise, Code zu schreiben, der ausgeführt wird, nachdem eine Verbindung hergestellt wurde](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="f915d-219">So stellen Sie eine domänenübergreifende Verbindung her</span><span class="sxs-lookup"><span data-stu-id="f915d-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="f915d-220">Wenn der Browser eine `http://contoso.com`Seite aus lädt, befindet sich die `http://contoso.com/signalr`SignalR-Verbindung in derselben Domäne unter .</span><span class="sxs-lookup"><span data-stu-id="f915d-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="f915d-221">Wenn die `http://contoso.com` Seite von `http://fabrikam.com/signalr`eine Verbindung zu herstellt, handelt es sich um eine domänenübergreifende Verbindung.</span><span class="sxs-lookup"><span data-stu-id="f915d-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="f915d-222">Aus Sicherheitsgründen sind domänenübergreifende Verbindungen standardmäßig deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="f915d-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="f915d-223">In SignalR 1.x wurden domänenübergreifende Anforderungen durch ein einzelnes EnableCrossDomain-Flag gesteuert.</span><span class="sxs-lookup"><span data-stu-id="f915d-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="f915d-224">Dieses Flag steuerte sowohl JSONP- als auch CORS-Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="f915d-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="f915d-225">Für eine größere Flexibilität wurde die gesamte CORS-Unterstützung aus der Serverkomponente von SignalR entfernt (JavaScript-Clients verwenden CORS weiterhin normal, wenn festgestellt wird, dass der Browser dies unterstützt), und neue OWIN-Middleware wurde zur Unterstützung dieser Szenarien bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="f915d-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="f915d-226">Wenn JSONP auf dem Client erforderlich ist (zur Unterstützung domänenübergreifender Anforderungen in älteren `EnableJSONP` Browsern), muss es explizit aktiviert werden, indem für das `HubConfiguration` Objekt auf `true`, wie unten gezeigt, festgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="f915d-227">JSONP ist standardmäßig deaktiviert, da es weniger sicher als CORS ist.</span><span class="sxs-lookup"><span data-stu-id="f915d-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="f915d-228">**Hinzufügen von Microsoft.Owin.Cors zu Ihrem Projekt:** Um diese Bibliothek zu installieren, führen Sie den folgenden Befehl in der Package Manager-Konsole aus:</span><span class="sxs-lookup"><span data-stu-id="f915d-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="f915d-229">Mit diesem Befehl wird die Version 2.1.0 des Pakets zu Ihrem Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="f915d-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="f915d-230">Aufrufen von UseCors</span><span class="sxs-lookup"><span data-stu-id="f915d-230">Calling UseCors</span></span>

 <span data-ttu-id="f915d-231">Der folgende Codeausschnitt veranschaulicht, wie domänenübergreifende Verbindungen in SignalR 2 implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="f915d-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="f915d-232">**Implementieren domänenübergreifender Anforderungen in SignalR 2**</span><span class="sxs-lookup"><span data-stu-id="f915d-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="f915d-233">Der folgende Code veranschaulicht, wie CORS oder JSONP in einem SignalR 2-Projekt aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="f915d-234">In diesem `Map` Codebeispiel wird anstelle `RunSignalR` von verwendet, `MapSignalR`sodass die CORS-Middleware nur für die SignalR-Anforderungen `MapSignalR`ausgeführt wird, die CORS-Unterstützung erfordern (und nicht für den gesamten Datenverkehr an dem unter .) angegebenen Pfad. Map kann auch für jede andere Middleware verwendet werden, die für ein bestimmtes URL-Präfix ausgeführt werden muss, und nicht für die gesamte Anwendung.</span><span class="sxs-lookup"><span data-stu-id="f915d-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="f915d-235">Legen Sie `jQuery.support.cors` in Ihrem Code nicht auf true fest.</span><span class="sxs-lookup"><span data-stu-id="f915d-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![Setzen Sie jQuery.support.cors nicht auf true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="f915d-237">SignalR übernimmt die Verwendung von CORS.</span><span class="sxs-lookup"><span data-stu-id="f915d-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="f915d-238">Das `jQuery.support.cors` Festlegen auf true deaktiviert JSONP, da Es dazu führt, dass SignalR davon ausgeht, dass der Browser CORS unterstützt.</span><span class="sxs-lookup"><span data-stu-id="f915d-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="f915d-239">Wenn Sie eine Verbindung mit einer lokalen Host-URL herstellen, betrachtet Internet Explorer 10 dies nicht als domänenübergreifende Verbindung, sodass die Anwendung lokal mit IE 10 arbeitet, auch wenn Sie keine domänenübergreifenden Verbindungen auf dem Server aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="f915d-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="f915d-240">Informationen zur Verwendung domänenübergreifender Verbindungen mit Internet Explorer 9 finden Sie in [diesem StackOverflow-Thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span><span class="sxs-lookup"><span data-stu-id="f915d-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="f915d-241">Informationen zur Verwendung domänenübergreifender Verbindungen mit Chrome finden Sie in [diesem StackOverflow-Thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span><span class="sxs-lookup"><span data-stu-id="f915d-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="f915d-242">Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen.</span><span class="sxs-lookup"><span data-stu-id="f915d-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="f915d-243">Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="f915d-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="f915d-244">So konfigurieren Sie die Verbindung</span><span class="sxs-lookup"><span data-stu-id="f915d-244">How to configure the connection</span></span>

<span data-ttu-id="f915d-245">Bevor Sie eine Verbindung herstellen, können Sie Abfragezeichenfolgenparameter oder die Transportmethode angeben.</span><span class="sxs-lookup"><span data-stu-id="f915d-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="f915d-246">Angeben von Abfragezeichenfolgenparametern</span><span class="sxs-lookup"><span data-stu-id="f915d-246">How to specify query string parameters</span></span>

<span data-ttu-id="f915d-247">Wenn Sie Daten an den Server senden möchten, wenn der Client eine Verbindung herstellt, können Sie dem Verbindungsobjekt Abfragezeichenfolgenparameter hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f915d-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="f915d-248">Die folgenden Beispiele zeigen, wie Sie einen Abfragezeichenfolgenparameter im Clientcode festlegen.</span><span class="sxs-lookup"><span data-stu-id="f915d-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="f915d-249">**Festlegen eines Abfragezeichenfolgenwerts vor dem Aufruf der Startmethode (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="f915d-250">**Festlegen eines Abfragezeichenfolgenwerts vor dem Aufruf der startmethode (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="f915d-251">Das folgende Beispiel zeigt, wie sie einen Abfragezeichenfolgenparameter im Servercode lesen.</span><span class="sxs-lookup"><span data-stu-id="f915d-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="f915d-252">So geben Sie die Transportmethode an</span><span class="sxs-lookup"><span data-stu-id="f915d-252">How to specify the transport method</span></span>

<span data-ttu-id="f915d-253">Im Rahmen der Verbindung verhandelt ein SignalR-Client normalerweise mit dem Server, um den besten Transport zu ermitteln, der sowohl vom Server als auch vom Client unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="f915d-254">Wenn Sie bereits wissen, welchen Transport Sie verwenden möchten, können Sie diesen Aushandlungsprozess umgehen, indem Sie die Transportmethode angeben, wenn Sie die `start` Methode aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="f915d-255">**Clientcode, der die Transportmethode angibt (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="f915d-256">**Clientcode, der die Transportmethode angibt (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="f915d-257">Alternativ können Sie mehrere Transportmethoden in der Reihenfolge angeben, in der SignalR sie ausprobieren soll:</span><span class="sxs-lookup"><span data-stu-id="f915d-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="f915d-258">**Clientcode, der ein benutzerdefiniertes Transport-Fallbackschema angibt (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="f915d-259">**Clientcode, der ein benutzerdefiniertes Transport-Fallbackschema angibt (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="f915d-260">Sie können die folgenden Werte verwenden, um die Transportmethode anzugeben:</span><span class="sxs-lookup"><span data-stu-id="f915d-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="f915d-261">"webSockets"</span><span class="sxs-lookup"><span data-stu-id="f915d-261">"webSockets"</span></span>
- <span data-ttu-id="f915d-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="f915d-262">"foreverFrame"</span></span>
- <span data-ttu-id="f915d-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="f915d-263">"serverSentEvents"</span></span>
- <span data-ttu-id="f915d-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="f915d-264">"longPolling"</span></span>

<span data-ttu-id="f915d-265">Die folgenden Beispiele zeigen, wie Sie herausfinden, welche Transportmethode von einer Verbindung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="f915d-266">**Clientcode, der die Transportmethode anzeigt, die von einer Verbindung (mit dem generierten Proxy) verwendet wird**</span><span class="sxs-lookup"><span data-stu-id="f915d-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="f915d-267">**Clientcode, der die transportische Methode anzeigt, die von einer Verbindung verwendet wird (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="f915d-268">Informationen zum Überprüfen der Transportmethode im Servercode finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context-Eigenschaft](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="f915d-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="f915d-269">Weitere Informationen zu Transporten und Fallbacks finden Sie unter [Einführung in SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="f915d-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="f915d-270">So erhalten Sie einen Proxy für eine Hub-Klasse</span><span class="sxs-lookup"><span data-stu-id="f915d-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="f915d-271">Jedes Verbindungsobjekt, das Sie erstellen, kapselt Informationen über eine Verbindung mit einem SignalR-Dienst, der eine oder mehrere Hubklassen enthält.</span><span class="sxs-lookup"><span data-stu-id="f915d-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="f915d-272">Um mit einer Hub-Klasse zu kommunizieren, verwenden Sie ein Proxyobjekt, das Sie selbst erstellen (wenn Sie den generierten Proxy nicht verwenden) oder das für Sie generiert wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="f915d-273">Auf dem Client ist der Proxyname eine Kamel-Case-Version des Hub-Klassennamens.</span><span class="sxs-lookup"><span data-stu-id="f915d-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="f915d-274">SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.</span><span class="sxs-lookup"><span data-stu-id="f915d-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="f915d-275">**Hub-Klasse auf dem Server**</span><span class="sxs-lookup"><span data-stu-id="f915d-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="f915d-276">**Abrufen eines Verweises auf den generierten Clientproxy für den Hub**</span><span class="sxs-lookup"><span data-stu-id="f915d-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="f915d-277">**Erstellen eines Clientproxys für die Hub-Klasse (ohne generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="f915d-278">Wenn Sie Ihre Hub-Klasse `HubName` mit einem Attribut dekorieren, verwenden Sie den genauen Namen, ohne die Groß-/Kleinschreibung zu ändern.</span><span class="sxs-lookup"><span data-stu-id="f915d-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="f915d-279">**Hub-Klasse auf dem Server mit HubName-Attribut**</span><span class="sxs-lookup"><span data-stu-id="f915d-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="f915d-280">**Abrufen eines Verweises auf den generierten Clientproxy für den Hub**</span><span class="sxs-lookup"><span data-stu-id="f915d-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="f915d-281">**Erstellen eines Clientproxys für die Hub-Klasse (ohne generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="f915d-282">Definieren von Methoden auf dem Client, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="f915d-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="f915d-283">Um eine Methode zu definieren, die der Server von einem Hub aufrufen `client` kann, fügen Sie dem `on` Hub-Proxy mithilfe der Eigenschaft des generierten Proxys einen Ereignishandler hinzu, oder rufen Sie die Methode auf, wenn Sie den generierten Proxy nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="f915d-284">Bei den Parametern kann es sich um komplexe Objekte handelt.</span><span class="sxs-lookup"><span data-stu-id="f915d-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="f915d-285">Fügen Sie den Ereignishandler `start` hinzu, bevor Sie die Methode zum Herstellen der Verbindung aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="f915d-286">(Wenn Sie nach dem Aufruf der `start` Methode Ereignishandler hinzufügen möchten, lesen Sie die Anmerkung unter [Herstellen einer Verbindung](#establishconnection) weiter oben in diesem Dokument, und verwenden Sie die Syntax zum Definieren einer Methode, ohne den generierten Proxy zu verwenden.)</span><span class="sxs-lookup"><span data-stu-id="f915d-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="f915d-287">Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="f915d-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="f915d-288">Auf dem `Clients.All.addContosoChatMessageToPage` Server wird `AddContosoChatMessageToPage`z. B. ausgeführt , `addContosoChatMessageToPage`, oder `addcontosochatmessagetopage` auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="f915d-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="f915d-289">**Definieren der Methode auf dem Client (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="f915d-290">**Alternative Methode auf Client (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="f915d-291">**Definieren der Methode auf dem Client (ohne den generierten Proxy oder beim Hinzufügen nach dem Aufrufen der Startmethode)**</span><span class="sxs-lookup"><span data-stu-id="f915d-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="f915d-292">**Servercode, der die Clientmethode aufruft**</span><span class="sxs-lookup"><span data-stu-id="f915d-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="f915d-293">Die folgenden Beispiele enthalten ein komplexes Objekt als Methodenparameter.</span><span class="sxs-lookup"><span data-stu-id="f915d-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="f915d-294">**Definieren einer Methode auf dem Client, die ein komplexes Objekt (mit dem generierten Proxy) übernimmt**</span><span class="sxs-lookup"><span data-stu-id="f915d-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="f915d-295">**Definieren einer Methode auf dem Client, die ein komplexes Objekt übernimmt (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="f915d-296">**Servercode, der das komplexe Objekt definiert**</span><span class="sxs-lookup"><span data-stu-id="f915d-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="f915d-297">**Servercode, der die Clientmethode mithilfe eines komplexen Objekts aufruft**</span><span class="sxs-lookup"><span data-stu-id="f915d-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="f915d-298">Aufrufen von Servermethoden vom Client</span><span class="sxs-lookup"><span data-stu-id="f915d-298">How to call server methods from the client</span></span>

<span data-ttu-id="f915d-299">Um eine Servermethode vom Client `server` aufzurufen, verwenden Sie `invoke` die Eigenschaft des generierten Proxys oder die Methode auf dem Hub-Proxy, wenn Sie den generierten Proxy nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f915d-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="f915d-300">Der Rückgabewert oder die Parameter können komplexe Objekte sein.</span><span class="sxs-lookup"><span data-stu-id="f915d-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="f915d-301">Übergeben Sie eine Kamel-Fall-Version des Methodennamens auf dem Hub.</span><span class="sxs-lookup"><span data-stu-id="f915d-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="f915d-302">SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.</span><span class="sxs-lookup"><span data-stu-id="f915d-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="f915d-303">Die folgenden Beispiele zeigen, wie eine Servermethode aufrufen wird, die keinen Rückgabewert hat, und wie eine Servermethode aufruft, die über einen Rückgabewert verfügt.</span><span class="sxs-lookup"><span data-stu-id="f915d-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="f915d-304">**Servermethode ohne HubMethodName-Attribut**</span><span class="sxs-lookup"><span data-stu-id="f915d-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="f915d-305">**Servercode, der das komplexe Objekt definiert, das in einem Parameter übergeben wird**</span><span class="sxs-lookup"><span data-stu-id="f915d-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="f915d-306">**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="f915d-307">**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="f915d-308">Wenn Sie die Hub-Methode mit einem `HubMethodName` Attribut versehen haben, verwenden Sie diesen Namen, ohne die Groß-/Kleinschreibung zu ändern.</span><span class="sxs-lookup"><span data-stu-id="f915d-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="f915d-309">**Servermethode** mit einem HubMethodName-Attribut</span><span class="sxs-lookup"><span data-stu-id="f915d-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="f915d-310">**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="f915d-311">**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="f915d-312">Die vorherigen Beispiele zeigen, wie eine Servermethode ohne Rückgabewert aufzurufen ist.</span><span class="sxs-lookup"><span data-stu-id="f915d-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="f915d-313">Die folgenden Beispiele zeigen, wie eine Servermethode mit einem Rückgabewert aufruft.</span><span class="sxs-lookup"><span data-stu-id="f915d-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="f915d-314">**Servercode für eine Methode mit einem Rückgabewert**</span><span class="sxs-lookup"><span data-stu-id="f915d-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="f915d-315">Die Für den Rückgabewert **verwendete Stock-Klasse**</span><span class="sxs-lookup"><span data-stu-id="f915d-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="f915d-316">**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="f915d-317">**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="f915d-318">Behandeln von Verbindungslebensdauerereignissen</span><span class="sxs-lookup"><span data-stu-id="f915d-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="f915d-319">SignalR stellt die folgenden Verbindungslebensdauerereignisse bereit, die Sie verarbeiten können:</span><span class="sxs-lookup"><span data-stu-id="f915d-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="f915d-320">`starting`: Wird ausgelöst, bevor Daten über die Verbindung gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="f915d-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="f915d-321">`received`: Wird ausgelöst, wenn Daten über die Verbindung empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="f915d-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="f915d-322">Stellt die empfangenen Daten bereit.</span><span class="sxs-lookup"><span data-stu-id="f915d-322">Provides the received data.</span></span>
- <span data-ttu-id="f915d-323">`connectionSlow`: Wird ausgelöst, wenn der Client eine langsame oder häufig abbrechende Verbindung erkennt.</span><span class="sxs-lookup"><span data-stu-id="f915d-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="f915d-324">`reconnecting`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="f915d-325">`reconnected`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="f915d-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="f915d-326">`stateChanged`: Wird ausgelöst, wenn sich der Verbindungsstatus ändert.</span><span class="sxs-lookup"><span data-stu-id="f915d-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="f915d-327">Stellt den alten und den neuen Status bereit (Verbinden, Verbinden, Erneute Verbindung oder Getrennt).</span><span class="sxs-lookup"><span data-stu-id="f915d-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="f915d-328">`disconnected`: Wird ausgelöst, wenn die Verbindung getrennt wurde.</span><span class="sxs-lookup"><span data-stu-id="f915d-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="f915d-329">Wenn Sie z. B. Warnmeldungen anzeigen möchten, wenn Verbindungsprobleme `connectionSlow` auftreten, die zu spürbaren Verzögerungen führen können, behandeln Sie das Ereignis.</span><span class="sxs-lookup"><span data-stu-id="f915d-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="f915d-330">**Behandeln des connectionSlow-Ereignisses (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="f915d-331">**Behandeln des connectionSlow-Ereignisses (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="f915d-332">Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="f915d-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="f915d-333">Umgang mit Fehlern</span><span class="sxs-lookup"><span data-stu-id="f915d-333">How to handle errors</span></span>

<span data-ttu-id="f915d-334">Der SignalR JavaScript-Client stellt ein `error` Ereignis bereit, für das Sie einen Handler hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="f915d-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="f915d-335">Sie können die fail-Methode auch verwenden, um einen Handler für Fehler hinzuzufügen, die aus einem Servermethodenaufruf resultieren.</span><span class="sxs-lookup"><span data-stu-id="f915d-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="f915d-336">Wenn Sie detaillierte Fehlermeldungen auf dem Server nicht explizit aktivieren, enthält das Ausnahmeobjekt, das SignalR nach einem Fehler zurückgibt, minimale Informationen über den Fehler.</span><span class="sxs-lookup"><span data-stu-id="f915d-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="f915d-337">Wenn z. B. `newContosoChatMessage` ein Aufruf von fehlschlägt,`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`enthält die Fehlermeldung im Fehlerobjekt " " Das Senden detaillierter Fehlermeldungen an Clients in der Produktion wird aus Sicherheitsgründen nicht empfohlen, aber wenn Sie detaillierte Fehlermeldungen zur Fehlerbehebung aktivieren möchten, verwenden Sie den folgenden Code auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="f915d-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="f915d-338">Das folgende Beispiel zeigt, wie Sie einen Handler für das Fehlerereignis hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f915d-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="f915d-339">**Hinzufügen eines Fehlerhandlers (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="f915d-340">**Hinzufügen eines Fehlerhandlers (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="f915d-341">Das folgende Beispiel zeigt, wie ein Fehler aus einem Methodenaufruf behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="f915d-342">**Behandeln eines Fehlers von einem Methodenaufruf (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="f915d-343">**Behandeln eines Fehlers von einem Methodenaufruf (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="f915d-344">Wenn ein Methodenaufruf fehlschlägt, wird das `error` Ereignis ebenfalls `error` ausgelöst, sodass der Code im Methodenhandler und im `.fail` Methodenrückruf ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f915d-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="f915d-345">So aktivieren Sie die clientseitige Protokollierung</span><span class="sxs-lookup"><span data-stu-id="f915d-345">How to enable client-side logging</span></span>

<span data-ttu-id="f915d-346">Um die clientseitige Protokollierung für `logging` eine Verbindung zu aktivieren, `start` legen Sie die Eigenschaft für das Verbindungsobjekt fest, bevor Sie die Methode zum Herstellen der Verbindung aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f915d-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="f915d-347">**Protokollierung aktivieren (mit dem generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="f915d-348">**Protokollierung aktivieren (ohne den generierten Proxy)**</span><span class="sxs-lookup"><span data-stu-id="f915d-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="f915d-349">Um die Protokolle anzuzeigen, öffnen Sie die Entwicklertools Ihres Browsers, und wechseln Sie zur Registerkarte Konsole. Ein Tutorial mit Schritt-für-Schritt-Anleitungen und Screenshots, die zeigen, wie Sie dies tun, finden Sie unter [ServerBroadcast mit ASP.NET Signalr - Anmelden aktivieren](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span><span class="sxs-lookup"><span data-stu-id="f915d-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
