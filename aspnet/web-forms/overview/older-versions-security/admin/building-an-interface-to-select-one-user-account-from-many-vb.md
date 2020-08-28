---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: Aufbauen einer Schnittstelle zum Auswählen eines Benutzerkontos aus vielen (VB) | Microsoft-Dokumentation
author: rick-anderson
description: In diesem Tutorial erstellen wir eine Benutzeroberfläche mit einem auslagerbaren, filterbaren Raster. Die Benutzeroberfläche besteht vor allem aus einer Reihe von LinkButtons für...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044583"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>Erstellen eine Schnittstelle zum Auswählen eines Benutzerkontos aus vielen (VB)

von [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Code herunterladen](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) oder [PDF herunterladen](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> In diesem Tutorial erstellen wir eine Benutzeroberfläche mit einem auslagerbaren, filterbaren Raster. Die Benutzeroberfläche besteht vor allem aus einer Reihe von LinkButtons zum Filtern der Ergebnisse basierend auf dem Anfangsbuchstaben des Benutzernamens und einem GridView-Steuerelement, das die entsprechenden Benutzer anzeigt. Wir beginnen mit der Auflistung aller Benutzerkonten in einer GridView. Fügen Sie dann in Schritt 3 die filterlink Buttons hinzu. Schritt 4 prüft das Paging der gefilterten Ergebnisse. Die in den Schritten 2 bis 4 erstellte Schnittstelle wird in den nachfolgenden Tutorials zum Ausführen administrativer Aufgaben für ein bestimmtes Benutzerkonto verwendet.

## <a name="introduction"></a>Einführung

Im Tutorial <a id="_msoanchor_1"></a> [*Zuweisen von Rollen zu Benutzern*](../roles/assigning-roles-to-users-vb.md) haben wir eine rudimentäre Oberfläche für einen Administrator erstellt, um einen Benutzer auszuwählen und seine Rollen zu verwalten. Insbesondere hat die Schnittstelle dem Administrator eine Dropdown Liste aller Benutzer angezeigt. Eine solche Schnittstelle eignet sich, wenn es sich um ein Dutzend Benutzerkonten handelt, die jedoch für Websites mit Hunderten oder Tausenden von Konten unhandlich ist. Ein auslagerbares, filterbares Raster ist eine geeignetere Benutzeroberfläche für Websites mit großen Benutzer Basen.

In diesem Tutorial erstellen wir eine solche Benutzeroberfläche. Die Benutzeroberfläche besteht vor allem aus einer Reihe von LinkButtons zum Filtern der Ergebnisse basierend auf dem Anfangsbuchstaben des Benutzernamens und einem GridView-Steuerelement, das die entsprechenden Benutzer anzeigt. Wir beginnen mit der Auflistung aller Benutzerkonten in einer GridView. Fügen Sie dann in Schritt 3 die filterlink Buttons hinzu. Schritt 4 prüft das Paging der gefilterten Ergebnisse. Die in den Schritten 2 bis 4 erstellte Schnittstelle wird in den nachfolgenden Tutorials zum Ausführen administrativer Aufgaben für ein bestimmtes Benutzerkonto verwendet.

Legen Sie direkt los.

## <a name="step-1-adding-new-aspnet-pages"></a>Schritt 1: Hinzufügen neuer ASP.NET Seiten

In diesem Tutorial und den nächsten beiden werden verschiedene Funktionen und Funktionen für die Verwaltung untersucht. Wir benötigen eine Reihe von ASP.NET-Seiten, um die in diesen Tutorials untersuchten Themen zu implementieren. Erstellen Sie diese Seiten, und aktualisieren Sie die Site Übersicht.

Beginnen Sie mit dem Erstellen eines neuen Ordners in dem Projekt mit dem Namen `Administration` . Fügen Sie als nächstes zwei neue ASP.NET-Seiten zum Ordner hinzu, wobei jede Seite mit der `Site.master` Master Seite verknüpft wird. Benennen Sie die Seiten:

- `ManageUsers.aspx`
- `UserInformation.aspx`

Fügen Sie auch zwei Seiten zum Stammverzeichnis der Website hinzu: `ChangePassword.aspx` und `RecoverPassword.aspx` .

Diese vier Seiten sollten zu diesem Zeitpunkt über zwei Inhalts Steuerelemente verfügen, eine für jeden der Inhalts Platzhalter der Master Seite: `MainContent` und `LoginContent` .

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

Wir möchten das Standard Markup der Master Seite für den `LoginContent` contentplachalter für diese Seiten anzeigen. Entfernen Sie daher das deklarative Markup für das `Content2` Inhalts Steuerelement. Danach sollte das Markup der Seite nur ein Inhalts Steuerelement enthalten.

Die ASP.NET-Seiten im `Administration` Ordner sind ausschließlich für Administratoren vorgesehen. Wir haben dem System im Tutorial zum <a id="_msoanchor_2"></a> [*Erstellen und Verwalten von Rollen*](../roles/creating-and-managing-roles-vb.md) eine Administrator Rolle hinzugefügt. schränken Sie den Zugriff auf diese beiden Seiten auf diese Rolle ein. Fügen Sie hierzu dem Ordner eine Datei hinzu, und konfigurieren Sie das zugehörige- `Web.config` `Administration` `<authorization>` Element, um Benutzer in der Administrator Rolle zuzulassen und alle anderen abzulehnen.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

An diesem Punkt sollte die Projektmappen-Explorer des Projekts ähnlich wie der Screenshot in Abbildung 1 aussehen.

[![Vier neue Seiten und eine Web.config Datei wurden der Website hinzugefügt.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**Abbildung 1**: vier neue Seiten und eine `Web.config` Datei wurden der Website hinzugefügt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))

Aktualisieren Sie abschließend die Site Map ( `Web.sitemap` ), um einen Eintrag auf der `ManageUsers.aspx` Seite einzuschließen. Fügen Sie den folgenden XML-Code nach dem hinzu, den Sie `<siteMapNode>` für die Lernprogramme für Rollen

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

Wenn die Site Übersicht aktualisiert wurde, besuchen Sie die Website über einen Browser. Wie in Abbildung 2 gezeigt, enthält die Navigation auf der linken Seite nun Elemente für die Verwaltungs Lernprogramme.

[![Die Site Übersicht enthält einen Knoten mit dem Namen "Benutzerverwaltung".](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**Abbildung 2**: die Site Übersicht enthält einen Knoten mit dem Namen "Benutzerverwaltung" ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>Schritt 2: Auflisten aller Benutzerkonten in einer GridView

Unser Ziel dieses Tutorials ist es, ein auslagerbares, filterbares Raster zu erstellen, über das ein Administrator ein zu verwaltende Benutzerkonto auswählen kann. Beginnen wir, indem wir *alle* Benutzer in einer GridView auflisten. Nach Abschluss dieses Vorgangs fügen wir die Filter-und Paginierungs Schnittstellen und-Funktionen hinzu.

Öffnen `ManageUsers.aspx` Sie die Seite im `Administration` Ordner, und fügen Sie eine GridView hinzu `ID` . Wenn Sie auf einen Moment festlegen, `UserAccounts` schreiben wir Code, um die Gruppe von Benutzerkonten mithilfe der `Membership` -Methode der-Klasse an die GridView zu binden `GetAllUsers` . Wie in den vorherigen Tutorials erläutert, `GetAllUsers` gibt die-Methode ein- `MembershipUserCollection` Objekt zurück, das eine Auflistung von- `MembershipUser` Objekten ist. Jede `MembershipUser` in der Auflistung enthält Eigenschaften wie `UserName` , `Email` , `IsApproved` usw.

Um die gewünschten Benutzerkontoinformationen in der GridView anzuzeigen, legen Sie die-Eigenschaft von GridView auf false fest, und `AutoGenerateColumns` fügen Sie boundfields für die `UserName` Eigenschaften, und für die Eigenschaften, und hinzu `Email` `Comment` `IsApproved` `IsLockedOut` `IsOnline` . Diese Konfiguration kann über das deklarative Markup des Steuer Elements oder über das Dialogfeld "Felder" angewendet werden. Abbildung 3 zeigt einen Screenshot des Dialog Felds Felder, nachdem das Kontrollkästchen Felder automatisch generieren deaktiviert wurde und boundfields und checkboxfields hinzugefügt und konfiguriert wurden.

[![Fügen Sie drei boundfields und drei checkboxfields zur GridView hinzu.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**Abbildung 3**: Hinzufügen von drei boundfields und drei checkboxfields zur GridView ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))

Stellen Sie nach dem Konfigurieren von GridView sicher, dass sein deklaratives Markup dem folgenden ähnelt:

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

Als nächstes müssen wir Code schreiben, der die Benutzerkonten an die GridView bindet. Erstellen Sie eine Methode `BindUserAccounts` mit dem Namen, um diese Aufgabe auszuführen, und rufen Sie Sie dann `Page_Load` beim ersten Besuchen der Seite über den-Ereignishandler auf.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

Nehmen Sie sich einen Moment Zeit, um die Seite über einen Browser zu testen. Wie in Abbildung 4 gezeigt, `UserAccounts` Listet die GridView den Benutzernamen, die e-Mail-Adresse und andere relevante Kontoinformationen für alle Benutzer im System auf.

[![Die Benutzerkonten werden in der GridView aufgeführt.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**Abbildung 4**: die Benutzerkonten werden in der GridView aufgelistet ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>Schritt 3: Filtern der Ergebnisse nach dem ersten Buchstaben des Benutzernamens

Derzeit werden `UserAccounts` in der GridView *alle* Benutzerkonten angezeigt. Bei Websites mit Hunderten oder Tausenden von Benutzerkonten ist es zwingend erforderlich, dass der Benutzer in der Lage ist, schnell auf die angezeigten Konten zu pdern. Dies können Sie erreichen, indem Sie der Seite filterlink Buttons hinzufügen. Fügen Sie der Seite 27 Link Buttons hinzu: eine mit dem Titel all und einen Link Button für jeden Buchstaben des Alphabets. Wenn ein Besucher auf die linktaste alle klickt, werden in der GridView alle Benutzer angezeigt. Wenn Sie auf einen bestimmten Buchstaben klicken, werden nur die Benutzer angezeigt, deren Benutzername mit dem ausgewählten Buchstaben beginnt.

Unsere erste Aufgabe besteht darin, die 27 LinkButton-Steuerelemente hinzuzufügen. Eine Möglichkeit besteht darin, die 27 Link Buttons deklarativ einzeln zu erstellen. Ein flexiblerer Ansatz ist die Verwendung eines Repeater-Steuer Elements mit einem `ItemTemplate` , das eine LinkButton-Methode rendert und dann die Filteroptionen als-Array an den Repeater bindet `String` .

Beginnen Sie, indem Sie der Seite oberhalb der GridView ein Wiederholungs Steuerelement hinzufügen `UserAccounts` . Legen Sie die-Eigenschaft des Wiederholungs Moduls `ID` so fest, `FilteringUI` dass die Vorlagen des Wiederholungs Moduls so konfiguriert werden, dass `ItemTemplate` ein Link Button rendert, dessen-Eigenschaft und-Eigenschaft `Text` `CommandName` an das aktuelle Array Element gebunden sind Wie im <a id="_msoanchor_3"></a> Tutorial [*Zuweisen von Rollen zu Benutzern*](../roles/assigning-roles-to-users-vb.md) erläutert, kann dies mithilfe der `Container.DataItem` Datenbindung-Syntax erreicht werden. Verwenden Sie die Repeater `SeparatorTemplate` , um eine vertikale Linie zwischen den einzelnen Links anzuzeigen.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

Um dieses Repeater mit den gewünschten Filteroptionen aufzufüllen, erstellen Sie eine Methode mit dem Namen `BindFilteringUI` . Stellen Sie sicher, dass diese Methode beim `Page_Load` ersten Laden der Seite vom-Ereignishandler aufgerufen wird.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

Diese Methode gibt die Filteroptionen als Elemente im `String` array `filterOptions` für jedes Element im Array an. der Repeater gerencht einen LinkButton, dessen `Text` -Eigenschaft und-Eigenschaft `CommandName` dem Wert des-Array Elements zugewiesen sind.

Abbildung 5 zeigt die `ManageUsers.aspx` Seite, wenn Sie in einem Browser angezeigt wird.

[![Der Repeater listet 27 Link Schaltflächen auf.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**Abbildung 5**: der Repeater listet 27 filterlink Buttons auf ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))

> [!NOTE]
> Benutzernamen können mit jedem beliebigen Zeichen beginnen, einschließlich Ziffern und Interpunktions Zeichen. Um diese Konten anzuzeigen, muss der Administrator die Option Alle LinkButton verwenden. Sie können auch einen Link Button hinzufügen, um alle Benutzerkonten zurückzugeben, die mit einer Zahl beginnen. Ich lasse dies als Übung für den Reader aus.

Das Klicken auf eine der filterlink Schaltflächen führt zu einem Postback und löst das Ereignis des Wiederholungs Moduls `ItemCommand` aus, aber es gibt keine Änderung im Raster, da wir noch Code schreiben müssen, um die Ergebnisse zu filtern. Die- `Membership` Klasse enthält eine [ `FindUsersByName` Methode](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) , die die Benutzerkonten zurückgibt, deren Benutzername mit einem angegebenen Suchmuster übereinstimmt. Mit dieser Methode können Sie nur die Benutzerkonten abrufen, deren Benutzernamen mit dem Buchstaben beginnen, der durch die `CommandName` des gefilterten Link Schaltflächen, auf die geklickt wurde, festgelegt wurde.

Aktualisieren Sie zunächst die `ManageUser.aspx` Code Behind-Klasse der Seite, sodass Sie eine Eigenschaft mit dem Namen enthält, `UsernameToMatch` die die Benutzernamen-Filter Zeichenfolge über Postbacks hinweg beibehält:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

Die- `UsernameToMatch` Eigenschaft speichert Ihren Wert, der ihr zugewiesen ist, `ViewState` mithilfe des Schlüssels "UsernameToMatch" in der Auflistung. Wenn der Wert dieser Eigenschaft gelesen wird, wird überprüft, ob ein Wert in der Auflistung vorhanden ist `ViewState` . andernfalls wird der Standardwert (eine leere Zeichenfolge) zurückgegeben. Die- `UsernameToMatch` Eigenschaft stellt ein gängiges Muster dar, d. r. einen Wert, der den Ansichts Zustand fortsetzt, sodass alle Änderungen an der Eigenschaft über Postbacks hinweg beibehalten werden. Weitere Informationen zu diesem Muster finden Sie unter [Understanding ASP.net View State](https://msdn.microsoftn-us/library/ms972976.aspx).

Aktualisieren Sie anschließend die- `BindUserAccounts` Methode, sodass anstelle von aufgerufen `Membership.GetAllUsers` wird. `Membership.FindUsersByName` übergeben Sie dabei den Wert der- `UsernameToMatch` Eigenschaft, die mit dem SQL-Platzhalter Zeichen "%" angehängt ist.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

Wenn nur die Benutzer angezeigt werden sollen, deren Benutzername mit dem Buchstaben a beginnt, legen Sie die `UsernameToMatch` -Eigenschaft auf fest, und rufen Sie dann auf `BindUserAccounts` , um einen Aufruf von zu `Membership.FindUsersByName("A%")` erhalten, der alle Benutzer zurückgibt, deren Benutzername mit einem beginnt. entsprechend, um *alle* Benutzer zurückzugeben, weisen Sie der-Eigenschaft eine leere Zeichenfolge zu `UsernameToMatch` `BindUserAccounts` `Membership.FindUsersByName("%")` .

Erstellen Sie einen Ereignishandler für das-Ereignis des Wiederholungs Moduls `ItemCommand` . Dieses Ereignis wird immer dann ausgelöst, wenn auf eine der filterlink Buttons geklickt wird. der Wert wird durch das- `CommandName` Objekt übermittelt `RepeaterCommandEventArgs` . Wir müssen der Eigenschaft den entsprechenden Wert zuweisen `UsernameToMatch` und dann die-Methode aufzurufen `BindUserAccounts` . Wenn `CommandName` alle ist, weisen Sie eine leere Zeichenfolge zu, `UsernameToMatch` damit alle Benutzerkonten angezeigt werden. Weisen Sie andernfalls den `CommandName` Wert zu. `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

Testen Sie mit diesem Code die Filter Funktionalität. Beim ersten Besuch der Seite werden alle Benutzerkonten angezeigt (siehe Abbildung 5). Wenn Sie auf eine Linkschaltfläche klicken, wird ein Postback ausgelöst und die Ergebnisse gefiltert, sodass nur die Benutzerkonten angezeigt werden, die mit beginnen.

[![Mithilfe der Schaltflächen zum Filtern von Links können Sie die Benutzer anzeigen, deren Benutzername mit einem bestimmten Buchstaben beginnt](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**Abbildung 6**: Verwenden der Link Schaltflächen zum Filtern, um die Benutzer anzuzeigen, deren Benutzername mit einem bestimmten Buchstaben beginnt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))

## <a name="step-4-updating-the-gridview-to-use-paging"></a>Schritt 4: Aktualisieren von GridView für die Verwendung von Paging

Die in Abbildung 5 und 6 dargestellte GridView listet alle Datensätze auf, die von der-Methode zurückgegeben werden `FindUsersByName` . Wenn hundert oder Tausende von Benutzerkonten vorhanden sind, kann dies zu Informations Überladungen führen, wenn alle Konten angezeigt werden (wie bei einem Klick auf die Schaltfläche "alle" oder beim ersten Besuch der Seite). Wenn Sie die Benutzerkonten in besser verwaltbaren Blöcken präsentieren möchten, konfigurieren Sie die GridView so, dass 10 Benutzerkonten gleichzeitig angezeigt werden.

Das GridView-Steuerelement bietet zwei Arten von Paging:

- **Standard-Paging** : leicht zu implementieren, aber ineffizient. Kurz gesagt: beim Paging mit Standardwert erwartet die GridView *alle* Datensätze aus der Datenquelle. Anschließend wird nur die entsprechende Seite der Datensätze angezeigt.
- **Benutzerdefiniertes Paging** : erfordert mehr Aufwand für die Implementierung, ist jedoch effizienter als das standardmäßige Paging, da die Datenquelle bei benutzerdefiniertem Paging nur die genaue Gruppe von Datensätzen zurückgibt, die angezeigt werden.

Der Leistungsunterschied zwischen Standard-und benutzerdefiniertem Paging kann beim Paging durch Tausende von Datensätzen beträchtlich sein. Da wir diese Schnittstelle aufbauen, weil es möglicherweise Hunderte oder Tausende von Benutzerkonten gibt, verwenden wir das benutzerdefinierte Paging.

> [!NOTE]
> Eine ausführlichere Erläuterung der Unterschiede zwischen dem standardmäßigen und dem benutzerdefinierten Paging sowie den Herausforderungen bei der Implementierung von benutzerdefiniertem Paging finden Sie unter [effizientes Paging durch große Datenmengen](https://asp.net/learn/data-access/tutorial-25-vb.aspx). Eine Analyse der Leistungsunterschiede zwischen Standard-und benutzerdefiniertem Paging finden Sie unter [benutzerdefiniertes Paging in ASP.net mit SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx).

Zum Implementieren von benutzerdefiniertem Paging benötigen wir zuerst einen Mechanismus, mit dem die genaue Teilmenge der Datensätze abgerufen wird, die von der GridView angezeigt werden. Die gute Nachricht ist, dass die `Membership` - `FindUsersByName` Methode der Klasse über eine Überladung verfügt, die es uns ermöglicht, den Seitenindex und die Seitengröße anzugeben, und nur die Benutzerkonten zurückgibt, die in diesen Datenbereich fallen.

Diese Überladung weist insbesondere die folgende Signatur auf: [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) .

Der *pagumdex* -Parameter gibt die Seite der zurück zugebende Benutzerkonten an. *PageSize* gibt an, wie viele Datensätze pro Seite angezeigt werden. Der *totalRecords* -Parameter ist ein `ByRef` Parameter, der die Gesamtzahl der Benutzerkonten im Benutzerspeicher zurückgibt.

> [!NOTE]
> Die von zurückgegebenen Daten `FindUsersByName` werden nach Benutzername sortiert. die Sortierkriterien können nicht angepasst werden.

Die GridView kann für die Verwendung von benutzerdefiniertem Paging konfiguriert werden, jedoch nur, wenn Sie an ein ObjectDataSource-Steuerelement gebunden ist. Damit das ObjectDataSource-Steuerelement benutzerdefiniertes Paging implementieren kann, sind zwei Methoden erforderlich: eine, die einen Start Zeilen Index und die maximale Anzahl der anzuzeigenden Datensätze übergeben wird, und gibt die genaue Teilmenge der Datensätze zurück, die innerhalb dieser Spanne liegen. und eine Methode, die die Gesamtanzahl der Datensätze zurückgibt, die durchlaufen werden. Die `FindUsersByName` Überladung akzeptiert einen Seitenindex und eine Seitengröße und gibt die Gesamtanzahl der Datensätze über einen `ByRef` Parameter zurück. Es ist also ein Schnittstellen Konflikt vorhanden.

Eine Möglichkeit besteht darin, eine Proxy Klasse zu erstellen, die die Schnittstelle verfügbar macht, die von ObjectDataSource erwartet wird, und dann intern die- `FindUsersByName` Methode aufruft. Eine weitere Option, die wir für diesen Artikel verwenden, besteht darin, eine eigene Paging-Schnittstelle zu erstellen und diese anstelle der integrierten pagingschnittstelle der GridView zu verwenden.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>Erstellen einer ersten, vorherigen, nächsten, letzten pagingschnittstelle

Erstellen Sie eine pagingschnittstelle mit den Links "First", "Previous", "Next" und "Last". Wenn Sie auf die erste Schaltfläche klicken, wird der Benutzer zur ersten Seite der Daten, während die vorherige Seite zurück zur vorherigen Seite wird. Entsprechend verschiebt Next und Last den Benutzer auf die nächste und letzte Seite. Fügen Sie die vier LinkButton-Steuerelemente unterhalb der `UserAccounts` GridView hinzu.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

Erstellen Sie als nächstes einen Ereignishandler für jedes der LinkButton- `Click` Ereignisse.

Abbildung 7 zeigt die vier LinkButtons, wenn Sie über die Visual Web Developer-Designansicht angezeigt werden.

[![Hinzufügen von "First", "Previous", "Next" und "Last" unterhalb der GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**Abbildung 7**: Hinzufügen von "First", "Previous", "Next" und "Last" unterhalb der GridView ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png)

### <a name="keeping-track-of-the-current-page-index"></a>Verfolgen des aktuellen Seiten Indexes

Wenn ein Benutzer die Seite zuerst besucht `ManageUsers.aspx` oder auf eine der Filter Schaltflächen klickt, möchten wir die erste Seite der Daten in der GridView anzeigen. Wenn der Benutzer auf eine der Navigations Link Schaltflächen klickt, muss der Seitenindex jedoch aktualisiert werden. Um den Seitenindex und die Anzahl der pro Seite anzuzeigenden Datensätze beizubehalten, fügen Sie der Code Behind-Klasse der Seite die folgenden beiden Eigenschaften hinzu:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

Wie die- `UsernameToMatch` Eigenschaft behält die- `PageIndex` Eigenschaft ihren Wert im Ansichts Zustand. Die schreibgeschützte `PageSize` Eigenschaft gibt einen hart codierten Wert zurück, 10. Ich lade den interessierten Reader ein, um diese Eigenschaft für die Verwendung desselben Musters zu aktualisieren `PageIndex` , und dann die `ManageUsers.aspx` Seite so zu erweitern, dass die Person, die die Seite besucht, angeben kann, wie viele Benutzerkonten pro Seite angezeigt werden sollen.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>Abrufen der Datensätze der aktuellen Seite, Aktualisieren des Seiten Indexes und aktivieren und Deaktivieren der Link Schaltflächen der Paging-Schnittstelle

Wenn die Paging-Schnittstelle eingerichtet ist und die `PageIndex` -Eigenschaft und die-Eigenschaft `PageSize` hinzugefügt wurden, können wir die-Methode aktualisieren, `BindUserAccounts` sodass Sie die entsprechende Überladung verwendet `FindUsersByName` . Außerdem muss diese Methode die pagingschnittstelle abhängig von der angezeigten Seite aktivieren oder deaktivieren. Wenn Sie die erste Seite der Daten anzeigen, sollten die ersten und vorherigen Links deaktiviert werden. "Next" und "Last" sollten beim Anzeigen der letzten Seite deaktiviert werden.

Aktualisieren Sie die `BindUserAccounts`-Methode mit folgendem Code:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

Beachten Sie, dass die Gesamtanzahl der Datensätze, die durchlaufen werden, durch den letzten Parameter der-Methode bestimmt wird `FindUsersByName` . Nachdem die angegebene Seite der Benutzerkonten zurückgegeben wurde, werden die vier LinkButtons entweder aktiviert oder deaktiviert, je nachdem, ob die erste oder letzte Seite der Daten angezeigt wird.

Der letzte Schritt besteht darin, den Code für die vier Ereignishandler von LinkButtons zu schreiben `Click` . Diese Ereignishandler müssen die `PageIndex` -Eigenschaft aktualisieren und dann die Daten über einen aufzurufenden `BindUserAccounts` , vorherigen und nächsten Ereignishandler erneut an die GridView-Methode binden. Der `Click` Ereignishandler für den letzten Link Button ist jedoch etwas komplexer, da wir bestimmen müssen, wie viele Datensätze angezeigt werden, um den letzten Seitenindex zu bestimmen.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

In den Abbildungen 8 und 9 wird die benutzerdefinierte pagingschnittstelle in Aktion angezeigt. Abbildung 8 zeigt die `ManageUsers.aspx` Seite, wenn Sie die erste Seite mit Daten für alle Benutzerkonten anzeigen. Beachten Sie, dass nur 10 der 13 Konten angezeigt werden. Wenn Sie auf den nächsten oder letzten Link klicken, wird ein Postback ausgelöst, der `PageIndex` auf 1 aktualisiert und die zweite Seite der Benutzerkonten an das Raster gebunden (siehe Abbildung 9).

[![Die ersten 10 Benutzerkonten werden angezeigt.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**Abbildung 8**: die ersten 10 Benutzerkonten werden angezeigt ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))

[![Beim Klicken auf den nächsten Link wird die zweite Seite der Benutzerkonten angezeigt.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**Abbildung 9**: Klicken auf den nächsten Link zeigt die zweite Seite der Benutzerkonten an ([Klicken Sie, um das Bild in voller Größe anzuzeigen](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))

## <a name="summary"></a>Zusammenfassung

Administratoren müssen häufig einen Benutzer aus der Liste der Konten auswählen. In den vorherigen Tutorials haben wir uns mit einer Dropdown Liste befasst, die mit den Benutzern gefüllt ist, aber dieser Ansatz ist nicht gut skalierbar. In diesem Tutorial haben wir eine bessere Alternative untersucht: eine filterbare Schnittstelle, deren Ergebnisse in einer auslagerbaren GridView angezeigt werden. Mit dieser Benutzeroberfläche können Administratoren ein Benutzerkonto zwischen Tausenden schnell und effizient suchen und auswählen.

Fröhliche Programmierung!

### <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu den in diesem Tutorial behandelten Themen finden Sie in den folgenden Ressourcen:

- [Benutzerdefiniertes Paging in ASP.net mit SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [Effizientes Paging durch große Datenmengen](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [Ein eigenes Websiteverwaltungs-Tool](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>Zum Autor

Scott Mitchell, Autor mehrerer ASP/ASP. net-Bücher und Gründer von 4GuysFromRolla.com, hat seit 1998 mit Microsoft-Webtechnologien gearbeitet. Scott arbeitet als unabhängiger Berater, Ausbilder und Writer. Sein letztes Buch ist *[Sams Teach Yourself ASP.NET 2,0 in 24 Stunden](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Scott kann bei [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) oder über seinen Blog von erreicht werden [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>Besonders vielen Dank

Diese tutorialreihe wurde von vielen hilfreichen Reviewern geprüft. Lead Reviewer für dieses Tutorial war Alicja Maziarz. Möchten Sie meine bevorstehenden MSDN-Artikel überprüfen? Wenn dies der Fall ist, löschen Sie eine Zeile unter

> [!div class="step-by-step"]
> [Zurück](unlocking-and-approving-user-accounts-cs.md)
> [Weiter](recovering-and-changing-passwords-vb.md)
