---
title: Das Metapaket „Microsoft.AspNetCore.App“ für ASP.NET Core 2.1 und höher
author: Rick-Anderson
description: Das Metapaket „Microsoft.AspNetCore.App“ enthält alle unterstützten ASP.NET Core- und Entity Framework Core-Pakete.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
uid: fundamentals/metapackage-app
ms.openlocfilehash: 68b5aca60273a8c6ef03c0a29842e6a5305adeb3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034437"
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a>Das Metapaket „Microsoft.AspNetCore.App“ für ASP.NET Core 2.1

Für dieses Feature ist ASP.NET Core 2.1 und höher für .NET Core 2.1 und höher erforderlich.

Das [Metapaket](/dotnet/core/packages#metapackages) [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.App) für ASP.NET Core:

* Enthält keine Drittanbieterabhängigkeiten außer [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/) und [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/). Diese Drittanbieterabhängigkeiten sind erforderlich, damit die Features der wichtigsten Frameworks funktionieren.
* Enthält alle unterstützten Pakete des ASP.NET Core-Teams außer denen, die Drittanbieterabhängigkeiten enthalten (von den bereits erwähnten abgesehen).
* Enthält alle unterstützten Pakete des Entity Framework Core-Teams außer denen, die Drittanbieterabhängigkeiten enthalten (von den bereits erwähnten abgesehen).

Im Paket `Microsoft.AspNetCore.App` sind alle Features von ASP.NET Core 2.1 und höher und Entity Framework Core 2.1 und höher enthalten. Die Standardprojektvorlagen für ASP.NET Core 2.1 und höher verwenden dieses Paket. Es wird empfohlen, dass Anwendungen für ASP.NET Core 2.1 und höher und Entity Framework Core 2.1 und höher das Paket `Microsoft.AspNetCore.App` verwenden.

Die Versionsnummer des Metapakets `Microsoft.AspNetCore.App` stellt die ASP.NET Core-Version und die Entity Framework Core-Version dar.

Durch die Verwendung des Metapakets `Microsoft.AspNetCore.App` werden Versionseinschränkungen bereitgestellt, die Ihre App schützen:

* Wenn ein Paket enthalten wird, das eine transitive (nicht direkte) Abhängigkeit von einem Paket in `Microsoft.AspNetCore.App` besitzt und diese Versionsnummern sich unterscheiden, generiert NuGet einen Fehler.
* Andere Pakete, die zu Ihrer App hinzugefügt werden, können die Version der in `Microsoft.AspNetCore.App` enthaltenen Pakete nicht ändern.
* Die Konsistenz von Versionen stellt eine zuverlässige Verwendbarkeit sicher. `Microsoft.AspNetCore.App` wurde dafür entwickelt, um nicht getestete Versionskombinationen von verwandten Komponenten zu verhindern, die in derselben App zusammen verwendet werden.

Anwendungen, die das Metapaket `Microsoft.AspNetCore.App` verwenden, profitieren automatisch vom freigegebenen ASP.NET Core-Framework. Bei Verwendung des Metapakets `Microsoft.AspNetCore.App` werden mit der Anwendung **keine** Objekte aus den referenzierten NuGet-Paketen für ASP.NET Core bereitgestellt. Das freigegebene ASP.NET Core-Framework enthält diese Objekte. Die Objekte im freigegebenen Framework sind zur Verbesserung der Startzeit der Anwendung vorkompiliert. Weitere Informationen zu freigegebenen Frameworks finden Sie unter [.NET Core distribution packaging (Packen von .NET Core-Verteilungen)](/dotnet/core/build/distribution-packaging).

Die folgende Projektdatei verweist auf das Metapaket `Microsoft.AspNetCore.App` für ASP.NET Core und ist eine typische ASP.NET Core 2.1-Vorlage.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>
```

Das zuvor erwähnte Markup stellt eine typische Vorlage für Vorlage 2.1 und höher dar. Es gibt keine Versionsnummer für den Paketverweis `Microsoft.AspNetCore.App` an. Wenn die Version nicht angegeben wird, wird vom SDK eine [implizite](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md) Version angegeben (`Microsoft.NET.Sdk.Web`). Es wird empfohlen, die vom SDK angegebene implizite Version beizubehalten, statt die Versionsnummer im Paketverweis explizit festzulegen. Wenn Sie Fragen zu dieser Vorgehensweise haben, können Sie einen GitHub-Kommentar unter [Discussion for the Microsoft.AspNetCore.App implicit version (Diskussion zur impliziten Version für Microsoft.AspNetCore.App)](https://github.com/aspnet/Docs/issues/6430) verfassen.

Die implizite Version wird auf `major.minor.0` festgelegt, wenn es sich um Apps für Mobilgeräte handelt. Der Rollforwardmechanismus des freigegebenen Frameworks führt die App auf der neuesten kompatiblen Version der installierten freigegebenen Frameworks aus. Stellen Sie sicher, dass die gleiche Version des freigegebenen Frameworks in allen Umgebungen installiert ist, um zu gewährleisten, dass die gleiche Version bei der Entwicklung, beim Testen und in der Produktion verwendet wird. Bei unabhängigen Apps wird die implizite Versionsnummer auf die Versionsnummer `major.minor.patch` des freigegebenen Frameworks festgelegt, das im installierten SDK zusammengefasst ist.

Das Angeben einer Versionsnummer im `Microsoft.AspNetCore.App`-Verweis garantiert **nicht**, dass diese Version des freigegebenen Frameworks ausgewählt wird. Gehen Sie beispielsweise davon aus, dass „2.1.1“ angegeben, aber „2.1.3“ installiert ist. In diesem Fall verwendet die App Version 2.1.3. Sie können den Rollforward (für „patch“ und/oder „minor“) deaktivieren. Dies wird jedoch nicht empfohlen. Weitere Informationen zum Rollforward des dotnet-Hosts und der Konfiguration seines Verhaltens finden Sie unter [dotnet host roll forward (Rollforward des dotnet-Hosts)](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).

Für `<Project Sdk` muss `Microsoft.NET.Sdk.Web` festgelegt werden, um die implizite Version `Microsoft.AspNetCore.App` verwenden zu können.  Wenn `<Project Sdk="Microsoft.NET.Sdk">` (ohne nachgestelltes `.Web`) verwendet wird:

* Die folgende Warnung wird generiert:

     *Warnung NU1604: Projektabhängigkeit Microsoft.AspNetCore.App ist eine inklusive untere Grenze nicht enthalten. Schließen Sie eine Untergrenze in die Abhängigkeitsversion ein, um konsistente Wiederherstellungsergebnisse zu erzielen.)*
* Dies ist ein bekanntes Problem mit dem .NET Core 2.1 SDK und wird im .NET Core SDK 2.2 behoben.

<a name="update"></a>

## <a name="update-aspnet-core"></a>Aktualisieren von ASP.NET Core

Das [Metapaket](/dotnet/core/packages#metapackages) `Microsoft.AspNetCore.App` zählt nicht zu den herkömmlichen Paketen, die über NuGet aktualisiert werden. Ähnlich wie bei `Microsoft.NETCore.App` stellt `Microsoft.AspNetCore.App` eine freigegebene Runtime dar, die über eine spezielle Semantik für die Versionsverwaltung verfügt, die außerhalb von NuGet behandelt wird. Weitere Informationen finden Sie unter [Pakete, Metapakete und Frameworks](/dotnet/core/packages).

So aktualisieren Sie ASP.NET Core:

* Auf dem Entwicklungscomputer und Buildserver: Herunterladen und Installieren der [.NET Core SDK](https://www.microsoft.com/net/download).
* Auf Bereitstellungsservern: Herunterladen und Installieren der [.NET Core-Runtime](https://www.microsoft.com/net/download).

 Für Anwendungen wird beim Neustart der Anwendungen ein Rollforward auf die neueste installierte Version ausgeführt. Die Versionsnummer von `Microsoft.AspNetCore.App` muss in der Projektdatei nicht aktualisiert werden. Weitere Informationen finden Sie unter [Von Frameworks abhängige Apps führen einen Rollforward aus](/dotnet/core/versions/selection#framework-dependent-apps-roll-forward).

Wenn Ihre Anwendung zuvor `Microsoft.AspNetCore.All` verwendet hat, finden Sie weitere Informationen unter [Migrieren von Microsoft.AspNetCore.All zu Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate).
