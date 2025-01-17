---
title: SccUninitialize-Funktion | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f71e34352150143c7db207ed31ea6e879f97ca18
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338494"
---
# <a name="sccuninitialize-function"></a>SccUninitialize-Funktion
Diese Funktion löscht alle Zuordnungen oder offene Verbindungen, die von einem vorherigen Aufruf von erstellt die [SccInitialize](../extensibility/sccinitialize-function.md) als Vorbereitung für das Quellcodeverwaltungs-Plug-in wird heruntergefahren.

## <a name="syntax"></a>Syntax

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>Parameter
 pvContext

[in] Der Zeiger auf die Datenquellen-Steuerelement-Plug-in Context-Struktur erstellt, der [SccInitialize](../extensibility/sccinitialize-function.md).

## <a name="return-value"></a>Rückgabewert
 Die Source-Steuerelement-Plug-in-Implementierung dieser Funktion muss einen der folgenden Werte zurückgeben:

|Wert|Beschreibung|
|-----------|-----------------|
|SCC_OK|Die Bereinigung wurde erfolgreich abgeschlossen.|

## <a name="remarks"></a>Hinweise
 Das Quellcodeverwaltungs-Plug-in ist verantwortlich für die Vorbereitung heruntergefahren werden, und Freigeben von Arbeitsspeicher, die das plug-in für die Context-Struktur zugeordnet ist. Die Funktion wird einmal für jede bestimmte Instanz eines Plug-Ins aufgerufen. Ein Aufruf der [SccInitialize](../extensibility/sccinitialize-function.md) dieses Aufrufs steht. Keine Projekte können immer noch geöffnet sein zum Zeitpunkt des Aufrufs von `SccUninitialize`.

## <a name="see-also"></a>Siehe auch
- [API-Funktionen von Quellcodeverwaltungs-Plug-Ins](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)