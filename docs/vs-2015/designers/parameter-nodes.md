---
title: Parameterknoten | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: da54db0b-3a3d-48dc-858c-7ac43aa04b13
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 110f380f7450d611de5786fb865bdee8e64195f6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184983"
---
# <a name="parameter-nodes"></a>Parameterknoten
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Im Shader-Designer stellen die Parameterknoten Eingaben für den Shader dar, die unter der Kontrolle der Anwendung auf einer pro-Zeichnen Grundlage sind, z.B. Materialeigenschaften, direktionale Beleuchtung, Kameraposition und Zeit. Da Sie diese Parameter mit jedem Zeichenaufruf ändern können, können Sie den gleichen Shader verwenden, um einem Objekt eine andere Darstellung zu geben.  
  
## <a name="parameter-node-reference"></a>Parameterknotenverweis  
  
|Knoten|Details|Eigenschaften|  
|----------|-------------|----------------|  
|**World-Position (Kamera)**|Die Position der Kamera im Raum.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float4`<br /> Die Kameraposition.|None|  
|**Lichtrichtung**|Der Vektor, der die Richtung von Licht aus einer Lichtquelle im Tangentialraum definiert.<br /><br /> Damit können Sie Licht- und Glanzlichteinwirkungen im Tangentialraum berechnen.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float3`<br /> Der Vektor vom aktuellen Pixel bis zu einer Lichtquelle.|None|  
|**Material (Umgebung)**|Der Beitrag der verschwommene Farbe des aktuellen Pixels, der indirekter Beleuchtung zugeordnet ist.<br /><br /> Die verschwommene Farbe eines Pixels simuliert die Interaktion zwischen Beleuchtung und groben Flächen. Sie können den Parameter „Material (Umgebung)“ nutzen, um ungefähr anzugeben, wie indirekte Beleuchtung zur Darstellung eines Objekts in der realen Welt beiträgt.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float4`<br /> Die diffuse Farbe des aktuellen Pixels aufgrund indirekter Beleuchtung, d.h. Umgebungsbeleuchtung.|**Zugriff**<br /> **Öffentlich**, sodass die Eigenschaft im Modell-Editor festgelegt werden kann, andernfalls **Privat**.<br /><br /> **Wert**<br /> Die diffuse Farbe des aktuellen Pixels aufgrund indirekter Beleuchtung, d.h. Umgebungsbeleuchtung.|  
|**Material (Diffus)**|Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung streut.<br /><br /> Die verschwommene Farbe eines Pixels simuliert die Interaktion zwischen Beleuchtung und groben Flächen. Können Sie den Parameter „Material (Diffus)“ verwenden, um zu ändern, wie das aktuelle Pixel direkte Beleuchtung streut, d.h. direktionale, Punkt- und Spotbeleuchtung.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float4`<br /> Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung streut.|**Zugriff**<br /> **Öffentlich**, sodass die Eigenschaft im Modell-Editor festgelegt werden kann, andernfalls **Privat**.<br /><br /> **Wert**<br /> Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung streut.|  
|**Material (Selbstleuchtend)**|Der Farbbeitrag des aktuellen Pixels, der selbstleuchtender Beleuchtung zugeordnet ist.<br /><br /> Damit können Sie ein leuchtendes Objekt simulieren; d.h. ein Objekt, das sein eigenes Licht bereitstellt. Dieses Licht wirkt sich nicht auf andere Objekte aus.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float4`<br /> Die Farbeinwirkung des aktuellen Pixels aufgrund der selbsterzeugten Beleuchtung.|**Zugriff**<br /> **Öffentlich**, sodass die Eigenschaft im Modell-Editor festgelegt werden kann, andernfalls **Privat**.<br /><br /> **Wert**<br /> Die Farbeinwirkung des aktuellen Pixels aufgrund der selbsterzeugten Beleuchtung.|  
|**Material (Glanz)**|Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung reflektiert.<br /><br /> Die glänzende Farbe eines Pixels simuliert die Interaktion zwischen Beleuchtung und reibungslosen und spiegelähnlichen Flächen. Sie können den Parameter Glanzmaterial verwenden, um zu ändern, wie das aktuelle Pixel direkte Beleuchtung streut, d.h. direktionale, Punkt- und Spotbeleuchtung.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float4`<br /> Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung reflektiert.|**Zugriff**<br /> **Öffentlich**, sodass die Eigenschaft im Modell-Editor festgelegt werden kann, andernfalls **Privat**.<br /><br /> **Wert**<br /> Eine Farbe, die beschreibt, wie das aktuelle Pixel die direkte Beleuchtung reflektiert.|  
|**Material (Glanzkraft)**|Ein Skalarwert, der die Intensität von Glanzlichtern beschreibt.<br /><br /> Je größer die Glanzkraft, desto intensiver und weitreichender die Glanzlichter.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float`<br /> Der Exponent, mit dem die Intensität von Glanzlichtern auf dem Material des aktuellen Pixels definiert wird.|**Zugriff**<br /> **Öffentlich**, sodass die Eigenschaft im Modell-Editor festgelegt werden kann, andernfalls **Privat**.<br /><br /> **Wert**<br /> Der Exponent, mit dem die Intensität von Glanzlichtern auf dem aktuellen Pixel definiert wird.|  
|**Normalisierte Zeit**|Die Zeit in Sekunden, normalisiert auf den Bereich [0, 1], damit auf 0 zurückgesetzt wird, wenn die Zeit 1 erreicht.<br /><br /> Sie können dies als Parameter in Shaderberechnungen verwenden, z.B. um Texturkoordinaten, Farbwerte oder andere Attribute zu animieren.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float`<br /> Die normalisierte Zeit in Sekunden.|None|  
|**Zeit**|Die Zeit in Sekunden.<br /><br /> Sie können dies als Parameter in Shaderberechnungen verwenden, z.B. um Texturkoordinaten, Farbwerte oder andere Attribute zu animieren.<br /><br /> **Ausgabe:**<br /><br /> `Output`: `float`<br /> Die Zeit in Sekunden.|None|
