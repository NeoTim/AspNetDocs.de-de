---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Testen der Sicherheit eines Kennworts (c#) | Microsoft-Dokumentation
author: wenz
description: Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln. Das Steuerelement, in der ASP-Steuerelements "PasswordStrength". N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: 1aeea5af6fee22a91893e52b6ebe15f9ed00db45
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115267"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="94777-104">Testen der Sicherheit eines Kennworts (C#)</span><span class="sxs-lookup"><span data-stu-id="94777-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="94777-105">durch [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="94777-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="94777-106">[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="94777-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="94777-107">Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="94777-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="94777-108">Das Steuerelement "PasswordStrength" in ASP.NET AJAX Control Toolkit kann überprüfen, wie gut ein Kennwort ist.</span><span class="sxs-lookup"><span data-stu-id="94777-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="94777-109">Übersicht</span><span class="sxs-lookup"><span data-stu-id="94777-109">Overview</span></span>

<span data-ttu-id="94777-110">Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="94777-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="94777-111">Die `PasswordStrength` -Steuerelement in ASP.NET AJAX Control Toolkit kann überprüfen, wie gut ein Kennwort ist.</span><span class="sxs-lookup"><span data-stu-id="94777-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="94777-112">Schritte</span><span class="sxs-lookup"><span data-stu-id="94777-112">Steps</span></span>

<span data-ttu-id="94777-113">Die `PasswordStrength` Steuerelement erweitert ein Textfeld, und überprüft, ob es sich bei das Kennwort an gut genug ist.</span><span class="sxs-lookup"><span data-stu-id="94777-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="94777-114">Er bietet eine Fülle von Optionen mithilfe von Attributen; Hier sind nur einige davon:</span><span class="sxs-lookup"><span data-stu-id="94777-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="94777-115">`MinimumNumericCharacters` minimale Anzahl der Zeichen im Kennwort erforderlich</span><span class="sxs-lookup"><span data-stu-id="94777-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="94777-116">`MinimumSymbolCharacters` minimale Anzahl von Symbolzeichen (nicht Buchstaben und Ziffern), die im Kennwort erforderlich</span><span class="sxs-lookup"><span data-stu-id="94777-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="94777-117">`PreferredPasswordLength` Mindestlänge des Kennworts</span><span class="sxs-lookup"><span data-stu-id="94777-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="94777-118">`RequiresUpperAndLowerCaseCharacters` Gibt an, ob das Kennwort muss Groß-und Kleinbuchstaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="94777-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="94777-119">Die `StrengthIndicatorType` stellt die Informationen bereit, wie Sie die Stärke des Kennworts verwendet, als Text vorhanden (Wert `"Text"`) oder als eine Art der Statusanzeige (Wert `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="94777-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="94777-120">In der `DisplayPosition` -Attribut, die Sie konfigurieren, in dem die Informationen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="94777-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="94777-121">Hier ist ein vollständiges Beispiel, einschließlich der ASP.NET AJAX `ScriptManager` -Steuerelement, das `PasswordStrength` -Steuerelement, und natürlich ein Textfeld, in denen der Benutzer ein Kennwort eingeben kann.</span><span class="sxs-lookup"><span data-stu-id="94777-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="94777-122">Die Zwecke dieser Demo ist das Feld für die letztgenannte Form ein normales Textfeld und nicht in ein Kennwortfeld, damit Sie während der Entwicklung sehen können, was Sie eingeben.</span><span class="sxs-lookup"><span data-stu-id="94777-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="94777-123">Führen Sie die Seite aus, und geben Sie den Weg: Nur, nachdem Sie Kleinbuchstaben, Großbuchstaben, Ziffern und Symbole eingegeben haben, wird das Kennwort als unbreakable angesehen.</span><span class="sxs-lookup"><span data-stu-id="94777-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="94777-124">[![Nachdem das Kennwort (Recht) gut ist.](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="94777-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="94777-125">Nachdem das Kennwort (Recht) gut ist ([klicken Sie, um das Bild in voller Größe anzeigen](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="94777-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="94777-126">Nächste</span><span class="sxs-lookup"><span data-stu-id="94777-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
