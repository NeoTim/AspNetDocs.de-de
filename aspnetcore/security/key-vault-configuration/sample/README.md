---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045587"
---
# <a name="key-vault-configuration-provider-sample-app"></a>Key Vault-Instanz Configuration Provider-Beispiel-App

Dieses Beispiel veranschaulicht die Verwendung von Azure Key Vault-Konfigurationsanbieter.

Das Beispiel ausgeführt wird, in einem von zwei Modi, die bestimmt, indem die `#define` Anweisung am Anfang der *"Program.cs"* Datei. Anweisungen hierzu finden Sie unter [Präprozessordirektiven im Beispielcode](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):

* `Basic` &ndash; Veranschaulicht die Verwendung einer Azure Key Vault-Client-ID und geheimen Schlüssel auf Access-Geheimnisse in Azure Key Vault gespeichert. Diese Version des Beispiels kann von jedem Standort und Azure App Service oder einem beliebigen Host können ASP.NET Core-Apps bereitgestellt, ausgeführt werden.
* `Managed` &ndash; Veranschaulicht, wie der Azure [verwaltete Dienstidentitäten](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) zum Authentifizieren der app in Azure Key Vault mit Azure AD-Authentifizierung ohne Anmeldeinformationen in der app Code oder Konfiguration. Eine Azure AD-Client-ID und geheimen Schlüssel nicht für die app für die Authentifizierung mit Azure Key Vault erforderlich. In diesem Beispiel muss in Azure App Service zum Untersuchen der verwalteten Dienstidentität Scearnio bereitgestellt werden.

Weitere Informationen finden Sie unter [Azure Key Vault-Konfigurationsanbieter](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration).
