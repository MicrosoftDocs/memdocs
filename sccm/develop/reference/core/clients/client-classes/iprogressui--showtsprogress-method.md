---
title: "IProgressUI::ShowTSProgress"
titleSuffix: "Configuration Manager"
ms.date: "03/12/2019"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 
author: adamgrosstx
ms.author: 
manager: 
---
# IProgressUI::ShowTSProgress Method
In Configuration Manager, the `ShowTSProgress` method displays custom task sequence progress information in a dialog box.

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
);  
```  

#### Parameters  
 `pszOrgName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the organization name that is shown in the progress dialog box. The value can be retrieved from the `_SMSTSOrgName` environment variable.  

 `pszTaskSequenceName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the name of the task sequence that is currently running. The value can be retrieved from the `_SMSTSPackageName` environment variable.  

 `pszCustomTitle`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the text for a custom message that replaces the default title text displayed in the progress dialog box. Pass an empty string if there is no custom message to show. The value can be obtained from the `_SMSTSCustomProgressDialogMessage` environment variable.  

 `pszCurrentAction`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the name of the current task sequence step. The value can be obtained from the `_SMSTSCurrentActionName` environment variable.  

 `uStep`  
 Data type: `ULONG`  

 Qualifiers: [in]  

 The current task sequence step number. The value can be obtained from the `SMSTSNextInstructionPointer` environment variable.  

 `uMaxStep`  
 Data type: `ULONG`  

 Qualifiers: [in]  

 The total number of steps in the task sequence. The value can be obtained from the `_SMSTSInstructionTableSize` environment variable.  


## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value. There are no `HRESULT` values returned that are specific to this method.  

 S_OK  
 The method succeeded.  

## See Also  
 [Operating System Deployment Client COM Automation Classes](../../../../../develop/reference/core/clients/client-classes/operating-system-deployment-client-com-automation-classes.md)   
 [IProgressUI Interface](../../../../../develop/reference/core/clients/client-classes/iprogressui-interface.md)   
 [About Reporting Configuration Manager Custom Action Progress](../../../../../develop/osd/about-reporting-configuration-manager-custom-action-progress.md)   
 [Extending Operating System Deployment](../../../../../develop/osd/extending-operating-system-deployment.md)   
 [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../../../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)
