---
title: 'Schritt 3: Zuweisen eines zufälligen Symbols zu jeder Bezeichnung'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- csharp
- vb
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae4b635f86eb67f04db3ba6243e7b0ba4634bfb4
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416667"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>Schritt 3: Zuweisen eines zufälligen Symbols zu jeder Bezeichnung
Es wäre zu einfach, wenn die Symbole in jedem Spiel in den gleichen Zellen erscheinen. Um dies zu vermeiden, weisen Sie die Symbole mithilfe einer `AssignIconsToSquares()`-Methode zufällig den Bezeichnungsfeldern des Formulars zu.

## <a name="to-assign-a-random-icon-to-each-label"></a>So weisen Sie jeder Bezeichnung ein zufälliges Symbol zu

1. Machen Sie sich vor dem Hinzufügen des folgenden Codes bewusst, wie die Methode funktioniert. Es ist ein neues Schlüsselwort verfügbar: `foreach` in Visual C# und `For Each` in Visual Basic. (Eine der Zeilen ist absichtlich auskommentiert. Dies wird am Ende dieser Prozedur erklärt.)

     [!code-csharp[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_1.vb)]

2. Fügen Sie die `AssignIconsToSquares()`-Methode wie im vorherigen Schritt gezeigt hinzu. Fügen Sie die Methode direkt ein unter dem Code aus [Schritt 2: Hinzufügen eines zufällig ausgewählten Objekts und einer Liste von Symbolen](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).

     Wie bereits erwähnt, enthält die `AssignIconsToSquares()`-Methode ein neues Element: Eine `foreach`-Schleife in Visual C# und eine `For Each`-Schleife in Visual Basic. Sie können eine `For Each`-Schleife verwenden, wenn Sie die gleiche Aktion immer wieder ausführen möchten. In diesem Fall sollen wie im folgenden Code erläutert die gleichen Anweisungen für jede Bezeichnung aus <xref:System.Windows.Forms.TableLayoutPanel> ausgeführt werden. Die erste Zeile erstellt eine Variable mit dem Namen `control`, die nacheinander jedes Steuerelement speichert. Jedes dieser Steuerelement umfasst die Anweisungen, die in der Schleife ausgeführt werden.

     [!code-csharp[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_2.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_2.vb)]

    > [!NOTE]
    > Die Namen "iconLabel" (Symbolbezeichnung) und "control" (Steuerelement) dienen zur Verdeutlichung der Verwendungsweise. Sie können diese Namen durch beliebige andere Namen ersetzen, ohne die Funktionsweise des Codes zu beeinflussen, sofern Sie die Namen in jeder Anweisung innerhalb der Schleife ändern.

     Die `AssignIconsToSquares()`-Methode durchläuft jedes Bezeichnungsfeld-Steuerelement in TableLayoutPanel und führt für jedes die gleichen Anweisungen aus. Diese Anweisungen rufen ein zufälliges Symbol ab aus der Liste aus [Schritt 2: Hinzufügen eines zufällig ausgewählten Objekts und einer Liste von Symbolen](../ide/step-2-add-a-random-object-and-a-list-of-icons.md). (Aus diesem Grund wurden zwei Exemplare jedes Symbols in die Liste eingefügt, damit zufälligen Bezeichnungsfeldern ein Symbolpaar zugewiesen werden kann.)

     Betrachten Sie den Code genauer, der innerhalb der `foreach`-Schleife oder der `For Each`-Schleife ausgeführt wird. Dabei handelt es sich um den folgenden Code.

     [!code-csharp[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_3.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_3.vb)]

     In der ersten Zeile wird die Variable **control** in eine Bezeichnung mit dem Namen **iconLabel** konvertiert. Die folgende Zeile ist eine `if`-Anweisung, die prüft, ob die Konvertierung erfolgt ist. Wenn die Konvertierung funktioniert, werden die Anweisungen innerhalb der `if`-Anweisung ausgeführt. (Wie Sie vielleicht aus vorherigen Lernprogrammen wissen, kann mit der `if`-Anweisung eine beliebige Bedingung geprüft werden.) Mit der ersten Zeile der `if`-Anweisung wird die Variable **randomNumber** erstellt, die eine Zufallszahl enthält, die einem der Elemente in der Symbolliste entspricht. Dazu verwendet die Anweisung die <xref:System.Random.Next>-Methode des <xref:System.Random>-Objekts, das Sie früher erstellt haben. Die `Next`-Methode gibt eine Zufallszahl zurück. Diese Zeile verwendet auch die <xref:System.Collections.Generic.List%601.Count>-Eigenschaft der **icons**-Liste, um den Bereich festzulegen, aus dem die Zufallszahl ausgewählt werden soll. Die nächste Zeile weist der <xref:System.Windows.Forms.Label.Text>-Eigenschaft des Bezeichnungsfelds eines der Symbollistenelemente zu. Die auskommentierte Zeile wird später in diesem Thema erläutert. Schließlich entfernt die letzte Zeile in der `if`-Anweisung das Symbol aus der Liste, das dem Formular hinzugefügt wurde.

     Vergessen Sie nicht: Wenn Sie sich über die Funktionsweise eines Codeabschnitts nicht sicher sind, können Sie den Mauszeiger über einem Codeelement positionieren und erhalten eine entsprechende QuickInfo. Mithilfe des Visual Studio-Debuggers können Sie auch während der Programmausführung jede Codezeile untersuchen. Weitere Informationen erhalten Sie unter [How do I: Step with The debugger in Visual Studio? (Wie setze ich den Debugger in Visual Studio ein?)](https://msdn.microsoft.com/vstudio/ee672313.aspx) oder [Navigate through code with the debugger (Navigieren im Code mit dem Debugger)](../debugger/navigating-through-code-with-the-debugger.md).

3. Um das Spielbrett mit Symbolen zu füllen, müssen Sie die `AssignIconsToSquares()`-Methode aufrufen, sobald das Programm startet. Wenn Sie Visual C# verwenden, fügen Sie direkt unterhalb des Aufrufs der `InitializeComponent()`-Methode im **Form1**_constructor_ eine Anweisung hinzu, mit der das Formular die neue Methode aufruft und sich entsprechend einrichtet, bevor es angezeigt wird. Konstruktoren werden aufgerufen, wenn Sie ein neues Objekt erstellen, beispielsweise eine Klasse oder eine Struktur. Weitere Informationen finden Sie unter [Konstruktoren (C#-Programmierhandbuch)](/dotnet/csharp/programming-guide/classes-and-structs/constructors) oder [Verwenden von Konstruktoren und Destruktoren](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\)) in Visual Basic.

     [!code-csharp[VbExpressTutorial4Step2_3_4#13](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_4.cs)]

     In Visual Basic fügen Sie den `AssignIconsToSquares()`-Methodenaufruf der `Form1_Load`-Methode hinzu, sodass der Code wie folgt aussieht.

    ```vb
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        AssignIconsToSquares()
    End Sub
    ```

4. Speichern Sie das Programm, und führen Sie es aus. Es sollte ein Formular mit zufälligen Symbolen angezeigt werden, die den einzelnen Bezeichnungen zugewiesen sind.

5. Schließen Sie das Programm, und führen Sie es erneut aus. In der folgenden Abbildung erkennen Sie, dass den einzelnen Bezeichnungsfeldern nun unterschiedliche Symbole zugewiesen sind.

     ![Gedächtnisspiel mit zufälligen Symbolen](../ide/media/express_tut4step3.png) Gedächtnisspiel mit zufälligen Symbolen

     Die Symbole sind jetzt sichtbar, weil sie nicht ausgeblendet wurden. Um sie vor dem Spieler zu verbergen, können Sie für die **ForeColor**-Eigenschaft jeder Bezeichnung die Farbe der **BackColor**-Eigenschaft verwenden.

    > [!TIP]
    > Eine andere Methode zum Ausblenden von Steuerelementen wie z.B. Bezeichnungen besteht darin, deren **Visible**-Eigenschaft auf **FALSE** festzulegen.

6. Um die Symbole auszublenden, stoppen Sie das Programm und entfernen die Kommentarmarken für die kommentierte Codezeile innerhalb der `For Each`-Schleife.

     [!code-csharp[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_5.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_5.vb)]

7. Wählen Sie auf der Menüleiste die Schaltfläche **Alle speichern**, um das Programm zu speichern, und führen Sie es anschließend aus. Die Symbole scheinen nicht mehr vorhanden zu sein, und es wird nur ein blauer Hintergrund angezeigt. Die Symbole werden jedoch zufällig zugewiesen und sind immer noch vorhanden. Da die Symbole die gleiche Farbe wie der Hintergrund besitzen, sind Sie für den Spieler nicht sichtbar. Es wäre ja auch ein langweiliges Spiel, wenn der Spieler alle Symbole sofort sehen könnte!

## <a name="to-continue-or-review"></a>So fahren Sie fort oder überprüfen die Angaben

- Den nächsten Schritt des Tutorials finden Sie unter [Schritt 4: Hinzufügen eines Click-Ereignishandlers zu jeder Bezeichnung](../ide/step-4-add-a-click-event-handler-to-each-label.md).

- Den vorherigen Schritt des Tutorials finden Sie unter [Schritt 2: Hinzufügen eines zufällig ausgewählten Objekts und einer Liste von Symbolen](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).
