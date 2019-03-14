---
title: Problembehandlung bei ASP.NET Core in IIS
author: guardrex
description: Erfahren Sie, wie Sie Probleme mit IIS-Bereitstellungen (IIS = Internet Information Services) von ASP.NET Core-Apps diagnostizieren können.
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 68fcd578c051ae9ba6234cad0465a7ef42f1ed14
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035587"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="c0ed4-103">Problembehandlung bei ASP.NET Core in IIS</span><span class="sxs-lookup"><span data-stu-id="c0ed4-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="c0ed4-104">Von [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="c0ed4-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c0ed4-105">Dieser Artikel enthält Anweisungen zum Diagnostizieren eines Startproblems der ASP.NET Core-App beim Hosten mithilfe von [Internet Information Services (IIS)](/iis).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue when hosting with [Internet Information Services (IIS)](/iis).</span></span> <span data-ttu-id="c0ed4-106">Die in diesem Artikel enthaltenen Informationen gelten für das Hosting in IIS unter Windows Server und Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-106">The information in this article applies to hosting in IIS on Windows Server and Windows Desktop.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="c0ed4-107">In Visual Studio entspricht ein ASP.NET Core-Projekt standardmäßig dem [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)-Hosting während des Debuggens.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-107">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="c0ed4-108">Ein *502.5: Prozessfehler* oder ein *500.30: Startfehler*, der beim lokalen Debuggen auftritt, kann mithilfe der Hinweise in diesem Thema behoben werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-108">A *502.5 - Process Failure* or a *500.30 - Start Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="c0ed4-109">In Visual Studio entspricht ein ASP.NET Core-Projekt standardmäßig dem [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)-Hosting während des Debuggens.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-109">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="c0ed4-110">Ein *502.5: Prozessfehler*, der beim lokalen Debuggen auftritt, kann mithilfe der Hinweise in diesem Thema behoben werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-110">A *502.5 Process Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

::: moniker-end

<span data-ttu-id="c0ed4-111">Weitere Themen zur Problembehandlung:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-111">Additional troubleshooting topics:</span></span>

<xref:host-and-deploy/azure-apps/troubleshoot>  
<span data-ttu-id="c0ed4-112">Obwohl App Service das [ASP.NET Core-Modul](xref:host-and-deploy/aspnet-core-module) und IIS für das Hosten von Apps verwendet, finden Sie im dedizierten Thema weitere, für App Service spezifische Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-112">Although App Service uses the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module) and IIS to host apps, see the dedicated topic for instructions specific to App Service.</span></span>

<xref:fundamentals/error-handling>  
<span data-ttu-id="c0ed4-113">Informationen zur Behandlung von Fehlern in ASP.NET Core-Apps während der Bereitstellung auf einem lokalen System.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-113">Discover how to handle errors in ASP.NET Core apps during development on a local system.</span></span>

[<span data-ttu-id="c0ed4-114">Lernen Sie das Debuggen mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0ed4-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="c0ed4-115">In diesem Thema werden die Features des Visual Studio-Debuggers vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-115">This topic introduces the features of the Visual Studio debugger.</span></span>

[<span data-ttu-id="c0ed4-116">Debuggen mit Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c0ed4-116">Debugging with Visual Studio Code</span></span>](https://code.visualstudio.com/docs/editor/debugging)  
<span data-ttu-id="c0ed4-117">Hier finden Sie weitere Informationen zur integrierten Debuggingunterstützung in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-117">Learn about the debugging support built into Visual Studio Code.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="c0ed4-118">App-Startfehler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-118">App startup errors</span></span>

### <a name="5025-process-failure"></a><span data-ttu-id="c0ed4-119">502.5: Prozessfehler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-119">502.5 Process Failure</span></span>

<span data-ttu-id="c0ed4-120">Der Workerprozess schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-120">The worker process fails.</span></span> <span data-ttu-id="c0ed4-121">Die App wird nicht gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-121">The app doesn't start.</span></span>

<span data-ttu-id="c0ed4-122">Das ASP.NET Core-Modul kann den .NET-Back-End-Prozess nicht starten.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-122">The ASP.NET Core Module attempts to start the backend dotnet process but it fails to start.</span></span> <span data-ttu-id="c0ed4-123">Die Ursache für einen Fehler beim Starten eines Prozesses kann in der Regel über Einträge im [Anwendungsereignisprotokoll](#application-event-log) und im [stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log) ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-123">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span> 

<span data-ttu-id="c0ed4-124">Eine allgemeine Fehlerbedingung ist, dass die App aufgrund einer Version des freigegebenen ASP.NET Core-Frameworks falsch konfiguriert ist, die nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-124">A common failure condition is the app is misconfigured due to targeting a version of the ASP.NET Core shared framework that isn't present.</span></span> <span data-ttu-id="c0ed4-125">Überprüfen Sie, welche Versionen des freigegebenen ASP.NET Core-Frameworks auf dem Zielcomputer installiert sind.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-125">Check which versions of the ASP.NET Core shared framework are installed on the target machine.</span></span>

<span data-ttu-id="c0ed4-126">Die Fehlerseite *502.5: Prozessfehler* wird zurückgegeben, wenn ein falsch konfiguriertes Hosting oder eine falsch konfigurierte App bewirkt, dass der Workerprozess fehlschlägt:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-126">The *502.5 Process Failure* error page is returned when a hosting or app misconfiguration causes the worker process to fail:</span></span>

![Browserfenster mit der Seite „502.5: Prozessfehler“](troubleshoot/_static/process-failure-page.png)

::: moniker range=">= aspnetcore-2.2"

### <a name="50030-in-process-startup-failure"></a><span data-ttu-id="c0ed4-128">500.30: Prozessinterner Startupfehler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-128">500.30 In-Process Startup Failure</span></span>

<span data-ttu-id="c0ed4-129">Der Workerprozess schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-129">The worker process fails.</span></span> <span data-ttu-id="c0ed4-130">Die App wird nicht gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-130">The app doesn't start.</span></span>

<span data-ttu-id="c0ed4-131">Das ASP.NET Core-Modul kann den .NET Core-CLR-In-Process nicht starten.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-131">The ASP.NET Core Module attempts to start the .NET Core CLR in-process, but it fails to start.</span></span> <span data-ttu-id="c0ed4-132">Die Ursache für einen Fehler beim Starten eines Prozesses kann in der Regel über Einträge im [Anwendungsereignisprotokoll](#application-event-log) und im [stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log) ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-132">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span> 

<span data-ttu-id="c0ed4-133">Eine allgemeine Fehlerbedingung ist, dass die App aufgrund einer Version des freigegebenen ASP.NET Core-Frameworks falsch konfiguriert ist, die nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-133">A common failure condition is the app is misconfigured due to targeting a version of the ASP.NET Core shared framework that isn't present.</span></span> <span data-ttu-id="c0ed4-134">Überprüfen Sie, welche Versionen des freigegebenen ASP.NET Core-Frameworks auf dem Zielcomputer installiert sind.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-134">Check which versions of the ASP.NET Core shared framework are installed on the target machine.</span></span>

### <a name="5000-in-process-handler-load-failure"></a><span data-ttu-id="c0ed4-135">500.0: Fehler beim Laden des prozessinternen Handlers</span><span class="sxs-lookup"><span data-stu-id="c0ed4-135">500.0 In-Process Handler Load Failure</span></span>

<span data-ttu-id="c0ed4-136">Der Workerprozess schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-136">The worker process fails.</span></span> <span data-ttu-id="c0ed4-137">Die App wird nicht gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-137">The app doesn't start.</span></span>

<span data-ttu-id="c0ed4-138">Das ASP.NET Core-Modul kann die .NET Core-CLR und den In-Process-Anforderungshandler (*aspnetcorev2_inprocess.dll*) nicht finden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-138">The ASP.NET Core Module fails to find the .NET Core CLR and find the in-process request handler (*aspnetcorev2_inprocess.dll*).</span></span> <span data-ttu-id="c0ed4-139">Überprüfen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-139">Check that:</span></span>

* <span data-ttu-id="c0ed4-140">Diese App legt entweder das NuGet-Paket [Microsoft.AspNetCore.Server.IIS](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) oder das Metapaket [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) als Ziel fest.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-140">The app targets either the [Microsoft.AspNetCore.Server.IIS](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) NuGet package or the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>
* <span data-ttu-id="c0ed4-141">Die Version des freigegebenen ASP.NET Core-Frameworks, die von der App als Ziel festgelegt ist, ist auf dem Zielcomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-141">The version of the ASP.NET Core shared framework that the app targets is installed on the target machine.</span></span>

### <a name="5000-out-of-process-handler-load-failure"></a><span data-ttu-id="c0ed4-142">500.0: Fehler beim Laden des prozessexternen Handlers</span><span class="sxs-lookup"><span data-stu-id="c0ed4-142">500.0 Out-Of-Process Handler Load Failure</span></span>

<span data-ttu-id="c0ed4-143">Der Workerprozess schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-143">The worker process fails.</span></span> <span data-ttu-id="c0ed4-144">Die App wird nicht gestartet.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-144">The app doesn't start.</span></span>

<span data-ttu-id="c0ed4-145">Das ASP.NET Core-Modul kann den Out-of-Process-Hostinganforderungshandler nicht finden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-145">The ASP.NET Core Module fails to find the out-of-process hosting request handler.</span></span> <span data-ttu-id="c0ed4-146">Stellen Sie sicher, dass sich *aspnetcorev2_outofprocess.dll* in einem Unterordner mit *aspnetcorev2.dll* befindet.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-146">Make sure the *aspnetcorev2_outofprocess.dll* is present in a subfolder next to *aspnetcorev2.dll*.</span></span> 

::: moniker-end

### <a name="500-internal-server-error"></a><span data-ttu-id="c0ed4-147">500: Interner Serverfehler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-147">500 Internal Server Error</span></span>

<span data-ttu-id="c0ed4-148">Die App wird gestartet, aber ein Fehler verhindert, dass der Server auf die Anforderung eingeht.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-148">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="c0ed4-149">Dieser Fehler tritt im Code der App während des Starts oder bei der Erstellung einer Antwort auf.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-149">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="c0ed4-150">Die Antwort enthält möglicherweise keinen Inhalt oder die Antwort wird als *500: Interner Serverfehler* im Browser angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-150">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="c0ed4-151">Das Anwendungsereignisprotokoll gibt normalerweise an, dass die Anwendung normal gestartet wurde.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-151">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="c0ed4-152">Aus Sicht des Servers ist dies richtig.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-152">From the server's perspective, that's correct.</span></span> <span data-ttu-id="c0ed4-153">Die App wurde gestartet, sie kann jedoch keine gültige Antwort generieren.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-153">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="c0ed4-154">[Führen Sie die App in einer Eingabeaufforderung](#run-the-app-at-a-command-prompt) auf dem Server aus oder [aktivieren Sie das stdout-Protokoll des ASP.NET Core-Moduls](#aspnet-core-module-stdout-log), um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-154">[Run the app at a command prompt](#run-the-app-at-a-command-prompt) on the server or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

### <a name="failed-to-start-application-errorcode-0x800700c1"></a><span data-ttu-id="c0ed4-155">Fehler beim Starten der Anwendung (ErrorCode 0x800700c1)</span><span class="sxs-lookup"><span data-stu-id="c0ed4-155">Failed to start application (ErrorCode '0x800700c1')</span></span>

```
EventID: 1010
Source: IIS AspNetCore Module V2
Failed to start application '/LM/W3SVC/6/ROOT/', ErrorCode '0x800700c1'.
```

<span data-ttu-id="c0ed4-156">Die App konnte nicht gestartet werden, weil die Assembly der App (*.dll*) nicht geladen werden konnte.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-156">The app failed to start because the app's assembly (*.dll*) couldn't be loaded.</span></span>

<span data-ttu-id="c0ed4-157">Dieser Fehler tritt bei einem Bitanzahlkonflikt zwischen der veröffentlichten App und dem w3wp/iisexpress-Prozess auf.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-157">This error occurs when there's a bitness mismatch between the published app and the w3wp/iisexpress process.</span></span>

<span data-ttu-id="c0ed4-158">Überprüfen Sie, ob die 32-Bit-Einstellung des Anwendungspools korrekt ist:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-158">Confirm that the app pool's 32-bit setting is correct:</span></span>

1. <span data-ttu-id="c0ed4-159">Wählen Sie im IIS-Manager unter **Anwendungspools** den Anwendungspool aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-159">Select the app pool in IIS Manager's **Application Pools**.</span></span>
1. <span data-ttu-id="c0ed4-160">Wählen Sie im Bereich **Aktionen** unter **Anwendungspool bearbeiten** **Erweiterte Einstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-160">Select **Advanced Settings** under **Edit Application Pool** in the **Actions** panel.</span></span>
1. <span data-ttu-id="c0ed4-161">Wählen Sie **32-Bit-Anwendungen aktivieren** aus:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-161">Set **Enable 32-Bit Applications**:</span></span>
   * <span data-ttu-id="c0ed4-162">Wenn Sie eine 32-Bit-(x86)-App bereitstellen, legen Sie den Wert auf `True` fest.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-162">If deploying a 32-bit (x86) app, set the value to `True`.</span></span>
   * <span data-ttu-id="c0ed4-163">Wenn Sie eine 64-Bit-(x64)-App bereitstellen, legen Sie den Wert auf `False` fest.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-163">If deploying a 64-bit (x64) app, set the value to `False`.</span></span>

### <a name="connection-reset"></a><span data-ttu-id="c0ed4-164">Verbindungszurücksetzung</span><span class="sxs-lookup"><span data-stu-id="c0ed4-164">Connection reset</span></span>

<span data-ttu-id="c0ed4-165">Falls ein Fehler auftritt, nachdem die Header gesendet wurden, ist es zu spät für den Server, einen **500: Interner Serverfehler** zu senden, wenn ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-165">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="c0ed4-166">Dies ist häufig der Fall, wenn während der Serialisierung komplexer Objekte für eine Antwort ein Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-166">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="c0ed4-167">Diese Art von Fehler wird angezeigt, wenn ein *Verbindungszurücksetzungsfehler* auf dem Client auftritt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-167">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="c0ed4-168">Mithilfe der [Anwendungsprotokollierung](xref:fundamentals/logging/index) können diese Fehlertypen behoben werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-168">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="c0ed4-169">Standardstarteinschränkungen</span><span class="sxs-lookup"><span data-stu-id="c0ed4-169">Default startup limits</span></span>

<span data-ttu-id="c0ed4-170">Das ASP.NET Core-Modul wurde mit dem Standardwert 120 Sekunden für das *StartupTimeLimit* konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-170">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="c0ed4-171">Wenn der Standardwert beibehalten wird, dauert der Start einer App möglicherweise bis zu zwei Minuten. Erst danach kann das Modul einen Prozessfehler protokollieren.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-171">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="c0ed4-172">Weitere Informationen zum Konfigurieren des Moduls finden Sie unter [Attribute des aspNetCore-Elements](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-172">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="c0ed4-173">Problembehandlung bei App-Startfehlern</span><span class="sxs-lookup"><span data-stu-id="c0ed4-173">Troubleshoot app startup errors</span></span>

### <a name="enable-the-aspnet-core-module-debug-log"></a><span data-ttu-id="c0ed4-174">Aktivieren des Debugprotokolls des ASP.NET Core-Moduls</span><span class="sxs-lookup"><span data-stu-id="c0ed4-174">Enable the ASP.NET Core Module debug log</span></span>

<span data-ttu-id="c0ed4-175">Fügen Sie der *web.config*-Datei der App die folgenden Handlereinstellungen hinzu, um Debugprotokolle des ASP.NET Core-Moduls zu aktivieren:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-175">Add the following handler settings to the app's *web.config* file to enable ASP.NET Core Module debug logs:</span></span>

```xml
<aspNetCore ...>
  <handlerSettings>
    <handlerSetting name="debugLevel" value="file" />
    <handlerSetting name="debugFile" value="c:\temp\ancm.log" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="c0ed4-176">Überprüfen Sie, ob der für das Protokoll angegebene Pfad vorhanden ist, und ob die Identität des Anwendungspools Schreibberechtigungen für den Speicherort hat.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-176">Confirm that the path specified for the log exists and that the app pool's identity has write permissions to the location.</span></span>

### <a name="application-event-log"></a><span data-ttu-id="c0ed4-177">Anwendungsereignisprotokoll</span><span class="sxs-lookup"><span data-stu-id="c0ed4-177">Application Event Log</span></span>

<span data-ttu-id="c0ed4-178">Greifen Sie auf das Anwendungsereignisprotokoll zu:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-178">Access the Application Event Log:</span></span>

1. <span data-ttu-id="c0ed4-179">Öffnen Sie das Menü „Start“, suchen Sie nach der **Ereignisanzeige**, und wählen Sie anschließend die App **Ereignisanzeige** aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-179">Open the Start menu, search for **Event Viewer**, and then select the **Event Viewer** app.</span></span>
1. <span data-ttu-id="c0ed4-180">Öffnen Sie unter **Ereignisanzeige** den Knoten **Windows-Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-180">In **Event Viewer**, open the **Windows Logs** node.</span></span>
1. <span data-ttu-id="c0ed4-181">Wählen Sie **Anwendung** aus, um das Anwendungsereignisprotokoll zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-181">Select **Application** to open the Application Event Log.</span></span>
1. <span data-ttu-id="c0ed4-182">Suchen Sie nach Fehlern, die mit der fehlerhaften App im Zusammenhang stehen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-182">Search for errors associated with the failing app.</span></span> <span data-ttu-id="c0ed4-183">Fehler weisen in der Spalte *Quelle* den Wert *IIS AspNetCore-Modul* oder *IIS Express AspNetCore-Modul* auf.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-183">Errors have a value of *IIS AspNetCore Module* or *IIS Express AspNetCore Module* in the *Source* column.</span></span>

### <a name="run-the-app-at-a-command-prompt"></a><span data-ttu-id="c0ed4-184">Ausführen der App in einer Eingabeaufforderung</span><span class="sxs-lookup"><span data-stu-id="c0ed4-184">Run the app at a command prompt</span></span>

<span data-ttu-id="c0ed4-185">Viele Startfehler erzeugen keine nützlichen Informationen im Anwendungsereignisprotokoll.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-185">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="c0ed4-186">Sie können die Ursache für einige Fehler ermitteln, indem Sie die App in einer Eingabeaufforderung auf dem Hostsystem ausführen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-186">You can find the cause of some errors by running the app at a command prompt on the hosting system.</span></span>

#### <a name="framework-dependent-deployment"></a><span data-ttu-id="c0ed4-187">Framework-abhängige Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="c0ed4-187">Framework-dependent deployment</span></span>

<span data-ttu-id="c0ed4-188">Wenn es sich bei der App um eine [Framework-abhängige Bereitstellung handelt](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span><span class="sxs-lookup"><span data-stu-id="c0ed4-188">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span></span>

1. <span data-ttu-id="c0ed4-189">Navigieren Sie in einer Eingabeaufforderung zum Bereitstellungsordner und führen Sie die App aus, indem Sie die Assembly der App mit *dotnet.exe* ausführen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-189">At a command prompt, navigate to the deployment folder and run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="c0ed4-190">Ersetzen Sie in folgendem Befehl den Namen der Assembly der App durch \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-190">In the following command, substitute the name of the app's assembly for \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span></span>
1. <span data-ttu-id="c0ed4-191">Die Konsolenausgabe der App, die Fehler anzeigt, wird in das Konsolenfenster geschrieben.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-191">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="c0ed4-192">Wenn der Fehler während einer Anforderung an die App auftritt, führen Sie eine Anforderung an den Host und Port aus, auf dem Kestrel empfangsbereit ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-192">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="c0ed4-193">Führen Sie unter Verwendung der Standardhosts und -ports eine Anforderung für `http://localhost:5000/` aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-193">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="c0ed4-194">Wenn die App normalerweise auf die Kestrel-Endpunktadresse reagiert, ist die Problemursache wahrscheinlich die Hostingkonfiguration (anstelle der App).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-194">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the hosting configuration and less likely within the app.</span></span>

#### <a name="self-contained-deployment"></a><span data-ttu-id="c0ed4-195">Eigenständige Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="c0ed4-195">Self-contained deployment</span></span>

<span data-ttu-id="c0ed4-196">Wenn es sich bei der App um eine [eigenständige Bereitstellung](/dotnet/core/deploying/#self-contained-deployments-scd) handelt:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-196">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd):</span></span>

1. <span data-ttu-id="c0ed4-197">Navigieren Sie in einer Eingabeaufforderung zum Bereitstellungsordner und führen Sie die ausführbaren Dateien der App aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-197">At a command prompt, navigate to the deployment folder and run the app's executable.</span></span> <span data-ttu-id="c0ed4-198">Ersetzen Sie in folgendem Befehl den Namen der Assembly der App durch \<assembly_name>: `<assembly_name>.exe`.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-198">In the following command, substitute the name of the app's assembly for \<assembly_name>: `<assembly_name>.exe`.</span></span>
1. <span data-ttu-id="c0ed4-199">Die Konsolenausgabe der App, die Fehler anzeigt, wird in das Konsolenfenster geschrieben.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-199">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="c0ed4-200">Wenn der Fehler während einer Anforderung an die App auftritt, führen Sie eine Anforderung an den Host und Port aus, auf dem Kestrel empfangsbereit ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-200">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="c0ed4-201">Führen Sie unter Verwendung der Standardhosts und -ports eine Anforderung für `http://localhost:5000/` aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-201">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="c0ed4-202">Wenn die App normalerweise auf die Kestrel-Endpunktadresse reagiert, ist die Problemursache wahrscheinlich die Hostingkonfiguration (anstelle der App).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-202">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the hosting configuration and less likely within the app.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="c0ed4-203">stdout-Protokoll des ASP.NET Core-Moduls</span><span class="sxs-lookup"><span data-stu-id="c0ed4-203">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="c0ed4-204">So aktivieren Sie stdout-Protokolle und zeigen diese an:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-204">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="c0ed4-205">Navigieren Sie zum Bereitstellungsordner der Website auf dem Hostsystem.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-205">Navigate to the site's deployment folder on the hosting system.</span></span>
1. <span data-ttu-id="c0ed4-206">Erstellen Sie den Ordner *logs*, wenn dieser nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-206">If the *logs* folder isn't present, create the folder.</span></span> <span data-ttu-id="c0ed4-207">Anweisungen zum Aktivieren von MSBuild für die automatische Erstellung des Ordners *logs* in der Bereitstellung finden Sie im Thema [Verzeichnisstruktur](xref:host-and-deploy/directory-structure).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-207">For instructions on how to enable MSBuild to create the *logs* folder in the deployment automatically, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>
1. <span data-ttu-id="c0ed4-208">Bearbeiten Sie die Datei *web.config*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-208">Edit the *web.config* file.</span></span> <span data-ttu-id="c0ed4-209">Legen Sie **stdoutLogEnabled** auf `true` fest, und ändern Sie den Pfad von **stdoutLogFile** so, dass auf den Ordner *logs* verwiesen wird (Beispiel: `.\logs\stdout`).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-209">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to point to the *logs* folder (for example, `.\logs\stdout`).</span></span> <span data-ttu-id="c0ed4-210">`stdout` im Pfad ist das Präfix des Protokolldateinamens.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-210">`stdout` in the path is the log file name prefix.</span></span> <span data-ttu-id="c0ed4-211">Ein Zeitstempel, eine Prozess-ID und eine Dateierweiterung werden bei der Protokollerstellung automatisch hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-211">A timestamp, process id, and file extension are added automatically when the log is created.</span></span> <span data-ttu-id="c0ed4-212">Mit `stdout` als Präfix des Dateinamens wird eine typische Protokolldatei als *stdout_20180205184032_5412.log* benannt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-212">Using `stdout` as the file name prefix, a typical log file is named *stdout_20180205184032_5412.log*.</span></span> 
1. <span data-ttu-id="c0ed4-213">Stellen Sie sicher, dass die Identität des Anwendungspools über Schreibberechtigungen für den Ordner *Protokolle* verfügt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-213">Ensure your application pool's identity has write permissions to the *logs* folder.</span></span>
1. <span data-ttu-id="c0ed4-214">Speichern Sie die aktualisierte Datei *web.config*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-214">Save the updated *web.config* file.</span></span>
1. <span data-ttu-id="c0ed4-215">Führen Sie eine Anforderung an die App aus.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-215">Make a request to the app.</span></span>
1. <span data-ttu-id="c0ed4-216">Navigieren Sie zu dem Ordner *logs*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-216">Navigate to the *logs* folder.</span></span> <span data-ttu-id="c0ed4-217">Suchen und öffnen Sie das aktuelle stdout-Protokoll.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-217">Find and open the most recent stdout log.</span></span>
1. <span data-ttu-id="c0ed4-218">Untersuchen Sie das Protokoll auf Fehler.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-218">Study the log for errors.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0ed4-219">Deaktivieren Sie die stdout-Protokollierung, wenn die Problembehandlung abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-219">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="c0ed4-220">Bearbeiten Sie die Datei *web.config*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-220">Edit the *web.config* file.</span></span>
1. <span data-ttu-id="c0ed4-221">Legen Sie **stdoutLogEnabled** auf `false` fest.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-221">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="c0ed4-222">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-222">Save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="c0ed4-223">Wenn das stdout-Protokoll nicht deaktiviert wird, können App- oder Serverfehler auftreten.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-223">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="c0ed4-224">Für die Protokollgröße oder die Anzahl von erstellten Protokolldateien ist kein Grenzwert festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-224">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="c0ed4-225">Verwenden Sie für die routinemäßige Protokollierung in einer ASP.NET Core-App eine Protokollierungsbibliothek, die die Protokolldateigröße beschränkt und die Protokolle rotiert.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-225">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="c0ed4-226">Weitere Informationen finden Sie im Artikel zur [Protokollierung von Drittanbietern](xref:fundamentals/logging/index#third-party-logging-providers).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-226">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="enable-the-developer-exception-page"></a><span data-ttu-id="c0ed4-227">Aktivieren der Seite mit Ausnahmen für Entwickler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-227">Enable the Developer Exception Page</span></span>

<span data-ttu-id="c0ed4-228">Die `ASPNETCORE_ENVIRONMENT` [Umgebungsvariable kann zur Datei web.config hinzugefügt werden](xref:host-and-deploy/aspnet-core-module#setting-environment-variables), um die App in der Entwicklungsumgebung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-228">The `ASPNETCORE_ENVIRONMENT` [environment variable can be added to web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) to run the app in the Development environment.</span></span> <span data-ttu-id="c0ed4-229">Solange die Umgebung nicht beim Starten der App von `UseEnvironment` im Host-Builder außer Kraft gesetzt wird, kann die [Seite mit Ausnahmen für Entwickler](xref:fundamentals/error-handling) durch Festlegen der Umgebungsvariable angezeigt werden, wenn die App ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-229">As long as the environment isn't overridden in app startup by `UseEnvironment` on the host builder, setting the environment variable allows the [Developer Exception Page](xref:fundamentals/error-handling) to appear when the app is run.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout"
      hostingModel="InProcess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

<span data-ttu-id="c0ed4-230">Das Festlegen der Umgebungsvariablen für `ASPNETCORE_ENVIRONMENT` wird nur bei der Verwendung von Staging- und Testservern empfohlen, die nicht für das Internet verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-230">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` is only recommended for use on staging and testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="c0ed4-231">Entfernen Sie nach der Fehlerbehebung die Umgebungsvariable aus der Datei *web.config*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-231">Remove the environment variable from the *web.config* file after troubleshooting.</span></span> <span data-ttu-id="c0ed4-232">Informationen zum Festlegen von Umgebungsvariablen in der Datei *web.config* finden Sie unter [Untergeordnetes environmentVariables-Element von aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-232">For information on setting environment variables in *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="c0ed4-233">Häufige Startfehler</span><span class="sxs-lookup"><span data-stu-id="c0ed4-233">Common startup errors</span></span>

<span data-ttu-id="c0ed4-234">Siehe <xref:host-and-deploy/azure-iis-errors-reference>.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-234">See <xref:host-and-deploy/azure-iis-errors-reference>.</span></span> <span data-ttu-id="c0ed4-235">Die meisten der häufig auftretenden Probleme, die den Start von Apps verhindern, werden im Referenzartikel behandelt.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-235">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="obtain-data-from-an-app"></a><span data-ttu-id="c0ed4-236">Abrufen von Daten aus einer App</span><span class="sxs-lookup"><span data-stu-id="c0ed4-236">Obtain data from an app</span></span>

<span data-ttu-id="c0ed4-237">Wenn eine App in der Lage sind, auf Anforderungen zu reagieren, erhalten Sie Anforderungen, Verbindungen und zusätzliche Daten von den Apps über die Inlinemiddleware des Terminals.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-237">If an app is capable of responding to requests, obtain request, connection, and additional data from the app using terminal inline middleware.</span></span> <span data-ttu-id="c0ed4-238">Weitere Informationen und Beispielcode finden Sie unter <xref:test/troubleshoot#obtain-data-from-an-app>.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-238">For more information and sample code, see <xref:test/troubleshoot#obtain-data-from-an-app>.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="c0ed4-239">Langsame oder hängende App</span><span class="sxs-lookup"><span data-stu-id="c0ed4-239">Slow or hanging app</span></span>

<span data-ttu-id="c0ed4-240">Wenn eine App bei einer Anforderung langsam reagiert oder hängt, rufen Sie eine [Dumpdatei](/visualstudio/debugger/using-dump-files) ab und analysieren diese.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-240">When an app responds slowly or hangs on a request, obtain and analyze a [dump file](/visualstudio/debugger/using-dump-files).</span></span> <span data-ttu-id="c0ed4-241">Dumpdateien können mit einem der folgenden Tools abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-241">Dump files can be obtained using any of the following tools:</span></span>

* [<span data-ttu-id="c0ed4-242">ProcDump</span><span class="sxs-lookup"><span data-stu-id="c0ed4-242">ProcDump</span></span>](/sysinternals/downloads/procdump)
* [<span data-ttu-id="c0ed4-243">DebugDiag</span><span class="sxs-lookup"><span data-stu-id="c0ed4-243">DebugDiag</span></span>](https://www.microsoft.com/download/details.aspx?id=49924)
* <span data-ttu-id="c0ed4-244">WinDbg: [Herunterladen von Debugtools für Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debuggen mit WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span><span class="sxs-lookup"><span data-stu-id="c0ed4-244">WinDbg: [Download Debugging tools for Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debugging Using WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="c0ed4-245">Remotedebuggen</span><span class="sxs-lookup"><span data-stu-id="c0ed4-245">Remote debugging</span></span>

<span data-ttu-id="c0ed4-246">Siehe [Remotedebuggen von ASP.NET Core auf einem IIS-Remotecomputer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in der Dokumentation zu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-246">See [Remote Debug ASP.NET Core on a Remote IIS Computer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in the Visual Studio documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="c0ed4-247">Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0ed4-247">Application Insights</span></span>

<span data-ttu-id="c0ed4-248">[Application Insights](/azure/application-insights/) stellt Telemetriedaten von Apps bereit, die von IIS gehostet werden, einschließlich Features für die Fehlerprotokollierung und die Berichterstellung.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-248">[Application Insights](/azure/application-insights/) provides telemetry from apps hosted by IIS, including error logging and reporting features.</span></span> <span data-ttu-id="c0ed4-249">Application Insights kann nur Fehler melden, die nach dem Start der App auftreten, wenn die Protokollierungsfeatures der App verfügbar werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-249">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="c0ed4-250">Weitere Informationen finden Sie unter [Application Insights for ASP.NET Core (Application Insights für ASP.NET Core)](/azure/application-insights/app-insights-asp-net-core).</span><span class="sxs-lookup"><span data-stu-id="c0ed4-250">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="additional-advice"></a><span data-ttu-id="c0ed4-251">Zusätzliche Hinweise</span><span class="sxs-lookup"><span data-stu-id="c0ed4-251">Additional advice</span></span>

<span data-ttu-id="c0ed4-252">Manchmal schlägt eine funktionsfähige App direkt nach der Durchführung eines Upgrades des .NET Core SDK auf dem Entwicklungscomputer oder der Paketversionen in der App fehl.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-252">Sometimes a functioning app fails immediately after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="c0ed4-253">In einigen Fällen können inkohärente Pakete eine App beschädigen, wenn größere Upgrades durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-253">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="c0ed4-254">Die meisten dieser Probleme können durch Befolgung der folgenden Anweisungen behoben werden:</span><span class="sxs-lookup"><span data-stu-id="c0ed4-254">Most of these issues can be fixed by following these instructions:</span></span>

1. <span data-ttu-id="c0ed4-255">Löschen Sie die Ordner *bin* und *obj*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-255">Delete the *bin* and *obj* folders.</span></span>
1. <span data-ttu-id="c0ed4-256">Löschen Sie die Paketcaches unter *%UserProfile%\\.nuget\\packages* und *%LocalAppData%\\Nuget\\v3-cache*.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-256">Clear the package caches at *%UserProfile%\\.nuget\\packages* and *%LocalAppData%\\Nuget\\v3-cache*.</span></span>
1. <span data-ttu-id="c0ed4-257">Stellen Sie das Projekt wieder her und erstellen Sie es neu.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-257">Restore and rebuild the project.</span></span>
1. <span data-ttu-id="c0ed4-258">Überprüfen Sie, ob die vorherige Bereitstellung auf dem Server vollständig gelöscht wurde, bevor Sie die App erneut bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-258">Confirm that the prior deployment on the server has been completely deleted prior to redeploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="c0ed4-259">Sie können Paketcaches ganz einfach löschen, indem Sie `dotnet nuget locals all --clear` über eine Eingabeaufforderung ausführen.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-259">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
>
> <span data-ttu-id="c0ed4-260">Darüber hinaus können Paketcaches mit dem Tool [nuget.exe](https://www.nuget.org/downloads) und durch Ausführung des Befehls `nuget locals all -clear` gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-260">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="c0ed4-261">*nuget.exe* ist wird unter dem Windows Desktop-Betriebssystem nicht gebündelt installiert und muss separat von der [NuGet-Website](https://www.nuget.org/downloads) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="c0ed4-261">*nuget.exe* isn't a bundled install with the Windows desktop operating system and must be obtained separately from the [NuGet website](https://www.nuget.org/downloads).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0ed4-262">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c0ed4-262">Additional resources</span></span>

* <xref:test/troubleshoot>
* <xref:fundamentals/error-handling>
* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/azure-apps/troubleshoot>
