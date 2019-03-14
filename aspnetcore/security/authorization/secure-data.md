---
title: Erstellen einer ASP.NET Core-app mit Benutzerdaten, die durch Autorisierung geschützt sind
author: rick-anderson
description: Informationen Sie zum Erstellen einer Razor-Seiten-app mit Benutzerdaten, die durch Autorisierung geschützt sind. Enthält, HTTPS, Authentifizierung und Sicherheit, ASP.NET Core Identity.
ms.author: riande
ms.date: 12/18/2018
ms.custom: seodec18
uid: security/authorization/secure-data
ms.openlocfilehash: bdba706c1ef24ebe35129cb8bb2d9949196245a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057087"
---
# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a>Erstellen einer ASP.NET Core-app mit Benutzerdaten, die durch Autorisierung geschützt sind

Von [Rick Anderson](https://twitter.com/RickAndMSFT) und [Joe Audette](https://twitter.com/joeaudette)

::: moniker range="<= aspnetcore-1.1"

Finden Sie unter [dieses PDF-Dokument](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) für die ASP.NET Core MVC-Version. Die ASP.NET Core 1.1-Version dieses Tutorials wird [dies](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) Ordner. Die ASP.NET Core-Beispiel befindet sich in 1.1 die [Beispiele](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).

::: moniker-end

::: moniker range="= aspnetcore-2.0"

Finden Sie unter [dieses PDF-Dokument](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_July16_18.pdf)

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

In diesem Tutorial veranschaulicht das Erstellen einer ASP.NET Core-Web-Apps mit Benutzerdaten, die durch Autorisierung geschützt sind. Es zeigt eine Liste von Kontakten, die (registrierter) Benutzer authentifiziert haben. Es gibt drei Sicherheitsgruppen:

* **Registrierte Benutzer** können alle genehmigten Daten anzeigen und bearbeiten und löschen können ihre eigenen Daten.
* **Manager** genehmigen oder ablehnen von Kontaktdaten können. Nur genehmigte Kontakte für Benutzer sichtbar sind.
* **Administratoren** können genehmigen/ablehnen und alle Daten bearbeiten und löschen.

In der folgenden Abbildung wird der Benutzer Rick (`rick@example.com`) angemeldet ist. Rick kann nur genehmigte Kontakte anzeigen und **bearbeiten**/**löschen**/**neu erstellen** Links, um seine Kontakte. Nur der letzte Datensatz erstellt, von Rick, zeigt **bearbeiten** und **löschen** Links. Andere Benutzer werden der letzte Eintrag nicht angezeigt, bis Manager oder Administratoren den Status "Genehmigt" annimmt.

![Screenshot der Rick angemeldet](secure-data/_static/rick.png)

In der folgenden Abbildung `manager@contoso.com` ist signiert, im und in der Rolle "Managers":

![Screenshot mit manager@contoso.com angemeldet](secure-data/_static/manager1.png)

Die folgende Abbildung zeigt die Manager Detailansicht eines Kontakts an:

![Anzeigen von Vorgesetzten eines Kontakts](secure-data/_static/manager.png)

Die **genehmigen** und **ablehnen** Schaltflächen sind nur für Manager und Administratoren angezeigt.

In der folgenden Abbildung `admin@contoso.com` in und in der Rolle "Administratoren" angemeldet ist:

![Screenshot mit admin@contoso.com angemeldet](secure-data/_static/admin.png)

Der Administrator muss alle Berechtigungen. Sie können lesen, bearbeiten und löschen Sie einen beliebigen Kontakt, und ändern Sie den Status von Kontakten.

Die app wurde erstellt, indem [Gerüstbau](xref:tutorials/first-mvc-app/adding-model#scaffold-the-movie-model) Folgendes `Contact` Modell:

[!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

Das Beispiel enthält die folgenden Handler für die Autorisierung:

* `ContactIsOwnerAuthorizationHandler`: Stellt sicher, dass ein Benutzer nur ihre Daten bearbeiten kann.
* `ContactManagerAuthorizationHandler`: Zum Genehmigen oder ablehnen von Kontakten können.
* `ContactAdministratorsAuthorizationHandler`: Ermöglicht es Administratoren, die zum Genehmigen oder ablehnen von Kontakten und zu bearbeiten und Löschen von Kontakten.

## <a name="prerequisites"></a>Vorraussetzungen

In diesem Tutorial wird verschoben. Sie sollten mit vertraut sein:

* [ASP.NET Core](xref:tutorials/first-mvc-app/start-mvc)
* [Authentifizierung](xref:security/authentication/identity)
* [Kontobestätigung und Kennwortwiederherstellung](xref:security/authentication/accconfirm)
* [Autorisierung](xref:security/authorization/introduction)
* [Entity Framework Core](xref:data/ef-mvc/intro)

::: moniker-end

::: moniker range="= aspnetcore-2.1"

In ASP.NET Core 2.1 `User.IsInRole` schlägt fehl, wenn `AddDefaultIdentity`. Dieses Tutorial verwendet `AddDefaultIdentity` und benötigt deshalb das ASP.NET Core 2.2 oder höher. Finden Sie unter [GitHub-Problem](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) für das Problem zu umgehen.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="the-starter-and-completed-app"></a>Die Starter und die fertige app

[Herunterladen](xref:index#how-to-download-a-sample) der [abgeschlossen](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app. [Test](#test-the-completed-app) die fertige app, damit Sie mit den Security-Features vertraut machen.

### <a name="the-starter-app"></a>Das Starter-app

[Herunterladen](xref:index#how-to-download-a-sample) der [Starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.

Führen Sie die app, tippen Sie auf die **ContactManager** verknüpfen, und stellen Sie sicher, Sie erstellen, bearbeiten und Löschen eines Kontakts.

## <a name="secure-user-data"></a>Schützen von Benutzerdaten

Die folgenden Abschnitte enthalten die wichtigsten Schritte zum Erstellen der sicheren Benutzer Daten-app. Möglicherweise finden Sie es hilfreich sein, auf das abgeschlossene Projekt zu verweisen.

### <a name="tie-the-contact-data-to-the-user"></a>Verknüpfen Sie die Kontaktdaten für den Benutzer

Verwenden Sie die ASP.NET [Identität](xref:security/authentication/identity) Benutzer-ID, um sicherzustellen, dass Benutzer ihre Daten, aber nicht für andere Benutzerdaten bearbeiten kann. Hinzufügen `OwnerID` und `ContactStatus` auf die `Contact` Modell:

[!code-csharp[](secure-data/samples/final2.1/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

`OwnerID` ist die ID des Benutzers aus der `AspNetUser` -Tabelle in der [Identität](xref:security/authentication/identity) Datenbank. Die `Status` Feld bestimmt, ob ein Kontakt allgemeine Benutzer angezeigt werden.

Erstellen Sie eine neue Migration, und aktualisieren Sie die Datenbank:

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="add-role-services-to-identity"></a>Fügen Sie Rollendienste hinzu, die Identität

Fügen Sie [Rollen](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) Rollendienste hinzufügen:

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet2&highlight=12)]

### <a name="require-authenticated-users"></a>Authentifizierte Benutzer

Legen Sie die Standardrichtlinie für die Authentifizierung der Benutzer authentifiziert werden müssen:

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet&highlight=17-99)] 

 Sie können die Authentifizierung auf der Ebene der Razor Page, Controller und Aktion mit Deaktivieren der `[AllowAnonymous]` Attribut. Einstellung die Standardrichtlinie für die Authentifizierung der Benutzer authentifiziert werden müssen schützt das neu hinzugefügte Razor-Seiten und Controller. Mit der Authentifizierung erforderlich, die in der Standardeinstellung sicherer ist als die auf neue Domänencontroller und Razor-Seiten enthalten die `[Authorize]` Attribut.

Hinzufügen ["AllowAnonymous"](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) auf den Index, Info "und" Wenden Sie sich an Seiten, damit anonyme Benutzer Informationen über die Website nutzen können, bevor sie sich registriert haben.

[!code-csharp[](secure-data/samples/final2.1/Pages/Index.cshtml.cs?highlight=1,6)]

### <a name="configure-the-test-account"></a>Konfigurieren des Testkontos

Die `SeedData` Klasse erstellt zwei Konten: Administrator und Manager. Verwenden der [Secret Manager-Tool](xref:security/app-secrets) , ein Kennwort für diese Konten festzulegen. Legen Sie das Kennwort aus dem Projektverzeichnis (das Verzeichnis mit *"Program.cs"*):

```console
dotnet user-secrets set SeedUserPW <PW>
```

Wenn Sie ein sicheres Kennwort nicht angegeben ist, eine Ausnahme wird ausgelöst, wenn `SeedData.Initialize` aufgerufen wird.

Update `Main` Testkennwort verwenden:

[!code-csharp[](secure-data/samples/final2.1/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a>Erstellen Sie die Testkonten und aktualisieren Kontakte

Update der `Initialize` -Methode in der die `SeedData` Klasse, um die Testkonten zu erstellen:

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet_Initialize)]

Fügen Sie die Administrator-Benutzer-ID und `ContactStatus` für die Contacts. Stellen Sie einen der Kontakte für "Gesendet" und eine "abgelehnt". Fügen Sie die Benutzer-ID und den Status an alle Kontakte hinzu. Nur ein Kontakt wird angezeigt:

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a>Besitzer, Manager und Administratoren Autorisierung Handler zu erstellen

Erstellen Sie eine `ContactIsOwnerAuthorizationHandler` -Klasse in der *Autorisierung* Ordner. Die `ContactIsOwnerAuthorizationHandler` stellt sicher, dass der Benutzer, die auf eine Ressource, das die Ressource besitzt.

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

Die `ContactIsOwnerAuthorizationHandler` Aufrufe [Kontext. Erfolgreiche](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) ist der aktuelle authentifizierte Benutzer der Besitzer des Kontakts. Autorisierung Handler in der Regel:

* Zurückgeben `context.Succeed` Wenn die Anforderungen erfüllt sind.
* Zurückgeben `Task.CompletedTask` Wenn sind nicht erfüllt. `Task.CompletedTask` ist weder Erfolg oder Misserfolg&mdash;dadurch, dass andere Handler Autorisierung ausgeführt.

Wenn Sie explizit ausführen müssen, zurückgeben [Kontext. Fehler](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).

Der app können Besitzer von Kontaktinformationen bearbeiten/löschen/erstellen ihre eigenen Daten. `ContactIsOwnerAuthorizationHandler` Überprüfen Sie den Vorgang, der im Parameter "Anforderung" übergeben muss nicht.

### <a name="create-a-manager-authorization-handler"></a>Erstellen Sie einen Ereignishandler der Manager-Autorisierung

Erstellen Sie eine `ContactManagerAuthorizationHandler` -Klasse in der *Autorisierung* Ordner. Die `ContactManagerAuthorizationHandler` überprüft, ob sich der Benutzer, die auf die Ressource eines Managers. Nur Manager können genehmigen oder ablehnen von Änderungen am Inhalt (neue oder geänderte).

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a>Erstellen Sie ein Administrator autorisierungshandler

Erstellen Sie eine `ContactAdministratorsAuthorizationHandler` -Klasse in der *Autorisierung* Ordner. Die `ContactAdministratorsAuthorizationHandler` überprüft, ob der Benutzer, die auf die Ressource ist ein Administrator. Administrator möglich, alle Vorgänge.

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a>Registrieren Sie die Autorisierung-Handler

Dienste, die mit Entity Framework Core müssen registriert werden, für die [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) mit [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions). Die `ContactIsOwnerAuthorizationHandler` verwendet ASP.NET Core [Identität](xref:security/authentication/identity), die basiert auf Entity Framework Core. Registrieren Sie die Handler mit der Sammlung von Diensten, damit sie verfügbar sind die `ContactsController` über [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection). Fügen Sie den folgenden Code am Ende der `ConfigureServices`:

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet_defaultPolicy&highlight=27-99)]

`ContactAdministratorsAuthorizationHandler` und `ContactManagerAuthorizationHandler` als Singletons hinzugefügt werden sollen. Sie Singletons sind, da sie nicht die EF verwenden und alle erforderlichen Informationen in den `Context` Parameter, der die `HandleRequirementAsync` Methode.

## <a name="support-authorization"></a>Unterstützung für Autorisierung

In diesem Abschnitt Aktualisieren Sie die Razor-Seiten und ein Operations-Anforderungen hinzufügen.

### <a name="review-the-contact-operations-requirements-class"></a>Überprüfen Sie die Kontaktinformationen Vorgänge Anforderungen-Klasse

Überprüfen Sie die `ContactOperations` Klasse. Diese Klasse enthält die Anforderungen der app unterstützt:

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-contacts-razor-pages"></a>Erstellen Sie eine Basisklasse für die Kontakte-Razor-Seiten

Erstellen Sie eine Basisklasse, die die in den Kontakten Razor-Seiten verwendeten Dienste enthält. Die Basisklasse der Klasse wird den Initialisierungscode an einem Ort:

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/DI_BasePageModel.cs)]

Der vorangehende Code:

* Fügt der `IAuthorizationService` Dienst den Zugriff auf die Handler für die Autorisierung.
* Fügt die Identität `UserManager` Service.
* Fügen Sie die `ApplicationDbContext` hinzu.

### <a name="update-the-createmodel"></a>Aktualisieren der CreateModel

Aktualisieren den erstellen-Page-Modell-Konstruktor verwendet die `DI_BasePageModel` Basisklasse:

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

Update der `CreateModel.OnPostAsync` Methode, um:

* Hinzufügen der Benutzer-ID an den `Contact` Modell.
* Rufen Sie die autorisierungshandler, um sicherzustellen, dass der Benutzer die Berechtigung zum Erstellen von Kontakten verfügt.

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a>Aktualisieren Sie die IndexModel

Update der `OnGetAsync` Methode, sodass nur genehmigte Kontakte für allgemeine Benutzer angezeigt werden:

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a>Aktualisieren Sie die EditModel

Fügen Sie einem autorisierungshandler, um sicherzustellen, dass der Benutzer ist Besitzer der den Kontakt hinzu. Da die Ressource Autorisierung überprüft wird, die `[Authorize]` -Attribut ist nicht ausreichend. Die app hat keinen Zugriff auf die Ressource, wenn die Attribute ausgewertet werden. Ressourcenbasierte Autorisierung muss zwingend erforderlich. Überprüfungen müssen ausgeführt werden, sobald die app Zugriff auf die Ressource, oder durch Laden in das Modell als auch innerhalb des Handlers selbst laden. Sie werden häufig die Ressource durch die Übergabe der Ressourcenschlüssel zugreifen.

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a>Aktualisieren Sie die DeleteModel

Aktualisieren Sie das Seitenmodell "löschen" um den autorisierungshandler für die zu verwenden, um sicherzustellen, dass der Benutzer über die Löschberechtigung für den Kontakt verfügt.

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a>Fügen Sie dem Prüfdienst in den Ansichten

Derzeit wird die Benutzeroberfläche zeigt bearbeiten und Löschen von Verknüpfungen für Kontakte, die der Benutzer nicht ändern kann.

Einfügen des autorisierungsdiensts in die *Views/_viewimports.cshtml* Datei, sodass sie für alle Ansichten verfügbar ist:

[!code-cshtml[](secure-data/samples/final2.1/Pages/_ViewImports.cshtml?highlight=6-99)]

Das vorhergehende Markup fügt mehrere `using` Anweisungen.

Update der **bearbeiten** und **löschen** verknüpft *Pages/Contacts/Index.cshtml* , sodass sie nur für Benutzer mit den entsprechenden Berechtigungen gerendert werden:

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml?highlight=34-36,62-999)]

> [!WARNING]
> Ausblenden von Links von Benutzern, die keine Berechtigung zum Ändern von Daten haben nicht die app zu sichern. Ausblenden von Links wird die app durch Anzeigen der einzige gültige Links Benutzerfreundlicher. Benutzer können die generierten URLs zum Aufrufen von bearbeiten und Löschen von Vorgänge für Daten, die sie besitzen keine hack. Der Razor Page oder einen Controller muss zugriffsüberprüfungen zum Schutz der Daten erzwingen.

### <a name="update-details"></a>Updatedetails

Aktualisieren Sie die Detailansicht, damit Manager genehmigen oder ablehnen von Kontakten können:

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml?name=snippet)]

Aktualisieren Sie das Seitenmodell Details an:

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="add-or-remove-a-user-to-a-role"></a>Hinzufügen oder Entfernen eines Benutzers zu einer Rolle

Finden Sie unter [dieses Problem](https://github.com/aspnet/Docs/issues/8502) Informationen auf:

* Entfernen Berechtigungen eines Benutzers ein. Stummschaltung z. B. einen Benutzer in einem Chat-app ein.
* Hinzufügen von Berechtigungen für einen Benutzer aus.

## <a name="test-the-completed-app"></a>Testen Sie die fertige app

Wenn Sie ein Kennwort für die per Seeding hinzugefügten Benutzerkonten bereits festgelegt haben, verwenden Sie die [Secret Manager-Tool](xref:security/app-secrets#secret-manager) zum Festlegen eines Kennworts:

* Wählen Sie ein sicheres Kennwort ein: Verwenden acht oder mehr Zeichen und mindestens einen Großbuchstaben, Zahl und symbol. Z. B. `Passw0rd!` erfüllt die Anforderungen für sichere Kennwörter.
* Führen Sie den folgenden Befehl aus dem Ordner des Projekts, in denen `<PW>` ist das Kennwort:

  ```console
  dotnet user-secrets set SeedUserPW <PW>
  ```

Wenn die app Kontakte hat:

* Löschen Sie alle Datensätze in der `Contact` Tabelle.
* Starten Sie die app zum Seeding der Datenbank neu.

Eine einfache Möglichkeit zum Testen der fertigen app wird auf drei verschiedene Browser (oder inkognito/InPrivate-Sitzungen) zu starten. Registrieren Sie einen neuen Benutzer in einem Browser (z. B. `test@example.com`). Melden Sie sich an jeden Browser mit einem anderen Benutzer. Überprüfen Sie die folgenden Vorgänge aus:

* Registrierte Benutzer können alle genehmigten wenden Sie sich an Daten anzeigen.
* Registrierte Benutzer können bearbeiten und ihre eigenen Daten löschen.
* Manager können genehmigen/Kontaktdaten ablehnen. Die `Details` anzeigen zeigt **genehmigen** und **ablehnen** Schaltflächen.
* Administratoren können genehmigen/ablehnen und alle Daten bearbeiten und löschen.

| Benutzer                | Ein Seeding ausgeführt, von der app | Optionen                                  |
| ------------------- | :---------------: | ---------------------------------------- |
| test@example.com    | Nein                | Löschen Sie bearbeiten und die eigenen Daten.                |
| manager@contoso.com | Ja               | Genehmigen oder ablehnen und eigene Daten bearbeiten und löschen. |
| admin@contoso.com   | Ja               | Genehmigen oder ablehnen und alle Daten bearbeiten und löschen. |

Erstellen Sie einen Kontakt in der Administrator-Browser. Kopieren Sie die URL für das Löschen und Bearbeiten von den Administrator wenden Sie sich an. Fügen Sie diesen Links, in den Browser des Testbenutzers zu überprüfen, ob die Testbenutzers diese Vorgänge kann nicht ein.

## <a name="create-the-starter-app"></a>Die Starter-app erstellen

* Erstellen einer Razor Pages-app, die mit dem Namen "ContactManager"
  * Erstellen Sie die app mit **einzelne Benutzerkonten**.
  * Nennen Sie ihn "ContactManager", sodass der Namespace den im Beispiel verwendeten Namespace entspricht.
  * `-uld` Gibt an, LocalDB anstelle von SQLite

  ```console
  dotnet new webapp -o ContactManager -au Individual -uld
  ```

* Hinzufügen *Models/Contact.cs*:

  [!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

* Gerüst der `Contact` Modell.
* Erstellen Sie der anfänglichen Migration und aktualisieren Sie die Datenbank zu:

  ```console
  dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
  dotnet ef database drop -f
  dotnet ef migrations add initial
  dotnet ef database update
  ```

* Update der **ContactManager** verankert werden der *Pages/_Layout.cshtml* Datei:

  ```cshtml
  <a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
  ```

* Testen der app, indem erstellen, bearbeiten und Löschen eines Kontakts

### <a name="seed-the-database"></a>Ausführen eines Seedings für die Datenbank

Hinzufügen der [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) -Klasse auf die *Daten* Ordner.

Rufen Sie `SeedData.Initialize` aus `Main`:

[!code-csharp[](secure-data/samples/starter2.1/Program.cs?name=snippet)]

Testen Sie, dass die app die Datenbank mit Anfangsdaten gefüllt. Wenn alle Zeilen in der DB-Kontakt vorhanden sind, wird die Seed-Methode nicht ausgeführt.

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Erstellen einer .NET Core- und SQL-Datenbank-Web-Apps in Azure App Service](/azure/app-service/app-service-web-tutorial-dotnetcore-sqldb)
* [ASP.NET Core-Autorisierung Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop). Dieser Übung wird ausführlicher auf den Sicherheitsfeatures, die in diesem Lernprogramm eingeführt.
* <xref:security/authorization/introduction>
* [Benutzerdefinierte, richtlinienbasierte Autorisierung](xref:security/authorization/policies)

::: moniker-end
