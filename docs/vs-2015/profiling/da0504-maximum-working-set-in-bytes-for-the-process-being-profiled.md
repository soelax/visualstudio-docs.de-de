---
title: 'DA0504: Maximale Arbeitsseite in Bytes für den Prozess, für den die Profilerstellung ausgeführt wird | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0504
- vs.performance.504
- vs.performance.rules.DA0504
ms.assetid: 36e71603-ece7-4000-85fc-9da4eed61bf2
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a990b428cfa03722ee5e02884344d96844825ee8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157161"
---
# <a name="da0504-maximum-working-set-in-bytes-for-the-process-being-profiled"></a>DA0504: Maximale Arbeitsseite in Bytes für den Prozess, für den die Profilerstellung ausgeführt wird
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Regel-Id | DA0504 |  
| Kategorie | Resource Manager |  
| Profilerstellungsmethode | Alle |  
| Nachricht | Diese Informationen war nur zu Informationszwecken gesammelt. Vom Leistungsindikator für die Verarbeitung von Arbeitsseiten wird die Belegung des physischen Speichers durch den Prozess ermittelt, für den die Profilerstellung ausgeführt wird. Bei dem gemeldeten Wert handelt es sich um den Maximalwert aus allen Messintervallen.|  
| Regeltyp | Informationen |  
  
 Wenn Sie Profile mithilfe der Sampling-, .NET-Arbeitsspeicher- oder Ressourcenkonfliktmethode Profile erstellen, müssen mindestens 10 Samplings erfasst werden, damit diese Regel ausgelöst wird.  
  
## <a name="rule-description"></a>Regelbeschreibung  
 In dieser Meldung wird die maximale Menge an virtuellem Arbeitsspeicher (in Bytes) gemeldet, die derzeit vom Prozess verwendet wird. Die Prozessarbeitsseite stellt Seiten aus dem Prozessadressbereich dar, die sich gegenwärtig im physischen Speicher befinden. Von dieser Regel wird der maximale Wert für die Prozessarbeitsseite bei aktiver Profilerstellung gemeldet.  
  
 Der gemeldete Wert enthält residente Seiten aus freigegebenen Arbeitsspeichersegmenten, auf die vom Prozess verwiesen wurde. In den berücksichtigten freigegebenen Arbeitsspeichersegmenten sind auch freigegebene DLLs enthalten, auf die vom Prozess verwiesen wird. Aufgrund von freigegebenen Arbeitsspeichersegmenten kann der Wert der Prozessarbeitsseite die Menge des virtuellen Arbeitsspeichers übersteigen, der vom Prozess belegt wird.  
  
 Die Größe der Prozessarbeitsseite spiegelt die Menge des virtuellen Arbeitsspeichers wider, die aktiv vom Prozess verwendet wird. Sie wird auch von der Menge an physischem Speicher (oder RAM) beeinflusst, die zum Ausführen der Anwendung verfügbar ist, sowie von der Auslastung dieses physischen Speichers durch andere ausgeführte Prozesse. Weitere Informationen zu Prozessarbeitsseiten finden Sie unter [Working Set (Arbeitsseite)](http://go.microsoft.com/fwlink/?LinkId=177830) in der Dokumentation zur Speicherverwaltung unter Windows auf MSDN.  
  
## <a name="how-to-use-rule-data"></a>Verwenden von Regeldaten  
 Diese Messdaten stammen aus der Windows-Leistungsüberwachung und dienen lediglich als Information. Mithilfe der Daten können Sie die Leistung anderer Versionen oder Builds des Programms vergleichen oder die Leistung der Anwendung in unterschiedlichen Testszenarios nachvollziehen.  
  
 Doppelklicken Sie auf die Meldung im Fenster „Fehlerliste“, um zur Ansicht [Markierungen](../profiling/marks-view.md) der Profilerstellungsdaten zu navigieren. Suchen Sie die Spalten mit den Leistungsindikatoren **Prozess\Arbeitsseite** und **Arbeitsspeicher\Seiten/s**. Suchen Sie anschließend den maximalen Wert von **Prozess\Arbeitsseite**, und vergleichen Sie ihn mit dem Wert von **Arbeitsspeicher\Seiten/s**. Häufig hängt der Maximalwert für Arbeitsseiten mit einem Intervall mit geringerer E/A-Auslagerungsaktivität zusammen. Dies gilt besonders bei Computern mit eingeschränktem Arbeitsspeicher.
