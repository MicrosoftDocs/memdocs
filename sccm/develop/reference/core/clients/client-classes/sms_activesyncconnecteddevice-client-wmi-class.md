---
title: "SMS_ActiveSyncConnectedDevice Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 01eb8a22-12dc-47ae-b6b4-2acde24e6e6a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ActiveSyncConnectedDevice Client WMI Class
The `SMS_ActiveSyncConnectedDevice` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents a device connected to the ActiveSync service.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ActiveSyncConnectedDevice : SMS_Class_Template  
{  
      String DeviceOEMInfo;  
      String DeviceType;  
      String InstalledClientID;  
      String InstalledClientServer;  
      String InstalledClientVersion;  
      String LastSyncTime;  
      String OS_AdditionalInfo;  
      String OS_Build;  
      String OS_Major;  
      String OS_Minor;  
      String OS_Platform;  
      String ProcessorArchitecture;  
      String ProcessorLevel;  
      String ProcessorRevision;  
};  
```  

## Methods  
 The `SMS_ActiveSyncConnectedDevice` class does not define any methods.  

## Properties  
 `DeviceOEMInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  

 [SMS_Report("True"), key]  

 OEM information for the device.  

 `DeviceType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 Type of device.  

 `InstalledClientID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 The ID of the installed client.  

 `InstalledClientServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 The ID of the server for the installed client.  

 `InstalledClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 The version of the installed client.  

 `LastSyncTime`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 The time when the device was last synchronized.  

 `OS_AdditionalInfo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 Additional information about the client operating system.  

 `OS_Build`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True")]  

 The build associated with the client operating system.  

 `OS_Major`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The major version number of the operating system.  

 `OS_Minor`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The minor version number of the operating system.  

 `OS_Platform`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The platform on which the operating system is running.  

 `ProcessorArchitecture`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The architecture for the device processor.  

 `ProcessorLevel`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: SMS_Report("True"), key]  

 The processor level.  

 `ProcessorRevision`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SMS_Report("True"), key]  

 The processor revision.  

## Remarks  
 All properties of this class are marked with qualifiers to indicate that they represent items that are generated dynamically (reported) based on the content of the SMS_def.mof file. For more information, see the `DrillThroughReportPath` property of [SMS_Report Server WMI Class](../../../../../develop/reference/misc/sms_report-server-wmi-class.md).  

## See Also  
 [Device Management Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/device-management-client-wmi-classes.md)   
 [SMS_ActiveSyncService Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_activesyncservice-client-wmi-class.md)
