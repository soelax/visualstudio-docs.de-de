---
title: Debuggen von GPU-Code | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c7e77a5a-cb57-4b11-9187-ecc89acc8775
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bb5342dc2b5da3d1192aadbbea186b5b21f179f3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691552"
---
# <a name="debugging-gpu-code"></a>Debuggen von GPU-Code
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Sie können C++-Code debuggen, der im Grafikprozessor (Graphics Processing Unit, GPU) ausgeführt wird. Die GPU-Debugunterstützung in Visual Studio umfasst die Raceerkennung, das Starten von Prozessen bzw. Anfügen an Prozesse sowie die Integration in die Debugfenster.  
  
## <a name="supported-platforms"></a>Unterstützte Plattformen  
 Debugging wird unter [!INCLUDE[win7](../includes/win7-md.md)], [!INCLUDE[win8](../includes/win8-md.md)], [!INCLUDE[winsvr08_r2](../includes/winsvr08-r2-md.md)] und [!INCLUDE[winserver8](../includes/winserver8-md.md)] unterstützt. Für das Debuggen im Softwareemulator ist [!INCLUDE[win8](../includes/win8-md.md)] oder [!INCLUDE[winserver8](../includes/winserver8-md.md)] erforderlich. Für das Debuggen auf der Hardware müssen Sie die Treiber für Ihre Grafikkarte installieren. Nicht alle Hardwarehersteller implementieren sämtliche Debuggerfunktionen. Weitere Informationen zu Einschränkungen finden Sie in der Dokumentation des Herstellers.  
  
> [!NOTE]
> Unabhängige Hardwareanbieter, die GPU-Debugging in Visual Studio unterstützen möchten, müssen eine DLL erstellen, mit der die VSD3DDebug-Schnittstelle implementiert wird und die auf ihre eigenen Treiber ausgerichtet ist.  
  
## <a name="configuring-gpu-debugging"></a>Konfigurieren von GPU-Debugging  
 Der Debugger kann nicht beim CPU- und GPU-Code in der gleichen App-Ausführung unterbrechen. Standardmäßig unterbricht der Debugger beim CPU-Code. Um den GPU-Code zu debuggen, verwenden Sie einen dieser beiden Schritte:  
  
- Wählen Sie in der Liste **Debugtyp** auf der Symbolleiste **Standard** die Option **Nur GPU** aus.  
  
- Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt, und wählen Sie **Eigenschaften** aus. Wählen Sie im Dialogfeld **Eigenschaftenseiten** die Option **Debuggen** und dann in der Liste **Debuggertyp** die Option **Nur GPU** aus.  
  
## <a name="launching-and-attaching-to-applications"></a>Starten von und Anfügen an Anwendungen  
 Sie können die Visual Studio-Debuggingbefehle verwenden, um das GPU-Debugging zu starten und zu beenden. Weitere Informationen finden Sie unter [Navigieren im Code mit dem Debugger](../debugger/navigating-through-code-with-the-debugger.md). Sie können den GPU-Debugger auch an einen laufenden Prozess anfügen, jedoch nur, wenn dieser Prozess GPU-Code ausführt. Weitere Informationen finden Sie unter [Anfügen an ausgeführte Prozesse](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
## <a name="run-current-tile-to-cursor-and-run-to-cursor"></a>Befehle "Aktuelle Kachel bis zum Cursor ausführen" und "Ausführen bis Cursor"  
 Wenn Sie im Grafikprozessor debuggen, stehen Ihnen zwei Möglichkeiten zum Ausführen bis zur Cursorposition zur Verfügung. Die Befehle für beide Optionen sind im Kontextmenü des Code-Editors verfügbar.  
  
1. Mit dem Befehl **Ausführen bis Cursor** wird die App ausgeführt, bis sie die Cursorposition erreicht und dann angehalten wird. Dies bedeutet nicht, dass der aktuelle Thread bis zur Cursorposition ausgeführt wird, sondern vielmehr, dass der erste Thread, der die Cursorposition erreicht, die Unterbrechung auslöst. Finden Sie unter [Navigieren im Code mit dem Debugger](../debugger/navigating-through-code-with-the-debugger.md)  
  
2. Mit dem Befehl **Aktuelle Kachel bis zum Cursor ausführen** wird die App ausgeführt, bis alle Threads in der aktuellen Kachel die Cursorposition erreichen und dann angehalten werden.  
  
## <a name="debugging-windows"></a>Debugfenster  
 Wenn Sie bestimmte Debugfenster verwenden, können Sie GPU-Threads überprüfen, kennzeichnen und einfrieren. Weitere Informationen finden Sie unter:  
  
- [Verwenden des Fensters "Parallele Stapel"](../debugger/using-the-parallel-stacks-window.md)  
  
- [Verwenden des Fensters „Aufgaben“](../debugger/using-the-tasks-window.md)  
  
- [Vorgehensweise: Verwenden des Fensters „Parallele Überwachung“](../debugger/how-to-use-the-parallel-watch-window.md)  
  
- [Debuggen von Threads und Prozessen](../debugger/debug-threads-and-processes.md) (Symbolleiste "Debugspeicherort")  
  
- [Vorgehensweise: Verwenden des Fensters „GPU-Threads“](../debugger/how-to-use-the-gpu-threads-window.md)  
  
## <a name="data-synchronization-exceptions"></a>Ausnahmen bei Datensynchronisierung  
 Der Debugger kann mehrere Datensynchronisierungsbedingungen während der Ausführung erkennen. Wenn eine Bedingung erkannt wird, wechselt der Debugger in den Unterbrechungszustand. Sie haben zwei Optionen: **Unterbrechen** oder **Weiter**. Im Dialogfeld **Ausnahmen** können Sie konfigurieren, ob der Debugger diese Bedingungen erkennen soll und bei welchen Bedingungen eine Unterbrechung ausgelöst werden soll. Weitere Informationen finden Sie unter [Verwalten von Ausnahmen mit dem Debugger](../debugger/managing-exceptions-with-the-debugger.md). Sie können auch die **Optionen** im Dialogfeld, um anzugeben, dass der Debugger Ausnahmen ignorieren soll, wenn die Daten, die geschrieben werden, nicht den Wert der Daten ändert. Weitere Informationen finden Sie unter [General, Debugging, Options Dialog Box](../debugger/general-debugging-options-dialog-box.md).  
  
## <a name="troubleshooting"></a>Problembehandlung  
  
### <a name="specifying-an-accelerator"></a>Festlegen einer Zugriffstaste  
 Haltepunkte im GPU-Code werden nur erreicht, wenn der Code auf der REF-Zugriffstaste [accelerator::direct3d_ref](https://msdn.microsoft.com/library/a514b1a7-3b3f-4011-be6c-f7b0d9a42663) ausgeführt wird. Wenn Sie keine Zugriffstaste im Code angeben, wird die REF-Zugriffstaste automatisch als **Debuggingbeschleunigungstyp** in den Projekteigenschaften ausgewählt. Wenn der Code explizit eine Zugriffstaste auswählt, wird die REF-Zugriffstaste nicht beim Debuggen verwendet und die Haltepunkte werden nicht erreicht, es sei denn, die GPU-Hardware verfügt über Debugunterstützung. Um dieses Problem zu beheben, schreiben Sie den Code so, dass die REF-Zugriffstaste beim Debuggen verwendet wird. Weitere Informationen finden Sie unter Projekteigenschaften und [mit Accelerator and Accelerator_view Objects](https://msdn.microsoft.com/library/18f0dc66-8236-4420-9f46-1a14f2c3fba1) und [Projekteinstellungen für eine C++ Debugkonfiguration](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
### <a name="conditional-breakpoints"></a>Bedingte Haltepunkte  
 Bedingte Haltepunkte im GPU-Code werden unterstützt, jedoch kann nicht jeder Ausdruck auf dem Gerät ausgewertet werden. Wenn ein Ausdruck nicht auf dem Gerät ausgewertet werden kann, wird er im Debugger ausgewertet. Der Debugger wird wahrscheinlich langsamer ausgeführt als das Gerät.  
  
### <a name="error-there-is-a-configuration-issue-with-the-selected-debugging-accelerator-type"></a>Fehler: Es gibt ein Konfigurationsproblem mit den ausgewählten Debuggingbeschleunigungstyp.  
 Dieser Fehler tritt auf, wenn es zwischen den Projekteinstellungen und der Konfiguration des PCs, auf dem Sie debuggen, eine Inkonsistenz gibt. Weitere Informationen finden Sie unter [Projekteinstellungen für eine C++-Debugkonfiguration](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
### <a name="error-the-debug-driver-for-the-selected-debugging-accelerator-type-is-not-installed-on-the-target-machine"></a>Fehler: Der debugtreiber für den ausgewählten Debuggingbeschleunigungstyp ist nicht auf dem Zielcomputer installiert.  
 Dieser Fehler tritt auf, wenn Sie auf einem Remotecomputer debuggen. Der Debugger kann bis zur Laufzeit nicht bestimmen, ob die Treiber auf dem Remotecomputer installiert sind. Die Treiber sind vom Hersteller der Grafikkarte erhältlich.  
  
### <a name="error-timeout-detection-and-recovery-tdr-must-be-disabled-at-the-remote-site"></a>Fehler: Timeouterkennungs-TDR (and Recovery) müssen auf der Remotewebsite deaktiviert werden.  
 Es ist möglich, dass die C++ AMP-Berechnungen das Standardzeitintervall überschreiten, das durch den Windows-TDR-Prozess (Timeout Detection and Recovery) festgelegt wird. Wenn dies geschieht, wird die Berechnung abgebrochen und die Daten gehen verloren. Weitere Informationen finden Sie unter [Behandlung von TDRs in C++ AMP](http://go.microsoft.com/fwlink/p/?LinkId=249154).  
  
## <a name="see-also"></a>Siehe auch  
 [Exemplarische Vorgehensweise: Debuggen einer C++ AMP-Anwendung](https://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)   
 [Project Settings for a C++ Debug Configuration (Projekteinstellungen für eine C++-Debugkonfiguration)](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Start GPU Debugging in Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=255381) (Starten von GPU-Debugging in Visual Studio)
