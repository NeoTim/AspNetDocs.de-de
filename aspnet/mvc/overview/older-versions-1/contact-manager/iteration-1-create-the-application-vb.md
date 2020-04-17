---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 'Iteration #1 – Erstellen der Anwendung (VB) | Microsoft Docs'
author: rick-anderson
description: 'In der ersten Iteration erstellen wir den Contact Manager auf einfachste Weise. Wir fügen Unterstützung für grundlegende Datenbankvorgänge hinzu: Erstellen, Lesen, Aktualisieren und D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542533"
---
# <a name="iteration-1--create-the-application-vb"></a>Iteration 1 – Erstellen der Anwendung (VB)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> In der ersten Iteration erstellen wir den Contact Manager auf einfachste Weise. Wir fügen Unterstützung für grundlegende Datenbankvorgänge hinzu: Erstellen, Lesen, Aktualisieren und Löschen (CRUD).

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

In dieser ersten Iteration erstellen wir die Basisanwendung. Ziel ist es, den Contact Manager so schnell und einfach wie möglich aufzubauen. In späteren Iterationen verbessern wir das Design der Anwendung.

Die Contact Manager-Anwendung ist eine grundlegende datenbankgesteuerte Anwendung. Sie können die Anwendung verwenden, um neue Kontakte zu erstellen, vorhandene Kontakte zu bearbeiten und Kontakte zu löschen.

In dieser Iteration führen wir die folgenden Schritte aus:

1. ASP.NET MVC-Anwendung
2. Erstellen einer Datenbank zum Speichern unserer Kontakte
3. Generieren einer Modellklasse für unsere Datenbank mit Microsoft Entity Framework
4. Erstellen Sie eine Controlleraktion und -ansicht, die es uns ermöglicht, alle Kontakte in der Datenbank aufzulisten.
5. Erstellen von Controlleraktionen und einer Ansicht, die es uns ermöglicht, einen neuen Kontakt in der Datenbank zu erstellen
6. Erstellen von Controlleraktionen und einer Ansicht, die es uns ermöglicht, einen vorhandenen Kontakt in der Datenbank zu bearbeiten
7. Erstellen von Controlleraktionen und einer Ansicht, die es uns ermöglicht, einen vorhandenen Kontakt in der Datenbank zu löschen

## <a name="software-prerequisites"></a>Erforderliche Software

In ASP.NET MVC-Anwendungen müssen Sie entweder Visual Studio 2008 oder Visual Web Developer 2008 auf Ihrem Computer installiert haben (Visual Web Developer ist eine kostenlose Version von Visual Studio, die nicht alle erweiterten Funktionen von Visual Studio enthält). Sie können entweder die Testversion von Visual Studio 2008 oder Visual Web Developer von der folgenden Adresse herunterladen:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Für ASP.NET MVC-Anwendungen mit Visual Web Developer müssen Sie Visual Web Developer Service Pack 1 installiert haben. Ohne Service Pack 1 können Sie keine Webanwendungsprojekte erstellen.

ASP.NET MVC-Framework. Sie können das ASP.NET MVC-Framework von der folgenden Adresse herunterladen:

[https://www.asp.net/mvc](../../../index.md)

In diesem Tutorial verwenden wir Microsoft Entity Framework, um auf eine Datenbank zuzugreifen. Das Entity Framework ist im .NET Framework 3.5 Service Pack 1 enthalten. Sie können dieses Service Pack von folgendem Speicherort herunterladen:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=de](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Als Alternative zu jedem dieser Downloads können Sie den Web Platform Installer (Web PI) nutzen. Sie können den Web-PI von der folgenden Adresse herunterladen:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC-Projekt

ASP.NET MVC Web Application Project. Starten Sie Visual Studio, und wählen Sie die Menüoption **Datei, Neues Projekt**aus. Das Dialogfeld **Neues Projekt** wird angezeigt (siehe Abbildung 1). Wählen Sie den **Webprojekttyp** und die **ASP.NET MVC-Webanwendungsvorlage** aus. Benennen Sie Den *neuen Projekt-Kontaktmanager,* und klicken Sie auf die Schaltfläche OK.

Stellen Sie sicher, dass .NET Framework 3.5 aus der Dropdownliste oben rechts im Dialogfeld **Neues Projekt** ausgewählt ist. Andernfalls wird die ASP.NET MVC-Webanwendungsvorlage nicht angezeigt.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**Abbildung 01**: Das Dialogfeld "Neues Projekt" ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image2.png))

ASP.NET MVC-Anwendung wird das Dialogfeld **Komponententestprojekt** erstellen angezeigt. Sie können dieses Dialogfeld verwenden, um anzugeben, dass Sie beim Erstellen der ASP.NET MVC-Anwendung ein Komponententestprojekt erstellen und der Projektmappe hinzufügen möchten. Obwohl wir in dieser Iteration keine Komponententests erstellen, sollten Sie die Option **Ja auswählen, ein Komponententestprojekt erstellen,** da wir planen, Komponententests in einer späteren Iteration hinzuzufügen. Das Hinzufügen eines Testprojekts beim ersten Erstellen eines neuen ASP.NET MVC-Projekts ist viel einfacher als das Hinzufügen eines Testprojekts, nachdem das ASP.NET MVC-Projekts erstellt wurde.

> [!NOTE] 
> 
> Da Visual Web Developer keine Testprojekte unterstützt, erhalten Sie das Dialogfeld Komponententestprojekt erstellen nicht, wenn Sie Visual Web Developer verwenden.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**Abbildung 02**: Das Dialogfeld Komponententestprojekt erstellen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image4.png))

ASP.NET MVC-Anwendung wird im Visual Studio-Projektmappen-Explorer-Fenster angezeigt (siehe Abbildung 3). Wenn das Projektmappen-Explorer-Fenster nicht angezeigt wird, können Sie dieses Fenster öffnen, indem Sie die Menüoption **Ansicht, Projektmappen-Explorer auswählen.** Beachten Sie, dass die Projektmappe zwei Projekte enthält: das ASP.NET MVC-Projekt und das Testprojekt. Das ASP.NET MVC-Projekt heißt ContactManager und das Testprojekt den Namen ContactManager.Tests.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**Abbildung 03**: Das Projektmappen-Explorer-Fenster ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>Löschen der Projektbeispieldateien

Die ASP.NET MVC-Projektvorlage enthält Beispieldateien für Controller und Ansichten. Bevor Sie eine neue ASP.NET MVC-Anwendung erstellen, sollten Sie diese Dateien löschen. Sie können Dateien und Ordner im Projektmappen-Explorer-Fenster löschen, indem Sie mit der rechten Maustaste auf eine Datei oder einen Ordner klicken und die Menüoption **Löschen**auswählen.

Sie müssen die folgenden Dateien aus dem ASP.NET MVC-Projekt löschen:

- Controller,HomeController.vb

- "Ansichten" ,,Home" und "About.aspx"

- Ansichten, Home, Index.aspx

Außerdem müssen Sie die folgende Datei aus dem Testprojekt löschen:

Controller-HomeControllerTest.vb

## <a name="creating-the-database"></a>Erstellen der Datenbank

Die Contact Manager-Anwendung ist eine datenbankgesteuerte Webanwendung. Wir verwenden eine Datenbank, um die Kontaktinformationen zu speichern.

Das ASP.NET MVC-Framework mit allen modernen Datenbanken, einschließlich Microsoft SQL Server-, Oracle-, MySQL- und IBM DB2-Datenbanken. In diesem Tutorial verwenden wir eine Microsoft SQL Server-Datenbank. Wenn Sie Visual Studio installieren, haben Sie die Möglichkeit, Microsoft SQL Server Express zu installieren, eine kostenlose Version der Microsoft SQL Server-Datenbank.

Erstellen Sie eine neue Datenbank,\_indem Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner "App-Daten" klicken und die Menüoption **Hinzufügen, Neues Element**auswählen. Wählen Sie im Dialogfeld **Neues Element hinzufügen** die **Datenkategorie** und die **SQL Server-Datenbankvorlage** aus (siehe Abbildung 4). Benennen Sie die neue Datenbank ContactManagerDB.mdf, und klicken Sie auf die Schaltfläche OK.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**Abbildung 04**: Erstellen einer neuen Microsoft SQL Server[Express-Datenbank ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image8.png))

Nachdem Sie die neue Datenbank erstellt haben, wird die Datenbank im Ordner App-Daten\_im Projektmappen-Explorer-Fenster angezeigt. Doppelklicken Sie auf die Datei ContactManager.mdf, um das Server Explorer-Fenster zu öffnen und eine Verbindung mit der Datenbank herzustellen.

> [!NOTE] 
> 
> Das Fenster Server-Explorer wird im Fall von Microsoft Visual Web Developer als Datenbank-Explorer-Fenster bezeichnet.

Sie können das Fenster Server-Explorer verwenden, um neue Datenbankobjekte wie Datenbanktabellen, Ansichten, Trigger und gespeicherte Prozeduren zu erstellen. Klicken Sie mit der rechten Maustaste auf den Ordner Tabellen, und wählen Sie die Menüoption **Neue Tabelle hinzufügen**aus. Der Datenbanktabellen-Designer wird angezeigt (siehe Abbildung 5).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**Abbildung 05**: Der Datenbanktabellen-Designer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image10.png))

Wir müssen eine Tabelle erstellen, die die folgenden Spalten enthält:

<a id="0.2_table01"></a>

| **Spaltenname** | **Datentyp** | **Nullen zulassen** |
| --- | --- | --- |
| Id | INT | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| Phone | nvarchar(50) | false |
| Email | nvarchar(255) | false |

Die erste Spalte, die Id-Spalte, ist speziell. Sie müssen die Id-Spalte als Identitätsspalte und Primärschlüsselspalte markieren. Sie geben an, dass eine Spalte eine Identitätsspalte ist, indem Sie die Spalteneigenschaften erweitern (siehe unten in Abbildung 6) und einen Bildlauf nach unten zur Identity Specification-Eigenschaft durchführen. Legen Sie die Eigenschaft **(Is Identity)** auf den Wert **Yes**fest.

Sie markieren eine Spalte als Primärschlüsselspalte, indem Sie die Spalte auswählen und auf die Schaltfläche mit dem Symbol eines Schlüssels klicken. Nachdem eine Spalte als Primärschlüsselspalte markiert wurde, wird neben der Spalte ein Symbol eines Schlüssels angezeigt (siehe Abbildung 6).

Nachdem Sie die Tabelle erstellt haben, klicken Sie auf die Schaltfläche Speichern (die Schaltfläche mit einem Symbol einer Diskette), um die neue Tabelle zu speichern. Geben Sie Ihrer neuen Tabelle den Namen *Kontakte*.

Nachdem Sie die Datenbanktabelle Kontakte erstellt haben, sollten Sie der Tabelle einige Datensätze hinzufügen. Klicken Sie im Fenster Server-Explorer mit der rechten Maustaste auf die Tabelle Kontakte, und wählen Sie die Menüoption **Tabellendaten anzeigen**aus. Geben Sie einen oder mehrere Kontakte in das angezeigte Raster ein.

## <a name="creating-the-data-model"></a>Erstellen des Datenmodells

Die ASP.NET MVC-Anwendung besteht aus Modellen, Ansichten und Controllern. Zunächst erstellen wir eine Modellklasse, die die Tabelle Kontakte darstellt, die wir im vorherigen Abschnitt erstellt haben.

In diesem Tutorial verwenden wir Microsoft Entity Framework, um automatisch eine Modellklasse aus der Datenbank zu generieren.

> [!NOTE] 
> 
> Das ASP.NET MVC-Framework ist in keiner Weise an das Microsoft Entity Framework gebunden. Sie können ASP.NET MVC mit alternativen Datenbankzugriffstechnologien wie NHibernate, LINQ to SQL oder ADO.NET verwenden.

Führen Sie die folgenden Schritte aus, um die Datenmodellklassen zu erstellen:

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner "Modelle" und wählen Sie **Hinzufügen, Neues Element**aus. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt (siehe Abbildung 6).
2. Wählen Sie die **Kategorie Daten** und die Vorlage **ADO.NET Entitätsdatenmodell** aus. Benennen Sie Ihr Datenmodell *ContactManagerModel.edmx,* und klicken Sie auf die Schaltfläche **Hinzufügen.** Der Assistent für das Entitätsdatenmodell wird angezeigt (siehe Abbildung 7).
3. Wählen Sie im Schritt **Modellinhalte auswählen** aus **Datenbank generieren** aus (siehe Abbildung 7).
4. Wählen Sie im Schritt **Datenverbindung auswählen** die Datenbank ContactManagerDB.mdf aus, und geben Sie den Namen *ContactManagerDBEntities* für die Entitätsverbindungseinstellungen ein (siehe Abbildung 8).
5. Aktivieren Sie im Schritt **Datenbankobjekte auswählen** das Kontrollkästchen Tabellen (siehe Abbildung 9). Das Datenmodell enthält alle Tabellen, die in der Datenbank enthalten sind (es gibt nur eine, die Tabelle Kontakte). Geben Sie den Namespace *Models*ein. Klicken Sie auf die Schaltfläche Fertig stellen, um den Assistenten abzuschließen.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**Abbildung 06**: Das Dialogfeld Neues Element hinzufügen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image12.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**Abbildung 07**: Wählen Sie Modellinhalt ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image14.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**Abbildung 08**: Wählen Sie Ihre Datenverbindung ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image16.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**Abbildung 09**: Wählen Sie Ihre Datenbankobjekte ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image18.png))

Nachdem Sie den Entitätsdatenmodell-Assistenten abgeschlossen haben, wird der Entity Data Model Designer angezeigt. Der Designer zeigt eine Klasse an, die jeder zu modellierenden Tabelle entspricht. Es sollte eine Klasse mit dem Namen Kontakte angezeigt werden.

Der Entitätsdatenmodell-Assistent generiert Klassennamen basierend auf Datenbanktabellennamen. Sie müssen fast immer den Namen der vom Assistenten generierten Klasse ändern. Klicken Sie im Designer mit der rechten Maustaste auf die Contacts-Klasse, und wählen Sie die Menüoption **Umbenennen**aus. Ändern Sie den Namen der Klasse von Kontakte (Plural) in Kontakt (Singular). Nachdem Sie den Klassennamen geändert haben, sollte die Klasse wie Abbildung 10 angezeigt werden.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**Abbildung 10**: Die[Contact-Klasse ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image20.png))

An dieser Stelle haben wir unser Datenbankmodell erstellt. Wir können die Contact-Klasse verwenden, um einen bestimmten Kontaktdatensatz in unserer Datenbank darzustellen.

## <a name="creating-the-home-controller"></a>Erstellen des Home-Controllers

Der nächste Schritt besteht darin, unseren Home-Controller zu erstellen. Der Home-Controller ist der Standardcontroller, der in einer ASP.NET MVC-Anwendung aufgerufen wird.

Erstellen Sie die Home-Controller-Klasse, indem Sie im Projektmappen-Explorer-Fenster mit der rechten Maustaste auf den Ordner Controller klicken und die Menüoption **"Controller hinzufügen"** auswählen (siehe Abbildung 11). Beachten Sie das Kontrollkästchen **Aktionsmethoden hinzufügen für Szenarien Erstellen, Aktualisieren und Details**. Stellen Sie sicher, dass dieses Kontrollkästchen aktiviert ist, bevor Sie auf die Schaltfläche **Hinzufügen** klicken.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**Abbildung 11**: Hinzufügen des[Home-Controllers ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image22.png))

Wenn Sie den Home-Controller erstellen, erhalten Sie die Klasse in Liste 1.

**Auflisten 1 - Controller-HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>Auflisten der Kontakte

Um die Datensätze in der Tabelle Kontakte-Datenbank anzuzeigen, müssen wir eine Index()-Aktion und eine Indexansicht erstellen.

Der Home-Controller enthält bereits eine Index()-Aktion. Wir müssen diese Methode so ändern, dass sie wie Listing 2 aussieht.

**Auflisten 2 - Controller-HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

Beachten Sie, dass die Home-Controller-Klasse \_in Listing 2 ein privates Feld mit dem Namen Entitäten enthält. Das \_Entitätsfeld stellt die Entitäten aus dem Datenmodell dar. Wir verwenden \_das Feld Entitäten, um mit der Datenbank zu kommunizieren.

Die Index()-Methode gibt eine Ansicht zurück, die alle Kontakte aus der Datenbanktabelle Kontakte darstellt. Die \_Ausdrucksentitäten. ContactSet.ToList() gibt die Liste der Kontakte als generische Liste zurück.

Nachdem wir nun den Indexcontroller erstellt haben, müssen wir als nächstes die Indexansicht erstellen. Kompilieren Sie ihre Anwendung vor dem Erstellen der Indexansicht, indem Sie die Menüoption **Build, Build Solution**auswählen. Sie sollten das Projekt immer kompilieren, bevor Sie eine Ansicht hinzufügen, damit die Liste der Modellklassen im Dialogfeld **Ansicht** hinzufügen angezeigt wird.

Sie erstellen die Indexansicht, indem Sie mit der rechten Maustaste auf die Index()-Methode klicken und die Menüoption **Ansicht hinzufügen** auswählen (siehe Abbildung 12). Wenn Sie diese Menüoption auswählen, wird das Dialogfeld **Ansicht hinzufügen** geöffnet (siehe Abbildung 13).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**Abbildung 12**: Hinzufügen der Indexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image24.png))

Aktivieren Sie im Dialogfeld **Ansicht hinzufügen** das Kontrollkästchen Erstellen einer **stark typisierten Ansicht**. Wählen Sie die Datenklasse ContactManager.Contact anzeigen und die Inhaltsliste anzeigen aus. Wenn Sie diese Optionen auswählen, wird eine Ansicht generiert, in der eine Liste der Kontaktdatensätze angezeigt wird.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**Abbildung 13**: Das Dialogfeld Ansicht hinzufügen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image26.png))

Wenn Sie auf die Schaltfläche **Hinzufügen** klicken, wird die Indexansicht in Liste 3 generiert. Beachten &lt;Sie die&gt; Direktive %- Page %, die oben in der Datei angezeigt wird. Die Indexansicht erbt von&lt;der ViewPage&lt;IEnumerable&gt; &gt; ContactManager.Models.Contact-Klasse. Mit anderen Worten, die Modellklasse in der Ansicht stellt eine Liste von Kontaktentitäten dar.

Der Text der Indexansicht enthält eine foreach-Schleife, die durch jeden der Kontakte iteriert, die durch die Modellklasse dargestellt werden. Der Wert jeder Eigenschaft der Contact-Klasse wird in einer HTML-Tabelle angezeigt.

**Auflisten 3 - Ansichten - Ansichten , Home, Index.aspx (unverändert)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

Wir müssen eine Änderung an der Indexansicht vornehmen. Da wir keine Detailansicht erstellen, können wir den Link Details entfernen. Suchen und Entfernen des folgenden Codes aus der Indexansicht:

.id = Element. ID)%&gt;

Nachdem Sie die Indexansicht geändert haben, können Sie die Kontakt-Manager-Anwendung ausführen. Wählen Sie die Menüoption Debuggen, Debuggen starten oder einfach F5 drücken. Wenn Sie die Anwendung zum ersten Mal ausführen, wird das Dialogfeld in Abbildung 14 angezeigt. Wählen Sie die Option **Web.config-Datei ändern, um das Debuggen zu aktivieren,** und klicken Sie auf die Schaltfläche OK.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**Abbildung 14**: Aktivieren des Debuggens ([Klicken Sie hier, um ein Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image28.png))

Die Indexansicht wird standardmäßig zurückgegeben. In dieser Ansicht werden alle Daten aus der Datenbanktabelle Kontakte aufgelistet (siehe Abbildung 15).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**Abbildung 15**: Die Indexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image30.png))

Beachten Sie, dass die Indexansicht unten in der Ansicht einen Link mit der Bezeichnung Neu erstellen enthält. Im nächsten Abschnitt erfahren Sie, wie Sie neue Kontakte erstellen.

## <a name="creating-new-contacts"></a>Erstellen neuer Kontakte

Damit Benutzer neue Kontakte erstellen können, müssen wir dem Home-Controller zwei Create()-Aktionen hinzufügen. Wir müssen eine Create()-Aktion erstellen, die ein HTML-Formular zum Erstellen eines neuen Kontakts zurückgibt. Wir müssen eine zweite Create()-Aktion erstellen, die die eigentliche Datenbankeinfügung des neuen Kontakts ausführt.

Die neuen Create()-Methoden, die wir dem Home-Controller hinzufügen müssen, sind in Liste 4 enthalten.

**Auflisten 4 - Controllers-HomeController.vb (mit Create-Methoden)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

Die erste Create()-Methode kann mit einem HTTP GET aufgerufen werden, während die zweite Create()-Methode nur von einem HTTP-POST aufgerufen werden kann. Mit anderen Worten, die zweite Create()-Methode kann nur aufgerufen werden, wenn ein HTML-Formular veröffentlicht wird. Die erste Create()-Methode gibt einfach eine Ansicht zurück, die das HTML-Formular zum Erstellen eines neuen Kontakts enthält. Die zweite Create()-Methode ist viel interessanter: Sie fügt den neuen Kontakt zur Datenbank hinzu.

Beachten Sie, dass die zweite Create()-Methode geändert wurde, um eine Instanz der Contact-Klasse zu akzeptieren. Die aus dem HTML-Formular veröffentlichten Formularwerte werden automatisch vom ASP.NET MVC-Framework an diese Contact-Klasse gebunden. Jedes Formularfeld aus dem HTML-Formular Erstellen wird einer Eigenschaft des Parameters Kontakt zugewiesen.

Beachten Sie, dass der Parameter Contact mit einem [Bind]-Attribut versehen ist. Das [Bind]-Attribut wird verwendet, um die Contact Id-Eigenschaft von der Bindung auszuschließen. Da die Id-Eigenschaft eine Identity-Eigenschaft darstellt, möchten wir die Id-Eigenschaft nicht festlegen.

Im Text der Create()-Methode wird das Entity Framework verwendet, um den neuen Kontakt in die Datenbank einzufügen. Der neue Kontakt wird dem vorhandenen Satz von Kontakten hinzugefügt, und die SaveChanges()-Methode wird aufgerufen, um diese Änderungen an die zugrunde liegende Datenbank zurückzuübertragen.

Sie können ein HTML-Formular zum Erstellen neuer Kontakte generieren, indem Sie mit der rechten Maustaste auf eine der beiden Create()-Methoden klicken und die Menüoption **Ansicht hinzufügen** auswählen (siehe Abbildung 16).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**Abbildung 16**: Hinzufügen der Ansicht Erstellen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image32.png))

Wählen Sie im Dialogfeld **Ansicht hinzufügen** die **ContactManager.Contact-Klasse** und die Option **Erstellen** für Den Ansichtsinhalt aus (siehe Abbildung 17). Wenn Sie auf die Schaltfläche **Hinzufügen** klicken, wird automatisch eine Ansicht erstellen generiert.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**Abbildung 17**: Eine Seitenexplosion anzeigen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image34.png))

Die Ansicht Erstellen enthält Formularfelder für jede der Eigenschaften der Contact-Klasse. Der Code für die Ansicht Erstellen ist in Liste 5 enthalten.

**Auflisten 5 - Ansichten - "Home" und "Create.aspx"**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

Nachdem Sie die Create()-Methoden geändert und die Ansicht Erstellen hinzugefügt haben, können Sie die Kontaktarbeitsanwendung ausführen und neue Kontakte erstellen. Klicken Sie auf den Link **Neu** erstellen, der in der Indexansicht angezeigt wird, um zur Ansicht Erstellen zu navigieren. Sie sollten die Ansicht in Abbildung 18 sehen.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**Abbildung 18**: Die Ansicht erstellen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image36.png))

## <a name="editing-contacts"></a>Bearbeiten von Kontakten

Das Hinzufügen der Funktionalität zum Bearbeiten eines Kontaktdatensatzes ähnelt dem Hinzufügen der Funktionalität zum Erstellen neuer Kontaktdatensätze. Zunächst müssen wir der Home-Controllerklasse zwei neue Edit-Methoden hinzufügen. Diese neuen Edit()-Methoden sind in Liste 6 enthalten.

**Auflisten 6 - Controllers-HomeController.vb (mit Edit-Methoden)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

Die erste Edit()-Methode wird von einem HTTP GET-Vorgang aufgerufen. Ein Id-Parameter wird an diese Methode übergeben, die die ID des bearbeiteten Kontaktdatensatzes darstellt. Das Entity Framework wird verwendet, um einen Kontakt abzurufen, der mit der ID übereinstimmt. Eine Ansicht, die ein HTML-Formular zum Bearbeiten eines Datensatzes enthält, wird zurückgegeben.

Die zweite Edit()-Methode führt die eigentliche Aktualisierung der Datenbank durch. Diese Methode akzeptiert eine Instanz der Contact-Klasse als Parameter. Das ASP.NET MVC-Framework bindet die Formularfelder aus dem Formular Bearbeiten automatisch an diese Klasse. Beachten Sie, dass Sie das Attribut [Bind] beim Bearbeiten eines Kontakts nicht einschließen (wir benötigen den Wert der Id-Eigenschaft).

Das Entity Framework wird verwendet, um den geänderten Kontakt in der Datenbank zu speichern. Der ursprüngliche Kontakt muss zuerst aus der Datenbank abgerufen werden. Als Nächstes wird die Entity Framework ApplyPropertyChanges()-Methode aufgerufen, um die Änderungen am Kontakt aufzuzeichnen. Schließlich wird die Entity Framework SaveChanges()-Methode aufgerufen, um die Änderungen an der zugrunde liegenden Datenbank beizubehalten.

Sie können die Ansicht generieren, die das Formular Bearbeiten enthält, indem Sie mit der rechten Maustaste auf die Edit()-Methode klicken und die Menüoption Ansicht hinzufügen auswählen. Wählen Sie im Dialogfeld Ansicht hinzufügen die **ContactManager.Models.Contact-Klasse** und den Inhalt der **Ansicht bearbeiten** aus (siehe Abbildung 19).

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**Abbildung 19**: Hinzufügen einer Bearbeitungsansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image38.png))

Wenn Sie auf die Schaltfläche Hinzufügen klicken, wird automatisch eine neue Bearbeitungsansicht generiert. Das generierte HTML-Formular enthält Felder, die den einzelnen Eigenschaften der Contact-Klasse entsprechen (siehe Liste 7).

**Auflisten 7 - Ansichten - "Home" und "Edit.aspx"**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Löschen von Kontakten

Wenn Sie Kontakte löschen möchten, müssen Sie der Home-Controller-Klasse zwei Delete()-Aktionen hinzufügen. Die erste Aktion Löschen() zeigt ein Bestätigungsformular zum Löschen an. Die zweite Delete()-Aktion führt den tatsächlichen Löschvorgang aus.

> [!NOTE] 
> 
> Später, in Iteration #7, ändern wir den Kontakt-Manager so, dass er einen einstufigen Ajax-Löschvorgang unterstützt.

Die beiden neuen Delete()-Methoden sind in Liste 8 enthalten.

**Auflisten 8 - Controllers-HomeController.vb (Methoden löschen)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

Die erste Delete()-Methode gibt ein Bestätigungsformular zum Löschen eines Kontaktdatensatzes aus der Datenbank zurück (siehe Abbildung20). Die zweite Delete()-Methode führt den tatsächlichen Löschvorgang für die Datenbank aus. Nachdem der ursprüngliche Kontakt aus der Datenbank abgerufen wurde, werden die Methoden Entity Framework DeleteObject() und SaveChanges() aufgerufen, um den Datenbanklöschvorgang auszuführen.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**Abbildung 20**: Die Löschbestätigungsansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image40.png))

Wir müssen die Indexansicht so ändern, dass sie einen Link zum Löschen von Kontaktdatensätzen enthält (siehe Abbildung 21). Sie müssen den folgenden Code derselben Tabellenzelle hinzufügen, die den Link Bearbeiten enthält:

.id = Element. ID)%&gt;

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**Abbildung 21**: Indexansicht mit Bearbeitungslink ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image42.png))

Als Nächstes müssen wir die Löschbestätigungsansicht erstellen. Klicken Sie mit der rechten Maustaste auf die Delete()-Methode in der Home-Controller-Klasse, und wählen Sie die Menüoption Ansicht hinzufügen aus. Das Dialogfeld Ansicht hinzufügen wird angezeigt (siehe Abbildung 22).

Anders als bei den Ansichten Liste, Erstellen und Bearbeiten enthält das Dialogfeld Ansicht hinzufügen keine Option zum Erstellen einer Löschansicht. Wählen Sie stattdessen die **Datenklasse ContactManager.Models.Contact** und den Inhalt der **leeren** Ansicht aus. Wenn Sie die Option Inhalt leeren auswählen, müssen wir die Ansicht selbst erstellen.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**Abbildung 22**: Hinzufügen der Löschbestätigungsansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image44.png))

Der Inhalt der Ansicht Löschen ist in Liste 9 enthalten. Diese Ansicht enthält ein Formular, das bestätigt, ob ein bestimmter Kontakt gelöscht werden soll (siehe Abbildung 21).

**Auflisten 9 - Ansichten - "Home" und "Delete.aspx"**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Ändern des Namens des Standardcontrollers

Es könnte Sie stören, dass der Name unserer Controllerklasse für die Arbeit mit Kontakten HomeController-Klasse heißt. Sollte der Controller nicht ContactController heißen?

Dieses Problem ist einfach genug, um zu beheben. Zunächst müssen wir den Namen des Home-Controllers umgestalten. Öffnen Sie die HomeController-Klasse im Visual Studio-Code-Editor, klicken Sie mit der rechten Maustaste auf den Namen der Klasse, und wählen Sie die Menüoption **Umbenennen**aus. Wenn Sie diese Menüoption auswählen, wird das Dialogfeld Umbenennen geöffnet.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**Abbildung 23**: Umgestaltung eines Controllernamens ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image46.png))

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**Abbildung 24**: Verwenden des Dialogfelds Umbenennen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image48.png))

Wenn Sie die Controllerklasse umbenennen, aktualisiert Visual Studio auch den Namen des Ordners im Ordner Ansichten. Visual Studio benennt den Ordner "Ansichten" in den Ordner "Ansichten" um.

Nachdem Sie diese Änderung vornehmen, verfügt Ihre Anwendung nicht mehr über einen Home-Controller. Wenn Sie Ihre Anwendung ausführen, wird die Fehlerseite in Abbildung 25 angezeigt.

[![Dialogfeld „New Project“ (Neues Projekt)](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**Abbildung 25**: Kein Standardcontroller ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](iteration-1-create-the-application-vb/_static/image50.png))

Wir müssen die Standardroute in der Datei Global.asax aktualisieren, um den Contact-Controller anstelle des Home-Controllers zu verwenden. Öffnen Sie die Datei Global.asax, und ändern Sie den Standardcontroller, der von der Standardroute verwendet wird (siehe Liste 10).

**Eintrag 10 - Global.asax.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

Nachdem Sie diese Änderungen vorgenommen haben, wird der Kontakt-Manager ordnungsgemäß ausgeführt. Jetzt wird die Contact-Controllerklasse als Standardcontroller verwendet.

## <a name="summary"></a>Zusammenfassung

In dieser ersten Iteration haben wir eine grundlegende Contact Manager-Anwendung auf die schnellste Art und Weise erstellt. Wir haben Visual Studio genutzt, um den anfangscode für unsere Controller und Ansichten automatisch zu generieren. Wir haben auch das Entity Framework genutzt, um unsere Datenbankmodellklassen automatisch zu generieren.

Derzeit können wir Kontaktdatensätze mit der Contact Manager-Anwendung auflisten, erstellen, bearbeiten und löschen. Mit anderen Worten, wir können alle grundlegenden Datenbankvorgänge ausführen, die für eine datenbankgesteuerte Webanwendung erforderlich sind.

Leider hat unsere Anwendung einige Probleme. Zuerst und ich zögere, dies zuzugeben, ist die Contact Manager-Anwendung nicht die attraktivste Anwendung. Es braucht einige Design-Arbeiten. In der nächsten Iteration wird erläutert, wie wir die Standardansichtmasterseite und das Cascading Stylesheet ändern können, um das Erscheinungsbild der Anwendung zu verbessern.

Zweitens haben wir keine Formularvalidierung implementiert. Beispielsweise steht Ihnen nichts entgegen, wenn Sie das Kontaktformular erstellen ohne Eingabe von Werten für eines der Formularfelder absenden können. Darüber hinaus können Sie ungültige Telefonnummern und E-Mail-Adressen eingeben. Wir beginnen, das Problem der Formularvalidierung in Iterations#3 anzugehen.

Schließlich und vor allem kann die aktuelle Iteration der Contact Manager-Anwendung nicht einfach geändert oder verwaltet werden. Beispielsweise wird die Datenbankzugriffslogik direkt in die Controlleraktionen integriert. Das bedeutet, dass wir unseren Datenzugriffscode nicht ändern können, ohne unsere Controller zu ändern. In späteren Iterationen untersuchen wir Softwareentwurfsmuster, die wir implementieren können, um den Contact Manager widerstandsfähiger gegenüber Änderungen zu machen.

> [!div class="step-by-step"]
> [Zurück](iteration-7-add-ajax-functionality-cs.md)
> [Weiter](iteration-2-make-the-application-look-nice-vb.md)
