---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Routing in ASP.NET Web-API | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675754"
---
# <a name="routing-in-aspnet-web-api"></a>Routing in der ASP.NET Web-API

von [Mike Wasson](https://github.com/MikeWasson)

In diesem Artikel wird beschrieben, wie ASP.NET Web-API HTTP-Anforderungen an Controller weiterleitet.

> [!NOTE]
> Wenn Sie mit ASP.NET MVC vertraut sind, ähnelt das Web-API-Routing dem MVC-Routing sehr. Der Hauptunterschied besteht darin, dass die Web-API das HTTP-Verb und nicht den URI-Pfad verwendet, um die Aktion auszuwählen. Sie können auch Dasrouting im MVC-Stil in der Web-API verwenden. Dieser Artikel geht nicht von Kenntnissen ASP.NET MVC aus.

## <a name="routing-tables"></a>Routingtabellen

In ASP.NET Web-API ist ein *Controller* eine Klasse, die HTTP-Anforderungen verarbeitet. Die öffentlichen Methoden des Controllers werden *als Aktionsmethoden* oder einfach *als Aktionen*bezeichnet. Wenn das Web-API-Framework eine Anforderung empfängt, leitet es die Anforderung an eine Aktion weiter.

Um zu bestimmen, welche Aktion aufgerufen werden soll, verwendet das Framework eine *Routingtabelle*. Die Visual Studio-Projektvorlage für Web-API erstellt eine Standardroute:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Diese Route wird in der *WebApiConfig.cs-Datei* definiert, die im *\_App-Start-Verzeichnis* abgelegt wird:

![](routing-in-aspnet-web-api/_static/image1.png)

Weitere Informationen zur `WebApiConfig` Klasse finden Sie unter [Konfigurieren ASP.NET Web-API](../advanced/configuring-aspnet-web-api.md).

Wenn Sie die Web-API selbst hosten, müssen `HttpSelfHostConfiguration` Sie die Routingtabelle direkt für das Objekt festlegen. Weitere Informationen finden Sie unter [Self-Host a Web API](../older-versions/self-host-a-web-api.md).

Jeder Eintrag in der Routingtabelle enthält eine *Routenvorlage*. Die Standardroutenvorlage für &quot;die Web-API ist api/-controller.&quot; In dieser &quot;Vorlage&quot; ist api ein literales Pfadsegment, und die Platzhaltervariablen "controller" und "id" sind Platzhaltervariablen.

Wenn das Web-API-Framework eine HTTP-Anforderung empfängt, versucht es, den URI mit einer der Routenvorlagen in der Routingtabelle abzugleichen. Wenn keine Route übereinstimmt, erhält der Client einen 404-Fehler. Die folgenden URIs entsprechen beispielsweise der Standardroute:

- /api/kontakte
- /api/kontakte/1
- /api/produkte/gizmo1

Der folgende URI stimmt jedoch nicht überein, da ihm das &quot;API-Segment&quot; fehlt:

- /Kontakte/1

> [!NOTE]
> Der Grund für die Verwendung von "api" in der Route ist, Kollisionen mit ASP.NET MVC-Routing zu vermeiden. Auf diese Weise &quot;können&quot; Sie /contacts zu einem &quot;MVC-Controller und /api/contacts&quot; zu einem Web-API-Controller aufrufen. Wenn Ihnen diese Konvention nicht gefällt, können Sie natürlich die Standardroutentabelle ändern.

Sobald eine übereinstimmende Route gefunden wurde, wählt die Web-API den Controller und die Aktion aus:

- Um den Controller zu &quot;finden, fügt die Web-API Controller&quot; zum Wert der Variable *"Controller"* hinzu.
- Um die Aktion zu finden, sucht web API das HTTP-Verb und sucht dann nach einer Aktion, deren Name mit diesem HTTP-Verbnamen beginnt. Bei einer GET-Anforderung sucht die Web-API beispielsweise &quot;&quot;nach einer &quot;Aktion&quot; &quot;mit dem&quot;Präfix Get , z. B. GetContact oder GetAllContacts . Diese Konvention gilt nur für GET-, POST-, PUT-, DELETE-, HEAD-, OPTIONS- und PATCH-Verben. Sie können andere HTTP-Verben aktivieren, indem Sie Attribute auf dem Controller verwenden. Ein Beispiel dafür werden wir später sehen.
- Andere Platzhaltervariablen in der Routenvorlage, wie z. B. *die Option "id",* werden Aktionsparametern zugeordnet.

Schauen wir uns ein Beispiel an. Angenommen, Sie definieren den folgenden Controller:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Hier sind einige mögliche HTTP-Anforderungen, zusammen mit der Aktion, die für jede aufgerufen wird:

| HTTP-Verb | URI-Pfad | Aktion | Parameter |
| --- | --- | --- | --- |
| GET | api/Produkte | GetAllProdukte | *(keine)* |
| GET | api/produkte/4 | GetProductById | 4 |
| Delete | api/produkte/4 | DeleteProduct | 4 |
| POST | api/Produkte | *(keine Übereinstimmung)* |  |

Beachten Sie, dass das Segment *"id"* des URI, falls vorhanden, dem *ID-Parameter* der Aktion zugeordnet ist. In diesem Beispiel definiert der Controller zwei GET-Methoden, eine mit einem *id-Parameter* und eine ohne Parameter.

Beachten Sie außerdem, dass die POST-Anforderung fehlschlägt, da der Controller keine &quot;Post... &quot; Methode.

## <a name="routing-variations"></a>Routing-Variationen

Im vorherigen Abschnitt wurde der grundlegende Routingmechanismus für ASP.NET Web-API beschrieben. In diesem Abschnitt werden einige Variationen beschrieben.

### <a name="http-verbs"></a>HTTP-Verben

Anstatt die Namenskonvention für HTTP-Verben zu verwenden, können Sie explizit das HTTP-Verb für eine Aktion angeben, indem Sie die Aktionsmethode mit einem der folgenden Attribute dekorieren:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

Im folgenden Beispiel `FindProduct` wird die Methode GET-Anforderungen zugeordnet:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Um mehrere HTTP-Verben für eine Aktion zuzulassen oder HTTP-Verben außer GET, PUT, POST, `[AcceptVerbs]` DELETE, HEAD, OPTIONS und PATCH zuzulassen, verwenden Sie das Attribut, das eine Liste von HTTP-Verben enthält.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Routing nach Aktionsname

Bei der Standardroutingvorlage verwendet Web API das HTTP-Verb, um die Aktion auszuwählen. Sie können jedoch auch eine Route erstellen, in der der Aktionsname im URI enthalten ist:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

In dieser Routenvorlage benennt der Parameter *"Aktion"* die Aktionsmethode auf dem Controller. Verwenden Sie bei diesem Routingstil Attribute, um die zulässigen HTTP-Verben anzugeben. Angenommen, Ihr Controller verfügt über die folgende Methode:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

In diesem Fall würde eine GET-Anforderung für "api/products/details/1" der `Details` Methode zugeordnet. Dieser Routingstil ähnelt ASP.NET MVC und eignet sich möglicherweise für eine RPC-API.

Sie können den Aktionsnamen überschreiben, indem Sie das `[ActionName]` Attribut verwenden. Im folgenden Beispiel gibt es zwei &quot;Aktionen, die api/products/thumbnail/*id*zugeordnet werden. Die eine unterstützt GET und die andere post:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Nicht-Aktionen

Um zu verhindern, dass eine Methode als `[NonAction]` Aktion aufgerufen wird, verwenden Sie das Attribut. Dies signalisiert dem Framework, dass die Methode keine Aktion ist, auch wenn sie andernfalls den Routingregeln entsprechen würde.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Weitere nützliche Informationen

Dieses Thema bot eine ansichtsebene Ansicht des Routings. Weitere Informationen finden Sie unter [Routing und Aktionsauswahl](routing-and-action-selection.md), in dem genau beschrieben wird, wie das Framework einen URI mit einer Route abgleicht, einen Controller auswählt und dann die zu aufrufende Aktion auswählt.
