---
title: Erfassen einer ETL-Ablaufverfolgung mit PerfView
ms.date: 06/27/2019
ms.topic: conceptual
helpviewer_keywords:
- perfview
- ETL Trace
author: mikeblome
ms.author: mblome
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Use perfview.exe to collect ETL traces for troubleshooting issues with Visual Studio
ms.openlocfilehash: 6b1f61888fa642ed544c6da7d1cf77c43b52b2d9
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461554"
---
# <a name="collect-an-etl-trace-with-perfview"></a>Erfassen einer ETL-Ablaufverfolgung mit PerfView

PerfView ist ein Tool, das basierend auf der [Ereignisablaufverfolgung für Windows](/windows/desktop/ETW/event-tracing-portal) ETL-Dateien (Event Trace Log, Ereignisablaufverfolgungs-Protokoll) erstellt, die bei der Behandlung bestimmter Probleme mit Visual Studio hilfreich sein können. Wenn Sie ein Problem melden, werden Sie möglicherweise vom Produktteam gebeten, PerfView zum Erfassen zusätzlicher Informationen auszuführen.

## <a name="install-perfview"></a>Installieren von PerfView

Laden Sie PerfView aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=28567) herunter.

## <a name="run-perfview"></a>Ausführen von PerfView

1. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf **PerfView.exe**, und wählen Sie **Als Administrator ausführen** aus.
1. Wählen Sie im Menü „Collect“ (Erfassen) die Option **Collect** aus.
1. Aktivieren Sie **Zip**, **Merge** und **ThreadTime**.
1. Erhöhen Sie **Circular MB** (MB für Umlaufprotokoll) auf 1000.
1. Ändern Sie **Current Dir** (Aktuelles Verzeichnis), um die ETL-Ablaufverfolgungen in einem angegebenen Ordner zu speichern, und „Data File“ (Datendatei), wenn Sie beabsichtigen, den Vorgang mehrmals durchzuführen.
1. Wählen Sie zum Starten der Datenaufzeichnung die Schaltfläche **Start Collection** (Sammlung starten).
1. Wählen Sie zum Beenden der Datenaufzeichnung die Schaltfläche **Stop Collection** (Sammlung beenden). Die Datei „PrefView.etl.zip“ wird im angegebenen Verzeichnis gespeichert.

PerfView kann nur die neuesten Daten speichern, die in den Puffer passen. Versuchen Sie daher, die Sammlung so bald wie möglich zu beenden, nachdem Visual Studio einzufrieren oder langsamer zu werden beginnt. Die Sammlung sollte nicht länger als 30 Sekunden durchgeführt werden, nachdem ein Problem aufgetreten ist.

Weitere Informationen erhalten Sie im [PerfView-Tutorial in Channel9](http://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-1-Collecting-data-with-the-Run-command).
