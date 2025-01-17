---
title: Verwalten von Projekt- und Projektmappeneigenschaften | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: d727efc0-1096-4ede-84b6-31a65da22ac0
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: dc27bd0cb93ab142d2a82758c72b27d14032d04e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674979"
---
# <a name="managing-project-and-solution-properties"></a>Verwalten von Projekt- und Projektmappeneigenschaften
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Projekte haben Eigenschaften, die viele Aspekte der Kompilierung, des Debuggens, des Testens und des Bereitstellens steuern. Einige Eigenschaften gibt es für alle Projekttypen, und einige gelten nur für bestimmte Sprachen oder Plattformen. Sie erhalten Zugriff auf die Projekteigenschaften, indem Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Projektknoten klicken und „Eigenschaften“ auswählen, oder indem Sie Eigenschaften in das **Schnellstart**-Suchfeld in der Menüleiste eingeben.  
  
 ![Projekt-Kontextmenü](../ide/media/vs2015-proj-prop-menu.gif "vs2015_proj_prop_menu")  
  
 .NET-Projekte haben außerdem einen Eigenschaftenknoten in der Projektstruktur selbst.  
  
 ![Knoten „Eigenschaften“ in der Struktur des Projektmappen-Explorers](../ide/media/vs2015-props-se.png "VS2015_Props_SE")  
  
> [!TIP]
> Projektmappen haben einige Eigenschaften, ebenso wie Projektelemente. Auf diese Eigenschaften wird im [Eigenschaftenfenster](../ide/reference/properties-window.md), nicht im **Projekt-Designer**, zugegriffen.  
  
## <a name="project-properties"></a>Projekteigenschaften  
 Projekteigenschaften sind in Gruppen organisiert, und jede Gruppe hat ihre eigene Eigenschaftenseite. Dabei können die Seiten für unterschiedliche Sprachen und Projekttypen unterschiedlich sein.  
  
### <a name="c-and-visual-basic-projects"></a>C#- und Visual Basic-Projekte  
 In C#- und Visual Basic-Projekten sind Eigenschaften im **Projekt-Designer** verfügbar. Die folgende Abbildung zeigt die Eigenschaftsseite „Build“ für ein WPF-Projekt in C#:  
  
 ![Visual Studio-Projekt-Designer](../ide/media/vs2015-proppage-build.png "VS2015_PropPage_Build")  
  
 Informationen zu den einzelnen Eigenschaftsseiten im Projekt-Designer finden Sie unter [Projekteigenschaftenreferenz](../ide/reference/project-properties-reference.md).  
  
### <a name="c-and-javascript-projects"></a>C++- und JavaScript-Projekte  
 C++- und JavaScript-Projekte haben eine andere Benutzeroberfläche zum Verwalten von Projekteigenschaften. Die folgende Abbildung zeigt eine Eigenschaftenseite für ein C++-Projekt (JavaScript-Seiten sind ähnlich):  
  
 ![Visual C&#43;&#43;-Projekteigenschaften](../ide/media/vs2015-projprops-cpp.png "VS2015_ProjProps_cpp")  
  
 Informationen zu C++-Projekteigenschaften finden Sie unter [Arbeiten mit Projekteigenschaften](https://msdn.microsoft.com/library/9b0d6f8b-7d4e-4e61-aa75-7d14944816cd). Weitere Informationen zu JavaScript-Eigenschaften finden Sie unter [Eigenschaftenseiten, JavaScript](../ide/reference/property-pages-javascript.md).  
  
## <a name="solution-properties"></a>Projektmappeneigenschaften  
 Um auf Eigenschaften für die Projektmappe zuzugreifen, klicken Sie mit der rechten Maustaste auf den Projektmappenknoten im **Projektmappen-Explorer** und wählen **Eigenschaften** aus. In dem Dialogfeld können Sie Projektkonfigurationen für Debug- oder Releasebuilds festlegen. Sie können auswählen, welche Projekte beim Drücken von F5 als Startprojekt verwendet werden sollen, und Sie können Codeanalyseoptionen festlegen.  
  
## <a name="see-also"></a>Siehe auch  
 [Projektmappen und Projekte in Visual Studio](../ide/solutions-and-projects-in-visual-studio.md)
