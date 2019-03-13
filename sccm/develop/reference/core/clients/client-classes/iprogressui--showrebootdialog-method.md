---
title: "IProgressUI::ShowRebootDialog"
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
# IProgressUI::ShowRebootDialog Method
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

 Pointer to the text for a custom message that replaces the default title text displayed in the reboot dialog box. Pass an empty string if there is no custom message to show. The value can be obtained from the `_SMSTSCustomProgressDialogMessage` environment variable.  

 `pszRebootMessage`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Pointer to the text for the custom message that will be displayed in the reboot dialog box. Pass an empty string if there is no custom message to show.

 `uTimeoutInSeconds`  
 Data type: `ULONG`  

 Qualifiers: [in]  

 Pointer to the value for the number of seconds the dialog box is displayed before closing. The value can be obtained from the `SMSTSErrorDialogTimeout` environment variable which is not configured in the task sequence by default. If an empty string is specified for `uTimeoutInSeconds` and `SMSTSErrorDialogTimeout` is not specified, a default of 900 seconds will be used.

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
