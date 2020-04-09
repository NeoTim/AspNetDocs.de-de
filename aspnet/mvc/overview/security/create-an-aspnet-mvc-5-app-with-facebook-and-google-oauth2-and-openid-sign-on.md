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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="7712b-103">Erstellen einer ASP.NET MVC 5-App mit Facebook, Twitter, LinkedIn und Google OAuth2-Anmeldung (C#)</span><span class="sxs-lookup"><span data-stu-id="7712b-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="7712b-104">von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7712b-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="7712b-105">In diesem Tutorial erfahren Sie, wie Sie eine ASP.NET MVC 5-Webanwendung erstellen, mit der sich Benutzer mit [OAuth 2.0](http://oauth.net/2/) mit Anmeldeinformationen eines externen Authentifizierungsanbieters wie Facebook, Twitter, LinkedIn, Microsoft oder Google anmelden können.</span><span class="sxs-lookup"><span data-stu-id="7712b-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="7712b-106">Der Einfachheit halber konzentriert sich dieses Tutorial auf die Arbeit mit Anmeldeinformationen von Facebook und Google.</span><span class="sxs-lookup"><span data-stu-id="7712b-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="7712b-107">Das Aktivieren dieser Anmeldeinformationen auf Ihren Websites bietet einen erheblichen Vorteil, da Millionen von Benutzern bereits Konten bei diesen externen Anbietern haben.</span><span class="sxs-lookup"><span data-stu-id="7712b-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="7712b-108">Diese Benutzer sind möglicherweise eher geneigt, sich für Ihre Website anzumelden, wenn sie keine neuen Anmeldeinformationen erstellen und sich merken müssen.</span><span class="sxs-lookup"><span data-stu-id="7712b-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="7712b-109">Siehe auch [ASP.NET MVC 5-App mit SMS und E-Mail-Zwei-Faktor-Authentifizierung](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7712b-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="7712b-110">Das Tutorial zeigt auch, wie Profildaten für den Benutzer hinzugefügt werden und wie die Mitgliedschafts-API zum Hinzufügen von Rollen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7712b-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="7712b-111">Dieses Tutorial wurde von [Rick Anderson](https://blogs.msdn.com/rickAndy) geschrieben [@RickAndMSFT](https://twitter.com/RickAndMSFT) ( Bitte folgen Sie mir auf Twitter: ).</span><span class="sxs-lookup"><span data-stu-id="7712b-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="7712b-112">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="7712b-112">Getting Started</span></span>

<span data-ttu-id="7712b-113">Beginnen Sie mit der Installation und Ausführung von [Visual Studio Express 2013 für Web](https://go.microsoft.com/fwlink/?LinkId=299058) oder Visual Studio [2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="7712b-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="7712b-114">Installieren Sie Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) oder höher.</span><span class="sxs-lookup"><span data-stu-id="7712b-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="7712b-115">Hilfe zu Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo! und mehr finden Sie in diesem [Beispielprojekt](https://github.com/matthewdunsdon/oauthforaspnet).</span><span class="sxs-lookup"><span data-stu-id="7712b-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="7712b-116">Sie müssen Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) oder höher installieren, um Google OAuth 2 zu verwenden und lokal ohne SSL-Warnungen zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="7712b-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="7712b-117">Klicken Sie auf der **Startseite** auf **Neues Projekt,** oder Sie können das Menü verwenden und **Datei**auswählen und dann **Neues Projekt**.</span><span class="sxs-lookup"><span data-stu-id="7712b-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="7712b-118">Erstellen Ihrer ersten Anwendung</span><span class="sxs-lookup"><span data-stu-id="7712b-118">Creating Your First Application</span></span>

<span data-ttu-id="7712b-119">Klicken Sie auf **Neues Projekt**, und wählen Sie dann auf der linken Seite **Visual C-** aus, dann **Web,** und wählen Sie dann **ASP.NET Webanwendung**aus.</span><span class="sxs-lookup"><span data-stu-id="7712b-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="7712b-120">Benennen Sie Ihr Projekt "MvcAuth" und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7712b-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="7712b-121">Klicken Sie im Dialogfeld **Neues ASP.NET Projekt** auf **MVC**.</span><span class="sxs-lookup"><span data-stu-id="7712b-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="7712b-122">Wenn es sich bei der Authentifizierung nicht um **einzelne Benutzerkonten handelt,** klicken Sie auf die Schaltfläche **Authentifizierung ändern,** und wählen Sie **Einzelne Benutzerkonten**aus.</span><span class="sxs-lookup"><span data-stu-id="7712b-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="7712b-123">Durch Überprüfen von **Host in der Cloud**ist die App sehr einfach in Azure zu hosten.</span><span class="sxs-lookup"><span data-stu-id="7712b-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="7712b-124">Wenn Sie **Host in der Cloud**ausgewählt haben, schließen Sie das Dialogfeld Konfigurieren ab.</span><span class="sxs-lookup"><span data-stu-id="7712b-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="7712b-125">Verwenden Sie NuGet, um auf die neueste OWIN-Middleware zu aktualisieren</span><span class="sxs-lookup"><span data-stu-id="7712b-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="7712b-126">Verwenden Sie den NuGet-Paket-Manager, um die [OWIN-Middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="7712b-127">Wählen Sie **Updates** im linken Menü aus.</span><span class="sxs-lookup"><span data-stu-id="7712b-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="7712b-128">Sie können auf die Schaltfläche **Alle aktualisieren** klicken oder nur nach OWIN-Paketen suchen (siehe nächstes Bild):</span><span class="sxs-lookup"><span data-stu-id="7712b-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="7712b-129">In der Folgenden Abbildung werden nur OWIN-Pakete angezeigt:</span><span class="sxs-lookup"><span data-stu-id="7712b-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="7712b-130">Über die Package Manager Console (PMC) können Sie den `Update-Package` Befehl eingeben, mit dem alle Pakete aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="7712b-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="7712b-131">Drücken Sie **F5** oder **Strg+F5,** um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7712b-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="7712b-132">In der Abbildung unten ist die Portnummer 1234.</span><span class="sxs-lookup"><span data-stu-id="7712b-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="7712b-133">Wenn Sie die Anwendung ausführen, wird eine andere Portnummer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7712b-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="7712b-134">Abhängig von der Größe Ihres Browserfensters müssen Sie möglicherweise auf das Navigationssymbol klicken, um die Links **Home**, **About**, **Kontakt**, **Registrieren** und **Anmelden** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7712b-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="7712b-135">Einrichten von SSL im Projekt</span><span class="sxs-lookup"><span data-stu-id="7712b-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="7712b-136">Um eine Verbindung mit Authentifizierungsanbietern wie Google und Facebook herzustellen, müssen Sie IIS-Express für die Verwendung von SSL einrichten.</span><span class="sxs-lookup"><span data-stu-id="7712b-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="7712b-137">Es ist wichtig, SSL nach der Anmeldung zu verwenden und nicht auf HTTP zurückzuwerfen, Ihr Login-Cookie ist genauso geheim wie Ihr Benutzername und Passwort, und ohne SSL senden Sie es im Klartext über den Draht.</span><span class="sxs-lookup"><span data-stu-id="7712b-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="7712b-138">Außerdem haben Sie sich bereits die Zeit genommen, den Handshake auszuführen und den Kanal zu sichern (was den Großteil dessen ausmacht, was HTTPS langsamer als HTTP macht), bevor die MVC-Pipeline ausgeführt wird, sodass die Umleitung zurück zu HTTP, nachdem Sie angemeldet sind, die aktuelle Anforderung oder zukünftige Anforderungen nicht viel schneller macht.</span><span class="sxs-lookup"><span data-stu-id="7712b-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="7712b-139">Klicken Sie im **Projektmappen-Explorer**auf das **MvcAuth-Projekt.**</span><span class="sxs-lookup"><span data-stu-id="7712b-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="7712b-140">Klicken Sie auf die F4-Taste, um die Projekteigenschaften anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7712b-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="7712b-141">Alternativ können Sie im **Menü Ansicht** **Eigenschaftenfenster**auswählen.</span><span class="sxs-lookup"><span data-stu-id="7712b-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="7712b-142">Ändern Sie **SSL Aktiviert** in True.</span><span class="sxs-lookup"><span data-stu-id="7712b-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="7712b-143">Kopieren Sie die SSL-URL `https://localhost:44300/` (sofern Sie keine anderen SSL-Projekte erstellt haben).</span><span class="sxs-lookup"><span data-stu-id="7712b-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="7712b-144">Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das **MvcAuth-Projekt,** und wählen Sie **Eigenschaften**aus.</span><span class="sxs-lookup"><span data-stu-id="7712b-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="7712b-145">Wählen Sie die **Registerkarte Web** aus, und fügen Sie dann die SSL-URL in das Feld **Projekt-URL** ein.</span><span class="sxs-lookup"><span data-stu-id="7712b-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="7712b-146">Speichern Sie die Datei (Ctl+S).</span><span class="sxs-lookup"><span data-stu-id="7712b-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="7712b-147">Sie benötigen diese URL, um Facebook- und Google-Authentifizierungs-Apps zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="7712b-148">Fügen Sie dem `Home` Controller das [RequireHttps-Attribut](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hinzu, damit alle Anforderungen HTTPS verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="7712b-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="7712b-149">Ein sichererer Ansatz besteht darin, der Anwendung den [RequireHttps-Filter](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7712b-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="7712b-150">Lesen Sie &quot;den Abschnitt Schützen Sie&quot; die Anwendung mit SSL und das Authorize-Attribut in meinem Tutorial [Erstellen Sie eine ASP.NET MVC-App mit auth und SQL DB, und stellen Sie sie in Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)bereit.</span><span class="sxs-lookup"><span data-stu-id="7712b-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="7712b-151">Ein Teil des Home-Controllers ist unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7712b-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="7712b-152">Drücken Sie STRG+F5, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7712b-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="7712b-153">Wenn Sie das Zertifikat in der Vergangenheit installiert haben, können Sie den Rest dieses Abschnitts überspringen und zu [Erstellen einer Google-App für OAuth 2 und Verbinden der App mit dem Projekt springen.](#goog)Andernfalls befolgen Sie die Anweisungen, um dem selbstsignierten Zertifikat zu vertrauen, das IIS Express generiert hat.</span><span class="sxs-lookup"><span data-stu-id="7712b-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="7712b-154">Lesen Sie das Dialogfeld **Sicherheitswarnung,** und klicken Sie dann auf **Ja,** wenn Sie das Zertifikat installieren möchten, das localhost darstellt.</span><span class="sxs-lookup"><span data-stu-id="7712b-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="7712b-155">Die Seite *Home* wird in IE angezeigt, und es gibt keine SSL-Warnungen.</span><span class="sxs-lookup"><span data-stu-id="7712b-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="7712b-156">Google Chrome akzeptiert auch das Zertifikat und zeigt HTTPS-Inhalte ohne Warnung an.</span><span class="sxs-lookup"><span data-stu-id="7712b-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="7712b-157">Firefox verwendet einen eigenen Zertifikatspeicher, sodass eine Warnung angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7712b-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="7712b-158">Für unsere Anwendung können Sie sicher auf **I Understand the Risks**klicken.</span><span class="sxs-lookup"><span data-stu-id="7712b-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="7712b-159">Erstellen einer Google-App für OAuth 2 und Verbinden der App mit dem Projekt</span><span class="sxs-lookup"><span data-stu-id="7712b-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="7712b-160">Aktuelle Google OAuth-Anweisungen finden Sie unter [Konfigurieren der Google-Authentifizierung in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span><span class="sxs-lookup"><span data-stu-id="7712b-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="7712b-161">Navigieren Sie zur [Google Developers Console](https://console.developers.google.com/).</span><span class="sxs-lookup"><span data-stu-id="7712b-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="7712b-162">Wenn Sie noch kein Projekt erstellt haben, wählen Sie **Anmeldeinformationen** auf der linken Registerkarte aus, und wählen Sie dann **Erstellen**aus.</span><span class="sxs-lookup"><span data-stu-id="7712b-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="7712b-163">Klicken Sie auf der linken Registerkarte auf **Anmeldeinformationen**.</span><span class="sxs-lookup"><span data-stu-id="7712b-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="7712b-164">Klicken Sie **auf Anmeldeinformationen erstellen** und dann auf **OAuth-Client-ID**.</span><span class="sxs-lookup"><span data-stu-id="7712b-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="7712b-165">Behalten Sie im Dialogfeld **Client-ID erstellen** die **Standardwebanwendung** für den Anwendungstyp bei.</span><span class="sxs-lookup"><span data-stu-id="7712b-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="7712b-166">Legen Sie die **Authorized JavaScript-Ursprünge** auf`https://localhost:44300/` die oben verwendete SSL-URL fest (es sei denn, Sie haben andere SSL-Projekte erstellt)</span><span class="sxs-lookup"><span data-stu-id="7712b-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="7712b-167">Legen Sie den **AUTHORIZED Redirect URI** auf:</span><span class="sxs-lookup"><span data-stu-id="7712b-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="7712b-168">Klicken Sie auf den Menüpunkt OAuth Consent, und legen Sie dann Ihre E-Mail-Adresse und Ihren Produktnamen fest.</span><span class="sxs-lookup"><span data-stu-id="7712b-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="7712b-169">Wenn Sie das Formular ausgefüllt haben, klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="7712b-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="7712b-170">Klicken Sie auf das Menüelement Bibliothek, suchen Sie **nach Google+ API**, klicken Sie darauf und drücken Sie aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="7712b-171">Das Bild unten zeigt die aktivierten APIs.</span><span class="sxs-lookup"><span data-stu-id="7712b-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="7712b-172">Besuchen Sie im Google APIs API Manager die Registerkarte **Anmeldeinformationen,** um die **Client-ID**zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7712b-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="7712b-173">Laden Sie diese Datei herunter, um eine JSON-Datei mit Anwendungsgeheimnissen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="7712b-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="7712b-174">Kopieren Sie die **ClientId** und `UseGoogleAuthentication` **ClientSecret** und fügen Sie sie in die Methode ein, die in der *Startup.Auth.cs* Datei im *Ordner App_Start* gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="7712b-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="7712b-175">Die unten gezeigten **ClientId-** und **ClientSecret-Werte** sind Beispiele und funktionieren nicht.</span><span class="sxs-lookup"><span data-stu-id="7712b-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="7712b-176">Sicherheit - Speichern Sie niemals vertrauliche Daten in Ihrem Quellcode.</span><span class="sxs-lookup"><span data-stu-id="7712b-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="7712b-177">Das Konto und die Anmeldeinformationen werden dem obigen Code hinzugefügt, um das Beispiel einfach zu halten.</span><span class="sxs-lookup"><span data-stu-id="7712b-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="7712b-178">Weitere Informationen finden Sie unter [Bewährte Methoden zum Bereitstellen von Kennwörtern und anderen vertraulichen Daten in ASP.NET und Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="7712b-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="7712b-179">Drücken Sie **STRG+F5,** um die Anwendung zu erstellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7712b-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="7712b-180">Klicken Sie auf den Link **Log in** .</span><span class="sxs-lookup"><span data-stu-id="7712b-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="7712b-181">Klicken Sie unter **Einen anderen Dienst zum Anmelden**verwenden auf **Google**.</span><span class="sxs-lookup"><span data-stu-id="7712b-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="7712b-182">Wenn Sie einen der oben genannten Schritte verpassen, erhalten Sie einen HTTP 401-Fehler.</span><span class="sxs-lookup"><span data-stu-id="7712b-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="7712b-183">Überprüfen Sie Ihre schritte oben erneut.</span><span class="sxs-lookup"><span data-stu-id="7712b-183">Recheck your steps above.</span></span> <span data-ttu-id="7712b-184">Wenn Sie eine erforderliche Einstellung (z. B. **Produktname)** verfehlen, fügen Sie den fehlenden Artikel hinzu und speichern Sie es. Es kann einige Minuten dauern, bis die Authentifizierung funktioniert.</span><span class="sxs-lookup"><span data-stu-id="7712b-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="7712b-185">Sie werden auf die Google-Website weitergeleitet, auf der Sie Ihre Anmeldeinformationen eingeben.</span><span class="sxs-lookup"><span data-stu-id="7712b-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="7712b-186">Nachdem Sie Ihre Anmeldeinformationen eingegeben haben, werden Sie aufgefordert, Berechtigungen für die soeben erstellten Webanwendung zu erteilen: </span><span class="sxs-lookup"><span data-stu-id="7712b-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="7712b-187">Klicken Sie auf **Annehmen**.</span><span class="sxs-lookup"><span data-stu-id="7712b-187">Click **Accept**.</span></span> <span data-ttu-id="7712b-188">Sie werden nun zurück zur **Registrierungsseite** der MvcAuth-Anwendung weitergeleitet, wo Sie Ihr Google-Konto registrieren können.</span><span class="sxs-lookup"><span data-stu-id="7712b-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="7712b-189">Sie können zwar den lokalen E-Mail-Registrierungsnamen in Ihr Gmail-Konto ändern, im Allgemeinen sollten Sie jedoch den Standard-E-Mail-Aliasnamen beibehalten (den Sie für die Authentifizierung verwendet haben).</span><span class="sxs-lookup"><span data-stu-id="7712b-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="7712b-190">Klicken Sie auf **Registrieren**.</span><span class="sxs-lookup"><span data-stu-id="7712b-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="7712b-191">Erstellen der App in Facebook und Verbinden der App mit dem Projekt</span><span class="sxs-lookup"><span data-stu-id="7712b-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="7712b-192">Aktuelle Anweisungen zur Facebook OAuth2-Authentifizierung finden Sie unter [Konfigurieren der Facebook-Authentifizierung](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="7712b-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="7712b-193">Untersuchen der Mitgliedschaftsdaten</span><span class="sxs-lookup"><span data-stu-id="7712b-193">Examine the Membership Data</span></span>

<span data-ttu-id="7712b-194">Klicken Sie im Menü **Ansicht** auf **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7712b-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="7712b-195">Erweitern Sie **DefaultConnection (MvcAuth),** erweitern **Sie Tabellen**, klicken Sie mit der rechten Maustaste auf **AspNetUsers,** und klicken Sie auf **Tabellendaten anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="7712b-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![Aspnetusers-Tabellendaten](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="7712b-197">Hinzufügen von Profildaten zur Benutzerklasse</span><span class="sxs-lookup"><span data-stu-id="7712b-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="7712b-198">In diesem Abschnitt fügen Sie den Benutzerdaten während der Registrierung Geburtsdatum und Heimatstadt hinzu, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7712b-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![reg mit Heimatstadt und Bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="7712b-200">Öffnen Sie die Datei *Models-IdentityModels.cs,* und fügen Sie Geburtsdatum und Heimatstadteigenschaften hinzu:</span><span class="sxs-lookup"><span data-stu-id="7712b-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="7712b-201">Öffnen Sie die Datei *Models-AccountViewModels.cs* und die `ExternalLoginConfirmationViewModel`festgelegten Geburtsdatums- und Heimatstadteigenschaften in .</span><span class="sxs-lookup"><span data-stu-id="7712b-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="7712b-202">Öffnen Sie die Datei *Controllers-AccountController.cs,* und fügen `ExternalLoginConfirmation` Sie Code für Geburtsdatum und Heimatstadt in der Aktionsmethode hinzu, wie gezeigt:</span><span class="sxs-lookup"><span data-stu-id="7712b-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="7712b-203">Fügen Sie Geburtsdatum und Heimatstadt zur Datei *Views-Konto-ExternalLoginConfirmation.cshtml hinzu:*</span><span class="sxs-lookup"><span data-stu-id="7712b-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="7712b-204">Löschen Sie die Mitgliedschaftsdatenbank, damit Sie Ihr Facebook-Konto erneut bei Ihrer Bewerbung registrieren können und überprüfen Sie, ob Sie das neue Geburtsdatum und die Profilinformationen der Heimatstadt hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="7712b-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="7712b-205">Klicken Sie im **Projektmappen-Explorer**auf das Symbol **Alle Dateien anzeigen,** und klicken Sie dann **Delete**mit der rechten Maustaste auf *Daten hinzufügen.\_&lt;&gt;*</span><span class="sxs-lookup"><span data-stu-id="7712b-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="7712b-206">Klicken Sie im Menü **Extras** auf **NuGet Package Manger**, und klicken Sie dann auf **Package Manager Console** (PMC).</span><span class="sxs-lookup"><span data-stu-id="7712b-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="7712b-207">Geben Sie die folgenden Befehle in die PMC ein.</span><span class="sxs-lookup"><span data-stu-id="7712b-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="7712b-208">Enable-Migrations</span><span class="sxs-lookup"><span data-stu-id="7712b-208">Enable-Migrations</span></span>
2. <span data-ttu-id="7712b-209">Add-Migration Init</span><span class="sxs-lookup"><span data-stu-id="7712b-209">Add-Migration Init</span></span>
3. <span data-ttu-id="7712b-210">Update-Datenbank</span><span class="sxs-lookup"><span data-stu-id="7712b-210">Update-Database</span></span>

<span data-ttu-id="7712b-211">Führen Sie die Anwendung aus und verwenden Sie FaceBook und Google, um sich anzumelden und einige Benutzer zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="7712b-212">Untersuchen der Mitgliedschaftsdaten</span><span class="sxs-lookup"><span data-stu-id="7712b-212">Examine the Membership Data</span></span>

<span data-ttu-id="7712b-213">Klicken Sie im Menü **Ansicht** auf **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7712b-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="7712b-214">Klicken Sie mit der rechten Maustaste auf **AspNetUsers,** und klicken Sie auf **Tabellendaten anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="7712b-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="7712b-215">Die `HomeTown` `BirthDate` Felder und felder sind unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7712b-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="7712b-216">Abmelden Ihrer App und Anmelden mit einem anderen Konto</span><span class="sxs-lookup"><span data-stu-id="7712b-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="7712b-217">Wenn Sie sich mit Facebook bei Ihrer App anmelden und sich dann abmelden und versuchen, sich erneut mit einem anderen Facebook-Konto anzumelden (mit demselben Browser), werden Sie sofort in das vorherige Facebook-Konto eingeloggt, das Sie verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="7712b-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="7712b-218">Um ein anderes Konto zu nutzen, musst du zu Facebook navigieren und dich bei Facebook ausloggen.</span><span class="sxs-lookup"><span data-stu-id="7712b-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="7712b-219">Die gleiche Regel gilt für alle anderen Drittanbieter-Authentifizierungsanbieter.</span><span class="sxs-lookup"><span data-stu-id="7712b-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="7712b-220">Alternativ können Sie sich mit einem anderen Konto anmelden, indem Sie einen anderen Browser verwenden.</span><span class="sxs-lookup"><span data-stu-id="7712b-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7712b-221">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7712b-221">Next Steps</span></span>

<span data-ttu-id="7712b-222">Weitere Informationen finden [Sie unter Einführung in die Anweisungen zu den Sicherheitsanbietern Yahoo und LinkedIn OAuth für OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) von Jerrie Pelser für Yahoo und LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="7712b-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="7712b-223">Siehe Jerries Pretty Social Login Buttons für ASP.NET MVC 5, um Social Login-Buttons zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="7712b-224">Folgen Sie meinem Tutorial [Erstellen Sie eine ASP.NET MVC-App mit auth und SQL DB, und stellen Sie sie in Azure App Service bereit,](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)das dieses Tutorial fortsetzt und Folgendes zeigt:</span><span class="sxs-lookup"><span data-stu-id="7712b-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="7712b-225">So stellen Sie Ihre App in Azure bereit.</span><span class="sxs-lookup"><span data-stu-id="7712b-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="7712b-226">So sichern Sie Ihre App mit Rollen.</span><span class="sxs-lookup"><span data-stu-id="7712b-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="7712b-227">So sichern Sie Ihre App mit den Filtern [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) und [Authorize.](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="7712b-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="7712b-228">Verwenden der Mitgliedschafts-API zum Hinzufügen von Benutzern und Rollen.</span><span class="sxs-lookup"><span data-stu-id="7712b-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="7712b-229">Bitte hinterlassen Sie Feedback darüber, wie Ihnen dieses Tutorial gefallen hat und was wir verbessern könnten.</span><span class="sxs-lookup"><span data-stu-id="7712b-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="7712b-230">Sie können auch neue Themen unter [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)anfordern.</span><span class="sxs-lookup"><span data-stu-id="7712b-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="7712b-231">Sie können sogar um neue Funktionen bitten und abstimmen, die ASP.NET hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7712b-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="7712b-232">Sie können z. B. für ein Tool zum Erstellen und Verwalten von [Benutzern und Rollen stimmen.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="7712b-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="7712b-233">Eine gute Erklärung zur Funktionsweise ASP.NET Externe Authentifizierungsdienste finden Sie unter Robert McMurray es [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span><span class="sxs-lookup"><span data-stu-id="7712b-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="7712b-234">Roberts Artikel geht auch ins Detail, um die Microsoft- und Twitter-Authentifizierung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="7712b-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="7712b-235">Tom Dykstras ausgezeichnetes [EF/MVC-Tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) zeigt, wie sie mit dem Entity Framework arbeiten.</span><span class="sxs-lookup"><span data-stu-id="7712b-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
