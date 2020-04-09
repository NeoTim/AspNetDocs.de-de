---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: JSON- und XML-Serialisierung in ASP.NET Web-API - ASP.NET 4.x
author: MikeWasson
description: Beschreibt die JSON- und XML-Verforerung in ASP.NET Web-API für ASP.NET 4.x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675832"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>JSON- und XML-Serialisierung in ASP.NET Web-API

von [Mike Wasson](https://github.com/MikeWasson)

In diesem Artikel werden die JSON- und XML-Formatters in ASP.NET Web-API beschrieben.

In ASP.NET Web-API ist ein *Medien-Typ-Formatter* ein Objekt, das:

- Lesen von CLR-Objekten aus einem HTTP-Nachrichtentext
- Schreiben von CLR-Objekten in einen HTTP-Nachrichtentext

Die Web-API stellt Medien-Typ-Formatters für JSON und XML bereit. Das Framework fügt diese Forern standardmäßig in die Pipeline ein. Clients können entweder JSON oder XML im Accept-Header der HTTP-Anforderung anfordern.

## <a name="contents"></a>Contents

- [JSON Media-Typ-Formatter](#json_media_type_formatter)

    - [Nur schreibgeschützte Eigenschaften](#json_readonly)
    - [Datumsangaben](#json_dates)
    - [Einzug](#json_indenting)
    - [Camel Casing](#json_camelcasing)
    - [Anonyme und schwach typisierte Objekte](#json_anon)
- [XML-Medientyp-Formatter](#xml_media_type_formatter)

    - [Nur schreibgeschützte Eigenschaften](#xml_readonly)
    - [Datumsangaben](#xml_dates)
    - [Einzug](#xml_indenting)
    - [Festlegen von XML-Serialisierungsdateien pro Typ](#xml_pertype)
- [Entfernen des JSON- oder XML-Forms](#removing_the_json_or_xml_formatter)
- [Umgang mit zirkulären Objektreferenzen](#handling_circular_object_references)
- [Testen der Objektserialisierung](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON Media-Typ-Formatter

Die JSON-Formatierung wird von der **JsonMediaTypeFormatter-Klasse** bereitgestellt. Standardmäßig verwendet **JsonMediaTypeFormatter** die [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) Bibliothek, um die Serialisierung durchzuführen. Json.NET ist ein Open-Source-Projekt eines Drittanbieters.

Wenn Sie möchten, können Sie die **JsonMediaTypeFormatter-Klasse** so konfigurieren, dass **dataContractJsonSerializer** anstelle Json.NET verwendet wird. Legen Sie dazu die **UseDataContractJsonSerializer-Eigenschaft** auf **true**fest:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON-Serialisierung

In diesem Abschnitt werden einige spezifische Verhaltensweisen des JSON-Verteilers mithilfe der [standardmäßigen Json.NET](https://github.com/JamesNK/Newtonsoft.Json) Serialisierung beschrieben. Dies ist nicht als umfassende Dokumentation der Json.NET Bibliothek gedacht; Weitere Informationen finden Sie in der [Json.NET Dokumentation](http://james.newtonking.com/projects/json/help/).

#### <a name="what-gets-serialized"></a>Was wird serialisiert?

Standardmäßig sind alle öffentlichen Eigenschaften und Felder in der serialisierten JSON enthalten. Um eine Eigenschaft oder ein Feld wegzulassen, dekorieren Sie sie mit dem **JsonIgnore-Attribut.**

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

Wenn Sie &quot;einen Opt-In-Ansatz&quot; bevorzugen, dekorieren Sie die Klasse mit dem **DataContract-Attribut.** Wenn dieses Attribut vorhanden ist, werden Member ignoriert, es sei denn, sie verfügen über den **DataMember**. Sie können **DataMember** auch verwenden, um private Member zu serialisieren.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Nur schreibgeschützte Eigenschaften

Schreibgeschützte Eigenschaften werden standardmäßig serialisiert.

<a id="json_dates"></a>
### <a name="dates"></a>Datumsangaben

Standardmäßig schreibt Json.NET Datumsangaben im [ISO 8601-Format.](http://www.w3.org/TR/NOTE-datetime) Datumsangaben in UTC (Coordinated Universal Time) werden mit einem "Z"-Suffix geschrieben. Zu den Datumsangaben in der Ortszeit gehört ein Zeitzonenversatz. Beispiel:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Standardmäßig Json.NET die Zeitzone beibehalten. Sie können dies überschreiben, indem Sie die DateTimeZoneHandling-Eigenschaft festlegen:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

Wenn Sie lieber [das Microsoft JSON-Datumsformat](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) anstelle von ISO 8601 verwenden möchten, legen Sie die **DateFormatHandling-Eigenschaft** für die Serialisierungseinstellungen fest:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Einzug

Um eingerücktes JSON zu schreiben, legen Sie die **Einstellung Formatierung** auf **Formatierung fest.Indented**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Camel Casing

Um JSON-Eigenschaftsnamen mit Kamelgehäuse zu schreiben, ohne das Datenmodell zu ändern, legen Sie den **CamelCasePropertyNamesContractResolver** für den Serialisierer fest:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Anonyme und schwach typisierte Objekte

Eine Aktionsmethode kann ein anonymes Objekt zurückgeben und an JSON serialisieren. Beispiel:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Der Antwortnachrichtentext enthält den folgenden JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Wenn Ihre Web-API lose strukturierte JSON-Objekte von Clients empfängt, können Sie den Anforderungstext in einen **Newtonsoft.Json.Linq.JObject-Typ** deserialisieren.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

In der Regel ist es jedoch besser, stark typisierte Datenobjekte zu verwenden. Dann müssen Sie die Daten nicht selbst analysieren, und Sie erhalten die Vorteile der Modellvalidierung.

Der XML-Serialisierungsprogramm unterstützt **JObject** keine anonymen Typen oder JObject-Instanzen. Wenn Sie diese Funktionen für Ihre JSON-Daten verwenden, sollten Sie den XML-Formatter aus der Pipeline entfernen, wie weiter unten in diesem Artikel beschrieben.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML-Medientyp-Formatter

Die XML-Formatierung wird von der **XmlMediaTypeFormatter-Klasse** bereitgestellt. Standardmäßig verwendet **XmlMediaTypeFormatter** die **DataContractSerializer-Klasse,** um die Serialisierung durchzuführen.

Wenn Sie möchten, können Sie **XmlMediaTypeFormatter** so konfigurieren, dass der **XmlSerializer** anstelle des **DataContractSerializer**verwendet wird. Legen Sie dazu die **UseXmlSerializer-Eigenschaft** auf **true**fest:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

Die **XmlSerializer-Klasse** unterstützt einen engeren Satz von Typen als **DataContractSerializer**, gibt jedoch mehr Kontrolle über die resultierende XML-Datei. Erwägen Sie die Verwendung von **XmlSerializer,** wenn Sie einem vorhandenen XML-Schema entsprechen müssen.

### <a name="xml-serialization"></a>XML-Serialisierung

In diesem Abschnitt werden einige spezifische Verhaltensweisen des XML-Umwerks mithilfe des Standardmäßigen **DataContractSerializer**beschrieben.

Standardmäßig verhält sich DataContractSerializer wie folgt:

- Alle öffentlichen Lese-/Schreibeigenschaften und Felder werden serialisiert. Um eine Eigenschaft oder ein Feld wegzulassen, dekorieren Sie sie mit dem **IgnoreDataMember-Attribut.**
- Private und geschützte Mitglieder werden nicht serialisiert.
- Schreibgeschützte Eigenschaften werden nicht serialisiert. (Der Inhalt einer schreibgeschützten Auflistungseigenschaft wird jedoch serialisiert.)
- Klassen- und Membernamen werden im XML genau so geschrieben, wie sie in der Klassendeklaration angezeigt werden.
- Es wird ein Standard-XML-Namespace verwendet.

Wenn Sie mehr Kontrolle über die Serialisierung benötigen, können Sie die Klasse mit dem **DataContract-Attribut** dekorieren. Wenn dieses Attribut vorhanden ist, wird die Klasse wie folgt serialisiert:

- &quot;Opt-in-Ansatz:&quot; Eigenschaften und Felder werden nicht standardmäßig serialisiert. Um eine Eigenschaft oder ein Feld zu serialisieren, dekorieren Sie sie mit dem **DataMember-Attribut.**
- Um ein privates oder geschütztes Element zu serialisieren, dekorieren Sie es mit dem **DataMember-Attribut.**
- Schreibgeschützte Eigenschaften werden nicht serialisiert.
- Um zu ändern, wie der Klassenname im XML angezeigt wird, legen Sie den *Parameter Name* im **DataContract-Attribut** fest.
- Um zu ändern, wie ein Membername im XML angezeigt wird, legen Sie den *Parameter Name* im **DataMember-Attribut** fest.
- Um den XML-Namespace zu ändern, legen Sie den *Namespace-Parameter* in der **DataContract-Klasse** fest.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Nur schreibgeschützte Eigenschaften

Schreibgeschützte Eigenschaften werden nicht serialisiert. Wenn eine schreibgeschützte Eigenschaft über ein privates Sicherungsfeld verfügt, können Sie das private Feld mit dem **DataMember-Attribut** markieren. Dieser Ansatz erfordert das **DataContract-Attribut** für die Klasse.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Datumsangaben

Die Daten werden im ISO 8601-Format geschrieben. Zum Beispiel, &quot;2012-05-23T20:21:37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Einzug

Um einzugsgeschützten XML zu schreiben, legen Sie die **Indent-Eigenschaft** auf **true**fest:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Festlegen von XML-Serialisierungsdateien pro Typ

Sie können verschiedene XML-Serialisierungsgeräte für verschiedene CLR-Typen festlegen. Sie verfügen beispielsweise über ein bestimmtes Datenobjekt, das **XmlSerializer** für die Abwärtskompatibilität benötigt. Sie können **XmlSerializer** für dieses Objekt verwenden und **DataContractSerializer** weiterhin für andere Typen verwenden.

Um einen XML-Serialisierungsmodul für einen bestimmten Typ festzulegen, rufen Sie **SetSerializer**auf.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Sie können einen **XmlSerializer** oder ein beliebiges Objekt angeben, das von **XmlObjectSerializer**ableitet.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>Entfernen des JSON- oder XML-Forms

Sie können den JSON-Formatter oder den XML-Formatter aus der Liste der Verteilstellen entfernen, wenn Sie sie nicht verwenden möchten. Die Hauptgründe dafür sind:

- So beschränken Sie Ihre Web-API-Antworten auf einen bestimmten Medientyp. Sie können z. B. entscheiden, nur JSON-Antworten zu unterstützen und den XML-Formatter zu entfernen.
- So ersetzen Sie den Standard-Formatter durch einen benutzerdefinierten Formatter. Sie können z. B. den JSON-Formatter durch eine eigene benutzerdefinierte Implementierung eines JSON-Forgottes ersetzen.

Der folgende Code zeigt, wie die Standard-Formatters entfernt werden. Rufen Sie dies über Ihre **\_Application Start-Methode** auf, die in Global.asax definiert ist.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Umgang mit zirkulären Objektreferenzen

Standardmäßig schreiben JSON- und XML-Formatters alle Objekte als Werte. Wenn zwei Eigenschaften auf dasselbe Objekt verweisen oder wenn dasselbe Objekt zweimal in einer Auflistung angezeigt wird, serialisiert der Formatter das Objekt zweimal. Dies ist ein besonderes Problem, wenn das Objektdiagramm Zyklen enthält, da der Serialisierer eine Ausnahme auslöst, wenn er eine Schleife im Diagramm erkennt.

Betrachten Sie die folgenden Objektmodelle und Controller.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Wenn Sie diese Aktion aufrufen, löst der Formatter eine Ausnahme aus, die in eine Antwort des Statuscodes 500 (Interner Serverfehler) an den Client übersetzt wird.

Um Objektverweise in JSON beizubehalten, fügen Sie der **Application Start-Methode\_** in der Datei Global.asax den folgenden Code hinzu:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Nun gibt die Controlleraktion JSON zurück, das wie folgt aussieht:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Beachten Sie, dass &quot;der&quot; Serialisierungsmodul beiden Objekten eine $id-Eigenschaft hinzufügt. Außerdem wird erkannt, dass die Employee.Department-Eigenschaft eine Schleife erstellt, sodass&quot;sie&quot;&quot;den&quot;Wert durch einen Objektverweis ersetzt: . $ref : 1 .

> [!NOTE]
> Objektverweise sind in JSON nicht Standard. Bevor Sie diese Funktion verwenden, sollten Sie prüfen, ob Ihre Clients in der Lage sein werden, die Ergebnisse zu analysieren. Es könnte besser sein, einfach Zyklen aus dem Diagramm zu entfernen. Beispielsweise wird in diesem Beispiel der Link von Employee back to Department nicht wirklich benötigt.

Um Objektverweise in XML beizubehalten, haben Sie zwei Möglichkeiten. Die einfachere Option `[DataContract(IsReference=true)]` besteht darin, Ihrer Modellklasse hinzuzufügen. Der *IsReference-Parameter* aktiviert Objektverweise. Denken Sie daran, dass **DataContract** Serialisierung Opt-In macht, so dass Sie auch **DataMember-Attribute** zu den Eigenschaften hinzufügen müssen:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Nun wird der Formatter XML ähnlich wie folgt produzieren:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Wenn Sie Attribute für Ihre Modellklasse vermeiden möchten, gibt es eine weitere Option: Erstellen Sie eine neue typspezifische **DataContractSerializer-Instanz,** und legen Sie *preserveObjectReferences* im Konstruktor **auf true** fest. Legen Sie diese Instanz dann als Serialisierungsmodul pro Typ auf dem XML-Medien-Typ-Formatter fest. Der folgende Code zeigt, wie Sie dies tun:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Testen der Objektserialisierung

Beim Entwerfen der Web-API ist es nützlich, zu testen, wie Ihre Datenobjekte serialisiert werden. Sie können dies tun, ohne einen Controller zu erstellen oder eine Controlleraktion aufzuberufen.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
