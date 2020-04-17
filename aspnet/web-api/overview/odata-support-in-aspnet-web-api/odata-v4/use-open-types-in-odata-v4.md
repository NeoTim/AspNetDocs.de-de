---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Öffnen von Typen in OData v4 mit ASP.NET Web-API | Microsoft Docs
author: rick-anderson
description: In OData v4 ist ein offener Typ ein strukturierter Typ, der dynamische Eigenschaften enthält, zusätzlich zu allen Eigenschaften, die in der Typdefinition deklariert werden. Öffnen...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543729"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Öffnen von Typen in OData v4 mit ASP.NET Web-API

von [Microsoft](https://github.com/microsoft)

> In OData v4 ist ein *offener Typ* ein strukturierter Typ, der dynamische Eigenschaften enthält, zusätzlich zu allen Eigenschaften, die in der Typdefinition deklariert werden. Mit offenen Typen können Sie Ihren Datenmodellen Flexibilität verleihen. In diesem Tutorial wird gezeigt, wie Sie offene Typen in ASP.NET Web-API OData verwenden.
> 
> In diesem Tutorial wird davon ausgegangen, dass Sie bereits wissen, wie Sie einen OData-Endpunkt in ASP.NET Web-API erstellen. Wenn dies nicht der Fall ist, lesen Sie zuerst [Einen OData v4-Endpunkt](create-an-odata-v4-endpoint.md) erstellen.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Im Tutorial verwendete Softwareversionen
> 
> 
> - Web-API OData 5.3
> - OData v4

Zunächst einige OData-Terminologie:

- Entitätstyp: Ein strukturierter Typ mit einem Schlüssel.
- Komplexer Typ: Ein strukturierter Typ ohne Schlüssel.
- Offener Typ: Ein Typ mit dynamischen Eigenschaften. Sowohl Entitätstypen als auch komplexe Typen können geöffnet sein.

Der Wert einer dynamischen Eigenschaft kann ein primitiver Typ, ein komplexer Typ oder ein Enumerationstyp sein. oder eine Sammlung dieser Typen. Weitere Informationen zu geöffneten Typen finden Sie in der [OData v4-Spezifikation](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Installieren der Web-OData-Bibliotheken

Verwenden Sie NuGet Package Manager, um die neuesten Web-API-OData-Bibliotheken zu installieren. Aus dem Fenster Paket-Manager-Konsole:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definieren der CLR-Typen

Definieren Sie zunächst die EDM-Modelle als CLR-Typen.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Wenn das Entity Data Model (EDM) erstellt wird,

- `Category`ist ein Enumerationstyp.
- `Address`ist ein komplexer Typ. (Es hat keinen Schlüssel, daher ist es kein Entitätstyp.)
- `Customer`ist ein Entitätstyp. (Es hat einen Schlüssel.)
- `Press`ist ein offener komplexer Typ.
- `Book`ist ein offener Entitätstyp.

Um einen offenen Typ zu erstellen, muss der `IDictionary<string, object>`CLR-Typ über eine Eigenschaft vom Typ verfügen, die die dynamischen Eigenschaften enthält.

## <a name="build-the-edm-model"></a>Erstellen des EDM-Modells

Wenn Sie **ODataConventionModelBuilder** zum Erstellen `Press` des `Book` EDM verwenden und automatisch als offene `IDictionary<string, object>` Typen hinzugefügt werden, basierend auf dem Vorhandensein einer Eigenschaft.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Sie können das EDM auch explizit mit **ODataModelBuilder**erstellen.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Hinzufügen eines OData Controllers

Fügen Sie als Nächstes einen OData-Controller hinzu. In diesem Tutorial verwenden wir einen vereinfachten Controller, der nur GET- und POST-Anforderungen unterstützt und eine In-Memory-Liste zum Speichern von Entitäten verwendet.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Beachten Sie, `Book` dass die erste Instanz keine dynamischen Eigenschaften aufweist. Die `Book` zweite Instanz verfügt über die folgenden dynamischen Eigenschaften:

- "Veröffentlicht": Primitiver Typ
- "Autoren": Sammlung primitiver Typen
- "Andere Kategorien": Auflistung von Enumerationstypen.

Außerdem verfügt `Press` die `Book` Eigenschaft dieser Instanz über die folgenden dynamischen Eigenschaften:

- "Blog": Primitiver Typ
- "Adresse": Komplexer Typ

## <a name="query-the-metadata"></a>Abfragen der Metadaten

Um das OData-Metadatendokument abzurufen, `~/$metadata`senden Sie eine GET-Anforderung an . Das Antwortgremium sollte wie folgt aussehen:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Aus dem Metadatendokument können Sie sehen, dass:

- Für `Book` die `Press` und-Typen ist `OpenType` der Wert des Attributs true. Die `Customer` `Address` und-Typen haben dieses Attribut nicht.
- Der `Book` Entitätstyp hat drei deklarierte Eigenschaften: ISBN, Title und Press. Die OData-Metadaten enthalten `Book.Properties` nicht die Eigenschaft aus der CLR-Klasse.
- Ebenso hat `Press` der komplexe Typ nur zwei deklarierte Eigenschaften: Name und Kategorie. Die Metadaten enthalten `Press.DynamicProperties` nicht die Eigenschaft aus der CLR-Klasse.

## <a name="query-an-entity"></a>Abfragen einer Entität

Um das Buch mit ISBN gleich "978-0-7356-7942-9" `~/Books('978-0-7356-7942-9')`zu erhalten, senden Sie eine GET-Anfrage an . Das Antwortgremium sollte wie folgt aussehen. (Eingerückt, um es lesbarer zu machen.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Beachten Sie, dass die dynamischen Eigenschaften inline mit den deklarierten Eigenschaften enthalten sind.

## <a name="post-an-entity"></a>POST einer Entität

Um eine Book-Entität hinzuzufügen, `~/Books`senden Sie eine POST-Anforderung an . Der Client kann dynamische Eigenschaften in der Anforderungsnutzlast festlegen.

Hier ist eine Beispielanforderung. Beachten Sie die Eigenschaften "Preis" und "Veröffentlicht".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Wenn Sie einen Haltepunkt in der Controllermethode festlegen, können Sie `Properties` sehen, dass die Web-API diese Eigenschaften dem Wörterbuch hinzugefügt hat.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Weitere Ressourcen

[OData Open Type-Beispiel](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
