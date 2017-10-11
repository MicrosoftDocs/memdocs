---
title: "SMS_DistributionPointGroup Class"
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
ms.assetid: 01cb6452-86e2-4af2-a851-7aa550ab7d7asearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DistributionPointGroup Server WMI Class
The `SMS_DistributionPointGroup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a group of distribution points rendered in the Configuration Manager console.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionPointGroup : SMS_BaseClass  
{  
    UInt32 CollectionCount;  
    UInt32 ContentCount;  
    Boolean ContentInSync;  
    String CreatedBy;  
    DateTime CreatedOn;  
    String Description;  
    String GroupID;  
    Boolean HasMember;  
    Boolean HasRelationship;  
    UInt32 MemberCount;  
    String ModifiedBy;  
    DateTime ModifiedOn;  
    String Name;  
    UInt32 OutOfSyncContentCount;  
    String SourceSite;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_DistributionPointGroup` class.  

|Method|Description|  
|------------|-----------------|  
|[AddDistributionPoints Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/adddistributionpoints-method-in-class-sms_distributionpointgroup.md)|Adds distribution points to this distribution point group.|  
|[AddPackages Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/addpackages-method-in-class-sms_distributionpointgroup.md)|Assigns a set of packages to the distribution point group.|  
|[AssociateCollections Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/associatecollections-method-in-class-sms_distributionpointgroup.md)|Associates a set of collections to this distribution point group.|  
|[DisassociateCollections Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/disassociatecollections-method-in-class-sms_distributionpointgroup.md)|Removes a set of associated collections from this distribution point group.|  
|[ReDistributePackage Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/redistributepackage-method-in-class-sms_distributionpointgroup.md)|Redistributes a package to all of the member distribution points.|  
|[RefreshDPGroup Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/refreshdpgroup-method-in-class-sms_distributionpointgroup.md)|Refreshes all of the member distribution points with the latest version of the targeted packages.|  
|[RemoveDistributionPoints Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/removedistributionpoints-method-in-class-sms_distributionpointgroup.md)|Removes distribution points from this distribution point group.|  
|[RemovePackages Method in Class SMS_DistributionPointGroup](../../../../../develop/reference/core/servers/configure/removepackages-method-in-class-sms_distributionpointgroup.md)|Removes a set of packages from this distribution point group.|  

## Properties  
 `CollectionCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Associated collection count.  

 `ContentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Associated content count.  

 `ContentInSync`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 Whether or not all the contents synchronized.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the user who created the distribution point group.  

 `CreatedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the distribution point group was created.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for the distribution point group.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Auto-generated unique identifier.  

 `HasMember`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if there is distribution point in this distribution point group.  

 `HasRelationship`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if there is collection associated with this distribution point group.  

 `MemberCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of members of this distribution point group.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the user who modified the distribution point group.  

 `ModifiedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the distribution point group was last modified.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, unique]  

 Name of this distribution point group.  

 `OutOfSyncContentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of out of sync content.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit("3")]  

 Source site for the distribution point group.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_NAL_Methods Server WMI Class](../../../../../develop/reference/misc/sms_nal_methods-server-wmi-class.md)
