---
title: Befehlszeilenoptionen für VSTest.Console.exe
ms.date: 07/12/2018
ms.topic: reference
helpviewer_keywords:
- vstest.console.exe
- command-line tests
ms.author: gewarren
author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 147ec9096be430d0bc81be65fdf68f927c0f3dac
ms.sourcegitcommit: 044bb54cb4552c8f4651feb11d62e52726117e75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661940"
---
# <a name="vstestconsoleexe-command-line-options"></a>Befehlszeilenoptionen für VSTest.Console.exe

*VSTest.Console.exe* ist das Befehlszeilentool für die Ausführung von Tests. Sie können in der Befehlszeile verschiedene Optionen in beliebiger Reihenfolge angeben. Diese Optionen werden unter [Allgemeine Befehlszeilenoptionen](#general-command-line-options) aufgeführt.

> [!NOTE]
> Der MSTest-Adapter in Visual Studio funktioniert aus Kompatibilitätsgründen auch im Legacymodus (entspricht dem Ausführen von Tests mit *mstest.exe*). Im Legacymodus kann er die TestCaseFilter-Funktion nicht nutzen. Der Adapter kann in den Legacymodus wechseln, wenn eine *TESTSETTINGS*-Datei angegeben wird, **forcelegacymode** in einer *RUNSETTINGS*-Datei auf **TRUE** festgelegt ist oder Attribute wie **HostType** verwendet werden.
>
> Sie müssen *VSTest.Console.exe* für die Durchführung automatisierter Tests auf einem auf der ARM-Architektur basierenden Computer verwenden.

## <a name="general-command-line-options"></a>Allgemeine Befehlszeilenoptionen

In der folgenden Tabelle werden sämtliche Optionen für *VSTest.Console.exe* mit einer kurzen Beschreibung aufgeführt. Durch Eingabe von `VSTest.Console/?` in eine Befehlszeile wird eine ähnliche Zusammenfassung ausgegeben.

| Option | BESCHREIBUNG |
|---|---|
|**[*Testdateinamen*]**|Führt Tests auf Grundlage der angegebenen Dateien aus. Trennt mehrere Testdateinamen durch Leerzeichen.<br />Beispiele: `mytestproject.dll`, `mytestproject.dll myothertestproject.exe`|
|**/Settings: [*Dateiname*]**|Führen Sie Tests mit zusätzlichen Einstellungen wie Datensammlern aus.<br />Ein Beispiel: `/Settings:Local.RunSettings`|
|**/Tests: [*Testname*]**|Führt Tests aus, die mit den eingegebenen Werten übereinstimmen. Um mehrere Werte bereitzustellen, trennen Sie diese durch Kommas.<br />Ein Beispiel: `/Tests:TestMethod1,testMethod2`<br />Die Befehlszeilenoption **/Tests** kann nicht zusammen mit der Befehlszeilenoption **/TestCaseFilter** verwendet werden.|
|**/Parallel**|Gibt an, dass die Tests parallel ausgeführt werden. Standardmäßig können alle verfügbaren Kerne auf dem Computer verwendet werden. Die Anzahl der zu verwendenden Kerne kann mithilfe einer Einstellungsdatei konfiguriert werden.|
|**/Enablecodecoverage**|Aktiviert den CodeCoverage-Datendiagnoseadapter im Testlauf.<br />Die Standardeinstellungen werden verwendet, wenn keine Einstellungsdatei angegeben wurde.|
|**/InIsolation**|Führt die Tests in einem isolierten Prozess aus.<br />Durch diese Isolation ist die Wahrscheinlichkeit, dass der *vstest.console.exe*-Prozess bei Testfehlern beendet wird, weniger hoch, die Tests werden jedoch möglicherweise langsamer ausgeführt.|
|**/UseVsixExtensions**|Durch diese Option werden in dem *vstest.console.exe*-Prozess die VSIX-Erweiterungen verwendet oder übersprungen, die im Testlauf (ggf.) installiert wurden.<br />Diese Option ist veraltet. Ab der nächsten Hauptversion von Visual Studio ist diese Option möglicherweise nicht mehr verfügbar. Fahren Sie mit der Verarbeitung der Erweiterungen fort, die in Form eines NuGet-Pakets verfügbar gemacht wurden.<br />Ein Beispiel: `/UseVsixExtensions:true`|
|**/TestAdapterPath:[*Pfad*]**|Erzwingt, dass der *vstest.console.exe*-Prozess im Testlauf (ggf.) benutzerdefinierte Testadapter aus einem angegebenen Pfad verwendet.<br />Ein Beispiel: `/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[*Plattformtyp*]**|Zielplattformarchitektur für die Testausführung.<br />Gültige Werte sind x86, x64 und ARM.|
|**/Framework: [*Frameworkversion*]**|.NET-Zielversion, die für die Testausführung verwendet werden soll.<br />Gültige Werte sind Framework35, Framework40, Framework45 und FrameworkUap10.<br />Wenn als Zielframework **Framework35** angegeben ist, werden die Tests in CLR 4.0 im „Kompatibilitätsmodus“ ausgeführt.<br />Ein Beispiel: `/Framework:framework40`|
|**/TestCaseFilter:[*Ausdruck*]**|Führt Tests aus, die mit dem angegebenen Ausdruck übereinstimmen.<br /><Expression\> ist vom Format <property\>=<value\>[\|<Expression\>].<br />Ein Beispiel: `/TestCaseFilter:"Priority=1"`<br />Ein Beispiel: `/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />Die Befehlszeilenoption **/TestsCaseFilter** kann nicht zusammen mit der Befehlszeilenoption **/Tests** verwendet werden. <br />Informationen zum Erstellen und Verwenden von Ausdrücken finden Sie unter [TestCase-Filter](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md).|
|**/?**|Zeigt Nutzungsinformationen an.|
|**/Logger:[*uri/friendlyname*]**|Geben Sie eine Protokollierung für die Testergebnisse an.<br />Beispiel: Verwenden Sie zum Protokollieren von Ergebnissen in einer Visual Studio-Testergebnisdatei (TRX) **/Logger:trx**.<br />Beispiel: Verwenden Sie TfsPublisher zum Veröffentlichen von Testergebnissen in Team Foundation Server:<br />**/logger:TfsPublisher;**<br />**Collection=<Projekt-URL\>;**<br />**BuildName=<Buildname\>;**<br />**TeamProject=<Projektname\>;**<br />**[;Platform=\<Standardwert: Any CPU>]**<br />**[;Flavor=\<Standardwert: Debug>]**<br />**[;RunTitle=<title\>]**|
|**/ListTests:[*Dateiname*]**|Listet gefundene Tests aus dem angegebenen Testcontainer auf.|
|**/ListDiscoverers**|Listet alle installierten Test-Discoverer auf.|
|**/ListExecutors**|Listet alle installierten Test-Executors auf.|
|**/ListLoggers**|Listet alle installierten Testprotokollierungen auf.|
|**/ListSettingsProviders**|Listet alle installierten Testeinstellungsanbieter auf.|
|**/Blame**|Verfolgt die Tests während ihrer Ausführung und verfolgt, ob der Test-Hostprozess abstürzt, gibt die Testnamen in der Reihenfolge ihrer Ausführung einschließlich des spezifischen Tests aus, der zum Zeitpunkt des Absturzes ausgeführt wurde. Durch diese Ausgabe kann der betreffende Test besser isoliert und weiter diagnostiziert werden. [Weitere Informationen](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md).|
|**/Diag:[*Dateiname*]**|Schreibt Protokolle zur Diagnoseablaufverfolgung für die angegebene Datei.|
|**/ResultsDirectory:[*path*]**|Das Verzeichnis mit den Testergebnissen wird am angegebenen Pfad erstellt, falls es noch nicht vorhanden ist.<br />Ein Beispiel: `/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*parentProcessId*]**|Prozess-ID des übergeordneten Prozesses, der für den Start des aktuellen Prozesses verantwortlich ist.|
|**/Port:[*port*]**|Der Port für die Socketverbindung und den Empfang der Ereignismeldungen.|
|**/Collect:[*dataCollector friendlyName*]**|Aktiviert den Datensammler für den Testlauf. [Weitere Informationen](https://aka.ms/vstest-collect).|

> [!TIP]
> Bei den Optionen und Werten muss die Groß-/Kleinschreibung nicht beachtet werden.

## <a name="examples"></a>Beispiele

Die Syntax für die Ausführung von *VSTest.Console.exe* lautet wie folgt:

`Vstest.console.exe [TestFileNames] [Options]`

Mit dem folgenden Befehl wird *VSTest.Console.exe* für die Bibliothek **myTestProject.dll** ausgeführt:

```cmd
vstest.console.exe myTestProject.dll
```

Mit dem folgenden Befehl wird *VSTest.Console.exe* mit mehreren Testdateien ausgeführt. Trennt Testdateinamen durch Leerzeichen:

```cmd
Vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

Mit dem folgenden Befehl wird *VSTest.Console.exe* mit verschiedenen Optionen ausgeführt. Die Tests werden in der Datei *myTestFile.dll* in einem isolierten Prozess ausgeführt. Zudem werden Einstellungen verwendet, die in der Datei *Local.RunSettings* angegeben sind. Darüber hinaus werden mit dem Befehl nur Tests ausgeführt, die mit „Priorität = 1“ gekennzeichnet sind. Die Ergebnisse werden in einer *TRX*-Datei protokolliert.

```cmd
vstest.console.exe  myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```
