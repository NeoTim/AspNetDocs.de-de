---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 'Iteration #5 – Erstellen von Komponententests (VB) | Microsoft Docs'
author: rick-anderson
description: In der fünften Iteration erleichtern wir die Wartung und Änderung unserer Anwendung durch Hinzufügen von Komponententests. Wir verspotten unsere Datenmodellklassen und erstellen Komponententests für o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: cc5425de86e7481894fbea242fa555b5598167f6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542338"
---
# <a name="iteration-5--create-unit-tests-vb"></a>Iteration 5 – Erstellen von Komponententests (VB)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> In der fünften Iteration erleichtern wir die Wartung und Änderung unserer Anwendung durch Hinzufügen von Komponententests. Wir verspotten unsere Datenmodellklassen und erstellen Komponententests für unsere Controller und Validierungslogik.

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

In der vorherigen Iteration der Contact Manager-Anwendung haben wir die Anwendung so umgestaltet, dass sie lockerer gekoppelt ist. Wir haben die Anwendung in unterschiedliche Controller-, Service- und Repository-Layer unterteilt. Jede Ebene interagiert über Schnittstellen mit der darunter liegenden Ebene.

Wir haben die Anwendung umgestaltet, um die Anwendung einfacher zu warten und zu modifizieren. Wenn wir beispielsweise eine neue Datenzugriffstechnologie verwenden müssen, können wir einfach die Repository-Schicht ändern, ohne den Controller oder die Service-Ebene zu berühren. Indem wir den Contact Manager lose gekoppelt haben, haben wir die Anwendung widerstandsfähiger für Änderungen gemacht.

Aber was passiert, wenn wir der Contact Manager-Anwendung eine neue Funktion hinzufügen müssen? Oder was passiert, wenn wir einen Fehler beheben? Eine traurige, aber gut bewiesene Wahrheit beim Schreiben von Code ist, dass, wenn Sie Code berühren, Sie das Risiko der Einführung neuer Fehler schaffen.

An einem schönen Tag kann Ihr Vorgesetzter Sie beispielsweise bitten, dem Kontakt-Manager eine neue Funktion hinzuzufügen. Sie möchte, dass Sie Unterstützung für Kontaktgruppen hinzufügen. Sie möchte, dass Sie Benutzern ermöglichen, ihre Kontakte in Gruppen wie Freunde, Unternehmen usw. zu organisieren.

Um diese neue Funktion zu implementieren, müssen Sie alle drei Layer der Contact Manager-Anwendung ändern. Sie müssen den Controllern, dem Service-Layer und dem Repository neue Funktionen hinzufügen. Sobald Sie mit dem Ändern von Code beginnen, besteht die Gefahr, dass Die zuvor funktionierenden Funktionen beeinträchtigt werden.

Die Umgestaltung unserer Anwendung in separate Ebenen, wie wir es in der vorherigen Iteration getan haben, war eine gute Sache. Es war eine gute Sache, weil es uns ermöglicht, Änderungen an ganzen Ebenen vorzunehmen, ohne den Rest der Anwendung zu berühren. Wenn Sie jedoch den Code innerhalb einer Ebene einfacher verwalten und ändern möchten, müssen Sie Komponententests für den Code erstellen.

Sie verwenden einen Komponententest, um eine einzelne Codeeinheit zu testen. Diese Codeeinheiten sind kleiner als die gesamten Anwendungsebenen. In der Regel verwenden Sie einen Komponententest, um zu überprüfen, ob sich eine bestimmte Methode im Code so verhält, wie Sie es erwarten. Sie würden z. B. einen Komponententest für die CreateContact()-Methode erstellen, die von der ContactManagerService-Klasse verfügbar gemacht wird.

Die Komponententests für eine Anwendung funktionieren wie ein Sicherheitsnetz. Wenn Sie Code in einer Anwendung ändern, können Sie eine Reihe von Komponententests ausführen, um zu überprüfen, ob die Änderung vorhandene Funktionen beeinträchtigt. Komponententests machen den Code sicher zu ändern. Komponententests machen den gesamten Code in Ihrer Anwendung widerstandsfähiger für Änderungen.

In dieser Iteration fügen wir Komponententests zu unserer Contact Manager-Anwendung hinzu. Auf diese Weise können wir in der nächsten Iteration Kontaktgruppen zu unserer Anwendung hinzufügen, ohne sich Gedanken über die Verletzung vorhandener Funktionen machen zu müssen.

> [!NOTE] 
> 
> Es gibt eine Vielzahl von Komponententestframeworks, einschließlich NUnit, xUnit.net und MbUnit. In diesem Tutorial verwenden wir das in Visual Studio enthaltene Komponententestframework. Sie können jedoch genauso einfach einen dieser alternativen Frameworks verwenden.

## <a name="what-gets-tested"></a>Was getestet wird

In der perfekten Welt würde Ihr codealler Code durch Komponententests abgedeckt werden. In der perfekten Welt hätten Sie das perfekte Sicherheitsnetz. Sie könnten jede Codezeile in Ihrer Anwendung ändern und sofort durch ausführen der Komponententests wissen, ob die Änderung die vorhandene Funktionalität gebrochen hat.

Wir leben jedoch nicht in einer perfekten Welt. In der Praxis konzentrieren Sie sich beim Schreiben von Komponententests auf das Schreiben von Tests für Ihre Geschäftslogik (z. B. Validierungslogik). Insbesondere schreiben Sie *keine* Komponententests für Ihre Datenzugriffslogik oder Ihre Ansichtslogik.

Um nützlich zu sein, müssen Komponententests sehr schnell ausgeführt werden. Sie können problemlos Hunderte (oder sogar Tausende) von Komponententests für eine Anwendung ansammeln. Wenn die Ausführung der Komponententests lange dauert, vermeiden Sie die Ausführung. Mit anderen Worten, lange laufende Komponententests sind für tägliche Codierungszwecke nutzlos.

Aus diesem Grund schreiben Sie in der Regel keine Komponententests für Code, der mit einer Datenbank interagiert. Das Ausführen von Hunderten von Komponententests für eine Live-Datenbank wäre zu langsam. Stattdessen verspotten Sie Ihre Datenbank und schreiben Code, der mit der Mock-Datenbank interagiert (wir besprechen das Verspotten einer Datenbank unten).

Aus einem ähnlichen Grund schreiben Sie in der Regel keine Komponententests für Ansichten. Um eine Ansicht zu testen, müssen Sie einen Webserver ausdrehen. Da das Aufdrehen eines Webservers ein relativ langsamer Prozess ist, wird das Erstellen von Komponententests für Ihre Ansichten nicht empfohlen.

Wenn Ihre Ansicht komplizierte Logik enthält, sollten Sie erwägen, die Logik in Helper-Methoden zu verschieben. Sie können Komponententests für Helper-Methoden schreiben, die ausgeführt werden, ohne einen Webserver zu drehen.

> [!NOTE] 
> 
> Während das Schreiben von Tests für Datenzugriffslogik oder Ansichtslogik keine gute Idee beim Schreiben von Komponententests ist, können diese Tests beim Erstellen von Funktions- oder Integrationstests sehr wertvoll sein.

> [!NOTE] 
> 
> ASP.NET MVC ist die Web Forms View Engine. Während das Web Forms View Engine von einem Webserver abhängig ist, sind andere Ansichtsmodule dies möglicherweise nicht.

## <a name="using-a-mock-object-framework"></a>Verwenden eines Mock-Objektframeworks

Beim Erstellen von Komponententests müssen Sie fast immer ein Mock Object-Framework nutzen. Mit einem Mock Object-Framework können Sie Mocks und Stubs für die Klassen in Ihrer Anwendung erstellen.

Sie können z. B. ein Mock Object-Framework verwenden, um eine Mock-Version Ihrer Repository-Klasse zu generieren. Auf diese Weise können Sie die Mock-Repository-Klasse anstelle der echten Repository-Klasse in Ihren Komponententests verwenden. Durch die Verwendung des Mock-Repositorys können Sie die Ausführung von Datenbankcode beim Ausführen eines Komponententests vermeiden.

Visual Studio enthält kein Mock Object-Framework. Es stehen jedoch mehrere kommerzielle und Open-Source-Mock-Objekt-Frameworks für das .NET-Framework zur Verfügung:

1. Moq - Dieses Framework ist unter der Open-Source-BSD-Lizenz verfügbar. Sie können Moq [https://code.google.com/p/moq/](https://code.google.com/p/moq/)von herunterladen.
2. Rhino Mocks - Dieses Framework ist unter der Open-Source-BSD-Lizenz verfügbar. Sie können Rhino Mocks von [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)herunterladen.
3. Typemock Isolator - Dies ist ein kommerzieller Rahmen. Sie können eine Testversion von [http://www.typemock.com/](http://www.typemock.com/)herunterladen.

In diesem Tutorial habe ich beschlossen, Moq zu verwenden. Sie können jedoch genauso einfach Rhino Mocks oder Typemock Isolator verwenden, um die Mock-Objekte für die Contact Manager-Anwendung zu erstellen.

Bevor Sie Moq verwenden können, müssen Sie die folgenden Schritte ausführen:

1. .
2. Bevor Sie den Download entpacken, stellen Sie sicher, dass Sie mit der rechten Maustaste auf die Datei klicken und auf die Schaltfläche **"Entsperren"** klicken (siehe Abbildung 1).
3. Entpacken Sie den Download.
4. Fügen Sie dem Testprojekt einen Verweis auf die Moq-Baugruppe hinzu, indem Sie die Menüoption **Projekt, Referenz hinzufügen auswählen,** um das Dialogfeld **Referenz hinzufügen** zu öffnen. Navigieren Sie auf der Registerkarte Durchsuchen zu dem Ordner, in dem Sie Moq entpackt haben, und wählen Sie die Moq.dll-Assembly aus. Klicken Sie auf die Schaltfläche **OK** (siehe Abbildung 2).

[![Entsperren von Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**Abbildung 01**: Entsperren von Moq([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-5-create-unit-tests-vb/_static/image2.png))

[![Referenzen nach dem Hinzufügen von Moq](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**Abbildung 02**: Referenzen nach dem Hinzufügen von Moq([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-5-create-unit-tests-vb/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>Erstellen von Komponententests für die Dienstschicht

Beginnen wir mit dem Erstellen einer Reihe von Komponententests für die Serviceschicht unserer Contact Manager-Anwendung. Wir verwenden diese Tests, um unsere Validierungslogik zu überprüfen.

Erstellen Sie im ContactManager.Tests-Projekt einen neuen Ordner mit dem Namen "Modelle". Klicken Sie als Nächstes mit der rechten Maustaste auf den Ordner "Modelle" und wählen Sie **Hinzufügen, Neuer Test**aus. Das Dialogfeld **"Neuer Test hinzufügen"** in Abbildung 3 wird angezeigt. Wählen Sie die **Komponententestvorlage** aus, und benennen Sie den neuen Test ContactManagerServiceTest.vb. Klicken Sie auf die Schaltfläche **OK,** um den neuen Test zu Ihrem Testprojekt hinzuzufügen.

> [!NOTE] 
> 
> Im Allgemeinen soll die Ordnerstruktur des Testprojekts mit der Ordnerstruktur Ihres ASP.NET MVC-Projekts übereinstimmen. Beispielsweise platzieren Sie Controllertests in einem Controllerordner, Modelltests in einem Ordner "Modelle" usw.

[![Modelle-KontaktManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**Abbildung 03**: Models-ContactManagerServiceTest.cs([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](iteration-5-create-unit-tests-vb/_static/image6.png)

Zunächst möchten wir die CreateContact()-Methode testen, die von der ContactManagerService-Klasse verfügbar gemacht wird. Wir erstellen die folgenden fünf Tests:

- CreateContact() - Tests, die CreateContact() gibt den Wert true zurück, wenn ein gültiger Kontakt an die Methode übergeben wird.
- CreateContactRequiredFirstName() - Testet, ob eine Fehlermeldung zum Modellstatus hinzugefügt wird, wenn ein Kontakt mit einem fehlenden Vornamen an die CreateContact()-Methode übergeben wird.
- CreateContactRequiredLastName() - Testet, ob eine Fehlermeldung zum Modellstatus hinzugefügt wird, wenn ein Kontakt mit einem fehlenden Nachnamen an die CreateContact()-Methode übergeben wird.
- CreateContactInvalidPhone() - Testet, ob dem Modellstatus eine Fehlermeldung hinzugefügt wird, wenn ein Kontakt mit einer ungültigen Telefonnummer an die CreateContact()-Methode übergeben wird.
- CreateContactInvalidEmail() - Testet, ob dem Modellstatus eine Fehlermeldung hinzugefügt wird, wenn ein Kontakt mit einer ungültigen E-Mail-Adresse an die CreateContact()-Methode übergeben wird.

Der erste Test überprüft, ob ein gültiger Kontakt keinen Validierungsfehler generiert. Die verbleibenden Tests überprüfen die einzelnen Validierungsregeln.

Der Code für diese Tests ist in Liste 1 enthalten.

**Auflisten 1 - Modelle-ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

Da wir die Contact-Klasse in Liste 1 verwenden, müssen wir unserem Testprojekt einen Verweis auf das Microsoft Entity Framework hinzufügen. Fügen Sie einen Verweis auf die System.Data.Entity-Assembly hinzu.

Liste 1 enthält eine Methode mit dem Namen Initialize(), die mit dem Attribut [TestInitialize] versehen ist. Diese Methode wird automatisch aufgerufen, bevor jeder komponententest ausgeführt wird (es wird 5 Mal direkt vor jedem Komponententest aufgerufen). Die Initialize()-Methode erstellt ein Mock-Repository mit der folgenden Codezeile:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

Diese Codezeile verwendet das Moq-Framework, um ein Mock-Repository über die IContactManagerRepository-Schnittstelle zu generieren. Das Mock-Repository wird anstelle des eigentlichen EntityContactManagerRepository verwendet, um den Zugriff auf die Datenbank zu vermeiden, wenn jeder Komponententest ausgeführt wird. Das Mock-Repository implementiert die Methoden der IContactManagerRepository-Schnittstelle, aber die Methoden tun eigentlich nichts.

> [!NOTE] 
> 
> Bei Verwendung des Moq-Frameworks \_wird zwischen \_mockRepository und mockRepository.Object unterschieden. Erstere bezieht sich auf die Mock(Of IContactManagerRepository)-Klasse, die Methoden zum Angeben des Verhaltens des Mock-Repositorys enthält. Letzteres bezieht sich auf das eigentliche Mock-Repository, das die IContactManagerRepository-Schnittstelle implementiert.

Das Mock-Repository wird in der Initialize()-Methode beim Erstellen einer Instanz der ContactManagerService-Klasse verwendet. Alle einzelnen Komponententests verwenden diese Instanz der ContactManagerService-Klasse.

Liste 1 enthält fünf Methoden, die jedem komponententest entsprechen. Jede dieser Methoden ist mit dem Attribut [TestMethod] versehen. Wenn Sie die Komponententests ausführen, wird jede Methode mit diesem Attribut aufgerufen. Mit anderen Worten, jede Methode, die mit dem [TestMethod]-Attribut versehen ist, ist ein Komponententest.

Der erste Komponententest mit dem Namen CreateContact() überprüft, ob der Aufruf von CreateContact() den Wert true zurückgibt, wenn eine gültige Instanz der Contact-Klasse an die Methode übergeben wird. Der Test erstellt eine Instanz der Contact-Klasse, ruft die CreateContact()-Methode auf und überprüft, ob CreateContact() den Wert true zurückgibt.

Die verbleibenden Tests überprüfen, dass beim Aufruf der CreateContact(-Methode mit einem ungültigen Kontakt die Methode false zurückgibt und die erwartete Validierungsfehlermeldung dem Modellstatus hinzugefügt wird. Beispielsweise erstellt der CreateContactRequiredFirstName()-Test eine Instanz der Contact-Klasse mit einer leeren Zeichenfolge für ihre FirstName-Eigenschaft. Als Nächstes wird die CreateContact()-Methode mit dem ungültigen Kontakt aufgerufen. Schließlich überprüft der Test, ob CreateContact() false zurückgibt und dass der Modellstatus die erwartete Validierungsfehlermeldung "Vorname ist erforderlich" enthält.

Sie können die Komponententests in Liste 1 ausführen, indem Sie die Menüoption **Testen, Ausführen, Alle Tests in Lösung (STRG+R, A)** auswählen. Die Ergebnisse der Tests werden im Fenster Testergebnisse angezeigt (siehe Abbildung 4).

[![Testergebnisse](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**Abbildung 04**: Testergebnisse ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-5-create-unit-tests-vb/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>Erstellen von Komponententests für Controller

ASP.NET MVC-Anwendung steuert den Fluss der Benutzerinteraktion. Beim Testen eines Controllers möchten Sie testen, ob der Controller das richtige Aktionsergebnis zurückgibt, und Daten anzeigen. Sie können auch testen, ob ein Controller mit Modellklassen in der erwarteten Weise interagiert.

Beispielsweise enthält Liste 2 zwei Komponententests für die Contact Controller Create()-Methode. Der erste Komponententest überprüft, ob die Create(-Methode an die Index-Aktion umgeleitet wird, wenn ein gültiger Kontakt an die Create()-Methode übergeben wird. Mit anderen Worten, wenn ein gültiger Kontakt übergeben wird, sollte die Create()-Methode ein RedirectToRouteResult zurückgeben, das die Indexaktion darstellt.

Wir möchten die ContactManager-Dienstschicht nicht testen, wenn wir die Controllerschicht testen. Daher spotten wir die Dienstschicht mit dem folgenden Code in der Initialize-Methode:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

Im Komponententest CreateValidContact() wird das Verhalten des Aufrufens der Service-Layer-Methode CreateContact() mit der folgenden Codezeile verspottet:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

Diese Codezeile bewirkt, dass der mock ContactManager-Dienst den Wert true zurückgibt, wenn seine CreateContact()-Methode aufgerufen wird. Durch Mocking auf der Dienstebene können wir das Verhalten unseres Controllers testen, ohne Code in der Dienstebene ausführen zu müssen.

Der zweite Komponententest überprüft, ob die Aktion Create() die Ansicht Erstellen zurückgibt, wenn ein ungültiger Kontakt an die Methode übergeben wird. Wir bewirken, dass die Service-Layer-Methode CreateContact() den Wert false mit der folgenden Codezeile zurückgibt:

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

Wenn sich die Create()-Methode wie erwartet verhält, sollte sie die Ansicht Erstellen zurückgeben, wenn der Service-Layer den Wert false zurückgibt. Auf diese Weise kann der Controller die Validierungsfehlermeldungen in der Ansicht Erstellen anzeigen, und der Benutzer hat die Möglichkeit, diese ungültigen Kontakteigenschaften zu korrigieren.

Wenn Sie Komponententests für Ihre Controller erstellen möchten, müssen Sie explizite Ansichtsnamen aus den Controlleraktionen zurückgeben. Geben Sie z. B. eine Ansicht wie folgt nicht zurück:

Rücklaufansicht()

Geben Sie stattdessen die Ansicht wie folgt zurück:

Rückgabeansicht("Erstellen")

Wenn Sie beim Zurückgeben einer Ansicht nicht explizit sind, gibt die ViewResult.ViewName-Eigenschaft eine leere Zeichenfolge zurück.

**Auflisten 2 - Controller-KontaktControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir Komponententests für unsere Contact Manager-Anwendung erstellt. Wir können diese Komponententests jederzeit ausführen, um zu überprüfen, ob sich unsere Anwendung weiterhin so verhält, wie wir es erwarten. Die Komponententests dienen als Sicherheitsnetz für unsere Anwendung und ermöglichen es uns, unsere Anwendung in Zukunft sicher zu modifizieren.

Wir haben zwei Sätze von Komponententests erstellt. Zuerst haben wir unsere Validierungslogik getestet, indem wir Komponententests für unsere Serviceschicht erstellt haben. Als nächstes haben wir unsere Flusssteuerungslogik getestet, indem wir Komponententests für unsere Controller-Schicht erstellt haben. Beim Testen unserer Service-Schicht haben wir unsere Tests für unsere Service-Schicht von unserer Repository-Schicht isoliert, indem wir unsere Repository-Schicht verspottet haben. Beim Testen der Controller-Schicht haben wir unsere Tests für unsere Controller-Schicht isoliert, indem wir die Service-Schicht verspottet haben.

In der nächsten Iteration ändern wir die Contact Manager-Anwendung so, dass sie Kontaktgruppen unterstützt. Wir fügen diese neue Funktionalität zu unserer Anwendung hinzu, indem wir einen Softwaredesignprozess namens Test-gesteuerte Entwicklung verwenden.

> [!div class="step-by-step"]
> [Zurück](iteration-4-make-the-application-loosely-coupled-vb.md)
> [Weiter](iteration-6-use-test-driven-development-vb.md)
