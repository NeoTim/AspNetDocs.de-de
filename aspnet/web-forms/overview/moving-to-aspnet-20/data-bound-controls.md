---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Datengebundene Steuerelemente | Microsoft Docs
author: rick-anderson
description: Die meisten ASP.NET Anwendungen basieren auf einem gewissen Grad an Datendarstellung aus einer Back-End-Datenquelle. Datengebundene Steuerelemente waren ein zentraler Bestandteil der Interaktion mit...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 941e2ed15b3da28991e7b06cbab570eb1b5b8899
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543079"
---
# <a name="data-bound-controls"></a>Datengebundene Steuerelemente

von [Microsoft](https://github.com/microsoft)

> Die meisten ASP.NET Anwendungen basieren auf einem gewissen Grad an Datendarstellung aus einer Back-End-Datenquelle. Datengebundene Steuerelemente waren ein zentraler Bestandteil der Interaktion mit Daten in dynamischen Webanwendungen. ASP.NET 2.0 führt einige wesentliche Verbesserungen an datengebundenen Steuerelementen ein, einschließlich einer neuen BaseDataBoundControl-Klasse und deklarativer Syntax.

Die meisten ASP.NET Anwendungen basieren auf einem gewissen Grad an Datendarstellung aus einer Back-End-Datenquelle. Datengebundene Steuerelemente waren ein zentraler Bestandteil der Interaktion mit Daten in dynamischen Webanwendungen. ASP.NET 2.0 führt einige wesentliche Verbesserungen an datengebundenen Steuerelementen ein, einschließlich einer neuen BaseDataBoundControl-Klasse und deklarativer Syntax.

Das BaseDataBoundControl fungiert als Basisklasse für die DataBoundControl-Klasse und die HierarchicalDataBoundControl-Klasse. In dieser Unterrichtseinheit werden die folgenden Klassen erläutert, die von DataBoundControl stammen:

- AdRotator
- Listensteuerelemente
- GridView
- Formview
- Detailsview

Außerdem werden die folgenden Klassen erläutert, die von der HierarchicalDataBoundControl-Klasse stammen:

- TreeView
- Menü
- Sitemappath

## <a name="databoundcontrol-class"></a>DataBoundControl-Klasse

Die DataBoundControl-Klasse ist eine abstrakte Klasse (in VB als MustInherit markiert), die für die Interaktion mit tabellen- oder listenartigen Daten verwendet wird. Die folgenden Steuerelemente sind einige der Steuerelemente, die von DataBoundControl stammen.

## <a name="adrotator"></a>AdRotator

Mit dem AdRotator-Steuerelement können Sie ein Grafikbanner auf einer Webseite anzeigen, die mit einer bestimmten URL verknüpft ist. Die angezeigte Grafik wird mithilfe von Eigenschaften für das Steuerelement gedreht. Die Häufigkeit der Anzeige einer bestimmten Anzeige auf einer Seite kann mithilfe der **Impressions-Eigenschaft** konfiguriert werden, und Anzeigen können mithilfe der Keyword-Filterung gefiltert werden.

AdRotator-Steuerelemente verwenden entweder eine XML-Datei oder eine Tabelle in einer Datenbank für Daten. Die folgenden Attribute werden in XML-Dateien verwendet, um das AdRotator-Steuerelement zu konfigurieren.

### <a name="imageurl"></a>ImageUrl
Die URL eines Bildes, das für die Anzeige angezeigt werden soll.

### <a name="navigateurl"></a>Navigateurl
Die URL, zu der der Benutzer beim Klicken auf die Anzeige geführt werden soll. Dies sollte URL-codiert sein.

### <a name="alternatetext"></a>Alternatetext
Der alternative Text, der in einer QuickInfo angezeigt und von Bildschirmleseprogrammen gelesen wird. Wird auch angezeigt, wenn das von ImageUrl angegebene Bild nicht verfügbar ist.

### <a name="keyword"></a>Stichwort
Definiert ein Schlüsselwort, das bei der Schlüsselwortfilterung verwendet werden kann. Wenn angegeben, werden nur anzeigen mit einem Schlüsselwort angezeigt, das dem Keyword-Filter entspricht.

### <a name="impressions"></a>Eindrücke
Eine Gewichtungsnummer, die bestimmt, wie oft eine bestimmte Anzeige angezeigt wird. Es ist relativ zum Eindruck anderer Anzeigen in der gleichen Datei. Der maximale Wert der Sammelaufrufe für alle Anzeigen in einer XML-Datei beträgt 2.048.000.000 1.

### <a name="height"></a>Höhe
Die Höhe der Anzeige in Pixel.

### <a name="width"></a>Breite
Die Breite der Anzeige in Pixel.

> [!NOTE]
> Die Attribute Höhe und Breite überschreiben die Höhe und Breite für das AdRotator-Steuerelement selbst.

Eine typische XML-Datei sieht möglicherweise wie folgt aus:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

Im obigen Beispiel wird die Anzeige für Contoso aufgrund des Werts für das Impressions-Attribut doppelt so häufig angezeigt wie die Anzeige für die ASP.NET Website.

Um Anzeigen aus der obigen XML-Datei anzuzeigen, fügen Sie einer Seite ein AdRotator-Steuerelement hinzu, und legen Sie fest, dass die **AdvertisementFile-Eigenschaft** auf die XML-Datei zeigt, wie unten gezeigt:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

Wenn Sie eine Datenbanktabelle als Datenquelle für Ihr AdRotator-Steuerelement verwenden, müssen Sie zunächst eine Datenbank mit dem folgenden Schema einrichten:

| **Spaltenname** | **Datentyp** | **Beschreibung** |
| --- | --- | --- |
| id | INT | Der Primärschlüssel. Diese Spalte kann einen beliebigen Namen haben. |
| ImageUrl | nvarchar(*Länge*) | Die relative oder absolute URL des Bildes, das für die Anzeige angezeigt werden soll. |
| Navigateurl | nvarchar(*Länge*) | Die Ziel-URL für die Anzeige. Wenn Sie keinen Wert angeben, handelt es sich bei der Anzeige nicht um einen Hyperlink. |
| Alternatetext | nvarchar(*Länge*) | Der Angezeigte Text, wenn das Bild nicht gefunden werden kann. In einigen Browsern wird der Text als QuickInfo angezeigt. Alternativer Text wird auch für die Barrierefreiheit verwendet, sodass Benutzer, die die Grafik nicht sehen können, ihre Beschreibung laut vorlesen hören können. |
| Stichwort | nvarchar(*Länge*) | Eine Kategorie für die Anzeige, nach der die Seite gefiltert werden kann. |
| Eindrücke | int(4) | Eine Zahl, die die Wahrscheinlichkeit angibt, wie oft die Anzeige angezeigt wird. Je größer die Zahl, desto häufiger wird die Anzeige angezeigt. Die Summe aller Impressionswerte in der XML-Datei darf 2.048.000.000 - 1 nicht überschreiten. |
| Breite | int(4) | Die Breite des Bildes in Pixel. |
| Höhe | int(4) | Die Höhe des Bildes in Pixel. |

In Fällen, in denen Sie bereits über eine Datenbank mit einem anderen Schema verfügen, können Sie die Eigenschaften **AlternateTextField**, **ImageUrlField**und **NavigateUrlField** verwenden, um die AdRotator-Attribute Ihrer vorhandenen Datenbank zuzuordnen. Um die Daten aus der Datenbank im AdRotator-Steuerelement anzuzeigen, fügen Sie der Seite ein Datenquellensteuerelement hinzu, konfigurieren Sie die Verbindungszeichenfolge für das Datenquellensteuerelement, um auf die Datenbank zu verweisen, und legen Sie die **DataSourceID-Eigenschaft** des AdRotator-Steuerelements auf die ID des Datenquellensteuerelements fest. In Fällen, in denen Sie AdRotator-Anzeigen programmgesteuert konfigurieren müssen, verwenden Sie das AdCreated-Ereignis. Das AdCreated-Ereignis nimmt zwei Parameter an. eines ein Objekt und das andere eine Instanz von AdCreatedEventArgs. Die AdCreatedEventArgs ist ein Verweis auf die Anzeige, die erstellt wird.

Der folgende Codeausschnitt legt ImageUrl, NavigateUrl und AlternateText für eine Anzeige programmgesteuert fest:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Listensteuerelemente

Listensteuerelemente umfassen listBox, DropDownList, CheckBoxList, RadioButtonList und BulletedList. Jedes dieser Steuerelemente kann An eine Datenquelle gebunden sein. Sie verwenden ein Feld in der Datenquelle als Anzeigetext und können optional ein zweites Feld als Wert eines Elements verwenden. Elemente können auch statisch zur Entwurfszeit hinzugefügt werden, und Sie können statische Elemente und dynamische Elemente aus einer Datenquelle mischen.

Um ein Listensteuerelement zu binden, fügen Sie der Seite ein Datenquellensteuerelement hinzu. Geben Sie einen SELECT-Befehl für das Datenquellensteuerelement an, und legen Sie dann die DataSourceID-Eigenschaft des Listensteuerelements auf die ID des Datenquellensteuerelements fest. Verwenden Sie die **Eigenschaften DataTextField** und **DataValueField,** um den Anzeigetext und den Wert für das Steuerelement zu definieren. Darüber hinaus können Sie die **DataTextFormatString-Eigenschaft** verwenden, um die Darstellung des Anzeigetextes wie folgt zu steuern:

| **Ausdruck** | **Beschreibung** |
| --- | --- |
| Preis:{0:C} | Für numerische/dezimale Daten. Zeigt das Literal "Price:" gefolgt von Zahlen im Währungsformat an. Das Währungsformat hängt von der Kultureinstellung ab, die im Kulturattribut in der **Page-Direktive** oder in der Datei Web.config angegeben ist. |
| {0:D4} | Für ganzzahlige Daten. Kann nicht mit Dezimalzahlen verwendet werden. Ganzzahlen werden in einem Feld mit null aufgepolstert angezeigt, das vier Zeichen breit ist. |
| {0:N2}% | Für numerische Daten. Zeigt die Zahl mit einer Genauigkeit von 2 Dezimalstellen gefolgt von der Literalgenauigkeit "%" an. |
| {0:000.0} | Für numerische/dezimale Daten. Zahlen werden auf eine Dezimalstelle gerundet. Zahlen mit weniger als drei Ziffern werden durch Nullen ergänzt. |
| {0:D} | Für Datums-/Uhrzeitdaten. Zeigt das lange Datumsformat an ("Donnerstag, 06. August 1996"). Das Datumsformat hängt von der Kultureinstellung der Seite oder der Datei Web.config ab. |
| {0:d} | Für Datums-/Uhrzeitdaten. Zeigt das kurzes Datumsformat an ("12/31/99"). |
| {0:JJ-MM-TT} | Für Datums-/Uhrzeitdaten. Zeigt Datum im numerischen Jahres-Monats-Tag-Format an (96-08-06) |

## <a name="gridview"></a>GridView

Das GridView-Steuerelement ermöglicht die tabellarische Datenanzeige und -bearbeitung mit einem deklarativen Ansatz und ist der Nachfolger des DataGrid-Steuerelements. Die folgenden Funktionen sind im GridView-Steuerelement verfügbar.

- Bindung an Datenquellensteuerelemente, z. B. SqlDataSource.
- Integrierte Sortierfunktionen.
- Integrierte Aktualisierungs- und Löschfunktionen.
- Integrierte Paging-Funktionen.
- Integrierte Zeilenauswahlfunktionen.
- Programmgesteuerter Zugriff auf das GridView-Objektmodell zum dynamischen Festlegen von Eigenschaften, behandeln von Ereignissen usw.
- Mehrere Schlüsselfelder.
- Mehrere Datenfelder für die Hyperlinkspalten.
- Anpassbares Erscheinungsbild durch Themen und Stile.

**Spaltenfelder**

Jede Spalte im GridView-Steuerelement wird durch ein DataControlField-Objekt dargestellt. Standardmäßig ist die AutoGenerateColumns-Eigenschaft auf **true**festgelegt, wodurch für jedes Feld in der Datenquelle ein AutoGeneratedField-Objekt erstellt wird. Jedes Feld wird dann als Spalte im GridView-Steuerelement in der Reihenfolge gerendert, in der jedes Feld in der Datenquelle angezeigt wird. Sie können auch manuell steuern, welche Spaltenfelder im **GridView-Steuerelement** angezeigt werden, indem Sie die **AutoGenerateColumns-Eigenschaft** auf **false** festlegen und dann Ihre eigene Spaltenfeldauflistung definieren. Verschiedene Spaltenfeldtypen bestimmen das Verhalten der Spalten im Steuerelement.

In der folgenden Tabelle sind die verschiedenen Spaltenfeldtypen aufgeführt, die verwendet werden können.

| **Spaltenfeldtyp** | **Beschreibung** |
| --- | --- |
| BoundField | Zeigt den Wert eines Felds in einer Datenquelle an. Dies ist der Standardspaltentyp des GridView-Steuerelements. |
| ButtonField | Zeigt eine Befehlsschaltfläche für jedes Element im GridView-Steuerelement an. Auf diese Weise können Sie eine Spalte mit benutzerdefinierten Schaltflächensteuerelementen erstellen, z. B. die Schaltfläche Hinzufügen oder Entfernen. |
| CheckBoxField | Zeigt ein Kontrollkästchen für jedes Element im GridView-Steuerelement an. Dieser Spaltenfeldtyp wird häufig verwendet, um Felder mit einem booleschen Wert anzuzeigen. |
| CommandField | Zeigt vordefinierte Befehlsschaltflächen an, um Auswahl-, Bearbeitungs- oder Löschvorgänge auszuführen. |
| HyperLinkField | Zeigt den Wert eines Felds in einer Datenquelle als Hyperlink an. Mit diesem Spaltenfeldtyp können Sie ein zweites Feld an die URL des Hyperlinks binden. |
| ImageField | Zeigt ein Bild für jedes Element im GridView-Steuerelement an. |
| Templatefield | Zeigt benutzerdefinierte Inhalte für jedes Element im GridView-Steuerelement gemäß einer angegebenen Vorlage an. Mit diesem Spaltenfeldtyp können Sie ein benutzerdefiniertes Spaltenfeld erstellen. |

Um eine Spaltenfeldauflistung deklarativ zu definieren, fügen Sie zunächst öffnende und schließende ** &lt;&gt; Columns-Tags** zwischen den öffnenden und schließenden Tags des GridView-Steuerelements hinzu. Als Nächstes listen Sie die Spaltenfelder auf, die zwischen den Tags "Öffnen" und "Schließen ** &lt;von Spalten"&gt; ** eingeschlossen werden sollen. Die angegebenen Spalten werden der Columns-Auflistung in der angegebenen Reihenfolge hinzugefügt. Die **Columns-Auflistung** speichert alle Spaltenfelder im Steuerelement und ermöglicht die programmgesteuerte Verwaltung der Spaltenfelder im GridView-Steuerelement.

Explizit deklarierte Spaltenfelder können in Kombination mit automatisch generierten Spaltenfeldern angezeigt werden. Wenn beide verwendet werden, werden explizit deklarierte Spaltenfelder zuerst gerendert, gefolgt von den automatisch generierten Spaltenfeldern.

## <a name="binding-to-data"></a>Bindung an Daten

Das GridView-Steuerelement kann an ein Datenquellensteuerelement (z. B. **SqlDataSource**, **ObjectDataSource**usw.) sowie an jede Datenquelle gebunden werden, die die System.Collections.IEnumerable-Schnittstelle implementiert (z. B. System.Data.DataView, System.Collections.ArrayList oder System.Collections.Hashtable). Verwenden Sie eine der folgenden Methoden, um das GridView-Steuerelement an den entsprechenden Datenquellentyp zu binden:

- Um eine Bindung an ein Datenquellensteuerelement zu erhalten, legen Sie die DataSourceID-Eigenschaft des GridView-Steuerelements auf den ID-Wert des Datenquellensteuerelements fest. Das GridView-Steuerelement bindet automatisch an das angegebene Datenquellensteuerelement und kann die Funktionen des Datenquellensteuerelements nutzen, um Sortier-, Aktualisierungs-, Lösch- und Pagingfunktionen durchzuführen. Dies ist die bevorzugte Methode zum Binden an Daten.
- Um eine Bindung an eine Datenquelle zu erhalten, die die System.Collections.IEnumerable-Schnittstelle implementiert, legen Sie programmgesteuert die DataSource-Eigenschaft des GridView-Steuerelements auf die Datenquelle fest, und rufen Sie dann die DataBind-Methode auf. Bei Verwendung dieser Methode bietet das GridView-Steuerelement keine integrierte Sortier-, Aktualisierungs-, Lösch- und Pagingfunktionalität. Sie müssen diese Funktionalität selbst bereitstellen.

## <a name="data-operations"></a>Datenvorgänge

Das GridView-Steuerelement bietet viele integrierte Funktionen, mit denen der Benutzer Elemente im Steuerelement sortieren, aktualisieren, löschen, auswählen und durchblättern kann. Wenn das GridView-Steuerelement an ein Datenquellensteuerelement gebunden ist, kann das GridView-Steuerelement die Funktionen des Datenquellensteuerelements nutzen und automatische Sortier-, Aktualisierungs- und Löschfunktionen bereitstellen.

> [!NOTE]
> Das GridView-Steuerelement kann Unterstützung für das Sortieren, Aktualisieren und Löschen mit anderen Arten von Datenquellen bereitstellen. Sie müssen jedoch einen geeigneten Ereignishandler für die Implementierung für diese Vorgänge bereitstellen.

Die Sortierung ermöglicht es dem Benutzer, die Elemente im GridView-Steuerelement in Bezug auf eine bestimmte Spalte zu sortieren, indem er auf die Spalte kopfklicken. Um die Sortierung zu aktivieren, legen Sie die AllowSorting-Eigenschaft auf **true**fest.

Die automatischen Aktualisierungs-, Lösch- und Auswahlfunktionen werden aktiviert, wenn auf eine Schaltfläche in einem **Spaltenfeld ButtonField** oder **TemplateField** mit dem Befehlsnamen "Bearbeiten", "Löschen" bzw. "Auswählen" geklickt wird. Das GridView-Steuerelement kann automatisch ein **CommandField-Spaltenfeld** mit der Schaltfläche Bearbeiten, Löschen oder Auswählen hinzufügen, wenn die Eigenschaft AutoGenerateEditButton, AutoGenerateDeleteButton oder AutoGenerateSelectButton auf **true**festgelegt ist.

> [!NOTE]
> Das Einfügen von Datensätzen in die Datenquelle wird vom GridView-Steuerelement nicht direkt unterstützt. Es ist jedoch möglich, Datensätze mithilfe des GridView-Steuerelements in Verbindung mit dem DetailsView- oder FormView-Steuerelement einzufügen.

Anstatt alle Datensätze in der Datenquelle gleichzeitig anzuzeigen, kann das GridView-Steuerelement die Datensätze automatisch in Seiten aufteilen. Um Paging zu aktivieren, legen Sie die AllowPaging-Eigenschaft auf **true**fest.

## <a name="customizing-the-user-interface"></a>Anpassen der Benutzeroberfläche

Sie können die Darstellung des GridView-Steuerelements anpassen, indem Sie die Stileigenschaften für die verschiedenen Teile des Steuerelements festlegen. In der folgenden Tabelle sind die verschiedenen Stileigenschaften aufgeführt.

| **Style-Eigenschaft** | **Beschreibung** |
| --- | --- |
| Alternatingrowstyle | Die Stileinstellungen für die abwechselnden Datenzeilen im GridView-Steuerelement. Wenn diese Eigenschaft festgelegt ist, werden die Datenzeilen abwechselnd zwischen den RowStyle-Einstellungen und den **AlternatingRowStyle-Einstellungen** angezeigt. |
| Editrowstyle | Die Stileinstellungen für die Zeile, die im GridView-Steuerelement bearbeitet wird. |
| Emptydatarowstyle | Die Stileinstellungen für die leere Datenzeile, die im GridView-Steuerelement angezeigt wird, wenn die Datenquelle keine Datensätze enthält. |
| Footerstyle | Die Stileinstellungen für die Fußzeilenzeile des GridView-Steuerelements. |
| Headerstyle | Die Stileinstellungen für die Kopfzeile des GridView-Steuerelements. |
| Pagerstyle | Die Stileinstellungen für die Pagerzeile des GridView-Steuerelements. |
| Rowstyle | Die Stileinstellungen für die Datenzeilen im GridView-Steuerelement. Wenn auch die **AlternatingRowStyle-Eigenschaft** festgelegt ist, werden die Datenzeilen abwechselnd zwischen den **RowStyle-Einstellungen** und den **AlternatingRowStyle-Einstellungen** angezeigt. |
| Selectedrowstyle | Die Stileinstellungen für die ausgewählte Zeile im GridView-Steuerelement. |

Sie können auch verschiedene Teile des Steuerelements ein- oder ausblenden. In der folgenden Tabelle sind die Eigenschaften aufgeführt, die steuern, welche Teile angezeigt oder ausgeblendet werden.

| **Eigenschaft** | **Beschreibung** |
| --- | --- |
| Showfooter | Zeigt den Fußzeilenabschnitt des GridView-Steuerelements an oder blendet ihn aus. |
| Showheader | Zeigt den Kopfzeilenabschnitt des GridView-Steuerelements ein oder blendet ihn aus. |

### <a name="events"></a>Ereignisse

Das GridView-Steuerelement stellt mehrere Ereignisse bereit, für die Sie programmieren können. Auf diese Weise können Sie eine benutzerdefinierte Routine ausführen, wenn ein Ereignis eintritt. In der folgenden Tabelle sind die vom GridView-Steuerelement unterstützten Ereignisse aufgeführt.

| **Event** | **Beschreibung** |
| --- | --- |
| Pageindexchanged | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber nachdem das GridView-Steuerelement den Auslagerungsvorgang verarbeitet hat. Dieses Ereignis wird häufig verwendet, wenn Sie eine Aufgabe ausführen müssen, nachdem der Benutzer zu einer anderen Seite im Steuerelement navigiert. |
| PageIndexChanging | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber bevor das GridView-Steuerelement den Auslagerungsvorgang verarbeitet. Dieses Ereignis wird häufig verwendet, um den Auslagerungsvorgang abzubrechen. |
| Rowcancelingedit | Tritt auf, wenn auf die Schaltfläche Abbrechen einer Zeile geklickt wird, aber bevor das GridView-Steuerelement den Bearbeitungsmodus beendet. Dieses Ereignis wird häufig verwendet, um den Abbruchvorgang zu beenden. |
| Rowcommand | Tritt auf, wenn im GridView-Steuerelement auf eine Schaltfläche geklickt wird. Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, wenn im Steuerelement auf eine Schaltfläche geklickt wird. |
| Rowcreated | Tritt auf, wenn eine neue Zeile im GridView-Steuerelement erstellt wird. Dieses Ereignis wird häufig verwendet, um den Inhalt einer Zeile zu ändern, wenn die Zeile erstellt wird. |
| Rowdatabound | Tritt auf, wenn eine Datenzeile an Daten im GridView-Steuerelement gebunden ist. Dieses Ereignis wird häufig verwendet, um den Inhalt einer Zeile zu ändern, wenn die Zeile an Daten gebunden ist. |
| RowDeleted | Tritt auf, wenn auf die Schaltfläche Löschen einer Zeile geklickt wird, aber nachdem das GridView-Steuerelement den Datensatz aus der Datenquelle gelöscht hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Löschvorgangs zu überprüfen. |
| RowDeleting | Tritt auf, wenn auf die Schaltfläche Löschen einer Zeile geklickt wird, aber bevor das GridView-Steuerelement den Datensatz aus der Datenquelle löscht. Dieses Ereignis wird häufig verwendet, um den Löschvorgang abzubrechen. |
| Rowediting | Tritt auf, wenn auf die Schaltfläche Bearbeiten einer Zeile geklickt wird, bevor das GridView-Steuerelement jedoch in den Bearbeitungsmodus wechselt. Dieses Ereignis wird häufig verwendet, um den Bearbeitungsvorgang abzubrechen. |
| Rowupdated | Tritt auf, wenn auf die Schaltfläche Aktualisieren einer Zeile geklickt wird, aber nachdem das GridView-Steuerelement die Zeile aktualisiert hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Aktualisierungsvorgangs zu überprüfen. |
| Rowupdating | Tritt auf, wenn auf die Schaltfläche Aktualisieren einer Zeile geklickt wird, aber bevor das GridView-Steuerelement die Zeile aktualisiert. Dieses Ereignis wird häufig verwendet, um den Aktualisierungsvorgang abzubrechen. |
| SelectedIndexChanged | Tritt auf, wenn auf die Schaltfläche Select einer Zeile geklickt wird, aber nachdem das GridView-Steuerelement den Auswahlvorgang verarbeitet hat. Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, nachdem eine Zeile im Steuerelement ausgewählt wurde. |
| SelectedIndexChanging | Tritt auf, wenn auf die Schaltfläche Select einer Zeile geklickt wird, aber bevor das GridView-Steuerelement den Auswahlvorgang verarbeitet. Dieses Ereignis wird häufig verwendet, um den Auswahlvorgang abzubrechen. |
| Sortiert | Tritt auf, wenn auf den Hyperlink zum Sortieren einer Spalte geklickt wird, nachdem das GridView-Steuerelement den Sortiervorgang verarbeitet hat. Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, nachdem der Benutzer auf einen Hyperlink geklickt hat, um eine Spalte zu sortieren. |
| Sortierung | Tritt auf, wenn auf den Hyperlink zum Sortieren einer Spalte geklickt wird, aber bevor das GridView-Steuerelement den Sortiervorgang verarbeitet. Dieses Ereignis wird häufig verwendet, um den Sortiervorgang abzubrechen oder eine benutzerdefinierte Sortierroutine auszuführen. |

## <a name="formview"></a>Formview

Das FormView-Steuerelement wird verwendet, um einen einzelnen Datensatz aus einer Datenquelle anzuzeigen. Es ähnelt dem DetailsView-Steuerelement, außer es zeigt benutzerdefinierte Vorlagen anstelle von Zeilenfeldern an. Das Erstellen eigener Vorlagen bietet Ihnen mehr Flexibilität bei der Steuerung der Anzeige der Daten. Das FormView-Steuerelement unterstützt die folgenden Funktionen:

- Bindung an Datenquellensteuerelemente, z. B. SqlDataSource und ObjectDataSource.
- Integrierte Einfügefunktionen.
- Integrierte Aktualisierungs- und Löschfunktionen.
- Integrierte Paging-Funktionen.
- Programmgesteuerter Zugriff auf das FormView-Objektmodell zum dynamischen Festlegen von Eigenschaften, behandeln von Ereignissen usw.
- Anpassbares Erscheinungsbild durch benutzerdefinierte Vorlagen, Designs und Stile.

## <a name="templates"></a>Vorlagen

Damit das FormView-Steuerelement Inhalte anzeigt, müssen Sie Vorlagen für die verschiedenen Teile des Steuerelements erstellen. Die meisten Vorlagen sind optional. Sie müssen jedoch eine Vorlage für den Modus erstellen, in dem das Steuerelement konfiguriert ist. Beispielsweise muss für ein FormView-Steuerelement, das das Einfügen von Datensätzen unterstützt, eine Einfügeelementvorlage definiert sein. In der folgenden Tabelle sind die verschiedenen Vorlagen aufgeführt, die Sie erstellen können.

| **Vorlagentyp** | **Beschreibung** |
| --- | --- |
| Edititemtemplate | Definiert den Inhalt für die Datenzeile, wenn sich das FormView-Steuerelement im Bearbeitungsmodus befindet. Diese Vorlage enthält in der Regel Eingabesteuerelemente und Befehlsschaltflächen, mit denen der Benutzer einen vorhandenen Datensatz bearbeiten kann. |
| Emptydatatemplate | Definiert den Inhalt für die leere Datenzeile, die angezeigt wird, wenn das FormView-Steuerelement an eine Datenquelle gebunden ist, die keine Datensätze enthält. Diese Vorlage enthält normalerweise Inhalt, um den Benutzer darauf aufmerksam zu machen, dass die Datenquelle keine Datensätze enthält. |
| Footertemplate | Definiert den Inhalt für die Fußzeilenzeile. Diese Vorlage enthält in der Regel alle zusätzlichen Inhalte, die Sie in der Fußzeile anzeigen möchten. Alternativ können Sie einfach Text angeben, der in der Fußzeile angezeigt werden soll, indem Sie die FooterText-Eigenschaft festlegen. |
| Headertemplate | Definiert den Inhalt für die Kopfzeile. Diese Vorlage enthält in der Regel alle zusätzlichen Inhalte, die Sie in der Kopfzeile anzeigen möchten. Alternativ können Sie einfach Text angeben, der in der Kopfzeile angezeigt werden soll, indem Sie die HeaderText-Eigenschaft festlegen. |
| ItemTemplate | Definiert den Inhalt für die Datenzeile, wenn sich das FormView-Steuerelement im schreibgeschützten Modus befindet. Diese Vorlage enthält normalerweise Inhalt, um die Werte eines vorhandenen Datensatzes anzuzeigen. |
| Insertitemtemplate | Definiert den Inhalt für die Datenzeile, wenn sich das FormView-Steuerelement im Einfügemodus befindet. Diese Vorlage enthält in der Regel Eingabesteuerelemente und Befehlsschaltflächen, mit denen der Benutzer einen neuen Datensatz hinzufügen kann. |
| Pagertemplate | Definiert den Inhalt für die Pagerzeile, die angezeigt wird, wenn das Paging-Feature aktiviert ist (wenn die AllowPaging-Eigenschaft auf **true**festgelegt ist). Diese Vorlage enthält in der Regel Steuerelemente, mit denen der Benutzer zu einem anderen Datensatz navigieren kann. |

Eingabesteuerelemente in der Bearbeitungselementvorlage und in der Elementvorlage einfügen können mithilfe eines zweiseitigen Bindungsausdrucks an die Felder einer Datenquelle gebunden werden. Dadurch kann das FormView-Steuerelement automatisch die Werte des Eingabesteuerelements für einen Aktualisierungs- oder Einfügevorgang extrahieren. Zweiweg-Bindungsausdrücke ermöglichen auch Eingabesteuerelemente in einer Bearbeitungselementvorlage, um die ursprünglichen Feldwerte automatisch anzuzeigen.

### <a name="binding-to-data"></a>Bindung an Daten

Das FormView-Steuerelement kann an ein Datenquellensteuerelement (z. B. **SqlDataSource**, AccessDataSource, **ObjectDataSource** usw.) oder an eine beliebige Datenquelle gebunden werden, die die System.Collections.IEnumerable-Schnittstelle implementiert (z. B. System.Data.DataView, System.Collections.ArrayList und System.Collections.Hashtable). Verwenden Sie eine der folgenden Methoden, um das FormView-Steuerelement an den entsprechenden Datenquellentyp zu binden:

- Um eine Bindung an ein Datenquellensteuerelement zu erhalten, legen Sie die DataSourceID-Eigenschaft des FormView-Steuerelements auf den ID-Wert des Datenquellensteuerelements fest. Das FormView-Steuerelement bindet automatisch an das angegebene Datenquellensteuerelement und kann die Funktionen des Datenquellensteuerelements nutzen, um Einfüge-, Aktualisierungs-, Lösch- und Pagingfunktionen auszuführen. Dies ist die bevorzugte Methode zum Binden an Daten.
- Um eine Verbindung an eine Datenquelle zu binden, die die **System.Collections.IEnumerable-Schnittstelle** implementiert, legen Sie programmgesteuert die DataSource-Eigenschaft des FormView-Steuerelements an die Datenquelle fest, und rufen Sie dann die DataBind-Methode auf. Bei Verwendung dieser Methode bietet das FormView-Steuerelement keine integrierte Einfüge-, Aktualisierungs-, Lösch- und Pagingfunktionalität. Sie müssen diese Funktionalität mithilfe des entsprechenden Ereignisses bereitstellen.

## <a name="data-operations"></a>Datenvorgänge

Das FormView-Steuerelement bietet viele integrierte Funktionen, mit denen der Benutzer Elemente im Steuerelement aktualisieren, löschen, einfügen und durchblättern kann. Wenn das FormView-Steuerelement an ein Datenquellensteuerelement gebunden ist, kann das FormView-Steuerelement die Funktionen des Datenquellensteuerelements nutzen und automatische Funktionen zum Aktualisieren, Löschen, Einfügen und Auslagerung bereitstellen. Das FormView-Steuerelement kann Unterstützung für Aktualisierungs-, Lösch-, Einfüge- und Pagingvorgänge mit anderen Datenquellentypen bereitstellen. Sie müssen jedoch einen geeigneten Ereignishandler für die Implementierung für diese Vorgänge bereitstellen.

Da das FormView-Steuerelement Vorlagen verwendet, bietet es keine Möglichkeit, automatisch Befehlsschaltflächen zum Aktualisieren, Löschen oder Einfügen von Vorgängen auszuführen. Sie müssen diese Befehlsschaltflächen manuell in die entsprechende Vorlage aufnehmen. Das FormView-Steuerelement erkennt bestimmte Schaltflächen, deren **CommandName-Eigenschaften** auf bestimmte Werte festgelegt sind. In der folgenden Tabelle sind die Befehlsschaltflächen aufgeführt, die vom FormView-Steuerelement erkannt werden.

| **Schaltfläche** | **Befehlsname-Wert** | **Beschreibung** |
| --- | --- | --- |
| Abbrechen | "Abbrechen" | Wird beim Aktualisieren oder Einfügen von Vorgängen verwendet, um den Vorgang abzubrechen und die vom Benutzer eingegebenen Werte zu verwerfen. Das FormView-Steuerelement kehrt dann in den von der DefaultMode-Eigenschaft angegebenen Modus zurück. |
| Löschen | "Löschen" | Wird beim Löschen von Vorgängen verwendet, um den angezeigten Datensatz aus der Datenquelle zu löschen. Löst die Ereignisse ItemDeleting und ItemDeleted aus. |
| Edit (Bearbeiten) | "Bearbeiten" | Wird bei Aktualisierungsvorgängen verwendet, um das FormView-Steuerelement in den Bearbeitungsmodus zu versetzen. Der in der **EditItemTemplate-Eigenschaft** angegebene Inhalt wird für die Datenzeile angezeigt. |
| Einfügen | "Einfügen" | Wird beim Einfügen von Vorgängen verwendet, um zu versuchen, einen neuen Datensatz mithilfe der vom Benutzer bereitgestellten Werte in die Datenquelle einzufügen. Hebt die Ereignisse ItemInserting und ItemInserted an. |
| Neu | "Neu" | Wird beim Einfügen von Vorgängen verwendet, um das FormView-Steuerelement in den Einfügemodus zu versetzen. Der in der **InsertItemTemplate-Eigenschaft** angegebene Inhalt wird für die Datenzeile angezeigt. |
| Seite | "Seite" | Wird in Pagingvorgängen verwendet, um eine Schaltfläche in der Pagerzeile darzustellen, die Paging ausführt. Um den Paging-Vorgang anzugeben, legen Sie die **CommandArgument-Eigenschaft** der Schaltfläche auf "Next", "Prev", "First", "Last" oder den Index der Seite fest, zu der navigiert werden soll. Hebt die Ereignisse PageIndexChanging und PageIndexChanged an. |
| Aktualisieren | "Update" | Wird bei Aktualisierungsvorgängen verwendet, um zu versuchen, den angezeigten Datensatz in der Datenquelle mit den vom Benutzer bereitgestellten Werten zu aktualisieren. Hebt die Ereignisse ItemUpdating und ItemUpdated an. |

Im Gegensatz zur Schaltfläche Löschen (die den angezeigten Datensatz sofort löscht) wechselt das FormView-Steuerelement in den Bearbeitungs- bzw. Einfügemodus, wenn auf die Schaltfläche Bearbeiten oder Neu geklickt wird. Im Bearbeitungsmodus wird der Inhalt der **EditItemTemplate-Eigenschaft** für das aktuelle Datenelement angezeigt. In der Regel wird die Vorlage für Bearbeitungselemente so definiert, dass die Schaltfläche Bearbeiten durch eine Schaltfläche "Aktualisieren" und "Abbrechen" ersetzt wird. Eingabesteuerelemente, die für den Datentyp des Felds geeignet sind (z. B. ein TextBox- oder checkBox-Steuerelement), werden in der Regel auch mit dem Wert eines Felds angezeigt, den der Benutzer ändern kann. Wenn Sie auf die Schaltfläche Aktualisieren klicken, wird der Datensatz in der Datenquelle aktualisiert, während durch Klicken auf die Schaltfläche Abbrechen alle Änderungen aufgehoben wird.

Ebenso wird der Inhalt der **InsertItemTemplate-Eigenschaft** für das Datenelement angezeigt, wenn sich das Steuerelement im Einfügemodus befindet. Die Vorlage zum Einfügen von Elementen ist in der Regel so definiert, dass die Schaltfläche Neu durch eine Schaltfläche Einfügen und Abbrechen ersetzt wird und leere Eingabesteuerelemente angezeigt werden, damit der Benutzer die Werte für den neuen Datensatz eingeben kann. Wenn Sie auf die Schaltfläche Einfügen klicken, wird der Datensatz in die Datenquelle eingefügt, während durch Klicken auf die Schaltfläche Abbrechen alle Änderungen aufgehoben wird.

Das FormView-Steuerelement bietet eine Auslagerungsfunktion, mit der der Benutzer zu anderen Datensätzen in der Datenquelle navigieren kann. Wenn diese Option aktiviert ist, wird im FormView-Steuerelement eine Pagerzeile angezeigt, die die Seitennavigationssteuerelemente enthält. Um Paging zu aktivieren, legen Sie die **AllowPaging-Eigenschaft** auf **true**fest. Sie können die Pagerzeile anpassen, indem Sie die Eigenschaften von Objekten festlegen, die im PagerStyle und in der PagerSettings-Eigenschaft enthalten sind. Anstatt die integrierte Pagerzeilenbenutzeroberfläche zu verwenden, können Sie mithilfe der **PagerTemplate-Eigenschaft** eine eigene Benutzeroberfläche erstellen.

## <a name="customizing-the-user-interface"></a>Anpassen der Benutzeroberfläche

Sie können die Darstellung des FormView-Steuerelements anpassen, indem Sie die Stileigenschaften für die verschiedenen Teile des Steuerelements festlegen. In der folgenden Tabelle sind die verschiedenen Stileigenschaften aufgeführt.

| **Style-Eigenschaft** | **Beschreibung** |
| --- | --- |
| Editrowstyle | Die Stileinstellungen für die Datenzeile, wenn sich das FormView-Steuerelement im Bearbeitungsmodus befindet. |
| Emptydatarowstyle | Die Stileinstellungen für die leere Datenzeile, die im FormView-Steuerelement angezeigt wird, wenn die Datenquelle keine Datensätze enthält. |
| Footerstyle | Die Stileinstellungen für die Fußzeilenzeile des FormView-Steuerelements. |
| Headerstyle | Die Stileinstellungen für die Kopfzeile des FormView-Steuerelements. |
| Insertrowstyle | Die Stileinstellungen für die Datenzeile, wenn sich das FormView-Steuerelement im Einfügemodus befindet. |
| Pagerstyle | Die Stileinstellungen für die Pagerzeile, die im FormView-Steuerelement angezeigt wird, wenn die Paging-Funktion aktiviert ist. |
| Rowstyle | Die Stileinstellungen für die Datenzeile, wenn sich das FormView-Steuerelement im schreibgeschützten Modus befindet. |

## <a name="events"></a>Ereignisse

Das FormView-Steuerelement stellt mehrere Ereignisse bereit, für die Sie programmieren können. Auf diese Weise können Sie eine benutzerdefinierte Routine ausführen, wenn ein Ereignis eintritt. In der folgenden Tabelle sind die vom FormView-Steuerelement unterstützten Ereignisse aufgeführt.

| **Event** | **Beschreibung** |
| --- | --- |
| Itemcommand | Tritt auf, wenn auf eine Schaltfläche innerhalb eines FormView-Steuerelements geklickt wird. Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, wenn im Steuerelement auf eine Schaltfläche geklickt wird. |
| Itemcreated | Tritt auf, nachdem alle FormViewRow-Objekte im FormView-Steuerelement erstellt wurden. Dieses Ereignis wird häufig verwendet, um die Werte eines Datensatzes zu ändern, bevor er angezeigt wird. |
| ItemDeleted | Tritt auf, wenn auf eine Schaltfläche Löschen (eine Schaltfläche mit der Aufserlegen der **CommandName-Eigenschaft** auf "Löschen") geklickt wird, nachdem das FormView-Steuerelement den Datensatz aus der Datenquelle gelöscht hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Löschvorgangs zu überprüfen. |
| ItemDeleting | Tritt auf, wenn auf eine Schaltfläche Löschen geklickt wird, aber bevor das FormView-Steuerelement den Datensatz aus der Datenquelle löscht. Dieses Ereignis wird häufig verwendet, um den Löschvorgang abzubrechen. |
| Iteminserted | Tritt auf, wenn auf eine Schaltfläche Einfügen (eine Schaltfläche mit der **Aufsatzname-Eigenschaft** "Einfügen") geklickt wird, nachdem das FormView-Steuerelement den Datensatz eingefügt hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Einfügevorgangs zu überprüfen. |
| ItemEinfügen | Tritt auf, wenn auf eine Schaltfläche Einfügen geklickt wird, aber bevor das FormView-Steuerelement den Datensatz einfügt. Dieses Ereignis wird häufig verwendet, um den Einfügevorgang abzubrechen. |
| Itemupdated | Tritt auf, wenn auf eine **CommandName** Schaltfläche "Aktualisieren" (eine Schaltfläche mit der Aufgebotseigenschaft "Update") geklickt wird, nachdem das FormView-Steuerelement die Zeile aktualisiert hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Aktualisierungsvorgangs zu überprüfen. |
| Itemupdating | Tritt auf, wenn auf eine Schaltfläche Aktualisieren geklickt wird, aber bevor das FormView-Steuerelement den Datensatz aktualisiert. Dieses Ereignis wird häufig verwendet, um den Aktualisierungsvorgang abzubrechen. |
| ModeChanged | Tritt auf, nachdem das FormView-Steuerelement den Modus geändert hat (zum Bearbeiten, Einfügen oder Schreibmodus). Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, wenn das FormView-Steuerelement die Modi ändert. |
| ModeChanging | Tritt ein, bevor das FormView-Steuerelement die Modi ändert (zum Bearbeiten, Einfügen oder SchreibgeschütztenModus). Dieses Ereignis wird häufig verwendet, um eine Modusänderung abzubrechen. |
| Pageindexchanged | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber nachdem das FormView-Steuerelement den Auslagerungsvorgang verarbeitet hat. Dieses Ereignis wird häufig verwendet, wenn Sie eine Aufgabe ausführen müssen, nachdem der Benutzer zu einem anderen Datensatz im Steuerelement navigiert. |
| PageIndexChanging | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber bevor das FormView-Steuerelement den Auslagerungsvorgang verarbeitet. Dieses Ereignis wird häufig verwendet, um den Auslagerungsvorgang abzubrechen. |

## <a name="detailsview"></a>Detailsview

Das DetailsView-Steuerelement wird verwendet, um einen einzelnen Datensatz aus einer Datenquelle in einer Tabelle anzuzeigen, in der jedes Feld des Datensatzes in einer Zeile der Tabelle angezeigt wird. Es kann in Kombination mit einem GridView-Steuerelement für Master-Detail-Szenarien verwendet werden. Das DetailsView-Steuerelement unterstützt die folgenden Funktionen:

- Bindung an Datenquellensteuerelemente, z. B. SqlDataSource.
- Integrierte Einfügefunktionen.
- Integrierte Aktualisierungs- und Löschfunktionen.
- Integrierte Paging-Funktionen.
- Programmgesteuerter Zugriff auf das DetailsView-Objektmodell zum dynamischen Festlegen von Eigenschaften, behandeln von Ereignissen usw.
- Anpassbares Erscheinungsbild durch Themen und Stile.

## <a name="row-fields"></a>Zeilenfelder

Jede Datenzeile im DetailsView-Steuerelement wird durch Deklarieren eines Feldsteuerelements erstellt. Verschiedene Zeilenfeldtypen bestimmen das Verhalten der Zeilen im Steuerelement. Feldsteuerelemente werden von DataControlField abstammen. In der folgenden Tabelle sind die verschiedenen Zeilenfeldtypen aufgeführt, die verwendet werden können.

| **Spaltenfeldtyp** | **Beschreibung** |
| --- | --- |
| BoundField | Zeigt den Wert eines Felds in einer Datenquelle als Text an. |
| ButtonField | Zeigt eine Befehlsschaltfläche im DetailsView-Steuerelement an. Auf diese Weise können Sie eine Zeile mit einem benutzerdefinierten Schaltflächensteuerelement anzeigen, z. B. einer Schaltfläche Hinzufügen oder Entfernen. |
| CheckBoxField | Zeigt ein Kontrollkästchen im DetailsView-Steuerelement an. Dieser Zeilenfeldtyp wird häufig verwendet, um Felder mit einem booleschen Wert anzuzeigen. |
| CommandField | Zeigt integrierte Befehlsschaltflächen an, um Bearbeitungs-, Einfüge- oder Löschvorgänge im DetailsView-Steuerelement auszuführen. |
| HyperLinkField | Zeigt den Wert eines Felds in einer Datenquelle als Hyperlink an. Mit diesem Zeilenfeldtyp können Sie ein zweites Feld an die URL des Hyperlinks binden. |
| ImageField | Zeigt ein Bild im DetailsView-Steuerelement an. |
| Templatefield | Zeigt benutzerdefinierte Inhalte für eine Zeile im DetailsView-Steuerelement gemäß einer angegebenen Vorlage an. Mit diesem Zeilenfeldtyp können Sie ein benutzerdefiniertes Zeilenfeld erstellen. |

Standardmäßig ist die AutoGenerateRows-Eigenschaft auf **true**festgelegt, wodurch automatisch ein gebundenes Zeilenfeldobjekt für jedes Feld eines bindbaren Typs in der Datenquelle generiert wird. Gültige bindbare Typen sind String, DateTime, Decimal, Guid und der Satz primitiver Typen. Jedes Feld wird dann in einer Zeile als Text in der Reihenfolge angezeigt, in der jedes Feld in der Datenquelle angezeigt wird.

Das automatische Generieren der Zeilen bietet eine schnelle und einfache Möglichkeit, jedes Feld im Datensatz anzuzeigen. Um jedoch die erweiterten Funktionen des DetailsView-Steuerelements nutzen zu können, müssen Sie die Zeilenfelder explizit deklarieren, die in das DetailsView-Steuerelement eingeschlossen werden sollen. Um die Zeilenfelder zu deklarieren, legen Sie zunächst die **AutoGenerateRows-Eigenschaft** auf **false**fest. Fügen Sie als ** &lt;Nächstes&gt; ** öffnende und schließende Fields-Tags zwischen den öffnenden und schließenden Tags des DetailsView-Steuerelements hinzu. Führen Sie schließlich die Zeilenfelder auf, die ** &lt;zwischen&gt; ** den tags öffnende und schließende Felder eingeschlossen werden sollen. Die angegebenen Zeilenfelder werden der Fields-Auflistung in der angegebenen Reihenfolge hinzugefügt. Mit der **Fields-Auflistung** können Sie die Zeilenfelder im DetailsView-Steuerelement programmgesteuert verwalten.

> [!NOTE]
> Automatisch generierte Zeilenfelder werden der Fields-Auflistung nicht hinzugefügt.

## <a name="binding-to-data"></a>Bindung an Daten

Das DetailsView-Steuerelement kann an ein Datenquellensteuerelement gebunden werden, z. B. **SqlDataSource** oder AccessDataSource, oder an eine beliebige Datenquelle, die die System.Collections.IEnumerable-Schnittstelle implementiert, z. B. System.Data.DataView, System.Collections.ArrayList und System.Collections.Hashtable.

Verwenden Sie eine der folgenden Methoden, um das DetailsView-Steuerelement an den entsprechenden Datenquellentyp zu binden:

- Um eine Bindung an ein Datenquellensteuerelement zu erhalten, legen Sie die DataSourceID-Eigenschaft des DetailsView-Steuerelements auf den ID-Wert des Datenquellensteuerelements fest. Das DetailsView-Steuerelement bindet automatisch an das angegebene Datenquellensteuerelement. Dies ist die bevorzugte Methode zum Binden an Daten.
- Um eine Bindung an eine Datenquelle zu erhalten, die die **System.Collections.IEnumerable-Schnittstelle** implementiert, legen Sie programmgesteuert die DataSource-Eigenschaft des DetailsView-Steuerelements auf die Datenquelle fest, und rufen Sie dann die DataBind-Methode auf.

## <a name="security"></a>Sicherheit

Dieses Steuerelement kann verwendet werden, um Benutzereingaben anzuzeigen, die schädliche Clientskripts enthalten können. Überprüfen Sie alle Informationen, die von einem Client gesendet werden, auf ausführbares Skript, SQL-Anweisungen oder anderen Code, bevor Sie ihn in Ihrer Anwendung anzeigen. ASP.NET bietet eine Eingabeanforderungsvalidierungsfunktion, um Skript und HTML in Benutzereingaben zu blockieren.

## <a name="data-operations"></a>Datenvorgänge

Das DetailsView-Steuerelement bietet integrierte Funktionen, mit denen der Benutzer Elemente im Steuerelement aktualisieren, löschen, einfügen und durchblättern kann. Wenn das DetailsView-Steuerelement an ein Datenquellensteuerelement gebunden ist, kann das DetailsView-Steuerelement die Funktionen des Datenquellensteuerelements nutzen und automatische Aktualisierungs-, Lösch-, Einfüge- und Pagingfunktionen bereitstellen.

Das DetailsView-Steuerelement kann Unterstützung für Aktualisierungs-, Lösch-, Einfüge- und Pagingvorgänge mit anderen Datenquellentypen bereitstellen. Sie müssen jedoch die Implementierung für diese Vorgänge in einem geeigneten Ereignishandler bereitstellen.

Das DetailsView-Steuerelement kann automatisch ein **CommandField-Zeilenfeld** mit der Schaltfläche Bearbeiten, Löschen oder Neu hinzufügen, indem die Eigenschaften AutoGenerateEditButton, AutoGenerateDeleteButton oder AutoGenerateInsertButton auf **true**gesetzt werden. Im Gegensatz zur Schaltfläche Löschen (die den ausgewählten Datensatz sofort löscht) wechselt das DetailsView-Steuerelement in den Bearbeitungs- bzw. Einfügemodus. Im Bearbeitungsmodus wird die Schaltfläche Bearbeiten durch eine Schaltfläche "Aktualisieren" und "Abbrechen" ersetzt. Eingabesteuerelemente, die für den Datentyp des Felds geeignet sind (z. B. ein TextBox- oder ein CheckBox-Steuerelement), werden mit dem Wert eines Felds angezeigt, den der Benutzer ändern kann. Wenn Sie auf die Schaltfläche Aktualisieren klicken, wird der Datensatz in der Datenquelle aktualisiert, während durch Klicken auf die Schaltfläche Abbrechen alle Änderungen aufgehoben wird. Ebenso wird im Einfügemodus die Schaltfläche Neu durch eine Schaltfläche Einfügen und Abbrechen ersetzt, und leere Eingabesteuerelemente werden angezeigt, damit der Benutzer die Werte für den neuen Datensatz eingeben kann.

Das DetailsView-Steuerelement bietet eine Auslagerungsfunktion, mit der der Benutzer zu anderen Datensätzen in der Datenquelle navigieren kann. Wenn diese Option aktiviert ist, werden Seitennavigationssteuerelemente in einer Pagerzeile angezeigt. Um Paging zu aktivieren, legen Sie die AllowPaging-Eigenschaft auf **true**fest. Die Pagerzeile kann mit den Eigenschaften PagerStyle und PagerSettings angepasst werden.

## <a name="customizing-the-user-interface"></a>Anpassen der Benutzeroberfläche

Sie können die Darstellung des DetailsView-Steuerelements anpassen, indem Sie die Stileigenschaften für die verschiedenen Teile des Steuerelements festlegen. In der folgenden Tabelle sind die verschiedenen Stileigenschaften aufgeführt.

| **Style-Eigenschaft** | **Beschreibung** |
| --- | --- |
| Alternatingrowstyle | Die Stileinstellungen für die abwechselnden Datenzeilen im DetailsView-Steuerelement. Wenn diese Eigenschaft festgelegt ist, werden die Datenzeilen abwechselnd zwischen den RowStyle-Einstellungen und den **AlternatingRowStyle-Einstellungen** angezeigt. |
| CommandRowStyle | Die Stileinstellungen für die Zeile, die die integrierten Befehlsschaltflächen im DetailsView-Steuerelement enthält. |
| Editrowstyle | Die Stileinstellungen für die Datenzeilen, wenn sich das DetailsView-Steuerelement im Bearbeitungsmodus befindet. |
| Emptydatarowstyle | Die Stileinstellungen für die leere Datenzeile, die im DetailsView-Steuerelement angezeigt wird, wenn die Datenquelle keine Datensätze enthält. |
| Footerstyle | Die Stileinstellungen für die Fußzeile des DetailsView-Steuerelements. |
| Headerstyle | Die Stileinstellungen für die Kopfzeile des DetailsView-Steuerelements. |
| Insertrowstyle | Die Stileinstellungen für die Datenzeilen, wenn sich das DetailsView-Steuerelement im Einfügemodus befindet. |
| Pagerstyle | Die Stileinstellungen für die Pagerzeile des DetailsView-Steuerelements. |
| Rowstyle | Die Stileinstellungen für die Datenzeilen im DetailsView-Steuerelement. Wenn auch die **AlternatingRowStyle-Eigenschaft** festgelegt ist, werden die Datenzeilen abwechselnd zwischen den **RowStyle-Einstellungen** und den **AlternatingRowStyle-Einstellungen** angezeigt. |
| FieldHeaderStyle | Die Stileinstellungen für die Kopfspalte des DetailsView-Steuerelements. |

## <a name="events"></a>Ereignisse

Das DetailsView-Steuerelement stellt mehrere Ereignisse bereit, für die Sie programmieren können. Auf diese Weise können Sie eine benutzerdefinierte Routine ausführen, wenn ein Ereignis eintritt. In der folgenden Tabelle sind die vom DetailsView-Steuerelement unterstützten Ereignisse aufgeführt. Das DetailsView-Steuerelement erbt diese Ereignisse auch von seinen Basisklassen: DataBinding, DataBound, Disposed, Init, Load, PreRender und Render.

| **Event** | **Beschreibung** |
| --- | --- |
| Itemcommand | Tritt auf, wenn im DetailsView-Steuerelement auf eine Schaltfläche geklickt wird. |
| Itemcreated | Tritt auf, nachdem alle DetailsViewRow-Objekte im DetailsView-Steuerelement erstellt wurden. Dieses Ereignis wird häufig verwendet, um die Werte eines Datensatzes zu ändern, bevor er angezeigt wird. |
| ItemDeleted | Tritt auf, wenn auf eine Schaltfläche Löschen geklickt wird, aber nachdem das DetailsView-Steuerelement den Datensatz aus der Datenquelle gelöscht hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Löschvorgangs zu überprüfen. |
| ItemDeleting | Tritt auf, wenn auf eine Schaltfläche Löschen geklickt wird, aber bevor das DetailsView-Steuerelement den Datensatz aus der Datenquelle löscht. Dieses Ereignis wird häufig verwendet, um den Löschvorgang abzubrechen. |
| Iteminserted | Tritt auf, wenn auf eine Schaltfläche Einfügen geklickt wird, aber nachdem das DetailsView-Steuerelement den Datensatz eingefügt hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Einfügevorgangs zu überprüfen. |
| ItemEinfügen | Tritt auf, wenn auf eine Schaltfläche Einfügen geklickt wird, aber bevor das DetailsView-Steuerelement den Datensatz einfügt. Dieses Ereignis wird häufig verwendet, um den Einfügevorgang abzubrechen. |
| Itemupdated | Tritt auf, wenn auf eine Schaltfläche Aktualisieren geklickt wird, aber nachdem das DetailsView-Steuerelement die Zeile aktualisiert hat. Dieses Ereignis wird häufig verwendet, um die Ergebnisse des Aktualisierungsvorgangs zu überprüfen. |
| Itemupdating | Tritt auf, wenn auf eine Schaltfläche Aktualisieren geklickt wird, aber bevor das DetailsView-Steuerelement den Datensatz aktualisiert. Dieses Ereignis wird häufig verwendet, um den Aktualisierungsvorgang abzubrechen. |
| ModeChanged | Tritt auf, nachdem das DetailsView-Steuerelement die Modi geändert hat (Bearbeiten, Einfügen oder Schreibmodus). Dieses Ereignis wird häufig verwendet, um eine Aufgabe auszuführen, wenn das DetailsView-Steuerelement die Modi ändert. |
| ModeChanging | Tritt auf, bevor das DetailsView-Steuerelement die Modi ändert (Bearbeiten, Einfügen oder Schreibmodus). Dieses Ereignis wird häufig verwendet, um eine Modusänderung abzubrechen. |
| Pageindexchanged | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber nachdem das DetailsView-Steuerelement den Auslagerungsvorgang verarbeitet. Dieses Ereignis wird häufig verwendet, wenn Sie eine Aufgabe ausführen müssen, nachdem der Benutzer zu einem anderen Datensatz im Steuerelement navigiert. |
| PageIndexChanging | Tritt auf, wenn auf eine der Pagerschaltflächen geklickt wird, aber bevor das DetailsView-Steuerelement den Auslagerungsvorgang verarbeitet. Dieses Ereignis wird häufig verwendet, um den Auslagerungsvorgang abzubrechen. |

## <a name="the-menu-control"></a>Die Menüsteuerung

Die Menüsteuerung in ASP.NET 2.0 ist als voll funktionsfähiges Navigationssystem konzipiert. Es kann leicht an hierarchische Datenquellen wie siteMapDataSource gebunden werden.

Eine Menü-Steuerelementstruktur kann deklarativ oder dynamisch definiert werden und besteht aus einem einzelnen Stammknoten und einer beliebigen Anzahl von Unterknoten. Der folgende Code definiert deklarativ ein Menü für das Menüsteuerelement.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

Im obigen Beispiel ist der Home.aspx-Knoten der Stammknoten. Alle anderen Knoten sind innerhalb des Stammknotens auf verschiedenen Ebenen geschachtelt.

Es gibt zwei Arten von Menüs, die das Menüsteuerelement rendern kann. statische Menüs und dynamische Menüs. Statische Menüs bestehen aus Menüelementen, die immer sichtbar sind. Dynamische Menüs bestehen aus Menüelementen, die nur sichtbar sind, wenn der Benutzer mit der Maus darüber zeigt. Kunden können statische Menüs häufig mit deklarativ definierten Menüs und dynamischen Menüs mit Menüs verwechseln, die zur Laufzeit datengebunden sind. Tatsächlich haben dynamische und statische Menüs nichts mit der Methode der Grundgesamtheit zu tun. Die Begriffe *statisch* und *dynamisch* beziehen sich nur darauf, ob das Menü standardmäßig statisch oder nur angezeigt wird, wenn der Benutzer etwas tut.

Die **StaticDisplayLevels-Eigenschaft** wird verwendet, um zu konfigurieren, wie viele Ebenen des Menüs statisch sind und daher standardmäßig angezeigt werden. Im obigen Beispiel führt das Festlegen der **StaticDisplayLevels-Eigenschaft** auf den Wert 2 dazu, dass das Menü den Startknoten, den Music-Knoten und den Movies-Knoten statisch anzeigt. Alle anderen Knoten werden dynamisch angezeigt, wenn der Benutzer den Mauszeiger über den übergeordneten Knoten zeigt.

Die **MaximumDynamicDisplayLevels-Eigenschaft** konfiguriert die maximale Anzahl dynamischer Ebenen, die das Menü anzeigen kann. Alle dynamischen Menüs auf einer Ebene, die höher ist als der von der **MaximumDynamicDisplayLevels-Eigenschaft** angegebene Wert, werden verworfen.

> [!NOTE]
> Es ist fast sicher, dass Es situationen kann, in denen Menüs aufgrund der MaximumDynamicDisplayLevels-Eigenschaft nicht gerendert werden. Stellen Sie in diesen Fällen sicher, dass die Eigenschaft so eingestellt ist, dass die Kundenmenüs angezeigt werden können.

## <a name="data-binding-the-menu-control"></a>Datenbindung des Menüsteuerelements

Das Menüsteuerelement kann an eine beliebige hierarchische Datenquelle gebunden werden, z. B. an siteMapDataSource oder XMLDataSource. Die SiteMapDataSource ist die am häufigsten verwendete Methode für die Datenbindung an ein Menüsteuerelement, da sie aus der Datei Web.sitemap speist und ihr Schema eine bekannte API für das Menüsteuerelement bereitstellt. Die folgende Auflistung zeigt eine einfache Web.sitemap-Datei.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Beachten Sie, dass es nur ein Root siteMapNode-Element gibt, in diesem Fall das Home-Element. Für jeden siteMapNode können mehrere Attribute konfiguriert werden. Die am häufigsten verwendeten Attribute sind:

- **url** Gibt die URL an, die angezeigt werden soll, wenn ein Benutzer auf das Menüelement klickt. Wenn dieses Attribut nicht vorhanden ist, wird der Knoten einfach zurückgeschrieben, wenn darauf geklickt wird.
- **Titel** Gibt den Text an, der im Menüelement angezeigt wird.
- **Beschreibung** Wird als Dokumentation für den Knoten verwendet. Wird auch als QuickInfo angezeigt, wenn die Maus über dem Knoten bewegt wird.
- **siteMapFile** Ermöglicht verschachtelte Sitemaps. Dieses Attribut muss auf eine wohlgeformte ASP.NET Sitemapdatei verweisen.
- **Rollen** Ermöglicht die Steuerung des Erscheinungsbilds eines Knotens durch ASP.NET Sicherheitstrimmen.

Beachten Sie, dass diese Attribute zwar alle optional sind, das Verhalten des Menüs jedoch möglicherweise nicht das ist, was erwartet wird, wenn sie nicht angegeben werden. Wenn z. B. das *URL-Attribut* angegeben wird, das *Beschreibungsattribut* jedoch nicht, ist der Knoten nicht sichtbar, und es gibt keine Möglichkeit, zu der angegebenen URL zu navigieren.

## <a name="controlling-a-menus-operation"></a>Steuern eines Menus-Vorgangs

Es gibt mehrere Eigenschaften, die sich auf den Betrieb eines ASP.NET Menu-Steuerelements auswirken. Die **Orientation** Orientation-Eigenschaft, die **DisappearAfter-Eigenschaft,** die **StaticItemFormatString-Eigenschaft** und die **StaticPopoutImageUrl-Eigenschaft** sind nur einige davon.

- Die **Ausrichtung** kann entweder *horizontal* oder *vertikal* festgelegt werden und steuert, ob statische Menüelemente horizontal in einer Reihe oder vertikal angeordnet und übereinander gestapelt sind. Diese Eigenschaft wirkt sich nicht auf dynamische Menüs aus.
- Die **DisappearAfter-Eigenschaft** konfiguriert, wie lange ein dynamisches Menü sichtbar bleiben soll, nachdem die Maus von ihr entfernt wurde. Der Wert wird in Millisekunden angegeben und ist standardmäßig 500. Wenn Sie diese Eigenschaft auf den Wert -1 festlegen, wird das Menü nie automatisch ausgeblendet. In diesem Fall verschwindet das Menü nur, wenn der Benutzer außerhalb des Menüs klickt.
- Die **StaticItemFormatString-Eigenschaft** erleichtert die Konsistente Wortwahl in Ihrem Menüsystem. Wenn Sie diese *{0}* Eigenschaft angeben, sollten Sie anstelle der Beschreibung eingegeben werden, die in der Datenquelle angezeigt wird. Um beispielsweise den Menüpunkt aus Übung 1 zu verwenden, sagen Sie "Unsere {0} Produkte besuchen" usw., geben Sie "Unsere Seite besuchen" für den StaticItemFormatString an. Zur Laufzeit wird ASP.NET jedes {0} Vorkommen von durch die richtige Beschreibung für das Menüelement ersetzen.
- Die **StaticPopoutImageUrl-Eigenschaft** gibt das Bild an, das verwendet wird, um anzugeben, dass ein bestimmter Menüknoten über untergeordnete Knoten verfügt, auf die mit der Maus darauf zugegriffen werden kann. Dynamische Menüs verwenden weiterhin das Standardbild.

## <a name="templated-menu-controls"></a>Vorlagenmenüsteuerelemente

Das Menü-Steuerelement ist ein Vorlagensteuerelement und ermöglicht zwei verschiedene ItemTemplates. StaticItemTemplate und DynamicItemTemplate. Mithilfe dieser Vorlagen können Sie problemlos Serversteuerelemente oder Benutzersteuerelemente zu Ihren Menüs hinzufügen.

Um die Vorlagen in Visual Studio .NET zu bearbeiten, klicken Sie im Menü auf die Schaltfläche Smarttag, und wählen Sie entweder Vorlagen bearbeiten aus. Sie können dann zwischen der Bearbeitung der StaticItemTemplate oder der DynamicItemTemplate wählen.

Alle Steuerelemente, die der StaticItemTemplate hinzugefügt werden, werden im statischen Menü angezeigt, wenn die Seite geladen wird. Alle Steuerelemente, die dem DynamicItemTemplate hinzugefügt werden, werden in allen Popupmenüs angezeigt.

## <a name="menu-events"></a>Menü-Ereignisse

Das Menüsteuerelement verfügt über zwei Ereignisse, die für sie eindeutig sind. **MenuItemClicked** und **das MenuItemDatabound-Ereignis.**

Das MenuItemClicked-Ereignis wird ausgelöst, wenn auf ein Menüelement geklickt wird. Das MenuItemDatabound-Ereignis wird ausgelöst, wenn ein Menüelement datengebunden ist. Die **MenuEventArgs,** die an den Ereignishandler übergeben werden, ermöglicht den Zugriff auf das Menüelement über die Item-Eigenschaft.

## <a name="controlling-a-menus-appearance"></a>Steuern einer Menüsdarstellung

Sie können auch die Darstellung eines Menüsteuerelements mithilfe eines oder mehrerer der vielen Stile beeinflussen, die zum Formatieren von Menüs verfügbar sind. Dazu gehören **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**und **DynamicHoverStyle**. Diese Eigenschaften werden mit einer Standardzeichenfolge für HTML-Stil konfiguriert. Das Folgende wirkt sich z. B. auf den Stil für dynamische Menüs aus.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Wenn Sie einen der Hover-Stile verwenden, müssen &lt;&gt; Sie der Seite ein Head-Element hinzufügen, wobei das *runat-Element* auf *Server*festgelegt ist.

Menüsteuerelemente unterstützen auch die Verwendung von ASP.NET 2.0-Themen.

## <a name="the-treeview-control"></a>Das TreeView-Steuerelement

Das TreeView-Steuerelement zeigt Daten in einer baumähnlichen Struktur an. Wie beim Menüsteuerelement können Daten problemlos an eine beliebige hierarchische Datenquelle wie die SiteMapDataSource gebunden werden.

Die erste Frage, die Kunden wahrscheinlich über das TreeView-Steuerelement in ASP.NET 2.0 stellen, ist, ob es mit dem TreeView IE WebControl zusammenhängt, das für ASP.NET 1.x verfügbar war. Es ist nicht. Das ASP.NET 2.0 TreeView-Steuerelement wurde von Grund auf neu geschrieben und bietet eine deutliche Verbesserung gegenüber dem IE TreeView WebControl, das zuvor verfügbar war.

Ich werde nicht ins Detail gehen, wie ein TreeView-Steuerelement an eine Siteübersicht gebunden wird, da es genau auf die gleiche Weise wie das Menüsteuerelement ausgeführt wird. Das TreeView-Steuerelement weist jedoch einige deutliche Unterschiede in der Funktionsweise auf.

Standardmäßig wird ein TreeView-Steuerelement vollständig erweitert angezeigt. Um den Erweiterungsgrad beim ersten Laden zu ändern, ändern Sie die **ExpandDepth-Eigenschaft** des Steuerelements. Dies ist besonders wichtig in Fällen, in denen die TreeView beim Erweitern bestimmter Knoten datengebunden ist.

## <a name="databinding-the-treeview-control"></a>DataBinding des TreeView-Steuerelements

Im Gegensatz zum Menu-Steuerelement eignet sich treeView gut für die Verarbeitung großer Datenmengen. Daher ist die TreeView neben der Datenbindung an eine SiteMapDataSource oder XMLDataSource häufig Daten, die an ein DataSet oder andere relationale Daten gebunden sind. In Fällen, in denen das TreeView-Steuerelement an große Datenmengen gebunden ist, ist es am besten, nur an Daten zu binden, die tatsächlich im Steuerelement sichtbar sind. Sie können dann Daten an zusätzliche Daten binden, wenn TreeView-Knoten erweitert werden.

In diesen Fällen sollte die **PopulateOnDemand-Eigenschaft** der TreeView auf *true*festgelegt werden. Anschließend müssen Sie eine Implementierung für die **TreeNodePopulate-Methode** bereitstellen.

## <a name="data-binding-without-postback"></a>Datenbindung ohne PostBack

Beachten Sie, dass beim ersten Erweitern eines Knotens im vorherigen Beispiel die Seite erneut aktualisiert und aktualisiert wird. Das ist in diesem Beispiel kein Problem, aber Sie können sich vorstellen, dass es sich in einer Produktionsumgebung mit einer großen Datenmenge befindet. Ein besseres Szenario wäre ein Szenario, in dem die TreeView ihre Knoten weiterhin dynamisch auffüllen würde, jedoch ohne einen Beitrag zurück zum Server.

Durch Festlegen der **Eigenschaften PopulateNodesFromClient** und **PopulateOnDemand** auf true wird das ASP.NET TreeView-Steuerelement Knoten dynamisch ohne Postback auffüllen. Wenn der übergeordnete Knoten erweitert wird, wird eine XMLHttp-Anforderung vom Client ausgeführt, und das OnTreeNodePopulate-Ereignis wird ausgelöst. Der Server antwortet mit einer XML-Dateninsel, die dann verwendet wird, um die untergeordneten Knoten zu binden.

ASP.NET erstellt dynamisch den Clientcode, der diese Funktionalität implementiert. Die &lt;&gt; Skript-Tags, die das Skript enthalten, werden generiert und verweisen auf eine AXD-Datei. Die folgende Auflistung zeigt z. B. die Skriptverknüpfungen für den Skriptcode, der die XMLHttp-Anforderung generiert.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Wenn Sie die AXD-Datei oben in Ihrem Browser durchsuchen und öffnen, wird der Code angezeigt, der die XMLHttp-Anforderung implementiert. Diese Methode verhindert, dass Kunden die Skriptdatei ändern.

## <a name="controlling-the-operation-of-the-treeview-control"></a>Steuern des Betriebs des TreeView-Steuerelements

Das TreeView-Steuerelement verfügt über mehrere Eigenschaften, die sich auf den Betrieb des Steuerelements auswirken. Die offensichtlichsten Eigenschaften sind **ShowCheckBoxes**, **ShowExpandCollapse**und **ShowLines**.

Die **ShowCheckBoxes-Eigenschaft** wirkt sich darauf aus, ob Knoten beim Rendern ein Kontrollkästchen anzeigen. Die gültigen Werte für diese Eigenschaft sind **None**, **Root**, **Parent**, **Leaf**und **All**. Diese wirken sich wie folgt auf das TreeView-Steuerelement aus:

| **Eigenschaftswert** | **Wirkung** |
| --- | --- |
| Keine | Kontrollkästchen werden auf keinem Knoten angezeigt. Dies ist die Standardeinstellung. |
| Root | Ein Kontrollkästchen wird nur auf dem Stammknoten angezeigt. |
| Parent | Ein Kontrollkästchen wird nur auf den Knoten mit untergeordneten Knoten angezeigt. Bei diesen untergeordneten Knoten kann es sich um übergeordnete Knoten oder Blattknoten erzittern. |
| Blatt | Ein Kontrollkästchen wird nur auf den Knoten angezeigt, die keine untergeordneten Knoten haben. |
| All | Auf allen Knoten wird ein Kontrollkästchen angezeigt. |

Wenn Kontrollkästchen verwendet werden, gibt die **CheckedNodes-Eigenschaft** eine Auflistung von TreeView-Knoten zurück, die beim Postback aktiviert sind.

Die **ShowExpandCollapse-Eigenschaft** steuert die Darstellung des Expand/Collapse-Images neben Stamm- und übergeordneten Knoten. Wenn diese Eigenschaft auf **false**festgelegt ist, werden TreeView-Knoten als Hyperlinks gerendert und durch Klicken auf den Link erweitert/reduziert.

Die **ShowLines-Eigenschaft** steuert, ob Linien angezeigt werden, die übergeordnete Knoten mit untergeordneten Knoten verbinden. Wenn **false** (Standardeinstellung), werden keine Zeilen angezeigt. Wenn **true**, verwendet das TreeView-Steuerelement Zeilenbilder in dem Ordner, der von der **LineImagesFolder-Eigenschaft** angegeben wird.

Zum Anpassen der Darstellung von TreeView-Linien enthält Visual Studio .NET 2005 ein Linien-Designer-Tool. Sie können auf dieses Tool mit der Smarttag-Schaltfläche im TreeView-Steuerelement wie unten zugreifen.

![](data-bound-controls/_static/image1.jpg)

**Abbildung 1**

Wenn Sie die Menüoption **Linienbilder anpassen** auswählen, wird das Werkzeug Linien-Designer gestartet, mit dem Sie die Darstellung von TreeView-Linien konfigurieren können.

## <a name="treeview-events"></a>TreeView-Ereignisse

Das TreeView-Steuerelement weist die folgenden eindeutigen Ereignisse auf:

- SelectedNodeChanged tritt auf, wenn ein Knoten basierend auf der **SelectAction-Eigenschaft** ausgewählt wird.
- TreeNodeCheckChanged Tritt auf, wenn der Status der Knotenkontrollkästchen geändert wird.
- TreeNodeExpanded tritt auf, wenn ein Knoten basierend auf der **SelectAction-Eigenschaft** erweitert wird.
- TreeNodeCollapsed Tritt auf, wenn ein Knoten reduziert wird.
- TreeNodeDataBound Tritt auf, wenn ein Knoten datengebunden ist.
- TreeNodePopulate Tritt auf, wenn ein Knoten aufgefüllt wird.

Mit der **SelectAction-Eigenschaft** können Sie konfigurieren, welches Ereignis ausgelöst wird, wenn ein Knoten ausgewählt wird. Die SelectAction-Eigenschaft bietet die folgenden Aktionen:

- TreeNodeSelectAction.Expand hebt TreeNodeExpanded an, wenn der Knoten ausgewählt ist.
- TreeNodeSelectAction.None Löst kein Ereignis aus, wenn der Knoten ausgewählt ist.
- TreeNodeSelectAction.Select Löst das SelectedNodeChanged-Ereignis aus, wenn der Knoten ausgewählt ist.
- TreeNodeSelectAction.SelectExpand Löst sowohl das SelectedNodeChanged-Ereignis als auch das TreeNodeExpanded-Ereignis aus, wenn der Knoten ausgewählt ist.

## <a name="controlling-appearance-with-styles"></a>Steuern des Erscheinungsbilds mit Stilen

Das TreeView-Steuerelement bietet viele Eigenschaften zum Steuern der Darstellung des Steuerelements mit Stilen. Die folgenden Eigenschaften sind verfügbar:

| **Eigenschaftsname** | **Steuerelemente** |
| --- | --- |
| HoverNodeStyle | Steuert den Stil von Knoten, wenn die Maus über ihnen schwebt. |
| LeafNodeStyle | Steuert den Stil von Blattknoten. |
| Nodestyle | Steuert den Stil für alle Knoten. Bestimmte Knotenstile (z. B. LeafNodeStyle) überschreiben diesen Stil. |
| ParentNodeStyle | Steuert den Stil für alle übergeordneten Knoten. |
| RootNodeStyle | Steuert den Stil für den Stammknoten. |
| SelectedNodeStyle | Steuert den Stil für den ausgewählten Knoten. |

Jede dieser Eigenschaften ist schreibgeschützt. Sie geben jedoch jeweils ein **TreeNodeStyle-Objekt** zurück, und die Eigenschaften dieses Objekts können mithilfe des *Eigenschaftssubpropertyformats* geändert werden. Um beispielsweise die **ForeColor-Eigenschaft** des **SelectedNodeStyle**festzulegen, verwenden Sie die folgende Syntax:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Beachten Sie, dass das obige Tag nicht geschlossen ist. Denn wenn Sie die hier gezeigte deklarative Syntax verwenden, würden Sie die TreeViews-Knoten auch in den HTML-Code aufnehmen.

Die Stileigenschaften können auch im Code mithilfe des *Formats property.subproperty* angegeben werden. Um beispielsweise die **ForeColor-Eigenschaft** des **RootNodeStyle** im Code festzulegen, verwenden Sie die folgende Syntax:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Eine umfassende Liste der verschiedenen Stileigenschaften finden Sie in der MSDN-Dokumentation zum TreeNodeStyle-Objekt.

## <a name="the-sitemappath-control"></a>Das SiteMapPath-Steuerelement

Das SiteMapPath-Steuerelement stellt ein Navigationssteuerelement für ASP.NET-Krümelbereite bereit. Wie die anderen Navigationssteuerelemente können es leicht Daten sein, die an hierarchische Datenquellen wie SiteMapDataSource oder XmlDataSource gebunden sind.

Ein SiteMapPath-Steuerelement besteht aus SiteMapNodeItem-Objekten. Es gibt drei Knotentypen. der Stammknoten, die übergeordneten Knoten und der aktuelle Knoten. Der Stammknoten ist der Knoten am oberen Rand der hierarchischen Struktur. Der aktuelle Knoten stellt die aktuelle Seite dar. Alle anderen Knoten sind übergeordnete Knoten.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>Steuern des Betriebs des SiteMapPath-Steuerelements

Die Eigenschaften, die den Betrieb des SiteMapPath-Steuerelements steuern, lauten wie folgt:

| **Eigenschaft** | **Beschreibung der Eigenschaft** |
| --- | --- |
| ParentLevelsAngezeigt | Steuert, wie viele übergeordnete Knoten angezeigt werden. Der Standardwert ist -1, was keine Beschränkung der Anzahl der angezeigten übergeordneten Knoten vorschreibt. |
| Pathdirection | Steuert die Richtung des SiteMapPath. Gültige Werte sind RootToCurrent (Standard) und CurrentToRoot. |
| Pathseparator | Eine Zeichenfolge, die das Zeichen steuert, das Knoten in einem SiteMapPath-Steuerelement trennt. Der Standardwert ist :. |
| RenderCurrentNodeAsLink | Ein boolescher Wert, der steuert, ob der aktuelle Knoten als Verknüpfung gerendert wird. Die Standardeinstellung lautet „false“. |
| Skiplinktext | Unterstützt die Barrierefreiheit, wenn die Seite von Bildschirmleseprogrammen angezeigt wird. Mit dieser Eigenschaft können Bildschirmleser das SiteMapPath-Steuerelement überspringen. Um diese Funktion zu deaktivieren, legen Sie die Eigenschaft auf String.Empty fest. |

## <a name="templated-sitemappath-controls"></a>Vorlagen-SiteMapPath-Steuerelemente

Das SiteMapControl ist ein Vorlagensteuerelement, und als solches können Sie verschiedene Vorlagen für die Anzeige des Steuerelements definieren. Um Vorlagen in einem SiteMapPath-Steuerelement zu bearbeiten, klicken Sie im Steuerelement auf die Schaltfläche Smarttag, und wählen Sie Vorlagen bearbeiten im Menü aus. Hier wird das Menü SiteMapTasks wie unten gezeigt angezeigt, in dem Sie zwischen den verschiedenen verfügbaren Vorlagen wählen können.

![](data-bound-controls/_static/image2.jpg)

**Abbildung 2**

Die **NodeTemplate-Vorlage** bezieht sich auf jeden Knoten im SiteMapPath. Wenn der Knoten ein Stammknoten oder der aktuelle Knoten ist und ein **RootNodeTemplate** oder **CurrentNodeTemplate** konfiguriert ist, wird die NodeTemplate überschrieben.

## <a name="sitemappath-events"></a>SiteMapPath-Ereignisse

Das SiteMapPath-Steuerelement verfügt über zwei Ereignisse, die nicht von der Control-Klasse abgeleitet sind. das **ItemCreated-Ereignis** und das **ItemDataBound-Ereignis.** Das ItemCreated-Ereignis wird ausgelöst, wenn ein SiteMapPath-Element erstellt wird. ItemDataBound wird ausgelöst, wenn die DataBind-Methode während der Datenbindung eines SiteMapPath-Knotens aufgerufen wird. Ein **SiteMapNodeItemEventArgs-Objekt** bietet zugriff auf das spezifische SiteMapNodeItem über die Item-Eigenschaft.

## <a name="controlling-appearance-with-styles"></a>Steuern des Erscheinungsbilds mit Stilen

Die folgenden Formatvorlagen sind für die Formatierung eines SiteMapPath-Steuerelements verfügbar.

| **Eigenschaftsname** | **Steuerelemente** |
| --- | --- |
| CurrentNodeStyle | Steuert den Stil des Textes für den aktuellen Knoten. |
| RootNodeStyle | Steuert den Stil des Textes für den Stammknoten. |
| Nodestyle | Steuert den Stil des Textes für alle Knoten, vorausgesetzt, dass ein CurrentNodeStyle oder RootNodeStyle nicht angewendet wird. |

Die NodeStyle-Eigenschaft wird entweder durch currentNodeStyle oder RootNodeStyle überschrieben. Jede dieser Eigenschaften ist schreibgeschützt und gibt ein **Style-Objekt** zurück. Um die Darstellung eines Knotens mithilfe einer dieser Eigenschaften zu beeinflussen, müssen Sie die Eigenschaften des zurückgegebenen Style-Objekts festlegen. Der folgende Code ändert z. B. die forecolor-Eigenschaft des aktuellen Knotens.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

Die Eigenschaft kann auch programmgesteuert wie folgt angewendet werden:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Wenn eine Vorlage angewendet wird, wird die Formatvorlage nicht angewendet.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Lab 1: Konfigurieren eines ASP.NET Menüsteuerelements

1. Erstellen Sie eine neue Website.
2. Fügen Sie eine Sitemap-Datei hinzu, indem Sie Datei, Neu, Datei und SiteMap aus der Liste der Dateivorlagen auswählen.
3. Öffnen Sie die Siteübersicht (standardmäßig Web.sitemap) und ändern Sie sie so, dass sie wie die Liste unten aussieht. Die Seiten, mit denen Sie in der Siteübersichtsdatei verknüpfen, sind nicht wirklich vorhanden, aber das wird für diese Übung kein Problem sein.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Öffnen Sie das Standardwebformular in der Entwurfsansicht.
5. Fügen Sie im Navigationsabschnitt der Toolbox der Seite ein neues Menüsteuerelement hinzu.
6. Fügen Sie im Abschnitt Daten der Toolbox eine neue SiteMapDataSource hinzu. Die SiteMapDataSource verwendet automatisch die Web.sitemap-Datei in Ihrer Website. (Die Datei Web.sitemap *muss* sich im Stammordner der Website befinden.)
7. Klicken Sie auf das Menüsteuerelement, und klicken Sie dann auf die Schaltfläche Smarttag, um das Dialogfeld Menüaufgaben anzuzeigen.
8. Wählen Sie im Dropdowndown "Datenquelle auswählen" SiteMapDataSource1 aus.
9. Klicken Sie auf den AutoFormat-Link, und wählen Sie ein Format für das Menü aus.
10. Legen Sie im Eigenschaftenbereich die **StaticDisplayLevels-Eigenschaft** auf 2 fest. Das Menüsteuerelement sollte nun den Knoten "Startseite", "Produkte" und "Dienste" im Designer anzeigen.
11. Durchsuchen Sie die Seite in Ihrem Browser, um das Menü zu verwenden. (Da die Seiten, die Sie der Siteübersicht hinzugefügt haben, nicht vorhanden sind, wird beim Versuch, zu ihnen zu navigieren, ein Fehler angezeigt.)

Experimentieren Sie mit dem Ändern der StaticDisplayLevels- und der MaximumDynamicDisplayLevels-Eigenschaften, und erfahren Sie, wie sich das Menü auswirkt.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Lab 2: Dynamisches Binden eines TreeView-Steuerelements

In dieser Übung wird davon ausgegangen, dass SQL Server lokal ausgeführt wird und dass die Northwind-Datenbank auf der SQL Server-Instanz vorhanden ist. Wenn diese Bedingungen nicht erfüllt sind, ändern Sie bitte die Verbindungszeichenfolge im Beispiel. Beachten Sie, dass Sie möglicherweise auch die SQL Server-Authentifizierung anstelle einer vertrauenswürdigen Verbindung angeben müssen.

1. Erstellen Sie eine neue Website.
2. Wechseln Sie zur Codeansicht für Default.aspx, und ersetzen Sie den gesamten Code durch den unten aufgeführten Code. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Speichern Sie die Seite als treeview.aspx.
4. Durchsuchen Sie die Seite.
5. Wenn die Seite zum ersten Mal angezeigt wird, zeigen Sie die Quelle der Seite in Ihrem Browser an. Beachten Sie, dass nur die sichtbaren Knoten an den Client gesendet wurden.
6. Klicken Sie auf das Pluszeichen neben einem beliebigen Knoten.
7. Zeigen Sie die Quelle auf der Seite erneut an. Beachten Sie, dass die neu angezeigten Knoten jetzt vorhanden sind.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Lab 3: Detailansicht und Bearbeiten von Daten mithilfe einer GridView und DetailsView

1. Erstellen Sie eine neue Website.
2. Fügen Sie der Website eine neue web.config hinzu.
3. Fügen Sie der Datei web.config eine Verbindungszeichenfolge hinzu, wie unten gezeigt: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > Möglicherweise müssen Sie die Verbindungszeichenfolge basierend auf Ihrer Umgebung ändern.
4. Speichern und schließen Sie die Datei "web.config".
5. Öffnen Sie Default.aspx, und fügen Sie ein neues SqlDataSource-Steuerelement hinzu.
6. Ändern Sie die ID des SqlDataSource-Steuerelements in **Produkte**.
7. Klicken Sie im Menü **SqlDataSource Tasks** auf **Datenquelle konfigurieren**.
8. Wählen Sie Im Dropdowndown der Verbindung die Option **Nordwind** aus, und klicken Sie auf Weiter.
9. Wählen Sie **Produkte** aus der Dropdown-Liste **Name** aus, und aktivieren Sie die Kontrollkästchen **ProductID**, **ProductName**, **UnitPrice**und **UnitsInStock** wie unten gezeigt. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. Klicken Sie auf **Weiter**.
11. Klicken Sie auf **Fertig stellen**.
12. Wechseln Sie zur Quellansicht, und untersuchen Sie den generierten Code. Beachten Sie **selectCommand**, **DeleteCommand**, **InsertCommand**und **UpdateCommand,** die dem SqlDataSource-Steuerelement hinzugefügt wurden. Beachten Sie auch die Parameter, die hinzugefügt wurden.
13. Wechseln Sie zur Entwurfsansicht, und fügen Sie der Seite ein neues GridView-Steuerelement hinzu.
14. Wählen Sie **Produkte** aus der Dropdownliste **Datenquelle auswählen** aus.
15. Aktivieren Sie **Paging** aktivieren und **Auswahl aktivieren,** wie unten gezeigt. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. Klicken Sie auf den Link **Spalten bearbeiten,** und stellen Sie sicher, dass **Felder automatisch generiert** aktiviert sind.
17. Klicken Sie auf **OK**.
18. Wenn das GridView-Steuerelement ausgewählt ist, klicken Sie im Eigenschaftenbereich auf die Schaltfläche neben der **DataKeyNames-Eigenschaft.**
19. Wählen Sie **ProductID** aus der Liste **&gt;** **Verfügbare Datenfelder** aus, und klicken Sie auf die Schaltfläche, um sie hinzuzufügen.
20. Klicken Sie auf OK.
21. Fügen Sie der Seite ein neues SqlDataSource-Steuerelement hinzu.
22. Ändern Sie die ID des SqlDataSource-Steuerelements in **Details**.
23. Wählen Sie im Menü SqlDataSource Tasks die Option **Datenquelle konfigurieren**aus.
24. Wählen Sie **Northwind** aus der Dropdown-Liste aus und klicken Sie auf **Weiter**.
25. Wählen Sie <strong>Produkte</strong> aus der <strong> \<Dropdown-Liste <strong>Name</strong> aus, und aktivieren Sie das Kontrollkästchen /strong>* im Listenfeld <strong>Spalten.</strong>
26. Klicken Sie auf die **Schaltfläche WHERE.**
27. Wählen Sie **ProductID** aus der Dropdownliste **Spalte** aus.
28. Wählen **=** Sie in der Dropdown-Liste Operator aus.
29. Wählen Sie **Steuerelement** aus der Dropdownliste **Quelle** aus.
30. Wählen Sie **GridView1** aus der Dropdownliste **Control ID** aus.
31. Klicken Sie auf die Schaltfläche **Hinzufügen,** um die WHERE-Klausel hinzuzufügen.
32. Klicken Sie auf **OK**.
33. Klicken Sie auf die Schaltfläche **Erweitert,** und aktivieren Sie das Kontrollkästchen **INSERT-, UPDATE- und DELETE-Anweisungen** generieren.
34. Klicken Sie auf **OK**.
35. Klicken Sie auf **Weiter** und klicken Sie auf **Fertig**stellen .
36. Fügen Sie der Seite ein DetailsView-Steuerelement hinzu.
37. Wählen Sie im Dropdowndowndropdown **Datenquelle auswählen** **Details**aus.
38. Aktivieren Sie das Kontrollkästchen **Editing aktivieren,** wie unten gezeigt. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Speichern Sie die Seite, und durchsuchen Sie Default.aspx.
40. Klicken Sie auf den Link **Auswählen** neben verschiedenen Datensätzen, um die DetailsView-Aktualisierung automatisch anzuzeigen.
41. Klicken Sie im DetailsView-Steuerelement auf den Link **Bearbeiten.**
42. Nehmen Sie eine Änderung am Datensatz vor, und klicken Sie auf **Aktualisieren**.
