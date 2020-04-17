---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Versionshinweise für ASP.NET und Webtools 2013.1 für Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools 2013.1 für Visual Studio 2012 beschrieben.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543573"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="d0a36-103">Anmerkungen zu dieser Version – ASP.NET and Web Tools 2013.1 für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d0a36-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="d0a36-104">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d0a36-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d0a36-105">In diesem Dokument wird die Veröffentlichung von ASP.NET und Webtools 2013.1 für Visual Studio 2012 beschrieben.</span><span class="sxs-lookup"><span data-stu-id="d0a36-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="d0a36-106">Contents</span><span class="sxs-lookup"><span data-stu-id="d0a36-106">Contents</span></span>

- [<span data-ttu-id="d0a36-107">Installationshinweise</span><span class="sxs-lookup"><span data-stu-id="d0a36-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="d0a36-108">Software-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="d0a36-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="d0a36-109">Neue Funktionen in ASP.NET und Webtools 2013.1 für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d0a36-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="d0a36-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d0a36-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="d0a36-111">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="d0a36-112">ASP.NET MVC 5-Vorlage</span><span class="sxs-lookup"><span data-stu-id="d0a36-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="d0a36-113">ASP.NET Web-API 2-Vorlage</span><span class="sxs-lookup"><span data-stu-id="d0a36-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="d0a36-114">Elementvorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="d0a36-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d0a36-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="d0a36-116">ASP.NET Gerüst</span><span class="sxs-lookup"><span data-stu-id="d0a36-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="d0a36-117">Razor Editor</span><span class="sxs-lookup"><span data-stu-id="d0a36-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="d0a36-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d0a36-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="d0a36-119">Bekannte Probleme und brechende Änderungen</span><span class="sxs-lookup"><span data-stu-id="d0a36-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="d0a36-120">ASP.NET Gerüst</span><span class="sxs-lookup"><span data-stu-id="d0a36-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="d0a36-121">MVC- und Web-API-Gerüstbau - HTTP 404, Fehler nicht gefunden</span><span class="sxs-lookup"><span data-stu-id="d0a36-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="d0a36-122">Visual Studio Express 2012 für Web funktioniert nach dem Hinzufügen eines Gerüstelements nicht mehr</span><span class="sxs-lookup"><span data-stu-id="d0a36-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="d0a36-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="d0a36-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="d0a36-124">Das Anzeigen der cshtml-Datei mit Browse With oder F5 verursacht einen Serverfehler</span><span class="sxs-lookup"><span data-stu-id="d0a36-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="d0a36-125">Url Rewrite und Tilde()</span><span class="sxs-lookup"><span data-stu-id="d0a36-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="d0a36-126">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="d0a36-127">Installationshinweise</span><span class="sxs-lookup"><span data-stu-id="d0a36-127">Installation Notes</span></span>

<span data-ttu-id="d0a36-128">[Installieren](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET und Webtools 2013.1 für Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d0a36-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="d0a36-129">Softwareanforderungen</span><span class="sxs-lookup"><span data-stu-id="d0a36-129">Software Requirements</span></span>

<span data-ttu-id="d0a36-130">Sie müssen entweder Über Visual Studio 2012 oder Visual Studio Express 2012 für Web verfügen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="d0a36-131">Neue Funktionen in ASP.NET und Webtools 2013.1 für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d0a36-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="d0a36-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d0a36-132">Bootstrap</span></span>

<span data-ttu-id="d0a36-133">Wenn Sie MVC 5-Controller und -Ansichten auf gerüsten, verwendet das Markup für die Ansichten [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="d0a36-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="d0a36-134">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="d0a36-135">ASP.NET MVC 5-Vorlage</span><span class="sxs-lookup"><span data-stu-id="d0a36-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="d0a36-136">Wir haben eine neue MVC 5-Vorlage hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="d0a36-137">Es verweist auf die neuesten MVC 5 NuGet-Pakete, und Sie können Gerüste verwenden, um Controller und Ansichten hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="d0a36-138">ASP.NET Web-API 2-Vorlage</span><span class="sxs-lookup"><span data-stu-id="d0a36-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="d0a36-139">Wir haben eine neue Web API 2-Vorlage hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="d0a36-140">Es verweist auf die neuesten NuGet-Pakete der Web-API 2, und Sie können Gerüste verwenden, um Controller und Ansichten hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="d0a36-141">Elementvorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-141">Item Templates</span></span>

<span data-ttu-id="d0a36-142">Wir haben neue Elementvorlagen für MVC 5-Ansichten, Webseiten (Razor 3) und Web-API 2-Controller hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="d0a36-143">Sie installieren die zugehörigen NuGet-Pakete zum Projekt, während sie neue Elemente hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="d0a36-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d0a36-144">Entity Framework 6</span></span>

<span data-ttu-id="d0a36-145">Wenn Sie einen MVC- oder Web-API-Controller mit Entity Framework erstellen, verwenden wir Framework 6.</span><span class="sxs-lookup"><span data-stu-id="d0a36-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="d0a36-146">Weitere Informationen zu Entity Framework finden Sie im [Entity Framework-Versionsverlauf](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="d0a36-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="d0a36-147">Sie können auch entity Framework 6 Tools für Visual Studio 2012 herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="d0a36-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="d0a36-148">Siehe [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="d0a36-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="d0a36-149">ASP.NET Gerüst</span><span class="sxs-lookup"><span data-stu-id="d0a36-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="d0a36-150">ASP.NET Scaffolding ist ein Codegenerierungsframework für ASP.NET Webanwendungen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="d0a36-151">Es erleichtert das Hinzufügen von Boilerplate-Code zu Ihrem Projekt, das mit einem Datenmodell interagiert.</span><span class="sxs-lookup"><span data-stu-id="d0a36-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="d0a36-152">In früheren Versionen von Visual Studio war das Gerüst auf ASP.NET MVC-Projekte beschränkt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="d0a36-153">Mit diesem Update können Sie jetzt Gerüste für jedes ASP.NET Projekt verwenden, einschließlich Web Forms.</span><span class="sxs-lookup"><span data-stu-id="d0a36-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="d0a36-154">Dieses Update unterstützt das Generieren von Seiten für ein Web Forms-Projekt nicht, aber Sie können dennoch Gerüste mit Web forms verwenden, indem Sie dem Projekt MVC-Abhängigkeiten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="d0a36-155">Unterstützung für das Generieren von Seiten für Web forms wird in einem zukünftigen Update hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="d0a36-156">Bei der Verwendung von Gerüsten stellen wir sicher, dass alle erforderlichen Abhängigkeiten im Projekt installiert sind.</span><span class="sxs-lookup"><span data-stu-id="d0a36-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="d0a36-157">Wenn Sie beispielsweise mit einem ASP.NET Web Forms-Projekt beginnen und dann gerüstbauweise einen Web-API-Controller hinzufügen, werden die erforderlichen NuGet-Pakete und -Referenzen automatisch zu Ihrem Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="d0a36-158">Um einem Web Forms-Projekt Ein MVC-Gerüst hinzuzufügen, fügen Sie ein **neues Gerüstelement** hinzu, und wählen Sie **mVC 5 Abhängigkeiten** im Dialogfeld aus.</span><span class="sxs-lookup"><span data-stu-id="d0a36-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="d0a36-159">Es gibt zwei Möglichkeiten für Gerüste MVC; Minimal und voll.</span><span class="sxs-lookup"><span data-stu-id="d0a36-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="d0a36-160">Wenn Sie Minimal auswählen, werden Ihrem Projekt nur die NuGet-Pakete und -Referenzen für ASP.NET MVC hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="d0a36-161">Wenn Sie die Option Voll auswählen, werden die minimalen Abhängigkeiten sowie die erforderlichen Inhaltsdateien für ein MVC-Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="d0a36-162">Unterstützung für Gerüst-Asynchron-Controller verwendet die neuen asynchronen Features von Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="d0a36-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="d0a36-163">Weitere Informationen und Tutorials finden Sie unter [ASP.NET Gerüstübersicht](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0a36-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="d0a36-164">Diese Tutorials zeigen Gerüste mit Visual Studio 2013, sind jedoch auch für ASP.NET und Webtools 2013.1 für Visual Studio 2012 anwendbar.</span><span class="sxs-lookup"><span data-stu-id="d0a36-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="d0a36-165">Razor Editor</span><span class="sxs-lookup"><span data-stu-id="d0a36-165">Razor Editor</span></span>

<span data-ttu-id="d0a36-166">Mit diesem Update unterstützt Visual Studio 2012 jetzt Razor 3-Tools/-bearbeitungen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="d0a36-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d0a36-167">NuGet 2.7</span></span>

<span data-ttu-id="d0a36-168">NuGet 2.7 enthält eine Vielzahl neuer Funktionen, die in [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7)ausführlich beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="d0a36-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="d0a36-169">Diese Version von NuGet entfällt die Notwendigkeit für Benutzer, NuGet explizit die Wiederherstellung fehlender Pakete zu erlauben.</span><span class="sxs-lookup"><span data-stu-id="d0a36-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="d0a36-170">Bei der Installation von NuGet 2.7 stimmen Benutzer implizit der automatischen Wiederherstellung fehlender Pakete zu.</span><span class="sxs-lookup"><span data-stu-id="d0a36-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="d0a36-171">Benutzer können die Paketwiederherstellung über die NuGet-Einstellungen in Visual Studio explizit deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="d0a36-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="d0a36-172">Diese Änderung vereinfacht die Funktionsweise der Paketwiederherstellung.</span><span class="sxs-lookup"><span data-stu-id="d0a36-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="d0a36-173">Bekannte Probleme und brechende Änderungen</span><span class="sxs-lookup"><span data-stu-id="d0a36-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="d0a36-174">ASP.NET Gerüst</span><span class="sxs-lookup"><span data-stu-id="d0a36-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="d0a36-175">MVC- und Web-API-Gerüstbau - HTTP 404, Fehler nicht gefunden</span><span class="sxs-lookup"><span data-stu-id="d0a36-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="d0a36-176">Wenn beim Hinzufügen eines Gerüstelements zu einem Projekt ein Fehler auftritt, ist es möglich, dass das Projekt in einem inkonsistenten Zustand bleibt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="d0a36-177">Einige der vorgenommenen Änderungen als Gerüste werden zurückgesetzt, andere Änderungen, wie z. B. die installierten NuGet-Pakete, werden nicht zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="d0a36-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="d0a36-178">Wenn die Änderungen der Routingkonfiguration zurückgesetzt werden, erhalten Benutzer beim Navigieren zu Gerüstelementen einen HTTP 404-Fehler.</span><span class="sxs-lookup"><span data-stu-id="d0a36-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="d0a36-179">Um diesen Fehler für MVC zu beheben, fügen Sie ein neues Gerüstelement hinzu, und wählen Sie MVC 5-Abhängigkeiten (minimal oder vollständig).</span><span class="sxs-lookup"><span data-stu-id="d0a36-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="d0a36-180">Dieser Prozess fügt dem Projekt alle erforderlichen Änderungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="d0a36-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="d0a36-181">So beheben Sie diesen Fehler für die Web-API:</span><span class="sxs-lookup"><span data-stu-id="d0a36-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="d0a36-182">Fügen Sie Ihrem Projekt die folgende WebApiConfig-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="d0a36-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="d0a36-183">Konfigurieren Sie WebApiConfig.Register\_in der Application Start-Methode in Global.asax wie folgt:</span><span class="sxs-lookup"><span data-stu-id="d0a36-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="d0a36-184">Visual Studio Express 2012 für Web funktioniert nach dem Hinzufügen eines Gerüstelements nicht mehr</span><span class="sxs-lookup"><span data-stu-id="d0a36-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="d0a36-185">Wenn Visual Studio Express 2012 für Web nach dem Hinzufügen eines Gerüstelements mit Entity Framework (z. B. Web API 2 Controller mit Aktionen unter Verwendung von Entity Framework) nicht mehr funktioniert, ist es möglich, dass Visual Studio Express das systemeigene Abbild einer Assembly, die von System.Web.Extensions abhängig ist, nicht geladen hat.</span><span class="sxs-lookup"><span data-stu-id="d0a36-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="d0a36-186">Um dieses Problem zu beheben, konfigurieren Sie Visual Studio Express so, dass es mit dem MSIL-Abbild von System.Web.Extensions funktioniert:</span><span class="sxs-lookup"><span data-stu-id="d0a36-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="d0a36-187">Öffnen Sie die Eingabeaufforderung im Administratormodus.</span><span class="sxs-lookup"><span data-stu-id="d0a36-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="d0a36-188">Wechseln Sie zu %ProgramFiles%'Microsoft Visual Studio 11.0'Common7'IDE oder %ProgramFiles(x86)%'Microsoft Visual Studio 11.0'Common7'IDE (für 64-Bit-Windows).</span><span class="sxs-lookup"><span data-stu-id="d0a36-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="d0a36-189">Öffnen Sie VWDExpress.exe.config in einem Texteditor.</span><span class="sxs-lookup"><span data-stu-id="d0a36-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="d0a36-190">Fügen Sie die &lt;folgende&gt;/&lt;Zeile&gt; unter dem Konfigurationslaufzeitelement hinzu:</span><span class="sxs-lookup"><span data-stu-id="d0a36-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="d0a36-191">Starten Sie Visual Studio Express 2012 für Web neu.</span><span class="sxs-lookup"><span data-stu-id="d0a36-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="d0a36-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="d0a36-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="d0a36-193">Das Anzeigen der cshtml-Datei mit Browse With oder F5 verursacht einen Serverfehler</span><span class="sxs-lookup"><span data-stu-id="d0a36-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="d0a36-194">Wenn Sie ein MVC 5-Projekt in Visual Studio 2012 erstellen (oder in Visual Studio 2012 ein MVC 5-Projekt öffnen, das in Visual Studio 2013 erstellt wurde) und versuchen, eine cshtml-Datei mithilfe von Durchsuchen With oder F5 anzuzeigen, wird eine Fehlermeldung angezeigt, die angibt: **Serverfehler in '/' Anwendung**.</span><span class="sxs-lookup"><span data-stu-id="d0a36-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="d0a36-195">Der Server versucht, zu`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="d0a36-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="d0a36-196">Um dieses Problem zu beheben, ändern Sie die Einstellung **Startaktion** in Ihrem Projekt in **Spezifische Seite**.</span><span class="sxs-lookup"><span data-stu-id="d0a36-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="d0a36-197">Sie müssen keinen Wert für die Seite angeben.</span><span class="sxs-lookup"><span data-stu-id="d0a36-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="d0a36-198">Nachdem Sie diese Änderung vornehmen, navigiert die`http://localhost:XXXX`Auswahl von F5 zum Stamm der Anwendung ( ).</span><span class="sxs-lookup"><span data-stu-id="d0a36-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="d0a36-199">Dieses Verhalten entspricht nicht dem Verhalten für MVC 5-Projekte in Visual Studio 2013, bei dem die Einstellung **Aktuelle Seite** die geöffnete Seite startet.</span><span class="sxs-lookup"><span data-stu-id="d0a36-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="d0a36-200">Url Rewrite und Tilde()</span><span class="sxs-lookup"><span data-stu-id="d0a36-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="d0a36-201">Nach dem Upgrade auf ASP.NET Razor 3 oder ASP.NET MVC 5 funktioniert die Tilde-Notation möglicherweise nicht mehr richtig, wenn Sie URL-Umschreibungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="d0a36-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="d0a36-202">Die URL-Umschreibung wirkt sich auf die tilde()-Notation&gt;in &lt;HTML-Elementen wie &lt;A/&gt;, &lt;SCRIPT/ , LINK/&gt;aus, und als Ergebnis wird die Tilde nicht mehr dem Stammverzeichnis zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="d0a36-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="d0a36-203">Wenn Sie beispielsweise Anforderungen für **asp.net/content** in **asp.net**umschreiben, wird das href-Attribut in &lt;A href="/content/"/&gt; in **/content/content/** anstelle von **/** aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="d0a36-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="d0a36-204">Um diese Änderung zu unterdrücken, können Sie den **IIS\_WasUrlRewritten-Kontext** auf jeder Webseite oder in **\_Application BeginRequest** in Global.asax auf false festlegen.</span><span class="sxs-lookup"><span data-stu-id="d0a36-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="d0a36-205">Vorlagen</span><span class="sxs-lookup"><span data-stu-id="d0a36-205">Templates</span></span>

<span data-ttu-id="d0a36-206">Wenn Sie ASP.NET MVC-Projekte mit Visual Studio 2012 unter Windows 8.1 oder Windows Server 2012 R2 erstellen, zeigt Visual Studio eine Fehlermeldung an, die besagt, dass "Konfigurieren von Web [URL] für ASP.NET 4.5 fehlgeschlagen ist".</span><span class="sxs-lookup"><span data-stu-id="d0a36-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![Konfigurationsfehler](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="d0a36-208">Dieser Fehler wird angezeigt, da Visual Studio 2012 die ASP.NET 4.5-Funktion nicht aktiviert, wenn sie auf diesen Windows-Versionen installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d0a36-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="d0a36-209">Führen Sie die unter [Windows-Features aktivierenden](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)Schritte aus, um ASP.NET 4.5 zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d0a36-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Ein- oder Ausschalten von Windows-Funktionen](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="d0a36-211">Alternativ können Sie ASP.NET 4.5 über die Befehlszeile aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d0a36-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="d0a36-212">Öffnen Sie die Eingabeaufforderung im Administratormodus.</span><span class="sxs-lookup"><span data-stu-id="d0a36-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="d0a36-213">Führen Sie den folgenden Befehl aus, um ASP.NET 4.5 zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d0a36-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
