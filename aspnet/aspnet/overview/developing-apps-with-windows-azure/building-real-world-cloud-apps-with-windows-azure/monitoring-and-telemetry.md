---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: Überwachung und Telemetrie (Erstellen von Echtzeit-Cloud-Apps mit Azure) | Microsoft Docs
author: MikeWasson
description: Das Building Real World Cloud Apps mit Azure E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es erklärt 13 Muster und Praktiken, die er...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675670"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>Überwachung und Telemetrie (Erstellen von Echtzeit-Cloud-Apps mit Azure)

von [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project herunterladen](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) oder [E-Book herunterladen](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Das **Building Real World Cloud Apps mit Azure** E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es werden 13 Muster und Vorgehensweisen erläutert, die Ihnen bei der erfolgreichen Entwicklung von Web-Apps für die Cloud helfen können. Informationen zum E-Book finden Sie [im ersten Kapitel](introduction.md).

Viele Menschen verlassen sich darauf, dass Kunden sie darüber informieren, wenn ihre Anwendung ausfällt. Das ist nirgendwo wirklich eine bewährte Methode, und vor allem nicht in der Cloud. Es gibt keine Garantie für eine schnelle Benachrichtigung, und wenn Sie benachrichtigt werden, erhalten Sie oft minimale oder irreführende Daten über das, was passiert ist. Mit guten Telemetrie- und Protokollierungssystemen können Sie wissen, was mit Ihrer App vor sich geht, und wenn etwas schief geht, finden Sie sofort etwas heraus und haben hilfreiche Informationen zur Fehlerbehebung, mit denen Sie arbeiten können.

## <a name="buy-or-rent-a-telemetry-solution"></a>Kaufen oder mieten Sie eine Telemetrielösung

> [!NOTE]
> Dieser Artikel wurde geschrieben, bevor [Application Insights](/azure/application-insights/app-insights-overview) veröffentlicht wurde. Application Insights ist der bevorzugte Ansatz für Telemetrielösungen in Azure. Weitere Informationen finden Sie unter [Einrichten von Application Insights für Ihre ASP.NET-Website.](/azure/application-insights/app-insights-asp-net)

Eines der Dinge, die an der Cloud-Umgebung großartig sind, ist, dass es wirklich einfach ist, Ihren Weg zum Sieg zu kaufen oder zu mieten. Telemetrie ist ein Beispiel. Ohne viel Aufwand können Sie ein wirklich gutes Telemetriesystem in Betrieb nehmen, sehr kostengünstig. Es gibt eine Reihe großartiger Partner, die in Azure integriert werden, und einige von ihnen verfügen über kostenlose Kontingente – so können Sie grundlegende Telemetrie datenfrei erhalten. Hier sind nur einige der derzeit in Azure verfügbaren:

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) enthält auch Überwachungsfunktionen.

Wir gehen schnell durch die Einrichtung von New Relic, um zu zeigen, wie einfach es sein kann, ein Telemetriesystem zu verwenden.

Melden Sie sich im Azure-Verwaltungsportal für den Dienst an. Klicken Sie auf **Neu**, und dann auf **Speichern**. Das Dialogfeld **"Auswählen eines Add-On"-Dialogfelds** wird angezeigt. Scrollen Sie nach unten und klicken Sie auf **Neues Relikt**.

![Add-On auswählen](monitoring-and-telemetry/_static/image1.png)

Klicken Sie auf den rechten Pfeil, und wählen Sie die gewünschte Dienstebene aus. Für diese Demo verwenden wir das kostenlose Kontingent.

![Add-on personalisieren](monitoring-and-telemetry/_static/image2.png)

Klicken Sie auf den rechten Pfeil, bestätigen Sie den "Kauf", und New Relic wird jetzt als Add-on im Portal angezeigt.

![Bewertung des Kaufs](monitoring-and-telemetry/_static/image3.png)

![Neues Relic-Add-on im Management-Portal](monitoring-and-telemetry/_static/image4.png)

Klicken Sie auf **Verbindungsinfo**, und kopieren Sie den Lizenzschlüssel.

![Verbindungsinformationen](monitoring-and-telemetry/_static/image5.png)

Wechseln Sie zur Registerkarte **Konfigurieren** für Ihre Web-App im Portal, legen Sie **die Leistungsüberwachung** auf **Add-On**fest, und legen Sie die Dropdown-Dropdown-Liste **"Add-On** auswählen" auf **Neues Relikt**fest. Klicken Sie dann auf **Speichern**.

![Neues Relikt auf der Registerkarte Konfigurieren](monitoring-and-telemetry/_static/image6.png)

Installieren Sie in Visual Studio das Paket "Neues Relikt NuGet" in Ihrer App.

![Entwickleranalyse auf der Registerkarte Konfigurieren](monitoring-and-telemetry/_static/image7.png)

Stellen Sie die App in Azure bereit, und beginnen Sie mit der Verwendung. Erstellen Sie ein paar Fix It-Aufgaben, um einige Aktivitäten für New Relic zu überwachen.

Kehren Sie dann zur Seite **"Neues Relikt"** auf der Registerkarte **"Add-ons"** des Portals zurück, und klicken Sie auf **Verwalten**. Das Portal sendet Sie an das Verwaltungsportal "Neues Relikt" und verwendet die einmalige Anmeldung für die Authentifizierung, sodass Sie Ihre Anmeldeinformationen nicht erneut eingeben müssen. Auf der Übersichtsseite finden Sie eine Vielzahl von Leistungsstatistiken. (Klicken Sie auf das Bild, um die Übersichtsseite in voller Größe anzuzeigen.)

[![Neue Registerkarte "Reliktüberwachung"](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

Hier sind nur einige der Statistiken, die Sie sehen können:

- Durchschnittliche Reaktionszeit zu unterschiedlichen Tageszeiten.

    ![Antwortzeit](monitoring-and-telemetry/_static/image10.png)
- Durchsatzraten (in Anfragen pro Minute) zu unterschiedlichen Tageszeiten.

    ![Throughput](monitoring-and-telemetry/_static/image11.png)
- Server-CPU-Zeit für die Verarbeitung verschiedener HTTP-Anforderungen.

    ![Webtransaktionszeiten](monitoring-and-telemetry/_static/image12.png)
- CPU-Zeit, die in verschiedenen Teilen des Anwendungscodes verbracht wurde:

    ![Ablaufverfolgungsdetails](monitoring-and-telemetry/_static/image13.png)
- Historische Leistungsstatistiken.

    ![Historische Aufführung](monitoring-and-telemetry/_static/image14.png)
- Aufrufe an externe Dienste wie den Blobdienst und Statistiken darüber, wie zuverlässig und reaktionsschnell der Dienst war.

    ![Externe Dienste](monitoring-and-telemetry/_static/image15.png)

    ![Externe Dienste](monitoring-and-telemetry/_static/image16.png)

    ![Externer Dienst](monitoring-and-telemetry/_static/image17.png)
- Informationen darüber, wo in der Welt oder wo in den USA Web-App-Verkehr kam.

    ![Gebiet](monitoring-and-telemetry/_static/image18.png)

Sie können auch Berichte und Ereignisse einrichten. Sie können z. B. jederzeit sagen, dass Sie Fehler sehen, eine E-Mail senden, um supportmitarbeiter über das Problem zu informieren.

![Berichte](monitoring-and-telemetry/_static/image19.png)

New Relic ist nur ein Beispiel für ein Telemetriesystem; All dies können Sie auch von anderen Diensten erhalten. Das Schöne an der Cloud ist, dass Sie ohne Code und für minimale oder gar keine Kosten plötzlich viel mehr Informationen darüber erhalten können, wie Ihre Anwendung verwendet wird und was Ihre Kunden tatsächlich erleben.

<a id="log"></a>
## <a name="log-for-insight"></a>Log für Einblicke

Ein Telemetriepaket ist ein guter erster Schritt, aber Sie müssen immer noch Ihren eigenen Code instrumentieren. Der Telemetriedienst informiert Sie, wenn ein Problem auftritt, und teilt Ihnen mit, was die Kunden erleben, aber er gibt Ihnen möglicherweise keine großen Einblicke in das, was in Ihrem Code vor sich geht.

Sie möchten nicht in einen Produktionsserver remote, um zu sehen, was Ihre App tut. Das mag praktisch sein, wenn Sie einen Server haben, aber was ist, wenn Sie auf Hunderte von Servern skaliert haben und Nicht wissen, in welche Sie entfernt werden müssen? Ihre Protokollierung sollte genügend Informationen bereitstellen, die Sie nie in Produktionsserver remote einstecken müssen, um Probleme zu analysieren und zu debuggen. Sie sollten genügend Informationen protokollieren, damit Sie Probleme ausschließlich über die Protokolle isolieren können.

### <a name="log-in-production"></a>Anmelden der Produktion

Viele Leute aktivieren die Ablaufverfolgung in der Produktion nur, wenn ein Problem auftritt und sie debuggen möchten. Dies kann zu einer erheblichen Verzögerung zwischen dem Zeitpunkt führen, zu dem Sie ein Problem kennen, und dem Zeitpunkt, zu dem Sie nützliche Informationen zur Fehlerbehebung erhalten. Und die Informationen, die Sie erhalten, sind möglicherweise nicht hilfreich für intermittierende Fehler.

Was wir in der Cloud-Umgebung empfehlen, in der Speicher kostengünstig ist, ist, dass Sie die Anmeldung in der Produktion immer verlassen. Auf diese Weise, wenn Fehler auftreten, haben Sie sie bereits protokolliert, und Sie haben historische Daten, die Ihnen helfen können, Probleme zu analysieren, die sich im Laufe der Zeit entwickeln oder regelmäßig zu verschiedenen Zeiten auftreten. Sie können einen Bereinigungsprozess automatisieren, um alte Protokolle zu löschen, aber Sie können feststellen, dass es teurer ist, einen solchen Prozess einzurichten, als die Protokolle aufzubewahren.

Die zusätzlichen Kosten der Protokollierung sind trivial im Vergleich zu der Menge an Zeit und Geld bei der Fehlerbehebung, die Sie sparen können, indem Sie alle Informationen, die Sie benötigen, bereits verfügbar haben, wenn etwas schief geht. Wenn Ihnen dann jemand sagt, dass er gestern Abend um 8:00 Uhr einen zufälligen Fehler hatte, sich aber nicht an den Fehler erinnert, können Sie leicht herausfinden, was das Problem war.

Für weniger als 4 USD pro Monat können Sie 50 Gigabyte an Protokollen bereithalten, und die Auswirkungen der Protokollierung auf die Leistung sind trivial, solange Sie eines im Auge behalten – um Leistungsengpässe zu vermeiden, stellen Sie sicher, dass Ihre Protokollierungsbibliothek asynchron ist.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>Unterscheiden von Protokollen, die von Protokollen, die Eine Aktion erfordern, informieren

Protokolle sind für INFORM (Ich möchte, dass Sie etwas wissen) oder ACT (Ich möchte, dass Sie etwas tun). Achten Sie darauf, NUR ACT-Protokolle für Probleme zu schreiben, bei denen eine Person oder ein automatisierter Prozess wirklich Maßnahmen ergreifen muss. Zu viele ACT-Protokolle verursachen Geräusche, was zu viel Arbeit erfordert, um alles zu durchstöten, um echte Probleme zu finden. Und wenn Ihre ACT-Protokolle automatisch Aktionen auslösen, wie z. B. das Senden von E-Mails an Support-Mitarbeiter, vermeiden Sie, dass Tausende solcher Aktionen durch ein einziges Problem ausgelöst werden.

In der .NET System.Diagnostics-Ablaufverfolgung können Protokollen Fehler-, Warnungs-, Info- und Debug-/Verbose-Ebene zugewiesen werden. Sie können ACT von INFORM-Protokollen unterscheiden, indem Sie die Fehlerstufe für ACT-Protokolle reservieren und die unteren Ebenen für INFORM-Protokolle verwenden.

![Protokolliergrade](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>Konfigurieren von Protokollierungsebenen zur Laufzeit

Es lohnt sich zwar, die Protokollierung immer in der Produktion zu verwenden, aber eine weitere bewährte Methode besteht darin, ein Protokollierungsframework zu implementieren, mit dem Sie zur Laufzeit die Detailgenauigkeit anpassen können, die Sie protokollieren, ohne Ihre Anwendung erneut bereitzustellen oder neu zu starten. Wenn Sie beispielsweise die Ablaufverfolgungsfunktion in verwenden, können `System.Diagnostics` Sie Fehler-, Warnungs-, Info- und Debug-/Verbose-Protokolle erstellen. Es wird empfohlen, Fehler-, Warnungs- und Infoprotokolle immer in der Produktion zu protokollieren, und Sie sollten in der Lage sein, die Debug/Verbose-Protokollierung dynamisch zur Fehlerbehebung von Fall zu Fall hinzuzufügen.

Web-Apps in Azure App Service bieten `System.Diagnostics` integrierte Unterstützung für das Schreiben von Protokollen in das Dateisystem, den Tabellenspeicher oder den Blobspeicher. Sie können für jedes Speicherziel verschiedene Protokollierungsebenen auswählen und die Protokollierungsebene spontan ändern, ohne die Anwendung neu zu starten. Die Blobspeicherunterstützung erleichtert das [HDInsight](https://docs.microsoft.com/azure/hdinsight/) Ausführen von HDInsight-Analyseaufträgen in Ihren Anwendungsprotokollen, da HDInsight weiß, wie sie direkt mit Blob-Speicher arbeiten.

### <a name="log-exceptions"></a>Protokollieren von Ausnahmen

Machen Sie nicht nur *Eine Ausnahme. ToString()* in Ihrem Protokollierungscode. Das lässt kontextbezogene Informationen außen vor. Bei SQL-Fehlern wird die SQL-Fehlernummer weggezurt. Schließen Sie für alle Ausnahmen Kontextinformationen, die Ausnahme selbst und innere Ausnahmen ein, um sicherzustellen, dass Sie alles bereitstellen, was für die Fehlerbehebung erforderlich ist. Kontextinformationen können z. B. den Servernamen, einen Transaktionsbezeichner und einen Benutzernamen (jedoch nicht das Kennwort oder geheime Informationen!) enthalten.

Wenn Sie sich darauf verlassen, dass jeder Entwickler mit der Ausnahmeprotokollierung das Richtige tut, werden einige davon nicht. Um sicherzustellen, dass es jedes Mal richtig gemacht wird, erstellen Sie die Ausnahmebehandlung direkt in Ihre Logger-Schnittstelle: Übergeben Sie das Ausnahmeobjekt selbst an die Loggerklasse, und protokollieren Sie die Ausnahmedaten ordnungsgemäß in der Loggerklasse.

### <a name="log-calls-to-services"></a>Protokollieren von Anrufen an Dienste

Es wird dringend empfohlen, dass Sie jedes Mal, wenn Ihre App einen Dienst aufruft, ein Protokoll schreiben, sei es in einer Datenbank oder einer REST-API oder einem externen Dienst. Fügen Sie nicht nur einen Hinweis auf Erfolg oder Misserfolg in Ihre Protokolle ein, sondern auch, wie lange jede Anforderung gedauert hat. In der Cloud-Umgebung werden häufig Probleme im Zusammenhang mit Verlangsamungen und nicht durch vollständige Ausfälle auftreten. Etwas, das normalerweise 10 Millisekunden dauert, kann plötzlich beginnen, eine Sekunde zu nehmen. Wenn Ihnen jemand sagt, dass Ihre App langsam ist, möchten Sie in der Lage sein, New Relic oder einen Telemetriedienst, den Sie haben, zu betrachten und ihre Erfahrung zu validieren, und dann möchten Sie in der Lage sein, Ihre eigenen Protokolle zu sehen, um in die Details zu tauchen, warum es langsam ist.

### <a name="use-an-ilogger-interface"></a>Verwenden einer ILogger-Schnittstelle

Was wir empfehlen, wenn Sie eine Produktionsanwendung erstellen, ist eine einfache *ILogger-Schnittstelle* zu erstellen und einige Methoden darin zu kleben. Dies macht es einfach, die Protokollierungsimplementierung später zu ändern und müssen nicht den gesamten Code durchlaufen, um dies zu tun. Wir könnten die `System.Diagnostics.Trace` Klasse in der gesamten Fix It-App verwenden, aber stattdessen verwenden wir sie unter den Abdeckungen in einer Protokollierungsklasse, die *ILogger*implementiert, und wir führen *ILogger-Methodenaufrufe* in der gesamten App durch.

Auf diese Weise, wenn Sie jemals Ihre Protokollierung [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) reicher machen möchten, können Sie mit dem gewünschten Protokollierungsmechanismus ersetzen. Wenn Ihre App beispielsweise wächst, können Sie entscheiden, dass Sie ein umfassenderes Protokollierungspaket wie [NLog](http://nlog-project.org/) oder [Enterprise Library Logging Application Block](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)verwenden möchten. ([Log4Net](http://logging.apache.org/log4net/) ist ein weiteres beliebtes Protokollierungsframework, aber es führt keine asynchrone Protokollierung aus.)

Ein möglicher Grund für die Verwendung eines Frameworks wie NLog besteht darin, die Protokollierungsausgabe in separate Datenspeicher mit hohem Volumen und hohem Wert aufzuteilen. Auf diese Weise können Sie große Mengen von INFORM-Daten effizient speichern, für die Sie keine schnellen Abfragen ausführen müssen, während Sie gleichzeitig schnellen Zugriff auf ACT-Daten beibehalten.

### <a name="semantic-logging"></a>Semantische Protokollierung

Eine relativ neue Möglichkeit zur Protokollierung, die nützlichere Diagnoseinformationen erzeugen kann, finden Sie unter [Enterprise Library Semantic Logging Application Block (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). SLAB verwendet [Event Tracing für Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) und [EventSource-Unterstützung](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) in .NET 4.5, um strukturiertere und abfraderbare Protokolle zu erstellen. Sie definieren für jeden Ereignistyp, den Sie protokollieren, eine andere Methode, mit der Sie die schreibenden Informationen anpassen können. Um beispielsweise einen SQL-Datenbankfehler zu `LogSQLDatabaseError` protokollieren, können Sie eine Methode aufrufen. Für diese Art von Ausnahme wissen Sie, dass eine wichtige Information die Fehlernummer ist, sodass Sie einen Fehlernummernparameter in die Methodensignatur aufnehmen und die Fehlernummer als separates Feld in den Protokolldatensatz aufnehmen können, den Sie schreiben. Da sich die Nummer in einem separaten Feld befindet, können Sie schneller und zuverlässiger Berichte basierend auf SQL-Fehlernummern abrufen, als wenn Sie die Fehlernummer nur in eine Nachrichtenzeichenfolge verketten würden.

## <a name="logging-in-the-fix-it-app"></a>Anmelden in der Fix It-App

### <a name="the-ilogger-interface"></a>Die ILogger-Schnittstelle

Hier ist die *ILogger-Schnittstelle* in der Fix It App.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

Mit diesen Methoden können Sie Protokolle auf den gleichen vier Ebenen schreiben, die von *System.Diagnostics*unterstützt werden. Die TraceApi-Methoden sind zum Protokollieren externer Dienstaufrufe mit Informationen zur Latenz. Sie können auch eine Reihe von Methoden für die Debug/Verbose-Ebene hinzufügen.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>Die Logger-Implementierung der ILogger-Schnittstelle

Die Implementierung der Schnittstelle ist wirklich einfach. Es ruft im Grunde nur in die *Standard-System.Diagnostics-Methoden.* Der folgende Ausschnitt zeigt alle drei Informationsmethoden und jeweils eine der anderen Methoden.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>Aufrufen der ILogger-Methoden

Jedes Mal, wenn Code in der Fix It-App eine Ausnahme abfängt, ruft er eine *ILogger-Methode* auf, um die Ausnahmedetails zu protokollieren. Und jedes Mal, wenn der Dienst die Datenbank, den Blobdienst oder eine REST-API aufruft, startet er eine Stoppuhr vor dem Aufruf, stoppt die Stoppuhr, wenn der Dienst zurückkehrt, und protokolliert die verstrichene Zeit zusammen mit Informationen über Erfolg oder Fehler.

Beachten Sie, dass die Protokollnachricht den Klassennamen und den Methodennamen enthält. Es ist eine gute Methode, um sicherzustellen, dass Protokollnachrichten identifizieren, welcher Teil des Anwendungscodes sie geschrieben hat.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Also jetzt für jedes Mal, wenn die Fix It-App einen Aufruf an SQL-Datenbank gemacht hat, können Sie den Aufruf, die Methode, die sie aufgerufen hat, und genau sehen, wie viel Zeit es gedauert hat.

![SQL-Datenbankabfrage in Protokollen](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

Wenn Sie die Protokolle durchsuchen, können Sie sehen, dass die Zeit, die Datenbankaufrufe dauern, variabel ist. Diese Informationen könnten nützlich sein: Da die App all dies protokolliert, können Sie historische Trends in der Funktionsweise des Datenbankdienstes im Laufe der Zeit analysieren. Beispielsweise ist ein Dienst die meiste Zeit schnell, aber Anforderungen schlagen möglicherweise fehl oder Die Antworten verlangsamen sich zu bestimmten Tageszeiten.

Sie können dasselbe für den Blob-Dienst tun – für jedes Mal, wenn die App eine neue Datei hochlädt, gibt es ein Protokoll, und Sie können genau sehen, wie lange es dauerte, jede Datei hochzuladen.

![Blob-Upload-Protokoll](monitoring-and-telemetry/_static/image23.png)

Es sind nur ein paar zusätzliche Codezeilen, die Sie jedes Mal schreiben müssen, wenn Sie einen Dienst aufrufen, und jetzt, wenn jemand sagt, dass sie auf ein Problem gestoßen sind, wissen Sie genau, was das Problem war, ob es ein Fehler war oder ob es nur langsam lief. Sie können die Ursache des Problems lokalisieren, ohne sich in einen Server zu setzen oder die Protokollierung nach dem Fehler zu aktivieren, und hoffen, ihn erneut zu erstellen.

## <a name="dependency-injection-in-the-fix-it-app"></a>Abhängigkeitsinjektion in der Fix It-App

Sie fragen sich vielleicht, wie der Repository-Konstruktor im obigen Beispiel die Protokollschnittstellenimplementierung erhält:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

Um die Schnittstelle mit der Implementierung zu verdrahten, verwendet die App [Abhängigkeitsinjektion (DI)](http://en.wikipedia.org/wiki/Dependency_injection)mit [AutoFac](http://autofac.org/). DI ermöglicht es Ihnen, ein Objekt zu verwenden, das auf einer Schnittstelle an vielen Stellen im gesamten Code basiert, und müssen nur an einer Stelle die Implementierung angeben, die verwendet wird, wenn die Schnittstelle instanziiert wird. Dies erleichtert das Ändern der Implementierung: Sie können z. B. den System.Diagnostics Logger durch einen NLog-Logger ersetzen. Oder für automatisierte Tests möchten Sie vielleicht eine Mock-Version des Loggers ersetzen.

Die Fix It-Anwendung verwendet DI in allen Repositorys und auf allen Controllern. Die Konstruktoren der Controllerklassen erhalten eine *ITaskRepository-Schnittstelle* auf die gleiche Weise, wie das Repository eine Loggerschnittstelle erhält:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

Die App verwendet die AutoFac DI-Bibliothek, um automatisch *TaskRepository-* und *Logger-Instanzen* für diese Konstruktoren bereitzustellen.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

Dieser Code sagt im Grunde, dass überall, wo ein Konstruktor eine *ILogger-Schnittstelle* benötigt, in einer Instanz der *Logger-Klasse* übergeben und wann immer er eine *IFixItTaskRepository-Schnittstelle* benötigt, in einer Instanz der *FixItTaskRepository-Klasse* übergeben wird.

[AutoFac](http://autofac.org/) ist eines von vielen Abhängigkeitsinjektionsframeworks, die Sie verwenden können. Eine weitere beliebte ist [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), die von Microsoft Patterns and Practices empfohlen und unterstützt wird.

## <a name="built-in-logging-support-in-azure"></a>Integrierte Protokollierungsunterstützung in Azure

Azure unterstützt die folgenden Arten der [Protokollierung für Web-Apps in Azure App Service:](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)

- System.Diagnostics-Ablaufverfolgung (Sie können die Ebenen ein- und ausschalten und im Flug festlegen, ohne die Site neu zu starten).
- Windows-Ereignisse.
- IIS-Protokolle (HTTP/FREB).

Azure unterstützt die folgenden Arten der [Protokollierung in Cloud Services:](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)

- System.Diagnostics-Ablaufverfolgung.
- Leistungsindikatoren.
- Windows-Ereignisse.
- IIS-Protokolle (HTTP/FREB).
- Benutzerdefinierte Verzeichnisüberwachung.

Die Fix It-App verwendet System.Diagnostics-Ablaufverfolgung. Alles, was Sie tun müssen, um System.Diagnostics-Protokollierung in einer Web-App zu aktivieren, ist einen Schalter im Portal zu kippen oder die REST-API aufzurufen. Klicken Sie im Portal auf die Registerkarte **Konfiguration** für Ihre Website, und scrollen Sie nach unten, um den Abschnitt **Anwendungsdiagnose anzuzeigen.** Sie können die Anmeldung ein- oder ausschalten und die gewünschte Protokollierungsebene auswählen. Sie können Azure die Protokolle in das Dateisystem oder in ein Speicherkonto schreiben lassen.

![App-Diagnose und Standortdiagnose auf registerkarte Konfigurieren](monitoring-and-telemetry/_static/image24.png)

Nachdem Sie die Protokollierung in Azure aktiviert haben, können Sie Protokolle im Visual Studio-Ausgabefenster anzeigen, während sie erstellt werden.

![Streaming-Protokolle-Menü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![Streaming-Protokolle-Menü](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

Sie können auch Protokolle in Ihr Speicherkonto schreiben lassen und diese mit jedem Tool anzeigen, das auf den Azure Storage Table-Dienst zugreifen kann, z. **B. Server Explorer** in Visual Studio oder [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).

![Protokolle im Server-Explorer](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>Zusammenfassung

Es ist wirklich einfach, ein sofort einsatzbereites Telemetriesystem, die Instrumentenprotokollierung in Ihrem eigenen Code und die Konfiguration der Protokollierung in Azure zu implementieren. Und wenn Sie Produktionsprobleme haben, hilft Ihnen die Kombination aus einem Telemetriesystem und benutzerdefinierten Protokollen, Probleme schnell zu lösen, bevor sie zu hauptgestellten Problemen für Ihre Kunden werden.

Im [nächsten Kapitel](transient-fault-handling.md) werden wir untersuchen, wie vorübergehende Fehler behandelt werden, damit sie nicht zu Produktionsproblemen werden, die Sie untersuchen müssen.

## <a name="resources"></a>Ressourcen

Weitere Informationen finden Sie in den folgenden Ressourcen.

Dokumentation hauptsächlich über Telemetrie:

- [Microsoft-Muster und -Praktiken - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx). Weitere Informationen finden Sie unter Anleitung zur Instrumentierung und Telemetrie, Anleitung zur Dienstmessung, Muster zur Überwachung des Integritätsendpunkts und Muster zur Wiederkonfiguration von Laufzeiten.
- [Penny Pinching in der Cloud: Aktivieren neuer Relic Performance Monitoring auf Azure-Websites](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx).
- [Bewährte Methoden für den Entwurf großer Dienste in Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Whitepaper von Mark Simms und Michael Thomassy. Weitere Informationen finden Sie im Abschnitt Telemetrie und Diagnose.
- [Entwicklung der nächsten Generation mit Application Insights](https://msdn.microsoft.com/magazine/dn683794.aspx). MSDN Magazin Artikel.

Dokumentation hauptsächlich über protokollieren:

- [Semantic Logging Application Block (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neil Mackenzie stellt mit SLAB die Argumente für die semantische Protokollierung vor.
- [Erstellen strukturierter und aussagekräftiger Protokolle mit semantischer Protokollierung](https://channel9.msdn.com/Events/Build/2013/3-336). (Video) Julian Dominguez stellt mit SLAB den Fall für semantische Protokollierung vor.
- [EF6 SQL-Protokollierung – Teil 1: Einfache Protokollierung](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). Arthur Vickers zeigt, wie Abfragen protokolliert werden, die von Entity Framework in EF 6 ausgeführt werden.
- [Verbindungssicherheit und Befehlsabfangen mit dem Entity Framework in einer ASP.NET MVC-Anwendung](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). Viertens in einer neunteiligen Lernprogrammreihe wird gezeigt, wie Sie die Abfangfunktion des Befehls EF 6 verwenden, um SQL-Befehle zu protokollieren, die von Entity Framework an die Datenbank gesendet werden.
- Verbessern Sie die [Protokollierung mit den C-5.0-Aufrufer-Infoattributen](http://www.dotnetcurry.com/showarticle.aspx?ID=972). So protokollieren Sie einfach den Namen der aufrufenden Methode, ohne sie in Literale zu codieren oder Reflektion zu verwenden, um sie manuell zu erhalten.

Dokumentation hauptsächlich zur Fehlerbehebung:

- [Azure Troubleshooting &amp; Debugging Blog](https://blogs.msdn.com/b/kwill/).
- [AzureTools – Das Diagnosedienstprogramm, das vom Azure Developer Support Team verwendet wird.](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true) Stellt einen Downloadlink für ein Tool vor, das auf einer Azure-VM zum Herunterladen und Ausführen einer Vielzahl von Diagnose- und Überwachungstools verwendet werden kann. Nützlich, wenn Sie ein Problem auf einer bestimmten VM diagnostizieren müssen.
- [Beheben Sie eine Web-App in Azure App Service mit Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). Ein Schritt-für-Schritt-Tutorial für die ersten Schritte mit DerSystem.Diagnostics-Ablaufverfolgung und Remote-Debugging.

Videos:

- [FailSafe: Erstellen skalierbarer, widerstandsfähiger Cloud-Services](https://channel9.msdn.com/Series/FailSafe). Neunteilige Serie von Ulrich Homann, Marc Mercuri und Mark Simms. Präsentiert allgemeine Konzepte und Architekturprinzipien auf sehr zugängliche und interessante Weise mit Geschichten aus der Erfahrung des Microsoft Customer Advisory Team (CAT) mit tatsächlichen Kunden. In den Episoden 4 und 9 geht es um Überwachung und Telemetrie. Episode 9 enthält eine Übersicht über die Überwachungsdienste MetricsHub, AppDynamics, New Relic und PagerDuty.
- [Groß erstellen: Lehren aus Azure-Kunden - Teil II](https://channel9.msdn.com/Events/Build/2012/3-030). Mark Simms spricht über das Entwerfen für Misserfolg und das Instrumentieren von allem. Ähnlich wie bei der Failsafe-Serie, geht aber mehr How-to-Details.

Codebeispiel:

- [Cloud Dienstgrundlagen in Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Beispielanwendung, die vom Microsoft Azure-Kundenberatungsteam erstellt wurde. Veranschaulicht sowohl Telemetrie- als auch Protokollierungspraktiken, wie in den folgenden Artikeln erläutert. Das Beispiel implementiert die Anwendungsprotokollierung mithilfe von [NLog](http://nlog-project.org/). Ausführliche Dokumentation finden Sie in der [Serie von vier TechNet-Wiki-Artikeln über Telemetrie und Protokollierung](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon).

> [!div class="step-by-step"]
> [Zurück](design-to-survive-failures.md)
> [Weiter](transient-fault-handling.md)
