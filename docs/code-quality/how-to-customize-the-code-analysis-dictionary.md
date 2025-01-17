---
title: 'Vorgehensweise: Anpassen des Codeanalysewörterbuchs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b43d731634022a2f3fcb9e00b552e75e5322db8c
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715236"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>Vorgehensweise: Anpassen des Codeanalysewörterbuchs

Codeanalyse mithilfe ein integriertes Wörterbuch Bezeichner im Code Rechtschreibung, grammatische Groß-/Kleinschreibung und andere Benennungskonventionen für von den Entwurfsrichtlinien von .NET auf Fehler überprüft. Sie können eine benutzerdefiniertes Wörterbuch XML-Datei hinzufügen, entfernen oder Ändern der Begriffe, Abkürzungen und Akronyme, die dem integrierten Wörterbuch erstellen.

Nehmen wir beispielsweise an, die Ihren Code enthalten, eine Klasse namens **DoorKnokker**. Codeanalyse würde den Namen identifiziert, als eine Zusammensetzung von zwei Wörtern: **Tür** und **Knokker**. Klicken Sie dann eine Warnung auslösen würde, **Knokker** nicht korrekt geschrieben ist. Um die Codeanalyse erkennen die Schreibweise zu erzwingen, können Sie den Begriff hinzufügen **Knokker** dem benutzerdefinierten Wörterbuch.

## <a name="to-create-a-custom-dictionary"></a>Erstellen Sie ein benutzerdefiniertes Wörterbuch

Erstellen Sie eine Datei mit dem Namen **CustomDictionary.xml**.

Definieren Sie die benutzerdefinierten Wörter, indem Sie mithilfe der folgenden XML-Struktur:

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>knokker</Word>
         </Unrecognized>
         <Recognized>
            <Word></Word>
         </Recognized>
         <Deprecated>
            <Term PreferredAlternate=""></Term>
         </Deprecated>
         <Compound>
            <Term CompoundAlternate=""></Term>
         </Compound>
         <DiscreteExceptions>
            <Term></Term>
         </DiscreteExceptions>
      </Words>
      <Acronyms>
         <CasingExceptions>
            <Acronym></Acronym>
         </CasingExceptions>
      </Acronyms>
   </Dictionary>
```

## <a name="custom-dictionary-elements"></a>Benutzerdefiniertes Wörterbuch-Elemente

Sie können das Verhalten des Codeanalysewörterbuchs ändern, durch das Hinzufügen von Bedingungen als innerer Text in das benutzerdefinierte Wörterbuch den folgenden Elementen:

- [Wörterbuch/Wörter/erkannt/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [Wörterbuch/Wörter/unbekannte/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [Dictionary/Words/Deprecated/Term[@PreferredAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [Dictionary/Words/Compound/Term[@CompoundAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [Dictionary/Acronyms/CasingExceptions/Acronym](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="BKMK_DictionaryWordsRecognizedWord"></a> Wörterbuch/Wörter/erkannt/Word

Zum Einschließen von eines Begriffs in der Liste der Begriffe, die die Codeanalyse identifiziert, die als korrekt geschrieben, fügen Sie den Begriff als innerer Text eines Elements Dictionary/Wörter/Recognized/Word hinzu. Begriffe im Wörterbuch/Wörter/Recognized/Word-Elemente sind nicht in der Groß-/Kleinschreibung beachtet.

**Beispiel**

```xml
<Dictionary>
      <Words>
         <Recognized>
            <Word>knokker</Word>
            ...
         </Recognized>
         ...
      </Words>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Wörter/Recognized-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1701: Zusammengesetzte Begriffen in Ressourcenzeichenfolgen sollte beachtet werden](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702: Bei zusammengesetzten Begriffen sollte beachtet werden](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703: Ressourcenzeichenfolgen sollten korrekt geschrieben werden](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704: Bezeichner sollten korrekt geschrieben werden](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709: Bezeichner sollten beachtet werden](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726: Bevorzugte Begriffe verwenden](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204: Literale sollten eine korrekte Rechtschreibung aufweisen](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsUnrecognizedWord"></a> Wörterbuch/Wörter/unbekannte/Word

Fügen Sie zum Ausschließen von eines Begriffs aus der Liste der Bedingungen, die Codeanalyse identifiziert, die als korrekt geschrieben, den Begriff als innerer Text eines Elements Dictionary/Wörter/Unrecognized/Word ausschließen. Begriffe im Wörterbuch/Wörter/Unrecognized/Word-Elemente sind nicht in der Groß-/Kleinschreibung beachtet.

**Beispiel**

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>meth</Word>
            ...
         </Unrecognized>
         ...
      </Words>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Wörter/nicht erkannt-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1701: Zusammengesetzte Begriffen in Ressourcenzeichenfolgen sollte beachtet werden](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702: Bei zusammengesetzten Begriffen sollte beachtet werden](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703: Ressourcenzeichenfolgen sollten korrekt geschrieben werden](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704: Bezeichner sollten korrekt geschrieben werden](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709: Bezeichner sollten beachtet werden](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726: Bevorzugte Begriffe verwenden](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204: Literale sollten eine korrekte Rechtschreibung aufweisen](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> / Wörter/veraltet/Wörterbucheinträge [@PreferredAlternate]

Um einen Begriff in der Liste der Begriffe enthalten, die die Codeanalyse identifiziert, als veraltet, fügen Sie den Begriff als innerer Text von einem Wörterbuch/Wörter/veraltet/Term-Element hinzu. Ein als veraltet markierte Begriff ist ein Wort, die richtig geschrieben ist, aber nicht verwendet werden sollte.

Um einen vorgeschlagenen alternativen Begriff in der Warnung einzuschließen, geben Sie die alternative im PreferredAlternate-Attribut des Elements Begriff aus. Sie können den Attributwert leer lassen, wenn Sie nicht, um einen alternativen vorzuschlagen möchten.

- Der als veraltet markierten Ausdruck in Wörterbucheinträge / / veraltet/Term-Element wird nicht beachtet.

- Der Attributwert PreferredAlternate ist Groß-/Kleinschreibung beachtet. Verwenden Sie für zusammengesetzte alternativen Pascal-Schreibweise.

**Beispiel**

```xml
<Dictionary>
      <Words>
         <Deprecated>
            <Term PreferredAlternate="LogOn">login</Term>
            ...
         </Deprecated>
         ...
      </Words>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Wörter/veraltet-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1701: Zusammengesetzte Begriffen in Ressourcenzeichenfolgen sollte beachtet werden](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702: Bei zusammengesetzten Begriffen sollte beachtet werden](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703: Ressourcenzeichenfolgen sollten korrekt geschrieben werden](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704: Bezeichner sollten korrekt geschrieben werden](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1726: Bevorzugte Begriffe verwenden](../code-quality/ca1726-use-preferred-terms.md)

### <a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> Dictionary/Words/Compound/Term[@CompoundAlternate]

Die integrierte Wörterbuch Begriffe einige als einzelne, separate Bedingungen und nicht als zusammengesetzter Begriff. Um einen Begriff in der Liste der Begriffe enthalten, die Codeanalyse als zusammengesetzter Begriff zu identifizieren und geben Sie die richtige Groß-/Kleinschreibung des Begriffs, fügen Sie den Begriff als innerer Text eines Elements Dictionary/Wörter/zusammengesetzte/Term hinzu. Geben Sie im CompoundAlternate-Attribut des Elements Begriff die einzelnen Wörter, aus denen der zusammengesetzte Begriff durch den ersten Buchstaben der einzelnen Wörter (Pascal-Schreibweise). Beachten Sie, dass der Begriff in den inneren Text angegebenen Wörterbuch/Wörter/DiscreteExceptions Liste automatisch hinzugefügt wird.

- Der als veraltet markierten Ausdruck in Wörterbucheinträge / / veraltet/Term-Element wird nicht beachtet.

- Der Attributwert PreferredAlternate ist Groß-/Kleinschreibung beachtet. Verwenden Sie für zusammengesetzte alternativen Pascal-Schreibweise.

**Beispiel**

```xml
<Dictionary>
      <Words>
         <Compound>
            <Term CompoundAlternate="CheckBox">checkbox</Term>
            ...
         </Compound>
         ...
      </Words>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Wörter/Compound-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1701: Zusammengesetzte Begriffen in Ressourcenzeichenfolgen sollte beachtet werden](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702: Bei zusammengesetzten Begriffen sollte beachtet werden](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703: Ressourcenzeichenfolgen sollten korrekt geschrieben werden](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704: Bezeichner sollten korrekt geschrieben werden](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> Wörterbuch/Wörter/DiscreteExceptions/Begriff

Um einen Ausdruck in der Liste der Begriffe auszuschließen, die Codeanalyse als einzelnes identifiziert, diskrete Wort der Begriff von der Groß-/ Kleinschreibregeln für zusammengesetzte Wörter ist dieses Kontrollkästchen aktiviert wird den Begriff als innerer Text eines Elements Dictionary/Wörter/DiscreteExceptions/Term hinzufügen. Der Begriff im Wörterbuch/Wörter/DiscreteExceptions/Term-Element wird nicht beachtet.

**Beispiel**

```xml
<Dictionary>
      <Words>
         <DiscreteExceptions>
            <Term>checkbox</Term>
            ...
         </DiscreteExceptions>
         ...
      </Words>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Wörter/DiscreteExceptions-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1701: Zusammengesetzte Begriffen in Ressourcenzeichenfolgen sollte beachtet werden](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702: Bei zusammengesetzten Begriffen sollte beachtet werden](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

### <a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Wörterbuch/Akronyme/CasingExceptions/Akronym

Um ein Akronym in der Liste der Begriffe enthalten, die die Codeanalyse als richtig geschriebenes identifiziert und anzugeben, wie das Akronym, wenn der Begriff, durch die Groß-/Kleinschreibung aktiviert ist-Regeln für die zusammengesetzte Wörter, fügen Sie den Begriff als innerer Text von einem Wörterbuch/Akronyme/CasingExceptions / Acronym-Element. Das Akronym in das Wörterbuch/Akronyme/CasingExceptions/Acronym-Element ist die Groß-/Kleinschreibung beachtet.

**Beispiel**

```xml
<Dictionary>
      <Acronyms>
         <CasingExceptions>
            <Acronym>NESW</Acronym>   <!-- North East South West -->
            ...
         </CasingExceptions>
         ...
      </Acronyms>
      ...
</Dictionary>
```

Begriffe im Wörterbuch/Akronyme/CasingExceptions-Knoten werden auf die folgenden Codeanalyseregeln angewendet:

- [CA1709: Bezeichner sollten beachtet werden](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

## <a name="BKMK_ToApplyACustomDictionaryToAProject"></a> Ein benutzerdefiniertes Wörterbuch in ein Projekt anwenden

1. In **Projektmappen-Explorer**, verwenden Sie eine der folgenden Verfahren:

2. Um ein Wörterbuch in ein einzelnes Projekt hinzuzufügen, mit der rechten Maustaste in des Namens des Projekts, und klicken Sie dann auf **vorhandenes Element hinzufügen**. Geben Sie die Datei in die **vorhandenes Element hinzufügen** Dialogfeld.

3. Um ein Wörterbuch hinzuzufügen, die von zwei oder mehr Projekte gemeinsam genutzt wird, suchen Sie die Datei in Teilen der **vorhandenes Element hinzufügen** Dialogfeld klicken Sie auf den Pfeil nach unten auf der **hinzufügen** Schaltfläche, und klicken Sie dann auf **als Link hinzufügen** .

4. In **Projektmappen-Explorer**, mit der rechten Maustaste die **CustomDictionary.xml** Dateinamen, und klicken Sie auf **Eigenschaften**.

5. Von der **Buildvorgang** Liste **"CodeAnalysisDictionary"** .

6. Von der **in Ausgabeverzeichnis kopieren** Liste **nicht kopieren**.