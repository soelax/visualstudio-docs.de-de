---
title: Assistentenschnittstelle (IDTWizard) | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7bd4e9a650bee4f5f13f1aeab39a59a1c04a253c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330898"
---
# <a name="wizard-interface-idtwizard"></a>Assistentenschnittstelle (IDTWizard)
Die integrierte Entwicklungsumgebung (IDE) verwendet die <xref:EnvDTE.IDTWizard> Schnittstelle für die Kommunikation mit dem Assistenten. Assistenten müssen diese Schnittstelle implementieren, um in der IDE installiert werden.

 Die <xref:EnvDTE.IDTWizard.Execute%2A> Methode ist die einzige Methode, die zugeordneten der <xref:EnvDTE.IDTWizard> Schnittstelle. Diese Methode implementieren, Assistenten und die IDE Ruft die Methode für die Schnittstelle. Das folgende Beispiel zeigt die Signatur der Methode.

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 Der Startmechanismus ist für beide Plattformen ähnlich der **neues Projekt** und **neues Element hinzufügen** Assistenten. Um zu starten, rufen Sie die <xref:EnvDTE.IDTWizard> in Dteinternal.h definierte Schnittstelle. Der einzige Unterschied ist der Satz von Kontext und den benutzerdefinierten Parametern, die auf die Schnittstelle übergeben werden, wenn die Schnittstelle aufgerufen wird.

 Die folgenden Informationen beschreiben die <xref:EnvDTE.IDTWizard> -Schnittstelle, die Assistenten implementieren müssen, um die Arbeiten in der [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. Die IDE-Aufrufe der <xref:EnvDTE.IDTWizard.Execute%2A> Methode auf und übergeben sie die folgenden Assistenten:

- Das DTE-Objekt

     Das DTE-Objekt ist der Stamm des Automatisierungsmodells.

- Das Handle für Fenster, um das Dialogfeld wie in der Codesegment gezeigt `hwndOwner ([in] long)`.

     Der Assistent verwendet diese `hwndOwner` als übergeordnetes Element für das Dialogfeld des Assistenten.

- Kontextparameter übergeben auf die Schnittstelle als Variante für SAFEARRAY wie gezeigt in das Codesegment `[in] SAFEARRAY (VARIANT)* ContextParams`.

     Kontextparameter enthalten ein Array von Werten, die spezifisch für die Art der Assistent gestartet wird und den aktuellen Status des Projekts. Die IDE übergibt die Kontextparameter, um dem Assistenten. Weitere Informationen finden Sie unter [Kontextparameter](../../extensibility/internals/context-parameters.md).

- Benutzerdefinierte Parameter auf die Schnittstelle als eine Variante für übergeben SAFEARRAY wie gezeigt in das Codesegment `[in] SAFEARRAY (VARIANT)* CustomParams`.

     Benutzerdefinierte Parameter enthalten, ein Array von benutzerdefinierten Parametern. Eine VSZ-Datei übergibt benutzerdefinierte Parameter an die IDE. Die Werte hängen von der `Param=` Anweisungen. Weitere Informationen finden Sie unter [benutzerdefinierte Parameter](../../extensibility/internals/custom-parameters.md).

- Rückgabewerte für die-Schnittstelle

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>Siehe auch
- [Kontextparameter](../../extensibility/internals/context-parameters.md)
- [Benutzerdefinierte Parameter](../../extensibility/internals/custom-parameters.md)
- [Assistenten](../../extensibility/internals/wizards.md)
- [Assistentendatei (VSZ)](../../extensibility/internals/wizard-dot-vsz-file.md)