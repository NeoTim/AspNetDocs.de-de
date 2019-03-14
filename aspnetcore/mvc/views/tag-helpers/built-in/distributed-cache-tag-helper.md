---
title: Taghilfsprogramm für verteilten Cache in ASP.NET Core
author: pkellner
description: Erfahren Sie, wie das Taghilfsprogramm für verteilten Cache verwendet wird.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: a5b33451a763c297c6d7885855a321c43435abb4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043917"
---
# <a name="distributed-cache-tag-helper-in-aspnet-core"></a>Taghilfsprogramm für verteilten Cache in ASP.NET Core

Von [Peter Kellner](http://peterkellner.net) und [Luke Latham](https://github.com/guardrex)

Durch das Taghilfsprogramm für verteilten Cache kann die Leistung Ihrer ASP.NET Core-App erheblich verbessert werden, indem deren Inhalte in einer verteilten Cachequelle zwischengespeichert werden.

Eine Übersicht der Taghilfsprogramme finden Sie unter <xref:mvc/views/tag-helpers/intro>.

Das Taghilfsprogramm für verteilten Cache erbt von derselben Basisklasse wie das Cache-Taghilfsprogramm. Alle Attribute des [Cache-Taghilfsprogramms](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper) sind für das Taghilfsprogramm für verteilten Cache verfügbar.

Das Taghilfsprogramm für verteilten Cache verwendet die [Konstruktorinjektion](xref:fundamentals/dependency-injection#constructor-injection-behavior). Die Schnittstelle <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache> wird an den Konstruktor des Taghilfsprogramms für verteilten Cache übergeben. Wenn keine konkrete Implementierung von `IDistributedCache` in `Startup.ConfigureServices` (*Startup.cs*) erstellt wurde, verwendet das Taghilfsprogramm für verteilten Cache zum Speichern von zwischengespeicherten Daten denselben In-Memory-Anbieter wie das [Cache-Taghilfsprogramm](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).

## <a name="distributed-cache-tag-helper-attributes"></a>Attribute des Taghilfsprogramms für verteilten Cache

### <a name="attributes-shared-with-the-cache-tag-helper"></a>Attribute, die für das Cache-Taghilfsprogramm freigegeben sind:

* `enabled`
* `expires-on`
* `expires-after`
* `expires-sliding`
* `vary-by-header`
* `vary-by-query`
* `vary-by-route`
* `vary-by-cookie`
* `vary-by-user`
* `vary-by priority`

Das Taghilfsprogramm für verteilten Cache erbt von derselben Klasse wie das Cache-Taghilfsprogramm. Beschreibungen dieser Attribute finden Sie im [Cache-Taghilfsprogramm](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).

### <a name="name"></a>Name

| Attributtyp | Beispiel                               |
| -------------- | ------------------------------------- |
| Zeichenfolge         | `my-distributed-cache-unique-key-101` |

`name` ist erforderlich. Das `name`-Attribut wird als Schlüssel für die einzelnen gespeicherten Cacheinstanzen verwendet. Im Gegensatz zum Cache-Taghilfsprogramm, das jeder Instanz basierend auf dem Namen der Razor-Seite und dem Speicherort auf der Razor-Seite einen Cacheschlüssel zuweist, basieren die Schlüssel des Taghilfsprogramms für verteilten Cache nur auf dem Attribut `name`.

Beispiel:

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a>Implementierungen von IDistributedCache im Taghilfsprogramm für verteilten Cache

In ASP.NET Core gibt es zwei Implementierungen von <xref:Microsoft.Extensions.Caching.Distributed.IDistributedCache>. Eine basiert auf SQL Server, die andere auf Redis. Ausführliche Informationen zu diesen Implementierungen finden Sie unter <xref:performance/caching/distributed>. Für beide Implementierungen wird eine Instanz von `IDistributedCache` in `Startup` festgelegt.

Es gibt keine Tagattribute, die einer bestimmten Implementierung von `IDistributedCache` explizit zugeordnet sind.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
