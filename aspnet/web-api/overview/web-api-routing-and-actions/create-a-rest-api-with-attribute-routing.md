---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Erstellen einer Rest-API mit Attribut Routing in ASP.net-Web-API 2 | Microsoft-Dokumentation
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188851"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>Erstellen einer Rest-API mit Attribut Routing in ASP.net-Web-API 2

von [Mike Wasson](https://github.com/MikeWasson)

Web-API 2 unterstützt eine neue Art von Routing namens *Attribut Routing*. Eine allgemeine Übersicht über das Attribut Routing finden Sie unter [Attribut Routing in der Web-API 2](attribute-routing-in-web-api-2.md). In diesem Tutorial verwenden Sie das Attribut Routing zum Erstellen einer Rest-API für eine Sammlung von Büchern. Die API unterstützt die folgenden Aktionen:

| Aktion | Beispiel-URI |
| --- | --- |
| Hier finden Sie eine Liste aller Bücher. | /api/books |
| Sie erhalten ein Buch anhand der ID. | /api/books/1 |
| Hier finden Sie die Details eines Buchs. | /api/books/1/details |
| Eine Liste der Bücher nach Genre erhalten. | /api/books/fantasy |
| Eine Liste der Bücher nach Veröffentlichungsdatum erhalten. | /API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (alternative Form) |
| Eine Liste der Bücher von einem bestimmten Autor erhalten. | /api/authors/1/books |

Alle Methoden sind schreibgeschützt (HTTP GET-Anforderungen).

Für die Datenebene verwenden wir Entity Framework. Buch Datensätze verfügen über die folgenden Felder:

- ID
- Titel
- Genre
- Veröffentlichungsdatum
- Preis
- Beschreibung
- AutorID (Fremdschlüssel für eine Autoren Tabelle)

Bei den meisten Anforderungen gibt die API jedoch eine Teilmenge dieser Daten zurück (Titel, Autor und Genre). Um den gesamten Datensatz zu erhalten, fordert der Client an `/api/books/{id}/details` .

## <a name="prerequisites"></a>Voraussetzungen

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional oder Enterprise Edition.

## <a name="create-the-visual-studio-project"></a>Erstellen des Visual Studio-Projekts

Führen Sie zuerst Visual Studio 2013 aus. Wählen Sie im Menü **Datei** die Option **neu** aus, und wählen Sie dann **Projekt**aus.

Erweitern Sie die **installierte**  >  **Visual c#** -Kategorie. Wählen Sie unter **Visual c#** die Option **Web**aus. Wählen Sie in der Liste der Projektvorlagen die Option **ASP.NET Webanwendung (.NET Framework)** aus. Nennen Sie das Projekt &quot; booksapi &quot; .

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

Wählen Sie im Dialogfeld **New ASP.NET Webanwendung** die Vorlage **leere** Vorlage aus. Aktivieren Sie unter "Ordner und Kern Verweise hinzufügen" das Kontrollkästchen **Web-API** . Klicken Sie auf **OK**.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

Dadurch wird ein Skeleton-Projekt erstellt, das für die Web-API-Funktionalität konfiguriert ist.

### <a name="domain-models"></a>Domänen Modelle

Fügen Sie als nächstes Klassen für Domänen Modelle hinzu. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner „Modelle“. Wählen Sie **Hinzufügen**und dann **Klasse**aus. Geben Sie der Klassen den Namen `Author`.

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Ersetzen Sie den Code in Author.cs durch Folgendes:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

Fügen Sie jetzt eine weitere Klasse namens hinzu `Book` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Hinzufügen eines Web-API-Controllers

In diesem Schritt fügen wir einen Web-API-Controller hinzu, der Entity Framework als Datenschicht verwendet.

Drücken Sie STRG+UMSCHALT+B, um das Projekt zu erstellen. Entity Framework verwendet Reflektion, um die Eigenschaften der Modelle zu ermitteln. Daher ist eine kompilierte Assembly erforderlich, um das Datenbankschema zu erstellen.

Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner „Controller“. Wählen Sie **Hinzufügen**und dann **Controller**aus.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

Wählen Sie im Dialogfeld **Gerüst hinzufügen** die Option **Web-API 2-Controller mit Aktionen aus, indem Sie Entity Framework verwenden**.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

Geben Sie im Dialogfeld **Controller hinzufügen** für **Controller Name den Namen** &quot; bookscontroller ein &quot; . Aktivieren Sie das &quot; Kontrollkästchen Async Controller-Aktionen verwenden &quot; . Wählen Sie für **Modell Klasse**die Option &quot; Buch aus &quot; . (Wenn die `Book` in der Dropdown Liste aufgeführte Klasse nicht angezeigt wird, stellen Sie sicher, dass Sie das Projekt erstellt haben.) Klicken Sie dann auf die Schaltfläche "+".

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

Klicken Sie im Dialogfeld **neuer Datenkontext** auf **Hinzufügen** .

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

Klicken Sie im Dialogfeld **Controller hinzufügen** auf **Hinzufügen** . Das Gerüst fügt eine Klasse mit dem Namen hinzu `BooksController` , die den API-Controller definiert. Außerdem wird im Ordner Models eine Klasse namens hinzugefügt `BooksAPIContext` , die den Datenkontext für Entity Framework definiert.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>Durchführen eines Datenbankseedings

Klicken Sie im Menü Extras auf **nuget-Paket-Manager**, und wählen Sie dann **Paket-Manager-Konsole**aus.

Geben Sie im Fenster Paket-Manager-Konsole den folgenden Befehl ein:

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

Mit diesem Befehl wird ein Migrations Ordner erstellt und eine neue Codedatei mit dem Namen Configuration.cs hinzugefügt. Öffnen Sie diese Datei, und fügen Sie der-Methode den folgenden Code hinzu `Configuration.Seed` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

Geben Sie im Fenster der Paket-Manager-Konsole die folgenden Befehle ein.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

Diese Befehle erstellen eine lokale Datenbank und rufen die Seed-Methode auf, um die Datenbank aufzufüllen.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>Dto-Klassen hinzufügen

Wenn Sie die Anwendung jetzt ausführen und eine GET-Anforderung an/API/Books/1 senden, sieht die Antwort in etwa wie folgt aus. (Ich habe zur besseren Lesbarkeit einen Einzug hinzugefügt.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

Stattdessen möchte ich, dass diese Anforderung eine Teilmenge der Felder zurückgibt. Außerdem möchte ich, dass Sie den Namen des Autors anstelle der Autoren-ID zurückgibt. Um dies zu erreichen, ändern wir die Controller Methoden so, dass ein *Datenübertragungs Objekt (Data Transfer Object* , dto) anstelle des EF-Modells zurückgegeben wird. Ein DTO ist ein Objekt, das nur zum Übertragen von Daten vorgesehen ist.

Klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das **Add**Projekt, und wählen Sie  |  **neuen Ordner**hinzufügen. Benennen Sie den Ordner &quot; DTOs &quot; . Fügen Sie `BookDto` dem Ordner DTOs eine Klasse mit dem Namen mit der folgenden Definition hinzu:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

Fügen Sie eine weitere Klasse namens `BookDetailDto`hinzu.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

Aktualisieren Sie anschließend die- `BooksController` Klasse, um-Instanzen zurückzugeben `BookDto` . Wir verwenden die abfragbare [. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) -Methode, um `Book` Instanzen in Instanzen zu projizieren `BookDto` . Im folgenden finden Sie den aktualisierten Code für die Controller-Klasse.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> Ich habe die `PutBook` `PostBook` Methoden, und gelöscht `DeleteBook` , da Sie für dieses Tutorial nicht benötigt werden.

Wenn Sie nun die Anwendung ausführen und/API/Books/1 anfordern, sollte der Antworttext wie folgt aussehen:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>Routen Attribute hinzufügen

Als nächstes konvertieren wir den Controller, um Attribut Routing zu verwenden. Fügen Sie zunächst dem Controller ein **routeprefix** -Attribut hinzu. Dieses Attribut definiert die anfänglichen URI-Segmente für alle Methoden auf diesem Controller.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

Fügen Sie dann wie folgt **[Route]** -Attribute zu den Controller Aktionen hinzu:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

Die Routen Vorlage für jede Controller Methode ist das Präfix und die im **Routen** Attribut angegebene Zeichenfolge. Bei der- `GetBook` Methode enthält die Routen Vorlage die parametrisierte Zeichenfolge &quot; {ID: int} &quot; , die entspricht, wenn das URI-Segment einen ganzzahligen Wert enthält.

| Methode | Routenvorlage | Beispiel-URI |
| --- | --- | --- |
| `GetBooks` | "API/Bücher" | `http://localhost/api/books` |
| `GetBook` | "API/Books/{ID: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>Buch Details anzeigen

Um Buch Details zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/{id}/details` , wobei *{ID}* die ID des Buchs ist.

Fügen Sie der `BooksController`-Klasse die folgende Methode hinzu.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

Wenn Sie anfordern `/api/books/1/details` , sieht die Antwort wie folgt aus:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>Bücher nach Genre erhalten

Um eine Liste der Bücher in einem bestimmten Genre zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/genre` , wobei *Genre* der Name des Genres ist. (Beispiel: `/api/books/fantasy`.)

Fügen Sie die folgende Methode hinzu `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

Hier definieren wir eine Route, die einen {Genre}-Parameter in der URI-Vorlage enthält. Beachten Sie, dass die Web-API diese beiden URIs unterscheiden und an verschiedene Methoden weiterleiten kann:

`/api/books/1`

`/api/books/fantasy`

Dies liegt daran, dass die- `GetBook` Methode eine Einschränkung enthält, dass das "ID"-Segment ein ganzzahliger Wert sein muss:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

Wenn Sie/API/Books/Fantasy anfordern, sieht die Antwort wie folgt aus:

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>Bücher von Autor erhalten

Um eine Liste der Bücher für einen bestimmten Autor zu erhalten, sendet der Client eine GET-Anforderung an `/api/authors/id/books` , wobei *ID* die ID des Autors ist.

Fügen Sie die folgende Methode hinzu `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

Dieses Beispiel ist interessant, da &quot; Bücher &quot; als untergeordnete Ressource von &quot; Autoren behandelt werden &quot; . Dieses Muster ist in den Rest-APIs sehr üblich.

Die Tilde (~) in der Routen Vorlage überschreibt das Routen Präfix im **routeprefix** -Attribut.

## <a name="get-books-by-publication-date"></a>Bücher nach Veröffentlichungsdatum erhalten

Um eine Liste der Bücher nach Veröffentlichungsdatum zu erhalten, sendet der Client eine GET-Anforderung an `/api/books/date/yyyy-mm-dd` , wobei *yyyy-mm-dd* das Datum ist.

Dies ist eine Möglichkeit, dies zu erreichen:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

Der- `{pubdate:datetime}` Parameter ist auf einen **DateTime** -Wert beschränkt. Dies funktioniert, aber es ist besser, als wir wollen. Beispielsweise entsprechen diese URIs auch der Route:

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

Es gibt nichts falsches, wenn diese URIs zugelassen werden. Allerdings können Sie die Route auf ein bestimmtes Format beschränken, indem Sie der Routen Vorlage eine Einschränkung für reguläre Ausdrücke hinzufügen:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

Nun stimmen nur die Datumsangaben im Format &quot; yyyy-mm-dd ab &quot; . Beachten Sie, dass wir den Regex nicht verwenden, um zu überprüfen, ob wir ein echtes Datum erhalten haben. Dies wird behandelt, wenn die Web-API versucht, das URI-Segment in eine **DateTime** -Instanz zu konvertieren. Ein ungültiges Datum, wie z. b. "2012-47-99", kann nicht konvertiert werden, und der Client erhält einen 404-Fehler.

Sie können auch ein Schrägstrich ( `/api/books/date/yyyy/mm/dd` ) durch Hinzufügen eines weiteren **[Route]** -Attributs mit einem anderen Regex unterstützen.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

Hier finden Sie ein sehr feines, aber wichtiges Detail. Die zweite Routen Vorlage enthält ein Platzhalter Zeichen ( \* ) am Anfang des {pubDate}-Parameters:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

Dadurch wird der Routing-Engine mitgeteilt, dass {pubDate} dem Rest des URIs entsprechen soll. Standardmäßig entspricht ein Vorlagen Parameter einem einzelnen URI-Segment. In diesem Fall möchten wir, dass {pubDate} mehrere URI-Segmente umfasst:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>Controller Code

Im folgenden finden Sie den gesamten Code für die bookscontroller-Klasse.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>Zusammenfassung

Das Attribut Routing bietet Ihnen mehr Kontrolle und größere Flexibilität beim Entwerfen der URIs für Ihre API.
