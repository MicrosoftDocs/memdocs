---
title: SMS_G_System_SoftwareUsageData Class
titleSuffix: Configuration Manager
description: Provides a view of raw metering data that combines file and user information with the raw data.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 01100026-63ae-4455-8462-218445b0df11
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_SoftwareUsageData Server WMI Class
The `SMS_G_System_SoftwareUsageData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides a view of raw metering data that combines file and user information with the raw data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_SoftwareUsageData : SMS_G_System  
{  
      String CompanyName;  
      Boolean EndNotCaptured;  
      DateTime EndTimeGMT;  
      DateTime EndTimeLocal;  
      String FileDescription;  
      SInt64 FileID;  
      String FileName;  
      UInt32 FileSize;  
      String FileVersion;  
      Boolean InTSSession;  
      String MeterDataID;  
      UInt32 ProductLanguage;  
      String ProductName;  
      String ProductVersion;  
      UInt32 ResourceID;  
      Boolean StartNotCaptured;  
      DateTime StartTimeGMT;  
      DateTime StartTimeLocal;  
      Boolean StillRunning;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_G_System_SoftwareUsageData` class does not define any methods.  

## Properties  
 `CompanyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the company that made the file, taken from the `Company` property of the file version resources.  

 `EndNotCaptured`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the metering agent could not capture the actual end time of the process.  

 `EndTimeGMT`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The date and time, in Universal Coordinated Time (UTC), when the process stopped running, if `StillRunning` is `false`. If it is `true`, `EndTimeGMT` indicates the time when the data was reported.  

 `EndTimeLocal`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time, in the local time zone of the client, when the process stopped running, if `StillRunning` is `false`. If it is `true`, `EndTimeLocal` indicates the time when the data was reported.  

 `FileDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the metered file, taken from the files version resources.  

 `FileID`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the file that was metered. To find the file information, the application matches this property to the ID in [SMS_ProductFileInfo Server WMI Class](../../../develop/reference/apps/sms_productfileinfo-server-wmi-class.md). To find the rules that caused the file to be metered, the application matches `FileID` to the ID in [SMS_MeteredFiles Server WMI Class](../../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md).  

 `FileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 File name of the metered file if the metering rule matched the file name. If it did not match, but the `OriginalFileName` property of the rule matched the original file name in the files version resources, this property represents the original file name.  

 `FileSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Size of the metered file.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 File version of the metered file, taken from the file version resources.  

 `InTSSession`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the file was used in a Terminal Server session. Set this property to `false` if the file was used in a console session.  

 `MeterDataID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  

 [key]  

 Unique ID of a particular instance of a running process on a computer. A record with this ID is created every time the client reports on the same instance of a running program.  

 `ProductLanguage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Subtype("Locale Id")]  

 Language ID of the metered file, taken from the file version resources.  

 `ProductName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Product name of the metered file, taken from the file version resources. This is not the product name of the rule that caused the file to be metered.  

 `ProductVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Product version of the metered file, taken from the file version resources.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 For this class, this property represents the ID of the computer that executed the metered program. To find the computer information, your application finds the record with the same resource ID in the [SMS_R_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md) class.  

 `StartNotCaptured`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the metering agent could not capture the actual start time of the process.  

 `StartTimeGMT`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time, in Universal Coordinated Time (UTC), when the program started.  

 `StartTimeLocal`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time, in the local time zone of the client, when the program started.  

 `StillRunning`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the program is still running. Set this property to `false` if `EndTime` represents the actual end time of the metered program.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Fully qualified user name of the user of the metered application.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class counts the number of distinct users and computers that used a metered file during a particular interval on a particular site.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
