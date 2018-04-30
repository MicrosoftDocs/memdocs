---
title: "SMS_OSDeploymentConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ee7798f1-3288-448f-b356-95518c58b9d8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_OSDeploymentConfig Server WMI Class
The `SMS_OSDeploymentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all OSD-related constants and settings with their ADK-specific values.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_OSDeploymentConfig : SMS_BaseClass  
{  
    String DeploymentKitVersion;  
    String DeploymentPropertyName;  
    String DeploymentPropertyValue;  
};  

```  

## Methods  
 The `SMS_OSDeploymentConfig` class does not define any methods.  

## Properties  
 `DeploymentKitVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 The version of the deployment kit with which this property is associated.  

 `DeploymentPropertyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 The name of the property.  

 `DeploymentPropertyValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The value of the property.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
