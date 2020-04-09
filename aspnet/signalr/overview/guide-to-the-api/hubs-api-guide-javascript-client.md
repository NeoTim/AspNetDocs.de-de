---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API Guide - JavaScript Client | Microsoft Docs
author: bradygaster
description: Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in JavaScript-Clients, z. B. Browsern und Windows Store (WinJS)-Applicat...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675712"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hubs API Guide - JavaScript Client

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in JavaScript-Clients, z. B. Browsern und Windows Store-Anwendungen (WinJS).
>
> Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen. Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden. Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden. SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.
>
> SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections. Eine Einführung in SignalR, Hubs und persistente Verbindungen finden Sie unter [Einführung in SignalR](../getting-started/introduction-to-signalr.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR Version 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Frühere Versionen dieses Themas
>
> Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
>
> Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten. Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Übersicht

Dieses Dokument enthält folgende Abschnitte:

- [Der generierte Proxy und was er für Sie tut](#genproxy)

    - [Wann der generierte Proxy verwendet werden soll](#cantusegenproxy)
- [Client-Setup](#clientsetup)

    - [Verweisen auf den dynamisch generierten Proxy](#dynamicproxy)
    - [Erstellen einer physischen Datei für den von SignalR generierten Proxy](#manualproxy)
- [So stellen Sie eine Verbindung her](#establishconnection)

    - [".connection.hub" ist das gleiche Objekt, das .hubConnection() erstellt.](#connequivalence)
    - [Asynchrone Ausführung der Startmethode](#asyncstart)
- [So stellen Sie eine domänenübergreifende Verbindung her](#crossdomain)
- [So konfigurieren Sie die Verbindung](#configureconnection)

    - [Angeben von Abfragezeichenfolgenparametern](#querystring)
    - [So geben Sie die Transportmethode an](#transport)
- [So erhalten Sie einen Proxy für eine Hub-Klasse](#getproxy)
- [Definieren von Methoden auf dem Client, die der Server aufrufen kann](#callclient)
- [Aufrufen von Servermethoden vom Client](#callserver)
- [Behandeln von Verbindungslebensdauerereignissen](#connectionlifetime)
- [Umgang mit Fehlern](#handleerrors)
- [So aktivieren Sie die clientseitige Protokollierung](#logging)

Eine Dokumentation zum Programmieren des Servers oder der .NET-Clients finden Sie in den folgenden Ressourcen:

- [SignalR Hubs API Guide - Server](hubs-api-guide-server.md)
- [SignalR Hubs API-Leitfaden - .NET Client](hubs-api-guide-net-client.md)

Die SignalR 2-Serverkomponente ist nur auf .NET 4.5 verfügbar (obwohl es einen .NET-Client für SignalR 2 auf .NET 4.0 gibt).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>Der generierte Proxy und was er für Sie tut

Sie können einen JavaScript-Client programmieren, um mit einem SignalR-Dienst mit oder ohne Proxy zu kommunizieren, den SignalR für Sie generiert. Der Proxy vereinfacht die Syntax des Codes, den Sie zum Herstellen einer Verbindung verwenden, schreibende Methoden, die der Server aufruft, und Aufrufmethoden auf dem Server.

Wenn Sie Code zum Aufrufen von Servermethoden schreiben, können Sie mit dem generierten Proxy eine `serverMethod(arg1, arg2)` Syntax `invoke('serverMethod', arg1, arg2)`verwenden, die so aussieht, als würden Sie eine lokale Funktion ausführen: Sie können schreiben statt . Die generierte Proxysyntax ermöglicht auch einen sofortigen und verständlichen clientseitigen Fehler, wenn Sie einen Servermethodennamen falsch eingeben. Und wenn Sie die Datei, die die Proxys definiert, manuell erstellen, können Sie auch IntelliSense-Unterstützung für das Schreiben von Code erhalten, der Servermethoden aufruft.

Angenommen, Sie haben die folgende Hub-Klasse auf dem Server:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Die folgenden Codebeispiele zeigen, wie JavaScript-Code `NewContosoChatMessage` aussieht, um die Methode auf `addContosoChatMessageToPage` dem Server aufzurufen und Aufrufe der Methode vom Server zu empfangen.

**Mit dem generierten Proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Ohne den generierten Proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Wann der generierte Proxy verwendet werden soll

Wenn Sie mehrere Ereignishandler für eine Clientmethode registrieren möchten, die der Server aufruft, können Sie den generierten Proxy nicht verwenden. Andernfalls können Sie den generierten Proxy verwenden oder nicht basierend auf Ihrer Codierungseinstellung. Wenn Sie es nicht verwenden möchten, müssen Sie nicht auf die URL "Signalr/Hubs" in einem `script` Element in Ihrem Clientcode verweisen.

<a id="clientsetup"></a>

## <a name="client-setup"></a>Clientsetup

Ein JavaScript-Client erfordert Verweise auf jQuery und die SignalR-Kern-JavaScript-Datei. Die jQuery-Version muss 1.6.4 oder größere versionen, wie 1.7.2, 1.8.2 oder 1.9.1 sein. Wenn Sie sich für die Verwendung des generierten Proxys entscheiden, benötigen Sie auch einen Verweis auf die von SignalR generierte JavaScript-Proxydatei. Das folgende Beispiel zeigt, wie die Verweise auf einer HTML-Seite aussehen können, die den generierten Proxy verwendet.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

Diese Verweise müssen in dieser Reihenfolge enthalten sein: jQuery first, SignalR core after, and SignalR proxies last.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Verweisen auf den dynamisch generierten Proxy

Im vorherigen Beispiel bezieht sich der Verweis auf den von SignalR generierten Proxy auf dynamisch generierten JavaScript-Code und nicht auf eine physische Datei. SignalR erstellt den JavaScript-Code für den Proxy on the fly und stellt ihn dem Client als Antwort auf die URL "/signalr/hubs" zur Last. Wenn Sie in Ihrer `MapSignalR` Methode eine andere Basis-URL für SignalR-Verbindungen auf dem Server angegeben haben, ist die URL für die dynamisch generierte Proxydatei Ihre benutzerdefinierte URL mit "/hubs", an die sie angehängt ist.

> [!NOTE]
> Verwenden Sie für Windows 8 (Windows Store)-JavaScript-Clients die physische Proxydatei anstelle der dynamisch generierten. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Erstellen einer physischen Datei für den von SignalR generierten Proxy.](#manualproxy)

Verwenden Sie in einer ASP.NET MVC 4- oder 5-Razor-Ansicht die Tilde, um auf den Anwendungsstamm in Ihrem Proxydateiverweis zu verweisen:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

Weitere Informationen zur Verwendung von SignalR in MVC 5 finden Sie [unter Erste Schritte mit SignalR und MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

Verwenden Sie `Url.Content` in einer ASP.NET MVC 3 Razor-Ansicht für Ihren Proxydateiverweis:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

Verwenden Sie `ResolveClientUrl` in einer ASP.NET Web Forms-Anwendung für den Proxydateiverweis oder registrieren Sie sie über den ScriptManager mithilfe eines relativen App-Stammpfads (beginnend mit einer Tilde):

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

Verwenden Sie in der Regel dieselbe Methode zum Angeben der URL "/signalr/hubs", die Sie für CSS- oder JavaScript-Dateien verwenden. Wenn Sie eine URL ohne Tilde angeben, funktioniert die Anwendung in einigen Szenarien ordnungsgemäß, wenn Sie in Visual Studio mit IIS Express testen, schlägt jedoch mit einem 404-Fehler fehl, wenn Sie bei der Bereitstellung auf vollständigem IIS bereitstellen. Weitere Informationen finden Sie unter **Auflösen von Verweisen auf Ressourcen auf Stammebene** [in Webservern in Visual Studio für ASP.NET Webprojekte](https://msdn.microsoft.com/library/58wxa9w5.aspx) auf der MSDN-Website.

Wenn Sie ein Webprojekt in Visual Studio 2017 im Debugmodus ausführen und Internet Explorer als Browser verwenden, wird die Proxydatei im **Projektmappen-Explorer** unter **Skripts**angezeigt.

Doppelklicken Sie auf **Hubs**, um den Inhalt der Datei anzuzeigen. Wenn Sie Visual Studio 2012 oder 2013 und Internet Explorer nicht verwenden oder sich nicht im Debugmodus befinden, können Sie den Inhalt der Datei auch abrufen, indem Sie zur URL "/signalR/hubs" navigieren. Wenn Ihre Website z. `http://localhost:56699`B. `http://localhost:56699/SignalR/hubs` unter ausgeführt wird, wechseln Sie in Ihrem Browser zu.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>Erstellen einer physischen Datei für den von SignalR generierten Proxy

Alternativ zum dynamisch generierten Proxy können Sie eine physische Datei mit dem Proxycode erstellen und auf diese Datei verweisen. Sie können dies tun, um das Caching- oder Bündelungsverhalten zu steuern oder IntelliSense zu erhalten, wenn Sie Aufrufe von Servermethoden codieren.

Führen Sie die folgenden Schritte aus, um eine Proxydatei zu erstellen:

1. Installieren Sie das [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet-Paket.
2. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum *Ordner tools,* der die Datei SignalR.exe enthält. Der Werkzeugordner befindet sich an folgendem Speicherort:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. Geben Sie den folgenden Befehl ein:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    Der Pfad zu Ihrer *DLL* ist in der Regel der *Ordner bin* in Ihrem Projektordner.

    Dieser Befehl erstellt eine Datei mit dem Namen *server.js* im selben Ordner wie *signalr.exe*.
4. Legen Sie die Datei *server.js* in einen entsprechenden Ordner in Ihrem Projekt, benennen Sie sie entsprechend Ihrer Anwendung um, und fügen Sie anstelle der Referenz "signalr/hubs" einen Verweis darauf hinzu.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>So stellen Sie eine Verbindung her

Bevor Sie eine Verbindung herstellen können, müssen Sie ein Verbindungsobjekt erstellen, einen Proxy erstellen und Ereignishandler für Methoden registrieren, die vom Server aufgerufen werden können. Wenn die Proxy- und Ereignishandler eingerichtet sind, `start` stellen Sie die Verbindung her, indem Sie die Methode aufrufen.

Wenn Sie den generierten Proxy verwenden, müssen Sie das Verbindungsobjekt nicht in Ihrem eigenen Code erstellen, da der generierte Proxycode dies für Sie tut.

<a id="nogenconnection"></a>

**Herstellen einer Verbindung (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Herstellen einer Verbindung (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen. Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

Standardmäßig ist der Hubspeicherort der aktuelle Server. Wenn Sie eine Verbindung zu einem anderen Server `start` herstellen, geben Sie die URL an, bevor Sie die Methode aufrufen, wie im folgenden Beispiel gezeigt:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> Normalerweise registrieren Sie Ereignishandler, `start` bevor Sie die Methode aufrufen, um die Verbindung herzustellen. Wenn Sie einige Ereignishandler registrieren möchten, nachdem Sie die Verbindung hergestellt haben, können Sie dies tun, `start` aber Sie müssen mindestens einen Ihrer Ereignishandler registrieren, bevor Sie die Methode aufrufen. Ein Grund dafür ist, dass es viele Hubs in einer Anwendung geben `OnConnected` kann, aber Sie möchten das Ereignis nicht auf jedem Hub auslösen, wenn Sie nur für einen von ihnen verwenden möchten. Wenn die Verbindung hergestellt wird, ist das Vorhandensein einer Clientmethode auf dem `OnConnected` Proxy eines Hubs, was SignalR anweist, das Ereignis auszulösen. Wenn Sie vor dem Aufruf der `start` Methode keine Ereignishandler registrieren, können Sie Methoden auf dem `OnConnected` Hub aufrufen, aber die Hub-Methode wird nicht aufgerufen, und es werden keine Clientmethoden vom Server aufgerufen.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>".connection.hub" ist das gleiche Objekt, das .hubConnection() erstellt.

Wie Sie an den Beispielen sehen können, `$.connection.hub` bezieht sich die Verwendung des generierten Proxys auf das Verbindungsobjekt. Dies ist das gleiche Objekt, das Sie beim Aufrufen `$.hubConnection()` erhalten, wenn Sie den generierten Proxy nicht verwenden. Der generierte Proxycode erstellt die Verbindung für Sie, indem die folgende Anweisung ausgeführt wird:

![Erstellen einer Verbindung in der generierten Proxydatei](hubs-api-guide-javascript-client/_static/image3.png)

Wenn Sie den generierten Proxy verwenden, `$.connection.hub` können Sie alles tun, was Sie mit einem Verbindungsobjekt tun können, wenn Sie den generierten Proxy nicht verwenden.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Asynchrone Ausführung der Startmethode

Die `start` Methode wird asynchron ausgeführt. Es gibt ein [jQuery Deferred-Objekt](http://api.jquery.com/category/deferred-object/)zurück, was bedeutet, dass `pipe` `done`Sie `fail`Rückruffunktionen hinzufügen können, indem Sie Methoden wie , und aufrufen. Wenn Sie Code haben, den Sie ausführen möchten, nachdem die Verbindung hergestellt wurde, z. B. einen Aufruf einer Servermethode, setzen Sie diesen Code in eine Rückruffunktion oder rufen Sie ihn von einer Rückruffunktion auf. Die `.done` Rückrufmethode wird ausgeführt, nachdem die Verbindung hergestellt wurde und nachdem `OnConnected` der Code, den Sie in der Ereignishandlermethode auf dem Server haben, die Ausführung abgeschlossen hat.

Wenn Sie die Anweisung "Jetzt verbunden" aus dem vorherigen Beispiel `start` als nächste Codezeile nach dem Methodenaufruf (nicht in einem `.done` Rückruf) setzen, wird die `console.log` Zeile ausgeführt, bevor die Verbindung hergestellt wird, wie im folgenden Beispiel gezeigt:

![Falsche Art und Weise, Code zu schreiben, der ausgeführt wird, nachdem eine Verbindung hergestellt wurde](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>So stellen Sie eine domänenübergreifende Verbindung her

Wenn der Browser eine `http://contoso.com`Seite aus lädt, befindet sich die `http://contoso.com/signalr`SignalR-Verbindung in derselben Domäne unter . Wenn die `http://contoso.com` Seite von `http://fabrikam.com/signalr`eine Verbindung zu herstellt, handelt es sich um eine domänenübergreifende Verbindung. Aus Sicherheitsgründen sind domänenübergreifende Verbindungen standardmäßig deaktiviert.

In SignalR 1.x wurden domänenübergreifende Anforderungen durch ein einzelnes EnableCrossDomain-Flag gesteuert. Dieses Flag steuerte sowohl JSONP- als auch CORS-Anforderungen. Für eine größere Flexibilität wurde die gesamte CORS-Unterstützung aus der Serverkomponente von SignalR entfernt (JavaScript-Clients verwenden CORS weiterhin normal, wenn festgestellt wird, dass der Browser dies unterstützt), und neue OWIN-Middleware wurde zur Unterstützung dieser Szenarien bereitgestellt.

Wenn JSONP auf dem Client erforderlich ist (zur Unterstützung domänenübergreifender Anforderungen in älteren `EnableJSONP` Browsern), muss es explizit aktiviert werden, indem für das `HubConfiguration` Objekt auf `true`, wie unten gezeigt, festgelegt wird. JSONP ist standardmäßig deaktiviert, da es weniger sicher als CORS ist.

**Hinzufügen von Microsoft.Owin.Cors zu Ihrem Projekt:** Um diese Bibliothek zu installieren, führen Sie den folgenden Befehl in der Package Manager-Konsole aus:

`Install-Package Microsoft.Owin.Cors`

Mit diesem Befehl wird die Version 2.1.0 des Pakets zu Ihrem Projekt hinzugefügt.

### <a name="calling-usecors"></a>Aufrufen von UseCors

 Der folgende Codeausschnitt veranschaulicht, wie domänenübergreifende Verbindungen in SignalR 2 implementiert werden.

**Implementieren domänenübergreifender Anforderungen in SignalR 2**

Der folgende Code veranschaulicht, wie CORS oder JSONP in einem SignalR 2-Projekt aktiviert wird. In diesem `Map` Codebeispiel wird anstelle `RunSignalR` von verwendet, `MapSignalR`sodass die CORS-Middleware nur für die SignalR-Anforderungen `MapSignalR`ausgeführt wird, die CORS-Unterstützung erfordern (und nicht für den gesamten Datenverkehr an dem unter .) angegebenen Pfad. Map kann auch für jede andere Middleware verwendet werden, die für ein bestimmtes URL-Präfix ausgeführt werden muss, und nicht für die gesamte Anwendung.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - Legen Sie `jQuery.support.cors` in Ihrem Code nicht auf true fest.
>
>     ![Setzen Sie jQuery.support.cors nicht auf true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR übernimmt die Verwendung von CORS. Das `jQuery.support.cors` Festlegen auf true deaktiviert JSONP, da Es dazu führt, dass SignalR davon ausgeht, dass der Browser CORS unterstützt.
> - Wenn Sie eine Verbindung mit einer lokalen Host-URL herstellen, betrachtet Internet Explorer 10 dies nicht als domänenübergreifende Verbindung, sodass die Anwendung lokal mit IE 10 arbeitet, auch wenn Sie keine domänenübergreifenden Verbindungen auf dem Server aktiviert haben.
> - Informationen zur Verwendung domänenübergreifender Verbindungen mit Internet Explorer 9 finden Sie in [diesem StackOverflow-Thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).
> - Informationen zur Verwendung domänenübergreifender Verbindungen mit Chrome finden Sie in [diesem StackOverflow-Thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).
> - Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen. Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>So konfigurieren Sie die Verbindung

Bevor Sie eine Verbindung herstellen, können Sie Abfragezeichenfolgenparameter oder die Transportmethode angeben.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Angeben von Abfragezeichenfolgenparametern

Wenn Sie Daten an den Server senden möchten, wenn der Client eine Verbindung herstellt, können Sie dem Verbindungsobjekt Abfragezeichenfolgenparameter hinzufügen. Die folgenden Beispiele zeigen, wie Sie einen Abfragezeichenfolgenparameter im Clientcode festlegen.

**Festlegen eines Abfragezeichenfolgenwerts vor dem Aufruf der Startmethode (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Festlegen eines Abfragezeichenfolgenwerts vor dem Aufruf der startmethode (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

Das folgende Beispiel zeigt, wie sie einen Abfragezeichenfolgenparameter im Servercode lesen.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>So geben Sie die Transportmethode an

Im Rahmen der Verbindung verhandelt ein SignalR-Client normalerweise mit dem Server, um den besten Transport zu ermitteln, der sowohl vom Server als auch vom Client unterstützt wird. Wenn Sie bereits wissen, welchen Transport Sie verwenden möchten, können Sie diesen Aushandlungsprozess umgehen, indem Sie die Transportmethode angeben, wenn Sie die `start` Methode aufrufen.

**Clientcode, der die Transportmethode angibt (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**Clientcode, der die Transportmethode angibt (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

Alternativ können Sie mehrere Transportmethoden in der Reihenfolge angeben, in der SignalR sie ausprobieren soll:

**Clientcode, der ein benutzerdefiniertes Transport-Fallbackschema angibt (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Clientcode, der ein benutzerdefiniertes Transport-Fallbackschema angibt (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Sie können die folgenden Werte verwenden, um die Transportmethode anzugeben:

- "webSockets"
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

Die folgenden Beispiele zeigen, wie Sie herausfinden, welche Transportmethode von einer Verbindung verwendet wird.

**Clientcode, der die Transportmethode anzeigt, die von einer Verbindung (mit dem generierten Proxy) verwendet wird**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**Clientcode, der die transportische Methode anzeigt, die von einer Verbindung verwendet wird (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

Informationen zum Überprüfen der Transportmethode im Servercode finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context-Eigenschaft](hubs-api-guide-server.md#contextproperty). Weitere Informationen zu Transporten und Fallbacks finden Sie unter [Einführung in SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>So erhalten Sie einen Proxy für eine Hub-Klasse

Jedes Verbindungsobjekt, das Sie erstellen, kapselt Informationen über eine Verbindung mit einem SignalR-Dienst, der eine oder mehrere Hubklassen enthält. Um mit einer Hub-Klasse zu kommunizieren, verwenden Sie ein Proxyobjekt, das Sie selbst erstellen (wenn Sie den generierten Proxy nicht verwenden) oder das für Sie generiert wird.

Auf dem Client ist der Proxyname eine Kamel-Case-Version des Hub-Klassennamens. SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.

**Hub-Klasse auf dem Server**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**Abrufen eines Verweises auf den generierten Clientproxy für den Hub**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**Erstellen eines Clientproxys für die Hub-Klasse (ohne generierten Proxy)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

Wenn Sie Ihre Hub-Klasse `HubName` mit einem Attribut dekorieren, verwenden Sie den genauen Namen, ohne die Groß-/Kleinschreibung zu ändern.

**Hub-Klasse auf dem Server mit HubName-Attribut**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**Abrufen eines Verweises auf den generierten Clientproxy für den Hub**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**Erstellen eines Clientproxys für die Hub-Klasse (ohne generierten Proxy)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Definieren von Methoden auf dem Client, die der Server aufrufen kann

Um eine Methode zu definieren, die der Server von einem Hub aufrufen `client` kann, fügen Sie dem `on` Hub-Proxy mithilfe der Eigenschaft des generierten Proxys einen Ereignishandler hinzu, oder rufen Sie die Methode auf, wenn Sie den generierten Proxy nicht verwenden. Bei den Parametern kann es sich um komplexe Objekte handelt.

Fügen Sie den Ereignishandler `start` hinzu, bevor Sie die Methode zum Herstellen der Verbindung aufrufen. (Wenn Sie nach dem Aufruf der `start` Methode Ereignishandler hinzufügen möchten, lesen Sie die Anmerkung unter [Herstellen einer Verbindung](#establishconnection) weiter oben in diesem Dokument, und verwenden Sie die Syntax zum Definieren einer Methode, ohne den generierten Proxy zu verwenden.)

Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt. Auf dem `Clients.All.addContosoChatMessageToPage` Server wird `AddContosoChatMessageToPage`z. B. ausgeführt , `addContosoChatMessageToPage`, oder `addcontosochatmessagetopage` auf dem Client.

**Definieren der Methode auf dem Client (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**Alternative Methode auf Client (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**Definieren der Methode auf dem Client (ohne den generierten Proxy oder beim Hinzufügen nach dem Aufrufen der Startmethode)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**Servercode, der die Clientmethode aufruft**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

Die folgenden Beispiele enthalten ein komplexes Objekt als Methodenparameter.

**Definieren einer Methode auf dem Client, die ein komplexes Objekt (mit dem generierten Proxy) übernimmt**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**Definieren einer Methode auf dem Client, die ein komplexes Objekt übernimmt (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**Servercode, der das komplexe Objekt definiert**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**Servercode, der die Clientmethode mithilfe eines komplexen Objekts aufruft**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Aufrufen von Servermethoden vom Client

Um eine Servermethode vom Client `server` aufzurufen, verwenden Sie `invoke` die Eigenschaft des generierten Proxys oder die Methode auf dem Hub-Proxy, wenn Sie den generierten Proxy nicht verwenden. Der Rückgabewert oder die Parameter können komplexe Objekte sein.

Übergeben Sie eine Kamel-Fall-Version des Methodennamens auf dem Hub. SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.

Die folgenden Beispiele zeigen, wie eine Servermethode aufrufen wird, die keinen Rückgabewert hat, und wie eine Servermethode aufruft, die über einen Rückgabewert verfügt.

**Servermethode ohne HubMethodName-Attribut**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**Servercode, der das komplexe Objekt definiert, das in einem Parameter übergeben wird**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Wenn Sie die Hub-Methode mit einem `HubMethodName` Attribut versehen haben, verwenden Sie diesen Namen, ohne die Groß-/Kleinschreibung zu ändern.

**Servermethode** mit einem HubMethodName-Attribut

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

Die vorherigen Beispiele zeigen, wie eine Servermethode ohne Rückgabewert aufzurufen ist. Die folgenden Beispiele zeigen, wie eine Servermethode mit einem Rückgabewert aufruft.

**Servercode für eine Methode mit einem Rückgabewert**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

Die Für den Rückgabewert **verwendete Stock-Klasse**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**Clientcode, der die Servermethode aufruft (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**Clientcode, der die Servermethode aufruft (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Behandeln von Verbindungslebensdauerereignissen

SignalR stellt die folgenden Verbindungslebensdauerereignisse bereit, die Sie verarbeiten können:

- `starting`: Wird ausgelöst, bevor Daten über die Verbindung gesendet werden.
- `received`: Wird ausgelöst, wenn Daten über die Verbindung empfangen werden. Stellt die empfangenen Daten bereit.
- `connectionSlow`: Wird ausgelöst, wenn der Client eine langsame oder häufig abbrechende Verbindung erkennt.
- `reconnecting`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden wird.
- `reconnected`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden ist.
- `stateChanged`: Wird ausgelöst, wenn sich der Verbindungsstatus ändert. Stellt den alten und den neuen Status bereit (Verbinden, Verbinden, Erneute Verbindung oder Getrennt).
- `disconnected`: Wird ausgelöst, wenn die Verbindung getrennt wurde.

Wenn Sie z. B. Warnmeldungen anzeigen möchten, wenn Verbindungsprobleme `connectionSlow` auftreten, die zu spürbaren Verzögerungen führen können, behandeln Sie das Ereignis.

**Behandeln des connectionSlow-Ereignisses (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**Behandeln des connectionSlow-Ereignisses (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Umgang mit Fehlern

Der SignalR JavaScript-Client stellt ein `error` Ereignis bereit, für das Sie einen Handler hinzufügen können. Sie können die fail-Methode auch verwenden, um einen Handler für Fehler hinzuzufügen, die aus einem Servermethodenaufruf resultieren.

Wenn Sie detaillierte Fehlermeldungen auf dem Server nicht explizit aktivieren, enthält das Ausnahmeobjekt, das SignalR nach einem Fehler zurückgibt, minimale Informationen über den Fehler. Wenn z. B. `newContosoChatMessage` ein Aufruf von fehlschlägt,`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`enthält die Fehlermeldung im Fehlerobjekt " " Das Senden detaillierter Fehlermeldungen an Clients in der Produktion wird aus Sicherheitsgründen nicht empfohlen, aber wenn Sie detaillierte Fehlermeldungen zur Fehlerbehebung aktivieren möchten, verwenden Sie den folgenden Code auf dem Server.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

Das folgende Beispiel zeigt, wie Sie einen Handler für das Fehlerereignis hinzufügen.

**Hinzufügen eines Fehlerhandlers (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**Hinzufügen eines Fehlerhandlers (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

Das folgende Beispiel zeigt, wie ein Fehler aus einem Methodenaufruf behandelt wird.

**Behandeln eines Fehlers von einem Methodenaufruf (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**Behandeln eines Fehlers von einem Methodenaufruf (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Wenn ein Methodenaufruf fehlschlägt, wird das `error` Ereignis ebenfalls `error` ausgelöst, sodass der Code im Methodenhandler und im `.fail` Methodenrückruf ausgeführt wird.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>So aktivieren Sie die clientseitige Protokollierung

Um die clientseitige Protokollierung für `logging` eine Verbindung zu aktivieren, `start` legen Sie die Eigenschaft für das Verbindungsobjekt fest, bevor Sie die Methode zum Herstellen der Verbindung aufrufen.

**Protokollierung aktivieren (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**Protokollierung aktivieren (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Um die Protokolle anzuzeigen, öffnen Sie die Entwicklertools Ihres Browsers, und wechseln Sie zur Registerkarte Konsole. Ein Tutorial mit Schritt-für-Schritt-Anleitungen und Screenshots, die zeigen, wie Sie dies tun, finden Sie unter [ServerBroadcast mit ASP.NET Signalr - Anmelden aktivieren](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).
