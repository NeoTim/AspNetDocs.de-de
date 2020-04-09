---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Zuordnen von SignalR-Benutzern zu Verbindungen | Microsoft Docs
author: bradygaster
description: In diesem Thema wird gezeigt, wie Informationen über Benutzer und deren Verbindungen beibehalten werden. Patrick Fletcher hat an diesem Thema mitgewirkt. Softwareversionen, die in diesem Thema verwendet werden...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675778"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="6ed94-105">Zuordnen von SignalR-Benutzern zu Verbindungen</span><span class="sxs-lookup"><span data-stu-id="6ed94-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="6ed94-106"> von [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6ed94-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="6ed94-107">In diesem Thema wird gezeigt, wie Informationen über Benutzer und deren Verbindungen beibehalten werden.</span><span class="sxs-lookup"><span data-stu-id="6ed94-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="6ed94-108">Patrick Fletcher hat an diesem Thema mitgewirkt.</span><span class="sxs-lookup"><span data-stu-id="6ed94-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="6ed94-109">In diesem Thema verwendete Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="6ed94-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="6ed94-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6ed94-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="6ed94-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6ed94-111">.NET 4.5</span></span>
> - <span data-ttu-id="6ed94-112">SignalR Version 2</span><span class="sxs-lookup"><span data-stu-id="6ed94-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="6ed94-113">Frühere Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="6ed94-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="6ed94-114">Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="6ed94-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="6ed94-115">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="6ed94-115">Questions and comments</span></span>
>
> <span data-ttu-id="6ed94-116">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="6ed94-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6ed94-117">Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="6ed94-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="6ed94-118">Einführung</span><span class="sxs-lookup"><span data-stu-id="6ed94-118">Introduction</span></span>

<span data-ttu-id="6ed94-119">Jeder Client, der eine Verbindung zu einem Hub herstellt, übergibt eine eindeutige Verbindungs-ID. Sie können diesen Wert `Context.ConnectionId` in der Eigenschaft des Hubkontexts abrufen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="6ed94-120">Wenn Ihre Anwendung einen Benutzer der Verbindungs-ID zuordnen und diese Zuordnung beibehalten muss, können Sie eine der folgenden Optionen verwenden:</span><span class="sxs-lookup"><span data-stu-id="6ed94-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="6ed94-121">Der Benutzer-ID-Anbieter (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="6ed94-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="6ed94-122">[In-Memory-Speicher](#inmemory), z. B. ein Wörterbuch</span><span class="sxs-lookup"><span data-stu-id="6ed94-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="6ed94-123">SignalR-Gruppe für jeden Benutzer</span><span class="sxs-lookup"><span data-stu-id="6ed94-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="6ed94-124">[Permanenter, externer Speicher](#database), z. B. eine Datenbanktabelle oder ein Azure-Tabellenspeicher</span><span class="sxs-lookup"><span data-stu-id="6ed94-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="6ed94-125">Jede dieser Implementierungen wird in diesem Thema angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6ed94-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="6ed94-126">Sie verwenden `OnConnected` `OnDisconnected`die `OnReconnected` , und `Hub` Methoden der Klasse, um den Benutzerverbindungsstatus nachzuverfolgen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="6ed94-127">Der beste Ansatz für Ihre Anwendung hängt von folgenden Faktoren ab:</span><span class="sxs-lookup"><span data-stu-id="6ed94-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="6ed94-128">Die Anzahl der Webserver, auf denen Ihre Anwendung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="6ed94-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="6ed94-129">Gibt an, ob Sie eine Liste der aktuell verbundenen Benutzer abrufen müssen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="6ed94-130">Gibt an, ob Sie Gruppen- und Benutzerinformationen beibehalten müssen, wenn die Anwendung oder der Server neu gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="6ed94-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="6ed94-131">Gibt es die Frage, ob die Latenz beim Aufrufen eines externen Servers ein Problem ist.</span><span class="sxs-lookup"><span data-stu-id="6ed94-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="6ed94-132">Die folgende Tabelle zeigt, welcher Ansatz für diese Überlegungen funktioniert.</span><span class="sxs-lookup"><span data-stu-id="6ed94-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="6ed94-133">Mehr als ein Server</span><span class="sxs-lookup"><span data-stu-id="6ed94-133">More than one server</span></span> | <span data-ttu-id="6ed94-134">Liste der aktuell verbundenen Benutzer abrufen</span><span class="sxs-lookup"><span data-stu-id="6ed94-134">Get list of currently connected users</span></span> | <span data-ttu-id="6ed94-135">Persistenkinformationen nach Neustarts</span><span class="sxs-lookup"><span data-stu-id="6ed94-135">Persist information after restarts</span></span> | <span data-ttu-id="6ed94-136">Optimale Leistung</span><span class="sxs-lookup"><span data-stu-id="6ed94-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6ed94-137">UserID-Anbieter</span><span class="sxs-lookup"><span data-stu-id="6ed94-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="6ed94-138">In-Memory</span><span class="sxs-lookup"><span data-stu-id="6ed94-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="6ed94-139">Einzelbenutzergruppen</span><span class="sxs-lookup"><span data-stu-id="6ed94-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="6ed94-140">Permanent, extern</span><span class="sxs-lookup"><span data-stu-id="6ed94-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="6ed94-141">IUserID-Anbieter</span><span class="sxs-lookup"><span data-stu-id="6ed94-141">IUserID provider</span></span>

<span data-ttu-id="6ed94-142">Mit dieser Funktion können Benutzer über eine neue Schnittstelle IUserIdProvider angeben, was die userId auf einer IRequest basiert.</span><span class="sxs-lookup"><span data-stu-id="6ed94-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="6ed94-143">**Der IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="6ed94-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="6ed94-144">Standardmäßig gibt es eine Implementierung, die die `IPrincipal.Identity.Name` des Benutzers als Benutzernamen verwendet.</span><span class="sxs-lookup"><span data-stu-id="6ed94-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="6ed94-145">Um dies zu ändern, registrieren Sie Ihre Implementierung beim `IUserIdProvider` globalen Host, wenn Ihre Anwendung gestartet wird:</span><span class="sxs-lookup"><span data-stu-id="6ed94-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="6ed94-146">Von einem Hub aus können Sie Nachrichten über die folgende API an diese Benutzer senden:</span><span class="sxs-lookup"><span data-stu-id="6ed94-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="6ed94-147">**Senden einer Nachricht an einen bestimmten Benutzer**</span><span class="sxs-lookup"><span data-stu-id="6ed94-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="6ed94-148">In-Memory-Speicher</span><span class="sxs-lookup"><span data-stu-id="6ed94-148">In-memory storage</span></span>

<span data-ttu-id="6ed94-149">Die folgenden Beispiele zeigen, wie Verbindungs- und Benutzerinformationen in einem Wörterbuch gespeichert werden, das im Arbeitsspeicher gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="6ed94-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="6ed94-150">Das Wörterbuch `HashSet` verwendet eine, um die Verbindungs-ID zu speichern. Ein Benutzer kann jederzeit mehr als eine Verbindung zur SignalR-Anwendung haben.</span><span class="sxs-lookup"><span data-stu-id="6ed94-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="6ed94-151">Beispielsweise verfügt ein Benutzer, der über mehrere Geräte oder mehr als eine Browserregisterkarte verbunden ist, über mehr als eine Verbindungs-ID.</span><span class="sxs-lookup"><span data-stu-id="6ed94-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="6ed94-152">Wenn die Anwendung heruntergefahren wird, gehen alle Informationen verloren, sie werden jedoch erneut aufgefüllt, wenn die Benutzer ihre Verbindungen wieder herstellen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="6ed94-153">In-Memory-Speicher funktioniert nicht, wenn Ihre Umgebung mehr als einen Webserver umfasst, da jeder Server über eine separate Sammlung von Verbindungen verfügen würde.</span><span class="sxs-lookup"><span data-stu-id="6ed94-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="6ed94-154">Das erste Beispiel zeigt eine Klasse, die die Zuordnung von Benutzern zu Verbindungen verwaltet.</span><span class="sxs-lookup"><span data-stu-id="6ed94-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="6ed94-155">Der Schlüssel für das HashSet ist der Name des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6ed94-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="6ed94-156">Das nächste Beispiel zeigt, wie die Verbindungszuordnungsklasse von einem Hub aus verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6ed94-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="6ed94-157">Die Instanz der Klasse wird in `_connections`einem Variablennamen gespeichert.</span><span class="sxs-lookup"><span data-stu-id="6ed94-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="6ed94-158">Einzelbenutzergruppen</span><span class="sxs-lookup"><span data-stu-id="6ed94-158">Single-user groups</span></span>

<span data-ttu-id="6ed94-159">Sie können eine Gruppe für jeden Benutzer erstellen und dann eine Nachricht an diese Gruppe senden, wenn Sie nur diesen Benutzer erreichen möchten.</span><span class="sxs-lookup"><span data-stu-id="6ed94-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="6ed94-160">Der Name jeder Gruppe ist der Name des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6ed94-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="6ed94-161">Wenn ein Benutzer über mehr als eine Verbindung verfügt, wird jede Verbindungs-ID der Gruppe des Benutzers hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6ed94-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="6ed94-162">Sie sollten den Benutzer nicht manuell aus der Gruppe entfernen, wenn der Benutzer die Verbindung trennt.</span><span class="sxs-lookup"><span data-stu-id="6ed94-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="6ed94-163">Diese Aktion wird automatisch vom SignalR-Framework ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="6ed94-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="6ed94-164">Das folgende Beispiel zeigt, wie Einzelbenutzergruppen implementiert werden.</span><span class="sxs-lookup"><span data-stu-id="6ed94-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="6ed94-165">Permanenter, externer Speicher</span><span class="sxs-lookup"><span data-stu-id="6ed94-165">Permanent, external storage</span></span>

<span data-ttu-id="6ed94-166">In diesem Thema wird gezeigt, wie Sie entweder eine Datenbank oder einen Azure-Tabellenspeicher zum Speichern von Verbindungsinformationen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6ed94-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="6ed94-167">Dieser Ansatz funktioniert, wenn Sie über mehrere Webserver verfügen, da jeder Webserver mit demselben Datenrepository interagieren kann.</span><span class="sxs-lookup"><span data-stu-id="6ed94-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="6ed94-168">Wenn Ihre Webserver nicht mehr funktionieren `OnDisconnected` oder die Anwendung neu gestartet wird, wird die Methode nicht aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="6ed94-169">Daher ist es möglich, dass Ihr Datenrepository Datensätze für Verbindungs-IDs enthält, die nicht mehr gültig sind.</span><span class="sxs-lookup"><span data-stu-id="6ed94-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="6ed94-170">Um diese verwaisten Datensätze zu bereinigen, können Sie jede Verbindung ungültig machen, die außerhalb eines Zeitrahmens erstellt wurde, der für Ihre Anwendung relevant ist.</span><span class="sxs-lookup"><span data-stu-id="6ed94-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="6ed94-171">Die Beispiele in diesem Abschnitt enthalten einen Wert für die Nachverfolgung beim Erstellen der Verbindung, zeigen jedoch nicht, wie alte Datensätze bereinigen werden, da Sie dies möglicherweise als Hintergrundprozess tun möchten.</span><span class="sxs-lookup"><span data-stu-id="6ed94-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="6ed94-172">Datenbank</span><span class="sxs-lookup"><span data-stu-id="6ed94-172">Database</span></span>

<span data-ttu-id="6ed94-173">Die folgenden Beispiele zeigen, wie Verbindungs- und Benutzerinformationen in einer Datenbank beibehalten werden.</span><span class="sxs-lookup"><span data-stu-id="6ed94-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="6ed94-174">Sie können jede Datenzugriffstechnologie verwenden; Das folgende Beispiel zeigt jedoch, wie Modelle mit Entity Framework definiert werden.</span><span class="sxs-lookup"><span data-stu-id="6ed94-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="6ed94-175">Diese Entitätsmodelle entsprechen Datenbanktabellen und -feldern.</span><span class="sxs-lookup"><span data-stu-id="6ed94-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="6ed94-176">Ihre Datenstruktur kann je nach den Anforderungen Ihrer Anwendung erheblich variieren.</span><span class="sxs-lookup"><span data-stu-id="6ed94-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="6ed94-177">Das erste Beispiel zeigt, wie Sie eine Benutzerentität definieren, die vielen Verbindungsentitäten zugeordnet werden kann.</span><span class="sxs-lookup"><span data-stu-id="6ed94-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="6ed94-178">Anschließend können Sie vom Hub aus den Status jeder Verbindung mit dem unten gezeigten Code nachverfolgen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="6ed94-179">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="6ed94-179">Azure table storage</span></span>

<span data-ttu-id="6ed94-180">Das folgende Azure-Tabellenspeicherbeispiel ähnelt dem Datenbankbeispiel.</span><span class="sxs-lookup"><span data-stu-id="6ed94-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="6ed94-181">Sie enthält nicht alle Informationen, die Sie benötigen, um mit Azure Table Storage Service zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="6ed94-182">Weitere Informationen finden Sie unter [Verwenden von Tabellenspeicher aus .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="6ed94-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="6ed94-183">Das folgende Beispiel zeigt eine Tabellenentität zum Speichern von Verbindungsinformationen.</span><span class="sxs-lookup"><span data-stu-id="6ed94-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="6ed94-184">Es partitioniert die Daten nach Benutzername und identifiziert jede Entität anhand der Verbindungs-ID, sodass ein Benutzer jederzeit mehrere Verbindungen haben kann.</span><span class="sxs-lookup"><span data-stu-id="6ed94-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="6ed94-185">Im Hub verfolgen Sie den Status der Verbindung jedes Benutzers.</span><span class="sxs-lookup"><span data-stu-id="6ed94-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
