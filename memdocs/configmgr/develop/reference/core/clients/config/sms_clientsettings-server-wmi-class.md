---
description: Learn how to represent the settings that apply to the clients which belong to a specified collection using SMS_ClientSettings class.
title: "SMS_ClientSettings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f46e48ff-60cd-4a68-a36e-9ece153d93c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientSettings Server WMI Class
The `SMS_ClientSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the settings that apply to the clients which belong to a specified collection. These settings override the default client settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientSettings : SMS_ClientSettingsBase  
{  
    SMS_ClientAgentConfig_BaseClass AgentConfigurations[];  
    UInt32 AssignmentCount;  
    String CreatedBy;  
    DateTime DateCreated;  
    DateTime DateModified;  
    String Description;  
    Boolean Enabled;  
    UInt32 FeatureType;  
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
 The following table lists the methods in the `SMS_ClientSettings` class.  

|Method|Description|  
|------------|-----------------|  
|[CheckPortalUrl Method for Class SMS_ClientSettings](../../../../../develop/reference/core/clients/config/checkportalurl-method-for-class-sms_clientsettings.md)|Checks whether the default application catalog website point in the default or custom client agent settings is set to `portalUrl`.|  

## Properties  
 `AgentConfigurations`  
 Data type: `SMS_ClientAgentConfig_BaseClass` Array  

 Access type: Read/Write  

 Qualifiers: none  

 `AgentConfigurations` is an array of type `SMS_ClientAgentConfig_BaseClass`. Many classes for individual features inherit from `SMS_ClientAgentConfig_BaseClass`. For example, `SMS_StateSystemConfig` and `SMS_HardwareInventoryAgentConfig`. You use these individual SMS_*Config classes to define the value of settings for their feature. The default value is null for `AgentConfigurations`.  

 `AssignmentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The count that how many collections are assigned to this setting. The default value is 0.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit]  

 Name of the user that created the client settings.  

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

 User defined description of the setting. The default value is \<null>.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Reserved for future use.  

 `FeatureType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Indicates if the settings are applied to regular `SMS_ClientSettings` or `SMS_AntimalwareSettings`. The default value is 2 when you create `SMS_ClientSettings`. Possible values are:  

|Value|Settings type|  
|-|-|  
|1|SMS_AntimalwareSettings|  
|2|SMS_ClientSettings|  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Reserved for future use.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read, sizelimit]  

 Name of the user that last modified the client settings.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [notnull]  

 Name of the component.  

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

|Value|Settings type|  
|-|-|  
|1|Device|  
|2|User|  

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
