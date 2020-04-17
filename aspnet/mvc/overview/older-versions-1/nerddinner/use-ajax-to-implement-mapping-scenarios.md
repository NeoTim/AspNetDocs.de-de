---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Verwenden von AJAX zum Implementieren von Zuordnungsszenarien | Microsoft Docs
author: rick-anderson
description: Schritt 11 zeigt, wie Sie aJAX-Mapping-Unterstützung in unsere NerdDinner-Anwendung integrieren, sodass Benutzer, die Abendessen erstellen, bearbeiten oder anzeigen, die...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542585"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>Implementieren von Zuordnungsszenarien mithilfe von AJAX

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 11 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 11 zeigt, wie Sie die AJAX-Mapping-Unterstützung in unsere NerdDinner-Anwendung integrieren und Benutzern, die Abendessen erstellen, bearbeiten oder anzeigen, ermöglichen, den Ort des Abendessens grafisch zu sehen.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner Step 11: Integrieren einer AJAX-Karte

Durch die Integration der AJAX-Mapping-Unterstützung werden wir unsere Anwendung nun optisch etwas spannender machen. Auf diese Weise können Benutzer, die Abendessen erstellen, bearbeiten oder anzeigen, den Ort des Abendessens grafisch anzeigen.

### <a name="creating-a-map-partial-view"></a>Erstellen einer Karten-Teilansicht

Wir werden Mapping-Funktionalität an mehreren Stellen in unserer Anwendung verwenden. Um unseren Code DRY beizubehalten, kapseln wir die allgemeine Kartenfunktionalität in einer einzigen Partiellenvorlage, die wir über mehrere Controlleraktionen und -ansichten hinweg wiederverwenden können. Wir nennen diese Teilansicht "map.ascx" und erstellen sie im Verzeichnis "Views".

Wir können die map.ascx teilweise erstellen, indem wir mit der rechten Maustaste auf das Verzeichnis "Views"-Dinners klicken und den Menübefehl "Hinzufügen"&gt;auswählen. Wir nennen die Ansicht "Map.ascx", überprüfen sie als Teilansicht und geben an, dass wir eine stark typisierte "Dinner"-Modellklasse übergeben werden:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, wird unsere Teilvorlage erstellt. Anschließend aktualisieren wir die Datei Map.ascx, um den folgenden Inhalt zu erhalten:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

Der &lt;erste&gt; Skriptverweis verweist auf die Microsoft Virtual Earth 6.2-Zuordnungsbibliothek. Der &lt;zweite&gt; Skriptverweis verweist auf eine map.js-Datei, die wir in Kürze erstellen werden und die unsere gemeinsame Javascript-Zuordnungslogik kapseln wird. Das &lt;div id="theMap"-Element&gt; ist der HTML-Container, den Virtual Earth zum Hosten der Karte verwendet.

Wir haben dann &lt;&gt; einen eingebetteten Skriptblock, der zwei JavaScript-Funktionen enthält, die für diese Ansicht spezifisch sind. Die erste Funktion verwendet jQuery, um eine Funktion zu verdrahten, die ausgeführt wird, wenn die Seite bereit ist, clientseitiges Skript auszuführen. Es ruft eine LoadMap()-Hilfsfunktion auf, die wir in unserer Map.js-Skriptdatei definieren, um das virtuelle Erdkartensteuerelement zu laden. Die zweite Funktion ist ein Rückrufereignishandler, der der Karte einen Pin hinzufügt, der einen Standort identifiziert.

Beachten Sie, wie wir &lt;einen serverseitigen %= %-Block&gt; innerhalb des clientseitigen Skriptblocks verwenden, um den Breiten- und Längengrad des Dinners, das wir in JavaScript zuordnen möchten, einzubetten. Dies ist eine nützliche Methode zum Ausgeben dynamischer Werte, die vom clientseitigen Skript verwendet werden können (ohne dass ein separater AJAX-Rückruf an den Server erforderlich ist, um die Werte abzurufen – was ihn schneller macht). Die &lt;%=&gt; %-Blöcke werden ausgeführt, wenn die Ansicht auf dem Server gerendert wird – und so landet die Ausgabe des HTML-Codes nur mit eingebetteten JavaScript-Werten (z. B. var latitude = 47.64312;).

### <a name="creating-a-mapjs-utility-library"></a>Erstellen einer Map.js-Dienstprogrammbibliothek

Erstellen wir nun die Map.js-Datei, mit der wir die JavaScript-Funktionalität für unsere Karte kapseln können (und implementieren Sie die LoadMap- und LoadPin-Methoden oben). Wir können dies tun, indem wir mit der rechten Maustaste auf das&gt;Verzeichnis "Scripts" in unserem Projekt klicken und dann den Menübefehl "Neues Element hinzufügen" auswählen, das JScript-Element auswählen und es "Map.js" nennen.

Unten ist der JavaScript-Code, den wir der Map.js-Datei hinzufügen, die mit Virtual Earth interagiert, um unsere Karte anzuzeigen und Standort-Pins für unsere Abendessen hinzuzufügen:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Integrieren der Karte in Formulare erstellen und bearbeiten

Wir integrieren nun die Map-Unterstützung in unsere vorhandenen Create- und Edit-Szenarien. Die gute Nachricht ist, dass dies ziemlich einfach zu tun ist, und erfordert nicht, dass wir unseren Controller-Code ändern. Da unsere Ansichten "Erstellen" und "Bearbeiten" eine gemeinsame "DinnerForm"-Teilansicht verwenden, um die Benutzeroberfläche des Dinnerformulars zu implementieren, können wir die Karte an einem Ort hinzufügen und sowohl unsere Create- als auch "Edit-Szenarien" verwenden.

Alles, was wir tun müssen, ist, die Teilansicht "Views"-Dinners-DinnerForm.ascx zu öffnen und zu aktualisieren, um unsere neue Karte teilweise einzuschließen. Unten ist, wie das aktualisierte DinnerForm aussehen wird, sobald die Karte hinzugefügt wird (Beachten Sie: die HTML-Formularelemente werden aus Gründen der Kürze aus dem Codeausschnitt unten weggelassen):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

Der DinnerForm-Teil oben nimmt ein Objekt vom Typ "DinnerFormViewModel" als Modelltyp an (da es sowohl ein Dinner-Objekt als auch eine SelectList zum Auffüllen der Dropdownliste von Ländern benötigt). Unsere Karte teilweise benötigt nur ein Objekt vom Typ "Dinner" als Modelltyp, und wenn wir die Karte teilweise rendern, übergeben wir nur die Dinner-Untereigenschaft von DinnerFormViewModel an sie:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Die JavaScript-Funktion, die wir der partiellen Verwendung jQuery hinzugefügt haben, um ein "blur"-Ereignis an das HTML-Textfeld "Address" anzufügen. Sie haben wahrscheinlich von "Fokus"-Ereignissen gehört, die ausgelöst werden, wenn ein Benutzer in ein Textfeld klickt oder Tabs aufgibt. Das Gegenteil ist ein "blur"-Ereignis, das ausgelöst wird, wenn ein Benutzer ein Textfeld verlässt. Der obige Ereignishandler löscht die Textfeldwerte für Breiten- und Längengrad, wenn dies geschieht, und zeichnet dann die neue Adressposition auf unserer Karte. Ein Rückrufereignishandler, den wir in der Datei map.js definiert haben, aktualisiert dann die Längen- und Breitengradtextfelder in unserem Formular mithilfe von Werten, die von der virtuellen Erde basierend auf der Adresse zurückgegeben werden, die wir ihm gegeben haben.

Und jetzt, wenn wir unsere Anwendung erneut ausführen und auf die Registerkarte "Host Dinner" klicken, sehen wir eine Standardkarte, die zusammen mit unseren Standard-Dinner-Formularelementen angezeigt wird:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Wenn wir eine Adresse eingeben und dann die Registerkarte entfernt, wird die Karte dynamisch aktualisiert, um den Speicherort anzuzeigen, und unser Ereignishandler füllt die Textfelder breiten/längengrad mit den Positionswerten aus:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Wenn wir das neue Abendessen speichern und es dann erneut zur Bearbeitung öffnen, werden wir feststellen, dass die Kartenposition angezeigt wird, wenn die Seite geladen wird:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Jedes Mal, wenn das Adressfeld geändert wird, werden die Karte und die Breiten-/Längengradkoordinaten aktualisiert.

Da nun die Karte die Spielortung anzeigt, können wir auch die Formularfelder Breiten- und Längengrad von sichtbaren Textfeldern in ausgeblendete Elemente ändern (da die Karte sie bei jeder Eingabe einer Adresse automatisch aktualisiert). Dazu wechseln wir von der Verwendung des HTML.TextBox()-HTML-Hilfsfelds zur Verwendung der Html.Hidden()-Hilfsmethode:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

Und jetzt sind unsere Formulare ein wenig benutzerfreundlicher und vermeiden es, den rohen Breiten-/Längengrad anzuzeigen (während sie immer noch bei jedem Dinner in der Datenbank gespeichert werden):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Integrieren der Karte in die Detailansicht

Nachdem wir nun die Karte in unsere Create- und Edit-Szenarien integriert haben, können wir sie auch in unser Detailszenario integrieren. Alles, was wir tun &lt;müssen, ist % Html.RenderPartial("map") aufzurufen; %&gt; in der Detailansicht.

Unten ist, wie der Quellcode zur vollständigen Detailansicht (mit Kartenintegration) aussieht:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

Und jetzt, wenn ein Benutzer zu einer /Dinners/Details/[id] URL navigiert, werden details über das Abendessen, den Ort des Abendessens auf der Karte (komplett mit einem Push-Pin, der beim Schweben den Titel des Abendessens und dessen Adresse anzeigt) angezeigt und einen AJAX-Link zu RSVP dafür haben:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Implementieren der Standortsuche in unserer Datenbank und unserem Repository

Um unsere AJAX-Implementierung abzuschließen, fügen wir der Startseite der Anwendung eine Karte hinzu, mit der Benutzer grafisch nach Abendessen in ihrer Nähe suchen können.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Zunächst implementieren wir Unterstützung innerhalb unserer Datenbank- und Datenrepository-Schicht, um effizient eine standortbasierte Radiussuche für Dinners durchzuführen. Wir könnten die neuen [räumlichen Features von SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) verwenden, um dies zu implementieren, oder [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) alternativ können wir einen SQL-Funktionsansatz verwenden, den Gary Dryden im Artikel hier besprochen hat: und Rob Conery bloggte hier über die Verwendung mit LINQ to SQL:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Um diese Technik zu implementieren, öffnen wir den "Server Explorer" in Visual Studio, wählen die NerdDinner-Datenbank aus und klicken dann mit der rechten Maustaste auf den unter ihm stehenden Unterknoten "Funktionen" und erstellen eine neue Funktion mit "Skalarwert":

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Anschließend fügen wir die folgende DistanceBetween-Funktion ein:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Anschließend erstellen wir eine neue Tabellenfunktion in SQL Server, die wir "NearestDinners" nennen:

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Diese "NearestDinners" Tischfunktion verwendet die DistanceBetween Hilfsfunktion, um alle Dinner innerhalb von 100 Meilen von dem Breiten- und Längengrad, den wir liefern, zurückzugeben:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Um diese Funktion aufzurufen, öffnen wir zuerst den LINQ to SQL-Designer, indem wir auf die Datei NerdDinner.dbml in unserem Verzeichnis "Models" doppelklicken:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Anschließend ziehen wir die Funktionen NearestDinners und DistanceBetween auf den LINQ-zu-SQL-Designer, wodurch sie als Methoden für unsere LINQ-SQL NerdDinnerDataContext-Klasse hinzugefügt werden:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Wir können dann eine "FindByLocation"-Abfragemethode für unsere DinnerRepository-Klasse verfügbar machen, die die NearestDinner-Funktion verwendet, um bevorstehende Dinner s zurückzugeben, die sich innerhalb von 100 Meilen vom angegebenen Speicherort befinden:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>Implementieren einer JSON-basierten AJAX-Suchaktionsmethode

Wir implementieren nun eine Controller-Aktionsmethode, die die neue FindByLocation()-Repository-Methode nutzt, um eine Liste von Dinner-Daten zurückzugeben, die zum Auffüllen einer Karte verwendet werden können. Diese Aktionsmethode wird die Dinner-Daten im JSON-Format (JavaScript Object Notation) zurückgeben, damit sie mit JavaScript auf dem Client leicht bearbeitet werden können.

Um dies zu implementieren, erstellen wir eine neue "SearchController"-Klasse, indem wir&gt;mit der rechten Maustaste auf das Verzeichnis "Controller" klicken und den Menübefehl "Add- Controller" auswählen. Anschließend implementieren wir eine "SearchByLocation"-Aktionsmethode innerhalb der neuen SearchController-Klasse wie folgt:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

Die SearchByLocation-Aktionsmethode des SearchControllers ruft intern die FindByLocation-Methode in DinnerRepository auf, um eine Liste der Abendessen in der Nähe abzurufen. Anstatt die Dinner-Objekte jedoch direkt an den Client zurückzugeben, gibt es stattdessen JsonDinner-Objekte zurück. Die JsonDinner-Klasse macht eine Teilmenge der Dinner-Eigenschaften verfügbar (z. B. aus Sicherheitsgründen gibt sie die Namen der Personen, die RSVP'd für ein Abendessen haben, nicht preis). Es enthält auch eine RSVPCount-Eigenschaft, die beim Dinner nicht vorhanden ist – und die dynamisch berechnet wird, indem die Anzahl der RSVP-Objekte gezählt wird, die einem bestimmten Abendessen zugeordnet sind.

Wir verwenden dann die Json()-Hilfsmethode in der Controller-Basisklasse, um die Reihenfolge der Abendessen mit einem JSON-basierten Drahtformat zurückzugeben. JSON ist ein Standardtextformat zur Darstellung einfacher Datenstrukturen. Im Folgenden finden Sie ein Beispiel dafür, wie eine JSON-formatierte Liste von zwei JsonDinner-Objekten aussieht, wenn sie von unserer Aktionsmethode zurückgegeben wird:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>Aufrufen der JSON-basierten AJAX-Methode mithilfe von jQuery

Wir können nun die Homepage der NerdDinner-Anwendung aktualisieren, um die SearchByLocation-Aktionsmethode des SearchControllers zu verwenden. Dazu öffnen wir die Ansichtsvorlage /Views/Home/Index.aspx und aktualisieren sie so, dass sie ein Textfeld, eine Suchschaltfläche, unsere Karte und ein &lt;div-Element&gt; namens dinnerList enthält:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Wir können dann zwei JavaScript-Funktionen zur Seite hinzufügen:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

Die erste JavaScript-Funktion lädt die Karte, wenn die Seite zum ersten Mal geladen wird. Die zweite JavaScript-Funktion verdrahtet einen JavaScript-Klick-Ereignishandler auf der Suchschaltfläche. Wenn die Schaltfläche gedrückt wird, ruft sie die JavaScript-Funktion FindDinnersGivenLocation() auf, die wir unserer Map.js-Datei hinzufügen:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Diese FindDinnersGivenLocation()-Funktion ruft map auf. Finden () auf der Virtual Earth Control, um es auf dem eingegebenen Ort zu zentrieren. Wenn der virtuelle Erdkarten-Service zurückkehrt, wird die Karte zurückgegeben. Die Find()-Methode ruft die callbackUpdateMapDinners-Rückrufmethode auf, die sie als letztes Argument übergeben hat.

Die callbackUpdateMapDinners()-Methode ist der Ort, an dem die eigentliche Arbeit ausgeführt wird. Es verwendet die hilfsmethode ".post() von jQuery, um einen AJAX-Aufruf für die SearchByLocation()-Aktionsmethode unseres SearchControllers auszuführen – und den Breiten- und Längengrad der neu zentrierten Karte zu übergeben. Es definiert eine Inline-Funktion, die aufgerufen wird, wenn die Hilfsmethode ".post() abgeschlossen ist und die JSON-formatierten Dinner-Ergebnisse, die von der SearchByLocation()-Aktionsmethode zurückgegeben werden, mit einer Variablen namens "dinners" übergeben werden. Es macht dann einen Foreach über jedes zurückgegebene Abendessen und verwendet den Breiten- und Längengrad des Abendessens und andere Eigenschaften, um einen neuen Pin auf der Karte hinzuzufügen. Es fügt auch einen Dinner-Eintrag zur HTML-Liste der Abendessen auf der rechten Seite der Karte hinzu. Anschließend wird ein Hover-Ereignis für die Pins und die HTML-Liste angezeigt, sodass Details zum Abendessen angezeigt werden, wenn ein Benutzer mit dem Mauszeiger über sie schwebt:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

Und jetzt, wenn wir die Anwendung ausführen und die Homepage besuchen, werden wir mit einer Karte vorgestellt. Wenn wir den Namen einer Stadt eingeben, wird die Karte die bevorstehenden Abendessen in ihrer Nähe anzeigen:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Wenn Sie den Mauszeiger über ein Abendessen bewegen, werden Details darüber angezeigt.

Wenn Sie entweder in der Blase oder auf der rechten Seite in der HTML-Liste auf den Dinner-Titel klicken, navigieren Sie uns zum Dinner – für das wir dann optional RSVP verwenden können:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Nächster Schritt

Wir haben jetzt alle Anwendungsfunktionen unserer NerdDinner-Anwendung implementiert. Sehen wir uns nun an, wie wir automatisierte Komponententests ermöglichen können.

> [!div class="step-by-step"]
> [Zurück](use-ajax-to-deliver-dynamic-updates.md)
> [Weiter](enable-automated-unit-testing.md)
