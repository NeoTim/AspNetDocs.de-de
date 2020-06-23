---
uid: ajax/cdn/overview
title: Microsoft AJAX-Content Delivery Network | Microsoft-Dokumentation
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: b66e812f0324be95effdd8d232baa6a59302b9df
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240601"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="8aa4e-102">Microsoft AJAX Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="8aa4e-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="8aa4e-103">Produktionsanwendungen sollten keine feste Abhängigkeit von CDN-Ressourcen erfordern.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="8aa4e-104">Anwendungen sollten auf das CDN-Asset, auf das verwiesen wird, testen und ein Fall Back-Asset verwenden, wenn das CDN nicht verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="8aa4e-105">Das Microsoft AJAX CDN hat keine SLA oberhalb und über die Verwendung eines Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="8aa4e-106">Verwenden Sie [dieses GitHub-Problem](https://github.com/dotnet/AspNetDocs/issues/116) , um Probleme mit dem Microsoft AJAX CDN zu melden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="8aa4e-107">Inhaltsverzeichnis</span><span class="sxs-lookup"><span data-stu-id="8aa4e-107">Table of Contents</span></span>

<span data-ttu-id="8aa4e-108">**[AJAX.Microsoft.com in AJAX.aspnetcdn.com umbenannt](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="8aa4e-109">**[Unterstützung von Visual Studio. vsdoc](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="8aa4e-110">**[Verwenden von ASP.NET AJAX aus dem CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="8aa4e-111">**[Verwenden von jQuery aus dem CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="8aa4e-112">**[Verwenden der jQuery-Benutzeroberfläche aus dem CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="8aa4e-113">**[Dateien von Drittanbietern im CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="8aa4e-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="8aa4e-114">jQuery-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="8aa4e-115">jQuery-Releases für das CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="8aa4e-116">jQuery-Benutzeroberflächen Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="8aa4e-117">jQuery-Validierungs Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="8aa4e-118">jQuery Mobile Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="8aa4e-119">jQuery-Vorlagen Releases auf dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="8aa4e-120">jQuery-Schleifen Versionen im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="8aa4e-121">jQuery-DataTables-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="8aa4e-122">Modernizr-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="8aa4e-123">Jshint-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="8aa4e-124">Knockout-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="8aa4e-125">Globalisieren von Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="8aa4e-126">Antworten auf Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="8aa4e-127">Bootstrap-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="8aa4e-128">Bootstrap touchkarussell Releases auf dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="8aa4e-129">Hammer.js Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="8aa4e-130">ASP.net Web Forms-und AJAX-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="8aa4e-131">ASP.NET MVC-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="8aa4e-132">ASP.net signalr-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="8aa4e-133">Das Microsoft AJAX Content Delivery Network (CDN) hostet beliebte JavaScript-Bibliotheken von Drittanbietern, z. b. jQuery, und ermöglicht es Ihnen, Sie problemlos zu Ihren Webanwendungen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="8aa4e-134">Beispielsweise können Sie mit der Verwendung von jQuery beginnen, das in diesem CDN gehostet wird. Fügen Sie &lt; &gt; dazu der Seite, die auf AJAX.aspnetcdn.com verweist, ein Skripttag hinzu.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="8aa4e-135">Wenn Sie das CDN nutzen, können Sie die Leistung Ihrer AJAX-Anwendungen erheblich verbessern.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="8aa4e-136">Der Inhalt des CDN wird auf Servern auf der ganzen Welt zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="8aa4e-137">Außerdem ermöglicht das CDN Browser die Wiederverwendung von zwischengespeicherten JavaScript-Dateien von Drittanbietern für Websites, die sich in verschiedenen Domänen befinden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="8aa4e-138">Das CDN unterstützt SSL (HTTPS) für den Fall, dass Sie eine Webseite mithilfe der Secure Sockets Layer bedienen müssen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="8aa4e-139">Das CDN hostet die folgenden Skript Bibliotheken von Drittanbietern, die von den Besitzern dieser Bibliotheken hochgeladen und für Sie lizenziert wurden:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="8aa4e-140">jQuery (www.jQuery.com)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="8aa4e-141">jQuery-Benutzeroberfläche (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="8aa4e-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="8aa4e-143">jQuery-Validierung (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="8aa4e-144">jQuery-Cycle (www.malsup.com/jQuery/Cycle/)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="8aa4e-145">jQuery-DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="8aa4e-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="8aa4e-146">Das Microsoft AJAX CDN enthält auch die folgenden Bibliotheken, die von Microsoft hochgeladen wurden:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="8aa4e-147">ASP.NET AJAX</span><span class="sxs-lookup"><span data-stu-id="8aa4e-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="8aa4e-148">ASP.NET-MVC-JavaScript-Dateien</span><span class="sxs-lookup"><span data-stu-id="8aa4e-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="8aa4e-149">ASP.net signalr JavaScript-Dateien</span><span class="sxs-lookup"><span data-stu-id="8aa4e-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="8aa4e-150">Microsoft beansprucht nicht den Besitz von Drittanbieterbibliotheken, die in diesem CDN gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-151">Die Urheberrechtsinhaber der Bibliotheken sind für Sie lizenziert.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="8aa4e-152">Alle Rechte, die Sie möglicherweise zum herunterladen und verwenden solcher Bibliotheken benötigen, werden ausschließlich von den jeweiligen Urheberrechts Besitzern erteilt.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="8aa4e-153">Da es sich hierbei nicht um Microsoft-Bibliotheken handelt, bietet Microsoft keinerlei Garantien oder Rechte für geistiges Eigentum (einschließlich aller impliziten Patentrechte) für die Drittanbieterbibliotheken, die in diesem CDN gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="8aa4e-154">Wenn Sie die JavaScript-Bibliothek übermitteln möchten, und Ihre Bibliothek ist eine der wichtigsten JavaScript-Bibliotheken (wie unter http://trends.builtwith.com) oder Erweiterungen/Plug-Ins für diese Bibliotheken aufgelistet, die (a) beliebt sind; oder (b) hilfreich für die Verwendung auf ASP.net dann wenden Sie sich an AjaxCDNSubmission@Microsoft.com .</span><span class="sxs-lookup"><span data-stu-id="8aa4e-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="8aa4e-155">AJAX.Microsoft.com in AJAX.aspnetcdn.com umbenannt</span><span class="sxs-lookup"><span data-stu-id="8aa4e-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="8aa4e-156">Das CDN, das verwendet wurde, um den Microsoft.com-Domänen Namen zu verwenden und wurde geändert, um den Domänen Namen aspnetcdn.com zu verwenden</span><span class="sxs-lookup"><span data-stu-id="8aa4e-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="8aa4e-157">Diese Änderung wurde vorgenommen, um die Leistung zu verbessern, weil ein Browser, auf den die Microsoft.com-Domäne verwiesen hat, alle Cookies von dieser Domäne über die Verbindung mit jeder Anforderung senden würde.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="8aa4e-158">Durch das Umbenennen in einen anderen Domänen Namen als Microsoft.com kann die Leistung um bis zu 25% gesteigert werden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="8aa4e-159">Beachten Sie, dass AJAX.Microsoft.com weiterhin funktionsfähig ist, aber AJAX.aspnetcdn.com empfohlen wird.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="8aa4e-160">Altes Format:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="8aa4e-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="8aa4e-161">Neues Format:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="8aa4e-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="8aa4e-162">Unterstützung von Visual Studio. vsdoc</span><span class="sxs-lookup"><span data-stu-id="8aa4e-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="8aa4e-163">Wenn Sie die vsdoc-Dateien ordnungsgemäß mit Visual Studio 2008 verwenden möchten, müssen Sie sicherstellen, dass Visual Studio 2008 SP1 installiert ist und dass der Hotfix für vsdoc-Dateien installiert ist.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="8aa4e-164">Diese erhalten Sie hier:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-164">You can get these from here:</span></span>

- [<span data-ttu-id="8aa4e-165">Herunterladen von Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Herunterladen von Visual Studio 2008 SP1")
- [<span data-ttu-id="8aa4e-166">Herunterladen des vsdoc-Hotfixes für Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Herunterladen des vsdoc-Hotfixes für Visual Studio 2008 SP1")

<span data-ttu-id="8aa4e-167">Visual Studio 2010 unterstützt vsdoc-Dateien ohne zusätzliche Patches.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="8aa4e-168">Verwenden von ASP.NET AJAX aus dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="8aa4e-169">Wenn Sie ASP.NET 4 verwenden, können Sie alle Anforderungen für ASP.NET Framework-Skripts an das CDN umleiten.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="8aa4e-170">Das Abrufen von Skripts aus dem CDN anstelle des lokalen Webservers kann die Leistung von öffentlichen ASP.NET-Websites erheblich verbessern.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="8aa4e-171">Verwenden Sie die Eigenschaft ScriptManager enablecdn, um alle ASP.NET Framework-Skript Anforderungen an das Microsoft AJAX CDN umzuleiten:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="8aa4e-172">Verwenden von jQuery aus dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="8aa4e-173">Sie können jQuery-Skripts verwenden, die auf dem CDN in Ihrer Webanwendung gehostet werden, indem Sie das folgende Skript Element einer Seite hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="8aa4e-174">Das CDN enthält auch die minierte Version des jQuery-Skripts, das Sie mit dem folgenden Element erhalten können:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="8aa4e-175">Fügen Sie das folgende-Element direkt nach dem-Element hinzu, das auf das CDN verweist, um zuzulassen, dass auf Ihrer eigenen Website ein Fall Back für die Seite durchgeführt wird, wenn das CDN nicht verfügbar ist:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="8aa4e-176">Die folgende Beispielseite verwendet die CDN-Version der jQuery-Bibliothek (mit Fall Back auf eine lokale Kopie), um den Inhalt eines div-Elements anzuzeigen, wenn auf eine Schaltfläche geklickt wird.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="8aa4e-177">Weitere Informationen zu jQuery und zum Herunterladen einer lokalen Version von jQuery finden Sie auf der [jQuery](http://jquery.com/) -Website.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="8aa4e-178">Verwenden der jQuery-Benutzeroberfläche aus dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="8aa4e-179">Das CDN hostet außerdem die jQuery-UI-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="8aa4e-180">Die jQuery UI-Bibliothek enthält einen umfangreichen Satz von Widgets und Effekten, die Sie in Ihren ASP.NET-Anwendungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="8aa4e-181">Auf der folgenden Seite wird beispielsweise veranschaulicht, wie Sie den jQuery UI DatePicker im Kontext einer ASP.net-Web Forms Anwendung verwenden können, um einen Popup Kalender anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="8aa4e-182">Wenn Sie den Fokus mit der Tastatur auf das Textfeld verschieben, wird ein Kalender angezeigt:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Mit DatePicker erstellter Popup Kalender](overview/_static/image1.png)

<span data-ttu-id="8aa4e-184">Beachten Sie, dass Sie im obigen Code drei Dateien aus dem CDN einschließen müssen:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="8aa4e-185">Die jQuery-Bibliothek &mdash; die jQuery UI-Bibliothek ist von der jQuery-Bibliothek abhängig.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="8aa4e-186">Sie müssen die jQuery-Bibliothek zu Ihrer Seite hinzufügen, bevor Sie die jQuery UI-Bibliothek hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="8aa4e-187">Die jQuery UI Library die jQuery UI &mdash; Library enthält alle jQuery-Benutzeroberflächen Effekte und-Widgets, wie z. b. das DatePicker-Widget, das auf der obigen Seite verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="8aa4e-188">Ein jQuery UI-Design &mdash; der jQuery-Benutzeroberfläche unterstützt verschiedene Designs.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="8aa4e-189">Die obige Seite enthält einen Link zu einer CSS-Datei, um das Redmond-Design zu importieren.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="8aa4e-190">Alle standardmäßigen jQuery-UI-Designs werden im CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="8aa4e-191">[Besuchen Sie diese Seite](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 für das Microsoft AJAX CDN") , um die Miniaturansichten für jedes Design anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="8aa4e-192">Weitere Informationen zur jQuery UI-Bibliothek finden Sie auf der offiziellen [Website der jQuery-Benutzeroberfläche](http://jQueryUI.com "Website der jQuery-Benutzeroberfläche").</span><span class="sxs-lookup"><span data-stu-id="8aa4e-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="8aa4e-193">Dateien von Drittanbietern im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="8aa4e-194">Das CDN hostet einige der am häufigsten verwendeten JavaScript-Bibliotheken von Drittanbietern.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="8aa4e-195">Microsoft beansprucht nicht den Besitz von Drittanbieterbibliotheken, die in diesem CDN gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-196">Die Urheberrechtsinhaber der Bibliotheken sind für Sie lizenziert.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="8aa4e-197">Alle Rechte, die Sie möglicherweise zum herunterladen und verwenden solcher Bibliotheken benötigen, werden ausschließlich von den jeweiligen Urheberrechts Besitzern erteilt.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="8aa4e-198">Da es sich hierbei nicht um Microsoft-Bibliotheken handelt, bietet Microsoft keinerlei Garantien oder Rechte für geistiges Eigentum (einschließlich aller impliziten Patentrechte) für die Drittanbieterbibliotheken, die in diesem CDN gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-199">jQuery-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-200">Die folgenden Versionen von jQuery werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="8aa4e-201">jQuery-Version 3.5.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="8aa4e-202">jQuery-Version 3.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="8aa4e-203">jQuery-Version 3.4.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="8aa4e-204">jQuery-Version 3.3.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="8aa4e-205">jQuery-Version 3.2.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="8aa4e-206">jQuery-Version 3.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="8aa4e-207">jQuery, Version 3.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="8aa4e-208">jQuery-Version 3.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="8aa4e-209">jQuery-Version 3.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="8aa4e-210">jQuery-Version 2.2.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="8aa4e-211">jQuery-Version 2.2.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="8aa4e-212">jQuery-Version 2.2.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="8aa4e-213">jQuery-Version 2.2.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="8aa4e-214">jQuery-Version 2.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="8aa4e-215">jQuery-Version 2.1.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="8aa4e-216">jQuery-Version 2.1.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="8aa4e-217">jQuery-Version 2.1.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="8aa4e-218">jQuery-Version 2.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="8aa4e-219">jQuery-Version 2.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="8aa4e-220">jQuery-Version 2.0.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="8aa4e-221">jQuery-Version 2.0.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="8aa4e-222">jQuery-Version 2.0.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="8aa4e-223">jQuery, Version 2.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="8aa4e-224">jQuery-Version 1.12.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="8aa4e-225">jQuery-Version 1.12.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="8aa4e-226">jQuery-Version 1.12.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="8aa4e-227">jQuery-Version 1.12.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="8aa4e-228">jQuery-Version 1.12.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="8aa4e-229">jQuery-Version 1.11.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="8aa4e-230">jQuery-Version 1.11.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="8aa4e-231">jQuery-Version 1.11.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="8aa4e-232">jQuery-Version 1.11.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="8aa4e-233">jQuery-Version 1.10.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="8aa4e-234">jQuery-Version 1.10.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="8aa4e-235">jQuery-Version 1.10.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="8aa4e-236">jQuery-Version 1.9.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="8aa4e-237">jQuery-Version 1.9.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="8aa4e-238">jQuery-Version 1.8.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="8aa4e-239">jQuery-Version 1.8.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="8aa4e-240">jQuery-Version 1.8.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="8aa4e-241">jQuery-Version 1.8.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="8aa4e-242">jQuery-Version 1.7.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="8aa4e-243">jQuery-Version 1.7.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="8aa4e-244">jQuery, Version 1,7</span><span class="sxs-lookup"><span data-stu-id="8aa4e-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="8aa4e-245">jQuery-Version 1.6.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="8aa4e-246">jQuery-Version 1.6.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="8aa4e-247">jQuery-Version 1.6.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="8aa4e-248">jQuery-Version 1.6.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="8aa4e-249">jQuery, Version 1,6</span><span class="sxs-lookup"><span data-stu-id="8aa4e-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="8aa4e-250">jQuery-Version 1.5.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="8aa4e-251">jQuery-Version 1.5.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="8aa4e-252">jQuery, Version 1,5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="8aa4e-253">jQuery-Version 1.4.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="8aa4e-254">jQuery-Version 1.4.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="8aa4e-255">jQuery-Version 1.4.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="8aa4e-256">jQuery-Version 1.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="8aa4e-257">jQuery, Version 1,4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="8aa4e-258">jQuery-Version 1.3.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-259">jQuery-Releases für das CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-260">Die folgenden Versionen der jQuery-Migration werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="8aa4e-261">jQuery-Migrations Version 3.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="8aa4e-262">jQuery-Migration Version 1.2.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="8aa4e-263">jQuery-Migration Version 1.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="8aa4e-264">jQuery-Migration Version 1.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="8aa4e-265">jQuery-Migration Version 1.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="8aa4e-266">jQuery-Migration Version 1.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-267">jQuery-Benutzeroberflächen Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-268">Die folgenden Versionen der jQuery UI-Bibliothek werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-269">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-270">jQuery-Benutzeroberfläche 1.12.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "jQuery UI 1.12.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-271">jQuery-Benutzeroberfläche 1.12.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "jQuery UI 1.12.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-272">jQuery-Benutzeroberfläche 1.11.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "jQuery UI 1.11.4 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-273">jQuery-Benutzeroberfläche 1.11.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "jQuery UI 1.11.3 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-274">jQuery-Benutzeroberfläche 1.11.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "jQuery UI 1.11.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-275">jQuery-Benutzeroberfläche 1.11.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "jQuery UI 1.11.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-276">jQuery-Benutzeroberfläche 1.11.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "jQuery UI 1.11.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-277">jQuery-Benutzeroberfläche 1.10.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "jQuery UI 1.10.4 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-278">jQuery-Benutzeroberfläche 1.10.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "jQuery UI 1.10.3 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-279">jQuery-Benutzeroberfläche 1.10.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "jQuery UI 1.10.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-280">jQuery-Benutzeroberfläche 1.10.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "jQuery UI 1.10.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-281">jQuery-Benutzeroberfläche 1.10.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "jQuery UI 1.10.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-282">jQuery-Benutzeroberfläche 1.9.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "jQuery UI 1.9.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-283">jQuery-Benutzeroberfläche 1.9.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "jQuery UI 1.9.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-284">jQuery-Benutzeroberfläche 1.9.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "jQuery UI 1.9.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-285">jQuery-Benutzeroberfläche 1.8.24</span><span class="sxs-lookup"><span data-stu-id="8aa4e-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "jQuery UI 1.8.24 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-286">jQuery-Benutzeroberfläche 1.8.23</span><span class="sxs-lookup"><span data-stu-id="8aa4e-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "jQuery UI 1.8.23 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-287">jQuery-Benutzeroberfläche 1.8.22</span><span class="sxs-lookup"><span data-stu-id="8aa4e-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "jQuery UI 1.8.22 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-288">jQuery-Benutzeroberfläche 1.8.21</span><span class="sxs-lookup"><span data-stu-id="8aa4e-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "jQuery UI 1.8.21 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-289">jQuery-Benutzeroberfläche 1.8.20</span><span class="sxs-lookup"><span data-stu-id="8aa4e-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "jQuery UI 1.8.20 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-290">jQuery-Benutzeroberfläche 1.8.19</span><span class="sxs-lookup"><span data-stu-id="8aa4e-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "jQuery UI 1.8.19 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-291">jQuery-Benutzeroberfläche 1.8.18</span><span class="sxs-lookup"><span data-stu-id="8aa4e-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "jQuery UI 1.8.18 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-292">jQuery-Benutzeroberfläche 1.8.17</span><span class="sxs-lookup"><span data-stu-id="8aa4e-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "jQuery UI 1.8.17 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-293">jQuery-Benutzeroberfläche 1.8.16</span><span class="sxs-lookup"><span data-stu-id="8aa4e-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "jQuery UI 1.8.16 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-294">jQuery-Benutzeroberfläche 1.8.15</span><span class="sxs-lookup"><span data-stu-id="8aa4e-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "jQuery UI 1.8.15 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-295">jQuery-Benutzeroberfläche 1.8.14</span><span class="sxs-lookup"><span data-stu-id="8aa4e-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "jQuery UI 1.8.14 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-296">jQuery-Benutzeroberfläche 1.8.13</span><span class="sxs-lookup"><span data-stu-id="8aa4e-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "jQuery UI 1.8.13 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-297">jQuery-Benutzeroberfläche 1.8.12</span><span class="sxs-lookup"><span data-stu-id="8aa4e-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "jQuery UI 1.8.12 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="8aa4e-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-299">jQuery-Benutzeroberfläche 1.8.10</span><span class="sxs-lookup"><span data-stu-id="8aa4e-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-300">jQuery-Benutzeroberfläche 1.8.9</span><span class="sxs-lookup"><span data-stu-id="8aa4e-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "jQuery UI 1.8.9 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-301">jQuery-Benutzeroberfläche 1.8.8</span><span class="sxs-lookup"><span data-stu-id="8aa4e-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "jQuery UI 1.8.8 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-302">jQuery-Benutzeroberfläche 1.8.7</span><span class="sxs-lookup"><span data-stu-id="8aa4e-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "jQuery UI 1.8.7 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-303">jQuery-Benutzeroberfläche 1.8.6</span><span class="sxs-lookup"><span data-stu-id="8aa4e-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-305">jQuery-Validierungs Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-306">Die folgenden Versionen des [jQuery-Validierungs](https://jqueryvalidation.org/ "jQuery-Validierungs-Plugin") -Plug-ins werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-307">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-308">jQuery Validate 1.19.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-308">jQuery Validate 1.19.2</span></span>](jquery-validate/cdnjqueryvalidate1192.md "jQuery-Validierung 1.19.2")
- [<span data-ttu-id="8aa4e-309">jQuery Validate 1.19.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-309">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery-Validierung 1.19.1")
- [<span data-ttu-id="8aa4e-310">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-310">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery-Validierung 1.19.0")
- [<span data-ttu-id="8aa4e-311">jQuery Validate 1.17.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-311">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery-Validierung 1.17.0")
- [<span data-ttu-id="8aa4e-312">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-312">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="8aa4e-313">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-313">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="8aa4e-314">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-314">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="8aa4e-315">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-315">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="8aa4e-316">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-316">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="8aa4e-317">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-317">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="8aa4e-318">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-318">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="8aa4e-319">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-319">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="8aa4e-320">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-320">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="8aa4e-321">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-321">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="8aa4e-322">jQuery-Überprüfung 1,9</span><span class="sxs-lookup"><span data-stu-id="8aa4e-322">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate Version 1.9")
- [<span data-ttu-id="8aa4e-323">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-323">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate Version 1.8.1")
- [<span data-ttu-id="8aa4e-324">jQuery-Überprüfung 1,8</span><span class="sxs-lookup"><span data-stu-id="8aa4e-324">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate Version 1.8")
- [<span data-ttu-id="8aa4e-325">jQuery-Überprüfung 1,7</span><span class="sxs-lookup"><span data-stu-id="8aa4e-325">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate Version 1.7")
- [<span data-ttu-id="8aa4e-326">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="8aa4e-326">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="8aa4e-327">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-327">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-328">jQuery Mobile Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-328">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-329">Die folgenden Versionen der mobilen jQuery-Bibliothek werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-329">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-330">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-330">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-331">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-331">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-332">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-332">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-333">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-333">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-334">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-334">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-335">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-335">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-336">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-336">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-337">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-337">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-338">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-338">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-339">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-339">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-340">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-340">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-341">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-341">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-342">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-342">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-343">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-343">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-344">jQuery Mobile 1,0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-344">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-345">jQuery Mobile 1,0 RC 2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-345">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-346">jQuery Mobile 1,0 RC 1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-346">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 für das Microsoft AJAX CDN")
- [<span data-ttu-id="8aa4e-347">jQuery Mobile 1,0 Beta 3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-347">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 für das Microsoft AJAX CDN")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-348">jQuery-Vorlagen Releases auf dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-348">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-349">Die folgenden Versionen des jQuery-Vorlagen-Plug-ins werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-349">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-350">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-350">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-351">jQuery Templates Beta 1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-351">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-352">jQuery-Schleifen Versionen im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-352">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-353">Die folgenden Versionen des Plug-Ins für den jQuery-Cycle werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-353">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-354">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-354">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-355">jQuery-Cycle 2,99</span><span class="sxs-lookup"><span data-stu-id="8aa4e-355">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="8aa4e-356">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="8aa4e-356">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="8aa4e-357">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="8aa4e-357">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-358">jQuery-DataTables-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-358">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-359">Die folgenden Versionen des jQuery-DataTables-Plug-ins werden auf diesem CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-359">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="8aa4e-360">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-360">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-361">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-361">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="8aa4e-362">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-362">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="8aa4e-363">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-363">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="8aa4e-364">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-364">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="8aa4e-365">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-365">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="8aa4e-366">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-366">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="8aa4e-367">jQuery-DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-367">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="8aa4e-368">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-368">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-369">Modernizr-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-369">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-370">Die folgenden Releases von [modernizr](http://www.modernizr.com "Modernizr") werden auf dem CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-370">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-371">Jshint-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-371">JSHint Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-372">Die folgenden Versionen von [jshint](http://www.jshint.com "JSHint") werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-372">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-373">Knockout-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-373">Knockout Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-374">Die folgenden Versionen von [Knockout](http://www.knockoutjs.com "K.o.") werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-374">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-375">Globalisieren von Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-375">Globalize Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-376">Die folgenden Releases von [Globalize](https://github.com/jquery/globalize "Globalisierung") werden auf dem CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-376">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="8aa4e-377">Globalize Version 1.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-377">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="8aa4e-378">Globalize Version 0.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-378">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="8aa4e-379">alle Kulturen</span><span class="sxs-lookup"><span data-stu-id="8aa4e-379">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="8aa4e-380">Ersetzen Sie "{Culture-Code}" durch den gewünschten Kultur Code, z. b. globalize.culture.en-GB.js= = Microsoft-Dateien im CDN = = diese Bibliotheken wurden von Microsoft hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-380">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-381">Antworten auf Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-381">Respond Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-382">Die folgenden Releases von [Antworten](https://github.com/scottjehl/Respond "Reagieren") werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-382">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="8aa4e-383">Antworten auf Version 1.4.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-383">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="8aa4e-384">Antworten auf Version 1.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-384">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="8aa4e-385">Antworten auf Version 1.4.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-385">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="8aa4e-386">Antworten auf Version 1.3.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-386">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="8aa4e-387">Antworten auf Version 1.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-387">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-388">Bootstrap-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-388">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-389">Die folgenden Versionen von [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") Bootstrap werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-389">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-450"></a><span data-ttu-id="8aa4e-390">Bootstrap-Version 4.5.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-390">Bootstrap version 4.5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-441"></a><span data-ttu-id="8aa4e-391">Bootstrap-Version 4.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-391">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="8aa4e-392">Bootstrap-Version 4.3.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-392">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="8aa4e-393">Bootstrap Version 4.2.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-393">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="8aa4e-394">Bootstrap-Version 4.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-394">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="8aa4e-395">Bootstrap-Version 4.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-395">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="8aa4e-396">Bootstrap-Version 3.4.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-396">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="8aa4e-397">Bootstrap-Version 3.4.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-397">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="8aa4e-398">Bootstrap-Version 3.3.7</span><span class="sxs-lookup"><span data-stu-id="8aa4e-398">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="8aa4e-399">Bootstrap Version 3.3.6</span><span class="sxs-lookup"><span data-stu-id="8aa4e-399">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="8aa4e-400">Bootstrap-Version 3.3.5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-400">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="8aa4e-401">Bootstrap-Version 3.3.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-401">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="8aa4e-402">Bootstrap-Version 3.3.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-402">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="8aa4e-403">Bootstrap-Version 3.3.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-403">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="8aa4e-404">Bootstrap-Version 3.3.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-404">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="8aa4e-405">Bootstrap-Version 3.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-405">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="8aa4e-406">Bootstrap Version 3.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-406">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="8aa4e-407">Bootstrap-Version 3.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-407">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="8aa4e-408">Bootstrap-Version 3.0.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-408">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="8aa4e-409">Bootstrap-Version 3.0.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-409">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="8aa4e-410">Bootstrap-Version 3.0.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-410">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="8aa4e-411">Bootstrap-Version 3.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-411">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="8aa4e-412">Bootstrap-Version 2.3.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-412">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="8aa4e-413">Bootstrap-Version 2.3.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-413">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-414">Bootstrap touchkarussell Releases auf dem CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-414">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-415">Die folgenden Versionen von [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap touchkarussell-Releases werden auf dem CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-415">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="8aa4e-416">Bootstrap touchkarussell Version 0.8.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-416">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-417">Hammer.js Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-417">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-418">Die folgenden Releases von [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js Releases werden im CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-418">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="8aa4e-419">Hammer.js Version 2.0.4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-419">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-420">ASP.net Web Forms-und AJAX-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-420">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-421">Die folgenden Versionen der ASP.NET AJAX-Bibliothek werden im CDN gehostet.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-421">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="8aa4e-422">Klicken Sie auf die einzelnen Links, um die tatsächliche Liste der Dateien anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="8aa4e-422">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="8aa4e-423">ASP.net Web Forms-und AJAX-Version 4.5.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-423">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms und AJAX 4.5.2")
- [<span data-ttu-id="8aa4e-424">ASP.net Web Forms und AJAX Version 4</span><span class="sxs-lookup"><span data-stu-id="8aa4e-424">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET-Web Forms und AJAX 4")
- [<span data-ttu-id="8aa4e-425">ASP.NET AJAX, Version 3,5</span><span class="sxs-lookup"><span data-stu-id="8aa4e-425">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET AJAX 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-426">ASP.NET MVC-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-426">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-427">Die folgenden ASP.NET-MVC-JavaScript-Dateien werden auf diesem CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-427">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="8aa4e-428">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-428">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="8aa4e-429">ASP.NET MVC 5,1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-429">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="8aa4e-430">ASP.NET MVC 5,0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-430">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="8aa4e-431">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-431">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="8aa4e-432">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-432">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="8aa4e-433">ASP.NET MVC 2,0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-433">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="8aa4e-434">ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-434">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="8aa4e-435">ASP.net signalr-Releases im CDN</span><span class="sxs-lookup"><span data-stu-id="8aa4e-435">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="8aa4e-436">Die folgenden ASP.net signalr JavaScript-Dateien werden auf diesem CDN gehostet:</span><span class="sxs-lookup"><span data-stu-id="8aa4e-436">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="8aa4e-437">ASP.net signalr 2.2.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-437">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="8aa4e-438">ASP.net signalr 2.2.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-438">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="8aa4e-439">ASP.net signalr 2.2.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-439">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="8aa4e-440">ASP.net signalr 2.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-440">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="8aa4e-441">ASP.net signalr 2.0.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-441">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="8aa4e-442">ASP.net signalr 2.0.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-442">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="8aa4e-443">ASP.net signalr 2.0.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-443">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="8aa4e-444">ASP.net signalr 2.0.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-444">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="8aa4e-445">ASP.net signalr 1.1.3</span><span class="sxs-lookup"><span data-stu-id="8aa4e-445">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="8aa4e-446">ASP.net signalr 1.1.2</span><span class="sxs-lookup"><span data-stu-id="8aa4e-446">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="8aa4e-447">ASP.net signalr 1.1.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-447">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="8aa4e-448">ASP.net signalr 1.1.0</span><span class="sxs-lookup"><span data-stu-id="8aa4e-448">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="8aa4e-449">ASP.net signalr 1.0.1</span><span class="sxs-lookup"><span data-stu-id="8aa4e-449">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="8aa4e-450">Informationen zu den Nutzungsbedingungen für das CDN finden Sie unter [Microsoft AJAX CDN-Nutzungsbedingungen](https://www.asp.net/terms-of-use "Nutzungsbedingungen für Microsoft AJAX CDN").</span><span class="sxs-lookup"><span data-stu-id="8aa4e-450">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
