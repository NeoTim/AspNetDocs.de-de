---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Tutorial: Server-Broadcast mit SignalR 2 | Microsoft Docs'
author: tdykstra
description: In diesem Tutorial wird gezeigt, wie Sie eine Webanwendung erstellen, die ASP.NET SignalR 2 verwendet, um Serverübertragungsfunktionen bereitzustellen.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675724"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="b8c34-103">Tutorial: Server-Broadcast mit SignalR 2</span><span class="sxs-lookup"><span data-stu-id="b8c34-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b8c34-104">In diesem Tutorial wird gezeigt, wie Sie eine Webanwendung erstellen, die ASP.NET SignalR 2 verwendet, um Serverübertragungsfunktionen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="b8c34-105">Serverübertragung bedeutet, dass der Server die an Clients gesendete Kommunikation startet.</span><span class="sxs-lookup"><span data-stu-id="b8c34-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="b8c34-106">Die Anwendung, die Sie in diesem Tutorial erstellen, simuliert einen Börsenticker, ein typisches Szenario für die Serverübertragungsfunktionalität.</span><span class="sxs-lookup"><span data-stu-id="b8c34-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="b8c34-107">In regelmäßigen Abständen aktualisiert der Server nach dem Zufallsprinzip die Aktienkurse und sendet die Aktualisierungen an alle verbundenen Clients.</span><span class="sxs-lookup"><span data-stu-id="b8c34-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="b8c34-108">Im Browser ändern sich die **Change** Zahlen **%** und Symbole in den Spalten Ändern und Spalten dynamisch als Reaktion auf Benachrichtigungen vom Server.</span><span class="sxs-lookup"><span data-stu-id="b8c34-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="b8c34-109">Wenn Sie zusätzliche Browser mit derselben URL öffnen, werden alle dieselben Daten und dieselben Änderungen gleichzeitig angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![Web erstellen](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="b8c34-111">In diesem Tutorial führen Sie Folgendes durch:</span><span class="sxs-lookup"><span data-stu-id="b8c34-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8c34-112">Erstellen des Projekts</span><span class="sxs-lookup"><span data-stu-id="b8c34-112">Create the project</span></span>
> * <span data-ttu-id="b8c34-113">Einrichten des Servercodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-113">Set up the server code</span></span>
> * <span data-ttu-id="b8c34-114">Überprüfen des Servercodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-114">Examine the server code</span></span>
> * <span data-ttu-id="b8c34-115">Einrichten des Clientcodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-115">Set up the client code</span></span>
> * <span data-ttu-id="b8c34-116">Untersuchen des Clientcodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-116">Examine the client code</span></span>
> * <span data-ttu-id="b8c34-117">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="b8c34-117">Test the application</span></span>
> * <span data-ttu-id="b8c34-118">Aktivieren der Protokollierung</span><span class="sxs-lookup"><span data-stu-id="b8c34-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8c34-119">Wenn Sie die Schritte zum Erstellen der Anwendung nicht durcharbeiten möchten, können Sie das SignalR.Sample-Paket in einem neuen Projekt "Empty ASP.NET Web Application" installieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="b8c34-120">Wenn Sie das NuGet-Paket installieren, ohne die Schritte in diesem Tutorial auszuführen, müssen Sie die Anweisungen in der Datei *readme.txt* befolgen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="b8c34-121">Zum Ausführen des Pakets müssen Sie eine OWIN-Startklasse hinzufügen, die die `ConfigureSignalR` Methode im installierten Paket aufruft.</span><span class="sxs-lookup"><span data-stu-id="b8c34-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="b8c34-122">Sie erhalten eine Fehlermeldung, wenn Sie die OWIN-Startklasse nicht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="b8c34-123">Weitere Informationen finden Sie im [Beispielabschnitt "Installieren des StockTicker"](#install-the-stockticker-sample) in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="b8c34-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8c34-124">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="b8c34-124">Prerequisites</span></span>

* <span data-ttu-id="b8c34-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) mit der Workload **ASP.NET und Webentwicklung**</span><span class="sxs-lookup"><span data-stu-id="b8c34-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="b8c34-126">Erstellen des Projekts</span><span class="sxs-lookup"><span data-stu-id="b8c34-126">Create the project</span></span>

<span data-ttu-id="b8c34-127">In diesem Abschnitt wird gezeigt, wie Sie Visual Studio 2017 verwenden, um eine leere ASP.NET Webanwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="b8c34-128">Erstellen Sie in Visual Studio eine ASP.NET Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="b8c34-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![Web erstellen](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="b8c34-130">Lassen Sie im Fenster **Neue ASP.NET Webapplication - SignalR.StockTicker** **Leer** aus und wählen Sie **OK**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="b8c34-131">Einrichten des Servercodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-131">Set up the server code</span></span>

<span data-ttu-id="b8c34-132">In diesem Abschnitt richten Sie den Code ein, der auf dem Server ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="b8c34-133">Erstellen der Stock-Klasse</span><span class="sxs-lookup"><span data-stu-id="b8c34-133">Create the Stock class</span></span>

<span data-ttu-id="b8c34-134">Sie beginnen mit *Stock* dem Erstellen der Stock-Modellklasse, die Sie zum Speichern und Übertragen von Informationen über einen Bestand verwenden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="b8c34-135">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Klasse** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b8c34-136">Benennen Sie die Klasse *Stock,* und fügen Sie sie dem Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="b8c34-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="b8c34-137">Ersetzen Sie den Code in der *Stock.cs* Datei durch diesen Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="b8c34-138">Die beiden Eigenschaften, die Sie beim `Symbol` Erstellen von Beständen festlegen, `Price`sind (z. B. MSFT für Microsoft) und .</span><span class="sxs-lookup"><span data-stu-id="b8c34-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="b8c34-139">Die anderen Eigenschaften hängen davon `Price`ab, wie und wann Sie .</span><span class="sxs-lookup"><span data-stu-id="b8c34-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="b8c34-140">Wenn Sie das `Price`erste Mal festlegen, wird `DayOpen`der Wert an weitergegeben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="b8c34-141">Danach berechnet die `Price`App beim Festlegen `Change` die `PercentChange` Und-Eigenschaftswerte `Price` basierend `DayOpen`auf der Differenz zwischen und .</span><span class="sxs-lookup"><span data-stu-id="b8c34-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="b8c34-142">Erstellen der StockTickerHub- und StockTicker-Klassen</span><span class="sxs-lookup"><span data-stu-id="b8c34-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="b8c34-143">Sie verwenden die SignalR Hub-API, um die Server-zu-Client-Interaktion zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="b8c34-144">Eine `StockTickerHub` Klasse, die von der `Hub` SignalR-Klasse ableitet, verarbeitet empfangende Verbindungen und Methodenaufrufe von Clients.</span><span class="sxs-lookup"><span data-stu-id="b8c34-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="b8c34-145">Sie müssen auch Bestandsdaten `Timer` verwalten und ein Objekt ausführen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="b8c34-146">Das `Timer` Objekt löst in regelmäßigen Abständen Preisaktualisierungen unabhängig von Clientverbindungen aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="b8c34-147">Sie können diese Funktionen nicht `Hub` in einer Klasse einsetzen, da Hubs vorübergehend sind.</span><span class="sxs-lookup"><span data-stu-id="b8c34-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="b8c34-148">Die App `Hub` erstellt eine Klasseninstanz für jede Aufgabe auf dem Hub, z. B. Verbindungen und Aufrufe vom Client an den Server.</span><span class="sxs-lookup"><span data-stu-id="b8c34-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="b8c34-149">Der Mechanismus, der Bestandsdaten speichert, Preise aktualisiert und die Preisaktualisierungen sendet, muss also in einer separaten Klasse ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="b8c34-150">Sie nennen die `StockTicker`Klasse .</span><span class="sxs-lookup"><span data-stu-id="b8c34-150">You'll name the class `StockTicker`.</span></span>

![Ausstrahlung von StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="b8c34-152">Sie möchten nur, `StockTicker` dass eine Instanz der Klasse auf dem Server ausgeführt wird, daher müssen Sie einen Verweis von jeder `StockTickerHub` Instanz auf die Singleton-Instanz `StockTicker` einrichten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="b8c34-153">Die `StockTicker` Klasse muss an Clients übertragen werden, da sie `StockTicker` über die Bestandsdaten verfügt und Aktualisierungen auslöst, aber keine `Hub` Klasse ist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="b8c34-154">Die `StockTicker` Klasse muss einen Verweis auf das SignalR Hub-Verbindungskontextobjekt abrufen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="b8c34-155">Anschließend kann das SignalR-Verbindungskontextobjekt verwendet werden, um es an Clients zu übertragen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="b8c34-156">Erstellen StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="b8c34-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="b8c34-157">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Neues Element** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b8c34-158">**Wählen** > Sie unter Neues Element hinzufügen **- SignalR.StockTicker**aus, installed**Visual C-Web** > **Web** > **SignalR** und dann **SignalR Hub Class (v2)** aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="b8c34-159">Benennen Sie die Klasse *StockTickerHub,* und fügen Sie sie dem Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="b8c34-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="b8c34-160">In diesem Schritt wird die *StockTickerHub.cs* Klassendatei erstellt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="b8c34-161">Gleichzeitig wird eine Reihe von Skriptdateien und Assemblyverweisen hinzugefügt, die SignalR zum Projekt unterstützen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="b8c34-162">Ersetzen Sie den Code in der *StockTickerHub.cs* Datei durch diesen Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="b8c34-163">Speichern Sie die Datei .</span><span class="sxs-lookup"><span data-stu-id="b8c34-163">Save the file.</span></span>

<span data-ttu-id="b8c34-164">Die App [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) verwendet die Hub-Klasse, um Methoden zu definieren, die die Clients auf dem Server aufrufen können.</span><span class="sxs-lookup"><span data-stu-id="b8c34-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="b8c34-165">Sie definieren eine Methode: `GetAllStocks()`.</span><span class="sxs-lookup"><span data-stu-id="b8c34-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="b8c34-166">Wenn ein Client zunächst eine Verbindung mit dem Server herstellt, ruft er diese Methode auf, um eine Liste aller Bestände mit ihren aktuellen Preisen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="b8c34-167">Die Methode kann synchron `IEnumerable<Stock>` ausgeführt und zurückgegeben werden, da sie Daten aus dem Arbeitsspeicher zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="b8c34-168">Wenn die Methode die Daten abrufen muss, indem sie etwas tut, das warten würde, `Task<IEnumerable<Stock>>` z. B. eine Datenbanksuche oder einen Webdienstaufruf, geben Sie als Rückgabewert an, um die asynchrone Verarbeitung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="b8c34-169">Weitere Informationen finden Sie unter [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronly](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span><span class="sxs-lookup"><span data-stu-id="b8c34-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="b8c34-170">Das `HubName` Attribut gibt an, wie die App auf den Hub im JavaScript-Code auf dem Client verweist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="b8c34-171">Der Standardname auf dem Client, wenn Sie dieses Attribut nicht verwenden, ist eine camelCase-Version des Klassennamens, die in diesem Fall `stockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="b8c34-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="b8c34-172">Wie Sie später beim Erstellen `StockTicker` der Klasse sehen werden, erstellt die App eine `Instance` Singleton-Instanz dieser Klasse in ihrer statischen Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="b8c34-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="b8c34-173">Diese Singleton-Instanz von `StockTicker` befindet sich im Arbeitsspeicher, unabhängig davon, wie viele Clients eine Verbindung herstellen oder trennen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="b8c34-174">Diese Instanz verwendet `GetAllStocks()` die Methode, um aktuelle Bestandsinformationen zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="b8c34-175">Erstellen StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="b8c34-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="b8c34-176">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Klasse** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="b8c34-177">Benennen Sie die Klasse *StockTicker,* und fügen Sie sie dem Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="b8c34-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="b8c34-178">Ersetzen Sie den Code in der *StockTicker.cs* Datei durch diesen Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="b8c34-179">Da alle Threads dieselbe Instanz des StockTicker-Codes ausführen, muss die StockTicker-Klasse threadsicher sein.</span><span class="sxs-lookup"><span data-stu-id="b8c34-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="b8c34-180">Überprüfen des Servercodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-180">Examine the server code</span></span>

<span data-ttu-id="b8c34-181">Wenn Sie den Servercode untersuchen, können Sie verstehen, wie die App funktioniert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="b8c34-182">Speichern der Singleton-Instanz in einem statischen Feld</span><span class="sxs-lookup"><span data-stu-id="b8c34-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="b8c34-183">Der Code initialisiert `_instance` das statische Feld, das die `Instance` Eigenschaft mit einer Instanz der Klasse unterstützt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="b8c34-184">Da der Konstruktor privat ist, ist er die einzige Instanz der Klasse, die die App erstellen kann.</span><span class="sxs-lookup"><span data-stu-id="b8c34-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="b8c34-185">Die App verwendet Lazy `_instance` [Initialisierung](/dotnet/framework/performance/lazy-initialization) für das Feld.</span><span class="sxs-lookup"><span data-stu-id="b8c34-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="b8c34-186">Es ist nicht aus Leistungsgründen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-186">It's not for performance reasons.</span></span> <span data-ttu-id="b8c34-187">Es soll sicherstellen, dass die Instanzerstellung threadsicher ist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="b8c34-188">Jedes Mal, wenn ein Client eine Verbindung mit dem Server herstellt, ruft eine neue Instanz der `StockTicker.Instance` StockTickerHub-Klasse, die `StockTickerHub` in einem separaten Thread ausgeführt wird, die StockTicker Singleton-Instanz von der statischen Eigenschaft ab, wie Sie zuvor in der Klasse gesehen haben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="b8c34-189">Speichern von Bestandsdaten in einem ConcurrentDictionary</span><span class="sxs-lookup"><span data-stu-id="b8c34-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="b8c34-190">Der Konstruktor initialisiert `_stocks` die Auflistung mit einigen `GetAllStocks` Stichprobenbestandsdaten und gibt die Bestände zurück.</span><span class="sxs-lookup"><span data-stu-id="b8c34-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="b8c34-191">Wie Sie bereits gesehen haben, wird `StockTickerHub.GetAllStocks`diese Sammlung von Beständen von zurückgegeben, einer Servermethode in der `Hub` Klasse, die Clients aufrufen können.</span><span class="sxs-lookup"><span data-stu-id="b8c34-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="b8c34-192">Die Bestandsauflistung ist als [ConcurrentDictionary-Typ](https://msdn.microsoft.com/library/dd287191.aspx) für die Threadsicherheit definiert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="b8c34-193">Alternativ können Sie ein [Dictionary-Objekt](https://msdn.microsoft.com/library/xfhwa508.aspx) verwenden und das Wörterbuch explizit sperren, wenn Sie Änderungen daran vornehmen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="b8c34-194">Für diese Beispielanwendung ist es in Ordnung, Anwendungsdaten im Arbeitsspeicher zu speichern `StockTicker` und die Daten zu verlieren, wenn die App die Instance entsorgt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="b8c34-195">In einer echten Anwendung würden Sie mit einem Back-End-Datenspeicher wie einer Datenbank arbeiten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="b8c34-196">Regelmäßige Aktualisierung der Aktienkurse</span><span class="sxs-lookup"><span data-stu-id="b8c34-196">Periodically updating stock prices</span></span>

<span data-ttu-id="b8c34-197">Der Konstruktor startet `Timer` ein Objekt, das regelmäßig Methoden aufruft, die Aktienkurse nach dem Zufallsprinzip aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="b8c34-198">`Timer`fordert `UpdateStockPrices`, die im Zustandsparameter null übergibt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="b8c34-199">Vor dem Aktualisieren der Preise nimmt `_updateStockPricesLock` die App eine Sperre für das Objekt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="b8c34-200">Der Code überprüft, ob ein anderer Thread `TryUpdateStockPrice` bereits Preise aktualisiert, und ruft dann jeden Bestand in der Liste auf.</span><span class="sxs-lookup"><span data-stu-id="b8c34-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="b8c34-201">Die `TryUpdateStockPrice` Methode entscheidet, ob der Aktienkurs geändert werden soll und wie viel er ihn ändern soll.</span><span class="sxs-lookup"><span data-stu-id="b8c34-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="b8c34-202">Wenn sich der Aktienkurs ändert, ruft `BroadcastStockPrice` die App an, um die Aktienkursänderung an alle verbundenen Kunden zu übertragen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="b8c34-203">Das `_updatingStockPrices` Flag, das [als flüchtig](https://msdn.microsoft.com/library/x13ttww7.aspx) gekennzeichnet ist, um sicherzustellen, dass es threadsicher ist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="b8c34-204">In einer echten `TryUpdateStockPrice` Anwendung würde die Methode einen Webdienst aufrufen, um den Preis nachzuschlagen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="b8c34-205">In diesem Code verwendet die App einen Zufallszahlengenerator, um Änderungen nach dem Zufallsprinzip vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="b8c34-206">Abrufen des SignalR-Kontexts, damit die StockTicker-Klasse an Clients übertragen werden kann</span><span class="sxs-lookup"><span data-stu-id="b8c34-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="b8c34-207">Da die Preisänderungen hier `StockTicker` im Objekt entstehen, ist es `updateStockPrice` das Objekt, das eine Methode für alle verbundenen Clients aufrufen muss.</span><span class="sxs-lookup"><span data-stu-id="b8c34-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="b8c34-208">In `Hub` einer Klasse verfügen Sie über eine `StockTicker` API zum Aufrufen von `Hub` Clientmethoden, leiten jedoch nicht `Hub` von der Klasse ab und haben keinen Verweis auf ein Objekt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="b8c34-209">Um an verbundene Clients `StockTicker` zu übertragen, muss die Klasse `StockTickerHub` die SignalR-Kontextinstanz für die Klasse abrufen und diese verwenden, um Methoden für Clients aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="b8c34-210">Der Code ruft einen Verweis auf den SignalR-Kontext ab, wenn er die Singleton-Klasseninstanz erstellt, diesen Verweis an den Konstruktor übergibt und der Konstruktor ihn in die `Clients` Eigenschaft setzt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="b8c34-211">Es gibt zwei Gründe, warum Sie den Kontext nur einmal abrufen möchten: Das Abrufen des Kontexts ist eine kostspielige Aufgabe, und wenn Sie ihn einmal abrufen, wird sichergestellt, dass die App die beabsichtigte Reihenfolge der an die Clients gesendeten Nachrichten beibehält.</span><span class="sxs-lookup"><span data-stu-id="b8c34-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="b8c34-212">Wenn `Clients` Sie die Eigenschaft des Kontexts abrufen und in der `StockTickerClient` Eigenschaft ablenken, können `Hub` Sie Code schreiben, um Clientmethoden aufzurufen, die wie in einer Klasse aussehen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="b8c34-213">Um z. B. an alle `Clients.All.updateStockPrice(stock)`Clients zu senden, können Sie schreiben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="b8c34-214">Die `updateStockPrice` Methode, die `BroadcastStockPrice` Sie aufrufen, ist noch nicht vorhanden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="b8c34-215">Sie fügen sie später hinzu, wenn Sie Code schreiben, der auf dem Client ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="b8c34-216">Sie können `updateStockPrice` hier `Clients.All` darauf verweisen, da dies dynamisch ist, was bedeutet, dass die App den Ausdruck zur Laufzeit auswertet.</span><span class="sxs-lookup"><span data-stu-id="b8c34-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="b8c34-217">Wenn dieser Methodenaufruf ausgeführt wird, sendet SignalR den Methodennamen und den Parameterwert an `updateStockPrice`den Client, und wenn der Client eine Methode mit dem Namen hat, ruft die App diese Methode auf und übergibt den Parameterwert an ihn.</span><span class="sxs-lookup"><span data-stu-id="b8c34-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="b8c34-218">`Clients.All`bedeutet, an alle Clients zu senden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="b8c34-219">Mit SignalR können Sie weitere Optionen angeben, an welche Clients oder Gruppen von Clients gesendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="b8c34-220">Weitere Informationen finden Sie unter [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="b8c34-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="b8c34-221">Registrieren der SignalR-Route</span><span class="sxs-lookup"><span data-stu-id="b8c34-221">Register the SignalR route</span></span>

<span data-ttu-id="b8c34-222">Der Server muss wissen, welche URL abgefangen und direkt an SignalR gesendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b8c34-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="b8c34-223">Fügen Sie dazu eine OWIN-Startklasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="b8c34-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="b8c34-224">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**Neues Element** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="b8c34-225">Wählen Sie unter **Neues Element hinzufügen - SignalR.StockTicker** **Installed** > **Visual C'Web** > **Web** und dann **OWIN Startup Class**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="b8c34-226">Benennen Sie die Klasse *Start,* und wählen Sie **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="b8c34-227">Ersetzen Sie den Standardcode in der *Startup.cs* Datei durch diesen Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="b8c34-228">Sie haben die Einrichtung des Servercodes abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="b8c34-229">Im nächsten Abschnitt richten Sie den Client ein.</span><span class="sxs-lookup"><span data-stu-id="b8c34-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="b8c34-230">Einrichten des Clientcodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-230">Set up the client code</span></span>

<span data-ttu-id="b8c34-231">In diesem Abschnitt richten Sie den Code ein, der auf dem Client ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="b8c34-232">Erstellen der HTML-Seite und der JavaScript-Datei</span><span class="sxs-lookup"><span data-stu-id="b8c34-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="b8c34-233">Die HTML-Seite zeigt die Daten an und die JavaScript-Datei organisiert die Daten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="b8c34-234">Erstellen von StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="b8c34-234">Create StockTicker.html</span></span>

<span data-ttu-id="b8c34-235">Zuerst fügen Sie den HTML-Client hinzu.</span><span class="sxs-lookup"><span data-stu-id="b8c34-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="b8c34-236">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**HTML-Seite** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="b8c34-237">Benennen Sie die Datei *StockTicker* und wählen Sie **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b8c34-238">Ersetzen Sie den Standardcode in der *Datei StockTicker.html* durch diesen Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="b8c34-239">Der HTML-Code erstellt eine Tabelle mit fünf Spalten, einer Kopfzeile und einer Datenzeile mit einer einzelnen Zelle, die alle fünf Spalten umfasst.</span><span class="sxs-lookup"><span data-stu-id="b8c34-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="b8c34-240">Die Datenzeile zeigt "Laden..." momentan, wenn die App gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="b8c34-241">JavaScript-Code entfernt diese Zeile und fügt an ihrer Stelle Zeilen mit Vom Server abgerufenen Bestandsdaten hinzu.</span><span class="sxs-lookup"><span data-stu-id="b8c34-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="b8c34-242">Die Skript-Tags geben Folgendes an:</span><span class="sxs-lookup"><span data-stu-id="b8c34-242">The script tags specify:</span></span>

    * <span data-ttu-id="b8c34-243">Die jQuery-Skriptdatei.</span><span class="sxs-lookup"><span data-stu-id="b8c34-243">The jQuery script file.</span></span>

    * <span data-ttu-id="b8c34-244">Die SignalR-Kernskriptdatei.</span><span class="sxs-lookup"><span data-stu-id="b8c34-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="b8c34-245">Die SignalR-Proxy-Skriptdatei.</span><span class="sxs-lookup"><span data-stu-id="b8c34-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="b8c34-246">Eine StockTicker-Skriptdatei, die Sie später erstellen werden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="b8c34-247">Die App generiert dynamisch die SignalR-Proxys-Skriptdatei.</span><span class="sxs-lookup"><span data-stu-id="b8c34-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="b8c34-248">Sie gibt die URL "/signalr/hubs" an und definiert Proxymethoden für die Methoden `StockTickerHub.GetAllStocks`in der Hub-Klasse, in diesem Fall für .</span><span class="sxs-lookup"><span data-stu-id="b8c34-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="b8c34-249">Wenn Sie möchten, können Sie diese JavaScript-Datei manuell generieren, indem Sie [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)verwenden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="b8c34-250">Vergessen Sie nicht, die dynamische `MapHubs` Dateierstellung im Methodenaufruf zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="b8c34-251">Erweitern Sie im **Projektmappen-Explorer** **Skripts**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="b8c34-252">Skriptbibliotheken für jQuery und SignalR sind im Projekt sichtbar.</span><span class="sxs-lookup"><span data-stu-id="b8c34-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b8c34-253">Der Paket-Manager installiert eine neuere Version der SignalR-Skripte.</span><span class="sxs-lookup"><span data-stu-id="b8c34-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="b8c34-254">Aktualisieren Sie die Skriptverweise im Codeblock so, dass sie den Versionen der Skriptdateien im Projekt entsprechen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="b8c34-255">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf *StockTicker.html*, und wählen Sie dann **Als Startseite festlegen**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="b8c34-256">Erstellen von StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="b8c34-256">Create StockTicker.js</span></span>

<span data-ttu-id="b8c34-257">Erstellen Sie nun die JavaScript-Datei.</span><span class="sxs-lookup"><span data-stu-id="b8c34-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="b8c34-258">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie**JavaScript-Datei** **hinzufügen** > aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="b8c34-259">Benennen Sie die Datei *StockTicker* und wählen Sie **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="b8c34-260">Fügen Sie diesen Code zur Datei *StockTicker.js* hinzu:</span><span class="sxs-lookup"><span data-stu-id="b8c34-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="b8c34-261">Untersuchen des Clientcodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-261">Examine the client code</span></span>

<span data-ttu-id="b8c34-262">Wenn Sie den Clientcode untersuchen, können Sie erfahren, wie der Clientcode mit dem Servercode interagiert, damit die App funktioniert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="b8c34-263">Starten der Verbindung</span><span class="sxs-lookup"><span data-stu-id="b8c34-263">Starting the connection</span></span>

<span data-ttu-id="b8c34-264">`$.connection`bezieht sich auf die SignalR-Proxys.</span><span class="sxs-lookup"><span data-stu-id="b8c34-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="b8c34-265">Der Code ruft einen Verweis `StockTickerHub` auf den Proxy `ticker` für die Klasse ab und legt ihn in die Variable ein.</span><span class="sxs-lookup"><span data-stu-id="b8c34-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="b8c34-266">Der Proxyname ist der Name, `HubName` der durch das Attribut festgelegt wurde:</span><span class="sxs-lookup"><span data-stu-id="b8c34-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="b8c34-267">Nachdem Sie alle Variablen und Funktionen definiert haben, initialisiert die letzte Codezeile in `start` der Datei die SignalR-Verbindung, indem sie die SignalR-Funktion aufruft.</span><span class="sxs-lookup"><span data-stu-id="b8c34-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="b8c34-268">Die `start` Funktion wird asynchron ausgeführt und gibt ein [jQuery Deferred-Objekt](http://api.jquery.com/category/deferred-object/)zurück.</span><span class="sxs-lookup"><span data-stu-id="b8c34-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="b8c34-269">Sie können die fertige Funktion aufrufen, um die Funktion anzugeben, die aufrufen soll, wenn die App die asynchrone Aktion beendet.</span><span class="sxs-lookup"><span data-stu-id="b8c34-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="b8c34-270">Alle Bestände erhalten</span><span class="sxs-lookup"><span data-stu-id="b8c34-270">Getting all the stocks</span></span>

<span data-ttu-id="b8c34-271">Die `init` Funktion `getAllStocks` ruft die Funktion auf dem Server auf und verwendet die Informationen, die der Server zurückgibt, um die Bestandstabelle zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="b8c34-272">Beachten Sie, dass Sie standardmäßig camelCasing auf dem Client verwenden müssen, obwohl der Methodenname auf dem Server pascal-cased ist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="b8c34-273">Die CamelCasing-Regel gilt nur für Methoden, nicht für Objekte.</span><span class="sxs-lookup"><span data-stu-id="b8c34-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="b8c34-274">Sie beziehen sich `stock.Symbol` z. B. auf und `stock.Price`, nicht `stock.symbol` oder `stock.price`.</span><span class="sxs-lookup"><span data-stu-id="b8c34-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="b8c34-275">In `init` der Methode erstellt die App HTML für eine Tabellenzeile für `formatStock` jedes vom `stock` Server empfangene Stockobjekt, indem sie die Formateigenschaften des Objekts aufruft und dann aufruft, `supplant` um Platzhalter in der `rowTemplate` Variablen durch die `stock` Objekteigenschaftswerte zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="b8c34-276">Der resultierende HTML-Code wird dann an die Bestandstabelle angehängt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="b8c34-277">Sie `init` rufen auf, indem `callback` Sie es als Funktion `start` übergeben, die nach Abschluss der asynchronen Funktion ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="b8c34-278">Wenn Sie `init` nach dem Aufruf `start`als separate JavaScript-Anweisung aufgerufen haben, schlägt die Funktion fehl, da sie sofort ausgeführt wird, ohne darauf zu warten, dass die Startfunktion den Verbindungsaufbau beendet.</span><span class="sxs-lookup"><span data-stu-id="b8c34-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="b8c34-279">In diesem Fall `init` würde die Funktion `getAllStocks` versuchen, die Funktion aufzurufen, bevor die App eine Serververbindung herstellt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="b8c34-280">Aktualisierte Aktienkurse</span><span class="sxs-lookup"><span data-stu-id="b8c34-280">Getting updated stock prices</span></span>

<span data-ttu-id="b8c34-281">Wenn der Server den Kurs einer Aktie `updateStockPrice` ändert, ruft er die auf verbundenen Clients auf.</span><span class="sxs-lookup"><span data-stu-id="b8c34-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="b8c34-282">Die App fügt die Funktion der `stockTicker` Clienteigenschaft des Proxys hinzu, um sie für Aufrufe vom Server verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="b8c34-283">Die `updateStockPrice` Funktion formatiert ein vom Server empfangenes Stockobjekt auf `init` die gleiche Weise wie in der Funktion in eine Tabellenzeile.</span><span class="sxs-lookup"><span data-stu-id="b8c34-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="b8c34-284">Anstatt die Zeile an die Tabelle anzuhängen, findet sie die aktuelle Zeile der Aktie in der Tabelle und ersetzt diese Zeile durch die neue Zeile.</span><span class="sxs-lookup"><span data-stu-id="b8c34-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="b8c34-285">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="b8c34-285">Test the application</span></span>

<span data-ttu-id="b8c34-286">Sie können die App testen, um sicherzustellen, dass sie funktioniert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="b8c34-287">Sie sehen, wie alle Browserfenster die Live-Aktientabelle mit schwankenden Aktienkursen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="b8c34-288">Aktivieren Sie in der Symbolleiste das **Skriptdebuggen,** und wählen Sie dann die Wiedergabeschaltfläche aus, um die App im Debugmodus auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![Screenshot des Benutzers, der den Debugmodus aktiviert und Play auswählt.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="b8c34-290">Es wird ein Browserfenster geöffnet, in dem die **Live Stock Table**angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="b8c34-291">Die Bestandstabelle zeigt zunächst das "Laden..." Nach kurzer Zeit zeigt die App dann die anfänglichen Bestandsdaten an, und dann beginnen sich die Aktienkurse zu ändern.</span><span class="sxs-lookup"><span data-stu-id="b8c34-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="b8c34-292">Kopieren Sie die URL aus dem Browser, öffnen Sie zwei weitere Browser, und fügen Sie die URLs in die Adressleisten ein.</span><span class="sxs-lookup"><span data-stu-id="b8c34-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="b8c34-293">Die anfängliche Bestandsanzeige ist die gleiche wie der erste Browser und Änderungen erfolgen gleichzeitig.</span><span class="sxs-lookup"><span data-stu-id="b8c34-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="b8c34-294">Schließen Sie alle Browser, öffnen Sie einen neuen Browser, und wechseln Sie zur gleichen URL.</span><span class="sxs-lookup"><span data-stu-id="b8c34-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="b8c34-295">Das StockTicker Singleton-Objekt wurde weiterhin auf dem Server ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="b8c34-296">Die **Live Stock Tabelle** zeigt, dass sich die Bestände weiter verändert haben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="b8c34-297">Die Anfangstabelle mit Denkzahlen ohne Änderung wird nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="b8c34-298">Schließen Sie den Browser.</span><span class="sxs-lookup"><span data-stu-id="b8c34-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="b8c34-299">Aktivieren der Protokollierung</span><span class="sxs-lookup"><span data-stu-id="b8c34-299">Enable logging</span></span>

<span data-ttu-id="b8c34-300">SignalR verfügt über eine integrierte Protokollierungsfunktion, die Sie auf dem Client aktivieren können, um bei der Fehlerbehebung zu helfen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="b8c34-301">In diesem Abschnitt aktivieren Sie die Protokollierung und zeigen Beispiele, die zeigen, wie Protokolle Ihnen sagen, welche der folgenden Transportmethoden SignalR verwendet:</span><span class="sxs-lookup"><span data-stu-id="b8c34-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="b8c34-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), unterstützt von IIS 8 und aktuellen Browsern.</span><span class="sxs-lookup"><span data-stu-id="b8c34-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="b8c34-303">[Servergesendete Ereignisse](http://en.wikipedia.org/wiki/Server-sent_events), die von anderen Browsern als Internet Explorer unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="b8c34-304">[Forever-Frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), unterstützt von Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b8c34-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="b8c34-305">[Ajax Long Polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), unterstützt von allen Browsern.</span><span class="sxs-lookup"><span data-stu-id="b8c34-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="b8c34-306">Für jede Verbindung wählt SignalR die beste Transportmethode aus, die sowohl der Server als auch der Client unterstützen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="b8c34-307">Öffnen Sie *StockTicker.js*.</span><span class="sxs-lookup"><span data-stu-id="b8c34-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="b8c34-308">Fügen Sie diese hervorgehobene Codezeile hinzu, um die Protokollierung unmittelbar vor dem Code zu aktivieren, der die Verbindung am Ende der Datei initialisiert:</span><span class="sxs-lookup"><span data-stu-id="b8c34-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="b8c34-309">Drücken Sie **F5,** um das Projekt auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="b8c34-310">Öffnen Sie das Entwicklertools-Fenster Ihres Browsers, und wählen Sie die Konsole aus, um die Protokolle anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="b8c34-311">Möglicherweise müssen Sie die Seite aktualisieren, um die Protokolle von SignalR anzuzeigen, die die Transportmethode für eine neue Verbindung aushandeln.</span><span class="sxs-lookup"><span data-stu-id="b8c34-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="b8c34-312">Wenn Sie Internet Explorer 10 unter Windows 8 (IIS 8) ausführen, lautet die Transportmethode **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="b8c34-313">Wenn Sie Internet Explorer 10 unter Windows 7 (IIS 7.5) ausführen, lautet die Transportmethode **iframe**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="b8c34-314">Wenn Sie Firefox 19 unter Windows 8 (IIS 8) ausführen, lautet die Transportmethode **WebSockets**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="b8c34-315">Installieren Sie in Firefox das Firebug-Add-In, um ein Konsolenfenster zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="b8c34-316">Wenn Sie Firefox 19 unter Windows 7 (IIS 7.5) ausführen, ist die Transportmethode **servergesendete** Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="b8c34-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="b8c34-317">Installieren Sie das StockTicker-Beispiel</span><span class="sxs-lookup"><span data-stu-id="b8c34-317">Install the StockTicker sample</span></span>

<span data-ttu-id="b8c34-318">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installiert die StockTicker-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="b8c34-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="b8c34-319">Das NuGet-Paket enthält mehr Funktionen als die vereinfachte Version, die Sie von Grund auf neu erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="b8c34-320">In diesem Abschnitt des Tutorials installieren Sie das NuGet-Paket und überprüfen die neuen Features und den Code, der sie implementiert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8c34-321">Wenn Sie das Paket installieren, ohne die vorherigen Schritte dieses Tutorials auszuführen, müssen Sie dem Projekt eine OWIN-Startklasse hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="b8c34-322">Diese Readme.txt-Datei für das NuGet-Paket erklärt diesen Schritt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="b8c34-323">Installieren des SignalR.Sample NuGet-Pakets</span><span class="sxs-lookup"><span data-stu-id="b8c34-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="b8c34-324">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="b8c34-325">Wählen Sie unter **NuGet Package Manager: SignalR.StockTicker**die Option **Durchsuchen**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="b8c34-326">Wählen Sie unter **Paketquelle** **nuget.org**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="b8c34-327">Geben Sie *SignalR.Sample* in das Suchfeld ein und wählen Sie **Microsoft.AspNet.SignalR.Sample** > **Install**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="b8c34-328">Erweitern Sie im **Projektmappen-Explorer**den Ordner *SignalR.Sample.*</span><span class="sxs-lookup"><span data-stu-id="b8c34-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="b8c34-329">Durch die Installation des SignalR.Sample-Pakets wurde der Ordner und sein Inhalt erstellt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="b8c34-330">Klicken Sie im Ordner *SignalR.Sample* mit der rechten Maustaste auf *StockTicker.html*, und wählen Sie dann **Als Startseite festlegen**aus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b8c34-331">Die Installation des SignalR.Sample NuGet-Pakets kann die Version von jQuery ändern, die Sie in Ihrem *Scripts-Ordner* haben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="b8c34-332">Die neue *Datei StockTicker.html,* die das Paket im *Ordner SignalR.Sample* installiert, ist mit der jQuery-Version synchron, die das Paket installiert, aber wenn Sie Ihre ursprüngliche *StockTicker.html-Datei* erneut ausführen möchten, müssen Sie möglicherweise zuerst den jQuery-Verweis im Skript-Tag aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b8c34-333">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="b8c34-333">Run the application</span></span>

 <span data-ttu-id="b8c34-334">Die Tabelle, die Sie in der ersten App gesehen haben, hatte nützliche Funktionen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="b8c34-335">Die vollständige Stock-Ticker-Anwendung zeigt neue Funktionen: ein horizontal scrollendes Fenster, das die Bestandsdaten und Aktien anzeigt, die ihre Farbe ändern, wenn sie steigen und fallen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="b8c34-336">Drücken Sie **F5** , um die App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="b8c34-337">Wenn Sie die App zum ersten Mal ausführen, wird der "Markt" "geschlossen" und Sie sehen eine statische Tabelle und ein Tickerfenster, das nicht scrollt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="b8c34-338">Wählen Sie **Open Market**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-338">Select **Open Market**.</span></span>

    ![Screenshot des Livetickers.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="b8c34-340">Das **Live Stock Ticker-Feld** beginnt horizontal zu scrollen, und der Server beginnt, regelmäßig Aktienkursänderungen nach dem Zufallsprinzip zu übertragen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="b8c34-341">Jedes Mal, wenn sich ein Aktienkurs ändert, aktualisiert die App sowohl die **Live Stock Table** als auch den Live Stock **Ticker**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="b8c34-342">Wenn die Kursänderung einer Aktie positiv ist, zeigt die App die Aktie mit grünem Hintergrund an.</span><span class="sxs-lookup"><span data-stu-id="b8c34-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="b8c34-343">Wenn die Änderung negativ ist, zeigt die App den Bestand mit einem roten Hintergrund an.</span><span class="sxs-lookup"><span data-stu-id="b8c34-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="b8c34-344">Wählen Sie **Markt schließen**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="b8c34-345">Die Tabellenaktualisierungen beenden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-345">The table updates stop.</span></span>

    * <span data-ttu-id="b8c34-346">Der Ticker hört auf zu scrollen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="b8c34-347">Klicken Sie auf **Zurücksetzen**.</span><span class="sxs-lookup"><span data-stu-id="b8c34-347">Select **Reset**.</span></span>

    * <span data-ttu-id="b8c34-348">Alle Bestandsdaten werden zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-348">All stock data is reset.</span></span>

    * <span data-ttu-id="b8c34-349">Die App stellt den Anfangszustand wieder her, bevor Preisänderungen gestartet werden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="b8c34-350">Kopieren Sie die URL aus dem Browser, öffnen Sie zwei weitere Browser, und fügen Sie die URLs in die Adressleisten ein.</span><span class="sxs-lookup"><span data-stu-id="b8c34-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="b8c34-351">In jedem Browser werden dieselben Daten dynamisch gleichzeitig aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b8c34-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="b8c34-352">Wenn Sie eines der Steuerelemente auswählen, reagieren alle Browser gleichzeitig auf die gleiche Weise.</span><span class="sxs-lookup"><span data-stu-id="b8c34-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="b8c34-353">Live Stock Ticker Anzeige</span><span class="sxs-lookup"><span data-stu-id="b8c34-353">Live Stock Ticker display</span></span>

<span data-ttu-id="b8c34-354">Die **Live Stock Ticker** Anzeige ist `<div>` eine ungeordnete Liste in einem Element, das von CSS-Stilen in eine einzelne Zeile formatiert ist.</span><span class="sxs-lookup"><span data-stu-id="b8c34-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="b8c34-355">Die App initialisiert und aktualisiert den Ticker auf die gleiche Weise `<li>` wie die Tabelle: durch Ersetzen von Platzhaltern in einer Vorlagenzeichenfolge und dynamisches Hinzufügen der `<li>` Elemente zum `<ul>` Element.</span><span class="sxs-lookup"><span data-stu-id="b8c34-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="b8c34-356">Die App enthält einen Bildlauf `animate` mit der funktion jQuery, um den `<div>`Rand links der ungeordneten Liste innerhalb der zu variieren.</span><span class="sxs-lookup"><span data-stu-id="b8c34-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="b8c34-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="b8c34-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="b8c34-358">Der Aktienticker HTML-Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="b8c34-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="b8c34-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="b8c34-360">Der Börsenticker CSS-Code:</span><span class="sxs-lookup"><span data-stu-id="b8c34-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="b8c34-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="b8c34-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="b8c34-362">Der jQuery-Code, mit dem er scrollen kann:</span><span class="sxs-lookup"><span data-stu-id="b8c34-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="b8c34-363">Zusätzliche Methoden auf dem Server, die der Client aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="b8c34-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="b8c34-364">Um der App mehr Flexibilität zu verleihen, gibt es zusätzliche Methoden, die die App aufrufen kann.</span><span class="sxs-lookup"><span data-stu-id="b8c34-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="b8c34-365">SignalR.Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="b8c34-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="b8c34-366">Die `StockTickerHub` Klasse definiert vier zusätzliche Methoden, die der Client aufrufen kann:</span><span class="sxs-lookup"><span data-stu-id="b8c34-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="b8c34-367">Die App `OpenMarket` `CloseMarket`ruft `Reset` , und als Reaktion auf die Schaltflächen oben auf der Seite auf.</span><span class="sxs-lookup"><span data-stu-id="b8c34-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="b8c34-368">Sie veranschaulichen das Muster eines Clients, der eine Statusänderung auslöst, die sofort an alle Clients weitergegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b8c34-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="b8c34-369">Jede dieser Methoden ruft eine `StockTicker` Methode in der Klasse auf, die die Änderung des Marktstatus verursacht, und sendet dann den neuen Status.</span><span class="sxs-lookup"><span data-stu-id="b8c34-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="b8c34-370">SignalR.Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="b8c34-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="b8c34-371">In `StockTicker` der Klasse behält die App den `MarketState` Status des `MarketState` Marktes mit einer Eigenschaft bei, die einen Enumeratwert zurückgibt:</span><span class="sxs-lookup"><span data-stu-id="b8c34-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="b8c34-372">Jede der Methoden, die den Marktstatus ändern, `StockTicker` tun dies innerhalb eines Sperrblocks, da die Klasse threadsicher sein muss:</span><span class="sxs-lookup"><span data-stu-id="b8c34-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="b8c34-373">Um sicherzustellen, dass dieser Code `_marketState` threadsicher ist, `MarketState` wird `volatile`das Feld, das die angegebene Eigenschaft unterstützt:</span><span class="sxs-lookup"><span data-stu-id="b8c34-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="b8c34-374">Die `BroadcastMarketStateChange` `BroadcastMarketReset` und-Methoden ähneln der BroadcastStockPrice-Methode, die Sie bereits gesehen haben, außer sie rufen verschiedene Methoden auf, die auf dem Client definiert sind:</span><span class="sxs-lookup"><span data-stu-id="b8c34-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="b8c34-375">Zusätzliche Funktionen auf dem Client, die der Server aufrufen kann</span><span class="sxs-lookup"><span data-stu-id="b8c34-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="b8c34-376">Die `updateStockPrice` Funktion verarbeitet nun sowohl die Tabelle als `jQuery.Color` auch die Tickeranzeige und blinkt in rot-grünen Farben.</span><span class="sxs-lookup"><span data-stu-id="b8c34-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="b8c34-377">Neue Funktionen in *SignalR.StockTicker.js* aktivieren und deaktivieren die Schaltflächen basierend auf dem Marktstatus.</span><span class="sxs-lookup"><span data-stu-id="b8c34-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="b8c34-378">Sie stoppen oder starten auch das **Live Stock Ticker** horizontales Scrollen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="b8c34-379">Da viele Funktionen zu `ticker.client`hinzugefügt werden, verwendet die App die [funktion jQuery extend,](http://api.jquery.com/jQuery.extend/) um sie hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="b8c34-380">Zusätzliche Clienteinrichtung nach dem Herstellen der Verbindung</span><span class="sxs-lookup"><span data-stu-id="b8c34-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="b8c34-381">Nachdem der Client die Verbindung hergestellt hat, muss noch einiges an Arbeit zu erledigen sein:</span><span class="sxs-lookup"><span data-stu-id="b8c34-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="b8c34-382">Finden Sie heraus, ob der Markt `marketOpened` geöffnet `marketClosed` oder geschlossen ist, um die entsprechende Funktion aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="b8c34-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="b8c34-383">Fügen Sie die Servermethodenaufrufe an die Schaltflächen an.</span><span class="sxs-lookup"><span data-stu-id="b8c34-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="b8c34-384">Die Servermethoden werden erst mit den Schaltflächen verdrahtet, nachdem die App die Verbindung hergestellt hat.</span><span class="sxs-lookup"><span data-stu-id="b8c34-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="b8c34-385">Es ist so, dass der Code die Servermethoden nicht aufrufen kann, bevor sie verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="b8c34-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8c34-386">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b8c34-386">Additional resources</span></span>

<span data-ttu-id="b8c34-387">In diesem Tutorial haben Sie gelernt, wie Sie eine SignalR-Anwendung programmieren, die Nachrichten vom Server an alle verbundenen Clients überträgt.</span><span class="sxs-lookup"><span data-stu-id="b8c34-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="b8c34-388">Jetzt können Sie Nachrichten regelmäßig und als Reaktion auf Benachrichtigungen von jedem Client senden.</span><span class="sxs-lookup"><span data-stu-id="b8c34-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="b8c34-389">Sie können das Konzept der Singleton-Instanz mit mehreren Threads verwenden, um den Serverstatus in Multiplayer-Onlinespielszenarien beizubehalten.</span><span class="sxs-lookup"><span data-stu-id="b8c34-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="b8c34-390">Ein Beispiel finden Sie [im ShootR-Spiel basierend auf SignalR](https://github.com/NTaylorMullen/ShootR).</span><span class="sxs-lookup"><span data-stu-id="b8c34-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="b8c34-391">Tutorials, die Peer-to-Peer-Kommunikationsszenarien zeigen, finden Sie unter [Erste Schritte mit SignalR](introduction-to-signalr.md) und [Echtzeitaktualisierung mit SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="b8c34-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="b8c34-392">Weitere Informationen zu SignalR finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="b8c34-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="b8c34-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="b8c34-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="b8c34-394">SignalR-Projekt</span><span class="sxs-lookup"><span data-stu-id="b8c34-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="b8c34-395">SignalR GitHub und Samples</span><span class="sxs-lookup"><span data-stu-id="b8c34-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="b8c34-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="b8c34-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="b8c34-397">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="b8c34-397">Next steps</span></span>

<span data-ttu-id="b8c34-398">In diesem Tutorial führen Sie Folgendes durch:</span><span class="sxs-lookup"><span data-stu-id="b8c34-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8c34-399">Erstellt das Projekt</span><span class="sxs-lookup"><span data-stu-id="b8c34-399">Created the project</span></span>
> * <span data-ttu-id="b8c34-400">Einrichten des Servercodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-400">Set up the server code</span></span>
> * <span data-ttu-id="b8c34-401">Geprüft den Servercode</span><span class="sxs-lookup"><span data-stu-id="b8c34-401">Examined the server code</span></span>
> * <span data-ttu-id="b8c34-402">Einrichten des Clientcodes</span><span class="sxs-lookup"><span data-stu-id="b8c34-402">Set up the client code</span></span>
> * <span data-ttu-id="b8c34-403">Geprüft den Clientcode</span><span class="sxs-lookup"><span data-stu-id="b8c34-403">Examined the client code</span></span>
> * <span data-ttu-id="b8c34-404">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="b8c34-404">Tested the application</span></span>
> * <span data-ttu-id="b8c34-405">Aktivierte Protokollierung</span><span class="sxs-lookup"><span data-stu-id="b8c34-405">Enabled logging</span></span>

<span data-ttu-id="b8c34-406">Fahren Sie mit dem nächsten Artikel fort, um zu erfahren, wie Sie eine Echtzeit-Webanwendung erstellen, die ASP.NET SignalR 2 verwendet.</span><span class="sxs-lookup"><span data-stu-id="b8c34-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b8c34-407">Erstellen einer Echtzeit-Web-App mit SignalR</span><span class="sxs-lookup"><span data-stu-id="b8c34-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
