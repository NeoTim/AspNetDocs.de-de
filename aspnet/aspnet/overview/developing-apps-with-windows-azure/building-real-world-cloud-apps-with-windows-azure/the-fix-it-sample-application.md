---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Anhang: Die Fix It-Beispielanwendung (Erstellen von Real-World Cloud-Apps mit Azure) | Microsoft Docs'
author: MikeWasson
description: Das Building Real World Cloud Apps mit Azure E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es erklärt 13 Muster und Praktiken, die er...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675634"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Anhang: Die Fix It-Beispielanwendung (Erstellen von Real-World Cloud-Apps mit Azure)

von [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[The Fix It Project herunterladen](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Das **Building Real World Cloud Apps mit Azure** E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es werden 13 Muster und Vorgehensweisen erläutert, die Ihnen bei der erfolgreichen Entwicklung von Web-Apps für die Cloud helfen können. Informationen zum E-Book finden Sie [im ersten Kapitel](introduction.md).

Dieser Anhang zum E-Book Building Real World Cloud Apps with Azure enthält die folgenden Abschnitte, die zusätzliche Informationen zur Fix It-Beispielanwendung enthalten, die Sie herunterladen können:

- [Bekannte Probleme](#knownissues)
- [bewährten Methoden](#bestpractices)
- [So führen Sie die App von Visual Studio aus auf Ihrem lokalen Computer aus](#run-in-vs)
- [Bereitstellen der Basis-App in Azure App Service-Web-Apps mithilfe der Windows PowerShell-Skripts](#deploybase)
- [Fehlerbehebung bei windows PowerShell-Skripts](#troubleshooting)
- [Bereitstellen der App mit Warteschlangenverarbeitung in Azure App Service-Web-Apps und einem Azure Cloud Service](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Bekannte Probleme

Die Fix It App wurde ursprünglich entwickelt, um einige der in diesem E-Book vorgestellten Muster so einfach wie möglich zu veranschaulichen. Da es im E-Book jedoch um das Erstellen von realen Apps geht, haben wir den Fix It-Code einem Überprüfungs- und Testprozess unterzogen, ähnlich dem, was wir für veröffentlichte Software tun würden. Wir fanden eine Reihe von Problemen, und wie bei jeder realen Anwendung, einige von ihnen haben wir behoben und einige von ihnen haben wir auf eine spätere Veröffentlichung verschoben.

Die folgende Liste enthält Probleme, die in einer Produktionsanwendung behandelt werden sollten, aber aus dem einen oder anderen Grund haben wir uns entschieden, in der ersten Version der Fix It-Beispielanwendung nicht zu behandeln.

### <a name="security"></a>Sicherheit

- Stellen Sie sicher, dass Sie einem nicht vorhandenen Besitzer keine Aufgabe zuweisen können.
- Stellen Sie sicher, dass Sie nur Aufgaben anzeigen und ändern können, die Sie erstellt haben oder Ihnen zugewiesen sind.
- Verwenden Sie HTTPS für Anmeldeseiten und Authentifizierungscookies.
- Geben Sie ein Zeitlimit für Authentifizierungscookies an.

### <a name="input-validation"></a>Eingabeüberprüfung

Im Allgemeinen würde eine Produktions-App mehr Eingabeüberprüfung als die Fix It-App. Beispielsweise sollte die Bildgröße / Bilddateigröße, die für den Upload zulässig ist, begrenzt werden.

### <a name="administrator-functionality"></a>Administratorfunktionalität

Ein Administrator sollte in der Lage sein, den Besitz für vorhandene Aufgaben zu ändern. Beispielsweise kann der Ersteller einer Aufgabe das Unternehmen verlassen, sodass niemand über die Berechtigung verfügt, die Aufgabe zu verwalten, es sei denn, der Administratorzugriff ist aktiviert.

### <a name="queue-message-processing"></a>Warteschlangen-Nachrichtenverarbeitung

Die Warteschlangennachrichtenverarbeitung in der Fix It-App wurde so konzipiert, dass sie einfach ist, um das warteschlangenzentrierte Arbeitsmuster mit einer minimalen Menge an Code zu veranschaulichen. Dieser einfache Code wäre für eine tatsächliche Produktionsanwendung nicht ausreichend.

- Der Code garantiert nicht, dass jede Warteschlangennachricht höchstens einmal verarbeitet wird. Wenn Sie eine Nachricht aus der Warteschlange erhalten, gibt es einen Timeoutzeitraum, in dem die Nachricht für andere Listener unsichtbar ist. Wenn das Timeout abläuft, bevor die Nachricht gelöscht wird, wird die Nachricht wieder sichtbar. Wenn eine Workerrolleninstanz eine lange Zeit mit der Verarbeitung einer Nachricht verbringt, ist es theoretisch möglich, dass dieselbe Nachricht zweimal verarbeitet wird, was zu einer doppelten Aufgabe in der Datenbank führt. Weitere Informationen zu diesem Problem finden Sie unter [Verwenden von Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).
- Die Warteschlangenabfragelogik könnte kostengünstiger sein, indem sie den Nachrichtenabruf mit batching. Jedes Mal, wenn Sie [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)aufrufen, entstehen Transaktionskosten. Stattdessen können Sie [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (beachten Sie den Plural 's') aufrufen, der mehrere Nachrichten in einer einzigen Transaktion abruft. Die Transaktionskosten für Azure Storage Queues sind sehr gering, sodass die Auswirkungen auf die Kosten in den meisten Szenarien nicht erheblich sind.
- Die enge Schleife im Warteschlangen-Nachrichtenverarbeitungscode verursacht EINE CPU-Affinität, die Multi-Core-VMs nicht effizient nutzt. Ein besseres Design würde die Taskparallelität verwenden, um mehrere asynchrone Aufgaben parallel auszuführen.
- Die Warteschlangennachrichtenverarbeitung verfügt nur über eine rudimentäre Ausnahmebehandlung. Der Code verarbeitet z. B. keine [Giftnachrichten](https://msdn.microsoft.com/library/ms789028.aspx). (Wenn die Nachrichtenverarbeitung eine Ausnahme verursacht, müssen Sie den Fehler protokollieren und die Nachricht löschen, oder die Workerrolle versucht, sie erneut zu verarbeiten, und die Schleife wird auf unbestimmte Zeit fortgesetzt.)

### <a name="sql-queries-are-unbounded"></a>SQL-Abfragen sind ungebunden

Der aktuelle Fix It-Code setzt keine Begrenzung, wie viele Zeilen die Abfragen für Indexseiten zurückgeben können. Wenn eine große Anzahl von Aufgaben in die Datenbank eingegeben wird, kann die Größe der resultierenden empfangenen Listen Leistungsprobleme verursachen. Die Lösung besteht darin, Paging zu implementieren. Ein Beispiel finden Sie unter [Sortieren, Filtern und Paging mit entity Framework in einer ASP.NET MVC-Anwendung](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).

### <a name="view-models-recommended"></a>Modelle anzeigen empfohlen

Die Fix It-App verwendet die FixItTask-Entitätsklasse, um Informationen zwischen dem Controller und der Ansicht zu übergeben. Eine bewährte Methode besteht darin, Ansichtsmodelle zu verwenden. Das Domänenmodell (z. B. die FixItTask-Entitätsklasse) basiert auf dem, was für die Datenpersistenz erforderlich ist, während ein Ansichtsmodell für die Datendarstellung entworfen werden kann. Weitere Informationen finden Sie unter [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).

### <a name="secure-image-blob-recommended"></a>Sicheres Bildblob empfohlen

Die Fix It App speichert hochgeladene Bilder als öffentlich, was bedeutet, dass jeder, der die URL findet, auf die Bilder zugreifen kann. Die Bilder konnten statt öffentlich gesichert werden.

### <a name="no-powershell-automation-scripts-for-queues"></a>Keine PowerShell-Automatisierungsskripts für Warteschlangen

PowerShell-Automatisierungsskripts wurden nur für die Basisversion von Fix It geschrieben, die vollständig in Azure App Service Web Apps ausgeführt wird. Wir haben keine Skripts zum Einrichten und Bereitstellen in der Web-App sowie zur Cloud Service-Umgebung bereitgestellt, die für die Warteschlangenverarbeitung erforderlich ist.

### <a name="special-handling-for-html-codes-in-user-input"></a>Spezielle Handhabung von HTML-Codes in der Benutzereingabe

ASP.NET verhindert automatisch viele Möglichkeiten, wie böswillige Benutzer siteübergreifende Skriptangriffe versuchen können, indem sie Skripts in Benutzereingabetextfelder eingeben. Und der `DisplayFor` MVC-Helfer, der zum Anzeigen von Aufgabentiteln verwendet wird, und Notizen automatisch HTML-kodiert Werte, die er an den Browser sendet. Aber in einer Produktions-App sollten Sie zusätzliche Maßnahmen ergreifen. Weitere Informationen finden Sie unter [Anforderungsvalidierung in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).

<a id="bestpractices"></a>
## <a name="best-practices"></a>Bewährte Methoden

Im Folgenden sind einige Probleme, die behoben wurden, nachdem sie in der Codeüberprüfung und testen der ursprünglichen Version der Fix It-App entdeckt wurden. Einige wurden dadurch verursacht, dass der ursprüngliche Programmierer keine Kenntnis von einer bestimmten Best Practice hatte, andere einfach, weil der Code schnell geschrieben wurde und nicht für veröffentlichte Software gedacht war. Wir listen die Probleme hier auf, falls es etwas gibt, das wir aus dieser Überprüfung und Tests gelernt haben, das für andere hilfreich sein könnte, die auch Web-Apps entwickeln.

### <a name="dispose-the-database-repository"></a>Entsorgen des Datenbank-Repositorys

Die `FixItTaskRepository` Klasse muss die `DbContext` Entity Framework-Instanz entsorgen. Wir haben dies `FixItTaskRepository` getan, indem wir in der Klasse implementiert `IDisposable` haben:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

Beachten Sie, dass AutoFac die `FixItTaskRepository` Instance automatisch entsorgt, sodass wir sie nicht explizit entsorgen müssen.

Eine weitere Möglichkeit `DbContext` besteht darin, die Membervariable aus `FixItTaskRepository`zu entfernen und stattdessen eine lokale `DbContext` Variable innerhalb jeder Repository-Methode innerhalb einer `using` Anweisung zu erstellen. Beispiel:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Singletons als solche mit DI registrieren

Da nur eine `PhotoService` Instanz `Logger` der Klasse und Klasse erforderlich ist, sollten diese Klassen [als einzelne Instanzen für die Abhängigkeitsinjektion](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*registriert werden:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Sicherheit: Keine Fehlerdetails für Benutzer anzeigen

Die ursprüngliche Fix It-App hatte keine generische Fehlerseite und ließ einfach alle Ausnahmen auf die Benutzeroberfläche blasen, sodass einige Ausnahmen, wie z. B. Datenbankverbindungsfehler, dazu führen können, dass eine vollständige Stapelablaufverfolgung im Browser angezeigt wird. Detaillierte Fehlerinformationen können manchmal Angriffe böswilliger Benutzer erleichtern. Die Lösung besteht darin, die Ausnahmedetails zu protokollieren und dem Benutzer eine Fehlerseite anzuzeigen, die keine Fehlerdetails enthält. Die Fix It-App wurde bereits protokolliert, und um `<customErrors mode=On>` eine Fehlerseite anzuzeigen, haben wir in der Datei Web.config hinzugefügt.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Standardmäßig wird dadurch *die Ansicht s.Shared-Error.cshtml* für Fehler angezeigt. Sie können *Error.cshtml* anpassen oder eine eigene `defaultRedirect` Fehlerseitenansicht erstellen und ein Attribut hinzufügen. Sie können auch verschiedene Fehlerseiten für bestimmte Fehler angeben.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Sicherheit: Nur zulassen, dass eine Aufgabe von ihrem Ersteller bearbeitet wird

Auf der Seite Dashboardindex werden nur Vom angemeldeten Benutzer erstellte Aufgaben angezeigt, aber ein böswilliger Benutzer kann eine URL mit einer ID für die Aufgabe eines anderen Benutzers erstellen. Wir haben Code in *DashboardController.cs* hinzugefügt, um in diesem Fall eine 404 zurückzugeben:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>Schlucken Sie keine Ausnahmen

Die ursprüngliche Fix It-App hat gerade null zurückgegeben, nachdem eine Ausnahme protokolliert wurde, die aus einer SQL-Abfrage resultierte:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

Dadurch wird es für den Benutzer so aussehen, als ob die Abfrage erfolgreich war, aber einfach keine Zeilen zurückgegeben hat. Die Lösung besteht darin, die Ausnahme nach dem Abfangen und Protokollieren erneut auszulösen:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Alle Ausnahmen in Workerrollen abfangen

Alle nicht behandelten Ausnahmen in einer Workerrolle führen dazu, dass die VM wiederverwendet wird, sodass Sie alles, was Sie tun, in einem Try-Catch-Block umschließen und alle Ausnahmen behandeln möchten.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Länge für Zeichenfolgeneigenschaften in Entitätsklassen angeben

Um einfachen Code anzuzeigen, hat die ursprüngliche Version der Fix It-App keine Längen für die Felder der FixItTask-Entität angegeben, und als Ergebnis wurden sie in der Datenbank als varchar(max) definiert. Infolgedessen würde die Benutzeroberfläche fast jede Menge von Eingaben akzeptieren. Durch das Festlegen von Längen werden Grenzwerte festgelegt, die sowohl für Benutzereingaben in der Webseite als auch für die Spaltengröße in der Datenbank gelten:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Markieren Sie private Mitglieder als schreibgeschützt, wenn keine Änderung erwartet wird

In der `DashboardController` Klasse wird z. B. eine Instanz von `FixItTaskRepository` erstellt und es wird nicht erwartet, dass sie sich ändert, daher haben wir sie als [schreibgeschützt](https://msdn.microsoft.com/library/acdd6hb7.aspx)definiert.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Liste verwenden. Any() statt Liste. Zählen() &gt; 0

Wenn Ihnen nur wichtig ist, ob ein oder mehrere Elemente in einer Liste den angegebenen Kriterien entsprechen, verwenden Sie die `Count` Any-Methode, da sie zurückgegeben wird, sobald ein Element gefunden wird, das den Kriterien entspricht, während die Methode immer jedes Element durchlaufen muss. [Any](https://msdn.microsoft.com/library/bb534972.aspx) Die Datei Dashboard *Index.cshtml* hatte ursprünglich folgenden Code:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Wir haben es geändert:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>Generieren von URLs in MVC-Ansichten mithilfe von MVC-Hilfsprogrammen

Für die Schaltfläche **"Fix It erstellen"** auf der Startseite hat die Fix It-App ein Ankerelement hart codiert:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

Für View/Action-Links wie diesen ist es besser, den [URL.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML-Helfer zu verwenden, zum Beispiel:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Verwenden von Task.Delay anstelle von Thread.Sleep in der Workerrolle

Die Vorlage für `Thread.Sleep` das neue Projekt fügt den Beispielcode für eine Workerrolle ein, aber wenn der Thread in den Ruhezustand versetzt wird, kann der Threadpool zusätzliche unnötige Threads auslösen. Sie können dies vermeiden, indem Sie stattdessen [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) verwenden.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Vermeiden Sie asynchrone Void

Wenn eine async-Methode keinen Wert zurückgeben muss, geben Sie einen `Task` Typ anstelle `void`von zurück.

Dieses Beispiel stammt `FixItQueueManager` aus der Klasse:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

Sie sollten `async void` nur für Ereignishandler der obersten Ebene verwendet werden. Wenn Sie eine `async void`Methode als definieren, kann der Aufrufer nicht auf die Methode **warten** oder Ausnahmen abfangen, die die Methode auslöst. Weitere Informationen finden Sie unter [Best Practices in Asynchrone Programmierung](https://msdn.microsoft.com/magazine/jj991977.aspx).

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>Verwenden eines Abbruchtokens zum Unterbrechen der Workerrollenschleife

In der Regel enthält die **Run-Methode** für eine Workerrolle eine Endlosschleife. Wenn die Workerrolle beendet wird, wird die [RoleEntryPoint.OnStop-Methode](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) aufgerufen. Sie sollten diese Methode verwenden, um die Arbeit, die innerhalb der **Run-Methode** ausgeführt wird, abzubrechen und ordnungsgemäß zu beenden. Andernfalls kann der Prozess mitten in einem Vorgang beendet werden.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Opt-out von automatischem MIME-Sniffing-Verfahren

In einigen Fällen meldet Internet Explorer einen MIME-Typ, der sich von dem vom Webserver angegebenen Typ unterscheidet. Wenn Internet Explorer beispielsweise HTML-Inhalte in einer Datei findet, die mit dem HTTP-Antwortheader Content-Type: text/plain übermittelt wird, bestimmt Internet Explorer, dass der Inhalt als HTML gerendert werden soll. Leider kann dieses "MIME-Sniffing" auch zu Sicherheitsproblemen für Server führen, die nicht vertrauenswürdige Inhalte hosten. Um dieses Problem zu bekämpfen, hat Internet Explorer 8 eine Reihe von Änderungen am MIME-Typ-Bestimmungscode vorgenommen und ermöglicht es Anwendungsentwicklern, [sich von MIME-Sniffing abzumelden.](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx) Der folgende Code wurde der Datei *Web.config* hinzugefügt.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Bündelung und Minierung ermöglichen

Wenn Visual Studio ein neues Webprojekt erstellt, ist die Bündelung und Minifizierung von JavaScript-Dateien standardmäßig nicht aktiviert. Wir haben eine Codezeile in BundleConfig.cs hinzugefügt:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Festlegen eines Ablauftimeouts für Authentifizierungscookies

Standardmäßig laufen Authentifizierungscookies in zwei Wochen ab. Eine kürzere Zeit ist sicherer. Sie können diese Einstellung in *StartupAuth.cs*ändern:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>So führen Sie die App von Visual Studio aus auf Ihrem lokalen Computer aus

Es gibt zwei Möglichkeiten, die Fix It-App auszuführen:

- Führen Sie die Basisanwendung aus, die neue Aufgaben direkt in die SQL-Datenbank schreibt.
- Führen Sie die Anwendung mit einer Warteschlange plus einem Back-End-Dienst aus, um Aufgaben zu erstellen. Das Warteschlangenmuster wird im Kapitel [Queue-Centric Work Pattern](queue-centric-work-pattern.md)beschrieben.

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Ausführen der Basisanwendung

1. Installieren Sie [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. Installieren Sie das [Azure SDK für .NET für Visual Studio](https://azure.microsoft.com/downloads/).
3. Laden Sie die ZIP-Datei aus der [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)herunter.
4. Klicken Sie im Datei-Explorer mit der rechten Maustaste auf die ZIP-Datei, und klicken Sie auf Eigenschaften, und klicken Sie dann im Eigenschaftenfenster auf Entsperren.
5. Entpacken Sie die Datei.
6. Doppelklicken Sie auf die .sln-Datei, um Visual Studio zu starten.
7. Klicken Sie im Menü **Extras** auf **NuGet Package Manager**und dann auf **Package Manager Console**.
8. Klicken Sie in der Package Manager Console (PMC) auf Wiederherstellen.
9. Beenden Sie Visual Studio.
10. Starten Sie den [Azure-Speicheremulator](/azure/storage/common/storage-use-emulator).
11. Starten Sie Visual Studio neu, und öffnen Sie die Projektmappendatei, die Sie im vorherigen Schritt geschlossen haben.
12. Stellen Sie sicher, dass das FixIt-Projekt als Startprojekt festgelegt ist, und drücken Sie dann STRG+F5, um das Projekt auszuführen.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Ausführen der Anwendung mit Warteschlangenverarbeitung

1. Folgen Sie den Anweisungen zum [Ausführen der Basisanwendung](#runbase), schließen Sie dann den Browser, und schließen Sie Visual Studio.
2. Starten Sie Visual Studio mit Administratorrechten. (Sie verwenden den Azure-Computeemulator, und das erfordert Administratorrechte.)
3. Ändern Sie in der Datei *Web.config* im *MyFixIt-Projekt* `appSettings/UseQueues` (dem Webprojekt) den Wert von "true":

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Wenn der [Azure-Speicheremulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) noch nicht ausgeführt wird, starten Sie ihn erneut.
5. Führen Sie das FixIt-Webprojekt und das MyFixItCloudService-Projekt gleichzeitig aus.

    Verwenden von Visual Studio:

   1. Drücken Sie **F5,** um das FixIt-Projekt auszuführen.
   2. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das MyFixItCloudService-Projekt, und klicken Sie dann auf Neue**Instanz starten** **debuggen** > .

    Verwenden von Visual Studio 2013 Express für Web:

   3. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die FixIt-Lösung, und wählen Sie **Eigenschaften**aus.
   4. Wählen Sie **Mehrere Startprojekte**aus.
   5. Wählen Sie in der Dropdown-Liste **Aktion** unter MyFixIt und MyFixItCloudService die Option **Start**aus.
   6. Klicken Sie auf **OK**.
   7. Drücken Sie **F5**, um beide Projekte auszuführen.

      Wenn Sie das MyFixItCloudService-Projekt ausführen, startet Visual Studio den Azure-Computeemulator. Je nach Firewallkonfiguration müssen Sie den Emulator möglicherweise über die Firewall zulassen.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Bereitstellen der Basis-App in Azure App Service-Web-Apps mithilfe der Windows PowerShell-Skripts

Zur Veranschaulichung des [Musters "Alles automatisieren"](automate-everything.md) wird die Fix It-App mit Skripts bereitgestellt, die eine Umgebung in Azure einrichten und das Projekt in der neuen Umgebung bereitstellen. In den folgenden Anweisungen wird erläutert, wie die Skripts verwendet werden.

Wenn Sie in Azure ohne Warteschlangen ausgeführt werden möchten und die Änderungen vorgenommen haben, um lokal mit Warteschlangen ausgeführt zu werden, stellen Sie sicher, dass Sie den Wert UseQueues appSetting wieder auf false setzen, bevor Sie mit den folgenden Anweisungen fortfahren.

In diesen Anweisungen wird davon ausgegangen, dass Sie die Fix It-Lösung bereits lokal heruntergeladen und ausgeführt haben und dass Sie über ein Azure-Konto oder ein Azure-Abonnement verfügen, für das Sie berechtigt sind.

1. Installieren Sie die **Azure PowerShell-Konsole.** Anweisungen hierzu finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).

    Diese angepasste Konsole ist für die Arbeit mit Ihrem Azure-Abonnement konfiguriert. Das Azure-Modul wird im *Verzeichnis "Programmdateien"* installiert und bei jeder Verwendung der Azure PowerShell-Konsole automatisch importiert.

    Wenn Sie lieber in einem anderen Hostprogramm arbeiten möchten, z. B. Windows PowerShell ISE, verwenden Sie das [Cmdlet Import-Modul,](https://go.microsoft.com/fwlink/?LinkID=141553) um das Azure-Modul zu importieren, oder verwenden Sie einen Befehl im Azure-Modul, um den automatischen Import des Moduls auszulösen.
2. Starten Sie Azure PowerShell mit der Option **Als Administrator ausführen.**
3. Führen Sie das [Cmdlet Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) aus, `RemoteSigned`um die Azure PowerShell-Ausführungsrichtlinie auf festzulegen. Geben Sie **Y** (für Ja) ein, um die Richtlinienänderung abzuschließen.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Mit dieser Einstellung können Sie lokale Skripts ausführen, die nicht digital signiert sind. (Sie können die Ausführungsrichtlinie auch auf `Unrestricted`festlegen, wodurch der Schritt "Entsperren" später entfallen würde, dies wird jedoch aus Sicherheitsgründen nicht empfohlen.)
4. Führen `Add-AzureAccount` Sie das Cmdlet aus, um PowerShell mit Anmeldeinformationen für Ihr Konto einzurichten.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Diese Anmeldeinformationen laufen nach einer gewissen Zeit ab `Add-AzureAccount` und Sie müssen das Cmdlet erneut ausführen. Da dieses E-Book geschrieben wird, beträgt die Frist bis zum Ablauf der Anmeldeinformationen 12 Stunden.
5. Wenn Sie über mehrere Abonnements verfügen, geben Sie mit dem Cmdlet Select-AzureSubscription das Abonnement an, in dem Sie die Testumgebung erstellen möchten.
6. Importieren Sie ein Verwaltungszertifikat für dasselbe Azure-Abonnement mithilfe von `Get-AzurePublishSettingsFile` und `Import-AzurePublishSettingsFile` cmdlets. Das erste dieser Cmdlets lädt eine Zertifikatdatei herunter, und in der zweiten geben Sie den Speicherort dieser Datei an, um sie zu importieren. > [!IMPORTANT]
   > Bewahren Sie die heruntergeladene Datei an einem sicheren Speicherort auf, oder löschen Sie sie, wenn Sie damit fertig sind, da sie ein Zertifikat enthält, das zum Verwalten Ihrer Azure-Dienste verwendet werden kann.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    Das Zertifikat wird für einen REST-API-Aufruf verwendet, der die IP-Adresse des Entwicklungscomputers erkennt, um eine Firewallregel auf dem SQL-Datenbankserver festzulegen.
7. Führen Sie das [Cmdlet Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) (Aliase sind `cd`, `chdir`, und `sl`) aus, um zu dem Verzeichnis zu navigieren, das die Skripts enthält. (Sie befinden sich im *Ordner "Automatisierung"* im Ordner Fix It-Lösung.) Setzen Sie den Pfad in Anführungszeichen, wenn einer der Verzeichnisnamen Leerzeichen enthält. Um beispielsweise zum `c:\Sample Apps\FixIt\Automation` Verzeichnis zu navigieren, können Sie den folgenden Befehl eingeben:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Damit Windows PowerShell diese Skripts ausführen kann, verwenden Sie das Cmdlet ["Unblock-File".](https://go.microsoft.com/fwlink/p/?linkid=294021) (Die Skripts werden blockiert, weil sie aus dem Internet heruntergeladen wurden.)

    > [!WARNING]
    > Sicherheit: Bevor `Unblock-File` Sie für ein Skript oder eine ausführbare Datei ausgeführt werden, öffnen Sie die Datei in Notepad, überprüfen Sie die Befehle, und stellen Sie sicher, dass sie keinen schädlichen Code enthalten.

    Der folgende Befehl führt `Unblock-File` z. B. das Cmdlet für alle Skripts im aktuellen Verzeichnis aus.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Um die Web-App für die Basis zu erstellen (keine Warteschlangenverarbeitung) Fix It-App, führen Sie das Skript zum Erstellen der Umgebung aus.

    Der `Name` erforderliche Parameter gibt den Namen der Datenbank an und wird auch für das Speicherkonto verwendet, das das Skript erstellt. Der Name muss innerhalb der azurewebsites.net-Domäne global eindeutig sein. Wenn Sie einen Namen angeben, der nicht eindeutig ist, z. B. Fixit `New-AzureWebsite` oder Test (oder sogar wie im Beispiel fixitdemo), schlägt das Cmdlet mit einem internen Fehler fehl, der einen Konflikt meldet. Das Skript konvertiert den Namen in alle Kleinbuchstaben, um die Namensanforderungen für Web-Apps, Speicherkonten und Datenbanken zu erfüllen.

    Der `SqlDatabasePassword` erforderliche Parameter gibt das Kennwort für das Administratorkonto an, das für SQL-Datenbank erstellt wird. Schließen Sie keine speziellen XML-Zeichen&amp; &lt; &gt; in das Kennwort ein (;). Dies ist eine Einschränkung der Art und Weise, wie die Skripts geschrieben wurden, und keine Einschränkung von Azure.

    Wenn Sie beispielsweise eine Web-App mit dem Namen "fixitdemo" erstellen und ein SQL Server-Administratorkennwort von "Passw0rd1" verwenden möchten, können Sie den folgenden Befehl eingeben:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Der Name muss in der azurewebsites.net Domäne eindeutig sein, und das Kennwort muss die SQL-Datenbankanforderungen für die Kennwortkomplexität erfüllen. (Das Beispiel Passw0rd1 erfüllt die Anforderungen.)

    Beachten Sie, dass der Befehl mit ". \". Um böswillige Ausführung von Skripts zu verhindern, erfordert Windows PowerShell, dass Sie beim Ausführen eines Skripts den vollqualifizierten Pfad zur Skriptdatei angeben. Sie können einen Punkt verwenden, um\"das aktuelle Verzeichnis anzugeben (". ) oder stellen Sie den vollqualifizierten Pfad bereit, z. B.:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Weitere Informationen zum Skript finden `Get-Help` Sie im Cmdlet.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Sie können `Detailed`die `Full` `Parameters`Parameter `Examples` , , und Parameter des Get-Help-Cmdlets verwenden, um die zurückgegebene Hilfe zu filtern.

    Wenn das Skript fehlschlägt oder Fehler generiert, z. B. "New-AzureWebsite : Call Set-AzureSubscription und Select-AzureSubscription first", haben Sie die Konfiguration von Azure PowerShell möglicherweise nicht abgeschlossen.

    Nachdem das Skript abgeschlossen ist, können Sie das Azure-Verwaltungsportal verwenden, um die Ressourcen anzuzeigen, die erstellt wurden, wie im Kapitel ["Alles automatisieren"](automate-everything.md) gezeigt.
10. Verwenden Sie das *AzureWebsite.ps1-Skript,* um das FixIt-Projekt in der neuen Azure-Umgebung bereitzustellen. Beispiel:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Wenn die Bereitstellung abgeschlossen ist, wird der Browser geöffnet, wobei Fix It in Azure ausgeführt wird.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Fehlerbehebung bei windows PowerShell-Skripts

Die häufigsten Fehler beim Ausführen dieser Skripts beziehen sich auf Berechtigungen. Stellen Sie `Add-AzureAccount` `Import-AzurePublishSettingsFile` sicher, dass und waren erfolgreich, und dass Sie sie für dasselbe Azure-Abonnement verwendet haben. Selbst `Add-AzureAccount` wenn sie erfolgreich war, müssen Sie es möglicherweise erneut ausführen. Die durch `Add-AzureAccount` Ablauf in 12 Stunden hinzugefügten Berechtigungen.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>Objektverweis nicht auf eine Instanz eines Objekts festgelegt.

Wenn das Skript Fehler zurückgibt, z. B. "Objektreferenz ist nicht auf eine Instanz eines Objekts festgelegt", was bedeutet, `Add-AzureAccount` dass Windows PowerShell kein zu verarbeitendes Objekt finden kann (dies ist eine Nullverweisausnahme), führen Sie das Cmdlet aus, und versuchen Sie es erneut.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: Auf dem Server ist ein interner Fehler aufgetreten.

Das `New-AzureWebsite` Cmdlet gibt einen internen Fehler zurück, wenn der Name in der Domäne azurewebsites.net nicht eindeutig ist. Um den Fehler zu beheben, verwenden Sie einen anderen Wert für den Namen, der sich im Name-Parameter *von New-AzureWebsiteEnv.ps1*befindet.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Neustart des Skripts

Wenn Sie das Skript *New-AzureWebsiteEnv.ps1* neu starten müssen, weil es fehlgeschlagen ist, bevor es die Meldung "Skript ist abgeschlossen" gedruckt hat, können Sie Ressourcen löschen, die das Skript vor dem Beenden erstellt hat. Wenn das Skript beispielsweise bereits die ContosoFixItDemo-Web-App erstellt hat und Sie das Skript erneut mit demselben Namen ausführen, schlägt das Skript fehl, da der Name verwendet wird.

Um zu bestimmen, welche Ressourcen das Skript vor dem Stopp erstellt hat, verwenden Sie die folgenden Cmdlets:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Um dieses Cmdlet auszuführen, leiten `Get-AzureSqlDatabase`Sie den Datenbankservernamen an:`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

Um diese Ressourcen zu löschen, verwenden Sie die folgenden Befehle. Beachten Sie, dass Sie beim Löschen des Datenbankservers automatisch die datenbanken löschen, die dem Server zugeordnet sind.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Bereitstellen der App mit Warteschlangenverarbeitung in Azure App Service-Web-Apps und einem Azure Cloud Service

Um Warteschlangen zu aktivieren, nehmen Sie die folgende Änderung in der Datei MyFixIt-Web.config vor. Unter `appSettings`ändern Sie `UseQueues` den Wert von in "true":

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Stellen Sie dann die MVC-Anwendung in einer Web-App in Azure App Service bereit, wie [zuvor](#deploybase)beschrieben .

Erstellen Sie als Nächstes einen neuen Azure-Clouddienst. Die in der Fix It-App enthaltenen Skripts erstellen oder stellen den Clouddienst nicht bereit, daher müssen Sie dafür das Azure-Portal verwenden. Klicken Sie im Portal auf **Neue** -- **Berechnung** – Cloud**Service-Schnellerstellung** **Cloud Service** -- , und geben Sie dann eine URL und einen Rechenzentrumsspeicherort ein. Verwenden Sie dasselbe Rechenzentrum, in dem Sie die Web-App bereitgestellt haben.

![](the-fix-it-sample-application/_static/image1.png)

Bevor Sie den Clouddienst bereitstellen können, müssen Sie einige der Konfigurationsdateien aktualisieren.

Ersetzen Sie unter `connectionStrings`unter den Wert der `appdb` Verbindungszeichenfolge durch die tatsächliche Verbindungszeichenfolge für die SQL-Datenbank. Sie können die Verbindungszeichenfolge aus dem Portal abrufen. Klicken Sie im Portal auf **SQL-Datenbanken** - **appdb** - **SQL-Datenbankverbindungszeichenfolgen für ADO .Net, ODBC, PHP und JDBC**anzeigen. Kopieren Sie die ADO.NET Verbindungszeichenfolge, und fügen Sie den Wert in die Datei app.config ein. Ersetzen Sie\_das\_Kennwort "-Ihr-Kennwort hier" durch Ihr Datenbankkennwort. (Angenommen, Sie haben die Skripts zum Bereitstellen der MVC-App verwendet, geben Sie das Datenbankkennwort im `SqlDatabasePassword` Skriptparameter an.)

Das Ergebnis sollte wie folgt aussehen:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

Ersetzen Sie unter `appSettings`die beiden Platzhalterwerte für das Azure-Speicherkonto.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Sie können den Zugriffsschlüssel über das Portal abrufen. Weitere Informationen [zum Verwalten von Speicherkonten](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

Ersetzen Sie in MyFixItCloudService-ServiceConfiguration.Cloud.cscfg dieselben zwei Platzhalterwerte für das Azure-Speicherkonto.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Jetzt können Sie den Clouddienst bereitstellen. Klicken Sie in Lösungsumgebung mit der rechten Maustaste auf das MyFixItCloudService-Projekt, und wählen Sie **Veröffentlichen**aus. Weitere Informationen finden Sie unter["Bereitstellen der Anwendung in Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", der in Teil 2 dieses [Tutorials](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)enthalten ist.

> [!div class="step-by-step"]
> [Zurück](more-patterns-and-guidance.md)
