---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: Authentifizierung von Benutzern mit Formularauthentifizierung (C) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie das Attribut [Authorize] verwenden, um bestimmte Seiten in Ihrer MVC-Anwendung mit dem Kennwort zu schützen. Sie erfahren, wie Sie die Websiteverwaltung zu verwenden...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540973"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>Authentifizieren von Benutzern bei der Formularauthentifizierung (C#)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie das Attribut [Authorize] verwenden, um bestimmte Seiten in Ihrer MVC-Anwendung mit dem Kennwort zu schützen. Sie erfahren, wie Sie das Websiteverwaltungstool zum Erstellen und Verwalten von Benutzern und Rollen verwenden. Außerdem erfahren Sie, wie Sie konfigurieren, wo Benutzerkonto- und Rolleninformationen gespeichert werden.

In diesem Tutorial wird erläutert, wie Sie die Formularauthentifizierung verwenden können, um die Ansichten in Ihren ASP.NET MVC-Anwendungen kennwortgeschützt zu schützen. Sie erfahren, wie Sie das Websiteverwaltungstool zum Erstellen von Benutzern und Rollen verwenden. Außerdem erfahren Sie, wie Sie verhindern können, dass nicht autorisierte Benutzer Controlleraktionen aufrufen. Schließlich erfahren Sie, wie Sie konfigurieren, wo Benutzernamen und Kennwörter gespeichert werden.

#### <a name="using-the-web-site-administration-tool"></a>Verwenden des Websiteverwaltungstools

Bevor wir etwas anderes tun, sollten wir damit beginnen, einige Benutzer und Rollen zu erstellen. Die einfachste Möglichkeit zum Erstellen neuer Benutzer und Rollen besteht darin, das Visual Studio 2008 Website Administration Tool zu nutzen. Sie können dieses Tool starten, indem Sie die Menüoption **Projekt, ASP.NET Konfiguration auswählen.** Alternativ können Sie das Websiteverwaltungstool starten, indem Sie auf das (etwas beängstigende) Symbol des Hammers klicken, der auf die Welt trifft, die oben im Projektmappen-Explorer-Fenster angezeigt wird (siehe Abbildung 1).

**Abbildung 1: Starten des Websiteverwaltungstools**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

Im Websiteverwaltungstool erstellen Sie neue Benutzer und Rollen, indem Sie die Registerkarte Sicherheit auswählen. Klicken Sie auf den Link **Benutzer erstellen,** um einen neuen Benutzer namens Stephen zu erstellen (siehe Abbildung 2). Geben Sie dem Stephen-Benutzer ein beliebiges Kennwort (z. B. *geheim*).

**Abbildung 2: Erstellen eines neuen Benutzers**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

Sie erstellen neue Rollen, indem Sie zunächst Rollen aktivieren und eine oder mehrere Rollen definieren. Aktivieren Sie Rollen, indem Sie auf den Link **Rollen aktivieren** klicken. Erstellen Sie als Nächstes eine Rolle mit dem Namen *Administratoren,* indem Sie auf den Link **Rollen erstellen oder verwalten** klicken (siehe Abbildung 3).

**Abbildung 3 : Erstellen einer neuen Rolle**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

Erstellen Sie schließlich einen neuen Benutzer mit dem Namen Sally, und ordnen Sie Sally der Rolle Administratoren zu, indem Sie beim Erstellen von Sally auf den Link Benutzer erstellen klicken und Administratoren auswählen (siehe Abbildung 4).

**Abbildung 4: Hinzufügen eines Benutzers zu einer Rolle**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

Wenn alles gesagt und getan ist, sollten Sie zwei neue Benutzer namens Stephen und Sally haben. Sie sollten auch über eine neue Rolle mit dem Namen Administratoren verfügen. Sally ist Mitglied der Rolle "Administratoren" und Stephen nicht.

#### <a name="requiring-authorization"></a>Erforderliche Autorisierung

Sie können verlangen, dass ein Benutzer authentifiziert wird, bevor der Benutzer eine Controlleraktion aufruft, indem Sie der Aktion das Attribut [Authorize] hinzufügen. Sie können das Attribut [Authorize] auf eine einzelne Controlleraktion oder auf eine gesamte Controllerklasse anwenden.

Beispielsweise macht der Controller in Listing 1 eine Aktion mit dem Namen CompanySecrets(verfügbar. Da diese Aktion mit dem Attribut [Authorize] versehen ist, kann diese Aktion nur aufgerufen werden, wenn ein Benutzer authentifiziert ist.

**Auflisten 1 – Controllers-HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

Wenn Sie die Aktion CompanySecrets() aufrufen, indem Sie die URL /Home/CompanySecrets in der Adressleiste Ihres Browsers eingeben, und Sie kein authentifizierter Benutzer sind, werden Sie automatisch zur Anmeldeansicht weitergeleitet (siehe Abbildung 5).

**Abbildung 5 – Die Login-Ansicht**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

Sie können die Anmeldeansicht verwenden, um Ihren Benutzernamen und Ihr Kennwort einzugeben. Wenn Sie kein registrierter Benutzer sind, können Sie auf den **Link Register** klicken, um zur Registeransicht zu navigieren (siehe Abbildung 6). Sie können die Ansicht Register verwenden, um ein neues Benutzerkonto zu erstellen.

**Abbildung 6 – Die Registeransicht**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

Nachdem Sie sich erfolgreich angemeldet haben, sehen Sie die Ansicht "Unternehmensgeheimnisse" (siehe Abbildung 7). Standardmäßig werden Sie weiterhin angemeldet, bis Sie Ihr Browserfenster schließen.

**Abbildung 7 – Die Ansicht "Unternehmensgeheimnisse"**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Autorisieren nach Benutzername oder Benutzerrolle

Sie können das Attribut [Authorize] verwenden, um den Zugriff auf eine Controlleraktion auf eine bestimmte Gruppe von Benutzern oder eine bestimmte Gruppe von Benutzerrollen zu beschränken. Der geänderte Home-Controller in Liste 2 enthält beispielsweise zwei neue Aktionen mit den Namen StephenSecrets() und AdministratorSecrets().

**Auflisten 2 – Controllers-HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

Nur ein Benutzer mit dem Benutzernamen Stephen kann die StephenSecrets()-Aktion aufrufen. Alle anderen Benutzer werden zur Anmeldeansicht umgeleitet. Die Users-Eigenschaft akzeptiert eine durch Kommas getrennte Liste von Benutzernamen.

Nur Benutzer in der Rolle Administratoren können die AdministratorSecrets()-Aktion aufrufen. Da Sally beispielsweise Mitglied der Gruppe Administratoren ist, kann sie die Aktion AdministratorSecrets() aufrufen. Alle anderen Benutzer werden zur Anmeldeansicht umgeleitet. Die Roles-Eigenschaft akzeptiert eine durch Kommas getrennte Liste von Rollennamen.

#### <a name="configuring-authentication"></a>Konfigurieren der Authentifizierung

An diesem Punkt fragen Sie sich möglicherweise, wo die Benutzerkonto- und Rolleninformationen gespeichert werden. Standardmäßig werden die Informationen in einer SQL Express-Datenbank mit dem Namen ASPNETDB.mdf gespeichert, die sich im App-Datenordner\_Ihrer MVC-Anwendung befindet. Diese Datenbank wird automatisch vom ASP.NET Framework generiert, wenn Sie mit der Mitgliedschaft beginnen.

Um die ASPNETDB.mdf-Datenbank im Projektmappen-Explorer-Fenster anzuzeigen, müssen Sie zunächst die Menüoption Projekt, Alle Dateien anzeigen auswählen.

Die Verwendung der SQL Express-Standarddatenbank ist beim Entwickeln einer Anwendung in Ordnung. Wahrscheinlich möchten Sie jedoch nicht die Standarddatenbank ASPNETDB.mdf für eine Produktionsanwendung verwenden. In diesem Fall können Sie die Speicherung von Benutzerkontoinformationen ändern, indem Sie die folgenden beiden Schritte ausführen:

1. Hinzufügen der Application Services-Datenbankobjekte zu Ihrer Produktionsdatenbank - Ändern der Anwendungsverbindungszeichenfolge, um auf die Produktionsdatenbank zu verweisen

Der erste Schritt besteht darin, der Produktionsdatenbank alle erforderlichen Datenbankobjekte (Tabellen und gespeicherte Prozeduren) hinzuzufügen. Die einfachste Möglichkeit, diese Objekte einer neuen Datenbank hinzuzufügen, besteht darin, die Vorteile des ASP.NET SQL Server-Setup-Assistenten zu nutzen (siehe Abbildung 8). Sie können dieses Tool starten, indem Sie die Visual Studio 2008-Eingabeaufforderung aus der Microsoft Visual Studio 2008-Programmgruppe öffnen und den folgenden Befehl über die Eingabeaufforderung ausführen:

aspnet-Regsql\_

**Abbildung 8 : Der ASP.NET SQL Server-Setup-Assistenten**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

Mit dem ASP.NET SQL Server-Installations-Assistenten können Sie eine SQL Server-Datenbank in Ihrem Netzwerk auswählen und alle Datenbankobjekte installieren, die für die ASP.NET Anwendungsdienste erforderlich sind. Der Datenbankserver muss sich nicht auf dem lokalen Computer befinden.

> [!NOTE] 
> 
> Wenn Sie den ASP.NET SQL Server-Setup-Assistenten nicht verwenden möchten, finden Sie SQL-Skripts zum Hinzufügen der Anwendungsdienstdatenbankobjekte im folgenden Ordner:
> 
> > C:-Windows-Microsoft.NET-Framework-V2.0.50727

Nachdem Sie die erforderlichen Datenbankobjekte erstellt haben, müssen Sie die von Ihrer MVC-Anwendung verwendete Datenbankverbindung ändern. Ändern Sie die ApplicationServices-Verbindungszeichenfolge in Ihrer Webkonfigurationsdatei (web.config), sodass sie auf die Produktionsdatenbank verweist. Beispielsweise verweist die geänderte Verbindung in Listing 3 auf eine Datenbank mit dem Namen MyProductionDB (die ursprüngliche ApplicationServices-Verbindungszeichenfolge wurde auskommentiert).

**Auflistung 3 – Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Konfigurieren von Datenbankberechtigungen

Wenn Sie Integrated Security zum Herstellen einer Verbindung mit Ihrer Datenbank verwenden, müssen Sie das richtige Windows-Benutzerkonto als Anmeldung zu Ihrer Datenbank hinzufügen. Das richtige Konto hängt davon ab, ob Sie den ASP.NET Development Server oder Internet Information Services als Webserver verwenden. Das richtige Benutzerkonto hängt auch von Ihrem Betriebssystem ab.

Wenn Sie den ASP.NET Development Server (den von Visual Studio verwendeten Standardwebserver) verwenden, wird die Anwendung im Kontext Ihres Windows-Benutzerkontos ausgeführt. In diesem Fall müssen Sie Ihr Windows-Benutzerkonto als Datenbankserveranmeldung hinzufügen.

Wenn Sie Internetinformationsdienste verwenden, müssen Sie alternativ entweder das ASPNET-Konto oder das NT AUTHORITY/NETWORK SERVICE-Konto als Datenbankserver-Anmeldung hinzufügen. Wenn Sie Windows XP verwenden, fügen Sie das ASPNET-Konto als Anmeldung zu Ihrer Datenbank hinzu. Wenn Sie ein neueres Betriebssystem wie Windows Vista oder Windows Server 2008 verwenden, fügen Sie das NT AUTHORITY/NETWORK SERVICE-Konto als Datenbankanmeldung hinzu.

Sie können Ihrer Datenbank mithilfe von Microsoft SQL Server Management Studio ein neues Benutzerkonto hinzufügen (siehe Abbildung 9).

**Abbildung 9: Erstellen einer neuen Microsoft SQL Server-Anmeldung**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

Nachdem Sie die erforderliche Anmeldung erstellt haben, müssen Sie die Anmeldung einem Datenbankbenutzer mit den richtigen Datenbankrollen zuordnen. Doppelklicken Sie auf die Anmeldung und wählen Sie die Registerkarte Benutzerzuordnung. Wählen Sie eine oder mehrere Datenbankrollen für Anwendungsdienste aus. Um benutzerauthentifizieren zu können, müssen Sie\_beispielsweise\_die Datenbankrolle aspnet Membership BasicAccess aktivieren. Um neue Benutzer zu erstellen, müssen Sie\_die\_Datenbankrolle aspnet-Mitgliedschaft FullAccess aktivieren (siehe Abbildung 10).

**Abbildung 10 – Hinzufügen von Application Services-Datenbankrollen**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie gelernt, wie Sie die Formularauthentifizierung beim Erstellen einer ASP.NET MVC-Anwendung verwenden. Zuerst haben Sie gelernt, wie Sie neue Benutzer und Rollen erstellen, indem Sie das Websiteverwaltungstool nutzen. Als Nächstes haben Sie gelernt, wie Sie das Attribut [Autorisieren] verwenden, um zu verhindern, dass nicht autorisierte Benutzer Controlleraktionen aufrufen. Schließlich haben Sie gelernt, wie Sie Ihre MVC-Anwendung so konfigurieren, dass Benutzer- und Rolleninformationen in einer Produktionsdatenbank gespeichert werden.

> [!div class="step-by-step"]
> [Nächste](authenticating-users-with-windows-authentication-cs.md)
