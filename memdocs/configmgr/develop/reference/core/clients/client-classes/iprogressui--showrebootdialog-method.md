---
title: IProgressUI::ShowRebootDialog
titleSuffix: Configuration Manager
description: IProgressUI::ShowRebootDialog method
ms.date: 04/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference


ms.assetid: f9c7b72d-e781-49e2-b5a7-23a3e005596f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# IProgressUI::ShowRebootDialog method

In Configuration Manager, the `ShowRebootDialog` method displays customizable reboot warning dialog box.  

## Syntax  

```  
[IDL]  
HRESULT ShowRebootDialog(  
     BSTR pszOrgName,  
     BSTR pszTaskSequenceName,  
     BSTR pszCustomTitle,  
     BSTR pszRebootMessage,  
     ULONG uErrorCode,  
     ULONG uTimeoutInSeconds,  
);  
```  

### Parameters

#### `pszOrgName`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the organization name that's shown in the progress dialog box. The value can be retrieved from the `_SMSTSOrgName` environment variable.  

#### `pszTaskSequenceName`
Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the name of the task sequence that's currently running. The value can be retrieved from the `_SMSTSPackageName` environment variable.  

#### `pszCustomTitle`
Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the text for a custom message that replaces the default title text displayed in the reboot dialog box. Pass an empty string if there's no custom message to show. The value can be obtained from the `_SMSTSCustomProgressDialogMessage` environment variable.  

#### `pszRebootMessage`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the text for the custom message that will be displayed in the reboot dialog box. Pass an empty string if there's no custom message to show.

#### `uTimeoutInSeconds`
Data type: `ULONG`  

Qualifiers: [in]  

Pointer to the value for the number of seconds the dialog box is displayed before closing. The value can be obtained from the `SMSTSErrorDialogTimeout` environment variable, which isn't configured in the task sequence by default. If an empty string is specified for `uTimeoutInSeconds` and `SMSTSErrorDialogTimeout` isn't specified, a default of 900 seconds will be used.

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.

S_OK  
The method succeeded.  

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  
