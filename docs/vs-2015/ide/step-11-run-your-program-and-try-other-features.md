---
title: 'Schritt 11: Ausführen des Programms und Ausprobieren weiterer Funktionen | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 656614d0-4fe7-4a67-8edc-c10919377d09
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d5a40d6aa7dca8b14210ea85b8428f4d315cd70b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679539"
---
# <a name="step-11-run-your-program-and-try-other-features"></a>Schritt 11: Ausführen des Programms und Ausprobieren weiterer Features
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Das Programm ist fertig und bereit zur Ausführung. Sie können das Programm ausführen und die Hintergrundfarbe von PictureBox festlegen. Um den Lerneffekt zu erhöhen, können Sie das Programm verbessern, indem Sie die Farbe des Formulars ändern, die Schaltflächen und das Kontrollkästchen anpassen und die Eigenschaften des Formulars ändern.  
  
 Informationen zum Herunterladen einer vollständige Version des Beispiels finden Sie unter [Tutorialbeispiel für vollständiges Bildanzeigeprogramm](http://code.msdn.microsoft.com/Complete-Picture-Viewer-7d91d3a8).  
  
 ![Link zum Video](../data-tools/media/playvideo.gif "PlayVideo")eine Videoversion dieses Themas finden Sie unter [Tutorial 1: Erstellen eines Bildanzeigeprogramms in Visual Basic - Video 5](http://go.microsoft.com/fwlink/?LinkId=205216) oder [Lernprogramm 1: Erstellen eines Bildanzeigeprogramms in C# -Video 5](http://go.microsoft.com/fwlink/?LinkId=205206). Diese Videos verwenden eine frühere Version von Visual Studio, sodass Menübefehle und andere Benutzeroberflächenelemente geringfügig abweichen können. Allerdings funktionieren die Konzepte und Prozeduren in der aktuellen Version von Visual Studio auf ähnliche Weise.  
  
### <a name="to-run-your-program-and-set-the-background-color"></a>So können Sie das Programm ausführen und die Hintergrundfarbe festlegen  
  
1. Wählen Sie F5 oder in der Menüleiste **Debuggen**, **Debuggen starten** aus.  
  
2. Bevor Sie ein Bild öffnen, wählen Sie die Schaltfläche **Hintergrundfarbe festlegen** aus. Das Dialogfeld **Farbe** wird geöffnet.  
  
     ![Dialogfeld „Farbe“](../ide/media/express-colordialog.png "Express_FarbeDialogfeld")  
Dialogfeld "Farbe"  
  
3. Wählen Sie eine Farbe aus, um die PictureBox-Hintergrundfarbe festzulegen. Schauen Sie sich die `backgroundButton_Click()`-Methode genau an, um zu verstehen, wie sie funktioniert.  
  
    > [!NOTE]
    > Sie können aus dem Internet ein Bild laden, indem Sie die URL des Bilds in das Dialogfeld **Datei öffnen** einfügen. Versuchen Sie, ein Bild mit einem transparenten Hintergrund zu finden, damit die Hintergrundfarbe angezeigt wird.  
  
4. Wählen Sie die Schaltfläche **Bild löschen** aus, um sicherzustellen, das es gelöscht wird. Beenden Sie dann das Programm, indem Sie die Schaltfläche **Schließen** auswählen.  
  
### <a name="to-try-other-features"></a>So probieren Sie weitere Funktionen aus  
  
- Ändern Sie die Farbe des Formulars und der Schaltflächen mit der **BackColor**-Eigenschaft.  
  
- Passen Sie die Schaltflächen und das Kontrollkästchen mit den Eigenschaften **Font** und **ForeColor** an.  
  
- Ändern Sie die Eigenschaften **FormBorderStyle** und **ControlBox** des Formulars.  
  
- Verwenden Sie die Eigenschaften **AcceptButton** und **CancelButton** des Formulars, damit Schaltflächen automatisch ausgewählt werden, wenn der Benutzer die EINGABETASTE oder ESC-TASTE auswählt. Veranlassen Sie, dass das Programm das Dialogfeld **Datei öffnen** öffnet, wenn der Benutzer die EINGABETASTE auswählt, und das Dialogfeld schließt, wenn der Benutzer ESC auswählt.  
  
### <a name="to-continue-or-review"></a>So fahren Sie fort oder überprüfen die Angaben  
  
- Weitere Informationen zum Programmieren in Visual Studio finden Sie unter [Programmierkonzepte](https://msdn.microsoft.com/library/65c12cca-af4f-4017-886e-2dbc00a189d6).  
  
- Weitere Informationen zu Visual Basic finden Sie unter [Entwickeln von Anwendungen mit Visual Basic](https://msdn.microsoft.com/library/1e1c0c81-6d95-4167-a98b-44b1efb6d25f).  
  
- Weitere Informationen zu Visual C# finden Sie in der [Einführung in die Programmiersprache C# und in .NET Framework](https://msdn.microsoft.com/library/0a2dff4e-cd84-42ff-8141-e89889b24081).  
  
- Das nächste Tutorial finden Sie unter [Tutorial 2: Erstellen ein Mathequiz mit Zeitmessung](../ide/tutorial-2-create-a-timed-math-quiz.md).  
  
- Den vorherigen Schritt des Tutorials finden Sie unter [Schritt 10: Schreiben von Code für zusätzliche Schaltflächen und ein Kontrollkästchen](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md).
