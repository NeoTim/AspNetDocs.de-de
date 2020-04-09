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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET-Webseiten-API-Schnellreferenz

 von [Tom FitzMacken](https://github.com/tfitzmac)

> Diese Seite enthält eine Liste mit kurzen Beispielen für die am häufigsten verwendeten Objekte, Eigenschaften und Methoden zum Programmieren ASP.NET Webseiten mit Razor-Syntax.
> 
> Beschreibungen mit "(v2)" wurden in ASP.NET Webseiten Version 2 eingeführt.
> 
> Die API-Referenzdokumentation finden Sie in der [ASP.NET Webseiten-Referenzdokumentation](https://go.microsoft.com/fwlink/?LinkId=208659) auf MSDN.
> 
> ## <a name="software-versions"></a>Softwareversionen
> 
> 
> - ASP.NET Webseiten (Razor) 3
>   
> 
> Dieses Tutorial funktioniert auch mit ASP.NET Webseiten 2 und ASP.NET Webseiten 1.0 (mit Ausnahme von Features, die als v2 gekennzeichnet sind).

Diese Seite enthält Referenzinformationen für Folgendes:

- [Klassen](#Classes)
- [Daten](#Data)
- [Hilfsmethoden](#Helpers)
- [Validation](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Klassen

### `AppState[key], AppState[index],App`

Enthält Daten, die von allen Seiten in der Anwendung gemeinsam genutzt werden können. Sie können die `App` dynamische Eigenschaft verwenden, um auf dieselben Daten zuzugreifen, wie im folgenden Beispiel:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Konvertiert einen Zeichenfolgenwert in einen booleschen Wert (true/false). Gibt false oder den angegebenen Wert zurück, wenn die Zeichenfolge nicht true/false darstellt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Konvertiert einen Zeichenfolgenwert in Datum/Uhrzeit. Gibt `DateTime.MinValue` den angegebenen Wert zurück, wenn die Zeichenfolge kein Datum/Uhrzeit darstellt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Konvertiert einen Zeichenfolgenwert in einen Dezimalwert. Gibt 0.0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keinen Dezimalwert darstellt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Konvertiert einen Zeichenfolgenwert in einen float. Gibt 0.0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keinen Dezimalwert darstellt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Konvertiert einen Zeichenfolgenwert in eine ganze Zahl. Gibt 0 oder den angegebenen Wert zurück, wenn die Zeichenfolge keine ganze Zahl darstellt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Erstellt eine browserkompatible URL aus einem lokalen Dateipfad mit optionalen zusätzlichen Pfadteilen.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Rendert *Wert* als HTML-Markup, anstatt ihn als HTML-codierte Ausgabe zu rendern.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Gibt true zurück, wenn der Wert von einer Zeichenfolge in den angegebenen Typ konvertiert werden kann.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Gibt true zurück, wenn das Objekt oder die Variable keinen Wert hat.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Gibt true zurück, wenn es sich bei der Anforderung um einen POST-Test handelt. (Anfangsanforderungen sind in der Regel ein GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Gibt den Pfad einer Layoutseite an, die auf diese Seite angewendet werden soll.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Enthält Daten, die zwischen der Seite, Layoutseiten und Teilseiten in der aktuellen Anforderung freigegeben wurden. Sie können die `Page` dynamische Eigenschaft verwenden, um auf dieselben Daten zuzugreifen, wie im folgenden Beispiel:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Layoutseiten) Rendert den Inhalt einer Inhaltsseite, die sich nicht in benannten Abschnitten befindet.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Rendert eine Inhaltsseite mit dem angegebenen Pfad und optionalen zusätzlichen Daten. Sie können die Werte der `PageData` zusätzlichen Parameter aus der Position (Beispiel 1) oder der Taste (Beispiel 2) abrufen.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Layoutseiten) Rendert einen Inhaltsabschnitt mit einem Namen. Legen Sie *fest, dass* ein Abschnitt optional ist.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Ruft den Wert eines HTTP-Cookies ab oder legt den Wert fest.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Ruft die Dateien ab, die in der aktuellen Anforderung hochgeladen wurden.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Ruft Daten ab, die in einem Formular (als Zeichenfolgen) gebucht wurden. `Request[key]`überprüft sowohl `Request.Form` die `Request.QueryString` als auch die Auflistungen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Ruft Daten ab, die in der URL-Abfragezeichenfolge angegeben wurden. `Request[key]`überprüft sowohl `Request.Form` die `Request.QueryString` als auch die Auflistungen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Deaktiviert selektiv die Anforderungsüberprüfung für ein Formularelement, einen Abfragezeichenfolgenwert, ein Cookie oder einen Headerwert. Die Anforderungsüberprüfung ist standardmäßig aktiviert und verhindert, dass Benutzer Markup oder andere potenziell gefährliche Inhalte veröffentlichen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Fügt der Antwort einen HTTP-Serverheader hinzu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Speichert die Seitenausgabe für eine bestimmte Zeit zwischen. Optional das *Gleiten* festlegen, um das Timeout für jeden Seitenzugriff zurückzusetzen, und *varyByParams,* um verschiedene Versionen der Seite für jede unterschiedliche Abfragezeichenfolge in der Seitenanforderung zwischenzuspeichern.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Leitet die Browseranforderung an einen neuen Speicherort um.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Legt den an den Browser gesendeten HTTP-Statuscode fest.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Schreibt den Inhalt von *Daten* in die Antwort mit einem optionalen MIME-Typ.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Schreibt den Inhalt einer Datei in die Antwort.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Layoutseiten) Definiert einen Inhaltsabschnitt mit einem Namen.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Decodiert eine Zeichenfolge, die HTML-codiert ist.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Codiert eine Zeichenfolge für das Rendern in HTML-Markup.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Gibt den physischen Serverpfad für den angegebenen virtuellen Pfad zurück.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Decodiert Text von einer URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Kodiert Text, um ihn in eine URL einzuzahlen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Ruft einen Wert ab oder legt ihn fest, bis der Benutzer den Browser schließt.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Zeigt eine Zeichenfolgendarstellung des Objektwerts an.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Ruft zusätzliche Daten von der URL ab (z. B. */MyPage/ExtraData*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Ändert das Kennwort für den angegebenen Benutzer.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Bestätigt ein Konto mithilfe des Kontobestätigungstokens.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Erstellt ein neues Benutzerkonto mit dem angegebenen Benutzernamen und Kennwort. Um ein Bestätigungstoken zu benötigen, übergeben Sie true für *requireConfirmationToken.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Ruft den Ganzzahlbezeichner für den aktuell angemeldeten Benutzer ab.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Ruft den Namen für den aktuell angemeldeten Benutzer ab.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Generiert ein Kennwort-Reset-Token, das per E-Mail an einen Benutzer gesendet werden kann, damit der Benutzer das Kennwort zurücksetzen kann.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Gibt die Benutzer-ID aus dem Benutzernamen zurück.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Gibt true zurück, wenn der aktuelle Benutzer angemeldet ist.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Gibt true zurück, wenn der Benutzer bestätigt wurde (z. B. durch eine Bestätigungs-E-Mail).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Gibt true zurück, wenn der Name des aktuellen Benutzers mit dem angegebenen Benutzernamen übereinstimmt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Meldet den Benutzer an, indem er ein Authentifizierungstoken im Cookie festlegt.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Meldet den Benutzer ab, indem das Authentifizierungstoken-Cookie entfernt wird.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Legt den HTTP-Status auf 401 (Nicht autorisiert) fest, wenn der Benutzer nicht authentifiziert ist.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Wenn der aktuelle Benutzer nicht Mitglied einer der angegebenen Rollen ist, wird der HTTP-Status auf 401 (Nicht autorisiert) festgelegt.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Wenn der aktuelle Benutzer nicht der durch *Benutzername*angegebene Benutzer ist, wird der HTTP-Status auf 401 (Unautorisiert) festgelegt.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Wenn das Kennwortzurücksetzungstoken gültig ist, wird das Kennwort des Benutzers in das neue Kennwort geändert.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Daten

### `Database.Execute(SQLstatement [,parameters]`

Führt *SQLstatement* (mit optionalen Parametern) wie INSERT, DELETE oder UPDATE aus und gibt eine Anzahl betroffener Datensätze zurück.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Gibt die Identitätsspalte aus der zuletzt eingefügten Zeile zurück.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Öffnet entweder die angegebene Datenbankdatei oder die Datenbank, die mithilfe einer benannten Verbindungszeichenfolge aus der *Datei Web.config* angegeben wird.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Öffnet eine Datenbank mit der Verbindungszeichenfolge. (Dies steht `Database.Open`im Gegensatz zu , die einen Verbindungszeichenfolgennamen verwendet.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Fragt die Datenbank mithilfe von *SQLstatement* ab (optional übergebene Parameter) und gibt die Ergebnisse als Auflistung zurück.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Führt *SQLstatement* (mit optionalen Parametern) aus und gibt einen einzelnen Datensatz zurück.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Führt *SQLstatement* (mit optionalen Parametern) aus und gibt einen einzelnen Wert zurück.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Hilfsmethoden

### `Analytics.GetGoogleHtml(webPropertyId)`

Rendert den Google Analytics JavaScript-Code für die angegebene ID.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Rendert den StatCounter Analytics JavaScript-Code für das angegebene Projekt.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Rendert den Yahoo Analytics JavaScript-Code für das angegebene Konto.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Übergibt eine Suche an Bing. Um die zu durchsuchende Site und einen Titel für `Bing.SiteUrl` `Bing.SiteTitle` das Suchfeld anzugeben, können Sie die und die Eigenschaften festlegen. Normalerweise legen Sie diese Eigenschaften auf der * \_AppStart-Seite* fest.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Initialisiert ein Diagramm.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Fügt einem Diagramm eine Legende hinzu.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Fügt dem Diagramm eine Reihe von Werten hinzu.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Gibt einen Hash für die angegebenen Daten zurück. Der Standardalgorithmus `sha256`ist .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Ermöglicht Facebook-Nutzern, eine Verbindung zu Seiten herzustellen.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Rendert die Benutzeroberfläche zum Hochladen von Dateien.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Rendert das angegebene Xbox Gamer-Tag.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Rendert das Gravatar-Bild für die angegebene E-Mail-Adresse.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Konvertiert ein Datenobjekt in eine Zeichenfolge im JsON-Format (JavaScript Object Notation).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Konvertiert eine JSON-codierte Eingabezeichenfolge in ein Datenobjekt, das Sie iterieren oder in eine Datenbank einfügen können.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Rendert Social-Networking-Links mit dem angegebenen Titel und der optionalen URL.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Ordnet einem Formularfeld eine Fehlermeldung zu. Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Ordnet einem Formular eine Fehlermeldung zu. Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Gibt true zurück, wenn keine Validierungsfehler vorliegen. Verwenden `ModelState` Sie den Helfer, um auf dieses Mitglied zuzugreifen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Rendert die Eigenschaften und Werte eines Objekts und aller untergeordneten Objekte.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Rendert den reCAPTCHA-Überprüfungstest.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Legt öffentliche und private Schlüssel für den reCAPTCHA-Dienst fest. Normalerweise legen Sie diese Eigenschaften auf der * \_AppStart-Seite* fest.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Gibt das Ergebnis des reCAPTCHA-Tests zurück.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Rendert Statusinformationen zu ASP.NET Webseiten.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Rendert einen Twitter-Stream für den angegebenen Benutzer.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Rendert einen Twitter-Stream für den angegebenen Suchtext.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Rendert einen Flash-Videoplayer für die angegebene Datei mit optionaler Breite und Höhe.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Rendert einen Windows Media Player für die angegebene Datei mit optionaler Breite und Höhe.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Rendert einen Silverlight-Player für die angegebene *.xap-Datei* mit der erforderlichen Breite und Höhe.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Gibt das durch *schlüssel*oder NULL angegebene Objekt zurück, wenn das Objekt nicht gefunden wird.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Entfernt das durch *Schlüssel* angegebene Objekt aus dem Cache.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Setzt *den Wert* unter dem vom *Schlüssel*angegebenen Namen in den Cache .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Erstellt ein `WebGrid` neues Objekt mithilfe von Daten aus einer Abfrage.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Rendert Markup, um Daten in einer HTML-Tabelle anzuzeigen.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Rendert einen Pager `WebGrid` für das Objekt.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Lädt ein Bild aus dem angegebenen Pfad.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Fügt das angegebene Bild als Wasserzeichen hinzu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Fügt dem Bild den angegebenen Text hinzu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Dreht das Bild horizontal oder vertikal um.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Lädt ein Bild, wenn ein Bild während eines Dateiuploads auf eine Seite gepostet wird.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Ändert die Größe eines Bildes.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Dreht das Bild nach links oder rechts.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Speichert das Bild im angegebenen Pfad.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Legt das Kennwort für den SMTP-Server fest. Normalerweise legen Sie diese Eigenschaft auf der * \_AppStart-Seite* fest.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Sendet eine E-Mail.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Legt den SMTP-Servernamen fest. Normalerweise legen Sie diese Eigenschaft auf der * \_AppStart-Seite* fest.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Legt den Benutzernamen für den SMTP-Server fest. Normalerweise sollten Sie diese Eigenschaft auf der * \_AppStart-Seite* festlegen.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Überprüfen

### `Html.ValidationMessage(field)`

(v2) Rendert eine Validierungsfehlermeldung für das angegebene Feld.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) Zeigt eine Liste aller Validierungsfehler an.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) Registriert ein Benutzereingabeelement für den angegebenen Validierungstyp.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) Rendert CSS-Klassenattribute dynamisch für die clientseitige Validierung, sodass Sie Validierungsfehlermeldungen formatieren können. (Erfordert, dass Sie auf die entsprechenden Clientskriptbibliotheken verweisen und CSS-Klassen definieren.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) Ermöglicht die clientseitige Validierung für das Benutzereingabefeld. (Erfordert, dass Sie auf die entsprechenden Clientskriptbibliotheken verweisen.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) Gibt true zurück, wenn alle Benutzereingabeelemente, die für die Validierung registriert sind, gültige Werte enthalten.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) Gibt an, dass Benutzer einen Wert für das Benutzereingabeelement angeben müssen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) Gibt an, dass Benutzer Werte für jedes der Benutzereingabeelemente angeben müssen. Mit dieser Methode können Sie keine benutzerdefinierte Fehlermeldung angeben.

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

(v2) Gibt einen Validierungstest an, wenn Sie die `Validation.Add` Methode verwenden.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
