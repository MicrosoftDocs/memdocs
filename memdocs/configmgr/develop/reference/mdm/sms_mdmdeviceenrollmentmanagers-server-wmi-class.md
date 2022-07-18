---
title: "SMS_MDMDeviceEnrollmentManagers Class"
titleSuffix: "Configuration Manager"
description: "The SMS_MDMDeviceEnrollmentManagers WMI class represents On-premises Mobile Device Management (MDM) device enrollment managers."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9b1f9352-f6bb-4a57-ae32-8d2c70045c34
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_MDMDeviceEnrollmentManagers Server WMI Class
The `SMS_MDMDeviceEnrollmentManagers` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents On-premises Mobile Device Management (MDM) device enrollment managers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMDeviceEnrollmentManagers : SMS_BaseClass  
{  
    UInt32 ResourceID;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_MDMDeviceEnrollmentManagers` class.  

|Method|Description|  
|------------|-----------------|  
|[InsertMultipleResourceIds Method in Class SMS_MDMDeviceEnrollmentManagers](../../../develop/reference/mdm/insertmultipleresourceids-method-in-class-sms_mdmdeviceenrollmentmanagers.md)|Inserts multiple resource IDs.|  
|[RemoveMultipleResourceIds Method in Class SMS_MDMDeviceEnrollmentManagers](../../../develop/reference/mdm/removemultipleresourceids-method-in-class-sms_mdmdeviceenrollmentmanagers.md)|Deletes multiple resource IDs.|  

## Properties  
 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Resource ID.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
