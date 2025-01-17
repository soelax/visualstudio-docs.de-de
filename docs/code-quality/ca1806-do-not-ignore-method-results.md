---
title: 'CA1806: Methodenergebnisse nicht ignorieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1806
- DoNotIgnoreMethodResults
helpviewer_keywords:
- CA1806
- DoNotIgnoreMethodResults
ms.assetid: fd805687-0817-481e-804e-b62cfb3b1076
author: gewarren
ms.author: gewarren
dev_langs:
- CPP
- CSharp
- VB
manager: jillfra
ms.openlocfilehash: 2e68fb6b4c40c165a09ae2631a2ad0a64bf52fbc
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921552"
---
# <a name="ca1806-do-not-ignore-method-results"></a>CA1806: Methodenergebnisse nicht ignorieren.

|||
|-|-|
|TypeName|DoNotIgnoreMethodResults|
|CheckId|CA1806|
|Kategorie|Microsoft.Usage|
|Unterbrechende Änderung|Nicht unterbrechende Änderung|

## <a name="cause"></a>Ursache

Für diese Warnung gibt es mehrere mögliche Gründe:

- Ein neues-Objekt wird erstellt, aber nie verwendet.

- Eine Methode, die eine neue Zeichenfolge erstellt und zurückgibt, wird aufgerufen, und die neue Zeichenfolge wird nie verwendet.

- Eine com-oder P/aufrufen-Methode, die ein HRESULT oder einen Fehlercode zurückgibt, der niemals verwendet wird. Regelbeschreibung

Unnötige Objekt Erstellung und zugeordnete Garbage Collection der Leistungsfähigkeit des nicht verwendeten Objekts.

Zeichen folgen sind unveränderlich, und Methoden wie String. touppergibt eine neue Instanz einer Zeichenfolge zurück, anstatt die Instanz der Zeichenfolge in der aufrufenden Methode zu ändern.

Das Ignorieren von HRESULT oder Fehlercode kann zu unerwartetem Verhalten bei Fehlerbedingungen oder zu Ressourcenmangel führen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Wenn Methode a eine neue Instanz eines B-Objekts erstellt, das nie verwendet wird, übergeben Sie die Instanz als Argument an eine andere Methode, oder weisen Sie die Instanz einer Variablen zu. Wenn das Erstellen eines Objekts unnötig ist, entfernen Sie es.-oder-

Wenn method a die Methode b aufruft, verwendet jedoch nicht die neue Zeichen folgen Instanz, die von der Methode b zurückgegeben wird. Übergeben Sie die Instanz als Argument an eine andere Methode, weisen Sie die Instanz einer Variablen zu. Oder entfernen Sie den-Befehl, wenn dies unnötig ist.

 -oder-

Wenn method a die Methode B aufruft, jedoch nicht das HRESULT oder den Fehlercode verwendet, das von der Methode zurückgegeben wird. Verwenden Sie das Ergebnis in einer Bedingungs Anweisung, weisen Sie das Ergebnis einer Variablen zu, oder übergeben Sie es als Argument an eine andere Methode.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel, es sei denn, das Erstellen des Objekts dient einem bestimmten Zweck.

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Klasse, die das Ergebnis des Aufruf von String. Trim ignoriert.

[!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_1.cs)]
[!code-vb[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/VisualBasic/ca1806-do-not-ignore-method-results_1.vb)]
[!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_1.cpp)]

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird der vorherige Verstoß korrigiert, indem das Ergebnis von String. Trim der Variablen zugewiesen wird, für die es aufgerufen wurde.

[!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_2.cs)]
[!code-vb[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/VisualBasic/ca1806-do-not-ignore-method-results_2.vb)]
[!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_2.cpp)]

## <a name="example"></a>Beispiel
Das folgende Beispiel zeigt eine Methode, die kein Objekt verwendet, das Sie erstellt.

> [!NOTE]
> Diese Verletzung kann in Visual Basic nicht reproduziert werden.

[!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_3.cpp)]
[!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_3.cs)]

## <a name="example"></a>Beispiel
Im folgenden Beispiel wird der vorherige Verstoß behoben, indem die unnötige Erstellung eines Objekts entfernt wird.

[!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../code-quality/codesnippet/CSharp/ca1806-do-not-ignore-method-results_4.cs)]
[!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../code-quality/codesnippet/CPP/ca1806-do-not-ignore-method-results_4.cpp)]

<!-- Examples don't exist for the below... -->
<!--
## Example
The following example shows a method that ignores the error code that the native method GetShortPathName returns.

## Example
The following example fixes the previous violation by checking the error code and throwing an exception when the call fails.
-->