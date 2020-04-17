---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Komplexe Typvererbung in OData v4 mit ASP.NET Web-API | Microsoft Docs
author: rick-anderson
description: Gemäß der OData v4-Spezifikation kann ein komplexer Typ von einem anderen komplexen Typ erben. (Ein komplexer Typ ist ein strukturierter Typ ohne Schlüssel.) Web-API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543599"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Komplexe Typvererbung in OData v4 mit ASP.NET Web-API

von [Microsoft](https://github.com/microsoft)

> Gemäß der OData [v4-Spezifikation](http://www.odata.org/documentation/odata-version-4-0/)kann ein komplexer Typ von einem anderen komplexen Typ erben. (Ein *komplexer* Typ ist ein strukturierter Typ ohne Schlüssel.) Web-API OData 5.3 unterstützt komplexe Typvererbung.
> 
> In diesem Thema wird gezeigt, wie ein Entitätsdatenmodell (Entity Data Model, EDM) mit komplexen Vererbungstypen erstellt wird. Den vollständigen Quellcode finden Sie unter [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Im Tutorial verwendete Softwareversionen
> 
> 
> - Web-API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>Modellhierarchie

Zur Veranschaulichung der komplexen Typvererbung verwenden wir die folgende Klassenhierarchie.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`ist ein abstrakter komplexer Typ. `Rectangle`, `Triangle`und `Circle` sind komplexe `Shape`Typen, `RoundRectangle` die von `Rectangle`abgeleitet sind und von abgeleitet werden. `Window`ist ein Entitätstyp `Shape` und enthält eine Instanz.

Hier sind die CLR-Klassen, die diese Typen definieren.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Erstellen des EDM-Modells

Zum Erstellen des EDM können Sie **ODataConventionModelBuilder**verwenden, das die Vererbungsbeziehungen aus den CLR-Typen ableitet.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Sie können das EDM auch explizit mit **ODataModelBuilder**erstellen. Dies erfordert mehr Code, gibt Ihnen aber mehr Kontrolle über das EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

In diesen beiden Beispielen wird dasselbe EDM-Schema erstellt.

## <a name="metadata-document"></a>Metadatendokument

Hier ist das OData-Metadatendokument, das die Vererbung komplexer Typen anzeigt.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

Aus dem Metadatendokument können Sie sehen, dass:

- Der `Shape` komplexe Typ ist abstrakt.
- Der `Rectangle` `Triangle`,- `Circle` und der komplexe `Shape`Typ haben den Basistyp .
- Der `RoundRectangle` Typ hat `Rectangle`den Basistyp .

## <a name="casting-complex-types"></a>Casting Complex-Typen

Das Casting für komplexe Typen wird jetzt unterstützt. Die folgende Abfrage gibt z. B. eine `Shape` in eine `Rectangle`aus.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Hier ist die Antwort Nutzlast:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
