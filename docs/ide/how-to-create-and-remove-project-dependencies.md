---
title: 'Vorgehensweise: Erstellen und Entfernen von Projektabhängigkeiten'
ms.date: 06/21/2017
ms.topic: conceptual
f1_keywords:
- VS.ProjectDependenciesDlg
helpviewer_keywords:
- vs.build.projectdependencies
- project dependencies
- builds [Visual Studio], setting up
- project build configurations, dependencies
- dependencies, project
- projects [Visual Studio], dependencies
ms.assetid: e2a0a8ff-dae7-40a8-b774-b88aa5235183
ms.technology: vs-ide-compile
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce26c74aced2dd979f9f9847d5c56ead30f897ce
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415582"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>Vorgehensweise: Erstellen und Entfernen von Projektabhängigkeiten

Beim Erstellen einer Projektmappe, die mehrere Projekte enthält, kann es erforderlich sein, bestimmte Projekte zuerst zu erstellen, um Code zu generieren, der von anderen Projekten verwendet wird. Wenn ein Projekt ausführbaren Code verarbeitet, der von einem anderen Projekt generiert wurde, wird auf das generierende Projekt als Projektabhängigkeit des verarbeitenden Projekts verwiesen. Solche Abhängigkeitsbeziehungen können im Dialogfeld **Projektabhängigkeiten** definiert werden.

## <a name="to-assign-dependencies-to-projects"></a>So weisen Sie Projekten Abhängigkeiten zu

1. Wählen Sie im **Projektmappen-Explorer** ein Projekt aus.

2. Klicken Sie im Menü **Projekt** auf **Projektabhängigkeiten**.

    Das Dialogfeld **Projektabhängigkeiten** wird geöffnet.

   > [!NOTE]
   > Die Option **Projektabhängigkeiten** ist nur in einer Projektmappe mit mehr als einem Projekt verfügbar.

3. Wählen Sie auf der Registerkarte **Abhängigkeiten** ein Projekt aus dem Dropdownmenü **Projekt** aus.

4. Aktivieren Sie im Feld **Abhängigkeiten** die Kontrollkästchen für alle weiteren Projekte, die vor Erstellung dieses Projekts erstellt werden müssen.

   Die Projektmappe muss aus mehr als einem Projekt bestehen, bevor Sie Projektabhängigkeiten erstellen können.

## <a name="to-remove-dependencies-from-projects"></a>So entfernen Sie Abhängigkeiten aus Projekten

1. Wählen Sie im **Projektmappen-Explorer** ein Projekt aus.

2. Klicken Sie im Menü **Projekt** auf **Projektabhängigkeiten**.

     Das Dialogfeld **Projektabhängigkeiten** wird geöffnet.

    > [!NOTE]
    > Die Option **Projektabhängigkeiten** ist nur in einer Projektmappe mit mehr als einem Projekt verfügbar.

3. Wählen Sie auf der Registerkarte **Abhängigkeiten** ein Projekt aus dem Dropdownmenü **Projekt** aus.

4. Deaktivieren Sie im Feld **Abhängigkeiten** die Kästchen neben anderen Projekten, die keine Abhängigkeiten dieses Projekts mehr sind.

## <a name="see-also"></a>Siehe auch

- [Erstellen und Bereinigen von Projekten und Projektmappen in Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Kompilieren und Erstellen](../ide/compiling-and-building-in-visual-studio.md)
- [Grundlagen der Buildkonfiguration](../ide/understanding-build-configurations.md)
- [Verwalten von Projekt- und Projektmappeneigenschaften](managing-project-and-solution-properties.md)
