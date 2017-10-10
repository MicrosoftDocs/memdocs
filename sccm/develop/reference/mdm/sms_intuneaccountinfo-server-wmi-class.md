---
title: "SMS_IntuneAccountInfo Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e9582b73-ef71-4cf6-963b-31ecf8dced26searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_IntuneAccountInfo Server WMI Class
The `SMS_IntuneAccountInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Microsoft Intune account information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_IntuneAccountInfo : SMS_BaseClass  
{  
    String AADTenantID;  
    String IntuneAccountID;  
    Datetime LastUpdateTime;  
};  

```  

## Methods  
 The `SMS_IntuneAccountInfo` class does not define any methods.  

## Properties  
 `AADTenantID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The GUID of the Azure Active Directory account.  

 `IntuneAccountID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The GUID of the Microsoft Intune account.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The last date and time that the account was updated.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)   
 [Configuration Manager Hybrid Server WMI Classes](../../../develop/reference/mdm/hybrid-server-wmi-classes.md)
