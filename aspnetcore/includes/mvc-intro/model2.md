---
ms.openlocfilehash: f2c9cad82eb25d350426465b3632862761740abe
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040497"
---
<a name="dc"></a>

Fügen Sie dem Ordner *Models* die folgende `MvcMovieContext`-Klasse hinzu:  

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Data/MvcMovieContext.cs)]


Der vorangehende Code erstellt eine `DbSet`-Eigenschaft für die Entitätenmenge. In der Terminologie von Entity Framework entspricht eine Entitätenmenge in der Regel einer Datenbanktabelle, und eine Entität entspricht einer Zeile in einer Tabelle.

<a name="cs"></a>

### <a name="add-a-database-connection-string"></a>Hinzufügen einer Datenbank-Verbindungszeichenfolge

Fügen Sie der Datei *appsettings.json* eine Verbindungszeichenfolge hinzu:

[!code-json[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings_SQLite.json?highlight=8-10)]

### <a name="add-required-nuget-packages"></a>Hinzufügen der erforderlichen NuGet-Pakete

Führen Sie den folgenden .NET Core-CLI-Befehl aus, um dem Projekt „SQLite“ und „CodeGeneration.Design“ hinzuzufügen:

```console
dotnet add package Microsoft.EntityFrameworkCore.SQLite
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
```

Das `Microsoft.VisualStudio.Web.CodeGeneration.Design`-Paket wird für den Gerüstbau benötigt.

<a name="reg"></a>

### <a name="register-the-database-context"></a>Registrieren des Datenbankkontexts

Fügen Sie am Anfang der Datei *Startup.cs* die folgenden `using`-Anweisungen ein.

```csharp
using MvcMovie.Models;
using Microsoft.EntityFrameworkCore;
```

Registrieren Sie den Datenbankkontext mit dem [Dependency Injection-Container](xref:fundamentals/dependency-injection) in `Startup.ConfigureServices`.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Startup.cs?name=snippet_UseSqlite&highlight=11-12)]

Erstellen Sie das Projekt zur Fehlerüberprüfung.