---
title: 'CA1033: Schnittstellenmethoden sollten von untergeordneten Typen aufgerufen werden können.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InterfaceMethodsShouldBeCallableByChildTypes
- CA1033
helpviewer_keywords:
- CA1033
- InterfaceMethodsShouldBeCallableByChildTypes
ms.assetid: 9f171497-a5e3-4769-a77b-7aed755b2662
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 10db644fe4cf65a7336ef8bd50dcf62e072e1c46
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922957"
---
# <a name="ca1033-interface-methods-should-be-callable-by-child-types"></a>CA1033: Schnittstellenmethoden sollten von untergeordneten Typen aufgerufen werden können.

|||
|-|-|
|TypeName|InterfaceMethodsShouldBeCallableByChildTypes|
|CheckId|CA1033|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Ein unversiegelter, extern sichtbarer Typ gibt eine explizite Methodenimplementierung einer öffentlichen Schnittstelle an und gibt keine alternative extern sichtbare Methode mit dem gleichen Namen an.

## <a name="rule-description"></a>Regelbeschreibung
Beachten Sie einen Basistyp, der eine öffentliche Schnittstellen Methode explizit implementiert. Ein Typ, der vom Basistyp abgeleitet wird, kann nur über einen Verweis auf die aktuelle Instanz (`this` in C#), die in die-Schnittstelle umgewandelt wird, auf die geerbte Schnittstellen Methode zugreifen. Wenn der abgeleitete Typ die geerbte Schnittstellen Methode (explizit) neu implementiert, kann auf die Basis Implementierung nicht mehr zugegriffen werden. Durch den Aufruf über den aktuellen Instanzverweis wird die abgeleitete Implementierung aufgerufen. Dies bewirkt eine Rekursion und einen eventuellen Stapelüberlauf.

Diese Regel meldet keine Verstöße gegen eine explizite Implementierung von <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> , wenn eine extern sichtbare `Close()` -oder `System.IDisposable.Dispose(Boolean)` -Methode bereitgestellt wird.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, implementieren Sie eine neue Methode, die die gleiche Funktionalität verfügbar macht und für abgeleitete Typen sichtbar ist, oder ändern Sie zu einer nicht expliziten Implementierung. Wenn ein Breaking Change akzeptabel ist, besteht eine Alternative darin, den Typ versiegelt zu machen.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn eine extern sichtbare Methode bereitgestellt wird, die über die gleiche Funktionalität, aber einen anderen Namen als die explizit implementierte Methode verfügt.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt einen Typ `ViolatingBase`,, der gegen die Regel verstößt, und einen `FixedBase`Typ,, der eine Korrektur für die Verletzung anzeigt.

[!code-csharp[FxCop.Design.ExplicitMethodImplementations#1](../code-quality/codesnippet/CSharp/ca1033-interface-methods-should-be-callable-by-child-types_1.cs)]

## <a name="see-also"></a>Siehe auch
[Schnittstellen](/dotnet/csharp/programming-guide/interfaces/index)