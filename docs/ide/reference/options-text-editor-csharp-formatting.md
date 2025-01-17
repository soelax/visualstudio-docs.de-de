---
title: C# -Editor-Formatierungsoptionen
ms.date: 08/14/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.NewLines
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Indentation
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Wrapping
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.Code_Style.Formatting.General
helpviewer_keywords:
- formatting options [C#]
- Text editor Options dialog box, formatting
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b555ede6ecf406f98c2e1ae9384b61664e8226cf
ms.sourcegitcommit: b468d71052a1b8a697f477ab23a3644de139f1e9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2019
ms.locfileid: "67260407"
---
# <a name="options-dialog-box-text-editor--c--code-style--formatting"></a>Dialogfeld „Optionen“: Text-Editor \> C# \> Codeformat \> Formatierung

Legen Sie auf der Seite **Formatierungsoptionen** und deren untergeordneten Seiten ([**Einzug**](#indentation-page), **Neue Zeilen**, **Abstand**, **Umbruch**) die Optionen zum Formatieren von Code im Code-Editor fest.

Wählen Sie in der Menüleiste **Tools** > **Optionen** um diese Optionsseite aufzurufen. Klicken Sie im Dialogfeld **Optionen** auf **Text-Editor** > **C#**  > **Codeformat** > **Formatierung**.

> [!TIP]
> Auf den Unterseiten **Einzug**, **Neue Zeilen**, **Abstand** und **Umbruch** wird jeweils ein Vorschaufenster im unteren Bereich angezeigt, auf dem Sie die Auswirkungen der jeweiligen Option prüfen können. Wählen Sie zur Verwendung des Vorschaufensters eine Formatierungsoption aus. Im Vorschaufenster wird ein Beispiel der ausgewählten Option angezeigt. Wenn Sie eine Einstellung ändern, indem Sie z.B. ein Optionsfeld oder ein Kontrollkästchen aktivieren oder deaktivieren, wird das Vorschaufenster in Anpassung an diese neue Einstellung aktualisiert.

## <a name="formatting-general-page"></a>Seite „Formatierung“ (Allgemein)

### <a name="general-settings"></a>Allgemeine Einstellungen

Es hängt von den Einstellungen ab, *wann* Formatierungsoptionen für den Code vom Code-Editor übernommen werden.

|Bezeichnung|BESCHREIBUNG|
|-----------|-----------------|
|**Automatisch während der Eingabe formatieren**|Wenn diese Bezeichnung deaktiviert ist, sind auch die Optionen **Beim Eingeben von ; Anweisung formatieren** und **Bei Eingabe von } Block formatieren** deaktiviert.|
|**Bei Eingabe von ; Anweisung automatisch formatieren**|Bei Auswahl dieser Option werden Anweisungen nach der Fertigstellung entsprechend den für den Editor ausgewählten Formatierungsoptionen formatiert.|
|**Bei Eingabe von } Block automatisch formatieren**|Bei Auswahl dieser Option werden Codeblöcke entsprechend den für den Editor ausgewählten Formatierungsoptionen formatiert, sobald der Codeblock abgeschlossen ist.|
|**Bei Verwendung der EINGABETASTE automatisch formatieren**|Bei Auswahl dieser Option wird Text formatiert, wenn Sie die **EINGABETASTE** drücken, damit dieser den für den Editor aktivierten Formatierungsoptionen entspricht.|
|**Beim Einfügen automatisch formatieren**|Bei Auswahl dieser Option wird in den Editor eingefügter Text entsprechend den für den Editor ausgewählten Formatierungsoptionen formatiert.|

::: moniker range="vs-2019"

Wenn Sie Codeformateinstellungen für C#-Dateien bisher mit dem Befehl **Dokument formatieren** in Visual Studio 2017 angewendet haben, finden Sie diese Funktion jetzt unter [**Codebereinigung**](../code-styles-and-code-cleanup.md#apply-code-styles).

::: moniker-end

::: moniker range="vs-2017"

### <a name="format-document-settings"></a>Einstellungen für Befehl „Dokument formatieren“

Mit den folgenden Einstellungen wird der Befehl **Dokument formatieren** so konfiguriert, dass zusätzliche Bereinigungsvorgänge für eine Datei ausgeführt werden. Weitere Informationen darüber, wie diese Einstellungen übernommen werden, finden Sie unter [Befehl „Dokument formatieren“](../code-styles-and-code-cleanup.md#apply-code-styles).

|Bezeichnung|BESCHREIBUNG|Entsprechende EditorConfig-Optionen und Regeln unter „Extras“ > „Optionen“|
|-----------|-----------------|-----------------|-----------------|
|**Alle C#-Formatierungsregeln anwenden (Einzug, Umbruch, Abstände)**|Durch den Befehl **Dokument formatieren** werden alle Formatierungsprobleme behoben. Diese Einstellung kann nicht angepasst werden.| [Grundlegende EditorConfig-Optionen](../../ide/create-portable-custom-editor-options.md)<br/>[.NET EditorConfig-Formatierungsoptionen](../../ide/editorconfig-formatting-conventions.md)<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Formatierung** > [**Einzug**, **Neue Zeilen**, **Abstand** oder **Umbruch**]|
|**Zusätzliche Codebereinigung während der Formatierung durchführen**|Bei Auswahl dieser Option werden die Korrekturen angewendet, die in den Regeln für den **Edit.FormatDocument**-Befehl angegeben wurden.| Nicht zutreffend |
|**Remove unnecessary usings** (Nicht erforderliche using-Anweisungen entfernen)|Bei Auswahl dieser Option werden unnötige `using`-Anweisungen entfernt, sobald **Edit.FormatDocument** ausgelöst wird.| Nicht zutreffend |
|**Sort usings** (using-Anweisungen sortieren)|Bei Auswahl dieser Option werden `using`-Anweisungen sortiert, sobald **Edit.FormatDocument** ausgelöst wird.| dotnet_sort_system_directives_first<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Erweitert** > **Place 'System' directives first when sorting usings („System“-Anweisungen beim Sortieren von using-Anweisungen oben anzeigen)** |
|**Geschweifte Klammern für einzeilige Steuerungsanweisungen hinzufügen/entfernen**|Bei Auswahl dieser Option werden einzeiligen Steuerungsanweisungen geschweifte Klammern hinzugefügt bzw. aus diesen entfernt, sobald **Edit.FormatDocument** ausgelöst wird.| csharp_prefer_braces<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Codeblockeinstellungen** > **Geschweifte Klammern bevorzugen** |
|**Zugriffsmodifizierer hinzufügen**|Bei Auswahl dieser Option werden Zugriffsmodifizierer hinzugefügt, sobald **Edit.FormatDocument** ausgelöst wird.| dotnet_style_require_accessibility_modifiers |
|**Zugriffsmodifizierer sortieren**|Bei Auswahl dieser Option werden Zugriffsmodifizierer sortiert, sobald **Edit.FormatDocument** ausgelöst wird.| csharp_preferred_modifier_order<br/>visual_basic_preferred_modifier_order |
|**Ausdrucks-/Blocktexteinstellungen anwenden**|Bei Auswahl dieser Option werden Ausdruckskörpermember in Blocktexte konvertiert (oder die umgekehrte Aktion wird ausgeführt), sobald **Edit.FormatDocument** ausgelöst wird.| [EditorConfig-Optionen für Ausdruckskörpermember](../../ide/editorconfig-language-conventions.md#expression-bodied-members)<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Ausdruckseinstellungen** > **Use expression body for methods, constructors, etc. (Ausdruckskörper für Methoden, Konstruktoren usw. verwenden)** |
|**Apply implicit/explicit type preferences** (Einstellungen für implizite/explizite Typen anwenden)|Bei Auswahl dieser Option wird `var` in den expliziten Typ konvertiert (oder die umgekehrte Aktion wird ausgeführt), sobald **Edit.FormatDocument** ausgelöst wird.| [EditorConfig-Optionen für explizite Typen](../../ide/editorconfig-language-conventions.md#implicit-and-explicit-types)<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **var-Einstellungen** |
|**Einstellungen für out-Inlinevariablen anwenden**|Bei Auswahl dieser Option werden `out`-Inlinevariablen nach Möglichkeit verwendet, sobald **Edit.FormatDocument** ausgelöst wird.| csharp_style_inlined_variable_declaration<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Variableneinstellungen** > **Inlinevariablendeklaration vorziehen** |
|**Typeinstellungen für Sprache/Framework anwenden**|Bei Auswahl dieser Option werden Sprachtypen in Frameworktypen konvertiert (oder die umgekehrte Aktion wird ausgeführt), sobald **Edit.FormatDocument** ausgelöst wird.| dotnet_style_predefined_type_for_locals_parameters_members<br/>dotnet_style_predefined_type_for_member_access<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Vordefinierte Typeinstellungen** |
|**Einstellungen für Objekt-/Sammlungsinitialisierung anwenden**|Bei Auswahl dieser werden nach Möglichkeit Objekt- und Elementinitialisierer verwendet, sobald **Edit.FormatDocument** ausgelöst wird.| dotnet_style_object_initializer<br/>dotnet_style_collection_initializer<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Ausdruckseinstellungen** > **Objektinitialisierer vorziehen** oder **Prefer collection initializer** (Elementinitialisierer vorziehen) |
|**this.-Qualifizierungseinstellungen anwenden**|Bei Auswahl dieser Option werden die `this.`-Einstellungen angewendet, sobald **Edit.FormatDocument** ausgelöst wird.| [EditorConfig-Optionen für this.-Qualifizierung](../../ide/editorconfig-language-conventions.md#this-and-me)<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **this.-Einstellungen** |
|**Private Felder nach Möglichkeit als schreibgeschützt festlegen**|Bei Auswahl dieser Option wird für private Felder nach Möglichkeit `readonly` festgelegt, sobald **Edit.FormatDocument** ausgelöst wird.| dotnet_style_readonly_field<br/><br/>**Extras** > **Optionen** > **Text-Editor** > **C#**  > **Codeformat** > **Voreinstellungen für Feld** > **Readonly bevorzugen** |
|**Unnötige Umwandlungen entfernen**|Bei Auswahl dieser Option werden nach Möglichkeit unnötige Umwandlungen entfernt, sobald **Edit.FormatDocument** ausgelöst wird.| Nicht zutreffend |
|**Nicht verwendete Variablen entfernen**|Bei Auswahl dieser Option werden nicht verwendete Variablen entfernt, sobald **Edit.FormatDocument** ausgelöst wird.| Nicht zutreffend |

![Codebereinigungseinstellungen für C# in Visual Studio](media/format-document-settings.png)

::: moniker-end

## <a name="indentation-page"></a>Seite „Einzug“

Die Einzugsoptionen auf dieser Seite werden angewendet, wenn Code automatisch formatiert wird. Code wird beispielsweise automatisch formatiert, wenn Sie Code in die Datei einfügen und die Option **Beim Einfügen automatisch formatieren** ausgewählt ist. (Die Option **Beim Einfügen automatisch formatieren** finden Sie unter **Formatierung** > **Allgemein**.)

![C#-Text-Editor-Einzugsoptionen in Visual Studio](media/csharp-indentation-options.png)

> [!TIP]
> Einzugsoptionen finden Sie zudem auf der Optionsseite **Text-Editor** > **C#**  > **Registerkarten**. Durch die Optionen wird lediglich festgelegt, an welche Position der Cursor im Code-Editor gesetzt wird, wenn Sie am Ende einer Zeile die **EINGABETASTE** drücken.
>
> ![Optionen für C#-Text-Editorregisterkarten in Visual Studio](media/csharp-tabs-options.png)

## <a name="see-also"></a>Siehe auch

- [Allgemein, Umgebung, Dialogfeld „Optionen“](../../ide/reference/general-environment-options-dialog-box.md)