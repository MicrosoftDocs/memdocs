---
title: "SMS_PendingReRegistrationOnSiteReAssignment Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c3387ae1-f546-4e05-b30e-b47ed252c15f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_PendingReRegistrationOnSiteReAssignment Client WMI Class
> [!IMPORTANT]
>  This class supports the Configuration Manager 2007 infrastructure and is not intended to be used directly from your code.  

 The `SMS_PendingReRegistrationOnSiteReAssignment` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents a pending re-registration at the time of site reassignment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PendingReRegistrationOnSiteReAssignment  
{  
      UInt32 Flags;  
      String LastAssignedSite;  
      String NewAssignedSite;  
};  
```  

## Methods  
 The `SMS_PendingReRegistrationOnSiteReAssignment` class does not define any methods.  

## Properties  
 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags defining options for the pending re-registration.  

 `LastAssignedSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code of the last site that was assigned.  

 `NewAssignedSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code of the new site being assigned.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
