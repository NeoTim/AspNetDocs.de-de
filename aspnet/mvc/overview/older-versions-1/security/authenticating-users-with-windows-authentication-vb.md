---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Authentifizierung von Benutzern mit Windows-Authentifizierung (VB) | Microsoft Docs
author: rick-anderson
description: Erfahren Sie, wie Sie die Windows-Authentifizierung im Kontext einer MVC-Anwendung verwenden. Sie erfahren, wie Sie die Windows-Authentifizierung im Webco Ihrer Anwendung aktivieren...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 446dcc338f61e1f76478c1085773e7ad089c73f4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540596"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>Authentifizieren von Benutzern bei der Windows-Authentifizierung (VB)

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie, wie Sie die Windows-Authentifizierung im Kontext einer MVC-Anwendung verwenden. Sie erfahren, wie Sie die Windows-Authentifizierung in der Webkonfigurationsdatei Ihrer Anwendung aktivieren und die Authentifizierung mit IIS konfigurieren. Schließlich erfahren Sie, wie Sie das Attribut [Autorisieren] verwenden, um den Zugriff auf Controlleraktionen auf bestimmte Windows-Benutzer oder -Gruppen zu beschränken.

In diesem Tutorial wird erläutert, wie Sie die in Internetinformationsdiensten integrierten Sicherheitsfunktionen nutzen können, um die Ansichten in Ihren MVC-Anwendungen kennwortgeschützt zu schützen. Sie erfahren, wie Controlleraktionen nur von bestimmten Windows-Benutzern oder -Benutzern aufgerufen werden, die Mitglieder bestimmter Windows-Gruppen sind.

Die Verwendung der Windows-Authentifizierung ist sinnvoll, wenn Sie eine interne Unternehmenswebsite (eine Intranetwebsite) erstellen und sie möchten, dass Ihre Benutzer ihre standardmäßigen Windows-Benutzernamen und Kennwörter beim Zugriff auf die Website verwenden können. Wenn Sie eine nach außen gerichtete Website (eine Internetwebsite) erstellen, sollten Sie stattdessen die Formularauthentifizierung verwenden.

#### <a name="enabling-windows-authentication"></a>Aktivieren der Windows-Authentifizierung

Wenn Sie eine neue ASP.NET MVC-Anwendung erstellen, ist die Windows-Authentifizierung standardmäßig nicht aktiviert. Die Formularauthentifizierung ist der Standardauthentifizierungstyp, der für MVC-Anwendungen aktiviert ist. Sie müssen die Windows-Authentifizierung aktivieren, indem Sie die Webkonfigurationsdatei (web.config) Ihrer MVC-Anwendung ändern. Suchen &lt;Sie&gt; den Authentifizierungsabschnitt, und ändern Sie ihn, um die Windows-authentifizierung anstelle der Formularauthentifizierung wie folgt zu verwenden:

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

Wenn Sie die Windows-Authentifizierung aktivieren, wird ihr Webserver für die Authentifizierung von Benutzern verantwortlich. In der Regel gibt es zwei verschiedene Arten von Webservern, die Sie beim Erstellen und Bereitstellen einer ASP.NET MVC-Anwendung verwenden.

Zunächst verwenden Sie beim Entwickeln einer MVC-Anwendung die ASP.NET Development Web Server, die in Visual Studio enthalten ist. Standardmäßig führt der ASP.NET Development Web Server alle Seiten im Kontext des aktuellen Windows-Kontos aus (unabhängig davon, welches Konto Sie für die Anmeldung bei Windows verwendet haben).

Der ASP.NET Development Web Server unterstützt auch die NTLM-Authentifizierung. Sie können die NTLM-Authentifizierung aktivieren, indem Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Namen Ihres Projekts klicken und Eigenschaften auswählen. Aktivieren Sie als Nächstes die Registerkarte Web, und aktivieren Sie das Kontrollkästchen NTLM (siehe Abbildung 1).

**Abbildung 1: Aktivieren der NTLM-Authentifizierung für den ASP.NET Development Web Server**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

Für eine Produktionswebanwendung verwenden Sie IIS als Webserver. IIS unterstützt verschiedene Arten der Authentifizierung, einschließlich:

- Standardauthentifizierung – Definiert als Teil des HTTP 1.0-Protokolls. Sendet Benutzernamen und Kennwörter im Klartext (Base64 codiert) über das Internet. - Digest-Authentifizierung – Sendet einen Hash eines Passworts anstelle des Kennworts selbst über das Internet. - Integrierte Windows-Authentifizierung (NTLM) – Die beste Art der Authentifizierung, die in Intranetumgebungen mit Windows verwendet werden kann. - Zertifikatauthentifizierung – Aktiviert die Authentifizierung mithilfe eines clientseitigen Zertifikats. Das Zertifikat wird einem Windows-Benutzerkonto zugeordnet.

> [!NOTE] 
> 
> Eine detailliertere Übersicht über diese verschiedenen [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)Authentifizierungstypen finden Sie unter .

Sie können Internet Information Services Manager verwenden, um einen bestimmten Authentifizierungstyp zu aktivieren. Beachten Sie, dass nicht bei jedem Betriebssystem alle Authentifizierungstypen verfügbar sind. Wenn Sie IIS 7.0 mit Windows Vista verwenden, müssen Sie außerdem die verschiedenen Typen der Windows-Authentifizierung aktivieren, bevor sie im InternetInformationsdienste-Manager angezeigt werden. Öffnen Sie **die Systemsteuerung, Programme, Programme und Funktionen, aktivieren oder deaktivieren Sie Windows-Funktionen**, und erweitern Sie den Knoten Internetinformationsdienste (siehe Abbildung 2).

**Abbildung 2: Aktivieren von Windows IIS-Features**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

Mithilfe von Internetinformationsdiensten können Sie verschiedene Authentifizierungstypen aktivieren oder deaktivieren. Abbildung 3 zeigt beispielsweise das Deaktivieren der anonymen Authentifizierung und das Aktivieren der integrierten Windows-Authentifizierung (NTLM), wenn IIS 7.0 verwendet wird.

**Abbildung 3 : Aktivieren der integrierten Windows-Authentifizierung**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Autorisieren von Windows-Benutzern und -Gruppen

Nachdem Sie die Windows-Authentifizierung &lt;&gt; aktiviert haben, können Sie das Attribut Autorisieren verwenden, um den Zugriff auf Controller oder Controlleraktionen zu steuern. Dieses Attribut kann auf einen gesamten MVC-Controller oder eine bestimmte Controlleraktion angewendet werden.

Der Home-Controller in Listing 1 macht beispielsweise drei Aktionen mit den Namen Index(), CompanySecrets() und StephenSecrets(verfügbar. Jeder kann die Index()-Aktion aufrufen. Allerdings können nur Mitglieder der lokalen Windows-Manager-Gruppe die Aktion CompanySecrets() aufrufen. Schließlich kann nur der Windows-Domänenbenutzer namens Stephen (in der Redmond-Domäne) die StephenSecrets()-Aktion aufrufen.

**Auflisten 1 – Controller-HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> Aufgrund der Windows-Benutzerkontensteuerung (UAC) verhält sich die lokale Administratorengruppe bei der Arbeit mit Windows Vista oder Windows Server 2008 anders als andere Gruppen. Das &lt;&gt; Authorize-Attribut erkennt ein Mitglied der lokalen Administratorengruppe nur dann richtig, wenn Sie die UAC-Einstellungen Ihres Computers ändern.

Was genau geschieht, wenn Sie versuchen, eine Controlleraktion aufzurufen, ohne die richtigen Berechtigungen zu haben, hängt vom Typ der aktivierten Authentifizierung ab. Wenn Sie den ASP.NET Development Server verwenden, erhalten Sie standardmäßig einfach eine leere Seite. Die Seite wird mit einem **401 Nicht autorisierten** HTTP-Antwortstatus bedient.

Wenn Sie hingegen IIS mit deaktivierter anonymer Authentifizierung und aktivierter Standardauthentifizierung verwenden, erhalten Sie bei jeder Anforderung der geschützten Seite immer wieder eine Eingabeaufforderung für das Anmeldedialogfeld (siehe Abbildung 4).

**Abbildung 4: Anmeldedialog mit der Standardauthentifizierung**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>Zusammenfassung

In diesem Tutorial wurde erläutert, wie Sie die Windows-Authentifizierung im Kontext einer ASP.NET MVC-Anwendung verwenden können. Sie haben gelernt, wie Sie die Windows-Authentifizierung in der Webkonfigurationsdatei Ihrer Anwendung aktivieren und wie Sie die Authentifizierung mit IIS konfigurieren. Schließlich haben Sie gelernt, &lt;&gt; wie Sie das Authorize-Attribut verwenden, um den Zugriff auf Controlleraktionen auf bestimmte Windows-Benutzer oder -Gruppen zu beschränken.

> [!div class="step-by-step"]
> [Zurück](authenticating-users-with-forms-authentication-vb.md)
> [Weiter](preventing-javascript-injection-attacks-vb.md)
