---
title: GlobalOn und GlobalOff | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b0ed68-d19e-473e-9af3-252c11d82bcf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ee29b677096e46d965e8191cf26a829587471dd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62969627"
---
# <a name="globalon-and-globaloff"></a>GlobalOn und GlobalOff
Die *VSPerfCmd.exe*-Optionen **GlobalOff** und **GlobalOn** halten die Profilerstellung für alle Prozesse und Threads in einer Profilerstellungssitzung über die Befehlszeile an bzw. setzen sie fort.

 Sie können **GlobalOff** und **GlobalOn** als die einzigen Optionen einer *VSPerfCmd.exe*-Befehlszeile angeben, oder Sie können sie in Befehlszeilen einschließen, die auch die Optionen **Start**, **Launch** (Starten) oder **Attach** (Anfügen) enthalten.

 **GlobalOn** und **GlobalOff** können auch mit den Optionen **ProcessOn**, **ProcessOff**, **ThreadOn** und **ThreadOff** kombiniert werden.

 Die Optionen **GlobalOn** und **GlobalOff** interagieren mit den Optionen **ProcessOn** und **ProcessOff**, die die Datensammlung für einen angegebenen Prozess steuern, sowie mit den Optionen **ThreadOn** und **ThreadOff**, die die Datensammlung für einen angegebenen Thread steuern.

 Die Optionen **GlobalOff** und **GlobalOn** beeinflussen auch die globale Start/Stop-Anzahl, die von den API-Funktionen des Profilers manipuliert wird.

- **GlobalOff** legt die globale Start/Stop-Anzahl sofort auf 0 fest und hält die Profilerstellung daher an.

- **GlobalOn** legt die globale Start/Stop-Anzahl sofort auf 1 fest und setzt die Profilerstellung daher fort.

  Weitere Informationen finden Sie unter [APIs für Profilerstellungstools](../profiling/profiling-tools-apis.md).

## <a name="syntax"></a>Syntax

```cmd
VSPerfCmd.exe /{GlobalOff|GlobalOn}

VSPerfCmd.exe /Start:Method /{GlobalOff|GlobalOn} [Options]

VSPerfCmd.exe {Launch:AppName|Attach:PID} /{GlobalOff|GlobalOn}[Options]
```

#### <a name="parameters"></a>Parameter
 Keiner

## <a name="valid-options"></a>Gültige Optionen
 **GlobalOn** und **GlobalOff** können in Befehlszeilen angegeben werden, die auch die folgenden Optionen enthalten:

 **Start:** `Method` initialisiert die Befehlszeilen-Profilerstellungssitzung und legt die angegebene Profilerstellungsmethode fest.

 **Launch:** `AppName` startet die angegebene Anwendung und beginnt die Profilerstellung mit der Samplingmethode.

 **Attach:** `PID` startet die Profilerstellung für den angegebenen Prozess.

 {**ProcessOff**|**ProcessOn**} **:** `PID` Beendet oder startet die Profilerstellung für den angegebenen Prozess

 {**ThreadOff**|**ThreadOn**} **:** `TID` Beendet oder startet die Profilerstellung für den angegebenen Prozess (nur Instrumentierungsmethode)

## <a name="example"></a>Beispiel
 In diesem Beispiel werden die Optionen **GlobalOff** und **GlobalOn** verwendet, um die Sammlung von Profilerstellungsdaten für das Starten und Herunterfahren der Anwendung zu vermeiden.

```cmd
; Initialize the profiler with profiling stopped.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp /GlobalOff
; Start an instrumented application and wait for it to warm up.
; Start profiling.
VSPerfCmd.exe /GlobalOn
; Exercise the application functionality that you want to profile.
; Stop profiling.
VSPerfCmd.exe /GlobalOff
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>Siehe auch
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [Profilerstellung für eigenständige Anwendungen](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [Profilerstellung für ASP.NET-Webanwendungen](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [Profilerstellung für Dienste](../profiling/command-line-profiling-of-services.md)