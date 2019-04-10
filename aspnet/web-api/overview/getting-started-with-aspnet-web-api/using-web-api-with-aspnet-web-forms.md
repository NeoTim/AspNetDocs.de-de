---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Mithilfe von Web-API mit ASP.NET Web Forms - ASP.NET 4.x
author: MikeWasson
description: Tutorial mit Code Schritt für Schritt eine ASP.NET Forms-Anwendung für ASP.NET Web-API hinzugefügt 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422576"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>Verwenden der Web-API mit ASP.NET Web Forms

durch [Mike Wasson](https://github.com/MikeWasson)

Dieses Tutorial führt Sie durch die Schritte zum Hinzufügen von Web-API zu einer herkömmlichen ASP.NET Web Forms-Anwendung in ASP.NET 4.x. 

## <a name="overview"></a>Übersicht

Obwohl ASP.NET Web-API mit ASP.NET MVC gepackt wurde, ist es einfach, eine herkömmliche ASP.NET Web Forms-Anwendung-Web-API hinzugefügt.

Um Web-API in einer Web Forms-Anwendung verwenden zu können, gibt es zwei Hauptschritte:

- Fügen Sie einen Web-API-Controller, die von abgeleitet der **ApiController** Klasse.
- Fügen Sie eine Routingtabelle die **Anwendung\_starten** Methode.

## <a name="create-a-web-forms-project"></a>Erstellen einer Web Forms-Projekt

Starten Sie Visual Studio, und wählen Sie **neues Projekt** aus der **starten** Seite. Alternativ wählen Sie in der **Datei** , wählen Sie im Menü **neu** und dann **Projekt**.

In der **Vorlagen** wählen Sie im Bereich **installierte Vorlagen** und erweitern Sie die **Visual C#-** Knoten. Klicken Sie unter **Visual C#-** Option **Web**. Wählen Sie in der Liste der Projektvorlagen das Projekt **ASP.NET Web Forms-Anwendung**. Geben Sie einen Namen für das Projekt, und klicken Sie auf **OK**.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>Erstellen Sie das Modell und Controller

In diesem Tutorial verwendet die gleichen Modell und Controller-Klassen als die [Einstieg](tutorial-your-first-web-api.md) Tutorial.

Fügen Sie zunächst eine Modellklasse. In **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie **Klasse hinzufügen**. Benennen Sie die Product-Klasse, und fügen Sie die folgende Implementierung:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

Fügen Sie einen Web-API-Controller zum Projekt., ein *Controller* ist das Objekt, das HTTP-Anforderungen für Web-API behandelt.

Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt. Wählen Sie **neues Element hinzufügen**.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

Klicken Sie unter **installierte Vorlagen**, erweitern Sie **Visual C#-** , und wählen Sie **Web**. Wählen Sie dann aus der Liste der Vorlagen, **Web API Controller Class**. Nennen Sie den Controller "ProductsController", und klicken Sie auf **hinzufügen**.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

Die **neues Element hinzufügen** Assistenten wird eine Datei namens ProductsController.cs erstellt. Löschen Sie die Methoden, die der Assistent enthalten, und fügen Sie die folgenden Methoden:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

Weitere Informationen zu den Code in diesem Controller, finden Sie unter den [Einstieg](tutorial-your-first-web-api.md) Tutorial.

## <a name="add-routing-information"></a>Hinzufügen von Routinginformationen

Anschließend wir fügen eine URI-Route also diese URIs der Form &quot;/API/Produkte/&quot; an den Controller weitergeleitet werden.

In **Projektmappen-Explorer**, doppelklicken Sie auf "Global.asax", um den Code-Behind-Datei "Global.asax.cs" zu öffnen. Fügen Sie die folgenden **mit** Anweisung.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

Klicken Sie dann fügen Sie den folgenden Code der **Anwendung\_starten** Methode:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

Weitere Informationen zu Routingtabellen finden Sie unter [Routing in ASP.NET Web-API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="add-client-side-ajax"></a>Hinzufügen der clientseitigen AJAX

Das ist alles, die müssen Sie eine Web-API zu erstellen, die Clients zugreifen können. Nun fügen Sie eine HTML-Seite, die jQuery zum Aufrufen der API verwendet.

Stellen Sie sicher, dass die Masterseite (z. B. *Site.Master*) umfasst eine `ContentPlaceHolder` mit `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Öffnen Sie die Datei "default.aspx". Ersetzen Sie den Standardtext, der im Abschnitt Inhalt ist an, wie dargestellt:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

Fügen Sie einen Verweis auf die jQuery-Quelldatei in die `HeaderContent` Abschnitt:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

Hinweis: Sie können problemlos den Skriptverweis hinzufügen, durch Ziehen und Ablegen der Datei aus **Projektmappen-Explorer** in das Fenster des Code-Editor.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

Fügen Sie den nachstehenden Skriptbaustein unterhalb des jQuery-Skript-Tags hinzu:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

Wenn das Dokument geladen wird, wird dieses Skript eine AJAX-Anforderung an &quot;-api/Produkte&quot;. Die Anforderung gibt eine Liste der Produkte im JSON-Format zurück. Das Skript fügt die Produktinformationen in den HTML-Tabelle.

Wenn Sie die Anwendung ausführen, sollte es wie folgt aussehen:

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
