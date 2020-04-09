---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Authentifizierung und Autorisierung in ASP.NET Web-API | Microsoft Docs
author: MikeWasson
description: Gibt einen allgemeinen Überblick über die Authentifizierung und Autorisierung in ASP.NET Web-API.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675862"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Authentifizierung und Autorisierung in der ASP.NET Web-API

von [Mike Wasson](https://github.com/MikeWasson)

Sie haben eine Web-API erstellt, möchten aber jetzt den Zugriff darauf steuern. In dieser Artikelserie werden einige Optionen zum Sichern einer Web-API vor nicht autorisierten Benutzern betrachtet. Diese Serie umfasst sowohl die Authentifizierung als auch die Autorisierung.

- *Die Authentifizierung* ist das Wissen über die Identität des Benutzers. Alice meldet sich beispielsweise mit ihrem Benutzernamen und Kennwort an, und der Server verwendet das Kennwort, um Alice zu authentifizieren.
- *Die Autorisierung* entscheidet, ob ein Benutzer eine Aktion ausführen darf. Alice verfügt beispielsweise über die Berechtigung, eine Ressource abzubekommen, aber keine Ressource zu erstellen.

Der erste Artikel der Serie gibt einen allgemeinen Überblick über Authentifizierung und Autorisierung in ASP.NET Web-API. In anderen Themen werden allgemeine Authentifizierungsszenarien für die Web-API beschrieben.

> [!NOTE]
> Danke an die Leute, die diese Serie revue passieren ließen und wertvolles Feedback gaben: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.

## <a name="authentication"></a>Authentifizierung

Die Web-API geht davon aus, dass die Authentifizierung auf dem Host erfolgt. Für das Webhosting ist der Host IIS, der HTTP-Module für die Authentifizierung verwendet. Sie können Ihr Projekt so konfigurieren, dass eines der in IIS oder ASP.NET integrierten Authentifizierungsmodule verwendet wird, oder ein eigenes HTTP-Modul schreiben, um eine benutzerdefinierte Authentifizierung durchzuführen.

Wenn der Host den Benutzer authentifiziert, erstellt er einen *Prinzipal*, bei dem es sich um ein [IPrincipal-Objekt](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) handelt, das den Sicherheitskontext darstellt, unter dem Code ausgeführt wird. Der Host fügt den Prinzipal an den aktuellen Thread an, indem **thread.CurrentPrincipal**gesetzt wird. Der Prinzipal **Identity** enthält ein zugeordnetes Identity-Objekt, das Informationen über den Benutzer enthält. Wenn der Benutzer authentifiziert ist, gibt die **Identity.IsAuthenticated-Eigenschaft** **true**zurück. Bei anonymen Anforderungen gibt **IsAuthenticated** **false**zurück. Weitere Informationen zu Prinzipalen finden Sie unter [Rollenbasierte Sicherheit](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>HTTP-Nachrichtenhandler für die Authentifizierung

Anstatt den Host für die Authentifizierung zu verwenden, können Sie Authentifizierungslogik in einen [HTTP-Nachrichtenhandler eintragen.](../advanced/http-message-handlers.md) In diesem Fall überprüft der Nachrichtenhandler die HTTP-Anforderung und legt den Prinzipal fest.

Wann sollten Sie Nachrichtenhandler für die Authentifizierung verwenden? Hier sind einige Kompromisse:

- Ein HTTP-Modul zeigt alle Anforderungen an, die die ASP.NET-Pipeline durchlaufen. Ein Nachrichtenhandler sieht nur Anforderungen, die an die Web-API weitergeleitet werden.
- Sie können Nachrichtenhandler pro Route festlegen, mit denen Sie ein Authentifizierungsschema auf eine bestimmte Route anwenden können.
- HTTP-Module sind spezifisch für IIS. Nachrichtenhandler sind host-agnostisch, sodass sie sowohl mit Webhosting als auch mit Selbsthosting verwendet werden können.
- HTTP-Module nehmen an der IIS-Protokollierung, -Überwachung usw. teil.
- HTTP-Module werden früher in der Pipeline ausgeführt. Wenn Sie die Authentifizierung in einem Nachrichtenhandler verarbeiten, wird der Prinzipal erst festgelegt, wenn der Handler ausgeführt wird. Darüber hinaus kehrt der Prinzipal zum vorherigen Prinzipal zurück, wenn die Antwort den Nachrichtenhandler verlässt.

Wenn Sie das Selbsthosting nicht unterstützen müssen, ist ein HTTP-Modul im Allgemeinen die bessere Option. Wenn Sie das Selbsthosting unterstützen müssen, sollten Sie einen Nachrichtenhandler in Betracht ziehen.

### <a name="setting-the-principal"></a>Festlegen des Prinzipals

Wenn Ihre Anwendung eine benutzerdefinierte Authentifizierungslogik ausführt, müssen Sie den Prinzipal an zwei Stellen festlegen:

- **Thread.CurrentPrincipal**. Diese Eigenschaft ist die Standardmethode zum Festlegen des Prinzips des Threads in .NET.
- **httpContext.Current.User**. Diese Eigenschaft ist spezifisch für ASP.NET.

Der folgende Code zeigt, wie der Prinzipal festgelegt wird:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Für Webhosting müssen Sie den Prinzipal an beiden Stellen festlegen. Andernfalls kann der Sicherheitskontext inkonsistent werden. Für das Selbsthosting ist **HttpContext.Current** jedoch null. Um sicherzustellen, dass Ihr Code host-agnostisch ist, überprüfen Sie daher, ob NULL ist, bevor Sie **httpContext.Current**zuweisen, wie gezeigt.

## <a name="authorization"></a>Authorization

Die Autorisierung erfolgt später in der Pipeline, näher am Controller. Auf diese Weise können Sie detailliertere Entscheidungen treffen, wenn Sie Zugriff auf Ressourcen gewähren.

- *Autorisierungsfilter* werden vor der Controlleraktion ausgeführt. Wenn die Anforderung nicht autorisiert ist, gibt der Filter eine Fehlerantwort zurück, und die Aktion wird nicht aufgerufen.
- Innerhalb einer Controlleraktion können Sie den aktuellen Prinzipal aus der **ApiController.User-Eigenschaft** abrufen. Sie können z. B. eine Liste von Ressourcen basierend auf dem Benutzernamen filtern und nur die Ressourcen zurückgeben, die zu diesem Benutzer gehören.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>Verwenden des [Authorize]-Attributs

Die Web-API stellt den integrierten Autorisierungsfilter [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)bereit. Dieser Filter überprüft, ob der Benutzer authentifiziert ist. Ist dies nicht der Fall, wird der HTTP-Statuscode 401 (Nicht autorisiert) zurückgegeben, ohne die Aktion aufzuberufen.

Sie können den Filter global, auf Controllerebene oder auf der Ebene einzelner Aktionen anwenden.

**Global:** Um den Zugriff für jeden Web-API-Controller einzuschränken, fügen Sie der globalen Filterliste den **AuthorizeAttribute-Filter** hinzu:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Controller**: Um den Zugriff für einen bestimmten Controller einzuschränken, fügen Sie den Filter als Attribut zum Controller hinzu:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Aktion**: Um den Zugriff für bestimmte Aktionen einzuschränken, fügen Sie das Attribut der Aktionsmethode hinzu:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Alternativ können Sie den Controller einschränken und dann anonymen Zugriff `[AllowAnonymous]` auf bestimmte Aktionen zulassen, indem Sie das Attribut verwenden. Im folgenden Beispiel `Post` ist die Methode `Get` eingeschränkt, aber die Methode ermöglicht anonymen Zugriff.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

In den vorherigen Beispielen ermöglicht der Filter jedem authentifizierten Benutzer den Zugriff auf die eingeschränkten Methoden. nur anonyme Benutzer werden ausgeschlossen. Sie können den Zugriff auch auf bestimmte Benutzer oder auf Benutzer in bestimmten Rollen beschränken:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Der **AuthorizeAttribute-Filter** für Web-API-Controller befindet sich im **Namespace System.Web.Http.** Es gibt einen ähnlichen Filter für MVC-Controller im **Namespace System.Web.Mvc,** der nicht mit Web-API-Controllern kompatibel ist.

### <a name="custom-authorization-filters"></a>Benutzerdefinierte Autorisierungsfilter

Um einen benutzerdefinierten Autorisierungsfilter zu schreiben, leiten Sie einen der folgenden Typen ab:

- **AuthorizeAttribute**. Erweitern Sie diese Klasse, um Autorisierungslogik basierend auf dem aktuellen Benutzer und den Rollen des Benutzers auszuführen.
- **AuthorizationFilterAttribute**. Erweitern Sie diese Klasse, um eine synchrone Autorisierungslogik auszuführen, die nicht unbedingt auf dem aktuellen Benutzer oder der aktuellen Rolle basiert.
- **IAuthorizationFilter**. Implementieren Sie diese Schnittstelle, um asynchrone Autorisierungslogik auszuführen. Wenn Ihre Autorisierungslogik z. B. asynchrone E/A- oder Netzwerkaufrufe ausführt. (Wenn Ihre Autorisierungslogik CPU-gebunden ist, ist es einfacher, von **AuthorizationFilterAttribute**abzuleiten, da Sie dann keine asynchrone Methode schreiben müssen.)

Das folgende Diagramm zeigt die Klassenhierarchie für die **AuthorizeAttribute-Klasse.**

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Autorisierung innerhalb einer Controller-Aktion

In einigen Fällen können Sie die Weiterführung einer Anforderung zulassen, aber das Verhalten basierend auf dem Prinzipal ändern. Die von Ihnen zurückgegebenen Informationen können sich z. B. je nach Rolle des Benutzers ändern. Innerhalb einer Controllermethode können Sie den aktuellen Prinzipal aus der **ApiController.User-Eigenschaft** abrufen.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
