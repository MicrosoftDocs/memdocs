---
title: "SMS_SIIB_UINALProvider Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f6e605b3-2359-426c-80fa-6926565638bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SIIB_UINALProvider Server WMI Class
The `SMS_SIIB_UINALProvider` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the network abstraction layer (NAL) provider used by the Configuration Manager console.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_UINALProvider : SMS_SiteInstallItemBase   
{  
   UInt32 DispIconID;  
   UInt32 DispNameID;  
   String DLLName;  
   String GUID;  
   String ItemName;  
   String ItemType;  
   String ProviderName;  
   SMS_UINAL_ResourceInfo ResourceInfo[];  
   String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_UINALProvider` class does not define any methods.  

## Properties  
 `DispIconID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource ID of the display icon.  

 `DispNameID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource ID of the display name.  

 `DLLName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the resource DLL containing the resource strings for `DispIconID` and `DispNameID`.  

 `GUID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 GUID representing the Microsoft Management Console node for the property page.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

 `ProviderName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the provider.  

 `ResourceInfo`  
 Data type: `SMS_UINAL_ResourceInfo` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_UINAL_ResourceInfo Server WMI Class](../../../develop/reference/misc/sms_uinal_resourceinfo-server-wmi-class.md) objects for property pages that reference the NAL provider.  

 `Units`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)   
 [SMS_UINAL_ResourceInfo Server WMI Class](../../../develop/reference/misc/sms_uinal_resourceinfo-server-wmi-class.md)
