---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Öffnen Sie die Typen in OData v4 mit ASP.NET Web-API | Microsoft-Dokumentation
author: microsoft
description: In OData v4 ist ein offener Typ eines strukturierten Typs, das dynamische Eigenschaften, zusätzlich zu den Eigenschaften enthält, die in der Definition eines Typs deklariert werden. Öffnen...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 69e2cc716a50c64ae5edf38a499abf4d80d75d3d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414958"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Öffnen Sie die Typen in OData v4 mit ASP.NET Web-API

by [Microsoft](https://github.com/microsoft)

> In OData v4 ein *offener Typ* ist ein strukturierter Typ, die dynamische Eigenschaften, zusätzlich zu den Eigenschaften enthält, die in der Definition eines Typs deklariert werden. Offene Typen können Sie die Flexibilität mit Ihren Datenmodellen hinzufügen. Dieses Tutorial zeigt, wie offene Typen in OData der ASP.NET Web-API verwendet wird.
> 
> In diesem Tutorial wird davon ausgegangen, dass Sie bereits wissen, wie zum Erstellen eines OData-Endpunkts in ASP.NET Web-API. Falls nicht, lesen Sie zunächst [erstellen ein OData v4-Endpunkts](create-an-odata-v4-endpoint.md) erste.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Softwareversionen, die in diesem Tutorial verwendet werden.
> 
> 
> - Web-API OData 5.3
> - OData v4


Zunächst einige Begriffe OData:

- Der Entitätstyp: Einen strukturierten Typ mit einem Schlüssel.
- Komplexer Typ: Einen strukturierten Typ ohne einen Schlüssel.
- Öffnen Sie die geben: Ein Typ mit dynamischen Eigenschaften. Sowohl Entitätstypen und komplexe Typen können geöffnet sein.

Der Wert einer dynamischen Eigenschaft kann es sich um einen primitiven Typ, komplexen Typ oder Enumerationstyp sein; oder eine Auflistung aller dieser Typen. Weitere Informationen zu offenen Typen, finden Sie unter den [OData v4-Spezifikation](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Installieren Sie die Web-OData-Bibliotheken

Verwenden der NuGet-Paketmanager, um die neuesten Web-API OData-Bibliotheken installieren. Aus dem Fenster Paket-Manager-Konsole:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definieren Sie die CLR-Typen

Zuerst definieren die EDM-Modelle als CLR-Typen.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Wenn der Entity Data Model (EDM) erstellt wird,

- `Category` ist ein Enumerationstyp.
- `Address` ist ein komplexer Typ. (sie einen Schlüssel muss nicht so, dass es sich nicht um ein Entitätstyp ist.)
- `Customer` ist ein Entitätstyp. (sie hat es sich um einen Schlüssel.)
- `Press` ist ein offener komplexen Typ.
- `Book` ist ein offener Entitätstyp an.

Um einen offenen Typ zu erstellen, müssen die CLR-Typ eine Eigenschaft des Typs `IDictionary<string, object>`, das die dynamischen Eigenschaften enthält.

## <a name="build-the-edm-model"></a>Das EDM-Modell erstellen

Bei Verwendung von **ODataConventionModelBuilder** EDM erstellen `Press` und `Book` werden automatisch hinzugefügt, als offene Typen, die basierend auf dem Vorhandensein einer `IDictionary<string, object>` Eigenschaft.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Sie können auch erstellen, das EDM explizit mit **ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Fügen Sie einen OData-Controller hinzu.

Als Nächstes fügen Sie einen OData-Controller hinzu. In diesem Tutorial verwenden wir einen vereinfachten Controller nur unterstützt zu erhalten und POST-Anforderungen, und verwendet eine in-Memory-Liste, um Entitäten zu speichern.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Beachten Sie, dass die erste `Book` Instanz hat keine dynamischen Eigenschaften. Die zweite `Book` Instanz hat die folgenden dynamischen Eigenschaften:

- "Published": Primitiver Typ
- "Autoren": Auflistung von primitiven Typen
- "OtherCategories": Die Auflistung von Enumerationstypen.

Darüber hinaus die `Press` -Eigenschaft dieses `Book` Instanz hat die folgenden dynamischen Eigenschaften:

- "Blog": Primitiver Typ
- "Address": Komplexer Typ

## <a name="query-the-metadata"></a>Abfragen der Metadaten

Um das Metadatendokument des OData zu erhalten, senden Sie eine GET-Anforderung an `~/$metadata`. Der Antworttext sollte etwa wie folgt aussehen:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

Aus dem Dokument sehen Sie, die Folgendes:

- Für die `Book` und `Press` Typen wird der Wert, der die `OpenType` -Attribut ist "true". Die `Customer` und `Address` Typen nicht über dieses Attribut verfügen.
- Die `Book` Entitätstyp verfügt über drei deklarierten Eigenschaften: ISBN, Titel, und drücken Sie. Die OData-Metadaten enthält keinen der `Book.Properties` Eigenschaft von der CLR-Klasse.
- Auf ähnliche Weise die `Press` komplexerer Typ verfügt über nur zwei deklarierten Eigenschaften: Der Name und Kategorie. Die Metadaten enthält keinen der `Press.DynamicProperties` Eigenschaft von der CLR-Klasse.

## <a name="query-an-entity"></a>Abfragen einer Entität

Um das Buch mit der ISBN-Nummer gleich "978-0-7356-7942-9" erhalten, senden Sie eine GET-Anforderung an `~/Books('978-0-7356-7942-9')`. Der Antworttext sollte etwa wie folgt aussehen. (Eingerückt, um sie besser lesbar zu machen.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Beachten Sie die dynamischen Eigenschaften sind die deklarierten Eigenschaften Inlineschemainformationen enthält.

## <a name="post-an-entity"></a>Stellen Sie eine Entität

Senden Sie eine POST-Anforderung zum Hinzufügen einer Entität Buch `~/Books`. Der Client kann dynamische Eigenschaften in der Anforderungsnutzlast festlegen.

Hier ist eine beispielanforderung ein. Beachten Sie die Eigenschaften "Price" und "Veröffentlicht".

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Wenn Sie einen Haltepunkt in der Controllermethode festlegen, Sie sehen, dass Web-API diese Eigenschaften auf der `Properties` Wörterbuch.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

[Beispiel für OData öffnen](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
