---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 'Iteration #7 – Ajax-Funktionalität (VB) hinzufügen | Microsoft Docs'
author: rick-anderson
description: In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung unserer Anwendung, indem wir Unterstützung für Ajax hinzufügen.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: 04eaaa129a56b765c090e64118ed528c65987b50
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542299"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>Iteration 7 – Hinzufügen von AJAX-Funktionen (VB)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung unserer Anwendung, indem wir Unterstützung für Ajax hinzufügen.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Erstellen einer Kontaktverwaltungs- ASP.NET MVC-Anwendung (VB)

In dieser Reihe von Tutorials erstellen wir eine gesamte Contact Management-Anwendung von Anfang bis Ende. Mit der Kontakt-Manager-Anwendung können Sie Kontaktinformationen - Namen, Telefonnummern und E-Mail-Adressen - für eine Personenliste speichern.

Wir erstellen die Anwendung über mehrere Iterationen. Mit jeder Iteration verbessern wir die Anwendung schrittweise. Das Ziel dieses Ansatzes mit mehreren Iterationen besteht darin, den Grund für jede Änderung zu verstehen.

- Iteration #1 - Erstellen Sie die Anwendung. In der ersten Iteration erstellen wir den Contact Manager auf einfachste Weise. Wir fügen Unterstützung für grundlegende Datenbankvorgänge hinzu: Erstellen, Lesen, Aktualisieren und Löschen (CRUD).

- Iteration #2 - Machen Sie die Anwendung schön aussehen. In dieser Iteration verbessern wir das Erscheinungsbild der Anwendung, indem wir die Standard-ASP.NET MVC-Ansichtsmasterseite und des kaskadierenden Stylesheets ändern.

- Iteration #3 - Formularüberprüfung hinzufügen. In der dritten Iteration fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen ein Formular einreichen, ohne die erforderlichen Formularfelder ausfüllen zu müssen. Wir validieren auch E-Mail-Adressen und Telefonnummern.

- Iteration #4 - Machen Sie die Anwendung lose gekoppelt. In dieser vierten Iteration nutzen wir mehrere Softwareentwurfsmuster, um die Wartung und Änderung der Contact Manager-Anwendung zu vereinfachen. Beispielsweise gestalten wir unsere Anwendung so um, dass sie das Repository-Muster und das Abhängigkeitsinjektionsmuster verwendet.

- Iteration #5 - Erstellen von Komponententests. In der fünften Iteration erleichtern wir die Wartung und Änderung unserer Anwendung durch Hinzufügen von Komponententests. Wir verspotten unsere Datenmodellklassen und erstellen Komponententests für unsere Controller und Validierungslogik.

- Iteration #6 - Verwenden Sie die testgesteuerte Entwicklung. In dieser sechsten Iteration fügen wir unserer Anwendung neue Funktionen hinzu, indem wir zuerst Komponententests schreiben und Code für die Komponententests schreiben. In dieser Iteration fügen wir Kontaktgruppen hinzu.

- Iteration #7 - Ajax-Funktionalität hinzufügen. In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung unserer Anwendung, indem wir Unterstützung für Ajax hinzufügen.

## <a name="this-iteration"></a>Diese Iteration

In dieser Iteration der Contact Manager-Anwendung gestalten wir unsere Anwendung um, um Ajax zu nutzen. Indem wir Die Vorteile von Ajax nutzen, machen wir unsere Anwendung reaktionsschneller. Wir können das Rendern einer ganzen Seite vermeiden, wenn wir nur eine bestimmte Region in einer Seite aktualisieren müssen.

Wir gestalten unsere Indexansicht so um, dass wir nicht die gesamte Seite neu anzeigen müssen, wenn jemand eine neue Kontaktgruppe auswählt. Wenn jemand stattdessen auf eine Kontaktgruppe klickt, aktualisieren wir einfach die Liste der Kontakte und lassen den Rest der Seite in Ruhe.

Wir ändern auch die Funktionsweise unseres Löschlinks. Anstatt eine separate Bestätigungsseite anzuzeigen, wird ein JavaScript-Bestätigungsdialogfeld angezeigt. Wenn Sie bestätigen, dass Sie einen Kontakt löschen möchten, wird ein HTTP DELETE-Vorgang für den Server ausgeführt, um den Kontaktdatensatz aus der Datenbank zu löschen.

Darüber hinaus nutzen wir jQuery, um Unserer Indexansicht Animationseffekte hinzuzufügen. Wir zeigen eine Animation an, wenn die neue Liste der Kontakte vom Server abgerufen wird.

Schließlich nutzen wir die ASP.NET AJAX-Frameworkunterstützung für die Verwaltung des Browserverlaufs. Wir erstellen Verlaufspunkte, wenn wir einen Ajax-Aufruf durchführen, um die Kontaktliste zu aktualisieren. Auf diese Weise funktioniert der Browser rückwärts und vorwärts Tasten.

## <a name="why-use-ajax"></a>Warum Ajax?

Die Verwendung von Ajax hat viele Vorteile. Erstens führt das Hinzufügen von Ajax-Funktionalität zu einer Anwendung zu einer besseren Benutzererfahrung. In einer normalen Webanwendung muss die gesamte Seite jedes Mal, wenn ein Benutzer eine Aktion ausführt, an den Server zurückgesendet werden. Wenn Sie eine Aktion ausführen, wird der Browser gesperrt und der Benutzer muss warten, bis die gesamte Seite abgerufen und erneut angezeigt wird.

Dies wäre eine inakzeptable Erfahrung im Falle einer Desktop-Anwendung. Aber traditionell lebten wir mit dieser schlechten Benutzererfahrung im Falle einer Webanwendung, weil wir nicht wussten, dass wir es besser machen könnten. Wir dachten, es sei eine Einschränkung von Web-Anwendungen, wenn es in Wirklichkeit nur eine Einschränkung unserer Vorstellungskraft war.

In einer Ajax-Anwendung müssen Sie die Benutzererfahrung nicht zum Stillstand bringen, nur um eine Seite zu aktualisieren. Stattdessen können Sie eine asynchrone Anforderung im Hintergrund ausführen, um die Seite zu aktualisieren. Sie zwingen den Benutzer nicht zu warten, während ein Teil der Seite aktualisiert wird.

Durch die Nutzung von Ajax können Sie auch die Leistung Ihrer Anwendung verbessern. Überlegen Sie, wie die Contact Manager-Anwendung derzeit ohne Ajax-Funktionalität funktioniert. Wenn Sie auf eine Kontaktgruppe klicken, muss die gesamte Indexansicht erneut angezeigt werden. Die Liste der Kontakte und die Liste der Kontaktgruppen müssen vom Datenbankserver abgerufen werden. Alle diese Daten müssen über das Kabel vom Webserver an den Webbrowser weitergegeben werden.

Nachdem wir unserer Anwendung Ajax-Funktionalität hinzugefügt haben, können wir jedoch vermeiden, dass die gesamte Seite erneut angezeigt wird, wenn ein Benutzer auf eine Kontaktgruppe klickt. Wir müssen die Kontaktgruppen nicht mehr aus der Datenbank holen. Wir müssen auch nicht die gesamte Indexansicht über den Draht schieben. Durch die Nutzung von Ajax reduzieren wir die Arbeit, die unser Datenbankserver leisten muss, und wir reduzieren den Netzwerkverkehr, der von unserer Anwendung benötigt wird.

## <a name="don-t-be-afraid-of-ajax"></a>Keine Angst vor Ajax

Einige Entwickler vermeiden die Verwendung von Ajax, weil sie sich Sorgen um Downlevel-Browser machen. Sie möchten sicherstellen, dass ihre Webanwendungen weiterhin funktionieren, wenn sie von einem Browser aufgerufen werden, der JavaScript nicht unterstützt. Da Ajax auf JavaScript angewiesen ist, vermeiden einige Entwickler die Verwendung von Ajax.

Wenn Sie jedoch darauf achten, wie Sie Ajax implementieren, können Sie Anwendungen erstellen, die sowohl mit Uplevel- als auch mit Downlevel-Browsern funktionieren. Unsere Contact Manager-Anwendung funktioniert mit Browsern, die JavaScript unterstützen, und Browsern, die dies nicht tun.

Wenn Sie die Contact Manager-Anwendung mit einem Browser verwenden, der JavaScript unterstützt, haben Sie eine bessere Benutzererfahrung. Wenn Sie beispielsweise auf eine Kontaktgruppe klicken, wird nur der Bereich der Seite aktualisiert, auf der Kontakte angezeigt werden.

Wenn Sie hingegen die Contact Manager-Anwendung mit einem Browser verwenden, der JavaScript nicht unterstützt (oder JavaScript deaktiviert hat), haben Sie eine etwas weniger wünschenswerte Benutzererfahrung. Wenn Sie beispielsweise auf eine Kontaktgruppe klicken, muss die gesamte Indexansicht wieder an den Browser gesendet werden, um die entsprechende Kontaktliste anzuzeigen.

## <a name="adding-the-required-javascript-files"></a>Hinzufügen der erforderlichen JavaScript-Dateien

Wir müssen drei JavaScript-Dateien verwenden, um Ajax-Funktionalität zu unserer Anwendung hinzuzufügen. Alle drei Dateien sind im Ordner Scripts einer neuen ASP.NET MVC-Anwendung enthalten.

Wenn Sie Ajax auf mehreren Seiten in Ihrer Anwendung verwenden möchten, ist es sinnvoll, die erforderlichen JavaScript-Dateien in die Masterseite Ihrer Anwendung aufzunehmen. Auf diese Weise werden die JavaScript-Dateien automatisch in allen Seiten Ihrer Anwendung enthalten sein.

Fügen Sie das folgende &lt;JavaScript im Head-Tag&gt; Ihrer Ansichtmasterseite hinzu:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Umgestaltung der Indexansicht für die Verwendung von Ajax

Beginnen wir, indem wir unsere Indexansicht so ändern, dass durch Klicken auf eine Kontaktgruppe nur der Bereich der Ansicht aktualisiert wird, in der Kontakte angezeigt werden. Das rote Feld in Abbildung 1 enthält die Region, die wir aktualisieren möchten.

[![Nur Kontakte aktualisieren](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**Abbildung 01**: Aktualisieren nur Kontakte ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-7-add-ajax-functionality-vb/_static/image2.png))

Der erste Schritt besteht darin, den Teil der Ansicht, den wir asynchron aktualisieren möchten, in einen separaten Teil (Benutzersteuerelement anzeigen) zu trennen. Der Abschnitt der Indexansicht, in dem die Kontakttabelle angezeigt wird, wurde in die Teilliste in Liste 1 verschoben.

**Auflisten 1 - Ansichten- Kontakt-Kontaktliste.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

Beachten Sie, dass der Teil in Listing 1 ein anderes Modell als die Indexansicht hat. Das *Inherits-Attribut* in &lt;der&gt; Direktive "%" Seite % gibt&lt;an, dass der Teil von der ViewUserControl Group-Klasse&gt; erbt.

Die aktualisierte Indexansicht ist in Liste 2 enthalten.

**Eintrag 2 - Ansichten, Kontakt, Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

Es gibt zwei Dinge, die Sie über die aktualisierte Ansicht in Liste 2 beachten sollten. Beachten Sie zunächst, dass der gesamte Inhalt, der in den Teil verschoben wurde, durch einen Aufruf von Html.RenderPartial(ersetzt wird. Die Html.RenderPartial()-Methode wird aufgerufen, wenn die Indexansicht zum ersten Mal angefordert wird, um den anfänglichen Satz von Kontakten anzuzeigen.

Beachten Sie zweitens, dass der Html.ActionLink(), der zum Anzeigen von Kontaktgruppen verwendet wird, durch einen Ajax.ActionLink() ersetzt wurde. Der Ajax.ActionLink() wird mit den folgenden Parametern aufgerufen:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

Der erste Parameter stellt den Text dar, der für die Verknüpfung angezeigt werden soll, der zweite Parameter stellt die Routenwerte und der dritte Parameter die Ajax-Optionen dar. In diesem Fall verwenden wir die Option UpdateTargetId &lt;Ajax, um auf das HTML-div-Tag&gt; zu verweisen, das wir nach Abschluss der Ajax-Anforderung aktualisieren möchten. Wir möchten das &lt;&gt; div-Tag mit der neuen Kontaktliste aktualisieren.

Die aktualisierte Index()-Methode des Kontaktcontrollers ist in Liste 3 enthalten.

**Auflisten 3 - Controllers-ContactController.vb (Indexmethode)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

Die aktualisierte Index()-Aktion gibt bedingt eines von zwei Dingen zurück. Wenn die Index()-Aktion von einer Ajax-Anforderung aufgerufen wird, gibt der Controller einen Teil zurück. Andernfalls gibt die Index()-Aktion eine gesamte Ansicht zurück.

Beachten Sie, dass die Index()-Aktion nicht so viele Daten zurückgeben muss, wenn sie von einer Ajax-Anforderung aufgerufen wird. Im Kontext einer normalen Anforderung gibt die Indexaktion eine Liste aller Kontaktgruppen und der ausgewählten Kontaktgruppe zurück. Im Kontext einer Ajax-Anforderung gibt die Index()-Aktion nur die ausgewählte Gruppe zurück. Ajax bedeutet weniger Arbeit auf Ihrem Datenbankserver.

Unsere modifizierte Indexansicht funktioniert sowohl bei Uplevel- als auch downlevel-Browsern. Wenn Sie auf eine Kontaktgruppe klicken und Ihr Browser JavaScript unterstützt, wird nur der Bereich der Ansicht aktualisiert, der die Liste der Kontakte enthält. Wenn Ihr Browser JavaScript hingegen nicht unterstützt, wird die gesamte Ansicht aktualisiert.

Unsere aktualisierte Indexansicht hat ein Problem. Wenn Sie auf eine Kontaktgruppe klicken, wird die ausgewählte Gruppe nicht hervorgehoben. Da die Liste der Gruppen außerhalb der Region angezeigt wird, die während einer Ajax-Anforderung aktualisiert wird, wird die rechte Gruppe nicht hervorgehoben. Dieses Problem wird im nächsten Abschnitt behoben.

## <a name="adding-jquery-animation-effects"></a>Hinzufügen von jQuery-Animationseffekten

Wenn Sie auf einen Link auf einer Webseite klicken, können Sie die Browser-Fortschrittsleiste verwenden, um zu erkennen, ob der Browser den aktualisierten Inhalt aktiv abruft. Beim Ausführen einer Ajax-Anforderung zeigt die Browser-Fortschrittsleiste hingegen keinen Fortschritt an. Dies kann Benutzer nervös machen. Woher wissen Sie, ob der Browser eingefroren wurde?

Es gibt mehrere Möglichkeiten, wie Sie einem Benutzer angeben können, dass während der Ausführung einer Ajax-Anforderung gearbeitet wird. Ein Ansatz besteht darin, eine einfache Animation anzuzeigen. Sie können z. B. eine Region ausblenden, wenn eine Ajax-Anforderung beginnt, und in der Region ausblenden, wenn die Anforderung abgeschlossen ist.

Wir verwenden die jQuery-Bibliothek, die im Microsoft ASP.NET MVC-Framework enthalten ist, um die Animationseffekte zu erstellen. Die aktualisierte Indexansicht ist in Liste 4 enthalten.

**Eintrag 4 - Ansichten, Kontakt, Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

Beachten Sie, dass die aktualisierte Indexansicht drei neue JavaScript-Funktionen enthält. Die ersten beiden Funktionen verwenden jQuery, um in der Liste der Kontakte auszublenden und auszublenden, wenn Sie auf eine neue Kontaktgruppe klicken. Die dritte Funktion zeigt eine Fehlermeldung an, wenn eine Ajax-Anforderung zu einem Fehler führt (z. B. Netzwerktimeout).

Die erste Funktion kümmert sich auch um die Hervorhebung der ausgewählten Gruppe. Dem übergeordneten Element (dem LI-Element) des angeklickten Elements wird ein class= selected-Attribut hinzugefügt. Auch hier macht es jQuery einfach, das richtige Element auszuwählen und die CSS-Klasse hinzuzufügen.

Diese Skripte sind mit Hilfe des Ajax.ActionLink() AjaxOptions Parameters an die Gruppenverknüpfungen gebunden. Der aktualisierte Ajax.ActionLink()-Methodenaufruf sieht wie folgt aus:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Hinzufügen von Browserverlaufsunterstützung

Wenn Sie auf einen Link klicken, um eine Seite zu aktualisieren, wird der Browserverlauf aktualisiert. Auf diese Weise können Sie auf die Schaltfläche "Zurück" des Browsers klicken, um in der Zeit wieder in den vorherigen Zustand der Seite zu wechseln. Wenn Sie beispielsweise auf die Kontaktgruppe Freunde und dann auf die Kontaktgruppe "Unternehmen" klicken, können Sie auf die Schaltfläche "Zurück" des Browsers klicken, um zurück zum Status der Seite zu navigieren, als die Kontaktgruppe Freunde ausgewählt wurde.

Leider wird durch das Ausführen einer Ajax-Anforderung der Browserverlauf nicht automatisch aktualisiert. Wenn Sie auf eine Kontaktgruppe klicken und die Liste der übereinstimmenden Kontakte mit einer Ajax-Anforderung abgerufen wird, wird der Browserverlauf nicht aktualisiert. Sie können die Schaltfläche "Zurück" des Browsers nicht verwenden, um nach der Auswahl einer neuen Kontaktgruppe zurück zu einer Kontaktgruppe zu navigieren.

Wenn Sie möchten, dass Benutzer die Schaltfläche "Zurück" des Browsers verwenden können, nachdem Sie Ajax-Anforderungen ausgeführt haben, müssen Sie etwas mehr Arbeit leisten. Sie müssen die im ASP.NET AJAX Framework integrierten Browserverlaufsverwaltungsfunktionen nutzen.

ASP.NET AJAX-Browserverlauf müssen Sie drei Dinge tun:

1. Aktivieren Sie den Browserverlauf, indem Sie die enableBrowserHistory-Eigenschaft auf true festlegen.
2. Speichern Sie Verlaufspunkte, wenn sich der Status einer Ansicht ändert, indem Sie die addHistoryPoint()-Methode aufrufen.
3. Rekonstruieren Sie den Status der Ansicht, wenn das Navigationsereignis ausgelöst wird.

Die aktualisierte Indexansicht ist in Liste 5 enthalten.

**Eintrag 5 - Ansichten, Kontakt, Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

In Listing 5 ist der Browserverlauf in der PageInit()-Funktion aktiviert. Die pageInit()-Funktion wird auch verwendet, um den Ereignishandler für das navigationsereignis einzurichten. Das Navigationsereignis wird ausgelöst, wenn die Schaltfläche Vorwärts oder Zurück des Browsers bewirkt, dass sich der Status der Seite ändert.

Die beginContactList()-Methode wird aufgerufen, wenn Sie auf eine Kontaktgruppe klicken. Diese Methode erstellt einen neuen Verlaufspunkt, indem die addHistoryPoint()-Methode aufgerufen wird. Die ID der aufgeklickten Kontaktgruppe wird dem Verlauf hinzugefügt.

Die Gruppen-ID wird aus einem expando-Attribut auf der Kontaktgruppenverknüpfung abgerufen. Der Link wird mit dem folgenden Aufruf von Ajax.ActionLink() gerendert.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

Der letzte Parameter, der an Ajax.ActionLink() übergeben wird, fügt der Verknüpfung ein expando-Attribut namens groupid hinzu (Kleinbuchstaben für XHTML-Kompatibilität).

Wenn ein Benutzer auf die Schaltfläche "Zurück" oder "Vorwärts" des Browsers trifft, wird das Navigationsereignis ausgelöst und die navigate()-Methode aufgerufen. Diese Methode aktualisiert die auf der Seite angezeigten Kontakte so, dass sie dem Status der Seite entsprechen, die dem Browserverlaufspunkt entspricht, der an die Navigate-Methode übergeben wird.

## <a name="performing-ajax-deletes"></a>Ausführen von Ajax-Löschvorgängen

Um einen Kontakt zu löschen, müssen Sie derzeit auf den Link Löschen klicken und dann auf die Schaltfläche Löschen klicken, die auf der Seite Bestätigung löschen angezeigt wird (siehe Abbildung 2). Dies scheint wie eine Menge von Seitenanfragen, um etwas Einfaches wie das Löschen eines Datenbankdatensatzes zu tun.

[![Die Bestätigungsseite zum Löschen](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**Abbildung 02**: Die Seite zur Bestätigung löschen([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](iteration-7-add-ajax-functionality-vb/_static/image4.png)

Es ist verlockend, die Seite bestätigung löschen und einen Kontakt direkt aus der Indexansicht zu löschen. Sie sollten diese Versuchung vermeiden, da dieser Ansatz Ihre Anwendung für Sicherheitslücken öffnet. Im Allgemeinen möchten Sie beim Aufrufen einer Aktion, die den Status Ihrer Webanwendung ändert, keinen HTTP GET-Vorgang ausführen. Wenn Sie einen Löschvorgang durchführen, möchten Sie einen HTTP-POST-Vorgang oder besser noch einen HTTP DELETE-Vorgang ausführen.

Der Link Löschen ist in der ContactList-Partie enthalten. Eine aktualisierte Version der ContactList-Partie ist in Liste 6 enthalten.

**Auflisten 6 - Ansichten- Kontakt-Kontaktliste.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

Der Link Löschen wird mit dem folgenden Aufruf der Ajax.ImageActionLink()-Methode gerendert:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Der Ajax.ImageActionLink() ist kein Standardbestandteil des ASP.NET MVC-Frameworks. Der Ajax.ImageActionLink() ist eine benutzerdefinierte Hilfsmethode, die im Contact Manager-Projekt enthalten ist.

Der Parameter AjaxOptions hat zwei Eigenschaften. Zunächst wird die Confirm-Eigenschaft verwendet, um ein Popup-JavaScript-Bestätigungsdialogfeld anzuzeigen. Zweitens wird die HttpMethod-Eigenschaft verwendet, um einen HTTP DELETE-Vorgang auszuführen.

Liste 7 enthält eine neue AjaxDelete()-Aktion, die dem Contact-Controller hinzugefügt wurde.

**Auflisten 7 - Controller-KontaktController.vb (AjaxDelete)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

Die Aktion AjaxDelete() ist mit einem AcceptVerbs-Attribut versehen. Dieses Attribut verhindert, dass die Aktion aufgerufen wird, außer von einem anderen HTTP-Vorgang als einem HTTP DELETE-Vorgang. Insbesondere können Sie diese Aktion nicht mit einem HTTP GET aufrufen.

Nachdem Sie den Datenbankdatensatz gelöscht haben, müssen Sie die aktualisierte Liste der Kontakte anzeigen, die den gelöschten Datensatz nicht enthält. Die AjaxDelete()-Methode gibt die ContactList teilweise und die aktualisierte Kontaktliste zurück.

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir unserer Contact Manager-Anwendung Ajax-Funktionalität hinzugefügt. Wir haben Ajax verwendet, um die Reaktionsfähigkeit und Leistung unserer Anwendung zu verbessern.

Zuerst haben wir die Indexansicht so umgestaltet, dass durch Klicken auf eine Kontaktgruppe nicht die gesamte Ansicht aktualisiert wird. Wenn Sie stattdessen auf eine Kontaktgruppe klicken, wird nur die Liste der Kontakte aktualisiert.

Als Nächstes haben wir jQuery-Animationseffekte verwendet, um in der Liste der Kontakte auszublenden und auszublenden. Das Hinzufügen von Animationen zu einer Ajax-Anwendung kann verwendet werden, um Benutzern der Anwendung das Äquivalent einer Browser-Fortschrittsleiste bereitzustellen.

Außerdem haben wir unserer Ajax-Anwendung Browserverlaufsunterstützung hinzugefügt. Wir haben Benutzern ermöglicht, auf die Schaltflächen "Zurück" und "Vorwärts" des Browsers zu klicken, um den Status der Indexansicht zu ändern.

Schließlich haben wir einen Löschlink erstellt, der HTTP DELETE-Vorgänge unterstützt. Durch die Durchführung von Ajax-Löschvorgängen ermöglichen wir es Benutzern, Datenbankdatensätze zu löschen, ohne dass der Benutzer eine zusätzliche Löschbestätigungsseite anfordern muss.

> [!div class="step-by-step"]
> [Vorherige](iteration-6-use-test-driven-development-vb.md)
