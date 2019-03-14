---
title: Image-Taghilfsprogramm in ASP.NET Core
author: pkellner
description: Veranschaulicht die Arbeit mit dem Image-Taghilfsprogramm.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: 5eb74a6698911a1c594d11573192cb1b9ed53b49
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030107"
---
# <a name="image-tag-helper-in-aspnet-core"></a><span data-ttu-id="79ef5-103">Image-Taghilfsprogramm in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="79ef5-103">Image Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="79ef5-104">Von [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="79ef5-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="79ef5-105">Das Image-Taghilfsprogramm optimiert das `<img>`-Tag für die Bereitstellung des Cache-Busting-Verhaltens bei statischen Bilddateien.</span><span class="sxs-lookup"><span data-stu-id="79ef5-105">The Image Tag Helper enhances the `<img>` tag to provide cache-busting behavior for static image files.</span></span>

<span data-ttu-id="79ef5-106">Eine Cache-Busting-Zeichenfolge ist ein eindeutiger Wert, der den Hash der statischen Bilddatei darstellt, der an die Asset-URL angefügt ist.</span><span class="sxs-lookup"><span data-stu-id="79ef5-106">A cache-busting string is a unique value representing the hash of the static image file appended to the asset's URL.</span></span> <span data-ttu-id="79ef5-107">Die eindeutige Zeichenfolge fordert Clients (und einige Proxys) auf, das Bild erneut vom Hostwebserver zu laden, und nicht über den Cache des Clients.</span><span class="sxs-lookup"><span data-stu-id="79ef5-107">The unique string prompts clients (and some proxies) to reload the image from the host web server and not from the client's cache.</span></span>

<span data-ttu-id="79ef5-108">Wenn es sich bei der Bildquelle (`src`) um eine statische Datei auf dem Hostwebserver handelt, gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="79ef5-108">If the image source (`src`) is a static file on the host web server:</span></span>

* <span data-ttu-id="79ef5-109">Eine eindeutige Cache-Busting-Zeichenfolge wird als Abfrageparameter an die Bildquelle angefügt.</span><span class="sxs-lookup"><span data-stu-id="79ef5-109">A unique cache-busting string is appended as a query parameter to the image source.</span></span>
* <span data-ttu-id="79ef5-110">Eine eindeutige Anforderungs-URL wird erstellt, die den aktualisierten Anforderungsparameter enthält, wenn die Datei auf dem Hostwebserver geändert wird.</span><span class="sxs-lookup"><span data-stu-id="79ef5-110">If the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span>

<span data-ttu-id="79ef5-111">Eine Übersicht der Taghilfsprogramme finden Sie unter <xref:mvc/views/tag-helpers/intro>.</span><span class="sxs-lookup"><span data-stu-id="79ef5-111">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="79ef5-112">Attribute von Image-Taghilfsprogrammen</span><span class="sxs-lookup"><span data-stu-id="79ef5-112">Image Tag Helper Attributes</span></span>

### <a name="src"></a><span data-ttu-id="79ef5-113">src</span><span class="sxs-lookup"><span data-stu-id="79ef5-113">src</span></span>

<span data-ttu-id="79ef5-114">Um das Image-Taghilfsprogramm zu aktivieren, wird das `src`-Attribut im Element `<img>` benötigt.</span><span class="sxs-lookup"><span data-stu-id="79ef5-114">To activate the Image Tag Helper, the `src` attribute is required on the `<img>` element.</span></span>

<span data-ttu-id="79ef5-115">Die Bildquelle (`src`) muss auf eine physische statische Datei auf dem Server verweisen.</span><span class="sxs-lookup"><span data-stu-id="79ef5-115">The image source (`src`) must point to a physical static file on the server.</span></span> <span data-ttu-id="79ef5-116">Wenn `src` ein Remote-URI ist, wird nicht der Parameter für die Cache-Busting-Abfragezeichenfolge generiert.</span><span class="sxs-lookup"><span data-stu-id="79ef5-116">If the `src` is a remote URI, the cache-busting query string parameter isn't generated.</span></span>

### <a name="asp-append-version"></a><span data-ttu-id="79ef5-117">asp-append-version</span><span class="sxs-lookup"><span data-stu-id="79ef5-117">asp-append-version</span></span>

<span data-ttu-id="79ef5-118">Wenn `asp-append-version` zusätzlich mit einem `true`-Wert sowie einem `src`-Attribut angegeben wird, wird das Image-Taghilfsprogramm aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="79ef5-118">When `asp-append-version` is specified with a `true` value along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="79ef5-119">Im folgenden Beispiel wird ein Image-Taghilfsprogramm verwendet:</span><span class="sxs-lookup"><span data-stu-id="79ef5-119">The following example uses an Image Tag Helper:</span></span>

```cshtml
<img src="~/images/asplogo.png" asp-append-version="true" />
```

<span data-ttu-id="79ef5-120">Wenn die statische Datei im Verzeichnis */wwwroot/images/* vorhanden ist, ähnelt der erstellte HTML-Code folgendem (der Hash wird abweichen):</span><span class="sxs-lookup"><span data-stu-id="79ef5-120">If the static file exists in the directory */wwwroot/images/*, the generated HTML is similar to the following (the hash will be different):</span></span>

```html
<img src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM" />
```

<span data-ttu-id="79ef5-121">Der Wert, der dem Parameter `v` zugewiesen ist, ist der Hashwert der Datei *asplogo.png* auf dem Datenträger.</span><span class="sxs-lookup"><span data-stu-id="79ef5-121">The value assigned to the parameter `v` is the hash value of the *asplogo.png* file on disk.</span></span> <span data-ttu-id="79ef5-122">Wenn der Webserver den Lesezugriff auf die statische Datei, auf die verwiesen wird, nicht erhalten kann, werden im gerenderten Markup keine `v`-Parameter dem Attribut `src` zugefügt.</span><span class="sxs-lookup"><span data-stu-id="79ef5-122">If the web server is unable to obtain read access to the static file, no `v` parameter is added to the `src` attribute in the rendered markup.</span></span>

## <a name="hash-caching-behavior"></a><span data-ttu-id="79ef5-123">Hashverhalten beim Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="79ef5-123">Hash caching behavior</span></span>

<span data-ttu-id="79ef5-124">Das Image-Taghilfsprogramm verwendet den Cacheanbieter auf dem lokalen Webserver, um den berechneten `Sha512`-Hash einer angegebenen Datei zu speichern.</span><span class="sxs-lookup"><span data-stu-id="79ef5-124">The Image Tag Helper uses the cache provider on the local web server to store the calculated `Sha512` hash of a given file.</span></span> <span data-ttu-id="79ef5-125">Wenn die Datei mehrmals angefordert wird, wird der Hash nicht neu berechnet.</span><span class="sxs-lookup"><span data-stu-id="79ef5-125">If the file is requested multiple times, the hash isn't recalculated.</span></span> <span data-ttu-id="79ef5-126">Der Cache wird durch einen Datei-Watcher ungültig gemacht, der an die Datei angefügt wird, wenn der `Sha512`-Hash der Datei berechnet wird.</span><span class="sxs-lookup"><span data-stu-id="79ef5-126">The cache is invalidated by a file watcher that's attached to the file when the file's `Sha512` hash is calculated.</span></span> <span data-ttu-id="79ef5-127">Wenn die Datei auf dem Datenträger geändert wird, wird ein neuer Hash berechnet und zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="79ef5-127">When the file changes on disk, a new hash is calculated and cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79ef5-128">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="79ef5-128">Additional resources</span></span>

* <xref:performance/caching/memory>
