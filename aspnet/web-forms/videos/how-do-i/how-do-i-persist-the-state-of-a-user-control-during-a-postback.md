---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: In diesem video Chris Pels zeigt, wie den Status der ein oder mehrere Objekte in einem Benutzersteuerelement beibehalten werden. Zuerst wird ein Benutzersteuerelement erstellt, die die Abilit darstellt...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59414776"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[Vorgehensweise]: Beibehalten des Zustands eines Benutzersteuerelements während eines Postbacks
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="d06c1-104">durch [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="d06c1-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="d06c1-105">In diesem video Chris Pels zeigt, wie den Status der ein oder mehrere Objekte in einem Benutzersteuerelement beibehalten werden.</span><span class="sxs-lookup"><span data-stu-id="d06c1-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="d06c1-106">Zuerst wird ein Benutzersteuerelement erstellt, die die Möglichkeit für einen Benutzer an die Filterkriterien für die Suche darstellt.</span><span class="sxs-lookup"><span data-stu-id="d06c1-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="d06c1-107">Darüber hinaus wird eine begleitende Filterklasse erstellt, um die Filterinformationen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d06c1-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="d06c1-108">Das Filter-Steuerelement sowie einige Methoden und Eigenschaften zum Speichern der aktuellen Filterinformationen in die Instanz der Klasse werden verschiedene Elemente der Benutzeroberfläche hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d06c1-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="d06c1-109">Als Nächstes wird die Benutzer Control-Persistenz implementiert, mit dem RegisterRequiresControlState-Methode und zugeordneten speichern/wiederherstellen-Methoden.</span><span class="sxs-lookup"><span data-stu-id="d06c1-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="d06c1-110">Diese Methoden werden die Instanz der-Klasse für den Filter und die Daten während des Seitenpostbacks speichern.</span><span class="sxs-lookup"><span data-stu-id="d06c1-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="d06c1-111">Es gibt eine Beschreibung der Vorgehensweise mehrere Objekte in der Implementierung des Steuerelements Zustand zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d06c1-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="d06c1-112">&#9654;Sehen Sie sich Video (23 Minuten)</span><span class="sxs-lookup"><span data-stu-id="d06c1-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
