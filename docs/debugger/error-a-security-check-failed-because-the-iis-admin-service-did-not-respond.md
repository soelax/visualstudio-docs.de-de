---
title: 'Fehler: Eine Sicherheitsprüfung ist fehlgeschlagen, weil der IIS-Verwaltungsdienst nicht reagiert hat | Microsoft-Dokumentation'
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.iis_not_responding
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ae97ae0594b06e9b35ac3bdd61eacf852968889
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851033"
---
# <a name="error-a-security-check-failed-because-the-iis-admin-service-did-not-respond"></a>Fehler: Fehler bei einer Sicherheitsüberprüfung, weil der IIS-Verwaltungsdienst nicht reagiert hat
Dieser Fehler tritt auf, wenn der IIS-Verwaltungsdienst nicht reagiert. Normalerweise weist dies auf ein Problem mit der IIS-Installation hin. Stellen Sie zunächst in der **Verwaltung** unter **Dienste** sicher, dass der Dienst ausgeführt wird.

### <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler

- Installieren Sie IIS mithilfe der Option **Software** in der Systemsteuerung neu.

- - oder - 

- IIS in der Systemsteuerung mithilfe der Einstellungen „Software“ vom Computer entfernen. Wenn Sie IIS entfernt haben und die Probleme weiterhin auftreten, vergewissern Sie sich in der Registrierung, dass der folgende Schlüssel nicht mehr existiert:

    `HKEY_CLASSES_ROOT\CLSID\{A9E69610-B80D-11D0-B9B9-00A0C922E750}`

     - oder - 

- Deaktivieren Sie den IIS-Verwaltungsdienst in der Systemsteuerung über die Option Verwaltung. Dadurch wird IIS auf dem Computer deaktiviert.

     Sie müssen den Computer nach jedem dieser drei Schritte neu starten.

     Weitere Informationen finden Sie in der IIS-Dokumentation.

## <a name="see-also"></a>Siehe auch
- [Debuggen von Webanwendungen: Fehler und Problembehandlung](../debugger/debugging-web-applications-errors-and-troubleshooting.md)