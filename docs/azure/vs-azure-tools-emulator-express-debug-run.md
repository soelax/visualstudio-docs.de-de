---
title: Emulator Express zum Ausführen/Debuggen eines Azure-Clouddiensts auf einem lokalen Computer
description: Verwenden von Emulator Express zum Ausführen und Debuggen eines Clouddiensts auf einem lokalen Computer
author: mikejo5000
manager: jillfra
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/06/2017
ms.author: mikejo
ms.openlocfilehash: 86ec00f5fdd80f4c42fdaf1d7c5c44e6008983de
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260674"
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Verwenden von Emulator Express zum Ausführen und Debuggen eines Azure-Clouddiensts auf einem lokalen Computer
Mithilfe von Emulator Express können Sie einen Clouddienst testen und debuggen, ohne Visual Studio als Administrator auszuführen. Abhängig von den Anforderungen Ihres Clouddiensts können Sie die Projekteinstellungen für die Verwendung von Emulator Express oder des vollständigen Emulators festlegen. Weitere Informationen zum vollständigen Emulator finden Sie unter [Ausführen einer Azure-Anwendung im Serveremulator](/azure/storage/common/storage-use-emulator).

## <a name="using-emulator-express-in-visual-studio"></a>Verwenden von Emulator Express in Visual Studio
Wenn Sie ein Azure-Projekt in Azure SDK 2.3 oder höher erstellen, wird Emulator Express automatisch verwendet. Für vorhandene Projekte, die mit einer früheren Version des Azure SDK erstellt wurden, führen Sie die folgenden Schritte aus, um Emulator Express auszuwählen:

1. Erstellen oder öffnen Sie ein Azure-Clouddienstprojekt in Visual Studio.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie im Kontextmenü die Option **Eigenschaften** aus.

1. Wählen Sie auf den Eigenschaftenseiten die Registerkarte **Web** aus.

    ![Eigenschaften für ein Azure-Clouddienstprojekt](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Wählen Sie unter **Lokaler Bereitstellungsserver** die Option **IIS Express verwenden** aus.

1. Wählen Sie unter **Emulator** die Option **Emulator Express verwenden** aus.

1. Um Emulator Express zu starten, führen Sie den folgenden Befehl an einer Eingabeaufforderung aus:

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Emulator Express-Einschränkungen
Die folgenden Probleme sind bekannte Einschränkungen von Emulator Express:

- Emulator Express ist nicht mit IIS-Webservern kompatibel.
- Der Clouddienst kann mehrere Rollen enthalten, dabei ist jedoch jede Rolle auf eine Instanz beschränkt.
- Der Zugriff auf Portnummern unterhalb von 1000 ist nicht möglich. Wenn Sie einen Authentifizierungsanbieter verwenden, der üblicherweise einen Port unter 1000 verwendet, müssen Sie diesen Wert u.U. in eine Portnummer über 1000 ändern.
- Einschränkungen, die auf den Azure-Compute-Emulator zutreffen, gelten auch für Emulator Express. Sie können z. B. nicht mehr als 50 Rolleninstanzen pro Bereitstellung verwenden. Weitere Informationen zum Azure-Serveremulator finden Sie unter [Ausführen einer Azure-Anwendung im Serveremulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Nächste Schritte
[Debuggen von Azure-Clouddiensten](vs-azure-tools-debugging-cloud-services-overview.md)
