---
title: "SMS_Boundary Class"
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
ms.assetid: b4026ec4-a938-4866-a3d0-e001582a7504searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Boundary Server WMI Class
The `SMS_Boundary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a boundary defined within the hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Boundary : SMS_BaseClass  
{  
    UInt32 BoundaryFlags;  
    UInt32 BoundaryID;  
    UInt32 BoundaryType;  
    String CreatedBy;  
    DateTime CreatedOn;  
    String DefaultSiteCode[];  
    String DisplayName;  
    UInt32 GroupCount;  
    String ModifiedBy;  
    DateTime ModifiedOn;  
    String SiteSystems[];  
    String Value;  
};  
```  

## Methods  
 The `SMS_Boundary` class does not define any methods.  

## Properties  
 `BoundaryFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is obsolete, use the `Flags` property in `SMS_BoundaryGroupSiteSystems` instead.  

 Specifies the connection type of the boundary. Possible values are:  

|||  
|-|-|  
|0|FAST|  
|1|SLOW|  

 `BoundaryID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique identifier of the boundary.  

 `BoundaryType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Boundary type.  

|||  
|-|-|  
|0|IPSUBNET|  
|1|ADSITE|  
|2|IPV6PREFIX|  
|3|IPRANGE|  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User that created the boundary.  

 `CreatedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the boundary was created.  

 `DefaultSiteCode`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site code new clients will be auto assigned to.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Display name of the boundary.  

 `GroupCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of boundary groups that have this boundary.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User that last modified the boundary.  

 `ModifiedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the boundary was last modified.  

 `SiteSystems`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site system machines within the boundary.  

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Boundary value.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
