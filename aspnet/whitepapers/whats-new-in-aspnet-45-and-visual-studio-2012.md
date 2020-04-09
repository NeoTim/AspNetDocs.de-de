---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: Neuerungen in ASP.NET 4.5 und Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: In diesem Dokument werden neue Funktionen und Verbesserungen beschrieben, die in ASP.NET 4.5 eingeführt werden. Es beschreibt auch Verbesserungen für die Web-Entwicklung gemacht...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675886"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>Neue Funktionen in ASP.NET 4.5 und Visual Studio 2012

> In diesem Dokument werden neue Funktionen und Verbesserungen beschrieben, die in ASP.NET 4.5 eingeführt werden. Außerdem werden Verbesserungen für die Webentwicklung in Visual Studio 2012 beschrieben. Dieses Dokument wurde ursprünglich am 29. Februar 2012 veröffentlicht.

- [ASP.NET Core Runtime und Framework](#_Toc318097372)

    - [Asynchrones Lesen und Schreiben von HTTP-Anforderungen und -Antworten](#_Toc318097373)
    - [Verbesserungen der HttpRequest-Verarbeitung](#_Toc318097374)
    - [Asynchrones Spülen einer Antwort](#_Toc318097375)
    - [Unterstützung für *await* und *Task*-Based Asynchronous Modules and Handlers](#_Toc318097376)
    - [Asynchrone HTTP-Module](#_Toc318097377)
    - [Asynchrone HTTP-Handler](#_Toc318097378)
    - [Neue ASP.NET Anforderungsvalidierungsfunktionen](#_Toc318097379)
    - [Verzögerte ("lazy") Anforderungsvalidierung](#_Toc318097380)
    - [Unterstützung für nicht validierte Anfragen](#_Toc318097381)
    - [AntiXSS-Bibliothek](#_Toc318097382)
    - [Unterstützung für WebSockets-Protokoll](#_Toc318097383)
    - [Bündelung und Minifizierung](#_Toc318097384)
    - [Leistungsverbesserungen für Webhosting](#_Toc_perf)

        - [Wichtige Leistungsfaktoren](#_Toc_perf_1)
        - [Anforderungen an neue Leistungsmerkmale](#_Toc_perf_2)
        - [Gemeinsame Versammlungen freigeben](#_Toc_perf_3)
        - [Verwenden der Multi-Core JIT-Kompilierung für schnelleren Start](#_Toc_perf_4)
        - [Optimieren der Garbage Collection zur Optimierung des Arbeitsspeichers](#_Toc_perf_5)
        - [Prefetching für Webanwendungen](#_Toc_perf_6)
- [ASP.NET Webformulare](#_Toc318097385)

    - [Stark typisierte Datensteuerelemente](#_Toc318097386)
    - [Modellbindung](#_Toc318097387)

        - [Auswählen von Daten](#_Toc318097388)
        - [Wertanbieter](#_Toc318097389)
        - [Filtern nach Werten aus einem Steuerelement](#_Toc318097390)
    - [HTML-codierte Datenbindungsausdrücke](#_Toc318097391)
    - [Unauffällige Validierung](#_Toc318097392)
    - [HTML5-Updates](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET-Webseiten 2](#_Toc318097395)
- [Visual Studio 2012-Release-Kandidat](#_Toc318097396)

    - [Projektfreigabe zwischen Visual Studio 2010 und Visual Studio 2012 Release Candidate (Projektkompatibilität)](#project-compatibility)
    - [Konfigurationsänderungen in ASP.NET 4.5 Website-Vorlagen](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [Native Unterstützung in IIS 7 für ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML-Editor](#_Toc318097397)

        - [Intelligente Aufgaben](#_Toc318097398)
        - [WAI-ARIA Unterstützung](#_Toc318097399)
        - [Neue HTML5-Snippets](#_Toc318097400)
        - [Extrahieren in die Benutzersteuerung](#_Toc318097401)
        - [IntelliSense für Code-Nuggets in Attributen](#_Toc318097402)
        - [Automatisches Umbenennen des übereinstimmenden Tags beim Umbenennen eines öffnenden oder schließenden Tags](#_Toc318097403)
        - [Generierung von Ereignishandlern](#_Toc318097404)
        - [Intelligenter Einzug](#_Toc318097405)
        - [Auto-Reduce-Anweisungsvervollständigung](#_Toc318097406)
    - [JavaScript-Editor](#_Toc318097407)

        - [Code-Umriss](#_Toc318097408)
        - [Klammernabgleich (zugehörige Klammer)](#_Toc318097409)
        - [Gehe zu Definition](#_Toc318097410)
        - [ECMAScript5-Unterstützung](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC-Signaturüberladungen](#_Toc318097413)
        - [Implizite Referenzen](#_Toc318097414)
    - [CSS-Editor](#_Toc318097415)

        - [Auto-Reduce-Anweisungsvervollständigung](#_Toc318097416)
        - [Hierarchischer Einzug.](#_Toc318097417)
        - [CSS Hacks Unterstützung](#_Toc318097418)
        - [Herstellerspezifische Schemas (-moz-,-webkit)](#_Toc318097419)
        - [Unterstützung für Kommentare und Kommentare](#_Toc318097420)
        - [Farbauswahl](#_Toc318097421)
        - [Snippets](#_Toc318097422)
        - [Benutzerdefinierte Regionen](#_Toc318097423)
    - [Seitenprüfung](#_Toc318097424)
    - [Veröffentlichung](#_Toc318097425)

        - [Veröffentlichungsprofile](#_Toc318097426)
        - [ASP.NET Vorkompilierung und Zusammenführung](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [Haftungsausschluss](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core Runtime und Framework

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>Asynchrones Lesen und Schreiben von HTTP-Anforderungen und -Antworten

ASP.NET 4 die Möglichkeit eingeführt, eine HTTP-Anforderungsentität als Stream mithilfe der *HttpRequest.GetBufferlessInputStream-Methode* zu lesen. Diese Methode bot Streamingzugriff auf die Anforderungsentität. Es wurde jedoch synchron ausgeführt, wodurch ein Thread für die Dauer einer Anforderung gebunden wurde.

ASP.NET 4.5 unterstützt die Möglichkeit, Streams asynchron auf einer HTTP-Anforderungsentität zu lesen, und die Möglichkeit, Sie asynchron zu löschen. ASP.NET 4.5 bietet Ihnen außerdem die Möglichkeit, eine HTTP-Anforderungsentität doppelt zu puffern, was die Integration mit nachgeschalteten HTTP-Handlern wie ASPX-Seitenhandlern und ASP.NET MVC-Controllern erleichtert.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>Verbesserungen der HttpRequest-Verarbeitung

Der Streamverweis, der von ASP.NET 4.5 von *HttpRequest.GetBufferlessInputStream* zurückgegeben wird, unterstützt sowohl synchrone als auch asynchrone Lesemethoden. Das von *GetBufferlessInputStream zurückgegebene* *Stream-Objekt* implementiert jetzt sowohl die BeginRead- als auch die EndRead-Methode. Mit den asynchronen *Stream-Methoden* können Sie die Anforderungsentität asynchron in Blöcken lesen, während ASP.NET den aktuellen Thread zwischen jeder Iteration einer asynchronen Leseschleife freigibt.

ASP.NET 4.5 hat auch eine Begleitmethode zum Lesen der Anforderungsentität in gepufferter Weise hinzugefügt: *HttpRequest.GetBufferedInputStream*. Diese neue Überladung funktioniert wie *GetBufferlessInputStream*, die sowohl synchrone als auch asynchrone Lesevorgänge unterstützt. Beim Lesen kopiert *GetBufferedInputStream* die Entitätsbytes jedoch auch in ASP.NET internen Puffer, sodass nachgelagerte Module und Handler weiterhin auf die Anforderungsentität zugreifen können. Wenn z. B. ein Upstreamcode in der Pipeline die Anforderungsentität bereits mit *GetBufferedInputStream*gelesen hat, können Sie weiterhin *HttpRequest.Form* oder *HttpRequest.Files*verwenden. Auf diese Weise können Sie asynchrone Verarbeitung für eine Anforderung durchführen (z. B. Streaming eines großen Dateiuploads in eine Datenbank), aber danach immer noch ASPX-Seiten und MVC-ASP.NET-Controller ausführen.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>Asynchrones Spülen einer Antwort

Das Senden von Antworten an einen HTTP-Client kann viel Zeit in Anspruch nehmen, wenn der Client weit entfernt ist oder über eine Verbindung mit geringer Bandbreite verfügt. Normalerweise ASP.NET puffert die Antwortbytes, wie sie von einer Anwendung erstellt werden. ASP.NET führt dann am Ende der Anforderungsverarbeitung einen einzelnen Sendevorgang der aufgelaufenen Puffer aus.

Wenn die gepufferte Antwort groß ist (z. B. beim Streamen einer großen Datei an einen Client), müssen Sie regelmäßig *HttpResponse.Flush* aufrufen, um gepufferte Ausgabe an den Client zu senden und die Speichernutzung unter Kontrolle zu halten. Da *Flush* jedoch ein synchroner Aufruf ist, verbraucht der iterativ aufrufende *Flush* weiterhin einen Thread für die Dauer potenziell lang andauernder Anforderungen.

ASP.NET 4.5 bietet Unterstützung für die asynchrone Ausführung von Leerungen mithilfe der *BeginFlush-* und *EndFlush-Methoden* der *HttpResponse-Klasse.* Mit diesen Methoden können Sie asynchrone Module und asynchrone Handler erstellen, die Daten inkrementell an einen Client senden, ohne Betriebssystemthreads zu binden. Zwischen *BeginFlush-* und *EndFlush-Aufrufen* gibt ASP.NET den aktuellen Thread frei. Dadurch wird die Gesamtzahl der aktiven Threads, die zur Unterstützung lang andauernder HTTP-Downloads erforderlich sind, erheblich reduziert.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>Unterstützung für *Await* und *Task* - Basierte asynchrone Module und Handler

Mit .NET Framework 4 wurde ein asynchrones Programmierkonzept eingeführt, das als *Aufgabe*bezeichnet wird. Aufgaben werden durch den *Aufgabentyp* und verwandte Typen im *Namespace System.Threading.Tasks* dargestellt. .NET Framework 4.5 baut darauf mit Compilererweiterungen auf, die das Arbeiten mit *Task-Objekten* vereinfachen. In .NET Framework 4.5 unterstützen die Compiler zwei neue Schlüsselwörter: *await* und *async*. Das Schlüsselwort *await* ist eine syntaktische Abkürzung für die Angabe, dass ein Codestück asynchron auf einen anderen Codeteil warten soll. Das *Schlüsselwort async* stellt einen Hinweis dar, mit dem Sie Methoden als aufgabenbasierte asynchrone Methoden markieren können.

Die Kombination aus *await*, *async*und dem *Task-Objekt* erleichtert Ihnen das Schreiben von asynchronem Code in .NET 4.5 erheblich. ASP.NET 4.5 unterstützt diese Vereinfachungen mit neuen APIs, mit denen Sie asynchrone HTTP-Module und asynchrone HTTP-Handler mithilfe der neuen Compilererweiterungen schreiben können.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>Asynchrone HTTP-Module

Angenommen, Sie möchten asynchrone Arbeit innerhalb einer Methode ausführen, die ein *Taskobjekt* zurückgibt. Im folgenden Codebeispiel wird eine asynchrone Methode definiert, die einen asynchronen Aufruf zum Herunterladen der Microsoft-Startseite ausführt. Beachten Sie die *async* Verwendung des async-Schlüsselworts in der Methodensignatur und den *await-Aufruf* von *DownloadStringTaskAsync*.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

Das ist alles, was Sie schreiben müssen – das .NET Framework verarbeitet automatisch das Entladen der Aufrufliste, während der Download auf den Download wartet, sowie die automatische Wiederherstellung der Aufrufliste nach dem Download.

Angenommen, Sie möchten diese asynchrone Methode in einem asynchronen ASP.NET HTTP-Modul verwenden. ASP.NET 4.5 enthält eine Hilfsmethode (*EventHandlerTaskAsyncHelper*) und einen neuen Delegattyp (*TaskEventHandler*), mit dem Sie aufgabenbasierte asynchrone Methoden in das ältere asynchrone Programmiermodell integrieren können, das von der ASP.NET HTTP-Pipeline verfügbar gemacht wird. Dieses Beispiel zeigt, wie:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>Asynchrone HTTP-Handler

Der traditionelle Ansatz zum Schreiben asynchroner Handler in ASP.NET besteht darin, die *IHttpAsyncHandler-Schnittstelle* zu implementieren. ASP.NET 4.5 führt den asynchronen Basistyp *HttpTaskAsyncHandler* ein, von dem Sie ableiten können, was das Schreiben asynchroner Handler erheblich vereinfacht.

Der *HttpTaskAsyncHandler-Typ* ist abstrakt und erfordert, dass Sie die *ProcessRequestAsync-Methode* überschreiben. Intern ASP.NET kümmert sich um die Integration der Rückgabesignatur (ein *Taskobjekt)* von *ProcessRequestAsync* mit dem älteren asynchronen Programmiermodell, das von der ASP.NET-Pipeline verwendet wird.

Das folgende Beispiel zeigt, wie Sie *Task* verwenden und als Teil der Implementierung eines asynchronen HTTP-Handlers *warten* können:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>Neue ASP.NET Anforderungsvalidierungsfunktionen

Standardmäßig führt ASP.NET Anforderungsüberprüfungen durch – es untersucht Anforderungen, die nach Markup oder Skript in Feldern, Headern, Cookies usw. suchen. Wenn eine erkannt wird, löst ASP.NET eine Ausnahme aus. Dies dient als erste Verteidigungslinie gegen potenzielle siteübergreifende Skriptangriffe.

ASP.NET 4.5 erleichtert das selektive Lesen nicht validierter Anforderungsdaten. ASP.NET 4.5 integriert auch die beliebte AntiXSS-Bibliothek, die früher eine externe Bibliothek war.

Entwickler haben häufig nach der Möglichkeit gefragt, die Anforderungsvalidierung für ihre Anwendungen selektiv zu deaktivieren. Wenn es sich bei Ihrer Anwendung beispielsweise um Forensoftware handelt, können Sie Benutzern erlauben, HTML-formatierte Forenbeiträge und Kommentare zu übermitteln, aber trotzdem sicherstellen, dass die Anforderungsüberprüfung alles andere überprüft.

ASP.NET 4.5 führt zwei Funktionen ein, die es Ihnen leicht machen, selektiv mit nicht validierten Eingaben zu arbeiten: verzögerte ("verzögerte") Anforderungsvalidierung und Zugriff auf nicht validierte Anforderungsdaten.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>Verzögerte ("lazy") Anforderungsvalidierung

In ASP.NET 4.5 unterliegen standardmäßig alle Anforderungsdaten der Anforderungsvalidierung. Sie können die Anwendung jedoch so konfigurieren, dass die Anforderungsüberprüfung so lange verzögert wird, bis Sie tatsächlich auf Anforderungsdaten zugreifen. (Dies wird manchmal als verzögerte Anforderungsüberprüfung bezeichnet, basierend auf Begriffen wie verzögertes Laden für bestimmte Datenszenarien.) Sie können die Anwendung so konfigurieren, dass die verzögerte Validierung in der Datei Web.config verwendet wird, indem Sie das *requestValidationMode-Attribut* im *httpRUntime-Element* auf 4.5 festlegen, wie im folgenden Beispiel:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

Wenn der Anforderungsüberprüfungsmodus auf 4.5 festgelegt ist, wird die Anforderungsüberprüfung nur für einen bestimmten Anforderungswert und nur ausgelöst, wenn der Code auf diesen Wert zugreift. Wenn Ihr Code beispielsweise den Wert Request.Form["forum\_post"] erhält, wird die Anforderungsüberprüfung nur für dieses Element in der Formularauflistung aufgerufen. Keines der anderen Elemente in der *Formularauflistung* wird überprüft. In früheren Versionen von ASP.NET wurde die Anforderungsüberprüfung für die gesamte Anforderungsauflistung ausgelöst, wenn auf ein Element in der Auflistung zugegriffen wurde. Das neue Verhalten erleichtert es verschiedenen Anwendungskomponenten, verschiedene Teile von Anforderungsdaten zu betrachten, ohne die Anforderungsüberprüfung für andere Teile auszulösen.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>Unterstützung für nicht validierte Anfragen

Die überprüfung der verzögerten Anforderung allein löst nicht das Problem, die Anforderungsüberprüfung selektiv zu umgehen. Der Aufruf von Request.Form["forum\_post"] löst weiterhin die Anforderungsüberprüfung für diesen bestimmten Anforderungswert aus. Sie können jedoch auf dieses Feld zugreifen, ohne die Validierung auszulösen, da Sie Markup in diesem Feld zulassen möchten.

Um dies zu ermöglichen, unterstützt ASP.NET 4.5 jetzt den ungültigen Zugriff auf Anforderungsdaten. ASP.NET 4.5 enthält eine neue *Unvalidierte* Auflistungseigenschaft in der *HttpRequest-Klasse.* Diese Auflistung bietet Zugriff auf alle allgemeinen Werte von Anforderungsdaten, wie *Form*, *QueryString*, *Cookies*und *Url*.

Um nicht validierte Anforderungsdaten lesen zu können, müssen Sie die Anwendung zunächst für die Verwendung des neuen Anforderungsüberprüfungsmodus konfigurieren, um nicht validierte Anforderungsdaten lesen zu können:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

Sie können dann die *HttpRequest.Unvalid-Eigenschaft* verwenden, um den nicht validierten Formularwert zu lesen:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> Sicherheit - *Verwenden Sie nicht validierte Anforderungsdaten mit Sorgfalt!* ASP.NET 4.5 die nicht validierten Anforderungseigenschaften und -auflistungen hinzugefügt, um Ihnen den Zugriff auf sehr spezifische nicht validierte Anforderungsdaten zu erleichtern. Sie müssen jedoch weiterhin eine benutzerdefinierte Überprüfung der Rohanforderungsdaten durchführen, um sicherzustellen, dass gefährlicher Text nicht für Benutzer gerendert wird.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS-Bibliothek

Aufgrund der Popularität der Microsoft AntiXSS-Bibliothek enthält ASP.NET 4.5 jetzt Kerncodierungsroutinen aus Version 4.0 dieser Bibliothek.

Die Codierungsroutinen werden vom *Typ AntiXssEncoder* im neuen *System.Web.Security.AntiXss-Namespace* implementiert. Sie können den *Typ AntiXssEncoder* direkt verwenden, indem Sie eine der statischen Codierungsmethoden aufrufen, die im Typ implementiert sind. Der einfachste Ansatz für die Verwendung der neuen Anti-XSS-Routinen besteht jedoch darin, eine ASP.NET-Anwendung zu konfigurieren, um standardmäßig die *AntiXssEncoder-Klasse* zu verwenden. Fügen Sie dazu der Datei Web.config das folgende Attribut hinzu:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

Wenn das *encoderType-Attribut* so eingestellt ist, dass es den *Typ AntiXssEncoder* verwendet, verwendet die gesamte Ausgabecodierung in ASP.NET automatisch die neuen Codierungsroutinen.

Dies sind die Teile der externen AntiXSS-Bibliothek, die in ASP.NET 4.5 integriert wurden:

- *HtmlEncode*, *HtmlFormUrlEncode*und *HtmlAttributeEncode*
- *XmlAttributeEncode* und *XmlEncode*
- *UrlEncode* und *UrlPathEncode* (neu)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Unterstützung für WebSockets-Protokoll

Das WebSockets-Protokoll ist ein standardbasiertes Netzwerkprotokoll, das definiert, wie eine sichere bidirektionale Echtzeitkommunikation zwischen einem Client und einem Server über HTTP hergestellt werden kann. Microsoft hat sowohl mit den IETF- als auch mit den W3C-Standardgremien zusammengearbeitet, um das Protokoll zu definieren. Das WebSockets-Protokoll wird von jedem Client (nicht nur von Browsern) unterstützt, wobei Microsoft umfangreiche Ressourcen investiert, die das WebSockets-Protokoll sowohl auf Client- als auch auf mobilen Betriebssystemen unterstützen.

Das WebSockets-Protokoll erleichtert das Erstellen von Datenübertragungen mit langer Laufzeit zwischen einem Client und einem Server. Beispielsweise ist das Schreiben einer Chatanwendung viel einfacher, da Sie eine echte, lang andauernde Verbindung zwischen einem Client und einem Server herstellen können. Sie müssen nicht auf Problemumgehungen wie periodische Abfragen oder HTTP-Langabfragen zurückgreifen, um das Verhalten eines Sockets zu simulieren.

ASP.NET 4.5 und IIS 8 enthalten Low-Level-WebSockets-Unterstützung, die es ASP.NET Entwicklern ermöglicht, verwaltete APIs zum asynchronen Lesen und Schreiben von Zeichenfolgen- und Binärdaten in einem WebSockets-Objekt zu verwenden. Für ASP.NET 4.5 gibt es einen neuen *System.Web.WebSockets-Namespace,* der Typen für die Arbeit mit dem WebSockets-Protokoll enthält.

Ein Browserclient stellt eine WebSockets-Verbindung her, indem er ein DOM *WebSocket-Objekt* erstellt, das auf eine URL in einer ASP.NET Anwendung verweist, wie im folgenden Beispiel:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

Sie können WebSockets-Endpunkte in ASP.NET mit einer beliebigen Art von Modul oder Handler erstellen. Im vorherigen Beispiel wurde eine .ashx-Datei verwendet, da .ashx-Dateien eine schnelle Möglichkeit zum Erstellen eines Handlers sind.

Gemäß dem WebSockets-Protokoll akzeptiert eine ASP.NET Anwendung die WebSockets-Anforderung eines Clients, indem sie angibt, dass die Anforderung von einer HTTP GET-Anforderung auf eine WebSockets-Anforderung aktualisiert werden soll. Hier sehen Sie ein Beispiel:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

Die *AcceptWebSocketRequest-Methode* akzeptiert einen Funktionsdelegat, da ASP.NET die aktuelle HTTP-Anforderung aufhebt und dann das Steuerelement an den Funktionsdelegat überträgt. Dieser Ansatz ähnelt im Prinzip der Verwendung von *System.Threading.Thread*, bei dem Sie einen Threadstart-Delegaten definieren, in dem Hintergrundarbeit ausgeführt wird.

Nachdem ASP.NET und der Client einen WebSockets-Handshake erfolgreich abgeschlossen haben, ruft ASP.NET Ihren Delegaten auf, und die WebSockets-Anwendung wird ausgeführt. Das folgende Codebeispiel zeigt eine einfache Echoanwendung, die die integrierte WebSockets-Unterstützung in ASP.NET verwendet:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

Die Unterstützung in .NET 4.5 für das *Await-Schlüsselwort* und asynchrone aufgabenbasierte Vorgänge eignet sich natürlich zum Schreiben von WebSockets-Anwendungen. Das Codebeispiel zeigt, dass eine WebSockets-Anforderung vollständig asynchron in ASP.NET ausgeführt wird. Die Anwendung wartet asynchron, bis eine Nachricht von einem Client gesendet wird, indem der Socket await aufgerufen *wird. ReceiveAsync*. Ebenso können Sie eine asynchrone Nachricht an einen Client senden, indem Sie *den Wartesocket aufrufen. SendAsync*.

Im Browser empfängt eine Anwendung WebSockets-Nachrichten über eine *onmessage-Funktion.* Um eine Nachricht von einem Browser zu senden, rufen Sie die *send-Methode* des WebSocket-DOM-Typs auf, wie in diesem Beispiel gezeigt: *WebSocket*

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

In Zukunft können wir Aktualisierungen dieser Funktionalität veröffentlichen, die einige der Low-Level-Codierungabstrahierung abstrahieren, die in dieser Version für WebSockets-Anwendungen erforderlich ist.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>Bündelung und Minimierung

Mit Bundling können Sie einzelne JavaScript- und CSS-Dateien zu einem Paket kombinieren, das wie eine einzelne Datei behandelt werden kann. Die Minifizierung verdichtet JavaScript- und CSS-Dateien, indem Leerzeichen und andere Zeichen entfernt werden, die nicht erforderlich sind. Diese Features funktionieren mit Webforms, ASP.NET MVC und Webseiten.

Bundles werden mit der Bundle-Klasse oder einer ihrer untergeordneten Klassen ScriptBundle und StyleBundle erstellt. Nach dem Konfigurieren einer Instanz eines Bundles wird das Paket für eingehende Anforderungen verfügbar gemacht, indem es einfach einer globalen BundleCollection-Instanz hinzugefügt wird. In den Standardvorlagen wird die Bundlekonfiguration in einer BundleConfig-Datei ausgeführt. Diese Standardkonfiguration erstellt Bundles für alle Kernskripts und csS-Dateien, die von den Vorlagen verwendet werden.

Bundles werden in Ansichten mit einer von mehreren möglichen Hilfsmethoden referenziert. Um das Rendern von unterschiedlichen Markups für ein Bundle im Debug-/Releasemodus zu unterstützen, verfügen die ScriptBundle- und StyleBundle-Klassen über die Hilfsmethode Render. Im Debugmodus generiert Render Markup für jede Ressource im Bundle. Im Freigabemodus generiert Render ein einzelnes Markupelement für das gesamte Bundle. Das Umschalten zwischen Debug- und Releasemodus kann erreicht werden, indem das Debugattribut des Kompilierungselements in web.config geändert wird, wie unten gezeigt:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

Darüber hinaus kann das Aktivieren oder Deaktivieren der Optimierung direkt über die BundleTable.EnableOptimizations-Eigenschaft festgelegt werden.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

Wenn Dateien gebündelt werden, werden sie zuerst alphabetisch sortiert (wie sie im **Projektmappen-Explorer**angezeigt werden). Sie werden dann so organisiert, dass bekannte Bibliotheken und ihre benutzerdefinierten Erweiterungen (wie jQuery, MooTools und Dojo) zuerst geladen werden. Die endgültige Reihenfolge für die Bündelung des Skriptordners wie oben gezeigt ist z. B.:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS-Dateien werden auch alphabetisch sortiert und dann neu organisiert, so dass reset.css und normalize.css vor jeder anderen Datei stehen. Die endgültige Sortierung der Bündelung des oben gezeigten Ordners "Stile" ist folgende:

1. reset.css
2. content.css
3. forms.css
4. globals.css
5. menu.css
6. styles.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Leistungsverbesserungen für Webhosting

Mit .NET Framework 4.5 und Windows 8 werden Funktionen eingeführt, mit denen Sie eine erhebliche Leistungssteigerung für Webserver-Workloads erzielen können. Dazu gehört eine Reduzierung (bis zu 35%) sowohl in der Startzeit als auch im Speicherbedarf von Webhosting-Sites, die ASP.NET verwenden.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>Wichtige Leistungsfaktoren

Idealerweise sollten alle Websites aktiv und im Speicher sein, um eine schnelle Antwort auf die nächste Anfrage zu gewährleisten, wann immer sie kommt. Zu den Faktoren, die sich auf die Reaktionsfähigkeit der Website auswirken können, gehören:

- Die Zeit, die eine Website nach dem Recycling eines App-Pools benötigt. Dies ist die Zeit, die benötigt wird, um einen Webserverprozess für die Site zu starten, wenn sich die Standortassemblys nicht mehr im Arbeitsspeicher befinden. (Die Plattformassemblys befinden sich noch im Arbeitsspeicher, da sie von anderen Sites verwendet werden.) Diese Situation wird als "Cold Site, warmes Framework-Startup" oder einfach nur als "Cold Site Startup" bezeichnet.
- Wie viel Speicher die Site belegt. Die Bedingungen hierfür sind "Pro-Standort-Speicherverbrauch" oder "nicht freigegebener Arbeitssatz".

Die neuen Leistungsverbesserungen konzentrieren sich auf beide Faktoren.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>Anforderungen an neue Leistungsmerkmale

Die Anforderungen an die neuen Funktionen lassen sich in folgende Kategorien unterteilen:

- Verbesserungen, die auf .NET Framework 4 ausgeführt werden.
- Verbesserungen, die .NET Framework 4.5 erfordern, aber auf jeder Windows-Version ausgeführt werden können.
- Verbesserungen, die nur mit .NET Framework 4.5 unter Windows 8 verfügbar sind.

Die Leistung steigt mit jeder Verbesserung, die Sie aktivieren können.

Einige der .NET Framework 4.5-Verbesserungen nutzen breitere Leistungsfeatures, die auch für andere Szenarien gelten.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>Gemeinsame Versammlungen freigeben

**Anforderung**: .NET Framework 4 und Visual Studio 11 Developer Preview SDK

Verschiedene Standorte auf einem Server verwenden häufig dieselben Hilfsassemblys (z. B. Assemblys aus einem Starterkit oder einer Beispielanwendung). Jeder Standort verfügt über eine eigene Kopie dieser Assemblys im Bin-Verzeichnis. Obwohl der Objektcode für die Assemblys identisch ist, handelt es sich um physisch getrennte Assemblys, sodass jede Assembly beim Start der kalten Site separat gelesen und separat im Arbeitsspeicher gespeichert werden muss.

Die neue Interning-Funktionalität löst diese Ineffizienz und reduziert sowohl RAM-Anforderungen als auch Ladezeit. Durch interning kann Windows eine einzelne Kopie jeder Assembly im Dateisystem behalten, und einzelne Assemblys in den Ordnern bin der Site werden durch symbolische Links zur einzelnen Kopie ersetzt. Wenn ein einzelner Standort eine eigene Version der Assembly benötigt, wird die symbolische Verknüpfung durch die neue Version der Assembly ersetzt, und nur dieser Standort ist betroffen.

Die Freigabe von Assemblys mithilfe symbolischer\_Links erfordert ein neues Tool mit dem Namen aspnet intern.exe, mit dem Sie den Speicher internierter Assemblys erstellen und verwalten können. Sie wird als Teil des Visual Studio 11 Developer Preview SDK bereitgestellt. (Es funktioniert jedoch auf einem System, auf dem nur .NET Framework 4 installiert ist, vorausgesetzt, Sie haben das neueste [Update](https://support.microsoft.com/kb/2468871)installiert .)

Um sicherzustellen, dass alle berechtigten Assemblys interniert wurden, führen Sie aspnet\_intern.exe regelmäßig aus (z. B. einmal pro Woche als geplante Aufgabe). Eine typische Verwendung ist wie folgt:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

Um alle Optionen anzuzeigen, führen Sie das Tool ohne Argumente aus.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>Verwenden der Multi-Core JIT-Kompilierung für schnelleren Start

**Anforderung**: .NET Framework 4.5

Für einen Start eines kalten Standorts müssen assemblys nicht nur vom Datenträger gelesen werden, sondern die Site muss JIT-kompiliert werden. Bei einem komplexen Standort kann dies zu erheblichen Verzögerungen führen. Eine neue allzweckübergreifende Technik in .NET Framework 4.5 reduziert diese Verzögerungen, indem die JIT-Kompilierung auf verfügbare Prozessorkerne verteilt wird. Es tut dies so viel und so früh wie möglich, indem es Informationen verwendet, die während früherer Starts der Website gesammelt wurden. Diese Funktion wurde von der [System.Runtime.ProfileOptimization.StartProfile-Methode](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) implementiert.

Die JIT-Kompilierung mit mehreren Kernen ist standardmäßig in ASP.NET aktiviert, sodass Sie nichts tun müssen, um diese Funktion zu nutzen. Wenn Sie diese Funktion deaktivieren möchten, legen Sie die folgende Einstellung in der Datei Web.config vor:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>Optimieren der Garbage Collection zur Optimierung des Arbeitsspeichers

**Anforderung**: .NET Framework 4.5

Sobald eine Site ausgeführt wird, kann die Verwendung des Garbage-Collector-Heaps (GC) ein wichtiger Faktor für den Speicherverbrauch sein. Wie jeder Garbage Collector macht auch der .NET Framework GC Kompromisse zwischen CPU-Zeit (Häufigkeit und Bedeutung von Auflistungen) und Speicherverbrauch (zusätzlicher Speicherplatz, der für neue, freigegebene oder freifähige Objekte verwendet wird). Für frühere Versionen haben wir Anleitungen zum Konfigurieren des GC bereitgestellt, um das richtige Gleichgewicht zu erzielen (z. B. [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).

Für .NET Framework 4.5 steht anstelle mehrerer eigenständiger Einstellungen eine Workload-definierte Konfigurationseinstellung zur Verfügung, die alle zuvor empfohlenen GC-Einstellungen sowie eine neue Optimierung ermöglicht, die zusätzliche Leistung für den Arbeitssatz pro Standort liefert.

Um die GC-Speicheroptimierung zu aktivieren, fügen Sie die folgende Einstellung zur Datei Windows-Microsoft.NET-Framework-v4.0.30319-aspnet.config hinzu:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(Wenn Sie mit den vorherigen Anleitungen für Änderungen an aspnet.config vertraut sind, beachten Sie, dass diese Einstellung die alten Einstellungen ersetzt, z. B. keine Notwendigkeit, gcServer, gcConcurrent usw. festzulegen. Sie müssen die alten Einstellungen nicht entfernen.)

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Prefetching für Webanwendungen

**Anforderung**: .NET Framework 4.5 läuft unter Windows 8

Für mehrere Versionen enthält Windows eine Technologie, die als [Prefetcher](http://en.wikipedia.org/wiki/Prefetcher) bekannt ist und die Lesekosten für Anwendungen reduziert. Da der Kaltstart ein Problem vor allem für Clientanwendungen darstellt, wurde diese Technologie nicht in Windows Server enthalten, das nur Komponenten enthält, die für einen Server unerlässlich sind. Prefetching ist jetzt in der neuesten Version von Windows Server verfügbar, wo es den Start einzelner Websites optimieren kann.

Für Windows Server ist der Prefetcher standardmäßig nicht aktiviert. Um den Prefetcher für Webhosting mit hoher Dichte zu aktivieren und zu konfigurieren, führen Sie den folgenden Befehlssatz in der Befehlszeile aus:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

Um den Prefetcher in ASP.NET Anwendungen zu integrieren, fügen Sie der Datei Web.config Folgendes hinzu:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>Stark typisierte Datensteuerelemente

In ASP.NET 4.5 enthält Web Forms einige Verbesserungen für die Arbeit mit Daten. Die erste Verbesserung sind stark typisierte Datensteuerelemente. Für Web Forms-Steuerelemente in früheren Versionen von ASP.NET zeigen Sie einen datengebundenen Wert mithilfe von *Eval* und einem Datenbindungsausdruck an:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

Für die zweiseitige Datenbindung verwenden Sie *Bind*:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

Zur Laufzeit verwenden diese Aufrufe Reflektion, um den Wert des angegebenen Elements zu lesen und dann das Ergebnis im Markup anzuzeigen. Dieser Ansatz erleichtert das Binden von Daten an beliebige, ungeformte Daten.

Datenbindungsausdrücke wie diese unterstützen jedoch keine Features wie IntelliSense für Membernamen, Navigation (z. B. Go To Definition) oder Kompilierungszeitüberprüfung für diese Namen.

Um dieses Problem zu beheben, fügt ASP.NET 4.5 die Möglichkeit hinzu, den Datentyp der Daten zu deklarieren, an die ein Steuerelement gebunden ist. Dazu verwenden Sie die neue *ItemType-Eigenschaft.* Wenn Sie diese Eigenschaft festlegen, stehen zwei neue typisierte Variablen im Bereich der Datenbindungsausdrücke zur Verfügung: *Item* und *BindItem*. Da die Variablen stark typisiert sind, profitieren Sie von den Vorteilen der Visual Studio-Entwicklung.

Verwenden Sie für zwei-Wege-Datenbindungsausdrücke die *Variable BindItem:*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

Die meisten Steuerelemente im ASP.NET Web Forms-Framework, die die Datenbindung unterstützen, wurden aktualisiert, um die *ItemType-Eigenschaft* zu unterstützen.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>Modellbindung

Die Modellbindung erweitert die Datenbindung in ASP.NET Web Forms-Steuerelementen, um mit dem codeorientierten Datenzugriff zu arbeiten. Es enthält Konzepte aus dem *ObjectDataSource-Steuerelement* und aus der Modellbindung in ASP.NET MVC.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>Auswählen von Daten

Um ein Datensteuerelement so zu konfigurieren, dass die Modellbindung zum Auswählen von Daten verwendet wird, legen Sie die *SelectMethod-Eigenschaft* des Steuerelements auf den Namen einer Methode im Code der Seite fest. Das Datensteuerelement ruft die Methode zum richtigen Zeitpunkt im Seitenlebenszyklus auf und bindet die zurückgegebenen Daten automatisch. Es ist nicht erforderlich, die *DataBind-Methode* explizit aufzurufen.

Im folgenden Beispiel ist das *GridView-Steuerelement* so konfiguriert, dass es eine Methode namens *GetCategories*verwendet:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

Sie erstellen die *GetCategories-Methode* im Code der Seite. Für eine einfache Auswahloperation benötigt die Methode keine Parameter und sollte ein *IEnumerable-* oder *IQueryable-Objekt* zurückgeben. Wenn die neue *ItemType-Eigenschaft* festgelegt ist (die stark typisierte Datenbindungsausdrücke aktiviert, wie zuvor unter [Stark typisierte Datensteuerelemente](#_Toc318097386) erläutert), sollten die generischen Versionen dieser Schnittstellen zurückgegeben werden – *IEnumerable&lt;T&gt; * oder *&lt;IQueryable T&gt;*, wobei der *T-Parameter* dem Typ der *ItemType-Eigenschaft* entspricht (z. B. *IQueryable&lt;Category&gt;*).

Das folgende Beispiel zeigt den Code für eine *GetCategories-Methode.* In diesem Beispiel wird das Entity Framework Code First-Modell mit der Northwind-Beispieldatenbank verwendet. Der Code stellt sicher, dass die Abfrage Details der zugehörigen Produkte für jede Kategorie über die *Include-Methode* zurückgibt. (Dadurch wird sichergestellt, dass das *TemplateField-Element* im Markup die Anzahl der Produkte in jeder Kategorie anzeigt, ohne dass eine [n+1-Auswahl erforderlich ist.)](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

Wenn die Seite ausgeführt wird, ruft das *GridView-Steuerelement* automatisch die *GetCategories-Methode* auf und rendert die zurückgegebenen Daten mithilfe der konfigurierten Felder:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Da die select-Methode ein *IQueryable-Objekt* zurückgibt, kann das *GridView-Steuerelement* die Abfrage vor der Ausführung weiter bearbeiten. Beispielsweise kann das *GridView-Steuerelement* dem zurückgegebenen *IQueryable-Objekt* Abfrageausdrücke zum Sortieren und Paging hinzufügen, bevor es ausgeführt wird, sodass diese Vorgänge vom zugrunde liegenden LINQ-Anbieter ausgeführt werden. In diesem Fall stellt Entity Framework sicher, dass diese Vorgänge in der Datenbank ausgeführt werden.

Das folgende Beispiel zeigt das *GridView-Steuerelement,* das geändert wurde, um das Sortieren und Paging zu ermöglichen:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

Wenn die Seite ausgeführt wird, kann das Steuerelement nun sicherstellen, dass nur die aktuelle Datenseite angezeigt wird und nach der ausgewählten Spalte sortiert wird:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

Um die zurückgegebenen Daten zu filtern, müssen der Select-Methode Parameter hinzugefügt werden. Diese Parameter werden von der Modellbindung zur Laufzeit aufgefüllt, und Sie können sie verwenden, um die Abfrage zu ändern, bevor Sie die Daten zurückgeben.

Angenommen, Sie möchten Benutzern das Filtern von Produkten durch Eingabe eines Schlüsselworts in die Abfragezeichenfolge überlassen. Sie können der Methode einen Parameter hinzufügen und den Code aktualisieren, um den Parameterwert zu verwenden:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

Dieser Code *Where* enthält einen Where-Ausdruck, wenn ein Wert für *das Schlüsselwort* bereitgestellt wird, und gibt dann die Abfrageergebnisse zurück.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>Wertanbieter

Im vorherigen Beispiel wurde nicht konkret angegeben, woher der Wert für den *Schlüsselwortparameter* stammt. Um diese Informationen anzugeben, können Sie ein Parameterattribut verwenden. In diesem Beispiel können Sie die *QueryStringAttribute-Klasse* im *System.Web.ModelBinding-Namespace* verwenden:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

Dadurch wird die Modellbindung angewiesen, zu versuchen, einen Wert aus der Abfragezeichenfolge zur Laufzeit an den *Schlüsselwortparameter* zu binden. (Dies kann die Ausführung einer Typkonvertierung beinhalten, in diesem Fall jedoch nicht.) Wenn ein Wert nicht bereitgestellt werden kann und der Typ nicht NULL ist, wird eine Ausnahme ausgelöst.

Die Quellen von Werten für diese Methoden werden als Wertanbieter bezeichnet, und die Parameterattribute, die angeben, welcher Wertanbieter verwendet werden soll, werden als Wertanbieterattribute bezeichnet. Web Forms enthält Wertanbieter und entsprechende Attribute für alle typischen Quellen von Benutzereingaben in einer Web Forms-Anwendung, z. B. Abfragezeichenfolge, Cookies, Formularwerte, Steuerelemente, Ansichtszustand, Sitzungsstatus und Profileigenschaften. Sie können auch benutzerdefinierte Wertanbieter schreiben.

Standardmäßig wird der Parametername als Schlüssel verwendet, um einen Wert in der Wertanbieterauflistung zu finden. Im Beispiel sucht der Code nach einem Abfragezeichenfolgenwert namens Schlüsselwort (z. B. s/default.aspx?keyword=chef). Sie können einen benutzerdefinierten Schlüssel angeben, indem Sie ihn als Argument an das Parameterattribut übergeben. Um z. B. den Wert der Abfragezeichenfolgenvariablen mit dem Namen q zu verwenden, können Sie dies tun:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

Wenn sich diese Methode im Code der Seite befindet, können Benutzer die Ergebnisse filtern, indem sie ein Schlüsselwort mithilfe der Abfragezeichenfolge übergeben:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

Die Modellbindung führt viele Aufgaben aus, die Sie andernfalls von Hand codieren müssten: Lesen des Werts, Überprüfen auf einen Nullwert, Versuchen, ihn in den entsprechenden Typ zu konvertieren, überprüfen, ob die Konvertierung erfolgreich war, und schließlich die Verwendung des Werts in der Abfrage. Die Modellbindung führt zu weit weniger Code und der Möglichkeit, die Funktionalität in der gesamten Anwendung wiederzuverwenden.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>Filtern nach Werten aus einem Steuerelement

Angenommen, Sie möchten das Beispiel erweitern, damit der Benutzer einen Filterwert aus einer Dropdownliste auswählen kann. Fügen Sie dem Markup die folgende Dropdownliste hinzu, und konfigurieren Sie es so, dass seine Daten von einer anderen Methode mithilfe der *SelectMethod-Eigenschaft* abstammen:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

In der Regel fügen Sie dem *GridView-Steuerelement* auch ein *EmptyDataTemplate-Element* hinzu, sodass das Steuerelement eine Meldung anzeigt, wenn keine übereinstimmenden Produkte gefunden werden:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

Fügen Sie im Seitencode die neue Auswahlmethode für die Dropdownliste hinzu:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

Aktualisieren Sie schließlich die *GetProducts* select-Methode, um einen neuen Parameter zu verwenden, der die ID der ausgewählten Kategorie aus der Dropdownliste enthält:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

Wenn die Seite nun ausgeführt wird, können Benutzer eine Kategorie aus der Dropdownliste auswählen, und das *GridView-Steuerelement* wird automatisch erneut gebunden, um die gefilterten Daten anzuzeigen. Dies ist möglich, da die Modellbindung die Werte von Parametern für ausgewählte Methoden verfolgt und erkennt, ob sich ein Parameterwert nach einem Postback geändert hat. Wenn dies der Zutun hat, erzwingt die Modellbindung, dass das zugehörige Datensteuerelement erneut an die Daten gebunden wird.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML-codierte Datenbindungsausdrücke

Sie können jetzt das Ergebnis von Datenbindungsausdrücken HTML-kodieren. Hinzufügen eines Doppelpunkts (:) bis zum Ende &lt;des %-Präfixes, das den Datenbindungsausdruck kennzeichnet:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>Unauffällige Validierung

Sie können jetzt die integrierten Validator-Steuerelemente so konfigurieren, dass unauffälliges JavaScript für die clientseitige Validierungslogik verwendet wird. Dadurch wird die Anzahl der inline im Seitenmarkup gerenderten JavaScript-Dateien erheblich reduziert und die Seitengröße insgesamt verringert. Sie können unauffälliges JavaScript für Validator-Steuerelemente auf eine der folgenden Arten konfigurieren:

- Global durch Hinzufügen der folgenden Einstellung zum * &lt;appSettings-Element&gt; * in der Datei Web.config: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- Global durch Festlegen der statischen *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode-Eigenschaft* auf *UnobtrusiveValidationMode.WebForms* (normalerweise in der *Application\_Start-Methode* in der Datei Global.asax).
- Individuell für eine Seite, indem Sie die neue *UnobtrusiveValidationMode-Eigenschaft* der *Page-Klasse* auf *UnobtrusiveValidationMode.WebForms*festlegen.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5-Updates

Es wurden einige Verbesserungen an Web Forms-Serversteuerelementen vorgenommen, um die neuen Funktionen von HTML5 zu nutzen:

- Die *TextMode-Eigenschaft* des *TextBox-Steuerelements* wurde aktualisiert, um die neuen HTML5-Eingabetypen wie *e-Mail*, *datetime*usw. zu unterstützen.
- Das *FileUpload-Steuerelement* unterstützt jetzt mehrere Datei-Uploads von Browsern, die diese HTML5-Funktion unterstützen.
- Validator-Steuerelemente unterstützen jetzt die Validierung von HTML5-Eingabeelementen.
- Neue HTML5-Elemente mit Attributen, die eine URL darstellen, unterstützen jetzt runat="server". Als Ergebnis können Sie ASP.NET Konventionen in URL-Pfaden verwenden, wie z. &lt;B. den Operator , um den Anwendungsstamm darzustellen&gt;(z. B. Video runat="server" src="/myVideo.wmv" / ).
- Das *UpdatePanel-Steuerelement* wurde korrigiert, um das Buchen von HTML5-Eingabefeldern zu unterstützen.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta ist jetzt in Visual Studio 11 Beta enthalten. ASP.NET MVC ist ein Framework für die Entwicklung hochprüfbarer und verwaltbarer Webanwendungen durch Nutzung des MVC-Musters (Model-View-Controller). ASP.NET MVC 4 erleichtert das Erstellen von Anwendungen für das mobile Web und enthält ASP.NET Web-API, mit der Sie HTTP-Dienste erstellen können, die jedes Gerät erreichen können. Weitere Informationen finden Sie in den [ASP.NET MVC 4-Versionshinweise](mvc4-release-notes.md).

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET-Webseiten 2

Zu den neuen Funktionen gehören die folgenden:

- Neue und aktualisierte Websitevorlagen.
- Hinzufügen einer server- und clientseitigen Validierung mithilfe des *Validierungshilfss.*
- Die Möglichkeit, Skripts mithilfe eines Assets-Managers zu registrieren.
- Aktivieren von Anmeldungen von Facebook und anderen Websites mit OAuth und OpenID.
- Hinzufügen von *Maps* Karten mithilfe des Karten-Hilfss.
- Ausführen von Webseiten-Anwendungen nebeneinander.
- Renderseiten für mobile Geräte.

Weitere Informationen zu diesen Features und ganzseitigen Codebeispielen finden Sie unter [Die wichtigsten Features in Webseiten 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

Dieser Abschnitt enthält Informationen zu Verbesserungen für die Webentwicklung in Visual Web Developer 11 Beta und Visual Studio 2012 Release Candidate.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Projektfreigabe zwischen Visual Studio 2010 und Visual Studio 2012 Release Candidate (Projektkompatibilität)

Bis Visual Studio 2012 Release Candidate, das Öffnen eines vorhandenen Projekts in einer neueren Version von Visual Studio den Konvertierungs-Assistenten gestartet hat. Dies erzwang eine Aktualisierung des Inhalts (Assets) eines Projekts und einer Projektmappe auf neue Formate, die nicht abwärtskompatibel waren. Daher konnten Sie das Projekt nach der Konvertierung nicht in der älteren Version von Visual Studio öffnen.

Viele Kunden haben uns gesagt, dass dies nicht der richtige Ansatz war. In Visual Studio 11 Beta unterstützen wir jetzt die Freigabe von Projekten und Lösungen mit Visual Studio 2010 SP1. Wenn Sie ein 2010-Projekt in Visual Studio 2012 Release Candidate öffnen, können Sie das Projekt weiterhin in Visual Studio 2010 SP1 öffnen.

> [!NOTE]
> Einige Arten von Projekten können nicht zwischen Visual Studio 2010 SP1 und Visual Studio 2012 Release Candidate gemeinsam genutzt werden. Dazu gehören einige ältere Projekte (z. B. ASP.NET MVC 2-Projekte) oder Projekte für besondere Zwecke (z. B. Setup-Projekte).

Wenn Sie ein Visual Studio 2010 SP1-Webprojekt zum ersten Mal in Visual Studio 11 Beta öffnen, werden der Projektdatei die folgenden Eigenschaften hinzugefügt:

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation und OldToolsVersion werden von dem Prozess verwendet, der die Projektdatei aktualisiert. Sie haben keinen Einfluss auf die Arbeit mit dem Projekt in Visual Studio 2010.

VisualStudioVersion ist eine neue Eigenschaft, die von MSBuild 4.5 verwendet wird und die Version von Visual Studio für das aktuelle Projekt angibt. Da diese Eigenschaft in MSBuild 4.0 (der Version von MSBuild, die Visual Studio 2010 SP1 verwendet) nicht vorhanden war, fügen wir der Projektdatei einen Standardwert hinzu.

Die VSToolsPath-Eigenschaft wird verwendet, um die richtige .targets-Datei zu bestimmen, die aus dem Pfad importiert werden soll, der durch die Einstellung MSBuildExtensionsPath32 dargestellt wird.

Es gibt auch einige Änderungen im Zusammenhang mit Importelementen. Diese Änderungen sind erforderlich, um die Kompatibilität zwischen beiden Versionen von Visual Studio zu unterstützen.

> [!NOTE]
> Wenn ein Projekt von Visual Studio 2010 SP1 und Visual Studio 11 Beta auf zwei verschiedenen\_Computern gemeinsam genutzt wird und das Projekt eine lokale Datenbank im Ordner App-Daten enthält, müssen Sie sicherstellen, dass die von der Datenbank verwendete Version von SQL Server auf beiden Computern installiert ist.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>Konfigurationsänderungen in ASP.NET 4.5 Website-Vorlagen

Die folgenden Änderungen wurden an der Standarddatei *Web.config* für Websites vorgenommen, die mithilfe von Websitevorlagen in Visual Studio 2012 Release Candidate erstellt werden:

- Im `<httpRuntime>` Element ist `encoderType` das Attribut jetzt standardmäßig so eingestellt, dass die AntiXSS-Typen verwendet werden, die ASP.NET hinzugefügt wurden. Weitere Informationen finden Sie unter [AntiXSS-Bibliothek](#_Toc318097382).
- Auch im `<httpRuntime>` Element `requestValidationMode` wird das Attribut auf "4.5" gesetzt. Dies bedeutet, dass die Anforderungsüberprüfung standardmäßig für die Verwendung der verzögerten ("lazy") Validierung konfiguriert ist. Weitere Informationen finden Sie unter [Neue ASP.NET Anforderungsvalidierungsfeatures](#_Toc318097379).
- Das `<modules>` Element `<system.webServer>` des Abschnitts `runAllManagedModulesForAllRequests` enthält kein Attribut. (Der Standardwert ist false.) Wenn Sie also eine Version von IIS 7 verwenden, die nicht auf SP1 aktualisiert wurde, können Probleme mit dem Routing an einem neuen Standort auftreten. Weitere Informationen finden Sie unter [Native Support in IIS 7 für ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).

Diese Änderungen wirken sich nicht auf vorhandene Anwendungen aus. Sie können jedoch einen Unterschied im Verhalten zwischen vorhandenen Websites und neuen Websites darstellen, die Sie für ASP.NET 4.5 mit den neuen Vorlagen erstellen.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>Native Unterstützung in IIS 7 für ASP.NET Routing

Dies ist keine Änderung an ASP.NET als solche, sondern eine Änderung der Vorlagen für neue Websiteprojekte, die Sie betreffen können, wenn Sie eine Version von IIS 7 arbeiten, auf die das SP1-Update nicht angewendet wurde.

In ASP.NET können Sie Anwendungen die folgende Konfigurationseinstellung hinzufügen, um das Routing zu unterstützen:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

Wenn **runAllManagedModulesForAllRequests** true ist, `http://mysite/myapp/home` wird eine URL wie ASP.NET, obwohl es keine *aspx*, *.mvc*oder ähnliche Erweiterung auf der URL gibt.

Ein Update, das auf IIS 7 vorgenommen wurde, macht die **runAllManagedModulesForAllRequests-Einstellung** überflüssig und unterstützt ASP.NET Routing nativ. (Informationen zum Update finden Sie im Microsoft Support-Artikel [Ein Update ist verfügbar, das bestimmten IIS 7.0- oder IIS 7.5-Handlern die Verarbeitung von Anforderungen ermöglicht, deren URLs nicht mit einem Zeitraum](https://support.microsoft.com/kb/980368)enden.)

Wenn Ihre Website unter IIS 7 ausgeführt wird und IIS aktualisiert wurde, müssen Sie **runAllManagedModulesForAllRequests** nicht auf true festlegen. Das Festlegen auf true wird nicht empfohlen, da die Anforderung unnötiger Verarbeitungsaufwand verursacht wird. Wenn diese Einstellung wahr ist, durchlaufen alle Anforderungen, einschließlich der Anforderungen für *.htm*, *.jpg*und andere statische Dateien, auch die ASP.NET Anforderungspipeline.

Wenn Sie eine neue ASP.NET 4.5-Website mit den Vorlagen erstellen, die in Visual Studio 2012 RC bereitgestellt werden, enthält die Konfiguration für die Website nicht die **Einstellung runAllManagedModulesForAllRequests.** Dies bedeutet, dass die Einstellung standardmäßig false ist.

Wenn Sie dann die Website unter Windows 7 ohne installiertes SP1 ausführen, enthält IIS 7 nicht das erforderliche Update. Daher funktioniert das Routing nicht, und es werden Fehler angezeigt. Wenn Sie ein Problem haben, bei dem das Routing nicht funktioniert, können Sie entweder die folgenden Schritte ausführen:

- Aktualisieren Sie Windows 7 auf SP1, wodurch das Update zu IIS 7 hinzugefügt wird.
- Installieren Sie das Update, das im zuvor aufgeführten Microsoft Support-Artikel beschrieben wurde.
- Legen Sie **runAllManagedModulesForAllRequests** in der Web.config-Datei dieser Website auf true fest. Beachten Sie, dass dies den Anforderungen einen gewissen Overhead hinzufügt.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML-Editor

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>Intelligente Aufgaben

In der Entwurfsansicht verfügen komplexe Eigenschaften von Serversteuerelementen häufig über zugeordnete Dialogfelder und Assistenten, um deren Einrichtung zu vereinfachen. Sie können z. B. ein spezielles Dialogfeld verwenden, um einem *Repeater-Steuerelement* eine Datenquelle hinzuzufügen oder einem *GridView-Steuerelement* Spalten hinzuzufügen.

Diese Art von UI-Hilfe für komplexe Eigenschaften war jedoch in der Quellansicht nicht verfügbar. Daher führt Visual Studio 11 Smart Tasks für die Quellansicht ein. Smart Tasks sind kontextbezogene Verknüpfungen für häufig verwendete Features in den Editoren "C" und "Visual Basic".

Bei ASP.NET Web Forms-Steuerelementen werden Smart Tasks auf Server-Tags als kleine Glyphe angezeigt, wenn sich die Einfügemarke innerhalb des Elements befindet:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

Die Intelligente Aufgabe wird erweitert, wenn Sie auf die Glyphe klicken oder STRG+ drücken. (punkt), wie in den Code-Editoren. Anschließend werden Verknüpfungen angezeigt, die der Ansicht "Intelligente Aufgaben" in der Entwurfsansicht ähneln.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

Die Smart-Aufgabe in der vorherigen Abbildung zeigt z. B. die GridView-Aufgabenoptionen. Wenn Sie Spalten bearbeiten auswählen, wird das folgende Dialogfeld angezeigt:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

Wenn Sie das Dialogfeld ausfüllen, werden dieselben Eigenschaften festgelegt, die Sie in der Entwurfsansicht festlegen können. Wenn Sie auf OK klicken, wird das Markup für das Steuerelement mit den neuen Einstellungen aktualisiert:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA Unterstützung

Das Schreiben barrierefreier Websites wird immer wichtiger. Der [WAI-ARIA-Barrierefreiheitsstandard](http://www.w3.org/WAI/intro/aria) definiert, wie Entwickler barrierefreie Websites schreiben sollen. Dieser Standard wird jetzt vollständig in Visual Studio unterstützt.

Das *Rollenattribut* verfügt beispielsweise jetzt über vollständige IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

Der WAI-ARIA-Standard führt auch Attribute ein, denen *Aria-* vorangestellt ist, mit denen Sie einem HTML5-Dokument Semantik hinzufügen können. Visual Studio unterstützt auch diese *Aria-Attribute* vollständig:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>Neue HTML5-Snippets

Um das Schreiben häufig verwendeter HTML5-Markups zu beschleunigen und zu vereinfachen, enthält Visual Studio eine Reihe von Ausschnitten. Ein Beispiel ist der Videoausschnitt:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

Um den Ausschnitt aufzurufen, drücken Sie zweimal die Tabulatortaste, wenn das Element in IntelliSense ausgewählt ist:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

Dadurch wird ein Ausschnitt erstellt, den Sie anpassen können.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>Extrahieren in die Benutzersteuerung

Bei großen Webseiten kann es eine gute Idee sein, einzelne Teile in Benutzersteuerelemente zu verschieben. Diese Form der Umgestaltung kann dazu beitragen, die Lesbarkeit der Seite zu erhöhen und die Seitenstruktur zu vereinfachen.

Um dies zu vereinfachen, können Sie beim Bearbeiten von Web Forms-Seiten in der Quellansicht jetzt Text auf einer Seite auswählen, mit der rechten Maustaste darauf klicken und dann "In Benutzersteuerung extrahieren" auswählen:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>IntelliSense für Code-Nuggets in Attributen

Visual Studio hat IntelliSense immer für serverseitige Code-Nuggets in jeder Seite oder jedem Steuerelement bereitgestellt. Jetzt enthält Visual Studio intelliSense auch Für Code-Nuggets in HTML-Attributen.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

Dies erleichtert das Erstellen von Datenbindungsausdrücken:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>Automatisches Umbenennen des übereinstimmenden Tags beim Umbenennen eines öffnenden oder schließenden Tags

Wenn Sie ein HTML-Element umbenennen (z. B. ein *div-Tag* in ein *Header-Tag* ändern), ändert sich auch das entsprechende öffnende oder schließende Tag in Echtzeit.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

Auf diese Weise wird der Fehler vermieden, bei dem Sie vergessen, ein schließendes Tag oder das falsche Zuspiel zu ändern.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>Generierung von Ereignishandlern

Visual Studio enthält jetzt Features in der Quellansicht, mit denen Sie Ereignishandler schreiben und manuell binden können. Wenn Sie einen Ereignisnamen in der Quellansicht bearbeiten, zeigt&gt;IntelliSense Create New Event an, &lt;das einen Ereignishandler im Code der Seite erstellt, der die richtige Signatur hat:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

Standardmäßig verwendet der Ereignishandler die ID des Steuerelements für den Namen der Ereignisbehandlungsmethode:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

Der resultierende Ereignishandler sieht wie folgt aus (in diesem Fall in C):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>Intelligenter Einzug

Wenn Sie die Eingabetaste drücken, während Sie sich in einem leeren HTML-Element befinden, platziert der Editor die Einfügemarke an die richtige Stelle:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

Wenn Sie an dieser Position die Eingabetaste drücken, wird das schließende Tag nach unten verschoben und eingerückt, um dem öffnenden Tag zu entsprechen. Die Einfügemarke ist ebenfalls eingerückt:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>Auto-Reduce-Anweisungsvervollständigung

Die IntelliSense-Liste in Visual Studio filtert jetzt basierend auf der Eingabe, sodass nur relevante Optionen angezeigt werden:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense filtert auch basierend auf dem Titelfall der einzelnen Wörter in der IntelliSense-Liste. Wenn Sie beispielsweise "dl" eingeben, werden sowohl dl als auch asp:DataList angezeigt:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

Diese Funktion macht es schneller, die Anweisungsvervollständigung für bekannte Elemente zu erhalten.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript-Editor

Der JavaScript-Editor in Visual Studio 2012 Release Candidate ist völlig neu und verbessert die Arbeit mit JavaScript in Visual Studio erheblich.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>Code outlining

Gliederungsbereiche werden jetzt automatisch für alle Funktionen erstellt, sodass Sie Teile der Datei reduzieren können, die für Ihren aktuellen Fokus nicht relevant sind.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>Klammernabgleich (zugehörige Klammer)

Wenn Sie die Einfügemarke auf eine öffnende oder schließende geschweifte Klammer setzen, hebt der Editor die passende Position hervor.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>Zur Definition wechseln

Mit dem Befehl Zur Definition wechseln Können Sie zur Quelle für eine Funktion oder Variable springen.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5-Unterstützung

Der Editor unterstützt die neue Syntax und APIs in ECMAScript5, der neuesten Version des Standards, der die JavaScript-Sprache beschreibt.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

IntelliSense für DOM-APIs wurde verbessert, mit Unterstützung für viele neue HTML5-APIs, einschließlich *querySelector*, DOM Storage, Cross-Document Messaging und *Canvas*. DOM IntelliSense wird jetzt von einer einzigen einfachen JavaScript-Datei und nicht von einer definition der systemeigenen Typbibliothek gesteuert. Dies macht es einfach zu erweitern oder zu ersetzen.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC-Signaturüberladungen

Detaillierte IntelliSense-Kommentare können nun für separate Überladungen von JavaScript-Funktionen deklariert werden, indem das neue * &lt;Signaturelement&gt; * verwendet wird, wie in diesem Beispiel gezeigt:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>Implizite Referenzen

Sie können jetzt JavaScript-Dateien zu einer zentralen Liste hinzufügen, die implizit in die Liste der Dateien aufgenommen wird, auf die eine bestimmte JavaScript-Datei oder ein blockierter Verweister verweist, was bedeutet, dass Sie IntelliSense für den Inhalt erhalten. Sie können z. B. jQuery-Dateien zur zentralen Liste von Dateien hinzufügen, und Sie erhalten IntelliSense für jQuery-Funktionen in jedem &lt;JavaScript-Dateiblock, unabhängig davon, ob Sie explizit darauf verwiesen haben (mit //reference /&gt;) oder nicht.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS-Editor

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>Auto-Reduce-Anweisungsvervollständigung

Die IntelliSense-Liste für CSS filtert jetzt basierend auf den CSS-Eigenschaften und Werten, die vom ausgewählten Schema unterstützt werden.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense unterstützt auch Titelfallsuchen:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>Hierarchischer Einzug

Der CSS-Editor verwendet Denktion, um hierarchische Regeln anzuzeigen, die Ihnen einen Überblick darüber geben, wie die Kaskadierungsregeln logisch organisiert sind. Im folgenden Beispiel ist die #list ein Selektor ein kaskadierendes untergeordnetes Element der Liste und wird daher eingerückt.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

Das folgende Beispiel zeigt eine komplexere Vererbung:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

Der Einzug einer Regel wird durch die übergeordneten Regeln bestimmt. Der hierarchische Einzug ist standardmäßig aktiviert, Sie können ihn jedoch im Dialogfeld Optionen deaktivieren (Tools, Optionen aus der Menüleiste):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS Hacks Unterstützung

Die Analyse von Hunderten von realen CSS-Dateien zeigt, dass CSS-Hacks sehr häufig sind, und jetzt unterstützt Visual Studio die am häufigsten verwendeten. Diese Unterstützung umfasst IntelliSense und\*die Validierung des\_Sterns ( ) und unterunterstreichen ( ) Eigenschaftenhacks:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

Typische Selektor-Hacks werden ebenfalls unterstützt, sodass hierarchische Einrückungen auch dann beibehalten werden, wenn sie angewendet werden. Ein typischer Selektor-Hack, der als Ziel für Internet Explorer 7 verwendet wird, besteht darin, einem Selektor * \*:first-child + html*voranzustellen. Wenn Sie diese Regel verwenden, wird der hierarchische Einzug beibehalten:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>Herstellerspezifische Schemas (-moz-, -webkit)

CSS3 führt viele Eigenschaften ein, die von verschiedenen Browsern zu unterschiedlichen Zeiten implementiert wurden. Dies zwang Entwickler zuvor, mithilfe herstellerspezifischer Syntax für bestimmte Browser zu codieren. Diese browserspezifischen Eigenschaften sind jetzt in IntelliSense enthalten.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>Unterstützung für Kommentare und Kommentare

Sie können CSS-Regeln jetzt mit den gleichen Tastenkombinationen kommentieren und aufarbeiten, die Sie im Code-Editor verwenden (Strg+K,C zum Kommentieren und Strg+K, sie zum Abkommentieren).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Farbauswahl

In früheren Versionen von Visual Studio bestand IntelliSense für farbbezogene Attribute aus einer Dropdownliste mit benannten Farbwerten. Diese Liste wurde durch eine voll funktionsfähige Farbauswahl ersetzt.

Wenn Sie einen Farbwert eingeben, wird die Farbauswahl automatisch angezeigt und zeigt eine Liste der zuvor verwendeten Farben gefolgt von einer Standardfarbpalette an. Sie können eine Farbe mit der Maus oder der Tastatur auswählen.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

Die Liste kann zu einer vollständigen Farbauswahl erweitert werden. Mit der Auswahl können Sie den Alphakanal steuern, indem Sie automatisch eine beliebige Farbe in RGBA konvertieren, wenn Sie den Schieberegler für die Deckkraft verschieben:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>Codeausschnitte

Ausschnitte im CSS-Editor erleichtern die Erstellung von browserübergreifenden Stilen. Viele CSS3-Eigenschaften, die browserspezifische Einstellungen erfordern, wurden jetzt in Snippets gerollt.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS-Snippets unterstützen erweiterte Szenarien (z. B. CSS3-Medienabfragen), indem sie das at-Symbol (- eingeben), das die IntelliSense-Liste anzeigt.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

Wenn Sie @media Wert auswählen und Tab drücken, fügt der CSS-Editor den folgenden Ausschnitt ein:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

Wie bei Codeausschnitten können Sie eigene CSS-Snippets erstellen.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>Benutzerdefinierte Regionen

Benannte Codebereiche, die bereits im Code-Editor verfügbar sind, stehen jetzt für die CSS-Bearbeitung zur Verfügung. Auf diese Weise können Sie verwandte Stilblöcke einfach gruppieren.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

Wenn eine Region reduziert wird, wird der Name der Region angezeigt:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Seitenprüfung

Seiteninspektor ist ein Tool, das eine Webseite (HTML, Web Forms, ASP.NET MVC oder Webseiten) in der Visual Studio-IDE rendert und Sie sowohl den Quellcode als auch die resultierende Ausgabe untersuchen können. Mit ASP.NET Seiten können Sie mit Page Inspector bestimmen, welcher serverseitige Code das HTML-Markup erstellt hat, das im Browser gerendert wird.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

Weitere Informationen zum Seiteninspektor finden Sie in den folgenden Tutorials:

- Verwenden des Seiteninspektors in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)
- Verwenden des Seiteninspektors in [ASP.NET Webformularen](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>Veröffentlichung

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>Veröffentlichungsprofile

In Visual Studio 2010 werden Veröffentlichungsinformationen für Webanwendungsprojekte nicht in der Versionskontrolle gespeichert und nicht für die Freigabe für andere Projekte entwickelt. In Visual Studio 2012 Release Candidate wurde das Format des Veröffentlichungsprofils geändert. Es wurde zu einem Team-Artefakt gemacht, und es ist jetzt einfach, von Builds auf der Grundlage von MSBuild zu nutzen. Konfigurationsinformationen zum Erstellen befinden sich im Dialogfeld Veröffentlichen, sodass Sie buildkonfigurationen vor der Veröffentlichung problemlos wechseln können.

Veröffentlichungsprofile werden im Ordner PublishProfiles gespeichert. Der Speicherort des Ordners hängt davon ab, welche Programmiersprache Sie verwenden:

- C-Code: Eigenschaften, PublishProfiles
- Visual Basic: Mein Projekt-PublishProfiles

Jedes Profil ist eine MSBuild-Datei. Während der Veröffentlichung wird diese Datei in die MSBuild-Datei des Projekts importiert. Wenn Sie in Visual Studio 2010 Änderungen am Veröffentlichungs- oder Paketprozess vornehmen möchten, müssen Sie Ihre Anpassungen in einer Datei mit dem Namen **ProjectName**.wpp.targets einfügen. Dies wird weiterhin unterstützt, aber Sie können Ihre Anpassungen jetzt im Veröffentlichungsprofil selbst einfügen. Auf diese Weise werden die Anpassungen nur für dieses Profil verwendet.

Sie können jetzt auch Veröffentlichungsprofile von MSBuild nutzen. Verwenden Sie dazu beim Erstellen des Projekts den folgenden Befehl:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

Der project.csproj-Wert ist der Pfad des Projekts, und ProfileName ist der Name des zu veröffentlichenden Profils. Alternativ können Sie den Profilnamen für die *PublishProfile-Eigenschaft* nicht übergeben, sondern den vollständigen Pfad an das Veröffentlichungsprofil übergeben.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET Vorkompilierung und Zusammenführung

Für Webanwendungsprojekte fügt Visual Studio 2012 Release Candidate auf der Seite Paket-/Veröffentlichungswebeigenschaften eine Option hinzu, mit der Sie den Inhalt Ihrer Website beim Veröffentlichen oder Verpacken des Projekts vorkompilieren und zusammenführen können. Um diese Optionen anzuzeigen, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, wählen Sie Eigenschaften aus, und wählen Sie dann die Eigenschaftenseite Paket/Web veröffentlichen aus. Die folgende Abbildung zeigt die Option Diese Anwendung vor dem Veröffentlichen vorkompilieren.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

Wenn diese Option ausgewählt ist, kompiliert Visual Studio die Anwendung vor, wenn Sie die Webanwendung veröffentlichen oder verpacken. Wenn Sie steuern möchten, wie die Site vorkompiliert oder Assemblys zusammengeführt werden, klicken Sie auf die Schaltfläche Erweitert, um diese Optionen zu konfigurieren.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Der Standardwebserver zum Testen von Webprojekten in Visual Studio ist jetzt IIS Express. Der Visual Studio Development Server ist weiterhin eine Option für den lokalen Webserver während der Entwicklung, aber IIS Express ist jetzt der empfohlene Server. Die Verwendung von IIS Express in Visual Studio 11 Beta ist der Verwendung in Visual Studio 2010 SP1 sehr ähnlich.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>Haftungsausschluss

Dies ist ein vorläufiges Dokument, das vor der kommerziellen Veröffentlichung der beschriebenen Software ggf. erheblich geändert wird.

Die in diesem Dokument enthaltenen Informationen stellen die Sicht der Microsoft Corporation der hier diskutierten Themen zum Zeitpunkt der Veröffentlichung dar. Da Microsoft auf wechselnde Marktbedingungen reagieren muss, sollten sie nicht als Verpflichtung seitens Microsoft interpretiert werden, und Microsoft kann die Genauigkeit der dargelegten Informationen nach dem Zeitpunkt der Veröffentlichung nicht garantieren.

Dieses Whitepaper dient ausschließlich Informationszwecken. MICROSOFT ÜBERNIMMT KEINE AUSDRÜCKLICHE, STILLSCHWEIGENDE ODER AUS GESETZ ERWACHSENDE GARANTIE IN BEZUG AUF DIE INFORMATIONEN IN DIESEM DOKUMENT.

Die Benutzer/innen sind verpflichtet, sich an alle anwendbaren Urheberrechtsgesetze zu halten. Unabhängig von der Anwendbarkeit der entsprechenden Urheberrechtsgesetze darf kein Teil dieses Dokuments ohne ausdrückliche schriftliche Erlaubnis der Microsoft Corporation für irgendwelche Zwecke vervielfältigt oder in einem Datenempfangssystem gespeichert oder darin eingelesen werden, unabhängig davon, auf welche Art und Weise oder mit welchen Mitteln (elektronisch, mechanisch, durch Fotokopieren, Aufzeichnen usw.) dies geschieht.

Es ist möglich, dass Microsoft Rechte an Patenten bzw. an angemeldeten Patenten, an Marken, Urheberrechten oder sonstigem geistigen Eigentum besitzt, die sich auf den fachlichen Inhalt dieses Dokuments beziehen. Die Bereitstellung dieses Dokuments gewährt Ihnen jedoch keinerlei Lizenzrechte an diesen Patenten, Marken, Urheberrechten oder anderem geistigen Eigentum, es sei denn, dies wurde ausdrücklich durch einen schriftlichen Lizenzvertrag mit der Microsoft Corporation vereinbart.

Sofern nicht anders angegeben, sind die hier dargestellten Beispielunternehmen, Organisationen, Produkte, Domainnamen, E-Mail-Adressen, Logos, Personen, Orte und Ereignisse fiktiv, und es ist keine Verbindung mit einem echten Unternehmen, einer Organisation, einem Produkt, einem Domänennamen, einer E-Mail-Adresse, einem Logo, einer Person, einem Ort oder einer Veranstaltung beabsichtigt oder sollte abgeleitet werden.

© 2012 Microsoft Corporation. Alle Rechte vorbehalten.

Microsoft und Windows sind eingetragene Marken oder Marken der Microsoft Corporation in den USA und/oder anderen Ländern.

Die in diesem Dokument erwähnten Namen von Unternehmen und Produkten können Marken der jeweiligen Eigentümer sein.
