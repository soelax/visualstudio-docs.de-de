---
title: 'CA2223: Member sollten sich durch mehr als nur den Rückgabetyp unterscheiden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MembersShouldDifferByMoreThanReturnType
- CA2223
helpviewer_keywords:
- CA2223
- MembersShouldDifferByMoreThanReturnType
ms.assetid: eb326d9f-50d9-48cb-84be-d41c84a8fe09
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: de64e0271370a3cdcc6f0963dbf06925621b9b65
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920188"
---
# <a name="ca2223-members-should-differ-by-more-than-return-type"></a>CA2223: Member sollten sich durch mehr als nur den Rückgabetyp unterscheiden.

|||
|-|-|
|TypeName|MembersShouldDifferByMoreThanReturnType|
|CheckId|CA2223|
|Kategorie|Microsoft.Usage|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Zwei öffentliche oder geschützte Member haben Signaturen, die mit Ausnahme des Rückgabe Typs identisch sind.

## <a name="rule-description"></a>Regelbeschreibung
Obwohl das Common Language Runtime die Verwendung von Rückgabe Typen ermöglicht, um zwischen ansonsten identischen Membern zu unterscheiden, befindet sich dieses Feature nicht im Common Language Specification, und es ist auch kein gängiges Feature von .NET-Programmiersprachen. Wenn sich Elemente nur nach Rückgabetyp unterscheiden, unterscheiden Entwickler und Entwicklungs Tools möglicherweise nicht ordnungsgemäß zwischen Ihnen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, ändern Sie den Entwurf der Member so, dass Sie nur anhand ihrer Namen und Parametertypen eindeutig sind, oder machen Sie die Member nicht verfügbar.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt in der Microsoft Intermediate Language (MSIL) einen Typ, der gegen diese Regel verstößt. Beachten Sie, dass diese Regel nicht mithilfe C# von oder Visual Basic verletzt werden kann.

```
.namespace UsageLibrary
{
  .class public auto ansi beforefieldinit ReturnTypeTest
         extends [mscorlib]System.Object
  {
    .method public hidebysig instance int32
            AMethod(int32 x) cil managed
    {
      // Code size       6 (0x6)
      .maxstack  1
      .locals init (int32 V_0)
      IL_0000:  ldc.i4.0
      IL_0001:  stloc.0
      IL_0002:  br.s       IL_0004

      IL_0004:  ldloc.0
      IL_0005:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig instance string
            AMethod(int32 x) cil managed
    {
      // Code size       10 (0xa)
      .maxstack  1
      .locals init (string V_0)
      IL_0000:  ldstr      "test"
      IL_0005:  stloc.0
      IL_0006:  br.s       IL_0008

      IL_0008:  ldloc.0
      IL_0009:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig specialname rtspecialname
            instance void  .ctor() cil managed
    {
      // Code size       7 (0x7)
      .maxstack  1
      IL_0000:  ldarg.0
      IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
      IL_0006:  ret
    } // end of method ReturnTypeTest::.ctor

  } // end of class ReturnTypeTest

} // end of namespace UsageLibrary
```