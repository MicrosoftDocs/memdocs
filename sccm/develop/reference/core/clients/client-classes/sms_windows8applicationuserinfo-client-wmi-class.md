---
title: "SMS_Windows8ApplicationUserInfo Class"
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
ms.assetid: 64bad706-813b-4f94-9c59-a7bf6dcda27asearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Windows8ApplicationUserInfo Client WMI Class
In Configuration Manager, the `SMS_Windows8ApplicationUserInfo` class is a client Windows Management Instrumentation (WMI) class that defines user information of an application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Windows8ApplicationUserInfo  
{  
      String FullName;  
      String InstallState;  
      String UserAccountName;  
      String UserSecurityId;  
};  
```  

## Methods  
 The `SMS_Windows8ApplicationUserInfo` class does not define any methods.  

## Properties  
 `FullName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Full name of the user.  

 `InstallState`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Installation state of the package. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|NotInstalled|The package has not been installed.|  
|Staged|The package has been downloaded.|  
|Installed|The package is ready for use.|  

 `UserAccountName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User account name.  

 `UserSecurityId`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 User security identifier.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)
