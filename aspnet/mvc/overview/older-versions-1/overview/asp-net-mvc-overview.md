---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: mVC-Übersicht ASP.NET | Microsoft Docs
author: rick-anderson
description: Erfahren Sie mehr über die Unterschiede zwischen ASP.NET MVC-Anwendung und ASP.NET Web Forms-Anwendungen. Erfahren Sie, wie Sie entscheiden, wann eine ASP.NET MVC-Anwendung erstellt werden soll.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541012"
---
# <a name="aspnet-mvc-overview"></a>Übersicht über ASP.NET MVC

von [Microsoft](https://github.com/microsoft)

> Erfahren Sie mehr über die Unterschiede zwischen ASP.NET MVC-Anwendung und ASP.NET Web Forms-Anwendungen. Erfahren Sie, wie Sie entscheiden, wann eine ASP.NET MVC-Anwendung erstellt werden soll.

Das Model View Controller-Architekturschema (MVC) trennt eine Anwendung in drei Hauptkomponenten: das Modell, die Ansicht und den Controller. Das ASP.NET MVC-Framework bietet eine Alternative zum ASP.NET Web Forms-Muster zum Erstellen von MVC-basierten Webanwendungen. Das ASP.NET MVC-Framework ist ein schlankes und leicht zu testendes Präsentationsframework, das (wie Web Forms-basierte Anwendungen) in vorhandene ASP.NET-Funktionen, z. B. Gestaltungsvorlagen und mitgliedschaftsbasierte Authentifizierung, integriert ist. Das MVC-Framework ist im **Namespace System.Web.Mvc** definiert und ist ein grundlegender, unterstützter Teil des **System.Web-Namespace.**   
  
MVC ist ein Standardentwurfsschema, mit dem viele Entwickler bereits vertraut sind. Bestimmte Arten von Webanwendungen profitieren vom MVC-Framework. Andere werden weiterhin das herkömmliche ASP.NET-Anwendungsschema verwenden, das auf Web Forms und Postbacks basiert. Andere Arten von Webanwendungen werden beide Ansätze kombinieren, da kein Ansatz den anderen ausschließt.   
  
Das MVC-Framework beinhaltet die folgenden Komponenten:

[![Aufrufen einer Controlleraktion, die einen Parameterwert erwartet](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Abbildung 01**: Aufrufen einer Controlleraktion, die einen Parameterwert erwartet ([Klicken Sie hier, um das Bild in voller Größe anzuzeigen](asp-net-mvc-overview/_static/image2.png))

- **Modelle**. Modellobjekte sind die Teile der Anwendung, die die Logik für die Datendomäne der Anwendung implementieren. Häufig speichern und rufen Modellobjekte den Modellzustand aus einer Datenbank ab. Beispielsweise kann ein Produktobjekt Informationen aus einer Datenbank abrufen, darauf arbeiten und dann aktualisierte Informationen in eine Products-Tabelle in SQL Server zurückschreiben.

In kleinen Anwendungen ist das Modell häufig nur konzeptionell und nicht physisch von den anderen Komponenten getrennt. Wenn die Anwendung beispielsweise nur einen Datensatz liest und an die Ansicht sendet, verfügt die Anwendung nicht über eine physische Modellebene und zugeordnete Klassen. In diesem Fall übernimmt der Datensatz die Rolle eines Modellobjekts.

- **Ansichten**. Ansichten sind die Komponenten, die die Benutzeroberfläche der Anwendung anzeigen. In der Regel wird diese Benutzeroberfläche aus den Modelldaten erstellt. Ein Beispiel wäre eine Bearbeitungsansicht einer Tabelle "Produkte", in der Textfelder, Dropdownlisten und Kontrollkästchen basierend auf dem aktuellen Status eines Products-Objekts angezeigt werden.

- **Controller**. Die Controller-Komponenten behandeln Benutzerinteraktionen, arbeiten mit dem Modell und wählen im letzten Schritt die Ansicht aus, mit der die Benutzeroberfläche gerendert wird. In einer MVC-Anwendung zeigt die Ansicht nur Informationen an. Benutzereingaben und -interaktionen werden vom Controller verarbeitet und beantwortet. Der Controller verarbeitet z. B. Abfragezeichenfolgenwerte und übergibt diese Werte an das Modell, das wiederum die Datenbank mithilfe der Werte abfragt.

Mithilfe des MVC-Schemas können Sie Anwendungen erstellen, in denen die verschiedenen Aspekte der Anwendung (Eingabelogik, Geschäftslogik und Benutzeroberflächen-Logik) getrennt voneinander verwaltet werden können. Zwischen diesen Elementen werden lose Verknüpfungen bereitgestellt. Das Schema gibt an, wo die verschiedenen Logikbereiche in der Anwendung gespeichert werden. Die Benutzeroberflächenlogik ist Teil der Ansicht (view). Die Eingabelogik gehört zum Controller. Die Geschäftslogik gehört zum Modell. Durch diese Trennung lässt sich bei der Erstellung die Komplexität einer Anwendung leichter überblicken, da Sie sich jeweils auf einen Aspekt der Implementierung konzentrieren können. Sie können z. B. unabhängig von der Geschäftslogik die Ansicht entwickeln und optimieren.   
  
Zusätzlich zur Verwaltung der Komplexität erleichtert das MVC-Schema das Testen von Anwendungen im Vergleich zu Web Forms-basierten ASP.NET-Webanwendungen. In einer Web Forms-basierten ASP.NET-Webanwendung wird z. B. eine einzelne Klasse sowohl für die Anzeigeausgabe als auch für das Reagieren auf Benutzereingaben verwendet. Das Schreiben automatisierter Tests für Web Forms-basierte ASP.NET-Anwendungen kann sehr schwierig sein, da bereits zum Testen einer einzelnen Seite die Seitenklasse, alle untergeordneten Steuerelemente und zusätzliche abhängige Klassen in der Anwendung instanziiert werden müssen. Da zum Ausführen der Seite so viele Klassen instanziiert werden müssen, kann es schwierig werden, spezifische Tests für einzelne Teile der Anwendung zu schreiben. Tests für Web Forms-basierte ASP.NET-Anwendungen sind daher ggf. schwieriger zu implementieren als Tests in einer MVC-Anwendung. Darüber hinaus ist für Tests in einer Web Forms-basierten ASP.NET-Anwendung ein Webserver erforderlich. Das MVC-Framework entkoppelt die Komponenten und nutzt intensiv Schnittstellen, sodass einzelne Komponenten isoliert vom Rest des Frameworks getestet werden können.   
  
Die lose Verknüpfung zwischen den drei Hauptkomponenten einer MVC-Anwendung begünstigt auch die parallele Entwicklung. Beispielsweise kann ein Entwickler an der Ansicht arbeiten, ein zweiter Entwickler an der Controllerlogik und ein dritter Entwickler kann sich auf die Geschäftslogik im Modell konzentrieren.

## <a name="deciding-when-to-create-an-mvc-application"></a>Entscheiden, wann eine MVC-Anwendung erstellt werden soll

Sie müssen sorgfältig prüfen, ob eine Webanwendung besser mit dem ASP.NET MVC-Framework oder mit dem ASP.NET Web Forms-Modell implementiert werden kann. Das MVC-Framework ist kein Ersatz für das Web Forms-Modell. Sie können jedes der beiden Frameworks für Webanwendungen verwenden. (In der Funktionsweise vorhandener Web Forms-basierter Anwendungen gibt es keine Änderungen.)   
  
Bevor Sie sich bei einer bestimmten Website für die Verwendung des MVC-Frameworks oder des Web Forms-Modells entscheiden, wägen Sie die Vorteile beider Ansätze gegeneinander ab.

### <a name="advantages-of-an-mvc-based-web-application"></a>Vorteile einer MVC-basierten Webanwendung

Die ASP.NET MVC-Framework bietet die folgenden Vorteile:

- Komplexe Anwendungen können leichter verwaltet werden, indem die Anwendung in die Komponenten Modell, Ansicht und Controller unterteilt wird.
- Es verwendet keine Ansichtszustände und severbasierten Formulare. Dadurch eignet sich das MVC-Framework für Entwickler, die das Verhalten einer Anwendung präzise kontrollieren möchten.
- Es verwendet ein Frontcontroller-Schema, das Webanwendungsanforderungen durch einen einzelnen Controller verarbeitet. Auf diese Weise können Sie im Anwendungsentwurf eine umfangreiche Routinginfrastruktur unterstützen. Weitere Informationen finden Sie unter [Front Controller](https://go.microsoft.com/fwlink/?LinkId=106357 "Front-Controller") auf der MSDN-Website.
- Es bietet eine bessere Unterstützung für die testgesteuerte Entwicklung.
- Es eignet sich gut für Webanwendungen, die von großen Teams von Entwicklern und Webdesignern unterstützt werden, die ein hohes Maß an Kontrolle über das Anwendungsverhalten benötigen.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Vorteile einer Web Forms-basierten Webanwendung

Das Web Forms-basierte Framework bietet die folgenden Vorteile:

- Es unterstützt ein Ereignismodell, das den Zustand über HTTP beibehält. Dies bietet Vorteile für die Entwicklung von webbasierten Geschäftsanwendungen. Die Web Forms-basierte Anwendung stellt Dutzende von Ereignissen bereit, die in Hunderten von Serversteuerelementen unterstützt werden.
- Es verwendet ein Seitencontroller-Schema, mit dem Funktionalität für einzelne Seiten hinzugefügt wird. Weitere Informationen finden Sie unter [Seitencontroller](https://go.microsoft.com/fwlink/?LinkId=106359 "Seitencontroller") auf der MSDN-Website.
- Es verwendet Ansichtszustand oder serverbasierte Formulare, die die Verwaltung von Statusinformationen vereinfachen können.
- Es eignet sich gut für kleine Webentwicklerteams und für Designer, die auf die große Anzahl verfügbarer Komponenten zurückgreifen möchten, um die Anwendungsentwicklung zu beschleunigen.
- Im Allgemeinen ist es für die Anwendungsentwicklung weniger komplex, da die Komponenten **(die** Page-Klasse, Steuerelemente usw.) eng integriert sind und in der Regel weniger Code als das MVC-Modell erfordern.

## <a name="features-of-the-aspnet-mvc-framework"></a>Funktionen des ASP.NET MVC-Frameworks

Die ASP.NET MVC-Framework stellt die folgenden Funktionen bereit:

- Trennung von Anwendungsaufgaben (Eingabelogik, Geschäftslogik und UI-Logik), Testbarkeit und testgesteuerte Entwicklung (TDD) standardmäßig. Alle Kernverträge im MVC-Framework sind schnittstellenbasiert und können mit Pseudoobjekten getestet werden. Dabei handelt es sich um simulierte Objekte, die das Verhalten tatsächlicher Objekte in der Anwendung imitieren. Sie können Komponententests der Anwendung schnell und flexibel durchführen, ohne die Controller in einem ASP.NET-Prozess ausführen zu müssen. Sie können jedes Komponententestframework verwenden, das mit .NET Framework kompatibel ist.
- Ein erweiterbares und austauschbares Framework. Die Komponenten des ASP.NET MVC-Frameworks wurden so entworfen, dass sie leicht ausgetauscht oder angepasst werden können. Sie können eine eigene Ansichts-Engine, eigene URL-Routingrichtlinien, eine eigene Serialisierung für Aktionsmethodenparameter und andere Komponenten einbinden. Das ASP.NET MVC-Framework unterstützt auch die Verwendung der Abhängigkeitseinfügung (Dependency Injection, DI) und die Steuerungsumkehrung bei Containermodellen (Inversion of Control, IOC). Di ermöglicht es Ihnen, Objekte in eine Klasse einzuschleusen, anstatt sich auf die Klasse zu verlassen, um das Objekt selbst zu erstellen. IOC gibt an, dass ein Objekt ein benötigtes anderes Objekt aus einer externen Quelle, z. B. einer Konfigurationsdatei, abrufen soll. Tests werden dadurch einfacher.
- Eine leistungsstarke URL-Mapping-Komponente, mit der Sie Anwendungen mit verständlichen und durchsuchbaren URLs erstellen können. URLs müssen keine Dateinamenerweiterungen beinhalten und sind so konzipiert, dass die URL-Benennungsschemas für Suchmaschinen und REST (Representational State Transfer)-Adressierung optimiert werden können.
- Unterstützung für das Verwenden von Markup aus vorhandenen Markupdateien für ASP.NET-Seiten (ASPX-Dateien), Benutzersteuerelemente (ASCX-Dateien) und Gestaltungsvorlagen (MASTER-Dateien) als Ansichtsvorlagen. Sie können vorhandene ASP.NET-Features mit dem ASP.NET MVC-Framework verwenden, z. B. verschachtelte Masterseiten, Inline-Ausdrücke (&lt;%= %&gt;), deklarative Serversteuerelemente, Vorlagen, Datenbindung, Lokalisierung usw.
- Unterstützung für vorhandene ASP.NET-Funktionen. Mit ASP.NET MVC können Sie bereits vorhandene Funktionen weiterverwenden, z. B. Formular- und Windows-Authentifizierung, URL-Autorisierung, Mitgliedschaft und Rollen, Zwischenspeichern von Ausgaben und Daten, Sitzungs- und Profilzustandsverwaltung, Systemüberwachung, das Konfigurationssystem und die Anbieterarchitektur.
