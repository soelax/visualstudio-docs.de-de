---
title: 'CA1903: Nur API aus Zielframework verwenden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UseOnlyAPIFromTargetedFramework
- CA1903
helpviewer_keywords:
- UseOnlyApiFromTargetedFramework
- CA1903
ms.assetid: efdb5cc7-bbd8-4fa7-9fff-02b91e59350e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7d972198898dd1a4cafa5280c129db38bb3e4982
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921287"
---
# <a name="ca1903-use-only-api-from-targeted-framework"></a>CA1903: Nur API aus Zielframework verwenden.

|||
|-|-|
|TypeName|UseOnlyApiFromTargetedFramework|
|CheckId|CA1903|
|Kategorie|Microsoft.Portability|
|Unterbrechende Änderung|Unterbrechen: Wenn Sie für die Signatur eines extern sichtbaren Members oder Typs ausgelöst werden.<br /><br /> Nicht unterbrechend: beim Auslösen im Text einer Methode.|

## <a name="cause"></a>Ursache
Ein Member oder Typ verwendet einen Member oder Typ, der in einem Service Pack eingeführt wurde, das nicht im Ziel Framework des Projekts enthalten war.

## <a name="rule-description"></a>Regelbeschreibung
In .NET Framework 2,0 Service Pack 1 und 2, .NET Framework 3,0 Service Pack 1 und 2 und .NET Framework 3,5 Service Pack 1 sind neue Member und Typen enthalten. Projekte, die auf die Hauptversionen des .NET Framework abzielen, können unbeabsichtigt Abhängigkeiten von diesen neuen APIs annehmen. Um diese Abhängigkeit zu verhindern, wird diese Regel für Verwendungen von neuen Membern und Typen ausgelöst, die nicht standardmäßig mit dem Ziel Framework des Projekts eingeschlossen wurden.

**Ziel Framework-und Service Pack-Abhängigkeiten**

|||
|-|-|
|Wenn das Ziel Framework|Ausgelöst bei der Verwendung von Membern, die in eingeführt wurden|
|.NET Framework 2.0|.NET Framework 2,0 SP1, .NET Framework 2,0 SP2|
|.NET Framework 3.0|.NET Framework 2,0 SP1, .NET Framework 2,0 SP2, .NET Framework 3,0 SP1, .NET Framework 3,0 SP2|
|.NET Framework 3.5|.NET Framework 3.5 SP1|
|.NET Framework 4|N/V|

Informationen zum Ändern des Ziel-Frameworks eines [Projekts finden Sie unter Gewusst wie: Ausrichten auf eine Version von .NET](../ide/how-to-target-a-version-of-the-dotnet-framework.md).

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Entfernen Sie alle Verwendungen des neuen Members oder Typs, um die Abhängigkeit des Service Pack zu entfernen. Wenn es sich um eine absichtliche Abhängigkeit handelt, sollten Sie entweder die Warnung unterdrücken oder diese Regel deaktivieren.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung aus dieser Regel, wenn dies keine absichtliche Abhängigkeit vom angegebenen Service Pack war. In dieser Situation kann die Anwendung möglicherweise nicht auf Systemen ausgeführt werden, auf denen dieses Service Pack nicht installiert ist. Unterdrücken Sie die Warnung, oder deaktivieren Sie diese Regel, wenn es sich um eine absichtliche Abhängigkeit handelt.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Klasse, die den Typ DateTimeOffset verwendet, der nur in .NET 2,0 Service Pack 1 verfügbar ist. In diesem Beispiel muss .NET Framework 2,0 in der Dropdown Liste Ziel Framework in den Projekteigenschaften ausgewählt worden sein.

[!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework#1](../code-quality/codesnippet/CSharp/ca1903-use-only-api-from-targeted-framework_1.cs)]

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird die zuvor beschriebene Verletzung behoben, indem die Verwendungen des DateTimeOffset-Typs durch den DateTime-Typ ersetzt werden.

[!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework2#1](../code-quality/codesnippet/CSharp/ca1903-use-only-api-from-targeted-framework_2.cs)]

## <a name="see-also"></a>Siehe auch

- [Portability Warnings](../code-quality/portability-warnings.md)
- [Übersicht über Frameworkziele](../ide/visual-studio-multi-targeting-overview.md)