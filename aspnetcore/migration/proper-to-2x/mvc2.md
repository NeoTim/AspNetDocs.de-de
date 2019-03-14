---
title: Migrieren von ASP.NET zu ASP.NET Core 2.0
author: isaac2004
description: Erhalten Sie Anleitungen zum Migrieren vorhandener ASP.NET MVC- oder Web-API-Anwendungen in ASP.NET Core 2.0.
ms.author: scaddie
ms.custom: mvc
ms.date: 10/24/2018
uid: migration/mvc2
ms.openlocfilehash: 9960932bd288ea12e346272f1838026778f1d355
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040007"
---
# <a name="migrate-from-aspnet-to-aspnet-core-20"></a><span data-ttu-id="89f84-103">Migrieren von ASP.NET zu ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="89f84-103">Migrate from ASP.NET to ASP.NET Core 2.0</span></span>

<span data-ttu-id="89f84-104">Von [Isaac Levin](https://isaaclevin.com)</span><span class="sxs-lookup"><span data-stu-id="89f84-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="89f84-105">Dieser Artikel dient als Leitfaden zum Migrieren von ASP.NET-Anwendungen zu ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="89f84-105">This article serves as a reference guide for migrating ASP.NET applications to ASP.NET Core 2.0.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89f84-106">Vorraussetzungen</span><span class="sxs-lookup"><span data-stu-id="89f84-106">Prerequisites</span></span>

<span data-ttu-id="89f84-107">Installieren Sie **eine** der folgenden Optionen aus [.NET Downloads: Windows](https://www.microsoft.com/net/download/windows):</span><span class="sxs-lookup"><span data-stu-id="89f84-107">Install **one** of the following from [.NET Downloads: Windows](https://www.microsoft.com/net/download/windows):</span></span>

* <span data-ttu-id="89f84-108">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="89f84-108">.NET Core SDK</span></span>
* <span data-ttu-id="89f84-109">Visual Studio für Windows</span><span class="sxs-lookup"><span data-stu-id="89f84-109">Visual Studio for Windows</span></span>
  * <span data-ttu-id="89f84-110">Workload **ASP.NET und Webentwicklung**</span><span class="sxs-lookup"><span data-stu-id="89f84-110">**ASP.NET and web development** workload</span></span>
  * <span data-ttu-id="89f84-111">Workload **Plattformübergreifende .NET Core-Entwicklung**</span><span class="sxs-lookup"><span data-stu-id="89f84-111">**.NET Core cross-platform development** workload</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="89f84-112">Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="89f84-112">Target frameworks</span></span>

<span data-ttu-id="89f84-113">ASP.NET Core 2.0-Projekte bieten Entwicklern die Flexibilität, Anwendungen für .NET Core, .NET Framework oder für beide Frameworks zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="89f84-113">ASP.NET Core 2.0 projects offer developers the flexibility of targeting .NET Core, .NET Framework, or both.</span></span> <span data-ttu-id="89f84-114">Informationen zur Auswahl eines geeigneten Frameworks finden Sie unter [Wahl zwischen .NET Core und .NET Framework für Server-Apps](/dotnet/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="89f84-114">See [Choosing between .NET Core and .NET Framework for server apps](/dotnet/standard/choosing-core-framework-server) to determine which target framework is most appropriate.</span></span>

<span data-ttu-id="89f84-115">Bei der Erstellung von Anwendungen für .NET Framework müssen Projekte auf einzelne NuGet-Pakete verweisen.</span><span class="sxs-lookup"><span data-stu-id="89f84-115">When targeting .NET Framework, projects need to reference individual NuGet packages.</span></span>

<span data-ttu-id="89f84-116">Wenn das Zielframework .NET Core ist, können Sie mit dem [Metapaket](xref:fundamentals/metapackage) für ASP.NET Core 2.0 auf die meisten expliziten Paketverweise verzichten.</span><span class="sxs-lookup"><span data-stu-id="89f84-116">Targeting .NET Core allows you to eliminate numerous explicit package references, thanks to the ASP.NET Core 2.0 [metapackage](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="89f84-117">Das `Microsoft.AspNetCore.All`-Metapaket können Sie folgendermaßen in Ihrem Projekt installieren:</span><span class="sxs-lookup"><span data-stu-id="89f84-117">Install the `Microsoft.AspNetCore.All` metapackage in your project:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.9" />
</ItemGroup>
```

<span data-ttu-id="89f84-118">Wenn das Metapaket verwendet wird, werden mit der Anwendung keine Pakete bereitgestellt, auf die im Metapaket verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="89f84-118">When the metapackage is used, no packages referenced in the metapackage are deployed with the app.</span></span> <span data-ttu-id="89f84-119">Die notwendigen Objekte sind im .NET Core-Laufzeitspeicher vorhanden und werden zur Verbesserung der Leistung vorkompiliert.</span><span class="sxs-lookup"><span data-stu-id="89f84-119">The .NET Core Runtime Store includes these assets, and they're precompiled to improve performance.</span></span> <span data-ttu-id="89f84-120">Finden Sie unter <xref:fundamentals/metapackage> Weitere Details.</span><span class="sxs-lookup"><span data-stu-id="89f84-120">See <xref:fundamentals/metapackage> for more detail.</span></span>

## <a name="project-structure-differences"></a><span data-ttu-id="89f84-121">Unterschiede bei Projektstrukturen</span><span class="sxs-lookup"><span data-stu-id="89f84-121">Project structure differences</span></span>

<span data-ttu-id="89f84-122">Das Dateiformat *.csproj* wurde in ASP.NET Core vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="89f84-122">The *.csproj* file format has been simplified in ASP.NET Core.</span></span> <span data-ttu-id="89f84-123">Zu einigen wichtigen Änderungen gehören folgende Punkte:</span><span class="sxs-lookup"><span data-stu-id="89f84-123">Some notable changes include:</span></span>

* <span data-ttu-id="89f84-124">Dateien müssen nicht explizit eingebunden werden, um als Teil des Projekts behandelt zu werden.</span><span class="sxs-lookup"><span data-stu-id="89f84-124">Explicit inclusion of files isn't necessary for them to be considered part of the project.</span></span> <span data-ttu-id="89f84-125">Dadurch wird in großen Entwicklerteams das Risiko von Konflikten beim Zusammenführen von XML-Dateien reduziert.</span><span class="sxs-lookup"><span data-stu-id="89f84-125">This reduces the risk of XML merge conflicts when working on large teams.</span></span>
* <span data-ttu-id="89f84-126">Auf GUID-Verweise zu anderen Projekten wird verzichtet, wodurch die Lesbarkeit von Dateien erhöht wird.</span><span class="sxs-lookup"><span data-stu-id="89f84-126">There are no GUID-based references to other projects, which improves file readability.</span></span>
* <span data-ttu-id="89f84-127">Die Datei kann bearbeitet werden, ohne in Visual Studio entladen zu werden:</span><span class="sxs-lookup"><span data-stu-id="89f84-127">The file can be edited without unloading it in Visual Studio:</span></span>

  ![Kontextmenüoption „Edit CSPROJ“ (CSPROJ-Datei bearbeiten) in Visual Studio 2017](_static/EditProjectVs2017.png)

## <a name="globalasax-file-replacement"></a><span data-ttu-id="89f84-129">Ersetzen der Datei „Global.asax“</span><span class="sxs-lookup"><span data-stu-id="89f84-129">Global.asax file replacement</span></span>

<span data-ttu-id="89f84-130">Mit ASP.NET Core wurde ein neuer Mechanismus für den Bootstrap einer Anwendung eingeführt.</span><span class="sxs-lookup"><span data-stu-id="89f84-130">ASP.NET Core introduced a new mechanism for bootstrapping an app.</span></span> <span data-ttu-id="89f84-131">Der Einstiegspunkt für ASP.NET-Anwendungen ist die Datei *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="89f84-131">The entry point for ASP.NET applications is the *Global.asax* file.</span></span> <span data-ttu-id="89f84-132">In der Datei *Global.asax* werden Aufgaben wie die Routenkonfiguration, die Einrichtung von Filtern und Bereichsregistrierungen bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="89f84-132">Tasks such as route configuration and filter and area registrations are handled in the *Global.asax* file.</span></span>

[!code-csharp[](samples/globalasax-sample.cs)]

<span data-ttu-id="89f84-133">Bei diesem Ansatz werden die Anwendung und der Server, auf dem die Anwendung bereitgestellt wird, so miteinander gekoppelt, dass es zu Konflikten mit der Implementierung kommt.</span><span class="sxs-lookup"><span data-stu-id="89f84-133">This approach couples the application and the server to which it's deployed in a way that interferes with the implementation.</span></span> <span data-ttu-id="89f84-134">[OWIN](http://owin.org/) wurde mit dem Ziel eingeführt, beide Komponenten zu entkoppeln und so mehrere Frameworks leichter gemeinsam verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="89f84-134">In an effort to decouple, [OWIN](http://owin.org/) was introduced to provide a cleaner way to use multiple frameworks together.</span></span> <span data-ttu-id="89f84-135">OWIN stellt eine Pipeline zur Verfügung, über die nur die benötigten Module hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="89f84-135">OWIN provides a pipeline to add only the modules needed.</span></span> <span data-ttu-id="89f84-136">Die Hostingumgebung verwendet eine [Startup](xref:fundamentals/startup)-Funktion, um Dienste und die Anforderungspipeline der Anwendung zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="89f84-136">The hosting environment takes a [Startup](xref:fundamentals/startup) function to configure services and the app's request pipeline.</span></span> <span data-ttu-id="89f84-137">`Startup` registriert die Middleware bei der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="89f84-137">`Startup` registers a set of middleware with the application.</span></span> <span data-ttu-id="89f84-138">Bei jeder Anforderung ruft die Anwendung alle Middlewarekomponenten auf, wobei der Hauptzeiger einer verknüpften Liste auf die vorhandenen Handler zeigt.</span><span class="sxs-lookup"><span data-stu-id="89f84-138">For each request, the application calls each of the middleware components with the head pointer of a linked list to an existing set of handlers.</span></span> <span data-ttu-id="89f84-139">Jede Middlewarekomponente kann einen oder mehrere Handler zur Anforderungspipeline hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="89f84-139">Each middleware component can add one or more handlers to the request handling pipeline.</span></span> <span data-ttu-id="89f84-140">Möglich wird dies, indem ein Verweis auf den Handler zurückgegeben wird, der zum neuen ersten Element der Liste wird.</span><span class="sxs-lookup"><span data-stu-id="89f84-140">This is accomplished by returning a reference to the handler that's the new head of the list.</span></span> <span data-ttu-id="89f84-141">Jeder Handler ist dafür verantwortlich, sich den nächsten Handler in der Liste zu merken und diesen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="89f84-141">Each handler is responsible for remembering and invoking the next handler in the list.</span></span> <span data-ttu-id="89f84-142">In ASP.NET Core ist `Startup` der Einstiegspunkt für eine Anwendung. Eine Abhängigkeit von *Global.asax* ist nicht mehr vorhanden.</span><span class="sxs-lookup"><span data-stu-id="89f84-142">With ASP.NET Core, the entry point to an application is `Startup`, and you no longer have a dependency on *Global.asax*.</span></span> <span data-ttu-id="89f84-143">Wenn Sie OWIN mit .NET Framework verwenden möchten, können Sie sich beispielsweise an folgendem Code für die Pipeline orientieren:</span><span class="sxs-lookup"><span data-stu-id="89f84-143">When using OWIN with .NET Framework, use something like the following as a pipeline:</span></span>

[!code-csharp[](samples/webapi-owin.cs)]

<span data-ttu-id="89f84-144">Hierdurch werden Ihre Standardrouten konfiguriert. Außerdem wird standardmäßig XmlSerialization anstelle von JSON verwendet.</span><span class="sxs-lookup"><span data-stu-id="89f84-144">This configures your default routes, and defaults to XmlSerialization over Json.</span></span> <span data-ttu-id="89f84-145">Bei Bedarf können Sie weitere Middleware (z.B. zum Laden von Diensten, für Konfigurationseinstellungen, für statische Dateien usw.) zur Pipeline hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="89f84-145">Add other Middleware to this pipeline as needed (loading services, configuration settings, static files, etc.).</span></span>

<span data-ttu-id="89f84-146">ASP.NET Core verwendet einen ähnlichen Ansatz, ist jedoch hinsichtlich des Einstiegspunkts nicht auf OWIN angewiesen.</span><span class="sxs-lookup"><span data-stu-id="89f84-146">ASP.NET Core uses a similar approach, but doesn't rely on OWIN to handle the entry.</span></span> <span data-ttu-id="89f84-147">Stattdessen kommt – ähnlich wie bei Konsolenanwendungen – in *Program.cs* die `Main`-Methode zum Einsatz, in der `Startup` geladen wird.</span><span class="sxs-lookup"><span data-stu-id="89f84-147">Instead, that's done through the *Program.cs* `Main` method (similar to console applications) and `Startup` is loaded through there.</span></span>

[!code-csharp[](samples/program.cs)]

<span data-ttu-id="89f84-148">In `Startup` muss die `Configure`-Methode enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="89f84-148">`Startup` must include a `Configure` method.</span></span> <span data-ttu-id="89f84-149">Fügen Sie in `Configure` der Pipeline die erforderliche Middleware hinzu.</span><span class="sxs-lookup"><span data-stu-id="89f84-149">In `Configure`, add the necessary middleware to the pipeline.</span></span> <span data-ttu-id="89f84-150">Im folgenden Beispiel, das der Standardwebsitevorlage entnommen wurde, werden mehrere Erweiterungsmethoden zum Konfigurieren der Pipeline verwendet. Hierdurch wird Folgendes unterstützt:</span><span class="sxs-lookup"><span data-stu-id="89f84-150">In the following example (from the default web site template), several extension methods are used to configure the pipeline with support for:</span></span>

* [<span data-ttu-id="89f84-151">BrowserLink</span><span class="sxs-lookup"><span data-stu-id="89f84-151">BrowserLink</span></span>](http://vswebessentials.com/features/browserlink)
* <span data-ttu-id="89f84-152">Fehlerseiten</span><span class="sxs-lookup"><span data-stu-id="89f84-152">Error pages</span></span>
* <span data-ttu-id="89f84-153">Statische Dateien</span><span class="sxs-lookup"><span data-stu-id="89f84-153">Static files</span></span>
* <span data-ttu-id="89f84-154">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="89f84-154">ASP.NET Core MVC</span></span>
* <span data-ttu-id="89f84-155">Identität</span><span class="sxs-lookup"><span data-stu-id="89f84-155">Identity</span></span>

[!code-csharp[](../../common/samples/WebApplication1/Startup.cs?highlight=8,9,10,14,17,19,21&start=58&end=84)]

<span data-ttu-id="89f84-156">Durch die Entkopplung von Host und Anwendung wird die Möglichkeit geschaffen, in der Zukunft eine Migration zu einer anderen Plattform vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="89f84-156">The host and application have been decoupled, which provides the flexibility of moving to a different platform in the future.</span></span>

<span data-ttu-id="89f84-157">Ausführliche Informationen zu ASP.NET Core-Start oder Middleware, finden Sie unter <xref:fundamentals/startup>.</span><span class="sxs-lookup"><span data-stu-id="89f84-157">For a more in-depth reference to ASP.NET Core Startup and Middleware, see <xref:fundamentals/startup>.</span></span>

## <a name="storing-configurations"></a><span data-ttu-id="89f84-158">Speichern von Konfigurationsdaten</span><span class="sxs-lookup"><span data-stu-id="89f84-158">Storing configurations</span></span>

<span data-ttu-id="89f84-159">ASP.NET unterstützt das Speichern von Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="89f84-159">ASP.NET supports storing settings.</span></span> <span data-ttu-id="89f84-160">Diese Einstellungen dienen z.B. der Unterstützung der Umgebung, in der die Anwendungen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="89f84-160">These setting are used, for example, to support the environment to which the applications were deployed.</span></span> <span data-ttu-id="89f84-161">Häufig werden alle benutzerdefinierten Schlüssel-Wert-Paare im Abschnitt `<appSettings>` der Datei *Web.config* gespeichert:</span><span class="sxs-lookup"><span data-stu-id="89f84-161">A common practice was to store all custom key-value pairs in the `<appSettings>` section of the *Web.config* file:</span></span>

[!code-xml[](samples/webconfig-sample.xml)]

<span data-ttu-id="89f84-162">Anwendungen lesen diese Einstellungen über die `ConfigurationManager.AppSettings`-Auflistung im `System.Configuration`-Namespace aus:</span><span class="sxs-lookup"><span data-stu-id="89f84-162">Applications read these settings using the `ConfigurationManager.AppSettings` collection in the `System.Configuration` namespace:</span></span>

[!code-csharp[](samples/read-webconfig.cs)]

<span data-ttu-id="89f84-163">ASP.NET Core kann Konfigurationsdaten der Anwendung in einer beliebigen Datei speichern und diese während des Middleware-Bootstraps laden.</span><span class="sxs-lookup"><span data-stu-id="89f84-163">ASP.NET Core can store configuration data for the application in any file and load them as part of middleware bootstrapping.</span></span> <span data-ttu-id="89f84-164">Die in Projektvorlagen verwendete Standarddatei ist *appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="89f84-164">The default file used in the project templates is *appsettings.json*:</span></span>

[!code-json[](samples/appsettings-sample.json)]

<span data-ttu-id="89f84-165">Diese Datei wird in Ihrer Anwendung in eine Instanz von `IConfiguration` in *Startup.cs* geladen:</span><span class="sxs-lookup"><span data-stu-id="89f84-165">Loading this file into an instance of `IConfiguration` inside your application is done in *Startup.cs*:</span></span>

[!code-csharp[](samples/startup-builder.cs)]

<span data-ttu-id="89f84-166">Die Anwendung liest aus `Configuration`, um die Einstellungen abzurufen:</span><span class="sxs-lookup"><span data-stu-id="89f84-166">The app reads from `Configuration` to get the settings:</span></span>

[!code-csharp[](samples/read-appsettings.cs)]

<span data-ttu-id="89f84-167">Dieser Ansatz kann erweitert werden, um einen noch stabileren Prozess zu gewährleisten. Beispielsweise kann über die [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) ein Dienst mit diesen Werten geladen werden.</span><span class="sxs-lookup"><span data-stu-id="89f84-167">There are extensions to this approach to make the process more robust, such as using [Dependency Injection](xref:fundamentals/dependency-injection) (DI) to load a service with these values.</span></span> <span data-ttu-id="89f84-168">Durch die Abhängigkeitsinjektion wird eine Reihe stark typisierter Konfigurationsobjekte zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="89f84-168">The DI approach provides a strongly-typed set of configuration objects.</span></span>

````csharp
// Assume AppConfiguration is a class representing a strongly-typed version of AppConfiguration section
services.Configure<AppConfiguration>(Configuration.GetSection("AppConfiguration"));
````

<span data-ttu-id="89f84-169">**Hinweis**: Ausführliche Informationen zur ASP.NET Core-Konfiguration, finden Sie unter <xref:fundamentals/configuration/index>.</span><span class="sxs-lookup"><span data-stu-id="89f84-169">**Note:** For a more in-depth reference to ASP.NET Core configuration, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="native-dependency-injection"></a><span data-ttu-id="89f84-170">Native Abhängigkeitsinjektion</span><span class="sxs-lookup"><span data-stu-id="89f84-170">Native dependency injection</span></span>

<span data-ttu-id="89f84-171">Ein wichtiges Ziel bei der Erstellung großer, skalierbarer Anwendungen besteht in der losen Kopplung von Komponenten und Diensten.</span><span class="sxs-lookup"><span data-stu-id="89f84-171">An important goal when building large, scalable applications is the loose coupling of components and services.</span></span> <span data-ttu-id="89f84-172">[Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) ist eine beliebte Methode hierfür, und es ist eine native Komponente von ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="89f84-172">[Dependency injection](xref:fundamentals/dependency-injection) is a popular technique for achieving this, and it's a native component of ASP.NET Core.</span></span>

<span data-ttu-id="89f84-173">In ASP.NET-Anwendungen greifen Entwickler in einer Drittanbieter-Bibliothek zum Implementieren von Abhängigkeitsinjektion zurück.</span><span class="sxs-lookup"><span data-stu-id="89f84-173">In ASP.NET applications, developers rely on a third-party library to implement dependency injection.</span></span> <span data-ttu-id="89f84-174">Eine solche Bibliothek ist [Unity](https://github.com/unitycontainer/unity), die von Microsoft Patterns & Practices bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="89f84-174">One such library is [Unity](https://github.com/unitycontainer/unity), provided by Microsoft Patterns & Practices.</span></span>

<span data-ttu-id="89f84-175">Ein Beispiel für das Einrichten der Abhängigkeitsinjektion mit Unity implementiert wird, `IDependencyResolver` , umschließt ein `UnityContainer`:</span><span class="sxs-lookup"><span data-stu-id="89f84-175">An example of setting up dependency injection with Unity is implementing `IDependencyResolver` that wraps a `UnityContainer`:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample8.cs)]

<span data-ttu-id="89f84-176">Erstellen Sie eine Instanz von `UnityContainer`, registrieren Sie den Dienst, und weisen Sie für Ihren Container den Abhängigkeitskonfliktlöser von `HttpConfiguration` der neuen Instanz von `UnityResolver` zu:</span><span class="sxs-lookup"><span data-stu-id="89f84-176">Create an instance of your `UnityContainer`, register your service, and set the dependency resolver of `HttpConfiguration` to the new instance of `UnityResolver` for your container:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample9.cs)]

<span data-ttu-id="89f84-177">Fügen Sie bei Bedarf `IProductRepository` ein:</span><span class="sxs-lookup"><span data-stu-id="89f84-177">Inject `IProductRepository` where needed:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample5.cs)]

<span data-ttu-id="89f84-178">Da es sich bei Dependency Injection Teil von ASP.NET Core ist, können Sie Ihren Dienst im Hinzufügen der `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="89f84-178">Because dependency injection is part of ASP.NET Core, you can add your service in the `Startup.ConfigureServices`:</span></span>

[!code-csharp[](samples/configure-services.cs)]

<span data-ttu-id="89f84-179">Genau wie bei Unity kann auch hier das Repository an einer beliebigen Stelle eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="89f84-179">The repository can be injected anywhere, as was true with Unity.</span></span>

<span data-ttu-id="89f84-180">Weitere Informationen zur Abhängigkeitsinjektion in ASP.NET Core finden Sie unter <xref:fundamentals/dependency-injection>.</span><span class="sxs-lookup"><span data-stu-id="89f84-180">For more information on dependency injection in ASP.NET Core, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="serving-static-files"></a><span data-ttu-id="89f84-181">Bereitstellen statischer Dateien</span><span class="sxs-lookup"><span data-stu-id="89f84-181">Serving static files</span></span>

<span data-ttu-id="89f84-182">Ein wichtiger Teil der Webentwicklung ist die Möglichkeit, statische, clientseitige Objekte bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="89f84-182">An important part of web development is the ability to serve static, client-side assets.</span></span> <span data-ttu-id="89f84-183">Die häufigsten Beispiele für statische Dateien sind HTML-, CSS-, JavaScript- und Bilddateien.</span><span class="sxs-lookup"><span data-stu-id="89f84-183">The most common examples of static files are HTML, CSS, Javascript, and images.</span></span> <span data-ttu-id="89f84-184">Diese Dateien müssen am veröffentlichten Speicherort der Anwendung (oder des CDN) gespeichert werden. Außerdem muss auf diese verwiesen werden, damit sie von einer Anforderung geladen werden können.</span><span class="sxs-lookup"><span data-stu-id="89f84-184">These files need to be saved in the published location of the app (or CDN) and referenced so they can be loaded by a request.</span></span> <span data-ttu-id="89f84-185">Dieser Prozess wurde in ASP.NET Core geändert.</span><span class="sxs-lookup"><span data-stu-id="89f84-185">This process has changed in ASP.NET Core.</span></span>

<span data-ttu-id="89f84-186">Statische Dateien werden in ASP.NET in verschiedenen Verzeichnissen gespeichert. Der Verweis auf die Dateien erfolgt in den Ansichten.</span><span class="sxs-lookup"><span data-stu-id="89f84-186">In ASP.NET, static files are stored in various directories and referenced in the views.</span></span>

<span data-ttu-id="89f84-187">In ASP.NET Core werden statische Dateien im Webstammverzeichnis (*&lt;content root&gt;/wwwroot*) gespeichert, falls keine anderen Einstellungen vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="89f84-187">In ASP.NET Core, static files are stored in the "web root" (*&lt;content root&gt;/wwwroot*), unless configured otherwise.</span></span> <span data-ttu-id="89f84-188">Die Dateien werden über den Aufruf der Erweiterungsmethode `UseStaticFiles` aus `Startup.Configure` in die Anforderungspipeline geladen:</span><span class="sxs-lookup"><span data-stu-id="89f84-188">The files are loaded into the request pipeline by invoking the `UseStaticFiles` extension method from `Startup.Configure`:</span></span>

[!code-csharp[](../../fundamentals/static-files/samples/1x/StartupStaticFiles.cs?highlight=3&name=snippet_ConfigureMethod)]

<span data-ttu-id="89f84-189">**Hinweis**: Wenn Sie Anwendungen für .NET Framework entwickeln, installieren Sie das NuGet-Paket `Microsoft.AspNetCore.StaticFiles`.</span><span class="sxs-lookup"><span data-stu-id="89f84-189">**Note:** If targeting .NET Framework, install the NuGet package `Microsoft.AspNetCore.StaticFiles`.</span></span>

<span data-ttu-id="89f84-190">Beispielsweise kann ein Browser an einem Speicherort wie `http://<app>/images/<imageFileName>` auf ein Bildobjekt im Ordner *wwwroot/images* zugreifen.</span><span class="sxs-lookup"><span data-stu-id="89f84-190">For example, an image asset in the *wwwroot/images* folder is accessible to the browser at a location such as `http://<app>/images/<imageFileName>`.</span></span>

<span data-ttu-id="89f84-191">**Hinweis**: Ausführliche Informationen zum Bereitstellen statischer Dateien in ASP.NET Core, finden Sie unter <xref:fundamentals/static-files>.</span><span class="sxs-lookup"><span data-stu-id="89f84-191">**Note:** For a more in-depth reference to serving static files in ASP.NET Core, see <xref:fundamentals/static-files>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89f84-192">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="89f84-192">Additional resources</span></span>

* [<span data-ttu-id="89f84-193">Portieren auf .NET Core – Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="89f84-193">Porting Libraries to .NET Core</span></span>](/dotnet/core/porting/libraries)
