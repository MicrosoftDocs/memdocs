---
title: "SMS_BoundaryGroup Class"
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
ms.assetid: 6c6cea04-987d-4ace-8ac4-7414493efb70searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_BoundaryGroup Server WMI Class
The `SMS_BoundaryGroup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a boundary group defined in the site hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BoundaryGroup : SMS_BaseClass  
{  
    String CreatedBy;  
    DateTime CreatedOn;  
    String DefaultSiteCode;  
    String Description;  
    UInt32 GroupID;  
    UInt32 MemberCount;  
    String ModifiedBy;  
    DateTime ModifiedOn;  
    String Name;  
    Boolean Shared;  
    UInt32 SiteSystemCount;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_BoundaryGroup` class.  

|Method|Description|  
|------------|-----------------|  
|[AddBoundary Method in Class SMS_BoundaryGroup](../../../../../develop/reference/core/servers/configure/addboundary-method-in-class-sms_boundarygroup.md)|Adds boundaries to this boundary group.|  
|[AddSiteSystem Method in Class SMS_BoundaryGroup](../../../../../develop/reference/core/servers/configure/addsitesystem-method-in-class-sms_boundarygroup.md)|Adds a site system to this boundary group.|  
|[RemoveBoundary Method in Class SMS_BoundaryGroup](../../../../../develop/reference/core/servers/configure/removeboundary-method-in-class-sms_boundarygroup.md)|Removes boundaries from this boundary group.|  
|[RemoveSiteSystem Method in Class SMS_BoundaryGroup](../../../../../develop/reference/core/servers/configure/removesitesystem-method-in-class-sms_boundarygroup.md)|Removes site systems from this boundary group.|  

## Properties  
 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User that created the boundary group.  

 `CreatedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the boundary group was created.  

 `DefaultSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("3")]  

 Site code new clients will be auto assigned to.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for the boundary group.  

 `GroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Auto-generated unique identifier for the boundary group.  

 `MemberCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of boundaries in the boundary group.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User that last modified the boundary group.  

 `ModifiedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the boundary group was last modified.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, unique]  

 Name of the boundary group.  

 `Shared`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this boundary group was created by migration manager for a shared distribution point.  

 `SiteSystemCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site system count.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
