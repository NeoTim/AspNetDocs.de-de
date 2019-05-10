---
uid: whitepapers/request-validation
title: Anforderungsvalidierung – Schutz vor Angriffen durch Skripteinschleusung | Microsoft-Dokumentation
author: rick-anderson
description: In diesem Artikel wird beschrieben, die Anforderung Überprüfungsfunktion von ASP.NET, wird standardmäßig die Anwendung verhindert wird von der Verarbeitung nicht codierte HTML-Inhalt senden...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130494"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="1de59-103">Anforderungsvalidierung – Schutz vor Angriffen durch Skripteinschleusung</span><span class="sxs-lookup"><span data-stu-id="1de59-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="1de59-104">Dieser Artikel beschreibt die Anforderung Überprüfungsfunktion von ASP.NET, wird standardmäßig die Anwendung verhindert wird von der Verarbeitung nicht codierte HTML-Inhalt an den Server gesendet.</span><span class="sxs-lookup"><span data-stu-id="1de59-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="1de59-105">Diese Anforderung Überprüfung-Funktion kann deaktiviert werden, wenn die Anwendung entwickelt wurde, um HTML-Daten sicher zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="1de59-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="1de59-106">Gilt für ASP.NET 1.1 und ASP.NET 2.0.</span><span class="sxs-lookup"><span data-stu-id="1de59-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="1de59-107">Anforderungsvalidierung, ein Feature von ASP.NET, seit Version 1.1, wird verhindert, dass der Server Inhalte mit nicht codierten HTML akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="1de59-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="1de59-108">Dieses Feature wurde entwickelt, um zu verhindern einige Script-Injection-Angriffen, bei dem Clientskriptcode oder HTML unbewusst an einen Server übermittelt, gespeichert und werden kann, klicken Sie dann anderen Benutzern angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1de59-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="1de59-109">Es wird weiterhin dringend empfohlen, dass Sie überprüfen, dass alle Eingabedaten und HTML codieren, die bei Bedarf.</span><span class="sxs-lookup"><span data-stu-id="1de59-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="1de59-110">Beispielsweise erstellen Sie eine Webseite, die anfordert, die e-Mail-Adresse eines Benutzers und dann speichert, die e-Mail-Adresse in einer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="1de59-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="1de59-111">Wenn der Benutzer eingibt &lt;Skript&gt;Warnung ("Hello from Script")&lt;/SCRIPT&gt; anstelle einer gültigen e-Mail-Adresse, wenn die Daten angezeigt werden, dieses Skript kann ausgeführt werden, wenn der Inhalt nicht ordnungsgemäß codiert wurde.</span><span class="sxs-lookup"><span data-stu-id="1de59-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="1de59-112">Die Anforderung Überprüfungsfunktion von ASP.NET verhindert dies.</span><span class="sxs-lookup"><span data-stu-id="1de59-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="1de59-113">Warum ist diese Funktion nützlich</span><span class="sxs-lookup"><span data-stu-id="1de59-113">Why this feature is useful</span></span>

<span data-ttu-id="1de59-114">Viele Websites sind nicht beachten Sie, dass sie für einfache Skript-Injection-Angriffe geöffnet sind.</span><span class="sxs-lookup"><span data-stu-id="1de59-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="1de59-115">Ob der Zweck dieser Art von der Website mit HTML handelt oder potenziell Clientskript zum Umleiten des Benutzers auf ein Hacker die Website ausgeführt ist, werden von Angriffen durch skripteinschleusung ein Problem, das Webentwickler mit befassen müssen.</span><span class="sxs-lookup"><span data-stu-id="1de59-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="1de59-116">Von Angriffen durch skripteinschleusung sind alle Webentwickler relevant, ob der ASP.NET, ASP oder anderen webtechnologien für die Entwicklung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1de59-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="1de59-117">Die ASP.NET-Validierungsfunktion für die Anforderung wird verhindert, dass proaktiv diese Angriffe durch nicht codierte HTML-Inhalt vom Server verarbeitet werden, es sei denn, der Entwickler entscheidet, um zuzulassen, dass der Inhalt nicht zugelassen.</span><span class="sxs-lookup"><span data-stu-id="1de59-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="1de59-118">Was Sie erwarten können: Fehler (Seite)</span><span class="sxs-lookup"><span data-stu-id="1de59-118">What to expect: Error Page</span></span>

<span data-ttu-id="1de59-119">Der nachstehende Screenshot zeigt einige Beispiel-ASP-Code:</span><span class="sxs-lookup"><span data-stu-id="1de59-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="1de59-120">Dieses Codes führt in eine einfache Seite, die Ihnen ermöglicht, geben Sie Text im Textfeld für die ausführen, klicken Sie auf die Schaltfläche, und zeigen Sie den Text in das Label-Steuerelement an:</span><span class="sxs-lookup"><span data-stu-id="1de59-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="1de59-121">Allerdings waren Sie z. B. JavaScript, `<script>alert("hello!")</script>` eingegeben und übermittelt, erhalten wir eine Ausnahme:</span><span class="sxs-lookup"><span data-stu-id="1de59-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="1de59-122">Die Fehlermeldung gibt an, dass eine "potenziell gefährliche Request.Form Value was detected" und enthält weitere Details in der Beschreibung, genau was aufgetreten ist und wie Sie das Verhalten zu ändern.</span><span class="sxs-lookup"><span data-stu-id="1de59-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="1de59-123">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1de59-123">For example:</span></span>

<span data-ttu-id="1de59-124">Request-Überprüfung hat einen Eingabewert potenziell gefährliche Client erkannt und Verarbeitung der Anforderung wurde abgebrochen.</span><span class="sxs-lookup"><span data-stu-id="1de59-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="1de59-125">Dieser Wert möglicherweise auf die Sicherheit Ihrer Anwendung, z. B. einen Cross-Site-scripting-Angriff beeinträchtigt.</span><span class="sxs-lookup"><span data-stu-id="1de59-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="1de59-126">Sie können die Request-Überprüfung deaktivieren, durch Festlegen von `validateRequest=false` in der Page-Direktive oder im Konfigurationsabschnitt.</span><span class="sxs-lookup"><span data-stu-id="1de59-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="1de59-127">Es wird jedoch dringend empfohlen, dass Ihre Anwendung explizit alle Eingaben in diesem Fall zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="1de59-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="1de59-128">Deaktivieren der Anforderungsvalidierung auf einer Seite</span><span class="sxs-lookup"><span data-stu-id="1de59-128">Disabling request validation on a page</span></span>

<span data-ttu-id="1de59-129">Anforderungsvalidierung auf einer Seite zu deaktivieren, Sie festlegen müssen, die `validateRequest` Attribut der Page-Direktive auf `false`:</span><span class="sxs-lookup"><span data-stu-id="1de59-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="1de59-130">Wenn Request-Überprüfung deaktiviert ist, kann Inhalte auf eine Seite gesendet werden; Es ist die Verantwortung für den Entwickler der Seite, um sicherzustellen, dass der Inhalt ordnungsgemäß codiert oder verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="1de59-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="1de59-131">Request-Überprüfung für Ihre Anwendung deaktivieren</span><span class="sxs-lookup"><span data-stu-id="1de59-131">Disabling request validation for your application</span></span>

<span data-ttu-id="1de59-132">Um die Anforderungsvalidierung für Ihre Anwendung zu deaktivieren, müssen Sie ändern oder erstellen Sie eine Web.config-Datei für Ihre Anwendung und das ValidateRequest-Attribut des der `<pages />` Abschnitt `false`:</span><span class="sxs-lookup"><span data-stu-id="1de59-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="1de59-133">Wenn Sie die Anforderungsvalidierung für alle Anwendungen auf dem Server deaktivieren möchten, können Sie diese Änderung der Datei "Machine.config" vornehmen.</span><span class="sxs-lookup"><span data-stu-id="1de59-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="1de59-134">Wenn die Request-Überprüfung deaktiviert ist, kann Inhalte für Ihre Anwendung gesendet werden; Es ist die Verantwortung für den Anwendungsentwickler, um sicherzustellen, dass der Inhalt ordnungsgemäß codiert oder verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="1de59-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="1de59-135">Der folgende Code wird geändert, um die Anforderungsvalidierung zu deaktivieren:</span><span class="sxs-lookup"><span data-stu-id="1de59-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="1de59-136">Wenn Sie der folgende JavaScript-Code in das Textfeld eingegeben wurde jetzt `<script>alert("hello!")</script>` das Ergebnis wäre:</span><span class="sxs-lookup"><span data-stu-id="1de59-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="1de59-137">Damit dies nicht geschieht, mit der Request-Überprüfung deaktiviert, müssen wir HTML-Codierung Inhalt.</span><span class="sxs-lookup"><span data-stu-id="1de59-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="1de59-138">Wie in HTML codieren Inhalt</span><span class="sxs-lookup"><span data-stu-id="1de59-138">How to HTML encode content</span></span>

<span data-ttu-id="1de59-139">Wenn Sie den Request-Überprüfung deaktiviert haben, ist es empfiehlt sich, HTML-Codierung von Inhalten, die für die zukünftige Verwendung gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="1de59-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="1de59-140">HTML-Codierung wird automatisch ersetzen "&lt;'oder'&gt;" (zusammen mit mehreren anderen Symbolen) mit ihren entsprechenden HTML-codierte Darstellung.</span><span class="sxs-lookup"><span data-stu-id="1de59-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="1de59-141">Z. B. "&lt;"wird ersetzt durch"&amp;Lt;' und '&gt;"wird ersetzt durch"&amp;Gt;".</span><span class="sxs-lookup"><span data-stu-id="1de59-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="1de59-142">Browser verwenden diese speziellen Codes zum Anzeigen der "&lt;'oder'&gt;" im Browser.</span><span class="sxs-lookup"><span data-stu-id="1de59-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="1de59-143">Inhalt kann ganz einfach HTML-codiert sein, auf dem Server mithilfe der `Server.HtmlEncode(string)` API.</span><span class="sxs-lookup"><span data-stu-id="1de59-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="1de59-144">Inhalt kann auch sein, einfach HTML-decodiert, d. h. auf standard HTML mit zurückgesetzt der `Server.HtmlDecode(string)` Methode.</span><span class="sxs-lookup"><span data-stu-id="1de59-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="1de59-145">Was zu:</span><span class="sxs-lookup"><span data-stu-id="1de59-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
