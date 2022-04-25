---
description: Learn how to use the SMS_SCI_Address class to represent a sender address, which is a link between the site for which the site control file exists and another site.  
title: "SMS_SCI_Address Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 757473b7-b517-4a03-b812-1dce4834cf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SCI_Address Server WMI Class
The `SMS_SCI_Address` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a sender address, which is a link between the site for which the site control file exists and another site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_Address : SMS_SiteControlItem   
{  
     UInt32 AddressPriorityOrder;  
     String AddressType;  
     String DesSiteCode;  
     String DesSiteName;  
     UInt32 DestinationType;  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     SMS_EmbeddedPropertyList PropLists[];  
     SMS_EmbeddedProperty Props[];  
     UInt32 RateLimitingSchedule[24];  
     String SiteCode;  
     String SiteName;  
     Boolean UnlimitedRateForAll;  
     SMS_SiteControlDaySchedule UsageSchedule[7];  
};  
```  

## Methods  
 The `SMS_SCI_Address` class does not define any methods.  

## Properties  
 `AddressPriorityOrder`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [none]  

 This property is deprecated.  

 `AddressType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [stringnumeration]  

 This property is deprecated.  

 `DesSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 Destination site code with which the sender communicates. The default value is "".  

- If `DestinationType` is 0, this value is the destination site code.  

- If `DestinationType` is 1, this value is the FQDN of the destination distribution point.  

  `DesSiteName`  
  Data type: `String`  

  Access type: Read-only  

  Qualifiers: [read]  

  Destination site name with which the sender communicates.  

  `DestinationType`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: [none]  

  Destination site type. Possible values are:  

|Value|Destination site type|  
|-|-|  
|0|Site server|  
|1|Distribution point|  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the configuration.  

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the configuration.  

 `RateLimitingSchedule`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Array of 24 integers, one for each hour of the day. The values for this 24-hour rate table range from 1 percent to 100 percent. If the `UnlimitedRateForAll` property is `true`, this property contains 100 percent for all 24 elements.  

 Use the rate-limiting schedule to prevent Configuration Manager from using all available bandwidth on the connection.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `SiteName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `UnlimitedRateForAll`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if unlimited rate is enabled for all senders. If this property is set to `false`, specify a rate schedule for the `RateLimitingSchedule` property. Otherwise, 100 percent is used.  

 `UsageSchedule`  
 Data type: `SMS_SiteControlDaySchedule` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Usage schedule array of seven [SMS_SiteControlDaySchedule Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontroldayschedule-server-wmi-class.md) objects, each representing one weekday, for example, 0 for Sunday, 1 for Monday. The schedule is used to control network load during critical time periods by restricting when data can be sent to the address.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is used for inter-site communication by Configuration Manager sender components. For more information, see [Configuration Manager Special Queries](../../../../../develop/core/understand/special-queries.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)   
 [SMS_SiteControlDaySchedule Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontroldayschedule-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
