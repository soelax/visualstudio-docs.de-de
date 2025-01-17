---
title: Schnellstart, Umgebung, Dialogfeld „Optionen“
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.QuickLaunch
- vs.quicklaunch
helpviewer_keywords:
- searching IDE
- IDE, searching
ms.assetid: 4200f297-d065-4723-9a30-d91ff2e26c9d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 1f5026a014b5adc96f0729d130c4398474d6d413
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605904"
---
# <a name="quick-launch-environment-options-dialog-box"></a>Schnellstart, Umgebung, Dialogfeld „Optionen“

Sie können **Schnellstart** verwenden, um Aktionen für IDE-Objekte wie Optionen, Vorlagen oder Menüs schnell zu suchen und auszuführen. Sie können **Schnellstart** nicht zur Suche nach Code und Symbolen verwenden. Das Suchfeld **Schnellstart** befindet sich rechts oben in der Menüleiste und kann mit der Tastenkombination **STRG**+**Q** aufgerufen werden. Geben Sie einfach die Suchzeichenfolge im Feld ein. Verwenden Sie ‘@@‘, um nach Zeichenfolgen zu suchen, die @ enthalten.

**Schnellstart** ist standardmäßig aktiviert, wenn Sie Visual Studio installieren. Auf der Menüleiste können Sie den **Schnellstart** darstellen oder ausblenden, indem Sie **Extras** > **Optionen** auswählen. Erweitern Sie den Knoten **Umgebungen**, und wählen Sie dann **Schnellstart** aus. Aktivieren oder deaktivieren Sie das Kontrollkästchen **Schnellstart aktivieren**. Sie können auf dieser Seite auch Suchkategorien aktivieren oder deaktivieren.

## <a name="category-list"></a>Kategorieliste

Schnellstart-Suchergebnisse werden in vier Kategorien unterteilt: **Zuletzt verwendet**, **Menüs**, **Optionen** und **Geöffnete Dokumente**. Außerdem wird die Anzahl von Elementen pro Kategorie angezeigt. Wenn die Suchergebnisse nach Kategorie durchlaufen werden sollen, drücken Sie die Tastenkombination **STRG**+**Q**. So werden alle Ergebnisse der nächsten Kategorie angezeigt. Nach Anzeigen der letzten Kategorie können Sie mit **STRG**+**Q** einige Ergebnisse aus jeder Kategorie aufrufen. Mit **STRG**+**UMSCHALT**+**Q** können Sie in umgekehrter Reihenfolge durch die Kategorien navigieren. Wählen Sie den Kategorienamen aus, um alle Suchergebnisse aus einer Kategorie anzuzeigen.

Sie können die folgenden Tastenkombinationen verwenden, um die Suche auf bestimmte Kategorien einzuschränken.

|Kategorie|Verknüpfung|Verknüpfungsbeschreibung|
|--------------|--------------| - |
|Zuletzt verwendet|@mru<br /><br /> Beispiel: `@mru font`|Zeigt bis zu fünf Elemente der Liste **Zuletzt verwendet** an.|
|Menüs|@menu<br /><br /> Beispiel: `@menu project`|Schränkt die Suche auf Menüelemente ein.|
|Optionen|@opt<br /><br /> Beispiel: `@opt font`|Schränkt die Suche auf Einstellungen im Dialogfeld **Optionen** ein.|
|Dokumente|@doc<br /><br /> Beispiel: `@doc program.cs`|Schränkt die Suche auf Dateinamen und Pfade der geöffneten Dokumente ein, die den Suchkriterien entsprechen. Der Text in den Dateien selbst wird nicht durchsucht.|

> [!NOTE]
> Die Tastenkombinationen können im Dialogfeld **Optionen** unter **Allgemein** > **Tastatur** geändert werden.

## <a name="show-previous-results"></a>Vorherige Ergebnisse anzeigen

Standardmäßig wird der eingegebene Suchbegriff nicht zwischen Suchsitzungen beibehalten. Die Suchzeichenfolge wird gelöscht, wenn Sie nach einem Begriff suchen. Bewegen Sie den Cursor außerhalb des Bereichs **Schnellstart** und dann wieder zurück. Um die Suchergebnisse beizubehalten, wechseln Sie in das Dialogfeld **Optionen**, wählen Sie **Schnellstart** aus, und aktivieren Sie dann das Kontrollkästchen **Suchergebnisse aus vorherigen Suchen anzeigen, wenn Schnellstart aktiviert ist** . Wenn Sie das nächste Mal eine Suche ausführen, verlassen Sie den Schnellstartbereich, und kehren Sie dahin zurück. Der Schnellstart behält den zuletzt verwendeten Suchbegriff bei und zeigt auch die Suchergebnisse an.
