---
title: "SMS_DPStatusInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2d5a2e47-4b71-4c8e-a31b-7074bf467fcc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DPStatusInfo Server WMI Class
The `SMS_DPStatusInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point status information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPStatusInfo : SMS_BaseClass  
{  
    Boolean IsDPMonEnabled;  
    Boolean IsMulticast;  
    Boolean IsPullDP;  
    Boolean IsPXE;  
    DateTime LastStatusTime;  
    UInt32 MessageCount;  
    UInt32 MessageState;  
    String NALPath;  
    String Name;  
    UInt32 NumberErrors;  
    UInt32 NumberInProgress;  
    UInt32 NumberInstalled;  
    UInt32 NumberUnknown;  
    String Version;  
};  
```  

## Methods  
 The `SMS_DPStatusInfo` class does not define any methods.  

## Properties  
 `IsDPMonEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this distribution point is monitored by distribution point monitor.  

 `IsMulticast`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this distribution point  is multicast enabled.  

 `IsPullDP`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 `true` if this is a pull  distribution point.  

 `IsPXE`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this distribution point is PXE enabled.  

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time of the last status message.  

 `MessageCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Count of the number of messages on this distribution point.  

 `MessageState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 State of the message.  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|Error|  

 `NALPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Distribution point NAL path.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the distribution point.  

 `NumberErrors`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Count of the failed content installations.  

 `NumberInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Count of the content installations in progress.  

 `NumberInstalled`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Count of the installed content.  

 `NumberUnknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Count of the unknown content.  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Version to which the distribution point is upgraded.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
