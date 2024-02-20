---
title: "IProgressUI::ShowSwapMediaDialog"
titleSuffix: Configuration Manager
description: "IProgressUI::ShowSwapMediaDialog method"
ms.date: 04/03/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e78bdee8-4e80-461a-8a0d-1db6a49a73db
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# IProgressUI::ShowSwapMediaDialog method

In Configuration Manager, the `ShowSwapMediaDialog` method displays message box to prompt a user to swap media.  

## Syntax  

```  
[IDL]  
HRESULT ShowSwapMediaDialog(  
     BSTR pszTaskSequenceName,  
     ULONG uMediaNumber
);  
```  

### Parameters

#### `pszTaskSequenceName`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the name of the task sequence that is currently running. The value can be retrieved from the `_SMSTSPackageName` environment variable.  

#### `uMediaNumber`

Data type: `ULONG`  

Qualifiers: [in]

The value of the media item to be swapped by the user.

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.

S_OK  
The method succeeded.  

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  
