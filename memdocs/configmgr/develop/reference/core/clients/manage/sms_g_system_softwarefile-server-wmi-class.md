---
title: SMS_G_System_SoftwareFile Class
description: The SMS_G_System_SoftwareFile class is an SMS Provider server class that contains information about all software files that were inventoried on the client computer.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2b64ccf4-9ab2-498a-a4be-dbcecadb1886
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_System_SoftwareFile Server WMI Class
The `SMS_G_System_SoftwareFile` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains information about all software files that were inventoried on the client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_SoftwareFile : SMS_G_System  
{  
     DateTime CreationDate;  
     UInt32 FileCount;  
     String FileDescription;  
     SInt64 FileID;  
     String FileName;  
     String FilePath;  
     SInt64 FileSize;  
     String FileVersion;  
     DateTime ModifiedDate;  
     DateTime FileModifiedDate;  
     UInt32 ProductId;  
     UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_G_System_SoftwareFile` class does not define any methods.  

## Properties  
 `CreationDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 Deprecated. The value is always `null`.  

 `FileCount`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: v  

 Value indicating the file count. This value is always 1 because Configuration Manager tracks individual file paths.  

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

 `FileName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers:  

 [DefaultOrder("ASC")]  

 Name of the file.  

 `FilePath`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Path to the software file location on the client computer.  

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

 The date and time when the record in the database was last modified.  

 `FileModifiedDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time when the file was last modified.  

 `ProductId`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Value that associates the software file with a software product represented by an [SMS_G_System_SoftwareProduct Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_softwareproduct-server-wmi-class.md) object. A value of 0 indicates that the software file is not associated with a known software product, that is, it is an unknown file. Files with a `ProductId` value is 0 are identical to [SMS_G_System_UnknownFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_unknownfile-server-wmi-class.md) objects.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key, ResID(6301), ResDLL("SMS_RXPL.dll")]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class represents both known product files and unknown product files. Known product files contain company and product resource information or are related to known product files. Although you can use this class for queries involving inventoried files, it is preferred to use [SMS_ProductFileInfo Server WMI Class](../../../../../develop/reference/apps/sms_productfileinfo-server-wmi-class.md).  

 Although [SMS_G_System_UnknownFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_unknownfile-server-wmi-class.md) defines the same unknown file information that is found in this class, there is no advantage to querying against `SMS_G_System_UnknownFile` for unknown product files. The following query returns all unknown product files from `SMS_G_System_SoftwareFile`.  

```  
SELECT * FROM SMS_G_System_SoftwareFile  
WHERE ProductId = 0  
```  

 The following query returns all known product files and their product information.  

```  
SELECT * FROM SMS_G_System_SoftwareFile swf  
JOIN SMS_G_System_SoftwareProduct swp ON swf.ProductId = swp.ProductId  
AND swf.ResourceID = swp.ResourceID  
```  

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
 [SMS_G_System_UnknownFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_unknownfile-server-wmi-class.md)   
 [SMS_ProductFileInfo Server WMI Class](../../../../../develop/reference/apps/sms_productfileinfo-server-wmi-class.md)
