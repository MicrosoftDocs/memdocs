---
title: "SMS_MDMBulkEnrollmentProfiles Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 57c1746d-4ee1-41db-b7a8-33dad15e2b96
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_MDMBulkEnrollmentProfiles Server WMI Class
The  `SMS_BulkEnrollmentProfiles` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents On-premises Mobile Device Management  (MDM)  bulk enrollment profiles.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMBulkEnrollmentProfiles : SMS_BaseClass  
{  
    String Certificate_CI_UniqueID;  
    Bool CRLCheckEnabled;  
    UInt32 EnrolledDeviceCount;  
    UInt32 EnrollmentProxyPointType;  
    String EnrollmentProxyPointUrl;  
    String MDMSiteCode  
    UInt32 Profile_ID;  
    String Profile_UniqueID;  
    String ProfileDescription;  
    String ProfileName;  
    UInt32 ProfileType;  
    UInt32 ProfileVersion;  
    UInt32 ProxyPort;  
    String ProxyServer;  
    UInt32 Status;  
    String Wifi_CI_UniqueID;  
};  

```  

## Methods  
 The `SMS_MDMBulkEnrollmentProfiles`  class does not define any methods.  

## Properties  
 `Certificate_CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique ID for a certificate configuration item.  

 `CRLCheckEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if certificate revocation list (CRL) check is  enabled.  

 `EnrolledDeviceCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of enrolled devices.  

 `EnrollmentProxyPointType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies the type of URL for all enrollment proxy points. Possible values are:  

|||  
|-|-|  
|0|NONE|  
|1|INTERNET|  
|2|INTRANET|  

 `EnrollmentProxyPointUrl`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Enrollment proxy point URL.  

 `MDMSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The MDM site code.  

 `Profile_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The profile ID.  

 `Profile_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, not_null]  

 Unique ID of the profile.  

 `ProfileDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The description of the profile.  

 `ProfileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the profile.  

 `ProfileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The profile type.  

 `ProfileVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The version of the profile.  

 `ProxyPort`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The proxy port number.  

 `ProxyServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The proxy server.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The status.  

 `Wifi_CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique ID for a Wi-Fi configuration item.  

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
