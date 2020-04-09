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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="93cec-103">webHooks-Handler ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93cec-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="93cec-104">Sobald WebHooks-Anforderungen von einem WebHook-Empfänger überprüft wurden, können sie durch Benutzercode verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="93cec-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="93cec-105">Hier kommen *Handler ins* Spiel.</span><span class="sxs-lookup"><span data-stu-id="93cec-105">This is where *handlers* come in.</span></span> <span data-ttu-id="93cec-106">Handler leiten von der [IWebHookHandler-Schnittstelle](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) ab, verwenden jedoch in der Regel die [WebHookHandler-Klasse,](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) anstatt direkt von der Schnittstelle abzuleiten.</span><span class="sxs-lookup"><span data-stu-id="93cec-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="93cec-107">Eine WebHook-Anforderung kann von einem oder mehreren Handlern verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="93cec-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="93cec-108">Handler werden in der Reihenfolge aufgerufen, die auf ihrer jeweiligen *Order-Eigenschaft* basiert, die von der niedrigsten zum höchsten Wert geht, wobei Order eine einfache ganze Zahl ist (vorgeschlagen, zwischen 1 und 100 zu sein):</span><span class="sxs-lookup"><span data-stu-id="93cec-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook Handler Order-Eigenschaftsdiagramm](_static/Handlers.png)

<span data-ttu-id="93cec-110">Ein Handler kann optional die *Response-Eigenschaft* im WebHookHandlerContext festlegen, was dazu führt, dass die Verarbeitung beendet wird und die Antwort als HTTP-Antwort an den WebHook zurückgesendet wird.</span><span class="sxs-lookup"><span data-stu-id="93cec-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="93cec-111">Im obigen Fall wird Handler C nicht aufgerufen, da er eine höhere Reihenfolge hat, als B und B die Antwort festlegt.</span><span class="sxs-lookup"><span data-stu-id="93cec-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="93cec-112">Das Festlegen der Antwort ist in der Regel nur für WebHooks relevant, bei dem die Antwort Informationen an die ursprüngliche API zurückführen kann.</span><span class="sxs-lookup"><span data-stu-id="93cec-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="93cec-113">Dies ist z. B. bei Slack WebHooks der Fall, bei dem die Antwort an den Kanal zurückgesendet wird, aus dem der WebHook stammt.</span><span class="sxs-lookup"><span data-stu-id="93cec-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="93cec-114">Handler können die Receiver-Eigenschaft festlegen, wenn sie nur WebHooks von diesem bestimmten Empfänger empfangen möchten.</span><span class="sxs-lookup"><span data-stu-id="93cec-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="93cec-115">Wenn sie den Empfänger nicht einstellen, werden sie für alle aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="93cec-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="93cec-116">Eine weitere häufige Verwendung einer Antwort besteht darin, eine *410 Gone-Antwort* zu verwenden, um anzugeben, dass der WebHook nicht mehr aktiv ist und keine weiteren Anforderungen gesendet werden sollten.</span><span class="sxs-lookup"><span data-stu-id="93cec-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="93cec-117">Standardmäßig wird ein Handler von allen WebHook-Empfängern aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="93cec-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="93cec-118">Wenn die *Receiver-Eigenschaft* jedoch auf den Namen eines Handlers festgelegt ist, empfängt dieser Handler nur WebHook-Anforderungen von diesem Empfänger.</span><span class="sxs-lookup"><span data-stu-id="93cec-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="93cec-119">Verarbeiten eines WebHooks</span><span class="sxs-lookup"><span data-stu-id="93cec-119">Processing a WebHook</span></span>

<span data-ttu-id="93cec-120">Wenn ein Handler aufgerufen wird, ruft er einen [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) ab, der Informationen über die WebHook-Anforderung enthält.</span><span class="sxs-lookup"><span data-stu-id="93cec-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="93cec-121">Die Daten, in der Regel der HTTP-Anforderungstext, sind über die *Data-Eigenschaft* verfügbar.</span><span class="sxs-lookup"><span data-stu-id="93cec-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="93cec-122">Der Typ der Daten sind in der Regel JSON- oder HTML-Formulardaten, aber es ist möglich, auf einen spezifischeren Typ zu umsetzen, falls gewünscht.</span><span class="sxs-lookup"><span data-stu-id="93cec-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="93cec-123">Beispielsweise können die benutzerdefinierten WebHooks, die von ASP.NET WebHooks generiert werden, wie folgt in den Typ [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) umgegossen werden:</span><span class="sxs-lookup"><span data-stu-id="93cec-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="93cec-124">Warteschlangenverarbeitung</span><span class="sxs-lookup"><span data-stu-id="93cec-124">Queued Processing</span></span>

<span data-ttu-id="93cec-125">Die meisten WebHook-Absender senden einen WebHook erneut, wenn eine Antwort nicht innerhalb von wenigen Sekunden generiert wird.</span><span class="sxs-lookup"><span data-stu-id="93cec-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="93cec-126">Dies bedeutet, dass der Handler die Verarbeitung innerhalb dieses Zeitrahmens abschließen muss, damit sie nicht erneut aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="93cec-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="93cec-127">Wenn die Verarbeitung länger dauert oder besser separat behandelt wird, kann der [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) verwendet werden, um die WebHook-Anforderung an eine Warteschlange zu senden, z. B. [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span><span class="sxs-lookup"><span data-stu-id="93cec-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="93cec-128">Eine Übersicht über eine [WebHookQueueHandler-Implementierung](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) finden Sie hier:</span><span class="sxs-lookup"><span data-stu-id="93cec-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
