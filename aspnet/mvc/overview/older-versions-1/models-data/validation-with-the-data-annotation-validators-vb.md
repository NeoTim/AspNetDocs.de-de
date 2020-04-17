---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Validierung mit den Datenanmerkungsvalidierern (VB) | Microsoft Docs
author: rick-anderson
description: Nutzen Sie den Datenanmerkungsmodellbinder, um die Validierung in einer ASP.NET MVC-Anwendung durchzuführen. Erfahren Sie, wie Sie die verschiedenen Typen von Validierungen verwenden...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542637"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>Überprüfung der Validierungssteuerelemente für Datenanmerkungen (VB)

von [Microsoft](https://github.com/microsoft)

> Nutzen Sie den Datenanmerkungsmodellbinder, um die Validierung in einer ASP.NET MVC-Anwendung durchzuführen. Erfahren Sie, wie Sie die verschiedenen Typen von Validierungsattributen verwenden und mit ihnen im Microsoft Entity Framework arbeiten.

In diesem Tutorial erfahren Sie, wie Sie die Datenanmerkungsvalidierer verwenden, um die Validierung in einer ASP.NET MVC-Anwendung durchzuführen. Der Vorteil der Verwendung der Data Annotation-Validierer besteht darin, dass Sie die Validierung einfach durch Hinzufügen eines oder mehrerer Attribute – z. B. des Attributs Erforderlich oder StringLength – zu einer Klasseneigenschaft ermöglichen.

Bevor Sie die Validatoren für Datenanmerkungen verwenden können, müssen Sie den Modellbinder für Datenanmerkungen herunterladen. Sie können das Data Annotations Model Binder Sample von der CodePlex-Website herunterladen, indem Sie [hier](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)klicken.

Es ist wichtig zu verstehen, dass das Data Annotations Model Binder kein offizieller Teil des Microsoft ASP.NET MVC-Frameworks ist. Obwohl der Modellbinder für Datenanmerkungen vom Microsoft ASP.NET MVC-Team erstellt wurde, bietet Microsoft keine offizielle Produktunterstützung für den in diesem Tutorial beschriebenen und verwendeten Modellbinder für Datenanmerkungen an.

## <a name="using-the-data-annotation-model-binder"></a>Verwenden des Datenanmerkungsmodellbinders

Um den Modellbinder für Datenanmerkungen in einer ASP.NET MVC-Anwendung zu verwenden, müssen Sie zunächst einen Verweis auf die Assembly Microsoft.Web.Mvc.DataAnnotations.dll und die Assembly System.ComponentModel.DataAnnotations.dll hinzufügen. Wählen Sie die Menüoption **Projekt, Referenz hinzufügen**. Klicken Sie anschließend auf die Registerkarte **Durchsuchen,** und navigieren Sie zu dem Speicherort, an dem Sie das Beispiel "Data Annotations Model Binder" heruntergeladen (und entpackt) haben (siehe **Abbildung 1**).

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**Abbildung 1:** Hinzufügen eines Verweises auf den Modellbinder für Datenanmerkungen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](validation-with-the-data-annotation-validators-vb/_static/image3.png))

Wählen Sie sowohl die Assembly Microsoft.Web.Mvc.DataAnnotations.dll als auch die Assembly System.ComponentModel.DataAnnotations.dll aus, und klicken Sie auf die Schaltfläche **OK.**

Sie können die Assembly System.ComponentModel.DataAnnotations.dll, die in .NET Framework Service Pack 1 enthalten ist, nicht mit dem Modellbinder für Datenanmerkungen verwenden. Sie müssen die Version der System.ComponentModel.DataAnnotations.dll-Baugruppe verwenden, die im Beispieldownload des Modellbinder-Beispiels für Data Annotations Model Binder enthalten ist.

Schließlich müssen Sie den DataAnnotations Model Binder in der Datei Global.asax registrieren. Fügen Sie dem Application\_Start()-Ereignishandler die folgende\_Codezeile hinzu, damit die Application Start()-Methode wie folgt aussieht:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

Diese Codezeile registriert den DataAnnotationsModelBinder als Standardmodellbinder für die gesamte ASP.NET MVC-Anwendung.

## <a name="using-the-data-annotation-validator-attributes"></a>Verwenden der Data Annotation Validator-Attribute

Wenn Sie den Modellbinder für Datenanmerkungen verwenden, verwenden Sie Validatorattribute, um die Validierung durchzuführen. Der Namespace System.ComponentModel.DataAnnotations enthält die folgenden Validierungsattribute:

- Bereich – Ermöglicht es Ihnen zu überprüfen, ob der Wert einer Eigenschaft zwischen einem angegebenen Wertebereich liegt.
- RegularExpression – Ermöglicht es Ihnen, zu überprüfen, ob der Wert einer Eigenschaft mit einem angegebenen Muster für reguläre Ausdrücke übereinstimmt.
- Erforderlich – Ermöglicht es Ihnen, eine Eigenschaft nach Bedarf zu markieren.
- StringLength – Ermöglicht es Ihnen, eine maximale Länge für eine Zeichenfolgeneigenschaft anzugeben.
- Validierung – Die Basisklasse für alle Validatorattribute.

> [!NOTE] 
> 
> Wenn Ihre Validierungsanforderungen von keinem der Standardprüfer erfüllt werden, haben Sie immer die Möglichkeit, ein benutzerdefiniertes Validatorattribut zu erstellen, indem Sie ein neues Validatorattribut vom Basisvalidierungsattribut erben.

Die Produktklasse in **Liste 1** veranschaulicht, wie diese Validatorattribute verwendet werden. Die Eigenschaften Name, Beschreibung und UnitPrice werden als erforderlich markiert. Die Name-Eigenschaft muss eine Zeichenfolgenlänge von weniger als 10 Zeichen haben. Schließlich muss die UnitPrice-Eigenschaft mit einem Muster für reguläre Ausdrücke übereinstimmen, das einen Währungsbetrag darstellt.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**Auflistung 1**: Models-Produkt.vb

Die Produktklasse veranschaulicht, wie ein zusätzliches Attribut verwendet wird: das DisplayName-Attribut. Mit dem DisplayName-Attribut können Sie den Namen der Eigenschaft ändern, wenn die Eigenschaft in einer Fehlermeldung angezeigt wird. Anstatt die Fehlermeldung "Das UnitPrice-Feld ist erforderlich" anzuzeigen, können Sie die Fehlermeldung "Das Preisfeld ist erforderlich" anzeigen.

> [!NOTE] 
> 
> Wenn Sie die von einem Validator angezeigte Fehlermeldung vollständig anpassen möchten, können Sie der ErrorMessage-Eigenschaft des Validators wie folgt eine benutzerdefinierte Fehlermeldung zuweisen:`<Required(ErrorMessage:="This field needs a value!")>`

Sie können die Produktklasse in **Liste 1** mit der Aktion Create()-Controller in **Liste 2**verwenden. Diese Controlleraktion zeigt die Ansicht Erstellen erneut an, wenn der Modellstatus Fehler enthält.

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**Auflistung 2**: Controller-ProduktController.vb

Schließlich können Sie die Ansicht in **Liste 3** erstellen, indem Sie mit der rechten Maustaste auf die Aktion Erstellen() klicken und die Menüoption **Ansicht hinzufügen**auswählen. Erstellen Sie eine stark typisierte Ansicht mit der Produktklasse als Modellklasse. Wählen Sie **Erstellen** aus der Dropdownliste Ansichtsinhalt aus (siehe **Abbildung 2**).

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**Abbildung 2:** Hinzufügen der Erstellungsansicht

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**Auflisten 3**: Ansichten, Produkt, Create.aspx

> [!NOTE] 
> 
> Entfernen Sie das Feld Id aus dem Formular Erstellen, das durch die Menüoption **Ansicht hinzufügen** generiert wird. Da das Feld ID einer Spalte Identität entspricht, möchten Sie Benutzern nicht erlauben, einen Wert für dieses Feld einzugeben.

Wenn Sie das Formular zum Erstellen eines Produkts absenden und keine Werte für die erforderlichen Felder eingeben, werden die Validierungsfehlermeldungen in **Abbildung 3** angezeigt.

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**Abbildung 3:** Fehlende erforderliche Felder

Wenn Sie einen ungültigen Währungsbetrag eingeben, wird die Fehlermeldung in **Abbildung 4** angezeigt.

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**Abbildung 4:** Ungültiger Währungsbetrag

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Verwenden von Datenanmerkungsvalidierern mit dem Entity Framework

Wenn Sie das Microsoft Entity Framework zum Generieren Ihrer Datenmodellklassen verwenden, können Sie die Validatorattribute nicht direkt auf Ihre Klassen anwenden. Da der Entity Framework-Designer die Modellklassen generiert, werden alle Änderungen, die Sie an den Modellklassen vornehmen, beim nächsten Vornehmen von Änderungen im Designer überschrieben.

Wenn Sie die Validatoren mit den vom Entity Framework generierten Klassen verwenden möchten, müssen Sie Metadatenklassen erstellen. Sie wenden die Validatoren auf die Metadatenklasse an, anstatt die Validatoren auf die tatsächliche Klasse anzuwenden.

Stellen Sie sich beispielsweise vor, Sie hätten eine Movie-Klasse mit dem Entity Framework erstellt (siehe **Abbildung 5**). Stellen Sie sich außerdem vor, dass Sie die Eigenschaften Movie Title und Director zu erforderlichen Eigenschaften machen möchten. In diesem Fall können Sie die partielle Klasse und Die Metadatenklasse in **Listing 4**erstellen.

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**Abbildung 5:** Von Entity Framework generierte Filmklasse

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**Auflisten 4**: Models-Movie.vb

Die Datei in **Liste 4** enthält zwei Klassen mit dem Namen Movie und MovieMetaData. Die Movie-Klasse ist eine Teilklasse. Sie entspricht der partiellen Klasse, die vom Entity Framework generiert wird und in der Datei DataModel.Designer.vb enthalten ist.

Derzeit unterstützt das .NET-Framework keine partiellen Eigenschaften. Daher gibt es keine Möglichkeit, die Validator-Attribute auf die Eigenschaften der Movie-Klasse anzuwenden, die in der Datei DataModel.Designer.vb definiert sind, indem die Validator-Attribute auf die Eigenschaften der Movie-Klasse angewendet werden, die in der Datei in **Listing 4**definiert sind.

Beachten Sie, dass die partielle Movie-Klasse mit einem MetadataType-Attribut versehen ist, das auf die MovieMetaData-Klasse verweist. Die MovieMetaData-Klasse enthält Proxyeigenschaften für die Eigenschaften der Movie-Klasse.

Die Validatorattribute werden auf die Eigenschaften der MovieMetaData-Klasse angewendet. Die Eigenschaften Title, Director und DateReleased sind alle als erforderliche Eigenschaften gekennzeichnet. Der Director-Eigenschaft muss eine Zeichenfolge zugewiesen werden, die weniger als 5 Zeichen enthält. Schließlich wird das DisplayName-Attribut auf die DateReleased-Eigenschaft angewendet, um eine Fehlermeldung wie "Das Feld "Datum freigegeben" anzuzeigen. anstelle des Fehlers "Das Feld DateReleased ist erforderlich."

> [!NOTE] 
> 
> Beachten Sie, dass die Proxyeigenschaften in der MovieMetaData-Klasse nicht dieselben Typen wie die entsprechenden Eigenschaften in der Movie-Klasse darstellen müssen. Die Director-Eigenschaft ist z. B. eine Zeichenfolgeneigenschaft in der Movie-Klasse und eine Objekteigenschaft in der MovieMetaData-Klasse.

Die Seite in **Abbildung 6** veranschaulicht die Fehlermeldungen, die zurückgegeben werden, wenn Sie ungültige Werte für die Movie-Eigenschaften eingeben.

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**Abbildung 6:** Verwenden von Validatoren mit dem Entity Framework ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie gelernt, wie Sie den Datenanmerkungsmodellbinder nutzen können, um die Validierung in einer ASP.NET MVC-Anwendung durchzuführen. Sie haben gelernt, wie Sie die verschiedenen Typen von Validierungsattributen verwenden, z. B. die Attribute Erforderlich und StringLength. Sie haben auch gelernt, wie Sie diese Attribute verwenden, wenn Sie mit Microsoft Entity Framework arbeiten.

> [!div class="step-by-step"]
> [Vorherige](validating-with-a-service-layer-vb.md)
