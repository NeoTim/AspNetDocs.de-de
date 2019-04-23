---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: Verwenden der TagBuilder-Klasse zum Erstellen von HTML-Hilfsprogrammen (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther stellt ein hilfreiches Dienstprogramm-Klasse in ASP.NET MVC-Framework mit dem Namen der TagBuilder-Klasse. Sie können die TagBuilder-Klasse, um problemlos verwenden...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 3227560c1d0c48f7738e26c87a0dbb140c410eee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59410096"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="1a72e-104">Verwenden der TagBuilder-Klasse zum Erstellen von HTML-Hilfsprogrammen (c#)</span><span class="sxs-lookup"><span data-stu-id="1a72e-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>

<span data-ttu-id="1a72e-105">durch [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="1a72e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="1a72e-106">Stephen Walther stellt ein hilfreiches Dienstprogramm-Klasse in ASP.NET MVC-Framework mit dem Namen der TagBuilder-Klasse.</span><span class="sxs-lookup"><span data-stu-id="1a72e-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="1a72e-107">Sie können die TagBuilder-Klasse verwenden, auf einfache Weise HTML-Tags erstellen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="1a72e-108">ASP.NET MVC-Framework umfasst eine hilfreiches Dienstprogramm-Klasse, die mit dem Namen der TagBuilder-Klasse, die Sie beim Erstellen von HTML-Hilfsprogramme verwenden können.</span><span class="sxs-lookup"><span data-stu-id="1a72e-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="1a72e-109">TagBuilder-Klasse, können wie der Name der Klasse bereits vermuten lässt, Sie ganz einfach HTML-Tags erstellen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="1a72e-110">In diesem kurzen Tutorial finden Sie eine Übersicht über die TagBuilder-Klasse, und erfahren Sie, wie Sie diese Klasse verwenden, beim Rendern von HTML erstellen eine einfache HTML-Hilfsobjekt, &lt;Img&gt; Tags.</span><span class="sxs-lookup"><span data-stu-id="1a72e-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="1a72e-111">Übersicht über die TagBuilder-Klasse</span><span class="sxs-lookup"><span data-stu-id="1a72e-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="1a72e-112">TagBuilder-Klasse ist in der System.Web.Mvc-Namespace enthalten.</span><span class="sxs-lookup"><span data-stu-id="1a72e-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="1a72e-113">Er hat fünf Methoden:</span><span class="sxs-lookup"><span data-stu-id="1a72e-113">It has five methods:</span></span>

- <span data-ttu-id="1a72e-114">AddCssClass() - ermöglicht Ihnen das Hinzufügen eines neuen *Klasse = ""* eine Tag-Attribut.</span><span class="sxs-lookup"><span data-stu-id="1a72e-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="1a72e-115">GenerateId() - können Sie ein Tag ein Id-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="1a72e-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="1a72e-116">Diese Methode ersetzt automatisch Punkte in der Id (in der Standardeinstellung werden Punkte durch Unterstriche ersetzt)</span><span class="sxs-lookup"><span data-stu-id="1a72e-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="1a72e-117">MergeAttribute() - können Sie Attribute, die ein Tag hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="1a72e-118">Es gibt mehrere Überladungen dieser Methode.</span><span class="sxs-lookup"><span data-stu-id="1a72e-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="1a72e-119">SetInnerText() - können Sie den inneren Text des Tags festlegen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="1a72e-120">Der innere Text ist HTML-Codierung.</span><span class="sxs-lookup"><span data-stu-id="1a72e-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="1a72e-121">ToString() - können Sie das Tag zu rendern.</span><span class="sxs-lookup"><span data-stu-id="1a72e-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="1a72e-122">Sie können angeben, ob es sich bei einem normalen Tag, ein Starttag, ein Endtag oder ein selbstschließendes Tag erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="1a72e-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="1a72e-123">TagBuilder-Klasse verfügt über vier wichtige Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="1a72e-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="1a72e-124">Attribute – alle Attribute des Tags darstellt.</span><span class="sxs-lookup"><span data-stu-id="1a72e-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="1a72e-125">IdAttributeDotReplacement - darstellt, das Zeichen, die von der GenerateId()-Methode verwendet werden, um die Zeiträume (der Standardwert ist ein Unterstrich) ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="1a72e-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="1a72e-126">InnerHTML - stellt den inneren Inhalt des Tags dar.</span><span class="sxs-lookup"><span data-stu-id="1a72e-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="1a72e-127">Diese Eigenschaft eine Zeichenfolge zuweisen *nicht* HTML-Codierung die Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="1a72e-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="1a72e-128">TagName - stellt den Namen des Tags dar.</span><span class="sxs-lookup"><span data-stu-id="1a72e-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="1a72e-129">Diese Methoden und Eigenschaften erhalten Sie alle grundlegenden Methoden und Eigenschaften, die Sie benötigen, um ein HTML-Tag zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="1a72e-130">Sie müssen unbedingt die TagBuilder-Klasse verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="1a72e-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="1a72e-131">Sie können stattdessen eine StringBuilder-Klasse verwenden.</span><span class="sxs-lookup"><span data-stu-id="1a72e-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="1a72e-132">Allerdings TagBuilder-Klasse das Leben macht etwas leichter.</span><span class="sxs-lookup"><span data-stu-id="1a72e-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="1a72e-133">Erstellen ein Image-HTML-Hilfsprogramm</span><span class="sxs-lookup"><span data-stu-id="1a72e-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="1a72e-134">Wenn Sie eine Instanz der TagBuilder-Klasse erstellen, übergeben Sie den Namen des Tags, die Sie an den Konstruktor TagBuilder erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="1a72e-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="1a72e-135">Anschließend rufen Sie Methoden wie die AddCssClass und MergeAttribute()-Methoden, die Attribute des Tags ändern.</span><span class="sxs-lookup"><span data-stu-id="1a72e-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="1a72e-136">Schließlich rufen Sie die ToString()-Methode zum Rendern des Tags.</span><span class="sxs-lookup"><span data-stu-id="1a72e-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="1a72e-137">Liste 1 enthält beispielsweise ein Bild HTML-Hilfsprogramm.</span><span class="sxs-lookup"><span data-stu-id="1a72e-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="1a72e-138">Das Image-Hilfsprogramm wird intern implementiert, mit einem TagBuilder, die eine HTML-darstellt &lt;Img&gt; Tag.</span><span class="sxs-lookup"><span data-stu-id="1a72e-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="1a72e-139">**1 – Helpers\ImageHelper.cs auflisten**</span><span class="sxs-lookup"><span data-stu-id="1a72e-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="1a72e-140">Die Klasse in der Liste 1 enthält zwei statische überladene Methoden, die mit dem Namen Image.</span><span class="sxs-lookup"><span data-stu-id="1a72e-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="1a72e-141">Wenn Sie die Image()-Methode aufrufen, können Sie ein Objekt übergeben, steht eine Reihe von HTML-Attribute oder nicht.</span><span class="sxs-lookup"><span data-stu-id="1a72e-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="1a72e-142">Beachten Sie, wie die TagBuilder.MergeAttribute()-Methode verwendet wird, die TagBuilder einzelner Attribute wie z. B. das Src-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="1a72e-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="1a72e-143">Beachten Sie außerdem, wie die TagBuilder.MergeAttributes()-Methode verwendet wird, eine Auflistung von Attributen der TagBuilder hinzu.</span><span class="sxs-lookup"><span data-stu-id="1a72e-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="1a72e-144">Die MergeAttributes()-Methode akzeptiert ein Wörterbuch&lt;string, object&gt; Parameter.</span><span class="sxs-lookup"><span data-stu-id="1a72e-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="1a72e-145">Die RouteValueDictionary-Klasse wird verwendet, um das Objekt, das die Auflistung von Attributen in ein Wörterbuch darstellt konvertieren&lt;string, object&gt;.</span><span class="sxs-lookup"><span data-stu-id="1a72e-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="1a72e-146">Nach der Erstellung der Image-Hilfe können Sie das Hilfsprogramm in Ihren ASP.NET MVC-Ansichten, genau wie die standardmäßigen HTML-Hilfsprogramme verwenden.</span><span class="sxs-lookup"><span data-stu-id="1a72e-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="1a72e-147">Die Ansicht im Codebeispiel 2 verwendet das Image-Hilfsprogramm, um dem gleichen Image von einer Xbox zweimal anzuzeigen (siehe Abbildung 1).</span><span class="sxs-lookup"><span data-stu-id="1a72e-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="1a72e-148">Das Hilfsprogramm Image() heißt mit und ohne eine Auflistung der HTML-Attribute.</span><span class="sxs-lookup"><span data-stu-id="1a72e-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="1a72e-149">**Codebeispiel 2 - Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="1a72e-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]


<span data-ttu-id="1a72e-150">[![Das Dialogfeld "Neues Projekt"](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1a72e-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="1a72e-151">**Abbildung 01**: Mit dem Image-Hilfsprogramm ([klicken Sie, um das Bild in voller Größe anzeigen](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1a72e-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>


<span data-ttu-id="1a72e-152">Beachten Sie, dass Sie mit dem Image-Helfer am oberen Rand der Ansicht Index.aspx verbundene Namespaces importieren müssen.</span><span class="sxs-lookup"><span data-stu-id="1a72e-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="1a72e-153">Das Hilfsprogramm wird mit der folgenden Anweisung importiert:</span><span class="sxs-lookup"><span data-stu-id="1a72e-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="1a72e-154">[Zurück](creating-custom-html-helpers-cs.md)
> [Weiter](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1a72e-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>
