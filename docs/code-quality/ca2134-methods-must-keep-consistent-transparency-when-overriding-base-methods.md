---
title: 'CA2134: Methoden müssen beim Überschreiben von Basismethoden eine konsistente Transparenz wahren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2134
ms.assetid: 3b17e487-0326-442e-90e1-dc0ba9cdd3f2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ca28f364307d4a2b73235bc6541cb8aa01abd56
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920655"
---
# <a name="ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods"></a>CA2134: Methoden müssen beim Überschreiben von Basismethoden eine konsistente Transparenz wahren.

|||
|-|-|
|TypeName|Methodsmustoverride withkonsistenttransparenz|
|CheckId|CA2134|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Diese Regel wird ausgelöst, wenn eine mit dem <xref:System.Security.SecurityCriticalAttribute> markierte Methode eine Methode überschreibt, die transparent oder <xref:System.Security.SecuritySafeCriticalAttribute>mit markiert ist. Die Regel wird auch ausgelöst, wenn eine Methode, die transparent oder mit <xref:System.Security.SecuritySafeCriticalAttribute> markiert ist, eine Methode überschreibt, die <xref:System.Security.SecurityCriticalAttribute>mit gekennzeichnet ist.

Die Regel wird angewendet, wenn eine virtuelle Methode überschrieben oder eine Schnittstelle implementiert wird.

## <a name="rule-description"></a>Regelbeschreibung
Diese Regel wird für Versuche ausgelöst, den Sicherheits Zugriff einer Methode weiter oben in der Vererbungs Kette zu ändern. Wenn eine virtuelle Methode in einer Basisklasse z. b. transparent oder sicherheitsrelevant ist, muss Sie von der abgeleiteten Klasse mit einer transparenten oder sicherheitskritischen Methode überschrieben werden. Umgekehrt muss die abgeleitete Klasse diese mit einer sicherheitskritischen Methode überschreiben, wenn Sie sicherheitskritisch ist. Die gleiche Regel gilt für die Implementierung von Schnittstellen Methoden.

Transparenzregeln werden erzwungen, wenn der Code anstelle der Laufzeit JIT kompiliert wird, sodass die Transparenz Berechnung nicht über dynamische Typinformationen verfügt. Daher muss das Ergebnis der Transparenz Berechnung in der Lage sein, nur von den statischen Typen zu bestimmen, die JIT-kompiliert werden, unabhängig vom dynamischen Typ.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, ändern Sie die Transparenz der Methode, die eine virtuelle Methode überschreibt, oder implementieren Sie eine Schnittstelle, die der Transparenz der virtuellen oder Schnittstellen Methode entspricht.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Warnungen von dieser Regel nicht unterdrücken. Verstöße gegen diese Regel führen zu einer Laufzeit <xref:System.TypeLoadException> für Assemblys, die Transparenz der Ebene 2 verwenden.

## <a name="examples"></a>Beispiele

### <a name="code"></a>Code
[!code-csharp[FxCop.Security.CA2134.MethodsMustOverrideWithConsistentTransparency#1](../code-quality/codesnippet/CSharp/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods_1.cs)]

## <a name="see-also"></a>Siehe auch
[Sicherheits transparenter Code, Ebene 2](/dotnet/framework/misc/security-transparent-code-level-2)