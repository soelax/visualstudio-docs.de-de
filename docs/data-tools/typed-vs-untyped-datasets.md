---
title: Typisierte Datasets im Vergleich zu nicht typisierten Datasets
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 31933e2045981fd6a0f38fb19a9480787c9f282a
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925583"
---
# <a name="typed-vs-untyped-datasets"></a>Typisierte Datasets im Vergleich zu nicht typisierten Datasets
Ein typisiertes DataSet ist ein DataSet, das zuerst von der Basis <xref:System.Data.DataSet> Klasse abgeleitet wird, und dann Informationen aus der in einer XSD-Datei gespeicherten **DataSet-Designer**verwendet, um eine neue, stark typisierte DataSet-Klasse zu generieren. Informationen aus dem Schema (Tabellen, Spalten usw.) werden generiert und in diese neue DataSet-Klasse als Satz von Objekten und Eigenschaften der ersten Klasse kompiliert. Da ein typisiertes DataSet von der Basis <xref:System.Data.DataSet> Klasse erbt, übernimmt die typisierte Klasse die gesamte Funktionalität <xref:System.Data.DataSet> der-Klasse und kann mit Methoden verwendet werden, die eine Instanz einer <xref:System.Data.DataSet> Klasse als Parameter annehmen.

Ein nicht typisiertes DataSet hat dagegen kein entsprechendes integriertes Schema. Wie bei einem typisierten DataSet enthält ein nicht typisiertes Dataset Tabellen, Spalten usw. – Diese werden jedoch nur als Auflistungen verfügbar gemacht. (Nachdem Sie jedoch die Tabellen und anderen Datenelemente in einem nicht typisierten Dataset manuell erstellt haben, können Sie die Struktur des Datasets mithilfe der- <xref:System.Data.DataSet.WriteXmlSchema%2A> Methode des Datasets als Schema exportieren.)

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>Vergleichen des Datenzugriffs in typisierten und nicht typisierten Datasets
Die-Klasse für ein typisiertes Dataset verfügt über ein Objektmodell, in dem die Eigenschaften die tatsächlichen Namen der Tabellen und Spalten übernehmen. Wenn Sie z. b. mit einem typisierten Dataset arbeiten, können Sie auf eine Spalte verweisen, indem Sie Code wie den folgenden verwenden:

[!code-csharp[VbRaddataDatasets#4](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_1.cs)]
[!code-vb[VbRaddataDatasets#4](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_1.vb)]

Wenn Sie hingegen mit einem nicht typisierten Dataset arbeiten, lautet der entsprechende Code:

[!code-csharp[VbRaddataDatasets#5](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_2.cs)]
[!code-vb[VbRaddataDatasets#5](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_2.vb)]

Der typisierte Zugriff ist nicht nur leichter lesbar, sondern wird auch vollständig von IntelliSense im **Code-Editor**von Visual Studio unterstützt. Die Syntax für das typisierte DataSet ist nicht nur einfacher zu arbeiten, sondern stellt die Typüberprüfung zur Kompilierzeit bereit, wodurch die Wahrscheinlichkeit von Fehlern beim Zuweisen von Werten zu datasetmembern erheblich reduziert wird. Wenn Sie den Namen einer Spalte in <xref:System.Data.DataSet> der Klasse ändern und dann die Anwendung kompilieren, erhalten Sie einen Buildfehler. Wenn Sie in der **Aufgabenliste**auf den Buildfehler doppelklicken, können Sie direkt zu den Zeilen oder Codezeilen wechseln, die auf den alten Spaltennamen verweisen. Der Zugriff auf Tabellen und Spalten in einem typisierten DataSet wird zur Laufzeit ebenfalls etwas beschleunigt, da der Zugriff zur Kompilierzeit und nicht über Auflistungen zur Laufzeit bestimmt wird.

Obwohl typisierte Datasets viele Vorteile haben, ist ein nicht typisiertes Dataset in einer Vielzahl von Situationen nützlich. Das offensichtlichste Szenario ist, wenn kein Schema für das Dataset verfügbar ist. Dies kann z. b. der Fall sein, wenn die Anwendung mit einer Komponente interagiert, die ein DataSet zurückgibt, Sie aber nicht im Voraus wissen, was die Struktur ist. Ebenso gibt es Zeiten, in denen Sie mit Daten arbeiten, die nicht über eine statische, vorhersagbare Struktur verfügen. In diesem Fall ist es unpraktisch, ein typisiertes DataSet zu verwenden, da Sie die typisierte DataSet-Klasse mit jeder Änderung in der Datenstruktur neu generieren müssten.

Im Allgemeinen gibt es viele Male, wenn Sie ein DataSet dynamisch erstellen können, ohne ein Schema verfügbar zu machen. In diesem Fall ist das Dataset einfach eine bequeme Struktur, in der Sie Informationen aufbewahren können, solange die Daten auf relationale Weise dargestellt werden können. Gleichzeitig können Sie die Funktionen des Datasets nutzen, z. b. die Möglichkeit, die Informationen zu serialisieren, um Sie an einen anderen Prozess zu übergeben, oder eine XML-Datei zu schreiben.

## <a name="see-also"></a>Siehe auch

- [Datasettools](../data-tools/dataset-tools-in-visual-studio.md)