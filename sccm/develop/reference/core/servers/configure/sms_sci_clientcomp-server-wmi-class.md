---
title: "SMS_SCI_ClientComp Class"
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
ms.assetid: f3c963c8-a0a0-4ff6-8999-69138f534023searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SCI_ClientComp Server WMI Class
The `SMS_SCI_ClientComp` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the component to install on a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_ClientComp : SMS_SiteControlItem   
{  
     String ClientComponentName;  
     UInt32 FileType;  
     UInt32 Flags;  
     String ItemName;  
     String ItemType;  
     SMS_EmbeddedPropertyList PropLists[];  
     SMS_EmbeddedProperty Props[];  
     SMS_Client_Reg_MultiString_List RegMultiStringLists[];  
     String SiteCode;  
};  
```  

## Methods  
 The `SMS_SCI_ClientComp` class does not define any methods.  

## Properties  
 `ClientComponentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the client component. The default value is "".  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Client component flag identifying whether a component is enabled or not. Possible values are:  

|||  
|-|-|  
|0|Not enabled|  
|1|Enabled|  

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

 `RegMultiStringLists`  
 Data type: `SMS_Client_Reg_MultiString_List` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md) objects for the configuration.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Run the following query for a complete list of client components defined for your site server.  

```  
SELECT * FROM SMS_SCI_ClientComp  
WHERE SiteCode = "<sitecode>"  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md)   
 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
