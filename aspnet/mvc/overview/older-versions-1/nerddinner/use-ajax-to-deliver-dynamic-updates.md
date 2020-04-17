---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Verwenden von AJAX zum Bereitstellen dynamischer Updates | Microsoft Docs
author: rick-anderson
description: Schritt 10 implementiert Unterstützung für eingeloggte Benutzer, um IHR Interesse an einem Abendessen zu erreichen, indem ein Ajax-basierter Ansatz verwendet wird, der in das Dinner-Detail integriert ist...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541246"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>Bereitstellen von dynamischen Updates mithilfe von AJAX

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 10 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 10 implementiert Unterstützung für eingeloggte Benutzer, um IHR Interesse an einem Abendessen zu nutzen, indem ein Ajax-basierter Ansatz verwendet wird, der in die Dinner-Details-Seite integriert ist.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner Schritt 10: AJAX ermöglicht RSVPs akzeptiert

Lassen Sie uns nun Unterstützung für eingeloggte Benutzer implementieren, um IHR Interesse an einem Abendessen zu nutzen. Wir ermöglichen dies mithilfe eines AJAX-basierten Ansatzes, der in die Details des Abendessens integriert ist.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Geben an, ob der Benutzer RSVP'd ist

Benutzer können die URL */Dinners/Details/[id*] besuchen, um Details zu einem bestimmten Abendessen zu sehen:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Die Aktionsmethode Details() wird wie folgt implementiert:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

Unser erster Schritt zur Implementierung der RSVP-Unterstützung besteht darin, unserem Dinner-Objekt eine "IsUserRegistered(username)"-Hilfsmethode hinzuzufügen (innerhalb der Dinner.cs Teilklasse, die wir zuvor erstellt haben). Diese Hilfsmethode gibt true oder false zurück, je nachdem, ob der Benutzer derzeit RSVP'd für das Dinner ist:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Anschließend können wir den folgenden Code zu unserer Detail.aspx-Ansichtsvorlage hinzufügen, um eine entsprechende Meldung anzuzeigen, die angibt, ob der Benutzer für das Ereignis registriert ist oder nicht:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

Und jetzt, wenn ein Benutzer ein Abendessen besucht, werden sie für sie registriert werden, wird diese Meldung angezeigt:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

Und wenn sie ein Dinner besuchen, sind sie nicht registriert für sie sehen die folgende Nachricht:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Implementieren der Registeraktionsmethode

Fügen wir nun die Funktionen hinzu, die erforderlich sind, um Benutzern RSVP für ein Abendessen auf der Detailseite zu ermöglichen.

Um dies zu implementieren, erstellen wir eine neue "RSVPController"-Klasse, indem wir&gt;mit der rechten Maustaste auf das Verzeichnis "Controller" klicken und den Menübefehl "Add- Controller" auswählen.

Wir implementieren eine "Register"-Aktionsmethode innerhalb der neuen RSVPController-Klasse, die eine ID für ein Dinner als Argument annimmt, das entsprechende Dinner-Objekt abruft, überprüft, ob sich der angemeldete Benutzer derzeit in der Liste der Benutzer befindet, die sich dafür registriert haben, und wenn nicht, fügt er ein RSVP-Objekt für sie hinzu:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Beachten Sie oben, wie wir eine einfache Zeichenfolge als Ausgabe der Aktionsmethode zurückgeben. Wir hätten diese Nachricht in eine Ansichtsvorlage einbetten können – aber da sie so klein ist, verwenden wir einfach die Content()-Hilfsmethode für die Controller-Basisklasse und geben eine Zeichenfolgennachricht wie oben zurück.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>Aufrufen der RSVPForEvent-Aktionsmethode mithilfe von AJAX

Wir verwenden AJAX, um die Registrierungsaktionsmethode aus unserer Detailansicht aufzurufen. Dies zu implementieren ist ziemlich einfach. Zuerst fügen wir zwei Skriptbibliotheksverweise hinzu:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

Die erste Bibliothek verweist auf die kernASP.NET Client-seitige Skriptbibliothek von AJAX. Diese Datei hat eine Größe von ca. 24k (komprimiert) und enthält die clientseitige AJAX-Kernfunktionalität. Die zweite Bibliothek enthält Dienstprogrammfunktionen, die in die integrierten AJAX-Hilfsmethoden von ASP.NET MVC integriert werden (die wir in Kürze verwenden werden).

Wir können dann den zuvor hinzugefügten Ansichtsvorlagencode aktualisieren, sodass wir anstelle einer Meldung "Sie sind nicht für dieses Ereignis registriert" stattdessen einen Link rendern, der bei einem Push-Aufruf einen AJAX-Aufruf ausführt, der unsere RSVPForEvent-Aktionsmethode auf unserem RSVP-Controller und RSVPs-Benutzer aufruft:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

Die oben verwendete Ajax.ActionLink()-Hilfsmethode ist integriert ASP.NET MVC und ähnelt der Html.ActionLink()-Hilfsmethode, mit der Ausnahme, dass sie anstelle einer Standardnavigation einen AJAX-Aufruf der Aktionsmethode ausführt, wenn auf den Link geklickt wird. Oben rufen wir die Aktionsmethode "Registrieren" auf dem "RSVP"-Controller auf und übergeben die DinnerID als "id"-Parameter. Der letzte AjaxOptions-Parameter, den wir übergeben, zeigt an, dass wir &lt;&gt; den von der Aktionsmethode zurückgegebenen Inhalt übernehmen und das HTML-div-Element auf der Seite aktualisieren möchten, dessen ID "rsvpmsg" ist.

Und jetzt, wenn ein Benutzer zu einem Abendessen surft, sind sie noch nicht registriert, noch sehen sie einen Link zu RSVP dafür:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

Wenn sie auf den Link "RSVP für dieses Ereignis" klicken, werden Sie einen AJAX-Aufruf an die Register-Aktionsmethode auf dem RSVP-Controller ausführen, und wenn sie abgeschlossen ist, wird eine aktualisierte Meldung wie folgt angezeigt:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

Die Netzwerkbandbreite und der Datenverkehr, die bei diesem AJAX-Aufruf erforderlich sind, sind wirklich leicht. Wenn der Benutzer auf den Link "RSVP für dieses Ereignis" klickt, wird eine kleine HTTP-POST-Netzwerkanforderung an die */Dinners/Register/1-URL* gestellt, die wie unten auf dem Draht aussieht:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

Und die Antwort unserer Register-Aktionsmethode lautet einfach:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Dieser leichte Anruf ist schnell und funktioniert auch über ein langsames Netzwerk.

### <a name="adding-a-jquery-animation"></a>Hinzufügen einer jQuery-Animation

Die von uns implementierte AJAX-Funktionalität funktioniert gut und schnell. Manchmal kann es jedoch so schnell gehen, dass ein Benutzer möglicherweise nicht bemerkt, dass der RSVP-Link durch neuen Text ersetzt wurde. Um das Ergebnis etwas offensichtlicher zu machen, können wir eine einfache Animation hinzufügen, um die Aufmerksamkeit auf die Update-Nachricht zu lenken.

Die Standardvorlage ASP.NET MVC-Projektenthältumfasst umfasst jQuery – eine ausgezeichnete (und sehr beliebte) Open-Source-JavaScript-Bibliothek, die auch von Microsoft unterstützt wird. jQuery bietet eine Reihe von Funktionen, einschließlich einer schönen HTML-DOM-Auswahl und Effektbibliothek.

Um jQuery zu verwenden, fügen wir zuerst einen Skriptverweis hinzu. Da wir jQuery an einer Vielzahl von Stellen innerhalb unserer Website verwenden werden, fügen wir den Skriptverweis in unserer Site.master-Master-Seitendatei hinzu, damit alle Seiten ihn verwenden können.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*Tipp: Stellen Sie sicher, dass Sie den JavaScript-Hotfix intellisense für VS 2008 SP1 installiert haben, der eine umfassendere intellisense-Unterstützung für JavaScript-Dateien (einschließlich jQuery) ermöglicht. Sie können es herunterladen von:http://tinyurl.com/vs2008javascripthotfix*

Code, der mit JQuery geschrieben wurde, verwendet häufig eine globale JavaScript-Methode ,,,,,die ein oder mehrere HTML-Elemente mithilfe eines CSS-Selektors abruft. Zum Beispiel wählt *"#rsvpmsg")* ein beliebiges HTML-Element mit der ID rsvpmsg aus, während *"(".something"* alle Elemente mit dem CSS-Klassennamen "something" auswählen würde. Sie können auch erweiterte Abfragen wie "Alle überprüften Optionsfelder zurückgeben" mit einer Selektorabfrage schreiben, z. B.: *."input[@type@checked=radio][ ]")*.

Nachdem Sie Elemente ausgewählt haben, können Sie Methoden aufrufen, um Maßnahmen zu ergreifen, wie z. B. das Ausblenden von Elementen: *"#rsvpmsg").*

Für unser RSVP-Szenario definieren wir eine einfache JavaScript-Funktion namens "AnimateRSVPMessage", die &lt;&gt; die "rsvpmsg" div auswählt und die Größe des Textinhalts animiert. Der folgende Code startet den Text klein und bewirkt dann, dass er über einen Zeitraum von 400 Millisekunden zunimmt:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Wir können dann diese JavaScript-Funktion verdrahten, die aufgerufen werden soll, nachdem unser AJAX-Aufruf erfolgreich abgeschlossen wurde, indem wir seinen Namen an unsere Ajax.ActionLink()-Hilfsmethode übergeben (über die AjaxOptions "OnSuccess"-Ereigniseigenschaft):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

Und jetzt, wenn auf den Link "RSVP für dieses Ereignis" geklickt wird und unser AJAX-Aufruf erfolgreich abgeschlossen wird, wird die zurückgesendete Inhaltsnachricht animiert und groß werden:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

Zusätzlich zur Bereitstellung eines "OnSuccess"-Ereignisses macht das AjaxOptions-Objekt OnBegin-, OnFailure- und OnComplete-Ereignisse verfügbar, die Sie verarbeiten können (zusammen mit einer Vielzahl anderer Eigenschaften und nützlicher Optionen).

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Bereinigung - Refactor out einer RSVP-Teilansicht

Unsere Detailansichtsvorlage beginnt ein wenig lang zu werden, was Überstunden machen es ein wenig schwieriger zu verstehen. Um die Lesbarkeit des Codes zu verbessern, erstellen wir abschließend eine Teilansicht – RSVPStatus.ascx –, die den gesamten RSVP-Ansichtscode für unsere Detailseite kapselt.

Wir können dies tun, indem Wir mit der rechten Maustaste&gt;auf den Ordner "Views"-Dinners klicken und dann den Menübefehl "Hinzufügen" auswählen. Wir lassen es ein Dinner-Objekt als sein stark typisiertes ViewModel nehmen. Wir können dann die RSVP-Inhalte aus unserer Details.aspx-Ansicht kopieren/einfügen.

Sobald wir dies getan haben, erstellen wir auch eine weitere Teilansicht – EditAndDeleteLinks.ascx –, die unseren Linkansichtscode bearbeiten und löschen kapselt. Wir haben auch ein Dinner-Objekt als sein stark typisiertes ViewModel und kopieren/einfügen der Befolgende Edit and Delete-Logik aus unserer Details.aspx-Ansicht.

Unsere Detailansichtsvorlage kann dann nur zwei Html.RenderPartial()-Methodenaufrufe unten enthalten:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

Dadurch wird der Code sauberer zu lesen und zu verwalten.

### <a name="next-step"></a>Nächster Schritt

Sehen wir uns nun an, wie wir AJAX noch weiter nutzen können, und fügen Sie unserer Anwendung interaktive Mapping-Unterstützung hinzu.

> [!div class="step-by-step"]
> [Zurück](secure-applications-using-authentication-and-authorization.md)
> [Weiter](use-ajax-to-implement-mapping-scenarios.md)
