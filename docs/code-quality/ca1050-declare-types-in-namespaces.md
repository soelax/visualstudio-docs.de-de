---
title: 'CA1050: Typen in Namespaces deklarieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1050
- DeclareTypesInNamespaces
helpviewer_keywords:
- DeclareTypesInNamespaces
- CA1050
ms.assetid: 1002748d-ac8d-404f-85dd-7a12d1ad3e05
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 869ff99243349ae01c63da0a7d9e6544761cbd39
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922503"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050: Typen in Namespaces deklarieren.

|||
|-|-|
|TypeName|DeclareTypesInNamespaces|
|CheckId|CA1050|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein öffentlicher oder geschützter Typ wird außerhalb des Gültigkeits Bereichs eines benannten Namespace definiert.

## <a name="rule-description"></a>Regelbeschreibung
Typen werden in Namespaces deklariert, um Namenskonflikte zu verhindern, und als Möglichkeit, verwandte Typen in einer Objekthierarchie zu organisieren. Typen, die sich außerhalb eines benannten Namespace befinden, befinden sich in einem globalen Namespace, auf den im Code nicht verwiesen werden kann.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, platzieren Sie den-Typ in einem Namespace.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Obwohl Sie eine Warnung nicht von dieser Regel unterdrücken müssen, ist dies sicher, wenn die Assembly nicht in Verbindung mit anderen Assemblys verwendet wird.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Bibliothek, die einen Typ aufweist, der fälschlicherweise außerhalb eines Namespaces deklariert wurde, und einen Typ, der denselben Namen aufweist, der in einem Namespace deklariert wurde.

[!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../code-quality/codesnippet/CSharp/ca1050-declare-types-in-namespaces_1.cs)]
[!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../code-quality/codesnippet/VisualBasic/ca1050-declare-types-in-namespaces_1.vb)]

## <a name="example"></a>Beispiel
Die folgende Anwendung verwendet die zuvor definierte Bibliothek. Beachten Sie, dass der Typ, der außerhalb eines Namespaces deklariert ist, `Test` erstellt wird, wenn der Name nicht durch einen Namespace qualifiziert ist. Beachten Sie außerdem, dass für `Test` den Zugriff `Goodspace`auf den-Typ in der Namespace Name erforderlich ist.

[!code-csharp[FxCop.Design.TestTypesLive#1](../code-quality/codesnippet/CSharp/ca1050-declare-types-in-namespaces_2.cs)]
[!code-vb[FxCop.Design.TestTypesLive#1](../code-quality/codesnippet/VisualBasic/ca1050-declare-types-in-namespaces_2.vb)]