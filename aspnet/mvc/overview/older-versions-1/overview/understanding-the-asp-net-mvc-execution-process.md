---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: Verstehen des ASP.NET MVC-Ausführungsprozesses | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie das ASP.NET MVC-Framework eine Browseranforderung Schritt für Schritt verarbeitet.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541025"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>Grundlegendes zum ASP.NET MVC-Ausführungsprozess

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie das ASP.NET MVC-Framework eine Browseranforderung Schritt für Schritt verarbeitet.

Anforderungen an eine ASP.NET MVC-basierte Webanwendung übergeben zuerst das **UrlRoutingModule-Objekt,** das ein HTTP-Modul ist. Dieses Modul analysiert die Anforderung und führt die Routenauswahl aus. Das **UrlRoutingModule-Objekt** wählt das erste Routenobjekt aus, das der aktuellen Anforderung entspricht. (Ein Routenobjekt ist eine Klasse, die **RouteBase**implementiert und in der Regel eine Instanz der **Route-Klasse** ist.) Wenn keine Routen übereinstimmen, führt das **UrlRoutingModule-Objekt** nichts aus und lässt die Anforderung auf die reguläre ASP.NET oder IIS-Anforderungsverarbeitung zurückfallen.

Aus dem ausgewählten **Route-Objekt** ruft das **UrlRoutingModule-Objekt** das **IRouteHandler-Objekt** ab, das dem **Route-Objekt** zugeordnet ist. In der Regel ist dies in einer MVC-Anwendung eine Instanz von **MvcRouteHandler**. Die **IRouteHandler-Instanz** erstellt ein **IHttpHandler-Objekt** und übergibt ihm das **IHttpContext-Objekt.** Standardmäßig ist die **IHttpHandler-Instanz** für MVC das **MvcHandler-Objekt.** Das **MvcHandler-Objekt** wählt dann den Controller aus, der die Anforderung letztendlich verarbeitet.

> [!NOTE]
> Wenn eine ASP.NET-MVC-Webanwendung in IIS 7.0 ausgeführt wird, ist keine Dateinamenerweiterung für MVC-Projekte erforderlich. In IIS 6.0 erfordert der Handler jedoch, dass Sie der ISAPI-DLL von ASP.NET die Dateinamenerweiterung .mvc zuordnen.

Das Modul und der Handler sind die Einstiegspunkte für das ASP.NET MVC-Framework. Sie führen die folgenden Aktionen aus:

- Auswählen des richtigen Controllers in einer MVC-Webanwendung.
- Abrufen einer bestimmten Controllerinstanz.
- Rufen Sie die **Execute-Methode** des Controllers auf.

Im Folgenden werden die Ausführungsphasen für ein MVC-Webprojekt aufgeführt:

- Empfangen der ersten Anforderung für die Anwendung. 

    - In der Datei Global.asax werden **Route-Objekte** zum **RouteTable-Objekt** hinzugefügt.
- Ausführen des Routings 

    - Das **UrlRoutingModule-Modul** verwendet das erste übereinstimmende **Route-Objekt** in der **RouteTable-Auflistung,** um das **RouteData-Objekt** zu erstellen, das es dann zum Erstellen eines **RequestContext** -**IHttpContext**) -Objekts verwendet.
- Erstellen eines MVC-Anforderungshandlers 

    - Das **MvcRouteHandler-Objekt** erstellt eine Instanz der **MvcHandler-Klasse** und übergibt ihr die **RequestContext-Instanz.**
- Erstellen des Controllers 

    - Das **MvcHandler-Objekt** verwendet die **RequestContext-Instanz,** um das **IControllerFactory-Objekt** (in der Regel eine Instanz der **DefaultControllerFactory-Klasse)** zu identifizieren, mit dem die Controllerinstanz erstellt werden soll.
- Execute controller - Die **MvcHandler-Instanz** ruft die Controller-S-Execute-Methode auf. **Execute** |
- Aufrufen der Aktion 

    - Die meisten Controller erben von der **Controller-Basisklasse.** Bei Controllern, die dies tun, bestimmt das **ControllerActionInvoker-Objekt,** das dem Controller zugeordnet ist, welche Aktionsmethode der aufzurufenden Controllerklasse und ruft diese Methode dann auf.
- Ausführen des Ergebnisses 

    - Eine typische Aktionsmethode kann Benutzereingaben empfangen, die entsprechenden Antwortdaten vorbereiten und dann das Ergebnis ausführen, indem ein Ergebnistyp zurückgegeben wird. Zu den integrierten Ergebnistypen, die ausgeführt werden können, gehören: **ViewResult** (das eine Ansicht rendert und der am häufigsten verwendete Ergebnistyp ist), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**und **EmptyResult**.
