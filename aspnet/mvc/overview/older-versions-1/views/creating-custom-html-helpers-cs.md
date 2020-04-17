---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Erstellen benutzerdefinierter HTML-Hilfsprogramme | Microsoft Docs
author: rick-anderson
description: Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML Helper...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542559"
---
# <a name="creating-custom-html-helpers-c"></a>Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (C#)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML-Hilfsprogrammen können Sie die Menge der mühsamen Eingabe von HTML-Tags reduzieren, die Sie ausführen müssen, um eine Standard-HTML-Seite zu erstellen.

Das Ziel dieses Tutorials besteht darin, zu veranschaulichen, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML-Hilfsprogrammen können Sie die Menge der mühsamen Eingabe von HTML-Tags reduzieren, die Sie ausführen müssen, um eine Standard-HTML-Seite zu erstellen.

Im ersten Teil dieses Tutorials beschreibe ich einige der vorhandenen HTML-Hilfsprogramme, die im ASP.NET MVC-Framework enthalten sind. Als Nächstes beschreibe ich zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogrammen: Ich erkläre, wie benutzerdefinierte HTML-Hilfsprogramme erstellt werden, indem eine statische Methode erstellt und eine Erweiterungsmethode erstellt wird.

## <a name="understanding-html-helpers"></a>Html-Hilfen verstehen

Ein HTML-Hilfsmann ist nur eine Methode, die eine Zeichenfolge zurückgibt. Die Zeichenfolge kann jede beliebige Art von Inhalt darstellen. Sie können beispielsweise HTML-Hilfsprogramme verwenden, um `<input>` `<img>` Standard-HTML-Tags wie HTML und Tags zu rendern. Sie können auch HTML-Hilfsprogramme verwenden, um komplexere Inhalte wie einen Tab-Strip oder eine HTML-Tabelle mit Datenbankdaten zu rendern.

Das ASP.NET MVC-Framework enthält den folgenden Satz von Standard-HTML-Helfern (dies ist keine vollständige Liste):

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

Betrachten Sie beispielsweise das Formular in Liste 1. Dieses Formular wird mit Hilfe von zwei der Standard-HTML-Helfer gerendert (siehe Abbildung 1). Dieses Formular `Html.BeginForm()` verwendet `Html.TextBox()` die und Helper-Methoden, um ein einfaches HTML-Formular zu rendern.

[![Mit HTML-Helfern gerenderte Seite](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Abbildung 01**: Seite gerendert mit HTML-Hilfsprogrammen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-html-helpers-cs/_static/image3.png))

**Auflistung 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Die Html.BeginForm() Helper-Methode wird verwendet, `<form>` um das Öffnen und Schließen von HTML-Tags zu erstellen. Beachten Sie, dass die `Html.BeginForm()` Methode innerhalb einer using-Anweisung aufgerufen wird. Die using-Anweisung `<form>` stellt sicher, dass das Tag am Ende des using-Blocks geschlossen wird.

Wenn Sie möchten, können Sie anstelle des Erstellens eines Using-Blocks die Html.EndForm()-Hilfsmethode aufrufen, um das `<form>` Tag zu schließen. Verwenden Sie den Ansatz, um `<form>` ein öffnendes und schließendes Tag zu erstellen, das Ihnen am intuitivsten erscheint.

Die `Html.TextBox()` Hilfsmethoden werden in Liste 1 `<input>` zum Rendern von HTML-Tags verwendet. Wenn Sie die Quellquelle in Ihrem Browser auswählen, wird die HTML-Quelle in Liste 2 angezeigt. Beachten Sie, dass die Quelle Standard-HTML-Tags enthält.

> [!IMPORTANT]
> Beachten Sie, dass der `Html.TextBox()`-HTML-Helfer mit `<%= %>` Tags anstelle von `<% %>` Tags gerendert wird. Wenn Sie das Gleichheitszeichen nicht einschließen, wird nichts im Browser gerendert.

Das ASP.NET MVC-Framework enthält eine kleine Gruppe von Helfern. Wahrscheinlich müssen Sie das MVC-Framework um benutzerdefinierte HTML-Hilfsprogramme erweitern. Im WeiterenVerlauf dieses Tutorials lernen Sie zwei Methoden zum Erstellen benutzerdefinierter HTML-Hilfsprogramme.

**Auflistung 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Erstellen von HTML-Hilfsprogrammen mit statischen Methoden

Die einfachste Möglichkeit zum Erstellen eines neuen HTML-Hilfselements besteht darin, eine statische Methode zu erstellen, die eine Zeichenfolge zurückgibt. Stellen Sie sich beispielsweise vor, dass Sie einen neuen HTML-Helfer erstellen, der ein HTML-Tag `<label>` rendert. Sie können die Klasse in Liste `<label>` 2 verwenden, um eine zu rendern.

**Auflistung 2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

Es gibt nichts Besonderes an der Klasse in Listing 2. Die `Label()` Methode gibt einfach eine Zeichenfolge zurück.

Die geänderte Indexansicht in `LabelHelper` Liste `<label>` 3 verwendet die zum Rendern von HTML-Tags. Beachten Sie, dass `<%@ imports %>` die Ansicht `Application1.Helpers` eine Direktive enthält, die den Namespace importiert.

**Auflistung 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Erstellen von HTML-Hilfsprogrammen mit Erweiterungsmethoden

Wenn Sie HTML-Hilfsprogramme erstellen möchten, die genau wie die Standard-HTML-Hilfsprogramme funktionieren, die im ASP.NET MVC-Framework enthalten sind, müssen Sie Erweiterungsmethoden erstellen. Mithilfe von Erweiterungsmethoden können Sie einer vorhandenen Klasse neue Methoden hinzufügen. Beim Erstellen einer HTML-Hilfsmethode fügen Sie der HtmlHelper-Klasse, die durch die Html-Eigenschaft einer Ansicht dargestellt wird, neue Methoden hinzu.

Die Klasse in Listing 3 fügt `HtmlHelper` der `Label()`Klasse mit dem Namen eine Erweiterungsmethode hinzu. Es gibt ein paar Dinge, die Sie über diese Klasse bemerken sollten. Beachten Sie zunächst, dass es sich bei der Klasse um eine statische Klasse handelt. Sie müssen eine Erweiterungsmethode mit einer statischen Klasse definieren.

Beachten Sie zweitens, dass `Label()` dem ersten Parameter `this`der Methode das Schlüsselwort vorangestellt wird. Der erste Parameter einer Erweiterungsmethode gibt die Klasse an, die die Erweiterungsmethode erweitert.

**Auflistung 3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Nachdem Sie eine Erweiterungsmethode erstellt und die Anwendung erfolgreich erstellt haben, wird die Erweiterungsmethode in Visual Studio Intellisense wie alle anderen Methoden einer Klasse angezeigt (siehe Abbildung 2). Der einzige Unterschied besteht darin, dass Erweiterungsmethoden mit einem speziellen Symbol neben ihnen angezeigt werden (ein Symbol eines Abwärtspfeils).

[![Verwenden der Html.Label()-Erweiterungsmethode](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Abbildung 02**: Verwenden der Html.Label()-Erweiterungsmethode ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-custom-html-helpers-cs/_static/image6.png))

Die geänderte Indexansicht in Listing 4 verwendet die Html.Label()-Erweiterungsmethode, um alle tags `<label>` zu rendern.

**Auflistung 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie zwei Methoden zum Erstellen benutzerdefinierter HTML-Hilfsprogramme gelernt. Zuerst haben Sie gelernt, `Label()` wie Sie einen benutzerdefinierten HTML-Hilfsmittel erstellen, indem Sie eine statische Methode erstellen, die eine Zeichenfolge zurückgibt. Als Nächstes haben Sie gelernt, wie Sie eine benutzerdefinierte `Label()` `HtmlHelper` HTML-Hilfsmethode erstellen, indem Sie eine Erweiterungsmethode für die Klasse erstellen.

In diesem Tutorial habe ich mich auf den Aufbau einer extrem einfachen HTML-Hilfsmethode konzentriert. Beachten Sie, dass ein HTML-Helfer so kompliziert sein kann, wie Sie möchten. Sie können HTML-Hilfsprogramme erstellen, die umfangreiche Inhalte wie Baumansichten, Menüs oder Tabellen mit Datenbankdaten rendern.

> [!div class="step-by-step"]
> [Zurück](asp-net-mvc-views-overview-cs.md)
> [Weiter](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
