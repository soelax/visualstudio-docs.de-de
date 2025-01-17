---
title: 'Visual Studio für Mac: Überblick'
description: Visual Studio für Mac bietet eine integrierte Entwicklungsumgebung zum Erstellen von .NET-Anwendungen unter macOS. Dazu gehören ASP.NET Core-Websites und Xamarin-Projekte für iOS, Android, Mac und Xamarin.Forms.
author: asb3993
ms.author: amburns
ms.date: 04/02/2019
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.custom: video
ms.openlocfilehash: aabb6b575edb68f3e72cad06f2497b8176e950fe
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2019
ms.locfileid: "67691501"
---
# <a name="visual-studio-2019-for-mac-tour"></a>Visual Studio 2019 für Mac: Überblick

Visual Studio für Mac ist eine _integrierte Entwicklungsumgebung_ für .NET auf dem Mac, die Sie verwenden können, um Code erst zu bearbeiten, zu debuggen und zu kompilieren und um anschließend eine App zu veröffentlichen. Neben erwarteten Features wie einem Standard-Editor und -Debugger enthält Visual Studio für Mac Compiler, Codevervollständigungstools, grafische Designer und die Quellcodeverwaltung zur Erleichterung der Entwicklung von Software.

Visual Studio für Mac unterstützt viele der Dateitypen, die auch vom entsprechenden Windows-Pendant unterstützt werden (z.B. `.csproj`-, `.fsproj`- oder `.sln`-Dateien), sowie Features wie EditorConfig. Sie können also die integrierte Entwicklungsumgebung verwenden, die Ihren Anforderungen am besten entspricht.
Das Erstellen, Öffnen und Entwickeln einer Anwendung ist eine vertraute Erfahrung für jeden, der schon einmal Visual Studio unter Windows verwendet hat. Zusätzlich werden auch in Visual Studio für Mac die leistungsstarken Tools eingesetzt, die sein Windows-Pendant zu einer derartig leistungsfähigen IDE machen. Die Roslyn-Compilerplattform wird für das Refactoring und IntelliSense verwendet. Das Projektsystem und die Build-Engine verwenden MSBuild. Der Quell-Editor unterstützt TextMate-Bündel. Das Produkt verwendet die gleichen Debugger-Engines für Xamarin- und .NET Core-Apps und die gleichen Designer für Xamarin.iOS und Xamarin.Android.

## <a name="what-can-i-do-in-visual-studio-for-mac"></a>Verwendungsweise von Visual Studio für Mac

Visual Studio für Mac unterstützt die folgenden Entwicklungstypen:

- ASP.NET Core-Webanwendungen mit C#, F# und Unterstützung von Razor-Seiten, JavaScript und TypeScript
- .NET Core-Konsolenanwendungen mit C# oder F#
- Plattformübergreifende Unity-Spiele und -Anwendungen mit C#
- Android-, iOS-, tvOS- und watchOS-Anwendungen in Xamarin mit C# oder F# und XAML
- Cocoa-Desktop-Apps in C# oder F#

In diesem Artikel werden verschiedene Bereiche von Visual Studio für Mac thematisiert, um einen Einblick in einige der Features zu geben, die es zu einem leistungsstarken Tool zur Erstellung dieser Anwendungen machen.

## <a name="ide-tour"></a>IDE-Überblick

Visual Studio für Mac ist in verschiedenen Abschnitten zum Verwalten von Anwendungsdateien und -einstellungen und zum Erstellen und Debuggen von Code organisiert.

## <a name="start-window"></a>Startfenster

Wenn Sie Visual Studio 2019 für Mac starten, wird für neue Benutzer ein Anmeldefenster angezeigt. Melden Sie sich mit Ihrem Microsoft-Konto an, um eine kostenpflichtige Lizenz (sofern Sie eine besitzen) zu aktivieren oder eine Verknüpfung zu Azure-Abonnements herzustellen. Sie können auf **Überspringen** drücken und sich später über das Menüelement **Visual Studio > Anmelden** anmelden.

![Anmelden bei Ihrem Microsoft-Konto](media/ide-tour-2019-start-signin.png)

Angemeldeten Benutzern wird das neue _Startfenster_ angezeigt, in dem eine Liste der zuletzt geöffneten Projekte dargestellt ist, sowie Schaltflächen, mit denen ein vorhandenes Projekt geöffnet oder ein neues erstellt werden kann.

![Wählen Sie zwischen aktuellen Projekten aus, oder erstellen Sie ein neues Element.](media/ide-tour-2019-start-projects.png)

## <a name="solutions-and-projects"></a>Projektmappen und Projekte

Das folgende Bild zeigt Visual Studio für Mac mit einer geladenen Anwendung:

![Visual Studio für Mac mit einer geladenen Anwendung](media/ide-tour-image17.png)

In den folgenden Abschnitten wird ein Überblick über die Hauptbereich von Visual Studio für Mac gegeben.

## <a name="solution-pad"></a>Projektmappenpad

Das Projektmappenpad organisiert die Projekte in einer Projektmappe:

![Im Projektmappenpad organisierte Projekte](media/ide-tour-image18.png)

Hier werden Dateien für den Quellcode, Ressourcen, Benutzeroberflächen und Abhängigkeiten in plattformspezifische Projekte organisiert.

Weitere Informationen zum Verwenden von Projekten und Projektmappen in Visual Studio für Mac finden Sie im Artikel [Projektmappen und Projekte](/visualstudio/mac/projects-and-solutions).

## <a name="assembly-references"></a>Assemblyverweise

Assemblyverweise für jedes Projekt stehen im Ordner „Verweise“ zu Verfügung:

![Ordner „Verweise“ im Projektmappenpad](media/ide-tour-image19.png)

Sie können mit dem Dialogfeld **Verweise bearbeiten** zusätzliche Verweise hinzufügen. Dieses kann durch Doppelklicken auf den Ordner „Verweise“ angezeigt werden, oder indem Sie auf **Verweise bearbeiten** in den Kontextmenüaktionen klicken:

![Dialogfeld „Verweise bearbeiten“](media/ide-tour-image20.png)

Weitere Informationen zum Verwenden von Verweisen in Visual Studio für Mac finden Sie im Artikel [Verwalten von Verweisen in einem Projekt](/visualstudio/mac/managing-references-in-a-project).

## <a name="dependencies--packages"></a>Abhängigkeiten/Pakete

Alle externen Abhängigkeiten, die in Ihrer App verwendet werden, werden in dem Ordner „Abhängigkeiten“ oder in dem Ordner „Pakete“ gespeichert, je nachdem, ob es sich um ein .NET Core- oder Xamarin.iOS- bzw. Xamarin.Android-Projekt handelt. Diese werden in der Regel in NuGet-Form bereitgestellt.

NuGet ist der beliebteste Paket-Manager für die .NET-Entwicklung. Mit der NuGet-Unterstützung von Visual Studio können Sie leicht nach Paketen suchen und diese in Ihrer Anwendung einem Projekt hinzufügen.

Um Ihrer Anwendung eine Abhängigkeit hinzuzufügen, klicken Sie mit der rechten Maustaste auf den Ordner Abhängigkeiten/Pakete und dann auf **Pakete hinzufügen**:

![Hinzufügen eines NuGet-Pakets](media/ide-tour-image21.png)

Informationen zum Verwenden eines NuGet-Pakets in einer Anwendung finden Sie im Artikel [Einschließen eines NuGet-Pakets in Ihr Projekt](/visualstudio/mac/nuget-walkthrough).

## <a name="refactoring"></a>Umgestaltung

Visual Studio für Mac bietet zwei praktische Möglichkeiten zum Umgestalten Ihres Codes: Kontextaktionen und Quellanalysen. Weitere Informationen finden Sie im Artikel [Umgestaltung](/visualstudio/mac/refactoring).

## <a name="debugging"></a>Debuggen

Visual Studio für Mac besitzt einen nativen Debugger, der das Debuggen für Xamarin.iOS-, Xamarin.Mac- und Xamarin.Android-Anwendungen unterstützt. Visual Studio für Mac verwendet den Soft-Debugger von Mono, der in die Mono-Laufzeit integriert wird und es Visual Studio für Mac ermöglicht, verwalteten Code für alle Plattformen zu debuggen. Weitere Informationen zum Debuggen finden Sie im Artikel [Debuggen mit Xamarin](/visualstudio/mac/debugging).

Der Debugger enthält umfangreiche Schnellansichten für besondere Typen wie Zeichenfolgen, Farben und URLs sowie Größen, Koordinaten und Bézierkurven.

Weitere Informationen zu den Datenschnellansichten des Debuggers finden Sie im Artikel [Datenvisualisierungen](/visualstudio/mac/data-visualizations).

## <a name="version-control"></a>Versionskontrolle

Visual Studio für Mac kann in die Quellcodeverwaltungs-Systeme Git und Subversion integriert werden. Projekte unter Quellcodeverwaltung werden mit dem Branch bezeichnet, der neben dem Namen der Projektmappe angezeigt wird:

![Branchname, der ein Projekt unter Quellcodeverwaltung angibt](media/ide-tour-image22.png)

Die Symbole von Dateien mit nicht committeten Änderungen sind im Projektmappenbereich mit einer Anmerkung versehen, wie in der folgenden Abbildung dargestellt:

![Ausgecheckte Dateien im Projektmappenpad](media/ide-tour-image23.png)

Weitere Informationen zum Verwenden der Versionskontrolle in Visual Studio finden Sie im Artikel [Versionskontrolle](/visualstudio/mac/version-control).

## <a name="next-steps"></a>Nächste Schritte

- [Installieren von Visual Studio für Mac](installation.md)
- [Überprüfen der verfügbaren Workloads](workloads.md)

## <a name="related-video"></a>Zugehörige Videos

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Overview/player]

## <a name="see-also"></a>Siehe auch

- [Visual Studio-IDE (unter Windows)](/visualstudio/ide/visual-studio-ide)
