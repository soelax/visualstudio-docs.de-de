---
title: 'CA2137: Transparente Methoden dürfen nur überprüfbare IL enthalten.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2137
ms.assetid: cbaeb0e1-56b6-43b4-812a-596b2859c329
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 98b75a9f67a24fd8bea1ecc3a8782b6bd9e6b34b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920604"
---
# <a name="ca2137-transparent-methods-must-contain-only-verifiable-il"></a>CA2137: Transparente Methoden dürfen nur überprüfbare IL enthalten.

|||
|-|-|
|TypeName|Transparentmethodsmustbeprüfbar|
|CheckId|CA2137|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Eine Methode enthält nicht überprüfbaren Code oder gibt einen Typ nach Verweis zurück.

## <a name="rule-description"></a>Regelbeschreibung
Diese Regel wird für Versuche durch sicherheitstransparenten Code ausgelöst, nicht überprüfbare MSIL (Microsoft Intermediate Language) auszuführen. Die Regel enthält jedoch kein vollständiges IL-Prüfmodul und verwendet stattdessen Heuristik, um die meisten Verletzungen der MSIL-Überprüfung abzufangen.

Um sicherzustellen, dass Ihr Code nur überprüfbare MSIL enthält, führen Sie " [Peer Verify. exe" (Peer Verify Tool)](/dotnet/framework/tools/peverify-exe-peverify-tool) für die Assembly aus. Führen Sie "Peer verify" mit der **/transparent** -Option aus, die die Ausgabe auf nicht überprüfbare transparente Methoden beschränkt, die einen Fehler verursachen würden. Wenn die/transparent-Option nicht verwendet wird, überprüft Peer Verify auch kritische Methoden, die nicht überprüfbaren Code enthalten dürfen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, markieren Sie die Methode <xref:System.Security.SecurityCriticalAttribute> mit <xref:System.Security.SecuritySafeCriticalAttribute> dem-Attribut oder dem-Attribut, oder entfernen Sie den nicht überprüfbaren Code.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
Die-Methode in diesem Beispiel verwendet nicht überprüfbaren Code und sollte mit dem- <xref:System.Security.SecurityCriticalAttribute> Attribut <xref:System.Security.SecuritySafeCriticalAttribute> oder dem-Attribut gekennzeichnet sein.

[!code-csharp[FxCop.Security.CA2137.TransparentMethodsMustBeVerifiable#1](../code-quality/codesnippet/CSharp/ca2137-transparent-methods-must-contain-only-verifiable-il_1.cs)]