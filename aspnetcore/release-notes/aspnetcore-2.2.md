---
title: Neuerungen in ASP.NET Core 2.2
author: tdykstra
description: Informationen zu den neuen Features in ASP.NET Core 2.2.
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/18/2018
uid: aspnetcore-2.2
ms.openlocfilehash: 6dcdf71ec5271690718dd1fe750a9a74d498a0f8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045107"
---
# <a name="whats-new-in-aspnet-core-22"></a>Neuerungen in ASP.NET Core 2.2

In diesem Artikel werden die wichtigsten Änderungen in ASP.NET Core 2.2 hervorgehoben und Links zu relevanter Dokumentation bereitgestellt.

## <a name="open-api-analyzers--conventions"></a>Open API-Analysetools und -Konventionen

Open API (auch als Swagger bekannt) ist eine sprachunabhängige Spezifikation für das Beschreiben von REST-APIs. Das Open API-Ökosystem verfügt über Tools, mit dem sich Clientcode mithilfe der Spezifikation ermitteln, testen und erzeugen lässt. Unterstützung für das Generieren und Visualisieren von Open API-Dokumenten in ASP.NET Core MVC wird über in der Community entstandene Projekte wie [NSwag](https://github.com/RSuter/NSwag) und [Swashbuckle.AspNetCore](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) bereitgestellt. ASP.NET Core 2.2 bietet verbesserte Tools und Runtimefunktionen für die Erstellung von Open API-Dokumenten.

Weitere Informationen finden Sie in den folgenden Ressourcen:

* <xref:web-api/advanced/analyzers>
* <xref:web-api/advanced/conventions>
* [ASP.NET Core 2.2.0-preview1: Open API Analyzers & Conventions](https://blogs.msdn.microsoft.com/webdev/2018/08/23/asp-net-core-2-20-preview1-open-api-analyzers-conventions/)

## <a name="problem-details-support"></a>Unterstützung bei Problemdetails

In ASP.NET Core 2.1 wurde `ProblemDetails` eingeführt, basierend auf der [RFC 7807](https://tools.ietf.org/html/rfc7807)-Spezifikation für die Übertragung von Fehlerdetails mit einer HTTP-Antwort. In 2.2 ist `ProblemDetails` die Standardantwort für Clientfehlercodes in Controllern mit dem `ApiControllerAttribute`. Ein `IActionResult`, das einen Statuscode für Clientfehler (4xx) zurückgegeben hat, gibt jetzt einen `ProblemDetails`-Text zurück. Das Ergebnis enthält auch eine Korrelations-ID, die zum Korrelieren des Fehlers mithilfe von Anforderungsprotokollen verwendet werden kann. Bei Clientfehlern verwendet `ProducesResponseType` standardmäßig `ProblemDetails` als Antworttyp. Dies wird in der Open API- bzw. Swagger-Ausgabe dokumentiert, die mit NSwag oder Swashbuckle.AspNetCore generiert wird.

## <a name="endpoint-routing"></a>Endpunktrouting

ASP.NET Core 2.2 verwendet ein neues System für das *Endpunktrouting* zum verbesserten Verteilen von Anforderungen. Die Änderungen umfassen neue API-Elemente für das Generieren von Links sowie Transformatoren für Routenparameter.

Weitere Informationen finden Sie in den folgenden Ressourcen:

* [Endpunktrouting in 2.2](https://blogs.msdn.microsoft.com/webdev/2018/08/27/asp-net-core-2-2-0-preview1-endpoint-routing/)
* [Parameter Transformers](https://www.hanselman.com/blog/ASPNETCore22ParameterTransformersForCleanURLGenerationAndSlugsInRazorPagesOrMVC.aspx) (Transformatoren für Routenparameter, Abschnitt **Routing**)
* [Unterschiede im Vergleich zu früheren Routingversionen](xref:fundamentals/routing?view=aspnetcore-2.2#differences-from-earlier-versions-of-routing)

## <a name="health-checks"></a>Integritätsprüfungen

Ein neuer Dienst für Integritätsprüfungen vereinfacht die Verwendung von ASP.NET Core in Umgebungen, in denen Integritätsprüfungen erforderlich sind, wie z.B. Kubernetes. Integritätsprüfungen umfassen Middleware und einen Satz Bibliotheken, die eine Abstraktion und einen Dienst für `IHealthCheck` definieren.

Integritätsprüfungen werden von einem Containerorchestrator oder Lastenausgleichsmodul verwendet, um schnell zu ermitteln, ob ein System normal auf Anforderung reagiert. Ein Containerorchestrator kann auf eine fehlerhafte Integritätsprüfung reagieren, indem die Ausführung einer Bereitstellung angehalten oder ein Container neu gestartet wird. Ein Lastenausgleichsmodul kann auf eine Integritätsprüfung reagieren, indem Datenverkehr von der fehlerhaften Instanz des Diensts weggeleitet wird.

Integritätsprüfungen werden von einer Anwendung als HTTP-Endpunkt verfügbar gemacht, der von Überwachungssystemen verwendet wird. Integritätsprüfungen können für eine Vielzahl von Echtzeit-Überwachungsszenarien und -Überwachungssystemen konfiguriert werden. Der Integritätsprüfungsdienst lässt sich in das [BeatPulse-Projekt](https://github.com/Xabaril/BeatPulse) integrieren. Damit lassen sich Überprüfungen für Dutzende von beliebten Systemen und Abhängigkeiten einfacher hinzufügen.

Weitere Informationen finden Sie unter [Integritätsprüfungen in ASP.NET Core](xref:host-and-deploy/health-checks).

## <a name="http2-in-kestrel"></a>HTTP/2 in Kestrel

In ASP.NET Core 2.2 wurde Unterstützung für HTTP/2 hinzugefügt. 

HTTP/2 ist eine umfassende Überarbeitung des HTTP-Protokolls. Einige der wichtigsten Features von HTTP/2 sind die Unterstützung für die Headerkomprimierung und Streams mit vollständigem Multiplexing über eine einzige Verbindung. HTTP/2 behält zwar die HTTP-Semantik bei (HTTP-Header, Methoden usw.), ist aber im Vergleich zu HTTP/1.x ein Breaking Change in Bezug darauf, wie Daten in Frames aufgeteilt und über das Netzwerk gesendet werden.

Aufgrund dieser Änderung bei der Frameerstellung müssen Server und Clients die verwendete Protokollversion aushandeln. Application-Layer Protocol Negotiation (ALPN) ist eine TLS-Erweiterung, die es dem Server und dem Client ermöglicht, die verwendete Protokollversion im Rahmen des TLS-Handshakes auszuhandeln. Es ist zwar möglich, dass Server und Client das Protokoll vorher kennen, aber alle wichtigen Browser unterstützt ALPN als einzige Möglichkeit, eine HTTP/2-Verbindung herzustellen.

Weitere Informationen finden Sie unter [HTTP/2-Unterstützung](xref:fundamentals/servers/index?view=aspnetcore-2.2#http2-support).

## <a name="kestrel-configuration"></a>Kestrel-Konfiguration

In früheren Versionen von ASP.NET Core werden Kestrel-Optionen durch Aufrufen von `UseKestrel` konfiguriert. In 2.2 werden Kestrel-Optionen durch Aufrufen von `ConfigureKestrel` auf dem Hostgenerator konfiguriert. Diese Änderung löst ein Problem mit der Reihenfolge von `IServer`-Registrierungen für das In-Process-Hosting. Weitere Informationen finden Sie in den folgenden Ressourcen:

* [Mitigate UseIIS conflict](https://github.com/aspnet/KestrelHttpServer/issues/2760) (Entschärfen von UseIIS-Konflikten)
* [Konfigurieren von Kestrel-Serveroptionen mit ConfigureKestrel](xref:fundamentals/servers/kestrel?view=aspnetcore-2.2#how-to-use-kestrel-in-aspnet-core-apps)

## <a name="iis-in-process-hosting"></a>IIS-In-Process-Hosting

In früheren Versionen von ASP.NET Core dient IIS als Reverseproxy. In 2.2 kann das ASP.NET Core-Modul die CoreCLR starten und eine App im IIS-Workerprozess (*w3wp.exe*) hosten. Das In-Process-Hosting verbessert die Leistung und Diagnose beim Ausführen mit IIS.

Weitere Informationen finden Sie unter [In-Process-Hosting für IIS](xref:host-and-deploy/aspnet-core-module?view=aspnetcore-2.2#in-process-hosting-model).

## <a name="signalr-java-client"></a>Java-Client für SignalR

ASP.NET Core 2.2 führt einen Java-Client für SignalR ein. Dieser Client unterstützt die Verbindung mit einem ASP.NET Core-SignalR-Server über Java-Code, einschließlich Android-Apps.

Weitere Informationen finden Sie unter [ASP.NET Core-SignalR-Java-Client](https://docs.microsoft.com/aspnet/core/signalr/java-client?view=aspnetcore-2.2).

## <a name="cors-improvements"></a>Verbesserungen an CORS

In früheren Versionen von ASP.NET Core ermöglicht CORS-Middleware das Senden von `Accept`-, `Accept-Language`-, `Content-Language`- und `Origin`-Headern unabhängig von den in `CorsPolicy.Headers` konfigurierten Werten. In 2.2 ist ein Abgleich mit einer CORS-Middleware-Richtlinie nur möglich, wenn die in `Access-Control-Request-Headers` gesendeten Header exakt mit den in `WithHeaders` angegebenen Headern übereinstimmen.

Weitere Informationen finden Sie unter [CORS-Middleware](xref:security/cors?view=aspnetcore-2.2#set-the-allowed-request-headers).

## <a name="response-compression"></a>Antwortkomprimierung

ASP.NET Core 2.2 kann Antworten mit dem [Brotli-Komprimierungsformat](https://tools.ietf.org/html/rfc7932) komprimieren.

Weitere Informationen finden Sie unter [Middleware für die Antwortkomprimierung unterstützt die Brotli-Komprimierung](xref:performance/response-compression?view=aspnetcore-2.2#brotli-compression-provider).

## <a name="project-templates"></a>Projektvorlagen

ASP.NET Core-Webprojektvorlagen wurden auf [Bootstrap 4](https://getbootstrap.com/docs/4.1/migration/) und [Angular 6](https://blog.angular.io/version-6-of-angular-now-available-cc56b0efa7a4) aktualisiert. Der neue Look ist optisch vereinfacht, sodass Sie die wichtigen Strukturen einer App leichter erkennen können.

![Start- oder Indexseite](~/tutorials/razor-pages/razor-pages-start/_static/home2.2.png)

## <a name="validation-performance"></a>Leistung bei der Überprüfung

Das Überprüfungssystem von MVC ist erweiterbar und flexibel und ermöglicht es Ihnen, für jede Anforderung zu festzulegen, welche Validierungssteuerelemente für ein bestimmtes Modell gelten. Dies ist sehr nützlich für die Erstellung von komplexen Validierungsanbietern. In den meisten Fällen verwendet eine Anwendung jedoch nur die integrierten Validierungssteuerelemente und benötigt diese zusätzliche Flexibilität nicht. Integrierte Validierungssteuerelemente umfassen Datenanmerkungen wie [Required], [StringLength] und `IValidatableObject`.

In ASP.NET Core 2.2 kann MVC die Überprüfung kurzschließen, wenn festgestellt wird, dass ein bestimmter Modellgraph keine Überprüfung erfordert. Das Überspringen von Überprüfungsergebnissen bietet erhebliche Verbesserungen beim Überprüfen von Modellen, die keine Validierungssteuerelemente besitzen oder besitzen können. Hierzu gehören Objekte wie Sammlungen von primitiven (z.B. `byte[]`, `string[]` und `Dictionary<string, string>`) oder komplexen Objektgraphen mit einer geringen Anzahl von Validierungssteuerelementen.

## <a name="http-client-performance"></a>Leistung von HTTP-Clients

In ASP.NET Core 2.2 wurde die Leistung von `SocketsHttpHandler` verbessert, indem Sperrkonflikte für den Verbindungspool reduziert wurden. Bei Apps, die viele ausgehende HTTP-Anforderungen senden – beispielsweise Microservicearchitekturen – wird der Durchsatz verbessert. Unter Last kann der `HttpClient`-Durchsatz um bis zu 60 % unter Linux und bis zu 20 % unter Windows gesteigert werden.

Weitere Informationen finden Sie beim [Pull Request, durch den diese Verbesserung erzielt wurde](https://github.com/dotnet/corefx/pull/32568).

## <a name="additional-information"></a>Zusätzliche Informationen

Die vollständige Liste der Änderungen finden Sie in den Versionshinweisen zu [ASP.NET Core 2.2](https://github.com/aspnet/Home/releases/tag/2.2.0).
