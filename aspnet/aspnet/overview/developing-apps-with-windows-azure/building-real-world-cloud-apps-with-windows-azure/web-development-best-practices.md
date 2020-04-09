---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Best Practices für die Webentwicklung (Erstellen von Echtzeit-Cloud-Apps mit Azure) | Microsoft Docs
author: MikeWasson
description: Das Building Real World Cloud Apps mit Azure E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es erklärt 13 Muster und Praktiken, die er...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675640"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Best Practices für die Webentwicklung (Erstellen von Cloud-Apps in der realen Welt mit Azure)

von [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), Tom [Dykstra](https://github.com/tdykstra)

[Fix It Project herunterladen](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) oder [E-Book herunterladen](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Das **Building Real World Cloud Apps mit Azure** E-Book basiert auf einer Präsentation, die von Scott Guthrie entwickelt wurde. Es werden 13 Muster und Vorgehensweisen erläutert, die Ihnen bei der erfolgreichen Entwicklung von Web-Apps für die Cloud helfen können. Informationen zum E-Book finden Sie [im ersten Kapitel](introduction.md).

In den ersten drei Mustern ging es um die Einrichtung eines agilen Entwicklungsprozesses; Der Rest dreht sich um Architektur und Code. Dies ist eine Sammlung von Best Practices für die Webentwicklung:

- [Zustandslose Webserver](#stateless) hinter einem intelligenten Load Balancer.
- [Vermeiden Sie den Sitzungsstatus](#sessionstate) (oder verwenden Sie verteilten Cache anstelle einer Datenbank, wenn Sie ihn nicht vermeiden können).
- [Verwenden Sie ein CDN](#cdn) zum Edge-Cache statischer Dateielemente (Bilder, Skripts).
- [Verwenden Sie die asynchrone Unterstützung von .NET 4.5,](#async) um das Blockieren von Aufrufen zu vermeiden.

Diese Vorgehensweisen gelten für alle Web-Entwicklungen, nicht nur für Cloud-Apps, aber sie sind besonders wichtig für Cloud-Apps. Sie helfen Ihnen dabei, die hochflexible Skalierung der Cloud-Umgebung optimal zu nutzen. Wenn Sie diese Vorgehensweisen nicht befolgen, stoßen Sie beim Versuch, Ihre Anwendung zu skalieren, auf Einschränkungen.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Zustandslose Web-Ebene hinter einem intelligenten Load Balancer

*Zustandslose Webebene* bedeutet, dass Sie keine Anwendungsdaten im Webserverspeicher oder Dateisystem speichern. Wenn Sie Ihre Web-Tier-Statuslosigkeit beibehalten, können Sie sowohl ein besseres Kundenerlebnis bieten als auch Geld sparen:

- Wenn die Webebene zustandslos ist und sich hinter einem Load Balancer befindet, können Sie schnell auf Änderungen im Anwendungsdatenverkehr reagieren, indem Sie Server dynamisch hinzufügen oder entfernen. In der Cloud-Umgebung, in der Sie nur für Serverressourcen bezahlen, solange Sie sie tatsächlich verwenden, kann diese Fähigkeit, auf Nachfrageänderungen zu reagieren, zu enormen Einsparungen führen.
- Eine zustandslose Webebene ist architektonisch viel einfacher, die Anwendung zu skalieren. Auch dadurch können Sie schneller auf Skalierungsanforderungen reagieren und weniger Geld für Entwicklung und Tests ausgeben.
- Cloud-Server müssen, wie lokale Server, gelegentlich gepatcht und neu gestartet werden. und wenn die Webebene zustandslos ist, führt das erneute Routing des Datenverkehrs beim vorübergehenden Ausfall eines Servers nicht zu Fehlern oder unerwartetem Verhalten.

Die meisten realen Anwendungen müssen den Status für eine Websitzung speichern. der Hauptpunkt ist, es nicht auf dem Webserver zu speichern. Sie können den Status auf andere Weise speichern, z. B. auf dem Client in Cookies oder aout of process server-side in ASP.NET Sitzungsstatus mithilfe eines Cacheanbieters. Sie können Dateien im [Windows Azure Blob-Speicher](unstructured-blob-storage.md) anstelle des lokalen Dateisystems speichern.

Ein Beispiel dafür, wie einfach es ist, eine Anwendung in Windows Azure-Websites zu skalieren, wenn Ihre Webebene zustandslos ist, finden Sie auf der Registerkarte **Skalieren** für eine Windows Azure-Website im Verwaltungsportal:

![Registerkarte "Skalieren"](web-development-best-practices/_static/image1.png)

Wenn Sie Webserver hinzufügen möchten, können Sie einfach den Schieberegler für die Instanzanzahl nach rechts ziehen. Legen Sie 5 fest, und klicken Sie auf **Speichern**, und innerhalb von Sekunden haben Sie 5 Webserver in Windows Azure, die den Datenverkehr Ihrer Website verarbeiten.

![Fünf Instanzen](web-development-best-practices/_static/image2.png)

Sie können den Instance-Countdown genauso einfach auf 3 oder zurück auf 1 festlegen. Wenn Sie zurückskalieren, sparen Sie sofort Geld, da Windows Azure minutenweise und nicht stundenweise berechnet.

Sie können Windows Azure auch anweisen, die Anzahl der Webserver basierend auf der CPU-Auslastung automatisch zu erhöhen oder zu verringern. Im folgenden Beispiel, wenn die CPU-Auslastung unter 60 % sinkt, wird die Anzahl der Webserver auf mindestens 2 sinken, und wenn die CPU-Auslastung über 80 % steigt, wird die Anzahl der Webserver auf maximal 4 erhöht.

![Skalierung nach CPU-Auslastung](web-development-best-practices/_static/image3.png)

Oder was ist, wenn Sie wissen, dass Ihre Website nur während der Arbeitszeit ausgelastet ist? Sie können Windows Azure anweisen, mehrere Server tagsüber auszuführen und auf einen einzelnen Server abends, nächte- und wochenenden zu verringern. Die folgende Serie von Screenshots zeigt, wie Sie die Website so einrichten, dass ein Server innerhalb weniger Zeiten und 4 Server während der Arbeitszeit von 8.00 bis 17.00 Uhr ausgeführt wird.

![Skalierung nach Zeitplan](web-development-best-practices/_static/image4.png)

![Zeitplanzeiten festlegen](web-development-best-practices/_static/image5.png)

![Tagesplan](web-development-best-practices/_static/image6.png)

![Weeknight Zeitplan](web-development-best-practices/_static/image7.png)

![Wochenendplan](web-development-best-practices/_static/image8.png)

Und natürlich kann all dies sowohl in Skripten als auch im Portal erfolgen.

Die Möglichkeit Ihrer Anwendung, horizontal zu skalieren, ist in Windows Azure nahezu unbegrenzt, solange Sie Hindernisse für das dynamische Hinzufügen oder Entfernen von Server-VMs vermeiden, indem Sie die Webebene statuslos halten.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Vermeiden des Sitzungsstatus

Im praktischen Einsatz von Cloud-Apps lässt sich das Speichern von Zustandsinformationen für eine Benutzersitzung oft nicht vermeiden. Allerdings beeinträchtigen einige Herangehensweisen die Leistung und Skalierbarkeit stärker als andere. Wenn Sie einen Sitzungszustand speichern müssen, ist es am besten, die Menge der Zustandsinformationen niedrig zu halten und sie in Cookies zu speichern. Wenn dies nicht möglich ist, besteht die nächstbeste Lösung darin, ASP.NET Sitzungsstatus mit einem Anbieter für [verteilten In-Memory-Cache](distributed-caching.md#sessionstate)zu verwenden. Die schlechteste Lösung im Hinblick auf Leistung und Skalierbarkeit wäre es, einen datenbankbasierten Sitzungszustandsanbieter zu verwenden.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Verwenden eines CDN zum Zwischenspeichern statischer Dateielemente

CDN ist ein Akronym für Content Delivery Network. Sie stellen statische Dateielemente wie Bilder und Skriptdateien an einen CDN-Anbieter zur Verfügung, und der Anbieter speichert diese Dateien in Rechenzentren auf der ganzen Welt zwischen, sodass sie überall dort, wo Benutzer auf Ihre Anwendung zugreifen, relativ schnelle Antworten und eine geringe Latenz für die zwischengespeicherten Assets erhalten. Dies beschleunigt die Gesamtladezeit der Website und reduziert die Last auf Ihren Webservern. CDNs sind besonders wichtig, wenn Sie ein Publikum erreichen, das geografisch weit verbreitet ist.

Windows Azure verfügt über ein CDN, und Sie können andere CDNs in einer Anwendung verwenden, die in Windows Azure oder einer beliebigen Webhostingumgebung ausgeführt wird.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Verwenden Sie die asynchrone Unterstützung von .NET 4.5, um das Blockieren von Aufrufen zu vermeiden

.NET 4.5 hat die Programmiersprachen "C" und "VB" erweitert, um die asynchrone Handhabung von Aufgaben wesentlich zu vereinfachen. Der Vorteil der asynchronen Programmierung ist nicht nur für parallele Verarbeitungssituationen, z. B. wenn Sie mehrere Webdienstaufrufe gleichzeitig starten möchten. Außerdem kann Ihr Webserver unter hohen Auslastungsbedingungen effizienter und zuverlässiger arbeiten. Auf einem Webserver ist nur eine begrenzte Anzahl von Threads verfügbar, und unter hohen Auslastungsbedingungen, wenn alle Threads verwendet werden, müssen eingehende Anforderungen warten, bis Threads freigegeben werden. Wenn Ihr Anwendungscode Aufgaben wie Datenbankabfragen und Webdienstaufrufe nicht asynchron verarbeitet, sind viele Threads unnötig gebunden, während der Server auf eine E/A-Antwort wartet. Dadurch wird die Menge des Datenverkehrs begrenzt, den der Server unter hohen Auslastungsbedingungen verarbeiten kann. Bei der asynchronen Programmierung werden Threads, die auf die Rückgabe von Daten durch einen Webdienst oder eine Datenbank warten, für den Dienst neuer Anforderungen freigegeben, bis die Daten empfangen werden. In einem ausgelasteten Webserver können dann hunderte oder tausende von Anforderungen zeitnah verarbeitet werden, die andernfalls auf die Freigegebene von Threads warten würden.

Wie Sie bereits gesehen haben, ist es so einfach, die Anzahl der Webserver, die Ihre Website verarbeiten, zu verringern, wie sie zu erhöhen. Wenn ein Server also einen höheren Durchsatz erzielen kann, benötigen Sie nicht so viele von ihnen, und Sie können Ihre Kosten senken, da Sie weniger Server für ein bestimmtes Datenverkehrsvolumen benötigen, als Sie es sonst tun würden.

Die Unterstützung für das asynchrone Programmiermodell .NET 4.5 ist in ASP.NET 4.5 für Web Forms, MVC und Web API enthalten. in Entity Framework 6 und in der [Windows Azure Storage-API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx).

### <a name="async-support-in-aspnet-45"></a>Async-Unterstützung in ASP.NET 4.5

In ASP.NET 4.5 wurde die Unterstützung für asynchrone Programmierung nicht nur der Sprache, sondern auch den MVC-, Webforms- und Web-API-Frameworks hinzugefügt. Beispielsweise empfängt eine ASP.NET MVC-Controller-Aktionsmethode Daten aus einer Webanforderung und übergibt die Daten an eine Ansicht, die dann den HTML-Code erstellt, der an den Browser gesendet werden soll. Häufig muss die Aktionsmethode Daten aus einer Datenbank oder einem Webdienst abrufen, um sie auf einer Webseite anzuzeigen oder in einer Webseite eingegebene Daten zu speichern. In diesen Szenarien ist es einfach, die Aktionsmethode asynchron zu machen: Anstatt ein *ActionResult-Objekt* zurückzugeben, geben Sie *&lt;Task ActionResult&gt; * zurück und markieren die Methode mit dem *Schlüsselwort async.* Wenn eine Codezeile innerhalb der Methode einen Vorgang startet, der Wartezeiten mit sich bringt, markieren Sie ihn mit dem Schlüsselwort await.

Hier ist eine einfache Aktionsmethode, die eine Repository-Methode für eine Datenbankabfrage aufruft:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

Und hier ist die gleiche Methode, die den Datenbankaufruf asynchron verarbeitet:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

Unter den Covern generiert der Compiler den entsprechenden asynchronen Code. Wenn die Anwendung den `FindTaskByIdAsync`Aufruf von `FindTask` ausführt, führt ASP.NET die Anforderung aus, und entlädt dann den Arbeitsthread und stellt ihn für die Verarbeitung einer anderen Anforderung zur Verfügung. Wenn `FindTask` die Anforderung abgeschlossen ist, wird ein Thread neu gestartet, um die Verarbeitung des Codes fortzusetzen, der nach diesem Aufruf erfolgt. Während der Zwischenzeit `FindTask` zwischen dem Zeitpunkt, an dem die Anforderung initiiert wird, und dem Zeitpunkt, an dem die Daten zurückgegeben werden, steht Ihnen ein Thread zur Verfügung, um nützliche Arbeit zu leisten, die andernfalls gebunden wäre und auf die Antwort wartet.

Es gibt einen gewissen Overhead für asynchronen Code, aber unter Bedingungen mit niedrigem Auslastung ist dieser Overhead vernachlässigbar, während Sie unter Bedingungen mit hoher Auslastung Anforderungen verarbeiten können, die andernfalls auf verfügbare Threads warten würden.

Seit ASP.NET 1.1 war es möglich, diese Art der asynchronen Programmierung zu machen, aber es war schwierig zu schreiben, fehleranfällig und schwierig zu debuggen. Nun, da wir die Codierung dafür in ASP.NET 4.5 vereinfacht haben, gibt es keinen Grund mehr, es nicht mehr zu tun.

### <a name="async-support-in-entity-framework-6"></a>Async-Unterstützung in Entity Framework 6

Als Teil der async-Unterstützung in 4.5 haben wir asynchrone Unterstützung für Webdienstaufrufe, Sockets und Dateisystem-E/A-Dienste bereitgestellt, aber das häufigste Muster für Webanwendungen ist es, eine Datenbank zu treffen, und unsere Datenbibliotheken unterstützten async nicht. Jetzt fügt Entity Framework 6 asynchrone Unterstützung für den Datenbankzugriff hinzu.

In Entity Framework 6 verfügen alle Methoden, die dazu führen, dass eine Abfrage oder ein Befehl an die Datenbank gesendet wird, über asynchrone Versionen. Das Beispiel hier zeigt die *Find* asynchrone Version der Find-Methode.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

Und diese asynchrone Unterstützung funktioniert nicht nur für Einfügungen, Löschungen, Aktualisierungen und einfache Funde, sondern auch für LINQ-Abfragen:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

Es gibt `Async` eine Version `ToList` der Methode, da in diesem Code die Methode ist, die bewirkt, dass eine Abfrage an die Datenbank gesendet wird. Die `Where` `OrderByDescending` und Methoden konfigurieren nur `ToListAsync` die Abfrage, während die Methode `result` die Abfrage ausführt und die Antwort in der Variablen speichert.

## <a name="summary"></a>Zusammenfassung

Sie können die hier beschriebenen Best Practices für die Webentwicklung in jedem Webprogrammierungsframework und jeder Cloudumgebung implementieren, aber wir verfügen über Tools in ASP.NET und Windows Azure, um dies zu vereinfachen. Wenn Sie diesen Mustern folgen, können Sie Ihre Webebene einfach horizontal skalieren, und Sie werden Ihre Ausgaben minimieren, da jeder Server in der Lage sein wird, mehr Datenverkehr zu verarbeiten.

Im [nächsten Kapitel](single-sign-on.md) wird untersucht, wie die Cloud Single Sign-On-Szenarien ermöglicht.

## <a name="resources"></a>Ressourcen

Weitere Informationen finden Sie in den folgenden Ressourcen.

Zustandslose Webserver:

- Microsoft Patterns and Practices - Anleitung zum [automatischen Skalieren](https://msdn.microsoft.com/library/dn589774.aspx).
- [Deaktivieren der Instance-Affinität von ARR in Windows Azure-Websites](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/). Blogbeitrag von Erez Benari, erläutert die Sitzungsaffinität in Windows Azure-Websites.

Cdn:

- [FailSafe: Erstellen skalierbarer, widerstandsfähiger Cloud-Services](https://channel9.msdn.com/Series/FailSafe). Neunteilige Videoserien von Ulrich Homann, Marc Mercuri und Mark Simms. Sehen Sie die CDN-Diskussion in Folge 3 ab 1:34:00 Uhr.
- [Microsoft Patterns and Practices Statisches Content Hosting-Muster](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN Bewertungen](http://www.cdnreviews.com/). Überblick über viele CDNs.

Asynchrone Programmierung:

- [Verwenden von asynchronen Methoden in ASP.NET MVC 4](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Tutorial von Rick Anderson.
- [Asynchrone Programmierung mit Async und Await (C- und Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). MSDN-Whitepaper, in dem die Gründe für die asynchrone Programmierung erläutert werden, wie sie in ASP.NET 4.5 funktioniert und wie Code zu ihrer Implementierung geschrieben wird.
- [Entity Framework Async-Abfrage und -Speicherung](https://msdn.microsoft.com/data/jj819165)
- [Erstellen ASP.NET Webanwendungen mit Async](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). Video-Präsentation von Rowan Miller. Enthält eine grafische Demonstration, wie asynchrone Programmierung einen dramatischen Anstieg des Webserverdurchsatzes unter hohen Auslastungsbedingungen ermöglichen kann.
- [FailSafe: Erstellen skalierbarer, widerstandsfähiger Cloud-Services](https://channel9.msdn.com/Series/FailSafe). Neunteilige Videoserien von Ulrich Homann, Marc Mercuri und Mark Simms. Diskussionen über die Auswirkungen asynchroner Programmierung auf die Skalierbarkeit finden Sie in Episode 4 und Folge 8.
- [Die Magie der Verwendung von asynchronen Methoden in ASP.NET 4.5 plus einem wichtigen gotcha](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Blogbeitrag von Scott Hanselman, in erster Linie über die Verwendung von async in ASP.NET Web Forms-Anwendungen.

Weitere Best Practices für die Webentwicklung finden Sie in den folgenden Ressourcen:

- [Die Fix It-Beispielanwendung - Best Practices](the-fix-it-sample-application.md#bestpractices). Der Anhang zu diesem E-Book listet eine Reihe von Best Practices auf, die in der Fix It-Anwendung implementiert wurden.
- [Webentwickler-Checkliste](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Zurück](continuous-integration-and-continuous-delivery.md)
> [Weiter](single-sign-on.md)
