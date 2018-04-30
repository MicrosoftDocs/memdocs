---
title: "ReassignClientsToSite Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 234e8b75-9c12-4e60-96ec-c816b9f1e3d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ReassignClientsToSite Method in Class SMS_Collection
The `ReassignClientsToSite` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, reassigns the Configuration Manager site for clients in the list.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ReassignClientsToSite(  
     UInt32 ResourceIDs[],  
     Boolean NewSiteCode  
     SInt32 ReturnValue  
);  
```  

#### Parameters  
 `ResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of member resources.  

 `NewSiteCode`  
 Data type: `String`  

 Qualifiers: [in]  

 The new site code for the clients.  

 `ReturnValue`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 The number of devices that were successfully reassigned.  

> [!IMPORTANT]
>  Even if there is an error, some devices may still get reassigned.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
