---
uid: webhooks/diagnostics/logging
title: ASP.NET WebHooks Protokollierung | Microsoft-Dokumentation
author: rick-anderson
description: So führen Sie die Protokollierung in ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 2e86d519c24da102075b4da0a32787c90deb0f6b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061237"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET WebHooks, die Protokollierung

Microsoft ASP.NET WebHooks verwendet Protokollierung als eine Möglichkeit zum Melden von Problemen und Problemen. Standardmäßig werden Protokolle geschrieben, mit ["System.Diagnostics.Trace"](https://msdn.microsoft.com/library/system.diagnostics.trace) verwenden, in dem sie gruppenverwaltete sein können [Ablaufverfolgungslistener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) wie alle anderen Datenstrom.

Wenn Sie Ihre Webanwendung als eine Azure-Web-App bereitstellen, die Protokolle werden automatisch übernommen und verwaltet werden können, zusammen mit anderen ["System.Diagnostics.Trace"](https://msdn.microsoft.com/library/system.diagnostics.trace) Protokollierung. Weitere Informationen finden Sie unter [Aktivieren der diagnoseprotokollierung für Web-apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Darüber hinaus Protokolle erhalten Sie direkt von innerhalb von Visual Studio unter [Problembehandlung bei Web-Apps in Azure App Service mithilfe von Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="redirecting-logs"></a>Umleiten von Protokollen

Anstatt das Schreiben von Protokollen auf ["System.Diagnostics.Trace"](https://msdn.microsoft.com/library/system.diagnostics.trace), es ist möglich, eine alternative protokollierungsimplementierung bereitstellen, die direkt an ein Protokoll-Manager, wie z. B. anmelden können [Log4Net](http://logging.apache.org/log4net/) und [NLog ](http://nlog-project.org/). Geben Sie einfach eine Implementierung von ["ILogger"](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) und registrieren Sie ihn mit einem Dependency Injection-Engine Ihrer Wahl, und es wird von Microsoft ASP.NET WebHooks übernommen zu erhalten. Informieren Sie sich [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) Details.
