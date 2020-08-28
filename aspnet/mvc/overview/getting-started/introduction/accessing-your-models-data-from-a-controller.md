---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Zugreifen auf die Daten des Modells von einem Controller | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045168"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Zugreifen auf Modelldaten anhand eines Controllers

von [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

In diesem Abschnitt erstellen Sie eine neue `MoviesController` Klasse und schreiben Code, mit dem die Filmdaten abgerufen und im Browser mithilfe einer Ansichts Vorlage angezeigt werden.

**Erstellen Sie die Anwendung** , und fahren Sie mit dem nächsten Schritt fort. Wenn Sie die Anwendung nicht erstellen, erhalten Sie einen Fehler beim Hinzufügen eines Controllers.

Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf den Ordner *Controller* , und klicken Sie dann auf **Hinzufügen**und dann auf **Controller**

![](accessing-your-models-data-from-a-controller/_static/image1.png)

Klicken Sie im Dialogfeld **Gerüst hinzufügen** auf **MVC 5-Controller mit Ansichten, verwenden Sie Entity Framework**, und klicken Sie dann auf **Hinzufügen**.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Wählen Sie **Movie (mvcmovie. Models)** für die Modell Klasse aus.
- Wählen Sie für die Datenkontext Klasse die Option " **wviedbcontext (mvcmovie. Models)** " aus.
- Geben Sie für den Controller Namen den Namen **moviescontroller**ein.

  In der folgenden Abbildung wird das Dialogfeld abgeschlossen angezeigt.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

Klicken Sie auf **Hinzufügen**. (Wenn Sie eine Fehlermeldung erhalten, haben Sie die Anwendung wahrscheinlich nicht erstellt, bevor Sie mit dem Hinzufügen des Controllers begonnen haben.) Visual Studio erstellt die folgenden Dateien und Ordner:

- *Eine MoviesController.cs* -Datei im *Controller* Ordner.
- Ein Ordner " *views\movies* ".
- " *Create. cshtml", "Delete. cshtml", "Details. cshtml", "Edit. cshtml*" und " *Index. cshtml* " im neuen Ordner " *views\movies* ".

Visual Studio erstellte automatisch die [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) -Aktionsmethoden und-Sichten (Create, Read, Update und DELETE) für Sie (die automatische Erstellung von CRUD-Aktionsmethoden und-Sichten wird als Gerüstbau bezeichnet). Sie verfügen jetzt über eine voll funktionsfähige Webanwendung, mit der Sie Film Einträge erstellen, auflisten, bearbeiten und löschen können.

Führen Sie die Anwendung aus, und klicken Sie auf den Link **MVC Movie** (oder navigieren Sie zu dem `Movies` Controller, indem Sie */Movies* an die URL in der Adressleiste Ihres Browsers Anhängen). Da sich die Anwendung auf das Standard Routing bezieht (definiert in der *App \_ start\routeconfig.cs* -Datei), wird die Browser Anforderung `http://localhost:xxxxx/Movies` an die Standard `Index` Aktionsmethode des Controllers weitergeleitet `Movies` . Anders ausgedrückt: die Browser Anforderung `http://localhost:xxxxx/Movies` ist praktisch identisch mit der Browser Anforderung `http://localhost:xxxxx/Movies/Index` . Das Ergebnis ist eine leere Liste von Filmen, da Sie noch keine hinzugefügt haben.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Erstellen eines Films

Klicken Sie auf den Link **Neu erstellen**. Geben Sie einige Details zu einem Film ein, und klicken Sie dann auf die Schaltfläche **Erstellen** .

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Sie können möglicherweise keine Dezimaltrennzeichen oder Kommas in das Feld Price eingeben. Um die jQuery-Validierung für nicht englische Gebiets Schemas zu unterstützen, die ein Komma ( &quot; , &quot; ) für einen Dezimaltrennzeichen und nicht-US-englische Datumsformate verwenden, müssen Sie *globalize.js* und ihre spezifischen *Kulturen/globalize.cultures.js* Datei (von [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) und JavaScript einschließen, um zu verwenden `Globalize.parseFloat` . Im nächsten Tutorial zeige ich Ihnen, wie dies geschieht. Geben Sie einstweilen ganze Zahlen wie 10 ein.

Wenn Sie auf die Schaltfläche **Erstellen** klicken, wird das Formular an den Server gesendet, auf dem die Filminformationen in der Datenbank gespeichert werden. Sie werden dann zur URL */Movies* umgeleitet, auf der Sie den neu erstellten Film in der Auflistung sehen können.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Erstellen Sie ein paar weitere Filmeinträge. Testen Sie die Links **Edit** (Bearbeiten), **Details** und **Delete** (Löschen), die alle funktionsbereit sind.

## <a name="examining-the-generated-code"></a>Untersuchen des generierten Codes

Öffnen Sie die Datei " *controllers\moviescontroller.cs* ", und überprüfen Sie die generierte `Index` Methode. Ein Teil des Movie-Controllers mit der- `Index` Methode wird unten dargestellt.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Eine Anforderung an den `Movies` Controller gibt alle Einträge in der `Movies` Tabelle zurück und übergibt dann die Ergebnisse an die `Index` Ansicht. Die folgende Zeile der- `MoviesController` Klasse instanziiert einen Film Daten Bank Kontext, wie zuvor beschrieben. Sie können den Film Daten Bank Kontext verwenden, um Filme abzufragen, zu bearbeiten und zu löschen.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Stark typisierte Modelle und das @model Schlüsselwort

An früherer Stelle in diesem Tutorial haben Sie erfahren, wie ein Controllerdaten oder Objekte mithilfe des-Objekts an eine Ansichts Vorlage übergeben kann `ViewBag` . `ViewBag`Ist ein dynamisches Objekt, das eine bequeme spät gebundene Methode zum Übergeben von Informationen an eine Ansicht bereitstellt.

MVC bietet auch die Möglichkeit, *stark* typisierte Objekte an eine Ansichts Vorlage zu übergeben. Dieser stark typisierte Ansatz ermöglicht eine bessere Kompilierzeit Überprüfung Ihres Codes und umfangreicheres [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) im Visual Studio-Editor. Der Gerüstbau Mechanismus in Visual Studio verwendet diesen Ansatz (d. h. die Übergabe eines *stark* typisierten Modells) mit den `MoviesController` Klassen-und Ansichts Vorlagen, als die Methoden und Sichten erstellt wurden.

Untersuchen Sie in der Datei " *controllers\moviescontroller.cs* " die generierte `Details` Methode. Die- `Details` Methode wird unten dargestellt.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

Der- `id` Parameter wird im Allgemeinen als Routendaten übergeben, z `http://localhost:1234/movies/details/1` . b. wird der Controller auf den Movie-Controller, die-Aktion auf `details` und `id` auf 1 festgelegt. Außerdem können Sie die ID wie folgt mit einer Abfrage Zeichenfolge übergeben:

`http://localhost:1234/movies/details?id=1`

Wenn eine- `Movie` Instanz gefunden wird, wird eine Instanz des `Movie` Modells an die `Details` Ansicht übermittelt:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

Überprüfen Sie den Inhalt der Datei " *views\movies\details.cshtml* ":

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Durch Einschließen einer- `@model` Anweisung am Anfang der Ansichts Vorlagen Datei können Sie den Objekttyp angeben, den die Sicht erwartet. Beim Erstellen des „Movies“-Controllers hat Visual Studio automatisch die folgende `@model`-Anweisung am Anfang der Datei *Details.cshtml* hinzugefügt:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Diese `@model`-Direktive ermöglicht Ihnen den Zugriff auf den Film, den der Controller an die Ansicht übergeben hat, indem ein stark typisiertes `Model`-Objekt verwendet wir. Beispielsweise übergibt der Code in der Vorlage *Details. cshtml* jedes Movie-Feld an die `DisplayNameFor` HTML-Hilfsprogramme und [Display for](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) mit dem stark typisierten- `Model` Objekt. Die `Create` -und- `Edit` Methoden und-Ansichts Vorlagen übergeben auch ein Movie Model-Objekt.

Überprüfen Sie die Ansichts Vorlage *Index. cshtml* und die- `Index` Methode in der Datei *MoviesController.cs* . Beachten Sie, wie der Code ein-Objekt erstellt, [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) Wenn es die- `View` Hilfsmethode in der- `Index` Aktionsmethode aufruft. Der Code übergibt dann diese `Movies` Liste von der `Index` Aktionsmethode an die Ansicht:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

Beim Erstellen des Film Controllers enthielt Visual Studio automatisch die folgende `@model` Anweisung am Anfang der Datei " *Index. cshtml* ":

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Diese `@model` Direktive ermöglicht Ihnen den Zugriff auf die Liste der Filme, die der Controller an die Ansicht übermittelt hat, indem `Model` er ein stark typisiertes-Objekt verwendet. In der Vorlage *Index. cshtml* durchläuft der Code z. b. die Filme durch Ausführen einer- `foreach` Anweisung über das stark typisierte- `Model` Objekt:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

Da das- `Model` Objekt stark typisiert ist (als- `IEnumerable<Movie>` Objekt), `item` wird jedes Objekt in der Schleife als typisiert `Movie` . Dies bedeutet neben anderen Vorteilen, dass Sie die Kompilierzeit Überprüfung des Codes und die vollständige IntelliSense-Unterstützung im Code-Editor erhalten:

![Modelintellisense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>Arbeiten mit SQL Server LocalDB

Entity Framework Code First festgestellt, dass die angegebene Daten bankverbindungs Zeichenfolge auf eine Datenbank verweist, die `Movies` noch nicht vorhanden war, sodass Code First die Datenbank automatisch erstellt hat. Sie können überprüfen, ob er erstellt wurde, indem Sie im Ordner *App- \_ Daten* suchen. Wenn die Datei *Movies. mdf* nicht angezeigt wird, klicken Sie auf der **Projektmappen-Explorer** Symbolleiste auf die Schaltfläche **alle Dateien anzeigen** , klicken Sie auf die Schaltfläche **Aktualisieren** , und erweitern Sie dann den Ordner *App- \_ Daten* .

![](accessing-your-models-data-from-a-controller/_static/image9.png)

Doppelklicken Sie auf *Movies. mdf* , um den **Server-Explorer**zu öffnen, und erweitern Sie dann den Ordner **Tabellen** , um die Tabelle Movies anzuzeigen. Beachten Sie das Schlüsselsymbol neben ID. Standardmäßig wird von EF eine Eigenschaft mit dem Namen ID als Primärschlüssel erstellt. Weitere Informationen zu EF und MVC finden Sie im hervorragenden Tutorial zu Tom Dykstra in [MVC und EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Klicken Sie mit der rechten Maustaste auf die `Movies` Tabelle, und wählen Sie **Tabellendaten anzeigen** aus, um die erstellten Daten anzuzeigen.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Klicken Sie mit der rechten Maustaste auf die `Movies` Tabelle, und wählen Sie **Tabellen Definition öffnen** , um die Tabellenstruktur anzuzeigen, die Entity Framework für Sie erstellt Code First.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Beachten Sie, dass das Schema der `Movies` Tabelle der-Klasse zugeordnet ist, die `Movie` Sie zuvor erstellt haben. Entity Framework Code First dieses Schema basierend auf Ihrer Klasse automatisch für Sie erstellt `Movie` .

Wenn Sie fertig sind, schließen Sie die Verbindung, indem Sie mit der rechten Maustaste auf " *muviedbcontext* " klicken und **Verbindung schließen**auswählen (Wenn Sie die Verbindung nicht schließen, erhalten Sie möglicherweise eine Fehlermeldung, wenn Sie das Projekt das nächste Mal ausführen).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Sie verfügen jetzt über eine Datenbank und Seiten zum Anzeigen, Bearbeiten, Aktualisieren und Löschen von Dateien. Im nächsten Tutorial untersuchen wir den restlichen Code und fügen eine `SearchIndex` Methode und eine `SearchIndex` Ansicht hinzu, mit der Sie in dieser Datenbank nach Filmen suchen können. Weitere Informationen zur Verwendung von Entity Framework mit MVC finden Sie unter [Erstellen eines Entity Framework Datenmodells für eine ASP.NET MVC-Anwendung](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Zurück](creating-a-connection-string.md)
> [Weiter](examining-the-edit-methods-and-edit-view.md)
