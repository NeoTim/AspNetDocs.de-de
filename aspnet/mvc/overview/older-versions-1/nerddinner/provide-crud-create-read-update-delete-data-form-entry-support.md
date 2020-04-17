---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (Erstellen, Lesen, Aktualisieren, Löschen) Unterstützung für Datenformulareinträge bereitstellen | Microsoft Docs
author: rick-anderson
description: Schritt 5 zeigt, wie Sie unsere DinnersController-Klasse weiter führen, indem Sie auch die Unterstützung für das Bearbeiten, Erstellen und Löschen von Dinners mit ihm aktivieren.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542624"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>Bereitstellen von CRUD-Unterstützung (Create, Read, Update, Delete) für Datenformulareinträge

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 5 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 5 zeigt, wie Sie unsere DinnersController-Klasse weiter führen, indem Sie auch die Unterstützung für das Bearbeiten, Erstellen und Löschen von Dinners mit ihm aktivieren.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner Schritt 5: Erstellen, Aktualisieren, Löschen von Formularszenarien

Wir haben Controller und Ansichten eingeführt und erläutert, wie sie verwendet werden können, um eine Auflistung/Details für Abendessen vor Ort zu implementieren. Unser nächster Schritt wird sein, unsere DinnersController-Klasse weiter zu bringen und auch Unterstützung für das Bearbeiten, Erstellen und Löschen von Dinners mit ihm zu ermöglichen.

### <a name="urls-handled-by-dinnerscontroller"></a>URLs, die von DinnersController verarbeitet werden

Wir haben zuvor Aktionsmethoden zu DinnersController hinzugefügt, die Unterstützung für zwei URLs implementiert haben: */Dinners* und */Dinners/Details/[id]*.

| **URL** | **Verb** | **Zweck** |
| --- | --- | --- |
| */Abendessen/* | GET | Zeigen Sie eine HTML-Liste der bevorstehenden Abendessen an. |
| */Dinners/Details/[id]* | GET | Zeigen Sie Details zu einem bestimmten Abendessen an. |

Wir werden nun Aktionsmethoden hinzufügen, um drei zusätzliche URLs zu implementieren: */Dinners/Edit/[id]*, */Dinners/Create*und */Dinners/Delete/[id]*. Diese URLs ermöglichen die Unterstützung für die Bearbeitung vorhandener Abendessen, das Erstellen neuer Abendessen und das Löschen von Abendessen.

Wir unterstützen sowohl HTTP GET- als auch HTTP POST-Verbinteraktionen mit diesen neuen URLs. HTTP GET-Anforderungen an diese URLs zeigen die ursprüngliche HTML-Ansicht der Daten an (ein Formular, das bei "Bearbeiten" mit den Dinner-Daten gefüllt wird), ein leeres Formular im Fall von "erstellen" und ein Bestätigungsbildschirm zum Löschen im Fall von "Löschen"). HTTP-POST-Anforderungen an diese URLs speichern/aktualisieren/löschen die Dinner-Daten in unserem DinnerRepository (und von dort in die Datenbank).

| **URL** | **Verb** | **Zweck** |
| --- | --- | --- |
| */Dinners/Bearbeiten/[id]* | GET | Zeigt ein bearbeitbares HTML-Formular mit Dinner-Daten an. |
| POST | Speichern Sie die Formularänderungen für ein bestimmtes Abendessen in der Datenbank. |
| */Dinners/Erstellen* | GET | Zeigen Sie ein leeres HTML-Formular an, mit dem Benutzer neue Abendessen definieren können. |
| POST | Erstellen Sie ein neues Dinner, und speichern Sie es in der Datenbank. |
| */Dinners/Löschen/[id]* | GET | Bestätigungsbildschirm löschen anzeigen. |
| POST | Löscht das angegebene Abendessen aus der Datenbank. |

### <a name="edit-support"></a>Edit-Support

Beginnen wir mit der Implementierung des "Bearbeiten"-Szenarios.

#### <a name="the-http-get-edit-action-method"></a>Die HTTP-GET Edit Action-Methode

Wir beginnen mit der Implementierung des HTTP -"GET"-Verhaltens unserer Edit-Aktionsmethode. Diese Methode wird aufgerufen, wenn die *URL /Dinners/Edit/[id]* angefordert wird. Unsere Implementierung sieht wie folgt aus:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

Der obige Code verwendet das DinnerRepository, um ein Dinner-Objekt abzurufen. Anschließend wird eine Ansichtsvorlage mit dem Dinner-Objekt gerendert. Da wir keinen Vorlagennamen nicht explizit an die *View()-Hilfsmethode* übergeben haben, wird der konventionsbasierte Standardpfad verwendet, um die Ansichtsvorlage aufzulösen: /Views/Dinners/Edit.aspx.

Lassen Sie uns nun diese Ansichtsvorlage erstellen. Wir tun dies, indem wir mit der rechten Maustaste in die Edit-Methode klicken und den Kontextmenübefehl "Ansicht hinzufügen" auswählen:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

Im Dialogfeld "Ansicht hinzufügen" geben wir an, dass wir ein Dinner-Objekt als Modell an unsere Ansichtsvorlage übergeben und eine "Bearbeiten"-Vorlage automatisch erstellen:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, fügt Visual Studio eine neue Ansichtsvorlagedatei "Edit.aspx" für uns im Verzeichnis "-Ansichten-Dinners" hinzu. Außerdem wird die neue Ansichtsvorlage "Edit.aspx" im Code-Editor geöffnet – gefüllt mit einer anfänglichen "Edit"-Gerüstimplementierung wie folgt:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Lassen Sie uns einige Änderungen am standardmäßigen "Bearbeiten"-Gerüst vornehmen, das generiert wurde, und die Vorlage für die Bearbeitungsansicht aktualisieren, um den Inhalt unten zu erhalten (wodurch einige der Eigenschaften entfernt werden, die wir nicht verfügbar machen möchten):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Wenn wir die Anwendung ausführen und die *URL "/Dinners/Edit/1"* anfordern, sehen wir die folgende Seite:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

Das HTML-Markup, das von unserer Ansicht generiert wird, sieht wie folgt aus. Es ist Standard-HTML &lt;&gt; – mit einem Formularelement, das einen HTTP-POST zur */Dinners/Edit/1-URL* ausführt, wenn die Schaltfläche "Speichern" &lt;Eingabetyp="senden"/&gt; gedrückt wird. Für &lt;jede bearbeitbare Eigenschaft&gt; wurde ein HTML-Eingabetyp="text"/ element ausgegeben:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() und Html.TextBox() Html-Hilfsmethoden

Unsere Ansichtsvorlage "Edit.aspx" verwendet mehrere "Html Helper"-Methoden: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox() und Html.ValidationMessage(). Diese Hilfsmethoden sorgen nicht nur für die Generierung von HTML-Markup für uns, sondern bieten auch integrierte Unterstützung bei der Fehlerbehandlung und -validierung.

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() Hilfsmethode

Die Html.BeginForm()-Hilfsmethode ist die &lt;&gt; Ausgabe des HTML-Formularelements in unserem Markup. In unserer Ansichtsvorlage Edit.aspx werden Sie feststellen, dass wir bei verwendungdieser Methode eine C-Anweisung "using" anwenden. Die offene geschweifte Klammer &lt;&gt; gibt den Anfang des Formularinhalts an, und &lt;die&gt; schließende geschweifte Klammer gibt das Ende des /form-Elements an:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Wenn Sie den "using"-Anweisungsansatz für ein Szenario wie dieses als unnatürlich empfinden, können Sie alternativ eine Html.BeginForm() und Html.EndForm()-Kombination verwenden (die dasselbe tut):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Wenn Html.BeginForm() ohne Parameter aufgerufen wird, wird ein Formularelement ausgegeben, das einen HTTP-POST-Eintrag an die URL der aktuellen Anforderung ausführt. Aus diesem Grund generiert unsere Bearbeitungsansicht ein * &lt;Formularaktion="/Dinners/Edit/1"&gt; method="post"-Element.* Wir hätten alternativ explizite Parameter an Html.BeginForm() übergeben können, wenn wir auf eine andere URL posten möchten.

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() Hilfsmethode

Unsere Edit.aspx-Ansicht verwendet die Html.TextBox()-Hilfsmethode, um &lt;&gt; Eingabetyp="text"/ Elemente auszugeben:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

Die obige Html.TextBox()-Methode verwendet einen einzelnen Parameter, der verwendet wird, &lt;um sowohl die&gt; id/name-Attribute des ausgabegemäßen Eingabetyps="text"/-Elements als auch die Modelleigenschaft zum Auffüllen des Textfeldwerts anzugeben. Beispielsweise hatte das Dinner-Objekt, das wir an die Edit-Ansicht übergeben haben, den Eigenschaftswert "Title" von ".NET Futures", und so ruft unsere Html.TextBox("Title")-Methode die Ausgabe auf: * &lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.

Alternativ können wir den ersten Html.TextBox()-Parameter verwenden, um die id/den Namen des Elements anzugeben, und dann den Wert explizit übergeben, der als zweiter Parameter verwendet werden soll:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Häufig möchten wir benutzerdefinierte Formatierungen für den ausgegebenen Wert durchführen. Die in .NET integrierte statische String.Format()-Methode ist für diese Szenarien nützlich. Unsere Ansichtsvorlage Edit.aspx verwendet diese Option, um den EventDate-Wert (der vom Typ DateTime ist) so zu formatieren, dass er keine Sekunden für die Zeit anzeigt:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Ein dritter Parameter für Html.TextBox() kann optional verwendet werden, um zusätzliche HTML-Attribute auszugeben. Der Codeausschnitt unten veranschaulicht, wie ein zusätzliches size="30"-Attribut und ein class="mycssclass"-Attribut für das &lt;Eingabetyp="text"/&gt; -Element gerendert wird. Beachten Sie, dass wir dem Namen des Klassenattributs mithilfe einer "Klasse"@" character because "entkommen, ist ein reserviertes Schlüsselwort in C':

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>Implementieren der HTTP-POST-Edit-Aktionsmethode

Wir haben jetzt die HTTP-GET-Version unserer Edit-Aktionsmethode implementiert. Wenn ein Benutzer die */Dinners/Edit/1-URL* anfordert, erhält er eine HTML-Seite wie die folgende:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

Wenn Sie die Schaltfläche "Speichern" drücken, wird ein Formularbeitrag an die &lt; */Dinners/Edit/1-URL* veröffentlicht und die HTML-Eingabeformularwerte&gt; mit dem VERB HTTP POST übermittelt. Implementieren wir nun das HTTP-POST-Verhalten unserer Edit-Action-Methode, mit der das Speichern des Dinners behandelt wird.

Zunächst fügen wir unserem DinnersController eine überladene Aktionsmethode "Bearbeiten" hinzu, auf der ein Attribut "AcceptVerbs" enthalten ist, das angibt, dass http POST-Szenarien verarbeitet werden:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

Wenn das Attribut [AcceptVerbs] auf überladene Aktionsmethoden angewendet wird, verarbeitet ASP.NET MVC automatisch das Senden von Anforderungen an die entsprechende Aktionsmethode, abhängig vom eingehenden HTTP-Verb. HTTP-POST-Anforderungen an */Dinners/Edit/[id]-URLs* gehen an die obige Edit-Methode, während alle anderen HTTP-Verbanforderungen an */Dinners/Edit/[id]-URLs* an die erste edit-Methode gehen, die wir implementiert haben (die kein `[AcceptVerbs]` Attribut hatte).

| **Side Topic: Warum über HTTP-Verben unterscheiden?** |
| --- |
| Sie könnten fragen – warum verwenden wir eine einzelne URL und differenzieren sein Verhalten über das HTTP-Verb? Warum nicht einfach zwei separate URLs haben, um das Laden und Speichern von Bearbeitungsänderungen zu handhaben? Beispiel: /Dinners/Edit/[id], um das Anfangsformular anzuzeigen, und /Dinners/Save/[id], um den Formularbeitrag zu behandeln, um ihn zu speichern? Der Nachteil beim Veröffentlichen von zwei separaten URLs ist, dass in Fällen, in denen wir auf /Dinners/Save/2 posten und dann das HTML-Formular aufgrund eines Eingabefehlers erneut anzeigen müssen, der Endbenutzer am Ende die /Dinners/Save/2-URL in der Adressleiste seines Browsers hat (da dies die URL war, auf die das Formular gesendet wurde). Wenn der Endbenutzer diese erneut angezeigte Seite in seine Browser-Favoritenliste markiert oder die URL kopiert/eingefügt und an einen Freund per E-Mail anlegt, wird am Ende eine URL gespeichert, die in Zukunft nicht mehr funktioniert (da diese URL von Beitragswerten abhängt). Durch das Aufzeigen einer einzelnen URL (z. B. /Dinners/Edit/[id]) und die Differenzierung der Verarbeitung durch das HTTP-Verb ist es für Endbenutzer sicher, die Bearbeitungsseite als Lesezeichen zu markieren und/oder die URL an andere zu senden. |

#### <a name="retrieving-form-post-values"></a>Abrufen von Formularpostwerten

Es gibt eine Vielzahl von Möglichkeiten, wie wir auf veröffentlichte Formularparameter innerhalb unserer HTTP POST "Edit"-Methode zugreifen können. Ein einfacher Ansatz besteht darin, einfach die Request-Eigenschaft in der Controller-Basisklasse zu verwenden, um auf die Formularauflistung zuzugreifen und die gebuchten Werte direkt abzurufen:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

Der obige Ansatz ist jedoch etwas ausführlich, vor allem, wenn wir Fehlerbehandlungslogik hinzufügen.

Ein besserer Ansatz für dieses Szenario besteht darin, die integrierte *UpdateModel()-Hilfsmethode* in der Controller-Basisklasse zu nutzen. Es unterstützt das Aktualisieren der Eigenschaften eines Objekts, das wir mit den eingehenden Formularparametern übergeben. Es verwendet Reflektion, um die Eigenschaftsnamen für das Objekt zu bestimmen, und konvertiert und weist ihnen dann automatisch Werte basierend auf den Eingabewerten zu, die vom Client übermittelt werden.

Wir könnten die UpdateModel()-Methode verwenden, um unsere HTTP-POST-Edit-Aktion mithilfe dieses Codes zu vereinfachen:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Wir können jetzt die */Dinners/Edit/1* URL besuchen und den Titel unseres Dinners ändern:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

Wenn wir auf die Schaltfläche "Speichern" klicken, führen wir einen Formularbeitrag für unsere Edit-Aktion aus, und die aktualisierten Werte werden in der Datenbank beibehalten. Wir werden dann zur Details-URL für das Dinner weitergeleitet (die die neu gespeicherten Werte anzeigt):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Behandeln von Bearbeitungsfehlern

Unsere aktuelle HTTP-POST-Implementierung funktioniert einwandfrei – außer wenn Fehler auftreten.

Wenn ein Benutzer beim Bearbeiten eines Formulars einen Fehler macht, müssen wir sicherstellen, dass das Formular mit einer informativen Fehlermeldung erneut angezeigt wird, die ihn zur Behebung des Formulars führt. Dies schließt Fälle ein, in denen ein Endbenutzer falsche Eingaben zuschreibt (z. B. eine fehlerhafte Datumszeichenfolge), sowie Fälle, in denen das Eingabeformat gültig ist, aber ein Verstoß gegen die Geschäftsregel vorliegt. Wenn Fehler auftreten, sollte das Formular die Eingabedaten beibehalten, die der Benutzer ursprünglich eingegeben hat, damit er seine Änderungen nicht manuell auffüllen muss. Dieser Vorgang sollte so oft wie nötig wiederholt werden, bis das Formular erfolgreich abgeschlossen ist.

ASP.NET MVC enthält einige nette integrierte Funktionen, die die Fehlerbehandlung und Formularneuanzeige vereinfachen. Um diese Features in Aktion zu sehen, aktualisieren wir unsere Edit-Aktionsmethode mit dem folgenden Code:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

Der obige Code ähnelt unserer vorherigen Implementierung – mit der Ausnahme, dass wir jetzt einen Try/Catch-Fehlerbehandlungsblock um unsere Arbeit wickeln. Wenn eine Ausnahme beim Aufrufen von UpdateModel() auftritt oder wenn wir versuchen, das DinnerRepository zu speichern (was eine Ausnahme auslöst, wenn das Dinner-Objekt, das wir speichern möchten, aufgrund einer Regelverletzung in unserem Modell ungültig ist), wird unser catch-Fehlerbehandlungsblock ausgeführt. Innerhalb davon werden alle Regelverstöße, die im Dinner-Objekt vorhanden sind, durchlaufen und zu einem ModelState-Objekt hinzufügen (das wir in Kürze besprechen werden). Wir zeigen dann die Ansicht erneut an.

Um diese Funktionsweise zu sehen, lassen Sie uns die Anwendung erneut ausführen, ein Dinner bearbeiten und es in einen leeren Titel, ein EventDate von "BOGUS" ändern, und verwenden Sie eine britische Telefonnummer mit dem Länderwert USA. Wenn wir die Schaltfläche "Speichern" drücken, kann unsere HTTP POST Edit-Methode das Dinner nicht speichern (weil Fehler auftreten) und zeigt das Formular erneut an:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Unsere Anwendung hat eine anständige Fehlererfahrung. Die Textelemente mit der ungültigen Eingabe werden rot hervorgehoben, und dem Endbenutzer werden validierungsfehlermeldungen angezeigt. Das Formular bewahrt auch die Eingabedaten, die der Benutzer ursprünglich eingegeben hat – so dass sie nichts nachfüllen müssen.

Wie, könnten Sie fragen, ist das geschehen? Wie haben sich die Textfelder Titel, EventDate und ContactPhone rot hervorgehoben und wissen, die ursprünglich eingegebenen Benutzerwerte auszugeben? Und wie wurden Fehlermeldungen in der Liste oben angezeigt? Die gute Nachricht ist, dass dies nicht von Zauberei geschehen ist - sondern weil wir einige der integrierten ASP.NET MVC-Funktionen verwendet haben, die Eingabevalidierung und Fehlerbehandlung Szenarien einfach machen.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>Verstehen von ModelState und den Validierungs-HTML-Hilfsmethoden

Controllerklassen verfügen über eine "ModelState"-Eigenschaftenauflistung, die eine Möglichkeit bietet, anzuzeigen, dass Fehler vorhanden sind, wenn ein Modellobjekt an eine Ansicht übergeben wird. Fehlereinträge in der ModelState-Auflistung identifizieren den Namen der Modelleigenschaft mit dem Problem (z. B. "Title", "EventDate" oder "ContactPhone") und ermöglichen die Angabe einer benutzerfreundlichen Fehlermeldung (z. B. "Titel ist erforderlich").

Die *UpdateModel()-Hilfsmethode* füllt die ModelState-Auflistung automatisch auf, wenn Fehler auftreten, während versucht wird, Formularwerte Eigenschaften im Modellobjekt zuzuweisen. Die EventDate-Eigenschaft unseres Dinner-Objekts ist beispielsweise vom Typ DateTime. Wenn die UpdateModel()-Methode im obigen Szenario nicht in der Lage war, ihr den Zeichenfolgenwert "BOGUS" zuzuweisen, fügte die UpdateModel()-Methode der ModelState-Auflistung einen Eintrag hinzu, der angibt, dass ein Zuweisungsfehler mit dieser Eigenschaft aufgetreten ist.

Entwickler können auch Code schreiben, um explizit Fehlereinträge in die ModelState-Auflistung hinzuzufügen, wie wir es unten in unserem "catch"-Fehlerbehandlungsblock tun, der die ModelState-Auflistung mit Einträgen auffüllt, die auf den aktiven Regelverletzungen im Dinner-Objekt basieren:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Html-Hilfsintegration mit ModelState

HTML-Hilfsmethoden - wie Html.TextBox() - überprüfen die ModelState-Auflistung beim Rendern der Ausgabe. Wenn ein Fehler für das Element vorliegt, rendern sie den vom Benutzer eingegebenen Wert und eine CSS-Fehlerklasse.

In unserer "Bearbeiten"-Ansicht verwenden wir beispielsweise die Html.TextBox()-Hilfsmethode, um das EventDate unseres Dinner-Objekts zu rendern:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Wenn die Ansicht im Fehlerszenario gerendert wurde, überprüfte die Html.TextBox()-Methode die ModelState-Auflistung, um festzustellen, ob Fehler im Zusammenhang mit der "EventDate"-Eigenschaft unseres Dinner-Objekts aufgetreten sind. Wenn festgestellt wurde, dass ein Fehler vorliegt, wurde die übermittelte Benutzereingabe ("BOGUS") &lt;als Wert gerendert&gt; und dem generierten Eingabetyp="textbox"/ Markup eine css-Fehlerklasse hinzugefügt:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

Sie können die Darstellung der css-Fehlerklasse so anpassen, dass sie nach Bewilliken aussieht. Die standardmäßige CSS-Fehlerklasse – "input-validation-error" – ist im Stylesheet *"content-site.css"* definiert und sieht wie folgt aus:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Diese CSS-Regel hat dazu geführt, dass unsere ungültigen Eingabeelemente wie folgt hervorgehoben wurden:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() Hilfsmethode

Die Html.ValidationMessage()-Hilfsmethode kann verwendet werden, um die ModelState-Fehlermeldung auszugeben, die einer bestimmten Modelleigenschaft zugeordnet ist:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

Die oben genannten Code-Ausgaben: * &lt;span class="field-validation-error"&gt; Der&lt;Wert 'BOGUS' ist ungültig /span&gt;*

Die Html.ValidationMessage()-Hilfsmethode unterstützt auch einen zweiten Parameter, mit dem Entwickler die angezeigte Fehlermeldung überschreiben können:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

Die obigen Codeausgaben: * &lt;span class="field-validation-error"&gt;\*&lt;/span&gt; * anstelle des Standardfehlertexts, wenn ein Fehler für die EventDate-Eigenschaft vorhanden ist.

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() Hilfsmethode

Die Html.ValidationSummary()-Hilfsmethode kann verwendet werden, um eine &lt;zusammenfassungsgenaue&gt;&lt;Fehlermeldung&gt; zu rendern, die von einer ul&gt;&lt;li/ /ul-Liste aller detaillierten Fehlermeldungen in der ModelState-Auflistung begleitet wird:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Die Html.ValidationSummary()-Hilfsmethode verwendet einen optionalen Zeichenfolgenparameter, der eine zusammenfassungsgenaue Fehlermeldung definiert, die über der Liste der detaillierten Fehler angezeigt wird:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

Sie können optional CSS verwenden, um zu überschreiben, wie die Fehlerliste aussieht.

#### <a name="using-a-addruleviolations-helper-method"></a>Verwenden einer AddRuleViolations-Hilfsmethode

Unsere anfängliche HTTP-POST Edit-Implementierung verwendete eine foreach-Anweisung innerhalb des catch-Blocks, um die Regelverletzungen des Dinner-Objekts zu durchlaufen und sie der ModelState-Auflistung des Controllers hinzuzufügen:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Wir können diesen Code ein wenig sauberer machen, indem wir dem NerdDinner-Projekt eine "ControllerHelpers"-Klasse hinzufügen und eine "AddRuleViolations"-Erweiterungsmethode implementieren, die der ASP.NET MVC ModelStateDictionary-Klasse eine Hilfsmethode hinzufügt. Diese Erweiterungsmethode kann die Logik kapseln, die zum Auffüllen des ModelStateDictionary mit einer Liste von RuleViolation-Fehlern erforderlich ist:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Wir können dann unsere HTTP-POST Edit-Aktionsmethode aktualisieren, um diese Erweiterungsmethode zu verwenden, um die ModelState-Auflistung mit unseren Dinner Rule Violations aufzufüllen.

#### <a name="complete-edit-action-method-implementations"></a>Vollständige Implementierung von Edit Action-Methoden

Der folgende Code implementiert die gesamte Controllerlogik, die für unser Edit-Szenario erforderlich ist:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

Das Schöne an unserer Edit-Implementierung ist, dass weder unsere Controller-Klasse noch unsere View-Vorlage etwas über die spezifischen Validierungs- oder Geschäftsregeln wissen müssen, die von unserem Dinner-Modell erzwungen werden. Wir können unserem Modell in Zukunft zusätzliche Regeln hinzufügen und müssen keine Codeänderungen an unserem Controller oder unserer Ansicht vornehmen, damit sie unterstützt werden können. Dies gibt uns die Flexibilität, unsere Anwendungsanforderungen in Zukunft mit einem Minimum an Codeänderungen einfach weiterzuentwickeln.

### <a name="create-support"></a>Erstellen von Support

Wir haben die Implementierung des "Edit"-Verhaltens unserer DinnersController-Klasse abgeschlossen. Lassen Sie uns nun fortfahren, um die "Create"-Unterstützung darauf zu implementieren – die es Benutzern ermöglicht, neue Dinnerhinzuzufügen hinzuzufügen.

#### <a name="the-http-get-create-action-method"></a>Die HTTP-GET Create Action-Methode

Wir beginnen mit der Implementierung des HTTP -"GET"-Verhaltens unserer Create-Aktionsmethode. Diese Methode wird aufgerufen, wenn jemand die */Dinners/Create* URL besucht. Unsere Implementierung sieht aus wie folgt:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

Der obige Code erstellt ein neues Dinner-Objekt und weist seine EventDate-Eigenschaft einer zukünftigen Woche zu. Anschließend wird eine Ansicht gerendert, die auf dem neuen Dinner-Objekt basiert. Da wir keinen Namen explizit an die *View()-Hilfsmethode* übergeben haben, wird der konventionsbasierte Standardpfad verwendet, um die Ansichtsvorlage aufzulösen: /Views/Dinners/Create.aspx.

Lassen Sie uns nun diese Ansichtsvorlage erstellen. Wir können dies tun, indem Wir mit der rechten Maustaste in die Aktionsmethode Erstellen klicken und den Kontextmenübefehl "Ansicht hinzufügen" auswählen. Im Dialogfeld "Ansicht hinzufügen" geben wir an, dass wir ein Dinner-Objekt an die Ansichtsvorlage übergeben, und wählen eine "Create"-Vorlage automatisch aufgerüst:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, speichert Visual Studio eine neue gerüstbasierte "Create.aspx"-Ansicht im Verzeichnis "-Views-Dinners" und öffnet sie in der IDE:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Lassen Sie uns einige Änderungen an der Standard-Gerüstdatei "erstellen" vornehmen, die für uns generiert wurde, und ändern Sie sie so, dass sie wie folgt aussieht:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

Und jetzt, wenn wir unsere Anwendung ausführen und auf die *"/Dinners/Create"-URL* im Browser zugreifen, wird die Benutzeroberfläche wie unten aus unserer Create Action-Implementierung gerendert:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>Implementieren der HTTP-POST-Erstellungsaktionsmethode

Wir haben die HTTP-GET-Version unserer Create-Aktionsmethode implementiert. Wenn ein Benutzer auf die Schaltfläche "Speichern" klickt, führt er einen Formularbeitrag &lt;an&gt; die *URL /Dinners/Create* aus und sendet die HTML-Eingabeformularwerte mit dem VERB HTTP POST.

Implementieren wir nun das HTTP-POST-Verhalten unserer Create-Aktionsmethode. Zunächst fügen wir unserem DinnersController eine überladene Aktionsmethode "Create" hinzu, auf der ein Attribut "AcceptVerbs" enthalten ist, das angibt, dass http POST-Szenarien verarbeitet werden:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

Es gibt eine Vielzahl von Möglichkeiten, wie wir auf die gebuchten Formularparameter in unserer HTTP-POST-fähigen "Create"-Methode zugreifen können.

Ein Ansatz besteht darin, ein neues Dinner-Objekt zu erstellen und dann die *UpdateModel()-Hilfsmethode* (wie bei der Edit-Aktion) zu verwenden, um es mit den gebuchten Formularwerten aufzufüllen. Wir können es dann zu unserem DinnerRepository hinzufügen, es in der Datenbank beibehalten und den Benutzer zu unserer Detail-Aktion umleiten, um das neu erstellte Dinner mit dem folgenden Code anzuzeigen:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternativ können wir einen Ansatz verwenden, bei dem unsere Create()-Aktionsmethode ein Dinner-Objekt als Methodenparameter verwenden kann. ASP.NET MVC instanziiert dann automatisch ein neues Dinner-Objekt für uns, füllt seine Eigenschaften mithilfe der Formulareingaben auf und übergibt es an unsere Aktionsmethode:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Unsere oben beschriebene Aktionsmethode überprüft, ob das Dinner-Objekt erfolgreich mit den Formularpostwerten aufgefüllt wurde, indem die ModelState.IsValid-Eigenschaft überprüft wird. Dies gibt false zurück, wenn Eingabekonvertierungsprobleme auftreten (z. B. eine Zeichenfolge von "BOGUS" für die EventDate-Eigenschaft), und wenn es Probleme gibt, zeigt unsere Aktionsmethode das Formular erneut an.

Wenn die Eingabewerte gültig sind, versucht die Aktionsmethode, das neue Dinner zum DinnerRepository hinzuzufügen und zu speichern. Es umschließt diese Arbeit innerhalb eines try/catch-Blocks und zeigt das Formular erneut an, wenn es Verstöße gegen Geschäftsregeln gibt (was dazu führen würde, dass die dinnerRepository.Save()-Methode eine Ausnahme auslöst).

Um dieses Fehlerbehandlungsverhalten in Aktion zu sehen, können wir die */Dinners/Create* URL anfordern und Details zu einem neuen Dinner ausfüllen. Falsche Eingaben oder Werte führen dazu, dass das Erstellungsformular mit den unten hervorgehobenen Fehlern erneut angezeigt wird:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Beachten Sie, dass in unserem Formular Erstellen genau die gleichen Validierungs- und Geschäftsregeln wie unser Formular Bearbeiten berücksichtigt werden. Dies liegt daran, dass unsere Validierungs- und Geschäftsregeln im Modell definiert und nicht in die Benutzeroberfläche oder den Controller der Anwendung eingebettet wurden. Dies bedeutet, dass wir später unsere Validierungs- oder Geschäftsregeln an einem einzigen Ort ändern/weiterentwickeln und sie in unserer gesamten Anwendung anwenden lassen können. Wir müssen weder innerhalb unserer Aktionsmethoden Bearbeiten oder Erstellen Code ändern, um neue Regeln oder Änderungen an bestehenden regeln automatisch zu berücksichtigen.

Wenn wir die Eingabewerte korrigieren und erneut auf die Schaltfläche "Speichern" klicken, wird unser Zusatz zum DinnerRepository erfolgreich sein, und ein neues Dinner wird der Datenbank hinzugefügt. Wir werden dann zur *URL /Dinners/Details/[id]* weitergeleitet– wo uns Details zum neu geschaffenen Dinner präsentiert werden:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Unterstützung löschen

Fügen wir nun "Löschen"-Unterstützung zu unserem DinnersController hinzu.

#### <a name="the-http-get-delete-action-method"></a>Die HTTP-GET-Löschaktionsmethode

Wir beginnen mit der Implementierung des HTTP GET-Verhaltens unserer Delete-Aktionsmethode. Diese Methode wird aufgerufen, wenn jemand die */Dinners/Delete/[id]* URL besucht. Im Folgenden finden Sie die Implementierung:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

Die Aktionsmethode versucht, das zu löschende Dinner abzurufen. Wenn das Dinner vorhanden ist, wird eine Ansicht basierend auf dem Dinner-Objekt gerendert. Wenn das Objekt nicht vorhanden ist (oder bereits gelöscht wurde), gibt es eine Ansicht zurück, die die Ansichtsvorlage "NotFound" rendert, die wir zuvor für unsere Aktionsmethode "Details" erstellt haben.

Wir können die Ansichtsvorlage "Löschen" erstellen, indem wir mit der rechten Maustaste in die Aktionsmethode Löschen klicken und den Kontextmenübefehl "Ansicht hinzufügen" auswählen. Im Dialogfeld "Ansicht hinzufügen" geben wir an, dass wir ein Dinner-Objekt als Modell an unsere Ansichtsvorlage übergeben und eine leere Vorlage erstellen:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

Wenn wir auf die Schaltfläche "Hinzufügen" klicken, fügt Visual Studio eine neue Ansichtsvorlagedatei "Delete.aspx" für uns in unserem Verzeichnis "-Ansichten-Dinners" hinzu. Wir fügen der Vorlage HTML und Code hinzu, um einen Löschbestätigungsbildschirm wie folgt zu implementieren:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

Der obige Code zeigt den Titel des zu &lt;löschenden Dinners an und gibt ein Formularelement&gt; aus, das einen POST-Test an die URL /Dinners/Delete/[id] ausführt, wenn der Endbenutzer auf die Schaltfläche "Löschen" klickt.

Wenn wir unsere Anwendung ausführen und auf die *URL "/Dinners/Delete/[id]"* für ein gültiges Dinner-Objekt zugreifen, rendert es die Benutzeroberfläche wie folgt:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Nebenthema: Warum machen wir einen POST-Test?** |
| --- |
| Sie fragen sich vielleicht – warum haben &lt;wir&gt; uns bemüht, ein Formular in unserem Bildschirm "Bestätigung löschen" zu erstellen? Warum verwenden Sie nicht einfach einen Standard-Hyperlink, um eine Verknüpfung mit einer Aktionsmethode herzustellen, die den eigentlichen Löschvorgang ausführt? Der Grund dafür ist, dass wir vorsichtig sein wollen, um vor Web-Crawlern und Suchmaschinen zu schützen, die unsere URLs entdecken und versehentlich dazu führen, dass Daten gelöscht werden, wenn sie den Links folgen. HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones. Eine gute Regel besteht darin, sicherzustellen, dass Sie immer destruktive oder Datenänderungsvorgänge hinter HTTP-POST-Anforderungen setzen. |

#### <a name="implementing-the-http-post-delete-action-method"></a>Implementieren der HTTP-POST-Aktion delete

Wir haben jetzt die HTTP-GET-Version unserer Delete-Aktionsmethode implementiert, die einen Löschbestätigungsbildschirm anzeigt. Wenn ein Endbenutzer auf die Schaltfläche "Löschen" klickt, führt er einen Formularbeitrag zur *URL /Dinners/Dinner/[id]* aus.

Implementieren wir nun das HTTP-"POST"-Verhalten der Delete-Aktionsmethode mithilfe des folgenden Codes:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Die HTTP-POST-Version unserer Delete-Aktionsmethode versucht, das zu löschende Dinner-Objekt abzurufen. Wenn es nicht gefunden werden kann (weil es bereits gelöscht wurde), wird unsere "NotFound"-Vorlage gerendert. Wenn das Dinner gefunden wird, wird es aus dem DinnerRepository gelöscht. Anschließend wird eine "Gelöschte" Vorlage gerendert.

Um die Vorlage "Gelöscht" zu implementieren, klicken wir mit der rechten Maustaste in die Aktionsmethode und wählen das Kontextmenü "Ansicht hinzufügen". Wir nennen unsere Ansicht "Gelöscht" und lassen sie eine leere Vorlage sein (und nehmen kein stark typisiertes Modellobjekt). Anschließend fügen wir einige HTML-Inhalte hinzu:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

Und jetzt, wenn wir unsere Anwendung ausführen und auf die *"/Dinners/Delete/[id]"* URL für ein gültiges Dinner-Objekt zugreifen, wird unser Dinner-Löschbestätigungsbildschirm wie folgt gerendert:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

Wenn wir auf die Schaltfläche "Löschen" klicken, führt sie einen HTTP-POST zur *URL /Dinners/Delete/[id]* aus, die das Dinner aus unserer Datenbank löscht und unsere Ansichtsvorlage "Gelöscht" anzeigt:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Modellbindungssicherheit

Wir haben zwei verschiedene Möglichkeiten zur Verwendung der integrierten Modellbindungsfunktionen von ASP.NET MVC erörtert. Die erste, die die UpdateModel()-Methode zum Aktualisieren von Eigenschaften für ein vorhandenes Modellobjekt verwendet, und die zweite, die die Unterstützung von ASP.NET MVC für das Übergeben von Modellobjekten als Aktionsmethodenparameter verwendet. Beide Techniken sind sehr leistungsstark und äußerst nützlich.

Diese Macht bringt auch Verantwortung mit sich. Es ist wichtig, bei der Annahme von Benutzereingaben immer paranoid in Bezug auf die Sicherheit zu sein, und dies gilt auch, wenn Objekte an die Formulareingabe binden. Sie sollten darauf achten, immer HTML-Codierung aller vom Benutzer eingegebenen Werte zu verwenden, um HTML- und JavaScript-Injektionsangriffe zu vermeiden, und vorsicht sorgsam bei SQL-Injektionsangriffen (Hinweis: Wir verwenden LINQ to SQL für unsere Anwendung, die automatisch Parameter kodiert, um diese Art von Angriffen zu verhindern). Sie sollten sich niemals allein auf die clientseitige Validierung verlassen und immer eine serverseitige Validierung einsetzen, um sich vor Hackern zu schützen, die versuchen, Ihnen gefälschte Werte zu senden.

Ein zusätzliches Sicherheitselement, um sicherzustellen, dass Sie bei der Verwendung der Bindungsfeatures von ASP.NET MVC nachdenken, ist der Bereich der Objekte, die Sie binden. Insbesondere möchten Sie sicherstellen, dass Sie die Sicherheitsauswirkungen der Eigenschaften verstehen, die Sie gebunden werden lassen, und sicherstellen, dass nur die Eigenschaften aktualisiert werden, die wirklich von einem Endbenutzer aktualisiert werden sollten.

Standardmäßig versucht die UpdateModel()-Methode, alle Eigenschaften des Modellobjekts zu aktualisieren, die den Parameterwerten eingehender Formularwerte entsprechen. Ebenso können Objekte, die als Aktionsmethodenparameter übergeben werden, standardmäßig auch alle ihre Eigenschaften über Formularparameter festlegen.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Sperrung der Bindung auf Nutzungsbasis

Sie können die Bindungsrichtlinie pro Verwendung sperren, indem Sie eine explizite "Includeliste" von Eigenschaften bereitstellen, die aktualisiert werden können. Dies kann durch Übergeben eines zusätzlichen String-Array-Parameters an die UpdateModel()-Methode wie folgt erfolgen:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Objekte, die als Aktionsmethodenparameter übergeben werden, unterstützen auch ein [Bind]-Attribut, das es ermöglicht, eine "Includeliste" zulässiger Eigenschaften wie folgt anzugeben:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Sperren der Bindung auf Typbasis

Sie können die Bindungsregeln auch pro Typ sperren. Auf diese Weise können Sie die Bindungsregeln einmal angeben und sie dann in allen Szenarien (einschließlich UpdateModel- und Aktionsmethodenparameterszenarien) auf alle Controller und Aktionsmethoden anwenden.

Sie können die Bindungsregeln pro Typ anpassen, indem Sie einem Typ ein [Bind]-Attribut hinzufügen oder es in der Datei Global.asax der Anwendung registrieren (nützlich für Szenarien, in denen Sie den Typ nicht besitzen). Sie können dann die Eigenschaften "Einschließen" und "Ausschließen" des Bind-Attributs verwenden, um zu steuern, welche Eigenschaften für die jeweilige Klasse oder Schnittstelle bindbar sind.

Wir verwenden diese Technik für die Dinner-Klasse in unserer NerdDinner-Anwendung und fügen ihr ein [Bind]-Attribut hinzu, das die Liste der bindbaren Eigenschaften auf Folgendes beschränkt:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

Beachten Sie, dass wir nicht zulassen, dass die RSVPs-Sammlung über Diebindung manipuliert wird, noch lassen wir die DinnerID- oder HostedBy-Eigenschaften über Die Bindung festlegen. Aus Sicherheitsgründen bearbeiten wir diese speziellen Eigenschaften stattdessen nur mithilfe von explizitem Code innerhalb unserer Aktionsmethoden.

### <a name="crud-wrap-up"></a>CRUD Wrap-Up

ASP.NET MVC enthält eine Reihe integrierter Funktionen, die bei der Implementierung von Formularbuchungsszenarien helfen. Wir haben eine Vielzahl dieser Funktionen verwendet, um CRUD UI-Unterstützung zusätzlich zu unserem DinnerRepository bereitzustellen.

Wir verwenden einen modellorientierten Ansatz, um unsere Anwendung zu implementieren. Das bedeutet, dass unsere gesamte Validierungs- und Geschäftsregellogik innerhalb unserer Modellebene definiert ist – und nicht innerhalb unserer Controller oder Ansichten. Weder unsere Controller-Klasse noch unsere View-Vorlagen wissen etwas über die spezifischen Geschäftsregeln, die von unserer Dinner-Modellklasse erzwungen werden.

Dadurch wird unsere Anwendungsarchitektur sauber bleiben und das Testen vereinfacht. Wir können unserer Modellebene in Zukunft zusätzliche Geschäftsregeln hinzufügen und *müssen keine Codeänderungen* an unserem Controller oder unserer Ansicht vornehmen, damit sie unterstützt werden können. Dies wird uns eine große Agilität bieten, um unsere Anwendung in der Zukunft weiterzuentwickeln und zu verändern.

Unser DinnersController ermöglicht jetzt Dinner-Listen/Details sowie Unterstützung zum Erstellen, Bearbeiten und Löschen. Den vollständigen Code für die Klasse finden Sie unten:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Nächster Schritt

Wir haben jetzt grundlegende CRUD (Create, Read, Update and Delete) Unterstützung implementieren in unserer DinnersController-Klasse.

Sehen wir uns nun an, wie wir ViewData- und ViewModel-Klassen verwenden können, um eine noch umfangreichere Benutzeroberfläche in unseren Formularen zu aktivieren.

> [!div class="step-by-step"]
> [Zurück](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [Weiter](use-viewdata-and-implement-viewmodel-classes.md)
