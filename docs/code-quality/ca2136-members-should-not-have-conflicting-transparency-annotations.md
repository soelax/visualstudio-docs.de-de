---
title: 'CA2136: Member dürfen keine miteinander in Konflikt stehenden Transparenzanmerkungen aufweisen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2127
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2136
helpviewer_keywords:
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2127
ms.assetid: ff5a1d18-7c52-4da5-8990-60be83a8ea81
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1dcef8fbfd61b8cd8c946f76d6fcb93dc46f1654
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920630"
---
# <a name="ca2136-members-should-not-have-conflicting-transparency-annotations"></a>CA2136: Member dürfen keine miteinander in Konflikt stehenden Transparenzanmerkungen aufweisen.

|||
|-|-|
|TypeName|TransparencyAnnotationsShouldNotConflict|
|CheckId|CA2136|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Diese Regel wird ausgelöst, wenn ein Typmember mit einem <xref:System.Security> Sicherheits Attribut markiert ist, das eine andere Transparenz aufweist als das Sicherheits Attribut eines Containers des Members.

## <a name="rule-description"></a>Regelbeschreibung
Transparenzattribute werden von größeren Codeelementen bis hin zu kleineren Elementen übernommen. Die Transparenzattribute von Codeelementen mit größerem Umfang haben Vorrang vor Transparenzattributen von Codeelementen, die im ersten Element enthalten sind. Eine-Klasse, die mit dem <xref:System.Security.SecurityCriticalAttribute> -Attribut markiert ist, kann z. b. keine Methode enthalten, die mit dem <xref:System.Security.SecuritySafeCriticalAttribute> -Attribut markiert ist.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um diese Verletzung zu beheben, entfernen Sie das Sicherheits Attribut aus dem Code Element, das einen niedrigeren Gültigkeitsbereich aufweist, oder ändern Sie das zugehörige Attribut, sodass es mit dem enthaltenden Code Element identisch ist.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Warnungen von dieser Regel nicht unterdrücken.

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird eine-Methode mit dem <xref:System.Security.SecuritySafeCriticalAttribute> -Attribut gekennzeichnet und ist ein Member einer Klasse, die mit dem <xref:System.Security.SecurityCriticalAttribute> -Attribut markiert ist. Das Sicherheits sichere Attribut sollte entfernt werden.

[!code-csharp[FxCop.Security.CA2136.TransparencyAnnotationsShouldNotConflict#1](../code-quality/codesnippet/CSharp/ca2136-members-should-not-have-conflicting-transparency-annotations_1.cs)]