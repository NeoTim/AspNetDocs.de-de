---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET Datenzugriff - Empfohlene Ressourcen | Microsoft Docs
author: rick-anderson
description: Dieses Thema enthält Links zu Dokumentationsressourcen zum Zugriff auf Daten in ASP.NET Webanwendungen, hauptsächlich mithilfe von Entity Framework und SQL Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675784"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET: Datenzugriff – Empfohlene Ressourcen

> Dieses Thema enthält Links zu Dokumentationsressourcen zum Zugriff auf Daten in ASP.NET Webanwendungen, hauptsächlich mithilfe von Entity Framework und SQL Server.
> 
> Wenn Sie einen großartigen Blogbeitrag, [Stackoverflow-Thread](http://stackoverflow.com) oder einen anderen Link kennen, der nützlich wäre, [senden Sie uns eine E-Mail](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) mit dem Link.
> 
> Zuletzt aktualisiert am 03.04.2014

Dieses Thema enthält folgende Abschnitte:

- [Erste Schritte mit dem Datenzugriff in ASP.NET](#gettingstarted)
- [Verwenden des Entity Frameworks](#ef)

    - [Verwenden von Entity Framework Code First](#cf)
    - [Verwenden von Entity Framework Code First Migrationen](#efcfmigrations)
    - [Verwenden von Entity Framework Database First oder Model First (EF-Designer)](#efdbf)
    - [Laden verwandter Daten in Entity Framework (Lazy Loading, Eager Loading und Explicit Loading)](#efrelateddata)
    - [Optimieren der Entity Framework-Performance](#optimizingef)
    - [Verarbeiten von Parallelität in einer Entity Framework-Anwendung](#efconcurrency)
    - [Bücher über das Entity Framework](#efbooks)
    - [Zusätzliche Entity Framework-Ressourcen](#otherefresources)
- [Datenbindung in ASP.NET Web Forms-Anwendungen](#wfdatabinding)

    - [Verwenden der Web formularmodellbindung](#wfmodelbinding)
    - [Verwenden von Web Forms-Datenquellensteuerelementen](#wfdsc)
    - [Verwenden von Web Forms Data Bound Controls und Data Binding Expressions](#wfdbc)
- [Arbeiten mit SQL Server-Datenbanken](#sqlserver)

    - [Arbeiten mit SQL Server Express LocalDB-Datenbanken](#sslocaldb)
    - [Arbeiten mit SQL Server Express-Datenbanken](#sse)
    - [Arbeiten mit Windows Azure SQL-Datenbank](#ssdb)
    - [Auswählen zwischen SQL Server und Windows Azure SQL-Datenbank](#ssdbchoosing)
- [Arbeiten mit NoSQL-Datenbankverwaltungssystemen](#nosql)
- [Verwenden von LINQ-Abfragen in ASP.NET Anwendungen](#linq)
- [Verwenden von Dynamic Data-Gerüsten](#dd)
- [Sichern des Datenzugriffs](#securing)
- [Optimieren der Datenzugriffsleistung](#optimizingdataaccess)
- [Bereitstellen einer Datenbank](#deploying)
- [Zugreifen auf Daten über einen Webdienst](#webservice)
- [Weitere Ressourcen](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>Erste Schritte mit dem Datenzugriff in ASP.NET

- [Datenspeicheroptionen (Erstellen von Echtzeit-Cloud-Apps mit Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). Kapitel eines E-Books über die Entwicklung für die Cloud. Stellt NoSQL-Datenbanken als Alternative vor, die viele Entwickler, die mit relationalen Datenbanken vertraut sind, tendenziell übersehen. Enthält Richtlinien, was Sie beachten müssen, wenn Sie relational oder NoSQL oder eine bestimmte Plattform auswählen.
- [ASP.NET Datenzugriffsoptionen](https://msdn.microsoft.com/library/ms178359.aspx) (MSDN). Eine Einführung in Datenzugriffsoptionen für relationale Datenbanken zum ASP.NET und Anleitungen zur Auswahl von Plattformen und Zugriffsmethoden, die für Ihr Szenario geeignet sind.
- [Relationale Datenbank](http://en.wikipedia.org/wiki/Relational_database). Wikipedia). Wenn Sie nicht mit relationalen Datenbanken gearbeitet haben, finden Sie auf dieser Seite eine Einführung in relationale Datenbankterminologie und -konzepte. Eine Einführung in SQL Server finden Sie unter [Arbeiten mit SQL Server-Datenbanken](#sqlserver) weiter unten in diesem Thema.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Verwenden des Entity Frameworks

- [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN). Anleitung zur Auswahl eines Entity Framework-Entwicklungsansatzes Database First, Model First oder Code First.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Verwenden von Entity Framework Code First

Die folgenden Tutorials bieten herunterladbare Beispielanwendungen:

- [Erste Schritte mit EF 6 mit MVC 5](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Umfasst eine Breite von Entity Framework Code First-Szenarien, einschließlich Migrations- und EF 6-Features wie Verbindungsresilienz, Befehlsabfangen und Asynchronisieren. Dies ist eine aktualisierte Version der [EF 5 / MVC 4 Serie](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Die frühere Serie enthält ein Tutorial zum Repository und Arbeitseinheitsmuster, das nicht in der neuen Serie enthalten ist.
- [Einführung in ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md). Umfasst eine engere Palette von Entity Framework Code First-Szenarien, führt jedoch eine umfassendere Aufgabe durch die Einführung von MVC-Features durch.
- [Modellbindung und Webformulare](https://go.microsoft.com/fwlink/?LinkId=286117). Verwendet Code First in einer Web Forms-Anwendung.
- [Erste Schritte mit ASP.NET 4.5 Web Forms](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Eine Einführung in Webformulare mit einer gewissen Abdeckung von Code First. Verwendet die Modellbindung.
- [MVC Music Store](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). Verwendet Code First in einer E-Commerce MVC 3-Anwendung, die auch Mitgliedschaft und Autorisierung implementiert. Die hier verwendete MVC-Version und ASP.NET-Mitgliedschaftssystem (Authentifizierung und Autorisierung) sind veraltet. weitere aktuelle Informationen zu ASP.NET Mitgliedschaft finden [https://asp.net/identity](https://asp.net/identity)Sie unter .

Weitere Ressourcen:

- [Entity Framework - Code First to a Existing Database](https://msdn.microsoft.com/data/jj200620). Msdn. Video und exemplarische Vorgehensweise, die zeigt, wie Code First mit einer vorhandenen Datenbank verwendet wird.
- [Data Developer Center - Entity Framework](https://msdn.microsoft.com/data/ef). Msdn. Ein Leitfaden zur Entity Framework-Dokumentation, das vom Entity Framework-Team erstellt und verwaltet wurde, finden Sie unter Den Link [Erste](https://msdn.microsoft.com/data/ee712907) Schritte.

Siehe auch [Bücher über entity Framework](#efbooks) und Additional Entity Framework [Resources](#otherefresources) weiter unten in diesem Thema.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Verwenden von Entity Framework Code First Migrationen

Die meisten der oben aufgeführten Code First-Tutorials behandeln Migrationen. Siehe auch die folgenden Ressourcen.

- [ASP.NET-Webbereitstellung mithilfe von Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)Dabei handelt es sich um eine Lernprogrammserie mit zwölf Teilen, in der die Bereitstellungsaufgaben vollständig vorgestellt werden. 2-teilige Tutorial-Serie, die zeigt, wie Code First Migrationen zum Bereitstellen einer Datenbank verwendet wird.
- [Stellen Sie eine Secure ASP.NET MVC 5-App mit Mitgliedschaft, OAuth und SQL-Datenbank auf einer Windows Azure-Website](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bereit. Microsoft Azure). Verwenden von Migrationen zum Bereitstellen von Mitgliedschafts- und Anwendungsdaten in Azure.
- [Übersicht über die Webbereitstellung für Visual Studio und ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). Im Abschnitt Konfigurieren der **Datenbankbereitstellung in Visual Studio** finden Sie eine Erläuterung zur Integration von Code First-Migrationen in Visual Studio-Webbereitstellungsfeatures.
- [Data Developer Center - Code First Migrations](https://msdn.microsoft.com/data/jj591621) (MSDN). Die Migrationsdokumentation des Entity Framework-Teams.
- [Migrations Screencast-Serie](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF-Blog). Drei Videos zu fortgeschrittenen Themen in Code First Migrationen.
- [Code First Migrations With ASP.NET Web Pages Sites](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). Mikesdotnetting-Blog). Zeigt, wie Code First-Migrationen mit einer ASP.NET-Website verwendet werden, indem der Datenkontext in einem Visual Studio-Klassenbibliotheksprojekt abgelegt wird.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Verwenden von Entity Framework Database First oder Model First (EF-Designer)

- [Erste Schritte mit Entity Framework 6 Database First mit MVC 5](../mvc/overview/getting-started/database-first-development/setting-up-database.md). Führen Sie ein Skript im Server-Explorer aus, um eine Datenbank zu erstellen, und verwenden Sie dann den Entity Framework-Designer, um das Datenmodell zu erstellen. Zeigt, wie sie einfache CRUD-Webseiten erstellen, und für andere Datenverarbeitungsfunktionen können Sie einem der Code First-Tutorials folgen, da alle EF-Workflows dieselbe DbContext-API verwenden.

Die folgenden Ressourcen sind älter. Sie sind nützlich, wenn Sie Version 4.0 des Entity Frameworks und ein Datenquellensteuerelement für die Datenbindung in einer Web Forms-Anwendung verwenden möchten.

- [Erste Schritte mit entity Framework 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). Zeigt, wie das **EntityDataSource-Steuerelement** verwendet wird.
- [Fortsetzung mit dem Entity Framework](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(Zeigt, wie das **ObjectDataSource-Steuerelement** verwendet wird. Enthält ein Tutorial zur Behandlung von Parallelität, ein Tutorial zur EF-Leistung und ein Tutorial zu den Neuerungen in EF 4.0.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Umgang mit verknüpften Daten in Entity Framework (Lazy Loading, Eager Loading und Explicit Loading)

- [Lesen verwandter Daten mit dem Entity Framework in einer ASP.NET MVC-Anwendung](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, MVC-Beispielanwendung. Die angezeigten Methoden gelten auch für die Web Forms-Modellbindung und den Database First-Workflow.
- [Data Developer Center - Laden verwandter Entitäten](https://msdn.microsoft.com/data/jj574232) (MSDN). Die Dokumentation des Entity Framework-Teams zum Laden verwandter Daten.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Optimieren der Entity Framework-Leistung

- [Erweiterte Entity Framework-Szenarien für eine ASP.NET Anwendung](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md). Zeigt, wie Sie eigene SQL-Anweisungen ausführen oder Ihre eigenen gespeicherten Prozeduren aufrufen, wie Sie die Änderungserkennung deaktivieren und wie Sie die Validierung beim Speichern von Änderungen deaktivieren.
- [Leistungsaspekte für Entity Framework 5](https://msdn.microsoft.com/data/hh949853) (MSDN).
- [Leistungserwägungen (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN).
- [Maximierung der Leistung mit dem Entity Framework in einer ASP.NET Webanwendung](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md). Gilt für Entity Framework 4.0.
- Siehe auch [Optimierung ASP.NET Datenzugriffs](#optimizingdataaccess) weiter unten in diesem Thema.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Verarbeiten von Parallelität in einer Entity Framework-Anwendung

- [Verarbeiten von Parallelität mit dem Entity Framework in einer ASP.NET MVC-Anwendung](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First, DbContext-API, mit einer MVC-Beispielanwendung.
- [Data Developer Center – Optimistische Parallelitätsmuster](https://msdn.microsoft.com/data/jj592904) (MSDN). Die Parallelitätsdokumentation des Entity Framework-Teams.
- [Verarbeiten von Parallelität mit entity Framework in einer ASP.NET Webanwendung](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Gilt für Entity Framework 4.0. Database First, ObjectContext-API, mit einer Web Forms-Beispielanwendung.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Bücher über das Entity Framework

- [Programming Entity Framework: DbContext](http://shop.oreilly.com/product/0636920022237.do) von Julie Lerman und Rowan Miller.
- [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) von Julie Lerman und Rowan Miller.

Beide Bücher sind mit den aktuellen empfohlenen Techniken auf dem neuesten Stand. Sie bieten eine umfassendere und dennoch leicht verständliche Einführung in das Entity Framework als alles, was im Internet verfügbar ist. Ein weiteres Buch, [Programming Entity Framework](http://shop.oreilly.com/product/9780596807252.do) von Julie Lerman, ist größer und umfassender, aber es ist älter und viele der Techniken, die es abdeckt, sind nicht mehr die empfohlene Methode, um das Entity Framework zu verwenden. Siehe auch die Liste der Vom Entity Framework-Team im [Data Developer Center - Books](https://msdn.microsoft.com/data/aa937716) auf der MSDN-Website empfohlenen Bücher.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>Andere Entity Framework-Ressourcen

- [Entity Framework (ADO.NET) Teamblog](https://blogs.msdn.com/b/adonet/). Eine der besten Ressourcen für die aktuellsten Informationen und Ankündigungen neuer Verbesserungen. Weitere EF-bezogene Blogs finden Sie im Blogroll unter [Erste Schritte mit Entity Framework](https://msdn.microsoft.com/data/ee712907).
- [MSDN Magazin](https://msdn.microsoft.com/magazine/default.aspx). Weitere Informationen finden Sie in der Spalte **Datenpunkte,** in der es häufig um Themen im Zusammenhang mit dem Entity Framework geht.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>Datenbindung in ASP.NET Web Forms-Anwendungen

- [ASP.NET Web Forms Data Access](https://msdn.microsoft.com/library/jj822927.aspx) Options<a id="wfmodelbinding"></a>(MSDN) .

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Verwenden der Web formularmodellbindung

- [Modellbindung und Webformulare](https://go.microsoft.com/fwlink/?LinkId=286117). Tutorial-Serie mit EF Code First.
- [Web Forms Model Binding Teil 1: Auswählen von Daten](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthries Blog). In diesen älteren Blogbeiträgen wurde die Eigenschaft, die derzeit ItemType heißt, ModelType genannt, ansonsten sind die darin enthaltenen Informationen jedoch gültig.
- [Web Forms Model Binding Part 2: Filtern von Daten](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthries Blog).
- [Web Forms Model Binding Part 3: Updating and Validation](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthries Blog).
- [ASP.NET 4.5 Web Forms Model Binding](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (Video).
- [Modellbindung Teil 1 - Auswählen von Daten](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (Video).
- [Modellbindung Teil 2 - Filtern](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (Video).
- [Erste Schritte mit ASP.NET 4.5 Web Forms - Datenelemente und Details anzeigen](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Verwenden von Web Forms-Datenquellensteuerelementen

- [Data Source Web Server Controls](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN).
- [Ankündigung der Veröffentlichung von Dynamic Data Provider und EntityDataSource-Steuerelement für Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx) (Microsoft Web Development Blog).

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Verwenden von Web Forms Data Bound Controls und Data Binding Expressions

- [Modellbindung und Webformulare](https://go.microsoft.com/fwlink/?LinkId=286117). Tutorial-Serie, die EF Code First verwendet.
- [Erste Schritte mit ASP.NET 4.5 Web Forms - Datenelemente und Details anzeigen](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md).
- [Stark typisierte Datensteuerungen](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthries Blog).
- [Stark typisierte Datensteuerungen](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (Video).
- [ASP.NET 4.5 Web Forms Strong Typed Data Controls](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (Video).
- [Data-Bound Web Server Controls](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN).
- [Datenbindungsausdrücke Übersicht](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). Diese Seite deckt nur **Eval** und **Bind**ab; Sie wurde nicht aktualisiert, um **Item** und **BindItem**einzuschließen.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>Arbeiten mit SQL Server-Datenbanken

- [SQL Server-Datenbankfeatures](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN). Eine allgemeine Einführung in eine Vielzahl von SQL Server-Themen finden Sie in den Einträgen unter diesem im ToC.
- [SQL Server Editions](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). Eine Zusammenfassung der verfügbaren SQL Server-Editionen mit Links zu weiteren Informationen zu jedem.)
- [SQL Server-Verbindungszeichenfolgen für ASP.NET Webanwendungen](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Verwenden von SQL Server Compact für ASP.NET Webanwendungen](https://msdn.microsoft.com/library/ms247257.aspx) (MSDN).
- [Microsoft SQL Server: Datenbankproduktbeispiele](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Beispiel adventureWorks-Datenbanken.
- [Installieren von Beispieldatenbanken](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). Zusätzlich zu den hier gezeigten Methoden können Sie auch eine der\_Beispiel-Mdf-Dateien in den App-Datenordner eines Webprojekts herunterladen, die Datenbank in LocalDB konvertieren und eine LocalDB-Verbindungszeichenfolge erstellen. Informationen dazu finden Sie unter [Gewusst wie: Upgrade auf LocalDB](https://msdn.microsoft.com/library/hh873188.aspx).

Siehe auch die folgenden Abschnitte zum Arbeiten mit SQL Server Express und LocalDB sowie zur Auswahl zwischen SQL Server und SQL-Datenbank.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>Arbeiten mit SQL Server Express LocalDB-Datenbanken

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). Die offizielle MSDN-Einführung in LocalDB.
- [SQL Server-Verbindungszeichenfolgen für ASP.NET Webanwendungen](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN).
- [Gewusst wie: Upgrade auf LocalDB](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN). Migrieren einer Mdf-Datei aus einer früheren Version von SQL Server Express in LocalDB. Sie müssen diesen Vorgang auch durchlaufen, wenn Sie eine der [SQL Server 2012-Beispieldatenbanken](https://go.microsoft.com/fwlink/?linkid=117483)herunterladen.
- [Einführung in LocalDB, einen verbesserten SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express-Blog). Hat mehr Hintergrundinformationen darüber, warum LocalDB erstellt wurde, als in MSDN enthalten ist.
- [LocalDB: Wo ist Meine Datenbank?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express-Blog). Informationen darüber, wo LocalDB-Datenbankdateien erstellt werden.
- [Verwenden von LocalDB mit Full IIS, Part 1: User Profile](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express-Blog). LocalDB ist nicht für die Arbeit mit IIS konzipiert. Diese Reihe von Blogbeiträgen erklärt die Probleme und einige Problemumgehungen.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>Arbeiten mit SQL Server Express-Datenbanken

- [SQL Server-Verbindungszeichenfolgen für ASP.NET Webanwendungen](https://msdn.microsoft.com/library/jj653752.aspx) (MSDN). Wenn Sie die Verbindungszeichenfolgeneinstellung AttachDBFileName mit SQL Server Express verwenden, lesen Sie insbesondere den Abschnitt Benutzerinstanzen auf dieser Seite.
- So übernehmen Sie den [Besitz Ihres lokalen SQL Server Express 2008](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) (SQL Server Express-Blog). Ein häufiges Problem besteht darin, dass Sie nicht mit SQL Server Express-Datenbanken arbeiten können, da Sie kein Administrator auf der SQL Server Express-Instanz sind. Standardmäßig ist nur die Person, die SQL Server Express installiert hat, ein Administrator. In diesem Blog wird erläutert, wie Sie sich als SQL Server Express-Administrator ausbilden, wenn Sie Administrator auf dem Computer sind.
- [Kann meine ASP.NET Webanwendung eine SQL Server Express-Datenbank in der Produktion verwenden?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Arbeiten mit Windows Azure SQL-Datenbank

- [Stellen Sie eine Secure ASP.NET MVC-App mit Mitgliedschaft, OAuth und SQL-Datenbank auf einer Windows Azure-Website](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure-Website) bereit.
- [SQL-Datenbanken](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure-Site). Erste Schritte Tutorials und Anleitungen.
- [Windows Azure SQL-Datenbank](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). Der Knoten der obersten Ebene des Inhaltsverzeichnisses für SQL-Datenbank in MSDN.
- [Windows Azure SQL Database TechNet Wiki Articles Index](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft TechNet-Website).
- [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). Ein Framework, mit dem Sie vorübergehende Netzwerkfehler und Verbindungsfehler behandeln können, die sich aus der Drosselung ergeben. Verfügbar in einem NuGet-Paket: [Enterprise Library 5.0 - Transient Fault Handling Application Block](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [Erste Schritte mit SQL Database and Entity Framework](https://msdn.microsoft.com/data/jj556244) (MSDN).
- [Windows Azure Training Kit](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft Download Center). Enthält praktische Übungseinheiten für SQL-Datenbank.
- [Windows Azure SQL-Datenbank-Community-Forum](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Wechseln zu Windows Azure SQL-Datenbank](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN). Ein Kapitel eines umfassenden End-to-End-Szenarios des Microsoft Patterns and Practices-Teams. Erläutert, warum Sie migrieren und wie Sie von SQL Server zu SQL Database migrieren.
- [Migrieren von SQL Server-Datenbanken zu Windows Azure SQL-Datenbank](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).
- [SQL-Datenbank-Migrations-Assistent](http://sqlazuremw.codeplex.com/). Ein Open-Source-Tool zum Migrieren von Datenbanken zu und von SQL-Datenbank.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>Auswählen zwischen SQL Server und Windows Azure SQL-Datenbank

- [Vergleichen Sie SQL Server mit der Windows Azure SQL-Datenbank](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet-Website).
- [Datenmigration zu Windows Azure SQL-Datenbank: Tools and Techniques](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN). Enthält Abschnitte, die SQL Server mit SQL-Datenbank vergleichen und Anleitungen zum Migrieren von SQL Server zu SQL Datenbank bereitstellen.
- [Windows Azure SQL-Datenbankbereitstellungshandbuch](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet-Website).
- [SQL Server-Funktionseinschränkungen (Windows Azure SQL-Datenbank)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN).
- [Windows Azure Table Storage und Windows Azure SQL-Datenbank – Verglichen und kontrastiert](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN). Für eine Anwendung, die Sie in Windows Azure bereitstellen, kann Windows Azure Table Storage eine Alternative zu Windows Azure SQL-Datenbank sein. In diesem Thema können Sie zwischen diesen Alternativen entscheiden.
- [Windows Azure SQL-Datenbank](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [Richtlinien und Einschränkungen (Windows Azure SQL-Datenbank)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>Arbeiten mit NoSQL-Datenbankverwaltungssystemen

- [Windows Azure Data Services](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure-Website). Weitere Informationen finden Sie im [Tabellendienst-Feature-Handbuch](https://docs.microsoft.com/azure/) und im **Abschnitt Big Data** auf der Seite.
- [ASP.NET Anwendung mit mehreren Ebenen mithilfe von Speichertabellen, Warteschlangen und Blobs](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure-Website). End-to-End-Tutorial mit herunterladbarer Beispielanwendung, die Windows Azure-SpeichernoSQL-Tabellen verwendet.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>Verwenden von LINQ-Abfragen in ASP.NET Anwendungen

- [ASP.NET Datenzugriffsoptionen](https://msdn.microsoft.com/library/ms178359.aspx#linq) (MSDN). Enthält eine Einführung in LINQ.
- [LINQ Trainingsvideos](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagners Blog).
- [ASP.NET Forum-Thread mit Links zu dynamischen LINQ-Ressourcen](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq).

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Verwenden von Dynamic Data Scaffolding

- [Dynamische Datenprojektvorlagen](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN). Anleitung zur Verwendung von Dynamic Data-Projekten.
- [ASP.NET Dynamic Data](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>Sichern des Datenzugriffs

- [Sichern des Datenzugriffs in ASP.NET](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN).
- [Sicherheitsaspekte (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN).
- [Gewusst wie: Sichern von Verbindungszeichenfolgen bei Verwendung von Datenquellensteuerelementen](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN).

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>Optimieren der Datenzugriffsleistung

- [ASP.NET -Leistungsübersicht](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET Caching](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [Verbesserung der ASP.NET-Leistung](https://msdn.microsoft.com/library/ff647787) (MSDN). Oben auf dieser Seite wird eine Warnung "Ruhemit dem Inhalt in Den Ruhestand versetzt" angezeigt, aber die meisten Informationen sind immer noch relevant, und es gibt keine vergleichbare aktualisierte Ressource.
- [Verbesserung der SQL Server-Leistung](https://msdn.microsoft.com/library/ff647793) (MSDN). Derselbe Kommentar wie der vorherige Link.

Siehe auch [optimieren die Entity Framework-Leistung](#optimizingef) weiter oben in diesem Thema.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>Bereitstellen einer Datenbank

- [ASP.NET Webbereitstellung - Empfohlene Ressourcen](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>Zugreifen auf Daten über einen Webdienst

- [Zugriff auf Daten über einen Webdienst (MSDN).](https://msdn.microsoft.com/library/ms178359.aspx#webservice) Anleitung zur Verwendung von Web-API im Vergleich zu WCF.
- [Erste Schritte mit ASP.NET Web-API](../web-api/index.md).
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>Weitere Ressourcen

- [ASP.NET Häufig gestellte Fragen zum Datenzugriff](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET Web Forms Tutorials - Daten](../web-forms/overview/data-access/index.md). Die meisten dieser Tutorials sind relativ alt; Stellen Sie sicher, dass Sie [zuerst ASP.NET Datenzugriffsoptionen](https://msdn.microsoft.com/library/ms178359.aspx) und [Datenspeicheroptionen (Erstellen von Real-World Cloud-Apps mit Windows Azure)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) lesen, damit Sie nicht zu weit in eine Datenzugriffsmethode gelangen, die für Ihr Szenario nicht geeignet ist.
- [ASP.NET MVC-Inhaltszuordnung](../mvc/overview/getting-started/recommended-resources-for-mvc.md).
- [ASP.NET Webseiten Tutorials - Daten](../web-pages/overview/data/index.md).
- [Zugriff auf Daten in Visual Studio](https://msdn.microsoft.com/library/wzabh8c4.aspx) (MSDN). Stellt eine Liste von Links bereit, die dieser Inhaltszuordnung ähneln, jedoch auf Visual Studio und nicht auf ASP.NET.
