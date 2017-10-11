---
title: "SMS_ClientSettingsBase Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 766a4537-74c1-43bd-b21f-8f028038635fsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ClientSettingsBase Server WMI Class
The `SMS_ClientSettingsBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents  the base class used by several client settings related classes (`SMS_AntimalwareSettings`, `SMS_ClientSettings`, and so on) for their simple properties.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientSettingsBase : SMS_BaseClass  
{  
    UInt32 AssignmentCount;  
    String CreatedBy;  
    DateTime DateCreated;  
    DateTime DateModified;  
    String Description;  
    Boolean Enabled;  
    UInt32 Flags;  
    String LastModifiedBy;  
    String Name;  
    UInt32 Priority;  
    String SecuredScopeNames[];  
    UInt32 SettingsID;  
    UInt32 Type;  
    String UniqueID;  
};  
```  

## Methods  
 The `SMS_ClientSettingsBase` class does not define any methods.  

## Properties  
 `AssignmentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Indicates how many collections are assigned to this client setting. The default value is 0.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit("512")]  

 Name of the user who created the client settings.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 The date and time when the client settings are created.  

 `DateModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 The date and time when the client settings are modified.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 An administrator generated description describing the settings configuration.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 `true` if the agent is enabled.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Reserved for future use.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit("512")]  

 Name of the user who last modified the client settings.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 The name of the component.  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Priority is used by the client to decide which value to take if the client belongs to more than one collection and multiple collections have client settings defined. The higher the number, the lower the relative priority to the client. All settings should have different priority numbers. The default value is the next available priority number.  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the security scopes with which the setting is associated. The default value is "Default".  

 `SettingsID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 For internal use only.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Type indicates whether the settings is applied to Device or User. The default value is 1 (Device).  

|||  
|-|-|  
|1|Device|  
|2|User |  

 `UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit("64")]  

 For internal use only.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
