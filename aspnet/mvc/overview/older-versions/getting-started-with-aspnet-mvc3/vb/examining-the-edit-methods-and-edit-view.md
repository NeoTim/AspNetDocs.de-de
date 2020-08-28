---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/examining-the-edit-methods-and-edit-view
title: Untersuchen der Bearbeitungsmethoden und Bearbeiten der Ansicht (VB) | Microsoft-Dokumentation
author: Rick-Anderson
description: Dieses Tutorial vermittelt Ihnen die Grundlagen der Entwicklung einer ASP.NET MVC-Webanwendung mithilfe von Microsoft Visual Web Developer 2010 Express Service Pack 1.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 5cb3c59b-1e96-464b-b3a8-c55607201872
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: fc4d59323ab3cc1e4a454676a0ec498f3c5246fd
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044596"
---
# <a name="examining-the-edit-methods-and-edit-view-vb"></a>Überprüfen der Edit-Methoden und -Ansicht (VB)

von [Rick Anderson](https://twitter.com/RickAndMSFT)

> Dieses Tutorial vermittelt Ihnen die Grundlagen der Entwicklung einer ASP.NET MVC-Webanwendung mit Microsoft Visual Web Developer 2010 Express Service Pack 1, einer kostenlosen Version von Microsoft Visual Studio. Stellen Sie sicher, dass Sie die unten aufgeführten Voraussetzungen installiert haben, bevor Sie beginnen. Sie können alle Komponenten installieren, indem Sie auf den folgenden Link klicken: [Webplattform-Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternativ können Sie die erforderlichen Komponenten einzeln mithilfe der folgenden Links installieren:
> 
> - [Erforderliche Komponenten für Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3-Tools aktualisieren](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(Laufzeit + Tool Unterstützung)
> 
> Wenn Sie Visual Studio 2010 anstelle von Visual Web Developer 2010 verwenden, installieren Sie die erforderlichen Komponenten, indem Sie auf den folgenden Link klicken: [Visual Studio 2010 Voraussetzungen](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Ein Visual Web Developer-Projekt mit VB.NET-Quellcode ist für dieses Thema verfügbar. [Laden Sie die VB.NET-Version herunter](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Wenn Sie c# bevorzugen, wechseln Sie zur [c#-Version](../cs/examining-the-edit-methods-and-edit-view.md) dieses Tutorials.

In diesem Abschnitt untersuchen Sie die generierten Aktionsmethoden und-Sichten für den Film Controller. Anschließend fügen Sie eine benutzerdefinierte Suchseite hinzu.

Führen Sie die Anwendung aus, und navigieren Sie zum `Movies` Controller, indem Sie */Movies* an die URL in der Adressleiste Ihres Browsers anhängen. Halten Sie den Mauszeiger auf einen **Bearbeitungs** Link, um die URL anzuzeigen, mit der er verknüpft ist.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

Der **Bearbeitungs** Link wurde von der- `Html.ActionLink` Methode in der *views\movies\index.vbhtml* -Sicht generiert:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image3.png)](examining-the-edit-methods-and-edit-view/_static/image2.png)

Das `Html` -Objekt ist ein Hilfsprogramm, das mithilfe einer Eigenschaft in der Basisklasse verfügbar gemacht wird `WebViewPage` . Die-Methode des-Hilfsprogramms `ActionLink` erleichtert das dynamische Generieren von HTML-Hyperlinks, die mit Aktionsmethoden auf Controllern verknüpft sind. Das erste Argument für die- `ActionLink` Methode ist der zu Rendering-Linktext (z `<a>Edit Me</a>` . b.). Das zweite Argument ist der Name der aufzurufenden Aktionsmethode. Das abschließende Argument ist ein [Anonymes Objekt](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , das die Routendaten generiert (in diesem Fall die ID 4).

Der generierte Link, der in der vorherigen Abbildung angezeigt wird, ist `http://localhost:xxxxx/Movies/Edit/4` . Die Standardroute übernimmt das URL-Muster `{controller}/{action}/{id}` . Daher übersetzt ASP.net `http://localhost:xxxxx/Movies/Edit/4` in eine Anforderung an die `Edit` Aktionsmethode des Controllers, `Movies` wobei der-Parameter `ID` gleich 4 ist.

Sie können auch Aktionsmethoden Parameter mithilfe einer Abfrage Zeichenfolge übergeben. Beispielsweise übergibt die URL `http://localhost:xxxxx/Movies/Edit?ID=4` auch den-Parameter `ID` von 4 an die `Edit` Aktionsmethode des `Movies` Controllers.

[![Editquerystring](examining-the-edit-methods-and-edit-view/_static/image5.png)](examining-the-edit-methods-and-edit-view/_static/image4.png)

Öffnen Sie den `Movies` Controller. Die zwei `Edit` Aktionsmethoden sind unten dargestellt.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample3.vb)]

Beachten Sie, dass der zweiten `Edit`-Aktionsmethode das `HttpPost`-Attribut vorangestellt ist. Dieses Attribut gibt an, dass die Überladung der- `Edit` Methode nur für Post-Anforderungen aufgerufen werden kann. Sie können das `HttpGet` -Attribut auf die erste Bearbeitungsmethode anwenden, dies ist jedoch nicht notwendig, da es sich hierbei um den Standardwert handelt. (Wir verweisen auf Aktionsmethoden, denen das `HttpGet` Attribut implizit als Methoden zugewiesen wird `HttpGet` .)

Die- `HttpGet` `Edit` Methode nimmt den Movie ID-Parameter an, sucht den Film mit der Entity Framework `Find` -Methode und gibt den ausgewählten Film an die Bearbeitungs Ansicht zurück. Als das Gerüstsystem die Bearbeitungsansicht erstellt hat, wurde die `Movie`-Klasse überprüft und Code zum Rendern der `<label>`- und `<input>`-Elemente für jede Eigenschaft der Klasse erstellt. Im folgenden Beispiel wird die Ansicht "Bearbeiten" gezeigt, die generiert wurde:

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.vbhtml)]

Beachten `@ModelType MvcMovie.Models.Movie` Sie, dass die Ansichts Vorlage eine-Anweisung am Anfang der Datei enthält – dies gibt an, dass die Sicht erwartet, dass das Modell für die Ansichts Vorlage vom Typ ist `Movie` .

Der Gerüst Code verwendet mehrere *Hilfsmethoden* , um das HTML-Markup zu optimieren. Das Hilfsprogramm [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) zeigt den Namen des Felds an ( &quot; Titel &quot; , &quot; ReleaseDate &quot; , &quot; Genre &quot; oder &quot; Preis &quot; ). Das-Hilfsprogramm [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) zeigt ein HTML-- `<input>` Element an. Das Hilfsprogramm [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) zeigt alle Validierungs Meldungen an, die dieser Eigenschaft zugeordnet sind.

Führen Sie die Anwendung aus, und navigieren Sie zur URL */Movies* . Klicken Sie auf einen Link **Bearbeiten**. Zeigen Sie im Browser den Quelltext für die Seite an. Der HTML-Code auf der Seite sieht wie im folgenden Beispiel aus. (Das Menü Markup wurde aus Gründen der Übersichtlichkeit ausgeschlossen.)

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html)]

Die- `<input>` Elemente befinden sich in einem HTML-- `<form>` Element, dessen-Attribut für `action` die Post-Bereitstellung an die URL */Movies/Edit* Die Formulardaten werden an den Server gesendet, wenn auf die Schaltfläche **Bearbeiten** geklickt wird.

## <a name="processing-the-post-request"></a>Verarbeiten der POST-Anforderung

Die folgende Liste zeigt die `HttpPost`-Version der `Edit`-Aktionsmethode.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample6.vb)]

Der ASP.NET Framework-Modell Binder nimmt die übermittelten Formular Werte an und erstellt ein `Movie` -Objekt, das als-Parameter übergeben wird `movie` . Durch die `ModelState.IsValid` Überprüfung des Codes wird überprüft, ob die Daten, die im Formular übermittelt werden, zum Ändern eines-Objekts verwendet werden können `Movie` . Wenn die Daten gültig sind, speichert der Code die Filmdaten in der-Auflistung `Movies` der- `MovieDBContext` Instanz. Der Code speichert dann die neuen Filmdaten in der Datenbank, indem die- `SaveChanges` Methode von aufgerufen `MovieDBContext` wird, die Änderungen an der Datenbank beibehält. Nach dem Speichern der Daten leitet der Code den Benutzer an die `Index` Aktionsmethode der- `MoviesController` Klasse um, die bewirkt, dass der aktualisierte Film in der Auflistung der Filme angezeigt wird.

Wenn die bereitgestellte Werte nicht gültig sind, werden Sie erneut im Formular angezeigt. Die Hilfsprogramme `Html.ValidationMessageFor` in der Ansicht " *Edit. vbhtml* " zeigen die entsprechenden Fehlermeldungen an.

[![abcnotvalid](examining-the-edit-methods-and-edit-view/_static/image7.png)](examining-the-edit-methods-and-edit-view/_static/image6.png)

> **Hinweis zu** Gebiets Schemas Wenn Sie normalerweise mit einem anderen Gebiets Schema als Englisch arbeiten, finden Sie weitere Informationen [unter unterstützende ASP.NET MVC 3-Validierung mit nicht englischen](https://msdn.microsoft.com/library/gg674880(VS.98).aspx) Gebiets Schemas.

## <a name="making-the-edit-method-more-robust"></a>Robuster gestalten der Bearbeitungsmethode

Die `HttpGet` `Edit` vom Gerüstbau systemgenerierte Methode prüft nicht, ob die an Sie übergebenen ID gültig ist. Wenn ein Benutzer das ID-Segment aus der URL ( `http://localhost:xxxxx/Movies/Edit` ) entfernt, wird der folgende Fehler angezeigt:

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image9.png)](examining-the-edit-methods-and-edit-view/_static/image8.png)

Ein Benutzer könnte auch eine ID übergeben, die nicht in der Datenbank vorhanden ist, z `http://localhost:xxxxx/Movies/Edit/1234` . b.. Sie können zwei Änderungen an der- `HttpGet` `Edit` Aktionsmethode vornehmen, um diese Einschränkung zu beheben. Ändern Sie zunächst den-Parameter so, dass er den `ID` Standardwert 0 (null) aufweist, wenn eine ID nicht explizit übergeben wird. Sie können auch überprüfen, ob die `Find` Methode tatsächlich einen Film gefunden hat, bevor Sie das Movie-Objekt an die Ansichts Vorlage zurückgeben. Die aktualisierte `Edit` Methode ist unten dargestellt.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample7.vb)]

Wenn kein Film gefunden wird, wird die- `HttpNotFound` Methode aufgerufen.

Alle- `HttpGet` Methoden folgen einem ähnlichen Muster. Sie erhalten ein Movie-Objekt (oder eine Liste von Objekten im Fall von `Index` ) und übergeben das Modell an die Ansicht. Die- `Create` Methode übergibt ein leeres Movie-Objekt an die CREATE-Sicht. Alle Methoden, die Daten erstellen, bearbeiten, löschen oder in beliebiger Weise ändern, nutzen dazu die `HttpPost`-Überladung der Methode. Das Ändern von Daten in einer HTTP Get-Methode stellt ein Sicherheitsrisiko dar, wie im Blogbeitrag Entry [ASP.NET MVC Tip #46 – use Delete Links (Erstellen von Sicherheitslücken](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)). Das Ändern von Daten in einer Get-Methode verstößt auch gegen bewährte HTTP-Methoden und das architektonische Rest-Muster, das angibt, dass Get-Anforderungen den Zustand der Anwendung nicht ändern sollten. Anders ausgedrückt: das Ausführen eines Get-Vorgangs sollte ein sicherer Vorgang sein, der keine Nebeneffekte hat.

## <a name="adding-a-search-method-and-search-view"></a>Hinzufügen einer Suchmethode und einer Such Ansicht

In diesem Abschnitt fügen Sie eine `SearchIndex` Aktionsmethode hinzu, mit der Sie Filme nach Genre oder Name durchsuchen können. Dies wird mithilfe der */Movies/SearchIndex* -URL zur Verfügung gestellt. In der Anforderung wird ein HTML-Formular angezeigt, das Eingabeelemente enthält, die ein Benutzer ausfüllen kann, um nach einem Film zu suchen. Wenn ein Benutzer das Formular sendet, erhält die Aktionsmethode die vom Benutzer gesendeten Suchwerte und verwendet die Werte, um die Datenbank zu durchsuchen.

![SearchIndx_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

## <a name="displaying-the-searchindex-form"></a>Anzeigen des SearchIndex-Formulars

Beginnen `SearchIndex` Sie, indem Sie der vorhandenen Klasse eine Aktionsmethode hinzufügen `MoviesController` . Die-Methode gibt eine Ansicht zurück, die ein HTML-Formular enthält. Der Code lautet wie folgt:

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample8.vb)]

In der ersten Zeile der- `SearchIndex` Methode wird die folgende [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) -Abfrage erstellt, um die Filme auszuwählen:

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample9.vb)]

Die Abfrage wird an dieser Stelle definiert, aber noch nicht für den Datenspeicher ausgeführt.

Wenn der- `searchString` Parameter eine Zeichenfolge enthält, wird die Film Abfrage so geändert, dass nach dem Wert der Such Zeichenfolge gefiltert wird, indem der folgende Code verwendet wird:

Wenn nicht String. IsNullOrEmpty (searchString), dann   
 Filme = Filme. Where (Function (s) s. Title. enthält (searchString))   
 Beenden, wenn

LINQ-Abfragen werden nicht ausgeführt, wenn Sie definiert oder durch Aufrufen einer Methode wie oder geändert werden `Where` `OrderBy` . Stattdessen wird die Abfrage Ausführung verzögert. Dies bedeutet, dass die Auswertung eines Ausdrucks verzögert wird, bis der erkannte Wert tatsächlich durchlaufen oder die- [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) Methode aufgerufen wird. Im `SearchIndex` Beispiel wird die Abfrage in der SearchIndex-Sicht ausgeführt. Weitere Informationen zur verzögerten Abfrageausführung finden Sie unter [Abfrageausführung](https://msdn.microsoft.com/library/bb738633.aspx).

Nun können Sie die `SearchIndex` Ansicht implementieren, in der das Formular für den Benutzer angezeigt wird. Klicken Sie mit der rechten Maustaste in die `SearchIndex` Methode, und klicken Sie dann auf **Ansicht hinzufügen** Geben Sie im Dialogfeld **Ansicht hinzufügen** an, dass Sie ein- `Movie` Objekt an die Ansichts Vorlage als Modell Klasse übergeben. Wählen Sie in der Liste **Gerüst Vorlage** die Option **Liste**aus, und klicken Sie dann auf **Hinzufügen**.

[![Addsearchview](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

Wenn Sie auf die Schaltfläche **Hinzufügen** klicken, wird die Ansichts Vorlage *views\movies\searchindex.vbhtml* erstellt. Da Sie **Liste** in der Liste **Gerüstbau Vorlage** ausgewählt haben, generiert Visual Web Developer automatisch einige Standard Inhalte in der Ansicht. Der Gerüstbau hat ein HTML-Formular erstellt. Die `Movie` Klasse wurde untersucht und Code erstellt, um `<label>` Elemente für jede Eigenschaft der Klasse zu erzeugen. In der folgenden Liste wird die erstellte Create View angezeigt:

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.vbhtml)]

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/SearchIndex*. Fügen Sie eine Abfragezeichenfolge wie `?searchString=ghost` an die URL an. Die gefilterten Filme werden angezeigt.

[![Searchqrystr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

Wenn Sie die Signatur der `SearchIndex` Methode so ändern, dass Sie einen Parameter mit dem Namen hat `id` , `id` entspricht der Parameter dem `{id}` Platzhalter für die Standardrouten, die in der Datei *Global. asax* festgelegt sind.

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

Die geänderte `SearchIndex` Methode sieht wie folgt aus:

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample12.vb)]

Sie können nun den Suchtitel als Routendaten (ein URL-Segment) anstatt als Wert einer Abfragezeichenfolge übergeben.

[![Searchroutedata](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

Sie können jedoch von den Benutzern nicht erwarten, dass sie jedes Mal die URL ändern, wenn sie nach einem Film suchen möchten. Nun fügen Sie die Benutzeroberfläche hinzu, um Sie beim Filtern von Filmen zu unterstützen. Wenn Sie die Signatur der- `SearchIndex` Methode geändert haben, um zu testen, wie der Routen gebundene ID-Parameter übergeben wird, ändern Sie ihn so, dass die- `SearchIndex` Methode einen Zeichen folgen Parameter namens annimmt `searchString` :

Öffnen Sie die Datei " *views\movies\searchindex.vbhtml* ", und `@Html.ActionLink("Create New", "Create")` fügen Sie direkt nach Folgendes hinzu:

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample13.vbhtml)]

Das-Hilfsprogramm `Html.BeginForm` erstellt ein öffnendes- `<form>` Tag. Das Hilfsprogramm bewirkt, dass `Html.BeginForm` das Formular in sich selbst gepostet wird, wenn der Benutzer das Formular durch Klicken auf die Schaltfläche **Filter** übermittelt.

Führen Sie die Anwendung aus, und suchen Sie nach einem Film.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

Es gibt keine Überladung der- `HttpPost` `SearchIndex` Methode. Sie benötigen Sie nicht, da die Methode den Zustand der Anwendung nicht ändert, sondern nur das Filtern von Daten. Wenn Sie die folgende Methode hinzugefügt `HttpPost` `SearchIndex` haben, entspricht der Aktions Aufruf der `HttpPost` `SearchIndex` -Methode, und die- `HttpPost` `SearchIndex` Methode würde wie in der folgenden Abbildung dargestellt ausgeführt werden.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample14.vb)]

[![Searchpostghost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

## <a name="adding-search-by-genre"></a>Hinzufügen der Suche nach Genre

Wenn Sie die `HttpPost` Version der-Methode hinzugefügt `SearchIndex` haben, löschen Sie Sie jetzt.

Als Nächstes fügen Sie eine Funktion hinzu, um Benutzern das Suchen nach Filmen nach Genre zu ermöglichen. Ersetzen Sie die `SearchIndex`-Methode durch den folgenden Code:

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample15.vb)]

Diese Version der- `SearchIndex` Methode nimmt einen zusätzlichen Parameter, nämlich, auf `movieGenre` . In den ersten Codezeilen wird ein- `List` Objekt erstellt, um Movie-Genres aus der Datenbank zu speichern.

Der folgende Code ist eine LINQ-Abfrage, die alle Genres aus der Datenbank abruft.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample16.vb)]

Der Code verwendet die- `AddRange` Methode der generischen- `List` Auflistung, um alle eindeutigen Genres der Liste hinzuzufügen. (Ohne den- `Distinct` Modifizierer würden doppelte Genres hinzugefügt werden – beispielsweise würde die-Komödie in unserem Beispiel zweimal hinzugefügt werden.) Der Code speichert dann die Liste der Genres im- `ViewBag` Objekt.

Der folgende Code zeigt, wie Sie den-Parameter überprüfen `movieGenre` . Wenn Sie nicht leer ist, schränkt der Code die Film Abfrage weiter ein, um die ausgewählten Filme auf das angegebene Genre zu beschränken.

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample17.vb)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Hinzufügen von Markup zur Ansicht "SearchIndex" zur Unterstützung der Suche nach Genre

Fügen Sie `Html.DropDownList` der Datei " *views\movies\searchindex.vbhtml* " direkt vor dem Hilfsprogramm ein Hilfsobjekt hinzu `TextBox` . Das vollständige Markup ist unten dargestellt:

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.vbhtml)]

Führen Sie die Anwendung aus, und navigieren Sie zu */Movies/SearchIndex*. Probieren Sie eine Suche nach Genre, nach Film Name und nach beiden Kriterien aus.

In diesem Abschnitt haben Sie die vom Framework generierten CRUD-Aktionsmethoden und-Sichten untersucht. Sie haben eine Such Aktionsmethode und-Ansicht erstellt, mit der Benutzer nach Film Titel und Genre suchen können. Im nächsten Abschnitt erfahren Sie, wie Sie dem Modell eine Eigenschaft hinzufügen `Movie` und wie Sie einen Initialisierer hinzufügen, mit dem automatisch eine Testdatenbank erstellt wird.

> [!div class="step-by-step"]
> [Zurück](accessing-your-models-data-from-a-controller.md)
> [Weiter](adding-a-new-field.md)
