---
title: Speichern von Daten in Projektdateien | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f1fc94b1fcb2529b41f1c74e2c6bfb9758171669
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334059"
---
# <a name="save-data-in-project-files"></a>Speichern von Daten in Projektdateien
Einem Projektuntertyp kann speichern und untertypspezifischen Daten in der Projektdatei abgerufen werden. Das Managed Package Framework (MPF) stellt zwei Schnittstellen für diese Aufgabe:

- Die <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> Schnittstelle ermöglicht den Zugriff von Eigenschaftswerten aus der **MSBuild** Abschnitt der Projektmappendatei. Die vom bereitgestellten Methoden <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> kann von einem Benutzer aufgerufen werden, wenn muss der Benutzer laden oder Speichern von verwandten Daten erstellen.

- Die <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> wird verwendet, um die nicht mit dem Build verknüpfte Daten in der formfreien XML beizubehalten. Die vom bereitgestellten Methoden <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> von aufgerufen werden, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] immer [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] muss nicht mit dem Build verknüpfte Daten in der Projektdatei beibehalten werden.

  Weitere Informationen zum Erstellen und nicht mit dem Build verknüpfte Daten beibehalten werden, finden Sie unter [beibehalten von Daten in der MSBuild-Projektdatei](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md).

## <a name="save-and-retrieve-build-related-data"></a>Speichern und abrufen, erstellen verknüpfte Daten

### <a name="to-save-a-build-related-data-in-the-project-file"></a>Im Zusammenhang der Daten in der Projektdatei, um einen Build zu speichern.

- Rufen Sie die <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> Methode, um einen vollständigen Pfad der Projektdatei zu speichern.

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string newFullPath = GetNewFullPath();
    // Set a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.SetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, newFullPath));
    ```

### <a name="to-retrieve-build-related-data-from-the-project-file"></a>Zum Abrufen von Build-Daten aus der Projektdatei

- Rufen Sie die <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A> Methode, um einen vollständigen Pfad der Projektdatei abzurufen.

    ```
    private SpecializedProject project;
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;
    string fullPath;
    // Get a full path of the project file.
    ErrorHandler.ThrowOnFailure(projectStorage.GetPropertyValue(
        "MSBuildProjectDirectory",
        String.Empty,
        (uint)_PersistStorageType.PST_PROJECT_FILE, out fullPath));
    ```

## <a name="save-and-retrieve-non-build-related-data"></a>Speichern und Abrufen von nicht mit dem Build verknüpfte Daten

### <a name="to-save-non-build-related-data-in-the-project-file"></a>Zum Speichern von nicht auf den Build bezogene Daten in der Projektdatei

1. Implementieren der <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A> Methode, um zu bestimmen, ob ein XML-Fragment geändert hat, seit dem letzten Speichern in dessen aktueller Datei.

    ```
    public int IsFragmentDirty(uint storage, out int pfDirty)
    {
        pfDirty = 0;
        switch (storage)
        {
            case (uint)_PersistStorageType.PST_PROJECT_FILE:
            {
                if (isDirty)
                    pfDirty |= 1;
                break;
            }
            case (uint)_PersistStorageType.PST_USER_FILE:
            {
                // We do not store anything in the user file.
                break;
            }
        }

        // Forward the call to inner flavor(s)
        if (pfDirty == 0 && innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).IsFragmentDirty(storage, out pfDirty);

        return VSConstants.S_OK;

    }
    ```

2. Implementieren der <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> Methode, um die XML-Daten in der Projektdatei zu speichern.

    ```
    public int Save(ref Guid guidFlavor, uint storage, out string pbstrXMLFragment, int fClearDirty)
    {
        pbstrXMLFragment = null;

        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Create XML for our data.
                    XmlDocument doc = new XmlDocument();
                    XmlNode root = doc.CreateElement(this.GetType().Name);

                    XmlNode node = doc.CreateElement(targetsTag);
                    node.AppendChild(doc.CreateTextNode(this.TargetsToExecute));
                    root.AppendChild(node);

                    node = doc.CreateElement(updateTargetsTag);
                    node.AppendChild(doc.CreateTextNode(this.UpdateTargetList.ToString()));
                    root.AppendChild(node);

                    doc.AppendChild(root);
                    // Get XML fragment representing our data
                    pbstrXMLFragment = doc.InnerXml;

                    if (fClearDirty != 0)
                        isDirty = false;
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Save(ref guidFlavor, storage, out pbstrXMLFragment, fClearDirty);

        return VSConstants.S_OK;
    }
    ```

### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>Zum Abrufen von nicht mit dem Build verknüpfter Daten in der Projektdatei

1. Implementieren der <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A> Methode initialisiert die projekterweiterungseigenschaften und andere Build-unabhängige Daten. Diese Methode wird aufgerufen, wenn es keine XML-Konfigurationsdaten in der Projektdatei vorhanden.

    ```
    public int InitNew(ref Guid guidFlavor, uint storage)
    {
        //Return,if it is our guid.
        if (IsMyFlavorGuid(ref guidFlavor))
            return VSConstants.S_OK;

        //Forward the call to inner flavor(s).
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).InitNew(ref guidFlavor, storage);

        return VSConstants.S_OK;
    ```

2. Implementieren der <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> Methode, um die XML-Daten aus der Projektdatei zu laden.

    ```
    public int Load(ref Guid guidFlavor, uint storage, string pszXMLFragment)
    {
        if (IsMyFlavorGuid(ref guidFlavor))
        {
            switch (storage)
            {
                case (uint)_PersistStorageType.PST_PROJECT_FILE:
                {
                    // Load our data from the XML fragment.
                    XmlDocument doc = new XmlDocument();
                    XmlNode node = doc.CreateElement(this.GetType().Name);
                    node.InnerXml = pszXMLFragment;
                    if (node == null
                        || node.FirstChild == null
                        || node.FirstChild.ChildNodes.Count == 0
                        || node.FirstChild.ChildNodes[0].Name != targetsTag)
                        break;
                    this.TargetsToExecute = node.FirstChild.ChildNodes[0].InnerText;

                    if (node.FirstChild.ChildNodes.Count <= 1
                        || node.FirstChild.ChildNodes[1].Name != updateTargetsTag)
                        break;
                    this.UpdateTargetList = bool.Parse(node.FirstChild.ChildNodes[1].InnerText);
                    break;
                }
                case (uint)_PersistStorageType.PST_USER_FILE:
                {
                    // We do not store anything in the user file.
                    break;
                }
            }
        }

        // Forward the call to inner flavor(s)
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)
            return ((IPersistXMLFragment)this.innerCfg).Load(ref guidFlavor, storage, pszXMLFragment);

        return VSConstants.S_OK;
    }
    ```

> [!NOTE]
> Alle Codebeispiele in diesem Thema werden die Teile eines umfangreicheren Beispiels unter [VSSDK-Beispiele](https://aka.ms/vs2015sdksamples).

## <a name="see-also"></a>Siehe auch
- [Beibehalten von Daten in der MSBuild-Projektdatei](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)