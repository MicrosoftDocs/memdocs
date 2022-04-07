---
title: "SMS_ClientSettingsDefault Class"
titleSuffix: "Configuration Manager"
description: "An SMS Provider server class that represents simple read-only default client settings properties."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7519ce9f-c724-4985-808f-24268cfeb60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientSettingsDefault Server WMI Class
The `SMS_ClientSettingsDefault` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents simple read-only default client settings properties.  

> [!NOTE]
>  Nothing in this class should be modified.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientSettingsDefault : SMS_BaseClass  
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
    UInt32 SettingsID;  
    String SiteCode;  
    UInt32 Type;  
    String UniqueID;  
};  
```  

## Methods  
 The `SMS_ClientSettingsDefault` class does not define any methods.  

## Properties  
 `AssignmentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 `AssignmentCount` is 0 only. In general, the default client settings apply to all clients in the hierarchy, unless overridden by values defined in `SMS_ClientSettings` which applies to certain collections.  

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

 Description is specified internally.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Reserved for future use.  

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

 Compared to `SMS_ClientSettings`, the priority is the lowest for `SMS_ClientSettingsDefault` (highest number) and should not be changed.  

 `SettingsID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 For internal use only.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 Three-letter site code for the CAS site.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Type is used to indicate if this setting is 'Device', 'User' or 'Default'. For `SMS_ClientSettingsDefault`, it is 0 meaning 'Default'.  

|Value|Setting type|  
|-|-|  
|0|Default|  
|1|Device|  
|2|User|  

 `UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit("64")]  

 The unique ID of the object.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
