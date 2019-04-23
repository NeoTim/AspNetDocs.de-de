---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Gewusst wie:] Verwenden Sie der Reponse.Filter-Eigenschaft, um HTML-Code in eine ASP.NET-Seite ersetzen | Microsoft-Dokumentation'
author: rick-anderson
description: In diesem video Chris Pels veranschaulicht, wie die Reponse.Filter-Eigenschaft zum Abfangen und ändern den HTML-Code auf eine Seite gesendet werden. Zuerst wird eine Beispielseite w erstellt...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59403427"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[Gewusst wie:] Mithilfe der Reponse.Filter-Eigenschaft, um HTML-Code in eine ASP.NET-Seite zu ersetzen.

durch [Chris Pels](https://twitter.com/chrispels)

In diesem video Chris Pels veranschaulicht, wie die Reponse.Filter-Eigenschaft zum Abfangen und ändern den HTML-Code auf eine Seite gesendet werden. Zunächst wird eine Beispielseite mit einigen einfachen Text erstellt. Anschließend wird eine benutzerdefinierte Stream-Klasse erstellt, der dient, wie der Stream Ersatz für den aktuellen Stream, der an den Browser des Benutzers gesendet wird. In dieser Klasse abgeleiteten Streamklasse werden der Inhalt der Seite aus dem Stream verändert, und klicken Sie dann in den Antwortstream geschrieben abgerufen. In dieser benutzerdefinierte Stream-Klasse wird die Write-Methode angepasst. dazu ersetzen Sie den HTML-Code in den Basis-Datenstrom, und ändern, was an den Browser des Benutzers gesendet wird. Schließlich wird der neue Stream-Klasse, die Eigenschaft "Response.Filter" auf der Seite zugewiesen\_Load-Ereignis, und dabei den Mechanismus zum Ändern der Inhalt der Seite bereitstellt.

[&#9654;Sehen Sie sich Video (13 Minuten)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
