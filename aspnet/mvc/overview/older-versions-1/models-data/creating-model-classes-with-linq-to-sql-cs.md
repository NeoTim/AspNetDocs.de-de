---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: Erstellen von Modellklassen mit LINQ zu SQL (C- | Microsoft Docs
author: rick-anderson
description: Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modell c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: eac6fec3a4cfd833b810378d946874a246d9a2c3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542728"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>Erstellen von Modellklassen mit LINQ to SQL (C#)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modellklassen erstellen und den Datenbankzugriff durchführen, indem Sie Microsoft LINQ to SQL nutzen.

Das Ziel dieses Tutorials besteht darin, eine Methode zum Erstellen von Modellklassen für eine ASP.NET MVC-Anwendung zu erklären. In diesem Tutorial erfahren Sie, wie Sie Modellklassen erstellen und den Datenbankzugriff durchführen, indem Sie Microsoft LINQ to SQL nutzen.

In diesem Tutorial erstellen wir eine grundlegende Movie-Datenbankanwendung. Wir beginnen damit, die Movie-Datenbank-Anwendung auf die schnellste und einfachste Weise zu erstellen. Wir führen alle unsere Datenzugriffe direkt über unsere Controller-Aktionen durch.

Als Nächstes erfahren Sie, wie Sie das Repository-Muster verwenden. Die Verwendung des Repository-Musters erfordert etwas mehr Arbeit. Der Vorteil dieses Musters besteht jedoch darin, dass Sie damit Anwendungen erstellen können, die an Änderungen angepasst werden können und leicht getestet werden können.

## <a name="what-is-a-model-class"></a>Was ist eine Modellklasse?

Ein MVC-Modell enthält die gesamte Anwendungslogik, die nicht in einer MVC-Ansicht oder einem MVC-Controller enthalten ist. Insbesondere enthält ein MVC-Modell ihre gesamte Anwendungsgeschäfts- und Datenzugriffslogik.

Sie können eine Vielzahl verschiedener Technologien verwenden, um Ihre Datenzugriffslogik zu implementieren. Sie können beispielsweise Ihre Datenzugriffsklassen mithilfe der Klassen Microsoft Entity Framework, NHibernate, Unterschall oder ADO.NET erstellen.

In diesem Tutorial verwende ich LINQ to SQL, um die Datenbank abzufragen und zu aktualisieren. LINQ to SQL bietet Ihnen eine sehr einfache Methode für die Interaktion mit einer Microsoft SQL Server-Datenbank. Es ist jedoch wichtig zu verstehen, dass das ASP.NET MVC-Framework in keiner Weise an LINQ to SQL gebunden ist. ASP.NET MVC ist mit jeder Datenzugriffstechnologie kompatibel.

## <a name="create-a-movie-database"></a>Erstellen einer Filmdatenbank

In diesem Tutorial -- um zu veranschaulichen, wie Sie Modellklassen erstellen können -- erstellen wir eine einfache Movie-Datenbankanwendung. Der erste Schritt besteht darin, eine neue Datenbank zu erstellen. Klicken Sie im\_Projektmappen-Explorer mit der rechten Maustaste auf den Ordner App-Daten, und wählen Sie die Menüoption **Hinzufügen, Neues Element**aus. Wählen Sie die **SQL Server-Datenbankvorlage** aus, geben Sie ihr den Namen MoviesDB.mdf, und klicken Sie auf die Schaltfläche **Hinzufügen** (siehe Abbildung 1).

[![Hinzufügen einer neuen SQL Server-Datenbank](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Abbildung 01**: Hinzufügen einer neuen SQL[Server-Datenbank ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))

Nachdem Sie die neue Datenbank erstellt haben, können Sie die Datenbank öffnen, indem\_Sie im Ordner App-Daten auf die Datei MoviesDB.mdf doppelklicken. Durch Doppelklicken auf die Datei MoviesDB.mdf wird das Fenster Server-Explorer geöffnet (siehe Abbildung 2).

Das Fenster Server-Explorer wird bei Verwendung von Visual Web Developer als Datenbank-Explorer-Fenster bezeichnet.

[![Verwenden des Server-Explorer-Fensters](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Abbildung 02**: Verwenden des Server-Explorer-Fensters ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))

Wir müssen unserer Datenbank eine Tabelle hinzufügen, die unsere Filme darstellt. Klicken Sie mit der rechten Maustaste auf den Ordner Tabellen, und wählen Sie die Menüoption **Neue Tabelle hinzufügen**aus. Wenn Sie diese Menüoption auswählen, wird der Tabellen-Designer geöffnet (siehe Abbildung 3).

[![Verwenden des Server-Explorer-Fensters](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Abbildung 03**: Der Tabellen-Designer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))

Wir müssen unserer Datenbanktabelle die folgenden Spalten hinzufügen:

| **Spaltenname** | **Datentyp** | **Nullen zulassen** |
| --- | --- | --- |
| Id | Int | False |
| Titel | Nvarchar(200) | False |
| Regisseur | Nvarchar(50) | False |

Sie müssen der Spalte Id zwei besondere Dinge antun. Zuerst müssen Sie die ID-Spalte als Primärschlüsselspalte markieren, indem Sie die Spalte im Tabellen-Designer auswählen und auf das Symbol eines Schlüssels klicken. LINQ to SQL erfordert, dass Sie Ihre Primärschlüsselspalten angeben, wenn Sie Einfügungen oder Aktualisierungen für die Datenbank durchführen.

Als Nächstes müssen Sie die Id-Spalte als Identitätsspalte markieren, indem Sie der **Is Identity-Eigenschaft** den Wert Ja zuweisen (siehe Abbildung 3). Eine Identitätsspalte ist eine Spalte, der automatisch eine neue Nummer zugewiesen wird, wenn Sie einer Tabelle eine neue Datenzeile hinzufügen.

## <a name="create-linq-to-sql-classes"></a>Erstellen von LINQ zu SQL-Klassen

Unser MVC-Modell enthält LINQ-zu-SQL-Klassen, die die tblMovie-Datenbanktabelle darstellen. Die einfachste Möglichkeit, diese LINQ-zu-SQL-Klassen zu erstellen, besteht darin, mit der rechten Maustaste auf den Ordner "Modelle" zu klicken, **Hinzufügen, Neues Element**auszuwählen, die Vorlage LINQ zu SQL-Klassen auszuwählen, den Klassen den Namen Movie.dbml zu geben und auf die Schaltfläche **Hinzufügen** zu klicken (siehe Abbildung 4).

[![Erstellen von LINQ-zu-SQL-Klassen](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Abbildung 04**: Erstellen von LINQ-zu-SQL-Klassen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))

Unmittelbar nach dem Erstellen des Movie LINQ to SQL Classes wird der Objektrelational-Designer angezeigt. Sie können Datenbanktabellen aus dem Server-Explorer-Fenster auf den Objektrelational-Designer ziehen, um LINQ-zu-SQL-Klassen zu erstellen, die bestimmte Datenbanktabellen darstellen. Wir müssen die tblMovie-Datenbanktabelle dem Object Relational Designer hinzufügen (siehe Abbildung 5).

[![Verwenden des Objektrelational-Designers](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Abbildung 05**: Verwenden des Objektrelational-Designers ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))

Standardmäßig erstellt der Objektrelational-Designer eine Klasse mit demselben Namen wie die Datenbanktabelle, die Sie auf den Designer ziehen. Wir wollen unsere Klasse `tblMovie`jedoch nicht nennen. Klicken Sie daher im Designer auf den Namen der Klasse, und ändern Sie den Namen der Klasse in Film.

Denken Sie schließlich daran, auf die Schaltfläche **Speichern** (das Bild der Diskette) zu klicken, um die LINQ in SQL-Klassen zu speichern. Andernfalls wird die LINQ-zu-SQL-Klasse nicht vom Object Relational Designer generiert.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Verwenden von LINQ to SQL in einer Controlleraktion

Da wir nun unsere LINQ-zu-SQL-Klassen haben, können wir diese Klassen verwenden, um Daten aus der Datenbank abzurufen. In diesem Abschnitt erfahren Sie, wie Sie LINQ-zu-SQL-Klassen direkt innerhalb einer Controlleraktion verwenden. Wir zeigen die Liste der Filme aus der tblMovies-Datenbanktabelle in einer MVC-Ansicht an.

Zuerst müssen wir die HomeController-Klasse ändern. Diese Klasse befindet sich im Ordner Controller Ihrer Anwendung. Ändern Sie die Klasse so, dass sie wie die Klasse in Liste 1 aussieht.

**Auflistung 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

Die `Index()` Aktion in Listing 1 verwendet eine LINQ `MovieDataContext`to SQL `MoviesDB` DataContext-Klasse (die ) zur Darstellung der Datenbank. Die `MoveDataContext` Klasse wurde vom Visual Studio Object Relational Designer generiert.

Eine LINQ-Abfrage wird für den DataContext ausgeführt, `tblMovies` um alle Filme aus der Datenbanktabelle abzurufen. Die Liste der Filme ist einer `movies`lokalen Variablen mit dem Namen zugewiesen. Schließlich wird die Liste der Filme über Ansichtsdaten an die Ansicht übergeben.

Um die Filme anzuzeigen, müssen wir als nächstes die Indexansicht ändern. Sie finden die Indexansicht `Views\Home\` im Ordner. Aktualisieren Sie die Indexansicht so, dass sie wie die Ansicht in Liste 2 aussieht.

**Auflistung 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Beachten Sie, dass die `<%@ import namespace %>` geänderte Indexansicht eine Direktive oben in der Ansicht enthält. Mit dieser `MvcApplication1.Models namespace`Richtlinie wird die importiert. Wir brauchen diesen Namespace, um `model` mit den Klassen `Movie` – insbesondere der Klasse – in der Ansicht zu arbeiten.

Die Ansicht in Liste `foreach` 2 enthält eine Schleife, die durch `ViewData.Model` alle von der Eigenschaft dargestellten Elemente iteriert. Der Wert `Title` der Eigenschaft wird `movie`für jede angezeigt.

Beachten Sie, dass `ViewData.Model` der Wert `IEnumerable`der Eigenschaft in eine umgecastet wird. Dies ist notwendig, um den `ViewData.Model`Inhalt von durchzuschleifen. Eine weitere Möglichkeit besteht darin, `view`eine stark typisierte zu erstellen. Wenn Sie eine stark `view`typisierte erstellen, werden sie die `ViewData.Model` Eigenschaft in einen bestimmten Typ in der CodeBehind-Klasse einer Ansicht umgeschichtet.

Wenn Sie die Anwendung nach `HomeController` dem Ändern der Klasse und der Indexansicht ausführen, erhalten Sie eine leere Seite. Sie erhalten eine leere Seite, da sich `tblMovies` keine Filmdatensätze in der Datenbanktabelle befinden.

Um der `tblMovies` Datenbanktabelle Datensätze hinzuzufügen, klicken `tblMovies` Sie im Fenster Server Explorer (Fenster Datenbank-Explorer in Visual Web Developer) mit der rechten Maustaste auf die Datenbanktabelle, und wählen Sie die Menüoption Tabellendaten anzeigen aus. Sie können `movie` Datensätze einfügen, indem Sie das angezeigte Raster verwenden (siehe Abbildung 6).

[![Einfügen von Filmen](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Abbildung 06**: Einfügen von Filmen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))

Nachdem Sie der `tblMovies` Tabelle einige Datenbankdatensätze hinzugefügt und die Anwendung ausgeführt haben, wird die Seite in Abbildung 7 angezeigt. Alle Filmdatenbankdatensätze werden in einer Aufzählung angezeigt.

[![Anzeigen von Filmen mit der Indexansicht](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Abbildung 07**: Anzeigen von Filmen mit der Indexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Verwenden des Repository-Musters

Im vorherigen Abschnitt haben wir LINQ-zu-SQL-Klassen direkt innerhalb einer Controlleraktion verwendet. Wir haben `MovieDataContext` die Klasse `Index()` direkt aus der Controller-Aktion verwendet. Bei einer einfachen Anwendung ist nichts dagegen einzuwenden. Die direkte Arbeit mit LINQ to SQL in einer Controllerklasse verursacht jedoch Probleme, wenn Sie eine komplexere Anwendung erstellen müssen.

Die Verwendung von LINQ to SQL innerhalb einer Controllerklasse erschwert das Umschalten von Datenzugriffstechnologien in Der Zukunft. Sie können z. B. von Microsoft LINQ zu SQL wechseln und Microsoft Entity Framework als Datenzugriffstechnologie verwenden. In diesem Fall müssen Sie jeden Controller, der auf die Datenbank in Ihrer Anwendung zugreift, neu schreiben.

Die Verwendung von LINQ to SQL innerhalb einer Controllerklasse erschwert auch das Erstellen von Komponententests für Ihre Anwendung. Normalerweise möchten Sie nicht mit einer Datenbank interagieren, wenn Sie Komponententests durchführen. Sie möchten die Komponententests verwenden, um die Anwendungslogik und nicht den Datenbankserver zu testen.

Um eine MVC-Anwendung zu erstellen, die an zukünftige Änderungen anpassungsfähiger ist und leichter getestet werden kann, sollten Sie das Repository-Muster verwenden. Wenn Sie das Repository-Muster verwenden, erstellen Sie eine separate Repository-Klasse, die die gesamte Datenbankzugriffslogik enthält.

Wenn Sie die Repository-Klasse erstellen, erstellen Sie eine Schnittstelle, die alle von der Repository-Klasse verwendeten Methoden darstellt. In Ihren Controllern schreiben Sie ihren Code für die Schnittstelle anstelle des Repositorys. Auf diese Weise können Sie das Repository in Zukunft mit verschiedenen Datenzugriffstechnologien implementieren.

Die Schnittstelle in Liste `IMovieRepository` 3 ist benannt `ListAll()`und stellt eine einzelne Methode mit dem Namen dar.

**Auflistung 3 –`Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

Die Repository-Klasse in Listing `IMovieRepository` 4 implementiert die Schnittstelle. Beachten Sie, dass `ListAll()` sie eine Mitdiesemliste `IMovieRepository` enthält, die der von der Schnittstelle erforderlichen Methode entspricht.

**Auflistung 4 –`Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Schließlich verwendet `MoviesController` die Klasse in Liste 5 das Repository-Muster. Es verwendet nicht mehr Direkt-LINQ-zu-SQL-Klassen.

**Auflistung 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Beachten Sie, dass die `MoviesController` Klasse in Listing 5 über zwei Konstruktoren verfügt. Der erste Konstruktor, der parameterlose Konstruktor, wird aufgerufen, wenn die Anwendung ausgeführt wird. Dieser Konstruktor erstellt eine `MovieRepository` Instanz der Klasse und übergibt sie an den zweiten Konstruktor.

Der zweite Konstruktor hat einen `IMovieRepository` einzelnen Parameter: einen Parameter. Dieser Konstruktor weist den Wert des Parameters einfach einem `_repository`Feld auf Klassenebene mit dem Namen zu.

Die `MoviesController` Klasse nutzt ein Softwareentwurfsmuster, das als Abhängigkeitsinjektionsmuster bezeichnet wird. Insbesondere verwendet es etwas, das Constructor Dependency Injection genannt wird. Sie können mehr über dieses Muster lesen, indem Sie den folgenden Artikel von Martin Fowler lesen:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Beachten Sie, dass der `MoviesController` gesamte Code in der Klasse (mit Ausnahme `IMovieRepository` des ersten `MovieRepository` Konstruktors) mit der Schnittstelle anstelle der tatsächlichen Klasse interagiert. Der Code interagiert mit einer abstrakten Schnittstelle anstelle einer konkreten Implementierung der Schnittstelle.

Wenn Sie die von der Anwendung verwendete Datenzugriffstechnologie ändern `IMovieRepository` möchten, können Sie einfach die Schnittstelle mit einer Klasse implementieren, die die alternative Datenbankzugriffstechnologie verwendet. Sie können z. `EntityFrameworkMovieRepository` B. `SubSonicMovieRepository` eine Klasse oder eine Klasse erstellen. Da die Controllerklasse für die Schnittstelle programmiert ist, `IMovieRepository` können Sie eine neue Implementierung von an die Controllerklasse übergeben, und die Klasse würde weiterhin funktionieren.

Wenn Sie die `MoviesController` Klasse testen möchten, können Sie außerdem eine `HomeController`gefälschte Film-Repository-Klasse an die übergeben. Sie können `IMovieRepository` die Klasse mit einer Klasse implementieren, die eigentlich nicht auf `IMovieRepository` die Datenbank zugreift, aber alle erforderlichen Methoden der Schnittstelle enthält. Auf diese Weise können `MoviesController` Sie die Klasse auf Einheit testen, ohne tatsächlich auf eine echte Datenbank zuzugreifen.

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu veranschaulichen, wie Sie MVC-Modellklassen erstellen können, indem Sie Microsoft LINQ to SQL nutzen. Wir haben zwei Strategien zur Anzeige von Datenbankdaten in einer ASP.NET MVC-Anwendung untersucht. Zuerst haben wir LINQ-zu-SQL-Klassen erstellt und die Klassen direkt innerhalb einer Controlleraktion verwendet. Mit LINQ-zu-SQL-Klassen innerhalb eines Controllers können Sie Datenbankdaten schnell und einfach in einer MVC-Anwendung anzeigen.

Als nächstes untersuchten wir einen etwas schwierigeren, aber definitiv tugendhafteren Pfad zum Anzeigen von Datenbankdaten. Wir nutzten das Repository-Muster und platzierten unsere gesamte Datenbankzugriffslogik in einer separaten Repository-Klasse. In unserem Controller haben wir unseren gesamten Code gegen eine Schnittstelle anstelle einer betonierten Klasse geschrieben. Der Vorteil des Repository-Musters besteht darin, dass es uns ermöglicht, Datenbankzugriffstechnologien in Zukunft einfach zu ändern und unsere Controller-Klassen einfach zu testen.

> [!div class="step-by-step"]
> [Zurück](creating-model-classes-with-the-entity-framework-cs.md)
> [Weiter](displaying-a-table-of-database-data-cs.md)
