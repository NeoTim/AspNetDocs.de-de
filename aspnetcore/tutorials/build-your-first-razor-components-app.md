---
title: Erstellen Ihrer ersten Razor Components-App
author: guardrex
description: Erstellen Sie schrittweise eine Razor Components-App, und lernen Sie grundlegende Razor Components-Konzepte kennen.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040777"
---
# <a name="build-your-first-razor-components-app"></a>Erstellen Ihrer ersten Razor Components-App

Von [Daniel Roth](https://github.com/danroth27) und [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

In diesem Tutorial erfahren Sie, wie Sie eine App mit Razor Components erstellen, und es demonstriert die grundlegenden Razor Components-Konzepte. Sie können für dieses Tutorial entweder ein Razor Components-basiertes (in .NET Core 3.0 oder höher unterstütztes) Projekt oder ein Blazor-basiertes (in einer zukünftigen Version von .NET Core unterstütztes) Projekt verwenden.

Für eine Benutzeroberfläche mit ASP.NET Core-Razor Components (*empfohlen*):

* Führen Sie die Anleitung in <xref:razor-components/get-started> aus, um ein Razor Components-basiertes Projekt zu erstellen.
* Benennen Sie das Projekt mit `RazorComponents`.
* Eine Projektmappe mit mehreren Projekten wird aus der Razor Components-Vorlage erstellt. Das Razor Components-Projekt wird als *RazorComponents.App* generiert.

Für eine Benutzeroberfläche mit Blazor:

* Führen Sie die Anleitung in <xref:spa/blazor/get-started> aus, um ein Blazor-basiertes Projekt zu erstellen.
* Benennen Sie das Projekt mit `Blazor`.
* Eine Lösung für ein einzelnes Projekt wird aus der Blazor-Vorlage erstellt.

[Zeigen Sie Beispielcode an, oder laden Sie diesen herunter](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample)). Weitere Voraussetzungen finden Sie in den folgenden Themen:

## <a name="build-components"></a>Erstellen von Komponenten

1. Navigieren Sie zu jeder der drei Seiten der App: „Home“, „Counter“ und „Fetch data“. Diese Seiten werden durch die Razor-Dateien im *Pages*-Ordner implementiert: *Index.cshtml*, *Counter.cshtml* und *FetchData.cshtml*.

1. Wählen Sie auf der Seite „Counter“ die Schaltfläche **Hier klicken** aus, um den Zähler ohne Seitenaktualisierung heraufzusetzen. Das Heraufsetzen eines Zählers auf einer Webseite erfordert normalerweise das Schreiben in JavaScript, aber Razor Components bietet einen besseren Ansatz mit C#.

1. Sehen Sie sich die Implementierung der Counter-Komponente in der *Counter.cshtml*-Datei an.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   Die Benutzeroberfläche der Counter-Komponente wird mithilfe von HTML definiert. Dynamische Renderinglogik (z.B. Schleifen, Bedingungen, Ausdrücken) wird über eine eingebettete C#-Syntax mit dem Namen [Razor](xref:mvc/views/razor) hinzugefügt. Das HTML-Markup und die C#-Renderinglogik werden zur Erstellungszeit in eine Komponentenklasse konvertiert. Der Name der generierten .NET-Klasse stimmt mit dem Namen der Datei überein.

   Member der Komponentenklasse werden in einem `@functions`-Block definiert. Im `@functions`-Block werden der Komponentenstatus (Eigenschaften, Felder) und Methoden für die Behandlung von Ereignissen oder das Definieren anderer Komponentenlogik angegeben. Diese Member werden dann als Teil der Renderinglogik der Komponente und zur Behandlung von Ereignissen verwendet.

   Wenn die **Hier klicken**-Schaltfläche ausgewählt wird:

   * Der registrierte `onclick`-Handler der Counter-Komponente wird aufgerufen (die `IncrementCount`-Methode).
   * Die Counter-Komponente generiert ihre Renderstruktur neu.
   * Die neue Renderstruktur wird mit der vorherigen verglichen.
   * Es werden nur Änderungen des Dokumentobjektmodells (Document Object Model, DOM) angewendet. Der angezeigte Zähler wird aktualisiert.

1. Ändern Sie die C#-Logik der Counter-Komponente, um das Zählerinkrement von eins auf zwei heraufzusetzen.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. Erstellen Sie die App neu, und führen Sie sie aus, um die Änderungen anzuzeigen. Wählen Sie die Schaltfläche **Hier klicken** aus, und der Zähler wird um zwei heraufgesetzt.

## <a name="use-components"></a>Verwenden von Komponenten

Beziehen Sie eine Komponente mithilfe einer HTML-ähnlichen Syntax in eine andere Komponente ein.

1. Fügen Sie die Counter-Komponente der Index-Komponente (Startseite) der App durch Hinzufügen eines `<Counter />`-Elements zur Index-Komponente hinzu.

   Wenn Sie für diese Oberfläche Blazor verwenden, enthält die Index-Komponente eine Survey Prompt-Komponente (`<SurveyPrompt>`-Element). Ersetzen Sie das `<SurveyPrompt>`-Element durch das `<Counter>`-Element.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. Erstellen Sie die App neu, und führen Sie sie aus. Die Startseite verfügt über einen eigenen Zähler.

## <a name="component-parameters"></a>Komponentenparameter

Komponenten können auch Parameter aufweisen. Komponentenparameter werden mithilfe nicht öffentlicher Eigenschaften für die Komponentenklasse definiert, die mit `[Parameter]` versehen ist. Verwenden Sie Attribute, um Argumente für eine Komponente im Markup anzugeben.

1. Aktualisieren Sie den `@functions`-C#-Code der Komponente:

   * Fügen Sie eine `IncrementAmount`-Eigenschaft hinzu, die mit dem `[Parameter]`-Attribut ausgestattet ist.
   * Ändern Sie die `IncrementCount`-Methode, um `IncrementAmount` beim Heraufsetzen des Werts von `currentCount` zu verwenden.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. Geben Sie unter Verwendung eines Attributs einen `IncrementAmount`-Parameter in das `<Counter>`-Element der Home-Komponente ein. Legen Sie den Wert fest, um den Zähler um zehn heraufzusetzen.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. Laden Sie die Seite neu. Der Zähler auf der Startseite wird jedes Mal, wenn die Schaltfläche **Hier klicken** ausgewählt wird, um zehn heraufgesetzt. Der Zähler auf der *Counter*-Seite wird um eins heraufgesetzt.

## <a name="route-to-components"></a>Weiterleiten an Komponenten

Die `@page`-Anweisung im oberen Teil der *Counter.cshtml*-Datei gibt an, dass diese Komponente ein Routingendpunkt ist. Die Counter-Komponente behandelt Anforderungen, die an `/Counter` gesendet werden. Ohne die `@page`-Anweisung behandelt die Komponente keine weitergeleiteten Anforderungen, aber die Komponente kann immer noch von anderen Komponenten verwendet werden.

## <a name="dependency-injection"></a>Dependency Injection

Im Dienstcontainer der App registrierte Dienste stehen für Komponenten über [Abhängigkeitsinjektion (DI, Dependency Injection)](xref:fundamentals/dependency-injection) zur Verfügung. Fügen Sie Dienste mit der `@inject`-Anweisung in eine Komponente ein.

Überprüfen Sie die Anweisungen der FetchData-Komponente (*Pages/FetchData.cshtml*). Mit der `@inject`-Anweisung wird die Instanz des `WeatherForecastService`-Diensts in die Komponente eingefügt:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

Der `WeatherForecastService`-Dienst ist als [Singleton](xref:fundamentals/dependency-injection#service-lifetimes) registriert, sodass eine Instanz des Diensts in der gesamten App verfügbar ist.

Die FetchData-Komponente verwendet den eingefügten Dienst als `ForecastService`, um ein Array von `WeatherForecast`-Objekten abzurufen:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

Eine [@foreach](/dotnet/csharp/language-reference/keywords/foreach-in)-Schleife rendert jede Vorhersageinstanz als eine Zeile in der Wetterdatentabelle:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a>Erstellen einer Aufgabenliste

Fügen Sie der App eine neue Seite hinzu, die eine einfache Aufgabenliste implementiert.

1. Fügen Sie dem Ordner *Pages* eine leere Datei mit dem Namen *Todo.cshtml* hinzu.

1. Geben Sie das ursprüngliche Markup für die Seite an:

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. Fügen Sie der Navigationsleiste die Todo-Seite hinzu.

   Die NavMenu-Komponente (*Shared/NavMenu.csthml*) wird im Layout der App verwendet. Layouts sind Komponenten, mit denen Sie die Duplizierung des Inhalts in der App vermeiden können. Weitere Informationen finden Sie unter <xref:razor-components/layouts>.

   Fügen Sie einen `<NavLink>` für die Todo-Seite hinzu, indem Sie das folgende Listenelementmarkup unterhalb der vorhandenen Listenelemente der Datei *Shared/NavMenu.csthml* hinzufügen:

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. Erstellen Sie die App neu, und führen Sie sie aus. Besuchen Sie die neue Todo-Seite, um sicherzustellen, dass der Link zur Todo-Seite funktioniert.

1. Fügen Sie eine *TodoItem.cs*-Datei dem Stamm des Projekts hinzu, die eine Klasse zum Darstellen eines Aufgabenelements enthalten soll. Verwenden Sie den folgenden C#-Code für die `TodoItem`-Klasse:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. Kehren Sie zur Todo-Komponente (*Todo.cshtml*) zurück:

   * Fügen Sie ein Feld für die Todo-Elemente in einem `@functions`-Block hinzu. Die Todo-Komponente verwaltet mit diesem Feld den Status der Aufgabenliste.
   * Fügen Sie ein Markup für eine unsortierte Liste und eine `foreach`-Schleife hinzu, um jedes Aufgabenelement als Listenelement zu rendern.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. Die App benötigt Benutzeroberflächenelemente, damit der Liste Aufgaben hinzugefügt werden können. Fügen Sie eine Texteingabe und eine Schaltfläche unterhalb der Liste hinzu:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. Erstellen Sie die App neu, und führen Sie sie aus. Bei Auswahl der Schaltfläche **Todo-Element hinzufügen** geschieht nichts, da kein Ereignishandler mit der Schaltfläche verknüpft ist.

1. Fügen Sie eine `AddTodo`-Methode der Todo-Komponente hinzu, und registrieren Sie sie mit dem `onclick`-Attribut für Schaltflächenklicks:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   Die `AddTodo`-C#-Methode wird aufgerufen, wenn die Schaltfläche ausgewählt wird.

1. Um den Titel des neuen Aufgabenelements abzurufen, fügen Sie ein `newTodo`-Zeichenfolgenfeld hinzu, und binden Sie es mithilfe des `bind`-Attributs an den Wert der Texteingabe:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. Aktualisieren Sie die `AddTodo`-Methode, um das `TodoItem` mit dem angegebenen Titel der Liste hinzuzufügen. Löschen Sie den Wert der Texteingabe, indem Sie für `newTodo` eine leere Zeichenfolge festlegen:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. Erstellen Sie die App neu, und führen Sie sie aus. Fügen Sie der Aufgabenliste einige Aufgabenelemente hinzu, um den neuen Code zu testen.

1. Der Titeltext für die einzelnen Aufgabenelemente kann bearbeitet werden, und ein Kontrollkästchen kann dem Benutzer helfen, die erledigten Elemente nachzuverfolgen. Fügen Sie für jedes Aufgabenelement eine Kontrollkästcheneingabe hinzu, und binden Sie ihren Wert an die `IsDone`-Eigenschaft. Ändern Sie `@todo.Title` in ein `<input>`-Element, das an `@todo.Title` gebunden ist:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. Um sicherzustellen, dass diese Werte gebunden sind, aktualisieren Sie den `<h1>`-Header, um die Anzahl der noch nicht erledigten Aufgabenelemente anzuzeigen (`IsDone` ist `false`).

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. Die erledigte Todo-Komponente (*Todo.cshtml*):

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. Erstellen Sie die App neu, und führen Sie sie aus. Fügen Sie Aufgabenelemente hinzu, um den neuen Code zu testen.

## <a name="publish-and-deploy-the-app"></a>Veröffentlichen und Bereitstellen der App

Wie Sie die App veröffentlichen, erfahren Sie unter <xref:host-and-deploy/razor-components/index#publish-the-app>.
