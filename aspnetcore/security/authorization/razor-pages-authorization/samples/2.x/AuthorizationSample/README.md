---
ms.openlocfilehash: 6ceb4bd6580d11ee5d6ff57a895c499308035858
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064037"
---
# <a name="aspnet-core-authorization-sample"></a>Beispiel: ASP.NET Core-Autorisierung

Dieses Beispiel veranschaulicht die Verwendung von Razor Pages-Autorisierung durch Konventionen. In diesem Beispiel wird veranschaulicht, die in beschriebenen Features der [autorisierungskonventionen für Razor Pages](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization) Thema.

Benutzerautorisierung in diesem Beispiel verwendet die Cookie-Authentifizierung, die Funktionen, in beschrieben der [verwenden der Cookieauthentifizierung ohne ASP.NET Core Identity](https://docs.microsoft.com/aspnet/core/security/authentication/cookie) Thema. Weitere Informationen zur Verwendung von ASP.NET Core Identity finden Sie unter <xref:security/authentication/identity>.

Beim Ausführen des Beispiels, verwenden Sie die e-Mail-Adresse **maria.rodriguez@contoso.com** zum Authentifizieren des Benutzers.

## <a name="examples-in-this-sample"></a>Beispiele

| Feature | Beschreibung |
| --- | --- |
| [AuthorizePage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) | Fügt eine [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) auf der Seite mit dem angegebenen Pfad. |
| [AuthorizeFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) | Fügt eine [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) für alle Seiten in einem Ordner mit dem angegebenen Pfad. |
| [AllowAnonymousToPage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) | Fügt eine [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) auf eine Seite mit dem angegebenen Pfad. |
| [AllowAnonymousToFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) | Fügt eine [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) für alle Seiten in einem Ordner mit dem angegebenen Pfad. |
