---
title: "SMS_Identification Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1310f54d-03a1-4c14-a017-09625250c6fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Identification Server WMI Class
The `SMS_Identification` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides basic information about the installed [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md) object, for example, its language version, site code, and provider. This class should return only one instance.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Identification : SMS_BaseClass   
{  
     UInt32 License;  
     UInt32 LocaleID;  
     UInt32 MonthlyReleaseVersion;  
     UInt32 Reserved;  
     String ServiceAccountName;  
     String SMSAvailableConsoleVersion;  
     UInt32 SMSBuildNumber;  
     UInt32 SMSMinBuildNumber;  
     String SMSProviderServer;  
     String SMSSiteServer;  
     String SMSVersion;  
     String ThisSiteCode;  
     String ThisSiteName;  
     String UIManifestHash;  
     String UIManifestHashAlgorithm;  
     String UIUpdateManifestHash;  
     String UIUpdateManifestHashAlgorithm;  
};  
```  

## Methods  
 The following table lists the methods in `SMS_Identification`.  

|Method|Description|  
|------------|-----------------|  
|[GetCurrentUser Method in Class SMS_Identification](../../../../../develop/reference/core/servers/configure/getcurrentuser-method-in-class-sms_identification.md)|Gets the domain\user name being used by the SMS Provider for authentication.|  
|[GetFileBinary Method in Class SMS_Identification](../../../../../develop/reference/core/servers/configure/getfilebinary-method-in-class-sms_identification.md)|Gets the binary user interface for a feature.|  
|[GetProviderVersion Method in Class SMS_Identification](../../../../../develop/reference/core/servers/configure/getproviderversion-method-in-class-sms_identification.md)|Gets the product version string from the version resources of the SMS Provider DLL.|  
|[GetSiteID Method in Class SMS_Identification](../../../../../develop/reference/core/servers/configure/getsiteid-method-in-class-sms_identification.md)|Gets the unique ID of the installed Configuration Manager site.|  

## Properties  
 `License`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 License type of the installation. Possible values are:  

|||  
|-|-|  
|0|Evaluation|  
|1|Non-evaluation|  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Subtype("Locale Id")]  

 ID of the locale used by the Configuration Manager installation, for example, English (1033) or German (1031).  

 `MonthlyReleaseVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Monthly Configuration Manager release version.  

 `Reserved`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 For internal use only.  

 `ServiceAccountName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the Configuration Manager service account, which is a special user account having administrative privileges that uses Configuration Manager to perform certain activities. The value includes the domain.  

 `SMSAvailableConsoleVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Available Configuration Manager console version.  

 `SMSBuildNumber`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Build version number of the installed Configuration Manager software.  

 `SMSMinBuildNumber`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 This property is deprecated.  

 `SMSProviderServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the server on which the SMS Provider is installed.  

> [!NOTE]
>  If a site has multiple SMS Providers installed, this will just return one of them.  

 `SMSSiteServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the server on which the Configuration Manager site server components are installed.  

 `SMSVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Major version number of the Configuration Manager installation, for example, 2.0. For the complete version number, see the `Version` property of [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md).  

 `ThisSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Site code for the installation.  

 `ThisSiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Friendly name of the site.  

 `UIManifestHash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Hash of the UIManifest.xml file stored on the site server.  

 `UIManifestHashAlgorithm`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Hash algorithm used to calculate the hash of the UIManifest.xml file stored on the site server.  

 `UIUpdateManifestHash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Hash of the UIUpdatemanifest.xml file stored on the site server.  

 `UIUpdateManifestHashAlgorithm`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Hash algorithm used to calculate the hash of the UIUpdatemanifest.xml file stored on the site server.  

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
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
