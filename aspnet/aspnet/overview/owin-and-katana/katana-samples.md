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
# <a name="katana-samples"></a>Katana-Beispiele

von [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana-Beispiele

**ASP.NET Routen** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
In einigen Anwendungen sollten Sie OWIN-Komponenten im Asp.Net-Routing-Tabelle seite an Seite mit Nicht-OWIN-Komponenten anschließen. In diesem Beispiel wird gezeigt, wie die RouteCollection-Erweiterungsmethoden MapOwinPath und MapOwinRoute verwendet werden, die von Microsoft.Owin.Host.SystemWeb bereitgestellt werden.

**Verzweigen von Pipelines** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN-Anforderungsverarbeitungspipelines müssen nicht linear sein, sie können verzweigt werden, um Anforderungen auf unterschiedliche Weise zu verarbeiten. Dieses Beispiel zeigt, wie eine Verzweigungspipeline basierend auf Anforderungspfaden oder anderen Anforderungsdaten wie Headern erstellt wird. Diese Komponenten sind im Paket Microsoft.Owin.Mapping nuget verfügbar.

**Benutzerdefinierter Server-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
Zeigt, wie sie beim Selbsthosting von OWIN einen benutzerdefinierten OWIN-Server verwenden.

**Eingebetteter** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Einige OWIN-Server können innerhalb Ihres&quot;eigenen Prozesses&quot;ausgeführt werden ( selbst gehostet ). In diesem Beispiel wird gezeigt, wie Sie eine OWIN-Anwendung mit den Tools starten, die vom Microsoft.Owin.Hosting-Nuget-Paket bereitgestellt werden.

**HelloWorld-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN ist eine HTTP-Server-API-Abstraktion, die die Anwendungsportabilität auf verschiedenen Servern ermöglicht. In diesem Beispiel wird veranschaulicht, wie Sie eine Hello World-Anwendung mit einigen **einfachen Wrappern** um die unformatierte OWIN-Abstraktion schreiben und auf einem Webserver wie ASP.NET ausführen.

**Hello World Raw OWIN** | [Beispiel-Quellcode](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
In diesem Beispiel wird veranschaulicht, wie Sie eine Hello World-Anwendung mithilfe der **unformatierten** OWIN-Abstraktion schreiben und auf einem Webserver wie Asp.Net ausführen.

**SignalR-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
Zeigt, wie SignalR mit OWIN / Katana selbst hosten wird. Weitere Informationen zum Selbsthosting von SignalR finden Sie unter [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Static Files Sample** | [Beispielfürst-Quellcode für](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) statische Dateien   
Zeigt, wie HTTP-Anforderungen für statische Dateien mit OWIN / Katana unterstützt werden.

**Web-API-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
In diesem Beispiel wird gezeigt, wie OWIN in IIS hosten und der OWIN-Pipeline eine Web-API hinzugefügt werden.

**Web Socket-Beispiel-Quellcode** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
Zeigt, wie Websockets in OWIN mithilfe der [System.Net.WebSockets.WebSockets.WebSocket-Klasse](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) unterstützt werden.
