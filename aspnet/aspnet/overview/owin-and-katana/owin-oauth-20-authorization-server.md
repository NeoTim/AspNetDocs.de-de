---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 Autorisierungsserver | Microsoft Docs
author: hongyes
description: In diesem Tutorial erfahren Sie, wie Sie einen OAuth 2.0 Authorization Server mit OWIN OAuth-Middleware implementieren. Dies ist ein erweitertes Tutorial, das nur outlin...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540399"
---
<a name="owin-oauth-20-authorization-server"></a>OWIN-OAuth 2.0-Autorisierungsserver
====================
von [Hongye Sun](https://github.com/hongyes) und [Praburaj Thiagarajan](https://github.com/Praburaj)

> In diesem Tutorial erfahren Sie, wie Sie einen OAuth 2.0 Authorization Server mit OWIN OAuth-Middleware implementieren. Dies ist ein erweitertes Tutorial, das nur die Schritte zum Erstellen eines OWIN OAuth 2.0 Autorisierungsservers beschreibt. Dies ist kein Schritt-für-Schritt-Tutorial. [Laden Sie den Beispielcode herunter.](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)
>
> > [!NOTE]
> > Diese Gliederung sollte nicht zum Erstellen einer sicheren Produktions-App verwendet werden. Dieses Tutorial soll nur eine Übersicht darüber enthalten, wie ein OAuth 2.0 Authorization Server mit OWIN OAuth Middleware implementiert wird.
>
>
> ## <a name="software-versions"></a>Softwareversionen
>
> | **Im Tutorial gezeigt** | **Funktioniert auch mit** |
> | --- | --- |
> | Windows 8.1 | Windows 8, Windows 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [Visual Studio 2013 Express für Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). Visual Studio 2012 mit dem neuesten Update sollte funktionieren, aber das Tutorial wurde nicht damit getestet, und einige Menüauswahlen und Dialogfelder unterscheiden sich. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
>
> Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie diese bei [Katana Project auf GitHub](https://github.com/aspnet/AspNetKatana/)veröffentlichen. Fragen und Kommentare zum Tutorial selbst finden Sie im Kommentarbereich am unteren Rand der Seite.


Das [OAuth 2.0-Framework](http://tools.ietf.org/html/rfc6749) ermöglicht es einer Drittanbieter-App, eingeschränkten Zugriff auf einen HTTP-Dienst zu erhalten. Anstatt die Anmeldeinformationen des Ressourcenbesitzers für den Zugriff auf eine geschützte Ressource zu verwenden, ruft der Client ein Zugriffstoken ab (eine Zeichenfolge, die einen bestimmten Bereich, eine bestimmte Lebensdauer und andere Zugriffsattribute angibt). Zugriffstoken werden von einem Autorisierungsserver mit Genehmigung des Ressourcenbesitzers an Clients von Drittanbietern ausgestellt.

Dieses Tutorial behandelt:

- So erstellen Sie einen Autorisierungsserver, um vier Autorisierungserteilungstypen und Aktualisierungstoken zu unterstützen:
    - Autorisierungscodeerteilung
    - Implizite Zuscheine
    - Resource Owner Password Credentials Grant
    - Clientcredentials Grant
- Erstellen eines Ressourcenservers, der durch ein Zugriffstoken geschützt ist.
- Erstellen von OAuth 2.0-Clients.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Voraussetzungen

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) oder das kostenlose [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), wie in **Softwareversionen** oben auf der Seite angegeben.
- Vertrautheit mit OWIN. Weitere Informationen finden Sie unter [Erste Schritte mit dem Katana-Projekt](https://msdn.microsoft.com/magazine/dn451439.aspx) und [Neuerungen in OWIN und Katana](index.md).
- Vertrautheit mit [OAuth-Terminologie,](http://tools.ietf.org/html/rfc6749) einschließlich [Rollen](http://tools.ietf.org/html/rfc6749#section-1.1), [Protokollfluss](http://tools.ietf.org/html/rfc6749#section-1.2)und [Autorisierungserteilung](http://tools.ietf.org/html/rfc6749#section-1.3). Die Einführung von [OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-1) bietet eine gute Einführung.

## <a name="create-an-authorization-server"></a>Erstellen eines Autorisierungsservers

In diesem Tutorial wird grob skizziert, wie [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) und ASP.NET MVC verwendet werden, um einen Autorisierungsserver zu erstellen. Wir hoffen, bald einen Download für das fertige Beispiel zur Verfügung zu stellen, da dieses Tutorial nicht jeden Schritt enthält. Erstellen Sie zunächst eine leere Web-App mit dem Namen *AuthorizationServer,* und installieren Sie die folgenden Pakete:

- Microsoft.AspNet.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- Microsoft.Owin.Security.Google (oder jedes andere Social-Login-Paket wie Microsoft.Owin.Security.Facebook)

Fügen Sie eine [OWIN-Startklasse](owin-startup-class-detection.md) unter dem Projektstammordner mit dem Namen *Startup*hinzu.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

Erstellen Sie einen *\_App-Startordner.* Wählen Sie den Ordner *App\_Start* aus, und verwenden Sie Shift+Alt+A, um die heruntergeladene Version der Datei *AuthorizationServer-App\_Start.Auth.cs* hinzuzufügen.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

Der obige Code ermöglicht Anwendungs-/externe Anmeldecookies und Die Google-Authentifizierung, die vom Autorisierungsserver selbst zur Verwaltung von Konten verwendet werden.

Die `UseOAuthAuthorizationServer` Erweiterungsmethode besteht darin, den Autorisierungsserver einzurichten. Die Einrichtungsoptionen sind:

- `AuthorizeEndpointPath`: Der Anforderungspfad, in dem Clientanwendungen den Benutzer-Agent umleiten, um die Zustimmung der Benutzer zum Ausstellen eines Tokens oder Codes einzuholen. Es muss mit einem führenden Schrägstrich`/Authorize`beginnen, zum Beispiel " ".
- `TokenEndpointPath`: Die Clientanwendungen des Anforderungspfads kommunizieren direkt, um das Zugriffstoken abzurufen. Es muss mit einem führenden Schrägstrich beginnen, wie "/Token". Wenn dem Client ein [geheimer Client\_](http://tools.ietf.org/html/rfc6749#appendix-A.2)ausgegeben wird, muss er diesem Endpunkt zur Verfügung gestellt werden.
- `ApplicationCanDisplayErrors`: Legen `true` Sie fest, ob die Webanwendung eine benutzerdefinierte `/Authorize` Fehlerseite für die Clientvalidierungsfehler auf dem Endpunkt generieren möchte. Dies ist nur in Fällen erforderlich, in denen der Browser nicht `client_id` zurück `redirect_uri` an die Clientanwendung umgeleitet wird, z. B. wenn die oder falsch sind. Der `/Authorize` Endpunkt sollte erwarten, dass "oauth. Fehler", "oauth. ErrorDescription" und "oauth. ErrorUri"-Eigenschaften werden der OWIN-Umgebung hinzugefügt.

    > [!NOTE]
    > Wenn nicht wahr, gibt der Autorisierungsserver eine Standardfehlerseite mit den Fehlerdetails zurück.
- `AllowInsecureHttp`: True, um Autorisierungs- und Tokenanforderungen für HTTP-URI-Adressen zu ermöglichen und eingehenden `redirect_uri` Autorisierungsanforderungsparametern zu erlauben, ÜBER HTTP-URI-Adressen zu verfügen.

    > [!WARNING]
    > Sicherheit - Dies ist nur für die Entwicklung.
- `Provider`: Das Objekt, das von der Anwendung bereitgestellt wird, um Ereignisse zu verarbeiten, die von der Authorization Server-Middleware ausgelöst werden. Die Anwendung kann die Schnittstelle vollständig implementieren oder `OAuthAuthorizationServerProvider` eine Instanz von erstellen und Delegaten zuweisen, die für die OAuth-Flows erforderlich sind, die dieser Server unterstützt.
- `AuthorizationCodeProvider`: Erstellt einen einmaligen Autorisierungscode, um zur Clientanwendung zurückzukehren. Damit der OAuth-Server sicher **MUST** ist, MUSS `AuthorizationCodeProvider` die Anwendung eine `OnCreate/OnCreateAsync` Instanz bereitstellen, für die `OnReceive/OnReceiveAsync`das vom Ereignis erzeugte Token nur für einen Aufruf von als gültig gilt.
- `RefreshTokenProvider`: Erstellt ein Aktualisierungstoken, das bei Bedarf zum Erstellen eines neuen Zugriffstokens verwendet werden kann. Wenn nicht angegeben, gibt der Autorisierungsserver `/Token` keine Aktualisierungstoken vom Endpunkt zurück.

## <a name="account-management"></a>Kontoverwaltung

OAuth ist es egal, wo oder wie Sie Ihre Benutzerkontoinformationen verwalten. Es ist [ASP.NET Identität,](../../../identity/index.md) die dafür verantwortlich ist. In diesem Tutorial vereinfachen wir den Kontoverwaltungscode und stellen einfach sicher, dass sich der Benutzer mit OWIN-Cookie-Middleware anmelden kann. Hier ist der vereinfachte `AccountController`Beispielcode für:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`wird verwendet, um den Client mit seiner registrierten Umleitungs-URL zu validieren. `ValidateClientAuthentication`überprüft den Grundlegendenschemaheader und Formulartext, um die Anmeldeinformationen des Clients abzufragen.

Die Anmeldeseite wird unten angezeigt:

![](owin-oauth-20-authorization-server/_static/image1.png)

Überprüfen Sie jetzt den Abschnitt OAuth 2 [Authorization Code Grant der](http://tools.ietf.org/html/rfc6749#section-4.1) IETF.

**Anbieter** (in der folgenden Tabelle) ist [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx). Anbieter, der vom `OAuthAuthorizationServerProvider`Typ ist, der alle OAuth-Serverereignisse enthält.

| Flow-Schritte aus dem Abschnitt Autorisierungscodeerteilung | Der Beispieldownload führt die folgenden Schritte aus mit: |
| --- | --- |
|  |  |
| (A) Der Client initiiert den Flow, indem er den Benutzer-Agent des Ressourcenbesitzers an den Autorisierungsendpunkt weiterleitet. Der Client enthält seinen Clientbezeichner, den angeforderten Bereich, den lokalen Status und einen Umleitungs-URI, an den der Autorisierungsserver den Benutzer-Agent zurücksendet, sobald der Zugriff gewährt (oder verweigert wird). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Der Autorisierungsserver authentifiziert den Ressourcenbesitzer (über den Benutzer-Agent) und stellt fest, ob der Ressourcenbesitzer die Zugriffsanforderung des Clients gewährt oder ablehnt. | **Wenn der&gt; Benutzer Zugriff gewährt &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Unter der Annahme, dass der Ressourcenbesitzer Zugriff gewährt, leitet der Autorisierungsserver den Benutzer-Agent mithilfe des zuvor angegebenen Umleitungs-URI (in der Anforderung oder während der Clientregistrierung) an den Client zurück. ... |  |
|  |  |
| (D) Der Client fordert ein Zugriffstoken vom Tokenendpunkt des Autorisierungsservers an, indem er den im vorherigen Schritt empfangenen Autorisierungscode einschließt. Bei der Anforderung authentifiziert sich der Client beim Autorisierungsserver. Der Client enthält den Umleitungs-URI, der zum Abrufen des Autorisierungscodes zur Überprüfung verwendet wird. | Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |

Eine Beispielimplementierung `AuthorizationCodeProvider.CreateAsync` `ReceiveAsync` für und zur Kontrolle der Erstellung und Validierung von Autorisierungscode wird unten gezeigt.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

Der obige Code verwendet ein in-Memory-Wörterbuch gleichzeitiges Wörterbuch, um den Code und das Identitätsticket zu speichern und die Identität nach dem Empfang des Codes wiederherzustellen. In einer echten Anwendung würde sie durch einen persistenten Datenspeicher ersetzt. Der Autorisierungsendpunkt ist für den Ressourcenbesitzer, der dem Client Zugriff gewährt. In der Regel benötigt es eine Benutzeroberfläche, damit der Benutzer auf eine Schaltfläche klicken und die Erteilung bestätigen kann. OWIN OAuth Middleware ermöglicht es Anwendungscode, den Autorisierungsendpunkt zu verarbeiten. In unserer Beispiel-App verwenden wir `OAuthController` einen MVC-Controller, der aufgerufen wird, um ihn zu behandeln. Hier ist die Beispielimplementierung:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

Die `Authorize` Aktion überprüft zunächst, ob sich der Benutzer beim Autorisierungsserver angemeldet hat. Ist dies nicht der Fall, fordert die Authentifizierungsmiddleware den Aufrufer auf, sich mit dem Cookie "Anwendung" zu authentifizieren, und leitet zur Anmeldeseite um. (Siehe hervorgehobener Code oben.) Wenn sich der Benutzer angemeldet hat, wird die Ansicht Autorisieren wie unten gezeigt gerendert:

![](owin-oauth-20-authorization-server/_static/image2.png)

Wenn die Schaltfläche **"Grant"** ausgewählt ist, erstellt die `Authorize` Aktion eine neue "Träger"-Identität und melden sich damit an. Es löst den Autorisierungsserver aus, um ein Inhabertoken zu generieren und es mit JSON-Nutzlast an den Client zurückzusenden.

### <a name="implicit-grant"></a>Implizite Zuscheine

Siehe jetzt den Abschnitt OAuth 2 [Implicit Grant der](http://tools.ietf.org/html/rfc6749#section-4.2) IETF.

 Der in Abbildung 4 dargestellte [implizite Grant-Flow](http://tools.ietf.org/html/rfc6749#section-4.2) ist der Flow und die Zuordnung, der die OWIN OAuth-Middleware folgt.

| Flow-Schritte aus dem Abschnitt Implizite Hilfe | Der Beispieldownload führt die folgenden Schritte aus mit: |
| --- | --- |
|  |  |
| (A) Der Client initiiert den Flow, indem er den Benutzer-Agent des Ressourcenbesitzers an den Autorisierungsendpunkt weiterleitet. Der Client enthält seinen Clientbezeichner, den angeforderten Bereich, den lokalen Status und einen Umleitungs-URI, an den der Autorisierungsserver den Benutzer-Agent zurücksendet, sobald der Zugriff gewährt (oder verweigert wird). | Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint |
|  |  |
| (B) Der Autorisierungsserver authentifiziert den Ressourcenbesitzer (über den Benutzer-Agent) und stellt fest, ob der Ressourcenbesitzer die Zugriffsanforderung des Clients gewährt oder ablehnt. | **Wenn der&gt; Benutzer Zugriff gewährt &lt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync |
|  |  |
| (C) Unter der Annahme, dass der Ressourcenbesitzer Zugriff gewährt, leitet der Autorisierungsserver den Benutzer-Agent mithilfe des zuvor angegebenen Umleitungs-URI (in der Anforderung oder während der Clientregistrierung) an den Client zurück. ... |  |
|  |  |
| (D) Der Client fordert ein Zugriffstoken vom Tokenendpunkt des Autorisierungsservers an, indem er den im vorherigen Schritt empfangenen Autorisierungscode einschließt. Bei der Anforderung authentifiziert sich der Client beim Autorisierungsserver. Der Client enthält den Umleitungs-URI, der zum Abrufen des Autorisierungscodes zur Überprüfung verwendet wird. |  |

Da wir bereits den Autorisierungsendpunkt (Aktion)`OAuthController.Authorize` für die Berechtigungscodeerteilung implementiert haben, wird automatisch auch der implizite Fluss aktiviert. Hinweis: `Provider.ValidateClientRedirectUri` wird verwendet, um die Client-ID mit ihrer Umleitungs-URL zu überprüfen, die den impliziten Grant-Fluss vor dem Senden des Zugriffstokens an böswillige Clients schützt ([Man-in-the-Middle-Angriff](https://www.owasp.org/index.php/Man-in-the-middle_attack)).

### <a name="resource-owner-password-credentials-grant"></a>Resource Owner Password Credentials Grant

Lesen Sie jetzt den Abschnitt OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) der IETF.

 Der in Abbildung 5 [dargestellte Ressourcenbesitzerkennwortanmeldeinformationen-Grant-Flow](http://tools.ietf.org/html/rfc6749#section-4.3) ist der Flow und die Zuordnung, der die OWIN OAuth-Middleware folgt.

| Flow-Schritte aus dem Abschnitt Ressourcenbesitzerkennwortanmeldeinformationen gewähren | Der Beispieldownload führt die folgenden Schritte aus mit: |
| --- | --- |
|  |  |
| (A) Der Ressourcenbesitzer gibt dem Client seinen Benutzernamen und sein Kennwort an. |  |
|  |  |
| (B) Der Client fordert ein Zugriffstoken vom Tokenendpunkt des Autorisierungsservers an, indem er die vom Ressourcenbesitzer empfangenen Anmeldeinformationen einschließt. Bei der Anforderung authentifiziert sich der Client beim Autorisierungsserver. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (C) Der Autorisierungsserver authentifiziert den Client, überprüft die Anmeldeinformationen des Ressourcenbesitzers und gibt, falls gültig, ein Zugriffstoken aus. |  |

Hier ist die `Provider.GrantResourceOwnerCredentials`Beispielimplementierung für:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> Der obige Code soll diesen Abschnitt des Tutorials erklären und sollte nicht in sicheren oder Produktions-Apps verwendet werden. Die Anmeldeinformationen der Ressourcenbesitzer werden nicht überprüft. Es wird davon ausgegangen, dass alle Anmeldeinformationen gültig sind, und es wird eine neue Identität für sie erstellt. Die neue Identität wird verwendet, um das Zugriffstoken und das Aktualisierungstoken zu generieren. Ersetzen Sie den Code durch Ihren eigenen sicheren Kontoverwaltungscode.


### <a name="client-credentials-grant"></a>Clientcredentials Grant

Lesen Sie jetzt den Abschnitt OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) der IETF.

 Der in Abbildung 6 [dargestellte Client Credentials Grant-Flow](http://tools.ietf.org/html/rfc6749#section-4.4) ist der Flow und die Zuordnung, der die OWIN OAuth-Middleware folgt.

| Flow-Schritte aus dem Abschnitt "Clientanmeldeinformationen gewähren" | Der Beispieldownload führt die folgenden Schritte aus mit: |
| --- | --- |
|  |  |
| (A) Der Client authentifiziert sich beim Autorisierungsserver und fordert ein Zugriffstoken vom Tokenendpunkt an. | Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (B) Der Autorisierungsserver authentifiziert den Client und gibt, falls gültig, ein Zugriffstoken aus. |  |

Hier ist die `Provider.GrantClientCredentials`Beispielimplementierung für:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> Der obige Code soll diesen Abschnitt des Tutorials erklären und sollte nicht in sicheren oder Produktions-Apps verwendet werden. Ersetzen Sie den Code durch Ihren eigenen sicheren Clientverwaltungscode.


### <a name="refresh-token"></a>Aktualisieren eines Tokens

Lesen Sie jetzt den Abschnitt OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) der IETF.

 Der in Abbildung 2 dargestellte [Refresh-Token-Flow](http://tools.ietf.org/html/rfc6749#section-1.5) ist der Flow und die Zuordnung, der die OWIN OAuth-Middleware folgt.

| Flow-Schritte aus dem Abschnitt "Clientanmeldeinformationen gewähren" | Der Beispieldownload führt die folgenden Schritte aus mit: |
| --- | --- |
|  |  |
| (G) Der Client fordert ein neues Zugriffstoken an, indem er sich beim Autorisierungsserver authentifiziert und das Aktualisierungstoken vorstellt. Die Clientauthentifizierungsanforderungen basieren auf dem Clienttyp und den Richtlinien des Autorisierungsservers. | Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync |
|  |  |
| (H) Der Autorisierungsserver authentifiziert den Client und überprüft das Aktualisierungstoken und gibt, falls gültig, ein neues Zugriffstoken (und optional ein neues Aktualisierungstoken) aus. |  |

Hier ist die `Provider.GrantRefreshToken`Beispielimplementierung für:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>Erstellen eines Ressourcenservers, der durch Zugriffstoken geschützt ist

Erstellen Sie ein leeres Web-App-Projekt, und installieren Sie die folgenden Pakete im Projekt:

- Microsoft.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

Erstellen Sie eine Startklasse, und konfigurieren Sie die Authentifizierung und web-API. Siehe *AuthorizationServer-ResourceServer-Startup.cs* im Beispieldownload.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

Weitere Informationen finden Sie im *Beispieldownload unter\_AuthorizationServer-ResourceServer-App-Start-Start-Start.Auth.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

Weitere Informationen finden Sie im *Beispieldownload unter\_AuthorizationServer-ResourceServer-App-Start-Start.WebApi.cs.*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`ermöglicht CORS für alle Domänen.
- `UseOAuthBearerAuthentication`Die Methode aktiviert OAuth Bearer-Token-Authentifizierungsmiddleware, die Das Bärentoken vom Autorisierungsheader in der Anforderung empfängt und validiert.
- `Config.SuppressDefaultHostAuthenticaiton`unterdrückt den standardmäßigen authentifizierten Prinzipal des Hosts aus der App, daher werden alle Anforderungen nach diesem Aufruf anonym.
- `HostAuthenticationFilter`aktiviert die Authentifizierung nur für den angegebenen Authentifizierungstyp. In diesem Fall ist es Träger-Authentifizierungstyp.

Um die authentifizierte Identität zu demonstrieren, erstellen wir einen ApiController, um die Ansprüche des aktuellen Benutzers auszugeben.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

Wenn sich der Autorisierungsserver und der Ressourcenserver nicht auf demselben Computer befinden, verwendet die OAuth-Middleware die verschiedenen Computerschlüssel, um das Inhaberzugriffstoken zu verschlüsseln und zu entschlüsseln. Um den gleichen privaten Schlüssel zwischen beiden Projekten `machinekey` zu teilen, fügen wir die gleiche Einstellung in beiden *web.config-Dateien* hinzu.

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>Erstellen von OAuth 2.0-Clients

 Wir verwenden das [Paket DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet, um den Clientcode zu vereinfachen.

### <a name="authorization-code-grant-client"></a>Autorisierungscode gewähren Client

 Dieser Client ist eine MVC-Anwendung. Es löst einen Autorisierungscodegrantfluss aus, um das Zugriffstoken vom Back-End abzurufen. Es hat eine einzige Seite, wie unten gezeigt:

![](owin-oauth-20-authorization-server/_static/image3.png)

- Die Schaltfläche **Autorisieren** leitet den Browser an den Autorisierungsserver um, um den Ressourcenbesitzer zu benachrichtigen, zugriff auf diesen Client zu gewähren.
- Die **Schaltfläche Aktualisieren** erhält ein neues Zugriffstoken und ein Aktualisierungstoken mit dem aktuellen Aktualisierungstoken.
- Die Access **Protected Resource API-Schaltfläche** ruft den Ressourcenserver auf, um die Anspruchsdaten des aktuellen Benutzers abzurufen und auf der Seite anzuzeigen.

Hier ist der Beispielcode des `HomeController` Clients.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`erfordert standardmäßig SSL. Da unsere Demo HTTP verwendet, müssen Sie in der Konfigurationsdatei folgende Einstellung hinzufügen:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> Sicherheit - Deaktivieren Sie SSL niemals in einer Produktions-App. Ihre Anmeldeinformationen werden jetzt im Klartext über den Draht gesendet. Der obige Code ist nur für lokales Beispiel-Debugging und Exploration.


### <a name="implicit-grant-client"></a>Impliziter Grant-Client

Dieser Client verwendet JavaScript, um:

1. Öffnen Sie ein neues Fenster, und leiten Sie es zum Autorisierungsendpunkt des Autorisierungsservers um.
2. Rufen Sie das Zugriffstoken aus URL-Fragmenten ab, wenn es zurückleitet.

Die folgende Abbildung zeigt diesen Prozess:

![](owin-oauth-20-authorization-server/_static/image4.png)

Der Client sollte zwei Seiten haben: eine für die Homepage und die andere für den Rückruf. Hier ist das Beispiel JavaScript-Code in der *Datei Index.cshtml* gefunden:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

Hier ist der Rückrufbehandlungscode in *der Datei SignIn.cshtml:*

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> Es wird jedoch dringend verfahren, JavaScript in eine externe Datei zu verschieben und nicht in das Razor-Markup einzubetten. Um diese Probe einfach zu halten, wurden sie kombiniert.


### <a name="resource-owner-password-credentials-grant-client"></a>Ressourcenbesitzer-Kennwortanmeldeinformationen gewähren Client

Wir verwenden eine Konsolen-App, um diesen Client vorzuführen. Hier folgt der Code:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>Clientanmeldeinformationen gewähren Client

Ähnlich wie bei der Resource Owner Password Credentials Grant, hier ist Konsolen-App-Code:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
