---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: Einführung in ASP.net Web Pages Veröffentlichen einer Website mithilfe von webmatrix | Microsoft-Dokumentation
author: Rick-Anderson
description: Dieses Tutorial ist der letzte Teil des Lernprogramm Satzes, der ASP.net Web Pages und Microsoft webmatrix einführt. Es wird erläutert, wie Sie Ihre Website veröffentlichen...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240592"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>Einführung in ASP.net Web Pages Veröffentlichen einer Website mithilfe von webmatrix

 von [Tom FitzMacken](https://github.com/tfitzmac)

> Dieses Tutorial ist der letzte Teil des Lernprogramm Satzes, der ASP.net Web Pages und Microsoft webmatrix einführt. Es wird erläutert, wie Sie Ihre Website im Internet veröffentlichen, damit andere Benutzer damit arbeiten können. Es wird vorausgesetzt, dass Sie die Reihe durchgeführt haben, indem Sie [eine konsistente Suche nach ASP.net Web Pages Websites erstellen](https://go.microsoft.com/fwlink/?LinkId=251585).
> 
> Sie erfahren, wie Sie Ihre Website mit veröffentlichen:
> 
> - Microsoft Azure
> - Webhostingunternehmen

## <a name="about-publishing-your-site"></a>Informationen zum Veröffentlichen Ihrer Website

Bis jetzt haben Sie Ihre gesamte Arbeit auf einem lokalen Computer abgeschlossen, einschließlich des Testens Ihrer Seiten. Um die<em>cshtml</em> -Seiten auszuführen, haben Sie den Webserver verwendet, der in webmatrix integriert ist, nämlich IIS Express. Natürlich kann die Website, die Sie erstellt haben, mit Ausnahme der von Ihnen erstellten Website nicht angezeigt werden. Damit andere mit Ihrer Website zusammenarbeiten können, müssen Sie Sie im Internet veröffentlichen.

Wenn Sie nicht bereits über Zugriff auf einen öffentlichen Webserver verfügen, bedeutet das veröffentlichen, dass Sie über ein Konto mit einer *cloudplattform* oder einem *Hostinganbieter*verfügen müssen. Eine cloudplattform, wie z. b. Microsoft Azure, stellt eine Bedarfs gesteuerte Infrastruktur für Ihre Anwendungen bereit. Ein Hostinganbieter ist ein Unternehmen, das über öffentlich zugängliche Webserver verfügt und Ihnen Speicherplatz für Ihre Website zur Verfügung stellt. Hostingpläne werden von wenigen USD pro Monat (oder sogar kostenlos) für kleine Websites auf zahlreiche hundert Dollar pro Monat für kommerzielle Websites mit hohem Volumen ausgeführt.

> [!NOTE]
> Möglicherweise haben Sie Zugriff auf einen öffentlichen Webserver über den Internetdienstanbieter (Internet Service Provider, ISP), den Sie verwenden, um den Internetdienst zu Hause zu laden. Der Hostinganbieter muss jedoch ASP.net Web Pages unterstützen. Viele ISPs sind nicht, aber es lohnt sich immer, Sie zu überprüfen.

In diesem Tutorial erhalten Sie eine Übersicht über die Veröffentlichung. Es ist nicht praktikabel, genaue Details für alles bereitzustellen, da der Prozess für jeden Hostinganbieter etwas abweicht. Sie erhalten jedoch eine gute Vorstellung davon, wie der Prozess funktioniert.

Dieses Tutorial enthält vier Abschnitte:

1. [Einrichten der Standardseite](#defaultpage)
2. Veröffentlichen (Wählen Sie eine der folgenden Optionen aus)  
 a. [Veröffentlichen Ihrer Website auf Microsoft Azure](#azure)  
 b. [Veröffentlichen der Website in einem Webhostingunternehmen](#host)
3. [Die Live Site wird aktualisiert: Wiederveröffentlichung](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Einrichten der Standardseite

Wenn ein Benutzer zur Basisadresse für Ihre Website navigiert, wird dem Benutzer die Standardseite für Ihre Website angezeigt. Wenn *Default.htm* z. b. als Standardseite für die Website auf festgelegt ist `www.contoso.com` , ist die Navigation zu mit `www.contoso.com` der Navigation zu identisch `www.contoso.com/Default.htm` .

Aktuell verwendet Ihre Website **default. cshtml** als Standardseite. Diese Seite ist für Ihre Standardseite einwandfrei, aber in diesem Tutorial haben Sie dieser Seite keinen Inhalt hinzugefügt, sodass eine leere Seite angezeigt wird. Öffnen Sie "default. cshtml", und ersetzen Sie den Inhalt durch den folgenden Code.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Ihre Website ist nun bereit für die Veröffentlichung. Zunächst erfahren Sie, wie Sie den Standort in Azure bereitstellen und dann in einem Webhostingunternehmen bereitstellen. Beide Optionen können für Ihre Website verwendet werden, und Sie müssen nur einer der Bereitstellungs Optionen folgen.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Veröffentlichen Ihrer Website auf Microsoft Azure

In diesem Tutorial wird zunächst erläutert, wie Sie Ihre Website auf Microsoft Azure bereitstellen. Wenn Sie sich mit einem Microsoft-Konto anmelden, können Sie bis zu 10 kostenlose Websites in Azure erstellen. Diese kostenlosen Websites stellen eine bequeme Möglichkeit zum Testen Ihrer Websites dar. Sie können diese Beispiel Website später jederzeit löschen, um zu vermeiden, dass alle Ihre kostenlosen Websites genutzt werden. Sie können ein kostenloses Testkonto in wenigen Minuten erstellen. Ausführliche Informationen finden Sie unter [Einen Monat kostenlos testen](https://azure.microsoft.com/free/dotnet/).

Klicken Sie im Menüband webmatrix auf die Schaltfläche **veröffentlichen** .

![Schaltfläche "veröffentlichen" im webmatrix-Menüband](publishing/_static/image1.png)

Das Dialogfeld **Website veröffentlichen** wird angezeigt. Wenn Sie sich nicht bei Ihrem Microsoft-Konto angemeldet haben, enthält das Dialogfeld den Link " **Get Started with Azure** ". Klicken Sie auf diesen Link.

![Website veröffentlichen](publishing/_static/image2.png)

Wenn Sie sich nicht bei einem Microsoft-Konto angemeldet haben, haben Sie die Gelegenheit, sich anzumelden. Sie müssen sich bei einem Microsoft-Konto anmelden, um Ihre Website in Azure zu veröffentlichen.

![Anmelden](publishing/_static/image3.png)

Nachdem Sie sich bei Ihrem Microsoft-Konto angemeldet haben, enthält das Dialogfeld Links zum Erstellen einer neuen Website in Azure oder zum Herstellen einer Verbindung mit einer Ihrer vorhandenen Websites in Azure.

![Neue Website erstellen](publishing/_static/image4.png)

Wählen Sie **neue Website erstellen**aus.

Wenn Sie Ihr Projekt mit dem Namen " **webpgesmovies**" benannt haben, lautet der Standardname für Ihre Website " **webpagesmovies.azurewebsites.net**". Dieser Standardname ist höchstwahrscheinlich nicht verfügbar, wie durch das rote Ausrufezeichen angegeben.

![Name der Standard Website](publishing/_static/image5.png)

Ändern Sie den Standortnamen in einen verfügbaren Standort, und wählen Sie einen Standort aus, der sich in der Nähe Ihres Standorts befindet.

![Name der geänderten Website](publishing/_static/image6.png)

Klicken Sie auf **OK**.

Webmatrix verwendet einen Test, um zu bestimmen, ob der Server mit Ihrer Site kompatibel ist.

![Kompatibilitätstest](publishing/_static/image7.png)

Wählen Sie **Weiter**.

Die Ergebnisse des Kompatibilitätstests werden angezeigt.

![Kompatibilitäts Ergebnis](publishing/_static/image8.png)

Wählen Sie **Weiter**.

Webmatrix zeigt die Dateien und Datenbanken an, die auf der Website veröffentlicht werden. Da dies das erste Mal ist, dass Sie die Website veröffentlichen, werden alle Dateien aufgelistet. Sie können eine Datei deaktivieren, die nicht zur Veröffentlichung bereit ist. In den nachfolgenden Veröffentlichungen werden nur die geänderten Dateien angezeigt. Weitere Informationen finden Sie [unter Aktualisieren der Live Website: wieder veröffentlichen](#update).

![Vorschau veröffentlichen](publishing/_static/image9.png)

Wählen Sie **Weiter**.

Nachdem der Standort in Azure bereitgestellt wurde, wird eine Meldung mit dem Hinweis angezeigt, dass die Bereitstellung abgeschlossen wurde.

![Veröffentlichung abgeschlossen](publishing/_static/image10.png)

Ihre Website und Ihre Datenbank wurden in Azure veröffentlicht und sind nun öffentlich verfügbar. Klicken Sie auf den Link in der Meldung mit dem Hinweis, dass die Veröffentlichung abgeschlossen ist, und ihre bereitgestellte Website wird angezeigt. Sie oder alle Benutzer mit Internet Zugriff können Datensätze in der Datenbank hinzufügen oder ändern.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Veröffentlichen der Website in einem Webhostingunternehmen

Wenn Sie sich dafür entscheiden, nicht in Azure zu veröffentlichen, können Sie Ihre Website stattdessen in einem Webhostingunternehmen veröffentlichen.

Klicken Sie auf den Link **Webhosting suchen** .

![Schaltfläche "Webhosting suchen" im Dialogfeld "Veröffentlichungs Einstellungen"](publishing/_static/image12.png)

Sie gelangen zu einer Seite auf der Microsoft-Website, auf der Hosting-Anbieter aufgeführt sind, die ASP.NET unterstützen.

![Seite auf der Microsoft-Website, die Hostinganbieter](publishing/_static/image13.png)

Natürlich kann es schwierig sein, jetzt genau zu wissen, welche Hostingfeatures Sie möglicherweise langfristig benötigen. Hier sind einige Punkte zu beachten:

- Für Zwecke der Webwebsite Movies-Website müssen Sie nicht über ein separates Add-on für SQL Server verfügen, das häufig zusätzliche Kosten verursacht. In Ihrer Website verwenden Sie SQL Server Compact Edition, die eigenständig ist. Möglicherweise benötigen Sie jedoch SQL Server Zugriff für einige zukünftige Website Aufgaben, die Sie ausführen. Wenn Sie denken, dass Sie das möglicherweise später SQL Server Funktion hinzufügen können.
- Überprüfen Sie, ob der Hostinganbieter das Web deploy Veröffentlichungs Protokoll unterstützt. Sie können mit dem FTP-Protokoll veröffentlichen, aber es ist bequemer, Web deploy zu verwenden.

Einige Websites bieten einen kostenlosen Testzeitraum. Eine kostenlose Testversion ist eine gute Möglichkeit, um die Veröffentlichung und das Hosting zu testen, während Sie noch mit webmatrix experimentieren und ASP.net Web Pages.

Wählen Sie ein ähnliches aus. Für dieses Tutorial haben wir DiscountASP.net ausgewählt, denn während wir das Tutorial erstellt haben, verfügte dieses Unternehmen über eine herauf Stufung, mit der Mitarbeiter eine Website für einige Monate kostenlos hosten können.

> [!NOTE]
> Unsere Wahl eines hostinganbieters für dieses Tutorial sollte nicht als Unterstützung für dieses Unternehmen interpretiert werden. Wir mussten aber einen zur Veranschaulichung auswählen, und DiscountASP.net ist eines der vielen Unternehmen, das ASP.net Web Pages und das Web deploy Protokoll für die Veröffentlichung unterstützt.

Wenn Sie sich beim Hostinganbieter registriert haben, sendet das Unternehmen in der Regel eine e-Mail, die einen Benutzernamen und ein Kennwort, die URL des Webservers usw. enthält. Wenn das Hostingunternehmen Web deploy-Protokoll unterstützt, sendet es Ihnen möglicherweise eine Datei mit Veröffentlichungs Einstellungen, oder Sie können eine Datei herunterladen. Eine Datei mit Veröffentlichungs Einstellungen vereinfacht den Prozess für Sie.

Wenn Sie sich angemeldet haben und bereit für die Veröffentlichung sind, klicken Sie im webmatrix-Menüband auf die Schaltfläche **veröffentlichen** . Das Dialogfeld **Veröffentlichungs Einstellungen** wird angezeigt.

Wenn Sie vom Hostinganbieter eine Datei mit Veröffentlichungs Einstellungen gesendet haben, klicken Sie auf den Link **Veröffentlichungs Einstellungen importieren** , und importieren Sie die Datei. Wenn Sie nicht über eine Datei mit Veröffentlichungs Einstellungen verfügen, füllen Sie die Felder mit den Werten aus, die das Hosting-Unternehmen Ihnen per e-Mail gesendet hat. Das Dialogfeld **Veröffentlichungs Einstellungen** könnte wie folgt aussehen:

![Im Dialogfeld "Veröffentlichungs Einstellungen" ausgefüllte Veröffentlichungs Einstellungen](publishing/_static/image14.png)

Klicken Sie auf **Verbindung**überprüfen. Wenn alles in Ordnung ist, wird das Dialogfeld **erfolgreich verbunden**, was bedeutet, dass es mit dem Server des hostinganbieters kommunizieren kann.

![Erfolgsmeldung, wenn die Veröffentlichungs Einstellungen richtig sind](publishing/_static/image15.png)

Wenn ein Problem vorliegt, informiert webmatrix am besten, was das Problem ist:

![Fehlermeldung, wenn ein Problem mit den Veröffentlichungs Einstellungen vorliegt](publishing/_static/image16.png)

Klicken Sie auf **Save**, um Ihre Einstellungen zu speichern. Webmatrix bietet einen Test, um sicherzustellen, dass die Kommunikation mit der Hostingsite ordnungsgemäß durchgeführt werden kann:

![Nachrichtenangebot, um den Veröffentlichungsprozess zu testen](publishing/_static/image17.png)

Klicken Sie auf **Ja**. Webmatrix lädt einige Beispieldateien in den Hostinganbieter hoch. Wenn der Kompatibilitätstest abgeschlossen ist, meldet webmatrix die Ergebnisse:

![Ergebnisse des Veröffentlichungs Tests](publishing/_static/image18.png)

Wenn Sie bereit sind, klicken Sie auf " **weiter** ", um den Veröffentlichungsprozess für "Real" zu starten. Webmatrix ermittelt, welche Dateien sich auf Ihrer Website befinden und sich bereits auf dem Host Server befinden (derzeit keine) und gibt Ihnen eine Vorschau des Veröffentlichungsprozesses:

![Vorschau der Dateien, die vom Veröffentlichungsprozess hochgeladen werden](publishing/_static/image19.png)

Die Liste der zu veröffentlichenden Dateien umfasst die Webseiten, die Sie erstellt haben, z. b. " *Movies. cshtml*". Die Liste enthält auch Dateien für Hilfsprogramme, die Sie installiert haben, die Dateien, die SQL Server Compact Edition für Ihre Datenbank ausgeführt werden sollen usw. Folglich kann der anfängliche Veröffentlichungsprozess beträchtlich sein.

Klicken Sie auf **Continue**(Weiter). Webmatrix kopiert die Dateien auf den Server des hostinganbieters. Wenn dies der Fall ist, werden die Ergebnisse in der Statusleiste angezeigt:

![Status leisten Meldung, wenn der Veröffentlichungs Vorgang erfolgreich abgeschlossen wurde](publishing/_static/image20.png)

Um Ihre Live-Website anzuzeigen, klicken Sie auf den Link in der Statusleiste. Fügen Sie der URL *Filme* hinzu, und Sie sehen die Datei *Movies. cshtml* , die Sie erstellt haben:

![Die Live Site, die die Seite "Filme" anzeigt](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Die Live Site wird aktualisiert: Wiederveröffentlichung

Nachdem Sie Ihre Website veröffentlicht haben (entweder in Azure oder in einem Webhostingunternehmen), gibt es zwei Kopien davon &mdash; auf Ihrem Computer und die Version des Dienstanbieters. Wahrscheinlich möchten Sie die Entwicklung der Website fortsetzen (sofern nichts anderes als Teil des nächsten Lernprogramm Satzes). Wenn Sie dies tun, müssen Sie die Website erneut veröffentlichen, um die Änderungen von Ihrem Computer auf den Dienstanbieter zu kopieren. Der Veröffentlichungsprozess in webmatrix kann ermitteln, welche Dateien auf Ihrer Website geändert wurden, und nur diese Dateien veröffentlichen.

Um zu sehen, wie die Wiederveröffentlichung funktioniert, öffnen Sie die Website *Movies. cshtml* , nehmen Sie einige kleine Änderungen vor, und speichern Sie die Datei. Ändern Sie beispielsweise den Titel in `Movies - Updated` .

Klicken Sie im Menüband auf die Schaltfläche **veröffentlichen** . Webmatrix bestimmt, was geändert wurde, und zeigt eine Vorschau der Dateien an, die veröffentlicht werden.

![Das Dialogfeld "veröffentlichen" zeigt geänderte Dateien an, die für die Wiederveröffentlichung bereit sind.](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> Standardmäßig wird Ihre Datenbank (*sdf* -Datei) von webmatrix nur beim ersten Veröffentlichen der Website veröffentlicht. Nachdem Ihre Website veröffentlicht wurde und die Benutzer mit der Website interagieren, verfügt die Datenbank auf der Live Website in der Regel über die tatsächlichen Daten der Website. Sie müssen sehr vorsichtig sein, die Live Datenbank nicht mit der *. sdf* -Datei zu überschreiben, die sich auf Ihrem Computer befindet, die in der Regel nur Testdaten enthält. Aus diesem Grund werden Sie sehen, dass die **Veröffentlichungs Veröffentlichung alle Remote Datenbanken überschreibt**und warum das Kontrollkästchen für *Webweb. sdf* standardmäßig deaktiviert ist.

Klicken Sie auf **Continue**(Weiter). Webmatrix veröffentlicht die geänderten Dateien und zeigt eine Erfolgsmeldung an, wie dies bei der ersten Veröffentlichung der Fall war.

Wechseln Sie zur Live-Website (Sie können auf den Link in der Erfolgsmeldung klicken, wenn Sie noch angezeigt wird), und überprüfen Sie, ob Ihre Änderung veröffentlicht wurde.

> [!TIP] 
> 
> **Remote Bearbeitung von Dateien**
> 
> Als Alternative zum Ändern der Website und anschließenden erneuten veröffentlichen können Sie Remote Dateien direkt in webmatrix bearbeiten. In diesem Szenario öffnen Sie eine Datei, die sich auf dem Dienstanbieter befindet, und webmatrix lädt eine Kopie davon herunter, damit Sie Sie bearbeiten können. Jedes Mal, wenn Sie die Datei speichern, sendet webmatrix die Änderungen an die Website.
> 
> Die Remote Bearbeitung ist eine einfache Möglichkeit, Änderungen an ihrer Live Website vorzunehmen. Die Änderungen, die Sie auf diese Weise vornehmen, werden jedoch nicht mit den Dateien Ihres lokalen Standorts synchronisiert. Zum Synchronisieren der lokalen Dateien mit dem Remote Standort können Sie die Remote Dateien herunterladen. Dieser Prozess funktioniert sehr ähnlich wie die Veröffentlichung, außer in umgekehrter Reihenfolge.
> 
> Weitere Informationen zu den Funktionen zur Remote Bearbeitung und zum Remote Download von webmatrix finden Sie hier. Sie sind sehr nützlich, wenn mehrere Personen an derselben Website auf unterschiedlichen Computern arbeiten müssen. Weitere Informationen finden Sie unter [veröffentlichen und Bearbeiten einer Remote Website mit webmatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Weitere Ressourcen

- [ASP.net webmatrix ASP.net Web Pages Forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), ein guter Ort, um Fragen zu stellen und Antworten zu erhalten.

> [!div class="step-by-step"]
> [Vorherige](layouts.md)
