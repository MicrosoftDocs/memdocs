---
title: "SMS_AdvertisementStatusInformation Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7bc41725-e274-4ce8-986f-1f55376a38c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AdvertisementStatusInformation Server WMI Class
The `SMS_AdvertisementStatusInformation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the state and description for a software distribution or software update status message.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdvertisementStatusInformation : SMS_BaseClass  
{  
      UInt32 MessageID;  
      String MessageName;  
      UInt32 MessageState;  
      String MessageStateName;  
};  
```  

## Methods  
 The `SMS_AdvertisementStatusInformation` class does not define any methods.  

## Properties  
 `MessageID`  
 Data type: `UInt32`  

 Access type: Read/write  

 Qualifiers: [key]  

 Software distribution or software update message ID.  

 `MessageName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Short description of the status message.  

 `MessageState`  
 Data type: `UInt32`  

 Access type: Read/write  

 Qualifiers: None  

 Numeric category (software update states >= 100, software distribution < 100). For more information, see the Remarks section later in this topic.  

 `MessageStateName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Short description of the message state.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The `MessageState` property can have one of the following values:  

|MessageState|Type|MessageStateName|  
|------------------|----------|----------------------|  
|-1|Delivery|Accepted - No further status|  
|0|Acceptance/Delivery|No Status|  
|1|Acceptance|Accepted|  
|2|Acceptance|Rejected|  
|3|Acceptance|Expired|  
|4|Delivery|Will Not Rerun|  
|5|Delivery|Download in Progress|  
|6|Delivery|Download Complete|  
|7|Delivery|Canceled|  
|8|Delivery|Waiting|  
|9|Delivery|Running|  
|10|Delivery|Retrying|  
|11|Delivery|Failed|  
|12|Delivery|Reboot Pending|  
|13|Delivery|Succeeded|  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)
