---
title: "SMS_CM_UpdatePackDetailedMonitoring Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0707d893-72e6-4fe5-8da2-2954e558ea13
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CM_UpdatePackDetailedMonitoring Server WMI Class
The `SMS_CM_UpdatePackDetailedMonitoring` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is used get the detailed update package installation status per site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackDetailedMonitoring: SMS_BaseClass  
{  
    SInt32 Applicable;  
    String Description;  
    SInt32 IsComplete;  
    DateTime MessageTime;  
    SInt32 OrderId;  
    String PackageGuid;  
    SInt32 Progress;  
    String SiteCode;  
    SInt32 SiteInstallID;  
    SInt32 SiteNumber;  
    SInt32 SiteType;  
    SInt32 StageId;  
    SInt32 SubStageid;  
    String SubStageName;  
};  

```  

## Methods  
 The `SMS_CM_UpdatePackDetailedMonitoring` class does not define any methods.  

## Properties  
 `Applicable`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Indicates whether the `SubStage` is applicable.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 A description of the `SubStage`.  

 `IsComplete`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Indicates whether the  `SubStage` has completed.  

 `MessageTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time that the message was created.  

 `OrderId`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The order in which the `SubStages` are listed in the user interface.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the update package.  

 `Progress`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The progress of the `SubStage`.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the site.  

 `SiteInstallID`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [none]  

 The number of installation retires.  

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

 `StageId`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The top-level stage with which the `SubStage` is associated.  

 `SubStageid`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 Unique identifier of the installation `SubStage`.  

 `SubStageName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the `SubStage`.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
