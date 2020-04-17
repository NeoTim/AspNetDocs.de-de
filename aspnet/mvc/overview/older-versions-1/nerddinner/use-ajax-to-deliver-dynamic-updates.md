---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Verwenden von AJAX zum Bereitstellen dynamischer Updates | Microsoft Docs
author: rick-anderson
description: Schritt 10 implementiert Unterstützung für eingeloggte Benutzer, um IHR Interesse an einem Abendessen zu erreichen, indem ein Ajax-basierter Ansatz verwendet wird, der in das Dinner-Detail integriert ist...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541246"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="31097-103">Bereitstellen von dynamischen Updates mithilfe von AJAX</span><span class="sxs-lookup"><span data-stu-id="31097-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="31097-104">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="31097-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="31097-105">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="31097-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="31097-106">Dies ist Schritt 10 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.</span><span class="sxs-lookup"><span data-stu-id="31097-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="31097-107">Schritt 10 implementiert Unterstützung für eingeloggte Benutzer, um IHR Interesse an einem Abendessen zu nutzen, indem ein Ajax-basierter Ansatz verwendet wird, der in die Dinner-Details-Seite integriert ist.</span><span class="sxs-lookup"><span data-stu-id="31097-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="31097-108">Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.</span><span class="sxs-lookup"><span data-stu-id="31097-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="31097-109">NerdDinner Schritt 10: AJAX ermöglicht RSVPs akzeptiert</span><span class="sxs-lookup"><span data-stu-id="31097-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="31097-110">Lassen Sie uns nun Unterstützung für eingeloggte Benutzer implementieren, um IHR Interesse an einem Abendessen zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="31097-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="31097-111">Wir ermöglichen dies mithilfe eines AJAX-basierten Ansatzes, der in die Details des Abendessens integriert ist.</span><span class="sxs-lookup"><span data-stu-id="31097-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="31097-112">Geben an, ob der Benutzer RSVP'd ist</span><span class="sxs-lookup"><span data-stu-id="31097-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="31097-113">Benutzer können die URL */Dinners/Details/[id*] besuchen, um Details zu einem bestimmten Abendessen zu sehen:</span><span class="sxs-lookup"><span data-stu-id="31097-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="31097-114">Die Aktionsmethode Details() wird wie folgt implementiert:</span><span class="sxs-lookup"><span data-stu-id="31097-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="31097-115">Unser erster Schritt zur Implementierung der RSVP-Unterstützung besteht darin, unserem Dinner-Objekt eine "IsUserRegistered(username)"-Hilfsmethode hinzuzufügen (innerhalb der Dinner.cs Teilklasse, die wir zuvor erstellt haben).</span><span class="sxs-lookup"><span data-stu-id="31097-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="31097-116">Diese Hilfsmethode gibt true oder false zurück, je nachdem, ob der Benutzer derzeit RSVP'd für das Dinner ist:</span><span class="sxs-lookup"><span data-stu-id="31097-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="31097-117">Anschließend können wir den folgenden Code zu unserer Detail.aspx-Ansichtsvorlage hinzufügen, um eine entsprechende Meldung anzuzeigen, die angibt, ob der Benutzer für das Ereignis registriert ist oder nicht:</span><span class="sxs-lookup"><span data-stu-id="31097-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="31097-118">Und jetzt, wenn ein Benutzer ein Abendessen besucht, werden sie für sie registriert werden, wird diese Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="31097-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="31097-119">Und wenn sie ein Dinner besuchen, sind sie nicht registriert für sie sehen die folgende Nachricht:</span><span class="sxs-lookup"><span data-stu-id="31097-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="31097-120">Implementieren der Registeraktionsmethode</span><span class="sxs-lookup"><span data-stu-id="31097-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="31097-121">Fügen wir nun die Funktionen hinzu, die erforderlich sind, um Benutzern RSVP für ein Abendessen auf der Detailseite zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="31097-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="31097-122">Um dies zu implementieren, erstellen wir eine neue "RSVPController"-Klasse, indem wir&gt;mit der rechten Maustaste auf das Verzeichnis "Controller" klicken und den Menübefehl "Add- Controller" auswählen.</span><span class="sxs-lookup"><span data-stu-id="31097-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="31097-123">Wir implementieren eine "Register"-Aktionsmethode innerhalb der neuen RSVPController-Klasse, die eine ID für ein Dinner als Argument annimmt, das entsprechende Dinner-Objekt abruft, überprüft, ob sich der angemeldete Benutzer derzeit in der Liste der Benutzer befindet, die sich dafür registriert haben, und wenn nicht, fügt er ein RSVP-Objekt für sie hinzu:</span><span class="sxs-lookup"><span data-stu-id="31097-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="31097-124">Beachten Sie oben, wie wir eine einfache Zeichenfolge als Ausgabe der Aktionsmethode zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="31097-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="31097-125">Wir hätten diese Nachricht in eine Ansichtsvorlage einbetten können – aber da sie so klein ist, verwenden wir einfach die Content()-Hilfsmethode für die Controller-Basisklasse und geben eine Zeichenfolgennachricht wie oben zurück.</span><span class="sxs-lookup"><span data-stu-id="31097-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="31097-126">Aufrufen der RSVPForEvent-Aktionsmethode mithilfe von AJAX</span><span class="sxs-lookup"><span data-stu-id="31097-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="31097-127">Wir verwenden AJAX, um die Registrierungsaktionsmethode aus unserer Detailansicht aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="31097-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="31097-128">Dies zu implementieren ist ziemlich einfach.</span><span class="sxs-lookup"><span data-stu-id="31097-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="31097-129">Zuerst fügen wir zwei Skriptbibliotheksverweise hinzu:</span><span class="sxs-lookup"><span data-stu-id="31097-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="31097-130">Die erste Bibliothek verweist auf die kernASP.NET Client-seitige Skriptbibliothek von AJAX.</span><span class="sxs-lookup"><span data-stu-id="31097-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="31097-131">Diese Datei hat eine Größe von ca. 24k (komprimiert) und enthält die clientseitige AJAX-Kernfunktionalität.</span><span class="sxs-lookup"><span data-stu-id="31097-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="31097-132">Die zweite Bibliothek enthält Dienstprogrammfunktionen, die in die integrierten AJAX-Hilfsmethoden von ASP.NET MVC integriert werden (die wir in Kürze verwenden werden).</span><span class="sxs-lookup"><span data-stu-id="31097-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="31097-133">Wir können dann den zuvor hinzugefügten Ansichtsvorlagencode aktualisieren, sodass wir anstelle einer Meldung "Sie sind nicht für dieses Ereignis registriert" stattdessen einen Link rendern, der bei einem Push-Aufruf einen AJAX-Aufruf ausführt, der unsere RSVPForEvent-Aktionsmethode auf unserem RSVP-Controller und RSVPs-Benutzer aufruft:</span><span class="sxs-lookup"><span data-stu-id="31097-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="31097-134">Die oben verwendete Ajax.ActionLink()-Hilfsmethode ist integriert ASP.NET MVC und ähnelt der Html.ActionLink()-Hilfsmethode, mit der Ausnahme, dass sie anstelle einer Standardnavigation einen AJAX-Aufruf der Aktionsmethode ausführt, wenn auf den Link geklickt wird.</span><span class="sxs-lookup"><span data-stu-id="31097-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="31097-135">Oben rufen wir die Aktionsmethode "Registrieren" auf dem "RSVP"-Controller auf und übergeben die DinnerID als "id"-Parameter.</span><span class="sxs-lookup"><span data-stu-id="31097-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="31097-136">Der letzte AjaxOptions-Parameter, den wir übergeben, zeigt an, dass wir &lt;&gt; den von der Aktionsmethode zurückgegebenen Inhalt übernehmen und das HTML-div-Element auf der Seite aktualisieren möchten, dessen ID "rsvpmsg" ist.</span><span class="sxs-lookup"><span data-stu-id="31097-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="31097-137">Und jetzt, wenn ein Benutzer zu einem Abendessen surft, sind sie noch nicht registriert, noch sehen sie einen Link zu RSVP dafür:</span><span class="sxs-lookup"><span data-stu-id="31097-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="31097-138">Wenn sie auf den Link "RSVP für dieses Ereignis" klicken, werden Sie einen AJAX-Aufruf an die Register-Aktionsmethode auf dem RSVP-Controller ausführen, und wenn sie abgeschlossen ist, wird eine aktualisierte Meldung wie folgt angezeigt:</span><span class="sxs-lookup"><span data-stu-id="31097-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="31097-139">Die Netzwerkbandbreite und der Datenverkehr, die bei diesem AJAX-Aufruf erforderlich sind, sind wirklich leicht.</span><span class="sxs-lookup"><span data-stu-id="31097-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="31097-140">Wenn der Benutzer auf den Link "RSVP für dieses Ereignis" klickt, wird eine kleine HTTP-POST-Netzwerkanforderung an die */Dinners/Register/1-URL* gestellt, die wie unten auf dem Draht aussieht:</span><span class="sxs-lookup"><span data-stu-id="31097-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="31097-141">Und die Antwort unserer Register-Aktionsmethode lautet einfach:</span><span class="sxs-lookup"><span data-stu-id="31097-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="31097-142">Dieser leichte Anruf ist schnell und funktioniert auch über ein langsames Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="31097-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="31097-143">Hinzufügen einer jQuery-Animation</span><span class="sxs-lookup"><span data-stu-id="31097-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="31097-144">Die von uns implementierte AJAX-Funktionalität funktioniert gut und schnell.</span><span class="sxs-lookup"><span data-stu-id="31097-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="31097-145">Manchmal kann es jedoch so schnell gehen, dass ein Benutzer möglicherweise nicht bemerkt, dass der RSVP-Link durch neuen Text ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="31097-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="31097-146">Um das Ergebnis etwas offensichtlicher zu machen, können wir eine einfache Animation hinzufügen, um die Aufmerksamkeit auf die Update-Nachricht zu lenken.</span><span class="sxs-lookup"><span data-stu-id="31097-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="31097-147">Die Standardvorlage ASP.NET MVC-Projektenthältumfasst umfasst jQuery – eine ausgezeichnete (und sehr beliebte) Open-Source-JavaScript-Bibliothek, die auch von Microsoft unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="31097-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="31097-148">jQuery bietet eine Reihe von Funktionen, einschließlich einer schönen HTML-DOM-Auswahl und Effektbibliothek.</span><span class="sxs-lookup"><span data-stu-id="31097-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="31097-149">Um jQuery zu verwenden, fügen wir zuerst einen Skriptverweis hinzu.</span><span class="sxs-lookup"><span data-stu-id="31097-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="31097-150">Da wir jQuery an einer Vielzahl von Stellen innerhalb unserer Website verwenden werden, fügen wir den Skriptverweis in unserer Site.master-Master-Seitendatei hinzu, damit alle Seiten ihn verwenden können.</span><span class="sxs-lookup"><span data-stu-id="31097-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="31097-151">*Tipp: Stellen Sie sicher, dass Sie den JavaScript-Hotfix intellisense für VS 2008 SP1 installiert haben, der eine umfassendere intellisense-Unterstützung für JavaScript-Dateien (einschließlich jQuery) ermöglicht. Sie können es herunterladen von:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="31097-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="31097-152">Code, der mit JQuery geschrieben wurde, verwendet häufig eine globale JavaScript-Methode ,,,,,die ein oder mehrere HTML-Elemente mithilfe eines CSS-Selektors abruft.</span><span class="sxs-lookup"><span data-stu-id="31097-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="31097-153">Zum Beispiel wählt *"#rsvpmsg")* ein beliebiges HTML-Element mit der ID rsvpmsg aus, während *"(".something"* alle Elemente mit dem CSS-Klassennamen "something" auswählen würde.</span><span class="sxs-lookup"><span data-stu-id="31097-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="31097-154">Sie können auch erweiterte Abfragen wie "Alle überprüften Optionsfelder zurückgeben" mit einer Selektorabfrage schreiben, z. B.: *."input[@type@checked=radio][ ]")*.</span><span class="sxs-lookup"><span data-stu-id="31097-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="31097-155">Nachdem Sie Elemente ausgewählt haben, können Sie Methoden aufrufen, um Maßnahmen zu ergreifen, wie z. B. das Ausblenden von Elementen: *"#rsvpmsg").*</span><span class="sxs-lookup"><span data-stu-id="31097-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="31097-156">Für unser RSVP-Szenario definieren wir eine einfache JavaScript-Funktion namens "AnimateRSVPMessage", die &lt;&gt; die "rsvpmsg" div auswählt und die Größe des Textinhalts animiert.</span><span class="sxs-lookup"><span data-stu-id="31097-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="31097-157">Der folgende Code startet den Text klein und bewirkt dann, dass er über einen Zeitraum von 400 Millisekunden zunimmt:</span><span class="sxs-lookup"><span data-stu-id="31097-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="31097-158">Wir können dann diese JavaScript-Funktion verdrahten, die aufgerufen werden soll, nachdem unser AJAX-Aufruf erfolgreich abgeschlossen wurde, indem wir seinen Namen an unsere Ajax.ActionLink()-Hilfsmethode übergeben (über die AjaxOptions "OnSuccess"-Ereigniseigenschaft):</span><span class="sxs-lookup"><span data-stu-id="31097-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="31097-159">Und jetzt, wenn auf den Link "RSVP für dieses Ereignis" geklickt wird und unser AJAX-Aufruf erfolgreich abgeschlossen wird, wird die zurückgesendete Inhaltsnachricht animiert und groß werden:</span><span class="sxs-lookup"><span data-stu-id="31097-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="31097-160">Zusätzlich zur Bereitstellung eines "OnSuccess"-Ereignisses macht das AjaxOptions-Objekt OnBegin-, OnFailure- und OnComplete-Ereignisse verfügbar, die Sie verarbeiten können (zusammen mit einer Vielzahl anderer Eigenschaften und nützlicher Optionen).</span><span class="sxs-lookup"><span data-stu-id="31097-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="31097-161">Bereinigung - Refactor out einer RSVP-Teilansicht</span><span class="sxs-lookup"><span data-stu-id="31097-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="31097-162">Unsere Detailansichtsvorlage beginnt ein wenig lang zu werden, was Überstunden machen es ein wenig schwieriger zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="31097-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="31097-163">Um die Lesbarkeit des Codes zu verbessern, erstellen wir abschließend eine Teilansicht – RSVPStatus.ascx –, die den gesamten RSVP-Ansichtscode für unsere Detailseite kapselt.</span><span class="sxs-lookup"><span data-stu-id="31097-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="31097-164">Wir können dies tun, indem Wir mit der rechten Maustaste&gt;auf den Ordner "Views"-Dinners klicken und dann den Menübefehl "Hinzufügen" auswählen.</span><span class="sxs-lookup"><span data-stu-id="31097-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="31097-165">Wir lassen es ein Dinner-Objekt als sein stark typisiertes ViewModel nehmen.</span><span class="sxs-lookup"><span data-stu-id="31097-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="31097-166">Wir können dann die RSVP-Inhalte aus unserer Details.aspx-Ansicht kopieren/einfügen.</span><span class="sxs-lookup"><span data-stu-id="31097-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="31097-167">Sobald wir dies getan haben, erstellen wir auch eine weitere Teilansicht – EditAndDeleteLinks.ascx –, die unseren Linkansichtscode bearbeiten und löschen kapselt.</span><span class="sxs-lookup"><span data-stu-id="31097-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="31097-168">Wir haben auch ein Dinner-Objekt als sein stark typisiertes ViewModel und kopieren/einfügen der Befolgende Edit and Delete-Logik aus unserer Details.aspx-Ansicht.</span><span class="sxs-lookup"><span data-stu-id="31097-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="31097-169">Unsere Detailansichtsvorlage kann dann nur zwei Html.RenderPartial()-Methodenaufrufe unten enthalten:</span><span class="sxs-lookup"><span data-stu-id="31097-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="31097-170">Dadurch wird der Code sauberer zu lesen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="31097-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="31097-171">Nächster Schritt</span><span class="sxs-lookup"><span data-stu-id="31097-171">Next Step</span></span>

<span data-ttu-id="31097-172">Sehen wir uns nun an, wie wir AJAX noch weiter nutzen können, und fügen Sie unserer Anwendung interaktive Mapping-Unterstützung hinzu.</span><span class="sxs-lookup"><span data-stu-id="31097-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="31097-173">[Zurück](secure-applications-using-authentication-and-authorization.md)
> [Weiter](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="31097-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
