---
title: 'CA1901: Deklarationen von P/Invoke müssen portabel sein.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
helpviewer_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
ms.assetid: 90361812-55ca-47f7-bce9-b8775d3b8803
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4a45b7061ae9d183ec7ee02a3b733ee9340b3689
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921302"
---
# <a name="ca1901-pinvoke-declarations-should-be-portable"></a>CA1901: Deklarationen von P/Invoke müssen portabel sein.

|||
|-|-|
|TypeName|PInvokeDeclarationsShouldBePortable|
|CheckId|CA1901|
|Kategorie|Microsoft.Portability|
|Unterbrechende Änderung|Unterbrechung: Wenn P/aufrufen außerhalb der Assembly sichtbar ist. Nicht unterbrechend: Wenn der P/Aufruf außerhalb der Assembly nicht sichtbar ist.|

## <a name="cause"></a>Ursache
Diese Regel wertet die Größe der einzelnen Parameter und den Rückgabewert von P/aufrufen aus und überprüft, ob ihre Größe beim Mars Hallen an nicht verwalteten Code auf 32-Bit-und 64-Bit-Plattformen korrekt ist. Der häufigste Verstoß gegen diese Regel besteht darin, eine ganze Zahl mit fester Größe zu übergeben, bei der eine Platt Form abhängige Variable mit Zeiger Größe erforderlich ist.

## <a name="rule-description"></a>Regelbeschreibung
Beide der folgenden Szenarien verstoßen gegen diese Regel:

- Der Rückgabewert oder-Parameter wird als ganze Zahl mit fester Größe typisiert, wenn er als `IntPtr`typisiert werden soll.

- Der Rückgabewert oder-Parameter wird als `IntPtr` typisiert, wenn er als Ganzzahl mit fester Größe typisiert werden soll.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Sie können diese Verletzung beheben, indem `IntPtr` Sie `UIntPtr` oder verwenden, um Handles `Int32` anstelle `UInt32`von oder darzustellen.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Sie sollten diese Warnung nicht unterdrücken.

## <a name="example"></a>Beispiel
Das folgende Beispiel veranschaulicht einen Verstoß gegen diese Regel.

```csharp
internal class NativeMethods
{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, IntPtr nIconIndex);
}
```

In diesem Beispiel wird der `nIconIndex` -Parameter `IntPtr`als deklariert, d. h. bei einer 32-Bit-Plattform auf einer-Bit-Plattform und bei einer 64-Bit-Plattform auf 8 Byte Breite. In der folgenden nicht verwalteten Deklaration sehen Sie, dass `nIconIndex` eine 4-Byte-Ganzzahl ohne Vorzeichen auf allen Plattformen ist.

```csharp
HICON ExtractIcon(HINSTANCE hInst, LPCTSTR lpszExeFileName,
    UINT nIconIndex);
```

## <a name="example"></a>Beispiel
Ändern Sie die Deklaration wie folgt, um die Verletzung zu beheben:

```csharp
internal class NativeMethods{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, uint nIconIndex);
}
```

## <a name="see-also"></a>Siehe auch
[Portability Warnings](../code-quality/portability-warnings.md)