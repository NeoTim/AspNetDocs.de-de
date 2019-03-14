---
title: Optionsmuster in ASP.NET Core
author: guardrex
description: Erfahren Sie, wie Sie Optionsmuster verwenden, um Gruppen von zusammengehörigen Einstellungen in ASP.NET Core-Anwendungen darzustellen.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: fundamentals/configuration/options
ms.openlocfilehash: 9566ed75375bdfaa9d6d8bf898b9fb2054356017
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065217"
---
# <a name="options-pattern-in-aspnet-core"></a>Optionsmuster in ASP.NET Core

Von [Luke Latham](https://github.com/guardrex)

::: moniker range="<= aspnetcore-1.1"

Laden Sie die Version 1.1 dieses Artikel unter [Optionsmuster in ASP.NET Core (Version 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Options_1.1.pdf) herunter.

::: moniker-end

Das Optionsmuster verwendet Klassen, um Gruppen von zusammengehörigen Einstellungen darzustellen. Wenn [Konfigurationseinstellungen](xref:fundamentals/configuration/index) nach Szenario in separate Klassen isoliert werden, entspricht die Anwendung zwei wichtigen Prinzipien der Softwareentwicklung:

* [Schnittstellentrennungsprinzip (ISP) oder Kapselung](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation): &ndash;-Szenarios (Klassen), die von Konfigurationseinstellungen abhängen, sind nur von den Konfigurationseinstellungen abhängig, die sie verwenden.
* [Trennung von Bereichen](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) &ndash;: Einstellungen für die verschiedenen Teile der Anwendung hängen nicht voneinander ab und sind nicht gekoppelt.

Optionen bieten auch einen Mechanismus, um Konfigurationsdaten zu validieren. Weitere Informationen finden Sie im Abschnitt [Optionsvalidierung](#options-validation).

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>Vorraussetzungen

Verweisen Sie auf das [Microsoft.AspNetCore.App-Metapaket](xref:fundamentals/metapackage-app), oder fügen Sie einen Paketverweis auf das Paket [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/) hinzu.

## <a name="options-interfaces"></a>Optionenschnittstellen

<xref:Microsoft.Extensions.Options.IOptionsMonitor`1> wird verwendet, um Optionen abzurufen und Benachrichtigungen über Optionen für `TOptions`-Instanzen zu verwalten. <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> unterstützt die folgenden Szenarios:

* Änderungsbenachrichtigungen
* [Benannte Optionen](#named-options-support-with-iconfigurenamedoptions)
* [Erneut ladbare Konfiguration](#reload-configuration-data-with-ioptionssnapshot)
* Selektive Optionsvalidierung (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>)

Mit [Postkonfigurationsszenarien](#options-post-configuration) können Sie Optionen festlegen oder ändern, nachdem alle <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Konfigurationen durchgeführt wurden.

<xref:Microsoft.Extensions.Options.IOptionsFactory`1> ist für das Erstellen neuer Optionsinstanzen zuständig. Es verfügt über eine einzelne <xref:Microsoft.Extensions.Options.IOptionsFactory`1.Create*>-Methode. Die Standardimplementierung akzeptiert alle registrierten <xref:Microsoft.Extensions.Options.IConfigureOptions`1> und <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1> und führt alle Konfigurationen zuerst und die Postkonfigurationen danach aus. Es wird zwischen <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> und <xref:Microsoft.Extensions.Options.IConfigureOptions`1> unterschieden, und es werden nur die entsprechenden Schnittstellen aufgerufen.

<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> wird von <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> zum Zwischenspeichern der `TOptions`-Instanzen verwendet. <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> erklärt Optionsinstanzen im Monitor für ungültig, sodass der Wert neu berechnet wird (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryRemove*>). Werte können manuell mit <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryAdd*> eingeführt werden. Die <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.Clear*>-Methode wird verwendet, wenn alle benannten Instanzen bei Bedarf neu erstellt werden sollen.

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> ist nützlich in Szenarien, in denen Optionen bei jeder Anforderung neu berechnet werden sollten. Weitere Informationen finden Sie im Abschnitt [Neuladen der Konfigurationsdaten mit IOptionsSnapshot](#reload-configuration-data-with-ioptionssnapshot).

<xref:Microsoft.Extensions.Options.IOptions`1> kann zum Unterstützen von Optionen verwendet werden. Allerdings unterstützt <xref:Microsoft.Extensions.Options.IOptions`1> nicht die oben beschriebenen Szenarios von <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>. Sie können <xref:Microsoft.Extensions.Options.IOptions`1> weiterhin in bestehenden Frameworks und Bibliotheken verwenden, die bereits die <xref:Microsoft.Extensions.Options.IOptions`1>-Schnittstelle verwenden und nicht die von <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> bereitgestellten Szenarios benötigen.

## <a name="general-options-configuration"></a>Allgemeine Optionskonfiguration

Die allgemeine Optionskonfiguration wird als Beispiel &num;1 in der Beispiel-App veranschaulicht.

Eine Optionsklasse muss nicht abstrakt sein und über einen öffentlichen parameterlosen Konstruktor verfügen. Die folgende Klasse `MyOptions` verfügt über die zwei Eigenschaften: `Option1` und `Option2`. Das Festlegen von Standardwerten ist optional, aber der Klassenkonstruktor im folgenden Beispiel legt den Standardwert von `Option1` fest. `Option2` hat den Standardwert festgelegt, indem die Eigenschaft direkt initialisiert wurde (*Models/MyOptions.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptions.cs?name=snippet1)]

Die `MyOptions`-Klasse wird zum Dienstcontainer mit <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure*> hinzugefügt und an die Konfiguration gebunden:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example1)]

Das folgende Seitenmodel verwendet [konstruktorbasierte Dependency Injection](xref:mvc/controllers/dependency-injection) mit <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>, um auf die Einstellungen zugreifen zu können (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example1)]

Die *appsettings.json*-Datei des Beispiels gibt Werte für `option1` und `option2` an:

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=2-3)]

Wenn die Anwendung ausgeführt wird, gibt die `OnGet`-Methode des Seitenmodells eine Zeichenfolge zurück, die die Werte der Optionsklasse anzeigt:

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> Wenn Sie eine benutzerdefinierte <xref:System.Configuration.ConfigurationBuilder>-Klasse verwenden, um Konfigurationsoptionen aus einer Einstellungsdatei zu laden, bestätigen Sie, dass der Basispfad ordnungsgemäß festgelegt ist:
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> Sie müssen den Basispfad nicht explizit festlegen, wenn Sie Konfigurationsoptionen über <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> aus der Einstellungsdatei laden.

## <a name="configure-simple-options-with-a-delegate"></a>Konfigurieren von einfachen Optionen mit einem Delegaten

Das Konfigurieren von einfachen Optionen mit einem Delegaten wird als Beispiel &num;2 in der Beispiel-App veranschaulicht.

Verwenden Sie einen Delegaten zum Festlegen von Optionswerten. Die Beispielanwendung verwendet die `MyOptionsWithDelegateConfig`-Klasse (*Models/MyOptionsWithDelegateConfig.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

Im folgenden Code wird ein zweiter <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Dienst zum Dienstcontainer hinzugefügt. Er verwendet einen Delegaten zum Konfigurieren der Bindung mit `MyOptionsWithDelegateConfig`:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example2)]

Sie können mehrere Konfigurationsanbieter hinzufügen. Konfigurationsanbieter sind über NuGet-Pakete verfügbar und werden in der Reihenfolge ihrer Registrierung angewendet. Weitere Informationen finden Sie unter <xref:fundamentals/configuration/index>.

Jeder Aufruf von <xref:Microsoft.Extensions.Options.IConfigureOptions`1.Configure*> fügt einen <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Dienst zum Dienstcontainer hinzu. Im vorherigen Beispiel wurden die Werte von `Option1` und `Option2` beide in *appsettings.json* angegeben, aber die Werte von `Option1` und `Option2` werden vom konfigurierten Delegaten überschrieben.

Wenn mehr als ein Konfigurationsdienst aktiviert ist, *gewinnt* die letzte angegebene Konfigurationsquelle und legt den Konfigurationswert fest. Wenn die Anwendung ausgeführt wird, gibt die `OnGet`-Methode des Seitenmodells eine Zeichenfolge zurück, die die Werte der Optionsklasse anzeigt:

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>Konfigurieren von Unteroptionen

Das Konfigurieren von Unteroptionen wird als Beispiel &num;3 in der Beispiel-App veranschaulicht.

Anwendungen sollten Optionsklassen erstellen, die für bestimmte Szenariogruppen (Klassen) in der Anwendung gelten. Die Komponenten der Anwendung, die Konfigurationswerte erfordern, sollten nur über Zugriff auf die Konfigurationswerte verfügen, die sie verwenden.

Beim Binden von Optionen zur Konfiguration ist jede Eigenschaft im Optionstyp an einen Konfigurationsschlüssel des `property[:sub-property:]`-Formulars gebunden. Die `MyOptions.Option1`-Eigenschaft ist beispielsweise an den Schlüssel `Option1` gebunden, der von der `option1`-Eigenschaft in *appsettings.json* gelesen wird.

Im folgenden Code wird ein dritter <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Dienst zum Dienstcontainer hinzugefügt. Er verbindet `MySubOptions` mit dem `subsection`-Abschnitt der *appSettings.json*-Datei:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example3)]

Die `GetSection`-Erweiterungsmethode erfordert das [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/)-NuGet-Paket. Wenn die Anwendung das [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app)-Metapaket (ASP.NET Core 2.1 oder höher) verwendet, ist das Paket automatisch eingeschlossen.

Die *appsettings.json*-Datei des Beispiels definiert ein `subsection`-Element mit Schlüsseln für `suboption1` und `suboption2`:

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=4-7)]

Die `MySubOptions`-Klasse definiert die Eigenschaften `SubOption1` und `SubOption2` zur Aufnahme der Optionswerte (*Models/MySubOptions.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MySubOptions.cs?name=snippet1)]

Die `OnGet`-Methode des Seitenmodells gibt eine Zeichenfolge mit den Optionswerten (*Pages/Index.cshtml.cs*) zurück:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example3)]

Wenn die App ausgeführt wird, gibt die `OnGet`-Methode eine Zeichenfolge zurück, die die Werte der untergeordneten Optionsklasse anzeigt:

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>Optionen, die durch ein Ansichtsmodell oder mit direkter View Injection bereitgestellt werden

Optionen, die durch ein Ansichtsmodell oder mit direkter View Injection bereitgestellt werden, werden im Beispiel &num;4 in der Beispiel-App veranschaulicht.

Optionen können in einem Ansichtsmodell oder durch direkte Injection von <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> in eine Ansicht (*Pages/Index.cshtml.cs*) angegeben werden:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example4)]

Die Beispiel-App zeigt das Einfügen von `IOptionsMonitor<MyOptions>` mit einer `@inject`-Anweisung:

[!code-cshtml[](options/samples/2.x/OptionsSample/Pages/Index.cshtml?range=1-10&highlight=4)]

Wenn die App ausgeführt wird, werden die Optionswerte in der gerenderten Seite angezeigt:

![Optionswerte Option1: value1_from_json und Option2: -1 werden aus dem Modell geladen und in die Ansicht eingefügt.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>Neuladen der Konfigurationsdaten mit IOptionsSnapshot

Das Neuladen der Konfigurationsdaten mit <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> wird im Beispiel &num;5 in der Beispiel-App veranschaulicht.

<xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> unterstützt das Neuladen von Optionen mit minimalem Verarbeitungsaufwand.

Optionen werden einmal pro Anforderung berechnet. Dies geschieht, wenn auf sie zugegriffen wird und sie für die Dauer der Anforderung zwischengespeichert werden.

Im folgenden Beispiel wird veranschaulicht, wie eine neue <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> nach den *appsettings.json*-Veränderungen erstellt wird (*Pages/Index.cshtml.cs*). Mehrere Anforderungen an den Server geben konstante Werte zurück, die von der *appsettings.json*-Datei bereitgestellt werden, bis die Datei geändert wird und die Konfiguration neu lädt.

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example5)]

Die folgende Abbildung zeigt die anfänglichen `option1`- und `option2`-Werte, die aus der *appsettings.json*-Datei geladen werden:

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

Ändern Sie die Werte in der *appsettings.json*-Datei auf `value1_from_json UPDATED` und `200`. Speichern Sie die *appsettings.json*-Datei. Aktualisieren Sie den Browser, um festzustellen, ob die Optionswerte aktualisiert wurden:

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>Unterstützung für benannte Optionen mit IConfigureNamedOptions

Unterstützung für benannte Optionen mit <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> wird als Beispiel &num;6 in der Beispiel-App veranschaulicht.

Die Unterstützung für *benannte Optionen* ermöglicht es der Anwendung, zwischen den Konfigurationen benannter Optionen zu unterscheiden. In der Beispiel-App werden benannte Optionen mit [OptionsServiceCollectionExtensions.Configure](xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure*) deklariert. Dadurch wird wiederum die Erweiterungsmethode [ConfigureNamedOptions\<TOptions>.Configure](xref:Microsoft.Extensions.Options.ConfigureNamedOptions`1.Configure*) aufgerufen:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example6)]

Die Beispielanwendung greift mit <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1.Get*> auf die benannten Optionen zu (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example6)]

Bei der Ausführung der Beispielanwendung werden die benannten Optionen zurückgegeben:

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

`named_options_1`-Werte werden von der Konfiguration bereitgestellt. Sie werden aus der *appsettings.json*-Datei geladen. `named_options_2`-Werte werden bereitgestellt vom:

* `named_options_2`-Delegat in `ConfigureServices` für `Option1`.
* Der Standardwert für `Option2` wird von der `MyOptions`-Klasse bereitgestellt.

## <a name="configure-all-options-with-the-configureall-method"></a>Konfigurieren aller Optionen mit der ConfigureAll-Methode

Konfigurieren Sie alle Optionsinstanzen mit der <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*>-Methode. Der folgende Code konfiguriert `Option1` für alle Konfigurationsinstanzen mit einem gemeinsamen Wert. Fügen Sie der `Startup.ConfigureServices`-Methode manuell den folgenden Code hinzu:

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

Das Ausführen der Beispielanwendung nach dem Hinzufügen des Codes führt zu folgendem Ergebnis:

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> Alle Optionen sind benannte Instanzen. Vorhandene <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Instanzen werden behandelt, als ob sie auf die `Options.DefaultName`-Instanz abzielen. Diese ist `string.Empty`. <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> implementiert auch <xref:Microsoft.Extensions.Options.IConfigureOptions`1>. Die standardmäßige Implementierung von <xref:Microsoft.Extensions.Options.IOptionsFactory`1> verfügt über eine Logik, um jede einzelne entsprechend zu verwenden. Die benannte Option `null` wird verwendet, um auf alle benannten Instanzen anstelle einer bestimmten benannten Instanz abzuzielen (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*> und <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*> verwenden diese Konvention).

## <a name="optionsbuilder-api"></a>OptionsBuilder-API

<xref:Microsoft.Extensions.Options.OptionsBuilder`1> dient zum Konfigurieren von `TOptions`-Instanzen. `OptionsBuilder` optimiert die Erstellung von benannten Optionen, da es sich nur um einen einzelnen Parameter für den ersten `AddOptions<TOptions>(string optionsName)`-Aufruf handelt statt um alle nachfolgenden Aufrufe. Die Optionsvalidierung und die `ConfigureOptions`-Überladungen, die Dienstabhängigkeiten akzeptieren, sind nur über `OptionsBuilder` verfügbar.

```csharp
// Options.DefaultName = "" is used.
services.AddOptions<MyOptions>().Configure(o => o.Property = "default");

services.AddOptions<MyOptions>("optionalName")
    .Configure(o => o.Property = "named");
```

## <a name="use-di-services-to-configure-options"></a>Verwenden von DI-Diensten zum Konfigurieren von Optionen

Beim Konfigurieren von Optionen haben Sie zwei Möglichkeiten, auf andere Dienste aus Dependency Injections zuzugreifen:

* Übergeben eines Konfigurationsdelegaten an [Konfigurieren](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) auf [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1). [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1) stellt Überladungen von [Konfigurieren](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) zur Verfügung, die es Ihnen ermöglichen, bis zu fünf Dienste zu verwenden, um Optionen zu konfigurieren:

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<Service1, Service2, Service3, Service4, Service5>(
          (o, s, s2, s3, s4, s5) => 
              o.Property = DoSomethingWith(s, s2, s3, s4, s5));
  ```

* Erstellen Ihres eigenen Typs, der <xref:Microsoft.Extensions.Options.IConfigureOptions`1> oder <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> implementiert, und Registrieren des Typs als Dienst.

Es empfiehlt sich das Übergeben eines Konfigurationsdelegaten an [Konfigurieren](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*), da das Erstellen eines Diensts etwas komplexer ist. Selbst einen eigenen Typ zu erstellen ist gleichbedeutend mit dem, was das Framework für Sie übernimmt, wenn Sie [Konfigurieren](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) verwenden. Wenn [Konfigurieren](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) aufgerufen wird, wird eine vorübergehende, generische <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> registriert, die über einen Konstruktor verfügt, der die angegeben generischen Diensttypen akzeptiert. 

::: moniker range=">= aspnetcore-2.2"

## <a name="options-validation"></a>Überprüfung von Optionen

Sie können Optionen überprüfen, wenn diese konfiguriert werden. Rufen Sie `Validate` mit einer Überprüfungsmethode auf, die `true` zurückgibt, wenn die Optionen gültig sind, und `false` zurückgibt, wenn sie es nicht sind:

```csharp
// Registration
services.AddOptions<MyOptions>("optionalOptionsName")
    .Configure(o => { }) // Configure the options
    .Validate(o => YourValidationShouldReturnTrueIfValid(o), 
        "custom error");

// Consumption
var monitor = services.BuildServiceProvider()
    .GetService<IOptionsMonitor<MyOptions>>();
  
try
{
    var options = monitor.Get("optionalOptionsName");
}
catch (OptionsValidationException e) 
{
   // e.OptionsName returns "optionalOptionsName"
   // e.OptionsType returns typeof(MyOptions)
   // e.Failures returns a list of errors, which would contain 
   //     "custom error"
}
```

Im vorherigen Beispiel wurde die benannte Optionsinstanz auf `optionalOptionsName` festgelegt. Die Standardoptionsinstanz ist `Options.DefaultName`.

Überprüfungen werden ausgeführt, wenn die Optionsinstanz erstellt wird. Ihre Optionsinstanz besteht die Überprüfung beim ersten Zugriff garantiert.

> [!IMPORTANT]
> Die Überprüfung von Optionen schützt nicht davor, dass Optionen nach der ersten Konfiguration und Überprüfung geändert werden.

Die `Validate`-Methode akzeptiert ein `Func<TOptions, bool>`-Element. Um die Überprüfung vollständig anzupassen, implementieren Sie `IValidateOptions<TOptions>`. Dies ermöglicht Folgendes:

* Eine Überprüfung von mehreren Optionstypen: `class ValidateTwo : IValidateOptions<Option1>, IValidationOptions<Option2>`
* Eine Überprüfung, die von einem anderen Optionstyp abhängig ist: `public DependsOnAnotherOptionValidator(IOptionsMonitor<AnotherOption> options)`

`IValidateOptions` validiert Folgendes:

* Eine bestimmte benannte Optionsinstanz.
* Alle Optionen, wenn `name` den Wert `null` aufweist.

Geben Sie ein `ValidateOptionsResult` aus Ihrer Implementierung der Schnittstelle zurück:

```csharp
public interface IValidateOptions<TOptions> where TOptions : class
{
    ValidateOptionsResult Validate(string name, TOptions options);
}
```

Die Überprüfung auf Basis von Datenanmerkungen ist über das Paket [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) durch Aufrufen der `ValidateDataAnnotations`-Methode in `OptionsBuilder<TOptions>` verfügbar. `Microsoft.Extensions.Options.DataAnnotations` ist im Metapaket [Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) (ASP.NET Core 2.2 oder höher) enthalten.

```csharp
private class AnnotatedOptions
{
    [Required]
    public string Required { get; set; }

    [StringLength(5, ErrorMessage = "Too long.")]
    public string StringLength { get; set; }

    [Range(-5, 5, ErrorMessage = "Out of range.")]
    public int IntRange { get; set; }
}

[Fact]
public void CanValidateDataAnnotations()
{
    var services = new ServiceCollection();
    services.AddOptions<AnnotatedOptions>()
        .Configure(o =>
        {
            o.StringLength = "111111";
            o.IntRange = 10;
            o.Custom = "nowhere";
        })
        .ValidateDataAnnotations();

    var sp = services.BuildServiceProvider();

    var error = Assert.Throws<OptionsValidationException>(() => 
        sp.GetRequiredService<IOptionsMonitor<AnnotatedOptions>>().Value);
    ValidateFailure<AnnotatedOptions>(error, Options.DefaultName, 1,
        "DataAnnotation validation failed for members Required " +
            "with the error 'The Required field is required.'.",
        "DataAnnotation validation failed for members StringLength " +
            "with the error 'Too long.'.",
        "DataAnnotation validation failed for members IntRange " +
            "with the error 'Out of range.'.");
}
```

Die vorzeitige Überprüfung (Fail-fast beim Start) wird für ein späteres Release in Erwägung.

::: moniker-end

## <a name="options-post-configuration"></a>Optionen für die Postkonfiguration

Legen Sie die Postkonfiguration mit <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1> fest. Die Postkonfiguration erfolgt, nachdem die gesamte <xref:Microsoft.Extensions.Options.IConfigureOptions`1>-Konfiguration abgeschlossen ist:

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

<xref:Microsoft.Extensions.Options.IPostConfigureOptions`1.PostConfigure*> ist nach dem Konfigurieren der benannten Optionen verfügbar:

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

Verwenden Sie <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*> zur Postkonfiguration aller Konfigurationsinstanzen:

```csharp
services.PostConfigureAll<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="accessing-options-during-startup"></a>Zugreifen auf Optionen während des Starts

<xref:Microsoft.Extensions.Options.IOptions`1> und <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> können in `Startup.Configure` verwendet werden, da Dienste erstellt werden, bevor die `Configure`-Methode ausgeführt wird.

```csharp
public void Configure(IApplicationBuilder app, IOptionsMonitor<MyOptions> optionsAccessor)
{
    var option1 = optionsAccessor.CurrentValue.Option1;
}
```

Verwenden Sie <xref:Microsoft.Extensions.Options.IOptions`1> oder <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> nicht in `Startup.ConfigureServices`. Es kann einen inkonsistenten Optionszustand geben. Dies liegt an der Reihenfolge der Dienstregistrierungen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:fundamentals/configuration/index>
