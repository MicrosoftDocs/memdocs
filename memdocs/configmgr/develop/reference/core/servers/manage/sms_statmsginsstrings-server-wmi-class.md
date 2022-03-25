---
description: Article detailing the use of SMS_StatMsgInsStrings in Configuration Manager to represent insertion strings that are inserted into the status message.
title: "SMS_StatMsgInsStrings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 731d9874-708d-4440-b312-7093d29f1c5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_StatMsgInsStrings Server WMI Class
The `SMS_StatMsgInsStrings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents insertion strings that are inserted into the status message.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StatMsgInsStrings : SMS_BaseClass  
{  
    UInt32 InsStrIndex;  
     String InsStrValue;  
     SInt64 RecordID;  
};  
```  

## Methods  
 The `SMS_StatMsgInsStrings` class does not define any methods.  

## Properties  
 `InsStrIndex`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [Description(""), key]  

 The index defining the order of the insertion strings. The index directly relates to the insertion points in the status message.  

 `InsStrValue`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Text to insert into the insertion point.  

 `RecordID`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: [key]  

 Record ID of the status message to which the insertion point belongs.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class represents insertion strings for Configuration Manager component messages and user-defined messages. The status message is represented by [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md). Your application can use the [RaiseRawStatusMsg Method in Class SMS_StatusMessage](../../../../../develop/reference/core/servers/manage/raiserawstatusmsg-method-in-class-sms_statusmessage.md) to add insertion strings. To delete insertion strings, the application deletes the associated status message.  

> [!NOTE]
>  Use the [SMS_StatInsStr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statinsstr-server-wmi-class.md) for a high-performance version of this class.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)   
 [SMS_StatInsStr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statinsstr-server-wmi-class.md)
