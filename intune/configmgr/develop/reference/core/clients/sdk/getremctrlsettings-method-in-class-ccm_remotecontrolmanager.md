---
title: GetRemCtrlSettings Method
description: The GetRemCtrlSettings Windows Management Instrumentation (WMI) class method in Configuration Manager that gets the remote control settings on a client computer.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b090c545-39e8-4e74-8b5b-d95a9a12ef29
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetRemCtrlSettings Method in Class CCM_RemoteControlManager
The `GetRemCtrlSettings` Windows Management Instrumentation (WMI) class method in Configuration Manager that gets the remote control settings on a client computer.    

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetRemCtrlSettings   
{  
    [IN]    UInt32 RemoteControlSettingsLoc  
    [OUT]   Boolean AllowClientChange  
    [OUT]   Boolean UseLocalSettings  
    [OUT]   Boolean RemoteControlEnabled  
    [OUT]   Boolean AllowRemCtrlToUnattended  
    [OUT]   Boolean PermissionRequired  
    [OUT]   UInt32 AccessLevel  
    [OUT]   UInt32 AudibleSignal  
    [OUT]   Boolean ConnectionBar  
    [OUT]   Boolean TaskbarIcon  
};  
```  

## Parameters  
 `RemoteControlSettingsLoc`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 RemoteControlSettingsLoc.    

 `AllowClientChange`  
 Data type: `Boolean`  

 Qualifiers: [id("1"), out]  

 `true` if users can change policy or notification settings in Software Center.     

 `UseLocalSettings`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), out]  

 `true` if Remote Assistance settings, which the user can configure in a Control Panel program, is going to get overridden by the Configuration Manager settings.    

 `RemoteControlEnabled`  
 Data type: `Boolean`  

 Qualifiers: [id("3"), out]  

 `true` if the remote control agent is enabled.   

 `AllowRemCtrlToUnattended`  
 Data type: `Boolean`  

 Qualifiers: [id("4"), out]  

 `true` if the user should be prompted for permission to remote control the computer.   

 `PermissionRequired`  
 Data type: `Boolean`  

 Qualifiers: [id("5"), out]  

 `true` if permission is required before starting a remote control session.    

 `AccessLevel`  
 Data type: `UInt32`  

 Qualifiers: [id("6"), out]  

 Access level allowed. Possible values are:   

|Value|Access level|  
|-|-|  
|0|No access|  
|1|View only|  
|2|Full control|  

 `AudibleSignal`  
 Data type: `UInt32`  

 Qualifiers: [id("7"), out]  

 Value indicating if a control beep should be sounded during a remote control session to signify that the computer is being remotely controlled. This is only for Remote Control, not Remote Assistance. Possible values are:   

|Value|Remote control beep|  
|-|-|  
|0|None|  
|1|Beginning and end of session|  
|2|Repeatedly|  

 `ConnectionBar`  
 Data type: `Boolean`  

 Qualifiers: [id("8"), out]  

 `true` to show the session connection bar.    

 `TaskbarIcon`  
 Data type: `Boolean`  

 Qualifiers: [id("9"), out]  

 `true` to show the session notification icon on the taskbar.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
