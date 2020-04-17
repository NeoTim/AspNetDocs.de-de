---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 'Iteration #6 – Verwenden sie die testgesteuerte Entwicklung (C) | Microsoft Docs'
author: rick-anderson
description: In dieser sechsten Iteration fügen wir unserer Anwendung neue Funktionen hinzu, indem wir zuerst Komponententests schreiben und Code für die Komponententests schreiben. In dieser Iteration,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: d0e8f30a075cc79c7410ffe1b8bf02da2bd44443
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542325"
---
# <a name="iteration-6--use-test-driven-development-c"></a>Iteration 6 – Verwenden der testgesteuerten Entwicklung (C#)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> In dieser sechsten Iteration fügen wir unserer Anwendung neue Funktionen hinzu, indem wir zuerst Komponententests schreiben und Code für die Komponententests schreiben. In dieser Iteration fügen wir Kontaktgruppen hinzu.

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

In der vorherigen Iteration der Contact Manager-Anwendung haben wir Komponententests erstellt, um ein Sicherheitsnetz für unseren Code bereitzustellen. Die Motivation für die Erstellung der Komponententests war, unseren Code widerstandsfähiger gegen Veränderungen zu machen. Mit den Komponententests können wir gerne Änderungen an unserem Code vornehmen und sofort wissen, ob wir bestehende Funktionen gebrochen haben.

In dieser Iteration verwenden wir Komponententests für einen ganz anderen Zweck. In dieser Iteration verwenden wir Komponententests als Teil einer Anwendungsdesign-Philosophie namens *testgesteuerte Entwicklung*. Wenn Sie die testgesteuerte Entwicklung üben, schreiben Sie zuerst Tests und dann Code für die Tests.

Genauer gesagt, wenn Sie testgesteuerte Entwicklung üben, gibt es drei Schritte, die Sie beim Erstellen von Code ausführen (Rot/ Grün/Refaktor):

1. Schreiben eines Komponententests, der fehlschlägt (Rot)
2. Schreibcode, der den Komponententest besteht (Grün)
3. Refaktorieren Sie Ihren Code (Refactor)

Zuerst schreiben Sie den Komponententest. Der Komponententest sollte Ihre Absicht zum Ausdruck bringen, wie Sie sich von Ihrem Code verhalten. Wenn Sie den Komponententest zum ersten Mal erstellen, sollte der Komponententest fehlschlagen. Der Test sollte fehlschlagen, da Sie noch keinen Anwendungscode geschrieben haben, der den Test erfüllt.

Als Nächstes schreiben Sie gerade genug Code, damit der Komponententest bestanden werden kann. Das Ziel ist es, den Code auf die faulste, schlampigste und schnellstmögliche Weise zu schreiben. Sie sollten keine Zeit damit verschwenden, über die Architektur Ihrer Anwendung nachzudenken. Stattdessen sollten Sie sich darauf konzentrieren, die minimale Menge an Code zu schreiben, die erforderlich ist, um die durch den Komponententest ausgedrückte Absicht zu erfüllen.

Nachdem Sie genügend Code geschrieben haben, können Sie zurücktreten und die Gesamtarchitektur Ihrer Anwendung berücksichtigen. In diesem Schritt schreiben Sie Ihren Code um (umgestalten), indem Sie Softwareentwurfsmuster -- wie das Repository-Muster -- nutzen, damit Ihr Code sicherer ist. Sie können Ihren Code in diesem Schritt furchtlos umschreiben, da Ihr Code von Komponententests abgedeckt wird.

Es gibt viele Vorteile, die sich aus der Praxis der testgesteuerten Entwicklung ergeben. Erstens zwingt Sie die testgesteuerte Entwicklung dazu, sich auf Code zu konzentrieren, der eigentlich geschrieben werden muss. Da Sie sich ständig darauf konzentrieren, nur genug Code zu schreiben, um einen bestimmten Test zu bestehen, werden Sie daran gehindert, in das Unkraut zu wandern und riesige Mengen an Code zu schreiben, den Sie nie verwenden werden.

Zweitens zwingt Sie eine "Test First"-Entwurfsmethodik dazu, Code aus der Perspektive der Verwendung des Codes zu schreiben. Mit anderen Worten, wenn Sie testgesteuerte Entwicklung praktizieren, schreiben Sie Ihre Tests ständig aus Benutzersicht. Daher kann eine testgesteuerte Entwicklung zu saubereren und verständlicheren APIs führen.

Schließlich zwingt Sie die testgesteuerte Entwicklung dazu, Komponententests als Teil des normalen Prozesses des Schreibens einer Anwendung zu schreiben. Wenn ein Projekttermin näher rückt, ist das Testen in der Regel das erste, was aus dem Fenster geht. Wenn Sie testgesteuerte Entwicklung praktizieren, sind Sie dagegen eher tugendhaft beim Schreiben von Komponententests, da die testgesteuerte Entwicklung Komponententests für den Prozess des Erstellens einer Anwendung von zentraler Bedeutung macht.

> [!NOTE] 
> 
> Um mehr über die testgesteuerte Entwicklung zu erfahren, empfehle ich Ihnen, Michael Feathers Buch **Working Effectively with Legacy Code**zu lesen.

In dieser Iteration fügen wir unserer Contact Manager-Anwendung eine neue Funktion hinzu. Wir unterstützen Kontaktgruppen. Sie können Kontaktgruppen verwenden, um Ihre Kontakte in Kategorien wie Geschäfts- und Freundesgruppen zu organisieren.

Wir fügen diese neue Funktionalität zu unserer Anwendung hinzu, indem wir einen Prozess der testgesteuerten Entwicklung verfolgen. Wir schreiben zuerst unsere Komponententests und wir schreiben unseren gesamten Code für diese Tests.

## <a name="what-gets-tested"></a>Was getestet wird

Wie wir in der vorherigen Iteration erläutert haben, schreiben Sie in der Regel keine Komponententests für Datenzugriffslogik oder Ansichtslogik. Sie schreiben keine Komponententests für die Datenzugriffslogik, da der Zugriff auf eine Datenbank ein relativ langsamer Vorgang ist. Sie schreiben keine Komponententests für die Ansichtslogik, da für den Zugriff auf eine Ansicht ein Relativ langsamer Vorgang erforderlich ist. Sie sollten keinen Komponententest schreiben, es sei denn, der Test kann immer wieder sehr schnell ausgeführt werden

Da die testgesteuerte Entwicklung von Komponententests angetrieben wird, konzentrieren wir uns zunächst auf das Schreiben von Controllern und Geschäftslogik. Wir vermeiden es, die Datenbank oder Ansichten zu berühren. Wir werden die Datenbank nicht bis zum Ende dieses Tutorials ändern oder unsere Ansichten erstellen. Wir beginnen mit dem, was getestet werden kann.

## <a name="creating-user-stories"></a>Erstellen von User Stories

Wenn Sie eine testgesteuerte Entwicklung praktizieren, beginnen Sie immer mit dem Schreiben eines Tests. Das wirft sofort die Frage auf: Wie entscheidet man, welchen Test zuerst geschrieben werden soll? Um diese Frage zu beantworten, sollten Sie eine Reihe von [**User Storys**](http://en.wikipedia.org/wiki/User_stories)schreiben.

Eine User Story ist eine sehr kurze (in der Regel ein Satz) Beschreibung einer Softwareanforderung. Es sollte sich um eine nicht technische Beschreibung einer Anforderung handelt, die aus DerErspektiersicht geschrieben wurde.

Hier ist der Satz von User Storys, die die Funktionen beschreiben, die für die neue Kontaktgruppenfunktionalität erforderlich sind:

1. Der Benutzer kann eine Liste der Kontaktgruppen anzeigen.
2. Der Benutzer kann eine neue Kontaktgruppe erstellen.
3. Der Benutzer kann eine vorhandene Kontaktgruppe löschen.
4. Der Benutzer kann beim Erstellen eines neuen Kontakts eine Kontaktgruppe auswählen.
5. Der Benutzer kann beim Bearbeiten eines vorhandenen Kontakts eine Kontaktgruppe auswählen.
6. Eine Liste der Kontaktgruppen wird in der Indexansicht angezeigt.
7. Wenn ein Benutzer auf eine Kontaktgruppe klickt, wird eine Liste mit übereinstimmenden Kontakten angezeigt.

Beachten Sie, dass diese Liste von User Storys für einen Kunden vollständig verständlich ist. Von technischen Umsetzungsdetails ist nicht die Rede.

Während Sie Ihre Anwendung erstellen, können die Benutzerstorys verfeinert werden. Sie können eine User Story in mehrere Storys (Anforderungen) aufteilen. Sie können z. B. entscheiden, dass das Erstellen einer neuen Kontaktgruppe eine Validierung umfassen sollte. Das Senden einer Kontaktgruppe ohne Namen sollte einen Validierungsfehler zurückgeben.

Nachdem Sie eine Liste von User Storys erstellt haben, können Sie den ersten Komponententest schreiben. Zunächst erstellen wir einen Komponententest zum Anzeigen der Liste der Kontaktgruppen.

## <a name="listing-contact-groups"></a>Auflisten von Kontaktgruppen

Unsere erste User Story ist, dass ein Benutzer in der Lage sein sollte, eine Liste von Kontaktgruppen anzuzeigen. Wir müssen diese Geschichte mit einem Test ausdrücken.

Erstellen Sie einen neuen Komponententest, indem Sie im ContactManager.Tests-Projekt mit der rechten Maustaste auf den Ordner Controller klicken, **Hinzufügen, Neuer Test**auswählen und die **Komponententestvorlage** auswählen (siehe Abbildung 1). Benennen Sie den neuen Komponententest GroupControllerTest.cs, und klicken Sie auf die Schaltfläche **OK.**

[![Hinzufügen des GroupControllerTest-Komponententests](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**Abbildung 01**: Hinzufügen des GroupControllerTest-Komponententests ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image2.png))

Unser erster Komponententest ist in Listing 1 enthalten. Dieser Test überprüft, ob die Index()-Methode des Gruppencontrollers eine Gruppe von Gruppen zurückgibt. Der Test überprüft, ob eine Auflistung von Gruppen in Ansichtsdaten zurückgegeben wird.

**Auflisten 1 - Controller-GruppeControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Wenn Sie den Code zum ersten Mal in Liste 1 in Visual Studio eingeben, erhalten Sie viele rote Squiggly-Linien. Wir haben die GroupController- oder Group-Klassen nicht erstellt.

An diesem Punkt können wir nicht einmal unsere Anwendung erstellen, so dass wir nicht unseren ersten Komponententest ausführen können. Das ist gut. Das gilt als Fehltest. Daher haben wir jetzt die Berechtigung, mit dem Schreiben von Anwendungscode zu beginnen. Wir müssen genügend Code schreiben, um unseren Test auszuführen.

Die Gruppencontrollerklasse in Liste 2 enthält das absolute Minimum an Code, das erforderlich ist, um den Komponententest zu bestehen. Die Index()-Aktion gibt eine statisch codierte Liste von Gruppen zurück (die Gruppenklasse ist in Liste 3 definiert).

**Auflisten 2 - Controller-GruppeController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**Auflisten 3 - Models-Gruppe.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

Nachdem wir die Klassen GroupController und Group zu unserem Projekt hinzugefügt haben, wird unser erster Komponententest erfolgreich abgeschlossen (siehe Abbildung 2). Wir haben die minimale Arbeit geleistet, die erforderlich ist, um den Test zu bestehen. Es ist Zeit zu feiern.

[![Erfolg!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**Abbildung 02**: Erfolg! ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>Erstellen von Kontaktgruppen

Nun können wir zur zweiten User Story übergehen. Wir müssen in der Lage sein, neue Kontaktgruppen zu schaffen. Wir müssen diese Absicht mit einem Test zum Ausdruck bringen.

Der Test in Listing 4 überprüft, ob das Aufrufen der Create()-Methode mit einer neuen Gruppe die Gruppe zur Liste der Gruppen hinzufügt, die von der Index()-Methode zurückgegeben werden. Mit anderen Worten, wenn ich eine neue Gruppe erstelle, dann sollte ich in der Lage sein, die neue Gruppe aus der Liste der Gruppen zurückzubekommen, die von der Index()-Methode zurückgegeben werden.

**Auflisten 4 - Controller-GruppeControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

Der Test in Listing 4 ruft die Group Controller Create()-Methode mit einer neuen Kontaktgruppe auf. Als Nächstes überprüft der Test, ob der Aufruf der Group Controller Index()-Methode die neue Gruppe in Ansichtsdaten zurückgibt.

Der geänderte Gruppencontroller in Listing 5 enthält das absolute Minimum an Änderungen, die erforderlich sind, um den neuen Test zu bestehen.

**Auflisten 5 - Controller-GruppeController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>Der Gruppencontroller in Listing 5 verfügt über eine neue Create()-Aktion. Durch diese Aktion wird eine Gruppe zu einer Auflistung von Gruppen hinzugefügt. Beachten Sie, dass die Aktion Index() geändert wurde, um den Inhalt der Auflistung von Gruppen zurückzugeben.

Wieder einmal haben wir die minimale Menge an Arbeit geleistet, die erforderlich ist, um den Komponententest zu bestehen. Nachdem wir diese Änderungen am Gruppencontroller vorgenommen haben, sind alle unsere Komponententests erfolgreich.

## <a name="adding-validation"></a>Hinzufügen der Validierung

Diese Anforderung wurde in der User Story nicht explizit angegeben. Es ist jedoch vernünftig, von einer Gruppe einen Namen zu verlangen. Andernfalls wäre das Organisieren von Kontakten in Gruppen nicht sehr nützlich.

Liste 6 enthält einen neuen Test, der diese Absicht zum Ausdruck bringt. Dieser Test überprüft, ob der Versuch, eine Gruppe zu erstellen, ohne einen Namen anzugeben, zu einer Validierungsfehlermeldung im Modellstatus führt.

**Auflisten 6 - Controller-GruppeControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

Um diesen Test zu erfüllen, müssen wir unserer Gruppeklasse eine Name-Eigenschaft hinzufügen (siehe Liste 7). Darüber hinaus müssen wir unserer Create()-Aktion des Gruppencontrollers ein kleines bisschen Validierungslogik hinzufügen (siehe Liste 8).

**Auflisten 7 - Models-Gruppe.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**Auflisten 8 - Controller-GruppeController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

Beachten Sie, dass die Aktion Gruppencontroller Create() jetzt sowohl Validierung als auch Datenbanklogik enthält. Derzeit besteht die vom Gruppencontroller verwendete Datenbank aus nichts weiter als einer In-Memory-Auflistung.

## <a name="time-to-refactor"></a>Zeit für die Umgestaltung

Der dritte Schritt in Rot/Grün/Refaktor ist der Refactor-Teil. An dieser Stelle müssen wir von unserem Code zurücktreten und überlegen, wie wir unsere Anwendung umgestalten können, um ihr Design zu verbessern. Die Refactor-Phase ist die Phase, in der wir intensiv über die beste Art und Weise der Implementierung von Software-Design-Prinzipien und -Mustern nachdenken.

Es steht uns frei, unseren Code in jeder Weise zu ändern, die wir wählen, um das Design des Codes zu verbessern. Wir verfügen über ein Sicherheitsnetz von Komponententests, die verhindern, dass wir bestehende Funktionen brechen.

Im Moment ist unser Group Controller ein Durcheinander aus der Perspektive eines guten Software-Designs. Der Gruppencontroller enthält ein verworrenes Durcheinander von Validierungs- und Datenzugriffscode. Um zu vermeiden, dass gegen das Prinzip der einheitlichen Verantwortung verstoßen wird, müssen wir diese Bedenken in verschiedene Klassen unterteilen.

Unsere umgesierte Gruppencontrollerklasse ist in Listing 9 enthalten. Der Controller wurde geändert, um die ContactManager-Dienstschicht zu verwenden. Dies ist die gleiche Dienstebene, die wir mit dem Contact-Controller verwenden.

Liste 10 enthält die neuen Methoden, die dem ContactManager-Dienst-Layer hinzugefügt wurden, um das Überprüfen, Auflisten und Erstellen von Gruppen zu unterstützen. Die IContactManagerService-Schnittstelle wurde aktualisiert, um die neuen Methoden einzuschließen.

Listing 11 enthält eine neue FakeContactManagerRepository-Klasse, die die IContactManagerRepository-Schnittstelle implementiert. Im Gegensatz zur EntityContactManagerRepository-Klasse, die auch die IContactManagerRepository-Schnittstelle implementiert, kommuniziert unsere neue FakeContactManagerRepository-Klasse nicht mit der Datenbank. Die FakeContactManagerRepository-Klasse verwendet eine In-Memory-Auflistung als Proxy für die Datenbank. Wir verwenden diese Klasse in unseren Komponententests als gefälschte Repository-Schicht.

**Auflisten 9 - Controller-GruppeController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**Auflisten 10 - Controller-KontaktManagerService.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**Auflisten 11 - Controller-FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

Das Ändern der IContactManagerRepository-Schnittstelle erfordert die Verwendung zum Implementieren der Methoden CreateGroup() und ListGroups() in der EntityContactManagerRepository-Klasse. Der faulste und schnellste Weg, dies zu tun, ist Stub-Methoden hinzuzufügen, die wie folgt aussehen:   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

Schließlich erfordern diese Änderungen am Design unserer Anwendung, dass wir einige Änderungen an unseren Komponententests vornehmen müssen. Wir müssen nun das FakeContactManagerRepository verwenden, wenn wir die Komponententests durchführen. Die aktualisierte GroupControllerTest-Klasse ist in Liste 12 enthalten.

**Auflisten 12 - Controller-GruppeControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

Nachdem wir all diese Änderungen vorgenommen haben, sind alle unsere Komponententests noch einmal erfolgreich. Wir haben den gesamten Zyklus von Rot/Grün/Refactor abgeschlossen. Wir haben die ersten beiden User Storys implementiert. Wir haben jetzt unterstützende Komponententests für die Anforderungen, die in den User Storys ausgedrückt werden. Die Implementierung der restlichen User Storys beinhaltet die Wiederholung des gleichen Zyklus von Rot/Grün/Refactor.

## <a name="modifying-our-database"></a>Ändern unserer Datenbank

Obwohl wir alle Anforderungen unserer Komponententests erfüllt haben, ist unsere Arbeit leider nicht getan. Wir müssen unsere Datenbank noch ändern.

Wir müssen eine neue Gruppendatenbanktabelle erstellen. Folgen Sie diesen Schritten:

1. Klicken Sie im Fenster Server-Explorer mit der rechten Maustaste auf den Ordner Tabellen, und wählen Sie die Menüoption **Neue Tabelle hinzufügen**aus.
2. Geben Sie die beiden unten im Tabellen-Designer beschriebenen Spalten ein.
3. Markieren Sie die ID-Spalte als Primärschlüssel und Identitätsspalte.
4. Speichern Sie die neue Tabelle mit dem Namen Gruppen, indem Sie auf das Symbol der Diskette klicken.

<a id="0.11_table01"></a>

| **Spaltenname** | **Datentyp** | **Nullen zulassen** |
| --- | --- | --- |
| Id | INT | False |
| Name | nvarchar(50) | False |

Als Nächstes müssen wir alle Daten aus der Tabelle Kontakte löschen (sonst können wir keine Beziehung zwischen den Tabellen Kontakte und Gruppen erstellen). Folgen Sie diesen Schritten:

1. Klicken Sie mit der rechten Maustaste auf die Tabelle Kontakte, und wählen Sie die Menüoption **Tabellendaten anzeigen**aus.
2. Löschen Sie alle Zeilen.

Als Nächstes müssen wir eine Beziehung zwischen der Datenbanktabelle Gruppen und der vorhandenen Kontakte-Datenbanktabelle definieren. Folgen Sie diesen Schritten:

1. Doppelklicken Sie im Fenster Server-Explorer auf die Tabelle Kontakte, um den Tabellen-Designer zu öffnen.
2. Fügen Sie der Tabelle Contacts mit dem Namen GroupId eine neue Ganzzahlspalte hinzu.
3. Klicken Sie auf die Schaltfläche Beziehung, um das Dialogfeld Fremdschlüsselbeziehungen zu öffnen (siehe Abbildung 3).
4. Klicken Sie auf die Schaltfläche Hinzufügen.
5. Klicken Sie auf die Schaltfläche Auslassung, die neben der Schaltfläche Tabellen- und Spaltenspezifikation angezeigt wird.
6. Wählen Sie im Dialogfeld Tabellen und Spalten Gruppen als Primärschlüsseltabelle und ID als Primärschlüsselspalte aus. Wählen Sie Kontakte als Fremdschlüsseltabelle und GroupId als Fremdschlüsselspalte aus (siehe Abbildung 4). Klicken Sie auf die Schaltfläche "OK".
7. Wählen Sie unter **INSERT und UPDATE Specification**den Wert **Kaskadierung** für **Löschregel**aus.
8. Klicken Sie auf die Schaltfläche Schließen, um das Dialogfeld Fremdschlüsselbeziehungen zu schließen.
9. Klicken Sie auf die Schaltfläche Speichern, um die Änderungen in der Tabelle Kontakte zu speichern.

[![Erstellen einer Datenbanktabellenbeziehung](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**Abbildung 03**: Erstellen einer Datenbanktabellenbeziehung ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image6.png))

[![Angeben von Tabellenbeziehungen](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**Abbildung 04**: Angeben von Tabellenbeziehungen([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](iteration-6-use-test-driven-development-cs/_static/image8.png)

### <a name="updating-our-data-model"></a>Aktualisieren unseres Datenmodells

Als Nächstes müssen wir unser Datenmodell aktualisieren, um die neue Datenbanktabelle darzustellen. Folgen Sie diesen Schritten:

1. Doppelklicken Sie im Ordner "Modelle", um den Entitäts-Designer zu öffnen, doppelklicken Sie auf die Datei ContactManagerModel.edmx.
2. Klicken Sie mit der rechten Maustaste auf die Designer-Oberfläche, und wählen Sie die Menüoption **Modell aus Datenbank aktualisieren**aus.
3. Wählen Sie im Update-Assistenten die Tabelle Gruppen aus, und klicken Sie auf die Schaltfläche Fertig stellen (siehe Abbildung 5).
4. Klicken Sie mit der rechten Maustaste auf die Entität Gruppen, und wählen Sie die Menüoption **Umbenennen**aus. Ändern Sie den Namen der *Entität Gruppen* in *Gruppe* (Singular).
5. Klicken Sie mit der rechten Maustaste auf die Navigationseigenschaft Gruppen, die am unteren Rand der Kontaktentität angezeigt wird. Ändern Sie den Namen der *Navigationseigenschaft Gruppen* in *Gruppe* (Singular).

[![Aktualisieren eines Entity Framework-Modells aus der Datenbank](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**Abbildung 05**: Aktualisieren eines Entity[Framework-Modells](iteration-6-use-test-driven-development-cs/_static/image10.png)aus der Datenbank (Klicken Sie hier, um das Bild in voller Größe anzuzeigen )

Nachdem Sie diese Schritte ausgeführt haben, stellt das Datenmodell sowohl die Tabellen Kontakte als auch Gruppen dar. Der Entitäts-Designer sollte beide Entitäten anzeigen (siehe Abbildung 6).

[![Entity Designer zeigt Gruppe und Kontakt an](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**Abbildung 06**: Entity Designer zeigt Gruppe und Kontakt an ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image12.png))

### <a name="creating-our-repository-classes"></a>Erstellen unserer Repository-Klassen

Als Nächstes müssen wir unsere Repository-Klasse implementieren. Im Laufe dieser Iteration haben wir der IContactManagerRepository-Schnittstelle mehrere neue Methoden hinzugefügt, während wir Code geschrieben haben, um unsere Komponententests zu erfüllen. Die endgültige Version der IContactManagerRepository-Schnittstelle ist in Liste 14 enthalten.

**Auflisten 14 - Modelle-IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

Wir haben keine der Methoden implementiert, die mit Kontaktgruppen zusammenhängen. Derzeit verfügt die EntityContactManagerRepository-Klasse über Stubmethoden für jede der Kontaktgruppenmethoden, die in der IContactManagerRepository-Schnittstelle aufgeführt sind. Die ListGroups()-Methode sieht z. B. derzeit wie folgt aus:

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

Die Stub-Methoden ermöglichten es uns, unsere Anwendung zu kompilieren und die Komponententests zu bestehen. Jetzt ist es jedoch an der Zeit, diese Methoden tatsächlich umzusetzen. Die endgültige Version der EntityContactManagerRepository-Klasse ist in Liste 13 enthalten.

**Auflisten 13 - Modelle-EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>Erstellen der Ansichten

ASP.NET MVC-Anwendung, wenn Sie das standardmäßige ASP.NET-Ansichtsmodul verwenden. Sie erstellen also keine Ansichten als Reaktion auf einen bestimmten Komponententest. Da eine Anwendung jedoch ohne Ansichten nutzlos wäre, können wir diese Iteration nicht abschließen, ohne die in der Contact Manager-Anwendung enthaltenen Ansichten zu erstellen und zu ändern.

Wir müssen die folgenden neuen Ansichten für die Verwaltung von Kontaktgruppen erstellen (siehe Abbildung 7):

- Ansichten- & Gruppen-Index.aspx - Zeigt liste der Kontaktgruppen an
- Ansichten- "Gruppe" –Bestätigungsformular zum Löschen einer Kontaktgruppe an

[![Die Gruppenindexansicht](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**Abbildung 07**: Die Gruppenindexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image14.png))

Wir müssen die folgenden vorhandenen Ansichten so ändern, dass sie Kontaktgruppen enthalten:

- Ansichten, Home, Create.aspx
- Ansichten, Home, Edit.aspx
- Ansichten, Home, Index.aspx

Sie können die geänderten Ansichten anzeigen, indem Sie sich die Visual Studio-Anwendung ansehen, die diesem Tutorial beiliegt. Abbildung 8 zeigt z. B. die Kontaktindexansicht.

[![Die Kontaktindexansicht](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**Abbildung 08**: Die Kontaktindex-Ansicht([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-6-use-test-driven-development-cs/_static/image16.png))

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir unserer Contact Manager-Anwendung neue Funktionen hinzugefügt, indem wir einer testgesteuerten Entwicklungsanwendungsentwurfsmethode folgen. Wir begannen mit der Erstellung einer Reihe von User Storys. Wir haben eine Reihe von Komponententests erstellt, die den Anforderungen der User Storys entsprechen. Schließlich haben wir gerade genug Code geschrieben, um die Anforderungen der Komponententests zu erfüllen.

Nachdem wir mit dem Schreiben von genügend Code fertig waren, um die Anforderungen der Komponententests zu erfüllen, haben wir unsere Datenbank und Unsere Ansichten aktualisiert. Wir haben unserer Datenbank eine neue Gruppentabelle hinzugefügt und unser Entity Framework-Datenmodell aktualisiert. Wir haben auch eine Reihe von Ansichten erstellt und geändert.

In der nächsten Iteration -- der letzten Iteration -- schreiben wir unsere Anwendung neu, um die Vorteile von Ajax zu nutzen. Durch die Nutzung von Ajax verbessern wir die Reaktionsfähigkeit und Leistung der Contact Manager-Anwendung.

> [!div class="step-by-step"]
> [Zurück](iteration-5-create-unit-tests-cs.md)
> [Weiter](iteration-7-add-ajax-functionality-cs.md)
