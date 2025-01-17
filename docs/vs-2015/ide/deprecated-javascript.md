---
title: '&lt;als veraltet markiert&gt; (JavaScript) | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: cf33d371-59da-4310-95ee-d7524fd9d58c
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b93a2b4dcc541f32c16766da0dd9dd19a4fdfe0d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68177816"
---
# <a name="ltdeprecatedgt-javascript"></a>&lt;als veraltet markiert&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Gibt eine veraltete Funktion oder Methode an.  
  
## <a name="syntax"></a>Syntax  
  
```  
<deprecated  
    type="deprecate|remove"  
    locid="descriptionID">description  
</deprecated>  
```  
  
#### <a name="parameters"></a>Parameter  
 `type`  
 Optional. Gibt an, ob die Funktion oder Methode in einer zukünftigen Version entfernt wird oder ob die Funktion oder Methode bereits entfernt wurde und ihre Verwendung möglicherweise zu einem Fehler führen wird. Legen Sie es auf `deprecate` fest, um anzugeben, dass die Funktion oder Methode in einer zukünftigen Version entfernt wird. Legen Sie es auf `remove` fest, um anzugeben, dass die Funktion oder Methode bereits entfernt wurde.  
  
 `locid`  
 Optional. Der Bezeichner für Lokalisierungsinformationen über die Funktion oder Methode. Der Bezeichner ist entweder eine Member-ID, oder er entspricht dem `name`-Attributwert in einem Meldungsbündel, das von OpenAjax-Metadaten definiert wird. Der Bezeichnertyp hängt vom Format ab, das im Element [\<loc>](../ide/loc-javascript.md) angegeben wird.  
  
 `description`  
 Optional. Eine Beschreibung der Funktion oder Methode, die veraltet ist.  
  
## <a name="remarks"></a>Anmerkungen  
 Die Elemente, die verwendet werden, um Funktionen, wie unter anderem `<deprecated>`, mit Anmerkungen zu versehen und müssen vor allen Anweisungen in den Funktionstext eingefügt werden. Wenn Sie eine Funktion als veraltet markieren, es wird empfohlen, die Sie ersetzen die [ \<summary >](../ide/summary-javascript.md) -Element mit der `<deprecated>` Element.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird die Verwendung des `<deprecated>`-Elements veranschaulicht.  
  
```javascript  
function areaFunction(radiusParam) {  
    /// <deprecated type="deprecate" >Determines the area of a circle when supplied a radius parameter.</deprecated>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Dokumentationskommentare](../ide/xml-documentation-comments-javascript.md)
