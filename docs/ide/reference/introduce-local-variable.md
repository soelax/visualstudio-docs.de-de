---
title: Bereitstellen einer lokalen Variable
description: Generieren Sie eine lokale Variable, um einen vorhandenen Ausdruck zu ersetzen. Wählen Sie den Ausdruck aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie das Menü „Schnellaktionen und Refactorings...“ aus. Wählen Sie dann „Lokales Element für alle Vorkommen von „Ausdruck“ bereitstellen“ aus.
ms.date: 01/26/2018
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 43f54072d495cfdd6607ccb033ffd1a1713ad8bb
ms.sourcegitcommit: 0f5f7955076238742f2071d286ad8e896f3a6cad
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/25/2019
ms.locfileid: "68483698"
---
# <a name="introduce-a-local-variable-in-visual-studio"></a>Bereitstellen einer lokalen Variable in Visual Studio

Diese Codegenerierung gilt für:

- C#

- Visual Basic

**Beschreibung:** Hiermit können Sie sofort eine lokale Variable generieren, um einen vorhandenen Ausdruck zu ersetzen.

**Hintergrund:** Sie verwenden Code, der bei Verwendung in einer lokalen Variable später problemlos wiederverwendet werden kann.

**Vorteile**: Sie könnten den Code für die Verwendung an verschiedenen Stellen mehrmals kopieren und einfügen. Besser wäre es jedoch, den Vorgang einmal durchzuführen, das Ergebnis in einer lokalen Variable zu speichern und durchgehend die lokale Variable zu verwenden.

## <a name="how-to"></a>Vorgehensweise

1. Markieren Sie den Ausdruck, der einer neuen lokalen Variable zugewiesen werden soll.

   - C#:

       ![Hervorgehobener Code – C#](media/local-highlight-cs.png)

   - Visual Basic:

       ![Hervorgehobener Code in Visual Basic](media/local-highlight-vb.png)

2. Führen Sie dann eine der folgenden Aktionen aus:

   - **Tastatur**
      - Drücken Sie an einer beliebigen Stelle in einer Zeile **STRG**+ **.** , um das Menü **Schnellaktionen und Refactorings** aufzurufen.
   - **Maus**
      - Führen Sie einen Rechtsklick durch, und klicken Sie auf das Menü **Schnellaktionen und Refactorings**.
      - Klicken Sie auf die Schaltfläche ![Schraubendrehersymbol](media/screwdriver.png) die am linken Rand angezeigt wird, sofern der Textcursor bereits in der Zeile mit dem hervorgehobenen Ausdruck platziert wurde.

   ![Vorschau der Aktion zum Bereitstellen eines lokalen Elements](media/local-preview-cs.png)

3. Wählen Sie **Introduce local for (all occurrences) of „expression“** (Lokales Element für (alle Vorkommen von) „Ausdruck“ bereitstellen) im Dropdownmenü aus.

   > [!TIP]
   > Klicken Sie im unteren Bereich des Vorschaufensters auf den Link **Vorschau der Änderungen**, um vor einer Auswahl [alle Änderungen anzuzeigen](../../ide/preview-changes.md), die vorgenommen werden.

   Die lokale Variable wird in Abhängigkeit vom angegebenen Typ erstellt. Geben Sie der neuen lokalen Variable einen neuen Namen.

   - C#:

       ![Ergebnis der Implementierung einer Schnittstelle in C#](media/local-result-cs.png)

   - Visual Basic:

       ![Ergebnis der Implementierung einer Schnittstelle in Visual Basic](media/local-result-vb.png)

   > [!NOTE]
   > Sie können die Menüoption **...alle Vorkommen von...** verwenden, um nicht nur den hervorgehobenen Ausdruck, sondern jede Instanz des ausgewählten Ausdrucks zu ersetzen.

## <a name="see-also"></a>Siehe auch

- [Codegenerierung](../code-generation-in-visual-studio.md)
- [Vorschau der Änderungen](../../ide/preview-changes.md)