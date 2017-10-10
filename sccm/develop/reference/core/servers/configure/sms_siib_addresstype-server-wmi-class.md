---
title: "SMS_SIIB_AddressType Class"
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
ms.assetid: 28c99fd5-9d17-4887-be4d-e9ab230d2728searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SIIB_AddressType Server WMI Class
The `SMS_SIIB_AddressType` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the Configuration Manager sender address type used by the Configuration Manager console.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_AddressType : SMS_SiteInstallItemBase   
{  
     String AddressType;  
     String ChmFile;  
     UInt32 DescriptionID;  
     UInt32 DispIconID;  
     UInt32 DispNameID;  
     UInt32 Flags;  
     String GUID;  
     String HtmFile;  
     String ItemName;  
     String ItemType;  
     String ResDLL;  
     String SiteCode;  
     String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_AddressType` class does not define any methods.  

## Properties  
 `AddressType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Address type. See the `AddressType` property of [SMS_SCI_Address Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_address-server-wmi-class.md).  

 `ChmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Compressed .chm file containing the .htm file for the address type. See `HtmFile`.  

 `DescriptionID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the description text for the sender.  

 `DispIconID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the display icon for the sender.  

 `DispNameID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the display name for the sender.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Flags indicating permission status to change Configuration Manager sender address types. Possible values are:  

 0  
 ALLOW_ADD  

 1  
 ALLOW_DELETE  

 2  
 ALLOW_MODIFY  

 3  
 ALLOW_SCHEDULE  

 4  
 ALLOW_RATE_LIMITING  

 `GUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 GUID representing the Microsoft Management Console node for the property page.  

 `HtmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Help file (.htm) for the address type.  

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

 Name of the resource DLL containing the resource Strings for `DescriptionID`,`DispIconID`, and `DispNameID`.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `Units`  
 Data type: `String`Array  

 Access type: Read-only  

 Qualifiers: None  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
