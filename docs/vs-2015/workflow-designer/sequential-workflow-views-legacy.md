---
title: Sequenzielle Workflowansichten (Vorgängerversion) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 2018-06-30
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sequential workflow views
- sequential workflows, views
ms.assetid: 135f24b9-1b37-442b-9ef8-f0f2108a3212
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 46c37ec7f3813078b9e70076bf92e6d0e1b86453
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "47523191"
---
# <a name="sequential-workflow-views-legacy"></a>Sequenzielle Workflowansichten (Vorgängerversion)
[!INCLUDE[vs2010](../includes/vs2010-md.md)] stellt eine Vorgängerversion von [!INCLUDE[wfd1](../includes/wfd1-md.md)] bereit, die zum Abzielen auf [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] oder [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] verwendet werden kann.  
  
 [!INCLUDE[wfd2](../includes/wfd2-md.md)] bietet eine Möglichkeit, [!INCLUDE[wf](../includes/wf-md.md)]-Anwendungen mithilfe der vertrauten [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]-Benutzeroberfläche grafisch zu erstellen. [!INCLUDE[wf](../includes/wf-md.md)]-Anwendungen bestehen aus Workflowprozessschritten, den so genannten Aktivitäten. Erstellen Sie zum Erstellen eines Workflows, Aktivitäten auf der Entwurfsoberfläche durch Ziehen die jeweiligen Aktivitätsdesigner aus **Toolbox** auf die Entwurfsoberfläche.  
  
 Beim Erstellen eines sequenziellen Workflows, d.h. eine [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040), drei Ansichten des Workflows zur Verfügung. Die Sichten befinden sich über die **Workflow** Menü und im Kontextmenü auf der Entwurfsoberfläche angezeigt.  
  
 In der folgenden Tabelle werden die Namen und Beschreibungen der einzelnen Ansichten aufgeführt.  
  
|Menü-/Registerkartenoption|Beschreibung|  
|----------------------|-----------------|  
|**Sequenziellen Workflow anzeigen**|Mit der rechten Maustaste Entwurfsoberfläche, und wählen die **sequenziellen Workflow anzeigen** Option im Kontextmenü zum Anzeigen der **sequenziellen Workflow** anzuzeigen, der angezeigt wird mit die aktivitätsbasierte grafische Darstellung des sequenziellen Workflows. Oder wählen Sie **sequenziellen Workflow anzeigen** aus der **Workflow** Menü.|  
|**Abbruchhandler anzeigen**|Mit der rechten Maustaste Entwurfsoberfläche, und wählen die **Abbruchhandler anzeigen** Option im Kontextmenü zum Anzeigen der **sequenziellen Workflow** anzuzeigen, der angezeigt wird der [CancellationHandlerActivity ](http://go.microsoft.com/fwlink?LinkID=65050) mit dem Workflow zugewiesene Aktivität. Oder wählen Sie **Abbruchhandler anzeigen** aus der **Workflow** Menü.|  
|**Fehlerhandler anzeigen**|Mit der rechten Maustaste Entwurfsoberfläche, und wählen die **Fehlerhandler anzeigen** Option im Kontextmenü zum Anzeigen der **Fehler** anzuzeigen, der angezeigt wird der [FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055) die Aktivität dem Workflow zugeordnet. Oder wählen Sie **Fehlerhandler anzeigen** aus der **Workflow** Menü.|  
  
 Weitere Informationen zu ähnlichen Ansichten finden Sie unter [Aktivitätsansichten (Vorgängerversion)](../workflow-designer/activity-views-legacy.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivitätsansichten (Vorgängerversion)](../workflow-designer/activity-views-legacy.md)   
 [Erstellen von Legacyworkflowprojekten](../workflow-designer/creating-legacy-workflow-projects.md)   
 [Workflow-Erstellungsmodi](http://go.microsoft.com/fwlink?LinkID=65014)