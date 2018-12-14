---
title: "SMS_MDMBulkEnrollmentPackages Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cf35074c-b179-4511-b824-27ef758bdb05
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_MDMBulkEnrollmentPackages Server WMI Class
The  `SMS_MDMBulkEnrollmentPackages` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents On-premises Mobile Device Management  (MDM) bulk enrollment packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMBulkEnrollmentPackages : SMS_BaseClass  
{  
    String CertificateId;  
    DateTime CreationTime;  
    DateTime ExpiryTime;  
    UInt32 Package_ID;  
    String PackageName;  
    UInt32 Profile_ID;  
    String  Profile_UniqueID;  
    String ProfileName;  
    UInt32 State;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_MDMBulkEnrollmentPackages` class.  

|Method|Description|  
|------------|-----------------|  
|[ImportForProfile Method in Class SMS_MDMBulkEnrollmentPackages](../../../develop/reference/mdm/importforprofile-method-in-class-sms_mdmbulkenrollmentpackages.md)|Imports an MDM bulk enrollment package for a profile.|  

## Properties  
 `CertificateId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique certificate ID, as a GUID.  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time the package was created.  

 `ExpiryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time the package expires.  

 `Package_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Package ID.  

 `PackageName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Package name.  

 `Profile_ID`  
 Data type: `uint32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Profile ID.  

 `Profile_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, not_null]  

 Unique ID of the Profile.  

 `ProfileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Profile name.  

 `State`  
 Data type: `uint32`  

 Access type: Read/Write  

 Qualifiers: none  

 State of the package.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)   
 [Configuration Manager Hybrid Server WMI Classes](../../../develop/reference/mdm/hybrid-server-wmi-classes.md)
