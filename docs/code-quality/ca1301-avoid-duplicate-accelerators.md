---
title: 'CA1301: Doppelte Zugriffstasten vermeiden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1301
- AvoidDuplicateAccelerators
helpviewer_keywords:
- CA1301
- AvoidDuplicateAccelerators
ms.assetid: 20570a00-864b-459c-a1fa-a6e9db5f1001
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 16cd44f00db13027d737b6a6b496877075ac6fa9
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922253"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301: Doppelte Zugriffstasten vermeiden.

|||
|-|-|
|TypeName|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|Kategorie|Microsoft.Globalization|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Ein Typ erweitert <xref:System.Windows.Forms.Control?displayProperty=fullName> und enthält zwei oder mehr Steuerelemente der obersten Ebene, die über identische Zugriffsschlüssel verfügen, die in einer Ressourcen Datei gespeichert werden.

## <a name="rule-description"></a>Regelbeschreibung

Eine Zugriffstaste, auch als Zugriffstaste bezeichnet, ermöglicht den Tastatur Zugriff auf ein Steuerelement mithilfe der **alt** -Taste. Wenn mehrere Steuerelemente denselben Zugriffsschlüssel aufweisen, ist das Verhalten des Zugriffsschlüssels nicht klar definiert. Möglicherweise ist der Benutzer nicht in der Lage, über die Zugriffstaste auf das beabsichtigte Steuerelement zuzugreifen, und ein anderes Steuerelement als das ist möglicherweise aktiviert.

Die aktuelle Implementierung dieser Regel ignoriert Menü Elemente. Menü Elemente im gleichen Untermenü dürfen jedoch nicht über identische Zugriffstasten verfügen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, definieren Sie eindeutige Zugriffsschlüssel für alle Steuerelemente.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt ein minimales Formular, das zwei Steuerelemente mit identischen Zugriffs Schlüsseln enthält. Die Schlüssel werden in einer Ressourcen Datei gespeichert, die nicht angezeigt wird. Ihre Werte werden jedoch in den auskommentierten `checkBox.Text` Zeilen angezeigt. Das Verhalten doppelter Acceleratoren kann durch Austauschen der `checkBox.Text` Zeilen mit ihren auskommentierten Entsprechungen überprüft werden. In diesem Fall wird in diesem Beispiel jedoch keine Warnung aus der Regel generiert.

[!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../code-quality/codesnippet/CSharp/ca1301-avoid-duplicate-accelerators_1.cs)]

## <a name="see-also"></a>Siehe auch

- <xref:System.Resources.ResourceManager?displayProperty=fullName>
- [Ressourcen in Desktop-Apps](/dotnet/framework/resources/index)