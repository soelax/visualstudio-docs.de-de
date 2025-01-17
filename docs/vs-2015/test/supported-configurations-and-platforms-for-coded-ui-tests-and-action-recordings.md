---
title: Unterstützte Konfigurationen und Plattformen für Tests der programmierten UI und Aktionsaufzeichnungen | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests
ms.assetid: 544742b5-4ec1-4d51-b941-72b2f6ff17bc
caps.latest.revision: 108
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 978979cfa7b374c7f1247a0ce582548ef1e87022
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705972"
---
# <a name="supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings"></a>Unterstützte Konfigurationen und Plattformen für Tests der programmierten UI und Aktionsaufzeichnungen
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Die unterstützten Konfigurationen und Plattformen für Tests der codierten UI für Visual Studio Enterprise werden in der folgenden Tabelle aufgeführt. Diese Konfigurationen gelten auch für Aktionsaufzeichnungen, die mit [!INCLUDE[MTRlong](../includes/mtrlong-md.md)]erstellt wurden.  
  
> [!NOTE]
> Der Prozess für den Test der codierten UI muss über die gleichen Rechte wie die getestete App verfügen.  
  
 **Anforderungen**  
  
- Visual Studio Enterprise  
  
## <a name="supported-configurations"></a>Unterstützte Konfigurationen  
  
|Konfiguration|Unterstützt|  
|-------------------|---------------|  
|Betriebssysteme|[!INCLUDE[win7](../includes/win7-md.md)]<br /><br /> [!INCLUDE[winsvr08_r2](../includes/winsvr08-r2-md.md)]<br /><br /> [!INCLUDE[win8](../includes/win8-md.md)]<br /><br /> Windows 10|  
|32-/64-Bit-Unterstützung|Windows-Betriebssysteme (32-Bit), auf denen [!INCLUDE[TCMext](../includes/tcmext-md.md)] (32-Bit) ausführt wird, können 32-Bit-Anwendungen testen.<br /><br /> Windows-Betriebssysteme (64-Bit), auf denen [!INCLUDE[TCMext](../includes/tcmext-md.md)] (32-Bit) ausführt wird, können 32-Bit-WOW-Anwendungen mit Benutzeroberflächensynchronisierung testen.<br /><br /> Windows-Betriebssysteme (64-Bit), auf denen [!INCLUDE[TCMext](../includes/tcmext-md.md)] (32-Bit) ausgeführt wird, können Windows Forms- und WPF-Anwendungen (64-Bit) ohne Benutzeroberflächensynchronisierung testen.|  
|Architektur|x86 und x64 **Hinweis:**  Internet Explorer wird im 64-Bit-Modus nur bei Ausführung unter [!INCLUDE[win8](../includes/win8-md.md)] oder höheren Versionen unterstützt.|  
|.NET|.NET 2.0, 3.0, 3.5, 4 und 4.5. **Hinweis:** [!INCLUDE[TCMext](../includes/tcmext-md.md)] und Visual Studio setzen .NET 4 voraus. Mit den aufgeführten .NET-Versionen entwickelte Anwendungen werden jedoch unterstützt.|  
  
> [!NOTE]
> Die*Benutzeroberflächensynchronisierung* ist eine Funktion, bei der die Wiedergabe in die Nachrichtenwarteschlange jedes Steuerelements überprüft wird. Wenn ein Steuerelement nicht auf das Ereignis reagierte, das an es gesendet wurde, wird das Ereignis erneut gesendet.  
  
## <a name="platform-support"></a>Plattformunterstützung  
  
|Plattform|Grad der Unterstützung|  
|--------------|----------------------|  
|Windows Phone-Apps|Nur auf WinRT-XAML basierende Phone-Apps werden unterstützt.|  
|Windows Store-Apps|Nur XAML-basierte Store-Apps werden unterstützt.|  
|Universelle Windows-Apps|Nur XAML-basierte universelle Windows-Apps für Phone und Desktop werden unterstützt.|  
|Microsoft Edge|In Visual Studio 2015 Update 2 und höher durch Verwendung der [Erweiterung für browserübergreifende Tests der programmierten UI](https://visualstudiogallery.msdn.microsoft.com/11cfc881-f8c9-4f96-b303-a2780156628d)|  
|Internet Explorer 8<br /><br /> Internet Explorer 9<br /><br /> Internet Explorer 10 **Wichtig:**  Internet Explorer 10 wird nur auf dem Desktop unterstützt. <br /><br /> Internet Explorer 11 **Wichtig:**  Internet Explorer 11 wird nur auf dem Desktop unterstützt.|Vollständige Unterstützung<br /><br /> -   **Unterstützung für HTML5 im Internet Explorer 9 und 10:** Tests der programmierten UI unterstützen die Aufzeichnung, Wiedergabe und Validierung der HTML5-Steuerelemente: Audio, Video, ProgressBar und Schieberegler. Weitere Informationen finden Sie unter [Using HTML5 Controls in Coded UI Tests (Verwenden von HTML5-Steuerelementen in Tests der programmierten UI)](../test/using-html5-controls-in-coded-ui-tests.md). **Warnung:**      Wenn Sie einen Test der programmierten UI in Internet Explorer 10 erstellen, wird dieser mit Internet Explorer 9 oder Internet Explorer 8 möglicherweise nicht ausgeführt. Der Grund hierfür ist, dass Internet Explorer 10 HTML5-Steuerelemente wie Audio, Video, ProgressBar und Schieberegler enthält. Diese HTML5-Steuerelemente werden von Internet Explorer 9 oder Internet Explorer 8 nicht erkannt. Entsprechend kann der Test der codierten UI unter Verwendung von Internet Explorer 9 einige HTML5-Steuerelemente enthalten, die auch nicht von Internet Explorer 8 erkannt werden.<br />-   **Unterstützung für die Rechtschreibprüfung von Internet Explorer 10:** Internet Explorer 10 enthält Rechtschreibprüfungsfunktionen für alle Textfelder. Dadurch können Sie aus einer Liste vorgeschlagener Korrekturen wählen. Der Test der codierten UI ignoriert Benutzeraktionen wie das Auswählen eines alternativen Rechtschreibvorschlags. Nur der endgültige in das Textfeld eingegebene Text wird aufgezeichnet.<br />     Die folgenden Aktionen werden für Tests der programmierten UI aufgezeichnet, die das Steuerelement für die Rechtschreibprüfung verwenden: „Zum Wörterbuch hinzufügen“, „Kopieren“, „Alle auswählen“ und „Ignorieren“.<br />-   **Unterstützung für Internet Explorer (64-Bit-Version) unter Windows 8:** Zuvor wurden 64-Bit-Versionen von Internet Explorer für Aufzeichnung und Wiedergabe nicht unterstützt. Mit [!INCLUDE[win8](../includes/win8-md.md)] und [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]können Tests der codierten UI für 64-Bit-Versionen von Internet Explorer ausgeführt werden. **Warnung:**      Die 64-Bit-Unterstützung für Internet Explorer gilt nur unter [!INCLUDE[win8](../includes/win8-md.md)] oder höher.<br />-   **Unterstützung für angeheftete Sites in Internet Explorer 9:** Mit Internet Explorer 9 wurden angeheftete Sites eingeführt. Mit angehefteten Websites können Sie Ihre Lieblingssites direkt über die Windows-Taskleiste aufrufen, ohne Internet Explorer zuerst öffnen zu müssen. Tests der codierten UI können nun absichtbewusste Aktionen für angeheftete Sites generieren. Weitere Informationen über angeheftete Sites finden Sie unter [Angeheftete Sites](http://go.microsoft.com/fwlink/?LinkId=220037).<br />-   **Unterstützung für semantische Tags in Internet Explorer 9:** Mit Internet Explorer 9 wurden die folgenden semantischen Tags eingeführt: section, nav, article, aside, hgroup, header, footer, figure, figcaption und mark. Tests der codierten UI ignorieren all diese semantischen Tags während der Aufzeichnung. Sie können mit dem Test-Generator für codierte UI Assertionen für diese Tags hinzufügen. Mit der Navigationssteuerung im Test-Generator für codierte UI können Sie zu all diesen Elementen navigieren und die zugehörigen Eigenschaften anzeigen.<br />-   **Nahtlose Behandlung von Leerzeichen zwischen Versionen von Internet Explorer:** Bei der Behandlung von Leerzeichen gibt es Unterschiede zwischen Internet Explorer 8, Internet Explorer 9 und Internet Explorer 10. Der Test der codierten UI behandelt diese Unterschiede nahtlos. Daher wird ein Test der codierten UI, der in Internet Explorer 8 erstellt wurde, beispielsweise problemlos in Internet Explorer 9 und Internet Explorer 10 wiedergegeben.<br />-   **Der Infobereich von Internet Explorer sind werden jetzt mit dem festgelegten Attribut "Bei Fehler fortsetzen" aufgezeichnet:** Alle Aktionen im Infobereich von Internet Explorer werden nun mit dem Attribut "Bei Fehler fortsetzen" aufgezeichnet. Wenn der Infobereich während der Wiedergabe nicht angezeigt wird, werden die Aktionen darin ignoriert, und der Test der codierten UI wird mit der nächsten Aktion fortgesetzt.|  
|Steuerelemente von Drittanbietern für Windows Forms und WPF|Vollständige Unterstützung<br /><br /> Um Steuerelemente von Drittanbietern in Windows Forms- und WPF-Anwendungen zu aktivieren, müssen Sie Verweise und Code hinzufügen. Weitere Informationen finden Sie unter [Aktivieren von Tests der programmierten UI Ihrer Steuerelemente](../test/enable-coded-ui-testing-of-your-controls.md).|  
|Internet Explorer 6<br /><br /> Internet Explorer 7|Wird nicht unterstützt.|  
|Chrome<br /><br /> Firefox|Die Aufzeichnung von Aktionsschritten wird nicht unterstützt. Coded UI-Tests können auf den Browsern Chrome und Firefox mit Visual Studio 2012 Update 4 oder höher wiedergegeben werden. Klicken Sie [hier](https://msdn.microsoft.com/library/jj835758.aspx) , um weitere Informationen zu erhalten.|  
|Opera<br /><br /> Safari|Wird nicht unterstützt.|  
|Silverlight|Wird nicht unterstützt.<br /><br /> Für Visual Studo 2013 können Sie jedoch das [Microsoft Visual Studio 2013 Coded UI Test Plugin for Silverlight](https://go.microsoft.com/fwlink/?LinkId=691026) aus der Visual Studio Gallery herunterladen.|  
|Flash/Java|Wird nicht unterstützt.|  
|Windows Forms 2.0 und höher|Vollständige Unterstützung **Hinweis**:  NetFx-Steuerelemente werden vollständig unterstützt, dies gilt jedoch nicht für alle Steuerelemente von Drittanbietern.|  
|WPF 3.5 und höher|Vollständige Unterstützung<br /><br /> **Hinweis** NetFx-Steuerelemente werden vollständig unterstützt, dies gilt jedoch nicht für alle Steuerelemente von Drittanbietern.|  
|Windows Win32|Funktioniert möglicherweise mit einigen bekannten Problemen, wird jedoch nicht offiziell unterstützt.|  
|MFC|Teilweise unterstützt. Auf der folgenden [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkId=206511) finden Sie Details zu den unterstützten Funktionen.|  
|SharePoint|Vollständige Unterstützung|  
|Office-Clientanwendungen|Wird nicht unterstützt.|  
|Dynamics CRM-Webclient|Vollständige Unterstützung|  
|Dynamics (Ax) 2012-Client|Aktionsaufzeichnung und -wiedergabe werden teilweise unterstützt. Weitere Informationen finden Sie auf der folgenden [Microsoft-Webssite](http://go.microsoft.com/fwlink/?LinkId=232677) .|  
|SAP|Wird nicht unterstützt.|  
|Citrix/Terminaldienste|Das Aufzeichnen von Aktionen auf einem Terminalserver wird nicht empfohlen. Die Aufzeichnung unterstützt nicht, dass mehrere Instanzen gleichzeitig ausgeführt werden.|  
|PowerBuilder|Teilweise unterstützt.<br /><br /> Die Unterstützung erfolgt in dem Umfang, in dem der Zugang zu PowerBuilder-Steuerelementen ermöglicht wird.|  
  
 Informationen zum Erstellen von Erweiterungen zur Unterstützung anderer Plattformen finden Sie unter [Aktivieren von Tests der programmierten UI Ihrer Steuerelemente](../test/enable-coded-ui-testing-of-your-controls.md) und [Extending Coded UI Tests and Action Recordings to Support Microsoft Excel (Erweitern von Tests der programmierten UI und Aktionsaufzeichnungen zur Unterstützung von Microsoft Excel)](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Benutzeroberflächenautomatisierung zum Testen des Codes](../test/use-ui-automation-to-test-your-code.md)   
 [Gewusst wie: Generieren eines Tests der codierten UI aus einer vorhandenen Aktionsaufzeichnung](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)
