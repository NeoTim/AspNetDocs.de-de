---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: Anzeigen von Daten in einem Diagramm mit ASP.NET Webseiten (Razor) | Microsoft Docs
author: rick-anderson
description: In diesem Kapitel wird erläutert, wie Daten in einem Diagramm angezeigt werden. In den vorherigen Kapiteln haben Sie gelernt, wie Daten manuell und in einem Raster angezeigt werden. In diesem Kapitel werden...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542884"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>Anzeigen von Daten in einem Diagramm mit ASP.NET Webseiten (Razor)

von [Microsoft](https://github.com/microsoft)

> In diesem Artikel wird erläutert, wie Sie mithilfe des Hilfsplans ein `Chart` Diagramm zum Anzeigen von Daten auf einer ASP.NET Webseiten-Website (Razor) verwenden.
> 
> **Was Sie lernen:**
> 
> - Anzeigen von Daten in einem Diagramm.
> - So formatieren Sie Diagramme mit integrierten Designs.
> - Speichern von Diagrammen und Zwischenspeichern für eine bessere Leistung.
> 
> Dies sind die ASP.NET Programmierfunktionen, die in dem Artikel eingeführt werden:
> 
> - Der `Chart` Helfer.
> 
> > [!NOTE]
> > Die Informationen in diesem Artikel gelten für ASP.NET Webseiten 1.0 und Webseiten 2.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Der Chart-Helfer

Wenn Sie Ihre Daten in grafischer Form `Chart` anzeigen möchten, können Sie den Helfer verwenden. Der `Chart` Helfer kann ein Bild rendern, das Daten in einer Vielzahl von Diagrammtypen anzeigt. Es unterstützt viele Optionen für formatieren und beschriften. Der `Chart` Helfer kann mehr als 30 Diagrammtypen rendern, einschließlich aller Diagrammtypen, die Sie aus Microsoft Excel oder anderen Werkzeugen kennen &#8212; Flächendiagramme, Balkendiagramme, Säulendiagramme, Liniendiagramme und Kreisdiagramme sowie spezialisiertere Diagramme wie Aktiendiagramme kennen.

| **Flächendiagramm** ![Beschreibung: Bild des Flächendiagrammtyps](7-displaying-data-in-a-chart/_static/image1.jpg) | **Balkendiagramm** ![Beschreibung: Bild des Balkendiagrammtyps](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Säulendiagramm** ![Beschreibung: Bild des Säulendiagrammtyps](7-displaying-data-in-a-chart/_static/image3.jpg) | **Liniendiagramm** ![Beschreibung: Bild des Liniendiagrammtyps](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Kreisdiagramm** ![Beschreibung: Bild des Kreisdiagrammtyps](7-displaying-data-in-a-chart/_static/image5.jpg) | **Stockchart** ![Beschreibung: Bild des Aktiendiagrammtyps](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Diagrammelemente

Diagramme zeigen Daten und zusätzliche Elemente wie Legenden, Achsen, Serien usw. Die folgende Abbildung zeigt viele diagrammelemente, die Sie `Chart` anpassen können, wenn Sie den Helfer verwenden. In diesem Artikel erfahren Sie, wie Sie einige (nicht alle) dieser Elemente festlegen.

![Beschreibung: Bild mit den Diagrammelementen](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Erstellen eines Diagramms aus Daten

Die Daten, die Sie in einem Diagramm anzeigen, können aus einem Array, aus den Ergebnissen stammen, die aus einer Datenbank zurückgegeben werden, oder aus Daten, die sich in einer XML-Datei befinden.

### <a name="using-an-array"></a>Verwenden eines Arrays

Wie in [Einführung in ASP.NET Webseitenprogrammierung mit der Razor-Syntax](https://go.microsoft.com/fwlink/?LinkId=202890)erläutert, können Sie mit einem Array eine Sammlung ähnlicher Elemente in einer einzelnen Variablen speichern. Sie können Arrays verwenden, um die Daten zu enthalten, die Sie in das Diagramm aufnehmen möchten.

Dieses Verfahren zeigt, wie Sie ein Diagramm aus Daten in Arrays mithilfe des Standarddiagrammtyps erstellen können. Außerdem wird gezeigt, wie das Diagramm auf der Seite angezeigt wird.

1. Erstellen Sie eine neue Datei mit dem Namen *ChartArrayBasic.cshtml*.
2. Ersetzen Sie den vorhandenen Inhalt durch Folgendes: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Der Code erstellt zuerst ein neues Diagramm und legt seine Breite und Höhe fest. Sie geben den Diagrammtitel `AddTitle` mithilfe der Methode an. Zum Hinzufügen von Daten `AddSeries` verwenden Sie die Methode. In diesem Beispiel verwenden `name` `xValue`Sie `yValues` die Parameter `AddSeries` , und Parameter der Methode. Der `name` Parameter wird in der Diagrammlegende angezeigt. Der `xValue` Parameter enthält ein Array von Daten, das entlang der horizontalen Achse des Diagramms angezeigt wird. Der `yValues` Parameter enthält ein Array von Daten, die zum Plotten der vertikalen Punkte des Diagramms verwendet werden.

    Die `Write` Methode rendert das Diagramm tatsächlich. Da Sie in diesem Fall keinen Diagrammtyp `Chart` angegeben haben, rendert der Helfer das Standarddiagramm, das ein Säulendiagramm ist.
3. Führen Sie die Seite im Browser aus. Der Browser zeigt das Diagramm an. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Verwenden einer Datenbankabfrage für Diagrammdaten

Wenn sich die Informationen, die Sie planen möchten, in einer Datenbank befinden, können Sie eine Datenbankabfrage ausführen und dann Daten aus den Ergebnissen verwenden, um das Diagramm zu erstellen. Dieses Verfahren zeigt Ihnen, wie Sie die Daten aus der Datenbank lesen und anzeigen, die im Artikel Einführung in das [Arbeiten mit einer Datenbank in ASP.NET Webseitenwebsites](https://go.microsoft.com/fwlink/?LinkId=202893)erstellt wurden.

1. Fügen Sie dem Stammverzeichnis der Website einen *Ordner "App-Daten"\_* hinzu, wenn der Ordner noch nicht vorhanden ist.
2. Fügen Sie im Ordner *App-Daten\_* die Datenbankdatei mit dem Namen *SmallBakery.sdf* hinzu, die unter Einführung in das [Arbeiten mit einer Datenbank in ASP.NET Webseitenwebsites](https://go.microsoft.com/fwlink/?LinkId=202893)beschrieben wird.
3. Erstellen Sie eine neue Datei mit dem Namen *ChartDataQuery.cshtml*.
4. Ersetzen Sie den vorhandenen Inhalt durch Folgendes:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Der Code öffnet zuerst die SmallBakery-Datenbank und `db`weist sie einer Variablen mit dem Namen zu. Diese Variable `Database` stellt ein Objekt dar, das zum Lesen und Schreiben in die Datenbank verwendet werden kann. Als Nächstes führt der Code eine SQL-Abfrage aus, um den Namen und den Preis jedes Produkts abzufragen. Der Code erstellt ein neues Diagramm und übergibt die `DataBindTable` Datenbankabfrage an ihn, indem er die Methode des Diagramms aufruft. Diese Methode verwendet zwei `dataSource` Parameter: Der Parameter ist für `xField` die Daten aus der Abfrage, und mit dem Parameter können Sie festlegen, welche Datenspalte für die x-Achse des Diagramms verwendet wird.

    Als Alternative zur `DataBindTable` Verwendung der Methode `AddSeries` können Sie `Chart` die Methode des Helfers verwenden. Mit `AddSeries` der Methode `xValue` können `yValues` Sie die und Parameter festlegen. Anstatt die `DataBindTable` Methode beispielsweise wie folgt zu verwenden:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Sie können `AddSeries` die Methode wie folgt verwenden:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Beide führen die gleichen Ergebnisse aus. Die `AddSeries` Methode ist flexibler, da Sie den Diagrammtyp und `DataBindTable` die Daten expliziter angeben können, die Methode jedoch einfacher zu verwenden ist, wenn Sie die zusätzliche Flexibilität nicht benötigen.
5. Führen Sie die Seite in einem Browser aus. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>Verwenden von XML-Daten

Die dritte Option für das Diagrammisten besteht darin, eine XML-Datei als Daten für das Diagramm zu verwenden. Dies erfordert, dass die XML-Datei auch über eine Schemadatei *(Xsd-Datei)* verfügt, die die XML-Struktur beschreibt. Dieses Verfahren zeigt Ihnen, wie Sie Daten aus einer XML-Datei lesen.

1. Erstellen Sie im Ordner *App-Daten\_* eine neue XML-Datei mit dem Namen *data.xml*.
2. Ersetzen Sie das vorhandene XML durch Folgendes, d. h. einige XML-Daten über Mitarbeiter in einem fiktiven Unternehmen. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. Erstellen Sie im Ordner *App-Daten\_* eine neue XML-Datei mit dem Namen *data.xsd*. (Beachten Sie, dass die Erweiterung dieses Mal *.xsd*.)
4. Ersetzen Sie die vorhandene XML-Datei durch Folgendes: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. Erstellen Sie im Stammverzeichnis der Website eine neue Datei mit dem Namen *ChartDataXML.cshtml*.
6. Ersetzen Sie den vorhandenen Inhalt durch Folgendes: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Der Code erstellt `DataSet` zuerst ein Objekt. Dieses Objekt wird verwendet, um die aus der XML-Datei gelesenen Daten zu verwalten und entsprechend den Informationen in der Schemadatei zu organisieren. (Beachten Sie, dass der obere `using SystemData`Rand des Codes die Anweisung enthält. Dies ist erforderlich, um mit `DataSet` dem Objekt arbeiten zu können. Weitere Informationen finden Sie unter [ &quot;Verwenden von&quot; Anweisungen und vollständig qualifizierten Namen](#SB_UsingStatements) weiter unten in diesem Artikel.)

    Als Nächstes erstellt `DataView` der Code ein Objekt basierend auf dem Dataset. Die Datenansicht stellt ein Objekt bereit, das das Diagramm an &#8212; das heißt, lesen und plotieren kann. Das Diagramm bindet mithilfe der `AddSeries` Methode an die Daten, wie Sie zuvor beim `xValue` Diagrammieren der Arraydaten gesehen haben, mit der Ausnahme, dass dieses Mal die und `yValues` die Parameter auf das `DataView` Objekt festgelegt werden.

    In diesem Beispiel wird auch gezeigt, wie Sie einen bestimmten Diagrammtyp angeben. Wenn die Daten in `AddSeries` der `chartType` Methode hinzugefügt werden, wird der Parameter auch so eingestellt, dass ein Kreisdiagramm angezeigt wird.
7. Führen Sie die Seite in einem Browser aus. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Verwenden" von Anweisungen und vollqualifizierten Namen
> 
> Das .NET Framework, auf dem ASP.NET Webseiten mit Razor-Syntax basiert, besteht aus vielen Tausenden von Komponenten (Klassen). Damit es mit all diesen Klassen zu arbeiten ist, sind sie in *Namespaces*organisiert, die ein wenig wie Bibliotheken sind. Der `System.Web` Namespace enthält beispielsweise Klassen, die die `System.Xml` Browser-/Serverkommunikation unterstützen, der Namespace enthält `System.Data` Klassen, die zum Erstellen und Lesen von XML-Dateien verwendet werden, und der Namespace enthält Klassen, mit denen Sie mit Daten arbeiten können.
> 
> Um auf eine bestimmte Klasse in .NET Framework zugreifen zu können, muss Code nicht nur den Klassennamen, sondern auch den Namespace kennen, in dem sich die Klasse befindet. `Chart` Um den Helfer verwenden zu können, muss Code `System.Web.Helpers.Chart` beispielsweise die Klasse finden, die den Namespace (`System.Web.Helpers`) mit dem Klassennamen (`Chart`) kombiniert. Dies wird als *vollständig qualifizierter* Name der Klasse bezeichnet, &#8212; ihre vollständige, eindeutige Position innerhalb der Weite von .NET Framework. Im Code würde dies wie folgt aussehen:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Es ist jedoch umständlich (und fehleranfällig), diese langen, vollqualifizierten Namen jedes Mal verwenden zu müssen, wenn Sie auf eine Klasse oder einen Helfer verweisen möchten. Um die Verwendung von Klassennamen zu vereinfachen, können Sie daher die Namespaces *importieren,* die Sie interessieren. Wenn Sie einen Namespace importiert haben, können Sie`Chart`nur einen Klassennamen`System.Web.Helpers.Chart`( ) anstelle des vollqualifizierten Namens ( ) verwenden. Wenn Ihr Code ausgeführt wird und auf einen Klassennamen trifft, kann er nur in den Namensräumen suchen, die Sie importiert haben, um diese Klasse zu finden.
> 
> Wenn Sie ASP.NET Webseiten mit Razor-Syntax zum Erstellen von Webseiten verwenden, verwenden `WebPage` Sie in der Regel jedes Mal denselben Satz von Klassen, einschließlich der Klasse, der verschiedenen Hilfsprogramme usw. Um Ihnen die Arbeit beim Importieren der relevanten Namespaces zu ersparen, wird bei jedem Erstellen einer Website ASP.NET so konfiguriert, dass automatisch eine Reihe von Kernnamespaces für jede Website importiert wird. Aus diesem Grund mussten Sie sich bisher nicht mit Namespaces oder Importen befassen. Alle Klassen, mit denen Sie gearbeitet haben, befinden sich in Namespaces, die bereits für Sie importiert wurden.
> 
> Manchmal müssen Sie jedoch mit einer Klasse arbeiten, die sich nicht in einem Namespace befindet, der automatisch für Sie importiert wird. In diesem Fall können Sie entweder den vollqualifizierten Namen dieser Klasse verwenden oder den Namespace, der die Klasse enthält, manuell importieren. Zum Importieren eines Namespace `using` verwenden`import` Sie die Anweisung (in Visual Basic), wie Sie in einem Beispiel zuvor im Artikel gesehen haben.
> 
> Die `DataSet` Klasse befindet sich `System.Data` z. B. im Namespace. Der `System.Data` Namespace ist nicht automatisch für ASP.NET Razor-Seiten verfügbar. Um mit der `DataSet` Klasse mit ihrem vollqualifizierten Namen zu arbeiten, können Sie daher Code wie folgt verwenden:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> Wenn Sie die `DataSet` Klasse wiederholt verwenden müssen, können Sie einen Namespace wie diesen importieren und dann nur den Klassennamen im Code verwenden:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Sie können `using` Anweisungen für alle anderen .NET Framework-Namespaces hinzufügen, auf die Sie verweisen möchten. Wie bereits erwähnt, müssen Sie dies jedoch nicht häufig tun, da sich die meisten Klassen, mit denen Sie arbeiten, in Namespaces befinden, die automatisch von ASP.NET für die Verwendung in *.cshtml-* und *VBhtml-Seiten* importiert werden.

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Anzeigen von Diagrammen innerhalb einer Webseite

In den Beispielen, die Sie bisher gesehen haben, erstellen Sie ein Diagramm, und dann wird das Diagramm direkt im Browser als Grafik gerendert. In vielen Fällen möchten Sie jedoch ein Diagramm als Teil einer Seite anzeigen, nicht nur von selbst im Browser. Dazu ist ein zweistufiger Prozess erforderlich. Der erste Schritt besteht darin, eine Seite zu erstellen, die das Diagramm generiert, wie Sie bereits gesehen haben.

Der zweite Schritt besteht darin, das resultierende Bild auf einer anderen Seite anzuzeigen. Um das Bild anzuzeigen, `<img>` verwenden Sie ein HTML-Element auf die gleiche Weise, wie Sie jedes Bild anzeigen würden. Anstatt jedoch auf eine *.jpg-* oder *.png-Datei* zu verweisen, verweist das `<img>` Element auf die *.cshtml-Datei,* die den `Chart` Helfer enthält, der das Diagramm erstellt. Wenn die Anzeigeseite `<img>` ausgeführt wird, ruft `Chart` das Element die Ausgabe des Helfers ab und rendert das Diagramm.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. Erstellen Sie eine Datei mit dem Namen *ShowChart.cshtml*.
2. Ersetzen Sie den vorhandenen Inhalt durch Folgendes: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Der Code `<img>` verwendet das Element, um das Diagramm anzuzeigen, das Sie zuvor in der Datei *ChartArrayBasic.cshtml* erstellt haben.
3. Führen Sie die Webseite in einem Browser aus. Die Datei *ShowChart.cshtml* zeigt das Diagrammbild basierend auf dem Code an, der in der Datei *ChartArrayBasic.cshtml* enthalten ist.

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Styling eines Diagramms

Der `Chart` Helfer unterstützt eine große Anzahl von Optionen, mit denen Sie die Darstellung des Diagramms anpassen können. Sie können Farben, Schriftarten, Rahmen usw. festlegen. Eine einfache Möglichkeit, die Darstellung eines Diagramms anzupassen, ist die Verwendung eines *Themas*. Designs sind Informationssammlungen, die angeben, wie ein Diagramm mithilfe von Schriftarten, Farben, Beschriftungen, Paletten, Rahmen und Effekten gerendert wird. (Beachten Sie, dass der Stil eines Diagramms nicht den Diagrammtyp angibt.)

In der folgenden Tabelle sind integrierte Designs aufgeführt.

| Design | BESCHREIBUNG |
| --- | --- |
| `Vanilla` | Zeigt rote Spalten auf weißem Hintergrund an. |
| `Blue` | Zeigt blaue Spalten auf einem blauen Farbverlaufshintergrund an. |
| `Green` | Zeigt blaue Spalten auf einem grünen Farbverlaufshintergrund an. |
| `Yellow` | Zeigt orangefarbene Spalten auf einem gelben Farbverlaufshintergrund an. |
| `Vanilla3D` | Zeigt rote 3D-Spalten auf weißem Hintergrund an. |

Sie können das Design angeben, das beim Erstellen eines neuen Diagramms verwendet werden soll.

1. Erstellen Sie eine neue Datei mit dem Namen *ChartStyleGreen.cshtml*.
2. Ersetzen Sie den vorhandenen Inhalt auf der Seite durch Folgendes:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Dieser Code ist derselbe wie das frühere Beispiel, das `theme` die Datenbank für `Chart` Daten verwendet, aber den Parameter hinzufügt, wenn er das Objekt erstellt. Im Folgenden wird der geänderte Code angezeigt:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Führen Sie die Seite in einem Browser aus. Sie sehen die gleichen Daten wie zuvor, aber das Diagramm sieht polierter aus: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Speichern eines Diagramms

Wenn Sie `Chart` den Helfer verwenden, wie Sie es bisher in diesem Artikel gesehen haben, erstellt der Helfer das Diagramm bei jedem Aufruf von Grund auf neu. Bei Bedarf fragt der Code für das Diagramm auch die Datenbank erneut ab oder liest die XML-Datei erneut, um die Daten abzurufen. In einigen Fällen kann dies ein komplexer Vorgang sein, z. B. wenn die Datenbank, die Sie abfragen, groß ist oder wenn die XML-Datei viele Daten enthält. Auch wenn das Diagramm nicht viele Daten enthält, erfordert das dynamische Erstellen eines Bildes Serverressourcen, und wenn viele Personen die Seite oder seiten anfordern, die das Diagramm anzeigen, kann dies Auswirkungen auf die Leistung Ihrer Website haben.

Um die potenziellen Auswirkungen des Erstellens eines Diagramms auf die Leistung zu verringern, können Sie ein Diagramm erstellen, wenn Sie es zum ersten Mal benötigen, und es dann speichern. Wenn das Diagramm erneut benötigt wird, anstatt es zu regenerieren, können Sie einfach die gespeicherte Version abrufen und rendern.

Sie können ein Diagramm auf folgende Weise speichern:

- Zwischenspeichern Sie das Diagramm im Computerspeicher (auf dem Server).
- Speichern Sie das Diagramm als Bilddatei.
- Speichern Sie das Diagramm als XML-Datei. Mit dieser Option können Sie das Diagramm ändern, bevor Sie es speichern.

### <a name="caching-a-chart"></a>Zwischenspeichern eines Diagramms

Nachdem Sie ein Diagramm erstellt haben, können Sie es zwischenspeichern. Das Zwischenspeichern eines Diagramms bedeutet, dass es nicht neu erstellt werden muss, wenn es erneut angezeigt werden muss. Wenn Sie ein Diagramm im Cache speichern, geben Sie ihm einen Schlüssel, der für dieses Diagramm eindeutig sein muss.

Im Cache gespeicherte Diagramme werden möglicherweise entfernt, wenn auf dem Server nicht mehr arbeitsspeicherabhängig ist. Darüber hinaus wird der Cache gelöscht, wenn die Anwendung aus irgendeinem Grund neu gestartet wird. Daher besteht die Standardmethode, mit einem zwischengespeicherten Diagramm zu arbeiten, darin, immer zuerst zu überprüfen, ob es im Cache verfügbar ist, und wenn nicht, und dann zu erstellen oder neu zu erstellen.

1. Erstellen Sie im Stammverzeichnis Ihrer Website eine Datei mit dem Namen *ShowCachedChart.cshtml*.
2. Ersetzen Sie den vorhandenen Inhalt durch Folgendes: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    Das `<img>` Tag `src` enthält ein Attribut, das auf die Datei *ChartSaveToCache.cshtml* verweist und einen Schlüssel als Abfragezeichenfolge an die Seite übergibt. Der Schlüssel enthält &quot;den&quot;Wert myChartKey . Die Datei *ChartSaveToCache.cshtml* enthält den `Chart` Helfer, der das Diagramm erstellt. Sie erstellen diese Seite gleich.

    Am Ende der Seite befindet sich ein Link zu einer Seite mit dem Namen *ClearCache.cshtml*. Das ist eine Seite, die Sie auch in Kürze erstellen werden. Sie benötigen *ClearCache.cshtml* nur, um die Zwischenspeicherung für dieses Beispiel zu testen – es ist kein Link oder eine Seite, die Sie normalerweise bei der Arbeit mit zwischengespeicherten Diagrammen einschließen würden.
3. Erstellen Sie im Stammverzeichnis Ihrer Website eine neue Datei mit dem Namen *ChartSaveToCache.cshtml*.
4. Ersetzen Sie den vorhandenen Inhalt durch Folgendes:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Der Code überprüft zunächst, ob etwas als Schlüsselwert in der Abfragezeichenfolge übergeben wurde. Wenn dies der Fall ist, versucht der Code, ein Diagramm aus dem Cache zu lesen, indem er die `GetFromCache` Methode aufruft und den Schlüssel übergibt. Wenn sich herausstellt, dass sich unter diesem Schlüssel nichts im Cache befindet (was beim ersten Abfragen des Diagramms passieren würde), erstellt der Code das Diagramm wie gewohnt. Wenn das Diagramm fertig ist, speichert der `SaveToCache`Code es im Cache, indem er aufruft. Diese Methode erfordert einen Schlüssel (damit das Diagramm später angefordert werden kann) und die Zeit, die das Diagramm im Cache speichern soll. (Die genaue Zeit, zu der Sie ein Diagramm zwischenspeichern würden, hängt davon ab, wie oft sich die Daten ändern könnten.) Die `SaveToCache` Methode erfordert `slidingExpiration` auch einen Parameter&#8212; wenn dieser wert ist, wird der Timeoutzähler bei jedem Zugriff auf das Diagramm zurückgesetzt. In diesem Fall bedeutet dies, dass der Cacheeintrag des Diagramms 2 Minuten nach dem letzten Zugriff einer Person auf das Diagramm abläuft. (Die Alternative zum gleitenden Ablauf ist der absolute Ablauf, d. h., der Cacheeintrag würde genau 2 Minuten nach seiner Einlage in den Cache ablaufen, unabhängig davon, wie oft darauf zugegriffen wurde.)

    Schließlich verwendet der `WriteFromCache` Code die Methode zum Abrufen und Rendern des Diagramms aus dem Cache. Beachten Sie, dass `if` sich diese Methode außerhalb des Blocks befindet, der den Cache überprüft, da das Diagramm aus dem Cache abholt, unabhängig davon, ob das Diagramm zunächst vorhanden war oder generiert und im Cache gespeichert werden musste.

    Beachten Sie, dass `AddTitle` die Methode im Beispiel einen Zeitstempel enthält. (Es fügt das aktuelle `DateTime.Now` Datum und die aktuelle Uhrzeit &#8212; &#8212; zum Titel hinzu.)
5. Erstellen Sie eine neue Seite mit dem Namen *ClearCache.cshtml,* und ersetzen Sie ihren Inhalt durch Folgendes:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Diese Seite `WebCache` verwendet den Helfer, um das Diagramm zu entfernen, das in *ChartSaveToCache.cshtml*zwischengespeichert ist. Wie bereits erwähnt, müssen Sie normalerweise keine solche Seite haben. Sie erstellen es hier nur, um das Zwischenspeichern zu vereinfachen.
6. Führen Sie die Webseite *ShowCachedChart.cshtml* in einem Browser aus. Auf der Seite wird das Diagrammbild basierend auf dem Code angezeigt, der in der Datei *ChartSaveToCache.cshtml* enthalten ist. Beachten Sie, was der Zeitstempel im Diagrammtitel sagt. 

    ![Beschreibung: Bild des Basisdiagramms mit Zeitstempel im Diagrammtitel](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Schließen Sie den Browser.
8. Führen Sie *ShowCachedChart.cshtml* erneut aus. Beachten Sie, dass der Zeitstempel derselbe ist wie zuvor, was darauf hinweist, dass das Diagramm nicht regeneriert wurde, sondern aus dem Cache gelesen wurde.
9. Klicken Sie in *ShowCachedChart.cshtml*auf den Link **Cache löschen.** Dadurch werden Sie zu *ClearCache.cshtml*, das meldet, dass der Cache gelöscht wurde.
10. Klicken Sie auf den Link **Zurück zu ShowCachedChart.cshtml,** oder führen Sie *ShowCachedChart.cshtml* von WebMatrix erneut aus. Beachten Sie, dass sich der Zeitstempel dieses Mal geändert hat, da der Cache gelöscht wurde. Daher musste der Code das Diagramm regenerieren und wieder in den Cache speichern.

### <a name="saving-a-chart-as-an-image-file"></a>Speichern eines Diagramms als Bilddatei

Sie können ein Diagramm auch als Bilddatei (z. B. als *JPG-Datei)* auf dem Server speichern. Sie können dann die Bilddatei so verwenden, wie Sie es bei jedem Bild tun würden. Der Vorteil ist, dass die Datei gespeichert und nicht in einem temporären Cache gespeichert wird. Sie können ein neues Diagrammbild zu unterschiedlichen Zeiten (z. B. stündlich) speichern und dann die Änderungen, die im Laufe der Zeit auftreten, permanent aufzeichnen. Beachten Sie, dass Sie sicherstellen müssen, dass Ihre Webanwendung über die Berechtigung zum Speichern einer Datei in dem Ordner auf dem Server verfügt, auf dem Sie die Bilddatei absetzen möchten.

1. Erstellen Sie im Stammverzeichnis Ihrer Website einen Ordner mit dem Namen * \_ChartFiles,* falls dieser noch nicht vorhanden ist.
2. Erstellen Sie im Stammverzeichnis Ihrer Website eine neue Datei mit dem Namen *ChartSave.cshtml*.
3. Ersetzen Sie den vorhandenen Inhalt durch Folgendes:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Der Code überprüft zuerst, ob die *JPG-Datei* vorhanden ist, indem die Methode aufgerufen wird. `File.Exists` Wenn die Datei nicht vorhanden ist, `Chart` erstellt der Code ein neues aus einem Array. Diesmal ruft der Code `Save` die Methode `path` auf und übergibt den Parameter, um den Dateipfad und den Dateinamen anzugeben, wo das Diagramm gespeichert werden soll. Im Textkörper der Seite `<img>` verwendet ein Element den Pfad, um auf die anzuzeigende *JPG-Datei* zu verweisen.
4. Führen Sie die Datei *ChartSave.cshtml* aus.
5. Zurück zu WebMatrix. Beachten Sie, dass eine Bilddatei mit dem Namen *chart01.jpg* im * \_* Ordner ChartFiles gespeichert wurde.

### <a name="saving-a-chart-as-an-xml-file"></a>Speichern eines Diagramms als XML-Datei

Schließlich können Sie ein Diagramm als XML-Datei auf dem Server speichern. Ein Vorteil der Verwendung dieser Methode gegenüber dem Zwischenspeichern des Diagramms oder dem Speichern des Diagramms in einer Datei besteht darin, dass Sie den XML-Code ändern können, bevor Sie das Diagramm anzeigen, wenn Sie möchten. Ihre Anwendung muss über Lese-/Schreibberechtigungen für den Ordner auf dem Server verfügen, auf dem Sie die Bilddatei ablegen möchten.

1. Erstellen Sie im Stammverzeichnis Ihrer Website eine neue Datei mit dem Namen *ChartSaveXml.cshtml*.
2. Ersetzen Sie den vorhandenen Inhalt durch Folgendes:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Dieser Code ähnelt dem Code, den Sie zuvor zum Speichern eines Diagramms im Cache gesehen haben, mit der Ausnahme, dass eine XML-Datei verwendet wird. Der Code überprüft zunächst, ob die XML-Datei vorhanden ist, indem die Methode aufgerufen wird. `File.Exists` Wenn die Datei vorhanden ist, `Chart` erstellt der Code ein `themePath` neues Objekt und übergibt den Dateinamen als Parameter. Dadurch wird das Diagramm basierend auf dem in der XML-Datei gespeicherten Diagramm erstellt. Wenn die XML-Datei noch nicht vorhanden ist, erstellt der `SaveXml` Code ein Diagramm wie normal und ruft es dann auf, um es zu speichern. Das Diagramm wird mit `Write` der Methode gerendert, wie Sie zuvor gesehen haben.

    Wie bei der Seite, die zwischenspeichern zeigte, enthält dieser Code einen Zeitstempel im Diagrammtitel.
3. Erstellen Sie eine neue Seite mit dem Namen *ChartDisplayXMLChart.cshtml,* und fügen Sie ihr das folgende Markup hinzu: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. Führen Sie die Seite *ChartDisplayXMLChart.cshtml* aus. Das Diagramm wird angezeigt. Beachten Sie den Zeitstempel im Titel des Diagramms.
5. Schließen Sie den Browser.
6. Klicken Sie in WebMatrix mit der **Refresh**rechten Maustaste auf den * \_Ordner ChartFiles,* klicken Sie auf Aktualisieren , und öffnen Sie dann den Ordner. Die Datei *XMLChart.xml* in diesem `Chart` Ordner wurde vom Helfer erstellt. 

    ![Beschreibung: Der _ChartFiles Ordner mit der Datei XMLChart.xml, die vom Chart-Helfer erstellt wurde.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. Führen Sie die Seite *ChartDisplayXMLChart.cshtml* erneut aus. Das Diagramm zeigt den gleichen Zeitstempel wie beim ersten Führte der Seite. Das liegt daran, dass das Diagramm aus dem zuvor gespeicherten XML generiert wird.
8. Öffnen Sie in * \_* WebMatrix den Ordner ChartFiles, und löschen Sie die Datei *XMLChart.xml.*
9. Führen Sie die Seite *ChartDisplayXMLChart.cshtml* erneut aus. Diesmal wird der Zeitstempel aktualisiert, `Chart` da der Helfer die XML-Datei neu erstellen musste. Wenn Sie möchten, überprüfen Sie den * \_Ordner ChartFiles,* und beachten Sie, dass die XML-Datei wieder vorhanden ist.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Weitere Ressourcen

- [Einführung in das Arbeiten mit einer Datenbank in ASP.NET Webseiten-Websites](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Verwenden von Caching in ASP.NET Webseiten-Websites zur Verbesserung der Leistung](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Diagrammklasse](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (ASP.NET Webseiten-API-Referenz auf MSDN)
