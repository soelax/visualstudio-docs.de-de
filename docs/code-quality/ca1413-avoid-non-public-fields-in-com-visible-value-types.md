---
title: 'CA1413: Nicht öffentliche Felder in für COM sichtbaren Werttypen vermeiden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
helpviewer_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
ms.assetid: 1352e7eb-fefc-4239-8847-25edc7804a54
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 3eb216af1b6cd742aff83b248b6752adea292345
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921838"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413: Nicht öffentliche Felder in für COM sichtbaren Werttypen vermeiden.

|||
|-|-|
|TypeName|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|Kategorie|Microsoft.Interoperability|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein Werttyp, der speziell für Component Object Model (com) als sichtbar gekennzeichnet ist, deklariert ein nicht öffentliches Instanzfeld.

## <a name="rule-description"></a>Regelbeschreibung
Nicht öffentliche Instanzenfelder von COM-sichtbaren Werttypen sind für COM-Clients sichtbar. Überprüfen Sie den Inhalt des Felds auf Informationen, die nicht verfügbar gemacht werden sollen oder die einen unbeabsichtigten Entwurf oder sicherheitseffekt haben.

Standardmäßig sind alle öffentlichen Werttypen für com sichtbar. Um falsch positive Ergebnisse zu reduzieren, erfordert diese Regel jedoch, dass die COM-Sichtbarkeit des Typs explizit angegeben wird. Die <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> enthaltende Assembly muss mit dem auf festgelegten festgelegt werden, `false` und der Typ muss <xref:System.Runtime.InteropServices.ComVisibleAttribute> mit dem `true`auf festgelegten Wert gekennzeichnet werden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben und das Feld zu verbergen, ändern Sie den Werttyp in einen Verweistyp <xref:System.Runtime.InteropServices.ComVisibleAttribute> , oder entfernen Sie das Attribut aus dem Typ.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn die öffentliche verfügbar machung des Felds akzeptabel ist.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt einen Typ, der gegen die Regel verstößt.

[!code-csharp[FxCop.Interoperability.NonpublicField#1](../code-quality/codesnippet/CSharp/ca1413-avoid-non-public-fields-in-com-visible-value-types_1.cs)]
[!code-vb[FxCop.Interoperability.NonpublicField#1](../code-quality/codesnippet/VisualBasic/ca1413-avoid-non-public-fields-in-com-visible-value-types_1.vb)]

## <a name="related-rules"></a>Verwandte Regeln
[CA1407: Statische Member in für COM sichtbaren Typen vermeiden](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

[CA1017: Assemblys mit ComVisibleAttribute markieren](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Siehe auch

- [Interoperabilität mit nicht verwaltetem Code](/dotnet/framework/interop/index)
- [Qualifizieren von .NET-Typen für die Interoperation](/dotnet/framework/interop/qualifying-net-types-for-interoperation)