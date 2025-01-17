---
title: Die ausgewählte Verbindung nutzt einen nicht unterstützten Datenbankanbieter | Microsoft-Dokumentation
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: adf0dd7392b492364a286b5984de52b2b4640ae2
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700158"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>Die ausgewählte Verbindung nutzt einen nicht unterstützten Anbieter.
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diese Meldung wird angezeigt, wenn Sie Elemente ziehen, die nicht die .NET Framework-Datenanbieter für SQL Server verwenden **Server-Explorer**/**Datenbank-Explorer** auf die [LINQ to SQL -Tools in Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md).  
  
 Der [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] unterstützt nur Datenverbindungen, die den .NET Framework-Anbieter für SQL Server verwenden. Nur Verbindungen zu Microsoft SQL Server oder zur Microsoft SQL Server-Datenbankdatei sind gültig.  
  
### <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
- Fügen Sie nur Elemente von Datenverbindungen hinzu, die den .NET Framework-Datenanbieter für SQL Server zu [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Data.SqlClient>   
 [.NET Framework-Datenanbieter](https://msdn.microsoft.com/library/03a9fc62-2d24-491a-9fe6-d6bdb6dcb131)   
 [Exemplarische Vorgehensweise: Erstellen von LINQ to SQL-Klassen (O / R-Designer)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)