---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Mitgliedschaft | Microsoft Docs
author: rick-anderson
description: ASP.NET Mitgliedschaft baut auf dem Erfolg des Formularauthentifizierungsmodells von ASP.NET 1.x auf. ASP.NET Forms-Authentifizierung bietet eine bequeme Möglichkeit,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543768"
---
# <a name="membership"></a>Mitgliedschaft

von [Microsoft](https://github.com/microsoft)

> ASP.NET Mitgliedschaft baut auf dem Erfolg des Formularauthentifizierungsmodells von ASP.NET 1.x auf. ASP.NET Forms-Authentifizierung bietet eine bequeme Möglichkeit, ein Anmeldeformular in Ihre ASP.NET Anwendung zu integrieren und Benutzer anhand einer Datenbank oder eines anderen Datenspeichers zu validieren.

ASP.NET Mitgliedschaft baut auf dem Erfolg des Formularauthentifizierungsmodells von ASP.NET 1.x auf. ASP.NET Forms-Authentifizierung bietet eine bequeme Möglichkeit, ein Anmeldeformular in Ihre ASP.NET Anwendung zu integrieren und Benutzer anhand einer Datenbank oder eines anderen Datenspeichers zu validieren. Die Member der FormsAuthentication-Klasse ermöglichen es, Cookies für die Authentifizierung zu verarbeiten, nach einem gültigen Login zu suchen, einen Benutzer auszuloggen usw. Das Implementieren der Formularauthentifizierung in einer ASP.NET 1.x-Anwendung kann jedoch eine angemessene Menge an Code erfordern.

Die Mitgliedschaft in ASP.NET 2.0 ist ein wichtiger Fortschritt gegenüber der Verwendung der Formularauthentifizierung allein. (Die Mitgliedschaft ist am robuststen, wenn sie mit der Formularauthentifizierung gekoppelt ist, aber die Verwendung der Formularauthentifizierung ist nicht erforderlich.) Wie Sie bald sehen werden, können Sie ASP.NET Mitgliedschaft und die Login-Steuerelemente in ASP.NET 2.0 verwenden, um ein leistungsfähiges Mitgliedschaftssystem zu implementieren, ohne viel Code zu schreiben.

## <a name="implementing-membership-in-aspnet-20"></a>Implementieren der Mitgliedschaft in ASP.NET 2.0

Die Mitgliedschaft wird durch die folgenden vier Schritte implementiert. Beachten Sie, dass es viele Unterschritte gibt, die beteiligt sind, sowie optionale Konfiguration, die ebenfalls implementiert werden können. Diese Schritte sollen das große Ganze der Konfiguration der Mitgliedschaft veranschaulichen.

1. Erstellen Sie Ihre Mitgliedschaftsdatenbank (wenn SQL Server als Mitgliedschaftsspeicher verwendet wird).)
2. Geben Sie die Mitgliedschaftsoptionen in den Anwendungskonfigurationsdateien an. (Die Mitgliedschaft ist standardmäßig aktiviert.)
3. Bestimmen Sie den Typ des Mitgliedschaftsspeichers, den Sie verwenden möchten. Folgende Optionen sind verfügbar: 

    - Microsoft SQL Server (Version 7.0 oder höher)
    - Active Directory-Speicher
    - Benutzerdefinierter Mitgliedschaftsanbieter
4. Konfigurieren Sie die Anwendung für ASP.NET Forms-Authentifizierung. Auch hier ist die Mitgliedschaft so konzipiert, dass die Formularauthentifizierung genutzt wird, die Verwendung der Formularauthentifizierung ist jedoch nicht erforderlich.
5. Definieren Sie Benutzerkonten für die Mitgliedschaft, und konfigurieren Sie ggf. Rollen.

## <a name="creating-the-membership-database"></a>Erstellen der Mitgliedschaftsdatenbank

Wenn Sie SQL Server 7.0 oder höher als Mitgliedschaftsspeicher verwenden,\_können Sie das Dienstprogramm aspnet regsql (das am einfachsten über die Befehlsaufforderung Visual Studio .NET 2005 verfügbar ist) verwenden, um die Datenbank zu konfigurieren. Das Dienstprogramm\_aspnet regsql kann als Eingabeaufforderungstool oder über einen GUI-Assistenten verwendet werden. Die Assistentenmethode ist die einfachste Möglichkeit, ihre Datenbank zu konfigurieren. Um auf den Assistenten zuzugreifen, führen Sie einfach den folgenden Befehl aus:

`aspnet_regsql W`

Sobald Sie diesen Befehl ausführen, wird Ihnen der ASP.NET SQL Server-Setup-Assistenten angezeigt, wie unten gezeigt.

![](membership/_static/image1.jpg)

**Abbildung 1**

Der ASP.NET SQL Server-Setup-Assistenten erstellt die Website in der Instanz, die Sie im Assistenten angeben. ASP.NET verwendet jedoch die Verbindungszeichenfolge in der Datei machine.config, um eine Verbindung mit der Datenbank herzustellen. Standardmäßig weist diese Verbindungszeichenfolge auf eine SQL Server 2005-Instanz hin. Wenn Sie also eine SQL Server 2000- oder SQL Server 7.0-Instanz verwenden, müssen Sie die Verbindungszeichenfolge in der Datei machine.config ändern. Diese Verbindungszeichenfolge kann hier gefunden werden:

[!code-xml[Main](membership/samples/sample1.xml)]

Wenn Sie die Verbindungszeichenfolge nicht ändern, erhalten Sie ASP.NET leider keinen beschreibenden Fehler. Es wird sich einfach weiterhin beschweren und sagen, dass Sie die Datenbank nicht erstellt haben. Im obigen Fall habe ich die Verbindungszeichenfolge so geändert, dass sie auf meine lokale SQL Server 2000-Instanz verweisen soll.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Angeben der Konfiguration und Hinzufügen von Benutzern und Rollen

Der nächste Schritt beim Konfigurieren der Mitgliedschaft besteht darin, die erforderlichen Informationen zur Datei web.config der Anwendung hinzuzufügen. In ASP.NET 1.x war das Ändern der Datei web.config manchmal schwierig, da lowerCamelCase verwendet wurde und Intellisense fehlte. Visual Studio .NET 2005 erleichtert die Aufgabe mit Intellisense für Konfigurationsdateien erheblich, aber ASP.NET 2.0 geht noch einen Schritt weiter, indem eine Weboberfläche zum Bearbeiten von Konfigurationsdateien bereitgestellt wird.

Sie können die Weboberfläche starten, indem Sie auf der Symbolleiste des Projektmappen-Explorers auf die Schaltfläche ASP.NET Konfiguration klicken. Sie können die Weboberfläche auch über Pop-ups starten, die angezeigt werden, wenn Login-Steuerelemente eingefügt werden.

![](membership/_static/image2.jpg)

**Abbildung 2**

Dadurch wird das unten gezeigte ASP.NET Websiteverwaltungstool gestartet. Die ASP.NET Websiteadministration ist eine Schnittstelle mit vier Registerkarten, die die Verwaltung von Anwendungseinstellungen erleichtert. Die folgenden Registerkarten sind verfügbar:

- **Start**
- **Sicherheit** Konfigurieren Sie Benutzer, Rollen und Zugriffe.
- **Anwendung** Konfigurieren Sie die Anwendungseinstellungen.
- **Anbieter** Konfigurieren und testen Sie Ihren Anwendungsmitgliedschaftsanbieter.

Mit dem Websiteverwaltungstool können Sie ganz einfach neue Benutzer erstellen, neue Rollen erstellen und Benutzer und Rollen verwalten. Diese Fähigkeit ist in der Windows-Benutzeroberfläche nicht verfügbar. Mit der Windows-Schnittstelle können Sie autorisierungseinstellungen einfach definieren und Anbieter hinzufügen, löschen und verwalten, funktionen, die nicht im Websiteverwaltungstool vorhanden sind.

Um die Windows-Schnittstelle zu starten, öffnen Sie das Snap-In "Internetinformationsdienste", klicken Sie mit der rechten Maustaste auf Ihre Anwendung, und wählen Sie Eigenschaften aus. Klicken Sie auf die Registerkarte ASP.NET, und klicken Sie dann auf die Schaltfläche Konfiguration bearbeiten. (Die Anwendung muss unter ASP.NET 2.0 ausgeführt werden, damit die Schaltfläche Konfiguration bearbeiten aktiviert werden kann. Sie können die ASP.NET Version auch im ASP.NET-Dialog konfigurieren.) Das Dialogfeld ASP.NET Konfigurationseinstellungen wird wie unten angezeigt.

![](membership/_static/image3.jpg)

**Abbildung 3**

Auf der Registerkarte Allgemein werden Verbindungszeichenfolgen und Anwendungseinstellungen aufgelistet. Alle Einstellungen in Kursivschrift werden in einer übergeordneten Konfigurationsdatei definiert (entweder die machine.config oder eine web.config auf einer höheren Ebene), und Einstellungen, die nicht kursiv sind, stammen aus der Anwendungskonfigurationsdatei. Wenn eine Einstellung auf Anwendungsebene hinzugefügt, entfernt oder bearbeitet wird, fügt ASP.NET die Einstellung auf Anwendungsebene web.config hinzu, entfernt oder bearbeitet wird, anstatt die Einstellung aus der Konfigurationsdatei zu entfernen, aus der sie geerbt wird.

Die Registerkarte Authentifizierung wird unten angezeigt. Hier konfigurieren Sie Ihre Mitgliedschaftseinstellungen. Formularauthentifizierungseinstellungen, Mitgliedschaftsanbieter und Rollenanbieter können hier konfiguriert werden.

![](membership/_static/image4.jpg)

**Abbildung 4**

## <a name="implementing-membership-in-your-application"></a>Implementieren der Mitgliedschaft in Ihrer Bewerbung

Die einfachste Möglichkeit, ASP.NET 2.0-Mitgliedschaft in Ihrer Anwendung zu implementieren, besteht darin, die bereitgestellten Anmeldesteuerelemente zu verwenden. Mit dieser Methode können Sie die Grundlagen der ASP.NET 2.0-Mitgliedschaft implementieren, ohne codezuschreiben.

Die folgenden Anmeldesteuerelemente sind in ASP.NET 2.0 verfügbar:

## <a name="login-control"></a>Login-Steuerung

Das Login-Steuerelement stellt eine Schnittstelle für personen bereit, sich bei Ihrem Mitgliedschaftssystem anzumelden. Es bietet Ihnen einen Benutzernamen und Passwort Textfeld und eine Login-Taste. Viele andere allgemeine Funktionen wie ein Link zur Registrierung für Personen, die dies noch nicht getan haben, ein Kontrollkästchen, das es dem Benutzer ermöglicht, sich automatisch bei nachfolgenden Besuchen anzumelden, ein Link für eine Passworterinnerung usw. Alle Funktionen des Login-Steuerelements sind über die Eigenschaften des Steuerelements anpassbar.

In ASP.NET 1.x mussten Entwickler eine angemessene Menge an Code schreiben, um eine Suche durchzuführen, wenn die Formularauthentifizierung verwendet wurde. Mit ASP.NET 2.0-Mitgliedschaft können Sie Benutzer validieren, ohne codezuschreiben. ASP.NET wird automatisch die Suche des Benutzers für Sie tun. (Wenn Sie das Login-Steuerelement verwenden, ohne ASP.NET-Mitgliedschaft zu verwenden, können Sie die **OnAuthenticate-Methode** verwenden, um den Benutzer zu überprüfen.)

## <a name="loginview-control"></a>LoginView-Steuerelement

Das LoginView-Steuerelement ist ein Vorlagensteuerelement, das standardmäßig zwei Vorlagen bereitstellt. AnonymousTemplate und Die LoggedInTemplate. Die angezeigte Vorlage hängt davon ab, ob der Benutzer bei Ihrem Mitgliedschaftssystem angemeldet ist oder nicht. Dieses Steuerelement wird in der Regel verwendet, um ein Login-Steuerelement anzuzeigen, wenn sich ein Benutzer noch nicht angemeldet hat, und ein LoginStatus-Steuerelement und/oder andere Anmeldesteuerelemente, wenn sich der Benutzer angemeldet hat. Wenn Sie die Rollenverwaltung in Ihrer ASP.NET Anwendung verwenden, kann das LoginView-Steuerelement eine bestimmte Vorlage basierend auf der Benutzerrolle anzeigen. (Weitere Informationen zu ASP.NET Rollenmanagement werden später behandelt.)

## <a name="passwordrecovery-control"></a>PasswordRecovery-Steuerung

Das PasswordRecovery-Steuerelement ermöglicht es Benutzern, eine E-Mail mit ihrem aktuellen Kennwort zu erhalten oder ihr Kennwort zurückzusetzen. Klartext und verschlüsselte Passwörter können wiederhergestellt und per E-Mail an Benutzer gesendet werden. Wenn das Kennwort gehasht wird, kann es nicht wiederhergestellt werden. Stattdessen muss der Benutzer ein Kennwort zurücksetzen.

## <a name="loginstatus-control"></a>LoginStatus-Steuerung

Das LoginStatus-Steuerelement wird verwendet, um Benutzern, die nicht angemeldet sind, eine Anmeldeanzeige und Benutzern, die derzeit angemeldet sind, eine Anmeldeanzeige anzuzeigen. Die Request.IsAuthenticated-Eigenschaft wird verwendet, um zu bestimmen, welcher Indikator angezeigt werden soll. Der Indikator, der vom LoginStatus-Steuerelement angezeigt wird, kann Text (implementiert über die **LoginText-** und **LogoutText-Eigenschaften)** oder Bilder (implementiert über die **LoginImageUrl-** und **LogoutImageUrl-Eigenschaften)** sein.

Wenn sich ein Benutzer über das LoginStatus-Steuerelement abmeldet, wird er oder sie an die URL umgeleitet, die von der **LogoutPageUrl-Eigenschaft** angegeben wird. Wenn diese Eigenschaft nicht festgelegt ist, wird die aktuelle Seite aktualisiert. Da die Website wahrscheinlich durch die Formularauthentifizierung geschützt ist, wird der Benutzer durch die Aktualisierung der aktuellen Seite auf die Anmeldeseite für die Website umgeleitet.

## <a name="loginname-control"></a>LoginName-Steuerung

Das LoginName-Steuerelement zeigt den Benutzernamen des Benutzers an, der derzeit bei der Website angemeldet ist.

## <a name="createuserwizard-control"></a>CreateUserWizard-Steuerelement

Das CreateUserWizard-Steuerelement bietet Benutzern eine bequeme Möglichkeit, sich für Ihr Mitgliedschaftssystem zu registrieren. Sie können Schritte (als Eine Sammlung von WizardSteps implementiert) über die unten gezeigte Schnittstelle hinzufügen.

![](membership/_static/image5.jpg)

**Abbildung 5**

Der CreateUserWizard ist ein Vorlagensteuerelement, das von der Wizard-Klasse abstammt und die folgenden Vorlagen bereitstellt:

- **HeaderTemplate** Diese Vorlage steuert die Darstellung der Kopfzeile des Assistenten.
- **SidebarTemplate** Diese Vorlage steuert die Darstellung der Seitenleiste des Assistenten.
- **StartNavigationTemplate** Diese Vorlage steuert die Darstellung der Navigation des Assistenten im Startschritt.
- **StepNavigationTemplate** Diese Vorlage steuert die Darstellung des Navigationsbereichs, wenn sie sich nicht im Start- oder Endschritt befindet.
- **FinishNavigationTemplate** Diese Vorlage steuert die Darstellung des Navigationsbereichs im Zielschritt.

Darüber hinaus erstellt ASP.NET für jeden Schritt, den Sie dem Assistenten hinzufügen, eine benutzerdefinierte Vorlage, die sowohl eine ContentTemplate- als auch eine CustomNavigationTemplate für diesen Schritt enthält. Ausführliche Informationen zum Anpassen des CreateUserWizard finden Sie in der Dokumentation VS.NET 2005:

## <a name="changepassword-control"></a>ChangePassword-Steuerung

Mit dem ChangePassword-Steuerelement können Benutzer ihr Kennwort ändern. Wenn die DisplayUserName-Eigenschaft true ist (standardmäßig ist sie false), kann der Benutzer sein Kennwort ändern, wenn er nicht angemeldet ist. Wenn der Benutzer bereits angemeldet *ist* und die DisplayUserName-Eigenschaft true ist, kann der Benutzer das Kennwort eines anderen Benutzers ändern, der nicht angemeldet ist, vorausgesetzt, er kennt die Benutzer-ID dieses Benutzers.

Wenn Benutzer Kennwörter ändern können sollen, ohne sich anmelden zu müssen, müssen Sie sicherstellen, dass die Seite, auf der das ChangePassword-Steuerelement angezeigt wird, anonymen Zugriff ermöglicht. Natürlich müssen Benutzer ihr altes Passwort angeben, um ihr Passwort zu ändern.

## <a name="role-management"></a>Rollenverwaltung

Mit der Rollenverwaltung können Sie Benutzern einer bestimmten Rolle zuweisen und dann den Zugriff auf bestimmte Dateien oder Ordner basierend auf dieser Rolle einschränken. Die Rollenverwaltung stellt auch eine API bereit, mit der Sie die Rolle einer Person programmgesteuert oder alle Benutzer in einer bestimmten Rolle bestimmen und entsprechend reagieren können.

Rollenverwaltung ist keine Anforderung in ASP.NET Mitgliedschaft, noch ist die Mitgliedschaft eine Voraussetzung für die Verwendung der Rollenverwaltung. Jedoch, die beiden ergänzen sich nett und es ist wahrscheinlich, dass Entwickler sie in Verbindung miteinander verwenden.

Um die Rollenverwaltung in Ihrer Anwendung zu aktivieren, nehmen Sie die folgende Änderung in Ihrer web.config-Datei vor:

[!code-xml[Main](membership/samples/sample2.xml)]

Wenn das **CacheRolesInCookie-Attribut** auf true festgelegt ist, ASP.NET eine Benutzerrollenmitgliedschaft in einem Cookie auf dem Client zwischenspeichert. Dadurch können Rollensuchen ohne Aufrufe in den RoleProvider erfolgen. Bei der Verwendung dieses Attributs sollten Entwickler darauf achten, dass das **cookieProtection-Attribut** auf Alle festgelegt ist. (Dies ist die Standardeinstellung.) Dadurch wird sichergestellt, dass die Cookie-Daten verschlüsselt sind und trägt dazu bei, dass der Cookie-Inhalt nicht geändert wurde. Rollen können mit dem Websiteverwaltungstool hinzugefügt werden. Es ermöglicht Ihnen, Rollen einfach zu definieren, den Zugriff auf Teile der Website basierend auf diesen Rollen zu konfigurieren und Benutzer Rollen zuzuweisen.

![](membership/_static/image6.jpg)

**Abbildung 6**

Wie oben gezeigt, können neue Rollen hinzugefügt werden, indem Sie einfach den Namen der Rolle eingeben und dann auf Rolle hinzufügen klicken. Vorhandene Rollen können verwaltet oder gelöscht werden, indem Sie auf den entsprechenden Link in der Liste der vorhandenen Rollen klicken.

Wenn Sie eine Rolle verwalten, können Sie Benutzer hinzufügen oder entfernen, wie unten gezeigt.

![](membership/_static/image7.jpg)

**Abbildung 7**

Wenn Sie das Kontrollkästchen "Benutzer ist in Rolle" aktivieren, können Sie problemlos einen Benutzer zu einer bestimmten Rolle hinzufügen. ASP.NET aktualisiert Ihre Mitgliedschaftsdatenbank automatisch mit den entsprechenden Einträgen. Sie sollten auch Zugriffsregeln für Ihre Anwendung konfigurieren. ASP.NET 1.x-Entwickler sind damit &lt;über&gt; das Autorisierungselement in der Datei web.config vertraut, und diese Option ist in ASP.NET 2.0 weiterhin verfügbar. Es ist jedoch einfacher, Zugriffsregeln mithilfe des Websiteverwaltungstools zu verwalten, wie unten gezeigt.

![](membership/_static/image8.jpg)

**Abbildung 8**

In diesem Fall wird der Verwaltungsordner hervorgehoben (es ist schwer zu sehen, da das Tool ihn hellgrau hervorhebt), und der Rolle Administratoren wurde Zugriff gewährt. Alle anderen Benutzer werden abgelehnt. Sie können auf das Kopfsymbol klicken, um eine Regel auszuwählen, und dann die Schaltflächen Nach oben und Nach unten verwenden, um die Regeln anzuordnen. Wie beim &lt;ASP.NET&gt; Autorisierungselement werden Regeln in der Reihenfolge verarbeitet, in der sie angezeigt werden. Mit anderen Worten, wenn die Reihenfolge der Regeln in der obigen Aufnahme umgekehrt würde, hätte niemand Zugriff auf den Administrationsordner, da die erste Regel, auf die ASP.NET stoßen würde, die Regel wäre, die jedem den Ordner verweigert.

ASP.NET 2.0 fügt dem Ordner, für den Sie eine Zugriffsregel angeben, eine web.config-Datei hinzu. Zugriffsregeln können über die Konfigurationsdatei oder über das Websiteadministrationstool bearbeitet werden. Mit anderen Worten, das Website-Verwaltungstool ist einfach eine Schnittstelle, über die die Konfigurationsdatei in einer benutzerfreundlichen Umgebung bearbeitet werden kann.

## <a name="using-roles-in-code"></a>Verwenden von Rollen im Code

Die API für die Rollenverwaltung hat sich seit Version 1.x nicht geändert. Die **IsInRole-Methode** wird verwendet, um zu bestimmen, ob ein Benutzer in einer bestimmten Rolle ist.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET erstellt auch eine RolePrincipal-Instanz als Mitglied des aktuellen Kontexts. Das RolePrincipal-Objekt kann verwendet werden, um alle Rollen abzuerlangen, zu denen der Benutzer gehört:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>Verwenden von RoleGroups mit dem LoginView-Steuerelement

Nachdem Sie nun über ein Verständnis der Rollenverwaltung und -mitgliedschaft verfügen, können Sie kurz erläutern, wie das LoginView-Steuerelement diese Funktion in ASP.NET 2.0 nutzt. Wie bereits erwähnt, ist das LoginView-Steuerelement ein Vorlagensteuerelement, das standardmäßig zwei Vorlagen enthält. AnonymousTemplate und Die LoggedInTemplate. Im Dialogfeld LoginView Tasks befindet sich ein Link (siehe unten), mit dem Sie RoleGroups bearbeiten können.

![](membership/_static/image9.jpg)

**Abbildung 9**

Jedes RoleGroup-Objekt enthält ein Array von Zeichenfolgen, das definiert, auf welche Rollen RoleGroup angewendet wird. Um dem LoginView-Steuerelement eine neue RoleGroup hinzuzufügen, klicken Sie auf den Link Rollengruppen bearbeiten. In der Abbildung oben sehen Sie, dass ich eine neue RoleGroup für Administratoren hinzugefügt habe. Wenn Ich diese RoleGroup (RoleGroup[0]) aus der Dropdownliste Ansichten auswänge, kann ich eine Vorlage konfigurieren, die nur Mitgliedern der Rolle Administratoren angezeigt wird. In der folgenden Abbildung habe ich eine neue RoleGroup hinzugefügt, die für Mitglieder der Rolle "Vertrieb" und der Verteilungsrolle gilt. Dadurch wird der Dropdownliste Ansichten im Dialogfeld LoginView-Aufgaben eine zweite RoleGroup hinzugefügt, und alle, die dieser Vorlage hinzugefügt werden, werden von jedem Benutzer in der Rolle "Vertrieb" oder "Verteilung" angezeigt.

![](membership/_static/image10.jpg)

**Abbildung 10**

## <a name="overriding-the-existing-membership-provider"></a>Überschreiben des vorhandenen Mitgliedschaftsanbieters

Es gibt mehrere Möglichkeiten, wie Sie die Funktionalität ASP.NET-Mitgliedschaft erweitern können. Zunächst können Sie natürlich die vorhandene Funktionalität der SqlMembershipProvider-Klasse ändern, indem Sie von ihr erben und ihre Methoden überschreiben. Wenn Sie z. B. beim Erstellen von Benutzern eigene Funktionen implementieren möchten, können Sie eine eigene Klasse erstellen, die von SqlMembershipProvider wie folgt erbt:

[!code-csharp[Main](membership/samples/sample5.cs)]

Wenn Sie hingegen einen eigenen Anbieter erstellen möchten (z. B. zum Speichern Ihrer Mitgliedsinformationen in einer Access-Datenbank), können Sie einen eigenen Anbieter erstellen.

## <a name="creating-your-own-membership-provider"></a>Erstellen eines eigenen Mitgliedschaftsanbieters

Um einen eigenen Mitgliedschaftsanbieter zu erstellen, müssen Sie zunächst eine Klasse erstellen, die von der MembershipProvider-Klasse erbt. Wenn Sie VB.NET verwenden, fügt Visual Studio 2005 die Stubs für alle Methoden hinzu, die Sie überschreiben müssen. Wenn Sie c- verwenden, ist es an Ihnen, die Stubs hinzuzufügen.

Sie müssen Folgendes überschreiben:

- ApplicationName-Eigenschaft
- ChangePassword-Funktion
- ChangePasswordQuestionAndAnswer-Funktion
- CreateUser-Funktion
- DeleteUser-Funktion
- EnablePasswordReset-Eigenschaft
- EnablePasswordRetrieval-Eigenschaft
- FindUsersByEmail-Funktion
- FindUsersByName-Funktion
- GetAllUsers-Funktion
- GetNumberOfUsersOnline-Funktion
- GetPassword-Funktion
- GetUser-Funktion
- GetUserNameByEmail-Funktion
- MaxInvalidPasswordAttempts-Eigenschaft
- MinRequiredNonAlphanumericCharacters-Eigenschaft
- MinRequiredPasswordLength-Eigenschaft
- PasswordAttemptWindow-Eigenschaft
- PasswordFormat-Eigenschaft
- PasswordStrengthRegularExpression-Eigenschaft
- RequiresQuestionAndAnswer-Eigenschaft
- RequiresUniqueEmail-Eigenschaft
- ResetPassword-Funktion
- Entsperren der Benutzerfunktion
- UpdateUser-Funktion
- ValidateUser-Funktion

Das ist eine ziemliche Liste, die als C-Entwickler implementiert werden soll. Möglicherweise ist es einfacher, die Klasse in VB.NET ohne Implementierung zu erstellen und dann .NET Reflector oder ein ähnliches Tool zu verwenden, um den Code in C zu konvertieren.

Die Verbindungszeichenfolge und andere Eigenschaften sollten in der Initialize-Methode auf ihre Standardwerte festgelegt werden. (Die Initialize-Methode wird ausgelöst, wenn der Anbieter zur Laufzeit geladen wird.) Der zweite Parameter für die Initialize-Methode ist vom Typ System.Collections.Specialized.NameValueCollection und ist ein Verweis auf das &lt;Add-Element,&gt; das Ihrem benutzerdefinierten Anbieter in der Datei web.config zugeordnet ist. Dieser Eintrag sieht wie folgt aus:

[!code-xml[Main](membership/samples/sample6.xml)]

Hier ist ein Beispiel für die Initialize-Methode.

[!code-csharp[Main](membership/samples/sample7.cs)]

Um den Benutzer beim Absenden des Anmeldeformulars zu überprüfen, müssen Sie die ValidateUser-Methode verwenden. Diese Methode wird ausgelöst, wenn der Benutzer auf die Anmeldeschaltfläche im Login-Steuerelement klickt. Sie platzieren Ihren Code, der die Benutzersuche ausführt, in dieser Methode.

Wie Sie sehen können, ist das Schreiben Ihres eigenen Mitgliedschaftsanbieters nicht schwierig und ermöglicht es Ihnen, diese leistungsstarke Funktionalität von ASP.NET 2.0 zu erweitern.
