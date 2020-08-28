---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: Validieren von Benutzer Anmelde Informationen anhand des Mitgliedschafts Benutzerspeicher (c#) | Microsoft-Dokumentation
author: rick-anderson
description: In diesem Tutorial wird erläutert, wie Sie die Anmelde Informationen eines Benutzers anhand der programmgesteuerten Mittel und des Anmeldungs Steuer Elements überprüfen.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: fd50f4e63c75cf77eb21629d0c11a859da6b357d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045233"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>Überprüfen der Anmeldeinformationen anhand des Mitgliedschaftsbenutzerspeichers (C#)

von [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Code herunterladen](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) oder [PDF herunterladen](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> In diesem Tutorial wird erläutert, wie Sie die Anmelde Informationen eines Benutzers anhand der programmgesteuerten Mittel und des Anmeldungs Steuer Elements anhand des Mitgliedschafts Benutzerspeicher überprüfen. Wir sehen uns auch an, wie die Darstellung und das Verhalten des Anmeldungs Steuer Elements angepasst werden.

## <a name="introduction"></a>Einführung

Im <a id="Tutorial05"></a> [vorherigen Tutorial](creating-user-accounts-cs.md) haben wir uns mit dem Erstellen eines neuen Benutzerkontos im Mitgliedschafts Framework beschäftigt. Wir haben uns zunächst mit dem programmgesteuerten Erstellen von Benutzerkonten über die `Membership` -Methode der Klasse beschäftigt `CreateUser` und dann mit dem websteuer Element CreateUserWizard untersucht. Auf der Anmeldeseite werden jedoch derzeit die angegebenen Anmelde Informationen anhand einer hart codierten Liste von Benutzernamen-und Kenn Wortpaaren überprüft. Wir müssen die Logik der Anmeldeseite aktualisieren, damit die Anmelde Informationen im Benutzerspeicher des Mitgliedschafts Frameworks überprüft werden.

Ähnlich wie beim Erstellen von Benutzerkonten können Anmelde Informationen Programm gesteuert oder deklarativ überprüft werden. Die Mitgliedschafts-API enthält eine Methode zum programmgesteuerten Überprüfen der Anmelde Informationen eines Benutzers für den Benutzerspeicher. Und ASP.net wird mit dem Login-websteuer Element ausgeliefert, das eine Benutzeroberfläche mit Textfeldern für den Benutzernamen und das Kennwort und eine Schaltfläche zum Anmelden rendert.

In diesem Tutorial wird erläutert, wie Sie die Anmelde Informationen eines Benutzers anhand der programmgesteuerten Mittel und des Anmeldungs Steuer Elements anhand des Mitgliedschafts Benutzerspeicher überprüfen. Wir sehen uns auch an, wie die Darstellung und das Verhalten des Anmeldungs Steuer Elements angepasst werden. Legen Sie direkt los.

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>Schritt 1: Überprüfen der Anmelde Informationen anhand des Mitgliedschafts Benutzerspeicher

Bei Websites, die die Formular Authentifizierung verwenden, meldet sich ein Benutzer an der Website an, indem er eine Anmeldeseite eingibt und seine Anmelde Informationen eingibt. Diese Anmelde Informationen werden dann mit dem Benutzerspeicher verglichen. Wenn Sie gültig sind, wird dem Benutzer ein Formular Authentifizierungs Ticket erteilt, bei dem es sich um ein Sicherheits Token handelt, das die Identität und Authentizität des Besuchers angibt.

Verwenden Sie die `Membership` - [ `ValidateUser` Methode](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)der-Klasse, um einen Benutzer mit dem Mitgliedschafts Framework zu validieren. Die- `ValidateUser` Methode nimmt zwei Eingabeparameter an: *`username`* und *`password`* gibt einen booleschen Wert zurück, der angibt, ob die Anmelde Informationen gültig sind. Wie bei der- `CreateUser` Methode, die wir im vorherigen Tutorial überprüft haben, delegiert die- `ValidateUser` Methode die tatsächliche Validierung an den konfigurierten Mitgliedschafts Anbieter.

`SqlMembershipProvider`Überprüft die angegebenen Anmelde Informationen, indem er das angegebene Kennwort des Benutzers über die `aspnet_Membership_GetPasswordWithFormat` gespeicherte Prozedur erhält. Beachten Sie, dass die Kenn `SqlMembershipProvider` Wörter von Benutzern in einem von drei Formaten speichert: Clear, verschlüsselt oder Hash. Die `aspnet_Membership_GetPasswordWithFormat` gespeicherte Prozedur gibt das Kennwort im RAW-Format zurück. Bei verschlüsselten oder Hash Kennwörtern transformiert der den `SqlMembershipProvider` *`password`* in die Methode übergebenen Wert `ValidateUser` in den entsprechenden verschlüsselten oder Hashwert und vergleicht ihn dann mit dem, was von der Datenbank zurückgegeben wurde. Wenn das in der Datenbank gespeicherte Kennwort mit dem vom Benutzer eingegebenen formatierten Kennwort übereinstimmt, sind die Anmelde Informationen gültig.

Aktualisieren Sie die Anmeldeseite (~/ `Login.aspx` ), damit die angegebenen Anmelde Informationen anhand des Mitgliedschafts Framework-Benutzer Stores überprüft werden. Wir haben diese Anmeldeseite im Abschnitt <a id="Tutorial02"></a> [*Übersicht über die Formular Authentifizierung*](../introduction/an-overview-of-forms-authentication-cs.md) erstellt und eine Schnittstelle mit zwei Textfeldern für Benutzername und Kennwort, ein Kontrollkästchen für die Erinnerung und eine Anmelde Schaltfläche erstellt (siehe Abbildung 1). Der Code überprüft die eingegebenen Anmelde Informationen anhand einer hart codierten Liste von Benutzernamen-und Kenn Wortpaaren (Scott/Password, jisun/Password und SAM/Password). Im Tutorial zur <a id="Tutorial03"></a> [*Konfiguration von Formular Authentifizierung und erweiterten Themen*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) haben wir den Code der Anmeldeseite aktualisiert, um zusätzliche Informationen in der Eigenschaft des Formular Authentifizierungs Tickets zu speichern `UserData` .

[![Die Benutzeroberfläche der Anmeldeseite enthält zwei Textfelder, eine CheckBoxList und eine Schaltfläche.](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**Abbildung 1**: die Benutzeroberfläche der Anmeldeseite enthält zwei Textfelder, eine CheckBoxList und eine Schaltfläche ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)).

Die Benutzeroberfläche der Anmeldeseite kann unverändert bleiben, aber wir müssen den Ereignishandler der Anmelde Schaltfläche durch Code ersetzen, der `Click` den Benutzer mit dem Mitgliedschafts Framework-Benutzerspeicher überprüft. Aktualisieren Sie den Ereignishandler so, dass der zugehörige Code wie folgt aussieht:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

Dieser Code ist erstaunlich einfach. Wir beginnen mit dem Aufrufen der- `Membership.ValidateUser` Methode und übergeben den angegebenen Benutzernamen und das zugehörige Kennwort. Wenn diese Methode true zurückgibt, wird der Benutzer über die `FormsAuthentication` RedirectFromLoginPage-Methode der Klasse bei der Site angemeldet. (Wie in der <a id="Tutorial2"></a> In der Übersicht über das Tutorial zur [*Formular Authentifizierung*](../introduction/an-overview-of-forms-authentication-cs.md) wird das `FormsAuthentication.RedirectFromLoginPage` Formular Authentifizierungs Ticket erstellt, und der Benutzer wird dann zur entsprechenden Seite umgeleitet.) Wenn die Anmelde Informationen ungültig sind, wird die `InvalidCredentialsMessage` Bezeichnung jedoch angezeigt, und der Benutzer wird darüber informiert, dass der Benutzername oder das Kennwort falsch war.

Das ist schon alles!

Um zu testen, ob die Anmeldeseite erwartungsgemäß funktioniert, versuchen Sie, sich mit einem der Benutzerkonten anzumelden, die Sie im vorherigen Tutorial erstellt haben. Wenn Sie noch kein Konto erstellt haben, erstellen Sie ein Konto auf der `~/Membership/CreatingUserAccounts.aspx` Seite.

> [!NOTE]
> Wenn der Benutzer die Anmelde Informationen eingibt und das Formular der Anmeldeseite sendet, werden die Anmelde Informationen, einschließlich Ihres Kennworts, über das Internet als nur- *Text*an den Webserver übertragen. Dies bedeutet, dass der Benutzername und das Kennwort von Hacker-Ermittlung des Netzwerk Datenverkehrs angezeigt werden. Um dies zu verhindern, ist es von entscheidender Bedeutung, den Netzwerk Datenverkehr mithilfe von [SSL (Secure Socket Layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)zu verschlüsseln. Dadurch wird sichergestellt, dass die Anmelde Informationen (und das HTML-Markup der gesamten Seite) ab dem Zeitpunkt, an dem Sie den Browser verlassen, verschlüsselt werden, bis Sie vom Webserver empfangen werden.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Wie das Mitgliedschafts Framework ungültige Anmeldeversuche behandelt

Wenn ein Besucher die Anmeldeseite erreicht und seine Anmelde Informationen übermittelt, sendet der Browser eine HTTP-Anforderung an die Anmeldeseite. Wenn die Anmelde Informationen gültig sind, enthält die HTTP-Antwort das Authentifizierungs Ticket in einem Cookie. Aus diesem Grund könnte ein Hacker, der versucht, in ihren Standort zu unterbrechen, ein Programm erstellen, das HTTP-Anforderungen mit einem gültigen Benutzernamen und einer Vermutung am Kennwort an die Anmeldeseite sendet. Wenn die Kenn Wort Schätzung richtig ist, gibt die Anmeldeseite das Authentifizierungs Ticket Cookie zurück. zu diesem Zeitpunkt weiß das Programm, dass es auf ein gültiges Paar aus Benutzername und Kennwort gestoßen ist. Durch Brute-Force kann ein solches Programm möglicherweise auf das Kennwort eines Benutzers stoßen, insbesondere, wenn das Kennwort schwach ist.

Um solche Brute-Force-Angriffe zu vermeiden, sperrt das Mitgliedschafts Framework einen Benutzer, wenn innerhalb eines bestimmten Zeitraums eine bestimmte Anzahl von erfolglosen Anmelde versuchen vorliegt. Die genauen Parameter können mit den folgenden beiden Konfigurationseinstellungen für den Mitgliedschafts Anbieter konfiguriert werden:

- `maxInvalidPasswordAttempts` : gibt an, wie viele ungültige Kenn Wort Versuche für den Benutzer innerhalb des Zeitraums zulässig sind, bevor das Konto gesperrt wird. Der Standardwert ist 5.
- `passwordAttemptWindow` : gibt den Zeitraum in Minuten an, in dem die angegebene Anzahl von ungültigen Anmelde versuchen bewirkt, dass das Konto gesperrt wird. Der Standardwert ist 10.

Wenn ein Benutzer gesperrt wurde, kann er sich erst anmelden, wenn ein Administrator Ihr Konto entsperrt. Wenn ein Benutzer gesperrt ist, gibt die `ValidateUser` Methode *immer* zurück `false` , auch wenn gültige Anmelde Informationen angegeben werden. Wenngleich dieses Verhalten die Wahrscheinlichkeit verringert, dass ein Hacker über Brute-Force-Methoden in Ihre Website unterteilt wird, kann es dazu führen, dass ein gültiger Benutzer gesperrt wird, der das Kennwort vergessen hat oder versehentlich die Feststell Sperre oder einen ungültigen Typisierungs Tag aufweist.

Leider gibt es kein integriertes Tool zum Entsperren eines Benutzerkontos. Zum Entsperren eines Kontos können Sie die Datenbank direkt ändern: Ändern Sie das `IsLockedOut` Feld in der `aspnet_Membership` Tabelle für das entsprechende Benutzerkonto, oder erstellen Sie eine webbasierte Schnittstelle, die ausgesperrte Konten mit Optionen zum Entsperren auflistet. In einem zukünftigen Tutorial wird das Erstellen von Verwaltungs Schnittstellen für das Ausführen allgemeiner Benutzerkonten-und Rollen bezogener Aufgaben untersucht.

> [!NOTE]
> Ein Nachteil der- `ValidateUser` Methode besteht darin, dass, wenn die angegebenen Anmelde Informationen ungültig sind, keine Erklärung dazu bereitgestellt wird. Die Anmelde Informationen sind möglicherweise ungültig, weil im Benutzerspeicher kein entsprechendes Benutzername/Kennwort-Paar vorhanden ist oder der Benutzer noch nicht genehmigt wurde oder weil der Benutzer gesperrt wurde. In Schritt 4 sehen Sie, wie eine ausführlichere Meldung an den Benutzer angezeigt wird, wenn der Anmeldeversuch fehlschlägt.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>Schritt 2: Erfassen von Anmelde Informationen über das Anmeldungs-websteuer Element

Das [Anmeldungs-websteuer](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) Element rendert eine Standardbenutzer Oberfläche, die dem von uns in der Übersicht über die <a id="SKM5"></a> [*Formular Authentifizierung*](../introduction/an-overview-of-forms-authentication-cs.md) erstellten Tutorial sehr ähnlich ist. Mit dem Login-Steuerelement können wir die Schnittstelle erstellen, um die Anmelde Informationen des Besuchers zu erfassen. Außerdem signiert das Anmeldungs Steuerelement den Benutzer automatisch (vorausgesetzt, die übermittelten Anmelde Informationen sind gültig), sodass wir keinen Code schreiben müssen.

Wir aktualisieren `Login.aspx` die manuell erstellte Schnittstelle und den Code durch ein Login-Steuerelement. Entfernen Sie zunächst das vorhandene Markup und den Code in `Login.aspx` . Sie können Sie ganz einfach löschen oder einfach kommentieren. Um deklaratives Markup auszukommentieren, müssen Sie es mit den Trennzeichen und umschließen `<%--` `--%>` . Sie können diese Trennzeichen manuell eingeben, oder Sie können, wie in Abbildung 2 gezeigt, den Text auswählen, der auskommentiert werden soll, und dann auf der Symbolleiste auf das Symbol ausgewählte Zeilen auskommentieren klicken. Entsprechend können Sie das Symbol Auskommentieren der ausgewählten Zeilen verwenden, um den ausgewählten Code in der Code Behind-Klasse auszukommentieren.

[![Kommentieren Sie das vorhandene deklarative Markup und den Quellcode in "Login. aspx" aus.](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**Abbildung 2**: auskommentieren des vorhandenen deklarativen Markups und des Quellcodes in `Login.aspx` ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png))

> [!NOTE]
> Das Symbol auskommentieren des ausgewählten Zeilen Symbols ist nicht verfügbar, wenn Sie das deklarative Markup in Visual Studio 2005 anzeigen. Wenn Sie nicht Visual Studio 2008 verwenden, müssen Sie die Trennzeichen und manuell hinzufügen `<%--` `--%>` .

Ziehen Sie als nächstes ein Anmelde Steuerelement aus der Toolbox auf die Seite, und legen Sie die zugehörige- `ID` Eigenschaft auf fest `myLogin` . An diesem Punkt sollte der Bildschirm in etwa wie in Abbildung 3 aussehen. Beachten Sie, dass die Standardschnittstelle des Anmeldungs Steuer Elements Textfeld-Steuerelemente für den Benutzernamen und das Kennwort, das nächste Kontrollkästchen Speichern und eine Anmelde Schaltfläche enthält. Es gibt auch Steuer `RequiredFieldValidator` Elemente für die beiden Textfelder.

[![Fügen Sie der Seite ein Anmelde Steuerelement hinzu.](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**Abbildung 3**: Hinzufügen eines Anmelde Steuer Elements zur Seite ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png))

Und wir sind fertig! Wenn Sie auf die Schaltfläche Anmelden des Anmeldungs Steuer Elements klicken, wird ein Postback ausgeführt, und das Login-Steuerelement ruft die- `Membership.ValidateUser` Methode auf und übergibt den eingegebenen Benutzernamen und das Kennwort. Wenn die Anmelde Informationen ungültig sind, zeigt das Anmeldungs Steuerelement eine solche Meldung an. Wenn die Anmelde Informationen jedoch gültig sind, erstellt das Anmelde Steuerelement das Formular Authentifizierungs Ticket und leitet den Benutzer an die entsprechende Seite weiter.

Das-Anmelde Steuerelement verwendet vier Faktoren, um die entsprechende Seite zu bestimmen, an die der Benutzer nach erfolgreicher Anmeldung umgeleitet werden soll:

- Gibt an, ob sich das Anmelde Steuerelement auf der Anmeldeseite befindet, wie durch `loginUrl` Festlegen von in der Konfiguration der Formular Authentifizierung definiert. der Standardwert dieser Einstellung lautet: `Login.aspx`
- Das vorhanden sein eines `ReturnUrl` QueryString-Parameters
- Der Wert der [ `DestinationUrl` Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) des Anmeldungs Steuer Elements.
- Der `defaultUrl` in den Konfigurationseinstellungen der Formular Authentifizierung angegebene Wert. der Standardwert dieser Einstellung ist `Default.aspx`

Abbildung 4 zeigt, wie das Anmeldungs Steuerelement diese vier Parameter verwendet, um die entsprechende Seiten Entscheidung zu treffen.

[![Fügen Sie der Seite ein Anmelde Steuerelement hinzu.](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**Abbildung 4**: Hinzufügen eines Anmelde Steuer Elements zur Seite ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png))

Nehmen Sie sich einen Moment Zeit, um das Anmeldungs Steuerelement zu testen, indem Sie die Website über einen Browser besuchen und sich als vorhandener Benutzer im Mitgliedschafts Framework anmelden.

Die gerenderte Schnittstelle des Anmelde Steuer Elements ist hochgradig konfigurierbar. Es gibt eine Reihe von Eigenschaften, die ihre Darstellung beeinflussen. Darüber hinaus kann das Login-Steuerelement in eine Vorlage konvertiert werden, um das Layout der Benutzeroberflächen Elemente genau zu steuern. Im weiteren Verlauf dieses Schritts wird untersucht, wie die Darstellung und das Layout angepasst werden.

### <a name="customizing-the-login-controls-appearance"></a>Anpassen der Darstellung des Anmeldungs Steuer Elements

Die Standard Eigenschafts Einstellungen des Login-Steuer Elements stellen eine Benutzeroberfläche mit einem Titel (anmelden), Textfeld-und Bezeichnungs Steuerelement für die Eingaben für Benutzername und Kennwort, das nächste Kontrollkästchen Speichern und eine Anmelde Schaltfläche dar. Der Anschein ist, dass diese Elemente über die zahlreichen Eigenschaften des Anmeldungs Steuer Elements konfiguriert werden können. Darüber hinaus können zusätzliche Benutzeroberflächen Elemente, wie z. b. ein Link zu einer Seite, um ein neues Benutzerkonto zu erstellen, hinzugefügt werden, indem eine Eigenschaft oder zwei festgelegt wird.

Wir beschäftigen uns ein paar Zeit, um die Darstellung unseres Login-Steuer Elements zu übernehmen. Da `Login.aspx` auf der Seite bereits Text am oberen Rand der Seite angezeigt wird, die Anmelde Informationen meldet, ist der Titel des Anmeldungs Steuer Elements überflüssig. Löschen Sie daher den [ `TitleText` Eigenschafts](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) Wert, um den Titel des Anmeldungs Steuer Elements zu entfernen.

Benutzer Name: und Kennwort: Bezeichnungen Links von zwei TextBox-Steuerelementen können über die [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) [ `PasswordLabelText` Eigenschaften](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)und angepasst werden. Ändern Sie den Benutzernamen: Bezeichnung in "Benutzername:". Die Formatvorlagen und TextBox-Stile können über die-Eigenschaft bzw. die-Eigenschaft konfiguriert werden [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) . [ `TextBoxStyle` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)

Die Text-Eigenschaft für das nächste Mal speichern kann über das Anmeldungs Steuerelement festgelegt werden, und der aktivierte [`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx) Standardzustand kann über den [`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) (standardmäßig false) konfiguriert werden. Legen Sie die-Eigenschaft auf "true" fest, `RememberMeSet` damit das Kontrollkästchen "merken Sie sich das nächste Mal" standardmäßig aktiviert wird.

Das Login-Steuerelement verfügt über zwei Eigenschaften zum Anpassen des Layouts der Steuerelemente der Benutzeroberfläche. Der [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) gibt an, ob der Benutzername: und das Kennwort: Bezeichnungen auf der linken Seite der entsprechenden Textfelder (Standard) oder darüber angezeigt werden. Der [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) gibt an, ob sich die Eingaben für Benutzername und Kennwort vertikal (eins oberhalb der anderen) oder horizontal befinden. Diese beiden Eigenschaften werden auf die Standardeinstellungen festgelegt, aber ich empfehle Ihnen, diese beiden Eigenschaften auf Ihre nicht standardmäßigen Werte festzulegen, um den resultierenden Effekt anzuzeigen.

> [!NOTE]
> Im nächsten Abschnitt, in dem Sie das Layout des Anmeldungs Steuer Elements konfigurieren, betrachten wir die Verwendung von Vorlagen, um das genaue Layout der Benutzeroberflächen Elemente des layoutsteuer Elements zu definieren.

Schließen Sie die Eigenschafts Einstellungen des Anmeldungs Steuer Elements [`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) ein, indem Sie die [ `CreateUserUrl` Eigenschaften](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) und auf noch nicht registriert festlegen Erstellen Sie ein Konto. und `~/Membership/CreatingUserAccounts.aspx` bzw. Dadurch wird der-Schnittstelle des Anmelde Steuer Elements ein Link hinzugefügt, der auf die Seite verweist, die wir im <a id="SKM6"></a> [vorherigen Tutorial](creating-user-accounts-cs.md)erstellt haben. Die Eigenschaften und-Eigenschaften und-Eigenschaften des Anmelde Steuer Elements [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) [ `HelpPageUrl` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) funktionieren auf die gleiche Weise wie das Rendern von Links zu einer Hilfeseite und einer Kenn Wort Wiederherstellungs Seite. [ `PasswordRecoveryUrl` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)

Nachdem Sie diese Eigenschaften geändert haben, sollten das deklarative Markup und die Darstellung Ihres Anmeldungs Steuer Elements in etwa wie in Abbildung 5 dargestellt aussehen.

[![Die Eigenschaften Werte des Anmeldungs Steuer Elements legen seine Darstellung](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**Abbildung 5**: die Eigenschaftswerte des Anmeldungs Steuer Elements legen seine Darstellung[vor (Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png))

### <a name="configuring-the-login-controls-layout"></a>Konfigurieren des Layouts des Anmeldungs Steuer Elements

Die Standardbenutzer Oberfläche des Anmeldungs-websteuer Elements legt die Schnittstelle in einem HTML-Code fest `<table>` . Aber was ist, wenn wir eine präzisere Kontrolle über die gerenderte Ausgabe benötigen? Vielleicht möchten wir den `<table>` durch eine Reihe von `<div>` Tags ersetzen. Oder was geschieht, wenn die Anwendung zusätzliche Anmelde Informationen für die Authentifizierung erfordert? Viele Finanz Websites erfordern beispielsweise, dass Benutzer nicht nur einen Benutzernamen und ein Kennwort angeben, sondern auch eine persönliche Identifikationsnummer (PIN) oder andere identifizierende Informationen. Der Grund dafür ist, dass das Anmelde Steuerelement in eine Vorlage konvertiert werden kann, von der aus das deklarative Markup der Schnittstelle explizit definiert werden kann.

Wir müssen zwei Schritte durchführen, um das Anmeldungs Steuerelement zu aktualisieren, um zusätzliche Anmelde Informationen zu sammeln:

1. Aktualisieren Sie die-Schnittstelle des Anmelde Steuer Elements, um websteuer Elemente zum Erfassen der zusätzlichen Anmelde Informationen einzubeziehen.
2. Überschreiben Sie die interne Authentifizierungs Logik des Anmelde Steuer Elements so, dass ein Benutzer nur authentifiziert wird, wenn der Benutzername und das Kennwort gültig sind und die zusätzlichen Anmelde Informationen gültig sind.

Zum Ausführen der ersten Aufgabe müssen wir das Login-Steuerelement in eine Vorlage konvertieren und die erforderlichen websteuer Elemente hinzufügen. Wie bei der zweiten Aufgabe kann die Authentifizierungs Logik des Anmeldungs Steuer Elements ersetzt werden, indem ein Ereignishandler für das- [ `Authenticate` Ereignis](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)des-Steuer Elements erstellt wird.

Aktualisieren Sie das Anmelde Steuerelement, damit Benutzer Benutzername, Kennwort und e-Mail-Adresse eingeben und nur den Benutzer authentifizieren können, wenn die angegebene e-Mail-Adresse mit Ihrer e-Mail-Adresse in der Datei übereinstimmt. Zuerst muss die-Schnittstelle des Anmelde Steuer Elements in eine Vorlage konvertiert werden. Wählen Sie im Smarttag des Anmeldungs Steuer Elements die Option in Vorlage konvertieren aus.

[![Konvertieren des Anmelde Steuer Elements in eine Vorlage](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**Abbildung 6**: Konvertieren des Anmeldungs Steuer Elements in eine Vorlage ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png))

> [!NOTE]
> Wenn Sie das Anmeldungs Steuerelement auf seine vorab Vorlagen Version zurücksetzen möchten, klicken Sie auf den Link Zurücksetzen des Smarttags des-Steuer Elements.

Beim Umrechnen des Anmeldungs Steuer Elements in eine Vorlage wird dem `LayoutTemplate` deklarativen Markup des Steuer Elements ein hinzugefügt, wobei HTML-Elemente und websteuer Elemente die Benutzeroberfläche definieren. Wie in Abbildung 7 gezeigt, werden durch die Typumwandlung in eine Vorlage eine Reihe von Eigenschaften aus dem Eigenschaftenfenster entfernt, z. b., `TitleText` `CreateUserUrl` usw., da diese Eigenschaftswerte bei Verwendung einer Vorlage ignoriert werden.

[![Es sind weniger Eigenschaften verfügbar, wenn das Login-Steuerelement in eine Vorlage konvertiert wird.](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**Abbildung 7**: Es sind weniger Eigenschaften verfügbar, wenn das Anmelde Steuerelement in eine Vorlage konvertiert wird ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png))

Das HTML-Markup in `LayoutTemplate` kann bei Bedarf geändert werden. Ebenso können Sie neue websteuer Elemente zur Vorlage hinzufügen. Es ist jedoch wichtig, dass die wichtigsten websteuer Elemente des Anmelde Steuer Elements in der Vorlage verbleiben und die zugewiesenen Werte beibehalten werden `ID` . Entfernen oder benennen Sie insbesondere die `UserName` Textfelder oder nicht `Password` , das `RememberMe` Kontrollkästchen, die `LoginButton` Schaltfläche, die `FailureText` Bezeichnung oder die Steuer `RequiredFieldValidator` Elemente.

Um die e-Mail-Adresse des Besuchers zu erfassen, müssen wir der Vorlage ein Textfeld hinzufügen. Fügen Sie das folgende deklarative Markup zwischen der Tabellenzeile ( `<tr>` ), die das `Password` Textfeld enthält, und der Tabellenzeile mit dem Kontrollkästchen nächste Uhrzeit speichern hinzu:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

Nachdem Sie das `Email` Textfeld hinzugefügt haben, besuchen Sie die Seite über einen Browser. Wie in Abbildung 8 gezeigt, enthält die Benutzeroberfläche des Anmeldungs Steuer Elements jetzt ein drittes Textfeld.

[![Das Login-Steuerelement enthält jetzt ein Textfeld für die e-Mail-Adresse des Benutzers.](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**Abbildung 8**: das Anmeldungs Steuerelement enthält jetzt ein Textfeld für die e-Mail-Adresse des Benutzers ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png))

An diesem Punkt verwendet das Anmeldungs Steuerelement immer noch die- `Membership.ValidateUser` Methode, um die angegebenen Anmelde Informationen zu überprüfen. Dementsprechend hat der in das Textfeld eingegebene Wert `Email` keinen Einfluss darauf, ob sich der Benutzer anmelden kann. In Schritt 3 wird erläutert, wie Sie die Authentifizierungs Logik des Anmeldungs Steuer Elements überschreiben, sodass die Anmelde Informationen nur gültig sind, wenn der Benutzername und das Kennwort gültig sind und die angegebene e-Mail-Adresse mit der e-Mail-Adresse der Datei übereinstimmt.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>Schritt 3: Ändern der Authentifizierungs Logik des Anmeldungs Steuer Elements

Wenn ein Besucher Ihre Anmelde Informationen bereitstellt und auf die Schaltfläche Anmelden klickt, wird ein Postback durchlaufen, und das Anmelde Steuerelement durchläuft seinen Authentifizierungs Workflow. Der Workflow beginnt mit der Erhöhung des- [ `LoggingIn` Ereignisses](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx). Alle diesem Ereignis zugeordneten Ereignishandler können den Anmeldevorgang abbrechen, indem Sie die- `e.Cancel` Eigenschaft auf festlegen `true` .

Wenn der Anmeldevorgang nicht abgebrochen wird, wird der Workflow durch das Erhöhen des- [ `Authenticate` Ereignisses](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)fortgesetzt. Wenn ein Ereignishandler für das-Ereignis vorhanden ist `Authenticate` , muss bestimmt werden, ob die angegebenen Anmelde Informationen gültig sind oder nicht. Wenn kein Ereignishandler angegeben ist, verwendet das-Anmelde Steuerelement die- `Membership.ValidateUser` Methode, um die Gültigkeit der Anmelde Informationen zu bestimmen.

Wenn die angegebenen Anmelde Informationen gültig sind, wird das Formular Authentifizierungs Ticket erstellt, das- [ `LoggedIn` Ereignis](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) ausgelöst, und der Benutzer wird an die entsprechende Seite umgeleitet. Wenn die Anmelde Informationen jedoch als ungültig eingestuft werden, wird das- [ `LoginError` Ereignis](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) ausgelöst, und es wird eine Meldung angezeigt, die den Benutzer darüber informiert, dass Ihre Anmelde Informationen ungültig sind. Standardmäßig legt das Login-Steuerelement bei einem Fehler einfach die `FailureText` Text-Eigenschaft des Label-Steuer Elements auf eine Fehlermeldung fest (der Anmeldeversuch war nicht erfolgreich. Versuchen Sie es noch mal.) Wenn jedoch die- [ `FailureAction` Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) des Anmeldungs Steuer Elements auf festgelegt ist `RedirectToLoginPage` , gibt das Anmelde Steuerelement einen `Response.Redirect` an die Anmeldeseite aus, die den QueryString-Parameter anfügt `loginfailure=1` (was bewirkt, dass das Anmeldungs Steuerelement die Fehlermeldung anzeigt).

Abbildung 9 enthält ein Flussdiagramm des Authentifizierungs Workflows.

[![Der Authentifizierungs Workflow des Anmeldungs Steuer Elements.](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**Abbildung 9**: der Authentifizierungs Workflow des Anmeldungs Steuer Elements ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png))

> [!NOTE]
> Wenn Sie sich Fragen, ob Sie die Seite der Seite verwenden würden `FailureAction` `RedirectToLogin` , sehen Sie sich das folgende Szenario an. `Site.master`Zurzeit hat unsere Master Seite aktuell den Text "Hello, Stranger", der in der linken Spalte angezeigt wird, wenn Sie von einem anonymen Benutzer besucht wird. angenommen, Sie möchten den Text durch ein Anmelde Steuerelement ersetzen. Dadurch kann sich ein anonymer Benutzer über eine beliebige Seite auf der Website anmelden, anstatt ihn direkt auf die Anmeldeseite zu übernehmen. Wenn sich ein Benutzer jedoch nicht über das Anmelde Steuerelement anmelden konnte, das von der Master Seite gerendert wurde, ist es möglicherweise sinnvoll, Sie an die Anmeldeseite () umzuleiten, `Login.aspx` da diese Seite wahrscheinlich zusätzliche Anweisungen, Links und andere Hilfe enthält, wie z. b

### <a name="creating-theauthenticateevent-handler"></a>Erstellen des `Authenticate` Ereignis Handlers

Um die benutzerdefinierte Authentifizierungs Logik einzuschließen, müssen wir einen Ereignishandler für das-Ereignis des Anmeldungs Steuer Elements erstellen `Authenticate` . Durch das Erstellen eines Ereignis Handlers für das- `Authenticate` Ereignis wird die folgende Ereignishandlerdefinition generiert:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

Wie Sie sehen können, `Authenticate` wird dem Ereignishandler ein Objekt vom Typ [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) als zweiter Eingabeparameter übergeben. Die- `AuthenticateEventArgs` Klasse enthält eine boolesche Eigenschaft `Authenticated` mit dem Namen, die verwendet wird, um anzugeben, ob die angegebenen Anmelde Informationen gültig sind. Unsere Aufgabe ist es, hier Code zu schreiben, der bestimmt, ob die angegebenen Anmelde Informationen gültig sind, und die- `e.Authenticate` Eigenschaft entsprechend festzulegen.

### <a name="determining-and-validating-the-supplied-credentials"></a>Bestimmen und Validieren der angegebenen Anmelde Informationen

Verwenden Sie die Eigenschaften und des Anmeldungs Steuer Elements [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) , um die vom Benutzer eingegebenen Benutzernamen-und Kenn Wort Anmelde Informationen zu bestimmen. [ `Password` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) Um die in alle zusätzlichen websteuer Elemente eingegebenen Werte (z. b. das `Email` Textfeld, das wir im vorherigen Schritt hinzugefügt haben) zu bestimmen, rufen *`LoginControlID`* `.FindControl` Sie mithilfe von (" *`controlID`* ") einen programmatischen Verweis auf das websteuer Element in der Vorlage ab, dessen- `ID` Eigenschaft gleich ist *`controlID`* . Um beispielsweise einen Verweis auf das `Email` Textfeld zu erhalten, verwenden Sie den folgenden Code:

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

Um die Anmelde Informationen des Benutzers zu überprüfen, müssen wir zwei Schritte ausführen:

1. Sicherstellen, dass der angegebene Benutzername und das Kennwort gültig sind
2. Stellen Sie sicher, dass die eingegebene e-Mail-Adresse der e-Mail-Adresse für den Benutzer entspricht

Um die erste Überprüfung zu erreichen, können wir einfach die `Membership.ValidateUser` Methode wie in Schritt 1 verwenden. Bei der zweiten Überprüfung müssen wir die e-Mail-Adresse des Benutzers bestimmen, damit wir ihn mit der e-Mail-Adresse vergleichen können, die Sie in das TextBox-Steuerelement eingegeben haben. Um Informationen zu einem bestimmten Benutzer zu erhalten, verwenden Sie die `Membership` - [ `GetUser` Methode](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)der-Klasse.

Die- `GetUser` Methode verfügt über eine Reihe von über Ladungen. Wenn Sie ohne Angabe von Parametern verwendet wird, werden Informationen über den aktuell angemeldeten Benutzer zurückgegeben. Wenn Sie Informationen zu einem bestimmten Benutzer abrufen möchten, müssen Sie `GetUser` den Benutzernamen übergeben. In jedem Fall `GetUser` gibt ein- [ `MembershipUser` Objekt](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)zurück, das Eigenschaften wie `UserName` ,, `Email` `IsApproved` , `IsOnline` usw. enthält.

Der folgende Code implementiert diese beiden Überprüfungen. Wenn beide übergeben werden, dann `e.Authenticate` wird auf festgelegt `true` , andernfalls wird Sie zugewiesen `false` .

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

Wenn dieser Code vorhanden ist, versuchen Sie, sich als gültiger Benutzer anzumelden, und geben Sie den richtigen Benutzernamen, das Kennwort und die e-Mail-Adresse ein. Versuchen Sie es erneut, aber verwenden Sie dieses Mal absichtlich eine falsche e-Mail-Adresse (siehe Abbildung 10). Probieren Sie es schließlich mit einem nicht vorhandenen Benutzernamen ein drittes Mal aus. Im ersten Fall sollten Sie erfolgreich an der Website angemeldet sein, aber in den letzten beiden Fällen sollten Sie die Meldung ungültige Anmelde Informationen für das Anmelde Steuerelement sehen.

[![Tito kann sich bei der Angabe einer falschen e-Mail-Adresse nicht anmelden](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**Abbildung 10**: Tito kann sich nicht anmelden, wenn eine falsche e-Mail-Adresse bereitgestellt wird ([Klicken Sie, um das Bild in voller Größe](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)

> [!NOTE]
> Wie im Abschnitt Gewusst wie: Ausführen von ungültigen Anmelde versuchen durch das Mitgliedschafts Framework in Schritt 1, wenn die `Membership.ValidateUser` Methode aufgerufen wird und ungültige Anmelde Informationen weitergegeben werden, verfolgt Sie den ungültigen Anmeldeversuch nach und sperrt den Benutzer, wenn er einen bestimmten Schwellenwert von ungültigen versuchen innerhalb eines bestimmten Zeitfensters überschreitet. Da die benutzerdefinierte Authentifizierungs Logik die- `ValidateUser` Methode aufruft, wird durch ein falsches Kennwort für einen gültigen Benutzernamen der Wert für den ungültigen Anmeldeversuch erhöht. dieser Wert wird jedoch nicht inkrementiert, wenn der Benutzername und das Kennwort gültig sind, die e-Mail-Adresse aber falsch ist. Wahrscheinlich ist dieses Verhalten geeignet, da es unwahrscheinlich ist, dass ein Hacker den Benutzernamen und das Kennwort kennt, aber Brute-Force-Verfahren verwenden muss, um die e-Mail-Adresse des Benutzers zu bestimmen.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>Schritt 4: verbessern der Meldung zur ungültigen Anmelde Informationen des Anmelde Steuer Elements

Wenn ein Benutzer versucht, sich mit ungültigen Anmelde Informationen anzumelden, zeigt das Anmeldungs Steuerelement eine Meldung mit dem Hinweis an, dass der Anmeldeversuch nicht erfolgreich war. Insbesondere zeigt das Steuerelement die Meldung an, die von der- [ `FailureText` Eigenschaft](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)angegeben wird, die den Standardwert ihres Anmelde Versuchs nicht erfolgreich war. Versuchen Sie es erneut.

Beachten Sie, dass es viele Gründe gibt, warum die Anmelde Informationen eines Benutzers ungültig sein können:

- Der Benutzername darf nicht vorhanden sein.
- Der Benutzername ist vorhanden, aber das Kennwort ist ungültig.
- Der Benutzername und das Kennwort sind gültig, aber der Benutzer ist noch nicht genehmigt.
- Der Benutzername und das Kennwort sind gültig, aber der Benutzer ist gesperrt (wahrscheinlich, weil er die Anzahl der ungültigen Anmeldeversuche innerhalb des angegebenen Zeitraums überschritten hat).

Möglicherweise gibt es auch andere Gründe, wenn Sie benutzerdefinierte Authentifizierungs Logik verwenden. Beispielsweise können mit dem Code, den wir in Schritt 3 geschrieben haben, der Benutzername und das Kennwort gültig sein, die e-Mail-Adresse ist jedoch möglicherweise falsch.

Unabhängig davon, warum die Anmelde Informationen ungültig sind, wird im Anmelde Steuerelement dieselbe Fehlermeldung angezeigt. Dieses fehlende Feedback kann für einen Benutzer verwirrend sein, dessen Konto noch nicht genehmigt wurde oder der gesperrt wurde. Mit etwas Arbeit können wir jedoch festlegen, dass das Anmeldungs Steuerelement eine geeignetere Meldung anzeigt.

Wenn ein Benutzer versucht, sich mit ungültigen Anmelde Informationen anzumelden, löst das-Anmelde Steuerelement sein `LoginError` Ereignis aus. Erstellen Sie einen Ereignishandler für dieses Ereignis, und fügen Sie den folgenden Code hinzu:

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

Der obige Code beginnt mit dem Festlegen der-Eigenschaft des Anmeldungs Steuer Elements `FailureText` auf den Standardwert (Ihr Anmeldeversuch war nicht erfolgreich. Versuchen Sie es noch mal.) Anschließend wird überprüft, ob der angegebene Benutzername einem vorhandenen Benutzerkonto zugeordnet ist. Wenn dies der Fall ist, werden die `MembershipUser` -und-Eigenschaften des resultierenden Objekts `IsLockedOut` `IsApproved` angenommen, um zu bestimmen, ob das Konto gesperrt wurde oder noch nicht genehmigt wurde. In beiden Fällen wird die- `FailureText` Eigenschaft auf einen entsprechenden-Wert aktualisiert.

Um diesen Code zu testen, versuchen Sie absichtlich, sich als vorhandener Benutzer anzumelden, aber verwenden Sie ein falsches Kennwort. Führen Sie diese fünfmal in einer Zeile innerhalb eines Zeitraums von 10 Minuten aus, und das Konto wird gesperrt. Wie in Abbildung 11 dargestellt, treten bei nachfolgenden Anmelde versuchen immer Fehler auf (selbst mit dem richtigen Kennwort), aber jetzt wird die Beschreibung angezeigt, dass Ihr Konto aufgrund zu vieler ungültiger Anmeldeversuche gesperrt wurde. Wenden Sie sich an den Administrator, damit die Nachricht nicht gesperrt ist.

[![Tito hat zu viele ungültige Anmeldeversuche durchgeführt und wurde gesperrt.](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**Abbildung 11**: Tito hat zu viele ungültige Anmeldeversuche durchgeführt und wurde gesperrt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png))

## <a name="summary"></a>Zusammenfassung

Vor diesem Tutorial haben unsere Anmeldeseite die angegebenen Anmelde Informationen anhand einer hart codierten Liste von Benutzername/Kennwort-Paaren überprüft. In diesem Tutorial haben wir die Seite aktualisiert, um die Anmelde Informationen anhand des Mitgliedschafts Frameworks zu überprüfen. In Schritt 1 haben wir uns mit der programmgesteuerten Verwendung der `Membership.ValidateUser` Methode beschäftigt. In Schritt 2 haben wir unsere manuell erstellte Benutzeroberfläche und den Code durch das Login-Steuerelement ersetzt.

Das-Anmelde Steuerelement rendert eine Standard Anmelde Benutzeroberfläche und überprüft die Anmelde Informationen des Benutzers automatisch anhand des Mitgliedschafts-Frameworks. Außerdem signiert das Anmeldungs Steuerelement im Falle gültiger Anmelde Informationen den Benutzer über die Formular Authentifizierung. Kurz gesagt, ist eine voll funktionsfähige Anmelde Benutzer Funktionalität verfügbar, indem Sie einfach das Anmelde Steuerelement auf eine Seite ziehen, ohne zusätzliches deklaratives Markup oder Code. Außerdem ist das Anmeldungs Steuerelement hochgradig anpassbar und ermöglicht ein gutes Maß an Kontrolle über die gerenderte Benutzeroberfläche und die Authentifizierungs Logik.

An diesem Punkt können Besucher unserer Website ein neues Benutzerkonto erstellen und sich bei der Website anmelden, aber wir haben noch immer das Einschränken des Zugriffs auf Seiten basierend auf dem authentifizierten Benutzer untersucht. Zurzeit kann jeder Benutzer, der authentifiziert oder anonym ist, jede Seite auf unserer Website anzeigen. Neben dem Steuern des Zugriffs auf die Seiten unserer Website auf Benutzerbasis haben wir möglicherweise bestimmte Seiten, deren Funktionalität vom Benutzer abhängt. Im nächsten Tutorial wird erläutert, wie der Zugriff und die in-Page-Funktionalität basierend auf dem angemeldeten Benutzer eingeschränkt werden.

Fröhliche Programmierung!

### <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu den in diesem Tutorial behandelten Themen finden Sie in den folgenden Ressourcen:

- [Anzeigen benutzerdefinierter Nachrichten für gesperrten und nicht genehmigte Benutzer](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [Überprüfen der Mitgliedschaft, Rollen und Profile von ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Vorgehensweise: Erstellen einer ASP.net-Anmeldeseite](https://msdn.microsoft.com/library/ms178331.aspx)
- [Technische Dokumentation zum Anmelde Steuerelement](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Verwenden der Anmeldungs Steuerelemente](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>Zum Autor

Scott Mitchell, Autor mehrerer ASP/ASP. net-Bücher und Gründer von 4GuysFromRolla.com, hat seit 1998 mit Microsoft-Webtechnologien gearbeitet. Scott arbeitet als unabhängiger Berater, Ausbilder und Writer. Sein letztes Buch ist *[Sams Teach Yourself ASP.NET 2,0 in 24 Stunden](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott kann bei [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) oder über seinen Blog von erreicht werden [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Besonders vielen Dank

Diese tutorialreihe wurde von vielen hilfreichen Reviewern geprüft. Die führenden Reviewer für dieses Tutorial waren Teresa Murphy und Michael Olivero. Möchten Sie meine bevorstehenden MSDN-Artikel überprüfen? Wenn dies der Fall ist, löschen Sie die Zeile in [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [Zurück](creating-user-accounts-cs.md)
> [Weiter](user-based-authorization-cs.md)
