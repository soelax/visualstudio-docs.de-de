---
title: Installieren von Visual Studio 2019 für Mac
description: Anweisungen zum Installieren von Visual Studio 2019 für Mac und zusätzlicher erforderlichen Komponenten für die plattformübergreifende Entwicklung
author: asb3993
ms.author: amburns
ms.date: 04/02/2019
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.openlocfilehash: 2086532f0602b4a2509358cbb6d57178a9a1a0d4
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2019
ms.locfileid: "67691467"
---
# <a name="install-visual-studio-2019-for-mac"></a>Installieren von Visual Studio 2019 für Mac

Installieren Sie Visual Studio 2019 für Mac, indem Sie die folgenden Schritte ausführen, um native, plattformübergreifende .NET-Apps unter macOS entwickeln zu können.

 > [!div class="button"]
 > [Visual Studio für Mac herunterladen](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=navigation+cta&utm_content=download+vsmac2019)

## <a name="requirements"></a>Requirements (Anforderungen)

- Ein Mac mit macOS High Sierra 10.12 oder höher.

Darüber hinaus benötigen Sie zum Erstellen von Xamarin-Apps für iOS oder macOS:

- Xcode 10.0 oder höher. Für gewöhnlich wird die neuste stabile Version empfohlen.
- eine Apple-ID Erstellen Sie eine kostenlose Apple-ID unter https://appleid.apple.com, wenn Sie noch keine besitzen. Dies ist für die Installation von und die Anmeldung bei Xcode erforderlich.

## <a name="installation-instructions"></a>Installationsanweisungen

1. Laden Sie das Installationsprogramm von der [Seite „Visual Studio für Mac“](https://aka.ms/vsmac) herunter.
2. Klicken Sie nach Abschluss des Downloads auf **VisualStudioforMacInstaller.dmg**, um den Installer einzubinden. Führen Sie ihn anschließend durch Doppelklicken auf das Pfeillogo aus:

    [![Auf großen Pfeil klicken, um die Installation zu starten](media/install-installer-sml.png)](media/install-installer.png#lightbox)

3. Möglicherweise wird Ihnen eine Warnmeldung angezeigt, in der Sie darauf hingewiesen werden, dass die Anwendung aus dem Internet heruntergeladen wird. Klicken Sie auf **Öffnen**.
4. Warten Sie, während das Installationsprogramm Ihr System überprüft:

    [![Das Installationsprogramm überprüft Ihr System auf installierte Komponenten](media/install-checking-sml.png)](media/install-checking.png#lightbox)

5. Ihnen wird eine Warnmeldung angezeigt, in der Sie dazu aufgefordert werden, die Datenschutz- und Lizenzbedingungen zu akzeptieren. Klicken Sie zum Lesen der Bedingungen auf die Links, und klicken Sie auf **Weiter**, wenn Sie die Bedingungen akzeptieren:

    [![Klicken Sie auf die Links zu den Datenschutz- und Lizenzbedingungen, und fahren Sie fort, wenn Sie diese akzeptieren](media/install-privacy-sml.png)](media/install-privacy.png#lightbox)

6. Die Liste der verfügbaren Workloads wird angezeigt. Wählen Sie die Komponenten aus, die Sie verwenden möchten:

    [![Wählen Sie aus, welche optionalen Workload-Features Sie gerne installieren würden](media/install-selection.png)](media/install-selection.png#lightbox)

   Wenn Sie nicht alle Plattformen installieren möchten, lesen Sie den nachfolgenden Leitfaden, um die zu installierenden Plattformen festzulegen:

   * **Apps mit Xamarin**:
      - Xamarin.Forms: Wählen Sie die Plattformen **Android** und **iOS** aus.
      - Nur iOS: Wählen Sie die **iOS**-Plattform aus. (Hinweis: Sie müssen [**Xcode**](https://developer.apple.com/xcode/) installieren.)
      - Nur Android: Wählen Sie die **Android**-Plattform aus. (Hinweis: Sie sollten darüber hinaus die entsprechenden Abhängigkeiten auswählen.)
      - Nur Mac: Wählen Sie die **macOS**-Plattform aus. (Hinweis: Sie müssen [**Xcode**](https://developer.apple.com/xcode/) installieren.)
      - Vollständig plattformübergreifende Xamarin-Apps: Wählen Sie die Plattformen **Android**, **iOS** und **macOS** aus.
   * **.NET Core-Anwendungen**: Wählen Sie die **.NET Core**-Plattform aus.
   * **ASP.NET Core-Webanwendungen**: Wählen Sie die **.NET Core**-Plattform aus.
   * **Entwicklung von plattformübergreifenden Unity-Spielen**: Neben Visual Studio für Mac müssen keine zusätzlichen Plattformen installiert werden. Weitere Informationen zur Installation der Unity-Erweiterung finden Sie im [Leitfaden zur Einrichtung von Unity](/visualstudio/mac/setup-vsmac-tools-unity).

7. Klicken Sie auf die Schaltfläche **Installieren**, nachdem Sie Ihre Auswahl getroffen haben.
8. Das Installationsprogramm zeigt während des Downloads den Fortschritt an und installiert Visual Studio für Mac sowie die ausgewählten Workloads. Möglicherweise werden Sie dazu aufgefordert, Ihr Kennwort einzugeben, um die für die Installation erforderlichen Berechtigungen zu erteilen.

Wenn während der Installation in einer Unternehmensumgebung Netzwerkprobleme auftreten, lesen Sie die Anweisungen unter [Installation hinter einer Firewall oder einem Proxy](https://docs.microsoft.com/visualstudio/mac/installation#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server).

Informationen zu den Änderungen in den [Versionshinweisen](https://docs.microsoft.com/visualstudio/releasenotes/vs2019-mac-relnotes).

> [!NOTE]
> Wenn Sie sich während der ursprünglichen Installation gegen die Installation einer Plattform oder eines Tools entschieden haben (indem Sie die Auswahl in Schritt 6 aufgehoben haben), müssen Sie den Installer erneut ausführen, wenn Sie die Komponenten später hinzufügen möchten.

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Installieren von Visual Studio für Mac hinter einer Firewall oder einem Proxyserver

Für die Installation von Visual Studio für Mac hinter einer Firewall müssen bestimmte Endpunkte zugänglich gemacht werden, um die Downloads der erforderlichen Tools und Updates für Ihre Software zuzulassen.

Konfigurieren Sie Ihr Netzwerk, damit der Zugriff auf die folgenden Speicherorte gewährt wird:

- [Visual Studio-Endpunkte](/visualstudio/install/install-visual-studio-behind-a-firewall-or-proxy-server)

## <a name="next-steps"></a>Nächste Schritte

Die Installation von Visual Studio für Mac ermöglicht Ihnen das Schreiben von Code für Ihre Apps. Hinsichtlich der nächsten Schritte zum Schreiben und Bereitstellen von Projekten werden folgende Leitfäden bereitgestellt:

### <a name="ios"></a>iOS

1. [Hello, iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/)
2. [Device Provisioning](https://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning) (Gerätebereitstellung) (zum Ausführen Ihrer Anwendung auf dem Gerät)

### <a name="android"></a>Android

1. [Using the Xamarin Android SDK Manager (Verwenden des Xamarin.Android SDK-Managers)](https://developer.xamarin.com/guides/android/getting_started/installation/android-sdk/?ide=xs)
2. [Android SDK-Emulator](https://developer.xamarin.com/guides/android/getting_started/installation/android-emulator/)
4. [Set Up Device for Development (Einrichten eines Geräts für die Entwicklung)](https://developer.xamarin.com/guides/android/getting_started/installation/set_up_device_for_development/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>Entwicklung von .NET Core-Apps, ASP.NET Core-Web-Apps und Unity-Spielen

Informationen zu anderen Workloads finden Sie auf der Seite zu den [Workloads](workloads.md).

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>Siehe auch

- [Deinstallieren von Visual Studio (unter Windows)](/visualstudio/install/install-visual-studio)
