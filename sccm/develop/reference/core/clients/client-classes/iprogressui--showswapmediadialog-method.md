---
title: "IProgressUI::ShowSwapMediaDialog"
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
# IProgressUI::ShowSwapMediaDialog Method
In Configuration Manager, the `ShowSwapMediaDialog` method displays message box to prompt a user to swap media.  

## Syntax  

```  
[IDL]  
HRESULT ShowSwapMediaDialog(  
     BSTR pszTaskSequenceName,  
     ULONG uMediaNumber
);  
```  

#### Parameters  
 `pszTaskSequenceName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the name of the task sequence that is currently running. The value can be retrieved from the `_SMSTSPackageName` environment variable.  

 `uMediaNumber`  
 Data type: `ULONG`  

 Qualifiers: [in]

 The value of the media item to be swapped by the user.

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
