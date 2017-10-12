---
title: "DeleteAssociation Method"
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
ms.assetid: 9b318231-7072-428e-9201-5fbdc8ba8d1csearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# DeleteAssociation Method in Class SMS_StateMigration
The `DeleteAssociation` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes the computer association between two system resources used in state migration.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 DeleteAssociation(  
      UInt32 SourceClientResourceID,  
      UInt32 RestoreClientResourceID  
);  
```  

#### Parameters  
 `SourceClientResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Resource ID for the source client.  

 `RestoreClientResourceID`  
 Data type: `uint32`  

 Qualifiers: [in]  

 Resource ID for the destination client.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application uses this method to remove an association that has been created by using a call to the [AddAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)   
 [AddAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md)
