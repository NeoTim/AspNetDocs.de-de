---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: Überprüfen mit einer Dienstschicht (c#) | Microsoft-Dokumentation
author: StephenWalther
description: Erfahren Sie, wie Sie eine Validierungslogik aus Ihre Controlleraktionen und in einer separaten Dienstschicht zu verschieben. In diesem Tutorial Stephen Walther wird erläutert, wie Sie...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 9b2a7e00b3c50a946ad0f2518880892f103a5c1b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387112"
---
# <a name="validating-with-a-service-layer-c"></a>Überprüfen mit einer Dienstschicht (C#)

durch [Stephen Walther](https://github.com/StephenWalther)

> Erfahren Sie, wie Sie eine Validierungslogik aus Ihre Controlleraktionen und in einer separaten Dienstschicht zu verschieben. In diesem Tutorial erläutert Stephen Walther an, wie Sie eine scharfe Trennung der Zuständigkeiten verwalten können, indem isoliert von Ihrer Dienstebene aus Ihrem Controller-Ebene.


Das Ziel dieses Lernprogramms ist eine Methode zum Ausführen der Validierung in ASP.NET MVC-Anwendungen beschrieben. In diesem Tutorial erfahren Sie, wie Sie eine Validierungslogik aus Ihren Controllern und in einer separaten Dienstschicht zu verschieben.

## <a name="separating-concerns"></a>Trennen von Concerns

Wenn Sie eine ASP.NET MVC-Anwendung erstellen, sollten Sie Ihre Datenbanklogik nicht in Ihre Controlleraktionen platzieren. Kombinieren Ihre Datenbank und Controller-Logik erschwert Ihre Anwendung im Laufe der Zeit beibehalten. Es wird empfohlen, dass Sie alle Ihre Datenbanklogik in einer separaten Repository-Ebene platzieren.

Liste 1 enthält beispielsweise ein einfaches Repository mit dem Namen der ProductRepository. Die produktrepository enthält alle Datenzugriffscode für die Anwendung. Die Liste enthält auch die IProductRepository-Schnittstelle, die das produktrepository implementiert.

**Listing 1 -- Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

Der Controller im Codebeispiel 2 verwendet die Repository-Ebene in der Index() und Create() Aktionen. Beachten Sie, dass dieser Controller keine Datenbanklogik nicht enthält. Erstellen eine Repository-Ebene können Sie eine saubere Trennung von Zuständigkeiten zu verwalten. Controller für die Anwendung datenflusskontrolllogik verantwortlich sind, und das Repository für die Logik für den Datenzugriff verantwortlich ist.

**Codebeispiel 2 - Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>Erstellen eine Dienstschicht

Also datenflusskontrolllogik Anwendung gehört, in einem Controller und Logik für den Datenzugriff in einem Repository gehört. In diesem Fall, in dem platziere Sie eine Validierungslogik? Eine Möglichkeit ist, platzieren Sie eine Validierungslogik in einem *Dienstschicht*.

Eine Dienstschicht ist eine zusätzliche Ebene in einer ASP.NET MVC-Anwendung, die Kommunikation zwischen einem Controller und einer Repositoryschicht vermittelt. Die Dienstschicht enthält Geschäftslogik. Insbesondere enthält sie Validierungslogik.

Die Product-Dienstebene in Programmausdruck 3 hat z. B. eine CreateProduct()-Methode. Die CreateProduct()-Methode ruft die ValidateProduct()-Methode, um ein neues Produkt zu überprüfen, bevor Sie das Produkt in der produktrepository übergeben.

**Codebeispiel 3 - Models\ProductService.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

Der Product-Controller wurde aktualisiert, in Listing 4 die Dienstschicht anstelle der Repositoryschicht verwenden. Die Controller-Schicht kommuniziert mit der Dienstebene. Die Dienstebene, die mit der Repositoryschicht kommuniziert werden. Jede Ebene hat eine separate Aufgabe.

**Programmausdruck 4 - Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

Beachten Sie, dass der Produktdienst in der Product-Controller-Konstruktor erstellt wurde. Wenn der Produktdienst erstellt wird, wird das Modellzustandswörterbuch an den Dienst übergeben. Der Produktdienst verwendet den Modellzustand Validierung Fehlermeldungen an den Controller zurückgesendet.

## <a name="decoupling-the-service-layer"></a>Entkopplung der Dienstebene

Es konnte nicht den Controller und die Dienstschichten in einer Hinsicht zu isolieren. Der Controller und die Dienstschichten kommunizieren über die Modellstatus. Anders gesagt: die Dienstschicht weist eine Abhängigkeit auf eine bestimmte Funktion von ASP.NET MVC-Framework.

Wir möchten die Dienstschicht aus unserem Controller-Ebene, die so weit wie möglich zu isolieren. Theoretisch sollten wir die Dienstschicht mit jeder Art von Anwendung nicht nur eine ASP.NET MVC-Anwendung verwenden können. Beispielsweise sollten wir in Zukunft zum Erstellen einer WPF-Front-End für unsere Anwendung. Es sollte eine Möglichkeit zum Entfernen der Abhängigkeit von ASP.NET MVC Modellstatus von unserem Dienstebene gefunden.

In Listing 5 ist wurde die Dienstschicht aktualisiert, damit er nicht mehr Modellzustand verwendet. Stattdessen wird jede Klasse, die die IValidationDictionary-Schnittstelle implementiert.

**Programmausdruck 5 - Models\ProductService.cs (entkoppelt)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

Die IValidationDictionary-Schnittstelle wird im Codebeispiel 6 definiert. Diese einfache Schnittstelle verfügt über eine einzelne Methode und eine einzelne Eigenschaft.

**Codebeispiel 6: Models\IValidationDictionary.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

Die Klasse im Codebeispiel 7, mit dem Namen der ModelStateWrapper-Klasse implementiert die IValidationDictionary-Schnittstelle. Sie können die ModelStateWrapper-Klasse instanziieren, indem Sie ein Modell State-Wörterbuch an den Konstruktor übergeben.

**Auflisten von 7 – Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

Schließlich verwendet der aktualisierte Controller im Codebeispiel 8 die ModelStateWrapper beim Erstellen der Dienstschicht in seinem Konstruktor.

**Auflisten von 8 – Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

Verwenden die IValidationDictionary können Schnittstelle und der ModelStateWrapper-Klasse wir unsere Dienstebene aus unserem Controller Ebene vollständig zu isolieren. Die Dienstschicht ist nicht mehr Modellstatus abhängig. Sie können jede Klasse übergeben, die um die Dienstebene der IValidationDictionary-Schnittstelle implementiert. Beispielsweise kann eine WPF-Anwendung die IValidationDictionary-Schnittstelle mit einer einfachen Auflistung-Klasse implementieren.

## <a name="summary"></a>Zusammenfassung

Das Ziel in diesem Tutorial war ein Ansatz für die Ausführung der Validierung in ASP.NET MVC-Anwendungen erläutert. In diesem Tutorial haben Sie gelernt, wie alle eine Validierungslogik aus Ihren Controllern und in einer separaten Dienstschicht verschieben. Außerdem haben Sie gelernt, Ihrer Dienstebene aus Ihrem Controller-Ebene zu isolieren, indem Sie eine Klasse ModelStateWrapper erstellen.

> [!div class="step-by-step"]
> [Zurück](validating-with-the-idataerrorinfo-interface-cs.md)
> [Weiter](validation-with-the-data-annotation-validators-cs.md)
