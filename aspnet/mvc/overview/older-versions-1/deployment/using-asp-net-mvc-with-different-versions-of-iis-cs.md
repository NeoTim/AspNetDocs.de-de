---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: Verwenden ASP.NET MVC mit verschiedenen Versionen von IIS (C) | Microsoft Docs
author: rick-anderson
description: In diesem Tutorial erfahren Sie, wie Sie ASP.NET MVC und URL Routing mit verschiedenen Versionen von Internetinformationsdiensten verwenden. Sie lernen verschiedene Strategien...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c239c3c7cbbaae5d9c5e4dd91dc66ff4e98bcfb
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542078"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>Verwendung von ASP.NET MVC mit verschiedenen IIS-Versionen (C#)

von [Microsoft](https://github.com/microsoft)

> In diesem Tutorial erfahren Sie, wie Sie ASP.NET MVC und URL Routing mit verschiedenen Versionen von Internetinformationsdiensten verwenden. Sie lernen verschiedene Strategien für die Verwendung ASP.NET MVC mit IIS 7.0 (klassischer Modus), IIS 6.0 und früheren Versionen von IIS.

Das ASP.NET MVC-Framework hängt vom ASP.NET Routing ab, browseranforderungen an Controlleraktionen weiterzuleiten. Um ASP.NET Routing nutzen zu können, müssen Sie möglicherweise zusätzliche Konfigurationsschritte auf Ihrem Webserver ausführen. Alles hängt von der Version von Internet Information Services (IIS) und dem Anforderungsverarbeitungsmodus für Ihre Anwendung ab.

Hier ist eine Zusammenfassung der verschiedenen Versionen von IIS:

- IIS 7.0 (integrierter Modus) - Keine spezielle Konfiguration erforderlich, um ASP.NET Routing zu verwenden.
- IIS 7.0 (klassischer Modus) - Sie müssen eine spezielle Konfiguration durchführen, um ASP.NET Routing zu verwenden.
- IIS 6.0 oder darunter – Sie müssen eine spezielle Konfiguration durchführen, um ASP.NET Routing zu verwenden.

Die neueste Version von IIS ist Version 7.5 (auf Win7). IIS 7 von IIS ist in Windows Server 2008 AND VISTA/SP1 und höher enthalten. Sie können IIS 7.0 auch auf jeder beliebigen Version des [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)Vista-Betriebssystems außer Home Basic installieren (siehe ).

IIS 7.0 unterstützt zwei Modi für die Verarbeitung von Anforderungen. Sie können den integrierten Modus oder den klassischen Modus verwenden. Sie müssen keine speziellen Konfigurationsschritte ausführen, wenn Sie IIS 7.0 im integrierten Modus verwenden. Sie müssen jedoch eine zusätzliche Konfiguration durchführen, wenn Sie IIS 7.0 im klassischen Modus verwenden.

Microsoft Windows Server 2003 enthält IIS 6.0. Sie können IIS 6.0 nicht auf IIS 7.0 aktualisieren, wenn Sie das Betriebssystem Windows Server 2003 verwenden. Sie müssen zusätzliche Konfigurationsschritte ausführen, wenn Sie IIS 6.0 verwenden.

Microsoft Windows XP Professional enthält IIS 5.1. Sie müssen zusätzliche Konfigurationsschritte ausführen, wenn Sie IIS 5.1 verwenden.

Schließlich enthält Microsoft Windows 2000 und Microsoft Windows 2000 Professional IIS 5.0. Sie müssen zusätzliche Konfigurationsschritte ausführen, wenn Sie IIS 5.0 verwenden.

## <a name="integrated-versus-classic-mode"></a>Integrierter im Vergleich zum klassischen Modus

IIS 7.0 kann Anforderungen mit zwei verschiedenen Anforderungsverarbeitungsmodi verarbeiten: integriert und klassisch. Integrierter Modus bietet eine bessere Leistung und mehr Funktionen. Der klassische Modus ist für die Abwärtskompatibilität mit früheren IIS-Versionen enthalten.

Der Anforderungsverarbeitungsmodus wird vom Anwendungspool bestimmt. Sie können bestimmen, welcher Verarbeitungsmodus von einer bestimmten Webanwendung verwendet wird, indem Sie den der Anwendung zugeordneten Anwendungspool bestimmen. Folgen Sie diesen Schritten:

1. Starten des Internet Information Services Managers
2. Wählen Sie im Fenster Verbindungen eine Anwendung aus.
3. Klicken Sie im Fenster Aktionen auf den Link **Grundeinstellungen,** um das Dialogfeld Anwendung bearbeiten zu öffnen (siehe Abbildung 1)
4. Beachten Sie den ausgewählten Anwendungspool.

Standardmäßig ist IIS so konfiguriert, dass es zwei Anwendungspools unterstützt: **DefaultAppPool** und **Classic .NET AppPool**. Wenn DefaultAppPool ausgewählt ist, wird Ihre Anwendung im integrierten Anforderungsverarbeitungsmodus ausgeführt. Wenn Classic .NET AppPool ausgewählt ist, wird Ihre Anwendung im klassischen Anforderungsverarbeitungsmodus ausgeführt.

[![Dialogfeld „New Project“ (Neues Projekt)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**Abbildung 1**: Erkennen des Anforderungsverarbeitungsmodus ([Klicken Sie hier, um ein Bild in voller Größe anzuzeigen](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))

Beachten Sie, dass Sie den Anforderungsverarbeitungsmodus im Dialogfeld Anwendung bearbeiten ändern können. Klicken Sie auf die Schaltfläche Auswählen, und ändern Sie den der Anwendung zugeordneten Anwendungspool. Stellen Sie fest, dass es Kompatibilitätsprobleme beim Ändern einer ASP.NET Anwendung vom klassischen in den integrierten Modus gibt. Weitere Informationen finden Sie in den folgenden Artikeln:

- Aktualisieren ASP.NET 1.1 auf IIS 7.0 unter Windows Vista und Windows Server 2008 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET Integration mit IIS 7.0 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

Wenn eine ASP.NET Anwendung den DefaultAppPool verwendet, müssen Sie keine zusätzlichen Schritte ausführen, um ASP.NET Routing (und damit ASP.NET MVC) zum Funktionieren zu bringen. Wenn die ASP.NET Anwendung jedoch für die Verwendung von Classic .NET AppPool konfiguriert ist und dann weiterlesen kann, müssen Sie noch mehr zu tun haben.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>Verwenden ASP.NET MVC mit älteren Versionen von IIS

Wenn Sie ASP.NET MVC mit einer älteren Version von IIS als IIS 7.0 oder IIS 7.0 verwenden müssen, haben Sie zwei Möglichkeiten. Zunächst können Sie die Routingtabelle ändern, um Dateierweiterungen zu verwenden. Anstatt beispielsweise eine URL wie /Store/Details anzufordern, fordern Sie eine URL wie /Store.aspx/Details an.

Die zweite Option besteht darin, eine so genannte *Platzhalterskriptzuordnung*zu erstellen. Mit einer Platzhalterskriptzuordnung können Sie jede Anforderung dem ASP.NET-Frameworkzuordnens zuordnen.

Wenn Sie keinen Zugriff auf Ihren Webserver haben (z. B. ihre ASP.NET MVC-Anwendung wird von einem Internetdienstanbieter gehostet), müssen Sie die erste Option verwenden. Wenn Sie die Darstellung Ihrer URLs nicht ändern möchten und Zugriff auf Ihren Webserver haben, können Sie die zweite Option verwenden.

Wir untersuchen jede Option im Detail in den folgenden Abschnitten.

## <a name="adding-extensions-to-the-route-table"></a>Hinzufügen von Erweiterungen zur Routentabelle

Die einfachste Möglichkeit, ASP.NET Routing mit älteren Versionen von IIS zu arbeiten, besteht darin, die Routingtabelle in der Datei Global.asax zu ändern. Die standardmäßige und unveränderte Datei Global.asax in Listing 1 konfiguriert eine Route namens Standardroute.

**Listing 1 - Global.asax (unverändert)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

Mit der in Liste 1 konfigurierten Standardroute können Sie URLs weiterleiten, die wie folgt aussehen:

/Home/Index

/Produkt/Details/3

/Produkt

Leider werden ältere Versionen von IIS diese Anforderungen nicht an das ASP.NET-Framework übergeben. Daher werden diese Anforderungen nicht an einen Controller weitergeleitet. Wenn Sie beispielsweise eine Browseranforderung für die URL /Home/Index stellen, wird die Fehlerseite in Abbildung 2 angezeigt.

[![Dialogfeld „New Project“ (Neues Projekt)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**Abbildung 2:** Empfangen eines 404 Not Found-Fehlers[(Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png)

Ältere Versionen von IIS ordnen nur bestimmte Anforderungen dem ASP.NET Framework zu. Die Anforderung muss für eine URL mit der richtigen Dateierweiterung sein. Beispielsweise wird eine Anforderung für /SomePage.aspx dem ASP.NET Framework zugeordnet. Eine Anforderung für /SomePage.htm ist jedoch nicht erforderlich.

Um ASP.NET Routing zu erledigen, müssen wir daher die Standardroute so ändern, dass sie eine Dateierweiterung enthält, die dem ASP.NET Framework zugeordnet ist.

Dies geschieht mit `registermvc.wsf`einem Skript mit dem Namen . Es wurde mit der ASP.NET MVC 1-Version in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`enthalten, aber ab ASP.NET 2 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)wurde dieses Skript in die ASP.NET Futures verschoben, verfügbar unter .

Durch ausführen dieses Skripts wird eine neue .mvc-Erweiterung mit IIS registriert. Nachdem Sie die Erweiterung .mvc registriert haben, können Sie Ihre Routen in der Datei Global.asax so ändern, dass die Routen die Erweiterung .mvc verwenden.

Die geänderte Datei Global.asax in Listing 2 funktioniert mit älteren Versionen von IIS.

**Listing 2 - Global.asax (modifiziert mit Erweiterungen)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**Wichtig:** Denken Sie daran, Ihre ASP.NET MVC-Anwendung erneut zu erstellen, nachdem Sie die Datei Global.asax geändert haben.

Es gibt zwei wichtige Änderungen an der Datei Global.asax in Listing 2. Es gibt jetzt zwei Routen, die in der Datei Global.asax definiert sind. Das URL-Muster für die Standardroute, die erste Route, sieht jetzt wie folgt aus:

.mvc/-action/

Durch das Hinzufügen der Erweiterung .mvc wird der Dateityp geändert, den das ASP.NET Routingmodul abfängt. Mit dieser Änderung leitet die ASP.NET MVC-Anwendung nun Anforderungen wie folgt:

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

Die zweite Route, die Root-Route, ist neu. Dieses URL-Muster für die Root-Route ist eine leere Zeichenfolge. Diese Route ist erforderlich, um Anforderungen, die mit dem Stamm Ihrer Anwendung gestellt wurden, abzugleichen. Die Root-Route entspricht z. B. einer Anforderung, die wie folgt aussieht:

[http://www.YourApplication.com/](http://www.YourApplication.com/)

Nachdem Sie diese Änderungen an der Routingtabelle vorgenommen haben, müssen Sie sicherstellen, dass alle Links in Ihrer Anwendung mit diesen neuen URL-Mustern kompatibel sind. Mit anderen Worten, stellen Sie sicher, dass alle Ihre Links die Erweiterung .mvc enthalten. Wenn Sie die Html.ActionLink()-Hilfsmethode verwenden, um Ihre Links zu generieren, sollten Sie keine Änderungen vornehmen müssen.

Anstatt das Skript registermvc.wcf zu verwenden, können Sie IIS eine neue Erweiterung hinzufügen, die dem ASP.NET Framework von Hand zugeordnet ist. Stellen Sie beim Hinzufügen einer neuen Erweiterung selbst sicher, dass das Kontrollkästchen Überprüfen, ob die **Datei vorhanden ist,** nicht aktiviert ist.

## <a name="hosted-server"></a>Gehosteter Server

Sie haben nicht immer Zugriff auf Ihren Webserver. Wenn Sie beispielsweise Ihre ASP.NET MVC-Anwendung über einen Internethostinganbieter hosten, haben Sie nicht unbedingt Zugriff auf IIS.

In diesem Fall sollten Sie eine der vorhandenen Dateierweiterungen verwenden, die dem ASP.NET Framework zugeordnet sind. Beispiele für Dateierweiterungen, die ASP.NET zugeordnet sind, sind die Erweiterungen .aspx, .axd und .ashx.

Beispielsweise verwendet die geänderte Datei Global.asax in Listing 3 die Erweiterung .aspx anstelle der Erweiterung .mvc.

**Listing 3 - Global.asax (modifiziert mit ASPX-Erweiterungen)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

Die Datei Global.asax in Listing 3 ist genau die gleiche wie die vorherige Datei Global.asax, mit Ausnahme der Tatsache, dass sie die Erweiterung .aspx anstelle der Erweiterung .mvc verwendet. Sie müssen keine Einrichtung auf Ihrem Remote-Webserver durchführen, um die ASPX-Erweiterung zu verwenden.

## <a name="creating-a-wildcard-script-map"></a>Erstellen einer Wildcard-Skriptzuordnung

Wenn Sie die URLs für Ihre ASP.NET MVC-Anwendung nicht ändern möchten und Zugriff auf Ihren Webserver haben, haben Sie eine zusätzliche Option. Sie können eine Platzhalterskriptzuordnung erstellen, die alle Anforderungen an den Webserver dem ASP.NET-Framework zuordnet. Auf diese Weise können Sie die Standard-ASP.NET MVC-Routingtabelle mit IIS 7.0 (im klassischen Modus) oder IIS 6.0 verwenden.

Beachten Sie, dass diese Option dazu führt, dass IIS jede Anforderung an den Webserver abfängt. Dazu gehören Anforderungen für Bilder, klassische ASP-Seiten und HTML-Seiten. Daher hat das Aktivieren einer Platzhalterskriptzuordnung ASP.NET Auswirkungen auf die Leistung.

So aktivieren Sie eine Platzhalterskriptzuordnung für IIS 7.0:

1. Wählen Sie Ihre Anwendung im Fenster Verbindungen aus
2. Stellen Sie sicher, dass die **Features-Ansicht** ausgewählt ist.
3. Doppelklicken Sie auf die Schaltfläche **Handler Mappings**
4. Klicken Sie auf den Link **Platzhalter-Skriptzuordnung hinzufügen** (siehe Abbildung 3)
5. Geben Sie den Pfad\_zur Datei aspnet isapi.dll ein (Sie können diesen Pfad aus der PageHandlerFactory-Skriptzuordnung kopieren)
6. Geben Sie den Namen MVC ein
7. Klicken Sie auf die **Schaltfläche OK**

[![Dialogfeld „New Project“ (Neues Projekt)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**Abbildung 3:** Erstellen einer Platzhalterskriptzuordnung mit IIS 7.0([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png)

Führen Sie die folgenden Schritte aus, um eine Platzhalterskriptzuordnung mit IIS 6.0 zu erstellen:

1. Klicken Sie mit der rechten Maustaste auf eine Website, und wählen Sie Eigenschaften aus
2. Wählen Sie die Registerkarte **Home Verzeichnis**
3. Klicken Sie auf die Schaltfläche **Konfiguration**
4. Wählen Sie die Registerkarte **Mappings**
5. Klicken Sie auf die Schaltfläche **Einfügen** (siehe Abbildung 4)
6. Fügen Sie den Pfad\_zur Datei aspnet isapi.dll in das Feld Ausführbare Datei ein (Sie können diesen Pfad aus der Skriptzuordnung für ASPX-Dateien kopieren)
7. Deaktivieren Sie das Kontrollkästchen **Überprüfen, ob eine Datei vorhanden ist.**
8. Klicken Sie auf die **Schaltfläche OK**

[![Dialogfeld „New Project“ (Neues Projekt)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**Abbildung 4:** Erstellen einer Platzhalterskriptzuordnung mit IIS 6.0([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png)

Nachdem Sie Platzhalterskriptzuordnungen aktiviert haben, müssen Sie die Routingtabelle in der Datei Global.asax so ändern, dass sie eine Stammroute enthält. Andernfalls wird die Fehlerseite in Abbildung 5 angezeigt, wenn Sie eine Anforderung für die Stammseite Ihrer Anwendung stellen. Sie können die geänderte Datei Global.asax in Listing 4 verwenden.

[![Dialogfeld „New Project“ (Neues Projekt)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**Abbildung 5**: Fehler beim Fehlenden Stammweg([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png)

**Listing 4 - Global.asax (modifiziert mit Root-Route)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

Nachdem Sie eine Platzhalterskriptzuordnung für IIS 7.0 oder IIS 6.0 aktiviert haben, können Sie Anforderungen stellen, die mit der Standardroutentabelle funktionieren, die wie folgt aussehen:

/

/Home/Index

/Produkt/Details/3

/Produkt

## <a name="summary"></a>Zusammenfassung

Das Ziel dieses Tutorials war es, zu erklären, wie Sie ASP.NET MVC verwenden können, wenn Sie eine ältere Version von IIS (oder IIS 7.0 im klassischen Modus) verwenden. Wir haben zwei Methoden zum Arbeiten ASP.NET Routings mit älteren IIS-Versionen erläutert: Ändern Sie die Standardroutentabelle oder erstellen Sie eine Platzhalterskriptzuordnung.

Für die erste Option müssen Sie die URLs ändern, die in Ihrer ASP.NET MVC-Anwendung verwendet werden. Ein sehr wichtiger Vorteil dieser ersten Option ist, dass Sie keinen Zugriff auf einen Webserver benötigen, um die Routingtabelle zu ändern. Das bedeutet, dass Sie diese erste Option auch dann verwenden können, wenn Sie Ihre ASP.NET MVC-Anwendung bei einem Internethosting-Unternehmen hosten.

Die zweite Option besteht darin, eine Platzhalterskriptzuordnung zu erstellen. Der Vorteil dieser zweiten Option besteht darin, dass Sie Ihre URLs nicht ändern müssen. Der Nachteil dieser zweiten Option besteht darin, dass sie sich auf die Leistung Ihrer ASP.NET MVC-Anwendung auswirken kann.

> [!div class="step-by-step"]
> [Nächste](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
