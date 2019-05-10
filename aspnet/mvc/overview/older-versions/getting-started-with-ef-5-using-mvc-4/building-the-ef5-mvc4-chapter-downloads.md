---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: Im Kapitel über das Erstellen von Downloads für die EF 5 MVC 4-Tutorials | Microsoft-Dokumentation
author: Rick-Anderson
description: Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET MVC 4-Anwendungen, die mit dem Entity Framework 5 Code First "und" Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 1138f1512690e01a09c73623c0d8db4a31eb921b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129845"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>Im Kapitel über das Erstellen von Downloads für die EF 5 MVC 4-Lernprogramme

durch [Rick Anderson]((https://twitter.com/RickAndMSFT))

[Abgeschlossenes Projekt herunterladen](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Die Contoso University-Beispielwebanwendung veranschaulicht, wie ASP.NET MVC 4-Anwendungen, die mit dem Entity Framework 5 Code First "und" Visual Studio 2012. Informationen zu dieser Tutorialreihe finden Sie im [ersten Tutorial der Reihe](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

## <a name="building-the-chapter-downloads"></a>Durchführen von Downloads der einzelnen Kapitel

1. Herunterladen Sie und Entpacken Sie die Projekt-Beispiel-Zip-Datei. In den entzippten Downloadpaket finden Sie zusätzliche Zip-Dateien, eine für den Abschluss der einzelnen Kapitel.
2. Klicken Sie mit der rechten Maustaste auf die gewünschte Zip-Datei, klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Unblock** Schaltfläche.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. Entzippen Sie die Datei aus.
4. Doppelklicken Sie auf die *CUx.sln* Datei zum Starten von Visual Studio.
5. Aus der **Tools** Menü klicken Sie auf **NuGet Paket-Manager**, dann **Paket-Manager Konsole**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. In der Paket-Manager-Konsole (PMC), klicken Sie auf **wiederherstellen**.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Beenden Sie Visual Studio.
8. Visual Studio neu starten, die Projektmappe öffnen Sie im vorherigen Schritt geschlossen.
9. In der Paket-Manager-Konsole (PMC), geben Sie die `Update-Database` Befehl:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > Wenn Sie den folgenden Fehler erhalten:  
    >   
    >  *Der Begriff "Update-Database" wird nicht als Namen für ein Cmdlet, Funktion, Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder wenn ein Pfad enthalten ist, stellen Sie sicher, dass der Pfad richtig ist, und versuchen Sie es erneut.*  
    > Beenden und starten Sie Visual Studio neu.

    Jede Migration wird ausgeführt, und klicken Sie dann die Seed-Methode wird ausgeführt. Sie können nun die app ausführen.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [Vorherige](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
