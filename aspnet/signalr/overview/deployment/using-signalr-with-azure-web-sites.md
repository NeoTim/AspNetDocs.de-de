---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Verwenden von SignalR mit Web-Apps in Azure App Service | Microsoft-Dokumentation
author: bradygaster
description: Dieses Dokument beschreibt, wie Sie eine SignalR-Anwendung zu konfigurieren, die in Microsoft Azure ausgeführt wird. Softwareversionen, die im Tutorial verwendet werden, Visual Studio 2013 oder VIS...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128141"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="e940a-104">Verwenden von SignalR mit Web-Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e940a-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="e940a-105">durch [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e940a-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e940a-106">Dieses Dokument beschreibt, wie Sie eine SignalR-Anwendung zu konfigurieren, die in Microsoft Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="e940a-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e940a-107">Softwareversionen, die in diesem Tutorial verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e940a-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="e940a-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) oder Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e940a-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="e940a-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e940a-109">.NET 4.5</span></span>
> - <span data-ttu-id="e940a-110">SignalR-Version 2</span><span class="sxs-lookup"><span data-stu-id="e940a-110">SignalR version 2</span></span>
> - <span data-ttu-id="e940a-111">Azure SDK 2.3 für Visual Studio 2013 oder 2012</span><span class="sxs-lookup"><span data-stu-id="e940a-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="e940a-112">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="e940a-112">Questions and comments</span></span>
>
> <span data-ttu-id="e940a-113">Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können.</span><span class="sxs-lookup"><span data-stu-id="e940a-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e940a-114">Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), oder die [Microsoft Azure-Foren](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span><span class="sxs-lookup"><span data-stu-id="e940a-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="e940a-115">Inhaltsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="e940a-115">Table of Contents</span></span>

- [<span data-ttu-id="e940a-116">Introduction (Einführung)</span><span class="sxs-lookup"><span data-stu-id="e940a-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="e940a-117">Bereitstellen einer SignalR-Web-App in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e940a-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="e940a-118">Aktivieren WebSockets in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e940a-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="e940a-119">Mithilfe der Azure Redis Cache-Rückwandplatine</span><span class="sxs-lookup"><span data-stu-id="e940a-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="e940a-120">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e940a-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="e940a-121">Einführung</span><span class="sxs-lookup"><span data-stu-id="e940a-121">Introduction</span></span>

<span data-ttu-id="e940a-122">ASP.NET SignalR kann verwendet werden, um eine neue Ebene der Interaktivität zwischen Server und Web oder -Clients für .NET zu bringen.</span><span class="sxs-lookup"><span data-stu-id="e940a-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="e940a-123">Wenn in Azure gehostet wird, SignalR-Anwendungen profitieren von der hoch verfügbare, skalierbare und leistungsstarke Umgebung, die in der Cloud bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="e940a-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="e940a-124">Bereitstellen einer SignalR-Web-App in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e940a-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="e940a-125">SignalR hinzufügen keine bestimmten schwierigkeiten für die Bereitstellung von einer Anwendung in Azure und der Bereitstellung mit einem lokalen Server.</span><span class="sxs-lookup"><span data-stu-id="e940a-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="e940a-126">Eine Anwendung, die SignalR verwendet in Azure gehostet werden kann, ohne Änderungen an der Konfiguration oder sonstige Einstellungen (über WebSockets-Unterstützung finden Sie unter [Aktivieren von WebSockets in Azure App Service](#websocket) unten.) In diesem Tutorial stellen Sie die Anwendung erstellt, der [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e940a-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="e940a-127">**Erforderliche Komponenten**</span><span class="sxs-lookup"><span data-stu-id="e940a-127">**Prerequisites**</span></span>

- <span data-ttu-id="e940a-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e940a-128">Visual Studio 2013.</span></span> <span data-ttu-id="e940a-129">Wenn Sie Visual Studio nicht haben, ist Visual Studio-2013 Express für Web in der Installation des Azure SDK enthalten.</span><span class="sxs-lookup"><span data-stu-id="e940a-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="e940a-130">[Azure SDK 2.3 für Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) oder [Azure SDK 2.3 für Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span><span class="sxs-lookup"><span data-stu-id="e940a-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="e940a-131">Um dieses Tutorial abzuschließen, benötigen Sie ein Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="e940a-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="e940a-132">Sie können [Ihre MSDN-abonnentenvorteile aktivieren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), oder [registrieren Sie sich für ein Testabonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e940a-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="e940a-133">Eine SignalR-Web-app Bereitstellen in Azure</span><span class="sxs-lookup"><span data-stu-id="e940a-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="e940a-134">Abschließen der [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), oder Laden Sie das fertige Projekt [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="e940a-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="e940a-135">Wählen Sie in Visual Studio **erstellen**, **veröffentlichen SignalR Chat**.</span><span class="sxs-lookup"><span data-stu-id="e940a-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="e940a-136">Wählen Sie im Dialogfeld "Web veröffentlichen" "Windows Azure-Websites".</span><span class="sxs-lookup"><span data-stu-id="e940a-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Wählen Sie die Azure-Websites](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="e940a-138">Wenn Sie sich mit Ihrem Microsoft-Konto angemeldet sind, klicken Sie auf **anmelden...**  in das Dialogfeld "vorhandene Website auswählen", und melden Sie sich.</span><span class="sxs-lookup"><span data-stu-id="e940a-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![Vorhandene Website auswählen](using-signalr-with-azure-web-sites/_static/image2.png)    ![Melden Sie sich bei Azure an.](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="e940a-141">Klicken Sie im Dialogfeld "vorhandene Website auswählen" auf **neu**.</span><span class="sxs-lookup"><span data-stu-id="e940a-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![Neue Website](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="e940a-143">Geben Sie im Dialogfeld "Website auf Windows Azure erstellen" einen eindeutigen Anwendungsnamen ein.</span><span class="sxs-lookup"><span data-stu-id="e940a-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="e940a-144">Wählen Sie die Ihnen am nächsten gelegene Region, in der Region-Dropdownliste.</span><span class="sxs-lookup"><span data-stu-id="e940a-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="e940a-145">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e940a-145">Click **Create**.</span></span>

    ![Erstellen Sie die Website in Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="e940a-147">Klicken Sie im Dialogfeld "Web veröffentlichen" auf **veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="e940a-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![Website veröffentlichen](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="e940a-149">Wenn die app die Veröffentlichung abgeschlossen ist, wird die SignalR Chat-Anwendung in Azure App Service-Web-Apps gehosteten in einem Browser geöffnet.</span><span class="sxs-lookup"><span data-stu-id="e940a-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![Website, die in einem Browser öffnen](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="e940a-151">Aktivieren WebSockets in Azure App Service-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="e940a-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="e940a-152">WebSockets muss explizit in Ihrer Web-app aktiviert werden, in einer SignalR-Anwendung verwendet werden; andernfalls, die andere Protokolle verwendet werden (finden Sie unter [Transporte und Fallbacks](../getting-started/introduction-to-signalr.md#transports) Einzelheiten).</span><span class="sxs-lookup"><span data-stu-id="e940a-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="e940a-153">Um WebSockets auf Azure App Service-Web-Apps zu verwenden, aktivieren sie im Abschnitt "Konfiguration" der Web-app.</span><span class="sxs-lookup"><span data-stu-id="e940a-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="e940a-154">Zu diesem Zweck öffnen Sie Ihre Web-app die [Azure-Verwaltungsportal](https://manage.windowsazure.com/), und wählen Sie konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e940a-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![Registerkarte „Konfigurieren“](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="e940a-156">Am oberen Rand der Konfigurationsseite stellen Sie sicher, dass .NET 4.5 für Ihre Web-app verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e940a-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET Framework Version 4.5-Einstellung](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="e940a-158">Auf der Seite-Konfiguration in der **WebSockets** wählen Sie die Einstellung **auf**.</span><span class="sxs-lookup"><span data-stu-id="e940a-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![WebSockets-Einstellung: Ein](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="e940a-160">Wählen Sie am unteren Rand der Konfigurationsseite, **speichern** zum Speichern der Änderungen.</span><span class="sxs-lookup"><span data-stu-id="e940a-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![Speichern Sie die Einstellungen](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="e940a-162">Mithilfe der Azure Redis Cache-Rückwandplatine</span><span class="sxs-lookup"><span data-stu-id="e940a-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="e940a-163">Wenn Sie mehrere Instanzen für Ihre Web-app, und die Benutzer dieser Instanzen müssen miteinander interagieren (sodass z. B. Chat-Nachrichten erstellt, die in einer Instanz mit anderen Instanzen verbundenen Benutzer erreichen können), wird die [Azure Redis Cache Rückwand](../performance/scaleout-with-redis.md) in Ihrer Anwendung implementiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="e940a-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="e940a-164">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e940a-164">Next Steps</span></span>

<span data-ttu-id="e940a-165">Weitere Informationen zu Web-Apps in Azure App Service, finden Sie unter [-Web-Apps – Übersicht](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span><span class="sxs-lookup"><span data-stu-id="e940a-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
