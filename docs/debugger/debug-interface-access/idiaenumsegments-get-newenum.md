---
title: 'Idiaenumsegments:: Get__newenum | Microsoft-Dokumentation'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::get__NewEnum method
ms.assetid: 504505fa-b35c-402f-a440-8972c589cc5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5c021e74c758b6409d42deae6a7e6831368367e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829809"
---
# <a name="idiaenumsegmentsgetnewenum"></a>IDiaEnumSegments::get__NewEnum
Ruft die <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> Version von diesem Enumerator.

## <a name="syntax"></a>Syntax

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>Parameter
 pRetVal

[out] Gibt die `IUnknown` Schnittstelle, die darstellt der <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> Version von diesem Enumerator.

## <a name="return-value"></a>Rückgabewert
 Wenn erfolgreich, wird `S_OK`ist, andernfalls ein Fehlercode zurückgegeben.

## <a name="see-also"></a>Siehe auch
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)