---
title: Hinzufügen einer Ansicht zu einer ASP.NET Core MVC-App
author: rick-anderson
description: Hinzufügen einer Ansicht zu einer einfachen ASP.NET Core MVC-App
ms.author: riande
ms.date: 03/04/2017
uid: tutorials/first-mvc-app/adding-view
ms.openlocfilehash: 32eddb233a8a6b9b8f480926673d15d568ce6ede
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032337"
---
# <a name="add-a-view-to-an-aspnet-core-mvc-app"></a>Hinzufügen einer Ansicht zu einer ASP.NET Core MVC-App

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

In diesem Abschnitt ändern Sie die `HelloWorldController`-Klasse so, dass [Razor](xref:mvc/views/razor)-Ansichtsdateien verwendet werden, um den Prozess des Generierens von HTML-Antworten für einen Client sauber zu kapseln.

Sie erstellen eine Ansichtsvorlagendatei mithilfe von Razor. Razor-basierte Ansichtsvorlagen haben die Dateinamenerweiterung *.cshtml*. Sie bieten eine elegante Möglichkeit zum Erstellen einer HTML-Ausgabe mit C#.

Derzeit gibt die `Index`-Methode eine Zeichenfolge mit der Meldung zurück, die in der Controllerklasse hartcodiert ist. Ersetzen Sie in der `HelloWorldController`-Klasse die `Index`-Methode durch den folgenden Code:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_4)]

Der vorangehende Code ruft die Methode<xref:Microsoft.AspNetCore.Mvc.Controller.View*> des Controllers auf. Er verwendet eine Ansichtsvorlage zum Generieren einer HTML-Antwort. Controllermethoden (auch *Aktionsmethoden* genannt), wie z. B. die `Index`-Methode oben, geben in der Regel ein <xref:Microsoft.AspNetCore.Mvc.IActionResult> (oder eine von <xref:Microsoft.AspNetCore.Mvc.ActionResult> abgeleitete Klasse) und keinen Typ wie `string` zurück.

## <a name="add-a-view"></a>Hinzufügen einer Ansicht

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* Klicken Sie mit der rechten Maustaste auf den Ordner *Views*, und klicken Sie dann **Hinzufügen > Neuer Ordner**. Nennen Sie den Ordner *HelloWorld*.

* Klicken Sie mit der rechten Maustaste auf den Ordner *Views/HelloWorld*, und klicken Sie dann **Hinzufügen > Neues Element**.

* Im Dialogfeld **Neues Element hinzufügen: MvcMovie**

  * Geben Sie in das Suchfeld rechts oben *Ansicht* ein.

  * Wählen Sie **Razor-Ansicht** aus.

  * Übernehmen Sie den im Feld **Name** stehenden Wert *Index.cshtml*.

  * Wählen Sie **Hinzufügen** aus.

![Dialogfeld „Neues Element hinzufügen“](adding-view/_static/add_view.png)

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

Fügen Sie die Ansicht `Index` für `HelloWorldController` hinzu.

* Fügen Sie einen neuen Ordner namens *Views/HelloWorld* hinzu.
* Fügen Sie dem Ordner *Views/HelloWorld* eine neue Datei namens *Index.cshtml* hinzu.

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio für Mac](#tab/visual-studio-mac)

* Klicken Sie mit der rechten Maustaste auf den Ordner *Views*, und klicken Sie dann **Hinzufügen > Neuer Ordner**. Nennen Sie den Ordner *HelloWorld*.
* Klicken Sie mit der rechten Maustaste auf den Ordner *Views/HelloWorld*, und klicken Sie dann **Hinzufügen > Neue Datei**.
* Führen Sie im Dialogfeld **Neue Datei** folgende Aktionen aus:

  * Wählen Sie im linken Bereich **Web** aus.
  * Wählen Sie im mittleren Bereich **Leere HTML-Datei** aus.
  * Geben Sie *Index.cshtml* in das Feld **Name** ein.
  * Wählen Sie **Neu** aus.

![Dialogfeld „Neues Element hinzufügen“](adding-view/_static/add_view.png)

---  
<!-- End of VS tabs -->

Ersetzen Sie den Inhalt der Razor-Ansichtsdatei *Views/HelloWorld/Index.cshtml* durch Folgendes:

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/HelloWorld/Index1.cshtml?highlight=7)]

Navigieren Sie zu `https://localhost:xxxx/HelloWorld`. Die `Index`-Methode im `HelloWorldController` hatte nicht viel zu tun. Sie diente zum Ausführen der Anweisung `return View();`, die angab, dass die Methode eine Ansichtsvorlagendatei zum Rendern einer Antwort im Browser verwenden sollte. Da Sie den Namen der Ansichtsvorlagendatei nicht explizit angegeben haben, verwendete MVC standardmäßig die Ansichtsdatei *Index.cshtml* im Ordner */Views/HelloWorld*. Die folgende Abbildung zeigt die Zeichenfolge "Hello from our View Template!“, die in der Ansicht hartcodiert ist.

![Browserfenster](~/tutorials/first-mvc-app/adding-view/_static/hell_template.png)

## <a name="change-views-and-layout-pages"></a>Ändern von Ansichten und Layoutseiten

Wählen Sie die Menülinks aus (**MvcMovie**, **Home**, **Privacy**). Auf jeder Seite wird dasselbe Menülayout gezeigt. Das Menülayout wird mithilfe der Datei *Views/Shared/_Layout.cshtml* implementiert. Öffnen Sie die Datei *Views/Shared/_Layout.cshtml*.

[Layout](xref:mvc/views/layout)-Vorlagen ermöglichen Ihnen, das HTML-Containerlayout Ihrer Website zentral anzugeben und dann auf mehrere Seiten Ihrer Website anzuwenden. Suchen Sie die Zeile `@RenderBody()`. `RenderBody` ist ein Platzhalter, bei dem alle ansichtsspezifischen Seiten, die Sie erstellen, von der Layoutseite *umschlossen* angezeigt werden. Wenn Sie beispielsweise den Link **Privacy** auswählen, wird die Ansicht **Views/Home/Privacy.cshtml** in der `RenderBody`-Methode gerendert.

## <a name="change-the-title-footer-and-menu-link-in-the-layout-file"></a>Ändern des Titels, der Fußzeile und Menülinks in der Layoutdatei

* Ändern Sie in den Elementen „Titel“ und „Fußzeile“ `MvcMovie` in `Movie App`.
* Ändern Sie das Ankerlement `<a class="navbar-brand" asp-area="" asp-controller="Home" asp-action="Index">MvcMovie</a>` in `<a class="navbar-brand" asp-controller="Movies" asp-action="Index">Movie App</a>`.

Im folgenden Markup sind die Änderungen hervorgehoben dargestellt:

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Shared/_Layout.cshtml?highlight=6,24,51)]

Im obigen Markup wurde das `asp-area`-[Anchor-Taghilfsprogramm Attribut](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) weggelassen, weil in dieser App keine [Bereiche](xref:mvc/controllers/areas) verwendet werden.

<!-- Routing has changed in 2.2, it's going to the last route.
>[!WARNING]
> We haven't implemented the `Movies` controller yet, so if you click the `Movie App` link, you get a 404 (Not found) error.
-->

**Hinweis:** Der `Movies`-Controller wurde nicht implementiert. An diesem Punkt ist der `Movie App`-Link nicht funktionsfähig.

Speichern Sie Ihre Änderungen, und wählen den **Privacy**-Link aus. Wie Sie sehen, wird auf der Browserregisterkarte der Titel **Privacy Policy - Movie App** anstelle des Titels **Privacy Policy - Mvc Movie** angezeigt:

![Registerkarte „Privacy“](~/tutorials/first-mvc-app/adding-view/_static/about2.png)

Wählen Sie den Link **Home** aus, und beachten Sie, dass im Text für den Titel und den Anker ebenfalls **Movie App** angezeigt wird. Wir haben also eine Änderung des Texts und Titels in der Layoutvorlage einmalig vorgenommen, die von der gesamten Website übernommen wird.

Untersuchen Sie die Datei *Views/_ViewStart.cshtml*:

```HTML
@{
    Layout = "_Layout";
}
```

Die Datei *Views/_ViewStart.cshtml* fügt jeder Ansicht die Datei *Views/Shared/_Layout.cshtml* hinzu. Die `Layout`-Eigenschaft kann verwendet werden, um eine andere Layoutansicht festzulegen, oder legen Sie sie auf `null` fest, damit keine Layoutdatei verwendet wird.

Ändern Sie den Titel und das `<h2>`-Element der Ansichtsdatei *Views/HelloWorld/Index.cshtml*:

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/HelloWorld/Index2.cshtml?highlight=2,5)]

Der Titel und das `<h2>`-Element sind geringfügig anders, sodass Sie sehen können, welcher Codeabschnitt die Anzeige ändert.

`ViewData["Title"] = "Movie List";` im Code oben legt die `Title`-Eigenschaft des Wörterbuchs `ViewData`auf „Movie List“ fest. Die `Title`-Eigenschaft wird im HTML-Element `<title>` der Layoutseite verwendet:

```HTML
<title>@ViewData["Title"] - Movie App</title>
   ```

Speichern Sie die Änderung, und navigieren Sie zu `https://localhost:xxxx/HelloWorld`. Sie sehen, dass sich der Browsertitel, die primäre Überschrift und die sekundären Überschriften geändert haben. (Wenn die Änderungen nicht im Browser angezeigt werden, zeigen Sie ggf. zwischengespeicherten Inhalt an. Drücken Sie in Ihrem Browser STRG+F5, um das Laden der Antwort vom Server zu erzwingen.) Der Titel des Browsers wird mithilfe des Elements `ViewData["Title"]` erstellt, das wir in der Ansichtsvorlange *Index.cshtml* festgelegt haben, und des zusätzlichen Elements „- Movie App“, das in der Layoutdatei hinzugefügt wurde.

Beachten Sie außerdem, wie der Inhalt der Ansichtsvorlage *Index.cshtml* mit der Ansichtsvorlage *Views/Shared/_Layout.cshtml* zusammengeführt und eine einzelne HTML-Antwort an den Browser gesendet wurde. Layoutvorlagen erleichtern ungemein das Vornehmen von Änderungen an allen Seiten in Ihrer Anwendung. Weitere Informationen dazu finden Sie unter [Layout](xref:mvc/views/layout).

![Ansicht mit Filmliste](~/tutorials/first-mvc-app/adding-view/_static/hell3.png)

Unser kleiner Beitrag zu den „Daten“ (in diesem Fall die Meldung "Hello from our View Template!") ist jedoch hartcodiert. Die MVC-Anwendung weist ein „V“ (View [Ansicht]) auf, und Sie verfügen über ein „C“ (Controller), aber noch nicht über ein „M“ (Modell).

## <a name="passing-data-from-the-controller-to-the-view"></a>Übergeben von Daten vom Controller an die Ansicht

Controlleraktionen werden als Antwort auf eine eingehende URL-Anforderung aufgerufen. Eine Controllerklasse ist der Ort, an dem der Code geschrieben wird, der die eingehenden Browseranforderungen verarbeitet. Der Controller ruft Daten aus einer Datenquelle ab und entscheidet, welche Art von Antwort an den Browser zurückgesendet wird. Ansichtsvorlagen können von einem Controller zum Generieren und Formatieren einer HTML-Antwort an den Browser verwendet werden.

Controller sind für die Bereitstellung der benötigten Daten zuständig, damit eine Ansichtsvorlage eine Antwort liefern kann. Eine bewährte Methode: Ansichtsvorlagen sollten **keine** Geschäftslogik ausführen bzw. nicht direkt mit einer Datenbank interagieren. Eine Ansichtsvorlage sollte stattdessen nur mit den Daten arbeiten, die ihr vom Controller bereitgestellt werden. Durch Beibehaltung dieser Bereichstrennung bleibt der Code übersichtlich, testfähig und verwaltbar.

Derzeit verwendet die `Welcome`-Methode in der `HelloWorldController`-Klasse die Parameter `name` und `ID` und gibt anschließend die Werte direkt an den Browser aus. Anstatt den Controller diese Antwort als Zeichenfolge rendern zu lassen, passen Sie den Controller so an, dass er eine Ansichtsvorlage verwendet. Die Ansichtsvorlage erstellt eine dynamische Antwort, was bedeutet, dass entsprechende Datenbestandteile vom Controller an die Ansicht übergeben werden müssen, damit eine Antwort erstellt wird. Lassen Sie hierzu den Controller die dynamischen Daten (Parameter), die die Ansichtsvorlage benötigt, in einem `ViewData`-Wörterbuch ablegen, auf das die Ansichtsvorlage zugreifen kann.

Ändern Sie in *HelloWorldController.cs* die `Welcome`-Methode so, dass die Werte `Message` und `NumTimes` dem Wörterbuch `ViewData` hinzugefügt werden. Das Wörterbuch `ViewData` ist ein dynamisches Objekt, was bedeutet, dass jeder beliebige Typ verwendet werden kann. Das `ViewData`-Objekt hat erst dann definierte Eigenschaften, wenn Sie ihm etwas hinzugefügt haben. Das [MVC-Modellbindungssystem](xref:mvc/models/model-binding) ordnet automatisch die benannten Parameter (`name` und `numTimes`) aus der Abfragezeichenfolge auf der Adressleiste den Parametern der Methode zu. Die vollständige Datei *HelloWorldController.cs* sieht wie folgt aus:

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/HelloWorldController.cs?name=snippet_5)]

Das Wörterbuchobjekt `ViewData` enthält Daten, die an die Ansicht übergeben werden. 

Erstellen Sie die Ansichtsvorlage für die Begrüßung namens *Views/HelloWorld/Welcome.cshtml*.

Erstellen Sie eine Schleife in der Ansichtsvorlage *Welcome.cshtml*, die „Hello“ `NumTimes` anzeigt. Ersetzen Sie den Inhalt von *Views/HelloWorld/Welcome.cshtml* durch Folgendes:

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/HelloWorld/Welcome.cshtml)]

Speichern Sie die Änderungen, und navigieren Sie zur folgenden URL:

`https://localhost:xxxx/HelloWorld/Welcome?name=Rick&numtimes=4`

Daten werden der URL entnommen und mithilfe der [MVC-Modellbindung](xref:mvc/models/model-binding) an den Controller übergeben. Der Controller packt die Daten in einem `ViewData`-Wörterbuch und übergibt das Objekt an die Ansicht. Die Ansicht rendert dann die Daten im HTML-Format im Browser.

![Die Ansicht „Privacy“ mit der Beschriftung „Welcome“ und der viermal gezeigten Wortfolge „Hello Rick“](~/tutorials/first-mvc-app/adding-view/_static/rick2.png)

Im obigen Beispiel wurde das Wörterbuch `ViewData` verwendet, um Daten vom Controller an eine Ansicht zu übergeben. Später in diesem Tutorial wird ein Ansichtsmodell verwendet, um Daten von einem Controller an eine Ansicht zu übergeben. Der Ansatz mit dem Ansichtsmodell für das Übergeben von Daten ist im Allgemeinen dem Ansatz mit dem Wörterbuch `ViewData` vorzuziehen. Weitere Informationen finden Sie in diesem Artikel zur [Verwendung von ViewBag, ViewData oder TempData](http://www.rachelappel.com/when-to-use-viewbag-viewdata-or-tempdata-in-asp-net-mvc-3-applications/) (in englischer Sprache).

Im nächsten Tutorial wird eine Filmdatenbank erstellt.

> [!div class="step-by-step"]
> [Zurück](adding-controller.md)
> [Weiter](adding-model.md)
