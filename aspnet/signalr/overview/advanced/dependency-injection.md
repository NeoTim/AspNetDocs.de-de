---
uid: signalr/overview/advanced/dependency-injection
title: Abhängigkeitsinjektion in SignalR | Microsoft-Dokumentation
author: bradygaster
description: Version der Software verwendete in diesem Thema Visual Studio 2013 .NET 4.5 SignalR Version 2-Vorgängerversionen des in diesem Thema Informationen zu früheren Versionen von...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 54e263e277852d2d478ce5bccd4164254498831a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024747"
---
<a name="dependency-injection-in-signalr"></a><span data-ttu-id="2da54-103">Abhängigkeitsinjektion in SignalR</span><span class="sxs-lookup"><span data-stu-id="2da54-103">Dependency Injection in SignalR</span></span>
====================
<span data-ttu-id="2da54-104">durch [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="2da54-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2da54-105">In diesem Thema verwendeten Softwareversionen</span><span class="sxs-lookup"><span data-stu-id="2da54-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2da54-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2da54-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2da54-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2da54-107">.NET 4.5</span></span>
> - <span data-ttu-id="2da54-108">SignalR-Version 2</span><span class="sxs-lookup"><span data-stu-id="2da54-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2da54-109">Vorherige Versionen dieses Themas</span><span class="sxs-lookup"><span data-stu-id="2da54-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2da54-110">Weitere Informationen zu früheren Versionen von SignalR, finden Sie unter [ältere Versionen von SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="2da54-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2da54-111">Fragen und Kommentare</span><span class="sxs-lookup"><span data-stu-id="2da54-111">Questions and comments</span></span>
>
> <span data-ttu-id="2da54-112">Lassen Sie Feedback, auf wie Ihnen in diesem Tutorial gefallen hat und was wir in den Kommentaren am unteren Rand der Seite verbessern können.</span><span class="sxs-lookup"><span data-stu-id="2da54-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2da54-113">Wenn Sie Fragen, die nicht direkt mit dem Tutorial verknüpft sind haben, können Sie sie veröffentlichen das [ASP.NET SignalR-Forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) oder [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="2da54-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="2da54-114">Abhängigkeitsinjektion ist eine Möglichkeit zum Entfernen von hartcodierten Abhängigkeiten zwischen Objekten, erleichtert Ihnen die Abhängigkeiten eines Objekts entweder zu Testzwecken (mithilfe von Mockobjekten) zu ersetzen oder Laufzeitverhalten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="2da54-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="2da54-115">In diesem Tutorial wird gezeigt, wie Abhängigkeitsinjektion in SignalR-Hubs.</span><span class="sxs-lookup"><span data-stu-id="2da54-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="2da54-116">Es wird gezeigt, wie IoC-Container mit SignalR verwenden.</span><span class="sxs-lookup"><span data-stu-id="2da54-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="2da54-117">Ein IoC-Container ist ein allgemeines Rahmenwerk für Dependency Injection.</span><span class="sxs-lookup"><span data-stu-id="2da54-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="2da54-118">Was ist Dependency Injection?</span><span class="sxs-lookup"><span data-stu-id="2da54-118">What is Dependency Injection?</span></span>

<span data-ttu-id="2da54-119">Überspringen Sie diesen Abschnitt, wenn Sie bereits über Dependency Injection vertraut sind.</span><span class="sxs-lookup"><span data-stu-id="2da54-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="2da54-120">*Abhängigkeitsinjektion* (DI) ist ein Muster, in dem sind Objekte nicht verantwortlich für das Erstellen ihrer eigenen Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="2da54-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="2da54-121">Hier ist ein einfaches Beispiel DI motivieren.</span><span class="sxs-lookup"><span data-stu-id="2da54-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="2da54-122">Nehmen wir an, dass Sie ein Objekt haben, die Meldungen protokolliert werden soll.</span><span class="sxs-lookup"><span data-stu-id="2da54-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="2da54-123">Sie definieren eine protokollierungsschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="2da54-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="2da54-124">In das Objekt, Sie erstellen eine `ILogger` Protokollieren von Meldungen:</span><span class="sxs-lookup"><span data-stu-id="2da54-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="2da54-125">Dies funktioniert, aber es ist dabei nicht um den optimalen Entwurf.</span><span class="sxs-lookup"><span data-stu-id="2da54-125">This works, but it's not the best design.</span></span> <span data-ttu-id="2da54-126">Wenn Sie ersetzen möchten `FileLogger` mit einem anderen `ILogger` Implementierung müssen so ändern Sie `SomeComponent`.</span><span class="sxs-lookup"><span data-stu-id="2da54-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="2da54-127">Angenommen, dass viele andere verwendet werden `FileLogger`, Sie müssen alle zu ändern.</span><span class="sxs-lookup"><span data-stu-id="2da54-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="2da54-128">Oder wenn Sie sich entscheiden, stellen `FileLogger` ein Singleton, Sie müssen auch in der gesamten Anwendung ändern.</span><span class="sxs-lookup"><span data-stu-id="2da54-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="2da54-129">Ein besserer Ansatz ist auf "Einfügen" ein `ILogger` in das Objekt, z. B. durch einen Konstruktor mit dem Argument:</span><span class="sxs-lookup"><span data-stu-id="2da54-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="2da54-130">Nachdem das Objekt nicht verantwortlich für die Auswahl der ist `ILogger` verwenden.</span><span class="sxs-lookup"><span data-stu-id="2da54-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="2da54-131">Sie können Swich `ILogger` Implementierungen, ohne die Objekte, die davon abhängen.</span><span class="sxs-lookup"><span data-stu-id="2da54-131">You can swich `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="2da54-132">Dieses Muster wird aufgerufen, [Konstruktorinjektion](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="2da54-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="2da54-133">Ein weiteres Muster ist die Setter-Injektion, in dem Sie die Abhängigkeit über einen Setter-Methode oder Eigenschaft festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2da54-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="2da54-134">Einfache Abhängigkeitsinjektion in SignalR</span><span class="sxs-lookup"><span data-stu-id="2da54-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="2da54-135">Betrachten Sie die Chat-Anwendung aus dem Lernprogramm [erste Schritte mit SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="2da54-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="2da54-136">So sieht die hubklasse über diese Anwendung aus:</span><span class="sxs-lookup"><span data-stu-id="2da54-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="2da54-137">Nehmen wir an, dass Chat-Nachrichten auf dem Server zu speichern, bevor diese gesendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="2da54-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="2da54-138">Sie definieren eine Schnittstelle, die diese Funktionalität abstrahiert und Dependency Injection zum Einfügen von der Schnittstelle verwenden möglicherweise die `ChatHub` Klasse.</span><span class="sxs-lookup"><span data-stu-id="2da54-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="2da54-139">Das einzige Problem ist, dass Hubs mit eine SignalR-Anwendung nicht direkt erstellen; SignalR, die sie für Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="2da54-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="2da54-140">Standardmäßig erwartet SignalR eine Hub-Klasse über einen parameterlosen Konstruktor verfügt.</span><span class="sxs-lookup"><span data-stu-id="2da54-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="2da54-141">Allerdings können Sie ganz einfach eine Funktion zum Erstellen von hubinstanzen registrieren und verwenden Sie diese Funktion zum Ausführen von DI.</span><span class="sxs-lookup"><span data-stu-id="2da54-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="2da54-142">Registrieren Sie die Funktion durch den Aufruf **GlobalHost.DependencyResolver.Register**.</span><span class="sxs-lookup"><span data-stu-id="2da54-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="2da54-143">Jetzt SignalR dieser anonymen Funktion aufgerufen wird, sobald es zum Erstellen muss einer `ChatHub` Instanz.</span><span class="sxs-lookup"><span data-stu-id="2da54-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="2da54-144">IoC-Container</span><span class="sxs-lookup"><span data-stu-id="2da54-144">IoC Containers</span></span>

<span data-ttu-id="2da54-145">Der vorherige Code ist in einfachen Fällen in Ordnung.</span><span class="sxs-lookup"><span data-stu-id="2da54-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="2da54-146">Aber immer noch Folgendes schreiben musste:</span><span class="sxs-lookup"><span data-stu-id="2da54-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="2da54-147">In einer komplexen Anwendung mit vielen Abhängigkeiten müssen Sie einen Großteil dieser "verknüpfen" Code schreiben zu können.</span><span class="sxs-lookup"><span data-stu-id="2da54-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="2da54-148">Dieser Code kann schwierig zu verwalten sein, insbesondere dann, wenn Abhängigkeiten geschachtelt sind.</span><span class="sxs-lookup"><span data-stu-id="2da54-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="2da54-149">Es ist auch schwer, Komponententests.</span><span class="sxs-lookup"><span data-stu-id="2da54-149">It is also hard to unit test.</span></span>

<span data-ttu-id="2da54-150">Eine Lösung ist einen IoC-Container verwenden.</span><span class="sxs-lookup"><span data-stu-id="2da54-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="2da54-151">Ein IoC-Container ist eine Softwarekomponente, die zum Verwalten von Abhängigkeiten zuständig ist. Typen mit dem Container registrieren, und klicken Sie dann den Container verwenden, um Objekte zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2da54-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="2da54-152">Der Container ermittelt automatisch die Abhängigkeit Beziehungen.</span><span class="sxs-lookup"><span data-stu-id="2da54-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="2da54-153">Viele IoC-Container können auch steuern, z. B. Objektlebensdauer und Bereich.</span><span class="sxs-lookup"><span data-stu-id="2da54-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="2da54-154">"IoC" steht für "Inversion of Control", dies ist ein allgemeines Muster, in denen ein Framework in Anwendungscode aufruft.</span><span class="sxs-lookup"><span data-stu-id="2da54-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="2da54-155">Ein IoC-Container erstellt die Objekte, die "die übliche ablaufsteuerung kehrt".</span><span class="sxs-lookup"><span data-stu-id="2da54-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="2da54-156">Verwenden von IoC-Container in SignalR</span><span class="sxs-lookup"><span data-stu-id="2da54-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="2da54-157">Der Chat-Anwendung ist möglicherweise zu einfach, um von einem IoC-Container zu profitieren.</span><span class="sxs-lookup"><span data-stu-id="2da54-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="2da54-158">Stattdessen sehen wir uns die [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) Beispiel.</span><span class="sxs-lookup"><span data-stu-id="2da54-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="2da54-159">Der StockTicker-Beispiel definiert zwei wichtigste Klassen:</span><span class="sxs-lookup"><span data-stu-id="2da54-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="2da54-160">`StockTickerHub`: Die hubklasse, die Clientverbindungen verwaltet.</span><span class="sxs-lookup"><span data-stu-id="2da54-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="2da54-161">`StockTicker`: Ein Singleton, der Aktienkurse enthält und in regelmäßigen Abständen aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="2da54-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="2da54-162">`StockTickerHub` enthält einen Verweis auf die `StockTicker` Singleton, während `StockTicker` enthält einen Verweis auf die **IHubConnectionContext** für die `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2da54-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="2da54-163">Er verwendet diese Schnittstelle für die Kommunikation mit `StockTickerHub` Instanzen.</span><span class="sxs-lookup"><span data-stu-id="2da54-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="2da54-164">(Weitere Informationen finden Sie unter [Serverübertragung mit ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span><span class="sxs-lookup"><span data-stu-id="2da54-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="2da54-165">Wir können einen IoC-Container verwenden, um diese Abhängigkeiten ein wenig zu entwirren.</span><span class="sxs-lookup"><span data-stu-id="2da54-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="2da54-166">Zunächst sehen wir vereinfachen die `StockTickerHub` und `StockTicker` Klassen.</span><span class="sxs-lookup"><span data-stu-id="2da54-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="2da54-167">In den folgenden Code habe ich die Teile auskommentiert, dass wir nicht brauchen.</span><span class="sxs-lookup"><span data-stu-id="2da54-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="2da54-168">Entfernen Sie den parameterlosen Konstruktor aus `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2da54-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="2da54-169">Wir werden stattdessen immer DI verwenden, um den Hub zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2da54-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="2da54-170">Entfernen Sie für StockTicker befindet die Singleton-Instanz.</span><span class="sxs-lookup"><span data-stu-id="2da54-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="2da54-171">Später verwenden wir den IoC-Container, zur Steuerung der Lebensdauer der StockTicker befindet.</span><span class="sxs-lookup"><span data-stu-id="2da54-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="2da54-172">Stellen Sie den Konstruktor außerdem öffentlich.</span><span class="sxs-lookup"><span data-stu-id="2da54-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="2da54-173">Als Nächstes können wir Umgestalten des Codes durch Erstellen einer Schnittstelle für `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2da54-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="2da54-174">Wir verwenden diese Schnittstelle zum Entkoppeln der `StockTickerHub` aus der `StockTicker` Klasse.</span><span class="sxs-lookup"><span data-stu-id="2da54-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="2da54-175">Visual Studio legt diese Art von Umgestaltung einfach.</span><span class="sxs-lookup"><span data-stu-id="2da54-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="2da54-176">Öffnen Sie die Datei StockTicker.cs der rechten Maustaste auf die `StockTicker` Klassendeklaration, und wählen Sie **Umgestalten** ... **Schnittstelle extrahieren**.</span><span class="sxs-lookup"><span data-stu-id="2da54-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="2da54-177">In der **Schnittstelle extrahieren** Dialogfeld klicken Sie auf **Alles markieren**.</span><span class="sxs-lookup"><span data-stu-id="2da54-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="2da54-178">Lassen Sie die anderen Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="2da54-178">Leave the other defaults.</span></span> <span data-ttu-id="2da54-179">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="2da54-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="2da54-180">Visual Studio erstellt eine neue Schnittstelle namens `IStockTicker`, und ändert sich auch `StockTicker` für die Ableitung `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2da54-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="2da54-181">Öffnen Sie die Datei IStockTicker.cs und ändern Sie die Schnittstelle für **öffentliche**.</span><span class="sxs-lookup"><span data-stu-id="2da54-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="2da54-182">In der `StockTickerHub` Klasse, ändern Sie die beiden Instanzen von `StockTicker` zu `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="2da54-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="2da54-183">Erstellen einer `IStockTicker` Schnittstelle ist nicht zwingend erforderlich, aber ich wollte, um anzuzeigen, wie Dependency Injection unterstützen kann, die Kopplung zwischen Komponenten in Ihrer Anwendung reduzieren.</span><span class="sxs-lookup"><span data-stu-id="2da54-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="2da54-184">Fügen Sie die Ninject-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="2da54-184">Add the Ninject Library</span></span>

<span data-ttu-id="2da54-185">Es gibt viele Open-Source-IoC-Container für .NET.</span><span class="sxs-lookup"><span data-stu-id="2da54-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="2da54-186">In diesem Tutorial verwende ich [Ninject](http://www.ninject.org/).</span><span class="sxs-lookup"><span data-stu-id="2da54-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="2da54-187">(Andere beliebten Bibliotheken enthalten [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), und [StructureMap ](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="2da54-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="2da54-188">Verwenden Sie NuGet Package Manager zum Installieren der [Ninject Bibliothek](https://nuget.org/packages/Ninject/3.0.1.10).</span><span class="sxs-lookup"><span data-stu-id="2da54-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="2da54-189">In Visual Studio aus der **Tools** Menü die Option **NuGet Package Manager** > **-Paket-Manager-Konsole**.</span><span class="sxs-lookup"><span data-stu-id="2da54-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="2da54-190">Geben Sie im Fenster Paket-Manager-Konsole den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="2da54-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="2da54-191">Ersetzen Sie den Abhängigkeitskonfliktlöser für SignalR</span><span class="sxs-lookup"><span data-stu-id="2da54-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="2da54-192">Um Ninject in SignalR verwenden zu können, erstellen Sie eine abgeleitete Klasse **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="2da54-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="2da54-193">Diese Klasse überschreibt die **"GetService"** und **GetServices** Methoden **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="2da54-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="2da54-194">SignalR ruft diese Methoden zum Erstellen von verschiedenen Objekten zur Laufzeit, einschließlich der Hub-Instanzen als auch verschiedene Dienste, die intern von SignalR verwendet.</span><span class="sxs-lookup"><span data-stu-id="2da54-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="2da54-195">Die **"GetService"** Methode erstellt eine einzelne Instanz eines Typs.</span><span class="sxs-lookup"><span data-stu-id="2da54-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="2da54-196">Überschreiben Sie diese Methode zum Aufrufen des Kernels Ninject **TryGet** Methode.</span><span class="sxs-lookup"><span data-stu-id="2da54-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="2da54-197">Wenn diese Methode null zurückgibt, ein Fallback auf den Standardkonfliktlöser.</span><span class="sxs-lookup"><span data-stu-id="2da54-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="2da54-198">Die **GetServices** Methode erstellt eine Auflistung von Objekten eines angegebenen Typs.</span><span class="sxs-lookup"><span data-stu-id="2da54-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="2da54-199">Überschreiben Sie diese Methode, um die Ergebnisse mit den Ergebnissen der Standardkonfliktlöser Ninject verketten.</span><span class="sxs-lookup"><span data-stu-id="2da54-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="2da54-200">Ninject Bindungen konfigurieren</span><span class="sxs-lookup"><span data-stu-id="2da54-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="2da54-201">Jetzt verwenden wir Ninject, um die Bindungen des Typs deklarieren.</span><span class="sxs-lookup"><span data-stu-id="2da54-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="2da54-202">Öffnen Sie "Startup.cs"-Klasse Ihrer Anwendung (entweder manuell gemäß den Paket-Anweisungen in der Erstellung `readme.txt`, oder die durch das Hinzufügen von Authentifizierung zu Ihrem Projekt erstellt wurde).</span><span class="sxs-lookup"><span data-stu-id="2da54-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="2da54-203">In der `Startup.Configuration` -Methode, Ninject-Container, der Ninject aufruft, erstellt die *Kernel*.</span><span class="sxs-lookup"><span data-stu-id="2da54-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="2da54-204">Erstellen Sie eine Instanz von unseren benutzerdefinierten Abhängigkeitskonfliktlöser:</span><span class="sxs-lookup"><span data-stu-id="2da54-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="2da54-205">Erstellen Sie eine Bindung für `IStockTicker` wie folgt:</span><span class="sxs-lookup"><span data-stu-id="2da54-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="2da54-206">Dieser Code ist zwei Dinge sagen.</span><span class="sxs-lookup"><span data-stu-id="2da54-206">This code is saying two things.</span></span> <span data-ttu-id="2da54-207">Erste, wenn die Anwendung muss eine `IStockTicker`, der Kernel sollten erstellen Sie eine Instanz des `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2da54-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="2da54-208">Zweitens wird die `StockTicker` Klasse sollte als ein Singleton-Objekt erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="2da54-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="2da54-209">Ninject erstellt eine Instanz des Objekts, und die gleiche Instanz für jede Anforderung zurück.</span><span class="sxs-lookup"><span data-stu-id="2da54-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="2da54-210">Erstellen Sie eine Bindung für **IHubConnectionContext** wie folgt:</span><span class="sxs-lookup"><span data-stu-id="2da54-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="2da54-211">Dieser Code Creatres eine anonyme Funktion, die zurückgibt ein **IHubConnection**.</span><span class="sxs-lookup"><span data-stu-id="2da54-211">This code creatres an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="2da54-212">Die **WhenInjectedInto** Methode weist Ninject, um diese Funktion zu verwenden, nur bei der Erstellung `IStockTicker` Instanzen.</span><span class="sxs-lookup"><span data-stu-id="2da54-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="2da54-213">Der Grund ist, dass SignalR erstellt **IHubConnectionContext** Instanzen intern, und wir wollen nicht außer Kraft setzen, wie SignalR werden erstellt.</span><span class="sxs-lookup"><span data-stu-id="2da54-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="2da54-214">Diese Funktion gilt nur für unsere `StockTicker` Klasse.</span><span class="sxs-lookup"><span data-stu-id="2da54-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="2da54-215">Übergeben Sie den Abhängigkeitskonfliktlöser in die **MapSignalR** Methode, indem eine hubkonfiguration hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="2da54-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="2da54-216">Aktualisieren Sie die Startup.ConfigureSignalR-Methode in der beispielanwendung Startup-Klasse, mit der neue Parameter:</span><span class="sxs-lookup"><span data-stu-id="2da54-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="2da54-217">Jetzt SignalR, verwenden Sie die im angegebenen Konfliktlösers wird **MapSignalR**, anstatt des Standardkonfliktlösers.</span><span class="sxs-lookup"><span data-stu-id="2da54-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="2da54-218">Hier ist die vollständige codeauflistung für `Startup.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="2da54-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="2da54-219">Um die Anwendung besteht in Visual Studio auszuführen, drücken Sie F5 aus.</span><span class="sxs-lookup"><span data-stu-id="2da54-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="2da54-220">Navigieren Sie im Browserfenster zu `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span><span class="sxs-lookup"><span data-stu-id="2da54-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="2da54-221">Die Anwendung verfügt über genau die gleiche Funktionalität wie vor.</span><span class="sxs-lookup"><span data-stu-id="2da54-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="2da54-222">(Eine Beschreibung finden Sie unter [Serverübertragung mit ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) Wir noch nicht das Verhalten geändert werden. soeben erstellt den Code einfacher zu testen, verwalten und entwickeln.</span><span class="sxs-lookup"><span data-stu-id="2da54-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>