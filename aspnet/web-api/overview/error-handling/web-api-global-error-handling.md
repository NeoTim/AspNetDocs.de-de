---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: Globale Fehlerbehandlung in ASP.NET Web-API 2 - ASP.NET 4.x
author: davidmatson
description: Eine Übersicht über die globale Fehlerbehandlung in ASP.NET Web API 2 für ASP.NET 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675430"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>Globale Fehlerbehandlung in ASP.NET Web-API 2

von [David Matson](https://github.com/davidmatson), [Rick Anderson](https://twitter.com/RickAndMSFT)

Dieses Thema bietet einen Überblick über die globale Fehlerbehandlung in ASP.NET Web-API 2 für ASP.NET 4.x. Heute gibt es in der Web-API keine einfache Möglichkeit, Fehler global zu protokollieren oder zu behandeln. Einige nicht behandelte Ausnahmen können über [Ausnahmefilter](exception-handling.md)verarbeitet werden, es gibt jedoch eine Reihe von Fällen, die Ausnahmefilter nicht verarbeiten können. Beispiel:

1. Von Controllerkonstruktoren ausgelöste Ausnahmen.
2. Von Meldungshandlern ausgelöste Ausnahmen
3. Während des Routings ausgelöste Ausnahmen.
4. Während der Serialisierung von Antwortinhalten ausgelöste Ausnahmen.

Wir möchten eine einfache, konsistente Möglichkeit bieten, diese Ausnahmen zu protokollieren und (wo möglich) zu behandeln. 

Es gibt zwei Hauptfälle für die Behandlung von Ausnahmen, den Fall, in dem wir in der Lage sind, eine Fehlerantwort zu senden, und den Fall, in dem wir nur die Ausnahme protokollieren können. Ein Beispiel für den letzteren Fall ist, wenn eine Ausnahme in der Mitte von Streaming-Antwortinhalten ausgelöst wird. in diesem Fall ist es zu spät, eine neue Antwortnachricht zu senden, da der Statuscode, die Header und der Teilinhalt bereits über den Draht gegangen sind, sodass wir die Verbindung einfach abbrechen. Auch wenn die Ausnahme nicht behandelt werden kann, um eine neue Antwortnachricht zu erzeugen, unterstützen wir weiterhin die Protokollierung der Ausnahme. In Fällen, in denen wir einen Fehler erkennen können, können wir eine entsprechende Fehlerantwort zurückgeben, wie im Folgenden gezeigt:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>Vorhandene Optionen

Zusätzlich zu [Ausnahmefiltern](exception-handling.md)können [Nachrichtenhandler](../advanced/http-message-handlers.md) heute verwendet werden, um alle Antworten auf 500 Ebenen zu beobachten, aber das Handeln auf diese Antworten ist schwierig, da ihnen der Kontext über den ursprünglichen Fehler fehlt. Nachrichtenhandler haben auch einige der gleichen Einschränkungen wie Ausnahmefilter in Bezug auf die Fälle, die sie behandeln können. Während die Web-API über eine Ablaufverfolgungsinfrastruktur verfügt, die Fehlerbedingungen erfasst, dient die Ablaufverfolgungsinfrastruktur zu Diagnosezwecken und ist nicht für die Ausführung in Produktionsumgebungen konzipiert oder geeignet. Globale Ausnahmebehandlung und Protokollierung sollten Dienste sein, die während der Produktion ausgeführt und in vorhandene Überwachungslösungen (z. B. [ELMAH )](https://code.google.com/p/elmah/)eingebunden werden können.

### <a name="solution-overview"></a>Übersicht über die Lösungen

 Wir bieten zwei neue benutzeraustauschbare Dienste, [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) und IExceptionHandler, um nicht behandelte Ausnahmen zu protokollieren und zu behandeln. Die Dienstleistungen sind sehr ähnlich, mit zwei Hauptunterschieden:

1. Wir unterstützen die Registrierung mehrerer Ausnahmeprotokollierungen, aber nur einen einzelnen Ausnahmehandler.
2. Ausnahmeprotokoller werden immer aufgerufen, auch wenn wir im Begriff sind, die Verbindung abzubrechen. Ausnahmehandler werden nur aufgerufen, wenn wir noch auswählen können, welche Antwortnachricht gesendet werden soll.

Beide Dienste bieten Zugriff auf einen Ausnahmekontext, der relevante Informationen ab dem Punkt enthält, an dem die Ausnahme erkannt wurde, insbesondere [die HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), die [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), die ausgelöste Ausnahme und die Ausnahmequelle (Details unten).

### <a name="design-principles"></a>Entwurfsprinzipien

1. **Keine brechenden Änderungen** Da diese Funktionalität in einer kleineren Version hinzugefügt wird, besteht eine wichtige Einschränkung, die sich auf die Lösung auswirkt, darin, dass es keine Änderungen gibt, weder zum Typkontrakten noch zum Verhalten. Diese Einschränkung schloss einige Bereinigungen aus, die wir gerne in Bezug auf bestehende Fangblöcke durchgeführt hätten, die Ausnahmen in 500 Antworten verwandelten. Diese zusätzliche Bereinigung ist etwas, das wir für eine nachfolgende Hauptversion in Betracht ziehen könnten. Wenn dies für Sie wichtig ist, stimmen Sie bitte darüber unter [ASP.NET Web-API-Benutzerstimme](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)ab.
2. **Aufrechterhaltung der Konsistenz mit Web-API-Konstrukten** Die Filterpipeline der Web-API ist eine hervorragende Möglichkeit, querschnittsübergreifende Bedenken mit der Flexibilität zu behandeln, die Logik auf einen aktionsspezifischen, Controller-spezifischen oder globalen Bereich anzuwenden. Filter, einschließlich Ausnahmefilter, haben immer Aktions- und Controllerkontexte, auch wenn sie im globalen Bereich registriert sind. Dieser Vertrag ist für Filter sinnvoll, bedeutet jedoch, dass Ausnahmefilter, auch global ausgerichtete, für einige Ausnahmebehandlungsfälle nicht geeignet sind, z. B. Ausnahmen von Nachrichtenhandlern, bei denen kein Aktions- oder Controllerkontext vorhanden ist. Wenn wir das flexible Scoping von Filtern für die Ausnahmebehandlung nutzen wollen, benötigen wir immer noch Ausnahmefilter. Wenn wir jedoch Ausnahmen außerhalb eines Controllerkontexts behandeln müssen, benötigen wir auch ein separates Konstrukt für die vollständige globale Fehlerbehandlung (etwas ohne den Controllerkontext und die Einschränkungen des Aktionskontexts).

### <a name="when-to-use"></a>Wann zu verwenden

- Ausnahmeprotokollierungen sind die Lösung, um alle nicht behandelten Ausnahmen zu sehen, die von der Web-API abgefangen werden.
- Ausnahmehandler sind die Lösung zum Anpassen aller möglichen Antworten an nicht behandelte Ausnahmen, die von der Web-API abgefangen werden.
- Ausnahmefilter sind die einfachste Lösung für die Verarbeitung der nicht behandelten Ausnahmen der Teilmenge, die sich auf eine bestimmte Aktion oder einen bestimmten Controller beziehen.

### <a name="service-details"></a>Dienstdetails

 Die Ausnahmeprotokollierungs- und Handlerdienstschnittstellen sind einfache asynchrone Methoden, die die entsprechenden Kontexte verwenden: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 Wir bieten auch Basisklassen für beide Schnittstellen. Das Überschreiben der Core-Methoden (Sync oder async) ist alles, was zum Protokollieren oder Behandeln zu den empfohlenen Zeiten erforderlich ist. Bei der `ExceptionLogger` Protokollierung stellt die Basisklasse sicher, dass die Core-Protokollierungsmethode nur einmal für jede Ausnahme aufgerufen wird (auch wenn sie später weiter oben in der Aufrufliste weiter verbreitet wird und erneut abgefangen wird). Die `ExceptionHandler` Basisklasse ruft die Kernbehandlungsmethode nur für Ausnahmen am oberen Rand der Aufrufliste auf und ignoriert ältere verschachtelte Catch-Blöcke. (Vereinfachte Versionen dieser Basisklassen finden Sie im Anhang unten.) Beide `IExceptionLogger` `IExceptionHandler` und erhalten Informationen über `ExceptionContext`die Ausnahme über eine .

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

Wenn das Framework eine Ausnahmeprotokollierung oder einen Ausnahmehandler aufruft, stellt es immer eine `Exception` und eine `Request`bereit. Mit Ausnahme von Komponententests wird `RequestContext`es auch immer eine . Es wird selten `ControllerContext` `ActionContext` eine und (nur beim Aufrufen von der catch-Block für Ausnahmefilter). Es wird sehr `Response`selten eine liefern (nur in bestimmten IIS-Fällen, wenn in der Mitte des Versuchs, die Antwort zu schreiben). Beachten Sie, dass es, `null` da einige dieser Eigenschaften `null` möglicherweise darin bestehen, dass der Consumer vor dem Zugriff auf Member der Ausnahmeklasse nachprüfe.`CatchBlock` ist eine Zeichenfolge, die angibt, welcher catch-Block die Ausnahme gesehen hat. Die catch-Blockzeichenfolgen lauten wie folgt:

- HttpServer (SendAsync-Methode)
- HttpControllerDispatcher (SendAsync-Methode)
- HttpBatchHandler (SendAsync-Methode)
- IExceptionFilter (ApiControllers Verarbeitung der Ausnahmefilterpipeline in ExecuteAsync)
- OWIN-Host:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (für Pufferausgabe)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (für Streaming-Ausgabe)
- Webhost:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (für Pufferausgabe)
    - HttpControllerHandler.WriteStreamedResponseContentAsync (für Streaming-Ausgabe)
    - HttpControllerHandler.WriteErrorResponseContentAsync (bei Fehlern bei der Fehlerwiederherstellung im gepufferten Ausgabemodus)

Die Liste der catch-Blockzeichenfolgen ist auch über statische schreibgeschützte Eigenschaften verfügbar. (Die Kern-Catch-Blockzeichenfolge befindet sich auf den statischen ExceptionCatchBlocks; der Rest wird jeweils in einer statischen Klasse für OWIN und Webhost angezeigt).`IsTopLevelCatchBlock` ist hilfreich, um das empfohlene Muster der Behandlung von Ausnahmen nur am oberen Rand der Aufrufliste zu befolgen. Anstatt Ausnahmen in 500 Antworten zu verwandeln, an der überall ein geschachtelter Catch-Block auftritt, kann ein Ausnahmehandler Ausnahmen propagieren lassen, bis sie vom Host angezeigt werden.

Zusätzlich zu `ExceptionContext`der erhält ein Logger eine weitere `ExceptionLoggerContext`Information über die volle :

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

Die zweite `CanBeHandled`Eigenschaft , ermöglicht es einer Protokollierung, eine Ausnahme zu identifizieren, die nicht behandelt werden kann. Wenn die Verbindung abgebrochen werden soll und keine neue Antwortnachricht gesendet werden kann, werden die Logger aufgerufen, aber der Handler wird ***nicht*** aufgerufen, und die Logger können dieses Szenario anhand dieser Eigenschaft identifizieren.

Zusätzlich zu `ExceptionContext`der erhält ein Handler eine weitere Eigenschaft, die er vollständig `ExceptionHandlerContext` festlegen kann, um die Ausnahme zu behandeln:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

Ein Ausnahmehandler gibt an, dass er `Result` eine Ausnahme behandelt hat, indem er die Eigenschaft auf ein Aktionsergebnis festlegt (z. B. [exceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)oder ein benutzerdefiniertes Ergebnis). Wenn `Result` die Eigenschaft null ist, wird die Ausnahme nicht behandelt, und die ursprüngliche Ausnahme wird erneut ausgelöst.

Für Ausnahmen am oberen Rand der Aufrufliste haben wir einen zusätzlichen Schritt unternommen, um sicherzustellen, dass die Antwort für API-Aufrufer geeignet ist. Wenn die Ausnahme an den Host weitergegeben wird, wird dem Aufrufer der gelbe Bildschirm des Todes oder eine andere vom Host bereitgestellte Antwort angezeigt, die in der Regel HTML und normalerweise keine geeignete API-Fehlerantwort ist. In diesen Fällen startet das Ergebnis ungleich NULL, und nur wenn `null` ein benutzerdefinierter Ausnahmehandler es explizit auf (unbehandelt) zurücksetzt, wird die Ausnahme an den Host weitergegeben. Die `Result` `null` Einstellung auf in solchen Fällen kann für zwei Szenarien nützlich sein:

1. OWIN gehostete Web-API mit benutzerdefinierter Ausnahmebehandlung von Middleware, die vor/außerhalb der Web-API registriert ist.
2. Lokales Debuggen über einen Browser, bei dem der gelbe Bildschirm des Todes tatsächlich eine hilfreiche Antwort für eine nicht behandelte Ausnahme ist.

Sowohl für Ausnahmeprotokollierungen als auch für Ausnahmehandler tun wir nichts, um wiederherzustellen, wenn der Logger oder Handler selbst eine Ausnahme auslöst. (Anstatt die Ausnahme propagieren zu lassen, lassen Sie Feedback am Ende dieser Seite, wenn Sie einen besseren Ansatz haben.) Der Vertrag für Ausnahmelogger und Handler besteht darin, dass sie ausnahmen nicht an ihre Aufrufer weitergeben lassen sollten. Andernfalls wird die Ausnahme nur an den Host weitergegeben, was zu einem HTML-Fehler führt (z. B. ASP). NET-Gelbbildschirm), der an den Client zurückgesendet wird (was normalerweise nicht die bevorzugte Option für API-Aufrufer ist, die JSON oder XML erwarten).

## <a name="examples"></a>Beispiele

### <a name="tracing-exception-logger"></a>Ablaufverfolgung stabellenerohnen

Die Ausnahmeprotokollierung unten sendet Ausnahmedaten an konfigurierte Ablaufverfolgungsquellen (einschließlich des Debugausgabefensters in Visual Studio).

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>Benutzerdefinierte Fehlermeldung Exception Handler

Der unten stehende Ausnahmehandler erzeugt eine benutzerdefinierte Fehlerantwort an Clients, einschließlich einer E-Mail-Adresse für die Kontaktaufnahme mit dem Support.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>Registrieren von Ausnahmefiltern

Wenn Sie die Projektvorlage "ASP.NET MVC 4 Web Application" zum Erstellen ihres `WebApiConfig` Projekts verwenden, legen Sie Ihren Web-API-Konfigurationscode in der Klasse im *Ordner App_Start:*

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>Anhang: Basisklassendetails

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
