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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Verwenden einer CAPTCHA, um zu verhindern, dass Bots Ihre ASP.NET Web Razor)-Website verwenden

von [Microsoft](https://github.com/microsoft)

> In diesem Artikel wird erläutert, wie Sie ReCaptcha (eine Sicherheitsmaßnahme) verwenden, um zu verhindern, dass automatisierte Programme (Bots) Aufgaben auf einer ASP.NET Website (Razor) ausführen.
> 
> **Sie lernen Folgendes:** 
> 
> - So fügen Sie Ihrer Website einen CAPTCHA-Test hinzu.
> 
> Dies sind die ASP.NET Funktionen, die in dem Artikel eingeführt werden:
> 
> - Der `ReCaptcha` Helfer.
> 
> > [!NOTE]
> > Die Informationen in diesem Artikel gelten für ASP.NET Webseiten 1.0 und Webseiten 2.

## <a name="about-captchas"></a>Über CAPTCHAs

Jedes Mal, wenn Sie Personen auf Ihrer Website registrieren lassen oder sogar einfach nur einen Namen und eine URL eingeben (wie für einen Blog-Kommentar), können Sie eine Flut von gefälschten Namen erhalten. Diese werden oft von automatisierten Programmen (Bots) verlassen, die versuchen, URLs in jeder Website zu verlassen, die sie finden können. (Eine häufige Motivation ist es, die URLs von Produkten zum Verkauf zu veröffentlichen.)

Sie können sicherstellen, dass ein Benutzer eine echte Person und kein Computerprogramm ist, indem Sie eine *CAPTCHA* verwenden, um Benutzer zu überprüfen, wenn sie sich registrieren oder anderweitig ihren Namen und ihre Website eingeben. CAPTCHA steht für Completely Automated Public Turing test to tell Computers and Humans Apart. Ein CAPTCHA ist ein *Challenge-Response-Test,* bei dem der Benutzer aufgefordert wird, etwas zu tun, was für eine Person einfach zu tun ist, aber für ein automatisiertes Programm schwierig ist. Die häufigste Art von CAPTCHA ist eine, bei der Sie einige verzerrte Buchstaben sehen und aufgefordert werden, sie einzugeben. (Die Verzerrung soll es Bots schwer machen, die Buchstaben zu entschlüsseln.)

## <a name="adding-a-recaptcha-test"></a>Hinzufügen eines ReCaptcha-Tests

In ASP.NET Seiten können `ReCaptcha` Sie den Helfer verwenden, um einen CAPTCHA-Test[http://recaptcha.net](http://recaptcha.net)zu rendern, der auf dem ReCaptcha-Dienst ( ) basiert. Der `ReCaptcha` Helfer zeigt ein Bild von zwei verzerrten Wörtern an, die Benutzer korrekt eingeben müssen, bevor die Seite überprüft wird. Die Benutzerantwort wird vom ReCaptcha.Net-Dienst überprüft.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Registrieren Sie Ihre[http://recaptcha.net](http://recaptcha.net)Website unter ReCaptcha.Net ( ). Wenn Sie die Registrierung abgeschlossen haben, erhalten Sie einen öffentlichen Schlüssel und einen privaten Schlüssel.
2. Fügen Sie die ASP.NET Web Helpers Library zu Ihrer Website hinzu, wie unter [Installieren von Helfern in einer ASP.NET Webseitenwebsite](https://go.microsoft.com/fwlink/?LinkId=252372)beschrieben, falls dies noch nicht der Fall ist.
3. Wenn Sie noch keine * \_AppStart.cshtml-Datei* haben, erstellen Sie im Stammordner einer Website eine Datei mit dem Namen * \_AppStart.cshtml*.
4. Fügen Sie `Recaptcha` die folgenden Hilfseinstellungen in der * \_Datei AppStart.cshtml* hinzu: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Legen `PublicKey` Sie `PrivateKey` die und Eigenschaften mit Ihren eigenen öffentlichen und privaten Schlüsseln fest.
6. Speichern Sie die * \_Datei AppStart.cshtml,* und schließen Sie sie.
7. Erstellen Sie im Stammordner einer Website eine neue Seite mit dem Namen *Recaptcha.cshtml*.
8. Ersetzen Sie den vorhandenen Inhalt durch Folgendes: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Führen Sie die Seite *Recaptcha.cshtml* in einem Browser aus. Wenn `PrivateKey` der Wert gültig ist, wird auf der Seite das ReCaptcha-Steuerelement und eine Schaltfläche angezeigt. Wenn Sie die Schlüssel nicht global in * \_AppStart.html*festgelegt haben, wird auf der Seite ein Fehler angezeigt. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Geben Sie die Wörter für den Test ein. Wenn Sie den ReCaptcha-Test bestehen, wird eine entsprechende Meldung angezeigt. Andernfalls wird eine Fehlermeldung angezeigt, und das ReCaptcha-Steuerelement wird erneut angezeigt.

> [!NOTE]
> Wenn sich Ihr Computer in einer Domäne befindet, die `defaultproxy` einen Proxyserver verwendet, müssen Sie möglicherweise das Element der *Datei Web.config* konfigurieren. Das folgende Beispiel zeigt eine *Web.config-Datei* mit dem Element, das `defaultproxy` so konfiguriert ist, dass der ReCaptcha-Dienst funktioniert.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Weitere Ressourcen

- [Anpassen des siteweiten Verhaltens für ASP.NET Webseiten-Websites](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha-Website](https://www.google.com/recaptcha)
