---
title: "SMS_CM_UpdatePackTopLevelMonitoring Class"
titleSuffix: "Configuration Manager"
description: "An SMS Provider server class that gets the top-level installation stages and status per site."
ms.date: "09/20/2016"
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b22bbfea-bf8e-4375-95b1-5fc2d021ded4
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3


---
# SMS_CM_UpdatePackTopLevelMonitoring Server WMI Class
The  `SMS_CM_UpdatePackTopLevelMonitoring` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is used to get the top level installation stages and status per site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackTopLevelMonitoring: SMS_BaseClass  
{  
    DateTime MessageTime;  
    String PackageGuid;  
    String SiteCode;  
    Sint32 SiteNumber;  
    Sint32 SiteType;  
    Sint32 StageCompleted;  
    Sint32 StageId;  
    String StageName;  
};  

```  

## Methods  
 The `SMS_CM_UpdatePackTopLevelMonitoring` class does not define any methods.  

## Properties  
 `MessageTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time that the message was created.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the update package.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the site.  

 `SiteNumber`  
 Data type: `Sint32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the site.  

 `SiteType`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The type of site to which the `SubStage` applies.  

 `StageCompleted`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Indicates whether the stage has completed.  

 `StageId`  
 Data type: `Sint32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The top-level stage with which the `SubStage` is associated.  

 `StageName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the stage.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
