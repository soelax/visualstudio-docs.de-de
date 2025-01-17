---
title: Befehlszeilenargumente für den Hilfeinhalts-Manager
ms.date: 11/01/2017
ms.topic: reference
ms.assetid: 3aa9890a-1147-42ba-adea-17935d184038
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 09b63b3d01329a5fe243d100eeea921299061433
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825087"
---
# <a name="command-line-arguments-for-the-help-content-manager"></a>Befehlszeilenargumente für den Hilfeinhalts-Manager

Sie können angeben, wie lokale Hilfeinhalte bereitgestellt und verwaltet werden sollen. Verwenden Sie dazu Befehlszeilenargumente für den Hilfeinhalts-Manager (*HlpCtntMgr.exe*). Sie müssen Skripts für dieses Befehlszeilentool mit Administratorberechtigungen ausführen. Die Skripts können nicht als Dienst ausgeführt werden. Mit diesem Tool können Sie folgende Aufgaben ausführen:

- Hinzufügen oder Aktualisieren lokaler Hilfeinhalte von Datenträgern oder aus der Cloud

- Entfernen lokaler Hilfeinhalte

- Verschieben des lokalen Hilfeinhaltsspeichers

- Automatisches Hinzufügen, Aktualisieren, Entfernen oder Verschieben lokaler Hilfeinhalte

Syntax:

```cmd
HlpCtntmgr.exe /operation Value /catalogname CatalogName /locale Locale /sourceuri InstallationPoint
```

Beispiel:

```cmd
hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us /sourceuri d:\productDocumentation\HelpContentSetup.msha
```

## <a name="switches-and-arguments"></a>Parameter und Argumente

In der folgenden Tabelle werden die Schalter und die Argumente definiert, die Sie für das Befehlszeilentool für den Hilfeinhalts-Manager verwenden können:

|Schalter|Erforderlich?|Argumente|
|------------|---------------|---------------|
|/operation|Ja|-   **Install** – Fügt dem lokalen Inhaltsspeicher Bücher aus der angegebenen Installationsquelle hinzu<br />     Dieser Schalter erfordert das Argument /booklist bzw. /sourceURI oder beide. Wenn Sie das Argument /sourceURI nicht angeben, wird der standardmäßige Visual Studio-URI als Installationsquelle verwendet. Ohne Angabe des Arguments /booklist werden alle Bücher unter /sourceUri installiert.<br />-   **Uninstall** – Entfernt die angegebenen Bücher aus dem lokalen Inhaltsspeicher<br />     Dieser Schalter erfordert das Argument /booklist oder /sourceURI.  Wenn Sie das Argument /sourceURI angeben, werden alle Bücher entfernt, und das Argument /booklist wird ignoriert.<br />-   **Move** – Verschiebt den lokalen Speicher zum angegebenen Pfad. Der lokale Standardspeicherpfad wird unter *%ProgramData%* als Verzeichnis festgelegt.<br />     Dieser Schalter erfordert die Argumente /locationPath und /catalogName. Fehlermeldungen werden im Ereignisprotokoll protokolliert, wenn Sie einen Pfad angeben, der nicht gültig ist, oder wenn der Speicherplatz im Laufwerk nicht ausreicht.<br />-   **Refresh** – Aktualisiert Themen, die nach der Installation bzw. der letzten Aktualisierung geändert wurden<br />     Dieser Schalter erfordert das Argument /sourceURI.|
|/catalogName|Ja|Gibt den Namen des Inhaltskatalogs an.|
|/locale|Nein|Gibt das Produktgebietsschema an, das zum Anzeigen und Verwalten der Inhalte für die aktuelle Instanz von Help Viewer verwendet wird. Geben Sie beispielsweise `EN-US` für Englisch (USA) an.<br /><br /> Wenn Sie kein Gebietsschema angeben, wird das Gebietsschema des Betriebssystems verwendet. Wenn dieses Gebietsschema nicht ermittelt werden kann, wird `EN-US` verwendet.<br /><br /> Wenn Sie ein ungültiges Gebietsschema angeben, wird im Ereignisprotokoll eine Fehlermeldung protokolliert.|
|/e|Nein|Weitet die Rechte des Hilfeinhalts-Managers auf Administratorrechte aus, wenn der aktuelle Benutzer über Administratoranmeldeinformationen verfügt.|
|/sourceURI|Nein|Gibt die URL an, über die Inhalt installiert wurde (Service-API), oder den Pfad zur Inhaltsinstallationsdatei (*MSHA*). Die URL kann auf die Produktgruppe (Knoten der obersten Ebene) oder auf Produktbücher (Knoten auf Blattebene) in einem Visual Studio 2010-Endpunkt verweisen. Am Ende der URL muss kein Schrägstrich (/) eingefügt werden. Wenn Sie einen nachgestellten Schrägstrich einfügen, erfolgt eine entsprechende Aktion.<br /><br /> Im Ereignisprotokoll wird eine Fehlermeldung protokolliert, wenn Sie eine Datei angeben, die nicht gefunden wird, nicht gültig ist oder auf die nicht zugegriffen werden kann. Es wird auch angegeben, wenn während der Verwaltung des Inhalts die Internetverbindung nicht verfügbar ist oder unterbrochen wurde.|
|/vendor|Nein|Gibt den Anbieter für den Produktinhalt an, der entfernt wird (beispielsweise `Microsoft`). Das Standardargument für diesen Schalter ist Microsoft.|
|/productName|Nein|Gibt den Produktnamen für die Bücher an, die entfernt werden. Der Produktname wird in den Dateien *helpcontentsetup.msha* oder *books.html* identifiziert, die im Inhalt enthalten waren. Sie können Bücher immer nur aus einem Produkt entfernen. Zum Entfernen von Büchern aus mehreren Produkten sind mehrere Installationen erforderlich.|
|/booklist|Nein|Gibt die Namen der zu verwaltenden Bücher an, getrennt durch Leerzeichen. Die Werte müssen mit den Buchtiteln übereinstimmen, wie auf den Installationsmedien aufgeführt.<br /><br /> Wenn Sie dieses Argument nicht angeben, werden alle empfohlenen Bücher installiert, die unter /sourceURI für das Produkt angegeben sind.<br /><br /> Enthält der Name eines Buchs ein oder mehrere Leerzeichen, formatieren Sie ihn mit doppelten Anführungszeichen ("), damit die Liste entsprechend getrennt wird.<br /><br /> Wenn Sie eine ungültige oder nicht erreichbare /sourceURI angeben, werden Fehlermeldungen protokolliert.|
|/skuId|Nein|Gibt die Stock Keeping Unit (SKU) des Produkts aus der Installationsquelle an und filtert Bücher, die durch den Schalter /SourceURI- ermittelt werden.|
|/membership|Nein|-   **Minimum** – Installiert den minimalen Hilfeinhalt auf Basis der SKU, die mit dem Schalter /skuId angegeben wurde. Die Zuordnung zwischen SKU und Inhalt wird in der Service-API verfügbar gemacht.<br />-   **Recommended** – Installiert eine Reihe empfohlener Bücher für die SKU, die mit dem Argument /skuId angegeben werden. Die Installationsquelle ist die Service-API oder die *MSHA-Datei*.<br />-   **Full** – Installiert den gesamten Satz von Büchern für die SKU, die mit dem Argument /skuId angegeben werden. Die Installationsquelle ist die Service-API oder die *MSHA-Datei*.|
|/locationpath|Nein|Gibt den Standardordner für den lokalen Hilfeinhalt an. Sie dürfen diesen Schalter nur zum Installieren oder Verschieben von Inhalt verwenden. Wenn Sie diesen Schalter angeben, müssen Sie auch den Schalter /silent angeben.|
|/silent|Nein|Installiert oder entfernt Hilfeinhalte ohne eine Bestätigung durch den Benutzer und ohne Anzeige einer Benutzeroberfläche. Auch im Bereich mit Statusbenachrichtigungen wird kein Symbol angezeigt. Die Ausgabe wird in einer Datei im Verzeichnis *%Temp%* protokolliert. **Wichtig:**  Für eine automatische Installation von Inhalt müssen Sie digital signierte *CAB*-Dateien verwenden, keine *MSHC*-Dateien.|
|/launchingApp|Nein|Definiert den Anwendungs- und Katalogkontext, wenn der Help Viewer ohne die übergeordnete Anwendung gestartet wird. Die Argumente für diesen Schalter sind *CompanyName*, *ProductName* und *VersionNumber* (z.B. `/launchingApp Microsoft,VisualStudio,16.0`).<br /><br /> Dies ist erforderlich, wenn Sie Inhalt mit dem Parameter „/silent“ installieren.|
|/wait *Sekunden*|Nein|Hält die Vorgänge zum Installieren, Deinstallieren und Aktualisieren an. Wird bereits ein Vorgang für den Katalog ausgeführt, wird eine festgelegte Anzahl von Sekunden gewartet, bis der Prozess fortgesetzt wird. Verwenden Sie 0 für eine unbegrenzte Wartezeit.|
|/?|Nein|Führt die Schalter und ihre Beschreibungen für das Befehlszeilentool für den Hilfeinhalts-Manager auf.|

### <a name="exit-codes"></a>Exitcodes

Wenn Sie das Befehlszeilentool für den Hilfeinhalts-Manager im automatischen Modus ausführen, werden folgende Exitcodes zurückgegeben:

```
Success = 0,

FailureToElevate = 100
InvalidCmdArgs = 101,
FailOnFetchingOnlineContent = 110,
FailOnFetchingContentFromDisk = 120,
FailOnFetchingInstalledBooks = 130,
NoBooksToUninstall = 200,
NoBooksToInstall = 300,
FailOnUninstall = 400,
FailOnInstall = 500,
FailOnMove = 600,
FailOnUpdate = 700,
FailOnRefresh = 800,
Cancelled = 900,
Others = 999,
ContentManagementDisabled = 1200,
OnlineHelpPreferenceDisabled = 1201
UpdateAlreadyRunning = 1300 - (Signals that the update didn't run because another was in progress.)
```

## <a name="see-also"></a>Siehe auch

- [Help Viewer-Administratorleitfaden](../help-viewer/administrator-guide.md)
- [Überschreibungen durch den Hilfeinhalts-Manager](../help-viewer/behavior-overrides.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)