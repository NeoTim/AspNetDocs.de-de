---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Erstellen von Modellklassen mit dem Entity Framework (VB) | Microsoft Docs
author: rick-anderson
description: In diesem Tutorial erfahren Sie, wie Sie ASP.NET MVC mit Microsoft Entity Framework verwenden. Sie erfahren, wie Sie den Entitäts-Assistenten verwenden, um eine ADO.NET Entität Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: cdba91969a6ed9c02965999bbc48d5c5cdea140d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542650"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a>Erstellen von Modellklassen mit dem Entity Framework (VB)

von [Microsoft](https://github.com/microsoft)

> In diesem Tutorial erfahren Sie, wie Sie ASP.NET MVC mit Microsoft Entity Framework verwenden. Sie erfahren, wie Sie mit dem Entitäts-Assistenten ein ADO.NET Entitätsdatenmodell erstellen. Im Verlauf dieses Tutorials erstellen wir eine Webanwendung, die veranschaulicht, wie Datenbankdaten mithilfe des Entity Framework ausgewählt, eingefügt, aktualisiert und gelöscht werden.

In diesem Tutorial wird erläutert, wie Sie Datenzugriffsklassen mithilfe von Microsoft Entity Framework erstellen können, wenn Sie eine ASP.NET MVC-Anwendung erstellen. In diesem Tutorial wird davon ausgegangen, dass das Microsoft Entity Framework nicht bereits bekannt ist. Am Ende dieses Tutorials erfahren Sie, wie Sie das Entity Framework zum Auswählen, Einfügen, Aktualisieren und Löschen von Datenbankdatensätzen verwenden.

Das Microsoft Entity Framework ist ein Object Relational Mapping (O/RM)-Tool, mit dem Sie automatisch eine Datenzugriffsebene aus einer Datenbank generieren können. Mit entity Framework können Sie die mühsame Arbeit beim Erstellen Ihrer Datenzugriffsklassen von Hand vermeiden.

> [!NOTE] 
> 
> Es besteht keine wesentliche Verbindung zwischen ASP.NET MVC und dem Microsoft Entity Framework. Es gibt mehrere Alternativen zum Entity Framework, die Sie mit ASP.NET MVC verwenden können. Sie können beispielsweise Ihre MVC-Modellklassen mit anderen O/RM-Tools wie Microsoft LINQ to SQL, NHibernate oder SubSonic erstellen.

Um zu veranschaulichen, wie Sie Microsoft Entity Framework mit ASP.NET MVC verwenden können, erstellen wir eine einfache Beispielanwendung. Wir erstellen eine Movie Database-Anwendung, mit der Sie Filmdatenbankdatensätze anzeigen und bearbeiten können.

In diesem Tutorial wird davon ausgegangen, dass Sie Über Visual Studio 2008 oder Visual Web Developer 2008 mit Service Pack 1 verfügen. Sie benötigen Service Pack 1, um das Entity Framework verwenden zu können. Sie können Visual Studio 2008 Service Pack 1 oder Visual Web Developer mit Service Pack 1 unter der folgenden Adresse herunterladen:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a>Erstellen der Filmbeispieldatenbank

Die Movie Database-Anwendung verwendet eine Datenbanktabelle mit dem Namen Filme, die die folgenden Spalten enthält:

| Spaltenname | Datentyp | Nullen zulassen? | Ist primärer Schlüssel? |
| --- | --- | --- | --- |
| Id | INT | False | True |
| Titel | nvarchar(100) | False | False |
| Regisseur | nvarchar(100) | False | False |

Sie können diese Tabelle einem ASP.NET MVC-Projekt hinzufügen, indem Sie die folgenden Schritte ausführen:

1. Klicken Sie im\_Projektmappen-Explorer mit der rechten Maustaste auf den Ordner App-Daten, und wählen Sie die Menüoption **Hinzufügen, Neues Element aus.**
2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option SQL **Server-Datenbank**aus , geben Sie der Datenbank den Namen MoviesDB.mdf, und klicken Sie auf die Schaltfläche **Hinzufügen.**
3. Doppelklicken Sie auf die Datei MoviesDB.mdf, um das Fenster Server Explorer/Database Explorer zu öffnen.
4. Erweitern Sie die Datenbankverbindung MoviesDB.mdf, klicken Sie mit der rechten Maustaste auf den Ordner Tabellen, und wählen Sie die Menüoption **Neue Tabelle hinzufügen**aus.
5. Fügen Sie im Tabellen-Designer die Spalten Id, Titel und Director hinzu.
6. Klicken Sie auf die Schaltfläche **Speichern** (es hat das Symbol der Diskette), um die neue Tabelle mit dem Namen Filme zu speichern.

Nachdem Sie die Tabelle Movies-Datenbank erstellt haben, sollten Sie der Tabelle einige Beispieldaten hinzufügen. Klicken Sie mit der rechten Maustaste auf die Tabelle Filme, und wählen Sie die Menüoption **Tabellendaten anzeigen**aus. Sie können gefälschte Filmdaten in das Raster eingeben, das angezeigt wird.

## <a name="creating-the-adonet-entity-data-model"></a>Erstellen des ADO.NET Entitätsdatenmodells

Um das Entity Framework verwenden zu können, müssen Sie ein Entitätsdatenmodell erstellen. Sie können den Visual *Studio-Entitätsdatenmodell-Assistenten* nutzen, um automatisch ein Entitätsdatenmodell aus einer Datenbank zu generieren.

Folgen Sie diesen Schritten:

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner "Modelle" und wählen Sie die Menüoption **Hinzufügen, Neues Element**aus.
2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Datenkategorie aus (siehe Abbildung 1).
3. Wählen Sie die Vorlage **ADO.NET Entitätsdatenmodell** aus, geben Sie dem Entitätsdatenmodell den Namen MoviesDBModel.edmx, und klicken Sie auf die Schaltfläche **Hinzufügen.** Wenn Sie auf die Schaltfläche **Hinzufügen** klicken, wird der Datenmodell-Assistent gestartet.
4. Wählen Sie im Schritt **Modellinhalte auswählen** die Option **Aus einer Datenbank generieren** aus, und klicken Sie auf die Schaltfläche **Weiter** (siehe Abbildung 2).
5. Wählen Sie im Schritt **Datenverbindung auswählen** die Datenbankverbindung MoviesDB.mdf aus, geben Sie die Entitäten-Verbindungseinstellungen mit dem Namen MoviesDBEntities ein, und klicken Sie auf die Schaltfläche **Weiter** (siehe Abbildung 3).
6. Wählen Sie im Schritt **Datenbankobjekte auswählen** die Tabelle Filmdatenbank aus, und klicken Sie auf die Schaltfläche **Fertig stellen** (siehe Abbildung 4).

Nachdem Sie diese Schritte ausgeführt haben, wird der ADO.NET Entity Data Model Designer (Entity Designer) geöffnet.

**Abbildung 1: Erstellen eines neuen Entitätsdatenmodells**

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

**Abbildung 2 – Wählen Sie den Schritt "Modellinhalt"**

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

**Abbildung 3 – Wählen Sie Ihre Datenverbindung**

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

**Abbildung 4 – Wählen Sie Ihre Datenbankobjekte**

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a>Ändern des ADO.NET Entitätsdatenmodells

Nachdem Sie ein Entitätsdatenmodell erstellt haben, können Sie das Modell ändern, indem Sie den Entitäts-Designer nutzen (siehe Abbildung 5). Sie können den Entitäts-Designer jederzeit öffnen, indem Sie auf die Datei MoviesDBModel.edmx doppelklicken, die im Ordner "Modelle" im Projektmappen-Explorer-Fenster enthalten ist.

**Abbildung 5: Der ADO.NET Entitätsdatenmodell-Designer**

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

Sie können z. B. den Entitäts-Designer verwenden, um die Namen der Klassen zu ändern, die vom Entitätsmodelldaten-Assistenten generiert werden. Der Assistent hat eine neue Datenzugriffsklasse mit dem Namen Filme erstellt. Mit anderen Worten, der Assistent gab der Klasse denselben Namen wie die Datenbanktabelle. Da wir diese Klasse verwenden, um eine bestimmte Movie-Instanz darzustellen, sollten wir die Klasse von Movies in Movie umbenennen.

Wenn Sie eine Entitätsklasse umbenennen möchten, können Sie im Entitäts-Designer auf den Klassennamen doppelklicken und einen neuen Namen eingeben (siehe Abbildung 6). Alternativ können Sie den Namen einer Entität im Eigenschaftenfenster ändern, nachdem Sie eine Entität im Entitäts-Designer ausgewählt haben.

**Abbildung 6 : Ändern eines Entitätsnamens**

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

Denken Sie daran, Ihr Entitätsdatenmodell zu speichern, nachdem Sie eine Änderung vorgenommen haben, indem Sie auf die Schaltfläche Speichern (das Symbol der Diskette) klicken. Im Lichte der Kulissen generiert der Entity Designer eine Reihe von Visual Basic .NET-Klassen. Sie können diese Klassen anzeigen, indem Sie die Datei MoviesDBModel.Designer.vb im Projektmappen-Explorer öffnen.

Ändern Sie den Code in der Designer.vb-Datei nicht, da Ihre Änderungen bei der nächsten Verwendung des Entitäts-Designers überschrieben werden. Wenn Sie die Funktionalität der entitätsklassen erweitern möchten, die in der Datei Designer.vb definiert sind, können Sie *Teilklassen* in separaten Dateien erstellen.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Auswählen von Datenbankdatensätzen mit dem Entity Framework

Beginnen wir mit dem Erstellen unserer Movie Database-Anwendung, indem wir eine Seite erstellen, auf der eine Liste von Filmdatensätzen angezeigt wird. Der Home-Controller in Listing 1 macht eine Aktion namens Index() verfügbar. Die Index()-Aktion gibt alle Filmdatensätze aus der Tabelle Filmdatenbank zurück, indem sie das Entity Framework nutzt.

**Auflisten 1 – Controller-HomeController.vb**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

Beachten Sie, dass der Controller in Liste 1 einen Konstruktor enthält. Der Konstruktor initialisiert ein Feld \_auf Klassenebene mit dem Namen db. Das \_db-Feld stellt die von Microsoft Entity Framework generierten Datenbankentitäten dar. Das \_db-Feld ist eine Instanz der MoviesDBEntities-Klasse, die vom Entitäts-Designer generiert wurde.

Das \_db-Feld wird innerhalb der Aktion Index() verwendet, um die Datensätze aus der Tabelle Movies-Datenbank abzurufen. Der \_Ausdruck db. MovieSet stellt alle Datensätze aus der Tabelle Movies-Datenbank dar. Die ToList()-Methode wird verwendet, um den Satz von Filmen in eine generische Sammlung von Movie-Objekten zu konvertieren: List( Of Movie).

Die Filmdatensätze werden mit Hilfe von LINQ to Entities abgerufen. Die Index()-Aktion in Listing 1 verwendet die *LINQ-Methodensyntax,* um den Satz von Datenbankdatensätzen abzurufen. Wenn Sie möchten, können Sie *query syntax* stattdessen die LINQ-Abfragesyntax verwenden. Die folgenden beiden Aussagen tun dasselbe:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

Verwenden Sie die LINQ-Syntax – Methodensyntax oder Abfragesyntax –, die Sie am intuitivsten finden. Es gibt keinen Leistungsunterschied zwischen den beiden Ansätzen – der einzige Unterschied ist Stil.

Die Ansicht in Liste 2 wird verwendet, um die Filmaufzeichnungen anzuzeigen.

**Auflisten 2 – Ansichten, Home, Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

Die Ansicht in Liste 2 enthält eine **For Each-Schleife,** die durch jeden Filmdatensatz iteriert und die Werte der Titel- und Regieeigenschaften des Filmdatensatzes anzeigt. Beachten Sie, dass neben jedem Datensatz ein Link zum Bearbeiten und Löschen angezeigt wird. Darüber hinaus wird am unteren Rand der Ansicht ein Link "Film hinzufügen" angezeigt (siehe Abbildung 7).

**Abbildung 7 – Die Indexansicht**

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

Die Indexansicht ist eine *typisierte Ansicht*. Die Indexansicht &lt;verfügt über&gt; eine %-Page-%-Direktive, die ein Inherits-Attribut enthält. Das Inherits-Attribut gibt die ViewData.Model-Eigenschaft in eine stark typisierte generische List-Auflistung von Movie-Objekten – eine List(Of Movie) um.

## <a name="inserting-database-records-with-the-entity-framework"></a>Einfügen von Datenbankdatensätzen mit dem Entity Framework

Sie können das Entity Framework verwenden, um das Einfügen neuer Datensätze in eine Datenbanktabelle zu vereinfachen. Liste 3 enthält zwei neue Aktionen, die der Home-Controllerklasse hinzugefügt wurden und die Sie zum Einfügen neuer Datensätze in die Tabelle Filmdatenbank verwenden können.

**Auflisten 3 – Controllers-HomeController.vb (Methoden hinzufügen)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

Die erste Add()-Aktion gibt einfach eine Ansicht zurück. Die Ansicht enthält ein Formular zum Hinzufügen eines neuen Filmdatenbankdatensatzes (siehe Abbildung 8). Wenn Sie das Formular absenden, wird die zweite Add()-Aktion aufgerufen.

Beachten Sie, dass die zweite Add()-Aktion mit dem AcceptVerbs-Attribut versehen ist. Diese Aktion kann nur aufgerufen werden, wenn ein HTTP-POST-Vorgang ausgeführt wird. Mit anderen Worten, diese Aktion kann nur aufgerufen werden, wenn ein HTML-Formular veröffentlicht wird.

Die zweite Add()-Aktion erstellt mit Hilfe der ASP.NET MVC TryUpdateModel()-Methode eine neue Instanz der Entity Framework Movie-Klasse. Die TryUpdateModel()-Methode nimmt die Felder in der FormCollection, die an die Add()-Methode übergeben wird, und weist die Werte dieser HTML-Formularfelder der Movie-Klasse zu.

Wenn Sie entity Framework verwenden, müssen Sie eine "weiße Liste" von Eigenschaften angeben, wenn Sie die TryUpdateModel- oder UpdateModel-Methoden verwenden, um die Eigenschaften einer Entitätsklasse zu aktualisieren.

Als Nächstes führt die Aktion Hinzufügen() eine einfache Formularüberprüfung durch. Die Aktion überprüft, ob sowohl die Title- als auch die Director-Eigenschaften Werte haben. Wenn ein Validierungsfehler auftritt, wird ModelState eine Validierungsfehlermeldung hinzugefügt.

Wenn keine Validierungsfehler vorliegen, wird der Tabelle Movies-Datenbank mit Hilfe des Entity Framework ein neuer Filmdatensatz hinzugefügt. Der neue Datensatz wird der Datenbank mit den folgenden zwei Codezeilen hinzugefügt:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

Die erste Codezeile fügt die neue Movie-Entität zu dem Satz von Filmen hinzu, die vom Entity Framework verfolgt werden. Die zweite Codezeile speichert alle Änderungen, die an den Filmen vorgenommen wurden, die in der zugrunde liegenden Datenbank nachverfolgt werden.

**Abbildung 8 – Die Ansicht Hinzufügen**

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a>Aktualisieren von Datenbankdatensätzen mit dem Entity Framework

Sie können fast den gleichen Ansatz verfolgen, um einen Datenbankdatensatz mit dem Entity Framework zu bearbeiten, wie der Ansatz, den wir gerade verfolgt haben, um einen neuen Datenbankdatensatz einzufügen. Liste 4 enthält zwei neue Controller-Aktionen mit dem Namen Edit(). Die erste Edit()-Aktion gibt ein HTML-Formular zum Bearbeiten eines Filmdatensatzes zurück. Die zweite Edit()-Aktion versucht, die Datenbank zu aktualisieren.

**Auflisten 4 – Controllers-HomeController.vb (Bearbeiten von Methoden)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

Die zweite Edit()-Aktion beginnt mit dem Abrufen des Movie-Datensatzes aus der Datenbank, die mit der ID des bearbeiteten Films übereinstimmt. Die folgende LINQ to Entities-Anweisung greift den ersten Datenbankdatensatz ab, der mit einer bestimmten ID übereinstimmt:

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

Als Nächstes wird die TryUpdateModel()-Methode verwendet, um die Werte der HTML-Formularfelder den Eigenschaften der Filmentität zuzuweisen. Beachten Sie, dass eine weiße Liste bereitgestellt wird, um die genauen Eigenschaften anzugeben, die aktualisiert werden sollen.

Als Nächstes wird eine einfache Überprüfung durchgeführt, um sicherzustellen, dass sowohl die Movie Title- als auch die Director-Eigenschaften Werte aufweisen. Wenn eine der beiden Eigenschaften einen Wert vermisst, wird ModelState eine Validierungsfehlermeldung hinzugefügt, und ModelState.IsValid gibt den Wert false zurück.

Wenn keine Validierungsfehler vorliegen, wird die zugrunde liegende Films-Datenbanktabelle mit allen Änderungen aktualisiert, indem die SaveChanges()-Methode aufgerufen wird.

Beim Bearbeiten von Datenbankdatensätzen müssen Sie die ID des bearbeiteten Datensatzes an die Controlleraktion übergeben, die die Datenbankaktualisierung durchführt. Andernfalls weiß die Controlleraktion nicht, welcher Datensatz in der zugrunde liegenden Datenbank aktualisiert werden soll. Die In-Liste 5 enthaltene Bearbeitungsansicht enthält ein ausgeblendetes Formularfeld, das die ID des bearbeiteten Datenbankdatensatzes darstellt.

**Auflisten 5 – Ansichten, Home, Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Löschen von Datenbankdatensätzen mit dem Entity Framework

Der letzte Datenbankvorgang, den wir in diesem Tutorial angehen müssen, ist das Löschen von Datenbankdatensätzen. Sie können die Controlleraktion in Liste 6 verwenden, um einen bestimmten Datenbankdatensatz zu löschen.

**Auflisten 6 -- ,,Controllers" (Aktion löschen)**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

Die Delete()-Aktion ruft zuerst die Movie-Entität ab, die mit der an die Aktion übergebenen ID übereinstimmt. Als Nächstes wird der Film aus der Datenbank gelöscht, indem die DeleteObject()-Methode gefolgt von der SaveChanges()-Methode aufgerufen wird. Schließlich wird der Benutzer zurück zur Indexansicht umgeleitet.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial sollte veranschaulicht werden, wie Sie datenbankgesteuerte Webanwendungen erstellen können, indem Sie ASP.NET MVC und Microsoft Entity Framework nutzen. Sie haben gelernt, wie Sie eine Anwendung erstellen, mit der Sie Datenbankdatensätze auswählen, einfügen, aktualisieren und löschen können.

Anschließend wurde erläutert, wie Sie den Entitätsdatenmodell-Assistenten verwenden können, um ein Entitätsdatenmodell aus Visual Studio zu generieren. Als Nächstes erfahren Sie, wie Sie LINQ to Entities verwenden, um eine Gruppe von Datenbankdatensätzen aus einer Datenbanktabelle abzurufen. Schließlich haben wir das Entity Framework zum Einfügen, Aktualisieren und Löschen von Datenbankdatensätzen verwendet.

> [!div class="step-by-step"]
> [Zurück](validation-with-the-data-annotation-validators-cs.md)
> [Weiter](creating-model-classes-with-linq-to-sql-vb.md)
