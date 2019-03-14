---
title: Das Metapaket „Microsoft.AspNetCore.All“ für ASP.NET Core 2.0
author: Rick-Anderson
description: Das Metapaket „Microsoft.AspNetCore.All“ wird für ASP.NET Core 2.1 oder höher nicht empfohlen.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064857"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a><span data-ttu-id="d7987-103">Das Metapaket „Microsoft.AspNetCore.All“ für ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="d7987-103">Microsoft.AspNetCore.All metapackage for ASP.NET Core 2.0</span></span>

> [!NOTE]
> <span data-ttu-id="d7987-104">Es wird empfohlen, für Anwendungen, die ASP.NET Core 2.1 und höher anzielen, das Metapaket [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) statt diesem Paket zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="d7987-104">We recommend applications targeting ASP.NET Core 2.1 and later use the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) rather than this package.</span></span> <span data-ttu-id="d7987-105">Weitere Informationen finden Sie in diesem Artikel unter [Migrieren von Microsoft.AspNetCore.All zu Microsoft.AspNetCore.App](#migrate).</span><span class="sxs-lookup"><span data-stu-id="d7987-105">See [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](#migrate) in this article.</span></span>

<span data-ttu-id="d7987-106">Für dieses Feature ist ASP.NET Core 2.x für .NET Core 2.x erforderlich.</span><span class="sxs-lookup"><span data-stu-id="d7987-106">This feature requires ASP.NET Core 2.x targeting .NET Core 2.x.</span></span>

<span data-ttu-id="d7987-107">Das Metapaket [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) für ASP.NET Core enthält:</span><span class="sxs-lookup"><span data-stu-id="d7987-107">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="d7987-108">alle unterstützten Pakete des ASP.NET Core-Teams</span><span class="sxs-lookup"><span data-stu-id="d7987-108">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="d7987-109">alle unterstützten Pakete von Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="d7987-109">All supported packages by the Entity Framework Core.</span></span>
* <span data-ttu-id="d7987-110">interne und Drittanbieterabhängigkeiten, die von ASP.NET Core und Entity Framework Core verwendet werden</span><span class="sxs-lookup"><span data-stu-id="d7987-110">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="d7987-111">In dem Paket `Microsoft.AspNetCore.All` sind alle Features von ASP.NET Core 2.x und Entity Framework Core 2.x enthalten.</span><span class="sxs-lookup"><span data-stu-id="d7987-111">All the features of ASP.NET Core 2.x and Entity Framework Core 2.x are included in the `Microsoft.AspNetCore.All` package.</span></span> <span data-ttu-id="d7987-112">Die Standardprojektvorlagen für ASP.NET Core 2.0 verwenden dieses Paket.</span><span class="sxs-lookup"><span data-stu-id="d7987-112">The default project templates targeting ASP.NET Core 2.0 use this package.</span></span>

<span data-ttu-id="d7987-113">Die Versionsnummer des Metapakets `Microsoft.AspNetCore.All` stellt die ASP.NET Core-Version und die Entity Framework Core-Version dar.</span><span class="sxs-lookup"><span data-stu-id="d7987-113">The version number of the `Microsoft.AspNetCore.All` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="d7987-114">Anwendungen, die das Metapaket `Microsoft.AspNetCore.All` verwenden, profitieren automatisch von dem [.NET Core-Laufzeitspeicher](/dotnet/core/deploying/runtime-store).</span><span class="sxs-lookup"><span data-stu-id="d7987-114">Applications that use the `Microsoft.AspNetCore.All` metapackage automatically take advantage of the [.NET Core Runtime Store](/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="d7987-115">Der Laufzeitspeicher enthält alle Laufzeitobjekte, die für die Ausführung von ASP.NET Core 2.x-Anwendungen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="d7987-115">The Runtime Store contains all the runtime assets needed to run ASP.NET Core 2.x applications.</span></span> <span data-ttu-id="d7987-116">Bei Verwendung des Metapakets `Microsoft.AspNetCore.All` werden **keine** Objekte aus den referenzierten ASP.NET Core NuGet-Paketen mit der Anwendung &mdash; bereitgestellt. Der .NET Core-Laufzeitspeicher enthält diese Objekte.</span><span class="sxs-lookup"><span data-stu-id="d7987-116">When you use the `Microsoft.AspNetCore.All` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application &mdash; the .NET Core Runtime Store contains these assets.</span></span> <span data-ttu-id="d7987-117">Die Objekte im Laufzeitspeicher sind zur Verbesserung der Startzeit der Anwendung vorkompiliert.</span><span class="sxs-lookup"><span data-stu-id="d7987-117">The assets in the Runtime Store are precompiled to improve application startup time.</span></span>

<span data-ttu-id="d7987-118">Sie können den Trimmprozess für Pakete verwenden, um nicht verwendete Pakete zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="d7987-118">You can use the package trimming process to remove packages that you don't use.</span></span> <span data-ttu-id="d7987-119">Getrimmte Pakete werden aus der veröffentlichten Anwendungsausgabe ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="d7987-119">Trimmed packages are excluded in published application output.</span></span>

<span data-ttu-id="d7987-120">Die folgende *.csproj*-Datei verweist auf das Metapaket `Microsoft.AspNetCore.All` für ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="d7987-120">The following *.csproj* file references the `Microsoft.AspNetCore.All` metapackage for ASP.NET Core:</span></span>

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a><span data-ttu-id="d7987-121">Implizite Versionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="d7987-121">Implicit versioning</span></span>

<span data-ttu-id="d7987-122">In ASP.NET Core 2.1 oder höher können Sie den `Microsoft.AspNetCore.All`-Paketverweis ohne Version angeben.</span><span class="sxs-lookup"><span data-stu-id="d7987-122">In ASP.NET Core 2.1 or later, you can specify the `Microsoft.AspNetCore.All` package reference without a version.</span></span> <span data-ttu-id="d7987-123">Wenn die Version nicht angegeben wird, wird vom SDK eine implizite Version angegeben (`Microsoft.NET.Sdk.Web`).</span><span class="sxs-lookup"><span data-stu-id="d7987-123">When the version isn't specified, an implicit version is specified by the SDK (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="d7987-124">Es wird empfohlen, die vom SDK angegebene implizite Version beizubehalten, statt die Versionsnummer im Paketverweis explizit festzulegen.</span><span class="sxs-lookup"><span data-stu-id="d7987-124">We recommend relying on the implicit version specified by the SDK and not explicitly setting the version number on the package reference.</span></span> <span data-ttu-id="d7987-125">Wenn Sie Fragen zu dieser Vorgehensweise haben, können Sie einen GitHub-Kommentar unter [Discussion for the Microsoft.AspNetCore.App implicit version (Diskussion zur impliziten Version für Microsoft.AspNetCore.App)](https://github.com/aspnet/Docs/issues/6430) verfassen.</span><span class="sxs-lookup"><span data-stu-id="d7987-125">If you have questions about this approach, leave a GitHub comment at the [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430).</span></span>

<span data-ttu-id="d7987-126">Die implizite Version wird auf `major.minor.0` festgelegt, wenn es sich um Apps für Mobilgeräte handelt.</span><span class="sxs-lookup"><span data-stu-id="d7987-126">The implicit version is set to `major.minor.0` for portable apps.</span></span> <span data-ttu-id="d7987-127">Der Rollforwardmechanismus des freigegebenen Frameworks führt die App auf der neuesten kompatiblen Version der installierten freigegebenen Frameworks aus.</span><span class="sxs-lookup"><span data-stu-id="d7987-127">The shared framework roll-forward mechanism runs the app on the latest compatible version among the installed shared frameworks.</span></span> <span data-ttu-id="d7987-128">Stellen Sie sicher, dass die gleiche Version des freigegebenen Frameworks in allen Umgebungen installiert ist, um zu gewährleisten, dass die gleiche Version bei der Entwicklung, beim Testen und in der Produktion verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d7987-128">To guarantee the same version is used in development, test, and production, ensure the same version of the shared framework is installed in all environments.</span></span> <span data-ttu-id="d7987-129">Bei unabhängigen Apps wird die implizite Versionsnummer auf die Versionsnummer `major.minor.patch` des freigegebenen Frameworks festgelegt, das im installierten SDK zusammengefasst ist.</span><span class="sxs-lookup"><span data-stu-id="d7987-129">For self-contained apps, the implicit version number is set to the `major.minor.patch` of the shared framework bundled in the installed SDK.</span></span>

<span data-ttu-id="d7987-130">Das Angeben einer Versionsnummer im `Microsoft.AspNetCore.All`-Paketverweis garantiert **nicht**, dass diese Version des freigegebenen Frameworks ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="d7987-130">Specifying a version number on the `Microsoft.AspNetCore.All` package reference does **not** guarantee that version of the shared framework is chosen.</span></span> <span data-ttu-id="d7987-131">Gehen Sie beispielsweise davon aus, dass „2.1.1“ angegeben, aber „2.1.3“ installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d7987-131">For example, suppose version "2.1.1" is specified, but "2.1.3" is installed.</span></span> <span data-ttu-id="d7987-132">In diesem Fall verwendet die App Version 2.1.3.</span><span class="sxs-lookup"><span data-stu-id="d7987-132">In that case, the app will use "2.1.3".</span></span> <span data-ttu-id="d7987-133">Sie können den Rollforward (für „patch“ und/oder „minor“) deaktivieren. Dies wird jedoch nicht empfohlen.</span><span class="sxs-lookup"><span data-stu-id="d7987-133">Although not recommended, you can disable roll forward (patch and/or minor).</span></span> <span data-ttu-id="d7987-134">Weitere Informationen zum Rollforward des dotnet-Hosts und der Konfiguration seines Verhaltens finden Sie unter [dotnet host roll forward (Rollforward des dotnet-Hosts)](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span><span class="sxs-lookup"><span data-stu-id="d7987-134">For more information regarding dotnet host roll-forward and how to configure its behavior, see [dotnet host roll forward](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span></span>

<span data-ttu-id="d7987-135">Das SDK des Projekts muss in der Projektdatei auf `Microsoft.NET.Sdk.Web` festgelegt werden, damit die implizite Versionsverwaltung von `Microsoft.AspNetCore.All` verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="d7987-135">The project's SDK must be set to `Microsoft.NET.Sdk.Web` in the project file to use the implicit version of `Microsoft.AspNetCore.All`.</span></span> <span data-ttu-id="d7987-136">Wenn das SDK `Microsoft.NET.Sdk` festgelegt wird (`<Project Sdk="Microsoft.NET.Sdk">` ganz oben in der Projektdatei), wird die folgende Warnung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="d7987-136">When the `Microsoft.NET.Sdk` SDK is specified (`<Project Sdk="Microsoft.NET.Sdk">` at the top of the project file), the following warning is generated:</span></span>

<span data-ttu-id="d7987-137">*Warnung NU1604: Projektabhängigkeit "Microsoft.aspnetcore.All" enthält keine inklusive untere Grenze. Schließen Sie eine Untergrenze in die Abhängigkeitsversion ein, um konsistente Wiederherstellungsergebnisse zu erzielen.)*</span><span class="sxs-lookup"><span data-stu-id="d7987-137">*Warning NU1604: Project dependency Microsoft.AspNetCore.All does not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span>

<span data-ttu-id="d7987-138">Dies ist ein bekanntes Problem mit dem .NET Core 2.1 SDK und wird im .NET Core SDK 2.2 behoben.</span><span class="sxs-lookup"><span data-stu-id="d7987-138">This is a known issue with the .NET Core 2.1 SDK and will be fixed in the .NET Core 2.2 SDK.</span></span>

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a><span data-ttu-id="d7987-139">Migrieren von Microsoft.AspNetCore.All zu Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="d7987-139">Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App</span></span>

<span data-ttu-id="d7987-140">Folgende Pakete sind in `Microsoft.AspNetCore.All`, aber nicht in `Microsoft.AspNetCore.App` enthalten.</span><span class="sxs-lookup"><span data-stu-id="d7987-140">The following packages are included in `Microsoft.AspNetCore.All` but not the `Microsoft.AspNetCore.App` package.</span></span>

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

<span data-ttu-id="d7987-141">Wenn Sie von `Microsoft.AspNetCore.All` zu `Microsoft.AspNetCore.App` migrieren möchten und Ihre App APIs aus den oben aufgeführten Paketen verwendet, fügen Sie in Ihrem Projekt Verweise auf diese Pakete hinzu.</span><span class="sxs-lookup"><span data-stu-id="d7987-141">To move from `Microsoft.AspNetCore.All` to `Microsoft.AspNetCore.App`, if your app uses any APIs from the above packages, or packages brought in by those packages, add references to those packages in your project.</span></span>

<span data-ttu-id="d7987-142">Alle Abhängigkeiten der vorangehenden Pakete, die keine Abhängigkeiten von `Microsoft.AspNetCore.App` sind, sind nicht implizit enthalten.</span><span class="sxs-lookup"><span data-stu-id="d7987-142">Any dependencies of the preceding packages that otherwise aren't dependencies of `Microsoft.AspNetCore.App` are not included implicitly.</span></span> <span data-ttu-id="d7987-143">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d7987-143">For example:</span></span>

* <span data-ttu-id="d7987-144">`StackExchange.Redis` als Abhängigkeit von `Microsoft.Extensions.Caching.Redis`</span><span class="sxs-lookup"><span data-stu-id="d7987-144">`StackExchange.Redis` as a dependency of `Microsoft.Extensions.Caching.Redis`</span></span>
* <span data-ttu-id="d7987-145">`Microsoft.ApplicationInsights` als Abhängigkeit von `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`</span><span class="sxs-lookup"><span data-stu-id="d7987-145">`Microsoft.ApplicationInsights` as a dependency of `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`</span></span>

## <a name="update-aspnet-core-21"></a><span data-ttu-id="d7987-146">Aktualisieren von ASP.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="d7987-146">Update ASP.NET Core 2.1</span></span>

<span data-ttu-id="d7987-147">Wir empfehlen die Migration zum Metapaket `Microsoft.AspNetCore.App` für 2.1 oder höher.</span><span class="sxs-lookup"><span data-stu-id="d7987-147">We recommend migrating to the `Microsoft.AspNetCore.App` metapackage for 2.1 and later.</span></span> <span data-ttu-id="d7987-148">Wenn Sie das `Microsoft.AspNetCore.All`-Metapaket weiterhin verwenden und sicherstellen möchten, dass die neueste Patchversion bereitgestellt wird, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="d7987-148">To keep using the `Microsoft.AspNetCore.All` metapackage and ensure the latest patch version is deployed:</span></span>

* <span data-ttu-id="d7987-149">Auf dem Entwicklungscomputer und Buildserver: Installieren Sie das neueste [.NET Core SDK](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d7987-149">On development machines and build servers: Install the latest [.NET Core SDK](https://www.microsoft.com/net/download).</span></span>
* <span data-ttu-id="d7987-150">Auf Bereitstellungsservern: Installieren Sie das neueste [.NET Core-Runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d7987-150">On deployment servers: Install the latest [.NET Core runtime](https://www.microsoft.com/net/download).</span></span>
 <span data-ttu-id="d7987-151">Für Ihre App wird bei einem Neustart der Anwendungen ein Rollforward auf die neueste installierte Version ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d7987-151">Your app will roll forward to the latest installed version on an application restart.</span></span>
