---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Horizontale Skalierung in SignalR mit Azure Servicebus (SignalR 1.x) | Microsoft-Dokumentation
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: cab185ccb048a374a08f4b5d978b30675c30a60d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59383959"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="cdba7-102">Horizontale Skalierung in SignalR mit Azure Service Bus (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="cdba7-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="cdba7-103">durch [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="cdba7-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="cdba7-104">In diesem Tutorial stellen Sie eine SignalR-Anwendung für eine Windows Azure-Webrolle, mit der Service Bus-Rückwandplatine zum Verteilen von Nachrichten an alle Rolleninstanzen bereit.</span><span class="sxs-lookup"><span data-stu-id="cdba7-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="cdba7-105">Erforderliche Komponenten:</span><span class="sxs-lookup"><span data-stu-id="cdba7-105">Prerequisites:</span></span>

- <span data-ttu-id="cdba7-106">Ein Windows Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="cdba7-106">A Windows Azure account.</span></span>
- <span data-ttu-id="cdba7-107">Die [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cdba7-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="cdba7-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="cdba7-108">Visual Studio 2012.</span></span>

<span data-ttu-id="cdba7-109">Die Service Bus-Rückwandplatine ist auch mit kompatibel [Service Bus für Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), Version 1.1.</span><span class="sxs-lookup"><span data-stu-id="cdba7-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="cdba7-110">Es ist jedoch nicht kompatibel mit Version 1.0 von Service Bus für Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cdba7-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="cdba7-111">Preise</span><span class="sxs-lookup"><span data-stu-id="cdba7-111">Pricing</span></span>

<span data-ttu-id="cdba7-112">Die Service Bus-Rückwandplatine werden Themen zum Senden von Nachrichten verwendet.</span><span class="sxs-lookup"><span data-stu-id="cdba7-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="cdba7-113">Aktuelle Preisinformationen, finden Sie unter [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="cdba7-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="cdba7-114">Zum Zeitpunkt der Erstellung dieses Dokuments können Sie für weniger als $1 1.000.000 Nachrichten pro Monat senden.</span><span class="sxs-lookup"><span data-stu-id="cdba7-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="cdba7-115">Der Rückwand sendet eine Service Bus-Nachricht für jeden Aufruf einer SignalR-Hub-Methode.</span><span class="sxs-lookup"><span data-stu-id="cdba7-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="cdba7-116">Es gibt auch einige Steuerungsnachrichten für Verbindungen, Trennvorgänge, verknüpfen oder eine verlassen Gruppen und So weiter.</span><span class="sxs-lookup"><span data-stu-id="cdba7-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="cdba7-117">In den meisten Fällen werden die meisten dem Volumen des Nachrichtenverkehrs hubmethodenaufrufe.</span><span class="sxs-lookup"><span data-stu-id="cdba7-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="cdba7-118">Übersicht</span><span class="sxs-lookup"><span data-stu-id="cdba7-118">Overview</span></span>

<span data-ttu-id="cdba7-119">Bevor wir mit dem ausführlichen Tutorial eingehen, sieht ein schnellen Überblick darüber, welche Aktionen Sie ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="cdba7-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="cdba7-120">Verwenden Sie Windows Azure-Portal, um einen neuen Service Bus-Namespace zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="cdba7-121">Fügen Sie diese NuGet-Pakete für Ihre Anwendung hinzu:</span><span class="sxs-lookup"><span data-stu-id="cdba7-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="cdba7-122">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="cdba7-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="cdba7-123">Microsoft.AspNet.SignalR.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="cdba7-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="cdba7-124">Erstellen einer SignalR-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="cdba7-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="cdba7-125">Fügen Sie den folgenden Code, der "Global.asax" So konfigurieren Sie die Rückwandplatine:</span><span class="sxs-lookup"><span data-stu-id="cdba7-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="cdba7-126">Wählen Sie für jede Anwendung einen anderen Wert für "Nameihrerapp" ein.</span><span class="sxs-lookup"><span data-stu-id="cdba7-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="cdba7-127">Verwenden Sie nicht den gleichen Wert für mehrere Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="cdba7-128">Erstellen Sie die Azure-Dienste</span><span class="sxs-lookup"><span data-stu-id="cdba7-128">Create the Azure Services</span></span>

<span data-ttu-id="cdba7-129">Erstellen Sie einen Cloud-Dienst aus, wie im [erstellen und Bereitstellen eines Clouddiensts](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span><span class="sxs-lookup"><span data-stu-id="cdba7-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="cdba7-130">Führen Sie die Schritte im Abschnitt "Vorgehensweise: Erstellen Sie einen Cloud-Dienst mithilfe der Schnellerfassung".</span><span class="sxs-lookup"><span data-stu-id="cdba7-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="cdba7-131">Für dieses Tutorial müssen Sie nicht, ein Zertifikat hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="cdba7-132">Erstellen Sie einen neuen Service Bus-Namespace, wie im [wie, verwendet Service Bus Themen/-Abonnements](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="cdba7-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="cdba7-133">Führen Sie die Schritte im Abschnitt "Erstellen einer Dienst-Namespace" aus.</span><span class="sxs-lookup"><span data-stu-id="cdba7-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="cdba7-134">Stellen Sie sicher, dass die gleiche Region für den Clouddienst und Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="cdba7-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="cdba7-135">Visual Studio-Projekt erstellen</span><span class="sxs-lookup"><span data-stu-id="cdba7-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="cdba7-136">Starten Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdba7-136">Start Visual Studio.</span></span> <span data-ttu-id="cdba7-137">Von der **Datei** Menü klicken Sie auf **neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="cdba7-138">In der **neues Projekt** Dialogfeld erweitern Sie **Visual C#-**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="cdba7-139">Klicken Sie unter **installierte Vorlagen**Option **Cloud** und wählen Sie dann **Windows Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="cdba7-140">Behalten Sie die standardmäßigen .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cdba7-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="cdba7-141">Nennen Sie die Anwendung ChatService, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="cdba7-142">In der **neuen Windows Azure-Cloud-Dienst** im Dialogfeld auf ASP.NET MVC 4-Webrolle.</span><span class="sxs-lookup"><span data-stu-id="cdba7-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="cdba7-143">Klicken Sie auf den Pfeil nach rechts-Schaltfläche (**&gt;**) um die Rolle der Projektmappe hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="cdba7-144">Zeigen Sie auf den die neue Rolle, also das Stiftsymbol angezeigt.</span><span class="sxs-lookup"><span data-stu-id="cdba7-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="cdba7-145">Klicken Sie auf dieses Symbol, um die Rolle umbenennen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-145">Click this icon to rename the role.</span></span> <span data-ttu-id="cdba7-146">Benennen Sie die Rolle "SignalRChat", und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="cdba7-147">In der **neues ASP.NET MVC 4-Projekt** Assistenten **Internetanwendung**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="cdba7-148">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-148">Click **OK**.</span></span> <span data-ttu-id="cdba7-149">Der Assistent erstellt zwei Projekte:</span><span class="sxs-lookup"><span data-stu-id="cdba7-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="cdba7-150">ChatService: Dieses Projekt ist das Windows Azure-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="cdba7-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="cdba7-151">Es definiert die Azure-Rollen und andere Konfigurationsoptionen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="cdba7-152">SignalRChat: Dieses Projekt ist das ASP.NET MVC 4-Projekt.</span><span class="sxs-lookup"><span data-stu-id="cdba7-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="cdba7-153">Erstellen Sie die SignalR Chat-Anwendung</span><span class="sxs-lookup"><span data-stu-id="cdba7-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="cdba7-154">Um die chatanwendung zu erstellen, führen Sie die Schritte in diesem Tutorial [erste Schritte mit SignalR und MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span><span class="sxs-lookup"><span data-stu-id="cdba7-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="cdba7-155">Verwenden Sie NuGet, um die erforderlichen Bibliotheken zu installieren.</span><span class="sxs-lookup"><span data-stu-id="cdba7-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="cdba7-156">Von der **Tools** , wählen Sie im Menü **NuGet Package Manager**, und wählen Sie dann **-Paket-Manager-Konsole**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="cdba7-157">In der **-Paket-Manager-Konsole** Fenster, geben Sie die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="cdba7-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="cdba7-158">Verwenden der `-ProjectName` Option aus, um die Pakete auf das ASP.NET MVC-Projekt, und nicht auf Windows Azure-Projekt zu installieren.</span><span class="sxs-lookup"><span data-stu-id="cdba7-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="cdba7-159">Konfigurieren der Rückwandplatine</span><span class="sxs-lookup"><span data-stu-id="cdba7-159">Configure the Backplane</span></span>

<span data-ttu-id="cdba7-160">Fügen Sie in der Datei Global.asax der Anwendung den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="cdba7-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="cdba7-161">Nun müssen Sie Ihre Service Bus-Verbindungszeichenfolge zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="cdba7-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="cdba7-162">Wählen Sie im Azure-Portal die Service Bus-Namespace, den Sie erstellt haben, und klicken Sie auf das Symbol "Zugriffsschlüssel".</span><span class="sxs-lookup"><span data-stu-id="cdba7-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="cdba7-163">Kopieren Sie die Verbindungszeichenfolge in die Zwischenablage, und fügen Sie ihn in das *"ConnectionString"* Variable.</span><span class="sxs-lookup"><span data-stu-id="cdba7-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="cdba7-164">Bereitstellung in Azure</span><span class="sxs-lookup"><span data-stu-id="cdba7-164">Deploy to Azure</span></span>

<span data-ttu-id="cdba7-165">Erweitern Sie im Projektmappen-Explorer die **Rollen** Ordner innerhalb des Projekts ChatService.</span><span class="sxs-lookup"><span data-stu-id="cdba7-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="cdba7-166">Mit der rechten Maustaste in der Rolle "SignalRChat", und wählen Sie **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="cdba7-167">Wählen Sie die Registerkarte **Konfiguration** aus. Klicken Sie unter **Instanzen** 2 auswählen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="cdba7-168">Sie können auch die Größe des virtuellen Computers festlegen, um **sehr klein**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="cdba7-169">Speichern Sie die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-169">Save the changes.</span></span>

<span data-ttu-id="cdba7-170">Klicken Sie im Projektmappen-Explorer das Projekt ChatService.</span><span class="sxs-lookup"><span data-stu-id="cdba7-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="cdba7-171">Wählen Sie **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="cdba7-172">Wenn dies Ihre erste Zeit mit der Veröffentlichung in Windows Azure ist, müssen Sie Ihre Anmeldeinformationen herunterladen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="cdba7-173">In der **veröffentlichen** -Assistenten klicken Sie auf "Sign in to download Credentials".</span><span class="sxs-lookup"><span data-stu-id="cdba7-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="cdba7-174">Dadurch werden Sie aufgefordert, sich bei Windows Azure-Portal anzumelden, und eine Datei mit veröffentlichungseinstellungen herunterladen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="cdba7-175">Klicken Sie auf **Import** , und wählen Sie die von Ihnen heruntergeladene Datei mit den veröffentlichungseinstellungen.</span><span class="sxs-lookup"><span data-stu-id="cdba7-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="cdba7-176">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-176">Click **Next**.</span></span> <span data-ttu-id="cdba7-177">In der **Veröffentlichungseinstellungen** Dialogfeld unter **Clouddienst**, wählen Sie den Clouddienst, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="cdba7-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="cdba7-178">Klicken Sie auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="cdba7-178">Click **Publish**.</span></span> <span data-ttu-id="cdba7-179">Es dauert einige Minuten, bis die Anwendung bereitstellen und starten die virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="cdba7-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="cdba7-180">Wenn Sie die chatanwendung ausführen, kommunizieren die Rolleninstanzen jetzt über Azure Service Bus, ein Service Bus-Thema mit.</span><span class="sxs-lookup"><span data-stu-id="cdba7-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="cdba7-181">Ein Thema ist eine Warteschlange, die mehrere Abonnenten ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="cdba7-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="cdba7-182">Der Rückwand wird automatisch erstellt, das Thema und die Abonnements.</span><span class="sxs-lookup"><span data-stu-id="cdba7-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="cdba7-183">Um die Abonnements und die Nachrichtenaktivität anzuzeigen, öffnen Sie das Azure-Portal, wählen Sie den Service Bus-Namespace, und klicken Sie auf "Themen".</span><span class="sxs-lookup"><span data-stu-id="cdba7-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="cdba7-184">Sie nehmen einige Minuten, bis die Aktivität auf dem Dashboard angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="cdba7-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="cdba7-185">SignalR verwaltet die Lebensdauer des Themas.</span><span class="sxs-lookup"><span data-stu-id="cdba7-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="cdba7-186">Solange Ihre Anwendung bereitgestellt wird, versuchen Sie nicht manuell löschen von Themen oder Ändern der Einstellungen für das Thema.</span><span class="sxs-lookup"><span data-stu-id="cdba7-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
