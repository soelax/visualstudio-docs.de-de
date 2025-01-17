---
title: 'CA2147: Transparente Methoden dürfen keine Sicherheitsassertionen verwenden.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SecurityTransparentCodeShouldNotAssert
- CA2147
- CA2128
helpviewer_keywords:
- CA2128
- SecurityTransparentCodeShouldNotAssert
ms.assetid: 5d31e940-e599-4b23-9b28-1c336f8d910e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1b56001f5a083317911edde9282b66758deb1b6
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920715"
---
# <a name="ca2147-transparent-methods-may-not-use-security-asserts"></a>CA2147: Transparente Methoden dürfen keine Sicherheitsassertionen verwenden.

|||
|-|-|
|TypeName|SecurityTransparentCodeShouldNotAssert|
|CheckId|CA2147|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Code, der als <xref:System.Security.SecurityTransparentAttribute> markiert ist, verfügt nicht über ausreichende Berechtigungen für Assert.

## <a name="rule-description"></a>Regelbeschreibung
Mit dieser Regel werden alle Methoden und Typen in einer Assembly analysiert, die entweder 100% transparent oder gemischt transparent/kritisch ist, und jede deklarative oder imperative <xref:System.Security.CodeAccessPermission.Assert%2A>Verwendung von Flags.

Zur Laufzeit bewirken alle Aufrufe <xref:System.Security.CodeAccessPermission.Assert%2A> von aus transparentem Code, dass eine <xref:System.InvalidOperationException> ausgelöst wird. Dies kann sowohl in 100% transparenten Assemblys als auch in gemischten transparenten/kritischen Assemblys auftreten, in denen eine Methode oder ein Typ als transparent deklariert ist, aber eine deklarative oder imperative Bestätigung enthält.

Der .NET Framework 2,0 hat eine Funktion mit dem Namen " *Transparenz*" eingeführt. Einzelne Methoden, Felder, Schnittstellen, Klassen und Typen können entweder transparent oder kritisch sein.

Transparenter Code ist nicht berechtigt, Sicherheits Privilegien zu erhöhen. Aus diesem Grund werden alle gewährten Berechtigungen automatisch an die Aufrufer-oder Host Anwendungsdomäne übermittelt. Beispiele für Erweiterungen sind Assert, LinkDemand, SuppressUnmanagedCode und `unsafe` Code.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um das Problem zu beheben, markieren Sie entweder den Code, der den Assert <xref:System.Security.SecurityCriticalAttribute>aufruft, mit, oder entfernen Sie den Assert.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrücken Sie keine Meldung von dieser Regel.

## <a name="example"></a>Beispiel
Dieser Code schlägt fehl, `SecurityTestClass` wenn transparent ist, wenn `Assert` die Methode einen <xref:System.InvalidOperationException>auslöst.

[!code-csharp[FxCop.Security.CA2147.TransparentMethodsMustNotUseSecurityAsserts#1](../code-quality/codesnippet/CSharp/ca2147-transparent-methods-may-not-use-security-asserts_1.cs)]

## <a name="example"></a>Beispiel
Eine Möglichkeit besteht darin, die SecurityTransparentMethod-Methode im folgenden Beispiel Code Review, und wenn die Methode für die Erhöhung als sicher eingestuft wird, markieren Sie SecurityTransparentMethod mit Secure-Critical. Dies erfordert, dass eine ausführliche, umfassende und fehlerfreie Sicherheitsüberprüfung für die Methode mit allen Aufrufen erfolgen muss, die innerhalb der Methode unter der Assert-Methode auftreten:

[!code-csharp[FxCop.Security.SecurityTransparentCode2#1](../code-quality/codesnippet/CSharp/ca2147-transparent-methods-may-not-use-security-asserts_2.cs)]

Eine andere Möglichkeit besteht darin, die Assert-Berechtigung aus dem Code zu entfernen und allen nachfolgenden Datei-e/a-Berechtigungen das übernehmen von SecurityTransparentMethod an den Aufrufer zu gestatten Dies ermöglicht Sicherheitsüberprüfungen. In diesem Fall ist keine Sicherheitsüberprüfung erforderlich, da die Berechtigungsanforderungen an den Aufrufer und/oder die Anwendungsdomäne weitergeleitet werden. Berechtigungsanforderungen werden durch die Sicherheitsrichtlinie, die Hostingumgebung und die Berechtigungen zum Gewähren von Code Quellen streng gesteuert.

## <a name="see-also"></a>Siehe auch
[Sicherheitswarnungen](../code-quality/security-warnings.md)