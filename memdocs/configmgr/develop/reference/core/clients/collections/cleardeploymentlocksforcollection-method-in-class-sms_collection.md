---
title: "ClearDeploymentLocksForCollection Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d7c2626e-b99c-48ab-bde2-429e1763d48f
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# ClearDeploymentLocksForCollection Method in Class SMS_Collection
The `ClearDeploymentLocksForCollection` Windows Management Instrumentation (WMI) class method, in Configuration Manager, clears deployment locks for a selected collection.  For example, if the server group option is selected for a collection, and an administrator sees that the deployments to the collection are stuck, then the administrator can use this method to release the deployment lock from a non-responsive client, allowing the other members of the collection to acquire a deployment lock.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ClearDeploymentLocksForCollection();  

```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)   
