---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Verwenden einer CAPTCHA, um zu verhindern, dass Bots Ihre ASP.NET Web Razor) Website verwenden | Microsoft Docs
author: rick-anderson
description: In diesem Artikel wird erläutert, wie Sie ReCaptcha (eine Sicherheitsmaßnahme) verwenden, um zu verhindern, dass automatisierte Programme (Bots) Aufgaben in einem ASP.NET Webseiten (Razor) ausführen, die wir...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543755"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="d4a14-103">Verwenden einer CAPTCHA, um zu verhindern, dass Bots Ihre ASP.NET Web Razor)-Website verwenden</span><span class="sxs-lookup"><span data-stu-id="d4a14-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="d4a14-104">von [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d4a14-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d4a14-105">In diesem Artikel wird erläutert, wie Sie ReCaptcha (eine Sicherheitsmaßnahme) verwenden, um zu verhindern, dass automatisierte Programme (Bots) Aufgaben auf einer ASP.NET Website (Razor) ausführen.</span><span class="sxs-lookup"><span data-stu-id="d4a14-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="d4a14-106">**Sie lernen Folgendes:**</span><span class="sxs-lookup"><span data-stu-id="d4a14-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="d4a14-107">So fügen Sie Ihrer Website einen CAPTCHA-Test hinzu.</span><span class="sxs-lookup"><span data-stu-id="d4a14-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="d4a14-108">Dies sind die ASP.NET Funktionen, die in dem Artikel eingeführt werden:</span><span class="sxs-lookup"><span data-stu-id="d4a14-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="d4a14-109">Der `ReCaptcha` Helfer.</span><span class="sxs-lookup"><span data-stu-id="d4a14-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="d4a14-110">Die Informationen in diesem Artikel gelten für ASP.NET Webseiten 1.0 und Webseiten 2.</span><span class="sxs-lookup"><span data-stu-id="d4a14-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="d4a14-111">Über CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="d4a14-111">About CAPTCHAs</span></span>

<span data-ttu-id="d4a14-112">Jedes Mal, wenn Sie Personen auf Ihrer Website registrieren lassen oder sogar einfach nur einen Namen und eine URL eingeben (wie für einen Blog-Kommentar), können Sie eine Flut von gefälschten Namen erhalten.</span><span class="sxs-lookup"><span data-stu-id="d4a14-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="d4a14-113">Diese werden oft von automatisierten Programmen (Bots) verlassen, die versuchen, URLs in jeder Website zu verlassen, die sie finden können.</span><span class="sxs-lookup"><span data-stu-id="d4a14-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="d4a14-114">(Eine häufige Motivation ist es, die URLs von Produkten zum Verkauf zu veröffentlichen.)</span><span class="sxs-lookup"><span data-stu-id="d4a14-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="d4a14-115">Sie können sicherstellen, dass ein Benutzer eine echte Person und kein Computerprogramm ist, indem Sie eine *CAPTCHA* verwenden, um Benutzer zu überprüfen, wenn sie sich registrieren oder anderweitig ihren Namen und ihre Website eingeben.</span><span class="sxs-lookup"><span data-stu-id="d4a14-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="d4a14-116">CAPTCHA steht für Completely Automated Public Turing test to tell Computers and Humans Apart.</span><span class="sxs-lookup"><span data-stu-id="d4a14-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="d4a14-117">Ein CAPTCHA ist ein *Challenge-Response-Test,* bei dem der Benutzer aufgefordert wird, etwas zu tun, was für eine Person einfach zu tun ist, aber für ein automatisiertes Programm schwierig ist.</span><span class="sxs-lookup"><span data-stu-id="d4a14-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="d4a14-118">Die häufigste Art von CAPTCHA ist eine, bei der Sie einige verzerrte Buchstaben sehen und aufgefordert werden, sie einzugeben.</span><span class="sxs-lookup"><span data-stu-id="d4a14-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="d4a14-119">(Die Verzerrung soll es Bots schwer machen, die Buchstaben zu entschlüsseln.)</span><span class="sxs-lookup"><span data-stu-id="d4a14-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="d4a14-120">Hinzufügen eines ReCaptcha-Tests</span><span class="sxs-lookup"><span data-stu-id="d4a14-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="d4a14-121">In ASP.NET Seiten können `ReCaptcha` Sie den Helfer verwenden, um einen CAPTCHA-Test[http://recaptcha.net](http://recaptcha.net)zu rendern, der auf dem ReCaptcha-Dienst ( ) basiert.</span><span class="sxs-lookup"><span data-stu-id="d4a14-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="d4a14-122">Der `ReCaptcha` Helfer zeigt ein Bild von zwei verzerrten Wörtern an, die Benutzer korrekt eingeben müssen, bevor die Seite überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="d4a14-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="d4a14-123">Die Benutzerantwort wird vom ReCaptcha.Net-Dienst überprüft.</span><span class="sxs-lookup"><span data-stu-id="d4a14-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="d4a14-124">Registrieren Sie Ihre[http://recaptcha.net](http://recaptcha.net)Website unter ReCaptcha.Net ( ).</span><span class="sxs-lookup"><span data-stu-id="d4a14-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="d4a14-125">Wenn Sie die Registrierung abgeschlossen haben, erhalten Sie einen öffentlichen Schlüssel und einen privaten Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="d4a14-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="d4a14-126">Fügen Sie die ASP.NET Web Helpers Library zu Ihrer Website hinzu, wie unter [Installieren von Helfern in einer ASP.NET Webseitenwebsite](https://go.microsoft.com/fwlink/?LinkId=252372)beschrieben, falls dies noch nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="d4a14-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="d4a14-127">Wenn Sie noch keine \* \_AppStart.cshtml-Datei\* haben, erstellen Sie im Stammordner einer Website eine Datei mit dem Namen \* \_AppStart.cshtml\*.</span><span class="sxs-lookup"><span data-stu-id="d4a14-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="d4a14-128">Fügen Sie `Recaptcha` die folgenden Hilfseinstellungen in der \* \_Datei AppStart.cshtml\* hinzu:</span><span class="sxs-lookup"><span data-stu-id="d4a14-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="d4a14-129">Legen `PublicKey` Sie `PrivateKey` die und Eigenschaften mit Ihren eigenen öffentlichen und privaten Schlüsseln fest.</span><span class="sxs-lookup"><span data-stu-id="d4a14-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="d4a14-130">Speichern Sie die \* \_Datei AppStart.cshtml,\* und schließen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="d4a14-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="d4a14-131">Erstellen Sie im Stammordner einer Website eine neue Seite mit dem Namen *Recaptcha.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="d4a14-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="d4a14-132">Ersetzen Sie den vorhandenen Inhalt durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="d4a14-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="d4a14-133">Führen Sie die Seite *Recaptcha.cshtml* in einem Browser aus.</span><span class="sxs-lookup"><span data-stu-id="d4a14-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="d4a14-134">Wenn `PrivateKey` der Wert gültig ist, wird auf der Seite das ReCaptcha-Steuerelement und eine Schaltfläche angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4a14-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="d4a14-135">Wenn Sie die Schlüssel nicht global in \* \_AppStart.html\*festgelegt haben, wird auf der Seite ein Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4a14-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="d4a14-136">Geben Sie die Wörter für den Test ein.</span><span class="sxs-lookup"><span data-stu-id="d4a14-136">Enter the words for the test.</span></span> <span data-ttu-id="d4a14-137">Wenn Sie den ReCaptcha-Test bestehen, wird eine entsprechende Meldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4a14-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="d4a14-138">Andernfalls wird eine Fehlermeldung angezeigt, und das ReCaptcha-Steuerelement wird erneut angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4a14-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="d4a14-139">Wenn sich Ihr Computer in einer Domäne befindet, die `defaultproxy` einen Proxyserver verwendet, müssen Sie möglicherweise das Element der *Datei Web.config* konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d4a14-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="d4a14-140">Das folgende Beispiel zeigt eine *Web.config-Datei* mit dem Element, das `defaultproxy` so konfiguriert ist, dass der ReCaptcha-Dienst funktioniert.</span><span class="sxs-lookup"><span data-stu-id="d4a14-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="d4a14-141">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d4a14-141">Additional Resources</span></span>

- [<span data-ttu-id="d4a14-142">Anpassen des siteweiten Verhaltens für ASP.NET Webseiten-Websites</span><span class="sxs-lookup"><span data-stu-id="d4a14-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="d4a14-143">ReCaptcha-Website</span><span class="sxs-lookup"><span data-stu-id="d4a14-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
