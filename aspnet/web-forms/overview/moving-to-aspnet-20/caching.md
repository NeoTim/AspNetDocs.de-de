---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Caching | Microsoft Docs
author: rick-anderson
description: Ein Verständnis des Cachings ist wichtig für eine leistungsstarke ASP.NET Anwendung. ASP.NET 1.x bot drei verschiedene Möglichkeiten zum Caching; Ausgangszwischenspeicherung,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542936"
---
# <a name="caching"></a>Zwischenspeicherung

von [Microsoft](https://github.com/microsoft)

> Ein Verständnis des Cachings ist wichtig für eine leistungsstarke ASP.NET Anwendung. ASP.NET 1.x bot drei verschiedene Möglichkeiten zum Caching; Ausgabezwischenspeicherung, Fragmentzwischenspeicherung und die Cache-API.

Ein Verständnis des Cachings ist wichtig für eine leistungsstarke ASP.NET Anwendung. ASP.NET 1.x bot drei verschiedene Möglichkeiten zum Caching; Ausgabezwischenspeicherung, Fragmentzwischenspeicherung und die Cache-API. ASP.NET 2.0 bietet alle drei dieser Methoden, fügt aber einige wichtige zusätzliche Funktionen hinzu. Es gibt mehrere neue Cacheabhängigkeiten, und Entwickler haben jetzt die Möglichkeit, auch benutzerdefinierte Cacheabhängigkeiten zu erstellen. Auch die Konfiguration des Cachings wurde in ASP.NET 2.0 deutlich verbessert.

## <a name="new-features"></a>Neue Funktionen

## <a name="cache-profiles"></a>Cache-Profile

Cacheprofile ermöglichen es Entwicklern, bestimmte Cacheeinstellungen zu definieren, die dann auf einzelne Seiten angewendet werden können. Wenn Sie z. B. einige Seiten haben, die nach 12 Stunden aus dem Cache abgelaufen sein sollen, können Sie problemlos ein Cacheprofil erstellen, das auf diese Seiten angewendet werden kann. Um ein neues Cacheprofil &lt;hinzuzufügen,&gt; verwenden Sie den Abschnitt outputCacheSettings in der Konfigurationsdatei. Im Folgenden finden Sie beispielsweise die Konfiguration eines Cacheprofils namens *Twoday,* das eine Cachedauer von 12 Stunden konfiguriert.

[!code-xml[Main](caching/samples/sample1.xml)]

Um dieses Cacheprofil auf eine bestimmte Seite anzuwenden, verwenden Sie das CacheProfile-Attribut der Direktive , wie unten gezeigt:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Benutzerdefinierte Cacheabhängigkeiten

ASP.NET 1.x-Entwickler schrien nach benutzerdefinierten Cache-Abhängigkeiten. In ASP.NET 1.x wurde die CacheDependency-Klasse versiegelt, was Entwickler daran hinderte, ihre eigenen Klassen daraus ableiten zu können. In ASP.NET 2.0 wird diese Einschränkung entfernt, und Entwickler können ihre eigenen benutzerdefinierten Cacheabhängigkeiten entwickeln. Die CacheDependency-Klasse ermöglicht die Erstellung einer benutzerdefinierten Cacheabhängigkeit basierend auf Dateien, Verzeichnissen oder Cacheschlüsseln.

Der folgende Code erstellt z. B. eine neue benutzerdefinierte Cacheabhängigkeit basierend auf einer Datei namens stuff.xml, die sich im Stammverzeichnis der Webanwendung befindet:

[!code-csharp[Main](caching/samples/sample3.cs)]

In diesem Szenario wird das zwischengespeicherte Element ungültig, wenn sich die Datei stuff.xml ändert.

Es ist auch möglich, eine benutzerdefinierte Cacheabhängigkeit mithilfe von Cacheschlüsseln zu erstellen. Bei Dieser Methode werden durch das Entfernen des Cacheschlüssels die zwischengespeicherten Daten ungültig. Das folgende Beispiel veranschaulicht dies:

[!code-csharp[Main](caching/samples/sample4.cs)]

Um das oben eingefügte Element ungültig zu machen, entfernen Sie einfach das Element, das in den Cache eingefügt wurde, um als Cacheschlüssel zu fungieren.

[!code-csharp[Main](caching/samples/sample5.cs)]

Beachten Sie, dass der Schlüssel des Elements, das als Cacheschlüssel fungiert, mit dem Wert identisch sein muss, der dem Array von Cacheschlüsseln hinzugefügt wird.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Polling-basierte SQL-Cache-Abhängigkeiten (auch als tabellenbasierte Abhängigkeiten bezeichnet)

SQL Server 7 und 2000 verwenden das abfragebasierte Modell für SQL-Cacheabhängigkeiten. Das abfragebasierte Modell verwendet einen Trigger für eine Datenbanktabelle, der ausgelöst wird, wenn sich die Daten in der Tabelle ändern. Dieser Trigger aktualisiert ein **changeId-Feld** in der Benachrichtigungstabelle, das regelmäßig überprüft ASP.NET. Wenn das **Feld changeId** aktualisiert wurde, weiß ASP.NET, dass sich die Daten geändert haben, und die zwischengespeicherten Daten werden ungültig.

> [!NOTE]
> SQL Server 2005 kann auch das abfragebasierte Modell verwenden, aber da das abfragebasierte Modell nicht das effizienteste Modell ist, ist es ratsam, ein abfragebasiertes Modell (später erläutert) mit SQL Server 2005 zu verwenden.

Damit eine SQL-Cacheabhängigkeit, die das abfragebasierte Modell verwendet, ordnungsgemäß funktioniert, müssen in den Tabellen Benachrichtigungen aktiviert sein. Dies kann programmgesteuert mit der SqlCacheDependencyAdmin-Klasse oder\_mit dem Dienstprogramm aspnet regsql.exe erreicht werden.

Die folgende Befehlszeile registriert die Tabelle Products in der Northwind-Datenbank auf einer SQL Server-Instanz mit dem Namen *dbase* for SQL Cache Dependency.

[!code-console[Main](caching/samples/sample6.cmd)]

Im Folgenden finden Sie eine Erläuterung der Befehlszeilenschalter, die im obigen Befehl verwendet werden:

| **Befehlszeilenschalter** | **Zweck** |
| --- | --- |
| -S *server* | Gibt den Servernamen an. |
| -ed | Gibt an, dass die Datenbank für die SQL-Cacheabhängigkeit aktiviert werden soll. |
| -d *\_Datenbankname* | Gibt den Datenbanknamen an, der für die SQL-Cacheabhängigkeit aktiviert werden soll. |
| -E | Gibt an, dass\_aspnet regsql die Windows-Authentifizierung beim Herstellen einer Verbindung mit der Datenbank verwenden soll. |
| -et | Gibt an, dass wir eine Datenbanktabelle für die SQL-Cacheabhängigkeit aktivieren. |
| -t *\_Tabellenname* | Gibt den Namen der Datenbanktabelle an, um die SQL-Cacheabhängigkeit zu aktivieren. |

> [!NOTE]
> Für aspnet\_regsql.exe stehen weitere Switches zur Verfügung. Führen Sie für eine vollständige\_Liste aspnet regsql.exe -? über eine Befehlszeile.

Wenn dieser Befehl ausgeführt wird, werden die folgenden Änderungen an der SQL Server-Datenbank vorgenommen:

- Eine **AspNet\_SqlCacheTablesForChangeNotification-Tabelle** wird hinzugefügt. Diese Tabelle enthält eine Zeile für jede Tabelle in der Datenbank, für die eine SQL-Cache-Abhängigkeit aktiviert wurde.
- Die folgenden gespeicherten Prozeduren werden innerhalb der Datenbank erstellt:

| AspNet\_SqlCachePollingStoredProcedure | Fragt die AspNet\_SqlCacheTablesForChangeNotification-Tabelle ab und gibt alle Tabellen zurück, die für die SQL-Cacheabhängigkeit aktiviert sind, sowie den Wert von changeId für jede Tabelle. Dieser gespeicherte proc wird zum Abrufen verwendet, um festzustellen, ob sich die Daten geändert haben. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | Gibt alle für die SQL-Cache-Abhängigkeit aktivierten\_Tabellen zurück, indem die AspNet SqlCacheTablesForChangeNotification-Tabelle abgefragt wird, und gibt alle Tabellen zurück, die für die SQL-Cache-Abhängigkeit aktiviert sind. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | Registriert eine Tabelle für die SQL-Cacheabhängigkeit, indem der erforderliche Eintrag in der Benachrichtigungstabelle hinzugefügt und der Trigger hinzugefügt wird. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | Hebt die Registrierung einer Tabelle für die SQL-Cacheabhängigkeit auf, indem der Eintrag in der Benachrichtigungstabelle entfernt wird, und der Trigger entfernt wird. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | Aktualisiert die Benachrichtigungstabelle, indem die changeId für die geänderte Tabelle erhöht wird. ASP.NET verwendet diesen Wert, um zu bestimmen, ob sich die Daten geändert haben. Wie unten angegeben, wird dieser gespeicherte proc durch den Trigger ausgeführt, der erstellt wird, wenn die Tabelle aktiviert ist. |

- Für die Tabelle wird ein SQL Server-Trigger namens ** _Tabellenname\__\_AspNet\_SqlCacheNotification\_Trigger** erstellt. Dieser Trigger führt die\_AspNet SqlCacheUpdateChangeIdStoredProcedure aus, wenn insert, UPDATE oder DELETE für die Tabelle ausgeführt wird.
- Der Datenbank wird eine SQL Server-Rolle namens **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** hinzugefügt.

Die **Aspnet\_\_ChangeNotification ReceiveNotificationsOnlyAccess** SQL Server-Rolle verfügt\_über EXEC-Berechtigungen für die AspNet SqlCachePollingStoredProcedure.- Damit das Abrufmodell ordnungsgemäß funktioniert, müssen Sie Ihr Prozesskonto\_der\_Rolle aspnet ChangeNotification ReceiveNotificationsOnlyAccess hinzufügen. Das Tool\_aspnet regsql.exe tut dies nicht für Sie.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Konfigurieren von Polling-basierten SQL-Cache-Abhängigkeiten

Es gibt mehrere Schritte, die zum Konfigurieren von abfragebasierten SQL-Cache-Abhängigkeiten erforderlich sind. Der erste Schritt besteht darin, die Datenbank und die Tabelle wie oben beschrieben zu aktivieren. Sobald dieser Schritt abgeschlossen ist, ist der Rest der Konfiguration wie folgt:

- Konfigurieren der ASP.NET Konfigurationsdatei.
- Konfigurieren der SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>Konfigurieren der ASP.NET Konfigurationsdatei

Zusätzlich zum Hinzufügen einer Verbindungszeichenfolge, wie in einem vorherigen &lt;&gt; Modul erläutert, müssen Sie auch ein Cacheelement mit einem &lt;sqlCacheDependency-Element&gt; konfigurieren, wie unten gezeigt:

[!code-xml[Main](caching/samples/sample7.xml)]

Diese Konfiguration ermöglicht eine SQL-Cacheabhängigkeit von der *pubs-Datenbank.* Beachten Sie, dass das &lt;pollTime-Attribut im sqlCacheDependency-Element&gt; standardmäßig 60000 Millisekunden oder 1 Minute beträgt. (Dieser Wert darf nicht kleiner als 500 Millisekunden sein.) In diesem Beispiel &lt;&gt; fügt das Add-Element eine neue Datenbank hinzu und überschreibt die pollTime, indem sie auf 9000000 Millisekunden gesetzt wird.

#### <a name="configuring-the-sqlcachedependency"></a>Konfigurieren der SqlCacheDependency

Der nächste Schritt besteht darin, die SqlCacheDependency zu konfigurieren. Die einfachste Möglichkeit, dies zu erreichen, besteht darin, den Wert für das SqlDependency-Attribut in der Direktive " Outcache" wie folgt anzugeben:

[!code-aspx[Main](caching/samples/sample8.aspx)]

In der obigen OutputCache-Direktive wird eine SQL-Cache-Abhängigkeit für die *Authors-Tabelle* in der *pubs-Datenbank* konfiguriert. Mehrere Abhängigkeiten können konfiguriert werden, indem sie durch ein Semikolon wie folgt getrennt werden:

[!code-aspx[Main](caching/samples/sample9.aspx)]

Eine weitere Methode zum Konfigurieren der SqlCacheDependency besteht darin, dies programmgesteuert zu tun. Der folgende Code erstellt eine neue SQL-Cacheabhängigkeit von der *Authors-Tabelle* in der *pubs-Datenbank.*

[!code-csharp[Main](caching/samples/sample10.cs)]

Einer der Vorteile der programmgesteuerten Definition der SQL-Cacheabhängigkeit besteht darin, dass Sie alle auftretenden Ausnahmen behandeln können. Wenn Sie beispielsweise versuchen, eine SQL-Cacheabhängigkeit für eine Datenbank zu definieren, die nicht für benachrichtigungsfähig ist, wird eine **DatabaseNotEnabledForNotificationException-Ausnahme** ausgelöst. In diesem Fall können Sie versuchen, die Datenbank für Benachrichtigungen zu aktivieren, indem Sie die **SqlCacheDependencyAdmin.EnableNotifications-Methode** aufrufen und den Datenbanknamen übergeben.

Wenn Sie versuchen, eine SQL-Cacheabhängigkeit für eine Tabelle zu definieren, die nicht für die Benachrichtigung aktiviert wurde, wird eine **TableNotEnabledForNotificationException** ausgelöst. Sie können dann die **SqlCacheDependencyAdmin.EnableTableForNotifications-Methode** aufrufen, die den Datenbanknamen und den Tabellennamen übergibt.

Das folgende Codebeispiel veranschaulicht, wie die Ausnahmebehandlung beim Konfigurieren einer SQL-Cacheabhängigkeit ordnungsgemäß konfiguriert wird.

[!code-csharp[Main](caching/samples/sample11.cs)]

Weitere Informationen:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Abfragebasierte SQL-Cache-Abhängigkeiten (nur SQL Server 2005)

Bei Verwendung von SQL Server 2005 für SQL-Cacheabhängigkeit ist das abfragebasierte Modell nicht erforderlich. Bei Verwendung mit SQL Server 2005 kommunizieren SQL-Cacheabhängigkeiten mithilfe von SQL Server 2005-Abfragebenachrichtigungen direkt über SQL-Verbindungen mit der SQL Server-Instanz (keine weitere Konfiguration ist erforderlich).

Die einfachste Möglichkeit, abfragebasierte Benachrichtigungen zu aktivieren, besteht darin, dies deklarativ zu tun, indem Sie das **SqlCacheDependency-Attribut** des Datenquellenobjekts auf **CommandNotification** festlegen und das **EnableCaching-Attribut** auf **true**festlegen. Bei dieser Methode ist kein Code erforderlich. Wenn sich das Ergebnis eines Befehls ändert, der für die Datenquelle ausgeführt wird, werden die Cachedaten ungültig.

Im folgenden Beispiel wird ein Datenquellensteuerelement für die SQL-Cacheabhängigkeit konfiguriert:

[!code-aspx[Main](caching/samples/sample12.aspx)]

Wenn in diesem Fall die im **SelectCommand** angegebene Abfrage ein anderes Ergebnis als ursprünglich zurückgibt, werden die zwischengespeicherten Ergebnisse ungültig.

Sie können auch angeben, dass alle Datenquellen für SQL-Cacheabhängigkeiten aktiviert sind, indem Sie das **SqlDependency-Attribut** der Direktive **- OutputCache"** auf **CommandNotification**festlegen. Das folgende Beispiel veranschaulicht dies.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> Weitere Informationen zu Abfragebenachrichtigungen in SQL Server 2005 finden Sie unter SQL Server Books Online.

Eine weitere Methode zum Konfigurieren einer abfragebasierten SQL-Cacheabhängigkeit besteht darin, dies programmgesteuert mithilfe der SqlCacheDependency-Klasse zu tun. Das folgende Codebeispiel veranschaulicht, wie dies erreicht wird.

[!code-csharp[Main](caching/samples/sample14.cs)]

Weitere Informationen:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Post-Cache-Ersetzung

Das Zwischenspeichern einer Seite kann die Leistung einer Webanwendung erheblich steigern. In einigen Fällen müssen jedoch die meisten Seiten zwischengespeichert und einige Fragmente innerhalb der Seite dynamisch sein. Wenn Sie beispielsweise eine Seite mit Nachrichtentexten erstellen, die für festgelegte Zeiträume vollständig statisch ist, können Sie festlegen, dass die gesamte Seite zwischengespeichert wird. Wenn Sie ein rotierendes Werbebanner einfügen möchten, das sich bei jeder Seitenanforderung geändert hat, muss der Teil der Seite, der die Anzeige enthält, dynamisch sein. Damit Sie eine Seite zwischenspeichern, aber einige Inhalte dynamisch ersetzen können, können Sie ASP.NET Post-Cache-Ersetzung verwenden. Bei der Post-Cache-Ersetzung wird die gesamte Seite mit bestimmten Teilen zwischengespeichert, die als vom Zwischenspeichern ausgenommen markiert sind. Im Beispiel der Anzeigenbanner können Sie mit dem AdRotator-Steuerelement die Post-Cache-Ersetzung nutzen, sodass Anzeigen dynamisch für jeden Benutzer und für jede Seitenaktualisierung erstellt werden.

Es gibt drei Möglichkeiten, die Post-Cache-Ersetzung zu implementieren:

- Deklarativ, mit dem Substitutionssteuerelement.
- Programmgesteuert mit der Substitutionssteuerungs-API.
- Implizit mit dem AdRotator-Steuerelement.

### <a name="substitution-control"></a>Substitutionskontrolle

Das ASP.NET Substitution-Steuerelement gibt einen Abschnitt einer zwischengespeicherten Seite an, der dynamisch und nicht zwischengespeichert wird. Sie platzieren ein Ersetzungssteuerelement an der Position auf der Seite, an der der dynamische Inhalt angezeigt werden soll. Zur Laufzeit ruft das Substitution-Steuerelement eine Methode auf, die Sie mit der MethodName-Eigenschaft angeben. Die Methode muss eine Zeichenfolge zurückgeben, die dann den Inhalt des Substitutionssteuerelements ersetzt. Die Methode muss eine statische Methode auf dem enthaltenden Page- oder UserControl-Steuerelement sein. Die Verwendung des Ersetzungssteuerelements bewirkt, dass die clientseitige Cachebarkeit in die Server-Cacheability geändert wird, sodass die Seite nicht auf dem Client zwischengespeichert wird. Dadurch wird sichergestellt, dass zukünftige Anforderungen an die Seite die Methode erneut aufrufen, um dynamischen Inhalt zu generieren.

### <a name="substitution-api"></a>Substitutions-API

Um dynamischen Inhalt für eine zwischengespeicherte Seite programmgesteuert zu erstellen, können Sie die [WriteSubstitution-Methode](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) im Seitencode aufrufen und sie als Parameter übergeben. Die Methode, die die Erstellung des dynamischen Inhalts verarbeitet, nimmt einen einzelnen [HttpContext-Parameter](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) an und gibt eine Zeichenfolge zurück. Die Rückgabezeichenfolge ist der Inhalt, der an der angegebenen Position ersetzt wird. Ein Vorteil beim Aufrufen der WriteSubstitution-Methode anstelle der deklarativen Verwendung des Substitution-Steuerelements besteht darin, dass Sie eine Methode eines beliebigen Objekts aufrufen können, anstatt eine statische Methode der Seite oder des UserControl-Objekts aufzurufen.

Wenn Sie die WriteSubstitution-Methode aufrufen, wird die clientseitige Cachebarkeit in die Server-Cacheability geändert, sodass die Seite nicht auf dem Client zwischengespeichert wird. Dadurch wird sichergestellt, dass zukünftige Anforderungen an die Seite die Methode erneut aufrufen, um dynamischen Inhalt zu generieren.

### <a name="adrotator-control"></a>AdRotator-Steuerung

Das AdRotator-Serversteuerelement implementiert intern Unterstützung für die Post-Cache-Ersetzung. Wenn Sie ein AdRotator-Steuerelement auf Ihrer Seite platzieren, werden für jede Anforderung eindeutige Anzeigen gerendert, unabhängig davon, ob die übergeordnete Seite zwischengespeichert wird. Daher wird eine Seite, die ein AdRotator-Steuerelement enthält, nur serverseitig zwischengespeichert.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy-Klasse

Die ControlCachePolicy-Klasse ermöglicht die programmgesteuerte Steuerung der Fragmentzwischenspeicherung mithilfe von Benutzersteuerelementen. ASP.NET bettet Benutzersteuerelemente in eine [BasePartialCachingControl-Instanz](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) ein. Die BasePartialCachingControl-Klasse stellt ein Benutzersteuerelement dar, für das die Ausgabezwischenspeicherung aktiviert ist.

Wenn Sie auf die [BasePartialCachingControl.CachePolicy-Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) eines [PartialCachingControl-Steuerelements](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) zugreifen, erhalten Sie immer ein gültiges ControlCachePolicy-Objekt. Wenn Sie jedoch auf die [UserControl.CachePolicy-Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) eines [UserControl-Steuerelements](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) zugreifen, erhalten Sie ein gültiges ControlCachePolicy-Objekt nur, wenn das Benutzersteuerelement bereits von einem BasePartialCachingControl-Steuerelement umschlossen ist. Wenn es nicht umschlossen ist, löst das controlCachePolicy-Objekt, das von der Eigenschaft zurückgegeben wird, Ausnahmen aus, wenn Sie versuchen, es zu bearbeiten, da es nicht über ein zugeordnetes BasePartialCachingControl verfügt. Um zu ermitteln, ob eine UserControl-Instanz das Zwischenspeichern unterstützt, ohne Ausnahmen zu generieren, überprüfen Sie die [SupportsCaching-Eigenschaft.](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)

Die Verwendung der ControlCachePolicy-Klasse ist eine von mehreren Möglichkeiten, wie Sie die Ausgabezwischenspeicherung aktivieren können. In der folgenden Liste werden Methoden beschrieben, mit denen Sie die Ausgabezwischenspeicherung aktivieren können:

- Verwenden Sie die [-OutputCache-Direktive,](https://msdn.microsoft.com/library/hdxfb6cy.aspx) um die Ausgabezwischenspeicherung in deklarativen Szenarien zu aktivieren.
- Verwenden Sie das [PartialCachingAttribute-Attribut,](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) um das Zwischenspeichern für ein Benutzersteuerelement in einer CodeBehind-Datei zu aktivieren.
- Verwenden Sie die ControlCachePolicy-Klasse, um Cacheeinstellungen in programmgesteuerten Szenarien anzugeben, in denen Sie mit BasePartialCachingControl-Instanzen arbeiten, die mit einer der vorherigen Methoden cacheaktiviert und dynamisch mit der [System.Web.UI.TemplateControl.LoadControl-Methode](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) geladen wurden.

Eine ControlCachePolicy-Instanz kann nur zwischen der Init- und der PreRender-Phase des Steuerelementlebenszyklus erfolgreich bearbeitet werden. Wenn Sie ein ControlCachePolicy-Objekt nach der PreRender-Phase ändern, löst ASP.NET eine Ausnahme aus, da alle Änderungen, die nach dem Rendern des Steuerelements vorgenommen wurden, die Cacheeinstellungen nicht tatsächlich beeinflussen können (ein Steuerelement wird während der Renderphase zwischengespeichert). Schließlich ist eine Benutzersteuerungsinstanz (und damit ihr ControlCachePolicy-Objekt) nur für programmgesteuerte Manipulationen verfügbar, wenn sie tatsächlich gerendert wird.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Änderungen an der Caching-Konfiguration - Das &lt;Zwischenspeichern-Element&gt;

In ASP.NET 2.0 gibt es mehrere Änderungen an der Caching-Konfiguration. Das &lt;Caching-Element&gt; ist neu in ASP.NET 2.0 und ermöglicht es Ihnen, Konfigurationsänderungen in der Konfigurationsdatei vorzunehmen. Die folgenden Attribute sind verfügbar.

| **Element** | **Beschreibung** |
| --- | --- |
| **Cache** | Optionales Element. Definiert globale Anwendungscacheeinstellungen. |
| **Outputcache** | Optionales Element. Gibt anwendungsweite Ausgabecacheeinstellungen an. |
| **outputCacheSettings** | Optionales Element. Gibt Ausgabecacheeinstellungen an, die auf Seiten in der Anwendung angewendet werden können. |
| **sqlCacheDependency** | Optionales Element. Konfiguriert die SQL-Cacheabhängigkeiten für eine ASP.NET-Anwendung. |

### <a name="the-ltcachegt-element"></a>Das &lt;&gt; Cacheelement

Die folgenden Attribute sind &lt;im&gt; Cacheelement verfügbar:

| **attribute** | **Beschreibung** |
| --- | --- |
| **disableMemoryCollection** | Optionales **boolescher** Attribut. Ruft einen Wert ab oder legt einen Wert fest, der angibt, ob die Cachespeichersammlung, die auftritt, wenn der Computer unter Speicherdruck steht, deaktiviert ist. |
| **disableExpiration** | Optionales **boolescher** Attribut. Ruft einen Wert ab oder legt einen Wert fest, der angibt, ob der Cacheablauf deaktiviert ist. Wenn diese Option deaktiviert ist, laufen zwischengespeicherte Elemente nicht ab, und es findet keine Hintergrundaufräumung abgelaufener Cacheelemente statt. |
| **privateBytesLimit** | Optionales **Int64-Attribut.** Ruft einen Wert ab oder legt einen Wert fest, der die maximale Größe der privaten Bytes einer Anwendung angibt, bevor der Cache mit dem Leeren abgelaufener Elemente beginnt und versucht, Den Speicher wiederzugewinnen. Dieser Grenzwert umfasst sowohl den vom Cache verwendeten Speicher als auch den normalen Speicheraufwand der ausgeführten Anwendung. Die Einstellung Null gibt an, dass ASP.NET seine eigenen Heuristiken verwenden, um zu bestimmen, wann mit dem Zurückgewinnen von Speicher begonnen werden soll. |
| **percentagePhysicalMemoryUsedLimit** | Optionales **Int32-Attribut.** Ruft einen Wert ab oder legt einen Wert fest, der den maximalen Prozentsatz des physischen Speichers eines Computers angibt, der von einer Anwendung verbraucht werden kann, bevor der Cache mit dem Leeren abgelaufener Elemente beginnt und versucht, Speicher wiederaufzugeben. Die Einstellung Null gibt an, dass ASP.NET seine eigenen Heuristiken verwenden, um zu bestimmen, wann mit dem Zurückgewinnen von Speicher begonnen werden soll. |
| **privateBytesPollTime** | Optionales **TimeSpan-Attribut.** Ruft einen Wert ab oder legt einen Wert fest, der das Zeitintervall zwischen dem Abruf nach der Speichernutzung privater Bytes der Anwendung angibt. |

### <a name="the-ltoutputcachegt-element"></a>Das &lt;outputCache-Element&gt;

Die folgenden Attribute sind &lt;für&gt; das outputCache-Element verfügbar.

|       <strong>attribute</strong>        |                                                                                                                                                                                                                                                       <strong>Beschreibung</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          Optionales <strong>boolescher</strong> Attribut. Aktiviert/deaktiviert den Seitenausgabecache. Wenn diese Option deaktiviert ist, werden unabhängig von den programmgesteuerten oder deklarativen Einstellungen keine Seiten zwischengespeichert. Der Standardwert ist <strong>true</strong>.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                Optionales <strong>boolescher</strong> Attribut. Aktiviert/deaktiviert den Anwendungsfragmentcache. Wenn diese Option deaktiviert ist, werden keine Seiten zwischengespeichert, unabhängig von der verwendeten [OutputCache-Direktive](https://msdn.microsoft.com/library/hdxfb6cy.aspx) oder dem Zwischenspeicherungsprofil. Enthält einen Cache-Steuerelementheader, der angibt, dass Upstream-Proxyserver sowie Browserclients nicht versuchen sollten, die Seitenausgabe zwischenzuspeichern. Der Standardwert ist <strong>false</strong>.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      Optionales <strong>boolescher</strong> Attribut. Ruft einen Wert ab oder legt einen Wert fest, der angibt, ob der <strong>Cache-Control:private-Header</strong> standardmäßig vom Ausgabecachemodul gesendet wird. Der Standardwert ist <strong>false</strong>.                                                                                                                                                      |
|      <strong>weglassenVaryStar</strong>      | Optionales <strong>boolescher</strong> Attribut. Aktiviert/deaktiviert das Senden<strong>eines \<Http - Vary: /strong><em>" Headers in der Antwort. Mit der Standardeinstellung false</em>wird ein \*Header " *Vary: <strong>" für die Ausgabe zwischengespeicherte Seiten gesendet. Wenn der Vary-Header gesendet wird, können verschiedene Versionen basierend auf den Im vary-Header angegebenen Angaben zwischengespeichert werden. Beispielsweise speichert <em>Vary:User-Agents</em> verschiedene Versionen einer Seite basierend auf dem Benutzer-Agent, der die Anforderung ausstellt. Der Standardwert ist **false</strong>. |

### <a name="the-ltoutputcachesettingsgt-element"></a>Das &lt;outputCacheSettings-Element&gt;

Das &lt;outputCacheSettings-Element&gt; ermöglicht die Erstellung von Cacheprofilen, wie zuvor beschrieben. Das einzige untergeordnete &lt;Element für&gt; das &lt;outputCacheSettings-Element ist das outputCacheProfiles-Element&gt; zum Konfigurieren von Cacheprofilen.

### <a name="the-ltsqlcachedependencygt-element"></a>Das &lt;sqlCacheDependency-Element&gt;

Die folgenden Attribute sind &lt;für das&gt; sqlCacheDependency-Element verfügbar.

| **attribute** | **Beschreibung** |
| --- | --- |
| **Aktiviert** | Erforderliches **boolesches** Attribut. Gibt an, ob Änderungen abgefragt werden. |
| **pollTime** | Optionales **Int32-Attribut.** Legt die Häufigkeit fest, mit der sqlCacheDependency die Datenbanktabelle nach Änderungen abfragt. Dieser Wert entspricht der Anzahl der Millisekunden zwischen aufeinanderfolgenden Abfragen. Sie darf nicht auf weniger als 500 Millisekunden festgelegt werden. Der Standardwert ist 1 Minute. |

### <a name="more-information"></a>Weitere Informationen

Es gibt einige zusätzliche Informationen, die Sie bezüglich der Cachekonfiguration beachten sollten.

- Wenn der Grenzwert für den Arbeitsprozess für private Bytes nicht festgelegt ist, verwendet der Cache einen der folgenden Grenzwerte: 

    - x86 2GB: 800MB oder 60% des physischen RAM, je nach
    - x86 3GB: 1800MB oder 60% des physischen RAM, je nach
    - x64: 1 Terabyte oder 60% des physischen RAM, je nach
- Wenn sowohl das Limit für &lt;den Workerprozess&gt; für private Bytes als auch der Cache privateBytesLimit/ festgelegt sind, verwendet der Cache das Minimum der beiden.
- Genau wie in 1.x legen wir Cache-Einträge ab und rufen GC auf. Sammeln Sie aus zwei Gründen: 

    - Wir sind sehr nah an der Grenze für private Bytes
    - Der verfügbare Speicher ist in der Nähe oder weniger als 10%
- Sie können Trimm- und Cache-Cache für &lt;niedrige verfügbare Speicherbedingungen&gt; effektiv deaktivieren, indem Sie Cache percentagePhysicalMemoryUseLimit/ auf 100 festlegen.
- Im Gegensatz zu 1.x setzt 2.0 das Trimmen aus und sammelt Anrufe, wenn der letzte GC. Collect hat private Bytes oder die Größe der verwalteten Heaps nicht um mehr als 1 % des Speicherlimits (Cache) reduziert.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: Benutzerdefinierte Cacheabhängigkeiten

1. Erstellen Sie eine neue Website.
2. Fügen Sie eine neue XML-Datei namens cache.xml hinzu, und speichern Sie sie im Stammverzeichnis der Webanwendung.
3. Fügen Sie der Page\_Load-Methode im CodeBehind von default.aspx den folgenden Code hinzu: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Fügen Sie oben auf default.aspx in der Quellansicht Folgendes hinzu: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Durchsuchen Sie Default.aspx. Was sagt die Zeit?
6. Aktualisieren Sie den Browser. Was sagt die Zeit?
7. Öffnen Sie cache.xml, und fügen Sie den folgenden Code hinzu: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Speichern Sie cache.xml.
9. Aktualisieren Sie Ihren Browser. Was sagt die Zeit?
10. Erläutern Sie, warum die Uhrzeit aktualisiert wurde, anstatt die zuvor zwischengespeicherten Werte anzuzeigen:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Lab 2: Verwenden von Polling-basierten Cacheabhängigkeiten

Diese Übungseinheit verwendet das Projekt, das Sie im vorherigen Modul erstellt haben, das die Bearbeitung von Daten in der Northwind-Datenbank über ein GridView- und DetailsView-Steuerelement ermöglicht.

1. Öffnen Sie das Projekt in Visual Studio 2005.
2. Führen Sie das\_Dienstprogramm aspnet regsql für die Northwind-Datenbank aus, um die Datenbank und die Tabelle Produkte zu aktivieren. Verwenden Sie den folgenden Befehl aus einer Visual Studio-Eingabeaufforderung: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Fügen Sie Ihrer web.config-Datei Folgendes hinzu: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Fügen Sie ein neues Webformular mit dem Namen showdata.aspx hinzu.
5. Fügen Sie der Seite showdata.aspx die folgende Ausgabecache-Direktive hinzu: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Fügen Sie dem Page\_Load von showdata.aspx den folgenden Code hinzu: 

    [!code-html[Main](caching/samples/sample21.html)]
7. Fügen Sie ein neues SqlDataSource-Steuerelement zu showdata.aspx hinzu und konfigurieren Sie es für die Verwendung der Northwind-Datenbankverbindung. Klicken Sie auf Weiter.
8. Aktivieren Sie die Kontrollkästchen ProductName und ProductID, und klicken Sie auf Weiter.
9. Klicken Sie auf Fertig stellen.
10. Fügen Sie der Seite showdata.aspx eine neue GridView hinzu.
11. Wählen Sie SqlDataSource1 aus der Dropdown-Liste aus.
12. Speichern und durchsuchen Sie showdata.aspx. Notieren Sie sich die angezeigte Zeit.
