---
title: "SMS_SCI_SiteDefinition Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: eee21135-4800-4002-90ed-f125270369e6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SCI_SiteDefinition Server WMI Class
The `SMS_SCI_SiteDefinition` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains general definitions for the site (for example, name) and for accounts (for example, SQL) used by Configuration Manager server components.  

> [!NOTE]
>  This class is vital to the operation of the site control infrastructure. Changing the values for an existing site might render the site control file unusable for further configuration. Existing objects for functioning sites should not be changed.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_SiteDefinition : SMS_SiteControlItem   
{  
     String AddressPublicKey;  
     UInt32 FileType;  
     String InstallDirectory;  
     String ItemName;  
     String ItemType;  
     String ParentSiteCode;  
     SMS_EmbeddedPropertyList PropLists[];  
     SMS_EmbeddedProperty Props[];  
     String ServiceAccount;  
     String ServiceAccountDomain;  
     String ServiceAccountPassword;  
     String ServiceExchangeKey;  
     String ServicePlaintextAccount;  
     String ServicePublicKey;  
     String SiteCode;  
     String SiteName;  
     String SiteServerDomain;  
     String SiteServerName;  
   String SiteServerPlatform;  
     UInt32 SiteType;  
     String SQLAccount;  
     String SQLAccountPassword;  
     String SQLDatabaseName;  
     String SQLPublicKey;  
     String SQLServerName;  
};  
```  

## Methods  
 The `SMS_SCI_SiteDefinition` class does not define any methods.  

## Properties  
 `AddressPublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `InstallDirectory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Directory on the site server where the Configuration Manager tree starts. The default value is "".  

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

 `ParentSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 Three-letter site code of the parent site (if there is one). The default value is "".  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the site.  

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the site.  

 `ServiceAccount`  
 Data type: String  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `ServiceAccountDomain`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `ServiceAccountPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `ServiceExchangeKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Public exchange key used to encrypt the value of `ServicePublicKey`. Provide no value for this property if `ServicePublicKey` is not encrypted.  

 `ServicePlaintextAccount`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `ServicePublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `SiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Unique friendly site name of the site server. The default value is "".  

 `SiteServerDomain`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Domain in which the site server participates. The default value is "".  

 `SiteServerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the Windows NT site server. The default value is "".  

 `SiteServerPlatform`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [StringEnumeration]  

 Processor platform of the site server. Possible values are:  

-   AMD64  

 `SiteType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [ResIDValueLookup("SiteType")]  

 Type of site. Possible values are listed for the `Type` property of [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md).  

 For this class, the default value is PRIMARY (2).  

|||  
|-|-|  
|1|Secondary|  
|2|Primary|  
|4|CAS|  

 `SQLAccount`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `SQLAccountPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `SQLDatabaseName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the SQL Server database on the server. The default value is "".  

 `SQLPublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `SQLServerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the computer running SQL Server for this installation. The default value is "".  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)   
 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)
