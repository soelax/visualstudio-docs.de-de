---
title: Initialisierungssequenz von Projektuntertypen | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f8b256e25bc9a63093d14eab50d7628c76558b9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349837"
---
# <a name="initialization-sequence-of-project-subtypes"></a>Initialisierungssequenz von Projektuntertypen
Die Umgebung erstellt ein Projekt durch Aufrufen der Basis projektfactoryimplementierung von <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>. Die Erstellung von einem Projektuntertyp wird gestartet, wenn die Umgebung bestimmt, dass die Liste mit Projekten Typ GUID für ein Projekt die Dateierweiterung nicht leer ist. Die Dateinamenerweiterung für Projektdateien und die Projekt-GUID angeben, ob das Projekt ist eine [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] oder [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] Projekttyp. Z. B. die Erweiterung .vbproj {F184B08F-C81C-45F6-A57F-5ABD9991F28F} zu identifizieren, und eine [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] Projekt.

## <a name="environments-initialization-of-project-subtypes"></a>Initialisierung der Umgebung von Projektuntertypen
 Das folgende Verfahren erläutert die Initialisierungssequenz für ein Projektsystem, die von mehreren Projektuntertypen aggregiert.

1. Die Umgebung ruft des Basisprojekts <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>, während das Projekt die Projektdatei analysiert werden, dass der aggregierte Projekttyp GUIDs Liste nicht `null`. Das Projekt wird beendet, ihr Projekt direkt zu erstellen.

2. Die projektaufrufe `QueryService` auf <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> zu einem Projektuntertyp, die mit der Umgebung-Implementierung des zu erstellenden Dienst den <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> Methode. Innerhalb dieser Methode wird die Umgebung rekursive Funktionsaufrufe an Ihre Implementierungen von <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>, <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> und <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> GUIDs, beginnend mit der äußeren Projektuntertyp Geben Sie Methoden, während sie die Liste der Projekttyp durchlaufen wird.

     Im folgenden Abschnitt wird die Initialisierungsschritte.

    1. Implementierung der Umgebung die <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> Methodenaufrufe der `HrCreateInnerProj` -Methode durch die folgende Funktionsdeklaration:

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         Wenn diese Funktion wird aufgerufen zum ersten Mal, d. h. für den äußeren Projektuntertyp, die Parameter `pOuter` und `pOwner` als übergeben `null` und die Funktion legt fest, den äußeren Projektuntertyp `IUnknown` zu `pOuter`.

    2. Als Nächstes die Umgebung ruft `HrCreateInnerProj` -Funktion mit dem zweiten Projekttyp-GUID in der Liste. Diese GUID entspricht der zweiten inneren Projektuntertyp einzelschrittausführung in Richtung Basisprojekts in der Aggregation-Sequenz.

    3. Die `pOuter` verweist jetzt auf die `IUnknown` des äußersten projektuntertyps, und `HrCreateInnerProj` ruft Ihre Implementierung der <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> gefolgt von einem Aufruf für Ihre Implementierung der <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>. In <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> Methode, die Sie das steuernde übergeben `IUnknown` des äußersten projektuntertyps, `pOuter`. Das Projekt im Besitz (inneren Projektuntertyp) muss hier die Projekt-Objekt zu erstellen. In der <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> übergeben Sie einen Zeiger auf die Implementierung der `IUnknown` des inneren Projekts, das aggregiert wird. Diese beiden Methoden erstellen, das Aggregation-Objekt, und Ihre Implementierungen müssen Sie COM-Aggregationsregeln, um sicherzustellen, dass es sich bei einem Projektuntertyp nicht am Ende ist, einen Verweiszähler auf sich selbst enthält.

    4. `HrCreateInnerProj` Ruft die Implementierung von <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>. Bei dieser Methode führt der Projektuntertyp Initialisierung. Sie können z. B. Projektmappenereignissen in registrieren <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>.

    5. `HrCreateInnerProj` wird rekursiv aufgerufen werden, bis die letzte GUID (die Basis-Projekt) in der Liste erreicht ist. Für jeden dieser Aufrufe werden die Schritte, bis d, C wiederholt. `pOuter` verweist auf den äußeren Projektuntertyp `IUnknown` für jede Ebene der Aggregation.

## <a name="example"></a>Beispiel

Im folgende Beispiel erläutert die programmgesteuerte in eine ungefähre Darstellung der <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> -Methode wird von der Umgebung implementiert. Der Code ist nur ein Beispiel. Es ist nicht vorgesehen, die kompiliert werden, und alle fehlerprüfungen entfernt wurde, aus Gründen der Übersichtlichkeit.

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>Siehe auch

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [Projektuntertypen](../../extensibility/internals/project-subtypes.md)