---
title: Hinzufügen von vertrauenswürdigen Herausgebers auf Clientcomputer für ClickOnce-apps
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- trusted application deployment, Trusted Publishers
ms.assetid: 35fe324c-45a1-4509-b7be-5c18b4b1b4ab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 426096670df1099568cadc2af68ae0ff50ca71e5
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263163"
---
# <a name="how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications"></a>Vorgehensweise: Hinzufügen eines vertrauenswürdigen Herausgebers zu einem Clientcomputer für ClickOnce-Anwendungen
Mit der Bereitstellung einer vertrauenswürdigen Anwendung können Sie Clientcomputer so konfigurieren, dass Ihre [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] -Anwendungen mit einer höheren Vertrauensebene ausgeführt werden ohne den Benutzer dazu aufzufordern. Die folgenden Verfahren zeigen, wie das Befehlszeilentool CertMgr.exe verwendet wird, um das Zertifikat des Herausgebers zum Speicher für vertrauenswürdige Herausgeber auf einem Clientcomputer hinzuzufügen.

 Die von Ihnen verwendeten Befehle weichen leicht davon ab, je nachdem ob die Zertifizierungsstelle, die Ihr Zertifikat herausgegeben hat, Teil eines vertrauenswürdigen Stamms eines Clients ist. Wenn ein Windows-Clientcomputer Teil einer Domäne ist, enthält er in einer Liste Zertifizierungsstellen, die als vertrauenswürdige Stämme gelten. Diese Liste wird normalerweise vom Systemadministrator konfiguriert. Wenn das Zertifikat von einer der vertrauenswürdigen Stämmen oder von einer Zertifizierungsstelle herausgegeben wurde, die mit einer dieser vertrauenswürdigen Stämme verknüpft ist, können Sie das Zertifikat zum vertrauenswürdigen Stammspeicher des Clients hinzufügen. Wenn andererseits das Zertifikat nicht von einem dieser vertrauenswürdigen Stämme ausgestellt wurde, müssen Sie das Zertifikat jeweils dem vertrauenswürdigen Stammspeicher des Clients und dem Speicher des vertrauenswürdigen Herausgebers hinzufügen.

> [!NOTE]
> Sie müssen Zertifikate auf diese Weise jedem Clientcomputer hinzufügen, auf dem Sie eine [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] -Anwendung bereitstellen möchten, die erweiterte Berechtigungen erfordert. Sie können die Zertifikate entweder manuell oder über eine Anwendung hinzufügen, die Sie für Ihre Clients bereitstellen. Sie müssen diese Computer nur einmal konfigurieren. Danach können Sie eine beliebige Anzahl von [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] -Anwendungen signiert mit demselben Zertifikat bereitstellen.

 Sie können ein Zertifikat auch mithilfe der Klasse <xref:System.Security.Cryptography.X509Certificates.X509Store> programmgesteuert zu einem Speicher hinzufügen.

 Einen Überblick über die Bereitstellung vertrauenswürdiger Anwendungen finden Sie unter [Überblick über die Bereitstellung vertrauenswürdiger Anwendungen](../deployment/trusted-application-deployment-overview.md).

### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-the-trusted-root"></a>So fügen Sie ein Zertifikat zum Speicher für vertrauenswürdige Herausgeber unter dem vertrauenswürdigen Stamm hinzu

1. Abrufen eines digitales Zertifikats von einer Zertifizierungsstelle.

2. Exportieren Sie das Zertifikat in das Format „Base64 X.509“ ( *.cer*). Weitere Informationen zu den Zertifikatformaten finden Sie unter [Exportieren eines Zertifikats](http://go.microsoft.com/fwlink/?LinkId=164793).

3. Führen Sie über die Eingabeaufforderung auf Clientcomputern den folgenden Befehl aus:

     **certmgr.exe -add certificate.cer -c -s -r localMachine TrustedPublisher**

### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-a-different-root"></a>So fügen Sie ein Zertifikat zum Speicher für vertrauenswürdige Herausgeber unter einem anderen Stamm hinzu

1. Abrufen eines digitales Zertifikats von einer Zertifizierungsstelle.

2. Exportieren Sie das Zertifikat in das Format „Base64 X.509“ ( *.cer*). Weitere Informationen zu den Zertifikatformaten finden Sie unter [Exportieren eines Zertifikats](http://go.microsoft.com/fwlink/?LinkId=164793).

3. Führen Sie über die Eingabeaufforderung auf Clientcomputern den folgenden Befehl aus:

     **certmgr.exe -add good.cer -c -s -r localMachine Root**

     **certmgr.exe -add good.cer -c -s -r localMachine TrustedPublisher**

## <a name="see-also"></a>Siehe auch
- [Exemplarische Vorgehensweise: Manuelles Bereitstellen einer ClickOnce-Anwendung](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [Secure ClickOnce applications (Sichern von ClickOnce-Anwendungen)](../deployment/securing-clickonce-applications.md)
- [Codezugriffssicherheit für ClickOnce-Anwendungen](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce und Authenticode](../deployment/clickonce-and-authenticode.md)
- [Trusted application deployment overview (Überblick: Bereitstellen vertrauenswürdiger Anwendungen)](../deployment/trusted-application-deployment-overview.md)
- [Vorgehensweise: ClickOnce-Sicherheitseinstellungen aktivieren](../deployment/how-to-enable-clickonce-security-settings.md)
- [Vorgehensweise: Festlegen einer Sicherheitszone für eine ClickOnce-Anwendung](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [Vorgehensweise: Festlegen Sie benutzerdefinierter Berechtigungen für eine ClickOnce-Anwendung](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [Vorgehensweise: Debuggen einer ClickOnce-Anwendung mit eingeschränkten Berechtigungen](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [Vorgehensweise: Hinzufügen eines vertrauenswürdigen Herausgebers auf einen Clientcomputer für ClickOnce-Anwendungen](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [Vorgehensweise: Erneutes Signieren von Anwendungs- und Bereitstellungsmanifesten](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
- [Vorgehensweise: Konfigurieren des Verhaltens der ClickOnce-Eingabeaufforderung zur Vertrauenswürdigkeit](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)