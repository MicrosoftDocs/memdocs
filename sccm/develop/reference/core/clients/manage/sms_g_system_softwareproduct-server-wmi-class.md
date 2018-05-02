---
title: "SMS_G_System_SoftwareProduct Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 37d49bb2-4753-4eb8-baad-627151098437
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_G_System_SoftwareProduct Server WMI Class
The `SMS_G_System_SoftwareProduct` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that provides software product information for software files that contain resource strings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_SoftwareProduct : SMS_G_System  
{  
     String CompanyName;  
     UInt32 ProductId;  
     UInt32 ProductLanguage;  
     String ProductName;  
     String ProductVersion;  
     UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_G_System_SoftwareProduct` class does not define any methods.  

## Properties  
 `CompanyName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the software manufacturer taken from the company name resource string. This name can be universally changed by using the rules that are defined in [SMS_SoftwareConversionRules Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_softwareconversionrules-server-wmi-class.md).  

 `ProductId`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 System Center Configuration Manager-supplied ID that uniquely identifies the product. The property links this product with the software file information contained in an [SMS_G_System_SoftwareFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_softwarefile-server-wmi-class.md) object.  

 `ProductLanguage`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [Subtype("Locale Id")]  

 Language taken from the language resource string.  

 `ProductName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers:[DefaultOrder("ASC")]  

 Value of the product name resource string.  

 `ProductVersion`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: none  

 Value of the product version resource string.  

 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The Software Inventory Agent inventories files identified in the site control file. To identify the files to inventory, the agent:  

1.  Queries the site control [SMS_SCI_ClientComp Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) objects for items having the value "Software Inventory Agent" for the `ClientComponentName` property.  

2.  Loops through the embedded property list. When the value for `PropertyName` is "Inventoriable Types", the agent updates the comma-delimited list of file names (including extensions) in the `Value2` property. When the value for `PropertyName` is "Inventory Schedule", the agent updates the interval string in the `Value2` property. For information about creating an interval string, see the example for the [WriteToString Method in Class SMS_ScheduleMethods](../../../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md) method. When the value for `PropertyName` is "Report Options", the agent updates the reporting options value in the `Value` property, specifying at least one reporting option for the software inventory to be collected. The following table lists the reporting options.  

    |Reporting option|Description|  
    |----------------------|-----------------|  
    |Product version information. Bit 0.|Inventories products that contain company and product resource information.|  
    |Files associated with known products. Bit 1.|Inventories files associated with products that contain company and product resource information. For example, Wwintl32.dll is inventoried because it is associated with Microsoft Word.<br /><br /> Set this bit only if the product version information reporting option is selected.|  
    |Files not associated with known products. Bit 2.|Inventories files that do not include company and product resource information (unknown files).|  

3.  For newly added inventory types, adds entries to the following `Path`, `Subdirectories`, and `Exclude` embedded property lists.  

 Updates the site control file. For information about updating the site control file, see [Configuration Manager Site Control File](../../../../../develop/core/understand/site-control-file.md).  

> [!NOTE]
>  Collecting inventory information for some files, for example, DLL files, can generate a large volume of network traffic and substantially increase the size of the System Center Configuration Manager database. For this reason, test any changes you make in a test environment before implementing them in a production environment.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)   
 [SMS_SoftwareConversionRules Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_softwareconversionrules-server-wmi-class.md)   
 [SMS_G_System_SoftwareFile Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_softwarefile-server-wmi-class.md)   
 [Configuration Manager Site Control File](../../../../../develop/core/understand/site-control-file.md)
