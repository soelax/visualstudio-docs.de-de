---
title: /SafeMode („devenv.exe“) | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /SafeMode Devenv switch
- Devenv, /SafeMode switch
- SafeMode switch
ms.assetid: b191f6a5-8f12-47ec-bcc7-b68149a22aa8
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 94e8e87f4440644f76906a70ea09a46282b109c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163365"
---
# <a name="safemode-devenvexe"></a>/SafeMode (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Startet [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] im abgesicherten Modus und lädt nur die Standardumgebung und -dienste  
  
## <a name="syntax"></a>Syntax  
  
```  
devenv /SafeMode   
```  
  
## <a name="remarks"></a>Anmerkungen  
 Dieser Schalter verhindert, dass beim Start von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackages von Drittanbietern geladen werden und stellt dadurch eine stabile Ausführung sicher.  
  
## <a name="description"></a>BESCHREIBUNG  
 Das folgende Beispiel zeigt [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] im abgesicherter Modus.  
  
## <a name="code"></a>Code  
  
```  
Devenv.exe /SafeMode  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Devenv-Befehlszeilenschalter](../../ide/reference/devenv-command-line-switches.md)
