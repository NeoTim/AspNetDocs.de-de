---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: Gewusst wie das ComboBox-Steuerelement verwenden? (C#) | Microsoft-Dokumentation
author: rick-anderson
description: ComboBox ist ein ASP.NET AJAX-Steuerelement, das die Flexibilität eines Textfelds mit einer Liste von Optionen kombiniert, die Benutzer auswählen können.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 035bcb2fb6cce246b904c295aba15efd17c2c232
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045064"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>Gewusst wie das ComboBox-Steuerelement verwenden? (C#)

von [Microsoft](https://github.com/microsoft)

> ComboBox ist ein ASP.NET AJAX-Steuerelement, das die Flexibilität eines Textfelds mit einer Liste von Optionen kombiniert, die Benutzer auswählen können.

Ziel dieses Tutorials ist es, das AJAX Control Toolkit ComboBox-Steuerelement zu erläutern. Das Kombinations Feld funktioniert wie eine Kombination zwischen einem standardmäßigen ASP.net-Dropdown List-Steuerelement und einem TextBox-Steuerelement. Sie können entweder aus einer bereits vorhandenen Liste von Elementen auswählen oder ein neues Element eingeben.

Das ComboBox-Steuerelement ähnelt dem AutoComplete Control Extender, aber die Steuerelemente werden in verschiedenen Szenarien verwendet. Der AutoComplete-Extender fragt einen Webdienst ab, um übereinstimmende Einträge zu erhalten. Das ComboBox-Steuerelement wird im Gegensatz dazu mit einem Satz von Elementen initialisiert. Der AutoComplete-Extender ist sinnvoll, wenn Sie mit einem großen Satz von Daten arbeiten (Millionen von Wagen teilen), während das ComboBox-Steuerelement beim Arbeiten mit einem kleinen Satz von Daten (Dutzende von Wagen teilen) sinnvoll ist.

## <a name="selecting-from-a-static-list-of-items"></a>Auswählen aus einer statischen Liste von Elementen

Beginnen wir mit einem einfachen Beispiel für die Verwendung des ComboBox-Steuer Elements. Stellen Sie sich vor, dass Sie eine statische Liste von Elementen in einer Dropdown Liste anzeigen möchten. Sie sollten jedoch die Möglichkeit offen lassen, dass die Liste nicht fertig ist. Sie möchten, dass Benutzer einen benutzerdefinierten Wert in die Liste eingeben.

Wir erstellen eine neue ASP.net-Web Forms Seite und verwenden das ComboBox-Steuerelement auf der Seite. Fügen Sie dem Projekt die neue ASP.NET-Seite hinzu, und wechseln Sie zu Designansicht.

Wenn Sie das ComboBox-Steuerelement auf der Seite verwenden möchten, müssen Sie der Seite ein ScriptManager-Steuerelement hinzufügen. Ziehen Sie das ScriptManager-Steuerelement von unterhalb der Registerkarte AJAX-Erweiterungen auf die Designer Oberfläche. Sie sollten das ScriptManager-Steuerelement oben auf der Seite hinzufügen. Sie können Sie direkt unterhalb des öffnenden serverseitigen &lt; Formular Tags hinzufügen &gt; .

Ziehen Sie als nächstes das ComboBox-Steuerelement auf die Seite. Sie können das ComboBox-Steuerelement in der Toolbox mit den anderen AJAX Control Toolkit-Steuerelementen und Steuerelement Erweiterungen suchen (siehe) Abbildung 1).

[![Einfaches Formular zum Erstellen einer Visitenkarte](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**Abbildung 01**: Auswählen des ComboBox-Steuer Elements aus der Toolbox ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image2.png))

Wir verwenden das ComboBox-Steuerelement, um eine statische Liste von Optionen anzuzeigen. Der Benutzer kann eine bestimmte Ebene von spiciness für sein Essen aus einer Liste mit drei Optionen auswählen: mild, Mittel und heiß (siehe Abbildung 2).

[![Auswählen aus einer statischen Liste von Elementen](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**Abbildung 02**: auswählen aus einer statischen Liste von Elementen ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image4.png))

Es gibt zwei Möglichkeiten, wie Sie diese Optionen dem ComboBox-Steuerelement hinzufügen können. Wählen Sie zunächst die Task Option Optionen bearbeiten, wenn Sie mit der Maus auf das Steuerelement in Designansicht zeigen und den Element-Editor öffnen (siehe Abbildung 3).

[![Bearbeiten von ComboBox-Elementen](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**Abbildung 03**: Bearbeiten von ComboBox-Elementen ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image6.png))

Die zweite Option besteht darin, die Liste der Elemente zwischen den öffnenden und schließenden &lt; ASP: ComboBox- &gt; Tags in der Quell Ansicht hinzuzufügen. Die Seite in der Liste 1 enthält das aktualisierte Kombinations Feld mit der Liste der Elemente.

**Codebeispiel 1: static. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

Wenn Sie die Seite in der Liste 1 öffnen, können Sie eine der bereits vorhandenen Optionen aus dem Kombinations Feld auswählen. Das heißt, das Kombinations Feld funktioniert genau wie ein Dropdown List-Steuerelement.

Sie haben jedoch auch die Möglichkeit, eine neue Auswahl (z. b. superspicy) einzugeben, die nicht in der Liste vorhanden ist. Das Kombinations Feld funktioniert auch wie ein TextBox-Steuerelement.

Unabhängig davon, ob Sie ein bereits vorhandenes Element auswählen oder wenn Sie ein benutzerdefiniertes Element eingeben, wird die Auswahl im Label-Steuerelement angezeigt, wenn Sie das Formular übermitteln. Wenn Sie das Formular senden, wird der btnSubmit \_ -Click-Handler ausgeführt, und die Bezeichnung wird aktualisiert (siehe Abbildung 4).

[![Anzeigen des ausgewählten Elements](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**Abbildung 04**: Anzeigen des ausgewählten Elements ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image8.png))

Das Kombinations Feld unterstützt die gleichen Eigenschaften wie das Dropdown List-Steuerelement zum Abrufen des ausgewählten Elements, nachdem ein Formular übermittelt wurde:

- SelectedItem. Text: zeigt den Wert der Text-Eigenschaft des ausgewählten Elements an.
- SelectedItem. Value: zeigt den Wert der Value-Eigenschaft des ausgewählten Elements an oder zeigt den Text an, der in das Kombinations Feld eingegeben wurde.
- SelectedValue-identisch mit SelectedItem. Value, außer dass diese Eigenschaft es Ihnen ermöglicht, das standardmäßige (anfängliche) ausgewählte Element anzugeben.

Wenn Sie eine benutzerdefinierte Auswahl in das Kombinations Feld eingeben, wird die benutzerdefinierte Auswahl sowohl den SelectedItem. Text-als auch der SelectedItem. Value-Eigenschaft zugewiesen.

## <a name="selecting-the-list-of-items-from-the-database"></a>Auswählen der Liste der Elemente aus der Datenbank

Sie können die Liste der Elemente, die in der ComboBox angezeigt werden, aus einer Datenbank abrufen. Beispielsweise können Sie das ComboBox-Steuerelement an ein SqlDataSource-Steuerelement, ein ObjectDataSource-Steuerelement, eine LinqDataSource oder eine EntityDataSource binden.

Stellen Sie sich vor, Sie möchten eine Liste der Filme in einem Kombinations Feld anzeigen. Sie möchten die Liste der Filme aus der Datenbanktabelle "Movies" abrufen. Folgen Sie diesen Schritten:

1. Erstellen einer Seite mit dem Namen "Movies. aspx"
2. Fügen Sie der Seite ein ScriptManager-Steuerelement hinzu, indem Sie den ScriptManager von der Registerkarte AJAX-Erweiterungen in der Toolbox auf die Seite ziehen.
3. Fügen Sie der Seite ein ComboBox-Steuerelement hinzu, indem Sie das Kombinations Feld auf die Seite ziehen.
4. Zeigen Sie in Designansicht mit der Maus auf das ComboBox-Steuerelement, und wählen Sie die Option **Datenquellen Aufgabe auswählen** (siehe Abbildung 5). Der Assistent zum Konfigurieren von Datenquellen wird gestartet.
5. Wählen Sie im Schritt **Datenquelle auswählen** die &lt; Option Neue Datenquelle aus &gt; .
6. Wählen Sie im Schritt **Wählen Sie einen Daten Quellentyp** aus die Option Datenbank aus.
7. Wählen Sie im Schritt **Wählen Sie Ihre Datenverbindung** aus die Datenbank aus (z. b. "moviesdb. mdf").
8. Wählen Sie im Schritt **Speichern Sie die Verbindungs Zeichenfolge in der Anwendungs Konfigurationsdatei** aus die Option zum Speichern der Verbindungs Zeichenfolge aus.
9. Wählen Sie im Schritt **Konfigurieren der SELECT-Anweisung** die Datenbanktabelle Movies aus, und wählen Sie alle Spalten aus.
10. Klicken Sie im Schritt **Test Abfrage** auf die Schaltfläche Fertigstellen.
11. Wählen Sie im Schritt **Datenquelle auswählen** die Spalte Titel für das anzuzeigende Feld und die Spalte ID für das Datenfeld aus (siehe Abbildung).
12. Klicken Sie auf die Schaltfläche OK, um den Assistenten zu schließen.

[![Auswählen einer Datenquelle](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**Abbildung 05**: Auswählen einer Datenquelle ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image10.png))

[![Auswählen der Felder für Daten Text und-Wert](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**Abbildung 06**: Auswählen der Felder für Daten Text und-Wert ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image12.png))

Nachdem Sie die obigen Schritte ausgeführt haben, ist das ComboBox-Steuerelement an ein SqlDataSource-Steuerelement gebunden, das die Filme aus der Datenbanktabelle "Movies" darstellt. Die Quelle für die Seite sieht wie in der Liste 2 aus (Ich habe die Formatierung etwas bereinigt).

**Codebeispiel 2: Movies. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

Beachten Sie, dass das ComboBox-Steuerelement über eine DataSourceID-Eigenschaft verfügt, die auf das SqlDataSource-Steuerelement verweist. Wenn Sie die Seite in einem Browser öffnen, wird die Liste der Filme aus der Datenbank angezeigt (siehe Abbildung 7). Sie können entweder einen Film aus der Liste auswählen oder einen neuen Film eingeben, indem Sie den Film in das Kombinations Feld eingeben.

[![Anzeigen einer Liste von Filmen](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**Abbildung 07**: Anzeigen einer Liste von Filmen ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>Festlegen von DropDownStyle

Mit der DropDownStyle-Eigenschaft ComboBox können Sie das Verhalten der ComboBox ändern. Diese Eigenschaft akzeptiert mögliche Werte:

- Dropdown-(Standardwert) das Kombinations Feld zeigt eine Dropdown Liste an, wenn Sie auf den Pfeil klicken, und Sie können einen benutzerdefinierten Wert eingeben.
- Einfach: im Kombinations Feld wird automatisch eine Dropdown Liste angezeigt, und Sie können einen benutzerdefinierten Wert eingeben.
- Dropdown List: das ComboBox-Steuerelement funktioniert genau wie ein DropDownList-Steuerelement.

Der Unterschied zwischen Dropdown und Simple ist, wenn die Liste der Elemente angezeigt wird. Im Fall von Simple wird die Liste sofort angezeigt, wenn Sie den Fokus auf das Kombinations Feld verschieben. Wenn Sie die Dropdown Liste auswählen, müssen Sie auf den Pfeil klicken, um die Liste der Elemente anzuzeigen.

Der DropDownList-Wert bewirkt, dass das ComboBox-Steuerelement genau wie ein Standardmäßiges DropDownList-Steuerelement funktioniert. Hier gibt es jedoch einen wichtigen Unterschied. In älteren Versionen von Internet Explorer wird ein Dropdown List-Steuerelement mit einem unendlichen z-Index angezeigt, sodass das Steuerelement vor allen vorgelagerten Steuerelementen angezeigt wird. Da das Kombinations Feld ein HTML &lt; &gt; -div-Tag anstelle eines HTML- &lt; Select-Tags rendert &gt; , respektiert das Kombinations Feld die z-Reihenfolge ordnungsgemäß.

## <a name="setting-the-autocompletemode"></a>Festlegen von AutoCompleteMode

Mithilfe der ComboBox AutoCompleteMode-Eigenschaft geben Sie an, was geschieht, wenn jemand Text in das Kombinations Feld eingibt. Diese Eigenschaft akzeptiert die folgenden möglichen Werte:

- None (Standardwert) das ComboBox-Tool bietet kein Verhalten für automatisches vervollständigen.
- Vorschlagen: im Kombinations Feld wird die Liste angezeigt, und das passende Element in der Liste wird hervorgehoben (siehe Abbildung 8).
- Anfügen: das ComboBox-Element zeigt die Liste nicht an und fügt das übereinstimmende Element in der Liste an, was Sie eingegeben haben (siehe Abbildung 9).
- Vorschlag anfügen: in der ComboBox wird die Liste angezeigt, und das übereinstimmende Element wird an die von Ihnen typisierte Liste angehängt (siehe Abbildung 10).

[![Die ComboBox macht einen Vorschlag.](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**Abbildung 08**: ComboBox macht einen Vorschlag ([Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image16.png))

[![ComboBox fügt übereinstimmenden Text an](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**Abbildung 09**: ComboBox fügt übereinstimmenden Text[an (Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image18.png))

[![ComboBox schlägt vor und fügt an](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**Abbildung 10**: ComboBox schlägt vor und fügt[Sie an (Klicken Sie, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-combobox-control-cs/_static/image20.png))

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie gelernt, wie Sie mit dem ComboBox-Steuerelement einen festgelegten Satz von Elementen anzeigen. Wir haben das ComboBox-Steuerelement sowohl an einen statischen Satz von Elementen als auch an eine Datenbanktabelle gebunden. Schließlich haben Sie erfahren, wie Sie das Verhalten der ComboBox ändern, indem Sie die Eigenschaften "DropDownStyle" und "AutoCompleteMode" festlegen.

> [!div class="step-by-step"]
> [Nächste](how-do-i-use-the-combobox-control-vb.md)
