---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: ASP.NET MVC-Routing – Übersicht (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther wird in diesem Tutorial zeigt, wie ASP.NET MVC-Framework Controlleraktionen Browseranforderungen zugeordnet.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: e2f2246e2126bd6e648f861bcb296fab62a748bb
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59380105"
---
# <a name="aspnet-mvc-routing-overview-c"></a>ASP.NET MVC-Routing – Übersicht (C#)

durch [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther wird in diesem Tutorial zeigt, wie ASP.NET MVC-Framework Controlleraktionen Browseranforderungen zugeordnet.


In diesem Tutorial haben Sie eine Einführung in eine wichtige Funktion von jeder ASP.NET MVC-Anwendung namens *ASP.NET-Routing*. Das Modul ASP.NET-Routing ist verantwortlich für die Zuordnung von eingehenden Browseranforderungen zu bestimmten MVC-Controlleraktionen. Am Ende dieses Lernprogramms werden Sie verstehen, wie die standardmäßige Routingtabelle Controlleraktionen Anforderungen zugeordnet.

## <a name="using-the-default-route-table"></a>Mithilfe der Standardroute-Tabelle

Wenn Sie eine neue ASP.NET MVC-Anwendung erstellen, ist die Anwendung bereits konfiguriert, um die Verwendung von ASP.NET-Routing. ASP.NET-Routing ist Setup an zwei Orten.

ASP.NET-Routing ist zunächst in Ihrer Anwendung Webkonfigurationsdatei (Web.config-Datei) aktiviert. Es gibt vier Abschnitte in der Konfigurationsdatei, die für routing relevant sind: Abschnitt system.web.httpModules, Abschnitt system.web.httpHandlers, Abschnitt system.webserver.modules und Abschnitt system.webserver.handlers. Achten Sie darauf, dass Sie nicht in diesen Abschnitten gelöscht werden, da ohne diese Abschnitte routing nicht mehr funktionieren.

Wichtiger ist, und Zweitens wird eine Routingtabelle, in der Datei Global.asax der Anwendung erstellt. Die Datei "Global.asax" ist eine spezielle Datei, die Ereignishandler für Ereignisse des Anwendungslebenszyklus ASP.NET enthält. Die Routingtabelle wird während des Ereignisses zum Starten der Anwendung erstellt.

Die Datei in Codebeispiel 1 enthält die Standarddatei "Global.asax" für eine ASP.NET MVC-Anwendung.

**Codebeispiel 1 – "Global.asax.cs"**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

Wenn eine MVC-Anwendung zuerst gestartet wird, die Anwendung\_Start()-Methode wird aufgerufen. Diese Methode ruft wiederum die RegisterRoutes()-Methode. Die RegisterRoutes()-Methode erstellt die Routentabelle an.

Die Standardroutingtabelle enthält eine einzelne Route (mit dem Namen "Default"). Ordnet die Standardroute das erste Segment der URL einen Controllernamen ein, das zweite Segment einer URL auf eine Controlleraktion durchzuführen und das dritte Segment, das einen Parameter namens **Id**.

Stellen Sie sich, dass Sie die folgende URL in die Adressleiste des Webbrowsers eingeben:

/Home/Index/3

Die Standardroute ordnet diese URL die folgenden Parameter:

- Controller = Home

- Aktion = Index

- id = 3

Wenn Sie die URL/Home/Index/3 anfordern, wird der folgende Code ausgeführt:

HomeController.Index(3)

Die Standardroute enthält Standardwerte für alle drei Parameter. Wenn Sie einen Controller nicht bereitgestellt wird, klicken Sie dann der Controller Parameter standardmäßig auf den Wert **Startseite**. Wenn Sie nicht, dass eine Aktion angeben, die Action-Parameter nimmt standardmäßig den Wert **Index**. Wenn Sie eine Id angeben nicht, standardmäßig der Id-Parameter zum Schluss auf eine leere Zeichenfolge.

Wir sehen uns einige Beispiele wie die Standardroute Controlleraktionen URLs zugeordnet. Stellen Sie sich, dass Sie die folgende URL in die Adressleiste Ihres Browsers eingeben:

/ Home

Aufgrund der standardmäßigen Parameter routenstandardwerte wird diese URL eingeben die Index()-Methode der HomeController-Klasse in Liste 2 aufgerufen werden verursachen.

**Codebeispiel 2 - Datei "HomeController.cs"**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

Programmausdruck 2 enthält die HomeController-Klasse eine Methode namens Index(), die einen einzelnen Parameter mit dem Namen Id. akzeptiert Die URL gibt bewirkt, dass die Index()-Methode, die mit einer leeren Zeichenfolge als Wert für den Id-Parameter aufgerufen werden.

Aufgrund der Art und Weise, dass das MVC-Framework Controlleraktionen aufruft entspricht die URL gibt auch die Index()-Methode der HomeController-Klasse in Programmausdruck 3.

**Codebeispiel 3 - Datei "HomeController.cs" (Index-Aktion ohne Parameter)**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

Die Methode Index() in Programmausdruck 3 akzeptiert keine Parameter. Die URL gibt, führt dazu, dass diese Index()-Methode aufgerufen werden. Die URL/Home/Index/3 ruft auch diese Methode (die Id wird ignoriert).

Die URL gibt entspricht auch die Index()-Methode der HomeController-Klasse in Listing 4.

**Programmausdruck 4 - Datei "HomeController.cs" (Index-Aktion mit NULL-Werte zulassen-Parameter)**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

In Listing 4 hat die Index()-Methode einen ganzzahligen Parameter an. Da der Parameter ein NULL-Werte zulassen-Parameter ist (es kann sich um den Wert Null haben), kann die Index() aufgerufen werden, ohne dass ein Fehler ausgelöst.

Zum Schluss Aufrufen der Methode Index() in Listing 5 mit der URL gibt führt dazu, dass eine Ausnahme aus, da der Id-Parameter *nicht* einen Parameter NULL-Werte zulässt. Wenn Sie versuchen, das Aufrufen der Methode Index() erhalten Sie den Fehler, die in Abbildung 1 angezeigt.

**Programmausdruck 5 - Datei "HomeController.cs" (Index-Aktion mit Id-Parameter)**

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]


[![Eine Controlleraktion aufgerufen wird, die einen Parameterwert erwartet](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)

**Abbildung 01**: Eine Controlleraktion, die einen Parameterwert erwartet aufrufen ([klicken Sie, um das Bild in voller Größe anzeigen](asp-net-mvc-routing-overview-cs/_static/image2.png))


Die URL/Home/Index/3, problemlos auf der anderen Seite mit die Index-Controlleraktion in Listing 5. Die Anforderung /Home/Index/3 bewirkt, dass die Index()-Methode, die mit einem Id-Parameter aufgerufen werden, die den Wert 3 hat.

## <a name="summary"></a>Zusammenfassung

Das Ziel in diesem Tutorial wurde eine kurze Einführung in das ASP.NET-Routing bereit. Wir untersucht die Standardroutingtabelle, die Sie durch eine neue ASP.NET MVC-Anwendung zu erhalten. Sie erfahren, wie die Standardroute Controlleraktionen URLs zugeordnet.

> [!div class="step-by-step"]
> [Nächste](understanding-action-filters-cs.md)
