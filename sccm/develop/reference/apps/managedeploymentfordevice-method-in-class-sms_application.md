---
title: "ManageDeploymentForDevice Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 08f1bef3-64b5-483a-8db9-95965e79b8edsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ManageDeploymentForDevice Method in Class SMS_Application
> [!WARNING]
>  This method is reserved for future use.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ManageDeploymentForDevice (  
     String   AssignmentUniqueID,  
     String   ClientGUID,  
     UInt32   Action  
);  

```  

#### Parameters  
 `AssignmentUniqueID`  
 Data type: `String`  

 Qualifiers: [in]  

 Identifier for the application deployment.  

 `ClientGUID`  
 Data type: `String`  

 Qualifiers: [in]  

 Unique identifier of a client.  

 `Action`  
 Data type: `UInt32`  

 Qualifiers: [in, enumeration]  

 Activate or deactivate deployment. Possible values are:  

|||  
|-|-|  
|1|Activate|  
|2|Deactivate|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
 [Configuration Manager Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
