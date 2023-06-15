---
title: SMS_G_System_UnknownFile Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents an unknown software file, that is, a file that doesn't contain product resource information or isn't related to a software product that contains product resource information.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0e608a1a-e069-4cbe-be18-e2173a6b8563
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_UnknownFile Server WMI Class
The `SMS_G_System_UnknownFile` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an unknown software file, that is, a file that does not contain product resource information or is not related to a software product that contains product resource information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_UnknownFile : SMS_G_System  
{  
     DateTime CreationDate;  
     UInt32 FileCount;  
     SInt64 FileID;  
     String FileDescription;  
     DateTime FileModifiedDate;  
     String FileName;  
     String FilePath;  
     SInt64 FileSize;  
     String FileVersion;  
     DateTime ModifiedDate;  
     UInt32 ProductId;  
     UInt32 ResourceID;   
};  
```  

## Methods  
 The `SMS_G_System_UnknownFile` class does not define any methods.  

## Properties  
 `CreationDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the file was created.  

 `FileCount`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Number of instances of this file found on the client.  

 `FileDescription`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Description from the description resource string. This value is blank for unknown files.  

 `FileID`  
 Data type: **SInt64**  

 Access type: Read/Write  

 Qualifiers: [key]  

 Configuration Manager-supplied ID that uniquely identifies the file.  

 `FileModifiedDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time the file was last modified.  

 `FileName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: [DefaultOrder("ASC")]  

 Name of the file.  

 `FilePath`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Path to the file where it was found on the client computer.  

 `FileSize`  
 Data type: **SInt64**  

 Access type: Read/Write  

 Qualifiers: None  

 Size of the file, in bytes.  

 `FileVersion`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Version from the version resource string. This value is blank for unknown files.  

 `ModifiedDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time the file was last modified.  

 `ProductId`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Although this class contains the same unknown file information that is found in [SMS_G_System_SoftwareFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_softwarefile-server-wmi-class.md), there is no advantage to querying against this class for unknown product files. It is recommended to use `SMS_G_System_SoftwareFile` for all queries involving inventoried files.  

 The Software Inventory Agent collects files identified in the site control file. To identify the files to collect, the agent:  

1.  Queries the site control [SMS_SCI_ClientComp Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) objects for items having the value "Software Inventory Agent" for the `ClientComponentName` property.  

2.  Loops through the embedded property list. When the value for `PropertyName` is "Inventoriable Types", the agent updates the comma-delimited list of file names (including extensions) in the `Value2` property. When the value for `PropertyName` is "Inventory Schedule", the agent updates the interval string in the `Value2` property. For information about creating an interval string, see the example for the [WriteToString Method in Class SMS_ScheduleMethods](../../../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md) method. When the value for `PropertyName` is "Report Options", the agent updates the reporting options value in the `Value` property, specifying at least one reporting option for the software inventory to be collected. The following table lists the reporting options.  

    |Reporting option|Description|  
    |----------------------|-----------------|  
    |Product version information. Bit 0.|Inventories products that contain company and product resource information.|  
    |Files associated with known products. Bit 1.|Inventories files associated with products that contain company and product resource information. For example, Wwintl32.dll is inventoried because it is associated with Microsoft Word.<br /><br /> Set this bit only if the product version information reporting option is selected.|  
    |Files not associated with known products. Bit 2.|Inventories files that do not include company and product resource information (unknown files).|  

3.  For newly added inventory types, adds entries to the following `Path`, `Subdirectories`, and `Exclude` embedded property lists.  

4.  Updates the site control file. For more information, see [About the site control file](../../../../core/understand/about-the-configuration-manager-site-control-file.md).  

> [!NOTE]
>  Collecting inventory information for some files, for example, DLL files, can generate a large volume of network traffic and substantially increase the size of the Configuration Manager database. For this reason, test any changes you make in a test environment before implementing them in a production environment.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)   
 [SMS_G_System_SoftwareFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_softwarefile-server-wmi-class.md)   
 [About the site control file](../../../../core/understand/about-the-configuration-manager-site-control-file.md)
