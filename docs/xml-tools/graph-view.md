---
title: Diagrammansicht im XML-Schema-Designer
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 5881afde-3f24-4eb9-bff8-6cb3fc8aade7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a9ef512108ae31617257becf702c2b820c0ab85
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68918636"
---
# <a name="graph-view"></a>Diagrammansicht

Die Diagrammansicht bietet eine grafische Darstellung der globalen Schemaknoten und der Beziehungen zwischen den Knoten. In der Diagrammansicht kann das Layout des Schemasets auf der Entwurfsoberfläche nicht geändert werden. Die Diagrammansicht enthält auch die Symbolleiste des XML-Schema-Designers und die Breadcrumb-Leiste.

Das folgende Bild zeigt die Diagrammansicht mit sechs globalen Knoten auf der Entwurfsoberfläche.

![Diagrammansicht im XML-Schema-Designer](../xml-tools/media/xsddesigner_graphview.gif)

## <a name="design-surface"></a>Entwurfs Oberfläche

In der Entwurfs Oberfläche der Diagramm Ansicht wird der Inhalt des Arbeitsbereichs des [XML-Schema-Designers](../xml-tools/xml-schema-designer-workspace.md)angezeigt. Wenn der Arbeitsbereich globale Knoten aus dem Schemaset enthält, werden die Knoten auf der Entwurfsoberfläche der Diagrammansicht angezeigt, und zwischen Knoten mit Beziehungen werden Pfeile gezeichnet.

Wenn Sie in der Diagramm Ansicht auf einen Knoten doppelklicken, wird der XML-Editor angezeigt.

Um ausgewählte Knoten aus dem Arbeitsbereich zu löschen, verwenden Sie die XSD- Designer-Symbolleiste oder die ENTF-Taste.

Wenn die Entwurfs Oberfläche leer ist, werden der XML-Editor, der **XML-Schema-Explorer**und das Wasserzeichen angezeigt. Das *Wasserzeichen* ist eine Liste mit Links zu allen Ansichten des XSD-Designers.

![XSD-Designer, Diagrammansicht](../xml-tools/media/xsdgraphviewwatermark.gif)

Wenn der Schemaset Fehler aufweist, wird der folgende Text am Ende der Liste angezeigt: "Verwenden Sie die Fehlerliste, um die Fehler in der Gruppe anzuzeigen und zu beheben."

## <a name="breadcrumb-bar"></a>Breadcrumb-Leiste

Die Breadcrumb-Leiste am unteren Rand der Diagrammansicht zeigt an, wo sich der ausgewählte Knoten im Schemaset befindet. Wenn mehrere Elemente ausgewählt sind, ist die Breadcrumb-Leiste leer.

## <a name="context-right-click-menu"></a>Kontextmenü (Rechtsklick)

In der folgenden Tabelle werden die Optionen beschrieben, die für alle Knoten auf der Entwurfsoberfläche der Diagrammansicht verfügbar sind.

|Option|Beschreibung|
|-|-----------------|
|**Im XML-Schema-Explorer anzeigen**|Legt den Fokus auf den Schema-Explorer und hebt den Schemasetknoten hervor.|
|**In Diagramm Ansicht anzeigen**|Wechselt zur Diagrammansicht (abgeblendet).|
|**Generieren von Beispiel-XML**|Ist nur für globale Elemente verfügbar. Generiert eine Beispiel-XML-Datei für das globale Element.|
|**Arbeitsbereich löschen**|Löscht den Arbeitsbereich und die Entwurfsoberfläche.|
|**Aus Arbeitsbereich entfernen**|Entfernt ausgewählte Knoten aus dem Arbeitsbereich und der Entwurfsoberfläche.|
|**Alles außer Auswahl aus Arbeitsbereich entfernen**|Entfernt nicht ausgewählte Knoten aus dem Arbeitsbereich und der Entwurfsoberfläche.|
|**Diagramm als Bild exportieren**|Speichert die Entwurfsoberfläche in einer XPS-Datei.|
|**Alle auswählen**|Wählt alle Knoten auf der Entwurfsoberfläche aus.|
|**Code anzeigen**|Öffnet die Datei, die den ausgewählten Knoten im XML-Editor enthält. Das Element, das im XML- **Schema-Explorer** ausgewählt ist, wird auch im XML-Editor ausgewählt.|
|**Eigenschaftenfenster**|Öffnet das **Eigenschaften** Fenster (wenn es nicht bereits geöffnet ist). In diesem Fenster werden Informationen zum Knoten angezeigt.|

Neben den oben beschriebenen allgemeinen Optionen enthält das Kontextmenü für globale Elemente die folgenden Optionen:

|Option|Beschreibung|
|-|-----------------|
|**Typdefinition hinzufügen**|Fügt dem Diagramm den Basistyp hinzu.|
|**Alle Verweise hinzufügen**|Fügt alle Knoten, die auf das Element verweisen, hinzu und zeichnet Pfeile, um die Beziehungen anzugeben.|
|**Ersetzungs Gruppenmitglieder hinzufügen**|Fügt alle Ersetzungsgruppenelemente hinzu. Diese Option wird in der Ansicht angezeigt, wenn das Element der Kopf oder das Mitglied einer Ersetzungsgruppe ist.|
|**Generieren von Beispiel-XML**|Generiert eine Beispiel-XML-Datei für das globale Element.|

Neben den oben beschriebenen allgemeinen Optionen enthält das Kontextmenü für globale einfache und globale komplexe Typen die folgenden Optionen:

|Option|Beschreibung|
|-|-----------------|
|**Basistyp hinzufügen**|Fügt den Basistyp des ausgewählten Typs hinzu, wenn der ausgewählte Typ von einem globalen Typ abgeleitet ist.|
|**Alle Verweise hinzufügen**|Fügt alle Verweise des ausgewählten Typs hinzu. Dazu zählen Elemente und Attribute des ausgewählten Typs und vom ausgewählten Typ abgeleitete Typen.|
|**Alle abgeleiteten Typen hinzufügen**|Fügt alle Typen hinzu, die direkt und indirekt vom ausgewählten Typ abgeleitet sind.|
|**Alle Vorgänger hinzufügen**|Fügt alle übergeordneten (Basis-)Typen hinzu.|

Neben den oben beschriebenen allgemeinen Optionen enthält das Kontextmenü für globale Gruppen und Attributgruppen die folgenden Optionen:

|Option|Beschreibung|
|-|-----------------|
|**Alle Verweise hinzufügen**|Fügt alle Knoten, die auf die Gruppe verweisen, hinzu und zeichnet Pfeile, um die Beziehungen anzugeben.|
|**Alle Mitglieder hinzufügen**|Fügt alle Mitglieder der Gruppe hinzu und zeichnet Pfeile, um die Beziehungen anzugeben.|

Neben den oben beschriebenen allgemeinen Optionen enthält das Kontextmenü für globale Attribute die folgenden Optionen:

|Option|Beschreibung|
|-|-----------------|
|**Alle Verweise hinzufügen**|Fügt alle Knoten, die auf die Gruppe verweisen, hinzu und zeichnet Pfeile, um die Beziehungen anzugeben.|

## <a name="properties-window"></a>Eigenschaftenfenster

Verwenden Sie das Kontextmenü (Rechtsklick), um das Fenster **Eigenschaften** zu öffnen. Standardmäßig wird das Fenster **Eigenschaften** in der unteren rechten Ecke von Visual Studio angezeigt. Wenn Sie auf einen Knoten klicken, der in der Inhalts Modell Ansicht gerendert wird, werden die Eigenschaften dieses Knotens im **Eigenschaften** Fenster angezeigt.

## <a name="xsd-toolbar"></a>XSD-Symbolleiste

Die folgenden XSD-Symbolleistenschaltflächen sind aktiviert, wenn die Diagrammansicht aktiv ist.

![Symbolleiste für XML-Schema-Designer](../xml-tools/media/xsdgraphviewtoolbar.gif)

|Option|Beschreibung|
|-|-----------------|
|**Start Ansicht anzeigen**|Wechselt zur [Start Ansicht](../xml-tools/start-view.md). Auf diese Sicht kann mit der Tastenkombination zugegriffen werden:STRG+**1**.|
|**Inhalts Modell Ansicht anzeigen**|Wechselt zur [Inhalts Modell Ansicht](../xml-tools/content-model-view.md). Auf diese Sicht kann mit der Tastenkombination zugegriffen werden:STRG+**2**.|
|**Diagramm Ansicht anzeigen**|Wechselt zur [Diagramm Ansicht](../xml-tools/graph-view.md). Auf diese Sicht kann mit der Tastenkombination zugegriffen werden:STRG+**3**.|
|**Arbeitsbereich löschen**|Löscht den Arbeitsbereich und die Entwurfsoberfläche.|
|**Aus Arbeitsbereich entfernen**|Entfernt ausgewählte Knoten aus dem Arbeitsbereich und der Entwurfsoberfläche.|
|**Alles außer Auswahl aus Arbeitsbereich entfernen**|Entfernt nicht ausgewählte Knoten aus dem Arbeitsbereich und der Entwurfsoberfläche. Diese Option ist in der Inhaltsmodellansicht und der Diagrammansicht aktiviert.|
|**Von links nach rechts**|Ändert das Layout in der Diagrammansicht in eine von links nach rechts angeordnete hierarchische Darstellung der Knoten. Auf diese Option kann mit der Tastenkombination zugegriffen werden: **Alt nach-** **rechts-Taste.** +|
|**Von rechts nach links**|Ändert das Layout in der Diagrammansicht in eine von rechts nach links angeordnete hierarchische Darstellung der Knoten. Auf diese Option kann mit der Tastenkombination zugegriffen werden: **Alt nach-** **Links-Taste.** +|
|**Von oben nach unten**|Ändert das Layout in der Diagrammansicht in eine von oben nach unten angeordnete hierarchische Darstellung der Knoten. Auf diese Option kann mit der Tastenkombination zugegriffen werden:Alt+-**Pfeil nach unten**.|
|**Unten nach oben**|Ändert das Layout in der Diagrammansicht in eine von unten nach oben angeordnete hierarchische Darstellung der Knoten. Auf diese Option kann mit der Tastenkombination zugegriffen werden: **Alt nach-** **oben-Taste.** +|

## <a name="panscroll"></a>Schwenken/Bildlauf

Sie können die Entwurfs Oberfläche schwenken, indem Sie die Scrollleisten verwenden oder indem Sie die **STRG** -Taste gedrückt halten, während Sie auf die Maus klicken und die Maus ziehen. Wenn Sie die Entwurfsoberfläche mittels Klicken und Ziehen schwenken, wird der Cursor als vier sich kreuzende und in unterschiedliche Richtungen weisende Pfeile angezeigt.

## <a name="undoredo"></a>Rückgängig/Wiederholen

Die Funktion zum Rückgängigmachen bzw. Wiederholen ist in der Diagrammansicht für folgende Aktionen aktiviert:

- Hinzufügen eines einzelnen Knotens per Drag &amp; Drop

- Hinzufügen mehrerer Knoten aus dem Suchergebnisfenster im Schema-Explorer oder Abfragen in der Ausgangsansicht

- Löschen einzelner oder mehrerer Knoten

## <a name="zoom"></a>Zoom

Die Zoomfunktion befindet sich in der unteren rechten Ecke der Diagrammansicht.

Der Zoomfaktor kann wie folgt gesteuert werden:

- Indem Sie die **STRG** -Taste gedrückt halten und das Mausrad drehen, wenn der Mauszeiger auf die Oberfläche der Diagramm Ansicht zeigt.

- Verwenden Sie das Schieberegler-Steuerelement. Auf dem Schieberegler wird der aktuelle Zoomfaktor angezeigt.

Der Zoom Schieberegler ist nicht transparent, wenn Sie ihn auswählen, darauf zeigen oder mit dem Mausrad **STRG** drücken, um zu zoomen. zu allen anderen Zeiten ist er transparent.

## <a name="xml-editor-integration"></a>Integration des XML-Editors

Sie können zwischen der Diagramm Ansicht und dem XML-Editor hin-und herwechseln, indem Sie auf einen Knoten klicken und das Menü Code Kontext anzeigen (Rechtsklick) verwenden.

Wenn Sie im XML-Editor Änderungen am Schemaset vornehmen, werden die Änderungen in der Diagramm Ansicht synchronisiert. Weitere Informationen finden Sie unter [Integration in den XML-Editor](../xml-tools/integration-with-xml-editor.md).

## <a name="see-also"></a>Siehe auch

- [Designoberfläche](../xml-tools/xml-schema-designer-workspace.md)