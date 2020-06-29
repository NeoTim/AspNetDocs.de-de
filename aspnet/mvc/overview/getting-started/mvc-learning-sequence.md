---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: Empfohlene MVC-Tutorials und-Artikel | Microsoft-Dokumentation
author: Rick-Anderson
description: Diese Seite enthält Links zu ASP.NET MVC-Tutorials und eine vorgeschlagene Sequenz.
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 7dc81cf09309194df4471fedfc74d4051f0fdb78
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484216"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>MVC – Empfohlene Tutorials und Artikel

von [Rick Anderson](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>Erste Schritte

- [Einstieg in ASP.NET MVC 5](introduction/getting-started.md) Diese 11-teilige Reihe ist ein guter Ausgangspunkt.
- [Pluralsight ASP.NET MVC 5-Grundlagen](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals) (Video Kurs)
- Einführung [in ASP.NET MVC](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC) von Jon Galloway und Christopher Harrison
- [Lebenszyklus einer ASP.NET MVC 5-Anwendung](lifecycle-of-an-aspnet-mvc-5-application.md) PDF-Dokument, das den Lebenszyklus einer ASP.NET MVC 5-App zeichnet.

<a id="con"></a>
## <a name="working-with-data"></a>Arbeiten mit Daten

- Ersten Schritten [mit EF 6 Code First mithilfe von MVC 5](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) Die preisgekrönte Serie von Tom Dykstra ist tief in EF zu tauchen.

<a id="wj"></a>
## <a name="security"></a>Sicherheit

- [Erstellen Sie eine ASP.NET MVC-App mit Authentifizierung und SQL-Datenbank, und stellen Sie Sie in Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) bereit. Dieses beliebte Tutorial führt Sie durch die Erstellung einer einfachen APP und das Hinzufügen von Mitgliedschaften und Rollen.
- [Erstellen einer ASP.NET MVC 5-App mit Facebook, Twitter, LinkedIn und Google OAuth2 Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) In diesem Tutorial wird gezeigt, wie Sie eine ASP.NET MVC 5-Webanwendung erstellen, die es Benutzern ermöglicht, sich mithilfe von OAuth 2,0 mit Anmelde Informationen eines externen Authentifizierungs Anbieters wie Facebook, Twitter, LinkedIn, Microsoft oder Google anzumelden.
- [Erstellen einer Secure ASP.NET MVC 5-Web-App mit Anmeldung, e-Mail-Bestätigung und Kenn Wort](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) Zurücksetzung Zum ersten Mal in einer Reihe von Identitäten enthält Code zum [erneuten Senden eines Bestätigungs Links](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend).
- [ASP.NET MVC 5-App mit zweistufiger SMS-und e-Mail-Authentifizierung](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) Zweitens zur Identitäts Reihe.
- [Bewährte Methoden für die Bereitstellung von Kennwörtern und anderen sensiblen Daten für ASP.NET und Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- [Zweistufige Authentifizierung mit SMS und e-Mail mit ASP.net Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) `isPersistent` und mit dem Sicherheits Cookie Code, der erfordert, dass ein Benutzer über ein validiertes e-Mail-Konto verfügt, bevor er sich anmelden kann, wie signinmanager die 2FA-Anforderung überprüft und mehr.
- [Konto Bestätigung und Kenn Wort Wiederherstellung mit ASP.net Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Bietet Details zur Identität, die in [Erstellen einer Secure ASP.NET MVC 5-Web-App mit Anmeldung, e-Mail-Bestätigung und Kenn Wort](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md) Zurücksetzung nicht gefunden wurde

<a id="da"></a>
## <a name="azure"></a>Azure

- [Erstellen einer ASP.net-Web-App in Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/) Kurzes und einfaches Tutorial für die Bereitstellung in Azure.
- [Erstellen Sie eine ASP.NET MVC-App mit Authentifizierung und SQL-Datenbank, und stellen Sie Sie in Azure bereit.](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>Leistung und Debuggen

- [Erstellen von Profilen und Debuggen der ASP.NET MVC-App mit Glimpse](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)

## <a name="aspnet-mvc-dropdownlistfor-with-selectlistitem"></a>ASP.NET MVC DropDownListFor with SelectListItem

Wenn Sie das-Hilfsprogramm verwenden <xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A> und an das- `SelectListItem` Hilfsprogramm übergeben, von dem es aufgefüllt wird, `DropdownListFor` ändert die übergebene Auflistung, nachdem Sie aufgerufen wurde. `DropdownListFor`ändert die `SelectListItems` ausgewählten Eigenschaften in den von der Dropdown Liste ausgewählten. Dies führt zu unerwartetem Verhalten.

, <xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A> <xref:System.Web.Mvc.Html.SelectExtensions.DropDownList%2A> , <xref:System.Web.Mvc.Html.SelectExtensions.EnumDropDownListFor%2A> , <xref:System.Web.Mvc.Html.SelectExtensions.ListBox%2A> Und <xref:System.Web.Mvc.Html.SelectExtensions.ListBoxFor%2A> aktualisieren die ausgewählte Eigenschaft eines beliebigen `IEnumerable<SelectListItem>` oder gefundenen in ViewData.

Die Problem Umgehung besteht darin, separate Enumerables mit unterschiedlichen `SelectListItem` Instanzen für jede Eigenschaft im Modell zu erstellen.

Weitere Informationen finden Sie unter

* [DropDownListFor ändert die an ihn über gegebene SelectListItem-Auflistung.](http://web.archive.org/web/20140902031437/http://aspnetwebstack.codeplex.com/workitem/1913)
* [Getselectlistwithdefaultvalue ändert IEnumerable <SelectListItem> SelectList.](https://github.com/aspnet/AspNetWebStack/issues/271)