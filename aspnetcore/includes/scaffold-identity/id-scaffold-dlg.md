---
ms.openlocfilehash: e5c80c80380dadfce9cff5ec268535076258d980
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041117"
---
Führen Sie die Identity-gerüstbauer:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Von **Projektmappen-Explorer**, mit der rechten Maustaste auf das Projekt > **hinzufügen** > **neues Gerüstelement**.
* Im linken Bereich, der die **Gerüst hinzufügen** wählen Sie im Dialogfeld **Identität** > **hinzufügen**.
* In der **ADD Identity** Dialogfeld Wählen Sie die gewünschten Optionen.
  * Wählen Sie Ihre vorhandene Layoutseite, oder durch falsche Markup die Layoutdatei überschrieben werden. Z. B. `~/Pages/Shared/_Layout.cshtml` für Razor-Seiten `~/Views/Shared/_Layout.cshtml` für MVC-Projekte
  * Wählen Sie die **+** Schaltfläche zum Erstellen eines neuen **Datenkontextklasse**.
* Wählen Sie **hinzufügen**.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Wenn Sie die ASP.NET Core-gerüstbauer noch nicht installiert haben, installieren Sie es jetzt:

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

Fügen Sie einen Paketverweis auf [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) auf das Projekt (\*csproj) Datei. Führen Sie den folgenden Befehl im Verzeichnis Projekts ein:

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

Führen Sie den folgenden Befehl zum Auflisten von Optionen gerüstbauer Identität:

```cli
dotnet aspnet-codegenerator identity -h
```

Führen Sie im Projektordner der gerüstbauer Identität, mit der gewünschten Optionen. Führen Sie z. B. um die Identität mit der standardmäßigen UI und die minimale Anzahl von Dateien einrichten, den folgenden Befehl ein:

```cli
dotnet aspnet-codegenerator identity --useDefaultUI
```

-------------
