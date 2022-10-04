---
title: "IProgressUI::ShowActionProgress"
titleSuffix: Configuration Manager
description: In Configuration Manager, the ShowActionProgress method displays custom action progress information in a dialog box while the custom action is running.
ms.date: 04/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4f08f27a-bb32-4a86-b7ca-ef745c311323
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# IProgressUI::ShowActionProgress method

In Configuration Manager, the `ShowActionProgress` method displays custom action progress information in a dialog box while the custom action is running.  

## Syntax  

```  
[IDL]  
HRESULT ShowActionProgress(  
     BSTR pszOrgName,  
     BSTR pszTaskSequenceName,  
     BSTR pszCustomTitle,  
     BSTR pszCurrentAction,  
     ULONG uStep,  
     ULONG uMaxStep,  
     BSTR pszActionExecInfo,  
     ULONG uActionExecStep,  
     ULONG uActionExecMaxStep  
);  
```  

### Parameters  

#### `pszOrgName`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the organization name that is shown in the progress dialog box. The value can be retrieved from the `_SMSTSOrgName` environment variable.  

#### `pszTaskSequenceName`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the name of the task sequence that is currently running. The value can be retrieved from the `_SMSTSPackageName` environment variable.  

#### `pszCustomTitle`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the text for a custom message that replaces the default title text displayed in the progress dialog box. Pass an empty string if there's no custom message to show. The value can be obtained from the `_SMSTSCustomProgressDialogMessage` environment variable.  

#### `pszCurrentAction`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to the name of the current task sequence step. The value can be obtained from the `_SMSTSCurrentActionName` environment variable.  

#### `uStep`

Data type: `ULONG`  

Qualifiers: [in]  

The current task sequence step number. The value can be obtained from the `SMSTSNextInstructionPointer` environment variable.  

#### `uMaxStep`

Data type: `ULONG`  

Qualifiers: [in]  

The total number of steps in the task sequence. The value can be obtained from the `_SMSTSInstructionTableSize` environment variable.  

#### `pszActionExecInfo`

Data type: `BSTR`  

Qualifiers: [in]  

Pointer to user-defined, action-specific progress information to be shown in the progress dialog box.  

#### `uActionExecStep`

Data type: `ULONG`  

Qualifiers: [in]  

The numerical step, within the total number of numerical steps, on which the action is currently working.  

Use this parameter to determine the percentage of the action that has been completed so far. For more information, see [Remarks](#remarks).

#### `uActionExecMaxStep`

Data type: `ULONG`  

Qualifiers: [in]  

The total number of numerical steps that the action does.  

Use this parameter to determine the percentage of the action that has been completed so far. For more information, see [Remarks](#remarks).

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.  

S_OK  
The method succeeded.  

## Remarks

The only required information for this method is for the `pszActionExecInfo`, `uActionExecStep`, and `uActionExecMaxStep` parameters. The other parameters can be obtained from the referenced environment variables.  

A call to `ShowActionProgress` should specify the percentage completion of the action using the `uActionExecStep` and `uActionExecMaxStep` parameters. For example, if `uActionExecStep` specifies the value 2 and `uActionExecMaxStep` specifies the value 10, the percentage completion of the action is 20 percent.  

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  
