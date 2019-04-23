---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Testen der Sicherheit eines Kennworts (VB) | Microsoft-Dokumentation
author: wenz
description: Kennwörter sind nahezu überall erforderlich, so, dass verzögerte Benutzer neigen dazu, einfache Kennwörter sind leicht zu entschlüsseln. Das Steuerelement, in der ASP-Steuerelements "PasswordStrength". N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: fb185c4147d516ab28d632b3e874b6f1d46f6576
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408419"
---
# <a name="testing-the-strength-of-a-password-vb"></a>Testen der Sicherheit eines Kennworts (VB)

durch [Christian Wenz](https://github.com/wenz)

[Code herunterladen](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) oder [PDF-Datei herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

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

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

Führen Sie die Seite aus, und geben Sie den Weg: Nur, nachdem Sie Kleinbuchstaben, Großbuchstaben, Ziffern und Symbole eingegeben haben, wird das Kennwort als unbreakable angesehen.


[![Nachdem das Kennwort (Recht) gut ist.](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

Nachdem das Kennwort (Recht) gut ist ([klicken Sie, um das Bild in voller Größe anzeigen](testing-the-strength-of-a-password-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Vorherige](testing-the-strength-of-a-password-cs.md)
