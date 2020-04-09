---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR Hubs API Guide - Server (C) | Microsoft Docs
author: bradygaster
description: Dieses Dokument bietet eine Einführung in die Programmierung der Serverseite der ASP.NET SignalR Hubs API für SignalR Version 2, wobei Codebeispiele...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675802"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR Hubs API Guide - Server (C')

von [Patrick Fletcher](https://github.com/pfletcher), Tom [Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Dieses Dokument bietet eine Einführung in die Programmierung der Serverseite der ASP.NET SignalR Hubs API für SignalR Version 2, wobei Codebeispiele allgemeine Optionen demonstrieren.
> 
> Mit der SignalR Hubs-API können Sie Remoteprozeduraufrufe (RPCs) von einem Server an verbundene Clients und von Clients an den Server durchführen. Im Servercode definieren Sie Methoden, die von Clients aufgerufen werden können, und rufen Methoden auf, die auf dem Client ausgeführt werden. Im Clientcode definieren Sie Methoden, die vom Server aufgerufen werden können, und rufen Methoden auf, die auf dem Server ausgeführt werden. SignalR kümmert sich um alle Client-to-Server-Anlagen für Sie.
> 
> SignalR bietet auch eine API auf niedrigerer Ebene namens Persistent Connections. Eine Einführung in SignalR, Hubs und persistente Verbindungen finden Sie unter [Einführung in SignalR 2](../getting-started/introduction-to-signalr.md).
> 
> ## <a name="software-versions-used-in-this-topic"></a>In diesem Thema verwendete Softwareversionen
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR Version 2
>   
> 
> 
> ## <a name="topic-versions"></a>Themenversionen
> 
> Informationen zu früheren Versionen von SignalR finden Sie unter [SignalR Ältere Versionen](../older-versions/index.md).
> 
> ## <a name="questions-and-comments"></a>Fragen und Kommentare
> 
> Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir in den Kommentaren am Ende der Seite verbessern könnten. Wenn Sie Fragen haben, die nicht direkt mit dem Tutorial zusammenhängen, können Sie sie [im ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Übersicht

Dieses Dokument enthält folgende Abschnitte:

- [So registrieren Sie SignalR Middleware](#route)

    - [Die /signalr URL](#signalrurl)
    - [Konfigurieren von SignalR-Optionen](#options)
- [Erstellen und Verwenden von Hub-Klassen](#hubclass)

    - [Hub-Objektlebensdauer](#transience)
    - [Camel-Gehäuse von Hub-Namen in JavaScript-Clients](#hubnames)
    - [Mehrere Hubs](#multiplehubs)
    - [Stark typisierte Hubs](#stronglytypedhubs)
- [Definieren von Methoden in der Hub-Klasse, die Clients aufrufen können](#hubmethods)

    - [Kamelgehäuse von Methodennamen in JavaScript-Clients](#methodnames)
    - [Wann asynchron ausgeführt werden soll](#asyncmethods)
    - [Definieren von Überladungen](#overloads)
    - [Melden des Fortschritts aus Hubmethodenaufrufen](#progress)
- [Aufrufen von Clientmethoden aus der Hub-Klasse](#callfromhub)

    - [Auswählen, welche Clients den RPC erhalten](#selectingclients)
    - [Keine Kompilierungszeitüberprüfung für Methodennamen](#dynamicmethodnames)
    - [Bei Fall-in-Sensitive-Methodennameabgleich](#caseinsensitive)
    - [Asynchrone Ausführung](#asyncclient)
- [Verwalten der Gruppenmitgliedschaft aus der Hub-Klasse](#groupsfromhub)

    - [Asynchrone Ausführung von Add- und Remove-Methoden](#asyncgroupmethods)
    - [Gruppenmitgliedschaft Persistenz](#grouppersistence)
    - [Einzelbenutzergruppen](#singleusergroups)
- [Behandeln von Verbindungslebensdauerereignissen in der Hub-Klasse](#connectionlifetime)

    - [Wenn OnConnected, OnDisconnected und OnReconnected aufgerufen werden](#onreconnected)
    - [Anruferstatus nicht bevölkert](#nocallerstate)
- [So erhalten Sie Informationen über den Client aus der Context-Eigenschaft](#contextproperty)
- [Übergeben des Status zwischen Clients und der Hub-Klasse](#passstate)
- [Behandeln von Fehlern in der Hub-Klasse](#handleErrors)
- [Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse](#callfromoutsidehub)

    - [Aufrufen von Clientmethoden](#callingclientsoutsidehub)
    - [Verwalten der Gruppenmitgliedschaft](#managinggroupsoutsidehub)
- [So aktivieren Sie die Ablaufverfolgung](#tracing)
- [Anpassen der Hubs-Pipeline](#hubpipeline)

Eine Dokumentation zum Programmieren von Clients finden Sie in den folgenden Ressourcen:

- [SignalR Hubs API-Handbuch - JavaScript-Client](hubs-api-guide-javascript-client.md)
- [SignalR Hubs API-Leitfaden - .NET Client](hubs-api-guide-net-client.md)

Die Serverkomponenten für SignalR 2 sind nur in .NET 4.5 verfügbar. Server mit .NET 4.0 müssen SignalR v1.x verwenden.

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>So registrieren Sie SignalR Middleware

Um die Route zu definieren, die Clients zum `MapSignalR` Herstellen einer Verbindung mit Ihrem Hub verwenden, rufen Sie die Methode auf, wenn die Anwendung gestartet wird. `MapSignalR`ist eine [Erweiterungsmethode](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) für die `OwinExtensions` Klasse. Das folgende Beispiel zeigt, wie Sie die SignalR Hubs-Route mithilfe einer OWIN-Startklasse definieren.

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

Wenn Sie einer ASP.NET MVC-Anwendung SignalR-Funktionalität hinzufügen, stellen Sie sicher, dass die SignalR-Route vor den anderen Routen hinzugefügt wird. Weitere Informationen finden Sie unter [Tutorial: Erste Schritte mit SignalR 2 und MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>Die /signalr URL

Standardmäßig lautet die Routen-URL, die Clients zum Herstellen einer Verbindung mit Ihrem Hub verwenden, "/signalr". (Verwechseln Sie diese URL nicht mit der URL "/signalr/hubs", die für die automatisch generierte JavaScript-Datei gilt. Weitere Informationen zum generierten Proxy finden Sie unter [SignalR Hubs API Guide - JavaScript Client - Der generierte Proxy und was er für Sie tut](hubs-api-guide-javascript-client.md#genproxy).)

Es kann außergewöhnliche Umstände geben, die diese Basis-URL nicht für SignalR nutzbar machen. Sie haben z. B. einen Ordner mit dem Namen *Signalr* in Ihrem Projekt und möchten den Namen nicht ändern. In diesem Fall können Sie die Basis-URL ändern, wie in den folgenden Beispielen gezeigt (ersetzen Sie "/signalr" im Beispielcode durch Ihre gewünschte URL).

**Servercode, der die URL angibt**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**JavaScript-Clientcode, der die URL angibt (mit dem generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**JavaScript-Clientcode, der die URL angibt (ohne den generierten Proxy)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**.NET-Clientcode, der die URL angibt**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>Konfigurieren von SignalR-Optionen

Überladen der `MapSignalR` Methode ermöglichen es Ihnen, eine benutzerdefinierte URL, einen benutzerdefinierten Abhängigkeitslöser und die folgenden Optionen anzugeben:

- Aktivieren Sie domänenübergreifende Anrufe mit CORS oder JSONP von Browserclients aus.

    Wenn der Browser eine `http://contoso.com`Seite aus lädt, befindet sich die `http://contoso.com/signalr`SignalR-Verbindung in derselben Domäne unter . Wenn die `http://contoso.com` Seite von `http://fabrikam.com/signalr`eine Verbindung zu herstellt, handelt es sich um eine domänenübergreifende Verbindung. Aus Sicherheitsgründen sind domänenübergreifende Verbindungen standardmäßig deaktiviert. Weitere Informationen finden Sie unter [ASP.NET SignalR Hubs API Guide - JavaScript Client - So stellen Sie eine domänenübergreifende Verbindung her.](hubs-api-guide-javascript-client.md#crossdomain)
- Aktivieren Sie detaillierte Fehlermeldungen.

    Wenn Fehler auftreten, besteht das Standardverhalten von SignalR darin, eine Benachrichtigung ohne Details zu den Geschehnissen an Clients zu senden. Das Senden detaillierter Fehlerinformationen an Clients wird in der Produktion nicht empfohlen, da böswillige Benutzer die Informationen möglicherweise bei Angriffen auf Ihre Anwendung verwenden können. Zur Fehlerbehebung können Sie diese Option verwenden, um vorübergehend eine informativere Fehlerberichterstattung zu aktivieren.
- Deaktivieren Sie automatisch generierte JavaScript-Proxydateien.

    Standardmäßig wird als Antwort auf die URL "/signalr/hubs" eine JavaScript-Datei mit Proxys für Ihre Hub-Klassen generiert. Wenn Sie die JavaScript-Proxys nicht verwenden möchten oder wenn Sie diese Datei manuell generieren und auf eine physische Datei in Ihren Clients verweisen möchten, können Sie diese Option verwenden, um die Proxygenerierung zu deaktivieren. Weitere Informationen finden Sie unter [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).

Das folgende Beispiel zeigt, wie Sie die SignalR-Verbindungs-URL und diese Optionen in einem Aufruf der `MapSignalR` Methode angeben. Um eine benutzerdefinierte URL anzugeben, ersetzen Sie "/signalr" im Beispiel durch die URL, die Sie verwenden möchten.

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>Erstellen und Verwenden von Hub-Klassen

Um einen Hub zu erstellen, erstellen Sie eine Klasse, die von [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)abstammt. Das folgende Beispiel zeigt eine einfache Hub-Klasse für eine Chatanwendung.

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

In diesem Beispiel kann ein `NewContosoChatMessage` verbundener Client die Methode aufrufen, und wenn dies der Fall ist, werden die empfangenen Daten an alle verbundenen Clients übertragen.

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>Hub-Objektlebensdauer

Sie instanziieren die Hub-Klasse nicht oder rufen ihre Methoden nicht über Ihren eigenen Code auf dem Server auf. alles, was von der SignalR Hubs-Pipeline für Sie erledigt wird. SignalR erstellt jedes Mal eine neue Instanz Ihrer Hub-Klasse, wenn es einen Hub-Vorgang verarbeiten muss, z. B. wenn ein Client eine Verbindung herstellt, die Verbindung trennt oder einen Methodenaufruf an den Server ausführt.

Da Instanzen der Hub-Klasse vorübergehend sind, können Sie sie nicht verwenden, um den Status von einem Methodenaufruf zum nächsten beizubehalten. Jedes Mal, wenn der Server einen Methodenaufruf von einem Client empfängt, verarbeitet eine neue Instanz Ihrer Hub-Klasse die Nachricht. Um den Status über mehrere Verbindungen und Methodenaufrufe beizubehalten, verwenden Sie eine andere Methode, z. B. eine `Hub`Datenbank oder eine statische Variable für die Hub-Klasse oder eine andere Klasse, die nicht von ableitet. Wenn Sie Daten im Arbeitsspeicher beibehalten, wird die Daten mithilfe einer Methode wie einer statischen Variable in der Hub-Klasse verloren gehen, wenn die App-Domäne wiederverwendet wird.

Wenn Sie Nachrichten von Ihrem eigenen Code an Clients senden möchten, der außerhalb der Hub-Klasse ausgeführt wird, können Sie dies nicht tun, indem Sie eine Hub-Klasseninstanz instanziieren, aber Sie können dies tun, indem Sie einen Verweis auf das SignalR-Kontextobjekt für Ihre Hub-Klasse abrufen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse.](#callfromoutsidehub)

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>Camel-Gehäuse von Hub-Namen in JavaScript-Clients

Standardmäßig verweisen JavaScript-Clients auf Hubs, indem sie eine Kamel-Case-Version des Klassennamens verwenden. SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann. Das vorherige Beispiel wird `contosoChatHub` wie in JavaScript-Code bezeichnet.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

Wenn Sie einen anderen Namen für Clients angeben `HubName` möchten, fügen Sie das Attribut hinzu. Wenn Sie `HubName` ein Attribut verwenden, gibt es auf JavaScript-Clients keine Namensänderung in Kamelfall.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>Mehrere Hubs

Sie können mehrere Hubklassen in einer Anwendung definieren. Wenn Sie dies tun, wird die Verbindung freigegeben, aber Gruppen sind getrennt:

- Alle Clients verwenden dieselbe URL, um eine SignalR-Verbindung mit Ihrem Dienst herzustellen ("/signalr" oder Ihre benutzerdefinierte URL, falls Sie eine angegeben haben), und diese Verbindung wird für alle Hubs verwendet, die vom Dienst definiert werden.

    Es gibt keinen Leistungsunterschied für mehrere Hubs im Vergleich zum Definieren aller Hub-Funktionen in einer einzelnen Klasse.
- Alle Hubs erhalten dieselben HTTP-Anforderungsinformationen.

    Da alle Hubs dieselbe Verbindung haben, erhalten die Server nur die Informationen über HTTP-Anforderung, die er erhält, die ursprüngliche HTTP-Anforderung, die die SignalR-Verbindung herstellt. Wenn Sie die Verbindungsanforderung verwenden, um Informationen vom Client an den Server zu übergeben, indem Sie eine Abfragezeichenfolge angeben, können Sie keine unterschiedlichen Abfragezeichenfolgen an verschiedene Hubs bereitstellen. Alle Hubs erhalten die gleichen Informationen.
- Die generierte JavaScript-Proxydatei enthält Proxys für alle Hubs in einer Datei.

    Weitere Informationen zu JavaScript-Proxys finden Sie unter [SignalR Hubs API Guide - JavaScript Client - Der generierte Proxy und was er für Sie tut.](hubs-api-guide-javascript-client.md#genproxy)
- Gruppen werden in Hubs definiert.

    In SignalR können Sie benannte Gruppen definieren, die an Teilmengen verbundener Clients übertragen werden sollen. Gruppen werden für jeden Hub separat verwaltet. Eine Gruppe mit dem Namen "Administratoren" würde z. B. einen Satz von Clients für Ihre `ContosoChatHub` `StockTickerHub` Klasse enthalten, und derselbe Gruppenname würde sich auf einen anderen Satz von Clients für Ihre Klasse beziehen.

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Stark typisierte Hubs

Um eine Schnittstelle für Ihre Hub-Methoden zu definieren, auf die Ihr Client verweisen kann `Hub<T>` (und Intellisense für `Hub`Ihre Hub-Methoden aktivieren), leiten Sie Ihren Hub von (in SignalR 2.1 eingeführt) ab und nicht:

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>Definieren von Methoden in der Hub-Klasse, die Clients aufrufen können

Um eine Methode auf dem Hub verfügbar zu machen, die vom Client aus aufrufbar sein soll, deklarieren Sie eine öffentliche Methode, wie in den folgenden Beispielen gezeigt.

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

Sie können einen Rückgabetyp und Parameter, einschließlich komplexer Typen und Arrays, wie in jeder C-Methode angeben. Alle Daten, die Sie in Parametern erhalten oder an den Aufrufer zurückgeben, werden mithilfe von JSON zwischen dem Client und dem Server übermittelt, und SignalR verarbeitet die Bindung komplexer Objekte und Arrays von Objekten automatisch.

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>Kamelgehäuse von Methodennamen in JavaScript-Clients

Standardmäßig verweisen JavaScript-Clients auf Hub-Methoden, indem sie eine Kamel-Case-Version des Methodennamens verwenden. SignalR nimmt diese Änderung automatisch vor, sodass JavaScript-Code JavaScript-Konventionen entsprechen kann.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

Wenn Sie einen anderen Namen für Clients angeben `HubMethodName` möchten, fügen Sie das Attribut hinzu.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>Wann asynchron ausgeführt werden soll

Wenn die Methode lang andauernd ausgeführt wird oder arbeiten muss, die warten würde, z. B. eine Datenbanksuche oder einen Webdienstaufruf, machen Sie die `T` Hub-Methode asynchron, indem Sie ein [Task-Objekt](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (anstelle der `void` Rückgabe) oder das [Task&lt;&gt; T-Objekt](https://msdn.microsoft.com/library/dd321424.aspx) (anstelle des Rückgabetyps) zurückgeben. Wenn Sie `Task` ein Objekt von der Methode zurückgeben, wartet SignalR, bis der `Task` abgeschlossen ist, und sendet dann das entpackte Ergebnis an den Client zurück, sodass es keinen Unterschied in der Art und Weise gibt, wie Sie den Methodenaufruf im Client codieren.

Wenn Sie eine Hub-Methode asynchron machen, wird vermieden, dass die Verbindung blockiert wird, wenn sie den WebSocket-Transport verwendet. Wenn eine Hub-Methode synchron ausgeführt wird und der Transport WebSocket ist, werden nachfolgende Aufrufe von Methoden auf dem Hub vom gleichen Client blockiert, bis die Hub-Methode abgeschlossen ist.

Das folgende Beispiel zeigt dieselbe Methode, die für die Synchron- oder Asynchronausführung codiert ist, gefolgt von JavaScript-Clientcode, der zum Aufrufen einer der beiden Versionen funktioniert.

**Synchrone**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**Asynchronen**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

Weitere Informationen zur Verwendung asynchroner Methoden in ASP.NET 4.5 finden Sie unter [Verwenden asynchroner Methoden in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="overloads"></a>

### <a name="defining-overloads"></a>Definieren von Überladungen

Wenn Sie Überladungen für eine Methode definieren möchten, muss die Anzahl der Parameter in jeder Überladung unterschiedlich sein. Wenn Sie eine Überlast nur durch die Angabe verschiedener Parametertypen unterscheiden, wird Ihre Hub-Klasse kompiliert, aber der SignalR-Dienst löst zur Laufzeit eine Ausnahme aus, wenn Clients versuchen, eine der Überladungen aufzurufen.

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>Melden des Fortschritts aus Hubmethodenaufrufen

SignalR 2.1 unterstützt das in .NET 4.5 eingeführte [Fortschrittsberichtsmuster.](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) Um die Fortschrittsberichterstattung zu implementieren, definieren Sie einen `IProgress<T>` Parameter für Ihre Hubmethode, auf den Ihr Client zugreifen kann:

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

Beim Schreiben einer lang andauernden Servermethode ist es wichtig, ein asynchrones Programmiermuster wie Async/ Await zu verwenden, anstatt den Hubthread zu blockieren.

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>Aufrufen von Clientmethoden aus der Hub-Klasse

Um Clientmethoden vom Server aufzurufen, verwenden Sie die `Clients` Eigenschaft in einer Methode in Ihrer Hubklasse. Das folgende Beispiel zeigt `addNewMessageToPage` Servercode, der alle verbundenen Clients aufruft, und Clientcode, der die Methode in einem JavaScript-Client definiert.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

Das Aufrufen einer Clientmethode ist ein asynchroner Vorgang und gibt eine `Task`zurück. Verwenden Sie `await`:

* So stellen Sie sicher, dass die Nachricht fehlerfrei gesendet wird. 
* So aktivieren Sie Abfangen und Behandeln von Fehlern in einem Try-Catch-Block.

**JavaScript-Client mit generiertem Proxy**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

Sie können keinen Rückgabewert von einer Clientmethode abrufen. Syntax, `int x = Clients.All.add(1,1)` wie sie nicht funktioniert.

Sie können komplexe Typen und Arrays für die Parameter angeben. Im folgenden Beispiel wird ein komplexer Typ an den Client in einem Methodenparameter übergeben.

**Servercode, der eine Clientmethode mithilfe eines komplexen Objekts aufruft**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**Servercode, der das komplexe Objekt definiert**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>Auswählen, welche Clients den RPC erhalten

Die Clients-Eigenschaft gibt ein [HubConnectionContext-Objekt](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) zurück, das mehrere Optionen zum Angeben bereitstellt, welche Clients die RPC empfangen:

- Alle verbundenen Clients.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- Nur der aufrufende Client.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- Alle Clients mit Ausnahme des aufrufenden Clients.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- Ein bestimmter Client, der durch die Verbindungs-ID identifiziert wurde.

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    Dieses Beispiel `addContosoChatMessageToPage` ruft den aufrufenden Client auf `Clients.Caller`und hat den gleichen Effekt wie die Verwendung von .
- Alle verbundenen Clients mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- Alle verbundenen Clients in einer angegebenen Gruppe.

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme des aufrufenden Clients.

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- Ein bestimmter Benutzer, der durch userId identifiziert wird.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    Standardmäßig ist `IPrincipal.Identity.Name`dies , aber dies kann durch [Registrieren einer Implementierung von IUserIdProvider beim globalen Host](mapping-users-to-connections.md#IUserIdProvider)geändert werden.
- Alle Clients und Gruppen in einer Liste von Verbindungs-IDs.

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- Eine Liste von Gruppen.

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- Ein Benutzer nach Namen.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- Eine Liste der Benutzernamen (eingeführt in SignalR 2.1).

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>Keine Kompilierungszeitüberprüfung für Methodennamen

Der von Ihnen angegebene Methodenname wird als dynamisches Objekt interpretiert, was bedeutet, dass es keine IntelliSense- oder Kompilierungszeitüberprüfung dafür gibt. Der Ausdruck wird zur Laufzeit ausgewertet. Wenn der Methodenaufruf ausgeführt wird, sendet SignalR den Methodennamen und die Parameterwerte an den Client, und wenn der Client über eine Methode verfügt, die dem Namen entspricht, wird diese Methode aufgerufen, und die Parameterwerte werden an ihn übergeben. Wenn auf dem Client keine Übereinstimmende Methode gefunden wird, wird kein Fehler ausgelöst. Informationen zum Format der Daten, die SignalR beim Aufrufen einer Clientmethode an den Client überträgt, finden Sie unter [Einführung in SignalR](../getting-started/introduction-to-signalr.md).

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>Bei Fall-in-Sensitive-Methodennameabgleich

Bei der Zuordnung zum Methodennamen wird die Groß-/Kleinschreibung nicht berücksichtigt. Auf dem `Clients.All.addContosoChatMessageToPage` Server wird `AddContosoChatMessageToPage`z. B. ausgeführt , `addcontosochatmessagetopage`, oder `addContosoChatMessageToPage` auf dem Client.

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>Asynchrone Ausführung

Die Methode, die Sie aufrufen, wird asynchron ausgeführt. Jeder Code, der nach einem Methodenaufruf an einen Client kommt, wird sofort ausgeführt, ohne darauf zu warten, dass SignalR die Übertragung von Daten an Clients beendet, es sei denn, Sie geben an, dass die nachfolgenden Codezeilen auf den Abschluss der Methode warten sollen. Das folgende Codebeispiel zeigt, wie zwei Clientmethoden sequenziell ausgeführt werden.

**Verwenden von Await (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

Wenn Sie `await` warten, bis eine Clientmethode abgeschlossen ist, bevor die nächste Codezeile ausgeführt wird, bedeutet dies nicht, dass Clients die Nachricht tatsächlich empfangen, bevor die nächste Codezeile ausgeführt wird. "Abschluss" eines Clientmethodenaufrufs bedeutet nur, dass SignalR alles Notwendige getan hat, um die Nachricht zu senden. Wenn Sie überprüfen müssen, ob Clients die Nachricht erhalten haben, müssen Sie diesen Mechanismus selbst programmieren. Sie können z. `MessageReceived` B. eine Methode auf `addContosoChatMessageToPage` dem Hub codieren, und in der Methode auf dem Client können Sie aufrufen, `MessageReceived` nachdem Sie die Arbeit, die Sie auf dem Client erledigen müssen, durchgeführt haben. Im `MessageReceived` Hub können Sie unabhängig davon tun, was vom tatsächlichen Clientempfang und der Verarbeitung des ursprünglichen Methodenaufrufs abhängt.

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>Verwenden einer Zeichenfolgenvariablen als Methodenname

Wenn Sie eine Client-Methode aufrufen möchten, indem Sie `Clients.All` eine `Clients.Others`Zeichenfolgenvariable als Methodennamen verwenden, umwerfen (oder , `Clients.Caller`, usw.) an `IClientProxy` und rufen Sie dann [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)auf.

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>Verwalten der Gruppenmitgliedschaft aus der Hub-Klasse

Gruppen in SignalR stellen eine Methode zum Senden von Nachrichten an bestimmte Teilmengen verbundener Clients bereit. Eine Gruppe kann eine beliebige Anzahl von Clients haben, und ein Client kann Mitglied einer beliebigen Anzahl von Gruppen sein.

Um die Gruppenmitgliedschaft zu verwalten, verwenden `Groups` Sie die Methoden [Hinzufügen](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) und [Entfernen,](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) die von der Eigenschaft der Hub-Klasse bereitgestellt werden. Das folgende Beispiel `Groups.Add` `Groups.Remove` zeigt die und Methoden, die in Hub-Methoden verwendet werden, die vom Clientcode aufgerufen werden, gefolgt von JavaScript-Clientcode, der sie aufruft.

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**JavaScript-Client mit generiertem Proxy**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

Sie müssen keine Gruppen explizit erstellen. Tatsächlich wird eine Gruppe automatisch erstellt, wenn Sie ihren `Groups.Add`Namen zum ersten Mal in einem Aufruf von angeben, und sie wird gelöscht, wenn Sie die letzte Verbindung aus der Mitgliedschaft in ihr entfernen.

Es gibt keine API zum Abrufen einer Gruppenmitgliedschaftsliste oder einer Liste von Gruppen. SignalR sendet Nachrichten an Clients und Gruppen basierend auf einem [Pub/Untermodell](http://en.wikipedia.org/wiki/Publish/subscribe), und der Server führt keine Listen von Gruppen oder Gruppenmitgliedschaften. Dies trägt zur Maximierung der Skalierbarkeit bei, da jedes Mal, wenn Sie einen Knoten zu einer Webfarm hinzufügen, jeder Status, den SignalR verwaltet, an den neuen Knoten weitergegeben werden muss.

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Asynchrone Ausführung von Add- und Remove-Methoden

Die `Groups.Add` `Groups.Remove` und-Methoden werden asynchron ausgeführt. Wenn Sie einer Gruppe einen Client hinzufügen und sofort mithilfe der Gruppe eine Nachricht an `Groups.Add` den Client senden möchten, müssen Sie sicherstellen, dass die Methode zuerst abgeschlossen wird. Das folgende Codebeispiel zeigt, wie Sie dies tun.

**Hinzufügen eines Clients zu einer Gruppe und anschließende Übermittlung dieses Clients**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>Gruppenmitgliedschaft Persistenz

SignalR verfolgt Verbindungen, nicht Benutzer, also wenn Sie möchten, dass sich ein Benutzer jedes Mal `Groups.Add` in derselben Gruppe aufhält, wenn der Benutzer eine Verbindung herstellt, müssen Sie jedes Mal anrufen, wenn der Benutzer eine neue Verbindung herstellt.

Nach einem vorübergehenden Verbindungsverlust kann SignalR die Verbindung manchmal automatisch wiederherstellen. In diesem Fall stellt SignalR dieselbe Verbindung wieder her, stellt keine neue Verbindung her, sodass die Gruppenmitgliedschaft des Clients automatisch wiederhergestellt wird. Dies ist auch dann möglich, wenn die temporäre Unterbrechung das Ergebnis eines Serverneustarts oder -fehlers ist, da der Verbindungsstatus für jeden Client, einschließlich der Gruppenmitgliedschaften, auf den Client gerundet wird. Wenn ein Server ausfällt und durch einen neuen Server ersetzt wird, bevor die Verbindung auftritt, kann ein Client automatisch eine Verbindung mit dem neuen Server herstellen und sich erneut in Gruppen registrieren, denen er angehört.

Wenn eine Verbindung nach einem Verbindungsverlust nicht automatisch wiederhergestellt werden kann, wenn die Verbindung unterbrochen wird oder wenn der Client die Verbindung trennt (z. B. wenn ein Browser zu einer neuen Seite navigiert), gehen Gruppenmitgliedschaften verloren. Das nächste Mal, wenn der Benutzer eine Verbindung herstellt, wird eine neue Verbindung hergestellt. Um Gruppenmitgliedschaften beizubehalten, wenn derselbe Benutzer eine neue Verbindung herstellt, muss Ihre Anwendung die Zuordnungen zwischen Benutzern und Gruppen nachverfolgen und Gruppenmitgliedschaften jedes Mal wiederherstellen, wenn ein Benutzer eine neue Verbindung herstellt.

Weitere Informationen zu Verbindungen und Wiederverbindungen finden Sie weiter unten in diesem Thema unter Behandeln von [Verbindungslebensdauerereignissen in der Hub-Klasse.](#connectionlifetime)

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>Einzelbenutzergruppen

Anwendungen, die SignalR verwenden, müssen in der Regel die Zuordnungen zwischen Benutzern und Verbindungen nachverfolgen, um zu wissen, welcher Benutzer eine Nachricht gesendet hat und welche Benutzer eine Nachricht empfangen sollen. Gruppen werden in einem der beiden häufig verwendeten Muster verwendet, um dies zu tun.

- Einzelbenutzergruppen.

    Sie können den Benutzernamen als Gruppennamen angeben und der Gruppe jedes Mal die aktuelle Verbindungs-ID hinzufügen, wenn der Benutzer eine Verbindung herstellt oder erneut eine Verbindung herstellt. So senden Sie Nachrichten an den Benutzer, den Sie an die Gruppe senden. Ein Nachteil dieser Methode besteht darin, dass die Gruppe Ihnen keine Möglichkeit bietet, herauszufinden, ob der Benutzer online oder offline ist.
- Nachverfolgen von Zuordnungen zwischen Benutzernamen und Verbindungs-IDs.

    Sie können eine Zuordnung zwischen jedem Benutzernamen und einer oder mehreren Verbindungs-IDs in einem Wörterbuch oder einer Datenbank speichern und die gespeicherten Daten jedes Mal aktualisieren, wenn der Benutzer eine Verbindung herstellt oder die Verbindung trennt. Um Nachrichten an den Benutzer zu senden, geben Sie die Verbindungs-IDs an. Ein Nachteil dieser Methode ist, dass sie mehr Speicher benötigt.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>Behandeln von Verbindungslebensdauerereignissen in der Hub-Klasse

Typische Gründe für die Behandlung von Ereignissen mit der Verbindungslebensdauer sind, nachzuverfolgen, ob ein Benutzer verbunden ist oder nicht, und die Zuordnung zwischen Benutzernamen und Verbindungs-IDs nachzuverfolgen. Um Ihren eigenen Code auszuführen, wenn Clients `OnConnected` `OnDisconnected`eine `OnReconnected` Verbindung herstellen oder trennen, überschreiben Sie die , und die virtuellen Methoden der Hub-Klasse, wie im folgenden Beispiel gezeigt.

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>Wenn OnConnected, OnDisconnected und OnReconnected aufgerufen werden

Jedes Mal, wenn ein Browser zu einer neuen Seite navigiert, muss `OnDisconnected` eine neue `OnConnected` Verbindung hergestellt werden, was bedeutet, dass SignalR die Methode nach der Methode ausführt. SignalR erstellt immer eine neue Verbindungs-ID, wenn eine neue Verbindung hergestellt wird.

Die `OnReconnected` Methode wird aufgerufen, wenn die Verbindung vorübergehend unterbrochen wurde, von der SignalR automatisch wiederhergestellt werden kann, z. B. wenn ein Kabel vorübergehend getrennt und wieder verbunden wird, bevor die Verbindung unterbrochen wird. Die `OnDisconnected` Methode wird aufgerufen, wenn der Client getrennt wird und SignalR die Verbindung nicht automatisch wieder herstellen kann, z. B. wenn ein Browser zu einer neuen Seite navigiert. Daher ist `OnConnected`eine mögliche Abfolge von `OnReconnected`Ereignissen `OnDisconnected`für einen bestimmten Client , ; oder `OnConnected` `OnDisconnected`, . Die Sequenz `OnConnected`, `OnDisconnected` `OnReconnected` wird für eine bestimmte Verbindung nicht angezeigt.

Die `OnDisconnected` Methode wird in einigen Szenarien nicht aufgerufen, z. B. wenn ein Server ausfällt oder die App-Domäne recycelt wird. Wenn ein anderer Server online geht oder die App-Domäne ihre Wiederverwertung abgeschlossen `OnReconnected` hat, können einige Clients möglicherweise die Verbindung wieder herstellen und das Ereignis ausschalten.

Weitere Informationen finden Sie [unter Grundlegendes zum Verständnis und Behandeln von Verbindungslebensdauerereignissen in SignalR](handling-connection-lifetime-events.md).

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>Anruferstatus nicht bevölkert

Die Ereignishandlermethoden für die Verbindungslebensdauer werden vom Server aufgerufen, `state` was bedeutet, dass jeder Status, den Sie in das Objekt auf dem Client setzen, nicht in der `Caller` Eigenschaft auf dem Server aufgefüllt wird. Weitere Informationen `state` zum Objekt `Caller` und zur Eigenschaft finden Sie weiter unten in diesem Thema [unter Übergeben des Status zwischen Clients und der Hub-Klasse.](#passstate)

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>So erhalten Sie Informationen über den Client aus der Context-Eigenschaft

Um Informationen über den Client `Context` abzubekommen, verwenden Sie die Eigenschaft der Hub-Klasse. Die `Context` Eigenschaft gibt ein [HubCallerContext-Objekt](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) zurück, das Zugriff auf die folgenden Informationen bietet:

- Die Verbindungs-ID des aufrufenden Clients.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    Die Verbindungs-ID ist eine GUID, die von SignalR zugewiesen wird (Sie können den Wert nicht in Ihrem eigenen Code angeben). Für jede Verbindung gibt es eine Verbindungs-ID, und die gleiche Verbindungs-ID wird von allen Hubs verwendet, wenn Sie mehrere Hubs in Ihrer Anwendung haben.
- HTTP-Headerdaten.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    Sie können auch HTTP-Header von `Context.Headers`abrufen. Der Grund für mehrere Verweise auf `Context.Headers` dasselbe ist, dass zuerst erstellt wurde, die `Context.Request` Eigenschaft wurde später hinzugefügt und `Context.Headers` wurde aus Gründen der Abwärtskompatibilität beibehalten.
- Abfragezeichenfolgendaten.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    Sie können auch Abfragezeichenfolgendaten aus `Context.QueryString`abrufen.

    Die Abfragezeichenfolge, die Sie in dieser Eigenschaft abrufen, ist diejenige, die mit der HTTP-Anforderung verwendet wurde, die die SignalR-Verbindung hergestellt hat. Sie können Abfragezeichenfolgenparameter im Client hinzufügen, indem Sie die Verbindung konfigurieren, was eine bequeme Möglichkeit ist, Daten über den Client vom Client an den Server zu übergeben. Das folgende Beispiel zeigt eine Möglichkeit zum Hinzufügen einer Abfragezeichenfolge in einem JavaScript-Client, wenn Sie den generierten Proxy verwenden.

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    Weitere Informationen zum Festlegen von Abfragezeichenfolgenparametern finden Sie in den API-Leitfäden für die [JavaScript-](hubs-api-guide-javascript-client.md) und [.NET-Clients.](hubs-api-guide-net-client.md)

    Sie können die Transportmethode, die für die Verbindung verwendet wird, in den Abfragezeichenfolgendaten sowie einige andere Werte finden, die intern von SignalR verwendet werden:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    Der Wert `transportMethod` von ist "webSockets", "serverSentEvents", "foreverFrame" oder "longPolling". Beachten Sie, dass Sie `OnConnected` bei überprüfung dieses Werts in der Ereignishandlermethode in einigen Szenarien zunächst einen Transportwert erhalten, der nicht die endgültige ausgehandelte Transportmethode für die Verbindung ist. In diesem Fall löst die Methode eine Ausnahme aus und wird später erneut aufgerufen, wenn die endgültige Transportmethode festgelegt ist.
- Cookies.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    Sie können auch `Context.RequestCookies`Cookies von erhalten.
- Benutzerinformationen.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- Das HttpContext-Objekt für die Anforderung :

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    Verwenden Sie diese `HttpContext.Current` Methode, `HttpContext` anstatt das Objekt für die SignalR-Verbindung abzusuchen.

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>Übergeben des Status zwischen Clients und der Hub-Klasse

Der Clientproxy `state` stellt ein Objekt bereit, in dem Sie Daten speichern können, die mit jedem Methodenaufruf an den Server übertragen werden sollen. Auf dem Server können Sie `Clients.Caller` auf diese Daten in der Eigenschaft in Hub-Methoden zugreifen, die von Clients aufgerufen werden. Die `Clients.Caller` Eigenschaft wird für die Verbindungslebensdauerereignishandlermethoden `OnConnected`, `OnDisconnected`und `OnReconnected`nicht aufgefüllt.

Das Erstellen oder `state` Aktualisieren von `Clients.Caller` Daten im Objekt und in der Eigenschaft funktioniert in beide Richtungen. Sie können Werte auf dem Server aktualisieren und diese an den Client zurückübergaben.

Das folgende Beispiel zeigt JavaScript-Clientcode, der den Status für die Übertragung an den Server mit jedem Methodenaufruf speichert.

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

Das folgende Beispiel zeigt den entsprechenden Code in einem .NET-Client.

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

In Ihrer Hub-Klasse können Sie `Clients.Caller` auf diese Daten in der Eigenschaft zugreifen. Das folgende Beispiel zeigt Code, der den im vorherigen Beispiel genannten Status abruft.

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> Dieser Mechanismus für den persistenten Zustand ist nicht für große `state` Datenmengen vorgesehen, da alles, was Sie in die oder `Clients.Caller` Eigenschaft legen, mit jedem Methodenaufruf rund ausgelöst wird. Es ist nützlich für kleinere Elemente wie Benutzernamen oder Leistungsindikatoren.

In VB.NET oder in einem stark typisierten Hub kann auf das `Clients.Caller`Aufruferstatusobjekt nicht über zugegriffen werden. verwenden `Clients.CallerState` (in SignalR 2.1 eingeführt):

**Verwenden von CallerState in C #**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**Verwenden von CallerState in Visual Basic**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>Behandeln von Fehlern in der Hub-Klasse

Um Fehler zu behandeln, die in Ihren Hub-Klassenmethoden auftreten, stellen Sie zunächst sicher, dass Sie `await`Ausnahmen von asynchronen Vorgängen (z. B. Aufrufen von Clientmethoden) mithilfe von "beachten". Verwenden Sie dann eine oder mehrere der folgenden Methoden:

- Umschließen Sie den Methodencode in try-catch-Blöcke, und protokollieren Sie das Ausnahmeobjekt. Für Debugging-Zwecke können Sie die Ausnahme an den Client senden, aber aus Sicherheitsgründen wird das Senden detaillierter Informationen an Clients in der Produktion nicht empfohlen.
- Erstellen Sie ein Hubs-Pipelinemodul, das die [OnIncomingError-Methode](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) verarbeitet. Das folgende Beispiel zeigt ein Pipelinemodul, das Fehler protokolliert, gefolgt von Code in Startup.cs, der das Modul in die Hubs-Pipeline einfügt.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- Verwenden `HubException` Sie die Klasse (eingeführt in SignalR 2). Dieser Fehler kann von jedem Hubaufruf ausgelöst werden. Der `HubError` Konstruktor nimmt eine Zeichenfolgennachricht und ein Objekt zum Speichern zusätzlicher Fehlerdaten. SignalR serialisiert die Ausnahme automatisch und sendet sie an den Client, wo sie zum Ablehnen oder Faildes des Hub-Methodenaufrufs verwendet wird.

    Die folgenden Codebeispiele veranschaulichen, wie sie während `HubException` eines Hub-Aufrufs ausgelöst werden und wie die Ausnahme auf JavaScript- und .NET-Clients behandelt wird.

    **Servercode zum Demonstrieren der HubException-Klasse**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **JavaScript-Clientcode demonstriert Reaktion auf das Auslösen einer HubException in einem Hub**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **.NET-Clientcode demonstriert Antwort auf das Auslösen einer HubException in einem Hub**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

Weitere Informationen zu Hub-Pipelinemodulen finden Sie weiter unten in diesem Thema unter [Anpassen der Hubs-Pipeline.](#hubpipeline)

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>So aktivieren Sie die Ablaufverfolgung

Um die serverseitige Ablaufverfolgung zu aktivieren, fügen Sie der Datei Web.config ein system.diagnostics-Element hinzu, wie in diesem Beispiel gezeigt:

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Wenn Sie die Anwendung in Visual Studio ausführen, können Sie die Protokolle im **Ausgabefenster** anzeigen.

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>Aufrufen von Clientmethoden und Verwalten von Gruppen außerhalb der Hub-Klasse

Um Clientmethoden aus einer anderen Klasse als Ihrer Hub-Klasse aufzurufen, rufen Sie einen Verweis auf das SignalR-Kontextobjekt für den Hub ab, und verwenden Sie diese, um Methoden für den Client oder Verwaltungsgruppen aufzurufen.

Die folgende `StockTicker` Beispielklasse ruft das Kontextobjekt ab, speichert es in einer Instanz der Klasse, speichert die Klasseninstanz in `updateStockPrice` einer statischen Eigenschaft und verwendet `StockTickerHub`den Kontext aus der singleton-Klasseninstanz, um die Methode auf Clients aufzurufen, die mit einem Hub mit dem Namen verbunden sind.

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

Wenn Sie den Kontext mehrmals in einem langlebigen Objekt verwenden müssen, erhalten Sie den Verweis einmal und speichern Sie ihn, anstatt ihn jedes Mal wieder zu erhalten. Durch das einmalige Abrufen des Kontexts wird sichergestellt, dass SignalR Nachrichten in derselben Reihenfolge an Clients sendet, in der Ihre Hubmethoden Clientmethodenaufrufen machen. Ein Tutorial zur Verwendung des SignalR-Kontexts für einen Hub finden Sie unter [ServerBroadcast mit ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>Aufrufen von Clientmethoden

Sie können angeben, welche Clients die RPC empfangen sollen, sie haben jedoch weniger Optionen als beim Aufruf von einer Hubklasse. Der Grund dafür ist, dass der Kontext keinem bestimmten Aufruf von einem Client zugeordnet ist, sodass methoden, die Kenntnisse der aktuellen Verbindungs-ID erfordern, wie z. `Clients.Others`B. oder `Clients.Caller`, oder `Clients.OthersInGroup`, nicht verfügbar sind. Die folgenden Optionen sind verfügbar:

- Alle verbundenen Clients.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- Ein bestimmter Client, der durch die Verbindungs-ID identifiziert wurde.

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- Alle verbundenen Clients mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- Alle verbundenen Clients in einer angegebenen Gruppe.

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- Alle verbundenen Clients in einer angegebenen Gruppe mit Ausnahme der angegebenen Clients, die durch die Verbindungs-ID identifiziert werden.

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

Wenn Sie ihre Nicht-Hub-Klasse von Methoden in Ihrer Hub-Klasse aufrufen, können `Clients.Client`Sie `Clients.AllExcept`die `Clients.Group` aktuelle `Clients.Caller` `Clients.Others`Verbindungs-ID übergeben und diese mit verwenden, oder , oder , um , oder `Clients.OthersInGroup`zu simulieren. Im folgenden Beispiel `MoveShapeHub` übergibt die Klasse `Broadcaster` die Verbindungs-ID an die Klasse, damit die `Broadcaster` Klasse simulieren `Clients.Others`kann.

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>Verwalten der Gruppenmitgliedschaft

Zum Verwalten von Gruppen haben Sie die gleichen Optionen wie in einer Hub-Klasse.

- Hinzufügen eines Clients zu einer Gruppe

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- Entfernen eines Clients aus einer Gruppe

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>Anpassen der Hubs-Pipeline

Mit SignalR können Sie Ihren eigenen Code in die Hub-Pipeline einfügen. Das folgende Beispiel zeigt ein benutzerdefiniertes Hubpipelinemodul, das jeden eingehenden Methodenaufruf protokolliert, der vom Client empfangen wurde, und den ausgehenden Methodenaufruf, der auf dem Client aufgerufen wird:

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

Der folgende Code in der *Startup.cs-Datei* registriert das Modul, das in der Hub-Pipeline ausgeführt werden soll:

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

Es gibt viele verschiedene Methoden, die Sie überschreiben können. Eine vollständige Liste finden Sie unter [HubPipelineModule-Methoden](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).
