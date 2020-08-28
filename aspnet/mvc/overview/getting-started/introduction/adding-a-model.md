---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Hinzufügen eines Modells | Microsoft-Dokumentation
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045116"
---
# <a name="adding-a-model"></a><span data-ttu-id="2602c-102">Hinzufügen eines Modells</span><span class="sxs-lookup"><span data-stu-id="2602c-102">Adding a Model</span></span>

<span data-ttu-id="2602c-103">von [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2602c-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="2602c-104">In diesem Abschnitt fügen Sie einige Klassen zum Verwalten von Filmen in einer-Datenbank hinzu.</span><span class="sxs-lookup"><span data-stu-id="2602c-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="2602c-105">Diese Klassen werden als &quot; Modell &quot; Teil der ASP.NET MVC-App verwendet.</span><span class="sxs-lookup"><span data-stu-id="2602c-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="2602c-106">Sie verwenden eine .NET Framework Datenzugriffs Technologie, die als [Entity Framework](https://docs.microsoft.com/ef/) bezeichnet wird, um diese Modellklassen zu definieren und mit Ihnen zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="2602c-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="2602c-107">Der Entity Framework (häufig als EF bezeichnet) unterstützt ein Entwicklungsparadigma namens *Code First*.</span><span class="sxs-lookup"><span data-stu-id="2602c-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="2602c-108">Code First ermöglicht es Ihnen, Modell Objekte zu erstellen, indem einfache Klassen geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="2602c-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="2602c-109">(Diese werden auch als poco-Klassen von &quot; einfachen CLR-Objekten bezeichnet. &quot; ) Anschließend können Sie die Datenbank dynamisch von ihren Klassen erstellen lassen, wodurch ein sehr sauberer und schneller Entwicklungs Workflow ermöglicht wird.</span><span class="sxs-lookup"><span data-stu-id="2602c-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="2602c-110">Wenn Sie die Datenbank zuerst erstellen müssen, finden Sie in diesem Tutorial Weitere Informationen zur MVC-und EF-App-Entwicklung.</span><span class="sxs-lookup"><span data-stu-id="2602c-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="2602c-111">Anschließend können Sie das Tutorial "Tom fzmakens [ASP.net Gerüstbau](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) " befolgen, das den Ansatz der Datenbank behandelt.</span><span class="sxs-lookup"><span data-stu-id="2602c-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="2602c-112">Hinzufügen von Modellklassen</span><span class="sxs-lookup"><span data-stu-id="2602c-112">Adding Model Classes</span></span>

<span data-ttu-id="2602c-113">Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf den Ordner *Modelle* , und wählen Sie **Hinzufügen**und dann **Klasse**aus.</span><span class="sxs-lookup"><span data-stu-id="2602c-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="2602c-114">Geben Sie den *Klassen* Namen &quot; Movie ein &quot; .</span><span class="sxs-lookup"><span data-stu-id="2602c-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="2602c-115">Fügen Sie der-Klasse die folgenden fünf Eigenschaften hinzu `Movie` :</span><span class="sxs-lookup"><span data-stu-id="2602c-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="2602c-116">Wir verwenden die- `Movie` Klasse, um Filme in einer Datenbank darzustellen.</span><span class="sxs-lookup"><span data-stu-id="2602c-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="2602c-117">Jede Instanz eines- `Movie` Objekts entspricht einer Zeile in einer Datenbanktabelle, und jede Eigenschaft der `Movie` Klasse wird einer Spalte in der Tabelle zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="2602c-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="2602c-118">Hinweis: um "System. Data. Entity" und die zugehörige Klasse zu verwenden, müssen Sie das [Entity Framework nuget-Paket](https://www.nuget.org/packages/EntityFramework/)installieren.</span><span class="sxs-lookup"><span data-stu-id="2602c-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="2602c-119">Weitere Anweisungen finden Sie unter dem Link.</span><span class="sxs-lookup"><span data-stu-id="2602c-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="2602c-120">Fügen Sie in der gleichen Datei die folgende `MovieDBContext` Klasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="2602c-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="2602c-121">Die- `MovieDBContext` Klasse stellt den Entity Framework Movie-Daten Bank Kontext dar, der das Abrufen, speichern und Aktualisieren von `Movie` Klassen Instanzen in einer Datenbank behandelt.</span><span class="sxs-lookup"><span data-stu-id="2602c-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="2602c-122">Der `MovieDBContext` wird von der `DbContext` Basisklasse abgeleitet, die von der Entity Framework bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="2602c-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="2602c-123">Damit auf und verwiesen werden kann `DbContext` `DbSet` , müssen Sie am Anfang der Datei die folgende-Anweisung hinzufügen `using` :</span><span class="sxs-lookup"><span data-stu-id="2602c-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="2602c-124">Hierzu können Sie manuell die using-Anweisung hinzufügen, oder Sie können mit dem Mauszeiger auf die roten Wellenlinien klicken `Show potential fixes` und dann auf `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="2602c-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="2602c-125">Hinweis: mehrere nicht verwendete `using` Anweisungen wurden entfernt.</span><span class="sxs-lookup"><span data-stu-id="2602c-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="2602c-126">In Visual Studio werden nicht verwendete Abhängigkeiten als grau angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2602c-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="2602c-127">Sie können nicht verwendete Abhängigkeiten entfernen, indem Sie den Mauszeiger über die grauen Abhängigkeiten bewegen, auf nicht verwendete using-Direktiven `Show potential fixes` **Entfernen klicken.**</span><span class="sxs-lookup"><span data-stu-id="2602c-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="2602c-128">Schließlich haben wir ein Modell hinzugefügt (M in MVC).</span><span class="sxs-lookup"><span data-stu-id="2602c-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="2602c-129">Im nächsten Abschnitt Arbeiten Sie mit der Datenbank-Verbindungs Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="2602c-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2602c-130">[Zurück](adding-a-view.md)
> [Weiter](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="2602c-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
