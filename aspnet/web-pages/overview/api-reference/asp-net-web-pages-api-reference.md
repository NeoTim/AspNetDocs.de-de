---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Webseiten (Razor) API-Schnellreferenz | Microsoft Docs
author: Rick-Anderson
description: Diese Seite enthält eine Liste mit kurzen Beispielen für die am häufigsten verwendeten Objekte, Eigenschaften und Methoden zum Programmieren ASP.NET Webseiten mit Razor-Syntax.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675850"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="dd589-103">ASP.NET-Webseiten-API-Schnellreferenz</span><span class="sxs-lookup"><span data-stu-id="dd589-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="dd589-104"> von [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dd589-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dd589-105">Diese Seite enthält eine Liste mit kurzen Beispielen für die am häufigsten verwendeten Objekte, Eigenschaften und Methoden zum Programmieren ASP.NET Webseiten mit Razor-Syntax.</span><span class="sxs-lookup"><span data-stu-id="dd589-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="dd589-106">Beschreibungen mit "(v2)" wurden in ASP.NET Webseiten Version 2 eingeführt.</span><span class="sxs-lookup"><span data-stu-id="dd589-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="dd589-107">Die API-Referenzdokumentation finden Sie in der [ASP.NET Webseiten-Referenzdokumentation](https://go.microsoft.com/fwlink/?LinkId=208659) auf MSDN.</span><span class="sxs-lookup"><span data-stu-id="dd589-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="dd589-108">Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="dd589-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="dd589-109">ASP.NET Webseiten (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="dd589-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="dd589-110">Dieses Tutorial funktioniert auch mit ASP.NET Webseiten 2 und ASP.NET Webseiten 1.0 (mit Ausnahme von Features, die als v2 gekennzeichnet sind).</span><span class="sxs-lookup"><span data-stu-id="dd589-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="dd589-111">Diese Seite enthält Referenzinformationen für Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dd589-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="dd589-112">Klassen</span><span class="sxs-lookup"><span data-stu-id="dd589-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="dd589-113">Daten</span><span class="sxs-lookup"><span data-stu-id="dd589-113">Data</span></span>](#Data)
- [<span data-ttu-id="dd589-114">Hilfsmethoden</span><span class="sxs-lookup"><span data-stu-id="dd589-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="dd589-115">Validation</span><span class="sxs-lookup"><span data-stu-id="dd589-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="dd589-116">Klassen</span><span class="sxs-lookup"><span data-stu-id="dd589-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="dd589-117">Enthält Daten, die von allen Seiten in der Anwendung gemeinsam genutzt werden können.</span><span class="sxs-lookup"><span data-stu-id="dd589-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="dd589-118">Sie können die `App` dynamische Eigenschaft verwenden, um auf dieselben Daten zuzugreifen, wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="dd589-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="dd589-119">Konvertiert einen Zeichenfolgenwert in einen booleschen Wert (true/false).</span><span class="sxs-lookup"><span data-stu-id="dd589-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="dd589-120">Gibt false oder den angegebenen Wert zurück, wenn die Zeichenfolge nicht true/false darstellt.</span><span class="sxs-lookup"><span data-stu-id="dd589-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="dd589-121">Konvertiert einen Zeichenfolgenwert in Datum/Uhrzeit.</span><span class="sxs-lookup"><span data-stu-id="dd589-121">Converts a string value to date/time.</span></span> <span data-ttu-id="dd589-122">Gibt `DateTime.MinValue` den angegebenen Wert zurück, wenn die Zeichenfolge kein Datum/Uhrzeit darstellt.</span><span class="sxs-lookup"><span data-stu-id="dd589-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="dd589-123">Konvertiert einen Zeichenfolgenwert in einen Dezimalwert.</span><span class="sxs-lookup"><span data-stu-id="dd589-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="dd589-124">Gibt 0.0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keinen Dezimalwert darstellt.</span><span class="sxs-lookup"><span data-stu-id="dd589-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="dd589-125">Konvertiert einen Zeichenfolgenwert in einen float.</span><span class="sxs-lookup"><span data-stu-id="dd589-125">Converts a string value to a float.</span></span> <span data-ttu-id="dd589-126">Gibt 0.0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keinen Dezimalwert darstellt.</span><span class="sxs-lookup"><span data-stu-id="dd589-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="dd589-127">Konvertiert einen Zeichenfolgenwert in eine ganze Zahl.</span><span class="sxs-lookup"><span data-stu-id="dd589-127">Converts a string value to an integer.</span></span> <span data-ttu-id="dd589-128">Gibt 0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keine ganze Zahl darstellt.</span><span class="sxs-lookup"><span data-stu-id="dd589-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="dd589-129">Erstellt eine browserkompatible URL aus einem lokalen Dateipfad mit optionalen zusätzlichen Pfadteilen.</span><span class="sxs-lookup"><span data-stu-id="dd589-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="dd589-130">Rendert *Wert* als HTML-Markup, anstatt ihn als HTML-codierte Ausgabe zu rendern.</span><span class="sxs-lookup"><span data-stu-id="dd589-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="dd589-131">Gibt true zurück, wenn der Wert von einer Zeichenfolge in den angegebenen Typ konvertiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="dd589-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="dd589-132">Gibt true zurück, wenn das Objekt oder die Variable keinen Wert hat.</span><span class="sxs-lookup"><span data-stu-id="dd589-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="dd589-133">Gibt true zurück, wenn es sich bei der Anforderung um einen POST-Test handelt.</span><span class="sxs-lookup"><span data-stu-id="dd589-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="dd589-134">(Anfangsanforderungen sind in der Regel ein GET.)</span><span class="sxs-lookup"><span data-stu-id="dd589-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="dd589-135">Gibt den Pfad einer Layoutseite an, die auf diese Seite angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="dd589-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="dd589-136">Enthält Daten, die zwischen der Seite, Layoutseiten und Teilseiten in der aktuellen Anforderung freigegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="dd589-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="dd589-137">Sie können die `Page` dynamische Eigenschaft verwenden, um auf dieselben Daten zuzugreifen, wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="dd589-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="dd589-138">(Layoutseiten) Rendert den Inhalt einer Inhaltsseite, die sich nicht in benannten Abschnitten befindet.</span><span class="sxs-lookup"><span data-stu-id="dd589-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="dd589-139">Rendert eine Inhaltsseite mit dem angegebenen Pfad und optionalen zusätzlichen Daten.</span><span class="sxs-lookup"><span data-stu-id="dd589-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="dd589-140">Sie können die Werte der `PageData` zusätzlichen Parameter aus der Position (Beispiel 1) oder der Taste (Beispiel 2) abrufen.</span><span class="sxs-lookup"><span data-stu-id="dd589-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="dd589-141">(Layoutseiten) Rendert einen Inhaltsabschnitt mit einem Namen.</span><span class="sxs-lookup"><span data-stu-id="dd589-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="dd589-142">Legen Sie *fest, dass* ein Abschnitt optional ist.</span><span class="sxs-lookup"><span data-stu-id="dd589-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="dd589-143">Ruft den Wert eines HTTP-Cookies ab oder legt den Wert fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="dd589-144">Ruft die Dateien ab, die in der aktuellen Anforderung hochgeladen wurden.</span><span class="sxs-lookup"><span data-stu-id="dd589-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="dd589-145">Ruft Daten ab, die in einem Formular (als Zeichenfolgen) gebucht wurden.</span><span class="sxs-lookup"><span data-stu-id="dd589-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="dd589-146">`Request[key]`überprüft sowohl `Request.Form` die `Request.QueryString` als auch die Auflistungen.</span><span class="sxs-lookup"><span data-stu-id="dd589-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="dd589-147">Ruft Daten ab, die in der URL-Abfragezeichenfolge angegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="dd589-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="dd589-148">`Request[key]`überprüft sowohl `Request.Form` die `Request.QueryString` als auch die Auflistungen.</span><span class="sxs-lookup"><span data-stu-id="dd589-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="dd589-149">Deaktiviert selektiv die Anforderungsüberprüfung für ein Formularelement, einen Abfragezeichenfolgenwert, ein Cookie oder einen Headerwert.</span><span class="sxs-lookup"><span data-stu-id="dd589-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="dd589-150">Die Anforderungsüberprüfung ist standardmäßig aktiviert und verhindert, dass Benutzer Markup oder andere potenziell gefährliche Inhalte veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="dd589-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="dd589-151">Fügt der Antwort einen HTTP-Serverheader hinzu.</span><span class="sxs-lookup"><span data-stu-id="dd589-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="dd589-152">Speichert die Seitenausgabe für eine bestimmte Zeit zwischen.</span><span class="sxs-lookup"><span data-stu-id="dd589-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="dd589-153">Optional das *Gleiten* festlegen, um das Timeout für jeden Seitenzugriff zurückzusetzen, und *varyByParams,* um verschiedene Versionen der Seite für jede unterschiedliche Abfragezeichenfolge in der Seitenanforderung zwischenzuspeichern.</span><span class="sxs-lookup"><span data-stu-id="dd589-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="dd589-154">Leitet die Browseranforderung an einen neuen Speicherort um.</span><span class="sxs-lookup"><span data-stu-id="dd589-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="dd589-155">Legt den an den Browser gesendeten HTTP-Statuscode fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="dd589-156">Schreibt den Inhalt von *Daten* in die Antwort mit einem optionalen MIME-Typ.</span><span class="sxs-lookup"><span data-stu-id="dd589-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="dd589-157">Schreibt den Inhalt einer Datei in die Antwort.</span><span class="sxs-lookup"><span data-stu-id="dd589-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="dd589-158">(Layoutseiten) Definiert einen Inhaltsabschnitt mit einem Namen.</span><span class="sxs-lookup"><span data-stu-id="dd589-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="dd589-159">Decodiert eine Zeichenfolge, die HTML-codiert ist.</span><span class="sxs-lookup"><span data-stu-id="dd589-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="dd589-160">Codiert eine Zeichenfolge für das Rendern in HTML-Markup.</span><span class="sxs-lookup"><span data-stu-id="dd589-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="dd589-161">Gibt den physischen Serverpfad für den angegebenen virtuellen Pfad zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="dd589-162">Decodiert Text von einer URL.</span><span class="sxs-lookup"><span data-stu-id="dd589-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="dd589-163">Kodiert Text, um ihn in eine URL einzuzahlen.</span><span class="sxs-lookup"><span data-stu-id="dd589-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="dd589-164">Ruft einen Wert ab oder legt ihn fest, bis der Benutzer den Browser schließt.</span><span class="sxs-lookup"><span data-stu-id="dd589-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="dd589-165">Zeigt eine Zeichenfolgendarstellung des Objektwerts an.</span><span class="sxs-lookup"><span data-stu-id="dd589-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="dd589-166">Ruft zusätzliche Daten von der URL ab (z. B. */MyPage/ExtraData*).</span><span class="sxs-lookup"><span data-stu-id="dd589-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="dd589-167">Ändert das Kennwort für den angegebenen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="dd589-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="dd589-168">Bestätigt ein Konto mithilfe des Kontobestätigungstokens.</span><span class="sxs-lookup"><span data-stu-id="dd589-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="dd589-169">Erstellt ein neues Benutzerkonto mit dem angegebenen Benutzernamen und Kennwort.</span><span class="sxs-lookup"><span data-stu-id="dd589-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="dd589-170">Um ein Bestätigungstoken zu benötigen, übergeben Sie true für *requireConfirmationToken.*</span><span class="sxs-lookup"><span data-stu-id="dd589-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="dd589-171">Ruft den Ganzzahlbezeichner für den aktuell angemeldeten Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="dd589-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="dd589-172">Ruft den Namen für den aktuell angemeldeten Benutzer ab.</span><span class="sxs-lookup"><span data-stu-id="dd589-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="dd589-173">Generiert ein Kennwort-Reset-Token, das per E-Mail an einen Benutzer gesendet werden kann, damit der Benutzer das Kennwort zurücksetzen kann.</span><span class="sxs-lookup"><span data-stu-id="dd589-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="dd589-174">Gibt die Benutzer-ID aus dem Benutzernamen zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="dd589-175">Gibt true zurück, wenn der aktuelle Benutzer angemeldet ist.</span><span class="sxs-lookup"><span data-stu-id="dd589-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="dd589-176">Gibt true zurück, wenn der Benutzer bestätigt wurde (z. B. durch eine Bestätigungs-E-Mail).</span><span class="sxs-lookup"><span data-stu-id="dd589-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="dd589-177">Gibt true zurück, wenn der Name des aktuellen Benutzers mit dem angegebenen Benutzernamen übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="dd589-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="dd589-178">Meldet den Benutzer an, indem er ein Authentifizierungstoken im Cookie festlegt.</span><span class="sxs-lookup"><span data-stu-id="dd589-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="dd589-179">Meldet den Benutzer ab, indem das Authentifizierungstoken-Cookie entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="dd589-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="dd589-180">Legt den HTTP-Status auf 401 (Nicht autorisiert) fest, wenn der Benutzer nicht authentifiziert ist.</span><span class="sxs-lookup"><span data-stu-id="dd589-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="dd589-181">Wenn der aktuelle Benutzer nicht Mitglied einer der angegebenen Rollen ist, wird der HTTP-Status auf 401 (Nicht autorisiert) festgelegt.</span><span class="sxs-lookup"><span data-stu-id="dd589-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="dd589-182">Wenn der aktuelle Benutzer nicht der durch *Benutzername*angegebene Benutzer ist, wird der HTTP-Status auf 401 (Unautorisiert) festgelegt.</span><span class="sxs-lookup"><span data-stu-id="dd589-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="dd589-183">Wenn das Kennwortzurücksetzungstoken gültig ist, wird das Kennwort des Benutzers in das neue Kennwort geändert.</span><span class="sxs-lookup"><span data-stu-id="dd589-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="dd589-184">Daten</span><span class="sxs-lookup"><span data-stu-id="dd589-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="dd589-185">Führt *SQLstatement* (mit optionalen Parametern) wie INSERT, DELETE oder UPDATE aus und gibt eine Anzahl betroffener Datensätze zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="dd589-186">Gibt die Identitätsspalte aus der zuletzt eingefügten Zeile zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="dd589-187">Öffnet entweder die angegebene Datenbankdatei oder die Datenbank, die mithilfe einer benannten Verbindungszeichenfolge aus der *Datei Web.config* angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="dd589-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="dd589-188">Öffnet eine Datenbank mit der Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="dd589-188">Opens a database using the connection string.</span></span> <span data-ttu-id="dd589-189">(Dies steht `Database.Open`im Gegensatz zu , die einen Verbindungszeichenfolgennamen verwendet.)</span><span class="sxs-lookup"><span data-stu-id="dd589-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="dd589-190">Fragt die Datenbank mithilfe von *SQLstatement* ab (optional übergebene Parameter) und gibt die Ergebnisse als Auflistung zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="dd589-191">Führt *SQLstatement* (mit optionalen Parametern) aus und gibt einen einzelnen Datensatz zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="dd589-192">Führt *SQLstatement* (mit optionalen Parametern) aus und gibt einen einzelnen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="dd589-193">Hilfsmethoden</span><span class="sxs-lookup"><span data-stu-id="dd589-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="dd589-194">Rendert den Google Analytics JavaScript-Code für die angegebene ID.</span><span class="sxs-lookup"><span data-stu-id="dd589-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="dd589-195">Rendert den StatCounter Analytics JavaScript-Code für das angegebene Projekt.</span><span class="sxs-lookup"><span data-stu-id="dd589-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="dd589-196">Rendert den Yahoo Analytics JavaScript-Code für das angegebene Konto.</span><span class="sxs-lookup"><span data-stu-id="dd589-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="dd589-197">Übergibt eine Suche an Bing.</span><span class="sxs-lookup"><span data-stu-id="dd589-197">Passes a search to Bing.</span></span> <span data-ttu-id="dd589-198">Um die zu durchsuchende Site und einen Titel für `Bing.SiteUrl` `Bing.SiteTitle` das Suchfeld anzugeben, können Sie die und die Eigenschaften festlegen.</span><span class="sxs-lookup"><span data-stu-id="dd589-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="dd589-199">Normalerweise legen Sie diese Eigenschaften auf der \* \_AppStart-Seite\* fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="dd589-200">Initialisiert ein Diagramm.</span><span class="sxs-lookup"><span data-stu-id="dd589-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="dd589-201">Fügt einem Diagramm eine Legende hinzu.</span><span class="sxs-lookup"><span data-stu-id="dd589-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="dd589-202">Fügt dem Diagramm eine Reihe von Werten hinzu.</span><span class="sxs-lookup"><span data-stu-id="dd589-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="dd589-203">Gibt einen Hash für die angegebenen Daten zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="dd589-204">Der Standardalgorithmus `sha256`ist .</span><span class="sxs-lookup"><span data-stu-id="dd589-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="dd589-205">Ermöglicht Facebook-Nutzern, eine Verbindung zu Seiten herzustellen.</span><span class="sxs-lookup"><span data-stu-id="dd589-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="dd589-206">Rendert die Benutzeroberfläche zum Hochladen von Dateien.</span><span class="sxs-lookup"><span data-stu-id="dd589-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="dd589-207">Rendert das angegebene Xbox Gamer-Tag.</span><span class="sxs-lookup"><span data-stu-id="dd589-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="dd589-208">Rendert das Gravatar-Bild für die angegebene E-Mail-Adresse.</span><span class="sxs-lookup"><span data-stu-id="dd589-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="dd589-209">Konvertiert ein Datenobjekt in eine Zeichenfolge im JsON-Format (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="dd589-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="dd589-210">Konvertiert eine JSON-codierte Eingabezeichenfolge in ein Datenobjekt, das Sie iterieren oder in eine Datenbank einfügen können.</span><span class="sxs-lookup"><span data-stu-id="dd589-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="dd589-211">Rendert Social-Networking-Links mit dem angegebenen Titel und der optionalen URL.</span><span class="sxs-lookup"><span data-stu-id="dd589-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="dd589-212">Ordnet einem Formularfeld eine Fehlermeldung zu.</span><span class="sxs-lookup"><span data-stu-id="dd589-212">Associates an error message with a form field.</span></span> <span data-ttu-id="dd589-213">Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="dd589-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="dd589-214">Ordnet einem Formular eine Fehlermeldung zu.</span><span class="sxs-lookup"><span data-stu-id="dd589-214">Associates an error message with a form.</span></span> <span data-ttu-id="dd589-215">Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="dd589-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="dd589-216">Gibt true zurück, wenn keine Validierungsfehler vorliegen.</span><span class="sxs-lookup"><span data-stu-id="dd589-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="dd589-217">Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="dd589-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="dd589-218">Rendert die Eigenschaften und Werte eines Objekts und aller untergeordneten Objekte.</span><span class="sxs-lookup"><span data-stu-id="dd589-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="dd589-219">Rendert den reCAPTCHA-Überprüfungstest.</span><span class="sxs-lookup"><span data-stu-id="dd589-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="dd589-220">Legt öffentliche und private Schlüssel für den reCAPTCHA-Dienst fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="dd589-221">Normalerweise legen Sie diese Eigenschaften auf der \* \_AppStart-Seite\* fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="dd589-222">Gibt das Ergebnis des reCAPTCHA-Tests zurück.</span><span class="sxs-lookup"><span data-stu-id="dd589-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="dd589-223">Rendert Statusinformationen zu ASP.NET Webseiten.</span><span class="sxs-lookup"><span data-stu-id="dd589-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="dd589-224">Rendert einen Twitter-Stream für den angegebenen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="dd589-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="dd589-225">Rendert einen Twitter-Stream für den angegebenen Suchtext.</span><span class="sxs-lookup"><span data-stu-id="dd589-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="dd589-226">Rendert einen Flash-Videoplayer für die angegebene Datei mit optionaler Breite und Höhe.</span><span class="sxs-lookup"><span data-stu-id="dd589-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="dd589-227">Rendert einen Windows Media Player für die angegebene Datei mit optionaler Breite und Höhe.</span><span class="sxs-lookup"><span data-stu-id="dd589-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="dd589-228">Rendert einen Silverlight-Player für die angegebene *.xap-Datei* mit der erforderlichen Breite und Höhe.</span><span class="sxs-lookup"><span data-stu-id="dd589-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="dd589-229">Gibt das durch *schlüssel*oder NULL angegebene Objekt zurück, wenn das Objekt nicht gefunden wird.</span><span class="sxs-lookup"><span data-stu-id="dd589-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="dd589-230">Entfernt das durch *Schlüssel* angegebene Objekt aus dem Cache.</span><span class="sxs-lookup"><span data-stu-id="dd589-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="dd589-231">Setzt *den Wert* unter dem vom *Schlüssel*angegebenen Namen in den Cache .</span><span class="sxs-lookup"><span data-stu-id="dd589-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="dd589-232">Erstellt ein `WebGrid` neues Objekt mithilfe von Daten aus einer Abfrage.</span><span class="sxs-lookup"><span data-stu-id="dd589-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="dd589-233">Rendert Markup, um Daten in einer HTML-Tabelle anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="dd589-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="dd589-234">Rendert einen Pager `WebGrid` für das Objekt.</span><span class="sxs-lookup"><span data-stu-id="dd589-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="dd589-235">Lädt ein Bild aus dem angegebenen Pfad.</span><span class="sxs-lookup"><span data-stu-id="dd589-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="dd589-236">Fügt das angegebene Bild als Wasserzeichen hinzu.</span><span class="sxs-lookup"><span data-stu-id="dd589-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="dd589-237">Fügt dem Bild den angegebenen Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="dd589-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="dd589-238">Dreht das Bild horizontal oder vertikal um.</span><span class="sxs-lookup"><span data-stu-id="dd589-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="dd589-239">Lädt ein Bild, wenn ein Bild während eines Dateiuploads auf eine Seite gepostet wird.</span><span class="sxs-lookup"><span data-stu-id="dd589-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="dd589-240">Ändert die Größe eines Bildes.</span><span class="sxs-lookup"><span data-stu-id="dd589-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="dd589-241">Dreht das Bild nach links oder rechts.</span><span class="sxs-lookup"><span data-stu-id="dd589-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="dd589-242">Speichert das Bild im angegebenen Pfad.</span><span class="sxs-lookup"><span data-stu-id="dd589-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="dd589-243">Legt das Kennwort für den SMTP-Server fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="dd589-244">Normalerweise legen Sie diese Eigenschaft auf der \* \_AppStart-Seite\* fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="dd589-245">Sendet eine E-Mail.</span><span class="sxs-lookup"><span data-stu-id="dd589-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="dd589-246">Legt den SMTP-Servernamen fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-246">Sets the SMTP server name.</span></span> <span data-ttu-id="dd589-247">Normalerweise legen Sie diese Eigenschaft auf der \* \_AppStart-Seite\* fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="dd589-248">Legt den Benutzernamen für den SMTP-Server fest.</span><span class="sxs-lookup"><span data-stu-id="dd589-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="dd589-249">Normalerweise sollten Sie diese Eigenschaft auf der \* \_AppStart-Seite\* festlegen.</span><span class="sxs-lookup"><span data-stu-id="dd589-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="dd589-250">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="dd589-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="dd589-251">(v2) Rendert eine Validierungsfehlermeldung für das angegebene Feld.</span><span class="sxs-lookup"><span data-stu-id="dd589-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="dd589-252">(v2) Zeigt eine Liste aller Validierungsfehler an.</span><span class="sxs-lookup"><span data-stu-id="dd589-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="dd589-253">(v2) Registriert ein Benutzereingabeelement für den angegebenen Validierungstyp.</span><span class="sxs-lookup"><span data-stu-id="dd589-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="dd589-254">(v2) Rendert CSS-Klassenattribute dynamisch für die clientseitige Validierung, sodass Sie Validierungsfehlermeldungen formatieren können.</span><span class="sxs-lookup"><span data-stu-id="dd589-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="dd589-255">(Erfordert, dass Sie auf die entsprechenden Clientskriptbibliotheken verweisen und CSS-Klassen definieren.)</span><span class="sxs-lookup"><span data-stu-id="dd589-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="dd589-256">(v2) Ermöglicht die clientseitige Validierung für das Benutzereingabefeld.</span><span class="sxs-lookup"><span data-stu-id="dd589-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="dd589-257">(Erfordert, dass Sie auf die entsprechenden Clientskriptbibliotheken verweisen.)</span><span class="sxs-lookup"><span data-stu-id="dd589-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="dd589-258">(v2) Gibt true zurück, wenn alle Benutzereingabeelemente, die für die Validierung registriert sind, gültige Werte enthalten.</span><span class="sxs-lookup"><span data-stu-id="dd589-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="dd589-259">(v2) Gibt an, dass Benutzer einen Wert für das Benutzereingabeelement angeben müssen.</span><span class="sxs-lookup"><span data-stu-id="dd589-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="dd589-260">(v2) Gibt an, dass Benutzer Werte für jedes der Benutzereingabeelemente angeben müssen.</span><span class="sxs-lookup"><span data-stu-id="dd589-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="dd589-261">Mit dieser Methode können Sie keine benutzerdefinierte Fehlermeldung angeben.</span><span class="sxs-lookup"><span data-stu-id="dd589-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="dd589-262">(v2) Gibt einen Validierungstest an, wenn Sie die `Validation.Add` Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="dd589-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
