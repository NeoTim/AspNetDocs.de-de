---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: Erstellen ein komplexeres Datenmodell für eine ASP.NET MVC-Anwendung (4 von 10) | Microsoft-Dokumentation
author: tdykstra
description: Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET MVC 4-Anwendungen, die mit dem Entity Framework 5 Code First "und" Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 2ba7ca22074fe3c131209482180f8f7706714dd5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129834"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>Erstellen ein komplexeres Datenmodell für eine ASP.NET MVC-Anwendung (4 von 10)

durch [Tom Dykstra](https://github.com/tdykstra)

[Abgeschlossenes Projekt herunterladen](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET MVC 4-Anwendungen, die mit dem Entity Framework 5 Code First "und" Visual Studio 2012. Informationen zu dieser Tutorialreihe finden Sie im [ersten Tutorial der Reihe](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Sie können die tutorialreihe vom Anfang starten oder [Herunterladen eines Startprojekts für dieses Kapitel](building-the-ef5-mvc4-chapter-downloads.md) und beginnen Sie hier.
> 
> > [!NOTE] 
> > 
> > Wenn Sie auf ein Problem Sie nicht lösen stoßen, [herunterladen im Kapitel über das abgeschlossene](building-the-ef5-mvc4-chapter-downloads.md) und versuchen Sie es zum Reproduzieren des Problems an. Die Lösung des Problems finden in der Regel durch Ihren Code, den vollständigen Code vergleichen. Einige häufige Fehler und zu deren Lösung finden Sie [Fehler und Problemumgehungen.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

In den vorherigen Tutorials haben Sie mit einem einfachen Datenmodell, das aus drei Entitäten Bestand aus. In diesem Tutorial fügen Sie weitere Entitäten und Beziehungen, und passen das Datenmodell von Formatierung, Validierung und Zuordnungsregeln für die Datenbank angeben. Sehen Sie zwei Möglichkeiten zum Anpassen des Datenmodells: durch Hinzufügen von Attributen, um Entitätsklassen und indem Sie Code hinzufügen, um den Datenbankkontext-Klasse.

Wenn Sie dies erledigt haben, bilden die Entitätsklassen ein vollständiges Datenmodell, das in der folgenden Abbildung dargestellt wird:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>Anpassen des Datenmodells mithilfe von Attributen

In diesem Abschnitt wird das Anpassen des Datenmodells mithilfe von Attributen erläutert, die Regeln zur Formatierung, Validierung und Datenbankzuordnung angeben. In einigen der in den folgenden Abschnitten Sie die vollständige erstellen werden `School` Datenmodell durch Hinzufügen von Attributen auf Klassen Sie bereits erstellte, und erstellen neue Klassen, die für die verbleibenden Entitätstypen im Modell.

### <a name="the-datatype-attribute"></a>Das DataType-Attribut

Für die Anmeldedaten von Studenten zeigen alle Webseiten derzeit die Zeit und das Datum an, obwohl für dieses Feld nur das Datum relevant ist. Indem Sie Attribute für die Datenanmerkung verwenden, können Sie eine Codeänderungen vornehmen, durch die das Anzeigeformat in jeder Ansicht korrigiert wird, in der die Daten angezeigt werden. Sie können dies beispielhaft testen, indem Sie ein Attribut zur `EnrollmentDate`-Eigenschaft der `Student`-Klasse hinzufügen.

In *Models\Student.cs*, Hinzufügen einer `using` -Anweisung für die `System.ComponentModel.DataAnnotations` Namespace und fügen `DataType` und `DisplayFormat` Attribute der `EnrollmentDate` -Eigenschaft, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) Attribut wird verwendet, um einen Datentyp anzugeben, der spezifischer als der datenbankinterne Typ ist. In diesem Fall soll nur das Datum verfolgt werden, nicht das Datum und die Zeit. Die [DataType-Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) stellt viele Datentypen, z. B. *Datum "," Uhrzeit "," PhoneNumber "," Währung "," EmailAddress* und vieles mehr. Das `DataType`-Attribut kann der Anwendung auch ermöglichen, typspezifische Features bereitzustellen. Z. B. eine `mailto:` Link erstellt werden kann, für die [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), und eine Datumsauswahl kann angegeben werden, für die [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in Browsern mit Unterstützung [HTML5](http://html5.org/). Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) Attribute gibt HTML 5 [Data -](http://ejohn.org/blog/html-5-data-attributes/) (ausgesprochen als *Daten Dash*) Attribute, die HTML5-Browsern genutzt werden können. Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) Attribute bieten keine Validierung.

`DataType.Date` gibt nicht das Format des Datums an, das angezeigt wird. Standardmäßig wird das Datenfeld gemäß den Standardformaten basierend auf dem Server des [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).

Das `DisplayFormat`-Attribut dient zum expliziten Angeben des Datumsformats:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

Die `ApplyFormatInEditMode` Einstellung gibt an, dass die angegebene Formatierung auch angewendet werden soll, wenn der Wert in einem Textfeld zur Bearbeitung angezeigt wird. (Möchten Sie vielleicht nicht, die für einige Felder, z. B. für Währungsangaben nicht empfiehlt das Währungssymbol im Textfeld für die Bearbeitung.)

Können Sie die [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) Attribut selbst, aber es ist im Allgemeinen eine gute Idee, verwenden Sie die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) auch Attribut. Die `DataType` -Attribut übermittelt die *Semantik* der Daten als dagegen spricht, wie sie auf dem Bildschirm gerendert, und bietet die folgenden Vorteile, die nicht im Lieferumfang enthalten `DisplayFormat`:

- Der Browser kann HTML5-Features (z. B. zum Anzeigen eines Kalendersteuerelements, dem Gebietsschema entsprechenden Währungssymbols, e-Mail-Links usw.) aktivieren.
- Standardmäßig rendert der Browser Daten mit dem richtigen Format basierend auf Ihrer [Gebietsschema](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- Die [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) Attribut kann MVC die richtige Feldvorlage zum Rendern der Daten auswählen zu aktivieren (die [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) von verwendet selbst verwendet die zeichenfolgenvorlage). Weitere Informationen finden Sie in Brad Wilsons [ASP.NET MVC 2-Vorlagen](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (Obwohl für MVC 2 geschrieben wird, gilt in diesem Artikel noch auf die aktuelle Version von ASP.NET MVC.)

Bei Verwendung der `DataType` Attribut mit einem Datumsfeld müssen Sie angeben der `DisplayFormat` Attribut auch, um sicherzustellen, dass das Feld in Chrome-Browsern richtig gerendert wird. Weitere Informationen finden Sie unter [dieser Stack Overflow-Thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

Führen Sie die Seite "Student" Index erneut aus, und beachten Sie, wie oft die Uhrzeit nicht mehr angezeigt werden. Dasselbe gilt für jede Ansicht, die verwendet werden die `Student` Modell.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>Des StringLengthAttribute

Sie können auch Regeln für die datenvalidierung und Meldungen, die mithilfe von Attributen angeben. Angenommen, Sie möchten sicherstellen, dass Benutzer nicht mehr als 50 Zeichen für einen Namen eingeben. Um diese Einschränkung hinzuzufügen, fügen [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) Attribute der `LastName` und `FirstMidName` Eigenschaften, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

Die [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) Attribut wird nicht verhindert, dass ein Benutzer Leerraum als Namen eingibt. Sie können die [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) Attribut, um Einschränkungen auf die Eingabe anzuwenden. Der folgende Code ist z. B. erforderlich, das erste Zeichen in Großbuchstaben geschrieben werden und die restlichen Zeichen alphabetisch sein müssen:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

Die [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) -Attribut stellt ähnliche Funktionalität wie die [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) Attribut jedoch keine clientseitige Validierung.

Führen Sie die Anwendung, und klicken Sie auf die **Schüler/Studenten** Registerkarte. Sie erhalten die folgende Fehlermeldung:

*Das Modell, das den Kontext "SchoolContext" unterstützt wurde geändert, da die Datenbank erstellt wurde. Erwägen Sie die Verwendung von Code First-Migrationen zum Aktualisieren der Datenbank ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

Das Datenbankmodell hat sich geändert, in einer Weise, die eine Änderung im Datenbankschema erfordert, und Entity Framework festgestellt, dass ein. Sie verwenden Migrationen, um das Schema aktualisieren, ohne dass Daten, die Sie in der Datenbank hinzugefügt, über die Benutzeroberfläche. Wenn Sie Daten geändert, die erstellt wurde die `Seed` Methode, die an den ursprünglichen Zustand aufgrund von geändert werden die [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) Methode, die Sie in verwenden der `Seed` Methode. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) entspricht einer "Upsert"-Operation von datenbankterminologie.)

Geben Sie die folgenden Befehle in die Paket-Manager-Konsole ein:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

Die `add-migration MaxLengthOnNames` Befehl erstellt eine Datei mit dem Namen  *&lt;Zeitstempel&gt;\_MaxLengthOnNames.cs*. Diese Datei enthält Code, der die Datenbank das aktuellen Datenmodell entsprechend aktualisiert wird. Der Zeitstempel mit dem Namen der Migrationsdatei vorangestellt wird von Entity Framework verwendet, um die Migrationen zu sortieren. Nachdem Sie mehrere Migrationen erstellt haben, wenn Sie die Datenbank löschen, oder wenn Sie das Projekt bereitstellen, mithilfe von Migrationen, werden alle Migrationen in der Reihenfolge angewendet, in denen sie erstellt wurden.

Führen Sie die **erstellen** Seite, und geben Sie entweder ein, die mehr als 50 Zeichen. Sobald Sie 50 Zeichen überschreiten, clientseitige Validierung sofort eine Fehlermeldung angezeigt.

![Client-side Val-Fehler](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Column-Attribut

Sie können ebenfalls Attribute verwenden, um zu steuern, wie Ihre Klassen und Eigenschaften der Datenbank zugeordnet werden. Angenommen, Sie haben den Namen `FirstMidName` für das Feld „first-name“ verwendet, da das Feld ebenfalls einen Zweitnamen enthalten kann. Sie möchten jedoch, dass die Datenbankspalte in `FirstName` umbenannt wird, damit Benutzer, die Ad-hob-Abfragen für die Datenbank schreiben, an diesen Namen gewöhnt sind. Sie können das `Column`-Attribut verwenden, um diese Zuordnung durchzuführen.

Das `Column`-Attribut gibt an, dass bei der Erstellung der Datenbank die Spalte des `Student`-Elements, die der `FirstMidName`-Eigenschaft zugeordnet ist, den Namen `FirstName` erhält. Wenn Ihr Code also auf `Student.FirstMidName` verweist, stammen die Daten aus der `FirstName`-Spalte der `Student`-Tabelle oder werden in dieser aktualisiert. Wenn Sie keine Spaltennamen angeben, wird ihnen den gleichen Namen wie die Namen der Eigenschaft zugewiesen.

Hinzufügen einer using-Anweisung für [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) und der Spalte Name-Attribut, um die `FirstMidName` -Eigenschaft, wie im folgenden hervorgehobenen Code gezeigt:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

Das Hinzufügen der [Spaltenattribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) ändert sich das Modell der SchoolContext sichern, damit er stimmt jedoch nicht die Datenbank überein. Geben Sie die folgenden Befehle in der PMC um eine weitere Migration zu erstellen:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

In **Server-Explorer** (**Datenbank-Explorer** Wenn Sie Express für Web verwenden), doppelklicken Sie auf die *für Schüler und Studenten* Tabelle.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

Die folgende Abbildung zeigt den ursprünglichen Spaltennamen an, wie es war, bevor Sie die ersten beiden Migrationen angewendet. Zusätzlich zu den Namen der Spalte ändern von `FirstMidName` zu `FirstName`, die zwei Namensspalten von geändert haben `MAX` auf 50 Zeichen.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Sie können auch Änderungen vornehmen, Datenbank Zuordnung mithilfe der [Fluent-API](https://msdn.microsoft.com/data/jj591617), wie Sie später in diesem Lernprogramm sehen werden.

> [!NOTE]
> Wenn Sie versuchen, die kompiliert werden, bevor Sie alle diese Entitätsklassen erstellt haben, erhalten Sie möglicherweise Compilerfehler angezeigt.

## <a name="create-the-instructor-entity"></a>Erstellen der Instructor-Entität

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Erstellen Sie *Models\Instructor.cs*, und Ersetzen Sie den Vorlagencode durch den folgenden Code:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Beachten Sie, dass einige Eigenschaften in den Entitäten `Student` und `Instructor` identisch sind. In der [Implementierung von Vererbung](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) Tutorial weiter unten in dieser Reihe werde gestalten Sie mithilfe von Vererbung zu diese Redundanz auszuschließen.

### <a name="the-required-and-display-attributes"></a>Die erforderlichen und Attribute anzeigen.

Die Attribute auf die `LastName` -Eigenschaft angeben, dass es ist ein erforderliches Feld, das, dass die Beschriftung für das Textfeld muss "Last Name" (statt dem Eigenschaftsnamen, die "LastName" ohne Leerzeichen) und der Wert nicht mehr als 50 Zeichen sein darf nicht.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

Die [StringLength-Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) legt die maximale Länge in der Datenbank und bietet clientseitige und serverseitige Validierung für ASP.NET MVC. Sie können ebenfalls die mindestens erforderliche Zeichenfolgenlänge in diesem Attribut angeben, dieser Wert hat jedoch keine Auswirkung auf das Datenbankschema. Die [erforderliche Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) ist nicht erforderlich für Werttypen wie "DateTime", Int, double, und "float". Werttypen können einen null-Wert zugewiesen werden, damit sie grundsätzlich erforderlich sind. Entfernen der [erforderliche Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) und Ersetzen Sie ihn mit einer Mindestlänge für Parameter für die `StringLength` Attribut:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

Deshalb können Sie auch die Klasse "Instructor" wie folgt schreiben können, können Sie mehrere Attribute in einer Zeile einfügen:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>Der FullName berechnete Eigenschaften

Bei `FullName` handelt es sich um eine berechnete Eigenschaft, die einen Wert zurückgibt, der durch das Verketten von zwei weiteren Eigenschaften erstellt wird. Aus diesem Grund ist es nur eine `get` Accessor, und keine `FullName` Spalte in der Datenbank generiert werden.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Die Kurse und die Navigationseigenschaften für die "OfficeAssignment"

Bei den Eigenschaften `Courses` und `OfficeAssignment` handelt es sich um Navigationseigenschaften. Wie bereits erwähnt wurde, werden sie in der Regel definiert als [virtuellen](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) , damit sie eine Entity Framework-Funktion wird aufgerufen, nutzen können [Lazy Load](https://msdn.microsoft.com/magazine/hh205756.aspx). Darüber hinaus, wenn eine Navigationseigenschaft mehrere Entitäten enthalten kann, der Typ muss implementieren die [ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx) Schnittstelle. (Z. B. [IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifiziert, aber nicht ["IEnumerable"&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) da `IEnumerable<T>` implementiert keine [hinzufügen ](https://msdn.microsoft.com/library/63ywd54z.aspx).

Ein Dozenten kann eine beliebige Anzahl von Kursen unterrichten, sodass `Courses` ist definiert als eine Auflistung von `Course` Entitäten. Unsere Geschäftsregeln Status ein Dozenten haben nur maximal ein Büro, also `OfficeAssignment` ist definiert als eine einzelne `OfficeAssignment` Entität (die möglicherweise `null` , wenn kein Büro zugewiesen ist).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>Erstellen der Entität "OfficeAssignment"

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Erstellen Sie *Models\OfficeAssignment.cs* durch den folgenden Code:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Erstellen Sie des Projekts, das speichert die Änderungen und stellt sicher, dass Sie Kopie erstellt noch nicht aus, und fügen Sie die Fehler, die der Compiler abfangen kann.

### <a name="the-key-attribute"></a>Das wichtigste Attribut

Es gibt eine 1: 0 (null)-oder-1-Beziehung zwischen der `Instructor` und `OfficeAssignment` Entitäten. Eine bürozuweisung ist nur vorhanden, im Verhältnis zu dem Dozenten zugewiesen wird, und daher ist deren Primärschlüssel auch der Fremdschlüssel für die `Instructor` Entität. Entity Framework nicht automatisch erkannt, aber `InstructorID` wie die primäre Datenbank wichtige dieser Entität, da der Name nicht folgt die `ID` oder *Classname* `ID` Benennungskonvention. Deshalb wird das `Key`-Attribut verwendet, um „InstructorID“ als Schlüssel zu erkennen:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Sie können auch die `Key` Attribut, wenn die Entität ihren eigenen Primärschlüssel besitzt, aber der Eigenschaftenname etwas anderes als möchten `classnameID` oder `ID`. Standardmäßig behandelt Entity Framework den Schlüssel als nicht-datenbankgeneriert, da die Spalte für eine identifizierende Beziehung vorgesehen ist.

### <a name="the-foreignkey-attribute"></a>Das Attribut ForeignKey

Wenn eine 1: 0 (null)-oder-1-Beziehung oder eine direkte Beziehung zwischen zwei Entitäten vorhanden ist (solche zwischen `OfficeAssignment` und `Instructor`), EF nicht funktioniert, welche Seite der Beziehung der Prinzipal ist und welche End abhängig ist. 1: 1-Beziehungen haben eine verweisnavigationseigenschaft in jeder Klasse, die andere Klasse. Die [ForeignKey Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) kann angewendet werden, um die abhängigen-Klasse, die Beziehung herzustellen. Wenn Sie weglassen der [ForeignKey Attribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), erhalten Sie die folgende Fehlermeldung, wenn Sie versuchen, die Migration zu erstellen:

Kann nicht das prinzipalende einer Zuordnung zwischen den Typen 'ContosoUniversity.Models.OfficeAssignment' und "ContosoUniversity.Models.Instructor" bestimmt. Das prinzipalende der Zuordnung muss explizit mithilfe der Beziehung fluent-API oder datenanmerkungen konfiguriert werden.

Später in diesem Tutorial zeigen wir, wie Sie diese Beziehung mit der fluent-API zu konfigurieren.

### <a name="the-instructor-navigation-property"></a>Die Navigationseigenschaft "Instructor"

Die `Instructor` Entität verfügt über eine auf NULL festlegbare `OfficeAssignment` Navigationseigenschaft (da ein Dozenten möglicherweise keine bürozuweisung verfügen), und die `OfficeAssignment` Entität hat einen NULL- `Instructor` Navigationseigenschaft (da eine bürozuweisung nicht möglich vorhanden sein, ohne einen Dozenten-- `InstructorID` nicht-NULL-Werte zulässt). Wenn ein `Instructor` Entität verfügt über einen zugehörigen `OfficeAssignment` Entität, jede Entität weist einen Verweis auf die andere in den Navigationseigenschaften.

Sie platzieren konnte eine `[Required]` Attribut für die Navigationseigenschaft "Instructor", um anzugeben, dass ein zugehöriger Dozent vorhanden sein muss, aber Sie müssen dies tun, da der Fremdschlüssel InstructorID (entspricht auch der Schlüssel für diese Tabelle) nicht auf NULL festlegbare ist.

## <a name="modify-the-course-entity"></a>Ändern der Entität „Course“

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

In *Models\Course.cs*, ersetzen Sie den Code, die Sie hinzugefügt haben weiter oben durch den folgenden Code:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Die Entität "Course" verfügt über eine Fremdschlüsseleigenschaft `DepartmentID` der verweist auf die verknüpfte `Department` Entität verfügt über eine `Department` Navigationseigenschaft. Entity Framework erfordert nicht, dass Sie eine Fremdschlüsseleigenschaft zu Ihrem Datenmodell hinzufügen, wenn eine Navigationseigenschaft für eine verknüpfte Entität vorhanden ist. EF erstellt automatisch Fremdschlüssel in der Datenbank, wo sie benötigt werden. Durch Fremdschlüssel im Datenmodell können Updates einfacher und effizienter durchgeführt werden. Z. B. Wenn Sie "abrufen" Entität "Course" zu bearbeiten, die `Department` -Entität ist null, wenn Sie es nicht geladen werden, also beim Aktualisieren der Entität "Course", Sie müssten zuerst abgerufen werden. die `Department` Entität. Wenn die Fremdschlüsseleigenschaft `DepartmentID` enthalten ist in das Datenmodell, müssen Sie nicht Abrufen der `Department` Entität, die vor dem aktualisieren.

### <a name="the-databasegenerated-attribute"></a>Das Attribut "databasegenerated"

Die [Attribut "databasegenerated"](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) mit der [keine](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) Parameter in der `CourseID` Eigenschaft gibt an, dass die Primärschlüssel-Werte werden vom Benutzer bereitgestellte, sondern von der Datenbank generiert.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

Standardmäßig wird in Entity Framework davon ausgegangen, dass Primärschlüsselwerte von der Datenbank generiert werden. Das ist in den meisten Fällen erwünscht. Beachten Sie jedoch bei `Course` Entitäten, die Sie verwenden eine benutzerdefinierte Kursnummer wie eine 1000er-Reihe für eine Abteilung, eine 2000er-Reihe für eine andere und so weiter.

### <a name="foreign-key-and-navigation-properties"></a>Foreign Key- und Navigationseigenschaften

Die Fremdschlüssel- und Navigationseigenschaften in der `Course` Entität stellen folgende Beziehungen dar:

- Ein Kurs ist einer Abteilung zugeordnet, sodass es aus den oben genannten Gründen eine `DepartmentID`-Fremdschlüsseleigenschaft und eine `Department`-Navigationseigenschaft gibt. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- In einem Kurs können beliebig viele Studenten angemeldet sein, darum stellt die `Enrollments`-Navigationseigenschaft eine Auflistung dar: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Ein Kurs kann von mehreren Dozenten unterrichtet werden, darum stellt die `Instructors`-Navigationseigenschaft eine Auflistung dar: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Erstellen der Entität "Department"

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Erstellen Sie *Models\Department.cs* durch den folgenden Code:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column-Attribut

Sie zuvor verwendet haben die [Spaltenattribut](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) Zuordnung des Spaltennamens zu ändern. Im Code für die `Department` Entität, die `Column` Attribut wird verwendet, um das Ändern der SQL-datentypzuordnung so, dass die Spalte definiert wird mithilfe der SQL Server [Geld](https://msdn.microsoft.com/library/ms179882.aspx) Typ in der Datenbank:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Spaltenzuordnung ist im Allgemeinen nicht erforderlich, da das Entity Framework wählt in der Regel die entsprechenden SQL Server-Datentyp, der basierend auf dem CLR-Typ, den Sie für die Eigenschaft zu definieren. Der CLR-Typ `decimal` wird dem SQL Server-Typ `decimal` zugeordnet. Aber in diesem Fall wissen Sie, dass die Spalte Währungsbeträge, enthalten sein wird und die [Geld](https://msdn.microsoft.com/library/ms179882.aspx) Datentyp besser geeignet ist.

### <a name="foreign-key-and-navigation-properties"></a>Foreign Key- und Navigationseigenschaften

Die Fremdschlüssel- und Navigationseigenschaften stellen folgende Beziehungen dar:

- Eine Abteilung kann einen Administrator besitzen oder nicht, und bei einem Administrator handelt es sich immer um einen Dozenten. Aus diesem Grund die `InstructorID` Eigenschaft ist als der Fremdschlüssel für die `Instructor` Entität und ein Fragezeichen wird nach hinzugefügt. die `int` typbezeichnung, um die Eigenschaft als auf NULL festlegbar zu markieren. Die Navigationseigenschaft heißt `Administrator` , enthält jedoch eine `Instructor` Entität: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Eine Abteilung kann viele Kurse aufweisen, gibt es also eine `Courses` Navigationseigenschaft: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Gemäß der Konvention aktiviert Entity Framework das kaskadierende Delete für nicht auf NULL festlegbare Fremdschlüssel und für m:n-Beziehungen. Dies kann zu zirkelregeln für kaskadierende DELETES, führen, die eine Ausnahme ausgelöst wird, wenn der initialisierercode ausgeführt wird. Wenn Sie nicht definieren, z. B. die `Department.InstructorID` Eigenschaft als NULL-Werte zulässt, würde Sie die folgenden Ausnahmemeldung erhalten, wenn der Initialisierer ausgeführt wird: "Referenzielle Beziehung führt zu einer zyklischen Verweis, der nicht zulässig ist." Wenn Ihre Geschäftsregeln erfordern `InstructorID` Eigenschaft als NULL-Werte zulässt, müssen Sie die folgende fluent-API verwenden, um kaskadierende DELETES für die Beziehung zu deaktivieren: 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>Ändern die Entität "Student"

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

In *Models\Student.cs*, ersetzen Sie den Code, die Sie hinzugefügt haben weiter oben durch den folgenden Code. Die Änderungen werden hervorgehoben.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>Die Entität "Enrollment"

 In *Models\Enrollment.cs*, ersetzen Sie den Code, die Sie hinzugefügt haben weiter oben durch den folgenden Code

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>Foreign Key- und Navigationseigenschaften

Die Fremdschlüssel- und Navigationseigenschaften stellen folgende Beziehungen dar:

- Ein Anmeldungsdatensatz gilt für einen einzelnen Kurs, sodass es eine `CourseID`-Fremdschlüsseleigenschaft und eine `Course`-Navigationseigenschaft gibt: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- Ein Anmeldungsdatensatz gilt für einen einzelnen Studenten, sodass es eine `StudentID`-Fremdschlüsseleigenschaft und eine `Student`-Navigationseigenschaft gibt: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>n:n-Beziehungen

Besteht eine m: n Beziehung zwischen der `Student` und `Course` Entitäten, und die `Enrollment` -Entität fungiert als m: n Jointabelle *mit Nutzlast* in der Datenbank. Dies bedeutet, dass die `Enrollment` Tabelle enthält zusätzliche Daten außer den Fremdschlüsseln für die verknüpften Tabellen (in diesem Fall ein Primärschlüssel und einem `Grade` Eigenschaft).

Die folgende Abbildung stellt dar, wie diese Beziehungen in einem Entitätsdiagramm aussehen. (Dieses Diagramm wurde mithilfe von generiert die [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d), erstellen das Diagramm ist nicht Teil des Tutorials wird nur verwendet wird hier als anschauliches Beispiel.)

!["Student" Course_many zu many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

Jede Beziehung weist eine 1 an einem Ende und ein Sternchen (\*), der am anderen, die angibt, einer 1: n Beziehung.

Wenn die `Enrollment` Tabelle nicht auf Unternehmensniveau Informationen enthalten, müssen sie nur die beiden Fremdschlüssel enthalten `CourseID` und `StudentID`. In diesem Fall würde es entsprechen einer m: n Jointabelle *ohne Nutzlast* (oder ein *reine Jointabelle*) in der Datenbank, und Sie hätten eine Modellklasse überhaupt zu erstellen. Die `Instructor` und `Course` Entitäten verfügen über diese Art von m: n Beziehung, und wie Sie sehen können, es ist keine Entitätsklasse zwischen ihnen:

!["Instructor" Course_many zu many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Eine Jointabelle ist jedoch in der Datenbank erforderlich, wie im folgenden Diagramm dargestellt:

!["Instructor" Course_many zu many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Das Entity Framework erstellt automatisch die `CourseInstructor` Tabelle, und Sie lesen und aktualisieren sie indirekt durch Lesen und Aktualisieren der `Instructor.Courses` und `Course.Instructors` Navigationseigenschaften.

## <a name="entity-diagram-showing-relationships"></a>Entitätsdiagramm mit angezeigten Beziehungen

Die folgende Abbildung stellt das Diagramm dar, das von Entity Framework Power Tools für das vollständige Modell „School“ erstellt wird.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Neben den Zeilen der m: n Beziehung (\* zu \*) und die Beziehungslinien für 1: n (1 bis \*), sehen Sie die Zeile 1-0 (null)-oder-1-Beziehung (1 zu 0.. 1) zwischen den `Instructor` und `OfficeAssignment` Entitäten und 0 (null)-oder-1-n-Beziehung (0.. 1: \*) zwischen den Entitäten "Instructor" und Abteilung.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>Anpassen des Datenmodells durch Hinzufügen von Code zum Kontext Datenbank

Als Nächstes fügen Sie die neuen Entitäten, die die `SchoolContext` Klasse, und passen Sie die Zuordnung mithilfe einiger [fluent-API](https://msdn.microsoft.com/data/jj591617) aufrufen. (Die API ist "fluent", da sie häufig durch Verketten mehrerer Methodenaufrufe zu einer einzigen Anweisung verwendet wird.)

In diesem Tutorial verwenden Sie die fluent-API nur für datenbankzuordnungen, die mit Attributen nicht möglich. Sie können die Fluent-API jedoch ebenfalls verwenden, um den Großteil der Regeln für die Formatierung, Validierung und Zuordnung anzugeben, die Sie mithilfe von Attributen festlegen können. Manche Attribute, z.B. `MinimumLength`, können nicht mit der Fluent-API angewendet werden. Wie bereits erwähnt, `MinimumLength` ändert nicht das Schema gilt nur für eine Client- und serverseitige Validierungsregel

Einige Entwickler bevorzugen die exklusive Verwendung der Fluent-API, um ihre Entitätsklassen „rein“ zu halten. Sie können Attribute und die Fluent-API verwenden, wenn Sie möchten. Einige Anpassungen können nur mithilfe der Fluent-API vorgenommen werden. Im Allgemeinen wird jedoch empfohlen, einen der beiden Ansätze auszuwählen und diesen so konsistent wie möglich zu verwenden.

Zum Hinzufügen, die neuen Entitäten auf die Daten modellieren, und führen Sie eine datenbankzuordnung, die Sie nicht mithilfe von Attributen, ersetzen Sie den Code in *DAL\SchoolContext.cs* durch den folgenden Code:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

Die neue Anweisung in der ["onmodelcreating"](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) Methode konfiguriert der m: n Jointabelle:

- Für die m: n Beziehung zwischen der `Instructor` und `Course` Entitäten, die der Code gibt an, die Tabellen- und Spaltennamen für die Jointabelle. Code zuerst kann die m: n Beziehung für Sie konfigurieren ohne diesen Code, aber wenn Sie ihn nicht aufrufen, erhalten Sie Standardnamen wie z. B. `InstructorInstructorID` für die `InstructorID` Spalte.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

Der folgende Code bietet ein Beispiel, wie Sie fluent-API anstelle von Attributen verwendet haben können, geben Sie die Beziehung zwischen der `Instructor` und `OfficeAssignment` Entitäten:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Weitere Informationen dazu, was hinter den Kulissen "fluent-API"-Anweisungen ausführen, finden Sie unter den [Fluent-API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) Blogbeitrag.

## <a name="seed-the-database-with-test-data"></a>Ausführen eines Seedings für die Datenbank mit Testdaten

Ersetzen Sie den Code in die *migrations\configuration. cs* -Datei mit den folgenden Code, um startwertdaten für neuen Entitäten zu gewährleisten, Sie erstellt haben.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

Im ersten Tutorial haben Sie gesehen, die meisten dieser Code einfach aktualisiert oder neue Entitätsobjekte erstellt und lädt Beispieldaten in Eigenschaften nach Bedarf für das Testen. Beachten Sie jedoch wie die `Course` -Entität, die eine m: n Beziehung umfasst, mit der `Instructor` Entität behandelt wird:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

Bei der Erstellung einer `Course` Objekt, initialisieren Sie die `Instructors` Navigationseigenschaft als eine leere Auflistung, die mit dem Code `Instructors = new List<Instructor>()`. Dadurch wird es möglich, `Instructor` Entitäten, die auf diese beziehen `Course` mithilfe der `Instructors.Add` Methode. Wenn Sie eine leere Liste erstellt haben, Sie wäre nicht hinzufügen, diese Beziehungen, da die `Instructors` Eigenschaft würde nicht null und nicht ausreichen würde eine `Add` Methode. Sie können auch die List-Initialisierung an den Konstruktor hinzufügen.

## <a name="add-a-migration-and-update-the-database"></a>Eine Migration hinzufügen und Aktualisieren der Datenbank

Geben Sie in der PMC die `add-migration` Befehl:

`PM> add-Migration Chap4`

Wenn Sie versuchen, die Datenbank an diesem Punkt zu aktualisieren, erhalten Sie den folgenden Fehler:

*Die ALTER TABLE-Anweisung steht in Konflikt mit der FOREIGN KEY-Einschränkung "FK\_Dbo. Kurs\_Dbo. Abteilung\_"DepartmentID" ". Der Konflikt trat in der Datenbank "ContosoUniversity", Tabelle "Dbo. Abteilung", Spalte"DepartmentID".*

Bearbeiten der &lt; *Zeitstempel&gt;\_Chap4.cs* Datei, und stellen Sie die folgenden codeänderungen (Sie eine SQL-Anweisung hinzufügen und Ändern einer `AddColumn` Anweisung):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(Stellen Sie sicher, dass Sie auskommentieren oder löschen Sie die vorhandenen `AddColumn` Zeile, wenn Sie den neuen Wert hinzufügen, oder Sie einen Fehler erhalten bei der Eingabe der `update-database` Befehl.)

Manchmal, wenn Sie Migrationen mit vorhandenen Daten ausführen, müssen Sie zum Einfügen von Stub-Daten in der Datenbank, foreign Key-Einschränkungen erfüllen, und das ist was Sie jetzt tun. Der generierte Code Fügt einen NULL- `DepartmentID` Fremdschlüssel für die `Course` Tabelle. Wenn es bereits Zeilen in der `Course` Tabelle, wenn der Code ausgeführt wird, die `AddColumn` Operation würde fehlschlagen, weil SQL Server nicht bekannt, welcher Wert um in der Spalte zu platzieren, die nicht null sein darf. Sie haben den Code, um der neuen Spalte einen Standardwert zuweist. aus diesem Grund geändert, und Sie erstellt haben, eine Abteilung "Lohnbuchhaltung" namens "Temp", die als standardfachbereich fungiert. Als Ergebnis, wenn bereits vorhanden sind `Course` Zeilen, wenn dieser Code ausgeführt, sie werden alle werden im Zusammenhang mit der Abteilung "Temp".

Wenn die `Seed` Methode ausgeführt wird, es fügt Zeilen in der `Department` Tabelle, und es werden vorhandene beziehen `Course` Zeilen in diese neue `Department` Zeilen. Wenn Sie Kurse in der Benutzeroberfläche hinzugefügt haben, klicken Sie dann nicht mehr benötigen Sie die Abteilung "Temp" oder den Standardwert für die `Course.DepartmentID` Spalte. Damit wird die Möglichkeit, dass eine Person Kurse hinzugefügt haben, mit der Anwendung, Sie würden auch aktualisieren möchten die `Seed` Methodencode, um sicherzustellen, dass alle `Course` Zeilen (nicht nur diejenigen, die von früheren Ausführungen eingefügt wurden die `Seed` Methode) haben gültige `DepartmentID` Werte vor dem Entfernen der Standardwert aus der Spalte Wert, und löschen Sie die Abteilung "Temp".

Nach dem Bearbeiten der &lt; *Zeitstempel&gt;\_Chap4.cs* Datei, geben Sie die `update-database` Befehl in der PMC die Migration ausgeführt.

> [!NOTE]
> Es ist möglich, dass andere Fehler auftreten, bei der Migration von Daten und zu Änderungen am Datenbankschema. Wenn Sie Migrationsfehler Sie nicht lösen erhalten, können Sie entweder die Verbindungszeichenfolge zumeist im Ändern der *"Web.config"* Datei oder die Datenbank löschen. Der einfachste Ansatz ist zum Umbenennen der Datenbank in *"Web.config"* Datei. Ändern Sie z. B. der Name der Datenbank in CU\_testen, wie im folgenden gezeigt:
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> Mit einer neuen Datenbank, sind keine Daten zu migrieren, und die `update-database` Befehl ist sehr wahrscheinlich ohne Fehler abgeschlossen. Anweisungen dazu, wie Sie die Datenbank zu löschen, finden Sie unter [Gewusst wie: Löschen einer Datenbank in Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).

Öffnen Sie die Datenbank in **Server-Explorer** wie zuvor, und erweitern Sie die **Tabellen** Knoten aus, um zu sehen, dass alle Tabellen erstellt wurden. (Falls noch **Server-Explorer** immer zu öffnen, klicken Sie auf die **aktualisieren** Schaltfläche.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Erstellen Sie keine Modellklasse für den `CourseInstructor` Tabelle. Wie bereits erwähnt, ist dies eine Jointabelle für die m: n Beziehung zwischen der `Instructor` und `Course` Entitäten.

Mit der rechten Maustaste die `CourseInstructor` Tabelle, und wählen Sie **Tabellendaten anzeigen** um sicherzustellen, dass sie Daten als Ergebnis des enthält die `Instructor` Entitäten, die Sie hinzugefügt, um haben die `Course.Instructors` Navigationseigenschaft.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>Zusammenfassung

Sie besitzen nun ein komplexeres Datenmodell und eine zugehörige Datenbank. Im folgenden Tutorial erfahren Sie mehr über verschiedene Möglichkeiten zum Zugriff auf verwandte Daten.

Links zu anderen Ressourcen des Entity Framework finden Sie in der [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Zurück](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Weiter](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
