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
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188621"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="26602-103">Unterstützen von odata-Abfrage Optionen in ASP.net-Web-API 2</span><span class="sxs-lookup"><span data-stu-id="26602-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="26602-104">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="26602-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="26602-105">In dieser Übersicht mit Codebeispielen werden die unterstützenden odata-Abfrage Optionen in ASP.net-Web-API 2 für ASP.NET 4. x veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="26602-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="26602-106">Odata definiert Parameter, die verwendet werden können, um eine odata-Abfrage zu ändern.</span><span class="sxs-lookup"><span data-stu-id="26602-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="26602-107">Der Client sendet diese Parameter in der Abfrage Zeichenfolge des Anforderungs-URI.</span><span class="sxs-lookup"><span data-stu-id="26602-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="26602-108">Zum Sortieren der Ergebnisse verwendet ein Client z. b. den $OrderBy-Parameter:</span><span class="sxs-lookup"><span data-stu-id="26602-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="26602-109">Die odata-Spezifikation ruft diese Parameter *Abfrage Optionen*auf.</span><span class="sxs-lookup"><span data-stu-id="26602-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="26602-110">Sie können odata-Abfrage Optionen für alle Web-API-Controller in Ihrem Projekt aktivieren, &#8212; der Controller kein odata-Endpunkt sein muss.</span><span class="sxs-lookup"><span data-stu-id="26602-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="26602-111">Dies bietet Ihnen eine bequeme Möglichkeit, Features wie das Filtern und sortieren zu jeder Web-API-Anwendung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="26602-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="26602-112">Lesen Sie vor dem Aktivieren der Abfrage Optionen das Thema [odata-Sicherheits Leit Faden](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="26602-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="26602-113">Aktivieren von odata-Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="26602-114">Beispielabfragen</span><span class="sxs-lookup"><span data-stu-id="26602-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="26602-115">Server gesteuerte Auslagerung</span><span class="sxs-lookup"><span data-stu-id="26602-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="26602-116">Einschränken der Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="26602-117">Direktes Aufrufen von Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="26602-118">Abfrage Validierung</span><span class="sxs-lookup"><span data-stu-id="26602-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="26602-119">Aktivieren von odata-Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-119">Enabling OData Query Options</span></span>

<span data-ttu-id="26602-120">Die Web-API unterstützt die folgenden odata-Abfrage Optionen:</span><span class="sxs-lookup"><span data-stu-id="26602-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="26602-121">Option</span><span class="sxs-lookup"><span data-stu-id="26602-121">Option</span></span> | <span data-ttu-id="26602-122">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="26602-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26602-123">$expand</span><span class="sxs-lookup"><span data-stu-id="26602-123">$expand</span></span> | <span data-ttu-id="26602-124">Erweitert Verwandte Entitäten Inline.</span><span class="sxs-lookup"><span data-stu-id="26602-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="26602-125">$filter</span><span class="sxs-lookup"><span data-stu-id="26602-125">$filter</span></span> | <span data-ttu-id="26602-126">Filtert die Ergebnisse basierend auf einer booleschen Bedingung.</span><span class="sxs-lookup"><span data-stu-id="26602-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="26602-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="26602-127">$inlinecount</span></span> | <span data-ttu-id="26602-128">Weist den Server an, die Gesamtanzahl der übereinstimmenden Entitäten in der Antwort einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="26602-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="26602-129">(Nützlich für Serverseitiges Paging.)</span><span class="sxs-lookup"><span data-stu-id="26602-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="26602-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="26602-130">$orderby</span></span> | <span data-ttu-id="26602-131">Sortiert die Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="26602-131">Sorts the results.</span></span> |
| <span data-ttu-id="26602-132">$select</span><span class="sxs-lookup"><span data-stu-id="26602-132">$select</span></span> | <span data-ttu-id="26602-133">Wählt aus, welche Eigenschaften in die Antwort eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="26602-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="26602-134">$skip</span><span class="sxs-lookup"><span data-stu-id="26602-134">$skip</span></span> | <span data-ttu-id="26602-135">Überspringt die ersten n Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="26602-135">Skips the first n results.</span></span> |
| <span data-ttu-id="26602-136">$top</span><span class="sxs-lookup"><span data-stu-id="26602-136">$top</span></span> | <span data-ttu-id="26602-137">Gibt nur die ersten n der Ergebnisse zurück.</span><span class="sxs-lookup"><span data-stu-id="26602-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="26602-138">Um odata-Abfrage Optionen zu verwenden, müssen Sie diese explizit aktivieren.</span><span class="sxs-lookup"><span data-stu-id="26602-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="26602-139">Sie können Sie für die gesamte Anwendung global aktivieren oder für bestimmte Controller oder bestimmte Aktionen aktivieren.</span><span class="sxs-lookup"><span data-stu-id="26602-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="26602-140">Um odata-Abfrage Optionen global zu aktivieren, müssen Sie **enablequerysupport** für die **httpconfiguration** -Klasse beim Start aufzurufen:</span><span class="sxs-lookup"><span data-stu-id="26602-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="26602-141">Die **enablequerysupport** -Methode ermöglicht globale Abfrage Optionen für jede Controller Aktion, die einen **iquerable** -Typ zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="26602-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="26602-142">Wenn Sie die Abfrage Optionen für die gesamte Anwendung nicht aktivieren möchten, können Sie Sie für bestimmte Controller Aktionen aktivieren, indem Sie der Aktionsmethode das **[querable]** -Attribut hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="26602-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="26602-143">Beispielabfragen</span><span class="sxs-lookup"><span data-stu-id="26602-143">Example Queries</span></span>

<span data-ttu-id="26602-144">In diesem Abschnitt werden die Typen von Abfragen gezeigt, die mithilfe der odata-Abfrage Optionen möglich sind.</span><span class="sxs-lookup"><span data-stu-id="26602-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="26602-145">Spezifische Details zu den Abfrage Optionen finden Sie in der odata-Dokumentation unter [www.odata.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="26602-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="26602-146">Informationen zu $Expand und $SELECT finden Sie unter [Verwenden von $SELECT, $Expand und $Value in ASP.net-Web-API odata](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="26602-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="26602-147">**Client gesteuerte Auslagerung**</span><span class="sxs-lookup"><span data-stu-id="26602-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="26602-148">Bei großen Entitätenmengen kann es vorkommen, dass der Client die Anzahl der Ergebnisse einschränkt.</span><span class="sxs-lookup"><span data-stu-id="26602-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="26602-149">Ein Client kann z. b. 10 Einträge gleichzeitig mit "Next"-Links anzeigen, um die nächste Seite mit Ergebnissen zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="26602-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="26602-150">Zu diesem Zweck verwendet der Client die Optionen $Top und $Skip.</span><span class="sxs-lookup"><span data-stu-id="26602-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="26602-151">Die $Top-Option gibt die maximale Anzahl von Einträgen an, die zurückgegeben werden, und die $Skip-Option gibt die Anzahl der zu über springenden Einträge an.</span><span class="sxs-lookup"><span data-stu-id="26602-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="26602-152">Im vorherigen Beispiel werden die Einträge 21 bis 30 abgerufen.</span><span class="sxs-lookup"><span data-stu-id="26602-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="26602-153">**Filterung**</span><span class="sxs-lookup"><span data-stu-id="26602-153">**Filtering**</span></span>

<span data-ttu-id="26602-154">Die Option $Filter ermöglicht einem Client das Filtern der Ergebnisse durch Anwenden eines booleschen Ausdrucks.</span><span class="sxs-lookup"><span data-stu-id="26602-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="26602-155">Die Filter Ausdrücke sind sehr leistungsstark. Dazu zählen logische und arithmetische Operatoren, Zeichen folgen Funktionen und Datumsfunktionen.</span><span class="sxs-lookup"><span data-stu-id="26602-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="26602-156">Gibt alle Produkte zurück, deren Kategorie "Toys" entspricht.</span><span class="sxs-lookup"><span data-stu-id="26602-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="26602-157">`http://localhost/Products?$filter=Category`EQ ' Toys '</span><span class="sxs-lookup"><span data-stu-id="26602-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="26602-158">Gibt alle Produkte zurück, deren Preis kleiner als 10 ist.</span><span class="sxs-lookup"><span data-stu-id="26602-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="26602-159">`http://localhost/Products?$filter=Price`lt 10</span><span class="sxs-lookup"><span data-stu-id="26602-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="26602-160">Logische Operatoren: gibt alle Produkte zurück, bei denen Price >= 5 und Price <= 15 ist.</span><span class="sxs-lookup"><span data-stu-id="26602-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="26602-161">`http://localhost/Products?$filter=Price`ge 5 und Preis Le 15</span><span class="sxs-lookup"><span data-stu-id="26602-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="26602-162">Zeichen folgen Funktionen: gibt alle Produkte mit "zz" im Namen zurück.</span><span class="sxs-lookup"><span data-stu-id="26602-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="26602-163">Datumsfunktionen: gibt alle Produkte mit ReleaseDate nach 2005 zurück.</span><span class="sxs-lookup"><span data-stu-id="26602-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="26602-164">`http://localhost/Products?$filter=year(ReleaseDate)`gt 2005</span><span class="sxs-lookup"><span data-stu-id="26602-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="26602-165">**Sortieren**</span><span class="sxs-lookup"><span data-stu-id="26602-165">**Sorting**</span></span>

<span data-ttu-id="26602-166">Um die Ergebnisse zu sortieren, verwenden Sie den $OrderBy Filter.</span><span class="sxs-lookup"><span data-stu-id="26602-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="26602-167">Nach Preis sortieren.</span><span class="sxs-lookup"><span data-stu-id="26602-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="26602-168">Sortieren Sie nach Preis in absteigender Reihenfolge (höchste zum niedrigsten).</span><span class="sxs-lookup"><span data-stu-id="26602-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="26602-169">Sortieren Sie nach Kategorie, und sortieren Sie Sie nach Preis in absteigender Reihenfolge innerhalb von Kategorien.</span><span class="sxs-lookup"><span data-stu-id="26602-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="26602-170">Server gesteuerte Auslagerung</span><span class="sxs-lookup"><span data-stu-id="26602-170">Server-Driven Paging</span></span>

<span data-ttu-id="26602-171">Wenn Ihre Datenbank Millionen von Datensätzen enthält, möchten Sie Sie nicht alle in einer Nutzlast senden.</span><span class="sxs-lookup"><span data-stu-id="26602-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="26602-172">Um dies zu verhindern, kann der Server die Anzahl der gesendeten Einträge in einer einzelnen Antwort einschränken.</span><span class="sxs-lookup"><span data-stu-id="26602-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="26602-173">Legen Sie zum **Aktivieren der Server** Auslagerung die **PageSize** -Eigenschaft im abfragbaren Attribut fest.</span><span class="sxs-lookup"><span data-stu-id="26602-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="26602-174">Der Wert ist die maximale Anzahl von Einträgen, die zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="26602-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="26602-175">Wenn Ihr Controller das odata-Format zurückgibt, enthält der Antworttext einen Link zur nächsten Seite der Daten:</span><span class="sxs-lookup"><span data-stu-id="26602-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="26602-176">Der Client kann den Link zum Abrufen der nächsten Seite verwenden.</span><span class="sxs-lookup"><span data-stu-id="26602-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="26602-177">Wenn Sie die Gesamtanzahl der Einträge im Resultset ermitteln möchten, kann der Client die $inlinecount Query-Option mit dem Wert "AllPages" festlegen.</span><span class="sxs-lookup"><span data-stu-id="26602-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="26602-178">Der Wert "AllPages" weist den Server an, die Gesamtanzahl in die Antwort einzubeziehen:</span><span class="sxs-lookup"><span data-stu-id="26602-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="26602-179">Next-Page-Links und Inline Anzahl erfordern beide das odata-Format.</span><span class="sxs-lookup"><span data-stu-id="26602-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="26602-180">Der Grund hierfür ist, dass odata spezielle Felder im Antworttext definiert, um den Link und die Anzahl zu speichern.</span><span class="sxs-lookup"><span data-stu-id="26602-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="26602-181">Bei nicht-odata-Formaten ist es weiterhin möglich, die Links der nächsten Seite und die Inline Anzahl zu unterstützen, indem die Abfrageergebnisse in ein \*\*PageResult &lt; T &gt; \*\* -Objekt eingebunden werden.</span><span class="sxs-lookup"><span data-stu-id="26602-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="26602-182">Es ist jedoch etwas mehr Code erforderlich.</span><span class="sxs-lookup"><span data-stu-id="26602-182">However, it requires a bit more code.</span></span> <span data-ttu-id="26602-183">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="26602-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="26602-184">Hier ist ein Beispiel für eine JSON-Antwort:</span><span class="sxs-lookup"><span data-stu-id="26602-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="26602-185">Einschränken der Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-185">Limiting the Query Options</span></span>

<span data-ttu-id="26602-186">Die Abfrage Optionen sorgen für eine hohe Kontrolle über die Abfrage, die auf dem Server ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="26602-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="26602-187">In einigen Fällen möchten Sie möglicherweise die verfügbaren Optionen aus Sicherheits-oder Leistungsgründen einschränken.</span><span class="sxs-lookup"><span data-stu-id="26602-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="26602-188">Das **[quervable]** -Attribut verfügt über einige integrierte Eigenschaften für diesen.</span><span class="sxs-lookup"><span data-stu-id="26602-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="26602-189">Die folgende Auflistung enthält einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="26602-189">Here are some examples.</span></span>

<span data-ttu-id="26602-190">Nur $Skip und $Top zulassen, um das Paging zu unterstützen, und nichts anderes:</span><span class="sxs-lookup"><span data-stu-id="26602-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="26602-191">Die Sortierung wird nur nach bestimmten Eigenschaften ermöglicht, um das Sortieren von Eigenschaften zu verhindern, die nicht in der Datenbank indiziert werden:</span><span class="sxs-lookup"><span data-stu-id="26602-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="26602-192">Ermöglicht die logische Funktion "EQ", aber keine anderen logischen Funktionen:</span><span class="sxs-lookup"><span data-stu-id="26602-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="26602-193">Arithmetische Operatoren dürfen nicht zugelassen werden:</span><span class="sxs-lookup"><span data-stu-id="26602-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="26602-194">Sie können Optionen Global einschränken, indem Sie eine **queryableattribute** -Instanz erstellen und Sie an die **enablequerysupport** -Funktion übergeben:</span><span class="sxs-lookup"><span data-stu-id="26602-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="26602-195">Direktes Aufrufen von Abfrage Optionen</span><span class="sxs-lookup"><span data-stu-id="26602-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="26602-196">Anstatt das **[quervable]** -Attribut zu verwenden, können Sie die Abfrage Optionen direkt in Ihrem Controller aufrufen.</span><span class="sxs-lookup"><span data-stu-id="26602-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="26602-197">Fügen Sie zu diesem Zweck der Controller Methode einen **odataqueryoptions** -Parameter hinzu.</span><span class="sxs-lookup"><span data-stu-id="26602-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="26602-198">In diesem Fall benötigen Sie das Attribut **[quervable]** nicht.</span><span class="sxs-lookup"><span data-stu-id="26602-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="26602-199">Die Web-API füllt **odataqueryoptions** aus der URI-Abfrage Zeichenfolge auf.</span><span class="sxs-lookup"><span data-stu-id="26602-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="26602-200">Übergeben Sie zum Anwenden der Abfrage ein **iquerable** -Element an die **ApplyTo** -Methode.</span><span class="sxs-lookup"><span data-stu-id="26602-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="26602-201">Die-Methode gibt eine andere **iquerable**zurück.</span><span class="sxs-lookup"><span data-stu-id="26602-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="26602-202">Wenn Sie für erweiterte Szenarien keinen **iquerable** -Abfrage Anbieter haben, können Sie **odataqueryoptions** untersuchen und die Abfrage Optionen in eine andere Form übersetzen.</span><span class="sxs-lookup"><span data-stu-id="26602-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="26602-203">(Informationen hierzu finden Sie beispielsweise im Blogbeitrag zum über [setzen von odata-Abfragen in HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), der auch ein [Beispiel](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)enthält.</span><span class="sxs-lookup"><span data-stu-id="26602-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="26602-204">Abfrage Validierung</span><span class="sxs-lookup"><span data-stu-id="26602-204">Query Validation</span></span>

<span data-ttu-id="26602-205">Das **[quervable]** -Attribut überprüft die Abfrage vor der Ausführung.</span><span class="sxs-lookup"><span data-stu-id="26602-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="26602-206">Der Validierungs Schritt wird in der **queryableattribute. validatequery** -Methode ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="26602-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="26602-207">Sie können auch den Validierungsprozess anpassen.</span><span class="sxs-lookup"><span data-stu-id="26602-207">You can also customize the validation process.</span></span>

<span data-ttu-id="26602-208">Siehe auch [odata-Sicherheits Leit Faden](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="26602-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="26602-209">Überschreiben Sie zunächst eine der Prüfungs-Klassen, die im **Web. http. odata. Query. Validators** -Namespace definiert sind.</span><span class="sxs-lookup"><span data-stu-id="26602-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="26602-210">Die folgende Prüfungs-Klasse deaktiviert z. b. die Option "DESC" für die $OrderBy-Option.</span><span class="sxs-lookup"><span data-stu-id="26602-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="26602-211">Unterklasse das **[quervable]** -Attribut, um die **validatequery** -Methode zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="26602-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="26602-212">Legen Sie dann das benutzerdefinierte Attribut entweder global oder pro Controller fest:</span><span class="sxs-lookup"><span data-stu-id="26602-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="26602-213">Wenn Sie **odataqueryoptions** direkt verwenden, legen Sie das Validierungs Steuerelement für die Optionen fest:</span><span class="sxs-lookup"><span data-stu-id="26602-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
