---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: Anzeigen einer Tabelle mit Datenbankdaten (VB) | Microsoft Docs
author: rick-anderson
description: In diesem Tutorial zeige ich zwei Methoden zum Anzeigen einer Gruppe von Datenbankdatensätzen. Ich zeige zwei Methoden zum Formatieren einer Gruppe von Datenbankdatensätzen in einem HTML-Ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541896"
---
# <a name="displaying-a-table-of-database-data-vb"></a>Anzeigen einer Tabelle von Datenbankdaten (VB)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> In diesem Tutorial zeige ich zwei Methoden zum Anzeigen einer Gruppe von Datenbankdatensätzen. Ich zeige zwei Methoden zum Formatieren eines Satzes von Datenbankdatensätzen in einer HTML-Tabelle. Zunächst zeige ich, wie Sie die Datenbankdatensätze direkt in einer Ansicht formatieren können. Als Nächstes zeige ich, wie Sie beim Formatieren von Datenbankdatensätzen Teile ausnutzen können.

Das Ziel dieses Tutorials besteht darin, zu erklären, wie Sie eine HTML-Tabelle mit Datenbankdaten in einer ASP.NET MVC-Anwendung anzeigen können. Zunächst erfahren Sie, wie Sie die in Visual Studio enthaltenen Gerüsttools verwenden, um eine Ansicht zu generieren, die eine Gruppe von Datensätzen automatisch anzeigt. Als Nächstes erfahren Sie, wie Sie beim Formatieren von Datenbankdatensätzen eine Teilvorlage als Vorlage verwenden.

## <a name="create-the-model-classes"></a>Erstellen der Modellklassen

Wir werden den Satz von Datensätzen aus der Tabelle Filme-Datenbank anzeigen. Die Tabelle "Filme"-Datenbank enthält die folgenden Spalten:

<a id="0.4_table01"></a>

| **Spaltenname** | **Datentyp** | **Nullen zulassen** |
| --- | --- | --- |
| Id | Int | False |
| Titel | Nvarchar(200) | False |
| Regisseur | NVarchar(50) | False |
| DateVeröffentlicht | Datetime | False |

Um die Tabelle Filme in unserer ASP.NET MVC-Anwendung darzustellen, müssen wir eine Modellklasse erstellen. In diesem Tutorial verwenden wir das Microsoft Entity Framework, um unsere Modellklassen zu erstellen.

> [!NOTE] 
> 
> In diesem Tutorial verwenden wir Microsoft Entity Framework. Es ist jedoch wichtig zu verstehen, dass Sie eine Vielzahl verschiedener Technologien verwenden können, um mit einer Datenbank aus einer ASP.NET MVC-Anwendung zu interagieren, einschließlich LINQ zu SQL, NHibernate oder ADO.NET.

Führen Sie die folgenden Schritte aus, um den Entitätsdatenmodell-Assistenten zu starten:

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner "Modelle" und wählen Sie die Menüoption **Hinzufügen, Neues Element**aus.
2. Wählen Sie die Kategorie **Daten** aus, und wählen Sie die Vorlage **ADO.NET Entitätsdatenmodell** aus.
3. Geben Sie Ihrem Datenmodell den Namen *MoviesDBModel.edmx* und klicken Sie auf die Schaltfläche **Hinzufügen.**

Nachdem Sie auf die Schaltfläche Hinzufügen geklickt haben, wird der Assistent für das Entitätsdatenmodell angezeigt (siehe Abbildung 1). Führen Sie die folgenden Schritte aus, um den Assistenten abzuschließen:

1. Wählen Sie im Schritt **Modellinhalte auswählen** die Option **Aus Datenbank generieren** aus.
2. Verwenden Sie im Schritt **Datenverbindung auswählen** die *Datenverbindung MoviesDB.mdf* und den Namen *MoviesDBEntities* für die Verbindungseinstellungen. Klicken Sie auf die Schaltfläche **Weiter**.
3. Erweitern Sie im Schritt **Datenbankobjekte auswählen** den Knoten Tabellen, und wählen Sie die Tabelle Filme aus. Geben Sie den Namespace *Models* ein, und klicken Sie auf die Schaltfläche **Fertig stellen.**

[![Erstellen von LINQ-zu-SQL-Klassen](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**Abbildung 01**: Erstellen von LINQ-zu-SQL-Klassen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](displaying-a-table-of-database-data-vb/_static/image2.png))

Nachdem Sie den Entitätsdatenmodell-Assistenten abgeschlossen haben, wird der Entity Data Model Designer geöffnet. Der Designer sollte die Movies-Entität anzeigen (siehe Abbildung 2).

[![Der Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**Abbildung 02**: Der Entity Data Model Designer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](displaying-a-table-of-database-data-vb/_static/image4.png))

Wir müssen eine Änderung vornehmen, bevor wir fortfahren. Der Entitätsdaten-Assistent generiert eine Modellklasse mit dem Namen *Filme,* die die Tabelle Movies-Datenbank darstellt. Da wir die Movies-Klasse verwenden, um einen bestimmten Film darzustellen, müssen wir den Namen der Klasse ändern, um *Film* statt *Filme* (Singular statt Plural) zu sein.

Doppelklicken Sie auf den Namen der Klasse auf der Designeroberfläche, und ändern Sie den Namen der Klasse von "Filme" in "Film". Nachdem Sie diese Änderung geändert haben, klicken Sie auf die Schaltfläche **Speichern** (das Symbol der Diskette), um die Movie-Klasse zu generieren.

## <a name="create-the-movies-controller"></a>Erstellen des Movies-Controllers

Nun, da wir eine Möglichkeit haben, unsere Datenbankdatensätze darzustellen, können wir einen Controller erstellen, der die Sammlung von Filmen zurückgibt. Klicken Sie im Fenster Visual Studio Solution Explorer mit der rechten Maustaste auf den Ordner Controller, und wählen Sie die Menüoption **"Controller hinzufügen"** (siehe Abbildung 3).

[![Das Menü Controller hinzufügen](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**Abbildung 03**: Das Menü Controller hinzufügen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](displaying-a-table-of-database-data-vb/_static/image6.png))

Wenn das Dialogfeld **Controller hinzufügen** angezeigt wird, geben Sie den Controllernamen MovieController ein (siehe Abbildung 4). Klicken Sie auf die Schaltfläche **Hinzufügen,** um den neuen Controller hinzuzufügen.

[![Das Dialogfeld Controller hinzufügen](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**Abbildung 04**: Das Dialogfeld Controller hinzufügen([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](displaying-a-table-of-database-data-vb/_static/image8.png)

Wir müssen die Index()-Aktion ändern, die vom Movie-Controller verfügbar gemacht wird, damit der Satz von Datenbankdatensätzen zurückgegeben wird. Ändern Sie den Controller so, dass er wie der Controller in Liste 1 aussieht.

**Auflisten 1 – Controller-MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

In Listing 1 wird die MoviesDBEntities-Klasse verwendet, um die MoviesDB-Datenbank darzustellen. Die *Ausdrucksentitäten. MovieSet.ToList()* gibt den Satz aller Filme aus der Tabelle Movies-Datenbank zurück.

## <a name="create-the-view"></a>Erstellen der Ansicht

Die einfachste Möglichkeit, einen Satz von Datenbankdatensätzen in einer HTML-Tabelle anzuzeigen, besteht darin, das von Visual Studio bereitgestellte Gerüst zu nutzen.

Erstellen Sie Ihre Anwendung, indem Sie die Menüoption **Build, Build Solution**auswählen. Sie müssen Ihre Anwendung erstellen, bevor Sie das Dialogfeld **Ansicht hinzufügen** öffnen, oder Ihre Datenklassen werden nicht im Dialogfeld angezeigt.

Klicken Sie mit der rechten Maustaste auf die Aktion Index() und wählen Sie die Menüoption **Ansicht hinzufügen** (siehe Abbildung 5).

[![Hinzufügen einer Ansicht](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**Abbildung 05**: Hinzufügen einer Ansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](displaying-a-table-of-database-data-vb/_static/image10.png))

Aktivieren Sie im Dialogfeld **Ansicht hinzufügen** das Kontrollkästchen Erstellen einer **stark typisierten Ansicht**. Wählen Sie die Movie-Klasse als **Ansichtsdatenklasse**aus. Wählen Sie *Liste* als **Ansichtsinhalt** aus (siehe Abbildung 6). Wenn Sie diese Optionen auswählen, wird eine stark typisierte Ansicht generiert, in der eine Liste von Filmen angezeigt wird.

[![Das Dialogfeld Ansicht hinzufügen](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**Abbildung 06**: Das Dialogfeld Ansicht hinzufügen([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](displaying-a-table-of-database-data-vb/_static/image12.png)

Nachdem Sie auf die Schaltfläche **Hinzufügen** geklickt haben, wird die Ansicht in Liste 2 automatisch generiert. Diese Ansicht enthält den Code, der zum Durchlaufen der Filmsammlung und zum Anzeigen der Eigenschaften eines Films erforderlich ist.

**Auflisten 2 – Ansichten, Movie, Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

Sie können die Anwendung ausführen, indem Sie die Menüoption **Debuggen, Debuggen starten** (oder die F5-Taste drücken). Durch Ausführen der Anwendung wird Internet Explorer gestartet. Wenn Sie zur /Movie-URL navigieren, wird die Seite in Abbildung 7 angezeigt.

[![Eine Tabelle mit Filmen](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**Abbildung 07**: Eine Tabelle mit Filmen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](displaying-a-table-of-database-data-vb/_static/image14.png))

Wenn Sie nichts über das Erscheinungsbild des Rasters von Datenbankdatensätzen in Abbildung 7 möchten, können Sie einfach die Indexansicht ändern. Sie können z. B. den *DateReleased-Header* in *Datum freigegeben* ändern, indem Sie die Indexansicht ändern.

## <a name="create-a-template-with-a-partial"></a>Erstellen einer Vorlage mit einem Teil

Wenn eine Ansicht zu kompliziert wird, ist es eine gute Idee, den Blick in Teile aufzuteilen. Die Verwendung von Teilteilen erleichtert das Verständnis und die Pflege Ihrer Ansichten. Wir erstellen einen Teil, den wir als Vorlage verwenden können, um jeden der Filmdatenbankdatensätze zu formatieren.

Führen Sie die folgenden Schritte aus, um den Teil zu erstellen:

1. Klicken Sie mit der rechten Maustaste auf den Ordner Ansichten/Film, und wählen Sie die Menüoption **Ansicht hinzufügen**aus.
2. Aktivieren Sie das Kontrollkästchen *Erstellen einer Teilansicht (.ascx)*.
3. Benennen Sie die partielle *MovieTemplate*.
4. Aktivieren Sie das Kontrollkästchen **Erstellen einer stark typisierten Ansicht**.
5. Wählen Sie Film als *Ansichtsdatenklasse*aus.
6. Wählen Sie Leer als *Ansichtsinhalt*aus.
7. Klicken Sie auf die Schaltfläche **Hinzufügen,** um den Teil zu Ihrem Projekt hinzuzufügen.

Nachdem Sie diese Schritte ausgeführt haben, ändern Sie den MovieTemplate-Teilteil so, dass es wie Eintrag 3 aussieht.

**Auflisten 3 – Ansichten- Und -Ansichten, MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

Der Teil in Liste 3 enthält eine Vorlage für eine einzelne Zeile von Datensätzen.

Die geänderte Indexansicht in Liste 4 verwendet den MovieTemplate-Teilteil.

**Auflisten 4 – Ansichten, Movie, Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

Die Ansicht in Liste 4 enthält eine For Each-Schleife, die durch alle Filme iteriert. Für jeden Film wird der MovieTemplate-Teil teilteil verwendet, um den Film zu formatieren. Die MovieTemplate wird gerendert, indem die RenderPartial()-Hilfsmethode aufgerufen wird.

Die geänderte Indexansicht rendert dieselbe HTML-Tabelle von Datenbankdatensätzen. Die Ansicht wurde jedoch erheblich vereinfacht.

Die RenderPartial()-Methode unterscheidet sich von den meisten anderen Hilfsmethoden, da keine Zeichenfolge zurückgegeben wird. Daher müssen Sie die &lt;RenderPartial()-Methode mit % Html.RenderPartial() %&gt; anstelle von&gt; &lt;%= Html.RenderPartial() % aufrufen.

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu erklären, wie Sie eine Reihe von Datenbankdatensätzen in einer HTML-Tabelle anzeigen können. Zuerst haben Sie gelernt, wie Sie eine Gruppe von Datenbankdatensätzen aus einer Controlleraktion zurückgeben, indem Sie das Microsoft Entity Framework nutzen. Als Nächstes haben Sie gelernt, wie Sie Visual Studio-Gerüste verwenden, um eine Ansicht zu generieren, die eine Sammlung von Elementen automatisch anzeigt. Schließlich haben Sie gelernt, wie Sie die Ansicht vereinfachen können, indem Sie einen Teilvorteil nutzen. Sie haben gelernt, wie Sie eine Teilvorlage als Vorlage verwenden, damit Sie jeden Datenbankdatensatz formatieren können.

> [!div class="step-by-step"]
> [Zurück](creating-model-classes-with-linq-to-sql-vb.md)
> [Weiter](performing-simple-validation-vb.md)
