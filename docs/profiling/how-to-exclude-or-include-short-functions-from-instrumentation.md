---
title: Ausschließen oder Einschließen kurzer Funktionen in die Instrumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, instrument events
- profiling tools, include short functions
- profiling tools, exclude short functions
ms.assetid: eaeead79-aafe-4490-86ff-6ed4cad9c15f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8f9601a39e755c1a3886f7049abd592d793fb4b
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261350"
---
# <a name="how-to-exclude-or-include-short-functions-from-instrumentation"></a>Vorgehensweise: Ausschließen oder Einschließen kurzer Funktionen in die Instrumentation
Die Profilerstellungstools schließen standardmäßig *Kleine Funktionen* von der Instrumentation aus. Kleine Funktionen sind kurze Funktionen, die keine Funktionsaufrufe ausführen. Das Ausschließen dieser kleinen Funktionen sorgt für weniger Instrumentation-Overhead und verbessert dadurch die Instrumentierungsgeschwindigkeit. Der Ausschluss kleiner Funktionen reduziert auch die Größe der Leistungsprofilerstellungsdatendatei (.*vsp*) und die Zeit, die für die Analyse erforderlich ist. Wenn kleine Funktionen ausgeschlossen werden, zählt die Zeit, die in den kleinen Funktionen verbracht wird, gegen die exklusive und inklusive Zeit der übergeordneten Funktionen. Kleine Funktionen können in die Instrumentation ausgeschlossen oder eingeschlossen werden, wie im folgenden Verfahren beschrieben wird.

### <a name="to-exclude-or-include-short-functions-from-instrumentation"></a>So schließen Sie kurze Funktionen in die Instrumentierung ein oder aus

1. Klicken Sie im **Leistungs-Explorer** mit der rechten Maustaste auf **Leistungssitzung**, und wählen Sie **Eigenschaften** aus.

     Das Dialogfeld **Eigenschaftenseiten** wird angezeigt.

2. Klicken Sie auf den **Eigenschaftenseiten** auf die Eigenschaften von **Instrumentierung**.

3. Wählen Sie zum Ausschließen von kleinen Funktionen in die Instrumentierung **Kleine Funktionen in die Instrumentierung ausschließen** Dies ist die Standardeinstellung.

     - oder - 

     Deaktivieren Sie zum Einschließen von kleinen Funktionen in die Instrumentierung **Kleine Funktionen in die Instrumentierung ausschließen**

4. Klicken Sie auf **OK**.

## <a name="see-also"></a>Siehe auch
- [Steuerung der Datensammlung](../profiling/controlling-data-collection.md)
- [Eigenschaften von Leistungssitzungen](../profiling/performance-session-properties.md)