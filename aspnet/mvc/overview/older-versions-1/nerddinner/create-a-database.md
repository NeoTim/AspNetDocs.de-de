---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Erstellen einer Datenbank | Microsoft-Dokumentation
author: rick-anderson
description: Schritt 2 zeigt die Schritte zum Erstellen der Datenbank mit allen Dinner- und RSVP-Daten für unsere NerdDinner-Anwendung.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541610"
---
# <a name="create-a-database"></a>Erstellen einer Datenbank

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 2 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 2 zeigt die Schritte zum Erstellen der Datenbank mit allen Dinner- und RSVP-Daten für unsere NerdDinner-Anwendung.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner Schritt 2: Erstellen der Datenbank

Wir verwenden eine Datenbank, um alle Dinner- und RSVP-Daten für unsere NerdDinner-Anwendung zu speichern.

Die folgenden Schritte zeigen das Erstellen der Datenbank mit der kostenlosen SQL Server Express-Edition (die Sie einfach mit V2 des [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)installieren können). Der gesamte Code, den wir schreiben, funktioniert sowohl mit SQL Server Express als auch mit dem vollständigen SQL Server.

### <a name="creating-a-new-sql-server-express-database"></a>Erstellen einer neuen SQL Server Express-Datenbank

Wir beginnen mit einem Rechtsklick auf unser Webprojekt und wählen dann den Menübefehl **&gt;"Neues Element hinzufügen":**

![](create-a-database/_static/image1.png)

Dadurch wird das Dialogfeld "Neues Element hinzufügen" von Visual Studio angezeigt. Wir filtern nach der Kategorie "Daten" und wählen die Elementvorlage "SQL Server-Datenbank" aus:

![](create-a-database/_static/image2.png)

Wir nennen die SQL Server Express-Datenbank, die wir erstellen möchten, "NerdDinner.mdf" und klicken Sie auf OK. Visual Studio fragt uns dann, ob wir diese\_Datei zu unserem Verzeichnis "App Data" hinzufügen möchten (ein Verzeichnis, das bereits mit Lese- und Schreibsicherheits-ACLs eingerichtet ist):

![](create-a-database/_static/image3.png)

Wir klicken auf "Ja" und unsere neue Datenbank wird erstellt und unserem Projektmappen-Explorer hinzugefügt:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Erstellen von Tabellen in unserer Datenbank

Wir haben jetzt eine neue leere Datenbank. Fügen wir ihm einige Tabellen hinzu.

Dazu navigieren wir zum Registerkartenfenster "Server Explorer" in Visual Studio, das es uns ermöglicht, Datenbanken und Server zu verwalten. SQL Server Express-Datenbanken, die\_im Ordner "App-Daten" unserer Anwendung gespeichert sind, werden automatisch im Server-Explorer angezeigt. Optional können wir das Symbol "Mit Datenbank verbinden" oben im Fenster "Server Explorer" verwenden, um der Liste weitere SQL Server-Datenbanken (sowohl lokale als auch Remote-

![](create-a-database/_static/image5.png)

Wir fügen zwei Tabellen zu unserer NerdDinner-Datenbank hinzu – eine zum Speichern unserer Dinners und die andere, um RSVP-Akzeptanzen zu verfolgen. Wir können neue Tabellen erstellen, indem wir mit der rechten Maustaste auf den Ordner "Tabellen" in unserer Datenbank klicken und den Menübefehl "Neue Tabelle hinzufügen" auswählen:

![](create-a-database/_static/image6.png)

Dadurch wird ein Tabellen-Designer geöffnet, mit dem wir das Schema unserer Tabelle konfigurieren können. Für unsere Tabelle "Dinners" fügen wir 10 Datenspalten hinzu:

![](create-a-database/_static/image7.png)

Wir möchten, dass die Spalte "DinnerID" ein eindeutiger Primärschlüssel für die Tabelle ist. Wir können dies konfigurieren, indem wir mit der rechten Maustaste auf die Spalte "DinnerID" klicken und den Menüpunkt "Primärschlüssel festlegen" auswählen:

![](create-a-database/_static/image8.png)

Zusätzlich zu dinnerID zu einem Primärschlüssel möchten wir es auch als "Identitätsspalte" konfigurieren, deren Wert automatisch erhöht wird, wenn neue Datenzeilen zur Tabelle hinzugefügt werden (d. h. die erste eingefügte Dinner-Zeile hat eine DinnerID von 1, die zweite eingefügte Zeile hat eine DinnerID von 2 usw.).

Wir können dies tun, indem wir die Spalte "DinnerID" auswählen und dann den Editor "Spalteneigenschaften" verwenden, um die Eigenschaft "(Is Identity)" in der Spalte auf "Ja" festzulegen. Wir verwenden die Standard-Identitätsstandards (beginnen Sie bei 1 und in Schritten 1 für jede neue Dinner-Zeile):

![](create-a-database/_static/image9.png)

Wir speichern dann unsere Tabelle, indem wir Strg-S eingeben oder den Menübefehl **Datei speichern&gt;** verwenden. Dies wird uns veranlassen, die Tabelle zu benennen. Wir nennen es "Dinners":

![](create-a-database/_static/image10.png)

Unsere neue Dinners-Tabelle wird dann in unserer Datenbank im Server-Explorer angezeigt.

Wir wiederholen dann die obigen Schritte und erstellen eine "RSVP"-Tabelle. Diese Tabelle mit 3 Spalten. Wir richten die RsvpID-Spalte als Primärschlüssel ein und machen sie zu einer Identitätsspalte:

![](create-a-database/_static/image11.png)

Wir speichern es und geben ihm den Namen "RSVP".

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Einrichten einer Fremdschlüsselbeziehung zwischen Tabellen

Wir haben jetzt zwei Tabellen in unserer Datenbank. Unser letzter Schemaentwurfsschritt besteht darin, eine 1:n-Beziehung zwischen diesen beiden Tabellen einzurichten – so dass wir jede Dinner-Zeile mit null oder mehr RSVP-Zeilen verknüpfen können, die für sie gelten. Wir werden dies tun, indem wir die Spalte "DinnerID" der RSVP-Tabelle so konfigurieren, dass sie eine Fremdschlüsselbeziehung zur Spalte "DinnerID" in der Tabelle "Dinners" hat.

Dazu öffnen wir die RSVP-Tabelle im Tabellen-Designer, indem wir im Server-Explorer darauf doppelklicken. Wir wählen dann die Spalte "DinnerID" darin aus, klicken mit der rechten Maustaste, und wählen sie die "Beziehungen..." Kontextmenü-Befehl:

![](create-a-database/_static/image12.png)

Dadurch wird ein Dialogfeld angezeigt, mit dem wir Beziehungen zwischen Tabellen einrichten können:

![](create-a-database/_static/image13.png)

Wir klicken auf die Schaltfläche "Hinzufügen", um dem Dialogeine eine neue Beziehung hinzuzufügen. Nachdem eine Beziehung hinzugefügt wurde, erweitern wir den Baumansichtsknoten "Tabellen und Spaltenspezifikation" innerhalb des Eigenschaftenrasters rechts neben dem Dialogfeld, und klicken dann auf "..." Aufknopf rechts davon:

![](create-a-database/_static/image14.png)

Klicken Sie auf die "..." button wird ein weiteres Dialogfeld aufführen, mit dem wir angeben können, welche Tabellen und Spalten an der Beziehung beteiligt sind, und die Beziehung benennen können.

Wir ändern die Primärschlüsseltabelle in "Dinners" und wählen die Spalte "DinnerID" in der Tabelle Abendessen als Primärschlüssel aus. Unsere RSVP-Tabelle wird die Fremdschlüsseltabelle und die RSVP sein. Die Spalte DinnerID wird als Fremdschlüssel zugeordnet:

![](create-a-database/_static/image15.png)

Nun wird jede Zeile in der RSVP-Tabelle einer Zeile in der Dinner-Tabelle zugeordnet. SQL Server behält die referenzielle Integrität für uns bei – und verhindert, dass wir eine neue RSVP-Zeile hinzufügen, wenn sie nicht auf eine gültige Dinner-Zeile hinweist. Es wird uns auch daran hindern, eine Dinner-Zeile zu löschen, wenn es noch RSVP-Zeilen gibt, die darauf verweisen.

### <a name="adding-data-to-our-tables"></a>Hinzufügen von Daten zu unseren Tabellen

Lassen Sie uns mit einigen Beispieldaten zu unserer Dinner-Tabelle schließen. Wir können einer Tabelle Daten hinzufügen, indem wir im Server-Explorer mit der rechten Maustaste darauf klicken und den Befehl "Tabellendaten anzeigen" auswählen:

![](create-a-database/_static/image16.png)

Wir fügen einige Zeilen mit Dinner-Daten hinzu, die wir später verwenden können, wenn wir mit der Implementierung der Anwendung beginnen:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Nächster Schritt

Wir haben die Erstellung unserer Datenbank abgeschlossen. Erstellen wir nun Modellklassen, die wir zum Abfragen und Aktualisieren verwenden können.

> [!div class="step-by-step"]
> [Zurück](create-a-new-aspnet-mvc-project.md)
> [Weiter](build-a-model-with-business-rule-validations.md)
