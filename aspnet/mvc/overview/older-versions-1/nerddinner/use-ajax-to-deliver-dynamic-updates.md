---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Bereitstellen von dynamischen Updates mithilfe von AJAX | Microsoft-Dokumentation
author: microsoft
description: Schritt 10-implementiert die Unterstützung für den angemeldeten Benutzer RSVP ihr Interesse an Ihre Teilnahme an einem Dinner, die mit einem Ajax-basierten Ansatz, integriert in die Dinner-Details...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128233"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="4395d-103">Bereitstellen von dynamischen Updates mithilfe von AJAX</span><span class="sxs-lookup"><span data-stu-id="4395d-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="4395d-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4395d-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="4395d-105">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="4395d-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="4395d-106">Dies ist Schritt 10 ein kostenloses ["NerdDinner"-webanwendungstutorial](introducing-the-nerddinner-tutorial.md) , die führt – Exemplarische Vorgehensweise erstellen eine kleine, jedoch abgeschlossen haben, Web-Anwendung mithilfe von ASP.NET MVC-1.</span><span class="sxs-lookup"><span data-stu-id="4395d-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="4395d-107">Schritt 10-implementiert die Unterstützung für den angemeldeten Benutzer RSVP ihr Interesse an Ihre Teilnahme an einem Dinner, die mit einem Ajax-basierten Ansatz, der innerhalb der Dinner-Detailseite integriert.</span><span class="sxs-lookup"><span data-stu-id="4395d-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="4395d-108">Wenn Sie ASP.NET MVC 3 verwenden, sollten Sie Sie folgen den [erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) Tutorials.</span><span class="sxs-lookup"><span data-stu-id="4395d-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="4395d-109">NerdDinner Schritt 10: Aktivieren von Bestätigungen AJAX akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="4395d-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="4395d-110">Nun implementieren wir Unterstützung für angemeldete Benutzer auf ihr Interesse an Ihre Teilnahme an einem Dinner zu antworten.</span><span class="sxs-lookup"><span data-stu-id="4395d-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="4395d-111">Dadurch wird es mit einem AJAX-basierten Ansatz, der innerhalb der Dinner-Detailseite integriert.</span><span class="sxs-lookup"><span data-stu-id="4395d-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="4395d-112">Gibt an, ob der Benutzer um Antwort gebeten wird</span><span class="sxs-lookup"><span data-stu-id="4395d-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="4395d-113">Benutzer besuchen können die *"/ dinners" / Details / [Id*] URL, um Details zu einem bestimmten Dinner anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="4395d-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="4395d-114">Die Details() Action-Methode wird implementiert, wie folgt:</span><span class="sxs-lookup"><span data-stu-id="4395d-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="4395d-115">Im ersten Schritt RSVP-Unterstützung implementieren werden das Dinner-Objekt (in der partiellen Dinner.cs-Klasse, die wir zuvor erstellt) eine Hilfsmethode "IsUserRegistered(username)" hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="4395d-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="4395d-116">"True" oder "false", je nachdem, ob der Benutzer derzeit für das Dinner um Antwort gebeten wird, gibt diese Hilfsmethode zurück:</span><span class="sxs-lookup"><span data-stu-id="4395d-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="4395d-117">Wir können klicken Sie dann den folgenden Code hinzufügen, um unsere Details.aspx-View-Vorlage zum Anzeigen von einer entsprechenden Meldung angezeigt, der angibt, ob der Benutzer registriert ist oder nicht für das Ereignis:</span><span class="sxs-lookup"><span data-stu-id="4395d-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="4395d-118">Und nun, wenn ein Benutzer eine Dinner besucht, für die sie registriert sind, sie erhalten diese Nachricht:</span><span class="sxs-lookup"><span data-stu-id="4395d-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="4395d-119">Und wenn sie eine Dinner sie nicht registriert besuchen, sind für die sie sehen die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="4395d-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="4395d-120">Implementieren die Register-Aktion-Methode</span><span class="sxs-lookup"><span data-stu-id="4395d-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="4395d-121">Fügen Sie die erforderlichen Funktionen zur Benutzern ermöglichen, die sich auf der Detailseite zum RSVP zu einem Dinner jetzt aus.</span><span class="sxs-lookup"><span data-stu-id="4395d-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="4395d-122">Um dies zu implementieren, werden wir eine neue "RSVPController"-Klasse erstellen, indem Sie mit der rechten Maustaste auf das Verzeichnis \Controllers und Auswählen der hinzufügen -&gt;Kontextmenübefehl von "Controller".</span><span class="sxs-lookup"><span data-stu-id="4395d-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="4395d-123">Wir implementieren eine Aktionsmethode "Registrieren", in der neuen RSVPController-Klasse, die eine Id zu einem Dinner als Argument akzeptiert, wird das entsprechende Dinner-Objekt, überprüft, wenn der angemeldete Benutzer derzeit in der Liste der Benutzer ist, die für sie registriert haben und ein RSVP-Objekt wird nicht für sie hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="4395d-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="4395d-124">Beachten Sie, oben, wie wir eine einfache Zeichenfolge als Ausgabe der Aktionsmethode zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="4395d-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="4395d-125">Wir konnten diese Nachricht in eine ansichtsvorlage – eingebettet haben, aber da es so klein ist verwenden wir die Content()-Hilfsmethode für die Basisklasse für Controller und zurück, der eine zeichenfolgenmeldung wie oben.</span><span class="sxs-lookup"><span data-stu-id="4395d-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="4395d-126">Aufruf der RSVPForEvent-Aktionsmethode, die mithilfe von AJAX</span><span class="sxs-lookup"><span data-stu-id="4395d-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="4395d-127">Wir verwenden AJAX, die Register-Aktion-Methode aus unserer Ansicht aufrufen.</span><span class="sxs-lookup"><span data-stu-id="4395d-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="4395d-128">Implementieren Dies ist recht einfach.</span><span class="sxs-lookup"><span data-stu-id="4395d-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="4395d-129">Zunächst fügen wir zwei Skriptverweise-Bibliothek:</span><span class="sxs-lookup"><span data-stu-id="4395d-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="4395d-130">Die erste Bibliothek verweist auf die ASP.NET AJAX Clientskript-Kernbibliothek.</span><span class="sxs-lookup"><span data-stu-id="4395d-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="4395d-131">Diese Datei ist ca. 24 KB Größe (komprimiert) und Core clientseitigen AJAX-Funktionen enthält.</span><span class="sxs-lookup"><span data-stu-id="4395d-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="4395d-132">Die zweite-Bibliothek enthält Hilfsfunktionen, die Integration in integrierten ASP.NETs AJAX-Hilfsmethoden (, verwenden wir in Kürze).</span><span class="sxs-lookup"><span data-stu-id="4395d-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="4395d-133">Wir können, und klicken Sie dann Update Vorlagencode anzeigen, die wir zuvor hinzugefügt haben, sodass statt Ausgeben einer Meldung "Sie sind nicht für dieses Ereignis registriert", wir stattdessen einem Link, der gerendert werden, wenn mithilfe von Push übertragen soll einen AJAX-Aufruf ausführt, der unsere RSVPForEvent Aktionsmethode auf unsere RSVP Controller aufruft und den Benutzer RSVPs:</span><span class="sxs-lookup"><span data-stu-id="4395d-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="4395d-134">Die oben verwendete Ajax.ActionLink()-Hilfsmethode wird erstellt in ASP.NET MVC und ähnelt die Hilfsmethode Html.ActionLink(), anstatt eine standard-Navigation einen AJAX-Aufruf an die Aktionsmethode vereinfacht, wenn auf der Link geklickt wird.</span><span class="sxs-lookup"><span data-stu-id="4395d-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="4395d-135">Über die Aktionsmethode "Registrieren" auf dem Controller "Bestätigung" aufrufen und wir die DinnerID als Parameter "Id" an sie übergibt.</span><span class="sxs-lookup"><span data-stu-id="4395d-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="4395d-136">Der letzte AjaxOptions-Parameter übergeben werden gibt an, dass wir den Inhalt von der Aktionsmethode zurückgegeben, und aktualisieren den HTML-Code &lt;Div&gt; Element auf der Seite mit der Id ist "Rsvpmsg".</span><span class="sxs-lookup"><span data-stu-id="4395d-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="4395d-137">Und jetzt beim Benutzer zu einem Dinner navigiert sie sind nicht für registriert, aber sie erhalten einen Link zur Bestätigung dafür:</span><span class="sxs-lookup"><span data-stu-id="4395d-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="4395d-138">Wenn sie den Link "RSVP für dieses Ereignis" klicken sie erstellen einen AJAX-Aufruf an die Register-Aktion-Methode auf dem Controller RSVP und bei Abschluss sehen sie eine aktualisierte Meldung wie die folgende:</span><span class="sxs-lookup"><span data-stu-id="4395d-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="4395d-139">Die Netzwerkbandbreite und der Datenverkehr bei der dieser AJAX-Aufruf sehr Schlank ist.</span><span class="sxs-lookup"><span data-stu-id="4395d-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="4395d-140">Klickt der Benutzer auf den Link "RSVP für dieses Ereignis", kleine HTTP POST-Netzwerk angefordert wird die */Dinners/Register/1* URL, die bei der Übertragung unter aussieht:</span><span class="sxs-lookup"><span data-stu-id="4395d-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="4395d-141">Und die Antwort auf unsere Register-Aktion-Methode ist einfach:</span><span class="sxs-lookup"><span data-stu-id="4395d-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="4395d-142">Dieser einfache Aufruf ist schnell und sogar über ein langsames Netzwerk funktioniert.</span><span class="sxs-lookup"><span data-stu-id="4395d-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="4395d-143">Hinzufügen von jQuery Animation</span><span class="sxs-lookup"><span data-stu-id="4395d-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="4395d-144">Die AJAX-Funktionalität, die wir implementiert haben, funktioniert gut und schnell.</span><span class="sxs-lookup"><span data-stu-id="4395d-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="4395d-145">Manchmal kann es so schnell weiter, jedoch passieren, dass ein Benutzer nicht bemerkt, dass die RSVP-Verknüpfung durch neuen Text ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="4395d-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="4395d-146">Um das Ergebnis ein wenig sichtbarer machen können wir eine einfache Animation, um die Aufmerksamkeit auf das Aktualisieren der Nachricht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="4395d-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="4395d-147">Die standardmäßige ASP.NET MVC-Projektvorlage enthält jQuery – eine hervorragende (und sehr beliebtes)-open-Source-JavaScript-Bibliothek, die auch von Microsoft unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="4395d-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="4395d-148">jQuery bietet es sich um eine Reihe von Features, darunter eine gute HTML-DOM-Auswahl und Effekte-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="4395d-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="4395d-149">Verwendung von jQuery fügen wir zuerst einen Skriptverweis auf sie.</span><span class="sxs-lookup"><span data-stu-id="4395d-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="4395d-150">Da wir hierfür jQuery in einer Vielzahl von Orten innerhalb unserer Website verwenden, fügen den Skriptverweis in unserer Masterseitendatei Site.master wir so, dass alle Seiten, die sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4395d-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="4395d-151">*Tipp: Stellen Sie sicher, dass Sie den JavaScript-Intellisense-Hotfix für Visual Studio 2008 SP1 installiert haben, die es umfangreichere Intellisense-Unterstützung für JavaScript-Dateien ermöglicht (einschließlich jQuery). Sie können es aus: http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="4395d-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="4395d-152">Geschrieben, häufig mit der JQuery-Code verwendet einen globalen "$ ()" JavaScript-Methode, die eine oder mehrere HTML-Elemente, die mit einem CSS-Selektor abruft.</span><span class="sxs-lookup"><span data-stu-id="4395d-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="4395d-153">Z. B. *$("#rsvpmsg")* wählt alle HTML-Element mit der Id der Rsvpmsg, während *$(".something")* wählen alle Elemente mit CSS "etwas" Klassenname.</span><span class="sxs-lookup"><span data-stu-id="4395d-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="4395d-154">Sie können auch komplexere Abfragen wie "alle aktivierten Optionsfelds return" schreiben mithilfe einer Abfrage Selektor wie: *$("Input [@type= Radio] [@checked]")*.</span><span class="sxs-lookup"><span data-stu-id="4395d-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="4395d-155">Wenn Sie Elemente ausgewählt haben, können Sie Methoden aufrufen, darauf zu ergreifen, wie sie verbergen: *$("#rsvpmsg").hide();*</span><span class="sxs-lookup"><span data-stu-id="4395d-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="4395d-156">In diesem Szenario RSVP definieren wir eine einfache JavaScript-Funktion, die mit dem Namen "AnimateRSVPMessage", die die "Rsvpmsg" auswählt &lt;Div&gt; und die Größe seines Textinhalts animiert.</span><span class="sxs-lookup"><span data-stu-id="4395d-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="4395d-157">Die folgenden Code wird gestartet, die kleinen Text ein, und bewirkt, dass sie über einen Zeitraum von 400 Millisekunden zu erhöhen:</span><span class="sxs-lookup"><span data-stu-id="4395d-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="4395d-158">Wir können dann über das Netzwerk von diesem JavaScript-Funktion, die aufgerufen werden, wenn unsere AJAX-Aufruf erfolgreich abgeschlossen wurde, übergeben Sie den Namen an unsere Ajax.ActionLink()-Hilfsmethode (mithilfe der AjaxOptions "OnSuccess" Ereigniseigenschaft):</span><span class="sxs-lookup"><span data-stu-id="4395d-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="4395d-159">Und jetzt den Link "RSVP für dieses Ereignis" geklickt wird, und unsere AJAX-Aufruf wird erfolgreich abgeschlossen, die Inhalt gesendete Nachricht Back wird animieren und anwachsen:</span><span class="sxs-lookup"><span data-stu-id="4395d-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="4395d-160">Zusätzlich zur Bereitstellung eines Ereignisses "OnSuccess", stellt der AjaxOptions-Objekt OnBegin OnFailure und OnComplete-Ereignisse, die Sie (zusammen mit verschiedenen anderen Eigenschaften und nützliche Optionen) behandeln können.</span><span class="sxs-lookup"><span data-stu-id="4395d-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="4395d-161">Bereinigung - Umgestaltung, eine Teilansicht mit Antworten</span><span class="sxs-lookup"><span data-stu-id="4395d-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="4395d-162">Die Vorlage unserer Details anzeigen beginnt mit der ein wenig lang werden, die im Laufe der Zeit etwas schwieriger zu verstehen erleichtern wird.</span><span class="sxs-lookup"><span data-stu-id="4395d-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="4395d-163">Um die Lesbarkeit des Codes zu verbessern, lassen Sie uns zum Schluss erstellen eine partielle Ansicht – RSVPStatus.ascx –, die alle RSVP View Code für unsere Seite "Details" zu kapseln.</span><span class="sxs-lookup"><span data-stu-id="4395d-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="4395d-164">Wir können dazu mit der rechten Maustaste auf den Ordner "\Views\Dinners" und wählen Sie dann die Add -&gt;Menübefehl anzeigen.</span><span class="sxs-lookup"><span data-stu-id="4395d-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="4395d-165">Wir müssen es ein Dinner-Objekt als die stark typisierte ViewModel zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="4395d-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="4395d-166">Wir können dann kopieren und den RSVP-Inhalt aus unserer Ansicht "Details.aspx" darin einfügen.</span><span class="sxs-lookup"><span data-stu-id="4395d-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="4395d-167">Sobald wir damit fertig sind, außerdem erstellen wir eine andere partielle Ansicht – EditAndDeleteLinks.ascx - auf, die unseren Code bearbeiten und löschen Link anzeigen kapselt.</span><span class="sxs-lookup"><span data-stu-id="4395d-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="4395d-168">Darüber hinaus haben Sie ein Dinner-Objekt als die stark typisierte ViewModel nutzen und die Logik für bearbeiten und Löschen von unserer Ansicht "Details.aspx" hinein kopieren und einfügen.</span><span class="sxs-lookup"><span data-stu-id="4395d-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="4395d-169">Unsere Details, die Vorlage kann anzeigen, und klicken Sie dann schließen Sie einfach zwei Html.RenderPartial() Methodenaufrufe am unteren Rand:</span><span class="sxs-lookup"><span data-stu-id="4395d-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="4395d-170">Dadurch wird der Code besser lesen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="4395d-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="4395d-171">Nächster Schritt</span><span class="sxs-lookup"><span data-stu-id="4395d-171">Next Step</span></span>

<span data-ttu-id="4395d-172">Jetzt sehen wir uns wie wir mithilfe von AJAX noch einen Schritt weiter und interaktive Unterstützung unserer Anwendung hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="4395d-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4395d-173">[Zurück](secure-applications-using-authentication-and-authorization.md)
> [Weiter](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="4395d-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
