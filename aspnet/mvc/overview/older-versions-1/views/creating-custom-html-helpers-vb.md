---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (VB) | Microsoft-Dokumentation
author: microsoft
description: Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch die Nutzung von HTML-Hilfsobjekt...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: e62e47bceddc516af7aa18fc66ed4ca4d704d277
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034947"
---
<a name="creating-custom-html-helpers-vb"></a>Erstellen von benutzerdefinierten HTML-Hilfsprogrammen (VB)
====================
by [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch Nutzen der HTML-Hilfsprogramme, können Sie die Menge der lästige Eingabe von HTML-Tags, die Sie ausführen müssen, um eine standard-HTML-Seite zu erstellen, reduzieren.


Das Ziel in diesem Tutorial wird veranschaulicht, wie Sie benutzerdefinierte HTML-Hilfsprogramme erstellen können, die Sie in Ihren MVC-Ansichten verwenden können. Durch Nutzen der HTML-Hilfsprogramme, können Sie die Menge der lästige Eingabe von HTML-Tags, die Sie ausführen müssen, um eine standard-HTML-Seite zu erstellen, reduzieren.

Im ersten Teil dieses Lernprogramms beschreibe ich einige der vorhandenen HTML-Hilfsprogramme in ASP.NET MVC-Framework enthalten. Als Nächstes beschreibe ich zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme: Ich erläutern, wie zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme durch Erstellen einer freigegebenen Methode und eine Erweiterungsmethode erstellen.

## <a name="understanding-html-helpers"></a>Grundlegendes zu HTML-Hilfsprogramme

Ein HTML-Hilfsprogramm ist nur eine Methode, die eine Zeichenfolge zurückgibt. Die Zeichenfolge kann jede Art von Inhalt darstellen, die Sie möchten. Beispielsweise können Sie HTML-Hilfsmethoden zum Rendern von HTML-standard HTML-Tags `<input>` und `<img>` Tags. Sie können auch HTML-Hilfsmethoden zum Rendern komplexeren Inhalts wie z. B. eine Registerkartenleiste oder eine HTML-Tabelle von Datenbankdaten verwenden.

ASP.NET MVC-Framework enthält den folgenden Satz von standardmäßigen HTML-Hilfsprogramme (Dies ist keine vollständige Liste):

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

Betrachten Sie beispielsweise das Formular in Codebeispiel 1. Dieses Formular wird mit der Hilfe von zwei der standardmäßigen HTML-Hilfsprogramme gerendert (siehe Abbildung 1). Dieses Formular verwendet die `Html.BeginForm()` und `Html.TextBox()` Helper-Methoden.


[![Rendern der Seite mit HTML-Hilfsprogramme](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**Abbildung 01**: Rendern der Seite mit HTML-Hilfsprogramme ([klicken Sie, um das Bild in voller Größe anzeigen](creating-custom-html-helpers-vb/_static/image3.png))


**Codebeispiel 1: `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

Die `Html.BeginForm()` Hilfsmethode wird verwendet, um das öffnende und schließende HTML erstellen `<form>` Tags. Beachten Sie, dass die `Html.BeginForm()` Methode wird aufgerufen, in einem using Anweisung. Die using-Anweisung wird sichergestellt, dass die `<form>` Tags geschlossen wird, am Ende der Verwendung von Block.

Falls gewünscht, statt zum Erstellen eines neuen, blockieren, können Sie die Html.EndForm() Helper-Methode zum Schließen Aufrufen der `<form>` Tag. Verwenden der Ansatz, erstellen eine öffnende und schließende `<form>` Tag, der Ihnen intuitivste erscheint.

Die `Html.TextBox()` Helper-Methoden werden zum Rendern von HTML in Codebeispiel 1 verwendet `<input>` Tags. Bei Auswahl von Quelltext anzeigen in Ihrem Browser sehen Sie die HTML-Quelle im Codebeispiel 2. Beachten Sie, dass die Quelle die standard-HTML-Tags enthält.

> [!IMPORTANT]
> Beachten Sie, dass die `Html.TextBox()`- HTML-Hilfsprogramm wird mit gerendert `<%= %>` anstelle von tags `<% %>` Tags. Wenn Sie nicht das Gleichheitszeichen enthalten, wird Klicken Sie dann "nothing" an den Browser gerendert.

ASP.NET MVC-Framework enthält eine kleine Gruppe von Hilfsprogrammen. In den meisten Fällen müssen Sie das MVC-Framework für benutzerdefinierte HTML-Hilfsprogramme zu erweitern. In den Rest dieses Tutorials erfahren Sie, zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme.

**Codebeispiel 2: `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>Erstellen von HTML-Hilfsprogramme mit freigegebenen Methoden

Die einfachste Möglichkeit zum Erstellen einer neuen HTML-Hilfe ist auf eine freigegebene Methode zu erstellen, die eine Zeichenfolge zurückgibt. Angenommen, Sie können eine neue HTML-Hilfsobjekt zu erstellen, die eine HTML rendert `<label>` Tag. Sie können mithilfe die Klasse in Liste 2 Rendern einer `<label>`.

**Codebeispiel 2: `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

Es gibt keine besonderen, über die Klasse im Codebeispiel 2. Die `Label()` Methode gibt einfach eine Zeichenfolge zurück.

Geänderte Ansicht "Index" in Programmausdruck 3 verwendet die `LabelHelper` zum Rendern von HTML `<label>` Tags. Beachten Sie, die die Ansicht enthält eine `<%@ imports %>` -Direktive, die den Application1.Helpers-Namespace importiert.

**Codebeispiel 2: `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Erstellen von HTML-Hilfsprogrammen mit Erweiterungsmethoden

Wenn Sie erstellen möchten wie HTML-Hilfsprogramme, der einfach funktioniert der standardmäßigen HTML-Hilfsprogramme, die in ASP.NET MVC-Framework enthalten, müssen Sie Erweiterungsmethoden erstellen. Erweiterungsmethoden ermöglichen Ihnen, neue Methoden zu einer vorhandenen Klasse hinzufügen. Wenn Sie eine HTML-Hilfsmethode erstellen, Sie neue Methoden zum Hinzufügen der `HtmlHelper` Klasse, die eine Ansicht des HTML-Eigenschaft dargestellt.

Visual Basic-Moduls in Programmausdruck 3 fügt eine Erweiterungsmethode namens `Label()` auf die `HtmlHelper` Klasse. Es gibt einige Dinge, die Sie zu diesem Modul sehen. Erstens ist zu beachten, dass das Modul mit versehen ist die `<Extension()>` Attribut. Um dieses Attribut verwenden, müssen Sie importieren die `System.Runtime.CompilerServices` Namespace

Zweitens: Beachten Sie, dass der erste Parameter der `Label()` Methode stellt der `HtmlHelper` Klasse. Der erste Parameter einer extensionmethode gibt an, die Klasse, die die Erweiterungsmethode erweitert wird.

**Codebeispiel 3: `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

Nachdem Sie eine Erweiterungsmethode erstellen, und erstellen Sie Ihre Anwendung erfolgreich, wird die Erweiterungsmethode in Visual Studio Intellisense wie alle anderen Methoden einer Klasse (siehe Abbildung 2). Der einzige Unterschied ist diese Erweiterung, die Methoden mit einem speziellen Symbol neben dem Namen (ein Symbol nach unten weisenden Pfeil) angezeigt werden.


[![Mithilfe der Erweiterungsmethode Html.Label()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**Abbildung 02**: Mithilfe der Erweiterungsmethode Html.Label() ([klicken Sie, um das Bild in voller Größe anzeigen](creating-custom-html-helpers-vb/_static/image6.png))


Geänderte Ansicht "Index" in Listing 4 verwendet die Html.Label()-Erweiterungsmethode, um alle Rendern die &lt;Bezeichnung&gt; Tags.

**Codebeispiel 4: `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie zwei Methoden zum Erstellen von benutzerdefinierten HTML-Hilfsprogramme. Zunächst haben Sie gelernt, erstellen Sie eine benutzerdefinierte `Label()` HTML-Hilfsobjekt, indem Sie eine freigegebene Methode erstellen, gibt eine Zeichenfolge zurück. Anschließend haben Sie gelernt, erstellen Sie eine benutzerdefinierte `Label()` HTML-Hilfsobjekt-Methode, indem Sie eine Erweiterungsmethode erstellen, auf die `HtmlHelper` Klasse.

Ich Schwerpunkt in diesem Tutorial erstellen eine sehr einfache HTML-Hilfsmethode. Beachten Sie, dass ein HTML-Hilfsprogramm kann so kompliziert, wie Sie möchten. Sie können HTML-Hilfsprogramme erstellen, die umfangreiche Inhalte, z. B. Strukturansichten, Menüs oder Tabellen der Datenbankdaten rendern.

> [!div class="step-by-step"]
> [Zurück](asp-net-mvc-views-overview-vb.md)
> [Weiter](using-the-tagbuilder-class-to-build-html-helpers-vb.md)