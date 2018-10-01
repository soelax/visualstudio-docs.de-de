---
title: Schaltflächen des Eigenschaftenfensters | Microsoft-Dokumentation
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 579f0a287e171872fccebbd251fae618ba615692
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "47520320"
---
# <a name="properties-window-buttons"></a>Schaltflächen des Eigenschaftenfensters
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Die neueste Version dieses Themas finden Sie unter [Schaltflächen des Eigenschaftenfensters](https://docs.microsoft.com/visualstudio/extensibility/internals/properties-window-buttons).  
  
Abhängig von der Entwicklungssprache und Produkttyp, bestimmte Schaltflächen werden standardmäßig angezeigt werden auf der Symbolleiste für den **Eigenschaften** Fenster. In allen Fällen die **nach Kategorien**, **Alphabetized**, **Eigenschaften**, und **Eigenschaftenseiten** Schaltflächen werden angezeigt. In Visual c# und Visual Basic die **Ereignisse** Schaltfläche wird ebenfalls angezeigt. In bestimmten Visual C++-Projekten die **VC++-Nachrichten** und **VC überschreibt** Schaltflächen werden angezeigt. Zusätzliche Schaltflächen möglicherweise für andere Projekttypen angezeigt. Weitere Informationen zu Schaltflächen in der **Eigenschaften** Fenster finden Sie unter [Fenster "Eigenschaften"](../../ide/reference/properties-window.md).  
  
## <a name="implementation-of-properties-window-buttons"></a>Implementierung der Schaltflächen des Eigenschaftenfensters  
 Beim Klicken auf die **nach Kategorien** Schaltfläche Visual Studio ruft die <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> Schnittstelle für das Objekt mit dem Fokus auf dessen Eigenschaften nach Kategorie zu sortieren. <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> wird implementiert, auf die `IDispatch` -Objekt, das angezeigt wird der **Eigenschaften** Fenster.  
  
 Es gibt 11 vordefinierte Eigenschaft-Kategorien, die negative Werte haben. Sie können benutzerdefinierte Kategorien definieren, aber es wird empfohlen, dass Sie diese positive Werte, die sie die vordefinierten Kategorien zu unterscheiden zuweisen.  
  
 Die <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> Methode gibt den entsprechenden Wert der Eigenschaftenkategorie für die angegebene Eigenschaft zurück. Die <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> Methode gibt eine Zeichenfolge, die den Kategorienamen enthält. Sie müssen nur Werte der benutzerdefinierten Kategorie unterstützen, da Visual Studio, die Kategoriewerte Standardeigenschaft weiß.  
  
 Beim Klicken auf die **Alphabetized** Schaltfläche, die Eigenschaften werden in alphabetischer Reihenfolge anhand des Namens angezeigt. Die Namen werden abgerufen, indem `IDispatch` entsprechend einen lokalisierten Sortieralgorithmus.  
  
 Wenn die **Eigenschaften** Fenster wird geöffnet, die **Eigenschaften** Schaltfläche wird automatisch angezeigt. ausgewählt. In anderen Teilen der Umgebung, die gleiche Schaltfläche wird angezeigt, und klicken Sie darauf, zeigen die **Eigenschaften** Fenster.  
  
 Die **Eigenschaftenseiten** Schaltfläche ist nur verfügbar wenn `ISpecifyPropertyPages` ist für das ausgewählte Objekt nicht implementiert. Eigenschaftenseiten Anzeige konfigurationsabhängigen Eigenschaften, die in der Regel von Projektmappen und Projekten zugeordnet sind, aber sie kann auch werden Projektelemente (z. B. in Visual C++) zugeordnet.  
  
> [!NOTE]
>  Sie können keine Symbolleisten-Schaltflächen zum Hinzufügen der **Eigenschaften** mithilfe von nicht verwaltetem Code. Um eine Symbolleisten-Schaltfläche hinzuzufügen, müssen Sie ein verwaltetes Objekt, das von abgeleitet ist erstellen <xref:System.Windows.Forms.Design.PropertyTab>.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern von Eigenschaften](../../extensibility/internals/extending-properties.md)
