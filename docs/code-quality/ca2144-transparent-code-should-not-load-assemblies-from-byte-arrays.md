---
title: 'CA2144: Transparenter Code darf keine Assemblys aus Bytearrays laden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2144
ms.assetid: 777b1310-6e16-4413-b4ee-5f3136304f82
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ff77d02ef9778112f5229e8104e9a1c1a1cde87
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920437"
---
# <a name="ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays"></a>CA2144: Transparenter Code darf keine Assemblys aus Bytearrays laden.

|||
|-|-|
|TypeName|TransparentMethodsShouldNotLoadAssembliesFromByteArrays|
|CheckId|CA2144|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Eine transparente Methode lädt eine Assembly aus einem Bytearray mit einer der folgenden Methoden:

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

## <a name="rule-description"></a>Regelbeschreibung
Die Sicherheitsüberprüfung für transparenten Code ist nicht so umfassend wie die Sicherheitsüberprüfung für wichtigen Code, da in transparentem Code keine sicherheitsrelevanten Aktionen ausgeführt werden können. Aus einem Bytearray geladene Assemblys werden in transparentem Code eventuell nicht erkannt, und dieses Bytearray könnte wichtigen oder sicherheitsgeschützten Code enthalten, der überwacht werden muss. Daher sollte transparenter Code keine Assemblys aus einem Bytearray laden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, markieren Sie die Methode, die die Assembly lädt <xref:System.Security.SecurityCriticalAttribute> , mit <xref:System.Security.SecuritySafeCriticalAttribute> dem-Attribut oder dem-Attribut.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Die Regel wird für den folgenden Code ausgelöst, da eine transparente Methode eine Assembly aus einem Bytearray lädt.

[!code-csharp[FxCop.Security.CA2144.TransparentMethodsShouldNotLoadAssembliesFromByteArrays#1](../code-quality/codesnippet/CSharp/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays_1.cs)]