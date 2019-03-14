---
title: DevOps mit ASP.NET Core und Azure
author: CamSoper
description: 'Ein Leitfaden, der End-to-End-Anleitungen zum Erstellen einer DevOps-Pipeline für eine in Azure gehostete ASP.NET Core-App bereitstellt.'
ms.author: casoper
ms.date: 08/07/2018
ms.custom: seodec18
uid: azure/devops/index
---
# <a name="devops-with-aspnet-core-and-azure"></a><span data-ttu-id="6c8fd-103">DevOps mit ASP.NET Core und Azure</span><span class="sxs-lookup"><span data-stu-id="6c8fd-103">DevOps with ASP.NET Core and Azure</span></span>

<span data-ttu-id="6c8fd-104">[![Titelbild](./media/cover-large.png)](https://aka.ms/devopsbook)</span><span class="sxs-lookup"><span data-stu-id="6c8fd-104">[![Cover Image](./media/cover-large.png)](https://aka.ms/devopsbook)</span></span>

<span data-ttu-id="6c8fd-105">Von [Cam Soper](https://twitter.com/camsoper) und [Scott Addie](https://twitter.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="6c8fd-105">By [Cam Soper](https://twitter.com/camsoper) and [Scott Addie](https://twitter.com/scottaddie)</span></span>

<span data-ttu-id="6c8fd-106">Dieser Leitfaden ist als [herunterladbares E-Book im PDF-Format](https://aka.ms/devopsbook) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-106">This guide is available as a [downloadable PDF e-book](https://aka.ms/devopsbook).</span></span>

## <a name="welcome"></a><span data-ttu-id="6c8fd-107">Willkommen</span><span class="sxs-lookup"><span data-stu-id="6c8fd-107">Welcome</span></span> 

<span data-ttu-id="6c8fd-108">Willkommen zum Leitfaden für den Azure-Entwicklungslebenszyklus für .NET.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-108">Welcome to the Azure Development Lifecycle guide for .NET!</span></span> <span data-ttu-id="6c8fd-109">In diesem Leitfaden werden die grundlegenden Konzepte zum Erstellen eines Entwicklungslebenszyklus für Azure mithilfe von .NET-Tools und -Prozessen vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-109">This guide introduces the basic concepts of building a development lifecycle around Azure using .NET tools and processes.</span></span> <span data-ttu-id="6c8fd-110">Nach Abschluss dieses Leitfadens können Sie die Vorteile einer ausgereiften DevOps-Toolkette nutzen.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-110">After finishing this guide, you'll reap the benefits of a mature DevOps toolchain.</span></span>

## <a name="who-this-guide-is-for"></a><span data-ttu-id="6c8fd-111">Für wen ist dieser Leitfaden gedacht?</span><span class="sxs-lookup"><span data-stu-id="6c8fd-111">Who this guide is for</span></span>

<span data-ttu-id="6c8fd-112">Sie sollten ein erfahrener ASP.NET Core-Entwickler (auf Ebene 200–300) sein.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-112">You should be an experienced ASP.NET Core developer (200-300 level).</span></span> <span data-ttu-id="6c8fd-113">Sie müssen nicht mit Azure vertraut sein, da dieses Thema in der Einführung behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-113">You don't need to know anything about Azure, as we'll cover that in this introduction.</span></span> <span data-ttu-id="6c8fd-114">DevOps-Techniker, die sich eher auf die Vorgänge als auf die Entwicklung konzentrieren, können ebenso von diesem Leitfaden profitieren.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-114">This guide may also be useful for DevOps engineers who are more focused on operations than development.</span></span>

<span data-ttu-id="6c8fd-115">Dieser Leitfaden ist für Windows-Entwickler konzipiert.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-115">This guide targets Windows developers.</span></span> <span data-ttu-id="6c8fd-116">Linux und macOS werden jedoch vollständig von .NET Core unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-116">However, Linux and macOS are fully supported by .NET Core.</span></span> <span data-ttu-id="6c8fd-117">Um diesen Leitfaden für Linux bzw. macOS zu nutzen, beachten Sie die Anzeigen für Linux-/macOS-Unterschiede.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-117">To adapt this guide for Linux/macOS, watch for callouts for Linux/macOS differences.</span></span>

## <a name="what-this-guide-doesnt-cover"></a><span data-ttu-id="6c8fd-118">Was in diesem Leitfaden nicht behandelt wird</span><span class="sxs-lookup"><span data-stu-id="6c8fd-118">What this guide doesn't cover</span></span>

<span data-ttu-id="6c8fd-119">Er bezieht sich auf eine kontinuierliche End-to-End-Bereitstellungserfahrung für .NET-Entwickler.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-119">This guide is focused on an end-to-end continuous deployment experience for .NET developers.</span></span> <span data-ttu-id="6c8fd-120">Es handelt sich nicht um eine vollständige Anleitung für alle Azure-Themen sowie für .NET-APIs für Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-120">It's not an exhaustive guide to all things Azure, and it doesn't focus extensively on .NET APIs for Azure services.</span></span> <span data-ttu-id="6c8fd-121">Der Schwerpunkt liegt vor allem bei der Continuous Integration, der Bereitstellung, der Überwachung und dem Debuggen.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-121">The emphasis is all around continuous integration, deployment, monitoring, and debugging.</span></span> <span data-ttu-id="6c8fd-122">Gegen Ende dieses Leitfadens finden Sie Empfehlungen für weitere Schritte.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-122">Near the end of the guide, recommendations for next steps are offered.</span></span> <span data-ttu-id="6c8fd-123">Darin enthalten sind Azure-Plattformdienste, die für ASP.NET Core-Entwickler nützlich sind.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-123">Included in the suggestions are Azure platform services that are useful to ASP.NET Core developers.</span></span>

## <a name="whats-in-this-guide"></a><span data-ttu-id="6c8fd-124">In diesem Handbuch</span><span class="sxs-lookup"><span data-stu-id="6c8fd-124">What's in this guide</span></span>

### <a name="tools-and-downloadsxrefazuredevopstools-and-downloads"></a>[<span data-ttu-id="6c8fd-125">Tools und Downloads</span><span class="sxs-lookup"><span data-stu-id="6c8fd-125">Tools and downloads</span></span>](xref:azure/devops/tools-and-downloads)

<span data-ttu-id="6c8fd-126">Erfahren Sie, wo die in diesem Leitfaden verwendeten Tools abgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-126">Learn where to acquire the tools used in this guide.</span></span>

### <a name="deploy-to-app-servicexrefazuredevopsdeploy-to-app-service"></a>[<span data-ttu-id="6c8fd-127">Bereitstellen in App Service</span><span class="sxs-lookup"><span data-stu-id="6c8fd-127">Deploy to App Service</span></span>](xref:azure/devops/deploy-to-app-service)

<span data-ttu-id="6c8fd-128">Informationen zu den verschiedenen Methoden zum Bereitstellen einer ASP.NET Core-App zu Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-128">Learn the various methods for deploying an ASP.NET Core app to Azure App Service.</span></span>

### <a name="continuous-integration-and-deploymentxrefazuredevopscicd"></a>[<span data-ttu-id="6c8fd-129">Continuous Integration und Continuous Deployment</span><span class="sxs-lookup"><span data-stu-id="6c8fd-129">Continuous integration and deployment</span></span>](xref:azure/devops/cicd)

<span data-ttu-id="6c8fd-130">Stellen Sie eine End-to-End-Lösung für Continuous Integration und Continuous Deployment für Ihre ASP.NET Core-App mit GitHub, Azure DevOps Services und Azure bereit.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-130">Build an end-to-end continuous integration and deployment solution for your ASP.NET Core app with GitHub, Azure DevOps Services, and Azure.</span></span>

### <a name="monitor-and-debugxrefazuredevopsmonitor"></a>[<span data-ttu-id="6c8fd-131">Überwachen und Debuggen</span><span class="sxs-lookup"><span data-stu-id="6c8fd-131">Monitor and debug</span></span>](xref:azure/devops/monitor)

<span data-ttu-id="6c8fd-132">Verwenden Sie Azure-Tools zum Überwachen, Optimieren und für die Problembehandlung Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-132">Use Azure's tools to monitor, troubleshoot, and tune your application.</span></span>

### <a name="next-stepsxrefazuredevopsnext-steps"></a>[<span data-ttu-id="6c8fd-133">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6c8fd-133">Next steps</span></span>](xref:azure/devops/next-steps)

<span data-ttu-id="6c8fd-134">Andere Lernpfade für die ASP.NET Core-Entwickler, die sich mit Azure vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-134">Other learning paths for the ASP.NET Core developer learning Azure.</span></span>

## <a name="additional-introductory-reading"></a><span data-ttu-id="6c8fd-135">Weiterführende einführende Literatur</span><span class="sxs-lookup"><span data-stu-id="6c8fd-135">Additional introductory reading</span></span>

<span data-ttu-id="6c8fd-136">Wenn Sie zum ersten Mal mit Cloud Computing arbeiten, können Sie in folgenden Artikeln die Grundlagen dazu nachlesen.</span><span class="sxs-lookup"><span data-stu-id="6c8fd-136">If this is your first exposure to cloud computing, these articles explain the basics.</span></span>

* [<span data-ttu-id="6c8fd-137">Was ist Cloud Computing?</span><span class="sxs-lookup"><span data-stu-id="6c8fd-137">What is Cloud Computing?</span></span>](https://azure.microsoft.com/overview/what-is-cloud-computing/)
* [<span data-ttu-id="6c8fd-138">Examples of Cloud Computing (Beispiele für Cloud Computing)</span><span class="sxs-lookup"><span data-stu-id="6c8fd-138">Examples of Cloud Computing</span></span>](https://azure.microsoft.com/overview/examples-of-cloud-computing/)
* [<span data-ttu-id="6c8fd-139">Was ist IaaS?</span><span class="sxs-lookup"><span data-stu-id="6c8fd-139">What is IaaS?</span></span>](https://azure.microsoft.com/overview/what-is-iaas/)
* [<span data-ttu-id="6c8fd-140">Was ist PaaS?</span><span class="sxs-lookup"><span data-stu-id="6c8fd-140">What is PaaS?</span></span>](https://azure.microsoft.com/overview/what-is-paas/)
