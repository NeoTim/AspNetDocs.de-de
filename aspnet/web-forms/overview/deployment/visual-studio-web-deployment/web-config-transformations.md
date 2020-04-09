---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'ASP.NET Webbereitstellung mit Visual Studio: Web.config-Dateitransformationen | Microsoft Docs'
author: tdykstra
description: In dieser Lernprogrammreihe erfahren Sie, wie Sie eine ASP.NET Webanwendung in Azure App Service Web Apps oder bei einem Hostinganbieter eines Drittanbieters bereitstellen (veröffentlichen) können.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675748"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>ASP.NET Webbereitstellung mit Visual Studio: Web.config-Dateitransformationen

von [Tom Dykstra](https://github.com/tdykstra)

[Starter Project herunterladen](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> In dieser Lernprogrammreihe erfahren Sie, wie Sie eine ASP.NET Webanwendung mithilfe von Visual Studio 2012 oder Visual Studio 2010 in Azure App Service-Web-Apps oder bei einem Drittanbieter bereitstellen (veröffentlichen). Weitere Informationen zur Serie finden Sie [im ersten Tutorial der Serie](introduction.md).

## <a name="overview"></a>Übersicht

In diesem Tutorial erfahren Sie, wie Sie den Vorgang des Änderns der *Datei Web.config* automatisieren, wenn Sie sie in verschiedenen Zielumgebungen bereitstellen. Die meisten Anwendungen verfügen über Einstellungen in der *Datei Web.config,* die bei der Bereitstellung der Anwendung unterschiedlich sein müssen. Durch die Automatisierung des Vorgangs der Vornehmen dieser Änderungen müssen Sie diese bei jeder Bereitstellung manuell erledigen, was mühsam und fehleranfällig wäre.

Erinnerung: Wenn Sie eine Fehlermeldung erhalten oder etwas nicht funktioniert, während Sie das Tutorial durchlaufen, überprüfen Sie die [Problembehandlungsseite](troubleshooting.md).

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config-Transformationen im Vergleich zu Web Deploy-Parametern

Es gibt zwei Möglichkeiten, den Vorgang der Änderung der *Web.config-Dateieinstellungen* zu automatisieren: [Web.config-Transformationen](https://msdn.microsoft.com/library/dd465326.aspx) und [Web Deploy-Parameter](https://msdn.microsoft.com/library/ff398068.aspx). Eine *Web.config-Transformationsdatei* enthält XML-Markup, das angibt, wie die *Datei Web.config* bei der Bereitstellung geändert wird. Sie können verschiedene Änderungen für bestimmte Buildkonfigurationen und für bestimmte Veröffentlichungsprofile angeben. Die Standardbuildkonfigurationen sind Debug und Release, und Sie können benutzerdefinierte Buildkonfigurationen erstellen. Ein Veröffentlichungsprofil entspricht in der Regel einer Zielumgebung. (Weitere Informationen zum Veröffentlichen von Profilen finden Sie im Tutorial [Bereitstellen in IIS als Testumgebung.)](deploying-to-iis.md)

Web Deploy-Parameter können verwendet werden, um viele verschiedene Arten von Einstellungen anzugeben, die während der Bereitstellung konfiguriert werden müssen, einschließlich Einstellungen, die in *Web.config-Dateien* enthalten sind. Wenn Sie *web.config-Dateiänderungen* angeben, sind Web Deploy-Parameter komplexer einzurichten, aber sie sind nützlich, wenn Sie den wert, der festgelegt werden soll, erst nach der Bereitstellung kennen. In einer Unternehmensumgebung können Sie z. B. ein *Bereitstellungspaket* erstellen und es einer Person in der IT-Abteilung zur Installation in der Produktion geben, und diese Person muss in der Lage sein, Verbindungszeichenfolgen oder Kennwörter einzugeben, die Sie nicht kennen.

Für das Szenario, das in dieser Lernprogrammreihe behandelt wird, wissen Sie im Voraus alles, was für die *Datei Web.config* getan werden muss, sodass Sie keine Web Deploy-Parameter verwenden müssen. Sie konfigurieren einige Transformationen, die je nach verwendeter Buildkonfiguration unterschiedlich sind, und einige, die je nach verwendetm Veröffentlichungsprofil unterschiedlich sind.

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Angeben von Web.config-Einstellungen in Azure

Wenn sich die *Web.config-Dateieinstellungen,* die `<connectionStrings>` Sie `<appSettings>` ändern möchten, im oder im Element befinden und Sie in Azure App Service für Web-Apps bereitstellen, haben Sie eine weitere Option zum Automatisieren von Änderungen während der Bereitstellung. Sie können die Einstellungen, die Sie in Azure wirksam werden möchten, auf der Registerkarte **Konfigurieren** der Seite Verwaltungsportal für Ihre Web-App eingeben (Scrollen Sie nach unten zu den **Abschnitten App-Einstellungen** und **Verbindungszeichenfolgen).** Wenn Sie das Projekt bereitstellen, wendet Azure die Änderungen automatisch an. Weitere Informationen finden Sie unter [Windows Azure-Websites: Funktionsweise von Anwendungszeichenfolgen und Verbindungszeichenfolgen](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

## <a name="default-transformation-files"></a>Standardtransformationsdateien

Erweitern Sie in **Solution Explorer** *Web.config,* um die Transformationsdateien *Web.Debug.config* und *Web.Release.config anzuzeigen,* die standardmäßig für die beiden Standardbuildkonfigurationen erstellt werden.

![Web.config_transform_files](web-config-transformations/_static/image1.png)

Sie können Transformationsdateien für benutzerdefinierte Buildkonfigurationen erstellen, indem Sie mit der rechten Maustaste auf die Datei Web.config klicken und im Kontextmenü **Config-Transformationen hinzufügen** auswählen. Für dieses Tutorial müssen Sie dies nicht tun, und die Menüoption ist deaktiviert, da Sie keine benutzerdefinierten Buildkonfigurationen erstellt haben.

Später erstellen Sie drei weitere Transformationsdateien, jeweils eine für die Test-, Staging- und Produktionsveröffentlichungsprofile. Ein typisches Beispiel für eine Einstellung, die Sie in einer Veröffentlichungsprofiltransformationsdatei behandeln würden, da sie von der Zielumgebung abhängt, ist ein WCF-Endpunkt, der sich für Test und Produktion unterscheidet. Sie erstellen Veröffentlichungsprofiltransformationsdateien in späteren Lernprogrammen, nachdem Sie die Veröffentlichungsprofile erstellt haben, mit denen sie beginnen.

## <a name="disable-debug-mode"></a>Deaktivieren des Debugmodus

Ein Beispiel für eine Einstellung, die von der `debug` Buildkonfiguration und nicht von der Zielumgebung abhängt, ist das Attribut. Bei einem Releasebuild sollten sie das Debuggen in der Regel deaktiviert haben, unabhängig davon, in welcher Umgebung Sie bereitstellen. Daher erstellen die Visual Studio-Projektvorlagen standardmäßig *Web.Release.config-Transformationsdateien* mit Code, der das `debug` Attribut aus dem `compilation` Element entfernt. Hier ist die Standard-Web.Release.config : zusätzlich zu einigen Beispieltransformationscode, `compilation` der auskommentiert `debug` wird, enthält es Code in das Element, das das Attribut entfernt: *Web.Release.config*

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

Das `xdt:Transform="RemoveAttributes(debug)"` Attribut gibt an, `debug` dass das Attribut `system.web/compilation` aus dem Element in der bereitgestellten *Datei Web.config* entfernt werden soll. Dies geschieht jedes Mal, wenn Sie einen Release-Build bereitstellen.

## <a name="limit-error-log-access-to-administrators"></a>Beschränken des Fehlerprotokollzugriffs für Administratoren

Wenn während der Anwendung ein Fehler auftritt, zeigt die Anwendung anstelle der vom System generierten Fehlerseite eine generische Fehlerseite an, und sie verwendet das [Paket Elmah NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) für die Fehlerprotokollierung und -berichterstattung. Das `customErrors` Element in der Anwendungsdatei *Web.config* gibt die Fehlerseite an:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

Um die Fehlerseite anzuzeigen, `mode` ändern `customErrors` Sie vorübergehend das Attribut des Elements von "RemoteOnly" in "On", und führen Sie die Anwendung aus Visual Studio aus. Verursachen Sie einen Fehler, indem Sie eine ungültige URL anfordern, z. *B. Studentsxxx.aspx*. Anstelle einer IIS-generierten Fehlerseite "Die Ressource kann nicht gefunden werden" wird die Seite *GenericErrorPage.aspx* angezeigt.

![Fehlerseite](web-config-transformations/_static/image2.png)

Um das Fehlerprotokoll anzuzeigen, ersetzen Sie alles in der URL nach der `http://localhost:51130/elmah.axd`Portnummer durch *elmah.axd* (z. B.) und drücken Sie die Eingabetaste:

![ELMAH Seite](web-config-transformations/_static/image3.png)

Vergessen Sie nicht, `customErrors` das Element wieder auf "RemoteOnly"-Modus zu setzen, wenn Sie fertig sind.

Auf Ihrem Entwicklungscomputer ist es praktisch, freien Zugriff auf die Fehlerprotokollseite zu ermöglichen, aber in der Produktion wäre dies ein Sicherheitsrisiko. Für den Produktionsstandort möchten Sie eine Autorisierungsregel hinzufügen, die den Fehlerprotokollzugriff auf Administratoren einschränkt, und sicherstellen, dass die Einschränkung auch im Test und im Staging funktioniert. Daher ist dies eine weitere Änderung, die Sie jedes Mal implementieren möchten, wenn Sie einen Release-Build bereitstellen, und daher gehört er in die Datei *Web.Release.config.*

Öffnen Sie *Web.Release.config* `location` und fügen Sie `configuration` ein neues Element unmittelbar vor dem schließenden Tag hinzu, wie hier gezeigt.

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

Der `Transform` Attributwert "Insert" `location` bewirkt, dass dieses Element `location` als gleichgeordnetzu zu allen vorhandenen Elementen in der *Datei Web.config* hinzugefügt wird. (Es gibt `location` bereits ein Element, das Autorisierungsregeln für die Seite **Credits aktualisieren** angibt.)

Jetzt können Sie eine Vorschau der Transformation anzeigen, um sicherzustellen, dass Sie sie korrekt codiert haben.

Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf *Web.Release.config,* und klicken Sie auf **Transformation anzeigen**.

![Vorschau-Transformationsmenü](web-config-transformations/_static/image4.png)

Es wird eine Seite geöffnet, die Ihnen die Datei *"Development Web.config"* auf der linken Seite anzeigt und zeigt, wie die bereitgestellte *Datei Web.config* auf der rechten Seite aussehen wird, wobei die Änderungen hervorgehoben werden.

![Vorschau der Debugtransformation](web-config-transformations/_static/image5.png)

![Vorschau der Standorttransformation](web-config-transformations/_static/image6.png)

( In der Vorschau werden möglicherweise einige zusätzliche Änderungen angezeigt, für die Sie keine Transformationen geschrieben haben: Diese betreffen in der Regel das Entfernen von Leerraum, das sich nicht auf die Funktionalität auswirkt.)

Wenn Sie die Site nach der Bereitstellung testen, testen Sie auch, ob die Autorisierungsregel wirksam ist.

> [!NOTE] 
> 
> **Sicherheitshinweis** Zeigen Sie niemals Fehlerdetails für die Öffentlichkeit in einer Produktionsanwendung an, oder speichern Sie diese Informationen an einem öffentlichen Ort. Angreifer können Fehlerinformationen verwenden, um Sicherheitslücken in einer Website zu erkennen. Wenn Sie ELMAH in Ihrer eigenen Anwendung verwenden, konfigurieren Sie ELMAH, um Sicherheitsrisiken zu minimieren. Das ELMAH-Beispiel in diesem Tutorial sollte nicht als empfohlene Konfiguration betrachtet werden. Es ist ein Beispiel, das ausgewählt wurde, um zu veranschaulichen, wie ein Ordner behandelt wird, in dem die Anwendung Dateien erstellen kann. Weitere Informationen finden Sie [unter Sichern des ELMAH-Endpunkts](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>Eine Einstellung, die Sie in Veröffentlichungsprofiltransformationsdateien behandeln

Ein häufiges Szenario besteht darin, *Web.config-Dateieinstellungen* zu verwenden, die in jeder Umgebung, in der Sie bereitstellen, unterschiedlich sein müssen. Beispielsweise kann eine Anwendung, die einen WCF-Dienst aufruft, einen anderen Endpunkt in Test- und Produktionsumgebungen benötigen. Die Anwendung der Contoso University enthält auch eine solche Einstellung. Diese Einstellung steuert einen sichtbaren Indikator auf den Seiten einer Website, der Ihnen mitteilt, in welcher Umgebung Sie sich befinden, z. B. Entwicklung, Test oder Produktion. Der Einstellungswert bestimmt, ob die Anwendung "(Dev)" oder "(Test)" an die Hauptüberschrift auf der *Site.Master-Masterseite* anfügt:

![Umweltindikator](web-config-transformations/_static/image7.png)

Die Umgebungsanzeige wird weggelassen, wenn die Anwendung in Staging oder Produktion ausgeführt wird.

Die Contoso University-Webseiten lesen einen `appSettings` Wert, der in der *Datei Web.config* festgelegt ist, um zu bestimmen, in welcher Umgebung die Anwendung ausgeführt wird:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

Der Wert sollte "Test" in der Testumgebung und "Prod" für Staging und Produktion sein.

Der folgende Code in einer Transformationsdatei implementiert diese Transformation:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

Der `xdt:Transform` Attributwert "SetAttributes" gibt an, dass der Zweck dieser Transformation darin besteht, Attributwerte eines vorhandenen Elements in der *Datei Web.config* zu ändern. Der `xdt:Locator` Attributwert "Match(key)" gibt an, dass es `key` sich `key` bei dem zu ändernden Element um das Element handelt, dessen Attribut mit dem hier angegebenen Attribut übereinstimmt. Das einzige andere `add` Attribut `value`des Elements ist , und das wird in der bereitgestellten *Datei Web.config* geändert. Der hier gezeigte `value` Code `Environment` `appSettings` bewirkt, dass das Attribut des Elements in der bereitgestellten *Web.config-Datei* auf "Test" festgelegt wird.

Diese Transformation gehört zu den Veröffentlichungsprofiltransformationsdateien, die Sie noch nicht erstellt haben. Sie erstellen und aktualisieren die Transformationsdateien, die diese Änderung implementieren, wenn Sie die Veröffentlichungsprofile für die Test-, Staging- und Produktionsumgebungen erstellen. Sie tun dies in der [Bereitstellung für IIS](deploying-to-iis.md) und die Bereitstellung in Produktions-Tutorials. [deploy to production](deploying-to-production.md)

> [!NOTE]
> Da sich diese `<appSettings>` Einstellung im Element befindet, haben Sie eine weitere Alternative zum Angeben der Transformation, wenn Sie in Azure App Service in Azure App Service [bereitstellen.](#watransforms)

## <a name="setting-connection-strings"></a>Festlegen von Verbindungszeichenfolgen

Obwohl die Standardtransformationsdatei ein Beispiel enthält, das zeigt, wie eine Verbindungszeichenfolge aktualisiert wird, müssen Sie in den meisten Fällen keine Verbindungszeichenfolgentransformationen einrichten, da Sie Verbindungszeichenfolgen im Veröffentlichungsprofil angeben können. Sie tun dies in der [Bereitstellung für IIS](deploying-to-iis.md) und die Bereitstellung in Produktions-Tutorials. [deploy to production](deploying-to-production.md)

## <a name="summary"></a>Zusammenfassung

Sie haben jetzt so viel wie möglich mit *Web.config-Transformationen* getan, bevor Sie die Veröffentlichungsprofile erstellen, und Sie haben eine Vorschau der bereitgestellten Web.config-Datei gesehen.

![Vorschau der Standorttransformation](web-config-transformations/_static/image8.png)

Im folgenden Tutorial kümmern Sie sich um Bereitstellungseinrichtungsaufgaben, für die Projekteigenschaften festgelegt werden müssen.

## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zu Themen, die in diesem Tutorial behandelt werden, finden Sie unter [Verwenden von Web.config-Transformationen zum Ändern von Einstellungen in der Web.config-Zieldatei oder app.config-Datei während](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) der Bereitstellung in der Webbereitstellungsinhaltszuordnung für Visual Studio und ASP.NET.

> [!div class="step-by-step"]
> [Zurück](preparing-databases.md)
> [Weiter](project-properties.md)
