---
title: 'CA1601: Verwenden Sie keine Timer, um Änderungen am Betriebszustand zu verhindern.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
helpviewer_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
ms.assetid: b8028c92-0696-4c54-9773-0028f29bda9a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b3c3fe41332d488d180ddafbedfe29da1a3855e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921793"
---
# <a name="ca1601-do-not-use-timers-that-prevent-power-state-changes"></a>CA1601: Verwenden Sie keine Timer, um Änderungen am Betriebszustand zu verhindern.

|||
|-|-|
|TypeName|DoNotUseTimersThatPreventPowerStateChanges|
|CheckId|CA1601|
|Kategorie|Microsoft.Mobility|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Für einen Timer ist ein Intervall festgelegt, das mehr als einmal pro Sekunde auftritt.

## <a name="rule-description"></a>Regelbeschreibung
Rufen Sie nicht öfter als einmal pro Sekunde ab, oder verwenden Sie Zeitgeber, die häufiger als einmal pro Sekunde auftreten. Regelmäßige Aktivitäten mit einer höheren Frequenz belasten die CPU und beeinflussen energiesparende Leerlauftimer, mit denen die Anzeige sowie die Festplatten ausgeschaltet werden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Legen Sie Zeit Geber Intervalle so fest, dass Sie weniger als einmal pro Sekunde auftreten.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Diese Regel sollte nur unterdrückt werden, wenn der Timer mehr als einmal pro Sekunde ausgelöst wird und die Überlegungen zur Mobilität sicher ignoriert werden können.