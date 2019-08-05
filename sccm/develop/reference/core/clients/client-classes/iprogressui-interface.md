---
title: IProgressUI interface
titleSuffix: Configuration Manager
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2c84a3bd-f8d8-46a4-9591-07186ca5fe65
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# IProgressUI interface

The `IProgressUI` automation interface in Configuration Manager represents the user interface that allows custom actions to report progress to the OS deployment task sequencing environment.  

## Methods for this interface

|Term|Definition|  
|----------|----------------|  
|[IProgressUI::CloseProgressDialog](/sccm/develop/reference/core/clients/client-classes/iprogressui--closeprogressdialog-method)|Closes open instances of `IProgressUI`|  
|[IProgressUI::ShowActionProgress](/sccm/develop/reference/core/clients/client-classes/iprogressui--showactionprogress-method)|Displays custom action progress information in a dialog box while the custom action is running.|  
|[IProgressUI::ShowErrorDialog](/sccm/develop/reference/core/clients/client-classes/iprogressui--showerrordialog-method)|Displays customizable error information in a dialog box.|
|[IProgressUI::ShowMessage](/sccm/develop/reference/core/clients/client-classes/iprogressui--showmessage-method)|Displays customizable dialog box.|
|[IProgressUI::ShowRebootDialog](/sccm/develop/reference/core/clients/client-classes/iprogressui--showrebootdialog-method)|Displays customizable reboot warning dialog box.|
|[IProgressUI::ShowSwapMediaDialog](/sccm/develop/reference/core/clients/client-classes/iprogressui--showswapmediadialog-method)|Displays message box to prompt a user to swap media.|
|[IProgressUI::ShowTSProgress](/sccm/develop/reference/core/clients/client-classes/iprogressui--showtsprogress-method)|Displays custom task sequence progress information in a dialog box.|

## Remarks

The GUID for `IProgressUI` is B64D758A-01C2-4bf0-9F17-621EFB9CF697.  

## See also

- [OS deployment client COM automation classes](/sccm/develop/reference/core/clients/client-classes/operating-system-deployment-client-com-automation-classes)  

- [ProgressUI Class](/sccm/develop/reference/core/clients/client-classes/progressui-client-com-automation-class)  

- [About reporting Configuration Manager custom action progress](/sccm/develop/osd/about-reporting-configuration-manager-custom-action-progress)  
