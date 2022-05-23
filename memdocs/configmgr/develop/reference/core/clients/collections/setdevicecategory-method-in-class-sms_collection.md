---
title: "SetDeviceCategory Method"
titleSuffix: "Configuration Manager"
description: "A Windows Management Instrumentation (WMI) class method, in Configuration Manager, assigns a category to a set of devices."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f1cf818c-711f-47d4-9cae-5e4f7aabc3c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetDeviceCategory Method in Class SMS_Collection
The `SetDeviceCategory` Windows Management Instrumentation (WMI) class method, in Configuration Manager, assigns a category to a set of devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SetDeviceCategory (  
    String CategoryID,   
    UInt32 ResourceIDs[]  
);  

```  

#### Parameters  
 `CategoryID`  
 Data type: `String`  

 Qualifiers: [in]  

 A device category ID. This value is a GUID in string format.  

 `ResourceIDs`  
 Data type: `UInt32 Array`  

 Qualifiers: [in]  

 An array of resource IDs. The items in the array represent the devices to which the category is to be assigned.  

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
