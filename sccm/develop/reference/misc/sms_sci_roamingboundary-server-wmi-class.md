---
title: "SMS_SCI_RoamingBoundary Class"
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
ms.assetid: 7a0619a5-338f-41e9-b3c6-383797533a83searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SCI_RoamingBoundary Server WMI Class
The `SMS_SCI_RoamingBoundary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes the Configuration Manager site boundary information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_RoamingBoundary : SMS_SiteControlItem  
{  
      String Details[];  
      String DisplayNames[];  
      UInt32 Filetype;  
      UInt32 Flags[];  
      Boolean IncludeSiteBoundary;  
      String ItemName;  
      String Itemtype;  
      String SiteCode;  
      String Types[];  
};  
```  

## Methods  
 The `SMS_SCI_RoamingBoundary` class does not define any methods.  

## Properties  
 `Details`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of details specifying the actual value for the roaming boundary.  

 `DisplayNames`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of display names for each boundary.  

 `Filetype`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 Type of site control file. See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Flags`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of flags specifying whether the roaming boundary is a fast or slow boundary.  

 `IncludeSiteBoundary`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Deprecated.  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Itemtype`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Name of the site control item. See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 For this class, the item type should always be "Roaming Boundary".  

 `SiteCode`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `Types`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Type of the roaming boundary. Possible values are:  

||  
|-|  
|IP Subnets|  
|AD Site Name|  
|IP Ranges|  
|IPv6 Prefixes|  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Your application should specify the `Details`, `DisplayNames`, `Flags`, and `Types` properties as parallel arrays.  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
