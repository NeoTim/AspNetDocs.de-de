---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Automatisierte Komponententests aktivieren | Microsoft Docs
author: rick-anderson
description: Schritt 12 zeigt, wie Sie eine Reihe von automatisierten Komponententests entwickeln, die unsere NerdDinner-Funktionalität überprüfen und uns das Vertrauen geben, Änderungen vorzunehmen...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541467"
---
# <a name="enable-automated-unit-testing"></a>Aktivieren von automatisierten Komponententests

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 12 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 12 zeigt, wie Sie eine Reihe von automatisierten Komponententests entwickeln, die unsere NerdDinner-Funktionalität überprüfen und uns das Vertrauen geben, in Zukunft Änderungen und Verbesserungen an der Anwendung vorzunehmen.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner Schritt 12: Komponententests

Lassen Sie uns eine Reihe von automatisierten Komponententests entwickeln, die unsere NerdDinner-Funktionalität überprüfen und uns das Vertrauen geben, in Zukunft Änderungen und Verbesserungen an der Anwendung vorzunehmen.

### <a name="why-unit-test"></a>Warum Komponententest?

Auf der Fahrt zur Arbeit eines Morgens haben Sie einen plötzlichen Blitz der Inspiration über eine Anwendung, an der Sie arbeiten. Sie erkennen, dass es eine Änderung gibt, die Sie implementieren können, die die Anwendung dramatisch verbessern wird. Es kann sich um eine Umgestaltung handelt, die den Code behebt, eine neue Funktion hinzufügt oder einen Fehler behebt.

Die Frage, die Sie konfrontiert, wenn Sie an Ihrem Computer ankommen, ist: "Wie sicher ist es, diese Verbesserung zu machen?" Was ist, wenn die Änderung Nebenwirkungen hat oder etwas bricht? Die Änderung ist möglicherweise einfach und dauert nur wenige Minuten, aber was ist, wenn es Stunden dauert, um alle Anwendungsszenarien manuell zu testen? Was passiert, wenn Sie vergessen, ein Szenario abzudecken und eine fehlerhafte Anwendung in die Produktion geht? Lohnt sich diese Verbesserung wirklich?

Automatisierte Komponententests können ein Sicherheitsnetz bieten, mit dem Sie Ihre Anwendungen kontinuierlich verbessern und keine Angst vor dem Code haben, an dem Sie arbeiten. Durch automatisierte Tests, die die Funktionalität schnell überprüfen, können Sie sicher programmieren – und Sie in die Lage versetzen, Verbesserungen vorzunehmen, die Sie sonst vielleicht nicht bequem gemacht hätten. Sie helfen auch, Lösungen zu schaffen, die besser bedienbar sind und eine längere Lebensdauer haben - was zu einer viel höheren Rendite führt.

Das ASP.NET MVC Framework macht es einfach und natürlich, die Anwendungsfunktionalität von Komponenten zu testen. Es ermöglicht auch einen TDD-Workflow (Test Driven Development), der die Test-First-basierte Entwicklung ermöglicht.

### <a name="nerddinnertests-project"></a>NerdDinner.Tests Projekt

Als wir unsere NerdDinner-Anwendung zu Beginn dieses Tutorials erstellt enden, wurden wir mit einem Dialog gefragt, ob wir ein Komponententestprojekt erstellen möchten, um mit dem Anwendungsprojekt zu gehen:

![](enable-automated-unit-testing/_static/image1.png)

Wir haben den "Ja, erstellen Sie ein Komponententestprojekt" ausgewählt – was dazu führte, dass ein "NerdDinner.Tests"-Projekt zu unserer Lösung hinzugefügt wurde:

![](enable-automated-unit-testing/_static/image2.png)

Das NerdDinner.Tests-Projekt verweist auf die NerdDinner-Anwendungsprojektassembly und ermöglicht es uns, ihm problemlos automatisierte Tests hinzuzufügen, die die Anwendungsfunktionalität überprüfen.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Erstellen von Komponententests für unsere Dinner-Modellklasse

Fügen wir unserem NerdDinner.Tests-Projekt einige Tests hinzu, die die Dinner-Klasse überprüfen, die wir beim Erstellen unserer Modellebene erstellt haben.

Wir beginnen mit der Erstellung eines neuen Ordners in unserem Testprojekt namens "Modelle", in dem wir unsere modellbezogenen Tests platzieren. Wir klicken dann mit der rechten Maustaste auf den Ordner und wählen den Befehl **&gt;"Neuer Test hinzufügen".** Dadurch wird das Dialogfeld "Neuer Test hinzufügen" angezeigt.

Wir erstellen einen "Komponententest" und nennen ihn "DinnerTest.cs":

![](enable-automated-unit-testing/_static/image3.png)

Wenn wir auf die Schaltfläche "OK" klicken, fügt Visual Studio dem Projekt eine DinnerTest.cs Datei hinzu (und öffnet sie):

![](enable-automated-unit-testing/_static/image4.png)

Die standardmäßige Visual Studio-Komponententestvorlage enthält eine Reihe von Kesselplattencodes, die ich ein wenig chaotisch finde. Lassen Sie uns es bereinigen, um nur den folgenden Code zu enthalten:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

Das [TestClass]-Attribut in der oben genannten DinnerTest-Klasse identifiziert es als Klasse, die Tests sowie optionalen Testinitialisierungs- und Teardowncode enthält. Wir können darin Tests definieren, indem wir öffentliche Methoden hinzufügen, auf denen ein [TestMethod]-Attribut enthalten ist.

Im Folgenden finden Sie den ersten von zwei Tests, die wir hinzufügen werden, dass unsere Dinner-Klasse trainieren. Der erste Test bestätigt, dass unser Dinner ungültig ist, wenn ein neues Dinner erstellt wird, ohne dass alle Eigenschaften richtig eingestellt werden. Der zweite Test bestätigt, ob unser Dinner gültig ist, wenn bei einem Dinner alle Eigenschaften mit gültigen Werten festgelegt wurden:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Sie werden oben feststellen, dass unsere Testnamen sehr explizit (und etwas ausführlich) sind. Wir tun dies, weil wir am Ende Hunderte oder Tausende von kleinen Tests erstellen könnten, und wir möchten es einfach machen, die Absicht und das Verhalten jedes einzelnen von ihnen schnell zu bestimmen (besonders, wenn wir eine Liste von Fehlern in einem Testläufer durchsehen). Die Testnamen sollten nach der Funktionalität benannt werden, die sie testen. Oben verwenden wir ein\_"Noun Should\_Verb" Namensmuster.

Wir strukturieren die Tests nach dem "AAA"-Testmuster – das steht für "Arrange, Act, Assert":

- Anordnen: Einrichten des zu testenden Geräts
- Akt: Übung der zu prüfenden Einheit und Erfassung der Ergebnisse
- Assert: Überprüfen des Verhaltens

Wenn wir Tests schreiben, wollen wir vermeiden, dass die einzelnen Tests zu viel tun. Stattdessen sollte jeder Test nur ein einziges Konzept überprüfen (was es viel einfacher macht, die Ursache von Fehlern zu ermitteln). Eine gute Richtlinie ist, zu versuchen, nur eine einzige Assertionsanweisung für jeden Test zu haben. Wenn Sie mehr als eine Assert-Anweisung in einer Testmethode haben, stellen Sie sicher, dass sie alle zum Testen desselben Konzepts verwendet werden. Machen Sie im Zweifelsfall einen weiteren Test.

### <a name="running-tests"></a>Tests werden ausgeführt

Visual Studio 2008 Professional (und höhere Editionen) enthält einen integrierten Testrunner, der zum Ausführen von Visual Studio Unit Test-Projekten innerhalb der IDE verwendet werden kann. Wir können den Menübefehl **Test-&gt;Run-&gt;All Tests in Solution** (oder Strg R, A) auswählen, um alle unsere Komponententests auszuführen. Alternativ können wir unseren Cursor innerhalb einer bestimmten Testklasse oder Testmethode positionieren und den Menübefehl **Test-&gt;Run-&gt;Tests in Current Context** (oder Typ Strg R, T) verwenden, um eine Teilmenge der Komponententests auszuführen.

Positionieren wir unseren Cursor innerhalb der DinnerTest-Klasse und geben Sie "Strg R, T" ein, um die beiden Tests auszuführen, die wir gerade definiert haben. Wenn wir dies tun, wird in Visual Studio ein Fenster "Testergebnisse" angezeigt, in dem die Ergebnisse unseres Testlaufs aufgeführt sind:

![](enable-automated-unit-testing/_static/image5.png)

*Hinweis: Im VS-Testergebnisfenster wird standardmäßig nicht die Spalte Klassenname angezeigt. Sie können dies hinzufügen, indem Sie im Fenster Testergebnisse mit der rechten Maustaste klicken und den Menübefehl Spalten hinzufügen/entfernen verwenden.*

Unsere beiden Tests dauerten nur einen Bruchteil einer Sekunde, um zu laufen – und wie Sie sehen können, bestanden sie beide. Wir können sie nun weiter ausführen und erweitern, indem wir zusätzliche Tests erstellen, die bestimmte Regelvalidierungen überprüfen und die beiden Hilfsmethoden - IsUserHost() und IsUserRegistered() – abdecken, die wir der Dinner-Klasse hinzugefügt haben. Mit all diesen Tests für die Dinner-Klasse wird es viel einfacher und sicherer, neue Geschäftsregeln und Validierungen hinzuzufügen. Wir können unsere neue Regellogik zu Dinner hinzufügen und dann innerhalb von Sekunden überprüfen, ob diese keine unserer vorherigen Logikfunktionen gebrochen hat.

Beachten Sie, wie die Verwendung eines beschreibenden Testnamens es einfach macht, schnell zu verstehen, was jeder Test überprüft. Ich empfehle, den Menübefehl **Extras-&gt;Optionen zu** verwenden, den Konfigurationsbildschirm Testwerkzeuge -&gt;Testausführung zu öffnen und das Kontrollkästchen "Doppelklicken auf ein fehlgeschlagenes oder nicht schlüssiges Komponententestergebnis" anzuzeigen, der den Fehlerpunkt im Test anzeigt. Auf diese Weise können Sie auf einen Fehler im Testergebnisfenster doppelklicken und sofort zum Assertionsfehler springen.

### <a name="creating-dinnerscontroller-unit-tests"></a>Erstellen von DinnersController-Komponententests

Lassen Sie uns nun einige Komponententests erstellen, die unsere DinnersController-Funktionalität überprüfen. Wir beginnen mit einem Rechtsklick auf den Ordner "Controller" in unserem Testprojekt und wählen dann den Menübefehl **&gt;"Neuer Test hinzufügen".** Wir erstellen einen "Einheitstest" und nennen ihn "DinnersControllerTest.cs".

Wir erstellen zwei Testmethoden, die die Aktionsmethode Details() auf dem DinnersController überprüfen. Die erste überprüft, ob eine Ansicht zurückgegeben wird, wenn ein vorhandenes Abendessen angefordert wird. Die zweite überprüft, ob eine "NotFound"-Ansicht zurückgegeben wird, wenn ein nicht vorhandenes Abendessen angefordert wird:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

Der obige Code kompiliert clean. Wenn wir die Tests ausführen, schlagen beide jedoch fehl:

![](enable-automated-unit-testing/_static/image6.png)

Wenn wir uns die Fehlermeldungen ansehen, werden wir feststellen, dass der Grund für den Fehler der Tests darin lag, dass unsere DinnersRepository-Klasse keine Verbindung mit einer Datenbank herstellen konnte. Unsere NerdDinner-Anwendung verwendet eine Verbindungszeichenfolge zu einer lokalen SQL Server\_Express-Datei, die sich unter dem Verzeichnis "App Data" des NerdDinner-Anwendungsprojekts befindet. Da unser NerdDinner.Tests-Projekt in einem anderen Verzeichnis als dem Anwendungsprojekt kompiliert und ausgeführt wird, ist der relative Pfadspeicherort unserer Verbindungszeichenfolge falsch.

Wir *könnten* dies beheben, indem wir die SQL Express-Datenbankdatei in unser Testprojekt kopieren und dann in der App.config unseres Testprojekts eine entsprechende Testverbindungszeichenfolge hinzufügen. Dadurch würden die oben genannten Tests aufgehoben und ausgeführt.

Komponententestcodes, die eine echte Datenbank verwenden, bringen jedoch eine Reihe von Herausforderungen mit sich. Dies gilt insbesondere in folgenden Fällen:

- Es verlangsamt die Ausführungszeit von Komponententests erheblich. Je länger es dauert, Tests auszuführen, desto geringer ist die Wahrscheinlichkeit, dass Sie sie häufig ausführen. Im Idealfall möchten Sie, dass Ihre Komponententests in Sekundenschnelle ausgeführt werden können – und sie so natürlich wie das Kompilieren des Projekts machen.
- Es erschwert die Einrichtungs- und Bereinigungslogik innerhalb von Tests. Sie möchten, dass jeder Komponententest isoliert und unabhängig von anderen ist (ohne Nebenwirkungen oder Abhängigkeiten). Wenn Sie mit einer echten Datenbank arbeiten, müssen Sie auf den Zustand achten und ihn zwischen den Tests zurücksetzen.

Sehen wir uns ein Entwurfsmuster namens "Abhängigkeitsinjektion" an, das uns helfen kann, diese Probleme zu umgehen und die Notwendigkeit zu vermeiden, eine echte Datenbank mit unseren Tests zu verwenden.

### <a name="dependency-injection"></a>Dependency Injection

Im Moment ist DinnersController eng mit der DinnerRepository-Klasse "gekoppelt". "Koppeln" bezieht sich auf eine Situation, in der eine Klasse explizit auf eine andere Klasse angewiesen ist, um zu arbeiten:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

Da die DinnerRepository-Klasse Zugriff auf eine Datenbank erfordert, erfordert die eng gekoppelte Abhängigkeit der DinnersController-Klasse vom DinnerRepository eine Datenbank, damit die DinnersController-Aktionsmethoden getestet werden können.

Wir können dies umgehen, indem wir ein Entwurfsmuster namens "Abhängigkeitsinjektion" verwenden – ein Ansatz, bei dem Abhängigkeiten (wie Repository-Klassen, die Datenzugriff bereitstellen) nicht mehr implizit innerhalb von Klassen erstellt werden, die sie verwenden. Stattdessen können Abhängigkeiten explizit an die Klasse übergeben werden, die sie mithilfe von Konstruktorargumenten verwendet. Wenn die Abhängigkeiten mithilfe von Schnittstellen definiert werden, haben wir die Flexibilität, "gefälschte" Abhängigkeitsimplementierungen für Komponententestszenarien zu übergeben. Auf diese Weise können wir testspezifische Abhängigkeitsimplementierungen erstellen, die eigentlich keinen Zugriff auf eine Datenbank erfordern.

Um dies in Aktion zu sehen, implementieren wir Abhängigkeitsinjektion mit unserem DinnersController.

#### <a name="extracting-an-idinnerrepository-interface"></a>Extrahieren einer IDinnerRepository-Schnittstelle

Unser erster Schritt wird darin bestehen, eine neue IDinnerRepository-Schnittstelle zu erstellen, die den Repository-Vertrag kapselt, den unsere Controller zum Abrufen und Aktualisieren von Dinners benötigen.

Wir können diesen Schnittstellenvertrag manuell definieren, indem wir mit der rechten Maustaste auf den Ordner "Modelle" klicken und dann den Menübefehl **&gt;"Neues Element hinzufügen"** auswählen und eine neue Schnittstelle mit dem Namen IDinnerRepository.cs erstellen.

Alternativ können wir die in Visual Studio Professional (und höheren Editionen) integrierten Umgestaltungstools verwenden, um automatisch eine Schnittstelle für uns aus unserer vorhandenen DinnerRepository-Klasse zu extrahieren und zu erstellen. Um diese Schnittstelle mit VS zu extrahieren, positionieren Sie einfach den Cursor im Texteditor in der DinnerRepository-Klasse, und klicken Sie dann mit der rechten Maustaste und wählen Sie den Menübefehl **"Refactor-&gt;Extract Interface":**

![](enable-automated-unit-testing/_static/image7.png)

Dadurch wird das Dialogfeld "Schnittstelle extrahieren" gestartet und wir werden aufgefordert, den Namen der zu erstellenden Schnittstelle zu erstellen. Es wird standardmäßig auf IDinnerRepository verwendet und wählt automatisch alle öffentlichen Methoden für die vorhandene DinnerRepository-Klasse aus, die der Schnittstelle hinzugefügt werden sollen:

![](enable-automated-unit-testing/_static/image8.png)

Wenn wir auf die Schaltfläche "OK" klicken, fügt Visual Studio unserer Anwendung eine neue IDinnerRepository-Schnittstelle hinzu:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

Und unsere bestehende DinnerRepository-Klasse wird aktualisiert, sodass sie die Schnittstelle implementiert:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>Aktualisieren von DinnersController zur Unterstützung der Konstruktorinjektion

Wir aktualisieren nun die DinnersController-Klasse, um die neue Schnittstelle zu verwenden.

Derzeit ist DinnersController so hartcodiert, dass das Feld "dinnerRepository" immer eine DinnerRepository-Klasse ist:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Wir ändern es so, dass das Feld "dinnerRepository" vom Typ IDinnerRepository anstelle von DinnerRepository ist. Wir fügen dann zwei öffentliche DinnersController-Konstruktoren hinzu. Einer der Konstruktoren ermöglicht das Übergeben eines IDinnerRepository als Argument. Der andere ist ein Standardkonstruktor, der unsere vorhandene DinnerRepository-Implementierung verwendet:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

Da ASP.NET MVC standardmäßig Controllerklassen mit Standardkonstruktoren erstellt, verwendet unser DinnersController zur Laufzeit weiterhin die DinnerRepository-Klasse, um datenzugriff durchzuführen.

Wir können nun jedoch unsere Komponententests aktualisieren, um eine "gefälschte" Dinner-Repository-Implementierung mit dem Parameterkonstruktor zu übergeben. Dieses "gefälschte" Dinner-Repository erfordert keinen Zugriff auf eine echte Datenbank und verwendet stattdessen In-Memory-Beispieldaten.

#### <a name="creating-the-fakedinnerrepository-class"></a>Erstellen der FakeDinnerRepository-Klasse

Erstellen wir eine FakeDinnerRepository-Klasse.

Wir beginnen mit der Erstellung eines "Fakes"-Verzeichnisses in unserem NerdDinner.Tests-Projekt und fügen dann eine neue FakeDinnerRepository-Klasse hinzu (mit der rechten Maustaste auf den Ordner klicken und **Add-&gt;New Class**auswählen):

![](enable-automated-unit-testing/_static/image9.png)

Wir aktualisieren den Code, sodass die FakeDinnerRepository-Klasse die IDinnerRepository-Schnittstelle implementiert. Wir können dann mit der rechten Maustaste darauf klicken und den Kontextmenübefehl "Implement interface IDinnerRepository" auswählen:

![](enable-automated-unit-testing/_static/image10.png)

Dies führt dazu, dass Visual Studio automatisch alle IDinnerRepository-Schnittstellenmember zu unserer FakeDinnerRepository-Klasse mit standardmäßigen "stub out"-Implementierungen hinzufügt:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Wir können dann die FakeDinnerRepository-Implementierung aktualisieren, um&lt;&gt; eine Speicherlisten-Dinner-Auflistung abzuarbeiten, die als Konstruktorargument an sie übergeben wurde:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Wir haben jetzt eine gefälschte IDinnerRepository-Implementierung, die keine Datenbank benötigt, und können stattdessen eine In-Memory-Liste von Dinner-Objekten ausarbeiten.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Verwenden des FakeDinnerRepository mit Komponententests

Kehren wir zu den DinnersController-Komponententests zurück, die zuvor fehlgeschlagen sind, da die Datenbank nicht verfügbar war. Wir können die Testmethoden aktualisieren, um ein FakeDinnerRepository zu verwenden, das mit Beispiel-In-Memory-Dinner-Daten auf dem DinnersController aufgefüllt wird, indem wir den folgenden Code verwenden:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

Und jetzt, wenn wir diese Tests ausführen, bestehen sie beide:

![](enable-automated-unit-testing/_static/image11.png)

Das Beste daran ist, dass sie nur einen Bruchteil einer Sekunde benötigen, um ausgeführt zu werden, und erfordern keine komplizierte Setup-/Bereinigungslogik. Wir können jetzt unseren gesamten DinnersController-Aktionsmethodencode (einschließlich Auflistung, Paging, Details, Erstellen, Aktualisieren und Löschen) testen, ohne jemals eine Verbindung zu einer echten Datenbank herstellen zu müssen.

| **Nebenthema: Dependency Injection Frameworks** |
| --- |
| Die manuelle Abhängigkeitsinjektion (wie oben) funktioniert gut, ist jedoch schwieriger zu verwalten, wenn die Anzahl der Abhängigkeiten und Komponenten in einer Anwendung zunimmt. Für .NET gibt es mehrere Abhängigkeitsinjektionsframeworks, die dazu beitragen können, noch mehr Flexibilität bei der Abhängigkeitsverwaltung zu bieten. Diese Frameworks, die manchmal auch als "Inversion of Control"(IoC)-Container bezeichnet werden, bieten Mechanismen, die eine zusätzliche Ebene der Konfigurationsunterstützung für das Angeben und Übergeben von Abhängigkeiten an Objekte zur Laufzeit ermöglichen (am häufigsten mithilfe der Konstruktorinjektion). Einige der beliebtesten OSS Dependency Injection / IOC Frameworks in .NET sind: AutoFac, Ninject, Spring.NET, StructureMap und Windsor. ASP.NET MVC macht Erweiterbarkeits-APIs verfügbar, die es Entwicklern ermöglichen, an der Auflösung und Instanziierung von Controllern teilzunehmen, und die es ermöglicht, Dependency Injection / IoC-Frameworks sauber in diesen Prozess zu integrieren. Die Verwendung eines DI/IOC-Frameworks würde es uns auch ermöglichen, den Standardkonstruktor aus unserem DinnersController zu entfernen – was die Kopplung zwischen dem DinnerRepository vollständig entfernen würde. Wir werden keine Abhängigkeitsinjektion / IOC-Framework mit unserer NerdDinner-Anwendung verwenden. Aber es ist etwas, das wir für die Zukunft in Betracht ziehen könnten, wenn die NerdDinner-Codebasis und die Funktionen wachsen würden. |

### <a name="creating-edit-action-unit-tests"></a>Erstellen von Edit Action Unit-Tests

Lassen Sie uns nun einige Komponententests erstellen, die die Edit-Funktionalität des DinnersControllers überprüfen. Wir beginnen mit dem Testen der HTTP-GET-Version unserer Edit-Aktion:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Wir erstellen einen Test, der überprüft, ob eine Ansicht, die von einem DinnerFormViewModel-Objekt unterstützt wird, wieder gerendert wird, wenn ein gültiges Abendessen angefordert wird:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Wenn wir den Test ausführen, werden wir jedoch feststellen, dass er fehlschlägt, da eine Nullverweisausnahme ausgelöst wird, wenn die Edit-Methode auf die User.Identity.Name-Eigenschaft zugreift, um die Dinner.IsHostedBy()-Prüfung durchzuführen.

Das User-Objekt in der Controller-Basisklasse kapselt Details über den angemeldeten Benutzer und wird von ASP.NET MVC aufgefüllt, wenn es den Controller zur Laufzeit erstellt. Da wir den DinnersController außerhalb einer Webserverumgebung testen, ist das User-Objekt nicht festgelegt (daher die Nullverweisausnahme).

### <a name="mocking-the-useridentityname-property"></a>Verspottung der User.Identity.Name-Eigenschaft

Mocking-Frameworks erleichtern das Testen, da wir dynamisch gefälschte Versionen abhängiger Objekte erstellen können, die unsere Tests unterstützen. Beispielsweise können wir in unserem Aktionstest Bearbeiten ein Mocking-Framework verwenden, um dynamisch ein User-Objekt zu erstellen, mit dem unser DinnersController einen simulierten Benutzernamen suchen kann. Dadurch wird verhindert, dass beim Ausführen des Tests ein Nullverweis ausgelöst wird.

Es gibt viele .NET-Mocking-Frameworks, die mit ASP.NET MVC verwendet [http://www.mockframeworks.com/](http://www.mockframeworks.com/)werden können (eine Liste davon finden Sie hier: ). Zum Testen unserer NerdDinner-Anwendung verwenden wir ein Open-Source-Mocking-Framework namens [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)"Moq", das kostenlos von heruntergeladen werden kann.

Nach dem Herunterladen fügen wir der Moq.dll-Assembly eine Referenz in unserem NerdDinner.Tests-Projekt hinzu:

![](enable-automated-unit-testing/_static/image12.png)

Anschließend fügen wir unserer Testklasse eine "CreateDinnersControllerAs(username)"-Hilfsmethode hinzu, die einen Benutzernamen als Parameter verwendet und dann die User.Identity.Name-Eigenschaft in der DinnersController-Instanz "verspottet":

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Oben verwenden wir Moq, um ein Mock-Objekt zu erstellen, das ein ControllerContext-Objekt fälscht (was ASP.NET MVC an Controller-Klassen übergibt, um Laufzeitobjekte wie Benutzer, Anforderung, Antwort und Sitzung verfügbar zu machen). Wir rufen die "SetupGet"-Methode auf dem Mock auf, um anzugeben, dass die HttpContext.User.Identity.Name-Eigenschaft in ControllerContext die Benutzername-Zeichenfolge zurückgeben soll, die wir an die Hilfsmethode übergeben haben.

Wir können eine beliebige Anzahl von ControllerContext-Eigenschaften und -Methoden verspotten. Um dies zu veranschaulichen, habe ich auch einen SetupGet()-Aufruf für die Request.IsAuthenticated-Eigenschaft hinzugefügt (die für die folgenden Tests nicht benötigt wird – aber sie hilft zu veranschaulichen, wie Sie Request-Eigenschaften verspotten können). Wenn wir fertig sind, weisen wir dem DinnersController eine Instanz des ControllerContext-Mocks zu, die unsere Hilfsmethode zurückgibt.

Wir können jetzt Komponententests schreiben, die diese Hilfsmethode verwenden, um Bearbeitungsszenarien zu testen, an denen verschiedene Benutzer beteiligt sind:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

Und jetzt, wenn wir die Tests ausführen, bestehen sie:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>Testen von UpdateModel()-Szenarien

Wir haben Tests erstellt, die die HTTP-GET-Version der Edit-Aktion abdecken. Lassen Sie uns nun einige Tests erstellen, die die HTTP-POST-Version der Edit-Aktion überprüfen:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

Das interessante neue Testszenario, das wir mit dieser Aktionsmethode unterstützen können, ist die Verwendung der UpdateModel()-Hilfsmethode in der Controller-Basisklasse. Wir verwenden diese Hilfsmethode, um Formular-Post-Werte an unsere Dinner-Objektinstanz zu binden.

Im Folgenden finden Sie zwei Tests, die zeigen, wie wir formulargepostete Werte für die zu verwendende UpdateModel()-Hilfsmethode bereitstellen können. Dazu erstellen und füllen wir ein FormCollection-Objekt aus, und weisen es dann der Eigenschaft "ValueProvider" auf dem Controller zu.

Der erste Test überprüft, ob bei einem erfolgreichen Speichern der Browser auf die Detailaktion umgeleitet wird. Der zweite Test überprüft, ob die Aktion beim Anzeigen ungültiger Eingaben die Bearbeitungsansicht erneut mit einer Fehlermeldung anzeigt.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Testen von Wrap-Up

Wir haben die Kernkonzepte von Komponententestcontrollerklassen behandelt. Wir können diese Techniken verwenden, um ganz einfach Hunderte von einfachen Tests zu erstellen, die das Verhalten unserer Anwendung überprüfen.

Da unsere Controller- und Modelltests keine echte Datenbank erfordern, sind sie extrem schnell und einfach auszuführen. Wir werden in der Lage sein, Hunderte von automatisierten Tests in Sekunden auszuführen und sofort Feedback zu erhalten, ob eine Änderung, die wir vorgenommen haben, etwas kaputt gemacht hat. Dies wird uns das Vertrauen geben, unsere Anwendung kontinuierlich zu verbessern, umzugestalten und zu verfeinern.

Wir haben das Testen als letztes Thema in diesem Kapitel behandelt – aber nicht, weil Sie am Ende eines Entwicklungsprozesses testen sollten! Im Gegenteil, Sie sollten automatisierte Tests so früh wie möglich in Ihrem Entwicklungsprozess schreiben. Auf diese Weise erhalten Sie sofortiges Feedback, während Sie sich entwickeln, hilft Ihnen, über die Anwendungsszenarien Ihrer Anwendung nachdenklich zu denken, und leitet Sie bei der Gestaltung Ihrer Anwendung mit Blick auf saubere Schichtung und Kopplung.

In einem späteren Kapitel des Buches wird Test Driven Development (TDD) erläutert und erläutert, wie sie mit ASP.NET MVC verwendet werden. TDD ist eine iterative Codierungspraxis, bei der Sie zuerst die Tests schreiben, die Ihr resultierender Code erfüllt. Mit TDD beginnen Sie mit jedem Feature, indem Sie einen Test erstellen, der die Funktionalität überprüft, die Sie implementieren möchten. Wenn Sie den Komponententest zuerst schreiben, können Sie das Feature und seine Funktionsweise klar verstehen. Erst nachdem der Test geschrieben wurde (und Sie haben überprüft, dass er fehlschlägt), implementieren Sie dann die tatsächliche Funktionalität, die der Test überprüft. Da Sie bereits zeitübersam über den Anwendungsfall nachgedacht haben, wie die Funktion funktionieren soll, haben Sie ein besseres Verständnis der Anforderungen und deren optimale Implementierung. Wenn Sie mit der Implementierung fertig sind, können Sie den Test erneut ausführen – und sofort Feedback erhalten, ob die Funktion korrekt funktioniert. Wir behandeln TDD mehr in Kapitel 10.

### <a name="next-step"></a>Nächster Schritt

Einige abschließende Wrap-Up-Kommentare.

> [!div class="step-by-step"]
> [Zurück](use-ajax-to-implement-mapping-scenarios.md)
> [Weiter](nerddinner-wrap-up.md)
