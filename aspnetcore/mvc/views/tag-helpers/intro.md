---
title: Taghilfsprogramme in ASP.NET Core
author: rick-anderson
description: Informationen zu Taghilfsprogrammen und deren Verwendung in ASP.NET Core
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2018
uid: mvc/views/tag-helpers/intro
ms.openlocfilehash: 4b9bceb3ce0153af2d9a30c402febe09707145b7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041237"
---
# <a name="tag-helpers-in-aspnet-core"></a>Taghilfsprogramme in ASP.NET Core

Von [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="what-are-tag-helpers"></a>Informationen zu Taghilfsprogrammen

Taghilfsprogramme ermöglichen serverseitigem Code das Mitwirken am Erstellen und Rendern von HTML-Elementen in Razor-Dateien. Beispielsweise kann der integrierte `ImageTagHelper` eine Versionsnummer an den Bildnamen anfügen. Bei jeder Änderung des Bilds generiert der Server eine neue eindeutige Version des Bilds, sodass Clients immer das aktuelle Bild (anstelle eines veralteten zwischengespeicherten Bilds) erhalten. Für häufige Aufgaben wie das Erstellen von Formularen und Links sowie das Laden von Objekten gibt es zahlreiche integrierte Taghilfsprogramme. Weitere Taghilfsprogramme sind in öffentlichen GitHub-Repositorys und als NuGet-Pakete verfügbar. Taghilfsprogramme werden in C# erstellt und sind für HTML-Elemente basierend auf dem Elementnamen, dem Attributnamen oder dem übergeordneten Tag konzipiert. Beispielsweise kann der integrierte `LabelTagHelper` für das HTML-`<label>`-Element verwendet werden, wenn die `LabelTagHelper`-Attribute angewendet werden. Wenn Sie sich mit [HTML-Hilfsprogrammen](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) auskennen,verringern Taghilfsprogramme die expliziten Übergänge zwischen HTML und C# in Razor-Ansichten. Häufig stellen HTML-Hilfsprogramme eine Alternative zu einem bestimmten Taghilfsprogramm dar. Allerdings ersetzen Taghilfsprogramme HTML-Hilfsprogramme nicht, und es gibt nicht für jedes HTML-Hilfsprogramm ein Taghilfsprogramm. Im Abschnitt [Taghilfsprogramme und HTML-Hilfsprogramme im Vergleich](#tag-helpers-compared-to-html-helpers) werden die Unterschiede detaillierter erläutert.

## <a name="what-tag-helpers-provide"></a>Vorteile eines Taghilfsprogramms

**Eine HTML-freundliche Entwicklung** Im Großen und Ganzen ist Razor-Markup, das Taghilfsprogramme verwendet, wie Standard-HTML aufgebaut. Front-End-Designer, die sich mit HTML, CSS oder JavaScript auskennen, können Razor bearbeiten, ohne sich mit der C#-Razor-Syntax auseinandersetzen zu müssen.

**Eine umfassende IntelliSense-Umgebung zum Erstellen von HTML und Razor-Markup** Dies stellt einen starken Kontrast zu HTML-Hilfsprogrammen dar – dem vorherigen Ansatz zum Erstellen von Markup in Razor-Ansichten auf Serverseite. Im Abschnitt [Taghilfsprogramme und HTML-Hilfsprogramme im Vergleich](#tag-helpers-compared-to-html-helpers) werden die Unterschiede detaillierter erläutert. Im Abschnitt [IntelliSense-Unterstützung für Taghilfsprogramme](#intellisense-support-for-tag-helpers) wird die IntelliSense-Umgebung beschrieben. Sogar Entwickler, die sich gut mit der Razor C#-Syntax auskennen, können mit Taghilfsprogrammen produktiver arbeiten als wenn sie C#-Razor-Markup schreiben würden.

**Produktiveres Arbeiten und Erstellen von stabilerem, zuverlässigerem und verwaltbarem Code mithilfe von Informationen, die nur auf dem Server verfügbar sind** Beispielsweise galt in der Vergangenheit für das Aktualisieren von Bildern, dass auch der Name des Bildes geändert werden muss, wenn das Bild geändert wurde. Bilder sollten zur Verbesserung der Leistung immer zwischengespeichert werden, denn wenn Sie nicht den Namen des Bildes ändern, kann es sein, dass Clients veraltete Kopien erhalten. In der Vergangenheit musste der Name des Bildes immer geändert werden, wenn dieses bearbeitet wurde, und jeder Verweis auf das Bild in der Web-App musste aktualisiert werden. Dies ist nicht nur ein sehr aufwendiges Verfahren, sondern auch eins, bei dem Fehler entstehen können. Sie könnten z.B. einen Verweis übersehen oder aus Versehen die falsche Zeichenfolge eingeben. Der integrierte `ImageTagHelper` führt dieses Verfahren automatisch durch. Das `ImageTagHelper`-Taghilfsprogramm kann eine Versionsnummer an den Bildnamen anfügen. Das bedeutet, dass der Server bei jeder Änderung eine neue eindeutige Version für das Bild generiert. Clients erhalten dann immer das aktuelle Bild. Die Verwendung des `ImageTagHelper` ist grundsätzlich kostenlos, bietet mehr Stabilität, und Sie sparen Zeit.

Die meisten integrierten Taghilfsprogramme sind für HTML-Standardelemente konzipiert und stellen serverseitige Attribute für die jeweiligen Elemente bereit. Das `<input>`-Element, das in vielen Ansichten im Ordner *Views/Accounts* (Ansichten/Konten) verwendet wird, enthält beispielsweise das `asp-for`-Attribut. Dieses Attribut extrahiert den Namen der angegebenen Modelleigenschaft, und fügt diesen in die gerenderte HTML-Seite ein. Gehen Sie von einer Razor-Ansicht mit folgendem Modell aus:

```csharp
public class Movie
{
    public int ID { get; set; }
    public string Title { get; set; }
    public DateTime ReleaseDate { get; set; }
    public string Genre { get; set; }
    public decimal Price { get; set; }
}
```

Das folgende Razor-Markup

```cshtml
<label asp-for="Movie.Title"></label>
```

wird der folgende HTML-Code generiert:

```html
<label for="Movie_Title">Title</label>
```

Das `asp-for`-Attribut wird von der `For`-Eigenschaft von [LabelTagHelper](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.labeltaghelper?view=aspnetcore-2.0) zur Verfügung gestellt. Weitere Informationen finden Sie unter [Erstellen von Taghilfsprogrammen](xref:mvc/views/tag-helpers/authoring).

## <a name="managing-tag-helper-scope"></a>Verwalten des Taghilfsprogrammbereichs

Der Taghilfsprogrammbereich wird über eine Kombination aus `@addTagHelper`, `@removeTagHelper` und dem Deaktivierungszeichen „!“ gesteuert.

<a name="add-helper-label"></a>

### <a name="addtaghelper-makes-tag-helpers-available"></a>`@addTagHelper` stellt Taghilfsprogramme zur Verfügung.

Wenn Sie eine neue ASP.NET Core-Web-App mit dem Namen *AuthoringTagHelpers* erstellen, wird die folgende *Views/_ViewImports.cshtml*-Datei Ihrem Projekt hinzugefügt:

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=2&range=2-3)]

Über die `@addTagHelper`-Anweisung werden Taghilfsprogramme in der Ansicht zur Verfügung gestellt. In diesem Fall ist *Pages/_ViewImports.cshtml* die Ansichtsdatei, die standardmäßig von allen Dateien im *Pages*-Ordner und den Unterordnern geerbt wird. Dadurch werden Taghilfsprogramme zur Verfügung gestellt. Im obenstehenden Code wird die Platzhaltersyntax („\*“) verwendet, um anzugeben, dass alle in der Assembly (*Microsoft.AspNetCore.Mvc.TagHelpers*) festgelegten Taghilfsprogramme für alle Ansichtsdateien im *Views*-Verzeichnis bzw. -Unterverzeichnis verfügbar sind. Über den ersten Parameter nach `@addTagHelper` wird das Taghilfsprogramm geladen („\*“ wird für alle Taghilfsprogramme verwendet), und über den zweiten Parameter „Microsoft.AspNetCore.Mvc.TagHelpers“ wird die Assembly angegeben, die die Taghilfsprogramme enthält. Bei *Microsoft.AspNetCore.Mvc.TagHelpers* handelt es sich um die Assembly für die integrierten ASP.NET Core-Taghilfsprogramme.

Verwenden Sie folgenden Code, wenn Sie alle Taghilfsprogramme in diesem Projekt zur Verfügung stellen wollen. Dadurch wird eine Assembly mit dem Namen *AuthoringTagHelpers* erstellt:

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=3)]

Wenn Ihr Projekt ein `EmailTagHelper`-Taghilfsprogramm mit einem Standardnamespace (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`) verwendet, können Sie den vollqualifizierten Namen Ihres Taghilfsprogramms zur Verfügung stellen:

```cshtml
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```

Wenn Sie einer Ansicht über einen vollqualifizierten Namen ein Taghilfsprogramm hinzufügen möchten, müssen Sie zunächst diesen Namen (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`) und dann den Assemblynamen (*AuthoringTagHelpers*) hinzufügen. Die meisten Entwickler verwenden am liebsten die Platzhaltersyntax („\*“). Mithilfe der Platzhaltersyntax können Sie das Platzhalterzeichen „\*“ als Suffix in einem vollqualifizierten Namen einfügen. Beispielsweise können Sie über die folgenden Anweisungen das `EmailTagHelper`-Hilfsprogramm integrieren:

```cshtml
@addTagHelper AuthoringTagHelpers.TagHelpers.E*, AuthoringTagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.Email*, AuthoringTagHelpers
```

Wie obenstehend bereits erwähnt, ist das Taghilfsprogramm für alle Ansichtsdateien im *Views*-Verzeichnis bzw. -Unterverzeichnis verfügbar, wenn Sie die `@addTagHelper`-Anweisung der Datei *Views/_ViewImports.cshtml* hinzufügen. Sie können die `@addTagHelper`-Anweisung in bestimmten Ansichtsdateien verwenden, wenn Sie festlegen möchten, dass das Taghilfsprogramm nur für diese Ansichten verfügbar ist.

<a name="remove-razor-directives-label"></a>

### <a name="removetaghelper-removes-tag-helpers"></a>Entfernen von Taghilfsprogrammen über `@removeTagHelper`

Das `@removeTagHelper`-Taghilfsprogramm enthält dieselben beiden Parameter wie `@addTagHelper` und entfernt ein bereits zuvor hinzugefügtes Taghilfsprogramm. Wenn z.B. der `@removeTagHelper` auf eine bestimmte Ansicht angewendet wird, wird das angegebene Taghilfsprogramm aus der Ansicht entfernt. Wenn Sie das `@removeTagHelper`-Taghilfsprogramm in einem *Views/Folder/_ViewImports.cshtml*-Ordner verwenden, wird das festgelegte Taghilfsprogramm aus allen Ansichten im *Ordner* entfernt.

### <a name="controlling-tag-helper-scope-with-the-viewimportscshtml-file"></a>Steuern des Taghilfsprogrammbereichs mit der *_ViewImports.cshtml*-Datei

Sie können jedem Ordner eine *_ViewImports.cshtml*-Datei hinzufügen, und die Ansichtsengine wendet die Anweisungen aus dieser Datei und der *Views/_ViewImports.cshtml*-Datei an. Wenn Sie für die *Startseiten*-Ansicht eine leere *Views/Home/_ViewImports.cshtml*-Ansicht hinzufügen, ändert sich nichts, da die *_ViewImports.cshtml*-Datei nur einen Zusatz darstellt. Alle `@addTagHelper`-Anweisungen, die Sie der *Views/Home/_ViewImports.cshtml*-Datei hinzufügen (die nicht in der Standarddatei *Views/_ViewImports.cshtml* enthalten sind) machen diese Taghilfsprogramme nur für Ansichten im *Basis*-Ordner verfügbar.

<a name="opt-out"></a>

### <a name="opting-out-of-individual-elements"></a>Deaktivieren individueller Elemente

Sie können Taghilfsprogramme auf Elementebene über das Deaktivierungszeichen „!“ für Taghilfsprogramme deaktivieren. Beispielsweise wird die `Email`-Validierung in `<span>` über dieses Zeichen deaktiviert:

```cshtml
<!span asp-validation-for="Email" class="text-danger"></!span>
```

Sie müssen dieses Zeichen auf das Start- und das Endtag anwenden. (Der Visual Studio-Editor fügt das Zeichen automatisch dem Endtag hinzu, wenn Sie es im Starttag verwendet haben.) Sobald Sie das Deaktivierungszeichen hinzugefügt haben, werden das Element und die Taghilfsprogrammattribute nicht mehr in unterschiedlichen Schriftarten angezeigt.

<a name="prefix-razor-directives-label"></a>

### <a name="using-taghelperprefix-to-make-tag-helper-usage-explicit"></a>Verwenden von `@tagHelperPrefix`, um die Verwendung von Taghilfsprogrammen erforderlich zu machen

Mithilfe der `@tagHelperPrefix`-Anweisung können Sie ein Tagpräfix angeben, um Unterstützung für Taghilfsprogramme zu aktivieren und ihre Verwendung explizit erforderlich zu machen. Beispielsweise können Sie das folgende Markup zu der *Views/_ViewImports.cshtml*-Datei hinzufügen:

```cshtml
@tagHelperPrefix th:
```
Im nachfolgend Codebild ist das Präfix des Taghilfsprogramms auf `th:` festgelegt, sodass nur die Elemente, die das Präfix `th:` verwenden, Taghilfsprogramme unterstützen (Elemente, für die Taghilfsprogramme aktiviert sind, werden in einer anderen Schriftart dargestellt). Die Elemente `<label>` und `<input>` enthalten das Präfix des Taghilfsprogramms. Für sie sind Taghilfsprogramme aktiviert, für das Element `<span>` hingegen nicht.

![Bild](intro/_static/thp.png)

Für `@addTagHelper` gelten dieselben Hierarchieregeln wie für `@tagHelperPrefix`.

## <a name="self-closing-tag-helpers"></a>Taghilfsprogramme als selbstschließende Tags

Viele Taghilfsprogramme können nicht als selbstschließende Tags verwendet werden. Einige Taghilfsprogramme sind als selbstschließende Tags konzipiert. Wenn Sie ein Taghilfsprogramm verwenden, das nicht als selbstschließendes Tag konzipiert ist, wird die gerenderte Ausgabe unterdrückt. Wenn Sie ein als selbstschließendes Tag konzipiertes Taghilfsprogramm verwenden, werden selbstschließende Tags in der gerenderten Ausgabe verwendet. Weitere Informationen finden Sie unter [Erstellen von Taghilfsprogrammen in ASP.NET Core](xref:mvc/views/tag-helpers/authoring) in [diesem Hinweis](xref:mvc/views/tag-helpers/authoring#self-closing).

## <a name="intellisense-support-for-tag-helpers"></a>IntelliSense-Unterstützung für Taghilfsprogramme

Wenn Sie eine neue ASP.NET Core-Web-App in Visual Studio erstellen, wird das NuGet-Paket „Microsoft.AspNetCore.Razor.Tools“ hinzugefügt. Dabei handelt es sich um das Paket, das Taghilfsprogramme hinzufügt.

Sie sollten ein HTML-`<label>`-Element schreiben. Wenn Sie `<l` im Visual Studio-Editor eingeben, zeigt IntelliSense passende Elemente an:

![Bild](intro/_static/label.png)

Sie erhalten nicht nur Hilfe für HTML, sondern es wird auch das Symbol „@" symbol with "“ mit <> darunter angezeigt.

![Bild](intro/_static/tagSym.png)

Erkennt das Element als für Taghilfsprogramme konzipiert an. Für reine HTML-Elemente wie `fieldset` wird das Symbol „<>“ angezeigt.

Ein reines HTML-`<label>`-Tag zeigt das HTML-Tag (im Standardfarbdesign von Visual Studio) in braun, die Attribute in rot und die Attributwerte in blau an.

![Bild](intro/_static/LableHtmlTag.png)

Wenn Sie `<label` eingeben, listet IntelliSense die verfügbaren HTML/CSS-Attribute und die für Taghilfsprogramme konzipierten Attribute auf:

![Bild](intro/_static/labelattr.png)

Aufgrund der Anweisungsvervollständigung von IntelliSense können Sie die TAB-Taste drücken, um die Anweisung mit dem ausgewählten Wert zu vervollständigen:

![Bild](intro/_static/stmtcomplete.png)

Wenn ein Taghilfsprogrammattribut eingegeben wird, ändern sich die Schriftarten des Tags und des Attributs. Wenn Sie das Standardfarbdesign von Visual Studio verwenden („Blau“ oder „Hell“), wird die Schrift in dunkellila angezeigt. Wenn Sie das Design „Dunkel“ verwenden, wird die Schrift in einem dunklen blaugrün angezeigt. Für die in diesem Artikel dargestellten Bilder wurde das Standarddesign verwendet.

![Bild](intro/_static/labelaspfor2.png)

Sie können die Visual Studio-Verknüpfung *CompleteWord* verwenden ([standardmäßig](/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) STRG+LEERTASTE in doppelten Anführungszeichen (""), und jetzt befinden Sie sich genauso wie in einer C#-Klasse in C#). IntelliSense zeigt alle Methoden und Eigenschaften auf dem Seitenmodell an. Die Methoden und Eigenschaften sind verfügbar, weil der Eigenschaftentyp `ModelExpression` ist. Im nachfolgenden Beispiel wird die `Register`-Ansicht bearbeitet, damit das `RegisterViewModel` verfügbar ist.

![Bild](intro/_static/intellemail.png)

IntelliSense listet die Eigenschaften und Methoden auf, die für das Modell auf der Seite verfügbar sind. Mithilfe der umfassenden IntelliSense-Umgebung können Sie die CSS-Klasse auswählen:

![Bild](intro/_static/iclass.png)

![Bild](intro/_static/intel3.png)

## <a name="tag-helpers-compared-to-html-helpers"></a>Taghilfsprogramme und HTML-Hilfsprogramme im Vergleich

Taghilfsprogramme werden an HTML-Elemente in Razor-Ansichten angefügt. [HTML-Hilfsprogramme](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) werden hingegen als Methoden aufgerufen, die mit HTML in Razor-Ansichten vermischt werden. Sehen Sie dich das folgende Razor-Markup an, das eine HTML-Bezeichnung mit der CSS-Klasse „caption“ erstellt:

```cshtml
@Html.Label("FirstName", "First Name:", new {@class="caption"})
```

Das `@`-Symbol teilt Razor mit, dass es sich um den Beginn des Codes handelt. Bei den nächsten beiden Parametern („FirstName“ und „First Name:“) handelt es sich um Zeichenfolgen. Daher kann [IntelliSense](/visualstudio/ide/using-intellisense) nicht helfen. Das letzte Argument:

```cshtml
new {@class="caption"}
```

Dabei handelt es sich um ein anonymes Objekt, das verwendet wird, um Attribute darzustellen. Da es sich bei <strong>class</strong> um ein reserviertes Schlüsselwort in C# handelt, sollten Sie das `@`-Symbol verwenden, um C# zu zwingen, „@class=“ als Symbol (Eigenschaftenname) zu interpretieren. Front-End-Designern (also Entwickler, die mit HTML, CSS oder JavaScript und anderen Clients vertraut sind, sich aber nicht mit C# und Razor auskennen) ist diese Zeile wahrscheinlich nicht bekannt. Die gesamte Zeile muss ohne Hilfe von IntelliSense erstellt werden.

Wenn Sie das `LabelTagHelper`-Taghilfsprogramm verwenden, kann dasselbe Markup wie folgt geschrieben sein:

![Bild](intro/_static/label2.png)

Wenn Sie die Taghilfsprogrammversion verwenden und `<l` im Visual Studio-Editor eingeben, zeigt IntelliSense passende Elemente an:

![Bild](intro/_static/label.png)

Mithilfe von IntelliSense können Sie die gesamte Zeile schreiben. Das `LabelTagHelper`-Taghilfsprogramm legt standardmäßig den Inhalt des `asp-for`-Attributwerts („FirstName“) auf „First Name“ fest. Es konvertiert also Eigenschaften mit Binnenmajuskel in einen Satz, der aus dem Eigenschaftennamen besteht, und in den ein Leerzeichen vor jedem Binnenmajuskel eingefügt wird. Das folgende Markup

![Bild](intro/_static/label2.png)

generiert:

```cshtml
<label class="caption" for="FirstName">First Name</label>
```

Der konvertierte Inhalt wird nicht verwendet, wenn Sie Inhalt zu `<label>` hinzufügen. Zum Beispiel:

![Bild](intro/_static/1stName.png)

generiert:

```cshtml
<label class="caption" for="FirstName">Name First</label>
```

Im folgenden Bild wird der Formularanteil der *Views/Account/Register.cshtml*-Razor-Ansicht angezeigt, der über die veraltete ASP.NET Core 4.5.x MVC-Vorlage generiert wird, die im Lieferumfang von Visual Studio 2015 enthalten ist.

![Bild](intro/_static/regCS.png)

Der Visual Studio-Editor zeigt C#-Code vor grauem Hintergrund an. Z.B. wird das `AntiForgeryToken`-HTML-Hilfsprogramm

```cshtml
@Html.AntiForgeryToken()
```

vor grauem Hintergrund angezeigt. Ein Großteil des Markups in der Registeransicht ist in C# geschrieben. Zum Vergleich wird in der folgenden Abbildung der entsprechende Ansatz unter Verwendung von Taghilfsprogrammen dargestellt:

![Bild](intro/_static/regTH.png)

Das Markup ist viel deutlicher und kann einfacher gelesen, bearbeitet und verwaltet werden als im Ansatz über das HTML-Hilfsprogramm. Der C#-Code ist auf die mindestens erforderlichen Informationen begrenzt, die der Server benötigt. Der Visual Studio-Editor zeigt Markup an, das von einem Taghilfsprogramm in einer anderen Schriftart angezeigt wird.

Sehen Sie sich die *Email*-Gruppe an:

[!code-csharp[](intro/sample/Register.cshtml?range=12-18)]

Alle asp-Attribute enthalten den Wert „Email“. „Email“ ist allerdings keine Zeichenfolge. In diesem Kontext ist „Email“ die C#-Modellausdruckseigenschaft für das `RegisterViewModel`.

Mithilfe des Visual Studio-Editors können Sie das **gesamte** Markup im Taghilfsprogrammansatz des Registerformulars schreiben. Visual Studio stellt hingegen für einen Großteil des Codes im HTML-Hilfsprogrammansatz keine Hilfe zur Verfügung. Im Abschnitt [IntelliSense-Unterstützung für Tag-Hilfsprogramme](#intellisense-support-for-tag-helpers) finden Sie mehr Details zum Arbeiten mit Taghilfsprogrammen im Visual Studio-Editor.

## <a name="tag-helpers-compared-to-web-server-controls"></a>Taghilfsprogramm zu Webserversteuerelementen im Vergleich

* Taghilfsprogramme besitzen das Element nicht, dem sie zugeordnet sind. Stattdessen sind sie nur Teil des Rendervorgangs des Elements und des Inhalts. [Webserversteuerelemente](https://msdn.microsoft.com/library/7698y1f0.aspx) für ASP.NET werden auf einer Seite deklariert und aufgerufen.

* [Webserversteuerelemente](https://msdn.microsoft.com/library/zsyt68f1.aspx) haben einen nicht trivialen Lebenszyklus, aufgrund dessen sich das Entwickeln und Debuggen als schwierig gestalten kann.

* Mithilfe von Webserversteuerelementen können Sie Funktionen zu den Dokumentobjektmodellelementen des Clients über Clientsteuerelemente hinzufügen. Taghilfsprogramme verfügen nicht über Dokumentobjektmodelle.

* Webserversteuerelemente umfassen die Browsererkennung nicht. Taghilfsprogramme haben keine Kenntnisse über den Browser.

* Mehrere Taghilfsprogramme können gleichzeitig auf dasselbe Element wirken (weitere Informationen finden Sie unter [Avoiding Tag Helper conflicts (Vermeiden von Konflikten mit Taghilfsprogrammen)](xref:mvc/views/tag-helpers/authoring#avoid-tag-helper-conflicts)). Sie können hingegen in der Regel keine Webserversteuerelemente erstellen.

* Taghilfsprogramme können das Tag und den Inhalt von HTML-Elementen verändern, dem sie zugeordnet sind. Ansonsten nehmen Sie keine Änderungen an der Seite vor. Der Funktionsbereich von Webserversteuerelementen ist weniger spezifisch. Sie können Aktionen ausführen, die andere Teile Ihrer Seite beeinflussen, wodurch Nebenwirkungen entstehen, die nicht vorgesehen sind.

* Webserversteuerelemente verwenden Typkonverter, um Zeichenfolgen in Objekte zu konvertieren. Mit Taghilfsprogrammen arbeiten Sie auf native Weise in C#, weshalb Sie keine Typkonvertierung durchführen müssen.

* Webserversteuerelemente verwenden [System.ComponentModel](/dotnet/api/system.componentmodel), um das Verhalten von Komponenten und Steuerelementen zur Laufzeit und Entwurfszeit zu implementieren. `System.ComponentModel` enthält die Basisklassen und Schnittstellen zum Implementieren von Attributen und Typkonvertern, die Datenquellen binden und Komponenten lizenzieren. Im Gegensatz dazu stehen Taghilfsprogramme, die in der Regel von `TagHelper` abgeleitet sind. Die `TagHelper`-Basisklasse stellt nur zwei Methoden zur Verfügung: `Process` und `ProcessAsync`.

## <a name="customizing-the-tag-helper-element-font"></a>Anpassen der Elementschriftart des Taghilfsprogramms

Sie können die Schriftart und die Farben über **Extras** > **Optionen** > **Umgebung** > **Schriftarten und Farben** anpassen:

![Bild](intro/_static/fontoptions2.png)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Erstellen von Taghilfsprogrammen](xref:mvc/views/tag-helpers/authoring)
* [Arbeiten mit Formularen](xref:mvc/views/working-with-forms)
* Auf der Seite [Beispiele für Taghilfsprogramme unter GitHub](https://github.com/dpaquette/TagHelperSamples) finden Sie Beispiele für Taghilfsprogramme, die Sie für die Arbeit mit [Bootstrap](http://getbootstrap.com/) verwenden können.
