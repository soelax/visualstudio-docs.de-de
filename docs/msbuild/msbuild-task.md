---
title: MSBuild-Aufgabe | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#MSBuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild task [MSBuild]
- MSBuild, MSBuild task
ms.assetid: 76577f6c-7669-44ad-a840-363e37a04d34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a58235b724f97e3934ab620677e530fbd9ba9726
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747356"
---
# <a name="msbuild-task"></a>MSBuild-Aufgabe
Erstellt [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Projekte aus einem anderen [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Projekt.

## <a name="parameters"></a>Parameter
 In der folgenden Tabelle werden die Parameter der `MSBuild` -Aufgabe beschrieben.

| Parameter | Beschreibung |
|-----------------------------------| - |
| `BuildInParallel` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, werden die gemäß `Projects`-Parameter angegebenen Projekte nach Möglichkeit gleichzeitig erstellt. Der Standardwert ist `false`. |
| `Projects` | Erforderlicher <xref:Microsoft.Build.Framework.ITaskItem>`[]`-Parameter.<br /><br /> Gibt die zu erstellenden Projektdateien an. |
| `Properties` | Optionaler `String` -Parameter.<br /><br /> Eine durch Semikolons getrennte Liste der Eigenschaftenname-Wert-Paare, die als globale Eigenschaften auf das untergeordnete Projekt angewendet werden. Wenn Sie diesen Parameter angeben, entspricht sie funktional dem Festlegen von Eigenschaften, die beim Erstellen mit [*MSBuild.exe*](../msbuild/msbuild-command-line-reference.md) den Schalter **-property** aufweisen. Beispiel:<br /><br /> `Properties="Configuration=Debug;Optimize=$(Optimize)"`<br /><br /> Wenn Sie Eigenschaften mithilfe des `Properties`-Parameters in das Projekt übergeben, erstellt [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] selbst dann eine neue Instanz des Projekts, wenn die Datei bereits geladen wurde. Wurde eine neue Instanz des Projekts erstellt, behandelt [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] diese als ein anderes Projekt mit anderen globalen Eigenschaften, das gleichzeitig mit anderen Instanzen des Projekts erstellt werden kann. So können z.B. eine Releasekonfiguration und eine Debugkonfiguration gleichzeitig erstellen. |
| `RebaseOutputs` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, werden die Pfade der relativen Pfade von Zielausgabeelementen der erstellten Projekte angepasst, damit sie relativ zum aufrufenden Projekt sind. Der Standardwert ist `false`. |
| `RemoveProperties` | Optionaler `String` -Parameter.<br /><br /> Gibt die zu entfernenden globalen Eigenschaften an. |
| `RunEachTargetSeparately` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, ruft die [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Aufgabe die einzelnen an [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] übergebenen Ziele in der Liste nicht gleichzeitig, sondern nacheinander auf. Wenn für diesen Parameter `true` eingestellt wird, ist gewährleistet, dass nachfolgende Ziele selbst dann aufgerufen werden, wenn zuvor aufgerufene Ziele nicht erfolgreich waren. Ansonsten würde ein Buildfehler den Aufruf aller nachfolgenden Ziele beenden. Der Standardwert ist `false`. |
| `SkipNonexistentProjects` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, werden Projektdateien übersprungen, die sich nicht auf dem Datenträger befinden. Ansonsten verursachen Projekte dieser Art einen Fehler. |
| `StopOnFirstFailure` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, wenn eines der Projekte nicht erstellt werden kann, werden keine weiteren Projekte erstellt. Dies wird zurzeit nicht unterstützt, wenn Sie gleichzeitig (mit mehreren Prozessoren) erstellen. |
| `TargetAndPropertyListSeparators` | Optionaler `String[]` -Parameter.<br /><br /> Gibt eine Liste mit Zielen und Eigenschaften als `Project`-Elementmetadaten an. Bei Trennzeichen werden vor der Verarbeitung die Escapezeichen entfernt. So wird z.B. % 3 b (';' mit Escapezeichen) behandelt, als wäre es ein ';' ohne Escapezeichen. |
| `TargetOutputs` | Optionaler schreibgeschützter <xref:Microsoft.Build.Framework.ITaskItem>`[]`-Parameter.<br /><br /> Gibt die Ausgaben der erstellten Ziele von allen Projektdateien zurück. Es werden nur die Ausgaben der angegebenen Ziele zurückgegeben, jedoch keine Ausgaben, die möglicherweise für Ziele vorhanden sind, von denen diese Ziele abhängen.<br /><br /> Der `TargetOutputs`-Parameter enthält zudem die folgenden Metadaten:<br /><br /> -   `MSBuildSourceProjectFile`: Die [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Projektdatei, die das Ziel enthält, das die Ausgaben festlegt.<br />-   `MSBuildSourceTargetName`: Das Ziel, das die Ausgaben festlegt. **Hinweis**:  Wenn Sie die Ausgaben einzelner Projektdateien oder Ziele separat ermitteln möchten, führen Sie die `MSBuild`-Aufgabe für jede Projektdatei und jedes Ziel einzeln aus. Wenn Sie die `MSBuild`-Aufgabe zum Erstellen aller Projektdateien nur einmal ausführen, werden die Ausgaben aller Ziele in einem Array zusammengefasst. |
| `Targets` | Optionaler `String` -Parameter.<br /><br /> Das Ziel oder die Ziele, die in den Projektdateien erstellt werden sollen. Verwenden Sie Semikolons, um eine Liste von Zielnamen zu trennen. Sind in der `MSBuild` Aufgabe keine Ziele angegeben, werden die in den Projektdateien angegebenen Standardziele erstellt. **Hinweis**:  Die jeweiligen Ziele müssen in allen Projektdateien auftreten. Wenn dies nicht der Fall ist, tritt ein Buildfehler auf. |
| `ToolsVersion` | Optionaler `String` -Parameter.<br /><br /> Gibt die `ToolsVersion` an, die verwendet werden muss, um Projekte zu erstellen, die an diese Aufgabe übergeben werden.<br /><br /> Ermöglicht es einem [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Task, ein Projekt zu erstellen, das auf eine Version von .NET Framework abzielt, die von der im Projekt angegebenen Version abweicht. Gültige Werte sind `2.0`, `3.0` und `3.5`. Der Standardwert lautet `3.5`. |
| `UnloadProjectsOnCompletion` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, wird das Projekt entladen, sobald der Vorgang abgeschlossen ist. |
| `UseResultsCache` | Optionaler `Boolean` -Parameter.<br /><br /> Wenn `true`, wird das zwischengespeicherte Ergebnis zurückgegeben (sofern vorhanden).<br /><br />  Wenn die MSBuild-Aufgabe ausgeführt wird, wird das Ergebnis in einem Bereich zwischengespeichert. <br /><br /> (ProjectFileName, GlobalProperties)[TargetNames]<br /><br /> als Liste von Buildelementen zwischengespeichert. |

## <a name="remarks"></a>Anmerkungen
 Zusätzlich zu den oben aufgeführten Parametern erbt diese Aufgabe Parameter von der <xref:Microsoft.Build.Tasks.TaskExtension>-Klasse, die selbst von der <xref:Microsoft.Build.Utilities.Task>-Klasse erbt. Eine Liste mit diesen zusätzlichen Parametern und ihren Beschreibungen finden Sie unter [TaskExtension-Basisklasse](../msbuild/taskextension-base-class.md).

 Anders als beim Starten von [MSBuild.exe](../msbuild/exec-task.md) mithilfe der *Exec-Aufgabe* verwendet diese Aufgabe denselben [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Prozess, um die untergeordneten Projekte zu erstellen. Die Liste bereits erstellter Ziele, die übersprungen werden können, wird sowohl von den übergeordneten als auch von den untergeordneten Builds genutzt. Diese Aufgabe ist zudem schneller, da kein neuer [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Prozess erstellt wird.

 Diese Aufgabe kann nicht nur Projektdateien, sondern auch Projektmappendateien verarbeiten.

 Alle Konfigurationen, mit denen [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] Projekten das gleichzeitige Erstellen ermöglicht, müssen mithilfe einer Konfigurationsdatei konfigurierbar gemacht werden. Dies gilt selbst dann, wenn die Konfiguration Remoteinfrastruktur (z.B. Ports, Protokolle, Timeouts, Wiederholungen usw.) umfasst. Konfigurationselemente sollten nach Möglichkeit während der `MSBuild`-Aufgabe als Aufgabenparameter angegeben werden können.

 Ab [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5 stellen Projektmappenprojekte „TargetOutputs“ aus den jeweils erstellten Unterprojekten bereit.

## <a name="pass-properties-to-projects"></a>Übergeben von Eigenschaften an Projekte
 In Versionen von [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] vor [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5 war das Übergeben unterschiedlicher Sätze von Eigenschaften in andere im [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Element aufgeführte Projekte sehr anspruchsvoll. Wenn Sie das Attribut „Properties“ der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) verwendet haben, wurde die jeweilige Einstellung nur dann auf alle erstellten Projekte angewendet, wenn Sie die [MSBuild-Aufgabe](../msbuild/msbuild-task.md) als Batch verarbeitet und bedingt unterschiedliche Eigenschaften für die einzelnen Projekte in der Elementliste bereitgestellt haben.

 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 3.5: Mit „Properties“ und „AdditionalProperties“ werden in dieser Version jedoch zwei neue reservierte Metadatenelemente bereitgestellt, mit denen Sie auf flexible Weise unterschiedliche Eigenschaften für verschiedene Projekte übergeben können, die mithilfe der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) erstellt werden.

> [!NOTE]
> Diese neuen Metadatenelemente gelten nur für Elemente, die im Attribut „Projects“ der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) übergeben werden.

## <a name="multi-processor-build-benefits"></a>Buildvorteile bei mehreren Prozessoren
 Einer der Hauptvorteile bei der Verwendung dieser neuen Metadaten zeigt sich, wenn Sie Projekte gleichzeitig auf einem System mit mehreren Prozessoren erstellen. Mithilfe der Metadaten können Sie alle Projekte in einem einzelnen Aufruf der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) konsolidieren, ohne eine Batchverarbeitung oder bedingte [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]-Aufgaben ausführen zu müssen. Und wenn Sie nur eine einzige [MSBuild-Aufgabe](../msbuild/msbuild-task.md) aufrufen, werden alle im Attribut „Projects“ aufgelisteten Projekte gleichzeitig erstellt. (Dies gilt allerdings nur, wenn das `BuildInParallel=true`-Attribut in der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) vorhanden ist.) Weitere Informationen finden Sie unter [Paralleles Erstellen von mehreren Projekten](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md).

## <a name="properties-metadata"></a>Properties-Metadaten
 Beim Erstellen mehrerer Projektmappendateien mithilfe der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) werden häufig nur unterschiedliche Buildkonfigurationen verwendet. Möglicherweise möchten Sie die Projektmappe a1 mithilfe der Debugkonfiguration und Projektmappe a2 mithilfe der Releasekonfiguration erstellen. In [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0 würde diese Projektdatei wie folgt aussehen:

> [!NOTE]
> Im folgenden Beispiel stellt „…“ zusätzliche Projektmappendateien dar.

### <a name="aproj"></a>a.proj

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="Build">
        <MSBuild Projects="a1.sln..." Properties="Configuration=Debug"/>
        <MSBuild Projects="a2.sln" Properties="Configuration=Release"/>
    </Target>
</Project>
```

 Mithilfe von Properties-Metadaten können Sie dies nun vereinfachen, um eine einzige [MSBuild-Aufgabe](../msbuild/msbuild-task.md) wie folgt zu verwenden:

### <a name="aproj"></a>a.proj

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <ProjectToBuild Include="a1.sln...">
            <Properties>Configuration=Debug</Properties>
        </ProjectToBuild>
        <ProjectToBuild Include="a2.sln">
            <Properties>Configuration=Release</Properties>
        </ProjectToBuild>
    </ItemGroup>
    <Target Name="Build">
        <MSBuild Projects="@(ProjectToBuild)"/>
    </Target>
</Project>
```

 \- oder –

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <ProjectToBuild Include="a1.sln..."/>
        <ProjectToBuild Include="a2.sln">
            <Properties>Configuration=Release</Properties>
        </ProjectToBuild>
    </ItemGroup>
    <Target Name="Build">
        <MSBuild Projects="@(ProjectToBuild)"
          Properties="Configuration=Debug"/>
    </Target>
</Project>
```

## <a name="additionalproperties-metadata"></a>AdditionalProperties-Metadaten
 Gehen Sie vom folgenden Szenario aus, in dem Sie zwei Projektmappendateien mithilfe der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) erstellen. Beide Dateien werden mithilfe der Releasekonfiguration erstellt, aber für die eine Datei wird die X86-Architektur und für die andere die ia64-Architektur verwendet. In [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0 müssten Sie mehrere Instanzen der [MSBuild-Aufgabe](../msbuild/msbuild-task.md) erstellen: Eine Instanz zum Erstellen des Projekts mithilfe der Releasekonfiguration und der X86-Architektur, die andere zum Erstellen des Projekts mithilfe der Releasekonfiguration und der ia64-Architektur. Die Projektdatei würde wie folgt aussehen:

### <a name="aproj"></a>a.proj

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="Build">
        <MSBuild Projects="a1.sln..." Properties="Configuration=Release;
          Architecture=x86"/>
        <MSBuild Projects="a2.sln" Properties="Configuration=Release;
          Architecture=ia64"/>
    </Target>
</Project>
```

 Mithilfe von AdditionalProperties-Metadaten können Sie dies nun vereinfachen, um eine einzige [MSBuild-Aufgabe](../msbuild/msbuild-task.md) wie folgt zu verwenden:

### <a name="aproj"></a>a.proj

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <ProjectToBuild Include="a1.sln...">
            <AdditionalProperties>Architecture=x86
              </AdditionalProperties>
        </ProjectToBuild>
        <ProjectToBuild Include="a2.sln">
            <AdditionalProperties>Architecture=ia64
              </AdditionalProperties>
        </ProjectToBuild>
    </ItemGroup>
    <Target Name="Build">
        <MSBuild Projects="@(ProjectToBuild)"
          Properties="Configuration=Release"/>
    </Target>
</Project>
```

## <a name="example"></a>Beispiel
 Im folgenden Beispiel werden die von der Elementauflistung `ProjectReferences` angegebenen Projekte mithilfe der `MSBuild`-Aufgabe erstellt. Die entsprechenden Zielausgaben werden in der Elementauflistung `AssembliesBuiltByChildProjects` gespeichert.

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <ProjectReferences Include="*.*proj" />
    </ItemGroup>

    <Target Name="BuildOtherProjects">
        <MSBuild
            Projects="@(ProjectReferences)"
            Targets="Build">
            <Output
                TaskParameter="TargetOutputs"
                ItemName="AssembliesBuiltByChildProjects" />
        </MSBuild>
    </Target>

</Project>
```

## <a name="see-also"></a>Siehe auch
- [Aufgaben](../msbuild/msbuild-tasks.md)
- [Referenz zu MSBuild-Tasks](../msbuild/msbuild-task-reference.md)