---
uid: webhooks/receiving/handlers
title: ASP.NET WebHooks-Handler | Microsoft Docs
author: rick-anderson
description: Behandeln von Anforderungen in ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675220"
---
# <a name="aspnet-webhooks-handlers"></a>webHooks-Handler ASP.NET

Sobald WebHooks-Anforderungen von einem WebHook-Empfänger überprüft wurden, können sie durch Benutzercode verarbeitet werden. Hier kommen *Handler ins* Spiel. Handler leiten von der [IWebHookHandler-Schnittstelle](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) ab, verwenden jedoch in der Regel die [WebHookHandler-Klasse,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) anstatt direkt von der Schnittstelle abzuleiten.

Eine WebHook-Anforderung kann von einem oder mehreren Handlern verarbeitet werden. Handler werden in der Reihenfolge aufgerufen, die auf ihrer jeweiligen *Order-Eigenschaft* basiert, die von der niedrigsten zum höchsten Wert geht, wobei Order eine einfache ganze Zahl ist (vorgeschlagen, zwischen 1 und 100 zu sein):

![WebHook Handler Order-Eigenschaftsdiagramm](_static/Handlers.png)

Ein Handler kann optional die *Response-Eigenschaft* im WebHookHandlerContext festlegen, was dazu führt, dass die Verarbeitung beendet wird und die Antwort als HTTP-Antwort an den WebHook zurückgesendet wird. Im obigen Fall wird Handler C nicht aufgerufen, da er eine höhere Reihenfolge hat, als B und B die Antwort festlegt.

Das Festlegen der Antwort ist in der Regel nur für WebHooks relevant, bei dem die Antwort Informationen an die ursprüngliche API zurückführen kann. Dies ist z. B. bei Slack WebHooks der Fall, bei dem die Antwort an den Kanal zurückgesendet wird, aus dem der WebHook stammt. Handler können die Receiver-Eigenschaft festlegen, wenn sie nur WebHooks von diesem bestimmten Empfänger empfangen möchten. Wenn sie den Empfänger nicht einstellen, werden sie für alle aufgerufen.

Eine weitere häufige Verwendung einer Antwort besteht darin, eine *410 Gone-Antwort* zu verwenden, um anzugeben, dass der WebHook nicht mehr aktiv ist und keine weiteren Anforderungen gesendet werden sollten.

Standardmäßig wird ein Handler von allen WebHook-Empfängern aufgerufen. Wenn die *Receiver-Eigenschaft* jedoch auf den Namen eines Handlers festgelegt ist, empfängt dieser Handler nur WebHook-Anforderungen von diesem Empfänger.

## <a name="processing-a-webhook"></a>Verarbeiten eines WebHooks

Wenn ein Handler aufgerufen wird, ruft er einen [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ab, der Informationen über die WebHook-Anforderung enthält. Die Daten, in der Regel der HTTP-Anforderungstext, sind über die *Data-Eigenschaft* verfügbar.

Der Typ der Daten sind in der Regel JSON- oder HTML-Formulardaten, aber es ist möglich, auf einen spezifischeren Typ zu umsetzen, falls gewünscht. Beispielsweise können die benutzerdefinierten WebHooks, die von ASP.NET WebHooks generiert werden, wie folgt in den Typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) umgegossen werden:

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>Warteschlangenverarbeitung

Die meisten WebHook-Absender senden einen WebHook erneut, wenn eine Antwort nicht innerhalb von wenigen Sekunden generiert wird. Dies bedeutet, dass der Handler die Verarbeitung innerhalb dieses Zeitrahmens abschließen muss, damit sie nicht erneut aufgerufen werden kann.

Wenn die Verarbeitung länger dauert oder besser separat behandelt wird, kann der [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) verwendet werden, um die WebHook-Anforderung an eine Warteschlange zu senden, z. B. [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).

Eine Übersicht über eine [WebHookQueueHandler-Implementierung](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) finden Sie hier:

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
