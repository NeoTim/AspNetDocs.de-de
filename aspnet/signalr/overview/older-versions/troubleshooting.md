---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR Fehlerbehebung (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: In diesem Artikel werden häufige Probleme bei der Entwicklung von SignalR-Anwendungen beschrieben.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543092"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>Problembehandlung für SignalR (SignalR 1.x)

von [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> In diesem Dokument werden häufige Probleme bei der Problembehandlung mit SignalR beschrieben.

Dieses Dokument enthält die folgenden Abschnitte.

- [Aufrufmethoden zwischen Client und Server fehlschlägt im Hintergrund](#connection)
- [Andere Verbindungsprobleme](#other)
- [Kompilierung und serverseitige Fehler](#server)
- [Visual Studio-Probleme](#vs)
- [Probleme mit Internetinformationsdiensten](#iis)
- [Azure-Probleme](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>Aufrufmethoden zwischen Client und Server fehlschlägt im Hintergrund

In diesem Abschnitt werden mögliche Ursachen für einen Methodenaufruf zwischen Client und Server beschrieben, der ohne aussagekräftige Fehlermeldung fehlschlägt. In einer SignalR-Anwendung verfügt der Server über keine Informationen über die Methoden, die der Client implementiert. Wenn der Server eine Clientmethode aufruft, werden der Methodenname und die Parameterdaten an den Client gesendet, und die Methode wird nur ausgeführt, wenn sie in dem vom Server angegebenen Format vorhanden ist. Wenn auf dem Client keine übereinstimmende Methode gefunden wird, geschieht nichts, und es wird keine Fehlermeldung auf dem Server ausgelöst.

Um Clientmethoden, die nicht aufgerufen werden, weiter zu untersuchen, können Sie die Protokollierung aktivieren, bevor Sie die Startmethode auf dem Hub aufrufen, um zu sehen, welche Aufrufe vom Server kommen. Informationen zum Aktivieren der Protokollierung in einer JavaScript-Anwendung finden Sie unter Aktivieren der [clientseitigen Protokollierung (JavaScript-Clientversion)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging). Informationen zum Aktivieren der Protokollierung in einer .NET-Clientanwendung finden Sie unter Aktivieren der [clientseitigen Protokollierung (.NET Client-Version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Falsch geschriebene Methode, falsche Methodensignatur oder falscher Hubname

Wenn der Name oder die Signatur einer aufgerufenen Methode nicht genau mit einer geeigneten Methode auf dem Client übereinstimmt, schlägt der Aufruf fehl. Stellen Sie sicher, dass der vom Server aufgerufene Methodenname mit dem Namen der Methode auf dem Client übereinstimmt. Außerdem erstellt SignalR den Hub-Proxy mithilfe von Camel-Cased-Methoden, wie `SendMessage` es in JavaScript angebracht ist, sodass eine auf dem Server aufgerufene Methode im Clientproxy aufgerufen `sendMessage` wird. Wenn Sie `HubName` das Attribut in Ihrem serverseitigen Code verwenden, stellen Sie sicher, dass der verwendete Name mit dem Namen übereinstimmt, der zum Erstellen des Hubs auf dem Client verwendet wird. Wenn Sie das `HubName` Attribut nicht verwenden, stellen Sie sicher, dass der Name des Hubs in einem JavaScript-Client Kamel-Cased ist, z. B. ChatHub anstelle von ChatHub.

### <a name="duplicate-method-name-on-client"></a>Doppelte Methodenname auf dem Client

Stellen Sie sicher, dass sie keine doppelte Methode auf dem Client haben, die sich nur von Fall zu Großundhälter unterscheidet. Wenn Ihre Clientanwendung über `sendMessage`eine Methode namens verfügt, stellen `SendMessage` Sie sicher, dass nicht auch eine Methode aufgerufen wird.

### <a name="missing-json-parser-on-the-client"></a>Fehlender JSON-Parser auf dem Client

SignalR erfordert, dass ein JSON-Parser vorhanden ist, um Aufrufe zwischen dem Server und dem Client zu serialisieren. Wenn Ihr Client nicht über einen integrierten JSON-Parser (z. B. Internet Explorer 7) verfügt, müssen Sie einen in Ihre Anwendung aufnehmen. Sie können den JSON-Parser [hier](http://nuget.org/packages/json2)herunterladen.

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Mixing Hub- und PersistentConnection-Syntax

SignalR verwendet zwei Kommunikationsmodelle: Hubs und PersistentConnections. Die Syntax zum Aufrufen dieser beiden Kommunikationsmodelle unterscheidet sich im Clientcode. Wenn Sie dem Servercode einen Hub hinzugefügt haben, stellen Sie sicher, dass der gesamte Clientcode die richtige Hubsyntax verwendet.

**JavaScript-Clientcode, der eine PersistentConnection in einem JavaScript-Client erstellt**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**JavaScript-Clientcode, der einen Hubproxy in einem Javascript-Client erstellt**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**Servercode mit dem Server code, der eine Route einer PersistentConnection zuordnet**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**Servercode, der eine Route einem Hub oder mehreren Hubs zuordnet, wenn Sie über mehrere Anwendungen verfügen**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>Verbindung gestartet, bevor Abonnements hinzugefügt werden

Wenn die Verbindung des Hubs gestartet wird, bevor dem Proxy Methoden hinzugefügt werden, die vom Server aufgerufen werden können, werden keine Nachrichten empfangen. Der folgende JavaScript-Code startet den Hub nicht ordnungsgemäß:

**Falscher JavaScript-Clientcode, der den Empfangen von Hubs-Nachrichten nicht zulässt**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Fügen Sie stattdessen die Methodenabonnements hinzu, bevor Sie Start aufrufen:

**JavaScript-Clientcode, der einem Hub ordnungsgemäß Abonnements hinzufügt**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Fehlender Methodenname auf dem Hubproxy

Stellen Sie sicher, dass die auf dem Server definierte Methode auf dem Client abonniert ist. Obwohl der Server die Methode definiert, muss sie dennoch dem Clientproxy hinzugefügt werden. Methoden können dem Clientproxy auf folgende Weise hinzugefügt werden (Beachten `client` Sie, dass die Methode dem Member des Hubs hinzugefügt wird, nicht dem Hub direkt):

**JavaScript-Clientcode, der einem Hubproxy Methoden hinzufügt**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Hub- oder Hubmethoden, die nicht als Öffentlich deklariert wurden

Um auf dem Client sichtbar zu sein, müssen `public`die Hubimplementierung und -methoden als deklariert werden.

### <a name="accessing-hub-from-a-different-application"></a>Zugreifen auf Hub von einer anderen Anwendung aus

Auf SignalR Hubs kann nur über Anwendungen zugegriffen werden, die SignalR-Clients implementieren. SignalR kann nicht mit anderen Kommunikationsbibliotheken (z. B. SOAP- oder WCF-Webdiensten) zusammenarbeiten. Wenn für Ihre Zielplattform kein SignalR-Client verfügbar ist, können Sie nicht direkt auf den Endpunkt des Servers zugreifen.

### <a name="manually-serializing-data"></a>Manuelle sserialisierende Daten

SignalR verwendet AUTOMATISCH JSON, um Ihre Methodenparameter zu serialisieren – es gibt keine Notwendigkeit, es selbst zu tun.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Remote Hub-Methode wird auf Client in OnDisconnected-Funktion nicht ausgeführt

Dieses Verhalten ist beabsichtigt. Wenn `OnDisconnected` aufgerufen wird, ist der `Disconnected` Hub bereits in den Zustand eingetreten, wodurch keine weiteren Hubmethoden aufgerufen werden können.

**Servercode, der Code im OnDisconnected-Ereignis korrekt ausführt**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>Verbindungslimit erreicht

Wenn Sie die Vollversion von IIS auf einem Clientbetriebssystem wie Windows 7 verwenden, wird ein Limit von 10 Verbindungen festgelegt. Verwenden Sie bei Verwendung eines Clientbetriebssystems stattdessen IIS Express, um dieses Limit zu vermeiden.

### <a name="cross-domain-connection-not-set-up-properly"></a>Domänenübergreifende Verbindung nicht ordnungsgemäß eingerichtet

Wenn eine domänenübergreifende Verbindung (eine Verbindung, für die sich die SignalR-URL nicht in derselben Domäne wie die Hostingseite befindet) nicht ordnungsgemäß eingerichtet ist, schlägt die Verbindung möglicherweise ohne Fehlermeldung fehl. Informationen zum Aktivieren der domänenübergreifenden Kommunikation finden Sie unter [Einrichten einer domänenübergreifenden Verbindung](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>Verbindung mit NTLM (Active Directory) funktioniert nicht in .NET Client

Eine Verbindung in einer .NET-Clientanwendung, die Domänensicherheit verwendet, schlägt möglicherweise fehl, wenn die Verbindung nicht ordnungsgemäß konfiguriert ist. Um SignalR in einer Domänenumgebung zu verwenden, legen Sie die erforderliche Verbindungseigenschaft wie folgt fest:

**Clientcode für den C-Client, der Verbindungsanmeldeinformationen implementiert**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>Andere Verbindungsprobleme

In diesem Abschnitt werden die Ursachen und Lösungen für bestimmte Symptome oder Fehlermeldungen beschrieben, die während einer Verbindung auftreten.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>Fehler "Start muss aufgerufen werden, bevor Daten gesendet werden können"

Dieser Fehler tritt häufig auf, wenn Code auf SignalR-Objekte verweist, bevor die Verbindung gestartet wird. Das Wireup für Handler und dergleichen, die auf dem Server definierte Methoden aufrufen, muss nach Abschluss der Verbindung hinzugefügt werden. Beachten Sie, `Start` dass der Aufruf asynchron ist, sodass Code nach dem Aufruf ausgeführt werden kann, bevor er abgeschlossen wird. Die beste Möglichkeit, Handler hinzuzufügen, nachdem eine Verbindung vollständig gestartet wurde, besteht darin, sie in eine Rückruffunktion zu setzen, die als Parameter an die start-Methode übergeben wird:

**JavaScript-Clientcode, der Ereignishandler korrekt hinzufügt, die auf SignalR-Objekte verweisen**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Dieser Fehler wird auch angezeigt, wenn eine Verbindung beendet wird, während SignalR-Objekte noch referenziert werden.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>Fehler "301 dauerhaft verschoben" oder "302 vorübergehend verschoben"

Dieser Fehler kann angezeigt werden, wenn das Projekt einen Ordner namens SignalR enthält, der den automatisch erstellten Proxy beeinträchtigt. Um diesen Fehler zu vermeiden, `SignalR` verwenden Sie keinen Ordner, der in Ihrer Anwendung aufgerufen wird, oder deaktivieren Sie die automatische Proxygenerierung. Weitere Informationen finden Sie unter [Der generierte Proxy und weitere Informationen dazu.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>"403 Forbidden"-Fehler in .NET- oder Silverlight-Client

Dieser Fehler kann in domänenübergreifenden Umgebungen auftreten, in denen die domänenübergreifende Kommunikation nicht ordnungsgemäß aktiviert ist. Informationen zum Aktivieren der domänenübergreifenden Kommunikation finden Sie unter [Einrichten einer domänenübergreifenden Verbindung](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Informationen zum Herstellen einer domänenübergreifenden Verbindung in einem Silverlight-Client finden Sie unter [Domänenübergreifende Verbindungen von Silverlight-Clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>Fehler "404 Nicht gefunden"

Es gibt mehrere Ursachen für dieses Problem. Überprüfen Sie alle folgenden Punkte:

- **Hubproxy-Adressverweis nicht korrekt formatiert:** Dieser Fehler tritt häufig auf, wenn der Verweis auf die generierte Hubproxyadresse nicht korrekt formatiert ist. Stellen Sie sicher, dass der Verweis auf die Hubadresse ordnungsgemäß vorgenommen wurde. Weitere Informationen finden Sie unter [Verweisen auf den dynamisch generierten Proxy.](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)
- **Hinzufügen von Routen zur Anwendung vor dem Hinzufügen der Hubroute:** Wenn Ihre Anwendung andere Routen verwendet, stellen Sie `MapHubs`sicher, dass die erste hinzugefügte Route der Aufruf von ist.

### <a name="500-internal-server-error"></a>"500 Interner Serverfehler"

Dies ist ein sehr generischer Fehler, der eine Vielzahl von Ursachen haben könnte. Die Details des Fehlers sollten im Ereignisprotokoll des Servers angezeigt werden oder über das Debuggen des Servers gefunden werden. Detailliertere Fehlerinformationen können durch Aktivieren detaillierter Fehler auf dem Server abgerufen werden. Weitere Informationen finden Sie unter [Behandeln von Fehlern in der Hub-Klasse](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>Fehler &lt;"TypeError:&gt; hubType ist nicht definiert"

Dieser Fehler tritt auf, `MapHubs` wenn der Aufruf nicht ordnungsgemäß erfolgt. Weitere Informationen finden Sie unter [Registrieren der SignalR-Route und Konfigurieren von SignalR-Optionen.](../guide-to-the-api/hubs-api-guide-server.md#route)

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException wurde vom Benutzercode nicht behandelt

Stellen Sie sicher, dass die Parameter, die Sie an Ihre Methoden senden, keine nicht serialisierbaren Typen (z. B. Dateihandles oder Datenbankverbindungen) enthalten. Wenn Sie Member für ein serverseitiges Objekt verwenden müssen, das nicht an den Client gesendet werden soll `JSONIgnore` (entweder aus Sicherheitsgründen oder aus Gründen der Serialisierung), verwenden Sie das Attribut.

### <a name="protocol-error-unknown-transport-error"></a>Fehler "Protokollfehler: Unbekannter Transport"

Dieser Fehler kann auftreten, wenn der Client die von SignalR verwendeten Transporte nicht unterstützt. Informationen dazu, welche Browser mit SignalR verwendet werden können, finden Sie unter [Transporte und Fallbacks.](../getting-started/introduction-to-signalr.md#transports)

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"Die JavaScript Hub-Proxygenerierung wurde deaktiviert."

Dieser Fehler tritt `DisableJavaScriptProxies` auf, wenn festgelegt wird, während `signalr/hubs`auch ein Verweis auf den dynamisch generierten Proxy bei enthält. Weitere Informationen zum manuellen Erstellen des Proxys finden Sie unter [Der generierte Proxy und was er für Sie tut.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"Die Verbindungs-ID ist im falschen Format" oder "Die Benutzeridentität kann sich während einer aktiven SignalR-Verbindung nicht ändern" Fehler

Dieser Fehler kann angezeigt werden, wenn die Authentifizierung verwendet wird und der Client abgemeldet wird, bevor die Verbindung beendet wird. Die Lösung besteht darin, die SignalR-Verbindung zu beenden, bevor der Client protokolliert wird.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Uncaught Error: SignalR: jQuery nicht gefunden. Stellen Sie sicher, dass auf jQuery vor dem SignalR.js-Dateifehler verwiesen wird.

Der SignalR JavaScript-Client erfordert die Ausführung von jQuery. Stellen Sie sicher, dass Ihr Verweis auf jQuery korrekt ist, dass der verwendete Pfad gültig ist und dass der Verweis auf jQuery vor dem Verweis auf SignalR liegt.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>Fehler "Uncaught TypeError:&lt;Cannot&gt;read property ' property ' of undefined"

Dieser Fehler resultiert, dass jQuery oder der Hubs-Proxy nicht ordnungsgemäß referenziert wurde. Stellen Sie sicher, dass Ihr Verweis auf jQuery und den Hubs-Proxy korrekt ist, dass der verwendete Pfad gültig ist und dass der Verweis auf jQuery vor dem Verweis auf den Hubs-Proxy liegt. Der Standardverweis auf den Hubs-Proxy sollte wie folgt aussehen:

**HTML-Client-side-Code, der korrekt auf den Hubs-Proxy verweist**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>Fehler "RuntimeBinderException wurde vom Benutzercode nicht behandelt"

Dieser Fehler kann auftreten, wenn `Hub.On` die falsche Überladung von verwendet wird. Wenn die Methode einen Rückgabewert hat, muss der Rückgabetyp als generischer Typparameter angegeben werden:

**Auf dem Client definierte Methode (ohne generierten Proxy)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>Verbindungs-ID ist inkonsistent oder Verbindungsunterbrechungen zwischen Seitenladevorgängen

Dieses Verhalten ist beabsichtigt. Da das Hubobjekt im Seitenobjekt gehostet wird, wird der Hub beim Aktualisieren der Seite zerstört. Eine mehrseitige Anwendung muss die Zuordnung zwischen Benutzern und Verbindungs-IDs beibehalten, damit sie zwischen Seitenladevorgängen konsistent sind. Die Verbindungs-IDs können auf dem `ConcurrentDictionary` Server entweder in einem Objekt oder in einer Datenbank gespeichert werden.

### <a name="value-cannot-be-null-error"></a>Fehler "Wert kann nicht null sein"

Serverseitige Methoden mit optionalen Parametern werden derzeit nicht unterstützt. Wenn der optionale Parameter weggelassen wird, schlägt die Methode fehl. Weitere Informationen finden Sie unter [Optionale Parameter](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox kann keine Verbindung zum Server &lt;&gt;unter Adresse herstellen " Fehler in Firebug

Diese Fehlermeldung kann in Firebug angezeigt werden, wenn die Aushandlung des WebSocket-Transports fehlschlägt und stattdessen ein anderer Transport verwendet wird. Dieses Verhalten ist beabsichtigt.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>Fehler "Das Remotezertifikat ist gemäß dem Validierungsverfahren ungültig" in der .NET-Clientanwendung

Wenn Ihr Server benutzerdefinierte Clientzertifikate benötigt, können Sie der Verbindung ein x509-Zertifikat hinzufügen, bevor die Anforderung gestellt wird. Fügen Sie das Zertifikat `Connection.AddClientCertificate`der Verbindung mithilfe von hinzu.

### <a name="connection-drops-after-authentication-times-out"></a>Verbindung fällt nach Demauthentifizierungszeit

Dieses Verhalten ist beabsichtigt. Authentifizierungsanmeldeinformationen können nicht geändert werden, während eine Verbindung aktiv ist. Um Anmeldeinformationen zu aktualisieren, muss die Verbindung beendet und neu gestartet werden.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected wird zweimal aufgerufen, wenn jQuery Mobile verwendet wird

Die Funktion von `initializePage` jQuery Mobile erzwingt die erneute Ausführung der Skripts auf jeder Seite und erstellt so eine zweite Verbindung. Zu den Lösungen für dieses Problem gehören:

- Fügen Sie den Verweis auf jQuery Mobile vor Ihrer JavaScript-Datei ein.
- Deaktivieren `initializePage` Sie die `$.mobile.autoInitializePage = false`Funktion, indem Sie .
- Warten Sie, bis die Initialisierung der Seite abgeschlossen ist, bevor Sie die Verbindung starten.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Nachrichten werden in Silverlight-Anwendungen mithilfe von Server-Gesendeten Ereignissen verzögert

Nachrichten werden verzögert, wenn Server-gesendete Ereignisse auf Silverlight verwendet werden. Um stattdessen die Verwendung langer Abfragen zu erzwingen, verwenden Sie beim Starten der Verbindung Folgendes:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>"Berechtigung verweigert" mit Forever Frame-Protokoll

Dies ist ein bekanntes Problem, [das hier](https://github.com/SignalR/SignalR/issues/1963)beschrieben wird. Dieses Symptom kann mit der neuesten JQuery-Bibliothek angezeigt werden. Die Problemumgehung besteht darin, Ihre Anwendung auf JQuery 1.8.2 herabzustufen.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Kompilierung und serverseitige Fehler

 Der folgende Abschnitt enthält mögliche Lösungen für Compiler- und serverseitige Laufzeitfehler. 

### <a name="reference-to-hub-instance-is-null"></a>Verweis auf Hub-Instanz ist null

Da für jede Verbindung eine Hubinstanz erstellt wird, können Sie selbst keine Instanz eines Hubs in Ihrem Code erstellen. Informationen zum Aufrufen von Methoden für einen Hub von außerhalb des Hubs selbst finden Sie unter [Aufrufen von Clientmethoden und Verwalten von Gruppen von außerhalb der Hubklasse,](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) um einen Verweis auf den Hubkontext zu erhalten.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session ist null

Dieses Verhalten ist beabsichtigt. SignalR unterstützt den ASP.NET Sitzungsstatus nicht, da das Aktivieren des Sitzungsstatus die Duplex-Messaging unterbrechen würde.

### <a name="no-suitable-method-to-override"></a>Keine geeignete Methode zum Überschreiben

Dieser Fehler wird möglicherweise angezeigt, wenn Sie Code aus älteren Dokumentationen oder Blogs verwenden. Stellen Sie sicher, dass Sie nicht auf Namen von Methoden verweisen, die geändert oder veraltet wurden (z. `OnConnectedAsync`B. ).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions.WebSocketServerUrl ist null

Dieses Verhalten ist beabsichtigt. Dieser Member ist veraltet und sollte nicht verwendet werden.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>Fehler "Eine Route mit dem Namen 'signalr.hubs' ist bereits in der Routensammlung vorhanden"

Dieser Fehler wird `MapHubs` angezeigt, wenn sie zweimal von Ihrer Anwendung aufgerufen wird. Einige Beispielanwendungen `MapHubs` rufen direkt in der globalen Anwendungsdatei auf. andere rufen in einer Wrapperklasse auf. Stellen Sie sicher, dass Ihre Anwendung nicht beides tut.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio-Probleme

In diesem Abschnitt werden Probleme beschrieben, die in Visual Studio aufgetreten sind.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Skriptdokumentknoten wird nicht im Projektmappen-Explorer angezeigt

Einige unserer Tutorials leiten Sie während des Debuggens zum Knoten "Skriptdokumente" im Projektmappen-Explorer. Dieser Knoten wird vom JavaScript-Debugger erstellt und wird nur beim Debuggen von Browserclients in Internet Explorer angezeigt. Der Knoten wird nicht angezeigt, wenn Chrome oder Firefox verwendet werden. Der JavaScript-Debugger wird auch nicht ausgeführt, wenn ein anderer Clientdebugger ausgeführt wird, z. B. der Silverlight-Debugger.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR funktioniert nicht auf Visual Studio 2008 oder früher

Dieses Verhalten ist beabsichtigt. SignalR erfordert .NET Framework 4 oder höher; Dies erfordert, dass SignalR-Anwendungen in Visual Studio 2010 oder höher entwickelt werden.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS-Probleme

Dieser Abschnitt enthält Probleme mit Internetinformationsdiensten.

### <a name="web-site-crashes-after-maphubs-call"></a>Website stürzt nach MapHubs-Aufruf ab

Dieses Problem wurde in der neuesten Version von SignalR behoben. Stellen Sie sicher, dass Sie die neueste version von SignalR verwenden, indem Sie Ihre Installation mit NuGet aktualisieren.

<a id="azure"></a>

## <a name="azure-issues"></a>Azure-Probleme

Dieser Abschnitt enthält Probleme mit Microsoft Azure.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Nachrichten werden nicht über die Azure-Backebene empfangen, nachdem die Themennamen geändert wurden.

Die von der Azure-Backplane verwendeten Themen sind nicht benutzerkonfigurierbar.
