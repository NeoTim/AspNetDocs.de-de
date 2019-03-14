---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038867"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a>Hinzufügen eines Modells zu einer ASP.NET Core MVC-App

Von [Rick Anderson](https://twitter.com/RickAndMSFT) und [Tom Dykstra](https://github.com/tdykstra)

In diesem Abschnitt fügen Sie einer Datenbank einige Klassen für die Verwaltung von Filmen hinzu. Diese Klassen bilden den „**M**odell“-Teil der **M**VC-App.

Verwenden Sie diese Klassen mit [Entity Framework Core](/ef/core) (EF Core), um mit einer Datenbank zu arbeiten. EF Core ist ein ORM-Framework (Objektrelationales Mapping, ORM), das den Datenzugriffscode vereinfacht, den Sie schreiben müssen. [EF Core unterstützt viele Datenbank-Engines](/ef/core/providers/).

Die Modellklassen, die Sie erstellen, werden als POCO-Klassen (von „plain-old CLR objects“) bezeichnet, da sie nicht über eine Abhängigkeit von EF Core verfügen. Sie definieren lediglich die Eigenschaften der Daten, die in der Datenbank gespeichert werden.

In diesem Tutorial schreiben Sie zuerst die Modellklassen. Anschließend erstellt EF Core die Datenbank. Eine alternative Methode, die hier nicht aufgeführt ist, besteht darin, Modellklassen aus einer vorhandenen Datenbank zu generieren. Weitere Informationen zu diesem Verfahren finden Sie unter [ASP.NET Core: Vorhandene Datenbank](/ef/core/get-started/aspnetcore/existing-db).

## <a name="add-a-data-model-class"></a>Hinzufügen einer Datenmodellklasse
