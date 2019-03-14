---
uid: whitepapers/aspnet-and-iis6
title: Ausführen von ASP.NET 1.1 mit IIS 6.0 | Microsoft-Dokumentation
author: rick-anderson
description: Während Windows Server 2003, IIS 6.0 und ASP.NET 1.1 enthält, werden diese Komponenten standardmäßig deaktiviert. In diesem Whitepaper wird beschrieben, wie IIS 6.0 ermöglichen eine...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 38cd0abc1e9133b9b86cff6dd2759ce98ac5a115
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036897"
---
<a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="e7a97-104">Ausführen von ASP.NET 1.1 mit IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="e7a97-104">Running ASP.NET 1.1 with IIS 6.0</span></span>
====================
> <span data-ttu-id="e7a97-105">Während Windows Server 2003, IIS 6.0 und ASP.NET 1.1 enthält, werden diese Komponenten standardmäßig deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="e7a97-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="e7a97-106">Dieses Whitepaper enthält Informationen zum Aktivieren von IIS 6.0 und ASP.NET 1.1 und verschiedene Konfigurationseinstellungen für die optimale Leistung zu erzielen, von IIS und ASP.NET empfohlen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="e7a97-107">Gilt für ASP.NET 1.1 und IIS 6.0.</span><span class="sxs-lookup"><span data-stu-id="e7a97-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>


<span data-ttu-id="e7a97-108">Im Lieferumfang von ASP.NET 1.1 ist Windows Server 2003, die auch die neueste Version von Internet Information Server (IIS) Version 6.0 enthält.</span><span class="sxs-lookup"><span data-stu-id="e7a97-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="e7a97-109">IIS 6.0 und ASP.NET 1.1 integrieren dienen und ASP.NET wird nun standardmäßig die neue IIS 6.0-Worker-Prozessmodell.</span><span class="sxs-lookup"><span data-stu-id="e7a97-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="e7a97-110">ASP.NET 1.1 ist nicht standardmäßig installiert.</span><span class="sxs-lookup"><span data-stu-id="e7a97-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="e7a97-111">Im Gegensatz zu früheren Versionen von Microsoft Server-Betriebssysteme ist Internet Information Server (IIS) nicht standardmäßig aktiviert. Es ist von ASP.NET 1.1.</span><span class="sxs-lookup"><span data-stu-id="e7a97-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="e7a97-112">Es gibt zwei Optionen zum Aktivieren von IIS:</span><span class="sxs-lookup"><span data-stu-id="e7a97-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="e7a97-113">Aktivieren von IIS, Option #1 - Serverkonfigurations-Assistent</span><span class="sxs-lookup"><span data-stu-id="e7a97-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="e7a97-114">Windows Server 2003 umfasst eine neue "Serverkonfigurations-Assistent" damit Sie Ihren Server ordnungsgemäß in den gewünschten Modus konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="e7a97-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="e7a97-115">Zum Starten des Assistenten - Hinweis: zum Ausführen des Assistenten, die Sie als Administrator - angemeldet sein müssen wechseln Sie zu: Starten Sie | Programme | Verwaltung und die Option "Konfiguration des Servers".</span><span class="sxs-lookup"><span data-stu-id="e7a97-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="e7a97-116">Nach dem Auswählen der Bildschirm "Serverkonfigurations-Assistent" Öffnen sollte angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="e7a97-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="e7a97-117">Klicken Sie auf "Weiter &gt;":</span><span class="sxs-lookup"><span data-stu-id="e7a97-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="e7a97-118">Klicken Sie auf "Weiter &gt;"</span><span class="sxs-lookup"><span data-stu-id="e7a97-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="e7a97-119">Auf diesem Bildschirm müssen Sie auf ' Anwendungsserver (IIS, ASP.NET) als die Optionen zum Konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e7a97-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="e7a97-120">Klicken Sie auf "Weiter &gt;".</span><span class="sxs-lookup"><span data-stu-id="e7a97-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="e7a97-121">Nach der Auswahl den Server als Anwendungsserver konfigurieren, wird dieser Bildschirm angezeigt, aufgefordert wird, welche zusätzlichen Funktionen installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="e7a97-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="e7a97-122">Keine der beiden Optionen ist standardmäßig ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="e7a97-122">Neither option is selected by default.</span></span> <span data-ttu-id="e7a97-123">Um ASP.NET automatisch zu aktivieren, müssen Sie auf "Aktivieren von ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="e7a97-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="e7a97-124">Klicken Sie auf "Weiter &gt;".</span><span class="sxs-lookup"><span data-stu-id="e7a97-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="e7a97-125">Dieser Bildschirm zeigt an, welche Optionen sind, installiert werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="e7a97-126">Klicken Sie auf "Weiter &gt;".</span><span class="sxs-lookup"><span data-stu-id="e7a97-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="e7a97-127">Sie werden dieser Bildschirm angezeigt, während die von Ihnen gewählten Option installiert werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="e7a97-128">Es ist normal, andere Dialogfeld angezeigt, die Felder angezeigt werden, wie Dienste installiert werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="e7a97-129">Sie können außerdem den Speicherort von der Windows 2003 Server-Installations-CD aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="e7a97-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="e7a97-130">Klicken Sie auf "Weiter &gt;" Wenn Sie fertig sind.</span><span class="sxs-lookup"><span data-stu-id="e7a97-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="e7a97-131">Klicken Sie auf "Fertig stellen": der Windows Server 2003 ist jetzt konfiguriert, um IIS 6.0 und ASP.NET 1.1 zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="e7a97-132">Aktivieren von IIS, Option #2 – manuelle Konfiguration von IIS und ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e7a97-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="e7a97-133">Wenn Sie nicht, verwenden Sie die "Serverkonfigurations-Assistent möchten" können Sie optional IIS 6.0 und ASP.NET 1.1 mithilfe von "Programme hinzufügen oder entfernen" in der Systemsteuerung installieren.</span><span class="sxs-lookup"><span data-stu-id="e7a97-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="e7a97-134">Öffnen Sie zunächst die Systemsteuerung:</span><span class="sxs-lookup"><span data-stu-id="e7a97-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="e7a97-135">Klicken Sie anschließend auf "Hinzufügen/entfernen Windows Components" werden der Windows-Komponenten-Assistent geöffnet:</span><span class="sxs-lookup"><span data-stu-id="e7a97-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="e7a97-136">Markieren Sie und überprüfen Sie 'Anwendungsserver' aus, und klicken Sie dann auf 'Details'?</span><span class="sxs-lookup"><span data-stu-id="e7a97-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="e7a97-137">Schaltfläche:</span><span class="sxs-lookup"><span data-stu-id="e7a97-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="e7a97-138">Überprüfen Sie zum Installieren von ASP.NET "ASP. NET ".</span><span class="sxs-lookup"><span data-stu-id="e7a97-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="e7a97-139">Klicken Sie auf "OK", um den Assistenten der Windows-Komponenten zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="e7a97-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="e7a97-140">Klicken Sie auf "Weiter &gt;" über den Assistenten zum Installieren von Windows-Komponenten:</span><span class="sxs-lookup"><span data-stu-id="e7a97-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="e7a97-141">Es ist normal, andere Dialogfeld angezeigt, die Felder angezeigt werden, wie Dienste installiert werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="e7a97-142">Sie können außerdem den Speicherort von der Windows 2003 Server-Installations-CD aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="e7a97-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="e7a97-143">Wenn die Installation abgeschlossen ist, sehen Sie den letzten Bildschirm des Assistenten für Windows-Komponente:</span><span class="sxs-lookup"><span data-stu-id="e7a97-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="e7a97-144">IIS 6.0 und ASP.NET 1.1 sind nun konfiguriert und verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e7a97-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="e7a97-145">Empfohlene Einstellungen</span><span class="sxs-lookup"><span data-stu-id="e7a97-145">Recommended Settings</span></span>

<span data-ttu-id="e7a97-146">Bei der Ausführung von ASP.NET 1.1 mit IIS 6.0 stehen mehrere Konfigurationseinstellungen, die empfohlen werden, um eine optimale Leistung von ASP.NET zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="e7a97-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="e7a97-147">Konfigurieren von Worker-Prozess-Speicherlimits</span><span class="sxs-lookup"><span data-stu-id="e7a97-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="e7a97-148">Konfigurieren von Arbeitsprozessen</span><span class="sxs-lookup"><span data-stu-id="e7a97-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="e7a97-149">Konfigurieren von Worker-Prozess-Speicherlimits</span><span class="sxs-lookup"><span data-stu-id="e7a97-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="e7a97-150">Standardmäßig wird IIS 6.0 keine Beschränkung auf die Größe des Arbeitsspeichers festgelegt, die IIS verwenden darf.</span><span class="sxs-lookup"><span data-stu-id="e7a97-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="e7a97-151">ASP. NET Cache-Funktion basiert auf eine Einschränkung des Arbeitsspeichers, damit der Cache nicht verwendete Elemente proaktiv aus dem Arbeitsspeicher entfernen kann.</span><span class="sxs-lookup"><span data-stu-id="e7a97-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="e7a97-152">Es wird empfohlen, dass Sie die speicherwiederverwendung-Feature von IIS 6.0 konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e7a97-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="e7a97-153">So konfigurieren Sie diese öffnen Internetinformationsdienste-Manager (Start | Programme | Verwaltung | Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="e7a97-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="e7a97-154">Sobald geöffnet ist, erweitern Sie den Ordner "Anwendungspools" aus:</span><span class="sxs-lookup"><span data-stu-id="e7a97-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="e7a97-155">Für jeden Anwendungspool:</span><span class="sxs-lookup"><span data-stu-id="e7a97-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="e7a97-156">Mit der rechten Maustaste auf Anwendungspools, z. B. "DefaultAppPool", und wählen Sie "Eigenschaften":</span><span class="sxs-lookup"><span data-stu-id="e7a97-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="e7a97-157">Aktivieren Sie als Nächstes Arbeitsspeicher wiederverwenden, indem Sie entweder auf "maximal verbrauchter Speicher (in MB):".</span><span class="sxs-lookup"><span data-stu-id="e7a97-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="e7a97-158">Der Wert darf nicht mehr als die Menge des Arbeitsspeichers (nicht virtuellen) auf dem Server sein, eine gute Annäherung 60 % des physischen Arbeitsspeichers, d. h. für einen Server mit 512MB physischen Arbeitsspeicher wählen 310.</span><span class="sxs-lookup"><span data-stu-id="e7a97-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="e7a97-159">Es wird außerdem empfohlen, dass die maximale 800 MB nicht überschreiten, wenn Sie einen Adressraum von 2 GB verwenden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="e7a97-160">Wenn der Speicherbereich für die Adresse des Servers/3 GB ist, kann der Höchstwert des Arbeitsspeichers für den Arbeitsprozess so hoch wie 1 800 MB sein:</span><span class="sxs-lookup"><span data-stu-id="e7a97-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="e7a97-161">Klicken Sie auf "Übernehmen" und "OK", um das Dialogfeld "Eigenschaften" zu beenden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="e7a97-162">Wiederholen Sie diesen Schritt für alle verfügbaren Anwendungspools.</span><span class="sxs-lookup"><span data-stu-id="e7a97-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="e7a97-163">Konfigurieren von Worker-Wiederverwendung</span><span class="sxs-lookup"><span data-stu-id="e7a97-163">Configuring worker recycling</span></span>

<span data-ttu-id="e7a97-164">IIS 6.0 ist standardmäßig so konfiguriert, um ihren Arbeitsprozess benötigt alle 29 Stunden wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="e7a97-165">Dies ist etwas aggressiver für eine Anwendung, die Ausführung von ASP.NET aus, und es wird empfohlen, dass automatische Arbeitsprozessen deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="e7a97-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="e7a97-166">Um automatische Arbeitsprozessen zu deaktivieren, öffnen Sie zunächst Internetinformationsdienste-Manager (Start | Programme | Verwaltung | Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="e7a97-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="e7a97-167">Sobald geöffnet ist, erweitern Sie den Ordner "Anwendungspools" aus:</span><span class="sxs-lookup"><span data-stu-id="e7a97-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="e7a97-168">Für jeden Anwendungspool:</span><span class="sxs-lookup"><span data-stu-id="e7a97-168">For each application pool:</span></span>

1. <span data-ttu-id="e7a97-169">Mit der rechten Maustaste auf Anwendungspools, z. B. "DefaultAppPool", und wählen Sie "Eigenschaften":</span><span class="sxs-lookup"><span data-stu-id="e7a97-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="e7a97-170">Deaktivieren Sie "Rbeitsprozesse (in Minuten):":</span><span class="sxs-lookup"><span data-stu-id="e7a97-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="e7a97-171">Klicken Sie auf "Übernehmen" und "OK", um das Dialogfeld "Eigenschaften" zu beenden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="e7a97-172">Wiederholen Sie diesen Schritt für alle verfügbaren Anwendungspools.</span><span class="sxs-lookup"><span data-stu-id="e7a97-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="e7a97-173">Gewährung des Schreibzugriffs auf das Dateisystem</span><span class="sxs-lookup"><span data-stu-id="e7a97-173">Granting write access to the file system</span></span>

<span data-ttu-id="e7a97-174">Wenn Ihre Anwendung Schreibzugriff auf das Dateisystem benötigt, und Sie NTFS, die Sie benötigen verwenden, so ändern Sie eine Access Zugriffssteuerungsliste (ACL) auf den Ordner oder die Datei um ASP.NET Zugriff zu gewähren.</span><span class="sxs-lookup"><span data-stu-id="e7a97-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="e7a97-175">Z. B. ASP.NET gewähren Schreibzugriff auf die c:\inetpub\wwwroot zunächst öffnen Sie Explorer, und navigieren Sie zu dem Verzeichnis:</span><span class="sxs-lookup"><span data-stu-id="e7a97-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="e7a97-176">Als Nächstes mit der rechten Maustaste auf das Verzeichnis, z. B. "Wwwroot" und wählen Sie die Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="e7a97-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="e7a97-177">Wählen Sie das Dialogfeld "Eigenschaften" die Registerkarte "Sicherheit":</span><span class="sxs-lookup"><span data-stu-id="e7a97-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="e7a97-178">Das Verzeichnis c:\inetpub\wwwroot\ ist eines speziellen Verzeichnisses, die spezielle Gruppe für IIS 6.0 "IIS\_WPG" Read wurde bereits erteilt &amp; Berechtigungen ausführen, Ordnerinhalt auflisten und lesen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="e7a97-179">Um Schreibberechtigungen zu gewähren, müssen Sie jedoch das Kontrollkästchen Zulassen für Schreibvorgänge zu aktivieren:</span><span class="sxs-lookup"><span data-stu-id="e7a97-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="e7a97-180">IIS 6.0 ist jetzt Schreibberechtigung für diesen Ordner.</span><span class="sxs-lookup"><span data-stu-id="e7a97-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="e7a97-181">Gewähren von Berechtigungen zum Schreiben in anderen Ordnern, führen Sie diese Schritte aus: Beachten Sie, Sie müssen möglicherweise IIS hinzufügen\_WPG-Gruppe, wenn es nicht bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="e7a97-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="e7a97-182">Gewähren von Schreibberechtigungen für IIS\_WPG jeder ASP.NET-Anwendung in dieses Verzeichnis schreiben können.</span><span class="sxs-lookup"><span data-stu-id="e7a97-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="e7a97-183">Unterstützt die integrierte Authentifizierung mit SQL Server</span><span class="sxs-lookup"><span data-stu-id="e7a97-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="e7a97-184">Integrierte Authentifizierung ermöglicht für SQL Server, Windows NT-Authentifizierung zu nutzen, überprüfen Sie die Anmeldekonten für SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e7a97-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="e7a97-185">Dadurch kann der Benutzer, den Standardprozess des SQL Server-Anmeldung zu umgehen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="e7a97-186">Bei diesem Ansatz kann ein Netzwerkbenutzer eine SQL Server-Datenbank zugreifen, ohne eine separate Anmeldung ID oder ein Kennwort angeben, da SQL Server die Kennwortinformationen zu Benutzern und das aus dem Windows NT Network-Security-Prozess erhält.</span><span class="sxs-lookup"><span data-stu-id="e7a97-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="e7a97-187">Auswählen der integrierten Authentifizierung für ASP.NET-Anwendungen ist eine gute Wahl, da keine Anmeldeinformationen in der Verbindungszeichenfolge für Ihre Anwendung ständig gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="e7a97-188">Stattdessen wird die Verbindungszeichenfolge zur Verbindung mit SQL wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="e7a97-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="e7a97-189">Diese Verbindungszeichenfolge weist SQL Server, die Windows-Anmeldeinformationen der Anwendung versucht, den Zugriff auf SQL Server verwenden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="e7a97-190">Im Fall von ASP.NET/IIS-Schnittstellen 6 wäre dies ein Konto in der IIS\_WPG-Gruppe.</span><span class="sxs-lookup"><span data-stu-id="e7a97-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="e7a97-191">Zum Aktivieren der integrierten Authentifizierung zwischen SQL Server und ASP.NET müssen Sie zuerst sicherstellen, dass SQL Server, für die integrierte Authentifizierung oder im gemischten Modus Authentifizierung konfiguriert ist - überprüfen Sie für Ihren Datenbankadministrator frei, um dies zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="e7a97-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="e7a97-192">Wenn SQL Server in einem dieser beiden Modi ist, können Sie die integrierte Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="e7a97-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="e7a97-193">Öffnen Sie SQL Server Enterprise Manager (Start | Programme | Microsoft SQL Server | Enterprise Manager), wählen Sie den entsprechenden Server, und erweitern Sie den Ordner Sicherheit:</span><span class="sxs-lookup"><span data-stu-id="e7a97-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="e7a97-194">Wenn "BUILTINT\IIS\_WPG" Gruppe ist nicht aufgeführt, mit der rechten Maustaste auf Anmeldungen, und wählen Sie "Neue Anmeldung":</span><span class="sxs-lookup"><span data-stu-id="e7a97-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="e7a97-195">In der "Name:" Textfeld Geben Sie "[Name des Servers bzw. der Domäne] \IIS\_WPG" oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten, um die Auswahl der Windows NT-Benutzers oder einer Gruppe zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="e7a97-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="e7a97-196">Wählen Sie den aktuellen Computer IIS\_WPG-Gruppe, und klicken Sie auf "Hinzufügen" und OK, um die Auswahl zu schließen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="e7a97-197">Sie müssen auch die Standarddatenbank und die Berechtigungen zum Zugriff auf die Datenbank festlegen.</span><span class="sxs-lookup"><span data-stu-id="e7a97-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="e7a97-198">Zum Festlegen die Standarddatenbank wählen Sie aus der Dropdownliste aus, z. B. folgenden Northwind ausgewählt ist:</span><span class="sxs-lookup"><span data-stu-id="e7a97-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="e7a97-199">Klicken Sie anschließend auf der Registerkarte "Datenbankzugriff":</span><span class="sxs-lookup"><span data-stu-id="e7a97-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="e7a97-200">Klicken Sie auf das Kontrollkästchen Zulassen für jede Datenbank, die Sie Zugriff auf zulassen möchten.</span><span class="sxs-lookup"><span data-stu-id="e7a97-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="e7a97-201">Sie müssen auch Datenbankrollen auswählen überprüfen Db\_Besitzer wird sichergestellt, dass die Anmeldung verfügt über alle erforderlichen Berechtigungen zum Verwalten und verwenden die ausgewählte Datenbank.</span><span class="sxs-lookup"><span data-stu-id="e7a97-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="e7a97-202">Klicken Sie auf OK, um das Dialogfeld "Eigenschaft" zu beenden.</span><span class="sxs-lookup"><span data-stu-id="e7a97-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="e7a97-203">Ihre ASP.NET-Anwendung ist jetzt konfiguriert, um die Unterstützung der integrierten SQL Server-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="e7a97-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="e7a97-204">Führen Sie ASP.NET 1.0 nicht im einheitlichen Modus von IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="e7a97-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="e7a97-205">ASP.NET 1.0 unter IIS 6.0 wird nur in IIS 5-Kompatibilitätsmodus unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e7a97-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="e7a97-206">Zum Konfigurieren von ASP.NET 1.0 im IIS 5.0-Kompatibilitätsmodus ausgeführt öffnen Sie Internetdienste-Manager zu, und klicken Sie mit der rechten Maustaste auf die Websites ein, und wählen Sie Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="e7a97-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="e7a97-207">Wechseln Sie zur Registerkarte "Dienst", und überprüfen? Ausführen WWW-Dienst im IIS 5.0-Isolationsmodus?</span><span class="sxs-lookup"><span data-stu-id="e7a97-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
