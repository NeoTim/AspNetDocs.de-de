---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: Unterstützende odata-Abfrage Optionen in ASP.net-Web-API 2-ASP.NET 4. x
author: MikeWasson
description: Übersicht mit Codebeispielen zeigt die unterstützenden odata-Abfrage Optionen in ASP.net-Web-API 2 für ASP.NET 4. x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188621"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>Unterstützen von odata-Abfrage Optionen in ASP.net-Web-API 2

von [Mike Wasson](https://github.com/MikeWasson)

In dieser Übersicht mit Codebeispielen werden die unterstützenden odata-Abfrage Optionen in ASP.net-Web-API 2 für ASP.NET 4. x veranschaulicht. 

Odata definiert Parameter, die verwendet werden können, um eine odata-Abfrage zu ändern. Der Client sendet diese Parameter in der Abfrage Zeichenfolge des Anforderungs-URI. Zum Sortieren der Ergebnisse verwendet ein Client z. b. den $OrderBy-Parameter:

`http://localhost/Products?$orderby=Name`

Die odata-Spezifikation ruft diese Parameter *Abfrage Optionen*auf. Sie können odata-Abfrage Optionen für alle Web-API-Controller in Ihrem Projekt aktivieren, &#8212; der Controller kein odata-Endpunkt sein muss. Dies bietet Ihnen eine bequeme Möglichkeit, Features wie das Filtern und sortieren zu jeder Web-API-Anwendung hinzuzufügen.

Lesen Sie vor dem Aktivieren der Abfrage Optionen das Thema [odata-Sicherheits Leit Faden](odata-security-guidance.md).

- [Aktivieren von odata-Abfrage Optionen](#enable)
- [Beispielabfragen](#examples)
- [Server gesteuerte Auslagerung](#server-paging)
- [Einschränken der Abfrage Optionen](#limiting_query_options)
- [Direktes Aufrufen von Abfrage Optionen](#ODataQueryOptions)
- [Abfrage Validierung](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>Aktivieren von odata-Abfrage Optionen

Die Web-API unterstützt die folgenden odata-Abfrage Optionen:

| Option | BESCHREIBUNG |
| --- | --- |
| $expand | Erweitert Verwandte Entitäten Inline. |
| $filter | Filtert die Ergebnisse basierend auf einer booleschen Bedingung. |
| $inlinecount | Weist den Server an, die Gesamtanzahl der übereinstimmenden Entitäten in der Antwort einzuschließen. (Nützlich für Serverseitiges Paging.) |
| $orderby | Sortiert die Ergebnisse. |
| $select | Wählt aus, welche Eigenschaften in die Antwort eingeschlossen werden sollen. |
| $skip | Überspringt die ersten n Ergebnisse. |
| $top | Gibt nur die ersten n der Ergebnisse zurück. |

Um odata-Abfrage Optionen zu verwenden, müssen Sie diese explizit aktivieren. Sie können Sie für die gesamte Anwendung global aktivieren oder für bestimmte Controller oder bestimmte Aktionen aktivieren.

Um odata-Abfrage Optionen global zu aktivieren, müssen Sie **enablequerysupport** für die **httpconfiguration** -Klasse beim Start aufzurufen:

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

Die **enablequerysupport** -Methode ermöglicht globale Abfrage Optionen für jede Controller Aktion, die einen **iquerable** -Typ zurückgibt. Wenn Sie die Abfrage Optionen für die gesamte Anwendung nicht aktivieren möchten, können Sie Sie für bestimmte Controller Aktionen aktivieren, indem Sie der Aktionsmethode das **[querable]** -Attribut hinzufügen.

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>Beispielabfragen

In diesem Abschnitt werden die Typen von Abfragen gezeigt, die mithilfe der odata-Abfrage Optionen möglich sind. Spezifische Details zu den Abfrage Optionen finden Sie in der odata-Dokumentation unter [www.odata.org](http://www.odata.org/).

Informationen zu $Expand und $SELECT finden Sie unter [Verwenden von $SELECT, $Expand und $Value in ASP.net-Web-API odata](using-select-expand-and-value.md).

**Client gesteuerte Auslagerung**

Bei großen Entitätenmengen kann es vorkommen, dass der Client die Anzahl der Ergebnisse einschränkt. Ein Client kann z. b. 10 Einträge gleichzeitig mit "Next"-Links anzeigen, um die nächste Seite mit Ergebnissen zu erhalten. Zu diesem Zweck verwendet der Client die Optionen $Top und $Skip.

`http://localhost/Products?$top=10&$skip=20`

Die $Top-Option gibt die maximale Anzahl von Einträgen an, die zurückgegeben werden, und die $Skip-Option gibt die Anzahl der zu über springenden Einträge an. Im vorherigen Beispiel werden die Einträge 21 bis 30 abgerufen.

**Filterung**

Die Option $Filter ermöglicht einem Client das Filtern der Ergebnisse durch Anwenden eines booleschen Ausdrucks. Die Filter Ausdrücke sind sehr leistungsstark. Dazu zählen logische und arithmetische Operatoren, Zeichen folgen Funktionen und Datumsfunktionen.

| Gibt alle Produkte zurück, deren Kategorie "Toys" entspricht. | `http://localhost/Products?$filter=Category` EQ ' Toys ' |
| --- | --- |
| Gibt alle Produkte zurück, deren Preis kleiner als 10 ist. | `http://localhost/Products?$filter=Price` lt 10 |
| Logische Operatoren: gibt alle Produkte zurück, bei denen Price >= 5 und Price <= 15 ist. | `http://localhost/Products?$filter=Price` ge 5 und Preis Le 15 |
| Zeichen folgen Funktionen: gibt alle Produkte mit "zz" im Namen zurück. | `http://localhost/Products?$filter=substringof('zz',Name)` |
| Datumsfunktionen: gibt alle Produkte mit ReleaseDate nach 2005 zurück. | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**Sortieren**

Um die Ergebnisse zu sortieren, verwenden Sie den $OrderBy Filter.

| Nach Preis sortieren. | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| Sortieren Sie nach Preis in absteigender Reihenfolge (höchste zum niedrigsten). | `http://localhost/Products?$orderby=Price desc` |
| Sortieren Sie nach Kategorie, und sortieren Sie Sie nach Preis in absteigender Reihenfolge innerhalb von Kategorien. | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>Server gesteuerte Auslagerung

Wenn Ihre Datenbank Millionen von Datensätzen enthält, möchten Sie Sie nicht alle in einer Nutzlast senden. Um dies zu verhindern, kann der Server die Anzahl der gesendeten Einträge in einer einzelnen Antwort einschränken. Legen Sie zum **Aktivieren der Server** Auslagerung die **PageSize** -Eigenschaft im abfragbaren Attribut fest. Der Wert ist die maximale Anzahl von Einträgen, die zurückgegeben werden.

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

Wenn Ihr Controller das odata-Format zurückgibt, enthält der Antworttext einen Link zur nächsten Seite der Daten:

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

Der Client kann den Link zum Abrufen der nächsten Seite verwenden. Wenn Sie die Gesamtanzahl der Einträge im Resultset ermitteln möchten, kann der Client die $inlinecount Query-Option mit dem Wert "AllPages" festlegen.

`http://localhost/Products?$inlinecount=allpages`

Der Wert "AllPages" weist den Server an, die Gesamtanzahl in die Antwort einzubeziehen:

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> Next-Page-Links und Inline Anzahl erfordern beide das odata-Format. Der Grund hierfür ist, dass odata spezielle Felder im Antworttext definiert, um den Link und die Anzahl zu speichern.

Bei nicht-odata-Formaten ist es weiterhin möglich, die Links der nächsten Seite und die Inline Anzahl zu unterstützen, indem die Abfrageergebnisse in ein **PageResult &lt; T &gt; ** -Objekt eingebunden werden. Es ist jedoch etwas mehr Code erforderlich. Beispiel:

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

Hier ist ein Beispiel für eine JSON-Antwort:

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>Einschränken der Abfrage Optionen

Die Abfrage Optionen sorgen für eine hohe Kontrolle über die Abfrage, die auf dem Server ausgeführt wird. In einigen Fällen möchten Sie möglicherweise die verfügbaren Optionen aus Sicherheits-oder Leistungsgründen einschränken. Das **[quervable]** -Attribut verfügt über einige integrierte Eigenschaften für diesen. Hier einige Beispiele.

Nur $Skip und $Top zulassen, um das Paging zu unterstützen, und nichts anderes:

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

Die Sortierung wird nur nach bestimmten Eigenschaften ermöglicht, um das Sortieren von Eigenschaften zu verhindern, die nicht in der Datenbank indiziert werden:

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

Ermöglicht die logische Funktion "EQ", aber keine anderen logischen Funktionen:

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

Arithmetische Operatoren dürfen nicht zugelassen werden:

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

Sie können Optionen Global einschränken, indem Sie eine **queryableattribute** -Instanz erstellen und Sie an die **enablequerysupport** -Funktion übergeben:

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>Direktes Aufrufen von Abfrage Optionen

Anstatt das **[quervable]** -Attribut zu verwenden, können Sie die Abfrage Optionen direkt in Ihrem Controller aufrufen. Fügen Sie zu diesem Zweck der Controller Methode einen **odataqueryoptions** -Parameter hinzu. In diesem Fall benötigen Sie das Attribut **[quervable]** nicht.

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Die Web-API füllt **odataqueryoptions** aus der URI-Abfrage Zeichenfolge auf. Übergeben Sie zum Anwenden der Abfrage ein **iquerable** -Element an die **ApplyTo** -Methode. Die-Methode gibt eine andere **iquerable**zurück.

Wenn Sie für erweiterte Szenarien keinen **iquerable** -Abfrage Anbieter haben, können Sie **odataqueryoptions** untersuchen und die Abfrage Optionen in eine andere Form übersetzen. (Informationen hierzu finden Sie beispielsweise im Blogbeitrag zum über [setzen von odata-Abfragen in HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), der auch ein [Beispiel](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)enthält.

<a id="query-validation"></a>
## <a name="query-validation"></a>Abfrage Validierung

Das **[quervable]** -Attribut überprüft die Abfrage vor der Ausführung. Der Validierungs Schritt wird in der **queryableattribute. validatequery** -Methode ausgeführt. Sie können auch den Validierungsprozess anpassen.

Siehe auch [odata-Sicherheits Leit Faden](odata-security-guidance.md).

Überschreiben Sie zunächst eine der Prüfungs-Klassen, die im **Web. http. odata. Query. Validators** -Namespace definiert sind. Die folgende Prüfungs-Klasse deaktiviert z. b. die Option "DESC" für die $OrderBy-Option.

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

Unterklasse das **[quervable]** -Attribut, um die **validatequery** -Methode zu überschreiben.

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

Legen Sie dann das benutzerdefinierte Attribut entweder global oder pro Controller fest:

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

Wenn Sie **odataqueryoptions** direkt verwenden, legen Sie das Validierungs Steuerelement für die Optionen fest:

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
