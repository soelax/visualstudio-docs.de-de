---
title: 'Vorgehensweise: Einschließen von erforderlichen Komponenten mit einer ClickOnce-Anwendung | Microsoft-Dokumentation'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c66bf0a5-8c93-4e68-a224-3b29ac36fe4d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47142e63976a743166e5211631e77a0c0878ad9c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406966"
---
# <a name="how-to-include-prerequisites-with-a-clickonce-application"></a>Vorgehensweise: Einschließen erforderlicher Komponenten in eine ClickOnce-Anwendung
Bevor Sie die erforderliche Software mit einer [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]-Anwendung verteilen können, müssen Sie zunächst die Installationspakete für diese erforderlichen Komponenten auf Ihren Entwicklungscomputer herunterladen. Wenn Sie eine Anwendung veröffentlichen und **Erforderliche Komponenten von demselben Speicherort wie Anwendung herunterladen** auswählen, tritt ein Fehler auf, wenn die Installationspakete nicht im Ordner **Pakete** enthalten sind.

> [!NOTE]
> Zum Hinzufügen eines Installationspakets für .NET Framework finden Sie unter [Handbuch für die Bereitstellung von .NET Framework für Entwickler](/dotnet/framework/deployment/deployment-guide-for-developers).

## <a name="Package"></a> So fügen Sie mit „Package.xml“ ein Installationspaket hinzu

1. Öffnen Sie im Datei-Explorer den Ordner **Pakete**.

    Standardmäßig ist der Pfad `%ProgramFiles(x86)%\Microsoft SDKs\ClickOnce Bootstrapper\Packages\`.

2. Öffnen Sie den Ordner für die erforderliche Komponente, die Sie hinzufügen möchten, und öffnen Sie dann den Sprachordner für die installierte Version von [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (z.B. **en** für Englisch).

3. Öffnen Sie im Editor die Datei *Package.xml*.

4. Suchen Sie die **Namen** -Element mit **http://go.microsoft.com/fwlink** , und kopieren Sie die URL. Schließen Sie die **LinkID**-Komponente ein.

   > [!NOTE]
   > Wenn kein **Namen** Element enthält **http://go.microsoft.com/fwlink** öffnen die **Product.xml** Datei im Stammordner für die erforderliche Komponente, und suchen Sie die **Fwlink** Zeichenfolge.

   > [!IMPORTANT]
   > Einige erforderliche Komponenten haben mehrere Installationspakete (z. B. für 32-Bit- oder 64-Bit-Systeme). Wenn mehrere **Name**-Elemente **fwlink** enthalten, müssen Sie die verbleibenden Schritte für jedes dieser Elemente überprüfen.

5. Fügen Sie die URL in die Adressleiste des Browsers ein, und wählen Sie dann, wenn Sie zum Ausführen oder Speichern aufgefordert werden, **Speichern** aus.

    In diesem Schritt wird die Installationsdatei auf den Computer heruntergeladen.

6. Kopieren Sie die Datei in den Stammordner für die erforderliche Komponente.

    Für die erforderliche Komponente von Windows Installer 4.5 kopieren Sie z.B. die Datei in den Ordner *\Packages\WindowsInstaller4_5*.

    Sie können das Installationspaket jetzt mit der Anwendung verteilen.

## <a name="see-also"></a>Siehe auch
- [Vorgehensweise: Installieren von Voraussetzungen mit einer ClickOnce-Anwendung](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
