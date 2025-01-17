---
title: 'CA1034: Geschachtelte Typen sollten nicht sichtbar sein.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a086ad80bd13fb18f866769db34d72cae3e67496
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922866"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034: Geschachtelte Typen sollten nicht sichtbar sein.

|||
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache

Ein extern sichtbarer Typ enthält eine extern sichtbare Typdeklaration. Von dieser Regel ausgenommen sind die von dieser Regel ausgefallenen Enumerationen und geschützten Typen.

## <a name="rule-description"></a>Regelbeschreibung
Ein geschachtelter Typ ist ein Typ, der innerhalb des Gültigkeits Bereichs eines anderen Typs deklariert wird. Bei der Einkapselung von privaten Implementierungsdetails des enthaltenden Typs sind die Typen von Typen nützlich. Bei dieser Verwendungsart sollten geschachtelte Typen nicht extern sichtbar sein.

Verwenden Sie keine extern sichtbaren gruppierten Typen für die logische Gruppierung oder, um Namenskonflikte zu vermeiden. Verwenden Sie stattdessen Namespaces.

Zu den Typen der Member gehört das Konzept der Member-Barrierefreiheit, die einige Programmierer nicht eindeutig verstehen.

Geschützte Typen können in vorklassen und in untergeordneten Typen in Szenarios für die vorab Anpassung verwendet werden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Wenn Sie nicht beabsichtigen, den Typ extern sichtbar zu machen, ändern Sie den Zugriff des Typs. Andernfalls entfernen Sie den vom übergeordneten Typ. Wenn der Zweck der Schachtelung darin besteht, den geschachtelten Typ zu kategorisieren, verwenden Sie stattdessen einen Namespace, um die Hierarchie zu erstellen.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt einen Typ, der gegen die Regel verstößt.

[!code-cpp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CPP/ca1034-nested-types-should-not-be-visible_1.cpp)]
[!code-csharp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CSharp/ca1034-nested-types-should-not-be-visible_1.cs)]
[!code-vb[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/VisualBasic/ca1034-nested-types-should-not-be-visible_1.vb)]