---
title: Factorybezogene Middlewareaktivierung in ASP.NET Core
author: guardrex
description: Informationen zur Verwendung von stark typisierter Middleware mit einer factorybezogenen Aktivierungsimplementierung von ASP.NET Core.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 08/14/2018
uid: fundamentals/middleware/extensibility
ms.openlocfilehash: 566a5c5f642a3f55e72a8e070c69d2bfddaee3a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052357"
---
# <a name="factory-based-middleware-activation-in-aspnet-core"></a>Factorybezogene Middlewareaktivierung in ASP.NET Core

Von [Luke Latham](https://github.com/guardrex)

Bei [IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)/[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) handelt es sich um einen Erweiterungspunkt für die [Middleware](xref:fundamentals/middleware/index)-Aktivierung.

Die Erweiterungsmethode `UseMiddleware` überprüft, ob der registrierte Typ einer Middleware `IMiddleware` implementiert. Falls dies der Fall ist, wird die im Container registrierte `IMiddlewareFactory`-Instanz im Container verwendet, um die `IMiddleware`-Implementierung aufzulösen, anstatt die konventionsbasierte Middlewareaktivierungslogik zu verwenden. Die Middleware wird als bereichsbezogener oder vorübergehender Dienst im Dienstcontainer der App registriert.

Vorteile:

* Aktivierung pro Anforderung (Injection von bereichsbezogenen Diensten)
* Starke Typisierung der Middleware

`IMiddleware` wird pro Anforderung aktiviert, sodass bereichsbezogene Dienste in den Konstruktor der Middleware eingefügt werden können.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility/sample) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

Die Beispiel-App stellt Middleware dar, die wie folgt aktiviert wurde:

* Per Konvention Weitere Informationen zur konventionellen Middlewareaktivierung finden Sie im Artikel [Middleware](xref:fundamentals/middleware/index).
* Durch die Implementierung von [IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) Die Standard-[MiddlewareFactory-Klasse](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory) aktiviert die Middleware.

Die Middlewareimplementierungen funktionieren auf identische Weise und erfassen den Wert, der von einem Abfragezeichenfolgenparameter (`key`) bereitgestellt wird. Die Middlewares verwenden einen eingefügten Datenbankkontext (einen bereichsbezogenen Dienst), um den Abfragezeichenwert in einer In-Memory Database zu erfassen.

## <a name="imiddleware"></a>IMiddleware

[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) definiert Middleware für die Anforderungspipeline der App. Die [InvokeAsync(HttpContext, RequestDelegate)](/dotnet/api/microsoft.aspnetcore.http.imiddleware.invokeasync#Microsoft_AspNetCore_Http_IMiddleware_InvokeAsync_Microsoft_AspNetCore_Http_HttpContext_Microsoft_AspNetCore_Http_RequestDelegate_)-Methode verarbeitet Anforderungen und gibt einen `Task` zurück, der für die Ausführung der Middleware steht.

Über Konventionen aktivierte Middleware:

[!code-csharp[](extensibility/sample/Middleware/ConventionalMiddleware.cs?name=snippet1)]

Über `MiddlewareFactory` aktivierte Middleware:

[!code-csharp[](extensibility/sample/Middleware/FactoryActivatedMiddleware.cs?name=snippet1)]

Für Middlewares werden Erweiterungen erstellt:

[!code-csharp[](extensibility/sample/Middleware/MiddlewareExtensions.cs?name=snippet1)]

Es ist nicht möglich, Objekte mit `UseMiddleware` an eine Middleware zu übergeben, die über eine Factory aktiviert wurde:

```csharp
public static IApplicationBuilder UseFactoryActivatedMiddleware(
    this IApplicationBuilder builder, bool option)
{
    // Passing 'option' as an argument throws a NotSupportedException at runtime.
    return builder.UseMiddleware<FactoryActivatedMiddleware>(option);
}
```

Die Middleware, die über eine Factory aktiviert wurde, wird dem integrierten Container in der *Startup.cs*-Datei hinzugefügt:

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet1&highlight=12)]

Beide Middlewares werden in der Anforderungsverarbeitungspipeline in `Configure` registriert:

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet2&highlight=14-15)]

## <a name="imiddlewarefactory"></a>IMiddlewareFactory

Die [IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)-Instanz stellt Methoden zur Verfügung, um Middleware zu erstellen. Die Implementierung der Middlewarefactory wird im Container als bereichsbezogener Dienst registriert.

Die Standardimplementierung von `IMiddlewareFactory`, [MiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory), befindet sich im Paket [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:fundamentals/middleware/index>
* <xref:fundamentals/middleware/extensibility-third-party-container>
