---
uid: webhooks/receiving/receivers
title: ASP.NET WebHooks-Empfänger | Microsoft Docs
author: rick-anderson
description: webHooks-ASP.NET-Empfänger
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675169"
---
# <a name="aspnet-webhooks-receivers"></a>webHooks-ASP.NET-Empfänger

Das Empfangen von WebHooks hängt davon ab, wer der Absender ist. Manchmal gibt es zusätzliche Schritte beim Registrieren eines WebHooks, um zu überprüfen, ob der Abonnent wirklich zuhört. Einige WebHooks stellen ein Push-to-Pull-Modell bereit, bei dem die HTTP-POST-Anforderung nur einen Verweis auf die Ereignisinformationen enthält, die dann unabhängig abgerufen werden sollen. Oft variiert das Sicherheitsmodell sehr stark.

Der Zweck von Microsoft ASP.NET WebHooks besteht darin, es einfacher und konsistenter zu machen, Ihre API zu verdrahten, ohne viel Zeit damit zu verbringen, herauszufinden, wie sie mit einer bestimmten Variante von WebHooks umgehen.

Ein WebHook-Empfänger ist für das Akzeptieren und Überprüfen von WebHooks von einem bestimmten Absender verantwortlich. Ein WebHook-Empfänger kann eine beliebige Anzahl von WebHooks unterstützen, die jeweils über eine eigene Konfiguration verfügen. Beispielsweise kann der GitHub WebHook-Empfänger WebHooks aus einer beliebigen Anzahl von GitHub-Repositorys akzeptieren.

## <a name="webhook-receiver-uris"></a>WebHook-Empfänger-URIs

Durch die Installation von Microsoft ASP.NET WebHooks erhalten Sie einen allgemeinen WebHook-Controller, der WebHook-Anforderungen von einer unbefristeten Anzahl von Diensten akzeptiert. Wenn eine Anforderung eintrifft, wählt sie den entsprechenden Empfänger aus, den Sie für die Verarbeitung eines bestimmten WebHook-Absenders installiert haben.

Der URI dieses Controllers ist der WebHook-URI, den Sie beim Dienst registrieren, und hat folgende Form:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Aus Sicherheitsgründen erfordern viele WebHook-Empfänger, dass der URI ein *https-URI* ist, und in einigen Fällen muss er auch einen zusätzlichen Abfrageparameter enthalten, der verwendet wird, um zu erzwingen, dass nur die beabsichtigte Partei WebHooks an den oben genannten URI senden kann.

Die `<receiver>` Komponente ist der Name des `github` `slack`Empfängers, z. B. oder .

Die *Id* ist ein optionaler Bezeichner, der verwendet werden kann, um eine bestimmte WebHook-Empfängerkonfiguration zu identifizieren. Dies kann verwendet werden, um N WebHooks bei einem bestimmten Empfänger zu registrieren. Die folgenden drei URIs können z. B. verwendet werden, um sich für drei unabhängige WebHooks zu registrieren:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Installieren eines WebHook-Empfängers

Um WebHooks mit Microsoft ASP.NET WebHooks zu empfangen, installieren Sie zunächst das Nuget-Paket für den WebHook-Anbieter oder die Anbieter, von denen Sie WebHooks erhalten möchten. Die Nuget-Pakete heißen [Microsoft.AspNet.WebHooks.Receivers.*,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) wobei der letzte Teil den unterstützten Dienst angibt. Beispiel:

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) bietet Unterstützung für den Empfang von WebHooks von GitHub und [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) bietet Unterstützung für den Empfang von WebHooks, die von ASP.NET WebHooks generiert werden.

Sofort finden Sie Unterstützung für Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello und WordPress, aber es ist möglich, eine beliebige Anzahl von anderen Anbietern zu unterstützen.

## <a name="configuring-a-webhook-receiver"></a>Konfigurieren eines WebHook-Empfängers

WebHook-Empfänger werden über das [IWebHookReceiverConfig-Inteface](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) konfiguriert, und bestimmte Implementierungen dieser Schnittstelle können mit jedem Abhängigkeitsinjektionsmodell registriert werden. Die Standardimplementierung verwendet Anwendungseinstellungen, die entweder in der Datei Web.config festgelegt werden können oder bei Verwendung von Azure Web Apps über das [Azure Portal](https://portal.azure.com/)festgelegt werden können.

![App-Einstellungen in Azure](_static/AzureAppSettings.png)

Das Format für Anwendungseinstellungsschlüssel lautet wie folgt:

```
MS_WebHookReceiverSecret_<receiver>
```

Der Wert ist eine durch Kommas getrennte Liste von Werten, die den Werten *von 'id'* entsprechen, für die WebHooks registriert wurden, z. B.:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Initialisieren eines WebHook-Empfängers

WebHook-Empfänger werden initialisiert, indem sie registriert werden, in der Regel in der statischen *WebApiConfig-Klasse,* z. B.:

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
