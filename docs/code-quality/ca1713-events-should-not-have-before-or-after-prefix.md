---
title: 'CA1713: Ereignisse sollten kein Before- oder After-Präfix aufweisen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EventsShouldNotHaveBeforeOrAfterPrefix
- CA1713
helpviewer_keywords:
- CA1713
- EventsShouldNotHaveBeforeOrAfterPrefix
ms.assetid: 855772a4-aa9e-410b-88c1-c5fba1ca63da
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee39ffbfd2e73a14fd42d574cef92a24784d1ad4
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921671"
---
# <a name="ca1713-events-should-not-have-before-or-after-prefix"></a>CA1713: Ereignisse sollten kein Before- oder After-Präfix aufweisen.

|||
|-|-|
|TypeName|EventsShouldNotHaveBeforeOrAfterPrefix|
|CheckId|CA1713|
|Kategorie|Microsoft.Naming|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Der Name eines Ereignisses beginnt mit ' before ' oder ' After '.

## <a name="rule-description"></a>Regelbeschreibung
Ereignis Namen sollten die Aktion beschreiben, durch die das Ereignis ausgelöst wird. Um verwandte Ereignisse zu benennen, die in einer bestimmten Reihenfolge ausgelöst werden, verwenden Sie die Gegenwarts- oder Vergangenheitsform, um ihre relative Position in der Aktionsfolge anzugeben. Wenn Sie z. b. ein Ereignispaar benennen, das beim Schließen einer Ressource ausgelöst wird, können Sie es als "Closing" und "Closed" anstelle von "BeforeClose" und "AfterClose" benennen.

Durch Benennungskonventionen erhalten Bibliotheken, die auf die Common Language Runtime abzielen, ein einheitliches Erscheinungsbild. Dadurch wird der Lernaufwand für neue Softwarebibliotheken verringert. Zudem wird das Kundenvertrauen dahingehend gestärkt, dass die Bibliothek von einem erfahrenen Entwickler für verwalteten Code erstellt wurde.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Entfernen Sie das Präfix aus dem Ereignis Namen, und ändern Sie ggf. den Namen so, dass er das vorhanden sein oder den letzten verstrichen eines Verbs verwendet

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.