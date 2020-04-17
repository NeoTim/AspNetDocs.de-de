---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Master-Seiten | Microsoft Docs
author: rick-anderson
description: Eine der wichtigsten Komponenten für eine erfolgreiche Website ist ein konsistentes Erscheinungsbild. In ASP.NET 1.x verwendeten Entwickler Benutzersteuerelemente, um allgemeine Seiten-Elem zu replizieren...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543183"
---
# <a name="master-pages"></a>Masterseiten

von [Microsoft](https://github.com/microsoft)

> Eine der wichtigsten Komponenten für eine erfolgreiche Website ist ein konsistentes Erscheinungsbild. In ASP.NET 1.x verwendeten Entwickler Benutzersteuerelemente, um allgemeine Seitenelemente in einer Webanwendung zu replizieren. Obwohl dies sicherlich eine praktikabelLösung ist, hat die Verwendung von Benutzersteuerelementen einige Nachteile. Beispielsweise erfordert eine Änderung der Position eines Benutzersteuerelements eine Änderung an mehreren Seiten auf einer Website. Benutzersteuerelemente werden auch in der Entwurfsansicht nicht gerendert, nachdem sie auf einer Seite eingefügt wurden.

Eine der wichtigsten Komponenten für eine erfolgreiche Website ist ein konsistentes Erscheinungsbild. In ASP.NET 1.x verwendeten Entwickler Benutzersteuerelemente, um allgemeine Seitenelemente in einer Webanwendung zu replizieren. Obwohl dies sicherlich eine praktikabelLösung ist, hat die Verwendung von Benutzersteuerelementen einige Nachteile. Beispielsweise erfordert eine Änderung der Position eines Benutzersteuerelements eine Änderung an mehreren Seiten auf einer Website. Benutzersteuerelemente werden auch in der Entwurfsansicht nicht gerendert, nachdem sie auf einer Seite eingefügt wurden.

ASP.NET 2.0 führt Masterseiten ein, um ein konsistentes Erscheinungsbild zu erhalten, und wie Sie bald sehen werden, stellen Masterseiten eine signifikante Verbesserung gegenüber der Benutzersteuerungsmethode dar.

## <a name="why-master-pages"></a>Warum Masterseiten?

Sie fragen sich vielleicht, warum Masterseiten in ASP.NET 2.0 benötigt wurden. Schließlich verwenden Websiteentwickler bereits Benutzersteuerelemente in ASP.NET 1.x, um Inhaltsbereiche zwischen Seiten freizugeben. Es gibt mehrere Gründe, warum Benutzersteuerelemente eine weniger optimale Lösung zum Erstellen eines gemeinsamen Layouts sind.

Benutzersteuerelemente definieren das Seitenlayout nicht. Stattdessen definieren sie das Layout und die Funktionalität für einen Teil einer Seite. Die Unterscheidung zwischen diesen beiden ist wichtig, da sie die Verwaltbarkeit einer Benutzersteuerungslösung erheblich erschwert. Wenn Sie beispielsweise die Position eines Benutzersteuerelements auf ihrer Seite ändern möchten, müssen Sie die tatsächliche Seite bearbeiten, auf der das Benutzersteuerelement angezeigt wird. Das ist in Ordnung, wenn Sie nur ein paar Seiten haben, aber in großen Websites, es wird schnell ein Site-Management-Albtraum!

Ein weiterer Nachteil der Verwendung von Benutzersteuerelementen zum Definieren eines gemeinsamen Layouts ist in der Architektur von ASP.NET selbst verwurzelt. Wenn ein öffentliches Mitglied eines Benutzersteuerelements geändert wird, müssen Sie alle Seiten neu kompilieren, die das Benutzersteuerelement verwenden. Im Gegenzug ASP.NET ihre Seiten dann erneut in JiE, wenn auf sie zum ersten Mal zugegriffen wird. Dies führt erneut zu einer nicht skalierbaren Architektur und einem Standortverwaltungsproblem für größere Standorte.

Beide Probleme (und viele mehr) werden von Masterseiten in ASP.NET 2.0 gut behandelt.

## <a name="how-master-pages-work"></a>Funktionsweise von Masterseiten

Eine Masterseite ist analog zu einer Vorlage für andere Seiten. Seitenelemente, die von anderen Seiten gemeinsam genutzt werden sollen (z. B. Menüs, Rahmen usw.), werden der Masterseite hinzugefügt. Wenn der Website neue Seiten hinzugefügt werden, können Sie sie einer Masterseite zuordnen. Eine Seite, die einer Masterseite zugeordnet ist, wird als **Inhaltsseite**bezeichnet. Standardmäßig übernimmt eine Inhaltsseite die Darstellung von der Masterseite. Wenn Sie jedoch eine Masterseite erstellen, können Sie Teile der Seite definieren, die die Inhaltsseite durch ihren eigenen Inhalt ersetzen kann. Diese Abschnitte werden mit einem neuen Steuerelement definiert, das in ASP.NET 2.0 eingeführt wurde. das **ContentPlaceHolder-Steuerelement.**

Eine Masterseite kann eine beliebige Anzahl von ContentPlaceHolder-Steuerelementen (oder gar keine) enthalten. Auf der Inhaltsseite wird der Inhalt aus den ContentPlaceHolder-Steuerelementen in **den Inhaltssteuerelementen** angezeigt, ein weiteres neues Steuerelement in ASP.NET 2.0. Standardmäßig sind die Inhaltsseiten Inhaltssteuerelemente leer, sodass Sie eigene Inhalte bereitstellen können. Wenn Sie den Inhalt der Masterseite innerhalb der Inhaltssteuerelemente verwenden möchten, können Sie dies tun, wie Sie weiter unten in dieser Unterrichtseinheit sehen werden. Das Content-Steuerelement wird dem ContentPlaceHolder-Steuerelement über das ContentPlaceHolderID-Attribut des Inhaltssteuerelements zugeordnet. Der folgende Code ordnet ein Content-Steuerelement einem ContentPlaceHolder-Steuerelement namens mainBody auf einer Masterseite zu.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Sie werden oft hören, wie Masterseiten als Basisklasse für andere Seiten beschrieben werden. Das stimmt eigentlich nicht. Die Beziehung zwischen Masterseiten und Inhaltsseiten ist keine Vererbung.

**Abbildung 1** zeigt eine Masterseite und eine zugehörige Inhaltsseite, wie sie in Visual Studio 2005 angezeigt werden. Sie können das ContentPlaceHolder-Steuerelement auf der Masterseite und das entsprechende Inhaltssteuerelement auf der Inhaltsseite sehen. Beachten Sie, dass der Inhalt der Masterseiten, der sich außerhalb des ContentPlaceHolder befindet, auf der Inhaltsseite sichtbar, aber abgeblendet ist. Nur der Inhalt innerhalb des ContentPlaceHolder kann durch die Inhaltsseite ersetzt werden. Alle anderen Inhalte, die von der Masterseite stammen, sind unveränderlich.

![Eine Masterseite und die zugehörige Inhaltsseite](master-pages/_static/image1.jpg)

**Abbildung 1:** Eine Masterseite und die zugehörige Inhaltsseite

## <a name="creating-a-master-page"></a>Erstellen einer Masterseite

So erstellen Sie eine neue Masterseite:

1. Öffnen Sie Visual Studio 2005, und erstellen Sie eine neue Website.
2. Klicken Sie auf Datei, Neu, Datei.
3. Wählen Sie Masterdatei aus dem Dialogfeld Neues Element hinzufügen aus, wie in **Abbildung 2**gezeigt.
4. Klicken Sie auf Hinzufügen.

![Erstellen einer neuen Masterseite](master-pages/_static/image2.jpg)

**Abbildung 2:** Erstellen einer neuen Masterseite

Beachten Sie, dass die Dateierweiterung für eine Masterseite *.master ist.* Dies ist eine der Möglichkeiten, wie sich eine Masterseite von einer normalen Seite unterscheidet. Der andere Hauptunterschied besteht darin, @Page dass die Masterseite @Master anstelle einer Richtlinie eine Direktive enthält. Wechseln Sie zur Quellansicht für die Masterseite, die Sie gerade erstellt haben, und überprüfen Sie den Code.

Eine neue Masterseite verfügt standardmäßig über ein ContentPlaceHolder-Steuerelement. In den meisten Fällen ist es sinnvoller, zuerst die allgemeinen Seitenelemente zu erstellen und dann ContentPlaceHolder-Steuerelemente dort einzufügen, wo benutzerdefinierter Inhalt gewünscht wird. In diesen Fällen möchten Entwickler das standardmäßige ContentPlaceHolder-Steuerelement löschen und neue einfügen, während die Seite entwickelt wird. ContentPlaceHolder-Steuerelemente können nicht in der Größe geändert werden, obwohl sie Größen-Handles anzeigen. Die ContentPlaceHolder-Steuerelementgrößen basieren automatisch auf dem Inhalt, der mit einer Ausnahme enthalten ist. Wenn Sie ein ContentPlaceHolder-Steuerelement innerhalb eines Blockelements, z. B. einer Tabellenzelle, platzieren, wird es entsprechend der Größe des Elements vergrößert.

## <a name="lab-1-working-with-master-pages"></a>Lab 1 Arbeiten mit Masterseiten

In dieser Übungseinheit erstellen Sie eine neue Masterseite und definieren drei ContentPlaceHolder-Steuerelemente. Anschließend erstellen Sie eine neue Inhaltsseite und ersetzen den Inhalt aus mindestens einem der ContentPlaceHolder-Steuerelemente.

1. Erstellen Sie eine Masterseite, und fügen Sie ContentPlaceHolder-Steuerelemente ein. 

    1. Erstellen Sie eine neue Masterseite, wie oben beschrieben.
    2. Löschen Sie das standardmäßige ContentPlaceHolder-Steuerelement.
    3. Wählen Sie das ContentPlaceHolder-Steuerelement aus, indem Sie auf den schattierten oberen Rand des Steuerelements klicken und es dann löschen, indem Sie auf die DEL-Taste auf Ihrer Tastatur klicken.
    4. Fügen Sie eine neue Tabelle mit der *Kopfzeile und* der Seitenvorlage ein, wie in Abbildung 3 dargestellt. Ändern Sie die Breite und Höhe auf jeweils 90 %, sodass die gesamte Tabelle im Designer sichtbar ist.

![](master-pages/_static/image3.jpg)

**Abbildung 3**

1. Platzieren Sie den Cursor in jede Zelle der Tabelle, und legen Sie die *Eigenschaft "tabellen- "The" von "the "the "the "the "the "the "the "the "the "top" fest.* *top*
2. Fügen Sie in der Toolbox ein ContentPlaceHolder-Steuerelement in die obere Zelle der Tabelle (die Kopfzeile) ein.
3. Wenn Sie dieses ContentPlaceHolder-Steuerelement einfügen, werden Sie feststellen, dass die Zeilenhöhe fast die gesamte Seite einnimmt, wie in Abbildung 4 dargestellt. Machen Sie sich darüber an dieser Stelle keine Sorgen.

![Der leere Bereich befindet sich in derselben Zelle wie der ContentPlaceHolder](master-pages/_static/image1.gif)

**Abbildung 4:** Der leere Bereich befindet sich in derselben Zelle wie der ContentPlaceHolder

1. Platzieren Sie ein ContentPlaceHolder-Steuerelement in den beiden anderen Zellen. Nachdem die anderen ContentPlaceHolder-Steuerelemente eingefügt wurden, sollte die Größe der Tabellenzellen wie erwartet sein. Die Seite sollte nun wie die seite in **Abbildung 5**aussehen.

![Der Master mit allen ContentPlaceHolder-Steuerelementen. Beachten Sie, dass die Zellenhöhe für die Kopfzelle jetzt das ist, was sie sein sollte](master-pages/_static/image2.gif)

**Abbildung 5:** Der Master mit allen ContentPlaceHolder-Steuerelementen. Beachten Sie, dass die Zellenhöhe für die Kopfzelle jetzt das ist, was sie sein sollte

1. Geben Sie textihrer Wahl in jedes der drei ContentPlaceHolder-Steuerelemente ein.
2. Speichern Sie die Masterseite als übung1.master.
3. Erstellen Sie ein neues Webformular, und ordnen Sie es der masterseite exercise1.master zu.
4. Wählen Sie Datei, Neu, Datei in Visual Studio 2005 aus.
5. Wählen Sie **WebFormular** im Dialogfeld Neues Element hinzufügen aus.
6. Stellen Sie sicher, dass das Kontrollkästchen Masterseite auswählen aktiviert ist, wie in Abbildung 6 dargestellt.

![Hinzufügen einer neuen Inhaltsseite](master-pages/_static/image3.gif)

**Abbildung 6:** Hinzufügen einer neuen Inhaltsseite

1. Klicken Sie auf Hinzufügen.
2. Wählen Sie exercise1.master im Dialogfeld Masterseite auswählen aus, wie in Abbildung 7 dargestellt.
3. Klicken Sie auf OK, um die neue Inhaltsseite hinzuzufügen.

Die neue Inhaltsseite wird in Visual Studio mit einem Inhaltssteuerelement für jedes ContentPlaceHolder-Steuerelement auf der Masterseite angezeigt. Standardmäßig sind die Inhaltssteuerelemente leer, sodass Sie eigene Inhalte hinzufügen können. Wenn Sie möchten, dass sie den Inhalt aus dem ContentPlaceHolder-Steuerelement auf der Masterseite verwenden, klicken Sie einfach auf das Smarttag-Symbol (den kleinen schwarzen Pfeil in der oberen rechten Ecke des Steuerelements) und wählen Sie *Standard auf Master-Inhalte* aus dem Smarttag aus, wie in **Abbildung 8**dargestellt. Wenn Sie dies tun, ändert sich das Menüelement in *Benutzerdefinierte Inhalte erstellen*. Wenn Sie an diesem Punkt darauf klicken, wird der Inhalt von der Masterseite entfernt, sodass Sie benutzerdefinierte Inhalte für dieses bestimmte Inhaltssteuerelement definieren können.

![Festlegen eines Inhaltssteuerelements auf Standard auf den Masterseiteninhalt](master-pages/_static/image4.gif)

**Abbildung 7:** Festlegen eines Inhaltssteuerelements auf Standard auf den Masterseiteninhalt

## <a name="connecting-master-page-and-content-pages"></a>Verbinden von Masterseiten und Inhaltsseiten

Die Zuordnung zwischen einer Masterseite und einer Inhaltsseite kann auf eine von vier verschiedenen Arten konfiguriert werden:

- Das <strong>MasterPageFile-Attribut</strong> der @Page Direktive
- Festlegen der **Page.MasterPageFile-Eigenschaft** im Code.
- Das ** &lt;&gt; Seitenelement** in der Anwendungskonfigurationsdatei (web.config im Stammordner der Anwendung)
- Das ** &lt;&gt; Seitenelement** in einer Unterordnerkonfigurationsdatei (web.config in einem Unterordner)

## <a name="masterpagefile-attribute"></a>MasterPageFile-Attribut

Das MasterPageFile-Attribut erleichtert das Anwenden einer Masterseite auf eine bestimmte ASP.NET Seite. Es ist auch die Methode, die zum Anwenden der Masterseite verwendet wird, wenn Sie das Kontrollkästchen **Masterseite auswählen** aktivieren, wie Sie es in Übung 1 getan haben.

## <a name="setting-pagemasterpagefile-in-code"></a>Festlegen von Page.MasterPageFile im Code

Durch Festlegen der MasterPageFile-Eigenschaft im Code können Sie zur Laufzeit eine bestimmte Masterseite auf Ihren Inhalt anwenden. Dies ist nützlich, wenn Sie möglicherweise eine bestimmte Masterseite basierend auf einer Benutzerrolle oder anderen Kriterien anwenden müssen. Die MasterPageFile-Eigenschaft muss in der PreInit-Methode festgelegt werden. Wenn sie nach der PreInit-Methode festgelegt wird, wird eine InvalidOperationException ausgelöst. Die Seite, auf der diese Eigenschaft festgelegt wird, muss auch über ein Inhaltssteuerelement als Steuerelement der obersten Ebene für die Seite verfügen. Andernfalls wird eine HttpException ausgelöst, wenn die MasterPageFile-Eigenschaft festgelegt wird.

## <a name="using-the-ltpagesgt-element"></a>Verwenden &lt;der&gt; Seiten Element

Sie können eine Masterseite für Ihre Seiten konfigurieren, &lt;indem&gt; Sie das masterPageFile-Attribut im Pages-Element der Datei web.config festlegen. Beachten Sie bei der Verwendung dieser Methode, dass web.config-Dateien, die in der Anwendungsstruktur niedriger sind, diese Einstellung überschreiben können. Jedes MasterPageFile-Attribut, @Page das in einer Direktive festgelegt ist, überschreibt diese Einstellung ebenfalls. Die &lt;Verwendung&gt; des Pages-Elements erleichtert das Erstellen einer *Mastermasterseite,* die bei Bedarf in bestimmten Ordnern oder Dateien überschrieben werden kann.

## <a name="properties-in-master-pages"></a>Eigenschaften in Masterseiten

Eine Masterseite kann Eigenschaften verfügbar machen, indem diese Eigenschaften einfach innerhalb der Masterseite öffentlich gemacht werden. Der folgende Code definiert beispielsweise eine Eigenschaft namens SomeProperty:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Um über die Seite Inhalt auf die SomeProperty-Eigenschaft zuzugreifen, müssen Sie die Master-Eigenschaft wie folgt verwenden:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Verschachteln von Masterseiten

Masterseiten sind die perfekte Lösung, um ein gemeinsames Erscheinungsbild in einer großen Webanwendung zu gewährleisten. Es ist jedoch nicht ungewöhnlich, dass bestimmte Teile einer großen Website eine gemeinsame Schnittstelle verwenden, während andere Teile eine andere Schnittstelle gemeinsam nutzen. Um diesen Bedarf zu beheben, sind mehrere Masterseiten die perfekte Lösung. Dies betrifft jedoch nicht die Tatsache, dass eine große Anwendung bestimmte Komponenten (z. B. ein Menü) enthält, die von allen Seiten und anderen Komponenten gemeinsam genutzt werden, die nur für bestimmte Abschnitte der Website freigegeben sind. Für diese Art von Situation füllen verschachtelte Masterseiten das Bedürfnis gut. Wie Sie gesehen haben, besteht eine normale Masterseite aus einer Masterseite und einer Inhaltsseite. In einer verschachtelten Masterseitensituation gibt es zwei Masterseiten. einen übergeordneten Master und einen untergeordneten Master. Die untergeordnete Masterseite ist auch eine Inhaltsseite, und ihr Master ist die übergeordnete Masterseite.

Hier ist der Code für eine typische Masterseite:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

In einem verschachtelten Masterszenario wäre dies der übergeordnete Master. Eine andere Masterseite würde diese Seite als Masterseite verwenden, und dieser Code würde wie folgt aussehen:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Beachten Sie, dass in diesem Szenario der untergeordnete Master auch eine Inhaltsseite für den übergeordneten Master ist. Der gesamte Inhalt des untergeordneten Masters wird in einem Inhaltssteuerelement angezeigt, das seinen Inhalt aus dem ContentPlaceHolder-Steuerelement des übergeordneten Elements abruft.

> [!NOTE]
> Designerunterstützung ist für verschachtelte Masterseiten nicht verfügbar. Wenn Sie mit verschachtelten Mastern entwickeln, müssen Sie die Quellansicht verwenden.

Dieses Video zeigt eine exemplarische Vorgehensweise bei der Verwendung verschachtelter Masterseiten.

![](master-pages/_static/image1.png)

[Öffnen sie Ein-Bild-Video](master-pages/_static/nested1.wmv)

![Auswählen einer Masterseite](master-pages/_static/image4.jpg)

**Abbildung 8:** Auswählen einer Masterseite
