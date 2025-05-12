---
title: SetRemCtrlSettings Method
titleSuffix: Configuration Manager
description: The SetRemCtrlSettings WMI class method specifies the remote control settings on a client computer.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: df307c37-020a-4972-8d7a-df0a57377ead
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SetRemCtrlSettings Method in Class CCM_RemoteControlManager
The `SetRemCtrlSettings` Windows Management Instrumentation (WMI) class method in Configuration Manager that specifies the remote control settings on a client computer.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 SetRemCtrlSettings   
{  
    [IN]    Boolean UseLocalSettings  
    [IN]    Boolean RemoteControlEnabled  
    [IN]    Boolean AllowRemCtrlToUnattended  
    [IN]    Boolean PermissionRequired  
    [IN]    UInt32 AccessLevel  
    [IN]    UInt32 AudibleSignal  
    [IN]    Boolean ConnectionBar  
    [IN]    Boolean TaskbarIcon  
};  
```  

## Parameters  
 `UseLocalSettings`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), in]  

 `true` if Remote Assistance settings, which the user might configure in a Control Panel program, should be overridden by the Configuration Manager settings.    

 `RemoteControlEnabled`  
 Data type: `Boolean`  

 Qualifiers: [id("1"), in]  

 `true` if the remote control agent is enabled.   

 `AllowRemCtrlToUnattended`  
 Data type: `Boolean`  

 Qualifiers: [id("2"), in]  

 `true` if remote control of an unattended computer is allowed.    

 `PermissionRequired`  
 Data type: `Boolean`  

 Qualifiers: [id("3"), in]  

 `true` if the user should be prompted for permission to remote control the computer.   

 `AccessLevel`  
 Data type: `UInt32`  

 Qualifiers: [id("4"), in]  

 Access level allowed. Possible values are:   

|Value|Access level|  
|-|-|  
|0|No access|  
|1|View only|  
|2|Full control|  

 `AudibleSignal`  
 Data type: `UInt32`  

 Qualifiers: [id("5"), in]  

 Value indicating if a control beep should be sounded during a remote control session to signify that the computer is being remotely controlled. This beep is only for Remote Control, not Remote Assistance. Possible values are:   

|Value|Remote control beep|  
|-|-|  
|0|None|  
|1|Beginning and end of session|  
|2|Repeatedly|  

 `ConnectionBar`  
 Data type: `Boolean`  

 Qualifiers: [id("6"), in]  

 `true` to show the session connection bar.    

 `TaskbarIcon`  
 Data type: `Boolean`  

 Qualifiers: [id("7"), in]  

 `true` to show the session notification icon on the taskbar.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
