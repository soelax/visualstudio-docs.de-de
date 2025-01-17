---
title: 'CA1054: URI-Parameter dürfen keine Zeichenfolgen sein.'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1054
- UriParametersShouldNotBeStrings
helpviewer_keywords:
- CA1054
- UriParametersShouldNotBeStrings
ms.assetid: 8e99d72b-a658-47a7-8dd5-9784ce2c30b8
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 659ea1008cd70571d035d0b178d01587c6b2ba0d
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/17/2019
ms.locfileid: "65842058"
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054: URI-Parameter dürfen keine Zeichenfolgen sein.

|||
|-|-|
|TypeName|UriParametersShouldNotBeStrings|
|CheckId|CA1054|
|Kategorie|Microsoft.Design|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache

Ein Typ deklariert eine Methode mit einem Zeichenfolgenparameter, deren Name, "Uri", "Uri", "Urn", "Urn", "Url" oder "Url enthält" und der Typ deklariert keine entsprechende Überladung, die akzeptiert eine <xref:System.Uri?displayProperty=fullName> Parameter.

Diese Regel nur sucht standardmäßig an extern sichtbare Typen, aber dies ist [konfigurierbare](#configurability).

## <a name="rule-description"></a>Regelbeschreibung

Diese Regel wird der Name des Parameters in Token auf Grundlage der Konvention Kamel-Schreibweise und überprüft, ob jedes Token "Uri", "Uri", "Urn", "Urn", "Url" oder "Url" entspricht. Wenn eine Übereinstimmung vorliegt, wird die Regel davon ausgegangen, dass der Parameter einen uniform Resource Identifier (URI) darstellt. Eine Zeichenfolgendarstellung eines URIs ist anfällig für Analyse- und Codierungsfehler und kann zu Sicherheitsmängeln führen. Wenn eine Methode eine Zeichenfolgendarstellung eines URIs annimmt, eine entsprechende Überladung bereitgestellt werden sollen, eine Instanz von akzeptiert die <xref:System.Uri> Klasse, die diese Dienste auf sichere Weise bereitstellt.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen

Um einen Verstoß gegen diese Regel zu beheben, ändern Sie den Parameter, um eine <xref:System.Uri> -Typ. Dies ist eine wichtige Änderung. Klicken Sie alternativ Geben Sie eine Überladung der Methode, die akzeptiert eine <xref:System.Uri> -Parameter ist; dies ist eine nicht unterbrechende Änderung.

## <a name="when-to-suppress-warnings"></a>Wenn Sie Warnungen unterdrücken

Es ist sicher eine Warnung dieser Regel zu unterdrücken, wenn der Parameter keinen URI darstellt.

## <a name="configurability"></a>Konfigurierbarkeit

Wenn Sie diese Regel aus ausführen, [FxCop-Analysen](install-fxcop-analyzers.md) (und nicht über die Analyse von statischem Code), können Sie konfigurieren, welche Teile Ihrer Codebasis, um die Ausführung dieser Regel auf, um basierend auf deren Barrierefreiheit. Z. B. um anzugeben, dass die Regel nur für die nicht öffentlichen API-Oberfläche ausgeführt werden soll, fügen Sie die folgenden Schlüssel-Wert-Paar in einer editorconfig-Datei in Ihrem Projekt:

```ini
dotnet_code_quality.ca1054.api_surface = private, internal
```

Sie können diese Option, die für diese eine Regel, für alle Regeln oder für alle Regeln in dieser Kategorie (Entwurf) konfigurieren. Weitere Informationen finden Sie unter [konfigurieren FxCop-Analysetools](configure-fxcop-analyzers.md).

## <a name="example"></a>Beispiel

Das folgende Beispiel zeigt einen Typ, `ErrorProne`, die gegen diese Regel und einen Typ, `SaferWay`, die die Regel erfüllt.

[!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1054-uri-parameters-should-not-be-strings_1.cs)]
[!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1054-uri-parameters-should-not-be-strings_1.vb)]
[!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1054-uri-parameters-should-not-be-strings_1.cpp)]

## <a name="related-rules"></a>Verwandte Regeln

- [CA1056: URI-Eigenschaften dürfen keine Zeichenfolgen sein.](../code-quality/ca1056-uri-properties-should-not-be-strings.md)
- [CA1055: URI-Rückgabewerte sollten keine Zeichenfolgen sein](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
- [CA2234: Übergeben Sie System.Uri-Objekte anstelle von Zeichenfolgen](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)
- [CA1057: URI-Überladungen der Zeichenfolge aufrufen System.Uri-Überladungen](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)