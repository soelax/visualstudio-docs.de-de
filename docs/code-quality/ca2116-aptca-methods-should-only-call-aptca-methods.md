---
title: 'CA2116: APTCA-Methoden sollten nur APTCA-Methoden aufrufen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f55c48583e47a4602f33d69799d1d86a6c9c3e56
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921148"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116: APTCA-Methoden sollten nur APTCA-Methoden aufrufen.

|||
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache

Eine Methode in einer Assembly mit dem <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> -Attribut ruft eine Methode in einer Assembly auf, die nicht über das-Attribut verfügt.

## <a name="rule-description"></a>Regelbeschreibung

Standardmäßig werden öffentliche oder geschützte Methoden in Assemblys mit starken Namen implizit durch einen [Link](/dotnet/framework/misc/link-demands) Aufruf für volle Vertrauenswürdigkeit geschützt. nur voll vertrauenswürdige Aufrufer können auf eine Assembly mit starkem Namen zugreifen. Assemblys mit starkem Namen, <xref:System.Security.AllowPartiallyTrustedCallersAttribute> die mit dem-Attribut (APTCA) gekennzeichnet sind, verfügen nicht über diesen Schutz. Das-Attribut deaktiviert den Link Aufruf, sodass Aufrufer, die nicht voll vertrauenswürdig sind, wie z. b. Code, der über ein Intranet oder das Internet ausgeführt wird, auf die Assembly zugreifen können.

Wenn das APTCA-Attribut in einer voll vertrauenswürdigen Assembly vorhanden ist und die Assembly Code in einer anderen Assembly ausführt, die keine teilweise vertrauenswürdigen Aufrufer zulässt, kann eine Sicherheitslücke ausgenutzt werden. Wenn zwei Methoden `M1` und `M2` die folgenden Bedingungen erfüllen, können böswillige Aufrufer `M1` die-Methode verwenden, um den impliziten voll Vertrauens `M2`würdigen Link Bedarf zu umgehen, der schützt:

- `M1`ist eine öffentliche Methode, die in einer voll vertrauenswürdigen Assembly mit dem APTCA-Attribut deklariert ist.

- `M1`Ruft eine Methode `M2` außerhalb `M1`der Assembly auf.

- `M2`die Assembly verfügt nicht über das APTCA-Attribut und sollte daher nicht von oder im Auftrag von Aufrufern ausgeführt werden, die teilweise vertrauenswürdig sind.

Ein teilweise vertrauenswürdiger `X` Aufrufer `M1`kann die `M1` -Methode `M2`aufzurufen, wodurch aufgerufen wird. Da `M2` nicht über das APTCA-Attribut verfügt, muss der unmittelbare`M1`Aufrufer () einen Link Bedarf für volle Vertrauenswürdigkeit erfüllen. `M1` hat volle Vertrauenswürdigkeit und erfüllt daher diese Überprüfung. Das Sicherheitsrisiko besteht darin `X` , dass nicht an der Erfüllung des Link Bedarfs teilnimmt `M2` , der vor nicht vertrauenswürdigen Aufrufern schützt. Daher dürfen Methoden mit dem APTCA-Attribut keine Methoden aufzurufen, die nicht über das-Attribut verfügen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Wenn das apcta-Attribut erforderlich ist, verwenden Sie eine Anforderung, um die Methode zu schützen, die die voll vertrauenswürdige Assembly aufruft. Welche Berechtigungen Sie benötigen, hängt von der Funktionalität ab, die von der-Methode verfügbar gemacht wird. Wenn dies möglich ist, schützen Sie die Methode mit einer Anforderung für vollständige Vertrauenswürdigkeit, um sicherzustellen, dass die zugrunde liegende Funktionalität nicht teilweise vertrauenswürdigen Aufrufern ausgesetzt ist. Wenn dies nicht möglich ist, wählen Sie einen Berechtigungs Satz aus, der die verfügbaren Funktionen effektiv schützt.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Um eine Warnung aus dieser Regel sicher zu unterdrücken, müssen Sie sicherstellen, dass die von der-Methode verfügbar gemachten Funktionen nicht direkt oder indirekt Aufrufern Zugriff auf vertrauliche Informationen, Vorgänge oder Ressourcen ermöglichen, die auf zerstörerische Weise verwendet werden können.

## <a name="example-1"></a>Beispiel 1
Im folgenden Beispiel werden zwei Assemblys und eine Testanwendung verwendet, um das Sicherheitsrisiko zu veranschaulichen, das von dieser Regel erkannt wird. Die erste Assembly verfügt nicht über das APTCA-Attribut und sollte nicht für teilweise vertrauenswürdige Aufrufer ( `M2` dargestellt durch in der vorherigen Diskussion) verfügbar sein.

[!code-csharp[FxCop.Security.NoAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_1.cs)]

## <a name="example-2"></a>Beispiel 2
Die zweite Assembly ist voll vertrauenswürdig und ermöglicht teilweise vertrauenswürdige Aufrufer ( `M1` in der vorherigen Diskussion dargestellt).

[!code-csharp[FxCop.Security.YesAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_2.cs)]

## <a name="example-3"></a>Beispiel 3
Die Testanwendung (dargestellt durch `X` in der vorherigen Diskussion) ist teilweise vertrauenswürdig.

[!code-csharp[FxCop.Security.TestAptcaMethods#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_3.cs)]

Dieses Beispiel erzeugt die folgende Ausgabe:

```txt
Demand for full trust:Request failed.
ClassRequiringFullTrust.DoWork was called.
```

## <a name="related-rules"></a>Verwandte Regeln

- [CA2117: APTCA-Typen sollten nur APTCA-Basis Typen erweitern](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>Siehe auch

- [Richtlinien für das Schreiben von sicherem Code](/dotnet/standard/security/secure-coding-guidelines)
- [Verwenden von Bibliotheken aus teilweise vertrauenswürdigem Code](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)
- [Link Aufrufe](/dotnet/framework/misc/link-demands)
- [Daten und Modellierung](/dotnet/framework/data/index)