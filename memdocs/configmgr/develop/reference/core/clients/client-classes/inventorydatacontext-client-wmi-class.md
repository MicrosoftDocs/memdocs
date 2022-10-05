---
title: InventoryDataContext Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the InventoryDataContext class is a client WMI class that represents the WMI context qualifiers to be used with inventory client agent WMI queries built from InventoryDataItem Client WMI class objects.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c606c59c-5e3a-468b-b6cd-305ab4bc5fbb
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# InventoryDataContext Client WMI Class
In Configuration Manager, the `InventoryDataContext` class is a client Windows Management Instrumentation (WMI) class that represents the WMI context qualifiers to be used with inventory client agent WMI queries built from [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md) objects. Typically, dynamic instance providers do not require context qualifiers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class InventoryDataContext : SMS_InventoryAgent_EmbeddedObject  
{  
    String Name;  
    String Type;  
    String Value[];  
};  
```  

## Methods  
 The `InventoryDataContext` class does not define any methods.  

## Properties  
 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [realkey]  

 Name of the context qualifier.  

 `Type`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 String representation of the WMI variant data type for the context qualifier (for example, 3 for integer and 8200 for string array).  

 `Value`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Context qualifier value, consistent with the specified data type.  

## Remarks  
 This class allows a generic method to specify context qualifiers for a WMI class query when they are needed. For example, the File System Inventory provider allows context qualifiers for specifying an amount of time to delay between back-to-back file operations. If no context qualifier is specified, there is no delay or throttling of scanning files on the system disk.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)   
 [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md)   
 [FileSystemFile Client WMI Class](../../../../../develop/reference/core/clients/client-classes/filesystemfile-client-wmi-class.md)
