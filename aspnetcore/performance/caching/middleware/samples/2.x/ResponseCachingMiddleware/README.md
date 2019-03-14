---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062717"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="d4bf2-101">Beispiel: ASP.NET Core-Antwort zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="d4bf2-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="d4bf2-102">Dieses Beispiel veranschaulicht die Verwendung von ASP.NET Core [Antworten Zwischenspeichern Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="d4bf2-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="d4bf2-103">Die app reagiert, mit der Indexseite, einschließlich einer `Cache-Control` -Header auf das Verhalten beim Zwischenspeichern zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d4bf2-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="d4bf2-104">Legt auch fest, die app die `Vary` Header zum Konfigurieren des Caches zum Verarbeiten der Antwort nur, wenn die `Accept-Encoding` Header nachfolgender Anforderungen entspricht, die aus der ursprünglichen Anforderung.</span><span class="sxs-lookup"><span data-stu-id="d4bf2-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="d4bf2-105">Beim Ausführen des Beispiels wird die Seite "Index" bereitgestellt, aus dem Cache gespeichert und bis zu 10 Sekunden lang zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="d4bf2-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
