---
title: "SMS_SIIB_SysResRole Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 15511027-14d3-48a9-b3f7-5a2e2fafd298
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SIIB_SysResRole Server WMI Class
The `SMS_SIIB_SysResRole` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a system role associated with a Configuration Manager console property page resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SIIB_SysResRole : SMS_SiteInstallItemBase   
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
   String RoleName;  
   String SiteCode;  
   String Units[];  
};  
```  

## Methods  
 The `SMS_SIIB_SysResRole` class does not define any methods.  

## Properties  
 `ChmFile`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 This property is deprecated.  

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

 Qualifiers: None  

 This property is deprecated.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Role flags. Currently the only supported flag is ASSIGNABLE (0).  

|Bit|Description|  
|---------|-----------------|  
|0|ASSIGNABLE|  

 `GUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 GUID representing the Microsoft Management Console node for the property page.  

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

 `RoleName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the role.  

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
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)
