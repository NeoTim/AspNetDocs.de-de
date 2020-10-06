---
title: Arbeiten mit SameSite-Cookies in ASP.net
author: rick-anderson
description: Erfahren Sie, wie Sie mit SameSite-Cookies in ASP.NET verwenden.
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 2a39663dcbfa97ae441edd9a9768172cafbaab03
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763458"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="6dcfe-103">Arbeiten mit SameSite-Cookies in ASP.net</span><span class="sxs-lookup"><span data-stu-id="6dcfe-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="6dcfe-104">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6dcfe-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6dcfe-105">SameSite ist ein [IETF](https://ietf.org/about/) -Entwurfs Standard, der Schutz vor Cross-Site Request fälschungstoken (CSRF) bietet.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="6dcfe-106">Ursprünglich in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)entworfen wurde, wurde der Entwurfs Standard in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="6dcfe-107">Der aktualisierte Standard ist nicht abwärts kompatibel mit dem vorherigen Standard, und es gibt folgende Unterschiede:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="6dcfe-108">Cookies ohne SameSite-Header werden `SameSite=Lax` standardmäßig als behandelt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="6dcfe-109">`SameSite=None` muss verwendet werden, um eine standortübergreifende Cookie-Verwendung zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="6dcfe-110">Cookies, die bestätigen, `SameSite=None` müssen auch als markiert werden `Secure` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="6dcfe-111">Bei Anwendungen, die verwenden, treten [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) möglicherweise Probleme mit- `sameSite=Lax` oder `sameSite=Strict` -Cookies auf, da `<iframe>` als standortübergreifende Szenarien behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="6dcfe-112">Der Wert `SameSite=None` ist vom [2016-Standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) nicht zulässig und bewirkt, dass einige Implementierungen solche Cookies als behandeln `SameSite=Strict` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="6dcfe-113">Siehe [Unterstützung älterer Browser](#sob) in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="6dcfe-114">Die `SameSite=Lax` Einstellung funktioniert für die meisten Anwendungs Cookies.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="6dcfe-115">Für einige Formen der Authentifizierung wie [OpenID Connect](https://openid.net/connect/) (oidc) und [WS-](https://auth0.com/docs/protocols/ws-fed) Verbund werden standardmäßig Post basierte Umleitungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="6dcfe-116">Die Post basierten Umleitungen veranlassen den SameSite-Browserschutz, sodass SameSite für diese Komponenten deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="6dcfe-117">Die meisten [OAuth](https://oauth.net/) -Anmeldungen sind aufgrund von Unterschieden in der Art der Anforderungs Abläufe nicht betroffen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="6dcfe-118">Jede ASP.NET-Komponente, die Cookies ausgibt, muss entscheiden, ob SameSite geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="6dcfe-119">Weitere Informationen finden Sie unter [bekannte Probleme](#known) bei Anwendungen nach Installation der 2019 .net SameSite-Updates.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="6dcfe-120">Verwenden von SameSite in ASP.NET 4.7.2 und 4,8</span><span class="sxs-lookup"><span data-stu-id="6dcfe-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="6dcfe-121">.NET 4.7.2 und 4,8 unterstützen [2019 den Entwurf Standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) für SameSite seit der Veröffentlichung von Updates im Dezember 2019.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="6dcfe-122">Entwickler können den Wert des SameSite-Headers mithilfe der [HttpCookie. SameSite-Eigenschaft](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)Programm gesteuert steuern.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="6dcfe-123">Wenn die- `SameSite` Eigenschaft auf `Strict` , oder festgelegt wird, werden die `Lax` `None` Werte im Netzwerk mit dem Cookie geschrieben.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="6dcfe-124">Wenn Sie den Wert auf festlegen, `(SameSiteMode)(-1)` wird angegeben, dass kein SameSite-Header mit dem Cookie im Netzwerk enthalten sein soll.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="6dcfe-125">Die [HttpCookie. Secure-Eigenschaft](/dotnet/api/system.web.httpcookie.secure)oder ' Requirements SSL ' in Konfigurationsdateien kann verwendet werden, um das Cookie als `Secure` oder nicht zu markieren.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="6dcfe-126">Neue `HttpCookie` Instanzen werden standardmäßig mit `SameSite=(SameSiteMode)(-1)` und verwendet `Secure=false` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="6dcfe-127">Diese Standardwerte können im-Konfigurations Abschnitt überschrieben werden `system.web/httpCookies` , wobei die Zeichenfolge `"Unspecified"` eine nur für die reine Konfiguration geeignete Syntax für ist `(SameSiteMode)(-1)` :</span><span class="sxs-lookup"><span data-stu-id="6dcfe-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="6dcfe-128">ASP.net gibt auch vier spezifische Cookies für diese Features aus: anonyme Authentifizierung, Formular Authentifizierung, Sitzungs Status und Rollen Verwaltung.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="6dcfe-129">Instanzen dieser Cookies, die in der Laufzeit abgerufen werden, können `SameSite` `Secure` wie jede andere HttpCookie-Instanz mithilfe der-Eigenschaft und der-Eigenschaft manipuliert werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="6dcfe-130">Aufgrund der patchentstehung des SameSite-Standards sind die Konfigurationsoptionen für diese vier Features jedoch inkonsistent.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="6dcfe-131">Die relevanten Konfigurations Abschnitte und-Attribute mit Standardwerten sind unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="6dcfe-132">Wenn `SameSite` für eine Funktion kein-Attribut oder ein verknüpftes Attribut vorhanden ist `Secure` , greift die Funktion auf die Standardwerte zurück, die im `system.web/httpCookies` oben beschriebenen Abschnitt konfiguriert wurden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="6dcfe-133">**Hinweis**: "nicht angegeben" ist zurzeit nur für verfügbar `system.web/httpCookies@sameSite` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="6dcfe-134">Wir hoffen, dass Sie den zuvor gezeigten cookiesamesite-Attributen in zukünftigen Updates eine ähnliche Syntax hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="6dcfe-135">`(SameSiteMode)(-1)`Die Einstellung im Code funktioniert weiterhin auf Instanzen dieser Cookies. \*</span><span class="sxs-lookup"><span data-stu-id="6dcfe-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="6dcfe-136">Neuzuweisen von .net-apps</span><span class="sxs-lookup"><span data-stu-id="6dcfe-136">Retarget .NET apps</span></span>

<span data-ttu-id="6dcfe-137">Ziel für .NET 4.7.2 oder höher:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="6dcfe-138">Stellen Sie sicher, dass *web.config* Folgendes enthält:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="6dcfe-139">Im [.net-Migrations Handbuch](/dotnet/framework/migration-guide/) finden Sie weitere Details.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="6dcfe-140">Überprüfen Sie, ob nuget-Pakete im Projekt auf die richtige Framework-Version abzielen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="6dcfe-141">Sie können die richtige Frameworkversion überprüfen, indem Sie die *packages.config* Datei untersuchen, z. b.:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="6dcfe-142">In der vorangehenden *packages.config* Datei hat das `Microsoft.ApplicationInsights` Paket Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="6dcfe-143">Ist für .NET 4.5.1 konzipiert.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="6dcfe-144">Muss das- `targetFramework` Attribut auf aktualisiert `net472` werden, wenn ein aktualisiertes Paket für das Framework-Ziel vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="6dcfe-145">.NET-Versionen vor 4.7.2</span><span class="sxs-lookup"><span data-stu-id="6dcfe-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="6dcfe-146">Microsoft bietet keine Unterstützung für .NET-Versionen, die 4.7.2 zum Schreiben desselben-Site-Cookie-Attributs verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="6dcfe-147">Wir haben keine zuverlässige Methode für Folgendes gefunden:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="6dcfe-148">Stellen Sie sicher, dass das Attribut basierend auf der Browserversion richtig geschrieben wurde.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="6dcfe-149">Abfangen und Anpassen von Authentifizierungs-und Sitzungs Cookies in älteren Framework-Versionen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="6dcfe-150">Änderungen im Dezember-patchverhalten</span><span class="sxs-lookup"><span data-stu-id="6dcfe-150">December patch behavior changes</span></span>

<span data-ttu-id="6dcfe-151">Die spezifische Behavior Change für .NET Framework gibt an, wie die- `SameSite` Eigenschaft den `None` Wert interpretiert:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="6dcfe-152">Vor dem Patch war der Wert `None` :</span><span class="sxs-lookup"><span data-stu-id="6dcfe-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="6dcfe-153">Geben Sie das Attribut überhaupt nicht aus.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="6dcfe-154">Nach dem Patch:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-154">After the patch:</span></span>
  * <span data-ttu-id="6dcfe-155">Der Wert bedeutet, dass `None` das Attribut mit dem Wert ausgegeben wird `None` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="6dcfe-156">`SameSite` `(SameSiteMode)(-1)` Der Wert bewirkt, dass das Attribut nicht ausgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="6dcfe-157">Der Standardwert von SameSite für die Formular Authentifizierung und Sitzungs Zustands Cookies wurde von `None` in geändert `Lax` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="6dcfe-158">Zusammenfassung der Auswirkungen von Änderungen auf Browser</span><span class="sxs-lookup"><span data-stu-id="6dcfe-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="6dcfe-159">Wenn Sie den Patch installieren und ein Cookie mit ausgeben `SameSite.None` , geschieht eins von zwei Dingen:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="6dcfe-160">Chrome V80 behandelt dieses Cookie gemäß der neuen Implementierung und erzwingt nicht die gleichen Website Einschränkungen für das Cookie.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="6dcfe-161">Alle Browser, die nicht zur Unterstützung der neuen Implementierung aktualisiert wurden, folgen der alten Implementierung.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="6dcfe-162">Die alte Implementierung besagt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-162">The old implementation says:</span></span>
  * <span data-ttu-id="6dcfe-163">Wenn Sie einen Wert sehen, den Sie nicht verstehen, ignorieren Sie ihn, und wechseln Sie zu strikt denselben Website Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="6dcfe-164">Entweder wird die app in Chrome unterbrochen, oder Sie unterbrechen an zahlreichen anderen stellen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="6dcfe-165">Verlauf und Änderungen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-165">History and changes</span></span>

<span data-ttu-id="6dcfe-166">Die SameSite-Unterstützung wurde zunächst in .NET 4.7.2 mithilfe des [Entwurfs Standards 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)implementiert.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="6dcfe-167">Die Updates vom 19. November 2019 für Windows aktualisierte .NET 4.7.2 + von der 2016-Standard-auf den 2019-Standard.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="6dcfe-168">Für andere Versionen von Windows werden weitere Updates demnächst durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="6dcfe-169">Weitere Informationen finden Sie unter <xref:samesite/kbs-samesite>.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="6dcfe-170">Der 2019-Entwurf der SameSite-Spezifikation:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="6dcfe-171">Ist **nicht** abwärts kompatibel mit dem 2016-Entwurf.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="6dcfe-172">Weitere Informationen finden Sie [unter unterstützen älterer Browser](#sob) in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="6dcfe-173">Gibt an, dass Cookies `SameSite=Lax` standardmäßig als behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="6dcfe-174">Gibt Cookies an, die explizit bestätigt werden, um `SameSite=None` die standortübergreifende Übermittlung zu aktivieren, sollte ebenfalls als gekennzeichnet werden `Secure` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="6dcfe-175">Wird von Patches unterstützt, die wie in den oben aufgeführten KB beschrieben ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="6dcfe-176">Ist für die standardmäßige Aktivierung durch [Chrome](https://chromestatus.com/feature/5088147346030592) in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="6dcfe-177">Die Umstellung auf diesen Standard in 2019 wurde gestartet.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"></a>

## <a name="known-issues"></a><span data-ttu-id="6dcfe-178">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="6dcfe-178">Known Issues</span></span>

<span data-ttu-id="6dcfe-179">Da die Entwurfs Spezifikationen 2016 und 2019 nicht kompatibel sind, führt das .NET Framework-Update von November 2019 einige Änderungen ein, die möglicherweise unterbrochen werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="6dcfe-180">Sitzungs Status-und Formular Authentifizierungs Cookies werden nun als nicht angegeben, sondern in das Netzwerk geschrieben `Lax` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="6dcfe-181">Obwohl die meisten apps mit `SameSite=Lax` Cookies arbeiten, werden apps, die über Websites oder Anwendungen bereitstellen, die verwenden, `iframe` möglicherweise feststellen, dass Ihre Sitzungs Status-oder Formular Autorisierungs Cookies nicht wie erwartet verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="6dcfe-182">Um dieses Problem zu beheben, ändern Sie den `cookieSameSite` Wert im entsprechenden Konfigurations Abschnitt, wie bereits erläutert.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="6dcfe-183">Bei httpCookies, die explizit `SameSite=None` im Code oder in der Konfiguration festgelegt wurden, wird dieser Wert jetzt mit dem Cookie geschrieben, während er zuvor ausgelassen wurde.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="6dcfe-184">Dies kann zu Problemen mit älteren Browsern führen, die nur den 2016 Draft-Standard unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="6dcfe-185">Wenn Sie auf Browser abzielen, die den 2019-Entwurfs Standard mit Cookies unterstützen `SameSite=None` , denken Sie daran, Sie auch zu markieren, `Secure` oder Sie werden nicht erkannt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="6dcfe-186">Verwenden Sie die app-Einstellung, um das 2016-Verhalten beim nicht schreiben wiederherzustellen `SameSite=None` `aspnet:SupressSameSiteNone=true` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="6dcfe-187">Beachten Sie, dass dies für alle httpCookies in der APP gilt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="6dcfe-188">Azure App Service – SameSite-Cookie-Behandlung</span><span class="sxs-lookup"><span data-stu-id="6dcfe-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="6dcfe-189">Informationen dazu, wie Azure App Service SameSite-Verhalten in .NET 4.7.2-apps konfiguriert, finden Sie unter [Azure App Service – SameSite Cookie Handling und .NET Framework 4.7.2-Patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="6dcfe-190">Unterstützung älterer Browser</span><span class="sxs-lookup"><span data-stu-id="6dcfe-190">Supporting older browsers</span></span>

<span data-ttu-id="6dcfe-191">Der 2016 SameSite-Standard hat festgestellt, dass unbekannte Werte als Werte behandelt werden müssen `SameSite=Strict` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="6dcfe-192">Apps, auf die von älteren Browsern zugegriffen wird, die den 2016 SameSite-Standard unterstützen, können unterbrechen, wenn Sie eine SameSite-Eigenschaft mit dem Wert erhalten `None` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="6dcfe-193">Web-Apps müssen die Browser Erkennung implementieren, wenn Sie ältere Browser unterstützen möchten.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="6dcfe-194">ASP.NET implementiert die Browser Erkennung nicht, da die Werte von Benutzer-Agents stark flüchtig sind und häufig geändert werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="6dcfe-195">Der Ansatz von Microsoft, das Problem zu beheben, besteht darin, Sie bei der Implementierung von Browser Erkennungs Komponenten zu unterstützen, um das `sameSite=None` Attribut aus Cookies zu entfernen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="6dcfe-196">Die Ratschläge von Google bestand darin, doppelte Cookies auszugeben, eine mit dem neuen Attribut und eine ohne das-Attribut.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="6dcfe-197">Wir werden jedoch die Ratschläge von Google in Erwägung gezogen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="6dcfe-198">Einige Browser, insbesondere Mobile Browser, haben sehr geringe Beschränkungen hinsichtlich der Anzahl von Cookies, die von einer Website oder von einem Domänen Namen gesendet werden können.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="6dcfe-199">Das Senden mehrerer Cookies, insbesondere von großen Cookies wie Authentifizierungs Cookies, kann das Mobile Browser Limit sehr schnell erreichen, was zu app-Fehlern führt, die schwer zu diagnostizieren und zu beheben sind.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="6dcfe-200">Außerdem gibt es als Framework ein großes Ökosystem aus Code und Komponenten von Drittanbietern, die möglicherweise nicht aktualisiert werden, um einen doppelten Cookie-Ansatz zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="6dcfe-201">Der Browser Erkennungs Code, der in den Beispielprojekten in [diesem GitHub-Repository]() verwendet wird, ist in zwei Dateien enthalten.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="6dcfe-202">C#-SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="6dcfe-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="6dcfe-203">VB samesitesupport. vb</span><span class="sxs-lookup"><span data-stu-id="6dcfe-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="6dcfe-204">Diese Erkennungen sind die am häufigsten verwendeten Browser-Agents, die den 2016-Standard unterstützen und für die das Attribut vollständig entfernt werden muss.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="6dcfe-205">Es ist nicht als umfassende Implementierung gemeint:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="6dcfe-206">In Ihrer APP werden möglicherweise Browser angezeigt, die für unsere Test Websites nicht angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="6dcfe-207">Sie sollten darauf vorbereitet sein, Erkennungen nach Bedarf für Ihre Umgebung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="6dcfe-208">Die Art und Weise, wie Sie die Erkennung verknüpfen, variiert entsprechend der von Ihnen verwendeten .NET-Version und des verwendeten Webframe Works.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="6dcfe-209">Der folgende Code kann an der [HttpCookie](/dotnet/api/system.web.httpcookie) -Aufruf Site aufgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="6dcfe-210">Weitere Informationen finden Sie in den folgenden ASP.NET 4.7.2 SameSite Cookie-Themen:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="6dcfe-211">C#-MVC</span><span class="sxs-lookup"><span data-stu-id="6dcfe-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="6dcfe-212">C#-WebForms</span><span class="sxs-lookup"><span data-stu-id="6dcfe-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="6dcfe-213">VB-WebForms</span><span class="sxs-lookup"><span data-stu-id="6dcfe-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="6dcfe-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="6dcfe-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="6dcfe-215">Sicherstellen, dass Ihre Website an https umgeleitet wird</span><span class="sxs-lookup"><span data-stu-id="6dcfe-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="6dcfe-216">Für ASP.NET 4. x, WebForms und MVC kann [das URL-Rewrite-Feature von IIS](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) verwendet werden, um alle Anforderungen an HTTPS umzuleiten.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="6dcfe-217">Der folgende XML-Code zeigt eine Beispiel Regel:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-217">The following XML shows a sample rule:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="6dcfe-218">Bei lokalen Installationen von IIS- [URL-Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) ist ein optionales Feature, das möglicherweise installiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="6dcfe-219">Testen von Apps für SameSite-Probleme</span><span class="sxs-lookup"><span data-stu-id="6dcfe-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="6dcfe-220">Sie müssen Ihre APP mit den von Ihnen unterstützten Browsern testen und die Szenarien durchlaufen, in denen Cookies beteiligt sind.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="6dcfe-221">Cookie-Szenarios in der Regel</span><span class="sxs-lookup"><span data-stu-id="6dcfe-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="6dcfe-222">Anmeldeformulare</span><span class="sxs-lookup"><span data-stu-id="6dcfe-222">Login forms</span></span>
* <span data-ttu-id="6dcfe-223">Externe Anmelde Mechanismen, z. b. Facebook, Azure AD, OAuth und oidc</span><span class="sxs-lookup"><span data-stu-id="6dcfe-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="6dcfe-224">Seiten, die Anforderungen von anderen Websites annehmen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="6dcfe-225">Seiten in Ihrer APP, die in iframes eingebettet werden sollen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="6dcfe-226">Sie sollten überprüfen, ob Cookies in Ihrer APP ordnungsgemäß erstellt, persistent gespeichert und gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="6dcfe-227">Apps, die mit Remote Standorten interagieren, z. b. durch die Anmeldung von Drittanbietern, benötigen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="6dcfe-228">Testen Sie die Interaktion in mehreren Browsern.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="6dcfe-229">Anwenden der in diesem Dokument beschriebenen [Browser Erkennung und-Entschärfung](#sob) .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="6dcfe-230">Testen Sie Web-Apps mithilfe einer Client Version, die das neue SameSite-Verhalten abonnieren kann.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="6dcfe-231">Chrome, Firefox und Chromium Edge verfügen über neue Feature-Flags, die für Tests verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="6dcfe-232">Nachdem Ihre APP die SameSite-Patches angewendet hat, testen Sie Sie mit älteren Client Versionen, insbesondere Safari.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="6dcfe-233">Weitere Informationen finden Sie [unter unterstützen älterer Browser](#sob) in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="6dcfe-234">Testen mit Chrome</span><span class="sxs-lookup"><span data-stu-id="6dcfe-234">Test with Chrome</span></span>

<span data-ttu-id="6dcfe-235">Chrome 78 + liefert irreführende Ergebnisse, da eine vorübergehende Entschärfung vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="6dcfe-236">Die temporäre Chrome-Minderung von 78 und höher ermöglicht Cookies, die weniger als zwei Minuten alt sind.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="6dcfe-237">Chrome 76 oder 77 mit aktivierten geeigneten testflags bietet genauere Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="6dcfe-238">Zum Testen des neuen SameSite-Verhaltens umschalten `chrome://flags/#same-site-by-default-cookies` in **aktiviert**.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="6dcfe-239">Ältere Versionen von Chrome (75 und niedriger) werden mit der neuen `None` Einstellung gemeldet.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="6dcfe-240">Siehe [Unterstützung älterer Browser](#sob) in diesem Dokument.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="6dcfe-241">Google stellt keine älteren Chrome-Versionen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="6dcfe-242">Befolgen Sie die Anweisungen unter [Herunterladen von Chrom](https://www.chromium.org/getting-involved/download-chromium) , um ältere Versionen von Chrome zu testen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="6dcfe-243">Laden Sie Chrome **nicht** von den von Ihnen bereitgestellten Links herunter, indem Sie nach älteren Versionen von Chrome suchen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="6dcfe-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="6dcfe-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="6dcfe-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="6dcfe-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="6dcfe-246">Wenn Sie keine 64-Bit-Version von Windows verwenden, können Sie den [omahaproxy-Viewer](https://omahaproxy.appspot.com/) verwenden, um zu überprüfen, welcher Chrom Branch Chrome 74 (v 74.0.3729.108) entspricht, indem Sie die [von Chrom bereitgestellten Anweisungen](https://www.chromium.org/getting-involved/download-chromium)verwenden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="6dcfe-247">Beginnend mit der Canary-Version `80.0.3975.0` kann die vorübergehende Entschärfung von Lax und Post zu Testzwecken deaktiviert werden. dazu wird das neue Flag verwendet `--enable-features=SameSiteDefaultChecksMethodRigorously` , um das Testen von Websites und Diensten im Endzustand des Features zuzulassen, bei dem die Entschärfung entfernt wurde.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="6dcfe-248">Weitere Informationen finden Sie in den Informationen zu den [Software Update](https://www.chromium.org/updates/same-site) -Projekten in der Projektwebsite.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="6dcfe-249">Test mit Chrome 80 und höher</span><span class="sxs-lookup"><span data-stu-id="6dcfe-249">Test with Chrome 80+</span></span>

<span data-ttu-id="6dcfe-250">[Laden Sie](https://www.google.com/chrome/) eine Version von Chrome herunter, die Ihr neues Attribut unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="6dcfe-251">Zum Zeitpunkt des Schreibens ist die aktuelle Version Chrome 80.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="6dcfe-252">Chrome 80 benötigt das Flag `chrome://flags/#same-site-by-default-cookies` , das für die Verwendung des neuen Verhaltens aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="6dcfe-253">Außerdem sollten Sie ( `chrome://flags/#cookies-without-same-site-must-be-secure` ) aktivieren, um das bevorstehende Verhalten von Cookies zu testen, für die kein SameSite-Attribut aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="6dcfe-254">Chrome 80 ist als Ziel festzulegen, damit der Schalter Cookies ohne das-Attribut als behandelt `SameSite=Lax` , wenn für bestimmte Anforderungen eine Zeitüberschreitung aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="6dcfe-255">Zum Deaktivieren der Zeitüberschreitung für die Zeitüberschreitung kann Chrome 80 mit dem folgenden Befehlszeilenargument gestartet werden:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="6dcfe-256">Chrome 80 enthält Warnmeldungen in der Browser Konsole über fehlende SameSite-Attribute.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="6dcfe-257">Verwenden Sie F12, um die Browser Konsole zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="6dcfe-258">Testen mit Safari</span><span class="sxs-lookup"><span data-stu-id="6dcfe-258">Test with Safari</span></span>

<span data-ttu-id="6dcfe-259">Safari 12 hat den vorherigen Entwurf streng implementiert und schlägt fehl, wenn der neue `None` Wert in einem Cookie liegt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="6dcfe-260">`None` wird über den Browser Erkennungs Code, der ältere Browser in diesem Dokument [unterstützt](#sob) , vermieden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="6dcfe-261">Testen Sie Safari 12-, Safari 13-und WebKit-basierte Anmeldungen im Betriebssystem Format unter Verwendung von msal, Adal oder einer beliebigen Bibliothek, die Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="6dcfe-262">Das Problem hängt von der zugrunde liegenden Betriebssystemversion ab.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="6dcfe-263">OSX-mujave (10,14) und IOS 12 haben bekanntermaßen Kompatibilitätsprobleme mit dem neuen SameSite-Verhalten.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="6dcfe-264">Durch ein Upgrade des Betriebssystems auf OSX Catalina (10,15) oder IOS 13 wird das Problem behoben.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="6dcfe-265">Safari verfügt derzeit nicht über ein Opt-in-Flag zum Testen des neuen Spezifikations Verhaltens.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="6dcfe-266">Testen mit Firefox</span><span class="sxs-lookup"><span data-stu-id="6dcfe-266">Test with Firefox</span></span>

<span data-ttu-id="6dcfe-267">Die Firefox-Unterstützung für den neuen Standard kann auf Version 68 + getestet werden, indem Sie sich auf der `about:config` Seite mit dem Feature-Flag anmelden `network.cookie.sameSite.laxByDefault` .</span><span class="sxs-lookup"><span data-stu-id="6dcfe-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="6dcfe-268">Es gab keine Berichte über Kompatibilitätsprobleme mit älteren Versionen von Firefox.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="6dcfe-269">Test mit Edge-Browser (Legacy)</span><span class="sxs-lookup"><span data-stu-id="6dcfe-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="6dcfe-270">Edge unterstützt den alten SameSite-Standard.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="6dcfe-271">Edge Version 44 + hat keine bekannten Kompatibilitätsprobleme mit dem neuen Standard.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="6dcfe-272">Testen mit Edge (Chrom)</span><span class="sxs-lookup"><span data-stu-id="6dcfe-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="6dcfe-273">SameSite-Flags werden auf der `edge://flags/#same-site-by-default-cookies` Seite festgelegt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="6dcfe-274">Es wurden keine Kompatibilitätsprobleme mit Edge-Chrom erkannt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="6dcfe-275">Testen mit einem Elektron</span><span class="sxs-lookup"><span data-stu-id="6dcfe-275">Test with Electron</span></span>

<span data-ttu-id="6dcfe-276">Zu den Electron-Versionen zählen ältere Versionen von Chromium.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="6dcfe-277">Beispielsweise ist die Version des von Teams verwendeten Elektrons Chrom 66, das das ältere Verhalten zeigt.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="6dcfe-278">Sie müssen ihre eigenen Kompatibilitätstests mit der Version des von Ihrem Produkt verwendeten-Elektronen durchführen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="6dcfe-279">Siehe [Unterstützung älterer Browser](#sob).</span><span class="sxs-lookup"><span data-stu-id="6dcfe-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="6dcfe-280">Wiederherstellen von SameSite-Patches</span><span class="sxs-lookup"><span data-stu-id="6dcfe-280">Reverting SameSite patches</span></span>

<span data-ttu-id="6dcfe-281">Sie können das aktualisierte SameSite-Verhalten in .NET Framework-apps auf das vorherige Verhalten zurücksetzen, bei dem das SameSite-Attribut nicht für einen Wert von ausgegeben wird `None` , und die Authentifizierungs-und Sitzungs Cookies zurücksetzen, um den Wert nicht auszugeben.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="6dcfe-282">Dies sollte als *äußerst vorübergehende Korrektur*angesehen werden, da die Chrome-Änderungen externe Post-Anforderungen oder die Authentifizierung für Benutzer mit Browsern unterstützen, die die Änderungen am Standard unterstützen.</span><span class="sxs-lookup"><span data-stu-id="6dcfe-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="6dcfe-283">Zurücksetzen des .NET 4.7.2-Verhaltens</span><span class="sxs-lookup"><span data-stu-id="6dcfe-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="6dcfe-284">Aktualisieren Sie *web.config* , um die folgenden Konfigurationseinstellungen einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="6dcfe-284">Update *web.config* to include the following configuration settings:</span></span>

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="6dcfe-285">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-285">Additional resources</span></span>

* [<span data-ttu-id="6dcfe-286">Anstehende SameSite-Cookie-Änderungen in ASP.net und ASP.net Core</span><span class="sxs-lookup"><span data-stu-id="6dcfe-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="6dcfe-287">Tipps zum Testen und Debuggen von SameSite-Standard und "SameSite = None;" Sichere Cookies</span><span class="sxs-lookup"><span data-stu-id="6dcfe-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="6dcfe-288">Chromium-Blog: Entwickler: machen Sie sich bereit für neue SameSite = None; Sichere Cookie-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="6dcfe-289">Erläuterte SameSite-Cookies</span><span class="sxs-lookup"><span data-stu-id="6dcfe-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="6dcfe-290">Chrome-Updates</span><span class="sxs-lookup"><span data-stu-id="6dcfe-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="6dcfe-291">.Net SameSite-Patches</span><span class="sxs-lookup"><span data-stu-id="6dcfe-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="6dcfe-292">Azure-Webanwendungen Website Informationen</span><span class="sxs-lookup"><span data-stu-id="6dcfe-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="6dcfe-293">Informationen zu gleichen Website Informationen zu Azure ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="6dcfe-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
