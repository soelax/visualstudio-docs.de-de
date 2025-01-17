---
title: Befehl „In Dateien ersetzen“ | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.replaceinfiles
helpviewer_keywords:
- Edit.ReplaceInFiles command
- Replace In Files command
- ReplaceInFiles command
ms.assetid: f116066a-4f65-4f2c-94ef-12cbd8cfb598
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8398f07cf6fa6bd2702b2d84ab0d29dcd614ed32
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157803"
---
# <a name="replace-in-files-command"></a>Befehl "In Dateien ersetzen"
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Ersetzt Text in Dateien mit einem Teil der Optionen, die auf der Registerkarte **In Dateien ersetzen** im Fenster **Suchen und Ersetzen** verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
Edit.ReplaceinFiles findwhat replacewith [/all] [/case]  
[/ext:extensions] [/keep] [/lookin:searchpath] [/options] [/regex]  
[/reset] [/stop] [/sub] [/text2] [/wild] [/word]  
```  
  
## <a name="arguments"></a>Argumente  
 `findwhat`  
 Erforderlich. Der Text, für den eine Übereinstimmung ermittelt werden soll.  
  
 `replacewith`  
 Erforderlich. Der Text, durch den der übereinstimmende Text ersetzt werden soll  
  
## <a name="switches"></a>Schalter  
 /all oder /a  
 Optional. Ersetzt den Suchtext bei jedem Vorkommen durch den Ersetzungstext  
  
 /case oder /c  
 Optional. Übereinstimmungen treten nur auf, wenn die groß und klein geschriebenen Zeichen mit den im `findwhat`-Argument angegebenen übereinstimmen.  
  
 /ext: `extensions`  
 Optional. Legt die Dateierweiterungen für die zu suchenden Dateien fest.  
  
 /keep oder /k  
 Optional. Gibt an, dass alle geänderten Dateien geöffnet bleiben  
  
 /lookin: `searchpath`  
 Optional. Das zu durchsuchende Verzeichnis. Wenn der Pfad Leerzeichen enthält, schließen Sie ihn vollständig in Anführungszeichen ein.  
  
 /options oder /t  
 Optional. Zeigt eine Liste der aktuellen Optionseinstellungen für die Suche an und führt keine Suche aus.  
  
 /regex oder /r  
 Optional. Verwendet vordefinierte Sonderzeichen im `findwhat`-Argument als Notationen, die Textmuster anstelle von Literalzeichen darstellen. Eine vollständige Liste von Zeichen für reguläre Ausdrücke finden Sie unter [Reguläre Ausdrücke](../../ide/using-regular-expressions-in-visual-studio.md).  
  
 /reset oder /e  
 Optional. Legt die Suchoptionen wieder auf die Standardeinstellungen fest und führt keine Suche aus.  
  
 /stop  
 Optional. Hält den aktuellen Suchvorgang an, wenn ein solcher ausgeführt wird. „In Dateien ersetzen“ ignoriert alle anderen Argumente, wenn `/stop` angegeben wurde. Um z.B. die aktuelle Ersetzung zu beenden, müssten Sie Folgendes eingeben:  
  
```  
>Edit.ReplaceinFiles /stop  
```  
  
 /sub oder /s  
 Optional. Durchsucht die Unterordner im Verzeichnis, das im Argument /lookin:`searchpath` angegeben wurde.  
  
 /text2 oder /2  
 Optional. Zeigt die Ergebnisse der Ersetzung im Fenster **Suchergebnisse 2** an.  
  
 /wild oder /l  
 Optional. Verwendet vordefinierte Sonderzeichen im `findwhat`-Argument als Notationen, um ein Zeichen oder eine Abfolge von Zeichen darzustellen.  
  
 /word oder /w  
 Optional. Sucht nur nach ganzen Wörtern  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird nach `btnCancel` gesucht. Danach werden alle CLS Dateien durch `btnReset` ersetzt, die sich im Ordner „My Visual Studio Projects“ (Meine Visual Studio-Projekte) befinden, und Informationen zu Ersetzung werden im Fenster **Suchergebnisse: 2** angezeigt.  
  
```  
>Edit.ReplaceinFiles btnCancel btnReset /lookin:"c:/my visual studio projects" /ext:.cls /text2  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Suchen und Ersetzen von Text](../../ide/finding-and-replacing-text.md)   
 [In Dateien ersetzen](../../ide/replace-in-files.md)   
 [Befehlsfenster](../../ide/reference/command-window.md)   
 [Such-/Befehlsfeld](../../ide/find-command-box.md)   
 [Visual Studio-Befehle](../../ide/reference/visual-studio-commands.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
