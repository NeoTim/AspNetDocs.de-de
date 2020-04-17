---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana Proben | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540440"
---
# <a name="katana-samples"></a><span data-ttu-id="c53c0-102">Katana-Beispiele</span><span class="sxs-lookup"><span data-stu-id="c53c0-102">Katana Samples</span></span>

<span data-ttu-id="c53c0-103">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c53c0-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="c53c0-104">Katana-Beispiele</span><span class="sxs-lookup"><span data-stu-id="c53c0-104">Katana Samples</span></span>

<span data-ttu-id="c53c0-105">**ASP.NET Routen** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="c53c0-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="c53c0-106">In einigen Anwendungen sollten Sie OWIN-Komponenten im Asp.Net-Routing-Tabelle seite an Seite mit Nicht-OWIN-Komponenten anschließen.</span><span class="sxs-lookup"><span data-stu-id="c53c0-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="c53c0-107">In diesem Beispiel wird gezeigt, wie die RouteCollection-Erweiterungsmethoden MapOwinPath und MapOwinRoute verwendet werden, die von Microsoft.Owin.Host.SystemWeb bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="c53c0-108">**Verzweigen von Pipelines** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="c53c0-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="c53c0-109">OWIN-Anforderungsverarbeitungspipelines müssen nicht linear sein, sie können verzweigt werden, um Anforderungen auf unterschiedliche Weise zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="c53c0-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="c53c0-110">Dieses Beispiel zeigt, wie eine Verzweigungspipeline basierend auf Anforderungspfaden oder anderen Anforderungsdaten wie Headern erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c53c0-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="c53c0-111">Diese Komponenten sind im Paket Microsoft.Owin.Mapping nuget verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c53c0-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="c53c0-112">**Benutzerdefinierter Server-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="c53c0-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="c53c0-113">Zeigt, wie sie beim Selbsthosting von OWIN einen benutzerdefinierten OWIN-Server verwenden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="c53c0-114">**Eingebetteter** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="c53c0-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="c53c0-115">Einige OWIN-Server können innerhalb Ihres&quot;eigenen Prozesses&quot;ausgeführt werden ( selbst gehostet ).</span><span class="sxs-lookup"><span data-stu-id="c53c0-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="c53c0-116">In diesem Beispiel wird gezeigt, wie Sie eine OWIN-Anwendung mit den Tools starten, die vom Microsoft.Owin.Hosting-Nuget-Paket bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="c53c0-117">**HelloWorld-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="c53c0-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="c53c0-118">OWIN ist eine HTTP-Server-API-Abstraktion, die die Anwendungsportabilität auf verschiedenen Servern ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="c53c0-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="c53c0-119">In diesem Beispiel wird veranschaulicht, wie Sie eine Hello World-Anwendung mit einigen **einfachen Wrappern** um die unformatierte OWIN-Abstraktion schreiben und auf einem Webserver wie ASP.NET ausführen.</span><span class="sxs-lookup"><span data-stu-id="c53c0-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="c53c0-120">**Hello World Raw OWIN** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="c53c0-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="c53c0-121">In diesem Beispiel wird veranschaulicht, wie Sie eine Hello World-Anwendung mithilfe der **unformatierten** OWIN-Abstraktion schreiben und auf einem Webserver wie Asp.Net ausführen.</span><span class="sxs-lookup"><span data-stu-id="c53c0-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="c53c0-122">**SignalR-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="c53c0-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="c53c0-123">Zeigt, wie SignalR mit OWIN / Katana selbst hosten wird.</span><span class="sxs-lookup"><span data-stu-id="c53c0-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="c53c0-124">Weitere Informationen zum Selbsthosting von SignalR finden Sie unter [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="c53c0-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="c53c0-125">**Static Files Sample** | [Beispielfürst-Quellcode für](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) statische Dateien </span><span class="sxs-lookup"><span data-stu-id="c53c0-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="c53c0-126">Zeigt, wie HTTP-Anforderungen für statische Dateien mit OWIN / Katana unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="c53c0-127">**Web-API-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="c53c0-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="c53c0-128">In diesem Beispiel wird gezeigt, wie OWIN in IIS hosten und der OWIN-Pipeline eine Web-API hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="c53c0-129">**Web Socket-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="c53c0-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="c53c0-130">Zeigt, wie Websockets in OWIN mithilfe der [System.Net.WebSockets.WebSockets.WebSocket-Klasse](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="c53c0-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
