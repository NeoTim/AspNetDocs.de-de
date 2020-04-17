---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 'Iteration #2 – Machen Sie die Anwendung schön (VB) | Microsoft Docs'
author: rick-anderson
description: In dieser Iteration verbessern wir das Erscheinungsbild der Anwendung, indem wir die Standard-ASP.NET MVC-Ansichtsmasterseite und des kaskadierenden Stylesheets ändern.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a97958db442c48bd696f6414f7226127984bc34
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542429"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>Iteration 2 – Optimieren der Gestaltung der Anwendung (VB)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> In dieser Iteration verbessern wir das Erscheinungsbild der Anwendung, indem wir die Standard-ASP.NET MVC-Ansichtsmasterseite und des kaskadierenden Stylesheets ändern.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Erstellen einer Kontaktverwaltungs- ASP.NET MVC-Anwendung (VB)

In dieser Reihe von Tutorials erstellen wir eine gesamte Contact Management-Anwendung von Anfang bis Ende. Mit der Contact Manager-Anwendung können Sie Kontaktinformationen – Namen, Telefonnummern und E-Mail-Adressen – für eine Personenliste speichern.

Wir erstellen die Anwendung über mehrere Iterationen. Mit jeder Iteration verbessern wir die Anwendung schrittweise. Das Ziel dieses Ansatzes mit mehreren Iterationen besteht darin, den Grund für jede Änderung zu verstehen.

- Iteration #1 – Erstellen Sie die Anwendung. In der ersten Iteration erstellen wir den Contact Manager auf einfachste Weise. Wir fügen Unterstützung für grundlegende Datenbankvorgänge hinzu: Erstellen, Lesen, Aktualisieren und Löschen (CRUD).

- Iteration #2 – Lassen Sie die Anwendung schön aussehen. In dieser Iteration verbessern wir das Erscheinungsbild der Anwendung, indem wir die Standard-ASP.NET MVC-Ansichtsmasterseite und des kaskadierenden Stylesheets ändern.

- Iteration #3 – Formularvalidierung hinzufügen. In der dritten Iteration fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen ein Formular einreichen, ohne die erforderlichen Formularfelder ausfüllen zu müssen. Wir validieren auch E-Mail-Adressen und Telefonnummern.

- Iteration #4 – Machen Sie die Anwendung lose gekoppelt. In dieser vierten Iteration nutzen wir mehrere Softwareentwurfsmuster, um die Wartung und Änderung der Contact Manager-Anwendung zu vereinfachen. Beispielsweise gestalten wir unsere Anwendung so um, dass sie das Repository-Muster und das Abhängigkeitsinjektionsmuster verwendet.

- Iteration #5 – Erstellen Sie Komponententests. In der fünften Iteration erleichtern wir die Wartung und Änderung unserer Anwendung durch Hinzufügen von Komponententests. Wir verspotten unsere Datenmodellklassen und erstellen Komponententests für unsere Controller und Validierungslogik.

- Iteration #6 – Verwenden Sie die testgesteuerte Entwicklung. In dieser sechsten Iteration fügen wir unserer Anwendung neue Funktionen hinzu, indem wir zuerst Komponententests schreiben und Code für die Komponententests schreiben. In dieser Iteration fügen wir Kontaktgruppen hinzu.

- Iteration #7 – Ajax-Funktionalität hinzufügen. In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung unserer Anwendung, indem wir Unterstützung für Ajax hinzufügen.

## <a name="this-iteration"></a>Diese Iteration

Das Ziel dieser Iteration besteht darin, das Erscheinungsbild der Contact Manager-Anwendung zu verbessern. Derzeit verwendet der Kontakt-Manager die Standard-ASP.NET MVC-Ansichtsmasterseite und das Cascading-Stylesheet (siehe Abbildung 1). Diese sehen nicht schlecht aus, aber ich möchte nicht, dass der Contact Manager genau wie jede andere ASP.NET MVC-Website aussieht. Ich möchte diese Dateien durch benutzerdefinierte Dateien ersetzen.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**Abbildung 01**: Die Standarddarstellung einer ASP.NET MVC-Anwendung ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image2.png))

In dieser Iteration bespreche ich zwei Ansätze zur Verbesserung des visuellen Designs unserer Anwendung. Zuerst zeige ich Ihnen, wie Sie die ASP.NET MVC Design-Galerie nutzen können, um eine kostenlose ASP.NET MVC-Designvorlage herunterzuladen. Mit der ASP.NET MVC Design Galerie können Sie eine professionelle Webanwendung erstellen, ohne Arbeit zu leisten.

Ich habe mich entschieden, keine Vorlage aus der ASP.NET MVC-Entwurfsgalerie für die Contact Manager-Anwendung zu verwenden. Stattdessen hatte ich ein individuelles Design von einem professionellen Design-Unternehmen erstellt. Im zweiten Teil dieses Tutorials erkläre ich, wie ich mit einem professionellen Designunternehmen zusammengearbeitet habe, um die endgültige ASP.NET MVC-Design zu erstellen.

## <a name="the-aspnet-mvc-design-gallery"></a>Die ASP.NET MVC Design Gallery

Die ASP.NET MVC Design Gallery ist eine kostenlose Ressource, die von Microsoft bereitgestellt wird. Die ASP.NET MVC Gallery befindet sich unter folgender Adresse:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

Die ASP.NET MVC Design Gallery beherbergt eine Sammlung kostenloser Website-Designs, die speziell für die Verwendung in einem ASP.NET MVC-Projekt erstellt wurden. Designs werden von Mitgliedern der Community hochgeladen. Besucher der Galerie können für ihre Lieblingsdesigns abstimmen (siehe Abbildung 2).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**Abbildung 02**: Die ASP.NET MVC Design Gallery ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image4.png))

Während ich dieses Tutorial schreibe, ist das beliebteste Design in der Galerie ein Design namens Oktober von David Hauser. Sie können diesen Entwurf für ein ASP.NET MVC-Projekt verwenden, indem Sie die folgenden Schritte ausführen:

1. Klicken Sie auf die Schaltfläche **Herunterladen,** um die Datei October.zip auf Ihren Computer herunterzuladen.
2. Klicken Sie mit der rechten Maustaste auf die heruntergeladene Datei October.zip und klicken Sie auf die Schaltfläche **Entsperren** (siehe Abbildung 3).
3. Entpacken Sie die Datei in einen Ordner mit dem Namen Oktober.
4. Wählen Sie alle Dateien aus dem Ordner DesignTemplate aus, die im Oktober-Ordner enthalten sind, klicken Sie mit der rechten Maustaste auf die Dateien, und wählen Sie die Menüoption **Kopieren**aus.
5. Klicken Sie im Fenster Visual Studio Solution Explorer mit der rechten Maustaste auf den ContactManager-Projektknoten, und wählen Sie die Menüoption **Einfügen** aus (siehe Abbildung 4).
6. Wählen Sie die Menüoption Visual Studio **Bearbeiten, Suchen und Ersetzen, Schnellersetzen** und Ersetzen *von [MyProjectName]* durch *ContactManager* (siehe Abbildung 5).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**Abbildung 03**: Entsperren einer aus dem Web heruntergeladenen Datei[(Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image6.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**Abbildung 04**: Überschreiben von Dateien im Projektmappen-Explorer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image8.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**Abbildung 05**: Ersetzen von [ProjectName] durch ContactManager ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image10.png))

Nachdem Sie diese Schritte ausgeführt haben, verwendet Ihre Webanwendung das neue Design. Die Seite in Abbildung 6 veranschaulicht das Erscheinungsbild der Contact Manager-Anwendung mit dem Oktoberentwurf.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**Abbildung 06**: ContactManager mit der[Oktober-Vorlage ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>Erstellen eines benutzerdefinierten ASP.NET MVC-Entwurfs

Die ASP.NET MVC Design Gallery bietet eine gute Auswahl an verschiedenen Designstilen. Die Galerie bietet Ihnen eine schmerzlose Möglichkeit, das Erscheinungsbild Ihrer ASP.NET MVC-Anwendungen anzupassen. Und natürlich hat die Galerie den großen Vorteil, völlig frei zu sein.

Möglicherweise müssen Sie jedoch ein völlig einzigartiges Design für Ihre Website erstellen. In diesem Fall ist es sinnvoll, mit einem Website-Design-Unternehmen zusammenzuarbeiten. Ich habe mich für diesen Ansatz für den Entwurf der Contact Manager-Anwendung entschieden.

Ich habe den Contact Manager aus Iteration #1 gezippt und das Projekt an die Konstruktionsfirma gesendet. Sie besaßen kein Visual Studio (Schande über sie!), aber das stellte kein Problem dar. Sie konnten Microsoft Visual Web Developer kostenlos [https://www.asp.net](https://www.asp.net) von der Website herunterladen und die Contact Manager-Anwendung in Visual Web Developer öffnen. In ein paar Tagen hatten sie das Design in Abbildung 7 erstellt.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**Abbildung 07**: Der ASP.NET MVC Contact Manager Design ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-2-make-the-application-look-nice-vb/_static/image14.png))

Das neue Design bestand aus zwei Hauptdateien: einer neuen cascading Stylesheet-Datei und einer neuen Ansichtsmasterseite. Eine Ansichtsmasterseite enthält das Layout und den freigegebenen Inhalt für Ansichten in einer ASP.NET MVC-Anwendung. Die Ansichtsmasterseite enthält z. B. die Kopfzeile, Navigationsregisterkarten und Fußzeile, die in Abbildung 7 angezeigt werden. Ich habe die vorhandene Site.Master-Ansichtsmasterseite im Ordner Ansichten und Gemeinsame Freigabe mit der neuen Site.Master-Datei des Designunternehmens überschrieben,

Die Designfirma erstellte auch ein neues kaskadierendes Stylesheet und einen Satz von Bildern. Ich habe diese neuen Dateien in den Ordner Inhalt gelegt und die vorhandene Site.css-Datei überschrieben. Sie sollten alle statischen Inhalte im Ordner Inhalt platzieren.

Beachten Sie, dass das neue Design für den Kontakt-Manager Bilder zum Bearbeiten und Löschen von Kontakten enthält. Neben jedem Kontakt in der HTML-Kontakttabelle wird ein Bild zum Bearbeiten und Löschen angezeigt.

Ursprünglich diese Links, die mit dem HTML gerendert wurden. ActionLink() Helfer wie folgt:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Die Html.ActionLink()-Methode unterstützt keine Bilder (die Methode HTML kodiert den Linktext aus Sicherheitsgründen). Daher habe ich die Aufrufe von Html.ActionLink() durch Aufrufe von Url.Action() wie folgt ersetzt:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Die Html.ActionLink()-Methode rendert einen gesamten HTML-Hyperlink. Die Url.Action()-Methode hingegen rendert nur die URL &lt;&gt; ohne das A-Tag.

Beachten Sie außerdem, dass das neue Design sowohl ausgewählte als auch nicht ausgewählte Registerkarten enthält. In Abbildung 8 ist z. B. die Registerkarte **Neue Kontakte erstellen** ausgewählt, und die Registerkarte Meine **Kontakte** ist nicht ausgewählt.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**Abbildung 08**: Ausgewählte und nicht ausgewählte Registerkarten([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](iteration-2-make-the-application-look-nice-vb/_static/image16.png)

Um das Rendern sowohl ausgewählter als auch nicht ausgewählter Registerkarten zu unterstützen, habe ich einen benutzerdefinierten HTML-Helfer namens MenuItemHelper erstellt. Diese Hilfsmethode rendert &lt;entweder&gt; ein &lt;li-Tag oder&gt; ein li-Class="selected"-Tag, je nachdem, ob der aktuelle Controller und die Aktion dem Controller und dem Aktionsnamen entsprechen, die an den Helfer übergeben werden. Der Code für den MenuItemHelper ist in Liste 1 enthalten.

**Auflisten 1 – Helpers-MenuItemHelper.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

Der MenuItemHelper verwendet die TagBuilder-Klasse intern, um das &lt;li&gt; HTML-Tag zu erstellen. Die TagBuilder-Klasse ist eine sehr nützliche Dienstprogrammklasse, die Sie immer dann verwenden können, wenn Sie ein neues HTML-Tag erstellen müssen. Es enthält Methoden zum Hinzufügen von Attributen, Hinzufügen von CSS-Klassen, Generieren von IDs und Ändern des inneren HTML-Codes des Tags.

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir das visuelle Design unserer ASP.NET MVC-Anwendung verbessert. Zuerst wurden Sie in die mVC Design Gallery ASP.NET eingeführt. Sie haben gelernt, wie Sie kostenlose Designvorlagen aus der ASP.NET MVC Design Gallery herunterladen, die Sie in Ihren ASP.NET MVC-Anwendungen verwenden können.

Als Nächstes haben wir erläutert, wie Sie einen benutzerdefinierten Entwurf erstellen können, indem Sie die standardmäßige cascading Stylesheet-Datei und die Masteransichtsseitendatei ändern. Um das neue Design zu unterstützen, mussten wir einige kleinere Änderungen an unserer Contact Manager-Anwendung vornehmen. Beispielsweise haben wir einen neuen HTML-Helfer namens MenuItemHelper hinzugefügt, der ausgewählte und nicht ausgewählte Registerkarten anzeigt.

In der nächsten Iteration befassen wir uns mit dem sehr wichtigen Thema der Validierung. Wir fügen unserer Anwendung Validierungscode hinzu, damit ein Benutzer keinen neuen Kontakt erstellen kann, ohne erforderliche Werte wie den Vor- und Nachnamen einer Person angeben zu müssen.

> [!div class="step-by-step"]
> [Zurück](iteration-1-create-the-application-vb.md)
> [Weiter](iteration-3-add-form-validation-vb.md)
