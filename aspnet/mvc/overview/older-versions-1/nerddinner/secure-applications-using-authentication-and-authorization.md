---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Sichere Anwendungen mit Authentifizierung und Autorisierung | Microsoft Docs
author: rick-anderson
description: Schritt 9 zeigt, wie Sie Authentifizierung und Autorisierung hinzufügen, um unsere NerdDinner-Anwendung zu sichern, so dass Benutzer sich registrieren und sich auf der Website anmelden müssen, um...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542572"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Sichern von Anwendungen mithilfe von Authentifizierung und Autorisierung

von [Microsoft](https://github.com/microsoft)

[PDF herunterladen](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Dies ist Schritt 9 eines kostenlosen ["NerdDinner" Anwendungs-Tutorials,](introducing-the-nerddinner-tutorial.md) das durch die Erstellung einer kleinen, aber vollständigen Webanwendung mit ASP.NET MVC 1 führt.
> 
> Schritt 9 zeigt, wie Sie Authentifizierung und Autorisierung hinzufügen, um unsere NerdDinner-Anwendung zu sichern, so dass Benutzer sich registrieren und sich auf der Website anmelden müssen, um neue Abendessen zu erstellen, und nur der Benutzer, der ein Abendessen veranstaltet, kann es später bearbeiten.
> 
> Wenn Sie ASP.NET MVC 3 verwenden, empfehlen wir Ihnen, die Tutorials [Erste Schritte mit MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) oder [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) zu befolgen.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner Schritt 9: Authentifizierung und Autorisierung

Im Moment gewährt unsere NerdDinner-Anwendung jedem, der die Website besucht, die Möglichkeit, die Details eines Abendessens zu erstellen und zu bearbeiten. Lassen Sie uns dies ändern, so dass Benutzer sich registrieren und auf der Website anmelden müssen, um neue Abendessen zu erstellen, und fügen Sie eine Einschränkung hinzu, so dass nur der Benutzer, der ein Abendessen veranstaltet, es später bearbeiten kann.

Um dies zu ermöglichen, verwenden wir Authentifizierung und Autorisierung, um unsere Anwendung zu sichern.

### <a name="understanding-authentication-and-authorization"></a>Grundlegendes zur Authentifizierung und Autorisierung

Bei der *Authentifizierung* wird die Identität eines Clients identifiziert und validiert, der auf eine Anwendung zugreift. Einfacher ausgedrückt geht es darum, herauszufinden, wer der Endnutzer ist, wenn er eine Website besucht. ASP.NET unterstützt mehrere Möglichkeiten, Browserbenutzer zu authentifizieren. Bei Internetwebanwendungen wird der am häufigsten verwendete Authentifizierungsansatz als "Formularauthentifizierung" bezeichnet. Mit der Formularauthentifizierung kann ein Entwickler ein HTML-Anmeldeformular in seiner Anwendung erstellen und dann den Benutzernamen/das Kennwort überprüfen, das ein Endbenutzer an eine Datenbank oder einen anderen Kennwortanmeldeinformationsspeicher übermittelt. Wenn die Kombination "Benutzername/Kennwort" korrekt ist, kann der Entwickler ASP.NET bitten, ein verschlüsseltes HTTP-Cookie auszugeben, um den Benutzer in zukünftigen Anforderungen zu identifizieren. Wir verwenden die Formularauthentifizierung mit unserer NerdDinner-Anwendung.

*Bei* der Autorisierung wird ermittelt, ob ein authentifizierter Benutzer über die Berechtigung zum Zugriff auf eine bestimmte URL/Ressource oder zum Ausführen einer Aktion verfügt. In unserer NerdDinner-Anwendung möchten wir beispielsweise autorisieren, dass nur Benutzer, die angemeldet sind, auf die */Dinners/Create* URL zugreifen und neue Dinners erstellen können. Wir möchten auch Autorisierungslogik hinzufügen, so dass nur der Benutzer, der ein Abendessen veranstaltet, es bearbeiten kann – und allen anderen Benutzern den Bearbeitungszugriff verweigern kann.

### <a name="forms-authentication-and-the-accountcontroller"></a>Formularauthentifizierung und AccountController

Die standardmäßige Visual Studio-Projektvorlage für ASP.NET MVC aktiviert automatisch die Formularauthentifizierung, wenn neue ASP.NET MVC-Anwendungen erstellt werden. Außerdem wird dem Projekt automatisch eine vorgefertigte Kontoanmeldeseite hinzugefügt – was die Integration der Sicherheit innerhalb einer Website wirklich einfach macht.

Die standardmäßige Site.master-Masterseite zeigt einen "Anmelden"-Link oben rechts auf der Website an, wenn der Benutzer, der darauf zugreift, nicht authentifiziert ist:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

Wenn Sie auf den Link "Anmelden" klicken, führt ein Benutzer zur */Account/LogOn-URL:*

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Besucher, die sich noch nicht registriert haben, können dies tun, indem Sie auf den Link "Registrieren" klicken – der sie zur *URL /Konto/Register* führt und ihnen die Eingabe von Kontodaten ermöglicht:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

Wenn Sie auf die Schaltfläche "Registrieren" klicken, wird ein neuer Benutzer innerhalb des ASP.NET-Mitgliedschaftssystems erstellt und der Benutzer mithilfe der Formularauthentifizierung auf der Website authentifiziert.

Wenn ein Benutzer angemeldet ist, ändert der Site.master die obere rechte Seite der Seite in die Ausgabe eines "Willkommen [Benutzername]!" und rendert einen "Abmelden"-Link anstelle eines "Anmelden". Durch Klicken auf den Link "Abmelden" wird der Benutzer abgemeldet:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

Die oben genannte Anmelde-, Abmelde- und Registrierungsfunktionalität wird innerhalb der AccountController-Klasse implementiert, die visual Studio unserem Projekt beim Erstellen des Projekts hinzugefügt hat. Die Benutzeroberfläche für den AccountController wird mithilfe von Ansichtsvorlagen im Verzeichnis "Ansichten" implementiert:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

Die AccountController-Klasse verwendet das ASP.NET Formularauthentifizierungssystem, um verschlüsselte Authentifizierungscookies auszugeben, und die ASP.NET-Mitgliedschafts-API zum Speichern und Überprüfen von Benutzernamen/Kennwörtern. Die ASP.NET-Mitgliedschafts-API ist erweiterbar und ermöglicht die Verwendung aller Kennwortanmeldeinformationen. ASP.NET wird mit integrierten Mitgliedschaftsanbieterimplementierungen ausgeliefert, die Benutzernamen/Kennwörter in einer SQL-Datenbank oder in Active Directory speichern.

Wir können konfigurieren, welcher Mitgliedschaftsanbieter unsere NerdDinner-Anwendung verwenden soll, indem wir die Datei &lt;&gt; "web.config" am Stamm des Projekts öffnen und nach dem darin folgenden Mitgliedschaftsbereich suchen. Die beim Erstellen des Projekts hinzugefügte Standard-Web.config registriert den SQL-Mitgliedschaftsanbieter und konfiguriert ihn so, dass er eine Verbindungszeichenfolge mit dem Namen "ApplicationServices" verwendet, um den Datenbankspeicherort anzugeben.

Die standardmäßige Verbindungszeichenfolge "ApplicationServices" (die im Abschnitt &lt;connectionStrings&gt; der Datei web.config angegeben ist) ist für die Verwendung von SQL Express konfiguriert. Sie verweist auf eine SQL Express-Datenbank mit dem Namen "ASPNETDB. MDF" unter dem Verzeichnis\_"App Data" der Anwendung. Wenn diese Datenbank nicht vorhanden ist, wenn die Mitgliedschafts-API zum ersten Mal in der Anwendung verwendet wird, erstellt ASP.NET automatisch die Datenbank und stellt das entsprechende Mitgliedschaftsdatenbankschema in der Anwendung bereit:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

Wenn wir anstelle von SQL Express eine vollständige SQL Server-Instanz verwenden (oder eine Verbindung mit einer entfernten Datenbank herstellen) möchten, müssen wir lediglich die Verbindungszeichenfolge "ApplicationServices" in der Datei web.config aktualisieren und sicherstellen, dass das entsprechende Mitgliedschaftsschema der Datenbank hinzugefügt wurde, auf die sie verweist. Sie können das Dienstprogramm\_"aspnet regsql.exe" im Verzeichnis "Windows"-Microsoft.NET-Framework-V2.0.50727- ausführen, um das entsprechende Schema für die Mitgliedschaft und die anderen ASP.NET Anwendungsdienste zu einer Datenbank hinzuzufügen.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>Autorisieren der /Dinners/Create URL mit dem Filter [Autorisieren]

Wir mussten keinen Code schreiben, um eine sichere Authentifizierungs- und Kontoverwaltungsimplementierung für die NerdDinner-Anwendung zu ermöglichen. Benutzer können neue Konten bei unserer Anwendung registrieren und sich auf der Website anmelden..

Jetzt können wir der Anwendung Autorisierungslogik hinzufügen und den Authentifizierungsstatus und Den Benutzernamen der Besucher verwenden, um zu steuern, was sie innerhalb der Website tun können und was nicht. Beginnen wir mit dem Hinzufügen von Autorisierungslogik zu den Aktionsmethoden "Erstellen" unserer DinnersController-Klasse. Insbesondere müssen Benutzer, die auf die */Dinners/Create* URL zugreifen, angemeldet sein. Wenn sie nicht angemeldet sind, leiten wir sie auf die Anmeldeseite um, damit sie sich anmelden können.

Die Implementierung dieser Logik ist ziemlich einfach. Alles, was wir tun müssen, ist, unseren Create-Aktionsmethoden ein [Authorize]-Filterattribut wie folgt hinzuzufügen:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC unterstützt die Möglichkeit, "Aktionsfilter" zu erstellen, die zum Implementieren wiederverwendbarer Logik verwendet werden können, die deklarativ auf Aktionsmethoden angewendet werden kann. Der [Authorize]-Filter ist einer der integrierten Aktionsfilter, die von ASP.NET MVC bereitgestellt werden, und ermöglicht es einem Entwickler, Autorisierungsregeln deklarativ auf Aktionsmethoden und Controllerklassen anzuwenden.

Wenn er ohne Parameter (wie oben) angewendet wird, erzwingt der [Authorize]-Filter, dass der Benutzer, der die Aktionsmethodenanforderung stellt, angemeldet sein muss – und er leitet den Browser automatisch an die Anmelde-URL um, wenn dies nicht der Fall ist. Bei dieser Umleitung wird die ursprünglich angeforderte URL als Querystring-Argument übergeben (z. B.: /Account/LogOn? ReturnUrl=%2fDinners%2fCreate). Der AccountController leitet den Benutzer dann zurück zur ursprünglich angeforderten URL, sobald er sich anmeldet.

Der [Authorize]-Filter unterstützt optional die Möglichkeit, eine Eigenschaft "Benutzer" oder "Rollen" anzugeben, die verwendet werden kann, um zu verlangen, dass der Benutzer sowohl angemeldet als auch innerhalb einer Liste zulässiger Benutzer oder eines Mitglieds einer zulässigen Sicherheitsrolle ist. Der folgende Code erlaubt z. B. nur zwei bestimmten Benutzern, "scottgu" und "billg", auf die /Dinners/Create URL zuzugreifen:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Das Einbetten bestimmter Benutzernamen in Code ist jedoch in der Regel ziemlich unverwaltbar. Ein besserer Ansatz besteht darin, übergeordnete "Rollen" zu definieren, anhand derer der Code überprüft wird, und dann Benutzer mithilfe einer Datenbank oder eines Active Directory-Systems der Rolle zuzuordnen (damit die tatsächliche Benutzerzuordnungsliste extern aus dem Code gespeichert werden kann). ASP.NET enthält eine integrierte Rollenverwaltungs-API sowie eine integrierte Gruppe von Rollenanbietern (einschließlich für SQL und Active Directory), die bei der Ausführung dieser Benutzer-/Rollenzuordnung helfen können. Wir könnten dann den Code aktualisieren, damit nur Benutzer innerhalb einer bestimmten "Admin"-Rolle auf die /Dinners/Create URL zugreifen können:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Verwenden der User.Identity.Name-Eigenschaft beim Erstellen von Abendessen

Wir können den Benutzernamen des aktuell angemeldeten Benutzers einer Anforderung mithilfe der User.Identity.Name-Eigenschaft abrufen, die in der Controller-Basisklasse verfügbar gemacht wird.

Als wir zuvor die HTTP-POST-Version unserer Create()-Aktionsmethode implementiert haben, hatten wir die "HostedBy"-Eigenschaft des Dinners in eine statische Zeichenfolge codiert. Wir können diesen Code jetzt aktualisieren, um stattdessen die User.Identity.Name-Eigenschaft zu verwenden, sowie automatisch einen RSVP für den Host hinzufügen, der das Dinner erstellt:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Da wir der Create()-Methode ein [Authorize]-Attribut hinzugefügt haben, stellt ASP.NET MVC sicher, dass die Aktionsmethode nur ausgeführt wird, wenn der Benutzer, der die /Dinners/Create URL besucht, auf der Website angemeldet ist. Daher enthält der User.Identity.Name Eigenschaftswert immer einen gültigen Benutzernamen.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Verwenden der User.Identity.Name-Eigenschaft beim Bearbeiten von Abendessen

Fügen wir nun eine Autorisierungslogik hinzu, die Benutzer einschränkt, sodass sie nur die Eigenschaften von Abendessen bearbeiten können, die sie selbst hosten.

Um dies zu unterstützen, fügen wir zuerst eine "IsHostedBy(Username)"-Hilfsmethode zu unserem Dinner-Objekt hinzu (innerhalb der Dinner.cs Teilklasse, die wir zuvor erstellt haben). Diese Hilfsmethode gibt true oder false zurück, je nachdem, ob ein bereitgestellter Benutzername mit der Dinner HostedBy-Eigenschaft übereinstimmt, und kapselt die Logik, die erforderlich ist, um einen Zeichenfolgenvergleich mit der Groß-/Kleinschreibung durchzuführen:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Anschließend fügen wir den Edit()-Aktionsmethoden in unserer DinnersController-Klasse ein [Authorize]-Attribut hinzu. Dadurch wird sichergestellt, dass Benutzer angemeldet sein müssen, um eine */Dinners/Edit/[id]-URL* anzufordern.

Anschließend können wir Code zu unseren Edit-Methoden hinzufügen, die die Dinner.IsHostedBy(Username)-Hilfsmethode verwenden, um zu überprüfen, ob der angemeldete Benutzer mit dem Dinner-Host übereinstimmt. Wenn der Benutzer nicht der Host ist, zeigen wir die Ansicht "InvalidOwner" an und beenden die Anforderung. Der Code dazu sieht wie folgt aus:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Wir können dann mit der rechten Maustaste auf das&gt;Verzeichnis "Views-Dinners" klicken und den Menübefehl "Hinzufügen- Ansicht" auswählen, um eine neue "InvalidOwner"-Ansicht zu erstellen. Wir füllen es mit der folgenden Fehlermeldung auf:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

Und jetzt, wenn ein Benutzer versucht, ein Abendessen zu bearbeiten, das er nicht besitzt, erhält er eine Fehlermeldung:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Wir können die gleichen Schritte für die Delete()-Aktionsmethoden in unserem Controller wiederholen, um auch die Berechtigung zum Löschen von Dinners zu sperren und sicherzustellen, dass nur der Host eines Dinners es löschen kann.

### <a name="showinghiding-edit-and-delete-links"></a>Anzeigen/Ausblenden von Links

Wir verlinken über unsere Details-URL auf die Aktionsmethode Bearbeiten und Löschen unserer DinnersController-Klasse:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

Derzeit zeigen wir die Aktionslinks Bearbeiten und Löschen an, unabhängig davon, ob der Besucher der Details-URL der Gastgeber des Abendessens ist. Lassen Sie uns dies ändern, so dass die Links nur angezeigt werden, wenn der besuchende Benutzer der Besitzer des Abendessens ist.

Die Details() Aktionsmethode in unserem DinnersController ruft ein Dinner-Objekt ab und übergibt es dann als Modellobjekt an unsere Ansichtsvorlage:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Wir können unsere Ansichtsvorlage aktualisieren, um die Links Bearbeiten und Löschen bedingt einzublenden, indem wir die Dinner.IsHostedBy()-Hilfsmethode wie folgt verwenden:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Nächste Schritte

Sehen wir uns nun an, wie authentifizierte Benutzer MIT AJAX RSVP für Abendessen aktivieren können.

> [!div class="step-by-step"]
> [Zurück](implement-efficient-data-paging.md)
> [Weiter](use-ajax-to-deliver-dynamic-updates.md)
