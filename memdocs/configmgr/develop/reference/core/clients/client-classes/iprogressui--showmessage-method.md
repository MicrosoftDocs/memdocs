---
title: "IProgressUI::ShowMessage"
titleSuffix: Configuration Manager
description: "IProgressUI::ShowMessage method"
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2b79dafd-c4ba-4832-88f7-62d2e6b4caf0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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

To evaluate the user's response to the message box, use the [IProgressUI::ShowMessageEx](iprogressui--showmessageex-method.md) method.

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  
