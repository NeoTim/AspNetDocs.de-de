---
title: Einführung in Blazor
author: guardrex
description: 'Entdecken Sie ASP.NET Core Blazor, eine neue Möglichkeit, interaktive clientseitige Apps mit .NET zu erstellen, die im Browser mit WebAssembly ausgeführt werden.'
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: spa/blazor/index
---
# <a name="introduction-to-blazor"></a><span data-ttu-id="6fa35-103">Einführung in Blazor</span><span class="sxs-lookup"><span data-stu-id="6fa35-103">Introduction to Blazor</span></span>

<span data-ttu-id="6fa35-104">Von [Daniel Roth](https://github.com/danroth27) und [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6fa35-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="6fa35-105">Blazor ist ein Single-Page-App-Framework zum Erstellen von interaktiven clientseitigen Web-Apps mit .NET.</span><span class="sxs-lookup"><span data-stu-id="6fa35-105">Blazor is a single-page app framework for building interactive client-side Web apps with .NET.</span></span> <span data-ttu-id="6fa35-106">Blazor verwendet offene Webstandards ohne Plug-Ins oder Codetranspilation.</span><span class="sxs-lookup"><span data-stu-id="6fa35-106">Blazor uses open web standards without plugins or code transpilation.</span></span> <span data-ttu-id="6fa35-107">Dieses Framework funktioniert in allen modernen Webbrowsern, einschließlich mobiler Browser.</span><span class="sxs-lookup"><span data-stu-id="6fa35-107">Blazor works in all modern web browsers, including mobile browsers.</span></span>

<span data-ttu-id="6fa35-108">Die Verwendung von .NET im Browser für die clientseitige Webentwicklung bietet viele Vorteile:</span><span class="sxs-lookup"><span data-stu-id="6fa35-108">Using .NET in the browser for client-side web development offers many advantages:</span></span>

* <span data-ttu-id="6fa35-109">**C#-Sprache**: Schreiben Sie Code in C# anstatt in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6fa35-109">**C# language**: Write code in C# instead of JavaScript.</span></span>
* <span data-ttu-id="6fa35-110">**.NET-Ökosystem**: Nutzen Sie das vorhandene Ökosystem von .NET-Bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="6fa35-110">**.NET Ecosystem**: Leverage the existing ecosystem of .NET libraries.</span></span>
* <span data-ttu-id="6fa35-111">**Full-Stack-Entwicklung**: Nutzen Sie server- und clientseitige Logik gemeinsam.</span><span class="sxs-lookup"><span data-stu-id="6fa35-111">**Full-stack development**: Share server and client-side logic.</span></span>
* <span data-ttu-id="6fa35-112">**Geschwindigkeit und Skalierbarkeit:** NET wurde für Leistung, Zuverlässigkeit und Sicherheit konzipiert.</span><span class="sxs-lookup"><span data-stu-id="6fa35-112">**Speed and scalability**: .NET was built for performance, reliability, and security.</span></span>
* <span data-ttu-id="6fa35-113">**Branchenführende Tools:** Bleiben Sie mit Visual Studio unter Windows, Linux und macOS produktiv.</span><span class="sxs-lookup"><span data-stu-id="6fa35-113">**Industry-leading tools**: Stay productive with Visual Studio on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="6fa35-114">**Stabilität und Konsistenz**:  Setzen Sie auf eine Sammlung von Sprachen, Frameworks und Tools, die stabil, funktionsreich und einfach zu verwenden sind.</span><span class="sxs-lookup"><span data-stu-id="6fa35-114">**Stability and consistency**:  Build on a commonset of languages, frameworks, and tools that are stable, feature-rich, and easy to use.</span></span>

<span data-ttu-id="6fa35-115">Das Ausführen von .NET-Code in einem Webbrowser wird durch [WebAssembly](http://webassembly.org) (Kurzform: *wasm*) ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="6fa35-115">Running .NET code inside web browsers is made possible by [WebAssembly](http://webassembly.org) (abbreviated *wasm*).</span></span> <span data-ttu-id="6fa35-116">WebAssembly ist ein offener Webstandard, der in Webbrowsern ohne Plug-Ins unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="6fa35-116">WebAssembly is an open web standard and supported in web browsers without plugins.</span></span> <span data-ttu-id="6fa35-117">Es handelt sich um ein Bytecodeformat, das für schnelles Downloaden und die maximale Ausführungsgeschwindigkeit optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="6fa35-117">WebAssembly is a compact bytecode format optimized for fast download and maximum execution speed.</span></span>

<span data-ttu-id="6fa35-118">WebAssembly-Code kann über JavaScript-Interoperabilität auf alle Funktionen des Browsers zugreifen.</span><span class="sxs-lookup"><span data-stu-id="6fa35-118">WebAssembly code can access the full functionality of the browser via JavaScript interop.</span></span> <span data-ttu-id="6fa35-119">Gleichzeitig wird der über WebAssembly ausgeführte .NET-Code in derselben vertrauenswürdigen Sandbox wie JavaScript ausgeführt, um böswillige Aktionen auf dem Clientcomputer zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="6fa35-119">At the same time, .NET code executed via WebAssembly runs in the same trusted sandbox as JavaScript to prevent malicious actions on the client machine.</span></span>

![Blazor führt .NET-Code unter Verwendung von WebAssembly im Browser aus.](index/_static/blazor.png)

<span data-ttu-id="6fa35-121">Folgendes geschieht, wenn eine Blazor-App in einem Browser erstellt und ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="6fa35-121">When a Blazor app is built and run in a browser:</span></span>

* <span data-ttu-id="6fa35-122">C#-Codedateien und Razor-Dateien werden in .NET-Assemblys kompiliert.</span><span class="sxs-lookup"><span data-stu-id="6fa35-122">C# code files and Razor files are compiled into .NET assemblies.</span></span>
* <span data-ttu-id="6fa35-123">Die Assemblys und die .NET-Runtime werden im Browser heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="6fa35-123">The assemblies and the .NET runtime are downloaded to the browser.</span></span>
* <span data-ttu-id="6fa35-124">Blazor startet die .NET-Runtime und konfiguriert die Runtime zum Laden der Assemblys für die App.</span><span class="sxs-lookup"><span data-stu-id="6fa35-124">Blazor bootstraps the .NET runtime and configures the runtime to load the assemblies for the app.</span></span> <span data-ttu-id="6fa35-125">Die Bearbeitung von Dokumentobjektmodellen (DOM) und API-Aufrufen im Browser wird von der Blazor-Runtime über die JavaScript-Interop verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="6fa35-125">Document Object Model (DOM) manipulation and browser API calls are handled by the Blazor runtime via JavaScript interop.</span></span>

<span data-ttu-id="6fa35-126">Blazor unterstützt Kernfunktionen, die für die meisten Apps erforderlich sind, beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="6fa35-126">Blazor supports core facilities required by most apps, including:</span></span>

* <span data-ttu-id="6fa35-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="6fa35-127">Parameters</span></span>
* <span data-ttu-id="6fa35-128">Ereignisbehandlung</span><span class="sxs-lookup"><span data-stu-id="6fa35-128">Event handling</span></span>
* <span data-ttu-id="6fa35-129">Datenbindung</span><span class="sxs-lookup"><span data-stu-id="6fa35-129">Data binding</span></span>
* <span data-ttu-id="6fa35-130">Routing</span><span class="sxs-lookup"><span data-stu-id="6fa35-130">Routing</span></span>
* <span data-ttu-id="6fa35-131">Dependency Injection</span><span class="sxs-lookup"><span data-stu-id="6fa35-131">Dependency injection</span></span>
* <span data-ttu-id="6fa35-132">Layouts</span><span class="sxs-lookup"><span data-stu-id="6fa35-132">Layouts</span></span>
* <span data-ttu-id="6fa35-133">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="6fa35-133">Templating</span></span>
* <span data-ttu-id="6fa35-134">Kaskadierende Werte</span><span class="sxs-lookup"><span data-stu-id="6fa35-134">Cascading values</span></span>

<span data-ttu-id="6fa35-135">Um die Größe der heruntergeladenen App zu verringern, wird nicht verwendeter Code aus der App entfernt, wenn sie vom [IL-Linker (Intermediate Language)](xref:host-and-deploy/razor-components/configure-linker) veröffentlicht wird.</span><span class="sxs-lookup"><span data-stu-id="6fa35-135">To reduce the size of the downloaded app unused code stripped out of the app when it's published by the [Intermediate Language (IL) Linker](xref:host-and-deploy/razor-components/configure-linker).</span></span>

<span data-ttu-id="6fa35-136">Blazor ist das clientseitige Hostingmodell von Razor Components.</span><span class="sxs-lookup"><span data-stu-id="6fa35-136">Blazor is the client-side hosting model for Razor Components.</span></span> <span data-ttu-id="6fa35-137">Da Razor Components die Renderinglogik einer Komponente von der Art und Weise entkoppeln, wie Benutzeroberflächenupdates angewendet werden, besteht Flexibilität hinsichtlich des Hostings von Razor Components.</span><span class="sxs-lookup"><span data-stu-id="6fa35-137">Because Razor Components decouple a component's rendering logic from how UI updates are applied, there's flexibility in how Razor Components can be hosted.</span></span> <span data-ttu-id="6fa35-138">Verwenden Sie ASP.NET Core Razor Components, um Razor Components auf dem Server in einer ASP.NET Core-App zu hosten, in der Benutzeroberflächenupdates über eine SignalR-Verbindung verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-138">Use ASP.NET Core Razor Components to host Razor Components on the server in an ASP.NET Core app where UI updates are handled over a SignalR connection.</span></span> <span data-ttu-id="6fa35-139">Weitere Informationen finden Sie unter <xref:razor-components/hosting-models#server-side-hosting-model>.</span><span class="sxs-lookup"><span data-stu-id="6fa35-139">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span> 

## <a name="components"></a><span data-ttu-id="6fa35-140">Komponenten</span><span class="sxs-lookup"><span data-stu-id="6fa35-140">Components</span></span>

<span data-ttu-id="6fa35-141">Eine *Razor Component* ist Bestandteil der Benutzeroberfläche (z.B. Seiten, Dialogfelder oder Formulare für die Dateneingabe).</span><span class="sxs-lookup"><span data-stu-id="6fa35-141">A *Razor Component* is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="6fa35-142">Komponenten behandeln Benutzerereignisse und definieren flexible Renderinglogik für die Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="6fa35-142">Components handle user events and define flexible UI rendering logic.</span></span> <span data-ttu-id="6fa35-143">Komponenten können geschachtelt sein und wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-143">Components can be nested and reused.</span></span>

<span data-ttu-id="6fa35-144">Komponenten sind in .NET-Assemblys integrierte .NET-Klassen, die gemeinsam genutzt und als NuGet-Pakete verteilt werden können.</span><span class="sxs-lookup"><span data-stu-id="6fa35-144">Components are .NET classes built into .NET assemblies that can be shared and distributed as NuGet packages.</span></span> <span data-ttu-id="6fa35-145">Die Klasse kann entweder in Form einer Razor-Markupseite (*CSHTML-Datei*) oder als C#-Klasse (*CS-Datei*) geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-145">The class can either be written in the form of a Razor markup page (*.cshtml*) or as a C# class (*.cs*).</span></span>

<span data-ttu-id="6fa35-146">[Razor](xref:mvc/views/razor) ist eine Syntax, mit der HTML-Markup mit C#-Code kombiniert werden kann.</span><span class="sxs-lookup"><span data-stu-id="6fa35-146">[Razor](xref:mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="6fa35-147">Razor wurde entwickelt, um die Produktivität von Entwicklern zu optimieren, da diese damit und unter Verwendung der [IntelliSense](/visualstudio/ide/using-intellisense)-Unterstützung innerhalb einer Datei zwischen Markup und C# wechseln können.</span><span class="sxs-lookup"><span data-stu-id="6fa35-147">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="6fa35-148">Razor Pages und MVC-Ansichten verwenden ebenfalls Razor.</span><span class="sxs-lookup"><span data-stu-id="6fa35-148">Razor Pages and MVC views also use Razor.</span></span> <span data-ttu-id="6fa35-149">Im Gegensatz zu Razor Pages und MVC-Ansichten, die auf einem Anforderung/Antwort-Modell aufbauen, werden Komponenten speziell für die Verarbeitung der Benutzeroberflächengestaltung verwendet.</span><span class="sxs-lookup"><span data-stu-id="6fa35-149">Unlike Razor Pages and MVC views, which are built around a request/response model, components are used specifically for handling UI composition.</span></span> <span data-ttu-id="6fa35-150">Razor Components können insbesondere für die clientseitige Benutzeroberflächenlogik und -gestaltung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-150">Razor Components can be used specifically for client-side UI logic and composition.</span></span>

<span data-ttu-id="6fa35-151">Das folgende Markup stellt ein Beispiel einer benutzerdefinierten Dialogfeldkomponente in einer Razor-Datei (*DialogComponent.cshtml*) dar:</span><span class="sxs-lookup"><span data-stu-id="6fa35-151">The following markup is an example of a custom dialog component in a Razor file (*DialogComponent.cshtml*):</span></span>

```cshtml
<div>
    <h2>@Title</h2>
    @BodyContent
    <button onclick=@OnOK>OK</button>
</div>

@functions {
    public string Title { get; set; }
    public RenderFragment BodyContent { get; set; }
    public Action OnOK { get; set; }
}
```

<span data-ttu-id="6fa35-152">Wenn diese Komponente an einer anderen Stelle in der App verwendet wird, beschleunigt IntelliSense die Entwicklung mithilfe von Syntax- und Parametervervollständigung.</span><span class="sxs-lookup"><span data-stu-id="6fa35-152">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="6fa35-153">Die Komponenten werden in einer In-Memory-Darstellung des Browser-DOMs gerendert, die als *Renderbaum* bezeichnet wird und anschließend verwendet werden kann, um die Benutzeroberfläche auf flexible und effiziente Weise zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="6fa35-153">Components render into an in-memory representation of the browser DOM called a *render tree* that can then be used to update the UI in a flexible and efficient way.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="6fa35-154">JavaScript-Interoperabilität</span><span class="sxs-lookup"><span data-stu-id="6fa35-154">JavaScript interop</span></span>

<span data-ttu-id="6fa35-155">Für Apps, die JavaScript-Bibliotheken und Browser-APIs von Drittanbietern erfordern, ist Blazor für die Interoperabilität mit JavaScript konzipiert.</span><span class="sxs-lookup"><span data-stu-id="6fa35-155">For apps that require third-party JavaScript libraries and browser APIs, Blazor interoperates with JavaScript.</span></span> <span data-ttu-id="6fa35-156">Komponenten können jede Bibliothek oder API verwenden, die auch von JavaScript verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="6fa35-156">Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="6fa35-157">C#-Code kann JavaScript-Code abfragen, und umgekehrt.</span><span class="sxs-lookup"><span data-stu-id="6fa35-157">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="6fa35-158">Weitere Informationen finden Sie unter [JavaScript interop (JavaScript-Interoperabilität)](xref:razor-components/javascript-interop).</span><span class="sxs-lookup"><span data-stu-id="6fa35-158">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="code-sharing-and-net-standard"></a><span data-ttu-id="6fa35-159">Codefreigabe und .NET Standard</span><span class="sxs-lookup"><span data-stu-id="6fa35-159">Code sharing and .NET Standard</span></span>

<span data-ttu-id="6fa35-160">Apps können auf bereits vorhandene [.NET Standard](/dotnet/standard/net-standard)-Bibliotheken verweisen und diese verwenden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-160">Apps can reference and use existing [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="6fa35-161">.NET Standard ist eine formale Spezifikation von .NET-APIs, die häufig für .NET-Implementierungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-161">.NET Standard is a formal specification of .NET APIs that are common across .NET implementations.</span></span> <span data-ttu-id="6fa35-162">Es wird .NET Standard 2.0 oder höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6fa35-162">.NET Standard 2.0 or higher is supported.</span></span> <span data-ttu-id="6fa35-163">APIs, die nicht in einem Webbrowser angewendet werden können (z.B. zum Zugreifen auf ein Dateisystem, zum Öffnen eines Sockets, für das Threading und für andere Features), lösen die Ausnahme <xref:System.PlatformNotSupportedException> aus.</span><span class="sxs-lookup"><span data-stu-id="6fa35-163">APIs that aren't applicable inside a web browser (for example, accessing the file system, opening a socket, threading, and other features) throw <xref:System.PlatformNotSupportedException>.</span></span> <span data-ttu-id="6fa35-164">.NET Standard-Klassenbibliotheken können für den gesamten Servercode und für mehrere browserbasierte Apps freigegeben werden.</span><span class="sxs-lookup"><span data-stu-id="6fa35-164">.NET Standard class libraries can be shared across server code and in browser-based apps.</span></span>

## <a name="optimization"></a><span data-ttu-id="6fa35-165">Optimierung</span><span class="sxs-lookup"><span data-stu-id="6fa35-165">Optimization</span></span>

<span data-ttu-id="6fa35-166">Die Größe der Nutzlast ist ein wichtiger Leistungsfaktor für die Nutzbarkeit einer App.</span><span class="sxs-lookup"><span data-stu-id="6fa35-166">Payload size is a critical performance factor for an app's useability.</span></span> <span data-ttu-id="6fa35-167">Blazor optimiert die Nutzlastgröße, um die Downloadzeiten zu verringern:</span><span class="sxs-lookup"><span data-stu-id="6fa35-167">Blazor optimizes payload size to reduce download times:</span></span>

* <span data-ttu-id="6fa35-168">Nicht verwendete Teile von .NET-Assemblys werden während des Buildvorgangs entfernt.</span><span class="sxs-lookup"><span data-stu-id="6fa35-168">Unused parts of .NET assemblies are removed during the build process.</span></span>
* <span data-ttu-id="6fa35-169">HTTP-Antworten werden komprimiert.</span><span class="sxs-lookup"><span data-stu-id="6fa35-169">HTTP responses are compressed.</span></span>
* <span data-ttu-id="6fa35-170">Die .NET-Runtime und die Assemblys werden im Browser zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="6fa35-170">The .NET runtime and assemblies are cached in the browser.</span></span>

<span data-ttu-id="6fa35-171">[Serverseitige Razor Components](xref:razor-components/index) bieten mithilfe der Verwaltung von .NET-Assemblys, der App-Assembly und der serverseitigen Runtime sogar eine noch kleinere Nutzlast als Blazor.</span><span class="sxs-lookup"><span data-stu-id="6fa35-171">[Server-side Razor Components](xref:razor-components/index) provides an even smaller payload size than Blazor by maintaining .NET assemblies, the app's assembly, and the runtime server-side.</span></span> <span data-ttu-id="6fa35-172">Razor Components-Apps stellen den Clients nur Markupdateien und statische Ressourcen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="6fa35-172">Razor Components apps only serve markup files and static assets to clients.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6fa35-173">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6fa35-173">Additional resources</span></span>

* <xref:razor-components/index>
* [<span data-ttu-id="6fa35-174">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="6fa35-174">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="6fa35-175">Leitfaden für C#</span><span class="sxs-lookup"><span data-stu-id="6fa35-175">C# Guide</span></span>](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [<span data-ttu-id="6fa35-176">HTML</span><span class="sxs-lookup"><span data-stu-id="6fa35-176">HTML</span></span>](https://www.w3.org/html/)
