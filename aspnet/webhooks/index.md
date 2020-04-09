---
uid: webhooks/index
title: ASP.NET WebHooks Übersicht | Microsoft Docs
author: rick-anderson
description: Eine Einführung in ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675440"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="6ab88-103">ASP.NET WebHooks im Überblick</span><span class="sxs-lookup"><span data-stu-id="6ab88-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="6ab88-104">WebHooks ist ein einfaches HTTP-Muster, das ein einfaches Pub-/Untermodell zum Verdrahten von Web-APIs und SaaS-Diensten bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="6ab88-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="6ab88-105">Wenn ein Ereignis in einem Dienst auftritt, wird eine Benachrichtigung in Form einer HTTP-POST-Anforderung an registrierte Abonnenten gesendet.</span><span class="sxs-lookup"><span data-stu-id="6ab88-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="6ab88-106">Die POST-Anfrage enthält Informationen über das Ereignis, die es dem Empfänger ermöglichen, entsprechend zu handeln.</span><span class="sxs-lookup"><span data-stu-id="6ab88-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="6ab88-107">Aufgrund ihrer Einfachheit, WebHooks sind bereits von einer großen Anzahl von Diensten wie [Dropbox,](http://dropbox.com/) [GitHub](https://www.github.com/), [Bitbucket,](https://bitbucket.org/) [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/)und viele mehr ausgesetzt.</span><span class="sxs-lookup"><span data-stu-id="6ab88-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="6ab88-108">Ein WebHook kann z. B. angeben, dass sich eine Datei in [Dropbox](http://dropbox.com/)geändert hat oder eine Codeänderung in GitHub festgeschrieben wurde oder eine Zahlung in [PayPal](http://www.paypal.com/)initiiert wurde oder eine Karte in [Trello](http://www.trello.com/)erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="6ab88-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="6ab88-109">Die Möglichkeiten sind endlos!</span><span class="sxs-lookup"><span data-stu-id="6ab88-109">The possibilities are endless!</span></span>

<span data-ttu-id="6ab88-110">Microsoft ASP.NET WebHooks erleichtert das Senden und Empfangen von WebHooks als Teil Ihrer ASP.NET Anwendung:</span><span class="sxs-lookup"><span data-stu-id="6ab88-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="6ab88-111">Auf der empfangenden Seite bietet es ein gemeinsames Modell für den Empfang und die Verarbeitung von WebHooks von einer beliebigen Anzahl von WebHook-Anbietern.</span><span class="sxs-lookup"><span data-stu-id="6ab88-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="6ab88-112">Es kommt aus dem Kasten mit Unterstützung für [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) und [Zendesk,](https://www.zendesk.com/) aber es ist einfach, Unterstützung für mehr hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6ab88-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="6ab88-113">Auf der sendenden Seite bietet es Unterstützung für die Verwaltung und Speicherung von Abonnements sowie für das Senden von Ereignisbenachrichtigungen an die richtige Gruppe von Abonnenten.</span><span class="sxs-lookup"><span data-stu-id="6ab88-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="6ab88-114">Auf diese Weise können Sie Ihre eigenen Ereignisse definieren, die Abonnenten abonnieren können, und sie benachrichtigen, wenn etwas passiert.</span><span class="sxs-lookup"><span data-stu-id="6ab88-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="6ab88-115">Die beiden Teile können je nach Szenario zusammen oder getrennt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6ab88-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="6ab88-116">Wenn Sie nur WebHooks von anderen Diensten empfangen müssen, können Sie nur das Empfängerteil verwenden. Wenn Sie WebHooks nur für andere verfügbar machen möchten, können Sie genau das tun.</span><span class="sxs-lookup"><span data-stu-id="6ab88-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="6ab88-117">Der Code zielt auf ASP.NET Web-API 2 und ASP.NET MVC 5 ab und ist als [OSS auf GitHub](https://github.com/aspnet/WebHooks)verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6ab88-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="6ab88-118">WebHooks Übersicht</span><span class="sxs-lookup"><span data-stu-id="6ab88-118">WebHooks Overview</span></span>

<span data-ttu-id="6ab88-119">WebHooks ist ein Muster, das bedeutet, dass es variiert, wie es von Dienst zu Dienst verwendet wird, aber die Grundidee ist die gleiche.</span><span class="sxs-lookup"><span data-stu-id="6ab88-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="6ab88-120">Sie können sich WebHooks als einfaches Pub-/Untermodell vorstellen, bei dem ein Benutzer Ereignisse abonnieren kann, die an anderer Stelle stattfinden.</span><span class="sxs-lookup"><span data-stu-id="6ab88-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="6ab88-121">Die Ereignisbenachrichtigungen werden als HTTP-POST-Anforderungen weitergegeben, die Informationen über das Ereignis selbst enthalten.</span><span class="sxs-lookup"><span data-stu-id="6ab88-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="6ab88-122">In der Regel enthält die HTTP-POST-Anforderung ein JSON-Objekt oder HTML-Formulardaten, die vom WebHook-Absender bestimmt werden, einschließlich Informationen über das Ereignis, das den WebHook auslösen wird.</span><span class="sxs-lookup"><span data-stu-id="6ab88-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="6ab88-123">Ein WebHook POST-Anforderungstext von [GitHub](https://www.github.com/) sieht z. B. aufgrund eines neuen Problems, das in einem bestimmten Repository geöffnet wird, wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="6ab88-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="6ab88-124">Um sicherzustellen, dass der WebHook tatsächlich vom beabsichtigten Absender stammt, wird die POST-Anforderung in irgendeiner Weise gesichert und dann vom Empfänger überprüft.</span><span class="sxs-lookup"><span data-stu-id="6ab88-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="6ab88-125">[GitHub WebHooks](https://developer.github.com/webhooks/) enthält beispielsweise einen *X-Hub-Signature* HTTP-Header mit einem Hash des Anforderungstexts, der von der Empfängerimplementierung überprüft wird, sodass Sie sich keine Gedanken darüber machen müssen.</span><span class="sxs-lookup"><span data-stu-id="6ab88-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="6ab88-126">Der WebHook-Fluss geht in der Regel in etwa wie folgt:</span><span class="sxs-lookup"><span data-stu-id="6ab88-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="6ab88-127">Der WebHook-Absender macht Ereignisse verfügbar, die ein Client abonnieren kann.</span><span class="sxs-lookup"><span data-stu-id="6ab88-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="6ab88-128">Die Ereignisse beschreiben beobachtbare Änderungen am System, z. B. dass ein neues Datenelement eingefügt wurde, dass ein Prozess abgeschlossen wurde oder etwas anderes.</span><span class="sxs-lookup"><span data-stu-id="6ab88-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="6ab88-129">Der WebHook-Empfänger abonniert sich durch die Registrierung eines WebHook, der aus vier Dingen besteht:</span><span class="sxs-lookup"><span data-stu-id="6ab88-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="6ab88-130">Ein URI für den Ort, an dem die Ereignisbenachrichtigung in Form einer HTTP-POST-Anforderung gebucht werden soll.</span><span class="sxs-lookup"><span data-stu-id="6ab88-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="6ab88-131">Eine Reihe von Filtern, die die einzelnen Ereignisse beschreiben, für die der WebHook ausgelöst werden soll.</span><span class="sxs-lookup"><span data-stu-id="6ab88-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="6ab88-132">Ein geheimer Schlüssel, der zum Signieren der HTTP-POST-Anforderung verwendet wird;</span><span class="sxs-lookup"><span data-stu-id="6ab88-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="6ab88-133">Zusätzliche Daten, die in die HTTP-POST-Anforderung aufgenommen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="6ab88-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="6ab88-134">Dies können z. B. zusätzliche HTTP-Headerfelder oder Eigenschaften sein, die im HTTP POST-Anforderungstext enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="6ab88-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="6ab88-135">Sobald ein Ereignis eintritt, werden die übereinstimmenden WebHook-Registrierungen gefunden und HTTP-POST-Anforderungen gesendet.</span><span class="sxs-lookup"><span data-stu-id="6ab88-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="6ab88-136">In der Regel wird die Generierung der HTTP-POST-Anforderungen mehrmals wiederholt, wenn der Empfänger aus irgendeinem Grund nicht antwortet oder die HTTP-POST-Anforderung zu einer Fehlerantwort führt.</span><span class="sxs-lookup"><span data-stu-id="6ab88-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="6ab88-137">WebHooks-Verarbeitungspipeline</span><span class="sxs-lookup"><span data-stu-id="6ab88-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="6ab88-138">Die Microsoft ASP.NET WebHooks-Verarbeitungspipeline für eingehende WebHooks sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="6ab88-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET WebHooks-Verarbeitungspipeline](_static/WebHookReceivers.png)

<span data-ttu-id="6ab88-140">Die beiden Schlüsselkonzepte sind *Receiver* und *Handler:*</span><span class="sxs-lookup"><span data-stu-id="6ab88-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="6ab88-141">*Receiver* sind für die Verarbeitung der besonderen Variante von WebHook von einem bestimmten Absender und für das Erzwingen von Sicherheitsüberprüfungen verantwortlich, um sicherzustellen, dass die WebHook-Anforderung tatsächlich vom beabsichtigten Absender stammt.</span><span class="sxs-lookup"><span data-stu-id="6ab88-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="6ab88-142">*Handler* sind in der Regel dort, wo Benutzercode ausgeführt wird, der den jeweiligen WebHook verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="6ab88-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="6ab88-143">In den folgenden Knoten werden diese Konzepte ausführlicher beschrieben.</span><span class="sxs-lookup"><span data-stu-id="6ab88-143">In the following nodes these concepts are described in more details.</span></span>
