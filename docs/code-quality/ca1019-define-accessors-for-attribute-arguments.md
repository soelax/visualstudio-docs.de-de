---
title: 'CA1019: Accessoren für Attributargumente definieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
helpviewer_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8422427997db291aa24bc8a8bacfdc59abe35998
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923079"
---
# <a name="ca1019-define-accessors-for-attribute-arguments"></a>CA1019: Accessoren für Attributargumente definieren.

|||
|-|-|
|TypeName|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Im Konstruktor definiert ein Attribut Argumente, die keine entsprechenden Eigenschaften haben.

## <a name="rule-description"></a>Regelbeschreibung
Attribute können obligatorische Argumente definieren, die angegeben werden müssen, wenn das Attribut auf ein Ziel angewendet wird. Diese Argumente werden auch als positionelle Argumente bezeichnet, da sie bei Attributkonstruktoren als positionelle Parameter angegeben werden. Für jedes obligatorische Argument muss das Attribut außerdem eine entsprechende schreibgeschützte Eigenschaft enthalten, damit der Wert des Arguments zur Ausführungszeit abgerufen werden kann. Diese Regel überprüft, ob Sie die entsprechende Eigenschaft für jeden Konstruktorparameter definiert haben.

Attribute können auch optionale Argumente definieren, die auch als benannte Argumente bezeichnet werden. Diese Argumente werden bei Attributkonstruktoren über ihren Namen angegeben und sollten über eine entsprechende Lese-Schreib-Eigenschaft verfügen.

Bei obligatorischen und optionalen Argumenten sollten die entsprechenden Eigenschaften und Konstruktorparameter denselben Namen, aber eine unterschiedliche groß-und Kleinschreibung verwenden. Eigenschaften verwenden die Pascal-Schreibweise, und Parameter verwenden Kamel Schreibweise.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, fügen Sie eine schreibgeschützte Eigenschaft für jeden Konstruktorparameter hinzu, der nicht über einen verfügt.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie eine Warnung aus dieser Regel, wenn Sie nicht möchten, dass der Wert des obligatorischen Arguments abgerufen werden kann.

## <a name="custom-attributes-example"></a>Beispiel für benutzerdefinierte Attribute

Das folgende Beispiel zeigt zwei Attribute, die einen obligatorischen (positionellen) Parameter definieren. Die erste Implementierung des-Attributs ist falsch definiert. Die zweite Implementierung ist richtig.

[!code-csharp[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_1.cs)]
[!code-vb[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/VisualBasic/ca1019-define-accessors-for-attribute-arguments_1.vb)]

## <a name="positional-and-named-arguments"></a>Positions-und benannte Argumente

Positions-und benannte Argumente machen es für Consumer Ihrer Bibliothek klar, welche Argumente für das Attribut obligatorisch sind und welche Argumente optional sind.

Das folgende Beispiel zeigt eine Implementierung eines Attributs, das sowohl positionelle als auch benannte Argumente hat:

[!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_2.cs)]

Im folgenden Beispiel wird gezeigt, wie Sie das benutzerdefinierte Attribut auf zwei Eigenschaften anwenden:

[!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_3.cs)]

## <a name="related-rules"></a>Verwandte Regeln
[CA1813: Nicht versiegelte Attribute vermeiden](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>Siehe auch
[Attribute](/dotnet/standard/design-guidelines/attributes)