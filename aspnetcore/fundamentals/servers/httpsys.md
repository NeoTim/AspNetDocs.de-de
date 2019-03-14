---
title: Implementierung des Http.sys-Webservers in ASP.NET Core
author: guardrex
description: Erfahren Sie mehr über HTTP.sys. einen Webserver für ASP.NET Core unter Windows. HTTP.sys basiert auf dem HTTP.sys-Kernelmodustreiber, stellt eine Alternative zu Kestrel dar und kann zum Herstellen einer direkten Verbindung mit dem Internet ohne Internetinformationsdienste (IIS) verwendet werden.
monikerRange: '>= aspnetcore-2.0'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/21/2019
uid: fundamentals/servers/httpsys
ms.openlocfilehash: abb426b1a41226e52d9b9b5c00c41ff816890d36
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038067"
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a>Implementierung des Http.sys-Webservers in ASP.NET Core

Von [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) und [Luke Latham](https://github.com/guardrex)

[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) ist ein [Webserver für ASP.NET Core](xref:fundamentals/servers/index), der nur unter Windows ausgeführt werden kann. HTTP.sys stellt eine Alternative zum [Kestrel](xref:fundamentals/servers/kestrel)-Server dar und bietet einige Features, die in Kestrel fehlen.

> [!IMPORTANT]
> HTTP.sys ist nicht mit dem [ASP.NET Core-Modul](xref:host-and-deploy/aspnet-core-module) kompatibel und kann nicht mit IIS oder IIS Express verwendet werden.

HTTP.sys unterstützt die folgenden Features:

* [Windows-Authentifizierung](xref:security/authentication/windowsauth)
* Portfreigabe
* HTTPS mit SNI
* HTTP/2 über TLS (Windows 10 oder höher)
* Direkte Dateiübertragung
* Zwischenspeichern von Antworten
* WebSockets (Windows 8 oder höher)

Unterstützte Windows-Versionen:

* Windows 7 oder höher
* Windows Server 2008 R2 oder höher

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

## <a name="when-to-use-httpsys"></a>Empfohlene Verwendung von HTTP.sys

HTTP.sys eignet sich für Bereitstellungen, auf die Folgendes zutrifft:

* Sie müssen den Server ohne IIS direkt mit dem Internet verbinden.

  ![HTTP.sys kommuniziert direkt mit dem Internet](httpsys/_static/httpsys-to-internet.png)

* Eine interne Bereitstellung erfordert ein Feature, das in Kestrel nicht verfügbar ist, z.B. die [Windows-Authentifizierung](xref:security/authentication/windowsauth).

  ![HTTP.sys kommuniziert direkt mit dem internen Netzwerk](httpsys/_static/httpsys-to-internal.png)

Bei HTTP.sys handelt es sich um eine ausgereifte Technologie, die Schutz vor vielen Arten von Angriffen bietet und zudem die Stabilität, Sicherheit und Skalierbarkeit eines Webservers mit vollem Funktionsumfang bereitstellt. IIS selbst wird auf HTTP.sys als HTTP-Listener ausgeführt.

## <a name="http2-support"></a>HTTP/2-Unterstützung

[HTTP/2](https://httpwg.org/specs/rfc7540.html) ist für ASP.NET Core-Apps aktiviert, wenn die folgenden Basisanforderungen erfüllt sind:

* Windows Server 2016/Windows 10 oder höher
* [ALPN](https://tools.ietf.org/html/rfc7301#section-3)-Verbindung (Application-Layer Protocol Negotiation)
* TLS 1.2-Verbindung oder höher

::: moniker range=">= aspnetcore-2.2"

Wenn eine HTTP/2-Verbindung hergestellt wurde, meldet [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) `HTTP/2`.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

Wenn eine HTTP/2-Verbindung hergestellt wurde, meldet [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) `HTTP/1.1`.

::: moniker-end

HTTP/2 ist standardmäßig aktiviert. Für die Verbindung wird ein Fallback auf HTTP/1.1 ausgeführt, wenn keine HTTP/2-Verbindung hergestellt wurde. In einer zukünftigen Version von Windows werden HTTP/2-Konfigurationsflags verfügbar sein, einschließlich der Möglichkeit, HTTP/2 mit HTTP.sys zu deaktivieren.

## <a name="kernel-mode-authentication-with-kerberos"></a>Kernelmodusauthentifizierung mit Kerberos

HTTP.sys delegiert zur Kernelmodusauthentifizierung mit dem Kerberos-Authentifizierungsprotokoll. Die Benutzermodusauthentifizierung wird nicht von Kerberos und HTTP.sys unterstützt. Das Computerkonto muss zum Entschlüsseln des Kerberos-Tokens/-Tickets verwendet werden, das von Active Directory abgerufen und zur Authentifizierung des Benutzers vom Client an den Server weitergeleitet wird. Registrieren Sie den Dienstprinzipalnamen (SPN) für den Host, nicht für den Benutzer der App.

## <a name="how-to-use-httpsys"></a>Empfohlene Verwendung von HTTP.sys

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a>Konfigurieren der ASP.NET Core-App für die Verwendung von HTTP.sys

1. Bei Verwendung des [Microsoft.AspNetCore.App-Metapakets](xref:fundamentals/metapackage-app) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)) (ASP.NET Core 2.1 oder höher) ist kein Paketverweis in der Projektdatei erforderlich. Wenn das `Microsoft.AspNetCore.App`-Metapaket nicht verwendet wird, fügen Sie einen Paketverweis auf [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) hinzu.

2. Rufen Sie die Erweiterungsmethode <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderHttpSysExtensions.UseHttpSys*> auf, wenn Sie den Webhost erstellen, und geben Sie dabei alle erforderlichen <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions> an:

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   Die weitere Konfiguration von HTTP.sys erfolgt über [Registrierungseinstellungen](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows).

   **HTTP.sys-Optionen**

   | Eigenschaft | Beschreibung | Standard |
   | -------- | ----------- | :-----: |
   | [AllowSynchronousIO](xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.AllowSynchronousIO) | Hiermit steuern Sie, ob eine synchrone Eingabe/Ausgabe für `HttpContext.Request.Body` und `HttpContext.Response.Body` zulässig ist. | `true` |
   | [Authentication.AllowAnonymous](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationManager.AllowAnonymous) | Hiermit lassen Sie anonyme Anforderungen zu. | `true` |
   | [Authentication.Schemes](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationManager.Schemes) | Hiermit geben Sie die zulässigen Authentifizierungsschemas an. Diese Eigenschaft kann jederzeit vor dem Verwerfen des Listeners geändert werden. Die Werte werden durch die [AuthenticationSchemes-Enumeration](xref:Microsoft.AspNetCore.Server.HttpSys.AuthenticationSchemes) bereitgestellt: `Basic`, `Kerberos`, `Negotiate`, `None` und `NTLM`. | `None` |
   | [EnableResponseCaching](xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.EnableResponseCaching) | Hiermit wird das Caching im [Kernelmodus](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) für Antworten mit geeigneten Headern versucht. Die Antwort enthält möglicherweise keine `Set-Cookie`-, `Vary`- oder `Pragma`-Header. Sie muss einen `Cache-Control`-Header enthalten, der vom Typ `public` ist und entweder ein `shared-max-age`- oder ein `max-age`-Wert oder ein `Expires`-Header ist. | `true` |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxAccepts> | Die maximale Anzahl gleichzeitiger Aufrufe. | 5 &times; [Environment.<br>ProcessorCount](xref:System.Environment.ProcessorCount) |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxConnections> | Die maximale Anzahl an gleichzeitigen Verbindungen, die akzeptiert werden. Verwenden Sie `-1`, um eine unbegrenzte Anzahl anzugeben. Verwenden Sie `null`, um die computerübergreifende Einstellung der Registrierung zu verwenden. | `null`<br>(unbegrenzt) |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxRequestBodySize> | Informationen hierzu finden Sie im Abschnitt <a href="#maxrequestbodysize">MaxRequestBodySize</a>. | 30.000.000 Bytes<br>(~28,6 MB) |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.RequestQueueLimit> | Die maximale Anzahl von Anforderungen, die in der Warteschlange gespeichert werden kann. | 1000 |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ThrowWriteExceptions> | Hiermit geben Sie an, ob Schreibvorgänge für Antworttext, die einen Fehler zurückgeben, weil die Verbindung zum Client getrennt wird, eine Ausnahme auslösen oder normal beendet werden. | `false`<br>(normal beenden) |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.Timeouts> | Machen Sie die HTTP.sys-Konfiguration <xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager> verfügbar. Diese kann auch in der Registrierung konfiguriert werden. Unter folgenden API-Links finden Sie Informationen zu den einzelnen Einstellungen sowie die Standardwerte:<ul><li>[TimeoutManager.DrainEntityBody](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.DrainEntityBody) &ndash; Die zulässige Zeit, in der die HTTP-Server-API den Entitätskörper in einer Keep-Alive-Verbindung leeren muss.</li><li>[TimeoutManager.EntityBody](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.EntityBody) &ndash; Die zulässige Zeit, in der der Entitätskörper der Anforderung eintreffen muss.</li><li>[TimeoutManager.HeaderWait](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.HeaderWait) &ndash; Die zulässige Zeit, in der die HTTP-Server-API den Anforderungsheader analysieren muss.</li><li>[TimeoutManager.IdleConnection](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.IdleConnection) &ndash; Die zulässige Zeit für eine Verbindung im Leerlauf.</li><li>[TimeoutManager.MinSendBytesPerSecond](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.MinSendBytesPerSecond) &ndash; Die Mindestsenderate für die Antwort.</li><li>[TimeoutManager.RequestQueue](xref:Microsoft.AspNetCore.Server.HttpSys.TimeoutManager.RequestQueue) &ndash; Die zulässige Zeit, die die Anforderung in der Anforderungswarteschlange verbleibt, bevor sie von der App übernommen wird.</li></ul> |  |
   | <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes> | Geben Sie die <xref:Microsoft.AspNetCore.Server.HttpSys.UrlPrefixCollection> an, die bei „HTTP.sys“ registriert werden soll. Besonders nützlich ist die Eigenschaft [UrlPrefixCollection.Add](xref:Microsoft.AspNetCore.Server.HttpSys.UrlPrefixCollection.Add*), mit der Sie der Sammlung ein Präfix hinzufügen können. Diese Eigenschaften können jederzeit vor dem Verwerfen des Listeners geändert werden. |  |

   <a name="maxrequestbodysize"></a>

   **MaxRequestBodySize**

   Die maximal zulässige Größe eines Anforderungstexts in Bytes. Wenn dieser Wert auf `null` festgelegt wird, ist die maximale Größe für Anforderungstexte unbegrenzt. Dieser Grenzwert wirkt sich nicht auf Verbindungen aus, für die ein Upgrade durchgeführt wurde – diese sind immer unbegrenzt.

   Die empfohlene Methode zum Überschreiben des Grenzwerts in einer ASP.NET Core-MVC-App für ein einzelnes `IActionResult` besteht im Verwenden von <xref:Microsoft.AspNetCore.Mvc.RequestSizeLimitAttribute> in einer Aktionsmethode:

   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   Eine Ausnahme wird ausgelöst, wenn die App versucht, den Grenzwert einer Anforderung zu konfigurieren, nachdem die App bereits mit dem Lesen der Anforderung begonnen hat. Sie können eine `IsReadOnly`-Eigenschaft verwenden, um darauf hinzuweisen, dass sich die `MaxRequestBodySize`-Eigenschaft im schreibgeschützten Zustand befindet, der Grenzwert also nicht mehr konfiguriert werden kann.

   Wenn die App <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.MaxRequestBodySize> pro Anforderung außer Kraft setzen sollte, verwenden Sie das <xref:Microsoft.AspNetCore.Http.Features.IHttpMaxRequestBodySizeFeature>:

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

3. Wenn Sie Visual Studio verwenden, stellen Sie sicher, dass die App nicht für die Ausführung von IIS oder IIS Express konfiguriert ist.

   In Visual Studio ist das Standardstartprofil auf IIS Express ausgerichtet. Wenn das Projekt als Konsolen-App ausgeführt werden soll, ändern Sie das ausgewählte Profil manuell, wie im folgenden Screenshot dargestellt:

   ![Auswählen des Profils der App-Konsole](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a>Konfigurieren von Windows Server

1. Bestimmen Sie die Ports, die für die App geöffnet werden sollen, und verwenden Sie die [Windows-Firewall](/windows/security/threat-protection/windows-firewall/create-an-inbound-port-rule) oder das PowerShell-Cmdlet [New-NetFirewallRule](/powershell/module/netsecurity/new-netfirewallrule), um Firewall-Ports zu öffnen, damit der Datenverkehr HTTP.sys erreichen kann. In den folgenden Befehlen und der Appkonfiguration wird Port 443 verwendet.

1. Öffnen Sie bei der Bereitstellung für eine Azure-VM die Ports in der [Netzwerksicherheitsgruppe](/azure/virtual-machines/windows/nsg-quickstart-portal). In den folgenden Befehlen und der Appkonfiguration wird Port 443 verwendet.

1. Beziehen Sie X.509-Zertifikate und installieren Sie sie, falls erforderlich.

   Erstellen Sie unter Windows selbstsignierte Zertifikate mit dem [PowerShell-Cmdlet „New-SelfSignedCertificate“](/powershell/module/pkiclient/new-selfsignedcertificate). Ein nicht unterstütztes Beispiel finden Sie unter [UpdateIISExpressSSLForChrome.ps1](https://github.com/aspnet/Docs/tree/master/aspnetcore/includes/make-x509-cert/UpdateIISExpressSSLForChrome.ps1).

   Installieren Sie entweder selbstsignierte oder CA-signierte Zertifikate im Speicher **Lokaler Server** > **Persönlich** des Servers.

1. Wenn es sich bei der App um eine [frameworkabhängige Bereitstellung](/dotnet/core/deploying/#framework-dependent-deployments-fdd) handelt, installieren Sie .NET Core, .NET Framework oder beides (wenn es sich um eine .NET Core-App für das .NET Framework handelt).

   * **.NET Core**&ndash;: Wenn die App .NET Core erfordert, rufen Sie das **.NET Core Runtime**-Installationsprogramm über [.NET Core-Downloads](https://dotnet.microsoft.com/download) ab, und führen Sie es aus. Installieren Sie nicht das vollständige SDK auf dem Server.
   * **.NET Framework**&ndash;: Erfordert die App .NET Framework, rufen Sie das [.NET Framework-Installationshandbuch](/dotnet/framework/install/) auf. Installieren Sie das erforderliche .NET Framework. Das Installationsprogramm für das neueste .NET Framework steht auf der Seite [.NET Core-Downloads](https://dotnet.microsoft.com/download) zur Verfügung.

   Wenn die App eine [eigenständige Bereitstellung](/dotnet/core/deploying/#framework-dependent-deployments-scd) ist, enthält die App die Runtime in ihrer Bereitstellung. Es ist keine Frameworkinstallation auf dem Server erforderlich.

1. Konfigurieren Sie URLs und Ports in der App.

   Standardmäßig ist ASP.NET Core an `http://localhost:5000` gebunden. Zum Konfigurieren von URL-Präfixen und Ports stehen folgende Optionen zur Verfügung:

   * <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseUrls*>
   * Befehlszeilenargument `urls`
   * Umgebungsvariable `ASPNETCORE_URLS`
   * <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes>

   Das folgende Codebeispiel zeigt, wie Sie <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.UrlPrefixes> mit der lokalen IP-Adresse `10.0.0.4` des Servers auf Port 443 verwenden:

   [!code-csharp[](httpsys/sample_snapshot/Program.cs?name=snippet1&highlight=11)]

   Ein Vorteil von `UrlPrefixes` besteht darin, dass bei falsch formatierten Präfixen sofort eine Fehlermeldung generiert wird.

   Die Einstellungen in `UrlPrefixes` überschreiben die Einstellungen für `UseUrls`/`urls`/`ASPNETCORE_URLS`. Daher bieten `UseUrls`, `urls` und die Umgebungsvariable `ASPNETCORE_URLS` den Vorteil, dass sie den Wechsel zwischen Kestrel und HTTP.sys vereinfachen. Weitere Informationen finden Sie unter <xref:fundamentals/host/web-host>.

   HTTP.sys verwendet die [HTTP Server-API-UrlPrefix-Zeichenfolgenformate](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).

   > [!WARNING]
   > Allgemeine Platzhalterbindungen (`http://*:80/` und `http://+:80`) dürfen **nicht** verwendet werden. Platzhalterbindungen auf oberster Ebene gefährden die Sicherheit Ihrer App. Dies gilt für starke und schwache Platzhalter. Verwenden Sie statt Platzhaltern explizite Hostnamen oder IP-Adressen. Platzhalterbindungen in untergeordneten Domänen (z.B. `*.mysub.com`) stellen kein Sicherheitsrisiko dar, wenn Sie die gesamte übergeordnete Domäne steuern (im Gegensatz zu `*.com`, das angreifbar ist). Weitere Informationen finden Sie unter [RFC 7230: Abschnitt 5.4: Host](https://tools.ietf.org/html/rfc7230#section-5.4).

1. URL-Präfixe können vorab auf dem Server registriert werden.

   Das integrierte Tool für die Konfiguration von HTTP.sys ist *netsh.exe*. Mithilfe von *netsh.exe* können Sie URL-Präfixe reservieren und X.509-Zertifikate zuweisen. Das Tool erfordert Administratorrechte.

   Verwenden Sie das Tool *netsh.exe*, um die URLs für die App zu registrieren:

   ```console
   netsh http add urlacl url=<URL> user=<USER>
   ```

   * `<URL>` &ndash; Der vollqualifizierte Uniform Resource Locator (URL). Verwenden Sie keine Platzhalterbindung. Verwenden Sie einen gültigen Hostnamen oder eine gültige lokale IP-Adresse. *Die URL muss einen nachgestellten Schrägstrich enthalten.*
   * `<USER>` &ndash; Gibt den Benutzer oder den Benutzergruppennamen an.

   Im folgenden Beispiel ist die lokale IP-Adresse des Servers `10.0.0.4`:

   ```console
   netsh http add urlacl url=https://10.0.0.4:443/ user=Users
   ```

   Wenn eine URL registriert ist, antwortet das Tool mit `URL reservation successfully added`.

   Verwenden Sie zum Löschen einer registrierten URL den Befehl `delete urlacl`:

   ```console
   netsh http delete urlacl url=<URL>
   ```

1. Registrieren Sie X.509-Zertifikate auf dem Server.

   Verwenden Sie das Tool *netsh.exe*, um Zertifikate für die App zu registrieren:

   ```console
   netsh http add sslcert ipport=<IP>:<PORT> certhash=<THUMBPRINT> appid="{<GUID>}"
   ```

   * `<IP>` &ndash; Gibt die lokale IP-Adresse für die Bindung an. Verwenden Sie keine Platzhalterbindung. Verwenden Sie eine gültige IP-Adresse.
   * `<PORT>` &ndash; Gibt den Port für die Bindung an.
   * `<THUMBPRINT>` &ndash; Der X.509-Zertifikatsfingerabdruck.
   * `<GUID>` &ndash; Eine vom Entwickler generierte GUID zur Darstellung der App zu Informationszwecken.

   Speichern Sie die GUID zu Referenzzwecken in der App als Paket-Tag:

   * In Visual Studio:
     * Öffnen Sie die Projekteigenschaften der App, indem Sie mit der rechten Maustaste auf die App im **Projektmappen-Explorer** klicken und **Eigenschaften** auswählen.
     * Wählen Sie die Registerkarte **Paket** aus.
     * Geben Sie die GUID ein, die Sie im Feld **Tags** erstellt haben.
   * Wenn Sie Visual Studio nicht verwenden:
     * Öffnen Sie die Projektdatei der App.
     * Fügen Sie einer neuen oder vorhandenen `<PropertyGroup>` mit der von Ihnen erstellten GUID eine `<PackageTags>`-Eigenschaft hinzu:

       ```xml
       <PropertyGroup>
         <PackageTags>9412ee86-c21b-4eb8-bd89-f650fbf44931</PackageTags>
       </PropertyGroup>
       ```

   Im folgenden Beispiel:

   * Die lokale IP-Adresse des Servers lautet `10.0.0.4`.
   * Ein zufälliger Online-GUID-Generator stellt den Wert `appid` bereit.

   ```console
   netsh http add sslcert 
       ipport=10.0.0.4:443 
       certhash=b66ee04419d4ee37464ab8785ff02449980eae10 
       appid="{9412ee86-c21b-4eb8-bd89-f650fbf44931}"
   ```

   Wenn ein Zertifikat registriert ist, antwortet das Tool mit `SSL Certificate successfully added`.

   Verwenden Sie zum Löschen einer Zertifikatsregistrierung den Befehl `delete sslcert`:

   ```console
   netsh http delete sslcert ipport=<IP>:<PORT>
   ```

   Referenzdokumentation für *netsh.exe*:

   * [Netsh Commands for Hypertext Transfer Protocol (HTTP) (Netsh-Befehle für Hypertext Transfer-Protokolle (HTTP))](https://technet.microsoft.com/library/cc725882.aspx)
   * [UrlPrefix Strings (UrlPrefix-Zeichenfolgen)](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

1. Führen Sie die App aus.

   Administratorberechtigungen sind nicht erforderlich, um die App auszuführen, wenn die Verbindung zum lokalen Host über HTTP (nicht HTTPS) mit einer Portnummer größer als 1024 erfolgt. Für andere Konfigurationen (z.B. über eine lokale IP-Adresse oder Bindung an Port 443) führen Sie die App mit Administratorberechtigungen aus.

   Die App antwortet auf die öffentliche IP-Adresse des Servers. In diesem Beispiel wird der Server aus dem Internet mit seiner öffentlichen IP-Adresse `104.214.79.47` erreicht.

   In diesem Beispiel wird ein Entwicklungszertifikat verwendet. Die Seite wird sicher geladen, nachdem die Warnung vor nicht vertrauenswürdigen Zertifikaten des Browsers umgangen wurde.

   ![Browserfenster mit Anzeige der geladenen Indexseite der App](httpsys/_static/browser.png)

## <a name="proxy-server-and-load-balancer-scenarios"></a>Proxyserver und Lastenausgleichsszenarien

Für Apps, die von HTTP.sys gehostet werden und mit Anforderungen aus dem Internet oder einem Unternehmensnetzwerk interagieren, ist möglicherweise eine zusätzliche Konfiguration erforderlich, wenn sie hinter Proxyservern und Lastenausgleichsmodulen hosten. Weitere Informationen hierzu feinden Sie unter [Konfigurieren von ASP.NET Core zur Verwendung mit Proxyservern und Lastenausgleich](xref:host-and-deploy/proxy-load-balancer).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Aktivieren der Windows-Authentifizierung mit HTTP.sys](xref:security/authentication/windowsauth#enable-windows-authentication-with-httpsys)
* [HTTP-Server-API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)
* [aspnet/HttpSysServer – GitHub-Repository (Quellcode)](https://github.com/aspnet/HttpSysServer/)
* [Der Host](xref:fundamentals/index#host)
* <xref:test/troubleshoot>
