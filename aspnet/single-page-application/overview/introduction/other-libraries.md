---
uid: single-page-application/overview/introduction/other-libraries
title: Andere Bibliotheken als Knockout | Microsoft-Dokumentation
author: madskristensen
description: Andere Bibliotheken als Knockout
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 5503a00df707ee79282a32c77ed2287e93cf8f48
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425469"
---
<a name="know-a-library-other-than-knockout"></a>Andere Bibliotheken als Knockout
====================
durch [Mads Kristensen](https://github.com/madskristensen)

Die [Single-Page-Anwendung (SPA) Vorlage](knockoutjs-template.md) eignet sich hervorragend für das Schreiben von Single-Page-Anwendungen. Die Vorlage verwendet [KnockoutJS](http://knockoutjs.com/) Anwendungsdaten an DOM-Elemente binden.

Knockout ist jedoch nicht die einzige JavaScript-Bibliothek zum Erstellen von rich-Client-Anwendungen. Andere Bibliotheken zu ähnliche Problemen auf unterschiedliche Weise lösen. Möglicherweise bevorzugen Sie eine einer Bibliothek über ein anderes, daher haben wir einige von Communitymitgliedern erstellte Vorlagen zum Download zur Verfügung haben. Jede dieser Vorlagen verwendet eine andere Mischung von Client-JavaScript-Bibliotheken.

Um eine Community erstellte Vorlage installieren zu können, finden Sie auf eines der Vorlage Seiten unten, und klicken Sie auf die Schaltfläche "herunterladen". Die Vorlagen werden als VSIX-Dateien bereitgestellt.

## <a name="backbonejs"></a>BackboneJS

[Backbone.js-SPA-Vorlage](../templates/backbonejs-template.md). Diese Vorlage enthält einen anfänglichen Gerüst für die Entwicklung einer [Backbone.js](http://backbonejs.org/) -Anwendung in ASP.NET MVC. Standardmäßig wird die grundlegende Anmeldefunktionalität ermöglichen, einschließlich Registrierung, Anmeldung, kennwortzurücksetzung durch Benutzer und Bestätigung durch den Benutzer mit basic-e-Mail-Vorlagen.

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa) ist eine open-Source-Bibliothek für die Verwaltung umfangreicher Daten in einem JavaScript-Client. Breeze verarbeitet Abfragen, Zwischenspeicherung, änderungsnachverfolgung, Validierung und mehr. Zwei Vorlagen enthalten, zum Kinderspiel wird:

- Die [Breeze/Knockout](../templates/breezeknockout-template.md) Vorlage erweitert die Knockout-SPA-Vorlage, die zeigt, wie einfach Sie eine Single-Page-Anwendung mit Breeze für die datenverwaltung und KnockoutJS für die Datenbindung erstellen können.
- Die [Breeze/Angular](../templates/breezeangular-template.md) Vorlage erweitert auch die Knockout-SPA-Vorlage mit Breeze, jedoch mit der [AngularJS](http://angularjs.org) -Bibliothek für die Datenbindung, Abhängigkeitsinjektion und Bildschirm-Verwaltung.

Darüber hinaus die [Hot Towel-SPA-Vorlage](../templates/hottowel-template.md) BreezeJS verwendet.

## <a name="emberjs"></a>EmberJS

[Ember.js-SPA-Vorlage](../templates/emberjs-template.md). Diese Vorlage verwendet [Ember](http://emberjs.com/), eine leistungsstarke MVC-JavaScript-Bibliothek, die eine Vielzahl von Herausforderungen für das Erstellen von rich Client-Anwendungen gelöst.

Die Ember-SPA-Vorlage ist eine erneute Implementierung die Knockout-SPA-Vorlage, die mithilfe der ember.js und Handlebars-Vorlagen.

## <a name="hot-towel"></a>Hot Towel

[Hot Towel-SPA-Vorlage](../templates/hottowel-template.md). Mit dieser Vorlage wird in mehreren JavaScript-Bibliotheken, einschließlich von Breeze und Knockout, RequireJS Twitter Bootstrap.

Im Vergleich mit den anderen Vorlagen, die hier aufgeführten bietet die Hot Towel-Vorlage eine vollständige Anwendung, die von der Sie Ihre eigenen erstellen können. Es gibt weitere Konzepte, die Sie berücksichtigen, aber sobald sie verstanden haben, mit dieser Vorlage einfach möglicherweise was Sie suchen. Wenn Sie möchten, Erstellen einer SPA, jedoch können nicht entscheiden, wo Sie beginnen, sollten Hot Towel und in Sekunden Sie eine SPA und alle Tools müssen, müssen Sie darauf erstellen.

## <a name="feature-table"></a>Feature-Tabelle

Hier sind die Funktionen, die durch jede SPA-Vorlage bereitgestellt wurde:


|                        | ASP.NET SPA | Backbone | Breeze/Angular | Breeze/KO |  Ember   | Hot Towel |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      Beispiel "ToDo"       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     Bare-Vorlage      |             | &#10003; |                |           |          | &#10003;  |
| Navigation und Verlauf |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        Bibliotheken       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;Backbone     |             | &#10003; |                |           |          |           |
|         Breeze         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        Durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |

