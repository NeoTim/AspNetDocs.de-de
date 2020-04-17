---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Erstellen eines Modells mit Geschäftsregelüberprüfungen | Microsoft Docs
author: rick-anderson
description: Schritt 3 zeigt, wie Sie ein Modell erstellen, mit dem wir die Datenbank für unsere NerdDinner-Anwendung abfragen und aktualisieren können.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541636"
---
# <a name="build-a-model-with-business-rule-validations"></a>Erstellen eines Modells mit Geschäftsregelüberprüfungen

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 3 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 3 zeigt, wie Sie ein Modell erstellen, mit dem wir die Datenbank für unsere NerdDinner-Anwendung abfragen und aktualisieren können.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner Schritt 3: Erstellen des Modells

In einem Modell-Ansicht-Controller-Framework bezieht sich der Begriff "Modell" auf die Objekte, die die Daten der Anwendung darstellen, sowie auf die entsprechende Domänenlogik, die Validierungs- und Geschäftsregeln in sie integriert. Das Modell ist in vielerlei Hinsicht das "Herz" einer MVC-basierten Anwendung, und wie wir später sehen werden, wird das Verhalten davon grundlegend getrieben.

Das ASP.NET MVC-Framework unterstützt die Verwendung beliebiger Datenzugriffstechnologie, und Entwickler können aus einer Vielzahl von umfangreichen .NET-Datenoptionen wählen, um ihre Modelle zu implementieren, darunter: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM oder einfach nur RohADO.NET DataReaders oder DataSets.

Für unsere NerdDinner-Anwendung werden wir LINQ to SQL verwenden, um ein einfaches Modell zu erstellen, das ziemlich genau unserem Datenbankdesign entspricht und einige benutzerdefinierte Validierungslogik und Geschäftsregeln hinzufügt. Anschließend implementieren wir eine Repository-Klasse, die die Datenpersistenzimplementierung vom Rest der Anwendung abstrahiert und es uns ermöglicht, sie einfach zu testen.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL ist ein ORM (Object relational Mapper), der als Teil von .NET 3.5 ausgeliefert wird.

LINQ to SQL bietet eine einfache Möglichkeit, Datenbanktabellen .NET-Klassen zuzuordnen, für die wir Codieren können. Für unsere NerdDinner-Anwendung verwenden wir sie, um die Dinners und RSVP-Tabellen in unserer Datenbank Dinner- und RSVP-Klassen zuzuordnen. Die Spalten der Dinner- und RSVP-Tabellen entsprechen den Eigenschaften der Dinner- und RSVP-Kurse. Jedes Dinner- und RSVP-Objekt stellt eine separate Zeile innerhalb der Dinners- oder RSVP-Tabellen in der Datenbank dar.

LINQ to SQL ermöglicht es uns, SQL-Anweisungen manuell zu erstellen, um Dinner- und RSVP-Objekte mit Datenbankdaten abzurufen und zu aktualisieren. Stattdessen definieren wir die Dinner- und RSVP-Klassen, wie sie der Datenbank zugeordnet sind und welche Beziehungen zwischen ihnen besteht. LINQ to SQL kümmert sich dann darum, die entsprechende SQL-Ausführungslogik zu generieren, die zur Laufzeit verwendet werden soll, wenn wir interagieren und sie verwenden.

Wir können die LINQ-Sprachunterstützung innerhalb von VB und C- verwenden, um ausdrucksstarke Abfragen zu schreiben, die Dinner- und RSVP-Objekte aus der Datenbank abrufen. Dies minimiert die Menge an Datencode, den wir schreiben müssen, und ermöglicht es uns, wirklich saubere Anwendungen zu erstellen.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Hinzufügen von LINQ zu SQL-Klassen zu unserem Projekt

Wir beginnen mit einem Rechtsklick auf den Ordner "Modelle" in unserem Projekt und wählen den Menübefehl **&gt;"Neues Element hinzufügen":**

![](build-a-model-with-business-rule-validations/_static/image1.png)

Dadurch wird das Dialogfeld "Neues Element hinzufügen" angezeigt. Wir filtern nach der Kategorie "Daten" und wählen die Vorlage "LINQ to SQL Classes" darin aus:

![](build-a-model-with-business-rule-validations/_static/image2.png)

Wir nennen das Element "NerdDinner" und klicken auf die Schaltfläche "Hinzufügen". Visual Studio fügt eine NerdDinner.dbml-Datei unter unserem Verzeichnis "Models" hinzu und öffnet dann den relationalen Designer von LINQ to SQL-Objekt:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Erstellen von Datenmodellklassen mit LINQ to SQL

LINQ to SQL ermöglicht es uns, schnell Datenmodellklassen aus vorhandenen Datenbankschemas zu erstellen. Dazu öffnen wir die NerdDinner-Datenbank im Server-Explorer und wählen die Tabellen aus, die wir darin modellieren möchten:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Wir können dann die Tabellen auf die LINQ-zu-SQL-Designeroberfläche ziehen. Wenn wir dies tun, erstellt LINQ to SQL automatisch Dinner- und RSVP-Klassen mithilfe des Schemas der Tabellen (mit Klasseneigenschaften, die den Datenbanktabellenspalten zugeordnet sind):

![](build-a-model-with-business-rule-validations/_static/image5.png)

Standardmäßig "pluralisiert" der LINQ to SQL-Designer Tabellen- und Spaltennamen automatisch, wenn Klassen basierend auf einem Datenbankschema erstellt werden. Zum Beispiel: Die Tabelle "Dinners" in unserem Obigen Beispiel führte zu einer "Dinner"-Klasse. Diese Klassenbenennung trägt dazu bei, unsere Modelle mit .NET-Namenskonventionen konsistent zu machen, und ich finde es in der Regel, dass der Designer dies praktisch behebt (insbesondere beim Hinzufügen vieler Tabellen). Wenn Ihnen jedoch der Name einer Vom Designer generierten Klasse oder Eigenschaft nicht gefällt, können Sie ihn immer überschreiben und in einen beliebigen Namen ändern. Sie können dies entweder tun, indem Sie den Entitäts-/Eigenschaftsnamen in der Zeile innerhalb des Designers bearbeiten oder ihn über das Eigenschaftenraster ändern.

Standardmäßig überprüft der LINQ-zu-SQL-Designer auch die Primärschlüssel-/Fremdschlüsselbeziehungen der Tabellen und erstellt basierend darauf automatisch standardmäßige "Beziehungszuordnungen" zwischen den verschiedenen Modellklassen, die er erstellt. Wenn wir z. B. die Tabellen Dinners und RSVP auf den LINQ to SQL-Designer gezogen haben, wurde eine 1:n-Beziehungszuordnung zwischen den beiden abgeleitet, basierend auf der Tatsache, dass die RSVP-Tabelle einen Fremdschlüssel zur Tabelle Dinners hatte (dies wird durch den Pfeil im Designer angezeigt):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Die obige Zuordnung bewirkt, dass LINQ zu SQL der RSVP-Klasse eine stark typisierte "Dinner"-Eigenschaft hinzufügt, die Entwickler verwenden können, um auf das Dinner zuzugreifen, das einem bestimmten RSVP zugeordnet ist. Außerdem wird die Dinner-Klasse über eine "RSVPs"-Auflistungseigenschaft verfügen, mit der Entwickler RSVP-Objekte abrufen und aktualisieren können, die einem bestimmten Dinner zugeordnet sind.

Im Folgenden sehen Sie ein Beispiel für Intellisense in Visual Studio, wenn wir ein neues RSVP-Objekt erstellen und es der RSVPs-Sammlung eines Dinners hinzufügen. Beachten Sie, wie LINQ to SQL automatisch eine "RSVPs"-Auflistung für das Dinner-Objekt hinzugefügt hat:

![](build-a-model-with-business-rule-validations/_static/image7.png)

Durch Hinzufügen des RSVP-Objekts zur RSVPs-Sammlung des Dinners werden wir LINQ zu SQL anwiesen, eine Fremdschlüsselbeziehung zwischen dem Dinner und der RSVP-Zeile in unserer Datenbank zu verknüpfen:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Wenn Ihnen nicht gefällt, wie der Designer eine Tabellenzuordnung modelliert oder benannt hat, können Sie sie überschreiben. Klicken Sie einfach auf den Assoziationspfeil innerhalb des Designers und greifen Sie über das Eigenschaftenraster auf seine Eigenschaften zu, um ihn umzubenennen, zu löschen oder zu ändern. Für unsere NerdDinner-Anwendung funktionieren die Standardzuordnungsregeln jedoch gut für die Datenmodellklassen, die wir erstellen, und wir können nur das Standardverhalten verwenden.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext-Klasse

Visual Studio erstellt automatisch .NET-Klassen, die die Modelle und Datenbankbeziehungen darstellen, die mit dem LINQ to SQL-Designer definiert wurden. Eine LINQ to SQL DataContext-Klasse wird auch für jede LINQ to SQL-Designerdatei generiert, die der Lösung hinzugefügt wurde. Da wir unser LINQ-zu-SQL-Klassenelement "NerdDinner" genannt haben, wird die erstellte DataContext-Klasse "NerdDinnerDataContext" heißen. Diese NerdDinnerDataContext-Klasse ist die primäre Art und Weise, wie wir mit der Datenbank interagieren.

Unsere NerdDinnerDataContext-Klasse macht zwei Eigenschaften verfügbar - "Dinners" und "RSVPs" -, die die beiden Tabellen darstellen, die wir in der Datenbank modelliert haben. Wir können mit dem Code LINQ-Abfragen für diese Eigenschaften schreiben, um Dinner- und RSVP-Objekte aus der Datenbank abzufragen und abzurufen.

Der folgende Code veranschaulicht, wie ein NerdDinnerDataContext-Objekt instanziiert und eine LINQ-Abfrage für dieses Objekt durchgeführt wird, um eine Sequenz von Abendessen zu erhalten, die in der Zukunft auftreten. Visual Studio bietet beim Schreiben der LINQ-Abfrage vollen Intellekt, und die von der Abfrage zurückgegebenen Objekte sind stark typisiert und unterstützen auch intellisense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Ein NerdDinnerDataContext ermöglicht es uns nicht nur, Nachfragen nach Dinner- und RSVP-Objekten zu ermöglichen, sondern verfolgt auch automatisch alle Änderungen, die wir anschließend an den Dinner- und RSVP-Objekten vornehmen, die wir durch sie abrufen. Wir können diese Funktion verwenden, um die Änderungen einfach wieder in der Datenbank zu speichern – ohne expliziten SQL-Updatecode schreiben zu müssen.

Der folgende Code veranschaulicht beispielsweise, wie sie eine LINQ-Abfrage verwenden, um ein einzelnes Dinner-Objekt aus der Datenbank abzurufen, zwei der Dinner-Eigenschaften zu aktualisieren und die Änderungen dann wieder in der Datenbank zu speichern:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Das NerdDinnerDataContext-Objekt im obigen Code hat automatisch die Eigenschaftsänderungen nachverfolgt, die am Dinner-Objekt vorgenommen wurden, das wir von ihm abgerufen haben. Wenn wir die "SubmitChanges()"-Methode aufgerufen haben, wird eine entsprechende SQL-Anweisung "UPDATE" für die Datenbank ausgeführt, um die aktualisierten Werte beizubehalten.

### <a name="creating-a-dinnerrepository-class"></a>Erstellen einer DinnerRepository-Klasse

Bei kleinen Anwendungen ist es manchmal in Ordnung, Controller direkt mit einer LINQ-zu-SQL DataContext-Klasse arbeiten zu lassen und LINQ-Abfragen in die Controller einzubetten. Wenn Anwendungen jedoch größer werden, wird dieser Ansatz umständlich zu warten und zu testen. Es kann auch dazu führen, dass wir dieselben LINQ-Abfragen an mehreren Stellen duplizieren.

Ein Ansatz, der die Wartung und den Test von Anwendungen vereinfachen kann, ist die Verwendung eines "Repository"-Musters. Eine Repository-Klasse hilft beim Kapseln von Datenabfragen und Persistenzlogik und abstrahiert die Implementierungsdetails der Datenpersistenz von der Anwendung. Die Verwendung eines Repository-Musters kann nicht nur anwendungscodecleaner sein, sondern auch das Ändern von Datenspeicherimplementierungen in Zukunft erleichtern und das Testen einer Anwendung durch Komponenten erleichtern, ohne dass eine echte Datenbank erforderlich ist.

Für unsere NerdDinner-Anwendung definieren wir eine DinnerRepository-Klasse mit der folgenden Signatur:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Hinweis: Später in diesem Kapitel extrahieren wir eine IDinnerRepository-Schnittstelle aus dieser Klasse und aktivieren die Abhängigkeitsinjektion damit auf unseren Controllern. Zunächst werden wir jedoch einfach anfangen und direkt mit der DinnerRepository-Klasse arbeiten.*

Um diese Klasse zu implementieren, klicken wir mit der rechten Maustaste auf unseren Ordner "Modelle" und wählen den Menübefehl **&gt;"Neues Element hinzufügen".** Im Dialogfeld "Neues Element hinzufügen" wählen wir die Vorlage "Klasse" aus und benennen die Datei "DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

Wir können dann unsere DinnerRepository-Klasse mit dem folgenden Code implementieren:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Abrufen, Aktualisieren, Einfügen und Löschen mit der DinnerRepository-Klasse

Nachdem wir nun unsere DinnerRepository-Klasse erstellt haben, sehen wir uns einige Codebeispiele an, die allgemeine Aufgaben veranschaulichen, die wir damit erledigen können:

#### <a name="querying-examples"></a>Abfragen von Beispielen

Der folgende Code ruft ein einzelnes Dinner mit dem DinnerID-Wert ab:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Der folgende Code ruft alle bevorstehenden Abendessen ab und schleift über sie:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Einfügen und Aktualisieren von Beispielen

Der folgende Code zeigt das Hinzufügen von zwei neuen Abendessen. Ergänzungen/Änderungen am Repository werden erst dann an die Datenbank übergeben, wenn die "Save()"-Methode aufgerufen wird. LINQ to SQL umschließt automatisch alle Änderungen in einer Datenbanktransaktion – entweder alle Änderungen passieren oder keine von ihnen, wenn unser Repository speichert:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Der folgende Code ruft ein vorhandenes Dinner-Objekt ab und ändert zwei Eigenschaften darauf. Die Änderungen werden zurück an die Datenbank übergeben, wenn die "Save()"-Methode in unserem Repository aufgerufen wird:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Der folgende Code ruft ein Abendessen ab und fügt ihm dann einen RSVP hinzu. Dies geschieht mithilfe der RSVPs-Auflistung für das Dinner-Objekt, das LINQ to SQL für uns erstellt hat (da zwischen den beiden in der Datenbank eine Primärschlüssel-/Fremdschlüsselbeziehung besteht). Diese Änderung wird als neue RSVP-Tabellenzeile in der Datenbank beibehalten, wenn die "Save()"-Methode im Repository aufgerufen wird:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Löschbeispiel

Der folgende Code ruft ein vorhandenes Dinner-Objekt ab und markiert es dann, dass es gelöscht wird. Wenn die "Save()"-Methode im Repository aufgerufen wird, wird das Löschen zurück in die Datenbank übertragen:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Integration von Validierung und Geschäftsregellogik in Modellklassen

Die Integration von Validierung und Geschäftsregellogik ist ein wichtiger Bestandteil jeder Anwendung, die mit Daten arbeitet.

#### <a name="schema-validation"></a>Schemavalidierung

Wenn Modellklassen mit dem LINQ-zu-SQL-Designer definiert werden, entsprechen die Datentypen der Eigenschaften in den Datenmodellklassen den Datentypen der Datenbanktabelle. Beispiel: Wenn die Spalte "EventDate" in der Tabelle Dinners eine "datetime" ist, ist die von LINQ to SQL erstellte Datenmodellklasse vom Typ "DateTime" (ein integrierter .NET-Datentyp). Dies bedeutet, dass Sie Kompilierungsfehler erhalten, wenn Sie versuchen, ihm eine ganze Zahl oder boolesche aus dem Code zuzuweisen, und es wird automatisch ein Fehler ausgelöst, wenn Sie versuchen, einen ungültigen Zeichenfolgentyp zur Laufzeit implizit in ihn zu konvertieren.

LINQ to SQL verarbeitet auch automatisch das Ausweichen von SQL-Werten für Sie, wenn Sie Zeichenfolgen verwenden – was Sie bei der Verwendung vor SQL-Injektionsangriffen schützt.

#### <a name="validation-and-business-rule-logic"></a>Validierung und Geschäftsregellogik

Die Schemaüberprüfung ist als erster Schritt nützlich, reicht aber selten aus. Die meisten realen Szenarien erfordern die Möglichkeit, umfangreichere Validierungslogik anzugeben, die mehrere Eigenschaften umfassen kann, Code auszuführen und häufig ein Bewusstsein für den Status eines Modells zu haben (z. B. wird es erstellt /aktualisiert/gelöscht oder in einem domänenspezifischen Zustand wie "archiviert"). Es gibt eine Vielzahl unterschiedlicher Muster und Frameworks, die zum Definieren und Anwenden von Validierungsregeln auf Modellklassen verwendet werden können, und es gibt mehrere .NET-basierte Frameworks, die dabei hilfreich sein können. Sie können so ziemlich jede von ihnen in ASP.NET MVC-Anwendungen verwenden.

Für die Zwecke unserer NerdDinner-Anwendung verwenden wir ein relativ einfaches und geradliniges Muster, bei dem wir eine IsValid-Eigenschaft und eine GetRuleViolations()-Methode für unser Dinner-Modellobjekt verfügbar machen. Die IsValid-Eigenschaft gibt true oder false zurück, je nachdem, ob die Validierungs- und Geschäftsregeln alle gültig sind. Die GetRuleViolations()-Methode gibt eine Liste aller Regelfehler zurück.

Wir implementieren IsValid und GetRuleViolations() für unser Dinner-Modell, indem wir unserem Projekt eine "Teilklasse" hinzufügen. Partielle Klassen können verwendet werden, um Klassen, die von einem VS-Designer verwaltet werden (wie die vom LINQ to SQL-Designer generierte Dinner-Klasse), Methoden/Eigenschaften/Ereignisse hinzuzufügen und zu vermeiden, dass das Tool mit unserem Code durcheinander kommt. Wir können unserem Projekt eine neue Teilklasse hinzufügen, indem wir mit der rechten Maustaste auf den Ordner "Models" klicken und dann den Menübefehl "Neues Element hinzufügen" auswählen. Wir können dann die Vorlage "Klasse" im Dialogfeld "Neues Element hinzufügen" auswählen und sie Dinner.cs nennen.

![](build-a-model-with-business-rule-validations/_static/image11.png)

Wenn Sie auf die Schaltfläche "Hinzufügen" klicken, wird unserem Projekt eine Dinner.cs Datei hinzugefügt und in der IDE geöffnet. Wir können dann ein grundlegendes Regel-/Validierungserzwingungsframework implementieren, indem wir den folgenden Code verwenden:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Ein paar Hinweise zum obigen Code:

- Der Dinner-Klasse wird ein "partielles" Schlüsselwort vorangestellt, d. h., der darin enthaltene Code wird mit der vom LINQ to SQL-Designer generierten/verwalteten Klasse kombiniert und in eine einzelne Klasse kompiliert.
- Die RuleViolation-Klasse ist eine Hilfsklasse, die wir dem Projekt hinzufügen, die es uns ermöglicht, weitere Details zu einer Regelverletzung bereitzustellen.
- Die Dinner.GetRuleViolations()-Methode bewirkt, dass unsere Validierungs- und Geschäftsregeln ausgewertet werden (wir werden sie in Kürze implementieren). Anschließend wird eine Sequenz von RuleViolation-Objekten zurückgegeben, die weitere Details zu Regelfehlern bereitstellen.
- Die Dinner.IsValid-Eigenschaft stellt eine praktische Hilfseigenschaft bereit, die angibt, ob das Dinner-Objekt über aktive RuleViolations verfügt. Es kann von einem Entwickler, der das Dinner-Objekt verwendet, jederzeit proaktiv überprüft werden (und löst keine Ausnahme aus).
- Die partielle Methode Dinner.OnValidate() ist ein Hook, den LINQ to SQL bereitstellt, der es uns ermöglicht, benachrichtigt zu werden, wenn das Dinner-Objekt in der Datenbank beibehalten wird. Unsere OnValidate()-Implementierung oben stellt sicher, dass das Dinner keine Regelverletzungen hat, bevor es gespeichert wird. Wenn es sich in einem ungültigen Zustand befindet, löst es eine Ausnahme aus, die dazu führt, dass LINQ to SQL die Transaktion abbricht.

Dieser Ansatz bietet einen einfachen Rahmen, in den wir Validierungs- und Geschäftsregeln integrieren können. Fügen wir jetzt die folgenden Regeln zu unserer GetRuleViolations()-Methode hinzu:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

Wir verwenden die "Yield Return"-Funktion von C, um eine Sequenz von Regelverletzungen zurückzugeben. Die ersten sechs Regelprüfungen oben erzwingen einfach, dass Zeichenfolgeneigenschaften auf unserem Dinner nicht null oder leer sein können. Die letzte Regel ist etwas interessanter und ruft eine PhoneValidator.IsValidNumber()-Hilfsmethode auf, die wir unserem Projekt hinzufügen können, um zu überprüfen, ob das ContactPhone-Nummernformat mit dem Land des Abendessens übereinstimmt.

Wir können . NET unterstützt unterstützung für reguläre Ausdrücke, um diese Telefonvalidierungsunterstützung zu implementieren. Im Folgenden finden Sie eine einfache PhoneValidator-Implementierung, die wir zu unserem Projekt hinzufügen können, mit der wir länderspezifische Regex-Musterprüfungen hinzufügen können:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Umgang mit Validierungs- und Geschäftslogikverletzungen

Nachdem wir nun den oben genannten Validierungs- und Geschäftsregelcode hinzugefügt haben, werden unsere Validierungslogikregeln jedes Mal, wenn wir versuchen, ein Dinner zu erstellen oder zu aktualisieren, ausgewertet und erzwungen.

Entwickler können Code wie unten schreiben, um proaktiv zu bestimmen, ob ein Dinner-Objekt gültig ist, und eine Liste aller darin behandelten Verstöße abzurufen, ohne Ausnahmen auszulösen:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Wenn wir versuchen, ein Dinner in einem ungültigen Zustand zu speichern, wird eine Ausnahme ausgelöst, wenn wir die Save()-Methode im DinnerRepository aufrufen. Dies liegt daran, dass LINQ to SQL automatisch unsere Dinner.OnValidate() partielle Methode aufruft, bevor die Änderungen des Abendessens spartiert, und wir Code zu Dinner.OnValidate() hinzugefügt haben, um eine Ausnahme auszulösen, wenn regelgebende Verstöße im Dinner vorliegen. Wir können diese Ausnahme abfangen und eine Liste der zu behebenden Verstöße erneut abrufen:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Da unsere Validierungs- und Geschäftsregeln innerhalb unserer Modellebene und nicht innerhalb der UI-Ebene implementiert sind, werden sie in allen Szenarien in unserer Anwendung angewendet und verwendet. Wir können später Geschäftsregeln ändern oder hinzufügen und alle Codes, die mit unseren Dinner-Objekten funktionieren, diese berücksichtigen lassen.

Die Flexibilität, Geschäftsregeln an einem Ort zu ändern, ohne dass diese Änderungen in der gesamten Anwendungs- und Uilogik aufgewirkt sind, ist ein Zeichen für eine gut geschriebene Anwendung und ein Vorteil, den ein MVC-Framework fördert.

### <a name="next-step"></a>Nächster Schritt

Wir haben jetzt ein Modell, mit dem wir unsere Datenbank abfragen und aktualisieren können.

Fügen wir nun einige Controller und Ansichten zu dem Projekt hinzu, mit denen wir eine HTML-Benutzeroberflächenerfahrung um das Projekt herum erstellen können.

> [!div class="step-by-step"]
> [Zurück](create-a-database.md)
> [Weiter](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
