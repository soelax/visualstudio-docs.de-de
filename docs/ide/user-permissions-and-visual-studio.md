---
title: Als Administrator ausführen
ms.date: 06/05/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, user permissions
- user permissions
- administrative privileges
- permissions
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d012c0902aa82eb057f9d69c0b85b13262e847a
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66747621"
---
# <a name="user-permissions-and-visual-studio"></a>Benutzerberechtigungen und Visual Studio

Aus Sicherheitsgründen sollten Sie Visual Studio möglichst als normaler Benutzer ausführen.

> [!WARNING]
> Sie sollten auch sicherstellen, dass Sie keine Visual Studio-Projektmappe kompilieren, starten oder debuggen, die nicht von einer vertrauenswürdigen Person oder einem vertrauenswürdigen Speicherort stammt.

Sie können fast jeden Vorgang in der Visual Studio-IDE als normaler Benutzer durchführen. Sie benötigen Administratorberechtigungen, um folgende Aufgaben durchzuführen:

|Bereich|Aufgabe|Weitere Informationen|
|----------|----------| - |
|Installation|Installieren von Visual Studio.|[Installieren von Visual Studio](../install/install-visual-studio.md)|
||Installieren, Aktualisieren oder Entfernen von lokalen Hilfeinhalten.|[Installieren und Verwalten von lokalen Hilfeinhalten](../help-viewer/install-manage-local-content.md)|
|Werkzeugkasten|Hinzufügen von klassischen COM-Steuerelementen zur **Toolbox**.|[Werkzeugkasten](../ide/reference/toolbox.md)|
|Erstellung|Verwenden von Postbuildereignissen, die eine Komponente registrieren.|[Grundlagen benutzerdefinierter Buildschritte und Buildereignisse](/cpp/build/understanding-custom-build-steps-and-build-events)|
||Einschließen eines Registrierungsschritts beim Erstellen von C++-Projekten.||
|Debuggen|Debuggen von Anwendungen, die mit höheren Berechtigungen ausgeführt werden.|[Debuggereinstellungen und -vorbereitung](../debugger/debugger-settings-and-preparation.md)|
||Debuggen von Anwendungen, die unter einem anderen Benutzerkonto ausgeführt werden, z.B. ASP.NET-Websites.|[Debuggen von ASP.NET- und AJAX-Anwendungen](../debugger/how-to-enable-debugging-for-aspnet-applications.md)|
||Debuggen in der Zone für XAML-Browseranwendungen (XBAP).|[WPF-Host (PresentationHost.exe)](/dotnet/framework/wpf/app-development/wpf-host-presentationhost-exe)|
||Verwenden des Emulators zum Debuggen von Clouddienstprojekten für Microsoft Azure.|[Debuggen eines Clouddiensts in Visual Studio](/azure/vs-azure-tools-debug-cloud-services-virtual-machines)|
||Konfigurieren einer Firewall für das Remotedebuggen.|[Remotedebuggen](../debugger/remote-debugging.md)|
|Leistungstools|Profilerstellung für eine Anwendung|[Einführung in die Leistungsprofilerstellung](../profiling/beginners-guide-to-performance-profiling.md)|
|Bereitstellung|Bereitstellen einer Webanwendung für Internetinformationsdienste (IIS) auf einem lokalen Computer.|[Bereitstellen einer ASP.NET-Web-App mit Visual Studio](/aspnet/web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/)|

## <a name="run-visual-studio-as-an-administrator"></a>Ausführen von Visual Studio als Administrator

Wenn Sie Visual Studio als Administrator ausführen müssen, befolgen Sie diese Schritte, um die IDE zu öffnen:

> [!NOTE]
> Diese Anweisungen gelten für Windows 10. Für andere Windows-Versionen lauten die Anweisungen ähnlich.

::: moniker range="vs-2017"

1. Öffnen Sie das Menü **Start**, und scrollen Sie zu Visual Studio 2017.

1. Wählen Sie im Kontextmenü von **Visual Studio 2017** die Optionen **Mehr** > **Als Administrator ausführen** aus.

   Beim Starten von Visual Studio wird **(Administrator)** nach dem Produktnamen in der Titelleiste angezeigt.

::: moniker-end

::: moniker range=">=vs-2019"

1. Öffnen Sie das Menü **Start**, und scrollen Sie zu Visual Studio 2019.

1. Wählen Sie im Kontextmenü von **Visual Studio 2019** die Optionen **Mehr** > **Als Administrator ausführen** aus.

   Beim Starten von Visual Studio wird **(Administrator)** nach dem Produktnamen in der Titelleiste angezeigt.

::: moniker-end

Sie können die Anwendungsverknüpfung ebenfalls so ändern, dass die Anwendung immer mit Administratorberechtigungen ausgeführt wird.

## <a name="see-also"></a>Siehe auch

- [Übertragung, Migration und Upgrade der Visual Studio-Projekte](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [Installieren von Visual Studio](../install/install-visual-studio.md)