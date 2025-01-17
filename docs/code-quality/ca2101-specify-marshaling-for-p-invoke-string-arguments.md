---
title: 'CA2101: Marshalling für P/Invoke-Zeichenfolgenargumente festlegen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1eb4c2535060f9a110d149e88ac2532e6ad1412
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921101"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: Marshalling für P/Invoke-Zeichenfolgenargumente festlegen.

|||
|-|-|
|TypeName|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|Kategorie|Microsoft.Globalization|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Ein Platt Form Aufruf-Member ermöglicht teilweise vertrauenswürdigen Aufrufern, verfügt über einen Zeichen folgen Parameter und führt die Zeichenfolge nicht explizit aus.

## <a name="rule-description"></a>Regelbeschreibung
Wenn Sie von Unicode in ANSI konvertieren, ist es möglich, dass nicht alle Unicode-Zeichen in einer bestimmten ANSI-Codepage dargestellt werden können. Die Zuordnung mit einer *optimalen Anpassung* versucht, dieses Problem zu lösen, indem ein Zeichen für das Zeichen ersetzt wird, das nicht dargestellt werden kann. Die Verwendung dieser Funktion kann ein potenzielles Sicherheitsrisiko darstellen, da Sie das gewählte Zeichen nicht steuern können. Beispielsweise könnte bösartiger Code absichtlich eine Unicode-Zeichenfolge erstellen, die Zeichen enthält, die nicht in einer bestimmten Codepage gefunden werden, die in Sonderzeichen für das Dateisystem konvertiert werden, z. b. "..". oder "/". Beachten Sie auch, dass Sicherheitsüberprüfungen für Sonderzeichen häufig auftreten, bevor die Zeichenfolge in ANSI konvertiert wird.

Die Zuordnung mit der optimalen Anpassung ist die Standardeinstellung für die nicht verwaltete Konvertierung (WChar zu MB). Wenn Sie die Zuordnung mit der optimalen Anpassung nicht explizit deaktivieren, kann Ihr Code aufgrund dieses Problems ein Sicherheitsrisiko darstellen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, müssen Sie Zeichen folgen Datentypen explizit Mars Hallen.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Methode, die gegen diese Regel verstößt, und zeigt dann, wie Sie die Verletzung beheben.

[!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../code-quality/codesnippet/CSharp/ca2101-specify-marshaling-for-p-invoke-string-arguments_1.cs)]