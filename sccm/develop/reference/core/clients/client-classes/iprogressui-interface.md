---
title: "IProgressUI Interface"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2c84a3bd-f8d8-46a4-9591-07186ca5fe65
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---
# IProgressUI Interface
The `IProgressUI` automation interface, in System Center Configuration Manager, represents the user interface that allows custom actions to report progress to the operating system deployment task sequencing environment.  

## In This Section  

|Term|Definition|  
|----------|----------------|  
|[IProgressUI::ShowActionProgress](../../../../../develop/reference/core/clients/client-classes/iprogressui--showactionprogress-method.md)|Displays custom action progress information in a dialog box while the custom action is running.|
|[IProgressUI::ShowErrorDialog](../../../../../develop/reference/core/clients/client-classes/iprogressui--showerrordialog-method.md)|Displays customizable error information in a dialog box.|
|[IProgressUI::ShowMessage](../../../../../develop/reference/core/clients/client-classes/iprogressui--showmessage-method.md)|Displays customizable dialog box.|
|[IProgressUI::ShowRebootDialog](../../../../../develop/reference/core/clients/client-classes/iprogressui--showrebootdialog-method.md)|Displays customizable reboot warning dialog box.|
|[IProgressUI::ShowSwapMediaDialog](../../../../../develop/reference/core/clients/client-classes/iprogressui--showswapmediadialog-method.md)|Displays message box to prompt a user to swap media.|
|[IProgressUI::ShowTSProgress](../../../../../develop/reference/core/clients/client-classes/iprogressui--showtsprogress-method.md)|Displays custom task sequence progress information in a dialog box.|
  








## Remarks  
 The GUID for `IProgressUI` is B64D758A-01C2-4bf0-9F17-621EFB9CF697.  

## See Also  
 [Operating System Deployment Client COM Automation Classes](../../../../../develop/reference/core/clients/client-classes/operating-system-deployment-client-com-automation-classes.md)   
 [ProgressUI Class](../../../../../develop/reference/core/clients/client-classes/progressui-client-com-automation-class.md)   
 [About Reporting Configuration Manager Custom Action Progress](../../../../../develop/osd/about-reporting-configuration-manager-custom-action-progress.md)   
 [Extending Operating System Deployment](../../../../../develop/osd/extending-operating-system-deployment.md)
