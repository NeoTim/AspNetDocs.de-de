---
uid: webhooks/diagnostics/logging
title: ASP.NET WebHooks-Protokollierung | Microsoft Docs
author: rick-anderson
description: So protokollieren Sie ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675340"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET WebHooks-Protokollierung

Microsoft ASP.NET WebHooks verwendet Protokollierung als Möglichkeit, Probleme und Probleme zu melden. Standardmäßig werden Protokolle mit [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) geschrieben, wo sie wie jeder andere Protokollstream mit [Trace Listenern](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) verarbeitet werden können.

Bei der Bereitstellung Ihrer Webanwendung als Azure Web App werden die Protokolle automatisch erfasst und können zusammen mit jeder anderen [System.Diagnostics.Trace-Protokollierung](https://msdn.microsoft.com/library/system.diagnostics.trace) verwaltet werden. Weitere Informationen finden Sie unter Aktivieren der [Diagnoseprotokollierung für Web-Apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Darüber hinaus können Protokolle direkt aus Visual Studio abgerufen werden, wie unter [Fehlerbehebung einer Web-App in Azure App Service mit Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)beschrieben.

## <a name="redirecting-logs"></a>Umleiten von Protokollen

Anstatt Protokolle in [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)zu schreiben, ist es möglich, eine alternative Protokollierungsimplementierung bereitzustellen, die sich direkt an einen Protokollmanager wie [Log4Net](http://logging.apache.org/log4net/) und [NLog](http://nlog-project.org/)protokollieren kann. Geben Sie einfach eine Implementierung von [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) und registrieren Sie es mit einer Abhängigkeit Injektion Saum Ihrer Wahl und es wird von Microsoft ASP.NET WebHooks abgeholt werden. Weitere Informationen finden Sie [unter Dependency Injection in ASP.NET Web API 2.](https://www.asp.net/web-api/overview/advanced/dependency-injection)
