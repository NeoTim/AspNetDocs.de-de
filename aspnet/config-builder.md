---
uid: config-builder
title: Konfigurations-Generatoren für ASP.NET
author: rick-anderson
description: Erfahren Sie, wie Sie Konfigurationsdaten aus anderen Quellen als web.config Werten aus externen Quellen erhalten.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424801"
---
# <a name="configuration-builders-for-aspnet"></a>Konfigurations-Generatoren für ASP.NET

Von [Stephen Molloy](https://github.com/StephenMolloy) und [Rick Anderson](https://twitter.com/RickAndMSFT)

Konfigurations-Generatoren stellen einen modernen und agilen Mechanismus für ASP.net-apps bereit, um Konfigurationswerte aus externen Quellen zu erhalten.

Konfigurations-Generatoren:

* Sind in .NET Framework 4.7.1 und höher verfügbar.
* Stellen Sie einen flexiblen Mechanismus zum Lesen von Konfigurations Werten bereit.
* Berücksichtigen Sie einige der grundlegenden Anforderungen von apps, die in einen Container und eine in der Cloud fokussierte Umgebung verschoben werden.
* Kann verwendet werden, um den Schutz von Konfigurationsdaten durch das Zeichnen aus Quellen zu verbessern, die zuvor nicht verfügbar waren (z. b. Azure Key Vault und Umgebungsvariablen) im .NET-Konfigurationssystem.

## <a name="keyvalue-configuration-builders"></a>Schlüssel-Wert-Konfigurations-Generatoren

Ein häufiges Szenario, das von Configuration Builder behandelt werden kann, ist die Bereitstellung eines grundlegenden Schlüssel-Wert-ersatzmechanismus für Konfigurations Abschnitte, die einem Schlüssel-Wert-Muster folgen. Das .NET Framework Konzept von configurationbuilder ist nicht auf bestimmte Konfigurations Abschnitte oder Muster beschränkt. Viele der Konfigurations-Generatoren in `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [nuget](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) funktionieren jedoch innerhalb des Schlüssel-Wert-Musters.

## <a name="keyvalue-configuration-builders-settings"></a>Einstellungen für die Schlüssel-/wertkonfigurationsbuilder

Die folgenden Einstellungen gelten für alle Schlüssel-Wert-Konfigurations-Generatoren in `Microsoft.Configuration.ConfigurationBuilders` .

### <a name="mode"></a>Mode

Die Konfigurations-Generatoren verwenden eine externe Quelle von Schlüssel-Wert-Informationen, um die ausgewählten Schlüssel-Wert-Elemente des Konfigurations Systems aufzufüllen. Insbesondere die `<appSettings/>` Abschnitte und `<connectionStrings/>` erhalten eine spezielle Behandlung der Configuration Builder. Die Generatoren funktionieren in drei Modi:

* `Strict`: Der Standardmodus. In diesem Modus arbeitet der Konfigurations-Generator nur mit bekannten Schlüssel/Wert-zentrierten Konfigurations Abschnitten. `Strict`-Modus Listet jeden Schlüssel im-Abschnitt auf. Wenn ein übereinstimmender Schlüssel in der externen Quelle gefunden wird:

   * Die Konfigurations-Generatoren ersetzen den Wert im resultierenden Konfigurations Abschnitt durch den Wert aus der externen Quelle.
* `Greedy`-Dieser Modus ist eng mit dem- `Strict` Modus verknüpft. Anstatt auf Schlüssel beschränkt zu sein, die in der ursprünglichen Konfiguration bereits vorhanden sind:

  * Die Konfigurations-Generatoren fügen alle Schlüssel-Wert-Paare aus der externen Quelle dem sich ergebenden Konfigurations Abschnitt hinzu.

* `Expand`: Verarbeitet den unformatierten XML-Code, bevor er in ein Konfigurations Abschnitts Objekt analysiert wird. Dies kann sich als Erweiterung von Token in einer Zeichenfolge vorstellen. Jeder Teil der unformatierten XML-Zeichenfolge, die dem Muster entspricht, `${token}` ist ein Kandidat für die Tokenerweiterung. Wenn kein entsprechender Wert in der externen Quelle gefunden wird, wird das Token nicht geändert. Generatoren in diesem Modus sind nicht auf die `<appSettings/>` Abschnitte und beschränkt `<connectionStrings/>` .

Das folgende Markup von *web.config* aktiviert die [Umgebungs](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) -Generator im- `Strict` Modus:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

Der folgende Code liest `<appSettings/>` und `<connectionStrings/>` in der vorherigen *web.config* Datei:

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

Im vorangehenden Code werden die Eigenschaftswerte auf festgelegt:

* Die Werte in der *web.config* -Datei, wenn die Schlüssel nicht in Umgebungsvariablen festgelegt sind.
* Die Werte der Umgebungsvariablen, sofern festgelegt.

Enthält beispielsweise Folgendes `ServiceID` :

* "Serviceid Wert from web.config", wenn die Umgebungsvariable `ServiceID` nicht festgelegt ist.
* Der Wert der `ServiceID` Umgebungsvariablen, sofern festgelegt.

In der folgenden Abbildung werden die `<appSettings/>` Schlüssel/Werte aus dem vorherigen *web.config* Datei Satz im Umgebungs-Editor angezeigt:

![Umgebungs-Editor](config-builder/static/env.png)

Hinweis: möglicherweise müssen Sie Visual Studio beenden und neu starten, um Änderungen in Umgebungsvariablen anzuzeigen.

### <a name="prefix-handling"></a>Präfix Behandlung

Wichtige Präfixe können das Festlegen von Schlüsseln vereinfachen:

* Die .NET Framework Konfiguration ist komplex und wird nicht eingefügt.
* Externe Schlüssel-/Wertquellen sind im allgemeinen grundlegend und flach. Umgebungsvariablen sind z. b. nicht vollständig.

Verwenden Sie einen der folgenden Ansätze, um sowohl in `<appSettings/>` als auch `<connectionStrings/>` in die Konfiguration über Umgebungsvariablen einzufügen:

* Mit dem `EnvironmentConfigBuilder` im Standard `Strict` Modus und den entsprechenden Schlüsselnamen in der Konfigurationsdatei. Der vorangehende Code und das Markup haben diese Vorgehensweise. Wenn Sie diesen Ansatz verwenden, können Sie in und **nicht** identisch benannte Schlüssel verwenden `<appSettings/>` `<connectionStrings/>` .
* Verwenden Sie zwei `EnvironmentConfigBuilder` s im `Greedy` -Modus mit unterschiedlichen Präfixen und `stripPrefix` . Bei diesem Ansatz kann die APP Lesen `<appSettings/>` und `<connectionStrings/>` ohne die Konfigurationsdatei aktualisieren zu müssen. Der nächste Abschnitt, [stripprefix](#stripprefix), zeigt, wie dies geschieht.
* Verwenden Sie zwei `EnvironmentConfigBuilder` s im- `Greedy` Modus mit unterschiedlichen Präfixen. Bei dieser Vorgehensweise können keine doppelten Schlüsselnamen vorhanden sein, da Schlüsselnamen sich durch das Präfix unterscheiden müssen.  Beispiel:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

Mit dem vorangehenden Markup kann die gleiche flatkey/Value-Quelle verwendet werden, um die Konfiguration für zwei verschiedene Abschnitte aufzufüllen.

Die folgende Abbildung zeigt die `<appSettings/>` -und `<connectionStrings/>` -Schlüssel/-Werte aus dem vorherigen *web.config* Datei Satz im Umgebungs-Editor:

![Umgebungs-Editor](config-builder/static/prefix.png)

Der folgende Code liest die `<appSettings/>` `<connectionStrings/>` Schlüssel/Werte und, die in der vorherigen *web.config* Datei enthalten sind:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

Im vorangehenden Code werden die Eigenschaftswerte auf festgelegt:

* Die Werte in der *web.config* -Datei, wenn die Schlüssel nicht in Umgebungsvariablen festgelegt sind.
* Die Werte der Umgebungsvariablen, sofern festgelegt.

Beispielsweise werden die folgenden Werte festgelegt, indem Sie die vorherige *web.config* Datei, die Schlüssel/Werte in der vorherigen Abbildung des Umgebungs-Editors und den vorherigen Code verwenden:

|  Schlüssel              | Wert |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | AppSetting_ServiceID von "dev"-Variablen|
|    AppSetting_default            | AppSetting_default Wert aus der enumerationsdatei |
|       ConnStr_default         | ConnStr_default Val von der Gesamt Version|

### <a name="stripprefix"></a>stripprefix

`stripPrefix`: Boolescher Wert, der Standardwert ist `false` . 

Das vorangehende XML-Markup trennt App-Einstellungen von Verbindungs Zeichenfolgen, erfordert jedoch, dass alle Schlüssel in der *web.config* -Datei das angegebene Präfix verwenden. Beispielsweise muss das Präfix `AppSetting` dem `ServiceID` Schlüssel ("AppSetting_ServiceID") hinzugefügt werden. Mit `stripPrefix` wird das Präfix nicht in der *web.config* Datei verwendet. Das Präfix ist in der Configuration Builder-Quelle erforderlich (z. b. in der-Umgebung). Wir erwarten, dass die meisten Entwickler verwenden werden `stripPrefix` .

Anwendungen entfernen in der Regel das Präfix. Im folgenden *web.config* wird das Präfix entfernt:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

In der vorangehenden *web.config* Datei befindet sich der `default` Schlüssel sowohl in `<appSettings/>` als auch in `<connectionStrings/>` .

Die folgende Abbildung zeigt die `<appSettings/>` -und `<connectionStrings/>` -Schlüssel/-Werte aus dem vorherigen *web.config* Datei Satz im Umgebungs-Editor:

![Umgebungs-Editor](config-builder/static/prefix.png)

Der folgende Code liest die `<appSettings/>` `<connectionStrings/>` Schlüssel/Werte und, die in der vorherigen *web.config* Datei enthalten sind:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

Im vorangehenden Code werden die Eigenschaftswerte auf festgelegt:

* Die Werte in der *web.config* -Datei, wenn die Schlüssel nicht in Umgebungsvariablen festgelegt sind.
* Die Werte der Umgebungsvariablen, sofern festgelegt.

Beispielsweise werden die folgenden Werte festgelegt, indem Sie die vorherige *web.config* Datei, die Schlüssel/Werte in der vorherigen Abbildung des Umgebungs-Editors und den vorherigen Code verwenden:

|  Schlüssel              | Wert |
| ----------------- | ------------ |
|     ServiceID           | AppSetting_ServiceID von "dev"-Variablen|
|    default            | AppSetting_default Wert aus der enumerationsdatei |
|    default         | ConnStr_default Val von der Gesamt Version|

### <a name="tokenpattern"></a>tokenpattern

`tokenPattern`: String, Standardwert`@"\$\{(\w+)\}"`

Das `Expand` Verhalten der Generatoren durchsucht die unformatierten XML-Daten nach Token, die wie aussehen `${token}` . Die Suche erfolgt mit dem regulären Standardausdruck `@"\$\{(\w+)\}"` . Der Satz von Zeichen, der entspricht, `\w` ist strenger als XML, und viele Konfigurations Quellen erlauben. Verwenden Sie, `tokenPattern` Wenn `@"\$\{(\w+)\}"` im Tokennamen mehr Zeichen als erforderlich sind.

`tokenPattern`Schnür

* Ermöglicht es Entwicklern, den Regex zu ändern, der für die Tokenübereinstimmung verwendet wird.
* Es wird keine Validierung durchgeführt, um sicherzustellen, dass es sich um einen wohlgeformten, nicht gefährlichen Regex handelt.
* Es muss eine Erfassungs Gruppe enthalten. Der gesamte regex muss mit dem gesamten Token identisch sein. Die erste Erfassung muss der Tokenname sein, der in der Konfigurations Quelle gesucht werden soll.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Configuration Builder in Microsoft.Configuration.Configurationbuilder

### <a name="environmentconfigbuilder"></a>Umgebungs-Generator

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[Umgebungs](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)Konfigurations Generator:

* Ist die einfachste der Configuration Builder.
* Liest Werte aus der Umgebung.
* Verfügt über keine zusätzlichen Konfigurationsoptionen.
* Der `name` Attribut Wert ist willkürlich.

**Hinweis:** In einer Windows-Container Umgebung werden Variablen, die zur Laufzeit festgelegt werden, nur in die EntryPoint-Prozessumgebung eingefügt. Apps, die als Dienst oder Non-EntryPoint-Prozess ausgeführt werden, nehmen diese Variablen nur dann entgegen, wenn Sie anderweitig über einen Mechanismus im Container eingefügt werden. Bei [IIS](https://github.com/Microsoft/iis-docker/pull/41) / -[ASP.net](https://github.com/Microsoft/aspnet-docker)-basierten Containern behandelt die aktuelle Version von [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) diese nur im *DefaultAppPool* . Andere Windows-basierte containervarianten müssen möglicherweise Ihren eigenen einschleusungs Mechanismus für nicht-EntryPoint-Prozesse entwickeln.

### <a name="usersecretsconfigbuilder"></a>Usersecreungsconfigbuilder

> [!WARNING]
> Speichern Sie niemals Kenn Wörter, sensible Verbindungs Zeichenfolgen oder andere sensible Daten im Quellcode. Produktionsgeheimnisse sollten nicht für Entwicklungs-oder Testzwecke verwendet werden.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

Dieser Konfigurations-Generator stellt eine ähnliche Funktion wie [ASP.net Core Secret Manager](/aspnet/core/security/app-secrets)bereit.

[Usersecretyconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) kann in .NET Framework Projekten verwendet werden, aber es muss eine geheime Datei angegeben werden. Alternativ können Sie die `UserSecretsId` -Eigenschaft in der Projektdatei definieren und die Datei mit den unformatierten Geheimnissen am richtigen Speicherort für den Lesevorgang erstellen. Um externe Abhängigkeiten aus dem Projekt herauszuhalten, ist die geheime Datei XML-formatiert. Die XML-Formatierung ist ein Implementierungsdetail, und das Format sollte nicht verlassen werden. Wenn Sie einen *secrets.jsfür* die Datei mit .net Core-Projekten freigeben müssen, sollten Sie die Verwendung von [simplejsonconfigbuilder](#simplejsonconfigbuilder)in Erwägung gezogen. Das `SimpleJsonConfigBuilder` Format für .net Core sollte auch als Implementierungsdetails angesehen werden, die geändert werden können.

Konfigurations Attribute für `UserSecretsConfigBuilder` :

* `userSecretsId`: Dies ist die bevorzugte Methode zum Identifizieren einer XML-Geheimnis Datei. Es funktioniert ähnlich wie .net Core, das eine `UserSecretsId` Projekt Eigenschaft zum Speichern dieses Bezeichners verwendet. Die Zeichenfolge muss eindeutig sein, es muss sich nicht um eine GUID handeln. Mit diesem Attribut `UserSecretsConfigBuilder` Suchen Sie in einem bekannten lokalen Speicherort ( `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` ) nach einer Geheimnis Datei, die zu diesem Bezeichner gehört.
* `userSecretsFile`: Ein optionales Attribut, das die Datei mit den geheimen Schlüsseln angibt. Das `~` Zeichen kann am Anfang verwendet werden, um auf den Anwendungs Stamm zu verweisen. Entweder ist dieses Attribut oder das `userSecretsId` Attribut erforderlich. Wenn beide angegeben sind, hat `userSecretsFile` Vorrang.
* `optional`: Boolesch, Standardwert `true` -verhindert eine Ausnahme, wenn die geheime Datei nicht gefunden werden kann. 
* Der `name` Attribut Wert ist willkürlich.

Die Geheimnis Datei hat das folgende Format:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>Azurekeyvaultconfigbuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[Azurekeyvaultconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) liest Werte, die in der [Azure Key Vault](/azure/key-vault/key-vault-whatis)gespeichert sind.

`vaultName`ist erforderlich (entweder der Name des Tresors oder ein URI für den Tresor). Mit den anderen Attributen können Sie steuern, mit welchem Tresor eine Verbindung hergestellt werden soll. Dies ist jedoch nur erforderlich, wenn die Anwendung nicht in einer Umgebung ausgeführt wird, die mit funktioniert `Microsoft.Azure.Services.AppAuthentication` . Die Authentifizierungs Bibliothek für Azure-Dienste wird verwendet, um nach Möglichkeit automatisch Verbindungsinformationen aus der Ausführungsumgebung auszuwählen. Sie können die automatische Erfassung von Verbindungsinformationen überschreiben, indem Sie eine Verbindungs Zeichenfolge angeben.

* `vaultName`-Erforderlich, wenn `uri` nicht angegeben ist. Gibt den Namen des Tresors in Ihrem Azure-Abonnement an, aus dem Schlüssel-Wert-Paare gelesen werden sollen.
* `connectionString`-Eine Verbindungs Zeichenfolge, die von [azureservicestokenprovider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) verwendet werden kann
* `uri`: Stellt eine Verbindung mit anderen Key Vault Anbietern mit dem angegebenen `uri` Wert her. Wenn nicht angegeben, ist Azure ( `vaultName` ) der Tresor Anbieter.
* `version`-Azure Key Vault stellt eine Versionsverwaltung für Geheimnisse bereit. Wenn `version` angegeben wird, ruft der Generator nur die geheimen Schlüssel ab, die mit dieser Version übereinstimmen.
* `preloadSecretNames`-Standardmäßig fragt dieser Generator **alle** Schlüsselnamen im Schlüssel Tresor ab, wenn dieser initialisiert wird. Um zu verhindern, dass alle Schlüsselwerte gelesen werden, legen Sie dieses Attribut auf fest `false` . Wenn diese Einstellung auf festgelegt wird, werden die `false` geheimen Schlüssel einzeln gelesen. Das Lesen von geheimen Schlüsseln kann nützlich sein, wenn der Tresor den Zugriff auf "abrufen", aber nicht auf "auflisten" zulässt. **Hinweis:** Wenn der-Modus verwendet wird `Greedy` , `preloadSecretNames` muss `true` (der Standardwert) sein.

### <a name="keyperfileconfigbuilder"></a>Keyperfileconfigbuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) ist ein grundlegender Konfigurations-Generator, der die Dateien eines Verzeichnisses als Quelle von Werten verwendet. Der Name einer Datei ist der Schlüssel, und der Inhalt ist der Wert. Dieser Konfigurations-Generator kann nützlich sein, wenn er in einer orchestrierten Container Umgebung ausgeführt wird. Systeme wie docker Swarm und Kubernetes stellen `secrets` Ihre orchestrierten Windows-Container in dieser Schlüssel-pro-Datei-Weise bereit.

Attribut Details:

* `directoryPath` – Erforderlich. Gibt einen Pfad an, in dem nach Werten gesucht werden soll. Docker für Windows geheimen Schlüssel werden standardmäßig im Verzeichnis " *c:\programdata\docker\secrets* " gespeichert.
* `ignorePrefix`-Dateien, die mit diesem Präfix beginnen, werden ausgeschlossen. Der Standardwert ist „ignore“ (ignorieren).
* `keyDelimiter`-Der Standardwert ist `null` . Wenn dieser Wert angegeben ist, durchläuft der Konfigurations-Generator mehrere Ebenen des Verzeichnisses und erstellt Schlüsselnamen mit diesem Trennzeichen. Wenn dieser Wert ist `null` , untersucht der Konfigurations-Generator nur die oberste Verzeichnisebene.
* `optional`-Der Standardwert ist `false` . Gibt an, ob der Konfigurations-Generator Fehler verursachen soll, wenn das Quellverzeichnis nicht vorhanden ist.

### <a name="simplejsonconfigbuilder"></a>Simplejsonconfigbuilder

> [!WARNING]
> Speichern Sie niemals Kenn Wörter, sensible Verbindungs Zeichenfolgen oder andere sensible Daten im Quellcode. Produktionsgeheimnisse sollten nicht für Entwicklungs-oder Testzwecke verwendet werden.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.Net Core-Projekte verwenden häufig JSON-Dateien für die Konfiguration. Der [simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) -Generator ermöglicht die Verwendung von .net Core-JSON-Dateien in der .NET Framework. Dieser Konfigurations-Generator stellt eine einfache Zuordnung von einer flachen Schlüssel-/Wert-Quelle zu bestimmten Schlüssel-Wert-Bereichen .NET Framework Konfiguration bereit. Dieser Konfigurations-Generator bietet **keine** hierarchischen Konfigurationen. Die JSON-Unterstützungs Datei ähnelt einem Wörterbuch, nicht einem komplexen hierarchischen Objekt. Eine hierarchische Datei mit mehreren Ebenen kann verwendet werden. Dieser Anbieter gibt `flatten` die Tiefe an, indem er den Eigenschaftsnamen auf jeder Ebene mithilfe eines Trenn Zeichens anfügt `:` .

Attribut Details:

* `jsonFile` – Erforderlich. Gibt die JSON-Datei an, aus der gelesen werden soll. Das `~` Zeichen kann am Anfang verwendet werden, um auf den Stamm der APP zu verweisen.
* `optional`-Boolescher Wert, der Standardwert ist `true` . Verhindert das Auslösen von Ausnahmen, wenn die JSON-Datei nicht gefunden werden kann.
* `jsonMode` - `[Flat|Sectional]`. `Flat` ist die Standardoption. Wenn `jsonMode` `Flat` den Wert hat, ist die JSON-Datei eine einzelne flatkey/Wert-Quelle. `EnvironmentConfigBuilder`Und `AzureKeyVaultConfigBuilder` sind auch einzelne flatkey-Wert-Quellen. Wenn der `SimpleJsonConfigBuilder` im-Modus konfiguriert ist `Sectional` :

  * Die JSON-Datei wird konzeptionell direkt auf der obersten Ebene in mehrere Wörterbücher aufgeteilt.
  * Jedes der Wörterbücher wird nur auf den Konfigurations Abschnitt angewendet, der mit dem an Sie angefügten Eigenschaftsnamen der obersten Ebene übereinstimmt. Beispiel:

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>Configuration Builder-Reihenfolge

Weitere Informationen finden Sie im GitHub [-Repository ASPNET/microsoftconfigurationbuilder](https://github.com/aspnet/MicrosoftConfigurationBuilders) in der [configurationbuilder-Ausführungsreihenfolge](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) .

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>Implementieren eines benutzerdefinierten Schlüssel-Wert-Konfigurations-Generators

Wenn die Konfigurations-Generatoren Ihren Anforderungen nicht entsprechen, können Sie ein benutzerdefiniertes schreiben. Die `KeyValueConfigBuilder` Basisklasse behandelt Ersetzungs Modi und die meisten Präfix Probleme. Ein Implementierungsprojekt benötigt nur:

* Erben Sie von der Basisklasse, und implementieren Sie mithilfe von und eine grundlegende Quelle von Schlüssel-Wert-Paaren `GetValue` `GetAllValues` :
* Fügen Sie dem Projekt die [Microsoft.Configuration.Configurationbuilder. Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) hinzu.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

Die `KeyValueConfigBuilder` -Basisklasse stellt einen Großteil der Arbeit und das konsistente Verhalten für Schlüssel-Wert-Konfigurations-Generatoren bereit.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [GitHub-Repository für Konfigurations-Generatoren](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [Dienst-zu-Dienst-Authentifizierung in Azure Key Vault mithilfe von .NET](/azure/key-vault/service-to-service-authentication#connection-string-support)
