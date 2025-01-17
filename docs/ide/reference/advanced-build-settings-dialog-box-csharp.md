---
title: Dialogfeld "Erweiterte Buildeinstellungen" (C#)
ms.date: 06/20/2017
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 306cecc6bdc194e0022c056ac0a87e2ab063d20b
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461881"
---
# <a name="advanced-build-settings-dialog-box-c"></a>Dialogfeld "Erweiterte Buildeinstellungen" (C#)

Verwenden Sie das Dialogfeld **Erweiterte Buildeinstellungen** des **Projekt-Designers**, um die erweiterten Buildkonfigurationseigenschaften des Projekts anzugeben. Dieses Dialogfeld gilt nur für [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]-Projekte.

## <a name="general"></a>Allgemein

Die folgenden Optionen geben Ihnen die Möglichkeit, allgemeine erweiterte Einstellungen vorzunehmen.

**Sprachversion**

Gibt die Version der zu verwendenden Sprache an. Die Funktionsgruppe ist für jede Version anders, weshalb diese Option dazu verwendet werden kann, den Compiler dazu zu zwingen, nur eine Untergruppe von implementierten Funktionen zu erlauben oder nur die Funktionen zu aktivieren, die mit einem bereits vorhandenen Standard kompatibel sind. Diese Einstellung hat folgende Optionen:

- **default**

   Setzt die aktuellen Version als Ziel.

- **ISO-1** und **ISO-2**

   Als Ziel werden jeweils die Standardfunktionen von ISO-1 und ISO-2 verwendet.

- **C# [Versionsnummer]**

   Als Ziel wird eine bestimmte Version von C# verwendet. Weitere Informationen finden Sie unter [/langversion (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option).

**Bericht für interne Compilerfehler**

Gibt an, ob Compilerfehler an Microsoft gemeldet werden sollen. Wenn **prompt** (Standardeinstellung) eingestellt ist, erhalten Sie eine Aufforderung, wenn ein interner Compilerfehler auftritt, die Ihnen die Option gibt, einen elektronischen Fehlerbericht an Microsoft zu senden. Wenn **send** eingestellt ist, werden Fehlerberichte automatisch gesendet. Wenn **queue** eingestellt ist, werden Fehlerberichte in eine Warteschlange gestellt. Wenn **none** eingestellt ist, wird der Fehler nur in der Eingabe des Compilertexts gemeldet. Weitere Informationen finden Sie unter [/errorreport (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option).

**Auf arithmetischen Über-/Unterlauf überprüfen**

Gibt an, ob ein arithmetischer Ganzzahlauszug, der sich außerhalb des Bereichs der [geprüften](/dotnet/csharp/language-reference/keywords/checked) oder [ungeprüften Schlüsselwörter](/dotnet/csharp/language-reference/keywords/unchecked) befindet und der einen Wert außerhalb des Bereichs des Datentyps nach sich zieht, eine Ausnahme verursacht. Weitere Informationen finden Sie unter [/checked (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option).

**Nicht auf mscorlib.dll verweisen**

Gibt an, ob „mscorlib.dll“ in Ihr Programm importiert wird und damit den gesamten Namespace <xref:System> definiert. Klicken Sie dieses Kästchen an, wenn Sie Ihren eigenen <xref:System>-Namespace und Objekte definieren oder erstellen möchten. Weitere Informationen finden Sie unter [/nostdlib (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option).

## <a name="output"></a>Output

Die folgenden Optionen geben Ihnen die Möglichkeit, erweiterte Ausgabeoptionen anzugeben.

**Debuginformationen**

Gibt den Typ der Debuginformationen an, die vom Compiler generiert werden. Informationen zur Konfiguration der Leistung einer Anwendung beim Debuggen finden Sie unter [Erleichtern des Debuggens für ein Image](/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug). Diese Einstellung hat folgende Optionen:

- **none**

   Gibt an, das keine Debuginformationen generiert werden

- **full**

   Ermöglicht es, einen Debugger an ein ausgeführtes Programm anzufügen.

- **pdbonly**

   Macht ein Debuggen von Quellcode möglich, wenn das Programm im Debugger gestartet wird. Der Assembler wird jedoch nur angezeigt, wenn das aktive Programm an den Debugger angefügt ist.

- **portable** (portabel)

   Erzeugt eine PDB-Datei, d.h. eine nicht plattformspezifische Symboldatei, die anderen Tools, besonders Debuggern, Informationen über die Erstellung und den Inhalt der wichtigsten ausführbaren Datei bereitstellt. Weitere Informationen finden Sie unter [Portable PDB](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md).

- **embedded** (eingebettet)

   Portable Symbolinformationen werden in der Assembly eingebettet. Es wird keine externe PDB-Datei generiert.

Weitere Informationen finden Sie unter [/debug (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option).

**Dateianordnung**

Gibt die Größe der Abschnitte in der Ausgabedatei an. Gültige Werte sind **512**, **1024**, **2048**, **4096** und **8192**. Diese Werte werden in Bytes angegeben. Jeder Abschnitt wird auf einer Grenze angeordnet, die ein Mehrfaches des Werts ist, wodurch die Größe der Ausgabedatei beeinflusst wird. Weitere Informationen finden Sie unter [/filealign (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option).

**Basisadresse der Bibliothek**

Gibt die bevorzugte Basisadresse an, unter der eine DLL geladen werden soll. Die Standard-Basisadresse für eine DLL-Datei wird durch die Common Language Runtime von .NET Framework festgelegt. Weitere Informationen finden Sie unter [/baseaddress (C# Compiler Options)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option).

## <a name="see-also"></a>Siehe auch

- [C#-Compileroptionen](/dotnet/csharp/language-reference/compiler-options/index)
- [Seite „Erstellen“, Projekt-Designer (C#)](../../ide/reference/build-page-project-designer-csharp.md)