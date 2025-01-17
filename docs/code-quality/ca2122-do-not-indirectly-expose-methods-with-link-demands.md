---
title: 'CA2122: Methoden mit Linkaufrufen nicht indirekt verfügbar machen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 340d8f0a45506f15cdd9281f7ecda463583c3144
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920823"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122: Methoden mit Linkaufrufen nicht indirekt verfügbar machen.

|||
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Nicht unterbrechende Änderung|

## <a name="cause"></a>Ursache
Ein öffentliches oder geschütztes Mitglied hat einen [Link](/dotnet/framework/misc/link-demands) und wird von einem Member aufgerufen, der keine Sicherheitsüberprüfungen ausführt.

## <a name="rule-description"></a>Regelbeschreibung
Ein Linkaufruf überprüft nur die Berechtigungen des unmittelbaren Aufrufers. Wenn ein Member `X` keine Sicherheitsanforderungen seiner Aufrufer erfüllt und Code aufruft, der durch einen Link Aufruf geschützt ist, kann ein Aufrufer `X` ohne die erforderliche Berechtigung für den Zugriff auf den geschützten Member verwenden.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Fügen Sie dem-Element eine Sicherheits [Daten-und Modellierungs-](/dotnet/framework/data/index) oder Verknüpfungs Anforderung hinzu, damit kein unsicherer Zugriff mehr auf den Member mit Link Bedarf geschützt wird.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Um eine Warnung aus dieser Regel sicher zu unterdrücken, müssen Sie sicherstellen, dass Ihr Code den Aufrufern nicht den Zugriff auf Vorgänge oder Ressourcen gewährt, die auf zerstörerische Weise verwendet werden können.

## <a name="example-1"></a>Beispiel 1
Die folgenden Beispiele zeigen eine Bibliothek, die gegen die Regel verstößt, und eine Anwendung, die die Schwachstellen der Bibliothek veranschaulicht. Die Beispiel Bibliothek stellt zwei Methoden bereit, die gegen die Regel verstoßen. Die `EnvironmentSetting` -Methode wird durch einen Link Aufruf für den uneingeschränkten Zugriff auf Umgebungsvariablen gesichert. Die `DomainInformation` -Methode stellt keine Sicherheitsanforderungen Ihrer Aufrufer her `EnvironmentSetting`, bevor Sie aufruft.

[!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../code-quality/codesnippet/CSharp/ca2122-do-not-indirectly-expose-methods-with-link-demands_1.cs)]

## <a name="example-2"></a>Beispiel 2
Die folgende Anwendung ruft den nicht geschützten Bibliotheks Member auf.

[!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../code-quality/codesnippet/CSharp/ca2122-do-not-indirectly-expose-methods-with-link-demands_2.cs)]

Dieses Beispiel erzeugt die folgende Ausgabe:

```txt
*Value from unsecured member: seattle.corp.contoso.com
```

## <a name="see-also"></a>Siehe auch

- [Richtlinien für das Schreiben von sicherem Code](/dotnet/standard/security/secure-coding-guidelines)
- [Link Aufrufe](/dotnet/framework/misc/link-demands)
- [Daten und Modellierung](/dotnet/framework/data/index)