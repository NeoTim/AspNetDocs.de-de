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
# <a name="aspnet-webhooks-overview"></a>ASP.NET WebHooks im Überblick

WebHooks ist ein einfaches HTTP-Muster, das ein einfaches Pub-/Untermodell zum Verdrahten von Web-APIs und SaaS-Diensten bereitstellt. Wenn ein Ereignis in einem Dienst auftritt, wird eine Benachrichtigung in Form einer HTTP-POST-Anforderung an registrierte Abonnenten gesendet. Die POST-Anfrage enthält Informationen über das Ereignis, die es dem Empfänger ermöglichen, entsprechend zu handeln.

Aufgrund ihrer Einfachheit, WebHooks sind bereits von einer großen Anzahl von Diensten wie [Dropbox,](http://dropbox.com/) [GitHub](https://www.github.com/), [Bitbucket,](https://bitbucket.org/) [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/)und viele mehr ausgesetzt. Ein WebHook kann z. B. angeben, dass sich eine Datei in [Dropbox](http://dropbox.com/)geändert hat oder eine Codeänderung in GitHub festgeschrieben wurde oder eine Zahlung in [PayPal](http://www.paypal.com/)initiiert wurde oder eine Karte in [Trello](http://www.trello.com/)erstellt wurde. Die Möglichkeiten sind endlos!

Microsoft ASP.NET WebHooks erleichtert das Senden und Empfangen von WebHooks als Teil Ihrer ASP.NET Anwendung:

* Auf der empfangenden Seite bietet es ein gemeinsames Modell für den Empfang und die Verarbeitung von WebHooks von einer beliebigen Anzahl von WebHook-Anbietern. Es kommt aus dem Kasten mit Unterstützung für [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) und [Zendesk,](https://www.zendesk.com/) aber es ist einfach, Unterstützung für mehr hinzuzufügen.

* Auf der sendenden Seite bietet es Unterstützung für die Verwaltung und Speicherung von Abonnements sowie für das Senden von Ereignisbenachrichtigungen an die richtige Gruppe von Abonnenten. Auf diese Weise können Sie Ihre eigenen Ereignisse definieren, die Abonnenten abonnieren können, und sie benachrichtigen, wenn etwas passiert.

Die beiden Teile können je nach Szenario zusammen oder getrennt verwendet werden. Wenn Sie nur WebHooks von anderen Diensten empfangen müssen, können Sie nur das Empfängerteil verwenden. Wenn Sie WebHooks nur für andere verfügbar machen möchten, können Sie genau das tun.

Der Code zielt auf ASP.NET Web-API 2 und ASP.NET MVC 5 ab und ist als [OSS auf GitHub](https://github.com/aspnet/WebHooks)verfügbar.

## <a name="webhooks-overview"></a>WebHooks Übersicht

WebHooks ist ein Muster, das bedeutet, dass es variiert, wie es von Dienst zu Dienst verwendet wird, aber die Grundidee ist die gleiche. Sie können sich WebHooks als einfaches Pub-/Untermodell vorstellen, bei dem ein Benutzer Ereignisse abonnieren kann, die an anderer Stelle stattfinden. Die Ereignisbenachrichtigungen werden als HTTP-POST-Anforderungen weitergegeben, die Informationen über das Ereignis selbst enthalten.

In der Regel enthält die HTTP-POST-Anforderung ein JSON-Objekt oder HTML-Formulardaten, die vom WebHook-Absender bestimmt werden, einschließlich Informationen über das Ereignis, das den WebHook auslösen wird. Ein WebHook POST-Anforderungstext von [GitHub](https://www.github.com/) sieht z. B. aufgrund eines neuen Problems, das in einem bestimmten Repository geöffnet wird, wie folgt aus:

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

Um sicherzustellen, dass der WebHook tatsächlich vom beabsichtigten Absender stammt, wird die POST-Anforderung in irgendeiner Weise gesichert und dann vom Empfänger überprüft. [GitHub WebHooks](https://developer.github.com/webhooks/) enthält beispielsweise einen *X-Hub-Signature* HTTP-Header mit einem Hash des Anforderungstexts, der von der Empfängerimplementierung überprüft wird, sodass Sie sich keine Gedanken darüber machen müssen.

Der WebHook-Fluss geht in der Regel in etwa wie folgt:

* Der WebHook-Absender macht Ereignisse verfügbar, die ein Client abonnieren kann. Die Ereignisse beschreiben beobachtbare Änderungen am System, z. B. dass ein neues Datenelement eingefügt wurde, dass ein Prozess abgeschlossen wurde oder etwas anderes.

* Der WebHook-Empfänger abonniert sich durch die Registrierung eines WebHook, der aus vier Dingen besteht:

     1. Ein URI für den Ort, an dem die Ereignisbenachrichtigung in Form einer HTTP-POST-Anforderung gebucht werden soll.

     2. Eine Reihe von Filtern, die die einzelnen Ereignisse beschreiben, für die der WebHook ausgelöst werden soll.

     3. Ein geheimer Schlüssel, der zum Signieren der HTTP-POST-Anforderung verwendet wird;

     4. Zusätzliche Daten, die in die HTTP-POST-Anforderung aufgenommen werden sollen. Dies können z. B. zusätzliche HTTP-Headerfelder oder Eigenschaften sein, die im HTTP POST-Anforderungstext enthalten sind.

* Sobald ein Ereignis eintritt, werden die übereinstimmenden WebHook-Registrierungen gefunden und HTTP-POST-Anforderungen gesendet. In der Regel wird die Generierung der HTTP-POST-Anforderungen mehrmals wiederholt, wenn der Empfänger aus irgendeinem Grund nicht antwortet oder die HTTP-POST-Anforderung zu einer Fehlerantwort führt.

## <a name="webhooks-processing-pipeline"></a>WebHooks-Verarbeitungspipeline

Die Microsoft ASP.NET WebHooks-Verarbeitungspipeline für eingehende WebHooks sieht wie folgt aus:

![ASP.NET WebHooks-Verarbeitungspipeline](_static/WebHookReceivers.png)

Die beiden Schlüsselkonzepte sind *Receiver* und *Handler:*

* *Receiver* sind für die Verarbeitung der besonderen Variante von WebHook von einem bestimmten Absender und für das Erzwingen von Sicherheitsüberprüfungen verantwortlich, um sicherzustellen, dass die WebHook-Anforderung tatsächlich vom beabsichtigten Absender stammt.

* *Handler* sind in der Regel dort, wo Benutzercode ausgeführt wird, der den jeweiligen WebHook verarbeitet.

In den folgenden Knoten werden diese Konzepte ausführlicher beschrieben.
