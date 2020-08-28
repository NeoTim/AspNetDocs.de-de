---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
title: Effizientes Paging durch große Datenmengen (c#) | Microsoft-Dokumentation
author: rick-anderson
description: Die Standard-Paging-Option eines Daten Präsentations Steuer Elements ist nicht geeignet, wenn Sie mit großen Datenmengen arbeiten, da das zugrunde liegende Datenquellen-Steuerelement abgerufen wird...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 59c01998-9326-4ecb-9392-cb9615962140
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 154bcfeed8e64869b7c32d35b4fb05b6e611dadc
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045272"
---
# <a name="efficiently-paging-through-large-amounts-of-data-c"></a>Effizientes Auslagern von großen Datenmengen (C#)

von [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Beispiel-app herunterladen](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_CS.exe) oder [PDF herunterladen](efficiently-paging-through-large-amounts-of-data-cs/_static/datatutorial25cs1.pdf)

> Die Standard-Paging-Option eines Daten Präsentations Steuer Elements ist nicht geeignet, wenn Sie mit großen Datenmengen arbeiten, da das zugrunde liegende Datenquellen-Steuerelement alle Datensätze abruft, auch wenn nur eine Teilmenge der Daten angezeigt wird. In diesen Fällen müssen wir das benutzerdefinierte Paging aktivieren.

## <a name="introduction"></a>Einführung

Wie bereits im vorherigen Tutorial erläutert, kann das Paging auf eine von zwei Arten implementiert werden:

- Das **Standardpaging** kann implementiert werden, indem Sie einfach die Option Paging aktivieren im Smarttags des dateiweb-Steuer Elements aktivieren. Wenn Sie jedoch eine Datenseite anzeigen, ruft ObjectDataSource *alle* Datensätze ab, auch wenn nur eine Teilmenge der Daten auf der Seite angezeigt wird.
- Durch **benutzerdefiniertes Paging** wird die Leistung der Standard Auslagerung verbessert, indem nur die Datensätze aus der Datenbank abgerufen werden, die für die vom Benutzer angeforderte Datenseite angezeigt werden müssen. das benutzerdefinierte Paging umfasst jedoch etwas mehr Aufwand für die Implementierung als die Standard Auslagerung.

Aufgrund der einfachen Implementierung aktivieren Sie ein Kontrollkästchen, und Sie haben es wieder getan! Standard-Paging ist eine attraktive Option. Der naive Ansatz beim Abrufen aller Datensätze ist jedoch eine unplausible Wahl, wenn Sie durch ausreichend große Datenmengen oder für Standorte mit vielen gleichzeitigen Benutzern Paging. In diesen Fällen müssen wir das benutzerdefinierte Paging aktivieren, um ein reaktionsfähiges System bereitzustellen.

Die Herausforderung von benutzerdefiniertem Paging besteht darin, eine Abfrage zu schreiben, die den genauen Satz von Datensätzen zurückgibt, die für eine bestimmte Datenseite benötigt werden. Glücklicherweise stellt Microsoft SQL Server 2005 ein neues Schlüsselwort für die Rangfolge der Ergebnisse bereit, das es uns ermöglicht, eine Abfrage zu schreiben, mit der die richtige Teilmenge der Datensätze effizient abgerufen werden kann. In diesem Tutorial erfahren Sie, wie Sie das neue Schlüsselwort "SQL Server 2005" verwenden, um benutzerdefiniertes Paging in einem GridView-Steuerelement zu implementieren. Obwohl die Benutzeroberfläche für benutzerdefiniertes Paging identisch mit der für die Standard Auslagerung ist, kann das Ausführen eines Einzel Vorgangs von einer Seite zur nächsten mithilfe von benutzerdefiniertem Paging mehrere Größenordnungen beschleunigen als die standardpaginierung.

> [!NOTE]
> Der genaue Leistungsgewinn, der durch das benutzerdefinierte Paging festgestellt wird, hängt von der Gesamtzahl der Datensätze ab, die durch den Datenbankserver eingefügt werden. Am Ende dieses Tutorials betrachten wir einige grobe Metriken, die die Vorteile der Leistung veranschaulichen, die durch das benutzerdefinierte Paging erzielt werden.

## <a name="step-1-understanding-the-custom-paging-process"></a>Schritt 1: Grundlegendes zum benutzerdefinierten pagingprozess

Beim Paging durch Daten sind die auf einer Seite angezeigten exakten Datensätze abhängig von der angeforderten Datenmenge und der Anzahl der pro Seite angezeigten Datensätze. Stellen Sie sich beispielsweise vor, dass Sie die 81-Produkte durchlaufen möchten, die 10 Produkte pro Seite anzeigen. Wenn Sie die erste Seite anzeigen, benötigen wir die Produkte 1 bis 10. beim Anzeigen der zweiten Seite interessieren wir uns für die Produkte 11 bis 20 usw.

Es gibt drei Variablen, die vorgeben, welche Datensätze abgerufen werden müssen und wie die pagingschnittstelle gerendert werden soll:

- **Zeilen Anfang Index** : der Index der ersten Zeile in der Datenseite, die angezeigt werden soll. Dieser Index kann berechnet werden, indem der Seitenindex von den Datensätzen multipliziert wird, die pro Seite angezeigt werden sollen. Wenn z. b. für die erste Seite (deren Seitenindex den Wert 0 hat) die Datensätze 10 gleichzeitig durchsucht werden, lautet der Start Zeilen Index 0 \* 10 + 1 oder 1. bei der zweiten Seite (deren Seitenindex 1 ist) ist der Start Zeilen Index 1 \* 10 + 1 oder 11.
- **Maximale Zeilen** Anzahl die maximale Anzahl der Datensätze, die pro Seite angezeigt werden sollen. Diese Variable wird als maximale Anzahl von Zeilen bezeichnet, da für die letzte Seite möglicherweise weniger Datensätze als die Seitengröße zurückgegeben werden. Wenn Sie z. b. das Paging durch die 81 Produkte 10 Datensätze pro Seite durchlaufen, wird auf der neunten und letzten Seite nur ein Datensatz angezeigt. Keine Seite zeigt jedoch mehr Datensätze an als der Wert für die maximale Zeilen Anzahl.
- **Gesamt** Anzahl der Datensätze die Gesamtanzahl der Datensätze, die durchlaufen werden. Diese Variable ist zwar nicht erforderlich, um zu bestimmen, welche Datensätze für eine bestimmte Seite abgerufen werden sollen, aber es wird die Paging-Schnittstelle vorgegeben. Wenn z. b. 81 Produkte durchlaufen werden, weiß die Paging-Schnittstelle, dass neun Seitenzahlen in der Pagingbenutzeroberfläche angezeigt werden.

Beim standardmäßigen Paging wird der Start Zeilen Index als Produkt des Seiten Indexes und der Seitengröße Plus 1 berechnet, während die maximale Zeilen Anzahl einfach die Seitengröße ist. Da bei der Standard Auslagerung alle Datensätze aus der Datenbank abgerufen werden, wenn eine Datenseite gerendert wird, ist der Index für jede Zeile bekannt, sodass der Übergang zur Zeile für den Zeilen Index zu einer trivialen Aufgabe wird. Außerdem ist die Gesamtanzahl der Datensätze sofort verfügbar, da Sie einfach die Anzahl der Datensätze in der Datentabelle (oder das Objekt, das zum Speichern der Daten Bank Ergebnisse verwendet wird) enthält.

Bei Angabe der Variablen "Start Row Index" und "Maximum rows" muss eine benutzerdefinierte pagingimplementierung nur die genaue Teilmenge der Datensätze zurückgeben, beginnend beim Start Zeilen Index und die maximale Zeilen Anzahl von Datensätzen. Das benutzerdefinierte Paging bietet zwei Herausforderungen:

- Wir müssen in der Lage sein, jeder Zeile in den auslagerbaren Daten einen Zeilen Index effizient zuzuordnen, damit wir mit dem Zurückgeben von Datensätzen am angegebenen Start Zeilen Index beginnen können.
- Wir müssen die Gesamtzahl der Datensätze angeben, die durchlaufen werden.

In den nächsten beiden Schritten untersuchen wir das SQL-Skript, das für die Beantwortung dieser beiden Probleme erforderlich ist. Zusätzlich zum SQL-Skript müssen auch Methoden in Dal und BLL implementiert werden.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>Schritt 2: Zurückgeben der Gesamtanzahl von Datensätzen, die durchlaufen werden

Bevor wir untersuchen, wie die genaue Teilmenge der Datensätze für die anzuzeigende Seite abgerufen wird, sehen Sie sich zunächst an, wie die Gesamtanzahl der Datensätze zurückgegeben werden soll, die durchlaufen werden. Diese Informationen sind erforderlich, um die Auslagerungs Benutzeroberfläche ordnungsgemäß zu konfigurieren. Die Gesamtanzahl der Datensätze, die von einer bestimmten SQL-Abfrage zurückgegeben werden, kann mithilfe der [ `COUNT` Aggregatfunktion](https://msdn.microsoft.com/library/ms175997.aspx)abgerufen werden. Um z. b. die Gesamtanzahl der Datensätze in der Tabelle zu ermitteln `Products` , können wir die folgende Abfrage verwenden:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample1.sql)]

Fügen Sie der dal eine Methode hinzu, die diese Informationen zurückgibt. Insbesondere erstellen wir eine dal-Methode namens `TotalNumberOfProducts()` , die die `SELECT` oben gezeigte Anweisung ausführt.

Öffnen Sie zunächst die `Northwind.xsd` typisierte Datasetdatei im `App_Code/DAL` Ordner. Klicken Sie anschließend im Designer mit der rechten Maustaste auf den, `ProductsTableAdapter` und wählen Sie Abfrage hinzufügen aus. Wie bereits in den vorherigen Tutorials gezeigt, können wir der dal eine neue Methode hinzufügen, die, wenn Sie aufgerufen wird, eine bestimmte SQL-Anweisung oder gespeicherte Prozedur ausführt. Wie bei unseren TableAdapter-Methoden in vorherigen Tutorials haben Sie sich dafür entschieden, eine Ad-hoc-SQL-Anweisung zu verwenden.

![Verwenden einer Ad-hoc-SQL-Anweisung](efficiently-paging-through-large-amounts-of-data-cs/_static/image1.png)

**Abbildung 1**: Verwenden einer Ad-hoc-SQL-Anweisung

Auf dem nächsten Bildschirm können Sie angeben, welche Art von Abfrage erstellt werden soll. Da diese Abfrage einen einzelnen Skalarwert zurückgibt, wird durch die Gesamtzahl der Datensätze in der `Products` Tabelle die-Option zurückgegeben `SELECT` , die eine Option für das debugwerten zurückgibt

![Konfigurieren der Abfrage für die Verwendung einer SELECT-Anweisung, die einen einzelnen Wert zurückgibt](efficiently-paging-through-large-amounts-of-data-cs/_static/image2.png)

**Abbildung 2**: Konfigurieren der Abfrage für die Verwendung einer SELECT-Anweisung, die einen einzelnen Wert zurückgibt

Nachdem Sie den Typ der zu verwendenden Abfrage angegeben haben, müssen Sie als nächstes die Abfrage angeben.

![Verwenden Sie die Abfrage SELECT count (*) from products.](efficiently-paging-through-large-amounts-of-data-cs/_static/image3.png)

**Abbildung 3**: Verwenden der SELECT count ( \* ) from Products-Abfrage

Geben Sie abschließend den Namen für die Methode an. Wie bereits erwähnt, verwenden Sie `TotalNumberOfProducts` .

![Benennen Sie die DAL-Methode totalnumofproducts.](efficiently-paging-through-large-amounts-of-data-cs/_static/image4.png)

**Abbildung 4**: Benennen der dal-Methode totalnumofproducts

Nachdem Sie auf Fertigstellen geklickt haben, fügt der Assistent die `TotalNumberOfProducts` Methode der dal hinzu. Die skalaren Rückgabe Methoden in der dal geben Werte zulässt-Typen zurück, wenn das Ergebnis der SQL-Abfrage ist `NULL` . `COUNT`Die Abfrage gibt jedoch immer einen Wert zurück, der kein `NULL` Wert ist. unabhängig davon gibt die DAL-Methode eine Ganzzahl zurück, die NULL-Werte zulässt.

Zusätzlich zur dal-Methode benötigen wir auch eine-Methode in der BLL. Öffnen `ProductsBLL` Sie die Klassendatei, und fügen Sie eine `TotalNumberOfProducts` Methode hinzu, die einfach zur dal s- `TotalNumberOfProducts` Methode aufruft:

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample2.cs)]

Die DAL s- `TotalNumberOfProducts` Methode gibt eine Ganzzahl zurück, die NULL-Werte zulässt. Wir haben jedoch die `ProductsBLL` Klasse s- `TotalNumberOfProducts` Methode so erstellt, dass Sie eine Standard Ganzzahl zurückgibt Daher muss die `ProductsBLL` Class s- `TotalNumberOfProducts` Methode den Wert Teil der von der dal s-Methode zurückgegebenen Ganzzahl zurückgeben, die NULL-Werte zulässt `TotalNumberOfProducts` . Der Aufruf von `GetValueOrDefault()` gibt den Wert der Ganzzahl zurück, die NULL-Werte zulässt, sofern vorhanden. wenn die Ganzzahl, die NULL-Werte zulässt, ist, `null` gibt Sie den standardmäßigen ganzzahligen Wert 0 zurück.

## <a name="step-3-returning-the-precise-subset-of-records"></a>Schritt 3: Zurückgeben der exakten Teilmenge von Datensätzen

Die nächste Aufgabe besteht darin, Methoden in der dal und der BLL zu erstellen, die die zuvor erläuterten Zeilen Index-und Maximum Rows-Variablen akzeptieren und die entsprechenden Datensätze zurückgeben. Bevor wir dies tun, betrachten wir zuerst das erforderliche SQL-Skript. Die Herausforderung besteht darin, dass wir in der Lage sein müssen, jeder Zeile in den gesamten auslagerenden Ergebnissen effizient einen Index zuzuweisen, damit wir nur die Datensätze zurückgeben können, beginnend beim Start Zeilen Index (und bis zur maximalen Anzahl von Datensätzen).

Dies ist keine Herausforderung, wenn in der Datenbanktabelle bereits eine Spalte vorhanden ist, die als Zeilen Index fungiert. Auf den ersten Blick könnten wir sehen, dass das `Products` Feld "Table s" `ProductID` ausreichen würde, da das erste Produkt `ProductID` 1, das zweite a 2 usw. hat. Wenn Sie ein Produkt löschen, bleibt jedoch eine Lücke in der Sequenz, wodurch dieser Ansatz aufgehoben wird.

Es gibt zwei allgemeine Verfahren, mit denen ein Zeilen Index effizient mit den Daten verknüpft wird, die durchlaufen werden können, sodass die genaue Teilmenge der Datensätze abgerufen werden kann:

- **Verwenden von SQL Server 2005 s `ROW_NUMBER()` Schlüsselwort** New in SQL Server 2005, das- `ROW_NUMBER()` Schlüsselwort ordnet eine Rangfolge jedem zurückgegebenen Datensatz auf der Grundlage einer Sortierung zu. Diese Rangfolge kann als Zeilen Index für jede Zeile verwendet werden.
- **Verwenden einer Tabellen Variablen und `SET ROWCOUNT` ** Mit SQL Server s- [ `SET ROWCOUNT` Anweisung](https://msdn.microsoft.com/library/ms188774.aspx) können Sie angeben, wie viele Datensätze insgesamt von einer Abfrage verarbeitet werden sollen, bevor Sie beendet werden. [Tabellen Variablen](http://www.sqlteam.com/item.asp?ItemID=9454) sind lokale T-SQL-Variablen, die Tabellendaten enthalten können, vergleichbar mit [temporären Tabellen](http://www.sqlteam.com/item.asp?ItemID=2029). Diese Vorgehensweise funktioniert auch mit Microsoft SQL Server 2005 und SQL Server 2000 (während der `ROW_NUMBER()` Ansatz nur mit SQL Server 2005).  
  
  Die Idee besteht darin, eine Tabellen Variable zu erstellen, die eine `IDENTITY` Spalte und Spalten für die Primärschlüssel der Tabelle enthält, deren Daten per Pager durchlaufen werden. Anschließend wird der Inhalt der Tabelle, deren Daten per Pager durchlaufen werden, in die Tabellen Variable eingefügt, wodurch ein sequenzieller Zeilen Index (über die `IDENTITY` Spalte) für jeden Datensatz in der Tabelle zugeordnet wird. Nachdem die Tabellen Variable aufgefüllt wurde, kann eine- `SELECT` Anweisung für die Tabellen Variable, die mit der zugrunde liegenden Tabelle verknüpft ist, ausgeführt werden, um die jeweiligen Datensätze abzurufen. Die- `SET ROWCOUNT` Anweisung wird verwendet, um die Anzahl der Datensätze, die in die Tabellen Variable gekippt werden müssen, intelligent einzuschränken.  
  
  Die Effizienz dieses Ansatzes basiert auf der angeforderten Seitenzahl, da dem Wert der `SET ROWCOUNT` Wert des Start Zeilen Index zuzüglich der maximalen Zeilen zugewiesen wird. Beim Paging durch Seiten mit niedriger Nummerierung, wie z. b. die ersten Seiten der Daten, ist dieser Ansatz sehr effizient. Sie stellt jedoch beim Abrufen einer Seite am Ende eine standardmäßige Auslagerungs ähnliche Leistung dar.

In diesem Tutorial wird das benutzerdefinierte Paging mithilfe des `ROW_NUMBER()` Schlüssel Worts implementiert. Weitere Informationen zur Verwendung der Tabellen Variablen und der `SET ROWCOUNT` Technik finden Sie unter [eine effizientere Methode für das Paging durch große Resultsets](http://www.4guysfromrolla.com/webtech/042606-1.shtml).

Das `ROW_NUMBER()` Schlüsselwort, das einer Rangfolge zugeordnet ist, mit jedem Datensatz, der über eine bestimmte Reihenfolge zurückgegeben wird

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample3.sql)]

`ROW_NUMBER()` Gibt einen numerischen Wert zurück, der den Rang für jeden Datensatz in Bezug auf die festgestellte Reihenfolge angibt. Um z. b. den Rang für jedes Produkt zu sehen, geordnet nach dem teuersten zum geringsten, können wir die folgende Abfrage verwenden:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample4.sql)]

Abbildung 5 zeigt die Ergebnisse dieser Abfrage, wenn Sie über das Abfragefenster in Visual Studio ausgeführt werden. Beachten Sie, dass die Produkte nach Preis zusammen mit einem Preis Rang für jede Zeile geordnet sind.

![Der Preis Rang ist für jeden zurückgegebenen Datensatz enthalten.](efficiently-paging-through-large-amounts-of-data-cs/_static/image5.png)

**Abbildung 5**: der Preis Rang ist für jeden zurückgegebenen Datensatz enthalten.

> [!NOTE]
> `ROW_NUMBER()` ist nur eine der vielen neuen Rang Folge Funktionen, die in SQL Server 2005 verfügbar sind. Eine ausführlichere Erläuterung von `ROW_NUMBER()` sowie der anderen Rang Folge Funktionen finden Sie unter Zurückgeben von [Rang Ergebnissen mit Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml).

Beim Sortieren der Ergebnisse anhand der angegebenen `ORDER BY` Spalte in der- `OVER` Klausel ( `UnitPrice` im obigen Beispiel) müssen SQL Server die Ergebnisse sortieren. Dies ist ein schneller Vorgang, wenn ein gruppierter Index für die Spalten vorhanden ist, nach denen die Ergebnisse geordnet werden, oder wenn es einen Abdeck enden Index gibt, der andernfalls kostengünstiger sein kann. Um die Leistung für ausreichend große Abfragen zu verbessern, sollten Sie einen nicht gruppierten Index für die Spalte hinzufügen, nach der die Ergebnisse geordnet sind. Eine ausführlichere Betrachtung der Leistungs Überlegungen finden Sie unter [Rang Folge Funktionen und Leistung in SQL Server 2005](http://www.sql-server-performance.com/ak_ranking_functions.asp) .

Die von zurückgegebenen Rang Folge Informationen `ROW_NUMBER()` können nicht direkt in der-Klausel verwendet werden `WHERE` . Allerdings kann eine abgeleitete Tabelle verwendet werden, um das Ergebnis zurückzugeben `ROW_NUMBER()` , das dann in der-Klausel angezeigt werden kann `WHERE` . Beispielsweise wird in der folgenden Abfrage eine abgeleitete Tabelle verwendet, um die Spalten ProductName und UnitPrice zusammen mit dem Ergebnis zurückzugeben `ROW_NUMBER()` , und anschließend wird eine-Klausel verwendet, `WHERE` um nur die Produkte zurückzugeben, deren Preis Rang zwischen 11 und 20 liegt:

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample5.sql)]

Um dieses Konzept etwas weiter zu erweitern, können wir diesen Ansatz verwenden, um eine bestimmte Datenseite mithilfe der gewünschten Werte für Start Zeilen Index und maximale Zeilen Anzahl abzurufen:

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample6.html)]

> [!NOTE]
> Wie wir später in diesem Tutorial sehen werden, wird der *`StartRowIndex`* von ObjectDataSource bereitgestellte ab Null indiziert, wohingegen der `ROW_NUMBER()` von SQL Server 2005 zurückgegebene Wert ab 1 indiziert wird. Daher gibt die `WHERE` -Klausel diese Datensätze zurück, wobei `PriceRank` streng größer als *`StartRowIndex`* und kleiner als oder gleich ist *`StartRowIndex`*  +  *`MaximumRows`* .

Nun haben wir erläutert, wie `ROW_NUMBER()` verwendet werden kann, um eine bestimmte Datenseite anhand der Werte für Start Zeilen Index und maximale Zeilen Anzahl abzurufen. nun müssen wir diese Logik als Methoden in Dal und BLL implementieren.

Beim Erstellen dieser Abfrage müssen wir die Reihenfolge festlegen, nach der die Ergebnisse sortiert werden. Sortieren Sie die Produkte nach Ihrem Namen in alphabetischer Reihenfolge. Dies bedeutet, dass wir mit der Implementierung des benutzerdefinierten Pagings in diesem Tutorial keinen benutzerdefinierten Auslagerungs Bericht erstellen können, der auch sortiert werden kann. Im nächsten Tutorial erfahren Sie jedoch, wie diese Funktionen bereitgestellt werden können.

Im vorherigen Abschnitt haben wir die DAL-Methode als Ad-hoc-SQL-Anweisung erstellt. Leider funktioniert der t-SQL-Parser in Visual Studio, der vom TableAdapter-Assistenten verwendet wird, nicht mit der Syntax, die `OVER` von der Funktion verwendet wird `ROW_NUMBER()` . Daher müssen wir diese dal-Methode als gespeicherte Prozedur erstellen. Wählen Sie im Menü Ansicht die Server-Explorer aus (oder drücken Sie STRG + ALT + S), und erweitern Sie den `NORTHWND.MDF` Knoten. Um eine neue gespeicherte Prozedur hinzuzufügen, klicken Sie mit der rechten Maustaste auf den Knoten gespeicherte Prozeduren, und wählen Sie neue gespeicherte Prozedur hinzufügen aus (siehe Abbildung 6).

![Fügen Sie eine neue gespeicherte Prozedur für das Paging durch die Produkte hinzu.](efficiently-paging-through-large-amounts-of-data-cs/_static/image6.png)

**Abbildung 6**: Hinzufügen einer neuen gespeicherten Prozedur für das Paging durch die Produkte

Diese gespeicherte Prozedur sollte zwei ganzzahlige Eingabeparameter akzeptieren: `@startRowIndex` und `@maximumRows` , und die `ROW_NUMBER()` Funktion, geordnet nach dem- `ProductName` Feld, wobei nur die Zeilen zurückgegeben werden, die größer sind als der angegebene `@startRowIndex` und kleiner oder gleich `@startRowIndex`  +  `@maximumRow` s. Geben Sie das folgende Skript in die neue gespeicherte Prozedur ein, und klicken Sie dann auf das Symbol speichern, um die gespeicherte Prozedur der Datenbank hinzuzufügen.

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample7.sql)]

Nehmen Sie sich nach dem Erstellen der gespeicherten Prozedur einen Moment Zeit, um Sie zu testen. Klicken Sie im Server-Explorer mit der rechten Maustaste auf den `GetProductsPaged` Namen der gespeicherten Prozedur, und wählen Sie die Option Ausführen aus. Anschließend werden Sie von Visual Studio zur Eingabe von Eingabe Parametern `@startRowIndex` und `@maximumRow` s aufgefordert (siehe Abbildung 7). Testen Sie verschiedene Werte, und überprüfen Sie die Ergebnisse.

![Geben Sie einen Wert für die @startRowIndex Parameter und ein. @maximumRows](efficiently-paging-through-large-amounts-of-data-cs/_static/image7.png)

<strong>Abbildung 7</strong>: Eingeben eines Werts für den @startRowIndex -Parameter und den- @maximumRows Parameter

Nachdem Sie diese Eingabeparameter Werte ausgewählt haben, zeigt das Ausgabefenster die Ergebnisse an. Abbildung 8 zeigt die Ergebnisse bei der Übergabe von 10 für den `@startRowIndex` -Parameter und den- `@maximumRows` Parameter.

[![Die Datensätze, die auf der zweiten Seite der Daten angezeigt werden, werden zurückgegeben.](efficiently-paging-through-large-amounts-of-data-cs/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image8.png)

**Abbildung 8**: die Datensätze, die auf der zweiten Seite der Daten angezeigt werden, werden zurückgegeben ([Klicken Sie, um das Bild in voller Größe anzuzeigen](efficiently-paging-through-large-amounts-of-data-cs/_static/image10.png))

Nachdem diese gespeicherte Prozedur erstellt wurde, können wir die- `ProductsTableAdapter` Methode erstellen. Öffnen `Northwind.xsd` Sie das typisierte DataSet, klicken Sie mit der rechten Maustaste in `ProductsTableAdapter` , und wählen Sie die Option Abfrage hinzufügen aus. Anstatt die Abfrage mit einer Ad-hoc-SQL-Anweisung zu erstellen, erstellen Sie Sie mithilfe einer vorhandenen gespeicherten Prozedur.

![Erstellen der dal-Methode mithilfe einer vorhandenen gespeicherten Prozedur](efficiently-paging-through-large-amounts-of-data-cs/_static/image11.png)

**Abbildung 9**: Erstellen der dal-Methode mithilfe einer vorhandenen gespeicherten Prozedur

Als nächstes werden wir aufgefordert, die aufzurufende gespeicherte Prozedur auszuwählen. Wählen Sie in `GetProductsPaged` der Dropdown Liste die gespeicherte Prozedur aus.

![Wählen Sie in der Dropdown Liste die gespeicherte Prozedur getproductspaged aus.](efficiently-paging-through-large-amounts-of-data-cs/_static/image12.png)

**Abbildung 10**: Auswählen der gespeicherten Prozedur "getproductspaged" aus der Dropdown Liste

Im nächsten Bildschirm werden Sie gefragt, welche Art von Daten von der gespeicherten Prozedur zurückgegeben wird: tabellarische Daten, ein einzelner Wert oder kein Wert. Da die `GetProductsPaged` gespeicherte Prozedur mehrere Datensätze zurückgeben kann, geben Sie an, dass Tabellendaten zurückgegeben werden.

![Gibt an, dass die gespeicherte Prozedur Tabellendaten zurückgibt.](efficiently-paging-through-large-amounts-of-data-cs/_static/image13.png)

**Abbildung 11**: angeben, dass die gespeicherte Prozedur Tabellendaten zurückgibt

Geben Sie abschließend die Namen der Methoden an, die Sie erstellen möchten. Wie bei den vorherigen Tutorials können Sie auch Methoden erstellen, indem Sie die Datentabelle ausfüllen verwenden und eine Datentabelle zurückgeben. Benennen Sie die erste Methode `FillPaged` und die zweite `GetProductsPaged` .

![Benennen Sie die Methoden fillpout und getproductspaged.](efficiently-paging-through-large-amounts-of-data-cs/_static/image14.png)

**Abbildung 12**: Benennen der Methoden "fillpout" und "getproductspaged"

Zusätzlich zum Erstellen einer dal-Methode, um eine bestimmte Produktseite zurückzugeben, müssen wir diese Funktionalität auch in der BLL bereitstellen. Wie die DAL-Methode muss die getproductspaged-Methode der BLL s zwei ganzzahlige Eingaben zum Angeben des Start Zeilen Indexes und der maximalen Zeilen akzeptieren und nur die Datensätze zurückgeben, die in den angegebenen Bereich fallen. Erstellen Sie eine solche BLL-Methode in der productbll-Klasse, die lediglich die getproductspaged-Methode von Dal s aufruft, wie im folgenden Beispiel:

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample8.cs)]

Sie können einen beliebigen Namen für die Eingabeparameter der BLL-Methode verwenden, aber wie wir in Kürze sehen werden, entscheiden wir uns für die Verwendung `startRowIndex` und Speicherung `maximumRows` von einem zusätzlichen Arbeitsaufwand, wenn Sie eine ObjectDataSource für die Verwendung dieser Methode konfigurieren.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>Schritt 4: Konfigurieren von ObjectDataSource für die Verwendung von benutzerdefiniertem Paging

Wenn die BLL-und Dal-Methoden für den Zugriff auf eine bestimmte Teilmenge von Datensätzen abgeschlossen sind, können wir ein GridView-Steuerelement erstellen, das die zugrunde liegenden Datensätze mithilfe von benutzerdefiniertem Paging durchläuft. Öffnen Sie zunächst die `EfficientPaging.aspx` Seite im `PagingAndSorting` Ordner, fügen Sie der Seite eine GridView hinzu, und konfigurieren Sie Sie für die Verwendung eines neuen ObjectDataSource-Steuer Elements. In unseren vorherigen Tutorials haben wir oft die ObjectDataSource für die Verwendung der `ProductsBLL` Class s- `GetProducts` Methode konfiguriert. Diesmal möchten wir jedoch die- `GetProductsPaged` Methode verwenden, da die- `GetProducts` Methode *alle* Produkte in der Datenbank zurückgibt, während `GetProductsPaged` nur eine bestimmte Teilmenge von Datensätzen zurückgibt.

![Konfigurieren von ObjectDataSource für die Verwendung der getproductspaged-Methode der productbll-Klasse](efficiently-paging-through-large-amounts-of-data-cs/_static/image15.png)

**Abbildung 13**: Konfigurieren von ObjectDataSource für die Verwendung der getproductspaged-Methode der productbll-Klasse

Da wir eine schreibgeschützte GridView-Sicht neu erstellen, nehmen Sie sich einen Moment Zeit, um die Dropdown Liste der Methode auf den Registerkarten einfügen, aktualisieren und löschen auf (keine) festzulegen.

Im nächsten Schritt fordert der ObjectDataSource-Assistent Sie zur Eingabe der Quellen der `GetProductsPaged` Methoden s `startRowIndex` und `maximumRows` Eingabeparameter Werte auf. Diese Eingabeparameter werden tatsächlich automatisch von der GridView festgelegt. lassen Sie die Quelle also auf keine festgelegt, und klicken Sie auf Fertigstellen.

![Belassen Sie die Eingabe Parameter Quellen als "None".](efficiently-paging-through-large-amounts-of-data-cs/_static/image16.png)

**Abbildung 14**: belassen der Eingabe Parameter Quellen als "None"

Nachdem Sie den ObjectDataSource-Assistenten abgeschlossen haben, enthält das GridView-Objekt ein BoundField-oder CheckBoxField-Objekt für jedes der Product Data-Felder. Sie können die Darstellung des GridView-s beliebig anpassen. Ich habe mich entschieden, nur die `ProductName` `CategoryName` Felder,, `SupplierName` , `QuantityPerUnit` und `UnitPrice` boundfields anzuzeigen. Konfigurieren Sie außerdem die GridView so, dass Paging unterstützt wird, indem Sie das Kontrollkästchen Paging aktivieren im Smarttags aktivieren. Nach diesen Änderungen sollten das deklarative Markup View-und ObjectDataSource-Markup in etwa wie folgt aussehen:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample9.aspx)]

Wenn Sie die Seite jedoch über einen Browser besuchen, ist die GridView nicht gefunden.

![Die GridView wird nicht angezeigt.](efficiently-paging-through-large-amounts-of-data-cs/_static/image17.png)

**Abbildung 15**: die GridView wird nicht angezeigt

Die GridView fehlt, weil die ObjectDataSource aktuell 0 als Werte für beide `GetProductsPaged` `startRowIndex` -und- `maximumRows` Eingabeparameter verwendet. Daher gibt die resultierende SQL-Abfrage keine Datensätze zurück, weshalb die GridView nicht angezeigt wird.

Um dieses Problem zu beheben, müssen wir ObjectDataSource für die Verwendung von benutzerdefiniertem Paging konfigurieren. Dies kann in den folgenden Schritten erreicht werden:

1. **Legen Sie die `EnablePaging` Eigenschaft `true` ObjectDataSource s auf fest** , um die ObjectDataSource anzugeben, die an die `SelectMethod` beiden zusätzlichen Parameter übergeben werden muss: eine, um den Start Zeilen Index ( [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) ) anzugeben, und eine, um die maximale Anzahl von Zeilen anzugeben ( [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) ).
2. **Legen Sie die Eigenschaften ObjectDataSource s `StartRowIndexParameterName` und `MaximumRowsParameterName` entsprechend fest** , und geben Sie die Namen der Eingabeparameter an, die `StartRowIndexParameterName` `MaximumRowsParameterName` `SelectMethod` für benutzerdefinierte Paginierung an übergeben werden. Standardmäßig lauten diese Parameternamen `startIndexRow` und `maximumRows` . aus diesem Grund wurden bei der Erstellung der- `GetProductsPaged` Methode in der BLL diese Werte für die Eingabeparameter verwendet. Wenn Sie für die BLL s-Methode verschiedene Parameternamen verwenden `GetProductsPaged` `startIndex` möchten, z. b. und `maxRows` , müssen Sie z. b. die ObjectDataSource s `StartRowIndexParameterName` -Eigenschaft und die-Eigenschaft entsprechend festlegen `MaximumRowsParameterName` (z. b. startIndex für `StartRowIndexParameterName` und MaxRows für `MaximumRowsParameterName` ).
3. **Legen Sie die ObjectDataSource s- [ `SelectCountMethod` Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) auf den Namen der Methode fest, die die Gesamtzahl der Datensätze zurückgibt, die durch das durchlaufen ( `TotalNumberOfProducts` ) zurückgeleitet werden** , dass die `ProductsBLL` Klasse s `TotalNumberOfProducts` die Gesamtzahl der Datensätze zurückgibt, die mithilfe einer dal-Methode, die eine Abfrage ausführt, durchlaufen werden `SELECT COUNT(*) FROM Products` Diese Informationen werden von ObjectDataSource benötigt, um die Paging-Schnittstelle ordnungsgemäß zu erzeugen.
4. **Entfernen Sie das `startRowIndex` -Element und das- `maximumRows` `<asp:Parameter>` Element aus dem deklarativen Markup von ObjectDataSource s** , wenn Sie ObjectDataSource mithilfe des Assistenten konfigurieren. Visual Studio hat automatisch zwei- `<asp:Parameter>` Elemente für die `GetProductsPaged` Eingabeparameter der Methode hinzugefügt. `EnablePaging` `true` Wenn Sie auf festlegen, werden diese Parameter automatisch übergeben. Wenn Sie auch in der deklarativen Syntax angezeigt werden, versucht ObjectDataSource, *vier* Parameter an die `GetProductsPaged` -Methode und zwei Parameter an die- `TotalNumberOfProducts` Methode zu übergeben. Wenn Sie vergessen, diese Elemente zu entfernen `<asp:Parameter>` , erhalten Sie beim Aufrufen der Seite über einen Browser eine Fehlermeldung wie die folgende: *ObjectDataSource "ObjectDataSource1" konnte keine nicht generische Methode "totalmaximiofproducts" finden, die Parameter hat: StartRowIndex, MaximumRows*.

Nachdem Sie diese Änderungen vorgenommen haben, sollte die deklarative Syntax von ObjectDataSource s wie folgt aussehen:

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample10.aspx)]

Beachten Sie, dass die `EnablePaging` -Eigenschaft und die-Eigenschaft `SelectCountMethod` festgelegt wurden und die `<asp:Parameter>` Elemente entfernt wurden. Abbildung 16 zeigt einen Screenshot der Eigenschaftenfenster, nachdem diese Änderungen vorgenommen wurden.

![Konfigurieren Sie zum Verwenden von benutzerdefiniertem Paging das ObjectDataSource-Steuerelement.](efficiently-paging-through-large-amounts-of-data-cs/_static/image18.png)

**Abbildung 16**: Konfigurieren des ObjectDataSource-Steuer Elements für die Verwendung von benutzerdefiniertem Paging

Nachdem Sie diese Änderungen vorgenommen haben, besuchen Sie diese Seite über einen Browser. Es sollten 10 Produkte aufgelistet werden, die alphabetisch sortiert sind. Nehmen Sie sich einen Moment Zeit, um die Datenseiten Weise zu durchlaufen. Es gibt zwar keinen visuellen Unterschied zwischen der Perspektive des Endbenutzers zwischen Standard-Paging und benutzerdefiniertem Paging, das benutzerdefinierte Paging wird jedoch effizienter durch große Datenmengen abgerufen, da nur die Datensätze abgerufen werden, die für eine bestimmte Seite angezeigt werden müssen.

[![Die Daten, geordnet nach dem Namen des Produkts, werden mithilfe von benutzerdefiniertem Paging ausgelagert.](efficiently-paging-through-large-amounts-of-data-cs/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image19.png)

**Abbildung 17**: die Daten, geordnet nach dem Namen des Produkts, werden mithilfe von benutzerdefiniertem Paging ausgelagert ([Klicken Sie, um das Bild in voller Größe anzuzeigen](efficiently-paging-through-large-amounts-of-data-cs/_static/image21.png))

> [!NOTE]
> Bei benutzerdefiniertem Paging wird der von der ObjectDataSource zurückgegebene Wert der Seitenanzahl `SelectCountMethod` im Ansichts Zustand der GridView gespeichert. Andere GridView-Variablen die `PageIndex` -,-, `EditIndex` `SelectedIndex` `DataKeys` -,-,-Auflistung usw. werden im *Steuerelement Zustand*gespeichert, der unabhängig vom Wert der-Eigenschaft der GridView persistent gespeichert wird `EnableViewState` . Da der `PageCount` Wert über Postbacks mit dem Ansichts Zustand beibehalten wird, ist es zwingend erforderlich, dass der Ansichts Zustand der GridView aktiviert ist, wenn Sie eine Paging-Schnittstelle verwenden, die einen Link zur letzten Seite enthält. (Wenn die pagingschnittstelle keinen direkten Link zur letzten Seite enthält, können Sie den Ansichts Zustand deaktivieren.)

Wenn Sie auf den Link letzte Seite klicken, wird ein Postback ausgelöst, und die GridView wird angewiesen, seine-Eigenschaft zu aktualisieren `PageIndex` . Wenn auf den letzten Seiten Link geklickt wird, weist die GridView deren- `PageIndex` Eigenschaft einem Wert zu, der kleiner als die zugehörige- `PageCount` Eigenschaft ist. Wenn der Ansichts Zustand deaktiviert ist, `PageCount` geht der Wert zwischen Postbacks verloren, und dem `PageIndex` wird stattdessen der maximale ganzzahlige Wert zugewiesen. Als nächstes versucht die GridView, den Zeilen Index zu ermitteln, indem die-Eigenschaft und die-Eigenschaft multipliziert werden `PageSize` `PageCount` . Dies führt zu einer, `OverflowException` da das Produkt die maximal zulässige ganzzahlige Größe überschreitet.

## <a name="implement-custom-paging-and-sorting"></a>Implementieren von benutzerdefiniertem Paging und Sortieren

Unsere aktuelle Implementierung der benutzerdefinierten Auslagerung erfordert, dass die Reihenfolge, in der die Daten per Pager durchlaufen werden, bei der Erstellung der gespeicherten Prozedur statisch angegeben wird `GetProductsPaged` . Möglicherweise haben Sie jedoch bemerkt, dass das GridView s-Smarttag neben der Option Paging aktivieren auch das Kontrollkästchen Sortierung aktivieren enthält. Das Hinzufügen von Sortierungs Unterstützung zu GridView mit unserer aktuellen benutzerdefinierten pagingimplementierung wird jedoch nur die Datensätze auf der aktuell angezeigten Datenseite sortieren. Wenn Sie z. b. die GridView so konfigurieren, dass auch Paging unterstützt wird, und dann beim Anzeigen der ersten Seite der Daten in absteigender Reihenfolge nach Produktname sortieren, wird die Reihenfolge der Produkte auf Seite 1 umgekehrt. Wie in Abbildung 18 gezeigt, zeigt Carnarvon Tigers als erstes Produkt, wenn die Sortierung in umgekehrter alphabetischer Reihenfolge erfolgt, die die 71 anderen Produkte ignoriert, die in alphabetischer Reihenfolge nach Carnarvon Tigers stehen. nur die Datensätze auf der ersten Seite werden in der Sortierung berücksichtigt.

[![Es werden nur die Daten sortiert, die auf der aktuellen Seite angezeigt werden.](efficiently-paging-through-large-amounts-of-data-cs/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image22.png)

**Abbildung 18**: nur die auf der aktuellen Seite angezeigten Daten werden sortiert ([Klicken Sie, um das Bild in voller Größe anzuzeigen](efficiently-paging-through-large-amounts-of-data-cs/_static/image24.png))

Die Sortierung gilt nur für die aktuelle Datenseite, da die Sortierung erfolgt, nachdem die Daten aus der BLL s `GetProductsPaged` -Methode abgerufen wurden, und diese Methode gibt nur die Datensätze für die jeweilige Seite zurück. Um die Sortierung ordnungsgemäß zu implementieren, müssen wir den Sortier Ausdruck an die-Methode übergeben, `GetProductsPaged` damit die Daten entsprechend sortiert werden können, bevor die jeweilige Datenseite zurückgegeben wird. Im nächsten Tutorial erfahren Sie, wie Sie dies erreichen.

## <a name="implementing-custom-paging-and-deleting"></a>Implementieren von benutzerdefiniertem Paging und löschen

Wenn Sie das Löschen von Funktionen in einer GridView aktivieren, deren Daten mittels benutzerdefinierter pagingverfahren ausgelagert werden, werden Sie feststellen, dass beim Löschen des letzten Datensatzes aus der letzten Seite das GridView-Tool ausgeblendet wird, anstatt die GridView s entsprechend zu dekrementieren `PageIndex` . Zum Reproduzieren dieses Fehlers aktivieren Sie das Löschen für das soeben erstellte Tutorial. Wechseln Sie zur letzten Seite (Seite 9), auf der ein einzelnes Produkt angezeigt werden soll, da wir das Paging über 81 Produkte, 10 Produkte auf einmal durchlaufen. Löschen Sie dieses Produkt.

Nach dem Löschen des letzten Produkts *sollte* die GridView automatisch zur achten Seite wechseln, und diese Funktionalität wird mit Standard Auslagerung angezeigt. Mit benutzerdefiniertem Paging wird jedoch nach dem Löschen des letzten Produkts auf der letzten Seite das GridView-Fenster ganz einfach auf dem Bildschirm ausgeblendet. Der genaue Grund dafür ist, dass dieser Vorgang etwas über den *Rahmen dieses Tutorials* hinausgeht. Weitere Informationen finden Sie unter [Löschen des letzten Datensatzes auf der letzten Seite aus einer GridView mit benutzerdefiniertem Paging](http://scottonwriting.net/sowblog/posts/7326.aspx) für die Details auf niedriger Ebene. In der Zusammenfassung werden die folgenden Schritte ausgeführt, die von der GridView ausgeführt werden, wenn auf die Schaltfläche "Löschen" geklickt wird:

1. Löschen des Datensatzes
2. Hiermit werden die entsprechenden Datensätze zum Anzeigen der angegebenen `PageIndex` und `PageSize`
3. Stellen Sie sicher, dass die `PageIndex` die Anzahl der Datenseiten in der Datenquelle nicht überschreitet. wenn dies der Fall ist, verringern Sie automatisch die GridView s- `PageIndex` Eigenschaft.
4. Binden der entsprechenden Datenseite an die GridView mithilfe der in Schritt 2 erhaltenen Datensätze

Das Problem ist darauf zurückzuführen, dass in Schritt 2 das `PageIndex` beim Abrufen der anzuzeigenden Datensätze verwendete die `PageIndex` der letzten Seite ist, deren einziger Datensatz soeben gelöscht wurde. Aus diesem Grund werden in Schritt 2 *keine* Datensätze zurückgegeben, da die letzte Seite der Daten keine Datensätze mehr enthält. In Schritt 3 erkennt das GridView-Objekt, dass seine- `PageIndex` Eigenschaft größer ist als die Gesamtzahl der Seiten in der Datenquelle (seit dem Löschen des letzten Datensatzes auf der letzten Seite) und verringert daher seine- `PageIndex` Eigenschaft. In Schritt 4 versucht die GridView, sich an die in Schritt 2 abgerufenen Daten zu binden. in Schritt 2 wurden jedoch keine Datensätze zurückgegeben, was zu einer leeren GridView führte. Beim standardmäßigen Paging wird dieses Problem nicht in der Oberfläche gelöst, da in Schritt 2 *alle* Datensätze aus der Datenquelle abgerufen werden.

Um dieses Problem zu beheben, haben wir zwei Möglichkeiten. Der erste besteht darin, einen Ereignishandler für den GridView s- `RowDeleted` Ereignishandler zu erstellen, der bestimmt, wie viele Datensätze auf der Seite angezeigt wurden, die soeben gelöscht wurde. Wenn nur ein Datensatz vorhanden ist, muss der soeben gelöschte Datensatz der letzte Datensatz sein, und wir müssen die GridView s Dekrement `PageIndex` . Natürlich möchten wir nur den aktualisieren, `PageIndex` Wenn der Löschvorgang tatsächlich erfolgreich war. Dies kann durch sicherstellen sichergestellt werden, dass die- `e.Exception` Eigenschaft ist `null` .

Diese Vorgehensweise funktioniert, weil Sie die `PageIndex` nach Schritt 1, aber vor Schritt 2 aktualisiert. Daher wird in Schritt 2 der entsprechende Satz von Datensätzen zurückgegeben. Verwenden Sie hierzu Code wie den folgenden:

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample11.cs)]

Eine Alternative Problem Umgehung besteht darin, einen Ereignishandler für das Ereignis "ObjectDataSource s" zu erstellen `RowDeleted` und die-Eigenschaft auf den Wert "1" festzulegen `AffectedRows` . Nachdem Sie den Datensatz in Schritt 1 gelöscht haben (aber bevor Sie die Daten in Schritt 2 erneut abrufen), aktualisiert die GridView deren- `PageIndex` Eigenschaft, wenn eine oder mehrere Zeilen von dem Vorgang betroffen sind. Die `AffectedRows` -Eigenschaft wird jedoch nicht von ObjectDataSource festgelegt, weshalb dieser Schritt ausgelassen wird. Eine Möglichkeit, diesen Schritt auszuführen, besteht darin, die Eigenschaft manuell festzulegen, `AffectedRows` Wenn der Löschvorgang erfolgreich abgeschlossen wurde. Dies kann mithilfe von Code wie dem folgenden erreicht werden:

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample12.cs)]

Der Code für beide Ereignishandler finden Sie in der Code Behind-Klasse des `EfficientPaging.aspx` Beispiels.

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>Vergleichen der Leistung von Default und Custom Paging

Da das benutzerdefinierte Paging nur die benötigten Datensätze abruft, während die Standard Paginierung *alle* Datensätze für jede angezeigte Seite zurückgibt, ist es klar, dass das benutzerdefinierte Paging effizienter ist als das Standardpaging. Aber wie viel effizienter ist das benutzerdefinierte Paging? Welche Art von Leistungssteigerungen können Sie anzeigen, indem Sie von der Standard Auslagerung zu benutzerdefiniertem Paging wechseln?

Leider gibt es hier keine Antwort. Der Leistungsgewinn hängt von einer Reihe von Faktoren ab. die wichtigsten zwei sind die Anzahl der Datensätze, die durchlaufen werden, sowie die Last auf dem Datenbankserver und die Kommunikationskanäle zwischen dem Webserver und dem Datenbankserver. Bei kleinen Tabellen mit nur wenigen Dutzend Datensätzen kann der Leistungsunterschied vernachlässigbar sein. Bei großen Tabellen mit Tausenden bis Hunderttausenden von Zeilen ist der Leistungsunterschied jedoch akut.

Ein Artikel von My, [Custom Paging in ASP.NET 2,0 mit SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx), enthält einige Leistungstests, die ich ausgeführt habe, um die Unterschiede in der Leistung zwischen diesen beiden Paging-Techniken beim Paging durch eine Datenbanktabelle mit 50.000 Datensätzen zu präsentieren. In diesen Tests habe ich die Zeit für die Ausführung der Abfrage auf SQL Server Ebene (mithilfe von [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)) und auf der ASP.NET-Seite unter Verwendung von [ASP.net s-Ablauf Verfolgungs Funktionen](https://msdn.microsoft.com/library/y13fw6we.aspx)überprüft. Beachten Sie, dass diese Tests in meinem Entwicklungsfeld mit einem einzelnen aktiven Benutzer ausgeführt wurden und daher nicht sicher sind und keine typischen Website-Auslastungs Muster imitieren. Unabhängig davon veranschaulichen die Ergebnisse die relativen Unterschiede in der Ausführungszeit für das standardmäßige und benutzerdefinierte Paging bei der Arbeit mit ausreichend großen Datenmengen.

|  | **Durchschn. Dauer (Sek.)** | **Reads** |
| --- | --- | --- |
| **Standard-Paging-SQL-Profiler** | 1,411 | 383 |
| **Benutzerdefiniertes Paging von SQL Profiler** | 0,002 | 29 |
| **Standard-Paging ASP.net Ablauf Verfolgung** | 2,379 | *N/V* |
| **Benutzerdefiniertes Paging ASP.net Ablauf Verfolgung** | 0,029 | *N/V* |

Wie Sie sehen können, erforderte das Abrufen einer bestimmten Datenseite im Durchschnitt 354 weniger Lesevorgänge und wurde in einem Bruchteil der Zeit abgeschlossen. Auf der Seite "ASP.net" konnte die Seite in der Nähe des standardmäßigen Auslagerungs Zeitraums (<sup>in der 1/100</sup> Nähe des standardmäßigen Paging) wieder hergestellt werden. Weitere Informationen zu diesen Ergebnissen sowie Code und eine Datenbank, die Sie herunterladen können, um diese Tests in ihrer eigenen Umgebung zu reproduzieren, finden Sie in diesem [Artikel](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) .

## <a name="summary"></a>Zusammenfassung

Standard-Paging ist ein geliefert zur Implementierung, aktivieren Sie das Kontrollkästchen Paging aktivieren im Smarttags des dateiweb-Steuer Elements, aber eine solche Einfachheit ergibt sich aus den Kosten der Leistung. Beim standardmäßigen Paging werden *alle* Datensätze zurückgegeben, wenn ein Benutzer eine beliebige Seite mit Daten anfordert, obwohl möglicherweise nur ein kleiner Bruchteil davon angezeigt wird. Zur Bekämpfung dieses Leistungs Aufwands bietet ObjectDataSource eine Alternative Paging-Option für benutzerdefiniertes Paging.

Während das benutzerdefinierte Paging bei der standardmäßigen Auslagerung von Leistungsproblemen verbessern kann, indem nur die Datensätze abgerufen werden, die angezeigt werden müssen, ist die Implementierung von benutzerdefiniertem Paging mehr beteiligt. Zuerst muss eine Abfrage geschrieben werden, die ordnungsgemäß (und effizient) auf die bestimmte Teilmenge der angeforderten Datensätze zugreift. Dies kann auf verschiedene Arten erreicht werden: das, das wir in diesem Tutorial untersucht haben, ist die Verwendung SQL Server 2005 s New `ROW_NUMBER()` -Funktion, um Ergebnisse zu ordnen und dann nur die Ergebnisse zurückzugeben, deren Rangfolge innerhalb eines angegebenen Bereichs liegt. Außerdem müssen wir eine Möglichkeit hinzufügen, um die Gesamtanzahl der Datensätze zu ermitteln, die durchlaufen werden. Nachdem Sie diese dal-und BLL-Methoden erstellt haben, müssen wir auch die ObjectDataSource so konfigurieren, dass Sie bestimmen kann, wie viele Datensätze durchlaufen werden, und die Werte für Start Zeilen Index und maximale Zeilen Menge an die BLL übergeben können.

Die Implementierung von benutzerdefiniertem Paging erfordert zwar eine Reihe von Schritten und ist nicht so einfach wie das standardmäßige Paging, das benutzerdefinierte Paging ist jedoch beim Paging durch ausreichend große Datenmengen notwendig. Wenn die untersuchten Ergebnisse angezeigt werden, kann das benutzerdefinierte Paging Sekunden aus der ASP.NET Seiten-Rendering-Zeit verringern und die Last auf dem Datenbankserver um eine oder mehrere Größenordnungen erhöhen.

Fröhliche Programmierung!

## <a name="about-the-author"></a>Zum Autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), Autor der sieben ASP/ASP. net-Bücher und Gründer von [4GuysFromRolla.com](http://www.4guysfromrolla.com), hat seit 1998 mit Microsoft-Webtechnologien gearbeitet. Scott arbeitet als unabhängiger Berater, Ausbilder und Writer. Sein letztes Buch ist [*Sams Teach Yourself ASP.NET 2,0 in 24 Stunden*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Er kann mit erreicht werden [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) oder über seinen Blog finden Sie unter [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

> [!div class="step-by-step"]
> [Zurück](paging-and-sorting-report-data-cs.md)
> [Weiter](sorting-custom-paged-data-cs.md)
