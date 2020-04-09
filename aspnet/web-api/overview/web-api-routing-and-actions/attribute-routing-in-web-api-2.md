---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Attributrouting in ASP.NET Web-API 2 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675387"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Attributrouting in ASP.NET Web-API 2

von [Mike Wasson](https://github.com/MikeWasson)

*Routing* ist die Art und Weise, wie die Web-API einen URI mit einer Aktion abgleicht. Web API 2 unterstützt einen neuen Routingtyp, das *attributrouting*. Wie der Name schon sagt, verwendet attributrouting Attribute, um Routen zu definieren. Das Attributrouting gibt Ihnen mehr Kontrolle über die URIs in Ihrer Web-API. Sie können z. B. problemlos URIs erstellen, die Ressourcenhierarchien beschreiben.

Der frühere Routingstil, das als konventionsbasiertes Routing bezeichnet wird, wird weiterhin vollständig unterstützt. Tatsächlich können Sie beide Techniken im selben Projekt kombinieren.

In diesem Thema wird gezeigt, wie Attributrouting aktiviert wird, und es werden die verschiedenen Optionen für das Attributrouting beschrieben. Ein End-to-End-Tutorial, das Attributrouting verwendet, finden Sie unter [Erstellen einer REST-API mit Attributrouting in Web-API 2](create-a-rest-api-with-attribute-routing.md).

## <a name="prerequisites"></a>Voraussetzungen

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community-, Professional- oder Enterprise-Edition

Alternativ können Sie NuGet Package Manager verwenden, um die erforderlichen Pakete zu installieren. Wählen Sie im Menü **Extras** in Visual Studio **NuGet Package Manager**aus , und wählen Sie dann **Package Manager Console**aus. Geben Sie im Fenster Package Manager Console den folgenden Befehl ein:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Warum Attributrouting?

Die erste Version der Web-API verwendet *konventionsbasiertes* Routing. In diesem Routingtyp definieren Sie eine oder mehrere Routenvorlagen, bei denen es sich im Grunde um parametrisierte Zeichenfolgen handelt. Wenn das Framework eine Anforderung empfängt, stimmt es mit dem URI mit der Routenvorlage überein. Weitere Informationen zum konventionsbasierten Routing finden Sie unter [Routing in ASP.NET Web-API](routing-in-aspnet-web-api.md).

Ein Vorteil des konventionsbasierten Routings besteht darin, dass Vorlagen an einem einzigen Ort definiert werden und die Routingregeln konsistent auf alle Controller angewendet werden. Leider macht es das konventionsbasierte Routing schwierig, bestimmte URI-Muster zu unterstützen, die in RESTful-APIs üblich sind. Ressourcen enthalten z. B. häufig untergeordnete Ressourcen: Kunden haben Aufträge, Filme haben Schauspieler, Bücher haben Autoren usw. Es ist natürlich, URIs zu erstellen, die diese Beziehungen widerspiegeln:

`/customers/1/orders`

Dieser URI-Typ ist mit konventionsbasiertem Routing schwer zu erstellen. Obwohl dies möglich ist, werden die Ergebnisse nicht gut skaliert, wenn Sie über viele Controller oder Ressourcentypen verfügen.

Beim Attributrouting ist es trivial, eine Route für diesen URI zu definieren. Sie fügen der Controlleraktion einfach ein Attribut hinzu:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Hier sind einige andere Muster, die Attributrouting macht einfach.

**API-Versionsverwaltung**

In diesem Beispiel würde "/api/v1/products" an einen anderen Controller als "/api/v2/products" weitergeleitet.

`/api/v1/products`
`/api/v2/products`

**Überladene URI-Segmente**

In diesem Beispiel ist "1" eine Bestellnummer, aber "ausstehend" wird einer Auflistung zugeordnet.

`/orders/1`
`/orders/pending`

**Mehrere Parametertypen**

In diesem Beispiel ist "1" eine Bestellnummer, aber "2013/06/16" gibt ein Datum an.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Aktivieren des Attributroutings

Um Attributrouting zu aktivieren, rufen Sie **MapHttpAttributeRoutes** während der Konfiguration auf. Diese Erweiterungsmethode ist in der **System.Web.Http.HttpConfigurationExtensions-Klasse** definiert.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Attributrouting kann mit [konventionsbasiertem](routing-in-aspnet-web-api.md) Routing kombiniert werden. Um konventionsbasierte Routen zu definieren, rufen Sie die **MapHttpRoute-Methode** auf.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Weitere Informationen zum Konfigurieren der Web-API finden Sie unter [Konfigurieren ASP.NET Web-API 2](../advanced/configuring-aspnet-web-api.md).

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Hinweis: Migrieren von Web-API 1

Vor Web-API 2 generierten die Web-API-Projektvorlagen Code wie folgt:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Wenn das Attributrouting aktiviert ist, löst dieser Code eine Ausnahme aus. Wenn Sie ein vorhandenes Web-API-Projekt aktualisieren, um Attributrouting zu verwenden, stellen Sie sicher, dass Dieser Konfigurationscode wie folgt aktualisiert wird:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Weitere Informationen finden Sie unter [Konfigurieren der Web-API mit ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Hinzufügen von Routenattributen

Hier ist ein Beispiel für eine Route, die mit einem Attribut definiert wurde:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

Die &quot;Zeichenfolge customers/'customerId'/orders&quot; ist die URI-Vorlage für die Route. Die Web-API versucht, den Anforderungs-URI mit der Vorlage abzugleichen. In diesem Beispiel sind "customers" und "orders" Literalsegmente, und "-customerId" ist ein variabler Parameter. Die folgenden URIs würden mit dieser Vorlage übereinstimmen:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Sie können die Übereinstimmung einschränken, indem Sie [Einschränkungen](#constraints)verwenden, die weiter unten in diesem Thema beschrieben werden.

Beachten Sie, dass &quot;&quot; der Parameter "customerId" in der Routenvorlage mit dem Namen des *customerId-Parameters* in der Methode übereinstimmt. Wenn die Web-API die Controlleraktion aufruft, versucht sie, die Routenparameter zu binden. Wenn der URI beispielsweise `http://example.com/customers/1/orders`lautet, versucht die Web-API, den Wert "1" an den *customerId-Parameter* in der Aktion zu binden.

Eine URI-Vorlage kann mehrere Parameter enthalten:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Alle Controllermethoden, die nicht über ein Routenattribut verfügen, verwenden konventionsbasiertes Routing. Auf diese Weise können Sie beide Routingtypen im gleichen Projekt kombinieren.

## <a name="http-methods"></a>HTTP-Methoden

Web-API wählt auch Aktionen basierend auf der HTTP-Methode der Anforderung (GET, POST, etc.). Standardmäßig sucht die Web-API nach einer Übereinstimmung ohne Groß-/Kleinschreibung mit dem Start des Controllermethodennamens. Beispielsweise entspricht eine Controllermethode mit dem Namen `PutCustomers` einer HTTP PUT-Anforderung.

Sie können diese Konvention überschreiben, indem Sie die Methode mit den folgenden Attributen dekorieren:

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptionen]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

Im folgenden Beispiel wird die CreateBook-Methode HTTP-POST-Anforderungen zugeordnet.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Verwenden Sie für alle anderen HTTP-Methoden, einschließlich nicht standardmäßiger Methoden, das **AcceptVerbs-Attribut,** das eine Liste von HTTP-Methoden enthält.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Routenpräfixe

Häufig beginnen die Routen in einem Controller mit demselben Präfix. Beispiel:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

Sie können ein gemeinsames Präfix für einen gesamten Controller festlegen, indem Sie das Attribut **[RoutePrefix]** verwenden:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Verwenden Sie eine Tilde für das Methodenattribut, um das Routenpräfix zu überschreiben:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Das Routenpräfix kann Parameter enthalten:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Routeneinschränkungen

Mit Routeneinschränkungen können Sie einschränken, wie die Parameter in der Routenvorlage abgeglichen werden. Die allgemeine &quot;Syntax lautet "Parameter:Constraint"&quot;. Beispiel:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Hier wird die erste Route nur &quot;&quot; ausgewählt, wenn das ID-Segment des URI eine ganze Zahl ist. Andernfalls wird die zweite Route gewählt.

In der folgenden Tabelle sind die unterstützten Einschränkungen aufgeführt.

| Einschränkung | BESCHREIBUNG | Beispiel |
| --- | --- | --- |
| alpha | Entspricht groß- oder kleinbuchstaben lateinischen Alphabetzeichen (a-z, A-Z) | X:alpha |
| bool | Entspricht einem booleschen Wert. | X:bool |
| datetime | Entspricht einem **DateTime-Wert.** | X:datetime |
| Decimal | Entspricht einem Dezimalwert. | X:dezimal |
| double | Entspricht einem 64-Bit-Gleitkommawert. | X:double |
| float | Entspricht einem 32-Bit-Gleitkommawert. | X:float |
| guid | Entspricht einem GUID-Wert. | X:guid |
| INT | Entspricht einem 32-Bit-Ganzzahlwert. | X:int |
| length | Entspricht einer Zeichenfolge mit der angegebenen Länge oder innerhalb eines angegebenen Längenbereichs. | X:Länge(6) X:Länge(1,20)" |
| long | Entspricht einem 64-Bit-Ganzzahlwert. | X:lang |
| max | Entspricht einer ganzzahligen Datei mit einem maximalwert. | X:max(10)" |
| Maxlength | Entspricht einer Zeichenfolge mit einer maximalen Länge. | X:maxlength(10) |
| Min | Entspricht einer ganzzahligen Datei mit einem Mindestwert. | X:min(10) |
| Minlength | Entspricht einer Zeichenfolge mit einer Mindestlänge. | x:minlength(10) |
| range | Entspricht einer ganzzahligen Datei innerhalb eines Wertebereichs. | X:range(10,50)" |
| regex | Entspricht einem regulären Ausdruck. | X:regex(-d{3}--d{3}--d-D-)){4} |

Beachten Sie, dass einige der &quot;Einschränkungen, z. B. min&quot;, Argumente in Klammern verwenden. Sie können mehrere Abhängigkeiten auf einen Parameter anwenden, der durch einen Doppelpunkt getrennt ist.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Benutzerdefinierte Routeneinschränkungen

Sie können benutzerdefinierte Routeneinschränkungen erstellen, indem Sie die **IHttpRouteConstraint-Schnittstelle** implementieren. Die folgende Einschränkung beschränkt z. B. einen Parameter auf einen Ganzzahlwert ungleich Null.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Der folgende Code zeigt, wie die Einschränkung registriert wird:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Jetzt können Sie die Einschränkung in Ihren Routen anwenden:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Sie können auch die gesamte **DefaultInlineConstraintResolver-Klasse** ersetzen, indem Sie die **IInlineConstraintResolver-Schnittstelle** implementieren. Dadurch werden alle integrierten Einschränkungen ersetzt, es sei denn, Ihre Implementierung von **IInlineConstraintResolver** fügt sie ausdrücklich hinzu.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>Optionale URI-Parameter und Standardwerte

Sie können einen URI-Parameter optional machen, indem Sie dem Routenparameter ein Fragezeichen hinzufügen. Wenn ein Routenparameter optional ist, müssen Sie einen Standardwert für den Methodenparameter definieren.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

Geben `/api/books/locale/1033` Sie `/api/books/locale` in diesem Beispiel dieselbe Ressource zurück.

Alternativ können Sie einen Standardwert in der Routenvorlage wie folgt angeben:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

Dies ist fast das gleiche wie im vorherigen Beispiel, aber es gibt einen leichten Unterschied im Verhalten, wenn der Standardwert angewendet wird.

- Im ersten Beispiel wird der Standardwert 1033 direkt dem Methodenparameter zugewiesen, sodass der Parameter genau diesen Wert hat.
- Im zweiten Beispiel ("-lcid:int=1033") wird der Standardwert "1033" durch den Modellbindungsprozess durchlaufen. Der Standardmodellbinder konvertiert "1033" in den numerischen Wert 1033. Sie können jedoch einen benutzerdefinierten Modellbinder anschließen, was etwas anderes tun kann.

(In den meisten Fällen sind die beiden Formulare gleichwertig, es sei denn, Sie haben benutzerdefinierte Modellbindemittel in der Pipeline.)

<a id="route-names"></a>
## <a name="route-names"></a>Routennamen

In der Web-API hat jede Route einen Namen. Routennamen sind nützlich zum Generieren von Verknüpfungen, sodass Sie einen Link in eine HTTP-Antwort einschließen können.

Um den Routennamen anzugeben, legen Sie die **Name-Eigenschaft** für das Attribut fest. Das folgende Beispiel zeigt, wie der Routenname festgelegt wird und wie der Routenname beim Generieren einer Verknüpfung verwendet wird.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Routenreihenfolge

Wenn das Framework versucht, einen URI mit einer Route abzugleichen, werden die Routen in einer bestimmten Reihenfolge ausgewertet. Um den Auftrag anzugeben, legen Sie die **Order-Eigenschaft** für das route-Attribut fest. Niedrigere Werte werden zuerst ausgewertet. Der Standardauftragswert ist Null.

Hier ist, wie die Gesamtbestellung bestimmt wird:

1. Vergleichen Sie die **Order-Eigenschaft** des route-Attributs.
2. Sehen Sie sich jedes URI-Segment in der Routenvorlage an. Ordnen Sie für jedes Segment wie folgt an:

    1. Literale Segmente.
    2. Routenparameter mit Einschränkungen.
    3. Routenparameter ohne Einschränkungen.
    4. Platzhalterparametersegmente mit Einschränkungen.
    5. Platzhalterparametersegmente ohne Einschränkungen.
3. Im Falle eines Unentschiedens werden Routen durch einen Ordinalzeichenfolgenvergleich ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) der Routenvorlage angeordnet.

Beispiel: Angenommen, Sie definieren den folgenden Controller:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Diese Routen werden wie folgt sortiert.

1. Bestellungen/Details
2. Bestellungen/ . . . . . . . . . . . . . . .
3. Bestellungen/-kundenname
4. Bestellungen/Datum\*
5. Aufträge/Ausstehende

Beachten Sie, dass "Details" ein Literalsegment ist und vor dem "id" angezeigt wird, aber "ausstehend" als letzter angezeigt wird, da die **Order-Eigenschaft** 1 ist. (In diesem Beispiel wird davon ausgegangen, dass keine Kunden mit den Namen "Details" oder "ausstehend" vorhanden sind. Versuchen Sie im Allgemeinen, mehrdeutige Routen zu vermeiden. In diesem Beispiel ist eine `GetByCustomer` bessere Routenvorlage für "customers/-customerName") .
