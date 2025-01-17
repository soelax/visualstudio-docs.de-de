---
title: Analyzer-Regelsätze
ms.date: 04/22/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, rule sets
- rule sets for analyzers
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 696e6bd46c17054494be2ea0e0f2a1af4fd703d7
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675488"
---
# <a name="rule-sets-for-roslyn-analyzers"></a>Regelsätze für Roslyn-Analysetools

Vordefinierten Regelsätzen sind einige Analyzer-NuGet-Pakete enthalten. Z. B. die Regelsätze, die enthalten sind die [Microsoft.CodeAnalysis.FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) NuGet-Analyzer-Paket (ab Version 2.6.2) aktivieren oder Deaktivieren von Regeln basierend auf ihrer Kategorie, z. B. Sicherheit, Benennung von oder die Leistung. Verwenden von Regelsätzen erleichtert es, nur diese Verletzungen von Namensregeln schnell zu erkennen, die auf einer bestimmten Kategorie der Regel beziehen.

Wenn Sie über ältere "FxCop" statische Codeanalyse zu Roslyn-Analysetools migrieren, aktivieren diese Regelsätze Sie weiterhin mithilfe der gleichen Regelkonfigurationen, die Sie zuvor verwendet.

## <a name="use-analyzer-rule-sets"></a>Verwenden von Regelsätzen für analyzer

Nach dem [installieren ein NuGet-Pakets Analyzer](install-roslyn-analyzers.md), suchen Sie die vordefinierten Regeln in der *Rulesets* Verzeichnis. Z. B., wenn Sie einen Verweis auf die `Microsoft.CodeAnalysis.FxCopAnalyzers` analyzerpaket, Sie finden die *Rulesets* Verzeichnis *% USERPROFILE%\\.nuget\packages\microsoft.codeanalysis.fxcopanalyzers\\ \<Version\>\rulesets*. Von dort kopieren Sie eine oder mehrere der die Rulesets aus, und fügen Sie sie in das Verzeichnis mit Visual Studio-Projekt oder direkt in **Projektmappen-Explorer**.

Sie können auch [Anpassen eines vordefinierten Regelsatzes](how-to-create-a-custom-rule-set.md) nach Bedarf. Sie können z. B. den Schweregrad der eine oder mehrere Regeln ändern, sodass Verletzungen als Fehler oder Warnungen angezeigt werden. die **Fehlerliste**.

## <a name="set-the-active-rule-set"></a>Legen Sie die aktiven Regelsatz

Der Prozess zum Festlegen der aktiven Regelsatz ist ein wenig anders, abhängig davon, ob Sie eine .NET Core und .NET Standard-Projekt oder ein Projekt .NET Framework.

### <a name="net-core"></a>.NET Core

Um einen Regelsatz zu den aktiven Regelsatz für die Analyse in .NET Core oder .NET Standard-Projekten zu machen, fügen Sie manuell die **CodeAnalysisRuleSet** Eigenschaft zu Ihrer Projektdatei. Im folgenden code wird beispielsweise Codeausschnitt legt `HelloWorld.ruleset` als aktiven Regelsatz festgelegt.

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

### <a name="net-framework"></a>.NET Framework

Damit wird eine Regel, die den aktiven Regelsatz für die Analyse in .NET Framework-Projekten festgelegt, mit der Maustaste, auf das Projekt im **Projektmappen-Explorer** , und wählen Sie **Eigenschaften**. Wählen Sie in den Eigenschaftenseiten des Projekts, das **Codeanalyse** Registerkarte. Klicken Sie unter **diesen Regelsatz ausführen**Option **Durchsuchen**, und wählen Sie dann den gewünschten Regelsatz, den Sie in das Projektverzeichnis kopiert. Jetzt sehen Sie nur Verletzungen von Namensregeln für solche Regeln, die im ausgewählten Regelsatz aktiviert sind.

## <a name="available-rule-sets"></a>Verfügbare Regelsätze

Der vordefinierte Analyse Regel umfassen drei Regelsätze, die alle Regeln im Paket betreffen&mdash;eine, die alle ermöglicht, eine, die alle deaktiviert, und eine, die Standardeinstellungen Schweregrad und die Aktivierung für jede Regel berücksichtigt:

- AllRulesEnabled.ruleset
- AllRulesDisabled.ruleset
- AllRulesDefault.ruleset

Darüber hinaus stehen zwei Regelsätze für die einzelnen Kategorien von Regeln, die im Paket, z. B. die Leistung oder Sicherheit. Ein Regelsatz aktiviert alle Regeln für die Kategorie aus, und ein Regelsatz berücksichtigt die Einstellungen der Schweregrad und die Aktivierung für jede Regel in der Kategorie.

Die [Microsoft.CodeAnalysis.FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) Analyzer NuGet-Paket enthält die Regelsätze für die folgenden Kategorien, die die Übereinstimmung der Regelsätze für ältere "FxCop" statische Codeanalyse verfügbar:

- Entwurf
- Dokumentation
- Verwaltbarkeit
- Benennen
- Leistung
- Zuverlässigkeit
- Sicherheit
- Verwendung

## <a name="see-also"></a>Siehe auch

- [FAQ zu Analysetools](analyzers-faq.md)
- [Overview of .NET Compiler Platform analyzers (Übersicht über .NET Compiler Platform-Analysetools)](roslyn-analyzers-overview.md)
- [Installieren von Analysen](install-roslyn-analyzers.md)
- [Verwenden von Analysen](use-roslyn-analyzers.md)
- [Verwenden von Regelsätzen zum Gruppe von Codeanalyseregeln](using-rule-sets-to-group-code-analysis-rules.md)
