---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: Batch löschen (c#) | Microsoft-Dokumentation
author: rick-anderson
description: Erfahren Sie, wie Sie mehrere Datenbankdatensätze in einem einzigen Vorgang löschen. In der UI-Schicht erstellen wir auf eine verbesserte GridView erstellt in einem früheren Zeitpunkt tut...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: da913e08cd007a89b659f87ef30ea15160692c09
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59416947"
---
# <a name="batch-deleting-c"></a>Löschen in Batches (C#)

durch [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Code herunterladen](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) oder [PDF-Datei herunterladen](batch-deleting-cs/_static/datatutorial65cs1.pdf)

> Erfahren Sie, wie Sie mehrere Datenbankdatensätze in einem einzigen Vorgang löschen. In der UI-Schicht erstellen wir auf eine verbesserte GridView, die in einem früheren Tutorial erstellt haben. In der Datenzugriffsebene umschließen wir die mehrere Löschvorgänge in einer Transaktion, um sicherzustellen, dass alle Löschvorgänge erfolgreich ausgeführt werden oder ein alle Löschvorgänge Rollback.


## <a name="introduction"></a>Einführung

Die [vorherigen Lernprogramm](batch-updating-cs.md) haben, wie Sie einen Batch bearbeiten unter Verwendung eines vollständig bearbeitbare GridView-Schnittstelle erstellen. In Situationen, in dem Benutzer werden häufig viele Datensätze gleichzeitigen bearbeiten, eine Schnittstelle für die Batchverarbeitung erfordert wesentlich weniger Postbacks und Tastatur, Maus Kontext-Schalter, wodurch die Endbenutzer-s-Effizienz verbessert. Diese Methode eignet sich auf ähnliche Weise für Seiten, bei denen es üblich, dass Benutzer mehrere Datensätze in einer Aktion zu löschen ist.

Jeder Benutzer, der einen online-e Mailclient verwendet hat ist bereits mit einer der am häufigsten verwendeten Batches löschen Schnittstellen vertraut sind: ein Kontrollkästchen in den einzelnen Zeilen in einem Raster mit einer entsprechenden alle markierte Elemente löschen Schaltfläche (siehe Abbildung 1). In diesem Tutorial ist recht kurz da wir haben bereits erfolgt alle aufwändigen arbeiten in vorherigen Tutorials zum Erstellen sowohl die webbasierte Schnittstelle und eine Methode, um eine Reihe von Datensätzen als einzelnen atomaren Vorgang zu löschen. In der [Hinzufügen einer GridView-Spalte mit Kontrollkästchen](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) Tutorial wir einer GridView-Ansicht, mit einer Spalte mit Kontrollkästchen und in erstellt der [Umschließen von Datenbankänderungen innerhalb einer Transaktion](wrapping-database-modifications-within-a-transaction-cs.md) Tutorial, die wir erstellt, eine Methode in haben die BLL, die eine Transaktion, zum Löschen verwenden würden einer `List<T>` von `ProductID` Werte. In diesem Tutorial haben wir bauen auf und merge unserer früheren Erfahrungen bei der um einen funktionierenden Batch löschen Beispiel zu erstellen.


[![Jede Zeile enthält ein Kontrollkästchen](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)

**Abbildung 1**: Jede Zeile enthält ein Kontrollkästchen ([klicken Sie, um das Bild in voller Größe anzeigen](batch-deleting-cs/_static/image2.png))


## <a name="step-1-creating-the-batch-deleting-interface"></a>Schritt 1: Erstellen den Batch, die Schnittstelle wird gelöscht.

Da wir bereits den löschen-Schnittstelle in Batch erstellt den [Hinzufügen einer GridView-Spalte mit Kontrollkästchen](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) Tutorial, wir können einfach kopieren, damit `BatchDelete.aspx` anstelle von Grund auf neu erstellen. Öffnen Sie zunächst die `BatchDelete.aspx` auf der Seite die `BatchData` Ordner und die `CheckBoxField.aspx` auf der Seite die `EnhancedGridView` Ordner. Von der `CheckBoxField.aspx` Seite, wechseln Sie zur Quellansicht, und kopieren Sie das Markup zwischen den `<asp:Content>` tags wie in Abbildung 2 dargestellt.


[![Kopieren Sie CheckBoxField.aspx deklarative Markup in die Zwischenablage](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)

**Abbildung 2**: Kopieren Sie deklarativen Markup `CheckBoxField.aspx` in die Zwischenablage ([klicken Sie, um das Bild in voller Größe anzeigen](batch-deleting-cs/_static/image4.png))


Navigieren Sie anschließend auf die Datenquellensicht `BatchDelete.aspx` , und fügen Sie den Inhalt der Zwischenablage in die `<asp:Content>` Tags. Auch kopieren und fügen Sie den Code aus, in der CodeBehind-Klasse in `CheckBoxField.aspx.cs` , in der CodeBehind-Klasse in `BatchDelete.aspx.cs` (der `DeleteSelectedProducts` Schaltfläche s `Click` -Ereignishandler der `ToggleCheckState` -Methode, und die `Click` -Ereignishandler für die `CheckAll` und `UncheckAll` Schaltflächen). Nach dem Kopieren über diesen Inhalt, der `BatchDelete.aspx` Seite s-Code-Behind-Klasse sollte den folgenden Code enthalten:


[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

Nach dem Kopieren über die deklarativen Markup und Quellcode in Ruhe testen `BatchDelete.aspx` es über einen Browser anzeigen. Daraufhin sollte eine GridView, die die ersten zehn Produkte in einer GridView-Ansicht, in dem jede Zeile mit dem Auflisten der Produktname s, Kategorie und Preis sowie ein Kontrollkästchen auflisten. Es sollten drei Schaltflächen vorhanden sein: Überprüft alle, alle deaktivieren und löschen Sie die ausgewählten Produkte. Alle Kontrollkästchen, auf die Schaltfläche "alle" ausgewählt werden, während alle deaktivieren Sie alle Kontrollkästchen löscht. Löschen ausgewählter Produkte auf wird eine Meldung angezeigt, die auflistet der `ProductID` Werte der ausgewählten Produkte, aber nicht tatsächlich die Produkte gelöscht werden.


[![Die Schnittstelle aus CheckBoxField.aspx wurde auf BatchDeleting.aspx verschoben](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)

**Abbildung 3**: Die Schnittstelle aus `CheckBoxField.aspx` wurde in `BatchDeleting.aspx` ([klicken Sie, um das Bild in voller Größe anzeigen](batch-deleting-cs/_static/image6.png))


## <a name="step-2-deleting-the-checked-products-using-transactions"></a>Schritt 2: Löschen die aktivierten Produkte, die mithilfe von Transaktionen

Mit dem Batch, löschen die Schnittstelle, die erfolgreich kopiert, um `BatchDeleting.aspx`, bleibt dann so aktualisieren den Code, damit die ausgewählten Produkte löschen-Schaltfläche mit aktivierten Produkte löscht die `DeleteProductsWithTransaction` -Methode in der die `ProductsBLL` Klasse. Dieser Methode hinzugefügt, die der [Umschließen von Datenbankänderungen innerhalb einer Transaktion](wrapping-database-modifications-within-a-transaction-cs.md) Tutorial akzeptiert als Eingabe eine `List<T>` von `ProductID` Werte und löscht die jeweils entsprechenden `ProductID` innerhalb des Bereichs einer die Transaktion.

Die `DeleteSelectedProducts` Schaltfläche s `Click` -Ereignishandler verwendet derzeit die folgenden `foreach` Schleife zum Durchlaufen der einzelnen GridView-Zeile:


[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

Für jede Zeile die `ProductSelector` Kontrollkästchen-Websteuerelements ist programmgesteuert auf die verwiesen wird. Wenn diese Option aktiviert ist, die Zeile s `ProductID` aus abgerufen wird die `DataKeys` Auflistung und die `DeleteResults` Bezeichnung s `Text` -Eigenschaft aktualisiert, um das Einschließen einer Meldung, dass die Zeile zum Löschen ausgewählt wurde.

Der obige Code tatsächlich löscht keine Einträge wie den Aufruf der `ProductsBLL` s-Klasse `Delete` Methode auskommentiert ist. Waren diese Delete-Logik angewendet werden, würde der Code die Produkte löschen, aber nicht innerhalb einer atomaren Operation. Das heißt, wenn die ersten Paar Löschvorgänge in der Sequenz war erfolgreich, aber Fehler bei der eine höhere Version (vielleicht aufgrund einer Verletzung der foreign Key-Einschränkung), würde eine Ausnahme ausgelöst werden, jedoch dieser Produkte, die bereits gelöscht. gelöschte bleibt.

Um die Unteilbarkeit gewährleisten zu können, müssen wir stattdessen die `ProductsBLL` Klasse s `DeleteProductsWithTransaction` Methode. Da diese Methode eine Liste der akzeptiert `ProductID` Werte müssen wir zunächst kompilieren, diese Liste, aus dem Raster und klicken Sie dann als Parameter übergeben. Erstellen wir zunächst eine Instanz von einem `List<T>` des Typs `int`. In der `foreach` Schleife wir die ausgewählten Produkte hinzufügen müssen `ProductID` Werte dieser `List<T>`. Nach der Schleife dies `List<T>` übergeben werden muss, um die `ProductsBLL` Klasse s `DeleteProductsWithTransaction` Methode. Update der `DeleteSelectedProducts` Schaltfläche s `Click` -Ereignishandler durch den folgenden Code:


[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

Der aktualisierte Code erstellt eine `List<T>` des Typs `int` (`productIDsToDelete`) und füllt sie mit der `ProductID` zu löschende Werte. Nach der `foreach` Schleife, es ist mindestens ein Produkt ausgewählt, die `ProductsBLL` s-Klasse `DeleteProductsWithTransaction` Methode aufgerufen wird, und übergeben Sie dieser Liste. Die `DeleteResults` Bezeichnung wird auch angezeigt, und die Daten erneut an die GridView gebunden, (, damit der neu gelöschte Datensätze als Zeilen im Raster nicht mehr angezeigt werden).

Abbildung 4 zeigt die GridView, nachdem eine Anzahl von Zeilen zum Löschen ausgewählt wurden. Abbildung 5 zeigt den Bildschirm sofort, nachdem die ausgewählten Produkte löschen-Schaltfläche geklickt wurde. Beachten Sie, dass in Abbildung 5 die `ProductID` Werte von der gelöschten Datensätze werden angezeigt, in der Beschriftung unter GridView und die Zeilen sind nicht mehr in den GridView-Ansicht.


[![Die ausgewählten Produkte werden gelöscht](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)

**Abbildung 4**: Die ausgewählten Produkte gelöscht werden ([klicken Sie, um das Bild in voller Größe anzeigen](batch-deleting-cs/_static/image8.png))


[![Gelöschte Werte Produkte "ProductID" unterhalb der GridView aufgeführt](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)

**Abbildung 5**: Die Produkte gelöscht `ProductID` Werte sind unter der GridView aufgeführt ([klicken Sie, um das Bild in voller Größe anzeigen](batch-deleting-cs/_static/image10.png))


> [!NOTE]
> So testen Sie die `DeleteProductsWithTransaction` Unteilbarkeit s-Methode, Manuelles Hinzufügen eines Eintrags für ein Produkt in der `Order Details` Tabelle, und klicken Sie dann versuchen, dieses Produkt (zusammen mit anderen) zu löschen. Beim Versuch, das Produkt mit einer zugeordneten Auftrag zu löschen, aber beachten Sie, wie die anderen ausgewählten Produkte löschungen Rollback ausgeführt werden, erhalten Sie eine Verletzung der foreign Key-Einschränkung.


## <a name="summary"></a>Zusammenfassung

Erstellen einen Batch löschen Schnittstelle umfasst das Hinzufügen einer GridView-Ansicht mit einer Spalte mit Kontrollkästchen und eine Schaltfläche-Websteuerelement, wenn auf Sie geklickt werden alle ausgewählten Zeilen als einen einzigen atomaren Vorgang gelöscht. In diesem Tutorial erstellt es eine solche Schnittstelle Arbeit, die in vorherigen Tutorials zwei von Datenfehlern [Hinzufügen einer GridView-Spalte mit Kontrollkästchen](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) und [Umschließen von Datenbankänderungen innerhalb einer Transaktion](wrapping-database-modifications-within-a-transaction-cs.md). Im ersten Tutorial wir einer GridView-Ansicht mit einer Spalte mit Kontrollkästchen erstellt und im letzten Fall, die wir implementiert einer Methode in der BLL, die beim Übergeben einer `List<T>` von `ProductID` Werte gelöscht haben, alle innerhalb des Bereichs einer Transaktion.

Im nächsten Tutorial erstellen wir eine Schnittstelle zum Ausführen von batcheinfügungen.

Viel Spaß beim Programmieren!

## <a name="about-the-author"></a>Der Autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), Autor von sieben Büchern zu ASP/ASP.NET und Gründer von [4GuysFromRolla.com](http://www.4guysfromrolla.com), arbeitet mit Microsoft-Web-Technologien seit 1998. Er ist als ein unabhängiger Berater, Schulungsleiter und Autor. Sein neueste Buch wird [*Sams Schulen selbst ASP.NET 2.0 in 24 Stunden*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Er ist unter [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) oder über seinen Blog finden Sie unter [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Besonderen Dank an

Diese tutorialreihe wurde durch viele hilfreiche Reviewer überprüft. Führendes Prüfer für dieses Tutorial wurden Hilton Giesenow und Teresa Murphy. Meine zukünftigen MSDN-Artikeln überprüfen möchten? Wenn dies der Fall ist, löschen Sie mir eine Linie an [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Zurück](batch-updating-cs.md)
> [Weiter](batch-inserting-cs.md)
