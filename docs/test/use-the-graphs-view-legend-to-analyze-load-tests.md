---
title: Verwenden der Legende der Grafikansicht zum Analysieren von Auslastungstests
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Load Test Analyzer, graphs view legend
- load tests, graphs view legend
ms.assetid: 0f6ba8e4-1343-419c-8a9f-240cf50efed7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4c29620cad3333144d65386e509339e2f5eccddf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562675"
---
# <a name="use-the-graphs-view-legend-to-analyze-load-tests"></a>Verwenden der Legende der Diagrammansicht zum Analysieren von Auslastungstests

Die Diagrammansicht des Auslastungstest-Analyzers enthält einen Legendenbereich, in dem Informationen zu allen dem derzeit ausgewählten Diagramm zugeordneten Leistungsindikatoren angezeigt werden.

![Legende für Diagrammansicht](../test/media/load_viewlegend.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Die Legende enthält die folgenden Informationen:

- **Im Diagramm anzeigen:** Geben Sie mithilfe der Kontrollkästchen an, ob die Linie für einen bestimmten Indikator wie z.B. **Benutzerauslastung** oder **Fehler/s** im Diagramm eingezeichnet werden soll. Aktivieren Sie ein Kontrollkästchen, wenn die Linie ins Diagramm eingezeichnet werden soll. Deaktivieren Sie ein Kontrollkästchen, um die Zeichnungslinie aus dem Diagramm zu entfernen. Wenn eine Zeichnungslinie entfernt wird, wird die Statistik für den Indikator weiterhin in der Legende angezeigt.

- **Bereich:** In dieser Spalte wird der y-Achsen-Bereich des Leistungsindikators angezeigt. Standardmäßig wird dieser Wert automatisch angepasst, wenn sich der Bereich der Beispieldaten ändert. Ein automatisch angepasster Bereich ist stets um die nächste Zehnerpotenz größer als der Maximalwert. Dazu gehören negative Zehnerpotenzen. Ein Diagramm kann eine Vielzahl von Indikatoren, jeder mit einem anderen Bereich, enthalten. Daher wird die y-Achse nicht mit einem bestimmten Bereich, sondern mit Werten von 0 bis 100 gekennzeichnet, die einen Prozentsatz des Gesamtbereichs für jeden Indikator darstellen. Für einen Indikator mit einem Bereich von 1000 z. B. würde ein Datenpunkt von 60 auf der y-Achse einem Wert von 600 für den Indikator entsprechen.

    > [!NOTE]
    > Sie können die automatische Bereichswertanpassung deaktivieren, indem Sie den Bereich auf einen bestimmten Wert beschränken. Wenn der Bereich beschränkt ist, werden alle den Bereich überschreitenden Werte als der maximale Wert angezeigt, den Sie oben im Diagramm angegeben haben. Beschränken Sie mithilfe des Dialogfelds **Zeichnungsoptionen** den Bereich auf einen bestimmten Wert.

- **Indikator:** Die vier Spalten **Indikator**, **Instanz**, **Kategorie** und **Computer** identifizieren zusammen den Leistungsindikator eindeutig.

- **Farbe:** Die Spalte **Farbe** zeigt die Farbe und die Linienart der gezeichneten Linie für den Leistungsindikator an. Im Dialogfeld **Zeichnungsoptionen** können Sie die Farbe oder Linienart eines Leistungsindikators im Diagramm ändern. Das Dialogfeld **Zeichnungsoptionen** ist im Kontextmenü der Legende verfügbar.

- **Statistik:** Die Spalten **Min.** , **Max.** , **Durchschn.** und **Letzte** zeigen die jeweilige Statistik für den Leistungsindikator an. Diese Werte entsprechen den Daten, die im sichtbaren Bereich des Diagramms angezeigt werden. Wenn Sie z. B. einen Bereich einer Ausführung vergrößern, spiegelt die Legendenstatistik Werte nur für den vergrößerten Bereich wider. Die Spalte "Letzte" stellt den Wert des Leistungsindikators des zuletzt abgeschlossenen Samplingintervalls dar.

    > [!NOTE]
    > Die Spalte "Letzte" wird nur in der Legende des Auslastungstest-Analyzers während der Ausführung des Auslastungstests angezeigt.

     Weitere Informationen finden Sie unter [Vorgehensweise: Vergrößern eines Diagrammbereichs in Auslastungstestergebnissen](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md).

Das Auswählen eines Elements in der Legende bewirkt Folgendes:

- Das Element kann aus der Legende und dem Diagramm entfernt werden. Klicken Sie mit der rechten Maustaste auf das Element, und wählen Sie **Löschen** aus, oder drücken Sie die **ENTF-TASTE**.

- Die gezeichnete Zeile im Diagramm wird hervorgehoben.

- Im Datenraster werden Daten für das ausgewählte Element angezeigt.

- Ermöglicht den Zugriff auf das Dialogfeld **Zeichnungsoptionen** für den Leistungsindikator.

> [!TIP]
> Sie können auf der Symbolleiste des **Auslastungstest-Analyzers** die Dropdownschaltfläche **Diagrammoptionen** verwenden und auf **Legende anzeigen** klicken, um das der Diagrammansicht zugeordnete Panel **Legende** anzuzeigen oder auszublenden.

## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Vergrößern eines Diagrammbereichs in Auslastungstestergebnissen](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)
- [Analyze Load Test Results in the Graphs View (Analysieren von Auslastungstestergebnissen in der Diagrammansicht)](../test/analyze-load-test-results-in-the-graphs-view.md)
