---
title: 'Sample Excel Extension: PropertyProvider-Klasse | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 075d9b8d-8658-4fca-8711-08304dbac1c5
caps.latest.revision: 11
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d38b430dd88eb1a732c4e4ca335a0a5bb057b1f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189452"
---
# <a name="sample-excel-extension-propertyprovider-class"></a>Sample Excel Extension: PropertyProvider-Klasse
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diese interne Klasse erweitert die <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>-Klasse und stellt Eigenschaftendienste für [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]-Elemente zur Aufzeichnung und Wiedergabe von Tests Benutzeroberfläche bereit.  
  
## <a name="getcontrolsupportlevel-method"></a>GetControlSupportLevel-Methode  
 Die <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A>-Methode gibt eine Zahl zurück, die die Unterstützungsebene angibt, die Eigenschaftenanbieter für das bereitgestellte Steuerelement anbieten können. Je höher der zurückgegebene Wert, desto umfassender die Unterstützung des Eigenschaftenanbieters für das Steuerelement. In diesem Fall prüft die Methode den Wert der <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.TechnologyName%2A>-Eigenschaft des dargestellten Steuerelements. Wenn der Wert „Excel“ lautet und <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IUITechnologyElement.ControlTypeName%2A> angibt, dass es sich um ein `CellElement` handelt, wird von der Methode der höchste Wert zurückgegeben. Andernfalls wird 0 (null) zurückgegeben, was bedeutet, dass keine Unterstützung verfügbar ist.  
  
## <a name="getpropertynames-method"></a>GetPropertyNames-Methode  
 Gibt ein Wörterbuch der Eigenschaftennamen und Eigenschaftendeskriptoren für die unterstützten Eigenschaften eines Steuerelements für Excel-Zellen zurück.  
  
## <a name="getpropertydescriptor-method"></a>GetPropertyDescriptor-Methode  
 Diese Methode wird vom Testframework aufgerufen, um den vordefinierten Eigenschaftendeskriptor für den angegebenen Eigenschaftennamen abzurufen.  
  
## <a name="getpropertyvalue-and-setpropertyvalue-methods"></a>GetPropertyValue und SetPropertyValue-Methode  
 Die `GetPropertyValue`-Methode gibt den Eigenschaftswert aus Excel mithilfe der `Communicator`-Klasse dieser Erweiterung zurück. Die `SetPropertyValue`-Methode verwendet die <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard>-Klasse und die `Communicator`-Komponente, um den Eigenschaftswert festzulegen. Diese Methoden werden vom Testframework aufgerufen.  
  
## <a name="code-generation-customization-methods"></a>Anpassungsmethoden für die Codegenerierung  
 Diese Methoden sind nicht für diese Erweiterung implementiert. Deshalb geben Sie entweder `null` zurück oder lösen <xref:System.NotImplementedException> aus.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard>   
 [Erweitern von Tests der codierten UI-Tests und Aktionsaufzeichnungen zur Unterstützung von Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
