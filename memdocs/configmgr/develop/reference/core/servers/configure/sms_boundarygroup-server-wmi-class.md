---
title: SMS_BoundaryGroup Class
titleSuffix: Configuration Manager
description: The SMS_BoundaryGroup WMI class is an SMS Provider server class that represents a boundary group defined in the site hierarchy.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6c6cea04-987d-4ace-8ac4-7414493efb70
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
    UInt64 Flags;  
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

 `Flags`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none

 Boundary group property flags.  

 |Value|Execution context|  
 |-|-|  
 |0|Allow peer downloads in this boundary group|  
 |1|Allow peer downloads in this boundary group **is not enabled**|  
 |2|During peer downloads, only use peers within the same subnet|  
 |4|Prefer distribution points over peers within the same subnet|  
 |8|Prefer cloud based sources over on-premises sources|  

 > [!NOTE]
 > These are binary flags. So multiple can be set at once. E.g. if a value of 6 is shown, then the first 3 are enabled.

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
