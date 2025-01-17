---
title: 'CA1002: Generische Listen nicht verfügbar machen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotExposeGenericLists
- CA1002
helpviewer_keywords:
- CA1002
- DoNotExposeGenericLists
ms.assetid: 5caac810-1a79-47df-a27b-c46c5040bf34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6e300edf07aa98facbe6059ba9574e238ec8f3e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923243"
---
# <a name="ca1002-do-not-expose-generic-lists"></a>CA1002: Generische Listen nicht verfügbar machen.

|||
|-|-|
|TypeName|DoNotExposeGenericLists|
|CheckId|CA1002|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein Typ enthält einen extern sichtbaren Member, bei <xref:System.Collections.Generic.List%601?displayProperty=fullName> dem es sich um <xref:System.Collections.Generic.List%601?displayProperty=fullName> einen Typ handelt, der einen- <xref:System.Collections.Generic.List%601?displayProperty=fullName> Typ zurückgibt oder dessen Signatur einen-Parameter enthält.

## <a name="rule-description"></a>Regelbeschreibung
 <xref:System.Collections.Generic.List%601?displayProperty=fullName>ist eine generische Auflistung, die für die Leistung und nicht Vererbung konzipiert ist. <xref:System.Collections.Generic.List%601?displayProperty=fullName>enthält keine virtuellen Member, die das Ändern des Verhaltens einer geerbten Klasse vereinfachen. Die folgenden generischen Auflistungen sind für Vererbung konzipiert und sollten <xref:System.Collections.Generic.List%601?displayProperty=fullName>anstelle von verfügbar gemacht werden.

- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, ändern <xref:System.Collections.Generic.List%601?displayProperty=fullName> Sie den Typ in eine der generischen Auflistungen, die für Vererbung entworfen wurden.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel, es sei denn, die Assembly, die diese Warnung auslöst, ist keine wiederverwendbare Bibliothek. Beispielsweise wäre es sicher, diese Warnung in einer leistungsoptimierten Anwendung zu unterdrücken, bei der der Leistungsvorteil durch die Verwendung generischer Listen erzielt wurde.

## <a name="related-rules"></a>Verwandte Regeln
[CA1005: Übermäßige Parameter für generische Typen vermeiden](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

[CA1010: Sammlungen sollten eine generische Schnittstelle implementieren.](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000: Statische Member nicht in generischen Typen deklarieren](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1006: Generische Typen in Element Signaturen nicht Schachteln](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

[CA1004: Generische Methoden sollten Typparameter bereitstellen.](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

[CA1003: Generische Ereignishandlerinstanzen verwenden](../code-quality/ca1003-use-generic-event-handler-instances.md)

[CA1007: Generika ggf. verwenden](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>Siehe auch
[Generika](/dotnet/csharp/programming-guide/generics/index)