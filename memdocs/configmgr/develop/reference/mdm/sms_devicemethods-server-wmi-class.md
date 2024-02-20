---
title: SMS_DeviceMethods Class
titleSuffix: Configuration Manager
description: The SMS_DeviceMethods WMI class is an SMS Provider server class that provides access to actions that you can take on mobile devices and Microsoft Exchange ActiveSync devices.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a775bb4c-6f9f-4918-bd96-892ca9e05467
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DeviceMethods Server WMI Class
The `SMS_DeviceMethods` Windows Management Instrumentation (WMI) class is an SMS Provider server class that  provides access to actions that you can take on mobile devices and Microsoft Exchange ActiveSync devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceMethods : SMS_Baseclass ();  
```  

## Methods  
 The following table shows the methods in `SMS_DeviceMethods`.  

|Method|Description|  
|------------|-----------------|  
|[AllowAccess Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/allowaccess-method-in-class-sms_devicemethods.md)|Lets the Exchange ActiveSync device connect to Exchange.|  
|[BlockAccess Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/blockaccess-method-in-class-sms_devicemethods.md)|Blocks the Exchange ActiveSync device from accessing to Exchange.|  
|[NEW SP1: CancelRetire Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/cancelretire-method-in-class-sms_devicemethods.md)|Cancels the retirement of this device from Configuration Manager.|  
|[CancelWipe Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/cancelwipe-method-in-class-sms_devicemethods.md)|Cancels a pending wipe request on mobile devices or Exchange ActiveSync devices.|  
|[NEW SP1: RequestRetire Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/requestretire-method-in-class-sms_devicemethods.md)|Retires this device from Configuration Manager.|  
|[RequestWipe Method in Class SMS_DeviceMethods](../../../develop/reference/mdm/requestwipe-method-in-class-sms_devicemethods.md)|Removes Microsoft Exchange and Configuration Manager software from the mobile device or Exchange ActiveSync device.|  

## Properties  
 The `SMS_DeviceMethods` class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Mobile device setting packages use programs, distribution points, and advertisements to collections to distribute their content.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)   
 [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)
