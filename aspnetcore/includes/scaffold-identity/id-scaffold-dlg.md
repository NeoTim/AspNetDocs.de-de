---
ms.openlocfilehash: e5c80c80380dadfce9cff5ec268535076258d980
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041117"
---
<span data-ttu-id="8fa1f-101">Führen Sie die Identity-gerüstbauer:</span><span class="sxs-lookup"><span data-stu-id="8fa1f-101">Run the Identity scaffolder:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="8fa1f-102">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8fa1f-102">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="8fa1f-103">Von **Projektmappen-Explorer**, mit der rechten Maustaste auf das Projekt > **hinzufügen** > **neues Gerüstelement**.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-103">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="8fa1f-104">Im linken Bereich, der die **Gerüst hinzufügen** wählen Sie im Dialogfeld **Identität** > **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-104">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="8fa1f-105">In der **ADD Identity** Dialogfeld Wählen Sie die gewünschten Optionen.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-105">In the **ADD Identity** dialog, select the options you want.</span></span>
  * <span data-ttu-id="8fa1f-106">Wählen Sie Ihre vorhandene Layoutseite, oder durch falsche Markup die Layoutdatei überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-106">Select your existing layout page, or your layout file will be overwritten with incorrect markup.</span></span> <span data-ttu-id="8fa1f-107">Z. B. `~/Pages/Shared/_Layout.cshtml` für Razor-Seiten `~/Views/Shared/_Layout.cshtml` für MVC-Projekte</span><span class="sxs-lookup"><span data-stu-id="8fa1f-107">For example `~/Pages/Shared/_Layout.cshtml` for Razor Pages `~/Views/Shared/_Layout.cshtml` for MVC projects</span></span>
  * <span data-ttu-id="8fa1f-108">Wählen Sie die **+** Schaltfläche zum Erstellen eines neuen **Datenkontextklasse**.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-108">Select the **+** button to create a new **Data context class**.</span></span>
* <span data-ttu-id="8fa1f-109">Wählen Sie **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-109">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="8fa1f-110">.NET Core-CLI</span><span class="sxs-lookup"><span data-stu-id="8fa1f-110">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="8fa1f-111">Wenn Sie die ASP.NET Core-gerüstbauer noch nicht installiert haben, installieren Sie es jetzt:</span><span class="sxs-lookup"><span data-stu-id="8fa1f-111">If you have not previously installed the ASP.NET Core scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="8fa1f-112">Fügen Sie einen Paketverweis auf [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) auf das Projekt (\*csproj) Datei.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-112">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (\*.csproj) file.</span></span> <span data-ttu-id="8fa1f-113">Führen Sie den folgenden Befehl im Verzeichnis Projekts ein:</span><span class="sxs-lookup"><span data-stu-id="8fa1f-113">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="8fa1f-114">Führen Sie den folgenden Befehl zum Auflisten von Optionen gerüstbauer Identität:</span><span class="sxs-lookup"><span data-stu-id="8fa1f-114">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="8fa1f-115">Führen Sie im Projektordner der gerüstbauer Identität, mit der gewünschten Optionen.</span><span class="sxs-lookup"><span data-stu-id="8fa1f-115">In the project folder, run the Identity scaffolder with the options you want.</span></span> <span data-ttu-id="8fa1f-116">Führen Sie z. B. um die Identität mit der standardmäßigen UI und die minimale Anzahl von Dateien einrichten, den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="8fa1f-116">For example, to setup identity with the default UI and the minimum number of files, run the following command:</span></span>

```cli
dotnet aspnet-codegenerator identity --useDefaultUI
```

-------------
