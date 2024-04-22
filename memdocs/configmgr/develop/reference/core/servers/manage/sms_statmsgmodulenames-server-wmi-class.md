---
description: Learn how to map module names to the message DLL containing the status message text using SMS_StatMsgModuleNames.
title: SMS_StatMsgModuleNames Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e75bcc02-6061-4461-8fd2-f28a2c661adf
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_StatMsgModuleNames Server WMI Class
The `SMS_StatMsgModuleNames` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that maps module names to the message DLL that contains the status message text.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StatMsgModuleNames : SMS_BaseClass  
{  
    String ModuleName;  
    String MsgDLLName;  
};  
```  

## Methods  
 The `SMS_StatMsgModuleNames` class does not define any methods.  

## Properties  
 `ModuleName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Module name as used in the `ModuleName` property of [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).  

 `MsgDLLName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Name of the corresponding resource DLL that contains the text of the message.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
