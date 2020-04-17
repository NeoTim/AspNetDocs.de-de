---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programmieren ASP.NET Webseiten (Razor) mit Visual Studio | Microsoft Docs
author: Rick-Anderson
description: In diesem Anhang wird erläutert, wie Sie Visual Studio 2010 oder Visual Web Developer 2010 Express verwenden können, um ASP.NET Webseiten mit der Razor-Syntax zu programmieren.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542897"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Programmieren ASP.NET Webseiten (Razor) mit Visual Studio

 von [Tom FitzMacken](https://github.com/tfitzmac)

> In diesem Artikel wird erläutert, wie Sie Visual Studio oder Visual Web Developer Express verwenden können, um ASP.NET Webseiten (Razor) zu programmieren.
>
> Sie lernen Folgendes
>
> - Was Sie installieren müssen (falls überhaupt), um mit ASP.NET Webseiten in Ihrer Version von Visual Studio zu arbeiten.
> - Hinzufügen von Unterstützung für ASP.NET Webseiten zu Visual Web Developer 2010 Express.
> - Verwenden von Features in Visual Studio zum Arbeiten mit ASP.NET Razor-Seiten, einschließlich IntelliSense und dem Debugger.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Im Tutorial verwendete Softwareversionen
>
>
> - ASP.NET Webseiten (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Dieses Tutorial funktioniert auch mit ASP.NET Webseiten 2, Visual Studio 2012, Visual Studio 2010 und WebMatrix 2.

Sie können ASP.NET Webseiten mit Razor-Syntax mit WebMatrix oder vielen anderen Code-Editoren programmieren. Sie können auch Microsoft Visual Studio verwenden, eine integrierte Entwicklungsumgebung (IDE) mit vollem Umfang, die eine leistungsstarke Reihe von Tools zum Erstellen vieler Anwendungstypen (nicht nur Websites) bereitstellt. Um mit ASP.NET Razor-Seiten zu arbeiten, können Sie [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)verwenden.

Zwei besonders nützliche Funktionen, die Visual Studio für die Programmierung mit ASP.NET Razor-Webseiten bereitstellt, sind:

- *IntelliSense*. Die in Visual Studio integrierte IntelliSense-Funktion ist umfassender als IntelliSense in WebMatrix.
- *Debugger*. Mit dem Debugger können Sie Ihren Code beheben, indem Sie ein Programm während der Ausführung anhalten, Variablen untersuchen und die Codezeile zeilefürsch ieren.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Verwenden von Visual Studio mit verschiedenen Versionen von ASP.NET Webseiten

Um ASP.NET Web-Apps in Visual Studio 2017 zu entwickeln, installieren Sie die **ASP.NET- und Webentwicklungsarbeitsauslastung.**

Visual Studio 2012 und Visual Studio 2013 unterstützen ASP.NET Webseiten. (Die Pakete, die zur Unterstützung ASP.NET Webseiten erforderlich sind, werden bei der Installation von Visual Studio installiert.)

Visual Studio 2010 bietet standardmäßig keine Unterstützung für ASP.NET Webseiten. Um ASP.NET Webseiten mit Visual Studio 2010 zu verwenden, müssen Sie das ASP.NET MVC-Paket installieren. Um ASP.NET Webseiten 2 zu erhalten, installieren Sie ASP.NET MVC 4.

In der folgenden Tabelle wird die Unterstützung für ASP.NET Webseiten in verschiedenen Versionen von Visual Studio zusammengefasst.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET-Webseiten 2** | Installieren ASP.NET MVC 4 | (Inbegriffen) | (Inbegriffen) |
| **ASP.NET-Webseiten 3** |  | Aktualisieren auf ASP.NET Webseiten 3 über NuGet | (Inbegriffen) |

Informationen zum Arbeiten mit Visual Studio 2010 finden Sie unter Installieren von [Support für ASP.NET Webseiten in Visual Studio 2010](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>Starten von Visual Studio über WebMatrix

Wenn Sie ein Projekt in WebMatrix gestartet haben und zu Visual Studio wechseln möchten, stellt WebMatrix eine Schaltfläche zum einfachen Öffnen des Projekts in Visual Studio bereit. Sie müssen Visual Studio auf Ihrem Computer installiert haben, damit diese Schaltfläche aktiviert werden kann. Die folgende Abbildung zeigt die Schaltfläche in WebMatrix.

![Starten von Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Wenn Sie auf die Schaltfläche klicken, wird das Projekt in Visual Studio geöffnet. Sie können problemlos zwischen WebMatrix und Visual Studio hin- und herwechseln. Sie werden benachrichtigt, wenn dateien in der anderen Umgebung geändert wurden und neu geladen werden müssen, um die neuesten Änderungen zu erhalten.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Erstellen ASP.NET Razor-Site in Visual Studio

So erstellen Sie eine ASP.NET Razor-Website in Visual Studio:

1. Öffnen Sie Visual Studio.
2. Klicken Sie im Menü **Datei** auf **Neue Website**.

    ![Erstellen einer neuen Website](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. Wählen Sie im Dialogfeld **Neue Website** die zu verwendende Sprache aus (Visual C oder Visual Basic).
4. Wählen Sie die **Vorlage ASP.NET Website (Razor)** aus.

    ![Rasierer-Website](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. Klicken Sie auf **OK**.

Ihr neues Projekt ist vorhanden und wird mit einigen Standardwebseiten gefüllt, die Ihnen bei den ersten Informationen helfen.

### <a name="using-intellisense"></a>Using IntelliSense

Nachdem Sie nun eine Website erstellt haben, können Sie sehen, wie IntelliSense in Visual Studio funktioniert.

1. Öffnen Sie auf der Website, die Sie gerade erstellt haben, die Seite *Default.cshtml.*
2. Geben `<h3>` Sie `@ServerInfo.` nach den Tags auf der Seite (einschließlich des Punktes) ein. Beachten Sie, wie IntelliSense `ServerInfo` die verfügbaren Methoden für den Helfer in einer Dropdownliste anzeigt.

    ![Intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Wählen `GetHtml` Sie die Methode aus der Liste aus, und drücken Sie dann die Eingabetaste. IntelliSense füllt die Methode automatisch aus. (Wie bei jeder Methode in C- müssen Sie Zeichen nach der Methode hinzufügen.) `()` Der abgeschlossene `GetHtml` Code für die Methode sieht wie im folgenden Beispiel aus:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Drücken Sie Strg+F5, um die Seite auszuführen. So sieht die Seite aus, wenn sie in einem Browser angezeigt wird:

    ![Standardseite im Browser](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Schließen Sie den Browser.

### <a name="using-the-debugger"></a>Verwenden des Debuggers

1. Fügen Sie oben auf der Seite *Default.cshtml* `Page.Title`nach der Zeile, die mit beginnt, die folgende Codezeile hinzu:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. Klicken Sie am grauen Rand des Editors links neben dem Code, um einen *Haltepunkt*hinzuzufügen. Ein Haltepunkt ist ein Marker, der den Debugger anweist, das Programm zu diesem Zeitpunkt nicht mehr auszuführen, damit Sie sehen können, was passiert.

    ![Sollpunkt festlegen](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. Entfernen Sie den `ServerInfo.GetHtml` Aufruf der Methode, `@myTime` und fügen Sie der Variablen an ihrer Stelle einen Aufruf hinzu. Dieser Aufruf zeigt den aktuellen Zeitwert an, der von der neuen Codezeile zurückgegeben wird.
4. Drücken Sie F5, um die Seite im Debugger auszuführen. Die Seite wird auf dem von Ihnen festgelegten Haltepunkt angehalten. Die folgende Abbildung zeigt, wie die Seite im Editor mit dem Haltepunkt (gelb) aussieht.

    ![Debug-Haltepunkt](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Klicken Sie in der Symbolleiste Debuggen auf die Schaltfläche **Schritt in** (oder drücken Sie F11), um die nächste Codezeile auszuführen. Jedes Mal, wenn Sie auf diese Schaltfläche klicken, leiten Sie die Ausführung zur nächsten Codezeile weiter.

    ![Schritt in die Taste](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. Untersuchen Sie den `myTime` Wert der Variablen, indem Sie den Mauszeiger darüber halten oder die Werte überprüfen, die in den Fenstern **Locals** und **Call Stack** angezeigt werden. Visual Studio zeigt den Wert der Variablen an.

    ![Zeitwert anzeigen](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Wenn Sie die Variable untersuchen und den Code durchlaufen, drücken Sie F5, um die Ausführung der Seite fortzusetzen, ohne an jeder Zeile anzuhalten. Wenn Sie den gesamten Code durchlaufen haben, zeigt der Browser die Seite an.

Weitere Informationen zum Debugger und zum Debuggen von Code in Visual Studio finden Sie unter [Exemplarische Vorgehensweise: Debuggen von Webseiten in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Verwenden von Razor in ASP.NET MVC-Projekten mit Visual Studio

Die Razor-Syntax wird auch in ASP.NET MVC-Projekten ausgiebig verwendet. MVC ist eine leistungsstarke, musterbasierte Möglichkeit, dynamische Websites zu erstellen. Wenn ihre ASP.NET Webseiten-Website schwierig zu verwalten ist, sollten Sie sie in eine ASP.NET MVC-Anwendung konvertieren. Ein Beispiel für das Erstellen einer MVC-Anwendung finden Sie unter [Erste Schritte mit ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Installieren der Unterstützung für ASP.NET Webseiten in Visual Studio 2010

In diesem Abschnitt wird gezeigt, wie Sie Visual Web Developer Express 2010 und die ASP.NET Web Pages Tools for Visual Studio installieren.

1. Wenn Sie noch nicht über den Web Platform Installer verfügen, laden Sie ihn von der folgenden URL herunter:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Führen Sie das Web platform Installer aus.
3. Klicken Sie auf die Registerkarte **Produkte.**

    ![Registerkarte WebPI-Produkte](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. Suchen Sie nach **ASP.NET MVC 4** (für ASP.NET Webseiten 2) und klicken Sie dann auf **Hinzufügen**. Zu diesen Produkten gehören Visual Studio-Tools zum Erstellen ASP.NET Razor-Websites.

    ![WebPi-Installationsoptionen](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Klicken Sie auf **Installieren,** um die Installation abzuschließen.
