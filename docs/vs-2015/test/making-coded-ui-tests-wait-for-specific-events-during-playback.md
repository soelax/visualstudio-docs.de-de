---
title: Festlegen, dass bei Wiedergabe von Tests der programmierten UI auf bestimmte Ereignisse gewartet wird | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 41981ad6-673e-492e-b739-9863b14157b1
caps.latest.revision: 26
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8c0158370ceb101e8c6934f92e2dd3e8689254c5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686317"
---
# <a name="making-coded-ui-tests-wait-for-specific-events-during-playback"></a>Festlegen, dass bei Wiedergabe von Tests der programmierten UI auf bestimmte Ereignisse gewartet wird
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Sie können bei der Wiedergabe eines Tests der programmierten UI festlegen, dass bei einem Test auf bestimmte Ereignisse gewartet werden soll, z. B. auf das Anzeigen eines Fensters, das Ausblenden einer Statusanzeige usw. Verwenden Sie hierzu die entsprechende „UITestControl.WaitForControlXXX()“-Methode, wie in der folgenden Tabelle beschrieben. Ein Beispiel für einen Test der programmierten UI, bei dem ein Steuerelement auf die Aktivierung mit der <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>-Methode wartet, finden Sie unter [Exemplarische Vorgehensweise: Erstellen, Bearbeiten und Verwalten von Tests der programmierten UI](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)  
  
 **Anforderungen**  
  
 Visual Studio Enterprise  
  
> [!TIP]
> Sie können mithilfe des Test-Editors der programmierten UI zudem Verzögerungen vor Aktionen hinzufügen. Weitere Informationen finden Sie unter [Vorgehensweise: Einfügen einer Verzögerung vor einer UI-Aktion, die mithilfe des Editors der programmierten UI](https://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0).  
  
 **UITestControl.WaitForControlXXX()-Methoden**  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlReady%2A>  
  
 Wartet darauf, dass das Steuerelement bereit ist, Maus- und Tastatureingaben zu akzeptieren. Die Engine ruft diese API für alle Aktionen dahingehend implizit auf, dass darauf gewartet werden soll, dass das Steuerelement bereit ist, bevor ein Vorgang ausgeführt wird. Allerdings in bestimmten vertraulichen Szenarien müssen Sie möglicherweise einen expliziten Aufruf ausführen.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>  
  
 Wartet auf die Aktivierung des Steuerelements, wenn der Assistent einige asynchrone Validierungen der Eingabe durch das Ausführen von Aufrufen am Server vornimmt. Beispielsweise können Sie eine Methode ausstellen, um auf die Aktivierung der Schaltfläche **Weiter** des Assistenten zu warten. Ein Beispiel zu dieser Methode finden Sie unter [Exemplarische Vorgehensweise: Erstellen, Bearbeiten und Verwalten von Tests der programmierten UI](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlExist%2A>  
  
 Wartet darauf, dass das Steuerelement auf der Benutzeroberfläche angezeigt wird. Beispielsweise, wenn Sie ein Fehlerdialogfeld erwarten, nachdem die Anwendung die Validierung der Parameter abgeschlossen hat. Die für die Validierung in Anspruch genommene Zeit ist variabel. Sie können diese Methode verwenden, um auf das Fehlerdialogfeld zu warten.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlNotExist%2A>  
  
 Wartet darauf, dass das Steuerelement auf der Benutzeroberfläche verschwindet. Beispielsweise können Sie auf das Verschwinden der Statusanzeige warten.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyEqual%2A>  
  
 Wartet darauf, dass die angegebene Eigenschaft des Steuerelements den angegebenen Wert aufweist. Beispielsweise, wenn Sie darauf warten, dass der Statustext zu **Fertig** geändert wird.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyNotEqual%2A>  
  
 Wartet darauf, dass die angegebene Eigenschaft des Steuerelements das Gegenteil eines angegebenen Werts aufweist. Beispielsweise, wenn Sie darauf warten, dass das Bearbeitungsfeld nicht länger schreibgeschützt ist, also bearbeitet werden kann.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlCondition%2A>  
  
 Wartet darauf, dass das angegebene Prädikat wieder `true` ist. Dies kann für einen komplexen „wait“-Vorgang (wie OR-Bedingungen) in einem angegebenen Steuerelement verwendet werden. Beispielsweise, wenn Sie darauf warten, bis der Statustext **Erfolgreich** oder **Fehlerhaft** lautet, wie dies im folgenden Code gezeigt wird:  
  
```csharp  
  
// Define the method to evaluate the condition   
private static bool IsStatusDone(UITestControl control)   
{   
    WinText statusText = control as WinText;   
    return statusText.DisplayText == "Succeeded" || statusText.DisplayText == "Failed";   
}   
  
// In test method, wait till the method evaluates to true   
statusText.WaitForControlCondition(IsStatusDone);  
  
```  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForCondition%2A>  
  
 Bei allen vorherigen Methoden handelt es sich um Instanzmethoden von „UITestControl“. Diese Methode ist eine statische Methode. Diese Methode wartet zudem darauf, dass das angegebene Prädikat `true` ist, aber sie kann für einen komplexen „wait“-Vorgang (wie OR-Bedingungen) in mehreren Steuerelementen verwendet werden. Beispielsweise können Sie warten, bis der Statustext **Erfolgreich** lautet oder bis eine Fehlermeldung angezeigt wird, wie dies im folgenden Code gezeigt wird:  
  
```csharp  
  
// Define the method to evaluate the condition   
private static bool IsStatusDoneOrError(UITestControl[] controls)   
{   
    WinText statusText = controls[0] as WinText;   
    WinWindow errorDialog = controls[1] as WinWindow;   
    return statusText.DisplayText == "Succeeded" || errorDialog.Exists;   
}   
  
// In test method, wait till the method evaluates to true   
UITestControl.WaitForCondition<UITestControl[]>(new UITestControl[] { statusText, errorDialog }, IsStatusDoneOrError);  
  
```  
  
 All diese Methoden weisen folgendes Verhalten auf:  
  
 Die Methoden geben „true“ zurück, wenn die Wartezeit erfolgreich ist, andernfalls wird „false“ zurückgegeben.  
  
 Das implizite Timeout für den Wartevorgang wird durch die Eigenschaft <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyTimeout%2A> angegeben. Der Standardwert dieser Eigenschaft ist „60000“ Millisekunden (eine Minute).  
  
 Die Methoden verfügen über eine Überladung für ein explizites Timeout in Millisekunden. Wenn der „wait“-Vorgang in einer impliziten Suche nach dem Steuerelement resultiert oder wenn die Anwendung ausgelastet ist, könnte die tatsächliche Wartezeit größer sein als der angegebene Timeout.  
  
 Die vorherigen Funktionen sind leistungsstark und flexibel und sollten fast alle Bedingungen erfüllen. Im Falle, dass diese Methoden Ihre Anforderungen jedoch nicht erfüllen, müssen Sie <xref:Microsoft.VisualStudio.TestTools.UITesting.Playback.Wait%2A> oder <xref:System.Threading.Thread.Sleep%2A> in Ihrem Code codieren. Es wird empfohlen, „Playback.Wait()“ anstelle der „Thread.Sleep()“-API zu verwenden. Die Gründe hierfür sind:  
  
 Sie können die <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.ThinkTimeMultiplier%2A>-Eigenschaft zum Ändern der Dauer des Standbymodus ändern. Standardmäßig ist diese Variable „1“. Sie können sie jedoch erhöhen oder verringern, um die Wartezeit über den gesamten Code hinweg zu ändern. Wenn Sie Tests insbesondere über ein langsames Netzwerk vornehmen oder wenn ein anderer langsamer Leistungsfall vorliegt, können Sie diese Variable an einer Stelle (oder sogar in der Konfigurationsdatei) auf „1,5“ ändern, um eine zusätzliche Wartezeit von 50 % an allen anderen Stellen hinzuzufügen.  
  
 „Playback.Wait()“ ruft „Thread.Sleep()“ (nach obiger Berechnung) intern in kleineren Blöcken in einer „for“-Schleife auf, während die Überprüfung für den „cancel\break“-Vorgang erfolgt. Mit „Playback.Wait()“ können Sie die Wiedergabe vor dem Ende der Wartezeit abbrechen, während der Standbymodus möglicherweise eine Ausnahme auslöst.  
  
> [!TIP]
> Mit dem Editor für Tests der programmierten UI können Sie Tests der programmierten UI mühelos ändern. Er ermöglicht das Suchen, Anzeigen und Bearbeiten der Testmethoden. Sie können auch UI-Aktionen und die zugehörigen Steuerelemente in der UI-Steuerelementzuordnung bearbeiten. Weitere Informationen finden Sie unter [Bearbeiten von Tests der programmierten UI mit dem Test-Editor für programmierte UI](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).  
  
 **Empfehlungen**  
  
 Weitere Informationen finden Sie unter [Tests für fortlaufende Übermittlung mit Visual Studio 2012 – Kapitel 5: Automatisieren von Systemtests](http://go.microsoft.com/fwlink/?LinkID=255196)  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Benutzeroberflächenautomatisierung zum Testen des Codes](../test/use-ui-automation-to-test-your-code.md)   
 [Erstellen von Tests der codierten UI](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)   
 [Exemplarische Vorgehensweise: Erstellen, bearbeiten und Verwalten von Tests der programmierten UI](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)   
 [Anatomy of a Coded UI Test (Aufbau eines Tests der programmierten UI)](../test/anatomy-of-a-coded-ui-test.md)   
 [Supported Configurations and Platforms for Coded UI Tests and Action Recordings (Unterstützte Konfigurationen und Plattformen für Tests der programmierten UI und Aktionsaufzeichnungen)](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)   
 [Vorgehensweise: Einfügen einer Verzögerung vor einer UI-Aktion, die mithilfe des Editors der programmierten UI](https://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0)
