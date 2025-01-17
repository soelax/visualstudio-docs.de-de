---
title: 'CA1408: AutoDual ClassInterfaceType nicht verwenden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: b79483e8703ea297634d0d81d5449c09b58c9fb7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921984"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408: AutoDual ClassInterfaceType nicht verwenden.

|||
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|Kategorie|Microsoft.Interoperability|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein Component Object Model sichtbarer Typ (com) ist mit dem <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> -Attribut gekennzeichnet, `AutoDual` das auf <xref:System.Runtime.InteropServices.ClassInterfaceType>den Wert von festgelegt ist.

## <a name="rule-description"></a>Regelbeschreibung
Typen, die eine duale Schnittstelle verwenden, ermöglichen Clients die Bindung an ein bestimmtes Schnittstellenlayout. Änderungen an einer zukünftigen Version des Layouts des Typs oder eines Basistyps führen zur Aufhebung der Verbindung zu COM-Clients, die eine Bindung zu der Schnittstelle haben. Wenn das <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> -Attribut nicht angegeben wird, wird standardmäßig eine Dispatch-Schnittstelle verwendet.

Sofern nicht anders gekennzeichnet, sind alle öffentlichen nicht generischen Typen für com sichtbar. alle nicht öffentlichen und generischen Typen sind für com nicht sichtbar.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, ändern Sie den Wert <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> des-Attributs in <xref:System.Runtime.InteropServices.ClassInterfaceType> den `None` Wert von, und definieren Sie die-Schnittstelle explizit.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel, es sei denn, es ist sicher, dass sich das Layout des Typs und der zugehörigen Basis Typen in einer zukünftigen Version nicht ändern.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Klasse, die gegen die Regel verstößt, und eine erneute Deklaration der-Klasse, um eine explizite-Schnittstelle zu verwenden.

[!code-csharp[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/CSharp/ca1408-do-not-use-autodual-classinterfacetype_1.cs)]
[!code-vb[FxCop.Interoperability.AutoDual#1](../code-quality/codesnippet/VisualBasic/ca1408-do-not-use-autodual-classinterfacetype_1.vb)]

## <a name="related-rules"></a>Verwandte Regeln
[CA1403: Automatische Layouttypen sollten nicht für com sichtbar sein](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

[CA1412: ComSource-Schnittstellen als IDispatch markieren](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>Siehe auch

- [Qualifizieren von .NET-Typen für die Interoperation](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [Interoperabilität mit nicht verwaltetem Code](/dotnet/framework/interop/index)