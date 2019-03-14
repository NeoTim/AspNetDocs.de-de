---
ms.openlocfilehash: 984edac5f093d59bd5e1d826df8f32fda89f9e46
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024577"
---
# <a name="work-with-sqlite-in-an-aspnet-core-mvc-app"></a>Arbeiten mit SQLite in einer ASP.NET Core MVC-App

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

Das `MvcMovieContext`-Objekt übernimmt die Aufgabe der Herstellung der Verbindung mit der Datenbank und Zuordnung von `Movie`-Objekten zu Datensätzen in der Datenbank. Der Datenbankkontext wird mit dem Container [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) in der Methode `ConfigureServices` in der Datei *Startup.cs* registriert:

[!code-csharp[](~/tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a>SQLite

Auf der [SQLite](https://www.sqlite.org/)-Website ist zu lesen:

> SQLite ist eine eigenständige, sehr zuverlässige, eingebettete, genehmigungsfreie SQL-Datenbank-Engine mit vollem Funktionsumfang. SQLite ist die weltweit am häufigsten verwendete Datenbank-Engine.

Es gibt viele Tools von Drittanbietern, die Sie herunterladen können, um eine SQLite-Datenbank zu verwalten und anzuzeigen. Die folgende Abbildung stammt aus [DB Browser for SQLite](http://sqlitebrowser.org/). Wenn Sie ein bestimmtes SQLite-Tool bevorzugen, geben Sie bitte in einem Kommentar dessen Vorteile an.

![DB Browser for SQLite mit der Filmdatenbank](~/tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a>Ausführen eines Seedings für die Datenbank

Erstellen Sie im Ordner *Models* die neue Klasse `SeedData`. Ersetzen Sie den generierten Code durch den folgenden:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

Wenn in der Datenbank Filme vorhanden sind, wird der Initialisierer des Seedings zurückgegeben.

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a>Hinzufügen des Initialisierers des Seedings

Fügen Sie den Initialisierer des Seedings in der Datei *Program.cs* zur `Main`-Methode hinzu:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]

::: moniker-end

### <a name="test-the-app"></a>Testen der App

Löschen Sie alle Datensätze in der Datenbank (damit die Seed-Methode ausgeführt wird). Beenden und starten Sie die App, um das Seeding der Datenbank auszuführen.
   
Die App zeigt die per Seeding hinzugefügten Daten.

![Im Browser geöffnete MVC Movie-Anwendung mit Filmdaten](~/tutorials/first-mvc-app/working-with-sql/_static/m55.png)
