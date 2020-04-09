---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: Kasse und Zahlung mit PayPal | Microsoft Docs
author: Erikre
description: In dieser Lernprogrammreihe werden Sie die Grundlagen zum Erstellen einer ASP.NET Web Forms-Anwendung mit ASP.NET 4.5 und Microsoft Visual Studio Express 2013 für Wir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675688"
---
# <a name="checkout-and-payment-with-paypal"></a>Bezahlvorgang und Zahlung mit PayPal

von [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys Sample Project herunterladen oder](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) [E-Book herunterladen (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> In dieser Lernprogrammreihe werden die Grundlagen zum Erstellen einer ASP.NET Web Forms-Anwendung mithilfe ASP.NET 4.5 und Microsoft Visual Studio Express 2013 für Web erläutert. Zur Begleitung dieser Lernprogrammreihe steht ein Visual Studio 2013-Projekt mit dem Quellcode von [C-Code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) zur Verfügung.

In diesem Tutorial wird beschrieben, wie Sie die Wingtip Toys-Beispielanwendung so ändern, dass sie Benutzerautorisierung, Registrierung und Zahlung mit PayPal einschließt. Nur Benutzer, die angemeldet sind, haben die Berechtigung zum Kauf von Produkten. Die integrierte Benutzerregistrierungsfunktion der ASP.NET 4.5 Web Forms-Projektvorlage enthält bereits viele snotwendige Funktionen. Sie fügen PayPal Express Checkout-Funktionalität hinzu. In diesem Tutorial verwenden Sie die Testumgebung für PayPal-Entwickler, sodass keine tatsächlichen Mittel übertragen werden. Am Ende des Tutorials testen Sie die Anwendung, indem Sie Produkte auswählen, die dem Warenkorb hinzugefügt werden sollen, auf die Schaltfläche "Auschecken" klicken und Daten an die PayPal-Testwebsite übertragen. Auf der PayPal-Testwebsite bestätigen Sie Ihre Versand- und Zahlungsinformationen und kehren dann zur lokalen Wingtip Toys-Beispielanwendung zurück, um den Kauf zu bestätigen und abzuschließen.

Es gibt mehrere erfahrene Zahlungsabwickler von Drittanbietern, die sich auf Online-Shopping spezialisiert haben, die skalierbarkeit und Sicherheit ansprechen. ASP.NET Entwickler sollten die Vorteile der Verwendung einer Zahlungslösung von Drittanbietern in Betracht ziehen, bevor Sie eine Einkaufs- und Einkaufslösung implementieren.

> [!NOTE] 
> 
> Die Wingtip Toys-Beispielanwendung wurde entwickelt, um spezifische ASP.NET Konzepte und Funktionen zu zeigen, die ASP.NET Webentwicklern zur Verfügung stehen. Diese Beispielanwendung wurde nicht für alle möglichen Umstände in Bezug auf Skalierbarkeit und Sicherheit optimiert.

## <a name="what-youll-learn"></a>Sie lernen Folgendes:

- So beschränken Sie den Zugriff auf bestimmte Seiten in einem Ordner.
- So erstellen Sie einen bekannten Warenkorb aus einem anonymen Warenkorb.
- So aktivieren Sie SSL für das Projekt.
- So fügen Sie dem Projekt einen OAuth-Anbieter hinzu.
- So verwenden Sie PayPal, um Produkte über die PayPal-Testumgebung zu kaufen.
- Anzeigen von Details aus PayPal in einem **DetailsView-Steuerelement.**
- So aktualisieren Sie die Datenbank der Wingtip Toys-Anwendung mit Details von PayPal.

## <a name="adding-order-tracking"></a>Hinzufügen von Auftragsverfolgung

In diesem Tutorial erstellen Sie zwei neue Klassen, um Daten aus der Reihenfolge zu verfolgen, die ein Benutzer erstellt hat. Die Klassen verfolgen Daten zu Versandinformationen, Einkaufssumme und Zahlungsbestätigung.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Hinzufügen der Modellklassen Order und OrderDetail

Zuvor haben Sie in dieser Lernprogrammreihe das Schema für Kategorien, `Category` `Product`Produkte `CartItem` und Einkaufswagenelemente definiert, indem Sie die , und Klassen im Ordner *Modelle* erstellt haben. Jetzt fügen Sie zwei neue Klassen hinzu, um das Schema für den Produktauftrag und die Details des Auftrags zu definieren.

1. Fügen Sie im Ordner **"Modelle"** eine neue Klasse mit dem Namen *Order.cs*hinzu.   
   Die neue Klassendatei wird im Editor angezeigt.
2. Ersetzen Sie den Standardcode durch Folgendes:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. Fügen Sie dem Ordner *Models* eine *OrderDetail.cs* Klasse hinzu.
4. Ersetzen Sie den Standardcode durch den folgenden Code:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

Die `Order` `OrderDetail` und-Klassen enthalten das Schema, um die Auftragsinformationen zu definieren, die für den Einkauf und versanden verwendet werden.

Darüber hinaus müssen Sie die Datenbankkontextklasse aktualisieren, die die Entitätsklassen verwaltet und Datenzugriff auf die Datenbank bereitstellt. Dazu fügen Sie der `OrderDetail` `ProductContext` Klasse die neu erstellten Auftrags- und Modellklassen hinzu.

1. Suchen und öffnen Sie im **Projektmappen-Explorer**die *ProductContext.cs* Datei.
2. Fügen Sie den hervorgehobenen Code zur *ProductContext.cs* Datei hinzu, wie unten gezeigt:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Wie bereits in dieser Lernprogrammreihe *ProductContext.cs* erwähnt, fügt `System.Data.Entity` der Code in der ProductContext.cs Datei den Namespace hinzu, sodass Sie Zugriff auf alle Kernfunktionen des Entity Framework haben. Diese Funktionalität umfasst die Möglichkeit, Daten abzufragen, einzufügen, zu aktualisieren und zu löschen, indem Sie mit stark typisierten Objekten arbeiten. Der obige `ProductContext` Code in der Klasse fügt `Order` `OrderDetail` Entity Framework-Zugriff auf die neu hinzugefügten Und Klassen hinzu.

## <a name="adding-checkout-access"></a>Hinzufügen von Kassenzugriff

Die Wingtip Toys-Beispielanwendung ermöglicht anonymen Benutzern, Produkte zu überprüfen und einem Warenkorb hinzuzufügen. Wenn sich jedoch anonyme Benutzer dafür entscheiden, die Produkte zu kaufen, die sie dem Warenkorb hinzugefügt haben, müssen sie sich bei der Website anmelden. Sobald sie sich angemeldet haben, können sie auf die eingeschränkten Seiten der Webanwendung zugreifen, die den Auscheck- und Kaufvorgang verarbeiten. Diese eingeschränkten Seiten sind im *Auscheckordner* der Anwendung enthalten.

### <a name="add-a-checkout-folder-and-pages"></a>Hinzufügen eines Auscheckordners und von Seiten

Sie erstellen nun den *Ordner "Auschecken"* und die darin angezeigten Seiten, die der Kunde während des Becheckvorgangs sehen wird. Sie werden diese Seiten später in diesem Tutorial aktualisieren.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen (**Wingtip Toys**), und wählen Sie **Einen neuen Ordner hinzufügen**aus. 

    ![Kasse und Zahlung mit PayPal - Neuer Ordner](checkout-and-payment-with-paypal/_static/image1.png)
2. Benennen Sie den neuen Ordner *Auschecken*.
3. Klicken Sie mit der rechten Maustaste auf den Ordner *Auschecken,* und wählen Sie dann**Neues Element** **hinzufügen**-&gt;aus. 

    ![Kasse und Zahlung mit PayPal - Neuer Artikel](checkout-and-payment-with-paypal/_static/image2.png)
4. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt.
5. Wählen Sie auf der linken Seite die Gruppe **"Visual C-Webvorlagen"**  - &gt; **Web** aus. Wählen Sie dann im mittleren Bereich **Webformular mit Masterseite**aus und nennen Sie es *CheckoutStart.aspx*. 

    ![Auschecken und Bezahlen mit PayPal - Neues Artikel-Dialog hinzufügen](checkout-and-payment-with-paypal/_static/image3.png)
6. Wählen Sie wie zuvor die *Site.Master-Datei* als Masterseite aus.
7. Fügen Sie die folgenden zusätzlichen Seiten mit den oben beschriebenen Schritten zum *Auscheckordner* hinzu:   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Hinzufügen einer Web.config-Datei

Durch Hinzufügen einer neuen *Web.config-Datei* zum *Ordner Auschecken* können Sie den Zugriff auf alle im Ordner enthaltenen Seiten einschränken.

1. Klicken Sie mit der rechten Maustaste auf den Ordner *Auschecken,* und wählen Sie **Neues Element** **hinzufügen**  - &gt; aus.  
   Das Dialogfeld **Neues Element hinzufügen** wird angezeigt.
2. Wählen Sie auf der linken Seite die Gruppe **"Visual C-Webvorlagen"**  - &gt; **Web** aus. Wählen Sie dann im mittleren Bereich **Webkonfigurationsdatei**aus , akzeptieren Sie den Standardnamen *von Web.config*, und wählen Sie dann **Hinzufügen**aus.
3. Ersetzen Sie den vorhandenen XML-Inhalt in der Datei *Web.config* durch den folgenden Code:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. Speichern Sie die *web.config*-Datei.

Die *Datei Web.config* gibt an, dass allen unbekannten Benutzern der Webanwendung der Zugriff auf die im Ordner *Auschecken* enthaltenen Seiten verweigert werden muss. Wenn der Benutzer jedoch ein Konto registriert hat und angemeldet ist, handelt es sich um einen bekannten Benutzer, der Zugriff auf die Seiten im Ordner *Auschecken* hat.

Es ist wichtig zu beachten, dass ASP.NET Konfiguration einer Hierarchie folgt, in der jede *Web.config-Datei* Konfigurationseinstellungen auf den Ordner anwendet, in dem sie sich befindet, und auf alle untergeordneten Verzeichnisse darunter.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Aktivieren von SSL für das Projekt

 Secure Sockets Layer (SSL) ist ein Protokoll, das Webservern und Webclients eine sichere Kommunikation durch Verschlüsselung ermöglicht. Wird kein SSL verwendet, können die zwischen Client und Server gesendeten Daten von jedem mit physischem Zugriff auf das Netzwerk per Paket-Sniffing ausgespäht werden. Außerdem sind verschiedene häufig verwendete Authentifizierungsschemas über einfaches HTTP nicht sicher. Insbesondere senden die einfache Authentifizierung und Formularauthentifizierung unverschlüsselte Anmeldeinformationen. Aus Sicherheitsgründen sollten diese Authentifizierungsschemas SSL verwenden. 

1. Klicken Sie im **Projektmappen-Explorer**auf das **WingtipToys-Projekt,** und drücken Sie dann **F4,** um das **Eigenschaftenfenster** anzuzeigen.
2. Ändern Von `true`SSL **Aktiviert** in .
3. Kopieren Sie die **SSL-URL** , damit Sie sie später verwenden können.   
 Die SSL-URL `https://localhost:44300/` wird angezeigt, es sei denn, Sie haben zuvor SSL-Websites erstellt (wie unten gezeigt).   
    ![Projekteigenschaften](checkout-and-payment-with-paypal/_static/image4.png)
4. Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das **WingtipToys-Projekt,** und klicken Sie auf **Eigenschaften**.
5. Klicken Sie auf der linken Registerkarte auf **Web**.
6. Ändern Sie die **Projekt-URL,** um die **SSL-URL** zu verwenden, die Sie zuvor gespeichert haben.   
    ![Projekt-Webeigenschaften](checkout-and-payment-with-paypal/_static/image5.png)
7. Drücken Sie **STRG+S**, um die Seite zu speichern.
8. Drücken Sie **STRG+F5** , um die Anwendung auszuführen. Visual Studio zeigt eine Option an, die es Ihnen ermöglicht, SSL-Warnungen zu vermeiden.
9. Klicken Sie auf **Ja** , um dem IIS Express SSL-Zertifikat zu vertrauen und fortzufahren.   
    ![IIS Express SSL-Zertifikatdetails](checkout-and-payment-with-paypal/_static/image6.png)  
  Es wird eine Sicherheitswarnung angezeigt.
10. Klicken Sie auf **Ja** , um das Zertifikat zu Ihrem Localhost zu installieren.   
    ![Dialogfeld "Sicherheitswarnung"](checkout-and-payment-with-paypal/_static/image7.png)  
  Das Browserfenster wird angezeigt.

Sie können Ihre Webanwendung jetzt ganz einfach lokal mit SSL testen.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>Hinzufügen eines OAuth 2.0-Anbieters

ASP.NET Web Forms bietet erweiterte Optionen für Mitgliedschaft und Authentifizierung. Diese Erweiterungen umfassen OAuth. OAuth ist ein offenes Protokoll, das die sichere Autorisierung in einer einfachen und Standardmethode von Web-, Mobil- und Desktopanwendungen ermöglicht. Die ASP.NET Web Forms-Vorlage verwendet OAuth, um Facebook, Twitter, Google und Microsoft als Authentifizierungsanbieter verfügbar zu machen. Auch wenn in diesem Lernprogramm nur Google als Authentifizierungsanbieter eingesetzt wird, können Sie den Code problemlos für die Verwendung einer der anderen Anbieter anpassen. Die Schritte zur Implementierung anderer Anbieter unterscheiden sich kaum von den Schritten in diesem Lernprogramm.

Abgesehen von der Authentifizierung werden in diesem Lernprogramm auch Rollen verwendet, um die Autorisierung zu implementieren. Nur Benutzer, die Sie der Rolle `canEdit` hinzufügen, können Daten ändern (Kontakte erstellen, bearbeiten oder löschen.

> [!NOTE] 
> 
> Windows Live-Anwendungen akzeptieren nur eine Live-URL für eine funktionierende Website, sodass Sie keine lokale Website-URL zum Testen von Anmeldungen verwenden können.

Mit den folgenden Schritten können Sie einen Google-Authentifizierungsanbieter hinzufügen.

1. Öffnen Sie die Datei *App\_Start.Auth.cs.*
2. Entfernen Sie die Kommentarzeichen aus der `app.UseGoogleAuthentication()` -Methode, sodass sie wie folgt aussieht: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. Navigieren Sie zur [Google Developers Console](https://console.developers.google.com/). Außerdem müssen Sie sich mit Ihrem Google Entwickler-E-Mail-Konto anmelden (gmail.com). Wenn Sie nicht über ein Google-Konto verfügen, wählen Sie den Link **Konto erstellen** aus.   
   Danach sehen Sie die **Google Entwickler-Konsole**.   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. Klicken Sie auf die Schaltfläche **Projekt** erstellen, und geben Sie einen Projektnamen und eine Projekt-ID ein (Sie können die Standardwerte verwenden). Klicken Sie dann auf das **Kontrollkästchen Vereinbarung** und die Schaltfläche **Erstellen.**  

    ![Google - Neues Projekt](checkout-and-payment-with-paypal/_static/image9.png)

    In wenigen Sekunden wird das neue Projekt erstellt, und Ihr Browser zeigt die Seite für neue Projekte an.
5. Klicken Sie auf der linken Registerkarte auf **APIs &amp; auth**, und dann auf **Anmeldeinformationen**.
6. Klicken Sie unter **OAuth**auf die **Create New Client ID** .   
   Das Dialogfeld **Client-ID erstellen** wird angezeigt.   
    ![Google - Client-ID erstellen](checkout-and-payment-with-paypal/_static/image10.png)
7. Behalten Sie im Dialogfeld **Client-ID erstellen** die **Standardwebanwendung** für den Anwendungstyp bei.
8. Legen Sie die **autorisierteJavaScript-Ursprung** auf die SSL-URL fest, die Sie zuvor in diesem Tutorial verwendet haben (es`https://localhost:44300/` sei denn, Sie haben andere SSL-Projekte erstellt).   
   Diese URL ist der Ursprung für Ihre Anwendung. In diesem Beispiel geben Sie nur die Test-URL "localhost" ein. Sie können jedoch mehrere URLs eingeben, um localhost und production zu berücksichtigen.
9. Legen Sie **Authorized Redirect URI** folgendermaßen fest: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Dieser Wert steht für den URI, den ASP.NET OAuth-Benutzer zur Kommunikation mit dem Google OAuth-Server verwenden. Merken Sie sich die `https://localhost:44300/` SSL-URL, die Sie oben verwendet haben (es sei denn, Sie haben andere SSL-Projekte erstellt).
10. Klicken Sie auf die Schaltfläche **Client-ID erstellen.**
11. Klicken Sie im linken Menü der Google Developers Console auf den Menüpunkt **Zustimmung** und legen Sie dann Ihre E-Mail-Adresse und Ihren Produktnamen fest. Wenn Sie das Formular ausgefüllt haben, klicken Sie auf **Speichern**.
12. Klicken Sie auf das **Menüelement APIs,** scrollen Sie nach unten und klicken Sie auf die Schaltfläche **aus** neben der **Google+ API**.   
    Wenn Sie diese Option akzeptieren, wird die Google+ API aktiviert.
13. Sie müssen auch das **Microsoft.Owin** NuGet-Paket auf Version 3.0.0 aktualisieren.   
    Wählen Sie im Menü **Extras** **NuGet Package Manager** und dann **NuGet-Pakete für Lösung verwalten**aus.  
    Suchen und aktualisieren Sie das **Microsoft.Owin-Paket** im Fenster **NuGet-Pakete** verwalten auf Version 3.0.0.
14. Aktualisieren Sie in `UseGoogleAuthentication` Visual Studio die Methode der *Startup.Auth.cs* Seite, indem Sie die **Client-ID** und den **geheimen Clientschlüssel** in die Methode kopieren und einfügen. Die unten angezeigten **Client-ID-** und **Client-Geheimwerte** sind Beispiele und funktionieren nicht. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Drücken Sie **STRG+F5,** um die Anwendung zu erstellen und auszuführen. Klicken Sie auf den Link **Log in** .
16. Klicken Sie unter **Einen anderen Dienst zum Anmelden**verwenden auf **Google**.  
    ![Anmelden](checkout-and-payment-with-paypal/_static/image11.png)
17. Wenn Sie Ihre Anmeldeinformationen eingeben müssen, werden Sie zur Google-Website umgeleitet, wo Sie Ihre Anmeldeinformationen eingeben.  
    ![Google - Anmeldung](checkout-and-payment-with-paypal/_static/image12.png)
18. Nachdem Sie Ihre Anmeldeinformationen eingegeben haben, werden Sie aufgefordert, der gerade erstellten Webanwendung Berechtigungen zu erteilen.  
    ![Standard-Dienstkonto für Projekt](checkout-and-payment-with-paypal/_static/image13.png)
19. Klicken Sie auf **Annehmen**. Sie werden nun zurück zur **Registrierungsseite** der **WingtipToys-Anwendung** weitergeleitet, wo Sie Ihr Google-Konto registrieren können.  
    ![Registrieren Sie sich mit Ihrem Google-Konto](checkout-and-payment-with-paypal/_static/image14.png)
20. Sie können zwar den lokalen E-Mail-Registrierungsnamen in Ihr Gmail-Konto ändern, im Allgemeinen sollten Sie jedoch den Standard-E-Mail-Aliasnamen beibehalten (den Sie für die Authentifizierung verwendet haben). Klicken Sie auf **Anmelden** wie oben gezeigt.

### <a name="modifying-login-functionality"></a>Ändern der Anmeldefunktionalität

Wie bereits in dieser Lernprogrammreihe erwähnt, wurde ein Großteil der Benutzerregistrierungsfunktionalität standardmäßig in die Vorlage ASP.NET Web Forms aufgenommen. Nun ändern Sie die Standardmäßigen Seiten *Login.aspx* `MigrateCart` und *Register.aspx,* um die Methode aufzurufen. Die `MigrateCart` Methode ordnet einem neu angemeldeten Benutzer einen anonymen Warenkorb zu. Durch die Zuordnung des Benutzers und des Warenkorbs wird die Wingtip Toys-Beispielanwendung in der Lage sein, den Warenkorb des Benutzers zwischen den Besuchen zu pflegen.

1. Suchen und öffnen Sie im **Projektmappen-Explorer**den *Ordner "Konto",* und öffnen Sie ihn.
2. Ändern Sie die CodeBehind-Seite mit dem Namen *Login.aspx.cs,* um den gelb markierten Code einzuschließen, sodass er wie folgt angezeigt wird:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. Speichern Sie die *Login.aspx.cs* Datei.

Im Moment können Sie die Warnung ignorieren, `MigrateCart` dass es keine Definition für die Methode gibt. Sie werden es etwas später in diesem Tutorial hinzufügen.

Die *Login.aspx.cs* CodeBehind-Datei unterstützt eine LogIn-Methode. Wenn Sie die Seite Login.aspx überprüfen, sehen Sie, dass diese Seite eine Schaltfläche `LogIn` "Anmelden" enthält, die beim Klicken den Handler auf dem CodeBehind auslöst.

Wenn `Login` die Methode auf der *Login.aspx.cs* aufgerufen wird, `usersShoppingCart` wird eine neue Instanz des mit Namen benannten Einkaufswagens erstellt. Die ID des Warenkorbs (eine GUID) `cartId` wird abgerufen und auf die Variable gesetzt. Anschließend wird `MigrateCart` die Methode aufgerufen `cartId` und übergibt sowohl den Namen als auch den Namen des angemeldeten Benutzers an diese Methode. Wenn der Warenkorb migriert wird, wird die GUID, die zum Identifizieren des anonymen Warenkorbs verwendet wird, durch den Benutzernamen ersetzt.

Zusätzlich zum Ändern der *Login.aspx.cs* CodeBehind-Datei, um den Warenkorb zu migrieren, wenn sich der Benutzer anmeldet, müssen Sie auch die *Register.aspx.cs CodeBehind-Datei* ändern, um den Warenkorb zu migrieren, wenn der Benutzer ein neues Konto erstellt und sich anmeldet.

1. Öffnen Sie im *Ordner Konto* die CodeBehind-Datei mit dem Namen *Register.aspx.cs*.
2. Ändern Sie die CodeBehind-Datei, indem Sie den Code gelb einschließen, sodass er wie folgt angezeigt wird:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. Speichern Sie die *Register.aspx.cs* Datei. Ignorieren Sie erneut die `MigrateCart` Warnung über die Methode.

Beachten Sie, dass der `CreateUser_Click` Code, den Sie im Ereignishandler `LogIn` verwendet haben, dem Code sehr ähnlich ist, den Sie in der Methode verwendet haben. Wenn sich der Benutzer an der Website registriert `MigrateCart` oder sich anmeldet, wird die Methode aufruft.

## <a name="migrating-the-shopping-cart"></a>Migrieren des Warenkorbs

Nachdem Sie den Anmelde- und Registrierungsprozess aktualisiert haben, können Sie den `MigrateCart` Code hinzufügen, um den Warenkorb mit der Methode zu migrieren.

1. Suchen Sie im **Projektmappen-Explorer**den *Ordner "Logik",* und öffnen Sie die ShoppingCartActions.cs-Klassendatei. *ShoppingCartActions.cs*
2. Fügen Sie den gelb markierten Code dem vorhandenen Code in der *ShoppingCartActions.cs-Datei* hinzu, sodass der Code in der *ShoppingCartActions.cs* Datei wie folgt angezeigt wird:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

Die `MigrateCart` Methode verwendet die vorhandene cartId, um den Warenkorb des Benutzers zu finden. Als Nächstes durchläuft der Code alle Warenkorbartikel `CartId` und ersetzt die `CartItem` Eigenschaft (wie im Schema angegeben) durch den angemeldeten Benutzernamen.

### <a name="updating-the-database-connection"></a>Aktualisieren der Datenbankverbindung

Wenn Sie diesem Tutorial mit der **vorgefertigten** Wingtip Toys-Beispielanwendung folgen, müssen Sie die Standardmitgliedschaftsdatenbank neu erstellen. Durch Ändern der Standardverbindungszeichenfolge wird die Mitgliedschaftsdatenbank bei der nächsten Anwendung erstellt.

1. Öffnen Sie die Datei *Web.config* im Stammverzeichnis des Projekts.
2. Aktualisieren Sie die Standardverbindungszeichenfolge so, dass sie wie folgt angezeigt wird:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>Integration von PayPal

PayPal ist eine webbasierte Abrechnungsplattform, die Zahlungen von Online-Händlern akzeptiert. In diesem Tutorial wird erläutert, wie Sie die Express Checkout-Funktionalität von PayPal in Ihre Anwendung integrieren. Express Checkout ermöglicht es Ihren Kunden, PayPal zu verwenden, um für die Artikel zu bezahlen, die sie ihrem Warenkorb hinzugefügt haben.

### <a name="create-paypal-test-accounts"></a>Erstellen von PayPal-Testkonten

Um die PayPal-Testumgebung verwenden zu können, müssen Sie ein Entwicklertestkonto erstellen und überprüfen. Sie verwenden das Entwicklertestkonto, um ein Käufertestkonto und ein Verkäufertestkonto zu erstellen. Die Anmeldeinformationen für Entwicklertestkonten ermöglichen der Wingtip Toys-Beispielanwendung auch den Zugriff auf die PayPal-Testumgebung.

1. Navigieren Sie in einem Browser zur Testwebsite für PayPal-Entwickler:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. Wenn Sie kein PayPal-Entwicklerkonto haben, erstellen Sie ein neues Konto, indem Sie auf **Anmelden**klicken und die Anmeldeschritte befolgen. Wenn Sie über ein vorhandenes PayPal-Entwicklerkonto verfügen, melden Sie sich an, indem Sie auf **Anmelden**klicken. Sie benötigen Ihr PayPal-Entwicklerkonto, um die Wingtip Toys-Beispielanwendung später in diesem Tutorial zu testen.
3. Wenn Sie sich gerade für Ihr PayPal-Entwicklerkonto angemeldet haben, müssen Sie möglicherweise Ihr PayPal-Entwicklerkonto bei PayPal überprüfen. Sie können Ihr Konto überprüfen, indem Sie die Schritte ausführen, die PayPal an Ihr E-Mail-Konto gesendet hat. Sobald Sie Ihr PayPal-Entwicklerkonto verifiziert haben, melden Sie sich wieder bei der PayPal-Entwicklertestwebsite an.
4. Nachdem Sie mit Ihrem PayPal-Entwicklerkonto bei der PayPal-Entwicklerwebsite angemeldet sind, müssen Sie ein PayPal-Käufertestkonto erstellen, wenn Sie noch keins haben. Um ein Käufertestkonto zu erstellen, klicken Sie auf der PayPal-Website auf die Registerkarte **Anwendungen,** und klicken Sie dann auf **Sandbox-Konten**.   
 Die Seite **Sandbox-Testkonten** wird angezeigt.   

    > [!NOTE] 
    > 
    > Die PayPal Developer-Website stellt bereits ein Händlertestkonto bereit.

    ![Checkout und Zahlung mit PayPal - Sandbox-Testkonten](checkout-and-payment-with-paypal/_static/image15.png)
5. Klicken Sie auf der Seite Sandbox-Testkonten auf **Konto erstellen**.
6. Wählen Sie auf der Seite **Testkonto erstellen** eine E-Mail und ein Kennwort für das Käufertestkonto Ihrer Wahl aus.   

    > [!NOTE] 
    > 
    > Sie benötigen die E-Mail-Adressen und das Kennwort des Käufers, um die Wingtip Toys-Beispielanwendung am Ende dieses Tutorials zu testen.

    ![Checkout und Zahlung mit PayPal - Sandbox-Testkonten](checkout-and-payment-with-paypal/_static/image16.png)
7. Erstellen Sie das Käufertestkonto, indem Sie auf die Schaltfläche **Konto erstellen** klicken.  
 Die Seite **Sandbox-Testkonten** wird angezeigt. 

    ![Kasse und Zahlung mit PayPal - PayPal-Konten](checkout-and-payment-with-paypal/_static/image17.png)
8. Klicken Sie auf der Seite **Sandbox-Testkonten** auf das E-Mail-Konto des **Moderators.**  
    **Profil-** und **Benachrichtigungsoptionen** werden angezeigt.
9. Wählen Sie die Option **Profil aus,** und klicken Sie dann auf **API-Anmeldeinformationen,** um Ihre API-Anmeldeinformationen für das Händlertestkonto anzuzeigen.
10. Kopieren Sie die TEST-API-Anmeldeinformationen in den Notizblock.

Sie benötigen Ihre angezeigten Classic TEST-API-Anmeldeinformationen (Benutzername, Kennwort und Signatur), um API-Aufrufe von der Wingtip Toys-Beispielanwendung an die PayPal-Testumgebung durchzuführen. Sie fügen die Anmeldeinformationen im nächsten Schritt hinzu.

### <a name="add-paypal-class-and-api-credentials"></a>Hinzufügen von PayPal-Klassen- und API-Anmeldeinformationen

Sie platzieren den Großteil des PayPal-Codes in einer einzigen Klasse. Diese Klasse enthält die Methoden, die für die Kommunikation mit PayPal verwendet werden. Außerdem fügen Sie Ihre PayPal-Anmeldeinformationen zu dieser Klasse hinzu.

1. Klicken Sie in der Wingtip Toys-Beispielanwendung in Visual Studio mit der rechten Maustaste auf den Ordner **"Logik",** und wählen Sie dann **Neues Element** **hinzufügen**  - &gt; aus.   
   Das Dialogfeld **Neues Element hinzufügen** wird angezeigt.
2. Wählen Sie unter **Visual C'** aus dem Bereich **Installiert** auf der linken Seite **Code**aus.
3. Wählen Sie im mittleren Bereich **Klasse**aus. Benennen Sie diese neue Klasse **PayPalFunctions.cs**.
4. Klicken Sie auf **Hinzufügen**.  
   Die neue Klassendatei wird im Editor angezeigt.
5. Ersetzen Sie den Standardcode durch den folgenden Code:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. Fügen Sie die Anmeldeinformationen der Händler-API (Benutzername, Kennwort und Signatur) hinzu, die Sie zuvor in diesem Tutorial angezeigt haben, damit Sie Funktionsaufrufe an die PayPal-Testumgebung durchführen können.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> In dieser Beispielanwendung fügen Sie einfach Anmeldeinformationen zu einer C-Datei (.cs) hinzu. In einer implementierten Lösung sollten Sie jedoch erwägen, Ihre Anmeldeinformationen in einer Konfigurationsdatei zu verschlüsseln.

Die NVPAPICaller-Klasse enthält den Großteil der PayPal-Funktionalität. Der Code in der Klasse stellt die Methoden bereit, die für einen Testkauf in der PayPal-Testumgebung erforderlich sind. Die folgenden drei PayPal-Funktionen werden verwendet, um Einkäufe zu tätigen:

- `SetExpressCheckout`-Funktion
- `GetExpressCheckoutDetails`-Funktion
- `DoExpressCheckoutPayment`-Funktion

Die `ShortcutExpressCheckout` Methode erfasst die Testkaufinformationen und Produktdetails aus `SetExpressCheckout` dem Warenkorb und ruft die PayPal-Funktion auf. Die `GetCheckoutDetails` Methode bestätigt Kaufdetails `GetExpressCheckoutDetails` und ruft die PayPal-Funktion auf, bevor Sie den Testkauf tätigen. Die `DoCheckoutPayment` Methode schließt den Testkauf aus der `DoExpressCheckoutPayment` Testumgebung ab, indem sie die PayPal-Funktion aufruft. Der verbleibende Code unterstützt die PayPal-Methoden und -Prozesse, z. B. Codierungszeichenfolgen, Dekodierung von Zeichenfolgen, Verarbeitung von Arrays und Bestimmen von Anmeldeinformationen.

> [!NOTE] 
> 
> Mit PayPal können Sie optionale Kaufdetails basierend auf der [API-Spezifikation von PayPal](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)einschließen. Durch Die Erweiterung des Codes in der Wingtip Toys-Beispielanwendung können Sie Lokalisierungsdetails, Produktbeschreibungen, Steuern, eine Kundendienstnummer sowie viele andere optionale Felder einschließen.

Beachten Sie, dass die in der **ShortcutExpressCheckout-Methode** angegebenen Rückgabe- und Abbruch-URLs eine Portnummer verwenden.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Wenn Visual Web Developer ein Webprojekt mit SSL ausführt, wird normalerweise der Port 44300 für den Webserver verwendet. Wie oben gezeigt, ist die Portnummer 44300. Wenn Sie die Anwendung ausführen, wird möglicherweise eine andere Portnummer angezeigt. Ihre Portnummer muss im Code korrekt festgelegt werden, damit Sie die Wingtip Toys-Beispielanwendung am Ende dieses Tutorials erfolgreich ausführen können. Im nächsten Abschnitt dieses Tutorials wird erläutert, wie Sie die lokale Hostportnummer abrufen und die PayPal-Klasse aktualisieren.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>Aktualisieren der LokalenHost-Portnummer in der PayPal-Klasse

Die Wingtip Toys-Beispielanwendung kauft Produkte, indem sie zur PayPal-Testwebsite navigiert und zu Ihrer lokalen Instanz der Wingtip Toys-Beispielanwendung zurückkehrt. Damit PayPal zur richtigen URL zurückkehrt, müssen Sie die Portnummer der lokal ausgeführten Beispielanwendung im oben genannten PayPal-Code angeben.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen (**WingtipToys**), und wählen Sie **Eigenschaften**aus.
2. Wählen Sie in der linken Spalte die Registerkarte **Web** aus.
3. Rufen Sie die Portnummer aus dem Feld **Projekt-Url** ab.
4. Aktualisieren Sie bei `returnURL` `cancelURL` Bedarf die und`NVPAPICaller`in der PayPal-Klasse ( ) in der *PayPalFunctions.cs-Datei,* um die Portnummer Ihrer Webanwendung zu verwenden:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Der hinzugefügte Code stimmt nun mit dem erwarteten Port für Ihre lokale Webanwendung überein. PayPal kann zur richtigen URL auf Ihrem lokalen Computer zurückkehren.

### <a name="add-the-paypal-checkout-button"></a>Hinzufügen der PayPal-Checkout-Schaltfläche

Nachdem die primären PayPal-Funktionen der Beispielanwendung hinzugefügt wurden, können Sie mit dem Hinzufügen des Markups und des Codes beginnen, der zum Aufrufen dieser Funktionen erforderlich ist. Zuerst müssen Sie die Auscheck-Schaltfläche hinzufügen, die der Benutzer auf der Warenkorbseite sehen wird.

1. Öffnen Sie die Datei *ShoppingCart.aspx.*
2. Scrollen Sie zum Ende der `<!--Checkout Placeholder -->` Datei, und suchen Sie nach dem Kommentar.
3. Ersetzen Sie den `ImageButton` Kommentar durch ein Steuerelement, sodass das Markup wie folgt ersetzt wird:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. Fügen *ShoppingCart.aspx.cs* Sie in der `UpdateBtn_Click` ShoppingCart.aspx.cs Datei nach dem Ereignishandler `CheckOutBtn_Click` am Ende der Datei den Ereignishandler hinzu:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. Fügen Sie *ShoppingCart.aspx.cs* auch in der ShoppingCart.aspx.cs `CheckoutBtn`Datei einen Verweis auf die hinzu, sodass auf die Schaltfläche "Neues Bild" wie folgt verwiesen wird:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Speichern Sie Ihre Änderungen sowohl in der *Datei ShoppingCart.aspx* als auch in der *ShoppingCart.aspx.cs-Datei.*
7. Wählen Sie im Menü **Debug**-&gt;**Build WingtipToys**aus.  
   Das Projekt wird mit dem neu hinzugefügten **ImageButton-Steuerelement** neu erstellt.

### <a name="send-purchase-details-to-paypal"></a>Kaufdetails an PayPal senden

Wenn der Benutzer auf der Warenkorbseite (*ShoppingCart.aspx*) auf die Schaltfläche **Auschecken** klickt, beginnt er mit dem Kaufvorgang. Der folgende Code ruft die erste PayPal-Funktion auf, die zum Kauf von Produkten erforderlich ist.

1. Öffnen Sie im Ordner *Auschecken* die CodeBehind-Datei mit dem Namen *CheckoutStart.aspx.cs*.   
   Achten Sie darauf, die CodeBehind-Datei zu öffnen.
2. Ersetzen Sie den vorhandenen Code durch folgenden Code:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Wenn der Benutzer der Anwendung auf der Warenkorbseite auf die Schaltfläche **Auschecken** klickt, navigiert der Browser zur Seite *CheckoutStart.aspx.* Wenn die Seite *CheckoutStart.aspx* geladen wird, wird die `ShortcutExpressCheckout` Methode aufgerufen. An dieser Stelle wird der Benutzer auf die PayPal-Testwebsite übertragen. Auf der PayPal-Website gibt der Benutzer seine PayPal-Anmeldeinformationen ein, überprüft die Kaufdetails, akzeptiert `ShortcutExpressCheckout` die PayPal-Vereinbarung und kehrt zur Wingtip Toys-Beispielanwendung zurück, bei der die Methode abgeschlossen ist. Wenn `ShortcutExpressCheckout` die Methode abgeschlossen ist, wird der Benutzer zur in der `ShortcutExpressCheckout` Methode angegebenen Seite *CheckoutReview.aspx* umgeleitet. Auf diese Weise kann der Benutzer die Bestelldetails in der Wingtip Toys-Beispielanwendung überprüfen.

### <a name="review-order-details"></a>Bestelldetails überprüfen

Nach der Rückkehr von PayPal werden auf der Seite *CheckoutReview.aspx* der Wingtip Toys-Beispielanwendung die Bestelldetails angezeigt. Auf dieser Seite kann der Benutzer die Bestelldetails vor dem Kauf der Produkte überprüfen. Die Seite *CheckoutReview.aspx* muss wie folgt erstellt werden:

1. Öffnen Sie im Ordner *Auschecken* die Seite mit dem Namen *CheckoutReview.aspx*.
2. Ersetzen Sie das vorhandene Markup durch Folgendes:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. Öffnen Sie die CodeBehind-Seite mit dem Namen *CheckoutReview.aspx.cs,* und ersetzen Sie den vorhandenen Code durch Folgendes:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

Das **DetailsView-Steuerelement** wird verwendet, um die Auftragsdetails anzuzeigen, die von PayPal zurückgegeben wurden. Außerdem speichert der obige Code die Bestelldetails in `OrderDetail` der Wingtip Toys-Datenbank als Objekt. Wenn der Benutzer auf die Schaltfläche **"Bestellung abschließen"** klickt, wird er zur Seite *CheckoutComplete.aspx* weitergeleitet.

> [!NOTE] 
> 
> **Tipp**
> 
> Beachten Sie im Markup der *Seite CheckoutReview.aspx,* dass das `<ItemStyle>` Tag verwendet wird, um den Stil der Elemente im **DetailsView-Steuerelement** am unteren Rand der Seite zu ändern. Wenn Sie die Seite in der **Entwurfsansicht** anzeigen (durch Auswählen von **Entwurf** in der unteren linken Ecke von Visual Studio), dann das **DetailsView-Steuerelement** und das **Smarttag** (das Pfeilsymbol oben rechts im Steuerelement) auswählen, können Sie die **DetailsView-Aufgaben**anzeigen.
> 
> ![Auschecken und Bezahlen mit PayPal - Felder bearbeiten](checkout-and-payment-with-paypal/_static/image18.png)
> 
> Wenn Sie **Felder bearbeiten**auswählen, wird das Dialogfeld **Felder** angezeigt. In diesem Dialogfeld können Sie die visuellen Eigenschaften, z. B. **ItemStyle**, des **DetailsView-Steuerelements** problemlos steuern.
> 
> ![Checkout und Zahlung mit PayPal - Felder Dialog](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Kompletter Kauf

*CheckoutComplete.aspx* Seite macht den Kauf von PayPal. Wie oben erwähnt, muss der Benutzer auf die Schaltfläche **Bestellung abschließen** klicken, bevor die Anwendung zur Seite *CheckoutComplete.aspx* navigiert.

1. Öffnen Sie im Ordner *Auschecken* die Seite mit dem Namen *CheckoutComplete.aspx*.
2. Ersetzen Sie das vorhandene Markup durch Folgendes:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. Öffnen Sie die CodeBehind-Seite mit dem Namen *CheckoutComplete.aspx.cs,* und ersetzen Sie den vorhandenen Code durch Folgendes:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

Wenn die Seite *CheckoutComplete.aspx* `DoCheckoutPayment` geladen wird, wird die Methode aufgerufen. Wie bereits erwähnt, schließt die `DoCheckoutPayment` Methode den Kauf aus der PayPal-Testumgebung ab. Sobald PayPal den Kauf der Bestellung abgeschlossen hat, zeigt die `ID` Seite *CheckoutComplete.aspx* dem Käufer eine Zahlungstransaktion an.

### <a name="handle-cancel-purchase"></a>Handle Cancel Purchase

Wenn der Benutzer beschließt, den Kauf zu stornieren, wird er auf die Seite *CheckoutCancel.aspx* weitergeleitet, auf der er sieht, dass seine Bestellung storniert wurde.

1. Öffnen Sie die Seite mit dem Namen *CheckoutCancel.aspx* im *Ordner Auschecken.*
2. Ersetzen Sie das vorhandene Markup durch Folgendes:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Behandeln von Kauffehlern

Fehler während des Kaufvorgangs werden von der Seite *CheckoutError.aspx* behandelt. Der Codebehind der *Seite CheckoutStart.aspx,* der Seite *CheckoutReview.aspx* und der Seite *CheckoutComplete.aspx* wird jeweils zur Seite *CheckoutError.aspx* umgeleitet, wenn ein Fehler auftritt.

1. Öffnen Sie die Seite mit dem Namen *CheckoutError.aspx* im *Ordner Auschecken.*
2. Ersetzen Sie das vorhandene Markup durch Folgendes:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

Die Seite *CheckoutError.aspx* wird mit den Fehlerdetails angezeigt, wenn während des Auscheckvorgangs ein Fehler auftritt.

## <a name="running-the-application"></a>Ausführen der Anwendung

Führen Sie die Anwendung aus, um zu sehen, wie Produkte gekauft werden. Beachten Sie, dass Sie in der PayPal-Testumgebung ausgeführt werden. Es wird kein tatsächliches Geld umgetauscht.

1. Stellen Sie sicher, dass alle Dateien in Visual Studio gespeichert sind.
2. Öffnen Sie einen Webbrowser, und navigieren Sie zu [https://developer.paypal.com](https://developer.paypal.com/).
3. Melden Sie sich mit Ihrem PayPal-Entwicklerkonto an, das Sie zuvor in diesem Tutorial erstellt haben.  
   Für die Entwickler-Sandbox von PayPal müssen [https://developer.paypal.com](https://developer.paypal.com/) Sie eingeloggt sein, um express checkout zu testen. Dies gilt nur für PayPals Sandbox-Tests, nicht für die Live-Umgebung von PayPal.
4. Drücken Sie in Visual Studio **F5,** um die Wingtip Toys-Beispielanwendung auszuführen.  
   Nachdem die Datenbank neu erstellt wurde, wird der Browser geöffnet und zeigt die Seite *Default.aspx* an.
5. Fügen Sie dem Warenkorb drei verschiedene Produkte hinzu, indem Sie die Produktkategorie auswählen, z. B. "Autos", und dann neben jedem Produkt auf **Zum Warenkorb** hinzufügen klicken.  
   Im Warenkorb wird das ausgewählte Produkt angezeigt.
6. Klicken Sie auf die **PayPal-Schaltfläche,** um zur Kasse zu schauen. 

    ![Kasse und Zahlung mit PayPal - Cart](checkout-and-payment-with-paypal/_static/image20.png)

   Für das Auschecken müssen Sie über ein Benutzerkonto für die Wingtip Toys-Beispielanwendung verfügen.
7. Klicken Sie auf den **Google-Link** auf der rechten Seite der Seite, um sich mit einem vorhandenen gmail.com-E-Mail-Konto anzumelden.  
   Wenn Sie kein gmail.com Konto haben, können Sie ein Konto zu Testzwecken [unter www.gmail.com](https://www.gmail.com/)erstellen. Sie können auch ein lokales Standardkonto verwenden, indem Sie auf "Registrieren" klicken. 

    ![Checkout und Zahlung mit PayPal - Anmelden](checkout-and-payment-with-paypal/_static/image21.png)
8. Melden Sie sich mit Ihrem Gmail-Konto und Passwort an. 

    ![Checkout und Zahlung mit PayPal - Gmail Anmelden](checkout-and-payment-with-paypal/_static/image22.png)
9. Klicken Sie auf die Schaltfläche **Anmelden,** um Ihr Gmail-Konto mit Ihrem Wingtip Toys-Beispielanwendungsbenutzernamen zu registrieren. 

    ![Auschecken und Bezahlen mit PayPal - Konto registrieren](checkout-and-payment-with-paypal/_static/image23.png)
10. Fügen Sie auf der PayPal-Testwebsite Ihre Käufer-E-Mail-Adresse und Ihr Kennwort hinzu, die Sie zuvor in diesem Tutorial erstellt haben, und klicken Sie dann auf die Schaltfläche **Anmelden.** **buyer** 

    ![Checkout und Zahlung mit PayPal - PayPal anmelden](checkout-and-payment-with-paypal/_static/image24.png)
11. Stimmen Sie der PayPal-Richtlinie zu und klicken Sie auf die Schaltfläche **"Zustimmen" und "Weiter".**  
    Beachten Sie, dass diese Seite nur angezeigt wird, wenn Sie dieses PayPal-Konto zum ersten Mal verwenden. Beachten Sie nochmals, dass dies ein Testkonto ist, kein echtes Geld wird umgetauscht. 

    ![Checkout und Zahlung mit PayPal - PayPal-Richtlinien](checkout-and-payment-with-paypal/_static/image25.png)
12. Überprüfen Sie die Bestellinformationen auf der Überprüfungsseite der PayPal-Testumgebung, und klicken Sie auf **Weiter**. 

    ![Checkout und Zahlung mit PayPal - Informationen überprüfen](checkout-and-payment-with-paypal/_static/image26.png)
13. Überprüfen Sie auf der Seite *CheckoutReview.aspx* den Bestellbetrag, und zeigen Sie die generierte Lieferadresse an. Klicken Sie dann auf die Schaltfläche **Bestellung abschließen.** 

    ![Checkout und Zahlung mit PayPal - Bestellüberprüfung](checkout-and-payment-with-paypal/_static/image27.png)
14. Die Seite **CheckoutComplete.aspx** wird mit einer Zahlungstransaktions-ID angezeigt. 

    ![Checkout und Zahlung mit PayPal - Checkout abgeschlossen](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Überprüfen der Datenbank

Wenn Sie die aktualisierten Daten in der Wingtip Toys-Beispielanwendungsdatenbank nach dem Ausführen der Anwendung überprüfen, können Sie sehen, dass die Anwendung den Kauf der Produkte erfolgreich aufgezeichnet hat.

Sie können die in der Datenbankdatei *Wingtiptoys.mdf* enthaltenen Daten mithilfe des **Fensters Datenbank-Explorer** **(Fenster Server-Explorer** in Visual Studio) überprüfen, wie Sie es zuvor in dieser Lernprogrammreihe getan haben.

1. Schließen Sie das Browserfenster, wenn es noch geöffnet ist.
2. Wählen Sie in Visual Studio oben im **Projektmappen-Explorer** das Symbol **Alle Dateien** anzeigen aus, damit Sie den Ordner **App-Daten\_** erweitern können.
3. Erweitern Sie den Ordner **App-Daten.\_**  
 Möglicherweise müssen Sie das Symbol **Alle Dateien** anzeigen für den Ordner auswählen.
4. Klicken Sie mit der rechten Maustaste auf die Datenbankdatei *Wingtiptoys.mdf,* und wählen Sie **Öffnen**aus.  
    **Server Explorer** wird angezeigt.
5. Erweitern Sie den Ordner **Tabellen** .
6. Klicken Sie mit der rechten Maustaste auf die Tabelle **"Bestellungen",** und wählen Sie **Tabellendaten anzeigen**aus.  
 Die Tabelle **"Orders"** wird angezeigt.
7. Überprüfen Sie die Spalte **PaymentTransactionID,** um erfolgreiche Transaktionen zu bestätigen. 

    ![Checkout und Zahlung mit PayPal - Testdatenbank](checkout-and-payment-with-paypal/_static/image29.png)
8. Schließen Sie das Tabellenfenster **"Orders".**
9. Klicken Sie im Server-Explorer mit der rechten Maustaste auf die Tabelle **OrderDetails,** und wählen Sie **Tabellendaten anzeigen**aus.
10. Überprüfen `OrderId` Sie `Username` die und-Werte in der Tabelle **OrderDetails.** Beachten Sie, dass `OrderId` `Username` diese Werte mit den und Werten übereinstimmen, die in der Tabelle **"Orders"** enthalten sind.
11. Schließen Sie das Tabellenfenster **OrderDetails.**
12. Klicken Sie mit der rechten Maustaste auf die Wingtip Toys-Datenbankdatei (*Wingtiptoys.mdf*) und wählen **Sie Verbindung schließen**aus.
13. Wenn das **Projektmappen-Explorer-Fenster** nicht angezeigt wird, klicken Sie unten im **Fenster Server-Explorer** auf **Projektmappen-Explorer,** um den **Projektmappen-Explorer** erneut anzuzeigen.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie Auftrags- und Bestelldetailschemas hinzugefügt, um den Kauf von Produkten nachzuverfolgen. Sie haben auch die PayPal-Funktionalität in die Wingtip Toys-Beispielanwendung integriert.

## <a name="additional-resources"></a>Weitere Ressourcen

[ASP.NET-Konfigurationsübersicht](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Bereitstellen einer Secure ASP.NET Web Forms App mit Mitgliedschaft, OAuth und SQL-Datenbank in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure – Kostenlose Testversion](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Haftungsausschluss

Dieses Tutorial enthält Beispielcode. Dieser Beispielcode wird "wie besehen" ohne jegliche Gewährleistung bereitgestellt. Dementsprechend übernimmt Microsoft keine Garantie für die Genauigkeit, Integrität oder Qualität des Beispielcodes. Sie erklären sich damit einverstanden, den Beispielcode auf eigenes Risiko zu verwenden. Unter keinen Umständen haftet Microsoft Ihnen gegenüber in irgendeiner Weise für Beispielcode, Inhalte, einschließlich, aber nicht beschränkt auf Fehler oder Auslassungen in Beispielcode, Inhalt oder Verluste oder Schäden jeglicher Art, die durch die Verwendung von Beispielcode entstehen. Sie werden hiermit benachrichtigt und erklären sich hiermit damit einverstanden, Microsoft von jeglichem Verlust, Verlust, Verletzungen oder Schäden jeglicher Art, einschließlich, aber nicht beschränkt auf Daseinsionen, die durch Material, das Sie posten, übertragen, verwenden oder auf das Sie sich verlassen, zu entschädigen, zu speichern und zu halten, einschließlich, aber nicht beschränkt auf die darin geäußerten Ansichten.

> [!div class="step-by-step"]
> [Zurück](shopping-cart.md)
> [Weiter](membership-and-administration.md)
