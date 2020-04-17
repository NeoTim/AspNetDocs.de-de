---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Erstellen einer MVC 3-Anwendung mit Razor und unauffälligem JavaScript | Microsoft Docs
author: rick-anderson
description: Die Beispielwebanwendung "Benutzerliste" veranschaulicht, wie einfach es ist, ASP.NET MVC 3-Anwendungen mit dem Razor-Ansichtsmodul zu erstellen. Die Beispielanwendung...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542455"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Erstellen einer MVC 3-Anwendung mit Razor und unaufdringlichem JavaScript

von [Microsoft](https://github.com/microsoft)

> Die Beispielwebanwendung "Benutzerliste" veranschaulicht, wie einfach es ist, ASP.NET MVC 3-Anwendungen mit dem Razor-Ansichtsmodul zu erstellen. Die Beispielanwendung zeigt, wie Sie das neue Razor-Ansichtsmodul mit ASP.NET MVC-Version 3 und Visual Studio 2010 verwenden, um eine fiktive Benutzerlistenwebsite zu erstellen, die Funktionen wie das Erstellen, Anzeigen, Bearbeiten und Löschen von Benutzern enthält.
> 
> In diesem Tutorial werden die Schritte beschrieben, die zum Erstellen des Beispiels für die Benutzerliste ASP.NET MVC 3-Anwendung ausgeführt wurden. Zu diesem Thema steht ein Visual Studio-Projekt mit Demento-Quellcode von C- und VB-Quellcode zur Verfügung: [Herunterladen](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Wenn Sie Fragen zu diesem Tutorial haben, posten Sie diese bitte im [MVC-Forum](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Übersicht

Die Anwendung, die Sie erstellen werden, ist eine einfache Benutzerlisten-Website. Benutzer können Benutzerinformationen eingeben, anzeigen und aktualisieren.

![Beispielsite](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Sie können das Projekt VB und C- abgeschlossen [hier](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)herunterladen.

## <a name="creating-the-web-application"></a>Erstellen der Webanwendung

Um das Tutorial zu starten, öffnen Sie Visual Studio 2010, und erstellen Sie ein neues Projekt mit der *ASP.NET MVC 3 Web Anwendungsvorlage.* Benennen Sie &quot;die Anwendung&quot;Mvc3Razor .

[![Neues MVC 3-Projekt](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

Wählen Sie im Dialogfeld **Neue ASP.NET MVC 3-Projekt** die Option **Internetanwendung aus**, wählen Sie das Razor-Ansichtsmodul aus, und klicken Sie dann auf **OK**.

![Neue ASP.NET MVC 3 Projektdialog](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

In diesem Tutorial verwenden Sie nicht die ASP.NET Mitgliedschaftsanbieter, sodass Sie alle Dateien löschen können, die mit der Anmeldung und Mitgliedschaft verknüpft sind. Entfernen Sie im **Projektmappen-Explorer**die folgenden Dateien und Verzeichnisse:

- *Controller-KontoController*
- *Modelle- und Kontomodelle*
- *Ansichten,\\freigegebene _LogOnPartial*
- *Views-Konto* (und alle Dateien in diesem Verzeichnis)

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Bearbeiten Sie `<div>` die `logindisplay` <em>&quot;</em>&quot; <em> \_Datei Layout.cshtml,</em> und ersetzen Sie das Markup innerhalb des namens elements durch die Meldung Login Disabled . Das folgende Beispiel zeigt das neue Markup:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Hinzufügen des Modells

Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf den Ordner *"Modelle",* wählen **Sie Hinzufügen**aus, und klicken Sie dann auf **Klasse**.

![Neue Benutzer-Mdl-Klasse](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Geben Sie der Klassen den Namen `UserModel`. Ersetzen Sie den Inhalt der *UserModel-Datei* durch den folgenden Code:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Die `UserModel` Klasse stellt Benutzer dar. Jeder Member der Klasse wird mit dem [Attribut Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) aus dem [DataAnnotations-Namespace](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) mit Anmerkungen versehen. Die Attribute im [DataAnnotations-Namespace](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) bieten eine automatische client- und serverseitige Validierung für Webanwendungen.

Öffnen `HomeController` Sie die `using` Klasse, und fügen `UserModel` Sie `Users` eine Direktive hinzu, damit Sie auf die und-Klassen zugreifen können:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Fügen Sie `HomeController` kurz nach der Deklaration `Users` den folgenden Kommentar und den Verweis auf eine Klasse hinzu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Die `Users` Klasse ist ein vereinfachter In-Memory-Datenspeicher, den Sie in diesem Tutorial verwenden. In einer echten Anwendung würden Sie eine Datenbank verwenden, um Benutzerinformationen zu speichern. Die ersten Zeilen `HomeController` der Datei werden im folgenden Beispiel gezeigt:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Erstellen Sie die Anwendung so, dass das Benutzermodell im nächsten Schritt für den Gerüstbau-Assistenten verfügbar ist.

## <a name="creating-the-default-view"></a>Erstellen der Standardansicht

Der nächste Schritt besteht darin, eine Aktionsmethode und eine Ansicht hinzuzufügen, um die Benutzer anzuzeigen.

Löschen Sie die vorhandene Datei *"Ansichten", "Home" und "Index".* Sie erstellen eine neue *Indexdatei,* um die Benutzer anzuzeigen.

Ersetzen `HomeController` Sie in der Klasse `Index` den Inhalt der Methode durch den folgenden Code:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Klicken Sie mit `Index` der rechten Maustaste in die Methode, und klicken Sie dann auf **Ansicht hinzufügen**.

![Ansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Wählen Sie die Option **Eine stark typisierte Ansicht erstellen** aus. Wählen Sie für **Datenklasse Anzeigen**die Option **Mvc3Razor.Models.UserModel**aus. (Wenn **Mvc3Razor.Models.UserModel** im Feld **Datenklassenansicht** nicht angezeigt wird, müssen Sie das Projekt erstellen.) Stellen Sie sicher, dass das Ansichtsmodul auf **Razor**eingestellt ist. Legen Sie **Inhalt anzeigen** auf **Liste** fest, und klicken Sie dann auf **Hinzufügen**.

![Indexansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Die neue Ansicht erstellt automatisch ein Gerüst für die `Index` Benutzerdaten, die an die Ansicht übergeben werden. Untersuchen Sie die neu generierte Datei *"Ansichten" und "Home" und "Index".* Die Links **"Neu erstellen**", **"Bearbeiten**", **"Details"** und **"Löschen"** funktionieren nicht, aber der Rest der Seite ist funktionsfähig. Führen Sie die Seite aus. Es wird eine Liste der Benutzer angezeigt.

![Indexseite](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Öffnen Sie die Datei *Index.cshtml,* und ersetzen `ActionLink` Sie das Markup für **Bearbeiten**, **Details**und **Löschen durch** den folgenden Code:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Der Benutzername wird als ID verwendet, um den ausgewählten Datensatz in den **Verknüpfungen Bearbeiten**, **Details**und **Löschen** zu suchen.

## <a name="creating-the-details-view"></a>Erstellen der Detailansicht

Der nächste Schritt besteht `Details` darin, eine Aktionsmethode und -ansicht hinzuzufügen, um Benutzerdetails anzuzeigen.

![Details](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Fügen Sie `Details` dem Startcontroller die folgende Methode hinzu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Klicken Sie mit `Details` der rechten Maustaste in die Methode, und wählen Sie dann <strong>Ansicht hinzufügen</strong>aus. Stellen Sie sicher, dass das Feld <strong>Datenklassenansicht</strong> <strong>Mvc3Razor.Models.UserModel</strong><em>enthält.</em> Legen Sie <strong>Inhalt anzeigen</strong> auf <strong>Details</strong> fest, und klicken Sie dann auf <strong>Hinzufügen</strong>.

![Detailansicht hinzufügen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Führen Sie die Anwendung aus, und wählen Sie einen Detaillink aus. Das automatische Gerüst zeigt jede Eigenschaft im Modell an.

![Details](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Erstellen der Bearbeitungsansicht

Fügen Sie `Edit` dem Startcontroller die folgende Methode hinzu.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Fügen Sie eine Ansicht wie in den vorherigen Schritten hinzu, legen Sie jedoch **Inhalt** **bearbeiten**an.

![Hinzufügen der Bearbeitungsansicht](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Führen Sie die Anwendung aus, und bearbeiten Sie den Vor- und Nachnamen eines der Benutzer. Wenn Sie `DataAnnotation` gegen Einschränkungen verstoßen, die `UserModel` auf die Klasse angewendet wurden, werden beim Absenden des Formulars Validierungsfehler angezeigt, die durch Servercode erzeugt werden. Wenn Sie z. B. &quot;beim&quot; &quot;Absenden des Formulars den Vornamen Ann in A&quot;ändern, wird im Formular der folgende Fehler angezeigt:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

In diesem Tutorial behandeln Sie den Benutzernamen als Primärschlüssel. Daher kann die Benutzernameneigenschaft nicht geändert werden. Legen Sie in der Datei *Edit.cshtml* kurz nach der Anweisung den `Html.BeginForm` Benutzernamen als ausgeblendetes Feld fest. Dadurch wird die Eigenschaft im Modell übergeben. Das folgende Codefragment zeigt `Hidden` die Platzierung der Anweisung:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Ersetzen `TextBoxFor` Sie `ValidationMessageFor` das und das Markup für den Benutzernamen durch einen `DisplayFor` Aufruf. Die `DisplayFor` Methode zeigt die Eigenschaft als schreibgeschütztes Element an. Das folgende Beispiel enthält das vollständige Markup. Das `TextBoxFor` Original `ValidationMessageFor` und die Anrufe werden mit den Zeichen Razor`@* *@`begin-comment und end-comment ( ) auskommentiert.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Aktivieren der clientseitigen Validierung

Um die clientseitige Validierung in ASP.NET MVC 3 zu aktivieren, müssen Sie zwei Flags festlegen und drei JavaScript-Dateien einschließen.

Öffnen Sie die *Datei Web.config* der Anwendung. Überprüfen `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` sie und sind in den Anwendungseinstellungen auf true festgelegt. Das folgende Fragment aus der Stammdatei *Web.config* zeigt die richtigen Einstellungen an:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Das `UnobtrusiveJavaScriptEnabled` Festlegen auf true ermöglicht eine unauffällige Ajax- und unauffällige Clientvalidierung. Wenn Sie eine unauffällige Validierung verwenden, werden die Validierungsregeln in HTML5-Attribute umgewandelt. HTML5-Attributnamen können nur aus Kleinbuchstaben, Zahlen und Bindestrichen bestehen.

Das `ClientValidationEnabled` Festlegen auf true ermöglicht die clientseitige Validierung. Durch Festlegen dieser Schlüssel in der Datei *"Web.config"* der Anwendung aktivieren Sie die Clientvalidierung und unauffälliges JavaScript für die gesamte Anwendung. Sie können diese Einstellungen auch in einzelnen Ansichten oder in Controllermethoden aktivieren oder deaktivieren, indem Sie den folgenden Code verwenden:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Außerdem müssen Sie mehrere JavaScript-Dateien in die gerenderte Ansicht einschließen. Eine einfache Möglichkeit, JavaScript in alle Ansichten einzuschließen, besteht darin, sie der Datei *Views-Shared\\_Layout.cshtml* hinzuzufügen. Ersetzen `<head>` Sie das Element der * \_Datei Layout.cshtml* durch den folgenden Code:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

Die ersten beiden jQuery-Skripte werden vom Microsoft Ajax Content Delivery Network (CDN) gehostet. Durch die Nutzung des Microsoft Ajax CDN können Sie die Leistung Ihrer Anwendungen im ersten Treffer deutlich verbessern.

Führen Sie die Anwendung aus, und klicken Sie auf einen Bearbeitungslink. Zeigen Sie die Quelle der Seite im Browser an. Die Browserquelle zeigt viele Attribute `data-val` des Formulars (für die Datenvalidierung). Wenn die Clientvalidierung und unauffällige JavaScript aktiviert ist, enthalten Eingabefelder mit einer Clientvalidierungsregel das `data-val="true"` Attribut, um eine unauffällige Clientüberprüfung auszulösen. Beispielsweise wurde `City` das Feld im Modell mit dem [Attribut Erforderlich](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) eingerichtet, was zu dem HTML-Code führt, der im folgenden Beispiel gezeigt wird:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Für jede Clientvalidierungsregel wird ein Attribut `data-val-rulename="message"`hinzugefügt, das das Formular hat. Im `City` zuvor gezeigten Feldbeispiel generiert die erforderliche `data-val-required` Clientvalidierungsregel das Attribut und die Meldung &quot;Das Feld "Stadt" ist erforderlich.&quot; Führen Sie die Anwendung aus, bearbeiten `City` Sie einen der Benutzer, und löschen Sie das Feld. Wenn Sie das Feld aus der Registerkarte herauslassen, wird eine clientseitige Validierungsfehlermeldung angezeigt.

![Stadt erforderlich](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Ebenso wird für jeden Parameter in der Clientvalidierungsregel ein `data-val-rulename-paramname=paramvalue`Attribut hinzugefügt, das das Formular hat. Die `FirstName` Eigenschaft wird z. B. mit dem [StringLength-Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) mit Anmerkungen versehen und gibt eine Mindestlänge von 3 und eine maximale Länge von 8 an. Die benannte `length` Datenvalidierungsregel `max` hat den Parameternamen und den Parameterwert 8. Im Folgenden wird der HTML-Code angezeigt, der für das `FirstName` Feld generiert wird, wenn Sie einen der Benutzer bearbeiten:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Weitere Informationen zur unauffälligen Clientvalidierung finden Sie im Eintrag [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) im Blog von Brad Wilson.

> [!NOTE]
> In ASP.NET MVC 3 Beta müssen Sie das Formular manchmal einreichen, um die clientseitige Validierung zu starten. Dies kann für die endgültige Version geändert werden.

## <a name="creating-the-create-view"></a>Erstellen der Erstellungsansicht

Der nächste Schritt besteht `Create` darin, eine Aktionsmethode und -ansicht hinzuzufügen, damit der Benutzer einen neuen Benutzer erstellen kann. Fügen Sie `Create` dem Startcontroller die folgende Methode hinzu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Fügen Sie eine Ansicht wie in den vorherigen Schritten hinzu, legen Sie jedoch **Inhalt** anzeigen auf **Erstellen**fest.

![Erstellen einer Sicht](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Führen Sie die Anwendung aus, wählen Sie den Link **Erstellen** aus, und fügen Sie einen neuen Benutzer hinzu. Die `Create` Methode nutzt automatisch die client- und serverseitige Validierung. Versuchen Sie, einen Benutzernamen einzugeben, &quot;der&quot;Leerraum enthält, z. B. Ben X . Wenn Sie das Feld Benutzername ausklappen, wird`White space is not allowed`ein clientseitig ersichtlicher Validierungsfehler ( ) angezeigt.

## <a name="add-the-delete-method"></a>Hinzufügen der Delete-Methode

Um das Tutorial abzuschließen, `Delete` fügen Sie dem Startcontroller die folgende Methode hinzu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Fügen `Delete` Sie eine Ansicht wie in den vorherigen Schritten hinzu und legen Sie Inhalt **löschen** **ansichtsbereit** fest.

![Ansicht löschen](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Sie haben jetzt eine einfache, aber voll funktionsfähige ASP.NET MVC 3-Anwendung mit Validierung.
