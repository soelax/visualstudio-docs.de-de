---
title: 'Exemplarische Vorgehensweise: Erstellen eines benutzerdefinierten Anweisungsprozessors | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
- walkthroughs [text templates], directive processor
ms.assetid: b8f35a36-14e1-4467-8f5f-e01402af14d5
caps.latest.revision: 76
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 325a0c594c142ab62aba47e5c721da5ade6f179f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704055"
---
# <a name="walkthrough-creating-a-custom-directive-processor"></a>Exemplarische Vorgehensweise: Erstellen eines benutzerdefinierten Anweisungsprozessors
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Die Richtlinie Prozessoren * arbeiten, indem Sie Code Hinzufügen der *generierten Transformationsklasse*. Aufrufen einer *Richtlinie* aus einer *Textvorlage*, der Rest des Codes, den Sie in der Textvorlage schreiben, kann die Funktionalität von der Anweisung bereitgestellten abhängig.  

 Sie können eigene benutzerdefinierte Direktivenprozessoren schreiben. Dies ermöglicht Ihnen das Anpassen der Textvorlagen. Zum Erstellen eines benutzerdefinierten Anweisungsprozessors erstellen Sie eine Klasse, die von <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> oder <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> erbt.  

 In dieser exemplarischen Vorgehensweise werden u. a. die folgenden Aufgaben beschrieben:  

- Erstellen eines benutzerdefinierten Direktivenprozessors  

- Registrieren des Anweisungsprozessors  

- Testen des Direktivenprozessors  

## <a name="prerequisites"></a>Vorraussetzungen  
 Um die exemplarische Vorgehensweise nachzuvollziehen, benötigen Sie Folgendes:  

- Visual Studio 2010  

- Visual Studio 2010 SDK  

## <a name="creating-a-custom-directive-processor"></a>Erstellen eines benutzerdefinierten Anweisungsprozessors  
 In dieser exemplarischen Vorgehensweise erstellen Sie einen benutzerdefinierten Direktivenprozessor. Sie fügen eine benutzerdefinierte Anweisung hinzu, von der eine XML-Datei gelesen, in einer <xref:System.Xml.XmlDocument>-Variable gespeichert und durch eine Eigenschaft verfügbar gemacht wird. Im Abschnitt "Testen des Anweisungsprozessors" verwenden Sie diese Eigenschaft in einer Textvorlage, um auf die XML-Datei zuzugreifen.  

 Der Aufruf der benutzerdefinierten Direktive sieht folgendermaßen aus:  

 `<#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<Your Path>DocFile.xml" #>`  

 Der benutzerdefinierte Anweisungsprozessor fügt die Variable und die Eigenschaft der generierten Transformationsklasse hinzu. In der Anweisung, die Sie hier erstellen, wird der von der Engine zur generierten Transformationsklasse hinzugefügte Code mithilfe von <xref:System.CodeDom>-Klassen erstellt. Die <xref:System.CodeDom>-Klassen erstellen abhängig von der im [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]-Parameter der `language`-Anweisung angegebenen Sprache Code in Visual C# oder `template`. Die Sprache des Direktivenprozessors und die Sprache der Textvorlage, die auf den Direktivenprozessor zugreift, müssen nicht identisch sein.  

 Der von der Anweisung erstellte Code sieht folgendermaßen aus:  

```csharp  
private System.Xml.XmlDocument document0Value;  

public virtual System.Xml.XmlDocument Document0  
{  
  get  
  {  
    if ((this.document0Value == null))  
    {  
      this.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>);  
    }  
    return this.document0Value;  
  }  
}  
```  

```vb  
Private document0Value As System.Xml.XmlDocument  

Public Overridable ReadOnly Property Document0() As System.Xml.XmlDocument  
    Get  
        If (Me.document0Value Is Nothing) Then  
            Me.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>)  
        End If  
        Return Me.document0Value  
    End Get  
End Property  
```  

#### <a name="to-create-a-custom-directive-processor"></a>So erstellen Sie einen benutzerdefinierten Direktivenprozessor  

1. Erstellen Sie in Visual Studio ein Visual C#- oder Visual Basic-Klassenbibliothekprojekt mit dem Namen "CustomDP".  

    > [!NOTE]
    > Wenn Sie den Anweisungsprozessor auf mehreren Computern installieren möchten, empfiehlt es sich, ein [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]-Erweiterungsprojekt (VSIX) zu verwenden und eine PKGDEF-Datei in die Erweiterung einzuschließen. Weitere Informationen finden Sie unter [bereitstellen einen benutzerdefinierten Anweisungsprozessor](../modeling/deploying-a-custom-directive-processor.md).  

2. Fügen Sie Verweise auf die folgenden Assemblys hinzu:  

    - **Microsoft.VisualStudio.TextTemplating.\*.0**  

    - **Microsoft.VisualStudio.TextTemplating.Interfaces.\*.0**  

3. Ersetzen Sie den Code in **Class1** durch den folgenden Code. Dieser Code definiert eine CustomDirectiveProcessor-Klasse, die von der <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor>-Klasse erbt und die erforderlichen Methoden implementiert.  

    ```csharp  
    using System;  
    using System.CodeDom;  
    using System.CodeDom.Compiler;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using Microsoft.VisualStudio.TextTemplating;  

    namespace CustomDP  
    {  
        public class CustomDirectiveProcessor : DirectiveProcessor  
        {  
            //this buffer stores the code that is added to the   
            //generated transformation class after all the processing is done   
            //---------------------------------------------------------------------  
            private StringBuilder codeBuffer;  

            //Using a Code Dom Provider creates code for the   
            //generated transformation class in either Visual Basic or C#.  
            //If you want your directive processor to support only one language, you  
            //can hard code the code you add to the generated transformation class.  
            //In that case, you do not need this field.  
            //--------------------------------------------------------------------------  
            private CodeDomProvider codeDomProvider;  

            //this stores the full contents of the text template that is being processed  
            //--------------------------------------------------------------------------  
            private String templateContents;  

            //These are the errors that occur during processing. The engine passes   
            //the errors to the host, and the host can decide how to display them,  
            //for example the host can display the errors in the UI  
            //or write them to a file.  
            //---------------------------------------------------------------------  
            private CompilerErrorCollection errorsValue;  
            public new CompilerErrorCollection Errors  
            {  
                get { return errorsValue; }  
            }  

            //Each time this directive processor is called, it creates a new property.  
            //We count how many times we are called, and append "n" to each new  
            //property name. The property names are therefore unique.  
            //-----------------------------------------------------------------------------  
            private int directiveCount = 0;  

            public override void Initialize(ITextTemplatingEngineHost host)  
            {  
                //we do not need to do any initialization work  
            }  

            public override void StartProcessingRun(CodeDomProvider languageProvider, String templateContents, CompilerErrorCollection errors)  
            {  
                //the engine has passed us the language of the text template  
                //we will use that language to generate code later  
                //----------------------------------------------------------  
                this.codeDomProvider = languageProvider;  
                this.templateContents = templateContents;  
                this.errorsValue = errors;  

                this.codeBuffer = new StringBuilder();  
            }  

            //Before calling the ProcessDirective method for a directive, the   
            //engine calls this function to see whether the directive is supported.  
            //Notice that one directive processor might support many directives.  
            //---------------------------------------------------------------------  
            public override bool IsDirectiveSupported(string directiveName)  
            {  
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    return true;  
                }  
                if (string.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    return true;  
                }  
                return false;  
            }  

            public override void ProcessDirective(string directiveName, IDictionary<string, string> arguments)  
            {  
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    string fileName;  

                    if (!arguments.TryGetValue("FileName", out fileName))  
                    {  
                        throw new DirectiveProcessorException("Required argument 'FileName' not specified.");  
                    }  

                    if (string.IsNullOrEmpty(fileName))  
                    {  
                        throw new DirectiveProcessorException("Argument 'FileName' is null or empty.");  
                    }  

                    //Now we add code to the generated transformation class.  
                    //This directive supports either Visual Basic or C#, so we must use the  
                    //System.CodeDom to create the code.  
                    //If a directive supports only one language, you can hard code the code.  
                    //--------------------------------------------------------------------------  

                    CodeMemberField documentField = new CodeMemberField();  

                    documentField.Name = "document" + directiveCount + "Value";  
                    documentField.Type = new CodeTypeReference(typeof(XmlDocument));  
                    documentField.Attributes = MemberAttributes.Private;  

                    CodeMemberProperty documentProperty = new CodeMemberProperty();  

                    documentProperty.Name = "Document" + directiveCount;  
                    documentProperty.Type = new CodeTypeReference(typeof(XmlDocument));  
                    documentProperty.Attributes = MemberAttributes.Public;  
                    documentProperty.HasSet = false;  
                    documentProperty.HasGet = true;  

                    CodeExpression fieldName = new CodeFieldReferenceExpression(new CodeThisReferenceExpression(), documentField.Name);  
                    CodeExpression booleanTest = new CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, new CodePrimitiveExpression(null));  
                    CodeExpression rightSide = new CodeMethodInvokeExpression(new CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", new CodePrimitiveExpression(fileName));  
                    CodeStatement[] thenSteps = new CodeStatement[] { new CodeAssignStatement(fieldName, rightSide) };  

                    CodeConditionStatement ifThen = new CodeConditionStatement(booleanTest, thenSteps);  
                    documentProperty.GetStatements.Add(ifThen);  

                    CodeStatement s = new CodeMethodReturnStatement(fieldName);  
                    documentProperty.GetStatements.Add(s);  

                    CodeGeneratorOptions options = new CodeGeneratorOptions();  
                    options.BlankLinesBetweenMembers = true;  
                    options.IndentString = "    ";  
                    options.VerbatimOrder = true;  
                    options.BracingStyle = "C";  

                    using (StringWriter writer = new StringWriter(codeBuffer, CultureInfo.InvariantCulture))  
                    {  
                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options);  
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options);  
                    }  

                }//end CoolDirective  

                //One directive processor can contain many directives.  
                //If you want to support more directives, the code goes here...  
                //-----------------------------------------------------------------  
                if (string.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    //code for SuperCoolDirective goes here...  
                }//end SuperCoolDirective  

                //Track how many times the processor has been called.  
                //-----------------------------------------------------------------  
                directiveCount++;  

            }//end ProcessDirective  

            public override void FinishProcessingRun()  
            {  
                this.codeDomProvider = null;  

                //important: do not do this:  
                //the get methods below are called after this method   
                //and the get methods can access this field  
                //-----------------------------------------------------------------  
                //this.codeBuffer = null;  
            }  

            public override string GetPreInitializationCodeForProcessingRun()  
            {  
                //Use this method to add code to the start of the   
                //Initialize() method of the generated transformation class.  
                //We do not need any pre-initialization, so we will just return "".  
                //-----------------------------------------------------------------  
                //GetPreInitializationCodeForProcessingRun runs before the   
                //Initialize() method of the base class.  
                //-----------------------------------------------------------------  
                return String.Empty;  
            }  

            public override string GetPostInitializationCodeForProcessingRun()  
            {  
                //Use this method to add code to the end of the   
                //Initialize() method of the generated transformation class.  
                //We do not need any post-initialization, so we will just return "".  
                //------------------------------------------------------------------  
                //GetPostInitializationCodeForProcessingRun runs after the  
                //Initialize() method of the base class.  
                //-----------------------------------------------------------------  
                return String.Empty;  
            }  

            public override string GetClassCodeForProcessingRun()  
            {  
                //Return the code to add to the generated transformation class.  
                //-----------------------------------------------------------------  
                return codeBuffer.ToString();  
            }  

            public override string[] GetReferencesForProcessingRun()  
            {  
                //This returns the references that we want to use when   
                //compiling the generated transformation class.  
                //-----------------------------------------------------------------  
                //We need a reference to this assembly to be able to call   
                //XmlReaderHelper.ReadXml from the generated transformation class.  
                //-----------------------------------------------------------------  
                return new string[]  
                {  
                    "System.Xml",  
                    this.GetType().Assembly.Location  
                };  
            }  

            public override string[] GetImportsForProcessingRun()  
            {  
                //This returns the imports or using statements that we want to   
                //add to the generated transformation class.  
                //-----------------------------------------------------------------  
                //We need CustomDP to be able to call XmlReaderHelper.ReadXml  
                //from the generated transformation class.  
                //-----------------------------------------------------------------  
                return new string[]  
                {  
                    "System.Xml",  
                    "CustomDP"  
                };  
            }  
        }//end class CustomDirectiveProcessor  

        //-------------------------------------------------------------------------  
        // the code that we are adding to the generated transformation class   
        // will call this method  
        //-------------------------------------------------------------------------  
        public static class XmlReaderHelper  
        {  
            public static XmlDocument ReadXml(string fileName)  
            {  
                XmlDocument d = new XmlDocument();  

                using (XmlTextReader reader = new XmlTextReader(fileName))  
                {  
                    try  
                    {  
                        d.Load(reader);  
                    }  
                    catch (System.Xml.XmlException e)  
                    {  
                        throw new DirectiveProcessorException("Unable to read the XML file.", e);  
                    }  
                }  
                return d;  
            }  
        }//end class XmlReaderHelper  
    }//end namespace CustomDP  
    ```  

    ```vb  
    Imports System  
    Imports System.CodeDom  
    Imports System.CodeDom.Compiler  
    Imports System.Collections.Generic  
    Imports System.Globalization  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports Microsoft.VisualStudio.TextTemplating  

    Namespace CustomDP  

        Public Class CustomDirectiveProcessor  
        Inherits DirectiveProcessor  

            'this buffer stores the code that is added to the   
            'generated transformation class after all the processing is done   
            '---------------------------------------------------------------  
            Private codeBuffer As StringBuilder  

            'Using a Code Dom Provider creates code for the  
            'generated transformation class in either Visual Basic or C#.  
            'If you want your directive processor to support only one language, you  
            'can hard code the code you add to the generated transformation class.  
            'In that case, you do not need this field.  
            '--------------------------------------------------------------------------  
            Private codeDomProvider As CodeDomProvider  

            'this stores the full contents of the text template that is being processed  
            '--------------------------------------------------------------------------  
            Private templateContents As String  

            'These are the errors that occur during processing. The engine passes   
            'the errors to the host, and the host can decide how to display them,  
            'for example the host can display the errors in the UI  
            'or write them to a file.  
            '---------------------------------------------------------------------  
            Private errorsValue As CompilerErrorCollection  
            Public Shadows ReadOnly Property Errors() As CompilerErrorCollection  
                Get  
                    Return errorsValue  
                End Get  
            End Property  

            'Each time this directive processor is called, it creates a new property.  
            'We count how many times we are called, and append "n" to each new  
            'property name. The property names are therefore unique.  
            '--------------------------------------------------------------------------  
            Private directiveCount As Integer = 0  

            Public Overrides Sub Initialize(ByVal host As ITextTemplatingEngineHost)  

                'we do not need to do any initialization work  
            End Sub  

            Public Overrides Sub StartProcessingRun(ByVal languageProvider As CodeDomProvider, ByVal templateContents As String, ByVal errors As CompilerErrorCollection)  

                'the engine has passed us the language of the text template  
                'we will use that language to generate code later  
                '----------------------------------------------------------  
                Me.codeDomProvider = languageProvider  
                Me.templateContents = templateContents  
                Me.errorsValue = errors  

                Me.codeBuffer = New StringBuilder()  
            End Sub  

            'Before calling the ProcessDirective method for a directive, the   
            'engine calls this function to see whether the directive is supported.  
            'Notice that one directive processor might support many directives.  
            '---------------------------------------------------------------------  
            Public Overrides Function IsDirectiveSupported(ByVal directiveName As String) As Boolean  

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  
                    Return True  
                End If  

                If String.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  
                    Return True  
                End If  

                Return False  
            End Function  

            Public Overrides Sub ProcessDirective(ByVal directiveName As String, ByVal arguments As IDictionary(Of String, String))  

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  

                    Dim fileName As String  

                    If Not (arguments.TryGetValue("FileName", fileName)) Then  
                        Throw New DirectiveProcessorException("Required argument 'FileName' not specified.")  
                    End If  

                    If String.IsNullOrEmpty(fileName) Then  
                        Throw New DirectiveProcessorException("Argument 'FileName' is null or empty.")  
                    End If  

                    'Now we add code to the generated transformation class.  
                    'This directive supports either Visual Basic or C#, so we must use the  
                    'System.CodeDom to create the code.  
                    'If a directive supports only one language, you can hard code the code.  
                    '--------------------------------------------------------------------------  

                    Dim documentField As CodeMemberField = New CodeMemberField()  

                    documentField.Name = "document" & directiveCount & "Value"  
                    documentField.Type = New CodeTypeReference(GetType(XmlDocument))  
                    documentField.Attributes = MemberAttributes.Private  

                    Dim documentProperty As CodeMemberProperty = New CodeMemberProperty()  

                    documentProperty.Name = "Document" & directiveCount  
                    documentProperty.Type = New CodeTypeReference(GetType(XmlDocument))  
                    documentProperty.Attributes = MemberAttributes.Public  
                    documentProperty.HasSet = False  
                    documentProperty.HasGet = True  

                    Dim fieldName As CodeExpression = New CodeFieldReferenceExpression(New CodeThisReferenceExpression(), documentField.Name)  
                    Dim booleanTest As CodeExpression = New CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, New CodePrimitiveExpression(Nothing))  
                    Dim rightSide As CodeExpression = New CodeMethodInvokeExpression(New CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", New CodePrimitiveExpression(fileName))  
                    Dim thenSteps As CodeStatement() = New CodeStatement() {New CodeAssignStatement(fieldName, rightSide)}  

                    Dim ifThen As CodeConditionStatement = New CodeConditionStatement(booleanTest, thenSteps)  
                    documentProperty.GetStatements.Add(ifThen)  

                    Dim s As CodeStatement = New CodeMethodReturnStatement(fieldName)  
                    documentProperty.GetStatements.Add(s)  

                    Dim options As CodeGeneratorOptions = New CodeGeneratorOptions()  
                    options.BlankLinesBetweenMembers = True  
                    options.IndentString = "    "  
                    options.VerbatimOrder = True  
                    options.BracingStyle = "VB"  

                    Using writer As StringWriter = New StringWriter(codeBuffer, CultureInfo.InvariantCulture)  

                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options)  
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options)  
                    End Using  

                End If  'CoolDirective  

                'One directive processor can contain many directives.  
                'If you want to support more directives, the code goes here...  
                '-----------------------------------------------------------------  
                If String.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) = 0 Then  

                    'code for SuperCoolDirective goes here  
                End If 'SuperCoolDirective  

                'Track how many times the processor has been called.  
                '-----------------------------------------------------------------  
                directiveCount += 1  
            End Sub 'ProcessDirective  

            Public Overrides Sub FinishProcessingRun()  

                Me.codeDomProvider = Nothing  

                'important: do not do this:  
                'the get methods below are called after this method   
                'and the get methods can access this field  
                '-----------------------------------------------------------------  
                'Me.codeBuffer = Nothing  
            End Sub  

            Public Overrides Function GetPreInitializationCodeForProcessingRun() As String  

                'Use this method to add code to the start of the   
                'Initialize() method of the generated transformation class.  
                'We do not need any pre-initialization, so we will just return "".  
                '-----------------------------------------------------------------  
                'GetPreInitializationCodeForProcessingRun runs before the   
                'Initialize() method of the base class.  
                '-----------------------------------------------------------------  
                Return String.Empty  
            End Function  

            Public Overrides Function GetPostInitializationCodeForProcessingRun() As String  

                'Use this method to add code to the end of the   
                'Initialize() method of the generated transformation class.  
                'We do not need any post-initialization, so we will just return "".  
                '------------------------------------------------------------------  
                'GetPostInitializationCodeForProcessingRun runs after the  
                'Initialize() method of the base class.  
                '-----------------------------------------------------------------  
                Return String.Empty  
            End Function  

            Public Overrides Function GetClassCodeForProcessingRun() As String  

                'Return the code to add to the generated transformation class.  
                '-----------------------------------------------------------------  
                Return codeBuffer.ToString()  
            End Function  

            Public Overrides Function GetReferencesForProcessingRun() As String()  

                'This returns the references that we want to use when   
                'compiling the generated transformation class.  
                '-----------------------------------------------------------------  
                'We need a reference to this assembly to be able to call   
                'XmlReaderHelper.ReadXml from the generated transformation class.  
                '-----------------------------------------------------------------  
                Return New String() {"System.Xml", Me.GetType().Assembly.Location}  
            End Function  

            Public Overrides Function GetImportsForProcessingRun() As String()  

                'This returns the imports or using statements that we want to   
                'add to the generated transformation class.  
                '-----------------------------------------------------------------  
                'We need CustomDP to be able to call XmlReaderHelper.ReadXml  
                'from the generated transformation class.  
                '-----------------------------------------------------------------  
                Return New String() {"System.Xml", "CustomDP"}  
            End Function  
        End Class 'CustomDirectiveProcessor  

        '--------------------------------------------------------------------------  
        ' the code that we are adding to the generated transformation class   
        ' will call this method  
        '--------------------------------------------------------------------------  
        Public Class XmlReaderHelper  

            Public Shared Function ReadXml(ByVal fileName As String) As XmlDocument  

                Dim d As XmlDocument = New XmlDocument()  

                Using reader As XmlTextReader = New XmlTextReader(fileName)  

                    Try  
                        d.Load(reader)  

                    Catch e As System.Xml.XmlException  

                        Throw New DirectiveProcessorException("Unable to read the XML file.", e)  
                    End Try  
                End Using  

                Return d  
            End Function  
        End Class 'XmlReaderHelper  

    End Namespace  
    ```  

4. Für [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] öffnen die **Projekt** und auf **CustomDP-Eigenschaften**. Auf der **Anwendung** Registerkarte **Stammnamespace**, löschen Sie den Standardwert `CustomDP`.  

5. Klicken Sie im Menü **Datei** auf **Alle speichern**.  

6. Klicken Sie im Menü **Erstellen** auf **Projektmappe erstellen**.  

### <a name="build-the-project"></a>Erstellen des Projekts  
 Erstellen Sie das Projekt. Klicken Sie im Menü **Erstellen** auf **Projektmappe erstellen**.  

## <a name="registering-the-directive-processor"></a>Registrieren des Anweisungsprozessors  
 Bevor Sie eine Richtlinie aus einer Textvorlage in aufrufen können [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], müssen Sie einen Registrierungsschlüssel für den anweisungsprozessor hinzufügen.  

> [!NOTE]
> Wenn Sie den Anweisungsprozessor auf mehreren Computern installieren möchten, empfiehlt es sich, eine [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]-Erweiterung (VSIX) zu definieren, die eine PKGDEF-Datei und die Assembly enthält. Weitere Informationen finden Sie unter [bereitstellen einen benutzerdefinierten Anweisungsprozessor](../modeling/deploying-a-custom-directive-processor.md).  

 Schlüssel für Direktivenprozessoren befinden sich unter folgendem Pfad in der Registrierung:  

```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors  
```  

 Für 64-Bit-Systeme wird der folgende Registrierungsort verwendet:  

```  
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors  
```  

 In diesem Abschnitt fügen Sie der Registrierung unter demselben Pfad einen Schlüssel für den benutzerdefinierten Anweisungsprozessor hinzu.  

> [!CAUTION]
> Durch eine fehlerhafte Bearbeitung der Registrierung kann das System ernsthaft beschädigt werden. Sichern Sie alle wichtigen Daten auf dem Computer, bevor Sie Änderungen an der Registrierung vornehmen.  

#### <a name="to-add-a-registry-key-for-the-directive-processor"></a>So fügen Sie einen Registrierungsschlüssel für den Anweisungsprozessor hinzu  

1. Führen Sie die `regedit` -Befehl über das Startmenü oder der Befehlszeile aus.  

2. Navigieren Sie zum Speicherort **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\\*.0\TextTemplating\DirectiveProcessors**, und klicken Sie auf den Knoten.  

    Auf 64-Bit-Systemen verwenden **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\\\*.0\TextTemplating\DirectiveProcessors**  

3. Fügen Sie einen neuen Schlüssel mit dem Namen "CustomDirectiveProcessor" hinzu.  

   > [!NOTE]
   > Diesen Namen verwenden Sie im Feld "Prozessor" der benutzerdefinierten Anweisungen. Dieser Name muss nicht mit dem Namen der Direktive, dem Namen der Direktivenprozessorklasse oder des Direktivenprozessornamespaces übereinstimmen.  

4. Fügen Sie einen neuen Zeichenfolgenwert mit dem Namen "Class" und dem Wert CustomDP.CustomDirectiveProcessor für den Namen der neuen Zeichenfolge hinzu.  

5. Fügen Sie einen neuen Zeichenfolgenwert mit dem Namen "CodeBase" hinzu, dessen Wert dem Pfad der zuvor in dieser exemplarischen Vorgehensweise erstellten CustomDP.dll entspricht.  

    Der Pfad sieht beispielsweise wie `C:\UserFiles\CustomDP\bin\Debug\CustomDP.dll`.  

    Folgende Werte müssen für den Registrierungsschlüssel festgelegt werden:  

   |   name    |  Typ  |                                   Daten                                   |
   |-----------|--------|--------------------------------------------------------------------------|
   | (Standard) | REG_SZ |                             (Wert nicht festgelegt)                              |
   |   Klasse   | REG_SZ |                    CustomDP.CustomDirectiveProcessor                     |
   | CodeBase  | REG_SZ | <strong>\<Pfad zur Projektmappe ></strong>CustomDP\bin\Debug\CustomDP.dll |

    Wenn Sie die Assembly im GAC gespeichert haben, sollten die Werte wie folgt aussehen:  

   |   name    |  Typ  |               Daten                |
   |-----------|--------|-----------------------------------|
   | (Standard) | REG_SZ |          (Wert nicht festgelegt)          |
   |   Klasse   | REG_SZ | CustomDP.CustomDirectiveProcessor |
   | Assembly  | REG_SZ |           CustomDP.dll            |

6. Starten Sie Visual Studio neu.  

## <a name="testing-the-directive-processor"></a>Testen des Anweisungsprozessors  
 Zum Testen des Direktivenprozessors müssen Sie eine Textvorlage erstellen, in der der Prozessor aufgerufen wird.  

 In diesem Beispiel ruft die Textvorlage die Anweisung auf und übergibt im Namen eine XML-Datei, die Dokumentation für eine Klassendatei enthält. Weitere Informationen finden Sie unter [XML-Dokumentationskommentare](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199).  

 Anschließend wird in der Textvorlage die von der Direktive erstellte <xref:System.Xml.XmlDocument>-Eigenschaft verwendet, um in der XML-Datei zu navigieren und die Dokumentationskommentare auszugeben.  

#### <a name="to-create-an-xml-file-for-use-in-testing-the-directive-processor"></a>So erstellen Sie eine XML-Datei zum Testen des Anweisungsprozessors  

1. Erstellen Sie eine Textdatei namens `DocFile.xml` mit einem Text-Editor (z. B. Editor).  

    > [!NOTE]
    > Diese Datei kann an einem beliebigen Speicherort erstellt werden (z. B. C:\Test\DocFile.xml).  

2. Fügen Sie folgenden Text in der Textdatei ein:  

    ```  
    <?xml version="1.0"?>  
    <doc>  
        <assembly>  
            <name>xmlsample</name>  
        </assembly>  
        <members>  
            <member name="T:SomeClass">  
                <summary>Class level summary documentation goes here.</summary>  
                <remarks>Longer comments can be associated with a type or member through the remarks tag</remarks>  
            </member>  
            <member name="F:SomeClass.m_Name">  
                <summary>Store for the name property</summary>  
            </member>   
            <member name="M:SomeClass.#ctor">  
                <summary>The class constructor.</summary>   
            </member>  
            <member name="M:SomeClass.SomeMethod(System.String)">  
                <summary>Description for SomeMethod.</summary>  
                <param name="s">Parameter description for s goes here</param>  
                <seealso cref="T:System.String">You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.</seealso>  
            </member>  
            <member name="M:SomeClass.SomeOtherMethod">  
                <summary>Some other method.</summary>  
                <returns>Return results are described through the returns tag.</returns>  
                <seealso cref="M:SomeClass.SomeMethod(System.String)">Notice the use of the cref attribute to reference a specific method</seealso>  
            </member>  
            <member name="M:SomeClass.Main(System.String[])">  
                <summary>The entry point for the application.</summary>  
                <param name="args">A list of command line arguments</param>  
            </member>  
            <member name="P:SomeClass.Name">  
                <summary>Name property</summary>  
                <value>A value tag is used to describe the property value</value>  
            </member>  
        </members>  
    </doc>  
    ```  

3. Speichern und schließen Sie die Datei.  

#### <a name="to-create-a-text-template-to-test-the-directive-processor"></a>So erstellen Sie eine Textvorlage zum Testen des Anweisungsprozessors  

1. Erstellen Sie in Visual Studio ein Visual C#- oder Visual Basic-Klassenbibliothekprojekt mit dem Namen "TemplateTest".  

2. Fügen Sie eine neue Textvorlagendatei mit dem Namen "TestDP.tt" hinzu.  

3. Stellen Sie sicher, dass die **benutzerdefiniertes Tool** von "TestDP.tt"-Eigenschaftensatz auf `TextTemplatingFileGenerator`.  

4. Ändern Sie den Inhalt von "TestDP.tt" in den folgenden Text.  

    > [!NOTE]
    > Achten Sie darauf, ersetzen Sie die Zeichenfolge <`YOUR PATH>` durch den Pfad zu der Datei "DocFile.xml".  

     Die Sprache der Textvorlage muss nicht mit der Sprache des Anweisungsprozessors identisch sein.  

    ```csharp  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" #>  
    <#@ output extension=".txt" #>  

    <#  //This will call the custom directive processor. #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  //Uncomment this line if you want to see the generated transformation class. #>  
    <#  //System.Diagnostics.Debugger.Break(); #>  

    <#  //This will use the results of the directive processor. #>  
    <#  //The directive processor has read the XML and stored it in Document0. #>  
    <#  
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");  

        foreach (XmlNode member in node.ChildNodes)  
        {  
            XmlNode name = member.Attributes.GetNamedItem("name");  
            WriteLine("{0,7}:  {1}", "Name", name.Value);  

            foreach (XmlNode comment in member.ChildNodes)  
            {  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);  
            }  
            WriteLine("");  
        }  
    #>  

    <#  //You can call the directive processor again and pass it a different file. #>  
    <# //@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\<Your Second File>" #>  

    <#  //To use the results of the second directive call, use Document1. #>  
    <#  
        //XmlNode node2 = Document1.DocumentElement.SelectSingleNode("members");  

        //...  
    #>  
    ```  

    ```vb  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" language="vb" #>  
    <#@ output extension=".txt" #>  

    <#  'This will call the custom directive processor. #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  'Uncomment this line if you want to see the generated transformation class. #>  
    <#  'System.Diagnostics.Debugger.Break() #>  

    <#  'This will use the results of the directive processor. #>  
    <#  'The directive processor has read the XML and stored it in Document0. #>  
    <#  
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")  

        Dim member As XmlNode  
        For Each member In node.ChildNodes  

            Dim name As XmlNode = member.Attributes.GetNamedItem("name")  
            WriteLine("{0,7}:  {1}", "Name", name.Value)  

            Dim comment As XmlNode  
            For Each comment In member.ChildNodes  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)  
            Next  

            WriteLine("")  
        Next  
    #>  

    <#  'You can call the directive processor again and pass it a different file. #>  
    <# '@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFileTwo.xml" #>  

    <#  'To use the results of the second directive call, use Document1. #>  
    <#  
        'node = Document1.DocumentElement.SelectSingleNode("members")  

        '...  
    #>  
    ```  

    > [!NOTE]
    > In diesem Beispiel ist der Wert des `Processor`-Parameters `CustomDirectiveProcessor`. Der Wert des `Processor`-Parameters muss dem Namen des Registrierungsschlüssels des Prozessors entsprechen.  

5. Klicken Sie im Menü **Datei** auf **Alle speichern**.  

#### <a name="to-test-the-directive-processor"></a>So testen Sie den Direktivenprozessor  

1. In **Projektmappen-Explorer**mit der rechten Maustaste auf "TestDP.tt", und klicken Sie dann auf **benutzerdefiniertes Tool ausführen**.  

     Für [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] Benutzer "TestDP.txt" möglicherweise nicht im angezeigt **Projektmappen-Explorer** standardmäßig. Um alle Dateien, die dem Projekt zugewiesen anzuzeigen, öffnen Sie die **Projekt** Menü **alle Dateien anzeigen**.  

2. In **Projektmappen-Explorer**, erweitern Sie den Knoten "TestDP.txt", und doppelklicken Sie dann auf "TestDP.txt", um sie im Editor zu öffnen.  

     Die generierte Textausgabe wird angezeigt. Die Ausgabe sollte wie folgt aussehen:  

    ```  
       Name:  T:SomeClass  
    summary:  Class level summary documentation goes here.  
    remarks:  Longer comments can be associated with a type or member through the remarks tag  

       Name:  F:SomeClass.m_Name  
    summary:  Store for the name property  

       Name:  M:SomeClass.#ctor  
    summary:  The class constructor.  

       Name:  M:SomeClass.SomeMethod(System.String)  
    summary:  Description for SomeMethod.  
      param:  Parameter description for s goes here  
    seealso:  You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.  

       Name:  M:SomeClass.SomeOtherMethod  
    summary:  Some other method.  
    returns:  Return results are described through the returns tag.  
    seealso:  Notice the use of the cref attribute to reference a specific method  

       Name:  M:SomeClass.Main(System.String[])  
    summary:  The entry point for the application.  
      param:  A list of command line arguments  

       Name:  P:SomeClass.Name  
    summary:  Name property  
      value:  A value tag is used to describe the property value  
    ```  

## <a name="adding-html-to-generated-text"></a>Hinzufügen von HTML zum generierten Text  
 Nachdem Sie den benutzerdefinierten Anweisungsprozessor getestet haben, können Sie dem generierten Text HTML hinzufügen.  

#### <a name="to-add-html-to-the-generated-text"></a>So fügen Sie dem generierten Text HTML hinzu  

1. Ersetzen Sie den Code in "TestDP.tt" durch den folgenden Code. Der HTML-Code ist hervorgehoben. Stellen Sie sicher, dass die Zeichenfolge ersetzen `YOUR PATH` durch den Pfad zu der Datei "DocFile.xml".  

    > [!NOTE]
    > Zusätzliche \<#-Starttags und #>-Endtags trennen den Anweisungscode von den HTML-Tags.  

    ```csharp  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" #>  
    <#@ output extension=".htm" #>  

    <#  //this will call the custom directive processor #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  //uncomment this line if you want to see the generated transformation class #>  
    <#  //System.Diagnostics.Debugger.Break(); #>  

    <html><body>  

    <#  //this will use the results of the directive processor #>  
    <#  //the directive processor has read the XML and stored it in Document0#>  
    <#  
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");  

        foreach (XmlNode member in node.ChildNodes)  
        {  
    #>  
    <h3>  
    <#      
            XmlNode name = member.Attributes.GetNamedItem("name");  
            WriteLine("{0,7}:  {1}", "Name", name.Value);  
    #>  
    </h3>  
    <#  
            foreach (XmlNode comment in member.ChildNodes)  
            {  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);  
    #>  
    <br/>  
    <#  
            }  
        }  
    #>  
    </body></html>  
    ```  

    ```vb  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" language="vb" #>  
    <#@ output extension=".htm" #>  

    <#  'this will call the custom directive processor #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  'uncomment this line if you want to see the generated transformation class #>  
    <#  'System.Diagnostics.Debugger.Break() #>  

    <html><body>  

    <#  'this will use the results of the directive processor #>  
    <#  'the directive processor has read the XML and stored it in Document0#>  
    <#  
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")  

        Dim member As XmlNode  
        For Each member In node.ChildNodes  
    #>  
    <h3>  
    <#      
            Dim name As XmlNode = member.Attributes.GetNamedItem("name")  
            WriteLine("{0,7}:  {1}", "Name", name.Value)  
    #>  
    </h3>  
    <#  
            Dim comment As XmlNode  
            For Each comment In member.ChildNodes  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)  
    #>  
    <br/>  
    <#  
            Next  
        Next  
    #>  
    </body></html>  
    ```  

2. Auf der **Datei** Menü klicken Sie auf **TestDP.txt speichern**.  

3. Zum Anzeigen der Ausgabe in einem Browser im **Projektmappen-Explorer**mit der rechten Maustaste auf "TestDP.htm", und klicken Sie auf **In Browser anzeigen**.  

     Die Ausgabe sollte dem ursprünglichen Text entsprechen, jedoch HTML-formatiert sein. Jeder Elementname sollte fett formatiert sein.
