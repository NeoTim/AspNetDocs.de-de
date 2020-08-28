---
uid: mvc/overview/getting-started/introduction/adding-validation
title: Hinzufügen der Validierung | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044349"
---
# <a name="adding-validation"></a>Hinzufügen der Validierung

von [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

In diesem Abschnitt fügen Sie dem Modell Validierungs Logik hinzu `Movie` , und Sie stellen sicher, dass die Validierungsregeln immer dann erzwungen werden, wenn ein Benutzer versucht, einen Film mit der Anwendung zu erstellen oder zu bearbeiten.

## <a name="keeping-things-dry"></a>Halten Sie die Dinge trocken

Eines der Kern Entwurfs-Grundsätze von ASP.NET MVC ist [Dry](http://en.wikipedia.org/wiki/Don't_repeat_yourself) ( &quot; Don't repeat yourself &quot; ). ASP.NET MVC fordert Sie auf, die Funktionalität oder das Verhalten nur einmal anzugeben, und kann es dann überall in einer Anwendung widerspiegeln. Dadurch wird der Code, den Sie schreiben müssen, reduziert, und der Code, den Sie schreiben, ist weniger fehleranfällig und leichter zu verwalten.

Die von ASP.NET MVC und Entity Framework Code First bereitgestellte Validierungs Unterstützung ist ein gutes Beispiel für das trockene Prinzip in Aktion. Sie können Validierungsregeln deklarativ an einem Ort angeben (in der Modell Klasse), und die Regeln werden überall in der Anwendung erzwungen.

Sehen wir uns nun an, wie Sie diese Validierungs Unterstützung in der Movie-Anwendung nutzen können.

## <a name="adding-validation-rules-to-the-movie-model"></a>Hinzufügen von Validierungsregeln zum Movie-Modell

Fügen Sie der-Klasse zunächst eine gewisse Validierungs Logik hinzu `Movie` .

Öffnen Sie Datei *Movie.cs*. Beachten Sie, dass der [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Namespace nicht enthält `System.Web` . DataAnnotations bietet eine integrierte Gruppe von Validierungs Attributen, die Sie deklarativ auf jede Klasse oder Eigenschaft anwenden können. (Es enthält auch Formatierungs Attribute wie [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , die bei der Formatierung helfen und keine Validierung bereitstellen.)

Aktualisieren Sie nun die `Movie` -Klasse, um die integrierten Attribute, [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)und Validation zu nutzen [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) . Ersetzen Sie die- `Movie` Klasse durch Folgendes:

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

Das [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) -Attribut legt die maximale Länge der Zeichenfolge fest und legt diese Einschränkung für die Datenbank fest. Daher ändert sich das Datenbankschema. Klicken Sie im **Server-Explorer** mit der rechten Maustaste auf die Tabelle **Filme** , und klicken Sie auf **Tabellen Definition öffnen**

![](adding-validation/_static/image1.png)

In der obigen Abbildung können Sie sehen, dass alle Zeichen folgen Felder auf [nvarchar (max)](https://technet.microsoft.com/library/ms186939.aspx)festgelegt sind. Wir werden Migrationen verwenden, um das Schema zu aktualisieren. Erstellen Sie die Projekt Mappe, öffnen Sie das Konsolenfenster des **Paket-Managers** , und geben Sie die folgenden Befehle ein:

[!code-console[Main](adding-validation/samples/sample2.cmd)]

Wenn dieser Befehl abgeschlossen ist, öffnet Visual Studio die Klassendatei, die die neue `DbMigration` abgeleitete Klasse mit dem angegebenen Namen definiert ( `DataAnnotations` ), und in der- `Up` Methode sehen Sie den Code, der die Schema Einschränkungen aktualisiert:

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

Das `Genre` Feld kann nicht mehr auf NULL festgelegt werden (d. h., Sie müssen einen Wert eingeben). Das `Rating` Feld hat eine maximale Länge von 5 und `Title` hat eine maximale Länge von 60. Die Mindestlänge von 3 auf, `Title` und der Bereich für `Price` hat keine Schema Änderungen erstellt.

Überprüfen Sie das Movie-Schema:

![](adding-validation/_static/image2.png)

Die Zeichen folgen Felder zeigen die neuen Längen Limits an und werden `Genre` nicht mehr als Nullable geprüft.

Die Validierungsattribute geben das Verhalten an, das Sie in den Modelleigenschaften erzwingen möchten, auf die sie angewendet werden. Die Attribute `Required` und `MinimumLength` geben an, dass eine Eigenschaft einen Wert haben muss. Ein Benutzer kann allerdings ein Leerzeichen eingeben, um diese Validierung zu erfüllen. Das [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) -Attribut wird verwendet, um einzuschränken, welche Zeichen eingegeben werden können. Im oben angegebenen Code sind für `Genre` und `Rating` nur Buchstaben (keine Leerzeichen, Zahlen und Sonderzeichen) erlaubt. Das [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) Attribut schränkt einen Wert innerhalb eines angegebenen Bereichs ein. Mit dem Attribut `StringLength` können Sie die maximale Länge einer Zeichenfolgeneigenschaft und optional die minimale Länge festlegen. Werttypen (z. b `decimal, int, float, DateTime` .) sind grundsätzlich erforderlich und benötigen nicht das `Required` Attribut.

Code First stellt sicher, dass die Validierungsregeln, die Sie für eine Modell Klasse angeben, erzwungen werden, bevor die Anwendung Änderungen in der Datenbank speichert. Beispielsweise löst der folgende Code eine [dbentityvalidationexception](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) -Ausnahme aus, wenn die- `SaveChanges` Methode aufgerufen wird, da mehrere erforderliche `Movie` Eigenschaftswerte fehlen:

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

Der obige Code löst die folgende Ausnahme aus:

*Fehler bei der Überprüfung für mindestens eine Entität. Weitere Informationen finden Sie unter der Eigenschaft "entityvalidationerrors".*

Das automatische Erzwingen von Validierungsregeln durch .NET Framework trägt dazu bei, die Anwendung stabiler zu machen. Darüber hinaus wird sichergestellt, dass Sie die Validierung nicht vergessen und nicht versehentlich falsche Daten in die Datenbank übernehmen.

## <a name="validation-error-ui-in-aspnet-mvc"></a>Validierungs Fehler-Benutzeroberfläche in ASP.NET MVC

Führen Sie die Anwendung aus, und navigieren Sie zur URL */Movies* .

Klicken Sie auf den Link **neu erstellen** , um einen neuen Film hinzuzufügen. Füllen Sie das Formular mit einigen ungültigen Werten aus. Wenn die clientseitige jQuery-Validierung den Fehler erkennt, wird eine Fehlermeldung angezeigt.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> um die jQuery-Validierung für nicht englische Gebiets Schemas zu unterstützen, die ein Komma (",") als Dezimaltrennzeichen verwenden, müssen Sie die nuget-Globalisierung wie zuvor in diesem Tutorial beschrieben einschließen.

Beachten Sie, dass das Formular automatisch eine rote Rahmenfarbe verwendet hat, um die Textfelder hervorzuheben, die ungültige Daten enthalten, und eine entsprechende Validierungs Fehlermeldung nebeneinander ausgegeben hat. Die Fehlermeldungen werden sowohl auf Clientseite (mithilfe von JavaScript und jQuery) als auch auf Serverseite erzwungen (wenn ein Benutzer JavaScript deaktiviert hat).

Ein echter Vorteil besteht darin, dass Sie eine einzelne Codezeile in der- `MoviesController` Klasse oder in der *Create. cshtml* -Sicht nicht ändern müssen, um diese Validierungs Benutzeroberfläche zu aktivieren. Die Controller und Ansichten, die Sie zuvor in diesem Tutorial erstellt haben, haben die angegebenen Validierungsregeln automatisch übernommen (mithilfe der Validierungsattribute für die Eigenschaften der Modellklasse `Movie`). Testen Sie die Validierung mithilfe der Aktionsmethode `Edit`, und es folgt die gleiche Validierung.

Die Formulardaten werden erst an den Server gesendet, wenn auf Clientseite keine Validierungsfehler mehr auftreten. Sie können dies überprüfen, indem Sie einen Haltepunkt in der HTTP Post-Methode verwenden, indem Sie das [Tool "Tools](http://fiddler2.com/fiddler2/)" oder die IE- [F12-Entwicklertools](https://msdn.microsoft.com/ie/aa740478)verwenden.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>So erfolgt die Überprüfung in der CREATE VIEW-und Create Action-Methode

Sie fragen sich vielleicht, wie die Benutzeroberfläche für die Validierung ohne Aktualisierungen von Code im Controller oder in Ansichten generiert wurde. Die nächste Liste zeigt, `Create` wie die Methoden in der `MovieController` Klasse aussehen. Sie sind unverändert, wie Sie Sie zuvor in diesem Tutorial erstellt haben.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

Die erste `Create`-Aktionsmethode (HTTP GET) zeigt das erste Formular „Create“ an. Die zweite Version (`[HttpPost]`) verarbeitet die Formularbereitstellung. Die zweite `Create` Methode (die `HttpPost` Version) überprüft `ModelState.IsValid` , ob für den Film Validierungs Fehler vorliegen. Wenn Sie diese Eigenschaft erhalten, werden alle Validierungs Attribute ausgewertet, die auf das Objekt angewendet wurden. Wenn das Objekt Überprüfungs Fehler aufweist, `Create` zeigt die Methode das Formular erneut an. Wenn keine Fehler vorliegen, speichert die Methode den neuen Film in der Datenbank. In unserem Movie-Beispiel wird **das Formular nicht an den Server gesendet, wenn Validierungs Fehler auf der Clientseite erkannt werden. die zweite** `Create` **Methode wird nie aufgerufen**. Wenn Sie JavaScript in Ihrem Browser deaktivieren, wird die Client Validierung deaktiviert, und mit der HTTP Post- `Create` Methode wird `ModelState.IsValid` überprüft, ob für den Film Validierungs Fehler vorliegen.

Sie können einen Haltepunkt in der `HttpPost Create`-Methode festlegen und überprüfen, ob die Methode tatsächlich niemals aufgerufen wird und die clientseitige Validierung die Formulardaten nicht sendet, wenn Validierungsfehler gefunden werden. Wenn Sie JavaScript in Ihrem Browser deaktivieren und dann das Formular mit Fehlern senden, wird der Haltepunkt erreicht. Sie erhalten auch ohne JavaScript weiterhin eine vollständige Validierung. In der folgenden Abbildung wird gezeigt, wie Sie JavaScript in Internet Explorer deaktivieren.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

Die folgende Abbildung zeigt, wie JavaScript im Firefox-Browser deaktiviert wird.

![](adding-validation/_static/image7.png)

Die folgende Abbildung zeigt, wie JavaScript im Chrome-Browser deaktiviert wird.

![](adding-validation/_static/image8.png)

Im folgenden finden Sie die *Ansichts Vorlage Create. cshtml* , die Sie zuvor in diesem Tutorial erstellt haben. Sie wird von den oben erläuterten Aktionsmethoden zum Anzeigen des anfänglichen Formulars und zum erneuten Anzeigen des Formulars bei einem Fehler verwendet.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

Beachten Sie, dass der Code ein `Html.EditorFor` Hilfsobjekt verwendet, um das- `<input>` Element für jede `Movie` Eigenschaft auszugeben. Neben diesem Hilfsprogramm ist ein aufzurufende `Html.ValidationMessageFor` Hilfsmethode. Diese beiden Hilfsmethoden arbeiten mit dem Modell Objekt, das vom Controller an die Ansicht (in diesem Fall ein-Objekt) übermittelt wird `Movie` . Sie suchen automatisch nach Validierungs Attributen, die im Modell angegeben sind, und zeigen Fehlermeldungen nach Bedarf an.

Wirklich nützlich an diesem Ansatz ist, dass weder der Controller noch die Ansichtsvorlage `Create` an den eigentlichen Validierungsregeln, die erzwungen werden, oder den spezifischen Fehlermeldungen, die angezeigt werden, beteiligt sind. Die Validierungsregeln und Fehlerzeichenfolgen werden nur in der `Movie`-Klasse angegeben. Diese gleichen Validierungsregeln werden automatisch auf die Ansicht `Edit` und alle anderen Ansichtsvorlagen angewendet, die Sie erstellen und die das Modell bearbeiten.

Wenn Sie die Validierungs Logik zu einem späteren Zeitpunkt ändern möchten, können Sie dies an genau einem Ort tun, indem Sie dem Modell Validierungs Attribute hinzufügen (in diesem Beispiel die- `movie` Klasse). Sie müssen sich keine Gedanken darüber machen, ob die verschiedenen Teile der Anwendung inkonsistent sind und wie Regeln erzwungen werden: Die gesamte Validierungslogik wird zentral definiert und überall verwendet. Dies hält den Code sehr übersichtlich und vereinfacht die Verwaltung und Entwicklung. Dies bedeutet, dass Sie das *trockene* Prinzip vollständig berücksichtigen werden.

## <a name="using-datatype-attributes"></a>Verwenden von „DataType“-Attributen

Öffnen Sie die Datei *Movie.cs*, und überprüfen Sie die Klasse `Movie`. Der- [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Namespace stellt zusätzlich zum integrierten Satz von Validierungs Attributen Formatierungs Attribute bereit. Wir haben bereits einen [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) -Enumerationswert auf das Veröffentlichungsdatum und die Preis Felder angewendet. Der folgende Code zeigt die `ReleaseDate` -Eigenschaft und die- `Price` Eigenschaft mit dem entsprechenden- [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) Attribut.

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribute enthalten nur Hinweise für die Anzeige-Engine zum Formatieren der Daten (und zum Bereitstellen von Attributen wie `<a>` für URLs und `<a href="mailto:EmailAddress.com">` für e-Mail). Sie können das [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) -Attribut verwenden, um das Format der Daten zu validieren. Das [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribut wird verwendet, um einen Datentyp anzugeben, der spezifischer als der systeminterne Typ der Datenbank ist. es handelt sich ***nicht*** um Validierungs Attribute. In diesem Fall soll nur das Datum verfolgt werden, nicht das Datum und die Zeit. Die [DataType-Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) stellt viele Datentypen bereit, wie z. b. *Datum, Uhrzeit, PhoneNumber, Currency, EmailAddress* usw. Das `DataType`-Attribut kann der Anwendung auch ermöglichen, typspezifische Features bereitzustellen. Beispielsweise kann ein `mailto:` Link für [DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)erstellt werden, und für [DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in Browsern, die [HTML5](http://html5.org/)unterstützen, kann eine Datumsauswahl angegeben werden. Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribute gibt HTML 5-Attribute aus *data dash*, die von HTML 5 [-](http://ejohn.org/blog/html-5-data-attributes/) Browsern verstanden werden können. Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribute bieten keine Validierung.

`DataType.Date` gibt nicht das Format des Datums an, das angezeigt wird. Standardmäßig wird das Datenfeld gemäß den Standardformaten basierend auf der [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)des Servers angezeigt.

Das `DisplayFormat`-Attribut dient zum expliziten Angeben des Datumsformats:

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

Die- `ApplyFormatInEditMode` Einstellung gibt an, dass die angegebene Formatierung auch angewendet werden soll, wenn der Wert zur Bearbeitung in einem Textfeld angezeigt wird. (Möglicherweise möchten Sie das Währungssymbol für einige Felder nicht ändern – z. b. für Währungswerte ist es möglicherweise nicht erforderlich, dass das Währungssymbol im Textfeld bearbeitet wird.)

Sie können das [Display Format](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) -Attribut eigenständig verwenden, aber es ist in der Regel eine gute Idee, auch das [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribut zu verwenden. Das `DataType` -Attribut überträgt die *Semantik* der Daten im Gegensatz zum Rendering auf einem Bildschirm und bietet die folgenden Vorteile, die Sie nicht erhalten `DisplayFormat` :

- Der Browser kann HTML5-Features aktivieren (z. b. zum Anzeigen eines Kalender Steuer Elements, des Gebiets Schema-entsprechenden Währungs Symbols, von e-Mail-Links usw.).
- Standardmäßig wird der Browserdaten basierend [auf Ihrem Gebiets](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)Schema im richtigen Format Rendering.
- Das [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) -Attribut kann MVC ermöglichen, die richtige Feld Vorlage zum renderingder Daten auszuwählen ( [Display Format](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , wenn es eigenständig verwendet wird, verwendet die Zeichen folgen Vorlage). Weitere Informationen finden Sie in den Vorlagen von Brad Wilson [ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (Obwohl für MVC 2 geschrieben, gilt dieser Artikel weiterhin für die aktuelle Version von ASP.NET MVC.)

Wenn Sie das- `DataType` Attribut mit einem Datumsfeld verwenden, müssen Sie auch das-Attribut angeben, um `DisplayFormat` sicherzustellen, dass das Feld ordnungsgemäß in Chrome-Browsern gerendert wird. Weitere Informationen finden Sie in [diesem StackOverflow-Thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

> [!NOTE]
> die jQuery-Validierung funktioniert nicht mit dem [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) -Attribut und dem [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)-Wert. Bei folgendem Code wird z.B. stets ein clientseitiger Validierungsfehler angezeigt, auch wenn sich das Datum im angegebenen Bereich befindet:
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> Sie müssen die jQuery-Datums Überprüfung deaktivieren, damit das [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) -Attribut mit [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)verwendet werden kann. Es ist in der Regel nicht empfehlenswert, harte Daten in ihren Modellen zu kompilieren, weshalb die Verwendung des [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) -Attributs und des [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) -Attributs nicht empfehlenswert ist.

Der folgende Code zeigt die Kombination von Attributen in einer Zeile:

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

Im nächsten Teil der Reihe überprüfen wir die Anwendung und nehmen einige Verbesserungen an den automatisch generierten Methoden `Details` und `Delete` vor.

> [!div class="step-by-step"]
> [Zurück](adding-a-new-field.md)
> [Weiter](examining-the-details-and-delete-methods.md)
