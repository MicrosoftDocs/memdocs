---
title: "SMS_ClientAdvertisementSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bc249ca7-68d9-4e6a-965b-9428b68f9646
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientAdvertisementSummary Server WMI Class
The `SMS_ClientAdvertisementSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a summary for an advertisement.  

## Syntax  

```  
Class SMS_ClientAdvertisementSummary  
{  
      UInt32 Accepted;  
      UInt32 Activity1day;  
      UInt32 Activity30days;  
      UInt32 Activity7days;  
      UInt32 AdvertFlags;  
      String AdvertisementID;  
      String AdvertisementName;  
      UInt32 Failed;  
      UInt32 HealthyAccepted;  
      UInt32 HealthyFailed;  
      UInt32 HealthyNotStarted;  
      UInt32 HealthyRetrying;  
      UInt32 HealthyRunning;  
      UInt32 HealthySucceeded;  
      UInt32 HealthyTargeted;  
      UInt32 HealthyWaiting;  
      UInt32 NotStarted;  
      UInt32 PackageFlags;  
      String PackageID;  
      UInt32 Retrying;  
      UInt32 Running;  
      UInt32 Succeeded;  
      UInt32 Targeted;  
      UInt32 Waiting;  
};  
```  

## Methods  
 The `SMS_ClientAdvertisementSummary` class does not define any methods.  

## Properties  
 `Accepted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of targeted clients that have accepted the specified advertisement.  

 `Activity1day`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have reported activity for the specified advertisement in the last 24 hours.  

 `Activity30days`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have reported activity for the specified advertisement in the last 30 days.  

 `Activity7days`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have reported activity for the specified advertisement in the last 7 days.  

 `AdvertFlags`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [bits]  

 Flags indicating how the advertisement is announced to the user. Possible values are listed for the `AdvertFlags` property of [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md). The default value is 0.  

 `AdvertisementID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Unique auto-generated key that identifies the advertisement.  

 `AdvertisementName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Required. Unique user-friendly name for the advertisement.  

 `Failed`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have failed to run the specified advertisement.  

 `HealthyAccepted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that have accepted the specified advertisement.  

 `HealthyFailed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that have failed to run the specified advertisement.  

 `HealthyNotStarted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that have not yet started to run the specified advertisement.  

 `HealthyRetrying`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that have experienced errors executing the specified advertisement and are retrying.  

 `HealthyRunning`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that are currently running the specified advertisement.  

 `HealthySucceeded`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that have successfully run the specified advertisement.  

 `HealthyTargeted`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients for the specified advertisement. This count should equal the total of `Succeeded`, `Failed` , `Running`, `Retrying`, `NotStarted`, and `Waiting`.  

 `HealthyWaiting`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of healthy targeted clients that are currently waiting for something to finish before running the specified advertisement. These computers might be waiting for content to download or for another advertisement to finish.  

 `NotStarted`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have not yet started to run the specified advertisement.  

 `PackageFlags`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [enumeration]  

 Flags for the package. Possible values are listed below. The default value is 0.  

 0  
 Regular software distribution package.  

 3  
 Driver package.  

 4  
 Task sequence package.  

 5  
 Software update package.  

 6  
 Device setting package.  

 257  
 Image package.  

 258  
 Boot image package.  

 259  
 Operating system install package.  

 `PackageID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 The associated Configuration Manager package ID.  

 `Retrying`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have experienced errors executing the specified advertisement and are retrying.  

 `Running`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that are currently running the specified advertisement.  

 `Succeeded`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that have successfully run the specified advertisement.  

 `Targeted`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients for the specified advertisement. This count should equal the total of `Succeeded`, `Failed` , `Running`, `Retrying`, `NotStarted`, and `Waiting`.  

 `Waiting`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 The number of targeted clients that are currently waiting for something to finish before running the specified advertisement. These computers might be waiting for content to download or for another advertisement to finish.  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
