---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: Erweiterte Entity Framework Szenarien für eine MVC-Webanwendung (10 von 10) | Microsoft-Dokumentation
author: tdykstra
description: Die Beispiel-Webanwendung der Beispiel-Web-App veranschaulicht, wie ASP.NET MVC 4-Anwendungen mithilfe der Entity Framework 5 Code First und Visual Studio erstellt werden...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85dd59016d904a9f654c438db977b5ae2c0187d2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045051"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>Erweiterte Entity Framework Szenarien für eine MVC-Webanwendung (10 von 10)

von [Tom Dykstra](https://github.com/tdykstra)

[Herunterladen des abgeschlossenen Projekts](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Die Beispiel-Webanwendung der Beispiel-Web-App veranschaulicht, wie ASP.NET MVC 4-Anwendungen mithilfe der Entity Framework 5 Code First und Visual Studio 2012 erstellt werden. Informationen zu dieser Tutorialreihe finden Sie im [ersten Tutorial der Reihe](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Sie können die tutorialreihe von Anfang an starten oder [ein Starter-Projekt für dieses Kapitel herunterladen](building-the-ef5-mvc4-chapter-downloads.md) und hier beginnen.
> 
> > [!NOTE] 
> > 
> > Wenn Sie auf ein Problem stoßen, das Sie nicht beheben können, [Laden Sie das abgeschlossene Kapitel herunter](building-the-ef5-mvc4-chapter-downloads.md) , und versuchen Sie, das Problem zu reproduzieren. Im Allgemeinen können Sie die Lösung für das Problem finden, indem Sie Ihren Code mit dem abgeschlossenen Code vergleichen. Informationen zu häufigen Fehlern und deren Lösung finden Sie unter [Fehler und](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) Problem Umgehungen.

Im vorherigen Tutorial haben Sie das Repository und Arbeitseinheits Muster implementiert. In diesem Tutorial werden die folgenden Themen behandelt:

- Ausführen von unformatierten SQL-Abfragen
- Ausführen von Abfragen ohne Nachverfolgung.
- Untersuchen von Abfragen, die an die Datenbank gesendet werden.
- Arbeiten mit Proxy Klassen.
- Deaktivieren der automatischen Erkennung von Änderungen.
- Deaktivieren der Validierung beim Speichern von Änderungen.
- [Fehler und Arbeit](#errors)

Für die meisten dieser Themen arbeiten Sie mit Seiten, die Sie bereits erstellt haben. Wenn Sie für Massen Aktualisierungen Rohdaten verwenden möchten, erstellen Sie eine neue Seite, auf der die Anzahl der Gutschriften aller Kurse in der Datenbank aktualisiert wird:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Um eine Abfrage ohne Nachverfolgung zu verwenden, fügen Sie der Bearbeitungsseite für Abteilungen neue Validierungs Logik hinzu:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>Ausführen von RAW-SQL-Abfragen

Die Entity Framework Code First-API umfasst Methoden, die es Ihnen ermöglichen, SQL-Befehle direkt an die Datenbank zu übergeben. Folgende Optionen stehen zur Auswahl:

- Verwenden Sie die `DbSet.SqlQuery`-Methode für Abfragen, die Entitätstypen zurückgeben. Die zurückgegebenen Objekte müssen vom Typ sein, der vom-Objekt erwartet wird `DbSet` , und Sie werden automatisch vom Daten Bank Kontext nachverfolgt, es sei denn, Sie deaktivieren die Nachverfolgung. (Informationen zur-Methode finden Sie im folgenden Abschnitt `AsNoTracking` .)
- Verwenden Sie die `Database.SqlQuery` Methode für Abfragen, die Typen zurückgeben, die keine Entitäten sind. Die zurückgegebenen Daten werden nicht vom Datenbankkontext nachverfolgt, auch wenn Sie diese Methode zum Abrufen von Entitätstypen verwenden.
- Verwenden Sie den [Database.Executesqlcommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) für nicht-Abfrage Befehle.

Einer der Vorteile von Entity Framework ist die Tatsache, dass vermieden wird, den Code zu eng an eine bestimmte Methode zum Speichern von Daten zu binden. Dies geschieht, indem SQL-Abfragen und -Befehle für Sie generiert werden. Somit müssen Sie sie nicht selbst schreiben. Es gibt jedoch außergewöhnliche Szenarios, in denen Sie bestimmte SQL-Abfragen ausführen müssen, die Sie manuell erstellt haben. diese Methoden ermöglichen es Ihnen, solche Ausnahmen zu behandeln.

Dies trifft immer zu, wenn Sie SQL-Befehle in einer Webanwendung ausführen. Treffen Sie deshalb Vorsichtsmaßnahmen, um Ihre Website vor Angriffen durch Einschleusung von SQL-Befehlen zu schützen. Verwenden Sie dazu parametrisierte Abfragen, um sicherzustellen, dass Zeichenfolgen, die von einer Webseite übermittelt werden, nicht als SQL-Befehle interpretiert werden können. In diesem Tutorial verwenden Sie parametrisierte Abfragen beim Integrieren von Benutzereingaben in eine Abfrage.

### <a name="calling-a-query-that-returns-entities"></a>Aufrufen einer Abfrage, die Entitäten zurückgibt

Angenommen, Sie möchten `GenericRepository` , dass die-Klasse zusätzliche Filter-und Sortierungs Flexibilität bereitstellt, ohne dass Sie eine abgeleitete Klasse mit zusätzlichen Methoden erstellen müssen. Eine Möglichkeit, dies zu erreichen, besteht darin, eine Methode hinzuzufügen, die eine SQL-Abfrage akzeptiert. Sie können dann eine beliebige Art von Filtern oder Sortieren im Controller angeben, z. b. eine- `Where` Klausel, die von einem Joins oder einer Unterabfrage abhängt. In diesem Abschnitt erfahren Sie, wie Sie eine solche Methode implementieren.

Erstellen Sie die- `GetWithRawSql` Methode, indem Sie den folgenden Code zu *GenericRepository.cs*hinzufügen:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

Nennen Sie in *CourseController.cs*die neue Methode von der- `Details` Methode, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

In diesem Fall könnten Sie die- `GetByID` Methode verwenden, aber Sie verwenden die- `GetWithRawSql` Methode, um zu überprüfen, ob die- `GetWithRawSQL` Methode funktioniert.

Führen Sie die Detailseite aus, um zu überprüfen, ob die SELECT-Abfrage funktioniert (Wählen Sie die Registerkarte **Kurs** und dann **Details** für einen Kurs).

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Aufrufen einer Abfrage, die andere Objekttypen zurückgibt

Sie haben zuvor ein Statistikraster für Studenten für die Infoseite erstellt, das die Anzahl der Studenten für jedes Anmeldedatum zeigt. Der Code, der dies in *HomeController.cs* durchführt, verwendet LINQ:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

Angenommen, Sie möchten den Code schreiben, der diese Daten direkt in SQL abruft, statt LINQ zu verwenden. Hierzu müssen Sie eine Abfrage ausführen, die etwas anderes als Entitäts Objekte zurückgibt. Dies bedeutet, dass Sie die- `Database.SqlQuery` Methode verwenden müssen.

Ersetzen Sie in *HomeController.cs*die LINQ-Anweisung in der- `About` Methode durch den folgenden Code:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Führen Sie die Seite Info aus. Sie zeigt die gleichen Daten wie zuvor.

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>Aufrufen einer Update Abfrage

Nehmen wir an, dass die Administratoren von Administratoren in der Lage sein sollen, Massen Änderungen in der Datenbank auszuführen, z. b. die Anzahl der Gutschriften für jeden Kurs zu ändern. Wenn die Universität über eine große Anzahl an Kursen verfügt, wäre es ineffizient, sie alle als Entitäten abzurufen und separat zu ändern. In diesem Abschnitt implementieren Sie eine Webseite, die es dem Benutzer ermöglicht, einen Faktor anzugeben, nach dem die Anzahl der Gutschriften für alle Kurse geändert werden soll, und Sie nehmen die Änderung vor, indem Sie eine SQL- `UPDATE` Anweisung ausführen. Die Webseite wird wie die folgende Abbildung aussehen:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

Im vorherigen Tutorial haben Sie das generische Repository verwendet, um `Course` Entitäten im Controller zu lesen und zu aktualisieren `Course` . Für diesen Massen Aktualisierungs Vorgang müssen Sie eine neue Repository-Methode erstellen, die nicht im generischen Repository ist. Zu diesem Zweck erstellen Sie eine dedizierte Klasse, die `CourseRepository` von der- `GenericRepository` Klasse abgeleitet wird.

Erstellen Sie im Ordner *dal* *CourseRepository.cs* , und ersetzen Sie den vorhandenen Code durch den folgenden Code:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

Ändern Sie in *UnitOfWork.cs*den `Course` Repository-Typ von `GenericRepository<Course>` in. `CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

Fügen Sie in *CourseController.cs*eine- `UpdateCourseCredits` Methode hinzu:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

Diese Methode wird sowohl für `HttpGet` als auch für verwendet `HttpPost` . Wenn die-Methode ausgeführt wird `HttpGet` `UpdateCourseCredits` , ist die `multiplier` Variable NULL, und in der Ansicht werden ein leeres Textfeld und eine Schaltfläche zum Senden angezeigt, wie in der obigen Abbildung dargestellt.

Wenn auf die Schaltfläche **Aktualisieren** geklickt wird und die-Methode ausgeführt wird `HttpPost` , `multiplier` erhält den Wert, der in das Textfeld eingegeben wird. Der Code ruft dann die Repository `UpdateCourseCredits` -Methode auf, die die Anzahl der betroffenen Zeilen zurückgibt, und dieser Wert wird im- `ViewBag` Objekt gespeichert. Wenn die Ansicht die Anzahl der betroffenen Zeilen im- `ViewBag` Objekt empfängt, wird diese Zahl anstelle des Textfelds und der Schaltfläche "Senden" angezeigt, wie in der folgenden Abbildung dargestellt:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

Erstellen Sie eine Ansicht im Ordner " *views\course* " für die Seite mit den Gutschriften zum Update Kurs:

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

Ersetzen Sie in *views\course\updatecoursecrediz.cshtml*den Vorlagen Code durch den folgenden Code:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

Führen Sie die `UpdateCourseCredits`-Methode aus, indem Sie die Registerkarte **Courses** (Kurse) auswählen, und dann „/UpdateCourseCredits“ am Ende der URL in die Adressleiste des Browsers einfügen (z.B.: `http://localhost:50205/Course/UpdateCourseCredits`). Geben Sie eine Zahl in das Textfeld ein:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

Klicken Sie auf **Aktualisieren**. Die Anzahl der betroffenen Zeilen wird angezeigt:

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

Klicken Sie auf **Zurück zur Liste**, um die Kursliste mit der geänderte Anzahl von Credits anzuzeigen.

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

Weitere Informationen zu unformatierten SQL-Abfragen finden Sie unter unformatierte [SQL-Abfragen](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) im Entity Framework Teamblog.

## <a name="no-tracking-queries"></a>Abfragen ohne Nachverfolgung

Wenn ein Daten Bank Kontext Daten Bank Zeilen abruft und Entitäts Objekte erstellt, die diese darstellen, wird standardmäßig nachverfolgt, ob die Entitäten im Arbeitsspeicher mit den Daten in der Datenbank synchronisiert sind. Die Daten im Arbeitsspeicher fungieren als Cache und werden verwendet, wenn Sie eine Entität aktualisieren. Diese Zwischenspeicherung ist in Webanwendungen oft überflüssig, da Kontextinstanzen in der Regel kurzlebig sind (eine neue wird bei jeder Anforderung erstellt und gelöscht), und der Kontext, der eine Entität liest, wird in der Regel gelöscht, bevor diese Entität erneut verwendet wird.

Mithilfe der-Methode können Sie angeben, ob der Kontext Entitäts Objekte für eine Abfrage nachverfolgt `AsNoTracking` . Typische Szenarios, in denen Sie das möglicherweise tun wollen, umfassen Folgendes:

- Die Abfrage ruft eine solche große Menge von Daten ab, durch die das Ausschalten der Nachverfolgung die Leistung merklich verbessern kann.
- Sie möchten eine Entität anfügen, um Sie zu aktualisieren, aber Sie haben zuvor dieselbe Entität für einen anderen Zweck abgerufen. Da diese Entität bereits vom Datenbankkontext nachverfolgt wird, können Sie die zu ändernde Entität nicht anfügen. Eine Möglichkeit, dies zu verhindern, ist die Verwendung der- `AsNoTracking` Option mit der vorherigen Abfrage.

In diesem Abschnitt implementieren Sie die Geschäftslogik, die die zweite dieser Szenarios veranschaulicht. Insbesondere erzwingen Sie eine Geschäftsregel, die besagt, dass ein Dozenten nicht Administrator mehrerer Abteilungen sein kann.

Fügen Sie in *DepartmentController.cs*eine neue Methode hinzu, die Sie von der-Methode und der-Methode aus abrufen können, `Edit` `Create` um sicherzustellen, dass keine zwei Abteilungen denselben Administrator aufweisen:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

Fügen Sie im- `try` Block der-Methode Code hinzu `HttpPost` `Edit` , um diese neue Methode aufzurufen, wenn keine Validierungs Fehler vorliegen. Der- `try` Block sieht nun wie im folgenden Beispiel aus:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

Führen Sie die Bearbeitungsseite der Abteilung aus, und versuchen Sie, den Administrator einer Abteilung in einen Dozenten zu ändern, der bereits Administrator einer anderen Abteilung ist. Sie erhalten die erwartete Fehlermeldung:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Führen Sie die Bearbeitungsseite für Abteilungen erneut aus, und ändern Sie dann den **Budget** Betrag. Wenn Sie auf **Speichern**klicken, wird eine Fehlerseite angezeigt:

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

Die Ausnahme Fehlermeldung lautet " `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` ", dies ist aufgrund der folgenden Ereignis Sequenz aufgetreten:

- Die- `Edit` Methode ruft die- `ValidateOneAdministratorAssignmentPerInstructor` Methode auf, die alle Abteilungen abruft, die Kim Abercrombie als Administrator haben. Dies bewirkt, dass die englische Abteilung gelesen wird. Da es sich um die Abteilung handelt, die bearbeitet wird, wird kein Fehler gemeldet. Als Ergebnis dieses Lesevorgangs wird die englische Abteilungs Entität, die aus der Datenbank gelesen wurde, jetzt jedoch vom Daten Bank Kontext nachverfolgt.
- Die- `Edit` Methode versucht, das- `Modified` Flag für die englische Abteilungs Entität festzulegen, die von der MVC-Modell Bindung erstellt wurde. Dies schlägt jedoch fehl, da der Kontext bereits eine Entität für die englische Abteilung nachverfolgt.

Eine Lösung für dieses Problem besteht darin, den Kontext daran zu halten, in-Memory-Abteilungs Entitäten zu verfolgen, die von der Überprüfungs Abfrage abgerufen werden. Dies hat keinen Nachteil, weil Sie diese Entität nicht aktualisieren oder Sie nicht wieder in eine Weise lesen, die davon profitieren würde, dass Sie im Arbeitsspeicher zwischengespeichert wird.

Geben Sie in *DepartmentController.cs*in der- `ValidateOneAdministratorAssignmentPerInstructor` Methode keine Nachverfolgung an, wie im folgenden dargestellt:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

Wiederholen Sie den Versuch, den **Budget** Betrag einer Abteilung zu bearbeiten. Dieses Mal ist der Vorgang erfolgreich, und der Standort wird erwartungsgemäß auf die Index Seite "Abteilungen" zurückgegeben, die den überarbeiteten Budget Wert anzeigt.

## <a name="examining-queries-sent-to-the-database"></a>Untersuchen der an die Datenbank gesendeten Abfragen

Manchmal ist es hilfreich, die tatsächlichen SQL-Abfragen anzuzeigen, die an die Datenbank gesendet werden. Zu diesem Zweck können Sie eine Abfrage Variable im Debugger untersuchen oder die-Methode der Abfrage aufzurufen `ToString` . Um dies auszuprobieren, sehen Sie sich eine einfache Abfrage an und sehen sich an, was passiert, wenn Sie Optionen wie Eager Loading, Filterung und Sortierung hinzufügen.

Ersetzen Sie in *Controllers/coursecontroller die-* `Index` Methode durch den folgenden Code:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

Legen Sie nun in *GenericRepository.cs* einen Haltepunkt für die `return query.ToList();` -Anweisungen und die-Anweisung der- `return orderBy(query).ToList();` Methode fest `Get` . Führen Sie das Projekt im Debugmodus aus, und wählen Sie die Kursindex Seite aus. Wenn der Code den Breakpoint erreicht, untersuchen Sie die `query` Variable. Die Abfrage, die an SQL Server gesendet wird, wird angezeigt. Dabei handelt es sich um eine einfache `Select` Anweisung:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.sql)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

Abfragen können zu lang sein, damit Sie in Visual Studio in den Debugfenstern angezeigt werden. Sie können den Variablen Wert kopieren und in einen Text-Editor einfügen, um die gesamte Abfrage anzuzeigen:

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

Nun fügen Sie der Index Seite Course eine Dropdown Liste hinzu, damit Benutzer nach einer bestimmten Abteilung filtern können. Sie sortieren die Kurse nach Titel und geben Eager Loading für die `Department` Navigations Eigenschaft an. Ersetzen Sie in *CourseController.cs*die- `Index` Methode durch den folgenden Code:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

Die-Methode empfängt den ausgewählten Wert der Dropdown Liste im- `SelectedDepartment` Parameter. Wenn nichts ausgewählt ist, wird dieser Parameter NULL sein.

Eine `SelectList` Sammlung, die alle Abteilungen enthält, wird an die Ansicht für die Dropdown Liste übermittelt. Die Parameter, die an den `SelectList` Konstruktor übergeben werden, geben den Wert Feldnamen, den Text Feldnamen und das ausgewählte Element an.

Bei der- `Get` Methode des `Course` Repository gibt der Code einen Filter Ausdruck, eine Sortierreihenfolge und Eager Loading für die `Department` Navigations Eigenschaft an. Der Filter Ausdruck gibt immer zurück `true` , wenn in der Dropdown Liste nichts ausgewählt ist (d `SelectedDepartment` . h. ist NULL).

Fügen Sie in " *views\course\index.cshtml*" direkt vor dem öffnenden `table` Tag den folgenden Code hinzu, um die Dropdown Liste und die Schaltfläche "Senden" zu erstellen:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

Wenn die Breakpoints in der-Klasse noch festgelegt `GenericRepository` sind, führen Sie die Index Seite Course aus. Fahren Sie mit dem ersten zwei Mal fort, dass der Code auf einen Haltepunkt trifft, damit die Seite im Browser angezeigt wird. Wählen Sie in der Dropdown Liste eine Abteilung aus, und klicken Sie auf **Filtern**:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

Dieses Mal wird der erste Breakpoint für die Abfrage der Abteilungen für die Dropdown Liste angezeigt. Überspringen Sie, und `query` zeigen Sie die Variable an, wenn der Code das nächste Mal den Breakpoint erreicht, um zu sehen, `Course` wie die Abfrage nun aussieht. Folgendes wird angezeigt:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.sql)]

Sie können sehen, dass es sich bei der Abfrage um eine Abfrage handelt, `JOIN` die `Department` Daten zusammen mit den `Course` Daten lädt und eine- `WHERE` Klausel enthält.

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>Arbeiten mit Proxy Klassen

Wenn das Entity Framework Entitäts Instanzen erstellt (z. b. beim Ausführen einer Abfrage), werden diese häufig als Instanzen eines dynamisch generierten abgeleiteten Typs erstellt, der als Proxy für die Entität fungiert. Dieser Proxy überschreibt einige virtuelle Eigenschaften der Entität, um beim Zugriff auf die Eigenschaft automatisch Hooks zum Ausführen von Aktionen einzufügen. Dieser Mechanismus wird z. b. verwendet, um Lazy Loading von Beziehungen zu unterstützen.

In den meisten Fällen müssen Sie sich diese Verwendung von Proxys nicht bewusst sein, aber es gibt Ausnahmen:

- In einigen Szenarien möchten Sie möglicherweise verhindern, dass die Entity Framework Proxy Instanzen erstellen. Beispielsweise ist das Serialisieren von nicht-Proxy Instanzen möglicherweise effizienter als das Serialisieren von Proxy Instanzen.
- Wenn Sie eine Entitäts Klasse mit dem-Operator instanziieren `new` , erhalten Sie keine Proxy Instanz. Dies bedeutet, dass Sie keine Funktionen wie Lazy Loading und die automatische Änderungs Nachverfolgung erhalten. Dies ist in der Regel in Ordnung. im Allgemeinen benötigen Sie Lazy Loading nicht, da Sie eine neue Entität erstellen, die sich nicht in der Datenbank befindet, und Sie benötigen im Allgemeinen keine Änderungs Nachverfolgung, wenn Sie die Entität explizit als markieren `Added` . Wenn Sie jedoch Lazy Loading benötigen und die Änderungs Nachverfolgung benötigen, können Sie mithilfe der-Methode der-Klasse neue Entitäts Instanzen mit Proxys erstellen `Create` `DbSet` .
- Möglicherweise möchten Sie einen tatsächlichen Entitätstyp aus einem Proxytyp erhalten. Sie können die- `GetObjectType` Methode der- `ObjectContext` Klasse verwenden, um den tatsächlichen Entitätstyp einer Proxytyp Instanz zu erhalten.

Weitere Informationen finden Sie unter [Arbeiten mit](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) Proxys im Entity Framework Teamblog.

## <a name="disabling-automatic-detection-of-changes"></a>Deaktivieren der automatischen Erkennung von Änderungen

Entity Framework bestimmt wie eine Entität geändert wurde (und welche Updates an die Datenbank gesendet werden müssen), indem die aktuellen Werte einer Entität mit den ursprünglichen Werten verglichen werden. Die ursprünglichen Werte werden gespeichert, wenn die Entität abgefragt oder angefügt wurde. Einige der Methoden, die automatisch eine Änderungserkennung durchführen, sind die folgenden:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Wenn Sie eine große Anzahl von Entitäten nachverfolgen und eine dieser Methoden mehrmals in einer Schleife aufzurufen, können Sie erhebliche Leistungsverbesserungen erzielen, indem Sie die automatische Änderungs Erkennung mithilfe der [autodetectchangesenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) -Eigenschaft vorübergehend ausschalten. Weitere Informationen finden Sie unter [Automatisches Erkennen von Änderungen](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).

## <a name="disabling-validation-when-saving-changes"></a>Deaktivieren der Validierung beim Speichern von Änderungen

Wenn Sie die- `SaveChanges` Methode aufzurufen, überprüft das Entity Framework standardmäßig die Daten in allen Eigenschaften aller geänderten Entitäten, bevor die Datenbank aktualisiert wird. Wenn Sie eine große Anzahl von Entitäten aktualisiert haben und die Daten bereits überprüft haben, ist diese Arbeit unnötig, und Sie können das Speichern der Änderungen weniger Zeit in Anspruch nehmen, indem Sie die Validierung vorübergehend deaktivieren. Dazu können Sie die [validateonsaveaktivierte](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) -Eigenschaft verwenden. Weitere Informationen finden Sie unter [Validierung](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).

## <a name="summary"></a>Zusammenfassung

Dies schließt diese Reihe von Tutorials zur Verwendung des Entity Framework in einer ASP.NET MVC-Anwendung ab. Links zu anderen Entity Framework Ressourcen finden Sie in der [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).

Weitere Informationen zum Bereitstellen der Webanwendung, nachdem Sie Sie erstellt haben, finden Sie unter [ASP.net Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in der MSDN Library.

Informationen zu anderen Themen im Zusammenhang mit MVC, z. b. Authentifizierung und Autorisierung, finden Sie in den von [MVC empfohlenen Ressourcen](../../getting-started/recommended-resources-for-mvc.md).

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>Danksagungen

- Tom Dykstra hat die Originalversion dieses Tutorials geschrieben und ist Senior Programming Writer im Inhalts Team von Microsoft-Webplattform und-Tools.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) hat dieses Tutorial gemeinsam verfasst und die meiste Arbeit für EF 5 und MVC 4 aktualisiert. Rick ist Senior Programming Writer für Microsoft, der sich auf Azure und MVC konzentriert.
- [Rowan Miller](http://www.romiller.com) und andere Mitglieder des Entity Framework Teams unterstützten Code Reviews und halfen dabei, viele Probleme mit Migrationen zu debuggen, die während des Aktualisierens des Tutorials für EF 5 entstanden sind.

## <a name="vb"></a>VB

Als das Tutorial ursprünglich erstellt wurde, haben wir sowohl c#-als auch VB-Versionen des abgeschlossenen Download Projekts bereitgestellt. Mit diesem Update stellen wir ein herunterladbares c#-Projekt für jedes Kapitel bereit, um den Einstieg in die Reihe zu vereinfachen. aufgrund von Zeitbeschränkungen und anderen Prioritäten haben wir das für VB nicht getan. Wenn Sie ein VB-Projekt mit diesen Tutorials erstellen und diese für andere Personen freigeben möchten, informieren Sie uns bitte.

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>Fehler und Problem Umgehungen

### <a name="cannot-createshadow-copy"></a>Erstellen/Schatten Kopie nicht möglich.

Fehlermeldung:

*Das Erstellen/Schatten kopieren von "dotnetopenauth. OpenID" ist nicht möglich, wenn diese Datei bereits vorhanden ist.*

Lösung:

Warten Sie einige Sekunden, und aktualisieren Sie die Seite.

### <a name="update-database-not-recognized"></a>Update-Datenbank wurde nicht erkannt.

Fehlermeldung:

*Der Begriff "Update-Database" wird nicht als Name eines Cmdlets, einer Funktion, einer Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder überprüfen Sie, ob der Pfad korrekt ist, und versuchen Sie es noch mal.* (Über den *`Update-Database`* Befehl in der PMC)

Lösung:

Beenden Sie Visual Studio. Öffnen Sie das Projekt erneut, und versuchen Sie es

### <a name="validation-failed"></a>Fehler bei der Überprüfung

Fehlermeldung:

*Fehler bei der Überprüfung für mindestens eine Entität. Weitere Informationen finden Sie unter der Eigenschaft "entityvalidationerrors".* (Über den *`Update-Database`* Befehl in der PMC)

Lösung:

Eine Ursache für dieses Problem sind Validierungs Fehler, wenn die-Methode ausgeführt wird `Seed` . Tipps zum Debuggen der-Methode finden Sie unter [Seeding und Debuggen Entity Framework (EF)-DSB](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` .

### <a name="http-50019-error"></a>HTTP 500,19-Fehler

Fehlermeldung:

*HTTP-Fehler 500,19-interner Server Fehler: auf die angeforderte Seite kann nicht zugegriffen werden, da die zugehörigen Konfigurationsdaten für die Seite ungültig sind.*

Lösung:

Eine Möglichkeit, diesen Fehler zu erhalten, besteht darin, mehrere Kopien der Lösung zu verwenden, von denen jeder dieselbe Portnummer verwendet. Sie können dieses Problem in der Regel beheben, indem Sie alle Instanzen von Visual Studio beenden und dann das Projekt neu starten, an dem Sie arbeiten. Wenn dies nicht funktioniert, versuchen Sie, die Portnummer zu ändern. Klicken Sie mit der rechten Maustaste auf die Projektdatei und dann auf Eigenschaften. Wählen Sie die Registerkarte **Web** aus, und ändern Sie dann die Portnummer im Textfeld **Projekt-URL** .

### <a name="error-locating-sql-server-instance"></a>Fehler beim Bestimmen der SQL Server-Instanz

Fehlermeldung:

*Netzwerk bezogener oder Instanzspezifischer Fehler beim Herstellen einer Verbindung mit SQL Server. Der Server wurde nicht gefunden oder war nicht zugänglich. Überprüfen Sie, ob der Instanzname richtig ist und SQL Server für die Verwendung von Remote Verbindungen konfiguriert ist. (Anbieter: SQL-Netzwerkschnittstellen, Fehler: 26-Fehler beim Suchen des angegebenen Servers/der angegebenen Instanz)*

Lösung:

Verbindungs Zeichenfolge überprüfen. Wenn Sie die Datenbank manuell gelöscht haben, ändern Sie den Namen der Datenbank in der Konstruktions Zeichenfolge.

> [!div class="step-by-step"]
> [Zurück](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [Weiter](building-the-ef5-mvc4-chapter-downloads.md)
