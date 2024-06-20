---
description: The SMS_SIIB_Configuration WMI class is an SMS Provider server class, in Configuration Manager, that represents the configuration in the Configuration Manager console.
title: SMS_SIIB_Configuration Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6ed67b68-4b47-4043-8c19-499d20ab304a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SIIB_Configuration Server WMI Class
The `SMS_SIIB_Configuration` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the configuration for a property page in the Configuration Manager console.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_Configuration : SMS_SiteInstallItemBase   
{  
   String ChmFile;  
   String ConfigUnitName;  
   String ConfigurationName;  
   UInt32  DescriptionID;  
   UInt32  DispIconID;  
   UInt32  DispNameID;  
   UInt32  Flags;  
   String GUID;  
   String HtmFile;  
   String ItemName;  
   String ItemType;  
   String ResDLL;  
   String SiteCode;  
   String Type;  
   String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_Configuration` class does not define any methods.  

## Properties  
 `ChmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `ConfigUnitName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the configuration unit to find in the site control file.

 `ConfigurationName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the configuration.  

 `DescriptionID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `DispIconID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `DispNameID`  
 Data type: `UInt32`  

 Access type: Read-only  

 This property is deprecated.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Flags defining the site to which the configuration applies. Possible values are listed below. The default value is 3.  

 0  
 SECONDARY  

 1  
 PRIMARY  

 `GUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `HtmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ResDLL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `Type`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 The configuration type. Possible values are:  

- COMPONENT_CONFIGURATION(Component Configuration)  

- DISCOVERY_METHOD(Discovery Method)  

- CLIENT_SETUP_METHOD(Client Setup Method)  

- INVENTORY_METHOD(Inventory Method)  

- CLIENT_AGENT(Client Agent)  

- CLIENT_ACCOUNT_CONFIGURATION(Client Account Configuration)  

- SERVER_ACCOUNT_CONFIGURATION(Server Account Configuration)  

  `Units`  
  Data type: `String` Array  

  Access type: Read-only  

  Qualifiers: None  

  See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
