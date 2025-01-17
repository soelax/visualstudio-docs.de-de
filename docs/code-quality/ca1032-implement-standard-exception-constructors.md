---
title: 'CA1032: Standardausnahmekonstruktoren implementieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad062154b8213d021c8c265aaf287d3a9335d0e4
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922882"
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032: Standardausnahmekonstruktoren implementieren.

|||
|-|-|
|TypeName|ImplementStandardExceptionConstructors|
|CheckId|CA1032|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache

Ein Typ wird <xref:System.Exception?displayProperty=fullName> erweitert, deklariert jedoch nicht alle erforderlichen Konstruktoren.

## <a name="rule-description"></a>Regelbeschreibung

Ausnahme Typen müssen die folgenden drei Konstruktoren implementieren:

- Public "netwexception ()"

- Public "netwexception" (Zeichenfolge)

- Public "netwexception" (String, Exception)

Wenn Sie im Gegensatz zu [Roslyn-basierten FxCop-Analyzern](../code-quality/roslyn-analyzers-overview.md)die Legacy-und die statische Code Analyse von FxCop ausführen, führt das Fehlen eines vierten Konstruktors ebenfalls zu einem Verstoß:

- Protected or private, "netwexception" (SerializationInfo, StreamingContext)

Falls nicht der vollständige Satz von Konstruktoren angegeben wird, wird eine ordnungsgemäße Behandlung von Ausnahmen unter Umständen erschwert. Beispielsweise wird der Konstruktor mit der Signatur `NewException(string, Exception)` verwendet, um Ausnahmen zu erstellen, die durch andere Ausnahmen verursacht werden. Ohne diesen Konstruktor können Sie keine Instanz Ihrer benutzerdefinierten Ausnahme erstellen und auslösen, die eine innere (geschachtelte) Ausnahme enthält. Dies ist der Zweck, den verwalteter Code in einer solchen Situation haben sollte.

Die ersten drei Ausnahmekonstruktoren sind gemäß Konvention öffentlich. Der vierte Konstruktor ist in nicht versiegelten Klassen und privat in versiegelten Klassen geschützt. Weitere Informationen finden [Sie unter CA2229: Implementieren Sie Serialisierungskonstruktoren](../code-quality/ca2229-implement-serialization-constructors.md).

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen

Um einen Verstoß gegen diese Regel zu beheben, fügen Sie der Ausnahme die fehlenden Konstruktoren hinzu, und stellen Sie sicher, dass Sie über die richtige Barrierefreiheit verfügen.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?

Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn die Verletzung durch die Verwendung einer anderen Zugriffsebene für die öffentlichen Konstruktoren verursacht wird. Außerdem ist es in Ordnung, die Warnung für den `NewException(SerializationInfo, StreamingContext)` Konstruktor zu unterdrücken, wenn Sie eine portable Klassenbibliothek (Portable Class Library, PCL) entwickeln.

## <a name="example"></a>Beispiel

Das folgende Beispiel enthält einen Ausnahmetyp, der gegen diese Regel verstößt, und einen Ausnahmetyp, der ordnungsgemäß implementiert ist.

[!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../code-quality/codesnippet/CSharp/ca1032-implement-standard-exception-constructors_1.cs)]

## <a name="see-also"></a>Siehe auch

[CA2229: Serialisierungskonstruktoren implementieren](../code-quality/ca2229-implement-serialization-constructors.md)