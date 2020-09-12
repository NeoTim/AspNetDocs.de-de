---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: Grundlegendes zu ASP.NET AJAX-Webdiensten | Microsoft-Dokumentation
author: scottcate
description: Webdienste sind ein integraler Bestandteil von .NET Framework, die eine plattformübergreifende Lösung zum Austauschen von Daten zwischen verteilten Systemen bereitstellen. Obwohl Web...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2020
ms.locfileid: "86162807"
---
# <a name="understanding-aspnet-ajax-web-services"></a>Grundlegendes zu Webdiensten von ASP.NET AJAX

von [Scott Cate](https://github.com/scottcate)

[PDF herunterladen](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Webdienste sind ein integraler Bestandteil von .NET Framework, die eine plattformübergreifende Lösung zum Austauschen von Daten zwischen verteilten Systemen bereitstellen. Obwohl Webdienste normalerweise verwendet werden, um unterschiedliche Betriebssysteme, Objekt Modelle und Programmiersprachen zu ermöglichen, Daten zu senden und zu empfangen, können Sie auch zum dynamischen Einfügen von Daten in eine ASP.NET AJAX-Seite oder zum Senden von Daten von einer Seite an ein Back-End-System verwendet werden. All dies ist möglich, ohne dass auf Post Back Vorgänge zurückgegriffen wird.

## <a name="calling-web-services-with-aspnet-ajax"></a>Aufrufen von Webdiensten mit ASP.NET AJAX

Dan Wahlin

Webdienste sind ein integraler Bestandteil von .NET Framework, die eine plattformübergreifende Lösung zum Austauschen von Daten zwischen verteilten Systemen bereitstellen. Obwohl Webdienste normalerweise verwendet werden, um unterschiedliche Betriebssysteme, Objekt Modelle und Programmiersprachen zu ermöglichen, Daten zu senden und zu empfangen, können Sie auch zum dynamischen Einfügen von Daten in eine ASP.NET AJAX-Seite oder zum Senden von Daten von einer Seite an ein Back-End-System verwendet werden. All dies ist möglich, ohne dass auf Post Back Vorgänge zurückgegriffen wird.

Obwohl das ASP.NET AJAX-Update Panel-Steuerelement eine einfache Möglichkeit zum Aktivieren einer beliebigen ASP.NET-Seite bietet, kann es vorkommen, dass Sie dynamisch auf Daten auf dem Server zugreifen müssen, ohne ein Update Panel zu verwenden. In diesem Artikel erfahren Sie, wie Sie dies erreichen, indem Sie Webdienste in ASP.NET-AJAX-Seiten erstellen und nutzen.

Dieser Artikel konzentriert sich auf die Funktionalität, die in den Core ASP.NET AJAX-Erweiterungen sowie in einem Webdienst-aktivierten Steuerelement im ASP.NET AJAX-Toolkit mit dem Namen AutoCompleteExtender verfügbar ist. Zu den behandelten Themen gehören das definieren AJAX-fähiger Webdienste, das Erstellen von Client Proxys und das Aufrufen von Webdiensten mit JavaScript Sie sehen auch, wie Webdienst Aufrufe direkt an ASP.net page-Methoden durchgeführt werden können.

## <a name="web-services-configuration"></a>Webdienst Konfiguration

Wenn ein neues Website Projekt mit Visual Studio 2008 erstellt wird, enthält die web.config Datei eine Reihe neuer Ergänzungen, die Benutzern früherer Versionen von Visual Studio möglicherweise nicht vertraut sind. Einige dieser Änderungen ordnen das "ASP"-Präfix den ASP.NET AJAX-Steuerelementen zu, sodass Sie in Seiten verwendet werden können, während andere erforderliche httpHandlers und httpModules definieren. In der Liste 1 werden Änderungen an dem- `<httpHandlers>` Element in web.config angezeigt, die sich auf Webdienst Aufrufe auswirken. Der zum Verarbeiten von ASMX-aufrufen verwendete HttpHandler-Standard Handler wird entfernt und durch eine ScriptHandlerFactory-Klasse ersetzt, die sich in der System.Web.Extensions.dll-Assembly befindet. System.Web.Extensions.dll enthält alle Kernfunktionen, die von ASP.NET AJAX verwendet werden.

**Codebeispiel 1. ASP.NET AJAX-webdiensthandlerkonfiguration**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

Diese HttpHandler-Ersetzung erfolgt, um JavaScript Object Notation (JSON)-Aufrufen von ASP.NET AJAX-Seiten an .NET-Webdienste mithilfe eines JavaScript-Webdienst Proxys zuzulassen. ASP.NET AJAX sendet JSON-Nachrichten anstelle der standardmäßigen SOAP-Aufrufe (Simple Object Access Protocol), die normalerweise Webdiensten zugeordnet sind, an Webdienste. Dies führt zu kleineren Anforderungs-und Antwort Nachrichten. Außerdem ist eine effizientere Client seitige Verarbeitung von Daten möglich, da die ASP.NET AJAX-JavaScript-Bibliothek für die Arbeit mit JSON-Objekten optimiert ist. In der Liste 2 und in der Liste 3 werden Beispiele für Webdienst-Anforderungs-und-Antwort Nachrichten angezeigt, die im JSON-Format Die in der Liste 2 angezeigte Anforderungs Nachricht übergibt einen Country-Parameter mit dem Wert "Belgien", während die Antwortnachricht in der Liste 3 ein Array von Kunden Objekten und deren zugeordneten Eigenschaften übergibt.

**Codebeispiel 2. Nach JSON serialisierte Webdienst-Anforderungs Nachricht**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]der Vorgangs Name wird als Teil der URL zum Webdienst definiert. Darüber hinaus werden Anforderungs Nachrichten nicht immer über JSON übermittelt. Webdienste können das ScriptMethod-Attribut verwenden, bei dem der UseHttpGet-Parameter auf "true" festgelegt ist. Dadurch werden Parameter über die Abfrage Zeichenfolgen-Parameter übergeben.*

**Codebeispiel 3. In JSON serialisierte Webdienst-Antwortnachricht**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

Im nächsten Abschnitt erfahren Sie, wie Sie Webdienste erstellen können, mit denen JSON-Anforderungs Nachrichten verarbeitet und sowohl mit einfachen als auch komplexen Typen beantwortet werden können.

## <a name="creating-ajax-enabled-web-services"></a>Erstellen von AJAX-aktivierten Webdiensten

Das ASP.NET AJAX-Framework bietet verschiedene Methoden zum Aufrufen von Webdiensten. Sie können das AutoCompleteExtender-Steuerelement (verfügbar im ASP.NET AJAX Toolkit) oder JavaScript verwenden. Vor dem Aufrufen eines Dienstanbieter müssen Sie es jedoch AJAX-aktivieren, damit es von Client-Skriptcode aufgerufen werden kann.

Unabhängig davon, ob Sie noch nicht mit ASP.NET-Webdiensten vertraut sind, ist es einfach, Dienste zu erstellen und AJAX-Dienste zu aktivieren. .NET Framework hat die Erstellung von ASP.NET-Webdiensten seit der ersten Veröffentlichung in 2002 und den ASP.NET AJAX-Erweiterungen unterstützt, die zusätzliche AJAX-Funktionen bereitstellen, die auf dem Standardsatz von Features von .NET Framework aufbauen. Visual Studio .net 2008 Beta 2 verfügt über integrierte Unterstützung für das Erstellen von ASMX-Webdienst Dateien und leitet den zugeordneten Code neben Klassen aus der System. Web. Services. WebService-Klasse automatisch ab. Wenn Sie der-Klasse Methoden hinzufügen, müssen Sie das WebMethod-Attribut anwenden, damit Sie von webdienstconsumern aufgerufen werden.

Codebeispiel 4 zeigt ein Beispiel für das Anwenden des WebMethod-Attributs auf eine Methode mit dem Namen getcustomersbycountry ().

**Codebeispiel 4. Verwenden des WebMethod-Attributs in einem Webdienst**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

Die getcustomersbycountry ()-Methode akzeptiert einen Country-Parameter und gibt ein Customer-Objekt Array zurück. Der an die Methode übergebenen Länder Wert wird an eine Geschäfts Schicht Klasse weitergeleitet, die wiederum eine datenebenenklasse aufruft, um die Daten aus der Datenbank abzurufen, die Eigenschaften des Kunden Objekts mit Daten füllen und das Array zurückgeben.

## <a name="using-the-scriptservice-attribute"></a>Verwenden des ScriptService-Attributs

Beim Hinzufügen des WebMethod-Attributs kann die getcustomersbycountry ()-Methode von Clients aufgerufen werden, die Standard-SOAP-Nachrichten an den Webdienst senden. es ist nicht zulässig, dass JSON-Aufrufe von ASP.NET AJAX-Anwendungen standardmäßig durchgeführt werden. Damit JSON-Aufrufe durchgeführt werden können, müssen Sie das-Attribut der ASP.NET AJAX-Erweiterung `ScriptService` auf die Webdienst Klasse anwenden. Dies ermöglicht es einem Webdienst, mithilfe von JSON formatierte Antwort Nachrichten zu senden und Client seitiges Skript das Abrufen eines Diensts durch Senden von JSON-Nachrichten zu ermöglichen.

In der Liste 5 wird ein Beispiel für das Anwenden des ScriptService-Attributs auf eine Webdienst Klasse mit dem Namen CustomersService veranschaulicht.

**Codebeispiel 5. Verwenden des ScriptService-Attributs für AJAX: Aktivieren eines Webdiensts**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

Das ScriptService-Attribut fungiert als Marker, das angibt, dass es von AJAX-Skriptcode aufgerufen werden kann. Sie verarbeitet keine der JSON-Serialisierungs-oder deserialisierungsaufgaben, die im Hintergrund auftreten. Die ScriptHandlerFactory (in web.config konfiguriert) und andere verwandte Klassen führen den Großteil der JSON-Verarbeitung aus.

## <a name="using-the-scriptmethod-attribute"></a>Verwenden des ScriptMethod-Attributs

Das ScriptService-Attribut ist das einzige ASP.NET AJAX-Attribut, das in einem .NET-Webdienst definiert werden muss, damit es von ASP.NET AJAX-Seiten verwendet werden kann. Ein anderes Attribut mit dem Namen "ScriptMethod" kann jedoch auch direkt auf Webmethoden in einem Dienst angewendet werden. ScriptMethod definiert drei Eigenschaften `UseHttpGet` , einschließlich, `ResponseFormat` und `XmlSerializeString` . Das Ändern der Werte dieser Eigenschaften kann in Fällen nützlich sein, in denen der von einer Webmethode akzeptierte Anforderungstyp zu Get geändert werden muss, wenn eine Webmethode unformatierte XML-Daten in Form eines-oder-Objekts zurückgeben muss `XmlDocument` `XmlElement` oder wenn Daten, die von einem Dienst zurückgegeben werden, immer als XML anstelle von JSON serialisiert werden sollen.

Die UseHttpGet-Eigenschaft kann verwendet werden, wenn eine Webmethode Get-Anforderungen anstelle von Post-Anforderungen akzeptieren soll. Anforderungen werden mithilfe einer URL gesendet, bei der Eingabeparameter für die Webmethode in QueryString-Parameter konvertiert wurden. Die UseHttpGet-Eigenschaft ist standardmäßig auf false festgelegt und sollte nur auf festgelegt werden, `true` Wenn Vorgänge bekanntermaßen sicher sind und sensible Daten nicht an einen Webdienst übergeben werden. In der Liste 6 wird ein Beispiel für die Verwendung des ScriptMethod-Attributs mit der UseHttpGet-Eigenschaft gezeigt.

**Codebeispiel 6. Verwenden des ScriptMethod-Attributs mit der UseHttpGet-Eigenschaft.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

Ein Beispiel für die Header, die gesendet werden, wenn die in Auflistung 6 gezeigte Webmethode httpgetecho aufgerufen wird, wird als nächstes angezeigt:

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

Das ScriptMethod-Attribut kann nicht nur zum Zulassen von HTTP GET-Anforderungen, sondern auch verwendet werden, wenn XML-Antworten von einem Dienst anstelle von JSON zurückgegeben werden müssen. Ein Webdienst kann z. b. einen RSS-Feed von einer Remote Website abrufen und als XmlDocument-oder XmlElement-Objekt zurückgeben. Die Verarbeitung der XML-Daten kann dann auf dem Client erfolgen.

In der Liste 7 wird ein Beispiel für die Verwendung der Response Format-Eigenschaft verwendet, um anzugeben, dass XML-Daten von einer Webmethode zurückgegeben werden sollen.

**Codebeispiel 7: Verwenden des ScriptMethod-Attributs mit der Response Format-Eigenschaft.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

Die Response Format-Eigenschaft kann auch zusammen mit der XmlSerializeString-Eigenschaft verwendet werden. Die XmlSerializeString-Eigenschaft hat den Standardwert false. Dies bedeutet, dass alle Rückgabe Typen außer Zeichen folgen, die von einer Webmethode zurückgegeben werden, als XML serialisiert werden, wenn die- `ResponseFormat` Eigenschaft auf festgelegt ist `ResponseFormat.Xml` . Wenn `XmlSerializeString` auf festgelegt ist `true` , werden alle Typen, die von einer Webmethode zurückgegeben werden, als XML-Zeichen folgen Typen serialisiert. Wenn die Response Format-Eigenschaft den Wert hat, `ResponseFormat.Json` wird die XmlSerializeString-Eigenschaft ignoriert.

In der Liste 8 ist ein Beispiel für die Verwendung der XmlSerializeString-Eigenschaft zum Erzwingen der Serialisierung von Zeichen folgen als XML dargestellt.

**Codebeispiel 8. Verwenden des ScriptMethod-Attributs mit der XmlSerializeString-Eigenschaft**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

Der Wert, der durch Aufrufen der in der Liste 8 dargestellten getxmlstring-Webmethode zurückgegeben wird, wird als nächstes angezeigt:

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

Obwohl das standardmäßige JSON-Format die Gesamtgröße der Anforderungs-und Antwort Nachrichten minimiert und leichter von ASP.NET AJAX-Clients in einem Browser übergreifenden Weise genutzt werden kann, können die Eigenschaften Response Format und XmlSerializeString verwendet werden, wenn Client Anwendungen wie Internet Explorer 5 oder höher davon ausgehen, dass XML-Daten von einer Webmethode zurückgegeben werden.

## <a name="working-with-complex-types"></a>Arbeiten mit komplexen Typen

In der Liste 5 wurde ein Beispiel für das Zurückgeben eines komplexen Typs mit dem Namen Customer von einem Webdienst gezeigt. Die Customer-Klasse definiert mehrere verschiedene einfache Typen intern als Eigenschaften wie "FirstName" und "LastName". Komplexe Typen, die als Eingabeparameter oder Rückgabetyp für eine AJAX-aktivierte Webmethode verwendet werden, werden automatisch in JSON serialisiert, bevor Sie an die Clientseite gesendet werden. Allerdings werden geschachtelte komplexe Typen (die intern in einem anderen Typ definiert sind) dem Client nicht standardmäßig als eigenständige Objekte zur Verfügung gestellt.

In Fällen, in denen ein von einem Webdienst verwendeter, von einem Webdienst verwendeter komplexer Typ auch auf einer Clientseite verwendet werden muss, kann das ASP.NET AJAX GenerateScriptType-Attribut zum Webdienst hinzugefügt werden. Beispielsweise enthält die in der Liste 9 angezeigte customerdetails-Klasse Adress-und Geschlecht-Eigenschaften, die die in der Liste enthaltenen ***komplexen Typen darstellen.***

**Codebeispiel 9. Die hier gezeigte customerdetails-Klasse enthält zwei komplexe komplexe Typen.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

Die Adress-und Geschlecht-Objekte, die in der customerdetails-Klasse in der Liste 9 definiert sind, werden nicht automatisch zur Verwendung auf der Clientseite über JavaScript zur Verfügung gestellt, da es sich um geschachtelte Typen handelt (Adresse ist eine Klasse und Geschlecht ist eine Enumeration). In Fällen, in denen ein geschachtelter Typ, der in einem Webdienst verwendet wird, auf der Clientseite verfügbar sein muss, kann das zuvor erwähnte GenerateScriptType-Attribut verwendet werden (siehe Codebeispiel 10). Dieses Attribut kann mehrmals hinzugefügt werden, wenn verschiedene, komplexe komplexe Typen von einem Dienst zurückgegeben werden. Sie kann direkt auf die Webdienst Klasse oder über bestimmte Webmethoden angewendet werden.

**Codebeispiel 10. Verwenden des generatescriptservice-Attributs zum Definieren von für den Client verfügbaren Typen.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

Durch Anwenden des `GenerateScriptType` -Attributs auf den Webdienst werden die Adress-und die Geschlecht-Typen automatisch zur Verwendung durch Client seitigen ASP.NET AJAX-JavaScript-Code zur Verfügung gestellt. Ein Beispiel für das JavaScript, das automatisch generiert und an den Client gesendet wird, indem das GenerateScriptType-Attribut für einen Webdienst hinzugefügt wird, wird in der Liste 11 angezeigt. Weiter unten in diesem Artikel erfahren Sie, wie Sie die folgenden komplexen Typen verwenden.

**Codebeispiel 11. Die für eine ASP.NET AJAX-Seite zur Verfügung gestellten komplexen komplexen Typen.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

Nachdem Sie nun gesehen haben, wie Sie Webdienste erstellen und für ASP.NET AJAX-Seiten zugänglich machen, betrachten wir nun die Erstellung und Verwendung von JavaScript-Proxys, damit Daten abgerufen oder an Webdienste gesendet werden können.

## <a name="creating-javascript-proxies"></a>JavaScript-Proxys

Das Aufrufen eines Standardweb Diensts (.net oder eine andere Plattform) umfasst in der Regel das Erstellen eines Proxy Objekts, das Sie vor den Komplexitäten zum Senden von SOAP-Anforderungs-und Antwort Nachrichten Mit ASP.NET AJAX-Webdienst aufrufen können JavaScript-Proxys erstellt und verwendet werden, um problemlos Dienste aufzurufen, ohne sich Gedanken über das Serialisieren und Deserialisieren von JSON-Nachrichten JavaScript-Proxys können automatisch mit dem ASP.NET AJAX-ScriptManager-Steuerelement generiert werden.

Das Erstellen eines JavaScript-Proxys, der Webdienste aufzurufen, erfolgt mithilfe der Services-Eigenschaft von ScriptManager. Mit dieser Eigenschaft können Sie einen oder mehrere Dienste definieren, die von einer ASP.NET AJAX-Seite asynchron aufgerufen werden können, um Daten zu senden oder zu empfangen, ohne dass Post Back Vorgänge erforderlich sind. Sie definieren einen Dienst, indem Sie das ASP.NET AJAX `ServiceReference` -Steuerelement verwenden und die Webdienst-URL der-Eigenschaft des Steuer Elements zuweisen `Path` . In der Liste 12 wird ein Beispiel für den Verweis auf einen Dienst mit dem Namen "CustomersService. asmx" veranschaulicht.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**Auflistung 12. Definieren eines Webdiensts, der auf einer ASP.NET AJAX-Seite verwendet wird.**

Durch das Hinzufügen eines Verweises auf "CustomersService. asmx" über das ScriptManager-Steuerelement wird ein JavaScript-Proxy dynamisch generiert und auf die Seite verwiesen. Der Proxy wird mithilfe des &lt; &gt; Skripttags eingebettet und dynamisch geladen, indem die Datei CustomersService. asmx aufgerufen und/JS am Ende der Datei angehängt wird. Im folgenden Beispiel wird gezeigt, wie der JavaScript-Proxy auf der Seite eingebettet wird, wenn das Debuggen in web.config deaktiviert ist:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]Wenn Sie den tatsächlich generierten JavaScript-Proxycode anzeigen möchten, können Sie die URL für den gewünschten .NET-Webdienst in das Adressfeld von Internet Explorer eingeben und/JS am Ende der Datei anfügen.*

Wenn das Debuggen in aktiviert ist web.config wird eine Debugversion des JavaScript-Proxys auf der Seite eingebettet, wie im folgenden dargestellt:

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

Der von ScriptManager erstellte JavaScript-Proxy kann auch direkt in die Seite eingebettet werden, anstatt mit dem &lt; &gt; src-Attribut des Skripttags darauf zu verweisen. Dies kann erreicht werden, indem die InlineScript-Eigenschaft des servicereferenzierungssteuerelements auf true festgelegt wird (der Standardwert ist false). Dies kann hilfreich sein, wenn ein Proxy nicht über mehrere Seiten hinweg gemeinsam genutzt wird und Sie die Anzahl der Netzwerk Aufrufe verringern möchten, die an den Server gerichtet sind. Wenn InlineScript auf true festgelegt ist, wird das Proxy Skript nicht vom Browser zwischengespeichert, sodass der Standardwert false in Fällen empfohlen wird, in denen der Proxy von mehreren Seiten in einer ASP.NET AJAX-Anwendung verwendet wird. Im folgenden wird ein Beispiel für die Verwendung der InlineScript-Eigenschaft angezeigt:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>JavaScript-Proxys

Sobald auf einen Webdienst durch eine ASP.NET AJAX-Seite mithilfe des ScriptManager-Steuer Elements verwiesen wird, kann ein-Rückruf an den Webdienst gesendet werden, und die zurückgegebenen Daten können mithilfe von Rückruf Funktionen verarbeitet werden. Ein Webdienst wird aufgerufen, indem auf seinen Namespace (sofern vorhanden), den Klassennamen und den Namen der Webmethode verwiesen wird. Alle Parameter, die an den Webdienst übermittelt werden, können zusammen mit einer Rückruffunktion definiert werden, die die zurückgegebenen Daten verarbeitet.

Ein Beispiel für die Verwendung eines JavaScript-Proxys zum Aufrufen einer Webmethode namens getcustomersbycountry () finden Sie in der Liste 13. Die getcustomersbycountry ()-Funktion wird aufgerufen, wenn ein Endbenutzer auf eine Schaltfläche auf der Seite klickt.

**Codebeispiel 13. Aufrufen eines Webdiensts mit einem JavaScript-Proxy**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

Dieser Rückruf verweist auf den interfacetraining-Namespace, die CustomersService-Klasse und die getcustomersbycountry-Webmethode, die im Dienst definiert sind. Sie übergibt einen Länder Wert, der aus einem Textfeld abgerufen wurde, sowie eine Rückruffunktion mit dem Namen "onwsrequestcomplete", die aufgerufen werden soll, wenn der asynchrone Webdienst Aufruf zurückgegeben wird. Onwsrequestcomplete verarbeitet das Array von Kunden Objekten, die vom Dienst zurückgegeben werden, und konvertiert sie in eine Tabelle, die auf der Seite angezeigt wird. Die aus dem-Befehl generierte Ausgabe ist in Abbildung 1 dargestellt.

[![Binden von Daten, die durch einen asynchronen AJAX-Aufrufe eines Webdiensts abgerufen werden.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**Abbildung 1**: Binden von Daten, die durch das Ausführen eines asynchronen AJAX-Aufrufes an einen Webdienst abgerufen werden.  ([Klicken Sie, um das Bild in voller Größe anzuzeigen](understanding-asp-net-ajax-web-services/_static/image3.png))

JavaScript-Proxys können auch unidirektionale Aufrufe an Webdienste durchführen, wenn eine Webmethode aufgerufen werden soll, der Proxy jedoch nicht auf eine Antwort warten sollte. Beispielsweise können Sie einen Webdienst zum Starten eines Prozesses, z. b. eines Arbeits Flusses, abrufen, jedoch nicht auf einen Rückgabewert vom Dienst warten. In Fällen, in denen ein unidirektionaler Aufrufs an einen Dienst vorgenommen werden muss, kann die in der Liste 13 gezeigte Rückruffunktion einfach ausgelassen werden. Da keine Rückruffunktion definiert ist, wartet das Proxy Objekt nicht, bis der Webdienst Daten zurückgibt.

## <a name="handling-errors"></a>Behandeln von Fehlern

Asynchrone Rückrufe an Webdienste können auf unterschiedliche Arten von Fehlern stoßen, z. b. wenn das Netzwerk ausfällt, der Webdienst nicht verfügbar ist oder eine Ausnahme zurückgegeben wird. Glücklicherweise ermöglichen JavaScript-Proxy Objekte, die vom ScriptManager generiert werden, dass mehrere Rückrufe definiert werden, um Fehler und Fehler zusätzlich zu dem zuvor gezeigten Erfolgs Rückruf zu behandeln. Eine Fehler Rückruffunktion kann direkt nach der Standard Rückruffunktion im-Befehl der Webmethode definiert werden, wie in der Liste 14 dargestellt.

**Codebeispiel 14. Definieren einer Fehler Rückruffunktion und Anzeigen von Fehlern.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

Alle Fehler, die auftreten, wenn der Webdienst aufgerufen wird, veranlassen, dass die onwsrequestfailed ()-Rückruffunktion aufgerufen wird, die ein Objekt akzeptiert, das den Fehler als Parameter darstellt. Das Error-Objekt stellt mehrere verschiedene Funktionen zur Verfügung, um die Ursache des Fehlers zu ermitteln, und gibt an, ob der-Timeout abgebrochen wurde. In der Liste 14 wird ein Beispiel für die Verwendung der verschiedenen Fehlerfunktionen veranschaulicht, und Abbildung 2 zeigt ein Beispiel für die Ausgabe, die von den Funktionen generiert wird.

[![Ausgabe, die durch Aufrufen von ASP.NET AJAX-Fehlerfunktionen generiert wird.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**Abbildung 2**: Ausgabe, die durch den Aufruf von ASP.NET AJAX-Fehlerfunktionen generiert wird.  ([Klicken Sie, um das Bild in voller Größe anzuzeigen](understanding-asp-net-ajax-web-services/_static/image6.png))

## <a name="handling-xml-data-returned-from-a-web-service"></a>Verarbeiten von von einem Webdienst zurückgegebenen XML-Daten

Früher haben Sie gesehen, wie eine Webmethode unformatierte XML-Daten zurückgeben kann, indem das ScriptMethod-Attribut zusammen mit der Response Format-Eigenschaft verwendet wird. Wenn Response Format auf ResponseFormat.Xml festgelegt ist, werden vom Webdienst zurückgegebene Daten als XML und nicht als JSON serialisiert. Dies kann hilfreich sein, wenn XML-Daten für die Verarbeitung mithilfe von JavaScript oder XSLT direkt an den Client übermittelt werden müssen. Zum aktuellen Zeitpunkt stellt Internet Explorer 5 oder höher das beste Client seitige Objektmodell zum Durchsuchen und Filtern von XML-Daten aufgrund der integrierten Unterstützung für MSXML bereit.

Das Abrufen von XML-Daten von einem Webdienst unterscheidet sich nicht vom Abrufen anderer Datentypen. Starten Sie, indem Sie den JavaScript-Proxy aufrufen, um die entsprechende Funktion aufzurufen und eine Rückruffunktion zu definieren. Nachdem der Rückruf zurückgegeben wurde, können Sie die Daten in der Rückruffunktion verarbeiten.

In der Liste 15 wird ein Beispiel für den Aufruf einer Webmethode namens getrssfeed () gezeigt, die ein XmlElement-Objekt zurückgibt. Getrssfeed () akzeptiert einen einzelnen Parameter, der die URL für den abzurufenden RSS-Feed darstellt.

**Codebeispiel 15. Arbeiten mit XML-Daten, die von einem Webdienst zurückgegeben werden.**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

In diesem Beispiel wird eine URL an einen RSS-Feed weitergeleitet, und die zurückgegebenen XML-Daten werden in der onwsrequestcomplete ()-Funktion verarbeitet. Onwsrequestcomplete () prüft zunächst, ob der Browser Internet Explorer ist, um zu ermitteln, ob der MSXML-Parser verfügbar ist. Wenn dies der Fall ist, wird eine XPath-Anweisung verwendet, um alle &lt; Element &gt; Tags im RSS-Feed zu suchen. Jedes Element wird dann durchlaufen, und die zugeordneten &lt; Titel und Verknüpfungs &gt; &lt; &gt; Tags werden gefunden und verarbeitet, um die Daten jedes Elements anzuzeigen. Abbildung 3 zeigt ein Beispiel für die Ausgabe, die bei einem ASP.NET AJAX-Aufrufe über einen JavaScript-Proxy zur getrssfeed ()-Webmethode generiert wurde.

## <a name="handling-complex-types"></a>Behandeln komplexer Typen

Komplexe Typen, die von einem Webdienst akzeptiert oder zurückgegeben werden, werden automatisch über einen JavaScript-Proxy verfügbar gemacht. Es ist jedoch nicht möglich, auf die auf der Clientseite basierenden komplexen Typen direkt zu zugreifen, es sei denn, das GenerateScriptType-Attribut wird wie zuvor erläutert auf den Dienst angewendet. Warum möchten Sie einen geschosteten komplexen Typ auf der Clientseite verwenden?

Um diese Frage zu beantworten, gehen Sie davon aus, dass eine ASP.NET AJAX-Seite Kundendaten anzeigt und es Endbenutzern ermöglicht, die Adresse eines Kunden zu aktualisieren. Wenn der Webdienst angibt, dass der Adresstyp (ein komplexer Typ, der in einer customerdetails-Klasse definiert ist) an den Client gesendet werden kann, kann der Aktualisierungsprozess in separate Funktionen aufgeteilt werden, um die Wiederverwendung des Codes zu verbessern.

[![Ausgabe aus dem Aufrufen eines Webdiensts, der RSS-Daten zurückgibt.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**Abbildung 3**: Ausgabe aus dem Aufrufen eines Webdiensts, der RSS-Daten zurückgibt.  ([Klicken Sie, um das Bild in voller Größe anzuzeigen](understanding-asp-net-ajax-web-services/_static/image9.png))

Codebeispiel 16 zeigt ein Beispiel für Client seitigen Code, der ein Adress Objekt aufruft, das in einem Modell Namespace definiert ist, es mit aktualisierten Daten füllt und es der Address-Eigenschaft eines customerdetails-Objekts zuweist. Das customerdetails-Objekt wird dann zur Verarbeitung an den Webdienst weitergegeben.

**Codebeispiel 16. Verwenden von komplexen komplexen Typen**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>Erstellen und Verwenden von Seiten Methoden

Webdienste stellen eine hervorragende Möglichkeit dar, wiederverwendbare Dienste für eine Vielzahl von Clients verfügbar zu machen, einschließlich ASP.NET AJAX-Seiten. Es gibt jedoch Fälle, in denen eine Seite Daten abrufen muss, die nie von anderen Seiten verwendet oder freigegeben werden. In diesem Fall scheint eine ASMX-Datei so zu sein, dass die Seite auf die Daten zugreifen kann, da der Dienst nur von einer einzelnen Seite verwendet wird.

ASP.NET AJAX bietet einen weiteren Mechanismus zum Erstellen von Webdienst ähnlichen aufrufen, ohne eigenständige ASMX-Dateien zu erstellen. Dies erfolgt mithilfe einer Technik, die als "Seiten Methoden" bezeichnet wird. Seiten Methoden sind statische (Shared in VB.net) Methoden, die direkt in eine Seite oder eine Code neben Datei eingebettet sind, auf die das WebMethod-Attribut angewendet wird. Durch Anwenden des WebMethod-Attributs können Sie mithilfe eines speziellen JavaScript-Objekts namens PageMethods aufgerufen werden, das zur Laufzeit dynamisch erstellt wird. Das PageMethods-Objekt fungiert als Proxy, der Sie vor dem JSON-Serialisierungs-/Deserialisierungsprozess schützt. Beachten Sie, dass Sie die EnablePageMethods-Eigenschaft von ScriptManager auf true festlegen müssen, damit Sie das PageMethods-Objekt verwenden können.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

In der Liste 17 finden Sie ein Beispiel für die Definition von zwei Seiten Methoden in einer ASP.NET-Code-neben Klasse. Diese Methoden rufen Daten von einer Geschäfts Schicht Klasse ab, die sich im APP- \_ Code Ordner der Website befindet.

**Codebeispiel 17. Definieren von Seiten Methoden**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

Wenn ScriptManager das vorhanden sein von Webmethoden auf der Seite erkennt, generiert es einen dynamischen Verweis auf das zuvor erwähnte PageMethods-Objekt. Der Aufruf einer Webmethode erfolgt durch Verweisen auf die PageMethods-Klasse, gefolgt vom Namen der Methode und allen erforderlichen Parameterdaten, die übergeben werden sollten. In der Liste 18 werden Beispiele für das Aufrufen der zuvor gezeigten zwei Seiten Methoden veranschaulicht.

**Codebeispiel 18. Aufrufen von Seiten Methoden mit dem PageMethods JavaScript-Objekt.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

Die Verwendung des PageMethods-Objekts ähnelt sehr der Verwendung eines JavaScript-Proxy Objekts. Sie geben zuerst alle Parameterdaten an, die an die Seiten Methode übergeben werden sollen, und definieren dann die Rückruffunktion, die aufgerufen werden soll, wenn der asynchrone Aufruf zurückgegeben wird. Ein Fehler Rückruf kann auch angegeben werden (in der Liste 14 finden Sie ein Beispiel für das Behandeln von Fehlern).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender und das ASP.NET AJAX-Toolkit

Das ASP.NET AJAX Toolkit (verfügbar [http://ajax.asp.net](http://ajax.asp.net) über) bietet mehrere Steuerelemente, die für den Zugriff auf Webdienste verwendet werden können. Insbesondere enthält das Toolkit ein nützliches Steuerelement mit dem Namen `AutoCompleteExtender` , das verwendet werden kann, um Webdienste aufzurufen und Daten auf Seiten anzuzeigen, ohne JavaScript-Code schreiben zu müssen.

Das AutoCompleteExtender-Steuerelement kann verwendet werden, um vorhandene Funktionen eines Textfelds zu erweitern und Benutzern das Auffinden von Daten zu erleichtern, nach denen Sie suchen. Beim eingeben in ein Textfeld kann das Steuerelement verwendet werden, um einen Webdienst abzufragen und die Ergebnisse unter dem Textfeld dynamisch anzuzeigen. Abbildung 4 zeigt ein Beispiel für die Verwendung des AutoCompleteExtender-Steuer Elements, um Kunden-IDs für eine Support Anwendung anzuzeigen. Wenn der Benutzer unterschiedliche Zeichen in das Textfeld eingibt, werden unterschiedliche Elemente basierend auf der Eingabe angezeigt. Benutzer können dann die gewünschte Kunden-ID auswählen.

Die Verwendung von AutoCompleteExtender innerhalb einer ASP.NET AJAX-Seite erfordert, dass die AjaxControlToolkit.dll-Assembly dem Ordner "bin" der Website hinzugefügt wird. Nachdem die Toolkit-Assembly hinzugefügt wurde, möchten Sie in web.config darauf verweisen, sodass die darin enthaltenen Steuerelemente für alle Seiten in einer Anwendung verfügbar sind. Dies kann durch Hinzufügen des folgenden Tags innerhalb des Tags der web.config Steuerelemente erreicht werden &lt; &gt; :

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

In Fällen, in denen Sie nur das-Steuerelement auf einer bestimmten Seite verwenden müssen, können Sie darauf verweisen, indem Sie die Reference-Direktive am oberen Rand einer Seite hinzufügen, anstatt web.config zu aktualisieren:

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![Verwenden des AutoCompleteExtender-Steuer Elements.](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**Abbildung 4**: Verwenden des AutoCompleteExtender-Steuer Elements  ([Klicken Sie, um das Bild in voller Größe anzuzeigen](understanding-asp-net-ajax-web-services/_static/image12.png))

Nachdem die Website für die Verwendung des ASP.NET AJAX-Toolkits konfiguriert wurde, kann der Seite ein AutoCompleteExtender-Steuerelement hinzugefügt werden, ähnlich wie Sie ein reguläres ASP.NET-Server Steuerelement hinzufügen. In der Liste 19 wird ein Beispiel für die Verwendung des-Steuer Elements zum Abrufen eines Webdiensts gezeigt.

**Codebeispiel 19. Verwenden des ASP.NET AJAX Toolkit AutoCompleteExtender-Steuer Elements.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

Der AutoCompleteExtender verfügt über verschiedene Eigenschaften, einschließlich der Standard-ID und der runat-Eigenschaften, die auf Server Steuerelementen gefunden werden. Darüber hinaus können Sie mit dieser Option definieren, wie viele Zeichen ein Endbenutzer eingibt, bevor der Webdienst Daten abgefragt. Die in der Liste 19 angezeigte MinimumPrefixLength-Eigenschaft bewirkt, dass der Dienst jedes Mal aufgerufen wird, wenn ein Zeichen in das Textfeld eingegeben wird. Sie sollten darauf achten, diesen Wert festzulegen, da der Benutzer jedes Mal ein Zeichen eingibt, dass der Webdienst nach Werten sucht, die mit den Zeichen im Textfeld verglichen werden. Der aufzurufende Webdienst und die Ziel-Webmethode werden mithilfe der servicepath-bzw. ServiceMethod-Eigenschaften definiert. Schließlich gibt die TargetControlID-Eigenschaft an, an welches Textfeld das AutoCompleteExtender-Steuerelement gebunden werden soll.

Für den aufgerufenen Webdienst muss das ScriptService-Attribut wie bereits erläutert angewendet werden, und die Ziel-Webmethode muss zwei Parameter mit den Namen "PrefixText" und "count" akzeptieren. Der PrefixText-Parameter stellt die vom Endbenutzer eingegebenen Zeichen dar, und der count-Parameter gibt an, wie viele Elemente zurückgegeben werden sollen (der Standardwert ist 10). In der Liste 20 wird ein Beispiel für die getcustomerids-Webmethode angezeigt, die vom AutoCompleteExtender-Steuerelement aufgerufen wird, das zuvor in der Liste 19 Die Webmethode Ruft eine Geschäfts Schicht Methode auf, die wiederum eine datenebenenmethode aufruft, die das Filtern der Daten und das Zurückgeben der übereinstimmenden Ergebnisse behandelt. Der Code für die Datenschicht Methode wird in der Liste 21 angezeigt.

**Auflistung 20. Filtern von Daten, die vom AutoCompleteExtender-Steuerelement gesendet werden.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**Codebeispiel 21. Filtern von Ergebnissen basierend auf der Eingabe von Endbenutzern.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>Zusammenfassung

ASP.NET AJAX bietet hervorragende Unterstützung für das Aufrufen von Webdiensten, ohne viel benutzerdefinierten JavaScript-Code zum Verarbeiten der Anforderungs-und Antwort Nachrichten zu schreiben. In diesem Artikel haben Sie erfahren, wie Sie .NET-Webdienste mit AJAX aktivieren, damit sie JSON-Nachrichten verarbeiten und JavaScript-Proxys mit dem ScriptManager-Steuerelement definieren können. Sie haben auch gesehen, wie JavaScript-Proxys verwendet werden können, um Webdienste aufzurufen, einfache und komplexe Typen zu verarbeiten und Fehler zu behandeln. Schließlich haben Sie gesehen, wie Seiten Methoden verwendet werden können, um den Prozess der Erstellung und Erstellung von Webdienst aufrufen zu vereinfachen, und wie das AutoCompleteExtender-Steuerelement den Endbenutzern bei der Eingabehilfe zur Verfügung stellen kann. Obwohl das in ASP.NET AJAX verfügbare Update Panel sicherlich die Wahl für viele AJAX-Programmierer ist, ist dies aufgrund seiner Einfachheit von Bedeutung. das wissen, wie Webdienste über JavaScript-Proxys aufgerufen werden können, kann in vielen Anwendungen nützlich sein.

## <a name="bio"></a>Biografie

Dan Wahlin (Microsoft Most Valuable Professional für ASP.net und XML Web Services) ist ein .net-Entwicklungs Dozenten und-architekturberater bei Interface Technical Training ( [http://www.interfacett.com](http://www.interfacett.com) ). Dan gründete die XML for ASP.NET Developers-Website ([www.XMLforASP.net](http://www.XMLforASP.NET)), ist im Büro des INETA-Referenten und spricht auf mehreren Konferenzen. Dan hat eine professionelle Windows-DNA (Wrox), ASP.net: Tipps, Tutorials und Code (Sams), ASP.NET 1,1 Insider Solutions, Professional ASP.NET 2,0 AJAX (Wrox), ASP.NET 2,0 MVP-Hacks und erstellte XML for ASP.NET Developers (Sams) verfasst. Beim Schreiben von Code, Artikeln oder Büchern hat Dan das Schreiben und Aufzeichnen von Musik und das Spielen von Golf und Basketball mit seiner Frau und ihren Kindern.

Scott Cate arbeitet seit 1997 mit Microsoft-Webtechnologien und ist der Präsident von myKB.com ([www.myKB.com](http://www.myKB.com)), wo er sich darauf spezialisiert hat, ASP.NET basierte Anwendungen zu schreiben, die sich auf die Software Lösungen der Wissensdatenbank konzentrieren. Scott kann per e-Mail unter oder in [scott.cate@myKB.com](mailto:scott.cate@myKB.com) seinem Blog unter [ScottCate.com](http://ScottCate.com) kontaktiert werden.

> [!div class="step-by-step"]
> [Zurück](understanding-asp-net-ajax-localization.md)
> [Weiter](understanding-asp-net-ajax-debugging-capabilities.md)
