---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Erstellen eines neuen ASP.NET MVC-Projekts | Microsoft Docs
author: rick-anderson
description: Schritt 1 zeigt Ihnen, wie Sie die grundlegende NerdDinner-Anwendungsstruktur an Ort und Stelle setzen.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541480"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Erstellen eines neuen ASP.NET MVC-Projekts

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 1 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 1 zeigt Ihnen, wie Sie die grundlegende NerdDinner-Anwendungsstruktur an Ort und Stelle setzen.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner Schritt 1:&gt;Datei- Neues Projekt

Wir beginnen unsere NerdDinner-Anwendung, indem wir den Menüpunkt **Datei-&gt;Neues Projekt** entweder in Visual Studio 2008 oder im kostenlosen Visual Web Developer 2008 Express auswählen.

Dadurch wird der Dialog "Neues Projekt" angezeigt. Um eine neue ASP.NET MVC-Anwendung zu erstellen, wählen wir den Knoten "Web" auf der linken Seite des Dialogfelds und dann die Projektvorlage "ASP.NET MVC Web Application" auf der rechten Seite aus:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Wichtig: Stellen Sie sicher, dass Sie ASP.NET MVC heruntergeladen und installiert haben – andernfalls wird es nicht im Dialogfeld Neues Projekt angezeigt. Sie können V2 des [Microsoft Web Platform Installerverwendens](https://www.microsoft.com/web/downloads/platform.aspx) verwenden, wenn Sie es noch nicht&gt;installiert haben (ASP.NET MVC ist im Abschnitt "Webplattform-Frameworks und Laufzeiten" verfügbar).*

Wir nennen das neue Projekt, das wir erstellen werden, "NerdDinner" und klicken dann auf die Schaltfläche "OK", um es zu erstellen.

Wenn wir auf "OK" klicken, ruft Visual Studio ein zusätzliches Dialogfeld auf, in dem wir aufgefordert werden, optional auch ein Komponententestprojekt für die neue Anwendung zu erstellen. Dieses Komponententestprojekt ermöglicht es uns, automatisierte Tests zu erstellen, die die Funktionalität und das Verhalten unserer Anwendung überprüfen (etwas, das wir später in diesem Tutorial behandeln werden).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

Die Dropdownliste "Testframework" im obigen Dialogfeld wird mit allen verfügbaren ASP.NET MVC-Komponententestprojektvorlagen aufgefüllt, die auf dem Computer installiert sind. Versionen können für NUnit, MBUnit und XUnit heruntergeladen werden. Das integrierte Visual Studio Unit Test-Framework wird ebenfalls unterstützt.

*Hinweis: Das Visual Studio Unit Test Framework ist nur mit Visual Studio 2008 Professional und höheren Versionen verfügbar. Wenn Sie VS 2008 Standard Edition oder Visual Web Developer 2008 Express verwenden, müssen Sie die NUnit-, MBUnit- oder XUnit-Erweiterungen für ASP.NET MVC herunterladen und installieren, damit dieses Dialogfeld angezeigt wird. Das Dialogfeld wird nicht angezeigt, wenn keine Testframeworks installiert sind.*

Wir verwenden den Standardnamen "NerdDinner.Tests" für das von uns erstellte Testprojekt und die Frameworkoption "Visual Studio Unit Test". Wenn wir auf die Schaltfläche "ok" klicken, erstellt Visual Studio eine Lösung für uns mit zwei Projekten - eines für unsere Webanwendung und eines für unsere Komponententests:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>Untersuchen der NerdDinner-Verzeichnisstruktur

Wenn Sie eine neue ASP.NET MVC-Anwendung mit Visual Studio erstellen, wird dem Projekt automatisch eine Reihe von Dateien und Verzeichnissen hinzugefügt:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET MVC-Projekte verfügen standardmäßig über sechs Verzeichnisse der obersten Ebene:

| **Verzeichnis** | **Zweck** |
| --- | --- |
| **/Controller** | Wo Sie Controller-Klassen einfügen, die URL-Anforderungen verarbeiten |
| **/Modelle** | Wo Sie Klassen setzen, die Daten darstellen und bearbeiten |
| **/Ansichten** | Wo Sie UI-Vorlagendateien einfügen, die für das Rendern der Ausgabe verantwortlich sind |
| **/Skripte** | Wo Sie JavaScript-Bibliotheksdateien und -skripts (.js) |
| **/Inhalt** | Wo Sie CSS- und Bilddateien und andere nicht-dynamische/nicht-JavaScript-Inhalte |
| **/App-Daten\_** | Wo Sie Datendateien speichern, die Sie lesen/schreiben möchten. |

ASP.NET MVC erfordert diese Struktur nicht. Tatsächlich partitionieren Entwickler, die an großen Anwendungen arbeiten, die Anwendung in der Regel über mehrere Projekte hinweg, um sie leichter zu verwalten (z. B. Datenmodellklassen werden häufig in einem separaten Klassenbibliotheksprojekt von der Webanwendung verwendet). Die Standardprojektstruktur stellt jedoch eine nette Standardverzeichniskonvention bereit, die wir verwenden können, um unsere Anwendungsprobleme sauber zu halten.

Wenn wir das Verzeichnis /Controllers erweitern, werden wir feststellen, dass Visual Studio dem Projekt standardmäßig zwei Controllerklassen – HomeController und AccountController – hinzugefügt hat:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

Wenn wir das Verzeichnis /Views erweitern, werden drei Unterverzeichnisse – /Home, /Account und /Shared – sowie mehrere Vorlagendateien darin standardmäßig ebenfalls zum Projekt hinzugefügt:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

Wenn wir die Verzeichnisse /Content und /Scripts erweitern, finden wir eine Site.css-Datei, die zum Formatieren aller HTML-Dateien auf der Website verwendet wird, sowie JavaScript-Bibliotheken, die ASP.NET AJAX- und jQuery-Unterstützung innerhalb der Anwendung aktivieren können:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

Wenn wir das NerdDinner.Tests-Projekt erweitern, finden wir zwei Klassen, die Komponententests für unsere Controllerklassen enthalten:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Diese von Visual Studio hinzugefügten Standarddateien bieten uns eine grundlegende Struktur für eine funktionierende Anwendung - komplett mit Homepage, über Seite, Kontoanmeldung/Logout/Registrierungsseiten und einer nicht behandelten Fehlerseite (alle verkabelt und aus dem Feld heraus).

### <a name="running-the-nerddinner-application"></a>Ausführen der NerdDinner-Anwendung

Wir können das Projekt ausführen, indem wir entweder die Menüelemente **Debug-&gt;Debugging starten** oder **Debug-&gt;Start ohne Debugging** auswählen:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Dadurch wird der integrierte ASP.NET Webserver mit Visual Studio gestartet und unsere Anwendung ausgeführt:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Unten ist die Startseite für unser neues Projekt (URL: "/"),wenn es läuft:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

Wenn Sie auf die Registerkarte "Über" klicken, wird eine Übersichtsseite angezeigt (URL: "/Home/About"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Ein Klick auf den Link "Anmelden" oben rechts führt uns zu einer Login-Seite (URL: "/Konto/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Wenn wir kein Login-Konto haben, können wir auf den Registerlink (URL: "/Konto/Register") klicken, um eines zu erstellen:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

Der Code zum Implementieren der oben genannten Home-, about- und logout/register-Funktionalität wurde standardmäßig hinzugefügt, als wir unser neues Projekt erstellt haben. Wir verwenden es als Ausgangspunkt unserer Anwendung.

### <a name="testing-the-nerddinner-application"></a>Testen der NerdDinner-Anwendung

Wenn wir die Professional Edition oder eine höhere Version von Visual Studio 2008 verwenden, können wir die integrierte Komponententest-IDE-Unterstützung in Visual Studio verwenden, um das Projekt zu testen:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

Wenn Sie eine der oben genannten Optionen auswählen, wird der Bereich "Testergebnisse" innerhalb der IDE geöffnet und uns der Status "Pass/Fail" für die 27 Komponententests in unserem neuen Projekt angezeigt, die die integrierte Funktionalität abdecken:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Später in diesem Tutorial werden wir mehr über automatisierte Tests sprechen und zusätzliche Komponententests hinzufügen, die die von uns implementierten Anwendungsfunktionen abdecken.

### <a name="next-step"></a>Nächster Schritt

Wir haben jetzt eine grundlegende Anwendungsstruktur eingerichtet. Erstellen wir nun [eine Datenbank zum Speichern unserer Anwendungsdaten](create-a-database.md).

> [!div class="step-by-step"]
> [Zurück](introducing-the-nerddinner-tutorial.md)
> [Weiter](create-a-database.md)
