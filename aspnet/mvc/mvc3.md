---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (enthält Das Tools Update vom April 2011) ASP.NET MVC 3 ist ein Framework zum Erstellen skalierbarer, standardbasierter Webanwendungen mit gut etablierten Designmustern...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675138"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(enthält Das Tools Update vom April 2011)*
> 
> ASP.NET MVC 3 ist ein Framework zum Erstellen skalierbarer, standardbasierter Webanwendungen unter Verwendung gut etablierter Entwurfsmuster und der Leistungsfähigkeit von ASP.NET und .NET Framework.
> 
> Es installiert Seite an Seite mit ASP.NET MVC 2, so starten Sie es heute!
> 
> Laden Sie das [Installationsprogramm hier](https://microsoft.com/download/details.aspx?id=4211) herunter

## <a name="top-features"></a>Top Features

- Integriertes Gerüstsystem erweiterbar über NuGet
- HTML 5-fähige Projektvorlagen
- Ausdrucksstarke Ansichten einschließlich der neuen Razor View Engine
- Leistungsstarke Haken mit Abhängigkeitsinjektion und globalen Aktionsfiltern
- Umfangreiche JavaScript-Unterstützung mit unauffälliger JavaScript-, jQuery-Validierung und JSON-Bindung
- *Lesen Sie die vollständige Funktionsliste [unten](#overview)*

## <a name="top-links"></a>Top Links

Neuerungen in ASP.NET MVC 3

- Phil Haack: [ASP.NET MVC 3 veröffentlicht](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express und Orchard veröffentlicht - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [Ankündigung der Veröffentlichung von ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [Versionshinweise für ASP.NET MVC 3](../whitepapers/mvc3-release-notes.md)

Installation und Hilfe

- Installieren ASP.NET MVC 3 mit dem [Web Platform Installer (empfohlen)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- Installieren ASP.NET MVC 3 mit der [ausführbaren Installationsdatei](https://go.microsoft.com/fwlink/?LinkID=208140)
- Installieren [ASP.NET MVC 3 für Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)
- Lesen Sie das [Intro to ASP.NET MVC 3 Tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- Holen Sie sich Hilfe und diskutieren Sie ASP.NET MVC 3 in den [Foren](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 Overview

ASP.NET MVC 3 baut auf ASP.NET MVC 1 und 2 auf und fügt großartige Funktionen hinzu, die Ihren Code vereinfachen und eine tiefere Erweiterbarkeit ermöglichen. Dieses Thema bietet einen Überblick über viele der neuen Funktionen, die in dieser Version enthalten sind und in den folgenden Abschnitten unterteilt sind:

- [Ausziehbares Gerüst mit MvcScaffold-Integration](#BM_MvcScaffolding)
- [HTML 5-fähige Projektvorlagen](#BM_HTML5)
- [Die Razor View Engine](#BM_TheRazorViewEngine)
- [Unterstützung für Multiple View Engines](#BM_Support_for_Multiple_View_Engines)
- [Controller-Verbesserungen](#BM_Controller_Improvements)
- [JavaScript und Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [Verbesserungen bei der Modellvalidierung](#BM_Model_Validation_Improvements)
- [Verbesserungen bei der Abhängigkeitsinjektion](#BM_Dependency_Injection_Improvements)
- [Weitere neue Funktionen](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>Ausziehbares Gerüst mit MvcScaffold-Integration

Das neue Gerüstsystem erleichtert das aufnehmen und produktive Verwenden von Produktionsvorgängen, wenn Sie völlig neu im Framework sind, und die Automatisierung gängiger Entwicklungsaufgaben, wenn Sie erfahren sind und bereits wissen, was Sie tun.

Dies wird durch das neue *NuGet-Gerüstpaket* namens **MvcScaffolding**unterstützt. Der Begriff "Gerüstbau" wird von vielen Softwaretechnologien verwendet, um zu bedeuten, dass "schnell eine grundlegende Gliederung Ihrer Software generiert wird, die Sie dann bearbeiten und anpassen können". Das Gerüstpaket, das wir für ASP.NET MVC erstellen, ist in mehreren Szenarien von großem Nutzen:

- **Wenn Sie zum ersten Mal ASP.NET MVC lernen,** weil es Ihnen eine schnelle Möglichkeit gibt, einen nützlichen, funktionierenden Code zu erhalten, den Sie dann bearbeiten und an Ihre Bedürfnisse anpassen können. Es erspart Ihnen das Trauma, auf eine leere Seite zu schauen und keine Ahnung zu haben, wo Sie anfangen sollen!
- **Wenn Sie ASP.NET MVC gut kennen und jetzt einige neue Add-On-Technologie** wie einen objektrelationalen Mapper, ein Ansichtsmodul, eine Testbibliothek usw. erkunden, weil der Ersteller dieser Technologie möglicherweise auch ein Gerüstpaket dafür erstellt hat.
- **Wenn Ihre Arbeit wiederholt das Erstellen ähnlicher Klassen oder Dateien einer Art umfasst,** da Sie benutzerdefinierte Gerüste erstellen können, die Testgeräte, Bereitstellungsskripts oder was auch immer Sie benötigen. Jeder in Ihrem Team kann auch Ihre benutzerdefinierten Gerüste verwenden.

Weitere Funktionen in MvcScaffolding sind:

- Unterstützung von C- und VB-Projekten
- Unterstützung für die Razor- und ASPX-Ansichtsmodule
- Unterstützt Gerüste in ASP.NET MVC-Bereichen und mit benutzerdefinierten Ansichtslayouts/Mastern
- Sie können die Ausgabe ganz einfach anpassen, indem Sie T4-Vorlagen bearbeiten
- Sie können komplett neue Gerüste mit benutzerdefinierter PowerShell-Logik und benutzerdefinierten T4-Vorlagen hinzufügen. Diese (und alle benutzerdefinierten Parameter, die Sie ihnen gegeben haben) werden automatisch in der Liste der Konsolenregisterkarten-Vervollständigung angezeigt.
- Sie können NuGet-Pakete mit zusätzlichen Gerüsten für verschiedene Technologien (z. B. es gibt jetzt ein Proof-of-Concept-Paket für LINQ to SQL) erhalten und diese miteinander kombinieren.

Das ASP.NET MVC 3 Tools Update bietet großartige Visual Studio-Unterstützung für dieses Gerüstsystem, z. B.:

- Das Dialogfeld "Controller hinzufügen" unterstützt jetzt das vollständige automatische Gerüst von Aktionen erstellen, Lesen, Aktualisieren und Löschen von Controllern und entsprechenden Ansichten. Standardmäßig wird dieser Datenzugriffscode mithilfe von EF Code First auf Gerüste verwendet.
- Add Controller Dialog unterstützt *erweiterbare Gerüste* über NuGet-Pakete wie *MvcScaffolding*. Dies ermöglicht das Einstecken von benutzerdefinierten Gerüsten in den Dialog, mit dem Sie Gerüste für andere Datenzugriffstechnologien wie NHibernate oder sogar JET mit ODBCDirect erstellen können, wenn Sie so geneigt sind!

Weitere Informationen zu Gerüstbau in ASP.NET MVC 3 finden Sie in den folgenden Ressourcen:

- Steve Sandersons Post-Serie, einschließlich: 

    1. [Einführung: Gerüst Ihrer ASP.NET MVC 3 Projekt mit dem MvcScaffolding Paket](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Standardverwendung: Typische Anwendungsfälle und Optionen](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Eins-zu-viele-Beziehungen](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Gerüstaktionen und Komponententests](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [Überschreiben der T4-Vorlagen](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Dieser Beitrag: Erstellen von benutzerdefinierten Gerüsten](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Scott Hanselmans Beitrag aus seiner PDC 2010-Sitzung [Aufbau eines Blogs mit Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 Versionshinweise](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5-Projektvorlagen

Das Dialogfeld Neues Projekt enthält ein Kontrollkästchen aktivieren HTML 5-Versionen von Projektvorlagen. Diese Vorlagen nutzen Modernizr 1.7, um Kompatibilitätsunterstützung für HTML 5 und CSS 3 in Down-Level-Browsern bereitzustellen.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Die Razor View Engine

ASP.NET MVC 3 kommt mit einer neuen Ansichts-Engine namens Razor, die die folgenden Vorteile bietet:

- Die Razor-Syntax ist sauber und prägnant und erfordert eine minimale Anzahl von Tastenanschlägen.
- Razor ist leicht zu erlernen, zum Teil, weil es auf vorhandenen Sprachen wie C und Visual Basic basiert.
- Visual Studio enthält IntelliSense und Codefarben für die Razor-Syntax.
- Razor-Ansichten können komponentengetestet werden, ohne dass Sie die Anwendung ausführen oder einen Webserver starten müssen.

Zu den neuen Razor-Funktionen gehören die folgenden:

- `@model`Syntax zum Angeben des Typs, der an die Ansicht übergeben wird.
- `@* *@`Kommentarsyntax.
- Die Möglichkeit, Standardwerte (z. `layoutpage`B. ) einmal für eine gesamte Site anzugeben.
- Die `Html.Raw` Methode zum Anzeigen von Text ohne HTML-Codierung.
- Unterstützung für die gemeinsame Nutzung von Code für mehrere Ansichten*\_(viewstart.cshtml* oder * \_viewstart.vbhtml-Dateien).*

Razor enthält auch neue HTML-Hilfsprogramme, z. B. die folgenden:

- `Chart`. Rendert ein Diagramm und bietet die gleichen Funktionen wie das Diagrammsteuerelement in ASP.NET 4.
- `WebGrid`. Rendert ein Datenraster mit Paging- und Sortierfunktionalität.
- `Crypto`. Verwendet Hashalgorithmen, um richtig gesalzene und gehashte Kennwörter zu erstellen.
- `WebImage`. Rendert ein Bild.
- `WebMail`. Sendet eine E-Mail.

Weitere Informationen zu Razor finden Sie in den folgenden Ressourcen:

- [Scott Guthries Blogbeitrag zur Einführung von Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Scott Guthries Blogbeitrag zur @model Einführung des Keywords](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Scott Guthries Blogbeitrag zur Einführung von Razor-Layouts](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Razor API Kurzübersicht](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 Versionshinweise](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Unterstützung für Multiple View Engines

Im Dialogfeld **Ansicht** hinzufügen in ASP.NET MVC 3 können Sie das Ansichtsmodul auswählen, mit dem Sie arbeiten möchten, und im Dialogfeld **Neues Projekt** können Sie das Standardansichtsmodul für ein Projekt angeben. Sie können das Web Forms-Ansichtsmodul (ASPX), Razor oder ein Open-Source-Ansichtsmodul wie [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/)oder [NDjango](http://ndjango.org/)auswählen.

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Controller-Verbesserungen

### <a name="global-action-filters"></a>Globale Aktionsfilter

Manchmal möchten Sie Logik ausführen, entweder bevor eine Aktionsmethode ausgeführt wird, oder nachdem eine Aktionsmethode ausgeführt wurde. Um dies zu unterstützen, stellte ASP.NET MVC 2 Aktionsfilter bereit. Aktionsfilter sind benutzerdefinierte Attribute, die eine deklarative Möglichkeit bieten, bestimmten Controlleraktionsmethoden Vor- und Nachaktionsverhalten hinzuzufügen. In einigen Fällen sollten Sie jedoch das Verhalten vor der Aktion oder nach der Aktion angeben, das für alle Aktionsmethoden gilt. Mit MVC 3 können Sie globale `GlobalFilters` Filter angeben, indem Sie sie der Auflistung hinzufügen. Weitere Informationen zu globalen Aktionsfiltern finden Sie in den folgenden Ressourcen:

- [Scott Guthries Blog zur MVC 3 Vorschau](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [Filtern in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Neue "ViewBag"-Eigenschaft

MVC 2-Controller `ViewData` unterstützen eine Eigenschaft, mit der Sie Daten mithilfe einer spät gebundenen Wörterbuch-API an eine Ansichtsvorlage übergeben können. In MVC 3 können Sie auch eine `ViewBag` etwas einfachere Syntax mit der Eigenschaft verwenden, um den gleichen Zweck zu erfüllen. Anstatt beispielsweise zu `ViewData["Message"]="text"`schreiben, können `ViewBag.Message="text"`Sie schreiben. Sie müssen keine stark typisierten Klassen definieren, `ViewBag` um die Eigenschaft zu verwenden. Da es sich um eine dynamische Eigenschaft handelt, können Sie stattdessen einfach Eigenschaften abrufen oder festlegen, und sie werden zur Laufzeit dynamisch aufgelöst. Intern `ViewBag` werden Eigenschaften als Name/Wert-Paare im `ViewData` Wörterbuch gespeichert. (Hinweis: In den meisten Vorabversionen von `ViewBag` MVC 3 `ViewModel` wurde die Eigenschaft als Eigenschaft bezeichnet.)

### <a name="new-actionresult-types"></a>Neue "ActionResult"-Typen

Die `ActionResult` folgenden Typen und die entsprechenden Hilfsmethoden sind in MVC 3 neu oder verbessert:

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). Gibt einen 404 HTTP-Statuscode an den Client zurück.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Gibt eine temporäre Umleitung (HTTP 302-Statuscode) oder eine permanente Umleitung (HTTP 301-Statuscode) zurück, abhängig von einem booleschen Parameter. In Verbindung mit dieser Änderung verfügt die [Controller-Klasse](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) nun `RedirectPermanent`über `RedirectToRoutePermanent`drei `RedirectToActionPermanent`Methoden zum Ausführen permanenter Umleitungen: , und . Diese Methoden geben `RedirectResult` eine `Permanent` Instanz von `true`zurück, deren Eigenschaft auf festgelegt ist.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Gibt einen benutzerdefinierten HTTP-Statuscode zurück.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript- und Ajax-Verbesserungen

Standardmäßig verwenden Ajax- und Validierungshelfer in MVC 3 einen unauffälligen JavaScript-Ansatz. Unauffälliges JavaScript vermeidet das Einfügen von Inline-JavaScript in HTML. Dies macht Ihren HTML-Code kleiner und weniger unübersichtlich und erleichtert das Austauschen oder Anpassen von JavaScript-Bibliotheken. Validierungshelfer in MVC `jQueryValidate` 3 verwenden das Plugin standardmäßig auch. Wenn Sie MVC 2-Verhalten wünschen, können Sie unauffälliges JavaScript mithilfe einer *web.config-Dateieinstellung* deaktivieren. Weitere Informationen zu JavaScript- und Ajax-Verbesserungen finden Sie in den folgenden Ressourcen:

- [Grundlegende Einführung in unauffälliges JavaScript auf der Wikipedia-Seite](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilsons unauffälliger JavaScript-Beitrag](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilsons unauffälliger JavaScript-Validierungsbeitrag](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Erstellen einer MVC 3-Anwendung mit Razor und unauffälligem JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (Tutorial auf der ASP.NET-Website)
- [MVC 3 Versionshinweise](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Clientseitige Validierung standardmäßig aktiviert

In früheren Versionen von MVC müssen `Html.EnableClientValidation` Sie die Methode explizit aus einer Ansicht aufrufen, um die clientseitige Validierung zu aktivieren. In MVC 3 ist dies nicht mehr erforderlich, da die clientseitige Validierung standardmäßig aktiviert ist. (Sie können dies mithilfe einer Einstellung in der Datei *web.config* deaktivieren.)

Damit die clientseitige Validierung funktioniert, müssen Sie weiterhin auf die entsprechenden jQuery- und jQuery-Validierungsbibliotheken in Ihrer Site verweisen. Sie können diese Bibliotheken auf Ihrem eigenen Server hosten oder über ein Content Delivery Network (CDN) wie die CDNs von Microsoft oder Google verweisen.

### <a name="remote-validator"></a>Remote-Validator

ASP.NET MVC 3 unterstützt die neue [RemoteAttribute-Klasse,](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) mit der Sie die Remote-Validator-Unterstützung des jQuery Validation-Plug-Ins nutzen können. Dadurch kann die clientseitige Validierungsbibliothek automatisch eine benutzerdefinierte Methode aufrufen, die Sie auf dem Server definieren, um Validierungslogik auszuführen, die nur serverseitig ausgeführt werden kann.

Im folgenden Beispiel `Remote` gibt das Attribut an, dass `UserNameAvailable` die `UsersController` Clientüberprüfung eine Aktion `UserName` mit dem Namen für die Klasse aufruft, um das Feld zu überprüfen.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

Das folgende Beispiel zeigt den entsprechenden Controller.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Weitere Informationen zur Verwendung `Remote` des Attributs finden Sie unter [Gewusst wie: Implementieren der Remotevalidierung in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in der MSDN-Bibliothek.

### <a name="json-binding-support"></a>JSON-Bindungsunterstützung

ASP.NET MVC 3 enthält integrierte JSON-Bindungsunterstützung, die es Aktionsmethoden ermöglicht, JSON-codierte Daten zu empfangen und an Aktionsmethodenparameter zu binden. Diese Funktion ist in Szenarien mit Clientvorlagen und Datenbindung nützlich. (Mit Clientvorlagen können Sie ein einzelnes Datenelement oder einen Satz von Datenelementen mithilfe von Vorlagen formatieren und anzeigen, die auf dem Client ausgeführt werden.) Mit MVC 3 können Sie Clientvorlagen einfach mit Aktionsmethoden auf dem Server verbinden, die JSON-Daten senden und empfangen. Weitere Informationen zur JSON-Bindungsunterstützung finden Sie im Abschnitt **JavaScript und AJAX-Verbesserungen** im [Blogbeitrag MVC 3 Preview von Scott Guthrie](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Verbesserungen bei der Modellvalidierung

### <a name="dataannotations-metadata-attributes"></a>Metadatenattribute "DataAnnotations"

ASP.NET MVC `DataAnnotations` 3 unterstützt Metadatenattribute wie `DisplayAttribute`.

### <a name="validationattribute-class"></a>Klasse "ValidationAttribute"

Die `ValidationAttribute` Klasse wurde in .NET Framework 4 `IsValid` verbessert, um eine neue Überladung zu unterstützen, die weitere Informationen zum aktuellen Validierungskontext bereitstellt, z. B. welches Objekt überprüft wird. Dies ermöglicht umfangreichere Szenarien, in denen Sie den aktuellen Wert basierend auf einer anderen Eigenschaft des Modells überprüfen können. Mit dem neuen `CompareAttribute` Attribut können Sie beispielsweise die Werte von zwei Eigenschaften eines Modells vergleichen. Im folgenden Beispiel `ComparePassword` muss die `Password` Eigenschaft mit dem Feld übereinstimmen, um gültig zu sein.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Validierungsschnittstellen

Mit der [IValidatableObject-Schnittstelle](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) können Sie eine Validierung auf Modellebene durchführen und Validierungsfehlermeldungen bereitstellen, die für den Status des Gesamtmodells oder zwischen zwei Eigenschaften innerhalb des Modells spezifisch sind. MVC 3 ruft nun `IValidatableObject` Fehler von der Schnittstelle bei der Modellbindung ab und kennzeichnet oder hebt die betroffenen Felder in einer Ansicht mithilfe der integrierten HTML-Formularhilfsprogramme automatisch an.

Die [IClientValidatable-Schnittstelle](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) ermöglicht es ASP.NET MVC zur Laufzeit zu ermitteln, ob ein Validator Unterstützung für die Clientvalidierung bietet. Diese Schnittstelle wurde so konzipiert, dass sie in eine Vielzahl von Validierungsframeworks integriert werden kann.

Weitere Informationen zu Validierungsschnittstellen finden Sie im Abschnitt **Verbesserungen bei der Modellvalidierung** im [Blogbeitrag MVC 3 Preview von Scott Guthrie](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx). (Beachten Sie jedoch, dass der Verweis auf "IValidateObject" im Blog "IValidatableObject" sein sollte.)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Verbesserungen bei der Abhängigkeitsinjektion

ASP.NET MVC 3 bietet eine bessere Unterstützung für die Anwendung von Dependency Injection (DI) und die Integration mit Dependency Injection oder Inversion of Control (IOC)-Containern. Unterstützung für DI wurde in den folgenden Bereichen hinzugefügt:

- Controller (Registrieren und Einspritzen von Controller-Fabriken, Injizieren von Controllern).
- Ansichten (Registrieren und Einfügen von Ansichtsmodulen, Einfügen von Abhängigkeiten in Ansichtsseiten).
- Aktionsfilter (Suchen und Einspritzen von Filtern).
- Modellbindemittel (Registrieren und Injizieren).
- Modellvalidierungsanbieter (Registrieren und Einspritzen).
- Modellieren von Metadatenanbietern (Registrieren und Einfügen).
- Wertanbieter (Registrieren und Einspritzen).

MVC 3 unterstützt die [Common Service Locator-Bibliothek](https://github.com/unitycontainer/commonservicelocator) und `IServiceLocator` alle DI-Container, die die Schnittstelle dieser Bibliothek unterstützen. Es unterstützt auch `IDependencyResolver` eine neue Schnittstelle, die die Integration von DI-Frameworks erleichtert.

Weitere Informationen zu DI in MVC 3 finden Sie in den folgenden Ressourcen:

- [Brad Wilsons Serie von Blogbeiträgen auf Service Location](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 Versionshinweise](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Weitere neue Funktionen

### <a name="nuget-integration"></a>NuGet-Integration

ASP.NET MVC 3 installiert und aktiviert NuGet automatisch als Teil seiner Einrichtung. NuGet ist ein kostenloser Open-Source-Paket-Manager, der das Auffinden, Installieren und Verwenden von .NET-Bibliotheken und -Tools in Ihren Projekten erleichtert. Es funktioniert mit allen Visual Studio-Projekttypen (einschließlich ASP.NET Web Forms und ASP.NET MVC).

NuGet ermöglicht Entwicklern, die Open-Source-Projekte verwalten (z. B. Projekte wie Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks und Elmah), ihre Bibliotheken zu verpacken und in einer Online-Galerie zu registrieren. Es ist dann einfach für .NET-Entwickler, die eine dieser Bibliotheken verwenden möchten, um das Paket zu finden und es in Projekten zu installieren, an denen sie arbeiten.

Mit dem ASP.NET 3 Tools Update enthalten Projektvorlagen JavaScript-Bibliotheken vorinstallierte NuGet-Pakete, sodass sie über NuGet aufrüstbar sind. Entity Framework Code First ist auch als NuGet-Paket vorinstalliert.

Weitere Informationen zu NuGet finden Sie in der [NuGet-Dokumentation](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Partipartielle Ausgabezwischenspeicherung

ASP.NET MVC unterstützt seit Version 1 das Zwischenspeichern von ganzseitigen Antworten. MVC 3 unterstützt auch partielle Ausgabezwischenspeicherung, mit der Sie Regionen oder Fragmente einer Antwort problemlos zwischenspeichern können. Weitere Informationen zum Caching finden Sie im Abschnitt **Partpartielle Seitenausgabezwischenspeicherung** in [Scott Guthries Blogbeitrag zum MVC 3-Release-Kandidaten](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) und im Abschnitt **Child Action Output Caching** der [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).

### <a name="granular-control-over-request-validation"></a>Granular Control over Request Validation

ASP.NET MVC verfügt über eine integrierte Anforderungsvalidierung, die automatisch vor XSS- und HTML-Injektionsangriffen schützt. Manchmal möchten Sie jedoch die Anforderungsüberprüfung explizit deaktivieren, z. B. wenn Sie Benutzern das Posten von HTML-Inhalten erlauben möchten (z. B. in Blogeinträgen oder CMS-Inhalten). Sie können nun ein [AllowHtml-Attribut](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) zu Modellen oder Ansichtsmodellen hinzufügen, um die Anforderungsüberprüfung pro Eigenschaft während der Modellbindung zu deaktivieren. Weitere Informationen zur Anforderungsüberprüfung finden Sie in den folgenden Ressourcen:

- Der Abschnitt **Unobtrusive JavaScript and Validation** in [Scott Guthries Blogbeitrag zum MVC 3 Release-Kandidaten](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).
- [MVC 3 Versionshinweise](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Erweiterbare Dialogbox "Neues Projekt"

In ASP.NET MVC 3 können Sie dem Dialogfeld Neues **Projekt** Projektvorlagen, Anzeigen von Modulen und Komponententestprojektframeworks hinzufügen.

### <a name="template-scaffolding-improvements"></a>Vorlagengerüstverbesserungen

ASP.NET MVC 3-Gerüstvorlagen können Primärschlüsseleigenschaften in Modellen besser identifizieren und entsprechend behandeln als in früheren Versionen von MVC. (Die Gerüstvorlagen stellen jetzt beispielsweise sicher, dass der Primärschlüssel nicht als bearbeitbares Formularfeld erstellt wird.)

Standardmäßig verwenden die Gerüste Erstellen und Bearbeiten `Html.EditorFor` jetzt den `Html.TextBoxFor` Helfer anstelle des Hilfss. Dadurch wird die Unterstützung für Metadaten im Modell in Form von Datenanmerkungsattributen verbessert, wenn im Dialogfeld Ansicht **hinzufügen** eine Ansicht generiert wird.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>Neue Überladungen für "Html.LabelFor" und "Html.LabelForModel"

Für die `LabelFor` und-Hilfsmethoden `LabelForModel` wurden neue Methodenüberladungen hinzugefügt. Mit den neuen Überladungen können Sie den Beschriftungstext angeben oder überschreiben.

### <a name="sessionless-controller-support"></a>Sessionless Controller-Unterstützung

In ASP.NET MVC 3 können Sie angeben, ob eine Controllerklasse den Sitzungsstatus verwenden soll und wenn ja, ob der Sitzungsstatus schreibgeschützt oder schreibgeschützt sein soll. Weitere Informationen zur Unterstützung sitzungsloser Controller finden Sie unter [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Neue "AdditionalMetadataAttribute"-Klasse

Sie können das [Attribut AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) verwenden, um das `ModelMetadata.AdditionalValues` Wörterbuch für eine Modelleigenschaft aufzufüllen. Wenn ein Ansichtsmodell beispielsweise über eine Eigenschaft verfügt, die nur einem Administrator angezeigt werden soll, können Sie diese Eigenschaft wie im folgenden Beispiel gezeigt mit Anmerkungen kommentieren:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Diese Metadaten werden für jede Anzeige- oder Editorvorlage verfügbar gemacht, wenn ein Produktansichtsmodell gerendert wird. Es liegt an Ihnen, die Metadateninformationen zu interpretieren.

### <a name="accountcontroller-improvements"></a>KontoController-Verbesserungen

Der AccountController in der Internetprojektvorlage wurde erheblich verbessert.

### <a name="new-intranet-project-template"></a>Neue Intranetprojektvorlage

Eine neue Intranetprojektvorlage ist enthalten, die die Windows-Authentifizierung aktiviert und den AccountController entfernt.
