---
title: 'Razor-Seiten mit EF Core in ASP.NET Core: CRUD (2 von 8)'
author: rick-anderson
description: In diesem Tutorial wird veranschaulicht, wie mit EF Core Erstellungs-, Lese-, Aktualisierungs- und Löschvorgänge durchgeführt werden
ms.author: riande
ms.date: 6/31/2017
uid: data/ef-rp/crud
ms.openlocfilehash: 4af16bdf3928609214c1255cdd411312c8b7d3f3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040107"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---crud---2-of-8"></a>Razor-Seiten mit EF Core in ASP.NET Core: CRUD (2 von 8)

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

Von [Tom Dykstra](https://github.com/tdykstra), [Jon P. Smith](https://twitter.com/thereformedprog) und [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [about the series](~/includes/RP-EF/intro.md)]

In diesem Tutorial wird der erstellte CRUD-Code (CRUD = Create, Read, Update, Delete; Erstellen, Lesen, Aktualisieren, Löschen) überprüft und angepasst.

Zur Minimierung der Komplexität und damit EF Core im Fokus dieser Tutorials bleibt, wird in den Seitenmodellen EF Core-Code verwendet. Einige Entwickler verwenden eine Dienstschicht oder ein Repositorymuster für die Erstellung einer Abstraktionsschicht zwischen der Benutzeroberfläche (Razor Pages) und der Datenzugriffsschicht.

In diesem Tutorial werden die Razor Pages „Create“ (Erstellen), „Edit“ (Bearbeiten), „Delete“ (Löschen) und „Details“ im Ordner *Students* erläutert.

Der erstellte Code verwendet folgendes Muster für die Seiten „Create“ (Erstellen), „Edit“ (Bearbeiten) und „Delete“ (Löschen):

* Abrufen und Anzeigen der angeforderten Daten mit der HTTP GET-Methode `OnGetAsync`.
* Speichern der an Daten vorgenommenen Änderungen mit der HTTP POST-Methode `OnPostAsync`.

Auf den Seiten „Index“ und „Details“ werden die angeforderten Daten mit der HTTP GET-Methode `OnGetAsync` abgerufen und angezeigt.

## <a name="singleordefaultasync-vs-firstordefaultasync"></a>„SingleOrDefaultAsync“ im Vergleich zu „FirstOrDefaultAsync“

Der generierte Code verwendet [FirstOrDefaultAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstordefaultasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstOrDefaultAsync__1_System_Linq_IQueryable___0__System_Threading_CancellationToken_). Im Allgemeinen wird dies [SingleOrDefaultAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleordefaultasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleOrDefaultAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) vorgezogen.

 `FirstOrDefaultAsync` ist beim Abrufen einer Entität effizienter als `SingleOrDefaultAsync`:

* Sofern mit dem Code nicht überprüft werden muss, ob von der Abfrage mehrere Entitäten zurückgegeben wurden.
* `SingleOrDefaultAsync` ruft weitere Daten ab und führt unnötige Arbeiten aus.
* `SingleOrDefaultAsync` löst eine Ausnahme aus, wenn mehrere Entitäten in den Filterabschnitt passen.
* `FirstOrDefaultAsync` löst keine Ausnahme aus, wenn mehrere Entitäten in den Filterabschnitt passen.

<a name="FindAsync"></a>

### <a name="findasync"></a>FindAsync

In einem Großteil des Codes kann [FindAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.findasync#Microsoft_EntityFrameworkCore_DbContext_FindAsync_System_Type_System_Object___) anstelle von `FirstOrDefaultAsync` verwendet werden.

`FindAsync`:

* Sucht eine Entität mit dem Primärschlüssel (PS). Wenn eine Entität mit dem PS vom Kontext nachverfolgt wird, wird sie ohne eine Anforderung an die Datenbank zurückgegeben.
* Ist einfach und präzise.
* Wurde für die Suche nach einer einzelnen Entität optimiert.
* Kann manchmal Leistungsvorteile haben, für normale Web-Apps ist dies jedoch selten der Fall.
* Verwendet implizit [FirstAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) anstelle von [SingleAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_).

Wenn Sie jedoch weitere Entitäten mithilfe von `Include` einschließen möchten, ist `FindAsync` jedoch nicht mehr sinnvoll. Dies bedeutet, dass Sie `FindAsync` möglicherweise abbrechen und in eine Abfrage verschieben müssen, während Ihre App weiter ausgeführt wird.

## <a name="customize-the-details-page"></a>Anpassen der Seite „Details“

Navigieren Sie zur Seite `Pages/Students`. Die Links **Bearbeiten**, **Details** und **Löschen** werden mithilfe des [Anchor-Taghilfsprogramms](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) in der Datei *Pages/Movies/Index.cshtml* generiert.

[!code-cshtml[](intro/samples/cu21/Pages/Students/Index1.cshtml?name=snippet)]

Führen Sie die App aus, und klicken Sie auf den Link **Details**. Die URL weist das Format `http://localhost:5000/Students/Details?id=2` auf. Die Studenten-ID wird mit einer Abfragezeichenfolge (`?id=2`) übergeben.

Aktualisieren Sie die Razor Pages „Edit“ (Bearbeiten), „Details“ und „Delete“ (Löschen) so, dass die Routenvorlage `"{id:int}"` verwendet wird. Ändern Sie die „page“-Direktive für jede dieser Seiten aus `@page` in `@page "{id:int}"`.

Eine Anforderung an die Seite mit der Routenvorlage „{id:int}“, die **nicht** den Integer enthält, gibt den HTTP-Fehler „404 – Nicht gefunden“ zurück. `http://localhost:5000/Students/Details` gibt beispielsweise den Fehler 404 zurück. Um die ID optional zu machen, fügen Sie `?` an die Routeneinschränkung an:

 ```cshtml
@page "{id:int?}"
```

Führen Sie die App aus, klicken Sie auf einen Details-Link, und überprüfen Sie, ob die ID in der URL in Form von Routendaten übergeben wird (`http://localhost:5000/Students/Details/2`).

Ändern Sie `@page` nicht global in `@page "{id:int}"`. Dadurch werden die Links zu den Seiten „Home“ und „Create“ (Erstellen) getrennt.

<!-- See https://github.com/aspnet/Scaffolding/issues/590 -->

### <a name="add-related-data"></a>Hinzufügen relevanter Daten

Der für die Indexseite „Students“ erstellte Code umfasst nicht die Eigenschaft `Enrollments`. In diesem Abschnitt werden die Inhalte der `Enrollments`-Auflistung auf der Seite „Details“ angezeigt.

Die Methode `OnGetAsync` der Datei *Pages/Students/Details.cshtml.cs* verwendet die Methode `FirstOrDefaultAsync` zum Abrufen einer einzelnen `Student`-Entität. Fügen Sie folgenden hervorgehobenen Code hinzu:

[!code-csharp[](intro/samples/cu21/Pages/Students/Details.cshtml.cs?name=snippet_Details&highlight=8-12)]

Aufgrund der Methoden [Include](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.include) und [ThenInclude](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.theninclude#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_ThenInclude__3_Microsoft_EntityFrameworkCore_Query_IIncludableQueryable___0_System_Collections_Generic_IEnumerable___1___System_Linq_Expressions_Expression_System_Func___1___2___) lädt der Kontext die Navigationseigenschaft `Student.Enrollments` und in jeder Registrierung die Navigationseigenschaft `Enrollment.Course`. Diese Methoden werden im lesebezogenen Datentutorial ausführlich überprüft.

Die Methode [AsNoTracking](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) verbessert die Leistung in Szenarios, wenn die zurückgegebenen Entitäten nicht im aktuellen Kontext aktualisiert werden. `AsNoTracking` wird später in diesem Tutorial behandelt.

### <a name="display-related-enrollments-on-the-details-page"></a>Anzeigen verknüpfter Registrierungen auf der Seite „Details“

Öffnen Sie die Datei *Pages/Students/Details.cshtml*. Fügen Sie folgenden hervorgehobenen Code hinzu, um eine Liste mit Registrierungen anzuzeigen:

[!code-cshtml[](intro/samples/cu21/Pages/Students/Details.cshtml?highlight=32-53)]

Wenn der Codeeinzug nach dem Einfügen des Codes falsch ist, drücken Sie Strg+K+D, um diesen zu korrigieren.

Der vorangehende Code durchläuft die Entitäten in der Navigationseigenschaft `Enrollments`. Für jede Registrierung werden der Kurstitel und die Klasse angezeigt. Der Kurstitel wird von der Entität „Course“ abgerufen, die in der Navigationseigenschaft `Course` der Entität „Enrollments“ gespeichert ist.

Führen Sie die App aus, wählen Sie die Registerkarte **Studenten** aus, und klicken Sie bei einem Studenten auf den Link **Details**. Die Liste der Kurse und Klassen für den ausgewählten Studenten wird angezeigt.

## <a name="update-the-create-page"></a>Aktualisieren der Seite „Erstellen“

Aktualisieren Sie die Methode `OnPostAsync` in der Datei *Pages/Students/Create.cshtml.cs* mit dem folgenden Code:

[!code-csharp[](intro/samples/cu21/Pages/Students/Create.cshtml.cs?name=snippet_OnPostAsync)]

<a name="TryUpdateModelAsync"></a>

### <a name="tryupdatemodelasync"></a>TryUpdateModelAsync

Überprüfen Sie den [TryUpdateModelAsync](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryupdatemodelasync#Microsoft_AspNetCore_Mvc_ControllerBase_TryUpdateModelAsync_System_Object_System_Type_System_String_)-Code:

[!code-csharp[](intro/samples/cu21/Pages/Students/Create.cshtml.cs?name=snippet_TryUpdateModelAsync)]

Im vorangehenden Code versucht `TryUpdateModelAsync<Student>`, das Objekt `emptyStudent` mithilfe der bereitgestellten Formularwerte aus der Eigenschaft [PageContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.pagecontext#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_PageContext) im [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) zu aktualisieren. `TryUpdateModelAsync` aktualisiert nur die aufgeführten Eigenschaften (`s => s.FirstMidName, s => s.LastName, s => s.EnrollmentDate`).

Im vorgehenden Beispiel:

* Ist das zweite Argument (`"student", // Prefix`) das Präfix, das für die Suche nach Werten verwendet wird. Die Groß-/Kleinschreibung wird hier nicht beachtet.
* Werden die bereitgestellten Formularwerte mithilfe der [Modellbindung](xref:mvc/models/model-binding#how-model-binding-works) in die Typen im `Student`-Modell konvertiert.

<a id="overpost"></a>

### <a name="overposting"></a>Overposting

Die Verwendung von `TryUpdateModel` zur Aktualisierung von Feldern mit bereitgestellten Werten ist eine bewährte Sicherheitsmethode, da Overposting verhindert wird. Angenommen, die Student-Entität enthält die Eigenschaft `Secret`, die auf dieser Webseite nicht aktualisiert oder hinzugefügt werden sollte:

[!code-csharp[](intro/samples/cu21/Models/StudentZsecret.cs?name=snippet_Intro&highlight=7)]

Selbst wenn die App auf der Razor Page „Create/Update“ (Erstellen/Aktualisieren) nicht über ein Feld vom Typ `Secret` verfügt, könnte ein Hacker den `Secret`-Wert durch Overposting festlegen. Ein Hacker könnte ein Tool wie Fiddler verwenden oder JavaScript-Code schreiben, um einen `Secret`-Formularwert bereitzustellen. Die Felder, die von der Modellbindung bei der Erstellung einer Student-Instanz verwendet werden, werden nicht durch den ursprünglichen Code begrenzt.

Jeder beliebige, vom Hacker in den `Secret`-Formularfeldern angegebene Wert wird in der Datenbank aktualisiert. Die folgende Abbildung zeigt das Fiddler-Tool beim Hinzufügen des Felds `Secret` (mit dem Wert „OverPost“) zu den bereitgestellten Formularwerten.

![Fiddler beim Hinzufügen des Felds „Secret“](../ef-mvc/crud/_static/fiddler.png)

Der Wert „OverPost“ wurde erfolgreich zur Eigenschaft `Secret` der eingefügten Zeile hinzugefügt. Der App-Designer hatte nie die Absicht, die Eigenschaft `Secret` auf der Seite „Erstellen“ festzulegen.

<a name="vm"></a>

### <a name="view-model"></a>ViewModel-Element

Ein Ansichtsmodell enthält in der Regel eine Teilmenge der im Modell enthaltenen Eigenschaften, die von der App verwendet werden. Das Anwendungsmodell wird häufig als Domänenmodell bezeichnet. Das Domänenmodell enthält normalerweise alle Eigenschaften, die die entsprechende Entität in der Datenbank erfordert. Das Ansichtsmodell enthält nur die Eigenschaften, die für die Benutzeroberflächenebene (z.B. die Seite „Erstellen“) erforderlich sind. Neben dem Ansichtsmodell verwenden einige Apps ein Bindungsmodell oder Eingabemodell für die Bereitstellung von Daten zwischen der Seitenmodellklasse auf den Razor Pages und dem Browser. Betrachten Sie das folgende `Student`-Ansichtsmodell:

[!code-csharp[](intro/samples/cu21/Models/StudentVM.cs)]

Ansichtsmodelle bieten eine alternative Möglichkeit zum Verhindern von Overposting. Das Ansichtsmodell enthält nur die Eigenschaften, die angezeigt oder aktualisiert werden sollen.

Im folgenden Code wird das `StudentVM`-Ansichtsmodell für die Erstellung eines neuen Studenten verwendet:

[!code-csharp[](intro/samples/cu21/Pages/Students/CreateVM.cshtml.cs?name=snippet_OnPostAsync)]

Die Methode [SetValues](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues.setvalues#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyValues_SetValues_System_Object_) legt die Werte dieses Objekts fest, indem sie Werte aus einem anderen [PropertyValues](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues)-Objekt liest. `SetValues` verwendet die Übereinstimmung von Eigenschaftsnamen. Der Ansichtsmodelltyp muss nicht mit dem Modelltyp verknüpft sein. Er muss lediglich über übereinstimmende Eigenschaften verfügen.

Für die Verwendung von `StudentVM` muss [CreateVM.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu21/Pages/Students/CreateVM.cshtml) aktualisiert werden, damit `StudentVM` statt `Student` verwendet wird.

Auf Razor Pages stellt die abgeleitete `PageModel`-Klasse das Ansichtsmodell dar.

## <a name="update-the-edit-page"></a>Aktualisieren der Seite „Bearbeiten“

Aktualisieren Sie das Seitenmodell für die Seite „Bearbeiten“: Die wichtigsten Änderungen werden hervorgehoben.

[!code-csharp[](intro/samples/cu21/Pages/Students/Edit.cshtml.cs?name=snippet_OnPostAsync&highlight=20,36)]

Die Codeänderungen sind bis auf wenige Ausnahmen mit denen auf der Seite „Erstellen“ vergleichbar:

* `OnPostAsync` weist den optionalen Parameter `id` auf.
* Anstatt einen leeren Studenten zu erstellen, wird der aktuelle Student aus der Datenbank abgerufen.
* `FirstOrDefaultAsync` wurde durch [FindAsync](/dotnet/api/microsoft.entityframeworkcore.dbset-1.findasync) ersetzt. `FindAsync` eignet sich für die Auswahl einer Entität über den Primärschlüssel. Weitere Informationen hierzu finden Sie unter [FindAsync](#FindAsync).

### <a name="test-the-edit-and-create-pages"></a>Testen der Seiten „Bearbeiten“ und „Erstellen“

Erstellen und bearbeiten Sie einige Student-Entitäten.

## <a name="entity-states"></a>Entitätsstatus

Im Datenbankkontext wird nachverfolgt, ob Entitäten im Arbeitsspeicher mit den zugehörigen Zeilen in der Datenbank synchron sind. Die Informationen zur Datenbanksynchronisierung bestimmen, was geschieht, wenn [SaveChangesAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) aufgerufen wird. Wenn beispielsweise eine neue Entität an die Methode [AddAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.addasync) übergeben wird, wird der Zustand dieser Entität auf [Added](/dotnet/api/microsoft.entityframeworkcore.entitystate#Microsoft_EntityFrameworkCore_EntityState_Added) festgelegt. Wenn `SaveChangesAsync` aufgerufen wird, gibt der Datenbankkontext den SQL-Befehl INSERT aus.

Eine Entität kann einen der [folgenden Status](/dotnet/api/microsoft.entityframeworkcore.entitystate) aufweisen:

* `Added`: Die Entität ist noch nicht in der Datenbank vorhanden. Die Methode `SaveChanges` gibt eine INSERT-Anweisung aus.

* `Unchanged`: Für diese Entität müssen keine Änderungen gespeichert werden. Eine Entität weist diesen Zustand auf, wenn sie von der Datenbank gelesen wird.

* `Modified`: Einige oder alle Eigenschaftswerte der Entität wurden geändert. Die Methode `SaveChanges` gibt eine UPDATE-Anweisung aus.

* `Deleted`: Die Entität wurde zum Löschen markiert. Die Methode `SaveChanges` gibt eine DELETE-Anweisung aus.

* `Detached`: Die Entität wird nicht vom Datenbankkontext nachverfolgt.

Zustandsänderungen werden in einer Desktop-App in der Regel automatisch festgelegt. Eine Entität wird gelesen, Änderungen werden vorgenommen, und der Entitätszustand wird automatisch in `Modified` geändert. Durch das Aufrufen von `SaveChanges` wird eine SQL UPDATE-Anweisung generiert, die nur die geänderten Eigenschaften aktualisiert.

In einer Web-App wird der `DbContext`verfügbar gemacht, der eine Entität liest und die Daten anzeigt, nachdem eine Seite gerendert wurde. Wenn die Methode `OnPostAsync` einer Seite aufgerufen wird, wird eine neue Webanforderung mit einer neuen Instanz von `DbContext` gestellt. Durch erneutes Lesen der Entität in diesem neuen Kontext wird die Desktopverarbeitung simuliert.

## <a name="update-the-delete-page"></a>Aktualisieren der Seite „Delete“ (Löschen)

In diesem Abschnitt wird Code hinzugefügt, um eine benutzerdefinierte Fehlermeldung zu implementieren, wenn der Aufruf von `SaveChanges` fehlschlägt. Fügen Sie eine Zeichenfolge hinzu, die mögliche Fehlermeldungen enthalten soll:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet1&highlight=12)]

Ersetzen Sie die `OnGetAsync`-Methode durch folgenden Code:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet_OnGetAsync&highlight=1,9,17-20)]

Der vorangehende Code enthält den optionalen Parameter `saveChangesError`. `saveChangesError` gibt an, ob die Methode nach einem Fehler beim Löschen des Studentenobjekts aufgerufen wurde. Der Löschvorgang schlägt möglicherweise aufgrund von vorübergehenden Netzwerkproblemen fehl. Vorübergehende Netzwerkfehler treten eher in der Cloud auf. `saveChangesError` ist „FALSE“, wenn die Methode `OnGetAsync` auf der Seite „Löschen“ über die Benutzeroberfläche aufgerufen wird. Wenn `OnGetAsync` von `OnPostAsync` aufgerufen wird (aufgrund des fehlgeschlagenen Löschvorgangs), ist der Parameter `saveChangesError` „TRUE“.

### <a name="the-delete-pages-onpostasync-method"></a>Die Methode „OnPostAsync“ auf „Löschen“-Seiten

Ersetzen Sie `OnPostAsync` durch den folgenden Code:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet_OnPostAsync)]

Der vorangehende Code ruft die ausgewählte Entität ab und anschließend die Methode [Remove](/dotnet/api/microsoft.entityframeworkcore.dbcontext.remove#Microsoft_EntityFrameworkCore_DbContext_Remove_System_Object_) auf, um den Zustand der Entität auf `Deleted` festzulegen. Wenn `SaveChanges` aufgerufen wird, wird der SQL-Befehl DELETE generiert. Wenn `Remove` fehlschlägt:

* Wird die Datenbankausnahme abgefangen.
* Wird die Methode `OnGetAsync` auf der Seite „Löschen“ mit `saveChangesError=true` aufgerufen.

### <a name="update-the-delete-razor-page"></a>Aktualisieren der Razor Page „Löschen“

Fügen Sie folgende hervorgehobene Fehlermeldung zur Razor Page „Löschen“ hinzu.
<!--
[!code-cshtml[](intro/samples/cu21/Pages/Students/Delete.cshtml?name=snippet&highlight=11)]
-->
[!code-cshtml[](intro/samples/cu21/Pages/Students/Delete.cshtml?range=1-13&highlight=10)]

Testen Sie die Seite „Löschen“.

## <a name="common-errors"></a>Häufige Fehler

„Students/Index“ oder andere Links funktionieren nicht:

Überprüfen Sie, ob die Razor Page die richtige `@page`-Anweisung enthält. Die Razor-Seite „Students/Index“ sollte beispielsweise **keine** Routenvorlage enthalten:

```cshtml
@page "{id:int}"
```

Die `@page`-Anweisung muss auf jeder Razor Page vorhanden sein.

::: moniker-end

> [!div class="step-by-step"]
> [Zurück](xref:data/ef-rp/intro)
> [Weiter](xref:data/ef-rp/sort-filter-page)
