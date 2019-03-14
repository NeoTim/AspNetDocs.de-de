---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'Iteration #3 – Hinzufügen der formularüberprüfung (c#) | Microsoft-Dokumentation'
author: microsoft
description: In der dritten Iteration fügen wir grundlegende formularvalidierung hinzu. Es wird verhindert, dass Personen senden eines Formulars ohne erforderlichen Felder des Formulars abzuschließen. Wir überprüfen außerdem Emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 4115b3898415d63ffb122f3d0fea93022f2baa02
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030417"
---
<a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="77bd1-105">Iteration #3 – Hinzufügen der formularüberprüfung (c#)</span><span class="sxs-lookup"><span data-stu-id="77bd1-105">Iteration #3 – Add form validation (C#)</span></span>
====================
<span data-ttu-id="77bd1-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="77bd1-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="77bd1-107">Code herunterladen</span><span class="sxs-lookup"><span data-stu-id="77bd1-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="77bd1-108">In der dritten Iteration fügen wir grundlegende formularvalidierung hinzu.</span><span class="sxs-lookup"><span data-stu-id="77bd1-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="77bd1-109">Es wird verhindert, dass Personen senden eines Formulars ohne erforderlichen Felder des Formulars abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="77bd1-110">Wir überprüfen auch die e-Mail-Adressen und Telefonnummern.</span><span class="sxs-lookup"><span data-stu-id="77bd1-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="77bd1-111">Erstellen einer Kontaktverwaltung ASP.NET MVC-Anwendung (c#)</span><span class="sxs-lookup"><span data-stu-id="77bd1-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="77bd1-112">In dieser Reihe von Tutorials erstellen wir eine gesamte Anwendung Kontaktverwaltung ab Beginn um den Vorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="77bd1-113">Die Contact Manager-Anwendung können Sie zum Speichern von Kontaktinformationen - Namen, Telefonnummern und e-Mail-Adressen – eine Liste der Personen an.</span><span class="sxs-lookup"><span data-stu-id="77bd1-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="77bd1-114">Wir erstellen die Anwendung über mehrere Iterationen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="77bd1-115">Bei jeder Iteration verbessern wir nach und nach der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="77bd1-116">Das Ziel dieses mehrere Iteration-Ansatzes ist, um den Grund für jede Änderung verstehen können.</span><span class="sxs-lookup"><span data-stu-id="77bd1-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="77bd1-117">Iteration #1 – Erstellen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="77bd1-118">In der ersten Iteration wir der Contact Manager in der einfachsten maximal möglicher Größe erstellen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="77bd1-119">Wir haben Unterstützung für grundlegender Datenbankvorgänge hinzugefügt: Erstellen Sie, lesen Sie, aktualisieren Sie und löschen Sie (CRUD).</span><span class="sxs-lookup"><span data-stu-id="77bd1-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="77bd1-120">Iteration #2 – Optimieren der Anwendung gut.</span><span class="sxs-lookup"><span data-stu-id="77bd1-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="77bd1-121">In dieser Iteration verbessern wir die Darstellung der Anwendung durch Ändern der Standard-Masterseite für ASP.NET MVC-Ansicht und cascading Stylesheet.</span><span class="sxs-lookup"><span data-stu-id="77bd1-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="77bd1-122">Iteration #3 – Hinzufügen der formularüberprüfung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="77bd1-123">In der dritten Iteration fügen wir grundlegende formularvalidierung hinzu.</span><span class="sxs-lookup"><span data-stu-id="77bd1-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="77bd1-124">Es wird verhindert, dass Personen senden eines Formulars ohne erforderlichen Felder des Formulars abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="77bd1-125">Wir überprüfen auch die e-Mail-Adressen und Telefonnummern.</span><span class="sxs-lookup"><span data-stu-id="77bd1-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="77bd1-126">Stellen Sie Iteration #4 – lose koppeln der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="77bd1-127">In dieser vierten Iteration nutzen wir einige Entwurfsmuster für Software zu verwalten und ändern Sie die Kontakt-Manager-Anwendung zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="77bd1-128">Z. B. gestalten wir unsere Anwendung, die dem Repositorymuster und dem Dependency Injection-Muster verwenden.</span><span class="sxs-lookup"><span data-stu-id="77bd1-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="77bd1-129">Iteration #5 – Erstellen von Komponententests.</span><span class="sxs-lookup"><span data-stu-id="77bd1-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="77bd1-130">In der fünften Iteration stellen wir unsere Anwendung einfacher zu verwalten und zu ändern, indem Sie die Komponententests hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="77bd1-131">Wir unsere Data Model-Klassen modellieren und erstellen Sie Komponententests für unseren Controller und die Validierungslogik.</span><span class="sxs-lookup"><span data-stu-id="77bd1-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="77bd1-132">Iteration #6 – Verwenden der testgesteuerten Entwicklung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="77bd1-133">In dieser Iteration sechsten fügen wir neue Funktionen zu unserer Anwendung zuerst Schreiben von Komponententests und Code für die Komponententests schreiben hinzu.</span><span class="sxs-lookup"><span data-stu-id="77bd1-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="77bd1-134">In dieser Iteration fügen wir wenden Sie sich an Gruppen hinzu.</span><span class="sxs-lookup"><span data-stu-id="77bd1-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="77bd1-135">Iteration #7 - Ajax-Funktionen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="77bd1-136">In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung der Anwendung durch Hinzufügen von Unterstützung für Ajax.</span><span class="sxs-lookup"><span data-stu-id="77bd1-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="77bd1-137">Diese Iteration</span><span class="sxs-lookup"><span data-stu-id="77bd1-137">This Iteration</span></span>

<span data-ttu-id="77bd1-138">In dieser zweiten Iteration der Contact Manager-Anwendung fügen wir grundlegende formularvalidierung hinzu.</span><span class="sxs-lookup"><span data-stu-id="77bd1-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="77bd1-139">Es wird verhindert, dass Benutzer einen Kontakt ohne Eingabe von Werten für die erforderlichen Felder des Formulars zu senden.</span><span class="sxs-lookup"><span data-stu-id="77bd1-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="77bd1-140">Wir überprüfen auch die Telefonnummern und e-Mail-Adressen (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="77bd1-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="77bd1-141">[![Das Dialogfeld "Neues Projekt"](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="77bd1-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="77bd1-142">**Abbildung 01**: Ein Formular mit Überprüfung ([klicken Sie, um das Bild in voller Größe anzeigen](iteration-3-add-form-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="77bd1-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="77bd1-143">In dieser Iteration fügen wir die Validierungslogik, direkt auf die Controlleraktionen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="77bd1-144">Im Allgemeinen ist dies nicht die empfohlene Methode zum Hinzufügen der Validierung zu einer ASP.NET MVC-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="77bd1-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="77bd1-145">Ein besserer Ansatz besteht darin die Validierungslogik einer Anwendung s in einem separaten [Dienstschicht](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span><span class="sxs-lookup"><span data-stu-id="77bd1-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="77bd1-146">In der nächsten Iteration gestalten wir die Contact Manager-Anwendung, um die Anwendung besser verwaltbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="77bd1-147">In dieser Iteration, aus Gründen der Einfachheit schreiben wir alle der Validierungscode manuell.</span><span class="sxs-lookup"><span data-stu-id="77bd1-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="77bd1-148">Anstelle der Validierungscode schreiben, selbst, könnten wir einen Validierungsframework nutzen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="77bd1-149">Beispielsweise können Sie die Microsoft Enterprise Library Validation Application Block (VAB) zum Implementieren von Validierungslogik für Ihre ASP.NET MVC-Anwendung aus.</span><span class="sxs-lookup"><span data-stu-id="77bd1-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="77bd1-150">Weitere Informationen zu der Validation Application Block finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="77bd1-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="77bd1-151">Hinzufügen einer Validierung zu Ansicht "erstellen"</span><span class="sxs-lookup"><span data-stu-id="77bd1-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="77bd1-152">Lassen Sie s starten, indem Sie die Erstellungsansicht Validierungslogik hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="77bd1-153">Glücklicherweise da wir die Erstellungsansicht mit Visual Studio generiert, enthält die Erstellungsansicht bereits aller erforderlichen Benutzeroberflächenlogik validierungsmeldungen werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="77bd1-154">Ansicht "erstellen" ist in Codebeispiel 1 enthalten.</span><span class="sxs-lookup"><span data-stu-id="77bd1-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="77bd1-155">**Codebeispiel 1 – \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="77bd1-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="77bd1-156">Beachten Sie, dass des Aufrufs an die Html.ValidationSummary()-Hilfsmethode, die direkt über das HTML-Formular angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="77bd1-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="77bd1-157">Wenn es Meldungen für Validierungsfehler sind, zeigt diese Methode validierungsmeldungen in eine Liste mit Aufzählungszeichen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="77bd1-158">Beachten Sie außerdem die Aufrufe an Html.ValidationMessage(), die neben jedem Formularfeld angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="77bd1-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="77bd1-159">Das Hilfsprogramm ValidationMessage() zeigt eine einzelne Validierungsfehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="77bd1-160">Im Fall von Codebeispiel 1 wird ein Sternchen angezeigt, wenn ein Überprüfungsfehler vorliegt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="77bd1-161">Zum Abschluss rendert das Hilfsobjekt Html.TextBox() automatisch eine Cascading Style Sheet-Klasse, bei der Überprüfungsfehler angezeigt, die vom Hilfsprogramm Eigenschaft zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="77bd1-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="77bd1-162">Das Hilfsprogramm Html.TextBox() rendert eine Klasse namens **Eingabe-Überprüfungsfehlern**.</span><span class="sxs-lookup"><span data-stu-id="77bd1-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="77bd1-163">Wenn Sie eine neue ASP.NET MVC-Anwendung erstellen, wird automatisch ein Stylesheet, mit dem Namen "Site.CSS" im Ordner "Content" erstellt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="77bd1-164">Dieses Stylesheet enthält die folgenden Definitionen für CSS-Klassen beziehen sich auf die Darstellung von Validierungsfehlermeldungen:</span><span class="sxs-lookup"><span data-stu-id="77bd1-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="77bd1-165">Die Feld-Überprüfungsfehlern-Klasse wird verwendet, zum Formatieren der Ausgabe, die vom Hilfsprogramm Html.ValidationMessage() gerendert.</span><span class="sxs-lookup"><span data-stu-id="77bd1-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="77bd1-166">Die Eingabe-Überprüfungsfehlern-Klasse wird verwendet, so formatieren Sie das Textfeld (Eingabe), die vom Hilfsprogramm Html.TextBox() gerendert.</span><span class="sxs-lookup"><span data-stu-id="77bd1-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="77bd1-167">Die Zusammenfassung der Validierungsfehler-Klasse wird verwendet, zum Formatieren der unsortierten Liste, die vom Hilfsprogramm Html.ValidationSummary() gerendert.</span><span class="sxs-lookup"><span data-stu-id="77bd1-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="77bd1-168">Sie können Stylesheet-Klassen in diesem Abschnitt anpassen die Darstellung von Validierungsfehlermeldungen beschrieben ändern.</span><span class="sxs-lookup"><span data-stu-id="77bd1-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="77bd1-169">Hinzufügen von Validierungslogik auf die Aktion erstellen</span><span class="sxs-lookup"><span data-stu-id="77bd1-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="77bd1-170">Moment, Ansicht "erstellen" niemals Überprüfungsfehlermeldungen angezeigt, weil wir die Logik, um alle Nachrichten generieren, die nicht geschrieben haben.</span><span class="sxs-lookup"><span data-stu-id="77bd1-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="77bd1-171">Um Überprüfungsfehlermeldungen anzuzeigen, müssen Sie die Fehlermeldungen ModelState hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="77bd1-172">Die UpdateModel() Methode hinzufügt, Fehlermeldungen ModelState automatisch Wenn Fehler beim Zuweisen einer Eigenschaft eines Formularfelds.</span><span class="sxs-lookup"><span data-stu-id="77bd1-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="77bd1-173">Z. B., wenn Sie versuchen, eine BirthDate-Eigenschaft die Zeichenfolge "Apple" zuweisen, die DateTime-Werte akzeptiert, fügt dann die UpdateModel()-Methode einen Fehler hinzu ModelState.</span><span class="sxs-lookup"><span data-stu-id="77bd1-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="77bd1-174">Die geänderte Create()-Methode in Liste 2 enthält einen neuen Abschnitt, der die Eigenschaften der Contact-Klasse überprüft, bevor die neue Kontakt in die Datenbank eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="77bd1-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="77bd1-175">**Codebeispiel 2 - Controllers\ContactController.cs (erstellen mit Überprüfung)**</span><span class="sxs-lookup"><span data-stu-id="77bd1-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="77bd1-176">Die Validate-Abschnitt erzwingt vier unterschiedliche Validierungsregeln an:</span><span class="sxs-lookup"><span data-stu-id="77bd1-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="77bd1-177">Die FirstName-Eigenschaft muss eine Länge größer als 0 (null) haben (und es darf nicht ausschließlich aus Leerzeichen bestehen)</span><span class="sxs-lookup"><span data-stu-id="77bd1-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="77bd1-178">Die LastName-Eigenschaft muss eine Länge größer als 0 (null) haben (und es darf nicht ausschließlich aus Leerzeichen bestehen)</span><span class="sxs-lookup"><span data-stu-id="77bd1-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="77bd1-179">Wenn die Phone-Eigenschaft einen Wert aufweist (hat eine Länge größer als 0) und dann die Phone-Eigenschaft auf einen regulären Ausdruck übereinstimmen muss.</span><span class="sxs-lookup"><span data-stu-id="77bd1-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="77bd1-180">Wenn die e-Mail-Eigenschaft einen Wert aufweist (hat eine Länge größer als 0) und dann die e-Mail-Eigenschaft mit einem regulären Ausdruck entsprechen muss.</span><span class="sxs-lookup"><span data-stu-id="77bd1-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="77bd1-181">Eine Regel validierungsverstoß liegt, wird ModelState eine Fehlermeldung mit Hilfe der Methode AddModelError() hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="77bd1-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="77bd1-182">Wenn Sie eine Nachricht ModelState hinzufügen, geben Sie den Namen einer Eigenschaft und den Text der eine Validierungsfehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="77bd1-183">Diese Fehlermeldung wird von den Hilfsmethoden Html.ValidationSummary() und Html.ValidationMessage() in der Ansicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="77bd1-184">Nachdem die Validierungsregeln ausgeführt werden, wird die Eigenschaft "IsValid" von ModelState überprüft.</span><span class="sxs-lookup"><span data-stu-id="77bd1-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="77bd1-185">Die Eigenschaft "IsValid" gibt false zurück, wenn alle Validierungsfehlermeldungen ModelState hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="77bd1-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="77bd1-186">Wenn die Validierung fehlschlägt, wird der erstellen-Form in die Fehlermeldungen erneut angezeigt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="77bd1-187">Ich habe die regulären Ausdrücke für die Überprüfung der Telefonnummer und e-Mail-Adresse aus dem Repository der reguläre Ausdruck unter [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="77bd1-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="77bd1-188">Die Bearbeitungsaktion Validierungslogik hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="77bd1-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="77bd1-189">Die Aktion Edit() aktualisiert einen Kontakt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="77bd1-190">Die Aktion Edit() muss genau die gleiche Überprüfungen als Create() Aktion durchführen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="77bd1-191">Anstelle den gleiche Überprüfungscode zu wiederholen, sollten wir den Contact-Controller so umgestalten, dass sowohl die Edit() die Create() Aktionen rufen Sie die gleiche Validierungsmethode.</span><span class="sxs-lookup"><span data-stu-id="77bd1-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="77bd1-192">Die geänderte Contact-Controller-Klasse ist in Programmausdruck 3 enthalten.</span><span class="sxs-lookup"><span data-stu-id="77bd1-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="77bd1-193">Diese Klasse verfügt über eine neue ValidateContact()-Methode, die in Create() sowohl Edit() Aktionen aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="77bd1-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="77bd1-194">**Codebeispiel 3 - Controllers\ContactController.cs**</span><span class="sxs-lookup"><span data-stu-id="77bd1-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="77bd1-195">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="77bd1-195">Summary</span></span>

<span data-ttu-id="77bd1-196">In dieser Iteration haben wir grundlegende formularvalidierung zu unserer Contact Manager-Anwendung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="77bd1-197">Unsere Validierungslogik verhindert, dass Benutzer übermitteln einen neuen Kontakt oder bearbeiten einen vorhandenen Kontakt ohne Angabe der Werte für die FirstName und LastName-Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="77bd1-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="77bd1-198">Darüber hinaus müssen die Benutzer gültige Telefonnummer und e-Mail-Adressen angeben.</span><span class="sxs-lookup"><span data-stu-id="77bd1-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="77bd1-199">In dieser Iteration haben wir die Validierungslogik zu unserer Contact Manager-Anwendung in die einfachste Möglichkeit, die mögliche hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="77bd1-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="77bd1-200">Allerdings wird Mischen von unserem Validierungslogik in unserer Controllerlogik Probleme für uns auf lange Sicht erstellen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="77bd1-201">Die Anwendung werden schwieriger zu verwalten und im Laufe der Zeit ändern.</span><span class="sxs-lookup"><span data-stu-id="77bd1-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="77bd1-202">In der nächsten Iteration werden wir unsere Validierungslogik und Datenbankzugriffslogik aus unserem Controller gestalten.</span><span class="sxs-lookup"><span data-stu-id="77bd1-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="77bd1-203">Es werden mehrere Prinzipien der Softwareentwicklung zu uns ermöglichen, Erstellen einer zunehmend lockerer verkoppelt und wartungsfreundlicher, nutzen.</span><span class="sxs-lookup"><span data-stu-id="77bd1-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="77bd1-204">[Zurück](iteration-2-make-the-application-look-nice-cs.md)
> [Weiter](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="77bd1-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>