---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Konfiguration und Instrumentierung | Microsoft Docs
author: rick-anderson
description: In ASP.NET 2.0 gibt es wesentliche Änderungen in Der Konfiguration und Instrumentierung. Die neue ASP.NET Konfigurations-API ermöglicht Konfigurationsänderungen pr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543053"
---
# <a name="configuration-and-instrumentation"></a>Konfiguration und Instrumentierung

von [Microsoft](https://github.com/microsoft)

> In ASP.NET 2.0 gibt es wesentliche Änderungen in Der Konfiguration und Instrumentierung. Die neue ASP.NET Konfigurations-API ermöglicht programmgesteuerte Konfigurationsänderungen. Darüber hinaus gibt es viele neue Konfigurationseinstellungen, die neue Konfigurationen und Instrumentierung ermöglichen.

In ASP.NET 2.0 gibt es wesentliche Änderungen in Der Konfiguration und Instrumentierung. Die neue ASP.NET Konfigurations-API ermöglicht programmgesteuerte Konfigurationsänderungen. Darüber hinaus gibt es viele neue Konfigurationseinstellungen, die neue Konfigurationen und Instrumentierung ermöglichen.

In diesem Modul werden wir ASP.NET der Konfigurations-API in Bezug auf das Lesen von und Das Schreiben in ASP.NET Konfigurationsdateien besprechen, und wir werden auch ASP.NET Instrumentierung behandeln. Wir werden auch die neuen Funktionen in ASP.NET Verfolgung behandeln.

## <a name="aspnet-configuration-api"></a>ASP.NET-Konfigurations-API

Mit der ASP.NET-Konfigurations-API können Sie Anwendungskonfigurationsdaten mithilfe einer einzigen Programmierschnittstelle entwickeln, bereitstellen und verwalten. Sie können die Konfigurations-API verwenden, um vollständige ASP.NET Konfigurationen programmgesteuert zu entwickeln und zu ändern, ohne den XML-Code in den Konfigurationsdateien direkt zu bearbeiten. Darüber hinaus können Sie die Konfigurations-API in Konsolenanwendungen und Skripts verwenden, die Sie entwickeln, in webbasierten Verwaltungstools und in Microsoft Management Console (MMC)-Snap-Ins.

Die folgenden beiden Konfigurationsverwaltungstools verwenden die Konfigurations-API und sind in der .NET Framework Version 2.0 enthalten:

- Das ASP.NET MMC-Snap-In, das die Konfigurations-API verwendet, um Verwaltungsaufgaben zu vereinfachen und eine integrierte Ansicht der lokalen Konfigurationsdaten von allen Ebenen der Konfigurationshierarchie bereitstellt.
- Das Websiteverwaltungstool, mit dem Sie Konfigurationseinstellungen für lokale und Remoteanwendungen, einschließlich gehosteter Websites, verwalten können.

Die ASP.NET Konfigurations-API umfasst eine Reihe von ASP.NET Verwaltungsobjekten, mit denen Sie Websites und Anwendungen programmgesteuert konfigurieren können. Verwaltungsobjekte werden als .NET Framework-Klassenbibliothek implementiert. Das Konfigurations-API-Programmiermodell trägt zur Gewährleistung von Codekonsistenz und -zuverlässigkeit bei, indem Datentypen zur Kompilierungszeit erzwungen werden. Um die Verwaltung von Anwendungskonfigurationen zu vereinfachen, können Sie mit der Konfigurations-API Daten anzeigen, die von allen Punkten in der Konfigurationshierarchie als einzelne Auflistung zusammengeführt werden, anstatt die Daten als separate Sammlungen aus verschiedenen Konfigurationsdateien anzuzeigen. Darüber hinaus können Sie mit der Konfigurations-API ganze Anwendungskonfigurationen bearbeiten, ohne den XML-Code in den Konfigurationsdateien direkt zu bearbeiten. Schließlich vereinfacht die API Konfigurationsaufgaben, indem Sie Verwaltungstools wie das Websiteverwaltungstool unterstützen. Die Konfigurations-API vereinfacht die Bereitstellung, indem sie die Erstellung von Konfigurationsdateien auf einem Computer unterstützt und Konfigurationsskripts auf mehreren Computern ausführt.

> [!NOTE]
> Die Konfigurations-API unterstützt die Erstellung von IIS-Anwendungen nicht.

## <a name="working-with-local-and-remote-configuration-settings"></a>Arbeiten mit lokalen und Remotekonfigurationseinstellungen

Ein Konfigurationsobjekt stellt die zusammengeführte Ansicht der Konfigurationseinstellungen dar, die für eine bestimmte physische Entität, z. B. einen Computer, oder für eine logische Entität, z. B. eine Anwendung oder eine Website, gelten. Die angegebene logische Entität kann auf dem lokalen Computer oder auf einem Remoteserver vorhanden sein. Wenn für eine angegebene Entität keine Konfigurationsdatei vorhanden ist, stellt das Configuration-Objekt die Standardkonfigurationseinstellungen dar, die von der Datei Machine.config definiert sind.

Sie können ein Configuration-Objekt abrufen, indem Sie eine der offenen Konfigurationsmethoden aus den folgenden Klassen verwenden:

1. Die ConfigurationManager-Klasse, wenn es sich bei Ihrer Entität um eine Clientanwendung handelt.
2. Die WebConfigurationManager-Klasse, wenn es sich bei Ihrer Entität um eine Webanwendung handelt.

Diese Methoden geben ein Configuration-Objekt zurück, das wiederum die erforderlichen Methoden und Eigenschaften bereitstellt, um die zugrunde liegenden Konfigurationsdateien zu behandeln. Sie können auf diese Dateien zum Lesen oder Schreiben zugreifen.

### <a name="reading"></a>Lesen

Sie verwenden die GetSection- oder GetSectionGroup-Methode, um Konfigurationsinformationen zu lesen. Der Benutzer oder Prozess, der liest, muss über Leseberechtigungen für alle Konfigurationsdateien in der Hierarchie verfügen.

> [!NOTE]
> Wenn Sie eine statische GetSection-Methode verwenden, die einen Pfadparameter verwendet, muss der Pfadparameter auf die Anwendung verweisen, in der der Code ausgeführt wird. Andernfalls wird der Parameter ignoriert, und die Konfigurationsinformationen für die aktuell ausgeführte Anwendung werden zurückgegeben.

### <a name="writing"></a>Schreiben

Sie verwenden eine der Save-Methoden, um Konfigurationsinformationen zu schreiben. Der Benutzer oder Prozess, der schreibt, muss über Schreibberechtigungen für die Konfigurationsdatei und das Verzeichnis auf der aktuellen Konfigurationshierarchieebene sowie über Leseberechtigungen für alle Konfigurationsdateien in der Hierarchie verfügen.

Um eine Konfigurationsdatei zu generieren, die die geerbten Konfigurationseinstellungen für eine angegebene Entität darstellt, verwenden Sie eine der folgenden Methoden zur Speicherkonfiguration:

1. Die Save-Methode zum Erstellen einer neuen Konfigurationsdatei.
2. Die SaveAs-Methode zum Generieren einer neuen Konfigurationsdatei an einem anderen Speicherort.

## <a name="configuration-classes-and-namespaces"></a>Konfigurationsklassen und Namespaces

Viele Konfigurationsklassen und -methoden ähneln einander. In der folgenden Tabelle werden die am häufigsten verwendeten Konfigurationsklassen und Namespaces beschrieben.

| **Konfigurationsklasse oder Namespace** | **Beschreibung** |
| --- | --- |
| [System.Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) Namespace | Enthält die Hauptkonfigurationsklassen für alle .NET Framework-Anwendungen. Abschnittshandlerklassen werden verwendet, um Konfigurationsdaten für einen Abschnitt aus Methoden wie GetSection und GetSectionGroup abzuholen. Diese beiden Methoden sind nicht statisch. |
| System.Configuration.Configuration-Klasse | Stellt einen Satz von Konfigurationsdaten für einen Computer, eine Anwendung, ein Webverzeichnis oder eine andere Ressource dar. Diese Klasse enthält nützliche Methoden, z. B. GetSection und GetSectionGroup, um Konfigurationseinstellungen zu aktualisieren und Verweise auf Abschnitte und Abschnittsgruppen abzuverweisen. Diese Klasse wird als Rückgabetyp für Methoden verwendet, die Entwurfszeitkonfigurationsdaten abrufen, z. B. die Methoden der WebConfigurationManager- und ConfigurationManager-Klassen. |
| System.Web.Configuration-Namespace | Enthält die Abschnittshandlerklassen für die ASP.NET Konfigurationsabschnitte, die unter [ASP.NET Konfigurationseinstellungen](https://msdn.microsoft.com/library/b5ysx397.aspx)definiert sind. Abschnittshandlerklassen werden verwendet, um Konfigurationsdaten für einen Abschnitt aus Methoden wie GetSection und GetSectionGroup abzuholen. |
| System.Web.Configuration.WebConfigurationManager-Klasse | Enthält nützliche Methoden zum Abrufen von Verweisen auf Konfigurationseinstellungen für Laufzeit und Entwurfszeit. Diese Methoden verwenden die System.Configuration.Configuration-Klasse als Rückgabetyp. Sie können die statische GetSection-Methode dieser Klasse oder die nicht statische GetSection-Methode der System.Configuration.ConfigurationManager-Klasse austauschbar verwenden. Für Webanwendungskonfigurationen wird anstelle der System.Configuration.ConfigurationManager-Klasse die System.Web.Configuration.WebConfigurationManager-Klasse empfohlen. |
| [System.Configuration.Provider-Namespace](https://msdn.microsoft.com/library/system.configuration.provider.aspx) | Bietet eine Möglichkeit zum Anpassen und Erweitern des Konfigurationsanbieters. Dies ist die Basisklasse für alle Anbieterklassen im Konfigurationssystem. |
| [System.Web.Management-Namespace](https://msdn.microsoft.com/library/system.web.management.aspx) | Enthält Klassen und Schnittstellen zum Verwalten und Überwachen der Integrität von Webanwendungen. Genau genommen wird dieser Namespace nicht als Teil der Konfigurations-API betrachtet. Beispielsweise wird die Ablaufverfolgung und das Auslösen von Ereignis durch die Klassen in diesem Namespace durchgeführt. |
| [System.Management.Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) Namespace | Stellt die Klassen bereit, die für die Instrumentierung von Anwendungen erforderlich sind, um ihre Verwaltungsinformationen und Ereignisse über Windows Management Instrumentation (WMI) potenziellen Verbrauchern zur Verfügung zu stellen. ASP.NET-Gesundheitsüberwachung verwendet WMI, um Ereignisse zu liefern. Genau genommen wird dieser Namespace nicht als Teil der Konfigurations-API betrachtet. |

## <a name="reading-from-aspnet-configuration-files"></a>Lesen aus ASP.NET Konfigurationsdateien

Die WebConfigurationManager-Klasse ist die Kernklasse zum Lesen aus ASP.NET Konfigurationsdateien. Es gibt im Wesentlichen drei Schritte zum Lesen ASP.NET Konfigurationsdateien:

1. Abrufen eines Configuration-Objekts mithilfe der OpenWebConfiguration-Methode.
2. Hier erhalten Sie einen Verweis auf den gewünschten Abschnitt in der Konfigurationsdatei.
3. Lesen Sie die gewünschten Informationen aus der Konfigurationsdatei.

Das Configuration-Objekt stellt keine bestimmte Konfigurationsdatei dar. Stattdessen stellt sie eine zusammengeführte Ansicht der Konfiguration eines Computers, einer Anwendung oder einer Website dar. Im folgenden Codebeispiel wird ein Configuration-Objekt instanziiert, das die Konfiguration einer Webanwendung namens *ProductInfo*darstellt.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> Wenn der Pfad /ProductInfo nicht vorhanden ist, gibt der obige Code die Ineinstellung in der Datei machine.config angegebenen Standardkonfiguration zurück.

Sobald Sie über das Configuration-Objekt verfügen, können Sie die GetSection- oder GetSectionGroup-Methode verwenden, um einen Drilldown in die Konfigurationseinstellungen zu führen. Im folgenden Beispiel wird ein Verweis auf die Identitätswechseleinstellungen für die oben genannte ProductInfo-Anwendung ab:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>Schreiben in ASP.NET Konfigurationsdateien

Wie beim Lesen aus Konfigurationsdateien ist die WebConfigurationManager-Klasse der Kern für das Schreiben in Asp.NET Konfigurationsdateien. Es gibt auch drei Schritte zum Schreiben in ASP.NET Konfigurationsdateien.

1. Abrufen eines Configuration-Objekts mithilfe der OpenWebConfiguration-Methode.
2. Hier erhalten Sie einen Verweis auf den gewünschten Abschnitt in der Konfigurationsdatei.
3. Schreiben Sie die gewünschten Informationen aus der Konfigurationsdatei mit der Save- oder SaveAs-Methode.

Der folgende Code ändert das &lt;&gt; **Debugattribut** des Kompilierungselements in false:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Wenn dieser Code ausgeführt wird, wird &lt;&gt; das **Debug-Attribut** des Kompilierungselements für die web.config-Datei der *webApp-Anwendung* auf false gesetzt.

## <a name="systemwebmanagement-namespace"></a>System.Web.Management-Namespace

Der Namespace System.Web.Management stellt die Klassen und Schnittstellen zum Verwalten und Überwachen des Zustands ASP.NET Anwendungen bereit.

Die Protokollierung erfolgt durch Definieren einer Regel, die Ereignisse einem Anbieter zuordnet. Die Regel definiert den Typ der Ereignisse, die an den Anbieter gesendet werden. Die folgenden Basisereignisse stehen Ihnen zum Protokollieren zur Verfügung:

| **Webbaseevent** | Die Basisereignisklasse für alle Ereignisse. Enthält die erforderlichen Eigenschaften für alle Ereignisse wie Ereigniscode, Ereignisdetailcode, Datum und Uhrzeit der Ausweichanzeige des Ereignisses, Sequenznummer, Ereignismeldung und Ereignisdetails. |
| --- | --- |
| **Webmanagementevent** | Die Basisereignisklasse für Verwaltungsereignisse, z. B. Anwendungslebensdauer, Anforderung, Fehler und Überwachungsereignisse. |
| **WebHeartbeatEvent** | Das Ereignis, das von der Anwendung in regelmäßigen Abständen generiert wird, um nützliche Laufzeitstatusinformationen zu erfassen. |
| **Webauditevent** | Die Basisklasse für Sicherheitsüberwachungsereignisse, die zum Markieren von Bedingungen wie Autorisierungsfehler, Entschlüsselungsfehler usw. verwendet *werden.* |
| **Webrequestevent** | Die Basisklasse für alle Informationsanforderungsereignisse. |
| **Webbaseerrorevent** | Die Basisklasse für alle Ereignisse, die Fehlerbedingungen anzeigen. |

Mit den verfügbaren Anbietertypen können Sie die Ereignisausgabe an Die Ereignisanzeige, SQL Server, Windows Management Instrumentation (WMI) und E-Mail senden. Die vorkonfigurierten Anbieter und Ereigniszuordnungen reduzieren den Arbeitsaufwand, der erforderlich ist, um die Ereignisausgabe protokollieren zu lassen.

ASP.NET 2.0 verwendet den sofort einsatzbereiten Ereignisprotokollanbieter, um Ereignisse basierend auf dem Starten und Beenden von Anwendungsdomänen zu protokollieren und alle nicht behandelten Ausnahmen zu protokollieren. Dies hilft, einige der grundlegenden Szenarien abzudecken. Angenommen, Ihre Anwendung löst eine Ausnahme aus, aber der Benutzer speichert den Fehler nicht und Sie können ihn nicht reproduzieren. Mit der Standardregel Ereignisprotokoll können Sie die Ausnahme- und Stapelinformationen sammeln, um eine bessere Vorstellung davon zu erhalten, welche Art von Fehler aufgetreten ist. Ein weiteres Beispiel gilt, wenn die Anwendung den Sitzungsstatus verliert. In diesem Fall können Sie im Ereignisprotokoll nachsehen, ob die Anwendungsdomäne wiedergegeben wird und warum die Anwendungsdomäne überhaupt beendet wurde.

Außerdem ist das Gesundheitsüberwachungssystem erweiterbar. Sie können z. B. benutzerdefinierte Webereignisse definieren, sie in Ihrer Anwendung ausrichten und dann eine Regel definieren, um die Ereignisinformationen an einen Anbieter wie Ihre E-Mail zu senden. So können Sie Ihre Instrumentierung einfach an die Gesundheitsüberwachungsanbieter binden. Als weiteres Beispiel können Sie jedes Mal, wenn ein Auftrag verarbeitet wird, ein Ereignis aussenden und eine Regel einrichten, die jedes Ereignis an die SQL Server-Datenbank sendet. Sie können auch ein Ereignis ausschalten, wenn sich ein Benutzer nicht mehrmals hintereinander anmeldet, und das Ereignis so einrichten, dass die E-Mail-basierten Anbieter verwendet werden.

Die Konfiguration für die Standardanbieter und -ereignisse wird in der globalen Datei Web.config gespeichert. Die globale Web.config-Datei speichert alle webbasierten Einstellungen, die in der Datei Machine.config in ASP.NET 1x gespeichert wurden. Die globale Datei Web.config befindet sich im folgenden Verzeichnis:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

Der &lt;Abschnitt&gt; healthMonitoring der globalen Web.config-Datei stellt Standardkonfigurationseinstellungen bereit. Sie können diese Einstellung überschreiben oder ihre &lt;eigenen&gt; Einstellungen konfigurieren, indem Sie den Abschnitt healthMonitoring in der Datei Web.config für Ihre Anwendung implementieren.

Der &lt;Abschnitt&gt; healthMonitoring der globalen Datei Web.config enthält die folgenden Elemente:

| **providers** | Enthält Anbieter, die für die Ereignisanzeige, WMI und SQL Server eingerichtet sind. |
| --- | --- |
| **Eventmappings** | Enthält Zuordnungen für die verschiedenen WebBase-Klassen. Sie können diese Liste erweitern, wenn Sie eine eigene Ereignisklasse generieren. Wenn Sie eine eigene Ereignisklasse generieren, erhalten Sie eine feinere Granularität gegenüber den Anbietern, an die Sie Informationen senden. Sie können z. B. nicht behandelte Ausnahmen so konfigurieren, dass sie an SQL Server gesendet werden, während Sie Ihre eigenen benutzerdefinierten Ereignisse per E-Mail senden. |
| **Regeln** | Verknüpft die eventMappings mit dem Anbieter. |
| **Pufferung** | Wird mit SQL Server und E-Mail-Anbietern verwendet, um zu bestimmen, wie oft die Ereignisse an den Anbieter gelöscht werden sollen. |

Im Folgenden finden Sie ein Codebeispiel aus der globalen Datei Web.config.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>So speichern Sie Ereignisse in der Ereignisanzeige

Wie bereits erwähnt, ist der Anbieter für die Protokollierung von Ereignissen in der Ereignisanzeige für Sie in der globalen Datei Web.config konfiguriert. Standardmäßig werden alle Ereignisse, die auf **WebBaseErrorEvent** und **WebFailureAuditEvent** basieren, protokolliert. Sie können zusätzliche Regeln hinzufügen, um zusätzliche Informationen im Ereignisprotokoll zu protokollieren. Wenn Sie z. B. alle Ereignisse (*d. h.* jedes Ereignis basierend auf **WebBaseEvent )** protokollieren möchten, können Sie der Web.config-Datei die folgende Regel hinzufügen:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Diese Regel würde die **Ereigniszuordnung "Alle Ereignisse"** mit dem Ereignisprotokollanbieter verknüpfen. Sowohl eventMapping als auch der Anbieter sind in der globalen Datei Web.config enthalten.

## <a name="how-to-store-events-to-sql-server"></a>Speichern von Ereignissen in SQL Server

Diese Methode verwendet die **ASPNETDB-Datenbank,** die\_vom Werkzeug Aspnet regsql.exe generiert wird. Der Standardanbieter verwendet die LokaleSqlServer-Verbindungszeichenfolge, die entweder eine\_dateibasierte Datenbank im App-Datenordner oder die lokale SQLExpress-Instanz von SQL Server verwendet. Sowohl die LocalSqlServer-Verbindungszeichenfolge als auch der SqlProvider werden in der globalen Web.config-Datei konfiguriert.

Die LocalSqlServer-Verbindungszeichenfolge in der globalen Web.config-Datei sieht wie folgt aus:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Wenn Sie eine andere SQL Server-Instanz verwenden möchten, müssen\_Sie das Tool Aspnet regsql.exe verwenden, das sie im %windir%-Microsoft.Net-Framework-v2.0 finden. \* Ordner. Verwenden Sie das\_Tool Aspnet regsql.exe, um eine benutzerdefinierte **ASPNETDB-Datenbank** auf der SQL Server-Instanz zu generieren, dann die Verbindungszeichenfolge zu Ihrer Anwendungskonfigurationsdatei hinzuzufügen und dann mithilfe der neuen Verbindungszeichenfolge einen Anbieter hinzuzufügen. Nachdem Sie die **ASPNETDB-Datenbank** erstellt haben, müssen Sie eine Regel festlegen, um eine eventMapping mit dem sqlProvider zu verknüpfen.

Unabhängig davon, ob Sie den Standardmäßigen SqlProvider verwenden oder Ihren eigenen Anbieter konfigurieren, müssen Sie eine Regel hinzufügen, die den Anbieter mit einer Ereigniszuordnung verknüpft. Die folgende Regel verknüpft den neuen Anbieter, den Sie oben erstellt haben, mit der **Ereigniszuordnung Alle Ereignisse.** Diese Regel protokolliert alle Ereignisse basierend auf **WebBaseEvent** und sendet sie an den MySqlWebEventProvider, der die MYASPNETDB-Verbindungszeichenfolge verwendet. Der folgende Code fügt eine Regel hinzu, um den Anbieter mit einer Ereigniszuordnung zu verknüpfen:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Wenn Sie nur Fehler an SQL Server senden möchten, können Sie die folgende Regel hinzufügen:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Wie man Ereignisse an WMI weiterleitet

Sie können die Ereignisse auch an WMI weiterleiten. Der WMI-Anbieter ist standardmäßig für Sie in der globalen Web.config-Datei konfiguriert.

Im folgenden Codebeispiel wird eine Regel zum Weiterleiten der Ereignisse an WMI hinzugefügt:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Sie müssen eine Regel hinzufügen, um dem Anbieter eine eventMapping-Zuordnung zuzuordnen, sowie eine WMI-Listeneranwendung, um die Ereignisse zu hören. Im folgenden Codebeispiel wird eine Regel hinzugefügt, um den WMI-Anbieter mit der **Ereigniszuordnung "Alle Ereignisse"** zu verknüpfen:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>So leiten Sie Ereignisse per E-Mail weiter

Sie können Ereignisse auch per E-Mail weiterleiten. Seien Sie vorsichtig, welche Ereignisregeln Sie Ihrem E-Mail-Anbieter zuordnen, da Sie sich unbeabsichtigt viele Informationen senden können, die möglicherweise besser für SQL Server oder das Ereignisprotokoll geeignet sind. Es gibt zwei E-Mail-Anbieter; SimpleMailWebEventProvider und TemplatedMailWebEventProvider. Jedes verfügt über dieselben Konfigurationsattribute, mit Ausnahme der Attribute "template" und "detailedTemplateErrors", die beide nur auf dem TemplatedMailWebEventProvider verfügbar sind.

> [!NOTE]
> Keiner dieser E-Mail-Anbieter ist für Sie konfiguriert. Sie müssen sie Ihrer Web.config-Datei hinzufügen.

Der Hauptunterschied zwischen diesen beiden E-Mail-Anbietern besteht darin, dass SimpleMailWebEventProvider E-Mails in einer generischen Vorlage sendet, die nicht geändert werden kann. Die Beispieldatei Web.config fügt diesen E-Mail-Anbieter mithilfe der folgenden Regel zur Liste der konfigurierten Anbieter hinzu:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

Die folgende Regel wird auch hinzugefügt, um den E-Mail-Anbieter an die **Ereigniszuordnung "Alle Ereignisse"** zu binden:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 Ablaufverfolgung

Es gibt drei wichtige Verbesserungen für die Ablaufverfolgung in ASP.NET 2.0.

1. Integrierte Ablaufverfolgungsfunktionalität
2. Programmgesteuerter Zugriff auf Ablaufverfolgungsnachrichten
3. Verbesserte Ablaufverfolgung auf Anwendungsebene

## <a name="integrated-tracing-functionality"></a>Integrierte Ablaufverfolgungsfunktionalität

Sie können jetzt Nachrichten, die von der System.Diagnostics.Trace-Klasse ausgegeben werden, an ASP.NET Ablaufverfolgungsausgabe weiterleiten und Nachrichten weiterleiten, die von ASP.NET Ablaufverfolgung an System.Diagnostics.Trace ausgegeben werden. Sie können ASP.NET Instrumentationsereignisse auch an System.Diagnostics.Trace weiterleiten. Diese Funktionalität wird durch das neue **writeToDiagnosticsTrace-Attribut** des &lt;Trace-Elements&gt; bereitgestellt. Wenn dieser boolesche Wert wahr ist, werden ASP.NET Trace-Meldungen an die System.Diagnostics-Ablaufverfolgungsinfrastruktur weitergeleitet, um sie von allen Listenern zu verwenden, die zum Anzeigen von Trace-Meldungen registriert sind.

## <a name="programmatic-access-to-trace-messages"></a>Programmgesteuerter Zugriff auf Trace-Nachrichten

ASP.NET 2.0 ermöglicht den programmgesteuerten Zugriff auf alle Ablaufverfolgungsnachrichten über die **TraceContextRecord-Klasse** und die **TraceRecords-Auflistung.** Die effizienteste Methode zum Zugriff auf Ablaufverfolgungsnachrichten besteht darin, einen **TraceContextEventHandler-Delegaten** (ebenfalls neu in ASP.NET 2.0) zu registrieren, um das neue **TraceFinished-Ereignis** zu verarbeiten. Sie können dann die Ablaufverfolgungsnachrichten nach Belieben durchlaufen.

Das folgende Codebeispiel veranschaulicht dies:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

Im obigen Beispiel durchlaufe ich die TraceRecords-Auflistung und schreibe dann jede Nachricht in den Antwortstream.

## <a name="improved-application-level-tracing"></a>Verbesserte Ablaufverfolgung auf Anwendungsebene

Die Ablaufverfolgung auf Anwendungsebene wird durch die Einführung &lt;des&gt; neuen **MostRecent-Attributs** des Trace-Elements verbessert. Dieses Attribut gibt an, ob die neueste Ablaufverfolgungsausgabe auf Anwendungsebene angezeigt wird und ältere Ablaufverfolgungsdaten über die durch requestLimit angegebenen Grenzwerte hinaus verworfen werden. Bei false werden Ablaufverfolgungsdaten für Anforderungen angezeigt, bis das requestLimit-Attribut erreicht ist.

## <a name="aspnet-command-line-tools"></a>ASP.NET Befehlszeilentools

Es gibt mehrere Befehlszeilentools, die bei der Konfiguration von ASP.NET helfen. ASP.NET Entwickler sollten mit dem\_Tool aspnet regiis.exe vertraut sein. ASP.NET 2.0 bietet drei weitere Befehlszeilentools, die bei der Konfiguration unterstützt werden können.

Die folgenden Befehlszeilentools sind verfügbar:

| **Tool** | **Verwenden Sie** |
| --- | --- |
| **aspnet\_regiis.exe** | Ermöglicht die Registrierung von ASP.NET bei IIS. Es gibt zwei Versionen dieser Tools, die mit ASP.NET 2.0 ausgeliefert werden, eine für 32-Bit-Systeme (im Framework-Ordner) und eine für 64-Bit-Systeme (im Ordner Framework64). Die 64-Bit-Version wird nicht auf einem 32-Bit-Betriebssystem installiert. |
| **aspnet\_regsql.exe** | Das ASP.NET SQL Server-Registrierungstool wird verwendet, um eine Microsoft SQL Server-Datenbank für die Verwendung durch die SQL Server-Anbieter in ASP.NET zu erstellen oder Optionen aus einer vorhandenen Datenbank hinzuzufügen oder zu entfernen. Die Datei\_Aspnet regsql.exe befindet sich im Ordner [drive:]-windows-microsoft.NET-Framework-versionNumber auf ihrem Webserver. |
| **aspnet\_regbrowsers.exe** | Das ASP.NET Browserregistrierungstool analysiert und kompiliert alle systemweiten Browserdefinitionen in eine Assembly und installiert die Assembly im globalen Assemblycache. Das Tool verwendet die Browser-Definitionsdateien (. BROWSER-Dateien) aus dem Unterverzeichnis .NET Framework Browsers. Das Tool befindet sich im Verzeichnis %SystemRoot%-Microsoft.NET-Framework-Version. |
| **aspnet\_compiler.exe** | Mit dem Tool ASP.NET Kompilierung können Sie eine ASP.NET Webanwendung kompilieren, entweder an Ort und Stelle oder für die Bereitstellung an einem Zielspeicherort, z. B. einem Produktionsserver. Die an Ort und Stelle kompilierte Anwendung unterstützt die Anwendungsleistung, da Endbenutzer bei der ersten Anforderung an die Anwendung während der Kompilierung der Anwendung keine Verzögerung feststellen. |

Da das Tool\_aspnet regiis.exe nicht neu in ASP.NET 2.0 ist, werden wir es hier nicht diskutieren.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server-Registrierungstool\_- aspnet regsql.exe

Sie können verschiedene Optionentypen mit dem ASP.NET SQL Server-Registrierungstool festlegen. Sie können eine SQL-Verbindung angeben, angeben, welche ASP.NET Anwendungsdienste SQL Server zum Verwalten von Informationen verwenden, angeben, welche Datenbank oder Tabelle für die SQL-Cacheabhängigkeit verwendet wird, und Unterstützung für die Verwendung von SQL Server zum Speichern von Prozeduren und Sitzungsstatus hinzufügen oder entfernen.

Mehrere ASP.NET Anwendungsdienste sind auf einen Anbieter angewiesen, um das Speichern und Abrufen von Daten aus einer Datenquelle zu verwalten. Jeder Anbieter ist spezifisch für die Datenquelle. ASP.NET enthält einen SQL Server-Anbieter für die folgenden ASP.NET Features:

- Mitgliedschaft (die [SqlMembershipProvider-Klasse).](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)
- Rollenverwaltung (die [SqlRoleProvider-Klasse).](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)
- Profil (die [SqlProfileProvider-Klasse).](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)
- Webparts Personalisierung (die [SqlPersonalizationProvider-Klasse).](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)
- Webereignisse (die [SqlWebEventProvider-Klasse).](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)

Wenn Sie ASP.NET installieren, enthält die Machine.config-Datei für Ihren Server Konfigurationselemente, die SQL Server-Anbieter für jedes der ASP.NET-Features angeben, die auf einem Anbieter basieren. Diese Anbieter sind standardmäßig so konfiguriert, dass eine Verbindung mit einer lokalen Benutzerinstanz von SQL Server Express 2005 hergestellt wird. Wenn Sie die von den Anbietern verwendete Standardverbindungszeichenfolge ändern, müssen Sie die SQL Server-Datenbank und die Datenbankelemente für die ausgewählte Funktion mit\_Aspnet regsql.exe installieren, bevor Sie eines der in der Computerkonfiguration konfigurierten ASP.NET Features verwenden können. Wenn die Datenbank, die Sie mit dem SQL-Registrierungstool angeben, noch nicht vorhanden ist (aspnetdb ist die Standarddatenbank, wenn keine Datenbank in der Befehlszeile angegeben ist), muss der aktuelle Benutzer über die Berechtigung zum Erstellen von Datenbanken in SQL Server sowie zum Erstellen von Schemaelementen in einer Datenbank verfügen.

### <a name="sql-cache-dependency"></a>SQL-Cacheabhängigkeit

Ein erweitertes Feature ASP.NET Ausgabezwischenspeicherung ist die SQL-Cacheabhängigkeit. Die SQL-Cacheabhängigkeit unterstützt zwei verschiedene Betriebsarten: einen, der eine ASP.NET Implementierung der Tabellenabfrage verwendet, und einen zweiten Modus, der die Abfragebenachrichtigungsfeatures von SQL Server 2005 verwendet. Das SQL-Registrierungstool kann verwendet werden, um den Tabellenabrufmodus zu konfigurieren.

### <a name="session-state"></a>Sitzungszustand

Standardmäßig werden Sitzungsstatuswerte und -informationen im ASP.NET Prozess im Arbeitsspeicher gespeichert. Alternativ können Sie Sitzungsdaten in einer SQL Server-Datenbank speichern, wo sie von mehreren Webservern gemeinsam genutzt werden können. Wenn die Datenbank, die Sie für den Sitzungsstatus mit dem SQL-Registrierungstool angeben, noch nicht vorhanden ist, muss der aktuelle Benutzer über die Berechtigung zum Erstellen von Datenbanken in SQL Server sowie zum Erstellen von Schemaelementen in einer Datenbank verfügen. Wenn die Datenbank vorhanden ist, muss der aktuelle Benutzer über die Berechtigung zum Erstellen von Schemaelementen in der vorhandenen Datenbank verfügen.

Um die Sitzungsstatusdatenbank auf SQL Server\_zu installieren, führen Sie das Tool Aspnet regsql.exe aus, und geben Sie die folgenden Informationen mit dem Befehl an:

- Der Name der SQL Server-Instanz mit der Option **-S.**
- Die Anmeldeinformationen für ein Konto, das über die Berechtigung zum Erstellen einer Datenbank auf einem Computer mit SQL Server verfügt. Verwenden Sie die Option **-E,** um den aktuell angemeldeten Benutzer zu verwenden, oder verwenden Sie die Option **-U,** um eine Benutzer-ID zusammen mit der Option **-P** anzugeben, um ein Kennwort anzugeben.
- Die Befehlszeilenoption **-ssadd,** um die Sitzungsstatusdatenbank hinzuzufügen.

Standardmäßig können Sie das Tool\_Aspnet regsql.exe nicht verwenden, um die Sitzungsstatusdatenbank auf einem Computer mit SQL Server 2005 Express Edition zu installieren.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>Das ASP.NET Browser-Registrierungstool\_- aspnet regbrowsers.exe

In ASP.NET Version 1.1 enthielt die Datei Machine.config einen Abschnitt namens &lt;browserCaps&gt;. Dieser Abschnitt enthielt eine Reihe von XML-Einträgen, die die Konfigurationen für verschiedene Browser basierend auf einem regulären Ausdruck definierten. Für ASP.NET Version 2.0 wird eine neue . BROWSER-Datei definiert die Parameter eines bestimmten Browsers mit XML-Einträgen. Sie fügen Informationen in einem neuen Browser hinzu, indem Sie eine neue hinzufügen. BROWSER-Datei in den Ordner, der sich auf Ihrem System befindet.

Da eine Anwendung nicht jedes Mal eine .config-Datei liest, wenn Browserinformationen erforderlich sind, können Sie eine neue erstellen. BROWSER-Datei und führen\_Sie Aspnet regbrowsers.exe aus, um die erforderlichen Änderungen zur Assembly hinzuzufügen. Dadurch kann der Server sofort auf die neuen Browserinformationen zugreifen, sodass Sie keine Ihrer Anwendungen herunterfahren müssen, um die Informationen aufzunehmen. Eine Anwendung kann über die Browser-Eigenschaft der aktuellen HttpRequest auf Browserfunktionen zugreifen.

Die folgenden Optionen sind verfügbar,\_wenn aspnet regbrowser.exe ausgeführt wird:

| **Option** | **Beschreibung** |
| --- | --- |
| **-?** | Zeigt den Hilfetext Aspnet\_regbbrowsers.exe im Befehlsfenster an. |
| **-i** | Erstellt die Assembly der Laufzeitbrowserfunktionen und installiert sie im globalen Assemblycache. |
| **-u** | Deinstalliert die Assembly der Laufzeitbrowserfunktionen aus dem globalen Assemblycache. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>Das ASP.NET Compilation Tool\_- aspnet compiler.exe

Das ASP.NET Kompilierungstool kann auf zwei allgemeine Arten verwendet werden: für die ortsspezifische Kompilierung und Kompilierung für die Bereitstellung, bei der ein Zielausgabeverzeichnis angegeben ist.

### <a name="compiling-an-application-in-place"></a>[Kompilieren einer Anwendung an Ort und Stelle](https://msdn.microsoft.com/library/ms229863.aspx)

Das ASP.NET Kompilierungstool kann eine Anwendung an Ort und Stelle kompilieren, d. h., es imitiert das Verhalten, mehrere Anforderungen an die Anwendung zu stellen, wodurch eine regelmäßige Kompilierung verursacht wird. Benutzer einer vorkompilierten Website erleben keine Verzögerung, die durch das Kompilieren der Seite bei der ersten Anforderung verursacht wird.

Wenn Sie eine Website vorab kompilieren, gelten die folgenden Elemente:

- Die Site behält ihre Dateien und Verzeichnisstruktur bei.
- Sie müssen über Compiler für alle Programmiersprachen verfügen, die von der Site auf dem Server verwendet werden.
- Wenn die Kompilierung einer Datei fehlschlägt, schlägt die Kompilierung der gesamten Site fehl.

Sie können eine Anwendung auch neu kompilieren, nachdem Sie ihr neue Quelldateien hinzugefügt haben. Das Tool kompiliert nur die neuen oder geänderten Dateien, es sei denn, Sie fügen die Option **-c** ein.

> [!NOTE]
> Die Kompilierung einer Anwendung, die eine geschachtelte Anwendung enthält, kompiliert die geschachtelte Anwendung nicht. Die geschachtelte Anwendung muss separat kompiliert werden.

### <a name="compiling-an-application-for-deployment"></a>[Kompilieren einer Anwendung für die Bereitstellung](https://msdn.microsoft.com/library/ms229863.aspx)

Sie kompilieren eine Anwendung für die Bereitstellung (Kompilierung an einen Zielspeicherort), indem Sie den parameter targetDir angeben. Der targetDir kann der endgültige Speicherort für die Webanwendung sein, oder die kompilierte Anwendung kann weiter bereitgestellt werden. Mit der Option **-u** kompiliert die Anwendung so, dass Sie Änderungen an bestimmten Dateien in der kompilierten Anwendung vornehmen können, ohne sie neu zu kompilieren. Aspnet\_compiler.exe unterscheidet zwischen statischen und dynamischen Dateitypen und behandelt sie beim Erstellen der resultierenden Anwendung unterschiedlich.

- Statische Dateitypen sind solche, denen kein Compiler oder Buildanbieter zugeordnet ist, z. B. Dateien, deren Benannte Erweiterungen wie .css, .gif, .htm, .html, .jpg, .js usw. haben. Diese Dateien werden einfach an den Zielspeicherort kopiert, wobei ihre relativen Stellen in der Verzeichnisstruktur beibehalten werden.
- Dynamische Dateitypen sind solche, denen ein Compiler oder Buildanbieter zugeordnet ist, einschließlich Dateien mit ASP.NET-spezifischen Dateinamenerweiterungen wie .asax, .ascx, .ashx, .aspx, .browser, .master usw. Das Tool ASP.NET Kompilierung generiert Assemblys aus diesen Dateien. Wenn die Option **-u** weggelassen wird, erstellt das Tool auch Dateien mit der Dateinamenerweiterung . COMPILED, die die ursprünglichen Quelldateien ihrer Assembly zuordnen. Um sicherzustellen, dass die Verzeichnisstruktur der Anwendungsquelle erhalten bleibt, generiert das Tool Platzhalterdateien an den entsprechenden Speicherorten in der Zielanwendung.

Sie müssen die Option **-u** verwenden, um anzugeben, dass der Inhalt der kompilierten Anwendung geändert werden kann. Andernfalls werden nachfolgende Änderungen ignoriert oder verursachen Laufzeitfehler.

In der folgenden Tabelle wird beschrieben, wie das Tool ASP.NET Kompilierung verschiedene Dateitypen verarbeitet, wenn die Option **-u** enthalten ist.

| **Dateityp** | **Compileraktion** |
| --- | --- |
| .ascx, .aspx, .master | Diese Dateien werden in Markup und Quellcode aufgeteilt, der sowohl CodeBehind-Dateien &lt;als auch code-behind-Dateien enthält, die in Skriptrunat="Server"-Elementen&gt; eingeschlossen sind. Quellcode wird in Assemblys mit Namen kompiliert, die von einem Hashalgorithmus abgeleitet werden, und die Assemblys werden im Bin-Verzeichnis abgelegt. Jeder Inlinecode, d. h. ** &lt; ** Code, der zwischen den und ** % ** Klammern eingeschlossen ist, ist in Markup enthalten und wird nicht kompiliert. Neue Dateien mit demselben Namen wie die Quelldateien werden erstellt, um das Markup zu enthalten, und in den entsprechenden Ausgabeverzeichnissen abgelegt. |
| .ashx, .asmx | Diese Dateien werden nicht kompiliert und in die Ausgabeverzeichnisse verschoben, wie es ist und nicht kompiliert wird. Wenn Sie den Handlercode kompilieren möchten, platzieren Sie den\_Code in Quellcodedateien im Verzeichnis App Code. |
| .cs, .vb, .jsl, .cpp (ohne CodeBehind-Dateien für die zuvor aufgeführten Dateitypen) | Diese Dateien werden kompiliert und als Ressource in Assemblys eingeschlossen, die auf sie verweisen. Quelldateien werden nicht in das Ausgabeverzeichnis kopiert. Wenn nicht auf eine Codedatei verwiesen wird, wird sie nicht kompiliert. |
| Benutzerdefinierte Dateitypen | Diese Dateien werden nicht kompiliert. Diese Dateien werden in die entsprechenden Ausgabeverzeichnisse kopiert. |
| Quellcodedateien im Unterverzeichnis App\_Code | Diese Dateien werden in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. |
| .resx- und .resource-Dateien im Unterverzeichnis App\_GlobalResources | Diese Dateien werden in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. Es\_wird kein App GlobalResources-Unterverzeichnis unter dem Hauptausgabeverzeichnis erstellt, und keine .resx- oder .resources-Dateien im Quellverzeichnis werden in die Ausgabeverzeichnisse kopiert. |
| .resx- und .resource-Dateien im Unterverzeichnis App\_LocalResources | Diese Dateien werden nicht kompiliert und in die entsprechenden Ausgabeverzeichnisse kopiert. |
| .skin-Dateien im\_Unterverzeichnis App Themes | Die .skin-Dateien und statischen Designdateien werden nicht kompiliert und in die entsprechenden Ausgabeverzeichnisse kopiert. |
| .browser Web.config Statische Dateitypen Assemblys, die bereits im Bin-Verzeichnis vorhanden sind | Diese Dateien werden wie in die Ausgabeverzeichnisse kopiert. |

In der folgenden Tabelle wird beschrieben, wie das ASP.NET Kompilierungstool verschiedene Dateitypen verarbeitet, wenn die Option **-u** weggelassen wird.

| **Dateityp** | **Compileraktion** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Diese Dateien werden in Markup und Quellcode aufgeteilt, der sowohl CodeBehind-Dateien &lt;als auch code-behind-Dateien enthält, die in Skriptrunat="Server"-Elementen&gt; eingeschlossen sind. Quellcode wird in Assemblys mit Namen kompiliert, die von einem Hashalgorithmus abgeleitet werden. Die resultierenden Assemblys werden im Bin-Verzeichnis abgelegt. Jeder Inlinecode, d. h. ** &lt; ** Code, der zwischen den und ** % ** Klammern eingeschlossen ist, ist in Markup enthalten und wird nicht kompiliert. Der Compiler erstellt neue Dateien, die das Markup mit demselben Namen wie die Quelldateien enthalten. Diese resultierenden Dateien werden im Bin-Verzeichnis abgelegt. Der Compiler erstellt auch Dateien mit demselben Namen wie die Quelldateien, jedoch mit der Erweiterung . COMPILED, die Zuordnungsinformationen enthalten. das. COMPILED-Dateien werden in den Ausgabeverzeichnissen platziert, die dem ursprünglichen Speicherort der Quelldateien entsprechen. |
| .ascx | Diese Dateien werden in Markup und Quellcode aufgeteilt. Quellcode wird in Assemblys kompiliert und im Bin-Verzeichnis mit Namen platziert, die von einem Hashalgorithmus abgeleitet werden. Es werden keine Markupdateien generiert. |
| .cs, .vb, .jsl, .cpp (ohne CodeBehind-Dateien für die zuvor aufgeführten Dateitypen) | Quellcode, auf den von den Assemblys verwiesen wird, die aus .ascx-, .ashx- oder ASPX-Dateien generiert werden, wird in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. Es werden keine Quelldateien kopiert. |
| Benutzerdefinierte Dateitypen | Diese Dateien werden wie dynamische Dateien kompiliert. Je nach Dateityp können sie basierend sind, kann der Compiler Zuordnungsdateien in den Ausgabeverzeichnissen platzieren. |
| Dateien im\_Unterverzeichnis App Code | Quellcodedateien in diesem Unterverzeichnis werden in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. |
| Dateien im\_App GlobalResources-Unterverzeichnis | Diese Dateien werden in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. Unterverzeichnis\_Von App GlobalResources wird kein Unterverzeichnis unter dem Hauptausgabeverzeichnis erstellt. Wenn die Konfigurationsdatei appliesTo="All" angibt, werden .resx- und .resources-Dateien in die Ausgabeverzeichnisse kopiert. Sie werden nicht kopiert, wenn sie von einem [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)referenziert werden. |
| .resx- und .resource-Dateien im Unterverzeichnis App\_LocalResources | Diese Dateien werden in Assemblys mit eindeutigen Namen kompiliert und im Bin-Verzeichnis abgelegt. Es werden keine .resx- oder .resource-Dateien in die Ausgabeverzeichnisse kopiert. |
| .skin-Dateien im\_Unterverzeichnis App Themes | Designs werden in Assemblys kompiliert und im Bin-Verzeichnis abgelegt. Stub-Dateien werden für .skin-Dateien erstellt und im entsprechenden Ausgabeverzeichnis abgelegt. Statische Dateien (z. B. .css) werden in die Ausgabeverzeichnisse kopiert. |
| .browser Web.config Statische Dateitypen Assemblys, die bereits im Bin-Verzeichnis vorhanden sind | Diese Dateien werden wie in das Ausgabeverzeichnis kopiert. |

### <a name="fixed-assembly-names"></a>[Feste Assemblynamen](https://msdn.microsoft.com/library/ms229863.aspx##)

Einige Szenarien, z. B. das Bereitstellen einer Webanwendung mit dem MSI Windows Installer, erfordern die Verwendung konsistenter Dateinamen und -inhalte sowie konsistente Verzeichnisstrukturen zum Identifizieren von Assemblys oder Konfigurationseinstellungen für Updates. In diesen Fällen können Sie die Option **-fixednames** verwenden, um anzugeben, dass das ASP.NET Kompilierungstool eine Assembly für jede Quelldatei kompilieren soll, anstatt die Assembly zu verwenden, in der mehrere Seiten in Assemblys kompiliert werden. Dies kann zu einer großen Anzahl von Assemblys führen.

### <a name="strong-name-compilation"></a>[Zusammenstellung mit starkem Namen](https://msdn.microsoft.com/library/ms229863.aspx##)

Die Optionen **-aptca**, **-delaysign**, **-keycontainer** und **-keyfile** werden\_bereitgestellt, sodass Sie Aspnet compiler.exe verwenden können, um Assemblys mit starkem Namen zu erstellen, ohne das [Strong Name Tool (Sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) separat zu verwenden. Diese Optionen entsprechen **AllowPartiallyTrustedCallersAttribute**, **AssemblyDelaySignAttribute**, **AssemblyKeyNameAttribute**und **AssemblyKeyFileAttribute**.

Die Erörterung dieser Attribute liegt außerhalb des Rahmens dieses Kurses.

## <a name="labs"></a>Labs

Jede der folgenden Übungseinheiten baut auf den vorherigen Übungseinheiten auf. Sie müssen sie in der Reihenfolge tun.

## <a name="lab-1-using-the-configuration-api"></a>Lab 1: Verwenden der Konfigurations-API

1. Erstellen Sie eine neue Website mit dem Namen *mod9lab*.
2. Fügen Sie der Website eine neue Webkonfigurationsdatei hinzu.
3. Fügen Sie der Datei web.config Folgendes hinzu:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Dadurch wird sichergestellt, dass Sie über die Berechtigung zum Speichern von Änderungen an der Datei web.config verfügen.

1. Fügen Sie ein neues Label-Steuerelement zu Default.aspx hinzu, und ändern Sie die ID in **lblDebugStatus**.
2. Fügen Sie ein neues Schaltflächensteuerelement zu Default.aspx hinzu.
3. Ändern Sie die ID des Button-Steuerelements in **btnToggleDebug** und den Text zum Umschalten des **Debugstatus**.
4. Öffnen Sie die Codeansicht für die CodeBehind-Datei von Default.aspx, und fügen Sie eine **using-Anweisung** für **System.Web.Configuration** wie folgt hinzu:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Fügen Sie der Klasse zwei\_private Variablen und eine Page Init-Methode hinzu, wie unten gezeigt:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Fügen Sie den\_folgenden Code zu Page Load hinzu:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Speichern und durchsuchen Sie default.aspx. Beachten Sie, dass das Label-Steuerelement den aktuellen Debugstatus anzeigt.
2. Doppelklicken Sie auf das Schaltflächensteuerelement im Designer, und fügen Sie dem Click-Ereignis für das Schaltflächensteuerelement den folgenden Code hinzu:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Speichern und durchsuchen Sie default.aspx, und klicken Sie auf die Schaltfläche.
2. Öffnen Sie die Datei web.config nach jedem Schaltflächenklick, und beobachten Sie das **Debugattribut** im &lt;Kompilierungsabschnitt.&gt;

## <a name="lab-2-logging-application-restarts"></a>Lab 2: Programmieren von Anwendungsneustarts

In dieser Übungseinheit erstellen Sie Code, mit dem Sie die Protokollierung von Anwendungsabschaltungen, -Starts und Neukompilierungen in der Ereignisanzeige umschalten können.

1. Fügen Sie default.aspx eine DropDownList hinzu, und ändern Sie die ID in ddlLogAppEvents.
2. Legen Sie die **AutoPostBack-Eigenschaft** für die DropDownList auf **true**fest.
3. Fügen Sie der Items-Auflistung für die DropDownList drei Elemente hinzu. Machen Sie den **Text** für das erste Element *Wert auswählen* und den Wert -1. Machen **Sie text** und **value** des zweiten Elements **True** und **text** and **value** of the third item **False**.
4. Fügen Sie default.aspx eine neue Bezeichnung hinzu. Ändern Sie die ID in **lblLogAppEvents**.
5. Öffnen Sie die CodeBehind-Ansicht für default.aspx, und fügen Sie eine neue Deklaration für eine Variable vom Typ HealthMonitoringSection hinzu, wie unten gezeigt:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Fügen Sie dem vorhandenen Code\_in Page Init den folgenden Code hinzu:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. Doppelklicken Sie auf die DropDownList, und fügen Sie dem SelectedIndexChanged-Ereignis den folgenden Code hinzu:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Durchsuchen Sie default.aspx.
2. Legen Sie die Dropdown-Liste auf **False**fest.
3. Löschen Sie das Anwendungsprotokoll in der Ereignisanzeige.
4. Klicken Sie auf die Schaltfläche, um das Debug-Attribut für die Anwendung zu ändern.
5. Aktualisieren Sie das Anwendungsprotokoll in der Ereignisanzeige. 

    1. Wurden Ereignisse protokolliert?
    2. Warum oder warum nicht?
6. Legen Sie die Dropdown-Liste auf **True fest.**
7. Klicken Sie auf die Schaltfläche, um das Debug-Attribut für die Anwendung umzuschalten.
8. Aktualisieren Sie die Anwendungsanmeldung in der Ereignisanzeige. 

    1. Wurden Ereignisse protokolliert?
    2. Was war der Grund für das Herunterfahren der App?
9. Experimentieren Sie mit dem Ein- und Ausschalten der Protokollierung, und sehen Sie sich die Änderungen an der Datei web.config an.

## <a name="more-information"></a>Weitere Informationen:

ASP.NET 2.0-Anbietermodell ermöglicht es Ihnen, Ihre eigenen Anbieter nicht nur für Anwendungsinstrumente zu erstellen, sondern auch für viele andere Anwendungen wie Mitgliedschaft, Profile usw. Ausführliche Informationen zum Schreiben eines benutzerdefinierten Anbieters zum Protokollieren von Anwendungsereignissen in einer Textdatei finden Sie [unter diesem Link](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp).
