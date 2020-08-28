---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: Erstellen des Mitgliedschafts Schemas in SQL Server (c#) | Microsoft-Dokumentation
author: rick-anderson
description: In diesem Tutorial werden die Verfahren zum Hinzufügen des erforderlichen Schemas zur Datenbank erläutert, um den sqlmembership shipprovider zu verwenden. Danach können wir...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 8160c422d7a20b7c6954f960e73d5d59f7b90a5f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044739"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>Erstellen des Mitgliedschaftsschemas in SQL Server (C#)

von [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Code herunterladen](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) oder [PDF herunterladen](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> In diesem Tutorial werden die Verfahren zum Hinzufügen des erforderlichen Schemas zur Datenbank erläutert, um den sqlmembership shipprovider zu verwenden. Danach untersuchen wir die Schlüsseltabellen im Schema und besprechen deren Zweck und Wichtigkeit. In diesem Tutorial wird erläutert, wie einer ASP.NET-Anwendung mitgeteilt wird, welchen Anbieter das Mitgliedschafts Framework verwenden sollte.

## <a name="introduction"></a>Einführung

Die vorherigen beiden Tutorials untersuchten die Verwendung der Formular Authentifizierung, um Website Besucher zu identifizieren. Das Formular Authentifizierungs Framework erleichtert Entwicklern das Anmelden von Benutzern bei einer Website und die Verwendung von Authentifizierungs Tickets über den Seitenbesuch hinweg. Die `FormsAuthentication` -Klasse enthält Methoden zum Erstellen des Tickets und zum Hinzufügen des Tickets zu den Cookies des Besuchers. `FormsAuthenticationModule`Überprüft alle eingehenden Anforderungen und erstellt und für diejenigen mit einem gültigen Authentifizierungs Ticket ein `GenericPrincipal` -Objekt und ein- `FormsIdentity` Objekt mit der aktuellen Anforderung. Bei der Formular Authentifizierung handelt es sich lediglich um einen Mechanismus zum Gewähren eines Authentifizierungs Tickets an einen Besucher bei der Anmeldung und bei nachfolgenden Anforderungen, um das Ticket zu ermitteln und die Identität des Benutzers zu bestimmen. Damit eine Webanwendung Benutzerkonten unterstützt, müssen wir immer noch einen Benutzerspeicher implementieren und Funktionen zum Überprüfen von Anmelde Informationen, Registrieren neuer Benutzer und der unzähligen anderen Benutzerkonto bezogenen Aufgaben hinzufügen.

Vor ASP.NET 2,0 waren Entwickler bei der Implementierung all dieser Aufgaben im Zusammenhang mit dem Benutzerkonto auf dem Hook. Glücklicherweise hat das ASP.net-Team dieses Manko erkannt und das Mitgliedschafts Framework mit ASP.NET 2,0 eingeführt. Das Mitgliedschafts Framework ist eine Reihe von Klassen in den .NET Framework, die eine programmgesteuerte Schnittstelle zum Ausführen von Aufgaben im Zusammenhang mit dem Benutzerkonto bereitstellen. Dieses Framework basiert auf dem [Anbieter Modell](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), das es Entwicklern ermöglicht, eine angepasste Implementierung in eine standardisierte API zu integrieren.

Wie im Lernprogramm zu den <a id="Tutorial1"></a> [*Sicherheitsgrundlagen und ASP.NET-Unterstützung*](../introduction/security-basics-and-asp-net-support-cs.md) erläutert, werden die .NET Framework mit zwei integrierten Mitgliedschafts Anbietern ausgeliefert: [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) und [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) . Wie der Name schon sagt, `SqlMembershipProvider` verwendet eine Microsoft SQL Server Datenbank als Benutzerspeicher. Um diesen Anbieter in einer Anwendung verwenden zu können, müssen wir dem Anbieter mitteilen, welche Datenbank als Speicher verwendet werden soll. Wie Sie sich vorstellen können, `SqlMembershipProvider` erwartet die Benutzerspeicher-Datenbank, dass bestimmte Datenbanktabellen, Sichten und gespeicherte Prozeduren vorhanden sind. Wir müssen dieses erwartete Schema der ausgewählten Datenbank hinzufügen.

In diesem Tutorial werden zunächst Techniken zum Hinzufügen des erforderlichen Schemas zur-Datenbank erläutert, um die zu verwenden `SqlMembershipProvider` . Danach untersuchen wir die Schlüsseltabellen im Schema und besprechen deren Zweck und Wichtigkeit. In diesem Tutorial wird erläutert, wie einer ASP.NET-Anwendung mitgeteilt wird, welchen Anbieter das Mitgliedschafts Framework verwenden sollte.

Legen Sie direkt los.

## <a name="step-1-deciding-where-to-place-the-user-store"></a>Schritt 1: entscheiden, wo der Benutzerspeicher platziert werden soll

Die Daten einer ASP.NET-Anwendung werden häufig in einer Reihe von Tabellen in einer Datenbank gespeichert. Beim Implementieren des `SqlMembershipProvider` Datenbankschemas müssen wir entscheiden, ob das Mitgliedschafts Schema in derselben Datenbank wie die Anwendungsdaten oder in einer alternativen Datenbank platziert werden soll.

Aus den folgenden Gründen wird empfohlen, das Mitgliedschafts Schema in derselben Datenbank wie die Anwendungsdaten zu suchen:

- **Wartbarkeit** "eine Anwendung, deren Daten in einer Datenbank gekapselt sind, ist leichter zu verstehen, zu warten und bereitzustellen, als eine Anwendung, die über zwei separate Datenbanken verfügt.
- **Relationale Integrität** "Durchsuchen der Mitgliedschafts bezogenen Tabellen in derselben Datenbank wie die Anwendungs Tabellen ist es möglich, [Foreign Key-Einschränkungen](http://en.wikipedia.org/wiki/Foreign_key) zwischen den primär Schlüsseln in den Mitgliedschafts bezogenen Tabellen und den zugehörigen Anwendungs Tabellen herzustellen.

Die Entkopplung von Benutzerspeicher-und Anwendungsdaten in separate Datenbanken ist nur sinnvoll, wenn Sie über mehrere Anwendungen verfügen, die jeweils separate Datenbanken verwenden, aber einen gemeinsamen Benutzerspeicher freigeben müssen.

### <a name="creating-a-database"></a>Erstellen einer Datenbank

Die Anwendung, die wir seit dem zweiten Tutorial aufgebaut haben, hat noch keine Datenbank benötigt. Wir benötigen jedoch für den Benutzerspeicher jetzt ein solches. Erstellen Sie einen, und fügen Sie diesem dann das für den Anbieter erforderliche Schema hinzu `SqlMembershipProvider` (siehe Schritt 2).

> [!NOTE]
> In dieser tutorialreihe werden wir eine [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) -Datenbank verwenden, um die Anwendungs Tabellen und das Schema zu speichern `SqlMembershipProvider` . Diese Entscheidung wurde aus zwei Gründen getroffen: Erstens, aufgrund der kostenlosen kostenlosen Express Edition, die die am weitesten lesbar zugängliche Version von SQL Server 2005; Zweitens können SQL Server 2005 Express Edition Datenbanken direkt in den Ordner der Webanwendung eingefügt werden. `App_Data` dadurch wird ein geliefert erstellt, um die Datenbank und die Webanwendung in einer ZIP-Datei zu verpacken und ohne spezielle Installationsanweisungen oder Konfigurationsoptionen erneut bereitzustellen. Wenn Sie lieber eine nicht Express Edition-Version von SQL Server befolgen möchten, können Sie es kostenlos tun. Die Schritte sind praktisch identisch. Das `SqlMembershipProvider` Schema kann mit einer beliebigen Version von Microsoft SQL Server 2000 und höher verwendet werden.

Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den `App_Data` Ordner, und wählen Sie neues Element hinzufügen aus. (Wenn ein `App_Data` Ordner in Ihrem Projekt nicht angezeigt wird, klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, wählen Sie ASP.NET Ordner hinzufügen aus, und wählen Sie aus `App_Data` .) Wählen Sie im Dialogfeld Neues Element hinzufügen eine neue SQL-Datenbank mit dem Namen aus `SecurityTutorials.mdf` . In diesem Tutorial fügen wir das `SqlMembershipProvider` Schema zu dieser Datenbank hinzu. in den nachfolgenden Tutorials werden zusätzliche Tabellen erstellt, um die Anwendungsdaten zu erfassen.

[![Fügen Sie dem App_Data Ordner eine neue SQL-Datenbank mit dem Namen "securitytutorials. mdf" hinzu.](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**Abbildung 1**: Hinzufügen einer neuen SQL-Datenbank `SecurityTutorials.mdf` mit dem Namen "Database" zum `App_Data` Ordner ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image3.png))

Wenn Sie dem Ordner eine Datenbank hinzufügen, wird `App_Data` dieser automatisch in der Ansicht Datenbank-Explorer angezeigt. (In der nicht Express Edition-Version von Visual Studio wird die Datenbank-Explorer als Server-Explorer bezeichnet.) Wechseln Sie zum Datenbank-Explorer, und erweitern Sie die soeben hinzugefügte `SecurityTutorials` Datenbank. Wenn die Datenbank-Explorer auf dem Bildschirm nicht angezeigt wird, klicken Sie auf das Menü Ansicht, und wählen Sie Datenbank-Explorer aus, oder drücken Sie STRG + ALT + S. Wie in Abbildung 2 gezeigt, `SecurityTutorials` ist die Datenbank leer. Sie enthält keine Tabellen, keine Sichten und keine gespeicherten Prozeduren.

[![Die securitytutorials-Datenbank ist zurzeit leer.](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**Abbildung 2**: die `SecurityTutorials` Datenbank ist zurzeit leer ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image6.png))

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>Schritt 2: Hinzufügen des `SqlMembershipProvider` Schemas zur Datenbank

`SqlMembershipProvider`Erfordert, dass ein bestimmter Satz von Tabellen, Sichten und gespeicherten Prozeduren in der Benutzerspeicher-Datenbank installiert wird. Diese erforderlichen Datenbankobjekte können mithilfe des [ `aspnet_regsql.exe` Tools](https://msdn.microsoft.com/library/ms229862.aspx)hinzugefügt werden. Diese Datei befindet sich im `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` Ordner.

> [!NOTE]
> Das `aspnet_regsql.exe` Tool verfügt sowohl über Befehlszeilen Funktionalität als auch über eine grafische Benutzeroberfläche. Die grafische Benutzeroberfläche ist benutzerfreundlicher und ist das, was wir in diesem Tutorial untersuchen werden. Die Befehlszeilenschnittstelle ist nützlich, wenn das Hinzufügen des `SqlMembershipProvider` Schemas automatisiert werden muss, z. b. in Buildskripts oder automatisierten Testszenarien.

Das `aspnet_regsql.exe` Tool wird verwendet, um ASP.net- *Anwendungsdienste* zu einer angegebenen SQL Server Datenbank hinzuzufügen oder zu entfernen. Die ASP.NET-Anwendungsdienste umfassen die Schemas für `SqlMembershipProvider` und `SqlRoleProvider` zusammen mit den Schemas für die SQL-basierten Anbieter für andere ASP.NET 2,0-Frameworks. Wir müssen dem Tool zwei Informationen bereitstellen `aspnet_regsql.exe` :

- Ob wir Anwendungsdienste hinzufügen oder entfernen möchten, und
- Die Datenbank, aus der das Anwendungs Dienst Schema hinzugefügt oder entfernt werden soll.

Wenn Sie aufgefordert werden, die Datenbank zu verwenden, `aspnet_regsql.exe` fordert das Tool uns auf, den Namen des Servers, auf dem sich die Datenbank befindet, die Sicherheits Anmelde Informationen für die Verbindung mit der Datenbank und den Datenbanknamen anzugeben. Wenn Sie die nicht-Express-Edition von SQL Server verwenden, sollten Sie diese Informationen bereits kennen, da es sich dabei um die gleichen Informationen handelt, die Sie über eine Verbindungs Zeichenfolge bereitstellen müssen, wenn Sie die Datenbank über eine ASP.NET-Webseite verwenden. Es ist jedoch etwas komplizierter, den Server-und Datenbanknamen zu ermitteln, wenn Sie eine SQL Server 2005 Express Edition Datenbank im `App_Data` Ordner verwenden.

Im folgenden Abschnitt wird eine einfache Möglichkeit zum Angeben des Server-und Daten Banknamens für eine SQL Server 2005 Express Edition Datenbank im `App_Data` Ordner erläutert. Wenn Sie SQL Server 2005 Express Edition nicht verwenden, können Sie mit dem Abschnitt Installieren des Anwendungsdienste fortfahren.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>Bestimmen des Server-und Daten Banknamens für eine SQL Server 2005 Express Edition Datenbank im `App_Data` Ordner

Um das Tool verwenden zu können, `aspnet_regsql.exe` müssen Sie den Namen des Servers und der Datenbank kennen. Der Servername ist `localhost\InstanceName` . Höchstwahrscheinlich ist der *instanceName* `SQLExpress` . Wenn Sie SQL Server 2005 Express Edition jedoch manuell installiert haben (d. h., Sie haben Sie bei der Installation von Visual Studio nicht automatisch installiert), ist es möglich, dass Sie einen anderen Instanznamen ausgewählt haben.

Der Datenbankname ist etwas schwieriger zu bestimmen. Datenbanken im `App_Data` Ordner verfügen in der Regel über einen Datenbanknamen, der eine [Globally Unique Identifier](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) zusammen mit dem Pfad zur Datenbankdatei enthält. Wir müssen diesen Datenbanknamen bestimmen, um das Anwendungs Dienst Schema über hinzuzufügen `aspnet_regsql.exe` .

Die einfachste Möglichkeit, den Datenbanknamen zu ermitteln, besteht darin, ihn über SQL Server Management Studio zu untersuchen. SQL Server Management Studio stellt eine grafische Benutzeroberfläche zum Verwalten von SQL Server 2005-Datenbanken bereit, wird jedoch nicht mit der Express-Edition von SQL Server 2005 ausgeliefert. Die gute Nachricht ist, dass Sie die kostenlose Express-Edition von SQL Server Management Studio [herunterladen können](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) .

> [!NOTE]
> Wenn Sie auch eine nicht Express Edition-Version von SQL Server 2005 auf Ihrem Desktop installiert haben, ist die Vollversion der Management Studio wahrscheinlich installiert. Sie können die Vollversion verwenden, um den Datenbanknamen zu ermitteln. Befolgen Sie dabei die unten aufgeführten Schritte für die Express Edition.

Schließen Sie zunächst Visual Studio, um sicherzustellen, dass alle Sperren, die von Visual Studio für die Datenbankdatei erzwungen werden, geschlossen werden. Starten Sie als nächstes SQL Server Management Studio, und stellen Sie eine Verbindung mit der `localhost\InstanceName` Datenbank für SQL Server 2005 Express Edition her. Wie bereits erwähnt, ist die Wahrscheinlichkeit, dass der Instanzname lautet `SQLExpress` . Wählen Sie für die Option Authentifizierung die Option Windows-Authentifizierung aus.

[![Herstellen einer Verbindung mit der SQL Server 2005 Express Edition Instanz](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**Abbildung 3**: Herstellen einer Verbindung mit der SQL Server 2005 Express Edition Instanz ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image9.png))

Nach dem Herstellen einer Verbindung mit der SQL Server 2005 Express Edition Instanz werden Management Studio Ordner für die Datenbanken, die Sicherheitseinstellungen, die Server Objekte usw. angezeigt. Wenn Sie die Registerkarte Datenbanken erweitern, sehen Sie, dass die `SecurityTutorials.mdf` Datenbank *nicht* in der Daten Bank Instanz registriert ist. Sie müssen zuerst die Datenbank anfügen.

Klicken Sie mit der rechten Maustaste auf den Ordner Datenbanken, und wählen Sie im Kontextmenü anfügen aus. Dadurch wird das Dialogfeld Datenbanken anfügen angezeigt. Klicken Sie hier auf die Schaltfläche hinzufügen, navigieren Sie zur `SecurityTutorials.mdf` Datenbank, und klicken Sie auf OK. Abbildung 4 zeigt das Dialogfeld Datenbanken anfügen, nachdem die `SecurityTutorials.mdf` Datenbank ausgewählt wurde. Abbildung 5 zeigt die Objekt-Explorer Management Studio, nachdem die Datenbank erfolgreich angefügt wurde.

[![Fügen Sie die Datenbank "securitytutorials. mdf" an.](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**Abbildung 4**: Anfügen der `SecurityTutorials.mdf` Datenbank ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image12.png))

[![Die Datenbank "securitytutorials. mdf" wird im Ordner "Datenbanken" angezeigt](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**Abbildung 5**: die `SecurityTutorials.mdf` Datenbank wird im Ordner "Datenbanken" angezeigt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image15.png))

Wie in Abbildung 5 gezeigt, `SecurityTutorials.mdf` verfügt die Datenbank über einen Recht abstruten Namen. Ändern Sie den Namen in einen besser denkbarer (und einfacheren) Namen. Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie im Kontextmenü Umbenennen aus, und benennen Sie Sie um `SecurityTutorialsDatabase` . Dadurch wird der Dateiname nicht geändert, sondern nur der Name, den die Datenbank verwendet, um sich selbst SQL Server zu identifizieren.

[![Benennen Sie die Datenbank in securitytutorialsdatabase um.](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**Abbildung 6**: Umbenennen der Datenbank in `SecurityTutorialsDatabase` ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))

An diesem Punkt kennen wir die Server-und Datenbanknamen für die `SecurityTutorials.mdf` Datenbankdatei: `localhost\InstanceName` `SecurityTutorialsDatabase` bzw.. Nun können Sie die Anwendungsdienste über das `aspnet_regsql.exe` Tool installieren.

### <a name="installing-the-application-services"></a>Installieren des Anwendungsdienste

Um das Tool zu starten `aspnet_regsql.exe` , wechseln Sie zum Startmenü, und wählen Sie ausführen aus. Geben Sie `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` in das Textfeld ein, und klicken Sie auf OK. Alternativ können Sie Windows-Explorer verwenden, um einen Drilldown in den entsprechenden Ordner auszuführen und auf die Datei zu doppelklicken `aspnet_regsql.exe` . Bei beiden Ansätzen werden die gleichen Ergebnisse erzielt.

Wenn Sie das `aspnet_regsql.exe` Tool ohne Befehlszeilenargumente ausführen, wird die grafische Benutzeroberfläche des ASP.NET SQL Server Setup-Assistenten gestartet. Der Assistent vereinfacht das Hinzufügen oder Entfernen der ASP.NET-Anwendungsdienste für eine angegebene Datenbank. Auf dem ersten Bildschirm des Assistenten, wie in Abbildung 7 dargestellt, wird der Zweck des Tools beschrieben.

[![Verwenden des ASP.NET-SQL Server Setup-Assistenten zum Hinzufügen des Mitgliedschafts Schemas](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**Abbildung 7**: Verwenden des ASP.NET-SQL Server Setup-Assistenten zum Hinzufügen des Mitgliedschafts Schemas ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image21.png))

Im zweiten Schritt des Assistenten werden Sie gefragt, ob Sie die Anwendungsdienste hinzufügen oder entfernen möchten. Da wir die für erforderlichen Tabellen, Sichten und gespeicherten Prozeduren hinzufügen möchten `SqlMembershipProvider` , wählen Sie die Option SQL Server für Anwendungsdienste konfigurieren aus. Wenn Sie dieses Schema später aus der Datenbank entfernen möchten, führen Sie diesen Assistenten erneut aus, und wählen Sie stattdessen die Option Anwendungs Dienst Informationen aus einer vorhandenen Datenbank entfernen aus.

[![Wählen Sie die Option SQL Server für Anwendungsdienste konfigurieren aus.](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**Abbildung 8**: Auswählen der Option "SQL Server für Anwendungsdienste konfigurieren" ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image24.png))

Im dritten Schritt werden die Datenbankinformationen angezeigt: der Servername, die Authentifizierungsinformationen und der Datenbankname. Wenn Sie mit diesem Tutorial gearbeitet haben und die Datenbank zu hinzugefügt haben, fügen Sie Sie an `SecurityTutorials.mdf` `App_Data` `localhost\InstanceName` , und benennen Sie Sie in um. `SecurityTutorialsDatabase` verwenden Sie dann die folgenden Werte:

- Server: `localhost\InstanceName`
- Windows-Authentifizierung
- Verbindung `SecurityTutorialsDatabase`

[![Datenbankinformationen eingeben](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**Abbildung 9**: eingeben der Datenbankinformationen ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image27.png))

Nachdem Sie die Datenbankinformationen eingegeben haben, klicken Sie auf Weiter. Im letzten Schritt werden die Schritte zusammengefasst, die ausgeführt werden. Klicken Sie auf Weiter, um die Anwendungsdienste zu installieren, und schließen Sie dann den Assistenten ab.

> [!NOTE]
> Wenn Sie Management Studio verwendet haben, um die Datenbank anzufügen und die Datenbankdatei umzubenennen, stellen Sie sicher, dass Sie die Datenbank trennen und Management Studio schließen, bevor Sie Visual Studio erneut öffnen. Um die Datenbank zu trennen `SecurityTutorialsDatabase` , klicken Sie mit der rechten Maustaste auf den Datenbanknamen, und wählen Sie im Menü Aufgaben die Option trennen aus.

Wenn Sie den Assistenten abgeschlossen haben, kehren Sie zu Visual Studio zurück, und navigieren Sie zum Datenbank-Explorer. Erweitern Sie den Ordner Tabellen. Es sollte eine Reihe von Tabellen angezeigt werden, deren Namen mit dem Präfix beginnen `aspnet_` . Ebenso finden Sie eine Vielzahl von Sichten und gespeicherten Prozeduren unter den Ordnern Sichten und gespeicherte Prozeduren. Diese Datenbankobjekte bilden das Anwendungs Dienst Schema. Die Mitgliedschafts-und Rollen spezifischen Datenbankobjekte werden in Schritt 3 untersucht.

[![Der Datenbank wurden eine Vielzahl von Tabellen, Sichten und gespeicherten Prozeduren hinzugefügt.](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**Abbildung 10**: eine Vielzahl von Tabellen, Sichten und gespeicherten Prozeduren wurden der Datenbank hinzugefügt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image30.png))

> [!NOTE]
> Die `aspnet_regsql.exe` grafische Benutzeroberfläche des Tools installiert das gesamte Anwendungs Dienst Schema. Wenn Sie jedoch `aspnet_regsql.exe` über die Befehlszeile ausführen, können Sie angeben, welche Komponenten für bestimmte Anwendungsdienste installiert (oder entfernt) werden sollen. Wenn Sie also nur die Tabellen, Sichten und gespeicherten Prozeduren hinzufügen möchten, die für die `SqlMembershipProvider` -und- `SqlRoleProvider` Anbieter erforderlich sind, führen Sie über `aspnet_regsql.exe` die Befehlszeile aus. Alternativ können Sie die entsprechende Teilmenge von T-SQL-CREATE-Skripts, die von verwendet werden, manuell ausführen `aspnet_regsql.exe` . Diese Skripts befinden sich im `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` Ordner mit Namen wie `InstallCommon.sql` , `InstallMembership.sql` , `InstallRoles.sql` , `InstallProfile.sql` , `InstallSqlState.sql` usw.

An dieser Stelle haben wir die Datenbankobjekte erstellt, die von benötigt werden `SqlMembershipProvider` . Wir müssen jedoch weiterhin das Mitgliedschafts Framework anweisen, dass es (im `SqlMembershipProvider` Gegensatz zum, der) verwendet `ActiveDirectoryMembershipProvider` und die `SqlMembershipProvider` Datenbank verwenden soll `SecurityTutorials` . Wir sehen uns an, wie Sie angeben, welcher Anbieter verwendet werden soll, und wie die Einstellungen des ausgewählten Anbieters in Schritt 4 angepasst werden. Zuerst sehen wir uns die soeben erstellten Datenbankobjekte genauer an.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>Schritt 3: Untersuchen der Kern Tabellen des Schemas

Beim Arbeiten mit den Mitgliedschafts-und Rollen Frameworks in einer ASP.NET-Anwendung werden die Implementierungsdetails vom Anbieter gekapselt. In zukünftigen Tutorials werden diese Frameworks über die `Membership` Klassen und .NET Framework `Roles` . Bei Verwendung dieser APIs auf hoher Ebene müssen wir uns nicht mit den Details auf niedriger Ebene befassen, wie z. b. welche Abfragen ausgeführt werden oder welche Tabellen von und geändert werden `SqlMembershipProvider` `SqlRoleProvider` .

Wir könnten die Mitgliedschafts-und Rollen Frameworks zuverlässig verwenden, ohne das in Schritt 2 erstellte Datenbankschema zu untersucht. Beim Erstellen von Tabellen zum Speichern von Anwendungsdaten müssen wir jedoch möglicherweise Entitäten erstellen, die sich auf Benutzer oder Rollen beziehen. `SqlMembershipProvider` `SqlRoleProvider` Beim Einrichten von Foreign Key-Einschränkungen zwischen den Anwendungsdaten Tabellen und den Tabellen, die in Schritt 2 erstellt wurden, ist es hilfreich, sich mit den Schemas und vertraut zu machen. In bestimmten seltenen Fällen müssen wir möglicherweise eine Schnittstelle mit den Benutzer-und Rollen speichern direkt auf Datenbankebene (anstelle der- `Membership` Klasse oder der- `Roles` Klasse) verwenden.

### <a name="partitioning-the-user-store-into-applications"></a>Partitionierung des Benutzer Stores in Anwendungen

Die Mitgliedschafts-und Rollen-Frameworks sind so konzipiert, dass ein einzelner Benutzer und ein Rollen Speicher von vielen verschiedenen Anwendungen gemeinsam genutzt werden können. Eine ASP.NET-Anwendung, die die Mitgliedschafts-oder Rollen Framework verwendet, muss angeben, welche Anwendungs Partition verwendet werden soll. Kurz gesagt können mehrere Webanwendungen dieselben Benutzer-und Rollen Speicher verwenden. Abbildung 11 stellt Benutzer-und Rollen Speicher dar, die in drei Anwendungen partitioniert sind: hrsite, customersite und salessite. Diese drei Webanwendungen verfügen jeweils über eigene eindeutige Benutzer und Rollen, aber ihre Benutzerkonten-und Rollen Informationen werden in den gleichen Datenbanktabellen gespeichert.

[![Benutzerkonten können über mehrere Anwendungen hinweg partitioniert werden.](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**Abbildung 11**: Benutzerkonten können über mehrere Anwendungen hinweg partitioniert werden ([Klicken Sie, um das Bild in voller Größe anzuzeigen](creating-the-membership-schema-in-sql-server-cs/_static/image33.png))

In der `aspnet_Applications` Tabelle werden diese Partitionen definiert. Jede Anwendung, die die Datenbank zum Speichern von Benutzerkontoinformationen verwendet, wird durch eine Zeile in dieser Tabelle dargestellt. Die `aspnet_Applications` Tabelle enthält vier Spalten: `ApplicationId` , `ApplicationName` , `LoweredApplicationName` und `Description` . `ApplicationId` ist vom Typ [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) und ist der Primärschlüssel der Tabelle `ApplicationName` . stellt einen eindeutigen benutzerfreundlichen Namen für jede Anwendung bereit.

Die anderen Mitgliedschafts-und Rollen bezogenen Tabellen werden wieder mit dem- `ApplicationId` Feld in verknüpft `aspnet_Applications` . Die `aspnet_Users` Tabelle, die einen Datensatz für jedes Benutzerkonto enthält, verfügt beispielsweise über ein `ApplicationId` Fremdschlüssel Feld, Ditto für die `aspnet_Roles` Tabelle. Das `ApplicationId` Feld in diesen Tabellen gibt die Anwendungs Partition an, zu der das Benutzerkonto oder die Rolle gehört.

### <a name="storing-user-account-information"></a>Speichern von Benutzerkontoinformationen

Die Benutzerkontoinformationen sind in zwei Tabellen untergebracht: `aspnet_Users` und `aspnet_Membership` . Die `aspnet_Users` Tabelle enthält Felder, die die wesentlichen Benutzerkontoinformationen enthalten. Die drei relevantesten Spalten lauten:

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` ist der Primärschlüssel (und vom Typ `uniqueidentifier` ). `UserName` ist vom Typ `nvarchar(256)` und bildet zusammen mit dem Kennwort die Anmelde Informationen des Benutzers. (Das Kennwort eines Benutzers wird in der `aspnet_Membership` Tabelle gespeichert.) `ApplicationId` verknüpft das Benutzerkonto mit einer bestimmten Anwendung in `aspnet_Applications` . In der-Spalte und der-Spalte ist eine zusammengesetzte [ `UNIQUE` Einschränkung](https://msdn.microsoft.com/library/ms191166.aspx) vorhanden `UserName` `ApplicationId` . Dadurch wird sichergestellt, dass jeder Benutzername in einer bestimmten Anwendung eindeutig ist, aber auch `UserName` in verschiedenen Anwendungen verwendet werden kann.

Die `aspnet_Membership` Tabelle enthält zusätzliche Benutzerkontoinformationen, wie z. b. das Kennwort des Benutzers, die e-Mail-Adresse, das Datum und die Uhrzeit der letzten Anmeldung usw. Zwischen den Datensätzen in den Tabellen und besteht eine eins-zu-eins-Entsprechung `aspnet_Users` `aspnet_Membership` . Diese Beziehung wird durch das- `UserId` Feld in gewährleistet `aspnet_Membership` , das als Primärschlüssel der Tabelle dient. Wie die `aspnet_Users` Tabelle `aspnet_Membership` enthält auch ein `ApplicationId` Feld, das diese Informationen an eine bestimmte Anwendungs Partition bindet.

### <a name="securing-passwords"></a>Sichern von Kenn Wörtern

Die Kenn Wort Informationen werden in der `aspnet_Membership` Tabelle gespeichert. Ermöglicht das Speichern von Kenn `SqlMembershipProvider` Wörtern in der Datenbank mithilfe einer der folgenden drei Verfahren:

- **Clear** : das Kennwort wird in der Datenbank als Klartext gespeichert. Ich empfehle dringend, diese Option zu verwenden. Wenn die Datenbank kompromittiert ist, wird Sie von einem Hacker gefunden, der eine Hintertür oder einen verärgerten-Mitarbeiter hat, der über Zugriff auf die Datenbank verfügt. die Anmelde Informationen für jeden einzelnen Benutzer sind für das nehmen vorhanden.
- Hash **-Kenn** Wörter werden mithilfe eines unidirektionalen Hash Algorithmus und eines zufällig generierten Salt-Werts Hashwert erstellt. Dieser Hashwert (zusammen mit dem Salt-Wert) wird in der-Datenbank gespeichert.
- **Verschlüsselt** : eine verschlüsselte Version des Kennworts wird in der Datenbank gespeichert.

Die verwendete Kenn Wort Speichermethode hängt von den `SqlMembershipProvider` in angegebenen Einstellungen ab `Web.config` . Wir sehen uns an, wie die `SqlMembershipProvider` Einstellungen in Schritt 4 angepasst werden. Das Standardverhalten ist das Speichern des Hashwerts des Kennworts.

Die für das Speichern des Kennworts Verantwortlichen Spalten lauten `Password` , `PasswordFormat` und `PasswordSalt` . `PasswordFormat` ein Feld vom Typ `int` , dessen Wert die Technik angibt, die zum Speichern des Kennworts verwendet wird: 0 für Clear; 1 für Hash; 2 für verschlüsselt. `PasswordSalt` wird unabhängig von der verwendeten Kenn Wort Speichermethode eine zufällig generierte Zeichenfolge zugewiesen. der Wert von `PasswordSalt` wird nur beim Berechnen des Hashwerts des Kennworts verwendet. Zum Schluss `Password` enthält die Spalte die eigentlichen Kenn Wort Daten, das nur-Text-Kennwort, der Hashwert des Kennworts oder das verschlüsselte Kennwort.

Tabelle 1 zeigt, wie diese drei Spalten für die verschiedenen Speichertechniken aussehen können, wenn das Kennwort MySecret gespeichert wird. .

| **Speichertechnik &lt; \_ o3a \_ p/&gt;** | **Kennwort &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **PasswordSalt &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Löschen | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| Hash | 2oxm6szhwbthf gjgkgqsc2ec9zm = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| Verschlüsselt | 62rzgdvhxykkqsmchz0yly7hs6onhpaocyarxv8g0f4cw56oxuu3e7inza9j9bkp | 2 | Lsrzhgs/AA/oqaxglhjnbw = = |

**Tabelle 1**: Beispiel Werte für die Kenn Wort bezogenen Felder, wenn das Kennwort MySecret gespeichert wird.

> [!NOTE]
> Der bestimmte Verschlüsselungs-oder Hash Algorithmus, der von verwendet `SqlMembershipProvider` wird, wird durch die Einstellungen im- `<machineKey>` Element bestimmt. Dieses Konfigurationselement wurde in Schritt 3 des <a id="Tutorial3"></a> Tutorials [*Konfiguration der Formular Authentifizierung und erweiterte Themen*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) erläutert.

### <a name="storing-roles-and-role-associations"></a>Speichern von Rollen und Rollen Zuordnungen

Das Rollen Framework ermöglicht es Entwicklern, eine Gruppe von Rollen zu definieren und anzugeben, welche Benutzer zu welchen Rollen gehören. Diese Informationen werden in der-Datenbank über zwei Tabellen aufgezeichnet: `aspnet_Roles` und `aspnet_UsersInRoles` . Jeder Datensatz in der `aspnet_Roles` Tabelle stellt eine Rolle für eine bestimmte Anwendung dar. Ähnlich wie `aspnet_Users` in der Tabelle `aspnet_Roles` enthält die Tabelle drei Spalten, die für unsere Diskussion relevant sind:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` ist der Primärschlüssel (und vom Typ `uniqueidentifier` ). `RoleName` ist vom Typ `nvarchar(256)`. Und `ApplicationId` verknüpft das Benutzerkonto mit einer bestimmten Anwendung in `aspnet_Applications` . `UNIQUE`In der-Spalte und der-Spalte ist eine zusammengesetzte Einschränkung vorhanden `RoleName` `ApplicationId` , die sicherstellt, dass jeder Rollenname in einer bestimmten Anwendung eindeutig ist.

Die `aspnet_UsersInRoles` Tabelle dient als Zuordnung zwischen Benutzern und Rollen. Es gibt nur zwei Spalten: `UserId` und `RoleId` zusammen bilden Sie einen zusammengesetzten Primärschlüssel.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>Schritt 4: Angeben des Anbieters und Anpassen der Einstellungen

Alle Frameworks, die das Anbieter Modell unterstützen (z. b. die Mitgliedschafts-und Rollen-Frameworks), fehlen Implementierungsdetails selbst und delegieren diese Aufgabe stattdessen an eine Anbieter Klasse. Im Fall des Mitgliedschafts-Frameworks definiert die- `Membership` Klasse die API zum Verwalten von Benutzerkonten, aber Sie interagiert nicht direkt mit einem Benutzerspeicher. Stattdessen übergeben die `Membership` Methoden der-Klasse die Anforderung an den konfigurierten Anbieter. Wir verwenden den `SqlMembershipProvider` . Wie weiß das Mitgliedschafts Framework beim Aufrufen einer der Methoden in der- `Membership` Klasse, dass der Aufruf an den delegiert werden soll `SqlMembershipProvider` ?

Die- `Membership` Klasse verfügt über eine- [ `Providers` Eigenschaft](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) , die einen Verweis auf alle registrierten Anbieter Klassen enthält, die für die Verwendung durch das Mitgliedschafts Framework verfügbar sind. Jeder registrierte Anbieter verfügt über einen zugeordneten Namen und Typ. Der Name bietet eine benutzerfreundliche Möglichkeit, auf einen bestimmten Anbieter in der Auflistung zu verweisen `Providers` , während der Typ die Anbieter Klasse identifiziert. Außerdem kann jeder registrierte Anbieter Konfigurationseinstellungen enthalten. Zu den Konfigurationseinstellungen für das Mitgliedschafts Framework zählen `passwordFormat` unter anderem und `requiresUniqueEmail` . Eine komplette Liste der von verwendeten Konfigurationseinstellungen finden Sie in Tabelle 2 `SqlMembershipProvider` .

Der `Providers` Inhalt der Eigenschaft wird durch die Konfigurationseinstellungen der Webanwendung angegeben. Standardmäßig verfügen alle Webanwendungen über einen Anbieter `AspNetSqlMembershipProvider` mit dem Namen vom Typ `SqlMembershipProvider` . Dieser Standard Mitgliedschafts Anbieter ist in registriert `machine.config` (befindet sich unter `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)` :

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

Wie das obige Markup zeigt, definiert das- [ `<membership>` Element](https://msdn.microsoft.com/library/1b9hw62f.aspx) die Konfigurationseinstellungen für das Mitgliedschafts Framework, während das untergeordnete- [ `<providers>` Element](https://msdn.microsoft.com/library/6d4936ht.aspx) die registrierten Anbieter angibt. Anbieter können mithilfe des-Elements oder des-Elements hinzugefügt oder entfernt werden [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) . verwenden Sie das- [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) Element, um alle derzeit registrierten Anbieter zu entfernen Wie das obige Markup zeigt, `machine.config` Fügt einen Anbieter mit dem Namen `AspNetSqlMembershipProvider` des Typs hinzu `SqlMembershipProvider` .

Zusätzlich zu den `name` -und- `type` Attributen enthält das- `<add>` Element Attribute, die die Werte für verschiedene Konfigurationseinstellungen definieren. In Tabelle 2 werden die verfügbaren `SqlMembershipProvider` -spezifischen Konfigurationseinstellungen zusammen mit einer Beschreibung aufgeführt.

> [!NOTE]
> Alle in Tabelle 2 notierten Standardwerte verweisen auf die in der-Klasse definierten Standardwerte `SqlMembershipProvider` . Beachten Sie, dass nicht alle Konfigurationseinstellungen in `AspNetSqlMembershipProvider` den Standardwerten der-Klasse entsprechen `SqlMembershipProvider` . Wenn Sie z. b. nicht in einem Mitgliedschafts Anbieter angegeben ist, wird `requiresUniqueEmail` standardmäßig true verwendet. Der `AspNetSqlMembershipProvider` überschreibt diesen Standardwert jedoch durch explizites angeben eines Werts von `false` .

| **Festlegen von &lt; \_ o3a \_ p/&gt;** | **Beschreibung &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | Beachten Sie, dass das Mitgliedschafts Framework ermöglicht, dass ein einzelner Benutzerspeicher über mehrere Anwendungen hinweg partitioniert werden kann. Diese Einstellung gibt den Namen der Anwendungs Partition an, die vom Mitgliedschafts Anbieter verwendet wird. Wenn dieser Wert nicht explizit angegeben wird, wird er zur Laufzeit auf den Wert des virtuellen Stammpfad der Anwendung festgelegt. |
| `commandTimeout` | Gibt den Timeout Wert für den SQL-Befehl (in Sekunden) an. Der Standardwert ist 30. |
| `connectionStringName` | Der Name der Verbindungs Zeichenfolge im- `<connectionStrings>` Element, das zum Herstellen einer Verbindung mit der Benutzerspeicher-Datenbank verwendet werden soll. Dieser Wert ist erforderlich. |
| `description` | Stellt eine benutzerfreundliche Beschreibung des registrierten Anbieters bereit. |
| `enablePasswordRetrieval` | Gibt an, ob Benutzer ihr vergessenes Kennwort abrufen dürfen. Standardwert: `false`. |
| `enablePasswordReset` | Gibt an, ob Benutzer Ihr Kennwort zurücksetzen können. Wird standardmäßig auf `true` festgelegt. |
| `maxInvalidPasswordAttempts` | Die maximale Anzahl von erfolglosen Anmelde versuchen, die für einen bestimmten Benutzer während der angegebenen auftreten können, `passwordAttemptWindow` bevor der Benutzer gesperrt wird. Der Standardwert ist 5. |
| `minRequiredNonalphanumericCharacters` | Die Mindestanzahl nicht alphanumerischer Zeichen, die im Kennwort eines Benutzers angezeigt werden müssen. Dieser Wert muss zwischen 0 und 128 liegen. der Standardwert ist 1. |
| `minRequiredPasswordLength` | Die Mindestanzahl von Zeichen, die in einem Kennwort erforderlich sind. Dieser Wert muss zwischen 0 und 128 liegen. der Standardwert ist 7. |
| `name` | Der Name des registrierten Anbieters. Dieser Wert ist erforderlich. |
| `passwordAttemptWindow` | Die Anzahl der Minuten, während der fehlgeschlagene Anmeldeversuche nachverfolgt werden. Wenn ein Benutzer innerhalb dieses angegebenen Fensters ungültige Anmeldungs Anmelde Informationen angibt `maxInvalidPasswordAttempts` , werden diese gesperrt. Der Standardwert ist 10. |
| `PasswordFormat` | Das Kenn Wort Speicherformat: `Clear` , `Hashed` oder `Encrypted` . Der Standardwert lautet `Hashed`. |
| `passwordStrengthRegularExpression` | Wenn angegeben, wird dieser reguläre Ausdruck zum Auswerten der Stärke des ausgewählten Kennworts des Benutzers verwendet, wenn ein neues Konto erstellt oder das Kennwort geändert wird. Der Standardwert ist eine leere Zeichenfolge. |
| `requiresQuestionAndAnswer` | Gibt an, ob ein Benutzer seine Sicherheitsfrage beim Abrufen oder Zurücksetzen seines Kennworts beantworten muss. Standardwert: `true`. |
| `requiresUniqueEmail` | Gibt an, ob alle Benutzerkonten in einer bestimmten Anwendungs Partition über eine eindeutige e-Mail-Adresse verfügen müssen. Standardwert: `true`. |
| `type` | Gibt den Typ des Anbieters an. Dieser Wert ist erforderlich. |

**Tabelle 2**: Mitgliedschafts-und `SqlMembershipProvider` Konfigurationseinstellungen

Zusätzlich zu `AspNetSqlMembershipProvider` können andere Mitgliedschafts Anbieter auf Anwendungs Basis registriert werden, indem der Datei ähnliches Markup hinzugefügt wird `Web.config` .

> [!NOTE]
> Das Framework für Rollen funktioniert in etwa wie folgt: Es gibt einen standardmäßigen registrierten Rollen Anbieter in, `machine.config` und die registrierten Anbieter können auf Anwendungs-zu-Anwendung-Basis in angepasst werden `Web.config` . In einem zukünftigen Tutorial werden das Rollen Framework und das dazugehörige Konfigurations Markup ausführlich erläutert.

### <a name="customizing-thesqlmembershipprovidersettings"></a>Anpassen der `SqlMembershipProvider` Einstellungen

Für den Standardwert `SqlMembershipProvider` ( `AspNetSqlMembershipProvider` ) ist das- `connectionStringName` Attribut auf festgelegt `LocalSqlServer` . Wie der- `AspNetSqlMembershipProvider` Anbieter wird der Name der Verbindungs Zeichenfolge `LocalSqlServer` in definiert `machine.config` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

Wie Sie sehen können, definiert diese Verbindungs Zeichenfolge eine SQL 2005 Express Edition-Datenbank unter | DataDirectory | aspnetdb. mdf. Die Zeichenfolge | DataDirectory | wird zur Laufzeit übersetzt, um auf das `~/App_Data/` Verzeichnis zu verweisen, also der Daten bankpfad | DataDirectory | aspnetdb. mdf "übersetzt in `~/App_Data` / `aspnet.mdf` .

Wenn in der Datei der Anwendung keine Mitgliedschafts Anbieter Informationen angegeben `Web.config` wurden, verwendet die Anwendung den standardmäßigen registrierten Mitgliedschafts Anbieter `AspNetSqlMembershipProvider` . Wenn die `~/App_Data/aspnet.mdf` Datenbank nicht vorhanden ist, wird Sie von der ASP.NET-Laufzeit automatisch erstellt und das Anwendungs Dienst Schema hinzugefügt. Wir möchten jedoch nicht die-Datenbank verwenden, `aspnet.mdf` sondern möchten die Datenbank verwenden, die `SecurityTutorials.mdf` wir in Schritt 2 erstellt haben. Diese Änderung kann auf zwei Arten durchgeführt werden:

- <strong>Geben Sie einen Wert für das</strong> <strong>`LocalSqlServer`</strong> <strong>Name der Verbindungs Zeichenfolge in</strong> <strong>`Web.config`</strong> <strong>.</strong> Durch Überschreiben des `LocalSqlServer` Werts für den Verbindungs Zeichenfolgen-Namen in `Web.config` können wir den standardmäßigen registrierten Mitgliedschafts Anbieter ( `AspNetSqlMembershipProvider` ) verwenden und ordnungsgemäß mit der `SecurityTutorials.mdf` Datenbank arbeiten. Diese Vorgehensweise ist in Ordnung, wenn Sie Inhalte mit den von angegebenen Konfigurationseinstellungen haben `AspNetSqlMembershipProvider` . Weitere Informationen zu dieser Technik finden Sie im Blogbeitrag von [Scott Guthrie](https://weblogs.asp.net/scottgu/), [Konfigurieren von ASP.NET 2,0 Anwendungsdienste für die Verwendung von SQL Server 2000 oder SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>Fügen Sie einen neuen registrierten Anbieter vom Typ</strong> <strong>`SqlMembershipProvider`</strong> hinzu. <strong>und konfigurieren</strong> <strong>`connectionStringName`</strong> <strong>festlegen, dass auf das</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>Datenbank:</strong> Diese Vorgehensweise ist nützlich in Szenarien, in denen andere Konfigurations Eigenschaften zusätzlich zur Daten bankverbindungs Zeichenfolge angepasst werden sollen. In meinen eigenen Projekten verwende ich diesen Ansatz immer aufgrund seiner Flexibilität und Lesbarkeit.

Bevor ein neuer registrierter Anbieter hinzugefügt werden kann, der auf die `SecurityTutorials.mdf` Datenbank verweist, müssen wir zunächst im Abschnitt in einen entsprechenden Wert für die Verbindungs Zeichenfolge einfügen `<connectionStrings>` `Web.config` . Das folgende Markup fügt eine neue Verbindungs Zeichenfolge mit dem Namen hinzu `SecurityTutorialsConnectionString` , die auf die SQL Server 2005 Express Edition `SecurityTutorials.mdf` Datenbank im `App_Data` Ordner verweist.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> Wenn Sie eine Alternative Datenbankdatei verwenden, aktualisieren Sie die Verbindungs Zeichenfolge nach Bedarf. Weitere Informationen zum bilden der richtigen Verbindungs Zeichenfolge finden Sie unter [connectionStrings.com](http://www.connectionstrings.com/).

Fügen Sie als nächstes der Datei das folgende Konfigurations Markup für die Mitgliedschaft hinzu `Web.config` . Dieses Markup registriert einen neuen Anbieter mit dem Namen `SecurityTutorialsSqlMembershipProvider` .

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

Zusätzlich zur Registrierung des `SecurityTutorialsSqlMembershipProvider` Anbieters definiert das obige Markup das- `SecurityTutorialsSqlMembershipProvider` Element als Standardanbieter (über das- `defaultProvider` Attribut im- `<membership>` Element). Denken Sie daran, dass das Mitgliedschafts Framework mehrere registrierte Anbieter aufweisen kann. Da `AspNetSqlMembershipProvider` als erster Anbieter in registriert ist `machine.config` , fungiert es als Standardanbieter, sofern nicht anders angegeben.

Derzeit verfügt unsere Anwendung über zwei registrierte Anbieter: `AspNetSqlMembershipProvider` und `SecurityTutorialsSqlMembershipProvider` . Vor der Registrierung des `SecurityTutorialsSqlMembershipProvider` Anbieters konnten jedoch alle zuvor registrierten Anbieter gelöscht werden, indem ein- [ `<clear />` Element](https://msdn.microsoft.com/library/t062y6yc.aspx) direkt vor dem-Element hinzugefügt wurde `<add>` . Dadurch `AspNetSqlMembershipProvider` wird der aus der Liste der registrierten Anbieter gelöscht, was bedeutet, dass der `SecurityTutorialsSqlMembershipProvider` der einzige registrierte Mitgliedschafts Anbieter ist. Wenn Sie diesen Ansatz verwenden, müssen wir nicht `SecurityTutorialsSqlMembershipProvider` als Standardanbieter markieren, da es sich dabei um den einzigen registrierten Mitgliedschafts Anbieter handelt. Weitere Informationen zum Verwenden von `<clear />` finden Sie unter Verwenden von zum [ `<clear />` Hinzufügen von Anbietern](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx).

Beachten Sie, dass die `SecurityTutorialsSqlMembershipProvider` - `connectionStringName` Einstellung auf den soeben hinzugefügten `SecurityTutorialsConnectionString` Namen der Verbindungs Zeichenfolge verweist und dass die `applicationName` Einstellung auf den Wert securitytutorials festgelegt wurde. Außerdem wurde die- `requiresUniqueEmail` Einstellung auf festgelegt `true` . Alle anderen Konfigurationsoptionen sind identisch mit den Werten in `AspNetSqlMembershipProvider` . Wenn Sie möchten, können Sie an dieser Stelle jederzeit Änderungen an der Konfiguration vornehmen. Beispielsweise können Sie die Kenn Wort Sicherheit erhöhen, indem Sie anstelle eines der beiden nicht-alphanumerischen Zeichen zwei nicht-alphanumerische Zeichen benötigen, oder indem Sie die Kenn Wort Länge auf acht Zeichen anstelle von 7 erhöhen.

> [!NOTE]
> Beachten Sie, dass das Mitgliedschafts Framework ermöglicht, dass ein einzelner Benutzerspeicher über mehrere Anwendungen hinweg partitioniert werden kann. Die Einstellung des Mitgliedschafts Anbieters `applicationName` gibt an, welche Anwendung der Anbieter bei der Arbeit mit dem Benutzerspeicher verwendet. Es ist wichtig, dass Sie explizit einen Wert für die `applicationName` Konfigurationseinstellung festlegen, denn wenn der `applicationName` nicht explizit festgelegt ist, wird er zur Laufzeit dem virtuellen Stammpfad der Webanwendung zugewiesen. Dies funktioniert einwandfrei, solange der virtuelle Stammpfad der Anwendung nicht geändert wird. Wenn Sie die Anwendung jedoch in einen anderen Pfad verschieben, `applicationName` ändert sich auch die Einstellung. In diesem Fall wird der Mitgliedschafts Anbieter mit einer anderen Anwendungs Partition arbeiten, als zuvor verwendet wurde. Benutzerkonten, die vor dem Verschieben erstellt wurden, befinden sich in einer anderen Anwendungs Partition, und diese Benutzer können sich nicht mehr bei der Website anmelden. Eine ausführlichere Erläuterung zu diesem Thema finden Sie unter [immer Festlegen der `applicationName` Eigenschaft beim Konfigurieren der ASP.NET 2,0-Mitgliedschaft und anderer Anbieter](https://weblogs.asp.net/scottgu/443634).

## <a name="summary"></a>Zusammenfassung

An dieser Stelle verfügen wir über eine Datenbank mit den konfigurierten Anwendungsdiensten ( `SecurityTutorials.mdf` ) und haben die Webanwendung so konfiguriert, dass das Mitgliedschafts Framework den `SecurityTutorialsSqlMembershipProvider` soeben registrierten Anbieter verwendet. Dieser registrierte Anbieter `SqlMembershipProvider` hat den Typ und ist `connectionStringName` auf die entsprechende Verbindungs Zeichenfolge ( `SecurityTutorialsConnectionString` ) und dessen `applicationName` Wert explizit festgelegt.

Wir sind nun bereit, das Mitgliedschafts Framework aus unserer Anwendung zu verwenden. Im nächsten Tutorial wird erläutert, wie neue Benutzerkonten erstellt werden. Im folgenden erfahren Sie, wie Sie die Authentifizierung von Benutzern, die Durchführung einer benutzerbasierten Autorisierung und das Speichern zusätzlicher Benutzer bezogener Informationen in der-Datenbank untersuchen.

Fröhliche Programmierung!

### <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu den in diesem Tutorial behandelten Themen finden Sie in den folgenden Ressourcen:

- [Legen Sie die `applicationName` -Eigenschaft beim Konfigurieren der ASP.NET 2,0-Mitgliedschaft und anderer Anbieter immer fest.](https://weblogs.asp.net/scottgu/443634)
- [Konfigurieren von ASP.NET 2,0 Anwendungsdienste für die Verwendung SQL Server 2000 oder SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Herunterladen von SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [Überprüfen der Mitgliedschaft, Rollen und Profile von ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Das- `<add>` Element für Anbieter für die Mitgliedschaft.](https://msdn.microsoft.com/library/whae3t94.aspx)
- [Das `<membership>` Element](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [Das `<providers>` Element für die Mitgliedschaft.](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [Verwenden `<clear />` beim Hinzufügen von Anbietern](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [Arbeiten direkt mit dem `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Video Schulung zu Themen in diesem Tutorial

- [Grundlegendes zu ASP.NET-Mitgliedschaften](../../../videos/authentication/understanding-aspnet-memberships.md)
- [Konfigurieren von SQL für die Arbeit mit Mitgliedschaftsschemas](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [Ändern der Mitgliedschaftseinstellungen im Mitgliedschaftsschema](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>Zum Autor

Scott Mitchell, Autor mehrerer ASP/ASP. net-Bücher und Gründer von 4GuysFromRolla.com, hat seit 1998 mit Microsoft-Webtechnologien gearbeitet. Scott arbeitet als unabhängiger Berater, Ausbilder und Writer. Sein letztes Buch ist *[Sams Teach Yourself ASP.NET 2,0 in 24 Stunden](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott kann bei [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) oder über seinen Blog von erreicht werden [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Besonders vielen Dank

Diese tutorialreihe wurde von vielen hilfreichen Reviewern geprüft. Lead Reviewer für dieses Tutorial war Alicja Maziarz. Möchten Sie meine bevorstehenden MSDN-Artikel überprüfen? Wenn dies der Fall ist, löschen Sie die Zeile in [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [Nächste](creating-user-accounts-cs.md)
