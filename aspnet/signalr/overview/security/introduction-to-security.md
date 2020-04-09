---
uid: signalr/overview/security/introduction-to-security
title: Einführung in SignalR Security | Microsoft Docs
author: bradygaster
description: Beschreibt die Sicherheitsprobleme, die Sie beim Entwickeln einer SignalR-Anwendung berücksichtigen müssen.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675808"
---
# <a name="introduction-to-signalr-security"></a>Einführung in die Sicherheit von SignalR-Anwendungen

von [Patrick Fletcher](https://github.com/pfletcher), Tom [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> In diesem Artikel werden die Sicherheitsprobleme beschrieben, die Sie beim Entwickeln einer SignalR-Anwendung berücksichtigen müssen.
>
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

- [SignalR-Sicherheitskonzepte](#concepts)

    - [Authentifizierung und Autorisierung](#authentication)
    - [Verbindungstoken](#connectiontoken)
    - [Wiedereinschließen von Gruppen beim erneuten Herstellen einer Verbindung](#rejoingroup)
- [Wie SignalR standortübergreifende Anforderungsfälschung verhindert](#csrf)
- [SignalR-Sicherheitsempfehlungen](#recommendations)

    - [SSL-Protokoll (Secure Socket Layers)](#ssl)
    - [Verwenden Sie keine Gruppen als Sicherheitsmechanismus](#groupsecurity)
    - [Sicherer Umgang mit Eingaben von Clients](#input)
    - [Abgleichen einer Änderung des Benutzerstatus mit einer aktiven Verbindung](#reconcile)
    - [Automatisch generierte JavaScript-Proxydateien](#autogen)
    - [Ausnahmen](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR-Sicherheitskonzepte

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>Authentifizierung und Autorisierung

SignalR bietet keine Funktionen zum Authentifizieren von Benutzern. Stattdessen integrieren Sie die SignalR-Features in die vorhandene Authentifizierungsstruktur für eine Anwendung. Sie authentifizieren Benutzer wie normalerweise in Ihrer Anwendung und arbeiten mit den Ergebnissen der Authentifizierung in Ihrem SignalR-Code. Sie können Ihre Benutzer beispielsweise mit ASP.NET Formularauthentifizierung authentifizieren und dann in Ihrem Hub erzwingen, welche Benutzer oder Rollen zum Aufrufen einer Methode autorisiert sind. In Ihrem Hub können Sie auch Authentifizierungsinformationen, z. B. Dennamen oder ob ein Benutzer zu einer Rolle gehört, an den Client übergeben.

SignalR stellt das [Authorize-Attribut](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) bereit, um anzugeben, welche Benutzer Zugriff auf einen Hub oder eine Methode haben. Sie wenden das Authorize-Attribut entweder auf einen Hub oder bestimmte Methoden in einem Hub an. Ohne das Authorize-Attribut sind alle öffentlichen Methoden auf dem Hub für einen Client verfügbar, der mit dem Hub verbunden ist. Weitere Informationen zu Hubs finden Sie unter [Authentifizierung und Autorisierung für SignalR Hubs](hub-authorization.md).

Sie wenden `Authorize` das Attribut auf Hubs an, jedoch nicht auf persistente Verbindungen. Um Autorisierungsregeln bei `PersistentConnection` verwendung einer `AuthorizeRequest` zu erzwingen, müssen Sie die Methode überschreiben. Weitere Informationen zu persistenten Verbindungen finden Sie unter [Authentifizierung und Autorisierung für SignalR Persistent Connections](persistent-connection-authorization.md).

<a id="connectiontoken"></a>

### <a name="connection-token"></a>Verbindungstoken

SignalR verringert das Risiko der Ausführung bösartiger Befehle durch Überprüfung der Identität des Absenders. Für jede Anforderung übergeben Client und Server ein Verbindungstoken, das die Verbindungs-ID und den Benutzernamen für authentifizierte Benutzer enthält. Die Verbindungs-ID identifiziert eindeutig jeden verbundenen Client. Der Server generiert nach dem Zufallsprinzip die Verbindungs-ID, wenn eine neue Verbindung erstellt wird, und behält diese ID für die Dauer der Verbindung bei. Der Authentifizierungsmechanismus für die Webanwendung stellt den Benutzernamen bereit. SignalR verwendet Verschlüsselung und eine digitale Signatur, um das Verbindungstoken zu schützen.

![](introduction-to-security/_static/image2.png)

Für jede Anforderung überprüft der Server den Inhalt des Tokens, um sicherzustellen, dass die Anforderung vom angegebenen Benutzer stammt. Der Benutzername muss der Verbindungs-ID entsprechen. Durch die Überprüfung sowohl der Verbindungs-ID als auch des Benutzernamens verhindert SignalR, dass ein böswilliger Benutzer problemlos die Identität eines anderen Benutzers angibt. Wenn der Server das Verbindungstoken nicht überprüfen kann, schlägt die Anforderung fehl.

![](introduction-to-security/_static/image4.png)

Da die Verbindungs-ID Teil des Überprüfungsprozesses ist, sollten Sie die Verbindungs-ID eines Benutzers nicht anderen Benutzern anzeigen oder den Wert auf dem Client speichern, z. B. in einem Cookie.

#### <a name="connection-tokens-vs-other-token-types"></a>Verbindungstoken im Vergleich zu anderen Tokentypen

Verbindungstoken werden gelegentlich von Sicherheitstools gekennzeichnet, da sie Sitzungstoken oder Authentifizierungstoken zu sein scheinen, was ein Risiko darstellt, wenn sie verfügbar gemacht werden.

Das Verbindungstoken von SignalR ist kein Authentifizierungstoken. Es wird verwendet, um zu bestätigen, dass der Benutzer, der diese Anforderung stellt, derselbe ist, der die Verbindung erstellt hat. Das Verbindungstoken ist erforderlich, da ASP.NET SignalR die Verbindung zwischen Servern verschieben kann. Das Token ordnet die Verbindung einem bestimmten Benutzer zu, bestätigt jedoch nicht die Identität des Benutzers, der die Anforderung stellt. Damit eine SignalR-Anforderung ordnungsgemäß authentifiziert werden kann, muss sie über ein anderes Token verfügen, das die Identität des Benutzers bestätigt, z. B. ein Cookie oder ein Inhabertoken. Das Verbindungstoken selbst erhebt jedoch keinen Anspruch darauf, dass die Anforderung von diesem Benutzer gestellt wurde, sondern nur, dass die im Token enthaltene Verbindungs-ID diesem Benutzer zugeordnet ist.

Da das Verbindungstoken keinen eigenen Authentifizierungsanspruch bereitstellt, wird es nicht als "Sitzungstoken" oder "Authentifizierungstoken" betrachtet. Wenn Sie das Verbindungstoken eines bestimmten Benutzers übernehmen und in einer Anforderung wiedergeben, die als ein anderer Benutzer (oder eine nicht authentifizierte Anforderung) authentifiziert wurde, schlagen sie fehl, da die Benutzeridentität der Anforderung und die im Token gespeicherte Identität nicht übereinstimmen.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>Wiedereinschließen von Gruppen beim erneuten Herstellen einer Verbindung

Standardmäßig weist die SignalR-Anwendung einen Benutzer automatisch den entsprechenden Gruppen zu, wenn die Verbindung nach einer temporären Unterbrechung wiederhergestellt wird, z. B. wenn eine Verbindung abgebrochen und wieder hergestellt wird, bevor die Verbindung ausläuft. Beim erneuten Herstellen einer Verbindung übergibt der Client ein Gruppentoken, das die Verbindungs-ID und die zugewiesenen Gruppen enthält. Das Gruppentoken ist digital signiert und verschlüsselt. Der Client behält nach einer erneuten Verbindung dieselbe Verbindungs-ID bei. Daher muss die Verbindungs-ID, die vom wieder verbundenen Client übergeben wird, mit der vorherigen Verbindungs-ID übereinstimmen, die vom Client verwendet wird. Diese Überprüfung verhindert, dass ein böswilliger Benutzer Anforderungen an nicht autorisierte Gruppen weitergibt, wenn die Verbindung erneut hergestellt wird.

Es ist jedoch wichtig zu beachten, dass das Gruppentoken nicht abläuft. Wenn ein Benutzer in der Vergangenheit einer Gruppe angehörte, aber aus dieser Gruppe ausgeschlossen wurde, kann dieser Benutzer möglicherweise ein Gruppentoken imitieren, das die verbotene Gruppe enthält. Wenn Sie sicher verwalten müssen, welche Benutzer zu welchen Gruppen gehören, müssen Sie diese Daten auf dem Server speichern, z. B. in einer Datenbank. Fügen Sie dann der Anwendung Logik hinzu, die auf dem Server überprüft, ob ein Benutzer zu einer Gruppe gehört. Ein Beispiel für das Überprüfen der Gruppenmitgliedschaft finden Sie unter [Arbeiten mit Gruppen](../guide-to-the-api/working-with-groups.md).

Das automatische Wiedereintritt von Gruppen gilt nur, wenn eine Verbindung nach einer vorübergehenden Unterbrechung wieder hergestellt wird. Wenn ein Benutzer die Verbindung trennt, indem er von der Anwendung weg navigiert oder die Anwendung neu gestartet wird, muss die Anwendung damit umgehen, wie dieser Benutzer den richtigen Gruppen hinzugefügt wird. Weitere Informationen finden Sie unter [Arbeiten mit Gruppen](../guide-to-the-api/working-with-groups.md).

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>Wie SignalR standortübergreifende Anforderungsfälschung verhindert

Cross-Site Request Forgery (CSRF) ist ein Angriff, bei dem eine böswillige Website eine Anforderung an eine anfällige Site sendet, an der der Benutzer derzeit angemeldet ist. SignalR verhindert CSRF, da es für eine bösartige Website äußerst unwahrscheinlich ist, eine gültige Anforderung für Ihre SignalR-Anwendung zu erstellen.

### <a name="description-of-csrf-attack"></a>Beschreibung des CSRF-Angriffs

Hier ist ein Beispiel für einen CSRF-Angriff:

1. Ein Benutzer meldet sich mithilfe der Formularauthentifizierung bei www.example.com an.
2. Der Server authentifiziert den Benutzer. Die Antwort vom Server enthält ein Authentifizierungscookie.
3. Ohne sich abzumelden, besucht der Benutzer eine bösartige Website. Diese bösartige Website enthält das folgende HTML-Formular:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   Beachten Sie, dass die Formularaktion an die anfällige Website und nicht an die schädliche Website abfessetzt. Dies ist der "cross-site" Teil von CSRF.
4. Der Benutzer klickt auf die Schaltfläche "Absenden". Der Browser enthält das Authentifizierungscookie mit der Anforderung.
5. Die Anforderung wird auf dem example.com Server mit dem Authentifizierungskontext des Benutzers ausgeführt und kann alles tun, was ein authentifizierter Benutzer tun darf.

Obwohl in diesem Beispiel der Benutzer auf die Schaltfläche "Formular" klicken muss, kann die schädliche Seite genauso einfach ein Skript ausführen, das eine AJAX-Anforderung an Ihre SignalR-Anwendung sendet. Darüber hinaus verhindert die Verwendung von SSL einen CSRF-Angriff nicht, da die bösartige Website eine "https://"-Anforderung senden kann.

In der Regel sind CSRF-Angriffe auf Websites möglich, die Cookies für die Authentifizierung verwenden, da Browser alle relevanten Cookies an die Zielwebsite senden. CSRF-Angriffe beschränken sich jedoch nicht auf die Nutzung von Cookies. Beispielsweise sind die Basic- und Digest-Authentifizierung ebenfalls anfällig. Nachdem sich ein Benutzer mit der Standard- oder Digestauthentifizierung angemeldet hat, sendet der Browser die Anmeldeinformationen automatisch, bis die Sitzung endet.

### <a name="csrf-mitigations-taken-by-signalr"></a>CSRF-Abschwächungen von SignalR

SignalR führt die folgenden Schritte aus, um zu verhindern, dass eine schädliche Website gültige Anforderungen an Ihre Anwendung erstellt. SignalR führt diese Schritte standardmäßig aus, Sie müssen keine Aktionen in Ihrem Code ausführen.

- **Deaktivieren von domänenübergreifenden Anforderungen** SignalR deaktiviert domänenübergreifende Anforderungen, um zu verhindern, dass Benutzer einen SignalR-Endpunkt von einer externen Domäne aufrufen. SignalR betrachtet jede Anforderung von einer externen Domäne als ungültig und blockiert die Anforderung. Es wird empfohlen, dieses Standardverhalten beizubehalten. Andernfalls könnte eine bösartige Website Benutzer dazu verleiten, Befehle an Ihre Website zu senden. Informationen zum Einrichten einer domänenübergreifenden Verbindung finden Sie unter So stellen Sie [eine domänenübergreifende Verbindung her.](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)
- **Verbindungstoken in Abfragezeichenfolge übergeben, nicht in Cookie** SignalR übergibt das Verbindungstoken als Abfragezeichenfolgenwert und nicht als Cookie. Das Speichern des Verbindungstokens in einem Cookie ist unsicher, da der Browser das Verbindungstoken versehentlich weiterleiten kann, wenn bösartiger Code auftritt. Außerdem verhindert das Übergeben des Verbindungstokens in der Abfragezeichenfolge, dass das Verbindungstoken über die aktuelle Verbindung hinaus beibehalten wird. Daher kann ein böswilliger Benutzer keine Anforderung unter den Authentifizierungsanmeldeinformationen eines anderen Benutzers stellen.
- **Überprüfen des Verbindungstokens** Wie im Abschnitt [Verbindungstoken](#connectiontoken) beschrieben, weiß der Server, welche Verbindungs-ID jedem authentifizierten Benutzer zugeordnet ist. Der Server verarbeitet keine Anforderung von einer Verbindungs-ID, die nicht mit dem Benutzernamen übereinstimmt. Es ist unwahrscheinlich, dass ein böswilliger Benutzer eine gültige Anforderung erraten könnte, da der böswillige Benutzer den Benutzernamen und die aktuelle zufällig generierte Verbindungs-ID kennen müsste. Diese Verbindungs-ID wird ungültig, sobald die Verbindung beendet wird. Anonyme Benutzer sollten keinen Zugriff auf vertrauliche Informationen haben.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR-Sicherheitsempfehlungen

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>SSL-Protokoll (Secure Socket Layers)

Das SSL-Protokoll verwendet Verschlüsselung, um den Datentransport zwischen einem Client und einem Server zu sichern. Wenn Ihre SignalR-Anwendung vertrauliche Informationen zwischen Client und Server überträgt, verwenden Sie SSL für den Transport. Weitere Informationen zum Einrichten von SSL finden Sie unter [Einrichten von SSL auf IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>Verwenden Sie keine Gruppen als Sicherheitsmechanismus

Gruppen sind eine bequeme Möglichkeit, verwandte Benutzer zu sammeln, aber sie sind kein sicherer Mechanismus, um den Zugriff auf vertrauliche Informationen zu beschränken. Dies gilt insbesondere dann, wenn Benutzer während einer erneuten Verbindung automatisch wieder Gruppen beitreten können. Erwägen Sie stattdessen, einer Rolle privilegierte Benutzer hinzuzufügen und den Zugriff auf eine Hubmethode nur auf Mitglieder dieser Rolle zu beschränken. Ein Beispiel für das Einschränken des Zugriffs basierend auf einer Rolle finden Sie unter [Authentifizierung und Autorisierung für SignalR Hubs](hub-authorization.md). Ein Beispiel für das Überprüfen des Benutzerzugriffs auf Gruppen beim erneuten Herstellen einer Verbindung finden Sie unter [Arbeiten mit Gruppen](../guide-to-the-api/working-with-groups.md).

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>Sicherer Umgang mit Eingaben von Clients

Um sicherzustellen, dass ein böswilliger Benutzer kein Skript an andere Benutzer sendet, müssen Sie alle Eingaben von Clients codieren, die für die Übertragung an andere Clients vorgesehen sind. Sie sollten Nachrichten auf den empfangenden Clients und nicht auf dem Server codieren, da Ihre SignalR-Anwendung möglicherweise über viele verschiedene Clienttypen verfügt. Daher funktioniert die HTML-Codierung für einen Webclient, jedoch nicht für andere Clienttypen. Beispielsweise würde eine Webclientmethode zum Anzeigen einer Chatnachricht den Benutzernamen `html()` und die Nachricht sicher verarbeiten, indem sie die Funktion aufruft.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>Abgleichen einer Änderung des Benutzerstatus mit einer aktiven Verbindung

Wenn sich der Authentifizierungsstatus eines Benutzers ändert, während eine aktive Verbindung besteht, erhält der Benutzer eine Fehlermeldung mit der Meldung "Die Benutzeridentität kann sich während einer aktiven SignalR-Verbindung nicht ändern." In diesem Fall sollte Ihre Anwendung erneut eine Verbindung zum Server herstellen, um sicherzustellen, dass die Verbindungs-ID und der Benutzername koordiniert sind. Wenn Ihre Anwendung dem Benutzer beispielsweise das Abmelden ermöglicht, während eine aktive Verbindung besteht, stimmt der Benutzername für die Verbindung nicht mehr mit dem Namen überein, der für die nächste Anforderung übergeben wird. Sie sollten die Verbindung beenden, bevor sich der Benutzer abmeldet, und sie dann neu starten.

Es ist jedoch wichtig zu beachten, dass die meisten Anwendungen die Verbindung nicht manuell beenden und starten müssen. Wenn Ihre Anwendung Benutzer nach dem Abmelden auf eine separate Seite umleitet, z. B. das Standardverhalten in einer Web Forms-Anwendung oder MVC-Anwendung, oder die aktuelle Seite nach dem Abmelden aktualisiert, wird die aktive Verbindung automatisch getrennt und erfordert keine zusätzlichen Aktionen.

Das folgende Beispiel zeigt, wie Sie eine Verbindung beenden und starten, wenn sich der Benutzerstatus geändert hat.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

Oder der Authentifizierungsstatus des Benutzers kann sich ändern, wenn Ihre Website einen gleitenden Ablauf mit der Formularauthentifizierung verwendet und keine Aktivität zum Gültighalten des Authentifizierungscookies vorhanden ist. In diesem Fall wird der Benutzer abgemeldet, und der Benutzername stimmt nicht mehr mit dem Benutzernamen im Verbindungstoken überein. Sie können dieses Problem beheben, indem Sie ein Skript hinzufügen, das regelmäßig eine Ressource auf dem Webserver anfordert, um das Authentifizierungscookie gültig zu halten. Das folgende Beispiel zeigt, wie sie alle 30 Minuten eine Ressource anfordern.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>Automatisch generierte JavaScript-Proxydateien

Wenn Sie nicht alle Hubs und Methoden für jeden Benutzer in die JavaScript-Proxydatei aufnehmen möchten, können Sie die automatische Generierung der Datei deaktivieren. Sie können diese Option wählen, wenn Sie über mehrere Hubs und Methoden verfügen, aber nicht möchten, dass jeder Benutzer alle Methoden kennt. Sie deaktivieren die automatische Generierung, indem Sie **EnableJavaScriptProxies** auf **false**festlegen.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

Weitere Informationen zu den JavaScript-Proxydateien finden Sie unter [Der generierte Proxy und was er für Sie tut.](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) <a id="exceptions"></a>

### <a name="exceptions"></a>Ausnahmen

Sie sollten vermeiden, Ausnahmeobjekte an Clients weiterzugeben, da die Objekte vertrauliche Informationen für die Clients verfügbar machen können. Rufen Sie stattdessen eine Methode auf dem Client auf, die die entsprechende Fehlermeldung anzeigt.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
