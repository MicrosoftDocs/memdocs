---
title: SMS_ObjectContainerItem Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that contains information about a Configuration Manager console folder item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: bfa25626-733e-4023-98b2-e1ff3ee18255
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ObjectContainerItem Server WMI Class
The `SMS_ObjectContainerItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager that contains information about a Configuration Manager console folder item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectContainerItem : SMS_BaseClass  
{  
    UInt32 ContainerNodeID;  
    String InstanceKey;  
    String MemberGuid;  
    UInt32 MemberID;  
    UInt32 ObjectType;  
    String ObjectTypeName;  
    String SourceSite;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ObjectContainerItem` class.  

|Method|Description|  
|------------|-----------------|  
|[MoveMembers Method in Class SMS_ObjectContainerItem](../../../../../develop/reference/core/servers/console/movemembers-method-in-class-sms_objectcontaineritem.md)|Moves one or more folder items to another folder.|  
|[MoveMembersEx Method in Class SMS_ObjectContainerItem](../../../../../develop/reference/core/servers/console/movemembersex-method-in-class-sms_objectcontaineritem.md)|Moves one or more folder items to another folder.|  

## Properties  
 `ContainerNodeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The unique ID of the folder.  

 `InstanceKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The name of the folder.  

 `MemberGuid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The guid of the relation.  

 `MemberID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 The unique ID of the relation.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [deprecated, enumeration, read]  

 The type of the folder. Possible values are listed below.  

| Value | Object type |
| ----- | ----------- |
|2|TYPE_PACKAGE|  
|3|TYPE_ADVERTISEMENT|  
|7|TYPE_QUERY|  
|8|TYPE_REPORT|  
|9|TYPE_METEREDPRODUCTRULE|  
|11|TYPE_CONFIGURATIONITEM|  
|14|TYPE_OSINSTALLPACKAGE|  
|17|TYPE_STATEMIGRATION|  
|18|TYPE_IMAGEPACKAGE|  
|19|TYPE_BOOTIMAGEPACKAGE|  
|20|TYPE_TASKSEQUENCEPACKAGE|  
|21|TYPE_DEVICESETTINGPACKAGE|  
|23|TYPE_DRIVERPACKAGE|  
|25|TYPE_DRIVER|  
|1011|TYPE_SOFTWAREUPDATE|  
|2011|TYPE_CONFIGURATIONBASELINE|
|5000|TYPE_DEVICE_COLLECTION|
|5001|TYPE_USER_COLLECTION|

 `ObjectTypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The WMI Class Name of the object. Example SMS_Package. This will take effect if the ObjectType is 0 or null.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The sitecode of the site that the relation was originally created from.  

## Remarks  
When attempting to move an item from a root node such as a user collection or device collection, the item doesn't exist as an SMS_ObjectContainerItem. As such a new instance will need to be created instead.
## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
