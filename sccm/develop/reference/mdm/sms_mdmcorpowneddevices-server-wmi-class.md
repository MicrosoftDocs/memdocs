---
title: "SMS_MDMCorpOwnedDevices Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 564b7a4a-cc7c-4a56-a1cd-f4d21d4bda7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_MDMCorpOwnedDevices Server WMI Class
The `SMS_MDMCorpOwnedDevices` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents On-premises Mobile Device Management  (MDM)  corporate owned devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMCorpOwnedDevices : SMS_BaseClass  
{  
    DateTime ActualEnrollmentProfileAssignedTime;  
    String ActualEnrollmentProfileId;  
    String AssetTag;  
    String Color;  
    String Description;  
    String DeviceAssignedBy;  
    DateTime DeviceAssignedDate;  
    String DeviceId;  
    String DeviceName;  
    UInt32 DeviceType;  
    UInt32 DiscoverySources;  
    String EnrollmentPackageId;  
    UInt32 EnrollmentStatus;  
    UInt32 EnrollmentType;  
    String ExchangeDeviceId;  
    String IMEI;  
    DateTime LastUpdateTime;  
    String Model;  
    String OSVersion;  
    DateTime ProfileAssignedTime;  
    String ProfileName;  
    DateTime ProfilePushedTime;  
    UInt32 ProfileStatus;  
    String ProfileUuid;  
    DateTime RequestEnrollmentProfileAssignedTime;  
    String RequestEnrollmentProfileId;  
    String SerialNumber;  
    String UniqueId;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_MDMCorpOwnedDevices` class.  

|Method|Description|  
|------------|-----------------|  
|[UpdateProfileIDForDevices Method in Class SMS_MDMCorpOwnedDevices](../../../develop/reference/mdm/updateprofileidfordevices-method-in-class-sms_mdmcorpowneddevices.md)|Updates the profile IDs for device serial numbers.|  

## Properties  
 `ActualEnrollmentProfileAssignedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time that the device enrolled to the profile.  

 `ActualEnrollmentProfileId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The profile to which the device enrolled.  

 `AssetTag`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Asset tag of the device.  

 `Color`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Color of the device.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the device.  

 `DeviceAssignedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The Apple ID of the person who assigned the device.  

 `DeviceAssignedDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time stamp when the device was assigned to the MDM server.  

 `DeviceId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The device ID of the device  

 `DeviceName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the device.  

 `DeviceType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The platform of the device.  

 `DiscoverySources`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Discovery source of the device.  

 `EnrollmentPackageId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The enrollment package ID.  

 `EnrollmentStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Enrollment status of the device.  

 `EnrollmentType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The corporate enrollment type.  

 `ExchangeDeviceId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The Exchange device ID of the device.  

 `IMEI`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The IMEI number of the device.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time stamp when the device was last updated.  

 `Model`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model of the device.  

 `OSVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Operating system version on the device.  

 `ProfileAssignedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time at which the  profile was assigned.  

 `ProfileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the profile.  

 `ProfilePushedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time that the profile was pushed from Apple.  

 `ProfileStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Status of the profile from Apple.  

 `ProfileUuid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 UUID of the profile currently assigned to the device.  

 `RequestEnrollmentProfileAssignedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time that the profile was requested to be assigned to the device.  

 `RequestEnrollmentProfileId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The profile to which the device is assigned.  

 `SerialNumber`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Serial number of the device.  

 `UniqueId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique ID of a device.  

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
