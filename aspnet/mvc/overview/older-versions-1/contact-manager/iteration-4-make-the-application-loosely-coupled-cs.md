---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 'Iteration #4 – Machen Sie die Anwendung lose gekoppelt | Microsoft Docs'
author: rick-anderson
description: In dieser vierten Iteration nutzen wir mehrere Softwareentwurfsmuster, um die Wartung und Änderung der Contact Manager-Anwendung zu vereinfachen. Für ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542364"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>Iteration 4 – Loses Koppeln der Anwendung (C#)

von [Microsoft](https://github.com/microsoft)

[Code herunterladen](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> In dieser vierten Iteration nutzen wir mehrere Softwareentwurfsmuster, um die Wartung und Änderung der Contact Manager-Anwendung zu vereinfachen. Beispielsweise gestalten wir unsere Anwendung so um, dass sie das Repository-Muster und das Abhängigkeitsinjektionsmuster verwendet.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Erstellen einer Kontaktverwaltungs-ASP.NET MVC-Anwendung (C-Anwendung)

In dieser Reihe von Tutorials erstellen wir eine gesamte Contact Management-Anwendung von Anfang bis Ende. Mit der Kontakt-Manager-Anwendung können Sie Kontaktinformationen - Namen, Telefonnummern und E-Mail-Adressen - für eine Personenliste speichern.

Wir erstellen die Anwendung über mehrere Iterationen. Mit jeder Iteration verbessern wir die Anwendung schrittweise. Das Ziel dieses Ansatzes mit mehreren Iterationen besteht darin, den Grund für jede Änderung zu verstehen.

- Iteration #1 - Erstellen Sie die Anwendung. In der ersten Iteration erstellen wir den Contact Manager auf einfachste Weise. Wir fügen Unterstützung für grundlegende Datenbankvorgänge hinzu: Erstellen, Lesen, Aktualisieren und Löschen (CRUD).

- Iteration #2 - Machen Sie die Anwendung schön aussehen. In dieser Iteration verbessern wir das Erscheinungsbild der Anwendung, indem wir die Standard-ASP.NET MVC-Ansichtsmasterseite und des kaskadierenden Stylesheets ändern.

- Iteration #3 - Formularüberprüfung hinzufügen. In der dritten Iteration fügen wir eine grundlegende Formularvalidierung hinzu. Wir verhindern, dass Personen ein Formular einreichen, ohne die erforderlichen Formularfelder ausfüllen zu müssen. Wir validieren auch E-Mail-Adressen und Telefonnummern.

- Iteration #4 - Machen Sie die Anwendung lose gekoppelt. In dieser vierten Iteration nutzen wir mehrere Softwareentwurfsmuster, um die Wartung und Änderung der Contact Manager-Anwendung zu vereinfachen. Beispielsweise gestalten wir unsere Anwendung so um, dass sie das Repository-Muster und das Abhängigkeitsinjektionsmuster verwendet.

- Iteration #5 - Erstellen von Komponententests. In der fünften Iteration erleichtern wir die Wartung und Änderung unserer Anwendung durch Hinzufügen von Komponententests. Wir verspotten unsere Datenmodellklassen und erstellen Komponententests für unsere Controller und Validierungslogik.

- Iteration #6 - Verwenden Sie die testgesteuerte Entwicklung. In dieser sechsten Iteration fügen wir unserer Anwendung neue Funktionen hinzu, indem wir zuerst Komponententests schreiben und Code für die Komponententests schreiben. In dieser Iteration fügen wir Kontaktgruppen hinzu.

- Iteration #7 - Ajax-Funktionalität hinzufügen. In der siebten Iteration verbessern wir die Reaktionsfähigkeit und Leistung unserer Anwendung, indem wir Unterstützung für Ajax hinzufügen.

## <a name="this-iteration"></a>Diese Iteration

In dieser vierten Iteration der Contact Manager-Anwendung gestalten wir die Anwendung um, um die Anwendung lockerer zu koppeln. Wenn eine Anwendung lose gekoppelt ist, können Sie den Code in einem Teil der Anwendung ändern, ohne den Code in anderen Teilen der Anwendung ändern zu müssen. Lose gekoppelte Anwendungen sind widerstandsfähiger gegenüber Änderungen.

Derzeit ist die gesamte Datenzugriffs- und Validierungslogik, die von der Contact Manager-Anwendung verwendet wird, in den Controllerklassen enthalten. Das ist eine schlechte Idee. Wenn Sie einen Teil Ihrer Anwendung ändern müssen, riskieren Sie, Fehler in einen anderen Teil Ihrer Anwendung einzuführen. Wenn Sie beispielsweise die Validierungslogik ändern, riskieren Sie, neue Fehler in Ihre Datenzugriffs- oder Controllerlogik einzuschleusen.

> [!NOTE] 
> 
> (SRP) sollte eine Klasse nie mehr als einen Grund haben, sich zu ändern. Das Mischen von Controller, Validierung und Datenbanklogik stellt einen massiven Verstoß gegen das Prinzip der einheitlichen Verantwortung dar.

Es gibt mehrere Gründe, warum Sie Ihre Anwendung möglicherweise ändern müssen. Möglicherweise müssen Sie Ihrer Anwendung ein neues Feature hinzufügen, Sie müssen möglicherweise einen Fehler in Ihrer Anwendung beheben oder sie müssen ändern, wie ein Feature Ihrer Anwendung implementiert wird. Anwendungen sind selten statisch. Sie neigen dazu, im Laufe der Zeit zu wachsen und zu mutieren.

Stellen Sie sich beispielsweise vor, dass Sie sich entscheiden, die Implementierung Ihrer Datenzugriffsebene zu ändern. Derzeit verwendet die Contact Manager-Anwendung Microsoft Entity Framework, um auf die Datenbank zuzugreifen. Sie können jedoch zu einer neuen oder alternativen Datenzugriffstechnologie wie ADO.NET Data Services oder NHibernate migrieren. Da der Datenzugriffscode jedoch nicht vom Validierungs- und Controllercode isoliert ist, gibt es keine Möglichkeit, den Datenzugriffscode in der Anwendung zu ändern, ohne anderen Code zu ändern, der nicht direkt mit dem Datenzugriff zusammenhängt.

Wenn eine Anwendung jedoch lose gekoppelt ist, können Sie Änderungen an einem Teil einer Anwendung vornehmen, ohne andere Teile einer Anwendung zu berühren. Sie können z. B. Datenzugriffstechnologien wechseln, ohne Ihre Validierungs- oder Controllerlogik zu ändern.

In dieser Iteration nutzen wir mehrere Software-Designmuster, die es uns ermöglichen, unsere Contact Manager-Anwendung in eine losere gekoppelte Anwendung umzugestalten. Wenn wir fertig sind, wird der Kontakt-Manager nichts tun, was er vorher nicht getan hat. In Zukunft können wir die Anwendung jedoch einfacher ändern.

> [!NOTE] 
> 
> Refactoring ist der Prozess des Umschreibens einer Anwendung in einer Weise, dass sie keine vorhandenen Funktionen verliert.

## <a name="using-the-repository-software-design-pattern"></a>Verwenden des Repository-Softwareentwurfsmusters

Unsere erste Änderung besteht darin, ein Software-Designmuster zu nutzen, das Repository-Muster genannt wird. Wir verwenden das Repository-Muster, um unseren Datenzugriffscode vom Rest unserer Anwendung zu isolieren.

Um das Repository-Muster zu implementieren, müssen wir die folgenden beiden Schritte ausführen:

1. Erstellen einer Schnittstelle
2. Erstellen einer konkreten Klasse, die die Schnittstelle implementiert

Zuerst müssen wir eine Schnittstelle erstellen, die alle Datenzugriffsmethoden beschreibt, die wir ausführen müssen. Die IContactManagerRepository-Schnittstelle ist in Liste 1 enthalten. Diese Schnittstelle beschreibt fünf Methoden: CreateContact(), DeleteContact(), EditContact(), GetContact und ListContacts().

**Auflisten 1 - Modelle-IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

Als Nächstes müssen wir eine konkrete Klasse erstellen, die die IContactManagerRepository-Schnittstelle implementiert. Da wir Microsoft Entity Framework für den Zugriff auf die Datenbank verwenden, erstellen wir eine neue Klasse mit dem Namen EntityContactManagerRepository. Diese Klasse ist in Liste 2 enthalten.

**Auflisten 2 - Modelle-EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

Beachten Sie, dass die EntityContactManagerRepository-Klasse die IContactManagerRepository-Schnittstelle implementiert. Die Klasse implementiert alle fünf Methoden, die von dieser Schnittstelle beschrieben werden.

Sie fragen sich vielleicht, warum wir uns mit einer Schnittstelle beschäftigen müssen. Warum müssen wir sowohl eine Schnittstelle als auch eine Klasse erstellen, die sie implementiert?

Mit einer Ausnahme wird der Rest unserer Anwendung mit der Schnittstelle und nicht mit der betonierten Klasse interagieren. Anstatt die Methoden aufzurufen, die von der EntityContactManagerRepository-Klasse verfügbar gemacht werden, rufen wir die Methoden auf, die von der IContactManagerRepository-Schnittstelle verfügbar gemacht werden.

Auf diese Weise können wir die Schnittstelle mit einer neuen Klasse implementieren, ohne den Rest unserer Anwendung ändern zu müssen. Beispielsweise können wir zu einem späteren Zeitpunkt eine DataServicesContactManagerRepository-Klasse implementieren, die die IContactManagerRepository-Schnittstelle implementiert. Die DataServicesContactManagerRepository-Klasse verwendet möglicherweise ADO.NET Data Services, um auf eine Datenbank anstelle des Microsoft Entity Framework zuzugreifen.

Wenn unser Anwendungscode für die IContactManagerRepository-Schnittstelle anstelle der konkreten EntityContactManagerRepository-Klasse programmiert ist, können wir konkrete Klassen wechseln, ohne den Rest unseres Codes zu ändern. Beispielsweise können wir von der EntityContactManagerRepository-Klasse zur DataServicesContactManagerRepository-Klasse wechseln, ohne unsere Datenzugriffs- oder Validierungslogik zu ändern.

Die Programmierung für Schnittstellen (Abstraktionen) anstelle konkreter Klassen macht unsere Anwendung widerstandsfähiger gegenüber Änderungen.

> [!NOTE] 
> 
> Sie können schnell eine Schnittstelle aus einer konkreten Klasse in Visual Studio erstellen, indem Sie die Menüoption Refactor, Extract Interface auswählen. Sie können beispielsweise zuerst die EntityContactManagerRepository-Klasse erstellen und dann die Extraktschnittstelle verwenden, um die IContactManagerRepository-Schnittstelle automatisch zu generieren.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Verwenden des Entwurfsmusters der Abhängigkeitsinjektionssoftware

Nachdem wir unseren Datenzugriffscode in eine separate Repository-Klasse migriert haben, müssen wir unseren Contact-Controller ändern, um diese Klasse zu verwenden. Wir werden ein Softwareentwurfsmuster namens Dependency Injection nutzen, um die Repository-Klasse in unserem Controller zu verwenden.

Der geänderte Kontaktcontroller ist in Liste 3 enthalten.

**Auflisten 3 - Controller-KontaktController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

Beachten Sie, dass der Kontaktcontroller in Liste 3 über zwei Konstruktoren verfügt. Der erste Konstruktor übergibt eine konkrete Instanz der IContactManagerRepository-Schnittstelle an den zweiten Konstruktor. Die Contact-Controllerklasse verwendet *Constructor Dependency Injection*.

Der einzige Ort, an dem die EntityContactManagerRepository-Klasse verwendet wird, befindet sich im ersten Konstruktor. Der Rest der Klasse verwendet die IContactManagerRepository-Schnittstelle anstelle der konkreten EntityContactManagerRepository-Klasse.

Dies erleichtert das Wechselder der Implementierungen der IContactManagerRepository-Klasse in der Zukunft. Wenn Sie die DataServicesContactRepository-Klasse anstelle der EntityContactManagerRepository-Klasse verwenden möchten, ändern Sie einfach den ersten Konstruktor.

Die Konstruktorabhängigkeitsinjektion macht auch die Contact-Controllerklasse sehr testbar. In den Komponententests können Sie den Contact-Controller instanziieren, indem Sie eine Mockimplementierung der IContactManagerRepository-Klasse übergeben. Diese Funktion der Abhängigkeitsinjektion wird uns in der nächsten Iteration sehr wichtig sein, wenn wir Komponententests für die Contact Manager-Anwendung erstellen.

> [!NOTE] 
> 
> Wenn Sie die Contact-Controller-Klasse vollständig von einer bestimmten Implementierung der IContactManagerRepository-Schnittstelle entkoppeln möchten, können Sie ein Framework nutzen, das Dependency Injection unterstützt, z. B. StructureMap oder Microsoft Entity Framework (MEF). Wenn Sie ein Dependency Injection-Framework nutzen, müssen Sie nie auf eine konkrete Klasse im Code verweisen.

## <a name="creating-a-service-layer"></a>Erstellen einer Service-Ebene

Sie haben vielleicht bemerkt, dass unsere Validierungslogik immer noch mit unserer Controllerlogik in der modifizierten Controllerklasse in Listing 3 verwechselt wird. Aus dem gleichen Grund, aus dem es eine gute Idee ist, unsere Datenzugriffslogik zu isolieren, ist es eine gute Idee, unsere Validierungslogik zu isolieren.

Um dieses Problem zu beheben, können wir eine separate [*Service-Schicht*](http://martinfowler.com/eaaCatalog/serviceLayer.html)erstellen. Die Service-Schicht ist eine separate Ebene, die wir zwischen unseren Controller- und Repository-Klassen einfügen können. Die Service-Schicht enthält unsere Geschäftslogik einschließlich unserer gesamten Validierungslogik.

Der ContactManagerService ist in Liste 4 enthalten. Sie enthält die Validierungslogik der Contact-Controllerklasse.

**Auflisten 4 - Modelle-ContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

Beachten Sie, dass der Konstruktor für den ContactManagerService ein ValidationDictionary erfordert. Die Dienstschicht kommuniziert über dieses ValidationDictionary mit der Controllerschicht. Wir besprechen das ValidationDictionary im folgenden Abschnitt ausführlich, wenn wir das Decorator-Muster besprechen.

Beachten Sie außerdem, dass contactManagerService die IContactManagerService-Schnittstelle implementiert. Sie sollten immer danach streben, mit Schnittstellen statt mit konkreten Klassen zu programmieren. Andere Klassen in der Contact Manager-Anwendung interagieren nicht direkt mit der ContactManagerService-Klasse. Stattdessen wird mit einer Ausnahme der Rest der Contact Manager-Anwendung für die IContactManagerService-Schnittstelle programmiert.

Die IContactManagerService-Schnittstelle ist in Liste 5 enthalten.

**Auflisten 5 - Modelle-IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

Die geänderte Contact-Controller-Klasse ist in Liste 6 enthalten. Beachten Sie, dass der Kontaktcontroller nicht mehr mit dem ContactManager-Repository interagiert. Stattdessen interagiert der Kontaktcontroller mit dem ContactManager-Dienst. Jede Ebene wird so weit wie möglich von anderen Layern isoliert.

**Auflisten 6 - Controller-KontaktController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

Unsere Anwendung verstößt nicht mehr gegen das Prinzip der einheitlichen Verantwortung (SRP). Dem Kontaktcontroller in Listing 6 wurde jede andere Verantwortung entzogen, als den Ablauf der Anwendungsausführung zu steuern. Die gesamte Validierungslogik wurde vom Kontaktcontroller entfernt und in die Dienstebene verschoben. Die gesamte Datenbanklogik wurde in die Repository-Ebene verschoben.

## <a name="using-the-decorator-pattern"></a>Verwenden des Decorator-Musters

Wir wollen in der Lage sein, unsere Service-Schicht vollständig von unserer Controller-Schicht zu entkoppeln. Grundsätzlich sollten wir in der Lage sein, unsere Service-Schicht in einer separaten Baugruppe von unserer Controller-Schicht zu kompilieren, ohne einen Verweis auf unsere MVC-Anwendung hinzufügen zu müssen.

Unsere Service-Schicht muss jedoch in der Lage sein, Validierungsfehlermeldungen an die Controllerebene zurückzugeben. Wie können wir es der Dienstschicht ermöglichen, Validierungsfehlermeldungen zu kommunizieren, ohne Controller und Dienstschicht zu koppeln? Wir können ein Software-Design-Muster namens [Decorator-Muster](http://en.wikipedia.org/wiki/Decorator_pattern)nutzen.

Ein Controller verwendet ein ModelStateDictionary mit dem Namen ModelState, um Validierungsfehler darzustellen. Daher könnten Sie versucht sein, ModelState von der Controller-Ebene an die Service-Ebene zu übergeben. Die Verwendung von ModelState im Dienst-Layer würde ihren Dienst-Layer jedoch von einem Feature des ASP.NET MVC-Frameworks abhängig machen. Dies wäre schlecht, da Sie eines Tages möglicherweise die Dienstschicht mit einer WPF-Anwendung anstelle einer ASP.NET MVC-Anwendung verwenden möchten. In diesem Fall möchten Sie nicht auf das ASP.NET MVC-Framework verweisen, um die ModelStateDictionary-Klasse zu verwenden.

Mit dem Decorator-Muster können Sie eine vorhandene Klasse in eine neue Klasse umschließen, um eine Schnittstelle zu implementieren. Unser Contact Manager-Projekt enthält die ModelStateWrapper-Klasse in Listing 7. Die ModelStateWrapper-Klasse implementiert die Schnittstelle in Liste 8.

**Auflisten 7 - Modelle- "Validierung" und "ModelStateWrapper.cs"**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Auflistung 8 - Models-Validierung- und -IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

Wenn Sie sich Liste 5 genau ansehen, werden Sie feststellen, dass die ContactManager-Dienstebene ausschließlich die IValidationDictionary-Schnittstelle verwendet. Der ContactManager-Dienst ist nicht von der ModelStateDictionary-Klasse abhängig. Wenn der Contact-Controller den ContactManager-Dienst erstellt, umschließt der Controller seinen ModelState wie folgt:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>Zusammenfassung

In dieser Iteration haben wir der Contact Manager-Anwendung keine neuen Funktionen hinzugefügt. Das Ziel dieser Iteration bestand darin, die Contact Manager-Anwendung so umzugestalten, dass sie einfacher zu verwalten und zu ändern ist.

Zuerst haben wir das Repository-Software-Designmuster implementiert. Wir haben den gesamten Datenzugriffscode in eine separate ContactManager-Repository-Klasse migriert.

Wir haben auch unsere Validierungslogik von unserer Controllerlogik isoliert. Wir haben eine separate Service-Schicht erstellt, die unseren gesamten Validierungscode enthält. Die Controllerschicht interagiert mit der Service-Ebene, und die Service-Ebene interagiert mit der Repository-Ebene.

Als wir die Service-Schicht erstellthaben, nutzten wir das Decorator-Muster, um ModelState von unserer Service-Ebene zu isolieren. In unserer Service-Schicht haben wir für die IValidationDictionary-Schnittstelle anstelle von ModelState programmiert.

Schließlich nutzten wir ein Software-Designmuster namens Dependency Injection-Muster. Dieses Muster ermöglicht es uns, gegen Schnittstellen (Abstraktionen) anstelle konkreter Klassen zu programmieren. Durch die Implementierung des Entwurfsmusters "Dependency Injection" wird unser Code ebenfalls testbarer. In der nächsten Iteration fügen wir Komponententests zu unserem Projekt hinzu.

> [!div class="step-by-step"]
> [Zurück](iteration-3-add-form-validation-cs.md)
> [Weiter](iteration-5-create-unit-tests-cs.md)
