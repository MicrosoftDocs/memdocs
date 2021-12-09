---
title: "SMS Provider Fundamentals"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c308fa4a-8d8b-42dc-87ec-f42667e314fd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS Provider Fundamentals in Configuration Manager
You use the SMS Provider to access and modify Configuration Manager data. The SMS Provider is a Windows Management Instrumentation (WMI) provider that can be accessed through either WMI or managed classes.  

## WMI Architecture  
 WMI is designed to function as a middle layer, by serving as a standard interface between management applications and the systems that they manage.  

### WMI Object Model  
 Management applications and scripts work with WMI through the WMI Object Model. The object model defines the programming interface to WMI.  

 For more information about WMI, see [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page).  

 The main elements of the WMI Object Model are shown in the following table:  

|Element|Description|  
|-------------|-----------------|  
|Locator|Used to locate a WMI Service that is running on a local or remote computer.|  
|Service object|Represents an actual connection to a WMI provider. This is the main point of contact to WMI programs.|  
|Objects|A managed object is a logical or physical enterprise component, such as a hard drive, network adapter, database system, operating system, process, or service. A managed object communicates with WMI through a WMI provider.|  
|Events|Used to track changes to WMI objects at run time. Events can be captured as objects and then manipulated in the same ways that any other objects, except that they cannot be changed or saved in WMI.|  
|Properties|Supplies descriptive or operational information about an object. For example, a `Win32_DiskDrive` object includes a property called `InterfaceType`, which might have the value of IDE for your C: drive. Properties can also be set to particular values, if the property is changeable. Setting `InterfaceType` to SCSI is not appropriate, because the only way to change the actual interface type is to replace the controller card. However, you can set a share name to a different value.|  
|Methods|Actions that you can execute on objects. For example, a `Win32_Directory` object includes a method called `Compress()` that allows the contents of a folder to be compressed in the same way as compressing the contents by using the Windows graphical user interface.|  
|Qualifiers|Characteristics of objects, properties, and methods. For example, a qualifier for a property might indicate that it is read-only, or it might list the allowable values for the property. A qualifier for an object might be that it is read-only.|  

## Schema  
 WMI objects are described by classes, providing definitions of their properties, attributes, and other information. These classes are organized into an inheritance hierarchy supporting object associations and grouped by areas of interest, such as networking, applications, and systems. Each area of interest represents a schema, which is a subset of the information that is available about the managed environment.  

 For more information, see the [Schema overview](configuration-manager-schema-overview.md).  

 For information about accessing the SMS Provider using WMI, see [WMI Configuration Manager Provider Fundamentals](../../../develop/core/understand/wmi-configuration-manager-provider-fundamentals.md)  

## WMI and .NET Framework applications  
 Configuration Manager has a .NET Framework library, Microsoft.ConfigurationManager.ManagementProvider, that wraps WMI and allows you to write managed applications.  

 For information about accessing the SMS Provider by using .NET Framework, see [.NET Managed Configuration Manager Provider Fundamentals](../../../develop/core/understand/managed-sms-provider-fundamentals-in-configuration-manager.md)  

 You can also use the .NET Framework WMI management namespace System.Management, but this does not provide any Configuration Manager-specific interfaces. It is, however, the recommended way to use managed code on a Configuration Manager client.

## See also

[SMS Provider fundamentals](sms-provider-fundamentals.md)
