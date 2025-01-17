---
title: Hinzufügen von Steuerelementen zum Dokument zur Laufzeit in VSTO-Add-in
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- application-level add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to documents at run time
- documents [Office development in Visual Studio], adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b6ac01f32a14589837d0cb7707cb3d2f8946bd0a
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328400"
---
# <a name="walkthrough-add-controls-to-a-document-at-runtime-in-a-vsto-add-in"></a>Exemplarische Vorgehensweise: Hinzufügen von Steuerelementen zu einem Dokument zur Laufzeit in einem VSTO-Add-in
  Sie können Steuerelemente jedem geöffneten Microsoft Office Word-Dokument mithilfe eines VSTO-Add-Ins hinzufügen. In dieser exemplarischen Vorgehensweise wird veranschaulicht, wie Sie das Menüband verwenden, um Benutzer hinzufügen können eine <xref:Microsoft.Office.Tools.Word.Controls.Button> oder <xref:Microsoft.Office.Tools.Word.RichTextContentControl> zu einem Dokument.

 **Gilt für:** Die Informationen in diesem Thema betreffen VSTO-Add-in-Projekte für Word 2010. Weitere Informationen finden Sie unter [Verfügbare Funktionen nach Office-Anwendung und Projekttyp](../vsto/features-available-by-office-application-and-project-type.md).

 In dieser exemplarischen Vorgehensweise werden die folgenden Aufgaben veranschaulicht:

- Erstellen eines neuen Word-VSTO-Add-In-Projekts

- Bereitstellen einer Benutzeroberfläche (UI) zum Hinzufügen von Steuerelementen zum Dokument

- Hinzufügen von Steuerelementen zum Dokument zur Laufzeit.

- Entfernen von Steuerelementen aus dem Dokument

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Vorraussetzungen
 Zum Durchführen dieser exemplarischen Vorgehensweise benötigen Sie die folgenden Komponenten:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] oder [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## <a name="create-a-new-word-add-in-project"></a>Erstellen eines neuen Word-Add-in-Projekts
 Beginnen Sie, indem Sie ein Word-VSTO-Add-In-Projekt erstellen.

### <a name="to-create-a-new-word-vsto-add-in-project"></a>So erstellen Sie ein neues Word-VSTO-Add-In-Projekt

1. Erstellen Sie ein VSTO-Add-in-Projekt für Word, mit dem Namen **WordDynamicControls**. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen von Office-Projekten in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. Fügen Sie einen Verweis auf die Assembly **Microsoft.Office.Tools.Word.v4.0.Utilities.dll** hinzu. Dieser Verweis ist erforderlich, um später in dieser exemplarischen Vorgehensweise dem Dokument programmgesteuert ein Windows Forms-Steuerelement hinzuzufügen.

## <a name="provide-a-ui-to-add-controls-to-a-document"></a>Geben Sie eine Benutzeroberfläche zum Hinzufügen von Steuerelementen zu einem Dokument
 Fügen Sie dem Menüband in Word eine benutzerdefinierte Registerkarte hinzu. Benutzer können Kontrollkästchen auf der Registerkarte aktivieren, um einem Dokument Steuerelemente hinzuzufügen.

### <a name="to-provide-a-ui-to-add-controls-to-a-document"></a>So stellen Sie eine Benutzeroberfläche zum Hinzufügen von Steuerelementen zu einem Dokument bereit

1. Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**.

2. Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **Menüband (Visueller Designer)** aus.

3. Ändern Sie den Namen des neuen Menübands in **MyRibbon**, und klicken Sie dann auf **Hinzufügen**.

    Die Datei **MyRibbon.cs** oder **MyRibbon.vb** wird im Menüband-Designer geöffnet. Sie beinhaltet eine standardmäßige Registerkarte und eine Gruppe.

4. Klicken Sie im Menüband-Designer auf die Gruppe **group1** .

5. Ändern Sie im Fenster **Eigenschaften** die **Bezeichnung** -Eigenschaft für **group1** in **Steuerelemente hinzufügen**.

6. Ziehen Sie ein **Kontrollkästchen** -Steuerelement von der Registerkarte **Steuerelemente für Office-Menübänder**der **Toolbox** auf **group1**.

7. Klicken Sie auf **CheckBox1** , um dieses Steuerelement auszuwählen.

8. Ändern Sie im Fenster **Eigenschaften** die folgenden Eigenschaften:

   | Eigenschaft | Wert |
   |-----------|-----------------------|
   | **Name** | **addButtonCheckBox** |
   | **Bezeichnung** | **Schaltfläche hinzufügen** |

9. Fügen Sie **group1**ein zweites Kontrollkästchen hinzu, und ändern Sie dann die folgenden Eigenschaften.

   | Eigenschaft | Wert |
   |-----------|---------------------------|
   | **Name** | **addRichTextCheckBox** |
   | **Bezeichnung** | **Rich-Text-Steuerelement hinzufügen** |

10. Doppelklicken Sie im Menüband-Designer auf **Schaltfläche hinzufügen**.

     Der <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> -Ereignishandler des Kontrollkästchens **Schaltfläche hinzufügen** wird im Code-Editor geöffnet.

11. Kehren Sie zum Menüband-Designer zurück, und doppelklicken Sie auf **Rich-Text-Steuerelement hinzufügen**.

     Der <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> -Ereignishandler des Kontrollkästchens **Rich-Text-Steuerelement hinzufügen** wird im Code-Editor geöffnet.

    Später in dieser exemplarischen Vorgehensweise werden Sie diesen Ereignishandlern Code hinzufügen, mit dem im aktiven Dokument Steuerelemente hinzugefügt und entfernt werden können.

## <a name="add-and-remove-controls-on-the-active-document"></a>Hinzufügen und Entfernen von Steuerelementen auf dem aktiven Dokument
 Sie müssen das aktive Dokument im VSTO-Add-In-Code in ein <xref:Microsoft.Office.Tools.Word.Document>*Hostelement* konvertieren, bevor Sie ein Steuerelement hinzufügen können. In Office-Projektmappen können verwaltete Steuerelemente nur zu Hostelementen hinzugefügt werden, die als Container für die Steuerelemente fungieren. In VSTO-Add-in-Projekten können Hostelemente können erstellt werden zur Laufzeit mithilfe der `GetVstoObject` Methode.

 Fügen Sie der `ThisAddIn` -Klasse Methoden hinzu, die aufgerufen werden können, um ein <xref:Microsoft.Office.Tools.Word.Controls.Button> - oder ein <xref:Microsoft.Office.Tools.Word.RichTextContentControl> -Steuerelement auf dem aktiven Dokument hinzuzufügen oder zu entfernen. Später in dieser exemplarischen Vorgehensweise werden Sie diese Methoden aus den <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> -Ereignishandlern der Kontrollkästchen im Menüband aufrufen.

### <a name="to-add-and-remove-controls-on-the-active-document"></a>So fügen Sie Steuerelemente auf dem aktiven Dokument hinzu oder entfernen diese

1. In **Projektmappen-Explorer**, doppelklicken Sie auf *"ThisAddIn.cs"* oder *"ThisAddIn.vb"* zum Öffnen der Datei im Code-Editor.

2. Fügen Sie der `ThisAddIn` -Klasse folgenden Code hinzu. Mit diesem Code werden ein <xref:Microsoft.Office.Tools.Word.Controls.Button> - und ein <xref:Microsoft.Office.Tools.Word.RichTextContentControl> -Objekt deklariert, die den Steuerelementen entsprechen, die dem Dokument hinzugefügt werden.

     [!code-vb[Trin_WordAddInDynamicControlsWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#1](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs#1)]

3. Fügen Sie der `ThisAddIn` -Klasse die folgende Methode hinzu. Wenn der Benutzer auf das Kontrollkästchen **Schaltfläche hinzufügen** im Menüband klickt, fügt diese Methode ein <xref:Microsoft.Office.Tools.Word.Controls.Button> -Objekt zur aktuellen Auswahl im Dokument hinzu, wenn das Kontrollkästchen aktiviert ist, oder löscht sie das <xref:Microsoft.Office.Tools.Word.Controls.Button> -Objekt, wenn das Kontrollkästchen deaktiviert ist.

     [!code-vb[Trin_WordAddInDynamicControlsWalkthrough#2](../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#2](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs#2)]

4. Fügen Sie der `ThisAddIn` -Klasse die folgende Methode hinzu. Wenn der Benutzer auf das Kontrollkästchen **Rich-Text-Steuerelement hinzufügen** im Menüband klickt, fügt diese Methode ein <xref:Microsoft.Office.Tools.Word.RichTextContentControl> -Objekt zur aktuellen Auswahl im Dokument hinzu, wenn das Kontrollkästchen aktiviert ist, oder löscht sie das <xref:Microsoft.Office.Tools.Word.RichTextContentControl> -Objekt, wenn das Kontrollkästchen deaktiviert ist.

     [!code-vb[Trin_WordAddInDynamicControlsWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#3](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs#3)]

## <a name="remove-the-button-control-when-the-document-is-saved"></a>Entfernen Sie das Schaltflächen-Steuerelement aus, wenn das Dokument gespeichert wird
 Windows Forms-Steuerelemente bleiben nicht erhalten, wenn das Dokument gespeichert und dann geschlossen wird. Im Dokument verbleibt aber ein ActiveX-Wrapper für jedes Steuerelement, und der Rand eines solchen Wrappers ist für Endbenutzer nach einem erneuten Öffnen des Dokuments sichtbar. Es gibt mehrere Möglichkeiten, dynamisch erstellte Windows Forms-Steuerelemente in VSTO-Add-Ins zu bereinigen. In dieser exemplarischen Vorgehensweise wird das <xref:Microsoft.Office.Tools.Word.Controls.Button> -Steuerelement programmgesteuert entfernt, wenn das Dokument gespeichert wird.

### <a name="to-remove-the-button-control-when-the-document-is-saved"></a>So entfernen Sie das Button-Steuerelement, wenn das Dokument gespeichert wird

1. In der *"ThisAddIn.cs"* oder *"ThisAddIn.vb"* Codedatei, fügen Sie die folgende Methode der `ThisAddIn` Klasse. Diese Methode ist ein Ereignishandler für das <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> -Ereignis. Wenn dem gespeicherten Dokument ein <xref:Microsoft.Office.Tools.Word.Document> -Hostelement zugeordnet ist, ruft der Ereignishandler das Hostelement ab und entfernt das <xref:Microsoft.Office.Tools.Word.Controls.Button> -Steuerelement, wenn es vorhanden ist.

     [!code-vb[Trin_WordAddInDynamicControlsWalkthrough#4](../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb#4)]
     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#4](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs#4)]

2. In C# fügen Sie dem `ThisAddIn_Startup` -Ereignishandler den folgenden Code hinzu. Dieser Code ist in C# erforderlich, um den `Application_DocumentBeforeSave` -Ereignishandler mit dem <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> -Ereignis zu verbinden.

     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#5](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs#5)]

## <a name="add-and-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>Fügen Sie hinzu und entfernen Sie Steuerelemente aus, wenn der Benutzer die Kontrollkästchen im Menüband klickt
 Ändern Sie abschließend die <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> -Ereignishandler der Kontrollkästchen, die Sie zum Menüband hinzufügen oder entfernen die Steuerelemente im Dokument hinzugefügt.

### <a name="to-add-or-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>Zum Hinzufügen oder entfernen steuert, wenn der Benutzer die Kontrollkästchen im Menüband klickt

1. In der *MyRibbon.cs* oder *MyRibbon.vb* Codedatei, ersetzen Sie den generierten `addButtonCheckBox_Click` und `addRichTextCheckBox_Click` -Ereignishandler durch den folgenden Code. Dieser Code definiert diese Ereignishandler neu, sodass aus ihnen die `ToggleButtonOnDocument` - und die `ToggleRichTextControlOnDocument` -Methode aufgerufen werden, die Sie der `ThisAddIn` -Klasse früher in dieser exemplarischen Vorgehensweise hinzugefügt haben.

     [!code-vb[Trin_WordAddInDynamicControlsWalkthrough#6](../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.vb#6)]
     [!code-csharp[Trin_WordAddInDynamicControlsWalkthrough#6](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.cs#6)]

## <a name="test-the-solution"></a>Testen der Lösung
 Fügen Sie einem Dokument Steuerelemente hinzu, indem Sie sie auf der benutzerdefinierten Registerkarte im Menüband auswählen. Wenn Sie das Dokument speichern, wird das <xref:Microsoft.Office.Tools.Word.Controls.Button> -Steuerelement entfernt.

### <a name="to-test-the-solution"></a>So testen Sie die Projektmappe

1. Drücken Sie **F5** um Ihr Projekt auszuführen.

2. Drücken Sie in das aktive Dokument **EINGABETASTE** mehrmals Hinzufügen neuer leere Absätze des Dokuments.

3. Wählen Sie den ersten Absatz aus.

4. Klicken Sie auf die Registerkarte **Add-Ins** .

5. Klicken Sie in der Gruppe **Steuerelemente hinzufügen** auf **Schaltfläche hinzufügen**.

     Im ersten Absatz wird eine Schaltfläche angezeigt.

6. Wählen Sie den letzten Absatz aus.

7. Klicken Sie in der Gruppe **Steuerelemente hinzufügen** auf **Rich-Text-Steuerelement hinzufügen**.

     Dem letzten Absatz wird ein Rich-Text-Inhaltssteuerelement hinzugefügt.

8. Speichern Sie das Dokument.

     Die Schaltfläche wird aus dem Dokument entfernt.

## <a name="next-steps"></a>Nächste Schritte
 In den folgenden Themen erhalten Sie weitere Informationen zu Steuerelementen in VSTO-Add-Ins:

- Ein Beispiel, das veranschaulicht, wie viele andere Typen von Steuerelementen zu einem Dokument zur Laufzeit hinzufügen und die Steuerelemente neu erstellt, wenn das Dokument erneut geöffnet wird, finden Sie im Word-Add-In dynamischen Steuerelemente Beispiel am [Office-Entwicklung-Beispiele und exemplarische Vorgehensweisen](../vsto/office-development-samples-and-walkthroughs.md).

- Eine exemplarische Vorgehensweise, das Hinzufügen von Steuerelementen zu einem Arbeitsblatt mithilfe eines VSTO-Add-Ins für Excel veranschaulicht, finden Sie unter [Exemplarische Vorgehensweise: Hinzufügen von Steuerelementen zu einem Arbeitsblatt zur Laufzeit in VSTO-add-in-Projekt](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md).

## <a name="see-also"></a>Siehe auch
- [Word-Projektmappen](../vsto/word-solutions.md)
- [Hinzufügen von Steuerelementen zu Office-Dokumenten zur Laufzeit](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Beibehalten von dynamischen Steuerelementen in Office-Dokumente](../vsto/persisting-dynamic-controls-in-office-documents.md)
- [Vorgehensweise: Hinzufügen von Windows Forms-Steuerelementen zu Office-Dokumenten](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Vorgehensweise: Hinzufügen von Inhaltssteuerelementen zu Word-Dokumenten](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Erweitern von Word-Dokumenten und Excel-Arbeitsmappen in VSTO-Add-ins zur Laufzeit](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
