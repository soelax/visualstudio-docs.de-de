---
title: ShowByDefault-Element (Visual Studio-Vorlagen)
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ShowByDefault
helpviewer_keywords:
- <ShowByDefault> element [Visual Studio Templates]
- ShowByDefault element [Visual Studio Templates]
ms.assetid: 7be783f6-0ef6-42bc-924a-df9a2eba7781
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c211f45423ce0f2166bbf8aa189d35ab386a7fee
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331984"
---
# <a name="showbydefault-element-visual-studio-templates"></a>ShowByDefault-Element (Visual Studio-Vorlagen)
Wenn `false`, gibt an, dass die Vorlage nur angezeigt werden, wird unter der angegebenen [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md).

 \<VSTemplate> \<TemplateData> \<ShowByDefault>

## <a name="syntax"></a>Syntax

```
<ShowByDefault> true/false </ShowByDefault>
```

## <a name="attributes-and-elements"></a>Attribute und Elemente
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.

### <a name="attributes"></a>Attribute
 Keine

### <a name="child-elements"></a>Untergeordnete Elemente
 Keine

### <a name="parent-elements"></a>Übergeordnete Elemente

|Element|Beschreibung|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Kategorisiert die Vorlage und definiert, wie diese in den Dialogfeldern **Neues Projekt** oder **Neues Element hinzufügen** angezeigt wird.|

## <a name="text-value"></a>Textwert
 Ein Textwert ist erforderlich.

 Der Text muss entweder `true` oder `false` sein. Gibt bei TRUE an, dass die Vorlage für alle Projekttypen angezeigt wird. Bei FALS wird die Vorlage nur unter der angegebenen `TemplateGroupID` angezeigt.

## <a name="remarks"></a>Hinweise
 `ShowByDefault` ist ein optionales Element. Der Standardwert ist `true`.

## <a name="example"></a>Beispiel
 Im folgenden Beispiel werden die Metadaten für eine [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]-Vorlage veranschaulicht.

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ShowByDefault>false</ShowByDefault>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Siehe auch
- [Erstellen von Projekt- und Elementvorlagen](../ide/creating-project-and-item-templates.md)
- [Schemareferenz zu Visual Studio-Vorlagen](../extensibility/visual-studio-template-schema-reference.md)
- [TemplateGroupID-Element (Visual Studio-Vorlagen)](../extensibility/templategroupid-element-visual-studio-templates.md)