---
title: Verwalten von Buildkonfigurationen mit Visual Basic-Entwicklereinstellungen
ms.date: 11/21/2018
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- advanced build configurations
- building with Visual Basic developer settings (Visual Studio)
- debug builds
- release builds
ms.assetid: eaea6e0b-6c61-4869-8d63-d372c745a23c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b422b1844ffb30c1c6f2f8fa8845995c98c794e4
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416843"
---
# <a name="how-to-manage-build-configurations-with-visual-basic-developer-settings-applied"></a>Vorgehensweise: Verwalten von Buildkonfigurationen mit aktivierten Visual Basic Developer-Einstellungen

Standardmäßig werden alle Optionen für die Buildkonfiguration ausgeblendet, wenn die Visual Basic-Entwicklereinstellungen aktiviert sind. In diesem Artikel wird erläutert, wie Sie diese Buildeinstellungen manuell aktivieren.

## <a name="enable-advanced-build-configurations"></a>Aktivieren von erweiterten Buildkonfigurationen

Standardmäßig blenden die Visual Basic-Entwicklereinstellungen die Option aus, das Dialogfeld **Konfigurations-Manager** und die Listen **Konfiguration** und **Plattform** im [Projekt-Designer](../ide/reference/application-page-project-designer-visual-basic.md) zu öffnen.

1. Klicken Sie im Menü **Extras** auf **Optionen**.

2. Erweitern Sie **Projekte und Projektmappen**, und klicken Sie auf **Allgemein**.

    > [!NOTE]
    > Der Knoten **Allgemein** ist auch sichtbar, wenn die Option **Alle Einstellungen anzeigen** deaktiviert ist. Wenn Sie alle verfügbaren Optionen anzeigen möchten, klicken Sie auf **Alle Einstellungen anzeigen**.

3. Klicken Sie auf **Erweiterte Buildkonfigurationen anzeigen**.

4. Klicken Sie auf **OK**.

     Der **Konfigurations-Manager** ist nun im Menü **Erstellen** verfügbar, und die Listen **Konfiguration** und **Plattform** werden im **Projekt-Designer** angezeigt.

## <a name="see-also"></a>Siehe auch

- [Grundlagen der Buildkonfiguration](../ide/understanding-build-configurations.md)
- [Kompilieren und Erstellen](../ide/compiling-and-building-in-visual-studio.md)
- [Umgebungseinstellungen](../ide/environment-settings.md)