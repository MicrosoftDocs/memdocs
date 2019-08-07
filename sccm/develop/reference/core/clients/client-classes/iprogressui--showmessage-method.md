---
title: IProgressUI::ShowMessage
titleSuffix: Configuration Manager
description: IProgressUI::ShowMessage method
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 2b79dafd-c4ba-4832-88f7-62d2e6b4caf0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# IProgressUI::ShowMessage method

In Configuration Manager, the `ShowMessage` method displays customizable dialog box.

## Syntax  

```  
[IDL]  
HRESULT ShowMessage(  
     BSTR pszText,  
     BSTR pszCaption,  
     ULONG uType
);  
```  

### Parameters  

#### `pszText`

Data type: `BSTR`  

Qualifiers: [in]

The text displayed in the message box body.
  
#### `pszCaption`

Data type: `BSTR`  

Qualifiers: [in]  

The text displayed in the message box windows header.

#### `uType`

Data type: `ULONG`  

Qualifiers: [in]

The value corresponding to one of the following possible values for the buttons:

- 0 - Ok
- 1 - Ok/Cancel
- 2 - Abort/Retry/Ignore
- 3 - Yes/No/Cancel
- 4 - Yes/No
- 5 - Retry/Cancel
- 6 - Cancel/Try Again/Continue

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.

S_OK  
The method succeeded.  

## See also

- [OS deployment client COM automation classes](/sccm/develop/reference/core/clients/client-classes/operating-system-deployment-client-com-automation-classes)  

- [IProgressUI interface](/sccm/develop/reference/core/clients/client-classes/iprogressui-interface)  

- [About reporting Configuration Manager custom action progress](/sccm/develop/osd/about-reporting-configuration-manager-custom-action-progress)  

- [How to use task sequence variables in a running Configuration Manager task sequence](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence)  
