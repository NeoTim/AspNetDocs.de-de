---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Die Überprüfung der Validierungssteuerelemente für Datenanmerkungen (VB) | Microsoft-Dokumentation
author: microsoft
description: Die Modellbindung des Daten-Anmerkung für die Validierung in ASP.NET MVC-Anwendungen nutzen. Erfahren Sie, wie die verschiedenen Typen von Validierungssteuerelement verwenden...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 6893d1f2445452b1d802b89027b09d8294bdc5b7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422836"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="8e7eb-104">Überprüfung der Validierungssteuerelemente für Datenanmerkungen (VB)</span><span class="sxs-lookup"><span data-stu-id="8e7eb-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="8e7eb-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8e7eb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8e7eb-106">Die Modellbindung des Daten-Anmerkung für die Validierung in ASP.NET MVC-Anwendungen nutzen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="8e7eb-107">Erfahren Sie, wie die verschiedenen Typen von Validierungssteuerelement-Attribute und mit ihnen im Microsoft Entity Framework arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>


<span data-ttu-id="8e7eb-108">In diesem Tutorial erfahren Sie, wie die Validierungssteuerelemente für die Datenanmerkung verwenden, für die Validierung in ASP.NET MVC-Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8e7eb-109">Der Vorteil der Verwendung der Validierungssteuerelemente für die Datenanmerkung ist, dass Sie eine Überprüfung durchführen, indem Sie einfach ein oder mehrere Attribute – z. B. die erforderliche oder StringLength-Attribut hinzufügen – einer Klasseneigenschaft bieten.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="8e7eb-110">Bevor Sie die Validierungssteuerelemente für die Datenanmerkung verwenden können, müssen Sie die Daten Anmerkungen Modellbindung herunterladen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="8e7eb-111">Sie können Anmerkungen Modell Binder Datenbeispiel, das von der CodePlex-Website herunterladen, indem Sie auf [hier](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span><span class="sxs-lookup"><span data-stu-id="8e7eb-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>


<span data-ttu-id="8e7eb-112">Es ist wichtig zu verstehen, dass die Modellbindung für Daten Anmerkungen keine offizielle Microsoft ASP.NET MVC-Framework gehört.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="8e7eb-113">Obwohl die Modellbindung für Daten Anmerkungen von den Microsoft ASP.NET MVC-Team erstellt wurde, bietet Microsoft keine offizielle Microsoft-Support für die Modellbindung des Daten-Anmerkungen beschrieben und in diesem Tutorial verwendet.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>


## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="8e7eb-114">Mithilfe der Modellbindung für Daten-Anmerkung</span><span class="sxs-lookup"><span data-stu-id="8e7eb-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="8e7eb-115">Um die Daten Anmerkungen Modellbindung in ASP.NET MVC-Anwendungen zu verwenden, müssen Sie zuerst einen Verweis auf die Microsoft.Web.Mvc.DataAnnotations.dll-Assembly und die System.ComponentModel.DataAnnotations.dll-Assembly hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="8e7eb-116">Wählen Sie die Menüoption **-Projekt "," Verweis hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="8e7eb-117">Klicken Sie dann auf die **Durchsuchen** Registerkarte, und navigieren Sie zum Speicherort, in dem Sie heruntergeladen (und entzippt) im Beispiel Daten Anmerkungen Modellbinder (finden Sie unter **Abbildung1**).</span><span class="sxs-lookup"><span data-stu-id="8e7eb-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="8e7eb-118">**Abbildung 1**: Hinzufügen eines Verweises auf die Modellbindung für Data Annotations ([klicken Sie, um das Bild in voller Größe anzeigen](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8e7eb-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="8e7eb-119">Wählen Sie zuerst die Microsoft.Web.Mvc.DataAnnotations.dll-Assembly und die System.ComponentModel.DataAnnotations.dll-Assembly, und klicken Sie auf die **OK** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>


<span data-ttu-id="8e7eb-120">Sie können keine die System.ComponentModel.DataAnnotations.dll-Assembly, die in .NET Framework Service Pack 1 mit der Modellbindung für Daten-Anmerkungen enthalten.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="8e7eb-121">Sie müssen die Version der im Beispiel für Daten Anmerkungen Binder-Download enthalten System.ComponentModel.DataAnnotations.dll Assembly verwenden.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>


<span data-ttu-id="8e7eb-122">Abschließend müssen Sie die Modellbindung "DataAnnotations" in der Datei "Global.asax" zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="8e7eb-123">Fügen Sie die folgende Zeile des Codes der Anwendung\_Start()-Ereignishandler so, dass die Anwendung\_Start()-Methode sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="8e7eb-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="8e7eb-124">Diese Codezeile wird der DataAnnotationsModelBinder als der Standardmodellbinder für die gesamte ASP.NET MVC-Anwendung registriert.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="8e7eb-125">Verwenden die Datenanmerkungsattribute-Validierungssteuerelement</span><span class="sxs-lookup"><span data-stu-id="8e7eb-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="8e7eb-126">Wenn Sie die Daten Anmerkungen Modellbindung verwenden, verwenden Sie die Validierungssteuerelement-Attribute für die Validierung.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="8e7eb-127">System.ComponentModel.DataAnnotations-Namespace enthält die folgenden Attribute für den systemintegritätsprüfungspunkt:</span><span class="sxs-lookup"><span data-stu-id="8e7eb-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="8e7eb-128">Bereich – können Sie überprüfen, ob der Wert einer Eigenschaft zwischen einem angegebenen Bereich von Werten liegt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="8e7eb-129">RegularExpression – können Sie überprüfen, ob der Wert einer Eigenschaft mit einem angegebenen regulären Ausdruck-Muster übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="8e7eb-130">Erforderlich: ermöglicht es Ihnen, eine Eigenschaft als erforderlich markieren.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="8e7eb-131">StringLength – können Sie eine maximale Länge für eine Zeichenfolgeneigenschaft angeben.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="8e7eb-132">Überprüfung: die Basisklasse für alle Validierungssteuerelement-Attribute.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8e7eb-133">Wenn bedarfsgerechte Überprüfung von einem standard-Validierungssteuerelemente nicht erfüllt werden müssen Sie immer die Möglichkeit, erstellen ein benutzerdefiniertes Validierungssteuerelement-Attribut durch ein neues Validierungssteuerelement-Attribut aus der Überprüfung Basisattribut erben.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>


<span data-ttu-id="8e7eb-134">Die Product-Klasse in **Codebeispiel 1** wird veranschaulicht, wie diese Attribute Validierungssteuerelement verwenden.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="8e7eb-135">Die Eigenschaften Name, Beschreibung und UnitPrice markiert werden nach Bedarf.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="8e7eb-136">Die Name-Eigenschaft müssen eine Länge der Zeichenfolge, die weniger als 10 Zeichen ist.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="8e7eb-137">Die UnitPrice-Eigenschaft muss schließlich Muster eines regulären Ausdrucks übereinstimmen, das einen Währungsbetrag darstellt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="8e7eb-138">**Codebeispiel 1**: Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="8e7eb-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="8e7eb-139">Die Product-Klasse veranschaulicht, wie ein zusätzliches Attribut: das DisplayName-Attribut.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="8e7eb-140">Das DisplayName-Attribut können Sie den Namen der Eigenschaft ändern, wenn die Eigenschaft in einer Fehlermeldung angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="8e7eb-141">Anstelle der Anzeige der Fehlermeldung "der UnitPrice-Feld ist erforderlich" können Sie anzeigen, der Fehlermeldung "das Preisfeld ist erforderlich".</span><span class="sxs-lookup"><span data-stu-id="8e7eb-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8e7eb-142">Wenn Sie die Fehlermeldung wird angezeigt, die durch ein Validierungssteuerelement vollständig anpassen möchten, können Sie eine benutzerdefinierte Fehlermeldung, des Validierungssteuerelements "ErrorMessage"-Eigenschaft wie folgt zuweisen:</span><span class="sxs-lookup"><span data-stu-id="8e7eb-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this:</span></span> `<Required(ErrorMessage:="This field needs a value!")>`


<span data-ttu-id="8e7eb-143">Können Sie die Product-Klasse in **Codebeispiel 1** mit Create() Controlleraktion in **Codebeispiel 2**.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="8e7eb-144">Diese Controlleraktion Ansicht "erstellen" wird erneut angezeigt, wenn Modellstatus alle Fehler enthält.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="8e7eb-145">**Codebeispiel 2**: Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="8e7eb-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="8e7eb-146">Schließlich können Sie die Ansicht erstellen **Codebeispiel 3** durch einen Rechtsklick auf die Aktion Create() und durch Auswählen der Menüoption **Ansicht hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="8e7eb-147">Erstellen Sie eine stark typisierte Ansicht mit der Product-Klasse, wie die Model-Klasse.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="8e7eb-148">Wählen Sie **erstellen** aus der Dropdownliste der Ansicht Inhalt (finden Sie unter **abbildung2**).</span><span class="sxs-lookup"><span data-stu-id="8e7eb-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="8e7eb-149">**Abbildung 2**: Hinzufügen der Ansicht "erstellen"</span><span class="sxs-lookup"><span data-stu-id="8e7eb-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="8e7eb-150">**Codebeispiel 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="8e7eb-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8e7eb-151">Entfernen Sie das Id-Feld von der erstellen-Form von generiert die **Ansicht hinzufügen** Option des Menüs.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="8e7eb-152">Da das Id-Feld eine Identity-Spalte entspricht, möchten keine Benutzer einen Wert für dieses Feld eingeben können.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>


<span data-ttu-id="8e7eb-153">Wenn Sie das Formular zum Erstellen eines Produkts senden und Sie werden keine Werte für die erforderlichen Felder eingeben, die Überprüfung von Fehlermeldungen, in **Abbildung 3** werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="8e7eb-154">**Abbildung 3**: Fehlende erforderliche Felder</span><span class="sxs-lookup"><span data-stu-id="8e7eb-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="8e7eb-155">Wenn Sie eine ungültige Währungsbetrag, und klicken Sie dann auf die Fehlermeldung im eingeben **Abbildung 4** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="8e7eb-156">**Abbildung 4**: Ungültige Währungsbetrag</span><span class="sxs-lookup"><span data-stu-id="8e7eb-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="8e7eb-157">Verwenden von Validierungssteuerelementen für Datenanmerkungen mit Entitätsframework</span><span class="sxs-lookup"><span data-stu-id="8e7eb-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="8e7eb-158">Wenn Sie Microsoft Entity Framework verwenden, um Ihre Data Model-Klassen zu generieren, können nicht Sie die Validierungssteuerelement-Attribute direkt auf Ihre Klassen anwenden.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="8e7eb-159">Da Entity Framework Designer der ViewModel-Klassen generiert, werden alle Änderungen, die Sie an die Modellklassen das nächste Mal überschrieben werden, die, das Sie im Designer Änderungen vornehmen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="8e7eb-160">Wenn Sie die Validierungssteuerelemente mit den Klassen generiert, die vom Entity Framework verwenden möchten, müssen Sie Meta Datenklassen erstellen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="8e7eb-161">Sie haben die Validierungssteuerelemente der Meta-Data-Klasse anstelle der Validierungssteuerelemente auf die tatsächliche Klasse anwenden.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="8e7eb-162">Beispiel: Angenommen, dass Sie eine Movie-Klasse, die mithilfe von Entity Framework erstellt haben (siehe **Abbildung 5**).</span><span class="sxs-lookup"><span data-stu-id="8e7eb-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="8e7eb-163">Stellen Sie sich vor, darüber hinaus, dass Sie den Filmtitel und Director Eigenschaften erforderlichen Eigenschaften machen möchten.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="8e7eb-164">In diesem Fall können Sie erstellen die partielle Klasse und Meta-Data-Klasse in **Listing 4**.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="8e7eb-165">**Abbildung 5**: Movie-Klasse, die von Entity Framework generierten</span><span class="sxs-lookup"><span data-stu-id="8e7eb-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="8e7eb-166">**Programmausdruck 4**: Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="8e7eb-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="8e7eb-167">Die Datei im **Listing 4** enthält zwei Klassen namens "Film" und "MovieMetaData aus.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="8e7eb-168">Die Movie-Klasse ist eine partielle Klasse.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-168">The Movie class is a partial class.</span></span> <span data-ttu-id="8e7eb-169">Er entspricht der partiellen Klasse, die vom Entity Framework, das in der Datei DataModel.Designer.vb enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="8e7eb-170">Derzeit werden teilweise Eigenschaften von .NET Framework nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="8e7eb-171">Daher besteht keine Möglichkeit, die Validierungssteuerelement-Attribute für die Movie-Klasse, die durch die Validierungssteuerelement-Attribute anwenden, auf die Movie-Klasse, die in der Datei definiert die Eigenschaften in der DataModel.Designer.vb-Datei definiert die Eigenschaften gelten **Listing 4**.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="8e7eb-172">Beachten Sie, dass die partielle Movie-Klasse mit dem Attribut "metadatatype" versehen ist, der auf die Klasse MovieMetaData aus zeigt.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="8e7eb-173">Die MovieMetaData aus-Klasse enthält Eigenschaften von Netzwerkproxy für die Eigenschaften der Movie-Klasse.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="8e7eb-174">Die Validierungssteuerelement-Attribute gelten für die Eigenschaften der Klasse MovieMetaData aus.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="8e7eb-175">Die Eigenschaften für Titel, Regisseur und DateReleased, die alle als erforderlichen Eigenschaften gekennzeichnet sind.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="8e7eb-176">Die Director-Eigenschaft muss eine Zeichenfolge zugewiesen werden, die weniger als 5 Zeichen enthält.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="8e7eb-177">Schließlich wird das DisplayName-Attribut angewendet, auf die DateReleased-Eigenschaft zum Anzeigen einer Fehlermeldung wie "das Feld Date freigegeben ist erforderlich".</span><span class="sxs-lookup"><span data-stu-id="8e7eb-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="8e7eb-178">statt den Fehler ist"das Feld" DateReleased"erforderlich".</span><span class="sxs-lookup"><span data-stu-id="8e7eb-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8e7eb-179">Beachten Sie, dass die Proxyeigenschaften in der Klasse MovieMetaData aus nicht dieselben Typen wie die entsprechenden Eigenschaften in die Movie-Klasse darstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="8e7eb-180">Beispielsweise ist die Director-Eigenschaft einer Zeichenfolgeneigenschaft in die Movie-Klasse und eine Eigenschaft des Objekts in der Klasse MovieMetaData aus.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>


<span data-ttu-id="8e7eb-181">Die Seite im **Abbildung 6** veranschaulicht die Fehlermeldungen zurückgegeben, wenn Sie ungültige Werte für die Movie-Eigenschaften eingeben.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="8e7eb-182">**Abbildung 6**: Entity Framework mit Validierungssteuerelementen ([klicken Sie, um das Bild in voller Größe anzeigen](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="8e7eb-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="8e7eb-183">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="8e7eb-183">Summary</span></span>

<span data-ttu-id="8e7eb-184">In diesem Tutorial haben Sie gelernt, wie die Modellbindung des Daten-Anmerkung für die Validierung in ASP.NET MVC-Anwendungen nutzen.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="8e7eb-185">Sie haben gelernt, wie die verschiedenen Typen von Validierungssteuerelement-Attribute wie z. B. die erforderlichen und StringLength-Attribute verwendet.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="8e7eb-186">Sie haben zudem, wie Sie diese Attribute verwenden, bei der Arbeit mit Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8e7eb-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8e7eb-187">Vorheriges</span><span class="sxs-lookup"><span data-stu-id="8e7eb-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
