---
title: 'CA2103: Imperative Sicherheit überprüfen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2103
- ReviewImperativeSecurity
helpviewer_keywords:
- CA2103
- ReviewImperativeSecurity
ms.assetid: d24fde71-bdf6-46c0-8965-9a73dc33c1aa
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7acbb9d0127dd2ddb6668e72db8fa88124ec2b3c
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921428"
---
# <a name="ca2103-review-imperative-security"></a>CA2103: Imperative Sicherheit überprüfen.

|||
|-|-|
|TypeName|ReviewImperativeSecurity|
|CheckId|CA2103|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Eine Methode verwendet imperative Sicherheit und erstellt möglicherweise die Berechtigung mit Zustandsinformationen oder Rückgabewerten, die sich ändern können, während die Forderung wirksam ist.

## <a name="rule-description"></a>Regelbeschreibung
Bei imperativer Sicherheit werden verwaltete Objekte verwendet, um während der Codeausführung Berechtigungen und Sicherheitsaktionen anzugeben, im Vergleich zur deklarativen Sicherheit, bei der Attribute verwendet werden, um Berechtigungen und Aktionen in Metadaten zu speichern. Imperative Sicherheit ist sehr flexibel, da Sie den Status eines Berechtigungs Objekts festlegen und Sicherheitsaktionen mithilfe von Informationen auswählen können, die bis zur Laufzeit nicht verfügbar sind. Mit dieser Flexibilität besteht das Risiko, dass die Laufzeitinformationen, mit denen Sie den Zustand einer Berechtigung ermitteln, unverändert bleiben, solange die Aktion wirksam ist.

Verwenden Sie, wenn irgend möglich, deklarative Sicherheit. Deklarative Anforderungen sind leichter zu verstehen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Überprüfen Sie die imperative Sicherheitsanforderungen, um sicherzustellen, dass sich der Status der Berechtigung nicht auf Informationen stützt, die sich ändern können, solange die Berechtigung verwendet wird.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Es ist sicher, eine Warnung aus dieser Regel zu unterdrücken, wenn sich die Berechtigung nicht auf das Ändern von Daten verlässt. Es ist jedoch besser, den imperativen Bedarf in seine deklarative Entsprechung zu ändern.

## <a name="see-also"></a>Siehe auch

- [Richtlinien für das Schreiben von sicherem Code](/dotnet/standard/security/secure-coding-guidelines)
- [Daten und Modellierung](/dotnet/framework/data/index)