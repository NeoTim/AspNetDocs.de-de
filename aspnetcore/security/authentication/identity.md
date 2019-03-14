---
title: Einführung in die Identität in ASP.NET Core
author: rick-anderson
description: Verwenden Sie Identität mit einer ASP.NET Core-app. Erfahren Sie, wie Anforderungen für Kennwörter (RequireDigit, RequiredLength, RequiredUniqueChars usw.) festgelegt.
ms.author: riande
ms.date: 08/08/2018
uid: security/authentication/identity
ms.openlocfilehash: 1a4e7fb3ac6a767ca17127dd58a9b9e65ed9a00b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046677"
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="7c4b7-104">Einführung in die Identität in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7c4b7-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="7c4b7-105">Von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7c4b7-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7c4b7-106">ASP.NET Core Identity handelt es sich um ein Mitgliedschaftssystem, das ASP.NET Core-apps Anmeldefunktionalität hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-106">ASP.NET Core Identity is a membership system that adds login functionality to ASP.NET Core apps.</span></span> <span data-ttu-id="7c4b7-107">Benutzer können ein Konto erstellen, mit der Anmeldung Informationen in die Identität oder einem externen Anmeldeanbieter können.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-107">Users can create an account with the login information stored in Identity or they can use an external login provider.</span></span> <span data-ttu-id="7c4b7-108">Einschließen von unterstützten externen anmeldungsanbietern [Facebook, Google, Twitter und Microsoft Account](xref:security/authentication/social/index).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-108">Supported external login providers include [Facebook, Google, Microsoft Account, and Twitter](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="7c4b7-109">Identität kann mithilfe einer SQL Server-Datenbank zum Speichern von Benutzernamen und Kennwörter, Profildaten konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-109">Identity can be configured using a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="7c4b7-110">Alternativ kann einem anderen permanenten Speicher verwendet werden, z. B. Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-110">Alternatively, another persistent store can be used, for example, Azure Table Storage.</span></span>

<span data-ttu-id="7c4b7-111">[Anzeigen oder Herunterladen der Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) ([zum Herunterladen)](xref:index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-111">[View or download the sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) ([how to download)](xref:index#how-to-download-a-sample)).</span></span>

<span data-ttu-id="7c4b7-112">In diesem Thema erfahren Sie, wie Identität verwenden, um zu registrieren, melden Sie sich, und melden Sie sich ein Benutzer.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-112">In this topic, you learn how to use Identity to register, log in, and log out a user.</span></span> <span data-ttu-id="7c4b7-113">Ausführlichere Anweisungen zum Erstellen von apps, die Identität verwenden, finden Sie im Abschnitt "Nächste Schritte" am Ende dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-113">For more detailed instructions about creating apps that use Identity, see the Next Steps section at the end of this article.</span></span>

::: moniker range=">= aspnetcore-2.1"

<a name="adi"></a>
## <a name="adddefaultidentity-and-addidentity"></a><span data-ttu-id="7c4b7-114">AddDefaultIdentity und AddIdentity</span><span class="sxs-lookup"><span data-stu-id="7c4b7-114">AddDefaultIdentity and AddIdentity</span></span>

<span data-ttu-id="7c4b7-115">[AddDefaultIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionUIExtensions_AddDefaultIdentity__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__) wurde in ASP.NET Core 2.1 eingeführt.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-115">[AddDefaultIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionUIExtensions_AddDefaultIdentity__1_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__) was introduced in ASP.NET Core 2.1.</span></span> <span data-ttu-id="7c4b7-116">Aufrufen von `AddDefaultIdentity` entspricht dem folgenden Aufruf:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-116">Calling `AddDefaultIdentity` is similar to calling the following:</span></span>

* [<span data-ttu-id="7c4b7-117">AddIdentity</span><span class="sxs-lookup"><span data-stu-id="7c4b7-117">AddIdentity</span></span>](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity?view=aspnetcore-2.1#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_AddIdentity__2_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Identity_IdentityOptions__)
* [<span data-ttu-id="7c4b7-118">AddDefaultUI</span><span class="sxs-lookup"><span data-stu-id="7c4b7-118">AddDefaultUI</span></span>](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderuiextensions.adddefaultui?view=aspnetcore-2.1#Microsoft_AspNetCore_Identity_IdentityBuilderUIExtensions_AddDefaultUI_Microsoft_AspNetCore_Identity_IdentityBuilder_)
* [<span data-ttu-id="7c4b7-119">AddDefaultTokenProviders</span><span class="sxs-lookup"><span data-stu-id="7c4b7-119">AddDefaultTokenProviders</span></span>](/dotnet/api/microsoft.aspnetcore.identity.identitybuilderextensions.adddefaulttokenproviders?view=aspnetcore-2.1#Microsoft_AspNetCore_Identity_IdentityBuilderExtensions_AddDefaultTokenProviders_Microsoft_AspNetCore_Identity_IdentityBuilder_)

<span data-ttu-id="7c4b7-120">Finden Sie unter [AddDefaultIdentity Quelle](https://github.com/aspnet/AspNetCore/blob/release/2.2/src/Identity/UI/src/IdentityServiceCollectionUIExtensions.cs#L47-L63) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-120">See [AddDefaultIdentity source](https://github.com/aspnet/AspNetCore/blob/release/2.2/src/Identity/UI/src/IdentityServiceCollectionUIExtensions.cs#L47-L63) for more information.</span></span>

::: moniker-end

## <a name="create-a-web-app-with-authentication"></a><span data-ttu-id="7c4b7-121">Erstellen einer Web-app mit Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-121">Create a Web app with authentication</span></span>

<span data-ttu-id="7c4b7-122">Erstellen Sie ein Projekt für die ASP.NET Core-Webanwendung mit einzelnen Benutzerkonten.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-122">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7c4b7-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c4b7-123">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="7c4b7-124">Wählen Sie **Datei** > **Neu** > **Projekt** aus.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-124">Select **File** > **New** > **Project**.</span></span>
* <span data-ttu-id="7c4b7-125">Wählen Sie **ASP.NET Core-Webanwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-125">Select **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="7c4b7-126">Nennen Sie das Projekt **"WebApp1"** haben denselben Namespace aufweist wie das Projekt zum Herunterladen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-126">Name the project **WebApp1** to have the same namespace as the project download.</span></span> <span data-ttu-id="7c4b7-127">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-127">Click **OK**.</span></span>
* <span data-ttu-id="7c4b7-128">Wählen Sie eine ASP.NET Core **Webanwendung**, und wählen Sie dann **Authentifizierung ändern**.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-128">Select an ASP.NET Core **Web Application**, then select **Change Authentication**.</span></span>
* <span data-ttu-id="7c4b7-129">Wählen Sie **einzelne Benutzerkonten** , und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-129">Select **Individual User Accounts** and click **OK**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7c4b7-130">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="7c4b7-130">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp --auth Individual -o WebApp1
```

---

<span data-ttu-id="7c4b7-131">Enthält das generierte Projekt [ASP.NET Core Identity](xref:security/authentication/identity) als eine [Razor-Klassenbibliothek](xref:razor-pages/ui-class).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-131">The generated project provides [ASP.NET Core Identity](xref:security/authentication/identity) as a [Razor Class Library](xref:razor-pages/ui-class).</span></span> <span data-ttu-id="7c4b7-132">Die Identity-Razor-Klassenbibliothek macht Endpunkte mit dem `Identity` Bereich.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-132">The Identity Razor Class Library exposes endpoints with the `Identity` area.</span></span> <span data-ttu-id="7c4b7-133">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-133">For example:</span></span>

* <span data-ttu-id="7c4b7-134">/ Identity/Konto/anmelden</span><span class="sxs-lookup"><span data-stu-id="7c4b7-134">/Identity/Account/Login</span></span>
* <span data-ttu-id="7c4b7-135">/ Identity/Account/Abmeldung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-135">/Identity/Account/Logout</span></span>
* <span data-ttu-id="7c4b7-136">/ / Account/Identitätsverwaltung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-136">/Identity/Account/Manage</span></span>

### <a name="test-register-and-login"></a><span data-ttu-id="7c4b7-137">Test-Registrierung und Anmeldung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-137">Test Register and Login</span></span>

<span data-ttu-id="7c4b7-138">Führen Sie die app aus, und registrieren Sie einen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-138">Run the app and register a user.</span></span> <span data-ttu-id="7c4b7-139">Je nach Bildschirmgröße, Sie müssen ggf. auf die Navigationsschaltfläche für die ein-/ausschalten, finden Sie unter den **registrieren** und **Anmeldung** Links.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-139">Depending on your screen size, you might need to select the navigation toggle button to see the **Register** and **Login** links.</span></span>

[!INCLUDE[](~/includes/view-identity-db.md)]

<a name="pw"></a>
### <a name="configure-identity-services"></a><span data-ttu-id="7c4b7-140">Konfigurieren der Identitätsdienste</span><span class="sxs-lookup"><span data-stu-id="7c4b7-140">Configure Identity services</span></span>

<span data-ttu-id="7c4b7-141">Dienste hinzugefügt werden, `ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-141">Services are added in `ConfigureServices`.</span></span> <span data-ttu-id="7c4b7-142">Das typische Muster besteht darin, alle `Add{Service}`-Methoden und dann alle `services.Configure{Service}`-Methoden aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-142">The typical pattern is to call all the `Add{Service}` methods, and then call all the `services.Configure{Service}` methods.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity/sample/WebApp1/Startup.cs?name=snippet_configureservices)]

<span data-ttu-id="7c4b7-143">Der vorangehende Code konfiguriert Identität mit Standardwerten für die Option.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-143">The preceding code configures Identity with default option values.</span></span> <span data-ttu-id="7c4b7-144">Dienste, die app über den zur Verfügung gestellt [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-144">Services are made available to the app through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="7c4b7-145">Identität ist aktiviert, durch den Aufruf [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-145">Identity is enabled by calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication#Microsoft_AspNetCore_Builder_AuthAppBuilderExtensions_UseAuthentication_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span></span> <span data-ttu-id="7c4b7-146">`UseAuthentication` Fügt der Authentifizierung [Middleware](xref:fundamentals/middleware/index) zu der Anforderungspipeline.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-146">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/WebApp1/Startup.cs?name=snippet_configure&highlight=18)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   <span data-ttu-id="7c4b7-147">Dienste stehen der Anwendung über [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-147">Services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="7c4b7-148">Identität für die Anwendung aktiviert ist, durch den Aufruf `UseAuthentication` in die `Configure` Methode.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-148">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="7c4b7-149">`UseAuthentication` Fügt der Authentifizierung [Middleware](xref:fundamentals/middleware/index) zu der Anforderungspipeline.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-149">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   <span data-ttu-id="7c4b7-150">Diese Dienste stehen der Anwendung über [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-150">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="7c4b7-151">Identität für die Anwendung aktiviert ist, durch den Aufruf `UseIdentity` in die `Configure` Methode.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-151">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="7c4b7-152">`UseIdentity` Fügt der cookiebasierte Authentifizierung [Middleware](xref:fundamentals/middleware/index) zu der Anforderungspipeline.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-152">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

::: moniker-end

<span data-ttu-id="7c4b7-153">Weitere Informationen finden Sie unter den [IdentityOptions Klasse](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) und [Anwendungsstart](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-153">For more information, see the [IdentityOptions Class](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) and [Application Startup](xref:fundamentals/startup).</span></span>

## <a name="scaffold-register-login-and-logout"></a><span data-ttu-id="7c4b7-154">Erstellen des Gerüsts für registrieren, Anmeldung und Abmeldung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-154">Scaffold Register, Login, and LogOut</span></span>

<span data-ttu-id="7c4b7-155">Führen Sie die [Gerüst Identity in einer Razor-Projekt mit Autorisierung](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization) Anweisungen zum Generieren der der Code in diesem Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-155">Follow the [Scaffold identity into a Razor project with authorization](xref:security/authentication/scaffold-identity#scaffold-identity-into-a-razor-project-with-authorization) instructions to generate the the code shown in this section.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7c4b7-156">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c4b7-156">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="7c4b7-157">Fügen Sie die Dateien registrieren, Anmeldung und Abmeldung hinzu.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-157">Add the Register, Login, and LogOut files.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7c4b7-158">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="7c4b7-158">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="7c4b7-159">Wenn Sie das Projekt mit dem Namen erstellt **"WebApp1"**, führen Sie die folgenden Befehle.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-159">If you created the project with name **WebApp1**, run the following commands.</span></span> <span data-ttu-id="7c4b7-160">Verwenden Sie andernfalls den richtigen Namespace für die `ApplicationDbContext`:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-160">Otherwise, use the correct namespace for the `ApplicationDbContext`:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet aspnet-codegenerator identity -dc WebApp1.Data.ApplicationDbContext --files "Account.Register;Account.Login;Account.Logout"
```

<span data-ttu-id="7c4b7-161">PowerShell arbeitet mit Semikolon als Befehlstrennzeichen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-161">PowerShell uses semicolon as a command separator.</span></span> <span data-ttu-id="7c4b7-162">Wenn Sie PowerShell verwenden, versehen Sie die Semikolons aus der Datei mit Escapezeichen, oder fügen Sie die Liste der Dateien in doppelte Anführungszeichen, wie im vorherigen Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-162">When using PowerShell, escape the semicolons in the file list or put the file list in double quotes, as the preceding example shows.</span></span>

---

### <a name="examine-register"></a><span data-ttu-id="7c4b7-163">Überprüfen Sie die Registrierung</span><span class="sxs-lookup"><span data-stu-id="7c4b7-163">Examine Register</span></span>

::: moniker range=">= aspnetcore-2.1"

   <span data-ttu-id="7c4b7-164">Wenn ein Benutzer klickt der **registrieren** Link die `RegisterModel.OnPostAsync` Aktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-164">When a user clicks the **Register** link, the `RegisterModel.OnPostAsync` action is invoked.</span></span> <span data-ttu-id="7c4b7-165">Der Benutzer wird erstellt, indem [CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_) auf die `_userManager` Objekt.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-165">The user is created by [CreateAsync](/dotnet/api/microsoft.aspnetcore.identity.usermanager-1.createasync#Microsoft_AspNetCore_Identity_UserManager_1_CreateAsync__0_System_String_) on the `_userManager` object.</span></span> <span data-ttu-id="7c4b7-166">`_userManager` wird durch Dependency Injection bereitgestellt):</span><span class="sxs-lookup"><span data-stu-id="7c4b7-166">`_userManager` is provided by dependency injection):</span></span>

   [!code-csharp[](identity/sample/WebApp1/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=7,22)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

   <span data-ttu-id="7c4b7-167">Wenn ein Benutzer klickt der **registrieren** Link die `Register` Aktion wird aufgerufen, auf `AccountController`.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-167">When a user clicks the **Register** link, the `Register` action is invoked on `AccountController`.</span></span> <span data-ttu-id="7c4b7-168">Die `Register` Aktion wird den Benutzer erstellt, durch den Aufruf `CreateAsync` auf die `_userManager` Objekt (bereitgestellt, um `AccountController` durch Dependency Injection):</span><span class="sxs-lookup"><span data-stu-id="7c4b7-168">The `Register` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to `AccountController` by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

::: moniker-end

   <span data-ttu-id="7c4b7-169">Wenn der Benutzer erfolgreich erstellt wurde, der angemeldete Benutzer wird durch den Aufruf von `_signInManager.SignInAsync`.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-169">If the user was created successfully, the user is logged in by the call to `_signInManager.SignInAsync`.</span></span>

   <span data-ttu-id="7c4b7-170">**Hinweis**: Finden Sie unter [Konto Bestätigung](xref:security/authentication/accconfirm#prevent-login-at-registration) Schritte, um sofortige Anmeldung bei der Registrierung zu verhindern.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-170">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>

### <a name="log-in"></a><span data-ttu-id="7c4b7-171">Anmelden</span><span class="sxs-lookup"><span data-stu-id="7c4b7-171">Log in</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7c4b7-172">Das Anmeldeformular wird angezeigt, wenn:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-172">The Login form is displayed when:</span></span>

* <span data-ttu-id="7c4b7-173">Die **melden Sie sich bei** Link ausgewählt wird.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-173">The **Log in** link is selected.</span></span>
* <span data-ttu-id="7c4b7-174">Ein Benutzer versucht, eine zugriffsbeschränkte Seite zugreifen, die sie autorisiert sind nicht, den Zugriff auf **oder** Wenn dies nicht getan haben sie vom System authentifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-174">A user attempts to access a restricted page that they aren't authorized to access **or** when they haven't been authenticated by the system.</span></span>

<span data-ttu-id="7c4b7-175">Wenn das Formular auf der Anmeldeseite gesendet wird, die `OnPostAsync` Aktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-175">When the form on the Login page is submitted, the `OnPostAsync` action is called.</span></span> <span data-ttu-id="7c4b7-176">`PasswordSignInAsync` wird aufgerufen, auf die `_signInManager` Objekt (bereitgestellt durch Dependency Injection).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-176">`PasswordSignInAsync` is called on the `_signInManager` object (provided by dependency injection).</span></span>

   [!code-csharp[](identity/sample/WebApp1/Areas/Identity/Pages/Account/Login.cshtml.cs?name=snippet&highlight=10-11)]

   <span data-ttu-id="7c4b7-177">Die Basis `Controller` -Klasse macht eine `User` -Eigenschaft, die Sie von Controllermethoden aus zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-177">The base `Controller` class exposes a `User` property that you can access from controller methods.</span></span> <span data-ttu-id="7c4b7-178">Sie können z. B. auflisten `User.Claims` und autorisierungsentscheidungen treffen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-178">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="7c4b7-179">Weitere Informationen finden Sie unter <xref:security/authorization/introduction>.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-179">For more information, see <xref:security/authorization/introduction>.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="7c4b7-180">Das Anmeldeformular wird angezeigt, wenn ein Benutzer auf die **melden Sie sich bei** verknüpfen oder umgeleitet werden, wenn eine Seite zugreifen, die eine Authentifizierung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-180">The Login form is displayed when users select the **Log in** link or are redirected when accessing a page that requires authentication.</span></span> <span data-ttu-id="7c4b7-181">Wenn der Benutzer das Formular auf die Anmeldeseite, sendet der `AccountController` `Login` Aktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-181">When the user submits the form on the Login page, the `AccountController` `Login` action is called.</span></span>

<span data-ttu-id="7c4b7-182">Die `Login` Aktionsaufrufen `PasswordSignInAsync` auf die `_signInManager` Objekt (bereitgestellt, um `AccountController` durch Dependency Injection).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-182">The `Login` action calls `PasswordSignInAsync` on the `_signInManager` object (provided to `AccountController` by dependency injection).</span></span>

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

<span data-ttu-id="7c4b7-183">Die Basis (`Controller` oder `PageModel`)-Klasse macht eine `User` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-183">The base (`Controller` or `PageModel`) class exposes a `User` property.</span></span> <span data-ttu-id="7c4b7-184">Z. B. `User.Claims` aufgelistet werden kann, um autorisierungsentscheidungen zu treffen.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-184">For example, `User.Claims` can be enumerated to make authorization decisions.</span></span>

::: moniker-end

### <a name="log-out"></a><span data-ttu-id="7c4b7-185">Melden Sie sich ab</span><span class="sxs-lookup"><span data-stu-id="7c4b7-185">Log out</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7c4b7-186">Die **Abmelden** Link Ruft die `LogoutModel.OnPost` Aktion.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-186">The **Log out** link invokes the `LogoutModel.OnPost` action.</span></span> 

[!code-csharp[](identity/sample/WebApp1/Areas/Identity/Pages/Account/Logout.cshtml.cs)]

<span data-ttu-id="7c4b7-187">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync) löscht der Ansprüche des Benutzers in einem Cookie gespeichert.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-187">[SignOutAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.signoutasync#Microsoft_AspNetCore_Identity_SignInManager_1_SignOutAsync) clears the user's claims stored in a cookie.</span></span> <span data-ttu-id="7c4b7-188">Nicht nach dem Aufruf umleiten `SignOutAsync` oder der Benutzer wird **nicht** abgemeldet werden.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-188">Don't redirect after calling `SignOutAsync` or the user will **not** be signed out.</span></span>

<span data-ttu-id="7c4b7-189">POST wird angegeben, der *Pages/Shared/_LoginPartial.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-189">Post is specified in the *Pages/Shared/_LoginPartial.cshtml*:</span></span>

[!code-csharp[](identity/sample/WebApp1/Pages/Shared/_LoginPartial.cshtml?highlight=16)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

   <span data-ttu-id="7c4b7-190">Auf der **Abmelden** verknüpfen Aufrufe der `LogOut` Aktion.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-190">Clicking the **Log out** link calls the `LogOut` action.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   <span data-ttu-id="7c4b7-191">Der vorangehende Code Ruft die `_signInManager.SignOutAsync` Methode.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-191">The preceding code calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="7c4b7-192">Die `SignOutAsync` Methode löscht der Ansprüche des Benutzers in einem Cookie gespeichert.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-192">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>

::: moniker-end

## <a name="test-identity"></a><span data-ttu-id="7c4b7-193">Testidentität</span><span class="sxs-lookup"><span data-stu-id="7c4b7-193">Test Identity</span></span>

<span data-ttu-id="7c4b7-194">Die Standardprojektvorlagen für Web zulassen anonymen Zugriff auf den Startseiten.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-194">The default web project templates allow anonymous access to the home pages.</span></span> <span data-ttu-id="7c4b7-195">Um die Identität zu testen, fügen [ `[Authorize]` ](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) , die "Datenschutz".</span><span class="sxs-lookup"><span data-stu-id="7c4b7-195">To test Identity, add [`[Authorize]`](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute) to the Privacy page.</span></span>

[!code-csharp[](identity/sample/WebApp1/Pages/Privacy.cshtml.cs?highlight=6)]

<span data-ttu-id="7c4b7-196">Wenn Sie angemeldet sind, melden Sie sich ab. Führen Sie die app, und wählen Sie die **Datenschutz** Link.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-196">If you are signed in, sign out. Run the app and select the **Privacy** link.</span></span> <span data-ttu-id="7c4b7-197">Sie werden zur Anmeldeseite umgeleitet.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-197">You are redirected to the login page.</span></span>

::: moniker range=">= aspnetcore-2.1"

### <a name="explore-identity"></a><span data-ttu-id="7c4b7-198">Untersuchen Sie die Identität</span><span class="sxs-lookup"><span data-stu-id="7c4b7-198">Explore Identity</span></span>

<span data-ttu-id="7c4b7-199">Identität noch ausführlicher untersuchen zu können:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-199">To explore Identity in more detail:</span></span>

* [<span data-ttu-id="7c4b7-200">Erstellen Sie die vollständige Benutzeroberfläche identitätsquelle</span><span class="sxs-lookup"><span data-stu-id="7c4b7-200">Create full identity UI source</span></span>](xref:security/authentication/scaffold-identity#create-full-identity-ui-source)
* <span data-ttu-id="7c4b7-201">Überprüfen Sie die Quelle der einzelnen Seiten und durchlaufen Sie den Debugger an.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-201">Examine the source of each page and step through the debugger.</span></span>

::: moniker-end

## <a name="identity-components"></a><span data-ttu-id="7c4b7-202">Identitätskomponenten</span><span class="sxs-lookup"><span data-stu-id="7c4b7-202">Identity Components</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7c4b7-203">Alle Identity abhängigen NuGet-Pakete sind in enthalten die [Microsoft.AspNetCore.App metapaket](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-203">All the Identity dependent NuGet packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

<span data-ttu-id="7c4b7-204">Das primäre Paket für die Identität ist [Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-204">The primary package for Identity is [Microsoft.AspNetCore.Identity](https://www.nuget.org/packages/Microsoft.AspNetCore.Identity/).</span></span> <span data-ttu-id="7c4b7-205">Dieses Paket enthält die Kerngruppe von Schnittstellen für ASP.NET Core Identity und befindet sich durch `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-205">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="7c4b7-206">Migrieren zu ASP.NET Core-Identität</span><span class="sxs-lookup"><span data-stu-id="7c4b7-206">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="7c4b7-207">Weitere Informationen und Anleitungen zum Migrieren von vorhandenen Identitätsspeicher, finden Sie unter [Migrieren von Authentifizierungs- und Identitätseinstellungen](xref:migration/identity).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-207">For more information and guidance on migrating your existing Identity store, see [Migrate Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="7c4b7-208">Festlegen der kennwortsicherheit</span><span class="sxs-lookup"><span data-stu-id="7c4b7-208">Setting password strength</span></span>

<span data-ttu-id="7c4b7-209">Finden Sie unter [Konfiguration](#pw) für ein Beispiel, das die Anforderungen für die Mindestlänge für Kennwörter legt diese fest.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-209">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c4b7-210">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7c4b7-210">Next Steps</span></span>

* [<span data-ttu-id="7c4b7-211">Konfigurieren von Identity</span><span class="sxs-lookup"><span data-stu-id="7c4b7-211">Configure Identity</span></span>](xref:security/authentication/identity-configuration)
* <xref:security/authorization/secure-data>
* <xref:security/authentication/add-user-data>
* <xref:security/authentication/identity-enable-qrcodes>
* <xref:migration/identity>
* <xref:security/authentication/accconfirm>
* <xref:security/authentication/2fa>
* <xref:host-and-deploy/web-farm>
