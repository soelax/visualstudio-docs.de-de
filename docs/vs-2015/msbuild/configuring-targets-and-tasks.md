---
title: Konfigurieren von Zielen und Aufgaben | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 9aabe67a-1720-4bbf-80d3-822b3ccf75c0
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9d3ed6456ecf4ca226368338078247a10d80cee3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196599"
---
# <a name="configuring-targets-and-tasks"></a>Konfigurieren von Zielen und Aufgaben
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Sie können MSBuild-Ziele und -Aufgaben so konfigurieren, dass sie prozessextern mit MSBuild ausgeführt werden, damit Sie auf Kontexte abzielen können, die sich von dem unterscheiden, in dem Sie die Ausführung eigentlich vorgesehen haben. Beispielsweise können Sie auf eine 32-Bit-.NET Framework 2.0-Anwendung abzielen, während der Entwicklungscomputer auf einem 64-Bit-.NET Framework 4.5-Betriebssystem ausgeführt wird. Sie können auch auf Computer abzielen die mit .NET Framework 4 oder früher ausgeführt werden. Die Kombination der 32- oder 64-Bitanzahl und der spezifischen .NET Framework-Version wird als der *Zielkontext* bezeichnet.  
  
## <a name="installation"></a>Installation  
 .NET Framework 4.5 und 4.5.1 ersetzen die Common Language Runtime (CLR) und die Ziele, Aufgaben und Tools von .NET Framework 4 , ohne sie umzubenennen. .NET Framework 4.5.1 wird zusammen mit [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] installiert.  
  
 Wenn Sie MSBuild von Visual Studio getrennt installieren möchten, sollten Sie das Installationspaket von der [MSBuild-Downloadsite](http://go.microsoft.com/fwlink/?LinkId=309745) herunterladen. Sie müssen außerdem die .NET Framework-Versionen installieren, die Sie zusätzlich verwenden möchten.  
  
## <a name="targets-and-tasks"></a>Ziele und Aufgaben  
 MSBuild führt bestimmte Buildaufgaben prozessextern aus, um auf mehr Kontexte abzuzielen.  Beispielsweise kann ein 32-Bit-MSBuild eine Buildaufgabe in einem 64-Bit-Prozess ausführen, um auf einen 64-Bit-Computer abzuzielen. Dies wird durch `UsingTask`-Argumente und `Task`-Parameter gesteuert. Die Ziele, die von .NET Framework 4.5 installiert werden, legen diese Argumente und Parameter fest, und es sind keine Änderungen erforderlich, um Anwendungen für die verschiedenen Zielkontexte zu erstellen.  
  
 Wenn Sie eigene Zielkontext erstellen möchten, müssen Sie diese Argumente und Parameter entsprechend festlegen. In der .NET Framework 4.5-Datei "Microsoft.Common.targets" und in der Datei "Microsoft.Common.Tasks" finden Sie einige Beispiele.  Informationen dazu, wie Sie eine benutzerdefinierte Aufgabe erstellen, die mehrere Zielkontexte verwenden kann, oder wie vorhandene Aufgaben geändert werden, finden Sie unter [Vorgehensweise: Konfigurieren von Zielen und Aufgaben](../msbuild/how-to-configure-targets-and-tasks.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Zielversionen](../msbuild/msbuild-multitargeting-overview.md)
