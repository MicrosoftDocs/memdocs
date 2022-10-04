---
title: SMS_DistributionPointInfo class
titleSuffix: Configuration Manager
description: An SMS Provider server class that provides information about a specific SMS_DistributionPoint server WMI class object.
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: aa3fabb4-c0b4-4a99-a8c3-0889e8c99491
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_DistributionPointInfo server WMI class

The `SMS_DistributionPointInfo` WMI class is an SMS Provider server class in Configuration Manager. It provides information about a specific [SMS_DistributionPoint server WMI class](sms_distributionpoint-server-wmi-class.md) object.  

## Syntax  

```MOF
Class SMS_DistributionPointInfo : SMS_BaseClass
{
      Boolean AddressScheduleEnabled;  
      String BindExcept;  
      Boolean BindPolicy;  
      Boolean BitsEnabled;
      Boolean CertificateType;  
      UInt32 Communication;  
      String Description;
      UInt32 DPFlags;  
      String Drive;
      UInt32 GroupCount;  
      Boolean HasRelationship;  
      Boolean HealthCheckEnabled;  
      UInt32 HealthCheckPriority;  
      String HealthCheckSchedule;  
      UInt32 ID;  
      String IdentityGUID;  
      Boolean InternetFacing;  
      Boolean IsActive;  
      Boolean IsMulticast;  
      Boolean IsPeerDP;
      Boolean IsProtected;
      Boolean IsPullDP;
      Boolean IsPXE;  
      String NALPath;
      String Name;  
      String OperatingSystem;  
      UInt32 Priority;  
      Boolean PreStagingAllowed;  
      String PXEPassword;  
      Boolean RateLimitsEnabled;  
      UInt32 Region;  
      String ResourceType;
      UInt32 ResponseDelay;  
      String ServerName;
      String ServiceType;
      String ShareName;
      String SiteCode;
      String SiteName;
      Boolean SupportUnknownMachines;  
      UInt32 TransferRate;  
      UInt32 UdaSetting;  
};  
```  

## Methods

The following table lists the methods in the `SMS_DistributionPointInfo` class.  

|Method|Description|  
|-|-|  
|[GetChainedPullDPs Method in Class SMSDistributionPointInfo](getchainedpulldps-method-in-class-smsdistributionpointinfo.md)|Ensures that when a source distribution point is assigned, a looping chain is not generated.|  
|[SetDPMaintenanceMode method in class SMS_DistributionPointInfo](setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)|Starting in version 1902, put a distribution point in maintenance mode.|


## Properties

### `AddressScheduleEnabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if a schedule on this address is configured.  

### `BindExcept`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

PXE bind exception.  

### `BindPolicy`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

PXE bind policy.  

### `BitsEnabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

`true` if the distribution point is BITS-enabled. The default value is `false`.  

### `CertificateType`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

PXE certificate type.  

### `Communication`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

HTTP or HTTPS. The default value is 0.  

### `Description`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Description of the distribution point.  

### `DPFlags`

Data type: `UInt32`  

Access type: Read-only  

Qualifiers: [enumeration, read]  

Distribution point flags.  

|Value|Distribution point flag|  
|-|-|  
|0|DP_TYPE_READONLY|  

### `Drive`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Drive that's to be used by the distribution point. The default value is "".  

### `GroupCount`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

Count of distribution point groups that have this distribution point.  

### `HasRelationship`

Data type: `Boolean`  

Access type: Read-only  

Qualifiers: [read]  

`true` if this distribution point is assigned to a distribution point group.  

### `HealthCheckEnabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if health check on this distribution point is enabled.  

### `HealthCheckPriority`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

Distribution point health thread manager thread priority. The default value is 4.  

### `HealthCheckSchedule`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

Schedule for health check.  

### `ID`

Data type: `UInt32`  

Access type: Read-only  

Qualifiers: [read]  

Distribution point ID. This value is stored in the database. The default value is 0.  

### `IdentityGUID`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

The distribution point identity, generated at the distribution point installation time. It's a GUID in `ClientKeyData` that identifies the distribution point. The GUID is associated with a certificate.  

### `InternetFacing`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if this distribution point is internet-facing. The default value is `false`.  

### `IsActive`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if this PXE is active. The default value is `false`.  

### `IsMulticast`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if multicast is enabled on this distribution point. The default value is `false`.  

### `IsPeerDP`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

`true` if the distribution point is a branch distribution point. The default value is `false`.  

### `IsProtected`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

`true` if the distribution point site system is protected. The default value is `false`.  

### `IsPullDP`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if the distribution point is a pull distribution point. The default value is `false`.  

### `IsPXE`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if PXE is enabled. The default value is `false`.  

### `NALPath`

Data type: `String`  

Access type: Read/Write  

Qualifiers: [key]  

Network abstraction layer (NAL) path to the distribution point. The default value is "".  

### `Name`

Data type: `String`  

Access type: Read-only  

Qualifiers: [read]  

Network operating system path.  

### `OperatingSystem`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

The OS of this computer.  

### `PreStagingAllowed`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if pre-staging is allowed.  

### `Priority`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

Distribution priority. The default value is 1.  

### `PXEPassword`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

PXE password. The default value is "".  

### `RateLimitsEnabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if rate limits are enabled.  

### `Region`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

The Azure region in which the cloud-based distribution point resides.  

### `ResourceType`

Data type: `String`  

Access type: Read/Write  

Qualifiers: [key]  

Resource type of the distribution point. The default value is "". The possible values are:

- Server  

- Server share  

### `ResponseDelay`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

PXE response delay.  

### `ServerName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Server name of the distribution point computer. The default value is "".  

### `ServiceType`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

Service type. For cloud-based distribution points only.  

### `ShareName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Obsolete. Shared distribution points aren't supported in Configuration Manager.  

### `SiteCode`

Data type: `String`  

Access type: Read/Write  

Qualifiers: [key, SizeLimit("3")]  

Site code of the site that owns the distribution point. The default value is "".  

### `SiteName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Site name. The default value is "".  

### `SupportUnknownMachines`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if PXE supports unknown computers. The default value is `false`.  

### `TransferRate`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

The average transfer rate in Kbps. The default value is 0.  

### `UdaSetting`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

PXE user-device affinity (UDA) setting.  


## Remarks

Class qualifiers for this class include:  

- Read (read-only)  

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../misc/class-and-property-qualifiers.md).  


## Requirements  

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../core/reqs/server-runtime-requirements.md).  

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../../core/reqs/server-development-requirements.md).


## See also

- [SMS_DistributionPoint server WMI class](sms_distributionpoint-server-wmi-class.md)
