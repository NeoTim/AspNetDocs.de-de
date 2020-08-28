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
# <a name="adding-a-model"></a>Hinzufügen eines Modells

von [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

In diesem Abschnitt fügen Sie einige Klassen zum Verwalten von Filmen in einer-Datenbank hinzu. Diese Klassen werden als &quot; Modell &quot; Teil der ASP.NET MVC-App verwendet.

Sie verwenden eine .NET Framework Datenzugriffs Technologie, die als [Entity Framework](https://docs.microsoft.com/ef/) bezeichnet wird, um diese Modellklassen zu definieren und mit Ihnen zu arbeiten. Der Entity Framework (häufig als EF bezeichnet) unterstützt ein Entwicklungsparadigma namens *Code First*. Code First ermöglicht es Ihnen, Modell Objekte zu erstellen, indem einfache Klassen geschrieben werden. (Diese werden auch als poco-Klassen von &quot; einfachen CLR-Objekten bezeichnet. &quot; ) Anschließend können Sie die Datenbank dynamisch von ihren Klassen erstellen lassen, wodurch ein sehr sauberer und schneller Entwicklungs Workflow ermöglicht wird. Wenn Sie die Datenbank zuerst erstellen müssen, finden Sie in diesem Tutorial Weitere Informationen zur MVC-und EF-App-Entwicklung. Anschließend können Sie das Tutorial "Tom fzmakens [ASP.net Gerüstbau](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) " befolgen, das den Ansatz der Datenbank behandelt.

## <a name="adding-model-classes"></a>Hinzufügen von Modellklassen

Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf den Ordner *Modelle* , und wählen Sie **Hinzufügen**und dann **Klasse**aus.

![](adding-a-model/_static/image1.png)

Geben Sie den *Klassen* Namen &quot; Movie ein &quot; .

Fügen Sie der-Klasse die folgenden fünf Eigenschaften hinzu `Movie` :

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Wir verwenden die- `Movie` Klasse, um Filme in einer Datenbank darzustellen. Jede Instanz eines- `Movie` Objekts entspricht einer Zeile in einer Datenbanktabelle, und jede Eigenschaft der `Movie` Klasse wird einer Spalte in der Tabelle zugeordnet.

Hinweis: um "System. Data. Entity" und die zugehörige Klasse zu verwenden, müssen Sie das [Entity Framework nuget-Paket](https://www.nuget.org/packages/EntityFramework/)installieren. Weitere Anweisungen finden Sie unter dem Link.

Fügen Sie in der gleichen Datei die folgende `MovieDBContext` Klasse hinzu:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

Die- `MovieDBContext` Klasse stellt den Entity Framework Movie-Daten Bank Kontext dar, der das Abrufen, speichern und Aktualisieren von `Movie` Klassen Instanzen in einer Datenbank behandelt. Der `MovieDBContext` wird von der `DbContext` Basisklasse abgeleitet, die von der Entity Framework bereitgestellt wird.

Damit auf und verwiesen werden kann `DbContext` `DbSet` , müssen Sie am Anfang der Datei die folgende-Anweisung hinzufügen `using` :

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Hierzu können Sie manuell die using-Anweisung hinzufügen, oder Sie können mit dem Mauszeiger auf die roten Wellenlinien klicken `Show potential fixes` und dann auf `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Hinweis: mehrere nicht verwendete `using` Anweisungen wurden entfernt. In Visual Studio werden nicht verwendete Abhängigkeiten als grau angezeigt. Sie können nicht verwendete Abhängigkeiten entfernen, indem Sie den Mauszeiger über die grauen Abhängigkeiten bewegen, auf nicht verwendete using-Direktiven `Show potential fixes` **Entfernen klicken.**

![](adding-a-model/_static/image3.png)

Schließlich haben wir ein Modell hinzugefügt (M in MVC). Im nächsten Abschnitt Arbeiten Sie mit der Datenbank-Verbindungs Zeichenfolge.

> [!div class="step-by-step"]
> [Zurück](adding-a-view.md)
> [Weiter](creating-a-connection-string.md)
