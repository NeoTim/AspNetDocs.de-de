---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks-Debugging | Microsoft Docs
author: rick-anderson
description: Debuggen ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675369"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET WebHooks-Debugging

## <a name="debugging-in-azure"></a>Debuggen in Azure

Informationen zum Debuggen Ihrer Webanwendung während der Ausführung in Azure finden Sie im Tutorial [Fehlerbehebung für eine Web-App in Azure App Service mit Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).

## <a name="debugging-with-source-and-symbols"></a>Debuggen mit Quelle und Symbolen

Zusätzlich zum Debuggen Ihres eigenen Codes ist es möglich, direkt in Microsoft ASP.NET WebHooks und in der Tat alle .NET zu debuggen. Dies funktioniert unabhängig davon, ob Sie lokal oder remote debuggen. Konfigurieren Sie zunächst Visual Studio so, dass die Quelle und die Symbole gefunden werden, indem Sie zu **Debuggen** und dann zu **Optionen und Einstellungen**gehen. Legen Sie die Optionen wie folgt fest:

![Optionen und Einstellungen](_static/SourceSymbols.png)

Fügen Sie dann einen Link zu [symbolsource.org](http://symbolsource.org) zum Herunterladen der Quelle und der Symbole hinzu. Gehen Sie auf die Registerkarte **Symbole** des Menüs oben und fügen Sie Folgendes als Symbolposition hinzu:

```
http://srv.symbolsource.org/pdb/Public
```

Stellen Sie außerdem sicher, dass das Cacheverzeichnis einen kurzen Namen hat. Andernfalls können die Dateinamen zu lang werden, was dazu führt, dass die Symbole nicht geladen werden. Ein Beispielpfad ist:

```
C:\SymCache
```

Die Einstellungen sollten wie folgt aussehen:

![Options Symbol Dateispeicherort Beispiel](_static/SymSource.png)
