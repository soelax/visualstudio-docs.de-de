---
title: Verwenden von ModelBus in einer Text Vorlage | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 5ed3e5c2-f60f-43c7-8ef4-754f511339c5
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 672efc49d712d9cd800bf53a2ca8487c96d502b6
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871681"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>Verwenden von Visual Studio-ModelBus in einer Textvorlage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Wenn Sie Textvorlagen schreiben, die ein Modell lesen, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] das ModelBus-Verweise enthält, können Sie die Verweise auflösen, um auf die Ziel Modelle zuzugreifen. In diesem Fall müssen Sie die Textvorlagen und die referenzierten domänenspezifische Sprachen (DSLs) anpassen:

- Die DSL, die das Ziel der Verweise müssen einen ModelBus-Adapter, der für den Zugriff von Textvorlagen konfiguriert ist. Wenn Sie die DSL als auch von anderem Code zugreifen, ist der neu konfigurierten zusätzlich zu den standardmäßigen ModelBus-Adapter erforderlich.

     Der Adapter-Manager muss von [vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140)) erben und muss über das `[HostSpecific(HostName)]`-Attribut verfügen.

- Die Vorlage muss von [modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140))erben.

> [!NOTE]
> Wenn Sie möchten die DSL-Modelle zu lesen, die keine ModelBus-Verweise enthalten, können Sie anweisungsprozessoren, die in den DSL-Projekten generiert werden. Weitere Informationen finden Sie unter [zugreifen auf Modelle aus Textvorlagen](../modeling/accessing-models-from-text-templates.md).

 Weitere Informationen zu Textvorlagen finden Sie unter [Design-Time Code Generation mithilfe von T4-Textvorlagen](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

## <a name="creating-a-model-bus-adapter-for-access-from-text-templates"></a>Erstellen eine Modellbusadapter für den Zugriff von Textvorlagen
 Um ein ModelBus-Verweis in einer Textvorlage zu beheben, müssen die Ziel-DSL einen kompatiblen Adapter. Text Vorlagen werden in einer separaten AppDomain aus den [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Dokument-Editoren ausgeführt. Daher muss der Adapter das Modell laden, anstatt über DTE darauf zuzugreifen.

#### <a name="to-create-a-modelbus-adapter-that-is-compatible-with-text-templates"></a>Um einen ModelBus-Adapter zu erstellen, die mithilfe von Textvorlagen kompatibel ist

1. Wenn das Ziel-DSL-Projektmappe keine **ModelBusAdapter** Projekt, erstellen Sie eine mit dem Assistenten für die Modelbus-Erweiterung:

    1. Laden Sie die [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus-Erweiterung herunter, und installieren Sie Sie, falls Sie dies noch nicht getan haben. Weitere Informationen finden Sie unter [Visualisierungs- und Modellierungs-SDK](http://go.microsoft.com/fwlink/?LinkID=185579).

    2. Öffnen Sie die DSL-Definitionsdatei. Mit der rechten Maustaste in der Entwurfsoberfläche, und klicken Sie dann auf **Modelbus aktivieren**.

    3. Wählen Sie im Dialogfeld **ich möchte diese DSL für ModelBus verfügbar machen**. Sie können beide Optionen auswählen, wenn Sie diese DSL Modelle verfügbar machen und Verweise auf andere DSLs nutzen möchten.

    4. Klicken Sie auf **OK**. Der DSL-Projektmappe wird ein neues ModelBusAdapter-Projekt hinzugefügt.

    5. Klicken Sie auf **alle Vorlagen transformieren**.

    6. Generieren Sie die Projektmappe neu.

2. Duplizieren Sie ggf. die DSL von einer Textvorlage sowohl von anderem Code, z. B.-Befehl, den Zugriff auf die **ModelBusAdapter** Projekt:

    1. Kopieren Sie in Windows Explorer, und fügen Sie den Ordner mit **ModelBusAdapter.csproj**.

    2. Benennen Sie die Projektdatei (z. B. **T4ModelBusAdapter.csproj**).

    3. In **Projektmappen-Explorer**mit der rechten Maustaste auf den Projektmappenknoten, zeigen Sie auf **hinzufügen**, und klicken Sie dann auf **vorhandenes Projekt**. Suchen Sie das neue adapterprojekt **T4ModelBusAdapter.csproj**.

    4. In den einzelnen `*.tt` Datei des neuen Projekts, ändern Sie den Namespace.

    5. Mit der rechten Maustaste in des neuen Projekts im Projektmappen-Explorer, und klicken Sie dann auf Eigenschaften. Ändern Sie die Namen der generierten Assembly und den Standardnamespace im Eigenschaften-Editor.

    6. Fügen Sie so, dass sie Verweise auf beide Adapter im DslPackage-Projekt einen Verweis auf das neue adapterprojekt hinzu.

    7. In DslPackage\source.extension.tt Hinzufügen von Zeilen, die auf das neue adapterprojekt verweist.

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **Alle Vorlagen transformieren** und die Projektmappe neu erstellen. Es sollte keine Buildfehler auftreten.

3. Fügen Sie in der neuen adapterprojekt Verweise auf die folgenden Assemblys hinzu:

    - Microsoft.VisualStudio.TextTemplating.11.0

         Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4. In "adaptermanager.tt":

    - Ändern Sie die Deklaration von adaptermanagerbase, sodass Sie von [vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140))erbt.

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - Ersetzen Sie am Ende der Datei die HostSpecific-Attribut vor der AdapterManager-Klasse. Entfernen Sie die folgende Zeile:

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         Fügen Sie die folgende Zeile ein:

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         Dieses Attribut filtert den Satz von Adaptern, der verfügbar ist, wenn ein Modelbus-Consumer für einen Adapter sucht.

5. **Alle Vorlagen transformieren** und die Projektmappe neu erstellen. Es sollte keine Buildfehler auftreten.

## <a name="writing-a-text-template-that-can-resolve-modelbus-references"></a>Schreiben einer Textvorlage, die ModelBus-Verweise auflösen kann
 In der Regel beginnen Sie mit einer Vorlage, die liest und Dateien aus einer DSL "Quelle" generiert. Diese Vorlage verwendet die Richtlinie, die generiert wird, in der Quelle DSL-Projekt zum Modell der Quelldateien in die Art und Weise zu lesen, das beschrieben ist [zugreifen auf Modelle aus Textvorlagen](../modeling/accessing-models-from-text-templates.md). Die Quell-DSL enthält jedoch die ModelBus-Verweise auf eine DSL "Target". Aus diesem Grund möchten Sie den Vorlagencode, lösen Sie die Verweise und Zugriff auf die Ziel-DSL zu aktivieren. Aus diesem Grund müssen Sie die Vorlage anpassen, indem Sie diese Schritte:

- Ändern Sie die Basisklasse der Vorlage in [modelbusenabledtexttransformation](/previous-versions/ee844263(v=vs.140)).

- Umfassen `hostspecific="true"` in der Template-Direktive.

- Fügen Sie Assemblyverweise hinzu, die Ziel-DSL und die Adapter und ModelBus aktivieren.

- Sie benötigen nicht die Richtlinie, die als Teil der Ziel-DSL generiert wird.

```
<#@ template debug="true" hostspecific="true" language="C#"
inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
<#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
<#@ output extension=".txt" #>
<#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
<#@ assembly name = "Company.TargetDsl.Dsl.dll" #>
<#@ assembly name = "Company.TargetDsl.T4ModelBusAdapter.dll" #>
<#@ assembly name = "System.Core" #>
<#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
<#@ import namespace="Company.TargetDsl" #>
<#@ import namespace="Company.TargetDsl.T4ModelBusAdapters" #>
<#@ import namespace="System.Linq" #>
<#
  SourceModelRoot source = this.ModelRoot; // Usual access to source model.
  // In the source DSL Definition, the root element has a model reference:
  using (TargetAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as TargetAdapter)
  {if (adapter != null)
   {
      // Get the root of the target model:
      TargetRoot target = adapter.ModelRoot;
    // The source DSL Definition has a class "SourceElement" embedded under the root.
    // (Let’s assume they’re all in the same model file):
    foreach (SourceElement sourceElement in source.Elements)
    {
      // In the source DSL Definition, each SourceElement has a MBR property:
      ModelBusReference elementReference = sourceElement.ReferenceToTarget;
      // Resolve the target model element:
      TargetElement element = adapter.ResolveElementReference<TargetElement>(elementReference);
#>
     The source <#= sourceElement.Name #> is linked to: <#= element.Name #> in target model: <#= target.Name #>.
<#
    }
  }}
  // Other useful code: this.Host.ResolvePath(filename) gets an absolute filename
  // from a path that is relative to the text template.
#>

```

 Wenn dieser Textvorlage ausgeführt wird, die `SourceDsl` Richtlinie lädt die Datei `Sample.source`. Die Vorlage stehen die Elemente dieses Modells, beginnend mit `this.ModelRoot`. Der Code kann es sich um die Domänenklassen und Eigenschaften für diese DSL verwenden.

 Darüber hinaus kann die Vorlage ModelBus-Verweise aufgelöst werden. Wenn die Verweise auf das Zielmodell verweisen, ermöglichen die assemblydirektiven dem Code, die Domänen Klassen und-Eigenschaften der DSL des Modells zu verwenden.

- Wenn Sie keine Anweisung verwenden, die von einem DSL-Projekt generiert wird, sollten Sie auch Folgendes einschließen.

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- Verwendung `this.ModelBus` , Zugriff auf die ModelBus erhalten.

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>Exemplarische Vorgehensweise: Testen einer Text Vorlage, die ModelBus verwendet
 In dieser exemplarischen Vorgehensweise gehen Sie folgendermaßen vor:

1. Erstellen Sie zwei DSLs. Eine DSL, die *Consumer*, verfügt über eine `ModelBusReference` -Eigenschaft, die auf der anderen DSL verweisen kann, die *Anbieter*.

2. Erstellen Sie zwei ModelBus-Adapter in den Anbieter: eine für den Zugriff durch Textvorlagen, die andere für normalen Code.

3. Erstellen Sie in einem einzelnen Projekt für die experimentelle Instanz Modelle der DSLs.

4. Legen Sie eine Domäneneigenschaft in einem Modell auf das andere Modell verweisen.

5. Schreiben Sie einen Doppelklickhandler, der das Modell wird geöffnet, auf das.

6. Schreiben einer Textvorlage, die das erste Modell zu laden, folgen Sie den Verweis auf das andere Modell und Lesen des anderen Modells kann.

#### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>Erstellen Sie eine DSL, die für ModelBus verfügbar ist.

1. Erstellen Sie eine neue DSL-Projektmappe. In diesem Beispiel wählen Sie die Lösungsvorlage Aufgabenfluss. Legen Sie den Sprachnamen `MBProvider` und die Dateinamenerweiterung zu ".provide".

2. In der DSL-Definitionsdiagramm mit der rechten Maustaste in eines leeren Bereich des Diagramms, die nicht im oberen Bereich, und klicken Sie dann auf **Modelbus aktivieren**.

   - Wenn Sie nicht sehen **Modelbus aktivieren**, müssen Sie herunterladen und installieren die VMSDK-ModelBus-Erweiterung. Diese finden Sie auf der vmsdk-Website: [Visualisierungs-und Modellierungs-SDK](http://go.microsoft.com/fwlink/?LinkID=185579)

3. In der **Modelbus aktivieren** wählen Sie im Dialogfeld **verfügbar zu machen diese DSL für ModelBus**, und klicken Sie dann auf **OK**.

    Ein neues Projekt `ModelBusAdapter`, wird der Projektmappe hinzugefügt.

   Sie verfügen nun über eine DSL, die von Textvorlagen über ModelBus zugegriffen werden kann. Im Code der Befehle, Ereignishandler und Regeln, die in der AppDomain des Modell-Editor-Datei ausgeführt werden, können Verweise auf diese behoben werden. Textvorlagen werden jedoch in einer separaten AppDomain ausgeführt, und es ein Modell können nicht zugegriffen werden, wenn er bearbeitet wird. Wenn Sie ModelBus-Verweise auf diese DSL von einer Textvorlage zugreifen möchten, müssen Sie einen separaten ModelBusAdapter verfügen.

#### <a name="to-create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>Um einen ModelBus-Adapter zu erstellen, die für Textvorlagen konfiguriert ist

1. Klicken Sie im Windows-Explorer kopieren Sie, und fügen Sie den Ordner, der ModelBusAdapter.csproj enthält.

    Nennen Sie den Ordner T4ModelBusAdapter.

    Benennen Sie die Projektdatei T4ModelBusAdapter.csproj.

2. Fügen Sie im Projektmappen-Explorer mit der Lösung MBProvider T4ModelBusAdapter hinzu. Mit der rechten Maustaste des Knotens Projektmappe, zeigen Sie auf **hinzufügen**, und klicken Sie dann auf **vorhandenes Projekt**.

3. Mit der rechten Maustaste des T4ModelBusAdapter-Projektknoten, und klicken Sie dann auf Eigenschaften. Ändern Sie im Fenster für die Projekteigenschaften, die **Assemblyname** und **Default Namespace** zu `Company.MBProvider.T4ModelBusAdapters`.

4. Fügen Sie in jeder Datei tt in T4ModelBusAdapter "T4" in den letzten Teil des Namespace, so, dass die Zeile der folgenden ähnelt.

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. In der `DslPackage` fügen einen Projektverweis auf `T4ModelBusAdapter`.

6. Fügen Sie in DslPackage\source.extension.tt, die folgende Zeile unter `<Content>`.

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. Fügen Sie im Projekt einen Verweis auf hinzu: `T4ModelBusAdapter` **Microsoft.VisualStudio.TextTemplating.Modeling.11.0**

8. Öffnen Sie T4ModelBusAdapter\AdapterManager.tt:

   1. Ändern Sie die Basisklasse von adaptermanagerbase in [vstexttemplatingmodelingadaptermanager](/previous-versions/ee844317(v=vs.140)). Dieser Teil der Datei ähnelt nun dem folgenden.

       ```
       namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters
       {
           /// <summary>
           /// Adapter manager base class (double derived pattern) for the <#= dslName #> Designer
           /// </summary>
           public partial class <#= dslName #>AdapterManagerBase
           : Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager
           {

       ```

   2. Fügen Sie am Ende der Datei die folgende zusätzliche Attribut vor der AdapterManager-Klasse.

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        Das Ergebnis ähnelt dem folgenden Code:

       ```
       /// <summary>
       /// ModelBus modeling adapter manager for a <#= dslName #>Adapter model adapter
       /// </summary>
       [Mef::Export(typeof(DslIntegration::ModelBusAdapterManager))]
       [Mef::ExportMetadata(DslIntegration::CompositionAttributes.AdapterIdKey,<#= dslName #>Adapter.AdapterId)]
       [DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]
       [Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]
       public partial class <#= dslName #>AdapterManager : <#= dslName #>AdapterManagerBase
       {
       }

       ```

9. Klicken Sie auf **alle Vorlagen transformieren** in der Titelleiste des Projektmappen-Explorers.

10. Generieren Sie die Projektmappe neu. Klicken Sie auf F5.

11. Stellen Sie sicher, dass die DSL durch Drücken von F5 ausgeführt wird. Öffnen Sie in der experimentellen Projekt `Sample.provider`. Schließen Sie die experimentelle Instanz von [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

    ModelBus-Verweise auf diese DSL können jetzt in Textvorlagen und auch in normalen Code behoben werden.

#### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>Erstellen Sie eine DSL mit einer Domäneneigenschaft ModelBus-Verweis

1. Erstellen Sie eine neue DSL mithilfe der Lösungsvorlage für die minimale Sprache. Benennen Sie die Sprache MBConsumer, und legen Sie die Dateinamenerweiterung zu ".consume".

2. Fügen Sie einen Verweis auf die Assembly MBProvider DSL im DSL-Projekt hinzu. Mit der rechten Maustaste `MBConsumer\Dsl\References` , und klicken Sie dann auf **Verweis hinzufügen**. In der **Durchsuchen** Registerkarte `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    Dadurch können Sie Code erstellen, die andere DSL verwendet. Wenn Sie Verweise auf mehrere DSLs erstellen möchten, fügen Sie sie auch hinzu.

3. In der DSL-Definitionsdiagramm mit der rechten Maustaste in des Diagramms, und klicken Sie dann auf **ModelBus aktivieren**. Wählen Sie im Dialogfeld **aktivieren diese DSL für ModelBus-Consumer**.

4. In der Klasse `ExampleElement`, fügen Sie eine neue Domäneneigenschaft `MBR`, und legen Sie im Fenster "Eigenschaften", dessen Typ auf `ModelBusReference`.

5. Mit der rechten Maustaste in die Eigenschaft "Domain" im Diagramm, und klicken Sie dann auf **bearbeiten ModelBusReference-spezifische Eigenschaften**. Wählen Sie im Dialogfeld **eines Modellelements**.

    Legen Sie den Dateifilter für das Dialogfeld wie folgt aus.

    `Provider File|*.provide`

    Die Teilzeichenfolge, nach "&#124;" ist ein Filter für das Dialogfeld zur Dateiauswahl. Können Sie festlegen, können Sie Dateien mithilfe von *.\*

    In der **Modellelement Typ** aus, geben Sie die Namen von einer oder mehr Domäne Klassen in der DSL (z. B. Company.MBProvider.Task)-Anbieter. Sie können abstrakte Klassen sein. Wenn Sie die Liste leer lassen, kann der Benutzer den Verweis auf ein Element festlegen.

6. Das Dialogfeld zu schließen und **alle Vorlagen transformieren**.

   Sie haben eine DSL erstellt, die Verweise auf Elemente in einer anderen DSL enthalten kann.

#### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>Erstellen Sie einen ModelBus-Verweis an eine andere Datei, in der Projektmappe

1. Drücken Sie in der Projektmappe MBConsumer STRG + F5. Eine experimentelle Instanz [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] von wird im Projekt **mbconsumer\debugging** geöffnet.

2. Fügen Sie eine Kopie des Sample.provide, um die **MBConsumer\Debugging** Projekt. Dies ist erforderlich, da ein ModelBus-Verweis auf eine Datei in der gleichen Projektmappe verweisen muss.

   1. Mit der rechten Maustaste in den Debugging-Projekt, zeigen Sie auf **hinzufügen**, und klicken Sie dann auf **vorhandenes Element**.

   2. In der **Element hinzufügen** Dialogfeld legen Sie den Filter auf **alle Dateien (\*.\*)** .

   3. Navigieren Sie zu `MBProvider\Debugging\Sample.provide` , und klicken Sie dann auf **hinzufügen**.

3. Öffnen Sie `Sample.consume`.

4. Klicken Sie auf eine Beispiel-Form, und klicken Sie im Fenster Eigenschaften auf **[...]**  in der MBR-Eigenschaft. Klicken Sie im Dialogfeld auf **Durchsuchen** , und wählen Sie `Sample.provide`. Klicken Sie im Fenster Elemente erweitern Sie die Task-Typ, und wählen Sie eines der Elemente.

5. Speichern Sie die Datei.

    (Die experimentelle Instanz von [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]kann noch nicht geschlossen werden.)

   Sie haben ein Modell erstellt, die einen ModelBus-Verweis auf ein Element in einem anderen Modell enthält.

#### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>Lösen Sie ein ModelBus-Verweis in einer Textvorlage

1. Öffnen Sie in der experimentellen [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]Instanz von eine Beispiel-Textvorlagen Datei. Legen Sie den Inhalt wie folgt.

    ```
    <#@ template debug="true" hostspecific="true" language="C#"
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
    <#@ MBConsumer processor="MBConsumerDirectiveProcessor" requires="fileName='Sample.consume'" #>
    <#@ output extension=".txt" #>
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
    <#@ assembly name = "Company.MBProvider.Dsl.dll" #>
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
    <#@ import namespace="Company.MBProvider" #>
    <#
      // Property provided by the Consumer directive processor:
      ExampleModel consumerModel = this.ExampleModel;
      // Iterate through Consumer model, listing the elements:
      foreach (ExampleElement element in consumerModel.Elements)
      {
    #>
       <#= element.Name #>
    <#
        if (element.MBR != null)
      using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(element.MBR))
      {
              // If we allowed multiple types or DSLs in the MBR, discover type here.
        Task task = adapter.ResolveElementReference<Task>(element.MBR);
    #>
            <#= element.Name #> is linked to Task: <#= task==null ? "(null)" : task.Name #>
    <#
          }
      }
    #>

    ```

     Beachten Sie die folgenden Punkte:

    1. Die `hostSpecific` und `inherits` Attribute der `template` Richtlinie muss festgelegt werden.

    2. Der Consumer-Modell wird auf die übliche Weise über den anweisungsprozessor zugegriffen, die in dieser DSL generiert wurde.

    3. Die Assembly "und" Import-Anweisungen müssen ModelBus und die Typen des Anbieters DSL zugreifen können.

    4. Wenn Sie wissen, dass viele MBRs mit dem gleichen Modell verknüpft sind, ist es besser, CreateAdapter nur einmal aufrufen.

2. Sie speichern die Vorlage. Stellen Sie sicher, dass die resultierende Textdatei der folgenden ähnelt.

    ```

    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2

    ```

#### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>Einen ModelBus-Verweis in einen Gestenhandler zu beheben

1. Schließen Sie die experimentelle [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]Instanz von, wenn Sie ausgeführt wird.

2. Hinzufügen einer Datei, die mit dem Namen MBConsumer\Dsl\Custom.cs und seinen Inhalt auf Folgendes festgelegt.

    ```

    namespace Company.MB2Consume
    {
      using Microsoft.VisualStudio.Modeling.Integration;
      using Company.MB3Provider;

      public partial class ExampleShape
      {
        public override void OnDoubleClick(Microsoft.VisualStudio.Modeling.Diagrams.DiagramPointEventArgs e)
        {
          base.OnDoubleClick(e);
          ExampleElement element = this.ModelElement as ExampleElement;
          if (element.MBR != null)
          {
            IModelBus modelbus = this.Store.GetService(typeof(SModelBus)) as IModelBus;
            using (ModelBusAdapter adapter = modelbus.CreateAdapter(element.MBR))
            {
              Task task = adapter.ResolveElementReference<Task>(element.MBR);
              // Open a window on this model:
              ModelBusView view = adapter.GetDefaultView();
              view.Show();
              view.SetSelection(element.MBR);
            }
          }
        }
      }
    }

    ```

3. Drücken Sie STRG+F5.

4. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Öffnen`Debugging\Sample.consume`Sie in der experimentellen Instanz von.

5. Doppelklicken Sie auf eine Form vom Typ.

     Wenn Sie auf das Element "MBR" festgelegt haben, wird das referenzierte Modell wird geöffnet, und das referenzierte Element ausgewählt ist.

## <a name="see-also"></a>Siehe auch
 [Integrieren von Modellen mithilfe von Visual Studio ModelBus](../modeling/integrating-models-by-using-visual-studio-modelbus.md) [Code Generierung und T4-Text Vorlagen](../modeling/code-generation-and-t4-text-templates.md)
