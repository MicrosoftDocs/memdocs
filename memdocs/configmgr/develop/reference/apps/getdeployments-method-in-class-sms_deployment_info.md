---
title: "GetDeployments Method"
titleSuffix: "Configuration Manager"
description: "The GetDeployments Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets advertisement identifier or Assignment identifier and related type for a deployment that is deployed to the specified resource."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6545ae78-95b6-48b6-b8ba-c09046b6cc31
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetDeployments Method in Class SMS_Deployment_Info
The `GetDeployments` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets advertisement identifier or Assignment identifier and related type for a deployment that is deployed to the specified resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetDeployments(  
     uint32 ResourceID,  
     string DeploymentIDs[],  
     uint32 DeploymentTypeID[]  
);  
```  

#### Parameters  
 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Configuration Manager supplied ID for the resource. This ID is not unique across sites.  

 `DeploymentIDs`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Unique auto-generated key for the deployment.  

 `DeploymentTypeID`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Type identifier of the deployment.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
