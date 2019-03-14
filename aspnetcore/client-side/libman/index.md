---
title: Clientseitiger Bibliothekserwerb in ASP.NET Core mit LibMan
author: scottaddie
description: 'Erfahren Sie, wie Sie clientseitige Bibliotheksobjekte in einem ASP.NET Core-Projekt über den Bibliotheks-Manager (LibMan) installieren.'
ms.author: scaddie
ms.custom: mvc
ms.date: 08/14/2018
uid: client-side/libman/index
---
# <a name="client-side-library-acquisition-in-aspnet-core-with-libman"></a>Clientseitiger Bibliothekserwerb in ASP.NET Core mit LibMan

Von [Scott Addie](https://twitter.com/Scott_Addie)

Der Bibliotheks-Manager (LibMan) ist ein einfaches, clientseitiges Tool zum Bibliothekserwerb. LibMan lädt beliebte Bibliotheken und Frameworks vom Dateisystem oder von einem [Content Delivery Network (CDN)](https://wikipedia.org/wiki/Content_delivery_network) herunter. Die unterstützten CDNs sind z.B. [CDNJS](https://cdnjs.com/) und [unpkg](https://unpkg.com/#/). Die ausgewählten Bibliotheksdateien werden abgerufen und an der entsprechenden Position innerhalb des ASP.NET Core-Projekts platziert.

## <a name="libman-use-cases"></a>LibMan-Einsatzbeispiele

LibMan bietet folgende Vorteile:

* Es werden nur die Bibliotheksdateien herunterladen, die Sie benötigten.
* Zusätzliche Tools, wie etwa [Node.js](https://nodejs.org), [npm](https://www.npmjs.com) und [WebPack](https://webpack.js.org), sind nicht nötig, um eine Teilmenge von Dateien in einer Bibliothek abzurufen.
* Dateien können an einer bestimmten Position platziert werden, ohne dass auf Buildaufgaben oder auf das manuelle Kopieren von Dateien zurückgegriffen werden muss.

Weitere Informationen über LibMans Vorteile sehen Sie sich [moderne Front-End-Web-Entwicklung in Visual Studio 2017: LibMan Segment](https://channel9.msdn.com/Events/Build/2017/B8073#time=43m34s).

LibMan ist kein Paketverwaltungssystem. Wenn Sie bereits einen Paket-Manager wie npm oder [yarn](https://yarnpkg.com) verwenden, tun Sie das auch weiterhin. LibMan wurde nicht dazu entwickelt, diese Tools zu ersetzen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* <xref:client-side/libman/libman-vs>
* <xref:client-side/libman/libman-cli>
* [GitHub-Repository für LibMan](https://github.com/aspnet/LibraryManager)
