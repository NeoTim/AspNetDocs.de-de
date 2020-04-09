---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Tutorial: Server-Broadcast mit SignalR 2 | Microsoft Docs'
author: tdykstra
description: In diesem Tutorial wird gezeigt, wie Sie eine Webanwendung erstellen, die ASP.NET SignalR 2 verwendet, um Serverübertragungsfunktionen bereitzustellen.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675724"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Tutorial: Server-Broadcast mit SignalR 2

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

In diesem Tutorial wird gezeigt, wie Sie eine Webanwendung erstellen, die ASP.NET SignalR 2 verwendet, um Serverübertragungsfunktionen bereitzustellen. Serverübertragung bedeutet, dass der Server die an Clients gesendete Kommunikation startet.

Die Anwendung, die Sie in diesem Tutorial erstellen, simuliert einen Börsenticker, ein typisches Szenario für die Serverübertragungsfunktionalität. In regelmäßigen Abständen aktualisiert der Server nach dem Zufallsprinzip die Aktienkurse und sendet die Aktualisierungen an alle verbundenen Clients. Im Browser ändern sich die **Change** Zahlen **%** und Symbole in den Spalten Ändern und Spalten dynamisch als Reaktion auf Benachrichtigungen vom Server. Wenn Sie zusätzliche Browser mit derselben URL öffnen, werden alle dieselben Daten und dieselben Änderungen gleichzeitig angezeigt.

![Web erstellen](tutorial-server-broadcast-with-signalr/_static/image1.png)

In diesem Tutorial führen Sie Folgendes durch:

> [!div class="checklist"]
> * Erstellen des Projekts
> * Einrichten des Servercodes
> * Überprüfen des Servercodes
> * Einrichten des Clientcodes
> * Untersuchen des Clientcodes
> * Testen der Anwendung
> * Aktivieren der Protokollierung

> [!IMPORTANT]
> Wenn Sie die Schritte zum Erstellen der Anwendung nicht durcharbeiten möchten, können Sie das SignalR.Sample-Paket in einem neuen Projekt "Empty ASP.NET Web Application" installieren. Wenn Sie das NuGet-Paket installieren, ohne die Schritte in diesem Tutorial auszuführen, müssen Sie die Anweisungen in der Datei *readme.txt* befolgen. Zum Ausführen des Pakets müssen Sie eine OWIN-Startklasse hinzufügen, die die `ConfigureSignalR` Methode im installierten Paket aufruft. Sie erhalten eine Fehlermeldung, wenn Sie die OWIN-Startklasse nicht hinzufügen. Weitere Informationen finden Sie im [Beispielabschnitt "Installieren des StockTicker"](#install-the-stockticker-sample) in diesem Artikel.

## <a name="prerequisites"></a>Voraussetzungen

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) mit der Workload **ASP.NET und Webentwicklung**

## <a name="create-the-project"></a>Erstellen des Projekts

In diesem Abschnitt wird gezeigt, wie Sie Visual Studio 2017 verwenden, um eine leere ASP.NET Webanwendung zu erstellen.

1. Erstellen Sie in Visual Studio eine ASP.NET Webanwendung.

    ![Web erstellen](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. Lassen Sie im Fenster **Neue ASP.NET Webapplication - SignalR.StockTicker** **Leer** aus und wählen Sie **OK**aus.

## <a name="set-up-the-server-code"></a>Einrichten des Servercodes

In diesem Abschnitt richten Sie den Code ein, der auf dem Server ausgeführt wird.

### <a name="create-the-stock-class"></a>Erstellen der Stock-Klasse

Sie beginnen mit *Stock* dem Erstellen der Stock-Modellklasse, die Sie zum Speichern und Übertragen von Informationen über einen Bestand verwenden.

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Klasse** **hinzufügen** > aus.

1. Benennen Sie die Klasse *Stock,* und fügen Sie sie dem Projekt hinzu.

1. Ersetzen Sie den Code in der *Stock.cs* Datei durch diesen Code:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Die beiden Eigenschaften, die Sie beim `Symbol` Erstellen von Beständen festlegen, `Price`sind (z. B. MSFT für Microsoft) und . Die anderen Eigenschaften hängen davon `Price`ab, wie und wann Sie . Wenn Sie das `Price`erste Mal festlegen, wird `DayOpen`der Wert an weitergegeben. Danach berechnet die `Price`App beim Festlegen `Change` die `PercentChange` Und-Eigenschaftswerte `Price` basierend `DayOpen`auf der Differenz zwischen und .

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>Erstellen der StockTickerHub- und StockTicker-Klassen

Sie verwenden die SignalR Hub-API, um die Server-zu-Client-Interaktion zu verarbeiten. Eine `StockTickerHub` Klasse, die von der `Hub` SignalR-Klasse ableitet, verarbeitet empfangende Verbindungen und Methodenaufrufe von Clients. Sie müssen auch Bestandsdaten `Timer` verwalten und ein Objekt ausführen. Das `Timer` Objekt löst in regelmäßigen Abständen Preisaktualisierungen unabhängig von Clientverbindungen aus. Sie können diese Funktionen nicht `Hub` in einer Klasse einsetzen, da Hubs vorübergehend sind. Die App `Hub` erstellt eine Klasseninstanz für jede Aufgabe auf dem Hub, z. B. Verbindungen und Aufrufe vom Client an den Server. Der Mechanismus, der Bestandsdaten speichert, Preise aktualisiert und die Preisaktualisierungen sendet, muss also in einer separaten Klasse ausgeführt werden. Sie nennen die `StockTicker`Klasse .

![Ausstrahlung von StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

Sie möchten nur, `StockTicker` dass eine Instanz der Klasse auf dem Server ausgeführt wird, daher müssen Sie einen Verweis von jeder `StockTickerHub` Instanz auf die Singleton-Instanz `StockTicker` einrichten. Die `StockTicker` Klasse muss an Clients übertragen werden, da sie `StockTicker` über die Bestandsdaten verfügt und Aktualisierungen auslöst, aber keine `Hub` Klasse ist. Die `StockTicker` Klasse muss einen Verweis auf das SignalR Hub-Verbindungskontextobjekt abrufen. Anschließend kann das SignalR-Verbindungskontextobjekt verwendet werden, um es an Clients zu übertragen.

#### <a name="create-stocktickerhubcs"></a>Erstellen StockTickerHub.cs

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Neues Element** **hinzufügen** > aus.

1. **Wählen** > Sie unter Neues Element hinzufügen **- SignalR.StockTicker**aus, installed**Visual C-Web** > **Web** > **SignalR** und dann **SignalR Hub Class (v2)** aus.

1. Benennen Sie die Klasse *StockTickerHub,* und fügen Sie sie dem Projekt hinzu.

    In diesem Schritt wird die *StockTickerHub.cs* Klassendatei erstellt. Gleichzeitig wird eine Reihe von Skriptdateien und Assemblyverweisen hinzugefügt, die SignalR zum Projekt unterstützen.

1. Ersetzen Sie den Code in der *StockTickerHub.cs* Datei durch diesen Code:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Speichern Sie die Datei .

Die App [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) verwendet die Hub-Klasse, um Methoden zu definieren, die die Clients auf dem Server aufrufen können. Sie definieren eine Methode: `GetAllStocks()`. Wenn ein Client zunächst eine Verbindung mit dem Server herstellt, ruft er diese Methode auf, um eine Liste aller Bestände mit ihren aktuellen Preisen abzurufen. Die Methode kann synchron `IEnumerable<Stock>` ausgeführt und zurückgegeben werden, da sie Daten aus dem Arbeitsspeicher zurückgibt.

Wenn die Methode die Daten abrufen muss, indem sie etwas tut, das warten würde, `Task<IEnumerable<Stock>>` z. B. eine Datenbanksuche oder einen Webdienstaufruf, geben Sie als Rückgabewert an, um die asynchrone Verarbeitung zu aktivieren. Weitere Informationen finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronly](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

Das `HubName` Attribut gibt an, wie die App auf den Hub im JavaScript-Code auf dem Client verweist. Der Standardname auf dem Client, wenn Sie dieses Attribut nicht verwenden, ist eine camelCase-Version des Klassennamens, die in diesem Fall `stockTickerHub`.

Wie Sie später beim Erstellen `StockTicker` der Klasse sehen werden, erstellt die App eine `Instance` Singleton-Instanz dieser Klasse in ihrer statischen Eigenschaft. Diese Singleton-Instanz von `StockTicker` befindet sich im Arbeitsspeicher, unabhängig davon, wie viele Clients eine Verbindung herstellen oder trennen. Diese Instanz verwendet `GetAllStocks()` die Methode, um aktuelle Bestandsinformationen zurückzugeben.

#### <a name="create-stocktickercs"></a>Erstellen StockTicker.cs

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Klasse** **hinzufügen** > aus.

1. Benennen Sie die Klasse *StockTicker,* und fügen Sie sie dem Projekt hinzu.

1. Ersetzen Sie den Code in der *StockTicker.cs* Datei durch diesen Code:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Da alle Threads dieselbe Instanz des StockTicker-Codes ausführen, muss die StockTicker-Klasse threadsicher sein.

### <a name="examine-the-server-code"></a>Überprüfen des Servercodes

Wenn Sie den Servercode untersuchen, können Sie verstehen, wie die App funktioniert.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Speichern der Singleton-Instanz in einem statischen Feld

Der Code initialisiert `_instance` das statische Feld, das die `Instance` Eigenschaft mit einer Instanz der Klasse unterstützt. Da der Konstruktor privat ist, ist er die einzige Instanz der Klasse, die die App erstellen kann. Die App verwendet Lazy `_instance` [Initialisierung](/dotnet/framework/performance/lazy-initialization) für das Feld. Es ist nicht aus Leistungsgründen. Es soll sicherstellen, dass die Instanzerstellung threadsicher ist.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

Jedes Mal, wenn ein Client eine Verbindung mit dem Server herstellt, ruft eine neue Instanz der `StockTicker.Instance` StockTickerHub-Klasse, die `StockTickerHub` in einem separaten Thread ausgeführt wird, die StockTicker Singleton-Instanz von der statischen Eigenschaft ab, wie Sie zuvor in der Klasse gesehen haben.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Speichern von Bestandsdaten in einem ConcurrentDictionary

Der Konstruktor initialisiert `_stocks` die Auflistung mit einigen `GetAllStocks` Stichprobenbestandsdaten und gibt die Bestände zurück. Wie Sie bereits gesehen haben, wird `StockTickerHub.GetAllStocks`diese Sammlung von Beständen von zurückgegeben, einer Servermethode in der `Hub` Klasse, die Clients aufrufen können.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Die Bestandsauflistung ist als [ConcurrentDictionary-Typ](https://msdn.microsoft.com/library/dd287191.aspx) für die Threadsicherheit definiert. Alternativ können Sie ein [Dictionary-Objekt](https://msdn.microsoft.com/library/xfhwa508.aspx) verwenden und das Wörterbuch explizit sperren, wenn Sie Änderungen daran vornehmen.

Für diese Beispielanwendung ist es in Ordnung, Anwendungsdaten im Arbeitsspeicher zu speichern `StockTicker` und die Daten zu verlieren, wenn die App die Instance entsorgt. In einer echten Anwendung würden Sie mit einem Back-End-Datenspeicher wie einer Datenbank arbeiten.

#### <a name="periodically-updating-stock-prices"></a>Regelmäßige Aktualisierung der Aktienkurse

Der Konstruktor startet `Timer` ein Objekt, das regelmäßig Methoden aufruft, die Aktienkurse nach dem Zufallsprinzip aktualisieren.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`fordert `UpdateStockPrices`, die im Zustandsparameter null übergibt. Vor dem Aktualisieren der Preise nimmt `_updateStockPricesLock` die App eine Sperre für das Objekt. Der Code überprüft, ob ein anderer Thread `TryUpdateStockPrice` bereits Preise aktualisiert, und ruft dann jeden Bestand in der Liste auf. Die `TryUpdateStockPrice` Methode entscheidet, ob der Aktienkurs geändert werden soll und wie viel er ihn ändern soll. Wenn sich der Aktienkurs ändert, ruft `BroadcastStockPrice` die App an, um die Aktienkursänderung an alle verbundenen Kunden zu übertragen.

Das `_updatingStockPrices` Flag, das [als flüchtig](https://msdn.microsoft.com/library/x13ttww7.aspx) gekennzeichnet ist, um sicherzustellen, dass es threadsicher ist.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

In einer echten `TryUpdateStockPrice` Anwendung würde die Methode einen Webdienst aufrufen, um den Preis nachzuschlagen. In diesem Code verwendet die App einen Zufallszahlengenerator, um Änderungen nach dem Zufallsprinzip vorzunehmen.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Abrufen des SignalR-Kontexts, damit die StockTicker-Klasse an Clients übertragen werden kann

Da die Preisänderungen hier `StockTicker` im Objekt entstehen, ist es `updateStockPrice` das Objekt, das eine Methode für alle verbundenen Clients aufrufen muss. In `Hub` einer Klasse verfügen Sie über eine `StockTicker` API zum Aufrufen von `Hub` Clientmethoden, leiten jedoch nicht `Hub` von der Klasse ab und haben keinen Verweis auf ein Objekt. Um an verbundene Clients `StockTicker` zu übertragen, muss die Klasse `StockTickerHub` die SignalR-Kontextinstanz für die Klasse abrufen und diese verwenden, um Methoden für Clients aufzurufen.

Der Code ruft einen Verweis auf den SignalR-Kontext ab, wenn er die Singleton-Klasseninstanz erstellt, diesen Verweis an den Konstruktor übergibt und der Konstruktor ihn in die `Clients` Eigenschaft setzt.

Es gibt zwei Gründe, warum Sie den Kontext nur einmal abrufen möchten: Das Abrufen des Kontexts ist eine kostspielige Aufgabe, und wenn Sie ihn einmal abrufen, wird sichergestellt, dass die App die beabsichtigte Reihenfolge der an die Clients gesendeten Nachrichten beibehält.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Wenn `Clients` Sie die Eigenschaft des Kontexts abrufen und in der `StockTickerClient` Eigenschaft ablenken, können `Hub` Sie Code schreiben, um Clientmethoden aufzurufen, die wie in einer Klasse aussehen. Um z. B. an alle `Clients.All.updateStockPrice(stock)`Clients zu senden, können Sie schreiben.

Die `updateStockPrice` Methode, die `BroadcastStockPrice` Sie aufrufen, ist noch nicht vorhanden. Sie fügen sie später hinzu, wenn Sie Code schreiben, der auf dem Client ausgeführt wird. Sie können `updateStockPrice` hier `Clients.All` darauf verweisen, da dies dynamisch ist, was bedeutet, dass die App den Ausdruck zur Laufzeit auswertet. Wenn dieser Methodenaufruf ausgeführt wird, sendet SignalR den Methodennamen und den Parameterwert an `updateStockPrice`den Client, und wenn der Client eine Methode mit dem Namen hat, ruft die App diese Methode auf und übergibt den Parameterwert an ihn.

`Clients.All`bedeutet, an alle Clients zu senden. Mit SignalR können Sie weitere Optionen angeben, an welche Clients oder Gruppen von Clients gesendet werden sollen. Weitere Informationen finden Sie unter [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Registrieren der SignalR-Route

Der Server muss wissen, welche URL abgefangen und direkt an SignalR gesendet werden soll. Fügen Sie dazu eine OWIN-Startklasse hinzu:

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Neues Element** **hinzufügen** > aus.

1. Wählen Sie unter **Neues Element hinzufügen - SignalR.StockTicker** **Installed** > **Visual C'Web** > **Web** und dann **OWIN Startup Class**aus.

1. Benennen Sie die Klasse *Start,* und wählen Sie **OK**.

1. Ersetzen Sie den Standardcode in der *Startup.cs* Datei durch diesen Code:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Sie haben die Einrichtung des Servercodes abgeschlossen. Im nächsten Abschnitt richten Sie den Client ein.

## <a name="set-up-the-client-code"></a>Einrichten des Clientcodes

In diesem Abschnitt richten Sie den Code ein, der auf dem Client ausgeführt wird.

### <a name="create-the-html-page-and-javascript-file"></a>Erstellen der HTML-Seite und der JavaScript-Datei

Die HTML-Seite zeigt die Daten an und die JavaScript-Datei organisiert die Daten.

#### <a name="create-stocktickerhtml"></a>Erstellen von StockTicker.html

Zuerst fügen Sie den HTML-Client hinzu.

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**HTML-Seite** **hinzufügen** > aus.

1. Benennen Sie die Datei *StockTicker* und wählen Sie **OK**.

1. Ersetzen Sie den Standardcode in der *Datei StockTicker.html* durch diesen Code:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    Der HTML-Code erstellt eine Tabelle mit fünf Spalten, einer Kopfzeile und einer Datenzeile mit einer einzelnen Zelle, die alle fünf Spalten umfasst. Die Datenzeile zeigt "Laden..." momentan, wenn die App gestartet wird. JavaScript-Code entfernt diese Zeile und fügt an ihrer Stelle Zeilen mit Vom Server abgerufenen Bestandsdaten hinzu.

    Die Skript-Tags geben Folgendes an:

    * Die jQuery-Skriptdatei.

    * Die SignalR-Kernskriptdatei.

    * Die SignalR-Proxy-Skriptdatei.

    * Eine StockTicker-Skriptdatei, die Sie später erstellen werden.

    Die App generiert dynamisch die SignalR-Proxys-Skriptdatei. Sie gibt die URL "/signalr/hubs" an und definiert Proxymethoden für die Methoden `StockTickerHub.GetAllStocks`in der Hub-Klasse, in diesem Fall für . Wenn Sie möchten, können Sie diese JavaScript-Datei manuell generieren, indem Sie [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)verwenden. Vergessen Sie nicht, die dynamische `MapHubs` Dateierstellung im Methodenaufruf zu deaktivieren.

1. Erweitern Sie im **Projektmappen-Explorer** **Skripts**.

    Skriptbibliotheken für jQuery und SignalR sind im Projekt sichtbar.

    > [!IMPORTANT]
    > Der Paket-Manager installiert eine neuere Version der SignalR-Skripte.

1. Aktualisieren Sie die Skriptverweise im Codeblock so, dass sie den Versionen der Skriptdateien im Projekt entsprechen.

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf *StockTicker.html*, und wählen Sie dann **Als Startseite festlegen**aus.

#### <a name="create-stocktickerjs"></a>Erstellen von StockTicker.js

Erstellen Sie nun die JavaScript-Datei.

1. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**JavaScript-Datei** **hinzufügen** > aus.

1. Benennen Sie die Datei *StockTicker* und wählen Sie **OK**.

1. Fügen Sie diesen Code zur Datei *StockTicker.js* hinzu:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>Untersuchen des Clientcodes

Wenn Sie den Clientcode untersuchen, können Sie erfahren, wie der Clientcode mit dem Servercode interagiert, damit die App funktioniert.

#### <a name="starting-the-connection"></a>Starten der Verbindung

`$.connection`bezieht sich auf die SignalR-Proxys. Der Code ruft einen Verweis `StockTickerHub` auf den Proxy `ticker` für die Klasse ab und legt ihn in die Variable ein. Der Proxyname ist der Name, `HubName` der durch das Attribut festgelegt wurde:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Nachdem Sie alle Variablen und Funktionen definiert haben, initialisiert die letzte Codezeile in `start` der Datei die SignalR-Verbindung, indem sie die SignalR-Funktion aufruft. Die `start` Funktion wird asynchron ausgeführt und gibt ein [jQuery Deferred-Objekt](http://api.jquery.com/category/deferred-object/)zurück. Sie können die fertige Funktion aufrufen, um die Funktion anzugeben, die aufrufen soll, wenn die App die asynchrone Aktion beendet.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Alle Bestände erhalten

Die `init` Funktion `getAllStocks` ruft die Funktion auf dem Server auf und verwendet die Informationen, die der Server zurückgibt, um die Bestandstabelle zu aktualisieren. Beachten Sie, dass Sie standardmäßig camelCasing auf dem Client verwenden müssen, obwohl der Methodenname auf dem Server pascal-cased ist. Die CamelCasing-Regel gilt nur für Methoden, nicht für Objekte. Sie beziehen sich `stock.Symbol` z. B. auf und `stock.Price`, nicht `stock.symbol` oder `stock.price`.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

In `init` der Methode erstellt die App HTML für eine Tabellenzeile für `formatStock` jedes vom `stock` Server empfangene Stockobjekt, indem sie die Formateigenschaften des Objekts aufruft und dann aufruft, `supplant` um Platzhalter in der `rowTemplate` Variablen durch die `stock` Objekteigenschaftswerte zu ersetzen. Der resultierende HTML-Code wird dann an die Bestandstabelle angehängt.

> [!NOTE]
> Sie `init` rufen auf, indem `callback` Sie es als Funktion `start` übergeben, die nach Abschluss der asynchronen Funktion ausgeführt wird. Wenn Sie `init` nach dem Aufruf `start`als separate JavaScript-Anweisung aufgerufen haben, schlägt die Funktion fehl, da sie sofort ausgeführt wird, ohne darauf zu warten, dass die Startfunktion den Verbindungsaufbau beendet. In diesem Fall `init` würde die Funktion `getAllStocks` versuchen, die Funktion aufzurufen, bevor die App eine Serververbindung herstellt.

#### <a name="getting-updated-stock-prices"></a>Aktualisierte Aktienkurse

Wenn der Server den Kurs einer Aktie `updateStockPrice` ändert, ruft er die auf verbundenen Clients auf. Die App fügt die Funktion der `stockTicker` Clienteigenschaft des Proxys hinzu, um sie für Aufrufe vom Server verfügbar zu machen.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

Die `updateStockPrice` Funktion formatiert ein vom Server empfangenes Stockobjekt auf `init` die gleiche Weise wie in der Funktion in eine Tabellenzeile. Anstatt die Zeile an die Tabelle anzuhängen, findet sie die aktuelle Zeile der Aktie in der Tabelle und ersetzt diese Zeile durch die neue Zeile.

## <a name="test-the-application"></a>Testen der Anwendung

Sie können die App testen, um sicherzustellen, dass sie funktioniert. Sie sehen, wie alle Browserfenster die Live-Aktientabelle mit schwankenden Aktienkursen anzeigen.

1. Aktivieren Sie in der Symbolleiste das **Skriptdebuggen,** und wählen Sie dann die Wiedergabeschaltfläche aus, um die App im Debugmodus auszuführen.

    ![Screenshot des Benutzers, der den Debugmodus aktiviert und Play auswählt.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    Es wird ein Browserfenster geöffnet, in dem die **Live Stock Table**angezeigt wird. Die Bestandstabelle zeigt zunächst das "Laden..." Nach kurzer Zeit zeigt die App dann die anfänglichen Bestandsdaten an, und dann beginnen sich die Aktienkurse zu ändern.

1. Kopieren Sie die URL aus dem Browser, öffnen Sie zwei weitere Browser, und fügen Sie die URLs in die Adressleisten ein.

    Die anfängliche Bestandsanzeige ist die gleiche wie der erste Browser und Änderungen erfolgen gleichzeitig.

1. Schließen Sie alle Browser, öffnen Sie einen neuen Browser, und wechseln Sie zur gleichen URL.

    Das StockTicker Singleton-Objekt wurde weiterhin auf dem Server ausgeführt. Die **Live Stock Tabelle** zeigt, dass sich die Bestände weiter verändert haben. Die Anfangstabelle mit Denkzahlen ohne Änderung wird nicht angezeigt.

1. Schließen Sie den Browser.

## <a name="enable-logging"></a>Aktivieren der Protokollierung

SignalR verfügt über eine integrierte Protokollierungsfunktion, die Sie auf dem Client aktivieren können, um bei der Fehlerbehebung zu helfen. In diesem Abschnitt aktivieren Sie die Protokollierung und zeigen Beispiele, die zeigen, wie Protokolle Ihnen sagen, welche der folgenden Transportmethoden SignalR verwendet:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), unterstützt von IIS 8 und aktuellen Browsern.

* [Servergesendete Ereignisse](http://en.wikipedia.org/wiki/Server-sent_events), die von anderen Browsern als Internet Explorer unterstützt werden.

* [Forever-Frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), unterstützt von Internet Explorer.

* [Ajax Long Polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), unterstützt von allen Browsern.

Für jede Verbindung wählt SignalR die beste Transportmethode aus, die sowohl der Server als auch der Client unterstützen.

1. Öffnen Sie *StockTicker.js*.

1. Fügen Sie diese hervorgehobene Codezeile hinzu, um die Protokollierung unmittelbar vor dem Code zu aktivieren, der die Verbindung am Ende der Datei initialisiert:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Drücken Sie **F5,** um das Projekt auszuführen.

1. Öffnen Sie das Entwicklertools-Fenster Ihres Browsers, und wählen Sie die Konsole aus, um die Protokolle anzuzeigen. Möglicherweise müssen Sie die Seite aktualisieren, um die Protokolle von SignalR anzuzeigen, die die Transportmethode für eine neue Verbindung aushandeln.

    * Wenn Sie Internet Explorer 10 unter Windows 8 (IIS 8) ausführen, lautet die Transportmethode **WebSockets**.

    * Wenn Sie Internet Explorer 10 unter Windows 7 (IIS 7.5) ausführen, lautet die Transportmethode **iframe**.

    * Wenn Sie Firefox 19 unter Windows 8 (IIS 8) ausführen, lautet die Transportmethode **WebSockets**.

        > [!TIP]
        > Installieren Sie in Firefox das Firebug-Add-In, um ein Konsolenfenster zu erhalten.

    * Wenn Sie Firefox 19 unter Windows 7 (IIS 7.5) ausführen, ist die Transportmethode **servergesendete** Ereignisse.

## <a name="install-the-stockticker-sample"></a>Installieren Sie das StockTicker-Beispiel

[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installiert die StockTicker-Anwendung. Das NuGet-Paket enthält mehr Funktionen als die vereinfachte Version, die Sie von Grund auf neu erstellt haben. In diesem Abschnitt des Tutorials installieren Sie das NuGet-Paket und überprüfen die neuen Features und den Code, der sie implementiert.

> [!IMPORTANT]
> Wenn Sie das Paket installieren, ohne die vorherigen Schritte dieses Tutorials auszuführen, müssen Sie dem Projekt eine OWIN-Startklasse hinzufügen. Diese Readme.txt-Datei für das NuGet-Paket erklärt diesen Schritt.

### <a name="install-the-signalrsample-nuget-package"></a>Installieren des SignalR.Sample NuGet-Pakets

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten** aus.

1. Wählen Sie unter **NuGet Package Manager: SignalR.StockTicker**die Option **Durchsuchen**aus.

1. Wählen Sie unter **Paketquelle** **nuget.org**aus.

1. Geben Sie *SignalR.Sample* in das Suchfeld ein und wählen Sie **Microsoft.AspNet.SignalR.Sample** > **Install**aus.

1. Erweitern Sie im **Projektmappen-Explorer**den Ordner *SignalR.Sample.*

    Durch die Installation des SignalR.Sample-Pakets wurde der Ordner und sein Inhalt erstellt.

1. Klicken Sie im Ordner *SignalR.Sample* mit der rechten Maustaste auf *StockTicker.html*, und wählen Sie dann **Als Startseite festlegen**aus.

    > [!NOTE]
    > Die Installation des SignalR.Sample NuGet-Pakets kann die Version von jQuery ändern, die Sie in Ihrem *Scripts-Ordner* haben. Die neue *Datei StockTicker.html,* die das Paket im *Ordner SignalR.Sample* installiert, ist mit der jQuery-Version synchron, die das Paket installiert, aber wenn Sie Ihre ursprüngliche *StockTicker.html-Datei* erneut ausführen möchten, müssen Sie möglicherweise zuerst den jQuery-Verweis im Skript-Tag aktualisieren.

### <a name="run-the-application"></a>Ausführen der Anwendung

 Die Tabelle, die Sie in der ersten App gesehen haben, hatte nützliche Funktionen. Die vollständige Stock-Ticker-Anwendung zeigt neue Funktionen: ein horizontal scrollendes Fenster, das die Bestandsdaten und Aktien anzeigt, die ihre Farbe ändern, wenn sie steigen und fallen.

1. Drücken Sie **F5** , um die App auszuführen.

     Wenn Sie die App zum ersten Mal ausführen, wird der "Markt" "geschlossen" und Sie sehen eine statische Tabelle und ein Tickerfenster, das nicht scrollt.

1. Wählen Sie **Open Market**.

    ![Screenshot des Livetickers.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * Das **Live Stock Ticker-Feld** beginnt horizontal zu scrollen, und der Server beginnt, regelmäßig Aktienkursänderungen nach dem Zufallsprinzip zu übertragen.

    * Jedes Mal, wenn sich ein Aktienkurs ändert, aktualisiert die App sowohl die **Live Stock Table** als auch den Live Stock **Ticker**.

    * Wenn die Kursänderung einer Aktie positiv ist, zeigt die App die Aktie mit grünem Hintergrund an.

    * Wenn die Änderung negativ ist, zeigt die App den Bestand mit einem roten Hintergrund an.

1. Wählen Sie **Markt schließen**.

    * Die Tabellenaktualisierungen beenden.

    * Der Ticker hört auf zu scrollen.

1. Klicken Sie auf **Zurücksetzen**.

    * Alle Bestandsdaten werden zurückgesetzt.

    * Die App stellt den Anfangszustand wieder her, bevor Preisänderungen gestartet werden.

1. Kopieren Sie die URL aus dem Browser, öffnen Sie zwei weitere Browser, und fügen Sie die URLs in die Adressleisten ein.

1. In jedem Browser werden dieselben Daten dynamisch gleichzeitig aktualisiert.

1. Wenn Sie eines der Steuerelemente auswählen, reagieren alle Browser gleichzeitig auf die gleiche Weise.

### <a name="live-stock-ticker-display"></a>Live Stock Ticker Anzeige

Die **Live Stock Ticker** Anzeige ist `<div>` eine ungeordnete Liste in einem Element, das von CSS-Stilen in eine einzelne Zeile formatiert ist. Die App initialisiert und aktualisiert den Ticker auf die gleiche Weise `<li>` wie die Tabelle: durch Ersetzen von Platzhaltern in einer Vorlagenzeichenfolge und dynamisches Hinzufügen der `<li>` Elemente zum `<ul>` Element. Die App enthält einen Bildlauf `animate` mit der funktion jQuery, um den `<div>`Rand links der ungeordneten Liste innerhalb der zu variieren.

#### <a name="signalrsample-stocktickerhtml"></a>SignalR.Sample StockTicker.html

Der Aktienticker HTML-Code:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR.Sample StockTicker.css

Der Börsenticker CSS-Code:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR.Sample SignalR.StockTicker.js

Der jQuery-Code, mit dem er scrollen kann:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Zusätzliche Methoden auf dem Server, die der Client aufrufen kann

Um der App mehr Flexibilität zu verleihen, gibt es zusätzliche Methoden, die die App aufrufen kann.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR.Sample StockTickerHub.cs

Die `StockTickerHub` Klasse definiert vier zusätzliche Methoden, die der Client aufrufen kann:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Die App `OpenMarket` `CloseMarket`ruft `Reset` , und als Reaktion auf die Schaltflächen oben auf der Seite auf. Sie veranschaulichen das Muster eines Clients, der eine Statusänderung auslöst, die sofort an alle Clients weitergegeben wird. Jede dieser Methoden ruft eine `StockTicker` Methode in der Klasse auf, die die Änderung des Marktstatus verursacht, und sendet dann den neuen Status.

#### <a name="signalrsample-stocktickercs"></a>SignalR.Sample StockTicker.cs

In `StockTicker` der Klasse behält die App den `MarketState` Status des `MarketState` Marktes mit einer Eigenschaft bei, die einen Enumeratwert zurückgibt:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Jede der Methoden, die den Marktstatus ändern, `StockTicker` tun dies innerhalb eines Sperrblocks, da die Klasse threadsicher sein muss:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Um sicherzustellen, dass dieser Code `_marketState` threadsicher ist, `MarketState` wird `volatile`das Feld, das die angegebene Eigenschaft unterstützt:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

Die `BroadcastMarketStateChange` `BroadcastMarketReset` und-Methoden ähneln der BroadcastStockPrice-Methode, die Sie bereits gesehen haben, außer sie rufen verschiedene Methoden auf, die auf dem Client definiert sind:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Zusätzliche Funktionen auf dem Client, die der Server aufrufen kann

Die `updateStockPrice` Funktion verarbeitet nun sowohl die Tabelle als `jQuery.Color` auch die Tickeranzeige und blinkt in rot-grünen Farben.

Neue Funktionen in *SignalR.StockTicker.js* aktivieren und deaktivieren die Schaltflächen basierend auf dem Marktstatus. Sie stoppen oder starten auch das **Live Stock Ticker** horizontales Scrollen. Da viele Funktionen zu `ticker.client`hinzugefügt werden, verwendet die App die [funktion jQuery extend,](http://api.jquery.com/jQuery.extend/) um sie hinzuzufügen.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Zusätzliche Clienteinrichtung nach dem Herstellen der Verbindung

Nachdem der Client die Verbindung hergestellt hat, muss noch einiges an Arbeit zu erledigen sein:

* Finden Sie heraus, ob der Markt `marketOpened` geöffnet `marketClosed` oder geschlossen ist, um die entsprechende Funktion aufzurufen.

* Fügen Sie die Servermethodenaufrufe an die Schaltflächen an.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Die Servermethoden werden erst mit den Schaltflächen verdrahtet, nachdem die App die Verbindung hergestellt hat. Es ist so, dass der Code die Servermethoden nicht aufrufen kann, bevor sie verfügbar sind.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

In diesem Tutorial haben Sie gelernt, wie Sie eine SignalR-Anwendung programmieren, die Nachrichten vom Server an alle verbundenen Clients überträgt. Jetzt können Sie Nachrichten regelmäßig und als Reaktion auf Benachrichtigungen von jedem Client senden. Sie können das Konzept der Singleton-Instanz mit mehreren Threads verwenden, um den Serverstatus in Multiplayer-Onlinespielszenarien beizubehalten. Ein Beispiel finden Sie [im ShootR-Spiel basierend auf SignalR](https://github.com/NTaylorMullen/ShootR).

Tutorials, die Peer-to-Peer-Kommunikationsszenarien zeigen, finden Sie unter [Erste Schritte mit SignalR](introduction-to-signalr.md) und [Echtzeitaktualisierung mit SignalR](tutorial-high-frequency-realtime-with-signalr.md).

Weitere Informationen zu SignalR finden Sie in den folgenden Ressourcen:

* [ASP.NET SignalR](../../index.md)
* [SignalR-Projekt](http://signalr.net/)
* [SignalR GitHub und Samples](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial führen Sie Folgendes durch:

> [!div class="checklist"]
> * Erstellt das Projekt
> * Einrichten des Servercodes
> * Geprüft den Servercode
> * Einrichten des Clientcodes
> * Geprüft den Clientcode
> * Testen der Anwendung
> * Aktivierte Protokollierung

Fahren Sie mit dem nächsten Artikel fort, um zu erfahren, wie Sie eine Echtzeit-Webanwendung erstellen, die ASP.NET SignalR 2 verwendet.
> [!div class="nextstepaction"]
> [Erstellen einer Echtzeit-Web-App mit SignalR](real-time-web-applications-with-signalr.md)
