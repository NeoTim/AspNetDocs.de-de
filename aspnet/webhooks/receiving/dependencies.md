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
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks-Empfängerabhängigkeiten

Microsoft ASP.NET WebHooks wurde unter Berücksichtigung der Abhängigkeitsinjektion entwickelt. Die meisten Abhängigkeiten im System können durch alternative Implementierungen ersetzt werden, die ein Abhängigkeitsinjektionsmodul verwenden.

Eine Liste der Empfängerabhängigkeiten finden Sie unter [DependencyScopeExtensions.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) Wenn keine Abhängigkeit registriert wurde, wird eine Standardimplementierung verwendet. Eine Liste der Standardimplementierungen finden Sie unter [ReceiverServices.](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)
