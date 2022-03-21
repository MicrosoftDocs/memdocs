---
title: "SMS_SIIB_SenderType Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1a2b53a2-4fa1-4671-baba-0e6fbfc63eb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SIIB_SenderType Server WMI Class
The `SMS_SIIB_SenderType` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the sender type for the associated Configuration Manager console property pages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_SenderType : SMS_SiteInstallItemBase   
{  
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
   String SenderType;  
   String SiteCode;  
   String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_SenderType` class does not define any methods.  

## Properties  
 `ChmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Compressed .chm file containing the .htm file for the sender type.  

 `DescriptionID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the description.  

 `DispIconID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the display icon.  

 `DispNameID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Resource ID of the display name.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Flags defining operations supported by the sender. Possible values are:  

 0  
 ALLOW_ADD  

 1  
 ALLOW_DELETE  

 2  
 ALLOW_MODIFY  

 `GUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 GUID representing the Microsoft Management Console node for the property page.  

 `HtmFile`  
 Data type: `String`  

 Access type: Read-only  

 Help file (.htm) for the sender type.  

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

 Name of the resource DLL containing the resource strings for `DescriptionID`, `DispIconID`, and `DispNameID`.  

 `SenderType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Sender service name.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

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
 [Configuration Manager Hierarchy Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
