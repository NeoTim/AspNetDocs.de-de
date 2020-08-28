---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
title: Verwenden von SQL-Cache Abhängigkeiten (c#) | Microsoft-Dokumentation
author: rick-anderson
description: Die einfachste Strategie zum Zwischenspeichern besteht darin, die zwischengespeicherten Daten nach einem bestimmten Zeitraum ablaufen zu lassen. Diese einfache Vorgehensweise bedeutet aber, dass die zwischengespeicherten Daten maintai...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 0e91842c-7f10-4aed-8c23-4ee3e2774014
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-cs
msc.type: authoredcontent
ms.openlocfilehash: 6a039cdfb1da294744b92648386468f69193ae6b
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045259"
---
# <a name="using-sql-cache-dependencies-c"></a>Verwenden von SQL-Cacheabhängigkeiten (C#)

von [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Code herunterladen](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_CS.zip) oder [PDF herunterladen](using-sql-cache-dependencies-cs/_static/datatutorial61cs1.pdf)

> Die einfachste Strategie zum Zwischenspeichern besteht darin, die zwischengespeicherten Daten nach einem bestimmten Zeitraum ablaufen zu lassen. Diese einfache Vorgehensweise bedeutet aber, dass die zwischengespeicherten Daten nicht mit der zugrunde liegenden Datenquelle zusammengeführt werden. Dies führt zu veralteten Daten, die zu lange dauern, oder aktuelle Daten, die zu bald abgelaufen sind. Ein besserer Ansatz ist die Verwendung der sqlcachedepend-Klasse, damit die Daten zwischengespeichert bleiben, bis die zugrunde liegenden Daten in der SQL-Datenbank geändert wurden. In diesem Tutorial erfahren Sie, wie.

## <a name="introduction"></a>Einführung

Die zwischen Speicherungs Techniken, die unter zwischen [Speichern von Daten mit der ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) und zwischen [Speichern von Daten in den Architektur](caching-data-in-the-architecture-cs.md) Lernprogrammen untersucht wurden, verwendeten einen zeitbasierten Ablauf, um die Daten aus dem Cache nach einem bestimmten Zeitraum zu entfernen. Diese Vorgehensweise ist die einfachste Methode, um die Leistungssteigerungen der Zwischenspeicherung gegen Daten Veraltung auszugleichen. Durch die Auswahl eines Zeitverlaufs von *x* Sekunden gibt ein Seiten Entwickler an, dass Sie die Leistungsvorteile der Zwischenspeicherung nur für *x* Sekunden genießen, aber Sie können sich darauf verlassen, dass Ihre Daten nie länger als maximal *x* Sekunden abgelaufen sind. Natürlich kann *x* für statische Daten auf die Lebensdauer der Webanwendung erweitert werden, wie im Tutorial zwischen [Speichern von Daten beim Anwendungsstart](caching-data-at-application-startup-cs.md) untersucht.

Beim Zwischenspeichern von Datenbankdaten wird häufig eine zeitbasierte Ablaufzeit für die einfache Verwendung ausgewählt, aber häufig eine unzureichende Lösung. Im Idealfall bleiben die Datenbankdaten so lange zwischengespeichert, bis die zugrunde liegenden Daten in der Datenbank geändert wurden. nur dann würde der Cache entfernt werden. Durch diese Vorgehensweise werden die Leistungsvorteile der Zwischenspeicherung maximiert und die Dauer veralteter Daten minimiert. Um diese Vorteile nutzen zu können, muss jedoch ein System vorhanden sein, das weiß, wann die zugrunde liegenden Datenbankdaten geändert wurden, und die entsprechenden Elemente aus dem Cache entfernt werden. Vor ASP.NET 2,0 waren Seiten Entwickler für die Implementierung dieses Systems verantwortlich.

ASP.NET 2,0 stellt eine- [ `SqlCacheDependency` Klasse](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx) und die erforderliche-Infrastruktur bereit, um zu bestimmen, wann eine Änderung in der Datenbank aufgetreten ist, sodass die entsprechenden zwischengespeicherten Elemente entfernt werden können. Es gibt zwei Verfahren, um zu bestimmen, wann sich die zugrunde liegenden Daten geändert haben: Benachrichtigung und Abruf. Nach der Erörterung der Unterschiede zwischen Benachrichtigung und Abruf erstellen wir die Infrastruktur, die für die Unterstützung von Abruf erforderlich ist, und untersuchen dann die Verwendung der `SqlCacheDependency` -Klasse in deklarativen und programmgesteuerten Szenarien.

## <a name="understanding-notification-and-polling"></a>Informationen zu Benachrichtigungen und Abruf

Es gibt zwei Techniken, mit denen bestimmt werden kann, wann die Daten in einer Datenbank geändert wurden: Benachrichtigung und Abruf. Bei der Benachrichtigung wird die ASP.NET-Laufzeit automatisch von der Datenbank benachrichtigt, wenn die Ergebnisse einer bestimmten Abfrage seit der letzten Ausführung der Abfrage geändert wurden. zu diesem Zeitpunkt werden die der Abfrage zugeordneten zwischengespeicherten Elemente entfernt. Beim Abrufen behält der Datenbankserver Informationen darüber bei, wann bestimmte Tabellen zuletzt aktualisiert wurden. Die ASP.NET-Laufzeit fragt regelmäßig die Datenbank ab, um zu überprüfen, welche Tabellen geändert wurden, seit Sie in den Cache eingegeben wurden. Bei den Tabellen, deren Daten geändert wurden, werden die zugehörigen Cache Elemente entfernt.

Die Benachrichtigungs Option erfordert weniger Setup als Abruf und ist präziser, da Änderungen auf Abfrage Ebene und nicht auf Tabellenebene nachverfolgt werden. Leider sind Benachrichtigungen nur in den vollständigen Editionen von Microsoft SQL Server 2005 verfügbar (d. h. die nicht-Express-Editionen). Die Abruf Option kann jedoch für alle Versionen von Microsoft SQL Server von 7,0 bis 2005 verwendet werden. Da in diesen Tutorials die Express Edition von SQL Server 2005 verwendet wird, konzentrieren wir uns auf das Einrichten und Verwenden der Abruf Option. Weitere Informationen zu SQL Server von Benachrichtigungsfunktionen von 2005 s finden Sie im Abschnitt weiter unten in diesem Tutorial.

Beim Abrufen muss die Datenbank so konfiguriert werden, dass Sie eine Tabelle mit dem Namen enthält, `AspNet_SqlCacheTablesForChangeNotification` die drei Spalten enthält: `tableName` , `notificationCreated` und `changeId` . Diese Tabelle enthält eine Zeile für jede Tabelle, die Daten enthält, die möglicherweise in einer SQL-Cache Abhängigkeit in der-Webanwendung verwendet werden müssen. Die- `tableName` Spalte gibt den Namen der Tabelle an `notificationCreated` , während das Datum und die Uhrzeit angibt, zu der die Zeile der Tabelle hinzugefügt wurde. Die `changeId` Spalte ist vom Datentyp `int` und hat den Anfangswert 0. Der Wert wird bei jeder Änderung der Tabelle inkrementiert.

Zusätzlich zur- `AspNet_SqlCacheTablesForChangeNotification` Tabelle muss die Datenbank auch Trigger für jede der Tabellen enthalten, die möglicherweise in einer SQL-Cache Abhängigkeit angezeigt werden. Diese Trigger werden immer dann ausgeführt, wenn eine Zeile eingefügt, aktualisiert oder gelöscht und der Wert der Tabelle `changeId` in erhöht wird `AspNet_SqlCacheTablesForChangeNotification` .

Die ASP.NET-Laufzeit verfolgt den aktuellen `changeId` für eine Tabelle, wenn Daten mit einem-Objekt zwischengespeichert werden `SqlCacheDependency` . Die Datenbank wird in regelmäßigen Abständen überprüft, und alle `SqlCacheDependency` Objekte `changeId` , deren Werte von dem Wert in der Datenbank abweichen, werden entfernt, da ein abweichender `changeId` Wert angibt, dass seit der Zwischenspeicherung der Daten eine Änderung an der Tabelle vorgenommen wurde.

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>Schritt 1: Untersuchen des `aspnet_regsql.exe` Befehlszeilen Programms

Beim Abruf Ansatz muss die Datenbank so eingerichtet werden, dass Sie die oben beschriebene Infrastruktur enthält: eine vordefinierte Tabelle ( `AspNet_SqlCacheTablesForChangeNotification` ), eine Handvoll gespeicherter Prozeduren und Trigger für jede Tabelle, die in SQL-Cache Abhängigkeiten in der Webanwendung verwendet werden kann. Diese Tabellen, gespeicherten Prozeduren und Trigger können über das Befehlszeilenprogramm erstellt werden `aspnet_regsql.exe` , das sich im `$WINDOWS$\Microsoft.NET\Framework\version` Ordner befindet. Um die `AspNet_SqlCacheTablesForChangeNotification` Tabelle und die zugehörigen gespeicherten Prozeduren zu erstellen, führen Sie den folgenden Befehl über die Befehlszeile aus:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample1.cmd)]

> [!NOTE]
> Um diese Befehle auszuführen, muss die angegebene Daten Bank Anmeldung in [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) den [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) Rollen und erfolgen. Weitere Informationen zum Überprüfen von T-SQL, das über das Befehlszeilenprogramm an die Datenbank gesendet `aspnet_regsql.exe` wird, finden Sie in [diesem Blogeintrag](http://scottonwriting.net/sowblog/posts/10709.aspx).

Wenn Sie z. b. die Infrastruktur zum Abrufen einer Microsoft SQL Server Datenbank mit dem Namen `pubs` auf einem Daten Bank Server mit dem Namen mithilfe der Windows-Authentifizierung hinzufügen möchten `ScottsServer` , navigieren Sie zum entsprechenden Verzeichnis, und geben Sie in der Befehlszeile Folgendes ein:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample2.cmd)]

Nachdem die Infrastruktur auf Datenbankebene hinzugefügt wurde, müssen die Trigger den Tabellen hinzugefügt werden, die in SQL-Cache Abhängigkeiten verwendet werden. Verwenden `aspnet_regsql.exe` Sie das Befehlszeilenprogramm erneut, aber geben Sie den Tabellennamen mithilfe des `-t` -Schalters und anstelle der `-ed` Verwendung des Schalters wie folgt an `-et` :

[!code-html[Main](using-sql-cache-dependencies-cs/samples/sample3.html)]

Zum Hinzufügen der Trigger zu den `authors` -und-Tabellen der-Datenbank in verwenden Sie Folgendes `titles` `pubs` `ScottsServer` :

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample4.cmd)]

Fügen Sie für dieses Tutorial die Trigger zu `Products` den `Categories` Tabellen, und hinzu `Suppliers` . Wir sehen uns die Befehlszeilen Syntax in Schritt 3 an.

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>Schritt 2: verweisen auf eine Microsoft SQL Server 2005 Express Edition-Datenbank in`App_Data`

Das `aspnet_regsql.exe` Befehlszeilenprogramm erfordert den Datenbank-und Servernamen, um die erforderliche Abruf Infrastruktur hinzuzufügen. Aber wie lautet der Datenbank-und Servername für eine Microsoft SQL Server 2005 Express-Datenbank, die sich im `App_Data` Ordner befindet? Anstatt zu ermitteln, was die Datenbank-und Servernamen sind, habe ich festgestellt, dass der einfachste Ansatz darin besteht, die Datenbank an die `localhost\SQLExpress` Daten Bank Instanz anzufügen und die Daten mit [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)umzubenennen. Wenn eine der Vollversionen von SQL Server 2005 auf Ihrem Computer installiert ist, haben Sie wahrscheinlich bereits SQL Server Management Studio auf dem Computer installiert. Wenn Sie nur über die Express Edition verfügen, können Sie die kostenlose [Microsoft SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)herunterladen.

Beginnen Sie mit dem Schließen von Visual Studio. Öffnen Sie als nächstes SQL Server Management Studio, und wählen Sie mithilfe der Windows-Authentifizierung eine Verbindung mit dem Server herstellen aus `localhost\SQLExpress` .

![Anfügen an den localhost\SQLExpress-Server](using-sql-cache-dependencies-cs/_static/image1.gif)

**Abbildung 1**: Anfügen an den `localhost\SQLExpress` Server

Nach dem Herstellen einer Verbindung mit dem Server zeigt Management Studio den Server an und enthält Unterordner für die Datenbanken, Sicherheit usw. Klicken Sie mit der rechten Maustaste auf den Ordner Datenbanken, und wählen Sie die Option anhängen. Dadurch wird das Dialogfeld Datenbanken anfügen angezeigt (siehe Abbildung 2). Klicken Sie auf die Schaltfläche hinzufügen, und wählen Sie den `NORTHWND.MDF` Daten Bank Ordner im Ordner Ihrer Webanwendung `App_Data` .

[![Fügen Sie das Northwnd an. MDF-Datenbank aus dem Ordner "App_Data"](using-sql-cache-dependencies-cs/_static/image2.gif)](using-sql-cache-dependencies-cs/_static/image1.png)

**Abbildung 2**: Anfügen der `NORTHWND.MDF` Datenbank aus dem `App_Data` Ordner ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image2.png))

Dadurch wird die Datenbank dem Ordner Datenbanken hinzugefügt. Der Datenbankname ist möglicherweise der vollständige Pfad zur Datenbankdatei oder der vollständige Pfad, dem eine [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)vorangesteht ist. Um zu vermeiden, dass Sie diesen langwierigen Datenbanknamen bei Verwendung des ASPNET \_regsql.exe-Befehlszeilen Tools eingeben müssen, benennen Sie die Datenbank in einen benutzerfreundlicheren Namen um, indem Sie mit der rechten Maustaste auf die gerade angefügte Datenbank klicken und Umbenennen auswählen. Ich habe meine Datenbank in "datatutorials" umbenannt.

![Benennen Sie die angefügte Datenbank in einen benutzerfreundlicheren Namen um.](using-sql-cache-dependencies-cs/_static/image3.gif)

**Abbildung 3**: Umbenennen der angefügten Datenbank in einen benutzerfreundlicheren Namen

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>Schritt 3: Hinzufügen der Abruf Infrastruktur zur Northwind-Datenbank

Nachdem die `NORTHWND.MDF` Datenbank nun aus dem `App_Data` Ordner angefügt wurde, können wir die Abruf Infrastruktur hinzufügen. Wenn Sie die Datenbank in datatutorials umbenannt haben, führen Sie die folgenden vier Befehle aus:

[!code-console[Main](using-sql-cache-dependencies-cs/samples/sample5.cmd)]

Nachdem Sie diese vier Befehle ausgeführt haben, klicken Sie in Management Studio mit der rechten Maustaste auf den Datenbanknamen, navigieren Sie zum Untermenü Tasks, und wählen Sie trennen aus. Schließen Sie dann Management Studio, und öffnen Sie Visual Studio erneut.

Nachdem Visual Studio erneut geöffnet wurde, führen Sie einen Drilldown in die Datenbank durch Server-Explorer aus. Beachten Sie die neue Tabelle ( `AspNet_SqlCacheTablesForChangeNotification` ), die neuen gespeicherten Prozeduren und die Trigger in den `Products` `Categories` Tabellen, und `Suppliers` .

![Die Datenbank enthält jetzt die erforderliche Abruf Infrastruktur.](using-sql-cache-dependencies-cs/_static/image4.gif)

**Abbildung 4**: die Datenbank enthält jetzt die erforderliche Abruf Infrastruktur

## <a name="step-4-configuring-the-polling-service"></a>Schritt 4: Konfigurieren des Abruf dienstanweises

Nachdem Sie die erforderlichen Tabellen, Trigger und gespeicherten Prozeduren in der-Datenbank erstellt haben, besteht der letzte Schritt darin, den Abruf Dienst zu konfigurieren. Dies geschieht durch `Web.config` angeben der zu verwendenden Datenbanken und der Abruf Häufigkeit in Millisekunden. Das folgende Markup fragt die Northwind-Datenbank einmal pro Sekunde ab.

[!code-xml[Main](using-sql-cache-dependencies-cs/samples/sample6.xml)]

Der `name` Wert im- `<add>` Element (northwinddb) ordnet einen lesbaren Namen einer bestimmten Datenbank zu. Beim Arbeiten mit SQL-Cache Abhängigkeiten müssen wir auf den hier definierten Datenbanknamen sowie auf die Tabelle verweisen, auf der die zwischengespeicherten Daten basieren. Wir zeigen Ihnen, wie Sie die- `SqlCacheDependency` Klasse verwenden, um den zwischengespeicherten Daten in Schritt 6 Programm gesteuert SQL-Cache Abhängigkeiten zuzuordnen.

Nachdem eine SQL-Cache Abhängigkeit hergestellt wurde, stellt das Abrufsystem eine Verbindung mit den Datenbanken her, die in den `<databases>` Elementen alle Millisekunden definiert sind, `pollTime` und führt die `AspNet_SqlCachePollingStoredProcedure` gespeicherte Prozedur aus. Diese gespeicherte Prozedur, die in Schritt 3 mithilfe des Befehlszeilen Tools hinzugefügt wurde, `aspnet_regsql.exe` gibt den- `tableName` Wert und den- `changeId` Wert für jeden Datensatz in zurück `AspNet_SqlCacheTablesForChangeNotification` . Veraltete SQL-Cache Abhängigkeiten werden aus dem Cache entfernt.

Die `pollTime` Einstellung führt zu einem Kompromiss zwischen Leistung und Daten Veraltung. Ein kleiner `pollTime` Wert erhöht die Anzahl der Anforderungen an die Datenbank, aber es werden schneller veraltete Daten aus dem Cache entfernt. Ein größerer `pollTime` Wert reduziert die Anzahl von Datenbankanforderungen, erhöht jedoch die Verzögerung zwischen dem Zeitpunkt, zu dem die Back-End-Daten geändert werden, und dem Entfernen der zugehörigen Cache Elemente. Glücklicherweise führt die Daten Bank Anforderung eine einfache gespeicherte Prozedur aus, die nur wenige Zeilen aus einer einfachen, einfachen Tabelle zurückgibt. Experimentieren Sie jedoch mit unterschiedlichen `pollTime` Werten, um ein optimales Gleichgewicht zwischen Datenbankzugriff und Daten Veraltung für Ihre Anwendung zu finden. Der kleinste `pollTime` zulässige Wert ist 500.

> [!NOTE]
> Im obigen Beispiel wird ein einzelner `pollTime` Wert im- `<sqlCacheDependency>` Element bereitstellt, aber Sie können optional auch den `pollTime` Wert im- `<add>` Element angeben. Dies ist hilfreich, wenn Sie mehrere Datenbanken angegeben haben und die Abruf Häufigkeit pro Datenbank anpassen möchten.

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>Schritt 5: Deklaratives arbeiten mit SQL-Cache Abhängigkeiten

In den Schritten 1 bis 4 haben wir uns mit dem Einrichten der erforderlichen Datenbankinfrastruktur und der Konfiguration des Abruf Systems beschäftigt. Mit dieser Infrastruktur können jetzt dem Daten Cache Elemente mit einer zugehörigen SQL-Cache Abhängigkeit mithilfe Programm gesteuerter oder deklarativer Verfahren hinzugefügt werden. In diesem Schritt untersuchen wir die deklarative Arbeit mit SQL-Cache Abhängigkeiten. In Schritt 6 betrachten wir die programmgesteuerte Vorgehensweise.

Im Tutorial zum zwischen [Speichern von Daten mit dem ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) -Tutorial wurden die deklarativen zwischen Speicherungs Funktionen von ObjectDataSource untersucht. Wenn Sie einfach die `EnableCaching` -Eigenschaft auf `true` und die- `CacheDuration` Eigenschaft auf ein Zeitintervall festlegen, werden die Daten, die vom zugrunde liegenden-Objekt für das angegebene Intervall zurückgegeben werden, von ObjectDataSource automatisch zwischengespeichert. Von ObjectDataSource können auch mindestens eine SQL-Cache Abhängigkeit verwendet werden.

Um die deklarative Verwendung von SQL-Cache Abhängigkeiten zu veranschaulichen, öffnen Sie die `SqlCacheDependencies.aspx` Seite im `Caching` Ordner, und ziehen Sie eine GridView aus der Toolbox auf den Designer. Legen Sie GridView s `ID` auf fest, `ProductsDeclarative` und wählen Sie aus dem smarttagtag aus, dass es an eine neue ObjectDataSource mit dem Namen gebunden werden soll `ProductsDataSourceDeclarative` .

[![Erstellen Sie eine neue ObjectDataSource namens productdatasourcedeclarative.](using-sql-cache-dependencies-cs/_static/image5.gif)](using-sql-cache-dependencies-cs/_static/image3.png)

**Abbildung 5**: Erstellen einer neuen ObjectDataSource namens `ProductsDataSourceDeclarative` ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image4.png))

Konfigurieren Sie ObjectDataSource für die Verwendung der `ProductsBLL` -Klasse, und legen Sie die Dropdown Liste auf der Registerkarte auswählen auf fest `GetProducts()` . Wählen Sie auf der Registerkarte Update die `UpdateProduct` Überladung mit drei Eingabe Parametern aus: `productName` , `unitPrice` und `productID` . Legen Sie die Dropdown Liste auf der Registerkarte Einfügen und löschen auf (keine) fest.

[![Verwenden der UpdateProduct-Überladung mit drei Eingabe Parametern](using-sql-cache-dependencies-cs/_static/image6.gif)](using-sql-cache-dependencies-cs/_static/image5.png)

**Abbildung 6**: Verwenden der UpdateProduct-Überladung mit drei Eingabe Parametern ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image6.png))

[![Legen Sie für die Registerkarten einfügen und löschen die Dropdown Liste auf (keine) fest.](using-sql-cache-dependencies-cs/_static/image7.gif)](using-sql-cache-dependencies-cs/_static/image7.png)

**Abbildung 7**: Festlegen der Dropdown Liste auf (keine) für die Registerkarten "Einfügen" und "Löschen" ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image8.png))

Nach dem Abschließen des Assistenten zum Konfigurieren von Datenquellen erstellt Visual Studio boundfields und checkboxfields in der GridView für jedes der Datenfelder. Entfernen Sie alle Felder `ProductName` ,, `CategoryName` und `UnitPrice` , und formatieren Sie diese Felder wie angezeigt. Aktivieren Sie aus dem GridView s-Smarttag die Kontrollkästchen Paging aktivieren, Sortierung aktivieren und Bearbeiten aktivieren. Die ObjectDataSource s-Eigenschaft wird von Visual Studio auf festgelegt `OldValuesParameterFormatString` `original_{0}` . Damit das Feature "GridView s Edit" ordnungsgemäß funktioniert, entfernen Sie diese Eigenschaft vollständig aus der deklarativen Syntax, oder legen Sie Sie auf den Standardwert zurück `{0}` .

Fügen Sie schließlich über der GridView ein Label-websteuer Element hinzu, und legen Sie dessen `ID` -Eigenschaft auf `ODSEvents` und die- `EnableViewState` Eigenschaft auf fest `false` . Nachdem Sie diese Änderungen vorgenommen haben, sollte das deklarative Markup der Seite in etwa wie folgt aussehen. Beachten Sie, dass ich einige ästhetische Anpassungen an den GridView-Feldern vorgenommen habe, die nicht erforderlich sind, um die SQL-Cache-Abhängigkeits Funktionalität zu veranschaulichen.

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample7.aspx)]

Erstellen Sie als nächstes einen Ereignishandler für das Ereignis ObjectDataSource s, `Selecting` und fügen Sie den folgenden Code hinzu:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample8.cs)]

Beachten Sie, dass das ObjectDataSource s- `Selecting` Ereignis nur beim Abrufen von Daten aus dem zugrunde liegenden-Objekt ausgelöst wird. Wenn die ObjectDataSource auf die Daten aus dem eigenen Cache zugreift, wird dieses Ereignis nicht ausgelöst.

Besuchen Sie diese Seite nun über einen Browser. Da wir noch keine Zwischenspeicherung implementieren müssen, sollte die Seite jedes Mal, wenn Sie das Raster bearbeiten, Sortieren oder bearbeiten, den Text "ausgelöste Ereignis Auslösung" anzeigen, wie in Abbildung 8 gezeigt.

[![Das Ereignis zum Auswählen von ObjectDataSource s wird jedes Mal ausgelöst, wenn die GridView per Pager, bearbeitet oder sortiert wird.](using-sql-cache-dependencies-cs/_static/image8.gif)](using-sql-cache-dependencies-cs/_static/image9.png)

**Abbildung 8**: das Ereignis "ObjectDataSource s" `Selecting` wird jedes Mal ausgelöst, wenn die GridView per Pager, bearbeitet oder sortiert wird ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image10.png)).

Wie im Tutorial zwischen [Speichern von Daten mit dem ObjectDataSource](caching-data-with-the-objectdatasource-cs.md) -Tutorial gezeigt, bewirkt das Festlegen der- `EnableCaching` Eigenschaft auf, `true` dass ObjectDataSource seine Daten für die Dauer zwischenspeichert, die von der-Eigenschaft angegeben wird `CacheDuration` . ObjectDataSource verfügt auch über eine- [ `SqlCacheDependency` Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx), die den zwischengespeicherten Daten mithilfe des folgenden Musters eine oder mehrere SQL-Cache Abhängigkeiten hinzufügt:

[!code-css[Main](using-sql-cache-dependencies-cs/samples/sample9.css)]

Dabei ist *DatabaseName* der Name der Datenbank, der im `name` -Attribut des `<add>` -Elements in angegeben ist `Web.config` , und *TableName* ist der Name der Datenbanktabelle. Um z. b. eine ObjectDataSource zu erstellen, die Daten unbegrenzt auf der Grundlage einer SQL-Cache Abhängigkeit von der Northwind s- `Products` Tabelle speichert, legen Sie die ObjectDataSource s `EnableCaching` -Eigenschaft auf `true` und deren- `SqlCacheDependency` Eigenschaft auf northwinddb: Products fest.

> [!NOTE]
> Sie können eine SQL-Cache Abhängigkeit *und* einen zeitbasierten Ablauf verwenden, indem Sie `EnableCaching` auf `true` , `CacheDuration` das Zeitintervall und `SqlCacheDependency` auf die Datenbank und den Tabellennamen festlegen. Die ObjectDataSource entfernt die Daten, wenn der zeitbasierte Ablauf erreicht wird, oder wenn das Abrufsystem feststellt, dass sich die zugrunde liegenden Datenbankdaten geändert haben, je nachdem, welcher Vorgang zuerst ausgeführt wird.

Die GridView in `SqlCacheDependencies.aspx` zeigt Daten aus zwei Tabellen an, `Products` und `Categories` (das Feld "Product s" `CategoryName` wird über ein-Feld abgerufen `JOIN` `Categories` ). Daher möchten wir zwei SQL-Cache Abhängigkeiten angeben: northwinddb: Products; Northwinddb: Kategorien.

[![Konfigurieren von ObjectDataSource zur Unterstützung der Zwischenspeicherung mithilfe von SQL-Cache Abhängigkeiten von Produkten und Kategorien](using-sql-cache-dependencies-cs/_static/image9.gif)](using-sql-cache-dependencies-cs/_static/image11.png)

**Abbildung 9**: Konfigurieren von ObjectDataSource zur Unterstützung der Zwischenspeicherung mithilfe von SQL-Cache Abhängigkeiten unter `Products` und `Categories` ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image12.png))

Nach dem Konfigurieren von ObjectDataSource zur Unterstützung der Zwischenspeicherung überprüfen Sie die Seite über einen Browser. Der Text "ausgelöste Ereignis Auslösung" sollte auf dem ersten Besuch der Seite angezeigt werden, sollte jedoch beim Paging, beim Sortieren oder beim Klicken auf die Schaltflächen "Bearbeiten" oder "Abbrechen" entfernt werden. Dies liegt daran, dass nach dem Laden der Daten in den ObjectDataSource s-Cache dort verbleibt, bis die- `Products` Tabelle oder die- `Categories` Tabelle geändert wird oder die Daten über die GridView aktualisiert werden.

Öffnen Sie nach dem Paging durch das Raster, und stellen Sie fest, dass der Text "ausgelöster Ereignis ausgelöste Text" angezeigt wird. Öffnen Sie ein neues Browserfenster, und navigieren Sie zum Abschnitt "Grundlagen" im Abschnitt bearbeiten, einfügen und Löschen `~/EditInsertDelete/Basics.aspx` Aktualisieren Sie den Namen oder den Preis eines Produkts. Zeigen Sie dann in das erste Browserfenster eine andere Datenseite an, Sortieren Sie das Raster, oder klicken Sie auf die Schaltfläche zum Bearbeiten von Zeilen. Dieses Mal sollte das ausgelöste Ereignis "auswählen" erneut angezeigt werden, da die zugrunde liegenden Datenbankdaten geändert wurden (siehe Abbildung 10). Wenn der Text nicht angezeigt wird, warten Sie einen Moment, und versuchen Sie es noch mal. Beachten Sie, dass der Abruf Dienst alle Millisekunden auf Änderungen an der `Products` Tabelle prüft `pollTime` . es gibt also eine Verzögerung zwischen dem Zeitpunkt, zu dem die zugrunde liegenden Daten aktualisiert werden, und dem Zeitpunkt, zu dem die zwischengespeicherten Daten entfernt werden.

[![Durch das Ändern der Products-Tabelle werden die zwischengespeicherten Produktdaten entfernt.](using-sql-cache-dependencies-cs/_static/image10.gif)](using-sql-cache-dependencies-cs/_static/image13.png)

**Abbildung 10**: Ändern der Products-Tabelle entfernt die zwischengespeicherten Produktdaten ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>Schritt 6: Programm gesteuertes arbeiten mit der- `SqlCacheDependency` Klasse

Im Tutorial zum zwischen [Speichern von Daten in der Architektur](caching-data-in-the-architecture-cs.md) wurden die Vorteile der Verwendung einer separaten Cache Schicht in der Architektur behandelt, anstatt das Zwischenspeichern eng mit der ObjectDataSource zu koppeln. In diesem Tutorial haben wir eine `ProductsCL` Klasse erstellt, um die programmgesteuerte Arbeit mit dem Daten Cache zu veranschaulichen. Verwenden Sie die-Klasse, um SQL-Cache Abhängigkeiten in der zwischen Speicherungs Ebene zu verwenden `SqlCacheDependency` .

Beim Abrufsystem `SqlCacheDependency` muss ein-Objekt mit einer bestimmten Datenbank und einem Tabellen Paar verknüpft werden. Der folgende Code erstellt z. b. ein- `SqlCacheDependency` Objekt, das auf der Tabelle Northwind database s basiert `Products` :

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample10.cs)]

Die beiden Eingabeparameter für den `SqlCacheDependency` s-Konstruktor sind die Datenbank-bzw. Tabellennamen. Wie bei der ObjectDataSource s- `SqlCacheDependency` Eigenschaft entspricht der verwendete Datenbankname dem Wert, der im- `name` Attribut des- `<add>` Elements in angegeben ist `Web.config` . Der Tabellenname ist der tatsächliche Name der Datenbanktabelle.

Um ein einem `SqlCacheDependency` Element zuzuordnen, das dem Daten Cache hinzugefügt wurde, verwenden Sie eine der- `Insert` Methoden Überladungen, die eine Abhängigkeit akzeptiert. Der folgende Code fügt dem Daten Cache für eine unbestimmte Dauer einen *Wert* hinzu, ordnet ihn jedoch einem `SqlCacheDependency` in der `Products` Tabelle zu. Kurz gesagt verbleiben *Werte* im Cache, bis Sie aufgrund von Arbeitsspeicher Einschränkungen entfernt werden oder das Abrufsystem festgestellt hat, dass die `Products` Tabelle seit der Zwischenspeicherung geändert wurde.

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample11.cs)]

Die s-Klasse der cachingschicht `ProductsCL` speichert aktuell Daten aus der `Products` Tabelle mithilfe eines zeitbasierten Ablaufs von 60 Sekunden. Aktualisieren Sie diese Klasse, sodass stattdessen SQL-Cache Abhängigkeiten verwendet werden. Die `ProductsCL` Klasse s- `AddCacheItem` Methode, die für das Hinzufügen der Daten zum Cache zuständig ist, enthält derzeit den folgenden Code:

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample12.cs)]

Aktualisieren Sie diesen Code, sodass `SqlCacheDependency` anstelle der Cache Abhängigkeit ein-Objekt verwendet wird `MasterCacheKeyArray` :

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample13.cs)]

Um diese Funktionalität zu testen, fügen Sie der Seite unterhalb der vorhandenen GridView eine GridView hinzu `ProductsDeclarative` . Legen Sie diese neue GridView s auf fest, `ID` `ProductsProgrammatic` und binden Sie Sie über das Smarttag an eine neue ObjectDataSource mit dem Namen `ProductsDataSourceProgrammatic` . Konfigurieren Sie ObjectDataSource, um die `ProductsCL` -Klasse zu verwenden, und legen Sie die Dropdown Listen auf den Registerkarten auswählen und Aktualisieren auf `GetProducts` `UpdateProduct` bzw. fest.

[![Konfigurieren von ObjectDataSource für die Verwendung der productscl-Klasse](using-sql-cache-dependencies-cs/_static/image11.gif)](using-sql-cache-dependencies-cs/_static/image15.png)

**Abbildung 11**: Konfigurieren von ObjectDataSource für die Verwendung der- `ProductsCL` Klasse ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image16.png))

[![Wählen Sie in der Dropdown Liste Registerkarte auswählen die Methode GetProducts aus.](using-sql-cache-dependencies-cs/_static/image12.gif)](using-sql-cache-dependencies-cs/_static/image17.png)

**Abbildung 12**: Auswählen der `GetProducts` Methode aus der Dropdown Liste "Registerkarte auswählen" ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image18.png))

[![Wählen Sie die UpdateProduct-Methode aus der Dropdown Liste der Registerkarte "Aktualisieren" aus.](using-sql-cache-dependencies-cs/_static/image13.gif)](using-sql-cache-dependencies-cs/_static/image19.png)

**Abbildung 13**: Auswählen der UpdateProduct-Methode aus der Dropdown Liste der Registerkarte "Aktualisieren" ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-sql-cache-dependencies-cs/_static/image20.png))

Nach dem Abschließen des Assistenten zum Konfigurieren von Datenquellen erstellt Visual Studio boundfields und checkboxfields in der GridView für jedes der Datenfelder. Entfernen Sie wie bei der ersten GridView, die dieser Seite hinzugefügt wurde, alle Felder,, `ProductName` `CategoryName` und `UnitPrice` , und formatieren Sie diese Felder wie gewünscht. Aktivieren Sie aus dem GridView s-Smarttag die Kontrollkästchen Paging aktivieren, Sortierung aktivieren und Bearbeiten aktivieren. Wie bei `ProductsDataSourceDeclarative` ObjectDataSource legt Visual Studio die `ProductsDataSourceProgrammatic` ObjectDataSource s- `OldValuesParameterFormatString` Eigenschaft auf fest `original_{0}` . Damit die Funktion zum Bearbeiten von GridView-Funktionen ordnungsgemäß funktioniert, legen Sie diese Eigenschaft auf zurück `{0}` (oder entfernen Sie die Eigenschafts Zuweisung aus der deklarativen Syntax).

Nachdem Sie diese Aufgaben abgeschlossen haben, sollten das resultierende GridView-und ObjectDataSource-Markup wie folgt aussehen:

[!code-aspx[Main](using-sql-cache-dependencies-cs/samples/sample14.aspx)]

Um die SQL-Cache Abhängigkeit in der zwischen Speicherungs Ebene zu testen, legen Sie einen Haltepunkt in der `ProductCL` -Methode der Klasse fest, `AddCacheItem` und starten Sie das Debugging Beim ersten Besuch `SqlCacheDependencies.aspx` sollte der Haltepunkt getroffen werden, da die Daten zum ersten Mal angefordert und im Cache abgelegt werden. Wechseln Sie als nächstes zu einer anderen Seite in der GridView, oder sortieren Sie eine der Spalten. Dies bewirkt, dass die GridView Ihre Daten anweist, aber die Daten sollten im Cache gefunden werden, da die Daten `Products` Bank Tabelle nicht geändert wurde. Wenn die Daten wiederholt nicht im Cache gefunden werden, stellen Sie sicher, dass genügend Arbeitsspeicher auf dem Computer verfügbar ist, und wiederholen Sie den Vorgang.

Öffnen Sie nach dem Paging durch einige wenige Seiten der GridView ein zweites Browserfenster, und navigieren Sie im Abschnitt bearbeiten, einfügen und löschen () zum Tutorial Grundlagen `~/EditInsertDelete/Basics.aspx` . Aktualisieren Sie einen Datensatz in der Tabelle Products, und zeigen Sie dann im ersten Browserfenster eine neue Seite an, oder klicken Sie auf einen der Sortier Header.

In diesem Szenario wird eine der beiden folgenden Punkte angezeigt: entweder wird der Breakpoint gedrückt, und es wird angegeben, dass die zwischengespeicherten Daten aufgrund der Änderung in der Datenbank entfernt wurden. oder der Haltepunkt wird nicht gedrückt, d `SqlCacheDependencies.aspx` . h., es werden nun veraltete Daten angezeigt. Wenn der Haltepunkt nicht gedrückt wird, liegt dies wahrscheinlich daran, dass der Abruf Dienst noch nicht ausgelöst wurde, da die Daten geändert wurden. Beachten Sie, dass der Abruf Dienst alle Millisekunden auf Änderungen an der `Products` Tabelle prüft `pollTime` . es gibt also eine Verzögerung zwischen dem Zeitpunkt, zu dem die zugrunde liegenden Daten aktualisiert werden, und dem Zeitpunkt, zu dem die zwischengespeicherten Daten entfernt werden.

> [!NOTE]
> Diese Verzögerung wird eher angezeigt, wenn eines der Produkte über die GridView in bearbeitet wird `SqlCacheDependencies.aspx` . Im Tutorial zum zwischen [Speichern von Daten in der Architektur](caching-data-in-the-architecture-cs.md) haben wir die `MasterCacheKeyArray` Cache Abhängigkeit hinzugefügt, um sicherzustellen, dass die durch die Methode der Klasse bearbeiteten Daten `ProductsCL` `UpdateProduct` aus dem Cache entfernt wurden. Diese Cache Abhängigkeit wurde jedoch ersetzt, wenn die `AddCacheItem` -Methode weiter oben in diesem Schritt geändert wurde `ProductsCL` . Daher werden die zwischengespeicherten Daten von der-Klasse weiterhin angezeigt, bis das Abrufsystem die Änderung an der `Products` Tabelle notiert. Wir sehen uns an, wie Sie die `MasterCacheKeyArray` Cache Abhängigkeit in Schritt 7 erneut einführen können.

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>Schritt 7: Zuordnen mehrerer Abhängigkeiten zu einem zwischengespeicherten Element

Beachten Sie, dass die `MasterCacheKeyArray` Cache Abhängigkeit verwendet wird, um sicherzustellen, dass *alle* produktbezogenen Daten aus dem Cache entfernt werden, wenn ein einzelnes Element, das in ihr verknüpft ist, aktualisiert wird. Die- `GetProductsByCategoryID(categoryID)` Methode speichert z `ProductsDataTables` . b. Instanzen für jeden eindeutigen *CategoryID* -Wert zwischen. Wenn eines dieser Objekte entfernt wird, `MasterCacheKeyArray` stellt die Cache Abhängigkeit sicher, dass die anderen ebenfalls entfernt werden. Ohne diese Cache Abhängigkeit ist es möglich, dass andere zwischengespeicherte Produktdaten veraltet sind, wenn die zwischengespeicherten Daten geändert werden. Folglich ist es wichtig, dass die `MasterCacheKeyArray` Cache Abhängigkeit bei der Verwendung von SQL-Cache Abhängigkeiten gewahrt bleibt. Die Data Cache s- `Insert` Methode ermöglicht jedoch nur ein einzelnes Abhängigkeits Objekt.

Außerdem müssen bei der Arbeit mit SQL-Cache Abhängigkeiten möglicherweise mehrere Datenbanktabellen als Abhängigkeiten verknüpft werden. Beispielsweise enthält das `ProductsDataTable` zwischengespeicherte in der `ProductsCL` -Klasse die Kategorien-und Lieferanten Namen für jedes Produkt, aber die- `AddCacheItem` Methode verwendet nur eine Abhängigkeit von `Products` . Wenn der Benutzer den Namen einer Kategorie oder eines Lieferanten aktualisiert, verbleiben die zwischengespeicherten Produktdaten in dieser Situation im Cache und sind veraltet. Daher möchten wir, dass die zwischengespeicherten Produktdaten nicht nur von der `Products` Tabelle, sondern auch von den `Categories` Tabellen und abhängig sind `Suppliers` .

Die- [ `AggregateCacheDependency` Klasse](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx) bietet eine Möglichkeit zum Zuordnen mehrerer Abhängigkeiten zu einem Cache Element. Beginnen Sie mit dem Erstellen einer `AggregateCacheDependency` Instanz von. Fügen Sie als nächstes den Satz von Abhängigkeiten mithilfe der `AggregateCacheDependency` s- `Add` Methode hinzu. Wenn Sie das Element anschließend in den Daten Cache einfügen, übergeben Sie die- `AggregateCacheDependency` Instanz. Wenn sich *eine* der `AggregateCacheDependency` Abhängigkeiten der Instanz ändert, wird das zwischengespeicherte Element entfernt.

Der folgende Code zeigt den aktualisierten Code für die-Methode der- `ProductsCL` Klasse `AddCacheItem` . Die-Methode erstellt die `MasterCacheKeyArray` Cache Abhängigkeit zusammen mit- `SqlCacheDependency` Objekten für die `Products` `Categories` -,-und- `Suppliers` Tabellen. Diese werden alle in einem- `AggregateCacheDependency` Objekt `aggregateDependencies` mit dem Namen kombiniert, das dann an die-Methode weitergegeben wird `Insert` .

[!code-csharp[Main](using-sql-cache-dependencies-cs/samples/sample15.cs)]

Testen Sie diesen neuen Code. Änderungen an den `Products` Tabellen, `Categories` oder bewirken nun, `Suppliers` dass die zwischengespeicherten Daten entfernt werden. Außerdem wird die `ProductsCL` `UpdateProduct` Cache Abhängigkeit durch die Methode der Klasse s, die aufgerufen wird, wenn ein Produkt über die GridView bearbeitet wird, entfernt `MasterCacheKeyArray` . Dadurch wird das zwischengespeicherte entfernt, `ProductsDataTable` und die Daten werden bei der nächsten Anforderung erneut abgerufen.

> [!NOTE]
> SQL-Cache Abhängigkeiten können auch mit der [Ausgabe](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)Zwischenspeicherung verwendet werden. Eine Demonstration dieser Funktionalität finden Sie unter Verwenden von [ASP.net Output Caching with SQL Server](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx).

## <a name="summary"></a>Zusammenfassung

Beim Zwischenspeichern von Datenbankdaten verbleiben die Daten idealerweise im Cache, bis Sie in der Datenbank geändert werden. Mit ASP.NET 2,0 können SQL-Cache Abhängigkeiten in deklarativen und programmgesteuerten Szenarien erstellt und verwendet werden. Eine der Herausforderungen bei diesem Ansatz besteht darin, herauszufinden, wann die Daten geändert wurden. Die vollständigen Versionen von Microsoft SQL Server 2005 bieten Benachrichtigungsfunktionen, die eine Anwendung Benachrichtigen können, wenn sich ein Abfrageergebnis geändert hat. Für die Express Edition von SQL Server 2005 und älteren Versionen von SQL Server muss stattdessen ein Abrufsystem verwendet werden. Glücklicherweise ist das Einrichten der erforderlichen Abruf Infrastruktur recht unkompliziert.

Fröhliche Programmierung!

## <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu den in diesem Tutorial behandelten Themen finden Sie in den folgenden Ressourcen:

- [Verwenden von Abfrage Benachrichtigungen in Microsoft SQL Server 2005](https://msdn.microsoft.com/library/ms175110.aspx)
- [Erstellen einer Abfrage Benachrichtigung](https://msdn.microsoft.com/library/ms188669.aspx)
- [Caching in ASP.net mit der- `SqlCacheDependency` Klasse](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server Registrierungs Tool ( `aspnet_regsql.exe` )](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [Übersicht über `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>Zum Autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), Autor der sieben ASP/ASP. net-Bücher und Gründer von [4GuysFromRolla.com](http://www.4guysfromrolla.com), hat seit 1998 mit Microsoft-Webtechnologien gearbeitet. Scott arbeitet als unabhängiger Berater, Ausbilder und Writer. Sein letztes Buch ist [*Sams Teach Yourself ASP.NET 2,0 in 24 Stunden*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Er kann mit erreicht werden [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com) oder über seinen Blog finden Sie unter [http://ScottOnWriting.NET](http://ScottOnWriting.NET) .

## <a name="special-thanks-to"></a>Besonders vielen Dank

Diese tutorialreihe wurde von vielen hilfreichen Reviewern geprüft. Die führenden Reviewer für dieses Tutorial waren Marko Rangel, Teresa Murphy und Hilton giesreviewer. Möchten Sie meine bevorstehenden MSDN-Artikel überprüfen? Wenn dies der Fall ist, löschen Sie die Zeile in [ mitchell@4GuysFromRolla.com .](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Zurück](caching-data-at-application-startup-cs.md)
> [Weiter](caching-data-with-the-objectdatasource-vb.md)
