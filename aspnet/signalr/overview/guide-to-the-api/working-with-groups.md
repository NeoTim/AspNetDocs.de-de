---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: Arbeiten mit Gruppen in SignalR | Microsoft-Dokumentation
author: bradygaster
description: In diesem Thema wird beschrieben, wie Informationen über die Gruppenmitgliedschaft mit der Hub-API beibehalten wird.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 384b7e5f07fa46ea3cc32e5c18c3c2327b7aedd3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025307"
---
<a name="working-with-groups-in-signalr"></a><span data-ttu-id="286ad-103">Arbeiten mit Gruppen in SignalR</span><span class="sxs-lookup"><span data-stu-id="286ad-103">Working with Groups in SignalR</span></span>
====================
<span data-ttu-id="286ad-104">durch [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="286ad-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="286ad-105">In diesem Thema wird beschrieben, wie zum Hinzufügen von Benutzern zu Gruppen und Beibehalten von Informationen über die Gruppenmitgliedschaft wird.</span><span class="sxs-lookup"><span data-stu-id="286ad-105">This topic describes how to add users to groups and persist group membership information.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="286ad-106">In diesem Thema verwendeten Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="286ad-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="286ad-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="286ad-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="286ad-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="286ad-108">.NET 4.5</span></span>
> - <span data-ttu-id="286ad-109">SignalR-Version 2</span><span class="sxs-lookup"><span data-stu-id="286ad-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="286ad-110">Vorherige Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="286ad-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="286ad-111">Weitere Informationen zu früheren Versionen von SignalR, finden Sie unter [ältere Versionen von SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="286ad-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="286ad-112">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="286ad-112">Questions and comments</span></span>
>
> <span data-ttu-id="286ad-113">Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können.</span><span class="sxs-lookup"><span data-stu-id="286ad-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="286ad-114">Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="286ad-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="286ad-115">Übersicht</span><span class="sxs-lookup"><span data-stu-id="286ad-115">Overview</span></span>

<span data-ttu-id="286ad-116">Gruppen in SignalR bieten eine Methode zum Übertragen von Nachrichten an die angegebene Teilmengen von verbundenen Clients.</span><span class="sxs-lookup"><span data-stu-id="286ad-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="286ad-117">Eine Gruppe kann eine beliebige Anzahl Clients umfassen, und ein Client kann Mitglied einer beliebigen Anzahl von Gruppen sein.</span><span class="sxs-lookup"><span data-stu-id="286ad-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="286ad-118">Sie haben keine Gruppen explizit zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="286ad-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="286ad-119">Aktiviert ist, eine Gruppe wird automatisch beim ersten Sie seinen Namen in einem Aufruf von Groups.Add angeben erstellt, und es wird gelöscht, wenn Sie aus der Mitgliedschaft in der sie die letzte Verbindung entfernen.</span><span class="sxs-lookup"><span data-stu-id="286ad-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="286ad-120">Eine Einführung zum Verwenden von Gruppen finden Sie unter [zum Verwalten von Gruppenmitgliedschaften aus der hubklasse](hubs-api-guide-server.md#groupsfromhub) in die Hubs-API – Server-Handbuch.</span><span class="sxs-lookup"><span data-stu-id="286ad-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="286ad-121">Es ist keine API zum Abrufen der Mitgliederliste einer Gruppe oder eine Liste der Gruppen ein.</span><span class="sxs-lookup"><span data-stu-id="286ad-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="286ad-122">SignalR sendet Nachrichten an Clients und Gruppen, die auf Grundlage eines Pub/Sub-Modells, und der Server behält keine Listen mit Gruppen oder Gruppenmitgliedschaften.</span><span class="sxs-lookup"><span data-stu-id="286ad-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="286ad-123">Dadurch wird das Maximieren der Skalierbarkeit, da Wenn Sie einen Knoten zu einer Webfarm hinzufügen, verfügt über einem beliebigen Zustand, in der SignalR verwaltet, die auf den neuen Knoten weitergegeben werden.</span><span class="sxs-lookup"><span data-stu-id="286ad-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="286ad-124">Wenn Sie einen Benutzer hinzufügen, um eine Gruppe mit der `Groups.Add` -Methode, die der Benutzer erhält Nachrichten, die zu dieser Gruppe für die Dauer der aktuellen Verbindung geleitet, aber die Mitgliedschaft des Benutzers in dieser Gruppe wird nicht beibehalten, über die aktuelle Verbindung.</span><span class="sxs-lookup"><span data-stu-id="286ad-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="286ad-125">Wenn Sie Informationen zu Gruppen und Gruppenmitgliedschaften dauerhaft beibehalten möchten, müssen Sie die Daten in einem Repository wie z. B. eine Datenbank oder Azure-Tabellenspeicher speichern.</span><span class="sxs-lookup"><span data-stu-id="286ad-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="286ad-126">Klicken Sie dann jedes Mal, wenn ein Benutzer eine Verbindung Ihrer Anwendung mit Sie aus dem Repository abrufen, welchen Gruppen der Benutzer angehört, und fügen Sie diesen Benutzer für diese Gruppen manuell.</span><span class="sxs-lookup"><span data-stu-id="286ad-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="286ad-127">Beim Wiederherstellen der Verbindung nach einer vorübergehenden Störung verknüpft neu der Benutzer automatisch die zuvor zugewiesene Gruppen.</span><span class="sxs-lookup"><span data-stu-id="286ad-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="286ad-128">Tritt automatisch eine Gruppe gilt nur beim Wiederherstellen der Verbindung nicht verwendet werden, wenn eine neue Verbindung herstellen.</span><span class="sxs-lookup"><span data-stu-id="286ad-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="286ad-129">Ein digital signiertes Token wird vom Client übergeben, die die Liste der zuvor zugewiesenen Gruppen enthält.</span><span class="sxs-lookup"><span data-stu-id="286ad-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="286ad-130">Wenn Sie möchten überprüfen, ob der Benutzer den angeforderten Gruppen angehört, können Sie das Standardverhalten überschreiben.</span><span class="sxs-lookup"><span data-stu-id="286ad-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="286ad-131">Dieses Thema enthält die folgenden Abschnitte:</span><span class="sxs-lookup"><span data-stu-id="286ad-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="286ad-132">Hinzufügen und Entfernen von Benutzern</span><span class="sxs-lookup"><span data-stu-id="286ad-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="286ad-133">Aufrufen von Membern einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="286ad-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="286ad-134">Mitgliedschaft in einer Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="286ad-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="286ad-135">Das Speichern von Gruppenmitgliedschaften in Azure-Tabellenspeicher</span><span class="sxs-lookup"><span data-stu-id="286ad-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="286ad-136">Überprüfen der Gruppenmitgliedschaft, beim Wiederherstellen der Verbindung</span><span class="sxs-lookup"><span data-stu-id="286ad-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="286ad-137">Hinzufügen und Entfernen von Benutzern</span><span class="sxs-lookup"><span data-stu-id="286ad-137">Adding and removing users</span></span>

<span data-ttu-id="286ad-138">Rufen Sie zum Hinzufügen oder Entfernen von Benutzern aus einer Gruppe, die [hinzufügen](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) oder [entfernen](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) Methoden und Verbindungs-Id des Benutzers und des Namens der Gruppe als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="286ad-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="286ad-139">Sie müssen sich nicht um einen Benutzer manuell aus einer Gruppe zu entfernen, wenn die Verbindung beendet wird.</span><span class="sxs-lookup"><span data-stu-id="286ad-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="286ad-140">Das folgende Beispiel zeigt die `Groups.Add` und `Groups.Remove` Methoden, die in hubmethoden verwendet.</span><span class="sxs-lookup"><span data-stu-id="286ad-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="286ad-141">Die `Groups.Add` und `Groups.Remove` Methoden asynchron ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="286ad-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="286ad-142">Wenn Sie einen Client zu einer Gruppe hinzufügen und eine Nachricht sofort an den Client senden, mit dem Group möchten, müssen Sie sicherstellen, dass die Methode Groups.Add zuerst beendet wird.</span><span class="sxs-lookup"><span data-stu-id="286ad-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="286ad-143">Die folgenden Codebeispiele zeigen, wie das geht.</span><span class="sxs-lookup"><span data-stu-id="286ad-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="286ad-144">Im Allgemeinen sollten Sie nicht einschließen `await` beim Aufrufen der `Groups.Remove` Methode, da die Verbindungs-Id, die Sie entfernen möchten, sind möglicherweise nicht mehr verfügbar.</span><span class="sxs-lookup"><span data-stu-id="286ad-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="286ad-145">In diesem Fall `TaskCanceledException` wird ausgelöst, nachdem die Anforderung ein auftritt Timeout. Wenn Ihre Anwendung sicherstellen muss, dass der Benutzer vor dem Senden einer Nachricht an die Gruppe aus der Gruppe entfernt wurde, können Sie hinzufügen `await` vor `Groups.Remove`, und klicken Sie dann Abfangen der `TaskCanceledException` Ausnahme, die ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="286ad-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="286ad-146">Aufrufen von Membern einer Gruppe</span><span class="sxs-lookup"><span data-stu-id="286ad-146">Calling members of a group</span></span>

<span data-ttu-id="286ad-147">Sie können Nachrichten an alle Mitglieder einer Gruppe oder nur angegebene Mitglieder der Gruppe senden, wie in den folgenden Beispielen gezeigt.</span><span class="sxs-lookup"><span data-stu-id="286ad-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="286ad-148">**Alle** verbundene Clients in einer angegebenen Gruppe.</span><span class="sxs-lookup"><span data-stu-id="286ad-148">**All** connected clients in a specified group.</span></span>

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="286ad-149">Alle verbundenen Clients in einer angegebenen Gruppe **mit Ausnahme der angegebenen Clients**identifizierte Verbindungs-ID.</span><span class="sxs-lookup"><span data-stu-id="286ad-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span>

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="286ad-150">Alle verbundenen Clients in einer angegebenen Gruppe **mit Ausnahme des aufrufenden Clients**.</span><span class="sxs-lookup"><span data-stu-id="286ad-150">All connected clients in a specified group **except the calling client**.</span></span>

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="286ad-151">Mitgliedschaft in einer Datenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="286ad-151">Storing group membership in a database</span></span>

<span data-ttu-id="286ad-152">Die folgenden Beispiele zeigen, wie Gruppen- und Informationen in einer Datenbank beibehalten werden sollen.</span><span class="sxs-lookup"><span data-stu-id="286ad-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="286ad-153">Sie können neue datenzugriffstechnologie verwenden. Im folgenden Beispiel zeigt jedoch wie Sie Modelle, die mithilfe von Entity Framework zu definieren.</span><span class="sxs-lookup"><span data-stu-id="286ad-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="286ad-154">Diese Entitätsmodelle, Tabellen und Felder entsprechen.</span><span class="sxs-lookup"><span data-stu-id="286ad-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="286ad-155">Die Datenstruktur kann je nach den Anforderungen Ihrer Anwendung erheblich variieren.</span><span class="sxs-lookup"><span data-stu-id="286ad-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="286ad-156">Dieses Beispiel enthält eine Klasse namens `ConversationRoom` Was wäre nur für eine Anwendung, die Benutzern ermöglicht, Konversationen zu verschiedenen Themen, wie z. B. Sport "oder" Gartenarbeit zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="286ad-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="286ad-157">Dieses Beispiel enthält auch eine Klasse für die Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="286ad-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="286ad-158">Connection-Klasse ist nicht unbedingt erforderlich ist, für die nachverfolgung der Gruppenmitgliedschaft, aber es ist häufig Teil stabile Lösung zum Nachverfolgen von Benutzern.</span><span class="sxs-lookup"><span data-stu-id="286ad-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="286ad-159">Anschließend können Sie im Hub, rufen die Gruppe und Informationen aus der Datenbank und der manuell zu den entsprechenden Gruppen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="286ad-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="286ad-160">Das Beispiel enthält Code zum Nachverfolgen der benutzerverbindungen keine.</span><span class="sxs-lookup"><span data-stu-id="286ad-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="286ad-161">In diesem Beispiel die `await` Schlüsselwort wird nicht angewendet, bevor Sie `Groups.Add` , da eine Nachricht nicht sofort auf Mitglieder der Gruppe gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="286ad-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="286ad-162">Wenn eine Nachricht an alle Mitglieder der Gruppe zu senden, unmittelbar nachdem das neue Element hinzugefügt werden sollen, Sie möchten gelten die `await` Schlüsselwort, um sicherzustellen, dass der asynchrone Vorgang abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="286ad-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="286ad-163">Das Speichern von Gruppenmitgliedschaften in Azure-Tabellenspeicher</span><span class="sxs-lookup"><span data-stu-id="286ad-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="286ad-164">Mit Azure Table Storage zum Speichern von Informationen von Gruppen- und ähnelt der Verwendung einer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="286ad-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="286ad-165">Das folgende Beispiel zeigt eine Tabelle-Entität, die den Namen und Gruppennamen speichert.</span><span class="sxs-lookup"><span data-stu-id="286ad-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="286ad-166">Rufen Sie im Hub die zugewiesenen Gruppen aus, wenn der Benutzer eine Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="286ad-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="286ad-167">Überprüfen der Gruppenmitgliedschaft, beim Wiederherstellen der Verbindung</span><span class="sxs-lookup"><span data-stu-id="286ad-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="286ad-168">In der Standardeinstellung weist erneut SignalR automatisch einen Benutzer den entsprechenden Gruppen beim Wiederherstellen der Verbindung von einer vorübergehenden Störung, z. B. wenn eine Verbindung gelöscht und erneut hergestellt wird, bevor die Verbindung ein eintritt Timeout. Gruppeninformationen des Benutzers wird in einem Token übergeben, beim Wiederherstellen der Verbindung, und dieses Token wird auf dem Server überprüft.</span><span class="sxs-lookup"><span data-stu-id="286ad-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="286ad-169">Weitere Informationen zu der Überprüfungsprozess für tritt der Benutzer, Gruppen, finden Sie unter [tritt von Gruppen beim Wiederherstellen der Verbindung](../security/introduction-to-security.md#rejoingroup).</span><span class="sxs-lookup"><span data-stu-id="286ad-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="286ad-170">Im Allgemeinen sollten Sie das Standardverhalten des automatisch tritt, dass die Gruppen auf Verbindung verwenden.</span><span class="sxs-lookup"><span data-stu-id="286ad-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="286ad-171">SignalR-Gruppen sind nicht als Sicherheitsmechanismus zum Einschränken des Zugriffs auf sensible Daten vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="286ad-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="286ad-172">Wenn Ihre Anwendung beim Wiederherstellen der Verbindung Gruppenmitgliedschaft des Benutzers überprüfen muss, können Sie das Standardverhalten jedoch überschreiben.</span><span class="sxs-lookup"><span data-stu-id="286ad-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="286ad-173">Ändern des Standardverhaltens kann einer Last mit der Datenbank hinzugefügt werden, da Gruppenmitgliedschaft des Benutzers abgerufen werden muss, für jeden erneuten Herstellen einer Verbindung und nicht nur dann, wenn der Benutzer eine Verbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="286ad-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="286ad-174">Wenn Sie auf der Gruppenmitgliedschaft überprüfen müssen erneut eine Verbindung herzustellen Sie, erstellen Sie ein neues Hub-Pipeline-Modul, das eine Liste mit zugewiesenen Gruppen zurückgibt, wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="286ad-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="286ad-175">Anschließend fügen Sie das Modul an die Hubpipeline wie unten markiert.</span><span class="sxs-lookup"><span data-stu-id="286ad-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]