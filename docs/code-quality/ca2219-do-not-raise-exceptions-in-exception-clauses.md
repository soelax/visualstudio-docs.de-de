---
title: 'CA2219: Keine Ausnahmen in Ausnahmeklauseln auslösen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f8e949e21530654882cba99a7d9fedad8b5b59b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920270"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: Keine Ausnahmen in Ausnahmeklauseln auslösen.

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|Kategorie|Microsoft.Usage|
|Unterbrechende Änderung|Nicht unterbrechend, unterbrechen|

## <a name="cause"></a>Ursache
Eine-Ausnahme wird von einer `finally`-, Filter-oder Fault-Klausel ausgelöst.

## <a name="rule-description"></a>Regelbeschreibung
Wenn eine Ausnahme in einer Exception-Klausel ausgelöst wird, erhöht Sie die Schwierigkeit des Debuggens erheblich.

Wenn eine Ausnahme in einer `finally` -oder-Fehler Klausel ausgelöst wird, verbirgt die neue Ausnahme die aktive Ausnahme, falls vorhanden. Dadurch wird der ursprüngliche Fehler schwer zu erkennen und zu debuggen.

Wenn eine Ausnahme in einer Filter Klausel ausgelöst wird, fängt die Laufzeit die Ausnahme automatisch ab und bewirkt, dass der Filter zu "false" ausgewertet wird. Es gibt keine Möglichkeit, den Unterschied zwischen dem Auswerten des Filters und einer Ausnahme, die von einem Filter ausgelöst wird, zu erkennen. Dadurch wird es schwierig, Fehler in der Logik des Filters zu erkennen und zu debuggen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um diesen Verstoß gegen diese Regel zu beheben, lösen Sie nicht explizit eine Ausnahme von `finally`einer-, Filter-oder Fault-Klausel aus.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung für diese Regel. Es gibt keine Szenarios, in denen eine Ausnahme, die in einer Exception-Klausel ausgelöst wird, den ausführenden Code als Vorteil bietet.

## <a name="related-rules"></a>Verwandte Regeln
[CA1065: Keine Ausnahmen an unerwarteten Speicherorten](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>Siehe auch
[Entwurfswarnungen](../code-quality/design-warnings.md)