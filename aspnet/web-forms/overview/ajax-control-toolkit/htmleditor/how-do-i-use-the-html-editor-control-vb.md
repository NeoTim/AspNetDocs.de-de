---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: Wie verwende ich das HTML-Editor-Steuerelement? (VB) | Microsoft Docs
author: rick-anderson
description: HTMLEditor ist ein ASP.NET AJAX-Steuerelement, mit dem Sie HTML-Inhalte einfach über Schaltflächen in einer Symbolleiste erstellen und bearbeiten können.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542832"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>Wie verwende ich das HTML-Editor-Steuerelement? (VB)

von [Microsoft](https://github.com/microsoft)

> HTMLEditor ist ein ASP.NET AJAX-Steuerelement, mit dem Sie HTML-Inhalte einfach über Schaltflächen in einer Symbolleiste erstellen und bearbeiten können.

Das Ziel dieses Tutorials ist es, Ihnen einen Überblick über das HTML-Editor-Steuerelement zu geben, das im AJAX Control Toolkit enthalten ist. Der HTML-Editor enthält Optionen zum Ändern der Schriftgröße, Zum Auswählen einer Schriftart, zum Ändern der Hintergrundfarbe, zum Ändern der Vordergrundfarbe, zum Hinzufügen von Links, zum Hinzufügen von Bildern, zum Ändern der Textausrichtung und zum Ausführen von Aus-, Kopier- und Einfügevorgängen (siehe Abbildung 1).

[![Der HTML-Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**Abbildung 01**: Der[HTML-Editor( Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](how-do-i-use-the-html-editor-control-vb/_static/image2.png)

Mit dem HTML-Editor können Sie Inhalte über einen Entwurfsmodus oder direkt HTML eingeben. Sie haben auch die Möglichkeit, eine Vorschau Ihrer HTML-Inhalte anzuzeigen (siehe Abbildung 2).

[![Design-, HTML- und Vorschauschaltflächen](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**Abbildung 02**: Design-, HTML- und Vorschauschaltflächen ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](how-do-i-use-the-html-editor-control-vb/_static/image4.png)

In diesem Tutorial erfahren Sie, wie Sie den HTML-Editor anzeigen, die Symbolleistenschaltflächen anpassen, die im HTML-Editor angezeigt werden, und wie Sie siteübergreifende Skriptangriffe vermeiden.

## <a name="displaying-the-html-editor"></a>Anzeigen des HTML-Editors

Bevor Sie den HTML-Editor in einer ASP.NET Seite verwenden können, müssen Sie der Seite zunächst ein ScriptManager-Steuerelement hinzufügen. Das ScriptManager-Steuerelement befindet sich unter der Registerkarte AJAX-Erweiterungen in der Visual Studio/Visual Web Developer Express-Toolbox.

Sie sollten das ScriptManager-Steuerelement oben auf der Seite vor anderen Steuerelementen auf der Seite platzieren. Sie können es z. B. direkt &lt;unter&gt; dem öffnenden serverseitigen Formulartag platzieren.

Das HTML-Editor-Steuerelement befindet sich in der Toolbox mit den restlichen AJAX Control Toolkit-Steuerelementen. Es heißt Editor-Steuerelement (siehe Abbildung 3).

[![Das HTML-Editor-Steuerelement](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**Abbildung 03**: Das HTML-Editor-Steuerelement([Klicken Sie hier, um das Bild in voller Größe anzuzeigen)](how-do-i-use-the-html-editor-control-vb/_static/image6.png)

Nachdem Sie den HTML-Editor auf eine Seite gezogen haben, können Sie seine Eigenschaften im Eigenschaftenblatt festlegen. Sie möchten z. B. normalerweise die Eigenschaften Breite und Höhe festlegen. Liste 1 enthält die Quelle für eine ASP.NET Seite, die einen HTML-Editor enthält.

**Eintrag 1 - SimpleEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

Die Seite in Liste 1 enthält ein HTML-Editor-Steuerelement, ein Schaltflächensteuerelement und ein Literal-Steuerelement. Wenn Sie auf die Schaltfläche klicken, wird der Inhalt des HTML-Editors im Literal-Steuerelement angezeigt (siehe Abbildung 4).

[![Senden eines Formulars mit einem HTML-Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**Abbildung 04**: Senden eines Formulars mit einem[HTML-Editor ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-html-editor-control-vb/_static/image8.png))

Die HTML Editor Content-Eigenschaft wird verwendet, um den html-Inhalt abzurufen, der in den HTML-Editor eingegeben wurde. Beachten Sie, dass dieser HTML-Inhalt JavaScript enthalten kann. Im nächsten Abschnitt wird erläutert, wie Sie JavaScript-Injektionsangriffe verhindern können.

## <a name="customizing-the-html-editor-toolbar"></a>Anpassen der HTML-Editor-Symbolleiste

Sie können genau anpassen, welche Schaltflächen im Editor angezeigt werden. Sie können z. B. die HTML-Registerkarte entfernen, um zu verhindern, dass Benutzer den HTML-Editor in den HTML-Modus wechseln. Sie können auch die Dropdown-Liste der Schriftgröße entfernen, um zu verhindern, dass Benutzer zu großen Text in einem Forums-Nachrichtenbeitrag erstellen (siehe Abbildung 5).

[![Ein angepasster HTML-Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**Abbildung 05**: Ein angepasster[HTML-Editor ( Klicken Sie hier, um das Bild in voller Größe anzuzeigen](how-do-i-use-the-html-editor-control-vb/_static/image10.png))

Sie passen die Symbolleistenschaltflächen an, indem Sie einen neuen HTML-Editor aus der Basis-Editor-Klasse ableiten. Beispielsweise enthält der benutzerdefinierte Editor in Listing 2 nur Symbolleistenschaltflächen für fett und kursiv. Alle anderen Symbolleistenschaltflächen wurden entfernt. Darüber hinaus wurde die HTML-Registerkarte vom unteren Rand des Editors entfernt (aber die Registerkarten Design und Vorschau sind immer noch vorhanden).

**Auflisten 2\_- App-Code-CustomEditor.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

Sie müssen die Klasse in Listing\_2 zu Ihrem App-Codeordner hinzufügen, damit die Klasse automatisch kompiliert wird. Wenn der\_Ordner App Code nicht auf Ihrer Website vorhanden ist, können Sie den Ordner einfach hinzufügen.

Nachdem Sie einen benutzerdefinierten Editor erstellt haben, können Sie ihn auf die gleiche Weise zu einer ASP.NET Seite hinzufügen, wie Sie den normalen HTML-Editor hinzufügen (siehe Liste 3).

**Eintrag 3 - ShowCustomEditor.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Vermeiden von Cross-Site Scripting (XSS)-Angriffen

Wenn Sie Eingaben von einem Benutzer akzeptieren und diese Eingaben auf Ihrer Website erneut anzeigen, öffnen Sie Ihre Website möglicherweise für Cross-Site Scripting (XSS)-Angriffe. Theoretisch könnte ein böswilliger Hacker JavaScript-Code übermitteln, der ausgeführt wird, wenn die Eingabe erneut angezeigt wird. JavaScript kann verwendet werden, um Benutzerkennwörter oder andere vertrauliche Informationen zu stehlen.

Normalerweise können Sie XSS-Angriffe durch HTML-Codierung aller Eingaben, die Sie von einem Benutzer abrufen, besiegen, bevor Sie sie auf einer Webseite anzeigen. Html-Codierung der Ausgabe des HTML-Editors würde &lt;jedoch&gt; nicht nur Skript-Tags codieren, sondern auch alle HTML-Tags kodieren. Mit anderen Worten, Sie würden alle Formatierungen wie Schriftart, Schriftgröße und Hintergrundfarbe verlieren.

Wenn Sie vertrauliche Informationen von Ihren Benutzern sammeln -- z. B. Kennwörter, Kreditkartennummern und Sozialversicherungsnummern -, sollten Sie keine nicht codierten Inhalte anzeigen, die Sie von einem Benutzer mit dem HTML-Editor abrufen. Sie sollten den HTML-Editor nur in Situationen verwenden, in denen Sie den HTML-Inhalt nicht erneut anzeigen oder der HTML-Inhalt von einer vertrauenswürdigen Partei an Ihre Website übermittelt wird.

Stellen Sie sich beispielsweise vor, dass Sie eine Bloganwendung erstellen. In diesem Fall ist es sinnvoll, den HTML-Editor beim Verfassen von Blogbeiträgen zu verwenden. Sie sind der Einzige, der einen Blogbeitrag einreicht, und vermutlich können Sie sich darauf vertrauen, dass Sie kein bösartiges JavaScript einreichen. Es ist jedoch nicht sinnvoll, den HTML-Editor zu verwenden, wenn anonyme Benutzer Kommentare posten können. Besonders vorsichtig ist es in Situationen, in denen Benutzer vertrauliche Informationen wie Kennwörter übermitteln. Möglicherweise könnte ein böswilliger Benutzer einen Kommentar veröffentlichen, der das richtige JavaScript zum Stehlen eines Kennworts enthält.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial wurde Ihnen eine kurze Übersicht über das HTML-Editor-Steuerelement im AJAX Control Toolkit zur Verfügung gestellt. Sie haben gelernt, wie Sie den HTML-Editor verwenden, um rich content von einem Benutzer zu akzeptieren und den Inhalt an den Server zu senden. Außerdem wurde erläutert, wie Sie die Symbolleistenschaltflächen anpassen können, die vom HTML-Editor angezeigt werden. Schließlich haben Sie gelernt, wie Sie siteübergreifende Skriptangriffe vermeiden können, wenn Sie den HTML-Editor verwenden, um potenziell schädliche Eingaben zu akzeptieren.

> [!div class="step-by-step"]
> [Vorherige](how-do-i-use-the-html-editor-control-cs.md)
