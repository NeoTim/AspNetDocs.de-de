---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: Verwenden der tagbuilder-Klasse zum Erstellen von HTMLC#-Hilfsprogrammen () | Microsoft-Dokumentation
author: StephenWalther
description: Stephen Walther führt Sie zu einer nützlichen Utility-Klasse im ASP.NET MVC-Framework mit dem Namen "tagbuilder Class". Sie können die tagbuilder-Klasse verwenden, um problemlos...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485607"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>Verwenden der tagbuilder-Klasse zum Erstellen von HTMLC#-Hilfsprogrammen ()

von [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther führt Sie zu einer nützlichen Utility-Klasse im ASP.NET MVC-Framework mit dem Namen "tagbuilder Class". Sie können die tagbuilder-Klasse verwenden, um problemlos HTML-Tags zu erstellen.

Das ASP.NET-MVC-Framework enthält eine nützliche Hilfsprogrammklasse mit dem Namen "tagbuilder", die Sie beim Entwickeln von HTML-Hilfsprogrammen verwenden können. Die tagbuilder-Klasse, wie der Name der Klasse, ermöglicht Ihnen das einfache Erstellen von HTML-Tags. In diesem kurzen Tutorial erhalten Sie eine Übersicht über die tagbuilder-Klasse, und Sie erfahren, wie Sie diese Klasse verwenden, wenn Sie ein einfaches HTML-Hilfsprogramm entwickeln, das HTML-&lt;IMG&gt; Tags rendert.

## <a name="overview-of-the-tagbuilder-class"></a>Übersicht über die tagbuilder-Klasse

Die tagbuilder-Klasse ist im Namespace System. Web. MVC enthalten. Sie verfügt über fünf Methoden:

- AddCssClass (): ermöglicht das Hinzufügen eines neuen *Class = ""* -Attributs zu einem Tag.
- GenerateID (): ermöglicht das Hinzufügen eines ID-Attributs zu einem Tag. Diese Methode ersetzt Zeiträume in der ID automatisch (Standardmäßig werden Zeiträume durch Unterstriche ersetzt).
- Mergeattribute (): ermöglicht das Hinzufügen von Attributen zu einem Tag. Es gibt mehrere über Ladungen dieser Methode.
- Setinnertext (): ermöglicht es Ihnen, den inneren Text des Tags festzulegen. Der innere Text ist die HTML-Codierung automatisch.
- Mit der Zeichenfolge (): ermöglicht das Rendering des Tags. Sie können angeben, ob Sie ein normales Tag, ein Starttag, ein Endtag oder ein selbstschließendes Tag erstellen möchten.

Die tagbuilder-Klasse verfügt über vier wichtige Eigenschaften:

- Attribute: stellt alle Attribute des Tags dar.
- Idattributedotreplacement: stellt das Zeichen dar, das von der generateID ()-Methode verwendet wird, um Zeiträume zu ersetzen (der Standardwert ist ein Unterstrich).
- InnerHTML: stellt den inneren Inhalt des Tags dar. Wenn Sie dieser Eigenschaft eine Zeichenfolge zuweisen, wird die Zeichenfolge *nicht* in HTML codiert.
- Tagname: stellt den Namen des Tags dar.

Diese Methoden und Eigenschaften verfügen über alle grundlegenden Methoden und Eigenschaften, die Sie zum Erstellen eines HTML-Tags benötigen. Sie müssen nicht unbedingt die tagbuilder-Klasse verwenden. Sie könnten stattdessen eine StringBuilder-Klasse verwenden. Die tagbuilder-Klasse macht Ihr Leben jedoch etwas einfacher.

## <a name="creating-an-image-html-helper"></a>Erstellen eines HTML-HTML-Hilfsprogramms

Wenn Sie eine Instanz der tagbuilder-Klasse erstellen, übergeben Sie den Namen des Tags, das Sie erstellen möchten, an den tagbuilder-Konstruktor. Als nächstes können Sie Methoden wie die addCssClass-Methode und die mergeattribute ()-Methode aufrufen, um die Attribute des Tags zu ändern. Zum Schluss wird die Methode "destring ()" aufgerufen, um das Tag zu Rendering.

Beispielsweise enthält die Auflistung 1 ein HTML-HTML-Hilfsprogramm. Das Image-Hilfsprogramm wird intern mit einem tagbuilder implementiert, das eine HTML-&lt;IMG&gt;-Tags darstellt.

**Codebeispiel 1-helpers\imagehelper.cs**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

Die Klasse in Auflistung 1 enthält zwei statische überladene Methoden mit dem Namen "Image". Wenn Sie die Image ()-Methode aufzurufen, können Sie ein Objekt übergeben, das einen Satz von HTML-Attributen darstellt.

Beachten Sie, wie die tagbuilder. mergeattribute ()-Methode verwendet wird, um dem tagbuilder einzelne Attribute wie das src-Attribut hinzuzufügen. Beachten Sie außerdem, wie die tagbuilder. mergeattribu()-Methode verwendet wird, um dem tagbuilder eine Auflistung von Attributen hinzuzufügen. Die mergeattribu()-Methode akzeptiert ein Wörterbuch&lt;Zeichenfolge, Objekt&gt;-Parameters. Die RouteValueDictionary-Klasse wird verwendet, um das Objekt, das die Auflistung von Attributen darstellt, in ein Wörterbuch&lt;Zeichenfolge, Objekt&gt;zu konvertieren.

Nachdem Sie das Image-Hilfsprogramm erstellt haben, können Sie das Hilfsprogramm in Ihren ASP.NET MVC-Ansichten genau wie alle anderen Standard-HTML-Hilfsprogramme verwenden. Die Ansicht in der Liste 2 verwendet das Image Helper, um das gleiche Bild einer Xbox zweimal anzuzeigen (siehe Abbildung 1). Das "Image ()"-Hilfsprogramm wird sowohl mit als auch ohne HTML-Attribut Auflistung aufgerufen.

**Codebeispiel 2: home\index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

[![des Dialog Felds "Neues Projekt"](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**Abbildung 01**: Verwenden des Image-Hilfsprogramms ([Klicken Sie, um das Bild in voller Größe anzuzeigen](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))

Beachten Sie, dass Sie den Namespace importieren müssen, der dem bildrhilfsobjekt am Anfang der Ansicht "index. aspx" zugeordnet ist. Das Hilfsprogramm wird mit der folgenden Direktive importiert:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [Zurück](creating-custom-html-helpers-cs.md)
> [Weiter](creating-page-layouts-with-view-master-pages-cs.md)
