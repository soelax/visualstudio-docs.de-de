---
title: Neues in Visual Studio 2019
titleSuffix: ''
description: Informationen zu den neuen Features in Visual Studio 2019
ms.date: 07/23/2019
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 00bec66b-bcee-46f5-91d9-f73a2b469744
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 1f4a055f62fe76c701858f82b4778f7a3b19fa0a
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68918789"
---
# <a name="whats-new-in-visual-studio-2019"></a>Neues in Visual Studio 2019

**Für [Release 16.2](/visualstudio/releases/2019/release-notes/) aktualisiert**

>[!div class="button"]
>[Herunterladen von Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)

Visual Studio 2019 bietet branchenführende Tools und Dienste für jeden Entwickler, jede App und jede Plattform. Ob Sie Visual Studio zum ersten Mal oder schon seit Jahren nutzen, Sie werden von der neuen Version überzeugt sein.

Im Folgenden erhalten Sie einen allgemeinen Überblick über die Neuheiten:

* **[Entwickeln:](#develop)** Arbeiten Sie fokussiert und effizient mit verbesserter Leistung, sofortiger Codebereinigung und besseren Suchergebnissen.
* **[Zusammenarbeiten:](#collaborate)** Profitieren Sie von intuitiver Zusammenarbeit über einen Git-First-Workflow, Bearbeitung und Debuggen in Echtzeit sowie von Code Reviews direkt in Visual Studio.
* **[Debuggen:](#debug)** Heben Sie bestimmte Werte hervor, oder navigieren Sie zu diesen, optimieren Sie die Arbeitsspeichernutzung, und erstellen Sie automatische Momentaufnahmen von der Ausführung Ihrer Anwendung.

Eine ausführliche Liste aller Neuheiten in dieser Version finden Sie in den [Versionshinweisen](/visualstudio/releases/2019/release-notes/).

## <a name="develop"></a>Entwicklung

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie mit den neuen Features viel Zeit sparen können. <br><br>*Länge des Videos: 3,00 Minuten*

> [!VIDEO https://www.youtube.com/embed/n5sJ4EewKGk]

### <a name="improved-search"></a>Verbesserte Suche

Unsere neue Suche, die bisher als Schnellstart bezeichnet wurde, ist jetzt schneller und effektiver. Suchergebnisse werden jetzt dynamisch während der Eingabe angezeigt. Zudem können in den Suchergebnissen oft Tastenkombinationen für Befehle inbegriffen sein, sodass Sie diese für die zukünftige Verwendung leichter speichern können.

   ![Animation: Die neue Suche in Visual Studio 2019](media/vs-2019/new-search-feature.gif)

Mit der neuen unscharfen Suchlogik finden Sie die gewünschten Ergebnisse, auch wenn Sie sich vertippen. Egal, ob Sie nach Befehlen, Einstellungen, einer Dokumentation oder anderen nützlichen Funktionen suchen: Mithilfe des neuen Suchfeatures finden Sie noch unkomplizierter, wonach Sie suchen.

### <a name="refactorings"></a>Refactorings

In C# gibt es viele neue und sehr nützliche Refactorings, die das Organisieren Ihres Codes vereinfachen. Sie werden als Vorschläge in der Glühbirne angezeigt und enthalten Aktionen, um beispielsweise Member in die Schnittstelle oder die Basisklasse zu verschieben, Namespaces anzupassen, sodass Sie einer Ordnerstruktur entsprechen, oder um Foreach-Schleifen in LINQ-Abfragen zu konvertieren usw.

   ![Animation: Die neuen Refactorings in Visual Studio 2019](media/vs-2019/refactorings.gif)

Rufen Sie die Refactorings einfach auf, indem Sie **STRG+.** drücken und die Aktion auswählen, die Sie ausführen möchten.

### <a name="intellicode"></a>IntelliCode

[Visual Studio IntelliCode](/visualstudio/intellicode/) unterstützt Ihre Softwareentwicklung mithilfe von künstlicher Intelligenz (KI). IntelliCode trainiert über 2.000 Open Source-Projekte auf GitHub &mdash; jedes mit über 100 Sternen &mdash; zum Generieren von Empfehlungen.

![Animation: IntelliCode in Visual Studio 2019](media/vs-2019/IntelliCode.gif)

Im Folgenden werden einige Möglichkeiten aufgeführt, wie Sie mit Visual Studio IntelliCode Ihre Produktivität steigern können:

* Bereitstellen von kontextabhängigen Codevervollständigungen
* Hilfe für Entwickler, sich an die Muster und Konventionen ihres Teams zu halten
* Suche nach schwer auffindbaren Codeproblemen
* Schwerpunkt auf Code Reviews, indem die Aufmerksamkeit auf die wichtigen Bereiche gerichtet wird

Bei der ersten Vorschauversion von IntelliCode als Erweiterung für Visual Studio wurde zunächst nur C# unterstützt. Seit der **neuen Version 16.1** werden auch C# und XAML unterstützt. (Die Unterstützung für C++ und TypeScript und JavaScript befinden sich jedoch weiterhin in der Vorschau.)

Und bei Verwendung von C# können Sie jetzt auch ein benutzerdefiniertes Modell für Ihren eigenen Code trainieren.

Weitere Informationen zu IntelliCode finden Sie in den Blogbeiträgen [Announcing the general availability of IntelliCode plus a sneak peek](https://devblogs.microsoft.com/visualstudio/announcing-the-general-availability-of-intellicode-plus-a-sneak-peek/) (Ankündigung der allgemeinen Verfügbarkeit von IntelliCode und erster Einblick) und [Code more, scroll less with Visual Studio IntelliCode](https://devblogs.microsoft.com/visualstudio/code-more-scroll-less-with-visual-studio-intellicode/) (Mehr codieren, weniger scrollen mit Visual Studio IntelliCode).

### <a name="code-cleanup"></a>Codebereinigung

Neben einem neuen Integritätsindikator für Dokumente gibt es auch einen neuen Befehl für die Codebereinigung. Mit diesem neuen Befehl können Sie Warnungen und Vorschläge mit nur einem Knopfdruck ermitteln und anschließend beheben bzw. umsetzen.

Bei der Bereinigung wird der Code formatiert, und es werden sämtliche Codekorrekturen vorgenommen, die von [aktuellen Einstellungen](code-styles-and-code-cleanup.md) und [EDITORCONFIG-Dateien](create-portable-custom-editor-options.md) vorgeschlagen werden.

   ![Screenshot: das neue Steuerelement für die Codebereinigung in Visual Studio 2019](media/vs-2019/code-cleanup-profile.png)

Sie können auch Korrektursammlungen als Profil speichern. Wenn Sie z.B. einige spezielle Korrekturen haben, die Sie beim Programmieren häufig anwenden, und eine weitere umfangreiche Korrektursammlung, die vor einem Code Review angewendet wird, können Sie Profile für diese verschiedenen Aufgaben konfigurieren.

   ![Screenshot: das Steuerelement zum Konfigurieren der Codebereinigung in Visual Studio 2019](media/vs-2019/code-cleanup-profile-configure.png)

### <a name="per-monitor-aware-pma-rendering"></a>PMA-Rendering (PMA = Per-Monitor Aware)

Wenn Sie Monitore verwenden, die mit unterschiedlichen Anzeigeskalierungsfaktoren konfiguriert sind, oder eine Remoteverbindung mit einem Computer herstellen, bei dem die Anzeigeskalierungsfaktoren von denen auf Ihrem Hauptgerät abweichen, werden Sie vielleicht feststellen, dass Visual Studio unscharf aussieht oder bei der falschen Skalierung gerendert wird.

Seit der Veröffentlichung von Visual Studio 2019 ist Visual Studio eine PMA-fähige (per-monitor aware) Anwendung. Jetzt rendert Visual Studio unabhängig von den verwendeten Skalierungsfaktoren für die Anzeige ordnungsgemäß.

   ![PMA-Rendering (PMA = Per-Monitor Aware) in Visual Studio 2019](media/vs-2019/pma-dpi-scaling.png)

Weitere Informationen finden Sie im Blogbeitrag [Better multi-monitor experience with Visual Studio 2019 (Bessere Erfahrung mit mehreren Monitoren mit Visual Studio 2019)](https://devblogs.microsoft.com/visualstudio/a-better-multi-monitor-experience-with-visual-studio-2019/).

### <a name="test-explorer"></a>Test-Explorer

**Neu in Version 16.2:** Der Test-Explorer wurde aktualisiert. Große Testdatensätze können nun besser verarbeitet werden, das Filtern wurde vereinfacht, Befehle sind besser auffindbar, Wiedergabelisten werden als Registerkarten angezeigt, und es gibt anpassbare Spalten, mit denen Sie die angezeigten Testinformationen optimieren können.

   ![Screenshot: Verbesserungen an der Benutzeroberfläche des Test-Explorers](media/vs-2019/test-explorer-ui.png)

## <a name="collaborate"></a>Zusammenarbeiten

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie Probleme im Team lösen können. <br><br>*Länge des Videos: 4,22 Minuten*

> [!VIDEO https://www.youtube.com/embed/dKLJsiK1QU8]

### <a name="cloud-first-workflow"></a>Cloud im Workflow an erster Stelle

Wenn Sie Visual Studio 2019 öffnen, wird Ihnen u.a. das neue Startfenster auffallen.

   ![Screenshot: das neue Startfenster in Visual Studio 2019](media/vs-2019/start-window-dark.png)

Im Startfenster stehen mehrere Optionen zur Verfügung, um schnell zum Code zu gelangen. Die Option zum Klonen oder Auschecken von Code aus einem Repository wird nun als erste dargestellt.

   ![Animation: Git in Visual Studio 2019 nun an oberster Position](media/vs-2019/git-first.gif)

Im Startfenster gibt es außerdem Optionen zum Öffnen eines Projekts oder einer Projektmappe, zum Öffnen eines lokalen Ordners oder zum Erstellen eines neuen Projekts.

Weitere Informationen finden Sie im Blogbeitrag [Get to code: How we designed the new Visual Studio start window (Entwurf des neuen Visual Studio-Startfensters)](https://devblogs.microsoft.com/visualstudio/get-to-code-how-we-designed-the-new-visual-studio-start-window/).

### <a name="live-share"></a>Live Share

[Visual Studio Live Share:](https://visualstudio.microsoft.com/services/live-share/) ist ein Entwicklerdienst, mit dem Sie eine Codebasis und deren Kontext für ein anderes Teammitglied freigeben können und direkt in Visual Studio eine sofortige bidirektionale Kollaboration erhalten. Mithilfe von Live Share können Ihre Teammitglieder ohne Probleme und auf sichere Weise ein Projekt, das Sie für sie freigegeben haben, lesen, bearbeiten und debuggen sowie darin navigieren.

In Visual Studio 2019 ist dieser Dienst standardmäßig installiert.

![Animation: das Feature „Live Share“ für die Zusammenarbeit in Visual Studio 2019](media/vs-2019/live-share.gif)

Weitere Informationen finden Sie in den Blogbeiträgen [Visual Studio Live Share for real-time code reviews and interactive education (Visual Studio Live Share für Echtzeit-Code Reviews und interaktiven Unterricht)](https://devblogs.microsoft.com/visualstudio/visual-studio-live-share-for-real-time-code-reviews-and-interactive-education/) und [Live Share now included with Visual Studio 2019 (Live Share jetzt in Visual Studio 2019 verfügbar)](https://devblogs.microsoft.com/visualstudio/live-share-now-included-with-visual-studio-2019/).

### <a name="integrated-code-reviews"></a>Integrierte Code Reviews

Es wurde eine neue Erweiterung eingeführt, die Sie für die Verwendung mit Visual Studio 2019 herunterladen können. Mit dieser neuen Erweiterung können Sie Pull Requests Ihres Teams überprüfen, ausführen und sogar debuggen, ohne Visual Studio verlassen zu müssen. Code wird sowohl in GitHub- als auch in Azure DevOps-Repositorys unterstützt.

   ![Screenshot: das neue Startfenster in Visual Studio 2019](media/vs-2019/pr-experience.png)

Weitere Informationen finden Sie im Blogbeitrag [Code reviews using the Visual Studio Pull Requests extension](https://devblogs.microsoft.com/visualstudio/code-reviews-using-the-visual-studio-pull-requests-extension/) (Codeprüfungen mit der Visual Studio Pull Requests-Erweiterung).

## <a name="debug"></a>Debug

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie beim Debuggen einen Fehler präzise einkreisen können. <br><br>*Länge des Videos: 3,54 Minuten*

> [!VIDEO https://www.youtube.com/embed/hr72Fs8n_9c]

### <a name="performance-gains"></a>Leistungsverbesserungen

Wir haben die Datenbreakpoints, die ursprünglich nur für C++ ausgerichtet waren, nun auch für .NET Core-Anwendungen angepasst.

   ![Animation: Datenbreakpoints für das Debuggen in Visual Studio 2019](media/vs-2019/debug-data-breakpoints.gif)

Datenbreakpoints können nun also unabhängig davon, ob Sie in C++ oder in .NET Core programmieren, eine gute Alternative zu regulären Breakpoints darstellen. Datenbreakpoints eignen sich auch ideal für Szenarios wie für die Suche nach der Position, an der ein globales Objekt bearbeitet, hinzugefügt oder aus einer Liste entfernt wird.

Wenn Sie in C++ große Anwendungen entwickeln, hat Visual Studio 2019 nun außerdem Symbole lokal verfügbar gemacht, mithilfe derer Sie diese Anwendungen debuggen können, ohne dass es zu arbeitsspeicherbezogenen Problemen kommt.

### <a name="search-while-debugging"></a>Suche während des Debuggens

Sie haben sicher schon mal im Überwachungsfenster unter einer Reihe von Werten nach einer Zeichenfolge gesucht. In Visual Studio 2019 haben wir die Suche in den Fenstern „Überwachung“, „Lokal“ und „Auto“ hinzugefügt, damit Sie die Objekte und Werte, nach denen Sie suchen, besser finden können.

   ![Animation: das Fenster für die Suche während des Debuggens in Visual Studio 2019](media/vs-2019/debug-window-search.gif)

Sie können auch formatieren, wie ein Wert in den Fenstern „Überwachung“, „Lokal“ und „Auto“ angezeigt wird.  Doppelklicken Sie in einem Fenster auf eines der Elemente, und fügen Sie ein Komma („,“) hinzu, um auf die Dropdown-Liste der möglichen Formatbezeichner Zugriff zu haben, von denen jeder eine Beschreibung des erwarteten Ergebnisses enthält.

   ![Das neue Überwachungsfenster und das Feature zur Wertformatierung in Visual Studio 2019](media/search-watch-window.png)

Weitere Informationen finden Sie im Blogbeitrag [Enhanced in Visual Studio 2019: Search for Objects and Properties in the Watch, Autos, and Locals Windows (Erweiterungen in Visual Studio 2019: Suchen nach Objekten und Eigenschaften in den Fenstern „Überwachen“, „Auto“ und „Lokal“)](https://devblogs.microsoft.com/visualstudio/enhanced-in-visual-studio-2019-search-for-objects-and-properties-in-the-watch-autos-and-locals-windows/).

### <a name="snapshot-debugger"></a>Momentaufnahmedebugger

Sie können eine Momentaufnahme der Ausführung Ihrer App in der Cloud abrufen, um genau zu sehen, was gerade geschieht. (Dieses Feature ist nur in Visual Studio Enterprise verfügbar.)

   ![Animation: der Momentaufnahmedebugger in Visual Studio 2019 Enterprise](media/vs-2019/snapshot-debugger.gif)

ASP.NET Core-Anwendungen und Desktopanwendungen, die auf einem virtuellen Azure Computer ausgeführt werden, werden nun unterstützt. Außerdem werden nun Anwendungen unterstützt, die in Azure Kubernetes Service ausgeführt werden. Der Momentaufnahmedebugger kann Sie dabei unterstützen, die Zeit zum Beheben von Fehlern, die in Produktionsumgebungen auftreten, erheblich zu reduzieren.

Weitere Informationen finden Sie auf der Seite [Debuggen von aktiven ASP.NET Azure-Apps mit dem Momentaufnahmedebugger](../debugger/debug-live-azure-applications.md) und in dem Blogbeitrag [Introducing Time Travel Debugging for Visual Studio Enterprise 2019](https://devblogs.microsoft.com/visualstudio/introducing-time-travel-debugging-for-visual-studio-enterprise-2019/) (Einführung in Time Travel Debugging für Visual Studio Enterprise 2019).

### <a name="microsoft-edge-insider-support"></a>Unterstützung von Microsoft Edge Insider

**Neu in Version 16.2:** Sie können einen Breakpoint in einer JavaScript-Anwendung festlegen und eine Debugsitzung starten, indem Sie den Browser [Microsoft Edge Insider](https://www.microsoftedgeinsider.com/) verwenden. Daraufhin öffnet Visual Studio ein neues Browserfenster mit aktiviertem Debuggen, das Sie dann zum Durchlaufen der JavaScript-Anwendung in Visual Studio verwenden können.

   ![Screenshot: JavaScript-Code, der im Browser gerendert wird](media/vs-2019/edge-chromium-breakpoint.png)

## <a name="whats-next"></a>Ausblick

Wir aktualisieren Visual Studio 2019 häufig mit neuen Features, die die Entwicklung immer weiter verbessern. Weitere Informationen zu unseren aktuellen Innovationen finden Sie im [Visual Studio Blog](https://devblogs.microsoft.com/visualstudio/). Was wir zurzeit in der Vorschau veröffentlicht haben, können Sie den [Visual Studio 2019 Preview Release Notes](/visualstudio/releases/2019/release-notes-preview/) (Anmerkungen zu Vorschauversionen in Visual Studio 2019) entnehmen.

Sie möchten mehr über unsere Pläne für Visual Studio 2019 erfahren? Weitere Informationen finden Sie in der [Visual Studio-Roadmap](/visualstudio/productinfo/vs-roadmap/).

## <a name="give-us-feedback"></a>Geben Sie uns Feedback

Warum sollten Sie dem Visual Studio-Team ein Feedback senden? Weil wir das Feedback unserer Kunden ernst nehmen. Es gibt den Anstoß zu vielen unserer Initiativen.

* Wenn Sie einen Vorschlag zur Verbesserung von Visual Studio haben, können Sie diesen mit dem Tool [Funktion vorschlagen](suggest-a-feature.md) einreichen.

* Wenn bei Ihnen Hängen, Abstürze oder andere Leistungsprobleme auftreten, können Sie die Schritte zur Reproduktion und unterstützende Dateien auf einfache Weise mithilfe des Tools [Problem melden](how-to-report-a-problem-with-visual-studio.md) mit uns teilen.

## <a name="see-also"></a>Siehe auch

* [Visual Studio 2019 – Versionshinweise](/visualstudio/releases/2019/release-notes/)
* [Neuigkeiten im Visual Studio 2019 SDK](../extensibility/whats-new-visual-studio-2019-sdk.md)
* [Versionshinweise für Visual Studio 2019 für Mac](/visualstudio/releasenotes/vs2019-mac-relnotes/)
* [Microsoft Build 2019-Konferenz](https://www.microsoft.com/build)
* [Microsoft Connect(); 2018 conference (Microsoft Connect(); 2018-Konferenz)](https://www.microsoft.com/connectevent)
