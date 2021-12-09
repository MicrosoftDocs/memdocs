---
title: "MoveFolders Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bc248af9-a09e-42cc-aceb-2a465e20d3f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# MoveFolders Method in Class SMS_ObjectContainerNode
The `MoveFolders` Windows Management (WMI) class method, in Configuration Manager, moves folders to another folder location.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 MoveFolders(  
      UInt32 ContainerNodeIDs[],  
      UInt32 TargetContainerNodeID,   
);  
```  

#### Parameters  
 `ContainerNodeIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of the folders, or nodes, to move.  

 `TargetContainerNodeID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The ID for the destination folder, or node.  

## Return Value  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ObjectContainerNode Server WMI Class](../../../../../develop/reference/core/servers/console/sms_objectcontainernode-server-wmi-class.md)   
