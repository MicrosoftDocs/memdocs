---
title: "SMS_OSDeploymentKitSupportedPlatforms Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c3db4103-1728-4135-8273-db37f5bd5f8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_OSDeploymentKitSupportedPlatforms Server WMI Class
The `SMS_OSDeploymentKitSupportedPlatforms` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that maps Assessment and Deployment Kit (ADK) versions to supported platforms.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_OSDeploymentKitSupportedPlatforms : SMS_SupportedPlatformsOfflineServicing  
{  
    String DeploymentKitVersion;  
    String Name;  
    String OsVersionBuild;  
    String ProductType;  
};  

```  

## Methods  
 The `SMS_OSDeploymentKitSupportedPlatforms` class does not define any methods.  

## Properties  
 `DeploymentKitVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [not_null]  

 The version of the deployment kit with which this property is associated.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 See [SMS_SupportedPlatformsOfflineServicing Server WMI Class](../../../develop/reference/core/servers/configure/sms_supportedplatformsofflineservicing-server-wmi-class.md).  

 `OsVersionBuild`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 See [SMS_SupportedPlatformsOfflineServicing Server WMI Class](../../../develop/reference/core/servers/configure/sms_supportedplatformsofflineservicing-server-wmi-class.md).  

 `ProductType`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 See [SMS_SupportedPlatformsOfflineServicing Server WMI Class](../../../develop/reference/core/servers/configure/sms_supportedplatformsofflineservicing-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
