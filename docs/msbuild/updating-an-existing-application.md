---
title: Aktualisieren einer vorhandenen Anwendung für MSBuild 15 | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf1c226fceff6ea17a7f83d750a93d6406a31c7d
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263737"
---
# <a name="update-an-existing-application-for-msbuild-15"></a>Aktualisieren einer vorhandenen Anwendung für MSBuild 15

Vor Version 15.0 von MSBuild wurde MSBuild aus dem globalen Assemblycache (GAC) geladen und MSBuild-Erweiterungen wurden in der Registrierung installiert. Dadurch wurde sichergestellt, dass alle Anwendungen die gleiche Version von MSBuild verwenden und auf die gleichen Toolsets zugreifen. Jedoch wurden auch parallele Installationen von verschiedenen Versionen von Visual Studio dadurch verhindert.

Um schnellere, kleinere und parallele Installationen zu unterstützen, platzieren Visual Studio 2017 und höhere Versionen MSBuild nicht mehr im GAC und ändern nicht mehr die Registrierung. Das bedeutet jedoch auch, dass Anwendungen, die die MSBuild-API zum Auswerten oder Erstellen von Projekten verwenden sollen, nicht implizit auf der Installation von Visual Studio basieren können.

## <a name="use-msbuild-from-visual-studio"></a>Verwenden von MSBuild in Visual Studio

Laden Sie MSBuild-Assemblys aus Visual Studio, und verwenden Sie die in Visual Studio verfügbaren SDKs, um sicherzustellen, dass programmgesteuerte Builds Ihrer Anwendung mit denen in Visual Studio oder *MSBuild.exe* übereinstimmen. Das NuGet-Paket „Microsoft.Build.Locator“ optimiert diesen Prozess.

## <a name="use-microsoftbuildlocator"></a>Verwenden von „Microsoft.Build.Locator“

Wenn Sie *Microsoft.Build.Locator.dll* mit Ihrer Anwendung weiterverteilen, müssen Sie keine anderen MSBuild-Assemblys verteilen.

Damit ein Projekt für die Verwendung von MSBuild 15 und der Locator-API aktualisiert werden kann, sind einige Änderungen in Ihrem Projekt erforderlich (unten beschrieben). Ein Beispiel dieser zum Aktualisieren eines Projekts erforderlichen Änderungen finden Sie in [den Commits für ein Beispielprojekt im MSBuildLocator-Repository](https://github.com/Microsoft/MSBuildLocator/commits/example-updating-to-msbuild-15).

### <a name="change-msbuild-references"></a>Ändern von MSBuild-Verweisen

Um sicherzustellen, dass MSBuild aus einem zentralen Speicherort geladen wird, dürfen Sie die Assemblys nicht mit Ihrer Anwendung verteilen.

Der Mechanismus zum Ändern Ihres Projekts, um das Laden aus einem zentralen Speicherort zu vermeiden, hängt davon ab, wie Sie auf MSBuild verweisen.

#### <a name="use-nuget-packages-preferred"></a>Verwenden von NuGet-Paketen (bevorzugt)

Diese Anweisungen setzen voraus, dass Sie [NuGet-Verweise im PackageReference-Stil](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files) verwenden.

Ändern Sie Ihre Projektdatei(en) so, dass sie mit den NuGet-Paketen auf MSBuild-Assemblys verweisen. Teilen Sie NuGet durch Angabe von `ExcludeAssets=runtime` mit, dass die Assemblys nur zur Buildzeit benötigt werden und nicht in das Ausgabeverzeichnis kopiert werden sollen.

Die Haupt- und Nebenversionen der MSBuild-Pakete müssen geringer als oder gleich der frühesten Version von Visual Studio sein, die Sie unterstützen möchten. Wenn Sie Visual Studio 2017 und höhere Versionen unterstützen möchten, verweisen Sie auf die Paketversion `15.1.548`.

Sie können z.B. das folgende XML verwenden:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.Build" Version="15.1.548" ExcludeAssets="runtime" />
  <PackageReference Include="Microsoft.Build.Utilities.Core" Version="15.1.548" ExcludeAssets="runtime" />
</ItemGroup>
```

#### <a name="use-extension-assemblies"></a>Verwenden von Erweiterungsassemblys

Wenn Sie NuGet-Pakete nicht verwenden können, können Sie auf MSBuild-Assemblys verweisen, die mit Visual Studio verteilt werden. Wenn Sie direkt auf MSBuild verweisen, stellen Sie sicher, dass es nicht in Ihr Ausgabeverzeichnis kopiert wird, indem Sie `Copy Local` auf `False` festlegen. In der Projektdatei entspricht diese Einstellung folgendem Code:

```xml
    <Reference Include="Microsoft.Build, Version=15.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
      <Private>False</Private>
    </Reference>
```

#### <a name="binding-redirects"></a>Bindungsumleitungen

Verweisen Sie auf das Paket „Microsoft.Build.Locator“, um sicherzustellen, dass Ihre Anwendung automatisch die erforderlichen Bindungsumleitungen aller Versionen von MSBuild-Assemblys auf Version `15.1.0.0` verwendet.

### <a name="ensure-output-is-clean"></a>Sicherstellen einer sauberen Ausgabe

Erstellen Sie Ihr Projekt, und überprüfen Sie das Ausgabeverzeichnis, um sicherzustellen, dass es keine *Microsoft.Build.\*.dll*-Assemblys enthält (außer der im nächsten Schritt hinzugefügten *Microsoft.Build.Locator.dll*).

### <a name="add-package-reference-for-microsoftbuildlocator"></a>Hinzufügen eines Paketverweises für Microsoft.Build.Locator

Fügen Sie einen NuGet-Paketverweis für [Microsoft.Build.Locator](https://www.nuget.org/packages/Microsoft.Build.Locator/) hinzu.

```xml
    <PackageReference Include="Microsoft.Build.Locator">
      <Version>1.1.2</Version>
    </PackageReference>
```

Legen Sie keine `ExcludeAssets=runtime` für das Microsoft.Build.Locator-Paket fest.

### <a name="register-instance-before-calling-msbuild"></a>Registrieren der Instanz vor dem Aufrufen von MSBuild

Fügen Sie einen Aufruf der Locator-API hinzu, bevor Sie eine Methode aufrufen, die MSBuild verwendet.

Die einfachste Möglichkeit, den Aufruf der Locator-API hinzuzufügen, ist, einen Aufruf

```csharp
MSBuildLocator.RegisterDefaults();
```

in Ihrem Code für den Anwendungsstart hinzuzufügen.

Sie können ein Ergebnis von `MSBuildLocator.QueryVisualStudioInstances()` zum manuellen Weitergeben an `MSBuildLocator.RegisterInstance()` auswählen, um eine umfassendere Steuerung des Ladens von MSBuild zu ermöglichen. In der Regel ist das jedoch nicht notwendig.
