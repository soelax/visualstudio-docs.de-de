---
title: 'CA1900: Werttypfelder sollten portabel sein.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f734d0cf28a5aec28ebbf635dd384efe176b1774
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921322"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900: Werttypfelder sollten portabel sein.

|||
|-|-|
|TypeName|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|Kategorie|Microsoft.Portability|
|Unterbrechende Änderung|Unterbrechung: Wenn das Feld außerhalb der Assembly sichtbar ist.<br /><br /> Nicht unterbrechend: Wenn das Feld außerhalb der Assembly nicht sichtbar ist.|

## <a name="cause"></a>Ursache
Mit dieser Regel wird überprüft, ob Strukturen, die mit expliziten Layouts deklariert werden, beim Marshalling an nicht verwalteten Code auf 64-Bit-Betriebssystemen korrekt ausgerichtet werden. IA-64 lässt keine nicht ausgerichteten Speicherzugriffe zu, und der Prozess stürzt ab, wenn diese Verletzung nicht korrigiert wird.

## <a name="rule-description"></a>Regelbeschreibung
Strukturen mit expliziten Layouts, die falsch ausgerichtete Felder enthalten, verursachen Abstürze bei 64-Bit-Betriebssystemen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Alle Felder, die kleiner als 8 Bytes sind, müssen Offsets aufweisen, die ein Vielfaches ihrer Größe aufweisen, und Felder, die 8 Bytes oder mehr umfassen, müssen Offsets aufweisen, die ein Vielfaches von 8 sind. Eine andere Lösung ist, `LayoutKind.Sequential` wenn vernünftig `LayoutKind.Explicit`, anstelle von zu verwenden.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Diese Warnung sollte nur unterdrückt werden, wenn Sie fehlerhaft auftritt.