---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR Hubs API Guide - .NET Client (C) | Microsoft Docs
author: bradygaster
description: Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in .NET-Clients wie Windows Store (WinRT), WPF, Silverlight und Cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675928"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR Hubs API Guide - .NET Client (C')

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Dieses Dokument enthält eine Einführung in die Verwendung der Hubs-API für SignalR-Version 2 in .NET-Clients wie Windows Store (WinRT), WPF, Silverlight und Konsolenanwendungen.
>
> Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen. Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden. Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden. SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.
>
> SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections. Eine Einführung in SignalR, Hubs und Persistent Connections oder ein Tutorial zum Erstellen einer vollständigen SignalR-Anwendung finden Sie unter [SignalR - Erste Schritte](../getting-started/index.md).
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

- [Client-Setup](#clientsetup)
- [So stellen Sie eine Verbindung her](#establishconnection)

    - [Domänenübergreifende Verbindungen von Silverlight-Clients](#slcrossdomain)
- [So konfigurieren Sie die Verbindung](#configureconnection)

    - [Festlegen der maximalen Anzahl gleichzeitiger Verbindungen in WPF-Clients](#maxconnections)
    - [Angeben von Abfragezeichenfolgenparametern](#querystring)
    - [So geben Sie die Transportmethode an](#transport)
    - [Angeben von HTTP-Headern](#httpheaders)
    - [Angeben von Clientzertifikaten](#clientcertificate)
- [Erstellen des Hub-Proxys](#proxy)
- [Definieren von Methoden auf dem Client, die der Server aufrufen kann](#callclient)

    - [Methoden ohne Parameter](#clientmethodswithoutparms)
    - [Methoden mit Parametern, Angabe von Parametertypen](#clientmethodswithparmtypes)
    - [Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter](#clientmethodswithdynamparms)
    - [So entfernen Sie einen Handler](#removehandler)
- [Aufrufen von Servermethoden vom Client](#callserver)
- [Behandeln von Verbindungslebensdauerereignissen](#connectionlifetime)
- [Umgang mit Fehlern](#handleerrors)
- [So aktivieren Sie die clientseitige Protokollierung](#logging)
- [WPF-, Silverlight- und Konsolenanwendungscodebeispiele für Clientmethoden, die der Server aufrufen kann](#wpfsl)

Ein Beispiel für .NET-Clientprojekte finden Sie unter den folgenden Ressourcen:

- [gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) auf GitHub.com (WinRT, Silverlight, Konsolen-App-Beispiele).
- [DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) auf GitHub.com (WPF-Beispiel).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) auf GitHub.com (Beispiel Konsolen-App).

Eine Dokumentation zum Programmieren des Servers oder der JavaScript-Clients finden Sie in den folgenden Ressourcen:

- [SignalR Hubs API Guide - Server](hubs-api-guide-server.md)
- [SignalR Hubs API-Handbuch - JavaScript-Client](hubs-api-guide-javascript-client.md)

Links zu API-Referenzthemen beziehen sich auf die .NET 4.5-Version der API. Wenn Sie .NET 4 verwenden, lesen Sie [die .NET 4-Version der API-Themen](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="clientsetup"></a>

## <a name="client-setup"></a>Clientsetup

Installieren Sie das [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet-Paket (nicht das [Microsoft.AspNet.SignalR-Paket).](http://nuget.org/packages/microsoft.aspnet.signalr) Dieses Paket unterstützt WinRT-, Silverlight-, WPF-, Konsolenanwendung und Windows Phone-Clients für .NET 4 und .NET 4.5.

Wenn sich die Version von SignalR auf dem Client von der Version auf dem Server unterscheidet, kann sich SignalR häufig an den Unterschied anpassen. Ein Server, auf dem SignalR Version 2 ausgeführt wird, unterstützt beispielsweise Clients, auf denen 1.1.x installiert ist, sowie Clients, auf denen Version 2 installiert ist. Wenn der Unterschied zwischen der Version auf dem Server und der Version auf dem Client zu groß `InvalidOperationException` ist oder wenn der Client neuer als der Server ist, löst SignalR eine Ausnahme aus, wenn der Client versucht, eine Verbindung herzustellen. Die Fehlermeldung lautet`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" ".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>So stellen Sie eine Verbindung her

Bevor Sie eine Verbindung herstellen können, `HubConnection` müssen Sie ein Objekt erstellen und einen Proxy erstellen. Um die Verbindung herzustellen, rufen Sie die `Start` Methode für das `HubConnection` Objekt auf.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> Für JavaScript-Clients müssen Sie mindestens einen Ereignishandler registrieren, bevor Sie die `Start` Methode aufrufen, um die Verbindung herzustellen. Dies ist für .NET-Clients nicht erforderlich. Für JavaScript-Clients erstellt der generierte Proxycode automatisch Proxys für alle Hubs, die auf dem Server vorhanden sind, und beim Registrieren eines Handlers geben Sie an, welche Hubs Ihr Client verwenden möchte. Für einen .NET-Client erstellen Sie Hub-Proxys jedoch manuell, daher geht SignalR davon aus, dass Sie einen hub verwenden, für den Sie einen Proxy erstellen.

Der Beispielcode verwendet die Standard-URL "/signalr", um eine Verbindung mit Ihrem SignalR-Dienst herzustellen. Informationen zum Angeben einer anderen Basis-URL finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).

Die `Start` Methode wird asynchron ausgeführt. Um sicherzustellen, dass nachfolgende Codezeilen erst ausgeführt werden, `await` nachdem die Verbindung hergestellt wurde, `.Wait()` verwenden Sie eine ASP.NET asynchrone Methode 4.5 oder eine synchrone Methode. Nicht in `.Wait()` einem WinRT-Client verwenden.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Domänenübergreifende Verbindungen von Silverlight-Clients

Informationen zum Aktivieren domänenübergreifender Verbindungen von Silverlight-Clients finden Sie unter [Verfügbarmachen eines Dienstes über Domänengrenzen](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)hinweg .

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>So konfigurieren Sie die Verbindung

Bevor Sie eine Verbindung herstellen, können Sie eine der folgenden Optionen angeben:

- Grenzwerte für gleichzeitige Verbindungen.
- Abfragezeichenfolgenparameter.
- Die Transportmethode.
- HTTP-Header.
- Clientzertifikate.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Festlegen der maximalen Anzahl gleichzeitiger Verbindungen in WPF-Clients

In WPF-Clients müssen Sie möglicherweise die maximale Anzahl gleichzeitiger Verbindungen von ihrem Standardwert 2 erhöhen. Der empfohlene Wert ist 10.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Weitere Informationen finden Sie unter [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Angeben von Abfragezeichenfolgenparametern

Wenn Sie Daten an den Server senden möchten, wenn der Client eine Verbindung herstellt, können Sie dem Verbindungsobjekt Abfragezeichenfolgenparameter hinzufügen. Das folgende Beispiel zeigt, wie ein Abfragezeichenfolgenparameter im Clientcode festgelegt wird.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

Das folgende Beispiel zeigt, wie sie einen Abfragezeichenfolgenparameter im Servercode lesen.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>So geben Sie die Transportmethode an

Im Rahmen der Verbindung verhandelt ein SignalR-Client normalerweise mit dem Server, um den besten Transport zu ermitteln, der sowohl vom Server als auch vom Client unterstützt wird. Wenn Sie bereits wissen, welchen Transport Sie verwenden möchten, können Sie diesen Aushandlungsprozess umgehen. Um die Transportmethode anzugeben, übergeben Sie ein Transportobjekt an die Start-Methode. Das folgende Beispiel zeigt, wie die Transportmethode im Clientcode angegeben wird.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

Der [Namespace Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) enthält die folgenden Klassen, die Sie zum Angeben des Transports verwenden können.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Verfügbar nur, wenn Server und Client .NET 4.5 verwenden.)
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Wählt automatisch den besten Transport aus, der sowohl vom Client als auch vom Server unterstützt wird. Dies ist der Standardtransport. Das Übergeben an `Start` die Methode hat den gleichen Effekt wie das Übergeben von nichts.)

Der ForeverFrame-Transport ist nicht in dieser Liste enthalten, da er nur von Browsern verwendet wird.

Informationen zum Überprüfen der Transportmethode im Servercode finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context-Eigenschaft](hubs-api-guide-server.md#contextproperty). Weitere Informationen zu Transporten und Fallbacks finden Sie unter [Einführung in SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Angeben von HTTP-Headern

Um HTTP-Header festzulegen, `Headers` verwenden Sie die Eigenschaft für das Verbindungsobjekt. Das folgende Beispiel zeigt, wie Sie einen HTTP-Header hinzufügen.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Angeben von Clientzertifikaten

Um Clientzertifikate hinzuzufügen, `AddClientCertificate` verwenden Sie die Methode für das Verbindungsobjekt.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Erstellen des Hub-Proxys

Um Methoden auf dem Client zu definieren, die ein Hub vom Server aufrufen kann, und um Methoden `CreateHubProxy` auf einem Hub auf dem Server aufzurufen, erstellen Sie einen Proxy für den Hub, indem Sie das Verbindungsobjekt aufrufen. Die Zeichenfolge, an `CreateHubProxy` die Sie übergeben werden, ist der `HubName` Name Ihrer Hub-Klasse oder der Name, der durch das Attribut angegeben wird, wenn eine Zeichenfolge auf dem Server verwendet wurde. Für die Namenszuordnung wird keine Groß-/Kleinschreibung berücksichtigt.

**Hub-Klasse auf dem Server**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Erstellen eines Clientproxys für die Hub-Klasse**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Wenn Sie Ihre Hub-Klasse `HubName` mit einem Attribut dekorieren, verwenden Sie diesen Namen.

**Hub-Klasse auf dem Server**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Erstellen eines Clientproxys für die Hub-Klasse**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Wenn Sie `HubConnection.CreateHubProxy` mehrmals mit `hubName`demselben aufrufen, erhalten `IHubProxy` Sie dasselbe zwischengespeicherte Objekt.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Definieren von Methoden auf dem Client, die der Server aufrufen kann

Um eine Methode zu definieren, die der `On` Server aufrufen kann, verwenden Sie die Methode des Proxys, um einen Ereignishandler zu registrieren.

Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt. Auf dem `Clients.All.UpdateStockPrice` Server wird `updateStockPrice`z. B. ausgeführt , `updatestockprice`, oder `UpdateStockPrice` auf dem Client.

Verschiedene Clientplattformen haben unterschiedliche Anforderungen für das Schreiben von Methodencode zum Aktualisieren der Benutzeroberfläche. Die gezeigten Beispiele beziehen sich auf WinRT-Clients (Windows Store .NET). Beispiele für WPF-, Silverlight- und Konsolenanwendungen werden [in einem separaten Abschnitt weiter unten in diesem Thema](#wpfsl)bereitgestellt.

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Methoden ohne Parameter

Wenn die Methode, die Sie behandeln, keine Parameter enthält, `On` verwenden Sie die nicht generische Überladung der Methode:

**Servercode, der clientmethod ohne Parameter aufruft**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**WinRT-Clientcode für eine Methode, die vom Server ohne Parameter aufgerufen wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Methoden mit Parametern, Angabe der Parametertypen

Wenn die Methode, die Sie behandeln, über Parameter verfügt, geben `On` Sie die Typen der Parameter als generische Typen der Methode an. Es gibt generische Überladungen der Methode, mit denen `On` Sie bis zu 8 Parameter angeben können (4 unter Windows Phone 7). Im folgenden Beispiel wird ein Parameter `UpdateStockPrice` an die Methode gesendet.

**Servercode, der die Clientmethode mit einem Parameter aufruft**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Die für den Parameter verwendete Stock-Klasse**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter

Alternativ zum Angeben von Parametern als `On` generische Typen der Methode können Sie Parameter als dynamische Objekte angeben:

**Servercode, der die Clientmethode mit einem Parameter aufruft**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Die für den Parameter verwendete Stock-Klasse**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**WinRT-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird[(siehe WPF- und Silverlight-Beispiele weiter unten in diesem Thema](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>So entfernen Sie einen Handler

Um einen Handler zu `Dispose` entfernen, rufen Sie seine Methode auf.

**Clientcode für eine vom Server aufgerufene Methode**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Clientcode zum Entfernen des Handlers**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Aufrufen von Servermethoden vom Client

Um eine Methode auf dem `Invoke` Server aufzurufen, verwenden Sie die Methode auf dem Hub-Proxy.

Wenn die Servermethode keinen Rückgabewert hat, verwenden Sie `Invoke` die nicht generische Überladung der Methode.

**Servercode für eine Methode ohne Rückgabewert**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Clientcode, der eine Methode aufruft, die keinen Rückgabewert hat**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Wenn die Servermethode über einen Rückgabewert verfügt, geben `Invoke` Sie den Rückgabetyp als generischen Typ der Methode an.

**Servercode für eine Methode, die einen Rückgabewert hat und einen komplexen Typparameter annimmt**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Die Für den Parameter und den Rückgabewert verwendete Stock-Klasse**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Clientcode, der eine Methode aufruft, die einen Rückgabewert hat und einen komplexen Typparameter annimmt, in einer ASP.NET 4.5-Async-Methode**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Clientcode, der eine Methode aufruft, die einen Rückgabewert hat und einen komplexen Typparameter annimmt, in einer synchronen Methode**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Die `Invoke` Methode wird asynchron ausgeführt `Task` und gibt ein Objekt zurück. Wenn Sie nicht `await` angeben `.Wait()`oder nicht , wird die nächste Codezeile ausgeführt, bevor die Methode, die Sie aufrufen, die Ausführung abgeschlossen hat.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Behandeln von Verbindungslebensdauerereignissen

SignalR stellt die folgenden Verbindungslebensdauerereignisse bereit, die Sie verarbeiten können:

- `Received`: Wird ausgelöst, wenn Daten über die Verbindung empfangen werden. Stellt die empfangenen Daten bereit.
- `ConnectionSlow`: Wird ausgelöst, wenn der Client eine langsame oder häufig abbrechende Verbindung erkennt.
- `Reconnecting`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden wird.
- `Reconnected`: Wird ausgelöst, wenn der zugrunde liegende Transport wieder verbunden ist.
- `StateChanged`: Wird ausgelöst, wenn sich der Verbindungsstatus ändert. Stellt den alten und den neuen Status bereit. Informationen zu Verbindungsstatuswerten finden Sie unter [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: Wird ausgelöst, wenn die Verbindung getrennt wurde.

Wenn Sie z. B. Warnmeldungen für Fehler anzeigen möchten, die nicht schwerwiegend sind, aber intermittierende Verbindungsprobleme verursachen, z. B. Langsamkeit oder häufiges Abbrechen der Verbindung, behandeln Sie das `ConnectionSlow` Ereignis.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Umgang mit Fehlern

Wenn Sie detaillierte Fehlermeldungen auf dem Server nicht explizit aktivieren, enthält das Ausnahmeobjekt, das SignalR nach einem Fehler zurückgibt, minimale Informationen über den Fehler. Wenn z. B. `newContosoChatMessage` ein Aufruf von fehlschlägt,`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`enthält die Fehlermeldung im Fehlerobjekt " " Das Senden detaillierter Fehlermeldungen an Clients in der Produktion wird aus Sicherheitsgründen nicht empfohlen, aber wenn Sie detaillierte Fehlermeldungen zur Fehlerbehebung aktivieren möchten, verwenden Sie den folgenden Code auf dem Server.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Um Fehler zu behandeln, die SignalR auslöst, können Sie einen Handler für das `Error` Ereignis für das Verbindungsobjekt hinzufügen.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Um Fehler aus Methodenaufrufen zu behandeln, umschließen Sie den Code in einem try-catch-Block.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>So aktivieren Sie die clientseitige Protokollierung

Um die clientseitige Protokollierung `TraceLevel` `TraceWriter` zu aktivieren, legen Sie die und eigenschaften für das Verbindungsobjekt fest.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>WPF-, Silverlight- und Konsolenanwendungscodebeispiele für Clientmethoden, die der Server aufrufen kann

Die zuvor gezeigten Codebeispiele zum Definieren von Clientmethoden, die der Server aufrufen kann, gelten für WinRT-Clients. Die folgenden Beispiele zeigen den entsprechenden Code für WPF-, Silverlight- und Konsolenanwendungsclients.

### <a name="methods-without-parameters"></a>Methoden ohne Parameter

**WPF-Clientcode für methode, die vom Server ohne Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Silverlight-Clientcode für methode, die vom Server ohne Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Konsolenanwendungsclientcode für Methode, die vom Server ohne Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Methoden mit Parametern, Angabe der Parametertypen

**WPF-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Silverlight-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Konsolenanwendungsclientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Methoden mit Parametern, Angabe dynamischer Objekte für die Parameter

**WPF-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Silverlight-Clientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Konsolenanwendungsclientcode für eine Methode, die vom Server mit einem Parameter aufgerufen wird, wobei ein dynamisches Objekt für den Parameter verwendet wird**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
