---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Profile, Designs und Webparts | Microsoft Docs
author: rick-anderson
description: In ASP.NET 2.0 gibt es wesentliche Änderungen in Der Konfiguration und Instrumentierung. Die neue ASP.NET Konfigurations-API ermöglicht Konfigurationsänderungen pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: 4bc98cca226a0bd9bd766a21e88b0facf2a4b610
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543638"
---
# <a name="profiles-themes-and-web-parts"></a>Profile, Designs und Webparts

von [Microsoft](https://github.com/microsoft)

> In ASP.NET 2.0 gibt es wesentliche Änderungen in Der Konfiguration und Instrumentierung. Die neue ASP.NET Konfigurations-API ermöglicht programmgesteuerte Konfigurationsänderungen. Darüber hinaus gibt es viele neue Konfigurationseinstellungen, die neue Konfigurationen und Instrumentierung ermöglichen.

ASP.NET 2.0 stellt eine wesentliche Verbesserung im Bereich der personalisierten Websites dar. Zusätzlich zu den bereits behandelten Mitgliedschaftsfeatures verbessern ASP.NET Profile, Designs und Webparts die Personalisierung von Websites erheblich.

## <a name="aspnet-profiles"></a>ASP.NET Profile

ASP.NET Profile ähneln Sitzungen. Der Unterschied besteht darin, dass ein Profil persistent ist, während eine Sitzung verloren geht, wenn der Browser geschlossen wird. Ein weiterer großer Unterschied zwischen Sitzungen und Profilen besteht darin, dass Profile stark typisiert sind, sodass Sie während des Entwicklungsprozesses intelliSense verfügen.

Ein Profil wird entweder in der Computerkonfigurationsdatei oder in der Datei web.config für die Anwendung definiert. (Sie können kein Profil in einer Unterordner-Datei web.config definieren.) Der folgende Code definiert ein Profil zum Speichern des Vor- und Nachnamens der Websitebesucher.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

Der Standarddatentyp für eine Profileigenschaft ist System.String. Im obigen Beispiel wurde kein Datentyp angegeben. Daher sind die Eigenschaften FirstName und LastName beide vom Typ String. Wie bereits erwähnt, sind Profileigenschaften stark typisiert. Der folgende Code fügt eine neue Eigenschaft für das Alter vom Typ Int32 hinzu.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Profile werden in der Regel bei der ASP.NET Forms-Authentifizierung verwendet. In Kombination mit der Formularauthentifizierung verfügt jeder Benutzer über ein separates Profil, das seiner Benutzer-ID zugeordnet ist. Es ist jedoch auch möglich, die Verwendung von Profilen in einer anonymen Anwendung mit dem &lt;anonymousIdentification-Element&gt; in der Konfigurationsdatei zusammen mit dem **allowAnonymous-Attribut** zuzulassen, wie unten gezeigt:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Wenn ein anonymer Benutzer die Website durchsucht, erstellt ASP.NET eine Instanz von **ProfileCommon** für den Benutzer. Dieses Profil verwendet eine eindeutige ID, die in einem Cookie im Browser gespeichert wird, um den Benutzer als eindeutigen Besucher zu identifizieren. Auf diese Weise können Sie Profilinformationen für Benutzer speichern, die anonym surfen.

## <a name="profile-groups"></a>Profilgruppen

Es ist möglich, Eigenschaften von Profilen zu gruppieren. Durch Gruppieren von Eigenschaften ist es möglich, mehrere Profile für eine bestimmte Anwendung zu simulieren.

Die folgende Konfiguration konfiguriert eine FirstName- und LastName-Eigenschaft für zwei Gruppen. Käufer und Interessenten.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Es ist dann möglich, Eigenschaften für eine bestimmte Gruppe wie folgt festzulegen:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Speichern komplexer Objekte

Bisher haben die von uns behandelten Beispiele einfache Datentypen in einem Profil gespeichert. Es ist auch möglich, komplexe Datentypen in einem Profil zu speichern, indem die Methode der Serialisierung mithilfe des **serializeAs-Attributs** wie folgt angegeben wird:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

In diesem Fall lautet der Typ PurchaseInvoice. Die PurchaseInvoice-Klasse muss als serialisierbar markiert werden und kann eine beliebige Anzahl von Eigenschaften enthalten. Wenn PurchaseInvoice beispielsweise über eine Eigenschaft namens **NumItemsPurchased**verfügt, können Sie wie folgt auf diese Eigenschaft im Code verweisen:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Profilvererbung

Es ist möglich, ein Profil für die Verwendung in mehreren Anwendungen zu erstellen. Durch Erstellen einer Profilklasse, die von ProfileBase abstammt, können Sie ein Profil in mehreren Anwendungen wiederverwenden, indem Sie das Attribut **"erbt"** verwenden, wie unten gezeigt:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

In diesem Fall würde die Klasse **PurchasingProfile** wie folgt aussehen:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Profilanbieter

ASP.NET Profile verwenden das Anbietermodell. Der Standardanbieter speichert die Informationen in einer\_SQL Server Express-Datenbank im Ordner App-Daten der Webanwendung mithilfe des SqlProfileProvider-Anbieters. Wenn die Datenbank nicht vorhanden ist, erstellt ASP.NET sie automatisch, wenn das Profil versucht, Informationen zu speichern.

In einigen Fällen können Sie jedoch Ihren eigenen Profilanbieter entwickeln. Die ASP.NET Profilfunktion ermöglicht es Ihnen, verschiedene Anbieter einfach zu verwenden.

Sie erstellen einen benutzerdefinierten Profilanbieter, wenn:

- Sie müssen Profilinformationen in einer Datenquelle speichern, z. B. in einer FoxPro-Datenbank oder in einer Oracle-Datenbank, die von den in .NET Framework enthaltenen Profilanbietern nicht unterstützt wird.
- Sie müssen Profilinformationen mithilfe eines Datenbankschemas verwalten, das sich vom Datenbankschema unterscheidet, das von den in .NET Framework enthaltenen Anbietern verwendet wird. Ein häufiges Beispiel ist, dass Sie Profilinformationen mit Benutzerdaten in eine vorhandene SQL Server-Datenbank integrieren möchten.

### <a name="required-classes"></a>Erforderliche Klassen

Um einen Profilanbieter zu implementieren, erstellen Sie eine Klasse, die die abstrakte Klasse System.Web.Profile.ProfileProvider erbt. Die abstrakte **Class ProfileProvider** wiederum erbt die abstrakte Klasse System.Configuration.SettingsProvider, die die abstrakte Klasse System.Configuration.Provider.ProviderBase erbt. Aufgrund dieser Vererbungskette müssen Sie zusätzlich zu den erforderlichen Membern der **ProfileProvider-Klasse** die erforderlichen Member der **Klassen SettingsProvider** und **ProviderBase** implementieren.

In den folgenden Tabellen werden die Eigenschaften und Methoden beschrieben, die Sie aus den abstrakten Klassen **ProviderBase**, **SettingsProvider**und **ProfileProvider** implementieren müssen.

### <a name="providerbase-members"></a>ProviderBase-Mitglieder

| **Member** | **Beschreibung** |
| --- | --- |
| Initialize-Methode | Nimmt als Eingabe den Namen der Anbieterinstanz und eine NameValueCollection der Konfigurationseinstellungen an. Wird verwendet, um Optionen und Eigenschaftswerte für die Anbieterinstanz festzulegen, einschließlich implementierungsspezifischer Werte und Optionen, die in der Computerkonfiguration oder Web.config-Datei angegeben sind. |

### <a name="settingsprovider-members"></a>SettingsProvider-Mitglieder

| **Member** | **Beschreibung** |
| --- | --- |
| ApplicationName-Eigenschaft | Der Anwendungsname, der bei jedem Profil gespeichert wird. Der Profilanbieter verwendet den Anwendungsnamen, um Profilinformationen für jede Anwendung separat zu speichern. Dadurch können mehrere ASP.NET Anwendungen dieselbe Datenquelle ohne Konflikt verwenden, wenn derselbe Benutzername in verschiedenen Anwendungen erstellt wird. Alternativ können mehrere ASP.NET Anwendungen eine Profildatenquelle gemeinsam nutzen, indem sie denselben Anwendungsnamen angeben. |
| GetPropertyValues-Methode | Nimmt als Eingabe ein SettingsContext- und ein SettingsPropertyCollection-Objekt an. Der **SettingsContext** stellt Informationen über den Benutzer bereit. Sie können die Informationen als Primärschlüssel verwenden, um Profileigenschafteninformationen für den Benutzer abzurufen. Verwenden Sie das **SettingsContext-Objekt,** um den Benutzernamen abzubekommen und unabhängig davon, ob der Benutzer authentifiziert oder anonym ist. Die **SettingsPropertyCollection** enthält eine Auflistung von SettingsProperty-Objekten. Jedes **SettingsProperty-Objekt** stellt den Namen und Typ der Eigenschaft sowie zusätzliche Informationen wie den Standardwert für die Eigenschaft und ob die Eigenschaft schreibgeschützt ist. Die **GetPropertyValues-Methode** füllt eine SettingsPropertyValueCollection mit SettingsPropertyValue-Objekten auf der Grundlage der als Eingabe bereitgestellten **SettingsProperty-Objekte** aus. Die Werte aus der Datenquelle für den angegebenen Benutzer werden den PropertyValue-Eigenschaften für jedes **SettingsPropertyValue-Objekt** zugewiesen, und die gesamte Auflistung wird zurückgegeben. Durch Aufrufen der Methode wird auch der LastActivityDate-Wert für das angegebene Benutzerprofil auf das aktuelle Datum und die aktuelle Uhrzeit aktualisiert. |
| SetPropertyValues-Methode | Nimmt als Eingabe ein **SettingsContext-** und ein **SettingsPropertyValueCollection-Objekt** an. Der **SettingsContext** stellt Informationen über den Benutzer bereit. Sie können die Informationen als Primärschlüssel verwenden, um Profileigenschafteninformationen für den Benutzer abzurufen. Verwenden Sie das **SettingsContext-Objekt,** um den Benutzernamen abzubekommen und unabhängig davon, ob der Benutzer authentifiziert oder anonym ist. Die **SettingsPropertyValueCollection** enthält eine Auflistung von **SettingsPropertyValue-Objekten.** Jedes **SettingsPropertyValue-Objekt** stellt den Namen, den Typ und den Wert der Eigenschaft sowie zusätzliche Informationen wie den Standardwert für die Eigenschaft und ob die Eigenschaft schreibgeschützt ist. Die **SetPropertyValues-Methode** aktualisiert die Profileigenschaftswerte in der Datenquelle für den angegebenen Benutzer. Durch Aufrufen der Methode werden auch die **Werte LastActivityDate** und LastUpdatedDate für das angegebene Benutzerprofil auf das aktuelle Datum und die aktuelle Uhrzeit aktualisiert. |

### <a name="profileprovider-members"></a>ProfileProvider-Mitglieder

| **Member** | **Beschreibung** |
| --- | --- |
| DeleteProfiles-Methode | Nimmt als Eingabe ein Zeichenfolgenarray mit Benutzernamen und löscht aus der Datenquelle alle Profilinformationen und **ApplicationName** Eigenschaftswerte für die angegebenen Namen, bei denen der Anwendungsname mit dem ApplicationName-Eigenschaftswert übereinstimmt. Wenn Ihre Datenquelle Transaktionen unterstützt, wird empfohlen, alle Löschvorgänge in eine Transaktion einzubeziehen und einen Rollback für die Transaktion durchzuführen und eine Ausnahme auszulösen, wenn ein Löschvorgang fehlschlägt. |
| DeleteProfiles-Methode | Nimmt als Eingabe eine Auflistung von ProfileInfo-Objekten und löscht aus der Datenquelle alle Profilinformationen **ApplicationName** und Eigenschaftswerte für jedes Profil, in dem der Anwendungsname mit dem ApplicationName-Eigenschaftswert übereinstimmt. Wenn Ihre Datenquelle Transaktionen unterstützt, wird empfohlen, alle Löschvorgänge in eine Transaktion einzubinden und einen Rollback für die Transaktion einzuschlagen und eine Ausnahme auszulösen, wenn ein Löschvorgang fehlschlägt. |
| DeleteInactiveProfiles-Methode | Nimmt als Eingabe einen ProfileAuthenticationOption-Wert und ein DateTime-Objekt an und löscht aus der Datenquelle alle Profilinformationen und Eigenschaftswerte, bei **ApplicationName** denen das letzte Aktivitätsdatum kleiner oder gleich dem angegebenen Datum und der angegebenen Uhrzeit ist und der Anwendungsname mit dem ApplicationName-Eigenschaftswert übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile gelöscht werden sollen. Wenn Ihre Datenquelle Transaktionen unterstützt, wird empfohlen, alle Löschvorgänge in eine Transaktion einzubinden und einen Rollback für die Transaktion einzuschlagen und eine Ausnahme auszulösen, wenn ein Löschvorgang fehlschlägt. |
| GetAllProfiles-Methode | Nimmt als Eingabe einen **ProfileAuthenticationOption-Wert,** eine ganze Zahl, die den Seitenindex angibt, eine ganze Zahl, die die Seitengröße angibt, und einen Verweis auf eine ganze Zahl, die auf die Gesamtzahl der Profile festgelegt wird. Gibt eine ProfileInfoCollection zurück, die **ProfileInfo-Objekte** für alle Profile in der Datenquelle enthält, in der der Anwendungsname mit dem **ApplicationName-Eigenschaftswert** übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile zurückgegeben werden sollen. Die von der **GetAllProfiles-Methode** zurückgegebenen Ergebnisse werden durch den Seitenindex und die Seitengrößenwerte eingeschränkt. Der Seitengrößenwert gibt die maximale Anzahl von **ProfileInfo-Objekten** an, die in der **ProfileInfoCollection**zurückgegeben werden sollen. Der Seitenindexwert gibt an, welche Seite der Ergebnisse zurückgegeben werden soll, wobei 1 die erste Seite identifiziert. Der Parameter für Gesamtdatensätze ist ein out-Parameter (Sie können **ByRef** in Visual Basic verwenden), der auf die Gesamtzahl der Profile festgelegt ist. Wenn der Datenspeicher beispielsweise 13 Profile für die Anwendung enthält und der Seitenindexwert 2 mit einer Seitengröße von 5 ist, enthält die zurückgegebene **ProfileInfoCollection** das sechste bis das zehnte Profil. Der Gesamtwert für Datensätze wird auf 13 festgelegt, wenn die Methode zurückgegeben wird. |
| GetAllInactiveProfiles-Methode | Nimmt als Eingabe einen **ProfileAuthenticationOption-Wert,** ein **DateTime-Objekt,** eine ganze Zahl, die den Seitenindex angibt, eine ganze Zahl, die die Seitengröße angibt, und einen Verweis auf eine ganze Zahl, die auf die Gesamtzahl der Profile festgelegt wird. Gibt eine **ProfileInfoCollection** zurück, die **ProfileInfo-Objekte** für alle Profile in der Datenquelle enthält, bei denen das datum der letzten Aktivität kleiner oder gleich der angegebenen **DateTime** ist und der Anwendungsname mit dem **ApplicationName-Eigenschaftswert** übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile zurückgegeben werden sollen. Die von der **GetAllInactiveProfiles-Methode** zurückgegebenen Ergebnisse werden durch den Seitenindex und die Seitengrößenwerte eingeschränkt. Der Seitengrößenwert gibt die maximale Anzahl von **ProfileInfo-Objekten** an, die in der **ProfileInfoCollection**zurückgegeben werden sollen. Der Seitenindexwert gibt an, welche Seite der Ergebnisse zurückgegeben werden soll, wobei 1 die erste Seite identifiziert. Der Parameter für Gesamtdatensätze ist ein out-Parameter (Sie können **ByRef** in Visual Basic verwenden), der auf die Gesamtzahl der Profile festgelegt ist. Wenn der Datenspeicher beispielsweise 13 Profile für die Anwendung enthält und der Seitenindexwert 2 mit einer Seitengröße von 5 ist, enthält die zurückgegebene **ProfileInfoCollection** das sechste bis das zehnte Profil. Der Gesamtwert für Datensätze wird auf 13 festgelegt, wenn die Methode zurückgegeben wird. |
| FindProfilesByUserName-Methode | Nimmt als Eingabe einen **ProfileAuthenticationOption-Wert,** eine Zeichenfolge, die einen Benutzernamen enthält, eine ganze Zahl, die den Seitenindex angibt, eine ganze Zahl, die die Seitengröße angibt, und einen Verweis auf eine ganze Zahl, die auf die Gesamtzahl der Profile festgelegt wird. Gibt eine **ProfileInfoCollection** zurück, die **ProfileInfo-Objekte** für alle Profile in der Datenquelle enthält, in denen der Benutzername mit dem angegebenen Benutzernamen übereinstimmt und der Anwendungsname mit dem **ApplicationName-Eigenschaftswert** übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile zurückgegeben werden sollen. Wenn Ihre Datenquelle zusätzliche Suchfunktionen unterstützt, z. B. Platzhalterzeichen, können Sie umfangreichere Suchfunktionen für Benutzernamen bereitstellen. Die von der **FindProfilesByUserName-Methode** zurückgegebenen Ergebnisse werden durch den Seitenindex und die Seitengrößenwerte eingeschränkt. Der Seitengrößenwert gibt die maximale Anzahl von **ProfileInfo-Objekten** an, die in der **ProfileInfoCollection**zurückgegeben werden sollen. Der Seitenindexwert gibt an, welche Seite der Ergebnisse zurückgegeben werden soll, wobei 1 die erste Seite identifiziert. Der Parameter für Gesamtdatensätze ist ein out-Parameter (Sie können **ByRef** in Visual Basic verwenden), der auf die Gesamtzahl der Profile festgelegt ist. Wenn der Datenspeicher beispielsweise 13 Profile für die Anwendung enthält und der Seitenindexwert 2 mit einer Seitengröße von 5 ist, enthält die zurückgegebene **ProfileInfoCollection** das sechste bis das zehnte Profil. Der Gesamtwert für Datensätze wird auf 13 festgelegt, wenn die Methode zurückgegeben wird. |
| FindInactiveProfilesByUserName-Methode | Nimmt als Eingabe einen **ProfileAuthenticationOption-Wert,** eine Zeichenfolge, die einen Benutzernamen, ein **DateTime-Objekt,** eine ganze Zahl, die den Seitenindex angibt, eine ganze Zahl, die die Seitengröße angibt, und einen Verweis auf eine ganze Zahl, die auf die Gesamtzahl der Profile festgelegt wird. Gibt eine **ProfileInfoCollection** zurück, die **ProfileInfo-Objekte** für alle Profile in der Datenquelle enthält, in der der Benutzername mit dem angegebenen Benutzernamen übereinstimmt, wobei das datum der letzten Aktivität kleiner oder gleich der angegebenen **DateTime**ist und der Anwendungsname mit dem **ApplicationName-Eigenschaftswert** übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile zurückgegeben werden sollen. Wenn Ihre Datenquelle zusätzliche Suchfunktionen unterstützt, z. B. Platzhalterzeichen, können Sie umfangreichere Suchfunktionen für Benutzernamen bereitstellen. Die von der **FindInactiveProfilesByUserName-Methode** zurückgegebenen Ergebnisse werden durch den Seitenindex und die Seitengrößenwerte eingeschränkt. Der Seitengrößenwert gibt die maximale Anzahl von **ProfileInfo-Objekten** an, die in der **ProfileInfoCollection**zurückgegeben werden sollen. Der Seitenindexwert gibt an, welche Seite der Ergebnisse zurückgegeben werden soll, wobei 1 die erste Seite identifiziert. Der Parameter für Gesamtdatensätze ist ein out-Parameter (Sie können **ByRef** in Visual Basic verwenden), der auf die Gesamtzahl der Profile festgelegt ist. Wenn der Datenspeicher beispielsweise 13 Profile für die Anwendung enthält und der Seitenindexwert 2 mit einer Seitengröße von 5 ist, enthält die zurückgegebene **ProfileInfoCollection** das sechste bis das zehnte Profil. Der Gesamtwert für Datensätze wird auf 13 festgelegt, wenn die Methode zurückgegeben wird. |
| GetNumberOfInActiveProfiles-Methode | Nimmt als Eingabe einen **ProfileAuthenticationOption-Wert** und ein **DateTime-Objekt** an und gibt eine Anzahl aller Profile in der Datenquelle zurück, bei denen das letzte Aktivitätsdatum kleiner oder gleich der angegebenen **DateTime** ist und der Anwendungsname mit dem **ApplicationName-Eigenschaftswert** übereinstimmt. Der Parameter **ProfileAuthenticationOption** gibt an, ob nur anonyme Profile, nur authentifizierte Profile oder alle Profile gezählt werden sollen. |

### <a name="applicationname"></a>ApplicationName

Da Profilanbieter Profilinformationen für jede Anwendung separat speichern, müssen Sie sicherstellen, dass das Datenschema den Anwendungsnamen enthält und dass Abfragen und Aktualisierungen auch den Anwendungsnamen enthalten. Der folgende Befehl wird beispielsweise verwendet, um einen Eigenschaftswert aus einer Datenbank basierend auf dem Benutzernamen und der Frage abzurufen, ob das Profil anonym ist, und stellt sicher, dass der **ApplicationName-Wert** in die Abfrage eingeschlossen wird.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET Themen

## <a name="what-are-aspnet-20-themes"></a>Was sind ASP.NET 2.0-Themen?

Einer der wichtigsten Aspekte einer Webanwendung ist ein konsistentes Erscheinungsbild auf der gesamten Website. ASP.NET 1.x-Entwickler verwenden in der Regel Cascading Style Sheets (CSS), um ein konsistentes Erscheinungsbild zu implementieren. ASP.NET 2.0-Themen verbessern CSS erheblich, da sie dem ASP.NET Entwickler die Möglichkeit geben, das Erscheinungsbild von ASP.NET Serversteuerelementen sowie HTML-Elementen zu definieren. ASP.NET Designs können auf einzelne Steuerelemente, eine bestimmte Webseite oder eine gesamte Webanwendung angewendet werden. Designs verwenden eine Kombination aus CSS-Dateien, einer optionalen Skindatei und einem optionalen Images-Verzeichnis, wenn Bilder benötigt werden. Die Skindatei steuert das visuelle Erscheinungsbild von ASP.NET Serversteuerelementen.

## <a name="where-are-themes-stored"></a>Wo werden Themen gespeichert?

Der Speicherort, an dem Themen gespeichert werden, hängt von ihrem Umfang ab. Designs, die auf jede Anwendung angewendet werden können, werden im folgenden Ordner gespeichert:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Ein Design, das für eine bestimmte Anwendung `App\_Themes\<Theme\_Name>` spezifisch ist, wird in einem Verzeichnis im Stammverzeichnis der Website gespeichert.

> [!NOTE]
> Eine Skindatei sollte nur die Eigenschaften der Serversteuerung ändern, die sich auf das Erscheinungsbild auswirken.

Ein globales Design ist ein Design, das auf jede Anwendung oder Website angewendet werden kann, die auf dem Webserver ausgeführt wird. Diese Designs werden standardmäßig im Verzeichnis ASP.NETClientfiles-Themes gespeichert, das sich innerhalb des Verzeichnisses v2.x.xxxxx befindet. Alternativ können Sie die Designdateien in den\_Ordner aspnet client/system\_web/[version]/Themes/[theme\_name] im Stammverzeichnis Ihrer Website verschieben.

Anwendungsspezifische Designs können nur auf die Anwendung angewendet werden, in der sich die Dateien befinden. Diese Dateien werden `App\_Themes/<theme\_name>` im Verzeichnis im Stammverzeichnis der Website gespeichert.

## <a name="the-components-of-a-theme"></a>Die Komponenten eines Themas

Ein Design besteht aus einer oder mehreren CSS-Dateien, einer optionalen Skindatei und einem optionalen Ordner "Images". Die CSS-Dateien können beliebige Randnamen sein (d. h. default.css oder theme.css usw.) und müssen sich im Stammverzeichnis des Themes-Ordners befinden. Die CSS-Dateien werden verwendet, um normale CSS-Klassen und Attribute für bestimmte Selektoren zu definieren. Um eine der CSS-Klassen auf ein Seitenelement anzuwenden, wird die **CSSClass-Eigenschaft** verwendet.

Die Skindatei ist eine XML-Datei, die Eigenschaftendefinitionen für ASP.NET Serversteuerelemente enthält. Der unten aufgeführte Code ist eine Beispiel-Skindatei.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

**Abbildung 1** unten zeigt eine kleine ASP.NET Seite, die ohne angewendetes Design durchsucht wurde. **Abbildung 2** zeigt dieselbe Datei mit einem angewendeten Design. Die Hintergrundfarbe und die Textfarbe werden über eine CSS-Datei konfiguriert. Die Darstellung der Schaltfläche und des Textfelds wird mithilfe der oben aufgeführten Skindatei konfiguriert.

![Kein Thema](profiles-themes-and-web-parts/_static/image1.gif)

**Abbildung 1:** Kein Thema

![Thema Angewendet](profiles-themes-and-web-parts/_static/image2.gif)

**Abbildung 2:** Angewendetes Thema

Die oben aufgeführte Skindatei definiert eine Standard-Skin für alle TextBox-Steuerelemente und Schaltflächensteuerelemente. Das bedeutet, dass jedes TextBox-Steuerelement und button-Steuerelement, das auf einer Seite eingefügt wird, diese Darstellung annehmen. Sie können auch eine Skin definieren, die mithilfe der **SkinID-Eigenschaft** des Steuerelements auf bestimmte Instanzen dieser Steuerelemente angewendet werden kann.

Der folgende Code definiert eine Skin für ein Button-Steuerelement. Nur Button-Steuerelemente mit einer **SkinID-Eigenschaft** von **goButton** übernehmen das Erscheinungsbild der Skin.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Sie können nur eine Standard-Skin pro Serversteuerelementtyp haben. Wenn Sie zusätzliche Skins benötigen, sollten Sie die SkinID-Eigenschaft verwenden.

## <a name="applying-themes-to-pages"></a>Anwenden von Designs auf Seiten

Ein Design kann mit einer der folgenden Methoden angewendet werden:

- Im &lt;Pages-Element&gt; der Datei web.config
- In @Page der Direktive einer Seite
- Programmgesteuert

## <a name="applying-a-theme-in-the-configuration-file"></a>Anwenden eines Themas in der Konfigurationsdatei

Verwenden Sie die folgende Syntax, um ein Design in der Anwendungskonfigurationsdatei anzuwenden:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

Der hier angegebene Designname muss mit dem Namen des Designsordners übereinstimmen. Dieser Ordner kann entweder an einem der oben in diesem Kurs genannten Speicherorte vorhanden sein. Wenn Sie versuchen, ein Design anzuwenden, das nicht vorhanden ist, tritt ein Konfigurationsfehler auf.

## <a name="applying-a-theme-in-the-page-directive"></a>Anwenden eines Themas in der Seitenrichtlinie

Sie können auch ein Design in der Direktive "Seite" anwenden. Mit dieser Methode können Sie ein Design für eine bestimmte Seite verwenden.

Um ein Design in @Page der Direktive anzuwenden, verwenden Sie die folgende Syntax:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Auch hier muss das hier angegebene Thema mit dem zuvor erwähnten Themenordner übereinstimmen. Wenn Sie versuchen, ein Design anzuwenden, das nicht vorhanden ist, tritt ein Buildfehler auf. Visual Studio hebt auch das Attribut hervor und benachrichtigt Sie, dass kein solches Design vorhanden ist.

## <a name="applying-a-theme-programmatically"></a>Programmgesteuertes Anwenden eines Themas

Um ein Design programmgesteuert anzuwenden, müssen Sie die **Theme-Eigenschaft** für die Seite in der **Page\_PreInit-Methode** angeben.

Um ein Design programmgesteuert anzuwenden, verwenden Sie die folgende Syntax:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

Aufgrund des Seitenlebenszyklus ist es erforderlich, das Design in der PreInit-Methode anzuwenden. Wenn Sie es nach diesem Punkt anwenden, wurde das Seitendesign bereits von der Laufzeit angewendet, und eine Änderung zu diesem Zeitpunkt ist zu spät im Lebenszyklus. Wenn Sie ein Design anwenden, das nicht vorhanden ist, tritt eine **HttpException** auf. Wenn ein Design programmgesteuert angewendet wird, wird eine Buildwarnung angezeigt, wenn Serversteuerelemente eine SkinID-Eigenschaft angegeben haben. Diese Warnung soll Sie darüber informieren, dass kein Thema deklarativ angewendet wird und ignoriert werden kann.

## <a name="exercise-1--applying-a-theme"></a>Übung 1 : Anwenden eines Themas

In dieser Übung wenden Sie ein ASP.NET Design auf eine Website an.

> [!IMPORTANT]
> Wenn Sie Microsoft Word verwenden, um Informationen in eine Skindatei einzugeben, stellen Sie sicher, dass Sie keine regulären Anführungszeichen durch intelligente Anführungszeichen ersetzen. Intelligente Zitate verursachen Probleme mit Skindateien.

1. Erstellen Sie eine neue ASP.NET-Website.
2. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie Neues Element hinzufügen aus.
3. Wählen Sie Webkonfigurationsdatei aus der Liste der Dateien aus, und klicken Sie auf Hinzufügen.
4. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und wählen Sie Neues Element hinzufügen aus.
5. Wählen Sie Skin File und klicken Sie auf Hinzufügen.
6. Klicken Sie auf Ja, wenn Sie gefragt werden,\_ob Sie die Datei im Ordner App Themes platzieren möchten.
7. Klicken Sie mit der rechten Maustaste\_auf den Ordner SkinFile im Ordner App Themes im Projektmappen-Explorer, und wählen Sie Neues Element hinzufügen aus.
8. Wählen Sie StyleSheet aus der Liste der Dateien aus, und klicken Sie auf Hinzufügen. Sie haben jetzt alle Dateien, die zum Implementieren Des neuen Themas erforderlich sind. Visual Studio hat jedoch Ihren Themenordner SkinFile benannt. Klicken Sie mit der rechten Maustaste auf diesen Ordner und ändern Sie den Namen in CoolTheme.
9. Öffnen Sie die Datei SkinFile.skin, und fügen Sie den folgenden Code am Ende der Datei hinzu: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. Speichern Sie die Datei SkinFile.skin.
11. Öffnen Sie StyleSheet.css.
12. Ersetzen Sie den gesamten darin enthaltenen Text durch Folgendes: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. Speichern Sie die Datei StyleSheet.css.
14. Öffnen Sie die Seite Default.aspx.
15. Fügen Sie ein TextBox-Steuerelement und ein Schaltflächensteuerelement hinzu.
16. Speichern Sie die Seite. Durchsuchen Sie nun die Seite Default.aspx. Es sollte als normales Webformular angezeigt werden.
17. Öffnen Sie die Datei web.config.
18. Fügen Sie Folgendes direkt `<system.web>` unter dem öffnenden Tag hinzu: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Speichern Sie die Datei web.config. Durchsuchen Sie nun die Seite Default.aspx. Es sollte mit dem angewendeten Thema angezeigt werden.
20. Wenn es noch nicht geöffnet ist, öffnen Sie die Seite Default.aspx in Visual Studio.
21. Wählen Sie die Schaltfläche aus.
22. Ändern Sie die **SkinID-Eigenschaft** in goButton. Beachten Sie, dass Visual Studio eine Dropdownliste mit gültigen SkinID-Werten für ein Schaltflächensteuerelement bereitstellt.
23. Speichern Sie die Seite. Sehen Sie sich nun die Seite in Ihrem Browser erneut an. Der Button sollte nun "go" sagen und im Aussehen breiter aussehen.

Mithilfe der **SkinID-Eigenschaft** können Sie ganz einfach verschiedene Skins für verschiedene Instanzen eines bestimmten Serversteuerelements konfigurieren.

## <a name="the-stylesheettheme-property"></a>Die StyleSheetTheme-Eigenschaft

Bisher haben wir nur über die Anwendung von Themen gesprochen, die die Theme-Eigenschaft verwenden. Bei Verwendung der Theme-Eigenschaft überschreibt die Skindatei alle deklarativen Einstellungen für Serversteuerelemente. In Übung 1 haben Sie beispielsweise eine SkinID von "goButton" für das Button-Steuerelement angegeben, die den Text der Schaltfläche in "go" geändert hat. Sie haben vielleicht bemerkt, dass die Text-Eigenschaft der Schaltfläche im Designer auf "Button" festgelegt wurde, aber das Thema überlagert dies. Das Design überschreibt immer alle Eigenschafteneinstellungen im Designer.

Wenn Sie die in der Skindatei des Themas definierten Eigenschaften mit im Designer angegebenen Eigenschaften überschreiben möchten, können Sie die **StyleSheetTheme-Eigenschaft** anstelle der Theme-Eigenschaft verwenden. Die StyleSheetTheme-Eigenschaft ist identisch mit der Theme-Eigenschaft, mit der Ausnahme, dass sie nicht alle expliziten Eigenschafteneinstellungen überschreibt, wie es die Theme-Eigenschaft tut.

Um dies in Aktion anzuzeigen, öffnen Sie die Datei web.config aus dem Projekt in Übung 1, und ändern Sie das `<pages>` Element in Folgendes:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Durchsuchen Sie nun die Seite Default.aspx, und Sie sehen, dass das Button-Steuerelement erneut über die Text-Eigenschaft "Button" verfügt. Das liegt daran, dass die explizite Eigenschaftseinstellung im Designer die Text-Eigenschaft überschreibt, die von der goButton SkinID festgelegt wird.

## <a name="overriding-themes"></a>Übergeordnete Themen

Ein globales Design kann überschrieben werden, indem ein Design\_mit demselben Namen im Ordner App Themes der Anwendung angewendet wird. Das Design wird jedoch nicht in einem echten Außerkraftsetzungsszenario angewendet. Wenn die Laufzeit auf Designdateien\_im Ordner App Themes trifft, wird das Design mithilfe dieser Dateien angewendet und das globale Design ignoriert.

Die StyleSheetTheme-Eigenschaft ist überschreibbar und kann im Code wie folgt überschrieben werden:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Webparts

ASP.NET Webparts ist ein integrierter Satz von Steuerelementen zum Erstellen von Websites, mit denen Endbenutzer den Inhalt, die Darstellung und das Verhalten von Webseiten direkt über einen Browser ändern können. Die Änderungen können auf alle Benutzer auf der Website oder auf einzelne Benutzer angewendet werden. Wenn Benutzer Seiten und Steuerelemente ändern, können die Einstellungen gespeichert werden, um die persönlichen Einstellungen eines Benutzers in zukünftigen Browsersitzungen beizubehalten, eine Funktion, die als Personalisierung bezeichnet wird. Diese Webparts-Funktionen bedeuten, dass Entwickler Endbenutzer in die Lage versetzen können, eine Webanwendung dynamisch und ohne Eingreifen von Entwicklern oder Administratoren zu personalisieren.

Mithilfe des Steuerelements Webparts können Sie als Entwickler Endbenutzern folgende Funktionen ermöglichen:

- Personalisieren Sie den Seiteninhalt. Benutzer können einer Seite neue Webparts-Steuerelemente hinzufügen, sie entfernen, ausblenden oder wie normale Fenster minimieren.
- Personalisieren Sie das Seitenlayout. Benutzer können ein Webparts-Steuerelement in eine andere Zone auf einer Seite ziehen oder dessen Aussehen, Eigenschaften und Verhalten ändern.
- Export- und Importsteuerelemente. Benutzer können Webparts-Steuerelementeinstellungen für die Verwendung auf anderen Seiten oder Websites importieren oder exportieren, um die Eigenschaften, das Erscheinungsbild und sogar die Daten in den Steuerelementen beizubehalten. Dies reduziert die Anforderungen an die Dateneingabe und Konfiguration für Endbenutzer.
- Erstellen Sie Verbindungen. Benutzer können Verbindungen zwischen Steuerelementen herstellen, sodass z. B. ein Diagrammsteuerelement ein Diagramm für die Daten in einem Aktienticker-Steuerelement anzeigen kann. Benutzer können nicht nur die Verbindung selbst personalisieren, sondern auch das Erscheinungsbild und die Details, wie das Diagrammsteuerelement die Daten anzeigt.
- Verwalten und personalisieren Sie Einstellungen auf Websiteebene. Autorisierte Benutzer können Einstellungen auf Websiteebene konfigurieren, bestimmen, wer auf eine Website oder Seite zugreifen kann, rollenbasierten Zugriff auf Steuerelemente festlegen usw. Beispielsweise kann ein Benutzer in einer Administratorrolle festlegen, dass ein Webparts-Steuerelement von allen Benutzern gemeinsam genutzt wird, und Benutzer, die keine Administratoren sind, daran hindern, das freigegebene Steuerelement zu personalisieren.

In der Regel arbeiten Sie mit Webparts auf drei Arten: Erstellen von Seiten, die Webparts-Steuerelemente verwenden, Erstellen einzelner Webparts-Steuerelemente oder Erstellen vollständiger, personalisierbarer Webanwendungen, z. B. eines Portals.

## <a name="page-development"></a>Seitenentwicklung

Seitenentwickler können mithilfe von visuellen Entwurfstools wie Microsoft Visual Studio 2005 Seiten erstellen, die Webparts verwenden. Ein Vorteil bei der Verwendung eines Tools wie Visual Studio besteht darin, dass der Webparts-Steuerelementsatz Features für die Drag-and-Drop-Erstellung und Konfiguration von Webparts-Steuerelementen in einem visuellen Designer bereitstellt. Sie können den Designer beispielsweise verwenden, um eine Webparts-Zone oder ein Webparts-Editor-Steuerelement auf die Entwurfsoberfläche zu ziehen, und dann das Steuerelement rechts im Designer mithilfe der vom Webparts-Steuerelementsatz bereitgestellten Benutzeroberfläche konfigurieren. Dies kann die Entwicklung von Webparts-Anwendungen beschleunigen und die Menge an Code reduzieren, die Sie schreiben müssen.

## <a name="control-development"></a>Steuerungsentwicklung

Sie können alle vorhandenen ASP.NET Steuerelementals als Webparts-Steuerelement verwenden, einschließlich standarderwebserversteuerelemente, benutzerdefinierte Serversteuerelemente und Benutzersteuerelemente. Für die maximale programmgesteuerte Steuerung Ihrer Umgebung können Sie auch benutzerdefinierte Webparts-Steuerelemente erstellen, die von der WebPart-Klasse stammen. Für die Entwicklung einzelner Webparts-Steuerelemente erstellen Sie in der Regel entweder ein Benutzersteuerelement und verwenden es als Webparts-Steuerelement, oder Sie entwickeln ein benutzerdefiniertes Webparts-Steuerelement.

Als Beispiel für die Entwicklung eines benutzerdefinierten Webparts-Steuerelements können Sie ein Steuerelement erstellen, um alle Funktionen anderer ASP.NET-Serversteuerelemente bereitzustellen, die nützlich sein könnten, um als personalisierbares Webparts-Steuerelement zu verpacken: Kalender, Listen, Finanzinformationen, Nachrichten, Taschenrechner, Rich-Text-Steuerelemente zum Aktualisieren von Inhalten, bearbeitbare Raster, die eine Verbindung zu Datenbanken herstellen, Diagramme, die ihre Anzeigen dynamisch aktualisieren. oder Wetter- und Reiseinformationen. Wenn Sie einen visuellen Designer mit Ihrem Steuerelement bereitstellen, kann jeder Seitenentwickler, der Visual Studio verwendet, das Steuerelement einfach in eine Webparts-Zone ziehen und es zur Entwurfszeit konfigurieren, ohne zusätzlichen Code schreiben zu müssen.

Personalisierung ist die Grundlage der Webparts-Funktion. Es ermöglicht Benutzern, das Layout, das Erscheinungsbild und das Verhalten von Webparts-Steuerelementen auf einer Seite zu ändern oder zu personalisieren. Die personalisierten Einstellungen sind langlebig: Sie werden nicht nur während der aktuellen Browsersitzung (wie im Ansichtszustand), sondern auch im Langzeitspeicher beibehalten, so dass die Einstellungen eines Benutzers auch für zukünftige Browsersitzungen gespeichert werden. Die Personalisierung ist standardmäßig für Webparts-Seiten aktiviert.

Die Strukturkomponenten der Benutzeroberfläche basieren auf der Personalisierung und stellen die Kernstruktur und die Dienste bereit, die für alle Webparts-Steuerelemente erforderlich sind. Eine Strukturkomponente der Benutzeroberfläche, die auf jeder Webparts-Seite erforderlich ist, ist das WebPartManager-Steuerelement. Obwohl dieses Steuerelement nie sichtbar ist, hat es die entscheidende Aufgabe, alle Webparts-Steuerelemente auf einer Seite zu koordinieren. Beispielsweise werden alle einzelnen Webparts-Steuerelemente nachverfolgt. Es verwaltet Webparts-Zonen (Regionen, die Webparts-Steuerelemente auf einer Seite enthalten) und welche Steuerelemente sich in welchen Zonen befinden. Außerdem werden die verschiedenen Anzeigemodi, in denen sich eine Seite befinden kann, wie z. B. Durchsuchen, Verbinden, Bearbeiten oder Katalogmodus, und ob Personalisierungsänderungen für alle Benutzer oder einzelne Benutzer gelten, nachverfolgt und gesteuert. Schließlich initiiert und verfolgt es Verbindungen und die Kommunikation zwischen Webparts-Steuerelementen.

Die zweite Art der Strukturkomponente der Benutzeroberfläche ist die Zone. Zonen fungieren als Layout-Manager auf einer Webparts-Seite. Sie enthalten und organisieren Steuerelemente, die von der Part-Klasse (Teilesteuerelemente) abstammen, und bieten die Möglichkeit, modulares Seitenlayout in horizontaler oder vertikaler Ausrichtung durchzuführen. Zonen bieten auch allgemeine und konsistente UI-Elemente (z. B. Kopf- und Fußzeilenstil, Titel, Rahmenstil, Aktionsschaltflächen usw.) für jedes Steuerelement, das sie enthalten. diese gemeinsamen Elemente werden als Chrom eines Steuerelements bezeichnet. In den verschiedenen Anzeigemodi und mit verschiedenen Steuerelementen werden verschiedene spezielle Zonentypen verwendet. Die verschiedenen Zonentypen werden im Abschnitt "Webparts Essential Controls" unten beschrieben.

Die Webparts-UI-Steuerelemente, die alle von der **Part-Klasse** stammen, umfassen die primäre Benutzeroberfläche auf einer Webparts-Seite. Der Webparts-Steuerelementsatz ist flexibel und inklusiv in den Optionen, die Sie zum Erstellen von Bauteilsteuerelementen erhalten. Zusätzlich zum Erstellen eigener benutzerdefinierter Webparts-Steuerelemente können Sie vorhandene ASP.NET Serversteuerelemente, Benutzersteuerelemente oder benutzerdefinierte Serversteuerelemente als Webparts-Steuerelemente verwenden. Die wesentlichen Steuerelemente, die am häufigsten zum Erstellen von Webparts-Seiten verwendet werden, werden im nächsten Abschnitt beschrieben.

## <a name="web-parts-essential-controls"></a>Webparts Wesentliche Steuerelemente

Der Webparts-Steuerelementsatz ist umfangreich, aber einige Steuerelemente sind wichtig, entweder weil sie erforderlich sind, damit Webparts funktionieren, oder weil sie die Steuerelemente sind, die am häufigsten auf Webparts-Seiten verwendet werden. Wenn Sie mit der Verwendung von Webparts und dem Erstellen grundlegender Webparts-Seiten beginnen, ist es hilfreich, mit den in der folgenden Tabelle beschriebenen grundlegenden Webparts-Steuerelementen vertraut zu sein.

| **Webparts-Steuerelement** | **Beschreibung** |
| --- | --- |
| Webpartmanager | Verwaltet alle Webparts-Steuerelemente auf einer Seite. Für jede Webparts-Seite ist ein (und nur ein) **WebPartManager-Steuerelement** erforderlich. |
| Catalogzone | Enthält CatalogPart-Steuerelemente. Verwenden Sie diese Zone, um einen Katalog von Webparts-Steuerelementen zu erstellen, aus denen Benutzer Steuerelemente auswählen können, die einer Seite hinzugefügt werden sollen. |
| Editorzone | Enthält EditorPart-Steuerelemente. Verwenden Sie diese Zone, um Benutzern das Bearbeiten und Personalisieren von Webparts-Steuerelementen auf einer Seite zu ermöglichen. |
| Webpartzone | Enthält und stellt das Gesamtlayout für die WebPart-Steuerelemente bereit, aus denen die Hauptbenutzeroberfläche einer Seite besteht. Verwenden Sie diese Zone immer dann, wenn Sie Seiten mit Webparts-Steuerelementen erstellen. Seiten können eine oder mehrere Zonen enthalten. |
| Connectionszone | Enthält WebPartConnection-Steuerelemente und stellt eine Benutzeroberfläche zum Verwalten von Verbindungen bereit. |
| WebPart (GenericWebPart) | Rendert die primäre Benutzeroberfläche; Die meisten Webparts-UI-Steuerelemente fallen in diese Kategorie. Für maximale programmgesteuerte Steuerelemente können Sie benutzerdefinierte Webparts-Steuerelemente erstellen, die vom **Webpart-Basissteuerelement** stammen. Sie können auch vorhandene Serversteuerelemente, Benutzersteuerelemente oder benutzerdefinierte Steuerelemente als Webparts-Steuerelemente verwenden. Wenn eines dieser Steuerelemente in einer Zone platziert wird, umschließt das **WebPartManager-Steuerelement** sie zur Laufzeit automatisch mit **GenericWebPart-Steuerelementen,** sodass Sie sie mit Webparts-Funktionalität verwenden können. |
| Catalogpart | Enthält eine Liste der verfügbaren Webparts-Steuerelemente, die Benutzer der Seite hinzufügen können. |
| Webpartconnection | Erstellt eine Verbindung zwischen zwei Webparts-Steuerelementen auf einer Seite. Die Verbindung definiert eines der Webparts-Steuerelemente als Anbieter (von Daten) und das andere als Consumer. |
| Editorpart | Dient als Basisklasse für die spezialisierten Editorsteuerelemente. |
| EditorPart-Steuerelemente (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart und PropertyGridEditorPart) | Benutzern das Personalisieren verschiedener Aspekte von Webparts UI-Steuerelementen auf einer Seite ermöglichen |

## <a name="lab-create-a-web-part-page"></a>Übung: Erstellen einer Webpartseite

In dieser Übungseinheit erstellen Sie eine Webpartseite, die Informationen über ASP.NET Profile aufenthält.

### <a name="creating-a-simple-page-with-web-parts"></a>Erstellen einer einfachen Seite mit Webparts

In diesem Teil der exemplarischen Vorgehensweise erstellen Sie eine Seite, die Webparts-Steuerelemente verwendet, um statischen Inhalt anzuzeigen. Der erste Schritt bei der Arbeit mit Webparts besteht darin, eine Seite mit zwei erforderlichen Strukturelementen zu erstellen. Zunächst benötigt eine Webparts-Seite ein WebPartManager-Steuerelement, um alle Webparts-Steuerelemente nachzuverfolgen und zu koordinieren. Zweitens benötigt eine Webparts-Seite eine oder mehrere Zonen, bei denen es sich um zusammengesetzte Steuerelemente handelt, die WebPart- oder andere Serversteuerelemente enthalten und einen angegebenen Bereich einer Seite belegen.

> [!NOTE]
> Sie müssen nichts tun, um die Personalisierung von Webparts zu aktivieren. Sie ist standardmäßig für den Webparts-Steuerelementsatz aktiviert. Wenn Sie zum ersten Mal eine Webparts-Seite auf einer Website ausführen, richtet ASP.NET einen standardmäßigen Personalisierungsanbieter ein, um Benutzerpersonalisierungseinstellungen zu speichern. Weitere Informationen zur Personalisierung finden Sie unter Übersicht zur Personalisierung von Webparts.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>So erstellen Sie eine Seite zum Enthalten von Webparts-Steuerelementen

1. Schließen Sie die Standardseite, und fügen Sie der Website eine neue Seite mit dem Namen WebPartsDemo.aspx hinzu.
2. Wechseln Sie zur **Entwurfsansicht.**
3. Stellen Sie im Menü **Ansicht** sicher, dass die Optionen **Nicht-Visuelle Steuerelemente** und **Details** ausgewählt sind, damit Layout-Tags und Steuerelemente ohne Benutzeroberfläche angezeigt werden.
4. Platzieren Sie die `<div>` Einfügemarke vor den Tags auf der Entwurfsoberfläche, und drücken Sie die EINGABETASTE, um eine neue Zeile hinzuzufügen. Positionieren Sie die Einfügemarke vor dem neuen Zeilenzeichen, klicken Sie im Menü auf das Dropdown-Listensteuerelement Format **blockieren,** und wählen Sie die Option **Überschrift 1** aus. Fügen Sie in der Überschrift den Text **WebParts Demonstration Page**hinzu.
5. Ziehen Sie auf der Registerkarte **WebParts** der Toolbox ein **WebPartManager-Steuerelement** auf die Seite `<div>`und positionieren Sie es direkt nach dem neuen Zeilenzeichen und vor den Tags.   
  
   Das **WebPartManager-Steuerelement** rendert keine Ausgabe, daher wird es als graues Feld auf der Designeroberfläche angezeigt.
6. Positionieren Sie die `<div>` Einfügemarke innerhalb der Tags.
7. Klicken Sie im Menü **Layout** auf **Tabelle einfügen**, und erstellen Sie eine neue Tabelle mit einer Zeile und drei Spalten. Klicken Sie auf die Schaltfläche **Zelleneigenschaften,** wählen Sie **oben** aus der Dropdown-Liste **Vertikale Ausrichtung** aus, klicken Sie auf **OK**, und klicken Sie erneut auf **OK,** um die Tabelle zu erstellen.
8. Ziehen Sie ein WebPartZone-Steuerelement in die linke Tabellenspalte. Klicken Sie mit der rechten Maustaste auf das **WebPartZone-Steuerelement,** wählen Sie **Eigenschaften**aus, und legen Sie die folgenden Eigenschaften fest:   
  
   KENNe: SidebarZone   
  
   HeaderText: Seitenleiste
9. Ziehen Sie ein zweites **WebPartZone-Steuerelement** in die mittlere Tabellenspalte, und legen Sie die folgenden Eigenschaften fest:   
  
   KENNe: MainZone   
  
   HeaderText: Haupt
10. Speichern Sie die Datei .

Ihre Seite verfügt nun über zwei unterschiedliche Zonen, die Sie separat steuern können. Keine zone hat jedoch keinen Inhalt, daher ist das Erstellen von Inhalten der nächste Schritt. In dieser exemplarischen Vorgehensweise arbeiten Sie mit Webparts-Steuerelementen, die nur statischen Inhalt anzeigen.

Das Layout einer Webparts-Zone &lt;wird&gt; durch ein zonetemplate-Element angegeben. Innerhalb der Zonenvorlage können Sie eine beliebige ASP.NET-Steuerelement hinzufügen, unabhängig davon, ob es sich um ein benutzerdefiniertes Webparts-Steuerelement, ein Benutzersteuerelement oder ein vorhandenes Serversteuerelement handelt. Beachten Sie, dass Sie hier das Label-Steuerelement verwenden und dass Sie einfach statischen Text hinzufügen. Wenn Sie ein reguläres Serversteuerelement in einer **WebPartZone-Zone** platzieren, behandelt ASP.NET das Steuerelement zur Laufzeit als Webparts-Steuerelement, das Webparts-Features für das Steuerelement aktiviert.

**So erstellen Sie Inhalte für die Hauptzone**

1. Ziehen Sie in der **Entwurfsansicht** ein **Label-Steuerelement** von der **Registerkarte Standard** der Toolbox in den Inhaltsbereich der Zone, deren **ID-Eigenschaft** auf MainZone festgelegt ist.
2. Wechseln Sie zur **Quellansicht.** Beachten Sie, dass ein &lt;zonetemplate-Element&gt; hinzugefügt wurde, um das **Label-Steuerelement** in der MainZone zu umschließen.
3. Fügen Sie **title** dem &lt;asp:label-Element&gt; ein Attribut mit dem Namen titel hinzu, und legen Sie dessen Wert auf Inhalt fest. Entfernen Sie das Attribut Text="Label" aus dem &lt;asp:label-Element.&gt; Fügen Sie zwischen den &lt;öffnenden und&gt; schließenden Tags des asp:label-Elements Text hinzu, z. B. **Willkommen auf meiner Startseite** in einem Paar h2-Element-Tags. &lt;&gt; Ihr Code sollte wie folgt aussehen. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Speichern Sie die Datei .

Erstellen Sie als Nächstes ein Benutzersteuerelement, das der Seite auch als Webparts-Steuerelement hinzugefügt werden kann.

### <a name="to-create-a-user-control"></a>So erstellen Sie ein benutzerdefiniertes Steuerelement

1. Fügen Sie Ihrer Website ein neues Webbenutzersteuerelement hinzu, das als Suchsteuerelement dienen soll. Deaktivieren Sie die Option zum Platzieren von **Quellcode in einer separaten Datei**. Fügen Sie sie im selben Verzeichnis wie die Seite WebPartsDemo.aspx hinzu, und nennen Sie sie SearchUserControl.ascx.   
  
    > [!NOTE]
    > Das Benutzersteuerelement für diese exemplarische Vorgehensweise implementiert keine tatsächliche Suchfunktionalität. Es wird nur verwendet, um Webparts-Features zu demonstrieren.
2. Wechseln Sie zur **Entwurfsansicht.** Ziehen Sie auf der Registerkarte **Standard** der Toolbox ein TextBox-Steuerelement auf die Seite.
3. Platzieren Sie die Einfügemarke nach dem Textfeld, das Sie gerade hinzugefügt haben, und drücken Sie die EINGABETASTE, um eine neue Zeile hinzuzufügen.
4. Ziehen Sie ein Schaltflächensteuerelement auf das Zeichenblatt in der neuen Zeile unter dem Textfeld, das Sie gerade hinzugefügt haben.
5. Wechseln Sie zur **Quellansicht.** Stellen Sie sicher, dass der Quellcode für das Benutzersteuerelement wie im folgenden Beispiel aussieht. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Speichern und schließen Sie die Datei.

Jetzt können Sie Webparts-Steuerelemente zur Sidebar-Zone hinzufügen. Sie fügen der Sidebar-Zone zwei Steuerelemente hinzu, eines mit einer Liste von Links und ein anderes, das Benutzersteuerelement, das Sie im vorherigen Verfahren erstellt haben. Die Verknüpfungen werden **Label** als Standard-Label-Serversteuerelement hinzugefügt, ähnlich wie Sie den statischen Text für die Hauptzone erstellt haben. Obwohl die einzelnen Serversteuerelemente, die im Benutzersteuerelement enthalten sind, direkt in der Zone enthalten sein könnten (wie das Beschriftungssteuerelement), sind sie in diesem Fall nicht. Stattdessen sind sie Teil des Benutzersteuerelements, das Sie im vorherigen Verfahren erstellt haben. Dies veranschaulicht eine allgemeine Möglichkeit, steuerelemente und zusätzliche Funktionen, die Sie in einem Benutzersteuerelement verwenden möchten, zu verpacken und dann auf dieses Steuerelement in einer Zone als Webparts-Steuerelement zu verweisen.

Zur Laufzeit umschließt der Webparts-Steuerelementsatz beide Steuerelemente mit GenericWebPart-Steuerelementen. Wenn ein **GenericWebPart-Steuerelement** ein Webserversteuerelement umschließt, ist das generische Teilesteuerelement das übergeordnete Steuerelement, und Sie können über die ChildControl-Eigenschaft des übergeordneten Steuerelements auf das Serversteuerelement zugreifen. Diese Verwendung generischer Bauteilsteuerelemente ermöglicht standardwebserversteuerelementen das gleiche grundlegende Verhalten und dieselben Attribute wie Webparts-Steuerelemente, die von der **WebPart-Klasse** stammen.

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>So fügen Sie Webparts-Steuerelemente zur Seitenleistenzone hinzu

1. Öffnen Sie die Seite WebPartsDemo.aspx.
2. Wechseln Sie zur **Entwurfsansicht.**
3. Ziehen Sie die von Ihnen erstellte Benutzersteuerungsseite SearchUserControl.ascx aus dem **Projektmappen-Explorer** in die Zone, deren **ID-Eigenschaft** auf SidebarZone festgelegt ist, und legen Sie sie dort ab.
4. Speichern Sie die Seite WebPartsDemo.aspx.
5. Wechseln Sie zur **Quellansicht.**
6. Fügen &lt;Sie innerhalb des&gt; asp:webpartzone-Elements für die SidebarZone, &lt;direkt über&gt; dem Verweis auf Ihr Benutzersteuerelement, ein asp:label-Element mit enthaltenen Links hinzu, wie im folgenden Beispiel gezeigt. Fügen Sie dem Benutzersteuerelement-Tag außerdem ein **Title-Attribut** mit dem Wert **Search**hinzu, wie gezeigt. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Speichern und schließen Sie die Datei.

Jetzt können Sie Ihre Seite testen, indem Sie in Ihrem Browser zu ihr navigieren. Auf der Seite werden die beiden Zonen angezeigt. Der folgende Screenshot zeigt die Seite.

**Webparts Demoseite mit zwei Zonen**

![Webparts VS Walkthrough 1 Screenshot](profiles-themes-and-web-parts/_static/image3.gif)

**Abbildung 3:** Webparts VS Walkthrough 1 Screenshot

In der Titelleiste jedes Steuerelements befindet sich ein Pfeil nach unten, der Zugriff auf ein Verbenmenü mit verfügbaren Aktionen bietet, die Sie für ein Steuerelement ausführen können. Klicken Sie auf das Verbenmenü für eines der Steuerelemente, klicken Sie dann auf das Verb **Minimieren,** und beachten Sie, dass das Steuerelement minimiert ist. Klicken Sie im Verbenmenü auf **Wiederherstellen**, und das Steuerelement kehrt zu seiner normalen Größe zurück.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Benutzer können Seiten bearbeiten und Layout ändern

Webparts bietet Benutzern die Möglichkeit, das Layout von Webparts-Steuerelementen zu ändern, indem sie von einer Zone in eine andere gezogen werden. Zusätzlich zum Verschieben von **WebPart-Steuerelementen** von einer Zone in eine andere können Sie Benutzern das Bearbeiten verschiedener Merkmale der Steuerelemente ermöglichen, einschließlich ihrer Darstellung, ihres Layouts und ihres Verhaltens. Der Webparts-Steuerelementsatz bietet grundlegende Bearbeitungsfunktionen für **WebPart-Steuerelemente.** Obwohl Sie dies in dieser exemplarischen Vorgehensweise nicht tun, können Sie auch benutzerdefinierte Editorsteuerelemente erstellen, mit denen Benutzer die Features von **WebPart-Steuerelementen** bearbeiten können. Wie beim Ändern der Position eines **WebPart-Steuerelements** basiert das Bearbeiten der Eigenschaften eines Steuerelements auf ASP.NET Personalisierung, um die von Benutzern vorgenommenen Änderungen zu speichern.

In diesem Teil der exemplarischen Vorgehensweise fügen Sie Benutzern die Möglichkeit hinzu, die grundlegenden Eigenschaften eines **WebPart-Steuerelements** auf der Seite zu bearbeiten. Um diese Features zu aktivieren, fügen Sie der Seite &lt;ein weiteres&gt; benutzerdefiniertes Benutzersteuerelement sowie ein asp:editorzone-Element und zwei Bearbeitungssteuerelemente hinzu.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>So erstellen Sie ein Benutzersteuerelement, das das Ändern des Seitenlayouts ermöglicht

1. Wählen Sie in Visual Studio im Menü **Datei** das Untermenü **Neu** aus, und klicken Sie auf die Option **Datei.**
2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **Webbenutzersteuerung**aus. Benennen Sie die neue Datei DisplayModeMenu.ascx. Deaktivieren Sie die Option zum Platzieren von **Quellcode in einer separaten Datei**.
3. Klicken Sie auf Hinzufügen, um das neue Steuerelement zu erstellen.
4. Wechseln Sie zur **Quellansicht.**
5. Entfernen Sie den gesamten vorhandenen Code in der neuen Datei, und fügen Sie den folgenden Code ein. Dieser Benutzersteuerungscode verwendet Features des Webparts-Steuerelementsatzes, mit denen eine Seite ihre Ansicht oder den Anzeigemodus ändern kann, und ermöglicht es Ihnen außerdem, das physische Erscheinungsbild und Layout der Seite zu ändern, während Sie sich in bestimmten Anzeigemodi befinden. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Speichern Sie die Datei, indem Sie auf das Symbol speichern auf der Symbolleiste klicken oder im Menü **Datei** **speichern** auswählen.

### <a name="to-enable-users-to-change-the-layout"></a>So ermöglichen Sie Benutzern, das Layout zu ändern

1. Öffnen Sie die Seite WebPartsDemo.aspx, und wechseln Sie zur **Entwurfsansicht.**
2. Positionieren Sie die Einfügemarke in der **Entwurfsansicht** direkt hinter dem **WebPartManager-Steuerelement,** das Sie zuvor hinzugefügt haben. Fügen Sie nach dem Text eine harte Rückgabe hinzu, sodass nach dem **WebPartManager-Steuerelement** eine leere Zeile vorhanden ist. Platzieren Sie die Einfügemarke auf der leeren Zeile.
3. Ziehen Sie das soeben erstellte Benutzersteuerelement (die Datei heißt DisplayModeMenu.ascx) auf die Seite WebPartsDemo.aspx, und legen Sie es in der leeren Zeile ab.
4. Ziehen Sie ein EditorZone-Steuerelement aus dem **WebParts-Abschnitt** der Toolbox in die verbleibende geöffnete Tabellenzelle auf der Seite WebPartsDemo.aspx.
5. Ziehen Sie im Abschnitt **WebParts** der Toolbox ein AppearanceEditorPart-Steuerelement und ein LayoutEditorPart-Steuerelement in das **EditorZone-Steuerelement.**
6. Wechseln Sie zur **Quellansicht.** Der resultierende Code in der Tabellenzelle sollte dem folgenden Code ähnlich aussehen. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. Speichern Sie die Datei WebPartsDemo.aspx. Sie haben ein Benutzersteuerelement erstellt, mit dem Sie anzeigemodi ändern und das Seitenlayout ändern können, und Sie haben auf das Steuerelement auf der primären Webseite verwiesen.

Sie können jetzt die Möglichkeit zum Bearbeiten von Seiten und Ändern des Layouts testen.

### <a name="to-test-layout-changes"></a>So testen Sie Layoutänderungen

1. Laden Sie die Seite in einen Browser.
2. Klicken Sie auf das Dropdown-Menü **Anzeigemodus,** und wählen Sie **Bearbeiten**aus. Die Zonentitel werden angezeigt.
3. Ziehen Sie das **Steuerelement "Meine Links"** über die Titelleiste von der Sidebar-Zone an den unteren Rand der Hauptzone. Ihre Seite sollte wie der folgende Screenshot aussehen.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Webparts Demo-Seite mit My Links-Steuerelement verschoben

![Webparts VS Walkthrough 2 Screenshot](profiles-themes-and-web-parts/_static/image4.gif)

**Abbildung 4:** Webparts VS Walkthrough 2 Screenshot

1. Klicken Sie auf das Dropdown-Menü **Anzeigemodus,** und wählen Sie **Durchsuchen**aus. Die Seite wird aktualisiert, die Zonennamen werden ausgeblendet, und das Steuerelement **"Meine Links"** bleibt an der Stelle, an der Sie sie positioniert haben.
2. Um zu demonstrieren, dass die Personalisierung funktioniert, schließen Sie den Browser, und laden Sie die Seite erneut. Die von Ihnen vorgenommenen Änderungen werden für zukünftige Browsersitzungen gespeichert.
3. Wählen Sie im Menü **Anzeigemodus** die Option **Bearbeiten**aus.   
  
   Jedes Steuerelement auf der Seite wird nun mit einem Abwärtspfeil in der Titelleiste angezeigt, der das Dropdown-Menü der Verben enthält.
4. Klicken Sie auf den Pfeil, um das Verbenmenü im Steuerelement **"Meine Links"** anzuzeigen. Klicken Sie auf das Verb **Bearbeiten.**   
  
   Das **EditorZone-Steuerelement** wird angezeigt und zeigt die von Ihnen hinzugefügten EditorPart-Steuerelemente an.
5. Ändern Sie im Abschnitt **Erscheinungsbild** des Bearbeitungssteuerelements den **Titel** in Meine Favoriten, verwenden Sie die Dropdownliste **Chrome Type,** um **Titel nur**auszuwählen, und klicken Sie dann auf **Übernehmen**. Der folgende Screenshot zeigt die Seite im Bearbeitungsmodus an.

### <a name="web-parts-demo-page-in-edit-mode"></a>Webparts-Demoseite im Bearbeitungsmodus

![Webparts VS Walkthrough 3 Screenshot](profiles-themes-and-web-parts/_static/image5.gif)

**Abbildung 5:** Webparts VS Walkthrough 3 Screenshot

1. Klicken Sie auf das Menü **Anzeigemodus,** und wählen Sie **Durchsuchen** aus, um in den Suchmodus zurückzukehren.
2. Das Steuerelement hat nun einen aktualisierten Titel und keinen Rahmen, wie im folgenden Screenshot gezeigt.

### <a name="edited-web-parts-demo-page"></a>Bearbeitete Webparts-Demoseite

![Webparts VS Walkthrough 4 Screenshot](profiles-themes-and-web-parts/_static/image6.gif)

**Abbildung 4:** Webparts VS Walkthrough 4 Screenshot

### <a name="adding-web-parts-at-run-time"></a>Hinzufügen von Webparts zur Laufzeit

Sie können Benutzern auch erlauben, Webparts-Steuerelemente zur Laufzeit zu ihrer Seite hinzuzufügen. Konfigurieren Sie dazu die Seite mit einem Webparts-Katalog, der eine Liste der Webparts-Steuerelemente enthält, die Benutzern zur Verfügung gestellt werden sollen.

**So ermöglichen Sie Benutzern das Hinzufügen von Webparts zur Laufzeit**

1. Öffnen Sie die Seite WebPartsDemo.aspx, und wechseln Sie zur **Entwurfsansicht.**
2. Ziehen Sie auf der Registerkarte **WebParts** der Toolbox ein CatalogZone-Steuerelement in die rechte Spalte der Tabelle unter dem **EditorZone-Steuerelement.**   
  
   Beide Steuerelemente können sich in derselben Tabellenzelle befinden, da sie nicht gleichzeitig angezeigt werden.
3. Weisen Sie im Eigenschaftenbereich der HeaderText-Eigenschaft des **CatalogZone-Steuerelements** die Zeichenfolge **Webparts hinzufügen** zu.
4. Ziehen Sie im Abschnitt **WebParts** der Toolbox ein DeclarativeCatalogPart-Steuerelement in den Inhaltsbereich des **CatalogZone-Steuerelements.**
5. Klicken Sie auf den Pfeil in der oberen rechten Ecke des **DeklarativeCatalogPart-Steuerelements,** um das Menü "Aufgaben" verfügbar zu machen, und wählen Sie dann **Vorlagen bearbeiten**aus.
6. Ziehen Sie im **Abschnitt Standard** der Toolbox ein **FileUpload-Steuerelement** und ein **Kalendersteuerelement** in den **WebPartsTemplate-Abschnitt** des **DeklarativeCatalogPart-Steuerelements.**
7. Wechseln Sie zur **Quellansicht.** Überprüfen Sie den &lt;Quellcode des asp:catalogzone-Elements.&gt; Beachten Sie, dass das **DeklarativeCatalogPart-Steuerelement** ein &lt;webpartstemplate-Element&gt; mit den beiden eingeschlossenen Serversteuerelementen enthält, die Sie Ihrer Seite aus dem Katalog hinzufügen können.
8. Fügen Sie jedem Steuerelement, das Sie dem Katalog hinzugefügt haben, eine **Title-Eigenschaft** hinzu, wobei der Zeichenfolgenwert für jeden Titel im Codebeispiel unten verwendet wird. Auch wenn der Titel keine Eigenschaft ist, die Sie normalerweise auf diesen beiden Serversteuerelementen zur Entwurfszeit festlegen können, werden sie, wenn ein Benutzer diese Steuerelemente zur Laufzeit einer **WebPartZone-Zone** aus dem Katalog hinzufügt, jeweils mit einem **GenericWebPart-Steuerelement** umschlossen. Dadurch können sie als Webparts-Steuerelemente fungieren, sodass sie Titel anzeigen können.   
  
   Der Code für die beiden Steuerelemente, die im **DeklarativeCatalogPart-Steuerelement** enthalten sind, sollte wie folgt aussehen. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Speichern Sie die Seite.

Sie können den Katalog jetzt testen.

### <a name="to-test-the-web-parts-catalog"></a>So testen Sie den Webparts-Katalog

1. Laden Sie die Seite in einen Browser.
2. Klicken Sie auf das Dropdown-Menü **Anzeigemodus,** und wählen Sie **Katalog**aus.   
  
   Der Katalog mit dem Titel **Webparts hinzufügen** wird angezeigt.
3. Ziehen Sie das Steuerelement **Meine Favoriten** aus der Hauptzone zurück an den oberen Rand der Sidebar-Zone, und legen Sie es dort ab.
4. Aktivieren Sie im Katalog **Webparts hinzufügen** beide Kontrollkästchen, und wählen Sie dann In der Dropdownliste, die die verfügbaren Zonen enthält, **Main** aus.
5. Klicken Sie im Katalog auf **Hinzufügen.** Die Steuerelemente werden der Hauptzone hinzugefügt. Wenn Sie möchten, können Sie Ihrer Seite mehrere Instanzen von Steuerelementen aus dem Katalog hinzufügen.   
  
   Der folgende Screenshot zeigt die Seite mit dem Datei-Upload-Steuerelement und den Kalender in der Hauptzone. 

![Steuerelemente, die der Hauptzone aus dem Katalog hinzugefügt wurden](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. Klicken Sie auf das Dropdown-Menü **Anzeigemodus,** und wählen Sie **Durchsuchen**aus. Der Katalog wird ausgeblendet, und die Seite wird aktualisiert.
7. Schließen Sie den Browser. Laden Sie die Seite erneut. Die von Ihnen vorgenommenen Änderungen bleiben bestehen.
