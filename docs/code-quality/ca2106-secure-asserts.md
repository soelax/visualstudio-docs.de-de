---
title: 'CA2106: Sichere Bestätigungen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2106
- SecureAsserts
helpviewer_keywords:
- CA2106
- SecureAsserts
ms.assetid: 91feb36e-6e2c-436c-8272-5aee31f77e98
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df19d31abe88c6d12bafc933ba740badb832eb16
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921074"
---
# <a name="ca2106-secure-asserts"></a>CA2106: Sichere Bestätigungen.

|||
|-|-|
|TypeName|SecureAsserts|
|CheckId|CA2106|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Eine Methode bestätigt eine Berechtigung und führt keine Sicherheitsüberprüfungen für den Aufrufer aus.

## <a name="rule-description"></a>Regelbeschreibung
Das Gewähren einer Sicherheitsberechtigung ohne Sicherheitsüberprüfungen durchzuführen, kann ein ausnutzbares Sicherheitsrisiko in Code hinterlassen. Ein Sicherheits Stapel-Walk wird beendet, wenn eine Sicherheits Berechtigung bestätigt wird. Wenn Sie eine Berechtigung ohne Überprüfung des Aufrufers bestätigen, könnte der Aufrufer indirekt Code ausführen, indem er ihre Berechtigungen verwendet. Bestätigungen ohne Sicherheitsüberprüfungen sind zulässig, wenn Sie sicher sind, dass Assert nicht schädlich verwendet werden kann. Eine Assert-Bestätigung ist harmlos, wenn der aufzurufende Code harmlos ist oder wenn Benutzer keine willkürlichen Informationen an den von Ihnen aufzurufenden Code übergeben können.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, fügen Sie der Methode oder dem deklarierenden Typ eine Sicherheitsanforderung hinzu.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Unterdrückt eine Warnung aus dieser Regel erst nach einer sorgfältigen Sicherheitsüberprüfung.

## <a name="see-also"></a>Siehe auch

- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
- [Richtlinien für das Schreiben von sicherem Code](/dotnet/standard/security/secure-coding-guidelines)