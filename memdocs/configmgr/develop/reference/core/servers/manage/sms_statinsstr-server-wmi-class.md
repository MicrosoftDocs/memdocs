---
description: Learn how to use the SMS_StatInsStr Class to represent a high-performance version of SMS_StatMsgInsStrings Server WMI class.
title: SMS_StatInsStr Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a18643d4-b69c-4a2b-8acf-b897968e19be
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_StatInsStr Server WMI Class
The `SMS_StatInsStr` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a high-performance version of [SMS_StatMsgInsStrings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsginsstrings-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StatInsStr : SMS_BaseClass  
{  
      UInt32 InsStrIndex;  
      String InsStrValue;  
      SInt64 RecordID;  
};  
```  

## Methods  
 The `SMS_StatInsStr` class does not define any methods.  

## Properties  
 `InsStrIndex`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The index defining the order of the insertion strings. The index directly relates to the insertion points in the status message.  

 `InsStrValue`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Text to insert into the insertion point.  

 `RecordID`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: none  

 Record ID of the status message to which the insertion point belongs.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class represents insertion strings for Configuration Manager component messages and user-defined messages. The status message is represented by [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md). Your application can use the [RaiseRawStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiserawstatusmsg-method-in-class-sms_statusmessage.md) to add insertion strings. To delete insertion strings, the application deletes the associated status message.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StatMsgInsStrings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsginsstrings-server-wmi-class.md)   
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
