---
title: Codegenerierung in einem Buildprozess
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: b3d61a5bcd530afb951f98f84f1f4e38e36f96d6
ms.sourcegitcommit: 9cfd3ef6c65f671a26322320818212a1ed5955fe
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533308"
---
# <a name="code-generation-in-a-build-process"></a>Code Generierung in einem Buildprozess

Die [Text Transformation](../modeling/code-generation-and-t4-text-templates.md) kann als Teil des [Buildprozesses](/azure/devops/pipelines/index) einer Visual Studio-Projekt Mappe aufgerufen werden. Es gibt Buildaufgaben, die für die Texttransformation angegeben wurden. Die T4-Buildaufgaben führen Entwurfszeittextvorlagen aus und kompilieren gleichzeitig Laufzeitvorlagen (vorverarbeitete Textvorlagen.)

Je nachdem, welche Build-Engine Sie verwenden, können die Buildaufgaben unterschiedliche Ergebnisse haben. Wenn Sie die Projekt Mappe in Visual Studio erstellen, kann eine Textvorlage auf die Visual Studio-API (EnvDTE) zugreifen, wenn das [hostspecific = "true"](../modeling/t4-template-directive.md) -Attribut festgelegt ist. Dies ist jedoch nicht der Fall, wenn Sie die Projekt Mappe über die Befehlszeile erstellen oder wenn Sie einen Serverbuild über Visual Studio initiieren. In diesen Fällen wird der Build von MSBuild ausgeführt, und ein anderer T4-Host wird verwendet. Dies bedeutet, dass Sie nicht wie Projekt Dateinamen auf die gleiche Weise zugreifen können, wenn Sie eine Textvorlage mithilfe von MSBuild erstellen. Sie können jedoch [Umgebungs Informationen mithilfe von buildparametern in Textvorlagen und direktivenprozessoren übergeben](#parameters).

## <a name="buildserver"></a>Computer konfigurieren

Installieren Sie das Modellierungs-SDK für Visual Studio, um Buildaufgaben auf dem Entwicklungs Computer zu aktivieren.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Wenn der [Buildserver](/azure/devops/pipelines/agents/agents) auf einem Computer ausgeführt wird, auf dem Visual Studio nicht installiert ist, kopieren Sie die folgenden Dateien vom Entwicklungs Computer auf den Buildcomputer. Ersetzen Sie die neuesten Versionsnummern für "*".

- $(ProgramFiles)\MSBuild\Microsoft\VisualStudio\v*.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.*.0.dll

  - Microsoft.TextTemplating.Build.Tasks.dll

  - Microsoft.TextTemplating.targets

- $(ProgramFiles)\Microsoft Visual Studio *.0\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.*.0.dll

  - Microsoft.VisualStudio.TextTemplating.Interfaces.*.0.dll (mehrere Dateien)

  - Microsoft.VisualStudio.TextTemplating.VSHost.*.0.dll

- $(ProgramFiles)\Microsoft Visual Studio *.0\Common7\IDE\PublicAssemblies\

  - Microsoft.VisualStudio.TextTemplating.Modeling.*.0.dll
  
> [!TIP]
> Wenn Sie beim Ausführen `MissingMethodException` von TextTemplating Build-Zielen auf einem Buildserver eine für eine Microsoft. Code Analysis-Methode erhalten, stellen Sie sicher, dass sich die Roslyn-Assemblys in einem Verzeichnis namens *Roslyn* befinden, das sich im selben Verzeichnis wie die ausführbare Build-Datei befindet ( *MSBuild. exe*).

## <a name="edit-the-project-file"></a>Bearbeiten der Projektdatei

Bearbeiten Sie die Projektdatei, um einige der Features in MSBuild zu konfigurieren, z. b. das Importieren der texttransformations-Ziele.

Wählen Sie in **Projektmappen-Explorer**im Kontextmenü des Projekts die Option **entladen** aus. Damit können Sie die CSPROJ- oder VBPROJ-Datei im XML-Editor zu bearbeiten. Wenn Sie die Bearbeitung abgeschlossen haben, klicken Sie auf neu **Laden**.

## <a name="import-the-text-transformation-targets"></a>Importieren der texttransformations-Ziele

Suchen Sie wie folgt eine Zeile in der VBPROJ-Datei oder in der CSPROJ-Datei:

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- oder –

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

Fügen Sie nach dieser Zeile den Textvorlagenimport ein:

```xml
<!-- Optionally make the import portable across VS versions -->
  <PropertyGroup>
    <!-- Get the Visual Studio version: -->
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">16.0</VisualStudioVersion>
    <!-- Keep the next element all on one line: -->
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
  </PropertyGroup>

<!-- This is the important line: -->
  <Import Project="$(VSToolsPath)\TextTemplating\Microsoft.TextTemplating.targets" />
```

## <a name="transform-templates-in-a-build"></a>Transformieren von Vorlagen in einem Build

Einige Eigenschaften, die Sie in die Projektdatei einfügen können, um die Transformationsaufgabe zu steuern:

- Führen Sie die Transformierensaufgabe am Anfang jedes Builds aus:

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- Dateien überschreiben, die schreibgeschützt sind, z. b. weil Sie nicht ausgecheckt sind:

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

- Transformieren Sie jede Vorlage jedes Mal:

    ```xml
    <PropertyGroup>
        <TransformOutOfDateOnly>false</TransformOutOfDateOnly>
    </PropertyGroup>
    ```

     Standardmäßig generiert die T4-MSBuild-Aufgabe erneut eine Ausgabedatei, wenn diese älter ist als:
     
     - die Vorlagen Datei
     - alle enthaltenen Dateien
     - alle Dateien, die zuvor von der Vorlage oder von einem von ihr verwendeten Direktivenprozessor gelesen wurden
     
     Dies ist ein leistungsfähiger Abhängigkeits Test als der von dem Befehl **Transform all Templates** in Visual Studio verwendet wird, der nur die Datumsangaben der Vorlage und der Ausgabedatei vergleicht.

Wenn Sie nur die Texttransformationen im Projekt ausführen möchten, rufen Sie die Aufgabe „TransformAll“ auf:

`msbuild myProject.csproj /t:TransformAll`

Zur Transformation einer bestimmten Textvorlage:

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

In TransformFile können Sie Platzhalter verwenden:

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>Quellcodeverwaltung

Es besteht keine spezifische integrierte Integration in ein Quellcodeverwaltungssystem. Sie können jedoch auch eigene Erweiterungen hinzufügen, um eine generierte Datei auszuchecken und einzuchecken. Standardmäßig vermeidet die Text Transformations Aufgabe das Überschreiben einer Datei, die als schreibgeschützt gekennzeichnet ist. Wenn eine solche Datei gefunden wird, wird ein Fehler in der Visual Studio-Fehlerliste protokolliert, und die Aufgabe schlägt fehl.

Fügen Sie die folgende Eigenschaft ein, um anzugeben, dass schreibgeschützte Dateien überschrieben werden sollen:

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

Wenn Sie den nachträglich verarbeitetes-Schritt nicht anpassen, wird eine Warnung in der Fehlerliste protokolliert, wenn eine Datei überschrieben wird.

## <a name="customize-the-build-process"></a>Anpassen des Buildprozesses

Texttransformation geschieht vor anderen Aufgaben im Buildprozess. Sie können Aufgaben definieren, die vor und nach der Transformation aufgerufen werden, indem Sie die Eigenschaften `$(BeforeTransform)` und `$(AfterTransform)` festlegen:

```xml
<PropertyGroup>
    <BeforeTransform>CustomPreTransform</BeforeTransform>
    <AfterTransform>CustomPostTransform</AfterTransform>
  </PropertyGroup>
  <Target Name="CustomPreTransform">
    <Message Text="In CustomPreTransform..." Importance="High" />
  </Target>
  <Target Name="CustomPostTransform">
    <Message Text="In CustomPostTransform..." Importance="High" />
  </Target>
```

In `AfterTransform` können Sie auf Dateilisten verweisen:

- GeneratedFiles – Eine Liste von Dateien, die vom Prozess geschrieben werden. Für Dateien, die vorhandene schreibgeschützte Dateien überschrieben haben, `%(GeneratedFiles.ReadOnlyFileOverwritten)` trifft zu. Diese Dateien können aus der Quellcodeverwaltung ausgecheckt werden.

- NonGeneratedFiles– Eine Liste von schreibgeschützten Dateien, die nicht überschrieben wurden.

Sie definieren z. B. eine Aufgabe zum Auschecken von GeneratedFiles.

## <a name="outputfilepath-and-outputfilename"></a>OutputFilePath und OutputFileName

Diese Eigenschaften werden nur von MSBuild verwendet. Sie beeinflussen nicht die Codegenerierung in Visual Studio. Sie leiten die generierte Ausgabedatei in einen anderen Ordner oder eine andere Datei um. Der Zielordner muss bereits vorhanden sein.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFilePath>MyFolder</OutputFilePath>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Ein nützlicher Ordner, zu dem umgeleitet `$(IntermediateOutputPath)`werden soll, ist.

Wenn Sie einen Ausgabe Dateinamen angeben, hat dieser Vorrang vor der Erweiterung, die in der Output-Direktive in den Vorlagen angegeben ist.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Das Angeben eines OutputFileName oder outputfilepath ist nicht empfehlenswert, wenn Sie auch Vorlagen in Visual Studio mit **Transform all** oder dem Einzel Datei Generator transformieren. Je nachdem, wie Sie die Transformation ausgelöst haben, werden Sie unterschiedliche Dateipfade erhalten. Dies kann verwirrend sein.

## <a name="add-reference-and-include-paths"></a>Hinzufügen von verweisen und einschließen von Pfaden

Der Host verfügt über einen Standardsatz an Pfaden, in denen er nach Assemblys sucht, auf die von Vorlagen verwiesen wird. So fügen Sie diesem Satz Pfade hinzu:

```xml
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

Stellen Sie eine durch Semikolons getrennte Liste bereit, um die Ordner festzulegen, in denen nach Includedateien gesucht wird. Normalerweise fügen Sie der vorhandenen Liste Pfade hinzu.

```xml
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

## <a name="parameters"></a>Übergeben von buildkontextdaten an die Vorlagen

Sie können Parameterwerte in der Projektdatei festlegen. Beispielsweise können Sie [Buildeigenschaften und](../msbuild/msbuild-properties.md) [Umgebungsvariablen](../msbuild/how-to-use-environment-variables-in-a-build.md)übergeben:

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

Legen Sie in einer Textvorlage `hostspecific` in der template-Direktive fest. Verwenden Sie die [Parameter](../modeling/t4-parameter-directive.md) Direktive, um Werte zu erhalten:

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

In einem Direktivenprozessor können Sie [itexttemplatingenginehost. resolveparametervalue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))aufrufen:

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> `ResolveParameterValue` ruft Daten nur dann aus `T4ParameterValues` ab, wenn Sie MSBuild verwenden. Wenn Sie die Vorlage mit Visual Studio transformieren, haben die Parameter Standardwerte.

## <a name="msbuild"></a>Verwenden von Projekteigenschaften in Assembly-und Includedirektiven

Visual Studio-Makros wie **$ (SolutionDir)** funktionieren nicht in MSBuild. Sie können stattdessen Projekteigenschaften verwenden.

Bearbeiten Sie die *csproj* -oder *vbproj* -Datei, um eine Projekt Eigenschaft zu definieren. In diesem Beispiel wird eine Eigenschaft mit dem Namen **mylibfolder**definiert:

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

Nun können Sie die Projekteigenschaft in der Assembly- und der Includedirektive verwenden:

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
<#@ include file="$(myLibFolder)\MyIncludeFile.t4" #>
```

Diese Direktiven rufen Werte von T4parameterValues in MSBuild- und Visual Studio-Hosts ab.

## <a name="q--a"></a>Fragen und Antworten

**Warum sollte ich Vorlagen auf dem Buildserver transformieren? Ich habe bereits Vorlagen in Visual Studio transformiert, bevor ich den Code eingecheckte.**

Wenn Sie eine enthaltene Datei oder eine andere von der Vorlage gelesene Datei aktualisieren, transformiert Visual Studio die Datei nicht automatisch. Durch das Transformieren von Vorlagen als Teil des Builds wird sichergestellt, dass alles auf dem neuesten Stand ist.

**Welche anderen Optionen gibt es für die Transformation von Textvorlagen?**

- Das [textTransform-Hilfsprogramm](../modeling/generating-files-with-the-texttransform-utility.md) kann in Befehls Skripts verwendet werden. In den meisten Fällen ist es einfacher, MSBuild zu verwenden.

- [Aufrufen von Text Transformation in einer Visual Studio-Erweiterung](../modeling/invoking-text-transformation-in-a-vs-extension.md).

- [Entwurfszeit-Textvorlagen](../modeling/design-time-code-generation-by-using-t4-text-templates.md) werden von Visual Studio transformiert.

- [Lauf Zeit Textvorlagen](../modeling/run-time-text-generation-with-t4-text-templates.md) werden zur Laufzeit in der Anwendung transformiert.

## <a name="see-also"></a>Siehe auch

::: moniker range="vs-2017"

- In der T4-MSBuild-Vorlage unter *% Program Files (x86)% \ Microsoft Visual Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets* gibt es eine gute Anleitung.

::: moniker-end

::: moniker range=">=vs-2019"

- In der T4-MSBuild-Vorlage unter *% Program Files (x86)% \ Microsoft Visual Studio\2019\Enterprise\msbuild\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets* gibt es eine gute Anleitung.

::: moniker-end

- [Schreiben einer T4-Textvorlage](../modeling/writing-a-t4-text-template.md)
