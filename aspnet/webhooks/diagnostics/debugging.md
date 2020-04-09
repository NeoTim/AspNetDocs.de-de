---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks-Debugging | Microsoft Docs
author: rick-anderson
description: Debuggen ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675369"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="3ca85-103">ASP.NET WebHooks-Debugging</span><span class="sxs-lookup"><span data-stu-id="3ca85-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="3ca85-104">Debuggen in Azure</span><span class="sxs-lookup"><span data-stu-id="3ca85-104">Debugging in Azure</span></span>

<span data-ttu-id="3ca85-105">Informationen zum Debuggen Ihrer Webanwendung während der Ausführung in Azure finden Sie im Tutorial [Fehlerbehebung für eine Web-App in Azure App Service mit Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="3ca85-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="3ca85-106">Debuggen mit Quelle und Symbolen</span><span class="sxs-lookup"><span data-stu-id="3ca85-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="3ca85-107">Zusätzlich zum Debuggen Ihres eigenen Codes ist es möglich, direkt in Microsoft ASP.NET WebHooks und in der Tat alle .NET zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="3ca85-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="3ca85-108">Dies funktioniert unabhängig davon, ob Sie lokal oder remote debuggen.</span><span class="sxs-lookup"><span data-stu-id="3ca85-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="3ca85-109">Konfigurieren Sie zunächst Visual Studio so, dass die Quelle und die Symbole gefunden werden, indem Sie zu **Debuggen** und dann zu **Optionen und Einstellungen**gehen.</span><span class="sxs-lookup"><span data-stu-id="3ca85-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="3ca85-110">Legen Sie die Optionen wie folgt fest:</span><span class="sxs-lookup"><span data-stu-id="3ca85-110">Set the options like this:</span></span>

![Optionen und Einstellungen](_static/SourceSymbols.png)

<span data-ttu-id="3ca85-112">Fügen Sie dann einen Link zu [symbolsource.org](http://symbolsource.org) zum Herunterladen der Quelle und der Symbole hinzu.</span><span class="sxs-lookup"><span data-stu-id="3ca85-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="3ca85-113">Gehen Sie auf die Registerkarte **Symbole** des Menüs oben und fügen Sie Folgendes als Symbolposition hinzu:</span><span class="sxs-lookup"><span data-stu-id="3ca85-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="3ca85-114">Stellen Sie außerdem sicher, dass das Cacheverzeichnis einen kurzen Namen hat. Andernfalls können die Dateinamen zu lang werden, was dazu führt, dass die Symbole nicht geladen werden.</span><span class="sxs-lookup"><span data-stu-id="3ca85-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="3ca85-115">Ein Beispielpfad ist:</span><span class="sxs-lookup"><span data-stu-id="3ca85-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="3ca85-116">Die Einstellungen sollten wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="3ca85-116">The settings should look similar to this:</span></span>

![Options Symbol Dateispeicherort Beispiel](_static/SymSource.png)
