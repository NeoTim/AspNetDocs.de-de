---
title: Migrieren von ASP.NET zu ASP.NET Core
author: isaac2004
description: Anweisungen zum Migrieren vorhandener ASP.NET MVC- oder Web-API-Apps zu ASP.NET Core Web.
ms.author: scaddie
ms.date: 12/11/2018
uid: migration/proper-to-2x/index
---
# <a name="migrate-from-aspnet-to-aspnet-core"></a><span data-ttu-id="d9740-103">Migration von ASP.NET zu ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d9740-103">Migrate from ASP.NET to ASP.NET Core</span></span>

<span data-ttu-id="d9740-104">Von [Isaac Levin](https://isaaclevin.com)</span><span class="sxs-lookup"><span data-stu-id="d9740-104">By [Isaac Levin](https://isaaclevin.com)</span></span>

<span data-ttu-id="d9740-105">Dieser Artikel dient als Leitfaden zum Migrieren von ASP.NET-Anwendungen zu ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d9740-105">This article serves as a reference guide for migrating ASP.NET apps to ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9740-106">Vorraussetzungen</span><span class="sxs-lookup"><span data-stu-id="d9740-106">Prerequisites</span></span>

[<span data-ttu-id="d9740-107">.NET Core SDK 2.2 oder höher</span><span class="sxs-lookup"><span data-stu-id="d9740-107">.NET Core SDK 2.2 or later</span></span>](https://www.microsoft.com/net/download)

## <a name="target-frameworks"></a><span data-ttu-id="d9740-108">Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="d9740-108">Target frameworks</span></span>

<span data-ttu-id="d9740-109">ASP.NET Core-Projekte bieten Entwicklern die Flexibilität, Anwendungen für .NET Core, .NET Framework oder für beide Frameworks zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d9740-109">ASP.NET Core projects offer developers the flexibility of targeting .NET Core, .NET Framework, or both.</span></span> <span data-ttu-id="d9740-110">Informationen zur Auswahl eines geeigneten Frameworks finden Sie unter [Wahl zwischen .NET Core und .NET Framework für Server-Apps](/dotnet/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="d9740-110">See [Choosing between .NET Core and .NET Framework for server apps](/dotnet/standard/choosing-core-framework-server) to determine which target framework is most appropriate.</span></span>

<span data-ttu-id="d9740-111">Bei der Erstellung von Anwendungen für .NET Framework müssen Projekte auf einzelne NuGet-Pakete verweisen.</span><span class="sxs-lookup"><span data-stu-id="d9740-111">When targeting .NET Framework, projects need to reference individual NuGet packages.</span></span>

<span data-ttu-id="d9740-112">Wenn das Zielframework .NET Core ist, können Sie mit dem [Metapaket](xref:fundamentals/metapackage-app) für ASP.NET Core auf die meisten expliziten Paketverweise verzichten.</span><span class="sxs-lookup"><span data-stu-id="d9740-112">Targeting .NET Core allows you to eliminate numerous explicit package references, thanks to the ASP.NET Core [metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="d9740-113">Das `Microsoft.AspNetCore.App`-Metapaket können Sie folgendermaßen in Ihrem Projekt installieren:</span><span class="sxs-lookup"><span data-stu-id="d9740-113">Install the `Microsoft.AspNetCore.App` metapackage in your project:</span></span>

```xml
<ItemGroup>
   <PackageReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>
```

<span data-ttu-id="d9740-114">Wenn das Metapaket verwendet wird, werden mit der Anwendung keine Pakete bereitgestellt, auf die im Metapaket verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="d9740-114">When the metapackage is used, no packages referenced in the metapackage are deployed with the app.</span></span> <span data-ttu-id="d9740-115">Die notwendigen Objekte sind im .NET Core-Laufzeitspeicher vorhanden und werden zur Verbesserung der Leistung vorkompiliert.</span><span class="sxs-lookup"><span data-stu-id="d9740-115">The .NET Core Runtime Store includes these assets, and they're precompiled to improve performance.</span></span> <span data-ttu-id="d9740-116">Weitere Informationen finden Sie unter [Das Metapaket „Microsoft.AspNetCore.App“ für ASP.NET Core 2.1](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="d9740-116">See [Microsoft.AspNetCore.App metapackage for ASP.NET Core](xref:fundamentals/metapackage-app) for more detail.</span></span>

## <a name="project-structure-differences"></a><span data-ttu-id="d9740-117">Unterschiede bei Projektstrukturen</span><span class="sxs-lookup"><span data-stu-id="d9740-117">Project structure differences</span></span>

<span data-ttu-id="d9740-118">Das Dateiformat *.csproj* wurde in ASP.NET Core vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="d9740-118">The *.csproj* file format has been simplified in ASP.NET Core.</span></span> <span data-ttu-id="d9740-119">Zu einigen wichtigen Änderungen gehören folgende Punkte:</span><span class="sxs-lookup"><span data-stu-id="d9740-119">Some notable changes include:</span></span>

- <span data-ttu-id="d9740-120">Dateien müssen nicht explizit eingebunden werden, um als Teil des Projekts behandelt zu werden.</span><span class="sxs-lookup"><span data-stu-id="d9740-120">Explicit inclusion of files isn't necessary for them to be considered part of the project.</span></span> <span data-ttu-id="d9740-121">Dadurch wird in großen Entwicklerteams das Risiko von Konflikten beim Zusammenführen von XML-Dateien reduziert.</span><span class="sxs-lookup"><span data-stu-id="d9740-121">This reduces the risk of XML merge conflicts when working on large teams.</span></span>
- <span data-ttu-id="d9740-122">Auf GUID-Verweise zu anderen Projekten wird verzichtet, wodurch die Lesbarkeit von Dateien erhöht wird.</span><span class="sxs-lookup"><span data-stu-id="d9740-122">There are no GUID-based references to other projects, which improves file readability.</span></span>
- <span data-ttu-id="d9740-123">Die Datei kann bearbeitet werden, ohne in Visual Studio entladen zu werden:</span><span class="sxs-lookup"><span data-stu-id="d9740-123">The file can be edited without unloading it in Visual Studio:</span></span>

    ![Kontextmenüoption „Edit CSPROJ“ (CSPROJ-Datei bearbeiten) in Visual Studio 2017](_static/EditProjectVs2017.png)

## <a name="globalasax-file-replacement"></a><span data-ttu-id="d9740-125">Ersetzen der Datei „Global.asax“</span><span class="sxs-lookup"><span data-stu-id="d9740-125">Global.asax file replacement</span></span>

<span data-ttu-id="d9740-126">Mit ASP.NET Core wurde ein neuer Mechanismus für den Bootstrap einer Anwendung eingeführt.</span><span class="sxs-lookup"><span data-stu-id="d9740-126">ASP.NET Core introduced a new mechanism for bootstrapping an app.</span></span> <span data-ttu-id="d9740-127">Der Einstiegspunkt für ASP.NET-Anwendungen ist die Datei *Global.asax*.</span><span class="sxs-lookup"><span data-stu-id="d9740-127">The entry point for ASP.NET applications is the *Global.asax* file.</span></span> <span data-ttu-id="d9740-128">In der Datei *Global.asax* werden Aufgaben wie die Routenkonfiguration, die Einrichtung von Filtern und Bereichsregistrierungen bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="d9740-128">Tasks such as route configuration and filter and area registrations are handled in the *Global.asax* file.</span></span>

[!code-csharp[](samples/globalasax-sample.cs)]

<span data-ttu-id="d9740-129">Bei diesem Ansatz werden die Anwendung und der Server, auf dem die Anwendung bereitgestellt wird, so miteinander gekoppelt, dass es zu Konflikten mit der Implementierung kommt.</span><span class="sxs-lookup"><span data-stu-id="d9740-129">This approach couples the application and the server to which it's deployed in a way that interferes with the implementation.</span></span> <span data-ttu-id="d9740-130">[OWIN](http://owin.org/) wurde mit dem Ziel eingeführt, beide Komponenten zu entkoppeln und so mehrere Frameworks leichter gemeinsam verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="d9740-130">In an effort to decouple, [OWIN](http://owin.org/) was introduced to provide a cleaner way to use multiple frameworks together.</span></span> <span data-ttu-id="d9740-131">OWIN stellt eine Pipeline zur Verfügung, über die nur die benötigten Module hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="d9740-131">OWIN provides a pipeline to add only the modules needed.</span></span> <span data-ttu-id="d9740-132">Die Hostingumgebung verwendet eine [Startup](xref:fundamentals/startup)-Funktion, um Dienste und die Anforderungspipeline der Anwendung zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d9740-132">The hosting environment takes a [Startup](xref:fundamentals/startup) function to configure services and the app's request pipeline.</span></span> <span data-ttu-id="d9740-133">`Startup` registriert die Middleware bei der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="d9740-133">`Startup` registers a set of middleware with the application.</span></span> <span data-ttu-id="d9740-134">Bei jeder Anforderung ruft die Anwendung alle Middlewarekomponenten auf, wobei der Hauptzeiger einer verknüpften Liste auf die vorhandenen Handler zeigt.</span><span class="sxs-lookup"><span data-stu-id="d9740-134">For each request, the application calls each of the middleware components with the head pointer of a linked list to an existing set of handlers.</span></span> <span data-ttu-id="d9740-135">Jede Middlewarekomponente kann einen oder mehrere Handler zur Anforderungspipeline hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d9740-135">Each middleware component can add one or more handlers to the request handling pipeline.</span></span> <span data-ttu-id="d9740-136">Möglich wird dies, indem ein Verweis auf den Handler zurückgegeben wird, der zum neuen ersten Element der Liste wird.</span><span class="sxs-lookup"><span data-stu-id="d9740-136">This is accomplished by returning a reference to the handler that's the new head of the list.</span></span> <span data-ttu-id="d9740-137">Jeder Handler ist dafür verantwortlich, sich den nächsten Handler in der Liste zu merken und diesen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="d9740-137">Each handler is responsible for remembering and invoking the next handler in the list.</span></span> <span data-ttu-id="d9740-138">In ASP.NET Core ist `Startup` der Einstiegspunkt für eine Anwendung. Eine Abhängigkeit von *Global.asax* ist nicht mehr vorhanden.</span><span class="sxs-lookup"><span data-stu-id="d9740-138">With ASP.NET Core, the entry point to an application is `Startup`, and you no longer have a dependency on *Global.asax*.</span></span> <span data-ttu-id="d9740-139">Wenn Sie OWIN mit .NET Framework verwenden möchten, können Sie sich beispielsweise an folgendem Code für die Pipeline orientieren:</span><span class="sxs-lookup"><span data-stu-id="d9740-139">When using OWIN with .NET Framework, use something like the following as a pipeline:</span></span>

[!code-csharp[](samples/webapi-owin.cs)]

<span data-ttu-id="d9740-140">Hierdurch werden Ihre Standardrouten konfiguriert. Außerdem wird standardmäßig XmlSerialization anstelle von JSON verwendet.</span><span class="sxs-lookup"><span data-stu-id="d9740-140">This configures your default routes, and defaults to XmlSerialization over Json.</span></span> <span data-ttu-id="d9740-141">Bei Bedarf können Sie weitere Middleware (z.B. zum Laden von Diensten, für Konfigurationseinstellungen, für statische Dateien usw.) zur Pipeline hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d9740-141">Add other Middleware to this pipeline as needed (loading services, configuration settings, static files, etc.).</span></span>

<span data-ttu-id="d9740-142">ASP.NET Core verwendet einen ähnlichen Ansatz, ist jedoch hinsichtlich des Einstiegspunkts nicht auf OWIN angewiesen.</span><span class="sxs-lookup"><span data-stu-id="d9740-142">ASP.NET Core uses a similar approach, but doesn't rely on OWIN to handle the entry.</span></span> <span data-ttu-id="d9740-143">Stattdessen kommt – ähnlich wie bei Konsolenanwendungen – in *Program.cs* die `Main`-Methode zum Einsatz, in der `Startup` geladen wird.</span><span class="sxs-lookup"><span data-stu-id="d9740-143">Instead, that's done through the *Program.cs* `Main` method (similar to console applications) and `Startup` is loaded through there.</span></span>

[!code-csharp[](samples/program.cs)]

<span data-ttu-id="d9740-144">In `Startup` muss die `Configure`-Methode enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="d9740-144">`Startup` must include a `Configure` method.</span></span> <span data-ttu-id="d9740-145">Fügen Sie in `Configure` der Pipeline die erforderliche Middleware hinzu.</span><span class="sxs-lookup"><span data-stu-id="d9740-145">In `Configure`, add the necessary middleware to the pipeline.</span></span> <span data-ttu-id="d9740-146">Im folgenden Beispiel, das der Standardwebsitevorlage entnommen wurde, konfigurieren Erweiterungsmethoden die Pipeline mit Unterstützung für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d9740-146">In the following example (from the default web site template), extension methods configure the pipeline with support for:</span></span>

* <span data-ttu-id="d9740-147">Fehlerseiten</span><span class="sxs-lookup"><span data-stu-id="d9740-147">Error pages</span></span>
* <span data-ttu-id="d9740-148">HTTP Strict Transport Security</span><span class="sxs-lookup"><span data-stu-id="d9740-148">HTTP Strict Transport Security</span></span>
* <span data-ttu-id="d9740-149">HTTP-Umleitung zu HTTPS</span><span class="sxs-lookup"><span data-stu-id="d9740-149">HTTP redirection to HTTPS</span></span>
* <span data-ttu-id="d9740-150">ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="d9740-150">ASP.NET Core MVC</span></span>

[!code-csharp[](samples/startup.cs)]

<span data-ttu-id="d9740-151">Durch die Entkopplung von Host und Anwendung wird die Möglichkeit geschaffen, in der Zukunft eine Migration zu einer anderen Plattform vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="d9740-151">The host and application have been decoupled, which provides the flexibility of moving to a different platform in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="d9740-152">Ausführliche Informationen zum Start einer Anwendung in ASP.NET Core und zu Middleware finden Sie unter [Startup in ASP.NET Core (Starten von Anwendungen in ASP.NET Core)](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="d9740-152">For a more in-depth reference to ASP.NET Core Startup and Middleware, see [Startup in ASP.NET Core](xref:fundamentals/startup)</span></span>

## <a name="store-configurations"></a><span data-ttu-id="d9740-153">Speicherkonfigurationen</span><span class="sxs-lookup"><span data-stu-id="d9740-153">Store configurations</span></span>

<span data-ttu-id="d9740-154">ASP.NET unterstützt das Speichern von Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="d9740-154">ASP.NET supports storing settings.</span></span> <span data-ttu-id="d9740-155">Diese Einstellungen dienen z.B. der Unterstützung der Umgebung, in der die Anwendungen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="d9740-155">These setting are used, for example, to support the environment to which the applications were deployed.</span></span> <span data-ttu-id="d9740-156">Häufig werden alle benutzerdefinierten Schlüssel-Wert-Paare im Abschnitt `<appSettings>` der Datei *Web.config* gespeichert:</span><span class="sxs-lookup"><span data-stu-id="d9740-156">A common practice was to store all custom key-value pairs in the `<appSettings>` section of the *Web.config* file:</span></span>

[!code-xml[](samples/webconfig-sample.xml)]

<span data-ttu-id="d9740-157">Anwendungen lesen diese Einstellungen über die `ConfigurationManager.AppSettings`-Auflistung im `System.Configuration`-Namespace aus:</span><span class="sxs-lookup"><span data-stu-id="d9740-157">Applications read these settings using the `ConfigurationManager.AppSettings` collection in the `System.Configuration` namespace:</span></span>

[!code-csharp[](samples/read-webconfig.cs)]

<span data-ttu-id="d9740-158">ASP.NET Core kann Konfigurationsdaten der Anwendung in einer beliebigen Datei speichern und diese während des Middleware-Bootstraps laden.</span><span class="sxs-lookup"><span data-stu-id="d9740-158">ASP.NET Core can store configuration data for the application in any file and load them as part of middleware bootstrapping.</span></span> <span data-ttu-id="d9740-159">Die in Projektvorlagen verwendete Standarddatei ist *appsettings.json*:</span><span class="sxs-lookup"><span data-stu-id="d9740-159">The default file used in the project templates is *appsettings.json*:</span></span>

[!code-json[](samples/appsettings-sample.json)]

<span data-ttu-id="d9740-160">Diese Datei wird in Ihrer Anwendung in eine Instanz von `IConfiguration` in *Startup.cs* geladen:</span><span class="sxs-lookup"><span data-stu-id="d9740-160">Loading this file into an instance of `IConfiguration` inside your application is done in *Startup.cs*:</span></span>

[!code-csharp[](samples/startup-builder.cs)]

<span data-ttu-id="d9740-161">Die Anwendung liest aus `Configuration`, um die Einstellungen abzurufen:</span><span class="sxs-lookup"><span data-stu-id="d9740-161">The app reads from `Configuration` to get the settings:</span></span>

[!code-csharp[](samples/read-appsettings.cs)]

<span data-ttu-id="d9740-162">Dieser Ansatz kann erweitert werden, um einen noch stabileren Prozess zu gewährleisten. Beispielsweise kann über die [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) ein Dienst mit diesen Werten geladen werden.</span><span class="sxs-lookup"><span data-stu-id="d9740-162">There are extensions to this approach to make the process more robust, such as using [Dependency Injection](xref:fundamentals/dependency-injection) (DI) to load a service with these values.</span></span> <span data-ttu-id="d9740-163">Durch die Abhängigkeitsinjektion wird eine Reihe stark typisierter Konfigurationsobjekte zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="d9740-163">The DI approach provides a strongly-typed set of configuration objects.</span></span>

````csharp
// Assume AppConfiguration is a class representing a strongly-typed version of AppConfiguration section
services.Configure<AppConfiguration>(Configuration.GetSection("AppConfiguration"));
````

> [!NOTE]
> <span data-ttu-id="d9740-164">Ausführliche Informationen zur ASP.NET Core-Konfiguration finden Sie unter [Configuration in ASP.NET Core (Konfiguration in ASP.NET Core)](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="d9740-164">For a more in-depth reference to ASP.NET Core configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

## <a name="native-dependency-injection"></a><span data-ttu-id="d9740-165">Native Abhängigkeitsinjektion</span><span class="sxs-lookup"><span data-stu-id="d9740-165">Native dependency injection</span></span>

<span data-ttu-id="d9740-166">Ein wichtiges Ziel bei der Erstellung großer, skalierbarer Anwendungen besteht in der losen Kopplung von Komponenten und Diensten.</span><span class="sxs-lookup"><span data-stu-id="d9740-166">An important goal when building large, scalable applications is the loose coupling of components and services.</span></span> <span data-ttu-id="d9740-167">Die [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) ist hierfür eine beliebte Methode und eine native Komponente von ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d9740-167">[Dependency Injection](xref:fundamentals/dependency-injection) is a popular technique for achieving this, and it's a native component of ASP.NET Core.</span></span>

<span data-ttu-id="d9740-168">Zur Implementierung der Dependency Injection greifen Entwickler in ASP.NET-Anwendungen auf Bibliotheken von Drittanbietern zurück.</span><span class="sxs-lookup"><span data-stu-id="d9740-168">In ASP.NET apps, developers rely on a third-party library to implement Dependency Injection.</span></span> <span data-ttu-id="d9740-169">Eine solche Bibliothek ist [Unity](https://github.com/unitycontainer/unity), die von Microsoft Patterns & Practices bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="d9740-169">One such library is [Unity](https://github.com/unitycontainer/unity), provided by Microsoft Patterns & Practices.</span></span>

<span data-ttu-id="d9740-170">Ein Beispiel für das Einrichten der Abhängigkeitsinjektion mit Unity ist die Implementierung der Schnittstelle `IDependencyResolver`, die einen `UnityContainer` umschließt:</span><span class="sxs-lookup"><span data-stu-id="d9740-170">An example of setting up Dependency Injection with Unity is implementing `IDependencyResolver` that wraps a `UnityContainer`:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample8.cs)]

<span data-ttu-id="d9740-171">Erstellen Sie eine Instanz von `UnityContainer`, registrieren Sie den Dienst, und weisen Sie für Ihren Container den Abhängigkeitskonfliktlöser von `HttpConfiguration` der neuen Instanz von `UnityResolver` zu:</span><span class="sxs-lookup"><span data-stu-id="d9740-171">Create an instance of your `UnityContainer`, register your service, and set the dependency resolver of `HttpConfiguration` to the new instance of `UnityResolver` for your container:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample9.cs)]

<span data-ttu-id="d9740-172">Fügen Sie bei Bedarf `IProductRepository` ein:</span><span class="sxs-lookup"><span data-stu-id="d9740-172">Inject `IProductRepository` where needed:</span></span>

[!code-csharp[](../../../aspnet/web-api/overview/advanced/dependency-injection/samples/sample5.cs)]

<span data-ttu-id="d9740-173">Da die Abhängigkeitsinjektion eine Komponente von ASP.NET Core ist, können Sie Ihren Dienst in *Startup.cs* der Methode `ConfigureServices` hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="d9740-173">Because Dependency Injection is part of ASP.NET Core, you can add your service in the `ConfigureServices` method of *Startup.cs*:</span></span>

[!code-csharp[](samples/configure-services.cs)]

<span data-ttu-id="d9740-174">Genau wie bei Unity kann auch hier das Repository an einer beliebigen Stelle eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="d9740-174">The repository can be injected anywhere, as was true with Unity.</span></span>

> [!NOTE]
> <span data-ttu-id="d9740-175">Weitere Informationen zur Dependency Injection finden Sie unter [Dependency Injection](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="d9740-175">For more information on dependency injection, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="serve-static-files"></a><span data-ttu-id="d9740-176">Bereitstellen statischer Dateien</span><span class="sxs-lookup"><span data-stu-id="d9740-176">Serve static files</span></span>

<span data-ttu-id="d9740-177">Ein wichtiger Teil der Webentwicklung ist die Möglichkeit, statische, clientseitige Objekte bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="d9740-177">An important part of web development is the ability to serve static, client-side assets.</span></span> <span data-ttu-id="d9740-178">Die häufigsten Beispiele für statische Dateien sind HTML-, CSS-, JavaScript- und Bilddateien.</span><span class="sxs-lookup"><span data-stu-id="d9740-178">The most common examples of static files are HTML, CSS, Javascript, and images.</span></span> <span data-ttu-id="d9740-179">Diese Dateien müssen am veröffentlichten Speicherort der Anwendung (oder des CDN) gespeichert werden. Außerdem muss auf diese verwiesen werden, damit sie von einer Anforderung geladen werden können.</span><span class="sxs-lookup"><span data-stu-id="d9740-179">These files need to be saved in the published location of the app (or CDN) and referenced so they can be loaded by a request.</span></span> <span data-ttu-id="d9740-180">Dieser Prozess wurde in ASP.NET Core geändert.</span><span class="sxs-lookup"><span data-stu-id="d9740-180">This process has changed in ASP.NET Core.</span></span>

<span data-ttu-id="d9740-181">Statische Dateien werden in ASP.NET in verschiedenen Verzeichnissen gespeichert. Der Verweis auf die Dateien erfolgt in den Ansichten.</span><span class="sxs-lookup"><span data-stu-id="d9740-181">In ASP.NET, static files are stored in various directories and referenced in the views.</span></span>

<span data-ttu-id="d9740-182">In ASP.NET Core werden statische Dateien im Webstammverzeichnis (*&lt;content root&gt;/wwwroot*) gespeichert, falls keine anderen Einstellungen vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="d9740-182">In ASP.NET Core, static files are stored in the "web root" (*&lt;content root&gt;/wwwroot*), unless configured otherwise.</span></span> <span data-ttu-id="d9740-183">Die Dateien werden über den Aufruf der Erweiterungsmethode `UseStaticFiles` aus `Startup.Configure` in die Anforderungspipeline geladen:</span><span class="sxs-lookup"><span data-stu-id="d9740-183">The files are loaded into the request pipeline by invoking the `UseStaticFiles` extension method from `Startup.Configure`:</span></span>

[!code-csharp[](../../fundamentals/static-files/samples/1x/StartupStaticFiles.cs?highlight=3&name=snippet_ConfigureMethod)]

> [!NOTE]
> <span data-ttu-id="d9740-184">Wenn Sie Anwendungen für .NET Framework entwickeln, installieren Sie das NuGet-Paket `Microsoft.AspNetCore.StaticFiles`.</span><span class="sxs-lookup"><span data-stu-id="d9740-184">If targeting .NET Framework, install the NuGet package `Microsoft.AspNetCore.StaticFiles`.</span></span>

<span data-ttu-id="d9740-185">Beispielsweise kann ein Browser an einem Speicherort wie `http://<app>/images/<imageFileName>` auf ein Bildobjekt im Ordner *wwwroot/images* zugreifen.</span><span class="sxs-lookup"><span data-stu-id="d9740-185">For example, an image asset in the *wwwroot/images* folder is accessible to the browser at a location such as `http://<app>/images/<imageFileName>`.</span></span>

> [!NOTE]
> <span data-ttu-id="d9740-186">Ausführliche Informationen zum Bereitstellen statischer Dateien in ASP.NET Core finden Sie im Artikel zu [statischen Dateien](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="d9740-186">For a more in-depth reference to serving static files in ASP.NET Core, see [Static files](xref:fundamentals/static-files).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9740-187">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d9740-187">Additional resources</span></span>

- [<span data-ttu-id="d9740-188">Portieren auf .NET Core – Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="d9740-188">Porting Libraries to .NET Core</span></span>](/dotnet/core/porting/libraries)
