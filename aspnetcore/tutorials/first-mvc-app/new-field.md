---
title: Hinzufügen eines neuen Felds zu einer ASP.NET Core MVC-App
author: rick-anderson
description: Erfahren Sie, wie Sie Entity Framework Code First-Migrationen verwenden, um ein neues Feld zu einem Modell hinzuzufügen und diese Änderung an eine Datenbank zu migrieren.
ms.author: riande
ms.custom: mvc
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/new-field
ms.openlocfilehash: 7993b36bf9115225e082d2929bb253aba5b18310
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039317"
---
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a>Hinzufügen eines neuen Felds zu einer ASP.NET Core MVC-App

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

In diesem Abschnitt werden [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First-Migrationen für folgende Zwecke verwendet:

* Dem Modell wird ein neues Feld hinzugefügt.
* Das neue Feld wird in die Datenbank migriert.

Wird EF Code First verwendet, um eine Datenbank automatisch zu erstellen, geht Code First wie folgt vor:

* Es fügt der Datenbank eine Tabelle hinzu, um das Schema der Datenbank nachzuverfolgen.
* Es überprüft, ob die Datenbank mit den Modellklassen synchron ist, aus denen sie generiert wurde. Wenn sie nicht synchron sind, löst EF eine Ausnahme aus. Dies erleichtert die Suche nach Problemen mit inkonsistenten Datenbanken bzw. inkonsistentem Code.

## <a name="add-a-rating-property-to-the-movie-model"></a>Hinzufügen einer Rating-Eigenschaft zum Movie-Modell

Fügen Sie eine `Rating`-Eigenschaft zu *Models/Movie.cs* hinzu:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

Erstellen Sie die App (STRG+UMSCHALT+B).

Da Sie der `Movie`-Klasse ein neues Feld hinzugefügt haben, müssen Sie die Positivliste für die Bindung aktualisieren, damit diese neue Eigenschaft eingeschlossen wird. Aktualisieren Sie in *MoviesController.cs* das `[Bind]`-Attribut für die Aktionsmethoden `Create` und `Edit` so, dass die `Rating`-Eigenschaft eingeschlossen wird:

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

Aktualisieren Sie die Ansichtsvorlagen, um die neue `Rating`-Eigenschaft in der Browseransicht anzuzeigen, zu erstellen und zu bearbeiten.

Bearbeiten Sie die Datei */Views/Movies/Index.cshtml*, und fügen Sie das Feld `Rating` hinzu:

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexGenreRating.cshtml?highlight=16,38&range=24-64)]

Aktualisieren Sie die Datei */Views/Movies/Create.cshtml* mit dem Feld `Rating`.

<!-- VS -------------------------->
# <a name="visual-studio--visual-studio-for-mactabvisual-studiovisual-studio-mac"></a>[Visual Studio / Visual Studio für Mac](#tab/visual-studio+visual-studio-mac)

Sie können die vorherige „Formulargruppe“ kopieren und einfügen und IntelliSense die Felder aktualisieren lassen. IntelliSense nutzt [Taghilfsprogramme](xref:mvc/views/tag-helpers/intro).

![Der Entwickler hat den Buchstaben R als Attributwert von „asp-for“ im zweiten „label“-Element der Ansicht eingegeben. Ein Intellisense-Kontextmenü mit den verfügbaren Feldern wird angezeigt, einschließlich „Rating“, das in der Liste automatisch hervorgehoben wird. Wenn der Entwickler auf das Feld klickt oder auf der Tastatur die EINGABETASTE drückt, wird der Wert auf „Rating“ festgelegt.](new-field/_static/cr.png)

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)
<!-- This tab intentionally left blank. -->
---  
<!-- End of VS tabs -->

Aktualisieren Sie die `SeedData`-Klasse so, dass sie einen Wert für die neue Spalte bereitstellt. Eine Beispieländerung wird nachstehend gezeigt, aber Sie sollten diese Änderung für jedes `new Movie`-Element vornehmen.

[!code-csharp[](start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

Die App funktioniert erst, nachdem die Datenbank mit dem neuen Feld aktualisiert wurde. Wird sie jetzt ausgeführt, wird die folgende `SqlException` ausgelöst:

`SqlException: Invalid column name 'Rating'.`

Dieser Fehler tritt auf, weil die aktualisierte Modellklasse „Movie“ sich vom Schema der Tabelle „Movie“ der vorhandenen Datenbank unterscheidet. (Die Datenbanktabelle enthält nicht die Spalte `Rating`.)

Es gibt mehrere Vorgehensweisen zum Beheben des Fehlers:

1. Lassen Sie die Datenbank von Entity Framework automatisch löschen und basierend auf dem neuen Modellklassenschema neu erstellen. Dieser Ansatz ist früh im Entwicklungszyklus sehr praktisch, wenn die aktive Entwicklung in einer Testdatenbank erfolgt. Er ermöglicht Ihnen, das Modell und das Datenbankschema schnell weiterzuentwickeln. Der Nachteil ist jedoch, dass in der Datenbank vorhandene Daten verloren gehen. Deshalb eignet sich dieser Ansatz nicht für eine Produktionsdatenbank! Das Verwenden eines Initialisierers zum automatischen Ausführen eines Seedings für eine Datenbank mit Testdaten ist häufig eine produktive Möglichkeit zum Entwickeln einer Anwendung. Dies ist ein guter Ansatz für die frühe Entwicklung und wenn SQLite verwendet wird.

2. Ändern Sie das Schema der vorhandenen Datenbank explizit so, dass es mit den Modellklassen übereinstimmt. Der Vorteil dieses Ansatzes ist, dass Sie Ihre Daten behalten. Sie können diese Änderung entweder manuell oder durch Erstellen eines Änderungsskripts für die Datenbank vornehmen.

3. Verwenden Sie Code First-Migrationen, um das Datenbankschema zu aktualisieren.

Für dieses Tutorial wird Code First-Migrationen verwendet.

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Öffnen Sie das Menü **Extras**. Wählen Sie dort **NuGet-Paket-Manager > Paket-Manager-Konsole** aus.

  ![PMC-Menü](adding-model/_static/pmc.png)

Geben Sie in der PMC die folgenden Befehle ein:

```powershell
Add-Migration Rating
Update-Database
```

Der Befehl `Add-Migration` weist das Migrationsframework an, das aktuelle `Movie`-Modell mit dem aktuellen `Movie`-Datenbankschema zu untersuchen und den notwendigen Code zu erstellen, um die Datenbank in das neue Modell zu migrieren.

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[Visual Studio Code / Visual Studio für Mac](#tab/visual-studio-code+visual-studio-mac)

[!INCLUDE[](~/includes/RP-mvc-shared/sqlite-warn.md)]

Führen Sie den folgenden Befehl aus:

```cli
dotnet ef migrations add Rating
dotnet ef database update
```

---  
<!-- End of VS tabs -->

Der Name „Rating“ ist beliebig und wird verwendet, um die Migrationsdatei zu benennen. Es ist hilfreich, einen aussagekräftigen Namen für die Migrationsdatei zu verwenden.

Werden alle Datensätze aus der Datenbank gelöscht, führt die initialize-Methode ein Seeding für die Datenbank aus und fügt das Feld `Rating` hinzu.

Führen Sie die App aus, und überprüfen Sie, ob Sie Filme mit dem Feld `Rating` erstellen/bearbeiten/anzeigen können. Sie müssen das Feld `Rating` den Ansichtsvorlagen `Edit`, `Details` und `Delete` hinzufügen.

> [!div class="step-by-step"]
> [Zurück](search.md)
> [Weiter](validation.md)  
