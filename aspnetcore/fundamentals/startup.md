---
title: Anwendungsstart in ASP.NET Core
author: tdykstra
description: Informationen zur Funktionsweise der Startklasse in ASP.NET Core bei der Konfiguration von Diensten und der Anforderungspipeline einer App.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/17/2019
uid: fundamentals/startup
ms.openlocfilehash: cfd0a57d5d0b60862b017a170b6d5cbddf56f15a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025357"
---
# <a name="app-startup-in-aspnet-core"></a>Anwendungsstart in ASP.NET Core

Von [Tom Dykstra](https://github.com/tdykstra), [Luke Latham](https://github.com/guardrex) und [Steve Smith](https://ardalis.com)

Die `Startup`-Klasse konfiguriert Dienste und die Anforderungspipeline einer App.

## <a name="the-startup-class"></a>Die Startup-Klasse

ASP.NET Core-Apps verwenden eine `Startup`-Klasse, die standardmäßig `Startup` genannt wird. Die `Startup`-Klasse:

* Kann eine <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*>-Methode enthalten, um die *Dienste* der App zu konfigurieren. Ein Dienst ist eine wiederverwendbare Komponente, die App-Funktionalität bereitstellt. Dienste werden in `ConfigureServices` konfiguriert, was auch als *registrieren* bezeichnet wird, und in der App über [Dependency Injection](xref:fundamentals/dependency-injection) oder <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*> genutzt.
* Enthält eine <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*>-Methode, um die Anforderungsverarbeitungspipeline einer App zu erstellen.

`ConfigureServices` und `Configure` werden beim App-Start durch die Runtime aufgerufen:

[!code-csharp[](startup/sample_snapshot/Startup1.cs?highlight=4,10)]

Die `Startup`-Klasse wird für die App angegeben, wenn der [Host](xref:fundamentals/index#host) der App erstellt wird. Der App-Host wird erstellt, wenn `Build` im Hostgenerator in der `Program`-Klasse aufgerufen wird. Die `Startup`-Klasse wird normalerweise angegeben, indem die [WebHostBuilderExtensions.UseStartup\<TStartup>](xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*)-Methode im Hostgenerator aufgerufen wird:

[!code-csharp[](startup/sample_snapshot/Program3.cs?name=snippet_Program&highlight=10)]

Der Host stellt Dienste für den `Startup`-Klassenkonstruktor bereit. Die App fügt über `ConfigureServices` zusätzliche Dienste hinzu. Daher sind sowohl die Host- als auch die App-Dienste in `Configure` und über die App verfügbar.

[Dependency Injection](xref:fundamentals/dependency-injection) wird häufig im Zusammenhang mit der `Startup`-Klasse verwendet, um Folgendes einzufügen:

* <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment>, um Dienste nach Umgebung zu konfigurieren.
* <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>, um Konfigurationen zu lesen.
* <xref:Microsoft.Extensions.Logging.ILoggerFactory>, um eine Protokollierung in `Startup.ConfigureServices` zu erstellen.

[!code-csharp[](startup/sample_snapshot/Startup2.cs?highlight=7-8)]

Sie können auch einen konventionsbasierten Ansatz wählen, anstatt `IHostingEnvironment` einzufügen. Wenn die App unterschiedliche `Startup`-Klassen für unterschiedliche Umgebungen definiert (z.B. `StartupDevelopment`), wird zur Laufzeit die entsprechende `Startup`-Klasse ausgewählt. Die Klasse, deren Namenssuffix mit der aktuellen Umgebung übereinstimmt, wird priorisiert. Wenn die App in der Entwicklungsumgebung ausgeführt wird und sowohl eine `Startup`-Klasse als auch eine `StartupDevelopment`-Klasse enthält, wird die `StartupDevelopment`-Klasse verwendet. Weitere Informationen finden Sie unter [Verwenden mehrerer Umgebungen](xref:fundamentals/environments#environment-based-startup-class-and-methods).

Weitere Informationen zum Host finden Sie unter [Der Host](xref:fundamentals/index#host). Weitere Informationen zum Umgang mit Fehlern beim Start finden Sie unter [Startup exception handling (Umgang mit Ausnahmen beim Start)](xref:fundamentals/error-handling#startup-exception-handling).

## <a name="the-configureservices-method"></a>Die ConfigureServices-Methode

Die <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*>-Methode:

* Dies ist optional.
* wird vor der `Configure`-Methode vom Host aufgerufen, um die App-Dienste zu konfigurieren.
* Über diese Methode werden standardmäßig [Konfigurationsoptionen](xref:fundamentals/configuration/index) festgelegt.

Das typische Muster besteht darin, alle `Add{Service}`-Methoden und dann alle `services.Configure{Service}`-Methoden aufzurufen. Ein Beispiel finden Sie unter [Konfigurieren der Identitätsdienste](xref:security/authentication/identity#pw).

Es kann sein, dass der Host einige Dienste konfiguriert, bevor die `Startup`-Methoden aufgerufen werden. Weitere Informationen finden Sie unter [Der Host](xref:fundamentals/index#host).

Für Features, die ein umfangreiches Setup erfordern, sind in <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection> `Add{Service}`-Erweiterungsmethoden verfügbar. ASP.NET Core-Apps registrieren Dienste in der Regel für Entity Framework, Identity und MVC:

[!code-csharp[](startup/sample_snapshot/Startup3.cs?highlight=4,7,11)]

Wenn Sie Dienste zum Dienstcontainer hinzufügen, können Sie auch über die App und die `Configure`-Methode auf diese zugreifen. Die Dienste werden über die [Dependency Injection](xref:fundamentals/dependency-injection) oder über <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*> aufgelöst.

## <a name="the-configure-method"></a>Die Configure-Methode

Die <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*>-Methode wird verwendet, um festzulegen, wie die App auf HTTP-Anforderungen reagiert. Sie können die Anforderungspipeline konfigurieren, indem Sie [Middlewarekomponenten](xref:fundamentals/middleware/index) zu einer <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>-Instanz hinzufügen. Die `Configure`-Methode kann auf `IApplicationBuilder` zugreifen, wird aber nicht im Dienstcontainer registriert. Über das Hosting wird ein `IApplicationBuilder` erstellt, der direkt an `Configure` übergeben wird.

Die [ASP.NET Core-Vorlagen](/dotnet/core/tools/dotnet-new) konfigurieren die Pipeline mit Unterstützung für:

* [die Seite mit Ausnahmen für Entwickler](xref:fundamentals/error-handling#the-developer-exception-page)
* [Ausnahmehandler](xref:fundamentals/error-handling#configure-a-custom-exception-handling-page)
* [HTTP Strict Transport Security (HSTS)](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts)
* [HTTPS-Umleitung](xref:security/enforcing-ssl)
* [Statische Dateien](xref:fundamentals/static-files)
* [die Datenschutzgrundverordnung (DSGVO)](xref:security/gdpr)
* ASP.NET Core-[MVC](xref:mvc/overview) und [Razor Pages](xref:razor-pages/index)

[!code-csharp[](startup/sample_snapshot/Startup4.cs)]

Jede `Use`-Erweiterungsmethode fügt mindestens eine Middlewarekomponente zu der Anforderungspipeline hinzu. Die `UseMvc`-Erweiterungsmethode fügt z.B. [Routingmiddleware](xref:fundamentals/routing) zur Anforderungspipeline hinzu und konfiguriert [MVC](xref:mvc/overview) als Standardhandler.

Jede Middlewarekomponente in der Anforderungspipeline ist für das Aufrufen der jeweils nächsten Komponente in der Pipeline oder, wenn nötig, für das Kurzschließen der Kette zuständig. Wenn das Kurzschließen nicht entlang der Middlewarekette passiert, hat jede Middleware eine zweite Chance die Anforderung zu verarbeiten, bevor sie an den Client gesendet wird.

In der `Configure`-Methodensignatur können außerdem auch zusätzliche Dienste wie `IHostingEnvironment` und `ILoggerFactory` festgelegt werden. Wenn Sie zusätzliche Dienste angegeben, werden diese eingefügt, sofern sie verfügbar sind.

Weitere Informationen zur Verwendung von `IApplicationBuilder` und der Reihenfolge der Middlewareverarbeitung finden Sie unter <xref:fundamentals/middleware/index>.

## <a name="convenience-methods"></a>Hilfsmethoden

Rufen Sie die Hilfsmethoden `ConfigureServices` und `Configure` im Hostgenerator auf, um Dienste und die Anforderungsverarbeitungspipeline ohne die `Startup`-Klasse zu konfigurieren. Wenn `ConfigureServices` mehrmals aufgerufen wird, werden diese Aufrufe einander angefügt. Wenn es mehrere Aufrufe der Methode `Configure` gibt, wird der letzte `Configure`-Aufruf verwendet.

[!code-csharp[](startup/sample_snapshot/Program1.cs?highlight=18,22)]

## <a name="extend-startup-with-startup-filters"></a>Erweitern Sie den Start mit Startfiltern

Verwenden Sie <xref:Microsoft.AspNetCore.Hosting.IStartupFilter>, um Middleware am Anfang und am Ende der [Configure](#the-configure-method)-Middlewarepipeline einer App zu konfigurieren. `IStartupFilter` ist nützlich, wenn Sie sicherstellen wollen, dass eine Middleware vor oder nach einer Middleware ausgeführt wird, die von Bibliotheken am Anfang oder am Ende der App-Pipeline hinzufügt wurden, die Anforderungen verarbeitet.

`IStartupFilter` implementiert eine <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*>-Methode, die ein `Action<IApplicationBuilder>`-Objekt empfängt und zurückgibt. Eine <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>-Schnittstelle definiert Klassen, um die Anforderungspipeline einer App zu konfigurieren. Weitere Informationen finden Sie unter [Erstellen einer Middlewarepipeline mit IApplicationBuilder](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder).

Jede `IStartupFilter`-Schnittstelle implementiert mindestens eine Middleware in die Anforderungspipeline. Die Filter werden in der Reihenfolge aufgerufen, in der sie zum Dienstcontainer hinzugefügt wurden. Über Filter kann Middleware hinzugefügt werden, bevor oder nachdem dem nächsten Filter die Kontrolle erteilt wird. D.h., sie wird am Anfang oder am Ende einer App-Pipeline hinzugefügt.

Im folgenden Beispiel wird veranschaulicht, wie Middleware bei `IStartupFilter` registriert wird.

Die `RequestSetOptionsMiddleware`-Middleware legt einen Optionswert über einen Parameter der Abfragezeichenfolge fest:

[!code-csharp[](startup/sample_snapshot/RequestSetOptionsMiddleware.cs?name=snippet1&highlight=21)]

Die `RequestSetOptionsMiddleware`-Klasse wird in der `RequestSetOptionsStartupFilter`-Klasse konfiguriert:

[!code-csharp[](startup/sample_snapshot/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

Das `IStartupFilter`-Objekt wird im Dienstcontainer in <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> registriert und passt `Startup` von außerhalb der `Startup`-Klasse an:

[!code-csharp[](startup/sample_snapshot/Program2.cs?name=snippet1&highlight=4-5)]

Wenn für `option` ein Parameter der Abfragezeichenfolge bereitgestellt wird, verarbeitet die Middleware die Wertzuweisung, bevor die MVC-Middleware die Antwort rendert:

![Browserfenster, in dem die gerenderte Indexseite geöffnet ist Der Wert von „Option“ wird als „From Middleware“ (Von der Middleware) gerendert. Dieser Vorgang ist von der Abfrage der Seite mit dem Parameter der Abfragezeichenfolge und dem Wert der Option abhängig, die auf „From Middleware“ festgelegt ist.](startup/_static/index.png)

Die Reihenfolge der Ausführung der Middleware ist von der Reihenfolge der `IStartupFilter`-Registrierungen abhängig:

* Es kann sein, dass mehrere Implementierungen von `IStartupFilter` mit denselben Objekten interagieren. Wenn die Reihenfolge für Sie wichtig ist, sollten Sie die `IStartupFilter`-Dienstregistrierungen der Implementierungen in der Reihenfolge anordnen, in der die Middleware ausgeführt werden soll.
* Bibliotheken fügen möglicherweise Middleware mit mindestens einer `IStartupFilter`-Implementierung hinzu, die vor oder nach anderer App-Middleware ausgeführt wird, die über `IStartupFilter` registriert wurde. Wenn Sie eine `IStartupFilter`-Middleware vor einer Middleware aufrufen möchten, die über die `IStartupFilter` einer Bibliothek hinzugefügt wurde, positionieren Sie die Dienstregistrierung, bevor die Bibliothek zum Dienstcontainer hinzugefügt wird. Wenn Sie diese danach aufrufen möchten, positionieren Sie die Dienstregistrierung, nachdem die Bibliothek hinzugefügt wurde.

## <a name="add-configuration-at-startup-from-an-external-assembly"></a>Hinzufügen von Konfigurationen aus einer externen Assembly beim Start

Eine <xref:Microsoft.AspNetCore.Hosting.IHostingStartup>-Implementierung ermöglicht das Hinzufügen von Erweiterungen zu einer App beim Start von einer externen Assembly außerhalb der `Startup`-Klasse der App aus. Weitere Informationen finden Sie unter <xref:fundamentals/configuration/platform-specific-configuration>.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Der Host](xref:fundamentals/index#host)
* <xref:fundamentals/environments>
* <xref:fundamentals/middleware/index>
* <xref:fundamentals/logging/index>
* <xref:fundamentals/configuration/index>
