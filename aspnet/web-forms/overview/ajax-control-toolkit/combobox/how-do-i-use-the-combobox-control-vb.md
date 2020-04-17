---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: Wie verwende ich das ComboBox Control? (VB) | Microsoft Docs
author: rick-anderson
description: ComboBox ist ein ASP.NET AJAX-Steuerelement, das die Flexibilität einer TextBox mit einer Liste von Optionen kombiniert, aus denen Benutzer auswählen können.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 237e3ef864238c11fc1fb49239c3f6fa3f75537d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543066"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a>Wie verwende ich das ComboBox Control? (VB)

von [Microsoft](https://github.com/microsoft)

> ComboBox ist ein ASP.NET AJAX-Steuerelement, das die Flexibilität einer TextBox mit einer Liste von Optionen kombiniert, aus denen Benutzer auswählen können.

Das Ziel dieses Tutorials ist es, das AJAX Control Toolkit ComboBox-Steuerelement zu erklären. Die ComboBox funktioniert wie eine Kombination aus einem Standard-ASP.NET DropDownList-Steuerelement und einem TextBox-Steuerelement. Sie können entweder aus einer bereits vorhandenen Liste von Artikeln auswählen oder einen neuen Artikel eingeben.

Die ComboBox ähnelt dem AutoComplete-Steuerelement-Extender, aber die Steuerelemente werden in verschiedenen Szenarien verwendet. Der AutoVervollständigen-Extender fragt einen Webdienst ab, um übereinstimmende Einträge abzurufen. Das ComboBox-Steuerelement hingegen wird mit einer Reihe von Elementen initialisiert. Die Verwendung des AutoComplete-Extenders ist sinnvoll, wenn Sie mit einem großen Satz von Daten (Millionen von Autoteilen) arbeiten, während die Verwendung der ComboBox-Steuerung sinnvoll ist, wenn Sie mit einem kleinen Satz von Daten (Dutzende von Autoteilen) arbeiten.

## <a name="selecting-from-a-static-list-of-items"></a>Auswählen aus einer statischen Liste von Elementen

Beginnen wir mit einem einfachen Beispiel für die Verwendung des ComboBox-Steuerelements. Stellen Sie sich vor, Sie möchten eine statische Liste von Elementen in einer Dropdownliste anzeigen. Sie möchten jedoch offen lassen, dass die Liste nicht vollständig ist. Sie möchten einem Benutzer erlauben, einen benutzerdefinierten Wert in die Liste einzugeben.

Wir erstellen eine neue ASP.NET Web Forms-Seite und verwenden das ComboBox-Steuerelement auf der Seite. Fügen Sie das neue ASP.NET Seite zu Ihrem Projekt hinzu, und wechseln Sie zur Entwurfsansicht.

Wenn Sie das ComboBox-Steuerelement auf der Seite verwenden möchten, müssen Sie der Seite ein ScriptManager-Steuerelement hinzufügen. Ziehen Sie das ScriptManager-Steuerelement unter der Registerkarte AJAX-Erweiterungen auf die Designer-Oberfläche. Sie sollten das ScriptManager-Steuerelement oben auf der Seite hinzufügen. Sie können es direkt unter dem &lt;&gt; öffnenden serverseitigen Formulartag hinzufügen.

Ziehen Sie als Nächstes das ComboBox-Steuerelement auf die Seite. Sie finden das ComboBox-Steuerelement in der Toolbox mit den anderen AJAX Control Toolkit-Steuerelementen und Control Extendern (siehe Abbildung1).

[![Einfaches Formular zum Erstellen einer Visitenkarte](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

**Abbildung 01**: Auswählen des ComboBox-Steuerelements aus der Toolbox ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image2.png))

Wir verwenden das ComboBox-Steuerelement, um eine statische Liste von Auswahlmöglichkeiten anzuzeigen. Der Benutzer kann aus einer Liste von drei Optionen eine bestimmte Würzefürebene für seine Lebensmittel auswählen: Mild, Medium und Hot (siehe Abbildung 2).

[![Auswählen aus einer statischen Liste von Elementen](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

**Abbildung 02**: Auswählen aus einer statischen Liste von Elementen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image4.png))

Es gibt zwei Möglichkeiten, diese Optionen zum ComboBox-Steuerelement hinzuzufügen. Zuerst wählen Sie die Taskoption Optionen bearbeiten aus, wenn Sie mit der Maus über das Steuerelement in der Entwurfsansicht bewegen, und öffnen Sie den Element-Editor (siehe Abbildung 3).

[![Bearbeiten von ComboBox-Elementen](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

**Abbildung 03**: Bearbeiten von ComboBox-Elementen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image6.png))

Die zweite Option besteht darin, die Liste der &lt;Elemente zwischen&gt; dem öffnenden und schließenden asp:ComboBox-Tag in der Quellansicht hinzuzufügen. Die Seite in Liste 1 enthält die aktualisierte ComboBox mit der Liste der Elemente.

**Auflistung 1 - Static.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

Wenn Sie die Seite in Liste 1 öffnen, können Sie eine der bereits vorhandenen Optionen aus der ComboBox auswählen. Mit anderen Worten, die ComboBox funktioniert wie ein DropDownList-Steuerelement.

Sie haben jedoch auch die Möglichkeit, eine neue Auswahl (z. B. Super Spicy) einzugeben, die nicht in der vorhandenen Liste enthalten ist. Die ComboBox funktioniert also auch wie ein TextBox-Steuerelement.

Unabhängig davon, ob Sie ein bereits vorhandenes Element auswählen oder ein benutzerdefiniertes Element eingeben, wird beim Absenden des Formulars Ihre Auswahl im Beschriftungssteuerelement angezeigt. Wenn Sie das Formular absenden, führt der btnSubmit\_Click-Handler die Bezeichnung aus und aktualisiert sie (siehe Abbildung 4).

[![Anzeigen des ausgewählten Elements](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

**Abbildung 04**: Anzeigen des ausgewählten Elements([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](how-do-i-use-the-combobox-control-vb/_static/image8.png)

Die ComboBox unterstützt dieselben Eigenschaften wie das DropDownList-Steuerelement zum Abrufen des ausgewählten Elements nach dem Absenden eines Formulars:

- SelectedItem.Text - Zeigt den Wert der Text-Eigenschaft des ausgewählten Elements an.
- SelectedItem.Value - Zeigt den Wert der Value-Eigenschaft des ausgewählten Elements oder den in die ComboBox eingegebenen Text an.
- SelectedValue - Gleich mit SelectedItem.Value, mit der Ausnahme, dass Sie mit dieser Eigenschaft das standardmäßige (anfangs) ausgewählte Element angeben können.

Wenn Sie eine benutzerdefinierte Auswahl in die ComboBox eingeben, wird die benutzerdefinierte Auswahl sowohl den Eigenschaften SelectedItem.Text als auch SelectedItem.Value zugewiesen.

## <a name="selecting-the-list-of-items-from-the-database"></a>Auswählen der Liste der Elemente aus der Datenbank

Sie können die Liste der Elemente abrufen, die von ComboBox aus einer Datenbank angezeigt werden. Sie können die ComboBox beispielsweise an ein SqlDataSource-Steuerelement, ein ObjectDataSource-Steuerelement, eine LinqDataSource oder eine EntityDataSource binden.

Stellen Sie sich vor, Sie möchten eine Liste von Filmen in einer ComboBox anzeigen. Sie möchten die Liste der Filme aus der Tabelle Filme-Datenbank abrufen. Folgen Sie diesen Schritten:

1. Erstellen einer Seite mit dem Namen Movies.aspx
2. Fügen Sie der Seite ein ScriptManager-Steuerelement hinzu, indem Sie den ScriptManager unter der Registerkarte AJAX-Erweiterungen in der Toolbox auf die Seite ziehen.
3. Fügen Sie der Seite ein ComboBox-Steuerelement hinzu, indem Sie die ComboBox auf die Seite ziehen.
4. Bewegen Sie in der Entwurfsansicht mit der Maus über das ComboBox-Steuerelement, und wählen Sie die Option **Datenquelle auswählen** aus (siehe Abbildung 5). Der Datenquellenkonfigurations-Assistent wird gestartet.
5. Wählen Sie im Schritt **Datenquelle** &lt;auswählen die&gt; Option Neue Datenquelle aus.
6. Wählen Sie im Schritt **Datenquellentyp auswählen** die Option Datenbank aus.
7. Wählen Sie im Schritt **Datenverbindung auswählen** Ihre Datenbank aus (z. B. MoviesDB.mdf).
8. Wählen Sie im Schritt **Verbindungszeichenfolge in der Anwendungskonfigurationsdatei** speichern die Option zum Speichern der Verbindungszeichenfolge aus.
9. Wählen Sie im Schritt **"Anweisung auswählen"** die Tabelle "Filme" und alle Spalten aus.
10. Klicken Sie im Schritt **Testabfrage** auf die Schaltfläche Fertig stellen.
11. Wählen Sie im Schritt **Datenquelle auswählen** die Spalte Titel für das anzuzeigende Feld und die Id-Spalte für das Datenfeld aus (siehe Abbildung).
12. Klicken Sie auf die Schaltfläche OK, um den Assistenten zu schließen.

[![Auswählen einer Datenquelle](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

**Abbildung 05**: Auswählen einer Datenquelle ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image10.png))

[![Auswählen der Datentext- und Wertfelder](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

**Abbildung 06**: Auswählen der Datentext- und Wertfelder ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image12.png))

Nachdem Sie die oben genannten Schritte ausgeführt haben, ist die ComboBox an ein SqlDataSource-Steuerelement gebunden, das die Filme aus der Tabelle Filme-Datenbank darstellt. Die Quelle für die Seite sieht aus wie Listing 2 (Ich habe die Formatierung ein wenig bereinigt).

**Auflisten 2 - Movies.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

Beachten Sie, dass das ComboBox-Steuerelement über eine DataSourceID-Eigenschaft verfügt, die auf das SqlDataSource-Steuerelement verweist. Wenn Sie die Seite in einem Browser öffnen, wird die Liste der Filme aus der Datenbank angezeigt (siehe Abbildung 7). Sie können entweder einen Film aus der Liste auswählen oder einen neuen Film eingeben, indem Sie den Film in die ComboBox eingeben.

[![Anzeigen einer Liste von Filmen](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

**Abbildung 07**: Anzeigen einer Liste von Filmen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>Festlegen des DropDownStyle

Sie können die ComboBox DropDownStyle-Eigenschaft verwenden, um das Verhalten der ComboBox zu ändern. Diese Eigenschaft akzeptiert dort mögliche Werte:

- DropDown - (Standardwert) Die ComboBox zeigt eine Dropdownliste an, wenn Sie auf den Pfeil klicken und Sie einen benutzerdefinierten Wert eingeben können.
- Einfach - Die ComboBox zeigt automatisch eine Dropdown-Liste an und Sie können einen benutzerdefinierten Wert eingeben.
- DropDownList - Die ComboBox funktioniert wie ein DropDownList-Steuerelement.

Der Unterschied zwischen DropDown und Simple ist, wenn die Liste der Elemente angezeigt wird. Im Fall von Einfach wird die Liste sofort angezeigt, wenn Sie den Fokus auf die ComboBox verschieben. Im Fall von DropDown müssen Sie auf den Pfeil klicken, um die Liste der Elemente anzuzeigen.

Der DropDownList-Wert bewirkt, dass das ComboBox-Steuerelement wie ein Standard-DropDownList-Steuerelement funktioniert. Hier gibt es jedoch einen wichtigen Unterschied. Ältere Versionen von Internet Explorer zeigen ein DropDownList-Steuerelement mit einem unendlichen Z-Index an, sodass das Steuerelement vor jedem Vor-Steuerelement angezeigt wird. Da die ComboBox ein &lt;&gt; HTML-div-Tag &lt;&gt; anstelle eines HTML-Auswahl-Tags rendert, respektiert die ComboBox die Z-Reihenfolge korrekt.

## <a name="setting-the-autocompletemode"></a>Festlegen des AutoCompleteMode

Sie verwenden die ComboBox AutoCompleteMode-Eigenschaft, um anzugeben, was geschieht, wenn jemand Text in die ComboBox eingibt. Diese Eigenschaft akzeptiert die folgenden möglichen Werte:

- Keine - (Standardwert) Die ComboBox bietet kein Verhalten zur automatischen Vervollständigung.
- Vorschlagen - Die ComboBox zeigt die Liste an und hebt das entsprechende Element in der Liste hervor (siehe Abbildung 8).
- Anfügen - Die ComboBox zeigt die Liste nicht an und fügt das entsprechende Element aus der Liste an das an, was Sie eingegeben haben (siehe Abbildung 9).
- SuggestAppend - Die ComboBox zeigt sowohl die Liste als auch das entsprechende Element aus der Liste an das an, was Sie eingegeben haben (siehe Abbildung 10).

[![Die ComboBox macht einen Vorschlag](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

**Abbildung 08**: Die ComboBox macht einen Vorschlag([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](how-do-i-use-the-combobox-control-vb/_static/image16.png)

[![ComboBox fügt übereinstimmenden Text an](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

**Abbildung 09**: ComboBox fügt passenden Text an[(Klicken Sie hier, um ein Bild in voller Größe anzuzeigen)](how-do-i-use-the-combobox-control-vb/_static/image18.png)

[![Die ComboBox schlägt vor und fügt](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

**Abbildung 10**: Die ComboBox schlägt vor und hängt an ([Klicken Sie hier, um ein Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-vb/_static/image20.png))

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie gelernt, wie Sie das ComboBox-Steuerelement verwenden, um einen festen Satz von Elementen anzuzeigen. Wir haben das ComboBox-Steuerelement sowohl an einen statischen Satz von Elementen als auch an eine Datenbanktabelle gebunden. Schließlich haben Sie gelernt, wie Sie das Verhalten der ComboBox ändern, indem Sie die Eigenschaften DropDownStyle und AutoCompleteMode festlegen.

> [!div class="step-by-step"]
> [Vorherige](how-do-i-use-the-combobox-control-cs.md)
