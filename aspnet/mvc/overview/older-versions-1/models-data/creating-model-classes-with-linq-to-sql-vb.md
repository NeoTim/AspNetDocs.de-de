---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: Erstellen von Modellklassen mit LINQ to SQL (VB) | Microsoft Docs
author: rick-anderson
description: Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modell c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a6133227eedc8934af7bf872532ca667b97d0f8
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542702"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>Erstellen von Modellklassen mit LINQ to SQL (VB)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modellklassen erstellen und den Datenbankzugriff durchführen, indem Sie Microsoft LINQ to SQL nutzen.

Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modellklassen erstellen und den Datenbankzugriff durchführen, indem Sie Microsoft LINQ to SQL nutzen.

In diesem Tutorial erstellen wir eine grundlegende Movie-Datenbankanwendung. Wir beginnen damit, die Movie-Datenbank-Anwendung auf die schnellste und einfachste Weise zu erstellen. Wir führen alle unsere Datenzugriffe direkt über unsere Controller-Aktionen durch.

Als Nächstes erfahren Sie, wie Sie das Repository-Muster verwenden. Die Verwendung des Repository-Musters erfordert etwas mehr Arbeit. Der Vorteil dieses Musters besteht jedoch darin, dass Sie damit Anwendungen erstellen können, die an Änderungen angepasst werden können und leicht getestet werden können.

## <a name="what-is-a-model-class"></a>Was ist eine Modellklasse?

Ein MVC-Modell enthält die gesamte Anwendungslogik, die nicht in einer MVC-Ansicht oder einem MVC-Controller enthalten ist. Insbesondere enthält ein MVC-Modell ihre gesamte Anwendungsgeschäfts- und Datenzugriffslogik.

Sie können eine Vielzahl verschiedener Technologien verwenden, um Ihre Datenzugriffslogik zu implementieren. Sie können beispielsweise Ihre Datenzugriffsklassen mithilfe der Klassen Microsoft Entity Framework, NHibernate, Unterschall oder ADO.NET erstellen.

In diesem Tutorial verwende ich LINQ to SQL, um die Datenbank abzufragen und zu aktualisieren. LINQ to SQL bietet Ihnen eine sehr einfache Methode für die Interaktion mit einer Microsoft SQL Server-Datenbank. Es ist jedoch wichtig zu verstehen, dass das ASP.NET MVC-Framework in keiner Weise an LINQ to SQL gebunden ist. ASP.NET MVC ist mit jeder Datenzugriffstechnologie kompatibel.

## <a name="create-a-movie-database"></a>Erstellen einer Filmdatenbank

In diesem Tutorial -- um zu veranschaulichen, wie Sie Modellklassen erstellen können -- erstellen wir eine einfache Movie-Datenbankanwendung. Der erste Schritt besteht darin, eine neue Datenbank zu erstellen. Klicken Sie im\_Projektmappen-Explorer mit der rechten Maustaste auf den Ordner App-Daten, und wählen Sie die Menüoption **Hinzufügen, Neues Element**aus. Wählen Sie die SQL Server-Datenbankvorlage aus, geben Sie ihr den Namen MoviesDB.mdf, und klicken Sie auf die Schaltfläche **Hinzufügen** (siehe Abbildung 1).

[![Hinzufügen einer neuen SQL Server-Datenbank](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**Abbildung 01**: Hinzufügen einer neuen SQL[Server-Datenbank ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))

Nachdem Sie die neue Datenbank erstellt haben, können Sie die Datenbank öffnen, indem\_Sie im Ordner App-Daten auf die Datei MoviesDB.mdf doppelklicken. Durch Doppelklicken auf die Datei MoviesDB.mdf wird das Fenster Server-Explorer geöffnet (siehe Abbildung 2).

|   | Das Fenster Server-Explorer wird bei Verwendung von Visual Web Developer als Datenbank-Explorer-Fenster bezeichnet. |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![Verwenden des Server-Explorer-Fensters](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**Abbildung 02**: Verwenden des Server-Explorer-Fensters ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))

Wir müssen unserer Datenbank eine Tabelle hinzufügen, die unsere Filme darstellt. Klicken Sie mit der rechten Maustaste auf den Ordner Tabellen, und wählen Sie die Menüoption **Neue Tabelle hinzufügen**aus. Wenn Sie diese Menüoption auswählen, wird der Tabellen-Designer geöffnet (siehe Abbildung 3).

[![Verwenden des Server-Explorer-Fensters](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**Abbildung 03**: Der Tabellen-Designer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))

Wir müssen unserer Datenbanktabelle die folgenden Spalten hinzufügen:

| **Spaltenname** | **Datentyp** | **Nullen zulassen** |
| --- | --- | --- |
| Id | Int | False |
| Titel | Nvarchar(200) | False |
| Regisseur | Nvarchar(50) | False |

Sie müssen der Spalte Id zwei besondere Dinge antun. Zuerst müssen Sie die ID-Spalte als Primärschlüsselspalte markieren, indem Sie die Spalte im Tabellen-Designer auswählen und auf das Symbol eines Schlüssels klicken. LINQ to SQL erfordert, dass Sie Ihre Primärschlüsselspalten angeben, wenn Sie Einfügungen oder Aktualisierungen für die Datenbank durchführen.

Als Nächstes müssen Sie die Id-Spalte als Identitätsspalte markieren, indem Sie der **Is Identity-Eigenschaft** den Wert Ja zuweisen (siehe Abbildung 3). Eine Identitätsspalte ist eine Spalte, der automatisch eine neue Nummer zugewiesen wird, wenn Sie einer Tabelle eine neue Datenzeile hinzufügen.

Nachdem Sie diese Änderungen vorgenommen haben, speichern Sie die Tabelle mit dem Namen tblMovie. Sie können die Tabelle speichern, indem Sie auf die Schaltfläche Speichern klicken.

## <a name="create-linq-to-sql-classes"></a>Erstellen von LINQ zu SQL-Klassen

Unser MVC-Modell enthält LINQ-zu-SQL-Klassen, die die tblMovie-Datenbanktabelle darstellen. Die einfachste Möglichkeit, diese LINQ-zu-SQL-Klassen zu erstellen, besteht darin, mit der rechten Maustaste auf den Ordner "Modelle" zu klicken, **Hinzufügen, Neues Element**auszuwählen, die Vorlage LINQ zu SQL-Klassen auszuwählen, den Klassen den Namen Movie.dbml zu geben und auf die Schaltfläche **Hinzufügen** zu klicken (siehe Abbildung 4).

[![Erstellen von LINQ-zu-SQL-Klassen](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**Abbildung 04**: Erstellen von LINQ-zu-SQL-Klassen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))

Unmittelbar nach dem Erstellen des Movie LINQ to SQL Classes wird der Objektrelational-Designer angezeigt. Sie können Datenbanktabellen aus dem Server-Explorer-Fenster auf den Objektrelational-Designer ziehen, um LINQ-zu-SQL-Klassen zu erstellen, die bestimmte Datenbanktabellen darstellen. Wir müssen die tblMovie-Datenbanktabelle dem Object Relational Designer hinzufügen (siehe Abbildung 4).

[![Verwenden des Objektrelational-Designers](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**Abbildung 05**: Verwenden des Objektrelational-Designers ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))

Standardmäßig erstellt der Objektrelational-Designer eine Klasse mit demselben Namen wie die Datenbanktabelle, die Sie auf den Designer ziehen. Wir möchten unsere Klasse jedoch nicht tblMovie nennen. Klicken Sie daher im Designer auf den Namen der Klasse, und ändern Sie den Namen der Klasse in Film.

Denken Sie schließlich daran, auf die Schaltfläche **Speichern** (das Bild der Diskette) zu klicken, um die LINQ in SQL-Klassen zu speichern. Andernfalls wird die LINQ-zu-SQL-Klasse nicht vom Object Relational Designer generiert.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Verwenden von LINQ to SQL in einer Controlleraktion

Da wir nun unsere LINQ-zu-SQL-Klassen haben, können wir diese Klassen verwenden, um Daten aus der Datenbank abzurufen. In diesem Abschnitt erfahren Sie, wie Sie LINQ-zu-SQL-Klassen direkt innerhalb einer Controlleraktion verwenden. Wir zeigen die Liste der Filme aus der tblMovies-Datenbanktabelle in einer MVC-Ansicht an.

Zuerst müssen wir die HomeController-Klasse ändern. Diese Klasse befindet sich im Ordner Controller Ihrer Anwendung. Ändern Sie die Klasse so, dass sie wie die Klasse in Liste 1 aussieht.

**Auflistung 1 –`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

Die Index()-Aktion in Listing 1 verwendet eine LINQ to SQL DataContext-Klasse (movieDataContext), um die MoviesDB-Datenbank darzustellen. Die MoveDataContext-Klasse wurde vom Visual Studio Object Relational Designer generiert.

Eine LINQ-Abfrage wird für den DataContext ausgeführt, um alle Filme aus der tblMovies-Datenbanktabelle abzurufen. Die Liste der Filme wird einer lokalen Variable mit dem Namen "Filme" zugewiesen. Schließlich wird die Liste der Filme über Ansichtsdaten an die Ansicht übergeben.

Um die Filme anzuzeigen, müssen wir als nächstes die Indexansicht ändern. Sie finden die Indexansicht im Ordner Ansichten, Startseite. Aktualisieren Sie die Indexansicht so, dass sie wie die Ansicht in Liste 2 aussieht.

**Auflistung 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

Beachten Sie, dass die &lt;geänderte Indexansicht&gt; oben in der Ansicht eine Direktive "%" import namespace %" enthält. Diese Direktive importiert den MvcApplication1-Namespace. Wir brauchen diesen Namespace, um mit den Modellklassen – insbesondere der Movie-Klasse – in der Ansicht zu arbeiten.

Die Ansicht in Liste 2 enthält eine For Each-Schleife, die durch alle Elemente iteriert, die durch die ViewData.Model-Eigenschaft dargestellt werden. Der Wert der Title-Eigenschaft wird für jeden Film angezeigt.

Beachten Sie, dass der Wert der ViewData.Model-Eigenschaft in eine IEnumerable-Eigenschaft umgegartt ist. Dies ist notwendig, um den Inhalt von ViewData.Model zu durchlaufen. Eine weitere Möglichkeit besteht darin, eine stark typisierte Ansicht zu erstellen. Wenn Sie eine stark typisierte Ansicht erstellen, geben Sie die ViewData.Model-Eigenschaft in einen bestimmten Typ in der CodeBehind-Klasse einer Ansicht um.

Wenn Sie die Anwendung nach dem Ändern der HomeController-Klasse und der Indexansicht ausführen, erhalten Sie eine leere Seite. Sie erhalten eine leere Seite, da sich in der tblMovies-Datenbanktabelle keine Filmdatensätze befinden.

Um der tblMovies-Datenbanktabelle Datensätze hinzuzufügen, klicken Sie im Fenster Server Explorer (Fenster Datenbank-Explorer in Visual Web Developer) mit der rechten Maustaste auf die tblMovies-Datenbanktabelle (Datenbank-Explorer-Fenster in Visual Web Developer), und wählen Sie die Menüoption **Tabellendaten anzeigen**aus. Sie können Filmdatensätze mithilfe des angezeigten Rasters einfügen (siehe Abbildung 5).

[![Einfügen von Filmen](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**Abbildung 06**: Einfügen von Filmen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))

Nachdem Sie der Tabelle tblMovies einige Datenbankdatensätze hinzugefügt und die Anwendung ausgeführt haben, wird die Seite in Abbildung 7 angezeigt. Alle Filmdatenbankdatensätze werden in einer Aufzählung angezeigt.

[![Anzeigen von Filmen mit der Indexansicht](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**Abbildung 07**: Anzeigen von Filmen mit der Indexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Verwenden des Repository-Musters

Im vorherigen Abschnitt haben wir LINQ-zu-SQL-Klassen direkt innerhalb einer Controlleraktion verwendet. Wir haben die MovieDataContext-Klasse direkt aus der Index()-Controlleraktion verwendet. Bei einer einfachen Anwendung ist nichts dagegen einzuwenden. Die direkte Arbeit mit LINQ to SQL in einer Controllerklasse verursacht jedoch Probleme, wenn Sie eine komplexere Anwendung erstellen müssen.

Die Verwendung von LINQ to SQL innerhalb einer Controllerklasse erschwert das Umschalten von Datenzugriffstechnologien in Der Zukunft. Sie können z. B. von Microsoft LINQ zu SQL wechseln und Microsoft Entity Framework als Datenzugriffstechnologie verwenden. In diesem Fall müssen Sie jeden Controller, der auf die Datenbank in Ihrer Anwendung zugreift, neu schreiben.

Die Verwendung von LINQ to SQL innerhalb einer Controllerklasse erschwert auch das Erstellen von Komponententests für Ihre Anwendung. Normalerweise möchten Sie nicht mit einer Datenbank interagieren, wenn Sie Komponententests durchführen. Sie möchten die Komponententests verwenden, um die Anwendungslogik und nicht den Datenbankserver zu testen.

Um eine MVC-Anwendung zu erstellen, die an zukünftige Änderungen anpassungsfähiger ist und leichter getestet werden kann, sollten Sie das Repository-Muster verwenden. Wenn Sie das Repository-Muster verwenden, erstellen Sie eine separate Repository-Klasse, die die gesamte Datenbankzugriffslogik enthält.

Wenn Sie die Repository-Klasse erstellen, erstellen Sie eine Schnittstelle, die alle von der Repository-Klasse verwendeten Methoden darstellt. In Ihren Controllern schreiben Sie ihren Code für die Schnittstelle anstelle des Repositorys. Auf diese Weise können Sie das Repository in Zukunft mit verschiedenen Datenzugriffstechnologien implementieren.

Die Schnittstelle in Listing 3 heißt IMovieRepository und stellt eine einzelne Methode mit dem Namen ListAll() dar.

**Auflistung 3 –`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

Die Repository-Klasse in Listing 4 implementiert die IMovieRepository-Schnittstelle. Beachten Sie, dass sie eine Methode namens ListAll() enthält, die der Methode entspricht, die von der IMovieRepository-Schnittstelle benötigt wird.

**Auflistung 4 –`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

Schließlich verwendet die MoviesController-Klasse in Listing 5 das Repository-Muster. Es verwendet nicht mehr Direkt-LINQ-zu-SQL-Klassen.

**Auflistung 5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

Beachten Sie, dass die MoviesController-Klasse in Listing 5 über zwei Konstruktoren verfügt. Der erste Konstruktor, der parameterlose Konstruktor, wird aufgerufen, wenn die Anwendung ausgeführt wird. Dieser Konstruktor erstellt eine Instanz der MovieRepository-Klasse und übergibt sie an den zweiten Konstruktor.

Der zweite Konstruktor hat einen einzelnen Parameter: einen IMovieRepository-Parameter. Dieser Konstruktor weist den Wert des Parameters einfach einem \_Feld auf Klassenebene mit dem Namen Repository zu.

Die MoviesController-Klasse nutzt ein Softwareentwurfsmuster, das als Abhängigkeitsinjektionsmuster bezeichnet wird. Insbesondere verwendet es etwas, das Constructor Dependency Injection genannt wird. Sie können mehr über dieses Muster lesen, indem Sie den folgenden Artikel von Martin Fowler lesen:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Beachten Sie, dass der gesamte Code in der MoviesController-Klasse (mit Ausnahme des ersten Konstruktors) mit der IMovieRepository-Schnittstelle anstelle der eigentlichen MovieRepository-Klasse interagiert. Der Code interagiert mit einer abstrakten Schnittstelle anstelle einer konkreten Implementierung der Schnittstelle.

Wenn Sie die von der Anwendung verwendete Datenzugriffstechnologie ändern möchten, können Sie einfach die IMovieRepository-Schnittstelle mit einer Klasse implementieren, die die alternative Datenbankzugriffstechnologie verwendet. Sie können z. B. eine EntityFrameworkMovieRepository-Klasse oder eine SubSonicMovieRepository-Klasse erstellen. Da die Controllerklasse für die Schnittstelle programmiert ist, können Sie eine neue Implementierung von IMovieRepository an die Controllerklasse übergeben, und die Klasse würde weiterhin funktionieren.

Wenn Sie die MoviesController-Klasse testen möchten, können Sie außerdem eine Gefälschte Film-Repository-Klasse an den MoviesController übergeben. Sie können die IMovieRepository-Klasse mit einer Klasse implementieren, die eigentlich nicht auf die Datenbank zugreift, aber alle erforderlichen Methoden der IMovieRepository-Schnittstelle enthält. Auf diese Weise können Sie die MoviesController-Klasse testen, ohne tatsächlich auf eine echte Datenbank zuzugreifen.

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu veranschaulichen, wie Sie MVC-Modellklassen erstellen können, indem Sie Microsoft LINQ to SQL nutzen. Wir haben zwei Strategien zur Anzeige von Datenbankdaten in einer ASP.NET MVC-Anwendung untersucht. Zuerst haben wir LINQ-zu-SQL-Klassen erstellt und die Klassen direkt innerhalb einer Controlleraktion verwendet. Mit LINQ-zu-SQL-Klassen innerhalb eines Controllers können Sie Datenbankdaten schnell und einfach in einer MVC-Anwendung anzeigen.

Als nächstes untersuchten wir einen etwas schwierigeren, aber definitiv tugendhafteren Pfad zum Anzeigen von Datenbankdaten. Wir nutzten das Repository-Muster und platzierten unsere gesamte Datenbankzugriffslogik in einer separaten Repository-Klasse. In unserem Controller haben wir unseren gesamten Code gegen eine Schnittstelle anstelle einer betonierten Klasse geschrieben. Der Vorteil des Repository-Musters besteht darin, dass es uns ermöglicht, Datenbankzugriffstechnologien in Zukunft einfach zu ändern und unsere Controller-Klassen einfach zu testen.

> [!div class="step-by-step"]
> [Zurück](creating-model-classes-with-the-entity-framework-vb.md)
> [Weiter](displaying-a-table-of-database-data-vb.md)
