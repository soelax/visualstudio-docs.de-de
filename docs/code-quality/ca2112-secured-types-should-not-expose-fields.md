---
title: 'CA2112: Gesicherte Typen sollten keine Felder verfügbar machen.'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43ef4165823f59045dda8c05b5679fdd3b795114
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921082"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112: Gesicherte Typen sollten keine Felder verfügbar machen.

|||
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|Kategorie|Microsoft.Security|
|Unterbrechende Änderung|Breaking|

## <a name="cause"></a>Ursache
Ein öffentlicher oder geschützter Typ enthält öffentliche Felder und wird durch einen [Link](/dotnet/framework/misc/link-demands)Aufruf gesichert.

## <a name="rule-description"></a>Regelbeschreibung
Wenn Code auf eine Instanz eines Typs zugreifen muss, der durch einen Linkaufruf gesichert ist, muss der Code für den Zugriff auf die Felder des Typs nicht die Anforderungen des Linkaufrufs erfüllen.

## <a name="how-to-fix-violations"></a>Behandeln von Verstößen
Um einen Verstoß gegen diese Regel zu beheben, legen Sie die Felder als nicht öffentlich fest, und fügen Sie öffentliche Eigenschaften oder Methoden hinzu, die die Felddaten zurückgeben. LinkDemand-Sicherheitsüberprüfungen für Typen schützen den Zugriff auf die Eigenschaften und Methoden des Typs. Die Code Zugriffssicherheit gilt jedoch nicht für Felder.

## <a name="when-to-suppress-warnings"></a>Wann sollten Warnungen unterdrückt werden?
Sowohl für Sicherheitsprobleme als auch für einen guten Entwurf sollten Verstöße behoben werden, indem die öffentlichen Felder nicht öffentlich gemacht werden. Sie können eine Warnung aus dieser Regel unterdrücken, wenn das Feld keine Informationen enthält, die geschützt bleiben sollen, und Sie sich nicht auf den Inhalt des Felds verlassen.

## <a name="example"></a>Beispiel
Das folgende Beispiel besteht aus einem Bibliothekstyp (`SecuredTypeWithFields`) mit ungesicherten Feldern, einem Typ`Distributor`(), der Instanzen des Bibliotheks Typs erstellen kann, und irrtümlich übergibt Instanzen an Typen keine Berechtigung zum Erstellen dieser Felder und Anwendungscode, der kann die Felder einer Instanz lesen, auch wenn Sie nicht über die Berechtigung verfügt, die den Typ sichert.

Der folgende Bibliotheks Code verstößt gegen die Regel.

[!code-csharp[FxCop.Security.LinkDemandOnField#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_1.cs)]

## <a name="example-1"></a>Beispiel 1
Die Anwendung kann aufgrund des Link Aufrufs, der den gesicherten Typ schützt, keine Instanz erstellen. Mit der folgenden Klasse kann die Anwendung eine Instanz des gesicherten Typs abrufen.

[!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_2.cs)]

## <a name="example-2"></a>Beispiel 2
Die folgende Anwendung veranschaulicht, wie der Code ohne Berechtigung für den Zugriff auf die Methoden eines gesicherten Typs auf seine Felder zugreifen kann.

[!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../code-quality/codesnippet/CSharp/ca2112-secured-types-should-not-expose-fields_3.cs)]

Dieses Beispiel erzeugt die folgende Ausgabe:

```txt
Creating an instance of SecuredTypeWithFields.
Secured type fields: 22, 33
Changing secured type's field...
Cached Object fields: 99, 33
```

## <a name="related-rules"></a>Verwandte Regeln

- [CA1051: Sichtbare Instanzfelder nicht deklarieren](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Siehe auch

- [Link Aufrufe](/dotnet/framework/misc/link-demands)
- [Daten und Modellierung](/dotnet/framework/data/index)