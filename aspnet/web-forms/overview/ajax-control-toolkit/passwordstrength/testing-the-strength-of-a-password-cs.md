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
ms.openlocfilehash: b71744df46f8b8d20efafa333a10370397c37d2f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048407"
---
<a name="testing-the-strength-of-a-password-c"></a>Testen der Sicherheit eines Kennworts (C#)
====================
durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln. Das Steuerelement "PasswordStrength" in ASP.NET AJAX Control Toolkit kann überprüfen, wie gut ein Kennwort ist.


## <a name="overview"></a>Übersicht

Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln. Die `PasswordStrength` -Steuerelement in ASP.NET AJAX Control Toolkit kann überprüfen, wie gut ein Kennwort ist.

## <a name="steps"></a>Schritte

Die `PasswordStrength` Steuerelement erweitert ein Textfeld, und überprüft, ob es sich bei das Kennwort an gut genug ist. Er bietet eine Fülle von Optionen mithilfe von Attributen; Hier sind nur einige davon:

- `MinimumNumericCharacters` minimale Anzahl der Zeichen im Kennwort erforderlich
- `MinimumSymbolCharacters` minimale Anzahl von Symbolzeichen (nicht Buchstaben und Ziffern), die im Kennwort erforderlich
- `PreferredPasswordLength` Mindestlänge des Kennworts
- `RequiresUpperAndLowerCaseCharacters` Gibt an, ob das Kennwort muss Groß-und Kleinbuchstaben verwenden.

Die `StrengthIndicatorType` stellt die Informationen bereit, wie Sie die Stärke des Kennworts verwendet, als Text vorhanden (Wert `"Text"`) oder als eine Art der Statusanzeige (Wert `"BarIndicator"`). In der `DisplayPosition` -Attribut, die Sie konfigurieren, in dem die Informationen angezeigt. Hier ist ein vollständiges Beispiel, einschließlich der ASP.NET AJAX `ScriptManager` -Steuerelement, das `PasswordStrength` -Steuerelement, und natürlich ein Textfeld, in denen der Benutzer ein Kennwort eingeben kann. Die Zwecke dieser Demo ist das Feld für die letztgenannte Form ein normales Textfeld und nicht in ein Kennwortfeld, damit Sie während der Entwicklung sehen können, was Sie eingeben.

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

Führen Sie die Seite aus, und geben Sie den Weg: Nur, nachdem Sie Kleinbuchstaben, Großbuchstaben, Ziffern und Symbole eingegeben haben, wird das Kennwort als unbreakable angesehen.


[![Nachdem das Kennwort (Recht) gut ist.](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

Nachdem das Kennwort (Recht) gut ist ([klicken Sie, um das Bild in voller Größe anzeigen](testing-the-strength-of-a-password-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Nächste](testing-the-strength-of-a-password-vb.md)
