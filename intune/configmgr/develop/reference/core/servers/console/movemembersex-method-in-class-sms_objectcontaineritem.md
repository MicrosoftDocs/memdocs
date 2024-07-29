---
description: Learn how the MoveMembersEx Windows Management Instrumentation (WMI) class method, in Configuration Manager, moves folder items to another folder.
title: MoveMembersEx Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 4623e1b2-d5cf-4d91-a9d2-4f6b2e35dd7d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# MoveMembersEx Method in Class SMS_ObjectContainerItem
The `MoveMembersEx` Windows Management Instrumentation (WMI) class method, in Configuration Manager, moves folder items to another folder.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 MoveMembers(  
     String InstanceKeys[],  
     UInt32 ContainerNodeID,   
     UInt32 TargetContainerNodeID,   
     UInt32 ObjectTypeName,  
);  
```  

#### Parameters  
 `InstanceKeys`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Instance keys that identify the folder items to move.  

 `ContainerNodeID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the folder, or node, from which to copy the items.  

 `TargetContainerNodeID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the folder, or node, to which to move the items.  

 `ObjectTypeName`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The name of the object supported by the console folder.  

## Return Value  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 An item cannot be moved to a folder of a different type. The `ObjectType` properties of [SMS_ObjectContainerNode Server WMI Class](../../../../../develop/reference/core/servers/console/sms_objectcontainernode-server-wmi-class.md) and [SMS_ObjectContainerItem Server WMI Class](../../../../../develop/reference/core/servers/console/sms_objectcontaineritem-server-wmi-class.md) can be used to determine object types.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
