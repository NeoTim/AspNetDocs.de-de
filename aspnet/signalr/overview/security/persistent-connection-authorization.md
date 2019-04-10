---
uid: signalr/overview/security/persistent-connection-authorization
title: Authentifizierung und Autorisierung für permanente SignalR-Verbindungen | Microsoft-Dokumentation
author: bradygaster
description: In diesem Thema wird beschrieben, wie Autorisierung auf eine permanente Verbindung erzwungen wird. Allgemeine Informationen zum Integrieren von Sicherheit in einer SignalR-Anwendung...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9399addc76b7ba0844efe5b935d16edfdd9ec9f0
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384981"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="de732-104">Authentifizierung und Autorisierung für permanente SignalR-Verbindungen</span><span class="sxs-lookup"><span data-stu-id="de732-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="de732-105">durch [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="de732-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="de732-106">In diesem Thema wird beschrieben, wie Autorisierung auf eine permanente Verbindung erzwungen wird.</span><span class="sxs-lookup"><span data-stu-id="de732-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="de732-107">Allgemeine Informationen über die Sicherheit in einer SignalR-Anwendung integrieren, finden Sie unter [Einführung zur Sicherheit](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="de732-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="de732-108">In diesem Thema verwendeten Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="de732-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="de732-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="de732-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="de732-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="de732-110">.NET 4.5</span></span>
> - <span data-ttu-id="de732-111">SignalR-Version 2</span><span class="sxs-lookup"><span data-stu-id="de732-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="de732-112">Vorherige Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="de732-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="de732-113">Weitere Informationen zu früheren Versionen von SignalR, finden Sie unter [ältere Versionen von SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="de732-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="de732-114">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="de732-114">Questions and comments</span></span>
>
> <span data-ttu-id="de732-115">Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können.</span><span class="sxs-lookup"><span data-stu-id="de732-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="de732-116">Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="de732-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="de732-117">Erzwingen der Autorisierung</span><span class="sxs-lookup"><span data-stu-id="de732-117">Enforce authorization</span></span>

<span data-ttu-id="de732-118">Autorisierungsregeln zu erzwingen, wenn es sich bei Verwendung einer [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) müssen Sie überschreiben die `AuthorizeRequest` Methode.</span><span class="sxs-lookup"><span data-stu-id="de732-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="de732-119">Sie können keine der `Authorize` Attribut mit permanenten Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="de732-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="de732-120">Die `AuthorizeRequest` Methode wird aufgerufen, durch das SignalR Framework vor jeder Anforderung, um sicherzustellen, dass der Benutzer zum Ausführen der angeforderten Aktion berechtigt ist.</span><span class="sxs-lookup"><span data-stu-id="de732-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="de732-121">Die `AuthorizeRequest` Methode wird nicht vom Client aufgerufen; stattdessen authentifiziert den Benutzer über Standardauthentifizierungsmechanismus Ihrer Anwendung.</span><span class="sxs-lookup"><span data-stu-id="de732-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="de732-122">Das folgende Beispiel zeigt, wie Sie Anforderungen an authentifizierte Benutzer beschränken.</span><span class="sxs-lookup"><span data-stu-id="de732-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="de732-123">Sie können eine beliebige benutzerdefinierte Autorisierungslogik in der Methode AuthorizeRequest hinzufügen; Es wird z. B. überprüft, ob ein Benutzer zu einer bestimmten Rolle gehört.</span><span class="sxs-lookup"><span data-stu-id="de732-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
