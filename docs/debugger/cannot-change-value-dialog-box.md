---
title: Kann nicht geändert werden (Dialogfeld) | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Cannot Change Value dialog box
- variables [debugger], editing
ms.assetid: 19e930c2-5fbf-4c83-aae8-a1dc3f8fcae8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f8f9dafe8ada8914591426dea9abc867de2236f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62564150"
---
# <a name="cannot-change-value-dialog-box"></a>Der Wert kann nicht geändert werden (Dialogfeld)
## <a name="error"></a>Fehler
 `The value of this variable cannot be changed` &#124;`The name` *Namen* `does not exist in the current context` &#124; *verschiedene andere Meldungen*

 Dieses Meldungsfeld wird angezeigt, wenn Sie versuchen, den Inhalt einer Variablen im Debuggerfenster (Fenster "Auto", "Überwachung" oder "Lokal") oder im Dialogfeld "Schnellüberwachung" auf einen ungültigen Wert zu ändern. Diese Meldung wird beispielsweise angezeigt, wenn Sie versuchen, den Wert einer Variablen mit einer ganzen Zahl in eine Zeichenfolge zu ändern.

## <a name="solution"></a>Lösung
 Stellen Sie sicher, dass der Wert, den Sie im Debuggerfenster oder im Fenster "Schnellüberwachung"eingeben, ein zulässiger Wert für die festzulegende Variable ist.

## <a name="see-also"></a>Siehe auch

- [Ausdrücke im Debugger](../debugger/expressions-in-the-debugger.md)