---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: Einführung ASP.NET Webseiten - HTML Form Basics | Microsoft Docs
author: Rick-Anderson
description: In diesem Tutorial werden die Grundlagen zum Erstellen eines Eingabeformulars und zum Behandeln der Benutzereingaben bei verwendungsASP.NET Webseiten (Razor) erläutert. Und jetzt, da Sie...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675922"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Einführung in ASP.NET Webseiten - HTML Form Basics

 von [Tom FitzMacken](https://github.com/tfitzmac)

> In diesem Tutorial werden die Grundlagen zum Erstellen eines Eingabeformulars und zum Behandeln der Benutzereingaben bei verwendungsASP.NET Webseiten (Razor) erläutert. Und jetzt, da Sie über eine Datenbank verfügen, verwenden Sie Ihre Formularkenntnisse, damit Benutzer bestimmte Filme in der Datenbank finden können. Es wird davon ausgegangen, dass Sie die Reihe durch [Einführung in die Anzeige von Daten mit ASP.NET Webseiten](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)abgeschlossen haben.
> 
> Sie lernen Folgendes:
> 
> - Erstellen eines Formulars mithilfe von Standard-HTML-Elementen.
> - So lesen Sie die Eingabe des Benutzers in einem Formular.
> - Erstellen einer SQL-Abfrage, die mithilfe eines vom Benutzer bereitstellten Suchbegriffs selektiv Daten abruft.
> - Wie man Felder auf der Seite "Erinnern" hat, was der Benutzer eingegeben hat.
>   
> 
> Diskutierte Features/Technologien:
> 
> - Das `Request`-Objekt.
> - Die `Where` SQL-Klausel.

## <a name="what-youll-build"></a>Sie lernen Folgendes

Im vorherigen Lernprogramm haben Sie eine Datenbank erstellt, ihr `WebGrid` Daten hinzugefügt und dann den Helfer zum Anzeigen der Daten verwendet. In diesem Tutorial fügen Sie ein Suchfeld hinzu, in dem Sie Filme eines bestimmten Genres suchen können oder deren Titel das eingegebene Wort enthält. (Sie können z. B. alle Filme finden, deren Genre "Action" lautet oder deren Titel "Harry" oder "Abenteuer" enthält.)

Wenn Sie mit diesem Tutorial fertig sind, haben Sie eine Seite wie diese:

![Filmseite mit Genre- und Titelsuche](form-basics/_static/image1.png)

Der Auflistungsteil der Seite ist derselbe &mdash; wie im letzten Tutorial ein Raster. Der Unterschied besteht darin, dass das Raster nur die Filme anzeigt, nach denen Sie gesucht haben.

## <a name="about-html-forms"></a>Informationen zu HTML-Formularen

(Wenn Sie Erfahrung mit dem Erstellen von HTML-Formularen und mit dem Unterschied zwischen `GET` und `POST`haben, können Sie diesen Abschnitt überspringen.)

Ein Formular enthält &mdash; Textfelder, Schaltflächen, Optionsfelder, Kontrollkästchen, Dropdownlisten usw. Benutzer füllen diese Steuerelemente aus oder treffen eine Auswahl, und senden dann das Formular, indem Sie auf eine Schaltfläche klicken.

Die grundlegende HTML-Syntax eines Formulars wird in diesem Beispiel veranschaulicht:

[!code-html[Main](form-basics/samples/sample1.html)]

Wenn dieses Markup auf einer Seite ausgeführt wird, wird ein einfaches Formular erstellt, das wie folgt aussieht:

![Grundlegendes HTML-Formular als im Browser gerendert](form-basics/_static/image2.png)

Das `<form>` Element umschließt HTML-Elemente, die übermittelt werden sollen. (Ein einfacher Fehler ist, Elemente zur Seite hinzuzufügen, aber `<form>` dann vergessen, sie in einem Element zu setzen. In diesem Fall wird nichts eingereicht.) Das `method` Attribut teilt dem Browser mit, wie die Benutzereingabe übermittelt wird. Sie legen `post` dies auf festzulegen, wenn Sie `get` eine Aktualisierung auf dem Server durchführen oder wenn Sie nur Daten vom Server abrufen.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET-, POST- und HTTP-Verbsicherheit**
> 
> HTTP, das Protokoll, das Browser und Server zum Informationsaustausch verwenden, ist in seinen grundlegenden Vorgängen bemerkenswert einfach. Browser verwenden nur wenige Verben, um Anforderungen an Server zu stellen. Wenn Sie Code für das Web schreiben, ist es hilfreich, diese Verben zu verstehen und wie Browser und Server sie verwenden. Bei weitem die am häufigsten verwendeten Verben sind diese:
> 
> - `GET`. Der Browser verwendet dieses Verb, um etwas vom Server abzurufen. Wenn Sie beispielsweise eine URL in Ihren Browser `GET` eingeben, führt der Browser einen Vorgang aus, um die gewünschte Seite anzufordern. Wenn die Seite Grafiken enthält, `GET` führt der Browser zusätzliche Vorgänge aus, um die Bilder abzubekommen. Wenn `GET` der Vorgang Informationen an den Server übergeben muss, werden die Informationen als Teil der URL in der Abfragezeichenfolge übergeben.
> - `POST`. Der Browser `POST` sendet eine Anforderung, um Daten zu übermitteln, die auf dem Server hinzugefügt oder geändert werden sollen. Das `POST` Verb wird z. B. verwendet, um Datensätze in einer Datenbank zu erstellen oder vorhandene zu ändern. Wenn Sie in den meisten Fall ein Formular ausfüllen und auf `POST` die Schaltfläche Senden klicken, führt der Browser einen Vorgang aus. Bei `POST` einem Vorgang befinden sich die an den Server übergebenen Daten im Hauptteil der Seite.
> 
> Ein wichtiger Unterschied zwischen diesen `GET` Verben besteht darin, dass ein Vorgang nichts auf dem Server ändern `GET` soll – oder um es etwas abstrakter zu sagen, dass ein Vorgang nicht zu einer Änderung des Zustands auf dem Server führt. Sie können `GET` einen Vorgang für dieselben Ressourcen begehen, so oft Sie möchten, und diese Ressourcen ändern sich nicht. (Eine `GET` Operation wird oft als "sicher" bezeichnet, oder um einen technischen Begriff zu verwenden, ist *idempotent*.) Im Gegensatz dazu ändert `POST` eine Anforderung natürlich bei jeder Ausführung des Vorgangs etwas auf dem Server.
> 
> Zwei Beispiele werden dazu beitragen, diese Unterscheidung zu veranschaulichen. Wenn Sie eine Suche mit einer Engine wie Bing oder Google durchführen, füllen Sie ein Formular aus, das aus einem Textfeld besteht, und klicken dann auf die Suchschaltfläche. Der Browser `GET` führt einen Vorgang aus, wobei der Wert, den Sie in das Feld eingegeben haben, als Teil der URL übergeben wird. Die `GET` Verwendung eines Vorgangs für diesen Formulartyp ist in Ordnung, da ein Suchvorgang keine Ressourcen auf dem Server ändert, sondern nur Informationen abruft.
> 
> Betrachten Sie nun den Prozess der Online-Bestellung. Sie geben die Bestelldetails ein und klicken dann auf die Schaltfläche Absenden. Dieser Vorgang ist `POST` eine Anforderung, da der Vorgang zu Änderungen auf dem Server führt, z. B. zu einem neuen Auftragsdatensatz, einer Änderung ihrer Kontoinformationen und möglicherweise vielen anderen Änderungen. Im `GET` Gegensatz zum Vorgang `POST` können Sie Ihre Anforderung nicht wiederholen– wenn Sie dieanforderung erneut übermittelt haben, würden Sie eine neue Bestellung auf dem Server generieren. (In solchen Fällen warnen Websites Sie oft davor, mehr als einmal auf eine Schaltfläche zum Absenden zu klicken, oder deaktivieren die Schaltfläche "Absenden", sodass Sie das Formular nicht versehentlich erneut senden.)
> 
> Im Verlauf dieses Tutorials verwenden Sie `GET` sowohl einen `POST` Vorgang als auch einen Vorgang, um mit HTML-Formularen zu arbeiten. Wir erklären in jedem Fall, warum das Verb, das Sie verwenden, das richtige ist.
> 
> (Weitere Informationen zu HTTP-Verben finden Sie im Artikel [Methodendefinitionen](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) auf der W3C-Website.)

Die meisten Benutzereingabeelemente sind HTML-Elemente. `<input>` Sie sehen `<input type="type" name="name">,` so aus, als ob *der Typ* die Art des gewünschten Benutzereingabesteuerelements angibt. Diese Elemente sind die gemeinsamen:

- Textfeld:`<input type="text">`
- Kontrollkästchen:`<input type="check">`
- Optionsfeld:`<input type="radio">`
- Schaltfläche:`<input type="button">`
- Schaltfläche "Senden":`<input type="submit">`

Sie können das `<textarea>` Element auch verwenden, um `<select>` ein mehrzeiliges Textfeld zu erstellen, und das Element, um eine Dropdown- oder Scrollliste zu erstellen. (Weitere Informationen zu HTML-Formularelementen finden Sie unter [HTML-Formulare und Eingaben](http://www.w3schools.com/html/html_forms.asp) auf der W3Schools-Website.)

Das `name` Attribut ist sehr wichtig, da der Name ist, wie Sie den Wert des Elements später erhalten, wie Sie in Kürze sehen werden.

Der interessante Teil ist, was Sie, der Seitenentwickler, mit den Eingaben des Benutzers tun. Diesen Elementen ist kein integriertes Verhalten zugeordnet. Stattdessen müssen Sie die Werte abrufen, die der Benutzer eingegeben oder ausgewählt hat, und etwas mit ihnen tun. Das erfahren Sie in diesem Tutorial.

> [!TIP] 
> 
> **HTML5- und Eingabeformulare**
> 
> Wie Sie vielleicht wissen, befindet sich HTML im Übergang, und die neueste Version (HTML5) bietet Unterstützung für intuitivere Möglichkeiten für Benutzer, Informationen einzugeben. In HTML5 können Sie beispielsweise (der Seitenentwickler) der Seite mitteilen, dass der Benutzer ein Datum eingeben soll. Der Browser kann dann automatisch einen Kalender anzeigen, anstatt dass der Benutzer ein Datum manuell eingeben muss. HTML5 ist jedoch neu und wird noch nicht in allen Browsern unterstützt.
> 
> ASP.NET WebPages unterstützt HTML5-Eingaben in dem Maße, wie es der Browser des Benutzers tut. Eine Vorstellung der neuen Attribute `<input>` für das Element in HTML5 finden Sie unter [HTML-Eingabetyp &lt;&gt; Attribut](http://www.w3schools.com/html/html_form_input_types.asp) auf der W3Schools-Website.

## <a name="creating-the-form"></a>Erstellen des Formulars

Öffnen Sie in WebMatrix im Arbeitsbereich **Dateien** die Seite *Movies.cshtml.*

Fügen Sie `</h1>` nach dem `<div>` schließenden `grid.GetHtml` Tag und vor dem öffnenden Tag des Aufrufs das folgende Markup hinzu:

[!code-html[Main](form-basics/samples/sample2.html)]

Dieses Markup erstellt ein Formular mit `searchGenre` einem Textfeld mit dem Namen und einer Schaltfläche zum Absenden. Das Textfeld und die Schaltfläche `<form>` "Senden" sind in ein Element eingeschlossen, dessen `method` Attribut auf `get`festgelegt ist. (Denken Sie daran, dass, wenn Sie das `<form>` Textfeld und die Schaltfläche "Senden" nicht in einem Element einfügen, nichts gesendet wird, wenn Sie auf die Schaltfläche klicken.) Sie verwenden `GET` das Verb hier, weil Sie ein Formular erstellen, das keine Änderungen auf dem Server vornimmt – es führt nur zu einer Suche. (Im vorherigen Tutorial haben `post` Sie eine Methode verwendet, d. h., wie Sie Änderungen an den Server übermitteln. Das sehen Sie im nächsten Tutorial erneut.)

Führen Sie die Seite aus. Obwohl Sie kein Verhalten für das Formular definiert haben, können Sie sehen, wie es aussieht:

![Filmseite mit Suchfeld für Genre](form-basics/_static/image3.png)

Geben Sie einen Wert in das Textfeld ein, z. B. "Komödie". Klicken Sie dann auf **Genre suchen**.

Notieren Sie sich die URL der Seite. Da Sie `<form>` das Attribut `method` des `get`Elements auf festlegen, ist der eingegebene Wert nun Teil der Abfragezeichenfolge in der URL, wie folgt:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Lesen von Formularwerten

Die Seite enthält bereits Code, der Datenbankdaten abruft und die Ergebnisse in einem Raster anzeigt. Nun müssen Sie Code hinzufügen, der den Wert des Textfelds liest, damit Sie eine SQL-Abfrage ausführen können, die den Suchbegriff enthält.

Da Sie die Methode des `get`Formulars auf festlegen, können Sie den Wert lesen, der in das Textfeld eingegeben wurde, indem Sie Code wie den folgenden verwenden:

`var searchTerm = Request.QueryString["searchGenre"];`

Das `Request.QueryString` Objekt `QueryString` (die `Request` Eigenschaft des Objekts) enthält die Werte `GET` von Elementen, die als Teil des Vorgangs übermittelt wurden. Die `Request.QueryString` Eigenschaft enthält eine *Auflistung* (eine Liste) der Werte, die im Formular gesendet werden. Um einen einzelnen Wert abzuerhalten, geben Sie den Namen des gewünschten Elements an. Aus diesem Grund müssen Sie `name` ein `<input>` Attribut`searchTerm`für das Element ( ) haben, das das Textfeld erstellt. (Weitere Informationen `Request` zum Objekt finden Sie später in der [Seitenleiste.)](#BKMK_TheRequestObject)

Es ist einfach genug, den Wert des Textfelds zu lesen. Aber wenn der Benutzer überhaupt nichts in das Textfeld eingegeben hat, aber trotzdem auf **Suchen** geklickt hat, können Sie diesen Klick ignorieren, da nichts zu suchen ist.

Der folgende Code ist ein Beispiel, das zeigt, wie diese Bedingungen implementiert werden. (Sie müssen diesen Code noch nicht hinzufügen; Sie werden dies gleich tun.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Der Test bricht auf diese Weise zusammen:

- Abrufen des `Request.QueryString["searchGenre"]`Werts von , nämlich `<input>` des `searchGenre`Werts, der in das Element mit dem Namen eingegeben wurde.
- Finden Sie heraus, ob es `IsEmpty` leer ist, indem Sie die Methode verwenden. Diese Methode ist die Standardmethode, um zu bestimmen, ob etwas (z. B. ein Formularelement) einen Wert enthält. Aber wirklich, Sie kümmern sich nur, wenn es *nicht* leer ist, daher ...
- Fügen `!` Sie den Operator `IsEmpty` vor dem Test hinzu. (Der `!` Operator bedeutet logisches NOT).

Im Klartext: `if` Die gesamte Bedingung übersetzt sich wie folgt: *Wenn das searchGenre-Element des Formulars nicht leer ist, dann ...*

Dieser Block legt die Bühne zum Erstellen einer Abfrage fest, die den Suchbegriff verwendet. Dies erledigen Sie im nächsten Abschnitt.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Das Anforderungsobjekt**
> 
> Das `Request` Objekt enthält alle Informationen, die der Browser an Ihre Anwendung sendet, wenn eine Seite angefordert oder übermittelt wird. Dieses Objekt enthält alle Informationen, die der Benutzer bereitstellt, z. B. Textfeldwerte oder eine Datei zum Hochladen. Es enthält auch alle Arten von zusätzlichen Informationen, wie Cookies, Werte in der URL-Abfragezeichenfolge (falls vorhanden), den Dateipfad der Seite, die ausgeführt wird, den Browsertyp, den der Benutzer verwendet, die Liste der Sprachen, die im Browser festgelegt sind, und vieles mehr.
> 
> Das `Request` Objekt ist eine *Auflistung* (Liste) von Werten. Sie erhalten einen individuellen Wert aus der Auflistung, indem Sie ihren Namen angeben:
> 
> `var someValue = Request["name"];`
> 
> Das `Request` Objekt macht tatsächlich mehrere Teilmengen verfügbar. Beispiel:
> 
> - `Request.Form`gibt Ihnen Werte aus `<form>` Elementen innerhalb des `POST` übermittelten Elements an, wenn es sich bei der Anforderung um eine Anforderung handelt.
> - `Request.QueryString`gibt Nur die Werte in der Abfragezeichenfolge der URL an. (In einer `http://mysite/myapp/page?searchGenre=action&page=2`URL `?searchGenre=action&page=2` wie ist der Abschnitt der URL die Abfragezeichenfolge.)
> - `Request.Cookies`Auf die vom Browser gesendeten Cookies zugreifen.
> 
> Um einen Wert zu erhalten, von dem Sie `Request["name"]`wissen, dass er sich im gesendeten Formular befindet, können Sie verwenden. Alternativ können Sie die spezifischeren `Request.Form["name"]` Versionen `POST` (für `Request.QueryString["name"]` Anforderungen) oder (für `GET` Anforderungen) verwenden. Natürlich ist *der Name* der Name des zu erhaltenden Elements.
> 
> Der Name des Elements, das Sie erhalten möchten, muss innerhalb der von Ihnen verwendenden Sammlung eindeutig sein. Aus diesem Grund `Request` stellt das Objekt `Request.Form` `Request.QueryString`die Teilmengen wie und bereit. Angenommen, Ihre Seite enthält `userName` ein Formularelement mit `userName`dem Namen und *auch* ein Cookie mit dem Namen . Wenn Sie `Request["userName"]`erhalten, ist unklar, ob Sie den Formularwert oder das Cookie verwenden möchten. Wenn Sie jedoch `Request.Form["userName"]` `Request.Cookie["userName"]`oder erhalten, werden Sie explizit zu dem Wert, den Sie erhalten sollen.
> 
> Es ist eine gute Praxis, spezifisch zu `Request` sein und die Teilmenge `Request.Form` `Request.QueryString`von dem zu verwenden, an dem Sie interessiert sind, wie oder . Für die einfachen Seiten, die Sie in diesem Tutorial erstellen, macht es wahrscheinlich keinen wirklichen Unterschied. Wenn Sie jedoch komplexere Seiten erstellen, `Request.Form` `Request.QueryString` können Sie die explizite Version verwenden oder Ihnen helfen, Probleme zu vermeiden, die auftreten können, wenn die Seite ein Formular (oder mehrere Formulare), Cookies, Abfragezeichenfolgenwerte usw. enthält.

## <a name="creating-a-query-by-using-a-search-term"></a>Erstellen einer Abfrage mithilfe eines Suchbegriffs

Nachdem Sie nun wissen, wie Sie den Vom Benutzer eingegebenen Suchbegriff abrufen, können Sie eine Abfrage erstellen, die ihn verwendet. Denken Sie daran, dass Sie eine SQL-Abfrage verwenden, die wie folgt aussieht, um alle Filmelemente aus der Datenbank zu erhalten:

`SELECT * FROM Movies`

Um nur bestimmte Filme zu erhalten, müssen `Where` Sie eine Abfrage verwenden, die eine Klausel enthält. Mit dieser Klausel können Sie eine Bedingung festlegen, für die Zeilen von der Abfrage zurückgegeben werden. Hier sehen Sie ein Beispiel:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Das Grundformat `WHERE column = value`ist . Sie können neben nur `=`, `>` wie (größer `<` als), `<>` (weniger als), (nicht gleich), `<=` (weniger als oder gleich) usw. verschiedene Operatoren verwenden, je nachdem, was Sie suchen.

Falls Sie sich fragen, SQL-Anweisungen &mdash; `SELECT` sind nicht `Select` Groß-/Kleinschreibung ist die gleiche wie (oder sogar `select`). Menschen nutzen Schlüsselwörter jedoch häufig in einer `SELECT` `WHERE`SQL-Anweisung, wie und , um das Lesen zu erleichtern.

### <a name="passing-the-search-term-as-a-parameter"></a>Übergeben des Suchbegriffs als Parameter

Die Suche nach einem bestimmten`WHERE Genre = 'Action'`Genre ist einfach genug ( ), aber Sie möchten in der Lage sein, nach jedem Genre zu suchen, das der Benutzer eingibt. Dazu erstellen Sie als SQL-Abfrage, die einen Platzhalter für den zu durchsuchenden Wert enthält. Es sieht wie folgt aus:

`SELECT * FROM Movies WHERE Genre = @0`

Der Platzhalter `@` ist das Zeichen gefolgt von Null. Wie Sie vielleicht vermuten, kann eine Abfrage mehrere Platzhalter `@0` `@1`enthalten, und sie würden den Namen , , `@2`, usw. haben.

Um die Abfrage einzurichten und den Wert tatsächlich zu übergeben, verwenden Sie den Code wie den folgenden:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Dieser Code ähnelt dem, was Sie bereits getan haben, um Daten im Raster anzuzeigen. Die einzigen Unterschiede sind:

- Die Abfrage enthält einen`WHERE Genre = @0"`Platzhalter ( ).
- Die Abfrage wird in`selectCommand`eine Variable ( ) eingefügt. zuvor haben Sie die Abfrage `db.Query` direkt an die Methode übergeben.
- Wenn Sie `db.Query` die Methode aufrufen, übergeben Sie sowohl die Abfrage als auch den Wert, der für den Platzhalter verwendet werden soll. (Wenn die Abfrage über mehrere Platzhalter verfügen würde, übergeben Sie sie alle als separate Werte an die Methode.)

Wenn Sie alle diese Elemente zusammensetzen, erhalten Sie den folgenden Code:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Wichtig!** Die Verwendung von `@0`Platzhaltern (z. B. ) zum Übergeben von Werten an einen SQL-Befehl ist für die Sicherheit *äußerst wichtig.* Die Art und Weise, wie Sie es hier sehen, mit Platzhaltern für variable Daten, ist die einzige Möglichkeit, SQL-Befehle zu erstellen.
> 
> Erstellen Sie niemals eine SQL-Anweisung, indem Sie literalen Text und Werte, die Sie vom Benutzer erhalten, zusammenstellen (verstellen). Durch das Verschließen von Benutzereingaben in einer SQL-Anweisung wird Ihre Website zu einem *SQL-Injektionsangriff* geöffnet, bei dem ein böswilliger Benutzer Werte an Ihre Seite sendet, die Ihre Datenbank hacken. (Weitere Informationen finden Sie im Artikel [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) auf der MSDN-Website.)

## <a name="updating-the-movies-page-with-search-code"></a>Aktualisieren der Filmseite mit Suchcode

Jetzt können Sie den Code in der Datei *Movies.cshtml* aktualisieren. Ersetzen Sie zunächst den Code im Codeblock oben auf der Seite durch diesen Code:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Der Unterschied besteht darin, dass Sie `selectCommand` die Abfrage in die `db.Query` Variable eingefügt haben, an die Sie später übergeben werden. Wenn Sie die SQL-Anweisung in eine Variable eintragen, können Sie die Anweisung ändern, was Sie tun werden, um die Suche durchzuführen.

Sie haben auch diese beiden Zeilen entfernt, die Sie später wieder einstecken werden:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Sie möchten die Abfrage noch nicht ausführen (d. h. anrufen `db.Query`) und `WebGrid` sie möchten den Helfer auch noch nicht initialisieren. Sie werden diese Dinge tun, nachdem Sie herausgefunden haben, welche SQL-Anweisung ausgeführt werden muss.

Nach diesem umgeschriebenen Block können Sie die neue Logik für die Verarbeitung der Suche hinzufügen. Der ausgefüllte Code sieht wie folgt aus. Aktualisieren Sie den Code auf Ihrer Seite, damit er mit diesem Beispiel übereinstimmt:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Die Seite funktioniert jetzt so. Jedes Mal, wenn die Seite ausgeführt `selectCommand` wird, öffnet der Code die Datenbank, `Movies` und die Variable wird auf die SQL-Anweisung festgelegt, die alle Datensätze aus der Tabelle abruft. Der Code initialisiert `searchTerm` auch die Variable.

Wenn die aktuelle Anforderung jedoch einen `searchGenre` Wert für `selectCommand` das Element enthält, wird der Code `Where` auf eine andere Abfrage festgelegt, d. h. auf eine Abfrage, die die Klausel enthält, nach einem Genre zu suchen. Es setzt `searchTerm` auch auf das, was für das Suchfeld übergeben wurde (was nichts sein könnte).

Unabhängig davon, welche `selectCommand`SQL-Anweisung in `db.Query` ist, ruft der Code `searchTerm`dann auf, um die Abfrage auszuführen, und übergibt sie, was auch immer in ist. Wenn nichts in `searchTerm`ist, spielt es keine Rolle, denn in diesem Fall gibt `selectCommand` es keinen Parameter, an den der Wert trotzdem übergeben werden kann.

Schließlich initialisiert der Code `WebGrid` den Hilfshelfer mithilfe der Abfrageergebnisse, genau wie zuvor.

Sie können sehen, dass Sie, indem Sie die SQL-Anweisung und den Suchbegriff in Variablen setzen, dem Code Flexibilität hinzugefügt haben. Wie Sie später in diesem Tutorial sehen werden, können Sie dieses grundlegende Framework verwenden und weiterhin Logik für verschiedene Arten von Suchvorgängen hinzufügen.

## <a name="testing-the-search-by-genre-feature"></a>Testen der Search-by-Genre-Funktion

Führen Sie in WebMatrix die Seite *Movies.cshtml* aus. Sie sehen die Seite mit dem Textfeld für Genre.

Geben Sie ein Genre ein, das Sie für einen Ihrer Testdatensätze eingegeben haben, und klicken Sie dann auf **Suchen**. Dieses Mal sehen Sie eine Liste nur der Filme, die zu diesem Genre passen:

![Film-Seitenliste nach der Suche nach Genre 'Comedies'](form-basics/_static/image4.png)

Geben Sie ein anderes Genre ein und suchen Sie erneut. Versuchen Sie, das Genre einzugeben, indem Sie alle Kleinbuchstaben oder alle Großbuchstaben verwenden, damit Sie sehen können, dass die Suche nicht groß ist.

## <a name="remembering-what-the-user-entered"></a>"Erinnern" Was der Benutzer eingegeben hat

Sie haben vielleicht bemerkt, dass Sie, nachdem Sie ein Genre eingegeben und auf **"Genre suchen"** geklickt haben, eine Auflistung für dieses Genre gesehen haben. Das Suchtextfeld war &mdash; jedoch leer, mit anderen Worten, es erinnerte sich nicht daran, was Sie eingegeben hatten.

Es ist wichtig zu verstehen, warum dieses Verhalten auftritt. Wenn Sie eine Seite senden, sendet der Browser eine Anforderung an den Webserver. Wenn ASP.NET die Anforderung erhält, erstellt er eine brandneue Instanz der Seite, führt den darin ausgeführten Code aus und rendert die Seite dann erneut im Browser. Tatsächlich weiß die Seite jedoch nicht, dass Sie nur mit einer früheren Version von sich selbst gearbeitet haben. Alles, was sie weiß, ist, dass es eine Anfrage, die einige Formulardaten enthalten hatte.

Jedes Mal, wenn &mdash; Sie eine Seite anfordern, ob zum ersten Mal oder durch Senden, &mdash; erhalten Sie eine neue Seite. Der Webserver verfügt nicht über speicherspeicher für Ihre letzte Anforderung. Auch ASP.NET nicht, und auch der Browser nicht. Die einzige Verbindung zwischen diesen separaten Instanzen der Seite sind alle Daten, die Sie zwischen ihnen übertragen. Wenn Sie z. B. eine Seite senden, kann die neue Seiteninstanz die Formulardaten abrufen, die von der vorherigen Instanz gesendet wurden. (Eine weitere Möglichkeit, Daten zwischen Seiten zu übergeben, ist die Verwendung von Cookies.)

Eine formale Möglichkeit, diese Situation zu beschreiben, ist zu sagen, dass Webseiten *zustandslos*sind. Webserver und die Seiten selbst sowie die Elemente auf der Seite enthalten keine Informationen über den vorherigen Status einer Seite. Das Web wurde auf diese Weise entwickelt, weil die Aufrechterhaltung des Status für einzelne Anforderungen schnell die Ressourcen von Webservern ausschöpfen würde, die oft Tausende, vielleicht sogar Hunderttausende von Anfragen pro Sekunde verarbeiten.

Deshalb war das Textfeld leer. Nachdem Sie die Seite übermittelt haben, ASP.NET eine neue Instanz der Seite erstellt und durch den Code und das Markup ausgeführt. Es gab nichts in diesem Code, das ASP.NET anwies, einen Wert in das Textfeld zu setzen. Also ASP.NET nichts getan, und das Textfeld wurde ohne Wert gerendert.

Es gibt tatsächlich eine einfache Möglichkeit, dieses Problem zu umgehen. Das Genre, das Sie *is* in das Textfeld &mdash; eingegeben haben, steht Ihnen im Code zur Verfügung, der sich in `Request.QueryString["searchGenre"]`befindet.

Aktualisieren Sie das Markup für `value` das Textfeld, `searchTerm`sodass das Attribut seinen Wert abruft, z. B. in diesem Beispiel:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Auf dieser Seite hätten Sie `value` das Attribut `searchTerm` auch auf die Variable festlegen können, da diese Variable auch das eingegebene Genre enthält. Aber das `Request` Objekt zu `value` verwenden, um das Attribut wie hier gezeigt festzulegen, ist die Standardmethode, um diese Aufgabe auszuführen. (Angenommen, Sie möchten &mdash; dies in einigen Situationen sogar tun, sie können die Seite *ohne* Werte in den Feldern rendern. Alles hängt davon ab, was mit Ihrer App vor sich geht.)

> [!NOTE]
> Sie können sich den Wert eines Textfelds, das für Kennwörter verwendet wird, nicht "erinnern". Es wäre eine Sicherheitslücke, wenn Benutzer ein Kennwortfeld mithilfe von Code ausfüllen können.

Führen Sie die Seite erneut aus, geben Sie ein Genre ein, und klicken Sie auf **Genre suchen**. Diesmal sehen Sie nicht nur die Ergebnisse der Suche, sondern das Textfeld merkt sich, was Sie beim letzten Mal eingegeben haben:

![Seite, die anzeigt, dass sich das Textfeld an den vorherigen Eintrag "erinnert" hat](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Suchen nach einem beliebigen Wort im Titel

Sie können jetzt nach einem beliebigen Genre suchen, aber Sie können auch nach einem Titel suchen. Es ist schwierig, einen Titel genau richtig zu bekommen, wenn Sie suchen, so dass Sie stattdessen nach einem Wort suchen können, das irgendwo in einem Titel angezeigt wird. Dazu verwenden Sie in SQL `LIKE` den Operator und die Syntax wie folgt:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Dieser Befehl erhält alle Filme, deren Titel "Abenteuer" enthalten. Wenn Sie `LIKE` den Operator verwenden, `%` fügen Sie das Platzhalterzeichen als Teil des Suchbegriffs ein. Die `LIKE 'adventure%'` Suche bedeutet "beginnend mit 'Abenteuer'". (Technisch bedeutet es "Die Saite 'Abenteuer' gefolgt von allem.") In ähnlicher Weise `LIKE '%adventure'` bedeutet der Suchbegriff "alles, was von der Zeichenfolge 'Abenteuer' gefolgt wird", was eine andere Möglichkeit ist, "mit 'Abenteuer' zu enden".

Der Suchbegriff `LIKE '%adventure%'` bedeutet daher "mit 'Abenteuer' überall im Titel." (Technisch gesehen "alles im Titel, gefolgt von 'Abenteuer', gefolgt von allem.")

Fügen `<form>` Sie innerhalb des Elements das folgende `</div>` Markup direkt unter dem `</form>` schließenden Tag für die Genresuche hinzu (kurz vor dem schließenden Element):

[!code-html[Main](form-basics/samples/sample10.html)]

Der Code, der diese Suche verarbeitet, ähnelt dem Code für die `LIKE` Genresuche, mit der Ausnahme, dass Sie die Suche zusammenstellen müssen. Fügen Sie diesen `if` Block im Codeblock oben auf `if` der Seite direkt nach dem Block für die Genresuche hinzu:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Dieser Code verwendet dieselbe Logik, die Sie zuvor `LIKE` gesehen haben,`%`mit der Ausnahme, dass die Suche einen Operator verwendet und der Code " " vor und nach dem Suchbegriff abgibt.

Beachten Sie, wie es einfach war, der Seite eine weitere Suche hinzuzufügen. Alles, was Sie tun mussten, war:

- Erstellen `if` Sie einen Block, der getestet wurde, um festzustellen, ob das entsprechende Suchfeld einen Wert hatte.
- Legen `selectCommand` Sie die Variable auf eine neue SQL-Anweisung fest.
- Legen `searchTerm` Sie die Variable auf den Wert fest, der an die Abfrage übergeben werden soll.

Hier ist der komplette Codeblock, der die neue Logik für eine Titelsuche enthält:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Hier ist eine Zusammenfassung der Funktionsweise dieses Codes:

- Die `searchTerm` Variablen `selectCommand` und werden oben initialisiert. Sie legen diese Variablen auf den entsprechenden Suchbegriff (falls vorhanden) und den entsprechenden SQL-Befehl basierend auf den Aktionen des Benutzers auf der Seite fest. Die Standardsuche ist der einfache Fall, alle Filme aus der Datenbank zu erhalten.
- In den `searchGenre` Tests `searchTitle`für und `searchTerm` wird der Code auf den Wert festgelegt, nach dem Sie suchen möchten. Diese Codeblöcke `selectCommand` werden auch auf einen entsprechenden SQL-Befehl für diese Suche festgelegt.
- Die `db.Query` Methode wird nur einmal aufgerufen, indem `selectedCommand` der SQL-Befehl verwendet wird und welcher Wert auch immer in `searchTerm`ist. Wenn es keinen Suchbegriff (kein Genre und kein `searchTerm` Titelwort) gibt, ist der Wert von einer leeren Zeichenfolge. Das spielt jedoch keine Rolle, da in diesem Fall die Abfrage keinen Parameter benötigt.

## <a name="testing-the-title-search-feature"></a>Testen der Titelsuchfunktion

Jetzt können Sie Ihre abgeschlossene Suchseite testen. Führen Sie *Movies.cshtml*aus.

Geben Sie ein Genre ein und klicken Sie auf **Genre suchen**. Das Raster zeigt Filme dieses Genres, wie zuvor.

Geben Sie ein Titelwort ein, und klicken Sie auf **Titel suchen**. Das Raster zeigt Filme an, die dieses Wort im Titel haben.

![Filmseitenliste nach der Suche nach 'The' im Titel](form-basics/_static/image6.png)

Lassen Sie beide Textfelder leer, und klicken Sie auf eine der beiden Schaltflächen. Das Raster zeigt alle Filme an.

## <a name="combining-the-queries"></a>Kombinieren der Abfragen

Möglicherweise stellen Sie fest, dass die Suchvorgänge, die Sie durchführen können, exklusiv sind. Sie können den Titel und das Genre nicht gleichzeitig durchsuchen, auch wenn beide Suchfelder Werte enthalten. Sie können z. B. nicht nach allen Actionfilmen suchen, deren Titel "Abenteuer" enthält. (Da die Seite jetzt codiert ist, erhält die Titelsuche Vorrang, wenn Sie Werte für Genre und Titel eingeben.) Um eine Suche zu erstellen, die die Bedingungen kombiniert, müssen Sie eine SQL-Abfrage mit einer Syntax wie der folgenden erstellen:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

Und Sie müssten die Abfrage ausführen, indem Sie eine Anweisung wie die folgende verwenden (grob gesprochen):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Das Erstellen von Logik, um viele Permutationen von Suchkriterien zu ermöglichen, kann ein wenig involviert sein, wie Sie sehen können. Deshalb hören wir hier auf.

## <a name="coming-up-next"></a>Coming Up Next

Im nächsten Tutorial erstellen Sie eine Seite, die ein Formular verwendet, auf der Benutzer Filme zur Datenbank hinzufügen können.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Vollständige Sendeliste für Filmseite (aktualisiert mit der Suche)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Weitere Ressourcen

- [Einführung in die ASP.NET-Webprogrammierung mit der Razor-Syntax](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL WHERE-Klausel](http://www.w3schools.com/sql/sql_where.asp) auf der W3Schools-Website
- [Artikel "Methodendefinitionen"](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) auf der W3C-Website

> [!div class="step-by-step"]
> [Zurück](displaying-data.md)
> [Weiter](entering-data.md)
