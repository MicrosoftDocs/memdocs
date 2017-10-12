---
title: "SMS_StatMsgAttributes Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 437e32f3-8fbd-4843-811e-9d53d8dce9d9searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_StatMsgAttributes Server WMI Class
The `SMS_StatMsgAttributes` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents optional data associated with a status message.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StatMsgAttributes : SMS_BaseClass  
{  
      UInt32 AttributeID;  
      DateTime AttributeTime;  
      String AttributeValue;  
      SInt64 RecordID;  
};  
```  

## Methods  
 The `SMS_StatMsgAttributes` class does not define any methods.  

## Properties  
 `AttributeID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers:  

 [key]  

 Type of attribute that is defined by the `AttributeValue` property. Possible values are:  

|||  
|-|-|  
|400|Package ID|  
|401|Advertisement ID|  
|402|Collection ID|  
|403|User Name|  
|404|Distribution Point|  
|405|Policy ID|  
|406|Policy Assignment ID|  
|407|Software Metering Rule ID|  
|408|Client SMS Unique ID|  
|409|Site Code|  
|410|Package Version|  
|411|Time Key|  
|412|Unique Update ID|  
|413|Product ID|  
|414|CI Assignment ID|  
|415|Object ID|  
|416|Object Type|  
|419|UpdateSourceUniqueID|  
|420|Collection Extended Properties ID|  
|421|Wake On LAN Object Type|  
|422|Wake On LAN Batch ID|  
|423|Machine Extended Properties ID|  
|424|Wake On LAN Number of Requests|  
|425|Unknown Machine|  
|426|MAC Address|  
|427|SMBIOS ID|  
|428|Application ID|  
|429|Application Version|  

 `AttributeTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: [key]  

 Date and time, in Universal Coordinated Time (UTC), when the message was generated.  

 `AttributeValue`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Attribute value having content that is determined by the `AttributeID` property.  

 `RecordID`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: None  

 Record ID of the status message with which the attribute is associated.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Use this class to associate specific information with a message. The attribute data is not displayed in the message text. Typically, the attribute values are used to query for status messages that reference a particular object. For example, your application can query for the attribute that retrieves all the messages associated with a particular Configuration Manager package.  

 Each attribute is stored as an instance of this class. Your application can use the raise status message methods to add attribute values. To delete attribute values, the application deletes the associated status message.  

> [!NOTE]
>  Use the [SMS_StatAttr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statattr-server-wmi-class.md) for a high-performance version of this class.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Status Server WMI Classes](../../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)   
 [SMS_StatAttr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statattr-server-wmi-class.md)
