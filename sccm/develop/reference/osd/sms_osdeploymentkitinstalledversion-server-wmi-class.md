---
title: "SMS_OSDeploymentKitInstalledVersion Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 634cb192-7fcd-4e8d-8730-3c1ed832bb61
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_OSDeploymentKitInstalledVersion Server WMI Class
The `SMS_OSDeploymentKitInstalledVersion` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a mapping of server names to an  installed Assessment and Deployment Kit (ADK) version.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_OSDeploymentKitInstalledVersion : SMS_BaseClass  
{  
    String DeploymentKitVersion;  
    String FQDN;  
    UInt32 MachineID;  
    String NetBiosName;  
};  

```  

## Methods  
 The `SMS_OSDeploymentKitInstalledVersion` class does not define any methods.  

## Properties  
 `DeploymentKitVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The version of the deployment kit installed on the computer.  

 `FQDN`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The fully qualified domain name of the computer.  

 `MachineID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 A unique identifier for the computer.  

 `NetBiosName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The NetBIOS name of the computer.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
