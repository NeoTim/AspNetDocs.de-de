---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: Erstellen von Seitenlayouts mit Ansichtsmasterseiten | Microsoft Docs
author: rick-anderson
description: In diesem Tutorial erfahren Sie, wie Sie ein gemeinsames Seitenlayout für mehrere Seiten in Ihrer Anwendung erstellen, indem Sie die Ansichtsmasterseiten nutzen. Sie können eine...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542520"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a>Erstellen von Seitenlayouts mit Ansichtsmasterseiten (C#)

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> In diesem Tutorial erfahren Sie, wie Sie ein gemeinsames Seitenlayout für mehrere Seiten in Ihrer Anwendung erstellen, indem Sie die Ansichtsmasterseiten nutzen. Sie können z. B. eine Ansichtsmasterseite verwenden, um ein zweispaltiges Seitenlayout zu definieren und das zweispaltige Layout für alle Seiten in Ihrer Webanwendung zu verwenden.

## <a name="creating-page-layouts-with-view-master-pages"></a>Erstellen von Seitenlayouts mit Ansichtsmasterseiten

In diesem Tutorial erfahren Sie, wie Sie ein gemeinsames Seitenlayout für mehrere Seiten in Ihrer Anwendung erstellen, indem Sie die Ansichtsmasterseiten nutzen. Sie können z. B. eine Ansichtsmasterseite verwenden, um ein zweispaltiges Seitenlayout zu definieren und das zweispaltige Layout für alle Seiten in Ihrer Webanwendung zu verwenden.

Sie können auch Die Ansichtsmasterseiten nutzen, um allgemeine Inhalte über mehrere Seiten in Ihrer Anwendung freizugeben. Sie können beispielsweise Ihr Website-Logo, Navigationslinks und Banneranzeigen auf einer Ansichtsmasterseite platzieren. Auf diese Weise wird diese Seite in Ihrer Anwendung auf jede Seite in Ihrer Anwendung automatisch angezeigt.

In diesem Tutorial erfahren Sie, wie Sie eine neue Ansichtsmasterseite und eine neue Ansichtsinhaltsseite basierend auf der Masterseite erstellen.

### <a name="creating-a-view-master-page"></a>Erstellen einer Ansichtsmasterseite

Beginnen wir mit dem Erstellen einer Ansichtmasterseite, die ein zweispaltiges Layout definiert. Sie fügen einem MVC-Projekt eine neue Ansichtsmasterseite hinzu, indem Sie mit der rechten Maustaste auf den Ordner Ansichten/Freigegebene Klicken, die Menüoption **Hinzufügen, Neues Element**auswählen und die **Vorlage MVC Ansicht master Page** auswählen (siehe Abbildung 1).

[![Hinzufügen einer Ansichtsmasterseite](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

**Abbildung 01**: Hinzufügen einer Ansichtsmasterseite ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))

Sie können mehr als eine Ansichtsmasterseite in einer Anwendung erstellen. Jede Ansichtsmasterseite kann ein anderes Seitenlayout definieren. Sie möchten beispielsweise, dass bestimmte Seiten über ein zweispaltiges Layout und andere Seiten über ein dreispaltiges Layout verfügen.

Eine Ansichtsmasterseite sieht sehr ähnlich aus wie eine Standard-ASP.NET MVC-Ansicht. Im Gegensatz zu einer normalen Ansicht enthält eine `<asp:ContentPlaceHolder>` Ansichtsmasterseite jedoch ein oder mehrere Tags. Die `<contentplaceholder>` Tags werden verwendet, um die Bereiche der Masterseite zu markieren, die auf einer einzelnen Inhaltsseite überschrieben werden können.

Die Ansichtsmasterseite in Liste 1 definiert beispielsweise ein zweispaltiges Layout. Es enthält `<contentplaceholder>` zwei Tags. Eine `<ContentPlaceHolder>` für jede Spalte.

**Auflistung 1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

Der Text der Ansichtsmasterseite in `<div>` Liste 1 enthält zwei Tags, die den beiden Spalten entsprechen. Die Spaltenklasse Cascading Style Sheet `<div>` wird auf beide Tags angewendet. Diese Klasse wird in dem Stylesheet definiert, das oben auf der Masterseite deklariert ist. Sie können eine Vorschau anzeigen, wie die Ansichtmasterseite gerendert wird, indem Sie zur Entwurfsansicht wechseln. Klicken Sie auf die Registerkarte Entwurf unten links im Quellcode-Editor (siehe Abbildung 2).

[![Vorschau einer Masterseite im Designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

**Abbildung 02**: Vorschau einer Masterseite im Designer ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))

### <a name="creating-a-view-content-page"></a>Erstellen einer Seite zum Anzeigen von Inhalten

Nachdem Sie eine Ansichtsmasterseite erstellt haben, können Sie eine oder mehrere Ansichtsinhaltsseiten basierend auf der Ansichtsmasterseite erstellen. Sie können z. B. eine Inhaltsseite der Indexansicht für den Startcontroller erstellen, indem Sie mit der rechten Maustaste auf den Ordner Ansichten/Startseite klicken, **Hinzufügen, Neues Element**auswählen, die Vorlage **"MVC-Ansichtsinhaltsseite"** auswählen, den Namen Index.aspx eingeben und auf die Schaltfläche **Hinzufügen** klicken (siehe Abbildung 3).

[![Hinzufügen einer Ansichtsinhaltsseite](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

**Abbildung 03**: Hinzufügen einer Ansichtsinhaltsseite ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))

Nachdem Sie auf die Schaltfläche Hinzufügen geklickt haben, wird ein neues Dialogfeld angezeigt, in dem Sie eine Ansichtsmasterseite auswählen können, die der Ansichtsinhaltsseite zugeordnet werden soll (siehe Abbildung 4). Sie können zur Masterseite Site.master-Ansicht navigieren, die wir im vorherigen Abschnitt erstellt haben.

[![Auswählen einer Masterseite](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

**Abbildung 04**: Auswählen einer Masterseite ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))

Nachdem Sie eine neue Ansichtsinhaltsseite basierend auf der Masterseite Site.master erstellt haben, erhalten Sie die Datei in Liste 2.

**Auflistung 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

Beachten Sie, dass `<asp:Content>` diese Ansicht ein `<asp:ContentPlaceHolder>` Tag enthält, das jedem der Tags auf der Ansichtmasterseite entspricht. Jedes `<asp:Content>` Tag enthält ein ContentPlaceHolderID-Attribut, das auf die bestimmte `<asp:ContentPlaceHolder>` Überschreibung verweist.

Beachten Sie außerdem, dass die Inhaltsansichtsseite in Listing 2 keines der normalen öffnenden und schließenden HTML-Tags enthält. Sie enthält z. B. nicht `<html>` `<head>` das Öffnen und Schließen oder Tags. Alle normalen Öffnen- und Schließen-Tags sind in der Ansichtmasterseite enthalten.

Alle Inhalte, die Sie auf einer Ansichtsinhaltsseite `<asp:Content>` anzeigen möchten, müssen in einem Tag platziert werden. Wenn Sie HTML oder andere Inhalte außerhalb dieser Tags platzieren, wird beim Anzeigen der Seite eine Fehlermeldung angezeigt.

Sie müssen nicht jedes `<asp:ContentPlaceHolder>` Tag von einer Masterseite in einer Inhaltsansichtsseite überschreiben. Sie müssen ein `<asp:ContentPlaceHolder>` Tag nur überschreiben, wenn Sie das Tag durch bestimmten Inhalt ersetzen möchten.

Beispielsweise enthält die geänderte Indexansicht in `<asp:Content>` Liste 3 nur zwei Tags. Jedes der `<asp:Content>` Tags enthält Text.

**Auflistung 3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

Wenn die Ansicht in Liste 3 angefordert wird, wird die Seite in Abbildung 5 gerendert. Beachten Sie, dass in der Ansicht eine Seite mit zwei Spalten gerendert wird. Beachten Sie außerdem, dass der Inhalt der Seite "Ansichtsinhalt" mit dem Inhalt der Ansichtsmasterseite zusammengeführt wird

[![Inhaltsseite Indexansicht](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

**Abbildung 05**: Die Inhaltsseite der Indexansicht ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>Ändern des Inhalts von Ansichtsmasterseiten

Ein Problem, das beim Arbeiten mit Ansichtsmasterseiten fast sofort auftritt, ist das Problem, den Inhalt der Ansichtmasterseite zu ändern, wenn verschiedene Ansichtsinhaltsseiten angefordert werden. Sie möchten beispielsweise, dass jede Seite in Ihrer Webanwendung einen eindeutigen Titel hat. Der Titel wird jedoch auf der Ansichtsmasterseite und nicht auf der Seite "Ansichtsinhalt" deklariert. Wie passen Sie also den Seitentitel für jede Ansichtsinhaltsseite an?

Es gibt zwei Möglichkeiten, den Titel zu ändern, der von einer Ansichtsinhaltsseite angezeigt wird. Zunächst können Sie dem Titelattribut der `<%@ page %>` Direktive, die oben auf einer Ansichtsinhaltsseite deklariert ist, einen Seitentitel zuweisen. Wenn Sie beispielsweise der Indexansicht den Seitentitel "Super Great Website" zuweisen möchten, können Sie oben in der Indexansicht die folgende Direktive einfügen:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

Wenn die Indexansicht im Browser gerendert wird, wird der gewünschte Titel in der Browsertitelleiste angezeigt:

[![Browser-Titelleiste](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)

Es gibt eine wichtige Anforderung, die eine Masteransichtsseite erfüllen muss, damit das Titelattribut funktioniert. Die Ansichtsmasterseite `<head runat="server">` muss ein Tag `<head>` anstelle eines normalen Tags für ihre Kopfzeile enthalten. Wenn `<head>` das Tag das Runat="server"-Attribut nicht enthält, wird der Titel nicht angezeigt. Die Standardansichtmasterseite enthält `<head runat="server">` das erforderliche Tag.

Ein alternativer Ansatz zum Ändern von Masterseiteninhalten von einer einzelnen Ansichtsinhaltsseite `<asp:ContentPlaceHolder>` besteht darin, den Bereich, den Sie ändern möchten, in ein Tag zu umschließen. Stellen Sie sich beispielsweise vor, dass Sie nicht nur den Titel, sondern auch die Meta-Tags ändern möchten, die von einer Masteransichtsseite gerendert werden. Die Masteransichtsseite in `<asp:ContentPlaceHolder>` Liste 4 `<head>` enthält ein Tag in ihrem Tag.

**Auflistung 4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

Beachten Sie, dass das `<asp:ContentPlaceHolder>` Tag in Listing 4 Standardinhalt enthält: einen Standardtitel und Standardmeta-Tags. Wenn Sie dieses `<asp:ContentPlaceHolder>` Tag nicht auf einer einzelnen Ansichtsinhaltsseite überschreiben, wird der Standardinhalt angezeigt.

Die Inhaltsansichtsseite in Liste `<asp:ContentPlaceHolder>` 5 überschreibt das Tag, um einen benutzerdefinierten Titel und benutzerdefinierte Meta-Tags anzuzeigen.

**Auflistung 5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a>Zusammenfassung

Dieses Tutorial bietet Ihnen eine grundlegende Einführung zum Anzeigen von Masterseiten und Zum Anzeigen von Inhaltsseiten. Sie haben gelernt, wie Sie neue Ansichtsmasterseiten und auf deren Grundlage Ansichtsinhaltsseiten erstellen. Wir haben auch untersucht, wie Sie den Inhalt einer Ansichtsmasterseite von einer bestimmten Ansichtsinhaltsseite aus ändern können.

> [!div class="step-by-step"]
> [Zurück](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [Weiter](passing-data-to-view-master-pages-cs.md)
