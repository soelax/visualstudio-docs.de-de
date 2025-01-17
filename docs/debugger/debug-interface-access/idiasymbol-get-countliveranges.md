---
title: IDiaSymbol::get_countLiveRanges | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_countLiveRanges
ms.assetid: 55f79e1a-d4c2-42cd-ab37-d8253b20e34c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8cd86edee72f3d25763fd3d19dd9c789e152ed6
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837462"
---
# <a name="idiasymbolgetcountliveranges"></a>IDiaSymbol::get_countLiveRanges
Ruft die Anzahl der gültigen-Adressbereiche, die den lokalen Symbolcache zugeordnet.

## <a name="syntax"></a>Syntax

```C++
HRESULT get_countLiveRanges ( 
   DWORD* count
);
```

#### <a name="parameters"></a>Parameter
 `count`

[out] Gibt die Anzahl der Adressbereiche zurück.

## <a name="return-value"></a>Rückgabewert
 Wenn erfolgreich, wird `S_OK`ist, andernfalls ein Fehlercode zurückgegeben.

## <a name="requirements"></a>Anforderungen
 Header: Dia2.h

 Bibliothek: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>Siehe auch
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)