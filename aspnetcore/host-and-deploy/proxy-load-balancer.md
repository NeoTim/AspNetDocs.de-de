---
title: Konfigurieren von ASP.NET Core zur Verwendung mit Proxyservern und Lastenausgleich
author: guardrex
description: Informationen zur Konfiguration von hinter Proxyservern und Lastenausgleichsmodulen gehosteten Apps, wobei wichtige Anforderungsinformationen häufig verdeckt werden
ms.author: riande
ms.custom: mvc
ms.date: 09/06/2018
uid: host-and-deploy/proxy-load-balancer
ms.openlocfilehash: a03250d6cafe7279c3fcf3957d33214a9b4ed514
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032037"
---
# <a name="configure-aspnet-core-to-work-with-proxy-servers-and-load-balancers"></a>Konfigurieren von ASP.NET Core zur Verwendung mit Proxyservern und Lastenausgleich

Von [Luke Latham](https://github.com/guardrex) und [Chris Ross](https://github.com/Tratcher)

In der für ASP.NET Core empfohlenen Konfiguration wird die App mit dem IIS/ASP.NET Core-Modul, Nginx oder Apache gehostet. Proxyserver, Lastenausgleichsmodule und anderen Netzwerkgeräte verdecken häufig Informationen über die Anforderung, bevor diese die App erreicht:

* Wenn HTTPS-Anforderungen über HTTP-Proxy ausgeführt werden, geht das ursprüngliche Schema (HTTPS) verloren und muss in einem Header weitergeleitet werden.
* Da eine App eine Anforderung über den Proxy empfängt und nicht über ihre echte Quelle im Internet oder Unternehmensnetzwerk, muss die ursprüngliche Client-IP-Adresse ebenfalls in einem Header weitergeleitet werden.

Diese Informationen können im Anforderungsprozess, z.B. in Umleitungen, bei der Authentifizierung, der Linkgenerierung, der Richtlinienauswertung und der Client-Geolocation wichtig sein.

## <a name="forwarded-headers"></a>Weitergeleitete Header

Gemäß der Konvention leiten Proxys Informationen in HTTP-Headern weiter.

| Header | Beschreibung |
| ------ | ----------- |
| X-Forwarded-For | Enthält Informationen zum Client, der die Anforderung und die nachfolgenden Proxys in einer Kette von Proxys initiiert hat. Dieser Parameter kann IP-Adressen (und optional Portnummern) enthalten. Der erste Parameter in einer Kette von Proxyservern gibt den Client an, auf dem die Anforderung zuerst gesendet wurde. Darauf folgen weitere Proxybezeichner. Der letzte Proxy in der Kette ist nicht in der Liste der Parameter. Die IP-Adresse des letzten Proxys und optional eine Portnummer stehen als Remote IP-Adresse auf der Transportschicht zur Verfügung. |
| X-Forwarded-Proto | Der Wert des ursprünglichen Schemas (HTTP/HTTPS). Der Wert kann auch eine Liste von Schemas sein, wenn die Anforderung mehrere Proxys durchlaufen hat. |
| X-Forwarded-Host | Der ursprüngliche Wert des Felds „Hostheader“. In der Regel ändern Proxys den Hostheader nicht. Informationen über Sicherheitslücken, durch die Rechteerweiterungen ermöglicht werden und die sich auf Systeme auswirken, in denen der Proxy Hostheader nicht validiert oder auf bekannte gute Werte beschränkt, finden Sie in der [Microsoft-Sicherheitsempfehlung CVE-2018-0787](https://github.com/aspnet/Announcements/issues/295). |

Die Middleware für weitergeleitete Header aus dem Paket [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) liest die Header und füllt die zugehörigen Felder in [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext) aus.

Die Middleware aktualisiert:

* [HttpContext.Connection.RemoteIpAddress](/dotnet/api/microsoft.aspnetcore.http.connectioninfo.remoteipaddress) &ndash; Auf den Headerwert `X-Forwarded-For` festlegen. Zusätzliche Einstellungen beeinflussen, wie die Middleware `RemoteIpAddress` festlegt. Einzelheiten finden Sie unter [Middleware für weitergeleitete Header: Optionen](#forwarded-headers-middleware-options).
* [HttpContext.Request.Scheme](/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme) &ndash; Auf den Headerwert `X-Forwarded-Proto` festlegen.
* [HttpContext.Request.Host](/dotnet/api/microsoft.aspnetcore.http.httprequest.host) &ndash; Auf den Headerwert `X-Forwarded-Host` festlegen.

Die [Standardeinstellungen](#forwarded-headers-middleware-options) der Middleware für weitergeleitete Header können konfiguriert werden. Folgende Standardeinstellungen sind verfügbar:

* Zwischen App und Quelle der Anforderungen ist nur ein *Proxy* vorhanden.
* Loopbackadressen sind für bekannte Proxys und bekannte Netzwerke konfiguriert.
* Die weitergeleiteten Header heißen `X-Forwarded-For` und `X-Forwarded-Proto`.

Beachten Sie, dass bei manchen Netzwerkgeräten eine zusätzliche Konfiguration erforderlich ist, damit die Header `X-Forwarded-For` und `X-Forwarded-Proto` hinzugefügt werden. Lesen Sie in der Anleitung des Geräteherstellers nach, wenn über einen Proxy übermittelte Anfragen ohne diese Header in der Anwendung eingehen. Verwendet das Gerät andere Headernamen als `X-Forwarded-For` und `X-Forwarded-Proto`, passen Sie die Optionen [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) und [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) entsprechend an. Weitere Informationen finden Sie in den Abschnitten [Middleware für weitergeleitete Header: Optionen](#forwarded-headers-middleware-options) und [Konfiguration für einen Proxy, der andere Headernamen nutzt](#configuration-for-a-proxy-that-uses-different-header-names).

## <a name="iisiis-express-and-aspnet-core-module"></a>IIS-/IIS Express und ASP.NET Core-Modul

Middleware für weitergeleitete Header wird standardmäßig durch Middleware für die Integration von IIS aktiviert, wenn die App hinter IIS und dem ASP.NET Core-Modul ausgeführt wird. Middleware für weitergeleitete Header wird aktiviert und zuerst in der Middlewarepipeline mit einer beschränkten Konfiguration ausgeführt, die für das ASP.NET Core-Modul spezifisch ist. Dies ist auf Bedenken in Bezug auf die Vertrauenswürdigkeit von weitergeleiteten Headern zurückzuführen (z.B. [IP-Spoofing](https://www.iplocation.net/ip-spoofing)). Die Middleware wird so konfiguriert, dass sie die Header `X-Forwarded-For` und `X-Forwarded-Proto` weiterleitet, und ist auf einen einzelnen localhost-Proxy beschränkt. Wenn zusätzliche Konfigurationsschritte erforderlich sind, finden Sie weitere Informationen unter [Middleware für weitergeleitete Header: Optionen](#forwarded-headers-middleware-options).

## <a name="other-proxy-server-and-load-balancer-scenarios"></a>Andere Proxyserver- und Lastenausgleichsszenarios

Außer bei der Verwendung als Middleware für die Integration von IIS wird die Middleware für weitergeleitete Header nicht standardmäßig aktiviert. Middleware für weitergeleitete Header muss aktiviert sein, damit eine App weitergeleitete Header mit [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) verarbeitet. Wenn nach der Aktivierung der Middleware [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) nicht für die Middleware angegeben wurde, ist [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) standardmäßig [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders).

Konfigurieren Sie die Middleware mit [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions), um die Header `X-Forwarded-For` und `X-Forwarded-Proto` in `Startup.ConfigureServices` weiterzuleiten. Rufen Sie die Methode [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) in `Startup.Configure` auf, bevor Sie andere Middleware aufrufen:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.Configure<ForwardedHeadersOptions>(options =>
    {
        options.ForwardedHeaders = 
            ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto;
    });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseForwardedHeaders();

    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();
    // In ASP.NET Core 1.x, replace the following line with: app.UseIdentity();
    app.UseAuthentication();
    app.UseMvc();
}
```

> [!NOTE]
> Wenn [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) nicht in `Startup.ConfigureServices` oder direkt für die Erweiterungsmethode mit [UseForwardedHeaders(IApplicationBuilder, ForwardedHeadersOptions)](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ForwardedHeadersExtensions_UseForwardedHeaders_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_ForwardedHeadersOptions_) angegeben wurde, müssen die Standardheader [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders) weitergeleitet werden. Die Eigenschaft [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) muss mit den weiterzuleitenden Headern konfiguriert werden.

## <a name="nginx-configuration"></a>Nginx-Konfiguration

Informationen zur Weiterleitung der Header `X-Forwarded-For` und `X-Forwarded-Proto` finden Sie unter <xref:host-and-deploy/linux-nginx#configure-nginx>. Weitere Informationen finden Sie unter [NGINX: Mit dem Forwarded-Header](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/).

## <a name="apache-configuration"></a>Apache-Konfiguration

`X-Forwarded-For` wird automatisch hinzugefügt (siehe [Mod_proxy der Apache-Modul: Reverse-Proxy-Anforderungsheader](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html#x-headers)). Informationen zur Weiterleitung des Headers `X-Forwarded-Proto` finden Sie unter <xref:host-and-deploy/linux-apache#configure-apache>.

## <a name="forwarded-headers-middleware-options"></a>Middleware für weitergeleitete Header: Optionen

[ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) steuern das Verhalten der Middleware für weitergeleitete Header. Im folgenden Beispiel werden die Standardwerte geändert:

* Beschränken Sie die Zahl der Einträge in den weitergeleiteten Headern auf `2`.
* Fügen Sie eine bekannte Proxyadresse von `127.0.10.1` hinzu.
* Ändern Sie den Namen des weitergeleiteten Headers vom Standardwert `X-Forwarded-For` in den Wert `X-Forwarded-For-My-Custom-Header-Name`.

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardLimit = 2;
    options.KnownProxies.Add(IPAddress.Parse("127.0.10.1"));
    options.ForwardedForHeaderName = "X-Forwarded-For-My-Custom-Header-Name";
});
```

::: moniker range=">= aspnetcore-2.1"

| Option | Beschreibung |
| ------ | ----------- |
| AllowedHosts | Begrenzt Hosts durch den `X-Forwarded-Host`-Header auf die angegebenen Werte.<ul><li>Werte werden mit Ordnungszahl/Groß-/Kleinschreibung ignorieren verglichen.</li><li>Portnummern müssen ausgeschlossen werden.</li><li>Wenn die Liste leer ist, sind alle Hosts zulässig.</li><li>Ein Platzhalter `*` auf der obersten Ebene lässt alle nicht leeren Hosts zu.</li><li>Unterdomänen-Platzhalter sind zulässig, stimmen aber nicht mit der Stammdomäne überein. Beispielsweise entspricht `*.contoso.com` der Unterdomäne `foo.contoso.com`, aber nicht der Stammdomäne `contoso.com`.</li><li>Unicode-Hostnamen sind zulässig, werden jedoch für den Abgleich in [Punycode](https://tools.ietf.org/html/rfc3492) konvertiert.</li><li>[IPv6-Adressen](https://tools.ietf.org/html/rfc4291) müssen Begrenzungsklammern einschließen und im [konventionellen Format](https://tools.ietf.org/html/rfc4291#section-2.2) vorliegen (z.B. `[ABCD:EF01:2345:6789:ABCD:EF01:2345:6789]`). IPv6-Adressen sind keine Sonderfälle, um auf logische Gleichheit zwischen verschiedenen Formaten zu prüfen, und es wird keine Kanonisierung durchgeführt.</li><li>Dadurch, dass die zulässigen Hosts nicht begrenzt werden, kann einem Angreifer die Möglichkeit eröffnet werden, von dem Dienst generierte Links zu fälschen.</li></ul>Der Standardwert ist eine leere [IList\<string>](/dotnet/api/system.collections.generic.ilist-1). |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-For` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-For`. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | Gibt an, welche Weiterleitungen verarbeitet werden sollen. Weitere Informationen zur Liste der anzuwendenden Felder finden Sie unter [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders). Typische Werte, die dieser Eigenschaft zugewiesen wurden, sind <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>.<br><br>Der Standardwert ist [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders). |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-Host` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-Host`. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-Proto` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-Proto`. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | Schränkt die Anzahl der Einträge in den Headern ein, die verarbeitet werden. Legen Sie den Wert `null` fest, um die Einschränkung zu deaktivieren. Diese Einstellung sollte jedoch nur vorgenommen werden, wenn `KnownProxies` oder `KnownNetworks` konfiguriert sind.<br><br>Der Standard ist 1. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | Adressbereiche bekannter Netzwerke; von dort weitergeleitete Header müssen akzeptiert werden. Geben Sie IP-Adressbereiche mithilfe der CIDR-Notation (Classless Interdomain Routing) an.<br><br>Wenn der Server Dualmodussockets verwendet, werden IPv4-Adressen in einem IPv6-Format bereitgestellt (z.B. wird `10.0.0.1` in IPv4 in IPv6 als `::ffff:10.0.0.1` dargestellt). Siehe [IPAddress.MapToIPv6](xref:System.Net.IPAddress.MapToIPv6*). Bestimmen Sie mithilfe der [HttpContext.Connection.RemoteIpAddress](xref:Microsoft.AspNetCore.Http.ConnectionInfo.RemoteIpAddress*), ob dieses Format erforderlich ist. Weitere Informationen finden Sie im Abschnitt [Konfiguration für eine IPv4-Adresse, die als IPv6-Adresse dargestellt wird](#configuration-for-an-ipv4-address-represented-as-an-ipv6-address).<br><br>Der Standardwert ist [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)> mit einem Eintrag für `IPAddress.Loopback`. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | Adressen bekannter Proxys, von denen weitergeleitete Header akzeptiert werden müssen. Verwenden Sie `KnownProxies`, um genaue IP-Adressübereinstimmungen anzugeben.<br><br>Wenn der Server Dualmodussockets verwendet, werden IPv4-Adressen in einem IPv6-Format bereitgestellt (z.B. wird `10.0.0.1` in IPv4 in IPv6 als `::ffff:10.0.0.1` dargestellt). Siehe [IPAddress.MapToIPv6](xref:System.Net.IPAddress.MapToIPv6*). Bestimmen Sie mithilfe der [HttpContext.Connection.RemoteIpAddress](xref:Microsoft.AspNetCore.Http.ConnectionInfo.RemoteIpAddress*), ob dieses Format erforderlich ist. Weitere Informationen finden Sie im Abschnitt [Konfiguration für eine IPv4-Adresse, die als IPv6-Adresse dargestellt wird](#configuration-for-an-ipv4-address-represented-as-an-ipv6-address).<br><br>Der Standardwert ist [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)> mit einem Eintrag für `IPAddress.IPv6Loopback`. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-For`. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-Host`. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-Proto`. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | Die Anzahl von Headerwerten muss in den [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) übereinstimmen, die verarbeitet werden.<br><br>Die Standardeinstellung in ASP.NET Core 1.x ist `true`. Die Standardeinstellung in ASP.NET Core 2.0 oder höher ist `false`. |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| Option | Beschreibung |
| ------ | ----------- |
| [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedforheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-For` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-For`. |
| [ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) | Gibt an, welche Weiterleitungen verarbeitet werden sollen. Weitere Informationen zur Liste der anzuwendenden Felder finden Sie unter [ForwardedHeaders Enum](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders). Typische Werte, die dieser Eigenschaft zugewiesen wurden, sind <code>ForwardedHeaders.XForwardedFor &#124; ForwardedHeaders.XForwardedProto</code>.<br><br>Der Standardwert ist [ForwardedHeaders.None](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheaders). |
| [ForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedhostheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedhostheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-Host` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-Host`. |
| [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xforwardedprotoheadername) angegebenen. Diese Option wird verwendet, wenn beim Proxy/Weiterleitenden nicht der Header `X-Forwarded-Proto` sondern ein anderer Header für die Weiterleitung der Informationen genutzt wird.<br><br>Die Standardeinstellung ist `X-Forwarded-Proto`. |
| [ForwardLimit](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardlimit) | Schränkt die Anzahl der Einträge in den Headern ein, die verarbeitet werden. Legen Sie den Wert `null` fest, um die Einschränkung zu deaktivieren. Diese Einstellung sollte jedoch nur vorgenommen werden, wenn `KnownProxies` oder `KnownNetworks` konfiguriert sind.<br><br>Der Standard ist 1. |
| [KnownNetworks](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownnetworks) | Adressbereiche bekannter Netzwerke; von dort weitergeleitete Header müssen akzeptiert werden. Geben Sie IP-Adressbereiche mithilfe der CIDR-Notation (Classless Interdomain Routing) an.<br><br>Wenn der Server Dualmodussockets verwendet, werden IPv4-Adressen in einem IPv6-Format bereitgestellt (z.B. wird `10.0.0.1` in IPv4 in IPv6 als `::ffff:10.0.0.1` dargestellt). Siehe [IPAddress.MapToIPv6](xref:System.Net.IPAddress.MapToIPv6*). Bestimmen Sie mithilfe der [HttpContext.Connection.RemoteIpAddress](xref:Microsoft.AspNetCore.Http.ConnectionInfo.RemoteIpAddress*), ob dieses Format erforderlich ist. Weitere Informationen finden Sie im Abschnitt [Konfiguration für eine IPv4-Adresse, die als IPv6-Adresse dargestellt wird](#configuration-for-an-ipv4-address-represented-as-an-ipv6-address).<br><br>Der Standardwert ist [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPNetwork](/dotnet/api/microsoft.aspnetcore.httpoverrides.ipnetwork)> mit einem Eintrag für `IPAddress.Loopback`. |
| [KnownProxies](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.knownproxies) | Adressen bekannter Proxys, von denen weitergeleitete Header akzeptiert werden müssen. Verwenden Sie `KnownProxies`, um genaue IP-Adressübereinstimmungen anzugeben.<br><br>Wenn der Server Dualmodussockets verwendet, werden IPv4-Adressen in einem IPv6-Format bereitgestellt (z.B. wird `10.0.0.1` in IPv4 in IPv6 als `::ffff:10.0.0.1` dargestellt). Siehe [IPAddress.MapToIPv6](xref:System.Net.IPAddress.MapToIPv6*). Bestimmen Sie mithilfe der [HttpContext.Connection.RemoteIpAddress](xref:Microsoft.AspNetCore.Http.ConnectionInfo.RemoteIpAddress*), ob dieses Format erforderlich ist. Weitere Informationen finden Sie im Abschnitt [Konfiguration für eine IPv4-Adresse, die als IPv6-Adresse dargestellt wird](#configuration-for-an-ipv4-address-represented-as-an-ipv6-address).<br><br>Der Standardwert ist [IList](/dotnet/api/system.collections.generic.ilist-1)\<[IPAddress](/dotnet/api/system.net.ipaddress)> mit einem Eintrag für `IPAddress.IPv6Loopback`. |
| [OriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalforheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalForHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalforheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-For`. |
| [OriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalhostheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalHostHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalhostheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-Host`. |
| [OriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.originalprotoheadername) | Verwenden Sie den Header, der von dieser Eigenschaft angegeben wurde, anstelle des von [ForwardedHeadersDefaults.XOriginalProtoHeaderName](/dotnet/api/microsoft.aspnetcore.httpoverrides.forwardedheadersdefaults.xoriginalprotoheadername) angegebenen.<br><br>Die Standardeinstellung ist `X-Original-Proto`. |
| [RequireHeaderSymmetry](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.requireheadersymmetry) | Die Anzahl von Headerwerten muss in den [ForwardedHeadersOptions.ForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedheaders) übereinstimmen, die verarbeitet werden.<br><br>Die Standardeinstellung in ASP.NET Core 1.x ist `true`. Die Standardeinstellung in ASP.NET Core 2.0 oder höher ist `false`. |

::: moniker-end

## <a name="scenarios-and-use-cases"></a>Szenarios und Anwendungsfälle

### <a name="when-it-isnt-possible-to-add-forwarded-headers-and-all-requests-are-secure"></a>Wenn keine weitergeleiteten Header hinzugefügt werden können und alle Anforderungen sicher sind

In einigen Fällen ist es möglicherweise ausgeschlossen, weitergeleitete Header den Anforderungen hinzuzufügen, die über einen Proxy an die App übermittelt werden. Wenn der Proxy erzwingt, dass alle öffentlichen externen Anforderungen HTTPS-Anforderungen sind, kann das Schema manuell in `Startup.Configure` festgelegt werden, bevor ein beliebiger Middlewaretyp verwendet wird:

```csharp
app.Use((context, next) =>
{
    context.Request.Scheme = "https";
    return next();
});
```

Dieser Code kann mit einer Umgebungsvariablen oder einer anderen Konfigurationseinstellung in einer Entwicklungs- oder Stagingumgebung deaktiviert werden.

### <a name="deal-with-path-base-and-proxies-that-change-the-request-path"></a>Umgang mit Pfadbasis und Proxys, die den Anforderungspfad ändern

Einige Proxys übergeben den Pfad intakt, aber mit einem App-basierten Pfad, der entfernt werden sollte, damit das Routing ordnungsgemäß funktioniert. [UsePathBaseExtensions.UsePathBase](/dotnet/api/microsoft.aspnetcore.builder.usepathbaseextensions.usepathbase)-Middleware teilt den Pfad in [HttpRequest.Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) und den App-Basispfad in [HttpRequest.PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase).

Wenn `/foo` der App-Basispfad für einen als `/foo/api/1` übergebenen Proxypfad ist, setzt die Middleware mit dem folgenden Befehl `Request.PathBase` auf `/foo` und `Request.Path` auf `/api/1`:

```csharp
app.UsePathBase("/foo");
```

Der ursprüngliche Pfad und die Pfadbasis werden erneut angewendet, wenn die Middleware in umgekehrter Reihenfolge erneut aufgerufen wird. Weitere Informationen zur Verarbeitungsreihenfolge in der Middleware finden Sie unter <xref:fundamentals/middleware/index>.

Wenn der Proxy den Pfad abschneidet (z.B. Weiterleitung von `/foo/api/1` zu `/api/1`), korrigieren Sie Umleitungen und Links, indem Sie die Eigenschaft [PathBase](/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase) der Anforderungen setzen:

```csharp
app.Use((context, next) =>
{
    context.Request.PathBase = new PathString("/foo");
    return next();
});
```

Wenn der Proxy Pfaddaten hinzufügt, verwerfen Sie einen Teil des Pfads, um Umleitungen und Links zu korrigieren, indem Sie [StartsWithSegments(PathString, PathString)](/dotnet/api/microsoft.aspnetcore.http.pathstring.startswithsegments#Microsoft_AspNetCore_Http_PathString_StartsWithSegments_Microsoft_AspNetCore_Http_PathString_Microsoft_AspNetCore_Http_PathString__) verwenden und der Eigenschaft [Path](/dotnet/api/microsoft.aspnetcore.http.httprequest.path) zuweisen:

```csharp
app.Use((context, next) =>
{
    if (context.Request.Path.StartsWithSegments("/foo", out var remainder))
    {
        context.Request.Path = remainder;
    }

    return next();
});
```

### <a name="configuration-for-a-proxy-that-uses-different-header-names"></a>Konfiguration für einen Proxy, der andere Headernamen verwendet

Verwendet der Proxy zum Weiterleiten der Proxyadresse/des Ports und zum Erzeugen der Schemainformationen andere Headernamen als `X-Forwarded-For` und `X-Forwarded-Proto`, passen Sie die Optionen [ForwardedForHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedforheadername) und [ForwardedProtoHeaderName](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions.forwardedprotoheadername) entsprechend an.

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardedForHeaderName = "Header_Name_Used_By_Proxy_For_X-Forwarded-For_Header";
    options.ForwardedProtoHeaderName = "Header_Name_Used_By_Proxy_For_X-Forwarded-Proto_Header";
});
```

### <a name="configuration-for-an-ipv4-address-represented-as-an-ipv6-address"></a>Konfiguration für eine IPv4-Adresse, die als IPv6-Adresse dargestellt wird

Wenn der Server Dualmodussockets verwendet, werden IPv4-Adressen in einem IPv6-Format bereitgestellt (z.B. wird `10.0.0.1` in IPv4 in IPv6 als `::ffff:10.0.0.1` oder `::ffff:a00:1` dargestellt). Siehe [IPAddress.MapToIPv6](xref:System.Net.IPAddress.MapToIPv6*). Bestimmen Sie mithilfe der [HttpContext.Connection.RemoteIpAddress](xref:Microsoft.AspNetCore.Http.ConnectionInfo.RemoteIpAddress*), ob dieses Format erforderlich ist.

Im folgenden Beispiel wird eine Netzwerkadresse, die weitergeleitete Header bereitstellt, der `KnownNetworks`-Liste im IPv6-Format hinzugefügt.

IPv4-Adresse: `10.11.12.1/8`

Konvertierte IPv6-Adresse: `::ffff:10.11.12.1`  
Präfixlänge des konvertierten: 104

Sie können die Adresse auch im Hexadezimalformat angeben (`10.11.12.1` in IPv6 als `::ffff:0a0b:0c01` dargestellt). Fügen Sie bei der Konvertierung einer IPv4-Adresse in IPv6 der CIDR-Präfixlänge 96 (`8` im Beispiel) für das zusätzliche `::ffff:`-IPv6-Präfix hinzu (8 + 96 = 104). 

```csharp
// To access IPNetwork and IPAddress, add the following namespaces:
// using using System.Net;
// using Microsoft.AspNetCore.HttpOverrides;
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.ForwardedHeaders =
        ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto;
    options.KnownNetworks.Add(new IPNetwork(
        IPAddress.Parse("::ffff:10.11.12.1"), 104));
});
```

## <a name="troubleshoot"></a>Problembehandlung

Wenn Header nicht wie erwartet zugewiesen werden, aktivieren Sie die [Protokollierung](xref:fundamentals/logging/index). Wenn die Protokolle nicht genügend Informationen zur Problembehandlung bereitstellen, listen Sie die vom Server empfangenen Anforderungsheader auf. Verwenden Sie Inlinemiddleware, um Anforderungsheader in eine App-Antwort zu schreiben oder die Header zu protokollieren. Platzieren Sie eines der folgenden Codebeispiele unmittelbar nach dem Aufruf von <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersExtensions.UseForwardedHeaders*> in `Startup.Configure`.

Um die Header in die Antwort der App zu schreiben, verwenden Sie die folgende Terminalinlinemiddleware:

```csharp
app.Run(async (context) =>
{
    context.Response.ContentType = "text/plain";

    // Request method, scheme, and path
    await context.Response.WriteAsync(
        $"Request Method: {context.Request.Method}{Environment.NewLine}");
    await context.Response.WriteAsync(
        $"Request Scheme: {context.Request.Scheme}{Environment.NewLine}");
    await context.Response.WriteAsync(
        $"Request Path: {context.Request.Path}{Environment.NewLine}");

    // Headers
    await context.Response.WriteAsync($"Request Headers:{Environment.NewLine}");

    foreach (var header in context.Request.Headers)
    {
        await context.Response.WriteAsync($"{header.Key}: " +
            $"{header.Value}{Environment.NewLine}");
    }

    await context.Response.WriteAsync(Environment.NewLine);

    // Connection: RemoteIp
    await context.Response.WriteAsync(
        $"Request RemoteIp: {context.Connection.RemoteIpAddress}");
});
```

Sie können auch in Protokolle anstatt in den Antworttext schreiben, indem Sie die folgende Inlinemiddleware verwenden. Dies ermöglicht es der Website, während des Debuggens normal zu funktionieren.

```csharp
var logger = _loggerFactory.CreateLogger<Startup>();

app.Use(async (context, next) =>
{
    // Request method, scheme, and path
    logger.LogDebug("Request Method: {METHOD}", context.Request.Method);
    logger.LogDebug("Request Scheme: {SCHEME}", context.Request.Scheme);
    logger.LogDebug("Request Path: {PATH}", context.Request.Path);

    // Headers
    foreach (var header in context.Request.Headers)
    {
        logger.LogDebug("Header: {KEY}: {VALUE}", header.Key, header.Value);
    }

    // Connection: RemoteIp
    logger.LogDebug("Request RemoteIp: {REMOTE_IP_ADDRESS}", 
        context.Connection.RemoteIpAddress);

    await next();
});
```

Bei der Verarbeitung werden `X-Forwarded-{For|Proto|Host}`-Werte in `X-Original-{For|Proto|Host}` verschoben. Wenn mehrere Werte in einem bestimmten Header vorhanden sind, beachten Sie die Prozessheader der Middleware für weitergeleitete Header in umgekehrter Reihenfolge von rechts nach links. Der Standardwert von `ForwardLimit` ist 1 (eins), sodass nur der ganz rechte Wert aus den Headern verarbeitet wird, es sei denn, der Wert von `ForwardLimit` wird erhöht.

Die ursprüngliche IP-Remoteadresse der Anforderung muss mit einem Eintrag in den `KnownProxies`- oder `KnownNetworks`-Listen übereinstimmen, bevor weitergeleitete Header verarbeitet werden. Auf diese Weise wird das Headerspoofing begrenzt, da keine Weiterleitungen von nicht vertrauenswürdigen Proxys akzeptiert werden. Wenn ein unbekannter Proxy erkannt wird, gibt die Protokollierung die Adresse des Proxys an:

```console
September 20th 2018, 15:49:44.168 Unknown proxy: 10.0.0.100:54321
```

Im vorherigen Beispiel ist 10.0.0.100 ein Proxyserver. Wenn der Server ein vertrauenswürdiger Proxy ist, fügen Sie die IP-Adresse des Servers `KnownProxies` (oder ein vertrauenswürdiges Netzwerk `KnownNetworks`) in `Startup.ConfigureServices` hinzu. Weitere Informationen finden Sie im Abschnitt [Middleware für weitergeleitete Header: Optionen](#forwarded-headers-middleware-options).

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

> [!IMPORTANT]
> Erlauben Sie nur vertrauenswürdigen Proxys und Netzwerken die Weiterleitung von Headern. Andernfalls sind Angriffe des Typs [IP-Spoofing](https://www.iplocation.net/ip-spoofing) möglich.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:host-and-deploy/web-farm>
* [Microsoft Security Advisory CVE-2018-0787: ASP.NET Core-Erhöhung des Berechtigungssicherheitsrisikos](https://github.com/aspnet/Announcements/issues/295)
