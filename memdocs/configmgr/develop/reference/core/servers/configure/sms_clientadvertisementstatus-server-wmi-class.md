---
description: The SMS_ClientAdvertisementStatus WMI class is an SMS Provider server class, in Configuration Manager, that records the last status message for every client and advertisement.
title: SMS_ClientAdvertisementStatus Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7cf70230-481e-4ab5-9f5b-30975b58b761
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientAdvertisementStatus Server WMI Class
The `SMS_ClientAdvertisementStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that records the last status message for every client and advertisement.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientAdvertisementStatus : SMS_BaseClass  
{  
      String AdvertisementID;  
      UInt32 LastAcceptanceMessageID;  
      String LastAcceptanceMessageIDName;  
      UInt32 LastAcceptanceMessageIDSeverity;  
      UInt32 LastAcceptanceState;  
      String LastAcceptanceStateName;  
      DateTime LastAcceptanceStatusTime;  
      String LastExecutionContext;  
      String LastExecutionResult;  
      UInt32 LastState;  
      String LastStateName;  
      UInt32 LastStatusMessageID;  
      String LastStatusMessageIDName;  
      UInt32 LastStatusMessageIDSeverity;  
      DateTime LastStatusTime;  
      UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_ClientAdvertisementStatus` class does not define any methods.  

## Properties  
 `AdvertisementID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers:  [key]  

 ID of the advertisement.  

 `LastAcceptanceMessageID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Last acceptance status message ID.  

 `LastAcceptanceMessageIDName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Short description of the last acceptance status message.  

 `LastAcceptanceMessageIDSeverity`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [enumeration]  

 The severity of the last acceptance status message. Possible values are:  

|Value|Status message severity|  
|-|-|  
|0x40000000|Error(3221225472)|  
|0x80000000|Warning(2147483648)|  
|0xC0000000|Informational(1073741824)|  

 `LastAcceptanceState`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Numeric category of the last acceptance status message.  

 `LastAcceptanceStateName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Short description of the acceptance category.  

 `LastAcceptanceStatusTime`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC), when the last acceptance message was generated.  

 `LastExecutionContext`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 User context (account) under which the program ran.  

 `LastExecutionResult`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Last string returned by a status Management Information Format (MIF) file (messages 10007 and 10009) or an error return code (10006).  

 `LastState`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Numeric category of the last delivery status message.  

 `LastStateName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Short description of the delivery category.  

 `LastStatusMessageID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Last delivery status message ID.  

 `LastStatusMessageIDName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Short description of the last delivery status message.  

 `LastStatusMessageIDSeverity`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 [enumeration]  

 The severity of the last delivery status message. Possible values are listed for `LastAcceptanceMessageIDSeverity`.   

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC), when the last delivery message was generated.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [key]  

 ID of the resource for the client.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Using this class is the primary way to determine advertisement status. Even if a client is no longer in the collection targeted by an advertisement, an instance still appears in this class. It records the last status message for every advertisement for each client.  

  Advertisement status is divided into two stages, Acceptance and Delivery, which are recorded separately. Acceptance is whether the client has received the advertisement and whether the client decides that the advertisement applies to it. Delivery is the status of everything that comes after; that is, the actual download and execution of the advertisement. Advertisement status messages have been categorized into several groups that indicate similar status for the advertisement.  

  For more information about categories see [SMS_AdvertisementStatusInformation Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisementstatusinformation-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AdvertisementStatusInformation Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisementstatusinformation-server-wmi-class.md)
