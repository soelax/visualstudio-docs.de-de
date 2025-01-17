---
title: Seite „Anwendung“ der C#-Projekteigenschaften
ms.date: 10/30/2018
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesApplicationWPF
- cs.ProjectPropertiesApplication
helpviewer_keywords:
- Project Designer, Application page
- Application page in Project Designer
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 897c3a82f5add84ad343c100b93fd8a4d2663610
ms.sourcegitcommit: d4920babfc3d24a3fe1d4bf446ed3fe73b344467
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "67160056"
---
# <a name="application-page-project-designer-c"></a>Seite "Anwendung", Projekt-Designer (C#)

Legen Sie auf der Seite **Anwendung** des **Projekt-Designers** die Anwendungseinstellungen und -eigenschaften des Projekts fest.

Um auf die Seite **Anwendung** zuzugreifen, wählen Sie im **Projektmappen-Explorer** einen Projektknoten (nicht den Knoten **Projektmappen** aus. Wählen Sie dann in der Menüleiste **Projekt** > **Eigenschaften** aus. Wenn der **Projekt-Designer** angezeigt wird, klicken Sie auf die Registerkarte **Anwendung**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="general-application-settings"></a>Allgemeine Anwendungseinstellungen

Mit den folgenden Optionen können Sie allgemeine Einstellungen für die Anwendung konfigurieren.

**Assemblyname**

Gibt den Namen der Ausgabedatei an, in der das Assemblymanifest enthalten ist. Durch Ändern dieser Eigenschaft wird auch die Eigenschaft **Ausgabename** geändert.

Sie können diese Änderung auch mithilfe von [/out (C#-Compileroptionen)](/dotnet/csharp/language-reference/compiler-options/out-compiler-option) in der Befehlszeile vornehmen.

Informationen zum programmgesteuerten Zugriff auf diese Eigenschaft finden Sie unter <xref:VSLangProj.ProjectProperties.AssemblyName%2A>.

**Standardnamespace**

Legt den Basisnamespace für alle Dateien fest, die dem Projekt hinzugefügt werden.

Weitere Informationen zum Erstellen von Namespaces im Code finden Sie unter [Namespace](/dotnet/csharp/language-reference/keywords/namespace).

Informationen zum programmgesteuerten Zugriff auf diese Eigenschaft finden Sie unter <xref:VSLangProj.ProjectProperties.RootNamespace%2A>.

**Zielframework**

Gibt die .NET-Version an, auf die die Anwendung ausgerichtet ist. Diese Option kann unterschiedliche Werte aufweisen, je nachdem, welche Versionen von .NET auf Ihrem Computer installiert sind.

Für .NET Framework-Projekte entspricht der Standardwert dem Zielframework, das Sie beim Erstellen des Projekts angegeben haben.

Für ein Projekt, das auf .NET Core abzielt, werden die verfügbaren Versionen ggf. wie folgt aussehen:

![Framework-Zielversionen für ein .NET Core-Projekt](../media/application-target-framework.png)

> [!NOTE]
> Die im Dialogfeld [Erforderliche Komponenten](../../ide/reference/prerequisites-dialog-box.md) aufgelisteten Pakete mit erforderlichen Komponenten werden automatisch festgelegt, wenn Sie das Dialogfeld zum ersten Mal öffnen. Wenn im Nachhinein Änderungen am Zielframework des Projekts vorgenommen werden, müssen Sie die erforderlichen Komponenten entsprechend dem neuen Zielframework manuell auswählen.

Weitere Informationen finden Sie unter [Übersicht über Frameworkziele](../../ide/visual-studio-multi-targeting-overview.md).

**Ausgabetyp**

Gibt den Typ der zu erstellenden Anwendung an. Die Werte unterscheiden sich je nach Projekttyp. Für ein **Konsolenanwendungsprojekt** können Sie zum Beispiel **Windows-Anwendung**, **Konsolenanwendung** oder **Klassenbibliothek** als Ausgabetyp angeben.

Für ein Webanwendungsprojekt müssen Sie **-Klassenbibliothek** angeben.

Weitere Informationen über die Eigenschaft **Ausgabetyp** finden Sie unter [/target (C#-Compileroptionen)](/dotnet/csharp/language-reference/compiler-options/target-compiler-option).

Informationen zum programmgesteuerten Zugreifen auf diese Eigenschaft finden Sie unter <xref:VSLangProj.ProjectProperties.OutputType%2A>.

**Bindungsumleitungen automatisch generieren**

Bindungsumleitungen werden zu Ihrem Projekt hinzugefügt, wenn Ihre App oder die zugehörigen Komponenten auf mehrere Versionen derselben Assembly verweisen. Wenn Sie Bindungsumleitungen manuell in der Projektdatei definieren möchten, deaktivieren Sie **Bindungsumleitungen automatisch generieren**.

Weitere Informationen zur Umleitung finden Sie unter [Umleiten von Assemblyversionen](/dotnet/framework/configure-apps/redirect-assembly-versions).

**Startobjekt**

Definiert den Einstiegspunkt, der aufgerufen werden soll, wenn die Anwendung geladen wird. Dieser wird üblicherweise entweder auf das Hauptformular der Anwendung oder auf die `Main`-Prozedur festgelegt, die beim Start der Anwendung ausgeführt werden soll. Da Klassenbibliotheken über keinen Einstiegspunkt verfügen, ist ihre einzige Option für diese Eigenschaft **(Nicht festgelegt)** .

In einem WPF-App-Projekt ist diese Option standardmäßig festgelegt auf **(Nicht festgelegt)** . Die andere Option ist \[projectname].App. Bei einem WPF-Projekt müssen Sie den Start-URI so einstellen, dass beim Starten der Anwendung eine UI-Ressource geladen wird. Öffnen Sie hierfür im Projekt die Datei *Application.xaml*, und legen Sie die `StartupUri`-Eigenschaft auf eine *XAML*-Datei in Ihrem Projekt fest, beispielsweise *Window1.xaml*. Eine Liste der zulässigen Stammelemente finden Sie unter <xref:System.Windows.Application.StartupUri%2A>. In einer Klasse im Projekt müssen Sie auch eine `public static void Main()`-Methode definieren. Diese Klasse wird in der **Startobjekt**-Liste als *ProjectName.ClassName* angezeigt. Sie können dann die Klasse als Startobjekt auswählen.

Weitere Informationen hierzu finden Sie unter [/main (C#-Compileroptionen)](/dotnet/csharp/language-reference/compiler-options/main-compiler-option). Informationen zum programmgesteuerten Zugriff auf diese Eigenschaft finden Sie unter <xref:VSLangProj.ProjectProperties.StartupObject%2A>.

**Assemblyinformationen**

Durch Klicken auf diese Schaltfläche wird das Dialogfeld [Assemblyinformationen](../../ide/reference/assembly-information-dialog-box.md) geöffnet.

## <a name="resources"></a>Ressourcen

Mit den **Ressourcen**-Optionen können Sie die Ressourceneinstellungen für Ihre App konfigurieren.

**Symbol und Manifest**

Standardmäßig ist dieses Optionsfeld markiert, und die Optionen **Symbol** und **Manifest** sind aktiviert. Dadurch können Sie Ihr eigenes Symbol oder andere Optionen zur Generierung von Manifesten auswählen. Lassen Sie dieses Optionsfeld ausgewählt, es sei denn, Sie stellen eine Ressourcendatei für das Projekt bereit.

**Symbol**

Legt die *ICO*-Datei fest, die als Programmsymbol verwendet werden soll. Klicken Sie auf **Durchsuchen**, um eine vorhandene Grafik zu suchen, oder geben Sie den Namen der gewünschten Datei ein. Weitere Informationen finden Sie unter [/win32icon (C#-Compileroptionen)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option).

Informationen zum programmgesteuerten Zugriff auf diese Eigenschaft finden Sie unter <xref:VSLangProj.ProjectProperties.ApplicationIcon%2A>.

**Manifest**

Aktiviert eine Manifestgenerierungsoption, wenn die Anwendung auf Windows Vista unter Benutzerkontensteuerung (UAC) ausgeführt wird. Diese Option kann die folgenden Werte aufweisen:

- **Manifest mit Standardeinstellungen einbetten**. Unterstützt die normale Vorgehensweise von Visual Studio unter Windows Vista, bei der durch Einbetten der Sicherheitsinformationen in die ausführbare Datei der Anwendung angegeben wird, dass `requestedExecutionLevel` `AsInvoker` sein soll. Dies ist die Standardoption.

- **Anwendung ohne Manifest erstellen**. Diese Methode wird auch als *Virtualisierung* bezeichnet. Verwenden Sie diese Option, wenn Kompatibilität mit früheren Anwendungen erforderlich ist.

- **Properties\app.manifest**. Diese Option ist für Anwendungen erforderlich, die über ClickOnce oder COM ohne Registrierung bereitgestellt wurden. Wenn Sie eine Anwendung über ClickOnce-Bereitstellung veröffentlichen, wird **Manifest** automatisch auf diese Option festgelegt.

**Ressourcendatei**

Wählen Sie dieses Optionsfeld aus, wenn Sie eine Ressourcendatei für das Projekt bereitstellen. Durch Auswahl dieser Option, werden die Optionen **Symbol** und **Manifest** deaktiviert.

Geben Sie einen Pfadnamen ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen ( **...** ), um dem Projekt eine Win32-Ressourcendatei hinzuzufügen.