---
title: 'CA2138: Transparente Methoden dürfen keine Methoden mit dem SuppressUnmanagedCodeSecurity-Attribut aufrufen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 316aef3b0f1f715857fde8eaf2a6e74b1a49e40f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920581"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138: Transparente Methoden dürfen keine Methoden mit dem SuppressUnmanagedCodeSecurity-Attribut aufrufen.

|||
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Eine Sicherheits transparente Methode ruft eine Methode auf, die mit dem <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> -Attribut markiert ist.

## <a name="rule-description"></a>Regelbeschreibung
Diese Regel wird für jede transparente Methode ausgelöst, die direkt in systemeigenen Code aufruft, z. b. mit einem Aufruf von P/Aufruf (Platt Form Aufruf). P/Call-und COM-Interop-Methoden, die <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> mit dem-Attribut markiert sind, führen dazu, dass LinkDemand für die aufrufende Methode ausgeführt wird. Da der Sicherheits transparente Code linkforderungen nicht erfüllen kann, kann der Code auch keine Methoden aufrufen, die mit dem SuppressUnmanagedCodeSecurity-Attribut gekennzeichnet sind, oder Methoden der Klasse, die mit dem SuppressUnmanagedCodeSecurity-Attribut markiert sind. Die Methode kann nicht ausgeführt werden, oder die Anforderung wird in eine vollständige Anforderung konvertiert.

Verstöße gegen diese Regel führen zu einem <xref:System.MethodAccessException> im Sicherheits Transparenz Modell der Ebene 2 und einer vollständigen Anforderung für <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> im Transparenz Modell der Ebene 1.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, entfernen <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> Sie das-Attribut, und markieren <xref:System.Security.SecurityCriticalAttribute> Sie die <xref:System.Security.SecuritySafeCriticalAttribute> Methode mit dem-Attribut oder dem-Attribut.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Warnung dieser Regel.

## <a name="example"></a>Beispiel
[!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../code-quality/codesnippet/CSharp/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute_1.cs)]