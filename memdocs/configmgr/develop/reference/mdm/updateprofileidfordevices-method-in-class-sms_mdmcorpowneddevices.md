---
title: "UpdateProfileIDForDevices Method"
titleSuffix: "Configuration Manager"
description: "update the  profile IDs for device serial numbers." 
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1843e467-9330-437c-b3d8-fe84a45284a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# UpdateProfileIDForDevices Method in Class SMS_MDMCorpOwnedDevices
The `UpdateProfileIdForDevices` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the  profile IDs for device serial numbers.  

## Syntax  

```  
sint32 UpdateProfileIdForDevices(  
     String RequestEnrollmentProfileId,  
     String DeviceSerialNumbers  
);  

```  

#### Parameters  
 `RequestEnrollmentProfileId`  
 Data type: `String`  

 Qualifiers: [in]  

 Enrollment profile ID.  

 `DeviceSerialNumbers`  
 Data type: `String Array`  

 Qualifiers: [in]  

 The serial number of the device.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MDMCorpOwnedDevices Server WMI Class](../../../develop/reference/mdm/sms_mdmcorpowneddevices-server-wmi-class.md)   
