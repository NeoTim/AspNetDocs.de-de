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
# <a name="mapping-signalr-users-to-connections"></a>Zuordnen von SignalR-Benutzern zu Verbindungen

 von [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> In diesem Thema wird gezeigt, wie Informationen über Benutzer und deren Verbindungen beibehalten werden.
>
> Patrick Fletcher hat an diesem Thema mitgewirkt.
>
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR Version 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Frühere Versionen dieses Themas
>
> Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
>
> Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten. Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).

## <a name="introduction"></a>Einführung

Jeder Client, der eine Verbindung zu einem Hub herstellt, übergibt eine eindeutige Verbindungs-ID. Sie können diesen Wert `Context.ConnectionId` in der Eigenschaft des Hubkontexts abrufen. Wenn Ihre Anwendung einen Benutzer der Verbindungs-ID zuordnen und diese Zuordnung beibehalten muss, können Sie eine der folgenden Optionen verwenden:

- [Der Benutzer-ID-Anbieter (SignalR 2)](#IUserIdProvider)
- [In-Memory-Speicher](#inmemory), z. B. ein Wörterbuch
- [SignalR-Gruppe für jeden Benutzer](#groups)
- [Permanenter, externer Speicher](#database), z. B. eine Datenbanktabelle oder ein Azure-Tabellenspeicher

Jede dieser Implementierungen wird in diesem Thema angezeigt. Sie verwenden `OnConnected` `OnDisconnected`die `OnReconnected` , und `Hub` Methoden der Klasse, um den Benutzerverbindungsstatus nachzuverfolgen.

Der beste Ansatz für Ihre Anwendung hängt von folgenden Faktoren ab:

- Die Anzahl der Webserver, auf denen Ihre Anwendung gehostet wird.
- Gibt an, ob Sie eine Liste der aktuell verbundenen Benutzer abrufen müssen.
- Gibt an, ob Sie Gruppen- und Benutzerinformationen beibehalten müssen, wenn die Anwendung oder der Server neu gestartet wird.
- Gibt es die Frage, ob die Latenz beim Aufrufen eines externen Servers ein Problem ist.

Die folgende Tabelle zeigt, welcher Ansatz für diese Überlegungen funktioniert.

|  | Mehr als ein Server | Liste der aktuell verbundenen Benutzer abrufen | Persistenkinformationen nach Neustarts | Optimale Leistung |
| --- | --- | --- | --- | --- |
| UserID-Anbieter | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| In-Memory |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Einzelbenutzergruppen | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Permanent, extern | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID-Anbieter

Mit dieser Funktion können Benutzer über eine neue Schnittstelle IUserIdProvider angeben, was die userId auf einer IRequest basiert.

**Der IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Standardmäßig gibt es eine Implementierung, die die `IPrincipal.Identity.Name` des Benutzers als Benutzernamen verwendet. Um dies zu ändern, registrieren Sie Ihre Implementierung beim `IUserIdProvider` globalen Host, wenn Ihre Anwendung gestartet wird:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

Von einem Hub aus können Sie Nachrichten über die folgende API an diese Benutzer senden:

**Senden einer Nachricht an einen bestimmten Benutzer**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>In-Memory-Speicher

Die folgenden Beispiele zeigen, wie Verbindungs- und Benutzerinformationen in einem Wörterbuch gespeichert werden, das im Arbeitsspeicher gespeichert ist. Das Wörterbuch `HashSet` verwendet eine, um die Verbindungs-ID zu speichern. Ein Benutzer kann jederzeit mehr als eine Verbindung zur SignalR-Anwendung haben. Beispielsweise verfügt ein Benutzer, der über mehrere Geräte oder mehr als eine Browserregisterkarte verbunden ist, über mehr als eine Verbindungs-ID.

Wenn die Anwendung heruntergefahren wird, gehen alle Informationen verloren, sie werden jedoch erneut aufgefüllt, wenn die Benutzer ihre Verbindungen wieder herstellen. In-Memory-Speicher funktioniert nicht, wenn Ihre Umgebung mehr als einen Webserver umfasst, da jeder Server über eine separate Sammlung von Verbindungen verfügen würde.

Das erste Beispiel zeigt eine Klasse, die die Zuordnung von Benutzern zu Verbindungen verwaltet. Der Schlüssel für das HashSet ist der Name des Benutzers.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Das nächste Beispiel zeigt, wie die Verbindungszuordnungsklasse von einem Hub aus verwendet wird. Die Instanz der Klasse wird in `_connections`einem Variablennamen gespeichert.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Einzelbenutzergruppen

Sie können eine Gruppe für jeden Benutzer erstellen und dann eine Nachricht an diese Gruppe senden, wenn Sie nur diesen Benutzer erreichen möchten. Der Name jeder Gruppe ist der Name des Benutzers. Wenn ein Benutzer über mehr als eine Verbindung verfügt, wird jede Verbindungs-ID der Gruppe des Benutzers hinzugefügt.

Sie sollten den Benutzer nicht manuell aus der Gruppe entfernen, wenn der Benutzer die Verbindung trennt. Diese Aktion wird automatisch vom SignalR-Framework ausgeführt.

Das folgende Beispiel zeigt, wie Einzelbenutzergruppen implementiert werden.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Permanenter, externer Speicher

In diesem Thema wird gezeigt, wie Sie entweder eine Datenbank oder einen Azure-Tabellenspeicher zum Speichern von Verbindungsinformationen verwenden. Dieser Ansatz funktioniert, wenn Sie über mehrere Webserver verfügen, da jeder Webserver mit demselben Datenrepository interagieren kann. Wenn Ihre Webserver nicht mehr funktionieren `OnDisconnected` oder die Anwendung neu gestartet wird, wird die Methode nicht aufgerufen. Daher ist es möglich, dass Ihr Datenrepository Datensätze für Verbindungs-IDs enthält, die nicht mehr gültig sind. Um diese verwaisten Datensätze zu bereinigen, können Sie jede Verbindung ungültig machen, die außerhalb eines Zeitrahmens erstellt wurde, der für Ihre Anwendung relevant ist. Die Beispiele in diesem Abschnitt enthalten einen Wert für die Nachverfolgung beim Erstellen der Verbindung, zeigen jedoch nicht, wie alte Datensätze bereinigen werden, da Sie dies möglicherweise als Hintergrundprozess tun möchten.

### <a name="database"></a>Datenbank

Die folgenden Beispiele zeigen, wie Verbindungs- und Benutzerinformationen in einer Datenbank beibehalten werden. Sie können jede Datenzugriffstechnologie verwenden; Das folgende Beispiel zeigt jedoch, wie Modelle mit Entity Framework definiert werden. Diese Entitätsmodelle entsprechen Datenbanktabellen und -feldern. Ihre Datenstruktur kann je nach den Anforderungen Ihrer Anwendung erheblich variieren.

Das erste Beispiel zeigt, wie Sie eine Benutzerentität definieren, die vielen Verbindungsentitäten zugeordnet werden kann.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Anschließend können Sie vom Hub aus den Status jeder Verbindung mit dem unten gezeigten Code nachverfolgen.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure Table Storage

Das folgende Azure-Tabellenspeicherbeispiel ähnelt dem Datenbankbeispiel. Sie enthält nicht alle Informationen, die Sie benötigen, um mit Azure Table Storage Service zu beginnen. Weitere Informationen finden Sie unter [Verwenden von Tabellenspeicher aus .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

Das folgende Beispiel zeigt eine Tabellenentität zum Speichern von Verbindungsinformationen. Es partitioniert die Daten nach Benutzername und identifiziert jede Entität anhand der Verbindungs-ID, sodass ein Benutzer jederzeit mehrere Verbindungen haben kann.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

Im Hub verfolgen Sie den Status der Verbindung jedes Benutzers.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
