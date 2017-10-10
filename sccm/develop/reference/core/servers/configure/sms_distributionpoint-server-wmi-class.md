---
title: "SMS_DistributionPoint Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: f639d294-8617-43a8-adad-6fb2a4590a5esearchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DistributionPoint Server WMI Class
The `SMS_DistributionPoint` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a distribution point from which a given package has been distributed to clients.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionPoint : SMS_BaseClass   
{   
      Boolean BitsEnabled;   
      Boolean IsPeerDP;   
      Boolean IsProtected;   
      UInt8 ISVData[];   
      UInt32 ISVDataSize;   
      String ISVString;  
      DateTime LastRefreshTime;   
      UInt32 ObjectTypeID;  
      String PackageID;   
      UInt32 PackageType;  
      Boolean RefreshNow;   
      String ResourceType;   
      String SecureObjectID;  
      String ServerNALPath;   
      String SiteCode;   
      String SiteName;   
      String SourceSite;   
      UInt32 Status;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_DistributionPoint` class.  

|Method|Description|  
|------------|-----------------|  
|[VerifyPackage Method in Class SMS_DistributionPoint](../../../../../develop/reference/core/servers/configure/verifypackage-method-in-class-sms_distributionpoint.md)|Verifies the integrity of the package.|  
|[CancelDistribution Method in Class SMS_DistributionPoint](../../../../../develop/reference/core/servers/configure/canceldistribution-method-in-class-sms_distributionpoint.md)|Cancels the distribution of a package.|  

## Properties  
 `BitsEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the distribution point is BITS-enabled. The default value is `false`.  

 `IsPeerDP`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the distribution point is a branch distribution point. The default value is `false`.  

 `IsProtected`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the distribution point site system is protected. The default value is `false`.  

 `ISVData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 Values allow a single ISV to store data that relates to the [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) object associated with the package. For more information, see the Remarks section later in this topic.  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size of the data indicated by `ISVData`. The default value is 0.  

 `ISVString`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 String for partner extensibility.  

 `LastRefreshTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of when the package was last updated on the distribution server. The default value is "19900101000000.000000+***".  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object class ID.  

|||  
|-|-|  
|2|SMS_Package|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  
|23|SMS_DriverPackage|  
|24|SMS_SoftwareUpdatesPackage|  
|31|SMS_Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for the package that was distributed to this distribution point. The default value is "".  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 The type of package.  

|Value|Description|  
|-----------|-----------------|  
|0|Regular software distribution package.|  
|3|Driver package.|  
|4|Task sequence package.|  
|5|Software update package.|  
|6|Device setting package.|  
|257|Image package.|  
|258|Boot image package.|  
|259|Operating system install package.|  

 `RefreshNow`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to signal Configuration Manager to update the package on the distribution point. The update is distribution point-specific and is equivalent to the **Refresh Distribution Point** action in the Configuration Manager console. This package update copies the latest content from the source of the package to a specific distribution point, so that the distribution point has the latest version. The source version of the package is not incremented, and the package content is not replicated to child sites. The default value is `false`.  

 `ResourceType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The resource type of the distribution point. The default value is "".  

 `SecureObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Security object key. For application, it's CI_UniqueID. For package, it's PackageID.  

 `ServerNALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Network abstraction layer (NAL) path to the distribution point server. The default value is "". For more information, see the Remarks section later in this topic.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 Site code of the site that this distribution point belongs to. The default value is "".  

 The value that is furnished for this property must match the value of `ServerNALPath`. Your application retrieves the value from [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md). For more information, see the Remarks section later in this topic.  

 `SiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Friendly name of the site where the package originates. The default value is "".  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 Site code of the site where the package originates. The default value is "".  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Current status of the package on the distribution point. Possible values are listed below. For more information, see the Remarks section later in this topic.  

|||  
|-|-|  
|0|NONE|  
|1|UPDATED|  
|2|ADDED|  
|3|DELETED|  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 A distribution point is always associated with a particular package, and a package can have several distribution points.  

 Your application cannot change the `PackageID` property after the distribution point is created. To associate the distribution point with a different package, the application must delete the `SMS_DistributionPoint` object and create a new instance with a new `PackageID` value.  

 The [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md) class contains a list of the available distribution points and their NAL paths. Your application should select the `NALPath` property of `SMS_SystemResourceList` that corresponds to a `RoleName` property setting of "SMS Distribution Point".  

 When your application deletes an instance of `SMS_DistributionPoint`, the instance is not totally deleted until its related components are deleted. Instead, Configuration Manager sets the `Status` property to 3 (delete) to inform the application that the distribution point is marked for deletion. To ensure that a query does not retrieve distribution points that have been deleted (marked for deletion), your application should add this case to its WHERE clause.  

 There are no restrictions or defined formats for the data that is indicated by `ISVData`. However, it is important that after ISV ownership of this property has been established, it should not be overwritten. Therefore, the application should first read the existing data in this property. If the data does not belong to the caller, it should not be modified. Any ISV or application that is using this property should include an identifier in the data so that the ownership can be easily established.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)
