---
title: Bereiche in ASP.NET Core
author: rick-anderson
description: Erfahren Sie mehr über Bereiche, ein Feature von ASP.NET MVC, das für die Organisation von verwandten Funktionalitäten in einer Gruppe als separater Namespace (für Routing) und Ordnerstruktur (für Ansichten) verwendet wird.
ms.author: riande
ms.date: 02/14/2019
uid: mvc/controllers/areas
ms.openlocfilehash: c21eed04ea68512515da262b6b6895dc1a821039
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061707"
---
# <a name="areas-in-aspnet-core"></a>Bereiche in ASP.NET Core

Von [Dhananjay Kumar](https://twitter.com/debug_mode) und [Rick Anderson](https://twitter.com/RickAndMSFT)

Bereiche sind ein Feature von ASP.NET, das für die Organisation von verwandten Funktionalitäten in eine Gruppe als separater Namespace (für Routing) und Ordnerstruktur (für Ansichten) verwendet wird. Mithilfe von Bereichen wird außerdem eine Hierarchie erstellt, damit das Routing durch Hinzufügen eines anderen Routenparameters ausgeführt werden kann: `area` zu `controller` und `action` oder einer Razor Page `page`.

Bereiche ermöglichen es, eine ASP.NET Core-Web-App in kleinere funktionale Gruppen zu partitionieren. Jede dieser Gruppen hat dabei ihre eigene Menge an Razor Pages, Controller, Ansichten und Modellen. Ein Bereich ist im Grunde genommen eine Struktur in einer App. In einem ASP.NET Core-Webprojekt werden logische Komponenten wie Seiten, Modelle, Controller und Ansichten in verschiedenen Ordner aufbewahrt. Die ASP.NET Core-Runtime verwendet Namenskonventionen, um die Beziehung zwischen diesen Komponenten zu erstellen. Bei einer großen App kann es von Vorteil sein, die App in mehrere Bereiche mit hoher Funktionalität aufzuteilen. Dies gilt z.B. für eine E-Commerce-App mit mehreren Geschäftseinheiten, wie Auftragsabschluss, Abrechnung und Suche. Jede dieser Einheiten hat ihre eigenen Bereiche, die Ansichten, Controller, Razor Pages und Modelle enthalten.

Die Verwendung von Bereichen in einem Projekt ist erwägenswert, wenn:

* Ihre App aus mehreren funktionalen Komponenten auf hoher Ebene besteht, die logisch getrennt sein können.
* Sie Ihre App partitionieren möchten, damit jeder funktionale Bereich unabhängig voneinander bearbeitet werden kann.

[Zeigen Sie Beispielcode an, oder laden Sie diesen herunter](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample)). Das Downloadbeispiel stellt eine einfache App für Testbereiche zur Verfügung.

## <a name="areas-for-controllers-with-views"></a>Bereiche für Controller mit Ansichten

Eine typische ASP.NET Core-Web-App, die Bereiche, Controller und Ansichten verwendet, beinhaltet Folgendes:

* Eine [Bereichsordnerstruktur](#area-folder-structure).
* Controller, die mit dem Attribut [&lbrack;Bereich&rbrack;](#attribute) versehen wurden, um dem Controller den Bereich zuzuordnen: [!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?name=snippet2)]
* Die [Bereichsroute, die dem Startup hinzugefügt wurde](#add-area-route): [!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet2&highlight=3-6)]

## <a name="area-folder-structure"></a>Bereichsordnerstruktur
Stellen Sie sich eine App vor, die zwei logische Gruppen hat, *Produkte* und *Dienste*. Wenn Bereiche verwendet werden, würde die Ordnerstruktur ähnlich dem Folgenden aussehen:

* Projektname
  * Bereiche
    * Products
      * Controller
        * HomeController.cs
        * ManageController.cs
      * Ansichten
        * Startseite
          * Index.cshtml
        * Verwalten
          * Index.cshtml
          * About.cshtml
    * Dienste
      * Controller
        * HomeController.cs
      * Ansichten
        * Startseite
          * Index.cshtml

Während das vorherige Layout typisch ist, wenn Bereiche verwendet werden, müssen nur die Ansichtsdateien diese Ordnerstruktur verwenden. Die Ansichtsermittlung sucht nach einer passenden Bereichsansichtsdatei im folgenden Ordner:

```text
/Areas/<Area-Name>/Views/<Controller-Name>/<Action-Name>.cshtml
/Areas/<Area-Name>/Views/Shared/<Action-Name>.cshtml
/Views/Shared/<Action-Name>.cshtml
/Pages/Shared/<Action-Name>.cshtml
   ```

Der Speicherort von Ordnern, die sich nicht auf die Ansicht beziehen, wie *Controller* und *Modelle* spielt **keine** Rolle. Die Ordner *Controller* und *Modelle* werden z.B. nicht benötigt. Der Inhalt von *Controller* und *Modelle* ist Code, der in eine .dll-Datei kompiliert wird. Der Inhalt von *Ansichten* wird nicht kompiliert, bis eine Anforderung an diese Ansicht gestellt wird.

<!-- TODO review:
The content of the *Views* isn't compiled until a request to that view has been made.

What about precompiled views? 
 -->
<a name="attribute"></a>

### <a name="associate-the-controller-with-an-area"></a>Zuordnen eines Controllers zu einem Bereich

Bereichscontroller werden mit dem Attribut [&lbrack;Bereich&rbrack;](xref:Microsoft.AspNetCore.Mvc.AreaAttribute) versehen:

[!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?highlight=5&name=snippet)]

### <a name="add-area-route"></a>Hinzufügen einer Bereichsroute

Bereichsrouten verwenden normalerweise konventionelles Routing anstatt Attributrouting. Beim herkömmlichen Routing ist die Reihenfolge wichtig. Routen mit Bereichen werden im Allgemeinen früher in der Routentabelle aufgeführt als die spezifischeren Routen ohne Bereich.

`{area:...}` kann als Token in Routenvorlagen verwendet werden, wenn der URL-Raum in allen Bereichen einheitlich ist:

[!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet&highlight=18-21)]

Im vorherigen Code wendet `exists` eine Einschränkung an: Die Route muss mit einem Bereich übereinstimmen. `{area:...}` zu verwenden ist die unkomplizierteste Methode, um Bereichen Routing hinzuzufügen.

Im folgenden Code wird <xref:Microsoft.AspNetCore.Builder.MvcAreaRouteBuilderExtensions.MapAreaRoute*> verwendet, um zwei benannte Bereichsrouten zu erstellen:

[!code-csharp[](areas/samples/MVCareas/StartupMapAreaRoute.cs?name=snippet&highlight=18-27)]

Wenn `MapAreaRoute` mit ASP.NET Core 2.2 verwendet werden soll, sehen Sie sich diesen [GitHub-Artikel](https://github.com/aspnet/AspNetCore/issues/7772) an.

Weitere Informationen finden Sie im Artikel [Routing zu Controlleraktionen in ASP.NET Core](xref:mvc/controllers/routing#areas).

### <a name="link-generation-with-areas"></a>Erstellen von Links mit Bereichen

Im folgenden Code aus dem [Beispieldownload](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) sehen Sie die Erstellung eines Links mit dem angegebenen Bereich:

[!code-cshtml[](areas/samples/MVCareas/Views/Shared/_testLinksPartial.cshtml?name=snippet)]

Links, die mit dem vorherigen Code erstellt wurden, gelten überall in der App.

Im Beispieldownload ist eine [partielle Ansicht](xref:mvc/views/partial) enthalten, die die vorherigen Links und dieselben Links beinhaltet, ohne dass der Bereich angegeben wird. In der [Layoutdatei]() wird auf die partielle Ansicht verwiesen. Jede Seite in der App stellt also die erstellen Links dar. Die Links, die ohne Angabe eines Bereichs erstellt werden, sind nur gültig, wenn auf sie von einer Seite im selben Bereich und Controller verwiesen wird.

Wenn der Bereich oder der Kontroller nicht angegeben werden, hängt das Routing von den *Umgebungswerten* ab. Die aktuellen Routenwerte der aktuellen Anforderung werden bei der Linkgenerierung als Umgebungswerte behandelt. Oft werden ungültige Links erstellt, wenn für die Beispiel-App die Umgebungswerte verwendet werden.

Weitere Informationen finden Sie unter [Routing zu Controlleraktionen in ASP.NET Core](xref:mvc/controllers/routing).

### <a name="shared-layout-for-areas-using-the-viewstartcshtml-file"></a>Freigegebenes Layout für Bereiche unter Verwendung der _ViewStart.cshtml-Datei

Um ein gemeinsames Layout für die gesamte App freizugeben, verschieben Sie *_ViewStart.cshtml* in den Stammordner der Anwendung.

<!-- This section will be completed after https://github.com/aspnet/Docs/pull/10978 is merged.
<a name="arp"></a>

## Areas for Razor Pages
-->
<a name="rename"></a>

### <a name="change-default-area-folder-where-views-are-stored"></a>Ändern des Standardbereichsordners, in dem Ansichten gespeichert sind

Der folgende Code ändert den Standardbereichsordner von `"Areas"` in `"MyAreas"`:

[!code-csharp[](areas/samples/MVCareas/Startup2.cs?name=snippet)]

<!-- TODO review - can we delete this. Areas doesn't change publishing - right? -->
### <a name="publishing-areas"></a>Veröffentlichen von Bereichen

Alle `*.cshtml`- und `wwwroot/**`-Dateien werden für die Ausgabe veröffentlicht, wenn `<Project Sdk="Microsoft.NET.Sdk.Web">` in der *CSPROJ*-Datei enthalten ist.
