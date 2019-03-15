---
title: Wiederverwendbare Razor-Benutzeroberfläche in Klassenbibliotheken mit ASP.NET Core
author: Rick-Anderson
description: Es wird erläutert, wie wiederverwendbare Teilansichten in einer Klassenbibliothek in ASP.NET Core mit Razor-Benutzeroberfläche zu erstellen.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/07/2018
ms.custom: seodec18
uid: razor-pages/ui-class
ms.openlocfilehash: e5f329dcc423a7b7d6c247d0d359d35d95283de4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030237"
---
# <a name="create-reusable-ui-using-the-razor-class-library-project-in-aspnet-core"></a>Erstellen von wiederverwendbaren Benutzeroberfläche, die mit dem Razor-Klassenbibliotheksprojekt in ASP.NET Core

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

Ansichten, Seiten, Controller, Seitenmodelle, [Ansichtskomponenten](xref:mvc/views/view-components) und Datenmodelle im Zusammenhang mit Razor können in einer Razor-Klassenbibliothek (Razor Class Library, RCL) zusammengefasst und erstellt werden. Die RCL kann verpackt und wiederverwendet werden. Sie kann in Anwendungen eingebunden werden, wodurch sich die in der RCL enthaltenen Ansichten und Seiten überschreiben lassen. Wenn eine Ansicht, Teilansicht oder Razor-Seite sowohl in der Web-App als auch in der RCL enthalten ist, hat das Razor-Markup (die *CSHTML*-Datei) in der Web-App Vorrang.

Dieses Feature erfordert [!INCLUDE[](~/includes/2.1-SDK.md)]

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/ui-class/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

## <a name="create-a-class-library-containing-razor-ui"></a>Erstellen einer Klassenbibliothek, die eine Razor-Benutzeroberfläche enthält

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Klicken Sie in Visual Studio im Menü **Datei** auf **Neu** > **Projekt**.
* Wählen Sie **ASP.NET Core-Webanwendung** aus.
* Geben Sie der Bibliothek einen Namen (z.B. „RazorClassLib“), und klicken Sie anschließend auf **OK**. Stellen Sie sicher, dass der Bibliotheksname nicht auf `.Views` endet, um zu verhindern, dass es zu einem Dateinamenkonflikt mit der generierten Ansichtsbibliothek kommt.
* Überprüfen Sie, ob **ASP.NET Core 2.1** oder höher ausgewählt ist.
* Klicken Sie auf **Razor Class Library** (Razor-Klassenbibliothek) > **OK**.

Eine Razor-Klassenbibliothek verfügt über die folgende Projektdatei:

[!code-xml[Main](ui-class/samples/cli/RazorUIClassLib/RazorUIClassLib.csproj)]

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Führen Sie `dotnet new razorclasslib` über die Befehlszeile aus. Zum Beispiel:

```console
dotnet new razorclasslib -o RazorUIClassLib
```

Weitere Informationen finden Sie unter [dotnet new](/dotnet/core/tools/dotnet-new). Stellen Sie sicher, dass der Bibliotheksname nicht auf `.Views` endet, um zu verhindern, dass es zu einem Dateinamenkonflikt mit der generierten Ansichtsbibliothek kommt.

------
Fügen Sie der RCL Razor-Dateien hinzu.

ASP.NET Core-Vorlagen wird davon ausgegangen, der RCL Inhalt befindet sich in der *Bereiche* Ordner. Finden Sie unter [RCL Seitenlayout](#afs) zum Erstellen der Inhalte in einer RCL, die verfügbar gemacht `~/Pages` statt `~/Areas/Pages`.

## <a name="referencing-razor-class-library-content"></a>Verweisen auf RCL-Inhalte

Folgende Komponenten können auf die RCL verweisen:

* NuGet-Pakete. Weitere Informationen finden Sie unter [Creating NuGet packages](/nuget/create-packages/creating-a-package) (Erstellen von NuGet-Paketen), [dotnet add package](/dotnet/core/tools/dotnet-add-package) und [Erstellen und Veröffentlichen eines NuGet-Pakets](/nuget/quickstart/create-and-publish-a-package-using-visual-studio).
* *{ProjectName}.csproj*-Dateien. Weitere Informationen finden Sie unter [dotnet add reference](/dotnet/core/tools/dotnet-add-reference).

## <a name="walkthrough-create-a-razor-class-library-project-and-use-from-a-razor-pages-project"></a>Exemplarische Vorgehensweise: Erstellen Sie einer Razor-Class-Library-Projekt aus und ein Projekt mit Razor Pages

Sie können das [vollständige Projekt](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/ui-class/samples) herunterladen und testen, anstatt es zu erstellen. Der Beispieldownload enthält zusätzlichen Code sowie Links, die das Testen des Projekts erleichtern. [In diesem GitHub-Issue](https://github.com/aspnet/Docs/issues/6098) können Sie in Form von Kommentaren Feedback zu Unterschieden zwischen Beispieldownloads und ausführlichen Anleitungen geben.

### <a name="test-the-download-app"></a>Testen der heruntergeladenen App

Wenn Sie die vollständige App nicht heruntergeladen haben und das Beispielprojekt selbst erstellen möchten, können Sie mit dem [nächsten Abschnitt](#create-a-razor-class-library) fortfahren.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Öffnen Sie die *SLN*-Datei in Visual Studio. Führen Sie die App aus.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Erstellen Sie über die Eingabeaufforderung im *cli*-Verzeichnis die RCL und die Web-App.

```console
dotnet build
```

Wechseln Sie ins Verzeichnis *WebApp1*, und führen Sie die App aus:

```console
dotnet run
```

------

Folgen Sie den Anweisungen in [Testen des WebApp1-Projekts](#test).

## <a name="create-a-razor-class-library"></a>Erstellen einer RCL

In diesem Abschnitt wird das Erstellen einer RCL beschrieben. Dabei werden der RCL Razor-Dateien hinzugefügt.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Erstellen Sie das RCL-Projekt:

* Klicken Sie in Visual Studio im Menü **Datei** auf **Neu** > **Projekt**.
* Wählen Sie **ASP.NET Core-Webanwendung** aus.
* Benennen Sie die app **RazorUIClassLib** > **OK**.
* Überprüfen Sie, ob **ASP.NET Core 2.1** oder höher ausgewählt ist.
* Klicken Sie auf **Razor Class Library** (Razor-Klassenbibliothek) > **OK**.
* Fügen Sie eine Razor-Datei für die Teilansicht mit dem Namen „_Message.cshtml“ unter *RazorUIClassLib/Areas/MyFeature/Pages/Shared* hinzu.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Führen Sie die folgenden Befehle über die Befehlszeile aus:

```console
dotnet new razorclasslib -o RazorUIClassLib
dotnet new page -n _Message -np -o RazorUIClassLib/Areas/MyFeature/Pages/Shared
dotnet new viewstart -o RazorUIClassLib/Areas/MyFeature/Pages
```

Die obenstehenden Befehle haben folgende Konsequenzen:

* Die `RazorUIClassLib`-RCL wird erstellt.
* Die Seite „Razor_Message“ wird erstellt und der RCL hinzugefügt. Durch den `-np`-Parameter wird die Seite ohne `PageModel` erstellt.
* Erstellt eine [_ViewStart.cshtml](xref:mvc/views/layout#running-code-before-each-view) Datei und fügt es der RCL hinzu.

Die *_ViewStart.cshtml* Datei ist erforderlich, um das Layout des Projekts mit Razor Pages verwenden (die im nächsten Abschnitt hinzugefügt wird).

------

### <a name="add-razor-files-and-folders-to-the-project"></a>Razor-Dateien und Ordner zum Projekt hinzufügen

* Ersetzen Sie das Markup in *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* durch den folgenden Code:

[!code-cshtml[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* Ersetzen Sie das Markup in *RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml* durch den folgenden Code:

[!code-cshtml[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml)]

`@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers` ist erforderlich, um die Teilansicht `<partial name="_Message" />` verwenden zu können. Wenn Sie nicht die `@addTagHelper`-Anweisung einbinden möchten, können Sie die Datei *_ViewImports.cshtml* hinzufügen. Zum Beispiel:

```console
dotnet new viewimports -o RazorUIClassLib/Areas/MyFeature/Pages
```

Weitere Informationen zu *_ViewImports.cshtml*, finden Sie unter [freigegebenen Richtlinien importieren](xref:mvc/views/layout#importing-shared-directives)

* Erstellen Sie die Klassenbibliothek, um sicherzustellen, dass keine Compilerfehler vorliegen:

```console
dotnet build RazorUIClassLib
```

Die Buildausgabe enthält *RazorUIClassLib.dll* und *RazorUIClassLib.Views.dll*. *RazorUIClassLib.Views.dll* enthält den kompilierten Razor-Inhalt.

### <a name="use-the-razor-ui-library-from-a-razor-pages-project"></a>Verwenden der Razor-Benutzeroberflächenbibliothek über ein Razor-Seiten-Projekt

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Erstellen Sie die Web-App mit Razor-Seiten:

* Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf die Projektmappe und anschließend auf **Hinzufügen** >  **Neues Projekt**.
* Wählen Sie **ASP.NET Core-Webanwendung** aus.
* Legen Sie als Namen für die App **WebApp1** fest.
* Überprüfen Sie, ob **ASP.NET Core 2.1** oder höher ausgewählt ist.
* Klicken Sie auf **Webanwendung** > **OK**.

* Klicken Sie im **Projektmappen-Explorer** zuerst mit der rechten Maustaste auf **WebApp1** und anschließend auf **Als Startprojekt festlegen**.
* Klicken Sie im **Projektmappen-Explorer** zuerst mit der rechten Maustaste auf **WebApp1** und anschließend auf **Buildabhängigkeiten** > **Projektabhängigkeiten**.
* Aktivieren Sie für **WebApp1** die Abhängigkeit **RazorUIClassLib**.
* Klicken Sie im **Projektmappen-Explorer** zuerst mit der rechten Maustaste auf **WebApp1** und anschließend auf **Hinzufügen** > **Verweis**.
* Aktivieren Sie im Dialogfeld **Verweis-Manager** das Kontrollkästchen neben **RazorUIClassLib**, und klicken Sie anschließend auf **OK**.

Führen Sie die App aus.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core-CLI](#tab/netcore-cli)

Erstellen Sie eine Web-App mit Razor-Seiten und eine Projektmappendatei, die die Razor-Seiten-App und die RCL enthält:

```console
dotnet new webapp -o WebApp1
dotnet new sln
dotnet sln add WebApp1
dotnet sln add RazorUIClassLib
dotnet add WebApp1 reference RazorUIClassLib
```

Erstellen Sie die Web-App, und führen Sie sie aus:

```console
cd WebApp1
dotnet run
```

---

<a name="test"></a>

### <a name="test-webapp1"></a>Testen des WebApp1-Projekts

Überprüfen Sie, ob die Razor-Benutzeroberflächenbibliothek verwendet wird.

* Wechseln Sie zu `/MyFeature/Page1`.

## <a name="override-views-partial-views-and-pages"></a>Überschreiben von Ansichten, Teilansichten und Seiten

Wenn eine Ansicht, Teilansicht oder Razor-Seite sowohl in der Web-App als auch in der RCL enthalten ist, hat das Razor-Markup (die *CSHTML*-Datei) in der Web-App Vorrang. Fügen Sie z. B. *WebApp1/Areas/MyFeature/Pages/Page1.cshtml* auf "WebApp1", und Seite1 aus dem "WebApp1" Vorrang vor Seite1 aus der Razor-Klassenbibliothek.

Ob Page1 in WebApp1 tatsächlich die Priorität zugeordnet wird, können Sie testen, indem Sie im Beispieldownload *WebApp1/Areas/MyFeature2* in *WebApp1/Areas/MyFeature* umbenennen.

Kopieren Sie die Teilansicht *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* nach *WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml*. Aktualisieren Sie das Markup, um den neuen Speicherort anzugeben. Erstellen Sie die App, und führen Sie sie aus, um sicherzustellen, dass die Version mit der Teilansicht der App verwendet wird.

<a name="afs"></a>

### <a name="rcl-pages-layout"></a>RCL Seitenlayout

Auf Inhalt RCL, als wäre es Teil der Web-app-Verweis *Seiten* Ordner das RCL-Projekt erstellen, mit der folgenden Dateistruktur:

* *RazorUIClassLib/Seiten*
* *RazorUIClassLib/Pages/Shared*

Nehmen wir an *RazorUIClassLib/Pages/Shared* enthält zwei partielle Dateien: *_Header.cshtml* und *_Footer.cshtml*. Die `<partial>` können Tags hinzugefügt werden *"_Layout.cshtml"* Datei:
  
```cshtml
<body>
  <partial name="_Header">
  @RenderBody()
  <partial name="_Footer">
</body>
```
