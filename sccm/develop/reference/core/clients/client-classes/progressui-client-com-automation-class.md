---
title: "ProgressUI Client COM Automation Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f60558cd-a2c9-401d-bca0-191cdf117bbe
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ProgressUI Client COM Automation Class
`ProgressUI` is a COM automation class, in System Center Configuration Manager, that represents a user interface that custom actions use to report progress to the Configuration Manager operating system deployment task sequencing environment. The class implements the `IProgressUI` interface, which has a method `ShowActionProgress` that is used to display custom action progress information in a dialog box while the custom action is running. You should not call any other method implemented in `ProgressUI`.  

## In This Section  

|Term|Definition|  
|----------|----------------|  
|[IProgressUI Interface](../../../../../develop/reference/core/clients/client-classes/iprogressui-interface.md)|Manages custom action progress information.|  

## Remarks  
 `ProgressUI` is implemented in TSProgressUI.exe.  

 The class GUID is F79474A1-7B80-4a18-BC7B-D3938BD93808.  

 The programmatic identifier (ProgID) is Microsoft.SMS.TsProgressUI.  

 To use `ProgressUI` in Visual Studio, add a reference to "SMS TSE Progress UI".  

## See Also  
 [Operating System Deployment Client COM Automation Classes](../../../../../develop/reference/core/clients/client-classes/operating-system-deployment-client-com-automation-classes.md)   
 [About Reporting Configuration Manager Custom Action Progress](../../../../../develop/osd/about-reporting-configuration-manager-custom-action-progress.md)   
 [Extending Operating System Deployment](../../../../../develop/osd/extending-operating-system-deployment.md)
