---
uid: web-api/overview/security/integrated-windows-authentication
title: Integrierte Windows-Authentifizierung | Microsoft-Dokumentation
author: MikeWasson
description: Beschreibt die Verwendung der integrierten Windows-Authentifizierung in ASP.net-Web-API.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424791"
---
# <a name="integrated-windows-authentication"></a><span data-ttu-id="91e15-103">Integrierte Windows-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="91e15-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="91e15-104">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="91e15-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="91e15-105">Die integrierte Windows-Authentifizierung ermöglicht es Benutzern, sich mit Ihren Windows-Anmelde Informationen mithilfe von Kerberos oder NTLM anzumelden.</span><span class="sxs-lookup"><span data-stu-id="91e15-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="91e15-106">Der Client sendet Anmelde Informationen im Autorisierungs Header.</span><span class="sxs-lookup"><span data-stu-id="91e15-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="91e15-107">Die Windows-Authentifizierung ist für Intranetumgebungen am besten geeignet.</span><span class="sxs-lookup"><span data-stu-id="91e15-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="91e15-108">Weitere Informationen finden Sie unter [Windows-Authentifizierung](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span><span class="sxs-lookup"><span data-stu-id="91e15-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="91e15-109">Vorteile</span><span class="sxs-lookup"><span data-stu-id="91e15-109">Advantages</span></span> | <span data-ttu-id="91e15-110">Nachteile</span><span class="sxs-lookup"><span data-stu-id="91e15-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="91e15-111">In IIS integriert.</span><span class="sxs-lookup"><span data-stu-id="91e15-111">Built into IIS.</span></span> | <span data-ttu-id="91e15-112">Wird nicht für Internet Anwendungen empfohlen.</span><span class="sxs-lookup"><span data-stu-id="91e15-112">Not recommended for Internet applications.</span></span> | 
| <span data-ttu-id="91e15-113">Die Benutzer Anmelde Informationen werden nicht in der Anforderung gesendet.</span><span class="sxs-lookup"><span data-stu-id="91e15-113">Does not send the user credentials in the request.</span></span> | <span data-ttu-id="91e15-114">Erfordert die Kerberos-oder NTLM-Unterstützung auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="91e15-114">Requires Kerberos or NTLM support in the client.</span></span> |
| <span data-ttu-id="91e15-115">Wenn der Client Computer zur Domäne gehört (z. b. Intranetanwendung), muss der Benutzer keine Anmelde Informationen eingeben.</span><span class="sxs-lookup"><span data-stu-id="91e15-115">If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="91e15-116">Der Client muss sich in der Active Directory Domäne befinden.</span><span class="sxs-lookup"><span data-stu-id="91e15-116">Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="91e15-117">Wenn Ihre Anwendung in Azure gehostet wird und Sie über eine lokale Active Directory Domäne verfügen, sollten Sie den Verbund Ihres lokalen AD mit Azure Active Directory in Erwägung gezogen.</span><span class="sxs-lookup"><span data-stu-id="91e15-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="91e15-118">Auf diese Weise können sich Benutzer mit Ihren lokalen Anmelde Informationen anmelden, die Authentifizierung erfolgt jedoch Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91e15-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="91e15-119">Weitere Informationen finden Sie unter [Azure-Authentifizierung](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="91e15-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="91e15-120">Um eine Anwendung zu erstellen, die die integrierte Windows-Authentifizierung verwendet, wählen Sie die Vorlage "Intranetanwendung" im MVC 4-Projekt-Assistenten aus.</span><span class="sxs-lookup"><span data-stu-id="91e15-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="91e15-121">Mit dieser Projektvorlage wird die folgende Einstellung in die Web.config Datei eingefügt:</span><span class="sxs-lookup"><span data-stu-id="91e15-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="91e15-122">Auf der Clientseite funktioniert die integrierte Windows-Authentifizierung mit jedem Browser, der das [Aushandlungs](http://www.ietf.org/rfc/rfc4559.txt) Authentifizierungsschema unterstützt, das die meisten wichtigen Browser enthält.</span><span class="sxs-lookup"><span data-stu-id="91e15-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="91e15-123">Für .NET-Client Anwendungen unterstützt die **HttpClient** -Klasse die Windows-Authentifizierung:</span><span class="sxs-lookup"><span data-stu-id="91e15-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="91e15-124">Die Windows-Authentifizierung ist anfällig für Angriffe durch Website übergreifende Anforderungs Fälschung (CSRF).</span><span class="sxs-lookup"><span data-stu-id="91e15-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="91e15-125">Weitere Informationen finden Sie unter [verhindern von Angriffen für Website übergreifende Anforderungs Fälschung (CSRF)](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="91e15-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>
