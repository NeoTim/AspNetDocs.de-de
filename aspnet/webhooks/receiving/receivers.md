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
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="146d3-103">webHooks-ASP.NET-Empfänger</span><span class="sxs-lookup"><span data-stu-id="146d3-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="146d3-104">Das Empfangen von WebHooks hängt davon ab, wer der Absender ist.</span><span class="sxs-lookup"><span data-stu-id="146d3-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="146d3-105">Manchmal gibt es zusätzliche Schritte beim Registrieren eines WebHooks, um zu überprüfen, ob der Abonnent wirklich zuhört.</span><span class="sxs-lookup"><span data-stu-id="146d3-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="146d3-106">Einige WebHooks stellen ein Push-to-Pull-Modell bereit, bei dem die HTTP-POST-Anforderung nur einen Verweis auf die Ereignisinformationen enthält, die dann unabhängig abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="146d3-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="146d3-107">Oft variiert das Sicherheitsmodell sehr stark.</span><span class="sxs-lookup"><span data-stu-id="146d3-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="146d3-108">Der Zweck von Microsoft ASP.NET WebHooks besteht darin, es einfacher und konsistenter zu machen, Ihre API zu verdrahten, ohne viel Zeit damit zu verbringen, herauszufinden, wie sie mit einer bestimmten Variante von WebHooks umgehen.</span><span class="sxs-lookup"><span data-stu-id="146d3-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="146d3-109">Ein WebHook-Empfänger ist für das Akzeptieren und Überprüfen von WebHooks von einem bestimmten Absender verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="146d3-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="146d3-110">Ein WebHook-Empfänger kann eine beliebige Anzahl von WebHooks unterstützen, die jeweils über eine eigene Konfiguration verfügen.</span><span class="sxs-lookup"><span data-stu-id="146d3-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="146d3-111">Beispielsweise kann der GitHub WebHook-Empfänger WebHooks aus einer beliebigen Anzahl von GitHub-Repositorys akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="146d3-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="146d3-112">WebHook-Empfänger-URIs</span><span class="sxs-lookup"><span data-stu-id="146d3-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="146d3-113">Durch die Installation von Microsoft ASP.NET WebHooks erhalten Sie einen allgemeinen WebHook-Controller, der WebHook-Anforderungen von einer unbefristeten Anzahl von Diensten akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="146d3-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="146d3-114">Wenn eine Anforderung eintrifft, wählt sie den entsprechenden Empfänger aus, den Sie für die Verarbeitung eines bestimmten WebHook-Absenders installiert haben.</span><span class="sxs-lookup"><span data-stu-id="146d3-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="146d3-115">Der URI dieses Controllers ist der WebHook-URI, den Sie beim Dienst registrieren, und hat folgende Form:</span><span class="sxs-lookup"><span data-stu-id="146d3-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="146d3-116">Aus Sicherheitsgründen erfordern viele WebHook-Empfänger, dass der URI ein *https-URI* ist, und in einigen Fällen muss er auch einen zusätzlichen Abfrageparameter enthalten, der verwendet wird, um zu erzwingen, dass nur die beabsichtigte Partei WebHooks an den oben genannten URI senden kann.</span><span class="sxs-lookup"><span data-stu-id="146d3-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="146d3-117">Die `<receiver>` Komponente ist der Name des `github` `slack`Empfängers, z. B. oder .</span><span class="sxs-lookup"><span data-stu-id="146d3-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="146d3-118">Die *Id* ist ein optionaler Bezeichner, der verwendet werden kann, um eine bestimmte WebHook-Empfängerkonfiguration zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="146d3-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="146d3-119">Dies kann verwendet werden, um N WebHooks bei einem bestimmten Empfänger zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="146d3-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="146d3-120">Die folgenden drei URIs können z. B. verwendet werden, um sich für drei unabhängige WebHooks zu registrieren:</span><span class="sxs-lookup"><span data-stu-id="146d3-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="146d3-121">Installieren eines WebHook-Empfängers</span><span class="sxs-lookup"><span data-stu-id="146d3-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="146d3-122">Um WebHooks mit Microsoft ASP.NET WebHooks zu empfangen, installieren Sie zunächst das Nuget-Paket für den WebHook-Anbieter oder die Anbieter, von denen Sie WebHooks erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="146d3-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="146d3-123">Die Nuget-Pakete heißen [Microsoft.AspNet.WebHooks.Receivers.\*,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) wobei der letzte Teil den unterstützten Dienst angibt.</span><span class="sxs-lookup"><span data-stu-id="146d3-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="146d3-124">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="146d3-124">For example</span></span>

<span data-ttu-id="146d3-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) bietet Unterstützung für den Empfang von WebHooks von GitHub und [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) bietet Unterstützung für den Empfang von WebHooks, die von ASP.NET WebHooks generiert werden.</span><span class="sxs-lookup"><span data-stu-id="146d3-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="146d3-126">Sofort finden Sie Unterstützung für Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello und WordPress, aber es ist möglich, eine beliebige Anzahl von anderen Anbietern zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="146d3-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="146d3-127">Konfigurieren eines WebHook-Empfängers</span><span class="sxs-lookup"><span data-stu-id="146d3-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="146d3-128">WebHook-Empfänger werden über das [IWebHookReceiverConfig-Inteface](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) konfiguriert, und bestimmte Implementierungen dieser Schnittstelle können mit jedem Abhängigkeitsinjektionsmodell registriert werden.</span><span class="sxs-lookup"><span data-stu-id="146d3-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="146d3-129">Die Standardimplementierung verwendet Anwendungseinstellungen, die entweder in der Datei Web.config festgelegt werden können oder bei Verwendung von Azure Web Apps über das [Azure Portal](https://portal.azure.com/)festgelegt werden können.</span><span class="sxs-lookup"><span data-stu-id="146d3-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![App-Einstellungen in Azure](_static/AzureAppSettings.png)

<span data-ttu-id="146d3-131">Das Format für Anwendungseinstellungsschlüssel lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="146d3-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="146d3-132">Der Wert ist eine durch Kommas getrennte Liste von Werten, die den Werten *von 'id'* entsprechen, für die WebHooks registriert wurden, z. B.:</span><span class="sxs-lookup"><span data-stu-id="146d3-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="146d3-133">Initialisieren eines WebHook-Empfängers</span><span class="sxs-lookup"><span data-stu-id="146d3-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="146d3-134">WebHook-Empfänger werden initialisiert, indem sie registriert werden, in der Regel in der statischen *WebApiConfig-Klasse,* z. B.:</span><span class="sxs-lookup"><span data-stu-id="146d3-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
