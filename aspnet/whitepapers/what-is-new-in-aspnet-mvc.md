---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: Neues in ASP.NET MVC 2 | Microsoft-Dokumentation
author: rick-anderson
description: Dieses Dokument beschreibt die neuen Features und Verbesserungen, die in ASP.NET MVC 2 eingeführt wurden. Dieses Dokument steht auch zum Herunterladen zur Verfügung.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045038"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>Neue Funktionen in ASP.NET MVC 2

> Dieses Dokument beschreibt die neuen Features und Verbesserungen, die in ASP.NET MVC 2 eingeführt wurden. Dieses Dokument steht auch zum [herunterladen](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf) zur Verfügung.

[Einführung](#_TOC1)   
[Aktualisieren eines ASP.NET MVC 1,0-Projekts auf ASP.NET MVC 2](#_TOC2)   
[Neue Features](#_TOC3)   
[Auf Vorlagen basierende Hilfsprogramme](#_TOC3_1)   
[Felder](#_TOC3_2)   
[Unterstützung für asynchrone Controller](#_TOC3_3)   
[Unterstützung für DefaultValueAttribute in Action-Method-Parametern](#_TOC3_4)   
[Unterstützung für das Binden von Binärdaten mit Modell Binder](#_TOC3_5)   
[Modelmetadata-und ModelMetadataProvider-Klassen](#_TOC3_6)   
[Unterstützung für DataAnnotations-Attribute](#_TOC3_7)   
[Modell Validierungs Steuerelement-Anbieter](#_TOC3_8)   
[Client seitige Validierung](#_TOC3_9)   
[Neue Code Ausschnitte für Visual Studio 2010](#_TOC3_10)   
[Neuer Requirements httpsattribute-Aktions Filter](#_TOC3_11)   
[Überschreiben des HTTP-Methoden Verbs](#_TOC3_12)   
[Neue hiddeninputattribute-Klasse für auf Vorlagen basierende Hilfsprogramme](#_TOC3_13)   
[Die HTML. ValidationSummary-Hilfsmethode kann Fehler auf Modell Ebene anzeigen.](#_TOC3_14)   
[T4-Vorlagen in Visual Studio generieren Code, der für die Ziel Version der .NET Framework](#_TOC3_15)[API-Verbesserungen](#_TOC4) spezifisch ist.  
[Wichtige Änderungen](#_TOC5)  
[Haftungsausschluss](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  Einführung

ASP.NET MVC 2 baut auf ASP.NET MVC 1,0 auf und führt einen großen Satz von Erweiterungen und Features ein, die sich auf die Steigerung der Produktivität konzentrieren. Diese Version ist mit ASP.NET MVC 1,0 kompatibel, sodass Ihre Kenntnisse, Kenntnisse, Code und Erweiterungen für ASP.NET MVC 1,0 weiterhin angewendet werden.

Weitere Informationen zu ASP.NET MVC finden Sie in den folgenden Ressourcen:

- [ASP.NET MVC-Dokumentation auf MSDN](https://go.microsoft.com/fwlink/?LinkId=159758)
- [Die ASP.NET-MVC-Website](https://asp.net/mvc/)
- [Die ASP.NET-MVC-Foren](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  Aktualisieren eines ASP.NET MVC 1,0-Projekts auf ASP.NET MVC 2

ASP.NET MVC 2 kann parallel zu ASP.NET MVC 1,0 auf dem gleichen Server installiert werden, was Anwendungsentwicklern Flexibilität bei der Wahl bietet, wann eine ASP.NET MVC 1,0-Anwendung auf ASP.NET MVC 2 aktualisiert werden soll. Weitere Informationen zum Upgrade finden Sie im Dokument [Aktualisieren einer ASP.NET MVC 1,0-Anwendung auf ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).

## <a name="new-features"></a><a id="_TOC3"></a>  Neue Features

In diesem Abschnitt werden die Funktionen beschrieben, die in der MVC 2-Version eingeführt wurden.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  Auf Vorlagen basierende Hilfsprogramme

Mit Vorlagen basierten Hilfsprogrammen können Sie automatisch HTML-Elemente für die Bearbeitung und Anzeige von Datentypen zuordnen. Wenn z. b. Daten vom Typ System. DateTime in einer Ansicht angezeigt werden, kann ein Benutzeroberflächen Element für die Datumsauswahl automatisch gerendert werden. Dies ähnelt der Funktionsweise von Feld Vorlagen in ASP.net-dynamische Daten. Weitere Informationen finden Sie unter [Verwenden von Vorlagen Hilfen zum Anzeigen von Daten](https://go.microsoft.com/fwlink/?LinkId=159062) auf der MSDN-Website.

### <a name="areas"></a><a id="_TOC3_2"></a>  Felder

Mit Bereichen können Sie ein umfangreiches Projekt in mehreren kleineren Abschnitten organisieren, um die Komplexität einer großen Webanwendung zu verwalten. Jeder Abschnitt ("Bereich") stellt in der Regel einen separaten Abschnitt einer großen Website dar und dient zum Gruppieren verwandter Gruppen von Controllern und Ansichten. Weitere Informationen finden Sie unter Exemplarische Vorgehensweise [: Organisieren einer ASP.NET MVC-Anwendung nach Bereichen](https://go.microsoft.com/fwlink/?LinkId=158978) auf der MSDN-Website.

Um einen neuen Bereich zu erstellen, klicken Sie in Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, klicken Sie auf Hinzufügen, und klicken Sie dann auf Bereich. Dadurch wird ein Dialogfeld angezeigt, in dem Sie zur Eingabe des Bereichs Namens aufgefordert werden. Nachdem Sie den Bereichs Namen eingegeben haben, fügt Visual Studio dem Projekt einen neuen Bereich hinzu.

Die folgende Abbildung zeigt ein Beispiel Layout für ein Projekt mit zwei Bereichen: admin und Blogs.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

Wenn Sie einen Bereich erstellen, fügt Visual Studio eine Klasse, die von AreaRegistration abgeleitet ist, zu jedem Bereich hinzu. Diese Klasse ist erforderlich, um den Bereich und seine Routen zu registrieren, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

Die Standard Projektvorlage für ASP.NET MVC 2 enthält einen aufzurufenden Befehl der registerallareas-Methode im Code für die Datei Global. asax. Diese Methode registriert jeden Bereich im Projekt, indem nach allen Typen gesucht wird, die von der AreaRegistration-Klasse abgeleitet werden, wobei eine Instanz des Typs instanziiert und anschließend die RegisterArea-Methode für die Instanz aufgerufen wird. Das folgende Beispiel zeigt, wie dies geschieht.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Wenn Sie den Namespace nicht in der RegisterArea-Methode angeben, indem Sie den Kontext aufrufen. Namespaces. Add-Methode, der Namespace der Registrierungs Klasse wird standardmäßig verwendet.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  Unterstützung für asynchrone Controller

ASP.NET MVC 2 ermöglicht es Controllern nun, Anforderungen asynchron zu verarbeiten. Dies kann zu Leistungssteigerungen führen, indem Server, die häufig blockierende Vorgänge (z. b. Netzwerk Anforderungen) aufzurufen, anstelle von nicht blockierenden Gegenstücken aufgerufen werden. Weitere Informationen finden Sie im Thema [using an Asynchronous Controller in ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) auf MSDN.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  Unterstützung für DefaultValueAttribute in Action-Method-Parametern

Die System. ComponentModel. DefaultValueAttribute-Klasse ermöglicht es, einen Standardwert für den Argument Parameter an eine Aktionsmethode bereitzustellen. Nehmen Sie beispielsweise an, dass die folgende Standardroute definiert ist:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

Nehmen Sie auch an, dass der folgende Controller und die folgende Aktionsmethode definiert sind:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Jede der folgenden Anforderungs-URLs Ruft die Ansichts Aktionsmethode auf, die im vorherigen Beispiel definiert ist.

- /Article/View/123
- /Article/View/123? Seite = 1 (identisch mit der vorherigen Anforderung)
- /Article/View/123? Seite = 2

Ohne das DefaultValueAttribute-Attribut wäre die erste URL aus der vorangehenden Liste nicht funktionsfähig, da das Seiten Argument ein Werttyp ist, der keine NULL-Werte zulässt, dessen Wert nicht angegeben wurde.

Wenn Ihr Code in Visual Basic 2010 oder Visual c# 2010 geschrieben ist, können Sie anstelle des Attributs DefaultValueAttribute optionale Parameter verwenden, wie im folgenden Beispiel gezeigt:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  Unterstützung für das Binden von Binärdaten mit Modell Binder

Es gibt zwei neue über Ladungen des HTML. Hidden-Hilfsobjekts, das binäre Werte als Base-64-codierte Zeichen folgen codiert:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Eine typische Verwendung besteht darin, einen Zeitstempel für ein Objekt in der Ansicht einzubetten. Die Anwendung kann z. b. das folgende Product-Objekt enthalten:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Ein Bearbeitungs Formular kann die Timestamp-Eigenschaft im Formular darstellen, wie im folgenden Beispiel gezeigt:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Dieses Markup rendert ein verborgenes Eingabe Element mit dem Zeitstempel-Wert als Base-64-codierte Zeichenfolge, die dem folgenden Beispiel ähnelt:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Dieses Formular kann an eine Aktionsmethode gesendet werden, die ein Argument vom Typ Product hat, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

In der Action-Methode wird die Timestamp-Eigenschaft ordnungsgemäß aufgefüllt, da die gepostete Base-64-codierte Zeichenfolge in ein Bytearray konvertiert wird.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  Modelmetadata-und ModelMetadataProvider-Klassen

Die ModelMetadataProvider-Klasse stellt eine Abstraktion zum Abrufen von Metadaten für das Modell in einer Ansicht bereit. MVC 2 enthält einen Standardanbieter, der die Metadaten verfügbar macht, die von den Attributen im System. ComponentModel. DataAnnotations-Namespace verfügbar gemacht werden. Metadatenanbieter, die Metadaten aus anderen Daten speichern bereitstellen, z. b. Datenbanken oder XML-Dateien, können erstellt werden.

Die viewdatadictionary-Klasse macht ein modelmetadata-Objekt verfügbar, das die Metadaten enthält, die von der ModelMetadataProvider-Klasse aus dem Modell extrahiert werden. Dadurch können die auf Vorlagen basierenden Hilfsprogramme diese Metadaten nutzen und ihre Ausgabe entsprechend anpassen.

Weitere Informationen finden Sie in der Dokumentation für die [modelmetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) -und [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) -Klassen.

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  Unterstützung für DataAnnotations-Attribute

ASP.NET MVC 2 unterstützt die Verwendung der Validierungs Attribute "RangeAttribute", "Requirements dattribute", "StringLengthAttribute" und "regexattribute" (definiert im System. ComponentModel. DataAnnotations-Namespace), wenn eine Bindung an ein Modell erfolgt, um die Eingabevalidierung bereitzustellen.

Weitere Informationen finden Sie unter Gewusst wie: Überprüfen von [Modelldaten mithilfe von DataAnnotations-Attributen](https://go.microsoft.com/fwlink/?LinkId=159063) auf der MSDN-Website. Ein Beispiel Projekt, das die Verwendung dieser Attribute veranschaulicht, finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  Modell Validierungs Steuerelement-Anbieter

Die Anbieter Klasse Modell Validierung stellt eine Abstraktion dar, die Validierungs Logik für das Modell bereitstellt. ASP.NET MVC enthält einen Standardanbieter auf der Grundlage von Validierungs Attributen, die im System. ComponentModel. DataAnnotations-Namespace enthalten sind. Sie können auch eigene Validierungs Anbieter erstellen, die benutzerdefinierte Validierungsregeln und benutzerdefinierte Zuordnungen von Validierungsregeln für das Modell definieren. Weitere Informationen finden Sie in der Dokumentation zur [modelvalidatorprovider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) -Klasse.

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  Client seitige Validierung

Die Model-Validator Provider-Klasse macht Validierungs Metadaten für den Browser in Form von JSON-serialisierten Daten verfügbar, die von einer Client seitigen Validierungs Bibliothek genutzt werden können. ASP.NET MVC 2 enthält eine clientvalidierungs Bibliothek und einen Adapter, der die zuvor notierten Attribute der DataAnnotations-Namespace Validierung unterstützt. Die Anbieter Klasse ermöglicht es Ihnen auch, andere Client Validierungs Bibliotheken zu verwenden, indem Sie einen Adapter schreiben, der die JSON-Daten verarbeitet und die Alternative Bibliothek aufruft.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  Neue Code Ausschnitte für Visual Studio 2010

Eine Reihe von HTML-Code Ausschnitten für ASP.NET MVC 2 wird mit Visual Studio 2010 installiert. Klicken Sie im Menü Extras auf Code Ausschnitt-Manager, um eine Liste dieser Ausschnitte anzuzeigen. Wählen Sie für die Sprache die Option HTML aus, und wählen Sie unter Speicherort die Option ASP.NET MVC 2 aus. Weitere Informationen zur Verwendung von Code Ausschnitten finden Sie in der Visual Studio-Dokumentation.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  Neuer Requirements httpsattribute-Aktions Filter

ASP.NET MVC 2 enthält eine neue Klasse "Requirements httpsattribute", die auf Aktionsmethoden und Controller angewendet werden kann. Standardmäßig leitet der Filter eine nicht-SSL (http)-Anforderung an die SSL-aktivierte (HTTPS)-Entsprechung um.

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  Überschreiben des HTTP-Methoden Verbs

Wenn Sie eine Website mit dem Rest-Architekturstil erstellen, werden HTTP-Verben verwendet, um zu bestimmen, welche Aktion für eine Ressource ausgeführt werden soll. Rest erfordert, dass Anwendungen den vollständigen Bereich der allgemeinen HTTP-Verben unterstützen, einschließlich get, Put, Post und DELETE.

ASP.NET MVC 2 enthält neue Attribute, die Sie auf Aktionsmethoden und die Feature Compact-Syntax anwenden können. Diese Attribute ermöglichen es ASP.NET MVC, eine Aktionsmethode basierend auf dem HTTP-Verb auszuwählen. Im folgenden Beispiel ruft eine Post-Anforderung die erste Aktionsmethode auf, und eine PUT-Anforderung Ruft die zweite Aktionsmethode auf.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

In früheren Versionen von ASP.NET MVC erforderte diese Aktionsmethode eine ausführlichere Syntax, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Da Browser nur die HTTP-Verben GET und Post unterstützen, ist es nicht möglich, eine Aktion an eine Aktion zu senden, die ein anderes Verb erfordert. Folglich ist es nicht möglich, alle Rest-Anforderungen nativ zu unterstützen.

Zur Unterstützung von Rest-Anforderungen bei Post-Vorgängen führt ASP.NET MVC 2 jedoch eine neue httpmethodoverride-HTML-Hilfsmethode ein. Diese Methode rendert ein verborgenes Eingabe Element, das bewirkt, dass das Formular jede HTTP-Methode effektiv emuliert. Beispielsweise können Sie mit der HTML-Hilfsmethode httpmethodoverride festlegen, dass eine Formular Übermittlung eine Put-oder DELETE-Anforderung ist. Das Verhalten von httpmethodoverride wirkt sich auf die folgenden Attribute aus:

- Httppostatutribute
- Httpputattribute
- Httpgetattribute
- Httpdeleteattribute
- Akzeptverbsattribute

Das verborgene Eingabe Element hat den Namen X-http-Method-override, und sein Wert ist auf das zu emulierende http-Verb festgelegt. Der Überschreibungs Wert kann auch in einem HTTP-Header oder in einem Abfrage Zeichen folgen Wert als Name/Wert-Paar angegeben werden.

Die außer Kraft Setzung kann nur verwendet werden, wenn die tatsächliche Anforderung eine Post-Anforderung ist. Der Überschreibungs Wert wird bei Anforderungen ignoriert, die ein anderes HTTP-Verb verwenden.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  Neue hiddeninputattribute-Klasse für auf Vorlagen basierende Hilfsprogramme

Sie können das neue hiddeninputattribute-Attribut auf eine Modell Eigenschaft anwenden, um anzugeben, ob ein verborgenes Eingabe Element gerendert werden soll, wenn das Modell in einer Editor Vorlage angezeigt wird. (Das-Attribut legt einen impliziten UIHint-Wert von hiddeninput fest). Mithilfe der displayvalue-Eigenschaft des Attributs können Sie angeben, ob der Wert im Editor-und Anzeigemodus angezeigt wird. Wenn displayvalue auf false festgelegt ist, wird nichts angezeigt, nicht sogar das HTML-Markup, das normalerweise ein Feld umgibt. Der Standardwert für "displayvalue" ist "true".

Sie können das hiddeninputattribute-Attribut in den folgenden Szenarien verwenden:

- Wenn eine Ansicht Benutzern das Bearbeiten der ID eines Objekts ermöglicht und es notwendig ist, den Wert anzuzeigen und ein verborgenes Eingabe Element bereitzustellen, das die alte ID enthält, sodass es an den Controller zurückgegeben werden kann.
- Wenn eine Ansicht Benutzern ermöglicht, eine binäre Eigenschaft zu bearbeiten, die niemals angezeigt werden soll, z. b. eine Zeitstempel-Eigenschaft. In diesem Fall werden der Wert und das umgebende HTML-Markup (z. b. Bezeichnung und Wert) nicht angezeigt.

Im folgenden Beispiel wird gezeigt, wie die hiddeninputattribute-Klasse verwendet wird.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Wenn das-Attribut auf true festgelegt ist (oder kein-Parameter angegeben ist), geschieht Folgendes:

- In Anzeige Vorlagen wird eine Bezeichnung gerendert, und der Wert wird dem Benutzer angezeigt.
- In Editor-Vorlagen wird eine Bezeichnung gerendert, und der Wert wird in einem verborgenen Eingabe Element gerendert.

Wenn das-Attribut auf false festgelegt ist, geschieht Folgendes:

- In Anzeige Vorlagen wird für dieses Feld nichts gerendert.
- In Editor-Vorlagen wird keine Bezeichnung gerendert, und der Wert wird in einem verborgenen Eingabe Element gerendert.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  Die HTML. ValidationSummary-Hilfsmethode kann Fehler auf Modell Ebene anzeigen.

Anstatt immer alle Validierungs Fehler anzuzeigen, verfügt die HTML. ValidationSummary-Hilfsmethode über eine neue Option, mit der nur Fehler auf Modell Ebene angezeigt werden. Dies ermöglicht das Anzeigen von Fehlern auf Modell Ebene in der Validierungs Zusammenfassung und feldspezifischen Fehlern, die neben den einzelnen Feldern angezeigt werden.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  T4-Vorlagen in Visual Studio generieren Code, der spezifisch für die Ziel Version des .NET Framework

Eine neue Eigenschaft ist für T4-Dateien über den ASP.NET MVC T4-Host verfügbar, der die Version der .NET Framework angibt, die von der Anwendung verwendet wird. Dies ermöglicht T4-Vorlagen das Generieren von Code und Markup, das für eine Version der .NET Framework spezifisch ist. In Visual Studio 2008 lautet der Wert immer .NET 3,5. In Visual Studio 2010 ist der Wert entweder .NET 3,5 oder .NET 4.

## <a name="api-improvements"></a><a id="_TOC4"></a>  API-Verbesserungen

In diesem Abschnitt werden die Änderungen an vorhandenen ASP.NET MVC-Typen und-Membern beschrieben.

- Es wurde eine geschützte virtuelle Methode "kreateaktioninvoker" in der Controller Klasse hinzugefügt. Diese Methode wird von der Eigenschaft "aktionsinvoker" des Controllers aufgerufen und ermöglicht eine verzögerte Instanziierung des invokers, wenn bereits kein aufrufende Instanz festgelegt ist.
- Es wurde eine geschützte Virtual-Methode in der Klasse "Autorität Attribute" hinzugefügt. Dadurch können Filter, die von "Autorität Attribute" abgeleitet sind, das Verhalten steuern, wenn die Autorisierung fehlschlägt.
- Eine Add (String key, Object value)-Methode wurde in der valueproviderdictionary-Klasse hinzugefügt. Dies ermöglicht es Ihnen, die Wörterbuch-initialisierersyntax für valueproviderdictionary zu verwenden, wie im folgenden Beispiel gezeigt:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- Eine get \_ Object-Methode wurde in der sys. MVC. ajaxcontext-Klasse hinzugefügt. Dabei handelt es sich um eine JavaScript-Methode, die der Methode "Get Data" ähnelt \_ , aber wenn der Inhaltstyp der Antwort "application/json" ist, \_ gibt Get Object das JSON-Objekt zurück.
- In der AuthorizationContext-Klasse wurde eine Aktions Deskriptor-Eigenschaft hinzugefügt.
- Ein urlparameter. Optionales Token, das verwendet werden kann, um Probleme beim Binden an ein Modell zu umgehen, das eine ID-Eigenschaft enthält, wenn die Eigenschaft in einem Formular Beitrag fehlt. Ausführlichere Informationen finden Sie im Eintrag [ASP.NET MVC 2 optionale URL Parameters](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) on Phil Haack es Blog.

## <a name="breaking-changes"></a><a id="_TOC5"></a>  Wichtige Änderungen

Die folgenden Änderungen können Fehler in vorhandenen ASP.NET MVC 1,0-Anwendungen verursachen.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>Änderung des Verhaltens der Eigenschaften Validierung für Klassen, die IDataErrorInfo implementieren

Bei Modell Objekten, die IDataErrorInfo zum Durchführen der Validierung verwenden, wird jede Eigenschaft überprüft, unabhängig davon, ob ein neuer Wert festgelegt wurde. In ASP.NET MVC 1,0 wurden nur Eigenschaften überprüft, für die neue Werte festgelegt wurden. In ASP.NET MVC 2 wird die Error-Eigenschaft von IDataErrorInfo nur aufgerufen, wenn alle Eigenschaften Validierungs Steuerelemente erfolgreich waren.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>Das Skript für die IIS-Skript Zuordnung ist im Installationsprogramm nicht mehr verfügbar.

Das Skript für die Skript Zuordnung von IIS ist ein Befehlszeilen Skript, das zum Konfigurieren von Skript Maps für IIS 6 und für IIS 7 im klassischen Modus verwendet wird. Das Skript für die Skript Zuordnung ist nicht erforderlich, wenn Sie die Visual Studio Development Server verwenden, oder wenn Sie IIS 7 im integrierten Modus verwenden. Die Skripts sind als separater, nicht unterstützter Download für den [ASP.net webstack](https://github.com/aspnet/AspNetWebStack)verfügbar.

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>Die HTML. Ersatz-Hilfsmethode in MVC Futures ist nicht mehr verfügbar.

Aufgrund von Änderungen im Renderingverhalten von MVC-Ansichts Modulen funktioniert die HTML. Ersatz-Hilfsmethode nicht und wurde entfernt.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>Die IValueProvider-Schnittstelle ersetzt alle Verwendungen von IDictionary.

Jedes Eigenschafts-oder Methoden Argument, das IDictionary in MVC 1,0 akzeptiert hat, akzeptiert jetzt IValueProvider. Diese Änderung betrifft nur Anwendungen, die benutzerdefinierte Wert Anbieter oder benutzerdefinierte Modell Binder enthalten. Zu den Eigenschaften und Methoden, die von dieser Änderung betroffen sind, zählen beispielsweise folgende:

- Die valueprovider-Eigenschaft der controllerbase-Klasse und der modelbindingcontext-Klasse.
- Die tryupdatemodel-Methoden der Controller Klasse.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Neue CSS-Klassen wurden in der Datei "Site. CSS" hinzugefügt.

Die Datei "Site. CSS" in den ASP.NET-MVC-Projektvorlagen wurde aktualisiert, um neue Stile zu enthalten, die von der Überprüfungs Funktionalität und von den auf Vorlagen basierenden Hilfsprogramme verwendet werden.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Hilfsprogramme geben nun ein mvchtmlstring-Objekt zurück.

Um die neue Syntax für HTML-Codierungs Ausdrücke in ASP.NET 4 nutzen zu können, ist der Rückgabetyp für HTML-Hilfsprogramme nun mvchtmlstring anstelle einer Zeichenfolge. Wenn Sie ASP.NET MVC 2 und die neuen Hilfsprogramme auf ASP.NET 3,5 verwenden, können Sie die HTML-Codierungs Syntax nicht nutzen. die neue Syntax ist nur verfügbar, wenn Sie ASP.NET MVC 2 auf ASP.NET 4 ausführen.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>Jsonresult antwortet jetzt nur auf HTTP POST-Anforderungen.

Um JSON-Hijacking-Angriffe zu mindern, die das Potenzial der Offenlegung von Informationen haben, antwortet die jsonresult-Klasse standardmäßig nur auf HTTP POST-Anforderungen. AJAX-Get-Aufrufe von Aktionsmethoden, die ein jsonresult-Objekt zurückgeben, sollten stattdessen für die Verwendung von Post geändert werden. Falls erforderlich, können Sie dieses Verhalten überschreiben, indem Sie die neue jsonrequestbehavior-Eigenschaft von jsonresult festlegen. Weitere Informationen zur potenziellen Ausnutzung finden Sie im Blogbeitrag [JSON Hijacking](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) im Blog von Phil Haack.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>Model-und modeltype-Eigenschaften Setter in modelbindingcontext sind veraltet.

Der modelbindingcontext-Klasse wurde eine neue festleg Bare modelmetadata-Eigenschaft hinzugefügt. Die neue Eigenschaft kapselt die Modell-und modeltype-Eigenschaften. Obwohl die Model-und modeltype-Eigenschaften veraltet sind, funktionieren die Eigenschaften Getter weiterhin, um die Abwärtskompatibilität zu Gewähr zeichnen. Sie delegieren an die modelmetadata-Eigenschaft, um den Wert abzurufen.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Änderungen an der defaultcontrollerfactory-Klasse unterbrechen benutzerdefinierte controllerfactorys, die davon abgeleitet sind

Die defaultcontrollerfactory-Klasse wurde durch Entfernen der RequestContext-Eigenschaft korrigiert. Anstelle dieser Eigenschaft wird die Anforderungs Kontext Instanz an die geschützten virtuellen Methoden GetControllerInstance und getcontrollertype übergeben. Diese Änderung betrifft benutzerdefinierte controllerfactorys, die von defaultcontrollerfactory abgeleitet werden.

Benutzerdefinierte controllerfactorys werden häufig verwendet, um Abhängigkeitsinjektion für ASP.NET MVC-Anwendungen bereitzustellen Um die benutzerdefinierten controllerfactorys für die Unterstützung von ASP.NET MVC 2 zu aktualisieren, ändern Sie die Methoden Signatur oder die Signaturen so, dass Sie mit den neuen Signaturen identisch ist, und verwenden Sie den Anforderungs Kontext Parameter

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Area" ist ein reservierter Routen Wert Schlüssel

Die Zeichenfolge "Area" in den Routen Werten hat nun eine besondere Bedeutung in ASP.NET MVC, genauso wie "controller" und "action". Wenn HTML-Hilfsprogramme mit einem Routen Wert Wörterbuch bereitgestellt werden, das "Area" enthält, wird "Area" in der Abfrage Zeichenfolge nicht mehr in der Abfrage Zeichenfolge angefügt.

Wenn Sie die Bereichs Funktion verwenden, stellen Sie sicher, dass Sie {Area} nicht als Teil Ihrer Routen-URL verwenden.

## <a name="disclaimer"></a><a id="_TOC6"></a>  ERS

Dies ist ein vorläufiges Dokument, das vor der kommerziellen Veröffentlichung der beschriebenen Software ggf. erheblich geändert wird.

Die in diesem Dokument enthaltenen Informationen stellen die Sicht der Microsoft Corporation der hier diskutierten Themen zum Zeitpunkt der Veröffentlichung dar. Da Microsoft auf wechselnde Marktbedingungen reagieren muss, sollten sie nicht als Verpflichtung seitens Microsoft interpretiert werden, und Microsoft kann die Genauigkeit der dargelegten Informationen nach dem Zeitpunkt der Veröffentlichung nicht garantieren.

Dieses Whitepaper dient ausschließlich Informationszwecken. MICROSOFT ÜBERNIMMT KEINE AUSDRÜCKLICHE, STILLSCHWEIGENDE ODER AUS GESETZ ERWACHSENDE GARANTIE IN BEZUG AUF DIE INFORMATIONEN IN DIESEM DOKUMENT.

Die Benutzer/innen sind verpflichtet, sich an alle anwendbaren Urheberrechtsgesetze zu halten. Unabhängig von der Anwendbarkeit der entsprechenden Urheberrechtsgesetze darf kein Teil dieses Dokuments ohne ausdrückliche schriftliche Erlaubnis der Microsoft Corporation für irgendwelche Zwecke vervielfältigt oder in einem Datenempfangssystem gespeichert oder darin eingelesen werden, unabhängig davon, auf welche Art und Weise oder mit welchen Mitteln (elektronisch, mechanisch, durch Fotokopieren, Aufzeichnen usw.) dies geschieht.

Es ist möglich, dass Microsoft Rechte an Patenten bzw. an angemeldeten Patenten, an Marken, Urheberrechten oder sonstigem geistigen Eigentum besitzt, die sich auf den fachlichen Inhalt dieses Dokuments beziehen. Die Bereitstellung dieses Dokuments gewährt Ihnen jedoch keinerlei Lizenzrechte an diesen Patenten, Marken, Urheberrechten oder anderem geistigen Eigentum, es sei denn, dies wurde ausdrücklich durch einen schriftlichen Lizenzvertrag mit der Microsoft Corporation vereinbart.

Sofern nicht anders angegeben, sind die in den Beispielen aufgeführten Unternehmen, Organisationen, Produkte, Domänen Namen, e-Mail-Adressen, Logos, Personen, Orte und Ereignisse frei erfunden, und keine Zuordnung zu echten Unternehmen, Organisationen, Produkten, Domänen Namen, e-Mail-Adressen, Logos, Personen, Orten oder Ereignissen ist beabsichtigt oder sollte abgeleitet werden.

© 2010 Microsoft Corporation. Alle Rechte vorbehalten.

Microsoft und Windows sind eingetragene Marken oder Marken der Microsoft Corporation in den USA und/oder anderen Ländern.

Die in diesem Dokument erwähnten Namen von Unternehmen und Produkten können Marken der jeweiligen Eigentümer sein.
