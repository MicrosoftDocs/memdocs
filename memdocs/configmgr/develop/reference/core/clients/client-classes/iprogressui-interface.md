---
title: IProgressUI interface
titleSuffix: Configuration Manager
description: "IProgressUI represents the user interface that allows custom actions to report progress to the OS deployment task sequencing environment."
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2c84a3bd-f8d8-46a4-9591-07186ca5fe65
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# IProgressUI interface

The `IProgressUI` automation interface in Configuration Manager represents the user interface that allows custom actions to report progress to the OS deployment task sequencing environment.  

## Methods for this interface

|Term|Definition|  
|----------|----------------|  
|[IProgressUI::CloseProgressDialog](iprogressui--closeprogressdialog-method.md)|Closes open instances of `IProgressUI`|  
|[IProgressUI::ShowActionProgress](iprogressui--showactionprogress-method.md)|Displays custom action progress information in a dialog box while the custom action is running.|  
|[IProgressUI::ShowErrorDialog](iprogressui--showerrordialog-method.md)|Displays customizable error information in a dialog box.|
|[IProgressUI::ShowMessage](iprogressui--showmessage-method.md)|Displays customizable dialog box.|
|[IProgressUI::ShowMessageEx](iprogressui--showmessageex-method.md)|Displays customizable dialog box and captures an integer result variable.|
|[IProgressUI::ShowRebootDialog](iprogressui--showrebootdialog-method.md)|Displays customizable reboot warning dialog box.|
|[IProgressUI::ShowSwapMediaDialog](iprogressui--showswapmediadialog-method.md)|Displays message box to prompt a user to swap media.|
|[IProgressUI::ShowTSProgress](iprogressui--showtsprogress-method.md)|Displays custom task sequence progress information in a dialog box.|

## Remarks

The GUID for `IProgressUI` is B64D758A-01C2-4bf0-9F17-621EFB9CF697.  

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [ProgressUI Class](progressui-client-com-automation-class.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  
