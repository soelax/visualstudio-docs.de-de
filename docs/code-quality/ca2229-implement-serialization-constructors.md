---
title: 'CA2229: Serialisierungskonstruktoren implementieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2229
- ImplementSerializationConstructors
helpviewer_keywords:
- CA2229
- ImplementSerializationConstructors
ms.assetid: 8e04d5fe-dfad-445a-972e-0648324fac45
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 11dfa98bb348f874a2774454cc465fb80cb71750
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920165"
---
# <a name="ca2229-implement-serialization-constructors"></a>CA2229: Serialisierungskonstruktoren implementieren.

|||
|-|-|
|TypeName|ImplementSerializationConstructors|
|CheckId|CA2229|
|Kategorie|Microsoft.Usage|
|Unterbrechende Änderung|Nicht unterbrechende Änderung|

## <a name="cause"></a>Ursache
Der-Typ implementiert <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> die-Schnittstelle, ist kein Delegat oder eine Schnittstelle, und eine der folgenden Bedingungen ist true:

- Der-Typ verfügt über keinen Konstruktor, der ein <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> -Objekt und <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> ein-Objekt (die Signatur des Serialisierungskonstruktors) annimmt.

- Der Typ ist nicht versiegelt, und der Zugriffsmodifizierer für den Serialisierungskonstruktor ist nicht geschützt (Family).

- Der Typ ist versiegelt, und der Zugriffsmodifizierer für den Serialisierungskonstruktor ist nicht privat.

## <a name="rule-description"></a>Regelbeschreibung
Diese Regel ist für Typen relevant, die die benutzerdefinierte Serialisierung unterstützen. Ein Typ unterstützt die benutzerdefinierte Serialisierung, <xref:System.Runtime.Serialization.ISerializable> wenn die-Schnittstelle implementiert wird. Der Serialisierungskonstruktor ist erforderlich, um Objekte zu deserialisieren oder neu zu erstellen, die mit der <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> -Methode serialisiert wurden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, implementieren Sie den Serialisierungskonstruktor. Definieren Sie den Konstruktor bei einer versiegelten Klasse als privaten Konstruktor. Definieren Sie ihn andernfalls als geschützten Konstruktor.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keinen Verstoß gegen die Regel. Der Typ ist nicht deserialisierbar und funktioniert in vielen Szenarios nicht.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt einen Typ, der die Regel erfüllt.

[!code-csharp[FxCop.Usage.ISerializableCtor#1](../code-quality/codesnippet/CSharp/ca2229-implement-serialization-constructors_1.cs)]

## <a name="related-rules"></a>Verwandte Regeln
[CA2237: Markieren von iserialisierbaren Typen mit SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Siehe auch

- <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>
- <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
- <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>