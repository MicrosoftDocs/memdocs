---
title: "SMS_MDMCorpEnrollmentProfiles Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e56a838-3a52-45c7-9f6d-62e2a199ea94searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MDMCorpEnrollmentProfiles Server WMI Class
The `SMS_MDMCorpEnrollmentProfiles` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents On-premises Mobile Device Management (MDM) corporate enrollment profiles.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMCorpEnrollmentProfiles : SMS_BaseClass  
{  
    String ConfigurationUrl;  
    DateTime CreationTime;  
    String Department;  
    String Description;  
    UInt32 DeviceCount;  
    UInt32 EnrollmentProgram;  
    UInt32 IsDefault;  
    UInt32 IsUserChallenge;  
    DateTime ModifiedTime;  
    String Name;  
    UInt32 PlatformType;  
    String ProfileId;  
    String ProfileSettings;  
    UInt32 SupervisionMode;  
};  

```  

## Methods  
 The `SMS_MDMCorpEnrollmentProfiles`  class does not define any methods.  

## Properties  
 `ConfigurationUrl`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The configuration URL used for enrollment.  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time the enrollment profile was created.  

 `Department`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Department.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the enrollment profile.  

 `DeviceCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of devices associated with the profile.  

 `EnrollmentProgram`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Enrollment Program.  

 `IsDefault`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Is the enrollment profile the default.  

 `IsUserChallenge`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Profile is user challenged.  

 `ModifiedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time the enrollment profile was modified.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the enrollment profile.  

 `PlatformType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Platform Type.  

 `ProfileId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Enrollment profile ID.  

 `ProfileSettings`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The enrollment profile settings.  

 `SupervisionMode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Profile mode is supervised or not supervised for iOS.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)   
 [Configuration Manager Hybrid Server WMI Classes](../../../develop/reference/mdm/hybrid-server-wmi-classes.md)
