---
title: Zweistufige Authentifizierung mit SMS in ASP.NET Core
author: rick-anderson
description: Erfahren Sie, wie Sie die zweistufige Authentifizierung (2FA) mit einer ASP.NET Core-app einrichten.
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.date: 09/22/2018
ms.custom: seodec18
uid: security/authentication/2fa
ms.openlocfilehash: 48bfc50378fc0ec212f5b9d4e7ce05bb4fc97b9d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052757"
---
# <a name="two-factor-authentication-with-sms-in-aspnet-core"></a><span data-ttu-id="3557c-103">Zweistufige Authentifizierung mit SMS in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3557c-103">Two-factor authentication with SMS in ASP.NET Core</span></span>

<span data-ttu-id="3557c-104">Durch [Rick Anderson](https://twitter.com/RickAndMSFT) und [Schweizer-Entwickler](https://github.com/Swiss-Devs)</span><span class="sxs-lookup"><span data-stu-id="3557c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Swiss-Devs](https://github.com/Swiss-Devs)</span></span>

>[!WARNING]
> <span data-ttu-id="3557c-105">Zwei Faktor-Authentifizierung (2FA) Authentifikator-apps, verwenden eine zeitbasierte Einmalkennwort Kennwort Algorithmus (TOTP), sind der empfohlene Ansatz für 2FA Branche.</span><span class="sxs-lookup"><span data-stu-id="3557c-105">Two factor authentication (2FA) authenticator apps, using a Time-based One-time Password Algorithm (TOTP), are the industry recommended approach for 2FA.</span></span> <span data-ttu-id="3557c-106">2FA TOTP mit SMS 2FA vorzuziehen ist.</span><span class="sxs-lookup"><span data-stu-id="3557c-106">2FA using TOTP is preferred to SMS 2FA.</span></span> <span data-ttu-id="3557c-107">Weitere Informationen finden Sie unter [QR-Code aktivieren-Generierung für Authentifikator-apps in ASP.NET Core TOTP](xref:security/authentication/identity-enable-qrcodes) für ASP.NET Core 2.0 und höher.</span><span class="sxs-lookup"><span data-stu-id="3557c-107">For more information, see [Enable QR Code generation for TOTP authenticator apps in ASP.NET Core](xref:security/authentication/identity-enable-qrcodes) for ASP.NET Core 2.0 and later.</span></span>

<span data-ttu-id="3557c-108">In diesem Tutorial veranschaulicht das Einrichten der zweistufigen Authentifizierung (2FA) mithilfe von SMS.</span><span class="sxs-lookup"><span data-stu-id="3557c-108">This tutorial shows how to set up two-factor authentication (2FA) using SMS.</span></span> <span data-ttu-id="3557c-109">Anweisungen werden vorgestellt, für das [Twilio](https://www.twilio.com/) und [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), aber Sie können alle anderen SMS-Anbieter verwenden.</span><span class="sxs-lookup"><span data-stu-id="3557c-109">Instructions are given for [twilio](https://www.twilio.com/) and [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/), but you can use any other SMS provider.</span></span> <span data-ttu-id="3557c-110">Es wird empfohlen [Kontobestätigung und Kennwortwiederherstellung](xref:security/authentication/accconfirm) vor Beginn dieses Tutorials.</span><span class="sxs-lookup"><span data-stu-id="3557c-110">We recommend you complete [Account Confirmation and Password Recovery](xref:security/authentication/accconfirm) before starting this tutorial.</span></span>

<span data-ttu-id="3557c-111">[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA)</span><span class="sxs-lookup"><span data-stu-id="3557c-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/2fa/sample/Web2FA).</span></span> <span data-ttu-id="3557c-112">[Zum Herunterladen](xref:index#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="3557c-112">[How to download](xref:index#how-to-download-a-sample).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="3557c-113">Erstellen eines neuen ASP.NET Core-Projekts</span><span class="sxs-lookup"><span data-stu-id="3557c-113">Create a new ASP.NET Core project</span></span>

<span data-ttu-id="3557c-114">Erstellen Sie eine neue ASP.NET Core-Web-app mit dem Namen `Web2FA` mit individuellen Benutzerkonten.</span><span class="sxs-lookup"><span data-stu-id="3557c-114">Create a new ASP.NET Core web app named `Web2FA` with individual user accounts.</span></span> <span data-ttu-id="3557c-115">Befolgen Sie die Anweisungen in <xref:security/enforcing-ssl> einrichten und die verbindliche Verwendung von HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3557c-115">Follow the instructions in <xref:security/enforcing-ssl> to set up and require HTTPS.</span></span>

### <a name="create-an-sms-account"></a><span data-ttu-id="3557c-116">Erstellen Sie eine SMS-Dienstkonto</span><span class="sxs-lookup"><span data-stu-id="3557c-116">Create an SMS account</span></span>

<span data-ttu-id="3557c-117">Erstellen Sie eine SMS-Dienstkonto, z. B. aus [Twilio](https://www.twilio.com/) oder [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span><span class="sxs-lookup"><span data-stu-id="3557c-117">Create an SMS account, for example, from [twilio](https://www.twilio.com/) or [ASPSMS](https://www.aspsms.com/asp.net/identity/core/testcredits/).</span></span> <span data-ttu-id="3557c-118">Notieren Sie die Anmeldeinformationen für die Authentifizierung (für Twilio: AccountSid "und" AuthToken, für die ASPSMS: UserKey und Kennwort).</span><span class="sxs-lookup"><span data-stu-id="3557c-118">Record the authentication credentials (for twilio: accountSid and authToken, for ASPSMS: Userkey and Password).</span></span>

#### <a name="figuring-out-sms-provider-credentials"></a><span data-ttu-id="3557c-119">Ermitteln Anmeldeinformationen für die SMS-Anbieter</span><span class="sxs-lookup"><span data-stu-id="3557c-119">Figuring out SMS Provider credentials</span></span>

<span data-ttu-id="3557c-120">**Twilio:** Kopieren Sie auf der Registerkarte Dashboard für Ihr Twilio-Konto die **Konto-SID** und **Authentifizierungstoken**.</span><span class="sxs-lookup"><span data-stu-id="3557c-120">**Twilio:** From the Dashboard tab of your Twilio account, copy the **Account SID** and **Auth token**.</span></span>

<span data-ttu-id="3557c-121">**ASPSMS:** Navigieren Sie in Ihren kontoeinstellungen zu **Userkey** und kopieren Sie ihn zusammen mit Ihrer **Kennwort**.</span><span class="sxs-lookup"><span data-stu-id="3557c-121">**ASPSMS:** From your account settings, navigate to **Userkey** and copy it together with your **Password**.</span></span>

<span data-ttu-id="3557c-122">Wir werden später speichern diese Werte sich mit dem Geheimnis-Manager-Tool in den Schlüsseln `SMSAccountIdentification` und `SMSAccountPassword`.</span><span class="sxs-lookup"><span data-stu-id="3557c-122">We will later store these values in with the secret-manager tool within the keys `SMSAccountIdentification` and `SMSAccountPassword`.</span></span>

#### <a name="specifying-senderid--originator"></a><span data-ttu-id="3557c-123">Angeben der Absender-ID / Ersteller</span><span class="sxs-lookup"><span data-stu-id="3557c-123">Specifying SenderID / Originator</span></span>

<span data-ttu-id="3557c-124">**Twilio:** Kopieren Sie Ihre Twilio auf der Registerkarte Zahlen **Telefonnummer**.</span><span class="sxs-lookup"><span data-stu-id="3557c-124">**Twilio:** From the Numbers tab, copy your Twilio **phone number**.</span></span>

<span data-ttu-id="3557c-125">**ASPSMS:** Klicken Sie im Menü Urheber entsperren entsperren Sie eine oder mehrere Urheber, oder wählen Sie eine alphanumerische Absender (von allen Netzwerken nicht unterstützt).</span><span class="sxs-lookup"><span data-stu-id="3557c-125">**ASPSMS:** Within the Unlock Originators Menu, unlock one or more Originators or choose an alphanumeric Originator (Not supported by all networks).</span></span>

<span data-ttu-id="3557c-126">Wir werden später speichern Sie diesen Wert mit dem Geheimnis-Manager-Tool im Schlüssel `SMSAccountFrom`.</span><span class="sxs-lookup"><span data-stu-id="3557c-126">We will later store this value with the secret-manager tool within the key `SMSAccountFrom`.</span></span>


### <a name="provide-credentials-for-the-sms-service"></a><span data-ttu-id="3557c-127">Geben Sie Anmeldeinformationen für den SMS-Dienst</span><span class="sxs-lookup"><span data-stu-id="3557c-127">Provide credentials for the SMS service</span></span>

<span data-ttu-id="3557c-128">Wir verwenden die [optionsmuster](xref:fundamentals/configuration/options) auf die Benutzer-Konto und dieser Schlüssel Einstellungen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="3557c-128">We'll use the [Options pattern](xref:fundamentals/configuration/options) to access the user account and key settings.</span></span>

   * <span data-ttu-id="3557c-129">Erstellen Sie eine Klasse zum Abrufen der sicheren SMS-Clientschlüssel.</span><span class="sxs-lookup"><span data-stu-id="3557c-129">Create a class to fetch the secure SMS key.</span></span> <span data-ttu-id="3557c-130">In diesem Beispiel die `SMSoptions` Klasse wird erstellt, der *Services/SMSoptions.cs* Datei.</span><span class="sxs-lookup"><span data-stu-id="3557c-130">For this sample, the `SMSoptions` class is created in the *Services/SMSoptions.cs* file.</span></span>

[!code-csharp[](2fa/sample/Web2FA/Services/SMSoptions.cs)]

<span data-ttu-id="3557c-131">Legen Sie die `SMSAccountIdentification`, `SMSAccountPassword` und `SMSAccountFrom` mit der [Secret-Manager-Tool](xref:security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="3557c-131">Set the `SMSAccountIdentification`, `SMSAccountPassword` and `SMSAccountFrom` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="3557c-132">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3557c-132">For example:</span></span>

```none
C:/Web2FA/src/WebApp1>dotnet user-secrets set SMSAccountIdentification 12345
info: Successfully saved SMSAccountIdentification = 12345 to the secret store.
```
* <span data-ttu-id="3557c-133">Fügen Sie das NuGet-Paket für den SMS-Anbieter hinzu.</span><span class="sxs-lookup"><span data-stu-id="3557c-133">Add the NuGet package for the SMS provider.</span></span> <span data-ttu-id="3557c-134">Über die Paket-Manager-Konsole (PMC) ausführen:</span><span class="sxs-lookup"><span data-stu-id="3557c-134">From the Package Manager Console (PMC) run:</span></span>

<span data-ttu-id="3557c-135">**Twilio:**
`Install-Package Twilio`</span><span class="sxs-lookup"><span data-stu-id="3557c-135">**Twilio:**
`Install-Package Twilio`</span></span>

<span data-ttu-id="3557c-136">**ASPSMS:**
`Install-Package ASPSMS`</span><span class="sxs-lookup"><span data-stu-id="3557c-136">**ASPSMS:**
`Install-Package ASPSMS`</span></span>


* <span data-ttu-id="3557c-137">Fügen Sie Code in die *Services/MessageServices.cs* Datei, die SMS zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="3557c-137">Add code in the *Services/MessageServices.cs* file to enable SMS.</span></span> <span data-ttu-id="3557c-138">Verwenden Sie entweder die Twilio oder Abschnitt ASPSMS:</span><span class="sxs-lookup"><span data-stu-id="3557c-138">Use either the Twilio or the ASPSMS section:</span></span>


<span data-ttu-id="3557c-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span><span class="sxs-lookup"><span data-stu-id="3557c-139">**Twilio:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_twilio.cs)]</span></span>

<span data-ttu-id="3557c-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span><span class="sxs-lookup"><span data-stu-id="3557c-140">**ASPSMS:** [!code-csharp[](2fa/sample/Web2FA/Services/MessageServices_ASPSMS.cs)]</span></span>

### <a name="configure-startup-to-use-smsoptions"></a><span data-ttu-id="3557c-141">Konfigurieren Sie beim Start verwenden `SMSoptions`</span><span class="sxs-lookup"><span data-stu-id="3557c-141">Configure startup to use `SMSoptions`</span></span>

<span data-ttu-id="3557c-142">Hinzufügen `SMSoptions` zum Dienstcontainer in die `ConfigureServices` -Methode in der die *"Startup.cs"*:</span><span class="sxs-lookup"><span data-stu-id="3557c-142">Add `SMSoptions` to the service container in the `ConfigureServices` method in the *Startup.cs*:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet1&highlight=4)]

### <a name="enable-two-factor-authentication"></a><span data-ttu-id="3557c-143">Zwei-Faktor-Authentifizierung aktivieren</span><span class="sxs-lookup"><span data-stu-id="3557c-143">Enable two-factor authentication</span></span>

<span data-ttu-id="3557c-144">Öffnen der *Views/Manage/Index.cshtml* Razor-Ansichtsdatei und entfernen, die der Kommentar Zeichen (also kein Markup auskommentiert ist).</span><span class="sxs-lookup"><span data-stu-id="3557c-144">Open the *Views/Manage/Index.cshtml* Razor view file and remove the comment characters (so no markup is commnted out).</span></span>

## <a name="log-in-with-two-factor-authentication"></a><span data-ttu-id="3557c-145">Melden Sie sich mit einer zweistufigen Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="3557c-145">Log in with two-factor authentication</span></span>

* <span data-ttu-id="3557c-146">Die app ausführen und einen neuen Benutzer registrieren</span><span class="sxs-lookup"><span data-stu-id="3557c-146">Run the app and register a new user</span></span>

![Web Application-Register-Ansicht in Microsoft Edge öffnen](2fa/_static/login2fa1.png)

* <span data-ttu-id="3557c-148">Tippen Sie auf Ihren Benutzernamen, das aktiviert wird, die `Index` Aktionsmethode im Controller der verwalten.</span><span class="sxs-lookup"><span data-stu-id="3557c-148">Tap on your user name, which activates the `Index` action method in Manage controller.</span></span> <span data-ttu-id="3557c-149">Tippen Sie dann auf die Telefonnummer **hinzufügen** Link.</span><span class="sxs-lookup"><span data-stu-id="3557c-149">Then tap the phone number **Add** link.</span></span>

![Verwalten von Ansicht: Tippen Sie auf den Link "hinzufügen"](2fa/_static/login2fa2.png)

* <span data-ttu-id="3557c-151">Fügen Sie eine Telefonnummer, die den Überprüfungscode erhalten, und tippen Sie auf **Überprüfungscode senden**.</span><span class="sxs-lookup"><span data-stu-id="3557c-151">Add a phone number that will receive the verification code, and tap **Send verification code**.</span></span>

![Telefonnummer an-Seite hinzufügen](2fa/_static/login2fa3.png)

* <span data-ttu-id="3557c-153">Sie erhalten eine Textnachricht mit dem Überprüfungscode.</span><span class="sxs-lookup"><span data-stu-id="3557c-153">You will get a text message with the verification code.</span></span> <span data-ttu-id="3557c-154">Geben Sie ihn, und tippen Sie auf **senden**</span><span class="sxs-lookup"><span data-stu-id="3557c-154">Enter it and tap **Submit**</span></span>

![Überprüfen Sie die Seite "Telefonnummer"](2fa/_static/login2fa4.png)

<span data-ttu-id="3557c-156">Wenn Sie keine SMS erhalten, finden Sie unter protokollseite Twilio.</span><span class="sxs-lookup"><span data-stu-id="3557c-156">If you don't get a text message, see twilio log page.</span></span>

* <span data-ttu-id="3557c-157">Die Ansicht "verwalten" zeigt, dass Ihre Telefonnummer wurde erfolgreich hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="3557c-157">The Manage view shows your phone number was added successfully.</span></span>

![Verwalten von Ansicht – Profiler - Telefonnummer wurde erfolgreich hinzugefügt.](2fa/_static/login2fa5.png)

* <span data-ttu-id="3557c-159">Tippen Sie auf **aktivieren** zweistufige Authentifizierung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="3557c-159">Tap **Enable** to enable two-factor authentication.</span></span>

![Verwalten von Ansicht: zwei-Faktor-Authentifizierung aktivieren](2fa/_static/login2fa6.png)

### <a name="test-two-factor-authentication"></a><span data-ttu-id="3557c-161">Die zweistufige Authentifizierung testen</span><span class="sxs-lookup"><span data-stu-id="3557c-161">Test two-factor authentication</span></span>

* <span data-ttu-id="3557c-162">Melden Sie sich ab.</span><span class="sxs-lookup"><span data-stu-id="3557c-162">Log off.</span></span>

* <span data-ttu-id="3557c-163">Anmelden.</span><span class="sxs-lookup"><span data-stu-id="3557c-163">Log in.</span></span>

* <span data-ttu-id="3557c-164">Das Benutzerkonto verfügt über zwei-Faktor-Authentifizierung aktiviert, müssen Sie die zweite Stufe der Authentifizierung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="3557c-164">The user account has enabled two-factor authentication, so you have to provide the second factor of authentication .</span></span> <span data-ttu-id="3557c-165">In diesem Tutorial haben Sie die Überprüfung per Telefon aktiviert.</span><span class="sxs-lookup"><span data-stu-id="3557c-165">In this tutorial you have enabled phone verification.</span></span> <span data-ttu-id="3557c-166">Die integrierten Vorlagen ermöglichen Ihnen das Einrichten von e-Mail als zweiter authentifizierungsfaktor auch.</span><span class="sxs-lookup"><span data-stu-id="3557c-166">The built in templates also allow you to set up email as the second factor.</span></span> <span data-ttu-id="3557c-167">Sie können die zweite Faktoren für die Authentifizierung wie z. B. QR-Codes einrichten.</span><span class="sxs-lookup"><span data-stu-id="3557c-167">You can set up additional second factors for authentication such as QR codes.</span></span> <span data-ttu-id="3557c-168">Tippen Sie auf **übermitteln**.</span><span class="sxs-lookup"><span data-stu-id="3557c-168">Tap **Submit**.</span></span>

![Überprüfungscode senden](2fa/_static/login2fa7.png)

* <span data-ttu-id="3557c-170">Geben Sie den Code, den Sie in der SMS-Nachricht erhalten.</span><span class="sxs-lookup"><span data-stu-id="3557c-170">Enter the code you get in the SMS message.</span></span>

* <span data-ttu-id="3557c-171">Durch Klicken auf die **diesen Browser merken** das Kontrollkästchen schließen Sie 2FA verwenden, melden Sie sich, wenn Sie den gleichen Browser und Geräte verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="3557c-171">Clicking on the **Remember this browser** check box will exempt you from needing to use 2FA to log on when using the same device and browser.</span></span> <span data-ttu-id="3557c-172">2FA aktiviert und auf **diesen Browser merken** erhalten Sie starke 2FA Schutz vor böswilligen Benutzern, die Ihr Konto zugreifen möchten, solange sie keinen Zugriff auf Ihr Gerät haben.</span><span class="sxs-lookup"><span data-stu-id="3557c-172">Enabling 2FA and clicking on **Remember this browser** will provide you with strong 2FA protection from malicious users trying to access your account, as long as they don't have access to your device.</span></span> <span data-ttu-id="3557c-173">Sie können auf allen privaten Geräten dazu, die Sie regelmäßig verwenden.</span><span class="sxs-lookup"><span data-stu-id="3557c-173">You can do this on any private device you regularly use.</span></span> <span data-ttu-id="3557c-174">Durch Festlegen von **diesen Browser merken**, Sie erhalten die Erhöhung der Sicherheit der 2FA von Geräten, die Sie nicht regelmäßig verwenden und Sie erhalten die Vorteile nicht auf Ihren eigenen Geräten 2FA durchlaufen haben.</span><span class="sxs-lookup"><span data-stu-id="3557c-174">By setting  **Remember this browser**, you get the added security of 2FA from devices you don't regularly use, and you get the convenience on not having to go through 2FA on your own devices.</span></span>

![Überprüfen Sie die Ansicht](2fa/_static/login2fa8.png)

## <a name="account-lockout-for-protecting-against-brute-force-attacks"></a><span data-ttu-id="3557c-176">Sperre zum Schutz vor brute-Force-Angriffen</span><span class="sxs-lookup"><span data-stu-id="3557c-176">Account lockout for protecting against brute force attacks</span></span>

<span data-ttu-id="3557c-177">Kontosperrung wird mit 2FA empfohlen.</span><span class="sxs-lookup"><span data-stu-id="3557c-177">Account lockout is recommended with 2FA.</span></span> <span data-ttu-id="3557c-178">Sobald ein Benutzer über ein lokales Konto oder ein Konto für soziales Netzwerk anmeldet, wird jeder fehlerhafte Versuch am 2FA gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3557c-178">Once a user signs in through a local account or social account, each failed attempt at 2FA is stored.</span></span> <span data-ttu-id="3557c-179">Wenn die maximale zugriffsversuchsfehlern erreicht ist, wird der Benutzer gesperrt ist (Standardwert: 5 Minuten Sperrung nach 5 Versuche fehlgeschlagen).</span><span class="sxs-lookup"><span data-stu-id="3557c-179">If the maximum failed access attempts is reached, the user is locked out (default: 5 minute lockout after 5 failed access attempts).</span></span> <span data-ttu-id="3557c-180">Eine erfolgreiche Authentifizierung setzt die Anzahl der fehlgeschlagenen Zugriffe Versuche und setzt die Uhr.</span><span class="sxs-lookup"><span data-stu-id="3557c-180">A successful authentication resets the failed access attempts count and resets the clock.</span></span> <span data-ttu-id="3557c-181">Die maximale Anzahl von fehlgeschlagenen Zugriffsversuchen und Dauer der Sperrung kann festgelegt werden, mit [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) und [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span><span class="sxs-lookup"><span data-stu-id="3557c-181">The maximum failed access attempts and lockout time can be set with [MaxFailedAccessAttempts](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) and [DefaultLockoutTimeSpan](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan).</span></span> <span data-ttu-id="3557c-182">Der folgende Code konfiguriert kontosperrung nach 10 Minuten nach 10 Versuche nicht erfolgreichen:</span><span class="sxs-lookup"><span data-stu-id="3557c-182">The following configures account lockout for 10 minutes after 10 failed access attempts:</span></span>

[!code-csharp[](2fa/sample/Web2FA/Startup.cs?name=snippet2&highlight=13-17)]

<span data-ttu-id="3557c-183">Überprüfen Sie, ob [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) legt `lockoutOnFailure` zu `true`:</span><span class="sxs-lookup"><span data-stu-id="3557c-183">Confirm that [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync) sets `lockoutOnFailure` to `true`:</span></span>

```csharp
var result = await _signInManager.PasswordSignInAsync(
                 Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: true);
```
