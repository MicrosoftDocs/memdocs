---
title: "IProgressUI::ShowMessage"
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
# IProgressUI::ShowMessage Method
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

#### Parameters  
 `pszText`  
 Data type: `BSTR`  

 Qualifiers: [in] 

 The text displayed in the message box body.
  
 `pszCaption`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 The text displayed in the message box windows header.

 `uType`  
 Data type: `ULONG`  

 Qualifiers: [in]

 The value corresponding to one of 7 sets of buttons. Possible values include:
 - 0 - Ok
 - 1 - Ok/Cancel
 - 2 - Abort/Retry/Ignore
 - 3 - Yes/No/Cancel
 - 4 - Yes/No
 - 5 - Retry/Cancel
 - 6 - Cancel/Try Again/Continue

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
