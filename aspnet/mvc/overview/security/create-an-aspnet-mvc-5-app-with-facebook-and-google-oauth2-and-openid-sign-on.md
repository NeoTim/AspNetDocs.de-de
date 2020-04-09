---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Erstellen Sie die MVC 5 App mit Facebook, Twitter, LinkedIn und Google OAuth2 Anmelden (C' ) | Microsoft Docs
author: Rick-Anderson
description: In diesem Tutorial erfahren Sie, wie Sie eine ASP.NET MVC 5-Webanwendung erstellen, mit der sich Benutzer mit OAuth 2.0 mit Anmeldeinformationen aus einer externen Authenti anmelden können...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675916"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Erstellen einer ASP.NET MVC 5-App mit Facebook, Twitter, LinkedIn und Google OAuth2-Anmeldung (C#)

von [Rick Anderson](https://twitter.com/RickAndMSFT)

> In diesem Tutorial erfahren Sie, wie Sie eine ASP.NET MVC 5-Webanwendung erstellen, mit der sich Benutzer mit [OAuth 2.0](http://oauth.net/2/) mit Anmeldeinformationen eines externen Authentifizierungsanbieters wie Facebook, Twitter, LinkedIn, Microsoft oder Google anmelden können. Der Einfachheit halber konzentriert sich dieses Tutorial auf die Arbeit mit Anmeldeinformationen von Facebook und Google.
> 
> Das Aktivieren dieser Anmeldeinformationen auf Ihren Websites bietet einen erheblichen Vorteil, da Millionen von Benutzern bereits Konten bei diesen externen Anbietern haben. Diese Benutzer sind möglicherweise eher geneigt, sich für Ihre Website anzumelden, wenn sie keine neuen Anmeldeinformationen erstellen und sich merken müssen.
> 
> Siehe auch [ASP.NET MVC 5-App mit SMS und E-Mail-Zwei-Faktor-Authentifizierung](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> Das Tutorial zeigt auch, wie Profildaten für den Benutzer hinzugefügt werden und wie die Mitgliedschafts-API zum Hinzufügen von Rollen verwendet wird. Dieses Tutorial wurde von [Rick Anderson](https://blogs.msdn.com/rickAndy) geschrieben [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Bitte folgen Sie mir auf Twitter: ).

<a id="start"></a>
## <a name="getting-started"></a>Erste Schritte

Beginnen Sie mit der Installation und Ausführung von [Visual Studio Express 2013 für Web](https://go.microsoft.com/fwlink/?LinkId=299058) oder Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566). Installieren Sie Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) oder höher. Hilfe zu Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo! und mehr finden Sie in diesem [Beispielprojekt](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Sie müssen Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) oder höher installieren, um Google OAuth 2 zu verwenden und lokal ohne SSL-Warnungen zu debuggen.

Klicken Sie auf der **Startseite** auf **Neues Projekt,** oder Sie können das Menü verwenden und **Datei**auswählen und dann **Neues Projekt**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Erstellen Ihrer ersten Anwendung

Klicken Sie auf **Neues Projekt**, und wählen Sie dann auf der linken Seite **Visual C-** aus, dann **Web,** und wählen Sie dann **ASP.NET Webanwendung**aus. Benennen Sie Ihr Projekt "MvcAuth" und klicken Sie dann auf **OK**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

Klicken Sie im Dialogfeld **Neues ASP.NET Projekt** auf **MVC**. Wenn es sich bei der Authentifizierung nicht um **einzelne Benutzerkonten handelt,** klicken Sie auf die Schaltfläche **Authentifizierung ändern,** und wählen Sie **Einzelne Benutzerkonten**aus. Durch Überprüfen von **Host in der Cloud**ist die App sehr einfach in Azure zu hosten.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Wenn Sie **Host in der Cloud**ausgewählt haben, schließen Sie das Dialogfeld Konfigurieren ab.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Verwenden Sie NuGet, um auf die neueste OWIN-Middleware zu aktualisieren

Verwenden Sie den NuGet-Paket-Manager, um die [OWIN-Middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)zu aktualisieren. Wählen Sie **Updates** im linken Menü aus. Sie können auf die Schaltfläche **Alle aktualisieren** klicken oder nur nach OWIN-Paketen suchen (siehe nächstes Bild):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

In der Folgenden Abbildung werden nur OWIN-Pakete angezeigt:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

Über die Package Manager Console (PMC) können Sie den `Update-Package` Befehl eingeben, mit dem alle Pakete aktualisiert werden.

Drücken Sie **F5** oder **Strg+F5,** um die Anwendung auszuführen. In der Abbildung unten ist die Portnummer 1234. Wenn Sie die Anwendung ausführen, wird eine andere Portnummer angezeigt.

Abhängig von der Größe Ihres Browserfensters müssen Sie möglicherweise auf das Navigationssymbol klicken, um die Links **Home**, **About**, **Kontakt**, **Registrieren** und **Anmelden** anzuzeigen.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Einrichten von SSL im Projekt

Um eine Verbindung mit Authentifizierungsanbietern wie Google und Facebook herzustellen, müssen Sie IIS-Express für die Verwendung von SSL einrichten. Es ist wichtig, SSL nach der Anmeldung zu verwenden und nicht auf HTTP zurückzuwerfen, Ihr Login-Cookie ist genauso geheim wie Ihr Benutzername und Passwort, und ohne SSL senden Sie es im Klartext über den Draht. Außerdem haben Sie sich bereits die Zeit genommen, den Handshake auszuführen und den Kanal zu sichern (was den Großteil dessen ausmacht, was HTTPS langsamer als HTTP macht), bevor die MVC-Pipeline ausgeführt wird, sodass die Umleitung zurück zu HTTP, nachdem Sie angemeldet sind, die aktuelle Anforderung oder zukünftige Anforderungen nicht viel schneller macht.

1. Klicken Sie im **Projektmappen-Explorer**auf das **MvcAuth-Projekt.**
2. Klicken Sie auf die F4-Taste, um die Projekteigenschaften anzuzeigen. Alternativ können Sie im **Menü Ansicht** **Eigenschaftenfenster**auswählen.
3. Ändern Sie **SSL Aktiviert** in True.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Kopieren Sie die SSL-URL `https://localhost:44300/` (sofern Sie keine anderen SSL-Projekte erstellt haben).
5. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das **MvcAuth-Projekt,** und wählen Sie **Eigenschaften**aus.
6. Wählen Sie die **Registerkarte Web** aus, und fügen Sie dann die SSL-URL in das Feld **Projekt-URL** ein. Speichern Sie die Datei (Ctl+S). Sie benötigen diese URL, um Facebook- und Google-Authentifizierungs-Apps zu konfigurieren.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Fügen Sie dem `Home` Controller das [RequireHttps-Attribut](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hinzu, damit alle Anforderungen HTTPS verwenden müssen. Ein sichererer Ansatz besteht darin, der Anwendung den [RequireHttps-Filter](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hinzuzufügen. Lesen Sie &quot;den Abschnitt Schützen Sie&quot; die Anwendung mit SSL und das Authorize-Attribut in meinem Tutorial [Erstellen Sie eine ASP.NET MVC-App mit auth und SQL DB, und stellen Sie sie in Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bereit. Ein Teil des Home-Controllers ist unten dargestellt.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Drücken Sie STRG+F5, um die Anwendung auszuführen. Wenn Sie das Zertifikat in der Vergangenheit installiert haben, können Sie den Rest dieses Abschnitts überspringen und zu [Erstellen einer Google-App für OAuth 2 und Verbinden der App mit dem Projekt springen.](#goog)Andernfalls befolgen Sie die Anweisungen, um dem selbstsignierten Zertifikat zu vertrauen, das IIS Express generiert hat.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Lesen Sie das Dialogfeld **Sicherheitswarnung,** und klicken Sie dann auf **Ja,** wenn Sie das Zertifikat installieren möchten, das localhost darstellt.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. Die Seite *Home* wird in IE angezeigt, und es gibt keine SSL-Warnungen.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome akzeptiert auch das Zertifikat und zeigt HTTPS-Inhalte ohne Warnung an. Firefox verwendet einen eigenen Zertifikatspeicher, sodass eine Warnung angezeigt wird. Für unsere Anwendung können Sie sicher auf **I Understand the Risks**klicken.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Erstellen einer Google-App für OAuth 2 und Verbinden der App mit dem Projekt

> [!WARNING]
> Aktuelle Google OAuth-Anweisungen finden Sie unter [Konfigurieren der Google-Authentifizierung in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).

1. Navigieren Sie zur [Google Developers Console](https://console.developers.google.com/).
2. Wenn Sie noch kein Projekt erstellt haben, wählen Sie **Anmeldeinformationen** auf der linken Registerkarte aus, und wählen Sie dann **Erstellen**aus.
3. Klicken Sie auf der linken Registerkarte auf **Anmeldeinformationen**.
4. Klicken Sie **auf Anmeldeinformationen erstellen** und dann auf **OAuth-Client-ID**. 

    1. Behalten Sie im Dialogfeld **Client-ID erstellen** die **Standardwebanwendung** für den Anwendungstyp bei.
    2. Legen Sie die **Authorized JavaScript-Ursprünge** auf`https://localhost:44300/` die oben verwendete SSL-URL fest (es sei denn, Sie haben andere SSL-Projekte erstellt)
    3. Legen Sie den **AUTHORIZED Redirect URI** auf:  
         `https://localhost:44300/signin-google`
5. Klicken Sie auf den Menüpunkt OAuth Consent, und legen Sie dann Ihre E-Mail-Adresse und Ihren Produktnamen fest. Wenn Sie das Formular ausgefüllt haben, klicken Sie auf **Speichern**.
6. Klicken Sie auf das Menüelement Bibliothek, suchen Sie **nach Google+ API**, klicken Sie darauf und drücken Sie aktivieren.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   Das Bild unten zeigt die aktivierten APIs.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Besuchen Sie im Google APIs API Manager die Registerkarte **Anmeldeinformationen,** um die **Client-ID**zu erhalten. Laden Sie diese Datei herunter, um eine JSON-Datei mit Anwendungsgeheimnissen zu speichern. Kopieren Sie die **ClientId** und `UseGoogleAuthentication` **ClientSecret** und fügen Sie sie in die Methode ein, die in der *Startup.Auth.cs* Datei im *Ordner App_Start* gefunden wurde. Die unten gezeigten **ClientId-** und **ClientSecret-Werte** sind Beispiele und funktionieren nicht.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Sicherheit - Speichern Sie niemals vertrauliche Daten in Ihrem Quellcode. Das Konto und die Anmeldeinformationen werden dem obigen Code hinzugefügt, um das Beispiel einfach zu halten. Weitere Informationen finden Sie unter [Bewährte Methoden zum Bereitstellen von Kennwörtern und anderen vertraulichen Daten in ASP.NET und Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
8. Drücken Sie **STRG+F5,** um die Anwendung zu erstellen und auszuführen. Klicken Sie auf den Link **Log in** .  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. Klicken Sie unter **Einen anderen Dienst zum Anmelden**verwenden auf **Google**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Wenn Sie einen der oben genannten Schritte verpassen, erhalten Sie einen HTTP 401-Fehler. Überprüfen Sie Ihre schritte oben erneut. Wenn Sie eine erforderliche Einstellung (z. B. **Produktname)** verfehlen, fügen Sie den fehlenden Artikel hinzu und speichern Sie es. Es kann einige Minuten dauern, bis die Authentifizierung funktioniert.
10. Sie werden auf die Google-Website weitergeleitet, auf der Sie Ihre Anmeldeinformationen eingeben.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Nachdem Sie Ihre Anmeldeinformationen eingegeben haben, werden Sie aufgefordert, Berechtigungen für die soeben erstellten Webanwendung zu erteilen: 
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Klicken Sie auf **Annehmen**. Sie werden nun zurück zur **Registrierungsseite** der MvcAuth-Anwendung weitergeleitet, wo Sie Ihr Google-Konto registrieren können. Sie können zwar den lokalen E-Mail-Registrierungsnamen in Ihr Gmail-Konto ändern, im Allgemeinen sollten Sie jedoch den Standard-E-Mail-Aliasnamen beibehalten (den Sie für die Authentifizierung verwendet haben). Klicken Sie auf **Registrieren**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Erstellen der App in Facebook und Verbinden der App mit dem Projekt

> [!WARNING]
> Aktuelle Anweisungen zur Facebook OAuth2-Authentifizierung finden Sie unter [Konfigurieren der Facebook-Authentifizierung](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Untersuchen der Mitgliedschaftsdaten

Klicken Sie im Menü **Ansicht** auf **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Erweitern Sie **DefaultConnection (MvcAuth),** erweitern **Sie Tabellen**, klicken Sie mit der rechten Maustaste auf **AspNetUsers,** und klicken Sie auf **Tabellendaten anzeigen**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![Aspnetusers-Tabellendaten](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Hinzufügen von Profildaten zur Benutzerklasse

In diesem Abschnitt fügen Sie den Benutzerdaten während der Registrierung Geburtsdatum und Heimatstadt hinzu, wie in der folgenden Abbildung dargestellt.

![reg mit Heimatstadt und Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Öffnen Sie die Datei *Models-IdentityModels.cs,* und fügen Sie Geburtsdatum und Heimatstadteigenschaften hinzu:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Öffnen Sie die Datei *Models-AccountViewModels.cs* und die `ExternalLoginConfirmationViewModel`festgelegten Geburtsdatums- und Heimatstadteigenschaften in .

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Öffnen Sie die Datei *Controllers-AccountController.cs,* und fügen `ExternalLoginConfirmation` Sie Code für Geburtsdatum und Heimatstadt in der Aktionsmethode hinzu, wie gezeigt:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Fügen Sie Geburtsdatum und Heimatstadt zur Datei *Views-Konto-ExternalLoginConfirmation.cshtml hinzu:*

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Löschen Sie die Mitgliedschaftsdatenbank, damit Sie Ihr Facebook-Konto erneut bei Ihrer Bewerbung registrieren können und überprüfen Sie, ob Sie das neue Geburtsdatum und die Profilinformationen der Heimatstadt hinzufügen können.

Klicken Sie im **Projektmappen-Explorer**auf das Symbol **Alle Dateien anzeigen,** und klicken Sie dann **Delete**mit der rechten Maustaste auf *Daten hinzufügen.\_&lt;&gt;*

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

Klicken Sie im Menü **Extras** auf **NuGet Package Manger**, und klicken Sie dann auf **Package Manager Console** (PMC). Geben Sie die folgenden Befehle in die PMC ein.

1. Enable-Migrations
2. Add-Migration Init
3. Update-Datenbank

Führen Sie die Anwendung aus und verwenden Sie FaceBook und Google, um sich anzumelden und einige Benutzer zu registrieren.

## <a name="examine-the-membership-data"></a>Untersuchen der Mitgliedschaftsdaten

Klicken Sie im Menü **Ansicht** auf **Server Explorer**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Klicken Sie mit der rechten Maustaste auf **AspNetUsers,** und klicken Sie auf **Tabellendaten anzeigen**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Die `HomeTown` `BirthDate` Felder und felder sind unten dargestellt.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Abmelden Ihrer App und Anmelden mit einem anderen Konto

Wenn Sie sich mit Facebook bei Ihrer App anmelden und sich dann abmelden und versuchen, sich erneut mit einem anderen Facebook-Konto anzumelden (mit demselben Browser), werden Sie sofort in das vorherige Facebook-Konto eingeloggt, das Sie verwendet haben. Um ein anderes Konto zu nutzen, musst du zu Facebook navigieren und dich bei Facebook ausloggen. Die gleiche Regel gilt für alle anderen Drittanbieter-Authentifizierungsanbieter. Alternativ können Sie sich mit einem anderen Konto anmelden, indem Sie einen anderen Browser verwenden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden [Sie unter Einführung in die Anweisungen zu den Sicherheitsanbietern Yahoo und LinkedIn OAuth für OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) von Jerrie Pelser für Yahoo und LinkedIn. Siehe Jerries Pretty Social Login Buttons für ASP.NET MVC 5, um Social Login-Buttons zu aktivieren.

Folgen Sie meinem Tutorial [Erstellen Sie eine ASP.NET MVC-App mit auth und SQL DB, und stellen Sie sie in Azure App Service bereit,](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)das dieses Tutorial fortsetzt und Folgendes zeigt:

1. So stellen Sie Ihre App in Azure bereit.
2. So sichern Sie Ihre App mit Rollen.
3. So sichern Sie Ihre App mit den Filtern [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) und [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)
4. Verwenden der Mitgliedschafts-API zum Hinzufügen von Benutzern und Rollen.

Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir verbessern könnten. Sie können auch neue Themen unter [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)anfordern. Sie können sogar um neue Funktionen bitten und abstimmen, die ASP.NET hinzugefügt werden sollen. Sie können z. B. für ein Tool zum Erstellen und Verwalten von [Benutzern und Rollen stimmen.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Eine gute Erklärung zur Funktionsweise ASP.NET Externe Authentifizierungsdienste finden Sie unter Robert McMurray es [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services). Roberts Artikel geht auch ins Detail, um die Microsoft- und Twitter-Authentifizierung zu aktivieren. Tom Dykstras ausgezeichnetes [EF/MVC-Tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) zeigt, wie sie mit dem Entity Framework arbeiten.
