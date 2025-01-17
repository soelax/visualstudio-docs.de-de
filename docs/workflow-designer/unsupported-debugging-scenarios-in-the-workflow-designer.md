---
title: Im Workflow-Designer nicht unterstützte Debugszenarien
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 6adbe379-41d0-4681-9cd0-b91f187c3c2c
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 9cda710a3a2f4945e96e706479996da0a1fa7e12
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825735"
---
# <a name="unsupported-debugging-scenarios-in-the-workflow-designer"></a>Im Workflow-Designer nicht unterstützte Debugszenarien

Der Workflow-Designer unterstützt die folgenden Debugszenarien nicht:

- Nach dem Bearbeiten von Code kann die Ausführung nicht fortgesetzt werden.

- Die Ausführung kann an einem beliebigen Punkt im Workflow nicht fortgesetzt werden (Nächste Anweisung festlegen).

- Die Ausführung kann nicht bis zum Cursor fortgesetzt werden (Ausführen bis Cursor).

- Der Workflow-Designer kann nicht verwendet werden, um Workflows zu debuggen, die ohne den Designer direkt im Code erstellt wurden.

- In früheren Versionen von Windows Workflow Foundation (WF) erstellte Workflows können nicht debuggt werden, in .NET Framework 4 oder höher.

- Es können keine Haltepunkte auf Verknüpfungen zwischen Aktivitäten oder <xref:System.Activities.Statements.Flowchart>-Knoten definiert werden.

- Die Zwischenablage steht während des Debuggens nicht zur Verfügung.

- Haltepunkte werden nicht beibehalten, wenn Aktivitäten kopiert oder eingefügt werden.

- Im Fenster Aufrufliste können keine Workflowhaltepunkte festgelegt werden.

- Beim Erstellen von Haltepunkten im Designer die **Zeile** und **Zeichen** Einstellungen in der **Neuer Haltepunkt** Dialogfeld nicht verwendet werden.

- Im Haltepunktfenster und im Kontextmenü werden die folgenden Spalten bzw. Optionen für das Debuggen von Workflows nicht unterstützt:

  - Bedingung

  - Trefferanzahl

  - Bei Treffer

  - Funktion

  - Daten

  - Verarbeiten

  - Gehe zu Disassembly
