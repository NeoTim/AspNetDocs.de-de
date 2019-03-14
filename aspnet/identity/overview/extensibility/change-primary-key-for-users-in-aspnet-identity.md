---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: Ändern des Primärschlüssels für Benutzer in ASP.NET Identity | Microsoft-Dokumentation
author: Rick-Anderson
description: In Visual Studio 2013 verwendet die standardwebanwendung einen Zeichenfolgenwert für den Schlüssel für Benutzerkonten an. ASP.NET Identity können Sie den Typ des Ändern der...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: d2856ce1ca61a29e091bfbd16647b673e6fc659b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033807"
---
<a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="64236-104">Ändern des Primärschlüssels für Benutzer in ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="64236-104">Change Primary Key for Users in ASP.NET Identity</span></span>
====================
<span data-ttu-id="64236-105">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="64236-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="64236-106">In Visual Studio 2013 verwendet die standardwebanwendung einen Zeichenfolgenwert für den Schlüssel für Benutzerkonten an.</span><span class="sxs-lookup"><span data-stu-id="64236-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="64236-107">ASP.NET Identity ermöglicht Ihnen, den Typ des Schlüssels, der Ihre Daten zu Anforderungen ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="64236-108">Beispielsweise können Sie den Typ des Schlüssels aus einer Zeichenfolge in eine ganze Zahl ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="64236-109">In diesem Thema wird gezeigt, wie für den Einstieg Standard, web-Anwendung und ändern den kontoschlüssel für den Benutzer auf eine ganze Zahl.</span><span class="sxs-lookup"><span data-stu-id="64236-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="64236-110">Sie können die gleichen Änderungen verwenden, um jede Art von Schlüssel in Ihrem Projekt zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="64236-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="64236-111">Es zeigt, wie Sie diese Änderungen in der standardwebanwendung übernommen, aber Sie können ähnliche Änderungen an einer benutzerdefinierten Anwendung anwenden.</span><span class="sxs-lookup"><span data-stu-id="64236-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="64236-112">Es zeigt die Änderungen, die erforderlich sind, bei der Arbeit mit MVC oder Web Forms.</span><span class="sxs-lookup"><span data-stu-id="64236-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="64236-113">Softwareversionen, die in diesem Tutorial verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="64236-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="64236-114">Visual Studio 2013 mit Update 2 (oder höher)</span><span class="sxs-lookup"><span data-stu-id="64236-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="64236-115">ASP.NET Identity 2.1 oder höher</span><span class="sxs-lookup"><span data-stu-id="64236-115">ASP.NET Identity 2.1 or later</span></span>


<span data-ttu-id="64236-116">Um die Schritte in diesem Tutorial ausführen zu können, müssen Sie Visual Studio 2013 Update 2 (oder höher), und eine Webanwendung, die aus der ASP.NET Web Application-Vorlage erstellten verfügen.</span><span class="sxs-lookup"><span data-stu-id="64236-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="64236-117">Die Vorlage, die in Update 3 geändert wird.</span><span class="sxs-lookup"><span data-stu-id="64236-117">The template changed in Update 3.</span></span> <span data-ttu-id="64236-118">In diesem Thema veranschaulicht, wie die Vorlage in Update 2 und Update 3 ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="64236-119">Dieses Thema enthält folgende Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="64236-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="64236-120">Ändern Sie den Typ des Schlüssels in der Identity-Klasse</span><span class="sxs-lookup"><span data-stu-id="64236-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="64236-121">Hinzufügen der benutzerdefinierte Identität-Klassen, die den Typ des Schlüssels verwenden</span><span class="sxs-lookup"><span data-stu-id="64236-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="64236-122">Ändern Sie die Kontext-Klasse und Benutzer-Manager, um den Schlüsseltyp zu verwenden</span><span class="sxs-lookup"><span data-stu-id="64236-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="64236-123">Start-Konfiguration ändern, verwenden Sie den Typ des Schlüssels</span><span class="sxs-lookup"><span data-stu-id="64236-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="64236-124">Ändern Sie für MVC mit Update 2 AccountController-Komponente um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="64236-125">Für MVC mit Update 3 ändern Sie, die AccountController und ManageController, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="64236-126">Ändern Sie für Web Forms mit Update 2 Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="64236-127">Für Webformulare mit Update 3 ändern Sie die Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="64236-128">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="64236-128">Run application</span></span>](#run)
- [<span data-ttu-id="64236-129">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="64236-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="64236-130">Ändern Sie den Typ des Schlüssels in der Identity-Klasse</span><span class="sxs-lookup"><span data-stu-id="64236-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="64236-131">Geben Sie in Ihrem Projekt aus der ASP.NET Web Application-Vorlage erstellt haben, dass die Klasse "applicationuser" eine ganze Zahl für den Schlüssel für Benutzerkonten verwendet.</span><span class="sxs-lookup"><span data-stu-id="64236-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="64236-132">Ändern Sie die Klasse "applicationuser" von "identityuser" erben, der den Typ aufweist, im IdentityModels.cs, **Int** für den generischen TKey-Parameter.</span><span class="sxs-lookup"><span data-stu-id="64236-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="64236-133">Sie übergeben außerdem die Namen der drei benutzerdefinierte Klasse mit der Sie noch nicht implementiert wurde.</span><span class="sxs-lookup"><span data-stu-id="64236-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="64236-134">Sie haben den Typ des Schlüssels geändert, aber in der Standardeinstellung die übrigen Teile der Anwendung weiterhin wird davon ausgegangen, dass der Schlüssel eine Zeichenfolge ist.</span><span class="sxs-lookup"><span data-stu-id="64236-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="64236-135">Sie müssen explizit den Typ des Schlüssels im Code angeben, die eine Zeichenfolge annimmt.</span><span class="sxs-lookup"><span data-stu-id="64236-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="64236-136">In der **"applicationuser"** Klasse, Ändern der **GenerateUserIdentityAsync** Methode, um ganze Zahl, einzufügen, wie im folgenden hervorgehobenen Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="64236-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="64236-137">Diese Änderung ist nicht erforderlich für Web Forms-Projekte mit der Update 3-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="64236-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="64236-138">Hinzufügen der benutzerdefinierte Identität-Klassen, die den Typ des Schlüssels verwenden</span><span class="sxs-lookup"><span data-stu-id="64236-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="64236-139">Die anderen Identitätsklassen, z. B. IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, werden immer noch mit einem Zeichenfolgenschlüssel eingerichtet.</span><span class="sxs-lookup"><span data-stu-id="64236-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="64236-140">Erstellen Sie neue Versionen dieser Klassen, die eine ganze Zahl für den Schlüssel angeben.</span><span class="sxs-lookup"><span data-stu-id="64236-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="64236-141">Sie müssen nicht viel Code zur Implementierung in diesen Klassen bereitstellen, legen Sie in erster Linie nur Int als Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="64236-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="64236-142">Die folgenden Klassen der IdentityModels.cs-Datei hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="64236-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="64236-143">Ändern Sie die Kontext-Klasse und Benutzer-Manager, um den Schlüsseltyp zu verwenden</span><span class="sxs-lookup"><span data-stu-id="64236-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="64236-144">In IdentityModels.cs, ändern Sie die Definition der **ApplicationDbContext** Klasse zur Verwendung der neuen benutzerdefinierten Klassen und eine **Int** für den Schlüssel, wie in den hervorgehobenen Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="64236-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="64236-145">Der ThrowIfV1Schema-Parameter ist nicht mehr gültig ist, im Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="64236-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="64236-146">Ändern Sie den Konstruktor aus, damit er nicht auf einen ThrowIfV1Schema-Wert übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="64236-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="64236-147">IdentityConfig.cs öffnen, und Ändern der **ApplicationUserManger** Ihr neuen Benutzer zu verwendende Klasse an Klasse zum Beibehalten von Daten zu speichern und ein **Int** für den Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="64236-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="64236-148">In der Vorlage Update 3 müssen Sie die ApplicationSignInManager-Klasse ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="64236-149">Start-Konfiguration ändern, verwenden Sie den Typ des Schlüssels</span><span class="sxs-lookup"><span data-stu-id="64236-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="64236-150">Ersetzen Sie in Startup.Auth.cs den OnValidateIdentity-Code, wie unten markiert.</span><span class="sxs-lookup"><span data-stu-id="64236-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="64236-151">Beachten Sie, dass die Definition der GetUserIdCallback analysiert den Zeichenfolgenwert in eine ganze Zahl.</span><span class="sxs-lookup"><span data-stu-id="64236-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="64236-152">Wenn Ihr Projekt nicht die generische Implementierung erkennt das **GetUserId** -Methode, müssen Sie möglicherweise das ASP.NET Identity-NuGet-Paket auf Version 2.1 aktualisieren</span><span class="sxs-lookup"><span data-stu-id="64236-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="64236-153">Sie haben zahlreiche Änderungen vorgenommen, auf die Infrastrukturklassen, die von ASP.NET Identity verwendet.</span><span class="sxs-lookup"><span data-stu-id="64236-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="64236-154">Wenn Sie versuchen, Kompilieren des Projekts, bemerken Sie viele Fehler.</span><span class="sxs-lookup"><span data-stu-id="64236-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="64236-155">Glücklicherweise sind die übrigen Fehler ähnliche.</span><span class="sxs-lookup"><span data-stu-id="64236-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="64236-156">Die Identity-Klasse erwartet eine ganze Zahl für den Schlüssel, aber der Controller (oder Web Form) ist einen String-Wert übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="64236-157">In jedem Fall müssen Sie durch Aufrufen von einer Zeichenfolge und ganze Zahl konvertieren **GetUserId&lt;Int&gt;**.</span><span class="sxs-lookup"><span data-stu-id="64236-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="64236-158">Sie können die Fehlerliste aus der Kompilierung funktioniert oder führen Sie die nachfolgenden Änderungen.</span><span class="sxs-lookup"><span data-stu-id="64236-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="64236-159">Die verbleibenden Änderungen richten sich nach dem Typ des Projekts, die Sie erstellen und zu denen die updateverwaltung, die Sie in Visual Studio installiert haben.</span><span class="sxs-lookup"><span data-stu-id="64236-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="64236-160">Sie können direkt zu dem entsprechenden Abschnitt über die folgenden Links wechseln.</span><span class="sxs-lookup"><span data-stu-id="64236-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="64236-161">Ändern Sie für MVC mit Update 2 AccountController-Komponente um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="64236-162">Für MVC mit Update 3 ändern Sie, die AccountController und ManageController, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="64236-163">Ändern Sie für Web Forms mit Update 2 Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="64236-164">Für Webformulare mit Update 3 ändern Sie die Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="64236-165">Ändern Sie für MVC mit Update 2 AccountController-Komponente um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="64236-166">Öffnen Sie die Datei "AccountController.cs".</span><span class="sxs-lookup"><span data-stu-id="64236-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="64236-167">Sie müssen die folgenden Methoden ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-167">You need to change the following methods.</span></span>

<span data-ttu-id="64236-168">**ConfirmEmail** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="64236-169">**Aufheben der Zuordnung** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="64236-170">**Manage(ManageUserViewModel)** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="64236-171">**LinkLoginCallback** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="64236-172">**RemoveAccountList** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="64236-173">**HasPassword** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="64236-174">Sie können jetzt [führen Sie die Anwendung](#run) und einen neuen Benutzer registrieren.</span><span class="sxs-lookup"><span data-stu-id="64236-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="64236-175">Für MVC mit Update 3 ändern Sie, die AccountController und ManageController, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="64236-176">Öffnen Sie die Datei "AccountController.cs".</span><span class="sxs-lookup"><span data-stu-id="64236-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="64236-177">Sie müssen die folgende Methode zu ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-177">You need to change the following method.</span></span>

<span data-ttu-id="64236-178">**ConfirmEmail** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="64236-179">**SendCode** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="64236-180">Öffnen Sie die ManageController.cs-Datei.</span><span class="sxs-lookup"><span data-stu-id="64236-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="64236-181">Sie müssen die folgenden Methoden ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-181">You need to change the following methods.</span></span>

<span data-ttu-id="64236-182">**Index** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="64236-183">**RemoveLogin** Methoden</span><span class="sxs-lookup"><span data-stu-id="64236-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="64236-184">**AddPhoneNumber** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="64236-185">**EnableTwoFactorAuthentication** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="64236-186">**DisableTwoFactorAuthentication** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="64236-187">**VerifyPhoneNumber** Methoden</span><span class="sxs-lookup"><span data-stu-id="64236-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="64236-188">**RemovePhoneNumber** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="64236-189">**ChangePassword** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="64236-190">**SetPassword** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="64236-191">**ManageLogins** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="64236-192">**LinkLoginCallback** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="64236-193">**HasPassword** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="64236-194">**HasPhoneNumber** Methode</span><span class="sxs-lookup"><span data-stu-id="64236-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="64236-195">Sie können jetzt [führen Sie die Anwendung](#run) und einen neuen Benutzer registrieren.</span><span class="sxs-lookup"><span data-stu-id="64236-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="64236-196">Ändern Sie für Web Forms mit Update 2 Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="64236-197">Für Webformulare mit Update 2 müssen Sie die folgenden Seiten ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="64236-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="64236-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="64236-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="64236-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="64236-201">Sie können jetzt [führen Sie die Anwendung](#run) und einen neuen Benutzer registrieren.</span><span class="sxs-lookup"><span data-stu-id="64236-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="64236-202">Für Webformulare mit Update 3 ändern Sie die Konto-Seiten, um den Typ des Schlüssels zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="64236-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="64236-203">Für Webformulare mit Update 3 müssen Sie die folgenden Seiten ändern.</span><span class="sxs-lookup"><span data-stu-id="64236-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="64236-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="64236-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="64236-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="64236-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="64236-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="64236-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="64236-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="64236-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="64236-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="64236-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="64236-212">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="64236-212">Run application</span></span>

<span data-ttu-id="64236-213">Sie haben alle erforderlichen Änderungen an der Standardvorlage für Web-Anwendung abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="64236-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="64236-214">Führen Sie die Anwendung und registrieren Sie einen neuen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="64236-214">Run the application and register a new user.</span></span> <span data-ttu-id="64236-215">Nach der Registrierung des Benutzers werden Sie feststellen, dass die Tabelle "aspnetusers" eine Id-Spalte eine ganze Zahl ist.</span><span class="sxs-lookup"><span data-stu-id="64236-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![neuen Primärschlüssel](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="64236-217">Wenn Sie zuvor die ASP.NET Identity Tabellen mit einem anderen primären Schlüssel erstellt haben, müssen Sie einige zusätzlichen Änderungen vornehmen.</span><span class="sxs-lookup"><span data-stu-id="64236-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="64236-218">Wenn möglich, nur löschen Sie die vorhandene Datenbank.</span><span class="sxs-lookup"><span data-stu-id="64236-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="64236-219">Die Datenbank wird mit den richtigen Entwurf neu erstellt werden, wenn Sie die Webanwendung ausführen und einen neuen Benutzer hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="64236-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="64236-220">Wenn der Löschvorgang nicht möglich ist, führen Sie Code first-Migrationen zum Ändern von Tabellen.</span><span class="sxs-lookup"><span data-stu-id="64236-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="64236-221">Allerdings wird der neue ganzzahlige Primärschlüssel nicht als eine SQL-IDENTITY-Eigenschaft in der Datenbank eingerichtet werden.</span><span class="sxs-lookup"><span data-stu-id="64236-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="64236-222">Sie müssen manuell die Id-Spalte als Identität festlegen.</span><span class="sxs-lookup"><span data-stu-id="64236-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="64236-223">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="64236-223">Other resources</span></span>

- [<span data-ttu-id="64236-224">Übersicht über benutzerdefinierte Speicheranbieter für ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="64236-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="64236-225">Migrieren einer vorhandenen Website von einem SQL-Mitgliedschaftsanbieter nach ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="64236-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="64236-226">Migrieren von Daten eines universellen Anbieters für Mitgliedschaften und Benutzerprofilen nach ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="64236-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="64236-227">[Beispielanwendung](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) mit geänderten Primärschlüssel</span><span class="sxs-lookup"><span data-stu-id="64236-227">[Sample application](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/ChangePK/readme.txt) with changed primary key</span></span>
