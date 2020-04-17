---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Verbesserungen in Visual Studio 2005 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2005 bietet Webanwendungsentwicklern eine lange Liste von Verbesserungen und Verbesserungen an Webprojekten.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542988"
---
# <a name="improvements-in-visual-studio-2005"></a>Verbesserungen in Visual Studio 2005

von [Microsoft](https://github.com/microsoft)

> Visual Studio 2005 bietet Webanwendungsentwicklern eine lange Liste von Verbesserungen und Verbesserungen an Webprojekten.

Visual Studio 2005 bietet Webanwendungsentwicklern eine lange Liste von Verbesserungen und Verbesserungen an Webprojekten. So leistungsfähig Visual Studio .NET 2002 und 2003 auch sind, es gab viele Beschwerden in der Art und Weise, wie Webprojekte behandelt wurden. Visual Studio 2005 fügt eine erhebliche Anzahl neuer Funktionen hinzu, um diese Beschwerden zu beheben. Informationen zu denjenigen, die die Art und Weise bevorzugen, wie Visual Studio .NET 2003 die Kompilierung von Webanwendungen verarbeitet hat, finden Sie unter [Webanwendungsprojekte](https://go.microsoft.com/fwlink/?LinkId=57870).

In dieser Unterrichtseinheit werden Verbesserungen bei der Erstellung, Verwaltung und Entwicklung von Webprojekten behandelt. In einem späteren Modul können Sie Verbesserungen beim Erstellen von Webprojekten und deren Bereitstellung gut abdecken.

## <a name="frontpage-server-extensions"></a>FrontPage Server-Erweiterungen

Visual Studio .NET 2002 und 2003 erforderten FrontPage Server-Erweiterungen auf dem Feld, um Webprojekte zu erstellen oder zu erstellen. Entwickler hatten die Wahl zwischen zwei verschiedenen Zugriffsmodi (FrontPage Server Extensions oder File Access Mode), beide verwendeten FrontPage Server Extensions, um Aufgaben wie das Festlegen des Anwendungsstamms in IIS usw. auszuführen.

Visual Studio 2005 entfernt die Abhängigkeit von FrontPage Server-Erweiterungen für lokale Projekte. Visual Studio 2005 greift jetzt direkt auf die IIS-Metabasis zu, anstatt die FrontPage Server-Erweiterungen zu verwenden. Visual Studio 2005 bietet außerdem Unterstützung für FTP, die remoteen Projektzugriff ermöglicht, ohne Dasszusungen von FrontPage Server erforderlich sind.

Für Entwickler, die FrontPage Server-Erweiterungen in ihren Projekten verwenden möchten, ist die Option weiterhin verfügbar. Aufgrund des starken Feedbacks der ASP.NET Entwickler-Community ist dies jedoch keine Anforderung.

> [!NOTE]
> FrontPage Server-Erweiterungen sind weiterhin für die Erstellung, das Öffnen, Öffnen usw. von Remote-Projekten erforderlich.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005 wird mit einem neuen Webserver namens ASP.NET Development Server ausgeliefert. (Dieser Webserver war früher als Cassini bekannt.)

Der ASP.NET Development Server bietet mehrere Vorteile.

- Nicht-Administratoren können nun einen Webserver entwickeln und debuggen.
- Der ASP.NET Development Server ordnet virtuelle Verzeichnisse dynamisch jedem Speicherort im Dateisystem zu, sodass flexible Projektstandorte möglich sind.
- Benutzer unter Windows XP Professional, die Bereits IIS verwenden, können jetzt neue Webanwendungen erstellen, die sich nicht auf die Datei- oder Ordnerstruktur ihrer Standardwebsite in IIS auswirken.

Es ist keine spezielle Konfiguration erforderlich, um die Vorteile des ASP.NET Development Server zu nutzen. Wenn ein Webprojekt, das auf dem Dateisystem gehostet wird, gedebuggen oder durchsucht wird, startet Visual Studio 2005 automatisch eine Instanz des ASP.NET Development Server auf einem zufälligen Port, um die Anforderung zu bedienen.

Weitere Informationen finden Sie weiter unten in dieser Unterrichtseinheit auf dem ASP.NET Development Server.

## <a name="improved-file-management"></a>Verbesserte Dateiverwaltung

In Visual Studio 2002 und 2003 wurden in einer Projektdatei (.vbproj für VB.NET und .csproj für C) Informationen zu allen Dateien in der Webanwendung gespeichert. Die Projektmappen-Explorer-Anzeige basiert auf den Dateiinformationen in der Projektdatei. Aus diesem Grund zeigt der Projektmappen-Explorer häufig ungenaue Informationen in Fällen an, in denen externe Editoren verwendet wurden. Visual Studio 2002 und 2003 würden Dateiänderungen häufig überschreiben oder die neueste Version von Dateien nicht anzeigen.

Visual Studio 2005 entfernt die Projektdatei. Stattdessen liest es die Datei- und Ordnerinformationen direkt vom Datenträger, was zu einer genauen Anzeige der Dateien in Ihrem Projekt führt. Da der Ordner "Referenzen" in Visual Studio 2002 und 2003 keinen tatsächlichen Ordner in Ihrer Webanwendung darstellt, entfernt Visual Studio 2005 auch den Ordner Referenzen aus dem Projektmappen-Explorer. Um auf die Verweise für Ihr Projekt in Visual Studio 2005 zuzugreifen, sollten Sie die Eigenschaftenseiten für das Projekt verwenden.

## <a name="creating-web-projects"></a>Erstellen von Webprojekten

Webentwicklern stehen viele neue Optionen für die Projekterstellung in Visual Studio 2005 zur Verfügung. Websites können nun an einer beliebigen Stelle im Dateisystem erstellt und dann mit dem neuen ASP.NET Development Server gedebuggég oder durchsucht werden. Entwickler können auch neue Websites mit FTP erstellen.

Klicken Sie hier, um eine exemplarische Vorgehensweise zum Erstellen von Webprojekten in Visual Studio 2005 anzuzeigen.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Öffnen sie Ein-Bild-Video](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Dateisystemprojekte

Wie Sie in der exemplarischen Vorgehensweise für Videos gesehen haben, können Sie Websites auf dem Dateisystem entweder auf dem lokalen Computer oder an einem Remotespeicherort über eine Dateifreigabe erstellen. Websites, die im Dateisystem erstellt werden, werden mit dem ASP.NET-Entwicklungsserver durchsucht und gedebuggég.

> [!NOTE]
> Der ASP.NET Development Server kann für Kunden verwirrung stiften. Wenn ein Webprojekt auf dem Dateisystem in der IISs-Verzeichnisstruktur erstellt wird (d. h. c:/inetpub/wwwroot), wird die Website weiterhin über den ASP.NET Development Server durchsucht, wenn sie in Visual Studio 2005 gestartet wird. Daher ist jede IIS-Konfiguration (d. h. Authentifizierungsmethoden) nicht anwendbar.

Das Standardwebprojekt entfernt auch einen Großteil des Overheads, indem es nur eine Default.aspx-Seite, default.cs Datei und einen Ordner "App/_Data enthält. Die web.config und spezielle Ordner (d.h. app/_code) werden nach Bedarf hinzugefügt. Ihr Webprojekt enthält nur die Dateien und Ordner, die Sie benötigen.

### <a name="http-projects"></a>HTTP-Projekte

HTTP-Projekte können projekte sein, die auf einer lokalen IIS-Website oder auf einer Remotewebsite erstellt werden. Der Standardspeicherort `http://localhost`des Projekts ist . Wenn Sie auf die Schaltfläche Durchsuchen klicken, gibt es zwei HTTP-Optionen: Lokale IIS und Remotesite. Der Hauptunterschied in diesen beiden Optionen ist die Methode, bei der die Websiteinformationen im Dialogfeld Standort auswählen angezeigt werden und wie die Dateien auf den Webserver kopiert werden.

Die Option Lokale IIS liest die Websiteinformationen aus der Metabasis auf dem lokalen Computer, und Dateien werden mit dem Dateisystem kopiert. Die Option Remotesite verwendet die FrontPage Server-Erweiterungen, und die Standortinformationen und -dateien werden mithilfe von HTTP- und FrontPage Server Extensions-RPC-Aufrufen kopiert.

> [!NOTE]
> Die Datei vs/_tmp.htm und get/_aspx/_ver.aspx werden nicht mehr zum Bestimmen von Versionsinformationen verwendet.

Die Standard-HTTP-Option ist Local IIS. Diese Option liest die IIS-Metabasis, um zu bestimmen, welche Websites verfügbar sind und an welchem Speicherort Inhalte erstellt werden sollen. Sie können einen anderen Ordner oder ein anderes virtuelles Verzeichnis auswählen, indem Sie ihn in der Strukturansicht auswählen. Sie können auch ein neues virtuelles Verzeichnis erstellen, Ordner als Anwendungen markieren und vorhandene virtuelle Verzeichnisse aus diesem Dialogfeld löschen.

![Der Dialog "Standort auswählen"](improvements-in-visual-studio-2005/_static/image1.gif)

**Abbildung 1:** Dialog position auswählen

Wenn Sie im Gegensatz zu früheren Versionen von Visual Studio das Kontrollkästchen **Secure Sockets Layer verwenden** aktivieren und das SSL-Zertifikat nicht mit der URL übereinstimmt, die Sie durchsuchen, wird ein Dialogfeld Sicherheitswarnung angezeigt, in dem Sie gefragt werden, ob Sie fortfahren möchten. Wenn das Zertifikat nicht übereinstimmen, schlägt das Erstellen des Projekts fehl, wenn das Zertifikat mit Visual Studio .NET 2003 übereinstimmt.

![Sicherheitswarnung in Bezug auf SSL-Zertifikat](improvements-in-visual-studio-2005/_static/image2.gif)

**Abbildung 2:** Sicherheitswarnung bezüglich SSL-Zertifikat

### <a name="note-on-host-headers"></a>Hinweis zu Host-Headern

Wenn Sie eine Webanwendung auf einer Website erstellen, die an eine bestimmte IP gebunden ist, müssen Sie sicherstellen, dass ein Hostheader konfiguriert ist. Andernfalls erstellt Visual Studio die `http://localhost`Site unter , aber die IP-Adresse wird nicht ordnungsgemäß aufgelöst, wenn die Site in der IDE durchsucht oder gedebuggég wird.

Wenn Sie die Option Remotesite auswählen, ändert sich das Dialogfeld, damit Sie die Ziel-URL für die neue Website eingeben können. Diese URL muss sich auf einem Server befinden, auf dem die FrontPage Server-Erweiterungen aktiviert sind. Wenn Sie mit dem lokalen Webserver mit den FrontPage Server-Erweiterungen arbeiten möchten, können Sie die Option Remotesite verwenden und eine lokale URL angeben.

![Erstellen einer Website auf einem Remoteserver](improvements-in-visual-studio-2005/_static/image1.jpg)

**Abbildung 3:** Erstellen einer Website auf einem Remoteserver

Wenn das SSL-Zertifikat nicht mit dem SSL-Zertifikat übereinstimmt, unterscheidet sich das Bestätigungsdialogfeld geringfügig von dem Dialogfeld, das bei Verwendung der Option Lokale IIS angezeigt wird, wenn eine Anwendung auf einer Remote-Site über SSL erstellt wird.

![Die Sicherheitswarnung für Remotestandorte](improvements-in-visual-studio-2005/_static/image3.gif)

**Abbildung 4:** Die Sicherheitswarnung für Remotestandorte

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 führt die Option zum Erstellen von Websites über FTP ein. Wenn Sie diese Option verwenden, erstellt die IDE die Dateien lokal im temporären Ordner des Benutzers und verwendet dann FTP, um die Dateien an den FTP-Speicherort zu verschieben.

> [!NOTE]
> Der Speicherort des temporären Ordners&lt;ist&gt;c:/Dokumente und Einstellungen/&lt;Benutzer&gt;/Lokale Einstellungen/Temp/VWDWebCache/ Server /_&lt;Anwendungsname&gt;

Wenn Sie die FTP-Option verwenden, wird Ihnen ein Dialogfeld Standort auswählen angezeigt. Sie geben die erforderlichen FTP-Verbindungsinformationen in dieses Dialogfeld ein, wie unten gezeigt.

![Der Standortdialog auswählen für FTP](improvements-in-visual-studio-2005/_static/image2.jpg)

**Abbildung 5:** Der Positionsdialog für FTP auswählen

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Übung: FTP-Site einrichten und ein Projekt erstellen

Mit den folgenden Schritten wird die FTP-Site so konfiguriert, dass ein Benutzer über einen Speicherort verfügt, auf den nur er über FTP hochladen kann.

### <a name="install-the-ftp-service"></a>Installieren des FTP-Dienstes

1. Öffnen Sie Programme entfernen hinzufügen, wählen Sie Windows-Komponenten hinzufügen/entfernen
2. Wählen Sie Internetinformationsdienste (Application Server unter Windows 2003) aus, und klicken Sie auf **Details**.
3. Überprüfen Sie **den FTP-Dienst (File Transfer Protocol)** und klicken Sie auf **OK**.
4. Klicken Sie auf **Weiter,** um den FTP-Dienst zu installieren.

### <a name="create-a-new-folder-for-content"></a>Erstellen eines neuen Ordners für Inhalte

1. Erstellen Sie im Windows Explorer einen neuen Ordner mit dem Namen **User1** in c:/inetpub/wwwroot.

#### <a name="configure-folders-and-permissions-on-folders"></a>Konfigurieren Sie Ordner und Berechtigungen für Ordner.

1. Öffnen Sie das Snap-In "Internetinformationsdienste" über Verwaltungstools. Sie haben nun einen FTP-Sites-Ordner unter dem Computernamenknoten.
2. Erweitern Sie **FTP-Sites**.
3. Klicken Sie mit der rechten Maustaste auf die **Standard-FTP-Site**, wählen Sie **Neu**, dann **Virtuelles Verzeichnis**aus , und klicken Sie dann auf **Weiter**.
4. Geben Sie **Benutzer1** für den Namen des virtuellen Verzeichnisses ein, und klicken Sie auf **Weiter**.
5. Geben Sie **c:/inetpub/wwwroot/User1** für den Pfad ein und klicken Sie auf **Weiter**.
6. Klicken Sie auf **Weiter,** und **beenden Sie** dann, um den Assistenten abzuschließen.
7. Klicken Sie mit der rechten Maustaste auf das virtuelle **Verzeichnis User1** unter Standard-FTP-Site, und wählen Sie **Eigenschaften**aus.
8. Aktivieren Sie das Kontrollkästchen **Schreiben,** und klicken Sie auf **OK,** um das Dialogfeld zu schließen.
9. Klicken Sie mit der rechten Maustaste auf **Standard-FTP-Site,** und wählen Sie **Eigenschaften**aus.
10. Deaktivieren Sie auf der Registerkarte **Sicherheitskonten** die Option **Anonyme Verbindungen zulassen**.
11. Klicken Sie im Dialogfeld auf **Ja,** um sie zu fragen, ob Sie fortfahren möchten.
12. Klicken Sie auf **OK**, um das Dialogfeld zu schließen.
13. Erweitern Sie die **Standardwebsite** unter dem Knoten **Websites.**
14. Klicken Sie mit der rechten Maustaste auf das **User1-Verzeichnis,** und wählen Sie **Eigenschaften** aus
15. Klicken Sie im Abschnitt **Anwendungseinstellungen** auf **Erstellen,** um den Ordner als Anwendung zu markieren.
16. Klicken Sie auf **OK**, um das Dialogfeld zu schließen.
17. Schließen Sie das Snap-In der Internetinformationsdienste.

### <a name="create-web-project"></a>Webprojekt erstellen

1. Öffnen Sie Visual Studio 2005.
2. Wählen Sie im Menü **Datei** die Option **Neue Website**aus.
3. Wählen Sie in der Dropdown-Liste **Standort** **FTP**aus.
4. Klicken Sie auf **Durchsuchen**.
5. Geben Sie **localhost** in das **Server-Textfeld** ein.
6. Geben Sie **Benutzer1** in das Textfeld Verzeichnis ein.
7. Klicken Sie auf **Öffnen**. Der FTP-Speicherort wird in das Dialogfeld Neue Website eingegeben.
8. Klicken Sie auf **OK**.
9. Deaktivieren Sie **die Option Anonyme Anmeldung** im Dialogfeld FTP-Anmeldung, geben Sie Ihre Anmeldeinformationen ein, und klicken Sie auf **OK**.
10. Was ist die URL für das Projekt? (Die URL für das Projekt wird im Projektmappen-Explorer angezeigt.)
11. Wählen Sie im Menü **Erstellen** die Option **Website erstellen** oder **Lösung erstellen**aus.
12. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Default.aspx, und wählen Sie **Ansicht im Browser**aus.
13. Geben Sie `http://localhost/user1` im Dialogfeld Website-URL Erforderlich die URL ein, und klicken Sie auf **OK**.

> [!NOTE]
> Wenn sie eine Fehlermeldung erhalten, die auf eine Unfähigkeit zum Laden des Typs /_Default hinweist, stellen Sie sicher, dass Sie ASP.NET 2.0 auf Ihrer Website und nicht in einer früheren Version ausführen. Sie können dies über die Registerkarte ASP.NET in Internetinformationsdienste tun.

## <a name="opening-web-projects"></a>Öffnen von Webprojekten

Das Öffnen von Webprojekten ähnelt dem Erstellen von Projekten. In den folgenden Abschnitten werden Bereiche aufgesucht, auf die Sie bei der Arbeit in der IDE achten müssen. Es umfasst auch die Arbeit mit Webprojekten mit HTTP und FTP.

Um ein Webprojekt zu öffnen, wählen Sie im Menü Datei die Option Website öffnen aus. Sie werden mit demselben zuvor behandelten Dialogfeld Standort auswählen aufgefordert, und Sie haben dieselben vier Optionen zur Verfügung: Dateisystem, lokale IIS, FTP und Remotesite.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Dateisystem

Wie bereits in diesem Modul angegeben, verwendet Visual Studio keine Projektdatei mehr. Wenn Sie also eine Website aus dem Dateisystem öffnen möchten, haben Sie die Möglichkeit, einen beliebigen Ordner auszuwählen, auch wenn der gewählte Ordner zunächst nicht als Webprojekt in Visual Studio erstellt wurde. Sie können z. B. den Ordner Eigene Dateien als Website öffnen, und Visual Studio öffnet ihn gerne und zeigt Ihre Dateien wie unten gezeigt an.

![Meine Dokumente, die als Website geöffnet wurden](improvements-in-visual-studio-2005/_static/image3.jpg)

**Abbildung 6:** *Meine Dokumente,* die als Website geöffnet wurden

Da Visual Studio nur bei Bedarf zusätzliche Dateien und Ordner erstellt, werden dem geöffneten Speicherort keine zusätzlichen Dateien oder Ordner hinzugefügt. Ein Nebeneffekt dieser Architektur besteht darin, dass Sie dadurch daran gehindert werden, Websites im Dateisystem zu verschachteln. Betrachten Sie beispielsweise die folgende Verzeichnisstruktur.

Webprojekt bei C:/MyWebSite

Ein weiteres Webprojekt bei C:/MyWebSite/Nested

Wenn Sie die Website unter c:/MyWebSite öffnen, wird der Ordner Verschachtelt als Unterordner dieser Anwendung angezeigt.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

Beim Öffnen von Websites über HTTP werden die Einstellungen entweder aus der IIS-Metabasis (Local IIS) oder mithilfe von FrontPage Server Extensions (Remote Site) gelesen. Wenn verschachtelte Webanwendungen vorhanden sind, werden diese auch mit einem Symbol angezeigt, das sie als Anwendung identifiziert. Wenn Sie mit der Arbeit mit Webanwendungen in FrontPage vertraut sind, ist das Verhalten in Visual Studio 2005 ähnlich.

Obwohl Visual Studio ein Symbol für Anwendungen anzeigt, die unter der Anwendung verschachtelt sind, die derzeit in der IDE geöffnet ist, können Sie sie nicht erweitern, um deren Inhalt anzuzeigen. Sie können jedoch auf sie doppelklicken, um sie zu öffnen. Wenn Sie dies tun, wird Ihnen ein Dialogfeld angezeigt, in dem Sie aufgefordert werden, entweder die Webanwendung zu öffnen (und die aktuell geöffnete Lösung zu ersetzen) oder die Webanwendung der aktuellen Lösung hinzuzufügen.

![Doppelklicken auf ein verschachteltes Anwendungssymbol zeigt Ihnen dieses Dialogfeld](improvements-in-visual-studio-2005/_static/image4.jpg)

**Abbildung 7:** Doppelklicken auf ein verschachteltes Anwendungssymbol zeigt Ihnen dieses Dialogfeld

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP-Site

Wenn Sie eine Site über FTP öffnen, werden die Dateien lokal in Ihren temporären Ordner kopiert. Der vollständige Pfad für den lokalen Speicherort wird im Eigenschaftenbereich für das Projekt angezeigt und mit dem folgenden Format erstellt.

C:/Dokumente und&lt;Einstellungen/ Benutzer&gt;/Lokale Einstellungen/Temp/VWDWebCache/&lt;Server&gt;/_&lt;Anwendungsname&gt;

Bei der Verwendung von FTP muss Visual Studio die Basis-URL für Ihr Projekt angeben, damit Sie sie wie unten gezeigt durchsuchen können. Wenn Sie keine Basis-URL angeben, werden Sie von Visual Studio beim ersten Versuch, eine Seite in der Website zu durchsuchen, dazu aufgefordert.

![Angeben einer Basis-URL für FTP-Sites](improvements-in-visual-studio-2005/_static/image5.jpg)

**Abbildung 8:** Angeben einer Basis-URL für FTP-Sites

## <a name="improvements-in-compilation"></a>Verbesserungen bei der Kompilierung

Die Arbeit mit Webanwendungen in Visual Studio 2005 ist deutlich schneller als frühere Versionen. Dies ist nicht zu einem kleinen Teil auf die Änderungen in der Kompilierungsarchitektur zurückzuführen.

In Visual Studio 2002 und 2003 wurden Webanwendungen in eine primäre Assembly kompiliert, die sich im Ordner /bin befindet. In Visual Studio 2005 wurde ein App/_Code Ordner hinzugefügt. Klassen und anderer Nicht-UI-Code werden dem Ordner App/_Code hinzugefügt. Wenn Visual Studio das Projekt erstellt, werden alle Dateien im Ordner App/_Code in eine einzelne App/_Code.dll-Datei kompiliert. Das Ergebnis dieser Änderung ist, dass nachfolgende Builds viel schneller sind als in früheren Versionen.

> [!NOTE]
> Das BEFEHLszeilendienstprogramm MSBuild kann auch zum Erstellen ASP.NET Webanwendungen verwendet werden. Dieses Tool wird in Modul 9 behandelt.

Eine weitere Kompilierungserweiterung ist die neue Option "Seiten aufbauen" im Menü "Build". Diese Funktion ermöglicht es einem Entwickler, nur die aktuelle Seite neu zu erstellen (zusammen mit natürlich und Abhängigkeiten), sodass Änderungen schneller kompiliert werden können. Da die Datei keine Hintergrundkompilierung zum Zwecke der Aktualisierung von IntelliSense usw. anbietet, werden sie von dieser Funktion enorm profitieren, da intelliSense schnell aktualisiert werden kann, indem einfach eine einzelne Seite neu erstellt wird.

Mit den Buildeigenschaften für ein Projekt können Sie den Buildtyp konfigurieren, der vor der Ausführung der Startseite auftritt. Entwickler können die aktuelle Seite nur erstellen, damit Visual Studio nach Codeänderungen schneller mit dem Debuggen von Anwendungen beginnen kann.

![Die Buildpage-Startaktion](improvements-in-visual-studio-2005/_static/image6.jpg)

**Abbildung 9:** Die Buildseitenstartaktion

Eine weitere großartige Erweiterung von Visual Studio und der ASP.NET-Architektur befindet sich im Bereich der Bearbeitung und Fortsetzung. In Visual Studio 2005 können Entwickler mit dem Debuggen eines Projekts beginnen und Codeänderungen am Projekt vornehmen, ohne den Debugger zu trennen. Tatsächlich können Sie buchstäblich mit dem Debuggen eines Projekts beginnen, eine neue Klasse hinzufügen, dieser Klasse Code hinzufügen, Ihrer Seite Code hinzufügen, der eine neue Instanz dieser Klasse erstellt, und eine Methode der Klasse ausführen, ohne den Debugger zu trennen. Die Ausführung des neuen Codes ist buchstäblich so einfach wie das Aktualisieren des Browsers!

Klicken Sie hier, um eine exemplarische Vorgehensweise für das Bearbeiten und Fortfahren in Visual Studio 2005 anzuzeigen.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Öffnen sie Ein-Bild-Video](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

Die robuste Bearbeitungs- und Weiterverwaltungsfunktionalität in ASP.NET 2.0 und Visual Studio 2005 ist auf eine Architekturänderung für ASP.NET Anwendungen zurückzuführen. In ASP.NET 1.x wurden in Visual Studio 2002/2003 erstellte Anwendungen in eine primäre Assembly kompiliert, die im Ordner /bin gespeichert wurde. Alle Klassen, Seiten usw. für die Anwendung wurden in diese eine DLL kompiliert. Zur Laufzeit kompilierte ASP.NET dann alle Steuerelemente, Daserstellungs- und ASP.NET Code innerhalb von Seiten und kopierte diese DLLs in den temporären Ordner ASP.NET.

In Visual Studio 2005 mit ASP.NET 2.0 wurden die beiden oben beschriebenen Kompilierungsmodelle (eines für Visual Studio und eines für ASP.NET zur Laufzeit) zu einem gemeinsamen Kompilierungsmodell zusammengeführt. Das bedeutet, dass alle Kompilierungsprobleme jetzt während der Entwicklungsphase und nicht zur Laufzeit erfasst werden. Es ermöglicht auch Designer- und IntelliSense-Unterstützung für Features wie Benutzersteuerelemente und Masterseiten.

Klicken Sie hier, um eine videobebilderische Vorgehensweise der Designerunterstützung für Benutzersteuerelemente anzuzeigen.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Öffnen sie Ein-Bild-Video](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Wenn ein Benutzersteuerelement von einer @Register Seite entfernt wird, verbleibt die Direktive im Markup und sollte manuell entfernt werden, um Parserfehler zu vermeiden, wenn das Benutzersteuerelement von der Website gelöscht wird.

Eine weitere Verbesserung im Visual Studio-Kompilierungsmodell ist die Funktion Website veröffentlichen. Da die Veröffentlichungsfunktion die Website vorkompiliert, können Entwickler die zusätzliche Leistung genießen, wenn sie bei Bedarf nichts kompilieren müssen. Außerdem wird der gesamte Quellcode im Ordner App/_Code in eine DLL vorkompiliert, sodass kein Quellcode bereitgestellt werden muss.

![Das Dialogfeld Website veröffentlichen](improvements-in-visual-studio-2005/_static/image7.jpg)

**Abbildung 10:** Dialogfeld "Veröffentlichung von Websites"

> [!NOTE]
> Das Dienstprogramm aspnet/_compile.exe kann auch zum Vorkompilieren einer ASP.NET Webanwendung verwendet werden. Dieses Tool wird in Modul 9 behandelt.

Wenn Sie eine Website veröffentlichen, werden die vorkompilierten Dateien im Ordner Temporäre ASP.NET Dateien gespeichert, wie unten gezeigt. Dateien mit einer *kompilierten Dateierweiterung* sind XML-Dateien, die Abhängigkeiten für bestimmte DLLs definieren. Webform- oder Benutzersteuerelemente werden in zufällige DLLs kompiliert, die mit *App/_Web/_* beginnen.

Wenn Sie das Kontrollkästchen *Diese vorkompilierte Website* zulassen aktiviert lassen, aktivieren Sie das Kontrollkästchen Aufweiterbar, sodass das Markup in Ihren Webformularen und Benutzersteuerelementen nicht in eine DLL vorkompiliert wird, sodass Sie nach der Bereitstellung Änderungen vornehmen können. Wenn Sie das Markup sperren möchten, damit Änderungen am bereitgestellten Inhalt nicht zulässig sind, deaktivieren Sie dieses Kontrollkästchen.

Mit dem Kontrollkästchen *Feste Benennung und einzelne Seitenassemblys* verwenden können Sie die Batchkompilierung deaktivieren, sodass jede Seite in eine Assembly mit festem Namen kompiliert wird. Wenn Sie dieses Kontrollkästchen deaktiviert lassen, können Sie die Batchkompilierung nutzen.

Mit dem Kontrollkästchen *Starke Benennung für vorkompilierte Assemblys* aktivieren können Sie Ihre vorkompilierten Assemblys mit starkem Namen benennen.

> [!NOTE]
> In ASP.NET 1.x mussten Assemblys mit starkem Namen im globalen Assemblycache (GAC) installiert werden. In ASP.NET 2.0 müssen Sie keine Assemblys mit starkem Namen im GAC installieren.

![Ein ASP.NET Anwendungen vorkompilierte Dateien](improvements-in-visual-studio-2005/_static/image8.jpg)

**Abbildung 11:** Ein ASP.NET Anwendungen vorkompilierte Dateien

> [!NOTE]
> In der obigen Anwendung gab es keine web.config-Datei. Wenn dies der Vorgang geschehen wäre, hätte es nach dem Veröffentlichungswebsiteprozess *Als PrecompiledApp.config* bezeichnet werden können.

## <a name="improvements-in-deployment"></a>Verbesserungen bei der Bereitstellung

Wie bei Visual Studio 2002 und 2003 bietet Visual Studio 2005 eine Funktion "Projekt kopieren". Die Funktion wurde jedoch in Visual Studio 2005 verstärkt und heißt jetzt Kopierwebsite.

Das Dialogfeld Website kopieren ist in einen linken und einen rechten Frame aufgeteilt. Der linke Frame wird als Quellwebsite und der rechte Frame als Remotewebsite bezeichnet. Eine Sache, die einige Entwickler verwirren kann, ist, dass die Im rechten Frame angezeigte Website nicht unbedingt eine Remote-Site ist. Es kann sich um eine Site im lokalen Dateisystem oder auf der lokalen Instanz von IIS erachten. Darüber hinaus ist die im linken Rahmen angezeigte Website nicht unbedingt die Quellwebsite, da Sie im Dialogfeld von der Remotewebsite *auf* der Quellwebsite veröffentlichen können.

Wenn Sie ein Projekt auf eine Remotewebsite kopieren, müssen auf dieser Website die FrontPage Server-Erweiterungen installiert sein. Ist dies nicht der Fall, müssen Sie eine Verbindung über FTP herstellen. Wenn Sie hingegen ein Projekt in die lokale IIS-Instanz kopieren, sind FrontPage Server-Erweiterungen nicht erforderlich.

> [!NOTE]
> Wenn Sie versuchen, eine neue Website auf der lokalen IIS-Instanz zu erstellen, und die FrontPage 2002-Servererweiterungen installiert sind, wird eine Fehlermeldung angezeigt, die Sie darauf hinweist, dass das Erstellen von Websites auf einem SharePoint-Server nicht unterstützt wird. In diesem Fall haben Sie die Möglichkeit, die FrontPage 2000-Servererweiterungen zu installieren oder die FrontPage Server-Erweiterungen zu entfernen.

Klicken Sie hier, um eine videobebilderte Vorgehensweise für die Funktion Website kopieren zu erhalten.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Öffnen sie Ein-Bild-Video](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Verbesserungen beim Debuggen

Es gibt vier wichtige Verbesserungen beim Debuggen in Visual Studio 2005.

- Das lokale Debuggen als Nicht-Administrator ist sofort möglich.
- Das Debug-Attribut für das Compilation-Element ist jetzt standardmäßig false.
- Remote-Debugging-Setup und -Konfiguration ist einfacher als zuvor.
- Sie können jetzt eine Website debuggen, die über einen FTP-Speicherort geöffnet wurde.

## <a name="debugging-as-a-non-administrator"></a>Debuggen als Nicht-Administrator

Durch das Hinzufügen des ASP.NET Development Server können Nicht-Administratoren einfach ASP.NET Anwendungen sofort debuggen. Wenn eine ASP.NET Anwendung, die auf dem lokalen Dateisystem ausgeführt wird, gedebuggt wird, startet Visual Studio den ASP.NET Development Server im Kontext des angemeldeten Benutzers. Dieser Benutzer kann diese Anwendung dann ohne zusätzliche Konfiguration debuggen.

## <a name="debug-is-false-by-default"></a>Debuggen ist standardmäßig false

In ASP.NET 1.x wurde das *Debugattribut* im *Kompilierungselement* der Datei web.config standardmäßig auf *true* festgelegt. Es wurde immer empfohlen, dass Entwickler dieses Attribut auf *false* setzen, bevor sie eine Anwendung in der Produktion bereitstellen, aber da die meisten Entwickler die Folgen des Festlegens des Debugattributs auf true nicht vollständig verstehen, haben sie es einfach so belassen, wie es ist.

Das schwerwiegendste Problem bei der Einstellung des Debugattributs auf true besteht darin, dass das ASP.NETs-Batchkompilierungsmodell deaktiviert wird. Daher wird jede Seite in eine separate DLL kompiliert. Wenn eine Webanwendung aus Tausenden von Seiten besteht (die auf keinen Fall unerhört sind), bedeutet dies, dass mehrere tausend kleine DLLs von dieser Anwendung erstellt werden. Diese DLLs sind zwar klein, werden jedoch nicht an einen bestimmten Speicherort im Arbeitsspeicher geladen. Daher verursachen sie eine Fragmentierung im Systemspeicher und können zu OutOfMemoryException-Vorkommen beitragen.

In ASP.NET 2.0 wird das Debugattribut standardmäßig auf false festgelegt. Wie Sie bereits gesehen haben, werden sie beim Debuggen einer ASP.NET Anwendung in Visual Studio 2005 aufgefordert, eine web.config-Datei mit aktiviertem Debuggen hinzuzufügen. Dies führt zu den gleichen Nachteilen wie in ASP.NET 1.x, aber jetzt wird der Entwickler eindeutig gewarnt, dass das Attribut auf false zurückgesetzt werden sollte, bevor die Anwendung in die Produktion verlagert wird.

## <a name="remote-debugging-setup-and-configuration"></a>Remote-Debugging-Setup und -Konfiguration

In Visual Studio 2002/2003 stützte sich das Remote-Debugging auf den Machine Debug Manager (mdm.exe) und den vs7jit.exe-Prozess. Aus diesem Grund war die Fehlerbehebung bei Remote-Debugging-Problemen oft eine Blackbox für Kunden und für PSS oft nicht viel besser.

Visual Studio 2005 entfernt die Abhängigkeit von den Prozessen mdm.exe und vs7jit.exe. Stattdessen wird jetzt der Remote-Debugmonitor-Dienst (msvsmon.exe.) verwendet.

Die Anforderung für das Debuggen in Visual Studio 2005 remote ist ganz einfach. Sie müssen msvsmon.exe vor dem Debuggen auf dem Remoteserver ausführen. Sie können den Remote-Debugmonitor von der Visual Studio-CD installieren oder einfach msvsmon.exe von einer Freigabe aus ausführen, ohne irgendetwas auf dem Webserver zu installieren.

Wenn Sie msvsmon.exe ausführen, wird es wahrscheinlich sein, dass es sich darüber beschwert, dass Ports für Remote-Debugging blockiert werden. Glücklicherweise können Sie die Ports ganz einfach im Warndialog entsperren, wie unten gezeigt.

![Benachrichtigung, dass die Windows-Firewall Remotedebugging blockiert](improvements-in-visual-studio-2005/_static/image9.jpg)

**Abbildung 12:** Benachrichtigung, dass die Windows-Firewall Remotedebugging blockiert

Nachdem Sie die Blockierung der für das Debuggen erforderlichen Ports aufgehoben haben, wird der Remote-Debugging-Monitor wie unten gezeigt angezeigt. Über diese Schnittstelle können Sie Verbindungen überwachen und Debugberechtigungen einfach ändern.

![Der Remote-Debugging-Monitor](improvements-in-visual-studio-2005/_static/image10.jpg)

**Abbildung 13:** Der Remote-Debugging-Monitor

Es ist auch möglich, eine Webanwendung, die über FTP geöffnet wurde, aus der Ferne zu debuggen. Die Schritte sind die gleichen wie die zuvor abgedeckten. Sie müssen jedoch eine Basis-URL für das Durchsuchen des FTP-Projekts angeben, wie weiter oben in diesem Modul beschrieben.

## <a name="lab-2"></a>Labor 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Remote-Debugging mit Visual Studio 2005

Diese Übungseinheit führt Sie durch das Remotedebugging mit Visual Studio 2005.

Klicken Sie hier, um eine Video-Exemplar-Through-Datei zu dieser Übungseinheit zu erhalten.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Öffnen sie Ein-Bild-Video](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

In dieser Übungseinheit müssen Sie über zwei Computer verfügen, von denen auf einem Visual Studio 2005 und auf dem anderen IIS 5 oder höher ausgeführt wird.

1. Öffnen Sie Visual Studio 2005, und erstellen Sie eine neue Website auf dem Remoteserver.

> [!NOTE]
> Sie können die Website auf einer Remote-IIS-Instanz oder über FTP erstellen.

1. Suchen Sie auf dem Remote-Webserver msvsmon.exe auf dem Entwicklungscomputer mithilfe eines UNC-Pfads, und führen Sie ihn aus.  
 Der Standardspeicherort für msvsmon.exe ist //Programmdateien/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.
2. Wenn Sie aufgefordert werden, ports für Remote-Debugging zu entsperren, tun Sie dies.
3. Öffnen Sie auf dem Entwicklungscomputer den CodeBehind für Default.aspx, und legen Sie einen Haltepunkt in der Page/_Load-Methode fest.
4. Starten Sie das Debuggen vom Entwicklungscomputer aus.

Sie sollten den Haltepunkt wie erwartet treffen.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Wie bereits erläutert, wird Visual Studio 2005 mit einem Webserver namens ASP.NET Development Server ausgeliefert. (Der ASP.NET Development Server wird manchmal als Cassini bezeichnet.) Dieser Webserver ist eine bequeme Möglichkeit zum Durchsuchen und Debuggen von Webanwendungen, die auf dem Dateisystem ausgeführt werden.

Der ASP.NET Development Server ist ein eingeschränkter Webserver. Remoteverbindungen sind nicht zulässig, es werden keine Anforderungen von einem anderen Benutzer als dem Benutzer zugelassen, der den Webserver gestartet hat. Es ist auch nicht in der Lage, ASP-Seiten zu bedienen. Nur ASP.NET Ressourcen und HTML-Ressourcen (einschließlich Bilder, CSS-Dateien usw.) werden bereitgestellt.

Der ASP.NET Development Server kann über die Befehlszeile gestartet werden, indem die Datei WebDev.WebServer.exe unter c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/* ausgeführt wird. Im folgenden Dialogfeld werden die verfügbaren Parameter angezeigt.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Abbildung 14**

> [!NOTE]
> Der ASP.NET Development Server wird nicht unterstützt, wenn er explizit über die Befehlszeile gestartet wird.
