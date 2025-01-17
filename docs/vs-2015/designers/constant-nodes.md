---
title: Konstante Knoten | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 2c798a50-a2d7-459b-9879-ad4ad8290c9b
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d38a4f8a182562c11dbb742cb26392218edfd981
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162657"
---
# <a name="constant-nodes"></a>Konstante Knoten
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Im Shader-Designer stellen konstante Knoten Literalwerte und interpolierte Vertexattribute in Pixel-Shader-Berechnungen dar. Vertexattribute werden interpoliert und unterscheiden sich daher für jedes Pixel: Jede Pixel-Shader-Instanz empfängt eine andere Version der Konstanten. Dadurch erhält jedes Pixel ein eigenes Aussehen.  
  
## <a name="vertex-attribute-interpolation"></a>Interpolation der Vertexattribute  
 Das Bild einer 3D-Szene in einem Spiel oder einer App erfolgt durch die mathematische Verarbeitung einer Anzahl von Objekten in Bildschirmpixel. Diese Objekte werden durch Scheitelpunkte, Vertexattribute und Definitionen von Primitiven definiert. Alle Informationen, die erforderlich sind, um einem Pixel sein eigenes Aussehen zu verleihen, werden durch Vertexattribute bereitgestellt. Sie vermischen sich je nach Nähe des Pixels zu den verschiedenen Scheitelpunkten, aus denen sein *Primitiv* besteht. Ein Primitiv ist ein grundlegendes Renderingelement, also eine einfache Form wie ein Punkt, eine Linie oder ein Dreieck. Ein Pixel, das sich in unmittelbarer Nähe eines einzigen Scheitelpunkts befindet, empfängt Konstanten, die mit diesem Scheitelpunkt fast identisch sind. Ein Pixel hingegen, das sich gleichmäßig zwischen allen Konstanten eines Primitivs erstreckt, empfängt Konstanten, die den Durchschnitt aller Scheitelpunkte bilden. In der Grafikprogrammierung werden die Konstanten, die die Pixel empfangen, als *interpoliert* bezeichnet. Wenn Pixel auf diese Weise konstant Daten erhalten, entsteht dadurch eine ausgezeichnete visuelle Qualität. Gleichzeitig wird weniger Arbeitsspeicher benötigt und der Bedarf an Bandbreite reduziert sich.  
  
 Obwohl jede Pixel-Shader-Instanz nur einen Satz von konstanten Werten empfängt, die nicht geändert werden können, erhalten unterschiedliche Pixel-Shader-Instanzen auch unterschiedliche konstante Datensätze. Aufgrund dieses Designs kann ein Shader-Programm für jedes Pixel in der Primitive eine unterschiedliche Farbausgabe erzeugen.  
  
## <a name="constant-node-reference"></a>Verzeichnis konstanter Knoten  
  
|Knoten|Details|Eigenschaften|  
|----------|-------------|----------------|  
|**Kameravektor**|Der Vektor, der sich vom aktuellen Pixel bis zur Kamera im Raum erstreckt.<br /><br /> Damit können Sie Reflektionen im Raum berechnen.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float3`<br /> Der Vektor vom aktuellen Pixel bis zur Kamera|None|  
|**Farbkonstante**|Ein konstanter Farbwert<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Der Farbwert.|**Ausgabe**<br /> Der Farbwert.|  
|**Konstante**|Ein konstanter Skalarwert<br /><br /> **Ausgabe**<br /><br /> `Output`: `float`<br /> Der Skalarwert.|**Ausgabe**<br /> Der Skalarwert.|  
|**2D-Konstante**|Eine Zwei-Komponenten-Vektorkonstante<br /><br /> **Ausgabe**<br /><br /> `Output`: `float2`<br /> Der Vektorwert.|**Ausgabe**<br /> Der Vektorwert.|  
|**3D-Konstante**|Eine Drei-Komponenten-Vektorkonstante<br /><br /> **Ausgabe**<br /><br /> `Output`: `float3`<br /> Der Vektorwert.|**Ausgabe**<br /> Der Vektorwert.|  
|**4D-Konstante**|Eine Vier-Komponenten-Vektorkonstante<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Der Farbwert.|**Ausgabe**<br /> Der Vektorwert.|  
|**Normalisierte Position**|Die Position des aktuellen Pixels, ausgedrückt in normalisierten Gerätekoordinaten.<br /><br /> Die X-und die Y-Koordinate sind Werte im Bereich von [-1, 1]. Die Z-Koordinate verfügt über einen Wert im Bereich [0, 1], und die W-Komponente enthält den Punkttiefenwert im Anzeigebereich; W ist nicht normalisiert.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Die Position des aktuellen Pixels|None|  
|**Punktfarbe**|Die diffuse Farbe des aktuellen Pixels, die eine Kombination der diffusen Materialfarbe und den Vertexfarbattributen darstellt<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Die diffuse Farbe des aktuellen Pixels.|None|  
|**Punkttiefe**|Die Tiefe des aktuellen Pixels im Anzeigebereich<br /><br /> **Ausgabe**<br /><br /> `Output`: `float`<br /> Die Tiefe des aktuellen Pixels|None|  
|**Normalisierte Punkttiefe**|Die Tiefe des aktuellen Pixels, ausgedrückt in normalisierten Gerätekoordinaten.<br /><br /> Das Ergebnis hat einen Wert im Bereich [0, 1].<br /><br /> **Ausgabe**<br /><br /> `Output`: `float`<br /> Die Tiefe des aktuellen Pixels|None|  
|**Bildschirmposition**|Die Position des aktuellen Pixels, ausgedrückt in Bildschirmkoordinaten.<br /><br /> Die Bildschirmkoordinaten basieren auf dem aktuellen Anzeigebereich. Die X- und die Y-Komponenten enthalten die Bildschirmkoordinaten, die Z-Komponente enthält die Tiefe normalisiert auf einen Bereich von [0, 1], und die W-Komponente enthält den Wert für die Tiefe im Anzeigeraum.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Die Position des aktuellen Pixels|None|  
|**Oberflächennormale**|Die Oberflächennormale des aktuellen Pixels im Objektraum.<br /><br /> Damit können Sie Lichteinwirkungen und Reflexionen im Objektraum berechnen.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float3`<br /> Die Oberflächennormale des aktuellen Pixels|None|  
|**Tangentialraum-Kameravektor**|Der Vektor, der sich vom aktuellen Pixel bis zur Kamera im Tangentialraum erstreckt.<br /><br /> Damit können Sie Reflektionen im Tangentialraum berechnen.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float3`<br /> Der Vektor vom aktuellen Pixel bis zur Kamera|None|  
|**Tangentialraum-Lichtrichtung**|Der Vektor, der die Richtung definiert, in der Licht einer Lichtquelle im Bereich der Tangente des aktuellen Pixels umgewandelt wird.<br /><br /> Damit können Damit können Sie Licht- und Glanzlichteinwirkungen im Tangentialraum berechnen.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float3`<br /> Der Vektor vom aktuellen Pixel bis zu einer Lichtquelle.|None|  
|**Globale Normale**|Die Oberflächennormale des aktuellen Pixels im Raum.<br /><br /> Damit können Sie Lichteinwirkungen und Reflexionen im Raum berechnen.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float3`<br /> Die Oberflächennormale des aktuellen Pixels|None|  
|**World-Position**|Die Position des aktuellen Pixels im Raum.<br /><br /> **Ausgabe**<br /><br /> `Output`: `float4`<br /> Die Position des aktuellen Pixels|None|
