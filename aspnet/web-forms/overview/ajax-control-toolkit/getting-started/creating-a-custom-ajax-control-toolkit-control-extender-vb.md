---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: Erstellen eines benutzerdefinierten AJAX Control Toolkit Control Extenders (VB) | Microsoft Docs
author: rick-anderson
description: Mit benutzerdefinierten Extendern können Sie die Funktionen von ASP.NET Steuerelementen anpassen und erweitern, ohne neue Klassen erstellen zu müssen.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: adce8e23ccf0a3364ee85534e98f8ea67ae4718d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543677"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>Erstellen eines benutzerdefinierten AJAX Control Toolkit-Steuerelement-Extenders (VB)

von [Microsoft](https://github.com/microsoft)

> Mit benutzerdefinierten Extendern können Sie die Funktionen von ASP.NET Steuerelementen anpassen und erweitern, ohne neue Klassen erstellen zu müssen.

In diesem Tutorial erfahren Sie, wie Sie einen benutzerdefinierten AJAX Control Toolkit-Steuerelement-Extender erstellen. Wir erstellen einen einfachen, aber nützlichen neuen Extender, der den Status einer Schaltfläche von deaktiviert in aktiviert ändert, wenn Sie Text in eine Textbox eingeben. Nachdem Sie dieses Tutorial gelesen haben, können Sie das ASP.NET AJAX Toolkit um eigene Steuerelement-Extender erweitern.

Sie können benutzerdefinierte Steuerelementerweiterungen mit Visual Studio oder Visual Web Developer erstellen (stellen Sie sicher, dass Sie über die neueste Version von Visual Web Developer verfügen).

## <a name="overview-of-the-disabledbutton-extender"></a>Übersicht über den DisabledButton Extender

Unser neuer Control Extender heißt DisabledButton Extender. Dieser Extender hat drei Eigenschaften:

- TargetControlID - Die TextBox, die das Steuerelement erweitert.
- TargetButtonIID - Die Schaltfläche, die deaktiviert oder aktiviert ist.
- DisabledText - Der Text, der ursprünglich in der Schaltfläche angezeigt wird. Wenn Sie mit der Eingabe beginnen, zeigt die Schaltfläche den Wert der Button Text-Eigenschaft an.

Sie verbinden den DisabledButton-Extender mit einem TextBox- und Button-Steuerelement. Bevor Sie Text eingeben, ist die Schaltfläche deaktiviert, und textBox und Button sehen wie folgt aus:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))

Nachdem Sie mit der Eingabe von Text begonnen haben, ist die Schaltfläche aktiviert, und TextBox und Button sehen wie folgt aus:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))

Um unseren Control Extender zu erstellen, müssen wir die folgenden drei Dateien erstellen:

- DisabledButtonExtender.vb – Diese Datei ist die serverseitige Steuerungsklasse, die das Erstellen des Extenders verwaltet und es Ihnen ermöglicht, die Eigenschaften zur Entwurfszeit festzulegen. Außerdem werden die Eigenschaften definiert, die für den Extender festgelegt werden können. Auf diese Eigenschaften kann über Code und zur Entwurfszeit zugegriffen werden und die in der Datei DisableButtonBehavior.js definierten Eigenschaften übereinstimmen.
- DisabledButtonBehavior.js – In dieser Datei fügen Sie die gesamte Clientskriptlogik hinzu.
- DisabledButtonDesigner.vb - Diese Klasse ermöglicht Entwurfszeitfunktionen. Sie benötigen diese Klasse, wenn der Steuerelement-Extender ordnungsgemäß mit dem Visual Studio/Visual Web Developer Designer funktionieren soll.

Ein Steuerelement-Extender besteht also aus einem serverseitigen Steuerelement, einem clientseitigen Verhalten und einer serverseitigen Designerklasse. In den folgenden Abschnitten erfahren Sie, wie Sie alle drei Dateien erstellen.

## <a name="creating-the-custom-extender-website-and-project"></a>Erstellen der Custom Extender-Website und des Projekts

Der erste Schritt besteht darin, ein Klassenbibliotheksprojekt und eine Website in Visual Studio/Visual Web Developer zu erstellen. Wir erstellen den benutzerdefinierten Extender im Klassenbibliotheksprojekt und testen den benutzerdefinierten Extender auf der Website.

Beginnen wir mit der Website. Führen Sie die folgenden Schritte aus, um die Website zu erstellen:

1. Wählen Sie die Menüoption **Datei, Neue Website**.
2. Wählen Sie die **ASP.NET Websitevorlage** aus.
3. Benennen Sie die neue Website *Website1*.
4. Klicken Sie auf die Schaltfläche **OK** .

Als Nächstes müssen wir das Klassenbibliotheksprojekt erstellen, das den Code für den Steuerelement-Extender enthält:

1. Wählen Sie die Menüoption **Datei, Hinzufügen, Neues Projekt**.
2. Wählen Sie die **Vorlage Klassenbibliothek** aus.
3. Benennen Sie die neue Klassenbibliothek mit dem Namen **CustomExtenders**.
4. Klicken Sie auf die Schaltfläche **OK** .

Nachdem Sie diese Schritte ausgeführt haben, sollte das Projektmappen-Explorer-Fenster wie Abbildung 1 aussehen.

[![Lösung mit Website- und Klassenbibliotheksprojekt](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**Abbildung 01**: Lösung mit Website- und Klassenbibliotheksprojekt ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))

Als Nächstes müssen Sie alle erforderlichen Assemblyverweise zum Klassenbibliotheksprojekt hinzufügen:

1. Klicken Sie mit der rechten Maustaste auf das CustomExtenders-Projekt, und wählen Sie die Menüoption **Referenz hinzufügen**aus.
2. Wählen Sie die Registerkarte .NET aus.
3. Fügen Sie Verweise auf die folgenden Assemblys hinzu:

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. Wählen Sie die Registerkarte Durchsuchen aus.
5. Fügen Sie einen Verweis auf die AjaxControlToolkit.dll-Assembly hinzu. Diese Assembly befindet sich in dem Ordner, in den Sie das AJAX Control Toolkit heruntergeladen haben.

Sie können überprüfen, ob Sie alle richtigen Referenzen hinzugefügt haben, indem Sie mit der rechten Maustaste auf Ihr Projekt klicken, Eigenschaften auswählen und auf die Registerkarte Referenzen klicken (siehe Abbildung 2).

[![Referenzordner mit erforderlichen Referenzen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**Abbildung 02**: Referenzordner mit erforderlichen Referenzen([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)

## <a name="creating-the-custom-control-extender"></a>Erstellen des benutzerdefinierten Steuerelement-Extenders

Jetzt, da wir unsere Klassenbibliothek haben, können wir mit dem Aufbau unserer Extender-Steuerung beginnen. Beginnen wir mit den nackten Knochen einer benutzerdefinierten Extender-Steuerelementklasse (siehe Liste 1).

**Auflistung 1 - MyCustomExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

Es gibt mehrere Dinge, die Sie über die Control Extender-Klasse in Listing 1 bemerken. Beachten Sie zunächst, dass die Klasse von der Base ExtenderControlBase-Klasse erbt. Alle AJAX Control Toolkit-Extendersteuerelemente stammen von dieser Basisklasse. Die Basisklasse enthält z. B. die TargetID-Eigenschaft, die eine erforderliche Eigenschaft jedes Steuerelement-Extenders ist.

Beachten Sie als Nächstes, dass die Klasse die folgenden beiden Attribute im Zusammenhang mit Clientskript enthält:

- WebResource - Bewirkt, dass eine Datei als eingebettete Ressource in eine Assembly eingeschlossen wird.
- ClientScriptResource : Bewirkt, dass eine Skriptressource aus einer Assembly abgerufen wird.

Das WebResource-Attribut wird verwendet, um die JavaScript-Datei MyControlBehavior.js in die Assembly einzubetten, wenn der benutzerdefinierte Extender kompiliert wird. Das ClientScriptResource-Attribut wird verwendet, um das Skript MyControlBehavior.js aus der Assembly abzurufen, wenn der benutzerdefinierte Extender in einer Webseite verwendet wird.

Damit die Attribute WebResource und ClientScriptResource funktionieren, müssen Sie die JavaScript-Datei als eingebettete Ressource kompilieren. Wählen Sie die Datei im Projektmappen-Explorer-Fenster aus, öffnen Sie das Eigenschaftenblatt, und weisen Sie den Wert *Embedded Resource* der **BuildAktion-Eigenschaft** zu.

Beachten Sie, dass der Steuerelement-Extender auch ein TargetControlType-Attribut enthält. Dieses Attribut wird verwendet, um den Typ des Steuerelements anzugeben, der durch den Steuerelementerweiterungser erweitert wird. Im Fall von Listing 1 wird der Control Extender verwendet, um eine TextBox zu erweitern.

Beachten Sie schließlich, dass der benutzerdefinierte Extender eine Eigenschaft mit dem Namen MyProperty enthält. Die Eigenschaft ist mit dem Attribut ExtenderControlProperty gekennzeichnet. Die Methoden GetPropertyValue() und SetPropertyValue() werden verwendet, um den Eigenschaftswert vom serverseitigen Steuerelement-Extender an das clientseitige Verhalten zu übergeben.

Lassen Sie uns fortfahren und den Code für unseren DisabledButton-Extender implementieren. Der Code für diesen Extender finden Sie in Liste 2.

**Eintrag 2 - DisabledButtonExtender.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

Der DisabledButton-Extender in Listing 2 verfügt über zwei Eigenschaften mit dem Namen TargetButtonID und DisabledText. Die IDReferenceProperty, die auf die TargetButtonID-Eigenschaft angewendet wird, verhindert, dass Sie dieser Eigenschaft etwas anderes als die ID eines Schaltflächensteuerelements zuweisen.

Die Attribute WebResource und ClientScriptResource ordnen diesem Extender ein clientseitiges Verhalten in einer Datei mit dem Namen DisabledButtonBehavior.js zu. Wir besprechen diese JavaScript-Datei im nächsten Abschnitt.

## <a name="creating-the-custom-extender-behavior"></a>Erstellen des benutzerdefinierten Extenderverhaltens

Die clientseitige Komponente eines Steuerelement-Extenders wird als Verhalten bezeichnet. Die eigentliche Logik zum Deaktivieren und Aktivieren der Schaltfläche ist im DisabledButton-Verhalten enthalten. Der JavaScript-Code für das Verhalten ist in Liste 3 enthalten.

**Auflistung 3 - DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

Die JavaScript-Datei in Listing 3 enthält eine clientseitige Klasse mit dem Namen DisabledButtonBehavior. Diese Klasse enthält, wie ihr serverseitiger Zwilling, zwei Eigenschaften namens TargetButtonID und\_DisabledText, auf\_die Sie mithilfe von get\_TargetButtonID/set TargetButtonID und get DisabledText/set\_DisabledText zugreifen können.

Die initialize()-Methode ordnet dem Zielelement für das Verhalten einen Keyup-Ereignishandler zu. Jedes Mal, wenn Sie einen Buchstaben in die TextBox eingeben, die diesem Verhalten zugeordnet ist, wird der Keyuphandler ausgeführt. Der Keyup-Handler aktiviert oder deaktiviert die Schaltfläche, je nachdem, ob die dem Verhalten zugeordnete TextBox Text enthält.

Denken Sie daran, dass Sie die JavaScript-Datei in Liste 3 als eingebettete Ressource kompilieren müssen. Wählen Sie die Datei im Projektmappen-Explorer-Fenster aus, öffnen Sie das Eigenschaftenblatt, und weisen Sie den Wert *Embedded Resource* der **BuildAktionseigenschaft** zu (siehe Abbildung 3). Diese Option ist sowohl in Visual Studio als auch in Visual Web Developer verfügbar.

[![Hinzufügen einer JavaScript-Datei als eingebettete Ressource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**Abbildung 03**: Hinzufügen einer JavaScript-Datei als eingebettete Ressource ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>Erstellen des custom Extender Designers

Es gibt eine letzte Klasse, die wir erstellen müssen, um unseren Extender zu vervollständigen. Wir müssen die Designerklasse in Listing 4 erstellen. Diese Klasse ist erforderlich, damit sich der Extender mit dem Visual Studio/Visual Web Developer Designer korrekt verhält.

**Eintrag 4 - DisabledButtonDesigner.vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

Sie ordnen den Designer in Listing 4 dem DisabledButton-Extender dem Designer-Attribut zu. Sie müssen das Designer-Attribut wie folgt auf die DisabledButtonExtender-Klasse anwenden:

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>Verwenden des benutzerdefinierten Extenders

Nachdem wir den DisabledButton-Steuerelement-Extender erstellt haben, ist es an der Zeit, ihn in unserer ASP.NET-Website zu verwenden. Zuerst müssen wir den benutzerdefinierten Extender zur Toolbox hinzufügen. Folgen Sie diesen Schritten:

1. Öffnen Sie eine ASP.NET Seite, indem Sie im Projektmappen-Explorer-Fenster auf die Seite doppelklicken.
2. Klicken Sie mit der rechten Maustaste auf die Toolbox und wählen Sie die Menüoption **Elemente auswählen**.
3. Navigieren Sie im Dialogfeld Toolbox-Elemente auswählen zur Assembly CustomExtenders.dll.
4. Klicken Sie auf die Schaltfläche **OK,** um das Dialogfeld zu schließen.

Nachdem Sie diese Schritte ausgeführt haben, sollte der DisabledButton-Steuerelement-Extender in der Toolbox angezeigt werden (siehe Abbildung 4).

[![DisabledButton in der Toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**Abbildung 04**: DisabledButton in der Toolbox([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)

Als Nächstes müssen wir eine neue ASP.NET Seite erstellen. Folgen Sie diesen Schritten:

1. Erstellen Sie eine neue ASP.NET Seite mit dem Namen ShowDisabledButton.aspx.
2. Ziehen Sie einen ScriptManager auf das Zeichenblatt.
3. Ziehen Sie ein TextBox-Steuerelement auf die Seite.
4. Ziehen Sie ein Schaltflächensteuerelement auf das Zeichenblatt.
5. Ändern Sie im Eigenschaftenfenster die Button ID-Eigenschaft in den Wert <em>btnSave</em> und die Text-Eigenschaft in den Wert *\*Speichern*.

Wir haben eine Seite mit einem Standard-ASP.NET TextBox- und Button-Steuerelement erstellt.

Als Nächstes müssen wir das TextBox-Steuerelement mit dem DisabledButton-Extender erweitern:

1. Wählen Sie die Option **Extender hinzufügen** aus, um das Dialogfeld Extender-Assistent zu öffnen (siehe Abbildung 5). Beachten Sie, dass das Dialogfeld unseren benutzerdefinierten DisabledButton-Extender enthält.
2. Wählen Sie den DisabledButton Extender aus, und klicken Sie auf **ok.**

[![Dialogfeld "Extender-Assistent"](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**Abbildung 05**: Dialogfeld des Extender-Assistenten ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))

Schließlich können wir die Eigenschaften des DisabledButton-Extenders festlegen. Sie können die Eigenschaften des DisabledButton-Extenders ändern, indem Sie die Eigenschaften des TextBox-Steuerelements ändern:

1. Wählen Sie die TextBox im Designer aus.
2. Erweitern Sie im Fenster Eigenschaften den Extender-Knoten (siehe Abbildung 6).
3. Weisen Sie der DisabledText-Eigenschaft den Wert *Save* und der Wert *btnSave* der TargetButtonID-Eigenschaft zu.

[![Festlegen von Extendereigenschaften](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**Abbildung 06**: Festlegen von Extendereigenschaften ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))

Wenn Sie die Seite ausführen (durch Drücken von F5), wird das Button-Steuerelement zunächst deaktiviert. Sobald Sie mit der Eingabe von Text in die TextBox beginnen, wird das Button-Steuerelement aktiviert (siehe Abbildung 7).

[![Der DisabledButton-Extender in Aktion](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**Abbildung 07**: Der DisabledButton Extender in Aktion ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu erklären, wie Sie das AJAX Control Toolkit mit benutzerdefinierten Extender-Steuerelementen erweitern können. In diesem Tutorial haben wir einen einfachen DisabledButton-Steuerelement-Extender erstellt. Wir haben diesen Extender implementiert, indem wir eine DisabledButtonExtender-Klasse, ein DisabledButtonBehavior JavaScript-Verhalten und eine DisabledButtonDesigner-Klasse erstellt haben. Sie führen ähnliche Schritte aus, wenn Sie einen benutzerdefinierten Steuerelement-Extender erstellen.

> [!div class="step-by-step"]
> [Vorherige](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
