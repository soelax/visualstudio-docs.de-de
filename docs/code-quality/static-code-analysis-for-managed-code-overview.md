---
title: Codeanalyse für verwalteten Code
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6c2202103bbff9de75921fba18f842f633419587
ms.sourcegitcommit: fd5a5b057df3d733f5224c305096907989811f85
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2019
ms.locfileid: "67196389"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Übersicht über die Codeanalyse für verwalteten Code in Visual Studio

Visual Studio Codeanalyse von verwaltetem Code ausführen kann, gibt es zwei Möglichkeiten: mit [binäre Analysen](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md), auch bekannt als FxCop statische Analyse der verwaltete Assemblys, und klicken Sie mit der moderner [Roslyn-Analysetools](../code-quality/roslyn-analyzers-overview.md). Dieses Thema behandelt die Analyse von statischem Code FxCop. Weitere Informationen zum Analysieren von Code mithilfe der Quell-Analyzer finden Sie unter [Übersicht der Roslyn-Analysetools](../code-quality/roslyn-analyzers-overview.md).

Codeanalyse für verwalteten Code analysiert verwaltete Assemblys und Informationen zu den Assemblys, z. B. Verstöße gegen die Programmier- und Entwurfsregeln Regeln dargelegten die [Entwurfsrichtlinien von .NET](/dotnet/standard/design-guidelines/).

Das Analysetool stellt die während einer Analyse durchgeführten Prüfungen als Warnmeldungen dar. In diesen Warnmeldungen werden alle relevanten Probleme im Zusammenhang mit Programmierung und Entwurf benannt. Nach Möglichkeit wird außerdem angegeben, wie das jeweilige Problem gelöst werden kann.

> [!NOTE]
> Analyse von statischem Code wird für .NET Core und .NET Standard-Projekte in Visual Studio nicht unterstützt. Wenn Sie die Codeanalyse für ein Projekt für .NET Core oder .NET Standard als Teil von Msbuild ausführen, sehen Sie eine Fehlermeldung ähnlich **Fehler: CA0055 : Plattform für konnte nicht identifiziert \<your.dll >** . Verwenden Sie zum Analysieren von Code in Projekten auf .NET Core oder .NET Standard [Roslyn-Analysetools](../code-quality/roslyn-analyzers-overview.md) stattdessen.

## <a name="ide-integrated-development-environment-integration"></a>Integration von IDE (integrierte Entwicklungsumgebung)

Sie können die Codeanalyse manuell oder automatisch auf das Projekt ausführen.

Um die Codeanalyse immer auszuführen, die Sie ein Projekt erstellen, wählen Sie **Codeanalyse für Build aktivieren** auf der Eigenschaftenseite des Projekts. Weitere Informationen finden Sie unter [Vorgehensweise: Enable and Disable Automatic Code Analysis (Vorgehensweise: Aktivieren und Deaktivieren der automatischen Codeanalyse)](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).

Die Codeanalyse manuell an einem Projekt ausführen, wählen Sie in der Menüleiste **analysieren** > **Codeanalyse ausführen** > **Ausführen der Codeanalyse für \<Projekt >** .

## <a name="rule-sets"></a>Regelsätze

Codeanalyseregeln für verwalteten Code werden in [Regelsätze](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) gruppiert. Sie können eines der Microsoft-Standardregelsätze verwenden, oder Sie können [Erstellen eines benutzerdefinierten Regelsatzes](../code-quality/how-to-create-a-custom-rule-set.md) auf eine bestimmte Anforderung zu erfüllen.

## <a name="suppress-warnings"></a>Unterdrücken von Warnungen

Es kann häufig hilfreich sein anzugeben, dass eine Warnung nicht zutreffend ist. Entwickler und andere Personen, die später möglicherweise den Code überprüfen, wissen dann, dass eine Warnung untersucht und unterdrückt oder ignoriert wurde.

Unterdrückung von Warnungen im Quellcode wird über benutzerdefinierte Attribute implementiert. Fügen Sie zum Unterdrücken einer Warnung das Attribut `SuppressMessage` zum Quellcode hinzu, wie im folgenden Beispiel dargestellt:

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
Public class MyClass
{
   // code
}
```

Weitere Informationen finden Sie unter [Unterdrücken von Warnungen](../code-quality/in-source-suppression-overview.md).

> [!NOTE]
> Wenn Sie ein Projekt in Visual Studio 2017 oder Visual Studio-2019 migrieren, können Sie mit einer großen Anzahl von Warnungen der Codeanalyse plötzlich konfrontiert werden. Wenn Sie nicht möchten Sie die Warnungen beheben und sofort produktiv werden soll, können Sie *Baseline* den Analyse-Zustand des Projekts. Von der **analysieren** , wählen Sie im Menü **Codeanalyse ausführen und aktive Probleme unterdrücken**.

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>Ausführen der Codeanalyse im Rahmen der Eincheckrichtlinien

In einer Organisation ist es sinnvoll festzulegen, dass beim Einchecken stets bestimmte Richtlinien beachtet werden müssen. Insbesondere die folgenden Richtlinien sollten eingehalten werden:

- Es gibt keine Buildfehler im Code eingecheckt wird.

- Die Codeanalyse wird als Teil des neuesten Builds ausgeführt.

Die Einhaltung dieser Vorgaben können Sie durch das Definieren von Eincheckrichtlinien gewährleisten. Weitere Informationen finden Sie unter [Verbessern der Codequalität mit Eincheckrichtlinien für das Projekt](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md).

## <a name="team-build-integration"></a>Team Build-integration

Sie können die integrierten Features des Buildsystems verwenden, um das Analysetool im Rahmen des Buildprozesses auszuführen. Weitere Informationen finden Sie unter [Azure Pipelines](/azure/devops/pipelines/index?view=vsts).

## <a name="see-also"></a>Siehe auch

- [Übersicht über die Roslyn-Analysetools](../code-quality/roslyn-analyzers-overview.md)
- [Verwenden von Regelsätzen zum Gruppieren von Codeanalyseregeln](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [Vorgehensweise: Enable and Disable Automatic Code Analysis (Vorgehensweise: Aktivieren und Deaktivieren der automatischen Codeanalyse)](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
