---
title: Sichere Speicherung von app-Geheimnissen bei der Entwicklung in ASP.NET Core
author: rick-anderson
description: Informationen Sie zum Speichern und Abrufen von vertraulichen Informationen wie app-Geheimnissen während der Entwicklung von ASP.NET Core-Apps.
ms.author: scaddie
ms.custom: mvc
ms.date: 01/31/2019
uid: security/app-secrets
ms.openlocfilehash: eaa2e9d1ba98d391a29a9ff55872d062df016b87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030147"
---
# <a name="safe-storage-of-app-secrets-in-development-in-aspnet-core"></a><span data-ttu-id="3a443-103">Sichere Speicherung von app-Geheimnissen bei der Entwicklung in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3a443-103">Safe storage of app secrets in development in ASP.NET Core</span></span>

<span data-ttu-id="3a443-104">Durch [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), und [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="3a443-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Daniel Roth](https://github.com/danroth27), and [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="3a443-105">[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([Vorgehensweise zum Herunterladen](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3a443-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/app-secrets/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3a443-106">Dieses Dokument erläutert die Verfahren zum Speichern und Abrufen von sensiblen Daten während der Entwicklung von ASP.NET Core-Apps.</span><span class="sxs-lookup"><span data-stu-id="3a443-106">This document explains techniques for storing and retrieving sensitive data during the development of an ASP.NET Core app.</span></span> <span data-ttu-id="3a443-107">Speichern Sie niemals Kennwörter oder andere sensiblen Daten im Quellcode.</span><span class="sxs-lookup"><span data-stu-id="3a443-107">Never store passwords or other sensitive data in source code.</span></span> <span data-ttu-id="3a443-108">Produktionsgeheimnisse sollten nicht verwendet werden zu Entwicklungs- oder Testzwecken.</span><span class="sxs-lookup"><span data-stu-id="3a443-108">Production secrets shouldn't be used for development or test.</span></span> <span data-ttu-id="3a443-109">Sie können Azure-Test- und -Produktionsgeheimnisse mit dem [Konfigurationsanbieter Azure Key Vault](xref:security/key-vault-configuration) speichern und schützen.</span><span class="sxs-lookup"><span data-stu-id="3a443-109">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

## <a name="environment-variables"></a><span data-ttu-id="3a443-110">Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="3a443-110">Environment variables</span></span>

<span data-ttu-id="3a443-111">Umgebungsvariablen werden zum Speichern von app-Geheimnisse in Code oder in lokalen Konfigurationsdateien zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="3a443-111">Environment variables are used to avoid storage of app secrets in code or in local configuration files.</span></span> <span data-ttu-id="3a443-112">Umgebungsvariablen Überschreiben von Konfigurationswerten für alle zuvor angegebenen Konfigurationsquellen.</span><span class="sxs-lookup"><span data-stu-id="3a443-112">Environment variables override configuration values for all previously specified configuration sources.</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="3a443-113">Konfigurieren Sie das Lesen der Werte von Umgebungsvariablen, durch den Aufruf [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in die `Startup` Konstruktor:</span><span class="sxs-lookup"><span data-stu-id="3a443-113">Configure the reading of environment variable values by calling [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=8)]

::: moniker-end

<span data-ttu-id="3a443-114">Erwägen Sie eine ASP.NET Core-Web-app in der **einzelne Benutzerkonten** Sicherheit ist aktiviert.</span><span class="sxs-lookup"><span data-stu-id="3a443-114">Consider an ASP.NET Core web app in which **Individual User Accounts** security is enabled.</span></span> <span data-ttu-id="3a443-115">Ist eine standardmäßige Datenbank-Verbindungszeichenfolge des Projekts enthalten *"appSettings.JSON"* Datei mit dem Schlüssel `DefaultConnection`.</span><span class="sxs-lookup"><span data-stu-id="3a443-115">A default database connection string is included in the project's *appsettings.json* file with the key `DefaultConnection`.</span></span> <span data-ttu-id="3a443-116">Die Standardverbindungszeichenfolge ist für LocalDB, im Benutzermodus ausgeführt wird und ein Kennwort erfordert.</span><span class="sxs-lookup"><span data-stu-id="3a443-116">The default connection string is for LocalDB, which runs in user mode and doesn't require a password.</span></span> <span data-ttu-id="3a443-117">Während der Bereitstellung von Apps die `DefaultConnection` Schlüssel-Wert kann überschrieben werden, mit dem Wert für eine Umgebungsvariable.</span><span class="sxs-lookup"><span data-stu-id="3a443-117">During app deployment, the `DefaultConnection` key value can be overridden with an environment variable's value.</span></span> <span data-ttu-id="3a443-118">Die Umgebungsvariable kann die vollständige Verbindungszeichenfolge mit vertraulichen Anmeldeinformationen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="3a443-118">The environment variable may store the complete connection string with sensitive credentials.</span></span>

> [!WARNING]
> <span data-ttu-id="3a443-119">Umgebungsvariablen werden in der Regel in einfachen, unverschlüsselten Text gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3a443-119">Environment variables are generally stored in plain, unencrypted text.</span></span> <span data-ttu-id="3a443-120">Wenn der Computer oder Prozess gefährdet ist, können die Umgebungsvariablen von nicht vertrauenswürdigen Parteien zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-120">If the machine or process is compromised, environment variables can be accessed by untrusted parties.</span></span> <span data-ttu-id="3a443-121">Zusätzliche Maßnahmen zum Verhindern der Offenlegung von geheimen Benutzerschlüssel können erforderlich sein.</span><span class="sxs-lookup"><span data-stu-id="3a443-121">Additional measures to prevent disclosure of user secrets may be required.</span></span>

## <a name="secret-manager"></a><span data-ttu-id="3a443-122">Geheimnis-Manager</span><span class="sxs-lookup"><span data-stu-id="3a443-122">Secret Manager</span></span>

<span data-ttu-id="3a443-123">Secret Manager-Tool werden sensible Daten gespeichert, während der Entwicklung von einem ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="3a443-123">The Secret Manager tool stores sensitive data during the development of an ASP.NET Core project.</span></span> <span data-ttu-id="3a443-124">In diesem Kontext ist ein Stück von sensiblen Daten ein app-Geheimnis an.</span><span class="sxs-lookup"><span data-stu-id="3a443-124">In this context, a piece of sensitive data is an app secret.</span></span> <span data-ttu-id="3a443-125">App-Geheimnisse werden in einem gesonderten Speicherort aus der Projektstruktur gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3a443-125">App secrets are stored in a separate location from the project tree.</span></span> <span data-ttu-id="3a443-126">Die app-Geheimnisse sind einem bestimmten Projekt zugeordnet oder für mehrere Projekte freigegeben.</span><span class="sxs-lookup"><span data-stu-id="3a443-126">The app secrets are associated with a specific project or shared across several projects.</span></span> <span data-ttu-id="3a443-127">Die app-Geheimnisse sind nicht in quellcodeverwaltung eingecheckt.</span><span class="sxs-lookup"><span data-stu-id="3a443-127">The app secrets aren't checked into source control.</span></span>

> [!WARNING]
> <span data-ttu-id="3a443-128">Secret Manager-Tool nicht zum Verschlüsseln der vertraulichen Daten und sollte nicht als vertrauenswürdiger Speicher behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-128">The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store.</span></span> <span data-ttu-id="3a443-129">Es ist nur zu Entwicklungszwecken.</span><span class="sxs-lookup"><span data-stu-id="3a443-129">It's for development purposes only.</span></span> <span data-ttu-id="3a443-130">Die Schlüssel und Werte werden in einer JSON-Konfigurationsdatei im Benutzerprofilverzeichnis gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3a443-130">The keys and values are stored in a JSON configuration file in the user profile directory.</span></span>

## <a name="how-the-secret-manager-tool-works"></a><span data-ttu-id="3a443-131">Wie funktioniert das Secret Manager-tool</span><span class="sxs-lookup"><span data-stu-id="3a443-131">How the Secret Manager tool works</span></span>

<span data-ttu-id="3a443-132">Secret Manager-Tool abstrahiert die Implementierungsdetails wie, wo und wie die Werte gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-132">The Secret Manager tool abstracts away the implementation details, such as where and how the values are stored.</span></span> <span data-ttu-id="3a443-133">Sie können das Tool verwenden, ohne zu wissen, diese Implementierungsdetails.</span><span class="sxs-lookup"><span data-stu-id="3a443-133">You can use the tool without knowing these implementation details.</span></span> <span data-ttu-id="3a443-134">Die Werte werden in einer JSON-Konfigurationsdatei in eine System-geschützten Benutzerprofilordner auf dem lokalen Computer gespeichert:</span><span class="sxs-lookup"><span data-stu-id="3a443-134">The values are stored in a JSON configuration file in a system-protected user profile folder on the local machine:</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="3a443-135">Windows</span><span class="sxs-lookup"><span data-stu-id="3a443-135">Windows</span></span>](#tab/windows)

<span data-ttu-id="3a443-136">System-Dateipfad:</span><span class="sxs-lookup"><span data-stu-id="3a443-136">File system path:</span></span>

`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

# <a name="macostabmacos"></a>[<span data-ttu-id="3a443-137">macOS</span><span class="sxs-lookup"><span data-stu-id="3a443-137">macOS</span></span>](#tab/macos)

<span data-ttu-id="3a443-138">System-Dateipfad:</span><span class="sxs-lookup"><span data-stu-id="3a443-138">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

# <a name="linuxtablinux"></a>[<span data-ttu-id="3a443-139">Linux</span><span class="sxs-lookup"><span data-stu-id="3a443-139">Linux</span></span>](#tab/linux)

<span data-ttu-id="3a443-140">System-Dateipfad:</span><span class="sxs-lookup"><span data-stu-id="3a443-140">File system path:</span></span>

`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`

---

<span data-ttu-id="3a443-141">Klicken Sie in der vorherigen Dateipfade, ersetzen Sie `<user_secrets_id>` mit der `UserSecretsId` Wert in der *csproj* Datei.</span><span class="sxs-lookup"><span data-stu-id="3a443-141">In the preceding file paths, replace `<user_secrets_id>` with the `UserSecretsId` value specified in the *.csproj* file.</span></span>

<span data-ttu-id="3a443-142">Schreiben Sie Code, von denen abhängig von der Speicherort oder das Format der Daten gespeichert werden, mit dem Geheimnis-Manager-Tool nicht.</span><span class="sxs-lookup"><span data-stu-id="3a443-142">Don't write code that depends on the location or format of data saved with the Secret Manager tool.</span></span> <span data-ttu-id="3a443-143">Details dieser Implementierung können sich ändern.</span><span class="sxs-lookup"><span data-stu-id="3a443-143">These implementation details may change.</span></span> <span data-ttu-id="3a443-144">Z. B. die geheimen Werte werden nicht verschlüsselt, aber konnte nicht in der Zukunft.</span><span class="sxs-lookup"><span data-stu-id="3a443-144">For example, the secret values aren't encrypted, but could be in the future.</span></span>

::: moniker range="<= aspnetcore-2.0"

## <a name="install-the-secret-manager-tool"></a><span data-ttu-id="3a443-145">Installieren Sie das Geheimnis-Manager-tool</span><span class="sxs-lookup"><span data-stu-id="3a443-145">Install the Secret Manager tool</span></span>

<span data-ttu-id="3a443-146">Secret Manager-Tool ist im Paket mit .NET Core-CLI in .NET Core SDK 2.1.300 oder höher.</span><span class="sxs-lookup"><span data-stu-id="3a443-146">The Secret Manager tool is bundled with the .NET Core CLI in .NET Core SDK 2.1.300 or later.</span></span> <span data-ttu-id="3a443-147">Für .NET Core SDK-Versionen vor 2.1.300 ist ein Tool-Installationsordner erforderlich.</span><span class="sxs-lookup"><span data-stu-id="3a443-147">For .NET Core SDK versions before 2.1.300, tool installation is necessary.</span></span>

> [!TIP]
> <span data-ttu-id="3a443-148">Führen Sie `dotnet --version` über eine Befehlsshell, die Anzahl der installierten .NET Core SDK-Version finden Sie unter.</span><span class="sxs-lookup"><span data-stu-id="3a443-148">Run `dotnet --version` from a command shell to see the installed .NET Core SDK version number.</span></span>

<span data-ttu-id="3a443-149">Wenn das .NET Core SDK verwendet das Tool enthält, wird eine Warnung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="3a443-149">A warning is displayed if the .NET Core SDK being used includes the tool:</span></span>

```console
The tool 'Microsoft.Extensions.SecretManager.Tools' is now included in the .NET Core SDK. Information on resolving this warning is available at (https://aka.ms/dotnetclitools-in-box).
```

<span data-ttu-id="3a443-150">Installieren Sie die [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet-Paket in Ihre ASP.NET Core-Projekt.</span><span class="sxs-lookup"><span data-stu-id="3a443-150">Install the [Microsoft.Extensions.SecretManager.Tools](https://www.nuget.org/packages/Microsoft.Extensions.SecretManager.Tools/) NuGet package in your ASP.NET Core project.</span></span> <span data-ttu-id="3a443-151">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3a443-151">For example:</span></span>

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_CsprojFile&highlight=15-16)]

<span data-ttu-id="3a443-152">Führen Sie den folgenden Befehl in einer Befehlsshell zum Überprüfen der Tool-Installationsordner:</span><span class="sxs-lookup"><span data-stu-id="3a443-152">Execute the following command in a command shell to validate the tool installation:</span></span>

```console
dotnet user-secrets -h
```

<span data-ttu-id="3a443-153">Secret Manager-Tool zeigt das Beispiel für die Verwendung, Optionen und Hilfe zu dem Befehl:</span><span class="sxs-lookup"><span data-stu-id="3a443-153">The Secret Manager tool displays sample usage, options, and command help:</span></span>

```console
Usage: dotnet user-secrets [options] [command]

Options:
  -?|-h|--help                        Show help information
  --version                           Show version information
  -v|--verbose                        Show verbose output
  -p|--project <PROJECT>              Path to project. Defaults to searching the current directory.
  -c|--configuration <CONFIGURATION>  The project configuration to use. Defaults to 'Debug'.
  --id                                The user secret ID to use.

Commands:
  clear   Deletes all the application secrets
  list    Lists all the application secrets
  remove  Removes the specified user secret
  set     Sets the user secret to the specified value

Use "dotnet user-secrets [command] --help" for more information about a command.
```

> [!NOTE]
> <span data-ttu-id="3a443-154">Müssen Sie sich im selben Verzeichnis wie die *csproj* Datei ist zum Ausführen des Tools, die definiert, der *csproj* Datei `DotNetCliToolReference` Elemente.</span><span class="sxs-lookup"><span data-stu-id="3a443-154">You must be in the same directory as the *.csproj* file to run tools defined in the *.csproj* file's `DotNetCliToolReference` elements.</span></span>

::: moniker-end

## <a name="set-a-secret"></a><span data-ttu-id="3a443-155">Legen Sie einen geheimen Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3a443-155">Set a secret</span></span>

<span data-ttu-id="3a443-156">Secret Manager-Tool wirkt sich auf projektspezifische Konfigurationseinstellungen, die in Ihrem Benutzerprofil gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3a443-156">The Secret Manager tool operates on project-specific configuration settings stored in your user profile.</span></span> <span data-ttu-id="3a443-157">Um vertrauliche Informationen eines Benutzers zu verwenden, definieren eine `UserSecretsId` Element innerhalb einer `PropertyGroup` von der *csproj* Datei.</span><span class="sxs-lookup"><span data-stu-id="3a443-157">To use user secrets, define a `UserSecretsId` element within a `PropertyGroup` of the *.csproj* file.</span></span> <span data-ttu-id="3a443-158">Der Wert des `UserSecretsId` ist beliebig, aber in dem Projekt eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="3a443-158">The value of `UserSecretsId` is arbitrary, but is unique to the project.</span></span> <span data-ttu-id="3a443-159">Entwickler in der Regel generiert eine GUID für die `UserSecretsId`.</span><span class="sxs-lookup"><span data-stu-id="3a443-159">Developers typically generate a GUID for the `UserSecretsId`.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](app-secrets/samples/2.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](app-secrets/samples/1.x/UserSecrets/UserSecrets.csproj?name=snippet_PropertyGroup&highlight=3)]

::: moniker-end

> [!TIP]
> <span data-ttu-id="3a443-160">Klicken Sie in Visual Studio mit der rechten Maustaste in des Projekts im Projektmappen-Explorer, und wählen **geheime Benutzerschlüssel verwalten** aus dem Kontextmenü.</span><span class="sxs-lookup"><span data-stu-id="3a443-160">In Visual Studio, right-click the project in Solution Explorer, and select **Manage User Secrets** from the context menu.</span></span> <span data-ttu-id="3a443-161">Diese stiftbewegung Fügt eine `UserSecretsId` Elements aufgefüllt durch eine GUID, zu der *csproj* Datei.</span><span class="sxs-lookup"><span data-stu-id="3a443-161">This gesture adds a `UserSecretsId` element, populated with a GUID, to the *.csproj* file.</span></span> <span data-ttu-id="3a443-162">Visual Studio öffnet eine *secrets.json* Datei im Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="3a443-162">Visual Studio opens a *secrets.json* file in the text editor.</span></span> <span data-ttu-id="3a443-163">Ersetzen Sie den Inhalt der *secrets.json* mit Schlüssel-Wert-Paare gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-163">Replace the contents of *secrets.json* with the key-value pairs to be stored.</span></span> <span data-ttu-id="3a443-164">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3a443-164">For example:</span></span>
> ```json
> {
>   "Movies": {
>     "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true",
>     "ServiceApiKey": "12345"
>   }
> }
> ```
> <span data-ttu-id="3a443-165">Die JSON-Struktur wird nach Änderungen über vereinfacht `dotnet user-secrets remove` oder `dotnet user-secrets set`.</span><span class="sxs-lookup"><span data-stu-id="3a443-165">The JSON structure is flattened after modifications via `dotnet user-secrets remove` or `dotnet user-secrets set`.</span></span> <span data-ttu-id="3a443-166">Z. B. Ausführung `dotnet user-secrets remove "Movies:ConnectionString"` reduziert die `Movies` Objektliteral.</span><span class="sxs-lookup"><span data-stu-id="3a443-166">For example, running `dotnet user-secrets remove "Movies:ConnectionString"` collapses the `Movies` object literal.</span></span> <span data-ttu-id="3a443-167">Die geänderte Datei ähnelt der folgenden:</span><span class="sxs-lookup"><span data-stu-id="3a443-167">The modified file resembles the following:</span></span>
> ```json
> {
>   "Movies:ServiceApiKey": "12345"
> }
> ```

<span data-ttu-id="3a443-168">Definieren Sie ein app-Geheimnis, bestehend aus einem Schlüssel und seinen Wert an.</span><span class="sxs-lookup"><span data-stu-id="3a443-168">Define an app secret consisting of a key and its value.</span></span> <span data-ttu-id="3a443-169">Der geheime Schlüssel des Projekts zugeordnet ist `UserSecretsId` Wert.</span><span class="sxs-lookup"><span data-stu-id="3a443-169">The secret is associated with the project's `UserSecretsId` value.</span></span> <span data-ttu-id="3a443-170">Führen Sie beispielsweise den folgenden Befehl aus dem Verzeichnis, in dem die *csproj* Datei vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="3a443-170">For example, run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```

<span data-ttu-id="3a443-171">Im vorherigen Beispiel ist der Doppelpunkt bedeutet, dass `Movies` ist ein Objekt als literal mit einem `ServiceApiKey` Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="3a443-171">In the preceding example, the colon denotes that `Movies` is an object literal with a `ServiceApiKey` property.</span></span>

<span data-ttu-id="3a443-172">Secret Manager-Tool kann auch aus anderen Verzeichnissen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-172">The Secret Manager tool can be used from other directories too.</span></span> <span data-ttu-id="3a443-173">Verwenden der `--project` Option aus, um den Dateisystempfad an dem Angeben der *csproj* Datei vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="3a443-173">Use the `--project` option to supply the file system path at which the *.csproj* file exists.</span></span> <span data-ttu-id="3a443-174">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3a443-174">For example:</span></span>

```console
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```

## <a name="set-multiple-secrets"></a><span data-ttu-id="3a443-175">Legen Sie mehrere geheime Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3a443-175">Set multiple secrets</span></span>

<span data-ttu-id="3a443-176">Ein Batch von geheimen Schlüsseln kann festgelegt werden, durch das Weiterleiten von JSON-Code für die `set` Befehl.</span><span class="sxs-lookup"><span data-stu-id="3a443-176">A batch of secrets can be set by piping JSON to the `set` command.</span></span> <span data-ttu-id="3a443-177">Im folgenden Beispiel die *"Input.JSON"* Dateiinhalt sind über die Pipeline an das `set` Befehl.</span><span class="sxs-lookup"><span data-stu-id="3a443-177">In the following example, the *input.json* file's contents are piped to the `set` command.</span></span>

# <a name="windowstabwindows"></a>[<span data-ttu-id="3a443-178">Windows</span><span class="sxs-lookup"><span data-stu-id="3a443-178">Windows</span></span>](#tab/windows)

<span data-ttu-id="3a443-179">Öffnen Sie eine Befehlsshell, und führen Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="3a443-179">Open a command shell, and execute the following command:</span></span>

  ```console
  type .\input.json | dotnet user-secrets set
  ```

# <a name="macostabmacos"></a>[<span data-ttu-id="3a443-180">macOS</span><span class="sxs-lookup"><span data-stu-id="3a443-180">macOS</span></span>](#tab/macos)

<span data-ttu-id="3a443-181">Öffnen Sie eine Befehlsshell, und führen Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="3a443-181">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

# <a name="linuxtablinux"></a>[<span data-ttu-id="3a443-182">Linux</span><span class="sxs-lookup"><span data-stu-id="3a443-182">Linux</span></span>](#tab/linux)

<span data-ttu-id="3a443-183">Öffnen Sie eine Befehlsshell, und führen Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="3a443-183">Open a command shell, and execute the following command:</span></span>

  ```console
  cat ./input.json | dotnet user-secrets set
  ```

---

## <a name="access-a-secret"></a><span data-ttu-id="3a443-184">Zugriff auf einen geheimen Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3a443-184">Access a secret</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="3a443-185">Die [ASP.NET Core-Konfigurations-API](xref:fundamentals/configuration/index) ermöglicht den Zugriff auf Secret Manager Geheimnisse.</span><span class="sxs-lookup"><span data-stu-id="3a443-185">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="3a443-186">Wenn das Projekt .NET Framework verwendet, installieren Sie die [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="3a443-186">If your project targets the .NET Framework, install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="3a443-187">In ASP.NET Core 2.0 oder höher, die Benutzer Geheimnisse Konfigurationsquelle wird automatisch hinzugefügt im Entwicklungsmodus Wenn, das Projekt aufruft <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> eine neue Instanz des Hosts mit vorkonfigurierten Standardwerten initialisiert werden.</span><span class="sxs-lookup"><span data-stu-id="3a443-187">In ASP.NET Core 2.0 or later, the user secrets configuration source is automatically added in development mode when the project calls <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> to initialize a new instance of the host with preconfigured defaults.</span></span> <span data-ttu-id="3a443-188">`CreateDefaultBuilder` Aufrufe <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> bei der <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName> ist <xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span><span class="sxs-lookup"><span data-stu-id="3a443-188">`CreateDefaultBuilder` calls <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> when the <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName> is <xref:Microsoft.AspNetCore.Hosting.EnvironmentName.Development>:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Program.cs?name=snippet_CreateWebHostBuilder&highlight=2)]

<span data-ttu-id="3a443-189">Wenn `CreateDefaultBuilder` wird nicht aufgerufen wird, hinzufügen die Konfigurationsquelle für Benutzer Geheimnisse explizit durch den Aufruf <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> in die `Startup` Konstruktor.</span><span class="sxs-lookup"><span data-stu-id="3a443-189">When `CreateDefaultBuilder` isn't called, add the user secrets configuration source explicitly by calling <xref:Microsoft.Extensions.Configuration.UserSecretsConfigurationExtensions.AddUserSecrets*> in the `Startup` constructor.</span></span> <span data-ttu-id="3a443-190">Rufen Sie `AddUserSecrets` nur wenn die app in der Entwicklungsumgebung ausgeführt wird wie im folgenden Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="3a443-190">Call `AddUserSecrets` only when the app runs in the Development environment, as shown in the following example:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="3a443-191">Die [ASP.NET Core-Konfigurations-API](xref:fundamentals/configuration/index) ermöglicht den Zugriff auf Secret Manager Geheimnisse.</span><span class="sxs-lookup"><span data-stu-id="3a443-191">The [ASP.NET Core Configuration API](xref:fundamentals/configuration/index) provides access to Secret Manager secrets.</span></span> <span data-ttu-id="3a443-192">Installieren Sie die [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="3a443-192">Install the [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) NuGet package.</span></span>

<span data-ttu-id="3a443-193">Hinzufügen die Konfigurationsquelle für Benutzer geheime Schlüssel mit einem Aufruf von [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in die `Startup` Konstruktor:</span><span class="sxs-lookup"><span data-stu-id="3a443-193">Add the user secrets configuration source with a call to [AddUserSecrets](/dotnet/api/microsoft.extensions.configuration.usersecretsconfigurationextensions.addusersecrets) in the `Startup` constructor:</span></span>

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupConstructor&highlight=12)]

::: moniker-end

<span data-ttu-id="3a443-194">Vertrauliche Informationen eines Benutzers abgerufen werden können, über die `Configuration` API:</span><span class="sxs-lookup"><span data-stu-id="3a443-194">User secrets can be retrieved via the `Configuration` API:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=14)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup.cs?name=snippet_StartupClass&highlight=26)]

::: moniker-end

## <a name="map-secrets-to-a-poco"></a><span data-ttu-id="3a443-195">Map-Geheimtipps für die ein POCO-Objekt</span><span class="sxs-lookup"><span data-stu-id="3a443-195">Map secrets to a POCO</span></span>

<span data-ttu-id="3a443-196">Zuordnen eines kompletten Objekts literal, ein POCO-Objekt (eine einfache .NET Klasse mit Eigenschaften) eignet sich für das Aggregieren von verwandten Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="3a443-196">Mapping an entire object literal to a POCO (a simple .NET class with properties) is useful for aggregating related properties.</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="3a443-197">Verwenden, um die vorherigen geheimen Schlüssel ein POCO-Objekt zugeordnet sind, die `Configuration` APIs [Objekt Graph Bindung](xref:fundamentals/configuration/index#bind-to-an-object-graph) Feature.</span><span class="sxs-lookup"><span data-stu-id="3a443-197">To map the preceding secrets to a POCO, use the `Configuration` API's [object graph binding](xref:fundamentals/configuration/index#bind-to-an-object-graph) feature.</span></span> <span data-ttu-id="3a443-198">Der folgende Code bindet an einen benutzerdefinierten `MovieSettings` POCO und greift auf die `ServiceApiKey` Eigenschaftswert:</span><span class="sxs-lookup"><span data-stu-id="3a443-198">The following code binds to a custom `MovieSettings` POCO and accesses the `ServiceApiKey` property value:</span></span>

::: moniker range=">= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

::: moniker range="= aspnetcore-1.0"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup3.cs?name=snippet_BindToObjectGraph)]

::: moniker-end

<span data-ttu-id="3a443-199">Die `Movies:ConnectionString` und `Movies:ServiceApiKey` geheime Schlüssel werden in den entsprechenden Eigenschaften im zugeordnet `MovieSettings`:</span><span class="sxs-lookup"><span data-stu-id="3a443-199">The `Movies:ConnectionString` and `Movies:ServiceApiKey` secrets are mapped to the respective properties in `MovieSettings`:</span></span>

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Models/MovieSettings.cs?name=snippet_MovieSettingsClass)]

## <a name="string-replacement-with-secrets"></a><span data-ttu-id="3a443-200">Zeichenfolgenersetzungen mit geheimen Schlüsseln</span><span class="sxs-lookup"><span data-stu-id="3a443-200">String replacement with secrets</span></span>

<span data-ttu-id="3a443-201">Speichern von Kennwörtern als nur-Text ist unsicher.</span><span class="sxs-lookup"><span data-stu-id="3a443-201">Storing passwords in plain text is insecure.</span></span> <span data-ttu-id="3a443-202">Z. B. eine Datenbankverbindungszeichenfolge, die in gespeicherten *"appSettings.JSON"* kann ein Kennwort für den angegebenen Benutzer enthalten:</span><span class="sxs-lookup"><span data-stu-id="3a443-202">For example, a database connection string stored in *appsettings.json* may include a password for the specified user:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings-unsecure.json?highlight=3)]

<span data-ttu-id="3a443-203">Ein sicherer Ansatz ist das Kennwort als Geheimnis gespeichert.</span><span class="sxs-lookup"><span data-stu-id="3a443-203">A more secure approach is to store the password as a secret.</span></span> <span data-ttu-id="3a443-204">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3a443-204">For example:</span></span>

```console
dotnet user-secrets set "DbPassword" "pass123"
```

<span data-ttu-id="3a443-205">Entfernen Sie die `Password` Schlüssel / Wert-Paar aus der Verbindungszeichenfolge in *"appSettings.JSON"*.</span><span class="sxs-lookup"><span data-stu-id="3a443-205">Remove the `Password` key-value pair from the connection string in *appsettings.json*.</span></span> <span data-ttu-id="3a443-206">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3a443-206">For example:</span></span>

[!code-json[](app-secrets/samples/2.x/UserSecrets/appsettings.json?highlight=3)]

<span data-ttu-id="3a443-207">Der geheime Schlüssel Wert kann festgelegt werden, auf eine [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) des Objekts [Kennwort](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) Eigenschaft, um die Verbindungszeichenfolge abgeschlossen:</span><span class="sxs-lookup"><span data-stu-id="3a443-207">The secret's value can be set on a [SqlConnectionStringBuilder](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder) object's [Password](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.password) property to complete the connection string:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](app-secrets/samples/2.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=14-17)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](app-secrets/samples/1.x/UserSecrets/Startup2.cs?name=snippet_StartupClass&highlight=26-29)]

::: moniker-end

## <a name="list-the-secrets"></a><span data-ttu-id="3a443-208">Auflisten der Geheimnisse.</span><span class="sxs-lookup"><span data-stu-id="3a443-208">List the secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="3a443-209">Führen den folgenden Befehl aus dem Verzeichnis, in dem die *csproj* Datei vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="3a443-209">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets list
```

<span data-ttu-id="3a443-210">Die folgende Ausgabe wird angezeigt:</span><span class="sxs-lookup"><span data-stu-id="3a443-210">The following output appears:</span></span>

```console
Movies:ConnectionString = Server=(localdb)\mssqllocaldb;Database=Movie-1;Trusted_Connection=True;MultipleActiveResultSets=true
Movies:ServiceApiKey = 12345
```

<span data-ttu-id="3a443-211">Im vorherigen Beispiel, bezeichnet ein Doppelpunkt in den Schlüsselnamen die Objekthierarchie in *secrets.json*.</span><span class="sxs-lookup"><span data-stu-id="3a443-211">In the preceding example, a colon in the key names denotes the object hierarchy within *secrets.json*.</span></span>

## <a name="remove-a-single-secret"></a><span data-ttu-id="3a443-212">Entfernen Sie einen einzelnen geheimen Schlüssel</span><span class="sxs-lookup"><span data-stu-id="3a443-212">Remove a single secret</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="3a443-213">Führen den folgenden Befehl aus dem Verzeichnis, in dem die *csproj* Datei vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="3a443-213">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets remove "Movies:ConnectionString"
```

<span data-ttu-id="3a443-214">Der app *secrets.json* Datei wurde geändert, um das zugeordnete Schlüssel-Wert-Paar Entfernen der `MoviesConnectionString` Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="3a443-214">The app's *secrets.json* file was modified to remove the key-value pair associated with the `MoviesConnectionString` key:</span></span>

```json
{
  "Movies": {
    "ServiceApiKey": "12345"
  }
}
```

<span data-ttu-id="3a443-215">Ausführung `dotnet user-secrets list` wird die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="3a443-215">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
Movies:ServiceApiKey = 12345
```

## <a name="remove-all-secrets"></a><span data-ttu-id="3a443-216">Entfernen Sie alle Geheimnisse</span><span class="sxs-lookup"><span data-stu-id="3a443-216">Remove all secrets</span></span>

[!INCLUDE[secrets.json file](~/includes/app-secrets/secrets-json-file-and-text.md)]

<span data-ttu-id="3a443-217">Führen den folgenden Befehl aus dem Verzeichnis, in dem die *csproj* Datei vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="3a443-217">Run the following command from the directory in which the *.csproj* file exists:</span></span>

```console
dotnet user-secrets clear
```

<span data-ttu-id="3a443-218">Alle benutzergeheimnisse für die app aus gelöscht wurden die *secrets.json* Datei:</span><span class="sxs-lookup"><span data-stu-id="3a443-218">All user secrets for the app have been deleted from the *secrets.json* file:</span></span>

```json
{}
```

<span data-ttu-id="3a443-219">Ausführung `dotnet user-secrets list` wird die folgende Meldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="3a443-219">Running `dotnet user-secrets list` displays the following message:</span></span>

```console
No secrets configured for this application.
```

## <a name="additional-resources"></a><span data-ttu-id="3a443-220">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3a443-220">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* <xref:security/key-vault-configuration>
