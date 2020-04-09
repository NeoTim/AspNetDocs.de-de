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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="eb1bb-103">JSON- und XML-Serialisierung in ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="eb1bb-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="eb1bb-104">von [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eb1bb-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="eb1bb-105">In diesem Artikel werden die JSON- und XML-Formatters in ASP.NET Web-API beschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="eb1bb-106">In ASP.NET Web-API ist ein *Medien-Typ-Formatter* ein Objekt, das:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="eb1bb-107">Lesen von CLR-Objekten aus einem HTTP-Nachrichtentext</span><span class="sxs-lookup"><span data-stu-id="eb1bb-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="eb1bb-108">Schreiben von CLR-Objekten in einen HTTP-Nachrichtentext</span><span class="sxs-lookup"><span data-stu-id="eb1bb-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="eb1bb-109">Die Web-API stellt Medien-Typ-Formatters für JSON und XML bereit.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="eb1bb-110">Das Framework fügt diese Forern standardmäßig in die Pipeline ein.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="eb1bb-111">Clients können entweder JSON oder XML im Accept-Header der HTTP-Anforderung anfordern.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="eb1bb-112">Contents</span><span class="sxs-lookup"><span data-stu-id="eb1bb-112">Contents</span></span>

- [<span data-ttu-id="eb1bb-113">JSON Media-Typ-Formatter</span><span class="sxs-lookup"><span data-stu-id="eb1bb-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="eb1bb-114">Nur schreibgeschützte Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eb1bb-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="eb1bb-115">Datumsangaben</span><span class="sxs-lookup"><span data-stu-id="eb1bb-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="eb1bb-116">Einzug</span><span class="sxs-lookup"><span data-stu-id="eb1bb-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="eb1bb-117">Camel Casing</span><span class="sxs-lookup"><span data-stu-id="eb1bb-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="eb1bb-118">Anonyme und schwach typisierte Objekte</span><span class="sxs-lookup"><span data-stu-id="eb1bb-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="eb1bb-119">XML-Medientyp-Formatter</span><span class="sxs-lookup"><span data-stu-id="eb1bb-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="eb1bb-120">Nur schreibgeschützte Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eb1bb-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="eb1bb-121">Datumsangaben</span><span class="sxs-lookup"><span data-stu-id="eb1bb-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="eb1bb-122">Einzug</span><span class="sxs-lookup"><span data-stu-id="eb1bb-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="eb1bb-123">Festlegen von XML-Serialisierungsdateien pro Typ</span><span class="sxs-lookup"><span data-stu-id="eb1bb-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="eb1bb-124">Entfernen des JSON- oder XML-Forms</span><span class="sxs-lookup"><span data-stu-id="eb1bb-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="eb1bb-125">Umgang mit zirkulären Objektreferenzen</span><span class="sxs-lookup"><span data-stu-id="eb1bb-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="eb1bb-126">Testen der Objektserialisierung</span><span class="sxs-lookup"><span data-stu-id="eb1bb-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="eb1bb-127">JSON Media-Typ-Formatter</span><span class="sxs-lookup"><span data-stu-id="eb1bb-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="eb1bb-128">Die JSON-Formatierung wird von der **JsonMediaTypeFormatter-Klasse** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="eb1bb-129">Standardmäßig verwendet **JsonMediaTypeFormatter** die [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) Bibliothek, um die Serialisierung durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="eb1bb-130">Json.NET ist ein Open-Source-Projekt eines Drittanbieters.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="eb1bb-131">Wenn Sie möchten, können Sie die **JsonMediaTypeFormatter-Klasse** so konfigurieren, dass **dataContractJsonSerializer** anstelle Json.NET verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="eb1bb-132">Legen Sie dazu die **UseDataContractJsonSerializer-Eigenschaft** auf **true**fest:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="eb1bb-133">JSON-Serialisierung</span><span class="sxs-lookup"><span data-stu-id="eb1bb-133">JSON Serialization</span></span>

<span data-ttu-id="eb1bb-134">In diesem Abschnitt werden einige spezifische Verhaltensweisen des JSON-Verteilers mithilfe der [standardmäßigen Json.NET](https://github.com/JamesNK/Newtonsoft.Json) Serialisierung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="eb1bb-135">Dies ist nicht als umfassende Dokumentation der Json.NET Bibliothek gedacht; Weitere Informationen finden Sie in der [Json.NET Dokumentation](http://james.newtonking.com/projects/json/help/).</span><span class="sxs-lookup"><span data-stu-id="eb1bb-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="eb1bb-136">Was wird serialisiert?</span><span class="sxs-lookup"><span data-stu-id="eb1bb-136">What Gets Serialized?</span></span>

<span data-ttu-id="eb1bb-137">Standardmäßig sind alle öffentlichen Eigenschaften und Felder in der serialisierten JSON enthalten.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="eb1bb-138">Um eine Eigenschaft oder ein Feld wegzulassen, dekorieren Sie sie mit dem **JsonIgnore-Attribut.**</span><span class="sxs-lookup"><span data-stu-id="eb1bb-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="eb1bb-139">Wenn Sie &quot;einen Opt-In-Ansatz&quot; bevorzugen, dekorieren Sie die Klasse mit dem **DataContract-Attribut.**</span><span class="sxs-lookup"><span data-stu-id="eb1bb-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="eb1bb-140">Wenn dieses Attribut vorhanden ist, werden Member ignoriert, es sei denn, sie verfügen über den **DataMember**.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="eb1bb-141">Sie können **DataMember** auch verwenden, um private Member zu serialisieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="eb1bb-142">Nur schreibgeschützte Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eb1bb-142">Read-Only Properties</span></span>

<span data-ttu-id="eb1bb-143">Schreibgeschützte Eigenschaften werden standardmäßig serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="eb1bb-144">Datumsangaben</span><span class="sxs-lookup"><span data-stu-id="eb1bb-144">Dates</span></span>

<span data-ttu-id="eb1bb-145">Standardmäßig schreibt Json.NET Datumsangaben im [ISO 8601-Format.](http://www.w3.org/TR/NOTE-datetime)</span><span class="sxs-lookup"><span data-stu-id="eb1bb-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="eb1bb-146">Datumsangaben in UTC (Coordinated Universal Time) werden mit einem "Z"-Suffix geschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="eb1bb-147">Zu den Datumsangaben in der Ortszeit gehört ein Zeitzonenversatz.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="eb1bb-148">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="eb1bb-149">Standardmäßig Json.NET die Zeitzone beibehalten.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="eb1bb-150">Sie können dies überschreiben, indem Sie die DateTimeZoneHandling-Eigenschaft festlegen:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="eb1bb-151">Wenn Sie lieber [das Microsoft JSON-Datumsformat](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) anstelle von ISO 8601 verwenden möchten, legen Sie die **DateFormatHandling-Eigenschaft** für die Serialisierungseinstellungen fest:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="eb1bb-152">Einzug</span><span class="sxs-lookup"><span data-stu-id="eb1bb-152">Indenting</span></span>

<span data-ttu-id="eb1bb-153">Um eingerücktes JSON zu schreiben, legen Sie die **Einstellung Formatierung** auf **Formatierung fest.Indented**:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="eb1bb-154">Camel Casing</span><span class="sxs-lookup"><span data-stu-id="eb1bb-154">Camel Casing</span></span>

<span data-ttu-id="eb1bb-155">Um JSON-Eigenschaftsnamen mit Kamelgehäuse zu schreiben, ohne das Datenmodell zu ändern, legen Sie den **CamelCasePropertyNamesContractResolver** für den Serialisierer fest:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="eb1bb-156">Anonyme und schwach typisierte Objekte</span><span class="sxs-lookup"><span data-stu-id="eb1bb-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="eb1bb-157">Eine Aktionsmethode kann ein anonymes Objekt zurückgeben und an JSON serialisieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="eb1bb-158">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="eb1bb-159">Der Antwortnachrichtentext enthält den folgenden JSON:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="eb1bb-160">Wenn Ihre Web-API lose strukturierte JSON-Objekte von Clients empfängt, können Sie den Anforderungstext in einen **Newtonsoft.Json.Linq.JObject-Typ** deserialisieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="eb1bb-161">In der Regel ist es jedoch besser, stark typisierte Datenobjekte zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="eb1bb-162">Dann müssen Sie die Daten nicht selbst analysieren, und Sie erhalten die Vorteile der Modellvalidierung.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="eb1bb-163">Der XML-Serialisierungsprogramm unterstützt **JObject** keine anonymen Typen oder JObject-Instanzen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="eb1bb-164">Wenn Sie diese Funktionen für Ihre JSON-Daten verwenden, sollten Sie den XML-Formatter aus der Pipeline entfernen, wie weiter unten in diesem Artikel beschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="eb1bb-165">XML-Medientyp-Formatter</span><span class="sxs-lookup"><span data-stu-id="eb1bb-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="eb1bb-166">Die XML-Formatierung wird von der **XmlMediaTypeFormatter-Klasse** bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="eb1bb-167">Standardmäßig verwendet **XmlMediaTypeFormatter** die **DataContractSerializer-Klasse,** um die Serialisierung durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="eb1bb-168">Wenn Sie möchten, können Sie **XmlMediaTypeFormatter** so konfigurieren, dass der **XmlSerializer** anstelle des **DataContractSerializer**verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="eb1bb-169">Legen Sie dazu die **UseXmlSerializer-Eigenschaft** auf **true**fest:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="eb1bb-170">Die **XmlSerializer-Klasse** unterstützt einen engeren Satz von Typen als **DataContractSerializer**, gibt jedoch mehr Kontrolle über die resultierende XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="eb1bb-171">Erwägen Sie die Verwendung von **XmlSerializer,** wenn Sie einem vorhandenen XML-Schema entsprechen müssen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="eb1bb-172">XML-Serialisierung</span><span class="sxs-lookup"><span data-stu-id="eb1bb-172">XML Serialization</span></span>

<span data-ttu-id="eb1bb-173">In diesem Abschnitt werden einige spezifische Verhaltensweisen des XML-Umwerks mithilfe des Standardmäßigen **DataContractSerializer**beschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="eb1bb-174">Standardmäßig verhält sich DataContractSerializer wie folgt:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="eb1bb-175">Alle öffentlichen Lese-/Schreibeigenschaften und Felder werden serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="eb1bb-176">Um eine Eigenschaft oder ein Feld wegzulassen, dekorieren Sie sie mit dem **IgnoreDataMember-Attribut.**</span><span class="sxs-lookup"><span data-stu-id="eb1bb-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="eb1bb-177">Private und geschützte Mitglieder werden nicht serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="eb1bb-178">Schreibgeschützte Eigenschaften werden nicht serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="eb1bb-179">(Der Inhalt einer schreibgeschützten Auflistungseigenschaft wird jedoch serialisiert.)</span><span class="sxs-lookup"><span data-stu-id="eb1bb-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="eb1bb-180">Klassen- und Membernamen werden im XML genau so geschrieben, wie sie in der Klassendeklaration angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="eb1bb-181">Es wird ein Standard-XML-Namespace verwendet.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-181">A default XML namespace is used.</span></span>

<span data-ttu-id="eb1bb-182">Wenn Sie mehr Kontrolle über die Serialisierung benötigen, können Sie die Klasse mit dem **DataContract-Attribut** dekorieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="eb1bb-183">Wenn dieses Attribut vorhanden ist, wird die Klasse wie folgt serialisiert:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="eb1bb-184">&quot;Opt-in-Ansatz:&quot; Eigenschaften und Felder werden nicht standardmäßig serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="eb1bb-185">Um eine Eigenschaft oder ein Feld zu serialisieren, dekorieren Sie sie mit dem **DataMember-Attribut.**</span><span class="sxs-lookup"><span data-stu-id="eb1bb-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="eb1bb-186">Um ein privates oder geschütztes Element zu serialisieren, dekorieren Sie es mit dem **DataMember-Attribut.**</span><span class="sxs-lookup"><span data-stu-id="eb1bb-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="eb1bb-187">Schreibgeschützte Eigenschaften werden nicht serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="eb1bb-188">Um zu ändern, wie der Klassenname im XML angezeigt wird, legen Sie den *Parameter Name* im **DataContract-Attribut** fest.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="eb1bb-189">Um zu ändern, wie ein Membername im XML angezeigt wird, legen Sie den *Parameter Name* im **DataMember-Attribut** fest.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="eb1bb-190">Um den XML-Namespace zu ändern, legen Sie den *Namespace-Parameter* in der **DataContract-Klasse** fest.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="eb1bb-191">Nur schreibgeschützte Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="eb1bb-191">Read-Only Properties</span></span>

<span data-ttu-id="eb1bb-192">Schreibgeschützte Eigenschaften werden nicht serialisiert.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="eb1bb-193">Wenn eine schreibgeschützte Eigenschaft über ein privates Sicherungsfeld verfügt, können Sie das private Feld mit dem **DataMember-Attribut** markieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="eb1bb-194">Dieser Ansatz erfordert das **DataContract-Attribut** für die Klasse.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="eb1bb-195">Datumsangaben</span><span class="sxs-lookup"><span data-stu-id="eb1bb-195">Dates</span></span>

<span data-ttu-id="eb1bb-196">Die Daten werden im ISO 8601-Format geschrieben.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="eb1bb-197">Zum Beispiel, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="eb1bb-198">Einzug</span><span class="sxs-lookup"><span data-stu-id="eb1bb-198">Indenting</span></span>

<span data-ttu-id="eb1bb-199">Um einzugsgeschützten XML zu schreiben, legen Sie die **Indent-Eigenschaft** auf **true**fest:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="eb1bb-200">Festlegen von XML-Serialisierungsdateien pro Typ</span><span class="sxs-lookup"><span data-stu-id="eb1bb-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="eb1bb-201">Sie können verschiedene XML-Serialisierungsgeräte für verschiedene CLR-Typen festlegen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="eb1bb-202">Sie verfügen beispielsweise über ein bestimmtes Datenobjekt, das **XmlSerializer** für die Abwärtskompatibilität benötigt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="eb1bb-203">Sie können **XmlSerializer** für dieses Objekt verwenden und **DataContractSerializer** weiterhin für andere Typen verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="eb1bb-204">Um einen XML-Serialisierungsmodul für einen bestimmten Typ festzulegen, rufen Sie **SetSerializer**auf.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="eb1bb-205">Sie können einen **XmlSerializer** oder ein beliebiges Objekt angeben, das von **XmlObjectSerializer**ableitet.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="eb1bb-206">Entfernen des JSON- oder XML-Forms</span><span class="sxs-lookup"><span data-stu-id="eb1bb-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="eb1bb-207">Sie können den JSON-Formatter oder den XML-Formatter aus der Liste der Verteilstellen entfernen, wenn Sie sie nicht verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="eb1bb-208">Die Hauptgründe dafür sind:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="eb1bb-209">So beschränken Sie Ihre Web-API-Antworten auf einen bestimmten Medientyp.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="eb1bb-210">Sie können z. B. entscheiden, nur JSON-Antworten zu unterstützen und den XML-Formatter zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="eb1bb-211">So ersetzen Sie den Standard-Formatter durch einen benutzerdefinierten Formatter.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="eb1bb-212">Sie können z. B. den JSON-Formatter durch eine eigene benutzerdefinierte Implementierung eines JSON-Forgottes ersetzen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="eb1bb-213">Der folgende Code zeigt, wie die Standard-Formatters entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="eb1bb-214">Rufen Sie dies über Ihre **\_Application Start-Methode** auf, die in Global.asax definiert ist.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="eb1bb-215">Umgang mit zirkulären Objektreferenzen</span><span class="sxs-lookup"><span data-stu-id="eb1bb-215">Handling Circular Object References</span></span>

<span data-ttu-id="eb1bb-216">Standardmäßig schreiben JSON- und XML-Formatters alle Objekte als Werte.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="eb1bb-217">Wenn zwei Eigenschaften auf dasselbe Objekt verweisen oder wenn dasselbe Objekt zweimal in einer Auflistung angezeigt wird, serialisiert der Formatter das Objekt zweimal.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="eb1bb-218">Dies ist ein besonderes Problem, wenn das Objektdiagramm Zyklen enthält, da der Serialisierer eine Ausnahme auslöst, wenn er eine Schleife im Diagramm erkennt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="eb1bb-219">Betrachten Sie die folgenden Objektmodelle und Controller.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="eb1bb-220">Wenn Sie diese Aktion aufrufen, löst der Formatter eine Ausnahme aus, die in eine Antwort des Statuscodes 500 (Interner Serverfehler) an den Client übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="eb1bb-221">Um Objektverweise in JSON beizubehalten, fügen Sie der **Application Start-Methode\_** in der Datei Global.asax den folgenden Code hinzu:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="eb1bb-222">Nun gibt die Controlleraktion JSON zurück, das wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="eb1bb-223">Beachten Sie, dass &quot;der&quot; Serialisierungsmodul beiden Objekten eine $id-Eigenschaft hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="eb1bb-224">Außerdem wird erkannt, dass die Employee.Department-Eigenschaft eine Schleife erstellt, sodass&quot;sie&quot;&quot;den&quot;Wert durch einen Objektverweis ersetzt: . $ref : 1 .</span><span class="sxs-lookup"><span data-stu-id="eb1bb-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="eb1bb-225">Objektverweise sind in JSON nicht Standard.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="eb1bb-226">Bevor Sie diese Funktion verwenden, sollten Sie prüfen, ob Ihre Clients in der Lage sein werden, die Ergebnisse zu analysieren.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="eb1bb-227">Es könnte besser sein, einfach Zyklen aus dem Diagramm zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="eb1bb-228">Beispielsweise wird in diesem Beispiel der Link von Employee back to Department nicht wirklich benötigt.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="eb1bb-229">Um Objektverweise in XML beizubehalten, haben Sie zwei Möglichkeiten.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="eb1bb-230">Die einfachere Option `[DataContract(IsReference=true)]` besteht darin, Ihrer Modellklasse hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="eb1bb-231">Der *IsReference-Parameter* aktiviert Objektverweise.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="eb1bb-232">Denken Sie daran, dass **DataContract** Serialisierung Opt-In macht, so dass Sie auch **DataMember-Attribute** zu den Eigenschaften hinzufügen müssen:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="eb1bb-233">Nun wird der Formatter XML ähnlich wie folgt produzieren:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="eb1bb-234">Wenn Sie Attribute für Ihre Modellklasse vermeiden möchten, gibt es eine weitere Option: Erstellen Sie eine neue typspezifische **DataContractSerializer-Instanz,** und legen Sie *preserveObjectReferences* im Konstruktor **auf true** fest.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="eb1bb-235">Legen Sie diese Instanz dann als Serialisierungsmodul pro Typ auf dem XML-Medien-Typ-Formatter fest.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="eb1bb-236">Der folgende Code zeigt, wie Sie dies tun:</span><span class="sxs-lookup"><span data-stu-id="eb1bb-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="eb1bb-237">Testen der Objektserialisierung</span><span class="sxs-lookup"><span data-stu-id="eb1bb-237">Testing Object Serialization</span></span>

<span data-ttu-id="eb1bb-238">Beim Entwerfen der Web-API ist es nützlich, zu testen, wie Ihre Datenobjekte serialisiert werden.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="eb1bb-239">Sie können dies tun, ohne einen Controller zu erstellen oder eine Controlleraktion aufzuberufen.</span><span class="sxs-lookup"><span data-stu-id="eb1bb-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
