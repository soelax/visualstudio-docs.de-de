---
title: Binden von WPF-Steuerelemente an einen WCF Data Service | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 8823537c-82f0-41f7-bf30-705f0e5e59fd
caps.latest.revision: 44
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fb08a016261ac0836ba6dd2dde5d8b0812aab806
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704920"
---
# <a name="bind-wpf-controls-to-a-wcf-data-service"></a>Binden von WPF-Steuerelementen an einen WCF-Datendienst
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In dieser exemplarischen Vorgehensweise erstellen Sie eine WPF-Anwendung, die datengebundene Steuerelemente enthält. Die Steuerelemente sind an Kundendatensätze gebunden, die in einem [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] gekapselt sind. Sie fügen außerdem die Schaltflächen hinzu, mit denen Kunden Datensätze anzeigen und ändern können.  
  
 In dieser exemplarischen Vorgehensweise werden die folgenden Aufgaben veranschaulicht:  
  
- Erstellen eines Entity Data Models, das aus Daten in der Beispieldatenbank AdventureWorksLT generiert wird.  
  
- Erstellen einer [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] , der die Daten im Entity Data Model zu einer WPF-Anwendung verfügbar macht.  
  
- Erstellen eines Satzes datengebundener Steuerelemente durch Ziehen von Elementen aus dem Fenster **Datenquellen** zum WPF-Designer.  
  
- Erstellen von Schaltflächen, mit denen die Navigation vorwärts und rückwärts durch die Kundendatensätze möglich ist.  
  
- Erstellen eine Schaltfläche, die für das Speichern von Änderungen an Daten in den Steuerelementen der [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] und der zugrunde liegenden Datenquelle.  
  
   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Vorraussetzungen  
 Zum Durchführen dieser exemplarischen Vorgehensweise benötigen Sie die folgenden Komponenten:  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
  
- Zugriff auf eine laufende Instanz von SQL Server oder SQL Server Express, an die eine AdventureWorksLT-Beispieldatenbank angefügt ist. Sie können die AdventureWorksLT-datenbankvon der [CodePlex-Website](http://go.microsoft.com/fwlink/?linkid=87843).  
  
  Vorkenntnisse der folgenden Konzepte sind ebenfalls hilfreich, wenn auch für die Durchführung der exemplarischen Vorgehensweise nicht erforderlich:  
  
- WCF Data Services. Weitere Informationen finden Sie unter [Übersicht](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb).  
  
- Datenmodelle in [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)].  
  
- Entity Data Models und der ADO.NET Entity Framework. Weitere Informationen finden Sie unter [Übersicht über Entity Framework](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0).  
  
- Arbeiten mit dem WPF-Designer. Weitere Informationen finden Sie unter [WPF- und Silverlight Designer Overview](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62).  
  
- WPF-Datenbindung. Weitere Informationen finden Sie unter [Übersicht über Datenbindung](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211).  
  
## <a name="create-the-service-project"></a>Erstellen Sie das Dienstprojekt  
 Beginnen Sie diese exemplarische Vorgehensweise, indem Sie ein Projekt für einen [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] erstellen.  
  
#### <a name="to-create-the-service-project"></a>So erstellen Sie das Dienstprojekt  
  
1. Starten Sie Visual Studio.  
  
2. Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
3. Erweitern Sie **Visual C#** oder**Visual Basic**, und wählen Sie dann **Web**.  
  
4. Wählen Sie die Projektvorlage **ASP.NET-Webanwendung** aus.  
  
5. In der **Namen** geben `AdventureWorksService` , und klicken Sie auf **OK**.  
  
     Visual Studio erstellt die `AdventureWorksService` Projekt.  
  
6. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf **Default.aspx**, und wählen Sie **Löschen** aus. Diese Datei wird für diese exemplarische Vorgehensweise benötigt.  
  
## <a name="create-an-entity-data-model-for-the-service"></a>Erstellen eines Entity Data Model für den Dienst  
 Damit die Daten mithilfe eines [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] für eine Anwendung verfügbar gemacht werden, müssen Sie ein Datenmodell für den Dienst definieren. Die [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] unterstützt zwei Arten von Datenmodellen: Entity Data Models und benutzerdefinierte Datenmodelle, die definiert sind, mit der common Language Runtime (CLR)-Objekte, implementieren die <xref:System.Linq.IQueryable%601> Schnittstelle. In dieser exemplarischen Vorgehensweise erstellen Sie ein Entity Data Model für das Datenmodell.  
  
#### <a name="to-create-an-entity-data-model"></a>So erstellen Sie ein Entity Data Model  
  
1. Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**.  
  
2. Klicken Sie in der Liste „Installierte Vorlagen“ auf **Daten**, und wählen Sie dann das Projektelement **ADO.NET Entity Data Model** aus.  
  
3. Ändern Sie den Namen in `AdventureWorksModel.edmx`, und klicken Sie auf **hinzufügen**.  
  
     Der **Assistent für Entity Data Model** wird geöffnet.  
  
4. Klicken Sie auf der Seite **Modellinhalt auswählen** auf **Aus Datenbank generieren**, und klicken Sie auf **Weiter**.  
  
5. Wählen Sie auf der Seite **Wählen Sie Ihre Datenverbindung aus** eine der folgenden Optionen aus:  
  
    - Wenn in der Dropdownliste eine Datenverbindung zur Beispieldatenbank "AdventureWorksLT" verfügbar ist, wählen Sie diese aus.  
  
    - Klicken Sie **Neue Verbindung**, und erstellen Sie eine Verbindung zur Datenbank AdventureWorksLT.  
  
6. Achten Sie darauf, dass auf der Seite **Wählen Sie Ihre Datenverbindung aus** die Option **Entitätsverbindungseinstellungen in App.Config speichern unter**, und klicken Sie dann auf **Weiter**.  
  
7. Erweitern Sie auf der Seite **Datenbankobjekte auswählen** den Punkt **Tabellen**, und wählen Sie dann die Tabelle **SalesOrderHeader** aus.  
  
8. Klicken Sie auf **Fertig stellen**.  
  
## <a name="create-the-service"></a>Erstellen Sie den Dienst.  
 Erstellen Sie eine [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] , die Daten im Entity Data Model zu einer WPF-Anwendung verfügbar zu machen.  
  
#### <a name="to-create-the-service"></a>So erstellen Sie den Dienst  
  
1. Wählen Sie im Menü **Projekt** die Option **Neues Element hinzufügen** aus.  
  
2. Klicken Sie in der Liste der installierten Vorlagen auf **Web**, und wählen Sie dann die **WCF Data Service** Projektelement.  
  
3. In der **Namen** geben `AdventureWorksService.svc`, und klicken Sie auf **hinzufügen**.  
  
     Visual Studio fügt die `AdventureWorksService.svc` zum Projekt.  
  
## <a name="configure-the-service"></a>Konfigurieren Sie den Dienst.  
 Damit der Dienst mit dem von Ihnen erstellten Entity Data Model funktioniert, muss er konfiguriert werden.  
  
#### <a name="to-configure-the-service"></a>So konfigurieren Sie den Dienst  
  
1. In der `AdventureWorks.svc` Codedatei, ersetzen Sie die `AdventureWorksService` Klassendeklaration durch den folgenden Code.  
  
     [!code-csharp[Data_WPFWCF#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworksservice.svc.cs#1)]
     [!code-vb[Data_WPFWCF#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworksservice.svc.vb#1)]  
  
     Dieser Code aktualisiert die `AdventureWorksService` Klasse, sodass sie von abgeleitet wird ein <xref:System.Data.Services.DataService%601> den Zugriff auf die `AdventureWorksLTEntities` Context-Klasse im Entity Data Model-Objekt. Außerdem aktualisiert er die Methode `InitializeService`, sodass Clients des Diensts vollen Lese-/Schreibzugriff auf die `SalesOrderHeader`-Entität haben.  
  
2. Erstellen Sie das Projekt und überprüfen Sie, ob es fehlerfrei erstellt wird.  
  
## <a name="create-the-wpf-client-application"></a>Erstellen der WPF-Clientanwendung  
 Um Daten aus dem [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] anzuzeigen, erstellen Sie eine neue WPF-Anwendung mit einer Datenquelle, die auf dem Dienst basiert. Später in dieser exemplarischen Vorgehensweise werden Sie datengebundene Steuerelemente zur Anwendung hinzufügen.  
  
#### <a name="to-create-the-wpf-client-application"></a>So erstellen Sie die WPF-Clientanwendung  
  
1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Lösungsknoten, dann auf **Hinzufügen**, und wählen Sie dann **Neues Projekt** aus.  
  
2. Erweitern Sie im Dialogfeld **Neues Projekt** den Punkt **Visual C#** oder **Visual Basic**, und wählen Sie dann **Windows**.  
  
3. Wählen Sie die Projektvorlage **WPF-Anwendung** aus.  
  
4. Geben Sie im Feld **Name** die Bezeichnung `AdventureWorksSalesEditor` ein, und klicken Sie auf **OK**.  
  
     Visual Studio fügt die `AdventureWorksSalesEditor` Projekt der Projektmappe.  
  
5. Klicken Sie im Menü **Daten** auf **Datenquellen anzeigen**.  
  
     Das Fenster **Datenquellen** wird geöffnet.  
  
6. Klicken Sie im **Datenquellenfenster** auf **Neue Datenquelle hinzufügen**.  
  
     Der **Assistent zum Konfigurieren von Datenquellen** wird geöffnet.  
  
7. Wählen Sie auf der Seite **Datenquellentyp auswählen** des Assistenten **Dienst**, und klicken Sie auf **Weiter**.  
  
8. Klicken Sie im Dialogfeld **Dienstverweis hinzufügen** auf **Ermitteln**.  
  
     Visual Studio durchsucht die aktuelle Lösung nach verfügbaren Diensten und fügt `AdventureWorksService.svc` zur Liste der verfügbaren Dienste in der **Services** Feld.  
  
9. In der **Namespace** geben `AdventureWorksService`.  
  
10. Geben Sie im Feld **Dienste** den Namen **AdventureWorksService.svc** ein, und klicken Sie auf **OK**.  
  
     Visual Studio lädt die Dienstinformation herunter und gibt dann an die **Datenquellenkonfiguration** Assistenten.  
  
11. Klicken Sie auf der Seite **Dienstverweis hinzufügen** auf **Fertig stellen**.  
  
     Visual Studio fügt Knoten hinzu, der die vom Dienst zurückgegebenen Daten im Fenster **Datenquellen** anzeigt.  
  
## <a name="define-the-user-interface-of-the-window"></a>Die Benutzeroberfläche des Fensters definieren  
 Fügen Sie dem Fenster eine Reihe von Schaltflächen hinzu, indem Sie XAML im WPF-Designer ändern. Später in dieser exemplarischen Vorgehensweise fügen Sie dann Code hinzu, mit dem Anwender die Verkaufsdatensätze mithilfe dieser Schaltflächen anzeigen und ändern können.  
  
#### <a name="to-create-the-window-layout"></a>So erstellen Sie das Fensterlayout  
  
1. In **Projektmappen-Explorer**, doppelklicken Sie auf "MainWindow.xaml".  
  
     Das Fenster wird automatisch im WPF-Designer geöffnet.  
  
2. Fügen Sie in der [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)]-Ansicht des Designers den folgenden Code zwischen den `<Grid>`-Tags hinzu:  
  
    ```  
    <Grid.RowDefinitions>  
        <RowDefinition Height="75" />  
        <RowDefinition Height="525" />  
    </Grid.RowDefinitions>  
    <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>  
    <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>  
    <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>  
    ```  
  
3. Erstellen Sie das Projekt.  
  
## <a name="create-the-data-bound-controls"></a>Erstellen Sie die datengebundenen Steuerelemente  
 Erstellen Sie Steuerelemente, die Kundendatensätze, indem Sie ziehen anzeigen die `SalesOrderHeaders` Knoten aus der **Datenquellen** in den Designer.  
  
#### <a name="to-create-the-data-bound-controls"></a>So erstellen Sie ein datengebundene Steuerelemente  
  
1. Klicken Sie im Fenster **Datenquellen** das Dropdownmenü für den Knoten **SalesOrderHeaders**, und wählen Sie **Details**.  
  
2. Erweitern Sie den Knoten **SalesOrderHeaders**.  
  
3. In diesem Beispiel werden einige Felder nicht angezeigt. Klicken Sie also das Dropdownmenü neben den folgenden Knoten, und wählen Sie **Keine**:  
  
   - **CreditCardApprovalCode**  
  
   - **ModifiedDate**  
  
   - **OnlineOrderFlag**  
  
   - **RevisionNumber**  
  
   - **Rowguid**  
  
     Durch diese Aktion wird Visual Studio daran gehindert, im nächsten Schritt datengebundene Steuerelemente für diese Knoten zu erstellen. In dieser exemplarischen Vorgehensweise wird davon ausgegangen Sie, dass der Endbenutzer nicht, diese Daten anzuzeigen.  
  
4. Ziehen Sie aus dem Fenster **Datenquellen** den Knoten **SalesOrderHeaders** auf das Raster unter der Zeile, in der die Schaltflächen sind.  
  
    Visual Studio erzeugt XAML und Code, der einen Satz von Steuerelementen erstellt, die mit Daten in der Tabelle **Product** verbunden sind. Weitere Informationen zu den generierten XAML und Code finden Sie unter [Binden von WPF-Steuerelementen an Daten in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
5. Klicken Sie im Designer auf das Textfeld neben der Bezeichnung **Customer ID**.  
  
6. Aktivieren Sie im Fenster **Eigenschaften** das Kontrollkästchen neben der Eigenschaft **IsReadOnly**.  
  
7. Legen Sie die Eigenschaft **IsReadOnly** für jedes der folgenden Textfelder fest:  
  
   - **Purchase Order Number**  
  
   - **Sales Order ID**  
  
   - **Sales Order Number**  
  
## <a name="load-the-data-from-the-service"></a>Laden Sie die Daten aus dem Dienst  
 Verwenden Sie den Webdienstproxy-Objekts, um die Umsatzdaten aus dem Dienst zu laden. Klicken Sie dann die Datenquelle für die zurückgegebenen Daten weisen die <xref:System.Windows.Data.CollectionViewSource> im WPF-Fenster.  
  
#### <a name="to-load-the-data-from-the-service"></a>So laden Sie die Daten aus dem Dienst  
  
1. Im Designer zum Erstellen der `Window_Loaded` Ereignishandler, doppelklicken Sie auf den Text, der liest: **MainWindow**.  
  
2. Ersetzen Sie den Ereignishandler durch den folgenden Code. Achten Sie darauf, dass Sie die Adresse *localhost* in diesem Code durch die lokale Hostadresse Ihres Entwicklungscomputers ersetzen.  
  
     [!code-csharp[Data_WPFWCF#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFWCF#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#2)]  
  
## <a name="navigatesales-records"></a>Navigatesales Datensätze  
 Fügen Sie Code hinzu, mit dessen Hilfe Benutzer durch die Salesdatensätze scrollen können, indem Sie die Schaltflächen **\<** und **>** verwenden.  
  
#### <a name="to-enable-users-to-navigate-sales-records"></a>Benutzern das Navigieren durch Sales Records ermöglichen  
  
1. Doppelklicken Sie im Designer die Schaltfläche **<** auf der Fensteroberfläche.  
  
     Visual Studio öffnet die CodeBehind-Datei und erstellt einen neuen `backButton_Click`-Ereignishandler für das <xref:System.Windows.Controls.Primitives.ButtonBase.Click>-Ereignis.  
  
2. Fügen Sie dem generierten `backButton_Click`-Ereignishandler folgenden Code hinzu:  
  
     [!code-csharp[Data_WPFWCF#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFWCF#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#3)]  
  
3. Kehren Sie zum Designer zurück, und doppelklicken Sie auf die Schaltfläche **>**.  
  
     Visual Studio öffnet die CodeBehind-Datei und erstellt einen neuen `nextButton_Click`-Ereignishandler für das <xref:System.Windows.Controls.Primitives.ButtonBase.Click>-Ereignis.  
  
4. Fügen Sie dem generierten `nextButton_Click`-Ereignishandler folgenden Code hinzu:  
  
     [!code-csharp[Data_WPFWCF#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFWCF#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#4)]  
  
## <a name="saving-changes-to-sales-records"></a>Änderungen an sales Records speichern  
 Fügen Sie Code, mit der Benutzer sowohl anzeigen als auch Änderungen an sales Records speichern, indem, die **speichern Änderungen** Schaltfläche.  
  
#### <a name="to-add-the-ability-to-save-changes-to-sales-records"></a>Die Möglichkeit zum Speichern von Änderungen zu Sales Records hinzufügen  
  
1. Doppelklicken Sie im Designer auf die Schaltfläche **Änderungen speichern**.  
  
     Visual Studio öffnet die CodeBehind-Datei und erstellt einen neuen `saveButton_Click`-Ereignishandler für das <xref:System.Windows.Controls.Primitives.ButtonBase.Click>-Ereignis.  
  
2. Fügen Sie dem `saveButton_Click`-Ereignishandler den folgenden Code hinzu.  
  
     [!code-csharp[Data_WPFWCF#5](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#5)]
     [!code-vb[Data_WPFWCF#5](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#5)]  
  
## <a name="testing-the-application"></a>Testen der Anwendung  
 Erstellen Sie die Anwendung und führen Sie sie aus; prüfen Sie, ob Sie die Kundendatensätze anzeigen und ändern können.  
  
#### <a name="to-test-the-application"></a>So testen Sie die Anwendung  
  
1. Auf **erstellen** Menü klicken Sie auf **Projektmappe**. Überprüfen Sie, ob die Lösung ohne Fehler erstellt wurde.  
  
2. Drücken Sie **STRG + F5**.  
  
     Visual Studio startet das Projekt **AdventureWorksService** ohne es zu debuggen.  
  
3. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt **AdventureWorksSalesEditor**.  
  
4. Klicken Sie im Kontextmenü unter **Debug** auf **Neue Instanz starten**.  
  
     Die Anwendung wird ausführt. Überprüfen Sie Folgendes:  
  
    - Die Textfelder zeigen unterschiedliche Datenfelder aus dem ersten Verkaufsdatensatz an, der die Sales Order ID **71774** vorweist.  
  
    - Sie können auf die Schaltflächen **>** oder **<** für die Navigation durch andere Verkaufsdatensätze klicken.  
  
5. Geben Sie Text in einen der Verkaufsdatensätze im Feld **Comment** ein, und klicken Sie anschließend auf **Änderungen speichern**.  
  
6. Schließen Sie die Anwendung und starten Sie sie dann erneut aus Visual Studio.  
  
7. Navigieren Sie zum Verkaufsdatensatz, den Sie geändert haben und überprüfen Sie, dass die Änderung nach dem Schließen und erneut Öffnen noch vorhanden ist.  
  
8. Schließen Sie die Anwendung.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Nach Abschluss dieser exemplarischen Vorgehensweise können Sie folgende Aufgaben ausführen:  
  
- Erfahren Sie, wie Sie das **Datenquellenfenster** in Visual Studio für die Bindung von WPF-Steuerelementen an andere Typen von Datenquellen verwenden. Weitere Informationen finden Sie unter [Binden von WPF-Steuerelemente zu einem Dataset](../data-tools/bind-wpf-controls-to-a-dataset.md).  
  
- Erfahren Sie, wie Sie das **Datenquellenfenster** in Visual Studio für die Anzeige zugehöriger Daten (das heißt, Daten in einer Beziehung zwischen übergeordneten und untergeordneten Daten) in WPF-Steuerelementen verwenden. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Anzeigen verknüpfter Daten in einer WPF-Anwendung](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Binden von WPF-Steuerelementen an Daten in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [Binden von WPF-Steuerelementen an Daten in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)   
 [Binden von WPF-Steuerelementen zu einem dataset](../data-tools/bind-wpf-controls-to-a-dataset.md)   
 [Übersicht](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)   
 [Übersicht über Entity Framework](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)   
 [WPF und Silverlight-Designer (Übersicht)](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)   
 [Übersicht zur Datenbindung](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)
