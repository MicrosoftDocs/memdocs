---
title: "SMS_PackageContentServerInfo Class"
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
ms.assetid: 401b63f0-8868-46ab-a935-9bdd9d307156searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_PackageContentServerInfo Server WMI Class
The `SMS_PackageContentServerInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents information about a given distribution point where an application or package has been distributed.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageContentServerInfo : SMS_BaseClass  
{  
    String ContentServerID;  
    String ContentServerSecurityID;  
    UInt32 ContentServerType;  
    String Description;  
    UInt32 IsBitsEnabled;  
    UInt32 IsPeerDP;  
    String Name;  
    String ObjectID;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    UInt32 PackageType;  
};  
```  

## Methods  
 The `SMS_PackageContentServerInfo` class does not define any methods.  

## Properties  
 `ContentServerID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Distribution point group unique identifier.  

 `ContentServerSecurityID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Distribution point identifier or distribution point group identifier for security.  

 `ContentServerType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Type of content server.  

|||  
|-|-|  
|1|Distribution Point|  
|2|Distribution Point Group|  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of distribution point or distribution point group.  

 `IsBitsEnabled`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if BITS is enabled.  

 `IsPeerDP`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the distribution point is a branch distribution point.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of distribution point or distribution point group.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Package identifier or CI_UniqueID.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object class identifier. Possible values are:  

|||  
|-|-|  
|42|SMS_DistributionPointInfo|  
|43|SMS_DistributionPointGroup|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The type of the package. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|Regular software distribution package.|  
|3|Driver package.|  
|4|Task sequence package.|  
|5|Software update package.|  
|6|Content package.|  
|8|Device setting package.|  
|257|Image package.|  
|258|Boot image package.|  
|259|Operating system install package.|  
|512|Application package.|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
