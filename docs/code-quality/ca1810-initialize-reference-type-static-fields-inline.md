---
title: 'CA1810: Statische Felder von Referenztypen inline initialisieren.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
helpviewer_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8838de46c6b14f698194f343aebec30402452970
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921526"
---
# <a name="ca1810-initialize-reference-type-static-fields-inline"></a>CA1810: Statische Felder von Referenztypen inline initialisieren.

|||
|-|-|
|TypeName|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|Kategorie|Microsoft.Performance|
|Unterbrechende Änderung|Nicht unterbrechend|

## <a name="cause"></a>Ursache
Ein Verweistyp deklariert einen expliziten statischen Konstruktor.

## <a name="rule-description"></a>Regelbeschreibung
Wenn ein Typ einen expliziten statischen Konstruktor deklariert, überprüft der JIT-Compiler (Just in Time) jede statische Methode und jeden Instanzenkonstruktor des Typs. Dadurch wird sichergestellt, dass der statische Konstruktor zuvor aufgerufen wurde. Die statische Initialisierung wird ausgelöst, wenn auf einen statischen Member zugegriffen wird oder wenn eine Instanz des Typs erstellt wird. Die statische Initialisierung wird jedoch nicht ausgelöst, wenn Sie eine Variable des Typs deklarieren, aber nicht verwenden. Dies kann wichtig sein, wenn die Initialisierung den globalen Zustand ändert.

Wenn alle statischen Daten inline initialisiert werden und ein expliziter statischer Konstruktor nicht deklariert ist, fügen Microsoft Intermediate Language (MSIL) `beforefieldinit` -Compiler das-Flag und einen impliziten statischen Konstruktor, der die statischen Daten initialisiert, dem MSIL-Typ hinzu. Definition. Wenn der JIT-Compiler auf `beforefieldinit` das-Flag trifft, werden die statischen Konstruktorüberprüfungen meistens nicht hinzugefügt. Die statische Initialisierung wird garantiert zu einem bestimmten Zeitpunkt ausgeführt, bevor auf statische Felder zugegriffen wird, jedoch nicht, bevor eine statische Methode oder ein Instanzkonstruktor aufgerufen wird. Beachten Sie, dass die statische Initialisierung jederzeit erfolgen kann, nachdem eine Variable vom Typ deklariert wurde.

Durch die Überprüfung statischer Konstruktoren kann die Leistung herabgesetzt werden. Häufig wird ein statischer Konstruktor nur zum Initialisieren statischer Felder verwendet. in diesem Fall müssen Sie nur sicherstellen, dass die statische Initialisierung vor dem ersten Zugriff eines statischen Felds erfolgt. Das `beforefieldinit` Verhalten ist für diese und die meisten anderen Typen geeignet. Sie ist nur ungeeignet, wenn die statische Initialisierung den globalen Zustand beeinflusst und eine der folgenden Punkte zutrifft:

- Die Auswirkung auf den globalen Status ist aufwendig und ist nicht erforderlich, wenn der Typ nicht verwendet wird.

- Auf die globalen Zustands Effekte kann ohne Zugriff auf statische Felder des Typs zugegriffen werden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, initialisieren Sie alle statischen Daten nach deren Deklaration und entfernen den statischen Konstruktor.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn die Leistung nicht relevant ist. oder, wenn globale Zustandsänderungen, die durch die statische Initialisierung verursacht werden, aufwendig sind oder garantiert werden müssen, bevor eine statische Methode des Typs aufgerufen oder eine Instanz des Typs erstellt wird.

## <a name="example"></a>Beispiel

Das folgende Beispiel zeigt einen Typ `StaticConstructor`,, der gegen die Regel verstößt, und einen `NoStaticConstructor`Typ,, der den statischen Konstruktor durch Inline Initialisierung ersetzt, um die Regel zu erfüllen.

[!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../code-quality/codesnippet/CSharp/ca1810-initialize-reference-type-static-fields-inline_1.cs)]
[!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../code-quality/codesnippet/VisualBasic/ca1810-initialize-reference-type-static-fields-inline_1.vb)]

Beachten Sie, dass das `beforefieldinit` -Flag für die MSIL-Definition `NoStaticConstructor` für die-Klasse hinzugefügt wird.

```
.class public auto ansi StaticConstructor
extends [mscorlib]System.Object
{
} // end of class StaticConstructor

.class public auto ansi beforefieldinit NoStaticConstructor
extends [mscorlib]System.Object
{
} // end of class NoStaticConstructor
```

## <a name="related-rules"></a>Verwandte Regeln

- [CA2207: Statische Felder für Werttyp Inline initialisieren](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)