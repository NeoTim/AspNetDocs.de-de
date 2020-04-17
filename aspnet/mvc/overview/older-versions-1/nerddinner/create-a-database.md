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
# <a name="create-a-database"></a><span data-ttu-id="f90fe-103">Erstellen einer Datenbank</span><span class="sxs-lookup"><span data-stu-id="f90fe-103">Create a Database</span></span>

<span data-ttu-id="f90fe-104">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f90fe-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f90fe-105">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="f90fe-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f90fe-106">Dies ist Schritt 2 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.</span><span class="sxs-lookup"><span data-stu-id="f90fe-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f90fe-107">Schritt 2 zeigt die Schritte zum Erstellen der Datenbank mit allen Dinner- und RSVP-Daten für unsere NerdDinner-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="f90fe-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="f90fe-108">Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="f90fe-109">NerdDinner Schritt 2: Erstellen der Datenbank</span><span class="sxs-lookup"><span data-stu-id="f90fe-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="f90fe-110">Wir verwenden eine Datenbank, um alle Dinner- und RSVP-Daten für unsere NerdDinner-Anwendung zu speichern.</span><span class="sxs-lookup"><span data-stu-id="f90fe-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="f90fe-111">Die folgenden Schritte zeigen das Erstellen der Datenbank mit der kostenlosen SQL Server Express-Edition (die Sie einfach mit V2 des [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)installieren können).</span><span class="sxs-lookup"><span data-stu-id="f90fe-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="f90fe-112">Der gesamte Code, den wir schreiben, funktioniert sowohl mit SQL Server Express als auch mit dem vollständigen SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f90fe-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="f90fe-113">Erstellen einer neuen SQL Server Express-Datenbank</span><span class="sxs-lookup"><span data-stu-id="f90fe-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="f90fe-114">Wir beginnen mit einem Rechtsklick auf unser Webprojekt und wählen dann den Menübefehl **&gt;"Neues Element hinzufügen":**</span><span class="sxs-lookup"><span data-stu-id="f90fe-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="f90fe-115">Dadurch wird das Dialogfeld "Neues Element hinzufügen" von Visual Studio angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f90fe-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="f90fe-116">Wir filtern nach der Kategorie "Daten" und wählen die Elementvorlage "SQL Server-Datenbank" aus:</span><span class="sxs-lookup"><span data-stu-id="f90fe-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="f90fe-117">Wir nennen die SQL Server Express-Datenbank, die wir erstellen möchten, "NerdDinner.mdf" und klicken Sie auf OK.</span><span class="sxs-lookup"><span data-stu-id="f90fe-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="f90fe-118">Visual Studio fragt uns dann, ob wir diese\_Datei zu unserem Verzeichnis "App Data" hinzufügen möchten (ein Verzeichnis, das bereits mit Lese- und Schreibsicherheits-ACLs eingerichtet ist):</span><span class="sxs-lookup"><span data-stu-id="f90fe-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="f90fe-119">Wir klicken auf "Ja" und unsere neue Datenbank wird erstellt und unserem Projektmappen-Explorer hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="f90fe-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="f90fe-120">Erstellen von Tabellen in unserer Datenbank</span><span class="sxs-lookup"><span data-stu-id="f90fe-120">Creating Tables within our Database</span></span>

<span data-ttu-id="f90fe-121">Wir haben jetzt eine neue leere Datenbank.</span><span class="sxs-lookup"><span data-stu-id="f90fe-121">We now have a new empty database.</span></span> <span data-ttu-id="f90fe-122">Fügen wir ihm einige Tabellen hinzu.</span><span class="sxs-lookup"><span data-stu-id="f90fe-122">Let's add some tables to it.</span></span>

<span data-ttu-id="f90fe-123">Dazu navigieren wir zum Registerkartenfenster "Server Explorer" in Visual Studio, das es uns ermöglicht, Datenbanken und Server zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="f90fe-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="f90fe-124">SQL Server Express-Datenbanken, die\_im Ordner "App-Daten" unserer Anwendung gespeichert sind, werden automatisch im Server-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f90fe-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="f90fe-125">Optional können wir das Symbol "Mit Datenbank verbinden" oben im Fenster "Server Explorer" verwenden, um der Liste weitere SQL Server-Datenbanken (sowohl lokale als auch Remote-</span><span class="sxs-lookup"><span data-stu-id="f90fe-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="f90fe-126">Wir fügen zwei Tabellen zu unserer NerdDinner-Datenbank hinzu – eine zum Speichern unserer Dinners und die andere, um RSVP-Akzeptanzen zu verfolgen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="f90fe-127">Wir können neue Tabellen erstellen, indem wir mit der rechten Maustaste auf den Ordner "Tabellen" in unserer Datenbank klicken und den Menübefehl "Neue Tabelle hinzufügen" auswählen:</span><span class="sxs-lookup"><span data-stu-id="f90fe-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="f90fe-128">Dadurch wird ein Tabellen-Designer geöffnet, mit dem wir das Schema unserer Tabelle konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="f90fe-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="f90fe-129">Für unsere Tabelle "Dinners" fügen wir 10 Datenspalten hinzu:</span><span class="sxs-lookup"><span data-stu-id="f90fe-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="f90fe-130">Wir möchten, dass die Spalte "DinnerID" ein eindeutiger Primärschlüssel für die Tabelle ist.</span><span class="sxs-lookup"><span data-stu-id="f90fe-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="f90fe-131">Wir können dies konfigurieren, indem wir mit der rechten Maustaste auf die Spalte "DinnerID" klicken und den Menüpunkt "Primärschlüssel festlegen" auswählen:</span><span class="sxs-lookup"><span data-stu-id="f90fe-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="f90fe-132">Zusätzlich zu dinnerID zu einem Primärschlüssel möchten wir es auch als "Identitätsspalte" konfigurieren, deren Wert automatisch erhöht wird, wenn neue Datenzeilen zur Tabelle hinzugefügt werden (d. h. die erste eingefügte Dinner-Zeile hat eine DinnerID von 1, die zweite eingefügte Zeile hat eine DinnerID von 2 usw.).</span><span class="sxs-lookup"><span data-stu-id="f90fe-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="f90fe-133">Wir können dies tun, indem wir die Spalte "DinnerID" auswählen und dann den Editor "Spalteneigenschaften" verwenden, um die Eigenschaft "(Is Identity)" in der Spalte auf "Ja" festzulegen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="f90fe-134">Wir verwenden die Standard-Identitätsstandards (beginnen Sie bei 1 und in Schritten 1 für jede neue Dinner-Zeile):</span><span class="sxs-lookup"><span data-stu-id="f90fe-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="f90fe-135">Wir speichern dann unsere Tabelle, indem wir Strg-S eingeben oder den Menübefehl **Datei speichern&gt;** verwenden.</span><span class="sxs-lookup"><span data-stu-id="f90fe-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="f90fe-136">Dies wird uns veranlassen, die Tabelle zu benennen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-136">This will prompt us to name the table.</span></span> <span data-ttu-id="f90fe-137">Wir nennen es "Dinners":</span><span class="sxs-lookup"><span data-stu-id="f90fe-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="f90fe-138">Unsere neue Dinners-Tabelle wird dann in unserer Datenbank im Server-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f90fe-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="f90fe-139">Wir wiederholen dann die obigen Schritte und erstellen eine "RSVP"-Tabelle.</span><span class="sxs-lookup"><span data-stu-id="f90fe-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="f90fe-140">Diese Tabelle mit 3 Spalten.</span><span class="sxs-lookup"><span data-stu-id="f90fe-140">This table with have 3 columns.</span></span> <span data-ttu-id="f90fe-141">Wir richten die RsvpID-Spalte als Primärschlüssel ein und machen sie zu einer Identitätsspalte:</span><span class="sxs-lookup"><span data-stu-id="f90fe-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="f90fe-142">Wir speichern es und geben ihm den Namen "RSVP".</span><span class="sxs-lookup"><span data-stu-id="f90fe-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="f90fe-143">Einrichten einer Fremdschlüsselbeziehung zwischen Tabellen</span><span class="sxs-lookup"><span data-stu-id="f90fe-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="f90fe-144">Wir haben jetzt zwei Tabellen in unserer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="f90fe-144">We now have two tables within our database.</span></span> <span data-ttu-id="f90fe-145">Unser letzter Schemaentwurfsschritt besteht darin, eine 1:n-Beziehung zwischen diesen beiden Tabellen einzurichten – so dass wir jede Dinner-Zeile mit null oder mehr RSVP-Zeilen verknüpfen können, die für sie gelten.</span><span class="sxs-lookup"><span data-stu-id="f90fe-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="f90fe-146">Wir werden dies tun, indem wir die Spalte "DinnerID" der RSVP-Tabelle so konfigurieren, dass sie eine Fremdschlüsselbeziehung zur Spalte "DinnerID" in der Tabelle "Dinners" hat.</span><span class="sxs-lookup"><span data-stu-id="f90fe-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="f90fe-147">Dazu öffnen wir die RSVP-Tabelle im Tabellen-Designer, indem wir im Server-Explorer darauf doppelklicken.</span><span class="sxs-lookup"><span data-stu-id="f90fe-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="f90fe-148">Wir wählen dann die Spalte "DinnerID" darin aus, klicken mit der rechten Maustaste, und wählen sie die "Beziehungen..." Kontextmenü-Befehl:</span><span class="sxs-lookup"><span data-stu-id="f90fe-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="f90fe-149">Dadurch wird ein Dialogfeld angezeigt, mit dem wir Beziehungen zwischen Tabellen einrichten können:</span><span class="sxs-lookup"><span data-stu-id="f90fe-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="f90fe-150">Wir klicken auf die Schaltfläche "Hinzufügen", um dem Dialogeine eine neue Beziehung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="f90fe-151">Nachdem eine Beziehung hinzugefügt wurde, erweitern wir den Baumansichtsknoten "Tabellen und Spaltenspezifikation" innerhalb des Eigenschaftenrasters rechts neben dem Dialogfeld, und klicken dann auf "..." Aufknopf rechts davon:</span><span class="sxs-lookup"><span data-stu-id="f90fe-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="f90fe-152">Klicken Sie auf die "..." button wird ein weiteres Dialogfeld aufführen, mit dem wir angeben können, welche Tabellen und Spalten an der Beziehung beteiligt sind, und die Beziehung benennen können.</span><span class="sxs-lookup"><span data-stu-id="f90fe-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="f90fe-153">Wir ändern die Primärschlüsseltabelle in "Dinners" und wählen die Spalte "DinnerID" in der Tabelle Abendessen als Primärschlüssel aus.</span><span class="sxs-lookup"><span data-stu-id="f90fe-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="f90fe-154">Unsere RSVP-Tabelle wird die Fremdschlüsseltabelle und die RSVP sein. Die Spalte DinnerID wird als Fremdschlüssel zugeordnet:</span><span class="sxs-lookup"><span data-stu-id="f90fe-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="f90fe-155">Nun wird jede Zeile in der RSVP-Tabelle einer Zeile in der Dinner-Tabelle zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="f90fe-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="f90fe-156">SQL Server behält die referenzielle Integrität für uns bei – und verhindert, dass wir eine neue RSVP-Zeile hinzufügen, wenn sie nicht auf eine gültige Dinner-Zeile hinweist.</span><span class="sxs-lookup"><span data-stu-id="f90fe-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="f90fe-157">Es wird uns auch daran hindern, eine Dinner-Zeile zu löschen, wenn es noch RSVP-Zeilen gibt, die darauf verweisen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="f90fe-158">Hinzufügen von Daten zu unseren Tabellen</span><span class="sxs-lookup"><span data-stu-id="f90fe-158">Adding Data to our Tables</span></span>

<span data-ttu-id="f90fe-159">Lassen Sie uns mit einigen Beispieldaten zu unserer Dinner-Tabelle schließen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="f90fe-160">Wir können einer Tabelle Daten hinzufügen, indem wir im Server-Explorer mit der rechten Maustaste darauf klicken und den Befehl "Tabellendaten anzeigen" auswählen:</span><span class="sxs-lookup"><span data-stu-id="f90fe-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="f90fe-161">Wir fügen einige Zeilen mit Dinner-Daten hinzu, die wir später verwenden können, wenn wir mit der Implementierung der Anwendung beginnen:</span><span class="sxs-lookup"><span data-stu-id="f90fe-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="f90fe-162">Nächster Schritt</span><span class="sxs-lookup"><span data-stu-id="f90fe-162">Next Step</span></span>

<span data-ttu-id="f90fe-163">Wir haben die Erstellung unserer Datenbank abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="f90fe-163">We've finished creating our database.</span></span> <span data-ttu-id="f90fe-164">Erstellen wir nun Modellklassen, die wir zum Abfragen und Aktualisieren verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f90fe-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f90fe-165">[Zurück](create-a-new-aspnet-mvc-project.md)
> [Weiter](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="f90fe-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
