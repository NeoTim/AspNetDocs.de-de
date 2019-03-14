---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038867"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="61271-101">Hinzufügen eines Modells zu einer ASP.NET Core MVC-App</span><span class="sxs-lookup"><span data-stu-id="61271-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="61271-102">Von [Rick Anderson](https://twitter.com/RickAndMSFT) und [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="61271-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="61271-103">In diesem Abschnitt fügen Sie einer Datenbank einige Klassen für die Verwaltung von Filmen hinzu.</span><span class="sxs-lookup"><span data-stu-id="61271-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="61271-104">Diese Klassen bilden den „**M**odell“-Teil der **M**VC-App.</span><span class="sxs-lookup"><span data-stu-id="61271-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="61271-105">Verwenden Sie diese Klassen mit [Entity Framework Core](/ef/core) (EF Core), um mit einer Datenbank zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="61271-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="61271-106">EF Core ist ein ORM-Framework (Objektrelationales Mapping, ORM), das den Datenzugriffscode vereinfacht, den Sie schreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="61271-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="61271-107">[EF Core unterstützt viele Datenbank-Engines](/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="61271-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="61271-108">Die Modellklassen, die Sie erstellen, werden als POCO-Klassen (von „plain-old CLR objects“) bezeichnet, da sie nicht über eine Abhängigkeit von EF Core verfügen.</span><span class="sxs-lookup"><span data-stu-id="61271-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="61271-109">Sie definieren lediglich die Eigenschaften der Daten, die in der Datenbank gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="61271-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="61271-110">In diesem Tutorial schreiben Sie zuerst die Modellklassen. Anschließend erstellt EF Core die Datenbank.</span><span class="sxs-lookup"><span data-stu-id="61271-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="61271-111">Eine alternative Methode, die hier nicht aufgeführt ist, besteht darin, Modellklassen aus einer vorhandenen Datenbank zu generieren.</span><span class="sxs-lookup"><span data-stu-id="61271-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="61271-112">Weitere Informationen zu diesem Verfahren finden Sie unter [ASP.NET Core: Vorhandene Datenbank](/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="61271-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="61271-113">Hinzufügen einer Datenmodellklasse</span><span class="sxs-lookup"><span data-stu-id="61271-113">Add a data model class</span></span>
