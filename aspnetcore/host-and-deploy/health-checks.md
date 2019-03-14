---
title: Integritätsprüfungen in ASP.NET Core
author: guardrex
description: Erfahren Sie, wie Sie Integritätsprüfungen für ASP.NET Core-Infrastrukturelemente wie Apps und Datenbanken einrichten.
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/health-checks
ms.openlocfilehash: e186a3cb484035199a8f355540c3e985db87ad98
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039297"
---
# <a name="health-checks-in-aspnet-core"></a>Integritätsprüfungen in ASP.NET Core

Von [Luke Latham](https://github.com/guardrex) und [Glenn Condron](https://github.com/glennc)

ASP.NET Core bietet Middleware für Integritätsprüfungen und Bibliotheken für die Berichterstellung für Komponenten der App-Infrastruktur.

Integritätsprüfungen werden von einer App als HTTP-Endpunkte verfügbar gemacht. Integritätsprüfungs-Endpunkte können für eine Vielzahl von Echtzeit-Überwachungsszenarien konfiguriert werden:

* Integritätstests können von Containerorchestratoren und Lastenausgleichsmodulen verwendet werden, um den Status einer App zu überprüfen. Ein Containerorchestrator kann z.B. auf eine fehlerhafte Integritätsprüfung reagieren, indem die Ausführung einer Bereitstellung angehalten oder ein Container neu gestartet wird. Ein Lastenausgleichsmodul kann auf eine fehlerhafte App reagieren, indem Datenverkehr von der fehlerhaften zu einer fehlerfreien Instanz umgeleitet wird.
* Die Nutzung von Arbeitsspeicher, Datenträgern und anderen physischen Serverressourcen kann auf einen fehlerfreien Status überwacht werden.
* Integritätsprüfungen können die Abhängigkeiten einer App testen, wie z.B. Datenbanken und externe Dienstendpunkte, um Verfügbarkeit und normale Funktionsweise zu bestätigen.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

Die Beispiel-App enthält Beispiele der Szenarien, die in diesem Thema beschrieben werden. Um die Beispiel-App für ein bestimmtes Szenario auszuführen, verwenden Sie den Befehl [dotnet run](/dotnet/core/tools/dotnet-run) aus dem Ordner des Projekts in einer Befehlsshell. Informationen zur Verwendung der Beispiel-App finden Sie in der Datei *README.md* der Beispiel-App und den Szenariobeschreibungen in diesem Thema.

## <a name="prerequisites"></a>Vorraussetzungen

Integritätsprüfungen werden in der Regel mit einem externen Überwachungsdienst oder Containerorchestrator verwendet, um den Status einer App zu überprüfen. Bevor Sie Integritätsprüfungen zu einer App hinzufügen, entscheiden Sie, welches Überwachungssystem verwendet werden soll. Das Überwachungssystem bestimmt, welche Arten von Integritätsprüfungen erstellt und wie die jeweiligen Endpunkte konfiguriert werden müssen.

Verweisen Sie auf das [Microsoft.AspNetCore.App-Metapaket](xref:fundamentals/metapackage-app), oder fügen Sie einen Paketverweis auf das Paket [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) hinzu.

Die Beispiel-App stellt Startcode bereit, um die Integritätsprüfungen für verschiedene Szenarien zu veranschaulichen. Das Szenario [Datenbanktest](#database-probe) überprüft die Integrität einer Datenbankverbindung mithilfe von [BeatPulse](https://github.com/Xabaril/BeatPulse). Das Szenario [DbContext-Test](#entity-framework-core-dbcontext-probe) überprüft eine Datenbank mithilfe eines EF Core-`DbContext`-Elements. Für ein Erkunden der Datenbankszenarios gilt für die Beispiel-App:

* Sie erstellt eine Datenbank und stellt deren Verbindungszeichenfolge in der Datei *appsettings.json* bereit.
* Sie hat die folgenden Paketverweise in ihrer Projektdatei:
  * [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/)
  * [Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore/)

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) wird von Microsoft nicht verwaltet oder unterstützt.

Ein anderes Szenario für Integritätsprüfungen zeigt, wie Sie Integritätsprüfungen auf einen Verwaltungsport filtern können. Für die Beispiel-App müssen Sie eine *Properties/launchSettings.json*-Datei erstellen, die die Verwaltungs-URL und den Verwaltungsport enthält. Weitere Informationen finden Sie im Abschnitt [Filtern nach Port](#filter-by-port).

## <a name="basic-health-probe"></a>Grundlegender Integritätstest

In vielen Apps genügt zur Ermittlung des App-Status eine grundlegende Integritätstestkonfiguration, die die Verfügbarkeit der App für die Verarbeitung von Anforderungen (*Lebendigkeit*) meldet.

Die grundlegende Konfiguration registriert Integritätsprüfungsdienste und ruft die Middleware für Integritätsprüfungen auf, damit diese an einem URL-Endpunkt mit dem Integritätsstatus antwortet. Standardmäßig werden keine spezifischen Integritätsprüfungen registriert, um eine bestimmte Abhängigkeit oder ein bestimmtes Subsystem zu testen. Die App wird als fehlerfrei angesehen, wenn sie an der URL des Integritätsendpunkts antworten kann. Der standardmäßige Antwortwriter schreibt den Status (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>) als Klartextantwort zurück an den Client und gibt den Status als [HealthStatus.Healthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus), [HealthStatus.Degraded](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) oder [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) an.

Registrieren Sie Integritätsprüfungsdienste mit <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> in `Startup.ConfigureServices`. Fügen Sie Middleware für Integritätsprüfungen mit <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> in der Anforderungsverarbeitungspipeline von `Startup.Configure` hinzu.

In der Beispiel-App wird der Integritätsprüfungs-Endpunkt in `/health` (*BasicStartup.cs*) erstellt:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/BasicStartup.cs?name=snippet1&highlight=5,10)]

Um das Szenario für die grundlegende Konfiguration mithilfe der Beispiel-App auszuführen, verwenden Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell:

```console
dotnet run --scenario basic
```

### <a name="docker-example"></a>Docker-Beispiel

[Docker](xref:host-and-deploy/docker/index) bietet eine integrierte `HEALTHCHECK`-Direktive, mit der Sie den Status einer App überprüfen können, die die grundlegende Konfiguration für Integritätsprüfungen verwendet:

```
HEALTHCHECK CMD curl --fail http://localhost:5000/health || exit
```

## <a name="create-health-checks"></a>Erstellen von Integritätsprüfungen

Integritätsprüfungen werden durch Implementieren der <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck>-Schnittstelle erstellt. Die <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck.CheckHealthAsync*>-Methode gibt ein `Task<` <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> `>` zurück, das die Integrität als `Healthy`, `Degraded` oder `Unhealthy` angibt. Das Ergebnis wird als Klartextantwort mit einem konfigurierbaren Statuscode geschrieben (diese Konfiguration wird im Abschnitt [Optionen für die Integritätsprüfung](#health-check-options) beschrieben). <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> kann auch optionale Schlüssel-Wert-Paare zurückgeben.

### <a name="example-health-check"></a>Beispiel für eine Integritätsprüfung

Die folgende `ExampleHealthCheck`-Klasse veranschaulicht das Layout einer Integritätsprüfung:

```csharp
public class ExampleHealthCheck : IHealthCheck
{
    public ExampleHealthCheck()
    {
        // Use dependency injection (DI) to supply any required services to the
        // health check.
    }

    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context, 
        CancellationToken cancellationToken = default(CancellationToken))
    {
        // Execute health check logic here. This example sets a dummy
        // variable to true.
        var healthCheckResultHealthy = true;

        if (healthCheckResultHealthy)
        {
            return Task.FromResult(
                HealthCheckResult.Healthy("The check indicates a healthy result."));
        }

        return Task.FromResult(
            HealthCheckResult.Unhealthy("The check indicates an unhealthy result."));
    }
}
```

### <a name="register-health-check-services"></a>Registrieren von Integritätsprüfungsdiensten

Der `ExampleHealthCheck`-Typ wird mit <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> zu den Integritätsprüfungsdiensten hinzugefügt:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck<ExampleHealthCheck>("example_health_check");
}
```

Die in der folgenden Abbildung gezeigte <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*>-Überladung legt den Fehlerstatus (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>) fest, der angegeben werden soll, wenn die Integritätsprüfung einen Fehler meldet. Wenn der Fehlerstatus auf `null` (Standardwert) festgelegt ist, wird [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) gemeldet. Diese Überladung ist ein nützliches Szenario für Bibliotheksersteller: Bei einem Integritätsprüfungsfehler wird der durch die Bibliothek angegebene Fehlerstatus von der App erzwungen, wenn die Implementierung der Integritätsprüfung die Einstellung berücksichtigt.

*Tags* können zum Filtern von Integritätsprüfungen verwendet werden (dies wird im Abschnitt [Filtern von Integritätsprüfungen](#filter-health-checks) genauer beschrieben).

```csharp
services.AddHealthChecks()
    .AddCheck<ExampleHealthCheck>(
        "example_health_check", 
        failureStatus: HealthStatus.Degraded, 
        tags: new[] { "example" });
```

<xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> kann auch eine Lambdafunktion ausführen. Im folgenden Beispiel wird der Name der Integritätsprüfung als `Example` angegeben, und die Prüfung gibt immer einen fehlerfreien Status zurück:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Example", () => 
            HealthCheckResult.Healthy("Example is OK!"), tags: new[] { "example" })
}
```

### <a name="use-health-checks-middleware"></a>Verwenden von Middleware für Integritätsprüfungen

Rufen Sie <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> in der Verarbeitungspipeline von `Startup.Configure` mit der Endpunkt-URL oder dem relativen Pfad auf:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health");
}
```

Wenn die Integritätsprüfungen an einem bestimmten Port lauschen sollen, verwenden Sie eine Überladung von <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*>, um den Port festzulegen (dies wird im Abschnitt [Filtern nach Port](#filter-by-port) genauer beschrieben):

```csharp
app.UseHealthChecks("/health", port: 8000);
```

Middleware für Integritätsprüfungen ist eine *Terminalmiddleware* in der Anforderungsverarbeitungspipeline der App. Der erste gefundene Integritätsprüfungs-Endpunkt, der eine exakte Übereinstimmung mit der Anforderungs-URL darstellt, wird ausgeführt und schließt den Rest der Middlewarepipeline kurz. Wenn kein Kurzschluss erfolgt, wird nach der durch Übereinstimmung ermittelten Integritätsprüfung keine weitere Middleware ausgeführt.

## <a name="health-check-options"></a>Optionen für die Integritätsprüfung

<xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions> ermöglichen die Anpassung des Verhaltens von Integritätsprüfungen:

* [Filtern von Integritätsprüfungen](#filter-health-checks)
* [Anpassen des HTTP-Statuscodes](#customize-the-http-status-code)
* [Unterdrücken von Cacheheadern](#suppress-cache-headers)
* [Anpassen der Ausgabe](#customize-output)

### <a name="filter-health-checks"></a>Filtern von Integritätsprüfungen

Standardmäßig führt die Middleware für Integritätsprüfungen alle registrierten Integritätsprüfungen aus. Um eine Teilmenge von Integritätsprüfungen auszuführen, stellen Sie eine Funktion bereit, die einen booleschen Wert an die Option <xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.Predicate> zurückgibt. Im folgenden Beispiel wird die `Bar`-Integritätsprüfung anhand ihres Tags (`bar_tag`) in der Bedingungsanweisung der Funktion herausgefiltert. Dabei wird `true` nur zurückgegeben, wenn die <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckRegistration.Tags>-Eigenschaft der Integritätsprüfung mit `foo_tag` oder `baz_tag` übereinstimmt:

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Foo", () => 
            HealthCheckResult.Healthy("Foo is OK!"), tags: new[] { "foo_tag" })
        .AddCheck("Bar", () => 
            HealthCheckResult.Unhealthy("Bar is unhealthy!"), tags: new[] { "bar_tag" })
        .AddCheck("Baz", () => 
            HealthCheckResult.Healthy("Baz is OK!"), tags: new[] { "baz_tag" });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // Filter out the 'Bar' health check. Only Foo and Baz execute.
        Predicate = (check) => check.Tags.Contains("foo_tag") || 
            check.Tags.Contains("baz_tag")
    });
}
```

### <a name="customize-the-http-status-code"></a>Anpassen des HTTP-Statuscodes

Verwenden Sie <xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.ResultStatusCodes>, um die Zuordnung des Integritätsstatus zu HTTP-Statuscodes anzupassen. Die folgenden <xref:Microsoft.AspNetCore.Http.StatusCodes>-Zuweisungen stellen die von der Middleware verwendeten Standardwerte dar. Ändern Sie die Statuscodewerte so, dass sie Ihren Anforderungen entsprechen.

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The following StatusCodes are the default assignments for
        // the HealthStatus properties.
        ResultStatusCodes =
        {
            [HealthStatus.Healthy] = StatusCodes.Status200OK,
            [HealthStatus.Degraded] = StatusCodes.Status200OK,
            [HealthStatus.Unhealthy] = StatusCodes.Status503ServiceUnavailable
        }
    });
}
```

### <a name="suppress-cache-headers"></a>Unterdrücken von Cacheheadern

<xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.AllowCachingResponses> steuert, ob die Middleware für Integritätsprüfungen einer Testantwort HTTP-Header hinzufügt, um die Zwischenspeicherung von Antworten zu verhindern. Wenn der Wert `false` (Standard) lautet, legt die Middleware die Header `Cache-Control`, `Expires` und `Pragma` fest oder überschreibt sie, um eine Zwischenspeicherung der Antworten zu verhindern. Wenn der Wert `true` lautet, ändert die Middleware die Cacheheader der Antwort nicht.

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The default value is false.
        AllowCachingResponses = false
    });
}
```

### <a name="customize-output"></a>Anpassen der Ausgabe

Mit der Option <xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.ResponseWriter> wird ein Delegat abgerufen oder festgelegt, der zum Schreiben der Antwort verwendet wird. Der Standarddelegat schreibt eine minimale Klartextantwort mit dem Zeichenfolgenwert [HealthReport.Status](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthReport.Status).

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // WriteResponse is a delegate used to write the response.
        ResponseWriter = WriteResponse
    });
}

private static Task WriteResponse(HttpContext httpContext, 
    HealthReport result)
{
    httpContext.Response.ContentType = "application/json";

    var json = new JObject(
        new JProperty("status", result.Status.ToString()),
        new JProperty("results", new JObject(result.Entries.Select(pair =>
            new JProperty(pair.Key, new JObject(
                new JProperty("status", pair.Value.Status.ToString()),
                new JProperty("description", pair.Value.Description),
                new JProperty("data", new JObject(pair.Value.Data.Select(
                    p => new JProperty(p.Key, p.Value))))))))));
    return httpContext.Response.WriteAsync(
        json.ToString(Formatting.Indented));
}
```

## <a name="database-probe"></a>Datenbanktest

Eine Integritätsprüfung kann eine Datenbankabfrage angeben, die als boolescher Test ausgeführt wird, um zu ermitteln, ob die Datenbank normal reagiert.

Die Beispiel-App verwendet [BeatPulse](https://github.com/Xabaril/BeatPulse), eine Bibliothek für Integritätsprüfungen für ASP.NET Core-Apps, um eine Integritätsprüfung für eine SQL Server-Datenbank auszuführen. BeatPulse führt eine `SELECT 1`-Abfrage in der Datenbank aus, um zu bestätigen, dass die Verbindung mit der Datenbank fehlerfrei ist.

> [!WARNING]
> Wenn Sie die Datenbankverbindung mithilfe einer Abfrage überprüfen, wählen Sie eine Abfrage aus, die eine schnelle Antwort zurückgibt. Bei einer Abfrage besteht immer das Risiko, dass die Datenbank überladen und ihre Leistung beeinträchtigt wird. In den meisten Fällen ist es nicht notwendig, eine Testabfrage auszuführen. Es genügt zumeist, einfach erfolgreich eine Verbindung mit der Datenbank herzustellen. Wenn Sie eine Abfrage ausführen müssen, wählen Sie eine einfache SELECT-Abfrage aus, wie z.B. `SELECT 1`.

Um die BeatPulse-Bibliothek zu verwenden, schließen Sie einen Paketverweis auf [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/) ein.

Geben Sie in der Datei *appsettings.json* der App eine gültige Zeichenfolge für die Datenbankverbindung an. Die App verwendet eine SQL Server-Datenbank namens `HealthCheckSample`:

[!code-json[](health-checks/samples/2.x/HealthChecksSample/appsettings.json?highlight=3)]

Registrieren Sie Integritätsprüfungsdienste mit <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> in `Startup.ConfigureServices`. Die Beispiel-App ruft die `AddSqlServer`-Methode von BeatPulse mit der Verbindungszeichenfolge der Datenbank (*DbHealthStartup.cs*) auf:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_ConfigureServices)]

Rufen Sie die Middleware für Integritätsprüfungen in der App-Verarbeitungspipeline in `Startup.Configure` auf:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_Configure)]

Um das Szenario für den Datenbanktest mithilfe der Beispiel-App auszuführen, verwenden Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell:

```console
dotnet run --scenario db
```

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) wird von Microsoft nicht verwaltet oder unterstützt.

## <a name="entity-framework-core-dbcontext-probe"></a>Entity Framework Core-DbContext-Test

Die `DbContext`-Überprüfung bestätigt, dass die App mit der Datenbank kommunizieren kann, die für einen EF Core-`DbContext` konfiguriert wurde. Die `DbContext` Überprüfung wird in Apps unterstützt, für die gilt:

* In ihnen wird [Entity Framework Core (EF Core)](/ef/core/) verwendet.
* Sie enthalten einen Paketverweis auf [Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore/).

`AddDbContextCheck<TContext>` registriert eine Integritätsprüfung für einen `DbContext`. Der `DbContext` wird als der `TContext` für die Methode bereitgestellt. Eine Überladung ist verfügbar, um den Fehlerstatus, Tags sowie eine benutzerdefinierte Testabfrage zu konfigurieren.

Standardmäßig:

* `DbContextHealthCheck` ruft die `CanConnectAsync`-Methode von EF Core auf. Sie können festlegen, welcher Vorgang ausgeführt wird, wenn die Integrität mit `AddDbContextCheck`-Methodenüberladungen überprüft wird.
* Der Name der Integritätsprüfung ist der Name des `TContext`-Typs.

In der Beispiel-App wird `AppDbContext` für `AddDbContextCheck` bereitgestellt und als Dienst in `Startup.ConfigureServices` registriert.

*DbContextHealthStartup.cs*:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_ConfigureServices)]

In der Beispiel-App fügt `UseHealthChecks` die Middleware für Integritätsprüfungen in `Startup.Configure` hinzu.

*DbContextHealthStartup.cs*:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_Configure)]

Um das `DbContext`-Testszenario unter Verwendung der Beispiel-App auszuführen, stellen Sie sicher, dass die durch die Verbindungszeichenfolge angegebene Datenbank in der SQL Server-Instanz nicht vorhanden ist. Falls die Datenbank vorhanden ist, löschen Sie sie.

Führen Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell aus:

```console
dotnet run --scenario dbcontext
```

Wenn die App ausgeführt wird, überprüfen Sie den Integritätsstatus, indem Sie in einem Browser eine Anforderung an den `/health`-Endpunkt senden. Datenbank und `AppDbContext` sind nicht vorhanden, also sendet die App die folgende Antwort:

```
Unhealthy
```

Fordern Sie die Beispiel-App auf, die Datenbank zu erstellen. Senden Sie eine `/createdatabase`-Anforderung. Die App sendet die folgende Antwort:

```
Creating the database...
Done!
Navigate to /health to see the health status.
```

Senden Sie eine Anforderung an den `/health`-Endpunkt. Datenbank und Kontext sind vorhanden, also sendet die App die folgende Antwort:

```
Healthy
```

Fordern Sie die Beispiel-App auf, die Datenbank zu löschen. Senden Sie eine `/deletedatabase`-Anforderung. Die App sendet die folgende Antwort:

```
Deleting the database...
Done!
Navigate to /health to see the health status.
```

Senden Sie eine Anforderung an den `/health`-Endpunkt. Die App meldet einen fehlerhaften Status:

```
Unhealthy
```

## <a name="separate-readiness-and-liveness-probes"></a>Separate Tests für Bereitschaft und Lebendigkeit

In einigen Hostingszenarien wird ein Integritätsprüfungspaar verwendet, bei dem zwischen zwei App-Status unterschieden wird:

* Die App funktioniert, ist aber noch nicht für den Empfang von Anforderungen bereit. Dieser Status gibt die *Bereitschaft* der App wieder.
* Die App funktioniert und antwortet auf Anforderungen. Dieser Status gibt die *Lebendigkeit* der App wieder.

Die Bereitschaftsprüfung führt in der Regel eine Reihe umfassenderer und zeitaufwendigerer Überprüfungen durch, um zu ermitteln, ob alle Subsysteme und Ressourcen der App verfügbar sind. Eine Lebendigkeitsprüfung führt nur eine schnelle Überprüfung aus, um zu ermitteln, ob die App für die Verarbeitung von Anforderungen verfügbar ist. Nachdem die App die Bereitschaftsprüfung einmal bestanden hat, muss die App nicht weiter mit diesen Prüfungen belastet werden – weitere Prüfungen müssen dann nur noch für die Lebendigkeit erfolgen.

Die Beispiel-App enthält eine Integritätsprüfung, um den Abschluss eines Starttasks mit langer Ausführungsdauer in einem [gehosteten Dienst](xref:fundamentals/host/hosted-services) zu melden. `StartupHostedServiceHealthCheck` macht die Eigenschaft `StartupTaskCompleted` verfügbar, die der gehostete Dienst auf `true` festlegen kann, wenn der Task mit langer Ausführungsdauer abgeschlossen ist (*StartupHostedServiceHealthCheck.cs*):

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/StartupHostedServiceHealthCheck.cs?name=snippet1&highlight=5)]

Der Hintergrundtask mit langer Ausführungsdauer wird von einem [gehosteten Dienst](xref:fundamentals/host/hosted-services) (*Services/StartupHostedService*) gestartet. Nach Abschluss des Tasks wird `StartupHostedServiceHealthCheck.StartupTaskCompleted` auf `true` festgelegt:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/Services/StartupHostedService.cs?name=snippet1&highlight=18-20)]

Die Integritätsprüfung wird mit <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> zusammen mit dem gehosteten Dienst in `Startup.ConfigureServices` registriert. Da der gehostete Dienst die Eigenschaft in der Integritätsprüfung festlegen muss, wird die Integritätsprüfung ebenfalls im Dienstcontainer (*LivenessProbeStartup.cs*) registriert:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices)]

Rufen Sie die Middleware für Integritätsprüfungen in der App-Verarbeitungspipeline in `Startup.Configure` auf. In der Beispiel-App werden die Integritätsprüfungs-Endpunkte in `/health/ready` für die Bereitschaftsprüfung und in `/health/live` für die Lebendigkeitsprüfung erstellt. Die Bereitschaftsprüfung filtert auf Integritätsprüfungen mit dem `ready`-Tag. Die Lebendigkeitsprüfung filtert `StartupHostedServiceHealthCheck` durch Rückgabe von `false` in [HealthCheckOptions.Predicate](xref:Microsoft.AspNetCore.Diagnostics.HealthChecks.HealthCheckOptions.Predicate) heraus (weitere Informationen finden Sie unter [Filtern von Integritätsprüfungen](#filter-health-checks)):

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_Configure)]

Um das Szenario für die Konfiguration von Bereitschafts-/Lebendigkeitsprüfungen mithilfe der Beispiel-App auszuführen, verwenden Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell:

```console
dotnet run --scenario liveness
```

Besuchen Sie `/health/ready` mehrmals in einem Browser, bis 15 Sekunden verstrichen sind. Die Integritätsprüfung meldet während der ersten 15 Sekunden *Fehlerhaft*. Nach 15 Sekunden meldet der Endpunkt *Fehlerfrei*, was darauf hindeutet, dass die Ausführung des Tasks mit langer Ausführungsdauer durch den gehosteten Dienst abgeschlossen wurde.

In diesem Beispiel wird auch ein Herausgeber der Integritätsprüfung erstellt (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Implementierung), der die erste Bereitschaftsprüfung mit einer Verzögerung von zwei Sekunden ausführt. Weitere Informationen finden Sie im Abschnitt [Herausgeber der Integritätsprüfung](#health-check-publisher).

### <a name="kubernetes-example"></a>Kubernetes-Beispiel

Die Verwendung von Bereitschafts- und Lebendigkeitstests ist in Umgebungen wie [Kubernetes](https://kubernetes.io/) sehr nützlich. In Kubernetes muss eine App möglicherweise zeitaufwendige Startaufgaben ausführen, bevor sie Anforderungen wie z.B. das Testen der Verfügbarkeit der zugrunde liegenden Datenbank annehmen kann. Durch Verwendung separater Überprüfungen kann der Orchestrator unterscheiden, ob eine App funktioniert, aber noch nicht bereit ist, oder ob die App nicht gestartet wurde. Weitere Informationen zu Bereitschafts- und Lebendigkeitstests in Kubernetes finden Sie in der Kubernetes-Dokumentation unter [Configure Liveness and Readiness Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) (Konfigurieren von Lebendigkeits- und Bereitschaftstests).

Das folgende Beispiel veranschaulicht die Konfiguration eines Bereitschaftstests in Kubernetes:

```
spec:
  template:
  spec:
    readinessProbe:
      # an http probe
      httpGet:
        path: /health/ready
        port: 80
      # length of time to wait for a pod to initialize
      # after pod startup, before applying health checking
      initialDelaySeconds: 30
      timeoutSeconds: 1
    ports:
      - containerPort: 80
```

## <a name="metric-based-probe-with-a-custom-response-writer"></a>Metrikbasierter Test mit einem benutzerdefinierten Antwortwriter

Die Beispiel-App veranschaulicht eine Arbeitsspeicher-Integritätsprüfung mit einem benutzerdefinierten Antwortwriter.

`MemoryHealthCheck` meldet einen beeinträchtigten Status, wenn die App mehr Arbeitsspeicher verwendet, als für den Schwellenwert festgelegt wurde (1 GB in der Beispiel-App). Das <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckResult> enthält Garbage Collector-Informationen (GC) für die App (*MemoryHealthCheck.cs*):

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/MemoryHealthCheck.cs?name=snippet1)]

Registrieren Sie Integritätsprüfungsdienste mit <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> in `Startup.ConfigureServices`. Die Integritätsprüfung wird nicht durch Übergabe an <xref:Microsoft.Extensions.DependencyInjection.HealthChecksBuilderAddCheckExtensions.AddCheck*> aktiviert, stattdessen wird `MemoryHealthCheck` als Dienst registriert. Alle bei <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck> registrierten Dienste stehen für die Dienste und Middleware für Integritätsprüfungen zur Verfügung. Es wird empfohlen, Integritätsprüfungsdienste als Singleton-Dienste zu registrieren.

*CustomWriterStartup.cs*:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_ConfigureServices&highlight=4)]

Rufen Sie die Middleware für Integritätsprüfungen in der App-Verarbeitungspipeline in `Startup.Configure` auf. Ein `WriteResponse`-Delegat wird in der `ResponseWriter`-Eigenschaft angegeben, um eine benutzerdefinierte JSON-Antwort auszugeben, wenn die Integritätsprüfung ausgeführt wird:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_Configure&highlight=6)]

Die `WriteResponse`-Methode formatiert das `CompositeHealthCheckResult` als JSON-Objekt und führt zu folgender JSON-Ausgabe für die Integritätsprüfungsantwort:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_WriteResponse)]

Um den metrikbasierten Test mit benutzerdefinierter Ausgabe des Antwortwriters mithilfe der Beispiel-App auszuführen, verwenden Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell:

```console
dotnet run --scenario writer
```

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) enthält Szenarien für metrikbasierte Integritätsprüfungen, einschließlich Prüfungen des Datenträgerspeichers und Lebendigkeitsprüfungen mit Maximalwert.
>
> [BeatPulse](https://github.com/Xabaril/BeatPulse) wird von Microsoft nicht verwaltet oder unterstützt.

## <a name="filter-by-port"></a>Filtern nach Port

Wenn <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> mit einem Port aufgerufen wird, werden Anforderungen durch Integritätsprüfungen auf den angegebenen Port beschränkt. Dieses Vorgehen wird normalerweise in einer Containerumgebung angewendet, um einen Port für Überwachungsdienste verfügbar zu machen.

Die Beispiel-App konfiguriert den Port mithilfe des [Umgebungsvariablen-Konfigurationsanbieters](xref:fundamentals/configuration/index#environment-variables-configuration-provider). Der Port wird in der Datei *launchSettings.json* festgelegt und über eine Umgebungsvariable an den Konfigurationsanbieter übergeben. Sie müssen den Server auch so konfigurieren, dass er am Verwaltungsport auf Anforderungen lauscht.

Um die Beispiel-App zum Veranschaulichen der Konfiguration des Verwaltungsports zu verwenden, erstellen Sie die Datei *launchSettings.json* in einem *Eigenschaften*-Ordner.

Die folgende *launchSettings.json* ist in den Projektdateien der Beispiel-App nicht vorhanden und muss manuell erstellt werden.

*Properties/launchSettings.json*:

```json
{
  "profiles": {
    "SampleApp": {
      "commandName": "Project",
      "commandLineArgs": "",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_URLS": "http://localhost:5000/;http://localhost:5001/",
        "ASPNETCORE_MANAGEMENTPORT": "5001"
      },
      "applicationUrl": "http://localhost:5000/"
    }
  }
}
```

Registrieren Sie Integritätsprüfungsdienste mit <xref:Microsoft.Extensions.DependencyInjection.HealthCheckServiceCollectionExtensions.AddHealthChecks*> in `Startup.ConfigureServices`. Der Aufruf von <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> gibt den Verwaltungsport an (*ManagementPortStartup.cs*):

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ManagementPortStartup.cs?name=snippet1&highlight=12,18)]

> [!NOTE]
> Sie können es vermeiden, die Datei *launchSettings.json* in der Beispiel-App erstellen zu müssen, indem Sie die URLs und den Verwaltungsport explizit im Code festlegen. Fügen Sie in *Program.cs* an der Stelle, an der <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> erstellt wird, einen Aufruf von <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseUrls*> hinzu, und geben Sie den normalen Antwortendpunkt der App und den Endpunkt des Verwaltungsports an. Geben Sie in *ManagementPortStartup.cs* an der Stelle, an der <xref:Microsoft.AspNetCore.Builder.HealthCheckApplicationBuilderExtensions.UseHealthChecks*> aufgerufen wird, explizit den Verwaltungsport an.
>
> *Program.cs*:
>
> ```csharp
> return new WebHostBuilder()
>     .UseConfiguration(config)
>     .UseUrls("http://localhost:5000/;http://localhost:5001/")
>     .ConfigureLogging(builder =>
>     {
>         builder.SetMinimumLevel(LogLevel.Trace);
>         builder.AddConfiguration(config);
>         builder.AddConsole();
>     })
>     .UseKestrel()
>     .UseStartup(startupType)
>     .Build();
> ```
>
> *ManagementPortStartup.cs*:
>
> ```csharp
> app.UseHealthChecks("/health", port: 5001);
> ```

Um das Szenario für die Konfiguration des Verwaltungsports mithilfe der Beispiel-App auszuführen, verwenden Sie den folgenden Befehl aus dem Ordner des Projekts in einer Befehlsshell:

```console
dotnet run --scenario port
```

## <a name="distribute-a-health-check-library"></a>Verteilen einer Integritätsprüfungsbibliothek

So verteilen Sie eine Integritätsprüfung als Bibliothek:

1. Schreiben Sie eine Integritätsprüfung, die die <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheck>-Schnittstelle als eigenständige Klasse implementiert. Die Klasse kann [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) (Dependency Injection, DI), Typaktivierung und [benannte Optionen](xref:fundamentals/configuration/options) verwenden, um auf Konfigurationsdaten zuzugreifen.

   ```csharp
   using System;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   namespace SampleApp
   {
       public class ExampleHealthCheck : IHealthCheck
       {
           private readonly string _data1;
           private readonly int? _data2;

           public ExampleHealthCheck(string data1, int? data2)
           {
               _data1 = data1 ?? throw new ArgumentNullException(nameof(data1));
               _data2 = data2 ?? throw new ArgumentNullException(nameof(data2));
           }

           public async Task<HealthCheckResult> CheckHealthAsync(
               HealthCheckContext context, CancellationToken cancellationToken)
           {
               try
               {
                   // Health check logic
                   //
                   // data1 and data2 are used in the method to
                   // run the probe's health check logic.

                   // Assume that it's possible for this health check
                   // to throw an AccessViolationException.

                   return HealthCheckResult.Healthy();
               }
               catch (AccessViolationException ex)
               {
                   return new HealthCheckResult(
                       context.Registration.FailureStatus,
                       description: "An access violation occurred during the check.",
                       exception: ex,
                       data: null);
               }
           }
       }
   }
   ```

1. Schreiben Sie eine Erweiterungsmethode mit Parametern, die von der nutzenden App in ihrer `Startup.Configure`-Methode aufgerufen werden. Nehmen Sie im folgenden Beispiel die folgende Signatur für die Integritätsprüfungsmethode an:

   ```csharp
   ExampleHealthCheck(string, string, int )
   ```

   Die oben stehende Signatur gibt an, dass `ExampleHealthCheck` weitere Daten benötigt, um die Testlogik für die Integritätsprüfung zu verarbeiten. Die Daten werden für den Delegaten bereitgestellt, der zum Erstellen der Integritätsprüfungsinstanz verwendet wird, wenn die Integritätsprüfung bei einer Erweiterungsmethode registriert wird. Im folgenden Beispiel gibt der Aufrufer optional Folgendes an:

   * Name der Integritätsprüfung (`name`). Wenn der Wert `null` ist, wird `example_health_check` verwendet.
   * string-Datenpunkt für die Integritätsprüfung (`data1`).
   * integer-Datenpunkt für die Integritätsprüfung (`data2`). Wenn der Wert `null` ist, wird `1` verwendet.
   * Fehlerstatus (<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus>). Die Standardeinstellung ist `null`. Wenn `null`, wird [HealthStatus.Unhealthy](xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthStatus) als Fehlerstatus gemeldet.
   * Tags (`IEnumerable<string>`).

   ```csharp
   using System.Collections.Generic;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   public static class ExampleHealthCheckBuilderExtensions
   {
       const string NAME = "example_health_check";

       public static IHealthChecksBuilder AddExampleHealthCheck(
           this IHealthChecksBuilder builder, 
           string name = default, 
           string data1, 
           int data2 = 1, 
           HealthStatus? failureStatus = default, 
           IEnumerable<string> tags = default)
       {
           return builder.Add(new HealthCheckRegistration(
               name ?? NAME,
               sp => new ExampleHealthCheck(data1, data2),
               failureStatus,
               tags));
       }
   }
   ```

## <a name="health-check-publisher"></a>Herausgeber der Integritätsprüfung

Wenn dem Dienstcontainer ein <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> hinzugefügt wird, führt das Integritätsprüfungssystem Ihre Integritätsprüfungen regelmäßig aus und ruft `PublishAsync` mit dem Ergebnis auf. Dies ist nützlich in einem Szenario mit pushbasiertem Integritätsüberwachungssystem, in dem jeder Prozess das Überwachungssystem regelmäßig aufrufen muss, um die Integrität zu bestimmen.

Die <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Schnittstelle weist eine einzige Methode auf:

```csharp
Task PublishAsync(HealthReport report, CancellationToken cancellationToken);
```

<xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions> ermöglichen Ihnen, Folgendes festzulegen:

* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Delay> &ndash; Die nach der App angewendete anfängliche Verzögerung beginnt vor der Ausführung von <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Instanzen. Die Verzögerung wird einmal beim Start angewendet und gilt nicht für die nachfolgenden Iterationen. Der Standardwert beträgt fünf Sekunden.
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Period> &ndash; Der Zeitraum der <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Ausführung. Der Standardwert ist 30 Sekunden.
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Predicate> &ndash; Wenn <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Predicate> `null` ist (Standard), führt der Herausgeber der Integritätsprüfung alle registrierten Integritätsüberprüfungen durch. Um eine Teilmenge von Integritätsprüfungen auszuführen, stellen Sie eine Funktion bereit, die die Menge der Prüfungen filtert. Das Prädikat wird in jedem Zeitraum ausgewertet.
* <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Timeout> &ndash; Das Timeout für die Ausführung der Integritätsprüfungen für alle <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Instanzen. Verwenden Sie <xref:System.Threading.Timeout.InfiniteTimeSpan> zur Ausführung ohne Timeout. Der Standardwert ist 30 Sekunden.

::: moniker range="= aspnetcore-2.2"

> [!WARNING]
> Im Release ASP.NET Core 2.2 wird die Einstellung <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Period> nicht von der <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Implementierung berücksichtigt; sie legt den Wert von <xref:Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherOptions.Delay> fest. Dieses Problem wird in ASP.NET Core 3.0 behoben. Weitere Informationen finden Sie unter [HealthCheckPublisherOptions.Period sets the value of .Delay (HealthCheckPublisherOptions.Period legt den Wert von „.Delay“ fest)](https://github.com/aspnet/Extensions/issues/1041).

::: moniker-end

In der Beispiel-App ist `ReadinessPublisher` eine <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Implementierung. Der Integritätsprüfungstatus wird in `Entries` aufgezeichnet und für jede Überprüfung protokolliert:

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ReadinessPublisher.cs?name=snippet_ReadinessPublisher&highlight=20,22-23)]

Im Beispiel `LivenessProbeStartup` der Beispiel-App `StartupHostedService` hat die Bereitschaftsprüfung eine Startverzögerung von zwei Sekunden und führt die Prüfung alle 30 Sekunden aus. Zum Aktivieren der <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher> Implementierung registriert das Beispiel `ReadinessPublisher` als Singletondienst im [Abhängigkeitsinjektionscontainer (Dependency Injection, DI)](xref:fundamentals/dependency-injection):

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices&highlight=12-17,28)]

::: moniker range="= aspnetcore-2.2"

> [!NOTE]
> Die folgende Problemumgehung ermöglicht das Hinzufügen einer <xref:Microsoft.Extensions.Diagnostics.HealthChecks.IHealthCheckPublisher>-Instanz zum Dienstcontainer, wenn einer oder mehrere andere gehostete Dienste der App bereits hinzugefügt wurden. Diese Problemumgehung ist mit dem Release von ASP.NET Core 3.0 nicht mehr erforderlich. Weitere Informationen finden Sie unter https://github.com/aspnet/Extensions/issues/639.
>
> ```csharp
> private const string HealthCheckServiceAssembly = 
>     "Microsoft.Extensions.Diagnostics.HealthChecks.HealthCheckPublisherHostedService";
>
> services.TryAddEnumerable(
>     ServiceDescriptor.Singleton(typeof(IHostedService), 
>         typeof(HealthCheckPublisherOptions).Assembly
>             .GetType(HealthCheckServiceAssembly)));
> ```

::: moniker-end

> [!NOTE]
> [BeatPulse](https://github.com/Xabaril/BeatPulse) enthält Herausgeber für verschiedene Systeme, einschließlich [Application Insights](/azure/application-insights/app-insights-overview).
>
> [BeatPulse](https://github.com/Xabaril/BeatPulse) wird von Microsoft nicht verwaltet oder unterstützt.
