---
title: SMS_CollectionSettings Class
description: Learn how the SMS_CollectionSettings class is an SMS Provider server class that represents settings for an SMS_Collection Server WMI Class object.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 332629f9-bbd6-4bb1-860b-baa11bce8744
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CollectionSettings Server WMI Class
The `SMS_CollectionSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents settings for an [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object.  

## Syntax  

```  
Class SMS_CollectionSettings : SMS_BaseClass   
{   
      UInt32 ClusterCount;  
      UInt32 ClusterPercentage;  
      UInt32 ClusterTimeout;  
      String CollectionID;   
      UInt32 CollectionVariablePrecedence;   
      SMS_CollectionVariable CollectionVariables[];   
      DateTime LastModificationTime;   
      UInt32 LocaleID;   
      UInt32 PollingInterval;   
      SMS_PowerConfig PowerConfigs[];  
      Boolean PollingIntervalEnabled;   
      String PostAction;  
      String PreAction;  
      UInt32 RebootCountdown;   
      Boolean RebootCountdownEnabled;   
      UInt32 RebootCountdownFinalWindow;   
      SMS_ServiceWindow ServiceWindows[];   
      String SourceSite;   
      UInt32 UseCluster;   
      UInt32 UseClusterPercentage;  
};  
```  

## Methods  
 The `SMS_CollectionSettings` class does not define any methods.  

## Properties  
 `ClusterCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of computers that can be offline in a cluster. The default value is 1.  

 `ClusterPercentage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Percent of computers that can be offline in a cluster. The default value is 50.  

 `ClusterTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Timeout for the scripts. The default value is 600.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, read]  

 A unique key that maps to the parent collection. The default value is "".  

 `CollectionVariablePrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Precedence that is used for conflict resolution. The default value is 1.  

 `CollectionVariables`  
 Data type: `SMS_CollectionVariable` Array  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 SMS_CollectionVariable Server WMI Class objects representing collection variables.  

 `LastModificationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last modification date and time for collection settings.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Locale ID to use in converting the localized name and description. The default value is 1033 (U.S. English).  

 You can get the locale for the Configuration Manager installation from the [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)`LocaleID` property.  

 `PostAction`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The Windows PowerShell script to run after an update deployment.  

 `PreAction`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The Windows PowerShell script to run before an update deployment.  

 `PollingInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Policy polling interval, in minutes. The default value is 5.  

 `PollingIntervalEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the polling interval is enabled. The default value is `false`.  

 `PowerConfigs`  
 Data type: `SMS_PowerConfig` Array  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 SMS_PowerConfig Server WMI Class objects representing the power configuration for a specific collection.  

 `RebootCountdown`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Reboot countdown. The default value is 5.  

 `RebootCountdownEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if reboot countdown is enabled. The default value is `false`.  

 `RebootCountdownFinalWindow`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The point at which the final maintenance window is shown for the reboot countdown. The default value is 5.  

 `ServiceWindows`  
 Data type: `SMS_ServiceWindow` Array  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 [SMS_ServiceWindow Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_servicewindow-server-wmi-class.md) objects representing maintenance windows that are used for making the collection settings.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [SizeLimit("3"), Not_null]  

 Site code of the source site.  

 `UseCluster`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 A non-zero value indicates that the  collection is being used as a cluster. The default value is 0.  

 `UseClusterPercentage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether to use the ClusterPercentage property. The default value is 1.  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
