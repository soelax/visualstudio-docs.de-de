---
title: Seite "Debuggen", Projekt-Designer
ms.date: 06/27/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a1f54485a4dd47b0aec4401f6cdfb39072e9f8cf
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461409"
---
# <a name="debug-page-project-designer"></a>Seite "Debuggen", Projekt-Designer

Verwenden Sie die Seite **Debuggen** des **Projekt-Designers**, um Eigenschaften für das Debugverhalten in einem Visual Basic oder C#-Projekt festzulegen.

Klicken Sie auf einen Projektknoten im **Projektmappen-Explorer**, um auf die Seite **Debuggen** zuzugreifen. Klicken Sie im Menü **Projekt** auf **\<ProjectName > Eigenschaften**. Sobald der **Projekt-Designer** angezeigt wird, klicken Sie auf die Registerkarte **Debuggen**.

> [!NOTE]
> Dieses Thema gilt nicht für UWP-Apps. Weitere Informationen zu UWP-Apps finden Sie unter [Starten einer Debugsitzung (VB, C#, C++ und XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md).

## <a name="configuration-and-platform"></a>Konfiguration und Plattform

Die folgenden Optionen ermöglichen es Ihnen, die anzuzeigende bzw. zu ändernde Konfiguration und Plattform auszuwählen.

**Konfiguration**

Gibt an, welche Konfigurationseinstellungen angezeigt oder geändert werden sollen. Die Einstellungen sind **Debuggen** (Standardeinstellung), **Freigeben** oder **Alle Konfigurationen**.

**Plattform**

Gibt an, welche Plattformeinstellungen angezeigt oder geändert werden sollen. Die Optionen sind **Beliebige CPU** (Standardeinstellung), **x64** oder **x86**.

## <a name="start-action"></a>Startaktion

Der **Startvorgang** gibt an, welches Element beim Debuggen der Anwendung gestartet wird: das Projekt, ein benutzerdefiniertes Programm, eine URL oder keines. Diese Option ist standardmäßig auf **Projekt starten** festgelegt. Die Einstellung **Startaktion** auf der Seite **Debuggen** bestimmt den Wert der `StartAction`-Eigenschaft.

**Projekt starten**

Wählen Sie diese Option aus, um anzugeben, dass die ausführbare Datei (bei Projekten für Windows-Anwendungen und Konsolenanwendungen) beim Debuggen der Anwendung gestartet werden soll. Diese Option ist standardmäßig ausgewählt.

**Externes Programm starten**

Wählen Sie diese Option aus, um anzugeben, dass ein bestimmtes Programm beim Debuggen der Anwendung gestartet werden soll.

**Browser mit URL starten**

Wählen Sie diese Option aus, um anzugeben, dass beim Debuggen der Anwendung auf eine bestimmte URL zugegriffen werden soll.

## <a name="start-options"></a>Startoptionen

**Befehlszeilenargumente**

Geben Sie in diesem Textfeld die Befehlszeilenargumente ein, die für das Debuggen verwendet werden sollen.

**Arbeitsverzeichnis**

Geben Sie in diesem Textfeld das Verzeichnis ein, aus dem das Projekt gestartet wird. Klicken Sie alternativ auf die Schaltfläche „Durchsuchen“ ( **...** ), um ein Verzeichnis auszuwählen.

**Remotecomputer verwenden**

Aktivieren Sie dieses Kontrollkästchen, und geben Sie den Pfad zum Remotecomputer in das Textfeld ein, um die Anwendung über einen Remotecomputer zu debuggen.

## <a name="debugger-engines"></a>Debugger-Engines

**Debuggen von nativem Code aktivieren**

Diese Option gibt an, ob das Debuggen von nativem Code unterstützt wird. Aktivieren Sie dieses Kontrollkästchen, wenn Sie COM-Objekte aufrufen, oder wenn Sie ein benutzerdefiniertes Programm starten, das Ihr Projekt aufruft und in nativem Code geschrieben ist, und Sie den nativen Code debuggen müssen. Deaktivieren Sie dieses Kontrollkästchen, um das Debuggen von unverwaltetem Code zu deaktivieren. Dieses Kontrollkästchen ist standardmäßig deaktiviert.

**SQL Server-Debuggen aktivieren**

Aktivieren oder deaktivieren Sie dieses Kontrollkästchen, um das Debuggen von SQL-Prozeduren über Ihre Visual Basic-Anwendung zu aktivieren oder zu deaktivieren. Dieses Kontrollkästchen ist standardmäßig deaktiviert.

## <a name="see-also"></a>Siehe auch

- [Erster Einblick in den Debugger](../../debugger/debugger-feature-tour.md)
- [Projekteinstellungen für C#-Debugkonfigurationen](../../debugger/project-settings-for-csharp-debug-configurations.md)
- [Projekteinstellungen für eine Visual Basic-Debugkonfiguration](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [Vorgehensweise: Debuggen einer ClickOnce-Anwendung mit eingeschränkten Berechtigungen](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [Vorgehensweise: Erstellen und Bearbeiten von Konfigurationen](../../ide/how-to-create-and-edit-configurations.md)