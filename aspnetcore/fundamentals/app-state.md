---
title: Sitzungs- und App-Zustand in ASP.NET Core
author: rick-anderson
description: Ansätze zum Erhalten des Sitzungs- und App-Zustands zwischen Sitzungen.
ms.author: riande
ms.custom: mvc
ms.date: 06/14/2018
uid: fundamentals/app-state
ms.openlocfilehash: a510e4f49e158203dd7c5e1e0bd28472541f7925
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024977"
---
# <a name="session-and-app-state-in-aspnet-core"></a>Sitzungs- und App-Zustand in ASP.NET Core

Von [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), [Diana LaRose](https://github.com/DianaLaRose) und [Luke Latham](https://github.com/guardrex)

Bei HTTP handelt es sich um ein zustandsloses Protokoll. HTTP-Anforderungen sind ohne zusätzliche Schritte unabhängige Nachrichten, die keine Benutzerwerte oder App-Zustände beibehalten. In diesem Artikel werden mehrere Ansätze zum Beibehalten von Benutzerdaten und App-Zuständen zwischen Anforderungen beschrieben.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

## <a name="state-management"></a>Zustandsverwaltung

Zustände können mithilfe mehrerer Ansätze gespeichert werden. Die Ansätze werden im Verlauf dieses Artikels beschrieben.

| Speicheransatz | Speichermechanismus |
| ---------------- | ----------------- |
| [Cookies](#cookies) | HTTP-Cookies (schließt möglicherweise Daten ein, die mit serverseitigem App-Code gespeichert wurden) |
| [Sitzungszustand](#session-state) | HTTP-Cookies und serverseitiger App-Code |
| [TempData](#tempdata) | HTTP-Cookies oder Sitzungszustand |
| [Abfragezeichenfolgen](#query-strings) | HTTP-Abfragezeichenfolgen |
| [Verborgene Felder](#hidden-fields) | HTTP-Formularfelder |
| [HttpContext.Items](#httpcontextitems) | Serverseitiger App-Code |
| [Cache](#cache) | Serverseitiger App-Code |
| [Abhängigkeitsinjektion](#dependency-injection) | Serverseitiger App-Code |

## <a name="cookies"></a>Cookies

Cookies speichern Daten anforderungsübergreifend. Da mit jeder Anforderung Cookies gesendet werden, sollte deren Größe auf ein Minimum begrenzt sein. Idealerweise sollte nur ein Bezeichner in einem Cookie gespeichert werden, während die Daten von der App gespeichert werden sollten. Die meisten Browser beschränken die Größe von Cookies auf 4096 Byte. Nur eine begrenzte Anzahl von Cookies ist für jede Domäne verfügbar.

Da Cookies manipuliert werden können, müssen sie von der App überprüft werden. Cookies können von Benutzern gelöscht werden und können auf Clients ablaufen. Cookies sind für gewöhnlich die dauerhafteste Form der Datenpersistenz auf dem Client.

Cookies werden häufig aus Personalisierungsgründen verwendet, wenn Inhalt für einen bekannten Benutzer angepasst wird. In den meisten Fällen wird der Benutzer nur identifiziert und nicht authentifiziert. Das Cookie kann den Benutzernamen, Kontonamen oder eine eindeutige Benutzer-ID (z.B. die GUID) speichern. Dann können Sie mit dem Cookie auf die persönlichen Einstellungen (z.B. die bevorzugte Farbe des Websitehintergrunds) des Benutzers zugreifen.

Beachten Sie die [Europäische Datenschutz-Grundverordnung (DSGVO)](https://ec.europa.eu/info/law/law-topic/data-protection) beim Ausstellen von Cookies und beim Umgang mit Aspekten des Datenschutzes. Weitere In finden Sie unter [General Data Protection Regulation (GDPR) support in ASP.NET Core (DSGVO-Unterstützung in ASP.NET Core)](xref:security/gdpr).

## <a name="session-state"></a>Sitzungszustand

Der Sitzungszustand ist ein Szenario in ASP.NET Core zum Speichern von Benutzerdaten, wenn der Benutzer eine Web-App verwendet. Der Sitzungszustand verwendet einen von der App verwalteten Speicher, um Daten für mehrere Anforderungen eines Clients beizubehalten. Die Sitzungsdaten werden in einem Cache zwischengespeichert und sind kurzlebig. Die Website sollte auch ohne die Sitzungsdaten weiterhin funktionieren. Kritische Anwendungsdaten sollten in der Benutzerdatenbank gespeichert und nur zur Leistungsoptimierung in der Sitzung zwischengespeichert werden.

> [!NOTE]
> Sitzungen werden in [SignalR](xref:signalr/index)-Apps nicht unterstützt, weil ein [SignalR-Hub](xref:signalr/hubs) unabhängig vom HTTP-Kontext ausgeführt werden kann. Das kann z.B. passieren, wenn eine lange Abrufanforderung von einem Hub länger als die Lebensdauer des HTTP-Kontexts einer Anforderung offen gehalten wird.

ASP.NET Core verwaltet den Sitzungszustand, indem ein Cookie an den Client übergeben wird, das die Sitzungs-ID enthält, die mit jeder Anforderung an den Server gesendet wird. Die App verwendet die Sitzungs-ID, um die Sitzungsdaten abzurufen.

Der Sitzungszustand verhält sich wie folgt:

* Da das Sitzungscookie browserspezifisch ist, können Sitzungen nicht für mehrere Browser gleichzeitig verwendet werden.
* Sitzungscookies werden gelöscht, wenn die Browsersitzung abläuft.
* Wenn für eine abgelaufene Sitzung ein Cookie empfangen wird, wird eine neue Sitzung erstellt, die dasselbe Cookie verwendet.
* Leere Sitzungen werden nicht beibehalten. Die Sitzung muss mindestens einen Wert enthalten, damit die Sitzung anforderungsübergreifend beibehalten wird. Wenn eine Sitzung nicht beibehalten wird, wird eine neue Sitzungs-ID für jede neue Anforderung erzeugt.
* Die App speichert Sitzungen für einen beschränkten Zeitraum nach der letzten Anforderung. Die App legt entweder ein Zeitlimit für die Sitzungen fest oder verwendet den Standardwert von 20 Minuten. Der Sitzungszustand eignet sich ideal zum Speichern von Benutzerdaten, die für eine bestimmte Sitzung zwar wichtig sind, die jedoch nicht dauerhaft sitzungsübergreifend gespeichert werden müssen.
* Sitzungsdaten werden entweder gelöscht, wenn die [ISession.Clear](/dotnet/api/microsoft.aspnetcore.http.isession.clear)-Implementierung aufgerufen wird oder wenn die Sitzung abläuft.
* Es gibt kein Standardverfahren, wie App-Code darüber informiert wird, dass ein Clientbrowser geschlossen wurde oder dass ein Sitzungscookie gelöscht wurde oder auf dem Client abgelaufen ist.
Die Vorlagen für ASP.NET Core MVC- und Razor-Seiten bieten Unterstützung für die [Unterstützung für die Datenschutz-Grundverordnung (DSGVO)](xref:security/gdpr). [Sitzungszustandscookies sind nicht unbedingt erforderlich](xref:security/gdpr#tempdata-provider-and-session-state-cookies-are-not-essential), denn der Sitzungszustand ist nicht funktionsfähig, wenn die Nachverfolgung deaktiviert ist.

> [!WARNING]
> Speichern Sie keine vertraulichen Daten im Sitzungszustand. Es besteht die Möglichkeit, dass der Benutzer seinen Browser nicht schließt oder die Sitzungscookies nicht löscht. Einige Browser behalten gültige Sitzungscookies browserfensterübergreifend bei. Eine Sitzung ist möglicherweise nicht nur auf einen Benutzer beschränkt, sodass der nächste Benutzer dasselbe Sitzungscookie verwendet.

Der Cacheanbieter im Arbeitsspeicher speichert Sitzungsdaten im Arbeitsspeicher des Servers, auf dem sich die App befindet. Beachten Sie in einem Szenario mit einer Serverfarm Folgendes:

* Verwenden Sie *Sticky Sessions* (anhaftende Sitzungen), um jede Sitzung an eine spezifische App-Instanz auf einem separaten Server zu binden. [Azure App Service](https://azure.microsoft.com/services/app-service/) verwendet [Routing von Anwendungsanforderungen (ARR)](/iis/extensions/planning-for-arr/using-the-application-request-routing-module), um Sticky Sessions standardmäßig zu erzwingen. Diese Sitzungen können allerdings Auswirkungen auf die Skalierbarkeit haben und Updates für Web-Apps erschweren. Ein geeigneteres Vorgehen ist das Verwenden von Redis oder über SQL Server verteilte Caches, für die keine Sticky Sessions notwendig sind. Weitere Informationen finden Sie unter <xref:performance/caching/distributed>.
* Das Sitzungscookie wird über [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) verschlüsselt. Der Datenschutz muss ordnungsgemäß konfiguriert sein, sodass er Sitzungscookies auf jedem Computer liest. Weitere Informationen finden Sie unter <xref:security/data-protection/introduction> und [Schlüsselspeicheranbieter](xref:security/data-protection/implementation/key-storage-providers).

### <a name="configure-session-state"></a>Konfigurieren des Sitzungszustands

::: moniker range=">= aspnetcore-2.0"

Das Paket [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/), das im [Metapaket Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) enthalten ist, bietet Middleware zum Verwalten des Sitzungszustands. `Startup` muss folgende Elemente enthalten, um die Sitzungsmiddleware zu aktivieren:

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Das Paket [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) stellt Middleware zum Verwalten des Sitzungszustands zur Verfügung. `Startup` muss folgende Elemente enthalten, um die Sitzungsmiddleware zu aktivieren:

::: moniker-end

* Einen der [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache)-Arbeitsspeichercaches Die `IDistributedCache`-Implementierung wird als Sicherungsspeicher für Sitzungen verwendet. Weitere Informationen finden Sie unter <xref:performance/caching/distributed>.
* Einen Aufruf von [AddSession](/dotnet/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions.addsession) in `ConfigureServices`.
* Einen Aufruf von [UseSession](/dotnet/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) in `Configure`.

Der folgende Code zeigt, wie Sie den speicherinternen Sitzungsanbieter mit einer Standardimplementierung von `IDistributedCache` im Arbeitsspeicher einrichten:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Startup.cs?name=snippet1&highlight=11,13-18,39)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Startup.cs?name=snippet1&highlight=5,7-12,19)]

::: moniker-end

Die Reihenfolge der Middleware ist wichtig. Im vorherigen Beispiel kommt es zu einer `InvalidOperationException`-Ausnahme, wenn `UseSession` nach `UseMvc` aufgerufen wird. Weitere Informationen finden Sie unter [Middleware](xref:fundamentals/middleware/index#order).

[HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session) ist verfügbar, nachdem der Sitzungszustand konfiguriert wurde.

Auf `HttpContext.Session` kann vor einem Aufruf von `UseSession` nicht zugegriffen werden.

Nachdem die App mit dem Schreiben in den Antwortdatenstrom begonnen hat, kann keine neue Sitzung mit einem neuen Sitzungscookie erstellt werden. Die Ausnahme wird im Webserverprotokoll erfasst und nicht im Browser angezeigt.

### <a name="load-session-state-asynchronously"></a>Asynchrones Laden des Sitzungszustands

Der Standardsitzungsanbieter in ASP.NET Core lädt Sitzungsaufzeichnungen aus dem zugrunde liegenden [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache)-Sicherungsspeicher nur asynchron, wenn die [ISession.LoadAsync](/dotnet/api/microsoft.aspnetcore.http.isession.loadasync)-Methode explizit vor den Methoden [TryGetValue](/dotnet/api/microsoft.aspnetcore.http.isession.trygetvalue), [Set](/dotnet/api/microsoft.aspnetcore.http.isession.set) oder [Remove](/dotnet/api/microsoft.aspnetcore.http.isession.remove) aufgerufen wird. Wenn `LoadAsync` nicht zuerst aufgerufen wird, werden die zugrunde liegenden Sitzungsaufzeichnungen synchron geladen, was entsprechende Auswirkungen auf die Leistung haben kann.

Damit Apps dieses Muster erzwingen, umschließen Sie die Implementierungen [DistributedSessionStore](/dotnet/api/microsoft.aspnetcore.session.distributedsessionstore) und [DistributedSession](/dotnet/api/microsoft.aspnetcore.session.distributedsession) mit Versionen, die eine Ausnahme auslösen, wenn die `LoadAsync`-Methode nicht vor `TryGetValue`, `Set` oder `Remove` aufgerufen wird. Registrieren Sie die umschlossenen Versionen in den Dienstcontainern.

### <a name="session-options"></a>Sitzungsoptionen

Verwenden Sie [Sitzungsoptionen](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions), um Standardwerte für Sitzungen zu überschreiben.

::: moniker range=">= aspnetcore-2.0"

| Option | Beschreibung |
| ------ | ----------- |
| [Cookie](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookie) | Bestimmt die Einstellungen, die zum Erstellen des Cookies verwendet wurden. Der Standardwert von [Name](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name) ist [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename) (`.AspNetCore.Session`). Der Standardwert von [Path](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path) ist [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath) (`/`). Der Standardwert von [SameSite](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite) ist [SameSiteMode.Lax](/dotnet/api/microsoft.aspnetcore.http.samesitemode) (`1`). Der Standardwert von [HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) ist `true`. Der Standardwert von [IsEssential](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.isessential) ist `false`. |
| [IdleTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) | `IdleTimeout` gibt an, wie lang die Sitzung sich im Leerlauf befinden darf, bevor die Inhalte verworfen werden. Jeder Zugriff auf eine Sitzung setzt das Zeitlimit zurück. Diese Einstellung gilt nur für den Inhalt der Sitzung und nicht für den Cookie. Der Standardwert beträgt 20 Minuten. |
| [IOTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.iotimeout) | Das Zeitlimit, wie lange eine Sitzung aus dem Speicher geladen werden soll oder wie lange sie in den Speicher committet werden soll. Diese Einstellung gilt möglicherweise nur für asynchrone Vorgänge. Dieses Zeitlimit kann mit [InfiniteTimeSpan](/dotnet/api/system.threading.timeout.infinitetimespan) deaktiviert werden. Der Standardwert beträgt 1&amp;#160;Minute. |

Die Sitzung verwendet ein Cookie, um Anforderungen eines Browsers nachzuverfolgen und zu identifizieren. Standardmäßig wird das Cookie `.AspNetCore.Session` genannt und verwendet den Pfad von `/`. Da das Standardcookie keine Domäne festlegt, wird es dem clientseitigen Skript auf der Seite nicht zur Verfügung gestellt, da der Standardwert von [HttpOnly](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly) `true` ist.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| Option | Beschreibung |
| ------ | ----------- |
| [CookieDomain](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiedomain) | Bestimmt die Domäne, mit der ein Cookie erstellt wurde. `CookieDomain` ist standardmäßig nicht festgelegt. |
| [CookieHttpOnly](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiehttponly) | Bestimmt, ob der Browser zulässt, dass auf das Cookie über clientseitiges JavaScript zugegriffen wird. Der Standardwert ist `true`. D.h., dass das Cookie nur an HTTP-Anforderungen übergeben und nicht für Skript auf der Seite verfügbar gemacht wird. |
| [CookieName](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiename) | Bestimmt den Cookienamen, der zum Beibehalten der Sitzungs-ID verwendet wird. Der Standardwert ist [SessionDefaults.CookieName](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiename) (`.AspNetCore.Session`). |
| [CookiePath](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiepath) | Bestimmt den Pfad, mit dem ein Cookie erstellt wurde. Der Standardwert ist [SessionDefaults.CookiePath](/dotnet/api/microsoft.aspnetcore.session.sessiondefaults.cookiepath) (`/`). |
| [CookieSecure](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.cookiesecure) | Bestimmt, ob das Cookie nur bei HTTPS-Anforderungen übertragen werden soll. Der Standardwert ist [CookieSecurePolicy.None](/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy) (`2`). |
| [IdleTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout) | `IdleTimeout` gibt an, wie lang die Sitzung sich im Leerlauf befinden darf, bevor die Inhalte verworfen werden. Jeder Zugriff auf eine Sitzung setzt das Zeitlimit zurück. Beachten Sie, dass dies nur für den Inhalt der Sitzung und nicht den Cookie gilt. Der Standardwert beträgt 20 Minuten. |

Die Sitzung verwendet ein Cookie, um Anforderungen eines Browsers nachzuverfolgen und zu identifizieren. Standardmäßig wird das Cookie `.AspNet.Session` genannt und verwendet den Pfad von `/`.

::: moniker-end

Verwenden Sie `SessionOptions`, um Standardwerte für Sitzungscookies zu überschreiben:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples_snapshot/2.x/SessionSample/Startup.cs?name=snippet1&highlight=13-18)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples_snapshot/1.x/SessionSample/Startup.cs?name=snippet1&highlight=5-9)]

::: moniker-end

Die App verwendet die [IdleTimeout](/dotnet/api/microsoft.aspnetcore.builder.sessionoptions.idletimeout)-Eigenschaft, um zu bestimmen, wie lange sich die Sitzung im Leerlauf befinden kann, bevor ihre Inhalte im Cache des Servers verworfen werden. Diese Eigenschaft ist unabhängig vom Ablauf der Cookies. Jede Anforderung, die über die [Sitzungsmiddleware](/dotnet/api/microsoft.aspnetcore.session.sessionmiddleware) übergeben wird, setzt das Zeitlimit zurück.

Der Sitzungszustand ist *nicht sperrend*. Die letzte Anforderung überschreibt die erste, wenn zwei Anforderungen gleichzeitig versuchen, die Inhalte einer Sitzung zu bearbeiten. `Session` wird als *kohärente Sitzung* implementiert, d.h., dass alle Inhalte zusammen gespeichert werden. Wenn zwei Anforderungen unterschiedliche Sitzungswerte bearbeiten möchten, überschreibt die letzte Anforderung möglicherweise Anforderungen der ersten.

### <a name="set-and-get-session-values"></a>Festlegen und Abrufen von Sitzungswerten

Sie können über die Razor Pages-Klasse [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) oder die MVC-Klasse [Controller](/dotnet/api/microsoft.aspnetcore.mvc.controller) mit [HttpContext.Session](/dotnet/api/microsoft.aspnetcore.http.httpcontext.session) auf den Sitzungszustand zugreifen. Bei der Eigenschaft handelt es sich um eine [ISession](/dotnet/api/microsoft.aspnetcore.http.isession)-Implementierung.

::: moniker range=">= aspnetcore-2.0"

Die `ISession`-Implementierung bietet mehrere Erweiterungsmethoden zum Festlegen und Abrufen von Integerwerten und Zeichenfolgenwerten. Die Erweiterungsmethoden befinden sich im Namespace [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http), wenn vom Projekt auf das Paket `using Microsoft.AspNetCore.Http;`Microsoft.AspNetCore.Http.Extensions[ verwiesen wird (fügen Sie eine ](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/)-Anweisung hinzu, um Zugriff auf die Erweiterungsmethoden zu erhalten). Beide Pakete sind im Metapaket [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) enthalten.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Die `ISession`-Implementierung bietet mehrere Erweiterungsmethoden zum Festlegen und Abrufen von ganzzahligen und Zeichenfolgenwerten. Die Erweiterungsmethoden befinden sich im Namespace [Microsoft.AspNetCore.Http](/dotnet/api/microsoft.aspnetcore.http), wenn vom Projekt auf das Paket `using Microsoft.AspNetCore.Http;`Microsoft.AspNetCore.Http.Extensions[ verwiesen wird (fügen Sie eine ](https://www.nuget.org/packages/Microsoft.AspNetCore.Http.Extensions/)-Anweisung hinzu, um Zugriff auf die Erweiterungsmethoden zu erhalten).

::: moniker-end

`ISession`-Erweiterungsmethoden:

* [Get(ISession, String)](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.get)
* [GetInt32(ISession, String)](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.getint32)
* [GetString(ISession, String)](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.getstring)
* [SetInt32(ISession, String, Int32)](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.setint32)
* [SetString(ISession, String, String)](/dotnet/api/microsoft.aspnetcore.http.sessionextensions.setstring)

Mit dem folgenden Codebeispiel wird der Sitzungswert für den `IndexModel.SessionKeyName`-Schlüssel (`_Name` in der Beispiel-App) auf einer Razor Pages-Seite abgerufen:

```csharp
@page
@using Microsoft.AspNetCore.Http
@model IndexModel

...

Name: @HttpContext.Session.GetString(IndexModel.SessionKeyName)
```

Im folgenden Codebeispiel wird veranschaulicht, wie Sie eine ganze Zahl und eine Zeichenfolge abrufen und festlegen können:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet1&highlight=18-19,22-23)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet1&highlight=10-11,18-19)]

::: moniker-end

Alle Sitzungsdaten müssen serialisiert werden, um ein Szenario mit einem verteilten Cache zu ermöglichen, auch wenn Sie den speicherinternen Cache verwenden. Die mindestens erforderlichen Zeichenfolgen- und Zahlenserialisierungsmodule werden bereitgestellt (siehe Methoden und Erweiterungsmethoden von [ISession](/dotnet/api/microsoft.aspnetcore.http.isession)). Komplexe Typen müssen vom Benutzer mit einem anderen Verfahren wie etwa JSON serialisiert werden.

Fügen Sie die folgenden Erweiterungsmethoden hinzu, um serialisierbare Objekte für eine Sitzung festzulegen und abzurufen:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Extensions/SessionExtensions.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Extensions/SessionExtensions.cs?name=snippet1)]

::: moniker-end

Im folgenden Beispiel wird dargestellt, wie Sie serialisierbare Objekte mit den Erweiterungsmethoden festlegen und abrufen:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet2)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet2&highlight=4,12)]

::: moniker-end

## <a name="tempdata"></a>TempData

ASP.NET Core macht [die TempData-Eigenschaft des Razor Pages-Seitenmodells](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.tempdata) oder [TempData eines MVC-Controllers](/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata) verfügbar. Diese Eigenschaft speichert Daten, bis sie gelesen wurden. Die Methoden [Keep](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.keep) und [Peek](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.itempdatadictionary.peek) können verwendet werden, um die Daten zu überprüfen, ohne sie zu löschen. TempData eignet sich besonders für die Weiterleitung, wenn Daten für mehr als eine Anforderung erforderlich sind. TempData wird von TempData-Anbietern implementiert, indem Cookies oder der Sitzungszustand verwendet werden.

### <a name="tempdata-providers"></a>TempData-Anbieter

::: moniker range=">= aspnetcore-2.0"

In ASP.NET Core 2.0 und höher wird der cookiebasierte TempData-Anbieter standardmäßig verwendet, um TempData in Cookies zu speichern.

Die Cookiedaten werden mit [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) verschlüsselt, mit [Base64UrlTextEncoder](/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder) codiert und anschließend in Blöcke unterteilt. Da das Cookie in Blöcke unterteilt wird, gilt die in ASP.NET Core 1.x gefundene Größenbeschränkung nicht für einzelne Cookies. Die Cookiedaten werden nicht komprimiert, da es zu Sicherheitsproblemen kommen kann, wenn Daten verschlüsselt werden, z.B. durch [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit))- und [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit))-Angriffe. Weitere Informationen zum cookiebasierten TempData-Anbieter finden Sie unter [CookieTempDataProvider](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.cookietempdataprovider).

::: moniker-end

::: moniker range="< aspnetcore-2.0"

In ASP.NET Core 1.0 und 1.1 wird der TempData-Anbieter für den Sitzungszustand als Standardanbieter verwendet.

::: moniker-end

### <a name="choose-a-tempdata-provider"></a>Auswählen eines TempData-Anbieters

Bevor Sie einen TempData-Anbieter auswählen, müssen Sie folgende Überlegungen anstellen:

1. Verwendet die App bereits den Sitzungszustand? Falls dies der Fall ist, hat die Verwendung des TempData-Anbieters abgesehen von der Größe der Daten keine zusätzlichen Auswirkungen auf die App.
2. Verwendet die App TempData nur selten für verhältnismäßig kleine Datenmengen (bis zu 500 Bytes)? Falls dies der Fall ist, entsteht durch das Cookie des TempData-Anbieters nur ein kleiner zusätzlicher Aufwand für jede Anforderung, die TempData enthält. Falls dies nicht der Fall ist, kann der Sitzungszustand des TempData-Anbieters nützlich sein, um Roundtrips für große Datenmengen für jede Anforderung durchzuführen, bis TempData verarbeitet wird.
3. Wird die App in einer Serverfarm auf mehreren Servern ausgeführt? Wenn dies der Fall ist, ist keine weitere Konfiguration erforderlich, um das Cookie des TempData-Anbieters außerhalb des Schutzes von Daten zu verwenden (siehe <xref:security/data-protection/introduction> und [Schlüsselspeicheranbieter](xref:security/data-protection/implementation/key-storage-providers)).

> [!NOTE]
> Die meisten Webclients (z.B. Webbrowser) erzwingen Einschränkungen für die maximale Größe der Cookies, für die Gesamtanzahl der Cookies oder für beides. Wenn Sie das Cookie des TempData-Anbieters verwenden, sollten Sie überprüfen, ob die App diese Einschränkungen überschreitet. Beachten Sie die Gesamtgröße der Daten. Rechnen Sie mit erhöhter Cookiegröße aufgrund von Verschlüsselung und Segmentierung.

### <a name="configure-the-tempdata-provider"></a>Konfigurieren des TempData-Anbieters

::: moniker range=">= aspnetcore-2.0"

Der cookiebasierte TempData-Anbieter ist standardmäßig aktiviert.

Verwenden Sie die Erweiterungsmethode [AddSessionStateTempDataProvider](/dotnet/api/microsoft.extensions.dependencyinjection.mvcviewfeaturesmvcbuilderextensions.addsessionstatetempdataprovider), um sitzungsbasierte TempData-Anbieter zu ermöglichen:

[!code-csharp[](app-state/samples_snapshot_2/2.x/SessionSample/Startup.cs?name=snippet1&highlight=11,13,32)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

Der folgende `Startup`-Klassencode konfiguriert den sitzungsbasierten TempData-Anbieter:

[!code-csharp[](app-state/samples_snapshot_2/1.x/SessionSample/Startup.cs?name=snippet1&highlight=4,9)]

::: moniker-end

Die Reihenfolge der Middleware ist wichtig. Im vorherigen Beispiel kommt es zu einer `InvalidOperationException`-Ausnahme, wenn `UseSession` nach `UseMvc` aufgerufen wird. Weitere Informationen finden Sie unter [Middleware](xref:fundamentals/middleware/index#order).

> [!IMPORTANT]
> Wenn Sie für .NET Framework entwickeln und den sitzungsbasierten TempData-Anbieter verwenden, fügen Sie das Paket [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session/) zu Ihrem Projekt hinzu.

## <a name="query-strings"></a>Abfragezeichenfolgen

Eine begrenzte Menge an Daten kann von einer Anforderung an eine andere übergeben werden, indem Sie diese zu der Abfragezeichenfolge einer neuen Anforderung hinzufügen. Dies ist nützlich, um den Zustand dauerhaft zu erfassen und Links mit einem eingebetteten Zustand zuzulassen, die über E-Mail oder soziale Netzwerke geteilt werden sollen. Verwenden Sie keine Abfragezeichenfolgen für vertrauliche Daten, da URL-Abfragezeichenfolgen öffentlich sind.

Wenn Daten in Abfragezeichenfolgen eingefügt werden, können sie nicht nur versehentlich freigegeben werden, sondern es entstehen auch Gelegenheiten für Versuche einer [websiteübergreifenden Anforderungsfälschung](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)), wodurch Benutzer dazu gebracht werden können, auf bösartige Websites zuzugreifen, während sie authentifiziert sind. Angreifer können dann Benutzerdaten von der App stehlen oder schädliche Aktionen im Namen eines Benutzers durchführen. Jeder gespeicherte App- oder Sitzungszustand muss vor solchen Anforderungsfälschungen geschützt sein. Weitere Informationen finden Sie unter [Preventing Cross-Site Request Forgery (XSRF/CSRF) attacks (Verhindern von websiteübergreifenden Anforderungsfälschungen (XSRF/CSRF))](xref:security/anti-request-forgery).

## <a name="hidden-fields"></a>Verborgene Felder

Daten können in ausgeblendeten Formularfeldern gespeichert und an die nächste Anforderung zurückgesendet werden. Dies ist häufig in mehrseitigen Formularen der Fall. Die App muss die in verborgenen Feldern gespeicherten Daten immer wieder überprüfen, da der Client die Daten manipulieren könnte.

## <a name="httpcontextitems"></a>HttpContext.Items

Die Auflistung [HttpContext.Items](/dotnet/api/microsoft.aspnetcore.http.httpcontext.items) wird verwendet, um Daten zu speichern, während eine einzelne Anforderung behandelt wird. Die Inhalte der Auflistung werden nach der Verarbeitung jeder Anforderung verworfen. Die `Items`-Auflistung wird häufig von Komponenten oder Middleware zur Kommunikation verwendet, wenn sie zu unterschiedlichen Zeitpunkten während einer Anforderung ausgeführt werden und es keinen direkten Weg gibt, Parameter zu übergeben.

Im folgenden Beispiel fügt [Middleware](xref:fundamentals/middleware/index) `isVerified` zur Auflistung `Items` hinzu.

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

An einem späteren Punkt in der Pipeline kann eine andere Middleware den Wert von `isVerified` zugreifen:

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync($"Verified: {context.Items["isVerified"]}");
});
```

Für Middleware, die nur von einer App verwendet wird, werden `string`-Schlüssel akzeptiert. Middleware, die von mehreren App-Instanzen verwendet wird, sollte eindeutige Objektschlüssel verwenden, um Schlüsselkonflikte zu vermeiden. Das folgenden Beispiel zeigt, wie Sie einen eindeutigen Objektschlüssel verwenden, der in einer Middlewareklasse definiert wurde:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Middleware/HttpContextItemsMiddleware.cs?name=snippet1&highlight=4,13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Middleware/HttpContextItemsMiddleware.cs?name=snippet1&highlight=5,14)]

::: moniker-end

Anderer Code kann auf den Wert zugreifen, der in `HttpContext.Items` gespeichert ist, indem er den Schlüssel verwendet, der von der Middlewareklasse zur Verfügung gestellt wird:

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-state/samples/2.x/SessionSample/Pages/Index.cshtml.cs?name=snippet3)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](app-state/samples/1.x/SessionSample/Controllers/HomeController.cs?name=snippet3)]

::: moniker-end

Dieser Ansatz hat außerdem den Vorteil, dass das Verwenden von Schlüsselzeichenfolgen im Code vermieden wird.

## <a name="cache"></a>cache

Das Caching stellt eine effiziente Möglichkeit zum Speichern und Abrufen von Daten dar. Die App kann die Lebensdauer zwischengespeicherter Elemente bestimmen.

Zwischengespeicherte Daten sind nicht mit einer spezifischen Anforderung, einem spezifischen Benutzer oder einer spezifischen Sitzung verknüpft. **Achten Sie darauf, dass Sie keine benutzerspezifischen Daten zwischenspeichern, die von den Anforderungen anderen Benutzer abgerufen werden können.**

Weitere Informationen finden Sie unter <xref:performance/caching/response>.

## <a name="dependency-injection"></a>Dependency Injection

Verwenden Sie [Dependency Injection](xref:fundamentals/dependency-injection), um Daten für Benutzer bereitzustellen:

1. Definieren Sie einen Dienst, der die Daten enthält. Definieren Sie z.B. die Klasse `MyAppData`:

    ```csharp
    public class MyAppData
    {
        // Declare properties and methods
    }
    ```

2. Fügen Sie die Dienstklasse zu `Startup.ConfigureServices` hinzu:

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddSingleton<MyAppData>();
    }
    ```

3. Verwenden Sie die Datendienstklasse:

    ::: moniker range=">= aspnetcore-2.0"

    ```csharp
    public class IndexModel : PageModel
    {
        public IndexModel(MyAppData myService)
        {
            // Do something with the service
            //    Examples: Read data, store in a field or property
        }
    }
    ```

    ::: moniker-end

    ::: moniker range="< aspnetcore-2.0"

    ```csharp
    public class HomeController : Controller
    {
        public HomeController(MyAppData myService)
        {
            // Do something with the service
            //    Examples: Read data, store in a field or property
        }
    }
    ```

    ::: moniker-end

## <a name="common-errors"></a>Häufige Fehler

* „Unable to resolve service for type 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' while attempting to activate 'Microsoft.AspNetCore.Session.DistributedSessionStore'. (Dienst kann nicht für den Typ „Microsoft.Extensions.Caching.Distributed.IDistributedCache“ aufgelöst werden, während versucht wird, auf „Microsoft.AspNetCore.Session.DistributedSessionStore“ zuzugreifen.)

  Dieser Fehler entsteht in der Regel, wenn nicht alle `IDistributedCache`-Implementierungen konfiguriert werden. Weitere Informationen finden Sie unter <xref:performance/caching/distributed> und <xref:performance/caching/memory>.

* Falls die Sitzungsmiddleware eine Sitzung nicht speichert (z.B. wenn der Sicherungsspeicher nicht verfügbar ist), protokolliert sie die Ausnahme, und die Anforderung wird ordnungsgemäß ausgeführt. Das führt zu unvorhersehbarem Verhalten.

  Nehmen wir an, dass ein Benutzer seinen Einkaufswagen in einer Sitzung speichert. Der Benutzer fügt ein Element zum Einkaufswagen hinzu, aber der Commit schlägt fehl. Die App wird nicht über den Fehler informiert und meldet dem Benutzer, dass das Element zum Einkaufswagen hinzugefügt wurde. Dies stimmt jedoch nicht.

  Es wird empfohlen, nach Fehlern zu suchen, indem Sie `await feature.Session.CommitAsync();` über App-Code aufrufen, wenn die App mit dem Schreiben in die Sitzung fertig ist. `CommitAsync` löst eine Ausnahme aus, wenn der Sicherungsspeicher nicht verfügbar ist. Wenn `CommitAsync` fehlschlägt, kann die App die Ausnahme verarbeiten. `LoadAsync` wird unter den gleichen Bedingungen ausgelöst, wenn der Sicherungsspeicher nicht verfügbar ist.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

<xref:host-and-deploy/web-farm>
