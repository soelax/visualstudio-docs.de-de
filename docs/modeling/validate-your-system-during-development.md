---
title: Überprüfen des Systems während der Entwicklung
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9fb9810f1c212dfb881f5725676a79c6307b9cfa
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476503"
---
# <a name="validate-your-system-during-development"></a>Überprüfen des Systems während der Entwicklung

Visual Studio können die Software mit benutzeranforderungen und die Architektur des Systems in Einklang zu bringen.

Informationen dazu, welche Versionen von Visual Studio die einzelnen Funktionen unterstützen, finden Sie unter [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="key-tasks"></a>Hauptaufgaben

Verwenden Sie die folgenden Aufgaben, um Ihre Software zu überprüfen:

|**Aufgaben**|**Verwandte Themen**|
|-|-|
|**Stellen Sie sicher, dass die Software die Anforderungen der Benutzer erfüllt**:<br /><br />Verwenden Sie Anforderungen und architektonische Modelle, um die Tests des Systems und seiner Komponenten zu organisieren. Durch diese Vorgehensweise können Sie sicherstellen, dass die Anforderungen, die für die Benutzer und andere Projektbeteiligte wichtig sind, getestet werden. Außerdem können Sie dadurch die Tests schneller aktualisieren, wenn sich die Anforderungen ändern.|- [Entwickeln von Tests aus einem Modell](../modeling/develop-tests-from-a-model.md)|
|**Stellen Sie sicher, dass die Software mit dem vorgesehenen Entwurf des Systems konsistent bleibt:**<br /><br />Abhängigkeitsdiagramme beschreiben die beabsichtigten Abhängigkeiten zwischen den Komponenten Ihrer Anwendung. Während der Entwicklung können Sie überprüfen, ob die tatsächlichen Abhängigkeiten im Code dem vorgesehenen Entwurf entsprechen.|- [Erstellen von Abhängigkeitsdiagrammen aus Ihrem code](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Überprüfen von Code mit Abhängigkeitsdiagrammen](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>Externe Ressourcen

|**Kategorie**|**Links**|
|-|-|
|**Videos**|![Link zum Video](../data-tools/media/playvideo.gif) [Channel 9: Doug Seven: Verstehen von Code und Entwurf von Systemen mit Visual Studio 2010](https://channel9.msdn.com/shows/VS2010Launch/Doug-Seven-Code-Understanding-and-Systems-Design-with-Visual-Studio-2010)<br /><br /> ![Link zum Video](../data-tools/media/playvideo.gif) [Channel 9: Entwerfen einer Anwendung](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-5-architecting-an-application))|
|**Foren**|- [Visual Studio-Visualisierungs- & Modellierungstools](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio-Erweiterbarkeit](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)|

## <a name="see-also"></a>Siehe auch

- [Modellieren von Benutzeranforderungen](../modeling/model-user-requirements.md)
- [Analyse und Modellarchitektur](../modeling/analyze-and-model-your-architecture.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
