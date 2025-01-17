---
title: 'Vorgehensweise: Anzeigen von vorhandenen Typen (Klassen-Designer) | Microsoft-Dokumentation'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c33ae053a605e50aa8d1940fc97f3c0f687b48fa
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695334"
---
# <a name="how-to-view-existing-types-class-designer"></a>Vorgehensweise: Anzeigen von vorhandenen Typen (Klassen-Designer)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um einen vorhandenen Typ und die zugehörigen Member anzuzeigen, fügen Sie seine Form einem Klassendiagramm hinzu.  
  
 Es werden lokale und referenzierte Typen angezeigt. Ein lokaler Typ ist im aktuell geöffneten Projekt vorhanden und kann sowohl gelesen als auch geschrieben werden. Ein Typ, auf den verwiesen wird, ist in einem anderen Projekt oder einer Assembly, auf die verwiesen wird, enthalten und ist schreibgeschützt.  
  
 Informationen zum Entwerfen neuer Typen in Klassendiagrammen finden Sie unter [Vorgehensweise: Erstellen von Typen mit Klassen-Designer](../ide/how-to-create-types-by-using-class-designer.md).  
  
### <a name="to-see-types-in-a-project-on-a-class-diagram"></a>So zeigen Sie Typen aus einem Projekt in einem Klassendiagramm an  
  
1. Öffnen Sie in einem Projekt aus dem Projektmappen-Explorer eine Klassendiagrammdatei (CD-Datei). Falls kein Klassendiagramm vorhanden ist, fügen Sie dem Projekt ein neues Klassendiagramm hinzu. Weitere Informationen finden Sie unter [How to: Hinzufügen von Klassendiagrammen zu Projekten (Klassen-Designer)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).  
  
2. Ziehen Sie vom Projekt im Projektmappen-Explorer eine Quellcodedatei in das Klassendiagramm.  
  
   > [!WARNING]
   > Wenn Ihre Projektmappe ein Projekt mit Code enthält, der für mehrere Apps freigegeben ist, können Sie Dateien oder Code nur aus folgenden Quellen in ein Klassendiagramm ziehen:  
   > 
   > - Das App-Projekt, welches das Diagramm enthält  
   >   - Ein freigegebenes Projekt, das vom App-Projekt importiert wurde  
   >   - Ein referenziertes Projekt  
   >   - Eine Assembly  
  
    Daraufhin werden die Formen, die die in der Quellcodedatei definierten Typen darstellen, im Diagramm an der Stelle angezeigt, an die Sie die Datei gezogen haben.  
  
   Sie können im Projekt enthaltene Typen auch anzeigen, indem Sie einen oder mehrere Typen vom Projektknoten in der Klassenansicht in das Klassendiagramm ziehen.  
  
> [!TIP]
> Wenn die Klassenansicht nicht geöffnet ist, rufen Sie sie über das Menü **Ansicht** auf. Weitere Informationen über die Klassenansicht finden Sie unter [Anzeigen von Klassen und deren Membern](https://msdn.microsoft.com/71e9e8f3-261a-4e0c-87bf-5ec48b8bf333).  
  
 Wählen Sie in der Klassenansicht einen oder mehrere Typen aus, klicken Sie mit der rechten Maustaste auf die ausgewählten Typen und wählen **Klassendiagramm anzeigen** aus, um Typen im Diagramm an den Standardorten anzuzeigen.  
  
> [!NOTE]
> Enthält das Projekt bereits ein geschlossenes Klassendiagramm mit dem Typ, wird das Klassendiagramm mit der Typform geöffnet. Ist in dem Projekt hingegen kein Klassendiagramm mit dem Typ enthalten, erstellt der Klassen-Designer im Projekt ein neues Klassendiagramm und öffnet dieses mit dem Typ.  
  
 Wenn Sie einen Typ in einem Diagramm zum ersten Mal anzeigen, wird die Form standardmäßig reduziert angezeigt. Sie können die Form erweitern, um ihren Inhalt anzuzeigen.  
  
### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>So zeigen Sie den Inhalt eines Projekts in einem Klassendiagramm an  
  
1. Klicken Sie im Projektmappen-Explorer oder in der Klassenansicht mit der rechten Maustaste auf das Projekt, und wählen Sie **Anzeigen** und anschließend **Klassendiagramm anzeigen** aus.  
  
     Daraufhin wird ein automatisch ausgefülltes Klassendiagramm erstellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorgehensweise: Anzeigen einer Vererbung zwischen Typen (Klassen-Designer)](../ide/how-to-view-inheritance-between-types-class-designer.md)   
 [Vorgehensweise: Anpassen von Klassendiagrammen (Klassen-Designer)](../ide/how-to-customize-class-diagrams-class-designer.md)   
 [Anzeigen von Typen und Beziehungen (Klassen-Designer)](../ide/viewing-types-and-relationships-class-designer.md)
