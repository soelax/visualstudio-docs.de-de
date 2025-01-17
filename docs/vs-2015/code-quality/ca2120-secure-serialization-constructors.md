---
title: 'CA2120: Sichere Serialisierungskonstruktoren | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2120
- SecureSerializationConstructors
helpviewer_keywords:
- SecureSerializationConstructors
- CA2120
ms.assetid: e9989da1-55a0-43f8-9aa9-da86afae3b41
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ea70b7f9462e3195a78b915691a5069ebd6fe6aa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154359"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120: Sichere Serialisierungskonstruktoren.
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecureSerializationConstructors|
|CheckId|CA2120|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
 Der Typ implementiert die <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> -Schnittstelle ist nicht, einen Delegaten oder eine Schnittstelle, und wird in einer Assembly deklariert, die teilweise vertrauenswürdige Aufrufer zulässt. Der Typ verfügt über einen Konstruktor, akzeptiert eine <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> Objekt und ein <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> Objekt (die Signatur des Serialisierungskonstruktors). Dieser Konstruktor wird nicht durch eine sicherheitsüberprüfung gesichert, aber eine oder mehrere der normalen Konstruktoren des Typs gesichert wird.

## <a name="rule-description"></a>Regelbeschreibung
 Diese Regel gilt für Typen, die benutzerdefinierte Serialisierung unterstützen. Ein Typ unterstützt die benutzerdefinierte Serialisierung, wenn er implementiert die <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> Schnittstelle. Der Serialisierungskonstruktor ist erforderlich und wird verwendet, um deserialisiert und erneut erstellen Objekte, die mit serialisiert wurden die <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> Methode. Da der Serialisierungskonstruktor weist und Objekte initialisiert werden, müssen auch sicherheitsüberprüfungen, die auf normalen Konstruktoren vorhanden sind auf den Serialisierungskonstruktor vorhanden sein. Wenn Sie diese Regel verletzen, können Aufrufer, die andernfalls keine Instanz erstellt werden konnte den Serialisierungskonstruktor dazu.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
 Um einen Verstoß gegen diese Regel zu beheben, schützen Sie den Serialisierungskonstruktor mit sicherheitsanforderungen, die identisch mit den anderen Konstruktoren geschützt sind.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
 Unterdrücken Sie keinen Verstoß gegen die Regel.

## <a name="example"></a>Beispiel
 Das folgende Beispiel zeigt einen Typ, der gegen die Regel verstößt.

 [!code-csharp[FxCop.Security.SerialCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SerialCtors/cs/FxCop.Security.SerialCtors.cs#1)]

## <a name="related-rules"></a>Verwandte Regeln
 [CA2229: Serialisierungskonstruktoren implementieren](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2237: Markieren von ISerializable-Typen mit SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Siehe auch
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>
