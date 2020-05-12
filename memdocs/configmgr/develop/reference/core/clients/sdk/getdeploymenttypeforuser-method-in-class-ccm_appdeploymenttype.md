---
title: "GetDeploymentTypeForUser Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 948b18b4-8925-4a63-9b7c-a2c8606fb4ce
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# GetDeploymentTypeForUser Method in Class CCM_AppDeploymentType
The `GetDeploymentTypeForUser` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that retrieves the application deployment type property for a user.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetDeploymentTypeForUser   
{  
    [IN]    String Id  
    [IN]    String Revision  
    [IN]    String User  
    [OUT]   Object DeploymentType  
};  
```  

## Parameters  
 `Id`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Identifier.    

 `Revision`  
 Data type: `String`  

 Qualifiers: [id("1"), in]  

 Revision.    

 `User`  
 Data type: `String`  

 Qualifiers: [id("2"), in]  

 User.    

 `DeploymentType`  
 Data type: `CCM_AppDeploymentType`  

 Qualifiers: [id("3"), out]  

 Deployment type.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
