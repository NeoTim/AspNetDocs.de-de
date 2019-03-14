---
title: ASP.NET Core-Middleware
author: rick-anderson
description: Erfahren Sie mehr über ASP.NET Core-Middleware und die Anforderungspipeline.
ms.author: riande
ms.custom: mvc
ms.date: 02/17/2019
uid: fundamentals/middleware/index
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="59e8b-103">ASP.NET Core-Middleware</span><span class="sxs-lookup"><span data-stu-id="59e8b-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="59e8b-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT) und [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="59e8b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="59e8b-105">Middleware ist Software, die zu einer Anwendungspipeline zusammengesetzt wird, um Anforderungen und Antworten zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="59e8b-106">Jede Komponente kann Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="59e8b-106">Each component:</span></span>

* <span data-ttu-id="59e8b-107">Entscheiden, ob die Anforderung an die nächste Komponente in der Pipeline übergeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="59e8b-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="59e8b-108">Ausführen von Arbeiten, bevor oder nachdem die nächste Komponente in der Pipeline aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="59e8b-108">Can perform work before and after the next component in the pipeline.</span></span>

<span data-ttu-id="59e8b-109">Anforderungsdelegaten werden verwendet, um die Anforderungspipeline zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="59e8b-110">Die Anforderungsdelegaten behandeln jede HTTP-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="59e8b-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="59e8b-111">Anforderungsdelegaten werden mit den Erweiterungsmethoden <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> und <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="59e8b-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="59e8b-112">Ein einzelner Anforderungsdelegat kann inline als anonyme Methode angegeben werden (sogenannte Inline-Middleware), oder er kann in einer wiederverwendbaren Klasse definiert werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="59e8b-113">Diese wiederverwendbaren Klassen und anonymen Inline-Methoden sind *Middleware* bzw. *Middlewarekomponenten*.</span><span class="sxs-lookup"><span data-stu-id="59e8b-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="59e8b-114">Jede Middlewarekomponente in der Anforderungspipeline ist für das Aufrufen der jeweils nächsten Komponente in der Pipeline oder, wenn nötig, für das Kurzschließen der Pipeline zuständig.</span><span class="sxs-lookup"><span data-stu-id="59e8b-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span> <span data-ttu-id="59e8b-115">Wenn eine Middleware einen Kurzschluss verursacht, wird diese als *Terminalmiddleware* bezeichnet, da sie verhindert, dass weitere Middleware die Anforderung verarbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="59e8b-115">When a middleware short-circuits, it's called a *terminal middleware* because it prevents further middleware from processing the request.</span></span>

<span data-ttu-id="59e8b-116">Unter <xref:migration/http-modules> wird der Unterschied zwischen Anforderungspipelines in ASP.NET Core und ASP.NET 4.x erklärt. Außerdem werden dort weitere Beispiele für Middleware gegeben.</span><span class="sxs-lookup"><span data-stu-id="59e8b-116"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="59e8b-117">Erstellen einer Middlewarepipeline mit IApplicationBuilder</span><span class="sxs-lookup"><span data-stu-id="59e8b-117">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="59e8b-118">Die ASP.NET Core-Anforderungspipeline besteht aus einer Sequenz von Anforderungsdelegaten, die nacheinander aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-118">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="59e8b-119">Das Konzept wird im folgenden Diagramm veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="59e8b-119">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="59e8b-120">Der Ausführungsthread folgt den schwarzen Pfeilen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-120">The thread of execution follows the black arrows.</span></span>

![Anforderungsverarbeitungsmuster mit eingehender Anforderung, deren Verarbeitung von drei Middlewares und die ausgehende Antwort der Anwendung.](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="59e8b-124">Jeder Delegat kann Vorgänge vor und nach dem nächsten Delegaten ausführen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-124">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="59e8b-125">Die Ausnahmebehandlungsdelegaten müssen am Anfang der Pipeline aufgerufen werden, sodass sie Ausnahmen abfangen können, die zu einem späteren Zeitpunkt in der Pipeline ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-125">Exception-handling delegates should be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="59e8b-126">Die einfachste mögliche ASP.NET Core-App enthält einen einzigen Anforderungsdelegaten, der alle Anforderungen verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-126">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="59e8b-127">In diesem Fall ist keine tatsächliche Anforderungspipeline vorhanden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-127">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="59e8b-128">Stattdessen wird eine einzelne anonyme Funktion als Antwort auf jede HTTP-Anforderung aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-128">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="59e8b-129">Der erste <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>-Delegat beendet die Pipeline.</span><span class="sxs-lookup"><span data-stu-id="59e8b-129">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="59e8b-130">Mit <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> können Sie mehrere Anforderungedelegate miteinander verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-130">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="59e8b-131">Der Parameter `next` steht für den nächsten Delegaten in der Pipeline.</span><span class="sxs-lookup"><span data-stu-id="59e8b-131">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="59e8b-132">Sie können die Pipeline kurzschließen, indem Sie den Parameter *next* *nicht* aufrufen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-132">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="59e8b-133">Normalerweise können Sie Aktionen sowohl vor als auch nach dem nächsten Delegaten durchführen. Dies wird in folgendem Beispiel veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="59e8b-133">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

<span data-ttu-id="59e8b-134">Wenn ein keine Anforderung an den nächsten Delegaten übergibt, wird dies als *Kurzschluss der Anforderungspipeline* bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-134">When a delegate doesn't pass a request to the next delegate, it's called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="59e8b-135">Das Kurzschließen ist oft sinnvoll, da es unnötige Arbeit verhindert.</span><span class="sxs-lookup"><span data-stu-id="59e8b-135">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="59e8b-136">Die [Middleware für statische Dateien](xref:fundamentals/static-files) kann beispielsweise als *Terminalmiddleware* fungieren, indem sie eine Anforderung für eine statische Datei zurückgibt und den Rest der Pipeline kurzschließt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-136">For example, [Static File Middleware](xref:fundamentals/static-files) can act as a *terminal middleware* by processing a request for a static file and short-circuiting the rest of the pipeline.</span></span> <span data-ttu-id="59e8b-137">Middleware, die noch vor der Middleware, die die weitere Verarbeitung beendet, zur Pipeline hinzugefügt wird, verarbeitet Code noch nach den `next.Invoke`-Anweisungen weiter.</span><span class="sxs-lookup"><span data-stu-id="59e8b-137">Middleware added to the pipeline before the middleware that terminates further processing still processes code after their `next.Invoke` statements.</span></span> <span data-ttu-id="59e8b-138">Sehen Sie sich allerdings die folgende Warnung zum Versuch an, in eine Antwort zu schreiben, die bereits gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="59e8b-138">However, see the following warning about attempting to write to a response that has already been sent.</span></span>

> [!WARNING]
> <span data-ttu-id="59e8b-139">Rufen Sie `next.Invoke` nicht auf, nachdem die Antwort an den Client gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="59e8b-139">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="59e8b-140">An <xref:Microsoft.AspNetCore.Http.HttpResponse> vorgenommene Änderungen lösen nach dem Start der Antwort eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="59e8b-140">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="59e8b-141">Änderungen wie das Festlegen von Headern und einem Statuscode lösen beispielsweise eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="59e8b-141">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="59e8b-142">Wenn Sie nach dem Aufruf von `next` in den Antworttext schreiben, kann dies:</span><span class="sxs-lookup"><span data-stu-id="59e8b-142">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="59e8b-143">einen Protokollverstoß verursachen,</span><span class="sxs-lookup"><span data-stu-id="59e8b-143">May cause a protocol violation.</span></span> <span data-ttu-id="59e8b-144">wenn Sie z.B. mehr als das genannte `Content-Length`-Objekt schreiben.</span><span class="sxs-lookup"><span data-stu-id="59e8b-144">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="59e8b-145">Fehler im Textformat auslösen,</span><span class="sxs-lookup"><span data-stu-id="59e8b-145">May corrupt the body format.</span></span> <span data-ttu-id="59e8b-146">wenn Sie z.B. eine HTML-Fußzeile in eine CSS-Datei schreiben.</span><span class="sxs-lookup"><span data-stu-id="59e8b-146">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="59e8b-147"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> ist ein nützlicher Hinweis, der angibt, ob Header gesendet wurden oder ob in den Text geschrieben wurde.</span><span class="sxs-lookup"><span data-stu-id="59e8b-147"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="59e8b-148">Auftrag</span><span class="sxs-lookup"><span data-stu-id="59e8b-148">Order</span></span>

<span data-ttu-id="59e8b-149">Die Reihenfolge, in der Middlewarekomponenten in der `Startup.Configure`-Methode hinzugefügt werden, legt die Reihenfolge fest, in der die Middlewarekomponenten bei Anforderungen aufgerufen werden. Bei Antworten gilt die umgekehrte Reihenfolge.</span><span class="sxs-lookup"><span data-stu-id="59e8b-149">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="59e8b-150">Die Reihenfolge trägt wesentlich zur Sicherheit, Leistung und Funktionalität bei.</span><span class="sxs-lookup"><span data-stu-id="59e8b-150">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="59e8b-151">Die folgenden `Startup.Configure`-Methode fügt Middlewarekomponenten für allgemeine App-Szenarien hinzu:</span><span class="sxs-lookup"><span data-stu-id="59e8b-151">The following `Startup.Configure` method adds middleware components for common app scenarios:</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="59e8b-152">Ausnahme-/Fehlerbehandlung</span><span class="sxs-lookup"><span data-stu-id="59e8b-152">Exception/error handling</span></span>
1. <span data-ttu-id="59e8b-153">HTTP Strict Transport Security Protocol</span><span class="sxs-lookup"><span data-stu-id="59e8b-153">HTTP Strict Transport Security Protocol</span></span>
1. <span data-ttu-id="59e8b-154">HTTPS-Umleitung</span><span class="sxs-lookup"><span data-stu-id="59e8b-154">HTTPS redirection</span></span>
1. <span data-ttu-id="59e8b-155">Statischer Dateiserver</span><span class="sxs-lookup"><span data-stu-id="59e8b-155">Static file server</span></span>
1. <span data-ttu-id="59e8b-156">Cookierichtliniendurchsetzung</span><span class="sxs-lookup"><span data-stu-id="59e8b-156">Cookie policy enforcement</span></span>
1. <span data-ttu-id="59e8b-157">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="59e8b-157">Authentication</span></span>
1. <span data-ttu-id="59e8b-158">Sitzung</span><span class="sxs-lookup"><span data-stu-id="59e8b-158">Session</span></span>
1. <span data-ttu-id="59e8b-159">MVC</span><span class="sxs-lookup"><span data-stu-id="59e8b-159">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    if (env.IsDevelopment())
    {
        // When the app runs in the Development environment:
        //   Use the Developer Exception Page to report app runtime errors.
        //   Use the Database Error Page to report database runtime errors.
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
    }
    else
    {
        // When the app doesn't run in the Development environment:
        //   Enable the Exception Handler Middleware to catch exceptions
        //     thrown in the following middlewares.
        //   Use the HTTP Strict Transport Security Protocol (HSTS)
        //     Middleware.
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // Use HTTPS Redirection Middleware to redirect HTTP requests to HTTPS.
    app.UseHttpsRedirection();

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Use Cookie Policy Middleware to conform to EU General Data 
    // Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // If the app uses session state, call Session Middleware after Cookie 
    // Policy Middleware and before MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. <span data-ttu-id="59e8b-160">Ausnahme-/Fehlerbehandlung</span><span class="sxs-lookup"><span data-stu-id="59e8b-160">Exception/error handling</span></span>
1. <span data-ttu-id="59e8b-161">Statische Dateien</span><span class="sxs-lookup"><span data-stu-id="59e8b-161">Static files</span></span>
1. <span data-ttu-id="59e8b-162">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="59e8b-162">Authentication</span></span>
1. <span data-ttu-id="59e8b-163">Sitzung</span><span class="sxs-lookup"><span data-stu-id="59e8b-163">Session</span></span>
1. <span data-ttu-id="59e8b-164">MVC</span><span class="sxs-lookup"><span data-stu-id="59e8b-164">MVC</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable the Exception Handler Middleware to catch exceptions
    //   thrown in the following middlewares.
    app.UseExceptionHandler("/Home/Error");

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Authenticate before you access secure resources.
    app.UseIdentity();

    // If the app uses session state, call UseSession before 
    // MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="59e8b-165">Im vorhergehenden Beispielcode wird jede Middleware-Erweiterungsmethode in <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> über den <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName>-Namespace verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="59e8b-165">In the preceding example code, each middleware extension method is exposed on <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> through the <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> namespace.</span></span>

<span data-ttu-id="59e8b-166"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> ist die erste Middlewarekomponente, die der Pipeline hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="59e8b-166"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="59e8b-167">Aus diesem Grund fängt die Middleware für den Ausnahmehandler alle Ausnahmen ab, die in späteren Aufrufen auftreten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-167">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="59e8b-168">Die Middleware für statische Dateien wird am Anfang der Pipeline aufgerufen, damit sie Anforderungen und Kurzschlüsse verarbeiten kann, ohne dass die verbleibenden Komponenten durchlaufen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-168">Static File Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="59e8b-169">Die Middleware für statische Dateien stellt **keine** Autorisierungsüberprüfungen bereit.</span><span class="sxs-lookup"><span data-stu-id="59e8b-169">The Static File Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="59e8b-170">Alle Dateien, die von ihr bearbeitet werden, Dateien unter *wwwroot* inbegriffen, sind öffentlich verfügbar.</span><span class="sxs-lookup"><span data-stu-id="59e8b-170">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="59e8b-171">Informationen zum Sichern statischer Dateien finden Sie unter <xref:fundamentals/static-files>.</span><span class="sxs-lookup"><span data-stu-id="59e8b-171">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="59e8b-172">Wenn die Anforderung nicht von der Middleware für statische Dateien verarbeitet wird, wird sie an die Authentifizierungsmiddleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>) übergeben, welche die Authentifizierung durchführt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-172">If the request isn't handled by the Static File Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="59e8b-173">Die Authentifizierung schließt nicht authentifizierte Anforderungen nicht kurz.</span><span class="sxs-lookup"><span data-stu-id="59e8b-173">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="59e8b-174">Auch wenn die Authentifizierungsmiddleware Anforderungen authentifiziert, erfolgt die Autorisierung (und Ablehnung) erst dann, wenn MVC eine spezifische Razor Page oder einen MVC-Controller und eine Aktion ausgewählt hat.</span><span class="sxs-lookup"><span data-stu-id="59e8b-174">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="59e8b-175">Wenn die Anforderung nicht von der Middleware für statische Dateien verarbeitet wird, wird sie an die Identity-Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>) übergeben, welche die Authentifizierung durchführt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-175">If the request isn't handled by Static File Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="59e8b-176">Identity schließt keine unautorisierten Anforderungen kurz.</span><span class="sxs-lookup"><span data-stu-id="59e8b-176">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="59e8b-177">Auch wenn Identity Anforderungen authentifiziert, erfolgt die Autorisierung (und Ablehnung) erst dann, wenn MVC einen spezifischen Controller und eine Aktion ausgewählt hat.</span><span class="sxs-lookup"><span data-stu-id="59e8b-177">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="59e8b-178">Im folgenden Beispiel wird eine Middlewarereihenfolge veranschaulicht, bei der Anforderungen statischer Dateien von der Middleware für statische Dateien vor der Middleware für die Antwortkomprimierung verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-178">The following example demonstrates a middleware order where requests for static files are handled by Static File Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="59e8b-179">Die statischen Dateien werden bei dieser Middlewarereihenfolge nicht komprimiert.</span><span class="sxs-lookup"><span data-stu-id="59e8b-179">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="59e8b-180">Die MVC-Antworten von <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> können komprimiert werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-180">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static File Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="59e8b-181">Use, Run und Map</span><span class="sxs-lookup"><span data-stu-id="59e8b-181">Use, Run, and Map</span></span>

<span data-ttu-id="59e8b-182">Konfigurieren Sie die HTTP-Pipeline mit `Use`, `Run` und `Map`.</span><span class="sxs-lookup"><span data-stu-id="59e8b-182">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="59e8b-183">Die `Use`-Methode kann die Pipeline kurzschließen (wenn sie keinen `next`-Anforderungsdelegaten aufruft).</span><span class="sxs-lookup"><span data-stu-id="59e8b-183">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="59e8b-184">`Run` ist eine Konvention. Einige Middlewarekomponenten machen möglicherweise `Run[Middleware]`-Methoden verfügbar, die am Ende einer Pipeline ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-184">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="59e8b-185"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>-Erweiterungen werden als Konvention zum Branchen der Pipeline verwendet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-185"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="59e8b-186">`Map*` brancht die Anforderungspipeline auf Grundlage von Übereinstimmungen des angegebenen Anforderungspfads.</span><span class="sxs-lookup"><span data-stu-id="59e8b-186">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="59e8b-187">Wenn der Anforderungspfad mit dem angegebenen Pfad beginnt, wird der Branch ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-187">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="59e8b-188">In der folgenden Tabelle sind die Anforderungen und Antworten von `http://localhost:1234` mit dem oben stehenden Code aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-188">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="59e8b-189">Anforderung</span><span class="sxs-lookup"><span data-stu-id="59e8b-189">Request</span></span>             | <span data-ttu-id="59e8b-190">Antwort</span><span class="sxs-lookup"><span data-stu-id="59e8b-190">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="59e8b-191">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="59e8b-191">localhost:1234</span></span>      | <span data-ttu-id="59e8b-192">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="59e8b-192">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="59e8b-193">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="59e8b-193">localhost:1234/map1</span></span> | <span data-ttu-id="59e8b-194">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="59e8b-194">Map Test 1</span></span>                   |
| <span data-ttu-id="59e8b-195">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="59e8b-195">localhost:1234/map2</span></span> | <span data-ttu-id="59e8b-196">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="59e8b-196">Map Test 2</span></span>                   |
| <span data-ttu-id="59e8b-197">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="59e8b-197">localhost:1234/map3</span></span> | <span data-ttu-id="59e8b-198">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="59e8b-198">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="59e8b-199">Wenn `Map` verwendet wird, werden die übereinstimmenden Pfadsegmente bzw. das übereinstimmende Pfadsegment aus `HttpRequest.Path` entfernt und für jede Anforderung an `HttpRequest.PathBase` angehängt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-199">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="59e8b-200">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) brancht die Anforderungspipeline auf Grundlage des Ergebnisses des angegebenen Prädikats.</span><span class="sxs-lookup"><span data-stu-id="59e8b-200">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="59e8b-201">Jedes Prädikat vom Typ `Func<HttpContext, bool>` kann verwendet werden, um Anforderungen einem neuen Branch der Pipeline zuzuordnen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-201">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="59e8b-202">Im folgenden Beispiel wird ein Prädikat verwendet, um das Vorhandensein der Abfragezeichenfolgenvariablen `branch` zu ermitteln:</span><span class="sxs-lookup"><span data-stu-id="59e8b-202">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="59e8b-203">In der folgenden Tabelle sind die Anforderungen und Antworten von `http://localhost:1234` mit dem oben stehenden Code aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-203">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="59e8b-204">Anforderung</span><span class="sxs-lookup"><span data-stu-id="59e8b-204">Request</span></span>                       | <span data-ttu-id="59e8b-205">Antwort</span><span class="sxs-lookup"><span data-stu-id="59e8b-205">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="59e8b-206">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="59e8b-206">localhost:1234</span></span>                | <span data-ttu-id="59e8b-207">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="59e8b-207">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="59e8b-208">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="59e8b-208">localhost:1234/?branch=master</span></span> | <span data-ttu-id="59e8b-209">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="59e8b-209">Branch used = master</span></span>         |

<span data-ttu-id="59e8b-210">`Map` unterstützt das Schachteln, wie z.B. in folgendem Code:</span><span class="sxs-lookup"><span data-stu-id="59e8b-210">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
    level1App.Map("/level2a", level2AApp => {
        // "/level1/level2a" processing
    });
    level1App.Map("/level2b", level2BApp => {
        // "/level1/level2b" processing
    });
});
   ```

<span data-ttu-id="59e8b-211">`Map` kann auch mehrere Segmente auf einmal zuordnen:</span><span class="sxs-lookup"><span data-stu-id="59e8b-211">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="59e8b-212">Integrierte Middleware</span><span class="sxs-lookup"><span data-stu-id="59e8b-212">Built-in middleware</span></span>

<span data-ttu-id="59e8b-213">Die folgenden Middlewarekomponenten sind im Lieferumfang von ASP.NET Core enthalten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-213">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="59e8b-214">Die Spalte *Reihenfolge* enthält Hinweise zur Platzierung der Middleware in der Pipeline, die die Anforderung verarbeitet, und zu den Bedingungen, unter denen die Middleware die Anforderungsverarbeitung möglicherweise beendet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-214">The *Order* column provides notes on middleware placement in the request processing pipeline and under what conditions the middleware may terminate request processing.</span></span> <span data-ttu-id="59e8b-215">Wenn eine Middleware einen Kurzschluss in der Anforderungsverarbeitungspipeline verursacht und verhindert, dass Downstreammiddleware eine Anforderung verarbeitet, wird diese als *Terminalmiddleware* bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-215">When a middleware short-circuits the request processing pipeline and prevents further downstream middleware from processing a request, it's called a *terminal middleware*.</span></span> <span data-ttu-id="59e8b-216">Weitere Informationen zu Kurzschlüssen finden Sie im Abschnitt [Erstellen einer Middlewarepipeline mit IApplicationBuilder](#create-a-middleware-pipeline-with-iapplicationbuilder).</span><span class="sxs-lookup"><span data-stu-id="59e8b-216">For more information on short-circuiting, see the [Create a middleware pipeline with IApplicationBuilder](#create-a-middleware-pipeline-with-iapplicationbuilder) section.</span></span>

| <span data-ttu-id="59e8b-217">Middleware</span><span class="sxs-lookup"><span data-stu-id="59e8b-217">Middleware</span></span> | <span data-ttu-id="59e8b-218">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="59e8b-218">Description</span></span> | <span data-ttu-id="59e8b-219">Auftrag</span><span class="sxs-lookup"><span data-stu-id="59e8b-219">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="59e8b-220">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="59e8b-220">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="59e8b-221">Bietet Unterstützung für Authentifizierungen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-221">Provides authentication support.</span></span> | <span data-ttu-id="59e8b-222">Bevor `HttpContext.User` erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="59e8b-222">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="59e8b-223">Terminal für OAuth-Rückrufe.</span><span class="sxs-lookup"><span data-stu-id="59e8b-223">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="59e8b-224">Cookierichtlinie</span><span class="sxs-lookup"><span data-stu-id="59e8b-224">Cookie Policy</span></span>](xref:security/gdpr) | <span data-ttu-id="59e8b-225">Verfolgt die Zustimmung von Benutzern zum Speichern persönlicher Informationen nach und erzwingt die Mindeststandards für Cookiefelder, z.B. `secure` und `SameSite`.</span><span class="sxs-lookup"><span data-stu-id="59e8b-225">Tracks consent from users for storing personal information and enforces minimum standards for cookie fields, such as `secure` and `SameSite`.</span></span> | <span data-ttu-id="59e8b-226">Befindet sich vor der Middleware, die Cookies ausstellt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-226">Before middleware that issues cookies.</span></span> <span data-ttu-id="59e8b-227">Beispiele: Authentifizierung, Sitzung, MVC (TempData).</span><span class="sxs-lookup"><span data-stu-id="59e8b-227">Examples: Authentication, Session, MVC (TempData).</span></span> |
| [<span data-ttu-id="59e8b-228">CORS</span><span class="sxs-lookup"><span data-stu-id="59e8b-228">CORS</span></span>](xref:security/cors) | <span data-ttu-id="59e8b-229">Konfiguriert die Ressourcenfreigabe zwischen verschiedenen Ursprüngen (Cross-Origin Resource Sharing, CORS).</span><span class="sxs-lookup"><span data-stu-id="59e8b-229">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="59e8b-230">Vor Komponenten, die CORS verwenden.</span><span class="sxs-lookup"><span data-stu-id="59e8b-230">Before components that use CORS.</span></span> |
| [<span data-ttu-id="59e8b-231">Diagnose</span><span class="sxs-lookup"><span data-stu-id="59e8b-231">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="59e8b-232">Konfiguriert Diagnosen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-232">Configures diagnostics.</span></span> | <span data-ttu-id="59e8b-233">Vor Komponenten, die Fehler erzeugen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-233">Before components that generate errors.</span></span> |
| [<span data-ttu-id="59e8b-234">Weitergeleitete Header</span><span class="sxs-lookup"><span data-stu-id="59e8b-234">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="59e8b-235">Leitet Proxyheader an die aktuelle Anforderung weiter.</span><span class="sxs-lookup"><span data-stu-id="59e8b-235">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="59e8b-236">Vor Komponenten, die die aktualisierten Felder nutzen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-236">Before components that consume the updated fields.</span></span> <span data-ttu-id="59e8b-237">Beispiele: Schema, Host, Client-IP, Methode.</span><span class="sxs-lookup"><span data-stu-id="59e8b-237">Examples: scheme, host, client IP, method.</span></span> |
| [<span data-ttu-id="59e8b-238">Integritätsprüfung</span><span class="sxs-lookup"><span data-stu-id="59e8b-238">Health Check</span></span>](xref:host-and-deploy/health-checks) | <span data-ttu-id="59e8b-239">Überprüft die Integrität der ASP.NET Core-App und ihrer Abhängigkeiten, z. B. Überprüfung der Datenbankverfügbarkeit.</span><span class="sxs-lookup"><span data-stu-id="59e8b-239">Checks the health of an ASP.NET Core app and its dependencies, such as checking database availability.</span></span> | <span data-ttu-id="59e8b-240">Abschließend, wenn eine Anforderung mit einem Integritätsprüfungs-Endpunkt übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-240">Terminal if a request matches a health check endpoint.</span></span> |
| [<span data-ttu-id="59e8b-241">Außerkraftsetzung der HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="59e8b-241">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="59e8b-242">Ermöglicht es eingehenden POST-Anforderungen, die Methode außer Kraft zu setzen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-242">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="59e8b-243">Vor Komponenten, die die aktualisierte Methode nutzen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-243">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="59e8b-244">HTTPS-Umleitung</span><span class="sxs-lookup"><span data-stu-id="59e8b-244">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="59e8b-245">Leitet alle HTTP-Anforderungen an HTTPS um (ASP.NET Core 2.1 oder höher).</span><span class="sxs-lookup"><span data-stu-id="59e8b-245">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="59e8b-246">Vor Komponenten, die die URL nutzen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-246">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="59e8b-247">HTTP Strict Transport Security (HSTS)</span><span class="sxs-lookup"><span data-stu-id="59e8b-247">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="59e8b-248">Sicherheits-Middleware, die einen besonderen Antwortheader hinzufügt (ASP.NET Core 2.1 oder höher).</span><span class="sxs-lookup"><span data-stu-id="59e8b-248">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="59e8b-249">Bevor Antworten gesendet werden und nach Komponenten, die Anforderungen ändern.</span><span class="sxs-lookup"><span data-stu-id="59e8b-249">Before responses are sent and after components that modify requests.</span></span> <span data-ttu-id="59e8b-250">Beispiele: weitergeleitete Header, URL-Umschreibung.</span><span class="sxs-lookup"><span data-stu-id="59e8b-250">Examples: Forwarded Headers, URL Rewriting.</span></span> |
| [<span data-ttu-id="59e8b-251">MVC</span><span class="sxs-lookup"><span data-stu-id="59e8b-251">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="59e8b-252">Verarbeitet Anforderungen mit MVC/Razor Pages (ASP.NET Core 2.0 oder höher).</span><span class="sxs-lookup"><span data-stu-id="59e8b-252">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="59e8b-253">Abschließend, wenn eine Anforderung mit einer Route übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-253">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="59e8b-254">OWIN</span><span class="sxs-lookup"><span data-stu-id="59e8b-254">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="59e8b-255">Interoperabilität mit auf OWIN basierten Apps, Servern und Middleware.</span><span class="sxs-lookup"><span data-stu-id="59e8b-255">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="59e8b-256">Abschließend, wenn die OWIN-Middleware die Anforderung vollständig verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="59e8b-256">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="59e8b-257">Zwischenspeichern von Antworten</span><span class="sxs-lookup"><span data-stu-id="59e8b-257">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="59e8b-258">Bietet Unterstützung für das Zwischenspeichern von Antworten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-258">Provides support for caching responses.</span></span> | <span data-ttu-id="59e8b-259">Vor Komponenten, für die das Zwischenspeichern erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="59e8b-259">Before components that require caching.</span></span> |
| [<span data-ttu-id="59e8b-260">Antwortkomprimierung</span><span class="sxs-lookup"><span data-stu-id="59e8b-260">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="59e8b-261">Bietet Unterstützung für das Komprimieren von Antworten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-261">Provides support for compressing responses.</span></span> | <span data-ttu-id="59e8b-262">Vor Komponenten, für die das Komprimieren erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="59e8b-262">Before components that require compression.</span></span> |
| [<span data-ttu-id="59e8b-263">Lokalisierung von Anforderungen</span><span class="sxs-lookup"><span data-stu-id="59e8b-263">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="59e8b-264">Bietet Unterstützung für die Lokalisierung.</span><span class="sxs-lookup"><span data-stu-id="59e8b-264">Provides localization support.</span></span> | <span data-ttu-id="59e8b-265">Vor der Lokalisierung vertraulicher Komponenten.</span><span class="sxs-lookup"><span data-stu-id="59e8b-265">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="59e8b-266">Routing</span><span class="sxs-lookup"><span data-stu-id="59e8b-266">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="59e8b-267">Definiert Anforderungsrouten und schränkt diese ein.</span><span class="sxs-lookup"><span data-stu-id="59e8b-267">Defines and constrains request routes.</span></span> | <span data-ttu-id="59e8b-268">Terminal für entsprechende Routen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-268">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="59e8b-269">Sitzung</span><span class="sxs-lookup"><span data-stu-id="59e8b-269">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="59e8b-270">Bietet Unterstützung für das Verwalten von Benutzersitzungen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-270">Provides support for managing user sessions.</span></span> | <span data-ttu-id="59e8b-271">Vor Komponenten, für die Sitzungen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="59e8b-271">Before components that require Session.</span></span> |
| [<span data-ttu-id="59e8b-272">Statische Dateien</span><span class="sxs-lookup"><span data-stu-id="59e8b-272">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="59e8b-273">Bietet Unterstützung für das Verarbeiten statischer Dateien und das Durchsuchen des Verzeichnisses.</span><span class="sxs-lookup"><span data-stu-id="59e8b-273">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="59e8b-274">Abschließend, wenn eine Anforderung mit einer Datei übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="59e8b-274">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="59e8b-275">URL-Umschreibung</span><span class="sxs-lookup"><span data-stu-id="59e8b-275">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="59e8b-276">Bietet Unterstützung für das Umschreiben von URLs und das Umleiten von Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-276">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="59e8b-277">Vor Komponenten, die die URL nutzen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-277">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="59e8b-278">WebSockets</span><span class="sxs-lookup"><span data-stu-id="59e8b-278">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="59e8b-279">Aktiviert das WebSockets-Protokoll.</span><span class="sxs-lookup"><span data-stu-id="59e8b-279">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="59e8b-280">Vor Komponenten, die WebSocket-Anforderungen annehmen müssen.</span><span class="sxs-lookup"><span data-stu-id="59e8b-280">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="additional-resources"></a><span data-ttu-id="59e8b-281">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="59e8b-281">Additional resources</span></span>

* <xref:fundamentals/middleware/write>
* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
