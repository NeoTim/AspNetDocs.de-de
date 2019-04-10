---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: Zuordnen von SignalR-Benutzern zu Verbindungen in SignalR 1.x | Microsoft-Dokumentation
author: bradygaster
description: In diesem Thema zeigt, wie Informationen über Benutzer und ihre Verbindungen beibehalten wird.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 75c8d2f4a102bef541195280a01d75271331dec4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422511"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="67708-103">Zuordnen von SignalR-Benutzern zu Verbindungen in SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="67708-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="67708-104">durch [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="67708-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="67708-105">In diesem Thema zeigt, wie Informationen über Benutzer und ihre Verbindungen beibehalten wird.</span><span class="sxs-lookup"><span data-stu-id="67708-105">This topic shows how to retain information about users and their connections.</span></span>


## <a name="introduction"></a><span data-ttu-id="67708-106">Einführung</span><span class="sxs-lookup"><span data-stu-id="67708-106">Introduction</span></span>

<span data-ttu-id="67708-107">Jeder Client, Herstellen einer Verbindung mit einem Hub übergibt eine eindeutige Verbindungs-Id an. Sie können diesen Wert im Abrufen der `Context.ConnectionId` Eigenschaft der Hub-Kontexts.</span><span class="sxs-lookup"><span data-stu-id="67708-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="67708-108">Wenn Ihre Anwendung muss einen Benutzer die Verbindungs-Id zuordnen, und die Zuordnung beizubehalten, können Sie eine der folgenden:</span><span class="sxs-lookup"><span data-stu-id="67708-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="67708-109">[In-Memory-Speicher](#inmemory), z. B. ein Wörterbuch</span><span class="sxs-lookup"><span data-stu-id="67708-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="67708-110">SignalR-Gruppe für jeden Benutzer</span><span class="sxs-lookup"><span data-stu-id="67708-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="67708-111">[Dauerhafte, externe Speicher](#database), z. B. eine Datenbanktabelle oder eine Azure-Tabellenspeicher</span><span class="sxs-lookup"><span data-stu-id="67708-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="67708-112">Jede dieser Implementierungen ist in diesem Thema dargestellt.</span><span class="sxs-lookup"><span data-stu-id="67708-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="67708-113">Sie verwenden die `OnConnected`, `OnDisconnected`, und `OnReconnected` Methoden der `Hub` Klasse, um den Verbindungsstatus für den Benutzer zu verfolgen.</span><span class="sxs-lookup"><span data-stu-id="67708-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="67708-114">Der beste Ansatz für Ihre Anwendung hängt von:</span><span class="sxs-lookup"><span data-stu-id="67708-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="67708-115">Die Anzahl von Webservern, die Ihre Anwendung hosten.</span><span class="sxs-lookup"><span data-stu-id="67708-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="67708-116">Gibt an, ob müssen Sie eine Liste der aktuell verbundenen Benutzer zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="67708-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="67708-117">Gibt an, ob müssen Sie die Gruppe und die Benutzerinformationen dauerhaft zu speichern, wenn die Anwendung oder den Server neu gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="67708-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="67708-118">Gibt an, ob die Latenz des Aufrufs von eines externen Servers ein Problem besteht.</span><span class="sxs-lookup"><span data-stu-id="67708-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="67708-119">Die folgende Tabelle zeigt, welcher Ansatz für diese Überlegungen funktioniert.</span><span class="sxs-lookup"><span data-stu-id="67708-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="67708-120">Mehr als einem server</span><span class="sxs-lookup"><span data-stu-id="67708-120">More than one server</span></span> | <span data-ttu-id="67708-121">Rufen Sie die Liste der derzeit verbundenen Benutzer</span><span class="sxs-lookup"><span data-stu-id="67708-121">Get list of currently connected users</span></span> | <span data-ttu-id="67708-122">Speichern Sie die Informationen nach dem Neustart</span><span class="sxs-lookup"><span data-stu-id="67708-122">Persist information after restarts</span></span> | <span data-ttu-id="67708-123">Eine optimale Leistung</span><span class="sxs-lookup"><span data-stu-id="67708-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="67708-124">Im Arbeitsspeicher</span><span class="sxs-lookup"><span data-stu-id="67708-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="67708-125">Einzelbenutzer-Gruppen</span><span class="sxs-lookup"><span data-stu-id="67708-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="67708-126">Externe permanente</span><span class="sxs-lookup"><span data-stu-id="67708-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="67708-127">In-Memory-Speicher</span><span class="sxs-lookup"><span data-stu-id="67708-127">In-memory storage</span></span>

<span data-ttu-id="67708-128">Die folgenden Beispiele zeigen, wie Sie die Verbindung und des Benutzers Informationen in einem Wörterbuch beizubehalten, die im Arbeitsspeicher gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="67708-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="67708-129">Das Wörterbuch verwendet eine `HashSet` die Verbindungs-Id zu speichern. Zu einem beliebigen Zeitpunkt kann ein Benutzer mehr als eine Verbindung mit dem SignalR-Anwendung verfügen.</span><span class="sxs-lookup"><span data-stu-id="67708-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="67708-130">Beispielsweise würde ein Benutzer, die über mehrere Geräte oder mehr als eine Registerkarte "Browser" verbunden ist mehr als ein Verbindungs-Id haben.</span><span class="sxs-lookup"><span data-stu-id="67708-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="67708-131">Wenn die Anwendung heruntergefahren wird, alle Informationen geht verloren, aber erneut aufgefüllt wird, wie die Benutzer die Verbindung erneut herzustellen.</span><span class="sxs-lookup"><span data-stu-id="67708-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="67708-132">In-Memory-Speicher funktionieren nicht, wenn die Umgebung mehrere Webserver umfasst, da jeder Server eine separate Auflistung von Verbindungen verfügen würde.</span><span class="sxs-lookup"><span data-stu-id="67708-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="67708-133">Das erste Beispiel zeigt eine Klasse, die Zuordnung von Benutzern zu Verbindungen verwaltet, werden.</span><span class="sxs-lookup"><span data-stu-id="67708-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="67708-134">Der Schlüssel für das HashSet werden der Name des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="67708-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="67708-135">Das nächste Beispiel zeigt, wie Sie mit der Zuordnung Verbindungsklasse über einen Hub.</span><span class="sxs-lookup"><span data-stu-id="67708-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="67708-136">Die Instanz der Klasse befindet sich in einen Variablennamen `_connections`.</span><span class="sxs-lookup"><span data-stu-id="67708-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="67708-137">Einzelbenutzer-Gruppen</span><span class="sxs-lookup"><span data-stu-id="67708-137">Single-user groups</span></span>

<span data-ttu-id="67708-138">Sie können eine Gruppe für jeden Benutzer erstellen und zu dieser Gruppe klicken Sie dann eine Nachricht senden, wenn Sie nur dieser Benutzer erreichen möchten.</span><span class="sxs-lookup"><span data-stu-id="67708-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="67708-139">Der Name jeder Gruppe ist der Name des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="67708-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="67708-140">Wenn ein Benutzer mehrere Verbindungen verfügt, wird die Gruppe des Benutzers jeder Verbindungs-Id hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="67708-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="67708-141">Sie sollten nicht manuell entfernen des Benutzers aus der Gruppe, wenn der Benutzer die Verbindung trennt.</span><span class="sxs-lookup"><span data-stu-id="67708-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="67708-142">Dadurch wird automatisch vom SignalR-Framework ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="67708-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="67708-143">Das folgende Beispiel zeigt, wie Sie Gruppen für einzelne Benutzer zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="67708-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="67708-144">Dauerhafte, externe Speicher</span><span class="sxs-lookup"><span data-stu-id="67708-144">Permanent, external storage</span></span>

<span data-ttu-id="67708-145">In diesem Thema wird gezeigt, wie eine Datenbank oder Azure-Tabellenspeicher verwenden Sie zum Speichern von Verbindungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="67708-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="67708-146">Dieser Ansatz funktioniert, wenn Sie mehrere Webserver haben, da jedem Webserver mit der gleichen Data-Repository interagieren kann.</span><span class="sxs-lookup"><span data-stu-id="67708-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="67708-147">Wenn Ihre Webserver arbeiten oder die Anwendung neu gestartet wird, beenden die `OnDisconnected` Methode wird nicht aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="67708-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="67708-148">Aus diesem Grund ist es möglich, dass Ihr Datenrepository Datensätze für Verbindungs-Ids gibt, die nicht mehr gültig sind.</span><span class="sxs-lookup"><span data-stu-id="67708-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="67708-149">Um diese verwaiste Einträge zu bereinigen, möchten Sie möglicherweise eine Verbindung für ungültig zu erklären, die außerhalb eines Zeitrahmens erstellt wurde, die für Ihre Anwendung relevant ist.</span><span class="sxs-lookup"><span data-stu-id="67708-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="67708-150">In die Beispielen in diesem Abschnitt enthalten einen Wert zum Nachverfolgen, wann die Verbindung erstellt wurde, aber nicht um alte Datensätze zu bereinigen, da möglicherweise Sie dies als Hintergrundprozess möchten anzeigen.</span><span class="sxs-lookup"><span data-stu-id="67708-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="67708-151">Datenbank</span><span class="sxs-lookup"><span data-stu-id="67708-151">Database</span></span>

<span data-ttu-id="67708-152">Die folgenden Beispiele zeigen, wie Sie die Verbindung und des Benutzers Informationen in einer Datenbank beibehalten wird.</span><span class="sxs-lookup"><span data-stu-id="67708-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="67708-153">Sie können neue datenzugriffstechnologie verwenden. Im folgenden Beispiel zeigt jedoch wie Sie Modelle, die mithilfe von Entity Framework zu definieren.</span><span class="sxs-lookup"><span data-stu-id="67708-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="67708-154">Diese Entitätsmodelle, Tabellen und Felder entsprechen.</span><span class="sxs-lookup"><span data-stu-id="67708-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="67708-155">Die Datenstruktur kann je nach den Anforderungen Ihrer Anwendung erheblich variieren.</span><span class="sxs-lookup"><span data-stu-id="67708-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="67708-156">Das erste Beispiel zeigt, wie Sie eine Benutzerentität definieren, die viele Entitäten der Verbindung zugeordnet werden können.</span><span class="sxs-lookup"><span data-stu-id="67708-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="67708-157">Anschließend können Sie im Hub den Status der einzelnen Verbindung mit den folgenden Code verfolgen.</span><span class="sxs-lookup"><span data-stu-id="67708-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="67708-158">Azure-Tabellenspeicher</span><span class="sxs-lookup"><span data-stu-id="67708-158">Azure table storage</span></span>

<span data-ttu-id="67708-159">Im folgenden Beispiel von Azure Table Storage ist ähnlich wie im Beispiel für die Datenbank.</span><span class="sxs-lookup"><span data-stu-id="67708-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="67708-160">Es enthält alle Informationen, die keine, die Sie benötigen würden, erste Schritte mit Azure Table Storage-Dienst.</span><span class="sxs-lookup"><span data-stu-id="67708-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="67708-161">Weitere Informationen finden Sie unter [Gewusst wie: Verwenden von Tabellenspeicher aus .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="67708-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="67708-162">Das folgende Beispiel zeigt eine Tabellenentität zum Speichern von Verbindungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="67708-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="67708-163">Sie Partitionen, die Daten über den Benutzernamen, und jede Entität von der Verbindungs­ID identifiziert werden, damit ein Benutzer mehrere Verbindungen zu einem beliebigen Zeitpunkt verfügen kann.</span><span class="sxs-lookup"><span data-stu-id="67708-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="67708-164">In den Hub verfolgen Sie den Status der Verbindung des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="67708-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
