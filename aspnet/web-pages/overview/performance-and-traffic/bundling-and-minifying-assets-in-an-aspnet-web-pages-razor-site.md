---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Bündelung und Minifying von Assets in einer ASP.NET-Website auf Webseiten | Microsoft Docs
author: rick-anderson
description: Bündelung und Minifizierung sind Möglichkeiten, Ihre Website schneller zu machen. Mit Bundling können Sie mehrere JavaScript- ( .js ) Dateien oder mehrere kaskadierende Stylesheets (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539915"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c2dee-104">Bündeln und Minimieren der Objekte in einer ASP.NET Web Pages-Website (Razor)</span><span class="sxs-lookup"><span data-stu-id="c2dee-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c2dee-105">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c2dee-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c2dee-106">Bündelung und Minifizierung sind Möglichkeiten, Ihre Website schneller zu machen.</span><span class="sxs-lookup"><span data-stu-id="c2dee-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="c2dee-107">Mit Bundling können Sie mehrere JavaScript- (*.js*)-Dateien oder mehrere cascading Stylesheet -*.css*) Dateien kombinieren, so dass sie als Einheit heruntergeladen werden können, anstatt als eine nach der anderen.</span><span class="sxs-lookup"><span data-stu-id="c2dee-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="c2dee-108">Die Minifikation drückt den Leerraum aus und führt andere Komprimierungstypen durch, um die heruntergeladenen Dateien so klein wie möglich zu machen.</span><span class="sxs-lookup"><span data-stu-id="c2dee-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="c2dee-109">Die RC-Version von ASP.NET Webseiten 2 unterstützt keine Bündelung und Minimierung, da das Paket, das die erforderlichen Elemente enthält, noch nicht in Microsoft WebMatrix verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="c2dee-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="c2dee-110">Wir entschuldigen uns für die Unannehmlichkeiten.</span><span class="sxs-lookup"><span data-stu-id="c2dee-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="c2dee-111">Es wird erwartet, dass das Paket in der endgültigen Version von ASP.NET Webseiten 2 und WebMatrix 2 verfügbar sein wird.</span><span class="sxs-lookup"><span data-stu-id="c2dee-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
