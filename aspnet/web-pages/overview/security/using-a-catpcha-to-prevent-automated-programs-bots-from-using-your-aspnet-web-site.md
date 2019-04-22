---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Verwenden ein CAPTCHA, um zu verhindern, dass Bots mit Ihrer ASP.NET-Webanwendung Razor) Standort | Microsoft-Dokumentation
author: microsoft
description: In diesem Artikel wird erläutert, wie ReCaptcha (Dies ist eine Sicherheitsmaßnahme) verwenden, um zu verhindern, dass die automatisierten Programmen (Bots) Ausführen von Aufgaben in einer ASP.NET Web Pages (Razor) wir...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: e7baafda8c5b6de4ab0de46948f969a6f0cc21ad
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59390908"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="7e408-103">Verwenden ein CAPTCHA, um zu verhindern, dass Bots mit Ihrer ASP.NET-Webanwendung Razor) Standort</span><span class="sxs-lookup"><span data-stu-id="7e408-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="7e408-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7e408-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7e408-105">In diesem Artikel wird erläutert, wie ReCaptcha (Dies ist eine Sicherheitsmaßnahme) verwenden, um zu verhindern, dass die automatisierten Programmen (Bots) Ausführen von Aufgaben in einer ASP.NET Web Pages (Razor)-Website wird.</span><span class="sxs-lookup"><span data-stu-id="7e408-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="7e408-106">**Sie lernen Folgendes:**</span><span class="sxs-lookup"><span data-stu-id="7e408-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="7e408-107">Wie Ihre Website einen CAPTCHA-Test hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7e408-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="7e408-108">Dies sind die Funktionen von ASP.NET in diesem Artikel:</span><span class="sxs-lookup"><span data-stu-id="7e408-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="7e408-109">Die `ReCaptcha` Helper.</span><span class="sxs-lookup"><span data-stu-id="7e408-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="7e408-110">Die Informationen in diesem Artikel gelten für ASP.NET Web Pages-1.0- und Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="7e408-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>


## <a name="about-captchas"></a><span data-ttu-id="7e408-111">Informationen zu CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="7e408-111">About CAPTCHAs</span></span>

<span data-ttu-id="7e408-112">Geben Sie jedes Mal, die Sie an Ihrem Standort oder sogar nur Personen registrieren können, einen Namen und eine URL (z.B. für einen Blogkommentar), erhalten Sie möglicherweise eine Flut von gefälschten Namen.</span><span class="sxs-lookup"><span data-stu-id="7e408-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="7e408-113">Diese werden häufig von automatisierten Programmen (Bots) beibehalten, die versuchen, die URLs auf jeder Website verlassen, die sie finden können.</span><span class="sxs-lookup"><span data-stu-id="7e408-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="7e408-114">(Eine allgemeine Motivation ist die URLs der Produkte für den Verkauf veröffentlichen.)</span><span class="sxs-lookup"><span data-stu-id="7e408-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="7e408-115">Sie können sicherstellen, dass ein Benutzer mit realen Person "und" nicht in einem Computerprogramm ist eine *CAPTCHA* zum valideren von Benutzern beim Registrieren oder andernfalls geben Sie ihren Namen und den Standort.</span><span class="sxs-lookup"><span data-stu-id="7e408-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="7e408-116">CAPTCHA steht für Öffentliche Turing vollständig automatisierten Test anzuweisen, Computer und Menschen auseinander liegen.</span><span class="sxs-lookup"><span data-stu-id="7e408-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="7e408-117">Ein CAPTCHA ist eine *Abfrage / Rückmeldung-* Test in der der Benutzer aufgefordert, etwas zu tun, die einfach für eine Person Sie jedoch für eine automatisierte Programm schwierig ist.</span><span class="sxs-lookup"><span data-stu-id="7e408-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="7e408-118">Die am häufigsten verwendete Typ der CAPTCHA ist, in dem Sie finden Sie einige verzerrten Buchstaben und werden zur Eingabe aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="7e408-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="7e408-119">(Die Verzerrung sollte um für Bots, die Buchstaben entschlüsseln schwer zu erleichtern.)</span><span class="sxs-lookup"><span data-stu-id="7e408-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="7e408-120">Hinzufügen eines ReCaptcha-Tests</span><span class="sxs-lookup"><span data-stu-id="7e408-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="7e408-121">In ASP.NET-Seiten können Sie mithilfe der `ReCaptcha` Hilfsmethode zum einen CAPTCHA-Test zu rendern, die basierend auf den ReCaptcha-Dienst ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="7e408-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="7e408-122">Die `ReCaptcha` Hilfsprogramm zeigt ein Bild von zwei verzerrt Wörtern, die Benutzer sich nicht ordnungsgemäß eingeben, bevor die Seite überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="7e408-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="7e408-123">Die Antwort des Benutzers wird durch den Dienst ReCaptcha.Net überprüft.</span><span class="sxs-lookup"><span data-stu-id="7e408-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="7e408-124">Registrieren Sie Ihre Website in ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="7e408-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="7e408-125">Wenn Sie die Registrierung abgeschlossen haben, erhalten Sie einen öffentlichen Schlüssel und einen privaten Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="7e408-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="7e408-126">Die ASP.NET Web Helpers Library zu Ihrer Website hinzufügen, wie in beschrieben [Hilfsprogramme installieren, in einer ASP.NET Web Pages-Website](https://go.microsoft.com/fwlink/?LinkId=252372), sofern Sie noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="7e408-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="7e408-127">Wenn Sie noch keinem  *\_AppStart.cshtml* Datei, erstellen Sie eine Datei namens im Stammordner einer Website  *\_AppStart.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7e408-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="7e408-128">Fügen Sie die folgenden `Recaptcha` Helper-Einstellungen in der  *\_AppStart.cshtml* Datei:</span><span class="sxs-lookup"><span data-stu-id="7e408-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="7e408-129">Legen Sie die `PublicKey` und `PrivateKey` Eigenschaften mit Ihren eigenen öffentlichen und privaten Schlüsseln.</span><span class="sxs-lookup"><span data-stu-id="7e408-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="7e408-130">Speichern Sie die  *\_AppStart.cshtml* Datei, und schließen Sie es.</span><span class="sxs-lookup"><span data-stu-id="7e408-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="7e408-131">Erstellen Sie im Stammordner einer Website, die neue Seite, die mit dem Namen *Recaptcha.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7e408-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="7e408-132">Ersetzen Sie den vorhandenen Inhalt durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="7e408-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="7e408-133">Führen Sie die *Recaptcha.cshtml* Seite in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="7e408-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="7e408-134">Wenn die `PrivateKey` Wert gültig ist, die Seite zeigt das ReCaptcha-Steuerelement und eine Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="7e408-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="7e408-135">Wenn Sie die Schlüssel nicht global in festgelegt hatten  *\_AppStart.html*, die Seite wird eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7e408-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="7e408-136">Geben Sie die Wörter für den Test ein.</span><span class="sxs-lookup"><span data-stu-id="7e408-136">Enter the words for the test.</span></span> <span data-ttu-id="7e408-137">Wenn Sie den Test ReCaptcha übergeben, sehen Sie eine entsprechende Meldung.</span><span class="sxs-lookup"><span data-stu-id="7e408-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="7e408-138">Andernfalls eine Fehlermeldung angezeigt, und die ReCaptcha-Steuerelement wird erneut angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7e408-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="7e408-139">Wenn der Computer in einer Domäne, die Proxyserver verwendet befindet, müssen Sie möglicherweise konfigurieren die `defaultproxy` Element der *"Web.config"* Datei.</span><span class="sxs-lookup"><span data-stu-id="7e408-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="7e408-140">Das folgende Beispiel zeigt eine *"Web.config"* -Datei mit den `defaultproxy` Element so konfiguriert, dass den ReCaptcha-Dienst funktioniert.</span><span class="sxs-lookup"><span data-stu-id="7e408-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="7e408-141">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7e408-141">Additional Resources</span></span>


- [<span data-ttu-id="7e408-142">Anpassen von standortweite Verhalten für ASP.NET Web Pages-Websites</span><span class="sxs-lookup"><span data-stu-id="7e408-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="7e408-143">ReCaptcha-Website</span><span class="sxs-lookup"><span data-stu-id="7e408-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
