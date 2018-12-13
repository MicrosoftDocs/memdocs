---
title: "SMS_Site Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a8824024-5e6c-49f9-a54e-9b5ec597b86d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Site Server WMI Class
The `SMS_Site` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents identification and status data for a Configuration Manager site installation.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Site : SMS_BaseClass   
{   
      UInt32 BuildNumber;   
      String Features;   
      String InstallDir;   
      UInt32 Mode;   
      String ReportingSiteCode;   
      UInt32 RequestedStatus;   
      UInt32 SecondarySiteCMUpdateStatus;  
      String ServerName;   
      String SiteCode;   
      String SiteName;   
      UInt32 Status;   
      String TimeZoneInfo;   
      UInt32 Type;   
      String Version;   
};  
```  

## Methods  
 The following table shows the methods in the `SMS_Site` class.  

|Method|Description|  
|------------|-----------------|  
|[EncryptDataEx Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/encryptdataex-method-in-class-sms_site.md)|Encrypts data using the specified site server’s public key and returns the encrypted data.|  
|[GetAutoUpgradeConfigs Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getautoupgradeconfigs-method-in-class-sms_site.md)|Gets configurations for auto-upgrade settings.|  
|[GetClientInfo Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getclientinfo-method-in-class-sms_site.md)|Gets information about a client.|  
|[GetClientPilotingConfigs Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getclientpilotingconfigs-method-in-class-sms_site.md)|Gets the configurations for client piloting settings.|  
|[GetFeatureState Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getfeaturestate-method-in-class-sms_site.md)|Gets the enabled/disabled state of a feature.|  
|[GetSiteADInfo Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/getsiteadinfo-method-in-class-sms_site.md)|Gets Active Directory information of site server.|  
|[ImportGlobalUserAccount Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/importglobaluseraccount-method-in-class-sms_site.md)|Encrypts data that is shared in the hierarchy.|  
|[ImportGlobalUserAccountEx Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/importglobaluseraccountex-method-in-class-sms_site.md)|Encrypts data that is shared in the hierarchy.|  
|[ImportMachineEntry Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md)|Imports computer information.|  
|[IsUsedCert Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/isusedcert-method-in-class-sms_site.md)|Determines whether the specified certificate is used.|  
|[RedistributeAutoUpgradeClientContent Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/redistributeautoupgradeclientcontent-method-in-class-sms_site.md)|Redistributes auto-upgrade client content to the specified distribution point.|  
|[SubmitAMTCert Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/submitamtcert-method-in-class-sms_site.md)|Submits a certificate for a computer that implements Intel Active Management Technology (Intel AMT).|  
|[SubmitRegistrationRecord Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/submitregistrationrecord-method-in-class-sms_site.md)|Submits a registration record.|  
|[UpdateAutoUpgradeClientContent Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/updateautoupgradeclientcontent-method-in-class-sms_site.md)|Updates auto-upgrade client content to all distribution points.|  
|[UpdateAutoUpgradeConfigs Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/updateautoupgradeconfigs-method-in-class-sms_site.md)|Updates configurations for auto-upgrade settings.|  
|[UpdateClientPilotingConfigs Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/updateclientpilotingconfigs-method-in-class-sms_site.md)|Updates the configurations for client piloting settings.|  
|[UpdateConsoleUsageData Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/updateconsoleusagedata-method-in-class-sms_site.md)|Updates console usage data received from console connections.|  
|[UpdateFeatureState Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/updatefeaturestate-method-in-class-sms_site.md)|Updates the enabled/disabled state of a feature.|  
|[VerifyNoLoops Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/verifynoloops-method-in-class-sms_site.md)|Determines whether the parent-child relationship for a given site results in a recursive loop.|  

## Properties  
 `BuildNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Configuration Manager build number. The default value is 0.  

 `Features`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved for internal use.  

 `InstallDir`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Directory in which Configuration Manager was installed. The default value is "".  

 `Mode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Mode of the site. Possible values are:  

|||  
|-|-|  
|1|Replication maintenance.|  
|2|Recovery in progress.|  
|3|Upgrade in progress.|  
|4|Evaluation has expired.|  
|5|Site expansion in progress.|  
|6|Interop mode where there are primary sites, having the same version as the CAS, were not upgraded.|  
|7|Interop mode where there are secondary sites, having the same version as the top-level site server, were not upgraded.|  

 `ReportingSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 Site code for the parent of the current site. The default value is "".  

 `RequestedStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Value indicating a request for secondary site status. Possible values are listed below. The default value is 1001.  

|||  
|-|-|  
|1001|Create a secondary site; the primary site will send down the installation media.|  
|1002|Create a secondary site using the installation media already available on the secondary site.|  
|1003|Secondary site creation has started.|  
|1004|Upgrade a secondary site; the primary site will send down the installation media.|  
|1005|Upgrade a secondary site using the installation media already available on the secondary site.|  
|1006|Secondary site upgrade has started.|  
|1007|Deinstall a secondary site.|  
|1008|Secondary site deinstall has started.|  
|1009|Delete a secondary site.|  
|1010|Secondary site deletion has started.|  
|1011|Recover a secondary site; the primary site will send down the installation media.|  
|1012|Recover a secondary site; the installation media is already available on the secondary site.|  
|1013|Secondary site recovery has started.|  

 Use this property for creating and upgrading a secondary site. Only values preceded by "SEC_REQUEST_" can be set.  

 `SecondarySiteCMUpdateStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Indicates whether the secondary site server has the latest Configuration Manager updates installed from its parent.  

 `ServerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Server name of the site on which Configuration Manager is installed. The default value is "".  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 Three-letter site code for the site. The default value is "".  

 `SiteName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the site. The default value is "".  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Current status of the site. Possible values are listed below. The default value is ACTIVE (1).  

|||  
|-|-|  
|1|ACTIVE|  
|2|PENDING|  
|3|FAILED|  
|4|DELETED|  
|5|UPGRADE|  
|6|Failed to delete or deinstall the secondary site.|  
|7|Failed to upgrade the secondary site.|  
|8|Secondary site recovery is in progress.|  
|9|Failed to recover secondary site.|  

 `TimeZoneInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Site server time zone represented as a Win32 `TIME_ZONE_INFORMATION` structure that is retrieved by the Win32 `GetTimeZoneInformation` function. The default value is "".  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Type of site. Possible values are listed below. The default value is SECONDARY (1).  

|||  
|-|-|  
|1|SECONDARY|  
|2|PRIMARY|  
|4|CAS|  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Complete Configuration Manager version of the current site. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  `SMS_Site` can be used to get the site server name from a known site code. For an example, see [How to Create a PXE Service Point Role](../../../../../develop/osd/how-to-enable-a-pxe-service-point-role.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
