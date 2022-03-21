---
title: "GetAdvertisements Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 269422ee-e896-49ca-9cdc-c648055d1395
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetAdvertisements Method in Class SMS_Advertisement
The `GetAdvertisements` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the advertisement id for a computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetAdvertisements(  
     uint32  ResourceID,  
     string  AdvertisementIDs[]  
);  
```  

#### Parameters  
 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Unique Configuration Manager-supplied ID for the resource.  

 `AdvertisementIDs`  
 Data type: `String` Array  

 Qualifiers: `[out]`  

 An array of unique auto-generated keys that Configuration Manager assigns to advertisements.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
