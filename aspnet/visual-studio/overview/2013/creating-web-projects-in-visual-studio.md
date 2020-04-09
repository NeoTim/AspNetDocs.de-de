---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Erstellen ASP.NET Webprojekte in Visual Studio 2013 | Microsoft Docs
author: tdykstra
description: In diesem Thema werden die Optionen zum Erstellen ASP.NET Webprojekten in Visual Studio 2013 mit Update 3 erläutert. Hier finden Sie einige der neuen Funktionen für die Webentwicklung c...
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675682"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Erstellen von ASP.NET-Webprojekten in Visual Studio 2013

von [Tom Dykstra](https://github.com/tdykstra)

> In diesem Thema werden die Optionen zum Erstellen ASP.NET Webprojekten in Visual Studio 2013 mit Update 3 erläutert.
> 
> Im Folgenden finden Sie einige der neuen Features für die Webentwicklung im Vergleich zu früheren Versionen von Visual Studio:
> 
> - Eine einfache Benutzeroberfläche zum Erstellen von Projekten, die [Unterstützung für mehrere ASP.NET Frameworks](#add) (Web Forms, MVC und Web-API) bieten.
> - [ASP.NET Identity](#indauth), ein neues ASP.NET Mitgliedschaftssystem, das in allen ASP.NET Frameworks gleich funktioniert und mit anderen Webhosting-Software als IIS funktioniert.
> - Die Verwendung von [Bootstrap,](#bootstrap) um reaktionsschnelle Design- und Themenfunktionen bereitzustellen.
> - Neue Features für Webformulare, die früher nur für MVC angeboten wurden, z. B. [automatische Testprojekterstellung](#testproj) und eine [Intranetwebsitevorlage](#winauth).
> 
> Informationen zum Erstellen von Webprojekten für Azure Cloud Services oder Azure Mobile Services finden Sie unter [Erste Schritte mit Azure Cloud Services und ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) und Erstellen einer [Ranglisten-App mit Azure Mobile Services .NET Backend](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Voraussetzungen

Dieser Artikel gilt für [Visual Studio 2013,](https://go.microsoft.com/fwlink/?LinkId=306566) bei dem [Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) installiert ist.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Webanwendungsprojekte im Vergleich zu Websiteprojekten

ASP.NET gibt Ihnen die Wahl zwischen zwei Arten von Webprojekten: *Webanwendungsprojekte* und *Websiteprojekte*. Wir empfehlen Webanwendungsprojekte für die Neuentwicklung, und dieser Artikel gilt nur für Webanwendungsprojekte. Weitere Informationen finden Sie unter [Webanwendungsprojekte im Vergleich zu Websiteprojekten in Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) auf der MSDN-Website.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Überblick über die Erstellung von Webanwendungsprojekten

Die folgenden Schritte zeigen, wie Sie ein Webprojekt erstellen:

1. Klicken Sie auf die **Startseite** oder das Menü **Datei** auf **Neues Projekt.**
2. Klicken Sie im Dialogfeld **Neues Projekt** im linken Bereich auf **Web,** und **ASP.NET Webanwendung** im mittleren Bereich.

    ![Dialogfeld "Neues Projekt"](creating-web-projects-in-visual-studio/_static/image1.png)

    Sie können **Cloud** im linken Bereich auswählen, um einen [Azure Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), Azure Mobile [Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)oder [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)zu erstellen. In diesem Thema werden diese Vorlagen nicht behandelt.
3. Klicken Sie im rechten Bereich auf das Kontrollkästchen **Application Insights zu Projekt hinzufügen,** wenn Sie eine Überwachung der Integrität und Nutzung für Ihre Anwendung wünschen. Weitere Informationen finden Sie unter [Leistungsüberwachung in Webanwendungen](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).
4. Geben Sie **Projektname**, **Speicherort**und andere Optionen an, und klicken Sie dann auf **OK**.

    Das Dialogfeld **Neues ASP.NET-Projekt** wird angezeigt.

    ![Dialogfeld "Neues Projekt"](creating-web-projects-in-visual-studio/_static/image2.png)
5. Klicken Sie auf eine Vorlage.

    ![Vorlage auswählen](creating-web-projects-in-visual-studio/_static/image3.png)
6. Wenn Sie Unterstützung für zusätzliche Frameworks hinzufügen möchten, die nicht in der Vorlage enthalten sind, klicken Sie auf das entsprechende Kontrollkästchen. (Im gezeigten Beispiel können Sie einem Web Forms-Projekt MVC und/oder Web-API hinzufügen.)

    ![Hinzufügen von Frameworks](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>Wenn Sie ein Komponententestprojekt hinzufügen möchten, klicken Sie auf **Komponententests hinzufügen**.

    ![Hinzufügen von Komponententests](creating-web-projects-in-visual-studio/_static/image5.png)
8. Wenn Sie eine andere Authentifizierungsmethode als die standardmäßige Vorlage verwenden möchten, klicken Sie auf **Authentifizierung ändern**.

    ![Konfigurieren der Authentifizierungsschaltfläche](creating-web-projects-in-visual-studio/_static/image6.png)

    ![Konfigurieren des Authentifizierungsdialogfelds](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Erstellen einer Web-App oder eines virtuellen Computers in Azure

Visual Studio enthält Funktionen, die die Arbeit mit Azure-Diensten zum Hosten von Webanwendungen vereinfachen. Sie können z. B. alle folgenden Schritte in der Visual Studio-IDE ausführen:

- Erstellen und verwalten Sie Web-Apps oder virtuelle Maschinen, die Ihre Anwendung über das Internet verfügbar machen.
- Zeigen Sie Protokolle an, die von der Anwendung erstellt wurden, während sie in der Cloud ausgeführt wird.
- Ausführen im Debugmodus remote ausgeführt, während die Anwendung in der Cloud ausgeführt wird.
- Anzeigen und Verwalten anderer Azure-Dienste, z. B. SQL-Datenbanken.

Sie können [ein Azure-Konto erstellen,](https://www.windowsazure.com/pricing/free-trial/) das grundlegende Dienste wie Web-Apps kostenlos enthält, und wenn Sie MSDN-Abonnent sind, können Sie [Vorteile aktivieren,](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) die Ihnen monatliche Gutschriften für zusätzliche Azure-Dienste gewähren. 

Im Dialogfeld **Neues ASP.NET Projekt** können Sie standardmäßig eine Web-App oder einen virtuellen Computer für ein neues Webprojekt erstellen. Wenn Sie keine neue Web-App oder einen virtuellen Computer erstellen möchten, deaktivieren Sie das Kontrollkästchen **Host in der Cloud.**

![Erstellen von Remoteressourcen](creating-web-projects-in-visual-studio/_static/image8.png)

Die Kontrollkästchenbeschriftung kann **Host in der Cloud** oder Erstellen von **Remoteressourcen**sein, und in beiden Fällen ist der Effekt derselbe. Wenn Sie das Kontrollkästchen aktiviert lassen, erstellt Visual Studio standardmäßig eine Web-App in Azure App Service. Sie können das Dropdown-Feld verwenden, um dies in eine **virtuelle Maschine** zu ändern, wenn Sie dies vorziehen. Wenn Sie noch nicht bei Azure angemeldet sind, werden Sie zur Eingabe von Azure-Anmeldeinformationen aufgefordert. Nachdem Sie sich angemeldet haben, können Sie in einem Dialogfeld die Ressourcen konfigurieren, die Visual Studio für Ihr Projekt erstellt. Die folgende Abbildung zeigt das Dialogfeld für eine Web-App; Es werden verschiedene Optionen angezeigt, wenn Sie eine virtuelle Maschine erstellen möchten.

![Konfigurieren der Azure-App-Einstellungen](creating-web-projects-in-visual-studio/_static/image9.png)

Weitere Informationen zum Verwenden dieses Prozesses zum Erstellen von Azure-Ressourcen finden Sie unter [Erste Schritte mit Azure und ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) und Erstellen eines virtuellen Computers für eine Website mit Visual [Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).

Der Rest dieses Artikels enthält weitere Informationen zu den verfügbaren Vorlagen und deren Optionen. Der Artikel stellt auch Bootstrap, das Layout- und Themenframework vor, das in den Vorlagen verwendet wird.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013-Webprojektvorlagen

Visual Studio verwendet Vorlagen, um Webprojekte zu erstellen. Eine Projektvorlage kann Dateien und Ordner im neuen Projekt erstellen, NuGet-Pakete installieren und Beispielcode für eine rudimentäre Arbeitsanwendung bereitstellen. Vorlagen implementieren die neuesten Webstandards und sollen Best Practices für die Verwendung von ASP.NET Technologien veranschaulichen und Ihnen einen Sprung beim Erstellen Ihrer eigenen Anwendung geben.

Visual Studio 2013 bietet die folgenden Optionen für Webprojektvorlagen für Projekte, die auf .NET 4.5 oder neuere Versionen von .NET Framework abzielen:

- [Leere Vorlage](#empty)
- [Web Forms-Vorlage](#wf)
- [MVC-Vorlage](#mvc)
- [Web-API-Vorlage](#webapi)
- [Einzelseite-Anwendungsvorlage](#spa)
- [Azure Mobile Service-Vorlage](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012-Vorlagen](#vs2012)

Sie können auch eine Visual Studio-Erweiterung installieren, die eine [Facebook-Vorlage](#facebook)bereitstellt.

Informationen zum Erstellen von Projekten, die auf .NET 4 abzielen, finden Sie weiter unten in [Visual Studio 2012-Vorlagen](#vs2012) in diesem Thema.

Informationen zum Erstellen ASP.NET Anwendungen für mobile Clients finden Sie [unter Mobile Support in ASP.NET](../../../mobile/overview.md).

<a id="empty"></a>
### <a name="empty-template"></a>Leere Vorlage

Die Vorlage Leer stellt die minimalen Ordner und Dateien für eine ASP.NET Web-App bereit, z. B. eine Projektdatei (*.csproj* oder .* vbproj*) und eine *Web.config-Datei.* Sie können Unterstützung für Web Forms, MVC und/oder Web-API hinzufügen, indem Sie die Kontrollkästchen unter Ordner **hinzufügen und Kernreferenzen für:** Label verwenden.

Für die Vorlage Leer sind keine Authentifizierungsoptionen verfügbar. Die Authentifizierungsfunktionalität ist in Beispielanwendungen implementiert, und die Vorlage "Leer" erstellt keine Beispielanwendung.

<a id="wf"></a>
### <a name="web-forms-template"></a>Web Forms-Vorlage

Das Web Forms-Framework bietet die folgenden Funktionen, mit denen Sie schnell Websites erstellen können, die reich an Benutzeroberflächen- und Datenzugriffsfeatures sind:

- Ein WYSIWYG-Designer in Visual Studio.
- Serversteuerelemente, die HTML rendern und die Sie anpassen können, indem Sie Eigenschaften und Stile festlegen.
- Eine umfangreiche Auswahl an Steuerelementen für den Datenzugriff und die Datenanzeige.
- Ein Ereignismodell, das Ereignisse verfügbar macht, die Sie wie eine Clientanwendung wie WPF programmieren können.
- Automatische Aufbewahrung des Zustands (Daten) zwischen HTTP-Anforderungen.

Im Allgemeinen erfordert das Erstellen einer Web Forms-Anwendung weniger Programmieraufwand als das Erstellen derselben Anwendung mithilfe des ASP.NET MVC-Frameworks. Web Forms ist jedoch nicht nur für eine schnelle Anwendungsentwicklung. Es gibt viele komplexe kommerzielle Anwendungen und Frameworks, die auf Web Forms basieren.

Da eine Web Forms-Seite und die Steuerelemente auf der Seite automatisch einen Großteil des Markups generieren, das an den Browser gesendet wird, haben Sie nicht die Art von detaillierter Kontrolle über den HTML-Code, ASP.NET MVC bietet. Das deklarative Modell zum Konfigurieren von Seiten und Steuerelementen minimiert die Menge an Code, die Sie schreiben müssen, blendet jedoch einige simtierte Verhaltensweisen von HTML und HTTP aus. Beispielsweise ist es nicht immer möglich, genau anzugeben, welches Markup von einem Steuerelement generiert werden kann.

Das Web Forms-Framework eignet sich nicht so leicht wie ASP.NET MVC für musterbasierte Entwicklungspraktiken wie [testgesteuerte Entwicklung,](http://en.wikipedia.org/wiki/Test-driven_development) [Trennung von Bedenken,](http://en.wikipedia.org/wiki/Separation_of_concerns) [Umkehrung der Kontrolle](http://en.wikipedia.org/wiki/Inversion_of_control)und [Abhängigkeitsinjektion](http://en.wikipedia.org/wiki/Dependency_injection). Wenn Sie Code auf diese Weise schreiben möchten, können Sie dies. es ist einfach nicht so automatisch wie im ASP.NET MVC-Framework. Das [ASP.NET Web Forms MVP-Projekt](http://webformsmvp.com/) zeigt einen Ansatz, der die Trennung von Bedenken und Testbarkeit erleichtert und gleichzeitig die schnelle Entwicklung aufrechterhält, für die Web Forms erstellt wurde. Microsoft SharePoint basiert auf Web Forms MVP.

Die Web Forms-Vorlage erstellt eine Web Forms-Beispielanwendung, die [Bootstrap](#bootstrap) verwendet, um responsive Entwurfs- und -themenfunktionen bereitzustellen. Die folgende Abbildung zeigt die Startseite.

![Web Forms-Vorlagen-App-Startseite](creating-web-projects-in-visual-studio/_static/image10.png)

Weitere Informationen zu Web formularen Informationen finden Sie [unter ASP.NET Web Forms](https://asp.net/web-forms). Informationen dazu, was die Web Forms-Vorlage für Sie tut, finden Sie unter [Erstellen einer grundlegenden Web Forms-Anwendung mit Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC-Vorlage

ASP.NET MVC wurde entwickelt, um musterbasierte Entwicklungspraktiken wie [testgesteuerte Entwicklung,](http://en.wikipedia.org/wiki/Test-driven_development) [Trennung von Bedenken,](http://en.wikipedia.org/wiki/Separation_of_concerns) [Inversion der Kontrolle](http://en.wikipedia.org/wiki/Inversion_of_control)und [Abhängigkeitsinjektion](http://en.wikipedia.org/wiki/Dependency_injection)zu erleichtern. Das Framework empfiehlt, die Geschäftslogikebene einer Webanwendung von der Präsentationsebene zu trennen. Durch die Aufteilung der Anwendung in Modelle (M), Ansichten (V) und Controller (C) kann ASP.NET MVC die Verwaltung der Komplexität in größeren Anwendungen vereinfachen.

Mit ASP.NET MVC arbeiten Sie direkter mit HTML und HTTP als in Web Forms. Web Forms kann z. B. den Status zwischen HTTP-Anforderungen automatisch beibehalten, Aber Sie müssen dies explizit in MVC codieren. Der Vorteil des MVC-Modells besteht darin, dass Sie die vollständige Kontrolle darüber haben, was Ihre Anwendung genau tut und wie sie sich in der Webumgebung verhält. Der Nachteil ist, dass Sie mehr Code schreiben müssen.

MVC wurde entwickelt, um erweiterbar zu sein und PowerEntwicklern die Möglichkeit zu bieten, das Framework an ihre Anwendungsanforderungen anzupassen. Darüber hinaus ist der ASP.NET MVC-Quellcode unter einer OSI-Lizenz verfügbar.

Die MVC-Vorlage erstellt eine MVC 5-Beispielanwendung, die [Bootstrap](#bootstrap) verwendet, um reaktionsfähige Entwurfs- und Thesenfunktionen bereitzustellen. Die folgende Abbildung zeigt die Startseite.

![MVC-Beispielanwendung](creating-web-projects-in-visual-studio/_static/image11.png)

Weitere Informationen zu MVC finden Sie [unter ASP.NET MVC](https://asp.net/mvc). Informationen zum Auswählen der MVC 4-Vorlage finden Sie weiter unten in diesem Artikel unter [Visual Studio 2012-Vorlagen.](#vs2012)

<a id="webapi"></a>
### <a name="web-api-template"></a>Web-API-Vorlage

Die Web-API-Vorlage erstellt einen Beispielwebdienst basierend auf der Web-API, einschließlich API-Hilfeseiten, die auf MVC basieren.

ASP.NET-Web-API ist ein Framework, das das Erstellen von HTTP-Diensten erleichtert, die eine Vielzahl verschiedener Clients bedienen können, einschließlich Browsern und mobilen Geräten. ASP.NET Web-API ist eine ideale Plattform zum Erstellen von RESTful-Diensten auf .NET Framework.

Die Web-API-Vorlage erstellt einen Beispielwebdienst. Die folgenden Abbildungen zeigen Beispielhilfeseiten.

![Web-API-Hilfeseite](creating-web-projects-in-visual-studio/_static/image12.png)

![Web-API-Hilfeseite für GET-API](creating-web-projects-in-visual-studio/_static/image13.png)

Weitere Informationen zur Web-API finden Sie [unter ASP.NET Web-API](https://asp.net/web-api).

<a id="spa"></a>
### <a name="single-page-application-template"></a>Vorlage für eine Anwendung mit einer Seite

Die VORLAGE für die Anwendung einer anwendung (Single Page Application, SPA) erstellt eine Beispielanwendung, die JavaScript, HTML 5 und [KnockoutJS](http://knockoutjs.com/) auf dem Client verwendet und die Web-API auf dem Server ASP.NET.

Die einzige Authentifizierungsoption für die SPA-Vorlage sind [einzelne Benutzerkonten](#indauth).

Die folgende Abbildung zeigt den Anfangszustand der Beispielanwendung, die von der SPA-Vorlage erstellt wird.

![SPA-Beispielanwendung](creating-web-projects-in-visual-studio/_static/image14.png)

Informationen zum Erstellen einer Anwendung mithilfe der SPA-Vorlage finden Sie unter [Web-API - Externe Authentifizierungsdienste](../../../web-api/overview/security/external-authentication-services.md).

Weitere Informationen zu ASP.NET Einzelseitenanwendungen und zu zusätzlichen SPA-Vorlagen, die andere JavaScript-Frameworks als KnockoutJS verwenden, finden Sie in den folgenden Ressourcen:

- [ASP.NET Einzelseitenanwendung](../../../single-page-application/index.md).
- [Grundlegendes zu Sicherheitsfunktionen in der SPA-Vorlage für VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [Einseitige Anwendungen: Erstellen Sie moderne, reaktionsschnelle Web-Apps mit ASP.NET](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook-Vorlage

Sie können eine [Visual Studio-Erweiterung installieren, die eine Facebook-Vorlage bereitstellt.](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409) Diese Vorlage erstellt eine Beispielanwendung, die für die Ausführung auf der Facebook-Website konzipiert ist. Es basiert auf ASP.NET MVC und verwendet Web-API für Echtzeit-Update-Funktionalität.

Für die Facebook-Vorlage sind keine Authentifizierungsoptionen verfügbar, da Facebook-Anwendungen auf der Facebook-Website ausgeführt werden und sich auf die Authentifizierung von Facebook verlassen.

Weitere Informationen zu ASP.NET Facebook-Anwendungen finden Sie unter [Aktualisieren der MVC-Facebook-API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012-Vorlagen

Das Dialogfeld zum Erstellen von Visual Studio 2013-Webprojekt bietet keinen Zugriff auf einige Vorlagen, die in Visual Studio 2012 verfügbar waren. Wenn Sie eine dieser Vorlagen verwenden möchten, können Sie im linken Bereich des Dialogfelds Visual Studio New Project auf den Knoten Visual Studio 2012 klicken.

![Visual Studio 2012-Vorlagen](creating-web-projects-in-visual-studio/_static/image15.png)

Mit dem **Visual Studio 2012-Knoten** können Sie die folgenden Webvorlagen auswählen, auf die Sie in der Standardliste der Vorlagen für Visual Studio 2013 keinen Zugriff haben:

- ASP.NET MVC 4-Webanwendung
- Webanwendung für ASP.NET Dynamic Data Entities
- ASP.NET-AJAX-Serversteuerelement
- ASP.NET-AJAX-Serversteuerelement-Extender
- ASP.NET-Serversteuerelement

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Bootstrap in den Visual Studio 2013-Webprojektvorlagen

Die Visual Studio 2013-Projektvorlagen verwenden [Bootstrap](http://getbootstrap.com/), ein layout- und von Twitter erstelltes Layout- und Themaisierungsframework. Bootstrap verwendet CSS3, um ein reaktionsschnelles Design bereitzustellen, was bedeutet, dass Layouts sich dynamisch an unterschiedliche Browserfenstergrößen anpassen können. In einem breiten Browserfenster sieht die von der Web Forms-Vorlage erstellte Homepage beispielsweise wie die folgende Abbildung aus:

![Web Forms-Vorlagen-App-Startseite](creating-web-projects-in-visual-studio/_static/image16.png)

Machen Sie das Fenster schmaler, und die horizontal angeordneten Spalten bewegen sich in vertikale Anordnung:

![Bootstrap vertikale Säulenanordnung](creating-web-projects-in-visual-studio/_static/image17.png)

Schließen Sie das Fenster ein wenig mehr, und das horizontale obere Menü verwandelt sich in ein Symbol, auf das Sie klicken können, um es in ein vertikal ausgerichtetes Menü zu erweitern:

![Bootstrap-Menüsymbol](creating-web-projects-in-visual-studio/_static/image18.png)

![Bootstrap vertikales Menü](creating-web-projects-in-visual-studio/_static/image19.png)

Sie können auch die Theierungsfunktion von Bootstrap verwenden, um das Erscheinungsbild der Anwendung leicht zu ändern. Sie können z. B. die folgenden Schritte ausführen, um das Design zu ändern.

1. Wechseln Sie in [http://Bootswatch.com](http://Bootswatch.com)Ihrem Browser zu , wählen Sie ein Design aus, und klicken Sie dann auf **Herunterladen**. (Dies lädt *bootstrap.min.css* standardmäßig herunter; wenn Sie den CSS-Code untersuchen möchten, erhalten Sie *bootstrap.css* anstelle der verdifizierten Version.)
2. Kopieren Sie den Inhalt der heruntergeladenen CSS-Datei.
3. Erstellen Sie in Visual Studio eine neue **Stylesheet-Datei** mit dem Namen *bootstrap-theme.css* im *Ordner Inhalt,* und fügen Sie den heruntergeladenen CSS-Code darin ein.
4. Öffnen Sie *App\_Start/Bundle.config* und ändern Sie *bootstrap.css* in *bootstrap-theme.css*.

Führen Sie das Projekt erneut aus, und die Anwendung hat ein neues Aussehen. Die folgende Abbildung zeigt die Wirkung des Amelia-Themas:

![Bootstrap Amelia Thema](creating-web-projects-in-visual-studio/_static/image20.png)

Viele Bootstrap-Themen sind verfügbar, sowohl kostenlose als auch Premium-Versionen. Bootstrap bietet auch eine Vielzahl von [UI-Komponenten, wie Dropdowns](http://twitter.github.io/bootstrap/components.html#dropdowns), [Schaltflächengruppen](http://twitter.github.io/bootstrap/components.html#buttonGroups)und [Symbole](http://twitter.github.io/bootstrap/base-css.html#images). Weitere Informationen zu Bootstrap finden Sie [auf der Bootstrap-Website](http://twitter.github.io/bootstrap/).

Wenn Sie den Web Forms-Designer in Visual Studio verwenden, beachten Sie, dass der Designer CSS3 nicht unterstützt, sodass nicht alle Auswirkungen von Bootstrap-Designs oder reaktionsfähigen Layoutänderungen genau angezeigt werden. Die Web Forms-Seiten werden jedoch korrekt angezeigt, wenn sie mit einem Browser angezeigt werden.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>Hinzufügen von Unterstützung für zusätzliche Frameworks

Wenn Sie eine Vorlage auswählen, wird das Kontrollkästchen für die von der Vorlage verwendeten Frameworks automatisch aktiviert. Wenn Sie beispielsweise die **Web Forms-Vorlage** auswählen, ist das Kontrollkästchen **Web Formulare** aktiviert, und Sie können sie nicht löschen.

![Vorlage auswählen](creating-web-projects-in-visual-studio/_static/image21.png)

![Hinzufügen von Frameworks](creating-web-projects-in-visual-studio/_static/image22.png)

Sie können das Kontrollkästchen für ein Framework aktivieren, das nicht in der Vorlage enthalten ist, um Unterstützung für dieses Framework hinzuzufügen, wenn das Projekt erstellt wird. Aktivieren Sie beispielsweise das Kontrollkästchen **Web Forms,** um die Verwendung von Web Forms *.aspx-Seiten* zu aktivieren, wenn Sie die MVC-Vorlage ausgewählt haben. Oder um MVC zu aktivieren, wenn Sie die Web Forms-Vorlage verwenden, klicken Sie auf das Kontrollkästchen **MVC.** Das Hinzufügen eines Frameworks ermöglicht Entwurfszeit- und Laufzeitunterstützung. Wenn Sie beispielsweise MVC-Unterstützung zu einem Web Forms-Projekt hinzufügen, können Sie Controller und Ansichten auf dem Gerüst erstellen.

Wenn Sie Web Forms und MVC in einem Projekt kombinieren und [Friendly URLs](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) in Web Forms aktivieren, kann es zu unerwarteten Routingproblemen kommen, bei denen eine URL mehrere mögliche Ziele enthält. Die Routen, die zuerst definiert werden, haben Vorrang. Wenn Sie z. `Home` B. über einen Controller `http://contoso.com/home` und eine *Home.aspx-Seite* verfügen, wird die `MapRoute` URL zu *Home.aspx* wechseln, wenn Sie die `EnableFriendlyUrls` Methode aufrufen, bevor Sie die Methode in *RouteConfig.cs*aufrufen, oder dieselbe URL wird in die Standardansicht für Ihren `Home` Controller wechseln, wenn Sie vor `MapRoute` `EnableFriendlyUrls`aufrufen.

Durch das Hinzufügen eines Frameworks wird keine Beispielanwendungsfunktionalität hinzugefügt. Wenn Sie beispielsweise Web Forms-Unterstützung hinzufügen, wenn Sie die MVC-Vorlage ausgewählt haben, wird keine *Default.aspx-Homepagedatei* erstellt. Es werden nur die Ordner, Dateien und Verweise hinzugefügt, die zur Unterstützung des Frameworks erforderlich sind. Aus diesem Grund ändert das Hinzufügen von Frameworks keine Authentifizierungsoptionen, die durch Code in Beispielanwendungen implementiert werden, die von den Vorlagen erstellt wurden. Wenn Sie beispielsweise die Vorlage Leer auswählen und Web Forms- oder MVC-Unterstützung hinzufügen, wird die Schaltfläche **Authentifizierung** konfigurieren weiterhin deaktiviert.

In den folgenden Abschnitten wird kurz die Auswirkungen der einzelnen Kontrollkästchen beschrieben.

### <a name="add-web-forms-support"></a>Web Forms-Unterstützung hinzufügen

Erstellt leere *Ordner für App-Daten\_* und *-Modelle* und eine *Global.asax-Datei.* Diese werden bereits von allen Vorlagen mit Ausnahme der Vorlage Leer erstellt, sodass das Aktivieren des Kontrollkästchens Web forms für andere Vorlagen keinen Unterschied macht.

Die Web Forms-Vorlage aktiviert standardmäßig Friendly URLs, aber wenn Sie Web Forms-Unterstützung zu anderen Vorlagen hinzufügen, indem Sie das Kontrollkästchen "Benutzerfreundliche URLs" aktivieren, werden die Benutzernichten-URLs nicht automatisch aktiviert.

### <a name="add-mvc-support"></a>MVC-Unterstützung hinzufügen

Installiert MVC-, Razor- und WebPages-NuGet-Pakete, erstellt leere *Ordner für\_App-Daten*, *Controller*, *Modelle*und *Ansichten,* erstellt den *Ordner App\_Start* mit *RouteConfig.cs* Datei und erstellt die *Datei Global.asax.*

### <a name="add-web-api-support"></a>Web-API-Unterstützung hinzufügen

Installiert WebApi- und Newtonsoft.Json NuGet-Pakete, erstellt leere *Ordner\_app Data*, *Controllers*und *Models,* erstellt den *Ordner App\_Start* mit *WebApiConfig.cs* Datei und erstellt die *Datei Global.asax.*

<a id="auth"></a>
## <a name="authentication-methods"></a>Authentifizierungsmethoden

Visual Studio 2013 bietet mehrere Authentifizierungsoptionen für die Vorlagen Web forms, MVC und Web API:

- [Keine Authentifizierung](#noauth)
- [Einzelne Benutzerkonten](#indauth) (ASP.NET Identity, früher als ASP.NET Mitgliedschaft bezeichnet)
- [Organisationskonten](#orgauth) (Windows Server Active Directory oder Azure Active Directory)
- [Windows-Authentifizierung](#winauth) (Intranet)

![Konfigurieren des Authentifizierungsdialogfelds](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>Keine Authentifizierung

Wenn Sie **Keine Authentifizierung**auswählen, enthält die Beispielanwendung keine Webseiten für die Anmeldung, keine Benutzeroberfläche, die angibt, wer angemeldet ist, keine Entitätsklassen für eine Mitgliedschaftsdatenbank und keine Verbindungszeichenfolge für eine Mitgliedschaftsdatenbank.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>Einzelne Benutzerkonten

Wenn Sie **Einzelne Benutzerkonten**auswählen, wird die Beispielanwendung so konfiguriert, dass ASP.NET Identity (früher als ASP.NET Mitgliedschaft bezeichnet) für die Benutzerauthentifizierung verwendet wird. ASP.NET Identity ermöglicht es einem Benutzer, ein Konto zu registrieren, indem er einen Benutzernamen und ein Kennwort auf der Website erstellt oder sich bei sozialen Anbietern wie Facebook, Google, Microsoft Account oder Twitter anmeldet. Der Standarddatenspeicher für Benutzerprofile in ASP.NET Identity ist eine SQL Server LocalDB-Datenbank, die Sie in SQL Server oder Azure SQL-Datenbank für den Produktionsstandort bereitstellen können.

In Visual Studio 2013 sind diese Features identisch wie in Visual Studio 2012, aber der zugrunde liegende Code für das ASP.NET-Mitgliedschaftssystem wurde neu geschrieben. Zu den Vorteilen der neuen Codebasis gehören:

- Das neue Mitgliedschaftssystem basiert auf [OWIN](http://owin.org/) und nicht auf dem ASP.NET Formularauthentifizierungsmodul. Dies bedeutet, dass Sie denselben Authentifizierungsmechanismus verwenden können, unabhängig davon, ob Sie Web Forms oder MVC in IIS verwenden oder selbst hostende Web-API oder SignalR.
- Die neue Mitgliedschaftsdatenbank wird von Entity Framework Code First verwaltet, und alle Tabellen werden durch Entitätsklassen dargestellt, die Sie ändern können. Dies bedeutet, dass Sie das Datenbankschema und die profilbezogene Webbenutzeroberfläche ganz einfach an Ihre eigenen Anforderungen anpassen und Ihre Updates einfach mithilfe von Code First-Migrationen bereitstellen können.

Das neue Mitgliedschaftssystem wird automatisch in den neuen Vorlagen implementiert und kann manuell in jedem Projekt implementiert werden, das auf .NET 4.5 oder höher abzielt.

ASP.NET Identity ist eine gute Wahl, wenn Sie eine Internet-Website erstellen, die hauptsächlich für externe Kunden ist. Wenn Ihre Organisation Active Directory oder Office 365 verwendet und Sie ein Projekt erstellen möchten, das die einmalige Anmeldung für Mitarbeiter und Geschäftspartner ermöglicht, ist die Option **Organisationskonten** möglicherweise die bessere Wahl.

Weitere Informationen zur Option Einzelne Benutzerkonten finden Sie in den folgenden Ressourcen:

- [www.asp.net/identity](../../../identity/index.md). Dokumentation über ASP.NET Identity auf der ASP.NET-Website.
- [Erstellen Sie eine ASP.NET MVC 5 App mit Facebook und Google OAuth2 und OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md). Zeigt außerdem, wie Benutzerprofildaten angepasst werden.
- [Web-API - Externe Authentifizierungsdienste](../../../web-api/overview/security/external-authentication-services.md)
- [Hinzufügen externer Anmeldungen zu Ihrer ASP.NET Anwendung in Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>Organisationskonten

Wenn Sie **Organisationskonten**auswählen, wird die Beispielanwendung für die Verwendung von Windows Identity Foundation (WIF) für die Authentifizierung basierend auf Benutzerkonten in Azure Active Directory (Azure AD, einschließlich Office 365) oder Windows Server Active Directory konfiguriert. Weitere Informationen finden Sie unter Optionen für die [Authentifizierung von Organisationskonten](#orgauthoptions) weiter unten in diesem Thema.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows-Authentifizierung

Wenn Sie **Die Windows-Authentifizierung**auswählen, wird die Beispielanwendung so konfiguriert, dass sie das Windows-Authentifizierungs-IIS-Modul für die Authentifizierung verwendet. Die Anwendung zeigt die Domänen- und Benutzer-ID des Active-Verzeichnisses oder des lokalen Computerkontos an, das bei Windows angemeldet ist, aber keine Benutzerregistrierung oder Anmeldebenutzeroberfläche enthält. Diese Option ist für Intranet-Websites vorgesehen.

Alternativ können Sie eine Intranetsite erstellen, die die [AD-Authentifizierung](#orgauthonprem)verwendet, indem Sie unter Organisationskonten die Option Lokal auswählen. Die Option On-Premises verwendet Windows Identity Foundation (WIF) anstelle des Windows-Authentifizierungsmoduls. Einige zusätzliche Schritte sind erforderlich, um die Option Lokal einrichten zu können, aber WIF aktiviert Features, die mit dem Windows-Authentifizierungsmodul nicht verfügbar sind. Mit WIF können Sie beispielsweise den Anwendungszugriff in Active Directory und Die Verzeichnisdaten von Abfrageverzeichnissen konfigurieren.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>Organisationskontoauthentifizierungsoptionen

Im Dialogfeld **Authentifizierung** konfigurieren werden mehrere Optionen für Azure Active Directory (Azure AD, einschließlich Office 365) oder Windows Server Active Directory (AD)-Kontoauthentifizierung angezeigt:

- [Cloud – Single Organization](#orgauthsingle) (Azure AD oder AD unter Verwendung der Verzeichnisintegration mit Azure AD)
- [Cloud – Multi Organization](#orgauthmulti) (Azure AD oder AD unter Verwendung der Verzeichnisintegration mit Azure AD)
- [On-Premises](#orgauthonprem) (AD)

Wenn Sie eine der Azure AD-Optionen ausprobieren möchten, aber noch kein Konto haben, [klicken Sie hier, um sich für ein Azure AD-Konto anzumelden.](https://go.microsoft.com/fwlink/?LinkId=309942)

> [!NOTE]
> Wenn Sie eine der Azure AD-Optionen auswählen, erfordert Ihr Projekt eine Datenbank, und Sie müssen sich bei einem globalen Administratorkonto für Ihren Azure AD-Mandanten anmelden. Geben Sie den Namen und das Kennwort admin@contoso.onmicrosoft.comfür ein Organisationskonto (z. B. ) ein, das über Administratorberechtigungen für Ihren Azure AD-Mandanten verfügt.
> 
> **Geben Sie keine Anmeldeinformationen für ein Microsoft-Konto (z. B. contoso@hotmail.com) in das Anmeldedialogfeld ein.**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>Cloud - Single Organization Authentication

![Single Organization Authentication](creating-web-projects-in-visual-studio/_static/image24.png)

Wählen Sie diese Option, wenn Sie die Authentifizierung für Benutzerkonten aktivieren möchten, die in einem Azure [AD-Mandanten](https://technet.microsoft.com/library/jj573650.aspx)definiert sind. Beispielsweise wird die Website contoso.com und sie wird Mitarbeitern der Firma Contoso zur Verfügung gestellt, die sich in der contoso.onmicrosoft.com Mieter befinden. Sie können Azure AD nicht so konfigurieren, dass Benutzer anderer Mandanten auf die Anwendung zugreifen können.

#### <a name="domain"></a>Domain

Geben Sie die Azure AD-Domäne ein, in der `contoso.onmicrosoft.com`Sie die Anwendung einrichten möchten, z. B.: . Wenn Sie über eine [benutzerdefinierte Domäne](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)verfügen, z. `contoso.com` B. anstelle von `contoso.onmicrosoft.com`, können Sie diese hier eingeben.

#### <a name="access-level"></a>Zugriffsebene

Wenn die Anwendung Verzeichnisinformationen mithilfe der Graph-API abfragen oder aktualisieren muss, wählen Sie **Single Sign-On, Read Directory Data** oder Single **Sign-On, Read and Write Directory Data**aus. Andernfalls wählen Sie **Single Sign-On**. Weitere Informationen finden Sie unter [Anwendungszugriffsebenen](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) und [Verwenden der Graph-API zum Abfragen](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)von Azure AD .

#### <a name="application-id-uri"></a>Anwendungs-ID-URI

Standardmäßig erstellt die Vorlage einen Anwendungs-ID-URI für Sie, indem der Projektname an die Azure AD-Domäne angehängt wird. Wenn der Projektname z. B. der Projektname lautet `Example` und die Domäne `contoso.onmicrosoft.com`lautet, wird `https://contoso.onmicrosoft.com/Example`der Anwendungs-ID-URI zu . Wenn Sie den Anwendungs-ID-URI manuell angeben möchten, erweitern Sie den Abschnitt **Weitere Optionen,** und geben Sie den Anwendungs-ID-URI in das Textfeld ein. Der Anwendungs-ID-URI `https://`muss mit beginnen.

Wenn eine Anwendung, die bereits in Azure AD bereitgestellt wurde, über denselben Anwendungs-ID-URI wie Visual Studio für das Projekt verfügt, wird das Projekt standardmäßig mit der vorhandenen Anwendung verbunden, anstatt eine neue bereitzustellen. Wenn in diesem Fall eine neue Anwendung bereitgestellt werden soll, deaktivieren Sie das Kontrollkästchen **Überschreiben des Anwendungseintrags, wenn bereits eine Anwendung mit derselben ID vorhanden ist.**

Wenn das Kontrollkästchen **Überschreiben** deaktiviert ist und Visual Studio eine vorhandene Anwendung mit demselben Anwendungs-ID-URI findet, erstellt es einen neuen URI, indem eine Zahl an den URI angehängt wird, den es verwenden sollte. Angenommen, der Projektname `Example`lautet , Sie lassen das Textfeld leer, sie deaktivieren das Kontrollkästchen **Überschreiben,** `https://contoso.onmicrosoft.com/Example`und der Azure AD-Mandant verfügt bereits über eine Anwendung mit dem URI . In diesem Fall wird eine neue Anwendung mit einem `https://contoso.onmicrosoft.com/Example_20130619330903`Anwendungs-ID-URI wie bereitgestellt.

#### <a name="provisioning-the-application-in-azure-ad"></a>Bereitstellen der Anwendung in Azure AD

Um die Anwendung in Azure AD bereitzustellen oder das Projekt mit einer vorhandenen Anwendung zu verbinden, benötigt Visual Studio die Anmeldeinformationen eines globalen Administrators für die Domäne. Wenn Sie im Dialogfeld **Authentifizierung konfigurieren** auf **OK** klicken, werden Sie aufgefordert, den Benutzernamen und das Kennwort eines globalen Administrators für die angegebene Domäne anzugeben. Wenn Sie später im Dialogfeld **"Neues ASP.NET Projekt** erstellen" auf **Projekt** erstellen klicken, stellt Visual Studio die Anwendung in Azure AD bereit. Beachten Sie, dass Visual Studio im Rahmen dieses Prozesses geheime Clientwerte in die Datei Web.config einbettet, die ein Jahr nach der Erstellung ablaufen.

Informationen zum Erstellen von Anwendungen, die **die Cloud - Single Organization-Authentifizierung** verwenden, finden Sie in den folgenden Ressourcen:

- [Azure-Authentifizierung](../2012/windows-azure-authentication.md)
- [Hinzufügen einer Anmeldung zu einer Webanwendung mithilfe von Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Entwickeln von ASP.NET-Apps mit Azure Active Directory](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Sichere ASP.NET Web-API mit Azure AD- und Microsoft OWIN-Komponenten](https://msdn.microsoft.com/magazine/dn463788.aspx)

Die Tutorials wurden für Visual Studio 2013 noch nicht aktualisiert. Einige der Tutorials, die Sie manuell anweisen, werden in Visual Studio 2013 automatisiert.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>Cloud - Multi-Organisationsauthentifizierung

![Authentifizierung mehrerer Organisationen](creating-web-projects-in-visual-studio/_static/image25.png)

Wählen Sie diese Option, wenn Sie die Authentifizierung für Benutzerkonten aktivieren möchten, die in mehreren Azure [AD-Mandanten](https://technet.microsoft.com/library/jj573650.aspx)definiert sind. Beispielsweise wird die Website contoso.com und sie wird Mitarbeitern der Firma Contoso zur Verfügung gestellt, die sich im contoso.onmicrosoft.com Mieter befinden, und Mitarbeitern der Fabrikam Company, die sich im fabrikam.onmicrosoft.com Mieter befinden.

Die von Ihnen eingegebenen Einstellungen und der Anwendungsbereitstellungsschritt ähneln der [Einzelorganisationsauthentifizierung](#orgauthsingle).

Informationen zum Erstellen von Anwendungen, die **die Cloud -Multi-Organisation-Authentifizierung** verwenden, finden Sie in den folgenden Ressourcen:

- [Einfache Web-App-Integration mit &amp; Azure Active Directory, ASP.NET Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) im Active Directory Team-Blog.
- [Entwickeln von mehrinstanzenfähigen Webanwendungen mit Azure](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) AD-Tutorial. Das Tutorial wurde für Visual Studio 2013 noch nicht aktualisiert. Einige sendeMittel, zu denen Sie manuell aufgefordert werden, werden in Visual Studio 2013 automatisiert.
- [Sie müssen sich mit Ihren eigenen verschiedenen Organisationen ASP.NET App anmelden, bevor Sie sich anmelden können.](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/) Blog von Vittorio Bertocci, der erklärt, wie ein häufiges Problem gelöst wird, auf das Menschen beim Erstellen eines Projekts stoßen, das die Authentifizierung mit mehreren Organisationen verwendet.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>Lokale Organisationsauthentifizierung

![Lokale Organisationsauthentifizierung](creating-web-projects-in-visual-studio/_static/image26.png)

Wählen Sie diese Option, wenn Sie die Authentifizierung für Benutzerkonten aktivieren möchten, die in Windows Server Active Directory (AD) definiert sind, und Sie Azure AD nicht verwenden möchten. Mit dieser Option können Sie eine Intranetsite oder eine Internetsite erstellen. Verwenden Sie für eine Internetsite Active Directory Federation Services (ADFS), um Zugriff auf AD bereitzustellen. Weitere Informationen finden Sie unter Verwenden der Option Lokale [Organisationsauthentifizierung (ADFS) mit ASP.NET in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).

Für eine Intranetsite können Sie alternativ die [Windows-Authentifizierung](#winauth) anstelle dieser Option auswählen. Für die Windows-Authentifizierungsoption müssen Sie keine Metadatendokument-URL angeben. Die Windows-Authentifizierung gibt Ihnen jedoch nicht die Möglichkeit, den Anwendungszugriff in Active Directory zu steuern oder Verzeichnisdaten abzufragen.

#### <a name="on-premises-authority"></a>On-Premises-Behörde

Geben Sie eine URL ein, die auf das Metadatendokument verweist. Das Metadatendokument enthält die Koordinaten der Behörde. Die Anwendung verwendet diese Koordinaten, um den Websign-On-Flow zu fahren.

#### <a name="application-id-uri"></a>Anwendungs-ID-URI

Stellen Sie einen eindeutigen URI bereit, mit dem AD diese Anwendung identifizieren kann, oder lassen Sie ihn leer, damit Visual Studio einen uri erstellen kann.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Nächste Schritte

Dieses Dokument enthält eine grundlegende Hilfe zum Erstellen eines neuen ASP.NET Webprojekts in Visual Studio 2013. Weitere Informationen zur Verwendung für Visual Studio [https://www.asp.net/visual-studio/](../../index.md)für die Webentwicklung finden Sie unter .
