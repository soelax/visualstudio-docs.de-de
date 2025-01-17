---
title: 'CA1023: Indexer sollten nicht mehrdimensional sein.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 08a45219eb2fceeaa9c58a140990ea577c941ff7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923040"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023: Indexer sollten nicht mehrdimensional sein.

|||
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein öffentlicher oder geschützter Typ enthält einen öffentlichen oder geschützten Indexer, der mehr als einen Index verwendet.

## <a name="rule-description"></a>Regelbeschreibung
Indexer, d. h. indizierte Eigenschaften, sollten einen einzelnen Index verwenden. Mehrdimensionale Indexer können die Verwendbarkeit der Bibliothek erheblich verringern. Wenn der Entwurf mehrere Indizes erfordert, überdenken Sie, ob der Typ einen logischen Datenspeicher darstellt. Wenn dies nicht der gibt, verwenden Sie eine-Methode.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, ändern Sie den Entwurf so, dass er eine Ganzzahl oder einen Zeichen folgen Index verwendet, oder verwenden Sie eine Methode anstelle des Indexers.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrückt eine Warnung aus dieser Regel nur, nachdem sorgfältig geprüft wurde, dass es sich nicht um einen Standardindexer handelt.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt einen-Typ `DayOfWeek03`mit einem mehrdimensionalen Indexer, der gegen die Regel verstößt. Der Indexer kann als Konvertierungstyp angesehen werden und wird daher besser als-Methode verfügbar gemacht. Der Typ wird in `RedesignedDayOfWeek03` umgestaltet, um die Regel zu erfüllen.

[!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
[!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
[!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## <a name="related-rules"></a>Verwandte Regeln
[CA1043: Ganzzahliges Argument oder Zeichen folgen Argument für Indexer verwenden](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

[CA1024: Verwenden Sie gegebenenfalls Eigenschaften](../code-quality/ca1024-use-properties-where-appropriate.md)