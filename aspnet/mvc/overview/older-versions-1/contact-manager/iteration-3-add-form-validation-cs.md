---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'Iteration #3 – Hinzufügen der Formularvalidierung (C) | Microsoft Docs'
author: rick-anderson
description: In der dritten Iteration fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen ein Formular einreichen, ohne die erforderlichen Formularfelder ausfüllen zu müssen. Wir validieren auch emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: c8442574d4901045f044f53ea12cd8330e8eaaa3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542377"
---
# <a name="iteration-3--add-form-validation-c"></a>Iteration 3 – Hinzufügen der Formularüberprüfung (C#)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> In der dritten Iteration fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen ein Formular einreichen, ohne die erforderlichen Formularfelder ausfüllen zu müssen. Wir validieren auch E-Mail-Adressen und Telefonnummern.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Erstellen einer Kontaktverwaltungs-ASP.NET MVC-Anwendung (C-Anwendung)

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

In dieser zweiten Iteration der Contact Manager-Anwendung fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen einen Kontakt einreichen, ohne Werte für die erforderlichen Formularfelder einzugeben. Wir validieren auch Telefonnummern und E-Mail-Adressen (siehe Abbildung 1).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**Abbildung 01**: Ein Formular mit Validierung ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-3-add-form-validation-cs/_static/image2.png))

In dieser Iteration fügen wir die Validierungslogik direkt zu den Controlleraktionen hinzu. Im Allgemeinen ist dies nicht die empfohlene Methode, um einer ASP.NET MVC-Anwendung eine Validierung hinzuzufügen. Ein besserer Ansatz besteht darin, die Validierungslogik einer Anwendung in einer separaten [Dienstschicht](http://martinfowler.com/eaaCatalog/serviceLayer.html)zu platzieren. In der nächsten Iteration gestalten wir die Contact Manager-Anwendung um, um die Anwendung wartungsfähiger zu machen.

Um die Dinge einfach zu halten, schreiben wir in dieser Iteration den gesamten Validierungscode von Hand. Anstatt den Validierungscode selbst zu schreiben, könnten wir ein Validierungsframework nutzen. Sie können z. B. den Microsoft Enterprise Library Validation Application Block (VAB) verwenden, um die Validierungslogik für Ihre ASP.NET MVC-Anwendung zu implementieren. Weitere Informationen zum Validierungsanwendungsblock finden Sie unter:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Hinzufügen von Validierung zur Ansicht Erstellen

Beginnen wir mit dem Hinzufügen von Validierungslogik zur Ansicht Erstellen. Da wir die Ansicht Erstellen mit Visual Studio generiert haben, enthält die Ansicht Erstellen glücklicherweise bereits die gesamte erforderliche Benutzeroberflächenlogik zum Anzeigen von Validierungsmeldungen. Die Ansicht Erstellen ist in Liste 1 enthalten.

**Eintrag 1 - ,,Ansichten", "Kontakt" und "Create.aspx"**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

Beachten Sie den Aufruf der Html.ValidationSummary()-Hilfsmethode, die direkt über dem HTML-Formular angezeigt wird. Wenn Überprüfungsfehlermeldungen vorliegen, zeigt diese Methode Validierungsmeldungen in einer Aufzählung an.

Beachten Sie außerdem die Aufrufe von Html.ValidationMessage(), die neben jedem Formularfeld angezeigt werden. Der ValidationMessage()-Hilfsfeld wird eine individuelle Validierungsfehlermeldung angezeigt. Im Fall von Listing 1 wird ein Sternchen angezeigt, wenn ein Validierungsfehler auftritt.

Schließlich rendert der Html.TextBox()-Hilfsfeldeine automatisch eine Cascading Style Sheet-Klasse, wenn der vom Helfer angezeigten Eigenschaft ein Validierungsfehler zugeordnet ist. Der Html.TextBox()-Hilfsfeld macht eine Klasse mit dem Namen **input-validation-error.**

Wenn Sie eine neue ASP.NET MVC-Anwendung erstellen, wird automatisch ein Stylesheet mit dem Namen Site.css im Ordner Inhalt erstellt. Dieses Stylesheet enthält die folgenden Definitionen für CSS-Klassen, die sich auf das Auftreten von Validierungsfehlermeldungen beziehen:

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

Die field-validation-error-Klasse wird verwendet, um die vom Html.ValidationMessage()-Hilfsfeld gerenderte Ausgabe zu formatieren. Die Eingabe-Validierung-Fehler-Klasse wird verwendet, um das Textfeld (Eingabe) zu formatieren, das vom Html.TextBox()-Hilfsfeld gerendert wird. Die Klasse validation-summary-errors wird verwendet, um die ungeordnete Liste zu formatieren, die vom Html.ValidationSummary()-Hilfser gerendert wird.

> [!NOTE] 
> 
> Sie können die in diesem Abschnitt beschriebenen Stylesheetklassen ändern, um die Darstellung von Validierungsfehlermeldungen anzupassen.

## <a name="adding-validation-logic-to-the-create-action"></a>Hinzufügen von Validierungslogik zur Erstellungsaktion

Im Moment zeigt die Ansicht Erstellen niemals Validierungsfehlermeldungen an, da wir die Logik zum Generieren von Nachrichten nicht geschrieben haben. Um Validierungsfehlermeldungen anzuzeigen, müssen Sie die Fehlermeldungen zu ModelState hinzufügen.

> [!NOTE] 
> 
> Die UpdateModel()-Methode fügt ModelState automatisch Fehlermeldungen hinzu, wenn ein Fehler beim Zuweisen des Werts eines Formularfelds zu einer Eigenschaft vorliegt. Wenn Sie beispielsweise versuchen, die Zeichenfolge "apple" einer BirthDate-Eigenschaft zuzuweisen, die DateTime-Werte akzeptiert, fügt die UpdateModel()-Methode ModelState einen Fehler hinzu.

Die geänderte Create()-Methode in Liste 2 enthält einen neuen Abschnitt, der die Eigenschaften der Contact-Klasse überprüft, bevor der neue Kontakt in die Datenbank eingefügt wird.

**Auflistung 2 - Controllers-ContactController.cs (Erstellen mit Validierung)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

Der Abschnitt "Validierung" erzwingt vier unterschiedliche Validierungsregeln:

- Die FirstName-Eigenschaft muss eine Länge größer als Null haben (und sie darf nicht nur aus Leerzeichen bestehen)
- Die LastName-Eigenschaft muss eine Länge größer als Null haben (und sie darf nicht nur aus Leerzeichen bestehen)
- Wenn die Phone-Eigenschaft einen Wert hat (hat eine Länge größer als 0), muss die Phone-Eigenschaft mit einem regulären Ausdruck übereinstimmen.
- Wenn die Email-Eigenschaft einen Wert hat (hat eine Länge größer als 0), muss die Email-Eigenschaft mit einem regulären Ausdruck übereinstimmen.

Wenn eine Validierungsregelverletzung vorliegt, wird ModelState mit Hilfe der AddModelError()-Methode eine Fehlermeldung hinzugefügt. Wenn Sie ModelState eine Nachricht hinzufügen, geben Sie den Namen einer Eigenschaft und den Text einer Validierungsfehlermeldung an. Diese Fehlermeldung wird in der Ansicht von den Hilfsmethoden Html.ValidationSummary() und Html.ValidationMessage() angezeigt.

Nachdem die Validierungsregeln ausgeführt wurden, wird die IsValid-Eigenschaft von ModelState überprüft. Die IsValid-Eigenschaft gibt false zurück, wenn ModelState Validierungsfehlermeldungen hinzugefügt wurden. Wenn die Überprüfung fehlschlägt, wird das Formular Erstellen mit den Fehlermeldungen erneut angezeigt.

> [!NOTE] 
> 
> Ich habe die regulären Ausdrücke für die Überprüfung der Telefonnummer und E-Mail-Adresse aus dem Repository für reguläre Ausdrucke unter[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>Hinzufügen von Validierungslogik zur Bearbeitungsaktion

Die Aktion Bearbeiten() aktualisiert einen Kontakt. Die Edit()-Aktion muss genau die gleiche Validierung wie die Aktion Create() durchführen. Anstatt denselben Validierungscode zu duplizieren, sollten wir den Contact-Controller so umgestalten, dass sowohl die Aktionen Create() als auch Edit() dieselbe Validierungsmethode aufrufen.

Die geänderte Contact-Controller-Klasse ist in Liste 3 enthalten. Diese Klasse verfügt über eine neue ValidateContact()-Methode, die sowohl innerhalb der Aktionen Create() als auch Edit() aufgerufen wird.

**Auflisten 3 - Controller-KontaktController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir unserer Contact Manager-Anwendung eine grundlegende Formularvalidierung hinzugefügt. Unsere Validierungslogik verhindert, dass Benutzer einen neuen Kontakt senden oder einen vorhandenen Kontakt bearbeiten, ohne Werte für die Eigenschaften FirstName und LastName angeben zu müssen. Darüber hinaus müssen Benutzer gültige Telefonnummern und E-Mail-Adressen angeben.

In dieser Iteration haben wir unserer Contact Manager-Anwendung die Validierungslogik auf einfachste Weise hinzugefügt. Das Mischen unserer Validierungslogik in unsere Controller-Logik wird uns jedoch langfristig Probleme bereiten. Unsere Anwendung wird im Laufe der Zeit schwieriger zu warten und zu modifizieren sein.

In der nächsten Iteration werden wir unsere Validierungslogik und Datenbankzugriffslogik aus unseren Controllern umgestalten. Wir werden mehrere Software-Design-Prinzipien nutzen, um eine losere gekoppelte und wartungsfähigere Anwendung zu erstellen.

> [!div class="step-by-step"]
> [Zurück](iteration-2-make-the-application-look-nice-cs.md)
> [Weiter](iteration-4-make-the-application-loosely-coupled-cs.md)
