---
title: 'CA1013: Gleichheitsoperator beim Überladen von Addition und Subtraktion überladen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8c82e7303ea4016974be04c3d8745cb2011017f0
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923160"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013: Gleichheitsoperator beim Überladen von Addition und Subtraktion überladen.

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Ein öffentlicher oder geschützter Typ implementiert den Additions- oder Subtraktionsoperator, ohne den Gleichheitsoperator zu implementieren.

## <a name="rule-description"></a>Regelbeschreibung
Wenn Instanzen eines Typs mithilfe von Vorgängen wie Addition und Subtraktion kombiniert werden können, sollten Sie fast immer Gleichheit definieren, um für `true` zwei Instanzen zurückzugeben, die dieselben Werte aufweisen.

Der Standard Gleichheits Operator kann nicht in einer überladenen Implementierung des Gleichheits Operators verwendet werden. Dies führt zu einem Stapelüberlauf. Um den Gleichheits Operator zu implementieren, verwenden Sie die Object. gleich-Methode in der Implementierung. Weitere Informationen finden Sie im folgenden Beispiel.

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, implementieren Sie den Gleichheits Operator, sodass er mathematisch mit den Additions-und Subtraktions Operatoren übereinstimmt.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn die Standard Implementierung des Gleichheits Operators das richtige Verhalten für den Typ bereitstellt.

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird ein Typ (`BadAddableType`) definiert, der gegen diese Regel verstößt. Dieser Typ sollte den Gleichheits Operator implementieren, damit zwei Instanzen, die dieselben Feldwerte `true` aufweisen, auf Gleichheit überprüft werden. Der Typ `GoodAddableType` zeigt die korrigierte Implementierung. Beachten Sie, dass dieser Typ auch den Ungleichheits Operator und <xref:System.Object.Equals%2A> über schreibungen implementiert, um andere Regeln zu erfüllen. Eine komplette Implementierung würde ebenfalls implementieren <xref:System.Object.GetHashCode%2A>.

[!code-csharp[FxCop.Design.AddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_1.cs)]

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird auf Gleichheit getestet, indem Instanzen der Typen verwendet werden, die zuvor in diesem Thema definiert wurden, um das standardmäßige und korrekte Verhalten für den Gleichheits Operator zu veranschaulichen.

[!code-csharp[FxCop.Design.TestAddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_2.cs)]

Dieses Beispiel erzeugt die folgende Ausgabe:

```txt
Bad type:  {2,2} {2,2} are equal? No
Good type: {3,3} {3,3} are equal? Yes
Good type: {3,3} {3,3} are == ?   Yes
Bad type:  {2,2} {9,9} are equal? No
Good type: {3,3} {9,9} are == ?   No
```

## <a name="see-also"></a>Siehe auch

- [Gleichheitsoperatoren](/dotnet/standard/design-guidelines/equality-operators)