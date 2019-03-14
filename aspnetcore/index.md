---
title: Einführung in ASP.NET Core
author: rick-anderson
description: 'Dieser Artikel enthält eine Einführung in ASP.NET Core, ein plattformübergreifendes, leistungsstarkes Open-Source-Framework für das Erstellen moderner, cloudbasierter Anwendungen, die mit dem Internet verbunden sind.'
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: index
---
# <a name="introduction-to-aspnet-core"></a>Einführung in ASP.NET Core

Von [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) und [Shaun Luttin](https://twitter.com/dicshaunary)

ASP.NET Core ist ein plattformübergreifendes, leistungsstarkes [Open-Source](https://github.com/aspnet/home)-Framework zum Erstellen moderner, cloudbasierter mit dem Internet verbundener Anwendungen. ASP.NET Core ermöglicht Folgendes:

* Erstellen von Web-Apps und -diensten, [IoT-Apps](https://www.microsoft.com/internet-of-things/) und mobilen Back-Ends.
* Verwenden Ihrer bevorzugten Entwicklungstools unter Windows, macOS und Linux
* Bereitstellen in der Cloud oder im lokalen System
* Ausführen in [.NET Core oder .NET Framework](/dotnet/articles/standard/choosing-core-framework-server)

## <a name="why-use-aspnet-core"></a>Gründe für ASP.NET Core

Millionen von Entwicklern setzen bei der Erstellung von Web-Apps auf [ASP.NET 4.x](/aspnet/overview). Bei ASP.NET Core handelt es sich um eine Neugestaltung von ASP.NET 4.x mit Änderungen an der Architektur, die ein schlankeres Framework mit größerer Modularität ergeben.

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a>Erstellen von Web-APIs und Webbenutzeroberflächen mithilfe von ASP.NET Core MVC

ASP.NET Core MVC bietet Funktionen zum Erstellen von [Web-APIs](xref:tutorials/first-web-api) und [Web-Apps](xref:tutorials/razor-pages/index):

* Das Muster [Model-View-Controller (MVC)](xref:mvc/overview) sorgt dafür, dass Ihre Web-APIs und Web-Apps testfähig sind.
* [Razor Pages](xref:razor-pages/index) ist ein seitenbasiertes Programmiermodell, mit dem Sie Webbenutzeroberflächen einfacher und schneller erstellen können.
* Das [Razor-Markup](xref:mvc/views/razor) bietet eine produktive Syntax für [Razor Pages](xref:razor-pages/index) und [MVC-Ansichten](xref:mvc/views/overview).
* [Taghilfsprogramme](xref:mvc/views/tag-helpers/intro) ermöglichen serverseitigem Code das Mitwirken am Erstellen und Rendern von HTML-Elementen in Razor-Dateien.
* Die integrierte Unterstützung für [mehrere Datenformate und Inhaltsaushandlung](xref:web-api/advanced/formatting) ermöglicht Ihren Web-APIs das Erreichen einer breiten Palette von Clients, wie z.B. Browser und Mobilgeräte.
* Die [Modellbindung](xref:mvc/models/model-binding) ordnet Daten aus HTTP-Anforderungen automatisch Aktionsmethodenparametern zu.
* Die [Modellvalidierung](xref:mvc/models/validation) führt automatisch eine client- und serverseitige Validierung aus.

## <a name="client-side-development"></a>Clientseitige Entwicklung

ASP.NET Core integriert sich nahtlos in gängige clientseitige Frameworks und Bibliotheken, einschließlich [Razor Components](xref:razor-components/index), [Angular](xref:spa/angular), [React](xref:spa/react) und [Bootstrap](https://getbootstrap.com/). Weitere Informationen finden Sie unter [Razor Components](xref:razor-components/index) und verwandten Themen unter *Clientseitige Entwicklung*.

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a>ASP.NET Core, das .NET Framework anzielt.

ASP.NET Core 2.x kann für .NET Core oder .NET Framework verwendet werden. ASP.NET Core-Apps, die .NET Framework anzielen, sind nicht plattformübergreifend, sondern können nur unter Windows ausgeführt werden. Für gewöhnlich besteht ASP.NET Core 2.x aus [.NET Standard](/dotnet/standard/net-standard)-Bibliotheken. Solange .NET Standard 2.0 unterstützt wird, können mit .NET Standard 2.0 geschriebene Apps überall ausgeführt werden.

ASP.NET Core 2.x wird unter .NET Framework-Versionen unterstützt, die mit dem .NET Standard 2.0 kompatibel sind:

* .NET Framework 4.7.1 und später wird dringend empfohlen.
* .NET Framework 4.6.1 und höher.

ASP.NET Core 3.0 und höher kann nur in .NET Core ausgeführt werden. Weitere Informationen zu dieser Änderung finden Sie im Blogbeitrag zu [kommenden Änderungen in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/).

Das Anzielen auf .NET Core bringt mit jedem Release mehr und mehr Vorteile mit sich. Einige Vorteile von .NET Core gegenüber .NET Framework sind:

* Plattformübergreifend Wird unter macOS, Linux und Windows ausgeführt.
* Leistungssteigerung
* Parallele Versionsverwaltung
* Neue APIs
* Quelle öffnen

Es wird daran gearbeitet, die API-Lücke von .NET Framework zu .NET Core zu schließen. Das [Windows Compatibility Pack](/dotnet/core/porting/windows-compat-pack) stellt Tausende nur unter Windows verfügbare APIs in .NET Core zur Verfügung. Diese APIs waren in .NET Core 1.x nicht verfügbar.

## <a name="recommended-learning-path"></a>Empfohlener Lernpfad

Als Einführung in die Entwicklung von ASP.NET Core-Apps empfehlen wir die folgenden Tutorials und Artikel:

1. Folgen Sie einem Tutorial, das für den Typ von App bestimmt ist, den Sie entwickeln oder verwalten möchten:

   |App-Typ  |Szenario  |Lernprogramm  |
   |----------|----------|----------|
   |Web-App       | Für Neuentwicklungen        |[Erste Schritte mit Razor Pages](xref:tutorials/razor-pages/razor-pages-start) |
   |Web-App       | Für die Verwaltung einer MVC-App |[Erste Schritte mit MVC](xref:tutorials/first-mvc-app/start-mvc)|
   |Web-API       |                            |[Erstellen einer Web-API](xref:tutorials/first-web-api)\*  |
   |Echtzeit-App |                            |[Erste Schritte mit SignalR](xref:tutorials/signalr) |

1. Folgen Sie einem Tutorial, in dem die Grundlagen des Datenzugriffs erklärt werden:

   |Szenario  |Lernprogramm  |
   |----------|----------|
   | Für Neuentwicklungen        |[Razor Pages mit Entity Framework Core](xref:data/ef-rp/intro) |
   | Für die Verwaltung einer MVC-App |[MVC mit Entity Framework Core](xref:data/ef-mvc/intro)

1. Übersicht über ASP.NET Core-Features, die alle App-Typen bieten:

   * [Grundlagen](xref:fundamentals/index)

1. Suchen Sie im Inhaltsverzeichnis nach weiteren interessanten Themen.

\* Es gibt ein neues [Web-API-Tutorial, dem Sie vollständig im Browser folgen können](https://docs.microsoft.com/learn/modules/build-web-api-net-core), ohne dass eine lokale Entwicklungsumgebung installiert werden muss.  Der Code wird in einer [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) ausgeführt, und zum Testen wird [curl](https://curl.haxx.se/) verwendet.

## <a name="how-to-download-a-sample"></a>Herunterladen eines Beispiels

Viele der Artikel und Tutorials enthalten Links zu Beispielcode.

1. [Laden Sie die Zip-Datei des ASP.NET Repositorys herunter](https://codeload.github.com/aspnet/Docs/zip/master).
1. Entpacken Sie die Datei *Docs-master.zip*.
1. Navigieren Sie mit der URL in der Beispielverknüpfung zum Beispielverzeichnis.

### <a name="preprocessor-directives-in-sample-code"></a>Präprozessoranweisungen in Beispielcode

In Beispiel-Apps werden die C#-Anweisungen `#define` und `#if-#else/#elif-#endif` zum selektiven Kompilieren und Ausführen unterschiedlicher Abschnitte des Beispielcodes verwendet. So werden verschiedene Szenarios veranschaulicht. Für die Beispiele, die diesen Ansatz verwenden, legen Sie die Anweisung `#define` am Anfang der C#-Dateien auf das Symbol fest, das dem Szenario zugeordnet ist, welches Sie ausführen möchten. Für einige Beispiele müssen Sie möglicherweise das Symbol in mehreren Dateien festlegen, um ein Szenario durchführen zu können.

Die folgende `#define`-Symbolliste gibt beispielsweise an, dass vier Szenarios verfügbar sind (ein Szenario pro Symbol). Die aktuelle Beispielkonfiguration führt das `TemplateCode`-Szenario aus:

```csharp
#define TemplateCode // or LogFromMain or ExpandDefault or FilterInCode
```

Damit das Beispiel das `ExpandDefault`-Szenario ausführt, definieren Sie das `ExpandDefault`-Symbol und lassen Sie die übrigen Symbole auskommentiert:

```csharp
#define ExpandDefault // TemplateCode or LogFromMain or FilterInCode
```

Weitere Informationen zur Verwendung von [C#-Präprozessoranweisungen](/dotnet/csharp/language-reference/preprocessor-directives/), um selektiv bestimmte Codeabschnitte zu kompilieren, finden Sie unter [#define (C#-Referenz)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define) und [#if (C#-Referenz)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if).

### <a name="regions-in-sample-code"></a>Bereiche in Beispielcode

Einige Beispiel-Apps enthalten Codeabschnitte, die von den C#-Anweisungen [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) und [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) umschlossen werden. Das Buildsystem der Dokumentation fügt diese Bereiche in den gerenderten Dokumentationsartikel ein.  

Namen von Bereichen enthalten oft das Wort „snippet“ (Ausschnitt). Im folgenden Beispiel ist ein Bereich mit dem Namen `snippet_FilterInCode` enthalten:

```csharp
#region snippet_FilterInCode
WebHost.CreateDefaultBuilder(args)
    .UseStartup<Startup>()
    .ConfigureLogging(logging =>
        logging.AddFilter("System", LogLevel.Debug)
            .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Trace))
            .Build();
#endregion
```

In der Markdowndatei wird auf den vorherigen C#-Codeausschnitt mit der folgenden Zeile verwiesen:

```
[!code-csharp[](sample/SampleApp/Program.cs?name=snippet_FilterInCode)]
```

Sie können die Anweisungen `#region` und `#endregion`, die den Code umschließen, ohne Weiteres ignorieren (oder entfernen). Ändern Sie jedoch den Code innerhalb dieser Anweisungen nicht, wenn Sie die im Artikel beschriebenen Beispielszenarios durchführen möchten. Wenn Sie andere Szenarios ausprobieren möchten, können Sie den Code anpassen.

Weitere Informationen finden Sie unter [Contribute to the ASP.NET documentation: Code snippets (Mitwirken an der ASP.NET-Dokumentation: Codeausschnitte)](https://github.com/aspnet/Docs/blob/master/CONTRIBUTING.md#code-snippets).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Ressourcen:

* <xref:getting-started>
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [ASP.NET Core – Grundlagen](xref:fundamentals/index)
* Im [wöchentlichen ASP.NET Community Standup](https://live.asp.net/) werden die Fortschritte und Pläne des Teams behandelt. Zudem werden neue Blogs und Drittanbietersoftware vorgestellt.
