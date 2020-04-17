---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Datenquellensteuerung | Microsoft Docs
author: rick-anderson
description: Das DataGrid-Steuerelement in ASP.NET 1.x bedeutete eine große Verbesserung beim Datenzugriff in Webanwendungen. Allerdings war es nicht so benutzerfreundlich, wie es hätte sein können....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540219"
---
# <a name="data-source-controls"></a>Datenquellen-Steuerelemente

von [Microsoft](https://github.com/microsoft)

> Das DataGrid-Steuerelement in ASP.NET 1.x bedeutete eine große Verbesserung beim Datenzugriff in Webanwendungen. Allerdings war es nicht so benutzerfreundlich, wie es hätte sein können. Es erforderte immer noch eine beträchtliche Menge an Code, um viel nützliche Funktionalität von ihm zu erhalten. Das ist das Modell bei allen Datenzugriffsbemühungen in 1.x.

Das DataGrid-Steuerelement in ASP.NET 1.x bedeutete eine große Verbesserung beim Datenzugriff in Webanwendungen. Allerdings war es nicht so benutzerfreundlich, wie es hätte sein können. Es erforderte immer noch eine beträchtliche Menge an Code, um viel nützliche Funktionalität von ihm zu erhalten. Das ist das Modell bei allen Datenzugriffsbemühungen in 1.x.

ASP.NET 2.0 adressiert dies teilweise mit Datenquellensteuerelementen. Die Datenquellensteuerelemente in ASP.NET 2.0 bieten Entwicklern ein deklaratives Modell zum Abrufen von Daten, Anzeigen von Daten und Bearbeiten von Daten. Der Zweck von Datenquellensteuerelementen besteht darin, eine konsistente Darstellung von Daten für datengebundene Steuerelemente unabhängig von der Quelle dieser Daten bereitzustellen. Das Herzstück der Datenquellensteuerelemente in ASP.NET 2.0 ist die abstrakte DataSourceControl-Klasse. Die DataSourceControl-Klasse stellt eine Basisimplementierung der IDataSource-Schnittstelle und der IListSource-Schnittstelle bereit, von der die IListSource die Datenquellensteuerung als DataSource eines datengebundenen Steuerelements (über die später diskutierte neue DataSourceId-Eigenschaft) zuweisen und die darin enthaltenen Daten als Liste verfügbar machen können. Jede Liste von Daten aus einem Datenquellensteuerelement wird als DataSourceView-Objekt verfügbar gemacht. Der Zugriff auf die DataSourceView-Instanzen wird von der IDataSource-Schnittstelle bereitgestellt. Die GetViewNames-Methode gibt beispielsweise eine ICollection zurück, mit der Sie die DataSourceViews auflisten können, die einem bestimmten Datenquellensteuerelement zugeordnet sind, und mit der GetView-Methode können Sie auf eine bestimmte DataSourceView-Instanz nach Namen zugreifen.

Datenquellensteuerelemente haben keine Benutzeroberfläche. Sie werden als Serversteuerelemente implementiert, sodass sie deklarative Syntax unterstützen können und bei Bedarf Zugriff auf den Seitenstatus haben. Datenquellensteuerelemente rendern kein HTML-Markup für den Client.

> [!NOTE]
> Wie Sie später sehen werden, gibt es auch Caching-Vorteile, die durch die Verwendung von Datenquellensteuerelementen erzielt werden.

## <a name="storing-connection-strings"></a>Speichern von Verbindungszeichenfolgen

Bevor wir uns mit der Konfiguration von Datenquellensteuerelementen befassen, sollten wir eine neue Funktion in ASP.NET 2.0 in Bezug auf Verbindungszeichenfolgen behandeln. ASP.NET 2.0 führt einen neuen Abschnitt in die Konfigurationsdatei ein, mit dem Sie Verbindungszeichenfolgen, die zur Laufzeit dynamisch gelesen werden können, einfach speichern können. Der &lt;Abschnitt&gt; connectionStrings erleichtert das Speichern von Verbindungszeichenfolgen.

Der folgende Ausschnitt fügt eine neue Verbindungszeichenfolge hinzu.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> Wie im &lt;Abschnitt&gt; appSettings &lt;wird&gt; der Abschnitt connectionStrings außerhalb des Abschnitts &lt;system.web&gt; in der Konfigurationsdatei angezeigt.

Um diese Verbindungszeichenfolge zu verwenden, können Sie die folgende Syntax verwenden, wenn Sie das ConnectionString-Attribut eines Serversteuerelements festlegen.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

Der &lt;Abschnitt&gt; connectionStrings kann auch verschlüsselt werden, sodass vertrauliche Informationen nicht verfügbar gemacht werden. Diese Fähigkeit wird in einem späteren Modul behandelt.

## <a name="caching-data-sources"></a>Zwischenspeichern von Datenquellen

Jedes DataSourceControl bietet vier Eigenschaften zum Konfigurieren von Zwischenspeicherungen. EnableCaching, CacheDuration, CacheExpirationPolicy und CacheKeyDependency.

## <a name="enablecaching"></a>Enablecaching

EnableCaching ist eine boolesche Eigenschaft, die bestimmt, ob die Zwischenspeicherung für das Datenquellensteuerelement aktiviert ist.

## <a name="cacheduration-property"></a>CacheDuration-Eigenschaft

Die CacheDuration-Eigenschaft legt die Anzahl der Sekunden fest, in denen der Cache gültig bleibt. Wenn Sie diese Eigenschaft auf **0** setzen, bleibt der Cache gültig, bis explizit ungültig wird.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy-Eigenschaft

Die CacheExpirationPolicy-Eigenschaft kann entweder auf **Absolute** oder **Sliding**festgelegt werden. Wenn Sie es auf Absolut festlegen, bedeutet die maximale Zeit, die die Daten zwischengespeichert werden, die Anzahl der Sekunden, die von der CacheDuration-Eigenschaft angegeben werden. Wenn Sie es auf Schieben setzen, wird die Ablaufzeit zurückgesetzt, wenn jeder Vorgang ausgeführt wird.

## <a name="cachekeydependency-property"></a>CacheKeyDependency-Eigenschaft

Wenn ein Zeichenfolgenwert für die CacheKeyDependency-Eigenschaft angegeben wird, richtet ASP.NET eine neue Cacheabhängigkeit basierend auf dieser Zeichenfolge ein. Auf diese Weise können Sie den Cache explizit ungültig machen, indem Sie einfach die CacheKeyDependency ändern oder entfernen.

**Wichtig:** Wenn der Identitätswechsel aktiviert ist und der Zugriff auf die Datenquelle und/oder den Inhalt von Daten auf der Clientidentität basiert, wird empfohlen, das Zwischenspeichern zu deaktivieren, indem EnableCaching auf False festgelegt wird. Wenn das Zwischenspeichern in diesem Szenario aktiviert ist und ein anderer Benutzer als der Benutzer, der die Daten ursprünglich angefordert hat, eine Anforderung ausstellt, wird die Autorisierung für die Datenquelle nicht erzwungen. Die Daten werden einfach aus dem Cache bereitgestellt.

## <a name="the-sqldatasource-control"></a>Das SqlDataSource-Steuerelement

Das SqlDataSource-Steuerelement ermöglicht einem Entwickler den Zugriff auf Daten, die in einer relationalen Datenbank gespeichert sind, die ADO.NET unterstützt. Sie kann den System.Data.SqlClient-Anbieter verwenden, um auf eine SQL Server-Datenbank, den System.Data.OleDb-Anbieter, den System.Data.Odbc-Anbieter oder den System.Data.OracleClient-Anbieter zuzugreifen, um auf Oracle zuzugreifen. Daher wird die SqlDataSource sicherlich nicht nur für den Zugriff auf Daten in einer SQL Server-Datenbank verwendet.

Um die SqlDataSource verwenden zu können, geben Sie einfach einen Wert für die ConnectionString-Eigenschaft an und geben einen SQL-Befehl oder eine gespeicherte Prozedur an. Das SqlDataSource-Steuerelement übernimmt die Arbeit mit der zugrunde liegenden ADO.NET Architektur. Es öffnet die Verbindung, fragt die Datenquelle ab oder führt die gespeicherte Prozedur aus, gibt die Daten zurück und schließt dann die Verbindung für Sie.

> [!NOTE]
> Da die DataSourceControl-Klasse die Verbindung automatisch für Sie schließt, sollte sie die Anzahl der Kundenaufrufe reduzieren, die durch undichte Datenbankverbindungen generiert werden.

Der Codeausschnitt unten bindet ein DropDownList-Steuerelement an ein SqlDataSource-Steuerelement mithilfe der Verbindungszeichenfolge, die wie oben gezeigt in der Konfigurationsdatei gespeichert ist.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Wie oben dargestellt, gibt die DataSourceMode-Eigenschaft der SqlDataSource den Modus für die Datenquelle an. Im obigen Beispiel ist DataSourceMode auf DataReader festgelegt. In diesem Fall gibt die SqlDataSource ein IDataReader-Objekt mit einem vorwärts- und schreibgeschützten Cursor zurück. Der angegebene Objekttyp, der zurückgegeben wird, wird vom verwendeten Anbieter gesteuert. In diesem Fall verwende ich den System.Data.SqlClient-Anbieter, wie im Abschnitt &lt;connectionStrings&gt; der Datei web.config angegeben. Daher ist das zurückgegebene Objekt vom Typ SqlDataReader. Durch Angabe eines DataSourceMode-Werts von DataSet können die Daten in einem DataSet auf dem Server gespeichert werden. In diesem Modus können Sie Funktionen wie Sortieren, Paging usw. hinzufügen. Wenn ich die SqlDataSource mit Daten an ein GridView-Steuerelement gebunden hätte, hätte ich den DataSet-Modus gewählt. Im Fall einer DropDownList ist der DataReader-Modus jedoch die richtige Wahl.

> [!NOTE]
> Beim Zwischenspeichern einer SqlDataSource oder accessDataSource muss die DataSourceMode-Eigenschaft auf DataSet festgelegt werden. Eine Ausnahme tritt auf, wenn Sie das Zwischenspeichern mit einem DataSourceMode von DataReader aktivieren.

## <a name="sqldatasource-properties"></a>SqlDataSource-Eigenschaften

Im Folgenden sind einige der Eigenschaften des SqlDataSource-Steuerelements zu finden.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Ein boolescher Wert, der angibt, ob ein select-Befehl abgebrochen wird, wenn einer der Parameter null ist. Der Standardwert lautet „true“.

### <a name="conflictdetection"></a>Conflictdetection

In einer Situation, in der mehrere Benutzer eine Datenquelle gleichzeitig aktualisieren, bestimmt die ConflictDetection-Eigenschaft das Verhalten des SqlDataSource-Steuerelements. Diese Eigenschaft wird als einer der Werte der ConflictOptions-Enumeration ausgewertet. Diese Werte sind **CompareAllValues** und **OverwriteChanges**. Wenn auf OverwriteChanges festgelegt, überschreibt die letzte Person, die Daten in die Datenquelle schreibt, alle vorherigen Änderungen. Wenn die ConflictDetection-Eigenschaft jedoch auf CompareAllValues festgelegt ist, werden Parameter für die vom SelectCommand zurückgegebenen Spalten erstellt, und Parameter werden auch erstellt, um die ursprünglichen Werte in jeder dieser Spalten zu enthalten, sodass die SqlDataSource bestimmen kann, ob sich die Werte seit der Ausführung des SelectCommand geändert haben.

### <a name="deletecommand"></a>Deletecommand

Legt die SQL-Zeichenfolge fest oder ruft sie ab, die beim Löschen von Zeilen aus der Datenbank verwendet wird. Dabei kann es sich entweder um eine SQL-Abfrage oder um einen gespeicherten Prozedurnamen handeln.

### <a name="deletecommandtype"></a>DeleteCommandType

Legt den Typ des Löschbefehls fest oder ruft ihn ab, entweder eine SQL-Abfrage (Text) oder eine gespeicherte Prozedur (StoredProcedure).

### <a name="deleteparameters"></a>Deleteparameters

Gibt die Parameter zurück, die vom DeleteCommand des SqlDataSourceView-Objekts verwendet werden, das dem SqlDataSource-Steuerelement zugeordnet ist.

### <a name="oldvaluesparameterformatstring"></a>Oldvaluesparameterformatstring

Diese Eigenschaft wird verwendet, um das Format der ursprünglichen Wertparameter in Fällen anzugeben, in denen die ConflictDetection-Eigenschaft auf CompareAllValues festgelegt ist. Der Standardwert bedeutet, {0} dass die ursprünglichen Wertparameter denselben Namen wie der ursprüngliche Parameter annehmen. Mit anderen Worten, wenn der Feldname EmployeeID ist, wäre der ursprüngliche Wertparameter @EmployeeID.

### <a name="selectcommand"></a>SelectCommand

Legt die SQL-Zeichenfolge fest oder ruft sie ab, die zum Abrufen von Daten aus der Datenbank verwendet wird. Dabei kann es sich entweder um eine SQL-Abfrage oder um einen gespeicherten Prozedurnamen handeln.

### <a name="selectcommandtype"></a>Selectcommandtype

Legt den Typ des Select-Befehls fest oder ruft ihn ab, entweder eine SQL-Abfrage (Text) oder eine gespeicherte Prozedur (StoredProcedure).

### <a name="selectparameters"></a>Selectparameters

Gibt die Parameter zurück, die vom SelectCommand des SqlDataSourceView-Objekts verwendet werden, das dem SqlDataSource-Steuerelement zugeordnet ist.

### <a name="sortparametername"></a>Sortparametername

Ruft den Namen eines gespeicherten Prozedurparameters ab oder legt ihn fest, der beim Sortieren von Daten verwendet wird, die vom Datenquellensteuerelement abgerufen werden. Gültig nur, wenn SelectCommandType auf StoredProcedure festgelegt ist.

### <a name="sqlcachedependency"></a>Sqlcachedependency

Eine durch Semikolons getrennte Zeichenfolge, die die Datenbanken und Tabellen angibt, die in einer SQL Server-Cacheabhängigkeit verwendet werden. (SQL-Cacheabhängigkeiten werden in einem späteren Modul erläutert.)

### <a name="updatecommand"></a>Updatecommand

Legt die SQL-Zeichenfolge fest oder ruft sie ab, die beim Aktualisieren von Daten in der Datenbank verwendet wird. Dabei kann es sich entweder um eine SQL-Abfrage oder um einen gespeicherten Prozedurnamen handeln.

### <a name="updatecommandtype"></a>UpdateCommandType

Legt den Typ des Aktualisierungsbefehls fest oder ruft ihn ab, entweder eine SQL-Abfrage (Text) oder eine gespeicherte Prozedur (StoredProcedure).

### <a name="updateparameters"></a>Updateparameters

Gibt die Parameter zurück, die vom UpdateCommand des SqlDataSourceView-Objekts verwendet werden, das dem SqlDataSource-Steuerelement zugeordnet ist.

## <a name="the-accessdatasource-control"></a>Das AccessDataSource-Steuerelement

Das AccessDataSource-Steuerelement leitet sich von der SqlDataSource-Klasse ab und wird zum Binden von Daten an eine Microsoft Access-Datenbank verwendet. Die ConnectionString-Eigenschaft für das AccessDataSource-Steuerelement ist eine schreibgeschützte Eigenschaft. Anstatt die ConnectionString-Eigenschaft zu verwenden, wird die DataFile-Eigenschaft verwendet, um auf die Zugriffsdatenbank zu verweisen, wie unten gezeigt.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

Die AccessDataSource legt immer den Providernamen der Basis SqlDataSource auf System.Data.OleDb fest und stellt über den OLE DB-Anbieter Microsoft.Jet.OLEDB.4.0 eine Verbindung mit der Datenbank her. Sie können das AccessDataSource-Steuerelement nicht verwenden, um eine Verbindung mit einer kennwortgeschützten Access-Datenbank herzustellen. Wenn Sie eine Verbindung zu einer kennwortgeschützten Datenbank herstellen müssen, sollten Sie das SqlDataSource-Steuerelement verwenden.

> [!NOTE]
> Die in der Website gespeicherten Zugriffsdatenbanken\_sollten im Verzeichnis App-Daten abgelegt werden. ASP.NET lässt das Durchsuchen von Dateien in diesem Verzeichnis nicht zu. Sie müssen dem Konto Lese- und Schreibberechtigungen\_für das App-Datenverzeichnis erteilen, wenn Sie Access-Datenbanken verwenden.

## <a name="the-xmldatasource-control"></a>Das XmlDataSource-Steuerelement

Die XmlDataSource wird verwendet, um XML-Daten an datengebundene Steuerelemente zu binden. Sie können mithilfe der DataFile-Eigenschaft an eine XML-Datei oder mithilfe der Data-Eigenschaft eine XML-Zeichenfolge binden. Die XmlDataSource macht XML-Attribute als bindbare Felder verfügbar. In Fällen, in denen Sie an Werte binden müssen, die nicht als Attribute dargestellt werden, müssen Sie eine XSL-Transformation verwenden. Sie können auch XPath-Ausdrücke verwenden, um XML-Daten zu filtern.

Betrachten Sie die folgende XML-Datei:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

Beachten Sie, dass die XmlDataSource eine XPath-Eigenschaft von *People/Person* verwendet, um nur nach den &lt;Personenknoten&gt; zu filtern. Die DropDownList bindet dann mithilfe der DataTextField-Eigenschaft an das LastName-Attribut.

Während das XmlDataSource-Steuerelement hauptsächlich zum Binden von Daten an schreibgeschützte XML-Daten verwendet wird, ist es möglich, die XML-Datendatei zu bearbeiten. Beachten Sie, dass in solchen Fällen das automatische Einfügen, Aktualisieren und Löschen von Informationen in der XML-Datei nicht automatisch erfolgt, wie dies bei anderen Datenquellensteuerelementen der Fall ist. Stattdessen müssen Sie Code schreiben, um die Daten manuell mit den folgenden Methoden des XmlDataSource-Steuerelements zu bearbeiten.

### <a name="getxmldocument"></a>GetXmlDocument

Ruft ein XmlDocument-Objekt ab, das den xml-Code enthält, der von der XmlDataSource abgerufen wurde.

### <a name="save"></a>Speichern

Speichert das in-Memory-XmlDocument wieder in der Datenquelle.

Es ist wichtig zu erkennen, dass die Save-Methode nur funktioniert, wenn die folgenden beiden Bedingungen erfüllt sind:

1. Die XmlDataSource verwendet die DataFile-Eigenschaft, um eine Bindung an eine XML-Datei anstelle der Data-Eigenschaft zum Binden an in-Memory-XML-Daten zu binden.
2. Über die Transform- oder TransformFile-Eigenschaft wird keine Transformation angegeben.

Beachten Sie auch, dass die Save-Methode unerwartete Ergebnisse liefern kann, wenn sie von mehreren Benutzern gleichzeitig aufgerufen wird.

## <a name="the-objectdatasource-control"></a>Das ObjectDataSource-Steuerelement

Die Datenquellensteuerelemente, die wir bis zu diesem Zeitpunkt abgedeckt haben, sind eine ausgezeichnete Wahl für zweistufige Anwendungen, bei denen die Datenquellensteuerung direkt mit dem Datenspeicher kommuniziert. Viele reale Anwendungen sind jedoch mehrstufige Anwendungen, bei denen ein Datenquellensteuerelement möglicherweise mit einem Geschäftsobjekt kommunizieren muss, das wiederum mit der Datenschicht kommuniziert. In diesen Situationen füllt die ObjectDataSource die Rechnung gut aus. ObjectDataSource arbeitet in Verbindung mit einem Quellobjekt. Das ObjectDataSource-Steuerelement erstellt eine Instanz des Quellobjekts, ruft die angegebene Methode auf und entsorgt die Objektinstanz alle innerhalb des Bereichs einer einzelnen Anforderung, wenn das Objekt über Instanzmethoden anstelle statischer Methoden verfügt (in Visual Basic freigegeben). Daher muss Ihr Objekt zustandslos sein. Das heißt, Ihr Objekt sollte alle erforderlichen Ressourcen innerhalb des Zeitraums einer einzelnen Anforderung erfassen und freigeben. Sie können steuern, wie das Quellobjekt erstellt wird, indem Sie das ObjectCreating-Ereignis des ObjectDataSource-Steuerelements verarbeiten. Sie können eine Instanz des Quellobjekts erstellen und dann die ObjectInstance-Eigenschaft der ObjectDataSourceEventArgs-Klasse auf diese Instanz festlegen. Das ObjectDataSource-Steuerelement verwendet die Instanz, die im ObjectCreating-Ereignis erstellt wird, anstatt eine eigene Instanz zu erstellen.

Wenn das Quellobjekt für ein ObjectDataSource-Steuerelement öffentliche statische Methoden (in Visual Basic freigegeben) verfügbar macht, die aufgerufen werden können, um Daten abzurufen und zu ändern, ruft ein ObjectDataSource-Steuerelement diese Methoden direkt auf. Wenn ein ObjectDataSource-Steuerelement eine Instanz des Quellobjekts erstellen muss, um Methodenaufrufe zu erstellen, muss das Objekt einen öffentlichen Konstruktor enthalten, der keine Parameter annimmt. Das ObjectDataSource-Steuerelement ruft diesen Konstruktor auf, wenn eine neue Instanz des Quellobjekts erstellt wird.

Wenn das Quellobjekt keinen öffentlichen Konstruktor ohne Parameter enthält, können Sie eine Instanz des Quellobjekts erstellen, das vom ObjectDataSource-Steuerelement im ObjectCreating-Ereignis verwendet wird.

## <a name="specifying-object-methods"></a>Angeben von Objektmethoden

Das Quellobjekt für ein ObjectDataSource-Steuerelement kann eine beliebige Anzahl von Methoden enthalten, die zum Auswählen, Einfügen, Aktualisieren oder Löschen von Daten verwendet werden. Diese Methoden werden vom ObjectDataSource-Steuerelement basierend auf dem Namen der Methode aufgerufen, der mithilfe der SelectMethod-, InsertMethod-, UpdateMethod- oder DeleteMethod-Eigenschaft des ObjectDataSource-Steuerelements identifiziert wird. Das Quellobjekt kann auch eine optionale SelectCount-Methode enthalten, die vom ObjectDataSource-Steuerelement mithilfe der SelectCountMethod-Eigenschaft identifiziert wird, die die Anzahl der Gesamtanzahl von Objekten in der Datenquelle zurückgibt. Das ObjectDataSource-Steuerelement ruft die SelectCount-Methode auf, nachdem eine Select-Methode aufgerufen wurde, um die Gesamtzahl der Datensätze an der Datenquelle abzurufen, die beim Paging verwendet werden sollen.

## <a name="lab-using-data-source-controls"></a>Lab mit Datenquellensteuerelementen

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Übung 1 - Anzeigen von Daten mit dem SqlDataSource-Steuerelement

In der folgenden Übung wird das SqlDataSource-Steuerelement zum Herstellen einer Verbindung mit der Northwind-Datenbank verwendet. Es wird davon ausgegangen, dass Sie Zugriff auf die Northwind-Datenbank auf einer SQL Server 2000-Instanz haben.

1. Erstellen Sie eine neue ASP.NET-Website.
2. Fügen Sie eine neue Datei web.config hinzu.

    1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und klicken Sie auf Neues Element hinzufügen.
    2. Wählen Sie Webkonfigurationsdatei aus der Liste der Vorlagen aus, und klicken Sie auf Hinzufügen.
3. Bearbeiten &lt;Sie&gt; den Abschnitt connectionStrings wie folgt: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Wechseln Sie zur Codeansicht, und fügen Sie dem &lt;asp:SqlDataSource-Steuerelement&gt; wie folgt ein ConnectionString-Attribut und ein SelectCommand-Attribut hinzu: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Fügen Sie in der Entwurfsansicht ein neues GridView-Steuerelement hinzu.
6. Wählen Sie im Dropdowndown "Datenquelle auswählen" im Menü GridView-Aufgaben sqlDataSource1 aus.
7. Klicken Sie mit der rechten Maustaste auf Default.aspx und wählen Sie im Menü Ansicht im Browser aus. Klicken Sie auf Ja, wenn Sie zum Speichern aufgefordert werden.
8. Die GridView zeigt die Daten aus der Tabelle Produkte an.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Übung 2 - Bearbeiten von Daten mit dem SqlDataSource-Steuerelement

In der folgenden Übung wird veranschaulicht, wie Daten ein DropDownList-Steuerelement mithilfe der deklarativen Syntax binden und die im DropDownList-Steuerelement dargestellten Daten bearbeiten können.

1. Löschen Sie in der Entwurfsansicht das GridView-Steuerelement aus Default.aspx. 

    **Wichtig**: Lassen Sie das SqlDataSource-Steuerelement auf der Seite.
2. Fügen Sie ein DropDownList-Steuerelement zu Default.aspx hinzu.
3. Wechseln Sie zur Quellansicht.
4. Fügen Sie dem &lt;asp:DropDownList-Steuerelement&gt; folgendes Attribut dataSourceId, DataTextField und DataValueField hinzu: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Speichern Sie Default.aspx, und zeigen Sie es im Browser an. Beachten Sie, dass die DropDownList alle Produkte aus der Northwind-Datenbank enthält.
6. Schließen Sie den Browser.
7. Fügen Sie in der Quellansicht von Default.aspx ein neues TextBox-Steuerelement unter dem DropDownList-Steuerelement hinzu. Ändern Sie die ID-Eigenschaft der TextBox in txtProductName.
8. Fügen Sie unter dem TextBox-Steuerelement ein neues Schaltflächensteuerelement hinzu. Ändern Sie die ID-Eigenschaft der Schaltfläche in btnUpdate und die Text-Eigenschaft in Aktualisieren des **Produktnamens**.
9. Fügen Sie in der Quellansicht von Default.aspx dem SqlDataSource-Tag wie folgt eine UpdateCommand-Eigenschaft und zwei neue UpdateParameters hinzu: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Beachten Sie, dass in diesem Code zwei Aktualisierungsparameter (ProductName und ProductID) hinzugefügt wurden. Diese Parameter werden der Text-Eigenschaft der txtProductName TextBox und der SelectedValue-Eigenschaft der dropDownList ddlProducts zugeordnet.
10. Wechseln Sie zur Entwurfsansicht, und doppelklicken Sie auf das Schaltflächensteuerelement, um einen Ereignishandler hinzuzufügen.
11. Fügen Sie dem btnUpdate\_Click-Code den folgenden Code hinzu: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Klicken Sie mit der rechten Maustaste auf Default.aspx, und wählen Sie es im Browser anzeigen. Klicken Sie auf Ja, wenn Sie aufgefordert werden, alle Änderungen zu speichern.
13. ASP.NET 2.0-Partialklassen ermöglichen die Kompilierung zur Laufzeit. Es ist nicht erforderlich, eine Anwendung zu erstellen, damit Codeänderungen wirksam werden.
14. Wählen Sie ein Produkt aus der DropDownList aus.
15. Geben Sie einen neuen Namen für das ausgewählte Produkt in die TextBox ein, und klicken Sie dann auf die Schaltfläche Aktualisieren.
16. Der Produktname wird in der Datenbank aktualisiert.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Übung 3 Verwenden des ObjectDataSource-Steuerelements

In dieser Übung wird veranschaulicht, wie sie das ObjectDataSource-Steuerelement und ein Quellobjekt für die Interaktion mit der Northwind-Datenbank verwenden.

1. Klicken Sie mit der rechten Maustaste auf das Projekt im Projektmappen-Explorer und klicken Sie auf Neues Element hinzufügen.
2. Wählen Sie Webformular in der Vorlagenliste aus. Ändern Sie den Namen in object.aspx, und klicken Sie auf Hinzufügen.
3. Klicken Sie mit der rechten Maustaste auf das Projekt im Projektmappen-Explorer und klicken Sie auf Neues Element hinzufügen.
4. Wählen Sie Klasse in der Vorlagenliste aus. Ändern Sie den Namen der Klasse in NorthwindData.cs, und klicken Sie auf Hinzufügen.
5. Klicken Sie auf Ja, wenn\_Sie aufgefordert werden, die Klasse zum App-Codeordner hinzuzufügen.
6. Fügen Sie der NorthwindData.cs Datei den folgenden Code hinzu: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Fügen Sie der Quellansicht von object.aspx den folgenden Code hinzu: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Speichern Sie alle Dateien, und durchsuchen Sie object.aspx.
9. Interagieren Sie mit der Benutzeroberfläche, indem Sie Details anzeigen, Mitarbeiter bearbeiten, Mitarbeiter hinzufügen und Mitarbeiter löschen.
