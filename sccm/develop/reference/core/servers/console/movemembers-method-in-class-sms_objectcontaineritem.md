---
title: "MoveMembers Method"
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
ms.assetid: 55a605ba-93f2-4b63-b34e-a36d41659665searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# MoveMembers Method in Class SMS_ObjectContainerItem
The `MoveMembers` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, moves folder items to another folder.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 MoveMembers(  
     String InstanceKeys[],  
     UInt32 ContainerNodeID,   
     UInt32 TargetContainerNodeID,   
     UInt32 ObjectType,  
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

 `ObjectType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The type of object supported by the console folder.  

## Return Value  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 An item cannot be moved to a folder of a different type. The `ObjectType` properties of [SMS_ObjectContainerNode Server WMI Class](../../../../../develop/reference/core/servers/console/sms_objectcontainernode-server-wmi-class.md) and [SMS_ObjectContainerItem Server WMI Class](../../../../../develop/reference/core/servers/console/sms_objectcontaineritem-server-wmi-class.md) can be used to determine object types.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Console Extension](../../../../../develop/reference/core/servers/console/console-extension-server-wmi-classes.md)
