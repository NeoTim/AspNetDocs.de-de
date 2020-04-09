---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks-Empfängerabhängigkeiten | Microsoft Docs
author: rick-anderson
description: Empfängerabhängigkeiten und Abhängigkeitsinjektion in ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675200"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="d1b32-103">ASP.NET WebHooks-Empfängerabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="d1b32-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="d1b32-104">Microsoft ASP.NET WebHooks wurde unter Berücksichtigung der Abhängigkeitsinjektion entwickelt.</span><span class="sxs-lookup"><span data-stu-id="d1b32-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="d1b32-105">Die meisten Abhängigkeiten im System können durch alternative Implementierungen ersetzt werden, die ein Abhängigkeitsinjektionsmodul verwenden.</span><span class="sxs-lookup"><span data-stu-id="d1b32-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="d1b32-106">Eine Liste der Empfängerabhängigkeiten finden Sie unter [DependencyScopeExtensions.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)</span><span class="sxs-lookup"><span data-stu-id="d1b32-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="d1b32-107">Wenn keine Abhängigkeit registriert wurde, wird eine Standardimplementierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="d1b32-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="d1b32-108">Eine Liste der Standardimplementierungen finden Sie unter [ReceiverServices.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)</span><span class="sxs-lookup"><span data-stu-id="d1b32-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
